---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
title: Ana sayfadan Içerik sayfası ile etkileşim kurma (VB) | Microsoft Docs
author: rick-anderson
description: Yöntemlerin nasıl çağrılacağını, Içerik sayfasının özellikleri, vb. ana sayfadaki koddan nasıl ayarlanacağını inceler.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: a6e2e1a0-c925-43e9-b711-1f178fdd72d7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 5367ad1b7f2fa11c635ad95754c9bcc1edcb6c1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615519"
---
# <a name="interacting-with-the-content-page-from-the-master-page-vb"></a>İçerik Sayfasından Ana Sayfa ile Etkileşim Kurma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_VB.pdf)

> Yöntemlerin nasıl çağrılacağını, Içerik sayfasının özellikleri, vb. ana sayfadaki koddan nasıl ayarlanacağını inceler.

## <a name="introduction"></a>Giriş

Önceki öğreticide, içerik sayfasının, ana sayfasıyla programlı bir şekilde nasıl etkileşimde bulunduğu incelendi. Ana sayfayı, en son eklenen beş ürünün listelendiği bir GridView denetimi içerecek şekilde güncelleştirdiğimiz geri çekin. Daha sonra kullanıcının yeni bir ürün ekleyebileceği bir içerik sayfası oluşturduk. Yeni bir ürün eklendikten sonra, ana sayfanın GridView 'u yenilemesi için gereken içerik sayfası, tam eklenen ürünü içerecek şekilde. Bu işlevsellik, ana sayfaya GridView 'a bağlanan verileri yenilenen bir genel yöntem eklenerek ve sonra bu yöntemi içerik sayfasından çağırarak gerçekleştirildi.

En yaygın içerik ve ana sayfa etkileşimi biçimi içerik sayfasından kaynaklanır. Bununla birlikte, ana sayfanın geçerli içerik sayfasını eylemde kullanması mümkündür ve ana sayfa, kullanıcıların da içerik sayfasında görüntülenen verileri değiştirmesine olanak tanıyan Kullanıcı arabirimi öğelerini içeriyorsa bu tür işlevler gerekebilir. Ürün bilgilerini bir GridView denetiminde görüntüleyen bir içerik sayfasını ve tıklandığı sırada tüm ürünlerin fiyatlarını iki katına ekleyen bir düğme denetimi içeren bir ana sayfayı düşünün. Önceki öğreticideki örnekteki örnekte olduğu gibi, yeni fiyatları görüntüleyecek şekilde çift fiyat düğmesine tıklandıktan sonra GridView 'in yenilenmesi gerekir, ancak bu senaryoda içerik sayfasının eylemde bulunması gereken ana sayfa budur.

Bu öğretici, içerik sayfasında ana sayfa çağırma işlevinin nasıl kullanılacağını açıklar.

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>Bir olay ve olay Işleyicileri aracılığıyla programlı etkileşimi geçersiz kılar

Bir ana sayfadan içerik sayfası işlevselliğinin çağrılması, etrafında başka bir yoldan daha zor bir yoldur. İçerik sayfasında tek bir ana sayfa bulunduğundan, içerik sayfasından programlama etkileşimini alırken hangi ortak yöntemlerin ve özelliklerin elden çıkarıldığımızda olduğunu biliyoruz. Ancak, bir ana sayfa, her biri kendi özellik ve yöntemlerine sahip birçok farklı içerik sayfasına sahip olabilir. Daha sonra, çalışma zamanına kadar hangi içerik sayfasının çağrılacağını bilmediğinizde, içerik sayfasında bir eylem gerçekleştirmek için ana sayfada kod yazabilir miyim?

Düğme denetimi gibi bir ASP.NET Web denetimi düşünün. Düğme denetimi, herhangi bir sayıda ASP.NET sayfasında görünebilir ve tıklandığı sayfayı uyarabileceği bir mekanizmaya ihtiyaç duyuyor. Bu, *Olaylar*kullanılarak gerçekleştirilir. Özellikle, düğme denetimi tıklandığında `Click` olayını başlatır; Düğmeyi içeren ASP.NET sayfası, isteğe bağlı olarak bir *olay işleyicisi*aracılığıyla bu bildirime yanıt verebilir.

Bu aynı model, içerik sayfalarında bir ana sayfa tetikleme işlevselliğine sahip olmak için kullanılabilir:

1. Ana sayfaya bir olay ekleyin.
2. Ana sayfanın içerik sayfasıyla iletişim kurması gerektiğinde olayı yükseltin. Örneğin, ana sayfanın, kullanıcının fiyatları iki katına çıkarması halinde içerik sayfasını uyarmasını gerekiyorsa, bu durum fiyatlar iki katına çıktıktan sonra bu olay hemen oluşturulur.
3. Bu içerik sayfalarında bazı işlemleri yapması gereken bir olay işleyicisi oluşturun.

Bu öğreticinin geri kalanında giriş bölümünde özetlenen örnek uygulanır; Yani, veritabanındaki ürünleri listeleyen bir içerik sayfası ve iki fiyata de bir düğme denetimi içeren bir ana sayfa.

## <a name="step-1-displaying-products-in-a-content-page"></a>1\. Adım: ürünleri bir Içerik sayfasında görüntüleme

İlk iş sıramız, Northwind veritabanından ürünleri listeleyen bir içerik sayfası oluşturmaktır. (Northwind veritabanını önceki öğreticide projeye ekledik, bu, [*Içerik sayfasından ana sayfayla etkileşime*](interacting-with-the-master-page-from-the-content-page-vb.md)geçin.) `Products.aspx`adlı `~/Admin` klasöre yeni bir ASP.NET sayfası ekleyerek başlayın, bunu `Site.master` ana sayfasına bağlamayı unutmayın. Şekil 1 ' de Bu sayfa Web sitesine eklendikten sonra Çözüm Gezgini gösterilmektedir.

[Yönetici klasörüne yeni bir ASP.NET sayfası eklemek ![](interacting-with-the-content-page-from-the-master-page-vb/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image1.png)

**Şekil 01**: `Admin` klasöre yeni bir ASP.NET sayfası ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image3.png))

[*Ana sayfada başlık, meta etiketler ve DIĞER HTML üst bilgilerini belirtme*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) öğreticisinde, açıkça ayarlanmamışsa sayfanın başlığını oluşturan `BasePage` adlı özel bir temel sayfa sınıfı oluşturduğumuz hatırlayın. `Products.aspx` sayfanın arka plan kod sınıfına gidin ve `BasePage` türetebilirsiniz (`System.Web.UI.Page`yerine).

Son olarak, `Web.sitemap` dosyasını bu ders için bir giriş içerecek şekilde güncelleştirin. Içeriğin ana sayfa etkileşimi dersi için `<siteMapNode>` altına aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample1.xml)]

Bu `<siteMapNode>` öğesinin eklenmesi dersler listesinde yansıtılır (bkz. Şekil 5).

`Products.aspx`dön. `MainContent`için Içerik denetiminde bir GridView denetimi ekleyin ve `ProductsGrid`adlandırın. GridView öğesini `ProductsDataSource`adlı yeni bir SqlDataSource denetimine bağlayın.

[GridView 'i yeni bir SqlDataSource denetimine bağlama ![](interacting-with-the-content-page-from-the-master-page-vb/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image4.png)

**Şekil 02**: GridView 'ı yeni bir SqlDataSource denetimine bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image6.png))

Sihirbazı Northwind veritabanını kullanacak şekilde yapılandırın. Önceki öğreticide çalıştıysanız, `Web.config``NorthwindConnectionString` adlı bir bağlantı dizesi zaten olmalıdır. Şekil 3 ' te gösterildiği gibi, açılan listeden bu bağlantı dizesini seçin.

[![SqlDataSource 'ı Northwind veritabanını kullanacak şekilde yapılandırma](interacting-with-the-content-page-from-the-master-page-vb/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image7.png)

**Şekil 03**: SqlDataSource 'ı Northwind veritabanını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image9.png))

Sonra, açılan listeden Ürünler tablosunu seçerek ve `ProductName` ve `UnitPrice` sütunlarını döndürerek veri kaynağı denetiminin `SELECT` ifadesini belirtin (bkz. Şekil 4). Ileri ' ye tıklayın ve ardından son ' a tıklayarak veri kaynağı Yapılandırma Sihirbazı 'nı doldurun.

[![Products tablosundan ProductName ve BirimFiyat alanlarını döndürün](interacting-with-the-content-page-from-the-master-page-vb/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image10.png)

**Şekil 04**: `Products` tablosundan `ProductName` ve `UnitPrice` alanlarını döndürün ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image12.png))

İşte bu kadar kolay! Sihirbazı tamamladıktan sonra Visual Studio, SqlDataSource denetimi tarafından döndürülen iki alanı yansıtmak için GridView 'a iki BoundFields ekler. GridView ve SqlDataSource denetimlerinin biçimlendirmesi aşağıda verilmiştir. Şekil 5 ' te bir tarayıcıdan görüntülendiklerinde sonuçlar gösterilmektedir.

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample2.aspx)]

[![her ürün ve fiyatı GridView 'da listelenir](interacting-with-the-content-page-from-the-master-page-vb/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image13.png)

**Şekil 05**: her ürün ve fiyatı GridView 'da listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image15.png))

> [!NOTE]
> GridView 'un görünümünü temizlemeyi ücretsiz olarak hissetmekten çekinmeyin. Bazı öneriler, görüntülenecek UnitPrice değerini bir para birimi olarak biçimlendirmeyi ve kılavuz görünümünü geliştirmek için arka plan renkleri ve yazı tiplerini kullanmayı içerir. ASP.NET içinde veri görüntüleme ve biçimlendirme hakkında daha fazla bilgi için bkz. My [Data öğretici Series Ile çalışma](../../data-access/index.md).

## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>2\. Adım: Ana sayfaya çift fiyatlar düğmesi ekleme

Sonraki görevimiz, ana sayfaya tıklandığı zaman veritabanındaki tüm ürünlerin fiyatını iki kez eklemek için bir düğme web denetimi eklemektir. `Site.master` ana sayfasını açın ve araç kutusu 'ndaki bir düğmeyi, bir önceki öğreticide eklediğimiz `RecentProductsDataSource` SqlDataSource denetiminin altına yerleştirerek tasarımcı üzerine sürükleyin. Düğmenin `ID` özelliğini `DoublePrice` ve `Text` özelliğini "çift ürün fiyatları" olarak ayarlayın.

Ardından, ana sayfaya `DoublePricesDataSource`adlandırarak bir SqlDataSource denetimi ekleyin. Bu SqlDataSource, tüm fiyatlara çift olmak üzere `UPDATE` ifadesini yürütmek için kullanılacaktır. Özellikle, `ConnectionString` ve `UpdateCommand` özelliklerini uygun bağlantı dizesi ve `UPDATE` bildirimine ayarlamanız gerekir. Sonra, `DoublePrice` düğmesine tıklandığında bu SqlDataSource denetiminin `Update` yöntemini çağırmanız gerekir. `ConnectionString` ve `UpdateCommand` özelliklerini ayarlamak için SqlDataSource denetimini seçip Özellikler penceresi gidin. `ConnectionString` özelliği, bir açılan listede `Web.config` zaten depolanmış olan bağlantı dizelerini listeler; Şekil 6 ' da gösterildiği gibi `NorthwindConnectionString` seçeneğini belirleyin.

[![NorthwindConnectionString kullanarak SqlDataSource 'ı yapılandırın](interacting-with-the-content-page-from-the-master-page-vb/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image16.png)

**Şekil 06**: SqlDataSource 'ı `NorthwindConnectionString` kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image18.png))

`UpdateCommand` özelliğini ayarlamak için Özellikler penceresi UpdateQuery seçeneğini bulun. Bu özellik seçildiğinde, üç nokta içeren bir düğmeyi görüntüler; Şekil 7 ' de gösterilen komut ve parametre Düzenleyici iletişim kutusunu göstermek için bu düğmeye tıklayın. İletişim kutusunun metin kutusuna aşağıdaki `UPDATE` ifadesini yazın:

[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample3.sql)]

Bu bildirim yürütüldüğünde, `Products` tablosundaki her bir kayıt için `UnitPrice` değeri ikiye katılacaktır.

[![SqlDataSource 'un UpdateCommand özelliğini ayarla](interacting-with-the-content-page-from-the-master-page-vb/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image19.png)

**Şekil 07**: SqlDataSource 'un `UpdateCommand` özelliğini ayarlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image21.png))

Bu özellikleri ayarladıktan sonra düğme ve SqlDataSource denetimlerinizin bildirim temelli biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample4.aspx)]

Her durumda, `DoublePrice` düğmesine tıklandığında `Update` yöntemi çağırılır. `DoublePrice` düğmesi için `Click` olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample5.vb)]

Bu işlevi test etmek için adım 1 ' de oluşturduğumuz `~/Admin/Products.aspx` sayfasını ziyaret edin ve "çift ürün fiyatları" düğmesine tıklayın. Düğmeye tıkladığınızda geri göndermeye neden olur ve tüm ürünlerin fiyatları ikiye katlanarak `DoublePrice` düğmenin `Click` olay işleyicisini yürütür. Daha sonra sayfa yeniden işlenir ve biçimlendirme döndürülür ve tarayıcıda yeniden görüntülenir. Ancak içerik sayfasındaki GridView, "çift ürün fiyatları" düğmesine tıklanmadan aynı fiyatları listeler. Bunun nedeni, GridView 'da başlangıçta yüklenen verilerin durumunu Görünüm durumunda depoladığından, aksi belirtilmedikçe geri yükleme sırasında yeniden yüklenmez. Farklı bir sayfayı ziyaret edip `~/Admin/Products.aspx` sayfasına geri dönerseniz, güncelleştirilmiş fiyatları görürsünüz.

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>3\. Adım: fiyatlar Iki katına çıkarılarak bir olay oluşturma

`~/Admin/Products.aspx` sayfasındaki GridView, katlama fiyatını hemen yansıtmadığından, bir Kullanıcı "çift ürün fiyatları" düğmesine tıklamamaları veya çalışmamış olduğunu olumsuz şekilde düşünebilir. Birkaç kez düğmeye tıkladıktan sonra fiyatların yeniden ve yeniden katlanmaları gerekebilir. Bu hatayı düzeltireceğiz, içerik sayfasında kılavuzun, yeni fiyatları iki katına çıkardıktan hemen sonra görüntülemesi gerekir.

Bu öğreticide daha önce anlatıldığı gibi, Kullanıcı `DoublePrice` düğmesine her tıkladığında ana sayfada bir olay yükseltmemiz gerekir. Bir olay, bir sınıfın (olay yayımcısının) başka bir sınıf kümesine (Olay aboneleri) bildirimde bulunduğunu bildiren bir yoldur. Bu örnekte, ana sayfa olay yayımcısıdır; `DoublePrice` düğmesine tıklandığında bu içerik sayfaları, aboneler olur.

Bir sınıf, yükseltilen olaya yanıt olarak yürütülen bir yöntem olan *olay işleyicisi*oluşturarak bir olaya abone olur. Yayımcı, bir *olay temsilcisi*tanımlayarak Başlatan olayları tanımlar. Olay temsilcisi, olay işleyicisinin hangi giriş parametrelerini kabul etmesi gerektiğini belirtir. .NET Framework, olay temsilcileri herhangi bir değer döndürmez ve iki giriş parametresini kabul etmez:

- Olay kaynağını tanımlayan `Object`ve
- `System.EventArgs` türetilen bir sınıf

Bir olay işleyicisine geçirilen ikinci parametre, olayla ilgili ek bilgiler içerebilir. Temel `EventArgs` sınıfı herhangi bir bilgi üzerinde geçmediğinden, .NET Framework `EventArgs` genişleten ve ek özellikleri kapsayan bir dizi sınıf içerir. Örneğin, `Command` olayına yanıt veren olay işleyicilerine `CommandEventArgs` bir örnek geçirilir ve iki bilgilendirici özellik içerir: `CommandArgument` ve `CommandName`.

> [!NOTE]
> Olayları oluşturma, oluşturma ve işleme hakkında daha fazla bilgi için bkz. [Olaylar ve temsilciler](https://msdn.microsoft.com/library/17sde2xt.aspx) ve [olay temsilcileri basit İngilizce](http://www.codeproject.com/KB/cs/eventdelegates.aspx).

Bir olayı tanımlamak için aşağıdaki sözdizimini kullanın:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample6.vb)]

Yalnızca Kullanıcı `DoublePrice` düğmesine tıkladığında içerik sayfasını uyarması ve diğer ek bilgileri daha fazla iletmemiz gerekdiğimiz için, ikinci parametresi olarak `System.EventArgs`türünde bir nesne kabul eden olay işleyicisini tanımlayan olay temsilcisi `EventHandler`kullanabiliriz. Ana sayfada olayı oluşturmak için aşağıdaki kod satırını ana sayfanın arka plan kod sınıfına ekleyin:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample7.vb)]

Yukarıdaki kod, `PricesDoubled`adlı ana sayfaya ortak bir olay ekler. Artık fiyatların iki katına çıktıktan sonra bu olayı geliştirmemiz gerekir. Bir olayı yükseltmek için aşağıdaki sözdizimini kullanın:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample8.vb)]

Burada *sender* ve *eventArgs* , abonenin olay işleyicisine geçirmek istediğiniz değerlerdir.

`DoublePrice` `Click` olay işleyicisini aşağıdaki kodla güncelleştirin:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample9.vb)]

Daha önce olduğu gibi `Click` olay işleyicisi, tüm ürünlerin fiyatlarını ikiye katmaya yönelik `DoublePricesDataSource` SqlDataSource denetiminin `Update` yöntemini çağırarak başlar. Olay işleyicisine iki ekleme vardır. İlk olarak, `RecentProducts` GridView 'un verileri yenilenir. Bu GridView, önceki öğreticideki ana sayfaya eklenmiştir ve en son eklenen beş ürünü görüntüler. Bu beş ürüne yönelik tek yönlü fiyatları görüntüleyecek şekilde bu kılavuzu yenilememiz gerekiyor. Bunu izleyerek `PricesDoubled` olayı tetiklenir. Ana sayfanın kendisi (`Me`) başvurusu olay işleyicisine olay kaynağı olarak gönderilir ve olay bağımsız değişkenleri olarak boş bir `EventArgs` nesnesi gönderilir.

## <a name="step-4-handling-the-event-in-the-content-page"></a>4\. Adım: Içerik sayfasında olayı Işleme

Bu noktada, `DoublePrice` düğme denetimine tıklandığında ana sayfa `PricesDoubled` olayını oluşturur. Ancak, bu yalnızca bir yarıydır. abonedeki etkinliği yine de ele almanız gerekir. Bu iki adımdan oluşur: olay işleyicisi oluşturma ve olay bağlantısı kodu ekleme, böylece olay olay işleyicisi yürütüldüğünde.

`Master_PricesDoubled`adlı bir olay işleyicisi oluşturarak başlayın. Ana sayfada `PricesDoubled` olayını tanımladığımızda, olay işleyicisinin iki giriş parametresi sırasıyla `Object` ve `EventArgs`türünde olmalıdır. Olay işleyicisinde, verileri kılavuza yeniden bağlamak için `ProductsGrid` GridView 'un `DataBind` yöntemini çağırın.

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample10.vb)]

Olay işleyicisinin kodu tamamlanmıştır, ancak henüz ana sayfanın bu olay işleyicisine yönelik `PricesDoubled` olayına gönderim yaptık. Abone bir olay işleyicisine aşağıdaki söz dizimi aracılığıyla bir olay ile kablolar sağlar:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample11.vb)]

*Yayımcı* , olay *EventName*'sini sunan nesneye bir başvurudur ve *MethodName* , abonede tanımlanan olay işleyicisinin adıdır.

Bu olay kablolama kodu ilk sayfada ve sonraki geri göndermeler üzerinde yürütülmelidir ve olay ortaya çıktığında önce sayfa yaşam döngüsünün bir noktasında gerçekleşmelidir. Olay kablolama kodu eklemek için iyi bir zaman, sayfa yaşam döngüsünün çok erken gerçekleştiği PreInit aşamasıdır.

`~/Admin/Products.aspx` açın ve bir `Page_PreInit` olay işleyicisi oluşturun:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample12.vb)]

Bu kablolama kodunu tamamlayabilmeniz için içerik sayfasından ana sayfaya programlı bir başvuruya ihtiyacımız var. Önceki öğreticide belirtildiği gibi, bunu iki şekilde yapabilirsiniz:

- Gevşek yazılı `Page.Master` özelliğini uygun ana sayfa türüne kaldırarak veya
- `.aspx` sayfasına bir `@MasterType` yönergesi ekleyerek ve sonra türü kesin belirlenmiş `Master` özelliğini kullanarak.

İkinci yaklaşımı kullanalım. Aşağıdaki `@MasterType` yönergesini sayfanın bildirim temelli biçimlendirmesinin en üstüne ekleyin:

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample13.aspx)]

`Page_PreInit` olay işleyicisine aşağıdaki olay kablolama kodunu ekleyin:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample14.vb)]

Bu kodla birlikte, içerik sayfasındaki GridView `DoublePrice` düğmesine tıklandığında yenilenir.

Şekil 8 ve 9 Bu davranışı gösterir. Şekil 8 ilk kez ziyaret edildiğinde sayfayı gösterir. Her iki `RecentProducts` GridView 'daki (ana sayfanın sol sütununda) ve `ProductsGrid` GridView (içerik sayfasında) fiyat değerlerini unutmayın. Şekil 9 ' da, `DoublePrice` düğmesi tıklandıktan hemen sonra aynı ekran görüntülenir. Gördüğünüz gibi, yeni fiyatlar anında her iki GridViews 'ta yansıtılır.

[Ilk fiyat değerlerini ![](interacting-with-the-content-page-from-the-master-page-vb/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image22.png)

**Şekil 08**: başlangıç fiyatı değerleri ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image24.png))

[![, tek çift fiyatlar GridViews 'ta görüntülenir](interacting-with-the-content-page-from-the-master-page-vb/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image25.png)

**Şekil 09**: yalnızca çift yönlü fiyatlar GridViews 'ta görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-content-page-from-the-master-page-vb/_static/image27.png))

## <a name="summary"></a>Özet

İdeal olarak, bir ana sayfa ve içerik sayfaları diğerinden tamamen ayrıdır ve etkileşim düzeyi gerektirmez. Ancak, ana sayfa veya içerik sayfasından değiştirilebilen verileri görüntüleyen bir ana sayfa ya da içerik sayfanız varsa, ekran güncelleştirilemediğinden, veriler değiştirildiğinde ana sayfanın içerik sayfasını (veya tam tersi) uyarmasını gerekebilir. Önceki öğreticide, bir içerik sayfasının, ana sayfası aracılığıyla programlı bir şekilde nasıl etkileşim kuracağını gördük. Bu öğreticide, bir ana sayfanın etkileşimi nasıl başlatabileceğini inceledik.

Bir içerik ve ana sayfa arasındaki programlama etkileşimi, içerik veya ana sayfadan kaynaklanırken, kullanılan etkileşim deseninin kaynağı temel alır. Farklar, bir içerik sayfasının tek bir ana sayfaya sahip olması ve bir ana sayfanın birçok farklı içerik sayfasına sahip olması olabilir. Bir ana sayfanın bir içerik sayfasıyla doğrudan etkileşim kurması yerine, ana sayfanın bazı bir eylemin gerçekleştiğinden emin olmak için bir olay oluşturması daha iyi bir yaklaşımdır. Eylem hakkında dikkatli olan içerik sayfaları olay işleyicileri oluşturabilir.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET 'deki verilere erişme ve verileri güncelleştirme](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [Olaylar ve temsilciler](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [Içerik ve ana sayfalar arasında bilgi geçirme](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET öğreticilerde verilerle çalışma](../../data-access/index.md)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren Suçi Banerjee idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Önceki](interacting-with-the-master-page-from-the-content-page-vb.md)
> [İleri](master-pages-and-asp-net-ajax-vb.md)
