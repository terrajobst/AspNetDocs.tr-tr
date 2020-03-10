---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2 ' deki birim testi denetleyicileri | Microsoft Docs
author: MikeWasson
description: Bu konuda, Web API 2 ' deki birim testi denetleyicileri için bazı özel teknikler açıklanmaktadır. Bu konuyu okumadan önce öğretici birimini okumak isteyebilirsiniz...
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: cdb1700537021e276669de1a9e0330a62659746c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554994"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="d6245-104">ASP.NET Web API 2’deki Birim Testi Denetleyicileri</span><span class="sxs-lookup"><span data-stu-id="d6245-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>

<span data-ttu-id="d6245-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d6245-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="d6245-106">Bu konuda, Web API 2 ' deki birim testi denetleyicileri için bazı özel teknikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d6245-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="d6245-107">Bu konuyu okumadan önce, çözümünüze bir birim testi projesinin nasıl ekleneceğini gösteren [ASP.NET Web API 2 öğretici birim testini](unit-testing-with-aspnet-web-api.md)okumak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6245-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d6245-108">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="d6245-108">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="d6245-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d6245-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="d6245-110">Web API 2</span><span class="sxs-lookup"><span data-stu-id="d6245-110">Web API 2</span></span>
> - <span data-ttu-id="d6245-111">[Moq](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="d6245-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="d6245-112">Moq kullandım, ancak aynı fikir herhangi bir sahte işlem çerçevesi için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d6245-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="d6245-113">Moq 4.5.30 (ve üzeri), Visual Studio 2017, Roslyn ve .NET 4,5 ve sonraki sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="d6245-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="d6245-114">Birim testlerinde ortak bir model &quot;düzenleme-işlem onaylama&quot;:</span><span class="sxs-lookup"><span data-stu-id="d6245-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="d6245-115">Düzenle: testin çalıştırılacağı önkoşulları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d6245-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="d6245-116">Davran: testi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d6245-116">Act: Perform the test.</span></span>
- <span data-ttu-id="d6245-117">Onaylama: testin başarılı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d6245-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="d6245-118">Düzenleme adımında, genellikle sahte veya saplama nesneleri kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d6245-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="d6245-119">Bu, bağımlılıkların sayısını en aza indirir, böylece test bir şeyi test etmeye odaklanır.</span><span class="sxs-lookup"><span data-stu-id="d6245-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="d6245-120">Web API denetleyicilerinizde birim testi yapmanız gereken bazı şeyler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d6245-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="d6245-121">Eylem doğru yanıt türünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="d6245-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="d6245-122">Geçersiz parametreler doğru hata yanıtını döndürür.</span><span class="sxs-lookup"><span data-stu-id="d6245-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="d6245-123">Eylem, depoda veya hizmet katmanında doğru yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="d6245-124">Yanıt bir etki alanı modeli içeriyorsa, model türünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d6245-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="d6245-125">Bunlar, test etmek için bazı genel şeylerdir, ancak Ayrıntılar denetleyici uygulamanıza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d6245-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="d6245-126">Özellikle, denetleyici eylemlerinizin **HttpResponseMessage** veya **ıhttpactionresult**döndürme konusunda büyük bir farklılık yapar.</span><span class="sxs-lookup"><span data-stu-id="d6245-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="d6245-127">Bu sonuç türleri hakkında daha fazla bilgi için bkz. [Web API 2 ' de eylem sonuçları](../getting-started-with-aspnet-web-api/action-results.md).</span><span class="sxs-lookup"><span data-stu-id="d6245-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="d6245-128">HttpResponseMessage döndüren eylemleri test etme</span><span class="sxs-lookup"><span data-stu-id="d6245-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="d6245-129">Eylemleri **HttpResponseMessage**döndüren bir denetleyiciye örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d6245-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="d6245-130">Denetleyicinin bir `IProductRepository`eklemek için bağımlılık ekleme işlemini kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d6245-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="d6245-131">Bu, bir sahte depo ekleyebildiğinden denetleyiciyi daha kararlı hale getirir.</span><span class="sxs-lookup"><span data-stu-id="d6245-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="d6245-132">Aşağıdaki birim testi, `Get` yönteminin yanıt gövdesine bir `Product` yazdığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="d6245-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="d6245-133">`repository` bir sahte `IProductRepository`olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d6245-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="d6245-134">Denetleyici üzerinde **istek** ve **yapılandırma** ayarlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d6245-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="d6245-135">Aksi takdirde, test bir **ArgumentNullException** veya **InvalidOperationException**ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d6245-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="d6245-136">Bağlantı oluşturma test ediliyor</span><span class="sxs-lookup"><span data-stu-id="d6245-136">Testing Link Generation</span></span>

<span data-ttu-id="d6245-137">`Post` yöntemi, yanıtta bağlantı oluşturmak için **UrlHelper. Link** öğesini çağırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="d6245-138">Bu, birim testinde biraz daha fazla kurulum gerektirir:</span><span class="sxs-lookup"><span data-stu-id="d6245-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="d6245-139">**UrlHelper** sınıfı için istek URL 'si ve rota verileri gerekir, bu nedenle testin bu değerler için değerleri ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6245-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="d6245-140">Diğer bir seçenek de sahte veya saplama **UrlHelper**.</span><span class="sxs-lookup"><span data-stu-id="d6245-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="d6245-141">Bu yaklaşımda, [Apicontroller. URL](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) ' nin varsayılan değerini sabit bir değer döndüren bir sahte veya saplama sürümüyle değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6245-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="d6245-142">[Moq](https://github.com/Moq) çerçevesini kullanarak testi yeniden yazalım.</span><span class="sxs-lookup"><span data-stu-id="d6245-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="d6245-143">`Moq` NuGet paketini test projesine yükler.</span><span class="sxs-lookup"><span data-stu-id="d6245-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="d6245-144">Bu sürümde, bir yol verisi ayarlamanız gerekmez, çünkü sahte **UrlHelper** sabit bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="d6245-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>

## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="d6245-145">Ihttpactionresult döndüren test eylemleri</span><span class="sxs-lookup"><span data-stu-id="d6245-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="d6245-146">Web API 2 ' de, bir denetleyici eylemi **ıhttpactionresult**döndürebilir ve bu, ASP.NET MVC 'de **ActionResult** öğesine benzer.</span><span class="sxs-lookup"><span data-stu-id="d6245-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="d6245-147">**Ihttpactionresult** ARABIRIMI, http yanıtları oluşturmak için bir komut kalıbı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d6245-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="d6245-148">Yanıt doğrudan oluşturmak yerine, denetleyici bir **ıhttpactionresult**döndürür.</span><span class="sxs-lookup"><span data-stu-id="d6245-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="d6245-149">Daha sonra, işlem hattı yanıtı oluşturmak için **ıhttpactionresult** öğesini çağırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="d6245-150">Bu yaklaşım, **HttpResponseMessage**için gereken birçok ayarı atlayabilmeniz için birim testlerini yazmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="d6245-151">Eylemleri **ıhttpactionresult**döndüren örnek bir denetleyici aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d6245-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="d6245-152">Bu örnekte, **ıhttpactionresult**kullanılarak bazı yaygın desenler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d6245-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="d6245-153">Ayrıca, birim testinin nasıl test olduğunu görelim.</span><span class="sxs-lookup"><span data-stu-id="d6245-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="d6245-154">Eylem, yanıt gövdesi ile 200 (Tamam) döndürür</span><span class="sxs-lookup"><span data-stu-id="d6245-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="d6245-155">`Get` yöntemi, ürün bulunursa `Ok(product)` çağırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="d6245-156">Birim testinde, dönüş türünün **Oknegoti, ContentResult** olduğundan ve döndürülen ürünün doğru kimliğe sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d6245-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="d6245-157">Birim testinin eylem sonucunu yürütmediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d6245-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="d6245-158">Eylem sonucunun HTTP yanıtını doğru bir şekilde oluşturduğunu varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6245-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="d6245-159">(Web API çerçevesinin kendi birim testlerine neden vardır!)</span><span class="sxs-lookup"><span data-stu-id="d6245-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="d6245-160">Eylem 404 döndürüyor (bulunamadı)</span><span class="sxs-lookup"><span data-stu-id="d6245-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="d6245-161">`Get` yöntemi, ürün bulunamazsa `NotFound()` çağırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="d6245-162">Bu durumda, birim testi yalnızca dönüş türünün **Notfoundsonucu**olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="d6245-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="d6245-163">Eylem, yanıt gövdesi olmayan 200 (Tamam) döndürür</span><span class="sxs-lookup"><span data-stu-id="d6245-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="d6245-164">`Delete` yöntemi, boş bir HTTP 200 yanıtı döndürmek için `Ok()` çağırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="d6245-165">Önceki örnekte olduğu gibi, birim testi dönüş türünü denetler, bu durumda **Okresult**.</span><span class="sxs-lookup"><span data-stu-id="d6245-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="d6245-166">Eylem, konum üst bilgisi ile 201 (oluşturuldu) döndürüyor</span><span class="sxs-lookup"><span data-stu-id="d6245-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="d6245-167">`Post` yöntemi, konum üstbilgisinde bir URI ile HTTP 201 yanıtı döndürmek için `CreatedAtRoute` çağırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="d6245-168">Birim testinde, eylemin doğru yönlendirme değerlerini ayarladiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d6245-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="d6245-169">Eylem, yanıt gövdesi olan bir 2xx döndürür</span><span class="sxs-lookup"><span data-stu-id="d6245-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="d6245-170">`Put` yöntemi bir yanıt gövdesi ile HTTP 202 (kabul edildi) yanıtı döndürmek için `Content` çağırır.</span><span class="sxs-lookup"><span data-stu-id="d6245-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="d6245-171">Bu durum 200 (Tamam) döndürmeye benzer, ancak birim testi de durum kodunu denetlemelidir.</span><span class="sxs-lookup"><span data-stu-id="d6245-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="d6245-172">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d6245-172">Additional Resources</span></span>

- [<span data-ttu-id="d6245-173">Birim testi ASP.NET Web API 2 ' de Entity Framework Mocking</span><span class="sxs-lookup"><span data-stu-id="d6245-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="d6245-174">[Bir ASP.NET Web API hizmeti için testler yazma](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (Youssef Moussaouı tarafından blog gönderisi).</span><span class="sxs-lookup"><span data-stu-id="d6245-174">[Writing tests for an ASP.NET Web API service](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="d6245-175">Yol hata ayıklayıcı ile ASP.NET Web API 'SI hata ayıklaması</span><span class="sxs-lookup"><span data-stu-id="d6245-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
