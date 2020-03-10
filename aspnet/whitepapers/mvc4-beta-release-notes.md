---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: Bu belgede, Visual Studio 2010 için ASP.NET MVC 4 Beta sürümü açıklanmaktadır.
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523305"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> Bu belgede, Visual Studio 2010 için ASP.NET MVC 4 Beta sürümü açıklanmaktadır.
> 
> > [!NOTE]
> > Bu en güncel sürüm değildir. ASP.NET MVC 4 RC sürüm notları [burada](mvc4-release-notes.md)bulunabilir.

- [Yükleme notları](#_Toc303253802)
- [Belgeler](#_Toc303253803)
- [Destek](#_Toc303253804)
- [Yazılım gereksinimleri](#_Toc303253805)
- [ASP.NET MVC 3 projesini ASP.NET MVC 4 ' e yükseltme](#_Toc303253806)
- [ASP.NET MVC 4 Beta sürümündeki yeni özellikler](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [ASP.NET tek sayfalı uygulama](#_Toc317096198)
    - [Varsayılan proje şablonlarına yönelik geliştirmeler](#_Toc303253808)
    - [Mobil proje şablonu](#_Toc303253809)
    - [Görüntüleme modları](#_Toc303253810)
    - [jQuery Mobile, görünüm değiştirici ve tarayıcı geçersiz kılma](#_Toc303253811)
    - [Visual Studio 'da kod oluşturmaya yönelik Tarifler](#_Toc303253812)
    - [Zaman uyumsuz denetleyiciler için görev desteği](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [Bilinen sorunlar ve son değişiklikler](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>Yükleme notları

Visual Studio 2010 için ASP.NET MVC 4 Beta, Web Platformu Yükleyicisi kullanılarak [ASP.NET MVC 4 ana sayfasından](../mvc/mvc4.md) yüklenebilir.

ASP.NET MVC 4 Beta sürümünü yüklemeden önce ASP.NET MVC 4 ' ün önceden yüklenmiş tüm önizlemelerini kaldırmanız gerekir.

Bu sürüm, .NET Framework 4,5 Geliştirici Önizlemesi ile uyumlu değildir. ASP.NET MVC 4 Beta sürümünü yüklemeden önce .NET 4,5 geliştirici önizlemeyi kaldırmanız gerekir.

ASP.NET MVC 4, ASP.NET MVC 3 ile yan yana yüklenebilir ve çalıştırılabilir.

<a id="_Toc303253803"></a>
## <a name="documentation"></a>Belgeler

ASP.NET MVC belgeleri aşağıdaki URL 'de MSDN Web sitesinde bulunabilir:

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET MVC hakkında öğreticiler ve diğer bilgiler ASP.NET Web sitesinin MVC 4 sayfasında ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)) bulunabilir.

<a id="_Toc303253804"></a>
## <a name="support"></a>Destek

Bu bir önizleme sürümüdür ve resmi olarak desteklenmez. Bu sürümle çalışma hakkında sorularınız varsa, ASP.NET MVC forumuna ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)) yayınlayın, burada ASP.net topluluğunun üyeleri çok sayıda resmi olmayan destek sağlayabilir.

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

Visual Studio için ASP.NET MVC 4 bileşenleri, PowerShell 2,0 ve Service Pack 1 ile Visual Studio 2010 ya da Service Pack 1 Visual Web Developer Express 2010 gerektirir.

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>ASP.NET MVC 3 projesini ASP.NET MVC 4 ' e yükseltme

ASP.NET MVC 4, aynı bilgisayarda ASP.NET MVC 3 ile yan yana yüklenebilir ve bu da bir ASP.NET MVC 3 uygulamasının ASP.NET MVC 4 ' e ne zaman yükseltileceğini seçme esnekliği sağlar.

Yükseltmenin en kolay yolu, yeni bir ASP.NET MVC 4 projesi oluşturmaktır ve var olan MVC 3 projesinden tüm görünümleri, denetleyicileri, kodu ve içerik dosyalarını yeni projeye kopyalayıp yeni projedeki derleme başvurularını eski projeyle eşleşecek şekilde güncellemedir. MVC 3 projesinde Web. config dosyasında değişiklik yaptıysanız, bu değişiklikleri MVC 4 projesindeki Web. config dosyasında da birleştirmeniz gerekir.

Mevcut bir ASP.NET MVC 3 uygulamasını sürüm 4 ' e el ile yükseltmek için aşağıdakileri yapın:

1. Projedeki tüm Web. config dosyalarında (projenin kökünde, görünümler klasöründe, diğeri ise projenizdeki her bir alana ilişkin Görünümler klasöründe bulunur), aşağıdaki metnin her bir örneğini değiştirin:

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    aşağıdaki metinle birlikte:

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. Kök Web. config dosyasında, Web *sayfaları: sürüm* öğesini "2.0.0.0" olarak güncelleştirin ve "true" değerine sahip yeni bir *Preserveloginurl* anahtarı ekleyin:

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. Çözüm Gezgini, *System. Web. Mvc* başvurusunu silin (sürüm 3 ' ü işaret eder). Ardından, *System. Web. Mvc* (v 4.0.0.0) öğesine bir başvuru ekleyin. Özellikle, derleme başvurularını güncelleştirmek için aşağıdaki değişiklikleri yapın. Ayrıntılar aşağıda verilmiştir:

    1. Çözüm Gezgini, aşağıdaki derlemelerdeki başvuruları silin: 

        - *System. Web. Mvc*(v 3.0.0.0)
        - *System. Web. Web sayfaları*(v 1.0.0.0)
        - *System. Web. Razor*(v 1.0.0.0)
        - *System. Web. Web sayfaları. Deployment*(v 1.0.0.0)
        - *System. Web. Web sayfaları. Razor*(v 1.0.0.0)
    2. Aşağıdaki derlemelere başvurular ekleyin: 

        - *System. Web. Mvc*(v 4.0.0.0)
        - *System. Web. Web sayfaları*(v 2.0.0.0)
        - *System. Web. Razor*(v 2.0.0.0)
        - *System. Web. Web sayfaları. Deployment*(v 2.0.0.0)
        - *System. Web. Web sayfaları. Razor*(v 2.0.0.0)
4. Çözüm Gezgini, proje adına sağ tıklayın ve ardından projeyi Kaldır ' ı seçin. Sonra adı tekrar sağ tıklayın ve *ProjectName*. csproj öğesini Düzenle ' yi seçin.
5. *Projecttypeguid* öğelerini bulun ve {E53F8FEA-EAE0-44A6-8774-FFD645390401} öğesini {E3E379DF-F4C6-4180-9B81-6769533ABE47} ile değiştirin.
6. Değişiklikleri kaydedin, düzenlemekte olduğunuz proje (. csproj) dosyasını kapatın, projeye sağ tıklayın ve ardından projeyi yeniden yükle ' yi seçin.
7. Proje ASP.NET MVC 'nin önceki sürümleri kullanılarak derlenen herhangi bir üçüncü taraf kitaplığına başvuruyorsa, kök Web. config dosyasını açın ve *yapılandırma* bölümünün altına aşağıdaki üç *bindingRedirect* öğesini ekleyin: 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a>ASP.NET MVC 4 Beta sürümündeki yeni özellikler

Bu bölümde ASP.NET MVC 4 Beta sürümünde tanıtılan özellikler açıklanmaktadır.

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4, tarayıcılar ve mobil cihazlar dahil olmak üzere çok sayıda istemciye ulaşabulabileceği HTTP Hizmetleri oluşturmaya yönelik yeni bir çerçeve olan ASP.NET Web API 'sini artık içerir. ASP.NET Web API 'SI Ayrıca, yeniden oluşan hizmetler oluşturmak için ideal bir platformdur.

ASP.NET Web API 'SI aşağıdaki özellikler için destek içerir:

- **Modern http programlama modeli:** Yeni ve kesin tür belirtilmiş bir HTTP nesne modeli kullanarak Web API 'inizdeki HTTP isteklerini ve yanıtlarını doğrudan erişin ve değiştirin. Aynı programlama modeli ve HTTP işlem hattı, istemci üzerinde yeni HttpClient türü aracılığıyla simetrik olarak kullanıma sunulmuştur.
- **Rotalar Için tam destek**: Web API 'leri artık, yönlendirme parametreleri ve kısıtlamalar dahil olmak üzere Web yığınının bir parçası olan tüm rota yeteneklerini destekler. Ayrıca, eylemlerle eşleme, kurallar için tam desteğe sahiptir, bu nedenle artık sınıflarınıza ve yöntemlerinize [HttpPost] gibi öznitelikler uygulamanız gerekmez.
- **İçerik anlaşması**: istemci ve sunucu birlikte ÇALıŞARAK bir API 'den döndürülen verilerin doğru biçimini belirleyebilir. XML, JSON ve form URL 'SI kodlamalı biçimler için varsayılan destek sağlıyoruz ve kendi biçimlerinizi ekleyerek ve hatta varsayılan içerik anlaşması stratejisini değiştirerek bu desteği genişletebilirsiniz.
- **Model bağlama ve doğrulama:** Model ciltler, bir HTTP isteğinin çeşitli parçalarından veri ayıklamanın kolay bir yolunu sağlar ve bu ileti parçalarını Web API 'SI eylemleri tarafından kullanılabilecek .NET nesnelerine dönüştürür.
- **Filtreler:** Web API 'Leri artık [Yetkilendir] özniteliği gibi bilinen filtreler dahil olmak üzere filtreleri desteklemektedir. Eylemler, yetkilendirme ve özel durum işleme için kendi filtrelerinizi yazabilir ve takabilirsiniz.
- **Sorgu kompozisyonu:** Yalnızca IQueryable&lt;T&gt;döndürülüyor, Web API 'niz OData URL kuralları aracılığıyla sorgulamayı destekleyecektir.
- **Http ayrıntılarının geliştirilmiş test edilebilirlik:** Statik bağlam nesnelerinde HTTP ayrıntılarını ayarlamak yerine, Web API eylemleri artık HttpRequestMessage ve HttpResponseMessage örnekleri ile çalışabilir. HTTP türlerine ek olarak özel türleriniz ile çalışmanıza olanak sağlamak için bu nesnelerin genel sürümleri de mevcuttur.
- **DependencyResolver aracılığıyla denetimin (IOC) Inversion 'ı geliştirildi:** Web API 'SI artık birçok farklı tesislere ait örnekleri almak için MVC 'nin bağımlılık Çözümleyicisi tarafından uygulanan hizmet bulucu modelini kullanır.
- **Kod tabanlı yapılandırma:** Web API yapılandırması, yalnızca kod aracılığıyla gerçekleştirilir ve yapılandırma dosyalarınızın temiz kalmasını önler.
- **Self-Host:** Web API 'Leri, yolların tam gücünden ve Web API 'sinin diğer özelliklerinin hala kullanılması sırasında IIS 'e ek olarak kendi işleminizde barındırılabilir.

ASP.NET Web API 'SI hakkında daha fazla bilgi için lütfen [https://www.asp.net/web-api](../web-api/index.md)ziyaret edin.

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a>ASP.NET tek sayfalı uygulama

ASP.NET MVC 4, JavaScript ve Web API 'Lerini kullanarak çok sayıda istemci tarafı etkileşimiyle tek sayfalı uygulamalar oluşturmaya yönelik deneyimin erken bir önizlemesini içerir. Bu destek şunları içerir:

- Önbelleğe alınmış verilerle daha zengin yerel etkileşimler için bir JavaScript kitaplıkları kümesi
- Çalışma birimi ve DAL desteği için ek Web API bileşenleri
- Hızlıca kullanmaya başlamak için yapı iskelesi içeren bir MVC proje şablonu

ASP.NET MVC 4 ' teki tek sayfalı uygulama desteğiyle ilgili daha fazla ayrıntı için lütfen [https://www.asp.net/single-page-application](../single-page-application/index.md)ziyaret edin.

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>Varsayılan proje şablonlarına yönelik geliştirmeler

Yeni ASP.NET MVC 4 projeleri oluşturmak için kullanılan şablon daha modern görünümlü bir Web sitesi oluşturmak üzere güncelleştirilmiştir:

![](mvc4-beta-release-notes/_static/image1.png)

Yüzeysel geliştirmeleri 'nin yanı sıra, yeni şablonda de geliştirilmiş işlevsellik vardır. Şablon, hiçbir özelleştirme olmadan hem masaüstü tarayıcılarında hem de mobil tarayıcılarda iyi bakmak için uyarlamalı işleme adlı bir teknik kullanır.

![](mvc4-beta-release-notes/_static/image2.png)

Uyarlamalı işleme eylemini görmek için bir mobil öykünücü kullanabilir veya masaüstü tarayıcı penceresini daha küçük olacak şekilde yeniden boyutlandırmayı deneyebilirsiniz. Tarayıcı penceresi yeterince az olduğunda, sayfanın düzeni değişecektir.

Varsayılan proje şablonunda başka bir geliştirme, JavaScript 'in kullanımı daha zengin bir kullanıcı arabirimi sağlamak için kullanılır. Şablonda kullanılan oturum açma ve kayıt bağlantıları, zengin bir oturum açma ekranı sunmak için jQuery UI Iletişim kutusunun nasıl kullanılacağına dair örneklerdir:

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>Mobil proje şablonu

Yeni bir proje başlatıyorsanız ve özellikle mobil ve tablet tarayıcıları için bir site oluşturmak istiyorsanız, yeni mobil uygulama projesi şablonunu kullanabilirsiniz. Bu, dokunarak iyileştirilmiş UI oluşturmaya yönelik açık kaynaklı bir kitaplık olan jQuery Mobile 'a dayalıdır:

![](mvc4-beta-release-notes/_static/image4.png)

Bu şablon, Internet uygulaması şablonuyla aynı uygulama yapısını içerir (ve denetleyici kodu neredeyse aynıdır), ancak daha iyi bakmak için jQuery Mobile kullanılarak stillendirilmiş ve dokunmatik tabanlı mobil cihazlarda iyi davranacağız. Mobil Kullanıcı arabirimine yönelik yapı ve stil oluşturma hakkında daha fazla bilgi edinmek için [jQuery Mobile Project Web sitesine](http://jquerymobile.com/)bakın.

Mobil olarak iyileştirilmiş görünümler eklemek istediğiniz masaüstü yönelimli bir siteniz zaten varsa veya masaüstü ve mobil tarayıcılara farklı biçimlendirilmiş görünümler sunan tek bir site oluşturmak istiyorsanız, yeni görüntüleme modları özelliğini kullanabilirsiniz. (Sonraki bölüme bakın.)

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>Görüntüleme modları

Yeni görüntü modları özelliği, bir uygulamanın, isteği yapan tarayıcıya bağlı olarak görünüm seçmesini sağlar. Örneğin, bir masaüstü tarayıcısı giriş sayfasını isterse, uygulama Views\home\ındex.cshtml şablonunu kullanabilir. Bir mobil tarayıcı giriş sayfasını isterse, uygulama Views\Home\Index.mobile.cshtml şablonunu döndürebilir.

Ayrıca, belirli tarayıcı türleri için düzenler ve partileri geçersiz kılınabilir. Örneğin:

- Views\Shared klasörünüzde hem \_Layout. cshtml hem de \_Layout. Mobile. cshtml şablonları varsa, uygulama varsayılan olarak mobil tarayıcıların istekleri sırasında \_Layout. Mobile. cshtml ve diğer istekler sırasında \_Layout. cshtml kullanır.
- Bir klasör hem \_MyPartial. cshtml hem de \_MyPartial. Mobile. cshtml içeriyorsa, yönerge @Html.Partial("\_MyPartial"), mobil tarayıcıların istekleri sırasında MyPartial. Mobile. cshtml 'yi ve diğer istekler sırasında MyPartial. cshtml dosyasını \_.\_

Diğer cihazlar için daha özel görünümler, düzenler veya kısmi görünümler oluşturmak istiyorsanız, bir istek belirli koşullara uysa aranacak adı belirtmek için yeni bir *Defaultdisplaymode* örneği kaydedebilirsiniz. Örneğin, "iPhone" dizesini, Apple iPhone tarayıcısı bir istek yaptığında geçerli bir görüntüleme modu olarak kaydetmek için, Global. asax dosyasındaki *Application\_start* yöntemine aşağıdaki kodu ekleyebilirsiniz:

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

Bu kod çalıştıktan sonra, bir Apple iPhone tarayıcısı istek yaptığında, uygulamanız Views\Shared\\_Layout. iPhone. cshtml düzeni (varsa) kullanır.

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a>jQuery Mobile, görünüm değiştirici ve tarayıcı geçersiz kılma

jQuery Mobile, dokunmatik iyileştirilmiş Web Kullanıcı arabirimi oluşturmaya yönelik açık kaynak bir kitaplıktır. JQuery Mobile 'ı bir ASP.NET MVC 4 uygulamasıyla kullanmak istiyorsanız, başlamanıza yardımcı olacak bir NuGet paketi indirebilir ve yükleyebilirsiniz. Visual Studio paket yöneticisi konsolundan yüklemek için aşağıdaki komutu yazın:

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

Bu, jQuery Mobile ve bazı yardımcı dosyalarını aşağıdakiler de dahil olmak üzere kurar:

- Görünüm/paylaşılan/\_düzen. Mobile. cshtml, jQuery Mobile tabanlı bir düzen.
- Görünümler/paylaşılan/\_Viewdeğiştirici. cshtml kısmi görünümü ve ViewSwitcherController.cs Controller içeren bir görünüm-değiştirici bileşeni.

Paketi yükledikten sonra, uygulamanızı bir mobil tarayıcı (veya Firefox [Kullanıcı Aracısı değiştirici](http://chrispederick.com/work/user-agent-switcher/) eklentisi gibi) kullanarak çalıştırın. JQuery Mobile 'ın düzen ve stil işleme yaptığından sayfalarınızın oldukça farklı olduğunu göreceksiniz. Bundan faydalanmak için şunları yapabilirsiniz:

- Daha önce [görüntüleme modları](#_Toc303253810) bölümünde açıklandığı gibi, mobil 'e özgü görünüm geçersiz kılmaları oluşturun (örneğin, mobil tarayıcılar için Views\home\ındex.cshtml 'yi geçersiz kılmak üzere Views\Home\Index.Mobile.cshtml oluşturun).
- Mobil görünümlerde dokunmatik iyileştirilmiş UI öğeleri ekleme hakkında daha fazla bilgi edinmek için [jQuery Mobile belgelerini](http://jquerymobile.com/) okuyun.

Mobil olarak iyileştirilmiş Web sayfalarına yönelik bir kural, metnin masaüstü görünümü veya tam site modu gibi, kullanıcıların sayfanın masaüstü sürümüne geçmelerini sağlayan bir bağlantı eklemektir. JQuery. Mobile. MVC paketi, bu amaçla bir örnek görünüm-değiştirici bileşeni içerir. Bu, varsayılan Views\Shared\\_Layout. Mobile. cshtml görünümünde kullanılır ve sayfa işlendiğinde şöyle görünür:

![](mvc4-beta-release-notes/_static/image5.png)

Ziyaretçiler bağlantıya tıkladıklarında aynı sayfanın masaüstü sürümüne geçiş yapılır.

Masaüstü düzeniniz varsayılan olarak bir görünüm değiştirici içermediği için, ziyaretçilerin mobil moda geçmek için bir yolu yoktur. Bunu etkinleştirmek için, *\_Viewdeğiştiricinize* aşağıdaki başvuruyu, *&lt;Body&gt;* öğesinin içinde yer alarak masaüstü mizanpajına ekleyin:

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

Görünüm değiştirici, tarayıcı geçersiz kılma adlı yeni bir özellik kullanır. Bu özellik, uygulamanızın istekleri gerçekten ait oldukları sunucudan farklı bir tarayıcıdan (Kullanıcı Aracısı) geliyormuş gibi işleme sağlar. Aşağıdaki tabloda, tarayıcı tarafından geçersiz kılınmakta olan Yöntemler listelenmiştir.

| `HttpContext.SetOverriddenBrowser(userAgentString)` | İsteğin asıl kullanıcı aracısı değerini belirtilen kullanıcı aracısını kullanarak geçersiz kılar. |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | İsteğin Kullanıcı Aracısı geçersiz kılma değerini veya geçersiz kılma belirtilmemişse gerçek Kullanıcı aracısı dizesini döndürür. |
| `HttpContext.GetOverriddenBrowser()` | İstek için ayarlanmış olan kullanıcı aracısına karşılık gelen bir *HttpBrowserCapabilitiesBase* örneği döndürür (gerçek veya geçersiz kılındı). Bu değeri, *ımobiledevice*gibi özellikleri almak için kullanabilirsiniz. |
| `HttpContext.ClearOverriddenBrowser()` | Geçerli isteğe ait tüm geçersiz kılınmış kullanıcı aracılarını kaldırır. |

Tarayıcı geçersiz kılma, ASP.NET MVC 4 ' ün temel bir özelliğidir ve jQuery. Mobile. MVC paketini yüklemeseniz bile kullanılabilir. Ancak, yalnızca görünüm, düzen ve kısmi görünüm seçimini etkiler; *istek. Browser* nesnesine bağlı olan diğer herhangi bir ASP.net özelliğini etkilemez.

Varsayılan olarak, Kullanıcı aracısının geçersiz kılınması bir tanımlama bilgisi kullanılarak depolanır. Geçersiz kılmayı başka bir yerde depolamak istiyorsanız (örneğin, bir veritabanında), varsayılan sağlayıcıyı değiştirebilirsiniz (*Browseroverridestore. Current*). Bu sağlayıcıya yönelik belgeler, ASP.NET MVC 'nin sonraki bir sürümüyle birlikte sunulacaktır.

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a>Visual Studio 'da kod oluşturmaya yönelik Tarifler

Yeni yemek tarifleri özelliği, Visual Studio 'Nun NuGet kullanarak yükleyebileceğiniz paketlere göre çözüme özgü kod oluşturmasını sağlar. Yemek tarifleri çerçevesi, geliştiricilerin kod oluşturma eklentilerini yazmasını kolaylaştırır. Bu, Ayrıca, Ekle alanı için yerleşik kod oluşturucularını değiştirmek, denetleyici eklemek ve görünüm eklemek için de kullanabilirsiniz. Tarifler NuGet paketleri olarak dağıtıldığından, kolayca kaynak denetimine denetlenebilir ve projedeki tüm geliştiricilerle otomatik olarak paylaşılabilir. Bunlar her çözüm için de kullanılabilir.

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>Zaman uyumsuz denetleyiciler için görev desteği

Artık zaman uyumsuz eylem yöntemlerini, *Task* veya *Task&lt;ActionResult&gt;* türünde bir nesne döndüren tek yöntemler olarak yazabilirsiniz.

Örneğin, Visual C# 5 kullanıyorsanız (veya [zaman uyumsuz CTP](https://msdn.microsoft.com/vstudio/async.aspx)kullanarak), aşağıdakine benzer bir zaman uyumsuz eylem yöntemi oluşturabilirsiniz:

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

Önceki eylem yönteminde, *Newsservice. GetHeadlinesAsync* ve *Sportsservice. GetScoresAsync* çağrıları zaman uyumsuz olarak çağrılır ve iş parçacığı havuzundan bir iş parçacığını engellemez.

*Görev* örnekleri döndüren zaman uyumsuz eylem metotları zaman aşımlarını de destekleyebilir. Eylem yönteminizin iptal edilebilir olması için, işlem yöntemi imzasına *CancellationToken* türünde bir parametre ekleyin. Aşağıdaki örnek, zaman aşımı süresi 2500 milisaniyelik ve zaman aşımı oluştuğunda *istemciye zaman aşımı görünümü görüntüleyen* zaman uyumsuz bir eylem yöntemini gösterir.

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 Beta, Microsoft Azure SDK 'sının 2011 Eylül 1,5 sürümünü destekler.

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>Bilinen sorunlar ve son değişiklikler

- **ASP.NET MVC 4 Beta sürümünü yükledikten sonra, Visual Studio 2010 Service Pack 1 CSHTML/VBHTML Düzenleyicisi 'ndeki CSHTML/VBHTML Düzenleyicisi, cshtml veya vbhtml dosyalarının içinde kod parçacığı veya JavaScript yazdıktan sonra uzun bir süre duraklamayabilir.** Bu yalnızca, yalnızca oluşturulan ve henüz derlenmemiş ASP.NET MVC 4 uygulamalarında oluşur.

    Geçici çözüm, bin klasöründeki derlemeleri almak için projeyi derlemek. Bin klasöründen derlemeleri kaldıran projeyi temizleyebiliyorsanız, düzenleyici sorunu geri gelecektir.

    Bu, sonraki sürümde düzeltilecektir.
- **C#Visual Studio 11 Beta için proje şablonları Global.asax.cs içinde yanlış bir bağlantı dizesi içerir.** Visual Studio 11 Beta sürümünde oluşturulan projeler için uygulama\_başlangıç yönteminde belirtilen varsayılan bağlantı, kaçışsız ters eğik çizgi (\) karakteri içeren bir LocalDB bağlantı dizesi içerir. Bu, bir SqlException üreten Entity Framework DbContext 'e erişme girişimleri sırasında bağlantı hatasına neden olur.

    Bu sorunu düzeltmek için, uygulama\_Start yöntemi içindeki ters eğik çizgi karakterini şu şekilde okunacak şekilde kaçış: Global.asax.cs.

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- **.NET 4,5 ' i hedefleyen ASP.NET MVC 4 uygulamaları, .NET 4,0 altında çalıştırıldığında System. net. http. dll derlemesine erişme girişiminde bir FileLoadException oluşturur.** .NET 4,5 altında oluşturulan ASP.NET MVC 4 uygulamaları, "dosya veya bütünleştirilmiş kod ' System .net. http ' veya bunun bağımlılıklarından biri yüklenemedi" adlı bir FileLoadException ile sonuçlanacak bir bağlama yeniden yönlendirmesi içerir. " uygulama .NET 4,0 yüklü bir sistemde yürütüldüğünde. Bu sorunu düzeltmek için, Web. config dosyasından aşağıdaki bağlama yeniden yönlendirmesini kaldırın:

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    Değiştirilen Web. config dosyasındaki derleme bağlama öğesi aşağıdaki gibi görünmelidir:

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <strong>Visual Basic projelerindeki "denetleyici Ekle" öğe şablonu, bir alanın içinden çağrıldığında yanlış bir ad alanı oluşturur</strong><strong>.</strong> Visual Basic kullanan bir ASP.NET MVC projesindeki alana denetleyici eklediğinizde, öğe şablonu denetleyiciye yanlış ad alanı ekler. Denetleyicideki herhangi bir eyleme gittiğinizde sonuç bir "dosya bulunamadı" hatasıdır.  
  
  Oluşturulan ad alanı kök ad alanından sonraki her şeyi atlar. Örneğin, oluşturulan ad alanı *RootNamespace* , ancak *RootNamespace. Areas. AreaName. Controllers* olmalıdır.
- **Razor görünüm altyapısında son değişiklikler.** Razor ayrıştırıcısının yeniden yazma kapsamında, *System. Web. Mvc. Razor*'den aşağıdaki türler kaldırılmıştır: 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  Aşağıdaki yöntemler de kaldırılmıştır: 

    - *MvcCSharpRazorCodeParser. Parseınhersdeyim(System. Web. Razor. Parser. Codeblockınfo)*
    - *MvcWebPageRazorHost. Dekoratecodegenerator (System. Web. Razor. Generator. RazorCodeGenerator)*
    - *MvcVBRazorCodeParser. Parseınhersdeyim(System. Web. Razor. Parser. Codeblockınfo)*
- **WebMatrix. WebData. dll, ASP.NET MVC 4 uygulamalarının/bin dizinine dahil edildiğinde, form kimlik doğrulamasının URL 'sini devralır.** , WebMatrix. WebData. dll derlemesini uygulamanıza ekleme (örneğin, "dağıtılabilir bağımlılıklar Ekle iletişim kutusu kullanıldığında" Razor sözdizimi ile ASP.NET Web sayfaları "nı seçerek), varsayılan ASP.NET MVC hesap denetleyicisi tarafından beklendiği gibi/Account/Login yerine/account/Logon için kimlik doğrulama oturumu açmayı geçersiz kılar. Bu davranışı engellemek ve Web. config 'in kimlik doğrulama bölümünde belirtilen URL 'YI kullanmak için PreserveLoginUrl adlı bir appSetting ekleyebilir ve bunu true olarak ayarlayabilirsiniz: 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- **NuGet Paket Yöneticisi, Visual Studio 2010 ve Visual Web Developer 2010 ' nin yan yana yüklemeleri için ASP.NET MVC 4 ' ü yüklemeye çalışırken yükleme işlemi başarısız olur.** Visual Studio 2010 ve Visual Web Developer 2010 ' i ASP.NET MVC 4 ile yan yana çalıştırmak için Visual Studio 'nun her iki sürümü de yüklendikten sonra ASP.NET MVC 4 ' ü yüklemelisiniz.
- **Önkoşullar zaten kaldırılmışsa, ASP.NET MVC 4 ' ün kaldırılması başarısız olur.** ASP.NET MVC 4'i temiz bir şekilde kaldırmak için Visual Studio 'Yu kaldırmadan önce ASP.NET MVC 4 ' ü kaldırmanız gerekir.
- **Varsayılan bir Web API projesi çalıştırmak, kullanıcının mevcut olmayan Registerapı metodunu kullanarak yollar eklemesi için hatalı bir şekilde doğrudan yönlendiren yönergeler gösterir.** Yollar, ASP.NET Route tablosu kullanılarak RegisterRoutes yöntemine eklenmelidir.
- **ASP.NET MVC 4 Beta sonları ASP.NET MVC 3 RTM uygulamaları yükleniyor.** ASP.NET MVC 3 RTM sürümüyle oluşturulmuş uygulamalar (ASP.NET MVC 3 Araçlar güncelleştirme sürümü ile değil), ASP.NET MVC 4 Beta ile yan yana çalışmak için aşağıdaki değişiklikleri gerektirir. Projeyi bu güncelleştirmeleri yapmadan oluşturmak derleme hatalarıyla sonuçlanır. 

    **Gerekli güncelleştirmeler**

  1. Kök Web. config dosyasında, anahtar *Web sayfaları: sürümü* ve *1.0.0.0*değeri Ile yeni bir *&lt;appSettings&gt;* girişi ekleyin.

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. Çözüm Gezgini, proje adına sağ tıklayın ve ardından projeyi Kaldır ' ı seçin. Sonra adı tekrar sağ tıklayın ve *ProjectName*. csproj öğesini Düzenle ' yi seçin.
  3. Aşağıdaki derleme başvurularını bulun: 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      Bunları aşağıdaki kodla değiştirin:

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. Değişiklikleri kaydedin, düzenlemekte olduğunuz proje (. csproj) dosyasını kapatın ve ardından projeye sağ tıklayıp yeniden yükle ' yi seçin.
