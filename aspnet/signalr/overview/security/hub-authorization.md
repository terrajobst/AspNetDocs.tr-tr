---
uid: signalr/overview/security/hub-authorization
title: SignalR hub 'Ları için kimlik doğrulaması ve yetkilendirme | Microsoft Docs
author: bradygaster
description: Bu konuda, hangi kullanıcıların veya rollerin hub yöntemlerine erişebileceğini nasıl kısıtlayabileceği açıklanmaktadır. Bu konuda kullanılan yazılım sürümleri .NET 4,5 SignalR ve Visual Studio 2013...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578920"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="a6c3d-104">SignalR Hub’ları için Kimlik Doğrulaması ve Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="a6c3d-104">Authentication and Authorization for SignalR Hubs</span></span>

<span data-ttu-id="a6c3d-105">, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a6c3d-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="a6c3d-106">Bu konuda, hangi kullanıcıların veya rollerin hub yöntemlerine erişebileceğini nasıl kısıtlayabileceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-106">This topic describes how to restrict which users or roles can access hub methods.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="a6c3d-107">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="a6c3d-107">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="a6c3d-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a6c3d-108">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="a6c3d-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="a6c3d-109">.NET 4.5</span></span>
> - <span data-ttu-id="a6c3d-110">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="a6c3d-110">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="a6c3d-111">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="a6c3d-111">Previous versions of this topic</span></span>
>
> <span data-ttu-id="a6c3d-112">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="a6c3d-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="a6c3d-113">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="a6c3d-113">Questions and comments</span></span>
>
> <span data-ttu-id="a6c3d-114">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="a6c3d-115">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="a6c3d-116">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="a6c3d-116">Overview</span></span>

<span data-ttu-id="a6c3d-117">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="a6c3d-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a6c3d-118">Yetkilendir özniteliği</span><span class="sxs-lookup"><span data-stu-id="a6c3d-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="a6c3d-119">Tüm Hub 'lar için kimlik doğrulaması gerektir</span><span class="sxs-lookup"><span data-stu-id="a6c3d-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="a6c3d-120">Özelleştirilmiş yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="a6c3d-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="a6c3d-121">Kimlik doğrulama bilgilerini istemcilere geçir</span><span class="sxs-lookup"><span data-stu-id="a6c3d-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="a6c3d-122">.NET istemcileri için kimlik doğrulama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="a6c3d-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="a6c3d-123">Forms kimlik doğrulaması ile tanımlama bilgisi</span><span class="sxs-lookup"><span data-stu-id="a6c3d-123">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="a6c3d-124">Windows Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a6c3d-124">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="a6c3d-125">Bağlantı üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="a6c3d-125">Connection header</span></span>](#header)
    - [<span data-ttu-id="a6c3d-126">Sertifika</span><span class="sxs-lookup"><span data-stu-id="a6c3d-126">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="a6c3d-127">Yetkilendir özniteliği</span><span class="sxs-lookup"><span data-stu-id="a6c3d-127">Authorize attribute</span></span>

<span data-ttu-id="a6c3d-128">SignalR, bir hub veya yönteme hangi kullanıcıların veya rollerin erişebileceğini belirtmek için [Yetkilendir](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) özniteliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-128">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="a6c3d-129">Bu öznitelik `Microsoft.AspNet.SignalR` ad alanında bulunur.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="a6c3d-130">`Authorize` özniteliğini bir hub 'daki bir hub 'a ya da belirli yöntemlere uygularsınız.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="a6c3d-131">`Authorize` özniteliğini bir hub sınıfına uyguladığınızda, belirtilen yetkilendirme gereksinimi, hub 'daki tüm yöntemlere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="a6c3d-132">Bu konu, uygulayabileceğiniz farklı türlerdeki yetkilendirme gereksinimlerine örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="a6c3d-133">`Authorize` özniteliği olmadan bağlı istemci, hub üzerindeki herhangi bir genel yönteme erişebilir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="a6c3d-134">Web uygulamanızda "admin" adlı bir rol tanımladıysanız, yalnızca bu roldeki kullanıcıların aşağıdaki kodla bir hub 'a erişebileceğini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="a6c3d-135">Ya da bir hub 'ın tüm kullanıcılar için kullanılabilir bir yöntem içerdiğini ve yalnızca kimliği doğrulanmış kullanıcılar tarafından kullanılabilen ikinci bir yöntemi aşağıda gösterildiği gibi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="a6c3d-136">Aşağıdaki örneklerde farklı yetkilendirme senaryoları ele verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a6c3d-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="a6c3d-137">`[Authorize]` – yalnızca kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="a6c3d-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="a6c3d-138">`[Authorize(Roles = "Admin,Manager")]` – yalnızca belirtilen rollerdeki kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="a6c3d-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="a6c3d-139">`[Authorize(Users = "user1,user2")]` – yalnızca belirtilen kullanıcı adlarına sahip kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="a6c3d-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="a6c3d-140">`[Authorize(RequireOutgoing=false)]` – yalnızca kimliği doğrulanmış kullanıcılar hub 'ı çağırabilir, ancak sunucudan istemcilere geri çağrılar bir ileti gönderebildiği ancak diğerlerinin iletiyi alabileceği gibi yetkilendirme ile sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="a6c3d-141">Requiregiden özelliği, hub içindeki bireyler yöntemlerine değil, yalnızca tüm Hub 'a uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="a6c3d-142">Requiregiden değeri false olarak ayarlandığında, yalnızca yetkilendirme gereksinimini karşılayan kullanıcılar sunucudan çağırılır.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="a6c3d-143">Tüm Hub 'lar için kimlik doğrulaması gerektir</span><span class="sxs-lookup"><span data-stu-id="a6c3d-143">Require authentication for all hubs</span></span>

<span data-ttu-id="a6c3d-144">Uygulama başladığında [requiauthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) metodunu çağırarak uygulamanızdaki tüm Hub 'lar ve hub yöntemleri için kimlik doğrulaması yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="a6c3d-145">Birden çok hub olduğunda ve bunların tümü için bir kimlik doğrulama gereksinimini zorlamak istediğinizde bu yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="a6c3d-146">Bu yöntemde rol, Kullanıcı veya giden yetkilendirme için gereksinimleri belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="a6c3d-147">Yalnızca hub yöntemlerine erişimin kimliği doğrulanmış kullanıcılarla kısıtlanmasını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="a6c3d-148">Bununla birlikte, ek gereksinimler belirtmek için yine de, yetkilendirme özniteliğini hub 'lara veya yöntemlere uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="a6c3d-149">Bir öznitelikte belirttiğiniz gereksinim, temel kimlik doğrulaması gereksinimine eklenir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="a6c3d-150">Aşağıdaki örnek, tüm Hub yöntemlerini kimliği doğrulanmış kullanıcılarla kısıtlayan bir başlangıç dosyası gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="a6c3d-151">Bir SignalR isteği işlendikten sonra `RequireAuthentication()` yöntemini çağırırsanız, SignalR bir `InvalidOperationException` özel durumu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="a6c3d-152">İşlem hattı çağrıldıktan sonra HubPipeline öğesine bir modül ekleyemediği için SignalR bu özel durumu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="a6c3d-153">Önceki örnekte, ilk isteğin işlenmesinden önce bir kez yürütülen `Configuration` yönteminde `RequireAuthentication` yönteminin çağrılması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="a6c3d-154">Özelleştirilmiş yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="a6c3d-154">Customized authorization</span></span>

<span data-ttu-id="a6c3d-155">Yetkilendirmenin nasıl belirlendiğini özelleştirmeniz gerekiyorsa, `AuthorizeAttribute` türeten bir sınıf oluşturabilir ve [userauthorization](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) metodunu geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="a6c3d-156">Her istek için, SignalR kullanıcının isteği tamamlamaya yetkili olup olmadığını belirlemede bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="a6c3d-157">Geçersiz kılınan yöntemde, yetkilendirme senaryonuz için gerekli mantığı sağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="a6c3d-158">Aşağıdaki örnek, talep tabanlı kimlik aracılığıyla yetkilendirmeyi nasıl zorlayacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="a6c3d-159">Kimlik doğrulama bilgilerini istemcilere geçir</span><span class="sxs-lookup"><span data-stu-id="a6c3d-159">Pass authentication information to clients</span></span>

<span data-ttu-id="a6c3d-160">İstemci üzerinde çalışan koddaki kimlik doğrulama bilgilerini kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="a6c3d-161">İstemci üzerindeki yöntemleri çağırırken gerekli bilgileri geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="a6c3d-162">Örneğin, bir sohbet uygulaması yöntemi, aşağıda gösterildiği gibi bir ileti gönderen kişinin kullanıcı adına bir parametre olarak geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="a6c3d-163">Ya da, aşağıda gösterildiği gibi, kimlik doğrulama bilgilerini temsil eden bir nesne oluşturabilir ve bu nesneyi bir parametre olarak geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="a6c3d-164">Kötü niyetli bir Kullanıcı bu istemciden gelen bir isteği taklit etmek için onu kullanabilmesi için, bir istemcinin bağlantı kimliğini asla diğer istemcilere iletmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="a6c3d-165">.NET istemcileri için kimlik doğrulama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="a6c3d-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="a6c3d-166">Bir konsol uygulaması gibi, kimliği doğrulanmış kullanıcılarla sınırlı bir hub ile etkileşime geçen bir .NET istemciniz varsa, kimlik doğrulama bilgilerini bir tanımlama bilgisine, bağlantı başlığına veya bir sertifikaya geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="a6c3d-167">Bu bölümdeki örneklerde, kullanıcının kimliğini doğrulamak için bu farklı yöntemlerin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="a6c3d-168">Bunlar tam işlevli SignalR uygulamaları değildir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="a6c3d-169">SignalR ile .NET istemcileri hakkında daha fazla bilgi için bkz. [hub API Kılavuzu-.NET istemcisi](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="a6c3d-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="a6c3d-170">Tanımlama Bilgisi</span><span class="sxs-lookup"><span data-stu-id="a6c3d-170">Cookie</span></span>

<span data-ttu-id="a6c3d-171">.NET istemciniz ASP.NET Forms kimlik doğrulaması kullanan bir hub ile etkileşime geçtiğinde, bağlantıda kimlik doğrulama tanımlama bilgisini el ile ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="a6c3d-172">Tanımlama bilgisini, [Hubconnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) nesnesindeki `CookieContainer` özelliğine eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="a6c3d-173">Aşağıdaki örnek, bir Web sayfasından kimlik doğrulama tanımlama bilgisi alan ve bu tanımlama bilgisini bağlantıya ekleyen bir konsol uygulamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="a6c3d-174">Konsol uygulaması, aşağıdaki arka plan kod dosyasını içeren boş bir sayfaya başvuruda bulunmak için kimlik bilgilerini <strong>www.contoso.com/RemoteLogin</strong> adresine gönderir.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-174">The console app posts the credentials to <strong>www.contoso.com/RemoteLogin</strong> which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="a6c3d-175">Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a6c3d-175">Windows authentication</span></span>

<span data-ttu-id="a6c3d-176">Windows kimlik doğrulamasını kullanırken, [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) özelliğini kullanarak geçerli kullanıcının kimlik bilgilerini geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="a6c3d-177">DefaultCredentials değeri için bağlantı kimlik bilgilerini ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="a6c3d-178">Bağlantı üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="a6c3d-178">Connection header</span></span>

<span data-ttu-id="a6c3d-179">Uygulamanız tanımlama bilgilerini kullanmıyor ise, Kullanıcı bilgilerini bağlantı üst bilgisinde geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="a6c3d-180">Örneğin, bağlantı üst bilgisinde bir belirteç geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="a6c3d-181">Ardından, hub 'da kullanıcının belirtecini doğrularsınız.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="a6c3d-182">Sertifika</span><span class="sxs-lookup"><span data-stu-id="a6c3d-182">Certificate</span></span>

<span data-ttu-id="a6c3d-183">Kullanıcıyı doğrulamak için bir istemci sertifikası geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="a6c3d-184">Bağlantıyı oluştururken sertifikayı eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="a6c3d-185">Aşağıdaki örnek, bağlantıya yalnızca bir istemci sertifikasının nasıl ekleneceğini gösterir. tam konsol uygulamasını göstermez.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="a6c3d-186">Sertifikayı oluşturmak için çeşitli farklı yollar sağlayan [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a6c3d-186">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
