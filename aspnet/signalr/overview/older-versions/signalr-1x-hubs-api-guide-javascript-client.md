---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: SignalR 1. x hub 'Ları API Kılavuzu-JavaScript Istemcisi | Microsoft Docs
author: bradygaster
description: Bu belgede, browsers ve Windows Mağazası (WinJS) applik gibi JavaScript istemcilerinde SignalR sürüm 1,1 için hub API 'SI kullanımı hakkında bir giriş sunulmaktadır...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 24850fe5229490bf600e09ad4718abb575a845fa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536444"
---
# <a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="9c550-103">SignalR 1.x Hubs API Kılavuzu - JavaScript İstemcisi</span><span class="sxs-lookup"><span data-stu-id="9c550-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>

<span data-ttu-id="9c550-104">by [Patrick Fletu](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9c550-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="9c550-105">Bu belgede, browsers ve Windows Mağazası (WinJS) uygulamaları gibi JavaScript istemcilerinde SignalR sürüm 1,1 için hub API 'SI kullanımı hakkında bir giriş sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9c550-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="9c550-106">SignalR hub 'Ları API 'SI, uzak yordam çağrılarını (RPC) bir sunucudan, istemcilerden ve istemcilerden sunucuya bağlı hale getirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c550-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="9c550-107">Sunucu kodu ' nda, istemciler tarafından çağrılabilen Yöntemler tanımlar ve istemcide çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="9c550-108">İstemci kodunda, sunucudan çağrılabilen yöntemleri tanımlayabilir ve sunucuda çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="9c550-109">SignalR, sizin için istemciden sunucuya sıhhi kını ele alır.</span><span class="sxs-lookup"><span data-stu-id="9c550-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="9c550-110">SignalR Ayrıca kalıcı bağlantılar adlı alt düzey bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="9c550-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="9c550-111">SignalR, hub 'Lar ve sürekli bağlantılara giriş veya tam bir SignalR uygulamasının nasıl oluşturulduğunu gösteren bir öğretici için bkz. [SignalR-Başlarken](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="9c550-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="9c550-112">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="9c550-112">Overview</span></span>

<span data-ttu-id="9c550-113">Bu belgede aşağıdaki bölümler yer alır:</span><span class="sxs-lookup"><span data-stu-id="9c550-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="9c550-114">Oluşturulan ara sunucu ve sizin için ne yapar</span><span class="sxs-lookup"><span data-stu-id="9c550-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="9c550-115">Oluşturulan ara sunucu ne zaman kullanılır?</span><span class="sxs-lookup"><span data-stu-id="9c550-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="9c550-116">İstemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="9c550-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="9c550-117">Dinamik olarak oluşturulan ara sunucuya başvurma</span><span class="sxs-lookup"><span data-stu-id="9c550-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="9c550-118">SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c550-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="9c550-119">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="9c550-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="9c550-120">$. Connection. hub, $. hubConnection () tarafından oluşturulan nesnedir.</span><span class="sxs-lookup"><span data-stu-id="9c550-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="9c550-121">Start yönteminin zaman uyumsuz yürütmesi</span><span class="sxs-lookup"><span data-stu-id="9c550-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="9c550-122">Etki alanları arası bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="9c550-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="9c550-123">Bağlantıyı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9c550-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="9c550-124">Sorgu dizesi parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="9c550-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="9c550-125">Taşıma yöntemini belirtme</span><span class="sxs-lookup"><span data-stu-id="9c550-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="9c550-126">Hub sınıfı için proxy alma</span><span class="sxs-lookup"><span data-stu-id="9c550-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="9c550-127">İstemcide sunucunun çağırabir yöntemi tanımlama</span><span class="sxs-lookup"><span data-stu-id="9c550-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="9c550-128">İstemciden sunucu yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="9c550-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="9c550-129">Bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="9c550-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="9c550-130">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="9c550-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="9c550-131">İstemci tarafı günlük kaydını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9c550-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="9c550-132">Sunucu veya .NET istemcilerini programlama hakkında belgeler için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="9c550-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="9c550-133">SignalR hub 'Ları API Kılavuzu-sunucu</span><span class="sxs-lookup"><span data-stu-id="9c550-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="9c550-134">SignalR hub 'Ları API Kılavuzu-.NET Istemcisi</span><span class="sxs-lookup"><span data-stu-id="9c550-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="9c550-135">API başvuru konularına bağlantılar, API 'nin .NET 4,5 sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="9c550-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="9c550-136">.NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.</span><span class="sxs-lookup"><span data-stu-id="9c550-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="9c550-137">Oluşturulan ara sunucu ve sizin için ne yapar</span><span class="sxs-lookup"><span data-stu-id="9c550-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="9c550-138">Bir JavaScript istemcisini, bir SignalR hizmeti ile iletişim kurmak için, SignalR 'nin sizin için oluşturduğu bir ara sunucu olmadan veya olmadan iletişim kurmaya programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="9c550-139">Proxy 'nin ne için yaptığı, bağlanmak için kullandığınız kodun sözdizimini basitleştirecek, sunucunun çağırdığı yöntemleri yazacak ve sunucuda Yöntemler çağıracaklarınız.</span><span class="sxs-lookup"><span data-stu-id="9c550-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="9c550-140">Sunucu yöntemlerini çağırmak için kod yazdığınızda, oluşturulan ara sunucu, yerel bir işlev yürütüyorsunuz gibi görünen sözdizimini kullanmanıza olanak sağlar: `invoke('serverMethod', arg1, arg2)`yerine `serverMethod(arg1, arg2)` yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="9c550-141">Oluşturulan proxy sözdizimi, bir sunucu yöntemi adını yanlış yazdığınız takdirde anında ve okunaklı bir istemci tarafı hatası da sunar.</span><span class="sxs-lookup"><span data-stu-id="9c550-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="9c550-142">Proxy 'leri tanımlayan dosyayı el ile oluşturursanız, sunucu yöntemlerini çağıran kod yazmak için IntelliSense desteği de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="9c550-143">Örneğin, sunucusunda aşağıdaki hub sınıfına sahip olduğunuzu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="9c550-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="9c550-144">Aşağıdaki kod örnekleri, sunucuda `NewContosoChatMessage` yöntemi çağırmak ve sunucudan `addContosoChatMessageToPage` yönteminin çağırmaları almak için hangi JavaScript kodunun göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c550-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="9c550-145">**Oluşturulan ara sunucu ile**</span><span class="sxs-lookup"><span data-stu-id="9c550-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="9c550-146">**Oluşturulan proxy olmadan**</span><span class="sxs-lookup"><span data-stu-id="9c550-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="9c550-147">Oluşturulan ara sunucu ne zaman kullanılır?</span><span class="sxs-lookup"><span data-stu-id="9c550-147">When to use the generated proxy</span></span>

<span data-ttu-id="9c550-148">Sunucunun çağırdığı bir istemci yöntemi için birden çok olay işleyicisini kaydetmek istiyorsanız, oluşturulan proxy 'yi kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="9c550-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="9c550-149">Aksi takdirde, oluşturulan proxy 'yi kullanmayı seçebilirsiniz veya kodlama tercihinizi temel alan değil ' i seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="9c550-150">Kullanmayı tercih ederseniz, istemci kodunuzda bir `script` öğesinde "SignalR/Hub" URL 'sine başvurmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9c550-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="9c550-151">İstemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="9c550-151">Client setup</span></span>

<span data-ttu-id="9c550-152">JavaScript istemcisi jQuery ve SignalR Core JavaScript dosyasına başvurular gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9c550-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="9c550-153">JQuery sürümü 1.6.4 veya 1.7.2, 1.8.2 veya 1.9.1 gibi büyük bir sonraki sürüm olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9c550-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="9c550-154">Oluşturulan proxy 'yi kullanmaya karar verirseniz, SignalR tarafından oluşturulan ara sunucu JavaScript dosyası için de bir başvuruya ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="9c550-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="9c550-155">Aşağıdaki örnek, başvuruların oluşturulan proxy 'yi kullanan bir HTML sayfasında nasıl görünebileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c550-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="9c550-156">Bu başvuruların bu sıraya dahil edilmesi gerekir: öncelikle jQuery, SignalR Core ve SignalR proxy 'lerinin son.</span><span class="sxs-lookup"><span data-stu-id="9c550-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="9c550-157">Dinamik olarak oluşturulan ara sunucuya başvurma</span><span class="sxs-lookup"><span data-stu-id="9c550-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="9c550-158">Yukarıdaki örnekte, SignalR tarafından oluşturulan proxy 'nin başvurusu, fiziksel bir dosyaya değil, dinamik olarak oluşturulan JavaScript koduna sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9c550-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="9c550-159">SignalR, anında ara sunucu için JavaScript kodunu oluşturur ve "/SignalR/Hub" URL 'sine yanıt olarak istemciye hizmet verir.</span><span class="sxs-lookup"><span data-stu-id="9c550-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="9c550-160">`MapHubs` yönteminizin sunucusunda SignalR bağlantıları için farklı bir temel URL belirttiyseniz, dinamik olarak oluşturulan ara sunucu dosyasının URL 'SI, "/Hub" a eklenmiş olan özel URL 'niz olur.</span><span class="sxs-lookup"><span data-stu-id="9c550-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="9c550-161">Windows 8 (Windows Mağazası) JavaScript istemcileri için, dinamik olarak oluşturulan bir yerine fiziksel proxy dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c550-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="9c550-162">Daha fazla bilgi için, bu konunun ilerleyen bölümlerinde [SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma](#manualproxy) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="9c550-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="9c550-163">ASP.NET MVC 4 Razor görünümünde, ara sunucu dosya başvurunuz içindeki uygulama köküne başvurmak için tilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="9c550-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="9c550-164">MVC 4 ' te SignalR kullanma hakkında daha fazla bilgi için bkz. [SignalR ve MVC 4 Ile çalışmaya](tutorial-getting-started-with-signalr-and-mvc-4.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="9c550-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="9c550-165">Bir ASP.NET MVC 3 Razor görünümünde, proxy dosyası başvurunuz için `Url.Content` kullanın:</span><span class="sxs-lookup"><span data-stu-id="9c550-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="9c550-166">Bir ASP.NET Web Forms uygulamasında, proxy dosyası başvurunuz için `ResolveClientUrl` kullanın veya bir uygulama kökü göreli yolu (tilde ile başlayarak) kullanarak ScriptManager aracılığıyla kaydedin:</span><span class="sxs-lookup"><span data-stu-id="9c550-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="9c550-167">Genel bir kural olarak, CSS veya JavaScript dosyaları için kullandığınız "/SignalR/Hub" URL 'sini belirtmek için aynı yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c550-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="9c550-168">Bir URL 'YI bir tilde kullanmadan belirtirseniz, bazı senaryolarda uygulamanız IIS Express kullanarak Visual Studio 'da test ettiğinizde doğru çalışacaktır ancak tam IIS 'e dağıtırken 404 hatasıyla başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="9c550-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="9c550-169">Daha fazla bilgi için MSDN sitesindeki [ASP.NET Web projeleri Için Visual Studio 'Daki Web sunucularındaki](https://msdn.microsoft.com/library/58wxa9w5.aspx) **kök düzeyindeki kaynaklara başvuruları çözme** konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="9c550-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="9c550-170">Visual Studio 2012 ' de bir Web projesini hata ayıklama modunda çalıştırdığınızda ve tarayıcınız olarak Internet Explorer kullanıyorsanız, aşağıdaki çizimde gösterildiği gibi, proxy dosyasını **betik belgeleri**altında **Çözüm Gezgini** görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![Çözüm Gezgini içinde JavaScript tarafından oluşturulan proxy dosyası](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="9c550-172">Dosyanın içeriğini görmek için **hub 'lara**çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9c550-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="9c550-173">Visual Studio 2012 ve Internet Explorer kullanmıyorsanız veya hata ayıklama modunda değilseniz, "/SignalR/Hub" URL 'sine giderek dosyanın içeriğini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="9c550-174">Örneğin, siteniz `http://localhost:56699`çalışıyorsa tarayıcınızda `http://localhost:56699/SignalR/hubs` gidin.</span><span class="sxs-lookup"><span data-stu-id="9c550-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="9c550-175">SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c550-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="9c550-176">Dinamik olarak oluşturulan ara sunucuya alternatif olarak, proxy koduna sahip ve bu dosyaya başvuran bir fiziksel dosya oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="9c550-177">Bu işlemi, önbelleğe alma veya paketleme davranışında denetim için ya da sunucu yöntemlerine yapılan çağrıları kodaktardığınızda IntelliSense 'i almak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="9c550-178">Bir proxy dosyası oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9c550-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="9c550-179">[Microsoft. Aspnet. SignalR. utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet paketini yükler.</span><span class="sxs-lookup"><span data-stu-id="9c550-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="9c550-180">Bir komut istemi açın ve SignalR. exe dosyasını içeren *Araçlar* klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="9c550-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="9c550-181">Araçlar klasörü şu konumdadır:</span><span class="sxs-lookup"><span data-stu-id="9c550-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="9c550-182">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="9c550-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="9c550-183">*. Dll* dosyanızın yolu, genellikle proje klasörünüzdeki *bin* klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="9c550-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="9c550-184">Bu komut, *SignalR. exe*ile aynı klasörde *Server. js* adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9c550-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="9c550-185">*Server. js* dosyasını projenize uygun bir klasöre yerleştirin, uygulamanız için uygun şekilde yeniden adlandırın ve "SignalR/hub 'lar" başvurusunun yerine buna bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c550-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="9c550-186">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="9c550-186">How to establish a connection</span></span>

<span data-ttu-id="9c550-187">Bir bağlantı kurmadan önce, bir bağlantı nesnesi oluşturmanız, bir ara sunucu oluşturmanız ve sunucudan çağrılabilecek yöntemler için olay işleyicilerini kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c550-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="9c550-188">Proxy ve olay işleyicileri ayarlandığında, `start` yöntemini çağırarak bağlantıyı kurun.</span><span class="sxs-lookup"><span data-stu-id="9c550-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="9c550-189">Oluşturulan proxy 'yi kullanıyorsanız, oluşturulan proxy kodu sizin için yaptığından, bağlantı nesnesini kendi kodunuzda oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9c550-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="9c550-190">**Bağlantı kurma (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="9c550-191">**Bağlantı kurma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="9c550-192">Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/SignalR" URL 'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9c550-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="9c550-193">Farklı bir temel URL belirtme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-/SignalR URL 'si](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="9c550-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="9c550-194">Normalde, bağlantıyı kurmak için `start` yöntemi çağrılmadan önce olay işleyicilerini kaydedersiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="9c550-195">Bağlantıyı kurduktan sonra bazı olay işleyicilerini kaydetmek istiyorsanız bunu yapabilirsiniz, ancak `start` yöntemi çağrılmadan önce olay işleyicilerden en az birini kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c550-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="9c550-196">Bunun bir nedeni, bir uygulamada birçok hub olabilir, ancak yalnızca bunlardan birine kullanacaksanız, her hub 'da `OnConnected` olayını tetiklemeniz istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="9c550-197">Bağlantı oluşturulduğunda, bir hub proxy üzerinde istemci yönteminin bulunması, SignalR 'nin `OnConnected` olayını tetiklemesine söyleme yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="9c550-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="9c550-198">`start` yöntemi çağrılmadan önce herhangi bir olay işleyicisini kaydetmezseniz, Hub üzerinde Yöntemler çağırabileceksiniz, ancak hub 'ın `OnConnected` yöntemi çağrılmaz ve sunucudan hiçbir istemci yöntemi çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="9c550-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="9c550-199">$. Connection. hub, $. hubConnection () tarafından oluşturulan nesnedir.</span><span class="sxs-lookup"><span data-stu-id="9c550-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="9c550-200">Örneklerden görebileceğiniz gibi, oluşturulan proxy 'yi kullandığınızda `$.connection.hub` bağlantı nesnesine başvurur.</span><span class="sxs-lookup"><span data-stu-id="9c550-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="9c550-201">Bu, oluşturulan proxy 'yi kullanmadığınız zaman `$.hubConnection()` çağırarak elde ettiğiniz nesnedir.</span><span class="sxs-lookup"><span data-stu-id="9c550-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="9c550-202">Oluşturulan proxy kodu, aşağıdaki ifadeyi yürüterek bağlantıyı sizin için oluşturur:</span><span class="sxs-lookup"><span data-stu-id="9c550-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Oluşturulan proxy dosyasında bağlantı oluşturma](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="9c550-204">Oluşturulan proxy 'yi kullanırken, oluşturulan proxy 'yi kullanmadığınız sırada bir bağlantı nesnesiyle yapabileceğiniz `$.connection.hub` her şeyi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="9c550-205">Start yönteminin zaman uyumsuz yürütmesi</span><span class="sxs-lookup"><span data-stu-id="9c550-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="9c550-206">`start` yöntemi zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="9c550-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="9c550-207">Bir [jQuery ertelenmiş nesnesi](http://api.jquery.com/category/deferred-object/)döndürür; bu, `pipe`, `done`ve `fail`gibi yöntemleri çağırarak geri çağırma işlevleri ekleyebileceðiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9c550-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="9c550-208">Bağlantı kurulduktan sonra, örneğin bir sunucu yöntemine yapılan çağrı gibi yürütmek istediğiniz kod varsa, bu kodu bir geri çağırma işlevine koyun veya bir geri çağırma işlevinden çağırın.</span><span class="sxs-lookup"><span data-stu-id="9c550-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="9c550-209">`.done` geri çağırma yöntemi, bağlantı kurulduktan sonra ve sunucudaki `OnConnected` olay işleyicisi yönteminde bulunan herhangi bir kod yürütmeyi bitirdiğinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="9c550-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="9c550-210">Yukarıdaki örnekteki "Şimdi bağlandı" ifadesini, `start` yöntem çağrısından (`.done` bir geri çağırmadan değil) sonraki kod satırı olarak yerleştirirseniz, aşağıdaki örnekte gösterildiği gibi `console.log` satırı bağlantı oluşturulmadan önce yürütülür:</span><span class="sxs-lookup"><span data-stu-id="9c550-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Bağlantı kurulduktan sonra çalışan kodu yazmanın yanlış yolu](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="9c550-212">Etki alanları arası bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="9c550-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="9c550-213">Genellikle tarayıcı `http://contoso.com`bir sayfa yüklerse, SignalR bağlantısı aynı etki alanında, `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="9c550-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="9c550-214">`http://contoso.com` sayfa, etki alanları arası bağlantı olan `http://fabrikam.com/signalr`bir bağlantı yapıyorsa.</span><span class="sxs-lookup"><span data-stu-id="9c550-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="9c550-215">Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="9c550-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="9c550-216">Etki alanları arası bağlantı kurmak için sunucuda etki alanları arası bağlantıların etkinleştirildiğinden emin olun ve bağlantı nesnesini oluştururken bağlantı URL 'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="9c550-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="9c550-217">SignalR, [JSONP](http://en.wikipedia.org/wiki/JSONP) veya [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)gibi etki alanları arası bağlantılar için uygun teknolojiyi kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="9c550-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="9c550-218">Sunucusunda, `MapHubs` yöntemini çağırdığınızda bu seçeneği belirleyerek etki alanları arası bağlantıları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9c550-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="9c550-219">İstemci üzerinde, bağlantı nesnesini oluştururken (oluşturulan proxy olmadan) veya Start yöntemini (oluşturulan ara sunucu ile) çağırmadan önce URL 'YI belirtin.</span><span class="sxs-lookup"><span data-stu-id="9c550-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="9c550-220">**Çapraz etki alanı bağlantısını belirten istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="9c550-221">**Çapraz etki alanı bağlantısını belirten istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="9c550-222">`$.hubConnection` oluşturucusunu kullandığınızda, otomatik olarak eklendiği için, URL 'ye `signalr` eklemeniz gerekmez (`useDefaultUrl` `false`olarak belirtmediğiniz sürece).</span><span class="sxs-lookup"><span data-stu-id="9c550-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="9c550-223">Farklı uç noktalara birden fazla bağlantı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="9c550-224">Kodunuzda `jQuery.support.cors` true olarak ayarlama.</span><span class="sxs-lookup"><span data-stu-id="9c550-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![JQuery. support. CORS 'yi true olarak ayarlama](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="9c550-226">SignalR, JSONP veya CORS kullanımını işler.</span><span class="sxs-lookup"><span data-stu-id="9c550-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="9c550-227">`jQuery.support.cors` true olarak ayarlamak, SignalR 'nin tarayıcının CORS 'yi desteklediğini varsaymasına neden olduğundan JSONP 'yi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="9c550-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="9c550-228">Bir localhost URL 'sine bağlanırken, Internet Explorer 10 bir etki alanları arası bağlantıyı düşünmez, bu nedenle sunucuda etki alanları arası bağlantıları etkinleştirmemiş olsanız bile, uygulama IE 10 ile yerel olarak çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="9c550-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="9c550-229">Internet Explorer 9 ile etki alanları arası bağlantıları kullanma hakkında daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)bakın.</span><span class="sxs-lookup"><span data-stu-id="9c550-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="9c550-230">Chrome ile etki alanları arası bağlantıları kullanma hakkında daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)bakın.</span><span class="sxs-lookup"><span data-stu-id="9c550-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="9c550-231">Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/SignalR" URL 'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9c550-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="9c550-232">Farklı bir temel URL belirtme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-/SignalR URL 'si](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="9c550-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="9c550-233">Bağlantıyı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9c550-233">How to configure the connection</span></span>

<span data-ttu-id="9c550-234">Bir bağlantı kurmadan önce sorgu dizesi parametreleri belirtebilir veya taşıma yöntemini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="9c550-235">Sorgu dizesi parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="9c550-235">How to specify query string parameters</span></span>

<span data-ttu-id="9c550-236">İstemci bağlandığı zaman sunucuya veri göndermek istiyorsanız, bağlantı nesnesine sorgu dizesi parametreleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="9c550-237">Aşağıdaki örneklerde, istemci kodunda bir sorgu dizesi parametresinin nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9c550-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="9c550-238">**Start metodunu çağırmadan önce bir sorgu dizesi değeri ayarlayın (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="9c550-239">**Start metodunu çağırmadan önce bir sorgu dizesi değeri ayarlayın (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="9c550-240">Aşağıdaki örnek, sunucu kodundaki bir sorgu dizesi parametresinin nasıl okunacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c550-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="9c550-241">Taşıma yöntemini belirtme</span><span class="sxs-lookup"><span data-stu-id="9c550-241">How to specify the transport method</span></span>

<span data-ttu-id="9c550-242">Bağlantı sürecinin bir parçası olarak, bir SignalR istemcisi normalde sunucu ve istemci tarafından desteklenen en iyi aktarımı tespit etmek üzere sunucuyla görüşür.</span><span class="sxs-lookup"><span data-stu-id="9c550-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="9c550-243">Kullanmak istediğiniz taşımayı zaten biliyorsanız, `start` yöntemini çağırdığınızda Transport metodunu belirterek bu anlaşma sürecini atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="9c550-244">**Taşıma yöntemini belirten istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="9c550-245">**Taşıma yöntemini belirten istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="9c550-246">Alternatif olarak, SignalR 'nin bunları denemesini istediğiniz sırada birden çok taşıma yöntemi belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c550-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="9c550-247">**Özel bir taşıma geri dönüş şeması belirten istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="9c550-248">**Özel bir taşıma geri dönüş şeması belirten istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="9c550-249">Taşıma yöntemini belirtmek için aşağıdaki değerleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c550-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="9c550-250">WebSockets</span><span class="sxs-lookup"><span data-stu-id="9c550-250">"webSockets"</span></span>
- <span data-ttu-id="9c550-251">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="9c550-251">"foreverFrame"</span></span>
- <span data-ttu-id="9c550-252">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="9c550-252">"serverSentEvents"</span></span>
- <span data-ttu-id="9c550-253">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="9c550-253">"longPolling"</span></span>

<span data-ttu-id="9c550-254">Aşağıdaki örneklerde, bir bağlantı tarafından hangi taşıma yönteminin kullanıldığını nasıl bulacağınız gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9c550-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="9c550-255">**Bir bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="9c550-256">**Bir bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="9c550-257">Sunucu kodundaki aktarım yöntemini denetleme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-bağlam özelliğinden istemci hakkında bilgi alma](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="9c550-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="9c550-258">Aktarımlar ve geri göndermeler hakkında daha fazla bilgi için bkz. [SignalR 'ye giriş-aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="9c550-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="9c550-259">Hub sınıfı için proxy alma</span><span class="sxs-lookup"><span data-stu-id="9c550-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="9c550-260">Oluşturduğunuz her bağlantı nesnesi bir veya daha fazla hub sınıfı içeren bir SignalR hizmetine bağlantı hakkındaki bilgileri kapsüller.</span><span class="sxs-lookup"><span data-stu-id="9c550-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="9c550-261">Bir hub sınıfıyla iletişim kurmak için kendi oluşturduğunuz (oluşturulan proxy kullanmıyorsanız) veya sizin için oluşturulan bir ara sunucu nesnesi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="9c550-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="9c550-262">İstemci üzerinde, proxy adı hub sınıfı adının Camel bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="9c550-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="9c550-263">SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="9c550-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="9c550-264">**Sunucudaki hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="9c550-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="9c550-265">**Hub için üretilen istemci ara sunucusuna bir başvuru alın**</span><span class="sxs-lookup"><span data-stu-id="9c550-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="9c550-266">**Hub sınıfı için istemci ara sunucusu oluşturma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="9c550-267">Hub sınıfınızı bir `HubName` özniteliğiyle süslemek isterseniz, büyük/küçük harf durumunu değiştirmeden tam adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c550-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="9c550-268">**HubName özniteliğine sahip sunucudaki hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="9c550-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="9c550-269">**Hub için üretilen istemci ara sunucusuna bir başvuru alın**</span><span class="sxs-lookup"><span data-stu-id="9c550-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="9c550-270">**Hub sınıfı için istemci ara sunucusu oluşturma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="9c550-271">İstemcide sunucunun çağırabir yöntemi tanımlama</span><span class="sxs-lookup"><span data-stu-id="9c550-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="9c550-272">Sunucunun bir hub 'dan çağıracaı bir yöntemi tanımlamak için, oluşturulan proxy 'nin `client` özelliğini kullanarak hub proxy 'sine bir olay işleyicisi ekleyin veya oluşturulan proxy kullanmıyorsanız `on` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9c550-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="9c550-273">Parametreler karmaşık nesneler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9c550-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="9c550-274">Bağlantıyı kurmak için `start` yöntemini çağırmadan önce olay işleyicisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c550-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="9c550-275">(`start` yöntemini çağırdıktan sonra olay işleyicileri eklemek istiyorsanız, bu belgede daha önce [bir bağlantı kurma](#establishconnection) bölümündeki nota bakın ve oluşturulan proxy 'yi kullanmadan bir yöntemi tanımlamak için gösterilen sözdizimini kullanın.)</span><span class="sxs-lookup"><span data-stu-id="9c550-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="9c550-276">Yöntem adı eşleştirme, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="9c550-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="9c550-277">Örneğin, sunucusundaki `Clients.All.addContosoChatMessageToPage`, istemcide `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`veya `addcontosochatmessagetopage` yürütülür.</span><span class="sxs-lookup"><span data-stu-id="9c550-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="9c550-278">**İstemci üzerinde yöntemi tanımlama (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="9c550-279">**İstemci üzerinde yöntemi tanımlamanın alternatif yolu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="9c550-280">**İstemci üzerinde yöntemi tanımlayın (oluşturulan ara sunucu olmadan veya başlangıç yöntemini çağırdıktan sonra eklenirken)**</span><span class="sxs-lookup"><span data-stu-id="9c550-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="9c550-281">**İstemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="9c550-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="9c550-282">Aşağıdaki örnekler, bir yöntem parametresi olarak karmaşık bir nesne içerir.</span><span class="sxs-lookup"><span data-stu-id="9c550-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="9c550-283">**İstemci üzerinde karmaşık bir nesne alan (oluşturulan ara sunucu ile) yöntemi tanımlayın**</span><span class="sxs-lookup"><span data-stu-id="9c550-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="9c550-284">**İstemci üzerinde karmaşık bir nesne alan (oluşturulan proxy olmadan) yöntemi tanımlayın**</span><span class="sxs-lookup"><span data-stu-id="9c550-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="9c550-285">**Karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="9c550-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="9c550-286">**Karmaşık bir nesne kullanarak istemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="9c550-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="9c550-287">İstemciden sunucu yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="9c550-287">How to call server methods from the client</span></span>

<span data-ttu-id="9c550-288">İstemciden bir sunucu yöntemi çağırmak için, oluşturulan proxy 'yi kullanmıyorsanız, oluşturulan ara sunucunun `server` özelliğini veya hub proxy üzerinde `invoke` yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c550-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="9c550-289">Dönüş değeri veya parametreleri karmaşık nesneler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9c550-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="9c550-290">Hub üzerindeki yöntem adının Camel bir sürümünü geçirin.</span><span class="sxs-lookup"><span data-stu-id="9c550-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="9c550-291">SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="9c550-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="9c550-292">Aşağıdaki örneklerde, dönüş değeri olmayan bir sunucu yönteminin nasıl çağrılacağını ve dönüş değerine sahip bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9c550-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="9c550-293">**HubMethodName özniteliği olmayan sunucu yöntemi**</span><span class="sxs-lookup"><span data-stu-id="9c550-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="9c550-294">**Bir parametreye geçirilen karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="9c550-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="9c550-295">**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="9c550-296">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="9c550-297">Hub yöntemini bir `HubMethodName` özniteliğiyle Süsleriniz durumunda bu adı, büyük/küçük harf olmadan kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c550-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="9c550-298">HubMethodName özniteliğiyle **sunucu yöntemi**</span><span class="sxs-lookup"><span data-stu-id="9c550-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="9c550-299">**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="9c550-300">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="9c550-301">Yukarıdaki örneklerde, dönüş değeri olmayan bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9c550-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="9c550-302">Aşağıdaki örneklerde, dönüş değeri olan bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9c550-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="9c550-303">**Dönüş değerine sahip bir yöntem için sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="9c550-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="9c550-304">Dönüş değeri **için kullanılan hisse senedi sınıfı**</span><span class="sxs-lookup"><span data-stu-id="9c550-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="9c550-305">**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="9c550-306">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="9c550-307">Bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="9c550-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="9c550-308">SignalR, işleyebilmeniz için aşağıdaki bağlantı ömrü olaylarını sağlar:</span><span class="sxs-lookup"><span data-stu-id="9c550-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="9c550-309">`starting`: bağlantı üzerinden herhangi bir veri gönderilmeden önce tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9c550-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="9c550-310">`received`: bağlantıda herhangi bir veri alındığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9c550-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="9c550-311">Alınan verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c550-311">Provides the received data.</span></span>
- <span data-ttu-id="9c550-312">`connectionSlow`: istemci yavaş veya sık bir bırakma bağlantısı algıladığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9c550-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="9c550-313">`reconnecting`: temeldeki aktarım yeniden bağlanmaya başladığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9c550-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="9c550-314">`reconnected`: temeldeki aktarım yeniden bağlandığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9c550-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="9c550-315">`stateChanged`: bağlantı durumu değiştiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9c550-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="9c550-316">Eski durumu ve yeni durumu (bağlanma, bağlanma, yeniden bağlanma veya bağlantısı kesildi) sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c550-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="9c550-317">`disconnected`: bağlantının bağlantısı kesildiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9c550-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="9c550-318">Örneğin, dikkat çekici gecikmelere neden olabilecek bağlantı sorunları olduğunda uyarı iletilerini göstermek istiyorsanız `connectionSlow` olayını işleyin.</span><span class="sxs-lookup"><span data-stu-id="9c550-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="9c550-319">**Connectionlow olayını işle (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="9c550-320">**Connectionlow olayını işle (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="9c550-321">Daha fazla bilgi için bkz. [SignalR 'de bağlantı ömrü olaylarını anlama ve işleme](index.md).</span><span class="sxs-lookup"><span data-stu-id="9c550-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="9c550-322">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="9c550-322">How to handle errors</span></span>

<span data-ttu-id="9c550-323">SignalR JavaScript istemcisi, için bir işleyici ekleyebileceğiniz bir `error` olayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c550-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="9c550-324">Ayrıca, bir sunucu yöntemi çağrısından kaynaklanan hatalara yönelik bir işleyici eklemek için Fail metodunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c550-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="9c550-325">Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, bir hatadan sonra SignalR 'nin döndürdüğü özel durum nesnesi hata hakkında en az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="9c550-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="9c550-326">Örneğin, `newContosoChatMessage` çağrısı başarısız olursa, hata nesnesindeki hata iletisi, güvenlik nedenleriyle, üretim aşamasındaki istemcilere ayrıntılı hata iletileri gönderilmesi "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" içerir, ancak sorun giderme amacıyla ayrıntılı hata iletileri etkinleştirmek istiyorsanız, sunucuda aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c550-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="9c550-327">Aşağıdaki örnek, hata olayı için nasıl işleyicinin ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c550-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="9c550-328">**Hata işleyicisi ekleme (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="9c550-329">**Hata işleyicisi ekleme (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="9c550-330">Aşağıdaki örnek, bir yöntem çağrısından bir hatanın nasıl işleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c550-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="9c550-331">**Yöntem çağrısından bir hata işleme (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="9c550-332">**Yöntem çağrısından bir hata işleme (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="9c550-333">Bir yöntem çağrısı başarısız olursa, `error` olayı da oluşturulur, bu nedenle `error` yöntemi işleyicisindeki kodunuz ve `.fail` Yöntem geri çağırması yürütülür.</span><span class="sxs-lookup"><span data-stu-id="9c550-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="9c550-334">İstemci tarafı günlük kaydını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9c550-334">How to enable client-side logging</span></span>

<span data-ttu-id="9c550-335">Bir bağlantıda istemci tarafı günlüğe kaydetmeyi etkinleştirmek için, bağlantıyı kurmak üzere `start` yöntemini çağırmadan önce bağlantı nesnesindeki `logging` özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9c550-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="9c550-336">**Günlüğe kaydetmeyi etkinleştirme (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="9c550-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="9c550-337">**Günlüğe kaydetmeyi etkinleştir (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="9c550-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="9c550-338">Günlükleri görmek için tarayıcınızın geliştirici araçlarını açın ve konsol sekmesine gidin. Bunun nasıl yapılacağını gösteren adım adım yönergeleri ve ekran görüntülerini gösteren bir öğretici için, bkz. [ASP.NET SignalR Ile sunucu yayını-günlüğü etkinleştirme](index.md).</span><span class="sxs-lookup"><span data-stu-id="9c550-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
