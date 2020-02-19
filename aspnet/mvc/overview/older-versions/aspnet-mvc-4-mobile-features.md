---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 mobil özellikleri | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticinin, Azure Web sitelerinde ASP.NET MVC 5 mobil Web uygulaması dağıtma konusunda kod örnekleri içeren bir MVC 5 sürümü bulunmaktadır.
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457654"
---
# <a name="aspnet-mvc-4-mobile-features"></a>ASP.NET MVC 4 Mobil Özellikleri

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticinin, [Azure Web sitelerinde ASP.NET MVC 5 mobil Web uygulaması dağıtma konusunda](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)kod örnekleri IÇEREN bir MVC 5 sürümü bulunmaktadır.

Bu öğretici, bir ASP.NET MVC 4 Web uygulamasındaki mobil özelliklerle nasıl çalışabileceğiniz hakkında temel bilgiler sağlar. Bu öğretici için [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) veya Visual web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer veya vwd&quot;) kullanabilirsiniz. Zaten varsa, Visual Studio 'nun profesyonel sürümünü kullanabilirsiniz.

Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun.

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (önerilir) veya Visual Studio Web Developer Express SP1. Visual Studio 2012, ASP.NET MVC 4 içerir. Visual Web Developer 2010 kullanıyorsanız, [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)' ü yüklemelisiniz.

Ayrıca, mobil tarayıcı öykünücüsünün olması gerekir. Aşağıdakilerden biri çalışacaktır:

- [Windows 7 telefon öykünücüsü](https://msdn.microsoft.com/library/ff402563(VS.92).aspx). (Bu öğreticide ekran görüntüleri çoğunda kullanılan öykünücü budur.)
- Kullanıcı aracısı dizesini bir iPhone 'a benzemek üzere değiştirin. [Bu](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) blog girişine bakın.
- [Opera mobil öykünücüsü](http://www.opera.com/developer/tools/mobile/)
- Kullanıcı aracısının iPhone olarak ayarlandığı [Apple Safari](http://www.apple.com/safari/download/) . Safari 'de Kullanıcı aracısının "iPhone" olarak nasıl ayarlanacağı hakkında yönergeler için bkz. Safari 'nin, David Alison 'un bloguna ön ceyi [nasıl öngörme](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) .

Kaynak kodlu Visual Studio C# projeleri, bu konuyla birlikte edinilebilir:

- [Başlatıcı projesi indirmesi](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [Proje indirmesi tamamlandı](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>Ne oluşturacağız?

Bu öğretici için, [Başlangıç projesinde](https://go.microsoft.com/fwlink/?LinkId=228307)sunulan basit konferans listeleme uygulamasına Mobil özellikler ekleyeceksiniz. Aşağıdaki ekran görüntüsünde, [Windows 7 telefon öykünücüsünde](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)görüldüğü gibi tamamlanmış uygulamanın Etiketler sayfası gösterilmektedir. Klavye girişini basitleştirmek için [Windows Phone öykünücüsü Için klavye eşlemesine](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) bakın.

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

[Kullanıcı aracısı dizesini](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)ayarlayarak mobil uygulamanızı geliştirmek Için Internet Explorer sürüm 9 veya 10, Firefox veya Chrome kullanabilirsiniz. Aşağıdaki görüntüde, Internet Explorer 'ın iPhone öykünmesi kullanılarak tamamlanan öğretici gösterilmektedir. Uygulamanızın hatalarını ayıklamanıza yardımcı olması için Internet Explorer F-12 geliştirici araçları ve [Fiddler aracını](http://www.fiddler2.com/fiddler2/) kullanabilirsiniz.

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>Öğrenmeniz gereken yetenekler

Öğrenirsiniz:

- ASP.NET MVC 4 şablonları, mobil cihazlarda görüntülemeyi geliştirmek için HTML5 `viewport` özniteliğini ve Uyarlamalı işlemeyi nasıl kullanır.
- Mobil olarak özel görünümler oluşturma.
- Kullanıcıların bir mobil görünüm ve uygulamanın masaüstü görünümü arasında geçiş yapmasını sağlayan bir görünüm değiştiricisi oluşturma.

### <a name="getting-started"></a>Başlarken

Aşağıdaki bağlantıyı kullanarak Başlatıcı projesi için konferans listeleme uygulamasını indirin: [indirin](https://go.microsoft.com/fwlink/?LinkId=228307). Ardından, Windows Gezgini 'nde *Mvcmobile. zip* dosyasına sağ tıklayın ve **Özellikler**' i seçin. **Mvcmobile. zip özellikleri** Iletişim kutusunda **Engellemeyi kaldır** düğmesini seçin. (Engellemeyi kaldırma, Web 'den indirdiğiniz bir *. zip* dosyasını kullanmaya çalıştığınızda oluşan bir güvenlik uyarısını önler.)

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

*Mvcmobile. zip* dosyasına sağ tıklayın ve dosyayı sıkıştırmayı açmak Için **Tümünü Ayıkla** ' yı seçin. Visual Studio 'da *Mvcmobile. sln* dosyasını açın.

Uygulamayı çalıştırmak için CTRL + F5 tuşlarına basın. Bu işlem, masaüstü tarayıcınızda görüntülenecektir. Mobil tarayıcı öykünücüsünü başlatın, konferans uygulamasının URL 'sini öykünücüye kopyalayın ve ardından **etikete göre gözatma** bağlantısına tıklayın. Windows Phone öykünücüsü kullanıyorsanız, URL çubuğuna tıklayın ve klavye erişimi almak için Duraklat tuşuna basın. Aşağıdaki görüntüde, *Alltags* görünümü gösterilir ( **etikete göre gözatamazsınız**' i seçerek).

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

Görüntü, bir mobil cihazda çok okunabilir. ASP.NET bağlantısını seçin.

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

ASP.NET etiketi görünümü çok daha karışık. Örneğin, **Tarih** sütununun okunması çok zordur. Öğreticide daha sonra, özellikle mobil tarayıcılar için olan ve ekranı okunabilir hale getirmek için *Alltags* görünümünün bir sürümünü oluşturacaksınız.

Note: Şu anda mobil önbelleğe alma altyapısında bir hata var. Üretim uygulamaları için, [sabit DisplayMode](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) parçasını paketini yüklemelisiniz. Düzeltme hakkındaki ayrıntılar için bkz. [ASP.NET MVC 4 mobil önbelleğe alma hatası düzeltildi](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) .

## <a name="css-media-queries"></a>CSS medya sorguları

[CSS medya sorguları](http://www.w3.org/TR/css3-mediaqueries/) , medya TÜRLERI için CSS uzantısı olan bir uzantıdır. Bu kişiler, belirli tarayıcılar (Kullanıcı aracıları) için varsayılan CSS kurallarını geçersiz kılan kurallar oluşturmanıza olanak sağlar. Mobil tarayıcıları hedefleyen CSS için ortak bir kural, en yüksek ekran boyutunu tanımlar. Yeni bir ASP.NET MVC 4 Internet projesi oluşturduğunuzda oluşturulan *Content\site.exe* dosyası aşağıdaki medya sorgusunu içerir:

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

Tarayıcı penceresi 850 piksel genişliğinde veya daha azsa, bu medya bloğunun içindeki CSS kurallarını kullanır. Bu gibi CSS medya sorgularını, küçük tarayıcılarda (mobil tarayıcılar gibi), masaüstü tarayıcılarının daha geniş ekranları için tasarlanan varsayılan CSS kurallarından daha iyi bir şekilde görüntülenmesini sağlamak için kullanabilirsiniz.

## <a name="the-viewport-meta-tag"></a>Görünüm penceresi meta etiketi

Çoğu mobil tarayıcı, mobil cihazın gerçek genişliğinden çok daha büyük olan bir sanal tarayıcı pencere genişliği ( *Görünüm penceresi*) tanımlar. Bu, mobil tarayıcıların tüm Web sayfasına sanal görüntü içinde sığması için izin verir. Kullanıcılar daha sonra ilginç içerikleri yakınlaştırabilir. Ancak, görünüm penceresinin genişliğini gerçek cihaz genişliğine ayarlarsanız, içerik mobil tarayıcıya sığdığından yakınlaştırma gerekmez.

ASP.NET MVC 4 düzen dosyasındaki Görünüm penceresi `<meta>` etiketi, Görünüm penceresini cihaz genişliğine göre ayarlar. Aşağıdaki satırda, ASP.NET MVC 4 düzen dosyasında Görünüm penceresi `<meta>` etiketi gösterilmektedir.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>CSS medya sorgularının ve Görünüm penceresi meta etiketinin etkisini İnceleme

Düzenleyicide *Views\shared\\_Layout. cshtml* dosyasını açın ve görünüm penceresi `<meta>` etiketini not edin. Aşağıdaki biçimlendirme, açıklamalı hattı gösterir.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

Düzenleyicide *Mvcmobile\content\site.exe* dosyasını açın ve medya sorgusundaki en büyük genişliği sıfır piksel olarak değiştirin. Bu, CSS kurallarının mobil tarayıcılarda kullanılmasını engeller. Aşağıdaki satırda değiştirilen medya sorgusu gösterilmektedir:

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

Değişikliklerinizi kaydedin ve mobil tarayıcı öykünücüsünde konferans uygulamasına gidin. Aşağıdaki resimdeki küçük metin, Görünüm penceresi `<meta>` etiketinin kaldırılmasına neden olur. Hiçbir Görünüm penceresi `<meta>` etiketiyle, tarayıcı varsayılan görünüm penceresi genişliğine (850 piksel veya çoğu mobil tarayıcı için daha geniş) yakınlaştırmış olur.

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

Değişikliklerinizi geri alma — düzen dosyasında Görünüm penceresi `<meta>` etiketinin açıklamasını kaldırın ve medya sorgusunu *site. css* dosyasında 850 piksel olarak geri yükleyin. Mobil kullanımı kolay ekran 'nin geri yüklendiğini doğrulamak için değişikliklerinizi kaydedin ve mobil tarayıcıyı yenileyin.

Görünüm penceresi `<meta>` etiketi ve CSS medya sorgusu ASP.NET MVC 4 ' e özgü değildir ve herhangi bir Web uygulamasındaki bu özelliklerden yararlanabilirsiniz. Ancak, yeni bir ASP.NET MVC 4 projesi oluşturduğunuzda oluşturulan dosyalarda yerleşik olarak bulunur.

Görünüm penceresi `<meta>` etiketi hakkında daha fazla bilgi için bkz. [bir Tale iki ayarlanamıyor (ikinci bölüm)](http://www.quirksmode.org/mobile/viewports2.html).

Sonraki bölümde, mobil tarayıcıya özgü görünümler sağlamayı öğreneceksiniz.

## <a name="overriding-views-layouts-and-partial-views"></a>Görünümleri, düzenleri ve kısmi görünümleri geçersiz kılma

ASP.NET MVC 4 ' teki önemli bir yeni özellik, genel olarak mobil tarayıcılar için, tek bir mobil tarayıcı veya belirli bir tarayıcı için herhangi bir görünümü (düzenler ve kısmi görünümler dahil) geçersiz kılmanızı sağlayan basit bir mekanizmadır. Mobil olarak belirli bir görünüm sağlamak için bir görünüm dosyası kopyalayabilir ve ekleyebilirsiniz *.* Dosya adına mobil. Örneğin, bir mobil *Dizin* görünümü oluşturmak için *Views\home\ındex.cshtml* öğesini *Views\Home\Index.Mobile.cshtml*konumuna kopyalayın.

Bu bölümde, mobil 'e özgü bir düzen dosyası oluşturacaksınız.

Başlamak için *views\shared\\_Layout. cshtml* dosyasını *views\shared\\_Layout. Mobile. cshtml*'e kopyalayın. *\_Layout. Mobile. cshtml* dosyasını açın ve **MVC4 konferansındaki** başlığı **konferans (mobil)** olarak değiştirin.

Her bir `Html.ActionLink` çağrısında, her *bir bağlantı için*"gözatarak" kaldırın. Aşağıdaki kod, mobil düzen dosyasının tamamlanan gövde bölümünü gösterir.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

*Views\home\alltags.cshtml* dosyasını *Views\Home\AllTags.Mobile.cshtml*'e kopyalayın. Yeni dosyayı açın ve `<h2>` öğesini "Etiketler" iken "Etiketler (e)" olarak değiştirin:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

Masaüstü tarayıcısı kullanarak ve mobil tarayıcı öykünücüsü 'nü kullanarak Etiketler sayfasına gidin. Mobil tarayıcı öykünücüsü yaptığınız iki değişikliği gösterir.

[![p2m_layoutTags. Mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

Buna karşılık masaüstü görüntüsü değişmemiştir.

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>Tarayıcıya özgü görünümler

Mobil ve masaüstüne özgü görünümlere ek olarak, tek bir tarayıcı için görünümler de oluşturabilirsiniz. Örneğin, özellikle iPhone tarayıcısı için olan görünümler oluşturabilirsiniz. Bu bölümde, iPhone tarayıcısı için bir düzen ve *Alltags* görünümündeki bir iPhone sürümü oluşturacaksınız.

*Global. asax* dosyasını açın ve `Application_Start` yöntemine aşağıdaki kodu ekleyin.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

Bu kod, gelen her istek için eşleştirilecek "iPhone" adlı yeni bir görüntüleme modunu tanımlar. Gelen istek tanımladığınız koşulla eşleşiyorsa (yani, Kullanıcı Aracısı "iPhone" dizesini içeriyorsa), ASP.NET MVC adı "iPhone" sonekini içeren görünümleri arayacaktır.

Kodda `DefaultDisplayMode`öğesine sağ tıklayın, **Çözümle**' yi ve ardından `using System.Web.WebPages;`' ı seçin. Bu, `DisplayModes` ve `DefaultDisplayMode` türlerinin tanımlandığı `System.Web.WebPages` ad alanına bir başvuru ekler.

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

Alternatif olarak, yalnızca aşağıdaki satırı dosyanın `using` bölümüne el ile ekleyebilirsiniz.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

*Global. asax* dosyasının tüm içeriği aşağıda gösterilmiştir.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

Değişiklikleri kaydedin. *Mvcmobile\views\shared\\_Layout. Mobile. cshtml* dosyasını *mvcmobile\views\shared\\_Layout. iPhone. cshtml*dosyasına kopyalayın. Yeni dosyayı açın ve `Conference (Mobile)` `h1` başlığını `Conference (iPhone)`olarak değiştirin.

*MvcMobile\Views\Home\AllTags.Mobile.cshtml* dosyasını *MvcMobile\Views\Home\AllTags.iPhone.cshtml*'e kopyalayın. Yeni dosyada, `<h2>` öğesini "Tags (k)" iken "Tags (iPhone)" olarak değiştirin.

Uygulamayı çalıştırın. Bir mobil tarayıcı öykünücüsü çalıştırın, Kullanıcı aracısının "iPhone" olarak ayarlandığından emin olun ve *Alltags* görünümüne gidin. Aşağıdaki ekran görüntüsünde, [Safari](http://www.apple.com/safari/download/) tarayıcısında Işlenen *alltags* görünümü gösterilmektedir. Windows için Safari 'yi [buradan](https://support.apple.com/kb/DL1531)indirebilirsiniz.

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

Bu bölümde, mobil düzenleri ve görünümleri oluşturmayı ve iPhone gibi belirli cihazlar için mizanpajları ve görünümleri oluşturmayı öğrendiniz. Sonraki bölümde, daha ilgi çekici mobil görünümler için jQuery Mobile 'dan nasıl yararlanacağınızı öğreneceksiniz.

## <a name="using-jquery-mobile"></a>JQuery Mobile 'ı kullanma

[JQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) Library, tüm büyük mobil tarayıcılarda çalışacak bir kullanıcı arabirimi çerçevesi sağlar. jQuery Mobile, CSS ve JavaScript 'i destekleyen mobil tarayıcılara *aşamalı geliştirme* uygular. Aşamalı geliştirme tüm tarayıcıların bir Web sayfasının temel içeriğini görüntülemesine izin verirken, daha güçlü tarayıcıların ve cihazların daha zengin bir görüntü almasına izin verir. Herhangi bir biçimlendirme değişikliği yapmadan mobil tarayıcılara uyum sağlamak için jQuery Mobile Style birçok öğesi ile birlikte bulunan JavaScript ve CSS dosyaları.

Bu bölümde, jQuery Mobile ve View-değiştirici pencere öğesini yükleyen *jQuery. Mobile. Mvc* NuGet paketini yükleyeceksiniz.

Başlamak için, daha önce oluşturduğunuz *paylaşılan\\_Layout. Mobile. cshtml* ve *Shared\\_Layout. iPhone. cshtml* dosyalarını silin.

*Views\Home\AllTags.Mobile.cshtml* ve *Views\Home\AllTags.iPhone.cshtml* dosyalarını *Views\Home\AllTags.iPhone.cshtml.Hide* ve *Views\Home\AllTags.Mobile.cshtml.Hide*olarak yeniden adlandırın. Dosyalar artık *. cshtml* uzantısına sahip olmadığından, *alltags* görünümünü işlemek için ASP.NET MVC çalışma zamanı tarafından kullanılmayacak.

Şunu yaparak *jQuery. Mobile. Mvc* NuGet paketini yükler:

1. **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' nu seçin.

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. **Paket Yöneticisi konsolunda**`Install-Package jQuery.Mobile.MVC -version 1.0.0` girin

Aşağıdaki görüntüde, NuGet jQuery. Mobile. MVC paketi tarafından MvcMobile projesine eklenen ve değiştirilen dosyalar gösterilmektedir. Eklenen dosyalar dosya adından sonra [Add] eklenmiş olur. Görüntü, *Content\ımages* KLASÖRÜNE eklenen GIF ve PNG dosyalarını göstermez.

![](aspnet-mvc-4-mobile-features/_static/image21.png)

JQuery. Mobile. MVC NuGet paketi aşağıdakileri yüklüyor:

- Uygulama, eklenen jQuery JavaScript ve CSS dosyalarına başvurmak için gereken *Start\paketlimobileconfig.cs dosyasını\_* . Aşağıdaki yönergeleri izlemeniz ve bu dosyada tanımlanan mobil pakete başvurmanız gerekir.
- jQuery Mobile CSS dosyaları.
- `ViewSwitcher` denetleyicisi pencere öğesi (*Controllers\viewswitchercontroller.cs*).
- jQuery Mobile JavaScript dosyaları.
- JQuery Mobile stilli bir düzen dosyası (*Views\shared\\_Layout. Mobile. cshtml*).
- Her sayfanın üst kısmında masaüstü görünümünden mobil görünüme geçiş yapmak için bir bağlantı sağlayan bir görünüm-değiştirici kısmi görünümü *(Mvcmobile\views\shared\\_ViewSwitcher. cshtml*) ve tam tersi.
- <em>Content\ımages</em> klasöründeki birkaç<em>. png</em> ve <em>. gif</em> resim dosyası.

*Global. asax* dosyasını açın ve `Application_Start` yönteminin son satırı olarak aşağıdaki kodu ekleyin.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

Aşağıdaki kod, tüm *Global. asax* dosyalarını gösterir.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> Internet Explorer 9 kullanıyorsanız ve sarı vurgulamada yukarıdaki `BundleMobileConfig` satırı görmüyorsanız, simgenin uyumluluk görünümü düğmesinin (kapalı) bir ana hat ![resminden](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Uyumluluk Görünümü düğmesinin resmi (kapalı)") uyumluluk görünümü ![düğmesinin (açık)](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Uyumluluk Görünümü düğmesinin resmi (açık)")bir düz renk resmine DEĞIŞTIRILMESINI sağlamak için, IE 'de [Uyumluluk Görünümü düğmesi](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![resmine (kapalı](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Uyumluluk Görünümü düğmesinin resmi (kapalı)") ) tıklayın. Alternatif olarak, bu öğreticiyi FireFox veya Chrome 'da görüntüleyebilirsiniz.

*Mvcmobile\views\shared\\_Layout. Mobile. cshtml* dosyasını açın ve `Html.Partial` çağrısından sonra doğrudan aşağıdaki biçimlendirmeyi ekleyin:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

Tüm *Mvcmobile\views\shared\\_Layout. Mobile. cshtml* dosyası aşağıda gösterilmektedir:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

Uygulamayı oluşturun ve mobil tarayıcı öykünücünüzde *Alltags* görünümüne gidin. Şunları görürsünüz:

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> IE veya Chrome için [Kullanıcı aracısı dizesini](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) iPhone 'a ayarlayarak ve ardından F-12 geliştirici araçlarını kullanarak, mobil özel kodda hata ayıklayabilirsiniz. Mobil tarayıcınız **giriş**, **Konuşmacı**, **etiket**ve **Tarih** bağlantılarını düğme olarak görüntülememezse jQuery Mobile Scripts ve CSS dosyalarına yapılan başvurular muhtemelen doğru değildir.

Stil değişikliklerine ek olarak, mobil görünümü ve Masaüstü görünümüne geçiş yapmanızı sağlayan bir bağlantıyı **görüntülemeyi** görürsünüz. **Masaüstü görünümü** bağlantısını seçin ve masaüstü görünümü görüntülenir.

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

Masaüstü görünümü, doğrudan mobil görünüme geri dönmek için bir yol sağlamaz. Şimdi bunu düzeltireceksiniz. *Views\shared\\_Layout. cshtml* dosyasını açın. Sayfa `body` öğesinin hemen altında, View-değiştirici pencere öğesini işleyen aşağıdaki kodu ekleyin:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

Mobil tarayıcıda *Alltags* görünümünü yenileyin. Artık masaüstü ve mobil görünümler arasında gezinebilirsiniz.

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> Hata ayıklama notiğine bakın: bir mobil cihaza ayarlanan Kullanıcı Aracısı dizesinin bulunduğu bir tarayıcı kullanırken hata ayıklamanıza yardımcı olmak için Views\Shared\\_ViewSwitcher. cshtml sonuna aşağıdaki kodu ekleyebilirsiniz.
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> ve *Views\shared\\_Layout. cshtml* dosyasına aşağıdaki başlığı ekleyerek.
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

Masaüstü tarayıcısında *Alltags* sayfasına gidin. Görünüm-değiştirici pencere öğesi yalnızca mobil düzen sayfasına eklendiğinden bir masaüstü tarayıcısında gösterilmez. Öğreticide daha sonra View-değiştirici pencere öğesini Masaüstü görünümüne nasıl ekleyebileceğiniz hakkında bilgi edineceksiniz.

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>Hoparlörler listesini iyileştirme

Mobil tarayıcıda **hoparlörler** bağlantısını seçin. Mobil görünüm (*allhoparlörler. Mobile. cshtml*) olmadığından, varsayılan hoparlörler ekranı (*allhoparlörler. cshtml*) mobil Düzen görünümü ( *\_Layout. Mobile. cshtml*) kullanılarak işlenir.

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

Varsayılan (mobil olmayan) bir görünümü, *görünümler\\_ViewStart. cshtml* dosyasında `true` `RequireConsistentDisplayMode` ayarlayarak bir mobil düzen içinde işlemeye genel olarak devre dışı bırakabilirsiniz:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

`RequireConsistentDisplayMode` `true`olarak ayarlandığında, mobil düzen (<em>\_Layout. Mobile. cshtml</em>) yalnızca mobil görünümler için kullanılır. (Diğer bir deyişle, görünüm dosyası <em>* * ViewName</em>biçimindedir<em>. Mobile. cshtml</em>.) mobil düzeninizin mobil olmayan görünümleriniz ile iyi çalışmasa `RequireConsistentDisplayMode` `true` olarak ayarlamak isteyebilirsiniz. Aşağıdaki ekran görüntüsünde, `RequireConsistentDisplayMode` `true`olarak ayarlandığında <em>hoparlör</em> sayfasının nasıl oluşturulduğu gösterilmektedir.

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

Görünüm dosyasında `RequireConsistentDisplayMode` `false` ayarlayarak bir görünümde tutarlı görüntü modunu devre dışı bırakabilirsiniz. *Views\home\allhoparlörkers.cshtml* dosyasında aşağıdaki biçimlendirme `RequireConsistentDisplayMode` `false`olarak ayarlanır:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>Mobil hoparlörler görünümü oluşturma

Yeni gördüğünüz gibi *hoparlörler* görünümü okunabilir, ancak bağlantılar küçüktür ve bir mobil cihazda dokunmak zordur. Bu bölümde, modern bir mobil uygulama gibi görünen bir mobil özel *hoparlörler* görünümü oluşturacaksınız; büyük, kolay dokunma bağlantıları görüntüler ve hoparlörleri hızlı bir şekilde bulmak için bir arama kutusu içerir.

*Allhoparlörler. cshtml* dosyasını *Allhoparlörler. Mobile. cshtml*'ye kopyalayın. *Allhoparlörler. Mobile. cshtml* dosyasını açın ve `<h2>` başlık öğesini kaldırın.

`<ul>` etiketinde `data-role` özniteliğini ekleyin ve değerini `listview`olarak ayarlayın. Diğer [`data-*` öznitelikleri](http://html5doctor.com/html5-custom-data-attributes/)gibi `data-role="listview"`, büyük liste öğelerini dokunmayı daha kolay hale getirir. Tamamlanan biçimlendirme şöyle görünür:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

Mobil tarayıcıyı yenileyin. Güncelleştirilmiş görünüm şöyle görünür:

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

Mobil görünüm iyileştirilse de uzun konuşmacı listesine gitmek zordur. Bu hatayı onarmak için, `<ul>` etiketinde `data-filter` özniteliğini ekleyin ve `true`olarak ayarlayın. Aşağıdaki kod `ul` işaretlemesini gösterir.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

Aşağıdaki görüntüde, sayfanın üst kısmındaki `data-filter` özniteliğiyle sonuçlanan arama filtresi kutusu gösterilmektedir.

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

Arama kutusuna her bir harfi yazarken jQuery Mobile, aşağıdaki görüntüde gösterildiği gibi gösterilen listeyi filtreler.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>Etiketler listesini iyileştirme

Varsayılan *hoparlörler* görünümü gibi, *Etiketler* görünümü okunabilir, ancak bağlantılar küçük ve bir mobil cihaza dokunmanız zor olur. Bu bölümde, tıpkı *hoparlörler* görünümünü düzeltilen şekilde *Etiketler* görünümünü düzeltireceksiniz.

Adın *Views\Home\AllTags.Mobile.cshtml*olması için&quot; son ekini *Views\Home\AllTags.Mobile.cshtml.Hide* dosyasına &quot;gizleyin. Yeniden adlandırılan dosyayı açın ve `<h2>` öğesini kaldırın.

`data-role` ve `data-filter` özniteliklerini, burada gösterildiği gibi `<ul>` etiketine ekleyin:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

Aşağıdaki görüntüde, `J`mektup filtrelemesinde Etiketler sayfası gösterilmektedir.

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>Tarih listesini iyileştirme

Bir mobil cihazda kullanılması daha kolay olması için *hoparlörleri* ve *Etiketler* görünümlerini geliştirmekte olduğunuz *Tarih* görünümünü geliştirebilirsiniz.

*Views\home\alldates,cshtml* dosyasını *Views\Home\AllDates.Mobile.cshtml*' e kopyalayın. Yeni dosyayı açın ve `<h2>` öğesini kaldırın.

`<ul>` etiketine `data-role="listview"` ekleyin, örneğin:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

Aşağıdaki görüntüde, **Tarih** sayfasının `data-role` özniteliğiyle nasıl göründüğü gösterilmektedir.

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) *Views\Home\AllDates.Mobile.cshtml* dosyasının içeriğini aşağıdaki kodla değiştirin:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

Bu kod tüm oturumları günlere göre gruplandırır. Her yeni gün için bir liste ayırıcı oluşturur ve bir ayırıcı altındaki her bir gün için tüm oturumları listeler. Bu kodun çalıştığı zaman şöyle görünür:

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>SessionsTable görünümünü geliştirme

Bu bölümde, bir oturum için mobil olarak belirli bir görünüm oluşturacaksınız. Yaptığımız değişiklikler oluşturduğumuz diğer görünümlerden daha kapsamlı olacaktır.

Mobil tarayıcıda **Konuşmacı** düğmesine dokunun ve arama kutusuna `Sc` yazın.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

**Scott Hanselman** bağlantısına dokunun.

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

Gördüğünüz gibi, ekran bir mobil tarayıcıda okunması zordur. Tarih sütunu okunması zor ve Etiketler sütunu görünümün dışında. Bu hatayı gidermek için, *Views\home\sessionstable.exe* *Views\Home\SessionsTable.Mobile.cshtml*dizinine kopyalayın ve sonra dosyanın içeriğini aşağıdaki kodla değiştirin:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

Kod, Oda ve Etiketler sütunlarını kaldırır ve başlık, konuşmacı ve tarihi dikey biçimlendirir, böylece tüm bu bilgiler mobil bir tarayıcıda okunabilir. Aşağıdaki görüntü, kod değişikliklerini yansıtır.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>SessionByCode görünümünü geliştirme

Son olarak, *Sessionbycode* görünümünün mobil 'e özgü bir görünümünü oluşturacaksınız. Mobil tarayıcıda **Konuşmacı** düğmesine dokunun ve arama kutusuna `Sc` yazın.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

**Scott Hanselman** bağlantısına dokunun. Scott Hanselman 'ın oturumları görüntülenir.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

**MS Web 'In sevgi bağlantısı yığınına genel bakış ' ı** seçin.

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

Varsayılan masaüstü görünümü uygundur, ancak geliştirebilirsiniz.

*Views\home\sessionbycode.exe* *Views\Home\SessionByCode.Mobile.cshtml* dizinine kopyalayın ve *Views\Home\SessionByCode.Mobile.cshtml* dosyasının içeriğini aşağıdaki biçimlendirme ile değiştirin:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

Yeni biçimlendirme, görünümün yerleşimini geliştirmek için `data-role` özniteliğini kullanır.

Mobil tarayıcıyı yenileyin. Aşağıdaki görüntüde, yaptığınız kod değişiklikleri yansıtılanlar:

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Wrapup ve gözden geçirme

Bu öğreticide, ASP.NET MVC 4 geliştirici önizlemesinin yeni mobil özellikleri tanıtılmıştır. Mobil özellikler şunları içerir:

- Yerleşimi, görünümleri ve kısmi görünümleri, hem genel hem de tek bir görünüm için geçersiz kılma özelliği.
- `RequireConsistentDisplayMode` özelliğini kullanarak düzen ve kısmi geçersiz kılma zorlaması üzerinde denetim.
- Mobil görünümler için bir görünüm değiştirici pencere öğesi de masaüstü görünümlerinde görüntülenebilirler.
- İPhone tarayıcısı gibi belirli tarayıcıları destekleme desteği.

## <a name="see-also"></a>Ayrıca Bkz.

- [jQuery Mobile](http://jquerymobile.com) sitesi.
- [jQuery Mobile genel bakış](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [W3C önerisi mobil Web uygulaması En Iyi uygulamaları](http://www.w3.org/TR/mwabp/)
- [Medya sorguları için W3C aday önerisi](http://www.w3.org/TR/css3-mediaqueries/)
