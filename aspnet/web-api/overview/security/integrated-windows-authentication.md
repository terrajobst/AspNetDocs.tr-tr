---
uid: web-api/overview/security/integrated-windows-authentication
title: Tümleşik Windows kimlik doğrulaması | Microsoft Docs
author: MikeWasson
description: Tümleşik Windows kimlik doğrulaması ASP.NET Web API'sini kullanmayı açıklar.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: 13dead421abf7ded73cbb2e5f87e54b1a869b5d4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077775"
---
<a name="integrated-windows-authentication"></a><span data-ttu-id="fbe50-103">Tümleşik Windows Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fbe50-103">Integrated Windows Authentication</span></span>
====================
<span data-ttu-id="fbe50-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fbe50-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fbe50-105">Tümleşik Windows kimlik doğrulaması, Kerberos veya NTLM kullanarak Windows kimlik bilgileriyle kullanıcıların oturum açmasına sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbe50-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="fbe50-106">İstemci kimlik bilgileri yetkilendirme üst bilgisinde gönderir.</span><span class="sxs-lookup"><span data-stu-id="fbe50-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="fbe50-107">Windows kimlik doğrulaması intranet ortamı için idealdir.</span><span class="sxs-lookup"><span data-stu-id="fbe50-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="fbe50-108">Daha fazla bilgi için [Windows kimlik doğrulaması](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span><span class="sxs-lookup"><span data-stu-id="fbe50-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="fbe50-109">Yararları</span><span class="sxs-lookup"><span data-stu-id="fbe50-109">Advantages</span></span> | <span data-ttu-id="fbe50-110">Dezavantajlar</span><span class="sxs-lookup"><span data-stu-id="fbe50-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="fbe50-111">-IIS ile oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="fbe50-111">- Built into IIS.</span></span> <span data-ttu-id="fbe50-112">-Kullanıcı kimlik bilgilerinin istekte göndermez.</span><span class="sxs-lookup"><span data-stu-id="fbe50-112">- Does not send the user credentials in the request.</span></span> <span data-ttu-id="fbe50-113">-İstemci bilgisayarı (örneğin, intranet uygulaması) etki alanı dahilse, kullanıcının kimlik bilgilerini girmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fbe50-113">- If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="fbe50-114">-Internet uygulamaları için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="fbe50-114">- Not recommended for Internet applications.</span></span> <span data-ttu-id="fbe50-115">-İstemci Kerberos veya NTLM desteğini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fbe50-115">- Requires Kerberos or NTLM support in the client.</span></span> <span data-ttu-id="fbe50-116">-İstemci, Active Directory etki alanında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fbe50-116">- Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="fbe50-117">Uygulamanızı Azure'da barındırılır ve bir şirket içi Active Directory etki alanı varsa, şirket içi AD'nizi Azure Active Directory ile Federasyon göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fbe50-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="fbe50-118">Böylece, kullanıcılar kendi şirket içi kimlik bilgileriyle oturum açabilir, ancak kimlik doğrulaması, Azure AD tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fbe50-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="fbe50-119">Daha fazla bilgi için [Azure kimlik doğrulaması](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fbe50-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>


<span data-ttu-id="fbe50-120">Tümleşik Windows kimlik doğrulaması kullanan bir uygulama oluşturmak için MVC 4 Proje Sihirbazı'nda "Intranet uygulaması" şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="fbe50-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="fbe50-121">Bu proje şablonu aşağıdaki ayarları Web.config dosyasına koyar:</span><span class="sxs-lookup"><span data-stu-id="fbe50-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="fbe50-122">İstemci tarafında, tümleşik Windows kimlik doğrulamasını destekleyen bir tarayıcı ile çalışır. [anlaş](http://www.ietf.org/rfc/rfc4559.txt) çoğu bilinen tarayıcılar içeren kimlik doğrulama düzeni.</span><span class="sxs-lookup"><span data-stu-id="fbe50-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="fbe50-123">.NET istemci uygulamaları için **HttpClient** sınıfı, Windows kimlik doğrulamasını destekler:</span><span class="sxs-lookup"><span data-stu-id="fbe50-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="fbe50-124">Windows kimlik doğrulaması için siteler arası istek sahteciliği (CSRF) saldırılarını karşı savunmasızdır.</span><span class="sxs-lookup"><span data-stu-id="fbe50-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="fbe50-125">Bkz: [siteler arası istek sahteciliği (CSRF) saldırılarını önleme](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="fbe50-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
