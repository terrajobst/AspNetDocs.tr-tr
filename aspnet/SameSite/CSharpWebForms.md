---
title: ASP.NET 4.7.2 C# WebForms Için SameSite tanımlama bilgisi örneği
author: blowdart
description: ASP.NET 4.7.2 C# WebForms Için SameSite tanımlama bilgisi örneği
ms.author: riande
ms.date: 2/15/2019
uid: samesite/CSharpWebForms
ms.openlocfilehash: 50d4745eca5954275abaa59dab726e7cf7ea193f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458485"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a>ASP.NET 4.7.2 C# WebForms Için SameSite tanımlama bilgisi örneği

.NET Framework 4,7, [SameSite](https://www.owasp.org/index.php/SameSite) özniteliği için yerleşik desteğe sahiptir, ancak özgün standarda uyar.
Düzeltme eki uygulanmış davranış, değeri bir `None`bir değere yaymaması yerine, özniteliği bir değeri olarak göstermek için `SameSite.None` anlamını değiştirdi. Değeri göstermek istiyorsanız, bir tanımlama bilgisinde `SameSite` özelliğini-1 olarak ayarlayabilirsiniz.

## <a name="sampleCode"></a>SameSite özniteliği yazılıyor

Aşağıda, bir tanımlama bilgisine bir SameSite özniteliği yazma örneği verilmiştir;

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookie
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for SameSite none.
// Note this will also require you to be running on HTTPS
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

Form kimlik doğrulaması tanımlama bilgisinin varsayılan sameSite özniteliği, `web.config` içindeki Forms kimlik doğrulama ayarlarının `cookieSameSite` parametresinde ayarlanır. 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

Oturum durumu için varsayılan sameSite özniteliği, `web.config` oturum ayarlarının ' tanımlama bilgisi Esamesitesi ' parametresinde de ayarlanır.

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

.NET için Kasım 2019 güncelleştirmesi, en uyumlu ayar olduğu gibi, form kimlik doğrulaması ve oturumunun varsayılan ayarlarını `lax` olarak değiştirdi, ancak iframe 'lere sayfa eklerseniz, bu ayarı None olarak döndürmeniz ve ardından, tarayıcı özelliğine bağlı olarak `none` davranışını ayarlamak için aşağıda gösterilen [yakam](#interception) kodunu eklemeniz gerekebilir.

### <a name="running-the-sample"></a>Örneği çalıştırma

Örnek projeyi çalıştırırsanız, ilk sayfada tarayıcı hata ayıklayıcıyı yükleyin ve site için tanımlama bilgisi toplamasını görüntülemek için kullanın.
Bunu kenar ve Chrome 'a bas `F12` için `Application` sekmesini seçin ve `Storage` bölümündeki `Cookies` seçeneğinin altındaki site URL 'sine tıklayın.

![Tarayıcı hata ayıklayıcısı tanımlama bilgisi listesi](sample/img/BrowserDebugger.png)

"Tanımlama bilgileri oluştur" düğmesine tıkladığınızda örnek tarafından oluşturulan tanımlama bilgisinin, [örnek kodda](#sampleCode)ayarlanan değerle eşleşen `Lax`bir SameSite özniteliği değerine sahip olduğunu görebilirsiniz.

## <a name="interception"></a>Denetleyeistemediğiniz tanımlama bilgilerini kesintiye uğratan

.NET 4.5.2, `Response.AddOnSendingHeaders`üstbilgilerin yazılmasını kesintiye uğratan yeni bir olay sunmuştur. Bu, tanımlama bilgilerini istemci makinesine döndürülmeden önce ele almak için kullanılabilir. Örnekte, tarayıcının yeni sameSite değişikliklerini destekleyip desteklemediğini kontrol eden bir statik yönteme yönelik olarak, yeni `None` değeri ayarlanmışsa, tanımlama bilgilerini özniteliği göstermeme olarak değiştirir.

Olayı işleme ve tanımlama bilgisi `sameSite` özniteliğini ayarlama hakkında bir [örnek için bkz](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) . [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) .

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

Belirli bir adlandırılmış tanımlama bilgisi davranışını çok aynı şekilde değiştirebilirsiniz; Aşağıdaki örnek, `Lax` varsayılan kimlik doğrulama tanımlama bilgisini `None` değerini destekleyen tarayıcılarda `None` olarak ayarlayın veya `None`desteklemeyen tarayıcılarda sameSite özniteliğini kaldırır.

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

## <a name="more-information"></a>Daha Fazla Bilgi

[Chrome güncelleştirmeleri](https://www.chromium.org/updates/same-site)

[ASP.NET belgeleri](/aspnet/samesite/system-web-samesite)

[.NET SameSite yamaları](/aspnet/samesite/kbs-samesite)