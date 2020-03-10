---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API 'SI içindeki HTTP Ileti Işleyicileri-ASP.NET 4. x
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Web API 'sindeki HTTP ileti işleyicilerine genel bakış
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622586"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="35283-103">ASP.NET Web API 'de HTTP Ileti Işleyicileri</span><span class="sxs-lookup"><span data-stu-id="35283-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="35283-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="35283-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="35283-105">*İleti işleyicisi* , http isteği alan ve http yanıtı döndüren bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="35283-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="35283-106">İleti işleyicileri soyut **HttpMessageHandler** sınıfından türetilir.</span><span class="sxs-lookup"><span data-stu-id="35283-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="35283-107">Genellikle, bir dizi ileti işleyicisi birlikte zincirleme yapılır.</span><span class="sxs-lookup"><span data-stu-id="35283-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="35283-108">İlk işleyici bir HTTP isteği alır, bazı işlemleri yapar ve isteği bir sonraki işleyiciye verir.</span><span class="sxs-lookup"><span data-stu-id="35283-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="35283-109">Bir noktada yanıt oluşturulur ve zinciri yedekler.</span><span class="sxs-lookup"><span data-stu-id="35283-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="35283-110">Bu düzene *temsilci seçme* işleyicisi denir.</span><span class="sxs-lookup"><span data-stu-id="35283-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="35283-111">Sunucu tarafı Ileti Işleyicileri</span><span class="sxs-lookup"><span data-stu-id="35283-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="35283-112">Sunucu tarafında, Web API 'SI ardışık düzeni bazı yerleşik ileti işleyicileri kullanır:</span><span class="sxs-lookup"><span data-stu-id="35283-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="35283-113">**HttpServer** , konaktan gelen isteği alır.</span><span class="sxs-lookup"><span data-stu-id="35283-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="35283-114">**Httproutingdispatcher** , isteği yola göre dağıtır.</span><span class="sxs-lookup"><span data-stu-id="35283-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="35283-115">**Httpcontrollerdispatcher** , Isteği BIR Web API denetleyicisine gönderir.</span><span class="sxs-lookup"><span data-stu-id="35283-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="35283-116">Komut hattına özel işleyiciler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35283-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="35283-117">İleti işleyicileri, HTTP iletileri düzeyinde (denetleyici eylemleri yerine) çalışan çapraz kesme sorunları için uygundur.</span><span class="sxs-lookup"><span data-stu-id="35283-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="35283-118">Örneğin, bir ileti işleyicisi şunları içerebilir:</span><span class="sxs-lookup"><span data-stu-id="35283-118">For example, a message handler might:</span></span>

- <span data-ttu-id="35283-119">İstek üst bilgilerini okuyun veya değiştirin.</span><span class="sxs-lookup"><span data-stu-id="35283-119">Read or modify request headers.</span></span>
- <span data-ttu-id="35283-120">Yanıtlara bir yanıt üst bilgisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="35283-120">Add a response header to responses.</span></span>
- <span data-ttu-id="35283-121">İstekleri denetleyiciye ulaşmadan önce doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="35283-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="35283-122">Bu diyagramda, ardışık düzene yerleştirilmiş iki özel işleyici gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="35283-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="35283-123">İstemci tarafında HttpClient Ayrıca ileti işleyicilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="35283-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="35283-124">Daha fazla bilgi için bkz. [HttpClient Ileti işleyicileri](httpclient-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="35283-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="35283-125">Özel Ileti Işleyicileri</span><span class="sxs-lookup"><span data-stu-id="35283-125">Custom Message Handlers</span></span>

<span data-ttu-id="35283-126">Özel bir ileti işleyicisi yazmak için, **System .net. http. DelegatingHandler** 'ten türetirsiniz ve **sendadsync** yöntemini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="35283-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="35283-127">Bu yöntem aşağıdaki imzaya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="35283-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="35283-128">Yöntemi, giriş olarak bir **HttpRequestMessage** alır ve zaman uyumsuz bir **HttpResponseMessage**döndürür.</span><span class="sxs-lookup"><span data-stu-id="35283-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="35283-129">Tipik bir uygulama şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="35283-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="35283-130">İstek iletisini işleyin.</span><span class="sxs-lookup"><span data-stu-id="35283-130">Process the request message.</span></span>
2. <span data-ttu-id="35283-131">İsteği iç işleyiciye göndermek için `base.SendAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="35283-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="35283-132">İç işleyici bir yanıt iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="35283-132">The inner handler returns a response message.</span></span> <span data-ttu-id="35283-133">(Bu adım zaman uyumsuzdur.)</span><span class="sxs-lookup"><span data-stu-id="35283-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="35283-134">Yanıtı işleyin ve çağırana döndürün.</span><span class="sxs-lookup"><span data-stu-id="35283-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="35283-135">Önemsiz bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="35283-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="35283-136">`base.SendAsync` çağrısı zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="35283-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="35283-137">İşleyici Bu çağrıdan sonra herhangi bir çalışmayı yapar, gösterildiği gibi **await** anahtar sözcüğünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="35283-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>

<span data-ttu-id="35283-138">Ayrıca, bir temsilci işleyicisi iç işleyiciyi atlayabilir ve yanıtı doğrudan oluşturabilir:</span><span class="sxs-lookup"><span data-stu-id="35283-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="35283-139">Bir temsilci işleyicisi `base.SendAsync`çağrılmadan yanıt oluşturursa, istek işlem hattının geri kalanını atlar.</span><span class="sxs-lookup"><span data-stu-id="35283-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="35283-140">Bu, isteği doğrulayan bir işleyici için yararlı olabilir (hata yanıtı oluşturma).</span><span class="sxs-lookup"><span data-stu-id="35283-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="35283-141">İşlem hattına Işleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="35283-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="35283-142">Sunucu tarafında bir ileti işleyicisi eklemek için, işleyiciyi **HttpConfiguration. MessageHandlers** koleksiyonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="35283-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="35283-143">Projeyi oluşturmak için "ASP.NET MVC 4 Web uygulaması" şablonunu kullandıysanız, bunu **WebApiConfig** sınıfının içinde yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="35283-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="35283-144">İleti işleyicileri **Messagehandlers** koleksiyonunda göründükleri sırada çağrılır.</span><span class="sxs-lookup"><span data-stu-id="35283-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="35283-145">İç içe olduklarından yanıt iletisi diğer yönde hareket eder.</span><span class="sxs-lookup"><span data-stu-id="35283-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="35283-146">Diğer bir deyişle, son işleyici yanıt iletisini ilk kez alır.</span><span class="sxs-lookup"><span data-stu-id="35283-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="35283-147">İç işleyicileri ayarlamanız gerekmez; Web API çerçevesi, ileti işleyicilerini otomatik olarak bağlar.</span><span class="sxs-lookup"><span data-stu-id="35283-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="35283-148">[Kendi kendine barındırıyorsanız](../older-versions/self-host-a-web-api.md), **Httpselfhostconfiguration** sınıfının bir örneğini oluşturun ve işleyicileri **messagehandlers** koleksiyonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="35283-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="35283-149">Şimdi özel ileti işleyicilerinin bazı örneklerine göz atalım.</span><span class="sxs-lookup"><span data-stu-id="35283-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="35283-150">Örnek: X-HTTP-Method-override</span><span class="sxs-lookup"><span data-stu-id="35283-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="35283-151">X-HTTP-Method-override standart olmayan bir HTTP üst bilgisi.</span><span class="sxs-lookup"><span data-stu-id="35283-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="35283-152">PUT veya DELETE gibi belirli HTTP istek türlerini gönderemediği istemciler için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="35283-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="35283-153">Bunun yerine, istemci bir POST isteği gönderir ve X-HTTP-Method-override üst bilgisini istenen metoda ayarlar.</span><span class="sxs-lookup"><span data-stu-id="35283-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="35283-154">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="35283-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="35283-155">X-HTTP-Method-override için destek ekleyen bir ileti işleyicisi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="35283-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="35283-156">**Sendadsync** yönteminde, işleyici istek ILETISININ bir post isteği olup olmadığını ve X-http-Method-override üst bilgisini içerip içermediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="35283-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="35283-157">Bu durumda, üst bilgi değerini doğrular ve sonra istek metodunu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="35283-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="35283-158">Son olarak, işleyici iletiyi sonraki işleyiciye geçirmek için `base.SendAsync` çağırır.</span><span class="sxs-lookup"><span data-stu-id="35283-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="35283-159">İstek **httpcontrollerdispatcher** sınıfına ulaştığında, **httpcontrollerdispatcher** isteği güncelleştirilmiş istek yöntemine göre yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="35283-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="35283-160">Örnek: özel yanıt üst bilgisi ekleme</span><span class="sxs-lookup"><span data-stu-id="35283-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="35283-161">Her yanıt iletisine özel bir üst bilgi ekleyen bir ileti işleyicisi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="35283-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="35283-162">İlk olarak, işleyici isteği iç ileti işleyicisine geçirmek için `base.SendAsync` çağırır.</span><span class="sxs-lookup"><span data-stu-id="35283-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="35283-163">İç işleyici bir yanıt iletisi döndürür, ancak bunu zaman uyumsuz bir **görev&lt;t&gt;** nesnesi kullanarak yapar.</span><span class="sxs-lookup"><span data-stu-id="35283-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="35283-164">Yanıt iletisi `base.SendAsync` zaman uyumsuz olarak tamamlanana kadar kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="35283-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="35283-165">Bu örnek, `SendAsync` tamamlandıktan sonra zaman uyumsuz olarak çalışmayı gerçekleştirmek için **await** anahtar sözcüğünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="35283-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="35283-166">.NET Framework 4,0 ' i hedefliyorsanız,&lt;T&gt;**görevini** kullanın **. Yönteme devam** edin:</span><span class="sxs-lookup"><span data-stu-id="35283-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="35283-167">Örnek: bir API anahtarı denetleniyor</span><span class="sxs-lookup"><span data-stu-id="35283-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="35283-168">Bazı Web Hizmetleri, istemcilerin istemesi için bir API anahtarı içermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="35283-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="35283-169">Aşağıdaki örnek bir ileti işleyicisinin geçerli bir API anahtarı için istekleri nasıl denetlegösterdiğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="35283-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="35283-170">Bu işleyici, URI sorgu dizesinde API anahtarını arar.</span><span class="sxs-lookup"><span data-stu-id="35283-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="35283-171">(Bu örnekte, anahtarın bir statik dize olduğunu varsaytık.</span><span class="sxs-lookup"><span data-stu-id="35283-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="35283-172">Gerçek bir uygulama, büyük olasılıkla daha karmaşık doğrulama kullanır.) Sorgu dizesi anahtarı içeriyorsa, işleyici isteği iç işleyiciye geçirir.</span><span class="sxs-lookup"><span data-stu-id="35283-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="35283-173">İstek geçerli bir anahtara sahip değilse, işleyici durum 403 olan bir yanıt iletisi oluşturur, yasak.</span><span class="sxs-lookup"><span data-stu-id="35283-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="35283-174">Bu durumda, işleyici `base.SendAsync`çağırmaz, bu nedenle iç işleyici isteği hiçbir şekilde almaz veya denetleyici yapmaz.</span><span class="sxs-lookup"><span data-stu-id="35283-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="35283-175">Bu nedenle, denetleyici tüm gelen isteklerin geçerli bir API anahtarı olduğunu varsayabilir.</span><span class="sxs-lookup"><span data-stu-id="35283-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="35283-176">API anahtarı yalnızca belirli denetleyici eylemlerine geçerliyse, ileti işleyicisi yerine bir eylem filtresi kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="35283-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="35283-177">İşlem filtreleri URI yönlendirmesi gerçekleştirildikten sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="35283-177">Action filters run after URI routing is performed.</span></span>

## <a name="per-route-message-handlers"></a><span data-ttu-id="35283-178">Yol başına Ileti Işleyicileri</span><span class="sxs-lookup"><span data-stu-id="35283-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="35283-179">**HttpConfiguration. messagehandlers** koleksiyonundaki işleyiciler küresel olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="35283-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="35283-180">Alternatif olarak, yolu tanımlarken belirli bir yola bir ileti işleyicisi ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="35283-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="35283-181">Bu örnekte, istek URI 'SI "Route2" ile eşleşiyorsa, istek `MessageHandler2`gönderilir.</span><span class="sxs-lookup"><span data-stu-id="35283-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="35283-182">Aşağıdaki diyagramda bu iki yolun işlem hattı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="35283-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="35283-183">`MessageHandler2` varsayılan **Httpcontrollerdispatcher**'ın yerini aldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="35283-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="35283-184">Bu örnekte, `MessageHandler2` yanıtı oluşturur ve "Route2" ile eşleşen istekler hiçbir şekilde denetleyiciye gitmez.</span><span class="sxs-lookup"><span data-stu-id="35283-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="35283-185">Bu, tüm Web API denetleyici mekanizmasını kendi özel uç noktanızla değiştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="35283-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="35283-186">Alternatif olarak, yönlendirme başına ileti işleyicisi, daha sonra bir denetleyiciye dağıtırsa **Httpcontrollerdispatcher**öğesine temsilci seçebilir.</span><span class="sxs-lookup"><span data-stu-id="35283-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="35283-187">Aşağıdaki kod, bu yolun nasıl yapılandırılacağını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="35283-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
