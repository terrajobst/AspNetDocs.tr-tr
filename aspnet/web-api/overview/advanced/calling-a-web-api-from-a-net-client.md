---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Bir .NET istemcisinden Web API'si çağırma (C#)-ASP.NET 4.x
author: MikeWasson
description: Bu öğreticide, bir .NET 4.x uygulamasından web API'si çağırma işlemi gösterilmektedir.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: ca3b9424f30f48c7b8c71b850ffeca64244b123b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112837"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="f289a-103">Bir .NET istemcisinden (C#) bir Web API'si çağırma</span><span class="sxs-lookup"><span data-stu-id="f289a-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="f289a-104">tarafından [Mike Wasson](https://github.com/MikeWasson) ve [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f289a-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f289a-105">[Tamamlanmış projeyi indirmek](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="f289a-105">[Download Completed Project](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="f289a-106">[Yükleme yönergeleri](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="f289a-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="f289a-107">Bu öğretici, bir .NET uygulamasından web API'si çağırma nasıl gösterir kullanarak [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="f289a-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="f289a-108">Bu öğreticide, aşağıdaki web API'si kullanan bir istemci uygulaması yazılır:</span><span class="sxs-lookup"><span data-stu-id="f289a-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="f289a-109">Eylem</span><span class="sxs-lookup"><span data-stu-id="f289a-109">Action</span></span> | <span data-ttu-id="f289a-110">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="f289a-110">HTTP method</span></span> | <span data-ttu-id="f289a-111">Göreli URI'si</span><span class="sxs-lookup"><span data-stu-id="f289a-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f289a-112">Bir ürün Kimliğine göre Al</span><span class="sxs-lookup"><span data-stu-id="f289a-112">Get a product by ID</span></span> | <span data-ttu-id="f289a-113">GET</span><span class="sxs-lookup"><span data-stu-id="f289a-113">GET</span></span> | <span data-ttu-id="f289a-114">/API'si/ürünler/*kimliği*</span><span class="sxs-lookup"><span data-stu-id="f289a-114">/api/products/*id*</span></span> |
| <span data-ttu-id="f289a-115">Yeni Ürün oluşturma</span><span class="sxs-lookup"><span data-stu-id="f289a-115">Create a new product</span></span> | <span data-ttu-id="f289a-116">POST</span><span class="sxs-lookup"><span data-stu-id="f289a-116">POST</span></span> | <span data-ttu-id="f289a-117">/ api/ürünleri</span><span class="sxs-lookup"><span data-stu-id="f289a-117">/api/products</span></span> |
| <span data-ttu-id="f289a-118">Bir ürün güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="f289a-118">Update a product</span></span> | <span data-ttu-id="f289a-119">PUT</span><span class="sxs-lookup"><span data-stu-id="f289a-119">PUT</span></span> | <span data-ttu-id="f289a-120">/API'si/ürünler/*kimliği*</span><span class="sxs-lookup"><span data-stu-id="f289a-120">/api/products/*id*</span></span> |
| <span data-ttu-id="f289a-121">Bir ürün Sil</span><span class="sxs-lookup"><span data-stu-id="f289a-121">Delete a product</span></span> | <span data-ttu-id="f289a-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="f289a-122">DELETE</span></span> | <span data-ttu-id="f289a-123">/API'si/ürünler/*kimliği*</span><span class="sxs-lookup"><span data-stu-id="f289a-123">/api/products/*id*</span></span> |

<span data-ttu-id="f289a-124">Bu API ile ASP.NET Web API'si uygulama hakkında bilgi edinmek için bkz: [bu destekler CRUD işlemleri bir Web API'si oluşturma](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="f289a-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="f289a-125">Kolaylık olması için istemci uygulaması Bu öğreticide bir Windows konsol uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f289a-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="f289a-126">**HttpClient** Windows Phone ve Windows Store uygulamaları için de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f289a-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="f289a-127">Daha fazla bilgi için [yazma Web API İstemci kodu birden çok platformları kullanarak taşınabilir kitaplıklar için](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="f289a-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="f289a-128">Konsol uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="f289a-128">Create the Console Application</span></span>

<span data-ttu-id="f289a-129">Visual Studio'da adlı yeni bir Windows konsol uygulaması oluşturma **HttpClientSample** ve aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="f289a-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="f289a-130">Yukarıdaki kod tam istemci uygulaması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f289a-130">The preceding code is the complete client app.</span></span>

<span data-ttu-id="f289a-131">`RunAsync` çalıştırır ve işlem tamamlanana kadar engeller.</span><span class="sxs-lookup"><span data-stu-id="f289a-131">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="f289a-132">Çoğu **HttpClient** yöntemlerdir zaman uyumsuz, bunların ağ g/ç gerçekleştirdiğinden.</span><span class="sxs-lookup"><span data-stu-id="f289a-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="f289a-133">Zaman uyumsuz görevlerin tümünü içinde yapılır `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="f289a-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="f289a-134">Bir uygulama ana iş parçacığı normalde engellemez, ancak bu uygulama etkileşimi izin vermez.</span><span class="sxs-lookup"><span data-stu-id="f289a-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="f289a-135">Web API İstemci kitaplıklarını yükleme</span><span class="sxs-lookup"><span data-stu-id="f289a-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="f289a-136">NuGet paketi Web API İstemci kitaplıkları paketini yüklemek için Yöneticisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="f289a-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="f289a-137">Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="f289a-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="f289a-138">Paket Yöneticisi Konsolu (PMC'de), aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="f289a-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="f289a-139">Önceki komutta aşağıdaki NuGet paketleri projeye ekler:</span><span class="sxs-lookup"><span data-stu-id="f289a-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="f289a-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="f289a-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="f289a-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="f289a-141">Newtonsoft.Json</span></span>

<span data-ttu-id="f289a-142">Json.NET, .NET için popüler bir yüksek performanslı JSON çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="f289a-142">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="f289a-143">Bir Model sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="f289a-143">Add a Model Class</span></span>

<span data-ttu-id="f289a-144">İnceleme `Product` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="f289a-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="f289a-145">Bu sınıf, web API'si tarafından kullanılan veri modeli ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="f289a-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="f289a-146">Bir uygulama kullanabilirsiniz **HttpClient** okumak için bir `Product` bir HTTP yanıt örneği.</span><span class="sxs-lookup"><span data-stu-id="f289a-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="f289a-147">Uygulama seri durumundan çıkarma kod yazmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f289a-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="f289a-148">Oluşturma ve HttpClient başlatma</span><span class="sxs-lookup"><span data-stu-id="f289a-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="f289a-149">Statik inceleyin **HttpClient** özelliği:</span><span class="sxs-lookup"><span data-stu-id="f289a-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="f289a-150">**HttpClient** kez oluşturulacak hedeflenen ve bir uygulamanın ömrü yeniden.</span><span class="sxs-lookup"><span data-stu-id="f289a-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="f289a-151">Aşağıdaki koşullar sonuçlanabilir **SocketException** hataları:</span><span class="sxs-lookup"><span data-stu-id="f289a-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="f289a-152">Yeni bir oluşturma **HttpClient** istek başına örnek.</span><span class="sxs-lookup"><span data-stu-id="f289a-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="f289a-153">Ağır yük altında sunucu.</span><span class="sxs-lookup"><span data-stu-id="f289a-153">Server under heavy load.</span></span>

<span data-ttu-id="f289a-154">Yeni bir oluşturma **HttpClient** istek başına örnek kullanılabilir yuva tüketebilir.</span><span class="sxs-lookup"><span data-stu-id="f289a-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="f289a-155">Aşağıdaki kod başlatır **HttpClient** örneği:</span><span class="sxs-lookup"><span data-stu-id="f289a-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="f289a-156">Yukarıdaki kod:</span><span class="sxs-lookup"><span data-stu-id="f289a-156">The preceding code:</span></span>

* <span data-ttu-id="f289a-157">Taban URI HTTP istekleri için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f289a-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="f289a-158">Sunucu uygulamasında kullanılan bağlantı noktası için bağlantı noktası numarasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f289a-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="f289a-159">Uygulama bağlantı noktası sunucu uygulaması için kullanıldıkları sürece çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f289a-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="f289a-160">"Application/json" için Accept üstbilgisini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f289a-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="f289a-161">Bu üst bilgi ayarlama, JSON biçiminde veri göndermek sunucuyı söyler.</span><span class="sxs-lookup"><span data-stu-id="f289a-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="f289a-162">Kaynak almak için bir GET isteği gönder</span><span class="sxs-lookup"><span data-stu-id="f289a-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="f289a-163">Aşağıdaki kod, bir ürün için bir GET isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="f289a-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="f289a-164">**GetAsync** yöntem, HTTP GET isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="f289a-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="f289a-165">Yöntemi tamamlandığında döndürür bir **HttpResponseMessage** , HTTP yanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="f289a-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="f289a-166">Yanıt durum kodu bir başarı kodu ise yanıt gövdesi bir ürün JSON gösterimini içerir.</span><span class="sxs-lookup"><span data-stu-id="f289a-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="f289a-167">Çağrı **ReadAsAsync** JSON yükü için seri durumdan çıkarılacak bir `Product` örneği.</span><span class="sxs-lookup"><span data-stu-id="f289a-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="f289a-168">**ReadAsAsync** yanıt gövdesi büyük olabileceğinden yöntemi zaman uyumsuz.</span><span class="sxs-lookup"><span data-stu-id="f289a-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="f289a-169">**HttpClient** HTTP yanıtı bir hata kodu içeriyorsa bir özel durum oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="f289a-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="f289a-170">Bunun yerine, **IsSuccessStatusCode** özelliği **false** durum bir hata kodu ise.</span><span class="sxs-lookup"><span data-stu-id="f289a-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="f289a-171">HTTP hata kodları özel durumlar olarak değerlendirilecek tercih ederseniz, çağrı [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) yanıt nesnesinde.</span><span class="sxs-lookup"><span data-stu-id="f289a-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="f289a-172">`EnsureSuccessStatusCode` Durum kodu 200 aralığın dışında kalan bir özel durum oluşturur&ndash;299.</span><span class="sxs-lookup"><span data-stu-id="f289a-172">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="f289a-173">Unutmayın **HttpClient** diğer nedenlerle özel durumlar oluşturabilecek &mdash; Örneğin, istek zaman aşımına uğrar.</span><span class="sxs-lookup"><span data-stu-id="f289a-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="f289a-174">Medya türü Biçimlendiricileri serisini kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="f289a-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="f289a-175">Zaman **ReadAsAsync** çağrılır hiçbir parametre olmadan varsayılan kullandığı *medya biçimlendiricileri* yanıt gövdesini okumak için.</span><span class="sxs-lookup"><span data-stu-id="f289a-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="f289a-176">Varsayılan biçimlendiricileri JSON, XML ve formu url kodlanmış verileri destekler.</span><span class="sxs-lookup"><span data-stu-id="f289a-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="f289a-177">Varsayılan biçimlendiricileri kullanmak yerine, için biçimlendiricileri listesi sağlayabilirsiniz **ReadAsAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f289a-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="f289a-178">Biçimlendiricileri listesi kullanarak bir özel medya türü biçimlendiricisi varsa yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="f289a-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="f289a-179">Daha fazla bilgi için [ASP.NET Web API 2'deki medya Biçimlendiricileri](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="f289a-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="f289a-180">Bir kaynak oluşturmak için bir POST isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="f289a-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="f289a-181">Aşağıdaki kodu içeren bir POST isteği gönderir. bir `Product` JSON biçimindeki örneği:</span><span class="sxs-lookup"><span data-stu-id="f289a-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="f289a-182">**PostAsJsonAsync** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="f289a-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="f289a-183">Bir nesne json'a seri hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f289a-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="f289a-184">JSON yükü bir POST isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="f289a-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="f289a-185">İstek başarılı olursa:</span><span class="sxs-lookup"><span data-stu-id="f289a-185">If the request succeeds:</span></span>

* <span data-ttu-id="f289a-186">201 (oluşturuldu) yanıt döndürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f289a-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="f289a-187">Yanıt URL'si oluşturulan kaynakların konumu üst bilgisini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="f289a-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="f289a-188">Bir kaynağı güncelleştirmek için PUT isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="f289a-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="f289a-189">Aşağıdaki kod, bir ürünü güncelleştirmek için PUT İsteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="f289a-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="f289a-190">**PutAsJsonAsync** yöntem çalışır gibi **PostAsJsonAsync**dışında posta yerine bir PUT İsteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="f289a-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="f289a-191">Bir kaynağı silmek için bir silme isteği gönderiliyor</span><span class="sxs-lookup"><span data-stu-id="f289a-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="f289a-192">Aşağıdaki kod, bir ürünü silmek için bir silme isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="f289a-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="f289a-193">GET gibi bir istek gövdesi bir silme isteği yok.</span><span class="sxs-lookup"><span data-stu-id="f289a-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="f289a-194">DELETE ile JSON veya XML biçiminde belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f289a-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="f289a-195">Örnek test</span><span class="sxs-lookup"><span data-stu-id="f289a-195">Test the sample</span></span>

<span data-ttu-id="f289a-196">İstemci uygulamayı test etmek için:</span><span class="sxs-lookup"><span data-stu-id="f289a-196">To test the client app:</span></span>

1. <span data-ttu-id="f289a-197">[İndirme](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) ve sunucu uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f289a-197">[Download](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="f289a-198">[Yükleme yönergeleri](/aspnet/core/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="f289a-198">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="f289a-199">Sunucu uygulamasının çalıştığı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f289a-199">Verify the server app is working.</span></span> <span data-ttu-id="f289a-200">Örneğin, `http://localhost:64195/api/products` ürünlerin listesini döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="f289a-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="f289a-201">HTTP isteklerini temel URI'sini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f289a-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="f289a-202">Sunucu uygulamasında kullanılan bağlantı noktası için bağlantı noktası numarasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f289a-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="f289a-203">İstemci uygulaması çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f289a-203">Run the client app.</span></span> <span data-ttu-id="f289a-204">Aşağıdaki çıkış üretilir:</span><span class="sxs-lookup"><span data-stu-id="f289a-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
