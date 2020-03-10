---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-cs
title: ObjectDataSource Ile verileri görüntüleme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğretici, bu denetimi kullanarak ObjectDataSource denetimine bakar ve önceki öğreticide oluşturulan BLL 'lerden alınan verileri havi olmadan bağlayabilirsiniz...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: af882aef-56f5-4e9a-8f95-3977fde20e74
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 9419504ace15b39c35a034dda22f2700ee720157
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78577478"
---
# <a name="displaying-data-with-the-objectdatasource-c"></a>ObjectDataSource ile Verileri Görüntüleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_4_CS.exe) veya [PDF 'yi indirin](displaying-data-with-the-objectdatasource-cs/_static/datatutorial04cs1.pdf)

> Bu öğretici, bu denetimi kullanarak ObjectDataSource denetimine bakar. bir kod satırı yazmak zorunda kalmadan, önceki öğreticide oluşturulan BLL 'lerden alınan verileri bağlayabilirsiniz!

## <a name="introduction"></a>Giriş

Uygulama mimarimiz ve Web sitesi sayfası düzeni tamamlanarak, çeşitli yaygın veri ve raporlama ile ilgili görevleri nasıl gerçekleştireceğinizi keşfetmeye başlamaya hazırız. Önceki öğreticilerde, DAL ve BLL 'den verileri bir ASP.NET sayfasındaki veri Web denetimine programlı bir şekilde bağlamayı gördük. Bu sözdizimi, veri Web denetiminin `DataSource` özelliğini görüntülenecek verilere atamak ve sonra denetimin `DataBind()` yöntemini çağırmak, ASP.NET 1. x uygulamalarında kullanılan modeldir ve 2,0 uygulamalarınızda kullanmaya devam edebilir. Ancak, ASP.NET 2.0 'ın yeni veri kaynağı denetimleri verilerle çalışmanın bildirime dayalı bir yolunu sunar. Bu denetimleri kullanarak, bir kod satırı yazmak zorunda kalmadan [önceki öğreticide](../introduction/creating-a-business-logic-layer-cs.md) oluşturulan BLL 'lerden alınan verileri bağlayabilirsiniz!

ASP.NET 2,0, varsa, kendi [özel veri kaynağı denetimlerinizi](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp)oluşturabileceğiniz gibi, [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w(vs.80).aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a(en-US,VS.80).aspx)ve [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x(en-US,VS.80).aspx) gibi beş yerleşik veri kaynağı denetimi ile birlikte sunulur. Öğretici uygulamamız için bir mimari geliştirdik, BLL sınıflarımızla ilgili ObjectDataSource kullanacağız.

![ASP.NET 2,0, beş yerleşik veri kaynağı denetimini Içerir](displaying-data-with-the-objectdatasource-cs/_static/image1.png)

**Şekil 1**: ASP.NET 2,0, beş yerleşik veri kaynağı denetimini içerir

ObjectDataSource, başka bir nesneyle çalışmak için bir proxy görevi görür. ObjectDataSource 'u yapılandırmak için, bu temel nesneyi ve yöntemlerinin, ObjectDataSource 'un `Select`, `Insert`, `Update`ve `Delete` yöntemlerine nasıl eşlendiğini belirttik. Bu temel nesne belirtilmişse ve yöntemleri ObjectDataSource 'a eşlendikten sonra, ObjectDataSource 'u bir veri Web denetimine bağlayabiliriz. ASP.NET, diğer kullanıcıların yanı sıra GridView, DetailsView, RadioButtonList ve DropDownList gibi birçok veri Web denetimi ile birlikte sunulur. Sayfa yaşam döngüsü sırasında, veri Web denetiminin, onun, ObjectDataSource 'un `Select` yöntemini çağırarak yerine, bağlandığı verilere erişmesi gerekebilir; veri Web denetimi ekleme, güncelleştirme veya silme desteği içeriyorsa, ObjectDataSource 'un `Insert`, `Update`veya `Delete` yöntemlerine çağrı yapılabilir. Bu çağrılar daha sonra aşağıdaki diyagramda gösterildiği gibi ObjectDataSource tarafından uygun temel nesnenin yöntemlerine yönlendirilir.

[ObjectDataSource bir proxy görevi görür ![](displaying-data-with-the-objectdatasource-cs/_static/image3.png)](displaying-data-with-the-objectdatasource-cs/_static/image2.png)

**Şekil 2**: ObjectDataSource bir ara sunucu görevi görür ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image4.png))

ObjectDataSource, veri ekleme, güncelleştirme veya silme yöntemlerini çağırmak için kullanılabilir ancak yalnızca verileri döndürmenize odaklanalım; gelecekteki öğreticiler, verileri değiştiren ObjectDataSource ve veri Web denetimlerini kullanarak araştıracaktır.

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>1\. Adım: ObjectDataSource denetimini ekleme ve yapılandırma

`BasicReporting` klasöründeki `SimpleDisplay.aspx` sayfasını açıp Tasarım görünümü ' e geçin ve araç kutusundan bir ObjectDataSource denetimini sayfanın tasarım yüzeyine sürükleyin. Herhangi bir biçimlendirme üretmediğinden, ObjectDataSource tasarım yüzeyinde gri kutu olarak görünür; yalnızca belirtilen nesneden bir yöntemi çağırarak verilere erişir. Bir ObjectDataSource tarafından döndürülen veriler GridView, DetailsView, FormView gibi bir veri Web denetimi tarafından görüntülenebilir.

> [!NOTE]
> Alternatif olarak, önce veri Web denetimini sayfaya ekleyebilir ve ardından akıllı etiketinden, açılan listeden &lt;yeni veri kaynağı&gt; seçeneğini belirleyebilirsiniz.

ObjectDataSource 'un temel alınan nesnesini ve bu nesnenin yöntemlerinin ObjectDataSource 'a nasıl eşlendiğini belirtmek için, ObjectDataSource 'un akıllı etiketindeki veri kaynağını Yapılandır bağlantısına tıklayın.

[![akıllı etiketten veri kaynağını Yapılandır bağlantısına tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image6.png)](displaying-data-with-the-objectdatasource-cs/_static/image5.png)

**Şekil 3**: akıllı etiketten veri kaynağını Yapılandır bağlantısına tıklayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image7.png))

Bu, veri kaynağı Yapılandırma Sihirbazı 'nı getirir. İlk olarak, ObjectDataSource 'un birlikte çalıştıkları nesneyi belirtmemiz gerekir. "Yalnızca veri bileşenlerini göster" onay kutusu işaretliyse, bu ekrandaki aşağı açılan listede yalnızca `DataObject` özniteliğiyle donatılmış nesneler listelenir. Şu anda listemize yazılan veri kümesindeki TableAdapters ve önceki öğreticide oluşturduğumuz BLL sınıfları yer almaktadır. `DataObject` özniteliğini Iş mantığı katman sınıflarına eklemeyi unuttuysanız, bu listede göremezsiniz. Bu durumda, tüm nesneleri görüntülemek için "yalnızca veri bileşenlerini göster" onay kutusunun işaretini kaldırın. Bu, BLL sınıflarını (yazılan veri kümesindeki diğer sınıflarla birlikte DataTable, DataRow, vb.) içermelidir.

Bu ilk ekrandan, açılan listeden `ProductsBLL` sınıfını seçin ve Ileri ' ye tıklayın.

[ObjectDataSource denetimiyle kullanılacak nesneyi belirtmek ![](displaying-data-with-the-objectdatasource-cs/_static/image9.png)](displaying-data-with-the-objectdatasource-cs/_static/image8.png)

**Şekil 4**: ObjectDataSource denetimiyle kullanılacak nesneyi belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image10.png))

Sihirbazın sonraki ekranında, ObjectDataSource 'un hangi yöntemi çağıracağına ilişkin istem sorulur. Açılan listede, önceki ekrandan Seçilen nesnedeki verileri döndüren yöntemler listelenmiştir. Burada `GetProductByProductID`, `GetProducts`, `GetProductsByCategoryID`ve `GetProductsBySupplierID`görüyoruz. Aşağı açılan listeden `GetProducts` yöntemini seçin ve son ' a tıklayın (önceki öğreticide gösterildiği gibi, `DataObjectMethodAttribute` `ProductBLL`yöntemlerine eklediyseniz, bu seçenek varsayılan olarak seçilidir).

[![SEÇIM sekmesinden verileri döndürme yöntemini seçin](displaying-data-with-the-objectdatasource-cs/_static/image12.png)](displaying-data-with-the-objectdatasource-cs/_static/image11.png)

**Şekil 5**: seçim sekmesinden verileri döndürme yöntemini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image13.png))

## <a name="configure-the-objectdatasource-manually"></a>ObjectDataSource 'ı El Ile yapılandırma

ObjectDataSource 'un veri kaynağını yapılandırma Sihirbazı, kullandığı nesneyi belirtmenin ve nesnenin hangi yöntemlerinin çağırılacağını ilişkilendirmenin hızlı bir yolunu sunar. Ancak, ObjectDataSource 'u Özellikler penceresi veya doğrudan bildirime dayalı İşaretlemede bulunan özellikleriyle yapılandırabilirsiniz. `TypeName` özelliğini, kullanılacak temel nesnenin türüne ve verileri alırken çağrılacak yönteme `SelectMethod` ayarlamanız yeterlidir.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample1.aspx)]

Veri kaynağı Yapılandırma Sihirbazı 'nı tercih etseniz bile, sihirbaz yalnızca geliştirici tarafından oluşturulan sınıfları listelediğinden, ObjectDataSource 'u el ile yapılandırmanız gerektiği zamanlar olabilir. ObjectDataSource 'u [Üyelik sınıfı](https://msdn.microsoft.com/library/system.web.security.membership.aspx)gibi .NET Framework bir sınıfa bağlamak istiyorsanız, Kullanıcı hesabı bilgilerine erişmek veya [Dizin sınıfına](https://msdn.microsoft.com/library/system.io.directory.aspx) dosya sistemi bilgileriyle çalışmak için, ObjectDataSource 'un özelliklerini el ile ayarlamanız gerekir.

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>2\. Adım: veri Web denetimi ekleme ve ObjectDataSource 'a bağlama

ObjectDataSource sayfaya eklendikten ve yapılandırıldıktan sonra, ObjectDataSource 'un `Select` yöntemi tarafından döndürülen verileri göstermek için sayfaya veri Web denetimleri eklemeye hazırız. Herhangi bir veri Web denetimi bir ObjectDataSource 'a bağlanabilir; bir GridView, DetailsView ve FormView 'da ObjectDataSource 'un verilerini görüntülemeye bakalım.

## <a name="binding-a-gridview-to-the-objectdatasource"></a>ObjectDataSource 'a bir GridView bağlama

Araç kutusundan `SimpleDisplay.aspx`tasarım yüzeyine bir GridView denetimi ekleyin. GridView 'un akıllı etiketinden, 1. adımda eklediğimiz ObjectDataSource denetimini seçin. Bu işlem, ObjectDataSource 'un `Select` yöntemi (yani Products DataTable tarafından tanımlanan Özellikler) tarafından döndürülen her bir özellik için GridView 'da otomatik olarak bir BoundField oluşturur.

[Sayfaya ![GridView eklendi ve bu, ObjectDataSource 'a bağlamıştır](displaying-data-with-the-objectdatasource-cs/_static/image15.png)](displaying-data-with-the-objectdatasource-cs/_static/image14.png)

**Şekil 6**: sayfaya bir GridView eklenmiştir ve ObjectDataSource 'a bağlanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image16.png))

Daha sonra akıllı etiketteki sütunları Düzenle seçeneğine tıklayarak GridView 'un BoundFields alanlarını özelleştirebilir, yeniden düzenleyebilir veya kaldırabilirsiniz.

[GridView 'un BoundFields alanlarını sütunları Düzenle Iletişim kutusuyla yönetme ![](displaying-data-with-the-objectdatasource-cs/_static/image18.png)](displaying-data-with-the-objectdatasource-cs/_static/image17.png)

**Şekil 7**: sütunları Düzenle Iletişim kutusu ile GridView 'un boundfields alanlarını yönetme ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image19.png))

GridView 'un BoundFields alanlarını değiştirmek, `ProductID`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitsInStock`, `UnitsOnOrder`ve `ReorderLevel` BoundFields alanlarını kaldırmak için bir dakikanızı ayırın. Sol alt kısımdaki listeden BoundField öğesini seçmeniz yeterlidir ve Sil düğmesine (kırmızı X) tıklayarak bunları kaldırın. Sonra, `CategoryName` ve `SupplierName` BoundFields `UnitPrice` BoundField ' dan önce bu BoundFields alanlarını seçip Yukarı oka tıklayarak BoundFields alanlarını yeniden düzenleyin. Kalan BoundFields `HeaderText` özelliklerini sırasıyla `Products`, `Category`, `Supplier`ve `Price`olarak ayarlayın. Sonra, BoundField 'un `HtmlEncode` özelliğini false olarak ayarlayıp `DataFormatString` özelliğini `{0:c}`olarak ayarlayarak `Price` BoundField değerini bir para birimi olarak biçimlendirilir. Son olarak, `ItemStyle`/`HorizontalAlign` özelliği aracılığıyla `Price` sağ ve ortadaki `Discontinued` onay kutusuna yatay olarak hizalayın.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample2.aspx)]

[GridView 'un BoundFields alanları ![özelleştirilmiş](displaying-data-with-the-objectdatasource-cs/_static/image21.png)](displaying-data-with-the-objectdatasource-cs/_static/image20.png)

**Şekil 8**: GridView 'un Boundfields alanları özelleştirildi ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image22.png))

## <a name="using-themes-for-a-consistent-look"></a>Tutarlı bir görünüm için temaları kullanma

Bu öğreticiler, mümkün olduğunda bir dış dosyada tanımlanan geçişli stil sayfalarını kullanmak yerine herhangi bir denetim düzeyindeki stil ayarını kaldırmak için çaba harcar. `Styles.css` dosyası, bu öğreticilerde kullanılan veri Web denetimlerinin görünümünü dikte etmek için kullanılması gereken `DataWebControlStyle`, `HeaderStyle`, `RowStyle`ve `AlternatingRowStyle` CSS sınıflarını içerir. Bunu gerçekleştirmek için, GridView 'ın `CssClass` özelliğini `DataWebControlStyle`ve `HeaderStyle`, `RowStyle`ve `AlternatingRowStyle` özellikleri uygun şekilde `CssClass` özellikleriyle ayarlayabiliriz.

Web denetimindeki bu `CssClass` özelliklerini ayarlıyoruz, öğreticilerimize eklenen her bir veri Web denetimi için bu özellik değerlerini açıkça ayarlamayı unutmamanız gerekir. Daha yönetilebilir bir yaklaşım, bir tema kullanarak GridView, DetailsView ve FormView denetimleri için CSS ile ilgili varsayılan özellikleri tanımlamaktır. Tema, ortak bir görünümü zorlamak için bir site genelinde sayfalara uygulanabilen denetim düzeyi özellik ayarları, görüntüler ve CSS sınıflarının koleksiyonudur.

Temamız herhangi bir görüntü veya CSS dosyası içermeyecektir (stil sayfasını Web uygulamasının kök klasöründe tanımlanmış olduğu gibi `Styles.css` bırakıyoruz, ancak iki kaplama de içerecektir. Bir kaplama, bir Web denetimi için varsayılan özellikleri tanımlayan bir dosyadır. Özellikle, GridView ve DetailsView denetimleri için, varsayılan `CssClass`ilişkili özellikleri belirten bir dış görünüm dosyası olacaktır.

Çözüm Gezgini proje adına sağ tıklayıp yeni öğe Ekle ' yi seçerek `GridView.skin` adlı projenize yeni bir kaplama dosyası ekleyerek başlayın.

[![GridView. Skin adlı bir dış görünüm dosyası ekleyin](displaying-data-with-the-objectdatasource-cs/_static/image24.png)](displaying-data-with-the-objectdatasource-cs/_static/image23.png)

**Şekil 9**: `GridView.skin` adlı bir dış görünüm dosyası ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image25.png))

Dış görünüm dosyalarının, `App_Themes` klasöründe bulunan bir temaya yerleştirilmesi gerekir. Henüz böyle bir klasörünüz olmadığı için, Visual Studio ilk dış görünümümüzü eklerken bizim için bir tane oluşturmak üzere önereceğiz. `App_Theme` klasörünü oluşturmak için Evet ' i tıklatın ve yeni `GridView.skin` dosyasını buraya yerleştirin.

[![Visual Studio 'Nun App_Theme klasörünü oluşturmasına Izin ver](displaying-data-with-the-objectdatasource-cs/_static/image27.png)](displaying-data-with-the-objectdatasource-cs/_static/image26.png)

**Şekil 10**: Visual Studio 'Nun `App_Theme` klasörünü oluşturmasına izin ver ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image28.png))

Bu, Skin adlı `App_Themes` klasöründe `GridView.skin`kaplama dosyası ile yeni bir tema oluşturur.

![GridView teması App_Theme klasörüne eklendi](displaying-data-with-the-objectdatasource-cs/_static/image29.png)

**Şekil 11**: GridView teması `App_Theme` klasörüne eklenmiştir

GridView temasını DataWebControls olarak yeniden adlandırın (`App_Theme` klasöründeki GridView klasörüne sağ tıklayın ve yeniden adlandır ' ı seçin. Sonra, `GridView.skin` dosyasına aşağıdaki biçimlendirmeyi girin:

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample3.aspx)]

Bu, DataWebControls temasını kullanan herhangi bir sayfada tüm GridView için `CssClass`ile ilgili özelliklerin varsayılan özelliklerini tanımlar. Daha kısa bir süre içinde kullanacağınız bir veri Web denetimi olan DetailsView için başka bir kaplama ekleyelim. `DetailsView.skin` adlı DataWebControls Theme öğesine yeni bir kaplama ekleyin ve aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample4.aspx)]

Temamız tanımlı, son adım temayı ASP.NET sayfamıza uygulayacaksınız. Bir tema, sayfa temelinde veya bir Web sitesindeki tüm sayfalar için uygulanabilir. Bu temayı Web sitesindeki tüm sayfalar için kullanalım. Bunu gerçekleştirmek için, `Web.config``<system.web>` bölümüne aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](displaying-data-with-the-objectdatasource-cs/samples/sample5.xml)]

İşte bu kadar kolay! `styleSheetTheme` ayarı, temada belirtilen özelliklerin Denetim düzeyinde belirtilen *özellikleri geçersiz kılmayacağını gösterir* . Tema ayarlarının koz denetim ayarlarına sahip olması gerektiğini belirtmek için, `styleSheetTheme`yerine `theme` özniteliğini kullanın; Ne yazık ki `theme` özniteliği aracılığıyla belirtilen tema ayarları Visual Studio Tasarım görünümü görünmez. Temalar ve kaplamalar hakkında daha fazla bilgi için Temalar kullanılarak [ASP.net Temalar ve dış görünümler 'e genel bakış](https://msdn.microsoft.com/library/ykzx33wh.aspx) ve [sunucu tarafı biçemlerini](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx) inceleyin; bkz. nasıl yapılır: bir temayı kullanmak için bir sayfa yapılandırma hakkında daha fazla bilgi için [ASP.net temalarını uygulama](https://msdn.microsoft.com/library/0yy5hxdk(VS.80).aspx) .

[GridView ![ürünün adını, kategorisini, tedarikçisine, fiyatını ve Discontinued bilgilerini görüntüler](displaying-data-with-the-objectdatasource-cs/_static/image31.png)](displaying-data-with-the-objectdatasource-cs/_static/image30.png)

**Şekil 12**: GridView ürünün adını, kategorisini, tedarikçisine, fiyatını ve Discontinued bilgilerini görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image32.png))

## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>DetailsView 'da tek seferde bir kayıt görüntüleme

GridView, bağlandığı veri kaynağı denetimi tarafından döndürülen her bir kayıt için bir satır görüntüler. Ancak, tek seferde tek bir kayıt veya yalnızca bir kayıt göstermek isteyebileceğiniz zamanlar olabilir. [DetailsView denetimi](https://msdn.microsoft.com/library/s3w1w7t4.aspx) bu işlevselliği sunarak, iki sütunlu bir HTML `<table>` ve denetime göre her bir sütun veya özellik için bir satır olarak işleme sağlar. DetailsView 'ı tek bir kayıt 90 derece döndürülmüş bir GridView olarak düşünebilirsiniz.

`SimpleDisplay.aspx`GridView 'un *üstüne* bir DetailsView denetimi ekleyerek başlayın. Ardından, GridView ile aynı ObjectDataSource denetimine bağlayın. GridView ile benzer şekilde, ObjectDataSource 'un `Select` yöntemi tarafından döndürülen nesnedeki her bir özellik için DetailsView 'a bir BoundField eklenecektir. Tek fark, DetailsView 'un BoundFields alanlarının dikey yerine yatay olarak yerleştirilme amaçlıdır.

[Sayfaya bir DetailsView eklemek ve bu öğeyi ObjectDataSource 'a bağlamak ![](displaying-data-with-the-objectdatasource-cs/_static/image34.png)](displaying-data-with-the-objectdatasource-cs/_static/image33.png)

**Şekil 13**: sayfaya bir DetailsView ekleyin ve bunu ObjectDataSource 'a bağlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image35.png))

GridView gibi, DetailsView tarafından döndürülen verilerin daha özelleştirilmiş bir görünümünü sağlamak için DetailsView 'un BoundFields alanları tweaked olabilir. Şekil 14 ' te, ' ın BoundFields öğesinden sonra, görünümü GridView örneğine benzer hale getirmek üzere yapılandırıldıktan `CssClass` özellikleri görüntülenir.

[DetailsView ![tek bir kayıt gösterir](displaying-data-with-the-objectdatasource-cs/_static/image37.png)](displaying-data-with-the-objectdatasource-cs/_static/image36.png)

**Şekil 14**: DetailsView tek bir kayıt gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image38.png))

DetailsView 'un yalnızca veri kaynağı tarafından döndürülen ilk kaydı görüntülediğini unutmayın. Kullanıcının tüm kayıtlarda tek seferde ilerme yapmasına izin vermek için, DetailsView için sayfalama 'yi etkinleştirmemiz gerekir. Bunu yapmak için, Visual Studio 'ya dönün ve DetailsView 'un akıllı etiketindeki disk belleğini etkinleştir onay kutusunu işaretleyin.

[DetailsView denetiminde Sayfalamayı etkinleştirmek ![](displaying-data-with-the-objectdatasource-cs/_static/image40.png)](displaying-data-with-the-objectdatasource-cs/_static/image39.png)

**Şekil 15**: DetailsView denetiminde sayfalamayı etkinleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image41.png))

[Sayfalama etkinken ![, DetailsView kullanıcının ürünleri görüntülemesini sağlar](displaying-data-with-the-objectdatasource-cs/_static/image43.png)](displaying-data-with-the-objectdatasource-cs/_static/image42.png)

**Şekil 16**: sayfalama etkinken, DetailsView kullanıcının ürünlerden herhangi birini görüntülemesine olanak tanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image44.png))

Sonraki öğreticilerde sayfalama hakkında daha fazla bilgi edineceksiniz.

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>Tek seferde bir kayıt göstermek için daha esnek bir düzen

DetailsView, ObjectDataSource 'tan döndürülen her bir kaydı görüntüleme konusunda oldukça isgıd ' dir. Verilerin daha esnek bir görünümünü isteyebilir. Örneğin, ürünün adı, kategorisi, tedarikçi, Fiyat ve Discontinued bilgilerini her biri ayrı bir satırda göstermek yerine, ürün adını ve fiyatını bir `<h4>` başlığında göstermek isteyebilir ve daha küçük bir yazı tipi boyutunda ad ve fiyat altında görünen kategori ve tedarikçi bilgileri. Ve değerlerin yanındaki özellik adlarını (ürün, kategori, vb.) gösterebiliriz.

[FormView denetimi](https://msdn.microsoft.com/library/fyf1dk77.aspx) bu özelleştirme düzeyini sağlar. FormView, alanları (GridView ve DetailsView gibi) kullanmak yerine, Web denetimleri, statik HTML ve [veri bağlama sözdiziminin](http://www.15seconds.com/issue/040630.htm)bir karışımını sağlayan şablonlar kullanır. ASP.NET 1. x öğesinden Yineleyici denetimini biliyorsanız, tek bir kayıt göstermek için FormView 'u Yineleyici olarak düşünebilirsiniz.

`SimpleDisplay.aspx` sayfanın tasarım yüzeyine bir FormView denetimi ekleyin. İlk olarak FormView, en azından denetim `ItemTemplate`sunmamız gerektiğini bildiren gri bir blok olarak görüntülenir.

[FormView bir ItemTemplate Içermelidir ![](displaying-data-with-the-objectdatasource-cs/_static/image46.png)](displaying-data-with-the-objectdatasource-cs/_static/image45.png)

**Şekil 17**: FormView bir `ItemTemplate` içermelidir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image47.png))

FormView 'un akıllı etiketi aracılığıyla doğrudan bir veri kaynağı denetimine bağlayabilirsiniz. Bu, varsayılan bir `ItemTemplate` otomatik olarak (`EditItemTemplate` ve `InsertItemTemplate`, ObjectDataSource denetiminin `InsertMethod` ve `UpdateMethod` özellikleri ayarlandıysa) otomatik olarak oluşturur. Ancak, bu örnek için verileri FormView 'a bağlayabilir ve `ItemTemplate` el ile belirtelim. FormView 'un `DataSourceID` özelliğini, ObjectDataSource denetiminin `ID` `ObjectDataSource1`ayarlayarak başlatın. Daha sonra, ürünün adını ve fiyatını bir `<h4>` öğesinde, daha küçük bir yazı tipi boyutunda bulunan kategori ve nakliyeci adlarını görüntüleyecek şekilde `ItemTemplate` oluşturun.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample6.aspx)]

[![Ilk ürün (Chai) özel bir biçimde görüntülenir](displaying-data-with-the-objectdatasource-cs/_static/image49.png)](displaying-data-with-the-objectdatasource-cs/_static/image48.png)

**Şekil 18**: ilk ürün (Chai) özel bir biçimde görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-objectdatasource-cs/_static/image50.png))

`<%# Eval(propertyName) %>`, veri bağlama sözdizimidir. `Eval` yöntemi, FormView denetimine bağlanmakta olan geçerli nesne için belirtilen özelliğin değerini döndürür. Bağlama ve veri bağlama hakkında daha fazla bilgi için ASP.NET 2,0 'teki Alex Homer 'ın [Basitleştirilmiş ve genişletilmiş veri bağlama söz dizimi](http://www.15seconds.com/issue/040630.htm) makalesine göz atın.

DetailsView gibi, FormView yalnızca ObjectDataSource 'tan döndürülen ilk kaydı gösterir. Ziyaretçilerin ürünlerin her seferinde bir kez ilerkullanmasına izin vermek için FormView 'da sayfalama özelliğini etkinleştirebilirsiniz.

## <a name="summary"></a>Özet

ASP.NET 2.0 'ın ObjectDataSource denetimine teşekkürler bir kod satırı yazmadan bir Iş mantığı katmanının verilerine erişme ve veri görüntüleme gerçekleştirebilirsiniz. ObjectDataSource bir sınıfın belirtilen yöntemini çağırır ve sonuçları döndürür. Bu sonuçlar, ObjectDataSource 'a bağlanan bir veri Web denetiminde görüntülenebilir. Bu öğreticide, GridView, DetailsView ve FormView denetimlerini ObjectDataSource 'a bağlamayı inceledik.

Şimdiye kadar, yalnızca bir parametre-daha az yöntemi çağırmak için ObjectDataSource 'un nasıl kullanılacağını gördünüz, ancak `ProductBLL` sınıfının `GetProductsByCategoryID(categoryID)`gibi giriş parametrelerini bekleyen bir yöntemi çağırmak istiyoruz? Bir veya daha fazla parametre bekleyen bir yöntemi çağırmak için, bu parametrelerin değerlerini belirtmek üzere ObjectDataSource 'ı yapılandırmamız gerekir. Bunu bir [sonraki öğreticimizde](declarative-parameters-cs.md)nasıl gerçekleştireceğinizi öğreneceğiz.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Kendi veri kaynağı denetimlerinizi oluşturun](https://msdn.microsoft.com/library/ms364049.aspx)
- [ASP.NET 2,0 için GridView örnekleri](https://msdn.microsoft.com/library/aa479339.aspx)
- [ASP.NET 2,0 ' de Basitleştirilmiş ve genişletilmiş veri bağlama söz dizimi](http://www.15seconds.com/issue/040630.htm)
- [ASP.NET 2,0 içinde Temalar](http://www.odetocode.com/Articles/423.aspx)
- [Temaları kullanan sunucu tarafı stilleri](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [Nasıl yapılır: program aracılığıyla ASP.NET temalarını uygulama](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](declarative-parameters-cs.md)
