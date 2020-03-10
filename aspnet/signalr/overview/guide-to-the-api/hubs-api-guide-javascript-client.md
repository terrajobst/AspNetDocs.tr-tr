---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi | Microsoft Docs
author: bradygaster
description: Bu belgede, browsers ve Windows Mağazası (WinJS) Applicat gibi JavaScript istemcilerinde SignalR sürüm 2 için hub API 'sini kullanma hakkında bir giriş sunulmaktadır...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536661"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="a3532-103">ASP.NET SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi</span><span class="sxs-lookup"><span data-stu-id="a3532-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="a3532-104">Bu belgede, browsers ve Windows Mağazası (WinJS) uygulamaları gibi JavaScript istemcilerinde SignalR sürüm 2 için hub API 'sinin kullanılmasına bir giriş sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a3532-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="a3532-105">SignalR hub 'Ları API 'SI, uzak yordam çağrılarını (RPC) bir sunucudan, istemcilerden ve istemcilerden sunucuya bağlı hale getirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3532-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="a3532-106">Sunucu kodu ' nda, istemciler tarafından çağrılabilen Yöntemler tanımlar ve istemcide çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="a3532-107">İstemci kodunda, sunucudan çağrılabilen yöntemleri tanımlayabilir ve sunucuda çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="a3532-108">SignalR, sizin için istemciden sunucuya sıhhi kını ele alır.</span><span class="sxs-lookup"><span data-stu-id="a3532-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="a3532-109">SignalR Ayrıca kalıcı bağlantılar adlı alt düzey bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="a3532-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="a3532-110">SignalR, hub 'Lar ve kalıcı bağlantılara giriş için bkz. [SignalR 'ye giriş](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="a3532-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="a3532-111">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="a3532-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="a3532-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a3532-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="a3532-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="a3532-113">.NET 4.5</span></span>
> - <span data-ttu-id="a3532-114">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="a3532-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="a3532-115">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="a3532-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="a3532-116">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="a3532-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="a3532-117">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="a3532-117">Questions and comments</span></span>
>
> <span data-ttu-id="a3532-118">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="a3532-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="a3532-119">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="a3532-120">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="a3532-120">Overview</span></span>

<span data-ttu-id="a3532-121">Bu belgede aşağıdaki bölümler yer alır:</span><span class="sxs-lookup"><span data-stu-id="a3532-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="a3532-122">Oluşturulan ara sunucu ve sizin için ne yapar</span><span class="sxs-lookup"><span data-stu-id="a3532-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="a3532-123">Oluşturulan ara sunucu ne zaman kullanılır?</span><span class="sxs-lookup"><span data-stu-id="a3532-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="a3532-124">İstemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="a3532-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="a3532-125">Dinamik olarak oluşturulan ara sunucuya başvurma</span><span class="sxs-lookup"><span data-stu-id="a3532-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="a3532-126">SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="a3532-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="a3532-127">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="a3532-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="a3532-128">$. Connection. hub, $. hubConnection () tarafından oluşturulan nesnedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="a3532-129">Start yönteminin zaman uyumsuz yürütmesi</span><span class="sxs-lookup"><span data-stu-id="a3532-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="a3532-130">Etki alanları arası bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="a3532-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="a3532-131">Bağlantıyı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a3532-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="a3532-132">Sorgu dizesi parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="a3532-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="a3532-133">Taşıma yöntemini belirtme</span><span class="sxs-lookup"><span data-stu-id="a3532-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="a3532-134">Hub sınıfı için proxy alma</span><span class="sxs-lookup"><span data-stu-id="a3532-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="a3532-135">İstemcide sunucunun çağırabir yöntemi tanımlama</span><span class="sxs-lookup"><span data-stu-id="a3532-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="a3532-136">İstemciden sunucu yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="a3532-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="a3532-137">Bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="a3532-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="a3532-138">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="a3532-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="a3532-139">İstemci tarafı günlük kaydını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a3532-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="a3532-140">Sunucu veya .NET istemcilerini programlama hakkında belgeler için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="a3532-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="a3532-141">SignalR hub 'Ları API Kılavuzu-sunucu</span><span class="sxs-lookup"><span data-stu-id="a3532-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="a3532-142">SignalR hub 'Ları API Kılavuzu-.NET Istemcisi</span><span class="sxs-lookup"><span data-stu-id="a3532-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="a3532-143">SignalR 2 sunucu bileşeni yalnızca .NET 4,5 ' de kullanılabilir (ancak .NET 4,0 ' de SignalR 2 için bir .NET istemcisi vardır).</span><span class="sxs-lookup"><span data-stu-id="a3532-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="a3532-144">Oluşturulan ara sunucu ve sizin için ne yapar</span><span class="sxs-lookup"><span data-stu-id="a3532-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="a3532-145">Bir JavaScript istemcisini, bir SignalR hizmeti ile iletişim kurmak için, SignalR 'nin sizin için oluşturduğu bir ara sunucu olmadan veya olmadan iletişim kurmaya programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="a3532-146">Proxy 'nin ne için yaptığı, bağlanmak için kullandığınız kodun sözdizimini basitleştirecek, sunucunun çağırdığı yöntemleri yazacak ve sunucuda Yöntemler çağıracaklarınız.</span><span class="sxs-lookup"><span data-stu-id="a3532-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="a3532-147">Sunucu yöntemlerini çağırmak için kod yazdığınızda, oluşturulan ara sunucu, yerel bir işlev yürütüyorsunuz gibi görünen sözdizimini kullanmanıza olanak sağlar: `invoke('serverMethod', arg1, arg2)`yerine `serverMethod(arg1, arg2)` yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="a3532-148">Oluşturulan proxy sözdizimi, bir sunucu yöntemi adını yanlış yazdığınız takdirde anında ve okunaklı bir istemci tarafı hatası da sunar.</span><span class="sxs-lookup"><span data-stu-id="a3532-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="a3532-149">Proxy 'leri tanımlayan dosyayı el ile oluşturursanız, sunucu yöntemlerini çağıran kod yazmak için IntelliSense desteği de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="a3532-150">Örneğin, sunucusunda aşağıdaki hub sınıfına sahip olduğunuzu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="a3532-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="a3532-151">Aşağıdaki kod örnekleri, sunucuda `NewContosoChatMessage` yöntemi çağırmak ve sunucudan `addContosoChatMessageToPage` yönteminin çağırmaları almak için hangi JavaScript kodunun göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="a3532-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="a3532-152">**Oluşturulan ara sunucu ile**</span><span class="sxs-lookup"><span data-stu-id="a3532-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="a3532-153">**Oluşturulan proxy olmadan**</span><span class="sxs-lookup"><span data-stu-id="a3532-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="a3532-154">Oluşturulan ara sunucu ne zaman kullanılır?</span><span class="sxs-lookup"><span data-stu-id="a3532-154">When to use the generated proxy</span></span>

<span data-ttu-id="a3532-155">Sunucunun çağırdığı bir istemci yöntemi için birden çok olay işleyicisini kaydetmek istiyorsanız, oluşturulan proxy 'yi kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="a3532-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="a3532-156">Aksi takdirde, oluşturulan proxy 'yi kullanmayı seçebilirsiniz veya kodlama tercihinizi temel alan değil ' i seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="a3532-157">Kullanmayı tercih ederseniz, istemci kodunuzda bir `script` öğesinde "SignalR/Hub" URL 'sine başvurmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a3532-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="a3532-158">İstemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="a3532-158">Client setup</span></span>

<span data-ttu-id="a3532-159">JavaScript istemcisi jQuery ve SignalR Core JavaScript dosyasına başvurular gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a3532-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="a3532-160">JQuery sürümü 1.6.4 veya 1.7.2, 1.8.2 veya 1.9.1 gibi büyük bir sonraki sürüm olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a3532-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="a3532-161">Oluşturulan proxy 'yi kullanmaya karar verirseniz, SignalR tarafından oluşturulan ara sunucu JavaScript dosyası için de bir başvuruya ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="a3532-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="a3532-162">Aşağıdaki örnek, başvuruların oluşturulan proxy 'yi kullanan bir HTML sayfasında nasıl görünebileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a3532-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="a3532-163">Bu başvuruların bu sıraya dahil edilmesi gerekir: öncelikle jQuery, SignalR Core ve SignalR proxy 'lerinin son.</span><span class="sxs-lookup"><span data-stu-id="a3532-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="a3532-164">Dinamik olarak oluşturulan ara sunucuya başvurma</span><span class="sxs-lookup"><span data-stu-id="a3532-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="a3532-165">Yukarıdaki örnekte, SignalR tarafından oluşturulan proxy 'nin başvurusu, fiziksel bir dosyaya değil, dinamik olarak oluşturulan JavaScript koduna sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a3532-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="a3532-166">SignalR, anında ara sunucu için JavaScript kodunu oluşturur ve "/SignalR/Hub" URL 'sine yanıt olarak istemciye hizmet verir.</span><span class="sxs-lookup"><span data-stu-id="a3532-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="a3532-167">`MapSignalR` yönteminizin sunucusunda SignalR bağlantıları için farklı bir temel URL belirttiyseniz, dinamik olarak oluşturulan ara sunucu dosyasının URL 'SI, "/Hub" a eklenmiş olan özel URL 'niz olur.</span><span class="sxs-lookup"><span data-stu-id="a3532-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="a3532-168">Windows 8 (Windows Mağazası) JavaScript istemcileri için, dinamik olarak oluşturulan bir yerine fiziksel proxy dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3532-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="a3532-169">Daha fazla bilgi için, bu konunun ilerleyen bölümlerinde [SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma](#manualproxy) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="a3532-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="a3532-170">Bir ASP.NET MVC 4 veya 5 Razor görünümünde, proxy dosyası başvurunuz içindeki uygulama köküne başvurmak için tilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="a3532-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="a3532-171">MVC 5 ' te SignalR kullanma hakkında daha fazla bilgi için bkz. [SignalR ve MVC 5 Ile çalışmaya](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="a3532-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="a3532-172">Bir ASP.NET MVC 3 Razor görünümünde, proxy dosyası başvurunuz için `Url.Content` kullanın:</span><span class="sxs-lookup"><span data-stu-id="a3532-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="a3532-173">Bir ASP.NET Web Forms uygulamasında, proxy dosyası başvurunuz için `ResolveClientUrl` kullanın veya bir uygulama kökü göreli yolu (tilde ile başlayarak) kullanarak ScriptManager aracılığıyla kaydedin:</span><span class="sxs-lookup"><span data-stu-id="a3532-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="a3532-174">Genel bir kural olarak, CSS veya JavaScript dosyaları için kullandığınız "/SignalR/Hub" URL 'sini belirtmek için aynı yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3532-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="a3532-175">Bir URL 'YI bir tilde kullanmadan belirtirseniz, bazı senaryolarda uygulamanız IIS Express kullanarak Visual Studio 'da test ettiğinizde doğru çalışacaktır ancak tam IIS 'e dağıtırken 404 hatasıyla başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a3532-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="a3532-176">Daha fazla bilgi için MSDN sitesindeki [ASP.NET Web projeleri Için Visual Studio 'Daki Web sunucularındaki](https://msdn.microsoft.com/library/58wxa9w5.aspx) **kök düzeyindeki kaynaklara başvuruları çözme** konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="a3532-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="a3532-177">Visual Studio 2017 ' de bir Web projesini hata ayıklama modunda çalıştırdığınızda ve tarayıcınız olarak Internet Explorer kullanıyorsanız, proxy dosyasını **betikler**altında **Çözüm Gezgini** görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="a3532-178">Dosyanın içeriğini görmek için **hub 'lara**çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a3532-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="a3532-179">Visual Studio 2012 veya 2013 ve Internet Explorer kullanmıyorsanız veya hata ayıklama modunda değilseniz, "/SignalR/Hub" URL 'sine giderek dosyanın içeriğini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="a3532-180">Örneğin, siteniz `http://localhost:56699`çalışıyorsa tarayıcınızda `http://localhost:56699/SignalR/hubs` gidin.</span><span class="sxs-lookup"><span data-stu-id="a3532-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="a3532-181">SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="a3532-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="a3532-182">Dinamik olarak oluşturulan ara sunucuya alternatif olarak, proxy koduna sahip ve bu dosyaya başvuran bir fiziksel dosya oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="a3532-183">Bu işlemi, önbelleğe alma veya paketleme davranışında denetim için ya da sunucu yöntemlerine yapılan çağrıları kodaktardığınızda IntelliSense 'i almak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="a3532-184">Bir proxy dosyası oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a3532-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="a3532-185">[Microsoft. Aspnet. SignalR. utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet paketini yükler.</span><span class="sxs-lookup"><span data-stu-id="a3532-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="a3532-186">Bir komut istemi açın ve SignalR. exe dosyasını içeren *Araçlar* klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="a3532-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="a3532-187">Araçlar klasörü şu konumdadır:</span><span class="sxs-lookup"><span data-stu-id="a3532-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="a3532-188">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="a3532-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="a3532-189">*. Dll* dosyanızın yolu, genellikle proje klasörünüzdeki *bin* klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="a3532-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="a3532-190">Bu komut, *SignalR. exe*ile aynı klasörde *Server. js* adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a3532-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="a3532-191">*Server. js* dosyasını projenize uygun bir klasöre yerleştirin, uygulamanız için uygun şekilde yeniden adlandırın ve "SignalR/hub 'lar" başvurusunun yerine buna bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a3532-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="a3532-192">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="a3532-192">How to establish a connection</span></span>

<span data-ttu-id="a3532-193">Bir bağlantı kurmadan önce, bir bağlantı nesnesi oluşturmanız, bir ara sunucu oluşturmanız ve sunucudan çağrılabilecek yöntemler için olay işleyicilerini kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a3532-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="a3532-194">Proxy ve olay işleyicileri ayarlandığında, `start` yöntemini çağırarak bağlantıyı kurun.</span><span class="sxs-lookup"><span data-stu-id="a3532-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="a3532-195">Oluşturulan proxy 'yi kullanıyorsanız, oluşturulan proxy kodu sizin için yaptığından, bağlantı nesnesini kendi kodunuzda oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a3532-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="a3532-196">**Bağlantı kurma (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="a3532-197">**Bağlantı kurma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="a3532-198">Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/SignalR" URL 'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a3532-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="a3532-199">Farklı bir temel URL belirtme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-/SignalR URL 'si](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="a3532-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="a3532-200">Varsayılan olarak, hub konumu geçerli sunucusudur; farklı bir sunucuya bağlanıyorsanız, aşağıdaki örnekte gösterildiği gibi `start` yöntemi çağrılmadan önce URL 'YI belirtin:</span><span class="sxs-lookup"><span data-stu-id="a3532-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="a3532-201">Normalde, bağlantıyı kurmak için `start` yöntemi çağrılmadan önce olay işleyicilerini kaydedersiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="a3532-202">Bağlantıyı kurduktan sonra bazı olay işleyicilerini kaydetmek istiyorsanız bunu yapabilirsiniz, ancak `start` yöntemi çağrılmadan önce olay işleyicilerden en az birini kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a3532-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="a3532-203">Bunun bir nedeni, bir uygulamada birçok hub olabilir, ancak yalnızca bunlardan birine kullanacaksanız, her hub 'da `OnConnected` olayını tetiklemeniz istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="a3532-204">Bağlantı oluşturulduğunda, bir hub proxy üzerinde istemci yönteminin bulunması, SignalR 'nin `OnConnected` olayını tetiklemesine söyleme yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="a3532-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="a3532-205">`start` yöntemi çağrılmadan önce herhangi bir olay işleyicisini kaydetmezseniz, Hub üzerinde Yöntemler çağırabileceksiniz, ancak hub 'ın `OnConnected` yöntemi çağrılmaz ve sunucudan hiçbir istemci yöntemi çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="a3532-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="a3532-206">$. Connection. hub, $. hubConnection () tarafından oluşturulan nesnedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="a3532-207">Örneklerden görebileceğiniz gibi, oluşturulan proxy 'yi kullandığınızda `$.connection.hub` bağlantı nesnesine başvurur.</span><span class="sxs-lookup"><span data-stu-id="a3532-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="a3532-208">Bu, oluşturulan proxy 'yi kullanmadığınız zaman `$.hubConnection()` çağırarak elde ettiğiniz nesnedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="a3532-209">Oluşturulan proxy kodu, aşağıdaki ifadeyi yürüterek bağlantıyı sizin için oluşturur:</span><span class="sxs-lookup"><span data-stu-id="a3532-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Oluşturulan proxy dosyasında bağlantı oluşturma](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="a3532-211">Oluşturulan proxy 'yi kullanırken, oluşturulan proxy 'yi kullanmadığınız sırada bir bağlantı nesnesiyle yapabileceğiniz `$.connection.hub` her şeyi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="a3532-212">Start yönteminin zaman uyumsuz yürütmesi</span><span class="sxs-lookup"><span data-stu-id="a3532-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="a3532-213">`start` yöntemi zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a3532-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="a3532-214">Bir [jQuery ertelenmiş nesnesi](http://api.jquery.com/category/deferred-object/)döndürür; bu, `pipe`, `done`ve `fail`gibi yöntemleri çağırarak geri çağırma işlevleri ekleyebileceðiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a3532-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="a3532-215">Bağlantı kurulduktan sonra, örneğin bir sunucu yöntemine yapılan çağrı gibi yürütmek istediğiniz kod varsa, bu kodu bir geri çağırma işlevine koyun veya bir geri çağırma işlevinden çağırın.</span><span class="sxs-lookup"><span data-stu-id="a3532-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="a3532-216">`.done` geri çağırma yöntemi, bağlantı kurulduktan sonra ve sunucudaki `OnConnected` olay işleyicisi yönteminde bulunan herhangi bir kod yürütmeyi bitirdiğinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a3532-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="a3532-217">Yukarıdaki örnekteki "Şimdi bağlandı" ifadesini, `start` yöntem çağrısından (`.done` bir geri çağırmadan değil) sonraki kod satırı olarak yerleştirirseniz, aşağıdaki örnekte gösterildiği gibi `console.log` satırı bağlantı oluşturulmadan önce yürütülür:</span><span class="sxs-lookup"><span data-stu-id="a3532-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Bağlantı kurulduktan sonra çalışan kodu yazmanın yanlış yolu](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="a3532-219">Etki alanları arası bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="a3532-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="a3532-220">Genellikle tarayıcı `http://contoso.com`bir sayfa yüklerse, SignalR bağlantısı aynı etki alanında, `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="a3532-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="a3532-221">`http://contoso.com` sayfa, etki alanları arası bağlantı olan `http://fabrikam.com/signalr`bir bağlantı yapıyorsa.</span><span class="sxs-lookup"><span data-stu-id="a3532-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="a3532-222">Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="a3532-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="a3532-223">SignalR 1. x içinde, çapraz etki alanı istekleri tek bir EnableCrossDomain bayrağıyla denetlenir.</span><span class="sxs-lookup"><span data-stu-id="a3532-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="a3532-224">Bu bayrak hem JSONP hem de CORS isteklerini denetlediniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="a3532-225">Daha fazla esneklik için, tüm CORS desteği, SignalR 'nin sunucu bileşeninden kaldırılmıştır (JavaScript istemcileri tarayıcının desteklediği algılanırsa CORS 'yi yine de kullanır) ve bu senaryoları desteklemek için yeni OWıN ara yazılımı kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="a3532-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="a3532-226">İstemci üzerinde JSONP gerekliyse (eski tarayıcılarda etki alanları arası istekleri desteklemek için), aşağıda gösterildiği gibi, `HubConfiguration` `true`nesnesindeki `EnableJSONP` ayarlanarak açıkça etkinleştirilmesi gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="a3532-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="a3532-227">JSONP, CORS 'den daha az güvenli olduğu için varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="a3532-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="a3532-228">**Projenize Microsoft. Owin. CORS ekleme:** Bu kitaplığı yüklemek için, Paket Yöneticisi konsolunda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a3532-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="a3532-229">Bu komut, paketin 2.1.0 sürümünü projenize ekler.</span><span class="sxs-lookup"><span data-stu-id="a3532-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="a3532-230">UseCors çağrılıyor</span><span class="sxs-lookup"><span data-stu-id="a3532-230">Calling UseCors</span></span>

 <span data-ttu-id="a3532-231">Aşağıdaki kod parçacığı, SignalR 2 ' de etki alanları arası bağlantıların nasıl uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a3532-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="a3532-232">**SignalR 2 ' de etki alanları arası istekleri uygulama**</span><span class="sxs-lookup"><span data-stu-id="a3532-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="a3532-233">Aşağıdaki kod, bir SignalR 2 projesinde CORS veya JSONP 'nin nasıl etkinleştirileceğini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="a3532-234">Bu kod örneği, `MapSignalR`yerine `Map` ve `RunSignalR` kullanır, böylece CORS ara yazılımı yalnızca CORS desteği gerektiren SignalR istekleri için çalışır (`MapSignalR`' de belirtilen yoldaki tüm trafik için değil.) Eşleme, uygulamanın tamamı yerine belirli bir URL öneki için çalıştırılması gereken diğer tüm ara yazılımlar için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a3532-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="a3532-235">Kodunuzda `jQuery.support.cors` true olarak ayarlama.</span><span class="sxs-lookup"><span data-stu-id="a3532-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![JQuery. support. CORS 'yi true olarak ayarlama](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="a3532-237">SignalR CORS kullanımını işler.</span><span class="sxs-lookup"><span data-stu-id="a3532-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="a3532-238">`jQuery.support.cors` true olarak ayarlamak, SignalR 'nin tarayıcının CORS 'yi desteklediğini varsaymasına neden olduğundan JSONP 'yi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="a3532-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="a3532-239">Bir localhost URL 'sine bağlanırken, Internet Explorer 10 bir etki alanları arası bağlantıyı düşünmez, bu nedenle sunucuda etki alanları arası bağlantıları etkinleştirmemiş olsanız bile, uygulama IE 10 ile yerel olarak çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="a3532-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="a3532-240">Internet Explorer 9 ile etki alanları arası bağlantıları kullanma hakkında daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)bakın.</span><span class="sxs-lookup"><span data-stu-id="a3532-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="a3532-241">Chrome ile etki alanları arası bağlantıları kullanma hakkında daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)bakın.</span><span class="sxs-lookup"><span data-stu-id="a3532-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="a3532-242">Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/SignalR" URL 'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a3532-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="a3532-243">Farklı bir temel URL belirtme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-/SignalR URL 'si](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="a3532-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="a3532-244">Bağlantıyı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a3532-244">How to configure the connection</span></span>

<span data-ttu-id="a3532-245">Bir bağlantı kurmadan önce sorgu dizesi parametreleri belirtebilir veya taşıma yöntemini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="a3532-246">Sorgu dizesi parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="a3532-246">How to specify query string parameters</span></span>

<span data-ttu-id="a3532-247">İstemci bağlandığı zaman sunucuya veri göndermek istiyorsanız, bağlantı nesnesine sorgu dizesi parametreleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="a3532-248">Aşağıdaki örneklerde, istemci kodunda bir sorgu dizesi parametresinin nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="a3532-249">**Start metodunu çağırmadan önce bir sorgu dizesi değeri ayarlayın (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="a3532-250">**Start metodunu çağırmadan önce bir sorgu dizesi değeri ayarlayın (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="a3532-251">Aşağıdaki örnek, sunucu kodundaki bir sorgu dizesi parametresinin nasıl okunacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a3532-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="a3532-252">Taşıma yöntemini belirtme</span><span class="sxs-lookup"><span data-stu-id="a3532-252">How to specify the transport method</span></span>

<span data-ttu-id="a3532-253">Bağlantı sürecinin bir parçası olarak, bir SignalR istemcisi normalde sunucu ve istemci tarafından desteklenen en iyi aktarımı tespit etmek üzere sunucuyla görüşür.</span><span class="sxs-lookup"><span data-stu-id="a3532-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="a3532-254">Kullanmak istediğiniz taşımayı zaten biliyorsanız, `start` yöntemini çağırdığınızda Transport metodunu belirterek bu anlaşma sürecini atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="a3532-255">**Taşıma yöntemini belirten istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="a3532-256">**Taşıma yöntemini belirten istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="a3532-257">Alternatif olarak, SignalR 'nin bunları denemesini istediğiniz sırada birden çok taşıma yöntemi belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3532-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="a3532-258">**Özel bir taşıma geri dönüş şeması belirten istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="a3532-259">**Özel bir taşıma geri dönüş şeması belirten istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="a3532-260">Taşıma yöntemini belirtmek için aşağıdaki değerleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3532-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="a3532-261">WebSockets</span><span class="sxs-lookup"><span data-stu-id="a3532-261">"webSockets"</span></span>
- <span data-ttu-id="a3532-262">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="a3532-262">"foreverFrame"</span></span>
- <span data-ttu-id="a3532-263">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="a3532-263">"serverSentEvents"</span></span>
- <span data-ttu-id="a3532-264">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="a3532-264">"longPolling"</span></span>

<span data-ttu-id="a3532-265">Aşağıdaki örneklerde, bir bağlantı tarafından hangi taşıma yönteminin kullanıldığını nasıl bulacağınız gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="a3532-266">**Bir bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="a3532-267">**Bir bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="a3532-268">Sunucu kodundaki aktarım yöntemini denetleme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-bağlam özelliğinden istemci hakkında bilgi alma](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="a3532-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="a3532-269">Aktarımlar ve geri göndermeler hakkında daha fazla bilgi için bkz. [SignalR 'ye giriş-aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="a3532-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="a3532-270">Hub sınıfı için proxy alma</span><span class="sxs-lookup"><span data-stu-id="a3532-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="a3532-271">Oluşturduğunuz her bağlantı nesnesi bir veya daha fazla hub sınıfı içeren bir SignalR hizmetine bağlantı hakkındaki bilgileri kapsüller.</span><span class="sxs-lookup"><span data-stu-id="a3532-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="a3532-272">Bir hub sınıfıyla iletişim kurmak için kendi oluşturduğunuz (oluşturulan proxy kullanmıyorsanız) veya sizin için oluşturulan bir ara sunucu nesnesi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="a3532-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="a3532-273">İstemci üzerinde, proxy adı hub sınıfı adının Camel bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="a3532-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="a3532-274">SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="a3532-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="a3532-275">**Sunucudaki hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="a3532-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="a3532-276">**Hub için üretilen istemci ara sunucusuna bir başvuru alın**</span><span class="sxs-lookup"><span data-stu-id="a3532-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="a3532-277">**Hub sınıfı için istemci ara sunucusu oluşturma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="a3532-278">Hub sınıfınızı bir `HubName` özniteliğiyle süslemek isterseniz, büyük/küçük harf durumunu değiştirmeden tam adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3532-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="a3532-279">**HubName özniteliğine sahip sunucudaki hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="a3532-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="a3532-280">**Hub için üretilen istemci ara sunucusuna bir başvuru alın**</span><span class="sxs-lookup"><span data-stu-id="a3532-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="a3532-281">**Hub sınıfı için istemci ara sunucusu oluşturma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="a3532-282">İstemcide sunucunun çağırabir yöntemi tanımlama</span><span class="sxs-lookup"><span data-stu-id="a3532-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="a3532-283">Sunucunun bir hub 'dan çağıracaı bir yöntemi tanımlamak için, oluşturulan proxy 'nin `client` özelliğini kullanarak hub proxy 'sine bir olay işleyicisi ekleyin veya oluşturulan proxy kullanmıyorsanız `on` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a3532-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="a3532-284">Parametreler karmaşık nesneler olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3532-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="a3532-285">Bağlantıyı kurmak için `start` yöntemini çağırmadan önce olay işleyicisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a3532-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="a3532-286">(`start` yöntemini çağırdıktan sonra olay işleyicileri eklemek istiyorsanız, bu belgede daha önce [bir bağlantı kurma](#establishconnection) bölümündeki nota bakın ve oluşturulan proxy 'yi kullanmadan bir yöntemi tanımlamak için gösterilen sözdizimini kullanın.)</span><span class="sxs-lookup"><span data-stu-id="a3532-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="a3532-287">Yöntem adı eşleştirme, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="a3532-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="a3532-288">Örneğin, sunucusundaki `Clients.All.addContosoChatMessageToPage`, istemcide `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`veya `addcontosochatmessagetopage` yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a3532-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="a3532-289">**İstemci üzerinde yöntemi tanımlama (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="a3532-290">**İstemci üzerinde yöntemi tanımlamanın alternatif yolu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="a3532-291">**İstemci üzerinde yöntemi tanımlayın (oluşturulan ara sunucu olmadan veya başlangıç yöntemini çağırdıktan sonra eklenirken)**</span><span class="sxs-lookup"><span data-stu-id="a3532-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="a3532-292">**İstemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="a3532-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="a3532-293">Aşağıdaki örnekler, bir yöntem parametresi olarak karmaşık bir nesne içerir.</span><span class="sxs-lookup"><span data-stu-id="a3532-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="a3532-294">**İstemci üzerinde karmaşık bir nesne alan (oluşturulan ara sunucu ile) yöntemi tanımlayın**</span><span class="sxs-lookup"><span data-stu-id="a3532-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="a3532-295">**İstemci üzerinde karmaşık bir nesne alan (oluşturulan proxy olmadan) yöntemi tanımlayın**</span><span class="sxs-lookup"><span data-stu-id="a3532-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="a3532-296">**Karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="a3532-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="a3532-297">**Karmaşık bir nesne kullanarak istemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="a3532-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="a3532-298">İstemciden sunucu yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="a3532-298">How to call server methods from the client</span></span>

<span data-ttu-id="a3532-299">İstemciden bir sunucu yöntemi çağırmak için, oluşturulan proxy 'yi kullanmıyorsanız, oluşturulan ara sunucunun `server` özelliğini veya hub proxy üzerinde `invoke` yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3532-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="a3532-300">Dönüş değeri veya parametreleri karmaşık nesneler olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3532-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="a3532-301">Hub üzerindeki yöntem adının Camel bir sürümünü geçirin.</span><span class="sxs-lookup"><span data-stu-id="a3532-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="a3532-302">SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="a3532-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="a3532-303">Aşağıdaki örneklerde, dönüş değeri olmayan bir sunucu yönteminin nasıl çağrılacağını ve dönüş değerine sahip bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="a3532-304">**HubMethodName özniteliği olmayan sunucu yöntemi**</span><span class="sxs-lookup"><span data-stu-id="a3532-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="a3532-305">**Bir parametreye geçirilen karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="a3532-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="a3532-306">**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="a3532-307">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="a3532-308">Hub yöntemini bir `HubMethodName` özniteliğiyle Süsleriniz durumunda bu adı, büyük/küçük harf olmadan kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3532-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="a3532-309">HubMethodName özniteliğiyle **sunucu yöntemi**</span><span class="sxs-lookup"><span data-stu-id="a3532-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="a3532-310">**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="a3532-311">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="a3532-312">Yukarıdaki örneklerde, dönüş değeri olmayan bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="a3532-313">Aşağıdaki örneklerde, dönüş değeri olan bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3532-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="a3532-314">**Dönüş değerine sahip bir yöntem için sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="a3532-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="a3532-315">Dönüş değeri **için kullanılan hisse senedi sınıfı**</span><span class="sxs-lookup"><span data-stu-id="a3532-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="a3532-316">**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="a3532-317">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="a3532-318">Bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="a3532-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="a3532-319">SignalR, işleyebilmeniz için aşağıdaki bağlantı ömrü olaylarını sağlar:</span><span class="sxs-lookup"><span data-stu-id="a3532-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="a3532-320">`starting`: bağlantı üzerinden herhangi bir veri gönderilmeden önce tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a3532-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="a3532-321">`received`: bağlantıda herhangi bir veri alındığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a3532-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="a3532-322">Alınan verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3532-322">Provides the received data.</span></span>
- <span data-ttu-id="a3532-323">`connectionSlow`: istemci yavaş veya sık bir bırakma bağlantısı algıladığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a3532-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="a3532-324">`reconnecting`: temeldeki aktarım yeniden bağlanmaya başladığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a3532-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="a3532-325">`reconnected`: temeldeki aktarım yeniden bağlandığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a3532-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="a3532-326">`stateChanged`: bağlantı durumu değiştiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a3532-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="a3532-327">Eski durumu ve yeni durumu (bağlanma, bağlanma, yeniden bağlanma veya bağlantısı kesildi) sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3532-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="a3532-328">`disconnected`: bağlantının bağlantısı kesildiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a3532-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="a3532-329">Örneğin, dikkat çekici gecikmelere neden olabilecek bağlantı sorunları olduğunda uyarı iletilerini göstermek istiyorsanız `connectionSlow` olayını işleyin.</span><span class="sxs-lookup"><span data-stu-id="a3532-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="a3532-330">**Connectionlow olayını işle (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="a3532-331">**Connectionlow olayını işle (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="a3532-332">Daha fazla bilgi için bkz. [SignalR 'de bağlantı ömrü olaylarını anlama ve işleme](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="a3532-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="a3532-333">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="a3532-333">How to handle errors</span></span>

<span data-ttu-id="a3532-334">SignalR JavaScript istemcisi, için bir işleyici ekleyebileceğiniz bir `error` olayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3532-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="a3532-335">Ayrıca, bir sunucu yöntemi çağrısından kaynaklanan hatalara yönelik bir işleyici eklemek için Fail metodunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3532-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="a3532-336">Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, bir hatadan sonra SignalR 'nin döndürdüğü özel durum nesnesi hata hakkında en az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a3532-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="a3532-337">Örneğin, `newContosoChatMessage` çağrısı başarısız olursa, hata nesnesindeki hata iletisi, güvenlik nedenleriyle, üretim aşamasındaki istemcilere ayrıntılı hata iletileri gönderilmesi "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" içerir, ancak sorun giderme amacıyla ayrıntılı hata iletileri etkinleştirmek istiyorsanız, sunucuda aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3532-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="a3532-338">Aşağıdaki örnek, hata olayı için nasıl işleyicinin ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a3532-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="a3532-339">**Hata işleyicisi ekleme (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="a3532-340">**Hata işleyicisi ekleme (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="a3532-341">Aşağıdaki örnek, bir yöntem çağrısından bir hatanın nasıl işleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a3532-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="a3532-342">**Yöntem çağrısından bir hata işleme (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="a3532-343">**Yöntem çağrısından bir hata işleme (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="a3532-344">Bir yöntem çağrısı başarısız olursa, `error` olayı da oluşturulur, bu nedenle `error` yöntemi işleyicisindeki kodunuz ve `.fail` Yöntem geri çağırması yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a3532-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="a3532-345">İstemci tarafı günlük kaydını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a3532-345">How to enable client-side logging</span></span>

<span data-ttu-id="a3532-346">Bir bağlantıda istemci tarafı günlüğe kaydetmeyi etkinleştirmek için, bağlantıyı kurmak üzere `start` yöntemini çağırmadan önce bağlantı nesnesindeki `logging` özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a3532-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="a3532-347">**Günlüğe kaydetmeyi etkinleştirme (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="a3532-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="a3532-348">**Günlüğe kaydetmeyi etkinleştir (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="a3532-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="a3532-349">Günlükleri görmek için tarayıcınızın geliştirici araçlarını açın ve konsol sekmesine gidin. Bunun nasıl yapılacağını gösteren adım adım yönergeleri ve ekran görüntülerini gösteren bir öğretici için, bkz. [ASP.NET SignalR Ile sunucu yayını-günlüğü etkinleştirme](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span><span class="sxs-lookup"><span data-stu-id="a3532-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
