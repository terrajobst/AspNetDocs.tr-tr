---
title: ASP.NET 4.7.2 VB WebForms için SameSite tanımlama bilgisi örneği
author: blowdart
description: ASP.NET 4.7.2 VB WebForms için SameSite tanımlama bilgisi örneği
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbWF
ms.openlocfilehash: 8979edecc5acf7dac81b9f53d31af00389f4727c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458443"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-webforms"></a><span data-ttu-id="256f8-103">ASP.NET 4.7.2 VB WebForms için SameSite tanımlama bilgisi örneği</span><span class="sxs-lookup"><span data-stu-id="256f8-103">SameSite cookie sample for ASP.NET 4.7.2 VB WebForms</span></span>
<span data-ttu-id="256f8-104">.NET Framework 4,7, [SameSite](https://www.owasp.org/index.php/SameSite) özniteliği için yerleşik desteğe sahiptir, ancak özgün standarda uyar.</span><span class="sxs-lookup"><span data-stu-id="256f8-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="256f8-105">Düzeltme eki uygulanmış davranış, değeri bir `None`bir değere yaymaması yerine, özniteliği bir değeri olarak göstermek için `SameSite.None` anlamını değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="256f8-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="256f8-106">Değeri göstermek istiyorsanız, bir tanımlama bilgisinde `SameSite` özelliğini-1 olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="256f8-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="256f8-107">SameSite özniteliği yazılıyor</span><span class="sxs-lookup"><span data-stu-id="256f8-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="256f8-108">Aşağıda, bir tanımlama bilgisine bir SameSite özniteliği yazma örneği verilmiştir;</span><span class="sxs-lookup"><span data-stu-id="256f8-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```vb
' Create the cookie
Dim sameSiteCookie As New HttpCookie("sameSiteSample")

' Set a value for the cookie
sameSiteCookie.Value = "sample"

' Set the secure flag, which Chrome's changes will require for SameSite none.
' Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = True

' Set the cookie to HTTP only which is good practice unless you really do need
' to access it client side in scripts.
sameSiteCookie.HttpOnly = True

' Expire the cookie in 1 minute
sameSiteCookie.Expires = Date.Now.AddMinutes(1)

' Add the SameSite attribute, this will emit the attribute with a value of none.
' To Not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None

' Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie)
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="256f8-109">Form kimlik doğrulaması tanımlama bilgisinin varsayılan sameSite özniteliği, `web.config` içindeki Forms kimlik doğrulama ayarlarının `cookieSameSite` parametresinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="256f8-109">The default sameSite attribute for a forms authentication cookie is set in the `cookieSameSite` parameter of the forms authentication settings in `web.config`</span></span> 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

<span data-ttu-id="256f8-110">Oturum durumu için varsayılan sameSite özniteliği, `web.config` oturum ayarlarının ' tanımlama bilgisi Esamesitesi ' parametresinde de ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="256f8-110">The default sameSite attribute for session state is also set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

<span data-ttu-id="256f8-111">.NET için Kasım 2019 güncelleştirmesi, en uyumlu ayar olduğu gibi, form kimlik doğrulaması ve oturumunun varsayılan ayarlarını `lax` olarak değiştirdi, ancak iframe 'lere sayfa eklerseniz, bu ayarı None olarak döndürmeniz ve ardından, tarayıcı özelliğine bağlı olarak `none` davranışını ayarlamak için aşağıda gösterilen [yakam](#interception) kodunu eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="256f8-111">The November 2019 update to .NET changed the default settings for Forms Authentication and Session to `lax` as is the most compatible setting, however if you embed pages into iframes you may need to revert this setting to None, and then add the [interception](#interception) code shown below to adjust the `none` behavior depending on browser capability.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="256f8-112">Örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="256f8-112">Running the sample</span></span>

<span data-ttu-id="256f8-113">Örnek projeyi çalıştırırsanız, ilk sayfada tarayıcı hata ayıklayıcıyı yükleyin ve site için tanımlama bilgisi toplamasını görüntülemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="256f8-113">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="256f8-114">Bunu kenar ve Chrome 'a bas `F12` için `Application` sekmesini seçin ve `Storage` bölümündeki `Cookies` seçeneğinin altındaki site URL 'sine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="256f8-114">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![Tarayıcı hata ayıklayıcısı tanımlama bilgisi listesi](sample/img/BrowserDebugger.png)

<span data-ttu-id="256f8-116">"Tanımlama bilgileri oluştur" düğmesine tıkladığınızda örnek tarafından oluşturulan tanımlama bilgisinin, [örnek kodda](#sampleCode)ayarlanan değerle eşleşen `Lax`bir SameSite özniteliği değerine sahip olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="256f8-116">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="256f8-117">Denetleyeistemediğiniz tanımlama bilgilerini kesintiye uğratan</span><span class="sxs-lookup"><span data-stu-id="256f8-117">Intercepting cookies you do not control</span></span>

<span data-ttu-id="256f8-118">.NET 4.5.2, `Response.AddOnSendingHeaders`üstbilgilerin yazılmasını kesintiye uğratan yeni bir olay sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="256f8-118">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="256f8-119">Bu, tanımlama bilgilerini istemci makinesine döndürülmeden önce ele almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="256f8-119">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="256f8-120">Örnekte, tarayıcının yeni sameSite değişikliklerini destekleyip desteklemediğini kontrol eden bir statik yönteme yönelik olarak, yeni `None` değeri ayarlanmışsa, tanımlama bilgilerini özniteliği göstermeme olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="256f8-120">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="256f8-121">Olayı işleme ve tanımlama bilgisi `sameSite` özniteliğini ayarlama hakkında bir [örnek için bkz](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) . [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) .</span><span class="sxs-lookup"><span data-stu-id="256f8-121">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) for an example of handling the event and adjusting the cookie `sameSite` attribute.</span></span>


```vb
Sub FilterSameSiteNoneForIncompatibleUserAgents(ByVal sender As Object)
    Dim application As HttpApplication = TryCast(sender, HttpApplication)

    If application IsNot Nothing Then
        Dim userAgent = application.Context.Request.UserAgent

        If SameSite.DisallowsSameSiteNone(userAgent) Then
            application.Response.AddOnSendingHeaders(
                Function(context)
                    Dim cookies = context.Response.Cookies

                    For i = 0 To cookies.Count - 1
                        Dim cookie = cookies(i)

                        If cookie.SameSite = SameSiteMode.None Then
                            cookie.SameSite = CType((-1), SameSiteMode)
                        End If
                    Next
                End Function)
        End If
    End If
End Sub
```

<span data-ttu-id="256f8-122">Belirli bir adlandırılmış tanımlama bilgisi davranışını çok aynı şekilde değiştirebilirsiniz; Aşağıdaki örnek, `Lax` varsayılan kimlik doğrulama tanımlama bilgisini `None` değerini destekleyen tarayıcılarda `None` olarak ayarlayın veya `None`desteklemeyen tarayıcılarda sameSite özniteliğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="256f8-122">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```vb
Public Shared Sub AdjustSpecificCookieSettings()
    HttpContext.Current.Response.AddOnSendingHeaders(Function(context)
            Dim cookies = context.Response.Cookies

            For i = 0 To cookies.Count - 1
            Dim cookie = cookies(i)

            If String.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal) Then

                If SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent) Then
                    cookie.SameSite = -1
                Else
                    cookie.SameSite = SameSiteMode.None
                End If

                cookie.Secure = True
            End If
            Next
        End Function)
End Sub
```

## <a name="more-information"></a><span data-ttu-id="256f8-123">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="256f8-123">More Information</span></span>

[<span data-ttu-id="256f8-124">Chrome güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="256f8-124">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="256f8-125">ASP.NET belgeleri</span><span class="sxs-lookup"><span data-stu-id="256f8-125">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="256f8-126">.NET SameSite yamaları</span><span class="sxs-lookup"><span data-stu-id="256f8-126">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)