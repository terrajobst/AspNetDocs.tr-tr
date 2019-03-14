---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API HTTP ileti işleyicileri | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 02/13/2012
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 0b0d7b4c543dc4e597c6c472083898f3a8095a83
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071601"
---
<a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="b7844-102">ASP.NET Web API HTTP ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="b7844-102">HTTP Message Handlers in ASP.NET Web API</span></span>
====================
<span data-ttu-id="b7844-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b7844-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b7844-104">A *ileti işleyicisi* HTTP isteği aldığında ve bir HTTP yanıtı döndüren bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="b7844-104">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="b7844-105">İleti işleyicileri türetilen Özet **HttpMessageHandler** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b7844-105">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="b7844-106">Genellikle, bir dizi ileti işleyicileri zincirleme birlikte.</span><span class="sxs-lookup"><span data-stu-id="b7844-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="b7844-107">İlk işleyici HTTP isteği aldığında, işlem yapar ve bir sonraki işleyici istek sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7844-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="b7844-108">Belirli bir noktada yanıt oluşturulur ve zincirinde döner.</span><span class="sxs-lookup"><span data-stu-id="b7844-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="b7844-109">Bu düzen adı verilen bir *temsilci olarak görevlendirme* işleyici.</span><span class="sxs-lookup"><span data-stu-id="b7844-109">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="b7844-110">Sunucu tarafı ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="b7844-110">Server-Side Message Handlers</span></span>

<span data-ttu-id="b7844-111">Sunucu tarafında, Web API ardışık düzeni bazı yerleşik ileti işleyicileri kullanır:</span><span class="sxs-lookup"><span data-stu-id="b7844-111">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="b7844-112">**HttpServer** istek ana bilgisayarından alır.</span><span class="sxs-lookup"><span data-stu-id="b7844-112">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="b7844-113">**HttpRoutingDispatcher** yola göre isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="b7844-113">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="b7844-114">**HttpControllerDispatcher** bir Web API denetleyicisine istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="b7844-114">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="b7844-115">İşlem hattı için özel işleyicileri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7844-115">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="b7844-116">İleti işleyicileri, HTTP iletileri (yerine denetleyici eylemleri) düzeyinde çalışan çapraz kesme konuları için uygundur.</span><span class="sxs-lookup"><span data-stu-id="b7844-116">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="b7844-117">Örneğin, bir ileti işleyicisi olabilir:</span><span class="sxs-lookup"><span data-stu-id="b7844-117">For example, a message handler might:</span></span>

- <span data-ttu-id="b7844-118">Okuma veya istek üst bilgilerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b7844-118">Read or modify request headers.</span></span>
- <span data-ttu-id="b7844-119">Yanıt üst bilgisi yanıtlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7844-119">Add a response header to responses.</span></span>
- <span data-ttu-id="b7844-120">Denetleyici ulaşmadan önce istekleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b7844-120">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="b7844-121">Bu diyagramda, ardışık düzende eklenen iki özel işleyicileri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b7844-121">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="b7844-122">İstemci tarafında HttpClient ileti işleyicileri de kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7844-122">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="b7844-123">Daha fazla bilgi için [HttpClient ileti işleyicileri](httpclient-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="b7844-123">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="b7844-124">Özel ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="b7844-124">Custom Message Handlers</span></span>

<span data-ttu-id="b7844-125">Özel ileti işleyicisi yazmak için türetilen **System.Net.Http.DelegatingHandler** ve geçersiz kılma **SendAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b7844-125">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="b7844-126">Bu yöntem, aşağıdaki imzası vardır:</span><span class="sxs-lookup"><span data-stu-id="b7844-126">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="b7844-127">Yöntem alır bir **HttpRequestMessage** giriş ve zaman uyumsuz olarak döndürür olarak bir **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="b7844-127">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="b7844-128">Tipik bir uygulaması şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="b7844-128">A typical implementation does the following:</span></span>

1. <span data-ttu-id="b7844-129">İşlem istek iletisi.</span><span class="sxs-lookup"><span data-stu-id="b7844-129">Process the request message.</span></span>
2. <span data-ttu-id="b7844-130">Çağrı `base.SendAsync` iç işleyici için istek gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7844-130">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="b7844-131">İç işleyici, bir yanıt iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="b7844-131">The inner handler returns a response message.</span></span> <span data-ttu-id="b7844-132">(Bu adım, zaman uyumsuz.)</span><span class="sxs-lookup"><span data-stu-id="b7844-132">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="b7844-133">Yanıta işlemek ve çağırana döndürmesi.</span><span class="sxs-lookup"><span data-stu-id="b7844-133">Process the response and return it to the caller.</span></span>

<span data-ttu-id="b7844-134">Önemsiz bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b7844-134">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="b7844-135">Çağrı `base.SendAsync` zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="b7844-135">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="b7844-136">İşleyici, bu çağrıdan sonra herhangi bir iş varsa, kullanmak **await** gösterildiği gibi anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="b7844-136">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>


<span data-ttu-id="b7844-137">Bir temsilci işleyicisi, ayrıca iç işleyici atlamak ve doğrudan yanıt oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b7844-137">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="b7844-138">Bir temsilci işleyicisi çağırmadan yanıtı oluşturur `base.SendAsync`, rest işlem hattının istek atlar.</span><span class="sxs-lookup"><span data-stu-id="b7844-138">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="b7844-139">(Bir hata yanıtı oluşturma) istek doğrulama için bir işleyici yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b7844-139">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="b7844-140">İşlem hattı için bir işleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="b7844-140">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="b7844-141">Sunucu tarafında bir ileti işleyicisi eklemek için ekleyebilirsiniz **HttpConfiguration.MessageHandlers** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="b7844-141">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="b7844-142">Projeyi oluşturmak için "ASP.NET MVC 4 Web uygulaması" şablonunu kullandıysanız, bu iç yapabileceğiniz **WebApiConfig** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b7844-142">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="b7844-143">İleti işleyicileri görünürler aynı sırayla çağrılır **MessageHandlers** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="b7844-143">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="b7844-144">Yanıt iletisi içe yer olduğundan, diğer yönde hareket eder.</span><span class="sxs-lookup"><span data-stu-id="b7844-144">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="b7844-145">Diğer bir deyişle, son ilk yanıt iletisi işleyicidir.</span><span class="sxs-lookup"><span data-stu-id="b7844-145">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="b7844-146">İç işleyicileri ayarlamanız gerekmez dikkat edin. Web API çerçevesi, ileti işleyicileri otomatik olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b7844-146">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="b7844-147">Eğer [kendi kendine barındırma](../older-versions/self-host-a-web-api.md), bir örneğini oluşturmak **HttpSelfHostConfiguration** sınıfı ve işleyicileri ekleyin **MessageHandlers** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="b7844-147">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="b7844-148">Artık özel ileti işleyicileri bazı örneklere bakalım.</span><span class="sxs-lookup"><span data-stu-id="b7844-148">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="b7844-149">Örnek: X-HTTP-yöntemi-geçersiz kıl</span><span class="sxs-lookup"><span data-stu-id="b7844-149">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="b7844-150">Standart olmayan bir HTTP üst bilgisi X-HTTP-Method-Override ' dir.</span><span class="sxs-lookup"><span data-stu-id="b7844-150">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="b7844-151">PUT veya silme gibi belirli HTTP istek türlerini gönderilemiyor istemciler için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b7844-151">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="b7844-152">Bunun yerine, istemci bir POST isteği gönderir ve istenen yöntemin X-HTTP-Method-Override üstbilgisini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b7844-152">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="b7844-153">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b7844-153">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="b7844-154">X-HTTP-Method-Override için destek ekleyen bir ileti işleyicisi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="b7844-154">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="b7844-155">İçinde **SendAsync** yöntemi, işleyici kontrol isteğine bir POST isteği olup ve X-HTTP-Method-Override üstbilgi içerip içermediğini.</span><span class="sxs-lookup"><span data-stu-id="b7844-155">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="b7844-156">Bu durumda, üstbilgi değeri doğrular ve ardından istek yöntemi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b7844-156">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="b7844-157">Son olarak, işleyici çağırır `base.SendAsync` iletiyi sonraki işleyicisine geçirilecek.</span><span class="sxs-lookup"><span data-stu-id="b7844-157">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="b7844-158">İstek ulaştığında **HttpControllerDispatcher** sınıfı **HttpControllerDispatcher** güncelleştirilmiş istek yöntemine dayalı isteği yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="b7844-158">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="b7844-159">Örnek: Bir özel yanıt üstbilgisi ekleme</span><span class="sxs-lookup"><span data-stu-id="b7844-159">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="b7844-160">Her yanıt iletisi için özel bir başlık ekler bir ileti işleyicisi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="b7844-160">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="b7844-161">İlk olarak, işleyici çağırır `base.SendAsync` iç ileti işleyicisi için isteği geçirilecek.</span><span class="sxs-lookup"><span data-stu-id="b7844-161">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="b7844-162">İç işleyici bir yanıt iletisi döndürür, ancak bu nedenle zaman uyumsuz olarak kullanarak yaptığı bir **görev&lt;T&gt;**  nesne.</span><span class="sxs-lookup"><span data-stu-id="b7844-162">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="b7844-163">Yanıt iletisi yüklenene kadar kullanılamaz `base.SendAsync` zaman uyumsuz olarak tamamlar.</span><span class="sxs-lookup"><span data-stu-id="b7844-163">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="b7844-164">Bu örnekte **await** işlerini yapmak için anahtar sözcüğü sonra zaman uyumsuz olarak `SendAsync` tamamlar.</span><span class="sxs-lookup"><span data-stu-id="b7844-164">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="b7844-165">.NET Framework 4.0 hedefliyorsanız kullanın **görev**&lt;T&gt;**. ContinueWith** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b7844-165">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="b7844-166">Örnek: Bir API anahtarı için denetimi</span><span class="sxs-lookup"><span data-stu-id="b7844-166">Example: Checking for an API Key</span></span>

<span data-ttu-id="b7844-167">Bazı web Hizmetleri, istemciler kendi istekte bir API anahtarı içerecek şekilde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b7844-167">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="b7844-168">Aşağıdaki örnek, bir ileti işleyicisi istekleri için geçerli bir API anahtarı nasıl denetleyebilirsiniz gösterir:</span><span class="sxs-lookup"><span data-stu-id="b7844-168">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="b7844-169">Bu işleyici, URI sorgu dizesinde API anahtarı arar.</span><span class="sxs-lookup"><span data-stu-id="b7844-169">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="b7844-170">(Bu örnekte, bir statik dize anahtar olduğunu varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="b7844-170">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="b7844-171">Gerçek bir uygulaması büyük olasılıkla çok daha karmaşık Doğrulamalar kullanmanız gerekir.) Sorgu dizesinin anahtar içeriyorsa, işleyici isteği iç işleyiciye geçirir.</span><span class="sxs-lookup"><span data-stu-id="b7844-171">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="b7844-172">İsteğin geçerli bir anahtar yoksa, işleyici durumu 403, bir yanıt iletisi oluşturur. Yasak.</span><span class="sxs-lookup"><span data-stu-id="b7844-172">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="b7844-173">Bu durumda, işleyici arama `base.SendAsync`, bu nedenle iç işleyici hiçbir zaman aldığı istek de denetleyicisi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="b7844-173">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="b7844-174">Bu nedenle, denetleyici gelen tüm istekleri için geçerli bir API anahtarı olduğunu varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7844-174">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="b7844-175">API anahtarı yalnızca belirli denetleyici eylemleri için geçerliyse, bir ileti işleyicisi yerine bir eyleme eylem filtresi kullanarak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b7844-175">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="b7844-176">Yönlendirme URI'si gerçekleştirildikten sonra eylem filtrelerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b7844-176">Action filters run after URI routing is performed.</span></span>


## <a name="per-route-message-handlers"></a><span data-ttu-id="b7844-177">Rota başına ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="b7844-177">Per-Route Message Handlers</span></span>

<span data-ttu-id="b7844-178">İşleyicileri **HttpConfiguration.MessageHandlers** koleksiyon genel olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b7844-178">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="b7844-179">Alternatif olarak, rota tanımlarken belirli bir yol için bir ileti işleyicisi ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b7844-179">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="b7844-180">İstek URI'si "Route2" eşleşiyorsa, bu örnekte, istek için gönderilen `MessageHandler2`.</span><span class="sxs-lookup"><span data-stu-id="b7844-180">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="b7844-181">Aşağıdaki diyagramda, bu iki yol için bir işlem hattı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b7844-181">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="b7844-182">Dikkat `MessageHandler2` varsayılan değiştirir **HttpControllerDispatcher**.</span><span class="sxs-lookup"><span data-stu-id="b7844-182">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="b7844-183">Bu örnekte, `MessageHandler2` yanıtı oluşturur ve "Route2" hiçbir zaman bir denetleyiciye Git eşleşen ister.</span><span class="sxs-lookup"><span data-stu-id="b7844-183">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="b7844-184">Bu, kendi özel uç nokta ile tüm Web API denetleyicisi mekanizması değiştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7844-184">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="b7844-185">Alternatif olarak, bir rota başına ileti işleyicisini temsil edebilir **HttpControllerDispatcher**, daha sonra bir denetleyiciye gönderir.</span><span class="sxs-lookup"><span data-stu-id="b7844-185">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="b7844-186">Aşağıdaki kod, bu rota yapılandırma işlemi gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b7844-186">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
