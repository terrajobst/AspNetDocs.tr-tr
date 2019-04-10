---
uid: web-api/overview/advanced/http-message-handlers
title: HTTP ileti işleyicileri ASP.NET Web API'si - ASP.NET 4.x
author: MikeWasson
description: ASP.NET, ASP.NET Web API HTTP ileti işleyicileri genel bir bakış 4.x
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 308d2e3dd21917e7656f7ffe889dc965d9275d74
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392112"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="40e11-103">ASP.NET Web API HTTP ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="40e11-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="40e11-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="40e11-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="40e11-105">A *ileti işleyicisi* HTTP isteği aldığında ve bir HTTP yanıtı döndüren bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="40e11-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="40e11-106">İleti işleyicileri türetilen Özet **HttpMessageHandler** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="40e11-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="40e11-107">Genellikle, bir dizi ileti işleyicileri zincirleme birlikte.</span><span class="sxs-lookup"><span data-stu-id="40e11-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="40e11-108">İlk işleyici HTTP isteği aldığında, işlem yapar ve bir sonraki işleyici istek sağlar.</span><span class="sxs-lookup"><span data-stu-id="40e11-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="40e11-109">Belirli bir noktada yanıt oluşturulur ve zincirinde döner.</span><span class="sxs-lookup"><span data-stu-id="40e11-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="40e11-110">Bu düzen adı verilen bir *temsilci olarak görevlendirme* işleyici.</span><span class="sxs-lookup"><span data-stu-id="40e11-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="40e11-111">Sunucu tarafı ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="40e11-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="40e11-112">Sunucu tarafında, Web API ardışık düzeni bazı yerleşik ileti işleyicileri kullanır:</span><span class="sxs-lookup"><span data-stu-id="40e11-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="40e11-113">**HttpServer** istek ana bilgisayarından alır.</span><span class="sxs-lookup"><span data-stu-id="40e11-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="40e11-114">**HttpRoutingDispatcher** yola göre isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="40e11-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="40e11-115">**HttpControllerDispatcher** bir Web API denetleyicisine istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="40e11-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="40e11-116">İşlem hattı için özel işleyicileri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40e11-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="40e11-117">İleti işleyicileri, HTTP iletileri (yerine denetleyici eylemleri) düzeyinde çalışan çapraz kesme konuları için uygundur.</span><span class="sxs-lookup"><span data-stu-id="40e11-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="40e11-118">Örneğin, bir ileti işleyicisi olabilir:</span><span class="sxs-lookup"><span data-stu-id="40e11-118">For example, a message handler might:</span></span>

- <span data-ttu-id="40e11-119">Okuma veya istek üst bilgilerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="40e11-119">Read or modify request headers.</span></span>
- <span data-ttu-id="40e11-120">Yanıt üst bilgisi yanıtlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="40e11-120">Add a response header to responses.</span></span>
- <span data-ttu-id="40e11-121">Denetleyici ulaşmadan önce istekleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="40e11-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="40e11-122">Bu diyagramda, ardışık düzende eklenen iki özel işleyicileri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="40e11-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="40e11-123">İstemci tarafında HttpClient ileti işleyicileri de kullanır.</span><span class="sxs-lookup"><span data-stu-id="40e11-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="40e11-124">Daha fazla bilgi için [HttpClient ileti işleyicileri](httpclient-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="40e11-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="40e11-125">Özel ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="40e11-125">Custom Message Handlers</span></span>

<span data-ttu-id="40e11-126">Özel ileti işleyicisi yazmak için türetilen **System.Net.Http.DelegatingHandler** ve geçersiz kılma **SendAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="40e11-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="40e11-127">Bu yöntem, aşağıdaki imzası vardır:</span><span class="sxs-lookup"><span data-stu-id="40e11-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="40e11-128">Yöntem alır bir **HttpRequestMessage** giriş ve zaman uyumsuz olarak döndürür olarak bir **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="40e11-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="40e11-129">Tipik bir uygulaması şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="40e11-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="40e11-130">İşlem istek iletisi.</span><span class="sxs-lookup"><span data-stu-id="40e11-130">Process the request message.</span></span>
2. <span data-ttu-id="40e11-131">Çağrı `base.SendAsync` iç işleyici için istek gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40e11-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="40e11-132">İç işleyici, bir yanıt iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="40e11-132">The inner handler returns a response message.</span></span> <span data-ttu-id="40e11-133">(Bu adım, zaman uyumsuz.)</span><span class="sxs-lookup"><span data-stu-id="40e11-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="40e11-134">Yanıta işlemek ve çağırana döndürmesi.</span><span class="sxs-lookup"><span data-stu-id="40e11-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="40e11-135">Önemsiz bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="40e11-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="40e11-136">Çağrı `base.SendAsync` zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="40e11-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="40e11-137">İşleyici, bu çağrıdan sonra herhangi bir iş varsa, kullanmak **await** gösterildiği gibi anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="40e11-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>


<span data-ttu-id="40e11-138">Bir temsilci işleyicisi, ayrıca iç işleyici atlamak ve doğrudan yanıt oluşturun:</span><span class="sxs-lookup"><span data-stu-id="40e11-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="40e11-139">Bir temsilci işleyicisi çağırmadan yanıtı oluşturur `base.SendAsync`, rest işlem hattının istek atlar.</span><span class="sxs-lookup"><span data-stu-id="40e11-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="40e11-140">(Bir hata yanıtı oluşturma) istek doğrulama için bir işleyici yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="40e11-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="40e11-141">İşlem hattı için bir işleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="40e11-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="40e11-142">Sunucu tarafında bir ileti işleyicisi eklemek için ekleyebilirsiniz **HttpConfiguration.MessageHandlers** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="40e11-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="40e11-143">Projeyi oluşturmak için "ASP.NET MVC 4 Web uygulaması" şablonunu kullandıysanız, bu iç yapabileceğiniz **WebApiConfig** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="40e11-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="40e11-144">İleti işleyicileri görünürler aynı sırayla çağrılır **MessageHandlers** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="40e11-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="40e11-145">Yanıt iletisi içe yer olduğundan, diğer yönde hareket eder.</span><span class="sxs-lookup"><span data-stu-id="40e11-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="40e11-146">Diğer bir deyişle, son ilk yanıt iletisi işleyicidir.</span><span class="sxs-lookup"><span data-stu-id="40e11-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="40e11-147">İç işleyicileri ayarlamanız gerekmez dikkat edin. Web API çerçevesi, ileti işleyicileri otomatik olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="40e11-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="40e11-148">Eğer [kendi kendine barındırma](../older-versions/self-host-a-web-api.md), bir örneğini oluşturmak **HttpSelfHostConfiguration** sınıfı ve işleyicileri ekleyin **MessageHandlers** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="40e11-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="40e11-149">Artık özel ileti işleyicileri bazı örneklere bakalım.</span><span class="sxs-lookup"><span data-stu-id="40e11-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="40e11-150">Örnek: X-HTTP-yöntemi-geçersiz kıl</span><span class="sxs-lookup"><span data-stu-id="40e11-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="40e11-151">Standart olmayan bir HTTP üst bilgisi X-HTTP-Method-Override ' dir.</span><span class="sxs-lookup"><span data-stu-id="40e11-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="40e11-152">PUT veya silme gibi belirli HTTP istek türlerini gönderilemiyor istemciler için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="40e11-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="40e11-153">Bunun yerine, istemci bir POST isteği gönderir ve istenen yöntemin X-HTTP-Method-Override üstbilgisini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="40e11-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="40e11-154">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="40e11-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="40e11-155">X-HTTP-Method-Override için destek ekleyen bir ileti işleyicisi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="40e11-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="40e11-156">İçinde **SendAsync** yöntemi, işleyici kontrol isteğine bir POST isteği olup ve X-HTTP-Method-Override üstbilgi içerip içermediğini.</span><span class="sxs-lookup"><span data-stu-id="40e11-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="40e11-157">Bu durumda, üstbilgi değeri doğrular ve ardından istek yöntemi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="40e11-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="40e11-158">Son olarak, işleyici çağırır `base.SendAsync` iletiyi sonraki işleyicisine geçirilecek.</span><span class="sxs-lookup"><span data-stu-id="40e11-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="40e11-159">İstek ulaştığında **HttpControllerDispatcher** sınıfı **HttpControllerDispatcher** güncelleştirilmiş istek yöntemine dayalı isteği yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="40e11-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="40e11-160">Örnek: Bir özel yanıt üstbilgisi ekleme</span><span class="sxs-lookup"><span data-stu-id="40e11-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="40e11-161">Her yanıt iletisi için özel bir başlık ekler bir ileti işleyicisi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="40e11-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="40e11-162">İlk olarak, işleyici çağırır `base.SendAsync` iç ileti işleyicisi için isteği geçirilecek.</span><span class="sxs-lookup"><span data-stu-id="40e11-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="40e11-163">İç işleyici bir yanıt iletisi döndürür, ancak bu nedenle zaman uyumsuz olarak kullanarak yaptığı bir **görev&lt;T&gt;**  nesne.</span><span class="sxs-lookup"><span data-stu-id="40e11-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="40e11-164">Yanıt iletisi yüklenene kadar kullanılamaz `base.SendAsync` zaman uyumsuz olarak tamamlar.</span><span class="sxs-lookup"><span data-stu-id="40e11-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="40e11-165">Bu örnekte **await** işlerini yapmak için anahtar sözcüğü sonra zaman uyumsuz olarak `SendAsync` tamamlar.</span><span class="sxs-lookup"><span data-stu-id="40e11-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="40e11-166">.NET Framework 4.0 hedefliyorsanız kullanın **görev**&lt;T&gt;**. ContinueWith** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="40e11-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="40e11-167">Örnek: Bir API anahtarı için denetimi</span><span class="sxs-lookup"><span data-stu-id="40e11-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="40e11-168">Bazı web Hizmetleri, istemciler kendi istekte bir API anahtarı içerecek şekilde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="40e11-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="40e11-169">Aşağıdaki örnek, bir ileti işleyicisi istekleri için geçerli bir API anahtarı nasıl denetleyebilirsiniz gösterir:</span><span class="sxs-lookup"><span data-stu-id="40e11-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="40e11-170">Bu işleyici, URI sorgu dizesinde API anahtarı arar.</span><span class="sxs-lookup"><span data-stu-id="40e11-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="40e11-171">(Bu örnekte, bir statik dize anahtar olduğunu varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="40e11-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="40e11-172">Gerçek bir uygulaması büyük olasılıkla çok daha karmaşık Doğrulamalar kullanmanız gerekir.) Sorgu dizesinin anahtar içeriyorsa, işleyici isteği iç işleyiciye geçirir.</span><span class="sxs-lookup"><span data-stu-id="40e11-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="40e11-173">İsteğin geçerli bir anahtar yoksa, işleyici durumu 403, bir yanıt iletisi oluşturur. Yasak.</span><span class="sxs-lookup"><span data-stu-id="40e11-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="40e11-174">Bu durumda, işleyici arama `base.SendAsync`, bu nedenle iç işleyici hiçbir zaman aldığı istek de denetleyicisi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="40e11-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="40e11-175">Bu nedenle, denetleyici gelen tüm istekleri için geçerli bir API anahtarı olduğunu varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40e11-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="40e11-176">API anahtarı yalnızca belirli denetleyici eylemleri için geçerliyse, bir ileti işleyicisi yerine bir eyleme eylem filtresi kullanarak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="40e11-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="40e11-177">Yönlendirme URI'si gerçekleştirildikten sonra eylem filtrelerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="40e11-177">Action filters run after URI routing is performed.</span></span>


## <a name="per-route-message-handlers"></a><span data-ttu-id="40e11-178">Rota başına ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="40e11-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="40e11-179">İşleyicileri **HttpConfiguration.MessageHandlers** koleksiyon genel olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="40e11-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="40e11-180">Alternatif olarak, rota tanımlarken belirli bir yol için bir ileti işleyicisi ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="40e11-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="40e11-181">İstek URI'si "Route2" eşleşiyorsa, bu örnekte, istek için gönderilen `MessageHandler2`.</span><span class="sxs-lookup"><span data-stu-id="40e11-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="40e11-182">Aşağıdaki diyagramda, bu iki yol için bir işlem hattı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="40e11-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="40e11-183">Dikkat `MessageHandler2` varsayılan değiştirir **HttpControllerDispatcher**.</span><span class="sxs-lookup"><span data-stu-id="40e11-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="40e11-184">Bu örnekte, `MessageHandler2` yanıtı oluşturur ve "Route2" hiçbir zaman bir denetleyiciye Git eşleşen ister.</span><span class="sxs-lookup"><span data-stu-id="40e11-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="40e11-185">Bu, kendi özel uç nokta ile tüm Web API denetleyicisi mekanizması değiştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="40e11-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="40e11-186">Alternatif olarak, bir rota başına ileti işleyicisini temsil edebilir **HttpControllerDispatcher**, daha sonra bir denetleyiciye gönderir.</span><span class="sxs-lookup"><span data-stu-id="40e11-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="40e11-187">Aşağıdaki kod, bu rota yapılandırma işlemi gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="40e11-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
