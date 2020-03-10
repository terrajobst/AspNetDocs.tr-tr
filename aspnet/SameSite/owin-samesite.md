---
title: SameSite tanımlama bilgileriyle ve .NET için açık Web arabirimiyle çalışma (OWıN)
author: rick-anderson
description: SameSite tanımlama bilgileriyle ve .NET için açık Web arabirimiyle çalışma (OWıN)
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: a3353fd0f0332899aaba26b83aea0ff7c3a6d19b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546216"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a>.NET için SameSite tanımlama bilgileri ve açık Web arabirimi (OWıN)

Gönderen [Rick Anderson](https://twitter.com/RickAndMSFT)

`SameSite`, siteler arası istek sahteciliğini önleme (CSRF) saldırılarına karşı bir koruma sağlamak için tasarlanan bir [IETF](https://ietf.org/about/) taslağının olması. [SameSite 2019 taslağı](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):

* Tanımlama bilgilerini varsayılan olarak `SameSite=Lax` olarak değerlendirir.
* Siteler arası teslimin etkinleştirilmesi için `SameSite=None` açıkça onaylama tanımlama bilgileri `Secure`olarak işaretlenmelidir.

`Lax` çoğu uygulama tanımlama bilgisi için geçerlidir. [OpenID Connect](https://openid.net/connect/) (OIDC) ve [WS-Federation](https://auth0.com/docs/protocols/ws-fed) gibi bazı kimlik doğrulama biçimlerinden bırı, temel yönlendirmeye gönderi sağlar. POST tabanlı yeniden yönlendirmeler `SameSite` tarayıcı korumalarını tetikler; bu nedenle `SameSite` bu bileşenler için devre dışıdır. Çoğu [OAuth](https://oauth.net/) oturum açma, istek akışının farklılığı nedeniyle etkilenmemektedir. Tüm diğer bileşenler, varsayılan olarak **`SameSite` ayarlamayın ve** istemcilerin varsayılan davranışını (eski veya yeni) kullanır.

`None` parametresi, önceki [2016 taslak standardını](https://tools.ietf.org/html/draft-west-first-party-cookies-07) uygulayan istemcilerle uyumluluk sorunlarına neden olur (örneğin, iOS 12). Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .

Tanımlama bilgilerini veren her bir OWıN bileşeni, `SameSite` uygun olup olmadığına karar vermeniz gerekir.

Bu makalenin ASP.NET 4. x sürümü için bkz. <xref:samesite/system-web-samesite>.

## <a name="api-usage-with-samesite"></a>SameSite ile API kullanımı

`Microsoft.Owin` kendi `SameSite` uygulamasına sahiptir:

* Bu, `System.Web`' deki birine doğrudan bağımlı değildir.
* `SameSite`, .NET 4,5 ve üzeri `Microsoft.Owin` paketleri tarafından tüm hedeflenebilir sürümleri üzerinde çalışmaktadır.
* Yalnızca [Systemwebpişirme IEManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) bileşeni, `System.Web` `HttpCookie` sınıfıyla doğrudan etkileşime girer.

`SystemWebCookieManager`, `SameSite` desteğini etkinleştirmek üzere .NET 4.7.2 `System.Web` API 'Lerine ve davranışı değiştirmek için düzeltme eklerine bağımlıdır.

`SystemWebCookieManager` kullanma nedenleri, [owın ve System. Web yanıt tanımlama bilgisi tümleştirme sorunları](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)içinde özetlenmiştir. `System.Web`üzerinde çalışırken `SystemWebCookieManager` önerilir.

Aşağıdaki kod, `Lax``SameSite` ayarlar:

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

Aşağıdaki API 'Ler `SameSite`kullanır:

* [Microsoft. Owin. SameSiteMode](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [Pişirme ıeoptions. SameSite](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* [Pişirme ıeauthenticationoptions sınıfı](/previous-versions/aspnet/dn385599(v%3Dvs.113)) <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [Pişirme ıeauthenticationoptions. tanımlama bilgisi Esamesitesi](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* [Iokıemanager](/previous-versions/aspnet/dn800238(v%3Dvs.113))
* [Systemwebtanıtım IEManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [Systemwebchunkingtarif IEManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [Pişirme ıeauthenticationoptions. pişirme Yöneticisi](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [Openıdconnectauthenticationoptions. tanımlama, IEManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a>Geçmiş ve değişiklikler

[Microsoft. Owin](https://www.nuget.org/packages/Microsoft.Owin/) [`SameSite` 2016 taslak standardını](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)hiçbir şekilde desteklemez.

[SameSite 2019 taslağı](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) için destek yalnızca `Microsoft.Owin` 4.1.0 ve üzeri sürümlerde kullanılabilir. Önceki sürümler için düzeltme eki yok.

`SameSite` belirtiminin 2019 taslağı:

* , 2016 taslağı ile geriye dönük olarak uyumlu **değildir** . Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.
* Tanımlama bilgilerinin varsayılan olarak `SameSite=Lax` olarak değerlendirilip değerlendirilmediğini belirtir.
* Siteler arası teslimin etkinleştirilmesi için `SameSite=None` açıkça onaylama tanımlama bilgilerini belirtir `Secure`olarak işaretlenmelidir. `None`, kabul etmek için yeni bir giriştir.
* , [Şubat 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)' de varsayılan olarak [Chrome](https://chromestatus.com/feature/5088147346030592) tarafından etkinleştirilmek üzere zamanlanır. Tarayıcılar 2019 içinde bu standarda geçmeyi başlattı.
* , BB makalelerinde açıklanan şekilde verilen düzeltme ekleri tarafından desteklenir. Daha fazla bilgi için bkz. <xref:samesite/kbs-samesite>.

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>Eski tarayıcıları destekleme

2016 `SameSite` standart uygulanan, bilinmeyen değerler `SameSite=Strict` değer olarak değerlendirilmelidir. 2016 `SameSite` standardını destekleyen eski tarayıcılardan erişilen uygulamalar, `None`değeriyle `SameSite` bir özellik edindiklerinde kesintiye uğramayabilir. Web uygulamaları, eski tarayıcıları desteklemek istiyorlarsa, tarayıcı algılaması gerçekleştirmelidir. ASP.NET tarayıcı algılamayı uygulamaz; çünkü kullanıcı aracıları değerleri yüksek ölçüde geçici ve sık sık değiştirilir. [Iokıemanager](/previous-versions/aspnet/dn800238(v%3Dvs.113)) 'daki bir uzantı noktası, kullanıcı aracısına özel mantık takmayı sağlar.
<!-- https://docs.microsoft.com/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

`Startup.Configuration`, aşağıdakine benzer bir kod ekleyin:

[!code-csharp[](sample/Startup1.cs?name=snippet)]

Yukarıdaki kod, .NET 4.7.2 veya üzeri `SameSite` Patch gerektirir.

Aşağıdaki kod, `SameSiteCookieManager`örnek bir uygulamasını gösterir:

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

Yukarıdaki örnekte, `DisallowsSameSiteNone` `CheckSameSite` yönteminde çağrılır. `DisallowsSameSiteNone`, Kullanıcı aracısının `SameSite` `None`desteklemediğini algılayan bir Kullanıcı yöntemidir:

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

Aşağıdaki kod bir örnek `DisallowsSameSiteNone` yöntemi gösterir:

> [!WARNING]
> Aşağıdaki kod yalnızca tanıtım amaçlıdır:
> * Tamamlanmış olarak düşünülmemelidir.
> * Korunmaz veya desteklenmez.

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>SameSite sorunları için test uygulamaları

Üçüncü taraf oturum açma bilgileri gibi uzak sitelerle etkileşim kuran uygulamalar şunlar gerekir:

* Etkileşimi birden çok tarayıcıda test edin.
* [Tarayıcı algılamasını ve](#sob) bu belgede açıklanan risk azaltma işlemini uygulayın.

Yeni `SameSite` davranışını kabul edebilir bir istemci sürümünü kullanarak Web uygulamalarını test edin. Chrome, Firefox ve Kmıum Edge tümünde test için kullanılabilecek yeni bir katılım özelliği bayrakları vardır. Uygulamanız `SameSite` düzeltme eklerini uyguladıktan sonra, daha eski istemci sürümleriyle test edin, özellikle Safari. Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.

### <a name="test-with-chrome"></a>Chrome ile test etme

Chrome 78 + bir yerde geçici bir risk azaltma yaptığından yanıltıcı sonuçlar verir. Chrome 78 + geçici risk azaltma, iki dakikadan daha eski tanımlama bilgilerine izin verir. Uygun test bayraklarıyla etkin olan Chrome 76 veya 77 daha doğru sonuçlar sağlar. Yeni `SameSite` davranışını test etmek için `chrome://flags/#same-site-by-default-cookies` **etkin**olarak değiştirin. Chrome 'un (75 ve üzeri) eski sürümleri, yeni `None` ayarı ile başarısız olarak bildirilir. Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .

Google, eski Chrome sürümlerini kullanılabilir hale getirir. Chrome 'un eski sürümlerini test etmek için [Kmıum indirme](https://www.chromium.org/getting-involved/download-chromium) bölümündeki yönergeleri izleyin. Chrome 'un eski sürümlerini arayarak sunulan bağlantılardan **Chrome indirmeyin** .

* [Kmıum 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Kmıum 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Safari ile test etme

Safari 12, önceki taslağı tamamen uyguladık ve yeni `None` değeri bir tanımlama bilgisinde olduğunda başarısız olur. Bu belgede [eski tarayıcıları destekleyen](#sob) tarayıcı algılama kodu aracılığıyla `None` kaçınılmaz. MSAL, ADAL veya kullandığınız herhangi bir kitaplığı kullanarak Safari 12, Safari 13 ve WebKit tabanlı işletim sistemi stili oturum açma stilini test edin. Sorun, temel alınan işletim sistemi sürümüne bağımlıdır. OSX Mojave (10,14) ve iOS 12 ' nin yeni `SameSite` davranışında uyumluluk sorunlarına sahip olduğu bilinmektedir. İşletim sistemini OSX Catalina (10,15) veya iOS 13 ' e yükseltmek sorunu düzeltir. Safari 'nin şu anda yeni belirtim davranışını test etmek için bir katılım bayrağı yoktur.

### <a name="test-with-firefox"></a>Firefox ile test etme

Yeni standart için Firefox desteği, `about:config` sayfasında özellik `network.cookie.sameSite.laxByDefault`bayrağıyla birlikte seçerek 68 + sürümü üzerinde test edilebilir. Daha eski Firefox sürümleriyle uyumluluk sorunları hakkında rapor yoktu.

### <a name="test-with-edge-browser"></a>Edge tarayıcısı ile test

Edge, eski `SameSite` standardını destekler. Edge sürüm 44, yeni standart ile bilinen uyumluluk sorunlarına sahip değildir.

### <a name="test-with-edge-chromium"></a>Edge ile test (Kmıum)

`SameSite` bayrakları `edge://flags/#same-site-by-default-cookies` sayfasında ayarlanır. Edge Kmıum ile hiçbir uyumluluk sorunu bulunmadı.

### <a name="test-with-electron"></a>Elektron ile test

Elektron sürümleri, daha eski bir Kmıum sürümlerini içerir. Örneğin, takımlar tarafından kullanılan elektron sürümü, eski davranışı gösteren Kmıum 66 ' dir. Ürününüzün kullandığı elektron sürümüyle kendi uyumluluk testinizi gerçekleştirmeniz gerekir. Aşağıdaki bölümde [daha eski tarayıcıları destekleme](#sob) bölümüne bakın.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kmıum blogu: geliştiriciler: yeni SameSite için hazırlanın = yok; Güvenli tanımlama bilgisi ayarları](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Aynı şekilde açıklanan SameSite tanımlama bilgileri](https://web.dev/samesite-cookies-explained/)
* [OWıN ve System. Web yanıt tanımlama bilgisi tümleştirme sorunları](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)
