---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-cs
title: ObjectDataSource ile verileri önbelleğe alma (C#) | Microsoft Docs
author: rick-anderson
description: Önbelleğe alma, yavaş ve hızlı bir Web uygulaması arasındaki farkı ifade edebilir. Bu öğretici, ASP.NET içinde önbelleğe alma hakkında ayrıntılı bir bakış sunan ilk dört
ms.author: riande
ms.date: 05/30/2007
ms.assetid: bd87413c-8160-4520-a8a2-43b555c4183a
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: c9883314d6153b9816d9bad2a281ab3c0a816448
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524257"
---
# <a name="caching-data-with-the-objectdatasource-c"></a>ObjectDataSource ile Verileri Önbelleğe Alma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_CS.exe) veya [PDF 'yi indirin](caching-data-with-the-objectdatasource-cs/_static/datatutorial58cs1.pdf)

> Önbelleğe alma, yavaş ve hızlı bir Web uygulaması arasındaki farkı ifade edebilir. Bu öğretici, ASP.NET ' de önbelleğe alma hakkında ayrıntılı bir bakış sunan ilk dört ilkidir. Önbelleğe alma işleminin temel kavramlarını ve ObjectDataSource denetimi aracılığıyla Sunu katmanına nasıl önbelleğe alınacağını öğrenin.

## <a name="introduction"></a>Giriş

Bilgisayar bilimi ' nde, *önbelleğe alma* , bir kopyasını elde etmek ve bir kopyasını daha hızlı bir konuma depolamak için pahalı olan verileri veya bilgileri alma işlemidir. Veri odaklı uygulamalar için büyük ve karmaşık sorgular genellikle uygulama yürütme zamanının çoğunu kullanır. Bu tür bir uygulama performansı daha sonra, uygulama s belleğindeki pahalı Veritabanı sorgularının sonuçları depolanarak genellikle iyileşebilirler.

ASP.NET 2,0, çeşitli önbelleğe alma seçenekleri sunar. Tüm Web sayfası veya Kullanıcı denetimi işlenmiş işaretleme, *çıktı önbelleği*aracılığıyla önbelleğe alınabilir. ObjectDataSource ve SqlDataSource denetimleri, önbelleğe alma yeteneklerini de sağlar ve bu sayede verilerin Denetim düzeyinde önbelleğe alınmasına izin verir. Ve ASP.NET s *veri önbelleği* , sayfa geliştiricilerinin nesneleri programlı bir şekilde önbelleğe almasını sağlayan zengin bir önbelleğe alma API 'si sağlar. Bu öğreticide ve sonraki üç adımda, ObjectDataSource s önbelleğe alma özelliklerinin yanı sıra veri önbelleğinin kullanılması anlatılmaktadır. Ayrıca, başlangıçta uygulama genelinde verilerin nasıl önbelleğe alınacağını ve SQL önbellek bağımlılıklarının kullanımı aracılığıyla önbelleğe alınmış verilerin nasıl güncel tutulacağını araştıracağız. Bu öğreticiler çıktı önbelleğe almayı araştırmaz. Çıktı önbelleğe alma hakkında ayrıntılı bir bakış için bkz. [ASP.NET 2,0 'de çıktı önbelleği](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx).

Önbelleğe alma, veri erişim katmanından sunum katmanı üzerinden yukarı, mimaride herhangi bir yerde uygulanabilir. Bu öğreticide, ObjectDataSource denetimi aracılığıyla sunum katmanına önbelleğe alma uygulama bölümüne bakacağız. Sonraki öğreticide Iş mantığı katmanında önbelleğe alma verilerini inceleyeceğiz.

## <a name="key-caching-concepts"></a>Anahtar önbelleğe alma kavramları

Önbelleğe alma, bir kopyasının oluşturulması ve bir kopyasını daha verimli bir yerde daha etkin erişilebilen bir konuma depolayarak bir uygulamanın genel performansını ve ölçeklenebilirliğini önemli ölçüde iyileştirebilir. Önbellek gerçek, temel alınan verilerin yalnızca bir kopyasını içerdiğinden, temel alınan veriler değişirse *eski veya eski*olabilir. Bu, bir sayfa geliştiricisi, önbellek öğesinin önbellekten *çıkarılabileceği* ölçütü belirtebileceği, aşağıdakilerden birini kullanarak:

- **Zamana dayalı ölçütler** mutlak veya kayan bir süre için önbelleğe bir öğe eklenebilir. Örneğin, bir sayfa geliştiricisi bir süreyi, deyin, 60 saniye olarak gösterebilir. Mutlak bir süre ile, önbelleğe alınan öğe, ne sıklıkta erişildiğine bakmaksızın önbelleğe eklendikten sonra 60 saniye çıkarıldı. Kayan bir süre ile, önbelleğe alınmış öğe son erişimden sonra 60 saniye çıkarıldı.
- **Bağımlılık tabanlı ölçütler** , bir bağımlılık, önbelleğe eklendiğinde bir öğe ile ilişkilendirilebilir. Öğe bağımlılığının değişiklik yaptığı değişiklikler önbellekten çıkarıldı. Bağımlılık bir dosya, başka bir önbellek öğesi veya ikisinin bir birleşimi olabilir. ASP.NET 2,0 Ayrıca, geliştiricilerin önbelleğe bir öğe eklemesini ve temel alınan veritabanı verileri değiştiğinde çıkarılmasını sağlayan SQL önbellek bağımlılıklarına izin verir. SQL önbellek bağımlılıklarını yakında SQL [önbellek bağımlılıkları](using-sql-cache-dependencies-cs.md) öğreticisini kullanarak inceleyeceğiz.

Belirtilen çıkarma ölçütlerine bakılmaksızın, zaman tabanlı veya bağımlılık tabanlı ölçütler karşılanmadan önbellekteki bir öğe *atılabilir* . Önbellek kapasiteye ulaştıysa, yeni bir öğe eklenebilmesi için mevcut öğelerin kaldırılması gerekir. Sonuç olarak, önbelleğe alınmış verilerle programlı olarak çalışırken, her zaman önbelleğe alınan verilerin mevcut olabileceğini varsaymanız gerekir. Sonraki öğreticimizde, *mimarideki verileri, mimaride önbelleğe alma*sırasında kullanarak önbellekteki verilere erişirken kullanılacak düzene bakacağız.

Önbelleğe alma, bir uygulamadan daha fazla performans sağlayan ekonomik bir yol sağlar. [Steven Smith](http://aspadvice.com/blogs/ssmith/) , makalede [ASP.NET önbelleğe alma: teknikler ve en iyi uygulamalar](https://msdn.microsoft.com/library/aa478965.aspx):

Önbelleğe alma, çok fazla zaman ve analiz gerekmeden yeterince iyi performans sağlamak için iyi bir yoldur. Bellek, bu nedenle, kodunuzu veya veritabanınızı en iyi duruma getirmeye çalışan bir gün veya hafta harcamak yerine çıktıyı 30 saniye boyunca önbelleğe alarak ihtiyacınız olan performansı alabilir, önbelleğe alma çözümünü (30 saniyelik eski verilerin Tamam olduğu varsayıldığında) ve üzerinde geçiş yapabilirsiniz. Sonuç olarak, kötü tasarım büyük olasılıkla sizi sizin için doğru şekilde tasarlayacaktır, böylece uygulamalarınızı doğru bir şekilde tasarlamaya çalışırsınız. Ancak bugün yeterince iyi performans almanız gerekiyorsa, önbelleğe alma işlemi harika bir [yaklaşım] olabilir, bu da uygulamanızı daha sonraki bir tarihte yeniden düzenlemeniz için zaman satın alabilirsiniz.

Önbelleğe alma işlemi, gelişmiş performans iyileştirmeleri sağlayabilse de, gerçek zamanlı, sık güncelleştirilen verileri kullanan uygulamalarla veya hatta daha fazla eski verilerin kabul edilemez olduğu durumlarda olduğu gibi tüm durumlarda geçerli değildir. Ancak uygulamaların çoğunluğu için önbelleğe alma kullanılmalıdır. ASP.NET 2,0 ' de önbelleğe alma hakkında daha fazla arka plan için [ASP.NET 2,0 hızlı başlangıç öğreticilerinin](https://quickstarts.asp.net/QuickStartv20/aspnet/) [performans için önbelleğe alma](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx) bölümüne bakın.

## <a name="step-1-creating-the-caching-web-pages"></a>1\. Adım: önbelleğe alma Web sayfalarını oluşturma

ObjectDataSource 'un önbelleğe alma özelliklerinin araştırmasına başlamadan önce, Web sitesi projemizdeki Bu öğretici ve sonraki üç için gereken ASP.NET sayfalarını oluşturmak için ilk olarak bir süre sürer. `Caching`adlı yeni bir klasör ekleyerek başlayın. Ardından, aşağıdaki ASP.NET sayfalarını bu klasöre ekleyerek her bir sayfayı `Site.master` ana sayfasıyla ilişkilendirdiğinizden emin olun:

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`

![Önbelleğe alma ile Ilgili öğreticiler için ASP.NET sayfaları ekleyin](caching-data-with-the-objectdatasource-cs/_static/image1.png)

**Şekil 1**: önbelleğe alma Ile ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `Caching` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[![Şekil 2: SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx 'e ekleme](caching-data-with-the-objectdatasource-cs/_static/image3.png)](caching-data-with-the-objectdatasource-cs/_static/image2.png)

**Şekil 2**: Şekil 2: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` 'e ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image4.png))

Son olarak, bu sayfaları `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, Ikili verilerle çalışmayı tamamladıktan sonra aşağıdaki biçimlendirmeyi ekleyin `<siteMapNode>`:

[!code-xml[Main](caching-data-with-the-objectdatasource-cs/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık önbelleğe alma öğreticilerinin öğelerini içerir.

![Site Haritası artık önbelleğe alma öğreticilerinin girdilerini Içerir](caching-data-with-the-objectdatasource-cs/_static/image5.png)

**Şekil 3**: site haritası artık önbelleğe alma öğreticilerinin girdilerini içerir

## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>2\. Adım: bir Web sayfasında ürünlerin listesini görüntüleme

Bu öğreticide, ObjectDataSource denetimi yerleşik önbelleğe alma özelliklerinin nasıl kullanılacağı açıklanır. Bu özelliklere bakmadan önce, ilk olarak bir sayfanın çalışması gerekir. `ProductsBLL` sınıfından bir ObjectDataSource tarafından alınan ürün bilgilerini listelemek için GridView kullanan bir Web sayfası oluşturalım.

`Caching` klasöründeki `ObjectDataSource.aspx` sayfasını açarak başlayın. Araç kutusundan bir GridView 'u tasarımcı üzerine sürükleyin, `ID` özelliğini `Products`olarak ayarlayın ve akıllı etiketinden, `ProductsDataSource`adlı yeni bir ObjectDataSource denetimine bağlamayı seçin. ObjectDataSource 'ı `ProductsBLL` sınıfıyla çalışacak şekilde yapılandırın.

[![, ObjectDataSource 'ı ProductsBLL sınıfını kullanacak şekilde yapılandırma](caching-data-with-the-objectdatasource-cs/_static/image7.png)](caching-data-with-the-objectdatasource-cs/_static/image6.png)

**Şekil 4**: ObjectDataSource 'ı `ProductsBLL` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image8.png))

Bu sayfa için, ObjectDataSource 'da önbelleğe alınan veriler GridView s arabirimi aracılığıyla değiştirildiğinde ne olduğunu inceleyebileceğiniz şekilde, s için düzenlenebilir bir GridView oluşturalım. Seç sekmesinde açılan listeyi varsayılan olarak ayarlayın, `GetProducts()`, ancak GÜNCELLEŞTIR sekmesindeki seçili öğeyi, giriş parametreleri olarak `productName`, `unitPrice`ve `productID` kabul eden `UpdateProduct` aşırı yüklemeye değiştirin.

[![GÜNCELLEŞTIRME sekmesi açılan listesini uygun UpdateProduct aşırı yüküne ayarla](caching-data-with-the-objectdatasource-cs/_static/image10.png)](caching-data-with-the-objectdatasource-cs/_static/image9.png)

**Şekil 5**: güncelleştirme sekmesi s açılan listesini uygun `UpdateProduct` aşırı yüklemeye ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image11.png))

Son olarak, INSERT ve DELETE sekmelerindeki açılan listeleri (yok) olarak ayarlayın ve son ' a tıklayın. Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra Visual Studio, ObjectDataSource `OldValuesParameterFormatString` özelliğini `original_{0}`olarak ayarlar. Veri öğreticisini [ekleme, güncelleştirme ve silmeye genel bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) konusunda açıklandığı gibi, güncelleştirme iş akışınız hata olmadan devam edebilmesi için, bu özelliğin bildirime dayalı sözdiziminden kaldırılması veya varsayılan değerine (`{0}`) yeniden ayarlanması gerekir.

Ayrıca, sihirbazın tamamlanması, her ürün veri alanı için GridView 'a bir alan ekler. `ProductName`, `CategoryName`ve `UnitPrice` BoundFields hariç tümünü kaldırın. Ardından, bu BoundFields 'in her birinin `HeaderText` özelliklerini sırasıyla ürün, kategori ve fiyat olarak güncelleştirin. `ProductName` alanı gerekli olduğundan, BoundField öğesini TemplateField öğesine dönüştürün ve `EditItemTemplate`bir RequiredFieldValidator ekleyin. Benzer şekilde, `UnitPrice` BoundField öğesini TemplateField 'a dönüştürün ve Kullanıcı tarafından girilen değerin sıfırdan büyük veya sıfıra eşit geçerli bir para birimi değeri olduğundan emin olmak için bir CompareValidator ekleyin. Bu değişikliklere ek olarak, `UnitPrice` değerini sağa hizalamak veya `UnitPrice` metnin biçimlendirmesini salt okunurdur ve Düzenle arabirimlerinde belirtmek gibi herhangi bir Aesthetic Characteristics değişikliğini gerçekleştirmeye başlayabilirsiniz.

GridView s akıllı etiketinde düzenleme etkinleştir onay kutusunu işaretleyerek GridView 'ı düzenlenebilir hale getirin. Ayrıca, Sayfalamayı Etkinleştir ve sıralamayı etkinleştir onay kutularını işaretleyin.

> [!NOTE]
> GridView s Editing arabirimini nasıl özelleştireceğinizi gözden geçirmeniz gerekiyor mu? Bu durumda, [veri değiştirme arabirimi](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) öğreticisini özelleştirmeye geri bakın.

[Düzen, sıralama ve sayfalama için GridView desteğini etkinleştirmek ![](caching-data-with-the-objectdatasource-cs/_static/image13.png)](caching-data-with-the-objectdatasource-cs/_static/image12.png)

**Şekil 6**: düzen, sıralama ve sayfalama Için GridView desteğini etkinleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image14.png))

Bu GridView değişikliklerini yaptıktan sonra, GridView ve ObjectDataSource 'un bildirim temelli işaretlemesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](caching-data-with-the-objectdatasource-cs/samples/sample2.aspx)]

Şekil 7 ' de gösterildiği gibi, düzenlenebilir GridView veritabanındaki her bir ürünün adını, kategorisini ve fiyatını listeler. En kısa süre içinde sonuçları sıralayın, bu işlem içindeki sayfaları düzenleyin ve bir kaydı düzenleyin.

[Her ürün adı, kategori ve fiyat ![sıralanabilir, disk belleğine alınabilir, düzenlenebilir bir GridView 'da listelenmiştir](caching-data-with-the-objectdatasource-cs/_static/image16.png)](caching-data-with-the-objectdatasource-cs/_static/image15.png)

**Şekil 7**: her ürün adı, kategori ve fiyat sıralanabilir, disk belleğine alınan, düzenlenebilir bir GridView 'da listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image17.png))

## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>3\. Adım: ObjectDataSource 'un verileri ne zaman Istediğini Inceleme

GridView `Products`, `ProductsDataSource` ObjectDataSource 'un `Select` yöntemini çağırarak verileri görüntülenecek şekilde alır. Bu ObjectDataSource, Iş mantığı katmanı s `ProductsBLL` sınıfının bir örneğini oluşturur ve `GetProducts()` yöntemini çağırır ve bu da veri erişim katmanı s `ProductsTableAdapter` s `GetProducts()` yöntemini çağırır. DAL yöntemi, Northwind veritabanına bağlanır ve yapılandırılmış `SELECT` sorgusunu yayınlar. Bu veriler daha sonra DAL olarak döndürülür ve bir `NorthwindDataTable`. DataTable nesnesi BLL 'e döndürülür. Bu, bunu GridView 'a döndüren ObjectDataSource öğesine döndürür. GridView daha sonra DataTable 'daki her bir `DataRow` için bir `GridViewRow` nesnesi oluşturur ve her `GridViewRow` sonunda istemciye döndürülen ve ziyaretçi tarayıcısı üzerinde görüntülenen HTML 'de işlenir.

Bu olay dizisi her biri ve GridView 'un temel alınan verilerine bağlanması gereken her seferinde oluşur. Sayfa ilk kez ziyaret edildiğinde, bir veri sayfasından diğerine geçiş yaparken, GridView sıralandığında veya GridView s verilerini yerleşik düzenleme veya silme arabirimleri aracılığıyla değiştirirken meydana gelir. GridView s görünüm durumu devre dışıysa, GridView her bir ve her geri göndermede de yeniden bağlanacaktır. GridView Ayrıca `DataBind()` yöntemi çağırarak verilerine açıkça yeniden bağlanabilir.

Verilerin veritabanından alındığı sıklığı tam olarak görmek için, verilerin ne zaman yeniden alındığını belirten bir ileti görüntülenmesini sağlayın. `ODSEvents`adlı GridView 'un üstüne bir etiket Web denetimi ekleyin. `Text` özelliğini temizleyin ve `EnableViewState` özelliğini `false`olarak ayarlayın. Etiketin altına bir Button Web Control ekleyin ve `Text` özelliğini postback olarak ayarlayın.

[GridView 'un üzerindeki sayfaya bir etiket ve düğme eklemek ![](caching-data-with-the-objectdatasource-cs/_static/image19.png)](caching-data-with-the-objectdatasource-cs/_static/image18.png)

**Şekil 8**: GridView 'un üzerindeki sayfaya bir etiket ve düğme ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image20.png))

Veri erişimi iş akışı sırasında, ObjectDataSource `Selecting` olayı temel alınan nesne oluşturulmadan ve yapılandırılan Yöntem çağrılmadan önce ateşlenir. Bu olay için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](caching-data-with-the-objectdatasource-cs/samples/sample3.cs)]

ObjectDataSource her bir veri için mimariye bir istek yaptığında, etiket tetiklenen olayı seçen metin görüntülenir.

Bu sayfayı bir tarayıcıda ziyaret edin. Sayfa ilk kez ziyaret edildiğinde, tetiklenen olayı seçen metin gösterilir. Geri gönder düğmesine tıklayın ve metnin kaybolduğunu unutmayın (GridView s `EnableViewState` özelliğinin `true`, varsayılan) olarak ayarlandığı varsayılır. Bunun nedeni, geri göndermede GridView 'un görünüm durumundan yeniden yapılandırılmış olması ve bu nedenle verileri için ObjectDataSource 'e geri gönderilmesi. Ancak verileri sıralama, sayfalama veya düzenlemenin yanı sıra GridView 'un veri kaynağına yeniden bağlanmasına neden olur ve bu nedenle olay harekete geçen metin seçimi yeniden belirir.

[GridView, veri kaynağına her bağlandığında ![tetiklenen olay seçildiğinde görüntülenir](caching-data-with-the-objectdatasource-cs/_static/image22.png)](caching-data-with-the-objectdatasource-cs/_static/image21.png)

**Şekil 9**: GridView 'un veri kaynağına yeniden bağlanması durumunda tetiklenen olayı seçme görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image23.png))

[Geri gönderme düğmesine tıklamak ![GridView 'un görünüm durumundan yeniden oluşturulmasına neden olur](caching-data-with-the-objectdatasource-cs/_static/image25.png)](caching-data-with-the-objectdatasource-cs/_static/image24.png)

**Şekil 10**: geri gönderme düğmesine tıklamak GridView 'un görünüm durumundan yeniden oluşturulmasına neden olur ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image26.png))

Verilerin her sayfalanışında veya sıralandığında veritabanı verilerinin alınması beklenebilir görünebilir. Bu yana, varsayılan sayfalama 'yı kullanmaya başladıktan sonra, ilk sayfa görüntülenirken ObjectDataSource tüm kayıtları almıştır. GridView sıralama ve sayfalama desteği sağlamasa bile, sayfa her kullanıcı tarafından ilk kez ziyaret edildiğinde (ve Görünüm durumu devre dışıysa her geri göndermede) verilerin veritabanından alınması gerekir. Ancak GridView tüm kullanıcılar için aynı verileri gösteriyorsa, bu ek veritabanı istekleri gereksiz olur. `GetProducts()` yönteminden döndürülen sonuçları önbelleğe alma ve GridView 'i bu önbelleğe alınmış sonuçlara bağlama.

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>4\. Adım: ObjectDataSource kullanarak verileri önbelleğe alma

Yalnızca birkaç özelliği ayarlayarak, ObjectDataSource, alınan verilerini ASP.NET veri önbelleğinde otomatik olarak önbelleğe almak üzere yapılandırılabilir. Aşağıdaki liste, ObjectDataSource 'un önbellekte ilgili özelliklerini özetler:

- Önbelleğe almayı etkinleştirmek için [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx) 'nin `true` olarak ayarlanması gerekir. Varsayılan, `false` değeridir.
- [CacheDuration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx) , verilerin önbelleğe alınma süresi (saniye cinsinden). Varsayılan değer, 0'dur. ObjectDataSource yalnızca `EnableCaching` `true` ve `CacheDuration` sıfırdan büyük bir değere ayarlandıysa verileri önbelleğe alacak.
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx) , `Absolute` veya `Sliding`olarak ayarlanabilir. `Absolute`, ObjectDataSource `CacheDuration` saniye boyunca alınan verilerini önbelleğe alır; `Sliding`, verilerin süresi yalnızca `CacheDuration` saniye boyunca erişilmedi. Varsayılan, `Absolute` değeridir.
- [CacheKeyDependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx) bu özelliği, ObjectDataSource s önbellek girişlerini varolan bir önbellek bağımlılığı ile ilişkilendirmek için kullanın. ObjectDataSource 'un veri girişleri, ilişkili `CacheKeyDependency`süresi dolduğunda önbellekten erken çıkartık olabilir. Bu özellik en yaygın olarak SQL önbellek bağımlılıkları öğreticisini [kullanarak](using-sql-cache-dependencies-cs.md) keşfedediğimiz bir konu olan ObjectDataSource s Cache ile SQL önbellek bağımlılığını ilişkilendirmek için kullanılır.

`ProductsDataSource` ObjectDataSource 'ı, verileri mutlak ölçekte 30 saniye önbellekte önbelleğe almak üzere yapılandıralım. ObjectDataSource `EnableCaching` özelliğini `true` ve `CacheDuration` özelliğini 30 olarak ayarlayın. `CacheExpirationPolicy` özelliğini varsayılan, `Absolute`olarak bırakın.

[![, verileri 30 saniye önbellekte önbelleğe almak için yapılandırın](caching-data-with-the-objectdatasource-cs/_static/image28.png)](caching-data-with-the-objectdatasource-cs/_static/image27.png)

**Şekil 11**: ObjectDataSource 'ı verileri 30 saniye önbellekte önbelleğe almak üzere yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-with-the-objectdatasource-cs/_static/image29.png))

Değişikliklerinizi kaydedin ve bu sayfayı bir tarayıcıda yeniden ziyaret edin. İlk olarak veri önbellekte olmadığında, sayfayı ilk kez ziyaret ettiğinizde başlatılan olay seçme metni görüntülenir. Ancak geri gönderme düğmesine tıklanarak, sıralama, sayfalama veya Düzenle ya da Iptal düğmelerini tıklatmak ile tetiklenen sonraki geri göndermeler, başlatılan olay harekete geçirilmiş metni *yeniden görüntülemez* . Bunun nedeni, `Selecting` olayının yalnızca ObjectDataSource temel nesnesinden verileri aldığında harekete geçirilir; veriler veri önbelleğinden çekilmezse `Selecting` olay harekete geçmeyecektir.

30 saniye sonra, veriler önbellekten çıkarılacaktır. `Insert`, `Update`veya `Delete` yöntemleri çağrılırsa, veriler önbellekten de çıkartılecektir. Sonuç olarak, 30 saniye geçtikten sonra veya güncelleştirme düğmesine tıklandıktan sonra, sıralama, sayfalama veya Düzenle ya da Iptal düğmelerini tıklatmak, ObjectDataSource 'un verileri temel nesnesinden almasını sağlar ve bu da `Selecting` olay tetiklendiğinde çalıştırılan olayı Seçme metnini görüntüler. Döndürülen bu sonuçlar veri önbelleğine geri yerleştirilir.

> [!NOTE]
> Çalışan olay harekete geçen metni sık sık görürseniz, ObjectDataSource 'un önbelleğe alınmış verilerle çalışmasını bekleseniz bile, bu durum Bellek kısıtlamalarından kaynaklanıyor olabilir. Yeterli boş bellek yoksa, ObjectDataSource tarafından önbelleğe eklenen veriler de atılabilir. ObjectDataSource, verileri doğru önbelleğe alma veya yalnızca verileri önbelleğe alma gibi görünmesine gerek yoksa belleği boşaltmak için bazı uygulamaları kapatın ve yeniden deneyin.

Şekil 12, ObjectDataSource 'un önbelleğe alma iş akışını gösterir. Ekranda seçme olayı harekete geçirildiğinde metin görüntülendiğinde, verilerin önbellekte olmaması ve temel alınan nesneden alınması gerekiyordu. Ancak bu metin eksik olduğunda, veriler önbellekten kullanılabilir olduğundan,. Veriler önbellekten döndürüldüğünde, temel alınan nesneye hiçbir çağrı yapılmaz ve bu nedenle veritabanı sorgusu yürütülmez.

![ObjectDataSource verileri veri önbelleğinden depolar ve alır](caching-data-with-the-objectdatasource-cs/_static/image30.png)

**Şekil 12**: ObjectDataSource, verileri veri önbelleğinden depolar ve alır

Her bir ASP.NET uygulamasının, tüm sayfalar ve ziyaretçiler genelinde paylaştığı kendi veri önbelleği örneği vardır. Diğer bir deyişle, ObjectDataSource tarafından veri önbelleğinde depolanan veriler aynı şekilde sayfayı ziyaret eden tüm kullanıcılar arasında paylaşılır. Bunu doğrulamak için `ObjectDataSource.aspx` sayfasını bir tarayıcıda açın. Sayfa ilk kez ziyaret edildiğinde, başlatılan olayı seçme metni görüntülenir (önceki testlerin önbelleğine eklenen verilerin şu anda çıkarıldığını varsayarak). İkinci bir tarayıcı örneği açın ve ilk tarayıcı örneğinden ikincisine URL 'YI kopyalayın ve yapıştırın. İkinci tarayıcı örneğinde, ilk olarak aynı önbelleğe alınmış verileri kullandığından, olay harekete geçen metin seçme metni gösterilmez.

Alınan veriler önbelleğe eklenirken, ObjectDataSource, `CacheDuration` ve `CacheExpirationPolicy` özellik değerlerini içeren bir önbellek anahtarı değeri kullanır; [`TypeName` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx) Ile belirtilen ObjectDataSource tarafından kullanılan temeldeki iş nesnesinin türü (`ProductsBLL`, bu örnekte); `SelectMethod` özelliğinin değeri ve `SelectParameters` koleksiyonundaki parametrelerin adı ve değerleri; ve `StartRowIndex` ve `MaximumRows` özelliklerinin, [Özel sayfalama](../paging-and-sorting/paging-and-sorting-report-data-cs.md) uygularken kullanılan değerleri.

Bu özelliklerin bir birleşimi olarak önbellek anahtarı değerinin oluşturulması, bu değerler değiştikçe benzersiz bir önbellek girişi sağlar. Örneğin, geçmiş öğreticilerde, belirtilen bir kategori için tüm ürünleri döndüren `ProductsBLL` sınıf s `GetProductsByCategoryID(categoryID)`kullanmaya baktık. Tek bir kullanıcı sayfaya gelebilir ve 1 `CategoryID` olan meşruleri görüntüleyebilir. ObjectDataSource, `SelectParameters` değerleri dikkate almadan sonuçlarını önbelleğe alıyorsa, içgörüler ürünleri önbellekte olduğu sürece, başka bir kullanıcı da sayfaya geldiğinde, büyük/küçük ürünler yerine önbelleğe alınmış içecek ürünlerini görürler. `SelectParameters`değerleri de dahil olmak üzere bu özelliklere göre önbellek anahtarını değiştirerek, ObjectDataSource, içecek ve koşullu kaynaklar için ayrı bir önbellek girişi tutar.

## <a name="stale-data-concerns"></a>Eski veri konuları

`Insert`, `Update`veya `Delete` yöntemlerinin herhangi biri çağrıldığında, ObjectDataSource öğeleri önbellekten otomatik olarak çıkarır. Bu, veriler sayfa aracılığıyla değiştirildiğinde önbellek girişlerini temizleyerek eski verilere karşı korumaya yardımcı olur. Ancak, önbelleğe alma kullanan bir ObjectDataSource, eski verileri görüntülemeye devam etmek için mümkündür. En basit durumda, bunun nedeni doğrudan veritabanı içinde değişen veri olabilir. Belki de bir veritabanı Yöneticisi veritabanındaki bazı kayıtları değiştiren bir betiği çalıştırdı.

Bu senaryo, daha hafif bir şekilde katlamayı de kaldırır. ObjectDataSource, veri değiştirme yöntemlerinden biri çağrıldığında öğeleri önbellekten çıkarlarken, kaldırılan önbelleğe alınmış öğeler, özellik değerlerinin (`CacheDuration`, `TypeName`, `SelectMethod`vb.) belirli bir birleşimine yöneliktir. Farklı `SelectMethods` veya `SelectParameters`kullanan, ancak yine de aynı verileri güncelleştirebilecek iki ObjectDataSources varsa, bir ObjectDataSource bir satırı güncelleştirebilir ve kendi önbellek girişlerini geçersiz kılabilir, ancak ikinci ObjectDataSource için karşılık gelen satır, hala önbelleğe alınmış olarak sunulur. Bu işlevi gösteren sayfalar oluşturmanızı teşvik ediyorum. Verilerini önbelleğe alma kullanan bir ObjectDataSource 'tan alıp `ProductsBLL` sınıf s `GetProducts()` yönteminden veri almak üzere yapılandırılmış bir düzenlenebilir GridView görüntüleyen bir sayfa oluşturun. Bu sayfaya (veya başka bir tane) başka bir düzenlenebilir GridView ve ObjectDataSource ekleyin, ancak bu ikinci ObjectDataSource için `GetProductsByCategoryID(categoryID)` yöntemini kullanın. İki ObjectDataSources `SelectMethod` özellikleri farklı olduğundan, bunların her biri kendi önbelleğe alınmış değerlerine sahiptir. Bir ürünü tek bir kılavuzda düzenlerseniz, daha sonra verileri diğer kılavuza geri bağladığınızda (sayfalama, sıralama vb.), yine de eski, önbelleğe alınmış verilere sahip olur ve diğer kılavuzdan yapılan değişikliği yansıtmaz.

Kısacası, yalnızca eski verilerin potansiyelini sağlamak istiyorsanız zaman tabanlı expiries kullanın ve verilerin yeniliği önemli olan senaryolar için daha kısa expiries kullanın. Eski veriler kabul edilebilir değilse, ya da SQL önbellek bağımlılıklarını kullanın veya (yeniden önbelleğe aldığınız veritabanı verileri olduğu varsayılarak). Gelecek bir öğreticide SQL önbellek bağımlılıklarını araştıracağız.

## <a name="summary"></a>Özet

Bu öğreticide, ObjectDataSource 'ın yerleşik önbelleğe alma yeteneklerini inceliyoruz. Yalnızca birkaç özelliği ayarlayarak, ObjectDataSource 'a belirtilen `SelectMethod` döndürülen sonuçları ASP.NET veri önbelleğine önbelleğe almak için talimat vereceğiz. `CacheDuration` ve `CacheExpirationPolicy` özellikleri, öğenin önbelleğe alındığı süreyi ve mutlak veya kayan bir süre sonu olup olmadığını gösterir. `CacheKeyDependency` özelliği, tüm ObjectDataSource 'lar önbellek girdilerini varolan bir önbellek bağımlılığı ile ilişkilendirir. Bu, zaman tabanlı süre sonuna ulaşılmadan önce ObjectDataSource 'un girişlerini önbellekten çıkarmak için kullanılabilir ve genellikle SQL önbellek bağımlılıklarıyla birlikte kullanılır.

ObjectDataSource, değerlerini veri önbelleğine yalnızca önbelleğe aldığından, ObjectDataSource 'ın yerleşik işlevselliğini programlı bir şekilde çoğaltabiliriz. Bu, ObjectDataSource bu işlevselliği kutudan çıkar, ancak bir mimarinin ayrı bir katmanında önbelleğe alma özelliği uygulayabiliriz. Bunu yapmak için, ObjectDataSource tarafından kullanılan mantığı tekrarlamanız gerekecektir. Sonraki öğreticimizde mimarideki veri önbelleğiyle programlı olarak nasıl çalışacağımız anlatılmaktadır.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET önbelleğe alma: teknikler ve En Iyi uygulamalar](https://msdn.microsoft.com/library/aa478965.aspx)
- [.NET Framework uygulamalar için önbelleğe alma Mimarisi Kılavuzu](https://msdn.microsoft.com/library/ee817645.aspx)
- [ASP.NET 2,0 ' de çıktı önbelleği](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni bir Murphy idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](caching-data-in-the-architecture-cs.md)
