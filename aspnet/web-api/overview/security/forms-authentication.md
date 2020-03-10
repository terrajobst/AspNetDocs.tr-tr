---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API 'sinde Forms kimlik doğrulaması | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'sinde Forms kimlik doğrulamasının kullanımını açıklar.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598597"
---
# <a name="forms-authentication-in-aspnet-web-api"></a>ASP.NET Web API 'sinde Forms kimlik doğrulaması

, [Mike te son](https://github.com/MikeWasson)

Form kimlik doğrulaması, kullanıcının kimlik bilgilerini sunucuya göndermek için bir HTML formu kullanır. Internet standardı değildir. Form kimlik doğrulaması, kullanıcının HTML formuyla etkileşime girebilmesi için yalnızca bir Web uygulamasından çağrılan Web API 'Leri için uygundur.

| Yararları | Dezavantajlar |
| --- | --- |
| -Kolay uygulama: ASP.NET yerleşik olarak yerleşik. -ASP.NET üyelik sağlayıcısını kullanır, bu da Kullanıcı hesaplarını yönetmeyi kolaylaştırır. | -Standart bir HTTP kimlik doğrulama mekanizması değildir; Standart yetkilendirme üst bilgisi yerine HTTP tanımlama bilgilerini kullanır. -Bir tarayıcı istemcisi gerektirir. -Kimlik bilgileri düz metin olarak gönderilir. -Siteler arası istek sahteciliği (CSRF) ile savunmasızdır; Anti-CSRF ölçüleri gerektirir. -Tarayıcı olmayan istemcilerden kullanılması zor. Oturum açma tarayıcı gerektirir. -Kullanıcı kimlik bilgileri istekte gönderilir. -Bazı kullanıcılar tanımlama bilgilerini devre dışı bırakır. |

Kısaca, ASP.NET ' de form kimlik doğrulaması şöyle çalışmaktadır:

1. İstemci, kimlik doğrulaması gerektiren bir kaynağı ister.
2. Kullanıcının kimliği doğrulanmıyorsa, sunucu HTTP 302 (bulunan) döndürür ve bir oturum açma sayfasına yönlendirir.
3. Kullanıcı kimlik bilgilerini girer ve formu gönderir.
4. Sunucu, özgün URI 'ye yeniden yönlendiren başka bir HTTP 302 döndürür. Bu yanıt bir kimlik doğrulama tanımlama bilgisi içerir.
5. İstemci, kaynağı yeniden ister. İstek, kimlik doğrulama tanımlama bilgisini içerir, bu nedenle sunucu isteği verir.

![](forms-authentication/_static/image1.png)

Daha fazla bilgi için bkz [. Forms kimlik doğrulamasına genel bakış.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)

## <a name="using-forms-authentication-with-web-api"></a>Web API ile form kimlik doğrulamasını kullanma

Forms kimlik doğrulaması kullanan bir uygulama oluşturmak için MVC 4 proje sihirbazında "Internet uygulaması" şablonunu seçin. Bu şablon, hesap yönetimi için MVC denetleyicileri oluşturur. Ayrıca, ASP.NET Fall 2012 güncelleştirmesinde bulunan "tek sayfalı uygulama" şablonunu da kullanabilirsiniz.

Web API denetleyicilerinizde, [[Yetkilendir] özniteliğini kullanma](authentication-and-authorization-in-aspnet-web-api.md#auth3)bölümünde açıklandığı gibi `[Authorize]` özniteliğini kullanarak erişimi kısıtlayabilirsiniz.

Forms-Authentication, isteklerin kimliğini doğrulamak için bir oturum tanımlama bilgisi kullanır. Tarayıcılar tüm ilgili tanımlama bilgilerini otomatik olarak hedef Web sitesine gönderir. Bu özellik, Forms kimlik doğrulamasının siteler arası istek sahteciliğini önleme (CSRF) saldırılarına karşı savunmasız kalmasına neden olur. [siteler arası istek sahteciliği (CSRF) saldırılarını önleme](preventing-cross-site-request-forgery-csrf-attacks.md)konusuna bakın.

Form kimlik doğrulaması, kullanıcının kimlik bilgilerini şifrelemez. Bu nedenle, SSL ile kullanılmadığı takdirde Forms kimlik doğrulaması güvenli değildir. Bkz. [Web API 'de SSL Ile çalışma](working-with-ssl-in-web-api.md).
