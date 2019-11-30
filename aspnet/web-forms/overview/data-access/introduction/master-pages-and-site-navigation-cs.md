---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
title: Ana sayfalar ve site gezintisi (C#) | Microsoft Docs
author: rick-anderson
description: Kullanıcı dostu web sitelerinin yaygın bir özelliği, tutarlı, site genelinde sayfa düzeni ve gezinti şemasına sahip olmadıklarından oluşur. Bu öğretici, y...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 5aee8202-a4e3-4aa9-8a95-cd5d156cea4c
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
msc.type: authoredcontent
ms.openlocfilehash: e1ddd43524a61ff2e012171eba1a8dc8efbf8f1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587474"
---
# <a name="master-pages-and-site-navigation-c"></a>Ana Sayfalar ve Site Gezintisi (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_3_CS.exe) veya [PDF 'yi indirin](master-pages-and-site-navigation-cs/_static/datatutorial03cs1.pdf)

> Kullanıcı dostu web sitelerinin yaygın bir özelliği, tutarlı, site genelinde sayfa düzeni ve gezinti şemasına sahip olmadıklarından oluşur. Bu öğreticide, kolayca güncelleştirilebilen tüm sayfalarda tutarlı bir görünüm oluşturma konusu ele alınabilir.

## <a name="introduction"></a>Giriş

Kullanıcı dostu web sitelerinin yaygın bir özelliği, tutarlı, site genelinde sayfa düzeni ve gezinti şemasına sahip olmadıklarından oluşur. ASP.NET 2,0, hem site genelinde sayfa düzeni hem de gezinti şeması uygulamayı büyük ölçüde kolaylaştıran iki yeni özellik sunar: Ana sayfalar ve site gezintisi. Ana sayfalar, geliştiricilerin belirlenen düzenlenebilir bölgelerle site genelinde bir şablon oluşturmalarına olanak tanır. Bu şablon daha sonra sitedeki ASP.NET sayfalara uygulanabilir. Bu ASP.NET sayfaların yalnızca ana sayfanın belirtilen düzenlenebilir bölgeleri için içerik sağlaması gerekir ana sayfadaki diğer tüm biçimlendirmeler ana sayfayı kullanan tüm ASP.NET sayfalarında aynıdır. Bu model, geliştiricilerin site genelinde sayfa düzeni tanımlamasına ve merkezileştirmesine olanak tanır ve böylece kolayca güncelleştirilebilecek tüm sayfalarda tutarlı bir görünüm oluşturmayı kolaylaştırır.

[Site gezinti sistemi](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) , sayfa geliştiricileri için bir site haritası ve bu site haritası için program aracılığıyla SORGULANACAK bir API 'yi tanımlama mekanizması sağlar. Yeni gezinti Web denetimi, TreeView ve IBU menü, site haritasının tümünü veya bir kısmını ortak bir gezinti kullanıcı arabirimi öğesinde işlemeyi kolaylaştırır. Varsayılan site gezinti sağlayıcısını kullanacağız. Bu, site haritamız XML biçimli bir dosyada tanımlanacaktır.

Bu kavramları göstermek ve Öğreticiler Web sitemizi daha kullanışlı hale getirmek için, bu dersi site genelinde sayfa düzeni tanımlama, bir site haritası uygulama ve gezinti kullanıcı arabirimini ekleme gibi bir adım harcaalım. Bu öğreticinin sonuna kadar öğretici web sayfalarımızı oluşturmak için şık bir Web sitesi tasarlayacağız.

[Bu öğreticinin nihai sonucunu ![](master-pages-and-site-navigation-cs/_static/image2.png)](master-pages-and-site-navigation-cs/_static/image1.png)

**Şekil 1**: Bu öğreticinin nihai sonucu ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image3.png))

## <a name="step-1-creating-the-master-page"></a>1\. Adım: Ana sayfayı oluşturma

İlk adım, site için ana sayfayı oluşturmaktır. Şu anda web sitemizden yalnızca yazılan veri kümesi (`Northwind.xsd`, `App_Code` klasörü), BLL sınıfları (`ProductsBLL.cs`, `CategoriesBLL.cs`, vb.), veritabanı (`App_Code` klasöründe), yapılandırma dosyası (`NORTHWND.MDF`) ve bir CSS stil sayfası dosyası (`App_Data`) oluşur. Bu örnekleri gelecekteki öğreticilerde daha ayrıntılı bir şekilde incelenebilmemiz için ilk iki öğreticiden DAL ve BLL 'yi kullanarak bu sayfaları ve dosyaları temizlerdim.

![Projemizdeki dosyalar](master-pages-and-site-navigation-cs/_static/image4.png)

**Şekil 2**: projemizdeki dosyalar

Ana sayfa oluşturmak için Çözüm Gezgini proje adına sağ tıklayın ve yeni öğe Ekle ' yi seçin. Ardından, şablon listesinden ana sayfa türünü seçin ve `Site.master`adlandırın.

[Web sitesine yeni ana sayfa eklemek ![](master-pages-and-site-navigation-cs/_static/image6.png)](master-pages-and-site-navigation-cs/_static/image5.png)

**Şekil 3**: Web sitesine yeni bir ana sayfa ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image7.png))

Site genelinde sayfa mizanpajını ana sayfada tanımlayın. Tasarım görünümü kullanabilir ve gereken düzen veya Web denetimlerini ekleyebilir ya da biçimlendirmeyi el ile kaynak görünümüne ekleyebilirsiniz. Ana sayfamda, dış dosya `Style.css`tanımlı CSS ayarlarıyla konumlandırma ve stiller için [geçişli stil sayfaları](http://www.w3schools.com/css/default.asp) kullanıyorum. Aşağıda gösterilen biçimlendirmeden söylemeirken, CSS kuralları, gezinti `<div>`içeriğinin solunda görünecek şekilde mutlak olarak konumlandırılması ve 200 piksel sabit genişliğine sahip olması gibi tanımlanır.

Site. Master

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample1.aspx)]

Ana sayfa, hem statik sayfa mizanpajını hem de ana sayfayı kullanan ASP.NET sayfaları tarafından düzenlenebilecek bölgeleri tanımlar. Bu içerik düzenlenebilir bölgeler, içerik `<div>`içinde görünebilen ContentPlaceHolder denetimiyle belirtilir. Ana sayfamız tek bir ContentPlaceHolder (`MainContent`) içeriyor, ancak ana sayfanın birden çok Contentbir yer tutucu olabilir.

Yukarıda girilen biçimlendirme ile, Tasarım görünümü geçiş ana sayfanın yerleşimini gösterir. Bu ana sayfayı kullanan tüm ASP.NET sayfaları, `MainContent` bölgenin işaretlemesini belirtmek için bu Tekdüzen düzenine sahip olacaktır.

[Tasarım görünümü Ile görüntülenirken ana sayfayı ![](master-pages-and-site-navigation-cs/_static/image9.png)](master-pages-and-site-navigation-cs/_static/image8.png)

**Şekil 4**: Ana sayfa, Tasarım görünümü ile görüntülenirken ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image10.png))

## <a name="step-2-adding-a-homepage-to-the-website"></a>2\. Adım: Web sitesine bir giriş sayfası ekleme

Ana sayfa tanımlı olarak, Web sitesi için ASP.NET sayfalarını eklemeye hazırız. Şimdi Web sitesinin giriş sayfasına `Default.aspx`ekleyerek başlayalım. Çözüm Gezgini proje adına sağ tıklayın ve yeni öğe Ekle ' yi seçin. Şablon listesinden Web formu seçeneğini belirleyin ve dosyayı `Default.aspx`olarak adlandırın. Ayrıca "Ana sayfa seç" onay kutusunu işaretleyin.

[Yeni bir Web formu eklemek ![ana sayfa seç onay kutusunu Işaretleyerek](master-pages-and-site-navigation-cs/_static/image12.png)](master-pages-and-site-navigation-cs/_static/image11.png)

**Şekil 5**: yeni bir Web formu ekleme, ana sayfa seç onay kutusu ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-pages-and-site-navigation-cs/_static/image13.png))

Tamam düğmesine tıkladıktan sonra bu yeni ASP.NET sayfasının kullanması gereken ana sayfayı seçmeniz istenir. Projenizde birden çok ana sayfanız olabilir, ancak yalnızca bir tane var.

[![bu ASP.NET sayfasının kullanması gereken ana sayfayı seçin](master-pages-and-site-navigation-cs/_static/image15.png)](master-pages-and-site-navigation-cs/_static/image14.png)

**Şekil 6**: Bu ASP.net sayfasının kullanması gereken ana sayfayı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image16.png))

Ana sayfa seçildikten sonra, yeni ASP.NET sayfaları aşağıdaki biçimlendirmeyi içerir:

Default. aspx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample2.aspx)]

`@Page` yönergesinde, kullanılan ana sayfa dosyasına bir başvuru vardır (`MasterPageFile="~/Site.master"`) ve ASP.NET sayfası biçimlendirmesi, ana sayfada tanımlanan ContentPlaceHolder denetimlerinin her biri için bir Içerik denetimi içerir ve bu denetimin Içerik denetimini belirli bir ContentPlaceHolder ile eşlemesiyle `ContentPlaceHolderID`. Içerik denetimi, ilgili ContentPlaceHolder 'da görünmesini istediğiniz biçimlendirmeyi yerleştirdiğiniz yerdir. `@Page` yönergesinin `Title` özniteliğini Home olarak ayarlayın ve Içerik denetimine bir miktar kaynaklı içerik ekleyin:

Default. aspx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample3.aspx)]

`@Page` yönergesindeki `Title` özniteliği, `<title>` öğesi ana sayfada tanımlansa bile sayfanın başlığını ASP.NET sayfasından ayarlayamamızı sağlar. Ayrıca, `Page.Title`kullanarak başlığı programlı bir şekilde ayarlayabiliriz. Ayrıca, ana sayfanın stil sayfaları (örneğin, `Style.css`) başvuruları, ASP.NET sayfasının ana sayfaya göreli olduğu dizinden bağımsız olarak, herhangi bir ASP.NET sayfasında çalışacak şekilde otomatik olarak güncelleştirildiğini unutmayın.

Tasarım görünümü geçiş yaparken sayfamızın bir tarayıcıda nasıl görüneceğini görebiliriz. ASP.NET sayfası için Tasarım görünümü, yalnızca içerik düzenlenebilir bölgelerin düzenlenebilir olduğunu, ana sayfada tanımlanan ContentPlaceHolder olmayan biçimlendirmenin gri olduğunu unutmayın.

[ASP.NET sayfasına ilişkin tasarım görünümünde ![hem düzenlenebilir hem de Düzenlenemeyen bölgeler gösterilir](master-pages-and-site-navigation-cs/_static/image18.png)](master-pages-and-site-navigation-cs/_static/image17.png)

**Şekil 7**: ASP.NET sayfası Için tasarım görünümü hem düzenlenebilir hem de düzenlenemeyen bölgeleri gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image19.png))

`Default.aspx` sayfası bir tarayıcı tarafından ziyaret edildiğinde, ASP.NET altyapısı sayfanın ana sayfa içeriğini ve ASP 'yi otomatik olarak birleştirir. NET 'in içeriği ve birleştirilmiş içeriği, istenen tarayıcıya gönderilen son HTML ile işler. Ana sayfanın içeriği güncelleştirilirken, bu ana sayfayı kullanan tüm ASP.NET sayfalarının içeriği bir sonraki istendiklerinde yeni ana sayfa içeriğiyle yeniden birleştirilmesi gerekir. Kısacası, ana sayfa modeli, değişiklikleri tüm sitede hemen yansıtılan tek sayfalı bir düzen şablonunun (Ana sayfa) tanımlanmasını sağlar.

## <a name="adding-additional-aspnet-pages-to-the-website"></a>Web sitesine ek ASP.NET sayfaları ekleme

Daha kısa bir süre içinde, siteye en sonunda çeşitli raporlama tanıtımları tutacak ek ASP.NET sayfa saplamalarının eklenmesi biraz zaman atalım. Toplam olarak 35 ' den fazla tanıtım olacaktır, bu nedenle tüm saplama sayfalarını oluşturmak yerine yalnızca ilk birkaç şey oluşturalım. Birçok tanıtımlar kategorisi de olacağı için gösterileri daha iyi yönetmek için kategoriler için bir klasör ekleyin. Şimdilik aşağıdaki üç klasörü ekleyin:

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

Son olarak, Şekil 8 ' de Çözüm Gezgini gösterildiği gibi yeni dosyalar ekleyin. Her dosya eklenirken "Ana sayfa seç" onay kutusunu işaretleyin.

![Aşağıdaki dosyaları ekleyin](master-pages-and-site-navigation-cs/_static/image20.png)

**Şekil 8**: aşağıdaki dosyaları ekleyin

## <a name="step-2-creating-a-site-map"></a>2\. Adım: site haritası oluşturma

Birden çok sayfadan oluşan bir Web sitesini yönetme sorunlarından biri, ziyaretçilerin sitede gezinme konusunda basit bir yol sağlamaktır. İle başlamak için sitenin gezinti yapısı tanımlanmalıdır. Daha sonra, bu yapının menüler veya içerik haritaları gibi gezinilebilir Kullanıcı Arabirimi öğelerine çevrilmesi gerekir. Son olarak, siteye yeni sayfa eklendikçe ve kaldırıldıkça bu bütün işlemin tutulması ve güncelleştirilmesi gerekir. ASP.NET 2,0 ' den önce, geliştiriciler sitenin gezinti yapısını oluşturmak, sürdürmek ve gezilebilir Kullanıcı Arabirimi öğelerine çevirmek için kendi kendilerine aittir. Ancak, ASP.NET 2,0 ile, geliştiriciler çok esnek yerleşik site gezinti sistemini kullanabilir.

ASP.NET 2,0 site gezinti sistemi, bir geliştiricinin bir site haritası tanımlamasına ve sonra bu bilgilere programlı bir API aracılığıyla erişmelerine yönelik bir yol sağlar. ASP.NET, site haritası verilerinin belirli bir şekilde biçimlendirilen bir XML dosyasında depolanmasını bekleyen bir site haritası sağlayıcısıyla birlikte gelir. Ancak, site gezinti sistemi [sağlayıcı modelinde](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) oluşturulduğundan, site haritası bilgilerini serileştirmek için alternatif yolları desteklemek üzere genişletilebilir. Jeff Prosise 'ın makalesi, [BEKLEDIĞINIZ SQL site eşleme sağlayıcısı](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx) , site haritasını bir SQL Server veritabanında depolayan bir site haritası sağlayıcısı oluşturmayı gösterir; başka bir seçenek de [dosya sistemi yapısına dayalı bir site haritası sağlayıcısı](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)oluşturmaktır.

Bununla birlikte, bu öğretici için ASP.NET 2,0 ile birlikte gelen varsayılan site haritası sağlayıcısını kullanalım. Site haritasını oluşturmak için Çözüm Gezgini proje adına sağ tıklayın, yeni öğe Ekle ' yi seçin ve site haritası seçeneğini belirleyin. Adı `Web.sitemap` olarak bırakın ve Ekle düğmesine tıklayın.

[![projenize bir site haritası ekleyin](master-pages-and-site-navigation-cs/_static/image22.png)](master-pages-and-site-navigation-cs/_static/image21.png)

**Şekil 9**: projenize bir site haritası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image23.png))

Site eşleme dosyası bir XML dosyasıdır. Visual Studio 'Nun site haritası yapısı için IntelliSense 'i sağladığını unutmayın. Site Haritası dosyası, tam olarak bir `<siteMapNode>` alt öğesi içermesi gereken kök düğümü olarak `<siteMap>` düğümüne sahip olmalıdır. Bu ilk `<siteMapNode>` öğesi, daha sonra rastgele sayıda alt öğe `<siteMapNode>` öğesi içerebilir.

Dosya sistemi yapısını taklit etmek için site haritasını tanımlayın. Diğer bir deyişle, üç klasörün her biri için bir `<siteMapNode>` öğesi ve bu klasörlerdeki her bir ASP.NET sayfası için alt `<siteMapNode>` öğeleri ekleyin, örneğin:

Web. sitemap

[!code-xml[Main](master-pages-and-site-navigation-cs/samples/sample4.xml)]

Site Haritası, sitenin çeşitli bölümlerini açıklayan bir hiyerarşi olan Web sitesinin gezinme yapısını tanımlar. `Web.sitemap` her `<siteMapNode>` öğesi, sitenin gezinti yapısındaki bir bölümü temsil eder.

[Site Haritası hiyerarşik bir gezinti yapısını temsil ![](master-pages-and-site-navigation-cs/_static/image25.png)](master-pages-and-site-navigation-cs/_static/image24.png)

**Şekil 10**: site haritası hiyerarşik bir gezinti yapısını temsil eder ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image26.png))

ASP.NET, .NET Framework [SiteMap sınıfı](https://msdn.microsoft.com/library/system.web.sitemap.aspx)aracılığıyla site haritasının yapısını gösterir. Bu sınıf, kullanıcının şu anda ziyaret ettiği bölüm hakkında bilgi döndüren bir `CurrentNode` özelliğine sahiptir; `RootNode` özelliği, site haritasının kökünü döndürür (ana, site haritamızda). Hem `CurrentNode` hem de `RootNode` özellikleri, site haritası hiyerarşisinin eklenmesine izin veren `ParentNode`, `ChildNodes`, `NextSibling`, `PreviousSibling`, vb. gibi özelliklere sahip [SiteMapNode](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) örnekleri döndürür.

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>3\. Adım: site haritasını temel alan bir menü görüntüleme

ASP.NET 2,0 ' deki verilere erişim, yeni [veri kaynağı denetimleri](https://msdn.microsoft.com/library/ms227679.aspx)aracılığıyla ASP.NET 1. x veya bildirimli olarak, programlı bir şekilde gerçekleştirilebilir. İlişkisel veritabanı verilerine erişim, ObjectDataSource denetimi, sınıflardan verilere erişim için ve diğer bir deyişle, SqlDataSource denetimi gibi çeşitli yerleşik veri kaynağı denetimleri vardır. Kendi [özel veri kaynağı denetimlerinizi](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/dnvs05/html/DataSourceCon1.asp)bile oluşturabilirsiniz.

Veri kaynağı denetimleri, ASP.NET sayfanız ile temel alınan veriler arasında bir ara sunucu olarak görev yapar. Veri kaynağı denetiminin alınan verilerini göstermek için, sayfada genellikle başka bir Web denetimi ekleyecek ve bunu veri kaynağı denetimine bağlayacağız. Bir Web denetimini bir veri kaynağı denetimine bağlamak için, Web denetiminin `DataSourceID` özelliğini veri kaynağı denetiminin `ID` özelliğinin değerine ayarlamanız yeterlidir.

ASP.NET, site haritasının verileriyle çalışmaya yardımcı olmak için, Web sitesinin site haritasında bir Web denetimi bağlamamızı sağlayan SiteMapDataSource denetimini içerir. İki Web denetimi, ağaç ve menü genellikle bir gezinti kullanıcı arabirimi sağlamak için kullanılır. Site Haritası verilerini bu iki denetimden birine bağlamak için, `DataSourceID` özelliği uygun şekilde ayarlanmış bir TreeView veya menü denetimiyle birlikte sayfaya bir SiteMapDataSource eklemeniz yeterlidir. Örneğin, ana sayfaya aşağıdaki biçimlendirmeyi kullanarak bir menü denetimi ekleyebiliriz:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample5.aspx)]

Yayınlanan HTML üzerinde daha ayrıntılı bir denetim için, SiteMapDataSource denetimini Yineleyici denetimine bağlayabiliriz, örneğin şöyle olabilir:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample6.aspx)]

SiteMapDataSource denetimi, site haritası hiyerarşisini tek seferde, kök site haritası düğümünden (ana, site haritamızda), ardından bir sonraki düzeye (temel raporlama, filtreleme raporları ve özelleştirilmiş biçimlendirme) başlayarak bir düzey döndürür. SiteMapDataSource, bir yineleyici öğesine bağlanırken döndürülen ilk düzeyi numaralandırır ve bu ilk düzeydeki her bir `SiteMapNode` örneği için `ItemTemplate` başlatır. `SiteMapNode`belirli bir özelliğine erişmek için, her bir `SiteMapNode``Url` ve `Title` özelliklerini köprü denetimi için alma biçimimiz olan `Eval(propertyName)`kullanabiliriz.

Yukarıdaki Yineleyici örnek aşağıdaki biçimlendirmeyi işleyecek:

[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample7.html)]

Bu site haritası düğümleri (temel raporlama, filtreleme raporları ve özelleştirilmiş biçimlendirme), ilk olarak değil, işlenen site eşlemesinin *ikinci* düzeyini oluşturur. Bunun nedeni, SiteMapDataSource 'un `ShowStartingNode` özelliğinin false olarak ayarlanması, SiteMapDataSource 'un kök site haritası düğümünü atlaması ve bunun yerine site haritası hiyerarşisinde ikinci düzeyi döndürmesinin başlamasını sağlar.

Temel raporlama, filtreleme raporları ve özelleştirilmiş biçimlendirme `SiteMapNode` s için alt öğeleri göstermek üzere ilk yineleyicisi 'nin `ItemTemplate`başka bir yineleyici ekleyebiliriz. Bu ikinci Yineleyici, `SiteMapNode` örneğinin `ChildNodes` özelliğine bağlanacak, şöyle olacaktır:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample8.aspx)]

Bu iki repeaters, aşağıdaki İşaretlemede sonuç (kısaltma için bazı biçimlendirmeler kaldırılmıştır):

[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample9.html)]

The [Kchel Andrew](http://www.rachelandrew.co.uk/)'ıN, [CSS antholoju tarafından seçilen CSS stillerinin kullanılması: 101 önemli Ipuçları, püf noktaları, &amp; hacimler](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance), `<ul>` ve `<li>` öğeleri, biçimlendirme aşağıdaki görsel çıktıyı üreten şekilde stillendirilemedir:

![Iki repeaters ve bazı CSS 'lerden oluşan bir menü](master-pages-and-site-navigation-cs/_static/image27.png)

**Şekil 11**: iki repeaters ve bazı CSS 'lerden oluşan bir menü

Bu menü, ana sayfada ve `Web.sitemap`tanımlanan site haritasına bağlı olarak, site haritasında yapılan herhangi bir değişiklik, `Site.master` ana sayfasını kullanan tüm sayfalarda hemen yansıtılacaktır.

## <a name="disabling-viewstate"></a>ViewState devre dışı bırakılıyor

Tüm ASP.NET denetimleri isteğe bağlı olarak, işlenmiş HTML 'de gizli form alanı olarak serileştirilmiş olan [görünüm durumuna](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/)kalıcı olarak devam edebilir. Görünüm durumu, denetimler tarafından, bir veri Web denetimine yönelik veriler gibi geri göndermeler genelinde program aracılığıyla değiştirilen durumlarını anımsamak için kullanılır. Görünüm durumu bilgilerin geri göndermeler arasında hatırlanmasına izin verdiğinden, bu, istemciye gönderilmesi gereken biçimlendirmenin boyutunu artırır ve yakından izlenmezse önemli sayfa blobuna yol açabilir. Veri Web denetimleri özellikle GridView, bir sayfaya onlarca fazladan kilobayt kadar biçimlendirme eklemek için özellikle ntoriou 'lar. Bu tür bir artış geniş bant veya intranet kullanıcıları için göz ardı edilebilir olsa da, Görünüm durumu çevirmeli kullanıcılara gidiş dönüş için birkaç saniye ekleyebilir.

Görünüm durumunun etkisini görmek için, tarayıcıda bir sayfayı ziyaret edin ve Web sayfası tarafından gönderilen kaynağı görüntüleyin (Internet Explorer 'da Görünüm menüsüne gidin ve kaynak seçeneğini belirleyin). Sayfadaki denetimlerin her biri tarafından kullanılan görünüm durumu ayırmayı görmek için [Sayfa izlemeyi](https://msdn.microsoft.com/library/sfbfw58f.aspx) da açabilirsiniz. Görünüm durumu bilgileri, açma `<form>` etiketinden hemen sonra `<div>` öğesinde bulunan `__VIEWSTATE`adlı gizli bir form alanında serileştirilir. Görünüm durumu yalnızca kullanılmakta olan bir Web formu olduğunda kalıcıdır; ASP.NET sayfanız bildirime dayalı sözdiziminde bir `<form runat="server">` içermiyorsa, işlenmiş İşaretlemede `__VIEWSTATE` gizli form alanı olmayacaktır.

Ana sayfa tarafından oluşturulan `__VIEWSTATE` form alanı, sayfanın oluşturulan biçimlendirmesine kabaca 1.800 bayt ekler. Bu ek blobunun nedeni, SiteMapDataSource denetiminin içerikleri görünüm durumu ' nu kalıcı olduğundan birincil olarak Yineleyici denetimine yöneliktir. Çok sayıda alan ve kayıt içeren bir GridView kullanırken, ek 1.800 baytları heyecanlanabilecek kadar çok görünmeyebilir, Görünüm durumu 10 veya daha fazla bir faktörle kolayca görünebilir.

Görünüm durumu, `EnableViewState` özelliği `false`olarak ayarlanarak, sayfa veya Denetim düzeyinde devre dışı bırakılabilir ve böylece işlenmiş biçimlendirmenin boyutu azalır. Bir veri Web denetiminin görünüm durumu, geri göndermeler genelinde veri Web denetimine bağlı verilerin devam ettiğinden, bir veri Web denetimi için görünüm durumunu devre dışı bırakırken verilerin her geri göndermede ve her geri göndermede bağlı olması gerekir. ASP.NET sürüm 1. x ' de, bu sorumluluk sayfa geliştiricisi Shoulders üzerinde. Ancak, ASP.NET 2,0 ile veri Web denetimleri, gerektiğinde her geri göndermede veri kaynağı denetimlerine yeniden bağlanmaya çalışır.

Sayfanın görünüm durumunu azaltmak için, yineleyici denetiminin `EnableViewState` özelliğini `false`olarak ayarlayalim. Bu, tasarımcıda Özellikler penceresi veya kaynak görünümünde bildirimli olarak yapılabilir. Bu değişikliği yaptıktan sonra, yineleyicisi 'nin bildirim temelli işaretleme şöyle görünmelidir:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample10.aspx)]

Bu değişiklikten sonra, sayfanın işlenmiş görünüm durumu boyutu bir boyutundaydı 52 bayta küçültülebilir, bu da görünüm durumu boyutunda %97 tasarruf sağlar! Bu dizideki öğreticilerde, oluşturulan biçimlendirmenin boyutunu azaltmak için varsayılan olarak veri Web denetimlerinin görünüm durumunu devre dışı bırakacağız. Örneklerin çoğunluğunda `EnableViewState` özelliği `false` olarak ayarlanacak ve bunu bahsetmeden yapmış olacak. Tek zaman görünümü durumu, veri Web denetimi 'nin beklenen işlevselliğini sağlaması için etkin olması gereken senaryolarda ele alınacaktır.

## <a name="step-4-adding-breadcrumb-navigation"></a>4\. Adım: Içerik Haritası gezintisi ekleme

Ana sayfayı tamamlayabilmeniz için her sayfaya bir içerik haritası gezintisi kullanıcı arabirimi öğesi ekleyelim. İçerik haritası, kullanıcıları site hiyerarşisi içindeki geçerli konumlarını hızlı bir şekilde gösterir. ASP.NET 2,0 ' de bir içerik haritası eklemenin kolay bir şekilde sayfaya bir e-bir denetim eklemesi yeterlidir; kod gerekmez.

Sitemiz için bu denetimi üstbilgiye `<div>`ekleyin:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample11.aspx)]

İçerik haritası, kullanıcının site haritası hiyerarşisinde ziyaret ettiği geçerli sayfayı ve bu site eşleme düğümünün "üst öğeleri", köke (sitem haritamızda ana) kadar tüm şekilde olduğunu gösterir.

![Içerik Haritası, geçerli sayfayı ve onun üst öğelerini site haritası hiyerarşisinde görüntüler](master-pages-and-site-navigation-cs/_static/image28.png)

**Şekil 12**: içerik haritası, geçerli sayfayı ve onun üst öğelerini site haritası hiyerarşisinde görüntüler

## <a name="step-5-adding-the-default-page-for-each-section"></a>5\. Adım: her bölüm için varsayılan sayfayı ekleme

Sitemizdeki öğreticiler, her kategori için bir klasör ve bu klasördeki ASP.NET sayfaları gibi ilgili öğreticiler için temel raporlama, filtreleme, özel biçimlendirme gibi farklı kategorilere ayrılmıştır. Ayrıca, her klasör bir `Default.aspx` sayfası içerir. Bu varsayılan sayfa için geçerli bölüm için tüm öğreticilerin görüntülenmesini görelim. Diğer bir deyişle, `BasicReporting` klasöründeki `Default.aspx` için `SimpleDisplay.aspx`, `DeclarativeParams.aspx`ve `ProgrammaticParams.aspx`bağlantıları vardır. Burada, `SiteMap` sınıfını ve bir veri Web denetimini kullanarak bu bilgileri `Web.sitemap`tanımlanan site haritasına göre görüntüleyebilirsiniz.

Yineleyicisi 'ni tekrar kullanarak sıralanmamış bir liste gösterelim, ancak bu kez öğreticilerin başlığını ve açıklamasını görüntüleyeceğiz. Bunu gerçekleştirmeye yönelik biçimlendirme ve kodun her bir `Default.aspx` sayfası için yinelenmesi gerektiğinden, bu UI mantığını bir [Kullanıcı denetiminde](https://msdn.microsoft.com/library/y6wb1a0e.aspx)kapsülleyebilirsiniz. `UserControls` adlı Web sitesinde bir klasör oluşturun ve `SectionLevelTutorialListing.ascx`adlı Web Kullanıcı denetimi türünde yeni bir öğeye ekleyin ve aşağıdaki biçimlendirmeyi ekleyin:

[![UserControls klasörüne yeni bir Web Kullanıcı denetimi Ekle](master-pages-and-site-navigation-cs/_static/image30.png)](master-pages-and-site-navigation-cs/_static/image29.png)

**Şekil 13**: `UserControls` klasöre yeni bir Web Kullanıcı denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image31.png))

SectionLevelTutorialListing. ascx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.cs

[!code-csharp[Main](master-pages-and-site-navigation-cs/samples/sample13.cs)]

Önceki Yineleyici örneğinde, `SiteMap` verilerini yineleyicisi 'ne bildirimli olarak bağladık; Ancak `SectionLevelTutorialListing` Kullanıcı denetimi, programlı olarak bunu yapar. `Page_Load` olay işleyicisinde, bu sayfanın URL 'sinin site eşlemesindeki bir düğüme eşlendiğinden emin olmak için bir denetim yapılır. Bu Kullanıcı denetimi karşılık gelen bir `<siteMapNode>` girişi olmayan bir sayfada kullanılıyorsa, `SiteMap.CurrentNode` `null` döndürür ve hiçbir veri yineleyicisi 'ne bağlanmayacak. `CurrentNode`olduğunu varsayarsak, `ChildNodes` koleksiyonunu Repeater 'a bağladık. Site Haritamız, her bölümdeki `Default.aspx` sayfası bu bölümdeki tüm öğreticilerin üst düğümüdür, bu kod, aşağıdaki ekran görüntüsünde gösterildiği gibi tüm bölüm öğreticilerinin bağlantılarını ve açıklamalarını görüntüler.

Bu Yineleyici oluşturulduktan sonra, her bir klasördeki `Default.aspx` sayfaları açın, Tasarım görünümü gidin ve Çözüm Gezgini Kullanıcı denetimini, öğretici listesinin görüntülenmesini istediğiniz tasarım yüzeyine sürüklemeniz yeterlidir.

[Kullanıcı denetimi varsayılan. aspx 'e eklenmiştir ![](master-pages-and-site-navigation-cs/_static/image33.png)](master-pages-and-site-navigation-cs/_static/image32.png)

**Şekil 14**: kullanıcı denetimi `Default.aspx` eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image34.png))

[Temel raporlama öğreticilerinin ![listeleniyor](master-pages-and-site-navigation-cs/_static/image36.png)](master-pages-and-site-navigation-cs/_static/image35.png)

**Şekil 15**: temel raporlama öğreticileri listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-site-navigation-cs/_static/image37.png))

## <a name="summary"></a>Özet

Site Haritası tanımlı ve ana sayfa tamamlandığına göre artık, verilerle ilgili öğreticilerimiz için tutarlı bir sayfa düzeni ve gezinti düzeni sunuyoruz. Sitemizi eklediğimiz sayfa sayısına bakılmaksızın, site genelinde sayfa düzeni veya site gezinti bilgilerini güncelleştirmek, bu bilgiler merkezi hale gelmiş olduğundan hızlı ve basit bir işlemdir. Özellikle, sayfa düzeni bilgileri Ana sayfa `Site.master` ve `Web.sitemap`site haritasında tanımlanmıştır. Bu site genelinde sayfa düzenine ve gezinti mekanizmasına ulaşmak için *herhangi bir* kod yazmak zorunda kalmadık ve Visual Studio 'DA Tam WYSIWYG Designer desteğini koruduk.

Veri erişimi katmanını ve Iş mantığı katmanını tamamladığınıza göre, tutarlı bir sayfa düzeni ve site gezintisi tanımlanmış, ortak raporlama desenlerini keşfetmeye başlamaya hazırız. [Sonraki](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) üç öğreticilerde, GridView, DetailsView ve FormView denetimlerinde BLL 'lerden alınan verileri görüntüleyen temel raporlama görevlerine bakacağız.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET ana sayfalarına genel bakış](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [ASP.NET 2,0 'de ana sayfalar](http://odetocode.com/Articles/419.aspx)
- [ASP.NET 2,0 tasarım şablonları](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [ASP.NET site gezintisine genel bakış](https://msdn.microsoft.com/library/e468hxky.aspx)
- [ASP.NET 2.0 'ın site gezintisi inceleniyor](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [ASP.NET 2,0 site gezinti özellikleri](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [ASP.NET görünüm durumunu anlama](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/viewstate.asp)
- [Nasıl yapılır: ASP.NET sayfası için Izlemeyi etkinleştirme](https://msdn.microsoft.com/library/94c55d08%28VS.80%29.aspx)
- [ASP.NET Kullanıcı denetimleri](https://msdn.microsoft.com/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Liz Shulok, dennıs Patterson ve Tepton Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](creating-a-business-logic-layer-cs.md)
> [İleri](creating-a-data-access-layer-vb.md)
