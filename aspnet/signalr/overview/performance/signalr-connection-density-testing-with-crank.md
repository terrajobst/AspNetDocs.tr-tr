---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: Crank ile SignalR bağlantı yoğunluğu | Microsoft Docs
author: bradygaster
description: Crank ile SignalR Bağlantı Yoğunluğu Testi
ms.author: bradyg
ms.date: 02/22/2015
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: 40c9764f0c47b83df8300553b4b290429937345c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076071"
---
<a name="signalr-connection-density-testing-with-crank"></a><span data-ttu-id="4494c-103">Crank ile SignalR Bağlantı Yoğunluğu Testi</span><span class="sxs-lookup"><span data-stu-id="4494c-103">SignalR Connection Density Testing with Crank</span></span>
====================
<span data-ttu-id="4494c-104">tarafından [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4494c-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4494c-105">Bu makalede, bir uygulama birden çok sanal istemcileri ile test etmek için mili Aracı'nı kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="4494c-105">This article describes how to use the Crank tool to test an application with multiple simulated clients.</span></span>


<span data-ttu-id="4494c-106">Uygulamanızı (ya da bir Azure web rolü, IIS veya Owın kullanarak şirket içinde barındırılan), barındırma ortamı içinde çalışır duruma geçtikten sonra yüksek düzeyde bağlantı yoğunluğu testi mili aracını kullanarak bir uygulamanın yanıt test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4494c-106">Once your application is running in its hosting environment (either an Azure web role, IIS, or self-hosted using Owin), you can test application's response to a high level of connection density using the Crank tool.</span></span> <span data-ttu-id="4494c-107">Barındırma ortamı, Internet Information Services (IIS) sunucu, bir Owın konak veya bir Azure web rolü olabilir.</span><span class="sxs-lookup"><span data-stu-id="4494c-107">The hosting environment can be an Internet Information Services (IIS) server, an Owin host, or an Azure web role.</span></span> <span data-ttu-id="4494c-108">(Not: Öğesinden bir bağlantı yoğunluğu testi performans verilerini almanız mümkün olmayacak şekilde performans sayaçları Azure App Service Web Apps üzerinde kullanılabilir değil.)</span><span class="sxs-lookup"><span data-stu-id="4494c-108">(Note: Performance counters are not available on Azure App Service Web Apps, so you will not be able to get performance data from a connection density test.)</span></span>

<span data-ttu-id="4494c-109">Bağlantı yoğunluğu testi bir sunucuda kurulabilecek eş zamanlı TCP bağlantılarını sayısını ifade eder.</span><span class="sxs-lookup"><span data-stu-id="4494c-109">Connection Density refers to the number of simultaneous TCP connections that can be established on a server.</span></span> <span data-ttu-id="4494c-110">Her TCP bağlantısı kendi ek yüke neden olur ve çok sayıda boşta kalan bağlantıların açma sonunda bir bellek sorunu oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4494c-110">Each TCP connection incurs its own overhead, and opening a large number of idle connections will eventually create a memory bottleneck.</span></span>

<span data-ttu-id="4494c-111">[SignalR codebase](https://github.com/signalr/signalr) adında bir yük testi araç içerir **Crank**.</span><span class="sxs-lookup"><span data-stu-id="4494c-111">[The SignalR codebase](https://github.com/signalr/signalr) includes a load-testing tool called **Crank**.</span></span> <span data-ttu-id="4494c-112">En son sürümünü mili bulunabilir [geliştirme dalını](https://github.com/SignalR/signalr/tree/dev) GitHub üzerinde.</span><span class="sxs-lookup"><span data-stu-id="4494c-112">The latest version of Crank can be found in [the Dev branch](https://github.com/SignalR/signalr/tree/dev) on GitHub.</span></span> <span data-ttu-id="4494c-113">Bir Zip arşivi signalr geliştirme dalı codebase indirebileceğiniz [burada](https://github.com/SignalR/SignalR/archive/dev.zip).</span><span class="sxs-lookup"><span data-stu-id="4494c-113">You can download a Zip archive of the Dev branch of the SignalR codebase [here](https://github.com/SignalR/SignalR/archive/dev.zip).</span></span>

<span data-ttu-id="4494c-114">Mili tam olarak sunucunun bellek saturate için sunucu donanımına olası boşta kalan bağlantıların toplam sayısını hesaplamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4494c-114">Crank may be used to fully saturate the server's memory in order to calculate the total number of idle connections possible on the server hardware.</span></span> <span data-ttu-id="4494c-115">Alternatif olarak, aynı zamanda mili yük testi için sunucunun belirli bir miktarda bellek baskısı altında belirli bir sayısı veya belirli bellek eşiğini ulaşılana kadar bağlantıları ramping kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4494c-115">Alternatively, you may also use Crank to load test the server under a certain amount of memory pressure, by ramping up connections until a specific count or a specific memory threshold is reached.</span></span>

<span data-ttu-id="4494c-116">Test ederken, uzak istemci herhangi bir yarışmaya kaynakları (yani TCP bağlantıları ve bellek gibi) önlemek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="4494c-116">When testing, it is important to use remote client(s) to avoid any competition for resources (i.e., TCP connections and memory).</span></span> <span data-ttu-id="4494c-117">Bunlar sunucunun tam kapasitesi (bellek veya CPU) erişmesini engelleyebilir. tüm performans sorunlarını vpn'den emin olmak için istemci izleme.</span><span class="sxs-lookup"><span data-stu-id="4494c-117">Monitor the client(s) to ensure that they are not hitting any bottlenecks that may prevent the server from reaching its full capacity (memory or CPU).</span></span> <span data-ttu-id="4494c-118">Tam sunucu iş yükü için istemcilerin sayısını artırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="4494c-118">You may need to increase the number of clients in order to fully load the server.</span></span>

### <a name="running-a-connection-density-test"></a><span data-ttu-id="4494c-119">Bir bağlantı yoğunluğu testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4494c-119">Running a Connection Density Test</span></span>

<span data-ttu-id="4494c-120">Bu bölümde bir SignalR uygulama bağlantı yoğunluğu testi çalıştırmak için gereken adımlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4494c-120">This section describes the steps needed to run a connection density test on a SignalR application.</span></span>

1. <span data-ttu-id="4494c-121">İndirin ve derleyin [geliştirme dalını signalr codebase](https://github.com/SignalR/SignalR/archive/dev.zip).</span><span class="sxs-lookup"><span data-stu-id="4494c-121">Download and build the [Dev branch of the SignalR codebase](https://github.com/SignalR/SignalR/archive/dev.zip).</span></span> <span data-ttu-id="4494c-122">Bir komut istemi'nde gidin &lt;proje dizini&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug.</span><span class="sxs-lookup"><span data-stu-id="4494c-122">In a command prompt, navigate to &lt;project directory&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug.</span></span>
2. <span data-ttu-id="4494c-123">Uygulamanızı, hedeflenen barındırma ortamına dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4494c-123">Deploy your application to its intended hosting environment.</span></span> <span data-ttu-id="4494c-124">Uygulamanızın kullandığı uç noktasını not edin; Örneğin, oluşturulan uygulamadaki [Başlarken Öğreticisi](../getting-started/tutorial-getting-started-with-signalr.md), uç nokta `http://<yourhost>:8080/signalr`.</span><span class="sxs-lookup"><span data-stu-id="4494c-124">Make a note of the endpoint that your application uses; for example, in the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), the endpoint is `http://<yourhost>:8080/signalr`.</span></span>
3. <span data-ttu-id="4494c-125">Yükleme [SignalR performans sayaçları](signalr-performance.md#perfcounters) sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="4494c-125">Install [SignalR performance counters](signalr-performance.md#perfcounters) on the server.</span></span> <span data-ttu-id="4494c-126">Uygulamanız Azure üzerinde çalışıyorsa, bkz. [bir Azure Web rolünde SignalR performans sayaçları kullanarak](using-signalr-performance-counters-in-an-azure-web-role.md).</span><span class="sxs-lookup"><span data-stu-id="4494c-126">If your application is running on Azure, see [Using SignalR Performance Counters in an Azure Web Role](using-signalr-performance-counters-in-an-azure-web-role.md).</span></span>

<span data-ttu-id="4494c-127">İçinde indirilen bir kod temelinde oluşturulan ve performans sayaçları, konakta yüklü sonra mili komut satırı aracı bulunabilir `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` klasör.</span><span class="sxs-lookup"><span data-stu-id="4494c-127">Once you've downloaded and built the codebase, and installed performance counters on your host, the Crank command-line tool can be found in the `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` folder.</span></span>

<span data-ttu-id="4494c-128">Mili aracı için kullanılabilir seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4494c-128">Available options for the Crank tool include:</span></span>

- <span data-ttu-id="4494c-129">**/?**: Yardım ekranını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4494c-129">**/?**: Shows the help screen.</span></span> <span data-ttu-id="4494c-130">Kullanılabilir seçenekler de görüntülenir **Url** parametresi atlanırsa.</span><span class="sxs-lookup"><span data-stu-id="4494c-130">The available options are also displayed if the **Url** parameter is omitted.</span></span>
- <span data-ttu-id="4494c-131">**/ Url**: SignalR bağlantıları için URL.</span><span class="sxs-lookup"><span data-stu-id="4494c-131">**/Url**: The URL for SignalR connections.</span></span> <span data-ttu-id="4494c-132">Bu parametre gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4494c-132">This parameter is required.</span></span> <span data-ttu-id="4494c-133">Bir SignalR uygulama için varsayılan eşlemeyi kullanarak yolun içinde sona erecek "/ signalr".</span><span class="sxs-lookup"><span data-stu-id="4494c-133">For a SignalR application using the default mapping, the path will end in "/signalr".</span></span>
- <span data-ttu-id="4494c-134">**/ Aktarım**: Kullanılan taşıma adı.</span><span class="sxs-lookup"><span data-stu-id="4494c-134">**/Transport**: The name of the transport used.</span></span> <span data-ttu-id="4494c-135">Varsayılan `auto`, en iyi kullanılabilir protokol seçer.</span><span class="sxs-lookup"><span data-stu-id="4494c-135">The default is `auto`, which will select the best available protocol.</span></span> <span data-ttu-id="4494c-136">Seçenekleriniz `WebSockets`, `ServerSentEvents`, ve `LongPolling` (`ForeverFrame` yerine Internet Explorer kullanıldığı bir seçenek mili için bu yana .NET istemci değildir).</span><span class="sxs-lookup"><span data-stu-id="4494c-136">Options include `WebSockets`, `ServerSentEvents`, and `LongPolling` (`ForeverFrame` is not an option for Crank, since the .NET client rather than Internet Explorer is used).</span></span> <span data-ttu-id="4494c-137">SignalR taşımalar nasıl seçer? daha fazla bilgi için bkz: [aktarım ve geri dönüşler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="4494c-137">For more information on how SignalR selects transports, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>
- <span data-ttu-id="4494c-138">**/ BatchSize**: Her toplu eklenen istemcilere sayısı.</span><span class="sxs-lookup"><span data-stu-id="4494c-138">**/BatchSize**: The number of clients added in each batch.</span></span> <span data-ttu-id="4494c-139">Varsayılan değer 50'dir.</span><span class="sxs-lookup"><span data-stu-id="4494c-139">The default is 50.</span></span>
- <span data-ttu-id="4494c-140">**/ ConnectInterval**: Bağlantılar ekleme arasındaki milisaniye cinsinden aralığı.</span><span class="sxs-lookup"><span data-stu-id="4494c-140">**/ConnectInterval**: The interval in milliseconds between adding connections.</span></span> <span data-ttu-id="4494c-141">Varsayılan değer 500'dür.</span><span class="sxs-lookup"><span data-stu-id="4494c-141">The default is 500.</span></span>
- <span data-ttu-id="4494c-142">**Bağlantı**: Uygulama yük testi için kullanılan bağlantı sayısı.</span><span class="sxs-lookup"><span data-stu-id="4494c-142">**/Connections**: The number of connections used to load-test the application.</span></span> <span data-ttu-id="4494c-143">Varsayılan değer 100. 000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="4494c-143">The default is 100,000.</span></span>
- <span data-ttu-id="4494c-144">**/ ConnectTimeout**: Test çalışmasını iptal etmeden önce saniye cinsinden zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="4494c-144">**/ConnectTimeout**: The timeout in seconds before aborting the test.</span></span> <span data-ttu-id="4494c-145">Varsayılan değer 300'dür.</span><span class="sxs-lookup"><span data-stu-id="4494c-145">The default is 300.</span></span>
- <span data-ttu-id="4494c-146">**MinServerMBytes**: Ulaşmak için en düşük sunucu megabayt.</span><span class="sxs-lookup"><span data-stu-id="4494c-146">**MinServerMBytes**: The minimum server megabytes to reach.</span></span> <span data-ttu-id="4494c-147">Varsayılan değer 500'dür.</span><span class="sxs-lookup"><span data-stu-id="4494c-147">The default is 500.</span></span>
- <span data-ttu-id="4494c-148">**SendBytes**: Boyutu bayt cinsinden sunucusuna gönderilen yük.</span><span class="sxs-lookup"><span data-stu-id="4494c-148">**SendBytes**: The size of the payload sent to the server in bytes.</span></span> <span data-ttu-id="4494c-149">Varsayılan değer 0'dır.</span><span class="sxs-lookup"><span data-stu-id="4494c-149">The default is 0.</span></span>
- <span data-ttu-id="4494c-150">**SendInterval**: Sunucuya iletileri arasında geçen milisaniye cinsinden gecikme.</span><span class="sxs-lookup"><span data-stu-id="4494c-150">**SendInterval**: The delay in milliseconds between messages to the server.</span></span> <span data-ttu-id="4494c-151">Varsayılan değer 500'dür.</span><span class="sxs-lookup"><span data-stu-id="4494c-151">The default is 500.</span></span>
- <span data-ttu-id="4494c-152">**SendTimeout**: İletileri sunucusu için milisaniye cinsinden zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="4494c-152">**SendTimeout**: The timeout in milliseconds for messages to the server.</span></span> <span data-ttu-id="4494c-153">Varsayılan değer 300'dür.</span><span class="sxs-lookup"><span data-stu-id="4494c-153">The default is 300.</span></span>
- <span data-ttu-id="4494c-154">**ControllerUrl**: Burada bir istemci bir denetleyici hub'ı barındıracak URL'si.</span><span class="sxs-lookup"><span data-stu-id="4494c-154">**ControllerUrl**: The Url where one client will host a controller hub.</span></span> <span data-ttu-id="4494c-155">Varsayılan olarak NULL'dur (denetleyici hub).</span><span class="sxs-lookup"><span data-stu-id="4494c-155">The default is null (no controller hub).</span></span> <span data-ttu-id="4494c-156">Denetleyici hub mili oturumu başladığında başlatıldı; Daha fazla kişi denetleyicisi hub'ı ve mili arasında yapılır.</span><span class="sxs-lookup"><span data-stu-id="4494c-156">The controller hub is started when the Crank session starts; no further contact between the controller hub and Crank is made.</span></span>
- <span data-ttu-id="4494c-157">**NumClients**: Uygulamaya bağlanmak için sanal istemci sayısı.</span><span class="sxs-lookup"><span data-stu-id="4494c-157">**NumClients**: The number of simulated clients to connect to the application.</span></span> <span data-ttu-id="4494c-158">Varsayılan biridir.</span><span class="sxs-lookup"><span data-stu-id="4494c-158">The default is one.</span></span>
- <span data-ttu-id="4494c-159">**Günlük dosyası**: Test çalıştırması için bir günlük dosyası için dosya adı.</span><span class="sxs-lookup"><span data-stu-id="4494c-159">**Logfile**: The filename for the logfile for the test run.</span></span> <span data-ttu-id="4494c-160">Varsayılan, `crank.csv` değeridir.</span><span class="sxs-lookup"><span data-stu-id="4494c-160">The default is `crank.csv`.</span></span>
- <span data-ttu-id="4494c-161">**SampleInterval**: Performans sayacı Örnekler arasındaki milisaniye olarak süre.</span><span class="sxs-lookup"><span data-stu-id="4494c-161">**SampleInterval**: The time in milliseconds between performance counter samples.</span></span> <span data-ttu-id="4494c-162">Varsayılan değer 1000'dir.</span><span class="sxs-lookup"><span data-stu-id="4494c-162">The default is 1000.</span></span>
- <span data-ttu-id="4494c-163">**SignalRInstance**: Sunucusunda performans sayaçları için örnek adı.</span><span class="sxs-lookup"><span data-stu-id="4494c-163">**SignalRInstance**: The instance name for the performance counters on the server.</span></span> <span data-ttu-id="4494c-164">Varsayılan istemci bağlantı durumu kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="4494c-164">The default is to use the client connection state.</span></span>

### <a name="example"></a><span data-ttu-id="4494c-165">Örnek</span><span class="sxs-lookup"><span data-stu-id="4494c-165">Example</span></span>

<span data-ttu-id="4494c-166">Aşağıdaki komutu adlı bir sitede sınayacak `pfsignalr` "ControllerHub" adlı bir hub ile bağlantı noktası 8080 üzerinde uygulama barındıran Azure üzerinde 100 bağlantı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4494c-166">The following command will test a site called `pfsignalr` on Azure that hosts an application on port 8080 with a hub named "ControllerHub", using 100 connections.</span></span>

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`