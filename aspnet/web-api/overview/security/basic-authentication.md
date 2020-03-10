---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 'sinde temel kimlik doğrulaması | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'sinde temel kimlik doğrulamasının kullanılmasını açıklar.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555729"
---
# <a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="2ce9a-103">ASP.NET Web API 'sinde temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2ce9a-103">Basic Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="2ce9a-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2ce9a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2ce9a-105">Temel kimlik doğrulaması [RFC 2617, http kimlik doğrulaması: temel ve Özet erişimi kimlik doğrulaması](http://www.ietf.org/rfc/rfc2617.txt)içinde tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="2ce9a-106">Dezavantajlar</span><span class="sxs-lookup"><span data-stu-id="2ce9a-106">Disadvantages</span></span>

- <span data-ttu-id="2ce9a-107">Kullanıcı kimlik bilgileri istekte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="2ce9a-108">Kimlik bilgileri düz metin olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="2ce9a-109">Kimlik bilgileri her istekle birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="2ce9a-110">Tarayıcı oturumunun sonlandırılacağından hariç, oturum açma yöntemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="2ce9a-111">Siteler arası istek için güvenlik açığı (CSRF); Anti-CSRF ölçüleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="2ce9a-112">Yararları</span><span class="sxs-lookup"><span data-stu-id="2ce9a-112">Advantages</span></span>

- <span data-ttu-id="2ce9a-113">Internet standart.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-113">Internet standard.</span></span>
- <span data-ttu-id="2ce9a-114">Tüm büyük tarayıcılar tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="2ce9a-115">Görece basit protokol.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-115">Relatively simple protocol.</span></span>

<span data-ttu-id="2ce9a-116">Temel kimlik doğrulaması aşağıdaki gibi çalışmaktadır:</span><span class="sxs-lookup"><span data-stu-id="2ce9a-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="2ce9a-117">Bir istek kimlik doğrulaması gerektiriyorsa, sunucu 401 (yetkisiz) döndürür.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="2ce9a-118">Yanıt, sunucunun temel kimlik doğrulamasını desteklediğini belirten bir WWW-Authenticate üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="2ce9a-119">İstemci, yetkilendirme üstbilgisinde istemci kimlik bilgileriyle başka bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="2ce9a-120">Kimlik bilgileri "ad: parola", Base64 kodlamalı dize olarak biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="2ce9a-121">Kimlik bilgileri şifrelenmedi.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="2ce9a-122">Temel kimlik doğrulaması, "bölge" bağlamında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="2ce9a-123">Sunucu, WWW-Authenticate üstbilgisindeki bölge adını içerir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="2ce9a-124">Kullanıcının kimlik bilgileri bu bölge içinde geçerli.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="2ce9a-125">Bir bölgenin tam kapsamı sunucu tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="2ce9a-126">Örneğin, kaynakları bölümlemek için birkaç bölge tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="2ce9a-127">Kimlik Bilgileri şifrelenmemiş olarak gönderildiğinden, temel kimlik doğrulaması yalnızca HTTPS üzerinden güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="2ce9a-128">Bkz. [Web API 'de SSL Ile çalışma](working-with-ssl-in-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="2ce9a-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="2ce9a-129">Temel kimlik doğrulaması da CSRF saldırılarına karşı savunmasızdır.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="2ce9a-130">Kullanıcı kimlik bilgilerini girdikten sonra, tarayıcı otomatik olarak onları oturum süresince aynı etki alanına, sonraki isteklere gönderir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="2ce9a-131">Bu, AJAX isteklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-131">This includes AJAX requests.</span></span> <span data-ttu-id="2ce9a-132">Bkz. [siteler arası Istek forgery (CSRF) saldırılarını önleme](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="2ce9a-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="2ce9a-133">IIS ile temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2ce9a-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="2ce9a-134">IIS temel kimlik doğrulamasını destekler, ancak bir desteklenmediği uyarısıyla vardır: kullanıcının kimliği Windows kimlik bilgileriyle doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="2ce9a-135">Bu, kullanıcının sunucunun etki alanında bir hesabı olması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="2ce9a-136">Herkese açık bir Web sitesi için genellikle bir ASP.NET üyelik sağlayıcısına göre kimlik doğrulaması yapmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="2ce9a-137">IIS kullanarak temel kimlik doğrulamasını etkinleştirmek için, ASP.NET projenizin Web. config dosyasında kimlik doğrulama modunu "Windows" olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2ce9a-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="2ce9a-138">Bu modda IIS, kimlik doğrulaması için Windows kimlik bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="2ce9a-139">Ayrıca, IIS 'de temel kimlik doğrulamasını etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="2ce9a-140">IIS Yöneticisi 'nde Özellikler Görünümü ' ne gidin, kimlik doğrulaması ' nı seçin ve temel kimlik doğrulamasını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="2ce9a-141">Web API projenizde, kimlik doğrulaması gerektiren herhangi bir denetleyici eylemi için `[Authorize]` özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="2ce9a-142">İstemci, istekteki yetkilendirme üst bilgisini ayarlayarak kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="2ce9a-143">Tarayıcı istemcileri bu adımı otomatik olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="2ce9a-144">Tarayıcı olmayan istemcilerin üstbilgiyi ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="2ce9a-145">Özel üyelikle temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2ce9a-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="2ce9a-146">Belirtildiği gibi, IIS 'de yerleşik olarak bulunan temel kimlik doğrulaması Windows kimlik bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="2ce9a-147">Bu, barındırma sunucusunda kullanıcılarınız için hesap oluşturmanız gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="2ce9a-148">Ancak, bir Internet uygulaması için Kullanıcı hesapları genellikle bir dış veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="2ce9a-149">Aşağıdaki kod, temel kimlik doğrulaması gerçekleştiren bir HTTP modülünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="2ce9a-150">Bu örnekte sözde bir yöntem olan `CheckPassword` yöntemini değiştirerek, bir ASP.NET üyelik sağlayıcısını kolayca takabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="2ce9a-151">Web API 2 ' de, bir HTTP modülü yerine bir [kimlik doğrulama filtresi](authentication-filters.md) veya [owın ara yazılımı](../../../aspnet/overview/owin-and-katana/index.md)yazmayı düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="2ce9a-152">HTTP modülünü etkinleştirmek için, **System. webserver** bölümündeki Web. config dosyanıza aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2ce9a-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="2ce9a-153">"YourAssemblyName" öğesini derlemenin adıyla değiştirin ("dll" uzantısını dahil değil).</span><span class="sxs-lookup"><span data-stu-id="2ce9a-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="2ce9a-154">Formlar veya Windows kimlik doğrulaması gibi diğer kimlik doğrulama düzenlerini devre dışı bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ce9a-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>
