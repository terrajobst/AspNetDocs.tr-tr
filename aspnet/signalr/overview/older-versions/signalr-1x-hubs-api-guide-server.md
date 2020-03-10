---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: ASP.NET SignalR hub 'Ları API Kılavuzu-sunucu (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bu belgede, SignalR sürüm 1,1 için ASP.NET SignalR hub API 'sinin sunucu tarafını programlama, kod örnekleri demonstratin...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579641"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a><span data-ttu-id="a9506-103">ASP.NET SignalR hub 'Ları API Kılavuzu-sunucu (SignalR 1. x)</span><span class="sxs-lookup"><span data-stu-id="a9506-103">ASP.NET SignalR Hubs API Guide - Server (SignalR 1.x)</span></span>

<span data-ttu-id="a9506-104">by [Patrick Fletu](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a9506-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="a9506-105">Bu belgede, SignalR sürüm 1,1 için ASP.NET SignalR hub 'ı API 'sinin sunucu tarafını programlama konusunda bir giriş ve ortak seçenekleri gösteren kod örnekleri sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a9506-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 1.1, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="a9506-106">SignalR hub 'Ları API 'SI, uzak yordam çağrılarını (RPC) bir sunucudan, istemcilerden ve istemcilerden sunucuya bağlı hale getirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9506-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="a9506-107">Sunucu kodu ' nda, istemciler tarafından çağrılabilen Yöntemler tanımlar ve istemcide çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="a9506-108">İstemci kodunda, sunucudan çağrılabilen yöntemleri tanımlayabilir ve sunucuda çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="a9506-109">SignalR, sizin için istemciden sunucuya sıhhi kını ele alır.</span><span class="sxs-lookup"><span data-stu-id="a9506-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="a9506-110">SignalR Ayrıca kalıcı bağlantılar adlı alt düzey bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="a9506-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="a9506-111">SignalR, hub 'Lar ve sürekli bağlantılara giriş veya tam bir SignalR uygulamasının nasıl oluşturulduğunu gösteren bir öğretici için bkz. [SignalR-Başlarken](index.md).</span><span class="sxs-lookup"><span data-stu-id="a9506-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="a9506-112">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="a9506-112">Overview</span></span>

<span data-ttu-id="a9506-113">Bu belgede aşağıdaki bölümler yer alır:</span><span class="sxs-lookup"><span data-stu-id="a9506-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="a9506-114">SignalR rotasını kaydetme ve SignalR seçeneklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a9506-114">How to register the SignalR route and configure SignalR options</span></span>](#route)

    - [<span data-ttu-id="a9506-115">/SignalR URL 'SI</span><span class="sxs-lookup"><span data-stu-id="a9506-115">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="a9506-116">SignalR seçeneklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a9506-116">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="a9506-117">Hub sınıfları oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="a9506-117">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="a9506-118">Hub nesnesi ömrü</span><span class="sxs-lookup"><span data-stu-id="a9506-118">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="a9506-119">Camel-JavaScript istemcilerinde hub adlarının büyük küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="a9506-119">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="a9506-120">Birden çok hub</span><span class="sxs-lookup"><span data-stu-id="a9506-120">Multiple Hubs</span></span>](#multiplehubs)
- [<span data-ttu-id="a9506-121">Hub sınıfında istemcilerin çağırabilmeniz için yöntemler tanımlama</span><span class="sxs-lookup"><span data-stu-id="a9506-121">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="a9506-122">Camel-JavaScript istemcilerinde yöntem adlarının büyük küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="a9506-122">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="a9506-123">Zaman uyumsuz olarak yürütme</span><span class="sxs-lookup"><span data-stu-id="a9506-123">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="a9506-124">Aşırı yüklemeleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="a9506-124">Defining overloads</span></span>](#overloads)
- [<span data-ttu-id="a9506-125">Hub sınıfından istemci yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="a9506-125">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="a9506-126">Hangi istemcilerin RPC alacağını seçme</span><span class="sxs-lookup"><span data-stu-id="a9506-126">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="a9506-127">Yöntem adları için derleme zamanı doğrulaması yok</span><span class="sxs-lookup"><span data-stu-id="a9506-127">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="a9506-128">Büyük/küçük harf duyarsız Yöntem adı eşleştirme</span><span class="sxs-lookup"><span data-stu-id="a9506-128">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="a9506-129">Zaman uyumsuz yürütme</span><span class="sxs-lookup"><span data-stu-id="a9506-129">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="a9506-130">Hub sınıfından grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="a9506-130">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="a9506-131">Ekleme ve kaldırma yöntemlerinin zaman uyumsuz yürütmesi</span><span class="sxs-lookup"><span data-stu-id="a9506-131">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="a9506-132">Grup üyeliği kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="a9506-132">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="a9506-133">Tek Kullanıcı grupları</span><span class="sxs-lookup"><span data-stu-id="a9506-133">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="a9506-134">Hub sınıfında bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="a9506-134">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="a9506-135">OnConnected, OnConnected ve OnConnected çağrıldığında</span><span class="sxs-lookup"><span data-stu-id="a9506-135">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="a9506-136">Çağıran durum doldurulmamış</span><span class="sxs-lookup"><span data-stu-id="a9506-136">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="a9506-137">Bağlam özelliğinden istemci hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="a9506-137">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="a9506-138">İstemcilerle hub sınıfı arasında durum geçirme</span><span class="sxs-lookup"><span data-stu-id="a9506-138">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="a9506-139">Hub sınıfında hataları işleme</span><span class="sxs-lookup"><span data-stu-id="a9506-139">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="a9506-140">İstemci yöntemlerini çağırma ve grupları hub sınıfı dışından yönetme</span><span class="sxs-lookup"><span data-stu-id="a9506-140">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="a9506-141">İstemci yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="a9506-141">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="a9506-142">Grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="a9506-142">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="a9506-143">İzlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a9506-143">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="a9506-144">Hub ardışık düzenini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="a9506-144">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="a9506-145">İstemcilerin programtasyonu hakkındaki belgeler için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="a9506-145">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="a9506-146">SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi</span><span class="sxs-lookup"><span data-stu-id="a9506-146">SignalR Hubs API Guide - JavaScript Client</span></span>](index.md)
- [<span data-ttu-id="a9506-147">SignalR hub 'Ları API Kılavuzu-.NET Istemcisi</span><span class="sxs-lookup"><span data-stu-id="a9506-147">SignalR Hubs API Guide - .NET Client</span></span>](index.md)

<span data-ttu-id="a9506-148">API başvuru konularına bağlantılar, API 'nin .NET 4,5 sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="a9506-148">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="a9506-149">.NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.</span><span class="sxs-lookup"><span data-stu-id="a9506-149">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a><span data-ttu-id="a9506-150">SignalR rotasını kaydetme ve SignalR seçeneklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a9506-150">How to register the SignalR route and configure SignalR options</span></span>

<span data-ttu-id="a9506-151">İstemcilerin hub 'ınıza bağlanmak için kullanacağı yolu tanımlamak için, uygulama başladığında [Maphubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a9506-151">To define the route that clients will use to connect to your Hub, call the [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="a9506-152">`MapHubs`, `System.Web.Routing.RouteCollection` sınıfı için bir [genişletme yöntemidir](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a9506-152">`MapHubs` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `System.Web.Routing.RouteCollection` class.</span></span> <span data-ttu-id="a9506-153">Aşağıdaki örnek, *küresel. asax* dosyasında SignalR hub yolunun nasıl tanımlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-153">The following example shows how to define the SignalR Hubs route in the *Global.asax* file.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

<span data-ttu-id="a9506-154">Bir ASP.NET MVC uygulamasına SignalR işlevselliği ekliyorsanız, SignalR yolunun diğer yollarla önce eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="a9506-154">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="a9506-155">Daha fazla bilgi için bkz. [öğretici: SignalR ve MVC 4 Ile çalışmaya](index.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="a9506-155">For more information, see [Tutorial: Getting Started with SignalR and MVC 4](index.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="a9506-156">/SignalR URL 'SI</span><span class="sxs-lookup"><span data-stu-id="a9506-156">The /signalr URL</span></span>

<span data-ttu-id="a9506-157">Varsayılan olarak, istemcilerin hub 'ınıza bağlanmak için kullanacağı yol URL 'SI "/SignalR" olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="a9506-157">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="a9506-158">(Bu URL 'YI otomatik olarak oluşturulan JavaScript dosyası için olan "/SignalR/Hub" URL 'siyle karıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="a9506-158">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="a9506-159">Oluşturulan ara sunucu hakkında daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-oluşturulan ara sunucu ve sizin için ne yapar](index.md).)</span><span class="sxs-lookup"><span data-stu-id="a9506-159">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).)</span></span>

<span data-ttu-id="a9506-160">Bu temel URL 'YI SignalR için kullanılamaz hale getirmek için olağandışı durumlar olabilir; Örneğin, projenizde *SignalR* adlı bir klasörünüz var ve adı değiştirmek istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-160">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="a9506-161">Bu durumda, aşağıdaki örneklerde gösterildiği gibi temel URL 'YI değiştirebilirsiniz (örnek kodda "/SignalR" değerini istediğiniz URL ile değiştirin).</span><span class="sxs-lookup"><span data-stu-id="a9506-161">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="a9506-162">**URL 'YI belirten sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="a9506-162">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

<span data-ttu-id="a9506-163">**URL 'YI belirten JavaScript istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a9506-163">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="a9506-164">**URL 'YI belirten JavaScript istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a9506-164">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

<span data-ttu-id="a9506-165">**URL 'YI belirten .NET istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="a9506-165">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="a9506-166">SignalR seçeneklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a9506-166">Configuring SignalR Options</span></span>

<span data-ttu-id="a9506-167">`MapHubs` yönteminin aşırı yüklemeleri, özel bir URL, özel bir bağımlılık Çözümleyicisi ve aşağıdaki seçenekleri belirtmenize olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="a9506-167">Overloads of the `MapHubs` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="a9506-168">Tarayıcı istemcilerinden etki alanları arası çağrıları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a9506-168">Enable cross-domain calls from browser clients.</span></span>

    <span data-ttu-id="a9506-169">Genellikle tarayıcı `http://contoso.com`bir sayfa yüklerse, SignalR bağlantısı aynı etki alanında, `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="a9506-169">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="a9506-170">`http://contoso.com` sayfa, etki alanları arası bağlantı olan `http://fabrikam.com/signalr`bir bağlantı yapıyorsa.</span><span class="sxs-lookup"><span data-stu-id="a9506-170">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="a9506-171">Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="a9506-171">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="a9506-172">Daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-etki alanları arası bağlantı oluşturma](index.md).</span><span class="sxs-lookup"><span data-stu-id="a9506-172">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](index.md).</span></span>
- <span data-ttu-id="a9506-173">Ayrıntılı hata iletilerini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a9506-173">Enable detailed error messages.</span></span>

    <span data-ttu-id="a9506-174">Hata oluştuğunda, SignalR 'nin varsayılan davranışı istemcilere ne olduğuna ilişkin ayrıntıları içermeyen bir bildirim iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="a9506-174">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="a9506-175">Kötü amaçlı kullanıcılar, uygulamanıza karşı saldırılara karşı bilgileri kullanabilabileceğinden, istemcilere ayrıntılı hata bilgileri gönderilmesi, üretimde önerilmez.</span><span class="sxs-lookup"><span data-stu-id="a9506-175">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="a9506-176">Sorun giderme için, bu seçeneği kullanarak daha fazla bilgilendirici hata raporlamayı geçici olarak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-176">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="a9506-177">Otomatik olarak oluşturulan JavaScript proxy dosyalarını devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="a9506-177">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="a9506-178">Varsayılan olarak, hub sınıflarınız için proxy 'leri olan bir JavaScript dosyası "/SignalR/Hub" URL 'sine yanıt olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a9506-178">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="a9506-179">JavaScript proxy 'lerini kullanmak istemiyorsanız veya bu dosyayı el ile oluşturmak ve istemcilerinizdeki fiziksel bir dosyaya başvurmak istiyorsanız, ara sunucu oluşturmayı devre dışı bırakmak için bu seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-179">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="a9506-180">Daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-SignalR tarafından oluşturulan ara sunucu için fiziksel dosya oluşturma](index.md).</span><span class="sxs-lookup"><span data-stu-id="a9506-180">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](index.md).</span></span>

<span data-ttu-id="a9506-181">Aşağıdaki örnek, SignalR bağlantı URL 'sinin ve bu seçeneklerin `MapHubs` metoduna yapılan bir çağrıda nasıl ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-181">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapHubs` method.</span></span> <span data-ttu-id="a9506-182">Özel bir URL belirtmek için örnekteki "/SignalR" değerini kullanmak istediğiniz URL ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a9506-182">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="a9506-183">Hub sınıfları oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="a9506-183">How to create and use Hub classes</span></span>

<span data-ttu-id="a9506-184">Bir hub oluşturmak için, [Microsoft. Aspnet. SignalR. hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)' dan türetilen bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9506-184">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="a9506-185">Aşağıdaki örnekte, bir sohbet uygulaması için basit bir hub sınıfı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a9506-185">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

<span data-ttu-id="a9506-186">Bu örnekte, bağlı bir istemci `NewContosoChatMessage` yöntemini çağırabilir ve ne zaman yapıldığında, alınan veriler tüm bağlı istemcilere göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="a9506-186">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="a9506-187">Hub nesnesi ömrü</span><span class="sxs-lookup"><span data-stu-id="a9506-187">Hub object lifetime</span></span>

<span data-ttu-id="a9506-188">Hub sınıfını örnekleyemezsiniz veya kendi kodunuzda kendi kodınızdan yöntemlerini çağıramazsınız; Her şey, SignalR hub 'ı tarafından sizin için yapılır.</span><span class="sxs-lookup"><span data-stu-id="a9506-188">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="a9506-189">SignalR, bir istemcinin bağlandığı, bağlantısı kesilen veya sunucuya bir yöntem çağrısı yaptığı zaman gibi bir hub işlemini her işlemesi gerektiğinde hub sınıfınızın yeni bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9506-189">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="a9506-190">Hub sınıfının örnekleri geçici olduğundan, bir sonraki yöntem çağrısından durumu korumak için bunları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="a9506-190">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="a9506-191">Sunucu istemciden bir yöntem çağrısı aldığında, hub sınıfınızın yeni bir örneği iletiyi işler.</span><span class="sxs-lookup"><span data-stu-id="a9506-191">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="a9506-192">Birden çok bağlantı ve yöntem çağrısı aracılığıyla durumu korumak için, veritabanı veya hub sınıfında bir statik değişken veya `Hub`türetmeyen farklı bir sınıf gibi başka bir yöntem kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9506-192">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="a9506-193">Hub sınıfında statik değişken gibi bir yöntemi kullanarak verileri bellekte kalıcı hale getirilürse, uygulama etki alanı geri dönüştürüldüğünde veriler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="a9506-193">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="a9506-194">Hub sınıfı dışında çalışan kendi kodlarınızdan istemcilere ileti göndermek istiyorsanız, bir hub sınıfı örneği oluşturarak bunu yapamazsınız, ancak hub sınıfınız için SignalR bağlam nesnesine bir başvuru alarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-194">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="a9506-195">Daha fazla bilgi için, bu konunun ilerleyen kısımlarında [istemci yöntemlerini çağırma ve hub sınıfının dışından grupları yönetme](#callfromoutsidehub) konularına bakın.</span><span class="sxs-lookup"><span data-stu-id="a9506-195">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="a9506-196">Camel-JavaScript istemcilerinde hub adlarının büyük küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="a9506-196">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="a9506-197">Varsayılan olarak, JavaScript istemcileri, sınıf adının Camel-cased bir sürümünü kullanarak hub 'Lara başvurur.</span><span class="sxs-lookup"><span data-stu-id="a9506-197">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="a9506-198">SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="a9506-198">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="a9506-199">Önceki örneğe JavaScript kodunda `contosoChatHub` adı verilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-199">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="a9506-200">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="a9506-200">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

<span data-ttu-id="a9506-201">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="a9506-201">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

<span data-ttu-id="a9506-202">İstemcilerin kullanması için farklı bir ad belirtmek istiyorsanız, `HubName` özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9506-202">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="a9506-203">Bir `HubName` özniteliği kullandığınızda JavaScript istemcilerinde ortası örneğine bir ad değişikliği yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="a9506-203">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="a9506-204">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="a9506-204">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

<span data-ttu-id="a9506-205">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="a9506-205">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="a9506-206">Birden çok hub</span><span class="sxs-lookup"><span data-stu-id="a9506-206">Multiple Hubs</span></span>

<span data-ttu-id="a9506-207">Bir uygulamada birden çok hub sınıfı tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-207">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="a9506-208">Bunu yaptığınızda bağlantı paylaşılır, ancak gruplar ayrıdır:</span><span class="sxs-lookup"><span data-stu-id="a9506-208">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="a9506-209">Tüm istemciler hizmetinize bir SignalR bağlantısı kurmak için aynı URL 'YI kullanır ("/SignalR" veya bir tane belirtilmişse özel URL 'niz) ve bu bağlantı, hizmet tarafından tanımlanan tüm Hub 'Lar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a9506-209">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="a9506-210">Tek bir sınıfta tüm Hub işlevlerini tanımlamaya kıyasla birden çok Hub için performans farkı yoktur.</span><span class="sxs-lookup"><span data-stu-id="a9506-210">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="a9506-211">Tüm Hub 'Lar aynı HTTP istek bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="a9506-211">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="a9506-212">Tüm Hub 'Lar aynı bağlantıyı paylaştığından, sunucunun aldığı tek HTTP istek bilgileri, SignalR bağlantısını kuran özgün HTTP isteğine gelir.</span><span class="sxs-lookup"><span data-stu-id="a9506-212">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="a9506-213">Bir sorgu dizesi belirterek istemciden sunucuya bilgi geçirmek için bağlantı isteğini kullanırsanız, farklı hub 'Lara farklı sorgu dizeleri sağlayamıyorum.</span><span class="sxs-lookup"><span data-stu-id="a9506-213">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="a9506-214">Tüm Hub 'Lar aynı bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="a9506-214">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="a9506-215">Oluşturulan JavaScript proxy 'leri dosyası, tek bir dosyadaki tüm Hub 'Lara ait proxy 'leri içerir.</span><span class="sxs-lookup"><span data-stu-id="a9506-215">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="a9506-216">JavaScript proxy 'leri hakkında daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-oluşturulan ara sunucu ve sizin için ne yapar](index.md).</span><span class="sxs-lookup"><span data-stu-id="a9506-216">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).</span></span>
- <span data-ttu-id="a9506-217">Gruplar, hub 'Lar içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a9506-217">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="a9506-218">SignalR 'de, bağlı istemcilerin alt kümelerine yayınlamak için adlandırılmış grupları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-218">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="a9506-219">Gruplar her Hub için ayrı ayrı tutulur.</span><span class="sxs-lookup"><span data-stu-id="a9506-219">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="a9506-220">Örneğin, "Administrators" adlı bir grup `ContosoChatHub` sınıfınız için bir istemci kümesi içerir ve aynı grup adı `StockTickerHub` sınıfınız için farklı bir istemci kümesine başvuracaktır.</span><span class="sxs-lookup"><span data-stu-id="a9506-220">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="a9506-221">Hub sınıfında istemcilerin çağırabilmeniz için yöntemler tanımlama</span><span class="sxs-lookup"><span data-stu-id="a9506-221">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="a9506-222">Merkezi üzerinde istemciden çağrılabilir olmasını istediğiniz bir yöntemi ortaya çıkarmak için aşağıdaki örneklerde gösterildiği gibi bir genel yöntem bildirin.</span><span class="sxs-lookup"><span data-stu-id="a9506-222">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="a9506-223">Herhangi C# bir yöntemde yaptığınız gibi, karmaşık türler ve diziler dahil olmak üzere bir dönüş türü ve parametreleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-223">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="a9506-224">Parametrelerde aldığınız veya çağırana geri döndürülen tüm veriler, istemci ile sunucu arasında JSON kullanılarak iletilir ve SignalR karmaşık nesnelerin ve nesne dizilerinin otomatik olarak bağlamasını işler.</span><span class="sxs-lookup"><span data-stu-id="a9506-224">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="a9506-225">Camel-JavaScript istemcilerinde yöntem adlarının büyük küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="a9506-225">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="a9506-226">Varsayılan olarak, JavaScript istemcileri, yöntem adının Camel-cased bir sürümünü kullanarak Merkez yöntemlerine başvurur.</span><span class="sxs-lookup"><span data-stu-id="a9506-226">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="a9506-227">SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="a9506-227">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="a9506-228">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="a9506-228">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="a9506-229">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="a9506-229">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="a9506-230">İstemcilerin kullanması için farklı bir ad belirtmek istiyorsanız, `HubMethodName` özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9506-230">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="a9506-231">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="a9506-231">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="a9506-232">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="a9506-232">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="a9506-233">Zaman uyumsuz olarak yürütme</span><span class="sxs-lookup"><span data-stu-id="a9506-233">When to execute asynchronously</span></span>

<span data-ttu-id="a9506-234">Yöntem uzun süre çalışabilir veya bir veritabanı araması veya bir Web hizmeti çağrısı gibi beklemeyi gerektirebilecek iş yapmak için, bir [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (`void` dönüşü yerine) veya [görev&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) nesnesi (`T` dönüş türü yerine) döndürerek hub yöntemini zaman uyumsuz yapın.</span><span class="sxs-lookup"><span data-stu-id="a9506-234">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="a9506-235">Yönteminden bir `Task` nesnesi döndürdüğünüzde, SignalR `Task` tamamlanmasını bekler ve sarmalanmamış sonucu istemciye geri gönderir. bu nedenle, istemcide yöntem çağrısını nasıl kodlayabilmeniz fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="a9506-235">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="a9506-236">Bir hub yönteminin zaman uyumsuz yapılması, WebSocket aktarımını kullandığında bağlantının engellenmesini önler.</span><span class="sxs-lookup"><span data-stu-id="a9506-236">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="a9506-237">Bir hub yöntemi zaman uyumlu olarak yürütülüyorsa ve aktarım WebSocket ise, hub yöntemi tamamlanana kadar hub üzerindeki yöntemlerin sonraki çağrıları aynı istemciden engellenir.</span><span class="sxs-lookup"><span data-stu-id="a9506-237">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="a9506-238">Aşağıdaki örnek, her iki sürümü de çağırmak için çalışan JavaScript istemci kodu tarafından zaman uyumlu veya zaman uyumsuz olarak çalışacak şekilde kodlanmış aynı yöntemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-238">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="a9506-239">**K**</span><span class="sxs-lookup"><span data-stu-id="a9506-239">**Synchronous**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="a9506-240">**Zaman uyumsuz-ASP.NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="a9506-240">**Asynchronous - ASP.NET 4.5**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="a9506-241">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="a9506-241">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="a9506-242">ASP.NET 4,5 ' de zaman uyumsuz yöntemlerin nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [ASP.NET MVC 4 Içinde zaman uyumsuz yöntemler kullanma](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="a9506-242">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="a9506-243">Aşırı yüklemeleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="a9506-243">Defining Overloads</span></span>

<span data-ttu-id="a9506-244">Bir yöntem için aşırı yüklemeleri tanımlamak istiyorsanız, her aşırı yüklemede parametre sayısı farklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a9506-244">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="a9506-245">Farklı parametre türleri belirterek bir aşırı yüklemeyi ayırt ediyorsanız, hub sınıfınız derlenir, ancak istemciler aşırı yüklemelerin birini çağırmaya çalıştığında, çalışma zamanında SignalR hizmeti bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9506-245">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="a9506-246">Hub sınıfından istemci yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="a9506-246">How to call client methods from the Hub class</span></span>

<span data-ttu-id="a9506-247">Sunucudan istemci yöntemlerini çağırmak için, hub sınıfınızın bir yönteminde `Clients` özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9506-247">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="a9506-248">Aşağıdaki örnek, tüm bağlı istemcilerde `addNewMessageToPage` çağıran sunucu kodunu ve bir JavaScript istemcisinde yöntemi tanımlayan istemci kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-248">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="a9506-249">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="a9506-249">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

<span data-ttu-id="a9506-250">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="a9506-250">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

<span data-ttu-id="a9506-251">İstemci yönteminden bir dönüş değeri alamazsınız; `int x = Clients.All.add(1,1)` gibi sözdizimi çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="a9506-251">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="a9506-252">Parametreler için karmaşık türler ve diziler belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-252">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="a9506-253">Aşağıdaki örnek, bir yöntem parametresinde istemciye karmaşık bir tür geçirir.</span><span class="sxs-lookup"><span data-stu-id="a9506-253">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="a9506-254">**Karmaşık bir nesne kullanarak istemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="a9506-254">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

<span data-ttu-id="a9506-255">**Karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="a9506-255">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

<span data-ttu-id="a9506-256">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="a9506-256">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="a9506-257">Hangi istemcilerin RPC alacağını seçme</span><span class="sxs-lookup"><span data-stu-id="a9506-257">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="a9506-258">Clients özelliği, hangi istemcilerin RPC alacağını belirtmek için çeşitli seçenekler sağlayan bir [Hubconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) nesnesi döndürür:</span><span class="sxs-lookup"><span data-stu-id="a9506-258">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="a9506-259">Bağlanan tüm istemciler.</span><span class="sxs-lookup"><span data-stu-id="a9506-259">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- <span data-ttu-id="a9506-260">Yalnızca çağıran istemci.</span><span class="sxs-lookup"><span data-stu-id="a9506-260">Only the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="a9506-261">Çağıran istemci dışındaki tüm istemciler.</span><span class="sxs-lookup"><span data-stu-id="a9506-261">All clients except the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="a9506-262">Bağlantı KIMLIĞIYLE tanımlanan belirli bir istemci.</span><span class="sxs-lookup"><span data-stu-id="a9506-262">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    <span data-ttu-id="a9506-263">Bu örnek, çağıran istemcide `addContosoChatMessageToPage` çağırır ve `Clients.Caller`ile aynı etkiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a9506-263">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="a9506-264">Belirtilen istemciler dışındaki tüm bağlı istemciler, bağlantı KIMLIĞIYLE tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a9506-264">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- <span data-ttu-id="a9506-265">Belirtilen bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="a9506-265">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- <span data-ttu-id="a9506-266">Belirtilen bir gruptaki, belirtilen istemciler hariç, bağlantı KIMLIĞIYLE tanımlanan tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="a9506-266">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- <span data-ttu-id="a9506-267">Çağıran istemci hariç, belirtilen bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="a9506-267">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="a9506-268">Yöntem adları için derleme zamanı doğrulaması yok</span><span class="sxs-lookup"><span data-stu-id="a9506-268">No compile-time validation for method names</span></span>

<span data-ttu-id="a9506-269">Belirttiğiniz Yöntem adı dinamik bir nesne olarak yorumlanır, yani bunun için IntelliSense veya derleme zamanı doğrulaması yoktur.</span><span class="sxs-lookup"><span data-stu-id="a9506-269">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="a9506-270">İfade çalışma zamanında değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-270">The expression is evaluated at run time.</span></span> <span data-ttu-id="a9506-271">Yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerlerini istemciye gönderir ve istemcinin adıyla eşleşen bir yöntemi varsa, bu yöntem çağrılır ve parametre değerleri kendisine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-271">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="a9506-272">İstemcide eşleşen bir yöntem bulunamazsa, hiçbir hata oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="a9506-272">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="a9506-273">İstemci yöntemini çağırdığınızda SignalR 'nin arka planda istemciye ilettiği verilerin biçimi hakkında daha fazla bilgi için bkz. [SignalR 'ye giriş](index.md).</span><span class="sxs-lookup"><span data-stu-id="a9506-273">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](index.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="a9506-274">Büyük/küçük harf duyarsız Yöntem adı eşleştirme</span><span class="sxs-lookup"><span data-stu-id="a9506-274">Case-insensitive method name matching</span></span>

<span data-ttu-id="a9506-275">Yöntem adı eşleştirme, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="a9506-275">Method name matching is case-insensitive.</span></span> <span data-ttu-id="a9506-276">Örneğin, sunucusundaki `Clients.All.addContosoChatMessageToPage`, istemcide `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`veya `addContosoChatMessageToPage` yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a9506-276">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="a9506-277">Zaman uyumsuz yürütme</span><span class="sxs-lookup"><span data-stu-id="a9506-277">Asynchronous execution</span></span>

<span data-ttu-id="a9506-278">Çağırdığınız yöntem zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a9506-278">The method that you call executes asynchronously.</span></span> <span data-ttu-id="a9506-279">Bir istemciye yönelik bir yöntem çağrısından sonra gelen herhangi bir kod, sonraki kod satırlarının Yöntem tamamlanmasını beklemesi gerekmediği takdirde, SignalR 'nin istemcilere veri aktarma işleminin bitmesini beklemeden hemen yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a9506-279">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="a9506-280">Aşağıdaki kod örnekleri, iki istemci yönteminin sırayla nasıl yürütüleceğini, .NET 4,5 ' de çalıştırılan kodu ve .NET 4 ' te çalıştırılan bir kodu kullanmayı göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="a9506-280">The following code examples show how to execute two client methods sequentially, one using code that works in .NET 4.5, and one using code that works in .NET 4.</span></span>

<span data-ttu-id="a9506-281">**.NET 4,5 örneği**</span><span class="sxs-lookup"><span data-stu-id="a9506-281">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

<span data-ttu-id="a9506-282">**.NET 4 örneği**</span><span class="sxs-lookup"><span data-stu-id="a9506-282">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

<span data-ttu-id="a9506-283">Bir sonraki kod satırından önce istemci yöntemi bitene kadar beklemek için `await` veya `ContinueWith` kullanırsanız, bu, istemcilerin bir sonraki kod çalıştırılmadan önce iletiyi gerçekten alacağı anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="a9506-283">If you use `await` or `ContinueWith` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="a9506-284">Bir istemci yöntemi çağrısının "tamamlama" işlemi, SignalR 'nin iletiyi göndermek için gereken her şeyi yaptığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a9506-284">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="a9506-285">İstemcilerin iletiyi aldığını doğrulamaya ihtiyacınız varsa, o mekanizmayı kendiniz programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-285">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="a9506-286">Örneğin, hub 'da bir `MessageReceived` yöntemi kod, istemci üzerindeki `addContosoChatMessageToPage` yönteminde, istemcide yapmanız gereken herhangi bir işi yaptıktan sonra `MessageReceived` çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-286">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="a9506-287">Hub 'daki `MessageReceived`, gerçek istemci alımı ve özgün yöntem çağrısının işlenmesine bağlı olarak herhangi bir işi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-287">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="a9506-288">Yöntem adı olarak bir dize değişkeni kullanma</span><span class="sxs-lookup"><span data-stu-id="a9506-288">How to use a string variable as the method name</span></span>

<span data-ttu-id="a9506-289">Bir istemci yöntemini, yöntem adı olarak bir dize değişkeni kullanarak çağırmak istiyorsanız, `Clients.All` (veya `Clients.Others`, `Clients.Caller`, vb.) `IClientProxy` ve sonra [Invoke (MethodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a9506-289">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="a9506-290">Hub sınıfından grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="a9506-290">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="a9506-291">SignalR içindeki gruplar, bağlı istemcilerin belirtilen alt kümelerine ileti yayınlamak için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9506-291">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="a9506-292">Bir grup herhangi bir sayıda istemciye sahip olabilir ve bir istemci herhangi bir sayıda grubun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-292">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="a9506-293">Grup üyeliğini yönetmek için, hub sınıfının `Groups` özelliği tarafından sunulan [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) ve [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9506-293">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="a9506-294">Aşağıdaki örnek, istemci kodu tarafından çağrılan ve ardından bunları çağıran JavaScript istemci kodunun ardından, hub yöntemlerinde kullanılan `Groups.Add` ve `Groups.Remove` yöntemlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-294">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="a9506-295">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="a9506-295">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

<span data-ttu-id="a9506-296">**Oluşturulan proxy kullanan JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="a9506-296">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

<span data-ttu-id="a9506-297">Açıkça grup oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a9506-297">You don't have to explicitly create groups.</span></span> <span data-ttu-id="a9506-298">Aslında bir grup, bir `Groups.Add`çağrısında adını ilk kez belirttiğinizde otomatik olarak oluşturulur ve içindeki üyeliğinden son bağlantıyı kaldırdığınızda silinir.</span><span class="sxs-lookup"><span data-stu-id="a9506-298">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="a9506-299">Grup üyeliği listesi veya Grup listesi almak için API yok.</span><span class="sxs-lookup"><span data-stu-id="a9506-299">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="a9506-300">SignalR bir [yayın/alt modele](http://en.wikipedia.org/wiki/Publish/subscribe)göre istemcilere ve gruplara iletiler gönderir ve sunucu grup veya grup üyelikleri listesini korumaz.</span><span class="sxs-lookup"><span data-stu-id="a9506-300">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="a9506-301">Bu, bir Web grubuna düğüm eklediğiniz her durumda, SignalR 'nin koruduğu tüm durumun yeni düğüme yayılması nedeniyle ölçeklenebilirliği en üst düzeye çıkarmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a9506-301">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="a9506-302">Ekleme ve kaldırma yöntemlerinin zaman uyumsuz yürütmesi</span><span class="sxs-lookup"><span data-stu-id="a9506-302">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="a9506-303">`Groups.Add` ve `Groups.Remove` yöntemleri zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a9506-303">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="a9506-304">Bir gruba bir istemci eklemek ve grubu kullanarak istemciye hemen ileti göndermek istiyorsanız, `Groups.Add` yönteminin önce tamamlandığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9506-304">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="a9506-305">Aşağıdaki kod örneklerinde bunun nasıl yapılacağı, biri .NET 4,5 ' de çalıştırılan kodu kullanarak ve bir diğeri de .NET 4 ' te çalıştırılan kod kullanılarak gösterilmektedir</span><span class="sxs-lookup"><span data-stu-id="a9506-305">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4</span></span>

<span data-ttu-id="a9506-306">**.NET 4,5 örneği**</span><span class="sxs-lookup"><span data-stu-id="a9506-306">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="a9506-307">**.NET 4 örneği**</span><span class="sxs-lookup"><span data-stu-id="a9506-307">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="a9506-308">Grup üyeliği kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="a9506-308">Group membership persistence</span></span>

<span data-ttu-id="a9506-309">SignalR, kullanıcıları değil bağlantıları izler, bu nedenle Kullanıcı her bağlantı kurduğunda bir kullanıcının aynı grupta olmasını istiyorsanız, Kullanıcı her yeni bağlantı kurduğunda `Groups.Add` çağırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9506-309">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="a9506-310">Geçici bir bağlantı kaybı sonrasında, bazı durumlarda SignalR bağlantıyı otomatik olarak geri yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-310">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="a9506-311">Bu durumda, SignalR aynı bağlantıyı geri yüklüyor, yeni bir bağlantı oluşturmamalıdır ve istemcinin grup üyeliği otomatik olarak geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a9506-311">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="a9506-312">Bu durum, geçici kesme sunucu yeniden başlatma veya başarısızlık nedeniyle bile, grup üyelikleri de dahil olmak üzere her bir istemcinin bağlantı durumu istemciye yuvarlandığı için mümkündür.</span><span class="sxs-lookup"><span data-stu-id="a9506-312">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="a9506-313">Bir sunucu kapalıysa ve bağlantı zaman aşımına uğramadan önce yeni bir sunucu tarafından değiştirilirse, istemci otomatik olarak yeni sunucuya yeniden bağlanabilir ve üyesi olan gruplara yeniden kaydolabilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-313">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="a9506-314">Bağlantı kesilirse veya bağlantı zaman aşımına uğrarsa ya da istemcinin bağlantısı kesildiğinde (örneğin, bir tarayıcı yeni bir sayfaya gittiğinde) bir bağlantı otomatik olarak geri yüklenemediğinde, grup üyelikleri kaybedilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-314">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="a9506-315">Kullanıcı bir sonraki sefer bağlanışında yeni bir bağlantı olur.</span><span class="sxs-lookup"><span data-stu-id="a9506-315">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="a9506-316">Aynı kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini sürdürmek için, uygulamanız kullanıcılar ve gruplar arasındaki ilişkilendirmeleri izlemek ve Kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini geri yüklemek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9506-316">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="a9506-317">Bağlantılar ve yeniden bağlantılar hakkında daha fazla bilgi için, bu konunun ilerleyen kısımlarında yer alarak [Merkez sınıfında bağlantı ömrü olaylarını işleme](#connectionlifetime) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a9506-317">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="a9506-318">Tek Kullanıcı grupları</span><span class="sxs-lookup"><span data-stu-id="a9506-318">Single-user groups</span></span>

<span data-ttu-id="a9506-319">SignalR kullanan uygulamalar genellikle hangi kullanıcının bir ileti gönderdiğini ve hangi kullanıcıların bir ileti aldıklarını bilmek için kullanıcılar ve bağlantılar arasındaki ilişkilendirmeleri takip etmelidir.</span><span class="sxs-lookup"><span data-stu-id="a9506-319">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="a9506-320">Gruplar, bunu yapmak için yaygın olarak kullanılan iki desenden birinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a9506-320">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="a9506-321">Tek Kullanıcı grupları.</span><span class="sxs-lookup"><span data-stu-id="a9506-321">Single-user groups.</span></span>

    <span data-ttu-id="a9506-322">Kullanıcı adını Grup adı olarak belirtebilir ve Kullanıcı her bağlandığında veya yeniden bağlandığında geçerli bağlantı KIMLIĞINI gruba ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-322">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="a9506-323">Gruba göndereceğiniz kullanıcıya ileti göndermek için.</span><span class="sxs-lookup"><span data-stu-id="a9506-323">To send messages to the user you send to the group.</span></span> <span data-ttu-id="a9506-324">Bu yöntemin bir dezavantajı, grubun, kullanıcının çevrimiçi veya çevrimdışı olduğunu anlamak için bir yol sağlamamasıdır.</span><span class="sxs-lookup"><span data-stu-id="a9506-324">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="a9506-325">Kullanıcı adlarıyla bağlantı kimlikleri arasındaki ilişkilendirmeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a9506-325">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="a9506-326">Her Kullanıcı adı ile bir veya daha fazla bağlantı kimliği arasında bir ilişki veya bir sözlükte veya veritabanında bir ilişki saklayabilir ve Kullanıcı her bağlanıp bağlantısı kesildiğinde depolanan verileri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-326">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="a9506-327">Kullanıcıya ileti göndermek için bağlantı kimliklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a9506-327">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="a9506-328">Bu yöntemin bir dezavantajı daha fazla bellek kaplar.</span><span class="sxs-lookup"><span data-stu-id="a9506-328">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="a9506-329">Hub sınıfında bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="a9506-329">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="a9506-330">Bağlantı ömrü olaylarının işlenmesinin tipik nedenleri, bir kullanıcının bağlanıp bağlanmadığını ve Kullanıcı adları ile bağlantı kimlikleri arasındaki ilişkilendirmeyi takip etmesidir.</span><span class="sxs-lookup"><span data-stu-id="a9506-330">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="a9506-331">İstemciler bağlandığında veya bağlantıyı kestikten sonra kendi kodunuzu çalıştırmak için, aşağıdaki örnekte gösterildiği gibi hub sınıfının `OnConnected`, `OnDisconnected`ve `OnReconnected` sanal yöntemlerini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="a9506-331">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="a9506-332">OnConnected, OnConnected ve OnConnected çağrıldığında</span><span class="sxs-lookup"><span data-stu-id="a9506-332">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="a9506-333">Her tarayıcı yeni bir sayfaya gittiğinde, yeni bir bağlantı kurulması gerekir. Bu, SignalR 'in, `OnDisconnected` yöntemi ve ardından `OnConnected` yöntemi tarafından yürütüleceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a9506-333">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="a9506-334">SignalR yeni bir bağlantı oluşturulduğunda her zaman yeni bir bağlantı KIMLIĞI oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9506-334">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="a9506-335">`OnReconnected` yöntemi, bir kablonun geçici olarak kesilmesi ve bağlantı zaman aşımına uğramadan önce yeniden bağlanması gibi, SignalR 'nin otomatik olarak kurtarabileceği bir bağlantıda geçici bir kesme olduğunda çağrılır. `OnDisconnected` yöntemi, istemcinin bağlantısı kesildiğinde çağrılır ve bir tarayıcı yeni bir sayfaya gittiğinde, SignalR otomatik olarak yeniden bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="a9506-335">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="a9506-336">Bu nedenle, belirli bir istemci için olası bir olay dizisi `OnConnected`, `OnReconnected``OnDisconnected`; ya da `OnConnected``OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="a9506-336">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="a9506-337">Belirli bir bağlantı için sıra `OnConnected`, `OnDisconnected``OnReconnected` görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-337">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="a9506-338">`OnDisconnected` yöntemi, bir sunucunun kapanması ya da uygulama etki alanının geri dönüştürülmesi gibi bazı senaryolarda çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="a9506-338">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="a9506-339">Başka bir sunucu satır üzerine geldiğinde veya uygulama etki alanının geri dönüşümü tamamlandığında, bazı istemciler `OnReconnected` olayı yeniden oluşturabilir ve tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-339">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="a9506-340">Daha fazla bilgi için bkz. [SignalR 'de bağlantı ömrü olaylarını anlama ve işleme](index.md).</span><span class="sxs-lookup"><span data-stu-id="a9506-340">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="a9506-341">Çağıran durum doldurulmamış</span><span class="sxs-lookup"><span data-stu-id="a9506-341">Caller state not populated</span></span>

<span data-ttu-id="a9506-342">Bağlantı ömrü olay işleyicisi yöntemleri sunucudan çağrılır, bu, istemcideki `state` nesnesine yerleştirdiğiniz herhangi bir durumun sunucudaki `Caller` özelliğinde doldurulmayacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a9506-342">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="a9506-343">`state` nesnesi ve `Caller` özelliği hakkında daha fazla bilgi için, bu konunun ilerleyen kısımlarında [istemciler ve hub sınıfı arasında durum geçirme](#passstate) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="a9506-343">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="a9506-344">Bağlam özelliğinden istemci hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="a9506-344">How to get information about the client from the Context property</span></span>

<span data-ttu-id="a9506-345">İstemci hakkında bilgi almak için, hub sınıfının `Context` özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9506-345">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="a9506-346">`Context` özelliği, aşağıdaki bilgilere erişim sağlayan bir [Hubcallercontext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) nesnesi döndürür:</span><span class="sxs-lookup"><span data-stu-id="a9506-346">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="a9506-347">Çağıran istemcinin bağlantı kimliği.</span><span class="sxs-lookup"><span data-stu-id="a9506-347">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    <span data-ttu-id="a9506-348">Bağlantı KIMLIĞI, SignalR tarafından atanan bir GUID 'dir (değeri kendi kodunuzda belirtemezsiniz).</span><span class="sxs-lookup"><span data-stu-id="a9506-348">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="a9506-349">Her bağlantı için bir bağlantı KIMLIĞI vardır ve uygulamanızda birden çok hub varsa, tüm Hub 'Lar tarafından aynı bağlantı KIMLIĞI kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a9506-349">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="a9506-350">HTTP üstbilgisi verileri.</span><span class="sxs-lookup"><span data-stu-id="a9506-350">HTTP header data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    <span data-ttu-id="a9506-351">Ayrıca, `Context.Headers`HTTP üst bilgilerini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-351">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="a9506-352">Aynı şey için birden çok başvuru olmasının nedeni `Context.Headers` ilk olarak oluşturulmuştur, `Context.Request` özelliği daha sonra eklenmiştir ve `Context.Headers` geriye dönük uyumluluk için tutulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a9506-352">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="a9506-353">Sorgu dizesi verileri.</span><span class="sxs-lookup"><span data-stu-id="a9506-353">Query string data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    <span data-ttu-id="a9506-354">`Context.QueryString`sorgu dizesi verilerini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-354">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="a9506-355">Bu özelliğe alacağınız sorgu dizesi, SignalR bağlantısını oluşturan HTTP isteğiyle birlikte kullanılmış olan bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="a9506-355">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="a9506-356">İstemciden sunucuya istemci hakkında verileri geçirmek için kullanışlı bir yol olan bağlantıyı yapılandırarak istemciye sorgu dizesi parametreleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-356">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="a9506-357">Aşağıdaki örnek, oluşturulan proxy 'yi kullandığınızda JavaScript istemcisine bir sorgu dizesi eklemenin bir yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-357">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    <span data-ttu-id="a9506-358">Sorgu dizesi parametreleri ayarlama hakkında daha fazla bilgi için, [JavaScript](index.md) ve [.net](index.md) istemcileri için API kılavuzlarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a9506-358">For more information about setting query string parameters, see the API guides for the [JavaScript](index.md) and [.NET](index.md) clients.</span></span>

    <span data-ttu-id="a9506-359">Sorgu dizesi verilerinde bağlantı için kullanılan aktarım yöntemini, SignalR tarafından dahili olarak kullanılan bazı diğer değerlerle birlikte bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9506-359">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    <span data-ttu-id="a9506-360">`transportMethod` değeri "webSockets", "serverSentEvents", "foreverFrame" veya "longPolling" olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a9506-360">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="a9506-361">Bu değeri `OnConnected` olay işleyicisi yönteminde denetlebileceğinizi unutmayın, bazı senaryolarda başlangıçta bağlantı için en son anlaşmalı aktarım yöntemi olmayan bir aktarım değeri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-361">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="a9506-362">Bu durumda yöntem bir özel durum oluşturur ve daha sonra son taşıma yöntemi oluşturulduğunda yeniden çağrılacaktır.</span><span class="sxs-lookup"><span data-stu-id="a9506-362">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="a9506-363">Özgü.</span><span class="sxs-lookup"><span data-stu-id="a9506-363">Cookies.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="a9506-364">`Context.RequestCookies`tanımlama bilgilerini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-364">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="a9506-365">Kullanıcı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a9506-365">User information.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- <span data-ttu-id="a9506-366">İstek için HttpContext nesnesi:</span><span class="sxs-lookup"><span data-stu-id="a9506-366">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    <span data-ttu-id="a9506-367">SignalR bağlantısı için `HttpContext` nesnesini almak üzere `HttpContext.Current` almak yerine bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9506-367">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="a9506-368">İstemcilerle hub sınıfı arasında durum geçirme</span><span class="sxs-lookup"><span data-stu-id="a9506-368">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="a9506-369">İstemci proxy 'si, her yöntem çağrısıyla sunucuya aktarılmasını istediğiniz verileri depolayabilmeniz için bir `state` nesnesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9506-369">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="a9506-370">Sunucusunda, bu verilere istemciler tarafından çağrılan hub yöntemlerinde `Clients.Caller` özelliğindeki erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-370">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="a9506-371">`Clients.Caller` özelliği, bağlantı ömrü olay işleyicisi yöntemleri `OnConnected`, `OnDisconnected`ve `OnReconnected`için doldurulmaz.</span><span class="sxs-lookup"><span data-stu-id="a9506-371">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="a9506-372">`state` nesnesindeki verileri oluşturma veya güncelleştirme ve `Clients.Caller` özelliği her iki yönde de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-372">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="a9506-373">Sunucudaki değerleri güncelleştirebilir ve istemciye geri geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-373">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="a9506-374">Aşağıdaki örnek, her yöntem çağrısıyla sunucuya iletilmek üzere durum depolayan JavaScript istemci kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-374">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

<span data-ttu-id="a9506-375">Aşağıdaki örnek, bir .NET istemcisinde denk kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-375">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

<span data-ttu-id="a9506-376">Hub sınıfınız içinde, `Clients.Caller` özelliğindeki bu verilere erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-376">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="a9506-377">Aşağıdaki örnek, önceki örnekte başvurulan durumu alan kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-377">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="a9506-378">Kalıcı duruma yönelik bu mekanizma, büyük miktarlarda veri için tasarlanmamıştır çünkü `state` veya `Clients.Caller` özelliğine yerleştirdiğiniz her şey, her yöntem çağrısı ile birlikte yuvarlama yaptığından.</span><span class="sxs-lookup"><span data-stu-id="a9506-378">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="a9506-379">Kullanıcı adları veya sayaçlar gibi daha küçük öğeler için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="a9506-379">It's useful for smaller items such as user names or counters.</span></span>

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="a9506-380">Hub sınıfında hataları işleme</span><span class="sxs-lookup"><span data-stu-id="a9506-380">How to handle errors in the Hub class</span></span>

<span data-ttu-id="a9506-381">Hub sınıfı yöntemleriniz içinde oluşan hataları işlemek için aşağıdaki yöntemlerden birini veya her ikisini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a9506-381">To handle errors that occur in your Hub class methods, use one or both of the following methods:</span></span>

- <span data-ttu-id="a9506-382">Yöntem kodunuzu try-catch bloklarına sarın ve özel durum nesnesini günlüğe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a9506-382">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="a9506-383">Hata ayıklama amacıyla, özel durumu istemciye gönderebilirsiniz, ancak üretimde istemcilere ayrıntılı bilgi gönderilmesi için güvenlik nedenleriyle önerilmez.</span><span class="sxs-lookup"><span data-stu-id="a9506-383">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="a9506-384">[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) yöntemini Işleyen bir hub işlem hattı modülü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9506-384">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="a9506-385">Aşağıdaki örnek, hataları kaydeden bir işlem hattı modülünü ve ardından modülü hub işlem hattına veren Global. asax dosyasındaki kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9506-385">The following example shows a pipeline module that logs errors, followed by code in Global.asax that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

<span data-ttu-id="a9506-386">Merkez ardışık düzen modülleri hakkında daha fazla bilgi için, bu konunun ilerleyen bölümlerinde hub işlem hattını [Özelleştirme](#hubpipeline) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a9506-386">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="a9506-387">İzlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a9506-387">How to enable tracing</span></span>

<span data-ttu-id="a9506-388">Sunucu tarafı izlemeyi etkinleştirmek için, aşağıdaki örnekte gösterildiği gibi, Web. config dosyanıza bir System. Diagnostics öğesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a9506-388">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

<span data-ttu-id="a9506-389">Uygulamayı Visual Studio 'da çalıştırdığınızda, günlükleri **Çıkış** penceresinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-389">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="a9506-390">İstemci yöntemlerini çağırma ve grupları hub sınıfı dışından yönetme</span><span class="sxs-lookup"><span data-stu-id="a9506-390">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="a9506-391">Hub sınıfınızın farklı bir sınıfından istemci yöntemlerini çağırmak için, Hub için SignalR bağlam nesnesine bir başvuru alın ve bunu istemci üzerindeki yöntemleri çağırmak veya grupları yönetmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9506-391">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="a9506-392">Aşağıdaki örnek `StockTicker` sınıfı, bağlam nesnesini alır, onu sınıfının bir örneğine depolar, sınıf örneğini statik bir özellikte depolar ve `StockTickerHub`adlı bir hub 'a bağlı istemcilerde `updateStockPrice` yöntemini çağırmak için singleton sınıfı örneğinden bağlamını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9506-392">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

<span data-ttu-id="a9506-393">İçeriği uzun süreli bir nesnede birden çok kez kullanmanız gerekiyorsa, başvuruyu bir kez alın ve her seferinde yeniden almak yerine kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a9506-393">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="a9506-394">Bağlam bir kez alındıktan sonra, SignalR 'nin, hub yöntemlerinizin istemci yöntemi etkinleştirmeleri haline gelen aynı sıradaki istemcilere ileti göndermesi güvence altına alınır.</span><span class="sxs-lookup"><span data-stu-id="a9506-394">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="a9506-395">Bir hub için SignalR bağlamını nasıl kullanacağınızı gösteren bir öğretici için, bkz. [ASP.NET SignalR Ile sunucu yayını](index.md).</span><span class="sxs-lookup"><span data-stu-id="a9506-395">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](index.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="a9506-396">İstemci yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="a9506-396">Calling client methods</span></span>

<span data-ttu-id="a9506-397">Hangi istemcilerin RPC alacağını belirtebilirsiniz, ancak bir hub sınıfından çağrı yaparken daha az seçeneğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="a9506-397">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="a9506-398">Bunun nedeni, bağlamın bir istemciden gelen belirli bir çağrıyla ilişkilendirilmediği, yani `Clients.Others`veya `Clients.Caller`ya da `Clients.OthersInGroup`gibi geçerli bağlantı KIMLIĞI hakkında bilgi gerektiren tüm yöntemler kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="a9506-398">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="a9506-399">Aşağıdaki seçenekler mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="a9506-399">The following options are available:</span></span>

- <span data-ttu-id="a9506-400">Bağlanan tüm istemciler.</span><span class="sxs-lookup"><span data-stu-id="a9506-400">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- <span data-ttu-id="a9506-401">Bağlantı KIMLIĞIYLE tanımlanan belirli bir istemci.</span><span class="sxs-lookup"><span data-stu-id="a9506-401">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- <span data-ttu-id="a9506-402">Belirtilen istemciler dışındaki tüm bağlı istemciler, bağlantı KIMLIĞIYLE tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a9506-402">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- <span data-ttu-id="a9506-403">Belirtilen bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="a9506-403">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- <span data-ttu-id="a9506-404">Belirtilen bir gruptaki, belirtilen istemciler hariç, bağlantı KIMLIĞIYLE tanımlanan tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="a9506-404">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

<span data-ttu-id="a9506-405">Hub sınıfınızın metotlarından hub olmayan sınıfa çağrı yapıyorsanız, geçerli bağlantı KIMLIĞINI geçirebilir ve `Clients.Caller`, `Clients.Others`veya `Clients.OthersInGroup`benzetimini yapmak için `Clients.Client`, `Clients.AllExcept`veya `Clients.Group` ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9506-405">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="a9506-406">Aşağıdaki örnekte, `MoveShapeHub` sınıfı bağlantı KIMLIĞINI `Broadcaster` sınıfına geçirir `Broadcaster` sınıfının `Clients.Others`benzetimini yapabilir.</span><span class="sxs-lookup"><span data-stu-id="a9506-406">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="a9506-407">Grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="a9506-407">Managing group membership</span></span>

<span data-ttu-id="a9506-408">Grupları yönetmek için bir hub sınıfında yaptığınız seçeneklerle aynı seçeneklere sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="a9506-408">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="a9506-409">Bir gruba istemci ekleme</span><span class="sxs-lookup"><span data-stu-id="a9506-409">Add a client to a group</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- <span data-ttu-id="a9506-410">Bir gruptan bir istemciyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="a9506-410">Remove a client from a group</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="a9506-411">Hub ardışık düzenini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="a9506-411">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="a9506-412">SignalR, kendi kodunuzu hub işlem hattına eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9506-412">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="a9506-413">Aşağıdaki örnek, istemcisinde çağrılan her bir gelen yöntem çağrısını günlüğe kaydeden özel bir hub işlem hattı modülünü ve istemcide çağrılan giden yöntem çağrısını gösterir:</span><span class="sxs-lookup"><span data-stu-id="a9506-413">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

<span data-ttu-id="a9506-414">*Global. asax* dosyasında aşağıdaki kod, modülü hub işlem hattında çalışacak şekilde kaydeder:</span><span class="sxs-lookup"><span data-stu-id="a9506-414">The following code in the *Global.asax* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

<span data-ttu-id="a9506-415">Geçersiz kılabileceğiniz birçok farklı yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="a9506-415">There are many different methods that you can override.</span></span> <span data-ttu-id="a9506-416">Tüm liste için bkz. [Hubpipelinemodule yöntemleri](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="a9506-416">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
