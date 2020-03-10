---
uid: signalr/overview/older-versions/signalr-performance
title: SignalR performansı (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: SignalR Performansı
ms.author: bradyg
ms.date: 07/03/2013
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 915fd822caae9bbcb0a688c6dd7a5b2bda12c9df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579613"
---
# <a name="signalr-performance-signalr-1x"></a><span data-ttu-id="4d46c-103">SignalR Performansı (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="4d46c-103">SignalR Performance (SignalR 1.x)</span></span>

<span data-ttu-id="4d46c-104">, [Patrick Fleti](https://github.com/pfletcher) tarafından</span><span class="sxs-lookup"><span data-stu-id="4d46c-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4d46c-105">Bu konu, bir SignalR uygulamasındaki performansı nasıl tasarlayacağınızı, ölçecek ve artırabileceğinizi açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>

<span data-ttu-id="4d46c-106">SignalR performansı ve ölçeklendirmeyle ilgili son bir sunum için bkz. [ASP.NET SignalR Ile gerçek zamanlı web 'ı ölçeklendirme](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="4d46c-106">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="4d46c-107">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="4d46c-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="4d46c-108">Tasarım konusunda dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="4d46c-108">Design considerations</span></span>](#design)
- [<span data-ttu-id="4d46c-109">SignalR sunucunuzu performans için ayarlama</span><span class="sxs-lookup"><span data-stu-id="4d46c-109">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="4d46c-110">Performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="4d46c-110">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="4d46c-111">SignalR performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="4d46c-111">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="4d46c-112">Diğer performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="4d46c-112">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="4d46c-113">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4d46c-113">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="4d46c-114">Tasarım konusunda dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="4d46c-114">Design considerations</span></span>

<span data-ttu-id="4d46c-115">Bu bölüm, bir SignalR uygulamasının tasarımı sırasında uygulanabilecek desenleri açıklar. Bu, performansın gereksiz ağ trafiği oluşturarak dengelenmemiş olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d46c-115">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="4d46c-116">Daraltma iletisi sıklığı</span><span class="sxs-lookup"><span data-stu-id="4d46c-116">Throttling message frequency</span></span>

<span data-ttu-id="4d46c-117">Büyük bir sıklıkta (gerçek zamanlı bir oyun uygulaması gibi) ileti gönderen bir uygulamada bile, çoğu uygulamanın bir saniyede birkaç ileti göndermesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4d46c-117">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="4d46c-118">Her bir istemcinin ürettiği trafik miktarını azaltmak için, kuyruklar ve iletileri sabit bir orandan daha sık teslim etmek üzere bir ileti döngüsü uygulanabilir (Bu süre içinde iletiler varsa, belirli bir sayıda iletiye kadar her saniye gönderilir. gönderilecek terval).</span><span class="sxs-lookup"><span data-stu-id="4d46c-118">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="4d46c-119">İletileri belirli bir hıza (hem istemciden hem de sunucudan) uygulayan örnek bir uygulama için bkz. [SignalR Ile yüksek frekanslı gerçek zamanlı](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="4d46c-119">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="4d46c-120">İleti boyutunu küçültme</span><span class="sxs-lookup"><span data-stu-id="4d46c-120">Reducing message size</span></span>

<span data-ttu-id="4d46c-121">Seri hale getirilmiş nesnelerinizin boyutunu azaltarak bir SignalR iletisinin boyutunu azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d46c-121">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="4d46c-122">Sunucu kodunda, aktarılmaları gerekmeyen özellikleri içeren bir nesne gönderiyorsanız, bu özelliklerin `JsonIgnore` özniteliği kullanılarak serileştirilmesine engel olun.</span><span class="sxs-lookup"><span data-stu-id="4d46c-122">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="4d46c-123">Özelliklerin adları da iletide depolanır; özelliklerinin adları `JsonProperty` özniteliği kullanılarak kısaltılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-123">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="4d46c-124">Aşağıdaki kod örneği, bir özelliğin istemciye gönderilme şeklini ve özellik adlarının nasıl kısaltılanmasını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="4d46c-124">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="4d46c-125">**Verilerin istemciye gönderilmesini hariç tutmak için Jsonıgnore özniteliğini ve ileti boyutunu azaltmak için JsonProperty özniteliğini gösteren .NET Server kodu**</span><span class="sxs-lookup"><span data-stu-id="4d46c-125">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="4d46c-126">İstemci kodunda okunabilirlik/bakım korumasını sürdürmek için, kısaltılmış Özellik adları, ileti alındıktan sonra insanla kolay adlarla yeniden eşlenir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-126">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="4d46c-127">Aşağıdaki kod örneğinde, kısaltılmış adları daha uzun bir süre yeniden eşleştirmenin, bir ileti sözleşmesi tanımlayarak (eşleme) ve sözleşmeyi iyileştirilmiş ileti sınıfına uygulamak için `reMap` işlevini kullanarak bir olası yol gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="4d46c-127">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="4d46c-128">**Kısaltılmış özellik adlarını insan tarafından okunabilen adlara yeniden eşleyen istemci tarafı JavaScript kodu**</span><span class="sxs-lookup"><span data-stu-id="4d46c-128">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="4d46c-129">Adlar istemciden sunucuya, aynı yöntemi kullanarak da kısaltılarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-129">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="4d46c-130">İleti nesnesinin bellek parmak izini (ileti için kullanılan bellek miktarı) azaltmada ayrıca performans de iyileştirebilirler.</span><span class="sxs-lookup"><span data-stu-id="4d46c-130">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="4d46c-131">Örneğin, bir `int` tam aralığı gerekmiyorsa bunun yerine bir `short` veya `byte` kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-131">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="4d46c-132">İletiler, sunucu belleğindeki ileti veri yolunda depolandığından, ileti boyutunu azaltmak sunucu belleği sorunlarını da ele alabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-132">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="4d46c-133">SignalR sunucunuzu performans için ayarlama</span><span class="sxs-lookup"><span data-stu-id="4d46c-133">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="4d46c-134">Aşağıdaki yapılandırma ayarları, sunucunuzu bir SignalR uygulamasında daha iyi performans için ayarlamak üzere kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-134">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="4d46c-135">ASP.NET uygulamasında performansı geliştirme hakkında genel bilgi için bkz. [ASP.net performansını geliştirme](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d46c-135">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="4d46c-136">**SignalR yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="4d46c-136">**SignalR configuration settings**</span></span>

- <span data-ttu-id="4d46c-137">**Defaultmessagebuffersize**: SignalR, bağlantı başına her hub 'da 1000 ileti tutar.</span><span class="sxs-lookup"><span data-stu-id="4d46c-137">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="4d46c-138">Büyük iletiler kullanılıyorsa, bu değer azaltılarak alleviated olabilen bellek sorunları oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-138">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="4d46c-139">Bu ayar bir ASP.NET uygulamasındaki `Application_Start` olay işleyicisine veya şirket içinde barındırılan bir uygulamadaki OWıN başlangıç sınıfının `Configuration` yöntemine ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-139">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="4d46c-140">Aşağıdaki örnek, kullanılan sunucu belleği miktarını azaltmak için uygulamanızın bellek parmak izini azaltmak üzere bu değerin nasıl azaltılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="4d46c-140">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="4d46c-141">**Varsayılan ileti arabelleği boyutunu azaltmak için Global. asax dosyasında .NET Server kodu**</span><span class="sxs-lookup"><span data-stu-id="4d46c-141">**.NET server code in Global.asax for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="4d46c-142">**IIS yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="4d46c-142">**IIS configuration settings**</span></span>

- <span data-ttu-id="4d46c-143">**Uygulama başına en fazla eşzamanlı istek**sayısı: eşzamanlı IIS isteklerinin sayısını artırmak, istek sunmak için kullanılabilir sunucu kaynaklarını arttırır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-143">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="4d46c-144">Varsayılan değer 5000 ' dir; Bu ayarı artırmak için, yükseltilmiş bir komut isteminde aşağıdaki komutları yürütün:</span><span class="sxs-lookup"><span data-stu-id="4d46c-144">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

<span data-ttu-id="4d46c-145">**ASP.NET yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="4d46c-145">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="4d46c-146">Bu bölüm `aspnet.config` dosyasında ayarlankullanılabilecek yapılandırma ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-146">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="4d46c-147">Bu dosya, platforma bağlı olarak iki konumdan birinde bulunur:</span><span class="sxs-lookup"><span data-stu-id="4d46c-147">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="4d46c-148">ASP.NET, SignalR performansını iyileştirebilecek ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4d46c-148">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="4d46c-149">**CPU başına en fazla eşzamanlı istek sayısı**: Bu ayarın artırılması, performans sorunlarını hafifedebilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-149">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="4d46c-150">Bu ayarı artırmak için aşağıdaki yapılandırma ayarını `aspnet.config` dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4d46c-150">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="4d46c-151">**Istek sırası sınırı**: Toplam bağlantı sayısı `maxConcurrentRequestsPerCPU` ayarını aşarsa, ASP.net bir kuyruğu kullanarak istekleri azaltmayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-151">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="4d46c-152">Kuyruğun boyutunu artırmak için `requestQueueLimit` ayarını artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d46c-152">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="4d46c-153">Bunu yapmak için, aşağıdaki yapılandırma ayarını `config/machine.config` `processModel` düğümüne ekleyin (`aspnet.config`yerine):</span><span class="sxs-lookup"><span data-stu-id="4d46c-153">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="4d46c-154">Performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="4d46c-154">Troubleshooting performance issues</span></span>

<span data-ttu-id="4d46c-155">Bu bölümde, uygulamanızda performans sorunlarını bulmanın yolları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-155">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="4d46c-156">WebSocket 'in kullanılmakta olduğu doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="4d46c-156">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="4d46c-157">SignalR, istemci ve sunucu arasındaki iletişim için çeşitli aktarımlar kullanabilir, ancak WebSocket önemli bir performans avantajı sunar ve istemci ve sunucu bunu destekliyorsa kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-157">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="4d46c-158">İstemci ve sunucunuzun WebSocket gereksinimlerini karşılayıp karşılamadığını öğrenmek için bkz. [aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="4d46c-158">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="4d46c-159">Uygulamanızda hangi taşımanın kullanıldığını belirlemek için tarayıcı geliştirici araçlarını kullanabilir ve bağlantı için hangi taşımanın kullanıldığını görmek üzere günlükleri inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d46c-159">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="4d46c-160">Internet Explorer ve Chrome 'daki tarayıcı geliştirme araçlarını kullanma hakkında daha fazla bilgi için bkz. [aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="4d46c-160">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="4d46c-161">SignalR performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="4d46c-161">Using SignalR performance counters</span></span>

<span data-ttu-id="4d46c-162">Bu bölümde, `Microsoft.AspNet.SignalR.Utils` paketinde bulunan SignalR performans sayaçlarının nasıl etkinleştirileceği ve kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-162">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="4d46c-163">SignalR. exe yükleniyor</span><span class="sxs-lookup"><span data-stu-id="4d46c-163">Installing signalr.exe</span></span>

<span data-ttu-id="4d46c-164">Performans sayaçları, SignalR. exe adlı bir yardımcı program kullanılarak sunucuya eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-164">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="4d46c-165">Bu yardımcı programı yüklemek için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d46c-165">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="4d46c-166">Visual Studio 'da **araçlar** > **nuget Paket Yöneticisi** > **çözüm için NuGet Paketlerini Yönet** ' i seçin</span><span class="sxs-lookup"><span data-stu-id="4d46c-166">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="4d46c-167">**SignalR. utils**araması yapın ve yüklemeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="4d46c-167">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="4d46c-168">Paketi yüklemek için lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="4d46c-168">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="4d46c-169">SignalR. exe, `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="4d46c-169">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="4d46c-170">SignalR. exe ile performans sayaçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="4d46c-170">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="4d46c-171">SignalR performans sayaçlarını yüklemek için aşağıdaki parametreyle bir yükseltilmiş komut isteminde SignalR. exe ' yi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4d46c-171">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="4d46c-172">SignalR performans sayaçlarını kaldırmak için, aşağıdaki parametreyle bir yükseltilmiş komut isteminde SignalR. exe ' yi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4d46c-172">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="4d46c-173">SignalR performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="4d46c-173">SignalR Performance counters</span></span>

<span data-ttu-id="4d46c-174">Yardımcı programlar paketi aşağıdaki performans sayaçlarını yükleme.</span><span class="sxs-lookup"><span data-stu-id="4d46c-174">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="4d46c-175">"Toplam" sayacı, son uygulama havuzunun veya sunucu yeniden başlatılmasından bu yana olayların sayısını ölçer.</span><span class="sxs-lookup"><span data-stu-id="4d46c-175">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="4d46c-176">**Bağlantı ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="4d46c-176">**Connection metrics**</span></span>

<span data-ttu-id="4d46c-177">Aşağıdaki ölçümler, gerçekleşen bağlantı ömrü olaylarını ölçer.</span><span class="sxs-lookup"><span data-stu-id="4d46c-177">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="4d46c-178">Daha fazla bilgi için bkz. [bağlantı ömrü olaylarını anlama ve işleme](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="4d46c-178">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="4d46c-179">**Bağlı bağlantılar**</span><span class="sxs-lookup"><span data-stu-id="4d46c-179">**Connections Connected**</span></span>
- <span data-ttu-id="4d46c-180">**Bağlantılar yeniden bağlandı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-180">**Connections Reconnected**</span></span>
- <span data-ttu-id="4d46c-181">**Bağlantı kesilen bağlantılar**</span><span class="sxs-lookup"><span data-stu-id="4d46c-181">**Connections Disconnected**</span></span>
- <span data-ttu-id="4d46c-182">**Geçerli bağlantı sayısı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-182">**Connections Current**</span></span>

<span data-ttu-id="4d46c-183">**İleti ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="4d46c-183">**Message metrics**</span></span>

<span data-ttu-id="4d46c-184">Aşağıdaki ölçümler, SignalR tarafından oluşturulan ileti trafiğini ölçer.</span><span class="sxs-lookup"><span data-stu-id="4d46c-184">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="4d46c-185">**Alınan bağlantı Iletileri toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-185">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="4d46c-186">**Gönderilen bağlantı Iletileri toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-186">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="4d46c-187">**Alınan bağlantı Iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-187">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="4d46c-188">**Gönderilen bağlantı Iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-188">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="4d46c-189">**İleti veri yolu ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="4d46c-189">**Message bus metrics**</span></span>

<span data-ttu-id="4d46c-190">Aşağıdaki ölçümler, gelen ve giden SignalR iletilerinin yerleştirildiği sıra, iç SignalR ileti veri yolu üzerinden trafiği ölçer.</span><span class="sxs-lookup"><span data-stu-id="4d46c-190">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="4d46c-191">İleti gönderildiğinde veya **yayımlandığında yayınlanır** .</span><span class="sxs-lookup"><span data-stu-id="4d46c-191">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="4d46c-192">Bu bağlamdaki bir **abone** , ileti veri yolundaki bir aboneliğiniz; Bu, istemci sayısına ve sunucunun kendine eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-192">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="4d46c-193">**Ayrılmış çalışan** , etkin bağlantılara veri gönderen bir bileşendir; Meşgul bir çalışan, etkin bir şekilde ileti gönderen bir **çalışandır** .</span><span class="sxs-lookup"><span data-stu-id="4d46c-193">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="4d46c-194">**Alınan ileti veri yolu Iletileri toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-194">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="4d46c-195">**Alınan ileti veri yolu iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-195">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="4d46c-196">**İleti veri yolu Iletileri yayımlandı toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-196">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="4d46c-197">**Yayınlanan ileti veri yolu iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-197">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="4d46c-198">**İleti veri yolu aboneleri geçerli**</span><span class="sxs-lookup"><span data-stu-id="4d46c-198">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="4d46c-199">**İleti veri yolu aboneleri toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-199">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="4d46c-200">**İleti veri yolu aboneleri/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-200">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="4d46c-201">**İleti veri yolu ayrılmış çalışanları**</span><span class="sxs-lookup"><span data-stu-id="4d46c-201">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="4d46c-202">**İleti veri yolu meşgul çalışanları**</span><span class="sxs-lookup"><span data-stu-id="4d46c-202">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="4d46c-203">**İleti veri yolu konuları geçerli**</span><span class="sxs-lookup"><span data-stu-id="4d46c-203">**Message Bus Topics Current**</span></span>

<span data-ttu-id="4d46c-204">**Hata ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="4d46c-204">**Error metrics**</span></span>

<span data-ttu-id="4d46c-205">Aşağıdaki ölçümler, SignalR ileti trafiği tarafından oluşturulan hataları ölçer.</span><span class="sxs-lookup"><span data-stu-id="4d46c-205">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="4d46c-206">Hub veya hub yöntemi çözümlenemiyorsa **Merkez çözümleme** hataları oluşur.</span><span class="sxs-lookup"><span data-stu-id="4d46c-206">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="4d46c-207">Hub **çağrısı** hataları, bir hub yöntemi çağrılırken oluşturulan özel durumlardır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-207">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="4d46c-208">**Aktarım** hataları, bir http isteği veya yanıtı sırasında oluşturulan bağlantı hatalardır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-208">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="4d46c-209">**Hatalar: tüm toplam**</span><span class="sxs-lookup"><span data-stu-id="4d46c-209">**Errors: All Total**</span></span>
- <span data-ttu-id="4d46c-210">**Hatalar: tümü/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-210">**Errors: All/Sec**</span></span>
- <span data-ttu-id="4d46c-211">**Hatalar: Merkez çözümleme toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-211">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="4d46c-212">**Hatalar: hub çözümleme/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-212">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="4d46c-213">**Hatalar: hub çağrısı toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-213">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="4d46c-214">**Hatalar: hub çağrı/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-214">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="4d46c-215">**Hatalar: aktarım toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-215">**Errors: Transport Total**</span></span>
- <span data-ttu-id="4d46c-216">**Hatalar: aktarım/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-216">**Errors: Transport/Sec**</span></span>

<span data-ttu-id="4d46c-217">**Genişleme ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="4d46c-217">**Scaleout metrics**</span></span>

<span data-ttu-id="4d46c-218">Aşağıdaki ölçümler, genişleme sağlayıcısı tarafından oluşturulan trafiği ve hataları ölçer.</span><span class="sxs-lookup"><span data-stu-id="4d46c-218">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="4d46c-219">Bu bağlamdaki bir **akış** , genişleme sağlayıcısı tarafından kullanılan bir ölçek birimidir; SQL Server kullanılırsa bu bir tablodur, Service Bus kullanılıyorsa bir konu ve redin kullanılıyorsa bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="4d46c-219">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="4d46c-220">Varsayılan olarak, yalnızca bir akış kullanılır, ancak SQL Server ve Service Bus yapılandırma yoluyla bu şekilde artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-220">By default, only one stream is used, but this can be increased through configuration on SQL Server and Service Bus.</span></span> <span data-ttu-id="4d46c-221">**Arabelleğe alma** akışı, hatalı bir duruma girmiş bir durumdur; akış hatalı durumdaysa, akış artık hatalı olana kadar geri düzleme gönderilen tüm iletiler hemen başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4d46c-221">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="4d46c-222">**Gönderme sırası uzunluğu** , gönderilen ancak henüz gönderilmemiş olan iletilerin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="4d46c-222">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="4d46c-223">**Alınan genişleme Ileti veri yolu Iletisi/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-223">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="4d46c-224">**Ölçek Genişletme akışı toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-224">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="4d46c-225">**Ölçek Genişletme akışları açık**</span><span class="sxs-lookup"><span data-stu-id="4d46c-225">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="4d46c-226">**Genişleme akışları arabelleğe alma**</span><span class="sxs-lookup"><span data-stu-id="4d46c-226">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="4d46c-227">**Ölçek Genişletme hataları toplamı**</span><span class="sxs-lookup"><span data-stu-id="4d46c-227">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="4d46c-228">**Genişleme hatası/sn**</span><span class="sxs-lookup"><span data-stu-id="4d46c-228">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="4d46c-229">**Genişleme gönderme sırası uzunluğu**</span><span class="sxs-lookup"><span data-stu-id="4d46c-229">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="4d46c-230">Bu sayaçların ölçüm hakkında daha fazla bilgi için bkz. [Azure Service Bus Ile SignalR ölçeği](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="4d46c-230">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="4d46c-231">Diğer performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="4d46c-231">Using other performance counters</span></span>

<span data-ttu-id="4d46c-232">Aşağıdaki performans sayaçları, uygulamanızın performansını izlemek için de yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d46c-232">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="4d46c-233">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="4d46c-233">**Memory**</span></span>

- <span data-ttu-id="4d46c-234">.NET CLR bellek sayısı tüm yığınlardaki bayt (W3wp için)</span><span class="sxs-lookup"><span data-stu-id="4d46c-234">.NET CLR Memory# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="4d46c-235">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="4d46c-235">**ASP.NET**</span></span>

- <span data-ttu-id="4d46c-236">ASP. NET\Requests geçerli</span><span class="sxs-lookup"><span data-stu-id="4d46c-236">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="4d46c-237">ASP. NET\Queued</span><span class="sxs-lookup"><span data-stu-id="4d46c-237">ASP.NET\Queued</span></span>
- <span data-ttu-id="4d46c-238">ASP. NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="4d46c-238">ASP.NET\Rejected</span></span>

<span data-ttu-id="4d46c-239">**'SUNA**</span><span class="sxs-lookup"><span data-stu-id="4d46c-239">**CPU**</span></span>

- <span data-ttu-id="4d46c-240">İşlemci Bilgileri\işlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="4d46c-240">Processor Information\Processor Time</span></span>

<span data-ttu-id="4d46c-241">**TCP/ıP**</span><span class="sxs-lookup"><span data-stu-id="4d46c-241">**TCP/IP**</span></span>

- <span data-ttu-id="4d46c-242">TCPv6/bağlantı kurdu</span><span class="sxs-lookup"><span data-stu-id="4d46c-242">TCPv6/Connections Established</span></span>
- <span data-ttu-id="4d46c-243">TCPv4/bağlantı kurdu</span><span class="sxs-lookup"><span data-stu-id="4d46c-243">TCPv4/Connections Established</span></span>

<span data-ttu-id="4d46c-244">**Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="4d46c-244">**Web Service**</span></span>

- <span data-ttu-id="4d46c-245">Web hizmeti \ geçerli bağlantılar</span><span class="sxs-lookup"><span data-stu-id="4d46c-245">Web Service\Current Connections</span></span>
- <span data-ttu-id="4d46c-246">Web hizmeti \ en fazla bağlantı sayısı</span><span class="sxs-lookup"><span data-stu-id="4d46c-246">Web Service\Maximum Connections</span></span>

<span data-ttu-id="4d46c-247">**İş Parçacığı Oluşturma**</span><span class="sxs-lookup"><span data-stu-id="4d46c-247">**Threading**</span></span>

- <span data-ttu-id="4d46c-248">Geçerli mantıksal Iş parçacıklarının\# .NET CLR LocksAndThreads</span><span class="sxs-lookup"><span data-stu-id="4d46c-248">.NET CLR LocksAndThreads\# of current logical Threads</span></span>
- <span data-ttu-id="4d46c-249">Geçerli fiziksel Iş parçacıklarının\# .NET CLR Lockkum Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="4d46c-249">.NET CLR LocksAnd Threads\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="4d46c-250">Diğer Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4d46c-250">Other Resources</span></span>

<span data-ttu-id="4d46c-251">ASP.NET performans izleme ve ayarlama hakkında daha fazla bilgi için aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="4d46c-251">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="4d46c-252">[ASP.NET performansına genel bakış](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="4d46c-252">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="4d46c-253">ASP.NET Iş parçacığı kullanımı IIS 7,5, IIS 7,0 ve IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="4d46c-253">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="4d46c-254">&lt;applicationPool&gt; öğesi (Web ayarları)</span><span class="sxs-lookup"><span data-stu-id="4d46c-254">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
