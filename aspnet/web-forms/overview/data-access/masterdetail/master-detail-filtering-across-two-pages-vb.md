---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: Iki sayfada ana/ayrıntı filtreleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, veritabanındaki tedarikçileri listelemek için GridView kullanarak bu kalıbı uygulayacağız. GridView 'daki her bir tedarikçi satırı, bir görüntüle içerir...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 252c6d5e48aff0087e090e3ddc1f58c84a2c030e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74622492"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>İki Sayfada Ana/Ayrıntı Filtreleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe) veya [PDF 'yi indirin](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> Bu öğreticide, veritabanındaki tedarikçileri listelemek için GridView kullanarak bu kalıbı uygulayacağız. GridView 'daki her bir tedarikçi satırı, tıklatıldığında, kullanıcıyı seçili tedarikçi için bu ürünleri listeleyen ayrı bir sayfaya alacak bir görünüm ürünleri bağlantısı içerir.

## <a name="introduction"></a>Giriş

Önceki iki öğreticilerde, "Ayrıntılar" göstermek için "ana" kayıtları ve bir [GridView](master-detail-filtering-with-a-dropdownlist-vb.md) ya da [DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md) denetimini göstermek üzere dropdownlists kullanarak ana/ayrıntı raporlarının tek bir Web sayfasında nasıl görüntüleneceğini gördük. Ana/ayrıntı raporlarında kullanılan diğer yaygın bir düzende, bir Web sayfasında ana kayıtlar ve başka bir sayfada gösterilen ayrıntılar yer alır. [ASP.net forumları](https://forums.asp.net/)gibi bir Forum Web sitesi, uygulamada bu düzenin harika bir örneğidir. ASP.NET forumları, daha fazla Forum, Web Forms, veri sunum denetimleri ve benzeri bir deyişle oluşur. Her Forum birçok iş parçacığından oluşur ve her iş parçacığı bir dizi gönderilerinden oluşur. ASP.NET forumları giriş sayfasında, Forumlar listelenir. Bir foruma tıkladığınızda, bu forum için iş parçacıklarını listeleyen `ShowForum.aspx` sayfasına gidin. Benzer şekilde, bir iş parçacığına tıkladığınızda tıklamış olan iş parçacığının gönderilerini görüntüleyen `ShowPost.aspx`olur.

Bu öğreticide, veritabanındaki tedarikçileri listelemek için GridView kullanarak bu kalıbı uygulayacağız. GridView 'daki her bir tedarikçi satırı, tıklatıldığında, kullanıcıyı seçili tedarikçi için bu ürünleri listeleyen ayrı bir sayfaya alacak bir görünüm ürünleri bağlantısı içerir.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>1\. adım: `Filtering`klasöre`SupplierListMaster.aspx`ve`ProductsForSupplierDetails.aspx`sayfaları ekleme

Üçüncü öğreticide sayfa düzeni tanımlarken, `BasicReporting`, `Filtering`ve `CustomFormatting` klasörlere bir dizi "başlangıç" sayfası ekledik. Bununla birlikte, bu öğretici için bu Öğreticiye bir başlangıç sayfası eklemedik, `Filtering` klasöre iki yeni sayfa eklemek için bir dakikanızı ayırın: `SupplierListMaster.aspx` ve `ProductsForSupplierDetails.aspx`. `SupplierListMaster.aspx`, `ProductsForSupplierDetails.aspx` seçili tedarikçinin ürünlerini görüntüleyeceği "ana" kayıtları (tedarikçiler) listeler.

Bu iki yeni sayfanın oluşturulması, bunları `Site.master` ana sayfayla ilişkilendirmeye yönelik olarak.

![Filtre klasörüne SupplierListMaster. aspx ve ProductsForSupplierDetails. aspx sayfalarını ekleyin](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**Şekil 1**: `Filtering` klasöre `SupplierListMaster.aspx` ve `ProductsForSupplierDetails.aspx` sayfalarını ekleyin

Ayrıca, projeye yeni sayfalar eklerken, site eşleme dosyası `Web.sitemap`, buna göre güncelleştirdiğinizden emin olun. Bu öğretici için, filtreleme raporlarının `<siteMapNode>` öğesinin bir alt öğesi olarak aşağıdaki XML içeriğini kullanarak site haritasına `SupplierListMaster.aspx` sayfasını ekleyin.

[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> [K. Scott Allen](http://odetocode.com/Blogs/scott/)'ın ücretsiz Visual Studio [site haritası makrosunu](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)kullanarak yeni ASP.NET sayfaları eklerken site haritası dosyasını güncelleştirme işlemini otomatikleştirmenize yardımcı olabilirsiniz.

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>2\. adım: `SupplierListMaster.aspx` 'da tedarikçi listesini görüntüleme

`SupplierListMaster.aspx` ve `ProductsForSupplierDetails.aspx` sayfaları oluşturulduktan sonra, bir sonraki adımımız `SupplierListMaster.aspx`tedarikçilerin GridView 'u oluşturmaktır. Sayfaya bir GridView ekleyin ve bunu yeni bir ObjectDataSource 'a bağlayın. Bu ObjectDataSource, tüm tedarikçileri döndürmek için `SuppliersBLL` sınıfının `GetSuppliers()` yöntemini kullanmalıdır.

[SuppliersBLL sınıfını seçin ![](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**Şekil 2**: `SuppliersBLL` sınıfını seçin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image4.png))

[![, GetSuppliers () yöntemini kullanmak için ObjectDataSource 'ı yapılandırma](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**Şekil 3**: ObjectDataSource 'ı `GetSuppliers()` yöntemini kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image7.png))

Tıklandığı zaman, Kullanıcı QueryString aracılığıyla seçili satırın `SupplierID` değerini geçirilerek `ProductsForSupplierDetails.aspx`, her GridView satırına görünüm ürünleri başlıklı bir bağlantı içermesi gerekir. Örneğin, Kullanıcı, Tokyo Traders tedarikçisine ait ürünleri görüntüle bağlantısına tıklasa (`SupplierID` değeri 4 ' e sahiptir), bunların `ProductsForSupplierDetails.aspx?SupplierID=4`gönderilmesi gerekir.

Bunu gerçekleştirmek için GridView 'a bir [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) ekleyin ve bu, her GridView satırına bir köprü ekler. GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayarak başlayın. Ardından, sol üst taraftaki listeden Hyperlinkalanını seçin ve Ekle ' ye tıklayarak GridView 'un alan listesine Hyperlinkalanını ekleyin.

[GridView 'a HyperLinkField eklemek ![](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**Şekil 4**: GridView 'a HyperLinkField ekleyin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image10.png))

Hyperlinkalanı her bir GridView satırındaki bağlantıyla aynı metin veya URL değerlerini kullanacak şekilde yapılandırılabilir veya bu değerleri belirli bir satıra bağlı veri değerlerinde temel alabilir. Tüm satırlarda statik bir değer belirtmek için Hyperlinkalanının `Text` veya `NavigateUrl` özelliklerini kullanın. Bağlantı metninin tüm satırlar için aynı olmasını istediğimiz için, Hyperlinkalanının `Text` özelliğini ürünleri görüntülemek için ayarlayın.

[![alanları görüntülemek için Hyperlinkalanının Text özelliğini ayarlayın](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**Şekil 5**: HyperLinkField 'ın `Text` özelliğini ürünleri görüntülemek için ayarlayın ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image13.png))

Metin veya URL değerlerini GridView satırına bağlı temel veriye göre olacak şekilde ayarlamak için, metin veya URL değerlerinin `DataTextField` veya `DataNavigateUrlFields` özelliklerinden çekililmesi gereken veri alanlarını belirtin. `DataTextField` yalnızca tek bir veri alanına ayarlanabilir; Ancak `DataNavigateUrlFields`, virgülle ayrılmış veri alanları listesine ayarlanabilir. Genellikle metin veya URL 'YI geçerli satırın veri alanı değerinin bir birleşimine ve bazı statik biçimlendirmeye dayandırıyoruz. Bu öğreticide, örneğin, her bir GridView 'un Row`SupplierID` değeri *`supplierID`* , HyperLinkField BAĞLANTıLARıNıN URL 'sinin `ProductsForSupplierDetails.aspx?SupplierID=supplierID`olmasını istiyoruz. Burada hem statik hem de veri tabanlı değerlere ihtiyacımız olduğuna dikkat edin: bağlantı URL 'sinin `ProductsForSupplierDetails.aspx?SupplierID=` kısmı statik, ancak *`supplierID`* bölümü değeri her satırın kendi `SupplierID` değeri olduğu için veri odaklı olur.

Statik ve veri tabanlı değerlerin bir birleşimini göstermek için `DataTextFormatString` ve `DataNavigateUrlFormatString` özelliklerini kullanın. Bu özelliklerde, gerekirse statik biçimlendirmeyi girin ve sonra `DataTextField` veya `DataNavigateUrlFields` özelliklerinde belirtilen alanın değerinin görüntülenmesini istediğiniz işareti `{0}` işaretini kullanın. `DataNavigateUrlFields` özelliğinde, ilk alan değerinin eklenmesini istediğiniz birden `{0}` çok alan `{1}`, ikinci alan değeri için ve bu şekilde devam eder.

Bunu öğreticimize uygulayarak `DataNavigateUrlFields` özelliğini `SupplierID`olarak ayarlamanız gerekir, çünkü değeri her satır temelinde özelleştirmeniz gereken veri alanı ve `DataNavigateUrlFormatString` özelliği de `ProductsForSupplierDetails.aspx?SupplierID={0}`.

[![, doğru bağlantı URL 'sini TedarikçiKimliği 'e göre eklemek için Hyperlinkalanını yapılandırın](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**Şekil 6**: Hyperlinkalanını `SupplierID` göre uygun bağlantı URL 'sini Içerecek şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image16.png))

Hyperlinkalanını ekledikten sonra GridView 'un alanlarını özelleştirmek ve yeniden sıralamak ücretsizdir. Aşağıdaki biçimlendirme, bazı küçük alan düzeyi özelleştirmeler yaptıktan sonra GridView 'ı gösterir.

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

`SupplierListMaster.aspx` sayfasını bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Şekil 7 ' de gösterildiği gibi, sayfa şu anda ürünleri görüntüle bağlantısı dahil olmak üzere tüm tedarikçilerini listeler. Ürünleri görüntüle bağlantısına tıkladığınızda, `ProductsForSupplierDetails.aspx`, bu işlem, tedarikçinin `SupplierID` bir sorgu dizesi aracılığıyla geçer.

[Her bir tedarikçi satırı ![ürünleri görüntüle bağlantısı Içerir](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**Şekil 7**: Her tedarikçi satırı bir görünüm ürünleri bağlantısını Içerir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image19.png))

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>3\. adım: Tedarikçinin ürünlerini`ProductsForSupplierDetails.aspx` listeleme

Bu noktada, `SupplierListMaster.aspx` sayfası kullanıcıları `ProductsForSupplierDetails.aspx`gönderiyor ve seçilen tedarikçinin `SupplierID` QueryString içinde geçiyor. Öğreticinin son adımı, `SupplierID`, QueryString aracılığıyla geçirilen `SupplierID` eşit olan `ProductsForSupplierDetails.aspx` GridView 'da görüntülemek içindir. `ProductsForSupplierDetails.aspx` sayfasına bir GridView ekleyerek, `ProductsBLL` sınıfından `GetProductsBySupplierID(supplierID)` yöntemini çağıran `ProductsBySupplierDataSource` adlı yeni bir ObjectDataSource denetimi kullanarak bu başlatmayı başarmak için.

[![ProductsBySupplierDataSource adlı yeni bir ObjectDataSource ekleyin](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**Şekil 8**: `ProductsBySupplierDataSource` adlı yeni bir ObjectDataSource ekleyin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image22.png))

[ProductsBLL sınıfını seçin ![](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**Şekil 9**: `ProductsBLL` sınıfını seçin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image25.png))

[![ObjectDataSource, Getproductsbysupplierıd (SupplierID) yöntemini çağırsın](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**Şekil 10**: ObjectDataSource 'un `GetProductsBySupplierID(supplierID)` metodunu çağırmasını[sağlar (tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image28.png))

Veri kaynağını yapılandırma sihirbazının son adımı, `GetProductsBySupplierID(supplierID)` yönteminin *`supplierID`* parametresinin kaynağını sağlamamızı ister. QueryString değerini kullanmak için, parametre kaynağını QueryString olarak ayarlayın ve QueryStringField metin kutusunda kullanılacak QueryString değeri adını girin (`SupplierID`).

[SupplierID parametre değerini SupplierID QueryString değerinden doldurmak ![](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**Şekil 11**: *`supplierID`* parametre değerini `SupplierID` QueryString değerinden doldur ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image31.png))

İşte bu kadar kolay! Şekil 12 ' de, `SupplierListMaster.aspx`Tokyo Traders bağlantısına tıklanarak ziyaret edildiğinde `ProductsForSupplierDetails.aspx` sayfası gösterilmektedir.

[![Tokyo Traders tarafından sağlanan ürünlerin gösterilmesi](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**Şekil 12**: Tokyo Traders tarafından sağlanan ürünler gösterilir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image34.png))

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>`ProductsForSupplierDetails.aspx` 'da Tedarikçi bilgilerini görüntüleme

Şekil 12 ' de gösterildiği gibi, `ProductsForSupplierDetails.aspx` sayfası yalnızca QueryString içinde belirtilen `SupplierID` tarafından sağlanan ürünleri listeler. Ancak bu sayfaya doğrudan gönderilen birisi, Şekil 12 ' nin Tokyo Traders ürünlerini gösterdiği olduğunu bilmez. Bu sorunu gidermek için, bu sayfada Tedarikçi bilgilerini de görüntüleriz.

GridView ürünlerinin üzerine bir FormView ekleyerek başlayın. `SuppliersBLL` sınıfının `GetSupplierBySupplierID(supplierID)` yöntemini çağıran `SuppliersDataSource` adlı yeni bir ObjectDataSource denetimi oluşturun.

[SuppliersBLL sınıfını seçin ![](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**Şekil 13**: `SuppliersBLL` sınıfını seçin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image37.png))

[![ObjectDataSource, Getsupplierbysupplierıd (SupplierID) yöntemini çağırsın](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**Şekil 14**: ObjectDataSource 'un `GetSupplierBySupplierID(supplierID)` metodunu çağırmasını[sağlar (tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image40.png))

`ProductsBySupplierDataSource`olduğu gibi, *`supplierID`* parametresinin `SupplierID` QueryString değeri değerine atanmasını sağlayabilirsiniz.

[SupplierID parametre değerini SupplierID QueryString değerinden doldurmak ![](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**Şekil 15**: *`supplierID`* parametre değerini `SupplierID` QueryString değerinden doldur ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image43.png))

FormView, Tasarım görünümü ObjectDataSource 'a bağlarken, Visual Studio otomatik olarak FormView 'un `ItemTemplate`, `InsertItemTemplate`ve `EditItemTemplate`, ObjectDataSource tarafından döndürülen her veri alanı için etiket ve metin kutusu Web denetimleriyle birlikte oluşturur. Yalnızca üretici bilgilerini `InsertItemTemplate` ve `EditItemTemplate`kaldırmak için ücretsiz olarak göstermek istiyoruz. Ardından, bir `<h3>` öğesinde tedarikçinin şirket adını ve şirket adının altındaki Adres, şehir, ülke ve telefon numarasını görüntüleyecek şekilde ItemTemplate 'i düzenleyin. Alternatif olarak, "[ObjectDataSource Ile verileri görüntüleme](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)" öğreticisini geri yaptığımız gibi FormView 'un `DataSourceID` el ile ayarlayabilir ve `ItemTemplate` işaretlemesini oluşturabilirsiniz.

Bu düzenlemeleriniz sonrasında, FormView 'un bildirim temelli işaretleme aşağıdakine benzer görünmelidir:

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

Şekil 16, yukarıdaki tedarikçi bilgileri eklendikten sonra `ProductsForSupplierDetails.aspx` sayfasının ekran görüntüsünü gösterir.

[Ürünlerin listesi ![tedarikçi hakkında bir Özet Içerir](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**Şekil 16**: Ürünlerin listesi, tedarikçiyle Ilgili bir Özet Içerir ([tam boyutlu görüntüyü görüntülemek Için tıklatın](master-detail-filtering-across-two-pages-vb/_static/image46.png))

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>`ProductsForSupplierDetails.aspx`Kullanıcı arabirimine son dokunmayı uygulama

Bu rapor için Kullanıcı deneyimini geliştirmek üzere `ProductsForSupplierDetails.aspx` sayfasında yapmak için çok sayıda ekleme vardır. Şu anda bir kullanıcının `ProductsForSupplierDetails.aspx` sayfasından üretici listesine geri gidebilmeleri için, tarayıcının geri düğmesine tıklamanız yeterlidir. `ProductsForSupplierDetails.aspx` sayfasına, kullanıcının ana listeye geri dönmesi için başka bir yol sağlayarak `SupplierListMaster.aspx`geri bağlayan bir köprü denetimi ekleyelim.

[Kullanıcıyı SupplierListMaster. aspx öğesine geri çekmek için köprü denetimi ekleme ![](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**Şekil 17**: Kullanıcıyı `SupplierListMaster.aspx` geri çekmek için bir köprü denetimi ekleyin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-vb/_static/image49.png))

Kullanıcı herhangi bir ürüne sahip olmayan bir tedarikçi için ürünleri görüntüle bağlantısına tıklasa, `ProductsForSupplierDetails.aspx` `ProductsBySupplierDataSource` ObjectDataSource hiçbir sonuç döndürmez. ObjectDataSource 'a bağlı GridView, kullanıcının tarayıcısında sayfada boş bir bölgeye neden olan herhangi bir biçimlendirmeyi işlemez. Seçili tedarikçiyle ilişkili ürün olmadığından, kullanıcıyla daha net bir şekilde iletişim kurmak için GridView 'un `EmptyDataText` özelliğini, böyle bir durum ortaya çıkarsa görüntülenmesini istediğimiz ileti olarak ayarlayabiliriz. Bu özelliği "Bu tedarikçi tarafından sunulan ürün yok" olarak ayarladı

Varsayılan olarak, Northwinds veritabanındaki tüm tedarikçiler en az bir ürün sağlar. Bununla birlikte, bu öğretici için `Products` tablosunu el ile değiştirdim ve bu sayede tedarikçinin escargots nouveaux, artık hiçbir ürünle ilişkili değil. Şekil 18, bu değişiklik yapıldıktan sonra escargots nouveaux için Ayrıntılar sayfasını gösterir.

[![kullanıcılara tedarikçinin herhangi bir ürün Sağlamadiğini bilgilendirilir](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**Şekil 18**: Kullanıcılara tedarikçinin hiçbir ürün Sağlamabileceği bildirilir ([tam boyutlu görüntüyü görüntülemek Için tıklatın](master-detail-filtering-across-two-pages-vb/_static/image52.png))

## <a name="summary"></a>Özet

Ana/ayrıntı raporları hem ana hem de ayrıntı kayıtlarını tek bir sayfada görüntüleyebilir, ancak birçok Web sitesinde iki Web sayfasında ayrılır. Bu öğreticide, "ana" Web sayfasındaki bir GridView 'da listelenen tedarikçilere ve "Ayrıntılar" sayfasında listelenen ilişkili ürünlere sahip olarak böyle bir Master/Detail raporunun nasıl uygulanacağını inceledik. Ana Web sayfasındaki her bir tedarikçi satırı, satırın `SupplierID` değerinin yanında geçen ayrıntılar sayfasına bir bağlantı içeriyordu. Bu tür satıra özgü bağlantılar, GridView 'un Hyperlinkalanı kullanılarak kolayca eklenebilir.

Ayrıntılar sayfasında, belirtilen tedarikçi için bu ürünlerin alınması `ProductsBLL` sınıfın `GetProductsBySupplierID(supplierID)` yöntemi çağrılarak gerçekleştirildi. *`supplierID`* parametre değeri, parametre kaynağı olarak QueryString kullanılarak bildirimli olarak belirtildi. Ayrıca, ayrıntılar sayfasında bir FormView kullanarak tedarikçi ayrıntılarının nasıl görüntüleneceğini de inceledik.

[Sonraki öğreticimiz](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) ana/ayrıntı raporlarında son bir deneyimdir. Bir GridView 'da, her satırda bir Seç düğmesi bulunan ürünlerin listesini görüntüleme bölümüne bakacağız. Seç düğmesine tıkladığınızda bu ürünün ayrıntıları aynı sayfada bir DetailsView denetiminde görüntülenir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](master-detail-filtering-with-two-dropdownlists-vb.md)
> [İleri](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)
