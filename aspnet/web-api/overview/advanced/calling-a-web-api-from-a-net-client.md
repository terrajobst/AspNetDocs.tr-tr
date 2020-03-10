---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET Istemcisinden bir Web API 'SI çağırma (C#)-ASP.NET 4. x
author: MikeWasson
description: Bu öğreticide, bir .NET 4. x uygulamasından bir Web API 'sinin nasıl çağrılacağını gösterilmektedir.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: ab3ba71839123e848dffaa59871f9dac8c1a88d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622621"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="0c8a2-103">.NET Istemcisinden bir Web API 'SI çağırma (C#)</span><span class="sxs-lookup"><span data-stu-id="0c8a2-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="0c8a2-104">, [Mike, son](https://github.com/MikeWasson) ve [Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="0c8a2-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0c8a2-105">[Tamamlanmış projeyi indirin](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="0c8a2-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="0c8a2-106">[Yönergeleri indirin](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="0c8a2-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="0c8a2-107">Bu öğreticide, [System .net. http. HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) kullanılarak .NET uygulamasından BIR Web API 'sinin nasıl çağrılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="0c8a2-108">Bu öğreticide, aşağıdaki Web API 'sini tüketen bir istemci uygulaması yazılmıştır:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="0c8a2-109">Eylem</span><span class="sxs-lookup"><span data-stu-id="0c8a2-109">Action</span></span> | <span data-ttu-id="0c8a2-110">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="0c8a2-110">HTTP method</span></span> | <span data-ttu-id="0c8a2-111">Göreli URI'si</span><span class="sxs-lookup"><span data-stu-id="0c8a2-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c8a2-112">KIMLIĞE göre ürün al</span><span class="sxs-lookup"><span data-stu-id="0c8a2-112">Get a product by ID</span></span> | <span data-ttu-id="0c8a2-113">GET</span><span class="sxs-lookup"><span data-stu-id="0c8a2-113">GET</span></span> | <span data-ttu-id="0c8a2-114">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="0c8a2-114">/api/products/*id*</span></span> |
| <span data-ttu-id="0c8a2-115">Yeni ürün oluştur</span><span class="sxs-lookup"><span data-stu-id="0c8a2-115">Create a new product</span></span> | <span data-ttu-id="0c8a2-116">POST</span><span class="sxs-lookup"><span data-stu-id="0c8a2-116">POST</span></span> | <span data-ttu-id="0c8a2-117">/api/Products</span><span class="sxs-lookup"><span data-stu-id="0c8a2-117">/api/products</span></span> |
| <span data-ttu-id="0c8a2-118">Bir ürünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0c8a2-118">Update a product</span></span> | <span data-ttu-id="0c8a2-119">PUT</span><span class="sxs-lookup"><span data-stu-id="0c8a2-119">PUT</span></span> | <span data-ttu-id="0c8a2-120">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="0c8a2-120">/api/products/*id*</span></span> |
| <span data-ttu-id="0c8a2-121">Bir ürünü silme</span><span class="sxs-lookup"><span data-stu-id="0c8a2-121">Delete a product</span></span> | <span data-ttu-id="0c8a2-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="0c8a2-122">DELETE</span></span> | <span data-ttu-id="0c8a2-123">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="0c8a2-123">/api/products/*id*</span></span> |

<span data-ttu-id="0c8a2-124">Bu API 'yi ASP.NET Web API 'SI ile nasıl uygulayacağınızı öğrenmek için bkz. [CRUD Işlemlerini destekleyen bir Web API 'Si oluşturma](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="0c8a2-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="0c8a2-125">Kolaylık olması için, bu öğreticideki istemci uygulaması bir Windows konsol uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="0c8a2-126">**HttpClient** , Windows Phone ve Windows Mağazası uygulamaları için de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="0c8a2-127">Daha fazla bilgi için bkz. [Taşınabilir kitaplıkları kullanarak birden çok platform Için Web API Istemci kodu yazma](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="0c8a2-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="0c8a2-128">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c8a2-128">Create the Console Application</span></span>

<span data-ttu-id="0c8a2-129">Visual Studio 'da **Httpclientsample** adlı yeni bir Windows konsol uygulaması oluşturun ve aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="0c8a2-130">Yukarıdaki kod, tüm istemci uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-130">The preceding code is the complete client app.</span></span>

<span data-ttu-id="0c8a2-131">`RunAsync` çalışır ve bloklar tamamlanana kadar engeller.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-131">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="0c8a2-132">Ağ g/ç gerçekleştirdiklerinden, çoğu **HttpClient** yöntemi zaman uyumsuz.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="0c8a2-133">Tüm zaman uyumsuz görevler `RunAsync`içinde yapılır.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="0c8a2-134">Normalde bir uygulama ana iş parçacığını engellemez, ancak bu uygulama hiçbir etkileşime izin vermez.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="0c8a2-135">Web API Istemci kitaplıklarını yükler</span><span class="sxs-lookup"><span data-stu-id="0c8a2-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="0c8a2-136">Web API Istemci kitaplıkları paketini yüklemek için NuGet Paket Yöneticisi 'Ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="0c8a2-137">**Araçlar** menüsünde **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="0c8a2-138">Paket Yöneticisi konsolunda (PMC), aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="0c8a2-139">Yukarıdaki komut, projeye aşağıdaki NuGet paketlerini ekler:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="0c8a2-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="0c8a2-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="0c8a2-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="0c8a2-141">Newtonsoft.Json</span></span>

<span data-ttu-id="0c8a2-142">Netmerak Soft. JSON (Json.NET olarak da bilinir), .NET için popüler bir yüksek performanslı JSON çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-142">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="0c8a2-143">Model sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="0c8a2-143">Add a Model Class</span></span>

<span data-ttu-id="0c8a2-144">`Product` sınıfını inceleyin:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="0c8a2-145">Bu sınıf, Web API 'SI tarafından kullanılan veri modeliyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="0c8a2-146">Bir uygulama, HTTP yanıtından bir `Product` örneğini okumak için **HttpClient** kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="0c8a2-147">Uygulamanın seri durumdan çıkarma kodu yazmak zorunda değildir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="0c8a2-148">HttpClient oluşturma ve başlatma</span><span class="sxs-lookup"><span data-stu-id="0c8a2-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="0c8a2-149">Statik **HttpClient** özelliğini inceleyin:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="0c8a2-150">**HttpClient** uygulamasının bir kez oluşturulması ve bir uygulamanın ömrü boyunca yeniden kullanılması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="0c8a2-151">Aşağıdaki koşullar, **SocketException** hatalarına neden olabilir:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="0c8a2-152">İstek başına yeni bir **HttpClient** örneği oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="0c8a2-153">Sunucu ağır yük altında.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-153">Server under heavy load.</span></span>

<span data-ttu-id="0c8a2-154">Her istek için yeni bir **HttpClient** örneği oluşturulması, kullanılabilir yuvaları tüketebilir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="0c8a2-155">Aşağıdaki kod, **HttpClient** örneğini başlatır:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="0c8a2-156">Yukarıdaki kod:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-156">The preceding code:</span></span>

* <span data-ttu-id="0c8a2-157">HTTP istekleri için temel URI 'yi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="0c8a2-158">Bağlantı noktası numarasını sunucu uygulamasında kullanılan bağlantı noktasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="0c8a2-159">Sunucu uygulaması için bağlantı noktası kullanılmadığı takdirde uygulama çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="0c8a2-160">Accept üst bilgisini "Application/JSON" olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="0c8a2-161">Bu üst bilgiyi ayarlamak, sunucuya verileri JSON biçiminde göndermesini söyler.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="0c8a2-162">Kaynak almak için GET isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="0c8a2-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="0c8a2-163">Aşağıdaki kod, bir ürün için GET isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="0c8a2-164">**GetAsync** YÖNTEMI http get isteğini gönderir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="0c8a2-165">Yöntem tamamlandığında, HTTP yanıtını içeren bir **HttpResponseMessage** döndürür.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="0c8a2-166">Yanıttaki durum kodu bir başarı kodu ise, yanıt gövdesi bir ürünün JSON gösterimini içerir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="0c8a2-167">JSON yükünün `Product` örneğine serisini kaldırmak için **Readasasync** çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="0c8a2-168">Yanıt gövdesi çok büyük olabileceğinden **Readasasync** yöntemi zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="0c8a2-169">HTTP yanıtı bir hata kodu içerdiğinde **HttpClient** bir özel durum oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="0c8a2-170">Bunun yerine, durum bir hata kodu ise **IsSuccessStatusCode** özelliği **false 'tur** .</span><span class="sxs-lookup"><span data-stu-id="0c8a2-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="0c8a2-171">HTTP hata kodlarını özel durumlar olarak kabul etmek isterseniz, yanıt nesnesinde [HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="0c8a2-172">`EnsureSuccessStatusCode` durum kodu 200&ndash;299 aralığının dışında kalırsa bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-172">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="0c8a2-173">**HttpClient** 'ın, istek zaman aşımına uğrarsa başka nedenlerle &mdash; özel durumlar oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="0c8a2-174">Seri durumdan çıkarılacak medya türü Formatlayıcıları</span><span class="sxs-lookup"><span data-stu-id="0c8a2-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="0c8a2-175">**Readasasync** parametresi olmadan çağrıldığında, yanıt gövdesini okumak için varsayılan *medya formatlayıcıları* kümesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="0c8a2-176">Varsayılan biçim JSON, XML ve form-URL kodlamalı verileri destekler.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="0c8a2-177">Varsayılan biçimleri kullanmak yerine, **Readasasync** yöntemine bir formatınters listesi sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="0c8a2-178">Özel bir medya türü biçimlendirici varsa, bir biçim listesinin kullanılması yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="0c8a2-179">Daha fazla bilgi için bkz. [ASP.NET Web API 2 ' de medya biçimleri](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="0c8a2-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="0c8a2-180">Kaynak oluşturmak için POST Isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="0c8a2-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="0c8a2-181">Aşağıdaki kod, JSON biçiminde bir `Product` örneği içeren bir POST isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="0c8a2-182">**Postasjsonasync** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="0c8a2-183">Bir nesneyi JSON 'a dizleştirir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="0c8a2-184">JSON yükünü bir POST isteğinde gönderir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="0c8a2-185">İstek başarılı olursa:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-185">If the request succeeds:</span></span>

* <span data-ttu-id="0c8a2-186">Bu, 201 (oluşturulan) yanıtı döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="0c8a2-187">Yanıt, konum üstbilgisindeki oluşturulan kaynakların URL 'sini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="0c8a2-188">Bir kaynağı güncelleştirmek için PUT Isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="0c8a2-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="0c8a2-189">Aşağıdaki kod bir ürünü güncelleştirmek için bir PUT isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="0c8a2-190">**Putasjsonasync** yöntemi, post yerıne bir PUT isteği göndermesi dışında, **postasjsonasync**yöntemi gibi çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="0c8a2-191">Bir kaynağı silmek için SILME Isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="0c8a2-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="0c8a2-192">Aşağıdaki kod, bir ürünü silmek için bir SILME isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="0c8a2-193">GET gibi, bir DELETE isteğinin bir istek gövdesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="0c8a2-194">DELETE ile JSON veya XML biçimi belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="0c8a2-195">Örneği test etme</span><span class="sxs-lookup"><span data-stu-id="0c8a2-195">Test the sample</span></span>

<span data-ttu-id="0c8a2-196">İstemci uygulamasını test etmek için:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-196">To test the client app:</span></span>

1. <span data-ttu-id="0c8a2-197">Sunucu uygulamasını [indirip](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-197">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="0c8a2-198">[Yönergeleri indirin](/aspnet/core/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="0c8a2-198">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="0c8a2-199">Sunucu uygulamasının çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-199">Verify the server app is working.</span></span> <span data-ttu-id="0c8a2-200">Örneğin, `http://localhost:64195/api/products` ürünlerin bir listesini döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="0c8a2-201">HTTP istekleri için temel URI 'yi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="0c8a2-202">Bağlantı noktası numarasını sunucu uygulamasında kullanılan bağlantı noktasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="0c8a2-203">İstemci uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0c8a2-203">Run the client app.</span></span> <span data-ttu-id="0c8a2-204">Aşağıdaki çıktı üretilir:</span><span class="sxs-lookup"><span data-stu-id="0c8a2-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
