---
uid: signalr/overview/older-versions/hub-authorization
title: SignalR hub 'Ları için kimlik doğrulaması ve yetkilendirme (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bu konuda, hangi kullanıcıların veya rollerin hub yöntemlerine erişebileceğini nasıl kısıtlayabileceği açıklanmaktadır.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558536"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="5a4f0-103">SignalR Hub’ları için Kimlik Doğrulaması ve Yetkilendirme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="5a4f0-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>

<span data-ttu-id="5a4f0-104">, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5a4f0-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5a4f0-105">Bu konuda, hangi kullanıcıların veya rollerin hub yöntemlerine erişebileceğini nasıl kısıtlayabileceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>

## <a name="overview"></a><span data-ttu-id="5a4f0-106">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="5a4f0-106">Overview</span></span>

<span data-ttu-id="5a4f0-107">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="5a4f0-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="5a4f0-108">Yetkilendir özniteliği</span><span class="sxs-lookup"><span data-stu-id="5a4f0-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="5a4f0-109">Tüm Hub 'lar için kimlik doğrulaması gerektir</span><span class="sxs-lookup"><span data-stu-id="5a4f0-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="5a4f0-110">Özelleştirilmiş yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="5a4f0-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="5a4f0-111">Kimlik doğrulama bilgilerini istemcilere geçir</span><span class="sxs-lookup"><span data-stu-id="5a4f0-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="5a4f0-112">.NET istemcileri için kimlik doğrulama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="5a4f0-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="5a4f0-113">Forms kimlik doğrulaması ile tanımlama bilgisi</span><span class="sxs-lookup"><span data-stu-id="5a4f0-113">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="5a4f0-114">Windows Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5a4f0-114">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="5a4f0-115">Bağlantı üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="5a4f0-115">Connection header</span></span>](#header)
    - [<span data-ttu-id="5a4f0-116">Sertifika</span><span class="sxs-lookup"><span data-stu-id="5a4f0-116">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="5a4f0-117">Yetkilendir özniteliği</span><span class="sxs-lookup"><span data-stu-id="5a4f0-117">Authorize attribute</span></span>

<span data-ttu-id="5a4f0-118">SignalR, bir hub veya yönteme hangi kullanıcıların veya rollerin erişebileceğini belirtmek için [Yetkilendir](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) özniteliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="5a4f0-119">Bu öznitelik `Microsoft.AspNet.SignalR` ad alanında bulunur.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="5a4f0-120">`Authorize` özniteliğini bir hub 'daki bir hub 'a ya da belirli yöntemlere uygularsınız.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="5a4f0-121">`Authorize` özniteliğini bir hub sınıfına uyguladığınızda, belirtilen yetkilendirme gereksinimi, hub 'daki tüm yöntemlere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="5a4f0-122">Uygulayabileceğiniz farklı yetkilendirme gereksinimleri türleri aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="5a4f0-123">`Authorize` özniteliği olmadan, hub 'daki tüm ortak Yöntemler hub 'a bağlı bir istemci tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="5a4f0-124">Web uygulamanızda "admin" adlı bir rol tanımladıysanız, yalnızca bu roldeki kullanıcıların aşağıdaki kodla bir hub 'a erişebileceğini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="5a4f0-125">Ya da bir hub 'ın tüm kullanıcılar için kullanılabilir bir yöntem içerdiğini ve yalnızca kimliği doğrulanmış kullanıcılar tarafından kullanılabilen ikinci bir yöntemi aşağıda gösterildiği gibi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="5a4f0-126">Aşağıdaki örneklerde farklı yetkilendirme senaryoları ele verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5a4f0-126">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="5a4f0-127">`[Authorize]` – yalnızca kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="5a4f0-127">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="5a4f0-128">`[Authorize(Roles = "Admin,Manager")]` – yalnızca belirtilen rollerdeki kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="5a4f0-128">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="5a4f0-129">`[Authorize(Users = "user1,user2")]` – yalnızca belirtilen kullanıcı adlarına sahip kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="5a4f0-129">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="5a4f0-130">`[Authorize(RequireOutgoing=false)]` – yalnızca kimliği doğrulanmış kullanıcılar hub 'ı çağırabilir, ancak sunucudan istemcilere geri çağrılar bir ileti gönderebildiği ancak diğerlerinin iletiyi alabileceği gibi yetkilendirme ile sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-130">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="5a4f0-131">Requiregiden özelliği, hub içindeki bireyler yöntemlerine değil, yalnızca tüm Hub 'a uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="5a4f0-132">Requiregiden değeri false olarak ayarlandığında, yalnızca yetkilendirme gereksinimini karşılayan kullanıcılar sunucudan çağırılır.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="5a4f0-133">Tüm Hub 'lar için kimlik doğrulaması gerektir</span><span class="sxs-lookup"><span data-stu-id="5a4f0-133">Require authentication for all hubs</span></span>

<span data-ttu-id="5a4f0-134">Uygulama başladığında [requiauthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) metodunu çağırarak uygulamanızdaki tüm Hub 'lar ve hub yöntemleri için kimlik doğrulaması yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="5a4f0-135">Birden çok hub olduğunda ve bunların tümü için bir kimlik doğrulama gereksinimini zorlamak istediğinizde bu yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="5a4f0-136">Bu yöntemle rol, Kullanıcı veya giden yetkilendirme belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="5a4f0-137">Yalnızca hub yöntemlerine erişimin kimliği doğrulanmış kullanıcılarla kısıtlanmasını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="5a4f0-138">Bununla birlikte, ek gereksinimler belirtmek için yine de, yetkilendirme özniteliğini hub 'lara veya yöntemlere uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="5a4f0-139">Özniteliklerde belirttiğiniz herhangi bir gereksinim, temel kimlik doğrulaması gereksinimine ek olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="5a4f0-140">Aşağıdaki örnek, tüm Hub yöntemlerini kimliği doğrulanmış kullanıcılarla kısıtlayan bir Global. asax dosyası gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="5a4f0-141">Bir SignalR isteği işlendikten sonra `RequireAuthentication()` yöntemini çağırırsanız, SignalR bir `InvalidOperationException` özel durumu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="5a4f0-142">Bu özel durum, işlem hattı çağrıldıktan sonra HubPipeline 'e modül ekleyemediği için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="5a4f0-143">Önceki örnekte, ilk isteğin işlenmesinden önce bir kez yürütülen `Application_Start` yönteminde `RequireAuthentication` yönteminin çağrılması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="5a4f0-144">Özelleştirilmiş yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="5a4f0-144">Customized authorization</span></span>

<span data-ttu-id="5a4f0-145">Yetkilendirmenin nasıl belirlendiğini özelleştirmeniz gerekiyorsa, `AuthorizeAttribute` türeten bir sınıf oluşturabilir ve [userauthorization](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) metodunu geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="5a4f0-146">Bu yöntem, kullanıcının isteği tamamlamaya yetkili olup olmadığını belirlemede her istek için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="5a4f0-147">Geçersiz kılınan yöntemde, yetkilendirme senaryonuz için gerekli mantığı sağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="5a4f0-148">Aşağıdaki örnek, talep tabanlı kimlik aracılığıyla yetkilendirmeyi nasıl zorlayacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="5a4f0-149">Kimlik doğrulama bilgilerini istemcilere geçir</span><span class="sxs-lookup"><span data-stu-id="5a4f0-149">Pass authentication information to clients</span></span>

<span data-ttu-id="5a4f0-150">İstemci üzerinde çalışan koddaki kimlik doğrulama bilgilerini kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="5a4f0-151">İstemci üzerindeki yöntemleri çağırırken gerekli bilgileri geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="5a4f0-152">Örneğin, bir sohbet uygulaması yöntemi, aşağıda gösterildiği gibi bir ileti gönderen kişinin kullanıcı adına bir parametre olarak geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="5a4f0-153">Ya da, aşağıda gösterildiği gibi, kimlik doğrulama bilgilerini temsil eden bir nesne oluşturabilir ve bu nesneyi bir parametre olarak geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="5a4f0-154">Kötü niyetli bir Kullanıcı bu istemciden gelen bir isteği taklit etmek için onu kullanabilmesi için, bir istemcinin bağlantı kimliğini asla diğer istemcilere iletmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="5a4f0-155">.NET istemcileri için kimlik doğrulama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="5a4f0-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="5a4f0-156">Bir konsol uygulaması gibi, kimliği doğrulanmış kullanıcılarla sınırlı bir hub ile etkileşime geçen bir .NET istemciniz varsa, kimlik doğrulama bilgilerini bir tanımlama bilgisine, bağlantı başlığına veya bir sertifikaya geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="5a4f0-157">Bu bölümdeki örneklerde, kullanıcının kimliğini doğrulamak için bu farklı yöntemlerin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="5a4f0-158">Bunlar tam işlevli SignalR uygulamaları değildir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="5a4f0-159">SignalR ile .NET istemcileri hakkında daha fazla bilgi için bkz. [hub API Kılavuzu-.NET istemcisi](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="5a4f0-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="5a4f0-160">Tanımlama Bilgisi</span><span class="sxs-lookup"><span data-stu-id="5a4f0-160">Cookie</span></span>

<span data-ttu-id="5a4f0-161">.NET istemciniz ASP.NET Forms kimlik doğrulaması kullanan bir hub ile etkileşime geçtiğinde, bağlantıda kimlik doğrulama tanımlama bilgisini el ile ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="5a4f0-162">Tanımlama bilgisini, [Hubconnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) nesnesindeki `CookieContainer` özelliğine eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="5a4f0-163">Aşağıdaki örnek, bir Web sayfasından kimlik doğrulama tanımlama bilgisi alan ve bu tanımlama bilgisini bağlantıya ekleyen bir konsol uygulamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="5a4f0-164">Örnekteki URL `https://www.contoso.com/RemoteLogin`, oluşturmanız gereken bir Web sayfasına işaret eder.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="5a4f0-165">Sayfa, postalanan Kullanıcı adı ve parolasını alır ve kimlik bilgileriyle kullanıcıya oturum açmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="5a4f0-166">Konsol uygulaması, aşağıdaki arka plan kod dosyasını içeren boş bir sayfaya başvuruda bulunmak için kimlik bilgilerini www.contoso.com/RemoteLogin adresine gönderir.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="5a4f0-167">Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5a4f0-167">Windows authentication</span></span>

<span data-ttu-id="5a4f0-168">Windows kimlik doğrulamasını kullanırken, [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) özelliğini kullanarak geçerli kullanıcının kimlik bilgilerini geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="5a4f0-169">DefaultCredentials değeri için bağlantı kimlik bilgilerini ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="5a4f0-170">Bağlantı üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="5a4f0-170">Connection header</span></span>

<span data-ttu-id="5a4f0-171">Uygulamanız tanımlama bilgilerini kullanmıyor ise, Kullanıcı bilgilerini bağlantı üst bilgisinde geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="5a4f0-172">Örneğin, bağlantı üst bilgisinde bir belirteç geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="5a4f0-173">Ardından, hub 'da kullanıcının belirtecini doğrularsınız.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="5a4f0-174">Sertifika</span><span class="sxs-lookup"><span data-stu-id="5a4f0-174">Certificate</span></span>

<span data-ttu-id="5a4f0-175">Kullanıcıyı doğrulamak için bir istemci sertifikası geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="5a4f0-176">Bağlantıyı oluştururken sertifikayı eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="5a4f0-177">Aşağıdaki örnek, bağlantıya yalnızca bir istemci sertifikasının nasıl ekleneceğini gösterir. tam konsol uygulamasını göstermez.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="5a4f0-178">Sertifikayı oluşturmak için çeşitli farklı yollar sağlayan [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5a4f0-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
