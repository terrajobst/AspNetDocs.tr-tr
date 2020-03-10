---
title: ASP.NET 4.7.2 VB MVC için SameSite tanımlama bilgisi örneği
author: blowdart
description: ASP.NET 4.7.2 VB MVC için SameSite tanımlama bilgisi örneği
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547812"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a>ASP.NET 4.7.2 VB MVC için SameSite tanımlama bilgisi örneği

.NET Framework 4,7, [SameSite](https://www.owasp.org/index.php/SameSite) özniteliği için yerleşik desteğe sahiptir, ancak özgün standarda uyar.
Düzeltme eki uygulanmış davranış, değeri bir `None`bir değere yaymaması yerine, özniteliği bir değeri olarak göstermek için `SameSite.None` anlamını değiştirdi. Değeri göstermek istiyorsanız, bir tanımlama bilgisinde `SameSite` özelliğini-1 olarak ayarlayabilirsiniz.

## <a name="sampleCode"></a>SameSite özniteliği yazılıyor

Aşağıda, bir tanımlama bilgisine bir SameSite özniteliği yazma örneği verilmiştir;

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

Oturum durumu için varsayılan sameSite özniteliği, `web.config` oturum ayarlarının ' tanımlama bilgisi Esamesitesi ' parametresinde ayarlanır

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a>MVC kimlik doğrulaması

OWIN MVC tanımlama bilgisi tabanlı kimlik doğrulaması, tanımlama bilgisi özniteliklerinin değiştirilmesini sağlamak için bir tanımlama bilgisi Yöneticisi kullanır. [Samesitepişirme IEManager. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) , bu tür bir sınıfın bir uygulamasıdır ve kendi projelerinize kopyalayabilirsiniz. 

Microsoft. Owin bileşenlerinizin 4.1.0 veya üzeri sürüme yükseltildiğinden emin olmanız gerekir. Örneğin tüm sürüm numaralarının eşleştiğinden emin olmak için `packages.config` dosyanızı denetleyin.

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

Kimlik doğrulama bileşenleri, başlangıç sınıfınıza ilişkin bir IEManager 'ı kullanacak şekilde yapılandırılmalıdır;

```vb
Public Sub Configuration(app As IAppBuilder)
    app.UseCookieAuthentication(New CookieAuthenticationOptions() With {
        .CookieSameSite = SameSiteMode.None,
        .CookieHttpOnly = True,
        .CookieSecure = CookieSecureOption.Always,
        .CookieManager = New SameSiteCookieManager(New SystemWebCookieManager())
    })
End Sub
```

Bunu destekleyen *her* bir bileşen için bir tanımlama bilgisi Yöneticisi ayarlanmalıdır; bu, ıeauthentication ve Openıdconnectauthentication bilgilerini içerir.

Yanıt tanımlama bilgisi tümleştirmesiyle ilgili [bilinen sorunlardan](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) kaçınmak Için Systemwebcookie IEManager kullanılır.

### <a name="running-the-sample"></a>Örneği çalıştırma

Örnek projeyi çalıştırırsanız, lütfen ilk sayfada tarayıcı hata ayıklayıcıyı yükleyin ve site için tanımlama bilgisi toplamasını görüntülemek için kullanın.
Bunu kenar ve Chrome 'a bas `F12` için `Application` sekmesini seçin ve `Storage` bölümündeki `Cookies` seçeneğinin altındaki site URL 'sine tıklayın.

![Tarayıcı hata ayıklayıcısı tanımlama bilgisi listesi](sample/img/BrowserDebugger.png)

"SameSite tanımlama bilgisi oluştur" düğmesine tıkladığınızda örnek tarafından oluşturulan tanımlama bilgisinin, [örnek kodda](#sampleCode)ayarlanan değerle eşleşen `Lax`bir SameSite özniteliği değeri olduğunu görürsünüz.

## <a name="interception"></a>Denetleyeistemediğiniz tanımlama bilgilerini kesintiye uğratan

.NET 4.5.2, `Response.AddOnSendingHeaders`üstbilgilerin yazılmasını kesintiye uğratan yeni bir olay sunmuştur. Bu, tanımlama bilgilerini istemci makinesine döndürülmeden önce ele almak için kullanılabilir. Örnekte, tarayıcının yeni sameSite değişikliklerini destekleyip desteklemediğini kontrol eden bir statik yönteme yönelik olarak, yeni `None` değeri ayarlanmışsa, tanımlama bilgilerini özniteliği göstermeme olarak değiştirir.

Olayı işleme bir örnek için bkz [. Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) ve olay işleme bir örnek Için [samesitetanýmlama bilgileri erewriter. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) ve kendi kodunuza kopyalayabileceğiniz tanımlama bilgisi `sameSite` özniteliği ayarlama.

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

Belirli bir adlandırılmış tanımlama bilgisi davranışını çok aynı şekilde değiştirebilirsiniz; Aşağıdaki örnek, `Lax` varsayılan kimlik doğrulama tanımlama bilgisini `None` değerini destekleyen tarayıcılarda `None` olarak ayarlayın veya `None`desteklemeyen tarayıcılarda sameSite özniteliğini kaldırır.

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

## <a name="more-information"></a>Daha Fazla Bilgi
 
[Chrome güncelleştirmeleri](https://www.chromium.org/updates/same-site)

[OWıN SameSite belgeleri](/aspnet/samesite/owin-samesite)

[ASP.NET belgeleri](/aspnet/samesite/system-web-samesite)

[.NET SameSite yamaları](/aspnet/samesite/kbs-samesite)