---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
title: Özel bir veritabanı odaklı site haritası sağlayıcısı oluşturma (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET 2,0 ' deki varsayılan site haritası sağlayıcısı, verilerini statik bir XML dosyasından alır. XML tabanlı sağlayıcı çok küçük ve orta-siz için uygun olduğunda...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: f904cd2c-a408-4484-9324-8b8d7fe33893
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
msc.type: authoredcontent
ms.openlocfilehash: 78051696bd75e1d574f55b1c5d5891fe67c3030d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78595370"
---
# <a name="building-a-custom-database-driven-site-map-provider-vb"></a>Özel Bir Veritabanı Odaklı Site Haritası Sağlayıcısı Oluşturma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_VB.zip) veya [PDF 'yi indirin](building-a-custom-database-driven-site-map-provider-vb/_static/datatutorial62vb1.pdf)

> ASP.NET 2,0 ' deki varsayılan site haritası sağlayıcısı, verilerini statik bir XML dosyasından alır. XML tabanlı sağlayıcı çok küçük ve orta ölçekli web sitelerine uygun olsa da, daha büyük web uygulamaları daha dinamik bir site eşlemesi gerektirir. Bu öğreticide, verileri Iş mantığı katmanından alan özel bir site haritası sağlayıcısı oluşturacağız ve bu, verileri veritabanından alır.

## <a name="introduction"></a>Giriş

ASP.NET 2,0 s site haritası özelliği, bir sayfa geliştiricisinin bir XML dosyası gibi bazı kalıcı bir medyada Web uygulaması site haritası tanımlamasına olanak sağlar. Tanımlandıktan sonra, site haritası verilerine [`System.Web` ad](https://msdn.microsoft.com/library/system.web.aspx) alanındaki [`SiteMap` sınıfı](https://msdn.microsoft.com/library/system.web.sitemap.aspx) aracılığıyla veya (örneğin,, menü ve TreeView denetimleri) çeşitli gezinti Web denetimleri aracılığıyla erişilebilir. Site Haritası sistemi, farklı site haritası serileştirme uygulamalarının oluşturulup bir Web uygulamasına takılabilmesi için [sağlayıcı modelini](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) kullanır. ASP.NET 2,0 ile birlikte gelen varsayılan site haritası sağlayıcısı, site haritası yapısını bir XML dosyasında devam ettirir. [Ana sayfalar ve site gezinti](../introduction/master-pages-and-site-navigation-vb.md) öğreticisine geri döndüğünüzde, bu yapıyı içeren `Web.sitemap` adlı bir dosya oluşturdunuz ve kendi XML 'sini her yeni öğretici bölümüyle güncelleştirdik.

Varsayılan XML tabanlı site haritası sağlayıcısı, bu öğreticiler gibi site haritası s yapısı oldukça statikse iyi bir şekilde çalışacaktır. Ancak birçok senaryoda, daha dinamik bir site haritası gerekir. Şekil 1 ' de gösterilen site haritasını göz önünde bulundurun; burada her bir kategori ve ürün, Web sitesi yapısında bölüm olarak görünür. Bu site haritasında, kök düğüme karşılık gelen Web sayfasını ziyaret eden tüm kategoriler listeleyebilir, ancak belirli bir kategorinin bir Web sayfasını ziyaret etmek, bu ürün ve belirli bir ürün Web sayfasını görüntülemek için bu ürün ayrıntılarını gösterir.

[Kategori ve ürünlerin site haritası yapısını derleme ![](building-a-custom-database-driven-site-map-provider-vb/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image1.png)

**Şekil 1**: Kategoriler ve ürünler site haritası yapısını derleme ([tam boyutlu görüntüyü görüntülemek için tıklatın](building-a-custom-database-driven-site-map-provider-vb/_static/image2.png))

Bu kategori ve ürün tabanlı yapı `Web.sitemap` dosyasına sabit olarak kodlanmasına karşın, bir kategori veya ürün eklendiğinde, kaldırıldığında veya yeniden adlandırıldığında dosyanın güncellenmesi gerekir. Sonuç olarak, site haritası bakımı, yapısı veritabanından alınırsa veya ideal olarak, uygulama mimarisinin Iş mantığı katmanından büyük ölçüde basitleştirilir. Bu şekilde, ürünler ve Kategoriler eklendikçe, yeniden adlandırıldığı veya silindiği için, site haritası bu değişiklikleri yansıtacak şekilde otomatik olarak güncelleştirilecek.

ASP.NET 2,0 s site haritası serileştirme, sağlayıcı modeline göre oluşturulduğundan, verileri veritabanı veya mimari gibi alternatif bir veri deposundan kullanan kendi özel site haritası sağlayıcımızı oluşturabiliriz. Bu öğreticide, BLL 'den verilerini alan özel bir sağlayıcı oluşturacağız. Haydi başlayın!

> [!NOTE]
> Bu öğreticide oluşturulan özel site haritası sağlayıcısı, uygulama mimarisi ve veri modeliyle sıkı bir şekilde bağlanmış. [SQL Server ' de site haritalarını depolayan](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) Jeff Prosise s ve makaleler [Için bekleyen SQL site haritası sağlayıcısı,](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) site haritası verilerini SQL Server depolamak için genelleştirilmiş bir yaklaşım inceliyor.

## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>Adım 1: özel site haritası sağlayıcı Web sayfaları oluşturma

Özel bir site haritası sağlayıcısı oluşturmaya başlamadan önce, ilk olarak bu öğreticide ihtiyacımız olan ASP.NET sayfaları ekleyelim. `SiteMapProvider`adlı yeni bir klasör ekleyerek başlayın. Ardından, aşağıdaki ASP.NET sayfalarını bu klasöre ekleyerek her bir sayfayı `Site.master` ana sayfasıyla ilişkilendirdiğinizden emin olun:

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

Ayrıca, `App_Code` klasörüne bir `CustomProviders` alt klasörü ekleyin.

![Site Haritası sağlayıcısına ilişkin ASP.NET sayfalarını ekleme-Ilgili öğreticiler](building-a-custom-database-driven-site-map-provider-vb/_static/image2.gif)

**Şekil 2**: site haritası sağlayıcısına Ilişkin ASP.NET sayfalarını ekleme-ilgili öğreticiler

Bu bölüm için yalnızca bir öğretici olduğundan, Bölüm öğreticileri hakkında `Default.aspx` gerekmez. Bunun yerine, `Default.aspx` kategorileri bir GridView denetiminde görüntüler. 2\. adımda bunu ele alacağız.

Sonra, `Default.aspx` sayfasına bir başvuru eklemek için `Web.sitemap` güncelleştirin. Özellikle, önbelleğe alma `<siteMapNode>`sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık tek site eşleme sağlayıcısı öğreticisi için bir öğe içeriyor.

![Site Haritası artık site haritası sağlayıcısı öğreticisi için bir giriş Içerir](building-a-custom-database-driven-site-map-provider-vb/_static/image3.gif)

**Şekil 3**: site haritası artık site haritası sağlayıcısı öğreticisi Için bir giriş içerir

Bu öğretici ana odak, özel bir site haritası sağlayıcısı oluşturmayı ve bu sağlayıcıyı kullanmak için bir Web uygulaması yapılandırmayı göstermektir. Özellikle, Şekil 1 ' de gösterildiği gibi her bir kategori ve ürün için bir düğüm ile birlikte kök düğüm içeren bir site haritası döndüren bir sağlayıcı oluşturacağız. Genel olarak, site eşlemesindeki her düğüm bir URL belirtebilir. Site Haritamız için kök düğüm s URL 'SI `~/SiteMapProvider/Default.aspx`olacak ve bu, veritabanındaki tüm kategorileri listeleyebileceğiniz anlamına gelir. Site haritadaki her kategori düğümü, belirtilen *CategoryID*'deki tüm ürünleri listeleyebileceğiniz `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`işaret eden bir URL 'ye sahip olur. Son olarak, her ürün site haritası düğümü `~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`işaret eder ve bu da belirli ürün ayrıntılarını görüntüler.

Başlamak için `Default.aspx`, `ProductsByCategory.aspx`ve `ProductDetails.aspx` sayfalarını oluşturmaya ihtiyacım var. Bu sayfalar sırasıyla 2, 3 ve 4. adımlarda tamamlanır. Bu öğreticinin sahibi site haritası sağlayıcılarında olduğundan ve geçmiş öğreticilerin bu çok sayfalı ana/ayrıntı raporlarının oluşturulmasını kapsadığından, 2 ile 4 arasındaki adımları karşılıyoruz. Birden çok sayfayı kapsayan ana/ayrıntı raporlarını oluştururken bir yenileyici gerekiyorsa, [Iki sayfa üzerinde ana/ayrıntı filtrelemesine](../masterdetail/master-detail-filtering-across-two-pages-vb.md) geri bakın.

## <a name="step-2-displaying-a-list-of-categories"></a>2\. Adım: kategorilerin listesini görüntüleme

`SiteMapProvider` klasöründeki `Default.aspx` sayfasını açın ve araç kutusu 'ndaki bir GridView 'u `ID` `Categories`olarak ayarlayarak tasarımcı üzerine sürükleyin. GridView s akıllı etiketinden, `CategoriesDataSource` adlı yeni bir ObjectDataSource 'a bağlayın ve `CategoriesBLL` sınıf s `GetCategories` metodunu kullanarak verilerini alması için yapılandırın. Bu GridView yalnızca kategorileri görüntülüyor ve veri değiştirme özellikleri sağlamadığı için GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden (hiçbiri) açılan listeleri ayarlayın.

[![, GetCategories metodunu kullanarak kategorileri döndürecek şekilde yapılandırın](building-a-custom-database-driven-site-map-provider-vb/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image3.png)

**Şekil 4**: `GetCategories` yöntemini kullanarak ([tam boyutlu görüntüyü görüntülemek Için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image4.png)) ObjectDataSource 'ı kategorileri döndürecek şekilde yapılandırın

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](building-a-custom-database-driven-site-map-provider-vb/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.png)

**Şekil 5**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinden açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image6.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`ve `BrochurePath`için bir BoundField ekler. GridView 'ı yalnızca `CategoryName` ve `Description` BoundFields alanlarını içerecek şekilde düzenleyin ve `CategoryName` BoundField ' `HeaderText` özelliğini category olarak güncelleştirin.

Sonra, bir HyperLinkField ekleyin ve bunu en sol alan olacak şekilde konumlandırın. `DataNavigateUrlFields` özelliğini `CategoryID` ve `DataNavigateUrlFormatString` özelliğini `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`olarak ayarlayın. `Text` özelliğini ürünleri görüntülemek için ayarlayın.

![GridView 'a HyperLinkField ekleyin](building-a-custom-database-driven-site-map-provider-vb/_static/image6.gif)

**Şekil 6**: `Categories` GridView 'A HyperLinkField ekleyin

ObjectDataSource oluşturup GridView s alanlarını özelleştirdikten sonra, iki denetim bildirim temelli biçimlendirme aşağıdaki gibi görünür:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample2.aspx)]

Şekil 7 ' de bir tarayıcıdan görüntülendiklerinde `Default.aspx` gösterilmektedir. Bir kategori s View Products bağlantısına tıkladığınızda sizi adım 3 ' te oluşturacağız `ProductsByCategory.aspx?CategoryID=categoryID`.

[![her kategori bir görünüm ürünleri bağlantısıyla birlikte listelenir](building-a-custom-database-driven-site-map-provider-vb/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image7.png)

**Şekil 7**: her kategori bir görünüm ürünleri bağlantısıyla birlikte listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image8.png))

## <a name="step-3-listing-the-selected-category-s-products"></a>3\. Adım: Seçili Kategori ürünlerini listeleme

`ProductsByCategory.aspx` sayfasını açın ve `ProductsByCategory`adlandırarak bir GridView ekleyin. Akıllı etiketinden, GridView 'u `ProductsByCategoryDataSource`adlı yeni bir ObjectDataSource 'a bağlayın. ObjectDataSource 'u `ProductsBLL` sınıf s `GetProductsByCategoryID(categoryID)` metodunu kullanacak şekilde yapılandırın ve GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinde açılan listeleri (yok) olarak ayarlayın.

[![ProductsBLL Class s Getproductsbycategoryıd (CategoryID) metodunu kullanın](building-a-custom-database-driven-site-map-provider-vb/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image9.png)

**Şekil 8**: `ProductsBLL` Class s `GetProductsByCategoryID(categoryID)` metodunu kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image10.png))

Veri kaynağını yapılandırma Sihirbazı ' nda son adım *CategoryID*için bir parametre kaynağı sorar. Bu bilgiler `CategoryID`QueryString alanından geçtiğinden, açılan listeden QueryString ' i seçin ve Şekil 9 ' da gösterildiği gibi QueryStringField metin kutusuna CategoryID yazın. Sihirbazı tamamladığınızda son ' a tıklayın.

[CategoryID parametresi için CategoryID QueryString alanını kullanın ![](building-a-custom-database-driven-site-map-provider-vb/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image11.png)

**Şekil 9**: *categoryıd* parametresi için `CategoryID` QueryString alanını kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image12.png))

Sihirbaz tamamlandıktan sonra Visual Studio, ürün verileri alanları için ilgili BoundFields ve bir CheckBoxField öğesini GridView 'a ekler. `ProductName`, `UnitPrice`ve `SupplierName` BoundFields hariç tümünü kaldırın. Bu üç sınır alanını, sırasıyla ürün, Fiyat ve tedarikçiyi okumak için `HeaderText` özelleştirin. `UnitPrice` BoundField öğesini para birimi olarak biçimlendirin.

Sonra, bir HyperLinkField ekleyin ve en soldaki konuma taşıyın. `Text` özelliğini, ayrıntıları, `DataNavigateUrlFields` özelliğini `ProductID`ve `DataNavigateUrlFormatString` özelliğini `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`olarak görüntülemek için ayarlayın.

![ProductDetails. aspx ' i Işaret eden bir görünüm ayrıntıları HyperLinkField ekleyin](building-a-custom-database-driven-site-map-provider-vb/_static/image10.gif)

**Şekil 10**: `ProductDetails.aspx` gösteren bir görünüm ayrıntıları hyperlinkalanı ekleme

Bu özelleştirmeler yapıldıktan sonra, GridView ve ObjectDataSource 'un bildirim temelli işaretlemesi aşağıdakine benzemelidir:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample3.aspx)]

`Default.aspx` bir tarayıcı aracılığıyla görüntülemek için geri dönün ve Içecek için ürünleri görüntüle bağlantısına tıklayın. Bu işlem sizi `ProductsByCategory.aspx?CategoryID=1`, Içgörüleri kategorisine ait olan Northwind veritabanındaki ürünlerin adlarını, fiyatlarını ve tedarikçilerini görmenizi sağlar (bkz. Şekil 11). Bu sayfayı, kullanıcıların Kategori listeleme sayfasına (`Default.aspx`) ve seçili kategori adı ve açıklamasını görüntüleyen bir DetailsView veya FormView denetimine geri dönmesi için bir bağlantı içermesi için de ücretsiz olarak geliştirebilirsiniz.

[Içsi adları, fiyatlar ve tedarikçiler ![görüntülenir](building-a-custom-database-driven-site-map-provider-vb/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image13.png)

**Şekil 11**: içecek adları, fiyatlar ve tedarikçiler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image14.png))

## <a name="step-4-showing-a-product-s-details"></a>4\. Adım: ürün s ayrıntılarını gösterme

Son sayfa `ProductDetails.aspx`, seçilen ürünlerin ayrıntılarını görüntüler. `ProductDetails.aspx` açın ve araç kutusundan bir DetailsView öğesini tasarımcı üzerine sürükleyin. DetailsView `ID` özelliğini `ProductInfo` olarak ayarlayın ve `Height` ve `Width` özellik değerlerini temizleyin. Kendi akıllı etiketinden, `ProductDataSource`adlı yeni bir ObjectDataSource 'a bağlayın ve `ProductsBLL` sınıf s `GetProductByProductID(productID)` yönteminden verileri çekmek için ObjectDataSource 'u yapılandırın. 2 ve 3. adımlarda oluşturulan önceki Web sayfalarında olduğu gibi, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden (hiçbiri) açılan listeleri ayarlayın.

[GetProductByProductID (ProductID) yöntemini kullanmak için ObjectDataSource 'ı yapılandırma ![](building-a-custom-database-driven-site-map-provider-vb/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.png)

**Şekil 12**: `GetProductByProductID(productID)` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image16.png))

Veri kaynağını yapılandırma sihirbazının son adımı, *ProductID* parametresinin kaynağını sorar. Bu veriler `ProductID`QueryString alanından geldiğinden, açılan listeyi QueryString ve QueryStringField metin kutusunu ProductID olarak ayarlayın. Son olarak, Sihirbazı tamamladıktan sonra son düğmesine tıklayın.

[![ProductID parametresini, ProductID QueryString alanından değerini çekmek için yapılandırın](building-a-custom-database-driven-site-map-provider-vb/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image17.png)

**Şekil 13**: *ProductID* parametresini, değerini `ProductID` QueryString alanından çekmek için yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image18.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio ilgili BoundFields ve ürün verileri alanları için DetailsView içinde bir CheckBoxField oluşturur. `ProductID`, `SupplierID`ve `CategoryID` BoundFields alanlarını kaldırın ve kalan alanları uygun gördüğünüz şekilde yapılandırın. Aesthetic Characteristics yapılandırmalarının, DetailsView 'umun ve ObjectDataSource 'un bildirim temelli biçimlendirmesi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample4.aspx)]

Bu sayfayı test etmek için `Default.aspx` dönün ve Içecek kategorisi için ürünleri görüntüle ' ye tıklayın. İçecek ürünleri listesinden, Chai Tea için Ayrıntıları görüntüle bağlantısına tıklayın. Bu, bir Chai Tea s ayrıntılarını gösteren `ProductDetails.aspx?ProductID=1`size götürür (bkz. Şekil 14).

[![Chai Tea s tedarikçisi, kategori, Fiyat ve diğer bilgiler görüntülenir](building-a-custom-database-driven-site-map-provider-vb/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image19.png)

**Şekil 14**: Chai Tea s tedarikçisi, kategori, Fiyat ve diğer bilgiler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image20.png))

## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>5\. Adım: bir site haritası sağlayıcısının Iç Işleyişini anlama

Site Haritası, Web sunucusu s bellekte bir hiyerarşi oluşturan `SiteMapNode` örneklerinin bir koleksiyonu olarak temsil edilir. Tam olarak bir kök olmalı, tüm kök olmayan düğümlerin tam olarak bir üst düğümü olmalıdır ve tüm düğümlerde rastgele sayıda alt öğe olabilir. Her `SiteMapNode` nesnesi, Web sitesi yapısındaki bir bölümü temsil eder; Bu bölümlerin genellikle karşılık gelen bir Web sayfası vardır. Sonuç olarak, [`SiteMapNode` sınıfı](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) `Title`, `Url`ve `Description`gibi özelliklere sahiptir ve `SiteMapNode` temsil ettiği bölüm için bilgi sağlar. Ayrıca hiyerarşideki her bir `SiteMapNode` benzersiz bir şekilde tanımlayan bir `Key` özelliği vardır ve bu hiyerarşiyi `ChildNodes`, `ParentNode`, `NextSibling`, `PreviousSibling`, vb. oluşturmak için kullanılan özellikleri de vardır.

Şekil 15, Şekil 1 ' den genel site haritası yapısını gösterir, ancak uygulama ayrıntıları daha ayrıntılı bir şekilde taslak yapılır.

[![her bir SiteMapNode 'un başlık, URL, anahtar ve benzeri özellikleri vardır](building-a-custom-database-driven-site-map-provider-vb/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.gif)

**Şekil 15**: her `SiteMapNode` `Title`, `Url`, `Key`vb. gibi özelliklere sahiptir ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image17.gif))

Site haritasına, [`System.Web` ad alanındaki](https://msdn.microsoft.com/library/system.web.aspx) [`SiteMap` sınıfı](https://msdn.microsoft.com/library/system.web.sitemap.aspx) aracılığıyla erişilebilir. Bu sınıf `RootNode` özelliği, site haritası kök `SiteMapNode` örneğini döndürür; `CurrentNode`, `Url` özelliği şu anda istenen sayfanın URL 'siyle eşleşen `SiteMapNode` döndürür. Bu sınıf, ASP.NET 2,0 s gezinti Web denetimleri tarafından dahili olarak kullanılır.

`SiteMap` sınıfı özelliklerine erişildiğinde, site eşleme yapısını bazı kalıcı ortamdan belleğe serileştirmelidir. Ancak, site haritası serileştirme mantığı `SiteMap` sınıfına sabit olarak kodlanmaz. Bunun yerine, çalışma zamanında `SiteMap` sınıfı, serileştirme için hangi site eşleme *sağlayıcısını* kullanacağınızı belirler. Varsayılan olarak, [`XmlSiteMapProvider` sınıfı](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx) kullanılır ve bu, site haritası yapısını düzgün BIÇIMLI bir XML dosyasından okur. Ancak, biraz iş sayesinde kendi özel site haritası sağlayıcımızı oluşturarız.

Tüm site haritası sağlayıcılarının, site haritası sağlayıcıları için gereken temel yöntemleri ve özellikleri içeren [`SiteMapProvider` sınıfından](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx)türetilmesi gerekir, ancak uygulama ayrıntılarının çoğunu atlar. İkinci bir sınıf, [`StaticSiteMapProvider`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx)`SiteMapProvider` sınıfını genişletir ve gerekli işlevselliğin daha sağlam bir uygulamasını içerir. Dahili olarak `StaticSiteMapProvider`, site haritasının `SiteMapNode` örneklerini bir `Hashtable` depolar ve `AddNode(child, parent)`, `RemoveNode(siteMapNode),` ve `Clear()` `SiteMapNode` iç `Hashtable`ekleyen ve çıkarmış yöntemler sağlar. `XmlSiteMapProvider` `StaticSiteMapProvider`türetilir.

`StaticSiteMapProvider`genişleten özel bir site eşleme sağlayıcısı oluştururken, geçersiz kılınabilmesi gereken iki Soyut yöntem vardır: [`BuildSiteMap`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx) ve [`GetRootNodeCore`](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx). `BuildSiteMap`, adının gösterdiği gibi, site haritası yapısının kalıcı depolamadan yüklenmesi ve bellekte oluşturulduğundan sorumludur. `GetRootNodeCore`, site eşlemesindeki kök düğümü döndürür.

Bir Web uygulamasının bir site haritası sağlayıcısı kullanabilmesi için önce uygulama yapılandırması 'nda kayıtlı olması gerekir. Varsayılan olarak, `XmlSiteMapProvider` sınıfı `AspNetXmlSiteMapProvider`adı kullanılarak kaydedilir. Ek site eşleme sağlayıcılarını kaydetmek için aşağıdaki biçimlendirmeyi `Web.config`ekleyin:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample5.xml)]

*Ad* değeri, sağlayıcıya okunabilir bir ad atar, ancak *tür* , site eşleme sağlayıcısının tam nitelikli tür adını belirtir. Özel site haritası sağlayıcımız oluşturulduktan sonra, adım 7 ' de *ad* ve *tür* değerlerinin somut değerlerini keşfedeceğiz.

Site haritası sağlayıcısı sınıfı, ilk kez `SiteMap` sınıfından erişildiğinde oluşturulur ve Web uygulamasının ömrü boyunca bellekte kalır. Site haritası sağlayıcısının birden çok, eşzamanlı Web sitesi ziyaretçilerinden çağrılabileceği yalnızca bir örneği olduğundan, sağlayıcı yöntemlerinin *iş parçacığı açısından güvenli*olması zorunludur.

Performans ve ölçeklenebilirlik nedenleriyle, bellek içi site eşleme yapısını önbelleğe aldık ve `BuildSiteMap` yöntemi her çağrıldığında bu önbelleğe alınmış yapıyı döndürmemiz önemlidir. `BuildSiteMap`, sayfada kullanımda olan gezinti denetimlerine ve site haritası yapısının derinliğine bağlı olarak, her kullanıcı için sayfa isteği başına birkaç kez çağrılabilir. Herhangi bir durumda, `BuildSiteMap` ' de site eşleme yapısını önbelleğe almadığımızda, her çağrıldığında, mimariden ürün ve kategori bilgilerini yeniden almanız gerekir (Bu, veritabanına bir sorgu oluşmasına neden olur). Önceki önbelleğe alma öğreticilerinde anlatıldığı gibi, önbelleğe alınan veriler eski hale gelebilir. Bunu yapmak için, ya zaman ya da SQL önbellek bağımlılığı tabanlı expiries 'yi kullanabiliriz.

> [!NOTE]
> Bir site haritası sağlayıcısı, isteğe bağlı olarak [`Initialize` yöntemi](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx)geçersiz kılabilir. `Initialize`, site eşleme sağlayıcısı ilk kez başlatıldığında ve şu gibi `<add>` öğesinde `Web.config` sağlayıcıya atanmış özel öznitelikleri geçirildiğinde çağrılır: `<add name="name" type="type" customAttribute="value" />`. Bir sayfa geliştiricisinin, sağlayıcı kodunu değiştirmek zorunda kalmadan çeşitli site haritası sağlayıcısıyla ilgili ayarları belirtmesini sağlamak istiyorsanız kullanışlıdır. Örneğin, kategori ve ürün verilerini mimarinin ötesinde doğrudan veritabanından okuuyoruz, büyük olasılıkla sayfa geliştiricisinin, sağlayıcı kodunda sabit kodlanmış bir değer kullanmak yerine `Web.config` aracılığıyla veritabanı bağlantı dizesini belirtmesini sağlamak istiyoruz. Adım 6 ' da derlenecek özel site haritası sağlayıcısı bu `Initialize` metodunu geçersiz kılmaz. `Initialize` yönteminin kullanılmasına ilişkin bir örnek için, [site haritalarını SQL Server makalesinde depolayan](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) [Jeff Prosise](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) s bölümüne bakın.

## <a name="step-6-creating-the-custom-site-map-provider"></a>6\. Adım: özel site haritası sağlayıcısı oluşturma

Northwind veritabanındaki Kategoriler ve ürünlerden site haritasını oluşturan özel bir site haritası sağlayıcısı oluşturmak için, `StaticSiteMapProvider`genişleten bir sınıf oluşturuyoruz. Adım 1 ' de `App_Code` klasörüne `CustomProviders` klasör eklemenizi istedi. bu klasöre `NorthwindSiteMapProvider`adlı yeni bir sınıf ekleyin. `NorthwindSiteMapProvider` sınıfına aşağıdaki kodu ekleyin:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample6.vb)]

Bir [`lock` bildirimiyle](https://msdn.microsoft.com/library/c5kehkcz.aspx)başlayan bu sınıf `BuildSiteMap` yöntemini keşfetmeye başlayın. `lock` deyimleri, tek seferde yalnızca bir iş parçacığının girmesine izin verir, böylece koda erişimi serileştirmesini ve iki eş zamanlı iş parçacığının başka bir yerde adımlanmasını önler.

Sınıf düzeyi `SiteMapNode` değişken `root`, site haritası yapısını önbelleğe almak için kullanılır. Site Haritası ilk kez oluşturulduğunda veya temel alınan veriler değiştirildikten sonra ilk kez için `root` `Nothing` olur ve site haritası yapısı oluşturulur. Site Haritası kök düğümü oluşturma işlemi sırasında `root` atandığında, bu yöntemin bir sonraki çağrılışında `root` `Nothing`olmayacaktır. Sonuç olarak, `root` `Nothing` olmadığı sürece site haritası yapısı yeniden oluşturmak zorunda kalmadan çağırana döndürülür.

Kök `Nothing`, site haritası yapısı ürün ve kategori bilgileri ' nden oluşturulur. Site Haritası, `SiteMapNode` örnekleri oluşturularak oluşturulur ve ardından hiyerarşi `StaticSiteMapProvider` sınıf s `AddNode` metoduna çağrılar aracılığıyla oluşturulur. `AddNode`, assıralanan `SiteMapNode` örneklerini bir `Hashtable`depolayarak iç muhasebeci gerçekleştirir. Hiyerarşiyi oluşturmadan önce, iç `Hashtable`öğeleri temizleyen `Clear` yöntemini çağırarak başladık. Sonra, `ProductsBLL` sınıf s `GetProducts` yöntemi ve elde edilen `ProductsDataTable` yerel değişkenlerde saklanır.

Site Haritası oluşturma işlemi, kök düğümü oluşturup `root`atamaya başlar. Burada kullanılan [`SiteMapNode` s oluşturucusunun](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx) aşırı yüklemesi ve bu `BuildSiteMap` boyunca aşağıdaki bilgiler geçirilir:

- Site eşleme sağlayıcısına (`Me`) yönelik bir başvuru.
- `SiteMapNode` s `Key`. Bu gerekli değer her `SiteMapNode`için benzersiz olmalıdır.
- `SiteMapNode` s `Url`. `Url` isteğe bağlıdır, ancak sağlanmışsa, her `SiteMapNode` s `Url` değeri benzersiz olmalıdır.
- Gerekli olan `SiteMapNode` s `Title`.

`AddNode(root)` yöntemi çağrısı, `SiteMapNode` `root` site eşlemesine kök olarak ekler. Sonra, `ProductsDataTable` her `ProductRow` numaralandırılır. Geçerli ürün kategorisi için zaten bir `SiteMapNode` varsa, buna başvurulur. Aksi takdirde, kategori için yeni bir `SiteMapNode` oluşturulur ve `AddNode(categoryNode, root)` yöntem çağrısıyla `SiteMapNode``root` alt öğesi olarak eklenir. Uygun kategori `SiteMapNode` düğüm bulduktan veya oluşturulduktan sonra, geçerli ürün için bir `SiteMapNode` oluşturulur ve `AddNode(productNode, categoryNode)`aracılığıyla kategori `SiteMapNode` alt öğesi olarak eklenir. `SiteMapNode` s `Url` Özellik değeri, ürün `SiteMapNode` s `Url` özelliği atandığında `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID` olduğunu unutmayın.`~/SiteMapNode/ProductDetails.aspx?ProductID=productID`

> [!NOTE]
> `CategoryID` için bir veritabanı `NULL` değeri olan ürünler, `Title` özelliği None olarak ayarlanmış ve `Url` özelliği boş bir dizeye ayarlanmış olan bir kategori `SiteMapNode` altında gruplandırılır. `ProductBLL` sınıf s `GetProductsByCategory(categoryID)` yöntemi şu anda yalnızca bir `NULL` `CategoryID` değeri olan ürünleri döndürme özelliği olmadığından, `Url` boş bir dizeye ayarlamaya karar verdim. Ayrıca, gezinti denetimlerinin, `Url` özelliği için bir değer olmayan bir `SiteMapNode` nasıl işlemesini göstermek istiyordum. Bu öğreticiyi genişletmenize, None `SiteMapNode` s `Url` özelliğinin `ProductsByCategory.aspx`işaret edebilmesi için, ancak yalnızca `NULL` `CategoryID` değerleri olan ürünleri görüntülerimize teşvik ediyorum.

Site Haritası oluşturulduktan sonra, `Categories` bir SQL önbellek bağımlılığı kullanılarak veri önbelleğine rastgele bir nesne eklenir ve bir `AggregateCacheDependency` nesnesi aracılığıyla tabloları `Products`. SQL önbellek *bağımlılıklarını kullanarak*önceki öğreticide SQL önbellek bağımlılıklarını araştırdık. Ancak, özel site haritası sağlayıcısı, henüz araştırdığımız veri önbelleği s `Insert` yönteminin bir aşırı yüklemesini kullanır. Bu aşırı yükleme, nesne önbellekten kaldırıldığında çağrılan bir temsilciyi son giriş parametresi olarak kabul eder. Özellikle, `NorthwindSiteMapProvider` sınıfında daha sonra tanımlanan `OnSiteMapChanged` yöntemine işaret eden yeni bir [`CacheItemRemovedCallback` temsilcisi](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx) geçiririz.

> [!NOTE]
> Site haritasının bellek içi temsili `root`sınıf düzeyi değişken aracılığıyla önbelleğe alınır. Özel site haritası sağlayıcısı sınıfının yalnızca bir örneği olduğundan ve bu örnek Web uygulamasındaki tüm iş parçacıkları arasında paylaşıldığından, bu sınıf değişkeni bir önbellek görevi görür. `BuildSiteMap` yöntemi veri önbelleğini de kullanır, ancak yalnızca `Categories` veya `Products` tablolarında temel alınan veritabanı verileri değiştiğinde bildirim alma anlamına gelir. Veri önbelleğine yerleştirdiğiniz değerin yalnızca geçerli tarih ve saat olduğunu unutmayın. Gerçek site haritası verileri veri önbelleğine *yerleştirmez* .

`BuildSiteMap` yöntemi, site haritasının kök düğümünü döndürerek tamamlanır.

Kalan Yöntemler oldukça basittir. `GetRootNodeCore` kök düğümü döndürmekten sorumludur. `BuildSiteMap` kök döndürdüğünden `GetRootNodeCore` yalnızca `BuildSiteMap` s dönüş değeri döndürür. `OnSiteMapChanged` yöntemi, önbellek öğesi kaldırıldığında `Nothing` geri `root` ayarlar. Kök `Nothing`, `BuildSiteMap` bir sonraki çağrılışında, site haritası yapısı yeniden oluşturulur. Son olarak, `CachedDate` özelliği, bu tür bir değer varsa veri önbelleğinde depolanan tarih ve saat değerini döndürür. Bu özellik, site haritası verilerinin son ne zaman önbelleğe alındığını öğrenmek için bir sayfa geliştiricisi tarafından kullanılabilir.

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>7\. Adım:`NorthwindSiteMapProvider` kaydetme

Web uygulamamız 6. adımda oluşturulan `NorthwindSiteMapProvider` site eşleme sağlayıcısını kullanmak için, bunu `Web.config``<siteMap>` bölümüne kaydetmemiz gerekir. Özel olarak, aşağıdaki biçimlendirmeyi `Web.config``<system.web>` öğesi içine ekleyin:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample7.xml)]

Bu biçimlendirme iki şeyi yapar: ilk olarak, yerleşik `AspNetXmlSiteMapProvider` varsayılan site eşleme sağlayıcısı olduğunu belirtir; İkincisi, adım 6 ' da oluşturulan özel site eşleme sağlayıcısını, çok daha fazla Northwind adıyla kaydeder.

> [!NOTE]
> Uygulama s `App_Code` klasöründe bulunan site haritası sağlayıcıları için, `type` özniteliğinin değeri yalnızca sınıf adıdır. Alternatif olarak, özel site eşleme sağlayıcısı derlenmiş bütünleştirilmiş kod ile Web uygulaması `/Bin` dizinine yerleştirilmiş ayrı bir sınıf kitaplığı projesinde oluşturulmuş olabilir. Bu durumda, `type` özniteliği değeri *ad alanı*olacaktır. *ClassName*, *AssemblyName* .

`Web.config`güncelleştirildikten sonra, bir tarayıcıda öğreticilerden herhangi bir sayfayı görüntülemek için bir dakikanızı ayırın. Soldaki gezinti arabiriminin hala `Web.sitemap`tanımlanan bölümleri ve öğreticileri gösterdiğini unutmayın. Bunun nedeni, varsayılan sağlayıcı olarak `AspNetXmlSiteMapProvider` soluyoruz. `NorthwindSiteMapProvider`kullanan bir gezinti kullanıcı arabirimi öğesi oluşturmak için, Northwind site haritası sağlayıcısının kullanılması gerektiğini açıkça belirtmemiz gerekir. Bunu adım 8 ' de nasıl gerçekleştireceğiz.

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>8\. Adım: özel site haritası sağlayıcısını kullanarak site haritası bilgilerini görüntüleme

`Web.config`, özel site eşleme sağlayıcısı oluşturulup kayıtlı `Default.aspx`, `ProductsByCategory.aspx`ve `ProductDetails.aspx` `SiteMapProvider` sayfalarına gezinti denetimleri eklemeye hazırız. `Default.aspx` sayfasını açıp araç kutusundan bir `SiteMapPath` sürükleyip tasarımcı üzerine sürükleyin. Bu denetim kutusu, araç kutusunun Gezinti bölümünde bulunur.

[![varsayılan. aspx 'e bir değer ekler](building-a-custom-database-driven-site-map-provider-vb/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image18.gif)

**Şekil 16**: `Default.aspx` Için bir fite ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image20.gif))

Bu denetim, site haritası içindeki geçerli sayfa konumunu gösteren bir içerik haritası görüntüler. Ana sayfa *ve site gezinti* öğreticisinde ana sayfanın en üstüne bir

Bu sayfayı bir tarayıcı aracılığıyla görüntülemek için bir dakikanızı ayırın. Şekil 16 ' da eklenen bu, varsayılan site haritası sağlayıcısını kullanır ve `Web.sitemap`verilerini çekmesini kullanır. Bu nedenle, içerik haritası, sağ üst köşedeki içerik haritasında olduğu gibi, site haritasını özelleştiren giriş &gt; gösterir.

[Içerik Haritası ![varsayılan site haritası sağlayıcısını kullanır](building-a-custom-database-driven-site-map-provider-vb/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.gif)

**Şekil 17**: Içerik Haritası varsayılan site haritası sağlayıcısını kullanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image23.gif))

Değer 1 ' in şekil 16 ' da eklenmesini sağlamak için, 6. adımda oluşturduğumuz özel site haritası sağlayıcısını kullanın, [`SiteMapProvider` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx) , `Web.config``NorthwindSiteMapProvider` atandığımız adı Northwind olarak ayarlayın. Ne yazık ki tasarımcı varsayılan site haritası sağlayıcısını kullanmaya devam eder, ancak bu özellik değişikliğini yaptıktan sonra sayfayı bir tarayıcı aracılığıyla ziyaret ederseniz, içerik haritası 'nın artık özel site haritası sağlayıcısını kullandığını görürsünüz.

[Içerik Haritası artık ![özel site haritası sağlayıcısını kullanıyor.](building-a-custom-database-driven-site-map-provider-vb/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image24.gif)

**Şekil 18**: Içerik Haritası artık özel site haritası sağlayıcısını kullanır `NorthwindSiteMapProvider` ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image26.gif))

Bu denetim `ProductsByCategory.aspx` ve `ProductDetails.aspx` sayfalarında daha işlevsel bir kullanıcı arabirimi görüntüler. Bu sayfalara bir, `SiteMapProvider` özelliğini Northwind olarak ayarlayarak bu sayfalara bir `Default.aspx`, Içecek için ürünleri görüntüle bağlantısına tıklayın ve ardından Chai Tea için Ayrıntıları görüntüle bağlantısını tıklatın. Şekil 19 ' u gösterdiği gibi, içerik haritası geçerli site haritası bölümünü (Chai Tea) ve bunların üst öğelerini içerir: Içecek ve tüm kategoriler.

[Içerik Haritası artık ![özel site haritası sağlayıcısını kullanıyor.](building-a-custom-database-driven-site-map-provider-vb/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.png)

**Şekil 19**: Içerik Haritası artık özel site haritası sağlayıcısını kullanır `NorthwindSiteMapProvider` ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image22.png))

Diğer gezinti kullanıcı arabirimi öğeleri, bu, menü ve TreeView denetimleri gibi, için de kullanılabilir. Bu öğreticide karşıdan yüklenebilecek `Default.aspx`, `ProductsByCategory.aspx`ve `ProductDetails.aspx` sayfaları (örneğin, tüm menü denetimleri dahil) (bkz. Şekil 20). ASP.NET 2,0 içindeki gezinti denetimleri ve site haritası sistemine daha ayrıntılı bir bakış için bkz. [ASP.NET 2,0 s site gezinti özelliklerini inceleme](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) ve [ASP.NET 2,0 quickbaşlangıçları](https://quickstarts.asp.net/QuickStartv20/aspnet/) 'Nın [site gezinti denetimlerini kullanma](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx) bölümü.

[Menü Denetim ![kategorilerin ve ürünlerin her birini listeler](building-a-custom-database-driven-site-map-provider-vb/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image28.gif)

**Şekil 20**: menü denetimi kategorilerin ve ürünlerin her birini listeler ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-a-custom-database-driven-site-map-provider-vb/_static/image30.gif))

Bu öğreticide daha önce bahsedildiği gibi, site haritası yapısına `SiteMap` sınıfı aracılığıyla programlı olarak erişilebilir. Aşağıdaki kod, Varsayılan sağlayıcının kök `SiteMapNode` döndürür:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample8.vb)]

`AspNetXmlSiteMapProvider`, uygulamamız için varsayılan sağlayıcıda olduğundan, yukarıdaki kod `Web.sitemap`tanımlanan kök düğümü döndürür. Varsayılan dışında bir site eşleme sağlayıcısına başvurmak için, şunun gibi `SiteMap` sınıf s [`Providers` özelliğini](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx) kullanın:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample9.vb)]

Burada *ad* , özel site haritası sağlayıcısının adıdır (web uygulamamız için Northwind).

Bir site haritası sağlayıcısına özgü bir üyeye erişmek için, sağlayıcı örneğini almak ve sonra uygun türe dönüştürmek için `SiteMap.Providers["name"]` kullanın. Örneğin, `NorthwindSiteMapProvider` s `CachedDate` özelliğini bir ASP.NET sayfasında göstermek için aşağıdaki kodu kullanın:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample10.vb)]

> [!NOTE]
> SQL önbellek bağımlılığı özelliğini test ettiğinizden emin olun. `Default.aspx`, `ProductsByCategory.aspx`ve `ProductDetails.aspx` sayfalarını ziyaret ettikten sonra düzenleme, ekleme ve silme bölümündeki öğreticilerden birine gidin ve bir kategorinin ya da ürünün adını düzenleyin. Sonra `SiteMapProvider` klasöründeki sayfalardan birine geri dönün. Yoklama mekanizmasına, temel alınan veritabanında yapılan değişikliği göz önünde bulunduracak kadar geçen sürenin geçtiğini varsayarsak, site haritasının yeni ürün veya kategori adını gösterecek şekilde güncellenmesi gerekir.

## <a name="summary"></a>Özet

ASP.NET 2,0 s site eşleme özellikleri, bir `SiteMap` sınıfı, yerleşik gezinti Web denetimleri ve bir XML dosyası için kalıcı site eşleme bilgilerini bekleyen bir varsayılan site haritası sağlayıcısı içerir. Site haritası bilgilerini bir veritabanı, uygulama mimarisi veya uzak Web hizmeti gibi başka bir kaynaktan kullanmak için özel bir site haritası sağlayıcısı oluşturulması gerekir. Bu, `SiteMapProvider` sınıfından doğrudan veya dolaylı olarak türetilen bir sınıf oluşturmayı içerir.

Bu öğreticide, ürün ve kategori bilgileri uygulama mimarisinden bağımsız olarak site haritasını temel alan özel bir site haritası sağlayıcısı oluşturmayı gördük. Sağlayıcımız `StaticSiteMapProvider` sınıfını genişletti ve verileri alan, site haritası hiyerarşisini oluşturan ve elde edilen yapıyı sınıf düzeyi bir değişkende önbelleğe alan bir `BuildSiteMap` yöntemi oluşturmayı planladı. Temel alınan `Categories` veya `Products` verileri değiştirildiğinde önbelleğe alınmış yapıyı geçersiz kılmak için bir geri çağırma işleviyle birlikte bir SQL önbellek bağımlılığı kullandık.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Site haritalarını SQL Server](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) ve [Istediğiniz SQL site eşleme sağlayıcısında](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) depolama
- [ASP.NET 2,0 s sağlayıcı modeline göz atın](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [Sağlayıcı araç seti](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [ASP.NET 2,0 s site gezinti özellikleri inceleniyor](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Gardner, Zack Jones, Teresa Murphy ve Bernadette Leigh. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Öncekini](building-a-custom-database-driven-site-map-provider-cs.md)
