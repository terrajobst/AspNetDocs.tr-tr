---
title: ASP.NET içinde SameSite tanımlama bilgileriyle çalışma
author: rick-anderson
description: ASP.NET içindeki site tanımlama bilgilerini nasıl kullanacağınızı öğrenin
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 7987a5d6c9b3a82679d42a2d381d471d56f495c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546748"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="b357b-103">ASP.NET içinde SameSite tanımlama bilgileriyle çalışma</span><span class="sxs-lookup"><span data-stu-id="b357b-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="b357b-104">Gönderen [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b357b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b357b-105">SameSite, siteler arası istek sahteciliği (CSRF) saldırılarına karşı bir koruma sağlamak için tasarlanmış bir [IETF](https://ietf.org/about/) taslak standardıdır.</span><span class="sxs-lookup"><span data-stu-id="b357b-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="b357b-106">[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)içinde orijinal drafted, taslak standart [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)' de güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="b357b-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="b357b-107">Güncelleştirilmiş standart, önceki standartlarla geriye dönük olarak uyumlu değildir ve aşağıdakiler en belirgin farklılıklardır:</span><span class="sxs-lookup"><span data-stu-id="b357b-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="b357b-108">SameSite üst bilgisi olmayan tanımlama bilgileri varsayılan olarak `SameSite=Lax` olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="b357b-109">`SameSite=None` siteler arası tanımlama bilgisi kullanımına izin vermek için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b357b-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="b357b-110">`SameSite=None` onayı olan tanımlama bilgileri ayrıca `Secure`olarak işaretlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="b357b-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="b357b-111">[`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) kullanan uygulamalar, `<iframe>` siteler arası senaryolar olarak değerlendirildiğinden `sameSite=Lax` veya `sameSite=Strict` tanımlama bilgileri ile ilgili sorunlarla karşılaşabilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-111">Applications that use [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) may experience issues with `sameSite=Lax` or `sameSite=Strict` cookies because `<iframe>` is treated as cross-site scenarios.</span></span>
* <span data-ttu-id="b357b-112">`SameSite=None` değere [2016 standart](https://tools.ietf.org/html/draft-west-first-party-cookies-07) izin verilmez ve bazı uygulamaların bu tür tanımlama bilgilerini `SameSite=Strict`olarak ele almasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b357b-112">The value `SameSite=None` is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as `SameSite=Strict`.</span></span> <span data-ttu-id="b357b-113">Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .</span><span class="sxs-lookup"><span data-stu-id="b357b-113">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="b357b-114">`SameSite=Lax` ayarı çoğu uygulama tanımlama bilgisi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b357b-114">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="b357b-115">[OpenID Connect](https://openid.net/connect/) (OIDC) ve [WS-Federation](https://auth0.com/docs/protocols/ws-fed) gibi bazı kimlik doğrulama biçimlerinden bırı, temel yönlendirmeye gönderi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b357b-115">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="b357b-116">POST tabanlı yeniden yönlendirmeler, SameSite tarayıcı korumalarının tetiklenmesi, bu nedenle bu bileşenler için SameSite devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="b357b-116">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="b357b-117">Çoğu [OAuth](https://oauth.net/) oturum açma, istek akışının farklılığı nedeniyle etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="b357b-117">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="b357b-118">Tanımlama bilgilerini veren her ASP.NET bileşeni, SameSite ' ın uygun olup olmadığına karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b357b-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="b357b-119">2019 .net SameSite güncelleştirmelerini yükledikten sonra uygulamalarla ilgili sorunların [bilinen sorunları](#known) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b357b-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="b357b-120">ASP.NET 4.7.2 ve 4,8 ' de SameSite kullanma</span><span class="sxs-lookup"><span data-stu-id="b357b-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="b357b-121">.NET 4.7.2 ve 4,8 Aralık 2019 ' de güncelleştirmelerin yayımlanmasından bu yana SameSite için [2019 taslak standardını](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) destekler.</span><span class="sxs-lookup"><span data-stu-id="b357b-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="b357b-122">Geliştiriciler [HttpCookie. SameSite özelliğini](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)kullanarak SameSite üst bilgisinin değerini programlı bir şekilde denetleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="b357b-123">`SameSite` özelliğini `Strict`, `Lax`veya `None` olarak ayarlamak, bu değerlerin tanımlama bilgisiyle ağ üzerinde yazılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b357b-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="b357b-124">`(SameSiteMode)(-1)` değerine eşit ayarı, tanımlama bilgisine sahip ağa hiçbir SameSite üstbilgisinin ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b357b-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="b357b-125">[HttpCookie. Secure özelliği](/dotnet/api/system.web.httpcookie.secure)veya yapılandırma dosyalarındaki ' RequireSSL ', tanımlama bilgisini `Secure` olarak işaretlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="b357b-126">Yeni `HttpCookie` örnekleri `SameSite=(SameSiteMode)(-1)` ve `Secure=false`varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b357b-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="b357b-127">Bu varsayılanlar, `system.web/httpCookies` yapılandırma bölümünde geçersiz kılınabilir, burada dize `"Unspecified"` `(SameSiteMode)(-1)`için yalnızca kolay bir yapılandırma sözdizimidir:</span><span class="sxs-lookup"><span data-stu-id="b357b-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="b357b-128">ASP.Net Ayrıca, bu özellikler için kendi kendine özgü dört tanımlama bilgisi verir: anonim kimlik doğrulaması, Forms kimlik doğrulaması, oturum durumu ve rol yönetimi.</span><span class="sxs-lookup"><span data-stu-id="b357b-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="b357b-129">Çalışma zamanında elde edilen bu tanımlama bilgilerinin örnekleri, diğer tüm HttpCookie örnekleri gibi `SameSite` ve `Secure` özellikleri kullanılarak değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="b357b-130">Ancak, aynı site standardının sürecinizin ortaya çıktı nedeniyle, bu dört özellik tanımlama bilgilerine yönelik yapılandırma seçenekleri tutarsız olur.</span><span class="sxs-lookup"><span data-stu-id="b357b-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="b357b-131">İlgili yapılandırma bölümleri ve öznitelikler, varsayılan olarak aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b357b-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="b357b-132">Bir özellik için `SameSite` veya `Secure` ilgili özniteliği yoksa, bu özellik yukarıda açıklanan `system.web/httpCookies` bölümünde yapılandırılan varsayılanlara geri döner.</span><span class="sxs-lookup"><span data-stu-id="b357b-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

<span data-ttu-id="b357b-133">**Note**: ' belirtilmemiş ' yalnızca şu anda `system.web/httpCookies@sameSite` kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="b357b-134">Gelecekteki güncelleştirmelerde daha önce gösterilen tanımlama bilgisi Esamesite özniteliklerine benzer bir sözdizimi eklemenizi umuyoruz.</span><span class="sxs-lookup"><span data-stu-id="b357b-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="b357b-135">Koddaki `(SameSiteMode)(-1)` ayarlanması bu tanımlama bilgilerinin örneklerinde hala geçerlidir. \*</span><span class="sxs-lookup"><span data-stu-id="b357b-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a><span data-ttu-id="b357b-136">.NET uygulamalarını yeniden hedefle</span><span class="sxs-lookup"><span data-stu-id="b357b-136">Retarget .NET apps</span></span>

<span data-ttu-id="b357b-137">.NET 4.7.2 veya üstünü hedeflemek için:</span><span class="sxs-lookup"><span data-stu-id="b357b-137">To target .NET 4.7.2 or later:</span></span>

* <span data-ttu-id="b357b-138">*Web. config* 'in aşağıdakileri içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="b357b-138">Ensure *web.config* contains the following:</span></span>  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  <span data-ttu-id="b357b-139">[.Net geçiş kılavuzunda](/dotnet/framework/migration-guide/) daha fazla ayrıntı vardır.</span><span class="sxs-lookup"><span data-stu-id="b357b-139">The [.NET Migration Guide](/dotnet/framework/migration-guide/) has more details.</span></span>

* <span data-ttu-id="b357b-140">Projedeki NuGet paketlerinin doğru çerçeve sürümüne hedeflenmiş olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b357b-140">Verify NuGet packages in the project are targeted at the correct framework version.</span></span> <span data-ttu-id="b357b-141">*Packages. config* dosyasını inceleyerek doğru Framework sürümünü doğrulayabilirsiniz, örneğin:</span><span class="sxs-lookup"><span data-stu-id="b357b-141">You can verify the correct framework version by examining the *packages.config* file, for example:</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  <span data-ttu-id="b357b-142">Önceki *Packages. config* dosyasında, `Microsoft.ApplicationInsights` paketi:</span><span class="sxs-lookup"><span data-stu-id="b357b-142">In the preceding *packages.config* file, the `Microsoft.ApplicationInsights` package:</span></span>
    * <span data-ttu-id="b357b-143">, .NET 4.5.1 'e yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="b357b-143">Is  targeted against .NET 4.5.1.</span></span>
    * <span data-ttu-id="b357b-144">Çerçeve hedefini hedefleyen güncelleştirilmiş bir paket varsa, `targetFramework` özniteliği `net472` olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-144">Should have its `targetFramework` attribute updated to `net472` if an updated package targeting your framework target exists.</span></span>

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a><span data-ttu-id="b357b-145">4\.7.2 'den önceki .NET sürümleri</span><span class="sxs-lookup"><span data-stu-id="b357b-145">.NET versions earlier than 4.7.2</span></span>

<span data-ttu-id="b357b-146">Microsoft, aynı-site tanımlama bilgisi özniteliğini yazmak için 4.7.2 'in daha düşük .NET sürümlerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="b357b-146">Microsoft does not support .NET versions lower that 4.7.2 for writing the same-site cookie attribute.</span></span> <span data-ttu-id="b357b-147">Şunları yapmak için güvenilir bir yol bulduk:</span><span class="sxs-lookup"><span data-stu-id="b357b-147">We have not found a reliable way to:</span></span>

* <span data-ttu-id="b357b-148">Özniteliğin tarayıcı sürümüne bağlı olarak doğru yazıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="b357b-148">Ensure the attribute is written correctly based on browser version.</span></span>
* <span data-ttu-id="b357b-149">Daha eski çerçeve sürümlerindeki kimlik doğrulama ve oturum tanımlama bilgilerini durdurur ve ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b357b-149">Intercept and adjust authentication and session cookies on older framework versions.</span></span>

### <a name="december-patch-behavior-changes"></a><span data-ttu-id="b357b-150">Aralık düzeltme eki davranış değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="b357b-150">December patch behavior changes</span></span>

<span data-ttu-id="b357b-151">.NET Framework için belirli davranış değişikliği `SameSite` özelliğin `None` değerini nasıl yorumlayacağını,:</span><span class="sxs-lookup"><span data-stu-id="b357b-151">The specific behavior change for .NET Framework is how the `SameSite` property interprets the `None` value:</span></span>

* <span data-ttu-id="b357b-152">Düzeltme ekinin önüne bir `None` değeri:</span><span class="sxs-lookup"><span data-stu-id="b357b-152">Before the patch a value of `None` meant:</span></span>
  * <span data-ttu-id="b357b-153">Özniteliği hiçbir şekilde gösterme.</span><span class="sxs-lookup"><span data-stu-id="b357b-153">Do not emit the attribute at all.</span></span>
* <span data-ttu-id="b357b-154">Düzeltme ekiyle sonra:</span><span class="sxs-lookup"><span data-stu-id="b357b-154">After the patch:</span></span>
  * <span data-ttu-id="b357b-155">`None`değeri, "özniteliği `None`bir değere yayma" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b357b-155">A value of `None`it means "Emit the attribute with a value of `None`".</span></span>
  * <span data-ttu-id="b357b-156">`(SameSiteMode)(-1)` `SameSite` değeri özniteliğin yayınlanmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b357b-156">A `SameSite` value of `(SameSiteMode)(-1)` causes the attribute not to be emitted.</span></span>

<span data-ttu-id="b357b-157">Form kimlik doğrulaması ve oturum durumu tanımlama bilgileri için varsayılan SameSite değeri `None` `Lax`olarak değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="b357b-157">The default SameSite value for forms authentication and session state cookies was changed from `None` to `Lax`.</span></span>

### <a name="summary-of-change-impact-on-browsers"></a><span data-ttu-id="b357b-158">Tarayıcılarda değişiklik etkisinin Özeti</span><span class="sxs-lookup"><span data-stu-id="b357b-158">Summary of change impact on browsers</span></span>

<span data-ttu-id="b357b-159">Düzeltme ekini yükler ve `SameSite.None`bir tanımlama bilgisi verirseniz, iki işlemlerden biri gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="b357b-159">If you install the patch and issue a cookie with `SameSite.None`, one of two things will happen:</span></span>
* <span data-ttu-id="b357b-160">Chrome V80, bu tanımlama bilgisini yeni uygulamaya göre değerlendirir ve tanımlama bilgisinde aynı site kısıtlamalarını zorlamayacaktır.</span><span class="sxs-lookup"><span data-stu-id="b357b-160">Chrome v80 will treat this cookie according to the new implementation, and not enforce same site restrictions on the cookie.</span></span>
* <span data-ttu-id="b357b-161">Yeni uygulamayı destekleyecek şekilde güncelleştirilmemiş herhangi bir tarayıcı eski uygulamayı takip edecektir.</span><span class="sxs-lookup"><span data-stu-id="b357b-161">Any browser that has not been updated to support the new implementation will follow the old implementation.</span></span> <span data-ttu-id="b357b-162">Eski uygulama şöyle diyor:</span><span class="sxs-lookup"><span data-stu-id="b357b-162">The old implementation says:</span></span>
  * <span data-ttu-id="b357b-163">Anladığınızı bir değer görürseniz, bunu yoksayın ve katı aynı site kısıtlamalarına geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="b357b-163">If you see a value you don't understand, ignore it and switch to strict same site restrictions.</span></span>

<span data-ttu-id="b357b-164">Böylece uygulama Chrome 'da kesilir veya çok sayıda başka yerde de kesintiye uğratır.</span><span class="sxs-lookup"><span data-stu-id="b357b-164">So either the app breaks in Chrome, or you break in numerous other places.</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="b357b-165">Geçmiş ve değişiklikler</span><span class="sxs-lookup"><span data-stu-id="b357b-165">History and changes</span></span>

<span data-ttu-id="b357b-166">SameSite desteği ilk olarak .NET 4.7.2 'de [2016 taslak standardı](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)kullanılarak uygulanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b357b-166">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="b357b-167">19 Kasım 2019, 2016 standardı ile 2019 standardına kadar, Windows için Kasım ' i güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="b357b-167">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="b357b-168">Diğer Windows sürümlerine ek güncelleştirmeler geliyor.</span><span class="sxs-lookup"><span data-stu-id="b357b-168">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="b357b-169">Daha fazla bilgi için bkz. <xref:samesite/kbs-samesite>.</span><span class="sxs-lookup"><span data-stu-id="b357b-169">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="b357b-170">SameSite belirtiminin 2019 taslağı:</span><span class="sxs-lookup"><span data-stu-id="b357b-170">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="b357b-171">, 2016 taslağı ile geriye dönük olarak uyumlu **değildir** .</span><span class="sxs-lookup"><span data-stu-id="b357b-171">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="b357b-172">Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b357b-172">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="b357b-173">Tanımlama bilgilerinin varsayılan olarak `SameSite=Lax` olarak değerlendirilip değerlendirilmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b357b-173">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="b357b-174">Siteler arası teslimin de `Secure`olarak işaretlenmesi için `SameSite=None` açıkça onaylama tanımlama bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b357b-174">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="b357b-175">Yukarıda listelenen BB 'de açıklandığı şekilde verilen düzeltme ekleri tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b357b-175">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="b357b-176">, [Şubat 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)' de varsayılan olarak [Chrome](https://chromestatus.com/feature/5088147346030592) tarafından etkinleştirilmek üzere zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="b357b-176">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="b357b-177">Tarayıcılar 2019 içinde bu standarda geçmeyi başlattı.</span><span class="sxs-lookup"><span data-stu-id="b357b-177">Browsers started moving to this standard in 2019.</span></span>

<a name="known"><a/>

## <a name="known-issues"></a><span data-ttu-id="b357b-178">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="b357b-178">Known Issues</span></span>

<span data-ttu-id="b357b-179">2016 ve 2019 taslak belirtimleri uyumlu olmadığından, Kasım 2019 .NET Framework güncelleştirmesi, kırılmaya neden olabilecek bazı değişiklikler sunar.</span><span class="sxs-lookup"><span data-stu-id="b357b-179">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="b357b-180">Oturum durumu ve Forms kimlik doğrulama tanımlama bilgileri artık ağa belirtilmemiş değil `Lax` olarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="b357b-180">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="b357b-181">Çoğu uygulama `SameSite=Lax` tanımlama bilgileriyle çalışırken, siteler arasında GÖNDERI yapan uygulamalar veya `iframe` kullanan uygulamalar, oturum durumu veya form yetkilendirme tanımlama bilgilerinin beklendiği şekilde kullanılmadığını bulabilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-181">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="b357b-182">Bu sorunu gidermek için, uygun yapılandırma bölümündeki `cookieSameSite` değerini daha önce anlatıldığı gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b357b-182">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="b357b-183">Artık kod veya yapılandırmada `SameSite=None` açıkça ayarlanmış olan HttpCookies, daha önce atlandığı halde bu değerin tanımlama bilgisiyle yazılmış olmasına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b357b-183">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="b357b-184">Bu, yalnızca 2016 taslak standardını destekleyen eski tarayıcılarla ilgili sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-184">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="b357b-185">`SameSite=None` tanımlama bilgileriyle 2019 taslak standardını destekleyen tarayıcıları hedeflerken, Ayrıca, `Secure` işaretlemeyi veya tanınmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b357b-185">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="b357b-186">`SameSite=None`yazmadan 2016 davranışına dönmek için `aspnet:SupressSameSiteNone=true`uygulama ayarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="b357b-186">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="b357b-187">Bunun, uygulamadaki tüm HttpCookies için uygulanacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b357b-187">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="b357b-188">Azure App Service — SameSite tanımlama bilgisi işleme</span><span class="sxs-lookup"><span data-stu-id="b357b-188">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="b357b-189">Azure App Service .NET 4.7.2 uygulamalarında SameSite davranışlarını yapılandırma hakkında bilgi için bkz. [Azure App Service — SameSite tanımlama bilgisi işleme ve .NET Framework 4.7.2 Patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .</span><span class="sxs-lookup"><span data-stu-id="b357b-189">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="b357b-190">Eski tarayıcıları destekleme</span><span class="sxs-lookup"><span data-stu-id="b357b-190">Supporting older browsers</span></span>

<span data-ttu-id="b357b-191">2016 SameSite Standard uygulanan, bilinmeyen değerlerin `SameSite=Strict` değer olarak değerlendirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="b357b-191">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="b357b-192">2016 SameSite standardını destekleyen eski tarayıcılardan erişilen uygulamalar, bir `None`değeri olan bir SameSite özelliği edindiklerinde kesintiye uğramayabilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-192">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="b357b-193">Web uygulamaları, eski tarayıcıları desteklemek istiyorlarsa, tarayıcı algılaması gerçekleştirmelidir.</span><span class="sxs-lookup"><span data-stu-id="b357b-193">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="b357b-194">ASP.NET tarayıcı algılamayı uygulamaz; çünkü kullanıcı aracıları değerleri yüksek ölçüde geçici ve sık sık değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-194">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span>

<span data-ttu-id="b357b-195">Microsoft 'un sorunu çözme yaklaşımı, tarayıcıyı desteklemez olarak bilindiğinde `sameSite=None` özniteliğini tanımlama bilgilerinden yürütmek için tarayıcı algılama bileşenleri uygulamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b357b-195">Microsoft's approach to fixing the problem is to help you implement browser detection components to strip the `sameSite=None` attribute from cookies if a browser is known to not support it.</span></span> <span data-ttu-id="b357b-196">Google 'ın önerisi, biri yeni özniteliğiyle, diğeri de özniteliği olmayan çift tanımlama bilgileri veriliydi.</span><span class="sxs-lookup"><span data-stu-id="b357b-196">Google's advice was to issue double cookies, one with the new attribute, and one without the attribute at all.</span></span> <span data-ttu-id="b357b-197">Bununla birlikte, Google 'ın öner, sınırlı olduğunu düşüntik.</span><span class="sxs-lookup"><span data-stu-id="b357b-197">However we consider Google's advice limited.</span></span> <span data-ttu-id="b357b-198">Bazı tarayıcılar, özellikle de mobil tarayıcılar bir sitenin tanımlama bilgisi sayısı veya bir etki alanı adı için çok küçük sınırlara sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b357b-198">Some browsers, especially mobile browsers have very small limits on the number of cookies a site, or a domain name can send.</span></span> <span data-ttu-id="b357b-199">Birden çok tanımlama bilgisi gönderdiğinizde, özellikle kimlik doğrulama tanımlama bilgileri gibi büyük tanımlama bilgileri mobil tarayıcı sınırına çok hızlı ulaşabilir ve bu da tanılama ve düzeltilmesi zor olan uygulama arızalarına yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-199">Sending multiple cookies, especially large cookies like authentication cookies can reach the mobile browser limit very quickly, causing app failures that are hard to diagnose and fix.</span></span> <span data-ttu-id="b357b-200">Framework 'ün yanı sıra, bir çift tanımlama bilgisi yaklaşımı kullanmak üzere güncelleştirilemeyebilir üçüncü taraf kodu ve bileşenleri büyük bir ekosistemi vardır.</span><span class="sxs-lookup"><span data-stu-id="b357b-200">Furthermore as a framework there is a large ecosystem of third party code and components that may not be updated to use a double cookie approach.</span></span>

<span data-ttu-id="b357b-201">[Bu GitHub deposundaki]() örnek projelerde kullanılan tarayıcı algılama kodu iki dosyada bulunuyor</span><span class="sxs-lookup"><span data-stu-id="b357b-201">The browser detection code used in the sample projects in [this GitHub repository]() is contained in two files</span></span>

* [<span data-ttu-id="b357b-202">C#SameSiteSupport.cs</span><span class="sxs-lookup"><span data-stu-id="b357b-202">C# SameSiteSupport.cs</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [<span data-ttu-id="b357b-203">VB SameSiteSupport. vb</span><span class="sxs-lookup"><span data-stu-id="b357b-203">VB SameSiteSupport.vb</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

<span data-ttu-id="b357b-204">Bu algılamalar, 2016 standardını desteklediğimiz ve özniteliği tamamen kaldırılması gereken en yaygın tarayıcı aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="b357b-204">These detections are the most common browser agents we have seen that support the 2016 standard and for which the attribute needs to be completely removed.</span></span> <span data-ttu-id="b357b-205">Bu, tamamen uygulama olarak tasarlanmamıştır:</span><span class="sxs-lookup"><span data-stu-id="b357b-205">It isn't meant as a complete implementation:</span></span>

* <span data-ttu-id="b357b-206">Uygulamanız, test sitemizdeki tarayıcıları görebilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-206">Your app may see browsers that our test sites do not.</span></span>
* <span data-ttu-id="b357b-207">Ortamınız için gereken algılamaları eklemeye hazır olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b357b-207">You should be prepared to add detections as necessary for your environment.</span></span>

<span data-ttu-id="b357b-208">Algılama işleminin nasıl yapılacağı, .NET ve kullanmakta olduğunuz Web çerçevesinin sürümüne göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="b357b-208">How you wire up the detection varies according the version of .NET and the web framework that you are using.</span></span> <span data-ttu-id="b357b-209">Aşağıdaki kod [HttpCookie](/dotnet/api/system.web.httpcookie) çağrı sitesinde çağrılabilir:</span><span class="sxs-lookup"><span data-stu-id="b357b-209">The following code can be called at the [HttpCookie](/dotnet/api/system.web.httpcookie) call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="b357b-210">Aşağıdaki ASP.NET 4.7.2 SameSite tanımlama bilgisi konularına bakın:</span><span class="sxs-lookup"><span data-stu-id="b357b-210">See the following ASP.NET 4.7.2 SameSite cookie topics:</span></span>

* [<span data-ttu-id="b357b-211">C#MVC</span><span class="sxs-lookup"><span data-stu-id="b357b-211">C# MVC</span></span>](xref:samesite/csMVC)
* [<span data-ttu-id="b357b-212">C#Formlarına</span><span class="sxs-lookup"><span data-stu-id="b357b-212">C# WebForms</span></span>](xref:samesite/CSharpWebForms)
* [<span data-ttu-id="b357b-213">VB WebForms</span><span class="sxs-lookup"><span data-stu-id="b357b-213">VB WebForms</span></span>](xref:samesite/vbWF)
* [<span data-ttu-id="b357b-214">VB MVC</span><span class="sxs-lookup"><span data-stu-id="b357b-214">VB MVC</span></span>](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a><span data-ttu-id="b357b-215">Sitenizin HTTPS 'ye yönlendirilmesini sağlama</span><span class="sxs-lookup"><span data-stu-id="b357b-215">Ensuring your site redirects to HTTPS</span></span>

<span data-ttu-id="b357b-216">ASP.NET 4. x, WebForms ve MVC için [IIS 'nın URL yeniden yazma](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) özelliği tüm istekleri https 'ye yönlendirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-216">For ASP.NET 4.x, WebForms and MVC, [IIS's URL Rewrite](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) feature can be used to redirect all requests to HTTPS.</span></span> <span data-ttu-id="b357b-217">Aşağıdaki XML örnek bir kural göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="b357b-217">The following XML shows a sample rule:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="b357b-218">[IIS URL yeniden yazma](https://www.iis.net/downloads/microsoft/url-rewrite) 'nin şirket içi yüklemelerinde, yüklenmesi gerekebilecek isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="b357b-218">In on-premises installations of [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) is an optional feature that may need installing.</span></span>

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="b357b-219">SameSite sorunları için test uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b357b-219">Test apps for SameSite problems</span></span>

<span data-ttu-id="b357b-220">Uygulamanızı, destekettiğiniz tarayıcılarla test etmeniz ve tanımlama bilgilerini içeren senaryolarınız üzerinden gitmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b357b-220">You must test your app with the browsers you support and go through your scenarios that involve cookies.</span></span> <span data-ttu-id="b357b-221">Tanımlama bilgisi senaryoları genellikle şunları içerir</span><span class="sxs-lookup"><span data-stu-id="b357b-221">Cookie scenarios typically involve</span></span>

* <span data-ttu-id="b357b-222">Oturum açma formları</span><span class="sxs-lookup"><span data-stu-id="b357b-222">Login forms</span></span>
* <span data-ttu-id="b357b-223">Facebook, Azure AD, OAuth ve OıDC gibi dış oturum açma mekanizmaları</span><span class="sxs-lookup"><span data-stu-id="b357b-223">External login mechanisms such as Facebook, Azure AD, OAuth and OIDC</span></span>
* <span data-ttu-id="b357b-224">Diğer sitelerden gelen istekleri kabul eden sayfalar</span><span class="sxs-lookup"><span data-stu-id="b357b-224">Pages that accept requests from other sites</span></span>
* <span data-ttu-id="b357b-225">Uygulamanızdaki iframe 'lere katıştırılacak şekilde tasarlanan sayfalar</span><span class="sxs-lookup"><span data-stu-id="b357b-225">Pages in your app designed to be embedded in iframes</span></span>

<span data-ttu-id="b357b-226">Tanımlama bilgilerinin uygulamanızda oluşturulduğunu, kalıcı olduğunu ve doğru şekilde silindiğini denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b357b-226">You should check that cookies are created, persisted and deleted correctly in your app.</span></span>

<span data-ttu-id="b357b-227">Üçüncü taraf oturum açma bilgileri gibi uzak sitelerle etkileşim kuran uygulamalar şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="b357b-227">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="b357b-228">Etkileşimi birden çok tarayıcıda test edin.</span><span class="sxs-lookup"><span data-stu-id="b357b-228">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="b357b-229">[Tarayıcı algılamasını ve](#sob) bu belgede açıklanan risk azaltma işlemini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b357b-229">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="b357b-230">Yeni SameSite davranışını kabul edebilir bir istemci sürümünü kullanarak Web uygulamalarını test edin.</span><span class="sxs-lookup"><span data-stu-id="b357b-230">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="b357b-231">Chrome, Firefox ve Kmıum Edge tümünde test için kullanılabilecek yeni bir katılım özelliği bayrakları vardır.</span><span class="sxs-lookup"><span data-stu-id="b357b-231">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="b357b-232">Uygulamanız SameSite düzeltme eklerini uyguladıktan sonra, daha eski istemci sürümleriyle test edin, özellikle Safari.</span><span class="sxs-lookup"><span data-stu-id="b357b-232">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="b357b-233">Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b357b-233">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="b357b-234">Chrome ile test etme</span><span class="sxs-lookup"><span data-stu-id="b357b-234">Test with Chrome</span></span>

<span data-ttu-id="b357b-235">Chrome 78 + bir yerde geçici bir risk azaltma yaptığından yanıltıcı sonuçlar verir.</span><span class="sxs-lookup"><span data-stu-id="b357b-235">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="b357b-236">Chrome 78 + geçici risk azaltma, iki dakikadan daha eski tanımlama bilgilerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="b357b-236">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="b357b-237">Uygun test bayraklarıyla etkin olan Chrome 76 veya 77 daha doğru sonuçlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b357b-237">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="b357b-238">Yeni SameSite davranışını test etmek için `chrome://flags/#same-site-by-default-cookies` **etkin**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b357b-238">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="b357b-239">Chrome 'un (75 ve üzeri) eski sürümleri, yeni `None` ayarı ile başarısız olarak bildirilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-239">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="b357b-240">Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .</span><span class="sxs-lookup"><span data-stu-id="b357b-240">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="b357b-241">Google, eski Chrome sürümlerini kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="b357b-241">Google does not make older chrome versions available.</span></span> <span data-ttu-id="b357b-242">Chrome 'un eski sürümlerini test etmek için [Kmıum indirme](https://www.chromium.org/getting-involved/download-chromium) bölümündeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="b357b-242">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="b357b-243">Chrome 'un eski sürümlerini arayarak sunulan bağlantılardan **Chrome indirmeyin** .</span><span class="sxs-lookup"><span data-stu-id="b357b-243">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="b357b-244">Kmıum 76 Win64</span><span class="sxs-lookup"><span data-stu-id="b357b-244">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="b357b-245">Kmıum 74 Win64</span><span class="sxs-lookup"><span data-stu-id="b357b-245">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* <span data-ttu-id="b357b-246">Windows 'un 64 bit sürümünü kullanmıyorsanız, [Kmahaproxy görüntüleyicisini](https://omahaproxy.appspot.com/) kullanarak kmıum dalının, [küzum tarafından sunulan yönergeleri](https://www.chromium.org/getting-involved/download-chromium)kullanarak Chrome 74 ' e (v 74.0.3729.108) karşılık geldiğini arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b357b-246">If you're not using a 64bit version of Windows you can use the [OmahaProxy viewer](https://omahaproxy.appspot.com/) to look up which Chromium branch corresponds to Chrome 74 (v74.0.3729.108) using the [instructions provided by Chromium](https://www.chromium.org/getting-involved/download-chromium).</span></span>

<span data-ttu-id="b357b-247">Canary sürüm `80.0.3975.0`başlayarak, LAX + geçici SONRASı hafifletme, devre dışı bırakılan özelliğin son bitiş durumunda siteler ve hizmetlerin test edilmesine izin vermek için yeni bayrak `--enable-features=SameSiteDefaultChecksMethodRigorously` kullanılarak test amacıyla etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-247">Starting in Canary version `80.0.3975.0`, the Lax+POST temporary mitigation can be disabled for testing purposes using the new flag `--enable-features=SameSiteDefaultChecksMethodRigorously` to allow testing of sites and services in the eventual end state of the feature where the mitigation has been removed.</span></span> <span data-ttu-id="b357b-248">Daha fazla bilgi için, bkz. Kmıum projeleri [SameSite Updates](https://www.chromium.org/updates/same-site)</span><span class="sxs-lookup"><span data-stu-id="b357b-248">For more information, see The Chromium Projects [SameSite Updates](https://www.chromium.org/updates/same-site)</span></span>

#### <a name="test-with-chrome-80"></a><span data-ttu-id="b357b-249">Chrome ile test 80 +</span><span class="sxs-lookup"><span data-stu-id="b357b-249">Test with Chrome 80+</span></span>

<span data-ttu-id="b357b-250">Yeni özniteliğini destekleyen Chrome 'un bir sürümünü [indirin](https://www.google.com/chrome/) .</span><span class="sxs-lookup"><span data-stu-id="b357b-250">[Download](https://www.google.com/chrome/) a version of Chrome that supports their new attribute.</span></span> <span data-ttu-id="b357b-251">Yazma sırasında, geçerli sürüm Chrome 80 ' dir.</span><span class="sxs-lookup"><span data-stu-id="b357b-251">At the time of writing, the current version is Chrome 80.</span></span> <span data-ttu-id="b357b-252">Chrome 80 ' in yeni davranışı kullanması için etkin `chrome://flags/#same-site-by-default-cookies` bayrağı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b357b-252">Chrome 80 needs the flag `chrome://flags/#same-site-by-default-cookies` enabled to use the new behavior.</span></span> <span data-ttu-id="b357b-253">Aynı zamanda, bir sameSite özniteliği etkin olmayan tanımlama bilgileri için yaklaşan davranışı test etmek üzere (`chrome://flags/#cookies-without-same-site-must-be-secure`) öğesini etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b357b-253">You should also enable (`chrome://flags/#cookies-without-same-site-must-be-secure`) to test the upcoming behavior for cookies which have no sameSite attribute enabled.</span></span> <span data-ttu-id="b357b-254">Chrome 80, anahtarın tanımlama bilgilerini öznitelik olmadan `SameSite=Lax`, belirli istekler için zaman aşımına uğramış bir yetkisiz kullanım süresi ile birlikte kabul etmek için hedefdir.</span><span class="sxs-lookup"><span data-stu-id="b357b-254">Chrome 80 is on target to make the switch to treat cookies without the attribute as `SameSite=Lax`, albeit with a timed grace period for certain requests.</span></span> <span data-ttu-id="b357b-255">Her zaman yetkisiz kullanım süresini devre dışı bırakmak için Chrome 80 aşağıdaki komut satırı bağımsız değişkeniyle başlatılabilir:</span><span class="sxs-lookup"><span data-stu-id="b357b-255">To disable the timed grace period Chrome 80 can be launched with the following command line argument:</span></span>

`--enable-features=SameSiteDefaultChecksMethodRigorously`

<span data-ttu-id="b357b-256">Chrome 80, tarayıcı konsolunda eksik olan sameSite öznitelikleri hakkında uyarı iletileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b357b-256">Chrome 80 has warning messages in the browser console about missing sameSite attributes.</span></span> <span data-ttu-id="b357b-257">Tarayıcı konsolunu açmak için F12 kullanın.</span><span class="sxs-lookup"><span data-stu-id="b357b-257">Use F12 to open the browser console.</span></span>

### <a name="test-with-safari"></a><span data-ttu-id="b357b-258">Safari ile test etme</span><span class="sxs-lookup"><span data-stu-id="b357b-258">Test with Safari</span></span>

<span data-ttu-id="b357b-259">Safari 12, önceki taslağı tamamen uyguladık ve yeni `None` değeri bir tanımlama bilgisinde olduğunda başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b357b-259">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="b357b-260">Bu belgede [eski tarayıcıları destekleyen](#sob) tarayıcı algılama kodu aracılığıyla `None` kaçınılmaz.</span><span class="sxs-lookup"><span data-stu-id="b357b-260">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="b357b-261">MSAL, ADAL veya kullandığınız herhangi bir kitaplığı kullanarak Safari 12, Safari 13 ve WebKit tabanlı işletim sistemi stili oturum açma stilini test edin.</span><span class="sxs-lookup"><span data-stu-id="b357b-261">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="b357b-262">Sorun, temel alınan işletim sistemi sürümüne bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="b357b-262">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="b357b-263">OSX Mojave (10,14) ve iOS 12 ' nin yeni SameSite davranışıyla uyumluluk sorunlarına sahip olduğu bilinmektedir.</span><span class="sxs-lookup"><span data-stu-id="b357b-263">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="b357b-264">İşletim sistemini OSX Catalina (10,15) veya iOS 13 ' e yükseltmek sorunu düzeltir.</span><span class="sxs-lookup"><span data-stu-id="b357b-264">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="b357b-265">Safari 'nin şu anda yeni belirtim davranışını test etmek için bir katılım bayrağı yoktur.</span><span class="sxs-lookup"><span data-stu-id="b357b-265">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="b357b-266">Firefox ile test etme</span><span class="sxs-lookup"><span data-stu-id="b357b-266">Test with Firefox</span></span>

<span data-ttu-id="b357b-267">Yeni standart için Firefox desteği, `about:config` sayfasında özellik `network.cookie.sameSite.laxByDefault`bayrağıyla birlikte seçerek 68 + sürümü üzerinde test edilebilir.</span><span class="sxs-lookup"><span data-stu-id="b357b-267">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="b357b-268">Daha eski Firefox sürümleriyle uyumluluk sorunları hakkında rapor yoktu.</span><span class="sxs-lookup"><span data-stu-id="b357b-268">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-legacy-browser"></a><span data-ttu-id="b357b-269">Edge (eski) tarayıcıyla test etme</span><span class="sxs-lookup"><span data-stu-id="b357b-269">Test with Edge (Legacy) browser</span></span>

<span data-ttu-id="b357b-270">Edge, eski SameSite standardını destekler.</span><span class="sxs-lookup"><span data-stu-id="b357b-270">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="b357b-271">Edge sürümü 44 +, yeni standart ile bilinen uyumluluk sorunlarına sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="b357b-271">Edge version 44+ doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="b357b-272">Edge ile test (Kmıum)</span><span class="sxs-lookup"><span data-stu-id="b357b-272">Test with Edge (Chromium)</span></span>

<span data-ttu-id="b357b-273">`edge://flags/#same-site-by-default-cookies` sayfasında SameSite bayrakları ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b357b-273">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="b357b-274">Edge Kmıum ile hiçbir uyumluluk sorunu bulunmadı.</span><span class="sxs-lookup"><span data-stu-id="b357b-274">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="b357b-275">Elektron ile test</span><span class="sxs-lookup"><span data-stu-id="b357b-275">Test with Electron</span></span>

<span data-ttu-id="b357b-276">Elektron sürümleri, daha eski bir Kmıum sürümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b357b-276">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="b357b-277">Örneğin, takımlar tarafından kullanılan elektron sürümü, eski davranışı gösteren Kmıum 66 ' dir.</span><span class="sxs-lookup"><span data-stu-id="b357b-277">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="b357b-278">Ürününüzün kullandığı elektron sürümüyle kendi uyumluluk testinizi gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b357b-278">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="b357b-279">Bkz. [eski tarayıcıları destekleme](#sob).</span><span class="sxs-lookup"><span data-stu-id="b357b-279">See [Supporting older browsers](#sob).</span></span>

## <a name="reverting-samesite-patches"></a><span data-ttu-id="b357b-280">SameSite yamaları geri alınıyor</span><span class="sxs-lookup"><span data-stu-id="b357b-280">Reverting SameSite patches</span></span>

<span data-ttu-id="b357b-281">.NET Framework uygulamalardaki güncelleştirilmiş sameSite davranışını bir `None`değeri için yayılmayan önceki davranışına geri döndürebilir ve değeri yaymayan kimlik doğrulama ve oturum tanımlama bilgilerini geri döndürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b357b-281">You can revert the updated sameSite behavior in .NET Framework apps to its previous behavior where the sameSite attribute is not emitted for a value of `None`, and revert the authentication and session cookies to not emit the value.</span></span> <span data-ttu-id="b357b-282">Bu, *son derece geçici bir çözüm*olarak görüntülenmelidir, çünkü Chrome değişiklikleri, standart değişiklikleri destekleyen tarayıcıları kullanan kullanıcılar için tüm dış post isteklerini veya kimlik doğrulamasını bozacaktır.</span><span class="sxs-lookup"><span data-stu-id="b357b-282">This should be viewed as an *extremely temporary fix*, as the Chrome changes will break any external POST requests or authentication for users using browsers which support the changes to the standard.</span></span>

### <a name="reverting-net-472-behavior"></a><span data-ttu-id="b357b-283">.NET 4.7.2 davranışını geri alma</span><span class="sxs-lookup"><span data-stu-id="b357b-283">Reverting .NET 4.7.2 behavior</span></span>

<span data-ttu-id="b357b-284">*Web. config dosyasını* aşağıdaki yapılandırma ayarlarını içerecek şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="b357b-284">Update *web.config* to include the following configuration settings:</span></span>

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a><span data-ttu-id="b357b-285">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b357b-285">Additional resources</span></span>

* [<span data-ttu-id="b357b-286">ASP.NET ve ASP.NET Core yaklaşan SameSite tanımlama bilgisi değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="b357b-286">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="b357b-287">Aynı-varsayılan ve "SameSite = none;. Güvenli "tanımlama bilgileri</span><span class="sxs-lookup"><span data-stu-id="b357b-287">Tips for testing and debugging SameSite-by-default and “SameSite=None; Secure” cookies</span></span>](https://www.chromium.org/updates/same-site/test-debug)
* [<span data-ttu-id="b357b-288">Kmıum blogu: geliştiriciler: yeni SameSite için hazırlanın = yok; Güvenli tanımlama bilgisi ayarları</span><span class="sxs-lookup"><span data-stu-id="b357b-288">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="b357b-289">Aynı şekilde açıklanan SameSite tanımlama bilgileri</span><span class="sxs-lookup"><span data-stu-id="b357b-289">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="b357b-290">Chrome güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="b357b-290">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)
* [<span data-ttu-id="b357b-291">.NET SameSite yamaları</span><span class="sxs-lookup"><span data-stu-id="b357b-291">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
* [<span data-ttu-id="b357b-292">Azure Web uygulamaları aynı site bilgileri</span><span class="sxs-lookup"><span data-stu-id="b357b-292">Azure Web Applications Same Site Information</span></span>](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [<span data-ttu-id="b357b-293">Azure ActiveDirectory aynı site bilgileri</span><span class="sxs-lookup"><span data-stu-id="b357b-293">Azure ActiveDirectory Same Site Information</span></span>](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
