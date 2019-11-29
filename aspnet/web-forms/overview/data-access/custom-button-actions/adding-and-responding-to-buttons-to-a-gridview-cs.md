---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
title: GridView 'a ekleme ve düğmelere yanıt verme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, hem bir şablon hem de bir GridView veya DetailsView denetiminin alanları için özel düğmeler ekleme bölümüne bakacağız. Özellikle de biz...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 128fdb5f-4c5e-42b5-b485-f3aee90a8e38
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
msc.type: authoredcontent
ms.openlocfilehash: 5c87386e4fe2c53b39162071689f2522dcc6c7ac
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74602770"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-c"></a>GridView’a Düğme Ekleme ve Bunları Yanıtlama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_CS.exe) veya [PDF 'yi indirin](adding-and-responding-to-buttons-to-a-gridview-cs/_static/datatutorial28cs1.pdf)

> Bu öğreticide, hem bir şablon hem de bir GridView veya DetailsView denetiminin alanları için özel düğmeler ekleme bölümüne bakacağız. Özellikle, kullanıcının tedarikçilerle sayfa oluşturmasını sağlayan bir FormView içeren bir arabirim oluşturacağız.

## <a name="introduction"></a>Giriş

Birçok raporlama senaryosu rapor verilerine salt okuma erişimi içerirken, raporların, görüntülenecek verilere göre eylemleri gerçekleştirme yeteneğini içermesi çok seyrek değildir. Genellikle bu, tıklatıldığında raporda görüntülenen her kayıtla birlikte bir Button, LinkButton veya ImageButton Web denetimi eklemeyi, tıklandığı zaman geri göndermeye neden olur ve bazı sunucu tarafı kodları çağırır. Kayda göre kayıt temelinde verileri düzenlemenin ve silmenin en yaygın örneği vardır. Aslında, veri öğreticisini [ekleme, güncelleştirme ve silmeye Ilişkin genel bakışın](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) yanı sıra, düzenlemenin ve silmenin yanı sıra GridView, DetailsView ve FormView denetimlerinin tek bir kod satırı yazmak zorunda kalmadan bu işlevselliği destekleyebilmesi yaygın bir çalışmadır.

Düzenle ve Sil düğmelerine ek olarak, GridView, DetailsView ve FormView denetimleri, tıklandığı sırada bazı özel sunucu tarafı mantığlarını, LinkButtons 'ı veya görüntü düğmelerini de içerebilir. Bu öğreticide, hem bir şablon hem de bir GridView veya DetailsView denetiminin alanları için özel düğmeler ekleme bölümüne bakacağız. Özellikle, kullanıcının tedarikçilerle sayfa oluşturmasını sağlayan bir FormView içeren bir arabirim oluşturacağız. Belirli bir tedarikçi için, FormView, bir düğme web denetimiyle birlikte tedarikçi hakkındaki bilgileri gösterir ve tıklandıklarında ilişkili tüm ürünlerini kullanımdan kaldırıldı olarak işaretleyebilir. Ek olarak, bir GridView, seçili tedarikçi tarafından sunulan bu ürünleri, tıklanmış olması durumunda ürünün `UnitPrice` %10 ' u (bkz. Şekil 1) yükseltir veya azalttığını gösteren fiyat ve Indirimli Fiyat düğmelerini içeren her bir satırla listeler.

[FormView ve GridView 'un her Ikisi de ![özel eylemleri gerçekleştiren düğmeler Içerir](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image1.png)

**Şekil 1**: hem FormView hem de GridView özel eylemleri gerçekleştiren düğmeler içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image3.png))

## <a name="step-1-adding-the-button-tutorial-web-pages"></a>1\. Adım: düğme öğreticisi Web sayfalarını ekleme

Özel düğmeler eklemeye bakmadan önce, Web sitesi projemizdeki Bu öğreticide gereken ASP.NET sayfalarını oluşturmak için bir dakikanızı atalım. `CustomButtons`adlı yeni bir klasör ekleyerek başlayın. Sonra, her bir sayfayı `Site.master` ana sayfayla ilişkilendirdiğinizden emin olmak için, aşağıdaki iki ASP.NET sayfasını bu klasöre ekleyin:

- `Default.aspx`
- `CustomButtons.aspx`

![Özel düğmelerle Ilgili öğreticiler için ASP.NET sayfaları ekleyin](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image4.png)

**Şekil 2**: özel düğmelerle ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `CustomButtons` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfanın Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image5.png)

**Şekil 3**: `Default.aspx` `SectionLevelTutorialListing.ascx` Kullanıcı denetimini ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image7.png))

Son olarak, sayfaları `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, sayfalama ve sıralama `<siteMapNode>`sonrasında aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık öğreticilerin düzenlenmesine, eklemeye ve silinmesine yönelik öğeler içerir.

![Site Haritası artık özel düğmeler öğreticisi için girişi Içerir](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image8.png)

**Şekil 4**: site haritası artık özel düğmeler öğreticisi Için girişi içerir

## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>2\. Adım: tedarikçileri listeleyen bir FormView ekleme

Tedarikçilerini listeleyen FormView 'ı ekleyerek Bu öğreticiye başlaalım. Bu FormView, giriş bölümünde anlatıldığı gibi, bir GridView 'da tedarikçi tarafından sunulan ürünleri göstererek kullanıcının tedarikçilerle sayfa eklemesine izin verir. Ayrıca, bu FormView, tıklandığında tedarikçinin ürünlerinin tümünü kullanımdan kaldırıldı olarak işaretleyecek bir düğme içerir. Kendimize 'e özel düğme ekleme konusunda sorun yapmadan önce, ilk olarak, tedarikçi bilgilerini görüntüleyecek şekilde FormView 'u oluşturalım.

`CustomButtons` klasöründeki `CustomButtons.aspx` sayfasını açarak başlayın. Araç kutusundan Tasarımcı üzerine sürükleyerek sayfaya bir FormView ekleyin ve `ID` özelliğini `Suppliers`olarak ayarlayın. FormView 'un akıllı etiketiyle `SuppliersDataSource`adlı yeni bir ObjectDataSource oluşturmayı tercih edin.

[SuppliersDataSource adlı yeni bir ObjectDataSource oluşturma ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image9.png)

**Şekil 5**: `SuppliersDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image11.png))

`SuppliersBLL` sınıfının `GetSuppliers()` yönteminden (bkz. Şekil 6) sorgulamalarını sağlayan bu yeni ObjectDataSource 'ı yapılandırın. Bu FormView, tedarikçi bilgilerini güncelleştirmek için bir arabirim sağlamadığından, GÜNCELLEŞTIR sekmesindeki aşağı açılan listeden (hiçbiri) seçeneğini belirleyin.

[Veri kaynağını SuppliersBLL Class s GetSuppliers () metodunu kullanacak şekilde yapılandırmak ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image12.png)

**Şekil 6**: veri kaynağını `SuppliersBLL` sınıfının `GetSuppliers()` metodunu kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image14.png))

ObjectDataSource yapılandırıldıktan sonra, Visual Studio FormView için bir `InsertItemTemplate`, `EditItemTemplate`ve `ItemTemplate` oluşturur. `InsertItemTemplate` ve `EditItemTemplate` kaldırın ve `ItemTemplate` yalnızca tedarikçinin şirket adını ve telefon numarasını görüntüleyecek şekilde değiştirin. Son olarak, akıllı etiketinden sayfalama etkinleştir onay kutusunu işaretleyerek (veya `AllowPaging` özelliğini `True`olarak ayarlayarak FormView için sayfalama desteğini açın). Bu değişikliklerden sonra sayfanızın bildirime dayalı biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample2.aspx)]

Şekil 7 ' de bir tarayıcıdan görüntülendiklerinde CustomButtons. aspx sayfası gösterilir.

[FormView ![Şu anda seçili olan tedarikçiden CompanyName ve telefon alanlarını listeler](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image15.png)

**Şekil 7**: FormView, şu anda seçili olan tedarikçiden `CompanyName` ve `Phone` alanlarını listeler ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image17.png))

## <a name="step-3-adding-a-gridview-that-lists-the-selected-suppliers-products"></a>3\. Adım: seçili tedarikçinin ürünlerini listeleyen bir GridView ekleme

Tüm ürünleri Durdur düğmesini FormView 'un şablonuna eklemeden önce, önce seçili tedarikçi tarafından sunulan ürünleri listeleyen FormView 'un altına bir GridView ekleyelim. Bunu gerçekleştirmek için, sayfaya bir GridView ekleyin, `ID` özelliğini `SuppliersProducts`olarak ayarlayın ve `SuppliersProductsDataSource`adlı yeni bir ObjectDataSource ekleyin.

[SuppliersProductsDataSource adlı yeni bir ObjectDataSource oluşturma ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image18.png)

**Şekil 8**: `SuppliersProductsDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image20.png))

Bu ObjectDataSource 'ı ProductsBLL sınıfının `GetProductsBySupplierID(supplierID)` yöntemini kullanacak şekilde yapılandırın (bkz. Şekil 9). Bu GridView bir ürünün fiyatının ayarlanmasına izin vermekle kalmaz, GridView 'daki yerleşik düzenlemeyle veya silmeden özellikleri kullanmayacaktır. Bu nedenle, ObjectDataSource 'un GÜNCELLEŞTIRME, ekleme ve SILME sekmeleri için açılan listeyi (yok) olarak ayarlayabiliriz.

[![veri kaynağını ProductsBLL sınıfı s Getproductsbysupplierıd (SupplierID) metodunu kullanacak şekilde yapılandırın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image21.png)

**Şekil 9**: veri kaynağını `ProductsBLL` sınıfının `GetProductsBySupplierID(supplierID)` metodunu kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image23.png))

`GetProductsBySupplierID(supplierID)` yöntemi bir giriş parametresini kabul ettiğinden, ObjectDataSource Sihirbazı bize bu parametre değerinin kaynağını sorar. FormView 'dan `SupplierID` değerini geçirmek için, parametre kaynağı açılır listesini kontrol ve ControlID açılan listesini `Suppliers` (adım 2 ' de oluşturulan FormView 'un KIMLIĞI) olarak ayarlayın.

[![SupplierID parametresinin Suppliers FormView denetiminden gelmesi gerektiğini belirtir](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image24.png)

**Şekil 10**: *`supplierID`* parametresinin `Suppliers` FormView denetiminden gelmesi gerektiğini belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image26.png))

ObjectDataSource sihirbazını tamamladıktan sonra GridView, her bir ürünün veri alanı için bir BoundField veya CheckBoxField içerecektir. Yalnızca `ProductName` ve `UnitPrice` BoundFields alanlarını `Discontinued` CheckBoxField ile birlikte göstermek için bunu kırpalım; Ayrıca, metnin bir para birimi olarak biçimlendirilmesi için `UnitPrice` BoundField olarak biçimlendirelim. GridView ve `SuppliersProductsDataSource` ObjectDataSource 'un bildirim temelli biçimlendirmesi aşağıdaki biçimlendirmeye benzer olmalıdır:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample3.aspx)]

Bu noktada, öğreticimiz ana/ayrıntı raporunu görüntüleyerek kullanıcının en üstteki FormView 'dan bir tedarikçi seçmesini ve alttaki GridView aracılığıyla söz konusu tedarikçi tarafından sunulan ürünleri görüntülemesini sağlar. Şekil 11 ' den bu sayfanın bir ekran görüntüsünü, FormView 'dan Tokyo Traders tedarikçisine seçerken gösterir.

[![seçili tedarikçinin ürünleri GridView 'da görüntülenir](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image27.png)

**Şekil 11**: seçili tedarikçinin ürünleri GridView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image29.png))

## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>4\. Adım: bir tedarikçiye yönelik tüm ürünleri sona erdirmek için DAL ve BLL yöntemleri oluşturma

FormView 'a bir düğme ekleyebilmemiz için, tıkladıklarında tedarikçinin tüm ürünlerini tamamen devam ettirir, bu eylemi gerçekleştiren DAL ve BLL 'ye bir yöntem eklememiz gerekir. Özellikle, bu yöntem `DiscontinueAllProductsForSupplier(supplierID)`olarak adlandırılır. FormView 'un düğmesine tıklandığında, bu yöntemi Iş mantığı katmanında, seçilen tedarikçinin `SupplierID`geçirerek çağıracağız; BLL daha sonra karşılık gelen veri erişim katmanı yöntemine çağrı yapılır, bu, veritabanında belirtilen tedarikçinin ürünlerini sürekli olarak devam eden `UPDATE` bir bildirim sağlar.

Önceki öğreticilerimizde yaptığımız gibi, DAL yöntemi oluşturmaya, sonra BLL yöntemine ve son olarak ASP.NET sayfasındaki işlevselliği uygulamaya göre aşağıdan yukarıya bir yaklaşım kullanacağız. `App_Code/DAL` klasöründe `Northwind.xsd` türü belirtilmiş veri kümesini açın ve `ProductsTableAdapter` yeni bir yöntem ekleyin (`ProductsTableAdapter` sağ tıklayın ve sorgu Ekle ' yi seçin). Bunun yapılması, yeni yöntemi ekleme sürecinde bize yol gösteren TableAdapter sorgu Yapılandırma Sihirbazı 'nı getirir. DAL yönteminizin bir geçici SQL ifadesini kullandığını belirterek başlayın.

[![geçici bir SQL Ifadesini kullanarak DAL yöntemi oluşturma](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image30.png)

**Şekil 12**: GEÇICI bir SQL IFADESINI kullanarak dal yöntemi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image32.png))

Daha sonra sihirbaz, oluşturulacak sorgu türünü bizimle uyarır. `DiscontinueAllProductsForSupplier(supplierID)` yönteminin `Products` veritabanı tablosunu güncelleştirmesi gerekir, çünkü `Discontinued` alanı belirtilen *`supplierID`* tarafından sunulan tüm ürünler için 1 olarak ayarlandığında, verileri güncelleştiren bir sorgu oluşturmanız gerekir.

[![GÜNCELLEŞTIRME sorgu türünü seçin](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image33.png)

**Şekil 13**: güncelleştirme sorgu türünü seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image35.png))

Sonraki sihirbaz ekranı, TableAdapter 'ın `Products` DataTable içinde tanımlanan her bir alanı güncelleştiren mevcut `UPDATE` ifadesini sağlar. Bu sorgu metnini aşağıdaki ifadeyle değiştirin:

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample4.sql)]

Bu sorguyu girdikten ve Ileri 'ye tıkladıktan sonra, son sihirbaz ekranı yeni yöntemin adının `DiscontinueAllProductsForSupplier`kullanımını ister. Son düğmesine tıklayarak Sihirbazı doldurun. Veri kümesi tasarımcısına döndükten sonra, `ProductsTableAdapter` adlı `DiscontinueAllProductsForSupplier(@SupplierID)`yeni bir yöntem görmeniz gerekir.

[yeni dal yönteminin adını ![adı allproductsfortedarikç](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image36.png)

**Şekil 14**: yeni dal yöntemini adlandırın `DiscontinueAllProductsForSupplier` ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image38.png))

Veri erişim katmanında oluşturulan `DiscontinueAllProductsForSupplier(supplierID)` yöntemi ile, sonraki göreviniz Iş mantığı katmanında `DiscontinueAllProductsForSupplier(supplierID)` yöntemini oluşturmaktır. Bunu gerçekleştirmek için `ProductsBLL` sınıf dosyasını açın ve aşağıdakileri ekleyin:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample5.cs)]

Bu yöntem, yalnızca DAL içindeki `DiscontinueAllProductsForSupplier(supplierID)` yöntemine çağrı yaparak, belirtilen *`supplierID`* parametre değerini geçirerek. Yalnızca bir tedarikçinin ürünlerinin belirli koşullarda kullanımdan yapılmasına izin verilen iş kuralları varsa, bu kuralların BLL 'de burada uygulanması gerekir.

> [!NOTE]
> `ProductsBLL` sınıfındaki `UpdateProduct` aşırı yüklemelerin aksine `DiscontinueAllProductsForSupplier(supplierID)` Yöntem imzası `DataObjectMethodAttribute` özniteliğini (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`) içermez. Bu, ObjectDataSource 'un, GÜNCELLEŞTIRME sekmesindeki veri kaynağı Yapılandırma Sihirbazı 'nın açılan listesinden `DiscontinueAllProductsForSupplier(supplierID)` yöntemini yavaşlatır. Bu özniteliği, ASP.NET sayfamızda doğrudan bir olay işleyicisinden `DiscontinueAllProductsForSupplier(supplierID)` yöntemi çağırmak yaptığımız için atlıyorum.

## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>5\. Adım: FormView 'a tüm ürünleri durdur düğmesi ekleme

BLL ve DAL içindeki `DiscontinueAllProductsForSupplier(supplierID)` yöntemi tamamlandıktan sonra, seçili tedarikçiye yönelik tüm ürünleri sona erdirme özelliği eklemek için son adım, FormView 'un `ItemTemplate`bir düğme web denetimi eklemektir. Bu tür bir düğmeyi, düğme metniyle tedarikçinin telefon numarasının altına ekleyelim, tüm ürünleri ve `DiscontinueAllProductsForSupplier``ID` özellik değerini sona erdirin. Bu düğme web denetimini, FormView 'un akıllı etiketindeki Şablonları Düzenle bağlantısına tıklayarak (Şekil 15 ' i görüntüleyin) veya doğrudan bildirime dayalı sözdizimi aracılığıyla ekleyebilirsiniz.

[![tüm ürünleri Durdur düğme web denetimi ile FormView 'e](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image39.png)

**Şekil 15**: FormView 'un `ItemTemplate` tüm ürünleri Durdur düğme web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image41.png))

Düğmeye sayfayı ziyaret eden bir kullanıcı tarafından tıklandığında, geri gönderme ve FormView 'un [`ItemCommand` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx) ateşlenir. Bu düğmeye tıklanmakta olan bu düğmeye yanıt olarak özel kod yürütmek için, bu olay için bir olay işleyicisi oluşturarız. Bu durumda, *her* düğme, LinkButton veya ImageButton Web denetimine FormView içinde tıklandığında `ItemCommand` olayının tetiklendiğine anlayın. Diğer bir deyişle, Kullanıcı FormView 'da bir sayfadan diğerine taşınırsa, `ItemCommand` olayı ateşlenir; Kullanıcı ekleme, güncelleştirme veya silmeyi destekleyen bir FormView 'da yeni, Düzenle veya Sil ' i tıklattığında aynı şey.

`ItemCommand` düğmenin tıklanmasından bağımsız olarak tetiklendiği için, olay işleyicisinde tüm ürünleri Durdur düğmesinin tıklandığını veya başka bir düğme olup olmadığını belirlemek için bir yol gerekir. Bunu gerçekleştirmek için, düğme Web denetiminin `CommandName` özelliğini tanımlayıcı bir değere ayarlayabiliriz. Düğmeye tıklandığında, bu `CommandName` değeri `ItemCommand` olay işleyicisine geçirilir ve tüm ürünleri Durdur düğmesinin tıklanmadığını belirlememize olanak tanır. Tüm ürünleri Durdur düğmesinin `CommandName` özelliğini, ürünleri kaldır olarak ayarlayın.

Son olarak, kullanıcının gerçekten seçili tedarikçinin ürünlerini kesmek istediğinizden emin olmak için bir istemci tarafı onaylama iletişim kutusu kullanalım. Öğreticiyi [silerken Istemci tarafı onaylama ekleme](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs.md) konusunda gördüğünüz gibi, bu, JavaScript bir bit ile gerçekleştirilebilir. Özellikle, düğme Web denetiminin OnClientClick özelliğini `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');` olarak ayarlayın

Bu değişiklikleri yaptıktan sonra FormView 'un bildirime dayalı sözdizimi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample6.aspx)]

Ardından, FormView 'un `ItemCommand` olayı için bir olay işleyicisi oluşturun. Bu olay işleyicisinde, önce tüm ürünleri Durdur düğmesine tıklanmadığını belirlememiz gerekir. Bu durumda, `ProductsBLL` sınıfının bir örneğini oluşturmak ve `DiscontinueAllProductsForSupplier(supplierID)` metodunu, seçili FormView 'un `SupplierID` geçirerek çağırmak istiyoruz:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample7.cs)]

FormView 'daki geçerli seçili tedarikçinin `SupplierID` FormView 'un [`SelectedValue` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)kullanılarak erişilebilir olduğunu unutmayın. `SelectedValue` özelliği, FormView 'da görüntülenmekte olan kaydın ilk veri anahtarı değerini döndürür. FormView 'un, veri anahtarı değerlerinin alındığı veri alanlarını belirten [`DataKeyNames` özelliği](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx), ObjectDataSource 'un adım 2 ' deki FormView 'a geri bağlanması sırasında otomatik olarak Visual Studio tarafından `SupplierID` olarak ayarlanmıştır.

`ItemCommand` olay işleyicisi oluşturulduktan sonra, sayfayı sınamak için bir dakikanızı ayırın. Cogutıva ve Sorgtada ' Las Cabras ' tedarikçisine gidin (benim için FormView 'daki beşinci tedarikçi). Bu Tedarikçi, her ikisi de *artık Discontinued olan* Sorgo Cabrales ve Sorgo Manchego La Pastora olmak üzere iki ürün sunmaktadır.

COOPERATIVA ve Sorgun ' Las Cabras ' öğesinin iş dışı olduğunu ve bu nedenle ürünlerinin sonlandırılmamakta olduğunu düşünün. Tüm ürünleri Durdur düğmesine tıklayın. Bu, istemci tarafı onaylama iletişim kutusunu görüntüler (bkz. Şekil 16).

[![Cooperativa de Sorgtada Las Cabras Iki etkin ürün sağlar](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image42.png)

**Şekil 16**: Cooperativa de Sorgtada Las Cabras Iki etkin ürün sağlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image44.png))

İstemci tarafı onaylama iletişim kutusunda Tamam ' a tıklarsanız, form gönderimi devam eder ve bu da FormView 'un `ItemCommand` olayının tetikleneceği geri göndermeye neden olur. Oluşturduğumuz olay işleyicisi yürütülecektir, `DiscontinueAllProductsForSupplier(supplierID)` yöntemini çağırır ve hem Sorgo Cabrales hem de Sorgo Manchego La Pastora ürünlerinin her ikisi de devam eder.

GridView 'un görünüm durumunu devre dışı bırakırsanız, GridView her geri göndermede temel alınan veri deposuna yeniden bağlanır ve bu nedenle hemen bu iki ürünün artık devre dışı bırakıldığını yansıtacak şekilde güncelleştirilir (bkz. Şekil 17). Ancak, GridView 'da görünüm durumunu devre dışı bırakıldıysanız, bu değişikliği yaptıktan sonra verileri GridView 'a el ile yeniden bağlamanız gerekir. Bunu gerçekleştirmek için, `DiscontinueAllProductsForSupplier(supplierID)` yöntemini çağırdıktan hemen sonra GridView 'un `DataBind()` yöntemine bir çağrı yapmanız yeterlidir.

[Tüm ürünleri Durdur düğmesine tıkladıktan sonra, tedarikçinin s ürünleri buna göre güncelleştirilir ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image45.png)

**Şekil 17**: tüm ürünleri Durdur düğmesine tıkladıktan sonra tedarikçinin ürünleri buna uygun şekilde güncelleştirilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image47.png))

## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-products-price"></a>6\. Adım: bir ürünün fiyatını ayarlamak için Iş mantığı katmanında UpdateProduct Overload oluşturma

FormView 'daki tüm ürünleri Durdur düğmesinin yanı sıra, GridView 'da bir ürünün fiyatını artırmak ve azaltmak için düğmeler eklemek üzere öncelikle uygun veri erişim katmanını ve Iş mantığı katman yöntemlerini eklememiz gerekir. DAL içinde tek bir ürün satırını güncelleştiren bir metoda zaten sahip olduğumuz için BLL 'deki `UpdateProduct` yöntemi için yeni bir aşırı yükleme oluşturarak bu işlevselliği sağlayabiliriz.

Son `UpdateProduct` aşırı yüklemeleri, ürün alanlarının bazı kombinasyonda skaler giriş değerleri olarak alınmıştır ve daha sonra yalnızca belirtilen ürüne ait bu alanları güncelleştirdi. Bu aşırı yüklemede, bu standarda göre biraz farklılık gösterir ve bunun yerine ürünün `ProductID` ve `UnitPrice` ayarlanacak yüzdeyi (yeni, ayarlanmış `UnitPrice` içine geçirmeye karşılık olarak) ayarlayın. Bu yaklaşım, geçerli ürünün `UnitPrice`belirlemekten endişelenmenize gerek olmadığı için ASP.NET sayfa arka plan kodu sınıfına yazdığımız kodu basitleştirir.

Bu öğretici için `UpdateProduct` aşırı yüklemesi aşağıda gösterilmektedir:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample8.cs)]

Bu aşırı yükleme, DAL `GetProductByProductID(productID)` yöntemi aracılığıyla belirtilen ürünle ilgili bilgileri alır. Daha sonra ürünün `UnitPrice` bir veritabanı `NULL` değeri atanıp atanmadığını görmek için kontrol eder. Bu değer ise, Fiyat değiştirilmemiş olarak kalır. Ancak,`NULL` olmayan bir `UnitPrice` değeri varsa, yöntem ürünün `UnitPrice` belirtilen yüzdeye (`unitPriceAdjustmentPercent`) göre güncelleştirir.

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>7\. Adım: GridView 'a artış ve küçültme düğmelerini ekleme

GridView (ve DetailsView), her ikisi de bir alan koleksiyonundan oluşur. BoundFields, CheckBoxFields ve TemplateFields 'e ek olarak, ASP.NET, adından da anlaşılacağı gibi, her satır için bir Button, LinkButton veya ImageButton içeren bir sütun olarak işleyen ButtonField 'ı içerir. FormView 'a benzer şekilde, GridView sayfalama düğmeleri içindeki *herhangi bir* düğmeye tıklamak, düğmeleri düzenleme veya silme, düğmeleri sıralama ve benzeri bir geri gönderme işlemine neden olur ve GridView 'un [`RowCommand` olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)oluşturur.

ButtonField, her düğme `CommandName` için belirtilen değeri atayan bir `CommandName` özelliğine sahiptir. FormView ile benzer şekilde, hangi düğmenin tıklandığını belirleyen `CommandName` değeri `RowCommand` olay işleyicisi tarafından kullanılır.

GridView 'a, biri düğme metin fiyatı + %10 ve diğeri fiyat-%10 olan iki yeni ButtonField ekleyelim. Bu ButtonFields alanlarını eklemek için GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayın, sol üstteki listeden ButtonField alan türünü seçin ve Ekle düğmesine tıklayın.

![GridView 'a Iki ButtonField ekleyin](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image48.png)

**Şekil 18**: GridView 'A Iki buttonalanı ekleme

İki ButtonField öğesini ilk iki GridView alanı olarak görünecek şekilde taşıyın. Ardından, bu iki ButtonFields `Text` özelliklerini Price + %10 ve Price-10 ' a ve `CommandName` özelliklerini sırasıyla ıncreaseprice ve DecreasePrice olarak ayarlayın. Varsayılan olarak, bir ButtonField, düğme sütununu LinkButtons olarak işler. Ancak, ButtonField 'ın [`ButtonType` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)aracılığıyla bu değiştirilebilir. Bu iki ButtonField 'ın düzenli basma düğmeleri olarak işlenmiş olmasına izin verlim; Bu nedenle, `ButtonType` özelliğini `Button`olarak ayarlayın. Şekil 19, bu değişiklikler yapıldıktan sonra alanlar iletişim kutusunu gösterir; Aşağıda, GridView 'un bildirime dayalı biçimlendirmesi verilmiştir.

![ButtonFields metin, CommandName ve ButtonType özelliklerini yapılandırın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image49.png)

**Şekil 19**: buttonfields `Text`, `CommandName`ve `ButtonType` özelliklerini yapılandırma

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample9.aspx)]

Bu ButtonFields ile oluşturulan son adım, GridView 'un `RowCommand` olayı için bir olay işleyicisi oluşturmaktır. Bu olay işleyicisi, Fiyat + %10 veya fiyat-10% düğmelerine tıklandığı için tetiklense, düğme tıklandığı satırın `ProductID` belirlenmesi ve sonra `ProductsBLL` sınıfının `UpdateProduct` yöntemini çağırarak `ProductID`birlikte uygun `UnitPrice` yüzde ayarlamasını geçirmeleri gerekir. Aşağıdaki kod bu görevleri gerçekleştirir:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample10.cs)]

Fiyatı + %10 veya fiyat-10% düğmesine tıklanmış olan satırın `ProductID` belirleyebilmek için, GridView 'un `DataKeys` koleksiyonuna başvurmalısınız. Bu koleksiyon, her GridView satırı için `DataKeyNames` özelliğinde belirtilen alanların değerlerini barındırır. GridView 'un `DataKeyNames` özelliği, ObjectDataSource 'u GridView 'a bağladığından Visual Studio tarafından ProductID olarak ayarlandığı için, `DataKeys(rowIndex).Value` belirtilen *RowIndex*için `ProductID` sağlar.

ButtonField, düğme `e.CommandArgument` parametresi aracılığıyla tıklandığı olan satırın *RowIndex* öğesinde otomatik olarak geçer. Bu nedenle, fiyatı + %10 veya fiyat-10% düğmesine tıklandığı satırın `ProductID` belirlenmesi için şunu kullanırız: `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`.

Tüm ürünleri Durdur düğmesinin bulunduğu gibi, GridView 'un görünüm durumunu devre dışı bırakırsanız, GridView her geri göndermede temel alınan veri deposuna yeniden bağlanır ve bu nedenle, tıklanarak oluşan bir fiyat değişikliğini yansıtacak şekilde hemen güncelleştirilir. düğmelerden birini kullanabilirsiniz. Ancak, GridView 'da görünüm durumunu devre dışı bırakıldıysanız, bu değişikliği yaptıktan sonra verileri GridView 'a el ile yeniden bağlamanız gerekir. Bunu gerçekleştirmek için, `UpdateProduct` yöntemini çağırdıktan hemen sonra GridView 'un `DataBind()` yöntemine bir çağrı yapmanız yeterlidir.

Şekil 20, Grandma Kelly 'in Homestead tarafından sunulan ürünleri görüntülerken sayfayı gösterir. Şekil 21, Grandma 'nın boyuna yayıldığı ve Kuzey Woods Cranbraz Sauce için fiyat-10% düğmesi bir kez tıklandıktan sonra, Fiyat + %10 ' dan sonra sonuçları gösterir.

[GridView ![Price + %10 ve Price-10% düğmelerini Içerir](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image50.png)

**Şekil 20**: GridView, Price + %10 ve Price-10% düğmelerini içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image52.png))

[![birinci ve üçüncü ürün için fiyatlar, Fiyat + %10 ve fiyat-10% düğmeleri aracılığıyla güncelleştirilmiştir](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image53.png)

**Şekil 21**: birinci ve üçüncü ürünün fiyatları, Fiyat + %10 ve fiyat-10% düğmeleriyle güncelleştirilmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image55.png))

> [!NOTE]
> GridView (ve DetailsView), TemplateFields öğesine eklenen düğmeler, LinkButtons veya ımagebuttons da içerebilir. BoundField 'da olduğu gibi, tıklandığı sırada bu düğmeler, GridView 'un `RowCommand` olayını oluşturacak şekilde bir geri gönderim kullanacaktır. Ancak, bir TemplateField öğesine düğme eklenirken düğme `CommandArgument`, ButtonFields kullanılırken olduğu gibi otomatik olarak satır dizinine ayarlanır. `RowCommand` olay işleyicisi içinde tıklanan düğmenin satır dizinini belirlemeniz gerekiyorsa, aşağıdaki kodu kullanarak düğmenin `CommandArgument` özelliğini TemplateField içindeki bildirime dayalı sözdiziminde el ile ayarlamanız gerekir:  
> `<asp:Button runat="server" ... CommandArgument='<%# ((GridViewRow) Container).RowIndex %>'`.

## <a name="summary"></a>Özet

GridView, DetailsView ve FormView denetimleri hepsi, düğme, LinkButtons veya ımagebuttons içerebilir. Bu tür düğmeler tıklandığında, geri göndermeye neden olur ve FormView ve DetailsView denetimlerinde `ItemCommand` olayı ve GridView 'daki `RowCommand` olayını yükseltir. Bu veri Web denetimlerinde, kayıtları silme veya düzenlemeyle ilgili yaygın komutla ilgili eylemleri işlemek için yerleşik işlevlere sahiptir. Ancak, tıklandığı zaman kendi özel kodumuzu yürütme ile yanıt veren düğmeleri de kullanabiliriz.

Bunu gerçekleştirmek için `ItemCommand` veya `RowCommand` olayı için bir olay işleyicisi oluşturmanız gerekir. Bu olay işleyicisinde, hangi düğmenin tıklandığını belirleyip ardından uygun özel eylemi ele almak için ilk olarak gelen `CommandName` değerini denetliyoruz. Bu öğreticide, belirli bir tedarikçiye yönelik tüm ürünleri sona erdirmek veya belirli bir ürünün fiyatını %10 oranında artırmak veya azaltmak için düğmeler ve Buttonalanlarını nasıl kullanacağınızı gördünüz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Next](adding-and-responding-to-buttons-to-a-gridview-vb.md)
