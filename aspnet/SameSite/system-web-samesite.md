---
title: ASP.NET içinde SameSite tanımlama bilgileriyle çalışma
author: rick-anderson
description: ASP.NET içindeki site tanımlama bilgilerini nasıl kullanacağınızı öğrenin
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: c81ca38648609aa5347d2a8cc11889fc85d81711
ms.sourcegitcommit: 4d439e01c82c7c95b19216fedaf5b1a11a1deb06
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76826620"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>ASP.NET içinde SameSite tanımlama bilgileriyle çalışma

Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite, siteler arası istek sahteciliği (CSRF) saldırılarına karşı bir koruma sağlamak için tasarlanmış bir [IETF](https://ietf.org/about/) taslak standardıdır. [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)içinde orijinal drafted, taslak standart [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)' de güncelleştirildi. Güncelleştirilmiş standart, önceki standartlarla geriye dönük olarak uyumlu değildir ve aşağıdakiler en belirgin farklılıklardır:

* SameSite üst bilgisi olmayan tanımlama bilgileri varsayılan olarak `SameSite=Lax` olarak değerlendirilir.
* `SameSite=None` siteler arası tanımlama bilgisi kullanımına izin vermek için kullanılmalıdır.
* `SameSite=None` onayı olan tanımlama bilgileri ayrıca `Secure`olarak işaretlenmelidir.
* SameSite = None değerine [2016 standardı](https://tools.ietf.org/html/draft-west-first-party-cookies-07) tarafından izin verilmez ve bazı uygulamaların bu tür tanımlama bilgilerini SameSite = Strict olarak ele almasına neden olur. Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .

`SameSite=Lax` ayarı çoğu uygulama tanımlama bilgisi için geçerlidir. [OpenID Connect](https://openid.net/connect/) (OIDC) ve [WS-Federation](https://auth0.com/docs/protocols/ws-fed) gibi bazı kimlik doğrulama biçimlerinden bırı, temel yönlendirmeye gönderi sağlar. POST tabanlı yeniden yönlendirmeler, SameSite tarayıcı korumalarının tetiklenmesi, bu nedenle bu bileşenler için SameSite devre dışı bırakıldı. Çoğu [OAuth](https://oauth.net/) oturum açma, istek akışının farklılığı nedeniyle etkilenmez.

`iframe` kullanan uygulamalar, "iframe 'ler siteler arası senaryolar olarak değerlendirildiğinden `SameSite=Lax` veya `SameSite=Strict` tanımlama bilgileri ile ilgili sorunlarla karşılaşabilir.

Tanımlama bilgilerini veren her ASP.NET bileşeni, SameSite ' ın uygun olup olmadığına karar vermeniz gerekir.

2019 .net SameSite güncelleştirmelerini yükledikten sonra uygulamalarla ilgili sorunların [bilinen sorunları](#known) bölümüne bakın.

## <a name="using-samesite-in-aspnet-472-and-48"></a>ASP.NET 4.7.2 ve 4,8 ' de SameSite kullanma

.NET 4.7.2 ve 4,8 Aralık 2019 ' de güncelleştirmelerin yayımlanmasından bu yana SameSite için [2019 taslak standardını](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) destekler. Geliştiriciler [HttpCookie. SameSite özelliğini](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)kullanarak SameSite üst bilgisinin değerini programlı bir şekilde denetleyebilir. `SameSite` özelliğini `Strict`, `Lax`veya `None` olarak ayarlamak, bu değerlerin tanımlama bilgisiyle ağ üzerinde yazılmasına neden olur. `(SameSiteMode)(-1)` değerine eşit ayarı, tanımlama bilgisine sahip ağa hiçbir SameSite üstbilgisinin ekleneceğini gösterir. [HttpCookie. Secure özelliği](/dotnet/api/system.web.httpcookie.secure)veya yapılandırma dosyalarındaki ' RequireSSL ', tanımlama bilgisini `Secure` olarak işaretlemek için kullanılabilir.

Yeni `HttpCookie` örnekleri `SameSite=(SameSiteMode)(-1)` ve `Secure=false`varsayılan olarak kullanılır. Bu varsayılanlar, `system.web/httpCookies` yapılandırma bölümünde geçersiz kılınabilir, burada dize `"Unspecified"` `(SameSiteMode)(-1)`için yalnızca kolay bir yapılandırma sözdizimidir:

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

ASP.Net Ayrıca, bu özellikler için kendi kendine özgü dört tanımlama bilgisi verir: anonim kimlik doğrulaması, Forms kimlik doğrulaması, oturum durumu ve rol yönetimi. Çalışma zamanında elde edilen bu tanımlama bilgilerinin örnekleri, diğer tüm HttpCookie örnekleri gibi `SameSite` ve `Secure` özellikleri kullanılarak değiştirilebilir. Ancak, aynı site standardının sürecinizin ortaya çıktı nedeniyle, bu dört özellik tanımlama bilgilerine yönelik yapılandırma seçenekleri tutarsız olur. İlgili yapılandırma bölümleri ve öznitelikler, varsayılan olarak aşağıda gösterilmiştir. Bir özellik için `SameSite` veya `Secure` ilgili özniteliği yoksa, bu özellik yukarıda açıklanan `system.web/httpCookies` bölümünde yapılandırılan varsayılanlara geri döner.

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequiresSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**Note**: ' belirtilmemiş ' yalnızca şu anda `system.web/httpCookies@sameSite` kullanılabilir. Gelecekteki güncelleştirmelerde daha önce gösterilen tanımlama bilgisi Esamesite özniteliklerine benzer bir sözdizimi eklemenizi umuyoruz. Koddaki `(SameSiteMode)(-1)` ayarlanması bu tanımlama bilgilerinin örneklerinde hala geçerlidir. *

## <a name="history-and-changes"></a>Geçmiş ve değişiklikler

SameSite desteği ilk olarak .NET 4.7.2 'de [2016 taslak standardı](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)kullanılarak uygulanmıştır.

19 Kasım 2019, 2016 standardı ile 2019 standardına kadar, Windows için Kasım ' i güncelleştirme. Diğer Windows sürümlerine ek güncelleştirmeler geliyor. Daha fazla bilgi için bkz. <xref:samesite/kbs-samesite>.

 SameSite belirtiminin 2019 taslağı:

* , 2016 taslağı ile geriye dönük olarak uyumlu **değildir** . Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.
* Tanımlama bilgilerinin varsayılan olarak `SameSite=Lax` olarak değerlendirilip değerlendirilmediğini belirtir.
* Siteler arası teslimin de `Secure`olarak işaretlenmesi için `SameSite=None` açıkça onaylama tanımlama bilgilerini belirtir.
* Yukarıda listelenen BB 'de açıklandığı şekilde verilen düzeltme ekleri tarafından desteklenir.
* , [Şubat 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)' de varsayılan olarak [Chrome](https://chromestatus.com/feature/5088147346030592) tarafından etkinleştirilmek üzere zamanlanır. Tarayıcılar 2019 içinde bu standarda geçmeyi başlattı.

<a name="known"><a/>

## <a name="known-issues"></a>Bilinen Sorunlar

2016 ve 2019 taslak belirtimleri uyumlu olmadığından, Kasım 2019 .NET Framework güncelleştirmesi, kırılmaya neden olabilecek bazı değişiklikler sunar.

* Oturum durumu ve Forms kimlik doğrulama tanımlama bilgileri artık ağa belirtilmemiş değil `Lax` olarak yazılır.
  * Çoğu uygulama `SameSite=Lax` tanımlama bilgileriyle çalışırken, siteler arasında GÖNDERI yapan uygulamalar veya `iframe` kullanan uygulamalar, oturum durumu veya form yetkilendirme tanımlama bilgilerinin beklendiği şekilde kullanılmadığını bulabilir. Bu sorunu gidermek için, uygun yapılandırma bölümündeki `cookieSameSite` değerini daha önce anlatıldığı gibi değiştirin.
* Artık kod veya yapılandırmada `SameSite=None` açıkça ayarlanmış olan HttpCookies, daha önce atlandığı halde bu değerin tanımlama bilgisiyle yazılmış olmasına sahiptir. Bu, yalnızca 2016 taslak standardını destekleyen eski tarayıcılarla ilgili sorunlara neden olabilir.
  * `SameSite=None` tanımlama bilgileriyle 2019 taslak standardını destekleyen tarayıcıları hedeflerken, Ayrıca, `Secure` işaretlemeyi veya tanınmadığını unutmayın.
  * `SameSite=None`yazmadan 2016 davranışına dönmek için `aspnet:SupressSameSiteNone=true`uygulama ayarını kullanın. Bunun, uygulamadaki tüm HttpCookies için uygulanacağını unutmayın.

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service — SameSite tanımlama bilgisi işleme

Azure App Service .NET 4.7.2 uygulamalarında SameSite davranışlarını yapılandırma hakkında bilgi için bkz. [Azure App Service — SameSite tanımlama bilgisi işleme ve .NET Framework 4.7.2 Patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>Eski tarayıcıları destekleme

2016 SameSite Standard uygulanan, bilinmeyen değerlerin `SameSite=Strict` değer olarak değerlendirilmelidir. 2016 SameSite standardını destekleyen eski tarayıcılardan erişilen uygulamalar, bir `None`değeri olan bir SameSite özelliği edindiklerinde kesintiye uğramayabilir. Web uygulamaları, eski tarayıcıları desteklemek istiyorlarsa, tarayıcı algılaması gerçekleştirmelidir. ASP.NET tarayıcı algılamayı uygulamaz; çünkü kullanıcı aracıları değerleri yüksek ölçüde geçici ve sık sık değiştirilir. Aşağıdaki kod <xref:HTTP.HttpCookie> çağrı sitesinde çağrılabilir:

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

Yukarıdaki örnekte `MyUserAgentDetectionLib.DisallowsSameSiteNone`, Kullanıcı aracısının SameSite `None`desteklemeymediğini algılayan Kullanıcı tarafından sağlanan bir kitaplıktır. Aşağıdaki kod bir örnek `DisallowsSameSiteNone` yöntemi gösterir:

> [!WARNING]
> Aşağıdaki kod yalnızca tanıtım amaçlıdır:
> * Tamamlanmış olarak düşünülmemelidir.
> * Korunmaz veya desteklenmez.

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>SameSite sorunları için test uygulamaları

Üçüncü taraf oturum açma bilgileri gibi uzak sitelerle etkileşim kuran uygulamalar şunlar gerekir:

* Etkileşimi birden çok tarayıcıda test edin.
* [Tarayıcı algılamasını ve](#sob) bu belgede açıklanan risk azaltma işlemini uygulayın.

Yeni SameSite davranışını kabul edebilir bir istemci sürümünü kullanarak Web uygulamalarını test edin. Chrome, Firefox ve Kmıum Edge tümünde test için kullanılabilecek yeni bir katılım özelliği bayrakları vardır. Uygulamanız SameSite düzeltme eklerini uyguladıktan sonra, daha eski istemci sürümleriyle test edin, özellikle Safari. Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.

### <a name="test-with-chrome"></a>Chrome ile test etme

Chrome 78 + bir yerde geçici bir risk azaltma yaptığından yanıltıcı sonuçlar verir. Chrome 78 + geçici risk azaltma, iki dakikadan daha eski tanımlama bilgilerine izin verir. Uygun test bayraklarıyla etkin olan Chrome 76 veya 77 daha doğru sonuçlar sağlar. Yeni SameSite davranışını test etmek için `chrome://flags/#same-site-by-default-cookies` **etkin**olarak değiştirin. Chrome 'un (75 ve üzeri) eski sürümleri, yeni `None` ayarı ile başarısız olarak bildirilir. Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .

Google, eski Chrome sürümlerini kullanılabilir hale getirir. Chrome 'un eski sürümlerini test etmek için [Kmıum indirme](https://www.chromium.org/getting-involved/download-chromium) bölümündeki yönergeleri izleyin. Chrome 'un eski sürümlerini arayarak sunulan bağlantılardan **Chrome indirmeyin** .

* [Kmıum 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Kmıum 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Safari ile test etme

Safari 12, önceki taslağı tamamen uyguladık ve yeni `None` değeri bir tanımlama bilgisinde olduğunda başarısız olur. Bu belgede [eski tarayıcıları destekleyen](#sob) tarayıcı algılama kodu aracılığıyla `None` kaçınılmaz. MSAL, ADAL veya kullandığınız herhangi bir kitaplığı kullanarak Safari 12, Safari 13 ve WebKit tabanlı işletim sistemi stili oturum açma stilini test edin. Sorun, temel alınan işletim sistemi sürümüne bağımlıdır. OSX Mojave (10,14) ve iOS 12 ' nin yeni SameSite davranışıyla uyumluluk sorunlarına sahip olduğu bilinmektedir. İşletim sistemini OSX Catalina (10,15) veya iOS 13 ' e yükseltmek sorunu düzeltir. Safari 'nin şu anda yeni belirtim davranışını test etmek için bir katılım bayrağı yoktur.

### <a name="test-with-firefox"></a>Firefox ile test etme

Yeni standart için Firefox desteği, `about:config` sayfasında özellik `network.cookie.sameSite.laxByDefault`bayrağıyla birlikte seçerek 68 + sürümü üzerinde test edilebilir. Daha eski Firefox sürümleriyle uyumluluk sorunları hakkında rapor yoktu.

### <a name="test-with-edge-browser"></a>Edge tarayıcısı ile test

Edge, eski SameSite standardını destekler. Edge sürüm 44, yeni standart ile bilinen uyumluluk sorunlarına sahip değildir.

### <a name="test-with-edge-chromium"></a>Edge ile test (Kmıum)

`edge://flags/#same-site-by-default-cookies` sayfasında SameSite bayrakları ayarlanır. Edge Kmıum ile hiçbir uyumluluk sorunu bulunmadı.

### <a name="test-with-electron"></a>Elektron ile test

Elektron sürümleri, daha eski bir Kmıum sürümlerini içerir. Örneğin, takımlar tarafından kullanılan elektron sürümü, eski davranışı gösteren Kmıum 66 ' dir. Ürününüzün kullandığı elektron sürümüyle kendi uyumluluk testinizi gerçekleştirmeniz gerekir. Aşağıdaki bölümde [daha eski tarayıcıları destekleme](#sob) bölümüne bakın.

## <a name="additional-resources"></a>Ek kaynaklar

* [ASP.NET ve ASP.NET Core yaklaşan SameSite tanımlama bilgisi değişiklikleri](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Kmıum blogu: geliştiriciler: yeni SameSite için hazırlanın = yok; Güvenli tanımlama bilgisi ayarları](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Aynı şekilde açıklanan SameSite tanımlama bilgileri](https://web.dev/samesite-cookies-explained/)
