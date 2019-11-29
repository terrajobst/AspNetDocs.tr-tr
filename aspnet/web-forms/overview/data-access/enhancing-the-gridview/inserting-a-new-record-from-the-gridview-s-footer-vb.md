---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
title: GridView 'un altbilgisine yeni bir kayıt ekleme (VB) | Microsoft Docs
author: rick-anderson
description: GridView denetimi, yeni bir veri kaydı eklemek için yerleşik destek sağlamayana, bu öğreticide bir... eklemek için GridView 'un nasıl artırılması gösterilmektedir.
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 528acc48-f20c-4b4e-aa16-4cc02f068ebb
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: 67ef370a90bc843f5c2da80bb43c8ef8de216b51
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74631659"
---
# <a name="inserting-a-new-record-from-the-gridviews-footer-vb"></a>GridView'ın Alt Bilgisinden Yeni Kayıt Ekleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_VB.exe) veya [PDF 'yi indirin](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/datatutorial53vb1.pdf)

> GridView denetimi, yeni bir veri kaydı eklemek için yerleşik destek sunmadığından, bu öğreticide ekleme arabirimi eklemek için GridView 'un nasıl artırılması gösterilmektedir.

## <a name="introduction"></a>Giriş

Veri öğreticisini [ekleme, güncelleştirme ve silmeye genel bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) konusunda açıklandığı gibi, GridView, DetailsView ve FormView Web denetimleri, yerleşik veri değiştirme yeteneklerini içerir. Bildirim temelli veri kaynağı denetimleriyle kullanıldığında, bu üç Web denetimi, tek bir kod satırı yazmak zorunda kalmadan verileri değiştirmek için hızlı ve kolay bir şekilde yapılandırılabilir. Ne yazık ki, yalnızca DetailsView ve FormView denetimleri yerleşik ekleme, düzenlenme ve silme özellikleri sağlar. GridView yalnızca Düzenle ve silme desteği sunar. Ancak, küçük bir dirsek Grease ile GridView 'u bir ekleme arabirimi içerecek şekilde artırabilir.

GridView 'a ekleme özellikleri ekleme konusunda, yeni kayıtların nasıl ekleneceğini, ekleme arabiriminin oluşturulmasına ve yeni kaydı eklemek için kodun yazılmasına karar vermekten sorumludur. Bu öğreticide, ekleme arabirimini GridView s Altbilgi satırına ekleme (bkz. Şekil 1) konusuna bakacağız. Her bir sütunun altbilgi hücresi, uygun veri toplama Kullanıcı arabirimi öğesini (ürün adı için bir metin kutusu, tedarikçi için bir DropDownList vb.) içerir. Ayrıca, tıklandığı zaman bir ekleme düğmesi için bir sütun gerekir ve bu da alt bilgi satırında verilen değerleri kullanarak `Products` tabloya yeni bir kayıt ekler.

[Alt bilgi satırı ![yeni ürünler eklemek için bir arabirim sağlar](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.png)

**Şekil 1**: alt bilgi satırı, yeni ürünler eklemek Için bir arabirim sağlar ([tam boyutlu görüntüyü görüntülemek için tıklatın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.png))

## <a name="step-1-displaying-product-information-in-a-gridview"></a>1\. Adım: GridView 'da ürün bilgilerini görüntüleme

GridView s altbilgisinde ekleme arabirimi oluşturmaya kendimize sorun yapmadan önce, ilk olarak veritabanındaki ürünleri listeleyen sayfaya bir GridView eklemeye odaklanalım. ' I `EnhancedGridView` klasöründeki `InsertThroughFooter.aspx` sayfasını açıp araç kutusu ' ndan tasarımcı üzerine sürükleyerek GridView s `ID` özelliğini `Products`olarak ayarlayarak başlayın. Sonra, `ProductsDataSource`adlı yeni bir ObjectDataSource 'a bağlamak için GridView s akıllı etiketini kullanın.

[![ProductsDataSource adlı yeni bir ObjectDataSource oluşturma](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.png)

**Şekil 2**: `ProductsDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.png))

ObjectDataSource 'ı, ürün bilgilerini almak için `ProductsBLL` sınıf s `GetProducts()` metodunu kullanacak şekilde yapılandırın. Bu öğreticide, ekleme özellikleri ekleme ve düzenlememe ve silme konusunda endişelenmenize gerek kalmaz. Bu nedenle, Ekle sekmesindeki açılan listenin `AddProduct()` olarak ayarlandığından ve UPDATE ve DELETE sekmelerindeki açılan listelerin (None) olarak ayarlandığından emin olun.

[AddProduct metodunu ObjectDataSource s Insert () yöntemine eşleyin ![](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.png)

**Şekil 3**: `AddProduct` yöntemini ObjectDataSource s `Insert()` yöntemine eşleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.png))

[![sekmeleri GÜNCELLEŞTIR ve SIL aşağı açılan listelerini (yok) olarak ayarlayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.png)

**Şekil 4**: GÜNCELLEŞTIRME ve silme sekmeleri açılan listesini ayarlama (yok) ([tam boyutlu görüntüyü görüntülemek için tıklatın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.png))

ObjectDataSource s veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio ilgili veri alanlarının her biri için GridView 'a alanları otomatik olarak ekler. Şimdilik, Visual Studio tarafından eklenen tüm alanları bırakın. Bu öğreticinin ilerleyen kısımlarında geri döneceğiz ve yeni bir kayıt eklenirken değerlerinin belirtilmemesi gereken bazı alanları kaldıracağız.

Veritabanında 80 ürüne yakın bir işlem olduğundan, bir kullanıcının yeni bir kayıt eklemek için Web sayfasının en altına doğru bir şekilde kaymanız gerekir. Bu nedenle, ekleme arabirimini daha görünür ve erişilebilir hale getirmek için sayfalama 'yi etkinleştirin. Sayfalama özelliğini açmak için GridView s akıllı etiketinden sayfalama etkinleştir onay kutusunu işaretleyin.

Bu noktada, GridView ve ObjectDataSource 'un bildirim temelli işaretlemesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample1.aspx)]

[![tüm ürün verileri alanları Sayfalanmış bir GridView 'da görüntülenir](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.png)

**Şekil 5**: tüm ürün verileri alanları Sayfalanmış bir GridView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.png))

## <a name="step-2-adding-a-footer-row"></a>2\. Adım: alt bilgi satırı ekleme

Başlık ve veri satırlarıyla birlikte, GridView bir altbilgi satırı içerir. Üstbilgi ve altbilgi satırları, GridView s [`ShowHeader`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showheader.aspx) ve [`ShowFooter`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showfooter.aspx) özelliklerinin değerlerine göre görüntülenir. Altbilgi satırını göstermek için `ShowFooter` özelliğini `True`olarak ayarlamanız yeterlidir. Şekil 6 ' da gösterildiği gibi, `ShowFooter` özelliğinin `True` olarak ayarlanması kılavuza bir altbilgi satırı ekler.

[Altbilgi satırını göstermek Için ![, ShowFooter öğesini true olarak ayarlayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.png)

**Şekil 6**: alt bilgi satırını görüntülemek için `ShowFooter` `True` olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.png))

Altbilgi satırının koyu kırmızı bir arka plan rengi olduğunu unutmayın. Bunun nedeni, oluşturma ve bulma [öğreticisiyle verileri görüntüleme](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) içindeki tüm sayfalara geri Uygulandığımız veri WebControls temasıdır. Özellikle `GridView.skin` dosyası, `FooterStyle` CSS sınıfını kullanan `FooterStyle` özelliğini yapılandırır. `FooterStyle` sınıfı `Styles.css` aşağıdaki gibi tanımlanır:

[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample2.css)]

> [!NOTE]
> Önceki öğreticilerdeki GridView s altbilgi satırını kullanarak araştırıyoruz. Gerekirse, bir Yenileyici için [GridView 'un altbilgi öğreticisindeki Özet bilgilerini görüntüleme](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) bölümüne geri dönün.

`ShowFooter` özelliğini `True`ayarladıktan sonra, çıktıyı bir tarayıcıda görüntülemek için bir dakikanızı ayırın. Şu anda altbilgi satırı herhangi bir metin veya Web denetimi içermiyor. 3\. adımda her bir GridView alanı için, uygun ekleme arabirimini içermesi için altbilgiyi değiştireceksiniz.

[Boş altbilgi satırı ![disk belleği arabirimi denetimlerinin üzerinde görüntülenir](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image13.png)

**Şekil 7**: boş alt bilgi satırı, sayfalama arabirimi denetimlerinin üzerinde görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image14.png))

## <a name="step-3-customizing-the-footer-row"></a>3\. Adım: altbilgi satırını özelleştirme

[GridView denetim öğreticisindeki Templatefields kullanarak](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) geri döndüğünüzde, Templatefields (boundfields veya checkboxfields yerine) kullanarak belirli bir GridView sütununun görüntülenmesini büyük ölçüde özelleştirmeyi gördük. [veri değişikliği arabirimini özelleştirme bölümünde,](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) bir GridView 'da Düzenle arabirimini özelleştirmek Için templatefields kullanma konusunda baktık. Bir TemplateField 'ın, belirli satır türlerinde kullanılan biçimlendirme, Web denetimleri ve veri bağlama sözdiziminin karışımını tanımlayan bir dizi şablondan oluştuğunu hatırlayın. `ItemTemplate`, örneğin, salt okuma satırları için kullanılan şablonu belirtir, `EditItemTemplate` düzenlenebilir satır için şablonu tanımlar.

`ItemTemplate` ve `EditItemTemplate`birlikte, TemplateField da altbilgi satırı için içerik belirten bir `FooterTemplate` içerir. Bu nedenle, `FooterTemplate`arabirim ekleyen her bir alan için gereken Web denetimlerini ekleyebiliriz. Başlamak için GridView 'daki tüm alanları TemplateFields 'e dönüştürün. Bu işlem, GridView s akıllı etiketindeki sütunları düzenle bağlantısına tıklanarak, sol alt köşedeki her bir alanı seçerek ve bu alanı bir TemplateField öğesine Dönüştür bağlantısına tıklayarak yapılabilir.

![Her alanı bir TemplateField öğesine Dönüştür](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.gif)

**Şekil 8**: her alanı bir TemplateField öğesine Dönüştür

Bu alanı bir TemplateField öğesine Dönüştür öğesine tıkladığınızda, geçerli alan türü bir eşdeğer TemplateField 'a döner. Örneğin, her bir BoundField, karşılık gelen veri alanını ve bir metin kutusundaki veri alanını görüntüleyen bir `EditItemTemplate` görüntüleyen bir etiketi içeren `ItemTemplate` bir TemplateField ile değiştirilmiştir. `ProductName` BoundField, aşağıdaki TemplateField biçimlendirmesine dönüştürüldü:

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample3.aspx)]

Benzer şekilde, `Discontinued` CheckBoxField, `ItemTemplate` ve `EditItemTemplate` onay kutusu Web denetimi içeren bir TemplateField 'a dönüştürüldü (`ItemTemplate` s CheckBox devre dışı bırakılır). `ProductID` BoundField salt okunurdur `ItemTemplate` ve `EditItemTemplate`etiket denetimiyle bir TemplateField 'a dönüştürüldü. Kısacası, mevcut bir GridView alanını TemplateField 'a dönüştürmek, mevcut alan işlevselliğinin hiçbirini kaybetmeden daha özelleştirilebilir TemplateField 'a geçiş yapmanın hızlı ve kolay bir yoludur.

Bu GridView, Düzenle desteği ile çalıştık ve yalnızca `ItemTemplate`bırakarak her TemplateField `EditItemTemplate` kaldırmayı ücretsiz hale gelmekten çekinmeyin. Bunu yaptıktan sonra, GridView s bildirim temelli işaretlerinizin aşağıdaki gibi görünmesi gerekir:

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample4.aspx)]

Her GridView alanı bir TemplateField 'a dönüştürüldüğünden, `FooterTemplate`her bir alana uygun ekleme arabirimini girebiliriz. Bazı alanlar ekleme arabirimine sahip olmayacaktır (`ProductID`, örneğin,); Diğerleri, yeni ürün bilgilerini toplamak için kullanılan Web denetimlerinde farklılık gösterecektir.

Düzenleme arabirimini oluşturmak için GridView s akıllı etiketinden Şablonları Düzenle bağlantısını seçin. Ardından, aşağı açılan listeden uygun alanı `FooterTemplate` seçin ve araç kutusundan uygun denetimi Tasarımcı üzerine sürükleyin.

[Her bir alan için uygun ekleme arabirimini ![ekleyin](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image15.png)

**Şekil 9**: her alan Için uygun ekleme arabirimini ekleyin `FooterTemplate` ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image16.png))

Aşağıdaki madde işaretli liste, eklenecek ekleme arabirimini belirterek GridView alanlarını numaralandırır:

- `ProductID` yok.
- `ProductName` metin kutusu ekleyin ve `ID` `NewProductName`olarak ayarlayın. Kullanıcının yeni ürün adı için bir değer girdiğinden emin olmak için bir RequiredFieldValidator denetimi de ekleyin.
- `SupplierID` yok.
- `CategoryID` yok.
- `QuantityPerUnit` metin kutusu ekleyin ve `ID` `NewQuantityPerUnit`olarak ayarlar.
- `UnitPrice`, girilen değerin sıfıra eşit veya daha büyük bir para birimi değeri olmasını sağlayan `NewUnitPrice` adlı bir metin kutusu ve bir CompareValidator ekleyin.
- `UnitsInStock`, `ID` `NewUnitsInStock`olarak ayarlanmış bir metin kutusunu kullanın. Girilen değerin sıfırdan büyük veya sıfıra eşit bir tamsayı değeri olmasını sağlayan bir CompareValidator ekleyin.
- `UnitsOnOrder`, `ID` `NewUnitsOnOrder`olarak ayarlanmış bir metin kutusunu kullanın. Girilen değerin sıfırdan büyük veya sıfıra eşit bir tamsayı değeri olmasını sağlayan bir CompareValidator ekleyin.
- `ReorderLevel`, `ID` `NewReorderLevel`olarak ayarlanmış bir metin kutusunu kullanın. Girilen değerin sıfırdan büyük veya sıfıra eşit bir tamsayı değeri olmasını sağlayan bir CompareValidator ekleyin.
- `Discontinued` bir onay kutusu ekleyin ve `ID` `NewDiscontinued`olarak ayarlar.
- `CategoryName` bir DropDownList ekleyin ve `ID` `NewCategoryID`olarak ayarlayın. `CategoriesDataSource` adlı yeni bir ObjectDataSource 'a bağlayın ve `CategoriesBLL` Class s `GetCategories()` metodunu kullanacak şekilde yapılandırın. `CategoryName` veri alanını, değerleri olarak `CategoryID` veri alanını kullanarak, DropDownList s `ListItem` s.
- `SupplierName` bir DropDownList ekleyin ve `ID` `NewSupplierID`olarak ayarlayın. `SuppliersDataSource` adlı yeni bir ObjectDataSource 'a bağlayın ve `SuppliersBLL` Class s `GetSuppliers()` metodunu kullanacak şekilde yapılandırın. `CompanyName` veri alanını, değerleri olarak `SupplierID` veri alanını kullanarak, DropDownList s `ListItem` s.

Doğrulama denetimlerinin her biri için `ForeColor` özelliğini temizleyerek, `FooterStyle` CSS sınıfının beyaz ön plan renginin varsayılan kırmızı yerine kullanılabilmesi gerekir. Ayrıca, ayrıntılı bir açıklama için `ErrorMessage` özelliğini kullanın, ancak `Text` özelliğini bir yıldız işareti olarak ayarlayın. Doğrulama denetimi metninin, ekleme arabiriminin iki satıra kaydırılmasına neden olmasını engellemek için, bir doğrulama denetimi kullanan her bir `FooterTemplate` s için `FooterStyle` s `Wrap` özelliğini false olarak ayarlayın. Son olarak, GridView 'un altına bir ValidationSummary denetimi ekleyin ve `ShowMessageBox` özelliğini `True` ve `ShowSummary` özelliğini `False`olarak ayarlayın.

Yeni bir ürün eklerken `CategoryID` ve `SupplierID`sağlamamız gerekir. Bu bilgiler, `CategoryName` ve `SupplierName` alanları için alt bilgi hücrelerindeki DropDownLists aracılığıyla yakalanır. Bu alanları `CategoryID` ve `SupplierID` TemplateFields olarak kullanmayı seçtim, çünkü kılavuz s veri satırlarında Kullanıcı, KIMLIK değerleri yerine kategori ve Tedarikçi adlarını görmeye daha fazla ilgi çekiyor. `CategoryID` ve `SupplierID` değerleri artık `CategoryName` ve `SupplierName` alan arabirim ekleme yaptığından, GridView 'dan `CategoryID` ve `SupplierID` TemplateFields alanlarını kaldırabiliriz.

Benzer şekilde, yeni bir ürün eklenirken `ProductID` de `ProductID` TemplateField da kaldırılabilir. Bununla birlikte, s `ProductID` alanı kılavuzda yer bırakalım. Ekleme arabirimini oluşturan TextBoxes, DropDownLists, CheckBox ve doğrulama denetimlerine ek olarak, tıklandığı sırada yeni ürünü veritabanına ekleme mantığını gerçekleştiren bir Ekle düğmesine de ihtiyacımız vardır. 4\. adımda, `ProductID` TemplateField s `FooterTemplate`ekleme arabirimine bir Ekle düğmesi ekleyeceğiz.

Çeşitli GridView alanlarının görünümünü geliştirmek için ücretsizdir. Örneğin, `UnitPrice` değerlerini bir para birimi olarak biçimlendirmek, `UnitsInStock`, `UnitsOnOrder`ve `ReorderLevel` alanlarını sağa hizalamak ve TemplateFields için `HeaderText` değerlerini güncellemek isteyebilirsiniz.

`FooterTemplate` s ' de arabirim ekleme, `SupplierID`ve `CategoryID` TemplateFields 'i oluşturma ve TemplateFields biçimlendirme ve hizalama aracılığıyla kılavuzun aestezlerinin geliştirilmesi için, GridView s bildirime dayalı işaretlerinizin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample5.aspx)]

Bir tarayıcıdan görüntülendiğinde, GridView s altbilgi satırı artık tamamlanan ekleme arabirimini içerir (bkz. Şekil 10). Bu noktada ekleme arabirimi, kullanıcının yeni ürüne yönelik verileri girdikleri ve veritabanına yeni bir kayıt eklemek istediği anlamına gelir. Ayrıca, altbilgiye girilen verilerin `Products` veritabanında yeni bir kayda nasıl çevrileceğini adresliyoruz. 4\. adımda ekleme arabirimine Ekle düğmesinin nasıl ekleneceğini ve tıklandığı zaman geri gönderme sırasında kodun nasıl yürütüleceğini inceleyeceğiz. 5\. adım, altbilginin içindeki verileri kullanarak nasıl yeni bir kayıt ekleneceğini gösterir.

[GridView altbilgisi ![yeni bir kayıt eklemek için bir arabirim sağlar](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image17.png)

**Şekil 10**: GridView altbilgisi, yeni bir kayıt eklemek Için bir arabirim sağlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image18.png))

## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>4\. Adım: ekleme arabirimine Ekle düğmesi ekleme

Ekleme arabirimine bir yere Ekle düğmesi eklememiz gerekir, çünkü bu arabirim eklenen alt bilgi satırı, kullanıcının yeni ürün bilgilerini girmeyi tamamladığını belirtebileceği anlamına gelir. Bu, mevcut `FooterTemplate` s ' den birine yerleştirilebilir veya bu amaçla kılavuza yeni bir sütun ekleyebiliriz. Bu öğreticide, s `FooterTemplate``ProductID` TemplateField s alanına Ekle düğmesini yerleştirelim.

Tasarımcıdan, GridView s akıllı etiketindeki Şablonları Düzenle bağlantısına tıklayın ve ardından açılır listeden `ProductID` alan s `FooterTemplate` seçin. Şablon için bir düğme web denetimi (veya tercih ediyorsanız, bir LinkButton veya ImageButton) ekleyin, KIMLIĞINI `CommandName` `AddProduct`olarak ayarlayarak ve Şekil 11 ' de gösterildiği gibi eklemek için `Text` özelliğini girin.

[![Add düğmesini ProductID TemplateField s FooterTemplate 'e yerleştir](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image19.png)

**Şekil 11**: ekle düğmesini `ProductID` TemplateField s `FooterTemplate` yerleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image20.png))

Ekle düğmesini ekledikten sonra sayfayı bir tarayıcıda test edin. Ekleme arabirimindeki geçersiz verilerle Ekle düğmesine tıkladığınızda, geri gönderme işlemi kısa devre dışı olur ve ValidationSummary denetimi geçersiz verileri gösterir (bkz. Şekil 12). Uygun veriler girildiğinde, Ekle düğmesine tıklamak geri göndermeye neden olur. Ancak veritabanına hiçbir kayıt eklenmez. INSERT işlemini gerçekten gerçekleştirmek için bir kod yazmanız gerekir.

[ekleme arabiriminde geçersiz veri varsa, ekleme düğmesi ![geri gönderme işlemi kısa bir süre sonra yapılır](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image21.png)

**Şekil 12**: ekleme arabiriminde geçersiz veri varsa, Düğme Ekle geri gönderme işlemi kısa bir süre sonra yapılır ([tam boyutlu görüntüyü görüntülemek için tıklatın](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image22.png))

> [!NOTE]
> Ekleme arabirimindeki doğrulama denetimleri bir doğrulama grubuna atanmadı. Bu, ekleme arabirimi sayfada tek doğrulama denetimleri kümesi olduğu sürece sorunsuz bir şekilde çalışıyor. Bununla birlikte, sayfada başka doğrulama denetimleri (örneğin, kılavuz s Editing Interface) varsa, bu denetimleri belirli bir doğrulama grubuyla ilişkilendirmek için ekleme arabirimi ve Ekle düğmesine `ValidationGroup` özelliklerine ilişkin doğrulama denetimlerine aynı değer atanmalıdır. Bir sayfadaki doğrulama denetimlerini ve düğmelerini doğrulama gruplarına bölümleme hakkında daha fazla bilgi için bkz. [ASP.NET 2,0 ' de doğrulama denetimlerini ayırma](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx) .

## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>5\. Adım:`Products`tabloya yeni bir kayıt ekleme

GridView 'un yerleşik düzenlemeyle ilgili özelliklerini kullandığınızda, GridView, güncelleştirmeyi gerçekleştirmek için gereken tüm işleri otomatik olarak işler. Özellikle, Güncelleştir düğmesine tıklandığında, Düzenle ' ye girilen değerleri, ObjectDataSource s `UpdateParameters` koleksiyonundaki parametrelere kopyalar ve ObjectDataSource s `Update()` metodunu çağırarak güncelleştirme dışına açılır. GridView, ekleme için böyle yerleşik işlevsellik sağlamadığından, ObjectDataSource 'un `Insert()` yöntemini çağıran kodu uygulamalıdır ve değerleri ekleme arabiriminden ObjectDataSource s `InsertParameters` koleksiyonuna kopyalar.

Ekle düğmesi tıklandıktan sonra bu ekleme mantığı yürütülmelidir. [GridView 'Daki düğmelerde ekleme ve bu düğmelere yanıt verme](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb.md) konusunda anlatıldığı gibi, GridView 'da düğme, LinkButton veya ImageButton 'a tıklandığında, gridview s `RowCommand` olayı geri gönderme sırasında ateşlenir. Bu olay, düğme, LinkButton veya ImageButton 'ın Altbilgi satırına Ekle düğmesi veya GridView tarafından otomatik olarak eklenmi (sıralamayı etkinleştir seçili olduğunda her sütunun üst kısmında bulunan LinkButtons gibi) açıkça eklenip eklenmeyeceğini veya Sayfalama arabirimindeki bağlantı düğmeleri, sayfalama Etkinleştir seçildiğinde).

Bu nedenle, Ekle düğmesine tıklayarak kullanıcıya yanıt vermek için, GridView s `RowCommand` olayı için bir olay işleyicisi oluşturuyoruz. Bu olay, GridView 'da *herhangi bir* düğme, LinkButton veya ImageButton 'a tıklandığında, yalnızca olay işleyicisine geçirilen `CommandName` özelliği Add düğmesinin (ınsert) `CommandName` değerine eşleniyorsa önemli ekleme mantığı ile devam ediyoruz. Ayrıca, yalnızca doğrulama denetimleri geçerli verileri raporlamamız durumunda da ilerlemeniz gerekir. Buna uyum sağlamak için, `RowCommand` olayı için aşağıdaki kodla bir olay işleyicisi oluşturun:

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample6.vb)]

> [!NOTE]
> Olay işleyicisinin neden `Page.IsValid` özelliğini kontrol ettiğine neden olduğunu merak ediyor olabilirsiniz. Bu durumda, ekleme arabiriminde geçersiz veriler sağlanmışsa geri gönderme bastırılmaz mi? Bu varsayım, Kullanıcı JavaScript 'ı devre dışı bırakılmadığından veya istemci tarafı doğrulama mantığını aşmak için gereken adımları gerçekleştirmedikçe doğrudur. Kısacası, bir asla istemci tarafı doğrulamasından kesinlikle güvenmemelidir; verilerle çalışmadan önce her zaman geçerlilik için sunucu tarafı denetimi gerçekleştirilmelidir.

1\. adımda `Insert()` yöntemi `ProductsBLL` sınıf s `AddProduct` yöntemine eşlendiği için `ProductsDataSource` ObjectDataSource oluşturduk. Yeni kaydı `Products` tablosuna eklemek için, yalnızca ObjectDataSource s `Insert()` metodunu çağırabiliriz:

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample7.vb)]

`Insert()` yöntemi çağrıdığına göre, tüm kalan değerler, ekleme arabiriminden `ProductsBLL` sınıf s `AddProduct` metoduna geçirilen parametrelere kopyalanır. [Ekleme, güncelleştirme ve silme öğreticisiyle Ilişkili olayları inceledikten](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) sonra, bu, ObjectDataSource s `Inserting` olayından elde edilebilir. `Inserting` olayında, denetimleri `Products` GridView s altbilgi satırından programlı bir şekilde başvurmalı ve değerlerini `e.InputParameters` koleksiyonuna atacağız. Kullanıcı `ReorderLevel` metin kutusunu boş bırakma gibi bir değeri atladıysanız, veritabanına eklenen değerin `NULL`olması gerektiğini belirtmemiz gerekir. `AddProducts` yöntemi null yapılabilir veritabanı alanları için Nullable türler kabul ettiğinden, null yapılabilir bir tür kullanın ve değeri Kullanıcı girişinin atlanmasından sonra `Nothing` olarak ayarlayın.

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample8.vb)]

`Inserting` olay işleyicisi tamamlandığında, yeni kayıtlar GridView s altbilgi satırı aracılığıyla `Products` veritabanı tablosuna eklenebilir. Devam edin ve birkaç yeni ürün eklemeyi deneyin.

## <a name="enhancing-and-customizing-the-add-operation"></a>Ekleme Işlemini geliştirme ve özelleştirme

Şu anda, Ekle düğmesine tıklanması veritabanı tablosuna yeni bir kayıt ekliyor, ancak kaydın başarıyla eklendiği bir görsel geri bildirim sağlamıyor. İdeal olarak, bir etiket Web denetimi veya istemci tarafı uyarı kutusu, kullanıcıya ekleme işlemi başarılı ile tamamlandığını bildirir. Bunu okuyucu için bir alıştırma olarak bırakıyorum.

Bu öğreticide kullanılan GridView, listelenen ürünlere herhangi bir sıralama düzeni uygulamaz ve son kullanıcının verileri sıralamasına izin vermez. Sonuç olarak, kayıtlar, birincil anahtar alanı tarafından veritabanında oldukları gibi sıralanır. Her yeni kayıt son bir `ProductID` bir değere sahip olduğundan, her yeni ürün eklendiğinde kılavuzun sonuna bir eklenir. Bu nedenle, yeni bir kayıt eklendikten sonra kullanıcıyı GridView 'un son sayfasına otomatik olarak göndermek isteyebilirsiniz. Bu, kullanıcının GridView 'a bağladıktan sonra son sayfaya gönderilmesi gerektiğini belirtmek için `RowCommand` olay işleyicisinde `ProductsDataSource.Insert()` çağrısından sonra aşağıdaki kod satırı eklenerek gerçekleştirilebilir:

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample9.vb)]

`SendUserToLastPage` başlangıçta bir `False`değeri atanan sayfa düzeyi Boole değişkenidir. GridView s `DataBound` olay işleyicisinde, `SendUserToLastPage` false ise, `PageIndex` özelliği kullanıcıyı son sayfaya gönderecek şekilde güncelleştirilir.

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample10.vb)]

`PageIndex` özelliğinin, `DataBound` olay işleyicisinde ayarlandığı neden (`RowCommand` olay işleyicisine karşılık olarak), `RowCommand` olay işleyicisi yeni kaydı `Products` veritabanı tablosuna eklememiz durumunda olur. Bu nedenle, `RowCommand` olay işleyicisinde son sayfa dizini (`PageCount - 1`), yeni ürün eklenmeden *önce* son sayfa dizinini temsil eder. Eklenmekte olan ürünlerin büyük bölümü için, son sayfa dizini yeni ürün eklendikten sonra aynı olur. Ancak eklenen ürün yeni bir son sayfa dizini ile sonuçlanırsa, `RowCommand` olay işleyicisindeki `PageIndex` yanlış bir şekilde güncelleştirdiğimiz takdirde, yeni son sayfa dizininin aksine ikinci son sayfaya (yeni ürün eklemeden önce son sayfa dizini) yönlendirilirsiniz. `DataBound` olay işleyicisi yeni ürün eklendikten ve verileri kılavuza yeniden bağladıktan sonra, `PageIndex` özelliğini ayarlayarak doğru son sayfa dizinini yeniden aldığınızı biliyoruz.

Son olarak, bu öğreticide kullanılan GridView, yeni bir ürün eklemek için toplanması gereken alan sayısı nedeniyle oldukça geniştir. Bu genişlik nedeniyle, DetailsView s dikey düzeni tercih edilebilir. Daha az girdi toplanarak GridView s genel genişliği azaltılabilir. Belki de yeni bir ürün eklerken `UnitsOnOrder`, `UnitsInStock`ve `ReorderLevel` alanları toplamamıza gerek duyduk. Bu, bu alanların GridView 'dan kaldırılabileceği durumdur.

Toplanan verileri ayarlamak için şu iki yaklaşımdan birini kullanabiliriz:

- `UnitsOnOrder`, `UnitsInStock`ve `ReorderLevel` alanları için değer bekleyen `AddProduct` yöntemini kullanmaya devam edin. `Inserting` olay işleyicisinde, ekleme arabiriminden kaldırılmış olan bu girişler için kullanılacak sabit kodlanmış, varsayılan değerler sağlayın.
- `UnitsOnOrder`, `UnitsInStock`ve `ReorderLevel` alanları için giriş kabul etmayan `ProductsBLL` sınıfında `AddProduct` yönteminin yeni bir aşırı yüklemesini oluşturun. Ardından, ASP.NET sayfasında, bu yeni aşırı yüklemeyi kullanmak için ObjectDataSource 'u yapılandırın.

Her iki seçenek de eşit olarak çalışacaktır. Önceki öğreticilerde, `ProductsBLL` sınıf s `UpdateProduct` yöntemi için birden fazla aşırı yükleme oluşturan ikinci seçeneği kullandık.

## <a name="summary"></a>Özet

GridView, DetailsView ve FormView 'da bulunan yerleşik ekleme özelliklerine sahip değildir, ancak bir çaba ile altbilgi satırına ekleme arabirimi eklenebilir. Bir GridView 'da altbilgi satırını göstermek için `ShowFooter` özelliğini `True`olarak ayarlayın. Alt bilgi satırı içeriği, alanı TemplateField 'a dönüştürerek ve ekleme arabirimi `FooterTemplate`ekleyerek her alan için özelleştirilebilir. Bu öğreticide gördüğümüz gibi `FooterTemplate` düğme, metin kutuları, DropDownLists, onay kutuları, veri odaklı Web denetimlerini (DropDownLists gibi) doldurmak için veri kaynağı denetimleri ve doğrulama denetimleri içerebilir. Kullanıcı girişini toplama denetimleriyle birlikte, bir Add Button, LinkButton veya ImageButton gereklidir.

Ekle düğmesine tıklandığında, ekleme iş akışını başlatmak için ObjectDataSource s `Insert()` yöntemi çağrılır. Daha sonra ObjectDataSource, yapılandırılmış Insert metodunu (Bu öğreticide `ProductsBLL` sınıf s `AddProduct` yöntemi) çağırır. Çağrılan INSERT yönteminden önce, GridView s ekleme arabirimi ' nden, ObjectDataSource s `InsertParameters` koleksiyonuna değerleri kopyalamamız gerekir. Bu, ObjectDataSource s `Inserting` olay işleyicisindeki arabirim Web denetimlerine ekleme ile programlı olarak başvuruda bulunarak gerçekleştirilebilir.

Bu öğreticide, GridView s görünümünü geliştirmek için teknik bakış tekniklerimiz tamamlanır. Sonraki öğreticiler kümesi, görüntüler, PDF 'Ler, Word belgeleri gibi ikili verilerle ve veri Web denetimlerinde nasıl çalışabilmeniz incelenecektir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider olarak gözden geçiren, Bernadette Leigh. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Öncekini](adding-a-gridview-column-of-checkboxes-vb.md)
