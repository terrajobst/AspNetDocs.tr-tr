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
# <a name="integrated-windows-authentication"></a><span data-ttu-id="3359e-103">Tümleşik Windows Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3359e-103">Integrated Windows Authentication</span></span>

<span data-ttu-id="3359e-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3359e-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3359e-105">Tümleşik Windows kimlik doğrulaması, kullanıcıların Kerberos veya NTLM kullanarak Windows kimlik bilgileriyle oturum açmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3359e-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="3359e-106">İstemci kimlik bilgilerini yetkilendirme üst bilgisinde gönderir.</span><span class="sxs-lookup"><span data-stu-id="3359e-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="3359e-107">Windows kimlik doğrulaması, intranet ortamı için idealdir.</span><span class="sxs-lookup"><span data-stu-id="3359e-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="3359e-108">Daha fazla bilgi için bkz. [Windows kimlik doğrulaması](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span><span class="sxs-lookup"><span data-stu-id="3359e-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="3359e-109">Yararları</span><span class="sxs-lookup"><span data-stu-id="3359e-109">Advantages</span></span> | <span data-ttu-id="3359e-110">Dezavantajlar</span><span class="sxs-lookup"><span data-stu-id="3359e-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="3359e-111">-IIS içinde yerleşik.</span><span class="sxs-lookup"><span data-stu-id="3359e-111">- Built into IIS.</span></span> <span data-ttu-id="3359e-112">-İstekte Kullanıcı kimlik bilgilerini göndermez.</span><span class="sxs-lookup"><span data-stu-id="3359e-112">- Does not send the user credentials in the request.</span></span> <span data-ttu-id="3359e-113">-İstemci bilgisayar etki alanına aitse (örneğin, intranet uygulaması), kullanıcının kimlik bilgilerini girmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3359e-113">- If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="3359e-114">-Internet uygulamaları için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="3359e-114">- Not recommended for Internet applications.</span></span> <span data-ttu-id="3359e-115">-İstemcide Kerberos veya NTLM desteği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3359e-115">- Requires Kerberos or NTLM support in the client.</span></span> <span data-ttu-id="3359e-116">-İstemci Active Directory etki alanında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3359e-116">- Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="3359e-117">Uygulamanız Azure üzerinde barındırılıyorsa ve şirket içi Active Directory etki alanınız varsa, şirket içi AD 'nizi Azure Active Directory ile federasyona eklemeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="3359e-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="3359e-118">Bu şekilde, kullanıcılar şirket içi kimlik bilgileriyle oturum açabilirler, ancak kimlik doğrulaması Azure AD tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3359e-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="3359e-119">Daha fazla bilgi için bkz. [Azure kimlik doğrulaması](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3359e-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>

<span data-ttu-id="3359e-120">Tümleşik Windows kimlik doğrulaması kullanan bir uygulama oluşturmak için, MVC 4 proje sihirbazında "Intranet uygulaması" şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="3359e-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="3359e-121">Bu proje şablonu, Web. config dosyasına aşağıdaki ayarı koyar:</span><span class="sxs-lookup"><span data-stu-id="3359e-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="3359e-122">İstemci tarafında, tümleşik Windows kimlik doğrulaması, çok büyük tarayıcıları içeren, [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) kimlik doğrulama düzenini destekleyen herhangi bir tarayıcıyla birlikte çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="3359e-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="3359e-123">.NET istemci uygulamaları için, **HttpClient** sınıfı Windows kimlik doğrulamasını destekler:</span><span class="sxs-lookup"><span data-stu-id="3359e-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="3359e-124">Windows kimlik doğrulaması, siteler arası istek sahteciliğini önleme (CSRF) saldırılarına karşı savunmasızdır.</span><span class="sxs-lookup"><span data-stu-id="3359e-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="3359e-125">Bkz. [siteler arası Istek forgery (CSRF) saldırılarını önleme](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="3359e-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
