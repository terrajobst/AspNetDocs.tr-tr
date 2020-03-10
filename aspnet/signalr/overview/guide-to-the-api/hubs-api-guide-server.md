---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR hub 'Ları API Kılavuzu-sunucuC#() | Microsoft Docs
author: bradygaster
description: Bu belgede, SignalR sürüm 2 için ASP.NET SignalR hub 'ı API 'sinin sunucu tarafını programlamaya yönelik bir giriş ve kod örnekleri içeren...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536752"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="48dd2-103">ASP.NET SignalR hub 'Ları API Kılavuzu-sunucuC#()</span><span class="sxs-lookup"><span data-stu-id="48dd2-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="48dd2-104">by [Patrick Fletu](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="48dd2-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="48dd2-105">Bu belgede, SignalR sürüm 2 için ASP.NET SignalR hub 'ı API 'sinin sunucu tarafını programlama konusunda bir giriş ve ortak seçenekleri gösteren kod örnekleri sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="48dd2-106">SignalR hub 'Ları API 'SI, uzak yordam çağrılarını (RPC) bir sunucudan, istemcilerden ve istemcilerden sunucuya bağlı hale getirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="48dd2-107">Sunucu kodu ' nda, istemciler tarafından çağrılabilen Yöntemler tanımlar ve istemcide çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="48dd2-108">İstemci kodunda, sunucudan çağrılabilen yöntemleri tanımlayabilir ve sunucuda çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="48dd2-109">SignalR, sizin için istemciden sunucuya sıhhi kını ele alır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="48dd2-110">SignalR Ayrıca kalıcı bağlantılar adlı alt düzey bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="48dd2-111">SignalR, hub 'Lar ve sürekli bağlantılara giriş için bkz. [SignalR 2 ' ye giriş](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="48dd2-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="48dd2-112">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="48dd2-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="48dd2-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="48dd2-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="48dd2-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="48dd2-114">.NET 4.5</span></span>
> - <span data-ttu-id="48dd2-115">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="48dd2-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="48dd2-116">Konu sürümleri</span><span class="sxs-lookup"><span data-stu-id="48dd2-116">Topic versions</span></span>
> 
> <span data-ttu-id="48dd2-117">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="48dd2-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="48dd2-118">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="48dd2-118">Questions and comments</span></span>
> 
> <span data-ttu-id="48dd2-119">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="48dd2-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="48dd2-120">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="48dd2-121">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="48dd2-121">Overview</span></span>

<span data-ttu-id="48dd2-122">Bu belgede aşağıdaki bölümler yer alır:</span><span class="sxs-lookup"><span data-stu-id="48dd2-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="48dd2-123">SignalR ara yazılımını kaydetme</span><span class="sxs-lookup"><span data-stu-id="48dd2-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="48dd2-124">/SignalR URL 'SI</span><span class="sxs-lookup"><span data-stu-id="48dd2-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="48dd2-125">SignalR seçeneklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="48dd2-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="48dd2-126">Hub sınıfları oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="48dd2-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="48dd2-127">Hub nesnesi ömrü</span><span class="sxs-lookup"><span data-stu-id="48dd2-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="48dd2-128">Camel-JavaScript istemcilerinde hub adlarının büyük küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="48dd2-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="48dd2-129">Birden çok hub</span><span class="sxs-lookup"><span data-stu-id="48dd2-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="48dd2-130">Kesin tür belirtilmiş hub 'Lar</span><span class="sxs-lookup"><span data-stu-id="48dd2-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="48dd2-131">Hub sınıfında istemcilerin çağırabilmeniz için yöntemler tanımlama</span><span class="sxs-lookup"><span data-stu-id="48dd2-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="48dd2-132">Camel-JavaScript istemcilerinde yöntem adlarının büyük küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="48dd2-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="48dd2-133">Zaman uyumsuz olarak yürütme</span><span class="sxs-lookup"><span data-stu-id="48dd2-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="48dd2-134">Aşırı yüklemeleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="48dd2-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="48dd2-135">Hub yöntemi etkinleştirmeleri üzerinden ilerlemeyi bildirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="48dd2-136">Hub sınıfından istemci yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="48dd2-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="48dd2-137">Hangi istemcilerin RPC alacağını seçme</span><span class="sxs-lookup"><span data-stu-id="48dd2-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="48dd2-138">Yöntem adları için derleme zamanı doğrulaması yok</span><span class="sxs-lookup"><span data-stu-id="48dd2-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="48dd2-139">Büyük/küçük harf duyarsız Yöntem adı eşleştirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="48dd2-140">Zaman uyumsuz yürütme</span><span class="sxs-lookup"><span data-stu-id="48dd2-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="48dd2-141">Hub sınıfından grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="48dd2-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="48dd2-142">Ekleme ve kaldırma yöntemlerinin zaman uyumsuz yürütmesi</span><span class="sxs-lookup"><span data-stu-id="48dd2-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="48dd2-143">Grup üyeliği kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="48dd2-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="48dd2-144">Tek Kullanıcı grupları</span><span class="sxs-lookup"><span data-stu-id="48dd2-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="48dd2-145">Hub sınıfında bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="48dd2-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="48dd2-146">OnConnected, OnConnected ve OnConnected çağrıldığında</span><span class="sxs-lookup"><span data-stu-id="48dd2-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="48dd2-147">Çağıran durum doldurulmamış</span><span class="sxs-lookup"><span data-stu-id="48dd2-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="48dd2-148">Bağlam özelliğinden istemci hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="48dd2-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="48dd2-149">İstemcilerle hub sınıfı arasında durum geçirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="48dd2-150">Hub sınıfında hataları işleme</span><span class="sxs-lookup"><span data-stu-id="48dd2-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="48dd2-151">İstemci yöntemlerini çağırma ve grupları hub sınıfı dışından yönetme</span><span class="sxs-lookup"><span data-stu-id="48dd2-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="48dd2-152">İstemci yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="48dd2-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="48dd2-153">Grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="48dd2-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="48dd2-154">İzlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="48dd2-155">Hub ardışık düzenini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="48dd2-156">İstemcilerin programtasyonu hakkındaki belgeler için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="48dd2-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="48dd2-157">SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi</span><span class="sxs-lookup"><span data-stu-id="48dd2-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="48dd2-158">SignalR hub 'Ları API Kılavuzu-.NET Istemcisi</span><span class="sxs-lookup"><span data-stu-id="48dd2-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="48dd2-159">SignalR 2 için sunucu bileşenleri yalnızca .NET 4,5 'de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="48dd2-160">.NET 4,0 çalıştıran sunucularda SignalR v1. x kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="48dd2-161">SignalR ara yazılımını kaydetme</span><span class="sxs-lookup"><span data-stu-id="48dd2-161">How to register SignalR middleware</span></span>

<span data-ttu-id="48dd2-162">İstemcilerin hub 'ınıza bağlanmak için kullanacağı yolu tanımlamak için, uygulama başladığında `MapSignalR` yöntemi çağırın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="48dd2-163">`MapSignalR`, `OwinExtensions` sınıfı için bir [genişletme yöntemidir](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) .</span><span class="sxs-lookup"><span data-stu-id="48dd2-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="48dd2-164">Aşağıdaki örnek, bir OWıN başlangıç sınıfı kullanarak SignalR hub yolunun nasıl tanımlanacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="48dd2-165">Bir ASP.NET MVC uygulamasına SignalR işlevselliği ekliyorsanız, SignalR yolunun diğer yollarla önce eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="48dd2-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="48dd2-166">Daha fazla bilgi için bkz. [öğretici: SignalR 2 ve MVC 5 Ile çalışmaya](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="48dd2-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="48dd2-167">/SignalR URL 'SI</span><span class="sxs-lookup"><span data-stu-id="48dd2-167">The /signalr URL</span></span>

<span data-ttu-id="48dd2-168">Varsayılan olarak, istemcilerin hub 'ınıza bağlanmak için kullanacağı yol URL 'SI "/SignalR" olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="48dd2-169">(Bu URL 'YI otomatik olarak oluşturulan JavaScript dosyası için olan "/SignalR/Hub" URL 'siyle karıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="48dd2-170">Oluşturulan ara sunucu hakkında daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-oluşturulan ara sunucu ve sizin için ne yapar](hubs-api-guide-javascript-client.md#genproxy).)</span><span class="sxs-lookup"><span data-stu-id="48dd2-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="48dd2-171">Bu temel URL 'YI SignalR için kullanılamaz hale getirmek için olağandışı durumlar olabilir; Örneğin, projenizde *SignalR* adlı bir klasörünüz var ve adı değiştirmek istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="48dd2-172">Bu durumda, aşağıdaki örneklerde gösterildiği gibi temel URL 'YI değiştirebilirsiniz (örnek kodda "/SignalR" değerini istediğiniz URL ile değiştirin).</span><span class="sxs-lookup"><span data-stu-id="48dd2-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="48dd2-173">**URL 'YI belirten sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="48dd2-174">**URL 'YI belirten JavaScript istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="48dd2-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="48dd2-175">**URL 'YI belirten JavaScript istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="48dd2-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="48dd2-176">**URL 'YI belirten .NET istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="48dd2-177">SignalR seçeneklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="48dd2-177">Configuring SignalR Options</span></span>

<span data-ttu-id="48dd2-178">`MapSignalR` yönteminin aşırı yüklemeleri, özel bir URL, özel bir bağımlılık Çözümleyicisi ve aşağıdaki seçenekleri belirtmenize olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="48dd2-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="48dd2-179">Tarayıcı istemcilerinden CORS veya JSONP kullanarak etki alanları arası çağrıları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="48dd2-180">Genellikle tarayıcı `http://contoso.com`bir sayfa yüklerse, SignalR bağlantısı aynı etki alanında, `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="48dd2-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="48dd2-181">`http://contoso.com` sayfa, etki alanları arası bağlantı olan `http://fabrikam.com/signalr`bir bağlantı yapıyorsa.</span><span class="sxs-lookup"><span data-stu-id="48dd2-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="48dd2-182">Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="48dd2-183">Daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-etki alanları arası bağlantı oluşturma](hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="48dd2-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="48dd2-184">Ayrıntılı hata iletilerini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="48dd2-185">Hata oluştuğunda, SignalR 'nin varsayılan davranışı istemcilere ne olduğuna ilişkin ayrıntıları içermeyen bir bildirim iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="48dd2-186">Kötü amaçlı kullanıcılar, uygulamanıza karşı saldırılara karşı bilgileri kullanabilabileceğinden, istemcilere ayrıntılı hata bilgileri gönderilmesi, üretimde önerilmez.</span><span class="sxs-lookup"><span data-stu-id="48dd2-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="48dd2-187">Sorun giderme için, bu seçeneği kullanarak daha fazla bilgilendirici hata raporlamayı geçici olarak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="48dd2-188">Otomatik olarak oluşturulan JavaScript proxy dosyalarını devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="48dd2-189">Varsayılan olarak, hub sınıflarınız için proxy 'leri olan bir JavaScript dosyası "/SignalR/Hub" URL 'sine yanıt olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="48dd2-190">JavaScript proxy 'lerini kullanmak istemiyorsanız veya bu dosyayı el ile oluşturmak ve istemcilerinizdeki fiziksel bir dosyaya başvurmak istiyorsanız, ara sunucu oluşturmayı devre dışı bırakmak için bu seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="48dd2-191">Daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-SignalR tarafından oluşturulan ara sunucu için fiziksel dosya oluşturma](hubs-api-guide-javascript-client.md#manualproxy).</span><span class="sxs-lookup"><span data-stu-id="48dd2-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="48dd2-192">Aşağıdaki örnek, SignalR bağlantı URL 'sinin ve bu seçeneklerin `MapSignalR` metoduna yapılan bir çağrıda nasıl ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="48dd2-193">Özel bir URL belirtmek için örnekteki "/SignalR" değerini kullanmak istediğiniz URL ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="48dd2-194">Hub sınıfları oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="48dd2-194">How to create and use Hub classes</span></span>

<span data-ttu-id="48dd2-195">Bir hub oluşturmak için, [Microsoft. Aspnet. SignalR. hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)' dan türetilen bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="48dd2-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="48dd2-196">Aşağıdaki örnekte, bir sohbet uygulaması için basit bir hub sınıfı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="48dd2-197">Bu örnekte, bağlı bir istemci `NewContosoChatMessage` yöntemini çağırabilir ve ne zaman yapıldığında, alınan veriler tüm bağlı istemcilere göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="48dd2-198">Hub nesnesi ömrü</span><span class="sxs-lookup"><span data-stu-id="48dd2-198">Hub object lifetime</span></span>

<span data-ttu-id="48dd2-199">Hub sınıfını örnekleyemezsiniz veya kendi kodunuzda kendi kodınızdan yöntemlerini çağıramazsınız; Her şey, SignalR hub 'ı tarafından sizin için yapılır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="48dd2-200">SignalR, bir istemcinin bağlandığı, bağlantısı kesilen veya sunucuya bir yöntem çağrısı yaptığı zaman gibi bir hub işlemini her işlemesi gerektiğinde hub sınıfınızın yeni bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="48dd2-201">Hub sınıfının örnekleri geçici olduğundan, bir sonraki yöntem çağrısından durumu korumak için bunları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="48dd2-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="48dd2-202">Sunucu istemciden bir yöntem çağrısı aldığında, hub sınıfınızın yeni bir örneği iletiyi işler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="48dd2-203">Birden çok bağlantı ve yöntem çağrısı aracılığıyla durumu korumak için, veritabanı veya hub sınıfında bir statik değişken veya `Hub`türetmeyen farklı bir sınıf gibi başka bir yöntem kullanın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="48dd2-204">Hub sınıfında statik değişken gibi bir yöntemi kullanarak verileri bellekte kalıcı hale getirilürse, uygulama etki alanı geri dönüştürüldüğünde veriler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="48dd2-205">Hub sınıfı dışında çalışan kendi kodlarınızdan istemcilere ileti göndermek istiyorsanız, bir hub sınıfı örneği oluşturarak bunu yapamazsınız, ancak hub sınıfınız için SignalR bağlam nesnesine bir başvuru alarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="48dd2-206">Daha fazla bilgi için, bu konunun ilerleyen kısımlarında [istemci yöntemlerini çağırma ve hub sınıfının dışından grupları yönetme](#callfromoutsidehub) konularına bakın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="48dd2-207">Camel-JavaScript istemcilerinde hub adlarının büyük küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="48dd2-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="48dd2-208">Varsayılan olarak, JavaScript istemcileri, sınıf adının Camel-cased bir sürümünü kullanarak hub 'Lara başvurur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="48dd2-209">SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="48dd2-210">Önceki örneğe JavaScript kodunda `contosoChatHub` adı verilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="48dd2-211">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="48dd2-212">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="48dd2-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="48dd2-213">İstemcilerin kullanması için farklı bir ad belirtmek istiyorsanız, `HubName` özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="48dd2-214">Bir `HubName` özniteliği kullandığınızda JavaScript istemcilerinde ortası örneğine bir ad değişikliği yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="48dd2-215">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="48dd2-216">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="48dd2-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="48dd2-217">Birden çok hub</span><span class="sxs-lookup"><span data-stu-id="48dd2-217">Multiple Hubs</span></span>

<span data-ttu-id="48dd2-218">Bir uygulamada birden çok hub sınıfı tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="48dd2-219">Bunu yaptığınızda bağlantı paylaşılır, ancak gruplar ayrıdır:</span><span class="sxs-lookup"><span data-stu-id="48dd2-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="48dd2-220">Tüm istemciler hizmetinize bir SignalR bağlantısı kurmak için aynı URL 'YI kullanır ("/SignalR" veya bir tane belirtilmişse özel URL 'niz) ve bu bağlantı, hizmet tarafından tanımlanan tüm Hub 'Lar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="48dd2-221">Tek bir sınıfta tüm Hub işlevlerini tanımlamaya kıyasla birden çok Hub için performans farkı yoktur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="48dd2-222">Tüm Hub 'Lar aynı HTTP istek bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="48dd2-223">Tüm Hub 'Lar aynı bağlantıyı paylaştığından, sunucunun aldığı tek HTTP istek bilgileri, SignalR bağlantısını kuran özgün HTTP isteğine gelir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="48dd2-224">Bir sorgu dizesi belirterek istemciden sunucuya bilgi geçirmek için bağlantı isteğini kullanırsanız, farklı hub 'Lara farklı sorgu dizeleri sağlayamıyorum.</span><span class="sxs-lookup"><span data-stu-id="48dd2-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="48dd2-225">Tüm Hub 'Lar aynı bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="48dd2-226">Oluşturulan JavaScript proxy 'leri dosyası, tek bir dosyadaki tüm Hub 'Lara ait proxy 'leri içerir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="48dd2-227">JavaScript proxy 'leri hakkında daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-oluşturulan ara sunucu ve sizin için ne yapar](hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="48dd2-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="48dd2-228">Gruplar, hub 'Lar içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="48dd2-229">SignalR 'de, bağlı istemcilerin alt kümelerine yayınlamak için adlandırılmış grupları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="48dd2-230">Gruplar her Hub için ayrı ayrı tutulur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="48dd2-231">Örneğin, "Administrators" adlı bir grup `ContosoChatHub` sınıfınız için bir istemci kümesi içerir ve aynı grup adı `StockTickerHub` sınıfınız için farklı bir istemci kümesine başvuracaktır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="48dd2-232">Kesin tür belirtilmiş hub 'Lar</span><span class="sxs-lookup"><span data-stu-id="48dd2-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="48dd2-233">İstemcinizin, kuruluşunuzun başvurmasıyla (ve hub yöntemlerinize IntelliSense 'i etkinleştirebileceğinden), hub yöntemlerinizi için bir arabirim tanımlamak için, hub 'ınızı `Hub`yerine `Hub<T>` (SignalR 2,1 ' de tanıtılan) türetirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48dd2-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="48dd2-234">Hub sınıfında istemcilerin çağırabilmeniz için yöntemler tanımlama</span><span class="sxs-lookup"><span data-stu-id="48dd2-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="48dd2-235">Merkezi üzerinde istemciden çağrılabilir olmasını istediğiniz bir yöntemi ortaya çıkarmak için aşağıdaki örneklerde gösterildiği gibi bir genel yöntem bildirin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="48dd2-236">Herhangi C# bir yöntemde yaptığınız gibi, karmaşık türler ve diziler dahil olmak üzere bir dönüş türü ve parametreleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="48dd2-237">Parametrelerde aldığınız veya çağırana geri döndürülen tüm veriler, istemci ile sunucu arasında JSON kullanılarak iletilir ve SignalR karmaşık nesnelerin ve nesne dizilerinin otomatik olarak bağlamasını işler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="48dd2-238">Camel-JavaScript istemcilerinde yöntem adlarının büyük küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="48dd2-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="48dd2-239">Varsayılan olarak, JavaScript istemcileri, yöntem adının Camel-cased bir sürümünü kullanarak Merkez yöntemlerine başvurur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="48dd2-240">SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="48dd2-241">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="48dd2-242">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="48dd2-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="48dd2-243">İstemcilerin kullanması için farklı bir ad belirtmek istiyorsanız, `HubMethodName` özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="48dd2-244">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="48dd2-245">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="48dd2-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="48dd2-246">Zaman uyumsuz olarak yürütme</span><span class="sxs-lookup"><span data-stu-id="48dd2-246">When to execute asynchronously</span></span>

<span data-ttu-id="48dd2-247">Yöntem uzun süre çalışabilir veya bir veritabanı araması veya bir Web hizmeti çağrısı gibi beklemeyi gerektirebilecek iş yapmak için, bir [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (`void` dönüşü yerine) veya [görev&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) nesnesi (`T` dönüş türü yerine) döndürerek hub yöntemini zaman uyumsuz yapın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="48dd2-248">Yönteminden bir `Task` nesnesi döndürdüğünüzde, SignalR `Task` tamamlanmasını bekler ve sarmalanmamış sonucu istemciye geri gönderir. bu nedenle, istemcide yöntem çağrısını nasıl kodlayabilmeniz fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="48dd2-249">Bir hub yönteminin zaman uyumsuz yapılması, WebSocket aktarımını kullandığında bağlantının engellenmesini önler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="48dd2-250">Bir hub yöntemi zaman uyumlu olarak yürütülüyorsa ve aktarım WebSocket ise, hub yöntemi tamamlanana kadar hub üzerindeki yöntemlerin sonraki çağrıları aynı istemciden engellenir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="48dd2-251">Aşağıdaki örnek, her iki sürümü de çağırmak için çalışan JavaScript istemci kodu tarafından zaman uyumlu veya zaman uyumsuz olarak çalışacak şekilde kodlanmış aynı yöntemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="48dd2-252">**K**</span><span class="sxs-lookup"><span data-stu-id="48dd2-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="48dd2-253">**En**</span><span class="sxs-lookup"><span data-stu-id="48dd2-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="48dd2-254">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="48dd2-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="48dd2-255">ASP.NET 4,5 ' de zaman uyumsuz yöntemlerin nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [ASP.NET MVC 4 Içinde zaman uyumsuz yöntemler kullanma](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="48dd2-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="48dd2-256">Aşırı yüklemeleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="48dd2-256">Defining Overloads</span></span>

<span data-ttu-id="48dd2-257">Bir yöntem için aşırı yüklemeleri tanımlamak istiyorsanız, her aşırı yüklemede parametre sayısı farklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="48dd2-258">Farklı parametre türleri belirterek bir aşırı yüklemeyi ayırt ediyorsanız, hub sınıfınız derlenir, ancak istemciler aşırı yüklemelerin birini çağırmaya çalıştığında, çalışma zamanında SignalR hizmeti bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="48dd2-259">Hub yöntemi etkinleştirmeleri üzerinden ilerlemeyi bildirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="48dd2-260">SignalR 2,1, .NET 4,5 ' de tanıtılan [ilerleme durumu raporlama deseninin](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) desteğini ekler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="48dd2-261">İlerleme raporlamayı uygulamak için, istemcinizin erişebileceği hub yönteminiz için bir `IProgress<T>` parametresi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="48dd2-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="48dd2-262">Uzun süre çalışan bir sunucu yöntemi yazarken, hub iş parçacığını engellemek yerine zaman uyumsuz/await gibi zaman uyumsuz bir programlama deseninin kullanılması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="48dd2-263">Hub sınıfından istemci yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="48dd2-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="48dd2-264">Sunucudan istemci yöntemlerini çağırmak için, hub sınıfınızın bir yönteminde `Clients` özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="48dd2-265">Aşağıdaki örnek, tüm bağlı istemcilerde `addNewMessageToPage` çağıran sunucu kodunu ve bir JavaScript istemcisinde yöntemi tanımlayan istemci kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="48dd2-266">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="48dd2-267">İstemci yöntemini çağırmak zaman uyumsuz bir işlemdir ve bir `Task`döndürür.</span><span class="sxs-lookup"><span data-stu-id="48dd2-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="48dd2-268">`await`kullanın:</span><span class="sxs-lookup"><span data-stu-id="48dd2-268">Use `await`:</span></span>

* <span data-ttu-id="48dd2-269">İletinin hatasız gönderildiğinden emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="48dd2-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="48dd2-270">Bir try-catch bloğunda yakalama ve işleme hatalarını etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="48dd2-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="48dd2-271">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="48dd2-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="48dd2-272">İstemci yönteminden bir dönüş değeri alamazsınız; `int x = Clients.All.add(1,1)` gibi sözdizimi çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="48dd2-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="48dd2-273">Parametreler için karmaşık türler ve diziler belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="48dd2-274">Aşağıdaki örnek, bir yöntem parametresinde istemciye karmaşık bir tür geçirir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="48dd2-275">**Karmaşık bir nesne kullanarak istemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="48dd2-276">**Karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="48dd2-277">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="48dd2-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="48dd2-278">Hangi istemcilerin RPC alacağını seçme</span><span class="sxs-lookup"><span data-stu-id="48dd2-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="48dd2-279">Clients özelliği, hangi istemcilerin RPC alacağını belirtmek için çeşitli seçenekler sağlayan bir [Hubconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) nesnesi döndürür:</span><span class="sxs-lookup"><span data-stu-id="48dd2-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="48dd2-280">Bağlanan tüm istemciler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="48dd2-281">Yalnızca çağıran istemci.</span><span class="sxs-lookup"><span data-stu-id="48dd2-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="48dd2-282">Çağıran istemci dışındaki tüm istemciler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="48dd2-283">Bağlantı KIMLIĞIYLE tanımlanan belirli bir istemci.</span><span class="sxs-lookup"><span data-stu-id="48dd2-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="48dd2-284">Bu örnek, çağıran istemcide `addContosoChatMessageToPage` çağırır ve `Clients.Caller`ile aynı etkiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="48dd2-285">Belirtilen istemciler dışındaki tüm bağlı istemciler, bağlantı KIMLIĞIYLE tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="48dd2-286">Belirtilen bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="48dd2-287">Belirtilen bir gruptaki, belirtilen istemciler hariç, bağlantı KIMLIĞIYLE tanımlanan tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="48dd2-288">Çağıran istemci hariç, belirtilen bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="48dd2-289">Kullanıcı kimliği tarafından tanımlanan belirli bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="48dd2-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="48dd2-290">Varsayılan olarak, bu `IPrincipal.Identity.Name`, ancak [genel ana bilgisayarıyla bir ıuserıdprovider uygulaması kaydedilerek](mapping-users-to-connections.md#IUserIdProvider)değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="48dd2-291">Bir bağlantı kimlikleri listesindeki tüm istemciler ve gruplar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="48dd2-292">Grupların listesi.</span><span class="sxs-lookup"><span data-stu-id="48dd2-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="48dd2-293">Ada göre bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="48dd2-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="48dd2-294">Kullanıcı adlarının bir listesi (SignalR 2,1 ' de tanıtılan).</span><span class="sxs-lookup"><span data-stu-id="48dd2-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="48dd2-295">Yöntem adları için derleme zamanı doğrulaması yok</span><span class="sxs-lookup"><span data-stu-id="48dd2-295">No compile-time validation for method names</span></span>

<span data-ttu-id="48dd2-296">Belirttiğiniz Yöntem adı dinamik bir nesne olarak yorumlanır, yani bunun için IntelliSense veya derleme zamanı doğrulaması yoktur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="48dd2-297">İfade çalışma zamanında değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="48dd2-298">Yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerlerini istemciye gönderir ve istemcinin adıyla eşleşen bir yöntemi varsa, bu yöntem çağrılır ve parametre değerleri kendisine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="48dd2-299">İstemcide eşleşen bir yöntem bulunamazsa, hiçbir hata oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="48dd2-300">İstemci yöntemini çağırdığınızda SignalR 'nin arka planda istemciye ilettiği verilerin biçimi hakkında daha fazla bilgi için bkz. [SignalR 'ye giriş](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="48dd2-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="48dd2-301">Büyük/küçük harf duyarsız Yöntem adı eşleştirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="48dd2-302">Yöntem adı eşleştirme, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="48dd2-303">Örneğin, sunucusundaki `Clients.All.addContosoChatMessageToPage`, istemcide `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`veya `addContosoChatMessageToPage` yürütülür.</span><span class="sxs-lookup"><span data-stu-id="48dd2-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="48dd2-304">Zaman uyumsuz yürütme</span><span class="sxs-lookup"><span data-stu-id="48dd2-304">Asynchronous execution</span></span>

<span data-ttu-id="48dd2-305">Çağırdığınız yöntem zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="48dd2-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="48dd2-306">Bir istemciye yönelik bir yöntem çağrısından sonra gelen herhangi bir kod, sonraki kod satırlarının Yöntem tamamlanmasını beklemesi gerekmediği takdirde, SignalR 'nin istemcilere veri aktarma işleminin bitmesini beklemeden hemen yürütülür.</span><span class="sxs-lookup"><span data-stu-id="48dd2-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="48dd2-307">Aşağıdaki kod örneği, iki istemci yönteminin sırayla nasıl yürütüleceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="48dd2-308">**Await kullanma (.NET 4,5)**</span><span class="sxs-lookup"><span data-stu-id="48dd2-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="48dd2-309">Bir sonraki kod satırından önce istemci yöntemi bitene kadar beklemek için `await` kullanırsanız, bu, istemcilerin bir sonraki kod çalıştırılmadan önce iletiyi gerçekten alacağını göstermez.</span><span class="sxs-lookup"><span data-stu-id="48dd2-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="48dd2-310">Bir istemci yöntemi çağrısının "tamamlama" işlemi, SignalR 'nin iletiyi göndermek için gereken her şeyi yaptığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="48dd2-311">İstemcilerin iletiyi aldığını doğrulamaya ihtiyacınız varsa, o mekanizmayı kendiniz programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="48dd2-312">Örneğin, hub 'da bir `MessageReceived` yöntemi kod, istemci üzerindeki `addContosoChatMessageToPage` yönteminde, istemcide yapmanız gereken herhangi bir işi yaptıktan sonra `MessageReceived` çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="48dd2-313">Hub 'daki `MessageReceived`, gerçek istemci alımı ve özgün yöntem çağrısının işlenmesine bağlı olarak herhangi bir işi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="48dd2-314">Yöntem adı olarak bir dize değişkeni kullanma</span><span class="sxs-lookup"><span data-stu-id="48dd2-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="48dd2-315">Bir istemci yöntemini, yöntem adı olarak bir dize değişkeni kullanarak çağırmak istiyorsanız, `Clients.All` (veya `Clients.Others`, `Clients.Caller`, vb.) `IClientProxy` ve sonra [Invoke (MethodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="48dd2-316">Hub sınıfından grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="48dd2-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="48dd2-317">SignalR içindeki gruplar, bağlı istemcilerin belirtilen alt kümelerine ileti yayınlamak için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="48dd2-318">Bir grup herhangi bir sayıda istemciye sahip olabilir ve bir istemci herhangi bir sayıda grubun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="48dd2-319">Grup üyeliğini yönetmek için, hub sınıfının `Groups` özelliği tarafından sunulan [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) ve [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="48dd2-320">Aşağıdaki örnek, istemci kodu tarafından çağrılan ve ardından bunları çağıran JavaScript istemci kodunun ardından, hub yöntemlerinde kullanılan `Groups.Add` ve `Groups.Remove` yöntemlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="48dd2-321">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="48dd2-322">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="48dd2-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="48dd2-323">Açıkça grup oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="48dd2-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="48dd2-324">Aslında bir grup, bir `Groups.Add`çağrısında adını ilk kez belirttiğinizde otomatik olarak oluşturulur ve içindeki üyeliğinden son bağlantıyı kaldırdığınızda silinir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="48dd2-325">Grup üyeliği listesi veya Grup listesi almak için API yok.</span><span class="sxs-lookup"><span data-stu-id="48dd2-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="48dd2-326">SignalR bir [yayın/alt modele](http://en.wikipedia.org/wiki/Publish/subscribe)göre istemcilere ve gruplara iletiler gönderir ve sunucu grup veya grup üyelikleri listesini korumaz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="48dd2-327">Bu, bir Web grubuna düğüm eklediğiniz her durumda, SignalR 'nin koruduğu tüm durumun yeni düğüme yayılması nedeniyle ölçeklenebilirliği en üst düzeye çıkarmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="48dd2-328">Ekleme ve kaldırma yöntemlerinin zaman uyumsuz yürütmesi</span><span class="sxs-lookup"><span data-stu-id="48dd2-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="48dd2-329">`Groups.Add` ve `Groups.Remove` yöntemleri zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="48dd2-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="48dd2-330">Bir gruba bir istemci eklemek ve grubu kullanarak istemciye hemen ileti göndermek istiyorsanız, `Groups.Add` yönteminin önce tamamlandığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="48dd2-331">Aşağıdaki kod örneği bunun nasıl yapılacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="48dd2-332">**Bir gruba istemci ekleme ve sonra bu istemciye mesajlaşma**</span><span class="sxs-lookup"><span data-stu-id="48dd2-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="48dd2-333">Grup üyeliği kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="48dd2-333">Group membership persistence</span></span>

<span data-ttu-id="48dd2-334">SignalR, kullanıcıları değil bağlantıları izler, bu nedenle Kullanıcı her bağlantı kurduğunda bir kullanıcının aynı grupta olmasını istiyorsanız, Kullanıcı her yeni bağlantı kurduğunda `Groups.Add` çağırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="48dd2-335">Geçici bir bağlantı kaybı sonrasında, bazı durumlarda SignalR bağlantıyı otomatik olarak geri yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="48dd2-336">Bu durumda, SignalR aynı bağlantıyı geri yüklüyor, yeni bir bağlantı oluşturmamalıdır ve istemcinin grup üyeliği otomatik olarak geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="48dd2-337">Bu durum, geçici kesme sunucu yeniden başlatma veya başarısızlık nedeniyle bile, grup üyelikleri de dahil olmak üzere her bir istemcinin bağlantı durumu istemciye yuvarlandığı için mümkündür.</span><span class="sxs-lookup"><span data-stu-id="48dd2-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="48dd2-338">Bir sunucu kapalıysa ve bağlantı zaman aşımına uğramadan önce yeni bir sunucu tarafından değiştirilirse, istemci otomatik olarak yeni sunucuya yeniden bağlanabilir ve üyesi olan gruplara yeniden kaydolabilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="48dd2-339">Bağlantı kesilirse veya bağlantı zaman aşımına uğrarsa ya da istemcinin bağlantısı kesildiğinde (örneğin, bir tarayıcı yeni bir sayfaya gittiğinde) bir bağlantı otomatik olarak geri yüklenemediğinde, grup üyelikleri kaybedilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="48dd2-340">Kullanıcı bir sonraki sefer bağlanışında yeni bir bağlantı olur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="48dd2-341">Aynı kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini sürdürmek için, uygulamanız kullanıcılar ve gruplar arasındaki ilişkilendirmeleri izlemek ve Kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini geri yüklemek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="48dd2-342">Bağlantılar ve yeniden bağlantılar hakkında daha fazla bilgi için, bu konunun ilerleyen kısımlarında yer alarak [Merkez sınıfında bağlantı ömrü olaylarını işleme](#connectionlifetime) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="48dd2-343">Tek Kullanıcı grupları</span><span class="sxs-lookup"><span data-stu-id="48dd2-343">Single-user groups</span></span>

<span data-ttu-id="48dd2-344">SignalR kullanan uygulamalar genellikle hangi kullanıcının bir ileti gönderdiğini ve hangi kullanıcıların bir ileti aldıklarını bilmek için kullanıcılar ve bağlantılar arasındaki ilişkilendirmeleri takip etmelidir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="48dd2-345">Gruplar, bunu yapmak için yaygın olarak kullanılan iki desenden birinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="48dd2-346">Tek Kullanıcı grupları.</span><span class="sxs-lookup"><span data-stu-id="48dd2-346">Single-user groups.</span></span>

    <span data-ttu-id="48dd2-347">Kullanıcı adını Grup adı olarak belirtebilir ve Kullanıcı her bağlandığında veya yeniden bağlandığında geçerli bağlantı KIMLIĞINI gruba ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="48dd2-348">Gruba göndereceğiniz kullanıcıya ileti göndermek için.</span><span class="sxs-lookup"><span data-stu-id="48dd2-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="48dd2-349">Bu yöntemin bir dezavantajı, grubun, kullanıcının çevrimiçi veya çevrimdışı olduğunu anlamak için bir yol sağlamamasıdır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="48dd2-350">Kullanıcı adlarıyla bağlantı kimlikleri arasındaki ilişkilendirmeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="48dd2-351">Her Kullanıcı adı ile bir veya daha fazla bağlantı kimliği arasında bir ilişki veya bir sözlükte veya veritabanında bir ilişki saklayabilir ve Kullanıcı her bağlanıp bağlantısı kesildiğinde depolanan verileri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="48dd2-352">Kullanıcıya ileti göndermek için bağlantı kimliklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="48dd2-353">Bu yöntemin bir dezavantajı daha fazla bellek kaplar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="48dd2-354">Hub sınıfında bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="48dd2-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="48dd2-355">Bağlantı ömrü olaylarının işlenmesinin tipik nedenleri, bir kullanıcının bağlanıp bağlanmadığını ve Kullanıcı adları ile bağlantı kimlikleri arasındaki ilişkilendirmeyi takip etmesidir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="48dd2-356">İstemciler bağlandığında veya bağlantıyı kestikten sonra kendi kodunuzu çalıştırmak için, aşağıdaki örnekte gösterildiği gibi hub sınıfının `OnConnected`, `OnDisconnected`ve `OnReconnected` sanal yöntemlerini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="48dd2-357">OnConnected, OnConnected ve OnConnected çağrıldığında</span><span class="sxs-lookup"><span data-stu-id="48dd2-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="48dd2-358">Her tarayıcı yeni bir sayfaya gittiğinde, yeni bir bağlantı kurulması gerekir. Bu, SignalR 'in, `OnDisconnected` yöntemi ve ardından `OnConnected` yöntemi tarafından yürütüleceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="48dd2-359">SignalR yeni bir bağlantı oluşturulduğunda her zaman yeni bir bağlantı KIMLIĞI oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="48dd2-360">`OnReconnected` yöntemi, bir kablonun geçici olarak kesilmesi ve bağlantı zaman aşımına uğramadan önce yeniden bağlanması gibi, SignalR 'nin otomatik olarak kurtarabileceği bir bağlantıda geçici bir kesme olduğunda çağrılır. `OnDisconnected` yöntemi, istemcinin bağlantısı kesildiğinde çağrılır ve bir tarayıcı yeni bir sayfaya gittiğinde, SignalR otomatik olarak yeniden bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="48dd2-361">Bu nedenle, belirli bir istemci için olası bir olay dizisi `OnConnected`, `OnReconnected``OnDisconnected`; ya da `OnConnected``OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="48dd2-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="48dd2-362">Belirli bir bağlantı için sıra `OnConnected`, `OnDisconnected``OnReconnected` görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="48dd2-363">`OnDisconnected` yöntemi, bir sunucunun kapanması ya da uygulama etki alanının geri dönüştürülmesi gibi bazı senaryolarda çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="48dd2-364">Başka bir sunucu satır üzerine geldiğinde veya uygulama etki alanının geri dönüşümü tamamlandığında, bazı istemciler `OnReconnected` olayı yeniden oluşturabilir ve tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="48dd2-365">Daha fazla bilgi için bkz. [SignalR 'de bağlantı ömrü olaylarını anlama ve işleme](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="48dd2-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="48dd2-366">Çağıran durum doldurulmamış</span><span class="sxs-lookup"><span data-stu-id="48dd2-366">Caller state not populated</span></span>

<span data-ttu-id="48dd2-367">Bağlantı ömrü olay işleyicisi yöntemleri sunucudan çağrılır, bu, istemcideki `state` nesnesine yerleştirdiğiniz herhangi bir durumun sunucudaki `Caller` özelliğinde doldurulmayacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="48dd2-368">`state` nesnesi ve `Caller` özelliği hakkında daha fazla bilgi için, bu konunun ilerleyen kısımlarında [istemciler ve hub sınıfı arasında durum geçirme](#passstate) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="48dd2-369">Bağlam özelliğinden istemci hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="48dd2-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="48dd2-370">İstemci hakkında bilgi almak için, hub sınıfının `Context` özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="48dd2-371">`Context` özelliği, aşağıdaki bilgilere erişim sağlayan bir [Hubcallercontext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) nesnesi döndürür:</span><span class="sxs-lookup"><span data-stu-id="48dd2-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="48dd2-372">Çağıran istemcinin bağlantı kimliği.</span><span class="sxs-lookup"><span data-stu-id="48dd2-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="48dd2-373">Bağlantı KIMLIĞI, SignalR tarafından atanan bir GUID 'dir (değeri kendi kodunuzda belirtemezsiniz).</span><span class="sxs-lookup"><span data-stu-id="48dd2-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="48dd2-374">Her bağlantı için bir bağlantı KIMLIĞI vardır ve uygulamanızda birden çok hub varsa, tüm Hub 'Lar tarafından aynı bağlantı KIMLIĞI kullanılır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="48dd2-375">HTTP üstbilgisi verileri.</span><span class="sxs-lookup"><span data-stu-id="48dd2-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="48dd2-376">Ayrıca, `Context.Headers`HTTP üst bilgilerini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="48dd2-377">Aynı şey için birden çok başvuru olmasının nedeni `Context.Headers` ilk olarak oluşturulmuştur, `Context.Request` özelliği daha sonra eklenmiştir ve `Context.Headers` geriye dönük uyumluluk için tutulmuştur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="48dd2-378">Sorgu dizesi verileri.</span><span class="sxs-lookup"><span data-stu-id="48dd2-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="48dd2-379">`Context.QueryString`sorgu dizesi verilerini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="48dd2-380">Bu özelliğe alacağınız sorgu dizesi, SignalR bağlantısını oluşturan HTTP isteğiyle birlikte kullanılmış olan bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="48dd2-381">İstemciden sunucuya istemci hakkında verileri geçirmek için kullanışlı bir yol olan bağlantıyı yapılandırarak istemciye sorgu dizesi parametreleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="48dd2-382">Aşağıdaki örnek, oluşturulan proxy 'yi kullandığınızda JavaScript istemcisine bir sorgu dizesi eklemenin bir yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="48dd2-383">Sorgu dizesi parametreleri ayarlama hakkında daha fazla bilgi için, [JavaScript](hubs-api-guide-javascript-client.md) ve [.net](hubs-api-guide-net-client.md) istemcileri için API kılavuzlarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="48dd2-384">Sorgu dizesi verilerinde bağlantı için kullanılan aktarım yöntemini, SignalR tarafından dahili olarak kullanılan bazı diğer değerlerle birlikte bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48dd2-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="48dd2-385">`transportMethod` değeri "webSockets", "serverSentEvents", "foreverFrame" veya "longPolling" olacaktır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="48dd2-386">Bu değeri `OnConnected` olay işleyicisi yönteminde denetlebileceğinizi unutmayın, bazı senaryolarda başlangıçta bağlantı için en son anlaşmalı aktarım yöntemi olmayan bir aktarım değeri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="48dd2-387">Bu durumda yöntem bir özel durum oluşturur ve daha sonra son taşıma yöntemi oluşturulduğunda yeniden çağrılacaktır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="48dd2-388">Özgü.</span><span class="sxs-lookup"><span data-stu-id="48dd2-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="48dd2-389">`Context.RequestCookies`tanımlama bilgilerini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="48dd2-390">Kullanıcı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="48dd2-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="48dd2-391">İstek için HttpContext nesnesi:</span><span class="sxs-lookup"><span data-stu-id="48dd2-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="48dd2-392">SignalR bağlantısı için `HttpContext` nesnesini almak üzere `HttpContext.Current` almak yerine bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="48dd2-393">İstemcilerle hub sınıfı arasında durum geçirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="48dd2-394">İstemci proxy 'si, her yöntem çağrısıyla sunucuya aktarılmasını istediğiniz verileri depolayabilmeniz için bir `state` nesnesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="48dd2-395">Sunucusunda, bu verilere istemciler tarafından çağrılan hub yöntemlerinde `Clients.Caller` özelliğindeki erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="48dd2-396">`Clients.Caller` özelliği, bağlantı ömrü olay işleyicisi yöntemleri `OnConnected`, `OnDisconnected`ve `OnReconnected`için doldurulmaz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="48dd2-397">`state` nesnesindeki verileri oluşturma veya güncelleştirme ve `Clients.Caller` özelliği her iki yönde de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="48dd2-398">Sunucudaki değerleri güncelleştirebilir ve istemciye geri geçirilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="48dd2-399">Aşağıdaki örnek, her yöntem çağrısıyla sunucuya iletilmek üzere durum depolayan JavaScript istemci kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="48dd2-400">Aşağıdaki örnek, bir .NET istemcisinde denk kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="48dd2-401">Hub sınıfınız içinde, `Clients.Caller` özelliğindeki bu verilere erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="48dd2-402">Aşağıdaki örnek, önceki örnekte başvurulan durumu alan kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="48dd2-403">Kalıcı duruma yönelik bu mekanizma, büyük miktarlarda veri için tasarlanmamıştır çünkü `state` veya `Clients.Caller` özelliğine yerleştirdiğiniz her şey, her yöntem çağrısı ile birlikte yuvarlama yaptığından.</span><span class="sxs-lookup"><span data-stu-id="48dd2-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="48dd2-404">Kullanıcı adları veya sayaçlar gibi daha küçük öğeler için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="48dd2-405">VB.NET veya türü kesin belirlenmiş bir hub 'da, çağıran durum nesnesine `Clients.Caller`üzerinden erişilemez; Bunun yerine `Clients.CallerState` kullanın (SignalR 2,1 ' de tanıtılan):</span><span class="sxs-lookup"><span data-stu-id="48dd2-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="48dd2-406">**İçinde CallerState kullanmaC#**</span><span class="sxs-lookup"><span data-stu-id="48dd2-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="48dd2-407">**Visual Basic 'de CallerState kullanma**</span><span class="sxs-lookup"><span data-stu-id="48dd2-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="48dd2-408">Hub sınıfında hataları işleme</span><span class="sxs-lookup"><span data-stu-id="48dd2-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="48dd2-409">Hub sınıfı yöntemleriniz içinde oluşan hataları işlemek için, ilk olarak, `await`kullanarak zaman uyumsuz işlemlerden (istemci yöntemlerini çağırma gibi) özel durumları "gözlemleyin".</span><span class="sxs-lookup"><span data-stu-id="48dd2-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="48dd2-410">Ardından aşağıdaki yöntemlerden birini veya daha fazlasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="48dd2-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="48dd2-411">Yöntem kodunuzu try-catch bloklarına sarın ve özel durum nesnesini günlüğe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="48dd2-412">Hata ayıklama amacıyla, özel durumu istemciye gönderebilirsiniz, ancak üretimde istemcilere ayrıntılı bilgi gönderilmesi için güvenlik nedenleriyle önerilmez.</span><span class="sxs-lookup"><span data-stu-id="48dd2-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="48dd2-413">[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) yöntemini Işleyen bir hub işlem hattı modülü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="48dd2-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="48dd2-414">Aşağıdaki örnek, hataları kaydeden bir işlem hattı modülünü ve ardından Startup.cs ' deki kodu hub ardışık düzenine çıkartır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="48dd2-415">`HubException` sınıfını kullanın (SignalR 2 ' de tanıtılan).</span><span class="sxs-lookup"><span data-stu-id="48dd2-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="48dd2-416">Bu hata herhangi bir hub çağrısından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="48dd2-417">`HubError` Oluşturucu bir dize iletisi ve ek hata verilerini depolamak için bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="48dd2-418">SignalR, özel durumu otomatik olarak serileştirmesini ve istemciye göndermesini, bu da hub yöntemi çağrısını reddetmek veya devretmek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="48dd2-419">Aşağıdaki kod örnekleri, bir hub çağrısı sırasında `HubException` oluşturmayı ve JavaScript ve .NET istemcilerindeki özel durumun nasıl işleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="48dd2-420">**HubException sınıfını gösteren sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="48dd2-421">**Bir hub 'da HubException oluşturma yanıtını gösteren JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="48dd2-422">**Bir hub 'da HubException oluşturma yanıtını gösteren .NET istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="48dd2-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="48dd2-423">Merkez ardışık düzen modülleri hakkında daha fazla bilgi için, bu konunun ilerleyen bölümlerinde hub işlem hattını [Özelleştirme](#hubpipeline) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="48dd2-424">İzlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-424">How to enable tracing</span></span>

<span data-ttu-id="48dd2-425">Sunucu tarafı izlemeyi etkinleştirmek için, aşağıdaki örnekte gösterildiği gibi, Web. config dosyanıza bir System. Diagnostics öğesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="48dd2-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="48dd2-426">Uygulamayı Visual Studio 'da çalıştırdığınızda, günlükleri **Çıkış** penceresinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="48dd2-427">İstemci yöntemlerini çağırma ve grupları hub sınıfı dışından yönetme</span><span class="sxs-lookup"><span data-stu-id="48dd2-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="48dd2-428">Hub sınıfınızın farklı bir sınıfından istemci yöntemlerini çağırmak için, Hub için SignalR bağlam nesnesine bir başvuru alın ve bunu istemci üzerindeki yöntemleri çağırmak veya grupları yönetmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="48dd2-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="48dd2-429">Aşağıdaki örnek `StockTicker` sınıfı, bağlam nesnesini alır, onu sınıfının bir örneğine depolar, sınıf örneğini statik bir özellikte depolar ve `StockTickerHub`adlı bir hub 'a bağlı istemcilerde `updateStockPrice` yöntemini çağırmak için singleton sınıfı örneğinden bağlamını kullanır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="48dd2-430">İçeriği uzun süreli bir nesnede birden çok kez kullanmanız gerekiyorsa, başvuruyu bir kez alın ve her seferinde yeniden almak yerine kaydedin.</span><span class="sxs-lookup"><span data-stu-id="48dd2-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="48dd2-431">Bağlam bir kez alındıktan sonra, SignalR 'nin, hub yöntemlerinizin istemci yöntemi etkinleştirmeleri haline gelen aynı sıradaki istemcilere ileti göndermesi güvence altına alınır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="48dd2-432">Bir hub için SignalR bağlamını nasıl kullanacağınızı gösteren bir öğretici için, bkz. [ASP.NET SignalR Ile sunucu yayını](../getting-started/tutorial-server-broadcast-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="48dd2-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="48dd2-433">İstemci yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="48dd2-433">Calling client methods</span></span>

<span data-ttu-id="48dd2-434">Hangi istemcilerin RPC alacağını belirtebilirsiniz, ancak bir hub sınıfından çağrı yaparken daha az seçeneğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="48dd2-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="48dd2-435">Bunun nedeni, bağlamın bir istemciden gelen belirli bir çağrıyla ilişkilendirilmediği, yani `Clients.Others`veya `Clients.Caller`ya da `Clients.OthersInGroup`gibi geçerli bağlantı KIMLIĞI hakkında bilgi gerektiren tüm yöntemler kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="48dd2-436">Aşağıdaki seçenekler mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="48dd2-436">The following options are available:</span></span>

- <span data-ttu-id="48dd2-437">Bağlanan tüm istemciler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="48dd2-438">Bağlantı KIMLIĞIYLE tanımlanan belirli bir istemci.</span><span class="sxs-lookup"><span data-stu-id="48dd2-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="48dd2-439">Belirtilen istemciler dışındaki tüm bağlı istemciler, bağlantı KIMLIĞIYLE tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="48dd2-440">Belirtilen bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="48dd2-441">Belirtilen bir gruptaki, belirtilen istemciler hariç, bağlantı KIMLIĞIYLE tanımlanan tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="48dd2-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="48dd2-442">Hub sınıfınızın metotlarından hub olmayan sınıfa çağrı yapıyorsanız, geçerli bağlantı KIMLIĞINI geçirebilir ve `Clients.Caller`, `Clients.Others`veya `Clients.OthersInGroup`benzetimini yapmak için `Clients.Client`, `Clients.AllExcept`veya `Clients.Group` ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="48dd2-443">Aşağıdaki örnekte, `MoveShapeHub` sınıfı bağlantı KIMLIĞINI `Broadcaster` sınıfına geçirir `Broadcaster` sınıfının `Clients.Others`benzetimini yapabilir.</span><span class="sxs-lookup"><span data-stu-id="48dd2-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="48dd2-444">Grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="48dd2-444">Managing group membership</span></span>

<span data-ttu-id="48dd2-445">Grupları yönetmek için bir hub sınıfında yaptığınız seçeneklerle aynı seçeneklere sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="48dd2-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="48dd2-446">Bir gruba istemci ekleme</span><span class="sxs-lookup"><span data-stu-id="48dd2-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="48dd2-447">Bir gruptan bir istemciyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="48dd2-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="48dd2-448">Hub ardışık düzenini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="48dd2-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="48dd2-449">SignalR, kendi kodunuzu hub işlem hattına eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="48dd2-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="48dd2-450">Aşağıdaki örnek, istemcisinde çağrılan her bir gelen yöntem çağrısını günlüğe kaydeden özel bir hub işlem hattı modülünü ve istemcide çağrılan giden yöntem çağrısını gösterir:</span><span class="sxs-lookup"><span data-stu-id="48dd2-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="48dd2-451">*Startup.cs* dosyasında aşağıdaki kod, modülü hub işlem hattında çalışacak şekilde kaydeder:</span><span class="sxs-lookup"><span data-stu-id="48dd2-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="48dd2-452">Geçersiz kılabileceğiniz birçok farklı yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="48dd2-452">There are many different methods that you can override.</span></span> <span data-ttu-id="48dd2-453">Tüm liste için bkz. [Hubpipelinemodule yöntemleri](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="48dd2-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
