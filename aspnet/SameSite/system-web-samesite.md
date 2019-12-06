---
title: ASP.NET içinde SameSite tanımlama bilgileriyle çalışma
author: rick-anderson
description: ASP.NET içindeki site tanımlama bilgilerini nasıl kullanacağınızı öğrenin
ms.author: riande
ms.date: 12/03/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 40e5c13b6834912c13b41cbfad7da8cd84ca6c8b
ms.sourcegitcommit: 969e7db924ebad3cc0f0cb0d65d148e8b9221b9a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/06/2019
ms.locfileid: "74902026"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>ASP.NET içinde SameSite tanımlama bilgileriyle çalışma

Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite, siteler arası istek sahteciliği (CSRF) saldırılarına karşı bir koruma sağlamak için tasarlanmış bir [IETF](https://ietf.org/about/) taslağının olması. [SameSite 2019 taslağı](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):

* Tanımlama bilgilerini varsayılan olarak `SameSite=Lax` olarak değerlendirir.
* Siteler arası teslimin etkinleştirilmesi için `SameSite=None` açıkça onaylama tanımlama bilgileri `Secure`olarak işaretlenmelidir.

`Lax` çoğu uygulama tanımlama bilgisi için geçerlidir. [OpenID Connect](https://openid.net/connect/) (OIDC) ve [WS-Federation](https://auth0.com/docs/protocols/ws-fed) gibi bazı kimlik doğrulama biçimlerinden bırı, temel yönlendirmeye gönderi sağlar. POST tabanlı yeniden yönlendirmeler, SameSite tarayıcı korumalarının tetiklenmesi, bu nedenle bu bileşenler için SameSite devre dışı bırakıldı. Çoğu [OAuth](https://oauth.net/) oturum açma, istek akışının farklılığı nedeniyle etkilenmez.

`None` parametresi, önceki [2016 taslak standardını](https://tools.ietf.org/html/draft-west-first-party-cookies-07) uygulayan istemcilerle uyumluluk sorunlarına neden olur (örneğin, iOS 12). Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .

Tanımlama bilgilerini gösteren her bir ASP.NET Core bileşeni, SameSite ' ın uygun olup olmadığına karar vermeniz gerekir.

## <a name="api-usage-with-samesite"></a>SameSite ile API kullanımı

Bkz [. HttpCookie. SameSite özelliği](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)

## <a name="history-and-changes"></a>Geçmiş ve değişiklikler

SameSite desteği ilk olarak .NET 4.7.2 'de [2016 taslak standardı](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)kullanılarak uygulanmıştır.

19 Kasım 2019, 2016 standardı ile 2019 standardına kadar, Windows için Kasım ' i güncelleştirme. Diğer Windows sürümlerine ek güncelleştirmeler geliyor. Daha fazla bilgi için aşağıdaki KB 'ye bakın:

* [KB makalesi 4531182](https://support.microsoft.com/help/4531182/kb4531182)
* [KB makalesi 4524421](https://support.microsoft.com/help/4524421/kb4524421)

 SameSite belirtiminin 2019 taslağı:

* , 2016 taslağı ile geriye dönük olarak uyumlu **değildir** . Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.
* Tanımlama bilgilerinin varsayılan olarak `SameSite=Lax` olarak değerlendirilip değerlendirilmediğini belirtir.
* Siteler arası teslimin etkinleştirilmesi için `SameSite=None` açıkça onaylama tanımlama bilgilerini belirtir `Secure`olarak işaretlenmelidir. `None`, kabul etmek için yeni bir giriştir.
* Yukarıda listelenen BB 'de açıklandığı şekilde verilen düzeltme ekleri tarafından desteklenir.
* , [Şubat 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)' de varsayılan olarak [Chrome](https://chromestatus.com/feature/5088147346030592) tarafından etkinleştirilmek üzere zamanlanır. Tarayıcılar 2019 içinde bu standarda geçmeyi başlattı.

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

* [Kmıum blogu: geliştiriciler: yeni SameSite için hazırlanın = yok; Güvenli tanımlama bilgisi ayarları](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Aynı şekilde açıklanan SameSite tanımlama bilgileri](https://web.dev/samesite-cookies-explained/)
