---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2 ' de izleme | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'sinde izlemenin nasıl etkinleştirileceğini gösterir.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598555"
---
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="a9733-103">ASP.NET Web API 2 ' de izleme</span><span class="sxs-lookup"><span data-stu-id="a9733-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="a9733-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a9733-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="a9733-105">Web tabanlı bir uygulamada hata ayıklamaya çalışırken, uygun bir izleme günlüğü kümesi için bir değiştirme yoktur.</span><span class="sxs-lookup"><span data-stu-id="a9733-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="a9733-106">Bu öğreticide, ASP.NET Web API 'sinde izlemenin nasıl etkinleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a9733-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="a9733-107">Bu özelliği, Web API çerçevesinin denetleyicinizi uyguladıktan önce ve sonra ne yaptığını izlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9733-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="a9733-108">Ayrıca, kendi kodunuzu izlemek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9733-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a9733-109">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="a9733-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="a9733-110">[Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (visual Studio 2015 ile de geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="a9733-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="a9733-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a9733-111">Web API 2</span></span>
> - [<span data-ttu-id="a9733-112">Microsoft. AspNet. WebApi. Tracing</span><span class="sxs-lookup"><span data-stu-id="a9733-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="a9733-113">Web API 'de System. Diagnostics Izlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a9733-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="a9733-114">İlk olarak yeni bir ASP.NET Web uygulaması projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="a9733-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="a9733-115">Visual Studio 'da, **Dosya** menüsünden **Yeni** > **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a9733-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="a9733-116">**Şablonlar**, **Web**, **ASP.NET Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="a9733-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="a9733-117">Web API 'SI proje şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="a9733-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="a9733-118">**Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni ve ardından **paket yönetim konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="a9733-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="a9733-119">Paket Yöneticisi konsolu penceresinde aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="a9733-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="a9733-120">İlk komut en son Web API izleme paketini yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="a9733-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="a9733-121">Ayrıca çekirdek Web API paketlerini de güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a9733-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="a9733-122">İkinci komut, WebApi. WebHost paketini en son sürüme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a9733-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="a9733-123">Web API 'nin belirli bir sürümünü hedeflemek istiyorsanız, izleme paketini yüklerken-Version bayrağını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9733-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="a9733-124">WebApiConfig.cs dosyasını uygulama\_başlangıç klasöründe açın.</span><span class="sxs-lookup"><span data-stu-id="a9733-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="a9733-125">**Register** yöntemine aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9733-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="a9733-126">Bu kod, [Systemdiagnosticstracewriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) SıNıFıNı Web API ardışık düzenine ekler.</span><span class="sxs-lookup"><span data-stu-id="a9733-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="a9733-127">**Systemdiagnosticstracewriter** sınıfı, izlemeleri [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)öğesine yazar.</span><span class="sxs-lookup"><span data-stu-id="a9733-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="a9733-128">İzlemeleri görmek için, uygulamayı hata ayıklayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a9733-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="a9733-129">Tarayıcıda `/api/values` adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="a9733-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="a9733-130">Trace deyimleri, Visual Studio 'daki çıkış penceresine yazılır.</span><span class="sxs-lookup"><span data-stu-id="a9733-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="a9733-131">( **Görünüm** menüsünde **Çıkış**' ı seçin).</span><span class="sxs-lookup"><span data-stu-id="a9733-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="a9733-132">**Systemdiagnosticstracewriter** izlemeleri **System. Diagnostics. Trace**'e yazardığı için, ek izleme dinleyicilerini kaydedebilirsiniz; Örneğin, bir günlük dosyasına izlemeler yazmak için.</span><span class="sxs-lookup"><span data-stu-id="a9733-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="a9733-133">İzleme yazarları hakkında daha fazla bilgi için MSDN 'deki [Izleme dinleyicileri](https://msdn.microsoft.com/library/4y5y10s7.aspx) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="a9733-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="a9733-134">SystemDiagnosticsTraceWriter 'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a9733-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="a9733-135">Aşağıdaki kod, izleme yazıcısının nasıl yapılandırılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9733-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="a9733-136">Denetleyebilmeniz gereken iki ayar vardır:</span><span class="sxs-lookup"><span data-stu-id="a9733-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="a9733-137">Isverbose: yanlışsa, her izleme en az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a9733-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="a9733-138">True ise izlemeler daha fazla bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a9733-138">If true, traces include more information.</span></span>
- <span data-ttu-id="a9733-139">MinimumLevel: en düşük izleme düzeyini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a9733-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="a9733-140">İzleme düzeyleri, sırasıyla hata ayıklama, bilgi, uyarı, hata ve önemli.</span><span class="sxs-lookup"><span data-stu-id="a9733-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="a9733-141">Web API uygulamanıza Izleme ekleme</span><span class="sxs-lookup"><span data-stu-id="a9733-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="a9733-142">İzleme yazıcısı eklemek, Web API işlem hattı tarafından oluşturulan izlemelere anında erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9733-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="a9733-143">İzleme yazıcısını, kendi kodunuzu izlemek için de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9733-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="a9733-144">İzleme yazıcısını almak için **HttpConfiguration. Services. GetTraceWriter**' ı çağırın.</span><span class="sxs-lookup"><span data-stu-id="a9733-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="a9733-145">Denetleyiciden, bu yönteme **Apicontroller. Configuration** özelliği aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a9733-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="a9733-146">Bir izleme yazmak için **ıstracewriter. Trace** yöntemini doğrudan çağırabilirsiniz, ancak [ıstracewriterextensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) sınıfı daha kolay olan bazı uzantı yöntemlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a9733-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="a9733-147">Örneğin, yukarıda gösterilen **Info** yöntemi Izleme düzeyi **bilgiyle**bir izleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9733-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="a9733-148">Web API Izleme altyapısı</span><span class="sxs-lookup"><span data-stu-id="a9733-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="a9733-149">Bu bölümde, Web API 'SI için özel bir izleme yazıcısının nasıl yazılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a9733-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="a9733-150">Microsoft. AspNet. WebApi. Tracing paketi, Web API 'sinde daha genel bir izleme altyapısının üzerine kurulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a9733-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="a9733-151">Microsoft. AspNet. WebApi. Tracing kullanmak yerine, [NLog](http://nlog-project.org/) veya [Log4net](http://logging.apache.org/log4net/)gibi başka bir izleme/günlüğe kaydetme kitaplığı da takabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9733-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="a9733-152">İzlemeleri toplamak için **ıstracewriter** arabirimini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a9733-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="a9733-153">İşte basit bir örnek:</span><span class="sxs-lookup"><span data-stu-id="a9733-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="a9733-154">**Istracewriter. Trace** yöntemi bir izleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9733-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="a9733-155">Çağıran bir kategori ve izleme düzeyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="a9733-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="a9733-156">Kategori, Kullanıcı tanımlı herhangi bir dize olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9733-156">The category can be any user-defined string.</span></span> <span data-ttu-id="a9733-157">**İzleme** uygulamanız aşağıdakileri yapması gerekir:</span><span class="sxs-lookup"><span data-stu-id="a9733-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="a9733-158">Yeni bir izleme kaydı **oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="a9733-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="a9733-159">Bunu gösterildiği gibi istek, kategori ve İzleme düzeyiyle başlatın.</span><span class="sxs-lookup"><span data-stu-id="a9733-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="a9733-160">Bu değerler, çağıran tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a9733-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="a9733-161">*Traceaction* temsilcisini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a9733-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="a9733-162">Bu temsilcinin içinde çağıranın, izleme **ecord**öğesinin geri kalanını doldurması beklenir.</span><span class="sxs-lookup"><span data-stu-id="a9733-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="a9733-163">İstediğiniz günlüğekaydetme tekniğini kullanarak izleme kaydını yazın.</span><span class="sxs-lookup"><span data-stu-id="a9733-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="a9733-164">Burada gösterilen örnek yalnızca **System. Diagnostics. Trace**öğesine çağrı yapılır.</span><span class="sxs-lookup"><span data-stu-id="a9733-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="a9733-165">Izleme yazıcısını ayarlama</span><span class="sxs-lookup"><span data-stu-id="a9733-165">Setting the Trace Writer</span></span>

<span data-ttu-id="a9733-166">İzlemeyi etkinleştirmek için, Web API 'nizi **ıstracewriter** uygulamanızı kullanacak şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9733-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="a9733-167">Bunu, aşağıdaki kodda gösterildiği gibi **HttpConfiguration** nesnesi aracılığıyla yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9733-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="a9733-168">Yalnızca bir izleme yazıcısı etkin olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9733-168">Only one trace writer can be active.</span></span> <span data-ttu-id="a9733-169">Web API 'SI varsayılan olarak hiçbir şey olmayan &quot;op&quot; izleyiciyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a9733-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="a9733-170">(&quot;-op&quot; izleyici, izleme kodunun bir izleme yazmadan önce izleme yazıcısının **null** olup olmadığını kontrol etmek zorunda kalmayacak şekilde bulunur.)</span><span class="sxs-lookup"><span data-stu-id="a9733-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="a9733-171">Web API Izlemenin çalışması</span><span class="sxs-lookup"><span data-stu-id="a9733-171">How Web API Tracing Works</span></span>

<span data-ttu-id="a9733-172">Web API 'de izleme bir *façlade* düzeni kullanır: izleme etkinleştirildiğinde, Web API 'si, istek işlem hattının çeşitli kısımlarını izleme çağrıları gerçekleştiren sınıflarla sarmalar.</span><span class="sxs-lookup"><span data-stu-id="a9733-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="a9733-173">Örneğin, bir denetleyici seçerken, işlem hattı **IHttpControllerSelector** arabirimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9733-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="a9733-174">İzleme etkinken, işlem hattı **IHttpControllerSelector** uygulayan ancak gerçek uygulamaya çağrı yapan bir sınıf ekler:</span><span class="sxs-lookup"><span data-stu-id="a9733-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API izleme façlade modelini kullanır.](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="a9733-176">Bu tasarımın avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a9733-176">The benefits of this design include:</span></span>

- <span data-ttu-id="a9733-177">İzleme yazıcısı eklemeyin, izleme bileşenleri örneklenemez ve hiçbir performans etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="a9733-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="a9733-178">**IHttpControllerSelector** gibi varsayılan Hizmetleri kendi özel uygulamanıza göre değiştirirseniz, izleme sarmalayıcı nesne tarafından yapıldığından izleme etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="a9733-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="a9733-179">Varsayılan **ıstracemanager** hizmetini değiştirerek tüm Web API izleme çerçevesini kendi özel çerçevesinden da değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9733-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="a9733-180">İzleme sisteminizi başlatmak için **ıstracemanager. Initialize** uygulamasını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a9733-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="a9733-181">Bunun, Web API 'sinde yerleşik olarak bulunan tüm izleme kodları da dahil olmak üzere *Tüm Trace çerçevesinin* yerini aldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a9733-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
