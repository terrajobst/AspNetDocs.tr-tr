---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: SignalR Izlemeyi etkinleştirme | Microsoft Docs
author: bradygaster
description: Bu belgede, SignalR sunucuları ve istemcileri için izlemenin nasıl etkinleştirileceği ve yapılandırılacağı açıklanmaktadır. İzleme, olaylar hakkında tanılama bilgilerini görüntülemenize olanak sağlar...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578836"
---
# <a name="enabling-signalr-tracing"></a><span data-ttu-id="f2010-104">SignalR İzlemeyi Etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f2010-104">Enabling SignalR Tracing</span></span>

<span data-ttu-id="f2010-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="f2010-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="f2010-106">Bu belgede, SignalR sunucuları ve istemcileri için izlemenin nasıl etkinleştirileceği ve yapılandırılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f2010-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="f2010-107">İzleme, SignalR uygulamanızda olaylarla ilgili tanılama bilgilerini görüntülemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f2010-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
>
> <span data-ttu-id="f2010-108">Bu konu, ilk başta Patrick Fleti tarafından yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="f2010-108">This topic was originally written by Patrick Fletcher.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f2010-109">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="f2010-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="f2010-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f2010-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="f2010-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="f2010-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="f2010-112">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="f2010-112">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="f2010-113">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="f2010-113">Questions and comments</span></span>
>
> <span data-ttu-id="f2010-114">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="f2010-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="f2010-115">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2010-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="f2010-116">İzleme etkinleştirildiğinde, bir SignalR uygulaması olaylar için günlük girişleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f2010-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="f2010-117">Olayları hem istemciden hem de sunucudan günlüğe kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2010-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="f2010-118">Sunucu günlüğü bağlantısı, genişleme sağlayıcısı ve ileti veri yolu olaylarını izleme.</span><span class="sxs-lookup"><span data-stu-id="f2010-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="f2010-119">İstemci üzerindeki izleme, bağlantı olaylarını günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f2010-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="f2010-120">SignalR 2,1 ve üzeri sürümlerde, istemci üzerindeki izleme, hub çağırma iletilerinin tam içeriğini günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f2010-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="f2010-121">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="f2010-121">Contents</span></span>

- [<span data-ttu-id="f2010-122">Sunucuda izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f2010-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="f2010-123">Sunucu olaylarını metin dosyalarına kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="f2010-124">Sunucu olaylarını olay günlüğüne kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="f2010-125">.NET istemcisinde izlemeyi etkinleştirme (Windows Masaüstü uygulamaları)</span><span class="sxs-lookup"><span data-stu-id="f2010-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="f2010-126">Masaüstü istemci olaylarını konsola kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="f2010-127">Masaüstü istemci olaylarını bir metin dosyasına kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="f2010-128">Windows Phone 8 istemcilerde izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f2010-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="f2010-129">İstemci olaylarını Windows Phone Kullanıcı arabirimine kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="f2010-130">İstemci olaylarını Windows Phone hata ayıklama konsoluna kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="f2010-131">JavaScript istemcisinde izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f2010-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="f2010-132">Sunucuda izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f2010-132">Enabling tracing on the server</span></span>

<span data-ttu-id="f2010-133">Uygulamanın yapılandırma dosyası (proje türüne bağlı olarak App. config veya Web. config) içindeki sunucuda izlemeyi etkinleştirirsiniz. Hangi olay kategorilerini günlüğe kaydetmek istediğinizi belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2010-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="f2010-134">Yapılandırma dosyasında, olayları bir metin dosyasına, Windows olay günlüğüne veya [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)uygulamasını kullanarak özel bir günlüğe günlüğe kaydetmek isteyip istemediğinizi de belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2010-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="f2010-135">Sunucu olay kategorileri aşağıdaki ileti türlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="f2010-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="f2010-136">Kaynak</span><span class="sxs-lookup"><span data-stu-id="f2010-136">Source</span></span> | <span data-ttu-id="f2010-137">İletiler</span><span class="sxs-lookup"><span data-stu-id="f2010-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="f2010-138">SignalR. SqlMessageBus</span><span class="sxs-lookup"><span data-stu-id="f2010-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="f2010-139">SQL Ileti veri yolu genişleme sağlayıcısı kurulumu, veritabanı işlemi, hata ve zaman aşımı olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="f2010-140">SignalR. ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="f2010-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="f2010-141">Service Bus genişleme sağlayıcısı konu oluşturma ve abonelik, hata ve mesajlaşma olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="f2010-142">SignalR. RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="f2010-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="f2010-143">Redsıs genişleme sağlayıcı bağlantısı, bağlantı kesilmesi ve hata olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="f2010-144">SignalR. ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="f2010-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="f2010-145">Genişleme mesajlaşma olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="f2010-146">SignalR. taşımalar. WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="f2010-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="f2010-147">WebSocket aktarım bağlantısı, bağlantı kesilmesi, mesajlaşma ve hata olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="f2010-148">SignalR. taşımalar. ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="f2010-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="f2010-149">ServerSentEvents aktarım bağlantısı, bağlantı kesme, mesajlaşma ve hata olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="f2010-150">SignalR. taşımalar. ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="f2010-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="f2010-151">ForeverFrame aktarım bağlantısı, bağlantı kesilmesi, mesajlaşma ve hata olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="f2010-152">SignalR.Transports.LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="f2010-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="f2010-153">Uzun Gplipop aktarım bağlantısı, bağlantı kesilmesi, mesajlaşma ve hata olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="f2010-154">SignalR. taşımalar. TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="f2010-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="f2010-155">Aktarım bağlantısı, bağlantı kesilmesi ve KeepAlive olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="f2010-156">SignalR. ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="f2010-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="f2010-157">Merkez bulma olayları</span><span class="sxs-lookup"><span data-stu-id="f2010-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="f2010-158">Sunucu olaylarını metin dosyalarına kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-158">Logging server events to text files</span></span>

<span data-ttu-id="f2010-159">Aşağıdaki kod, her olay kategorisi için izlemenin nasıl etkinleştirileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f2010-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="f2010-160">Bu örnek, uygulamayı metin dosyalarına olayları günlüğe kaydetmek üzere yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f2010-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="f2010-161">**İzlemeyi etkinleştirmek için XML sunucusu kodu**</span><span class="sxs-lookup"><span data-stu-id="f2010-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="f2010-162">Yukarıdaki kodda `SignalRSwitch` girdisi, belirtilen günlüğe gönderilen olaylar için [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) kullanılan öğesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2010-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="f2010-163">Bu durumda, tüm hata ayıklama ve izleme iletilerinin kaydedildiği `Verbose` olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f2010-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="f2010-164">Aşağıdaki çıktıda, yukarıdaki yapılandırma dosyası kullanılarak bir uygulama için `transports.log.txt` dosyasındaki girişler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f2010-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="f2010-165">Yeni bir bağlantı, kaldırılan bir bağlantı ve aktarım sinyali olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="f2010-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="f2010-166">Sunucu olaylarını olay günlüğüne kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-166">Logging server events to the event log</span></span>

<span data-ttu-id="f2010-167">Olayları bir metin dosyası yerine olay günlüğüne kaydetmek için `sharedListeners` düğümündeki girişlerin değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f2010-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="f2010-168">Aşağıdaki kod, sunucu olaylarının olay günlüğüne nasıl günlüğe alınacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="f2010-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="f2010-169">**Olay günlüğüne olayları günlüğe kaydetmek için XML sunucusu kodu**</span><span class="sxs-lookup"><span data-stu-id="f2010-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="f2010-170">Olaylar uygulama günlüğüne kaydedilir ve aşağıda gösterildiği gibi Olay Görüntüleyicisi aracılığıyla kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="f2010-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![SignalR günlüklerini gösteren Olay Görüntüleyicisi](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="f2010-172">Olay günlüğünü kullanırken, bulunan ileti sayısını korumak için **TraceLevel** . **Error** ' u ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2010-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="f2010-173">.NET istemcisinde izlemeyi etkinleştirme (Windows Masaüstü uygulamaları)</span><span class="sxs-lookup"><span data-stu-id="f2010-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="f2010-174">.NET istemcisi, bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)uygulamasını kullanarak olayları konsola, bir metin dosyasına veya özel bir günlüğe kaydedebilir.</span><span class="sxs-lookup"><span data-stu-id="f2010-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="f2010-175">.NET istemcisinde günlüğe kaydetmeyi etkinleştirmek için, bağlantının `TraceLevel` özelliğini bir [Tracelevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) değerine ve `TraceWriter` özelliğini geçerli bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) örneğine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2010-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="f2010-176">Masaüstü istemci olaylarını konsola kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="f2010-177">Aşağıdaki C# kod, .net istemcisindeki olaylarının konsola nasıl günlüğe alınacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="f2010-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="f2010-178">Masaüstü istemci olaylarını bir metin dosyasına kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="f2010-179">Aşağıdaki C# kod, .net istemcisindeki olayların bir metin dosyasına nasıl günlüğe alınacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="f2010-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="f2010-180">Aşağıdaki çıktıda, yukarıdaki yapılandırma dosyası kullanılarak bir uygulama için `ClientLog.txt` dosyasındaki girişler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f2010-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="f2010-181">Sunucuya bağlanan istemciyi ve `addMessage`adlı bir istemci yöntemini çağıran hub 'ı gösterir:</span><span class="sxs-lookup"><span data-stu-id="f2010-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="f2010-182">Windows Phone 8 istemcilerde izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f2010-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="f2010-183">Windows Phone uygulamalar için SignalR uygulamaları, masaüstü uygulamaları ile aynı .NET istemcisini kullanır, ancak [Console. out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) ve [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) ile bir dosyaya yazma kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f2010-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="f2010-184">Bunun yerine, izleme için özel bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) uygulamasının oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2010-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span>

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="f2010-185">İstemci olaylarını Windows Phone Kullanıcı arabirimine kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="f2010-186">[SignalR kod temeli](https://github.com/SignalR/SignalR/archive/master.zip) , `TextBlockWriter`adlı özel bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) uygulamasını kullanarak, izleme çıkışını bir [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) öğesine yazan Windows Phone bir örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="f2010-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="f2010-187">Bu sınıf, **Samples/Microsoft. Aspnet. SignalR. Client. WP8. Samples** projesinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="f2010-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="f2010-188">Bir `TextBlockWriter`örneği oluştururken geçerli [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)içinde geçirin ve izleme çıktısı için kullanılacak bir [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) oluşturacak bir [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f2010-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="f2010-189">Daha sonra, izleme çıktısı, geçirilen [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) içinde oluşturulan yeni bir [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) öğesine yazılır:</span><span class="sxs-lookup"><span data-stu-id="f2010-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="f2010-190">İstemci olaylarını Windows Phone hata ayıklama konsoluna kaydetme</span><span class="sxs-lookup"><span data-stu-id="f2010-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="f2010-191">Kullanıcı arabirimi yerine hata ayıklama konsoluna çıkış göndermek için, hata ayıklama penceresine yazan bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) uygulamasını oluşturun ve bunu bağlantınızın [tracewriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) özelliğine atayın:</span><span class="sxs-lookup"><span data-stu-id="f2010-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="f2010-192">İzleme bilgileri, Visual Studio 'daki hata ayıklama penceresine yazılır:</span><span class="sxs-lookup"><span data-stu-id="f2010-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="f2010-193">JavaScript istemcisinde izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f2010-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="f2010-194">Bir bağlantıda istemci tarafı günlüğe kaydetmeyi etkinleştirmek için, bağlantıyı kurmak üzere `start` yöntemini çağırmadan önce bağlantı nesnesindeki `logging` özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2010-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="f2010-195">**Tarayıcı konsolunda izlemeyi etkinleştirmeye yönelik istemci JavaScript kodu (oluşturulan ara sunucu ile)**</span><span class="sxs-lookup"><span data-stu-id="f2010-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="f2010-196">**Tarayıcı konsolunda izlemeyi etkinleştirmeye yönelik istemci JavaScript kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="f2010-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="f2010-197">İzleme etkinleştirildiğinde, JavaScript istemcisi olayları tarayıcı konsoluna kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f2010-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="f2010-198">Tarayıcı konsoluna erişmek için bkz. [aktarımları izleme](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span><span class="sxs-lookup"><span data-stu-id="f2010-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="f2010-199">Aşağıdaki ekran görüntüsünde, izlemenin etkinleştirildiği bir SignalR JavaScript istemcisi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f2010-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="f2010-200">Tarayıcı konsolundaki bağlantı ve hub çağırma olaylarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="f2010-200">It shows connection and hub invocation events in the browser console:</span></span>

![Tarayıcı konsolundaki SignalR izleme olayları](enabling-signalr-tracing/_static/image4.png)
