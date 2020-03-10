---
uid: web-api/overview/security/integrated-windows-authentication
title: Tümleşik Windows kimlik doğrulaması | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'de tümleşik Windows kimlik doğrulamasının kullanılmasını açıklar.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: e4f31f191f3c0fabff308ea5dadb0f1d9ce7d448
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621746"
---
# <a name="integrated-windows-authentication"></a>Tümleşik Windows Kimlik Doğrulaması

, [Mike te son](https://github.com/MikeWasson)

Tümleşik Windows kimlik doğrulaması, kullanıcıların Kerberos veya NTLM kullanarak Windows kimlik bilgileriyle oturum açmasına olanak sağlar. İstemci kimlik bilgilerini yetkilendirme üst bilgisinde gönderir. Windows kimlik doğrulaması, intranet ortamı için idealdir. Daha fazla bilgi için bkz. [Windows kimlik doğrulaması](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).

| Yararları | Dezavantajlar |
| --- | --- |
| -IIS içinde yerleşik. -İstekte Kullanıcı kimlik bilgilerini göndermez. -İstemci bilgisayar etki alanına aitse (örneğin, intranet uygulaması), kullanıcının kimlik bilgilerini girmesi gerekmez. | -Internet uygulamaları için önerilmez. -İstemcide Kerberos veya NTLM desteği gerektirir. -İstemci Active Directory etki alanında olmalıdır. |

> [!NOTE]
> Uygulamanız Azure üzerinde barındırılıyorsa ve şirket içi Active Directory etki alanınız varsa, şirket içi AD 'nizi Azure Active Directory ile federasyona eklemeyi düşünün. Bu şekilde, kullanıcılar şirket içi kimlik bilgileriyle oturum açabilirler, ancak kimlik doğrulaması Azure AD tarafından gerçekleştirilir. Daha fazla bilgi için bkz. [Azure kimlik doğrulaması](../../../visual-studio/overview/2012/windows-azure-authentication.md).

Tümleşik Windows kimlik doğrulaması kullanan bir uygulama oluşturmak için, MVC 4 proje sihirbazında "Intranet uygulaması" şablonunu seçin. Bu proje şablonu, Web. config dosyasına aşağıdaki ayarı koyar:

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

İstemci tarafında, tümleşik Windows kimlik doğrulaması, çok büyük tarayıcıları içeren, [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) kimlik doğrulama düzenini destekleyen herhangi bir tarayıcıyla birlikte çalışacaktır. .NET istemci uygulamaları için, **HttpClient** sınıfı Windows kimlik doğrulamasını destekler:

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Windows kimlik doğrulaması, siteler arası istek sahteciliğini önleme (CSRF) saldırılarına karşı savunmasızdır. Bkz. [siteler arası Istek forgery (CSRF) saldırılarını önleme](preventing-cross-site-request-forgery-csrf-attacks.md).
