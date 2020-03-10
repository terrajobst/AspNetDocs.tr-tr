---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
title: Ana sayfalar ve ASP.NET AJAX (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET AJAX ve ana sayfaları kullanma seçeneklerini açıklar. ScriptManagerProxy sınıfını kullanmaya bakar; farklı JS dosyalarının nasıl yüklendiğini açıklar...
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 0c55eb66-ba44-4d49-98e8-5c87fd9b1111
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
msc.type: authoredcontent
ms.openlocfilehash: 8cd1d57b4d2aa01654da53ab2b1cc01f71ad8a87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629166"
---
# <a name="master-pages-and-aspnet-ajax-c"></a>Ana Sayfalar ve ASP.NET AJAX (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_CS.pdf)

> ASP.NET AJAX ve ana sayfaları kullanma seçeneklerini açıklar. ScriptManagerProxy sınıfını kullanmaya bakar; ScriptManager 'ın ana sayfa veya Içerik sayfasında kullanılıp kullanılmadığını bağlı olarak çeşitli JS dosyalarının nasıl yüklendiğini açıklar.

## <a name="introduction"></a>Giriş

Son birkaç yılda daha fazla geliştirici, [Ajax](http://en.wikipedia.org/wiki/Ajax_(programming))özellikli Web uygulamaları oluşturuyor. AJAX özellikli bir Web sitesi, daha hızlı bir kullanıcı deneyimi sunmak için bir dizi ilgili Web teknolojisini kullanır. Microsoft 'un [ASP.NET AJAX çerçevesi](../../../../ajax/index.md)sayesınde, AJAX etkin ASP.NET uygulamaları oluşturma işlemi çok kolay başaramayabiliriz. ASP.NET AJAX, ASP.NET 3,5 ve Visual Studio 2008 ' de yerleşiktir; Ayrıca, ASP.NET 2,0 uygulamaları için ayrı bir indirme olarak da kullanılabilir.

ASP.NET AJAX çerçevesiyle AJAX özellikli Web sayfaları oluştururken, çerçeveyi kullanan her sayfaya ve tam olarak bir [ScriptManager denetimi](https://msdn.microsoft.com/library/bb398863.aspx) eklemeniz gerekir. Adından da anlaşılacağı gibi, ScriptManager, AJAX etkin Web sayfalarında kullanılan istemci tarafı betiğini yönetir. ScriptManager, en azından, tarayıcıya ASP.NET AJAX Istemci kitaplığını oluşturan JavaScript dosyalarını indirmesini sağlayan HTML 'yi yayar. Özel JavaScript dosyaları, komut dosyası etkin Web Hizmetleri ve özel uygulama hizmeti işlevlerini kaydetmek için de kullanılabilir.

Siteniz ana sayfaları kullanıyorsa (olduğu gibi), her bir tek içerik sayfasına bir ScriptManager denetimi eklemeniz gerekmez; Bunun yerine, ana sayfaya bir ScriptManager denetimi ekleyebilirsiniz. Bu öğretici, ScriptManager denetiminin ana sayfaya nasıl ekleneceğini gösterir. Ayrıca, belirli bir içerik sayfasında özel komut dosyaları ve betik Hizmetleri kaydetmek için ScriptManagerProxy denetimini nasıl kullanacağınızı da arar.

> [!NOTE]
> Bu öğretici, ASP.NET AJAX çerçevesiyle AJAX özellikli Web uygulamaları tasarlamayı veya oluşturmayı araştırmaz. AJAX kullanımı hakkında daha fazla bilgi için, Bu öğreticinin sonundaki [ASP.NET AJAX videoları](../../../videos/aspnet-ajax/index.md) ve [öğreticilerine](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)ve daha fazla okuma bölümünde listelenen kaynaklara bakın.

## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>ScriptManager denetimi tarafından yayılan biçimlendirmeyi İnceleme

ScriptManager denetimi, tarayıcıya ASP.NET AJAX Istemci kitaplığını oluşturan JavaScript dosyalarını indirmesini sağlayan biçimlendirmeyi yayar. Ayrıca, bu kitaplığı Başlatan sayfaya satır içi JavaScript bir bit ekler. Aşağıdaki biçimlendirmede, ScriptManager denetimi içeren bir sayfanın işlenmiş çıktısına eklenen içerik gösterilmektedir:

[!code-html[Main](master-pages-and-asp-net-ajax-cs/samples/sample1.html)]

`<script src="url"></script>` Etiketler, tarayıcıya JavaScript dosyasını *URL*'de indirip yürütmeye yönlendirir. ScriptManager üç tür etiket yayar; tek bir dosyaya başvuru `WebResource.axd`, diğeri dosyanın `ScriptResource.axd`başvurudur. Bu dosyalar aslında web sitenizde dosya olarak mevcut değildir. Bunun yerine, bu dosyalardan birine yönelik bir istek Web sunucusuna ulaştığında, ASP.NET altyapısı QueryString 'i inceler ve uygun JavaScript içeriğini döndürür. Bu üç dış JavaScript dosyası tarafından sunulan betik, ASP.NET AJAX Framework 'ün Istemci kitaplığını oluşturur. ScriptManager tarafından yayılan diğer `<script>` etiketleri, bu kitaplığı Başlatan satır içi betik içerir.

ScriptManager tarafından yayılan dış betik başvuruları ve satır içi betik, ASP.NET AJAX çerçevesini kullanan bir sayfa için gereklidir, ancak Framework kullanmayan sayfalar için gerekli değildir. Bu nedenle, ASP.NET AJAX çerçevesini kullanan sayfalara yalnızca bir ScriptManager eklemek için ideal olmasının bir nedeni olabilir. Bu da yeterlidir, ancak çerçeveyi kullanan çok sayıda sayfanız varsa, en az bir tane olmak üzere tüm sayfalara ScriptManager denetimini (yinelenen bir görev) ekleyebilirsiniz. Alternatif olarak, ana sayfaya bir ScriptManager ekleyebilirsiniz ve bu gerekli betiği tüm içerik sayfalarına çıkartır. Bu yaklaşımda, zaten ana sayfa tarafından eklendiğinden, ASP.NET AJAX çerçevesini kullanan yeni bir sayfaya bir ScriptManager eklemek zorunda değilsiniz. 1\. adım, ana sayfaya bir ScriptManager ekleme konusunda adım adım yol gösterir.

> [!NOTE]
> Ana sayfanızın kullanıcı arabirimi içinde AJAX işlevselliği eklemeyi planlıyorsanız, ana sayfada ScriptManager ' ı dahil etmeniz gerekir.

ScriptManager 'ın ana sayfaya eklenmesinin bir alt tarafı, gerekli olup olmadığına bakılmaksızın yukarıdaki betiğin *her* sayfada yayılmalarından biridir. Bu, ScriptManager 'ın dahil olduğu sayfalar (Ana sayfa aracılığıyla) için henüz ASP.NET AJAX çerçevesinin herhangi bir özelliğini kullanmayın. Ancak ne kadar bant genişliği harcandınız?

- ScriptManager tarafından yayılan gerçek içerik (yukarıda gösterilen) 1 KB 'tan fazla.
- Ancak `<script>` öğesi tarafından başvurulan üç harici betik dosyası, sıkıştırılmamış yaklaşık 450KB veri içerir; gzip sıkıştırması kullanan bir Web sitesinde, bu toplam bant genişliği 100 KB 'ın yakınında azaltılabilir. Ancak, bu komut dosyaları bir yılda tarayıcı tarafından önbelleğe alınır, yani yalnızca bir kez indirilmeleri ve sonra sitedeki diğer sayfalarda yeniden kullanılabilir.

En iyi durumda, betik dosyaları önbelleğe alındığında toplam maliyet 1 KB 'tır ve bu da yok edilebilir. Ancak, betik dosyaları henüz indirilmedi ve Web sunucusu herhangi bir sıkıştırma biçimini kullanmadıysa, en kötü durumda, bant genişliği isabetinin 450KB 'den büyük olması ve bir geniş bant bağlantısı üzerinden bir saniyeden  Çevirmeli modemler üzerinde kullanıcılar. Her ne kadar iyi haber, dış betik dosyaları tarayıcı tarafından önbelleğe alındığından, bu en kötü durum senaryosu nadiren meydana gelir.

> [!NOTE]
> ScriptManager denetimini ana sayfaya yerleştirmeye devam ediyorsanız, Web formunu (ana sayfada `<form runat="server">` biçimlendirme) göz önünde bulundurun. Geri gönderme modelini kullanan her ASP.NET sayfası, tam olarak bir Web formu içermelidir. Web formu eklemek ek içerik ekler: bir dizi gizli form alanı, `<form>` etiketinin kendisi ve gerekirse, betikten geri gönderme başlatmak için bir JavaScript işlevi. Bu biçimlendirme geri gönderme olmayan sayfalar için gereksizdir. Bu yabancı biçimlendirme, Web formunu ana sayfadan kaldırarak ve bir tane olması gereken her bir içerik sayfasına el ile ekleyerek ortadan kaldırılabilir. Ancak, ana sayfada Web formunu kullanmanın avantajları, belirli içerik sayfalarına gereksiz yere eklenmesinin olumsuz yönlerini ortadan

## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>1\. Adım: Ana sayfaya ScriptManager denetimi ekleme

ASP.NET AJAX çerçevesini kullanan her Web sayfasında tam olarak bir ScriptManager denetimi bulunmalıdır. Bu gereksinim nedeniyle, genellikle tüm içerik sayfalarında ScriptManager denetimi otomatik olarak dahil olmak üzere ana sayfaya tek bir ScriptManager denetimi yerleştirmek mantıklı olur. Ayrıca, ScriptManager, UpdatePanel ve UpdateProgress denetimleri gibi ASP.NET AJAX sunucu denetimlerinden önce gelmelidir. Bu nedenle, ScriptManager 'ı Web formu içindeki herhangi bir ContentPlaceHolder denetimine koymak en iyisidir.

`Site.master` ana sayfasını açın ve Web formu içindeki sayfaya, ancak `<div id="topContent">` öğesinden önce bir ScriptManager denetimi ekleyin (bkz. Şekil 1). Visual Web Developer 2008 veya Visual Studio 2008 kullanıyorsanız, ScriptManager denetimi, AJAX uzantıları sekmesindeki araç kutusunda bulunur. Visual Studio 2005 kullanıyorsanız, önce ASP.NET AJAX çerçevesini yüklemeniz ve denetimleri araç kutusuna eklemeniz gerekir. ASP.NET 2,0 için Framework 'ü almak üzere [ASP.NET AJAX wiki](https://github.com/DevExpress/AjaxControlToolkit/wiki) 'yi ziyaret edin.

ScriptManager 'ı sayfaya ekledikten sonra, `ID` `ScriptManager1` olan `MyManager`olarak değiştirin.

[ScriptManager 'ı ana sayfaya eklemek ![](master-pages-and-asp-net-ajax-cs/_static/image2.png)](master-pages-and-asp-net-ajax-cs/_static/image1.png)

**Şekil 01**: ScriptManager 'ı ana sayfaya ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image3.png))

## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>2\. Adım: bir Içerik sayfasından ASP.NET AJAX çerçevesini kullanma

ScriptManager denetimi ana sayfaya eklendiğinde, artık herhangi bir içerik sayfasına ASP.NET AJAX Framework işlevselliği ekleyebiliriz. Northwind veritabanından rastgele seçilmiş bir ürünü görüntüleyen yeni bir ASP.NET sayfası oluşturalım. Bu görüntülemeyi her 15 saniyede bir, yeni bir ürün göstererek güncelleştirmek için ASP.NET AJAX Framework Zamanlayıcı denetimini kullanacağız.

`ShowRandomProduct.aspx`adlı kök dizinde yeni bir sayfa oluşturarak başlayın. Bu yeni sayfayı `Site.master` ana sayfasına bağlamayı unutmayın.

[Web sitesine yeni bir ASP.NET sayfası eklemek ![](master-pages-and-asp-net-ajax-cs/_static/image5.png)](master-pages-and-asp-net-ajax-cs/_static/image4.png)

**Şekil 02**: Web sitesine yeni bir ASP.NET sayfası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image6.png))

[*Ana sayfada başlık, meta etiketler ve DIĞER HTML üst bilgilerini belirtme*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) öğreticisinde, açıkça ayarlanmamışsa sayfanın başlığını oluşturan `BasePage` adlı özel bir temel sayfa sınıfı oluşturduğumuz hatırlayın. `ShowRandomProduct.aspx` sayfanın arka plan kod sınıfına gidin ve `BasePage` türetebilirsiniz (`System.Web.UI.Page`yerine).

Son olarak, `Web.sitemap` dosyasını bu ders için bir giriş içerecek şekilde güncelleştirin. Ana Içerik sayfası etkileşim dersi için `<siteMapNode>` altına aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](master-pages-and-asp-net-ajax-cs/samples/sample2.xml)]

Bu `<siteMapNode>` öğesinin eklenmesi dersler listesinde yansıtılır (bkz. Şekil 5).

### <a name="displaying-a-randomly-selected-product"></a>Rastgele seçili bir ürünü görüntüleme

`ShowRandomProduct.aspx`dön. Tasarımcıdan bir UpdatePanel denetimini araç kutusundan `MainContent` Içerik denetimine sürükleyin ve `ID` özelliğini `ProductPanel`olarak ayarlayın. UpdatePanel, ekranda kısmi sayfa geri gönderme yoluyla, zaman uyumsuz olarak güncelleştirilebilen bir bölgeyi temsil eder.

İlk göreviniz, UpdatePanel içinde rastgele seçilmiş bir ürünle ilgili bilgileri görüntülemektir. Bir DetailsView denetimini UpdatePanel 'a sürükleyerek başlayın. DetailsView denetiminin `ID` özelliğini `ProductInfo` olarak ayarlayın ve `Height` ve `Width` özelliklerini temizleyin. DetailsView 'un akıllı etiketini genişletin ve veri kaynağı seç açılan listesinden DetailsView ' ı `RandomProductDataSource`adlı yeni bir SqlDataSource denetimine bağlamayı seçin.

[DetailsView öğesini yeni bir SqlDataSource denetimine bağlama ![](master-pages-and-asp-net-ajax-cs/_static/image8.png)](master-pages-and-asp-net-ajax-cs/_static/image7.png)

**Şekil 03**: DetailsView 'ı yeni bir SqlDataSource denetimine bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image9.png))

SqlDataSource denetimini Northwind veritabanına bağlanmak için ( [*Içerik sayfası öğreticiden ana sayfayla etkileşime*](interacting-with-the-content-page-from-the-master-page-cs.md) geçmek için oluşturduğumuz) `NorthwindConnectionString` kullanarak yapılandırın. SELECT ifadesini yapılandırırken özel bir SQL ifadesini belirtmeyi seçin ve ardından aşağıdaki sorguyu girin:

[!code-sql[Main](master-pages-and-asp-net-ajax-cs/samples/sample3.sql)]

`SELECT` yan tümcesindeki `TOP 1` anahtar sözcüğü yalnızca sorgu tarafından döndürülen ilk kaydı döndürür. [`NEWID()` işlevi](https://msdn.microsoft.com/library/ms190348.aspx) , yeni bir [genel benzersiz tanımlayıcı değeri (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) oluşturur ve tablonun kayıtlarını rastgele bir sırada döndürmek için bir `ORDER BY` yan tümcesinde kullanılabilir.

[![SqlDataSource 'ı tek ve rastgele seçilmiş bir kayıt döndürecek şekilde yapılandırın](master-pages-and-asp-net-ajax-cs/_static/image11.png)](master-pages-and-asp-net-ajax-cs/_static/image10.png)

**Şekil 04**: SqlDataSource 'yi tek ve rastgele seçilmiş bir kayıt döndürecek şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image12.png))

Sihirbazı tamamladıktan sonra, Visual Studio yukarıdaki sorgu tarafından döndürülen iki sütun için bir BoundField oluşturur. Bu noktada sayfanızın bildirime dayalı biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample4.aspx)]

Şekil 5 ' te bir tarayıcıdan görüntülendiklerinde `ShowRandomProduct.aspx` sayfası gösterilmektedir. Sayfayı yeniden yüklemek için tarayıcınızın yenileme düğmesine tıklayın; Rastgele seçilen yeni bir kayıt için `ProductName` ve `UnitPrice` değerlerini görmeniz gerekir.

[Rastgele bir ürünün adı ![ve fiyat görüntülenir](master-pages-and-asp-net-ajax-cs/_static/image14.png)](master-pages-and-asp-net-ajax-cs/_static/image13.png)

**Şekil 05**: rastgele bir ürünün adı ve fiyatı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image15.png))

### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>Her 15 saniyede bir yeni ürün otomatik olarak görüntüleniyor

ASP.NET AJAX Framework, belirli bir zamanda geri gönderme gerçekleştiren bir zamanlayıcı denetimi içerir; geri göndermede, zamanlayıcının `Tick` olayı tetiklenir. Zamanlayıcı denetimi bir UpdatePanel içine yerleştirilirse, kısmen bir sayfa geri gönderme tetikleyip, yeni bir rastgele seçili ürünü göstermek üzere verileri DetailsView 'a yeniden bağlayabilirsiniz.

Bunu gerçekleştirmek için, araç kutusundan bir Zamanlayıcı sürükleyin ve UpdatePanel 'a bırakın. Zamanlayıcının `ID` `Timer1` olan `ProductTimer` ve `Interval` özelliği 60000 ' den 15000 ' e değiştirin. `Interval` özelliği, geri göndermeler arasındaki milisaniye sayısını belirtir; Bunu 15000 olarak ayarlamak, zamanlayıcının 15 saniyede bir kısmi sayfa geri gönderme tetiklemesine neden olur. Bu noktada zamanlayıcının bildirim temelli biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample5.aspx)]

Zamanlayıcının `Tick` olayı için bir olay işleyicisi oluşturun. Bu olay işleyicisinde, DetailsView 'un `DataBind` yöntemini çağırarak verileri DetailsView 'a yeniden bağlamanız gerekir. Bunun yapılması, DetailsView 'un verileri veri kaynağı denetiminden yeniden almasına izin verir. Bu, yeni bir rastgele seçilmiş kayıt (tarayıcının Yenile düğmesine tıklayarak sayfayı yeniden yüklerken olduğu gibi) seçer ve görüntüler.

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample6.cs)]

İşte bu kadar kolay! Sayfayı bir tarayıcı aracılığıyla yeniden ziyaret edin. Başlangıçta, rastgele bir ürünün bilgileri görüntülenir. Ekranı gönderdikten sonra, 15 saniye sonra, yeni bir ürün ile ilgili bilgilerin mevcut ekranın yerini aldığını fark edersiniz.

Burada neler olduğunu daha iyi görmek için, denetimin son güncelleştirilme süresini gösteren bir etiket denetimi ekleyelim. UpdatePanel içinde bir etiket Web denetimi ekleyin, `ID` `LastUpdateTime`olarak ayarlayın ve `Text` özelliğini temizleyin. Ardından, UpdatePanel 'ın `Load` olayı için bir olay işleyicisi oluşturun ve etikette geçerli saati görüntüleyin. (UpdatePanel 'ın `Load` olayı her tam veya kısmi sayfa geri göndermede tetiklenir.)

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample7.cs)]

Bu değişiklik tamamlandıktan sonra sayfa, o sırada görüntülenen ürünün yüklendiği saati içerir. Şekil 6 ilk kez ziyaret edildiğinde sayfayı gösterir. Şekil 7 ' de zamanlayıcı denetimi "ele alındıktan sonra 15 saniye" ve yeni bir ürünle ilgili bilgileri göstermek için UpdatePanel yenilendikten sonra sayfa görüntülenir.

[Rastgele seçilmiş bir ürün ![sayfa yükleme sırasında görüntülenir](master-pages-and-asp-net-ajax-cs/_static/image17.png)](master-pages-and-asp-net-ajax-cs/_static/image16.png)

**Şekil 06**: sayfa yükleme üzerinde rastgele seçilmiş bir ürün görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image18.png))

[Rastgele seçilen yeni bir ürün görüntülenirken 15 saniyede bir ![](master-pages-and-asp-net-ajax-cs/_static/image20.png)](master-pages-and-asp-net-ajax-cs/_static/image19.png)

**Şekil 07**: 15 saniyede bir rastgele seçilen yeni bir ürün görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image21.png))

## <a name="step-3-using-the-scriptmanagerproxy-control"></a>3\. Adım: ScriptManagerProxy denetimini kullanma

ScriptManager, ASP.NET AJAX Framework Istemci kitaplığı için gerekli betiği dahil etme ile birlikte özel JavaScript dosyalarını, betik etkin Web hizmetlerine başvuruları ve özel kimlik doğrulama, yetkilendirme ve profil hizmetlerini de kaydedebilir. Genellikle bu özelleştirmeler belirli bir sayfaya özeldir. Ancak, Özel Betik dosyalarına, Web hizmeti başvurularına veya kimlik doğrulama, yetkilendirme veya profil hizmetlerine ana sayfadaki ScriptManager 'da başvuruluyorsa, bunlar Web sitesinin *Tüm* sayfalarına dahil edilir.

Sayfa temelinde ScriptManager ile ilgili özelleştirmeler eklemek için ScriptManagerProxy denetimini kullanın. Bir içerik sayfasına ScriptManagerProxy ekleyebilir ve ardından özel JavaScript dosyasını, Web hizmeti başvurusunu veya kimlik doğrulama, yetkilendirme ya da profil hizmetini ScriptManagerProxy üzerinden kaydedebilirsiniz; Bu, belirli içerik sayfası için bu hizmetleri kaydetmenin etkisine sahiptir.

> [!NOTE]
> Bir ASP.NET sayfasında yalnızca birden fazla ScriptManager denetimi bulunabilir. Bu nedenle, ScriptManager denetimi ana sayfada zaten tanımlanmışsa bir içerik sayfasına ScriptManager denetimi ekleyemezsiniz. ScriptManagerProxy 'nin tek amacı, geliştiricilerin ana sayfada ScriptManager 'ı tanımlamak için bir yol sağlamaktır, ancak yine de sayfa temelinde ScriptManager özelleştirmeleri ekleme olanağına sahiptir.

ScriptManagerProxy denetimini çalışırken görmek için `ShowRandomProduct.aspx` içindeki UpdatePanel 'ı, Zamanlayıcı denetimini duraklatmak veya devam ettirmeye yönelik istemci tarafı komut dosyası kullanan bir düğme içerecek şekilde kullanalım. Zamanlayıcı denetiminde, istenen işlevselliğe ulaşmak için kullandığımız üç istemci tarafı yöntemi vardır:

- `_startTimer()`-Zamanlayıcı denetimini başlatır
- `_raiseTick()`-süreölçer denetiminin "çentik" olmasına neden olur, bu nedenle sunucuya geri ve `Tick` olayını ortaya koyar
- `_stopTimer()`-Zamanlayıcı denetimini durduruyor

`timerEnabled` adlı bir değişkenle ve `ToggleTimer`adlı bir işlevle bir JavaScript dosyası oluşturalım. `timerEnabled` değişkeni Zamanlayıcı denetiminin etkin mi yoksa devre dışı mı olduğunu gösterir; Varsayılan olarak true değerini alır. `ToggleTimer` işlevi iki giriş parametresini kabul eder: DURATION/Resume düğmesine ve Zamanlayıcı denetiminin istemci tarafı `id` değerine bir başvuru. Bu işlev, `timerEnabled`değerini değiştirir, Zamanlayıcı denetimine bir başvuru alır, süreölçeri başlatır veya sonlandırır (`timerEnabled`değerine bağlı olarak) ve düğmenin görüntü metnini "Duraklat" veya "devam" olarak güncelleştirir. Bu işlev, duraklatma/Resume düğmesine tıklandığında çağrılır.

`Scripts`adlı Web sitesinde yeni bir klasör oluşturarak başlayın. Ardından, JScript dosyası türünde `TimerScript.js` adlı betikler klasörüne yeni bir dosya ekleyin.

[![Scripts klasörüne yeni bir JavaScript dosyası ekleyin](master-pages-and-asp-net-ajax-cs/_static/image23.png)](master-pages-and-asp-net-ajax-cs/_static/image22.png)

**Şekil 08**: `Scripts` klasöre yeni bir JavaScript dosyası ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image24.png))

[![Web sitesine yeni bir JavaScript dosyası eklenmiştir](master-pages-and-asp-net-ajax-cs/_static/image26.png)](master-pages-and-asp-net-ajax-cs/_static/image25.png)

**Şekil 09**: Web sitesine yeni bir JavaScript dosyası eklenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image27.png))

Sonra, aşağıdaki komut dosyasını TimerScript. js dosyasına ekleyin:

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample8.cs)]

Şimdi bu özel JavaScript dosyasını `ShowRandomProduct.aspx`kaydetmeniz gerekir. `ShowRandomProduct.aspx` dönün ve sayfaya bir ScriptManagerProxy denetimi ekleyin; `ID` `MyManagerProxy`olarak ayarlayın. Özel bir JavaScript dosyasını kaydetmek için tasarımcıda ScriptManagerProxy denetimini seçip Özellikler penceresi gidin. Özelliklerden biri komut dosyaları olarak adlandırılmış. Bu özelliğin belirlenmesi, Şekil 10 ' da gösterilen ScriptReference koleksiyon düzenleyicisini görüntüler. Yeni bir betik başvurusu eklemek için Ekle düğmesine tıklayın ve ardından yol özelliğindeki betik dosyasının yolunu girin: `~/Scripts/TimerScript.js`.

[ScriptManagerProxy denetimine betik başvurusu ekleme ![](master-pages-and-asp-net-ajax-cs/_static/image29.png)](master-pages-and-asp-net-ajax-cs/_static/image28.png)

**Şekil 10**: ScriptManagerProxy denetimine bir betik başvurusu ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image30.png))

Komut dosyası başvurusunu ekledikten sonra, aşağıdaki biçimlendirme kod parçacığında gösterildiği gibi, ScriptManagerProxy denetiminin bildirime dayalı biçimlendirmesi, tek bir `ScriptReference` girişi ile bir `<Scripts>` koleksiyonu içerecek şekilde güncelleştirilir:

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample9.aspx)]

`ScriptReference` girişi, ScriptManagerProxy öğesine, işlenen biçimlendirmesinde JavaScript dosyasına bir başvuru ekler. Diğer bir deyişle, komut dosyasını ScriptManagerProxy dosyasına kaydederek `ShowRandomProduct.aspx` sayfanın işlenmiş çıktısı artık başka bir `<script src="url"></script>` etiketi içerir: `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`.

Artık `ShowRandomProduct.aspx` sayfasındaki istemci betiğinden `TimerScript.js` tanımlanan `ToggleTimer` işlevini çağırabiliriz. Aşağıdaki HTML 'yi UpdatePanel içine ekleyin:

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample10.aspx)]

Bu, "pause" metnini içeren bir düğme görüntüler. Her tıklandığında JavaScript işlevi `ToggleTimer` çağrılır, düğmeye bir başvuru ve Zamanlayıcı denetiminin kimlik değeri (`ProductTimer`) geçer. Zamanlayıcı denetiminin `id` değerini elde etmek için söz dizimini aklınızda edin. `<%=ProductTimer.ClientID%>`, `ProductTimer` Zamanlayıcı denetiminin `ClientID` özelliğinin değerini yayar. [*Içerik sayfalarında DENETIM kimliği adlandırması*](control-id-naming-in-content-pages-cs.md) öğreticide, sunucu tarafı `ID` değeri ile elde edilen istemci tarafı `id` değeri arasındaki farkları ve `ClientID` istemci tarafı `id`nasıl döndürdüğünü tartıştık.

Şekil 11 ' de bir tarayıcıdan ilk kez ziyaret edildiğinde Bu sayfa gösterilir. Süreölçer Şu anda çalışıyor ve görüntülenen ürün bilgilerini 15 saniyede bir güncelleştirir. Şekil 12 Duraklat düğmesine tıklandıktan sonra ekranı gösterir. Duraklat düğmesine tıklamak süreölçeri sonlandırır ve düğmenin metnini "devam" olarak güncelleştirir. Kullanıcı Sürdür ' e tıkladıktan sonra ürün bilgileri yenilenir (ve 15 saniyede bir yenilemeye devam eder).

[![süreölçer denetimini durdurmak için Duraklat düğmesine tıklayın](master-pages-and-asp-net-ajax-cs/_static/image32.png)](master-pages-and-asp-net-ajax-cs/_static/image31.png)

**Şekil 11**: süreölçer denetimini durdurmak Için Duraklat düğmesine tıklayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image33.png))

[![zamanlayıcıyı yeniden başlatmak için geri dön düğmesine tıklayın](master-pages-and-asp-net-ajax-cs/_static/image35.png)](master-pages-and-asp-net-ajax-cs/_static/image34.png)

**Şekil 12**: zamanlayıcıyı yeniden başlatmak Için sürdürür düğmesine tıklayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-pages-and-asp-net-ajax-cs/_static/image36.png))

## <a name="summary"></a>Özet

ASP.NET AJAX çerçevesini kullanarak AJAX etkin Web uygulamaları oluştururken, her AJAX etkin Web sayfasının bir ScriptManager denetimi içermesi zorunludur. Bu işlemi kolaylaştırmak için, her bir içerik sayfasına bir ScriptManager eklemek yerine ana sayfaya bir ScriptManager ekleyebiliriz. 1\. adım, bir içerik sayfasında AJAX işlevselliğini uygulama bölümünde 2. adım arandığında, ScriptManager 'ın ana sayfaya nasıl ekleneceğini gösterdi.

Belirli bir içerik sayfasına özel betikler, betik etkin Web hizmetlerine başvurular veya özelleştirilmiş kimlik doğrulama, yetkilendirme ya da profil hizmetleri eklemeniz gerekiyorsa, içerik sayfasına bir ScriptManagerProxy denetimi ekleyin ve ardından şunu yapılandırın özelleştirmeler burada. 3\. adım özel bir JavaScript dosyasını belirli bir içerik sayfasında kaydetmek için ScriptManagerProxy 'nin nasıl kullanılacağını inceledi.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET AJAX çerçevesi](../../../../ajax/index.md)
- [ASP.NET AJAX öğreticileri](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [ASP.NET AJAX videoları](../../../videos/aspnet-ajax/index.md)
- [Microsoft ASP.NET AJAX ile etkileşimli kullanıcı arabirimi oluşturma](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [Kayıtları rastgele sıralamak için NEWıD kullanma](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [Zamanlayıcı denetimini kullanma](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Önceki](interacting-with-the-content-page-from-the-master-page-cs.md)
> [İleri](specifying-the-master-page-programmatically-cs.md)
