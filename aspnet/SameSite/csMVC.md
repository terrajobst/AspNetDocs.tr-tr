---
title: ASP.NET 4.7.2 C# MVC Için SameSite tanımlama bilgisi örneği
author: blowdart
description: ASP.NET 4.7.2 C# MVC Için SameSite tanımlama bilgisi örneği
ms.author: riande
ms.date: 2/15/2019
uid: samesite/csMVC
ms.openlocfilehash: dcbd0bee009669fb747d74e6ccef07fbae70a236
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458457"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-mvc"></a><span data-ttu-id="b17bb-103">ASP.NET 4.7.2 C# MVC Için SameSite tanımlama bilgisi örneği</span><span class="sxs-lookup"><span data-stu-id="b17bb-103">SameSite cookie sample for ASP.NET 4.7.2 C# MVC</span></span>

<span data-ttu-id="b17bb-104">.NET Framework 4,7, [SameSite](https://www.owasp.org/index.php/SameSite) özniteliği için yerleşik desteğe sahiptir, ancak özgün standarda uyar.</span><span class="sxs-lookup"><span data-stu-id="b17bb-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="b17bb-105">Düzeltme eki uygulanmış davranış, değeri bir `None`bir değere yaymaması yerine, özniteliği bir değeri olarak göstermek için `SameSite.None` anlamını değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="b17bb-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="b17bb-106">Değeri göstermek istiyorsanız, bir tanımlama bilgisinde `SameSite` özelliğini-1 olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b17bb-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="b17bb-107">SameSite özniteliği yazılıyor</span><span class="sxs-lookup"><span data-stu-id="b17bb-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="b17bb-108">Aşağıda, bir tanımlama bilgisine bir SameSite özniteliği yazma örneği verilmiştir;</span><span class="sxs-lookup"><span data-stu-id="b17bb-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookieSite none.
// Note this will also require you to be running on HTTPS
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for Same
sameSiteCookie.Secure = true;

// Set the cookie to HTTP only which is good practice unless you really do need
// to access it client side in scripts.
sameSiteCookie.HttpOnly = true;

// Add the SameSite attribute, this will emit the attribute with a value of none.
// To not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None;

// Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie);
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="b17bb-109">Oturum durumu için varsayılan sameSite özniteliği, `web.config` oturum ayarlarının ' tanımlama bilgisi Esamesitesi ' parametresinde ayarlanır</span><span class="sxs-lookup"><span data-stu-id="b17bb-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="b17bb-110">MVC kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b17bb-110">MVC Authentication</span></span>

<span data-ttu-id="b17bb-111">OWIN MVC tanımlama bilgisi tabanlı kimlik doğrulaması, tanımlama bilgisi özniteliklerinin değiştirilmesini sağlamak için bir tanımlama bilgisi Yöneticisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="b17bb-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="b17bb-112">[SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs) , bu tür bir sınıfın, kendi projelerinize kopyalayabileceği bir uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="b17bb-112">The [SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="b17bb-113">Microsoft. Owin bileşenlerinizin 4.1.0 veya üzeri sürüme yükseltildiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b17bb-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="b17bb-114">Örneğin tüm sürüm numaralarının eşleştiğinden emin olmak için `packages.config` dosyanızı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b17bb-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <!-- other packages -->
  <package id="Microsoft.Owin.Host.SystemWeb" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security.Cookies" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net472" />
  <package id="Owin" version="1.0" targetFramework="net472" />
</packages>
```

<span data-ttu-id="b17bb-115">Daha sonra kimlik doğrulama bileşenleri, başlangıç sınıfınıza ilişkin bir IEManager 'ı kullanacak şekilde yapılandırılmalıdır;</span><span class="sxs-lookup"><span data-stu-id="b17bb-115">The authentication components must then be configured to use the CookieManager in your startup class;</span></span>

```c#
public void Configuration(IAppBuilder app)
{
    app.UseCookieAuthentication(new CookieAuthenticationOptions
    {
        CookieSameSite = SameSiteMode.None,
        CookieHttpOnly = true,
        CookieSecure = CookieSecureOption.Always,
        CookieManager = new SameSiteCookieManager(new SystemWebCookieManager())
    });
}
```

<span data-ttu-id="b17bb-116">Bunu destekleyen *her* bir bileşen için bir tanımlama bilgisi Yöneticisi ayarlanmalıdır; bu, ıeauthentication ve Openıdconnectauthentication bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b17bb-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="b17bb-117">Yanıt tanımlama bilgisi tümleştirmesiyle ilgili [bilinen sorunlardan](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) kaçınmak Için Systemwebcookie IEManager kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b17bb-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="b17bb-118">Örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b17bb-118">Running the sample</span></span>

<span data-ttu-id="b17bb-119">Örnek projeyi çalıştırırsanız, ilk sayfada tarayıcı hata ayıklayıcıyı yükleyin ve site için tanımlama bilgisi toplamasını görüntülemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b17bb-119">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="b17bb-120">Bunu kenar ve Chrome 'a bas `F12` için `Application` sekmesini seçin ve `Storage` bölümündeki `Cookies` seçeneğinin altındaki site URL 'sine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b17bb-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![Tarayıcı hata ayıklayıcısı tanımlama bilgisi listesi](sample/img/BrowserDebugger.png)

<span data-ttu-id="b17bb-122">"Tanımlama bilgileri oluştur" düğmesine tıkladığınızda örnek tarafından oluşturulan tanımlama bilgisinin, [örnek kodda](#sampleCode)ayarlanan değerle eşleşen `Lax`bir SameSite özniteliği değerine sahip olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b17bb-122">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="b17bb-123">Denetleyeistemediğiniz tanımlama bilgilerini kesintiye uğratan</span><span class="sxs-lookup"><span data-stu-id="b17bb-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="b17bb-124">.NET 4.5.2, `Response.AddOnSendingHeaders`üstbilgilerin yazılmasını kesintiye uğratan yeni bir olay sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="b17bb-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="b17bb-125">Bu, tanımlama bilgilerini istemci makinesine döndürülmeden önce ele almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b17bb-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="b17bb-126">Örnekte, tarayıcının yeni sameSite değişikliklerini destekleyip desteklemediğini kontrol eden bir statik yönteme yönelik olarak, yeni `None` değeri ayarlanmışsa, tanımlama bilgilerini özniteliği göstermeme olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b17bb-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="b17bb-127">Olayı işleme bir [örnek için bkz](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) [. Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) , ve kendi kodunuza kopyalayabileceğiniz tanımlama bilgisi `sameSite` özniteliğini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="b17bb-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```c#
public static void FilterSameSiteNoneForIncompatibleUserAgents(object sender)
{
    HttpApplication application = sender as HttpApplication;
    if (application != null)
    {
        var userAgent = application.Context.Request.UserAgent;
        if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
        {
            HttpContext.Current.Response.AddOnSendingHeaders(context =>
            {
                var cookies = context.Response.Cookies;
                for (var i = 0; i < cookies.Count; i++)
                {
                    var cookie = cookies[i];
                    if (cookie.SameSite == SameSiteMode.None)
                    {
                        cookie.SameSite = (SameSiteMode)(-1); // Unspecified
                    }
                }
            });
        }
    }
}
```

<span data-ttu-id="b17bb-128">Belirli bir adlandırılmış tanımlama bilgisi davranışını çok aynı şekilde değiştirebilirsiniz; Aşağıdaki örnek, `Lax` varsayılan kimlik doğrulama tanımlama bilgisini `None` değerini destekleyen tarayıcılarda `None` olarak ayarlayın veya `None`desteklemeyen tarayıcılarda sameSite özniteliğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="b17bb-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```c#
public static void AdjustSpecificCookieSettings()
{
    HttpContext.Current.Response.AddOnSendingHeaders(context =>
    {
        var cookies = context.Response.Cookies;
        for (var i = 0; i < cookies.Count; i++)
        {
            var cookie = cookies[i]; 
            // Forms auth: ".ASPXAUTH"
            // Session: "ASP.NET_SessionId"
            if (string.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal))
            { 
                if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
                {
                    cookie.SameSite = -1;
                }
                else
                {
                    cookie.SameSite = SameSiteMode.None;
                }
                cookie.Secure = true;
            }
        }
    });
}
```

### <a name="more-information"></a><span data-ttu-id="b17bb-129">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="b17bb-129">More Information</span></span>
 
[<span data-ttu-id="b17bb-130">Chrome güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="b17bb-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="b17bb-131">OWıN SameSite belgeleri</span><span class="sxs-lookup"><span data-stu-id="b17bb-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="b17bb-132">ASP.NET belgeleri</span><span class="sxs-lookup"><span data-stu-id="b17bb-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="b17bb-133">.NET SameSite yamaları</span><span class="sxs-lookup"><span data-stu-id="b17bb-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)