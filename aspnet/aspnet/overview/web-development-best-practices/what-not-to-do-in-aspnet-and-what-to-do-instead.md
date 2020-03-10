---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: ASP.NET 'de ne yapacaklarınız ve bunun yerine yapılacaklar | Microsoft Docs
author: Rick-Anderson
description: Bu konu başlığı altında, insanların ASP.NET Web projeleri içinde bulunduğu birkaç yaygın hata açıklanmaktadır. Bu commo 'dan kaçınmak için yapmanız gerekenler için öneriler sağlar...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616993"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a>ASP.NET’te yapılmaması gerekenler ve bunların yerine yapılması gerekenler

> Bu konu başlığı altında, insanların ASP.NET Web projeleri içinde bulunduğu birkaç yaygın hata açıklanmaktadır. Bu, yaygın hatalardan kaçınmak için yapmanız gerekenler için öneriler sağlar. Bu, Norveççe Geliştirici Konferansı 'ndaki bir **edi** tarafından bir [sunumu](http://vimeo.com/68390507) temel alır.

## <a name="disclaimer"></a>Sorumluluk reddi

Bu konu, uygulamanızın güvenli ve verimli olmasını sağlamaya yönelik kapsamlı bir kılavuz olarak tasarlanmamıştır. Bu konuda özetlenen güvenlik ve performans için en iyi uygulamaları izlemeniz gerekir. Yalnızca .NET sınıfları ve işlemleriyle ilgili yaygın hatalardan kaçınmaya önerilir.

## <a name="overview"></a>Genel bakış

Bu konu aşağıdaki bölümleri içermektedir:

- [Standartlar uyumluluğu](#standards)

    - [Denetim bağdaştırıcıları](#adapters)
    - [Denetimlerde stil özellikleri](#styleprop)
    - [Sayfa ve denetim geri çağırmaları](#callback)
    - [Tarayıcı özelliği algılama](#browsercap)
- [Güvenlik](#security)

    - [İstek doğrulaması](#validation)
    - [Tanımlama bilgisi olmayan formlar kimlik doğrulaması ve oturumu](#cookieless)
    - [EnableViewStateMac](#viewstatemac)
    - [Orta güven](#medium)
    - [&lt;appSettings&gt;](#appsettings)
    - [UrlPathEncode](#urlpathencode)
- [Güvenilirlik ve performans](#performance)

    - [PreSendRequestHeaders ve PreSendRequestContent](#presend)
    - [Web Forms ile zaman uyumsuz sayfa olayları](#asyncevents)
    - [Yangın ve-unut Işi](#fire)
    - [Varlık gövdesi iste](#requestentity)
    - [Response. Redirect ve Response. End](#redirect)
    - [EnableViewState ve ViewStateMode](#viewstatemode)
    - [SqlMembershipProvider](#sqlprovider)
    - [Uzun süre çalışan Istekler (> 110 saniye)](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a>Standartlar uyumluluğu

<a id="adapters"></a>

### <a name="control-adapters"></a>Denetim bağdaştırıcıları

Öneri: Uyarlamalı işleme için denetim bağdaştırıcılarını kullanmayı durdurun ve bunun yerine CSS medya sorgularını ve standartlara uyumlu HTML 'yi kullanın.

Farklı cihazlar ve ortamlar için özelleştirilmiş sunu kodunu işlemek üzere .NET 2,0 ' de bulunan denetim bağdaştırıcıları tanıtılmıştır. Artık bu Uyarlamalı işleme CSS ve HTML ile gerçekleştirilebilir. Denetim bağdaştırıcılarını kullanmayı durdurup var olan bağdaştırıcıları CSS ve HTML 'ye dönüştürmeniz gerekir.

Daha fazla bilgi için bkz. [medya sorguları](http://www.w3.org/TR/css3-mediaqueries/) ve [nasıl yapılır: ASP.NET Web Forms/MVC uygulamanıza mobil sayfa ekleme](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a>Denetimlerde stil özellikleri

Öneri: Denetim biçimlendirmesinde stil değerlerini ayarlamayı durdurun ve bunun yerine CSS stil sayfalarında biçimlendirme değerlerini ayarlayın.

Web sunucusu denetimleri, satır içi stil özelliklerini ayarlamak için kullanılabilecek düzinelerce özellikler içerir. Örneğin, ForeColor özelliği bir denetim için metnin rengini ayarlar. CSS stil sayfaları aracılığıyla aynı etkiyi daha verimli bir şekilde gerçekleştirebilirsiniz. Stil sayfaları, stil değerlerini merkezileştirmenizi ve bu değerleri uygulamanız genelinde ayarlamaktan kaçınmanızı sağlar.

Aşağıdaki örnek, metni kırmızı olarak ayarlayan bir CSS sınıfını gösterir.

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

Sonraki örnek, CSS sınıfının dinamik olarak nasıl uygulanacağını gösterir.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a>Sayfa ve denetim geri çağırmaları

Öneri: sayfa ve denetim geri çağırmaları kullanmayı durdurun ve bunun yerine aşağıdakilerden herhangi birini kullanın: AJAX, UpdatePanel, MVC eylem yöntemleri, Web API veya SignalR.

Önceki ASP.NET sürümlerinde, sayfa ve denetim geri çağırma yöntemleri, bir sayfanın tamamını yenilemeksizin Web sayfasının bir bölümünü güncelleştirmenizi etkindi. Artık [Ajax](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) veya [SignalR](../../../signalr/index.md)aracılığıyla kısmi sayfa güncelleştirmelerini gerçekleştirebilirsiniz. Kolay URL 'Ler ve yönlendirme sorunları oluşmasına neden olabileceğinden, geri çağırma yöntemlerini kullanmayı durdurmanız gerekir. Denetimler varsayılan olarak, geri çağırma yöntemlerini etkinleştirmez, ancak bu özelliği bir denetimde etkinleştirdiyseniz, devre dışı bırakmanız gerekir.

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a>Tarayıcı özelliği algılama

Öneri: statik tarayıcı yeteneği algılamayı kullanmayı durdurun ve bunun yerine dinamik özellik algılamayı kullanın.

Önceki ASP.NET sürümlerinde, her tarayıcı için desteklenen özellikler bir XML dosyasında depolanmıştı. Statik arama aracılığıyla Özellik desteğini algılama en iyi yaklaşım değildir. Şimdi, bir tarayıcının desteklenen özelliklerini [Modernizr](http://modernizr.com/)gibi bir özellik algılama çerçevesi kullanarak dinamik olarak algılayabilirsiniz. Özellik algılama, bir yöntemi veya özelliği kullanmayı deneyerek ve sonra tarayıcının istenen sonucu ürettiğine bakmak için desteği belirler. Varsayılan olarak, Modernizr, Web uygulaması şablonlarına dahil edilmiştir.

<a id="security"></a>

## <a name="security"></a>Güvenlik

<a id="validation"></a>

### <a name="request-validation"></a>İstek doğrulaması

Öneri: Kullanıcı girişini doğrulayın ve çıktıyı kullanıcılardan kodlayın.

İstek doğrulama, her isteği denetleyen ve algılanan bir tehdit bulunursa isteği durduran bir ASP.NET özelliğidir. Uygulamanızı siteler arası betik saldırılarına karşı korumak için istek doğrulamasına bağlı değildir. Bunun yerine, kullanıcıların tüm girişlerini doğrulayın ve çıktıyı kodlayın. Bazı sınırlı durumlarda, girişi doğrulamak için normal ifadeler kullanabilirsiniz, ancak daha karmaşık durumlarda değerin izin verilen değerlerle eşleşip eşleşmediğini belirten .NET sınıflarını kullanarak Kullanıcı girişini doğrulamanız gerekir.

Aşağıdaki örnek, bir kullanıcı tarafından girilen URI 'nin geçerli olup olmadığını anlamak için URI sınıfında statik bir yöntemin nasıl kullanılacağını gösterir.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

Ancak, URI 'yi yeterince doğrulamak için `http` veya `https`belirttiğinden emin olun. Aşağıdaki örnek, URI 'nin geçerli olduğunu doğrulamak için örnek yöntemlerini kullanır.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

Kullanıcı girişini HTML olarak veya bir SQL sorgusunda Kullanıcı girişi ile birlikte işlemeden önce, kötü amaçlı kodun dahil olmamasını sağlamak için değerleri kodlayın.

Biçimlendirme içindeki değeri, aşağıda gösterildiği gibi% &lt;%:%&gt; sözdizimiyle bir HTML olarak kodlayabilirsiniz.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

Ya da Razor söz dizimi ' de, aşağıda gösterildiği gibi @ ile HTML kodlaması yapabilirsiniz.

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

Sonraki örnekte, arka plan kodundaki bir değeri HTML olarak kodlama gösterilmektedir.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

Bir SQL komutları için bir değeri güvenli bir şekilde kodlamak için [Sqlparametresi](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)gibi komut parametrelerini kullanın. <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a>Tanımlama bilgisi olmayan formlar kimlik doğrulaması ve oturumu

Öneri: tanımlama bilgilerini gerektir.

Kimlik doğrulama bilgilerinin sorgu dizesinde geçirilmesi güvenli değildir. Bu nedenle, uygulamanız kimlik doğrulaması içerdiğinde tanımlama bilgileri gerektir. Tanımlama bilgileriniz gizli bilgileri depoluyorsa, tanımlama bilgisi için SSL istemeyi düşünün.

Aşağıdaki örnek, Forms kimlik doğrulamasının SSL üzerinden aktarılan bir tanımlama bilgisi gerektirdiğini Web. config dosyasında nasıl belirtmektir gösterilmektedir.

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a>EnableViewStateMac

Öneri: hiçbir şekilde yanlış olarak ayarlanamaz.

Varsayılan olarak, EnableViewStateMac değeri true olarak ayarlanır. Uygulamanız görünüm durumunu kullanmıyor olsa da EnableViewStateMac 'i false olarak ayarlamayın. Bu değeri false olarak ayarlamak, uygulamanızı siteler arası komut dosyası oluşturma ile savunmasız hale getirir.

ASP.NET 4.5.2 'den başlayarak, çalışma zamanı **enableViewStateMac = true değerini**uygular. Yanlış olarak ayarlamış olsanız bile, çalışma zamanı bu değeri yoksayar ve değeri true olarak ayarlanmış şekilde devam eder. Daha fazla bilgi için bkz. [ASP.NET 4.5.2 ve EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).

Aşağıdaki örnek, EnableViewStateMac 'i true olarak ayarlamayı gösterir. Varsayılan olarak true olduğundan, bu değeri gerçekten true olarak ayarlamanız gerekmez. Ancak, uygulamanızdaki herhangi bir sayfada false olarak ayarlarsanız, bu değeri hemen düzeltmeniz gerekir.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a>Orta güven

Öneri: güvenlik sınırı olarak orta güvene (veya başka bir güven düzeyine) bağlı değildir.

Kısmi güven, uygulamanızı yeterince korumaz ve kullanılmamalıdır. Bunun yerine, tam güven kullanın ve güvenilir olmayan uygulamaları ayrı uygulama havuzlarında yalıtın. Ayrıca, her uygulama havuzunu benzersiz bir kimlik altında çalıştırın. Daha fazla bilgi için bkz. [ASP.net kısmi güven, uygulama yalıtımını garanti etmez](https://support.microsoft.com/kb/2698981).

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a>&lt;appSettings&gt;

Öneri: &lt;appSettings&gt; öğesinde güvenlik ayarlarını devre dışı bırakın.

AppSettings öğesi, güvenlik güncelleştirmeleri için gereken birçok değer içerir. Bu değerleri değiştirmemelisiniz veya devre dışı bırakmanız gerekir. Bir güncelleştirme dağıtımı sırasında bu değerleri devre dışı bırakmanız gerekiyorsa, dağıtımı tamamladıktan sonra hemen yeniden etkinleştirin.

Ayrıntılar için bkz. [ASP.net appSettings öğesi](https://msdn.microsoft.com/library/hh975440.aspx).

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a>UrlPathEncode

Öneri: bunun yerine [urlencode](https://msdn.microsoft.com/library/zttxte6w.aspx) kullanın.

UrlPathEncode yöntemi, çok özel bir tarayıcı uyumluluk sorununu çözmek için .NET Framework eklenmiştir. Bir URL 'YI yeterli şekilde kodlamaz ve uygulamanızı siteler arası komut dosyası oluşturma işleminden korumaz. Bunu uygulamanızda asla kullanmamalısınız. Bunun yerine, [urlencode](https://msdn.microsoft.com/library/zttxte6w.aspx)kullanın.

Aşağıdaki örnek, bir köprü denetimi için bir kodlanmış URL 'nin sorgu dizesi parametresi olarak nasıl geçirileceğini gösterir.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a>Güvenilirlik ve performans

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a>PreSendRequestHeaders ve PreSendRequestContent

Öneri: Bu olayları yönetilen modüllerle kullanmayın. Bunun yerine, gerekli görevi gerçekleştirmek için yerel bir IIS modülü yazın. Bkz. [yerel kod http modülleri oluşturma](https://msdn.microsoft.com/library/ms693629.aspx).

[PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) ve [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) olaylarını yerel IIS modülleriyle birlikte kullanabilirsiniz.
> [!WARNING]
> `IHttpModule`uygulayan yönetilen modüllerle `PreSendRequestHeaders` ve `PreSendRequestContent` kullanmayın. Bu özelliklerin ayarlanması, zaman uyumsuz isteklerle ilgili sorunlara neden olabilir. Uygulama Isteği yönlendirme (ARR) ve WebSockets birleşimi, W3wp 'in kilitlenmesine neden olabilecek erişim ihlali özel durumlarına neden olabilir. Örneğin, iiscore! W3_CONTEXT_BASE:: Getıblastnotification + 68 in ııscore. dll ' de bir erişim ihlali özel durumu (0xC0000005) oldu.

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a>Web formlarıyla zaman uyumsuz sayfa olayları

Öneri: Web Forms ' de, sayfa yaşam döngüsü olayları için zaman uyumsuz void yöntemleri yazmaktan kaçının ve bunun yerine zaman uyumsuz kod için [Page. RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) kullanın.

Bir sayfa olayını **Async** ve **void**ile işaretlediğinizde, zaman uyumsuz kodun ne zaman bittiğini belirleyemezsiniz. Bunun yerine, zaman uyumsuz kodu, tamamlanma durumunu izlemenize olanak verecek şekilde çalıştırmak için Page. RegisterAsyncTask kullanın.

Aşağıdaki örnek, zaman uyumsuz kod içeren bir düğme tıklama işleyicisini gösterir. Bu örnek, zaman uyumsuz bir görevin yalnızca Basitleştirilmiş bir örneği olarak sağlanmış olan ve önerilen bir uygulama olarak değil, zaman uyumsuz olarak bir dize değeri okumayı içerir.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

Zaman uyumsuz görevler kullanıyorsanız, Web. config dosyasında http çalışma zamanı hedef çerçevesini 4,5 (veya sonraki bir sürüm) olarak ayarlayın. Hedef Framework 'ün 4,5 olarak ayarlanması, .NET 4,5 ' de eklenen yeni eşitleme bağlamını etkinleştirir. Bu değer, Visual Studio 'daki yeni projelerde varsayılan olarak ayarlanır, ancak var olan bir projeyle çalışıyorsanız ayarlanmamalıdır.

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a>Yangın ve-unut işi

Öneri: ASP.NET içinde bir istek işlenirken, yangın ve unutma işini başlatmaktan kaçının (ThreadPool. QueueUserWorkItem metodunu çağırmak veya bir temsilciyi tekrar tekrar çağıran bir zamanlayıcı oluşturmak).

Uygulamanız ASP.NET içinde çalışan bir yangın-ve-unut işi içeriyorsa, uygulamanız eşitlenmemiş olabilir. Herhangi bir zamanda, uygulama etki alanı yok edilebilir, böylece devam eden işlem artık uygulamanın geçerli durumuyla eşleşmeyebilir.

Bu iş türünü ASP.NET dışında taşımalısınız. Azure 'da bir Web Işleri, Windows hizmeti veya çalışan rolü kullanarak devam eden işler gerçekleştirebilir ve bu kodu başka bir işlemden çalıştırabilirsiniz.

Bu çalışmayı ASP.NET içinde gerçekleştirmeniz gerekiyorsa kodu çalıştırmak için [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) adlı NuGet paketini ekleyebilirsiniz.

<a id="requestentity"></a>

### <a name="request-entity-body"></a>Varlık gövdesi iste

Öneri: işleyicinin Execute olayından önce Request. form veya Request. InputStream okumaktan kaçının.

Request. form veya Request. InputStream öğesinden okunan en erken, işleyicinin Execute olayı sırasında. MVC 'de denetleyici işleyicidir ve yürütme olayı eylem yöntemi çalıştırıldığında olur. Web Forms, sayfa işleyicisi ve Execute olayı Page. Init olayının tetiklendiği bir olaydır. İstek varlığı gövdesini Execute olayından daha önce okuduğunuzda, isteğin işlenmesini kesintiye uğratır.

Execute olayından önce istek varlığı gövdesini okumanız gerekiyorsa, ya [Request. GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) veya [Request. GetBufferedInputStream çağrıldıktan](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)kullanın. GetBufferlessInputStream kullandığınızda, istekten ham akışı alır ve tüm isteği işleme sorumluluğunu kabul edersiniz. GetBufferlessInputStream çağrıldıktan sonra, Request. form ve Request. InputStream, ASP.NET tarafından doldurulmadığı için kullanılamaz. GetBufferedInputStream çağrıldıktan kullandığınızda, istekten akışın bir kopyasını alırsınız. İstek. form ve Request. InputStream hala daha sonra istek içinde kullanılabilir, çünkü ASP.NET diğer kopyayı doldurur.

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a>Response. Redirect ve Response. End

Öneri: [Response. Redirect (dize)](https://msdn.microsoft.com/library/t9dwyts4.aspx)çağrıldıktan sonra iş parçacığının nasıl işlendiği farklarından haberdar olun.

[Response. Redirect (dize)](https://msdn.microsoft.com/library/t9dwyts4.aspx) yöntemi Response. End yöntemini çağırır. Zaman uyumlu bir işlemde, Istek. Redirect çağrısı geçerli iş parçacığının hemen iptal edilmesine neden olur. Ancak, zaman uyumsuz bir işlemde, yanıt. Redirect çağrısı geçerli iş parçacığını iptal etmez, bu nedenle kod yürütmesi istek için devam eder. Zaman uyumsuz bir işlemde, kod yürütmeyi durdurmak için yönteminden görevi döndürmelidir.

MVC projesinde Response. Redirect öğesini çağırmamalıdır. Bunun yerine, bir RedirectResult döndürün.

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a>EnableViewState ve ViewStateMode

Öneri: hangi denetimlerin görünüm durumunu kullanması üzerinde ayrıntılı denetim sağlamak için EnableViewState yerine ViewStateMode kullanın.

Sayfa yönergesinde EnableViewState yanlış olarak ayarlandığında, sayfa içindeki tüm denetimler için Görünüm durumu devre dışı bırakılır ve etkinleştirilemez. Sayfanızda yalnızca belirli denetimler için görünüm durumunu etkinleştirmek istiyorsanız, bu sayfada ViewStateMode 'u devre dışı olarak ayarlayın.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

Ardından, ViewStateMode 'u yalnızca görüntüleme durumu gereken denetimlerde etkin olarak ayarlayın.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

Yalnızca ihtiyacı olan denetimler için görünüm durumunu etkinleştirerek, Web sayfalarınız için Görünüm durumunun boyutunu küçültebilirsiniz.

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a>SqlMembershipProvider

Öneri: Evrensel sağlayıcıları kullanın.

Geçerli proje şablonlarında, SqlMembershipProvider, bir NuGet paketi olarak kullanılabilen [ASP.net Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)ile değiştirilmiştir. Şablonların önceki bir sürümüyle oluşturulmuş bir projede SqlMembershipProvider kullanıyorsanız, evrensel sağlayıcılara geçmeniz gerekir. Evrensel sağlayıcılar, Entity Framework tarafından desteklenen tüm veritabanları ile çalışır.

Daha fazla bilgi için bkz. [ASP.net Universal Providers tanıtımı](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a>Uzun süre çalışan istekler (> 110 saniye)

Öneri: bağlı istemciler için [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) veya [SignalR](../../../signalr/index.md) kullanın ve zaman uyumsuz g/ç işlemlerini kullanın.

Uzun süre çalışan istekler, Web uygulamanızda öngörülemeyen sonuçlara ve düşük performansa neden olabilir. İstek için varsayılan zaman aşımı ayarı 110 saniyedir. Oturum durumunu uzun süre çalışan bir istekle kullanıyorsanız, ASP.NET, oturum nesnesi üzerindeki kilidi 110 saniye sonra serbest bırakacaktır. Ancak, uygulamanız, kilit serbest bırakıldığında oturum nesnesi üzerindeki bir işlemin ortasında olabilir ve işlem başarıyla tamamlanmayabilir. İlk istek çalışırken kullanıcıdan ikinci bir istek engellenirse ikinci istek, oturum nesnesine tutarsız bir durumda erişebilir.

Uygulamanız engelleme (veya zaman uyumlu) g/ç işlemlerini içeriyorsa, uygulama yanıt vermemeye yönelik olur.

Performansı artırmak için .NET Framework zaman uyumsuz g/ç işlemlerini kullanın. Ayrıca, istemcileri sunucusuna bağlamak için WebSockets veya SignalR kullanın. Bu özellikler, uzun süreli istekleri verimli bir şekilde işlemek için tasarlanmıştır.
