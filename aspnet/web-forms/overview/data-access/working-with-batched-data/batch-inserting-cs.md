---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-cs
title: Toplu ekleme (C#) | Microsoft Docs
author: rick-anderson
description: Tek bir işlemde birden çok veritabanı kaydını eklemeyi öğrenin. Kullanıcı arabirimi katmanında, GridView 'un kullanıcının birden çok n girmesine izin verecek şekilde uzadık...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: cf025e08-48fc-4385-b176-8610aa7b5565
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-cs
msc.type: authoredcontent
ms.openlocfilehash: 5dc4d0b6ac9bf3aa2baa54fe9f5d4149494e47d2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74584762"
---
# <a name="batch-inserting-c"></a>Toplu Ekleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_CS.zip) veya [PDF 'yi indirin](batch-inserting-cs/_static/datatutorial66cs1.pdf)

> Tek bir işlemde birden çok veritabanı kaydını eklemeyi öğrenin. Kullanıcı arabirimi katmanında, GridView 'un, kullanıcının birden çok yeni kayıt girmelerini sağlayacak şekilde genişlettik. Veri erişim katmanında, tüm eklemelerin başarılı veya Tüm eklemelerin geri alındığından emin olmak için bir işlem içindeki birden fazla ekleme işlemini sardık.

## <a name="introduction"></a>Giriş

[Toplu güncelleştirme](batch-updating-cs.md) öğreticisinde, GridView denetimini birden çok kaydın düzenlenebildiği bir arabirimi sunacak şekilde özelleştirmeye baktık. Sayfayı ziyaret eden Kullanıcı bir dizi değişiklik yapabilir ve sonra tek bir düğme tıklamış olarak toplu güncelleştirme gerçekleştirebilir. Kullanıcıların çok sayıda kaydı tek bir noktada güncelleştirdikleri durumlar için, böyle bir arabirim, veri öğreticisini [ekleme, güncelleştirme ve silmeye genel bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) konusunda ilk olarak araştırılan varsayılan satır başına Düzenle özelliklerine kıyasla sayaçsız tıklama ve klavyeden fare bağlam anahtarlarını kaydedebilir.

Bu kavram, kayıt eklerken de uygulanabilir. Burada, Northwind Traders 'da belirli bir kategori için bir dizi ürün içeren tedarikçilerle genellikle sevkiyatlar aldığımızda düşünün. Örnek olarak, Tokyo Traders ' den farklı çay ve kahve ürünlerinin bir sevkiyatını alabiliriz. Bir Kullanıcı her seferinde bir DetailsView denetimi aracılığıyla altı ürüne girerse, aynı değer sayısını tekrar tekrar seçmek gerekir: aynı kategoriyi (Içecek), aynı tedarikçiyi (Tokyo Traders), aynı Discontinued değerini ( False) ve sipariş değeri (0) üzerinde aynı birimleri. Bu yinelenen veri girişi yalnızca zaman alabilir, ancak hatalara açıktır.

Az iş sayesinde, kullanıcının tedarikçiden ve kategoriye bir kez seçmesini sağlayan bir toplu iş ekleme arabirimi oluşturabilir, bir dizi ürün adı ve birim fiyatı girebilir ve sonra yeni ürünleri veritabanına eklemek için bir düğmeye tıklayabilirsiniz (bkz. Şekil 1). Her ürün eklendikçe `ProductName` ve `UnitPrice` veri alanlarına metin kutularına girilen değerler atanır, ancak `CategoryID` ve `SupplierID` değerleri, formun en üstündeki DropDownLists değerleri olarak atanır. `Discontinued` ve `UnitsOnOrder` değerleri sırasıyla `false` ve 0 ' ın sabit kodlanmış değerlerine ayarlanır.

[Batch ekleme arabirimini ![](batch-inserting-cs/_static/image2.png)](batch-inserting-cs/_static/image1.png)

**Şekil 1**: toplu ekleme arabirimi ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image3.png))

Bu öğreticide Şekil 1 ' de gösterilen Batch ekleme arabirimini uygulayan bir sayfa oluşturacağız. Önceki iki öğreticilerde olduğu gibi, bir işlemin kapsamındaki eklemeleri, Atomicity sağlamak için kaydıracağız. Haydi başlayın!

## <a name="step-1-creating-the-display-interface"></a>1\. Adım: görüntüleme arabirimi oluşturma

Bu öğretici, iki bölgeye bölünen tek bir sayfadan oluşur: bir görüntüleme bölgesi ve ekleme bölgesi. Bu adımda oluşturacağımız görüntüleme arabirimi, bir GridView 'daki ürünleri gösterir ve Işlem ürün sevkiyatı başlıklı bir düğme içerir. Bu düğmeye tıklandığında, görüntüleme arabirimi, Şekil 1 ' de gösterilen ekleme arabirimiyle değiştirilmiştir. Görüntüleme arabirimi, Sevkiyat veya Iptal düğmelerinden ürün Ekle ' ye tıkladıktan sonra döndürülür. 2\. adımda ekleme arabirimini oluşturacağız.

İki arabirime sahip bir sayfa oluştururken, tek seferde yalnızca biri görünebilir, her arabirim genellikle diğer denetimler için bir kapsayıcı görevi gören [panel Web denetimi](http://www.w3schools.com/aspnet/control_panel.asp)içine yerleştirilir. Bu nedenle sayfamız her bir arabirim için iki panel denetimine sahip olacaktır.

`BatchData` klasöründeki `BatchInsert.aspx` sayfasını açıp araç kutusu 'ndaki bir paneli tasarımcı üzerine sürükleyin (bkz. Şekil 2). Panel s `ID` özelliğini `DisplayInterface`olarak ayarlayın. Paneli tasarımcıya eklerken, `Height` ve `Width` özellikleri sırasıyla 50px ve 125px olarak ayarlanır. Bu özellik değerlerini Özellikler penceresi temizleyin.

[Araç kutusundan Tasarımcı üzerine bir panel sürükleyin ![](batch-inserting-cs/_static/image5.png)](batch-inserting-cs/_static/image4.png)

**Şekil 2**: araç kutusundan Tasarımcı üzerine bir panel sürükleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image6.png))

Sonra, bir düğme ve GridView denetimini panele sürükleyin. Düğme s `ID` özelliğini `ProcessShipment` ve `Text` özelliğine, ürün sevk Irsaliyesini Işleyecek şekilde ayarlayın. GridView s `ID` özelliğini `ProductsGrid` ve akıllı etiketinden `ProductsDataSource`adlı yeni bir ObjectDataSource 'a bağlayın. `ProductsBLL` sınıf s `GetProducts` yönteminden verileri çekmek için ObjectDataSource 'ı yapılandırın. Bu GridView yalnızca verileri göstermek için kullanıldığından, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden (hiçbiri) açılan listeleri ayarlayın. Veri kaynağını yapılandırma Sihirbazı 'nı gerçekleştirmek için son ' a tıklayın.

[![ProductsBLL Class s GetProducts yönteminden döndürülen verileri görüntüleme](batch-inserting-cs/_static/image8.png)](batch-inserting-cs/_static/image7.png)

**Şekil 3**: `ProductsBLL` Class s `GetProducts` yönteminden döndürülen verileri görüntüle ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image9.png))

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](batch-inserting-cs/_static/image11.png)](batch-inserting-cs/_static/image10.png)

**Şekil 4**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinden açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image12.png))

ObjectDataSource Sihirbazı 'nı tamamladıktan sonra, Visual Studio, ürün verileri alanları için BoundFields ve bir CheckBoxField ekleyecek. `ProductName`, `CategoryName`, `SupplierName`, `UnitPrice`ve `Discontinued` alanları hariç tümünü kaldırın. Aesthetic Characteristics özelleştirmelerini ücretsiz hale getirebilirsiniz. `UnitPrice` alanını bir para birimi değeri olarak biçimlendirmeye, alanları yeniden sınıflandırmaya ve alanların `HeaderText` değerlerinin birkaç yerine adlandırmaya karar verdim. GridView 'ı Ayrıca, GridView s akıllı etiketinde sayfalama etkinleştir ve sıralamayı etkinleştir onay kutularını işaretleyerek sayfalama ve sıralama desteğini içerecek şekilde yapılandırın.

Panel, düğme, GridView ve ObjectDataSource 'ı ekledikten ve GridView s alanlarını özelleştirirken, sayfa için bildirim temelli işaretleriniz şuna benzer olmalıdır:

[!code-aspx[Main](batch-inserting-cs/samples/sample1.aspx)]

Düğme ve GridView için biçimlendirmenin açılış ve kapanış `<asp:Panel>` etiketleri içinde göründüğünü unutmayın. Bu denetimler `DisplayInterface` paneli içinde olduğundan, panel s `Visible` özelliğini `false`olarak ayarlayarak onları gizleyebiliriz. 3\. adım, bir düğmeye yanıt olarak panel s `Visible` özelliğini programlı bir şekilde değiştirmeye, diğerini gizleyerek bir arabirim göstermeye yönelik olarak bakar.

Bir tarayıcıdan ilerleme durumunu görüntülemek için bir dakikanızı ayırın. Şekil 5 ' i gösterdiği gibi, bir GridView üzerinde, bir kerede on ürünü listeleyen bir Işlem ürün sevkiyat düğmesi görmeniz gerekir.

[GridView ![ürünleri listeler ve sıralama ve sayfalama özellikleri sunar](batch-inserting-cs/_static/image14.png)](batch-inserting-cs/_static/image13.png)

**Şekil 5**: GridView ürünleri listeler ve sıralama ve sayfalama özellikleri sunar ([tam boyutlu görüntüyü görüntülemek için tıklatın](batch-inserting-cs/_static/image15.png))

## <a name="step-2-creating-the-inserting-interface"></a>2\. Adım: ekleme arabirimi oluşturma

Görüntüleme arabirimi tamamlandıktan sonra ekleme arabirimini oluşturmaya hazırız. Bu öğreticide, s için tek bir tedarikçi ve kategori değeri isteyen bir ekleme arabirimi oluşturun ve ardından kullanıcının en fazla beş ürün adı ve birim fiyat değeri girmesine izin verin. Bu arabirim ile Kullanıcı, hepsi aynı kategori ve tedarikçiyi paylaştığı, ancak benzersiz ürün adları ve fiyatlarına sahip olan beş yeni ürüne eklenebilir.

Araç kutusu 'ndaki bir paneli tasarımcı üzerine sürükleyip, mevcut `DisplayInterface` panelinin altına yerleştirerek başlayın. Bu yeni eklenen bölmenin `ID` özelliğini `InsertingInterface` olarak ayarlayın ve `Visible` özelliğini `false`olarak ayarlayın. `InsertingInterface` panel s `Visible` özelliğini 3. adımdaki `true` olarak ayarlayan kodu ekleyeceğiz. Ayrıca, panel s `Height` ve `Width` özellik değerlerini de temizleyin.

Ardından şekil 1 ' de geri gösterilen ekleme arabirimini oluşturmamız gerekiyor. Bu arabirim çeşitli HTML teknikleri aracılığıyla oluşturulabilir, ancak büyük bir şekilde, dört sütunlu, yedi satırlık bir tablo kullanacağız.

> [!NOTE]
> HTML `<table>` öğeleri için biçimlendirme girerken kaynak görünümü kullanmayı tercih ediyorum. Visual Studio, tasarımcı aracılığıyla `<table>` öğeleri eklemeye yönelik araçlar içerirken, tasarımcı, `style` için sorulmayan ayarları biçimlendirmeye ekleme konusunda çok daha fazla şey görünüyor. `<table>` biçimlendirmeyi oluşturduktan sonra, Web denetimlerini eklemek ve özelliklerini ayarlamak için genellikle tasarımcıya geri dönirim. Önceden belirlenmiş sütunlar ve satırlar içeren tablolar oluştururken tablo [Web](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx) denetimi yerıne statik HTML kullanmayı tercih ediyorum; çünkü tablo Web denetimi Içine yerleştirilmiş Web denetimlerine yalnızca `FindControl("controlID")` düzeniyle erişilebilir. Ancak, Tablo Web denetimi programlı bir şekilde oluşturulabileceğinizden, dinamik boyutlardaki tablolar için Tablo Web denetimlerini (satırlar veya sütunları bir veritabanına veya Kullanıcı tarafından belirtilen ölçütlere göre) kullanır.

`InsertingInterface` panelinin `<asp:Panel>` etiketleri arasına aşağıdaki biçimlendirmeyi girin:

[!code-html[Main](batch-inserting-cs/samples/sample2.html)]

Bu `<table>` biçimlendirme henüz herhangi bir Web denetimi içermez, bu tür bir şekilde ekleyeceğiz. Her bir `<tr>` öğesinin belirli bir CSS sınıfı ayarını içerdiğini unutmayın: tedarikçinin ve kategori DropDownLists 'ın gideceği üst bilgi satırı için `BatchInsertHeaderRow`; Sevkiyat ve Iptal düğmelerinden ürünlerin ekleneceği alt bilgi satırı için `BatchInsertFooterRow`; ve, ürün ve birim fiyat metin kutusu denetimlerini içerecek olan satırların `BatchInsertRow` ve `BatchInsertAlternatingRow` değerleri. Ekleme arabirimine, bu öğreticiler genelinde kullanılan GridView ve DetailsView denetimlerine benzer bir görünüm vermek için `Styles.css` dosyasında karşılık gelen CSS sınıfları oluşturdum. Bu CSS sınıfları aşağıda gösterilmiştir.

[!code-css[Main](batch-inserting-cs/samples/sample3.css)]

Bu biçimlendirme girildiğinde Tasarım görünümü geri döndürün. Bu `<table>`, Şekil 6 ' da gösterildiği gibi, tasarımcıda dört sütunlu, yedi satırlık tablo olarak gösterilmelidir.

[![ekleme arabirimi dört sütunlu, yedi satırlık bir tablodan oluşur](batch-inserting-cs/_static/image17.png)](batch-inserting-cs/_static/image16.png)

**Şekil 6**: ekleme arabirimi dört sütunlu, yedi satırlık bir tablodan oluşur ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image18.png))

Şimdi ekleme arabirimine Web denetimleri eklemeye hazırsınız. Araç kutusundan iki DropDownLists öğesini, tablodaki ve kategori için bir tabloda bulunan uygun hücrelere sürükleyin.

Tedarikçinin DropDownList s `ID` özelliğini `Suppliers` olarak ayarlayın ve `SuppliersDataSource`adlı yeni bir ObjectDataSource 'a bağlayın. `SuppliersBLL` sınıf s `GetSuppliers` yönteminden verileri almak için yeni ObjectDataSource 'u yapılandırın ve GÜNCELLEŞTIRME sekmesi s açılan listesini (None) olarak ayarlayın. Sihirbazı tamamladığınızda son ' a tıklayın.

[![SuppliersBLL sınıfı s GetSuppliers metodunu kullanmak için ObjectDataSource 'ı yapılandırma](batch-inserting-cs/_static/image20.png)](batch-inserting-cs/_static/image19.png)

**Şekil 7**: `SuppliersBLL` sınıf s `GetSuppliers` metodunu ([tam boyutlu görüntüyü görüntülemek Için tıklayın](batch-inserting-cs/_static/image21.png)) kullanmak üzere ObjectDataSource 'ı yapılandırın

`Suppliers` DropDownList `CompanyName` veri alanını görüntülemesini ve `ListItem` s değerleri olarak `SupplierID` veri alanını kullanmasını sağlayabilirsiniz.

[![CompanyName veri alanını görüntüleyin ve SupplierID değerini değer olarak kullanın](batch-inserting-cs/_static/image23.png)](batch-inserting-cs/_static/image22.png)

**Şekil 8**: `CompanyName` veri alanını görüntüleyin ve değer olarak `SupplierID` kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image24.png))

İkinci DropDownList `Categories` adlandırın ve `CategoriesDataSource`adlı yeni bir ObjectDataSource 'a bağlayın. `CategoriesDataSource` ObjectDataSource 'ı `CategoriesBLL` Class s `GetCategories` metodunu kullanacak şekilde yapılandırın; GÜNCELLEŞTIRME ve SILME sekmelerinden açılan listeleri (yok) olarak ayarlayın ve Sihirbazı tamamladıktan sonra son ' a tıklayın. Son olarak, DropDownList 'ın `CategoryName` veri alanını göstermesini ve `CategoryID` değer olarak kullanmasına sahip olmanız gerekir.

Bu iki DropDownLists eklendikten ve uygun şekilde yapılandırılmış ObjectDataSources 'lar ile bağlandıktan sonra, ekranınız Şekil 9 ' a benzer görünmelidir.

[Başlık satırı ![artık tedarikçileri ve kategorileri DropDownLists Içerir](batch-inserting-cs/_static/image26.png)](batch-inserting-cs/_static/image25.png)

**Şekil 9**: başlık satırı artık `Suppliers` ve `Categories` dropdownlists ([tam boyutlu görüntüyü görüntülemek Için tıklayın](batch-inserting-cs/_static/image27.png)) içerir

Şimdi her yeni ürünün adını ve fiyatını toplamak için metin kutuları oluşturmanız gerekir. Araç kutusundan bir TextBox denetimini, beş ürün adı ve fiyat satırı için tasarımcı üzerine sürükleyin. Metin kutularının `ID` özelliklerini `ProductName1`, `UnitPrice1`, `ProductName2`, `UnitPrice2`, `ProductName3`, `UnitPrice3`vb. olarak ayarlayın.

Birim Fiyat metin kutularının her biri için bir CompareValidator ekleyin ve `ControlToValidate` özelliğini uygun `ID`olarak ayarlar. Ayrıca, `Operator` özelliğini `GreaterThanEqual`, `ValueToCompare` 0 olarak ayarlayın ve `Currency``Type`. Bu ayarlar, girildiyse fiyatın, sıfıra eşit veya sıfırdan büyük geçerli bir para birimi değeri olduğundan emin olmak için CompareValidator yönlendirir. `Text` özelliğini \*olarak ayarlayın ve fiyata `ErrorMessage` sıfırdan büyük veya sıfıra eşit olmalıdır. Ayrıca, lütfen tüm para birimi sembollerini atlayın.

> [!NOTE]
> `Products` veritabanı tablosundaki `ProductName` alanı `NULL` değerlere izin vermediği halde ekleme arabirimi herhangi bir RequiredFieldValidator denetimi içermez. Bunun nedeni kullanıcının en fazla beş ürün girmelerini sağlamak istiyoruz. Örneğin, Kullanıcı ilk üç satır için ürün adı ve birim fiyatını sağlamamız, son iki satırı boş bırakarak sisteme yalnızca üç yeni ürün ekleyeceğiz. Ancak `ProductName` gerekli olduğundan, karşılık gelen bir ürün adı değerinin sağlandığı bir birim fiyatı girilmişse emin olmak için programlı olarak kontrol etmemiz gerekir. Adım 4 ' te bu denetimi kullanıma sunacağız.

Kullanıcı girişi doğrulanırken, değer bir para birimi simgesi içeriyorsa, CompareValidator geçersiz verileri raporlar. Kullanıcıya fiyat girerken para birimi sembolünü atmasını bildiren bir görsel ipucu olarak kullanılacak, birim fiyat kutularının her birinin bir $ ın önüne ekleyin.

Son olarak, `InsertingInterface` paneli içinde bir ValidationSummary denetimi ekleyin, `ShowMessageBox` özelliğini `true` ve `ShowSummary` özelliğine `false`olarak ayarlar. Bu ayarlarla, Kullanıcı geçersiz bir birim fiyat değeri girerse, sorunlu metin kutusu denetimlerinin yanında bir yıldız işareti görünür ve ValidationSummary, daha önce belirttiğimiz hata iletisini gösteren bir istemci tarafı MessageBox görüntüler.

Bu noktada ekranınızın Şekil 10 ' a benzer olması gerekir.

[Ekleme arabirimi ![, artık ürün adları ve fiyatları için metin kutuları Içerir](batch-inserting-cs/_static/image29.png)](batch-inserting-cs/_static/image28.png)

**Şekil 10**: ekleme arabirimi artık ürün adları ve fiyatları Için metin kutuları içerir ([tam boyutlu görüntüyü görüntülemek için tıklatın](batch-inserting-cs/_static/image30.png))

Sonraki adımda, Sevkiyat ve Iptal düğmelerinden ürün Ekle ' ye alt bilgi satırına eklememiz gerekiyor. Araç kutusundan iki düğme denetimini ekleme arabiriminin altbilgisine sürükleyin, düğmeleri `ID` Özellikler `AddProducts` ve `CancelButton` ve `Text` özellikleri, Sevkiyat ve Iptal 'tan ürün eklemek için, sırasıyla ayarlar. Ayrıca, `CancelButton` Control s `CausesValidation` özelliğini `false`olarak ayarlayın.

Son olarak, iki arabirim için durum iletilerini görüntüleyecek bir etiket Web denetimi eklememiz gerekiyor. Örneğin, bir Kullanıcı ürünlerin yeni bir sevkiyatını başarıyla eklediğinde, görüntüleme arabirimine dönmek ve bir onay iletisi göstermek istiyoruz. Ancak, Kullanıcı yeni bir ürün için bir fiyat sağlar, ancak ürün adını kaparsa, `ProductName` alanı gerekli olduğundan bir uyarı iletisi görüntüliyoruz. Bu iletinin her iki arabirim için de görüntülenmesi gerektiğinden, sayfanın üst kısmına Pano dışından yerleştirin.

Araç kutusundan bir etiket Web denetimini tasarımcıda sayfanın en üstüne sürükleyin. `ID` özelliğini `StatusLabel`olarak ayarlayın, `Text` özelliğini temizleyin ve `Visible` ve `EnableViewState` özelliklerini `false`olarak ayarlayın. Önceki öğreticilerde gördüğimize göre `EnableViewState` özelliğinin `false` olarak ayarlanması, etiket s özellik değerlerini programlı bir şekilde değiştirebilmemiz ve sonraki geri göndermede otomatik olarak varsayılan değerlerine geri dönmemize olanak sağlar. Bu, sonraki geri göndermede ortadan bulunan bazı kullanıcı eylemine yanıt olarak bir durum iletisi göstermek için kodu basitleştirir. Son olarak, büyük, italik, kalın ve kırmızı bir yazı tipinde metin görüntüleyen `Styles.css` tanımlanmış bir CSS sınıfının adı olan `StatusLabel` Control s `CssClass` özelliğini uyarı olarak ayarlayın.

Şekil 11 ' ın etiketi eklendikten ve yapılandırıldıktan sonra Visual Studio Tasarımcısı gösterilmektedir.

[![, StatusLabel denetimini Iki Panel denetiminin üzerine yerleştirin](batch-inserting-cs/_static/image32.png)](batch-inserting-cs/_static/image31.png)

**Şekil 11**: `StatusLabel` denetimini Iki Panel denetiminin üstüne yerleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image33.png))

## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>3\. Adım: görüntüleme ve ekleme arabirimleri arasında geçiş yapma

Bu noktada, görüntü ve ekleme arabirimlerimiz için biçimlendirmeyi tamamladık, ancak yine de iki görevle hala ayrıldık:

- Görüntüleme ve ekleme arabirimleri arasında geçiş yapma
- Sevkıyata eklenen ürünler veritabanına ekleniyor

Şu anda, görüntüleme arabirimi görünür ancak ekleme arabirimi gizli. Bunun nedeni, `DisplayInterface` panel s `Visible` özelliğinin `true` (varsayılan değer) olarak ayarlandığı, `InsertingInterface` panel s `Visible` özelliği ise `false`olarak ayarlanmıştır. İki arabirim arasında geçiş yapmak için, her bir denetimin `Visible` özellik değerini değiştirmek zorunda olduğumuz her bir denetim için yeterlidir.

Işlem ürünü sevk Irsaliyesi düğmesine tıklandığında, görüntüleme arabiriminden ekleme arabirimine geçmek istiyoruz. Bu nedenle, bu düğme s `Click` için aşağıdaki kodu içeren bir olay işleyicisi oluşturun:

[!code-csharp[Main](batch-inserting-cs/samples/sample4.cs)]

Bu kod yalnızca `DisplayInterface` paneli gizler ve `InsertingInterface` panelini gösterir.

Sonra, ekleme arabirimindeki, Sevkiyat ve Iptal düğmesi denetimlerinden ürün Ekle ' ye yönelik olay işleyicileri oluşturun. Bu düğmelerden birine tıklandığında, görüntüleme arabirimine geri dönmemiz gerekir. Her iki düğme denetimi için de `Click` olay işleyicileri oluşturun, bu sayede bir yöntem olarak ekleyeceğiz `ReturnToDisplayInterface`. `InsertingInterface` paneli gizleme ve `DisplayInterface` panelini gösterme ek olarak, `ReturnToDisplayInterface` yönteminin Web denetimlerini önceden düzenlenen durumuna döndürmesi gerekir. Bu, DropDownLists `SelectedIndex` özelliklerinin 0 olarak ayarlanmasını ve metin kutusu denetimlerinin `Text` özelliklerini temizlemeyi içerir.

> [!NOTE]
> Görüntüleme arabirimine dönmeden önce denetimleri ön Düzenle durumuna döndürmediyseniz ne olabileceğini göz önünde bulundurun. Kullanıcı, ürün sevk Irsaliyesini Işle düğmesine tıklayabilir, sevkıyata ürünleri girebilir ve ardından sevkıyata ürün Ekle ' ye tıklayabilirsiniz. Bu, ürünleri ekleyecek ve Kullanıcı görüntüleme arabirimine döndürüyor. Bu noktada Kullanıcı başka bir sevkiyat eklemek isteyebilir. Işlem ürün sevkiyat düğmesine tıklandıktan sonra ekleme arabirimine geri döner, ancak DropDownList seçimleri ve metin kutusu değerleri yine de önceki değerleriyle doldurulur.

[!code-csharp[Main](batch-inserting-cs/samples/sample5.cs)]

`Click` olay işleyicilerinin her ikisi de yalnızca `ReturnToDisplayInterface` yöntemini çağırır, ancak 4. adımda ürün Ekle `Click` olay işleyicisine geri dönebiliyoruz ve ürünleri kaydetmek için kod ekleyeceğiz. `ReturnToDisplayInterface`, `Suppliers` ve `Categories` DropDownLists ilk seçeneklerine dönerek başlar. İki sabitler `firstControlID` ve `lastControlID`, ekleme arabirimindeki ürün adını ve birim fiyat metin kutularını adlandırırken kullanılan başlangıç ve bitiş denetim dizini değerlerini işaretleyip metin kutusu denetimlerinin `Text` özelliklerini boş bir dizeye doğru ayarlayan `for` döngüsünün sınırları içinde kullanılır. Son olarak, ekleme arabiriminin gizlenmesi ve görüntüleme arabiriminin gösterilmesi için paneller `Visible` Özellikler sıfırlanır.

Bu sayfayı bir tarayıcıda test etmek için bir dakikanızı ayırın. Sayfayı ilk kez ziyaret edildiğinde, Şekil 5 ' te gösterildiği gibi görüntüleme arabirimini görmeniz gerekir. Ürün sevk Irsaliyesini Işle düğmesine tıklayın. Sayfa geri gönderilir ve şimdi Şekil 12 ' de gösterildiği gibi ekleme arabirimini görmeniz gerekir. Sevkiyat veya Iptal düğmelerinden ürün Ekle ' ye tıklamak sizi görüntüleme arabirimine döndürür.

> [!NOTE]
> Ekleme arabirimini görüntülerken, birim fiyat metin kutularındaki Comparedoğrulayıcıları test etmek için bir dakikanızı ayırın. Geçersiz para birimi değerleri veya sıfırdan küçük bir değere sahip fiyatlarla, sevkıyata ürün Ekle düğmesine tıkladığınızda bir istemci tarafı MessageBox uyarısı görmeniz gerekir.

[Işlem ürün sevkıyatı düğmesine tıklandıktan sonra ekleme arabirimi ![görüntülenir](batch-inserting-cs/_static/image35.png)](batch-inserting-cs/_static/image34.png)

**Şekil 12**: Işlem ürünü sevkiyat düğmesine tıklandıktan sonra ekleme arabirimi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image36.png))

## <a name="step-4-adding-the-products"></a>4\. Adım: ürünleri ekleme

Bu öğretici için her şey, ürünleri sevkiyat düğmesinden `Click` olay işleyicisinden veritabanına kaydetmesidir. Bu, `ProductsDataTable` oluşturularak ve sağlanan ürün adlarının her biri için bir `ProductsRow` örneği eklenerek gerçekleştirilebilir. Bu `ProductsRow` eklendikten sonra, `ProductsDataTable`geçen `ProductsBLL` sınıfı s `UpdateWithTransaction` yöntemine çağrı yapılır. Işlem öğreticisindeki [sarmalama veritabanı değişiklikleri](wrapping-database-modifications-within-a-transaction-cs.md) içinde oluşturulan `UpdateWithTransaction` yönteminin `ProductsDataTable` `ProductsTableAdapter` s `UpdateWithTransaction` metoduna geçirmediğini hatırlayın. Buradan, bir ADO.NET işlemi başlatılır ve TableAdapter DataTable içindeki her eklenen `ProductsRow` için veritabanına `INSERT` bir bildirim yayınlar. Tüm ürünlerin hatasız eklendiği varsayılarak, işlem kaydedilir, aksi takdirde geri alınır.

Sevkiyat düğmesinden (`Click` etkinlik Ekle) olay işleyicisi için kod aynı zamanda bir hata denetimi gerçekleştirmesi gerekir. Ekleme arabiriminde kullanılan bir RequiredFieldValidators olmadığından, Kullanıcı adını atlayarak bir ürünün fiyatını girebilir. Ürünün adı gerekli olduğundan, bu tür bir koşul, kullanıcıyı uyarmak ve ekleme işlemine devam etmemiz gerekir. Tüm `Click` olay işleyicisi kodu aşağıda verilmiştir:

[!code-csharp[Main](batch-inserting-cs/samples/sample6.cs)]

Olay işleyicisi, `Page.IsValid` özelliğinin `true`değerini döndürmesi sağlanarak başlar. `false`döndürürse, bir veya daha fazla Comparedoğrulayıcılarının geçersiz verileri bildirdiği anlamına gelir; Böyle bir durumda, girilen ürünleri eklemeye çalışmak istemedik veya Kullanıcı tarafından girilen birim fiyat değerini `ProductsRow` s `UnitPrice` özelliğine atamaya çalışırken bir özel durumla karşılaşırsınız.

Sonra yeni bir `ProductsDataTable` örneği oluşturulur (`products`). `for` döngüsü, ürün adı ve birim fiyat metin kutuları üzerinden yinelemek için kullanılır ve `Text` özellikleri, `productName` ve `unitPrice`yerel değişkenlerine okunurdur. Kullanıcı birim fiyatı için bir değer girdiyseniz ancak karşılık gelen ürün adı için değilse, bir birim fiyat sağlarsanız, ürünün adını da dahil etmeniz ve olay işleyicisine çıkıyması durumunda `StatusLabel` iletiyi görüntüler.

Bir ürün adı sağlanmışsa, `ProductsDataTable` s `NewProductsRow` yöntemi kullanılarak yeni bir `ProductsRow` örneği oluşturulur. Bu yeni `ProductsRow` örneği `ProductName` özelliği geçerli ürün adı metin kutusuna ayarlanır, ancak `SupplierID` ve `CategoryID` özellikleri, ekleme arabirimi s üstbilgisindeki DropDownLists 'in `SelectedValue` özelliklerine atanır. Kullanıcı ürün fiyatı için bir değer girdiyseniz, `ProductsRow` örnek s `UnitPrice` özelliğine atanır; Aksi halde, özelliği atanmamış olarak bırakılır ve bu, veritabanındaki `UnitPrice` `NULL` bir değere neden olur. Son olarak, `Discontinued` ve `UnitsOnOrder` özellikleri sırasıyla sabit kodlanmış değerlere `false` ve 0 ' a atanır.

Özellikler, `ProductsRow` örneğine atandıktan sonra, `ProductsDataTable`eklenir.

`for` döngüsünün tamamlanmasında, herhangi bir ürünün eklenip eklenmeyeceğini denetliyoruz. Kullanıcı, tüm ürün adlarını veya fiyatları girmeden önce, sevk Irsaliyesinden ürün Ekle ' ye tıklamış olabilir. `ProductsDataTable`en az bir ürün varsa `ProductsBLL` sınıf s `UpdateWithTransaction` yöntemi çağrılır. Daha sonra, veriler `ProductsGrid` GridView 'a yeniden bağlanır, böylece yeni eklenen ürünlerin görüntüleme arabiriminde görünmesi gerekir. `StatusLabel`, bir onay iletisi görüntüleyecek şekilde güncelleştirilir ve `ReturnToDisplayInterface` çağrılır, ekleme arabirimini gizler ve görüntüleme arabirimini gösterir.

Hiçbir ürün girilmemişse ekleme arabirimi görüntülenmeye devam eder, ancak hiçbir ürün eklenmedi. Lütfen metin kutularına ürün adlarını ve birim fiyatlarını girin.

Şekil s 13, 14 ve 15, ekleme ve görüntüleme arabirimlerini eylemde gösterir. Şekil 13 ' te, Kullanıcı karşılık gelen bir ürün adı olmadan bir birim fiyat değeri girmiştir. Şekil 14 ' te, üç yeni ürün başarıyla eklendikten sonra görüntüleme arabirimi gösterilmektedir, Şekil 15 ' te yeni eklenen ürünlerden ikisi (üçüncü bir önceki sayfada bulunur) gösterilir.

[Birim fiyatı girilirken bir ürün adı ![gerekir](batch-inserting-cs/_static/image38.png)](batch-inserting-cs/_static/image37.png)

**Şekil 13**: birim fiyatını girerken bir ürün adı gereklidir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image39.png))

[![Tedarikçi Mayumi s için üç yeni grup eklenmiştir](batch-inserting-cs/_static/image41.png)](batch-inserting-cs/_static/image40.png)

**Şekil 14**: Tedarikçi Mayumi s Için üç yeni vegon eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image42.png))

[Yeni Ürünler GridView 'un son sayfasında bulunabilir ![](batch-inserting-cs/_static/image44.png)](batch-inserting-cs/_static/image43.png)

**Şekil 15**: yeni ürünler GridView 'un son sayfasında bulunabilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-inserting-cs/_static/image45.png))

> [!NOTE]
> Bu öğreticide kullanılan toplu ekleme mantığı, işlem kapsamındaki eklemeleri sarmalanmış. Bunu doğrulamak için, bir veritabanı düzeyindeki hatayı tam olarak tanıtın. Örneğin, yeni `ProductsRow` örnek s `CategoryID` özelliğini `Categories` DropDownList içindeki seçili değere atamak yerine `i * 5`gibi bir değere atayın. Burada `i` Loop Indexer ve 1 ile 5 arasında değişen değerler vardır. Bu nedenle, toplu işteki iki veya daha fazla ürün eklenirken ilk ürünün geçerli bir `CategoryID` değeri (5) olacaktır, ancak sonraki ürünlerin `Categories` tablosundaki `CategoryID` değerlerle eşleşmeyen `CategoryID` değerleri olacaktır. Ağ etkisi, ilk `INSERT` başarılı olacağı ve sonrasında bir yabancı anahtar kısıtlaması ihlalinden sonra başarısız olacak. Batch INSERT atomik olduğundan, ilk `INSERT` geri alınacak ve toplu işlem ekleme işlemi başlamadan önce veritabanını durumuna döndürmeyecektir.

## <a name="summary"></a>Özet

Bu ve önceki iki öğreticide, verilerin toplu olarak güncelleştirilmesine, silinmesine ve eklenmesine izin veren arabirimler oluşturdunuz ve bu işlem, [bir işlem öğreticisindeki sarmalama veritabanı değişiklikleri](wrapping-database-modifications-within-a-transaction-cs.md) Içindeki veri erişim katmanına eklediğimiz işlem desteğini kullandı. Bazı senaryolarda, bu tür toplu işleme kullanıcı arabirimleri tıklama, geri alma ve klavyeden fare bağlam anahtarlarının sayısını izleyerek Son Kullanıcı verimliliğini büyük ölçüde geliştirir ve ayrıca temel alınan verilerin bütünlüğünü de sürdürmenize olanak sağlar.

Bu öğretici, toplu verilerle çalışma hakkındaki görünmizi tamamlar. Sonraki öğreticilerde, TableAdapter s yöntemlerindeki saklı yordamları kullanma, DAL içinde bağlantı ve komut düzeyi ayarlarını yapılandırma, bağlantı dizelerini şifreleme ve daha fazlasını içeren çeşitli gelişmiş veri erişim katmanı senaryoları ele maktadır!

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, kton Giesenow ve S Ren Jacob Lauritsen. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](batch-deleting-cs.md)
> [İleri](wrapping-database-modifications-within-a-transaction-vb.md)
