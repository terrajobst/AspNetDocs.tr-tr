---
uid: signalr/overview/performance/signalr-performance
title: SignalR performansı | Microsoft Docs
author: bradygaster
description: SignalR Performansı
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558326"
---
# <a name="signalr-performance"></a><span data-ttu-id="cf59c-103">SignalR Performansı</span><span class="sxs-lookup"><span data-stu-id="cf59c-103">SignalR Performance</span></span>

<span data-ttu-id="cf59c-104">, [Patrick Fleti](https://github.com/pfletcher) tarafından</span><span class="sxs-lookup"><span data-stu-id="cf59c-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="cf59c-105">Bu konu, bir SignalR uygulamasındaki performansı nasıl tasarlayacağınızı, ölçecek ve artırabileceğinizi açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="cf59c-106">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="cf59c-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="cf59c-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="cf59c-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="cf59c-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="cf59c-108">.NET 4.5</span></span>
> - <span data-ttu-id="cf59c-109">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="cf59c-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="cf59c-110">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="cf59c-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="cf59c-111">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="cf59c-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="cf59c-112">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="cf59c-112">Questions and comments</span></span>
>
> <span data-ttu-id="cf59c-113">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="cf59c-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="cf59c-114">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf59c-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="cf59c-115">SignalR performansı ve ölçeklendirmeyle ilgili son bir sunum için bkz. [ASP.NET SignalR Ile gerçek zamanlı web 'ı ölçeklendirme](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="cf59c-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="cf59c-116">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="cf59c-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="cf59c-117">Tasarım konusunda dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="cf59c-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="cf59c-118">SignalR sunucunuzu performans için ayarlama</span><span class="sxs-lookup"><span data-stu-id="cf59c-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="cf59c-119">Performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="cf59c-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="cf59c-120">SignalR performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="cf59c-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="cf59c-121">Diğer performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="cf59c-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="cf59c-122">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cf59c-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="cf59c-123">Tasarım konusunda dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="cf59c-123">Design considerations</span></span>

<span data-ttu-id="cf59c-124">Bu bölüm, bir SignalR uygulamasının tasarımı sırasında uygulanabilecek desenleri açıklar. Bu, performansın gereksiz ağ trafiği oluşturarak dengelenmemiş olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf59c-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="cf59c-125">Daraltma iletisi sıklığı</span><span class="sxs-lookup"><span data-stu-id="cf59c-125">Throttling message frequency</span></span>

<span data-ttu-id="cf59c-126">Büyük bir sıklıkta (gerçek zamanlı bir oyun uygulaması gibi) ileti gönderen bir uygulamada bile, çoğu uygulamanın bir saniyede birkaç ileti göndermesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cf59c-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="cf59c-127">Her bir istemcinin ürettiği trafik miktarını azaltmak için, kuyruklar ve iletileri sabit bir orandan daha sık teslim etmek üzere bir ileti döngüsü uygulanabilir (Bu süre içinde iletiler varsa, belirli bir sayıda iletiye kadar her saniye gönderilir. gönderilecek terval).</span><span class="sxs-lookup"><span data-stu-id="cf59c-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="cf59c-128">İletileri belirli bir hıza (hem istemciden hem de sunucudan) uygulayan örnek bir uygulama için bkz. [SignalR Ile yüksek frekanslı gerçek zamanlı](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="cf59c-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="cf59c-129">İleti boyutunu küçültme</span><span class="sxs-lookup"><span data-stu-id="cf59c-129">Reducing message size</span></span>

<span data-ttu-id="cf59c-130">Seri hale getirilmiş nesnelerinizin boyutunu azaltarak bir SignalR iletisinin boyutunu azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf59c-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="cf59c-131">Sunucu kodunda, aktarılmaları gerekmeyen özellikleri içeren bir nesne gönderiyorsanız, bu özelliklerin `JsonIgnore` özniteliği kullanılarak serileştirilmesine engel olun.</span><span class="sxs-lookup"><span data-stu-id="cf59c-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="cf59c-132">Özelliklerin adları da iletide depolanır; özelliklerinin adları `JsonProperty` özniteliği kullanılarak kısaltılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="cf59c-133">Aşağıdaki kod örneği, bir özelliğin istemciye gönderilme şeklini ve özellik adlarının nasıl kısaltılanmasını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="cf59c-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="cf59c-134">**Verilerin istemciye gönderilmesini hariç tutmak için Jsonıgnore özniteliğini ve ileti boyutunu azaltmak için JsonProperty özniteliğini gösteren .NET Server kodu**</span><span class="sxs-lookup"><span data-stu-id="cf59c-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="cf59c-135">İstemci kodunda okunabilirlik/bakım korumasını sürdürmek için, kısaltılmış Özellik adları, ileti alındıktan sonra insanla kolay adlarla yeniden eşlenir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="cf59c-136">Aşağıdaki kod örneğinde, kısaltılmış adları daha uzun bir süre yeniden eşleştirmenin, bir ileti sözleşmesi tanımlayarak (eşleme) ve sözleşmeyi iyileştirilmiş ileti sınıfına uygulamak için `reMap` işlevini kullanarak bir olası yol gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="cf59c-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="cf59c-137">**Kısaltılmış özellik adlarını insan tarafından okunabilen adlara yeniden eşleyen istemci tarafı JavaScript kodu**</span><span class="sxs-lookup"><span data-stu-id="cf59c-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="cf59c-138">Adlar istemciden sunucuya, aynı yöntemi kullanarak da kısaltılarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="cf59c-139">İleti nesnesinin bellek parmak izini (ileti için kullanılan bellek miktarı) azaltmada ayrıca performans de iyileştirebilirler.</span><span class="sxs-lookup"><span data-stu-id="cf59c-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="cf59c-140">Örneğin, bir `int` tam aralığı gerekmiyorsa bunun yerine bir `short` veya `byte` kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="cf59c-141">İletiler, sunucu belleğindeki ileti veri yolunda depolandığından, ileti boyutunu azaltmak sunucu belleği sorunlarını da ele alabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="cf59c-142">SignalR sunucunuzu performans için ayarlama</span><span class="sxs-lookup"><span data-stu-id="cf59c-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="cf59c-143">Aşağıdaki yapılandırma ayarları, sunucunuzu bir SignalR uygulamasında daha iyi performans için ayarlamak üzere kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="cf59c-144">ASP.NET uygulamasında performansı geliştirme hakkında genel bilgi için bkz. [ASP.net performansını geliştirme](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf59c-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="cf59c-145">**SignalR yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="cf59c-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="cf59c-146">**Defaultmessagebuffersize**: SignalR, bağlantı başına her hub 'da 1000 ileti tutar.</span><span class="sxs-lookup"><span data-stu-id="cf59c-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="cf59c-147">Büyük iletiler kullanılıyorsa, bu değer azaltılarak alleviated olabilen bellek sorunları oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="cf59c-148">Bu ayar bir ASP.NET uygulamasındaki `Application_Start` olay işleyicisine veya şirket içinde barındırılan bir uygulamadaki OWıN başlangıç sınıfının `Configuration` yöntemine ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="cf59c-149">Aşağıdaki örnek, kullanılan sunucu belleği miktarını azaltmak için uygulamanızın bellek parmak izini azaltmak üzere bu değerin nasıl azaltılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="cf59c-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="cf59c-150">**Varsayılan ileti arabelleği boyutunu azaltmak için Startup.cs içindeki .NET Server kodu**</span><span class="sxs-lookup"><span data-stu-id="cf59c-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="cf59c-151">**IIS yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="cf59c-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="cf59c-152">**Uygulama başına en fazla eşzamanlı istek**sayısı: eşzamanlı IIS isteklerinin sayısını artırmak, istek sunmak için kullanılabilir sunucu kaynaklarını arttırır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="cf59c-153">Varsayılan değer 5000 ' dir; Bu ayarı artırmak için, yükseltilmiş bir komut isteminde aşağıdaki komutları yürütün:</span><span class="sxs-lookup"><span data-stu-id="cf59c-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="cf59c-154">**ApplicationPool QueueLength**: Bu, uygulama havuzu için http. sys kuyruklarının en fazla istek sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="cf59c-155">Sıra dolduğunda, yeni istekler 503 "hizmet kullanılamıyor" yanıtını alır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="cf59c-156">Varsayılan değer 1000'dir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-156">The default value is 1000.</span></span>

    <span data-ttu-id="cf59c-157">Uygulamanızı barındıran uygulama havuzundaki çalışan işlemin sıra uzunluğu kısaltaştırın, bellek kaynaklarını tasarrufu sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="cf59c-158">Daha fazla bilgi için bkz. [uygulama havuzlarını yönetme, ayarlama ve yapılandırma](https://technet.microsoft.com/library/cc745955.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf59c-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="cf59c-159">**ASP.NET yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="cf59c-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="cf59c-160">Bu bölüm `aspnet.config` dosyasında ayarlankullanılabilecek yapılandırma ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="cf59c-161">Bu dosya, platforma bağlı olarak iki konumdan birinde bulunur:</span><span class="sxs-lookup"><span data-stu-id="cf59c-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="cf59c-162">ASP.NET, SignalR performansını iyileştirebilecek ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cf59c-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="cf59c-163">**CPU başına en fazla eşzamanlı istek sayısı**: Bu ayarın artırılması, performans sorunlarını hafifedebilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="cf59c-164">Bu ayarı artırmak için aşağıdaki yapılandırma ayarını `aspnet.config` dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cf59c-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="cf59c-165">**Istek sırası sınırı**: Toplam bağlantı sayısı `maxConcurrentRequestsPerCPU` ayarını aşarsa, ASP.net bir kuyruğu kullanarak istekleri azaltmayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="cf59c-166">Kuyruğun boyutunu artırmak için `requestQueueLimit` ayarını artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf59c-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="cf59c-167">Bunu yapmak için, aşağıdaki yapılandırma ayarını `config/machine.config` `processModel` düğümüne ekleyin (`aspnet.config`yerine):</span><span class="sxs-lookup"><span data-stu-id="cf59c-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="cf59c-168">Performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="cf59c-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="cf59c-169">Bu bölümde, uygulamanızda performans sorunlarını bulmanın yolları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="cf59c-170">WebSocket 'in kullanılmakta olduğu doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="cf59c-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="cf59c-171">SignalR, istemci ve sunucu arasındaki iletişim için çeşitli aktarımlar kullanabilir, ancak WebSocket önemli bir performans avantajı sunar ve istemci ve sunucu bunu destekliyorsa kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="cf59c-172">İstemci ve sunucunuzun WebSocket gereksinimlerini karşılayıp karşılamadığını öğrenmek için bkz. [aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="cf59c-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="cf59c-173">Uygulamanızda hangi taşımanın kullanıldığını belirlemek için tarayıcı geliştirici araçlarını kullanabilir ve bağlantı için hangi taşımanın kullanıldığını görmek üzere günlükleri inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf59c-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="cf59c-174">Internet Explorer ve Chrome 'daki tarayıcı geliştirme araçlarını kullanma hakkında daha fazla bilgi için bkz. [aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="cf59c-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="cf59c-175">SignalR performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="cf59c-175">Using SignalR performance counters</span></span>

<span data-ttu-id="cf59c-176">Bu bölümde, `Microsoft.AspNet.SignalR.Utils` paketinde bulunan SignalR performans sayaçlarının nasıl etkinleştirileceği ve kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="cf59c-177">SignalR. exe yükleniyor</span><span class="sxs-lookup"><span data-stu-id="cf59c-177">Installing signalr.exe</span></span>

<span data-ttu-id="cf59c-178">Performans sayaçları, SignalR. exe adlı bir yardımcı program kullanılarak sunucuya eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="cf59c-179">Bu yardımcı programı yüklemek için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="cf59c-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="cf59c-180">Visual Studio 'da **araçlar** > **nuget Paket Yöneticisi** > **çözüm için NuGet Paketlerini Yönet** ' i seçin</span><span class="sxs-lookup"><span data-stu-id="cf59c-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="cf59c-181">**SignalR. utils**araması yapın ve yüklemeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="cf59c-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="cf59c-182">Paketi yüklemek için lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="cf59c-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="cf59c-183">SignalR. exe, `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="cf59c-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="cf59c-184">SignalR. exe ile performans sayaçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="cf59c-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="cf59c-185">SignalR performans sayaçlarını yüklemek için aşağıdaki parametreyle bir yükseltilmiş komut isteminde SignalR. exe ' yi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cf59c-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="cf59c-186">SignalR performans sayaçlarını kaldırmak için, aşağıdaki parametreyle bir yükseltilmiş komut isteminde SignalR. exe ' yi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cf59c-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="cf59c-187">SignalR performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="cf59c-187">SignalR Performance counters</span></span>

<span data-ttu-id="cf59c-188">Yardımcı programlar paketi aşağıdaki performans sayaçlarını yükleme.</span><span class="sxs-lookup"><span data-stu-id="cf59c-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="cf59c-189">"Toplam" sayacı, son uygulama havuzunun veya sunucu yeniden başlatılmasından bu yana olayların sayısını ölçer.</span><span class="sxs-lookup"><span data-stu-id="cf59c-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="cf59c-190">**Bağlantı ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="cf59c-190">**Connection metrics**</span></span>

<span data-ttu-id="cf59c-191">Aşağıdaki ölçümler, gerçekleşen bağlantı ömrü olaylarını ölçer.</span><span class="sxs-lookup"><span data-stu-id="cf59c-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="cf59c-192">Daha fazla bilgi için bkz. [bağlantı ömrü olaylarını anlama ve işleme](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="cf59c-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="cf59c-193">**Bağlı bağlantılar**</span><span class="sxs-lookup"><span data-stu-id="cf59c-193">**Connections Connected**</span></span>
- <span data-ttu-id="cf59c-194">**Bağlantılar yeniden bağlandı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="cf59c-195">**Bağlantı kesilen bağlantılar**</span><span class="sxs-lookup"><span data-stu-id="cf59c-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="cf59c-196">**Geçerli bağlantı sayısı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-196">**Connections Current**</span></span>

<span data-ttu-id="cf59c-197">**İleti ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="cf59c-197">**Message metrics**</span></span>

<span data-ttu-id="cf59c-198">Aşağıdaki ölçümler, SignalR tarafından oluşturulan ileti trafiğini ölçer.</span><span class="sxs-lookup"><span data-stu-id="cf59c-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="cf59c-199">**Alınan bağlantı Iletileri toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="cf59c-200">**Gönderilen bağlantı Iletileri toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="cf59c-201">**Alınan bağlantı Iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="cf59c-202">**Gönderilen bağlantı Iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="cf59c-203">**İleti veri yolu ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="cf59c-203">**Message bus metrics**</span></span>

<span data-ttu-id="cf59c-204">Aşağıdaki ölçümler, gelen ve giden SignalR iletilerinin yerleştirildiği sıra, iç SignalR ileti veri yolu üzerinden trafiği ölçer.</span><span class="sxs-lookup"><span data-stu-id="cf59c-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="cf59c-205">İleti gönderildiğinde veya **yayımlandığında yayınlanır** .</span><span class="sxs-lookup"><span data-stu-id="cf59c-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="cf59c-206">Bu bağlamdaki bir **abone** , ileti veri yolundaki bir aboneliğiniz; Bu, istemci sayısına ve sunucunun kendine eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="cf59c-207">**Ayrılmış çalışan** , etkin bağlantılara veri gönderen bir bileşendir; Meşgul bir çalışan, etkin bir şekilde ileti gönderen bir **çalışandır** .</span><span class="sxs-lookup"><span data-stu-id="cf59c-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="cf59c-208">**Alınan ileti veri yolu Iletileri toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="cf59c-209">**Alınan ileti veri yolu iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="cf59c-210">**İleti veri yolu Iletileri yayımlandı toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="cf59c-211">**Yayınlanan ileti veri yolu iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="cf59c-212">**İleti veri yolu aboneleri geçerli**</span><span class="sxs-lookup"><span data-stu-id="cf59c-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="cf59c-213">**İleti veri yolu aboneleri toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="cf59c-214">**İleti veri yolu aboneleri/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="cf59c-215">**İleti veri yolu ayrılmış çalışanları**</span><span class="sxs-lookup"><span data-stu-id="cf59c-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="cf59c-216">**İleti veri yolu meşgul çalışanları**</span><span class="sxs-lookup"><span data-stu-id="cf59c-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="cf59c-217">**İleti veri yolu konuları geçerli**</span><span class="sxs-lookup"><span data-stu-id="cf59c-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="cf59c-218">**Hata ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="cf59c-218">**Error metrics**</span></span>

<span data-ttu-id="cf59c-219">Aşağıdaki ölçümler, SignalR ileti trafiği tarafından oluşturulan hataları ölçer.</span><span class="sxs-lookup"><span data-stu-id="cf59c-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="cf59c-220">Hub veya hub yöntemi çözümlenemiyorsa **Merkez çözümleme** hataları oluşur.</span><span class="sxs-lookup"><span data-stu-id="cf59c-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="cf59c-221">Hub **çağrısı** hataları, bir hub yöntemi çağrılırken oluşturulan özel durumlardır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="cf59c-222">**Aktarım** hataları, bir http isteği veya yanıtı sırasında oluşturulan bağlantı hatalardır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="cf59c-223">**Hatalar: tüm toplam**</span><span class="sxs-lookup"><span data-stu-id="cf59c-223">**Errors: All Total**</span></span>
- <span data-ttu-id="cf59c-224">**Hatalar: tümü/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="cf59c-225">**Hatalar: Merkez çözümleme toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="cf59c-226">**Hatalar: hub çözümleme/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="cf59c-227">**Hatalar: hub çağrısı toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="cf59c-228">**Hatalar: hub çağrı/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="cf59c-229">**Hatalar: aktarım toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="cf59c-230">**Hatalar: aktarım/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="cf59c-231">**Genişleme ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="cf59c-231">**Scaleout metrics**</span></span>

<span data-ttu-id="cf59c-232">Aşağıdaki ölçümler, genişleme sağlayıcısı tarafından oluşturulan trafiği ve hataları ölçer.</span><span class="sxs-lookup"><span data-stu-id="cf59c-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="cf59c-233">Bu bağlamdaki bir **akış** , genişleme sağlayıcısı tarafından kullanılan bir ölçek birimidir; SQL Server kullanılırsa bu bir tablodur, Service Bus kullanılıyorsa bir konu ve redin kullanılıyorsa bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="cf59c-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="cf59c-234">Her akış, sıralı okuma ve yazma işlemlerini sağlar; tek bir akış olası bir ölçeklendirme tıkanıkıdır, bu nedenle bu performans sorununu azaltmaya yardımcı olmak için akış sayısı artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="cf59c-235">Birden çok akış kullanılıyorsa, SignalR, belirli bir bağlantıdan gönderilen iletilerin sırada olmasını sağlamak üzere bu akışlarda iletileri otomatik olarak dağıtır (parça).</span><span class="sxs-lookup"><span data-stu-id="cf59c-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="cf59c-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) ayarı, SignalR tarafından tutulan genişleme gönderme sırasının uzunluğunu denetler.</span><span class="sxs-lookup"><span data-stu-id="cf59c-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="cf59c-237">Bu değeri 0 ' dan büyük bir değere ayarlamak, bir gönderme sırasındaki tüm iletilerin aynı anda yapılandırılmış mesajlaşma biriktirme düzlemine gönderilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf59c-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="cf59c-238">Kuyruğun boyutu yapılandırılan uzunluğun üzerine gittiğinde, sıradaki ileti sayısı tekrar ayarından daha az olana kadar sonraki Gönder çağrıları bir [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ile hemen başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cf59c-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="cf59c-239">Uygulanan arka düzlemler genellikle kendi sıraya alma veya akış denetimine sahip olduğundan sıraya alma varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="cf59c-240">SQL Server durumda, bağlantı havuzu her seferinde gönderilen gönderme sayısını etkin bir şekilde kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="cf59c-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="cf59c-241">Varsayılan olarak, SQL Server ve redin için yalnızca bir akış kullanılır, Service Bus için beş akış kullanılır ve sıraya alma devre dışıdır, ancak bu ayarlar SQL Server ve Service Bus yapılandırması aracılığıyla değiştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="cf59c-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="cf59c-242">**SQL Server backdüzlemi için tablo sayısını ve sıra uzunluğunu yapılandırmaya yönelik .NET sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="cf59c-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="cf59c-243">**Service Bus backdüzlemi için konu sayısını ve sıra uzunluğunu yapılandırmaya yönelik .NET sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="cf59c-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="cf59c-244">**Arabelleğe alma** akışı, hatalı bir duruma girmiş bir durumdur; akış hatalı durumdaysa, akış artık hatalı olana kadar geri düzleme gönderilen tüm iletiler hemen başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cf59c-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="cf59c-245">**Gönderme sırası uzunluğu** , gönderilen ancak henüz gönderilmemiş olan iletilerin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="cf59c-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="cf59c-246">**Alınan genişleme Ileti veri yolu Iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="cf59c-247">**Ölçek Genişletme akışı toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="cf59c-248">**Ölçek Genişletme akışları açık**</span><span class="sxs-lookup"><span data-stu-id="cf59c-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="cf59c-249">**Genişleme akışları arabelleğe alma**</span><span class="sxs-lookup"><span data-stu-id="cf59c-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="cf59c-250">**Ölçek Genişletme hataları toplamı**</span><span class="sxs-lookup"><span data-stu-id="cf59c-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="cf59c-251">**Genişleme hatası/sn**</span><span class="sxs-lookup"><span data-stu-id="cf59c-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="cf59c-252">**Genişleme gönderme sırası uzunluğu**</span><span class="sxs-lookup"><span data-stu-id="cf59c-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="cf59c-253">Bu sayaçların ölçüm hakkında daha fazla bilgi için bkz. [Azure Service Bus Ile SignalR ölçeği](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="cf59c-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="cf59c-254">Diğer performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="cf59c-254">Using other performance counters</span></span>

<span data-ttu-id="cf59c-255">Aşağıdaki performans sayaçları, uygulamanızın performansını izlemek için de yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="cf59c-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="cf59c-256">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="cf59c-256">**Memory**</span></span>

- <span data-ttu-id="cf59c-257">.NET CLR bellek\\tüm yığınlardaki (W3wp için) # bayt</span><span class="sxs-lookup"><span data-stu-id="cf59c-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="cf59c-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="cf59c-258">**ASP.NET**</span></span>

- <span data-ttu-id="cf59c-259">ASP. NET\Requests geçerli</span><span class="sxs-lookup"><span data-stu-id="cf59c-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="cf59c-260">ASP. NET\Queued</span><span class="sxs-lookup"><span data-stu-id="cf59c-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="cf59c-261">ASP. NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="cf59c-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="cf59c-262">**'SUNA**</span><span class="sxs-lookup"><span data-stu-id="cf59c-262">**CPU**</span></span>

- <span data-ttu-id="cf59c-263">İşlemci Bilgileri\işlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="cf59c-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="cf59c-264">**TCP/ıP**</span><span class="sxs-lookup"><span data-stu-id="cf59c-264">**TCP/IP**</span></span>

- <span data-ttu-id="cf59c-265">TCPv6/bağlantı kurdu</span><span class="sxs-lookup"><span data-stu-id="cf59c-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="cf59c-266">TCPv4/bağlantı kurdu</span><span class="sxs-lookup"><span data-stu-id="cf59c-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="cf59c-267">**Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="cf59c-267">**Web Service**</span></span>

- <span data-ttu-id="cf59c-268">Web hizmeti \ geçerli bağlantılar</span><span class="sxs-lookup"><span data-stu-id="cf59c-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="cf59c-269">Web hizmeti \ en fazla bağlantı sayısı</span><span class="sxs-lookup"><span data-stu-id="cf59c-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="cf59c-270">**İş Parçacığı Oluşturma**</span><span class="sxs-lookup"><span data-stu-id="cf59c-270">**Threading**</span></span>

- <span data-ttu-id="cf59c-271">Geçerli mantıksal Iş parçacıklarının #\\.NET CLR kilitleri ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="cf59c-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="cf59c-272">Geçerli fiziksel Iş parçacığı\\.NET CLR kilitleri ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="cf59c-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="cf59c-273">Diğer Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cf59c-273">Other Resources</span></span>

<span data-ttu-id="cf59c-274">ASP.NET performans izleme ve ayarlama hakkında daha fazla bilgi için aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="cf59c-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="cf59c-275">[ASP.NET performansına genel bakış](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="cf59c-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="cf59c-276">ASP.NET Iş parçacığı kullanımı IIS 7,5, IIS 7,0 ve IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="cf59c-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="cf59c-277">&lt;applicationPool&gt; öğesi (Web ayarları)</span><span class="sxs-lookup"><span data-stu-id="cf59c-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
