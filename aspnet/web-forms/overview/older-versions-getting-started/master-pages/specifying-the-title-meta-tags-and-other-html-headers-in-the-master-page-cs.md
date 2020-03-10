---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
title: Ana sayfada başlık, meta etiketler ve diğer HTML üst bilgilerini belirtme (C#) | Microsoft Docs
author: rick-anderson
description: ', İçerik sayfasından ana sayfada assıralanmış &lt;Head&gt; öğelerini tanımlamaya yönelik farklı tekniklere bakar.'
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 0aa1c84f-c9e2-4699-b009-0e28643ecbc6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: a4ec96a5b90f664655d554c064f9d50e76ad2d58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587110"
---
# <a name="specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-c"></a>Ana Sayfada Başlık, Meta Etiketler ve Diğer HTML Üst Bilgilerini Belirtme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_03_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_03_CS.pdf)

> , İçerik sayfasından ana sayfada assıralanmış &lt;Head&gt; öğelerini tanımlamaya yönelik farklı tekniklere bakar.

## <a name="introduction"></a>Giriş

Visual Studio 2008 ' de oluşturulan yeni ana sayfalar, varsayılan olarak iki ContentPlaceHolder denetimine sahiptir: bir adlandırılmış baş ve `<head>` öğesinde bulunur; ve bir adlandırılmış `ContentPlaceHolder1`, Web formu içine yerleştirilmiş. `ContentPlaceHolder1` amacı, Web formunda sayfa temelinde özelleştirilebilecek bir bölge tanımlamaktır. ContentPlaceHolder `head`, sayfaların `<head>` bölümüne özel içerik eklemesini sağlar. (Kuşkusuz, bu iki Içerik yer tutucusu değiştirilebilir veya kaldırılabilir ve ana sayfaya ek ContentPlaceHolder eklenebilir. `Site.master`ana sayfamız Şu anda dört ContentPlaceHolder denetimine sahip.)

HTML `<head>` öğesi, belgenin kendisinin parçası olmayan Web sayfası belgesiyle ilgili bilgiler için bir depo görevi görür. Bu, Web sayfası başlığı, arama motorları veya iç gezginler tarafından kullanılan meta bilgiler ve RSS akışları, JavaScript ve CSS dosyaları gibi dış kaynakların bağlantıları gibi bilgileri içerir. Bu bilgilerden bazıları Web sitesindeki tüm sayfalarla ilgili olabilir. Örneğin, her ASP.NET sayfası için aynı CSS kurallarını ve JavaScript dosyalarını Global olarak içeri aktarmak isteyebilirsiniz. Ancak, sayfaya özgü `<head>` öğesinin bölümleri vardır. Sayfa başlığı ana bir örnektir.

Bu öğreticide, ana sayfada ve onun içerik sayfalarında genel ve sayfaya özgü `<head>` bölümü işaretlemesini nasıl tanımlayacağınızı inceleyeceğiz.

## <a name="examining-the-master-pagesheadsection"></a>Ana sayfanın`<head>`bölümü inceleniyor

Visual Studio 2008 tarafından oluşturulan varsayılan ana sayfa dosyası `<head>` bölümünde aşağıdaki biçimlendirmeyi içerir:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample1.aspx)]

`<head>` öğesinin, bir sunucu denetimi olduğunu (statik HTML yerine) belirten bir `runat="server"` özniteliği içerdiğine dikkat edin. Tüm ASP.NET sayfaları, `System.Web.UI` ad alanında bulunan [`Page` sınıfından](https://msdn.microsoft.com/library/system.web.ui.page.aspx)türetilir. Bu sınıf, sayfanın `<head>` bölgesine erişim sağlayan bir `Header` özelliği içerir. [`Header` özelliğini](https://msdn.microsoft.com/library/system.web.ui.page.header.aspx) kullanarak, bir ASP.net sayfanın başlığını ayarlayabilir veya işlenmiş `<head>` bölümüne ek biçimlendirme ekleyebilirsiniz. Daha sonra, sayfanın `Page_Load` olay işleyicisine bir kod yazarak bir içerik sayfasının `<head>` öğesini özelleştirmek mümkündür. Adım 1 ' de sayfanın başlığını programlı olarak ayarlamayı inceleyeceğiz.

Yukarıdaki `<head>` öğesinde gösterilen biçimlendirme baş adlı bir ContentPlaceHolder denetimi de içerir. İçerik sayfaları program aracılığıyla `<head>` öğesine özel içerik ekleye, bu ContentPlaceHolder denetimi gerekli değildir. Ancak, bir içerik sayfasının `<head>` öğesine statik biçimlendirme eklemesi gereken durumlarda, statik biçimlendirme, programlı olarak değil, karşılık gelen Içerik denetimine bildirimli olarak eklenebildiği durumlarda faydalıdır.

`<title>` öğesine ve baş ContentPlaceHolder 'a ek olarak, ana sayfanın `<head>` öğesi tüm sayfalarda ortak olan `<head>`düzeyinde biçimlendirme içermelidir. Web sitemizden tüm sayfalar `Styles.css` dosyasında tanımlanan CSS kurallarını kullanır. Sonuç olarak, [*ana sayfalar Ile site genelinde düzen oluşturma*](creating-a-site-wide-layout-using-master-pages-cs.md) öğreticisindeki `<head>` öğesini, karşılık gelen bir `<link>` öğesini içerecek şekilde güncelleştirdik. `Site.master` ana sayfanın geçerli `<head>` biçimlendirmesi aşağıda gösterilmektedir.

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample2.aspx)]

## <a name="step-1-setting-a-content-pages-title"></a>1\. Adım: Içerik sayfasının başlığını ayarlama

Web sayfasının başlığı `<title>` öğesi ile belirtilir. Her bir sayfanın başlığını uygun bir değere ayarlamanız önemlidir. Bir sayfa ziyaret edildiğinde, başlığı tarayıcının başlık çubuğunda görüntülenir. Buna ek olarak, bir sayfanın işaretini kaldırdığınızda, tarayıcılar sayfanın başlığını yer işareti için önerilen ad olarak kullanır. Ayrıca, birçok arama altyapısı, arama sonuçlarını görüntülerken sayfanın başlığını gösterir.

> [!NOTE]
> Varsayılan olarak, Visual Studio ana sayfadaki `<title>` öğesini "Başlıksız sayfa" olarak ayarlar. Benzer şekilde, yeni ASP.NET sayfaları, `<title>` "Başlıksız sayfa" olarak ayarlanmıştır. Sayfanın başlığını uygun bir değere ayarlamayı kolayca unutabileceğinden, Internet üzerinde "Başlıksız sayfa" başlıklı birçok sayfa vardır. Bu başlıkla Google for Web sayfalarını aramak kabaca 2.460.000 sonuç döndürüyor. Microsoft, "adsız sayfa" başlıklı web sayfalarını yayımlamaya açıktır. Bu yazma sırasında, bir Google Search, Microsoft.com etki alanında 236 Web sayfası raporladı.

Bir ASP.NET sayfası başlığını aşağıdaki yollarla belirtebilir:

- Değeri doğrudan `<title>` öğesi içine yerleştirerek
- `<%@ Page %>` yönergesinde `Title` özniteliğini kullanma
- `Page.Title="title"` veya `Page.Header.Title="title"`gibi bir kod kullanarak sayfanın `Title` özelliğini programlı olarak ayarlama.

İçerik sayfalarında, ana sayfada tanımlandığı gibi `<title>` öğesi yoktur. Bu nedenle, bir içerik sayfasının başlığını ayarlamak için `<%@ Page %>` yönergesinin `Title` özniteliğini kullanabilir ya da programlı bir şekilde ayarlayabilirsiniz.

### <a name="setting-the-pages-title-declaratively"></a>Sayfanın başlığını bildirimli olarak ayarlama

Bir içerik sayfasının başlığı, [`<%@ Page %>` yönergesinin](https://msdn.microsoft.com/library/ydy4x04a.aspx)`Title` özniteliği aracılığıyla bildirimli olarak ayarlanabilir. Bu özellik, `<%@ Page %>` yönergesinin doğrudan değiştirilerek veya Özellikler penceresi aracılığıyla ayarlanabilir. Her iki yaklaşımdan de bakalım.

Kaynak görünümünden, sayfanın bildirim temelli biçimlendirmesinin en üstünde bulunan `<%@ Page %>` yönergesini bulun. `Default.aspx` için `<%@ Page %>` yönergesi aşağıdadır:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample3.aspx)]

`<%@ Page %>` yönergesi, sayfayı ayrıştırırken ve derlerken ASP.NET altyapısının kullandığı sayfaya özgü öznitelikleri belirtir. Bu, ana sayfa dosyasını, kod dosyasının konumunu ve başlığını diğer bilgiler arasında içerir.

Varsayılan olarak, yeni bir içerik sayfası oluştururken Visual Studio `Title` özniteliğini başlıksız sayfa olarak ayarlar. `Default.aspx`"adsız sayfa" `Title` özniteliğini "Ana sayfa öğreticileri" olarak değiştirin ve ardından sayfayı bir tarayıcı üzerinden görüntüleyin. Şekil 1 ' de, yeni sayfa başlığını yansıtan tarayıcının başlık çubuğu gösterilmektedir.

![Tarayıcının başlık çubuğunda artık &quot;başlıksız sayfa yerine &quot;ana sayfa öğreticileri&quot; gösteriliyor&quot;](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image1.png)

**Şekil 01**: tarayıcının başlık çubuğu artık "Başlıksız sayfa" yerine "Ana sayfa öğreticileri" gösteriyor

Sayfanın başlığı Özellikler penceresi de ayarlanabilir. Özellikler penceresi, `Title` özelliğini içeren sayfa düzeyi özelliklerini yüklemek için, açılan listeden belge ' yi seçin. Şekil 2 ' de, `Title` "Ana sayfa öğreticileri" olarak ayarlandıktan sonra Özellikler penceresi gösterilmektedir.

![Başlığı Özellikler penceresinden de yapılandırabilirsiniz](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image2.png)

**Şekil 02**: başlığı Özellikler penceresinden, aynı şekilde yapılandırabilirsiniz

### <a name="setting-the-pages-title-programmatically"></a>Sayfanın başlığını programlama yoluyla ayarlama

Ana sayfanın `<head runat="server">` biçimlendirmesi, sayfa ASP.NET altyapısı tarafından işlendiğinde bir [`HtmlHead` sınıf](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.aspx) örneğine çevrilir. `HtmlHead` sınıfı, değeri işlenmiş `<title>` öğesinde yansıtılan bir [`Title` özelliğine](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.title.aspx) sahiptir. Bu özelliğe, `Page.Header.Title`aracılığıyla bir ASP.NET sayfasının arka plan kod sınıfından erişilebilir; Ayrıca, bu özelliğe `Page.Title`aracılığıyla erişilebilir.

Sayfanın başlığını programlı bir şekilde ayarlamak için `About.aspx` sayfanın arka plan kod sınıfına gidin ve sayfanın `Load` olayı için bir olay işleyicisi oluşturun. Sonra, sayfanın başlığını "Ana sayfa öğreticileri:: about:: *date*" olarak ayarlayın, burada *Tarih* geçerli tarihtir. Bu kodu ekledikten sonra `Page_Load` olay işleyiciniz şuna benzer şekilde görünmelidir:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample4.cs)]

Şekil 3 `About.aspx` sayfasını ziyaret ederken tarayıcının başlık çubuğunu gösterir.

![Sayfanın başlığı programlı olarak ayarlanır ve geçerli tarihi Içerir](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image3.png)

**Şekil 03**: sayfanın başlığı programlı olarak ayarlanır ve geçerli tarihi içerir

## <a name="step-2-automatically-assigning-a-page-title"></a>2\. Adım: otomatik olarak sayfa başlığı atama

1\. adımda gördüğünüz gibi, sayfanın başlığı bildirimli olarak veya program aracılığıyla ayarlanabilir. Ancak başlığı daha açıklayıcı bir şekilde değiştirmeyi unutursanız, sayfanız "adsız sayfa" varsayılan başlığına sahip olur. İdeal olarak, kendi değerini açıkça belirttiğimiz olayda, sayfanın başlığı bizim için otomatik olarak ayarlanır. Örneğin, çalışma zamanında sayfanın başlığı "Başlıksız sayfa" ise, başlığın otomatik olarak ASP.NET sayfasının dosya adıyla aynı olması için güncelleştirilmesini isteyebilirsiniz. İyi haber, büyük bir ön çalışmadır. Bu, başlığın otomatik olarak atanmasını olanaklı hale gelir.

Tüm ASP.NET Web sayfaları, `System.Web.UI` ad alanındaki `Page` sınıfından türetilir. `Page` sınıfı, bir ASP.NET sayfası için gereken en düşük işlevselliği tanımlar ve `IsPostBack`, `IsValid`, `Request`ve `Response`gibi önemli özellikleri birçok başka konuda gösterir. Bir Web uygulamasındaki her sayfa için ek özellikler veya işlevler gerekir. Bunu sağlamanın yaygın bir yolu, özel bir temel sayfa sınıfı oluşturmaktır. Özel bir temel sayfa sınıfı, `Page` sınıfından türeten ve ek işlevler içeren oluşturduğunuz bir sınıftır. Bu temel sınıf oluşturulduktan sonra, ASP.NET sayfalarınızın (`Page` sınıfı değil) ondan türemesini sağlayabilirsiniz ve böylece ASP.NET sayfalarınıza genişletilmiş işlevler sunar.

Bu adımda, başlık başka bir şekilde ayarlanmamışsa, sayfanın başlığını otomatik olarak ASP.NET sayfasının dosya adına ayarlayan bir temel sayfa oluşturuyoruz. 3\. adım, site haritasını temel alan sayfanın başlığını ayarlamaya bakar.

> [!NOTE]
> Özel temel sayfa sınıfları oluşturma ve kullanma hakkında kapsamlı bir inceleme, bu öğretici serisinin kapsamı dışındadır. Daha fazla bilgi için, [ASP.net sayfalarınızın arka plan kod sınıfları Için özel bir temel sınıf kullanarak](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)okuyun.

### <a name="creating-the-base-page-class"></a>Taban sayfası sınıfını oluşturma

İlk göreviniz, `Page` sınıfını genişleten bir sınıf olan temel sayfa sınıfı oluşturmaktır. Çözüm Gezgini proje adına sağ tıklayıp, ASP.NET klasörü Ekle ' yi seçip `App_Code`' yı seçerek projenize bir `App_Code` klasörü ekleyerek başlayın. Sonra `App_Code` klasörüne sağ tıklayın ve `BasePage.cs`adlı yeni bir sınıf ekleyin. Şekil 4 ' te, `App_Code` klasörden sonra Çözüm Gezgini gösterilmektedir ve `BasePage.cs` sınıfı eklendikten sonra.

![App_Code klasörü ve BasePage adlı bir sınıf ekleyin](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image4.png)

**Şekil 04**: `App_Code` klasörü ve `BasePage` adlı bir sınıf ekleme

> [!NOTE]
> Visual Studio, iki proje yönetimi modunu destekler: Web sitesi projeleri ve Web uygulaması projeleri. `App_Code` klasörü, Web sitesi proje modeliyle kullanılmak üzere tasarlanmıştır. Web uygulaması proje modeli kullanıyorsanız, `BasePage.cs` sınıfını `Classes`gibi `App_Code`dışında bir klasöre yerleştirin. Bu konu hakkında daha fazla bilgi için [Web sitesi projesini bir Web uygulaması projesine geçirme](http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx)konusuna bakın.

Özel temel sayfa, ASP.NET Pages 'in arka plan kod sınıfları için temel sınıf görevi görbildiğinden, `Page` sınıfını genişlemelidir.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample5.cs)]

Bir ASP.NET sayfası istendiğinde, istenen sayfada HTML olarak işlenmekte olan bir dizi aşamadan geçer. `Page` sınıfının `OnEvent` yöntemini geçersiz kılarak bir aşamaya dokunabilirsiniz. Taban sayfamız için, `LoadComplete` aşaması tarafından açıkça belirtilmemişse, başlığı otomatik olarak ayarlayalim (tahmin ettiğiniz gibi, `Load` aşamasından sonra gerçekleşir).

Bunu gerçekleştirmek için `OnLoadComplete` yöntemini geçersiz kılın ve aşağıdaki kodu girin:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample6.cs)]

`OnLoadComplete` yöntemi, `Title` özelliğinin henüz açık olarak belirlenmediğini belirleyerek başlar. `Title` Özellik `null`, boş bir dize veya "Başlıksız sayfa" değerine sahipse, istenen ASP.NET sayfasının dosya adına atanır. İstenen ASP.NET sayfasının fiziksel yoluna `C:\MySites\Tutorial03\Login.aspx`, örneğin, `Request.PhysicalPath` özelliği aracılığıyla erişilebilir. `Path.GetFileNameWithoutExtension` yöntemi, yalnızca dosya adı bölümünü çekmek için kullanılır ve bu dosya adı daha sonra `Page.Title` özelliğine atanır.

> [!NOTE]
> Başlık biçimini iyileştirmek için sizi bu mantığı geliştirmeye davet ediyorum. Örneğin, sayfanın dosya adı `Company-Products.aspx`, yukarıdaki kod "şirket-ürünler" başlığını oluşturur, ancak "Şirket ürünleri" içinde olduğu gibi Dash bir boşluk ile yerine geçer. Ayrıca, bir durum değişikliği olduğunda bir boşluk eklemeyi göz önünde bulundurun. Diğer bir deyişle, dosya adını `OurBusinessHours.aspx` dönüştüren kodu bir "Iş saatlerimiz" başlığına eklemeyi göz önünde bulundurun.

### <a name="having-the-content-pages-inherit-the-base-page-class"></a>Içerik sayfalarının temel sayfa sınıfını devralmasını

Artık `Page` sınıfı yerine özel temel sayfadan (`BasePage`) türetmek için sitemizdeki ASP.NET sayfalarını güncelleştirmeniz gerekiyor. Bunu gerçekleştirmek için, her bir arka plan kod sınıfına gidin ve sınıf bildirimini öğesinden değiştirin:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample7.cs)]

Hedef:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample8.cs)]

Bunu yaptıktan sonra, bir tarayıcı aracılığıyla siteyi ziyaret edin. `Default.aspx` veya `About.aspx`gibi başlık açıkça ayarlanmış bir sayfayı ziyaret ederseniz, açıkça belirtilen başlık kullanılır. Ancak, başlığı varsayılan ("Başlıksız sayfa") olan bir sayfayı ziyaret ederseniz, taban sayfası sınıfı başlığı sayfanın dosya adına ayarlar.

Şekil 5 ' te bir tarayıcıdan görüntülendiklerinde `MultipleContentPlaceHolders.aspx` sayfası gösterilmektedir. Başlığın tam olarak sayfanın dosya adı (uzantı), "Çoğulsuz Contentyertutucuları" şeklinde olduğunu unutmayın.

[![bir başlık açıkça belirtilmemişse, sayfanın dosya adı otomatik olarak kullanılır](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image6.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image5.png)

**Şekil 05**: bir başlık açıkça belirtilmemişse, sayfanın dosya adı otomatik olarak kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklatın](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image7.png))

## <a name="step-3-basing-the-page-title-on-the-site-map"></a>3\. Adım: sayfa başlığını site haritasında temel alma

ASP.NET, sayfa geliştiricilerinin bir dış kaynakta (bir XML dosyası veya veritabanı tablosu gibi) hiyerarşik bir site haritası tanımlamasına olanak tanıyan sağlam bir site haritası çerçevesi sunar. Bu, site haritası hakkında bilgi görüntülemek için Web denetimleriyle birlikte (örneğin, Menü ve TreeView denetimleri).

Site Haritası yapısına, bir ASP.NET sayfasının arka plan kod sınıfından de programlı olarak erişilebilir. Bu şekilde, sayfanın başlığını site haritasında karşılık gelen düğümün başlığına otomatik olarak ayarlayabiliriz. Bu işlevi sunabilmesi için 2. adımda oluşturulan `BasePage` sınıfını geliştirelim. Ancak ilk olarak sitemiz için bir site haritası oluşturmamız gerekiyor.

> [!NOTE]
> Bu öğreticide, okuyucunun zaten ASP 'yi öğrenildiği varsayılmaktadır. NET sitesinin harita özellikleri. Site haritasını kullanma hakkında daha fazla bilgi için, bkz. çok parçalı makale serime, [ASP 'Yi İnceleme. NET 'in site gezintisi](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx).

### <a name="creating-the-site-map"></a>Site Haritası oluşturma

Site Haritası sistemi, site haritası API 'sini bellek ve kalıcı bir mağaza arasında site haritası bilgilerini serileştiren mantığa bağlayan, [Sağlayıcı modeli](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)inşa edilir. .NET Framework, varsayılan site eşleme sağlayıcısı olan [`XmlSiteMapProvider` sınıfıyla](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)birlikte gelir. Adından da anlaşılacağı gibi, `XmlSiteMapProvider`, site haritası deposu olarak bir XML dosyası kullanır. Bu sağlayıcıyı site haritamızı tanımlamak için kullanalım.

Web sitesinin `Web.sitemap`adlı kök klasörde bir site haritası dosyası oluşturarak başlayın. Bunu gerçekleştirmek için, Çözüm Gezgini Web sitesinin adına sağ tıklayın, yeni öğe Ekle ' yi seçin ve Site Haritası şablonunu seçin. Dosyanın `Web.sitemap` olarak adlandırıldığından emin olun ve Ekle ' ye tıklayın.

[![Web sitesinin kök klasörüne Web. sitemap adlı bir dosya ekleyin](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image9.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image8.png)

**Şekil 06**: Web sitesinin kök klasörüne `Web.sitemap` adlı bir dosya ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image10.png))

Aşağıdaki XML 'i `Web.sitemap` dosyasına ekleyin:

[!code-xml[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample9.xml)]

Bu XML, Şekil 7 ' de gösterilen hiyerarşik site haritası yapısını tanımlar.

![Site Haritası Şu anda üç site haritası düğümünden oluşturulmuş](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image11.png)

**Şekil 07**: site haritası şu anda üç site haritası düğümünden oluşturulmuş

Yeni örnekler eklediğimiz için ilerideki öğreticilerde site haritası yapısını güncelleştireceğiz.

### <a name="updating-the-master-page-to-include-navigation-web-controls"></a>Ana sayfayı gezinti Web denetimlerini Içerecek şekilde güncelleştirme

Artık tanımlanmış bir site haritası olduğuna göre, ana sayfayı gezinti Web denetimlerini içerecek şekilde güncellemenize izin verin. Özellikle, site haritasında tanımlanan her düğüm için liste öğesiyle sıralanmamış bir liste oluşturan dersler bölümünde sol sütuna bir ListView denetimi ekleyelim.

> [!NOTE]
> ListView denetimi ASP.NET sürüm 3,5 ' e yenidir. ASP.NET 'in önceki bir sürümünü kullanıyorsanız, bunun yerine Yineleyici denetimini kullanın. ListView denetimi hakkında daha fazla bilgi için bkz. [ASP.NET 3.5 ListView ve DataPager denetimleri kullanma](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx).

Dersler bölümünden var olan sıralanmamış liste işaretlemesini kaldırarak başlayın. Sonra, araç kutusu ' ndan bir ListView denetimini sürükleyin ve ders başlığının altına bırakın. ListView, diğer görünüm denetimleriyle birlikte araç kutusunun veri bölümünde bulunur: GridView, DetailsView ve FormView. ListView 'un ID özelliğini `LessonsList`olarak ayarlayın.

Veri kaynağı yapılandırma sihirbazından ListView öğesini `LessonsDataSource`adlı yeni bir SiteMapDataSource denetimine bağlamayı seçin. SiteMapDataSource denetimi, site haritası sisteminin hiyerarşik yapısını döndürür.

[bir SiteMapDataSource denetimini LessonsList ListView Denetimine bağlama ![](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image13.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image12.png)

**Şekil 08**: `LessonsList` ListView denetimine bir SiteMapDataSource denetimi bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image14.png))

SiteMapDataSource denetimini oluşturduktan sonra, ListView 'un şablonlarını, SiteMapDataSource denetimi tarafından döndürülen her düğüm için bir liste öğesiyle birlikte sıralanmamış bir liste oluşturmak üzere tanımlamamız gerekir. Bu, aşağıdaki şablon işaretlemesi kullanılarak gerçekleştirilebilir:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample10.aspx)]

`LayoutTemplate`, SiteMapDataSource tarafından döndürülen her öğeyi belirli bir dersin bağlantısını içeren bir liste öğesi (`<li>`) olarak işlerken `ItemTemplate`, sıralanmamış bir liste için (`<ul>...</ul>`) biçimlendirme üretir.

ListView şablonlarını yapılandırdıktan sonra, Web sitesini ziyaret edin. Şekil 9 ' da gösterildiği gibi dersler bölümü, ana öğe içeren tek bir madde işaretli öğesi içerir. , Yaklaşık ve birden çok ContentPlaceHolder denetim dersi kullanıyor? SiteMapDataSource, hiyerarşik bir veri kümesi döndürmek için tasarlanmıştır, ancak ListView denetimi yalnızca hiyerarşinin tek bir düzeyini görüntüleyebilir. Sonuç olarak, yalnızca SiteMapDataSource tarafından döndürülen ilk site haritası düğümü düzeyi görüntülenir.

[Dersler bölümü tek bir liste öğesi Içerir ![](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image16.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image15.png)

**Şekil 09**: dersler bölümü tek bir liste öğesi içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image17.png))

Birden çok düzeyi göstermek için `ItemTemplate`içinde birden çok ListViews iç içe geçirebiliriz. Bu teknik, [veri öğreticisi serisi Ile çalışmamın](../../data-access/index.md) [ *ana sayfalarında ve site gezinti* öğreticisinde](../../data-access/introduction/master-pages-and-site-navigation-cs.md) incelendi. Ancak, bu öğretici serisi için site haritamız yalnızca iki düzey içerir: giriş (en üst düzey); ve her ders evin bir alt öğesi. İç içe geçmiş bir ListView yapmak yerine, [`ShowStartingNode` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) `false`olarak ayarlayarak SiteMapDataSource 'un başlangıç düğümünü döndürmamasını isteyebilirsiniz. Net etkisi, site haritası düğümlerinin ikinci katmanını döndürerek SiteMapDataSource 'un başlattığı bir sonucudur.

Bu değişiklik ile, ListView hakkında, ve birden çok ContentPlaceHolder denetim dersi kullanarak, ancak giriş için bir madde işareti öğesi atlar. Bu sorunu gidermek için, `LayoutTemplate`giriş için açıkça bir madde işareti öğesi ekleyebiliriz:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample11.aspx)]

SiteMapDataSource 'u başlangıç düğümünü atlamak ve açıkça bir giriş madde işareti öğesi eklemek üzere yapılandırarak, dersler bölümü artık amaçlanan çıktıyı görüntüler.

[Dersler bölümü, giriş ve her alt düğüm için bir madde Işareti öğesi Içerir ![](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image19.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image18.png)

**Şekil 10**: dersler bölümü, giriş ve her alt düğüm Için bir madde Işareti öğesi içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image20.png))

### <a name="setting-the-title-based-on-the-site-map"></a>Site Haritası temelinde başlık ayarlama

Site Haritası ile, site haritasında belirtilen başlığı kullanmak için `BasePage` sınıfınızı güncelleştirebiliriz. 2\. adımda, sayfanın başlığı sayfa geliştiricisi tarafından açıkça ayarlanmamışsa, yalnızca site haritası düğümünün başlığını kullanmak istiyoruz. İstenen sayfada açıkça ayarlanmış bir sayfa başlığı yoksa ve site haritasında bulunamazsa, adım 2 ' de yaptığımız gibi, istenen sayfanın dosya adını (uzantıyı azaltır) kullanmaya geri döneceğiz. Şekil 11 ' de bu karar süreci gösterilmektedir.

![Açıkça ayarlanmış bir sayfa başlığı yokluğunda, karşılık gelen site haritası düğümünün başlığı kullanılır](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image21.png)

**Şekil 11**: açıkça ayarlanmış bir sayfa başlığı yokluğunda, karşılık gelen site haritası düğümünün başlığı kullanılır

`BasePage` sınıfının `OnLoadComplete` yöntemini aşağıdaki kodu içerecek şekilde güncelleştirin:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample12.cs)]

Daha önce olduğu gibi `OnLoadComplete` yöntemi, sayfanın başlığının açıkça ayarlanmış olup olmadığını belirleyerek başlar. `Page.Title` `null`, boş bir dize veya "Başlıksız sayfa" değeri atanmışsa, kod otomatik olarak `Page.Title`bir değer atar.

Kullanılacak başlığı öğrenmek için, kod [`SiteMap` sınıfının](https://msdn.microsoft.com/library/system.web.sitemap.aspx) [`CurrentNode` özelliğine](https://msdn.microsoft.com/library/system.web.sitemap.currentnode.aspx)başvurarak başlatılır. `CurrentNode`, site haritasında istenen sayfaya karşılık gelen [`SiteMapNode`](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) örneğini döndürür. O sırada istenen sayfanın site haritasında bulunduğu varsayıldığında, `SiteMapNode``Title` özelliği sayfanın başlığına atanır. Şu anda istenen sayfa site haritasında yoksa, `CurrentNode` `null` döndürür ve istenen sayfanın dosya adı başlık olarak kullanılır (adım 2 ' de yapıldığı gibi).

Şekil 12 ' de bir tarayıcıdan görüntülendiklerinde `MultipleContentPlaceHolders.aspx` sayfası gösterilmektedir. Bu sayfanın başlığı açıkça ayarlanmadığından, bunun yerine karşılık gelen site haritası düğümünün başlığı kullanılır.

![Çoğulcontentyertutucuları. aspx sayfasının başlığı site eşlemesinden çekilir](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image22.png)

**Şekil 12**: `MultipleContentPlaceHolders.aspx` sayfasının başlığı site eşlemesinden çekilir

## <a name="step-4-adding-other-page-specific-markup-to-theheadsection"></a>4\. Adım:`<head>`bölümüne sayfaya özgü diğer biçimlendirmeleri ekleme

Adım 1, 2 ve 3 ' te sayfa temelinde `<title>` öğesi özelleştiriliyor. `<title>`ek olarak, `<head>` bölümü `<meta>` öğeleri ve `<link>` öğeleri içerebilir. Bu öğreticide daha önce belirtildiği gibi, `Site.master``<head>` bölümü `Styles.css`için bir `<link>` öğesi içerir. Bu `<link>` öğesi ana sayfa içinde tanımlandığından, tüm içerik sayfaları için `<head>` bölümüne dahil edilmiştir. Ancak sayfa temelinde `<meta>` ve `<link>` öğeleri ekleme hakkında nasıl gidebiliriz?

`<head>` bölümüne sayfaya özgü içerik eklemenin en kolay yolu, ana sayfada bir ContentPlaceHolder denetimi oluşturmaktır. Bu tür bir ContentPlaceHolder (adlandırılmış `head`) zaten var. Bu nedenle, özel `<head>` biçimlendirme eklemek için sayfada ilgili bir Içerik denetimi oluşturun ve işaretlemeyi buraya yerleştirin.

Sayfaya özel `<head>` biçimlendirme eklemeyi göstermek için, geçerli içerik sayfası kümesi için bir `<meta>` açıklama öğesi ekleyelim. `<meta>` Description öğesi, Web sayfası hakkında kısa bir açıklama sağlar; çoğu arama altyapısı, arama sonuçlarını görüntülerken bu bilgileri bir biçimde birleştirmekte.

`<meta>` Description öğesi aşağıdaki biçimdedir:

[!code-html[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample13.html)]

Bu biçimlendirmeyi bir içerik sayfasına eklemek için yukarıdaki metni, ana sayfanın baş ContentPlaceHolder öğesine eşlenen Içerik denetimine ekleyin. Örneğin, `Default.aspx`için `<meta>` açıklama öğesi tanımlamak için aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample14.aspx)]

Baş ContentPlaceHolder, HTML sayfasının gövdesinde olmadığından, Içerik denetimine eklenen biçimlendirme Tasarım görünümü gösterilmez. `<meta>` Description öğesini bir tarayıcıdan `Default.aspx` ziyaret edin. Sayfa yüklendikten sonra, kaynağı görüntüleyin ve `<head>` bölümünün Içerik denetiminde belirtilen biçimlendirmeyi içerdiğini unutmayın.

`<meta>` Description öğelerini `About.aspx`, `MultipleContentPlaceHolders.aspx`ve `Login.aspx`eklemek için bir dakikanızı ayırın.

### <a name="programmatically-adding-markup-to-theheadregion"></a>Program aracılığıyla`<head>`bölgesine biçimlendirme ekleme

Baş ContentPlaceHolder ana sayfanın `<head>` bölgesine bildirimli olarak özel biçimlendirme ekleyememize olanak sağlar. Özel biçimlendirme de programlı bir şekilde eklenebilir. `Page` sınıfının `Header` özelliğinin ana sayfada tanımlanan `HtmlHead` örneğini (`<head runat="server">`) döndürdüğünü hatırlayın.

`<head>` bölgesine program aracılığıyla içerik ekleyebilmekte olan içerik dinamik olduğunda faydalıdır. Belki de sayfayı ziyaret eden kullanıcıya dayalıdır; Belki de bir veritabanından çekilmekte olabilir. Nedeninden bağımsız olarak, denetimler koleksiyonuna şöyle bir şekilde denetimler ekleyerek `HtmlHead` içerik ekleyebilirsiniz:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample15.cs)]

Yukarıdaki kod, sayfayı tanımlayan anahtar sözcüklerin virgülle ayrılmış bir listesini sağlayan `<head>` bölgesine `<meta>` Keywords öğesi ekler. Bir `<meta>` etiketi eklemek için [`HtmlMeta`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlmeta.aspx) örneği oluşturup `Name` ve `Content` özelliklerini ayarlayıp `Header``Controls` koleksiyonuna ekleyin. Benzer şekilde, programlı olarak bir `<link>` öğesi eklemek için, bir [`HtmlLink`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmllink.aspx) nesnesi oluşturun, özelliklerini ayarlayın ve ardından `Header``Controls` koleksiyonuna ekleyin.

> [!NOTE]
> Rastgele biçimlendirme eklemek için, bir [`LiteralControl`](https://msdn.microsoft.com/library/system.web.ui.literalcontrol.aspx) örneği oluşturun, `Text` özelliğini ayarlayın ve `Header``Controls` koleksiyonuna ekleyin.

## <a name="summary"></a>Özet

Bu öğreticide, sayfa temelinde `<head>` bölge biçimlendirmesi eklemenin çeşitli yollarına baktık. Ana sayfa, ContentPlaceHolder ile bir `HtmlHead` örneği (`<head runat="server">`) içermelidir. `HtmlHead` örneği, içerik sayfalarının `<head>` bölgesine ve bildirimli olarak erişmesini ve sayfa başlığını programlı olarak ayarlamanızı sağlar; ContentPlaceHolder denetimi, bir Içerik denetimi aracılığıyla `<head>` bölümüne bildirimli olarak özel biçimlendirme eklenmesini sağlar.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET içinde sayfanın başlığını dinamik olarak ayarlama](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP 'yi İnceleme. NET 'in site gezintisi](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [HTML meta etiketlerini kullanma](http://searchenginewatch.com/showPage.html?page=2167931)
- [ASP.NET 'deki ana sayfalar](http://www.odetocode.com/articles/419.aspx)
- [ASP.NET 3.5 'in ListView ve DataPager denetimlerinin kullanımı](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET sayfalarınızın arka plan kod sınıfları için özel bir temel sınıf kullanma](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticiye ilişkin müşteri adayı gözden geçirenler Zack Jones ve suchi Banerjee ' di. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](multiple-contentplaceholders-and-default-content-cs.md)
> [İleri](urls-in-master-pages-cs.md)
