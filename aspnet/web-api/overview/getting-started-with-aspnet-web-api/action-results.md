---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2-ASP.NET 4. x ile eylem sonuçları
author: MikeWasson
description: ASP.NET Web API 'sinin döndürülen değeri bir denetleyici eyleminden ASP.NET 4. x içinde HTTP yanıt iletisine nasıl dönüştüreceğini açıklar.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 1eaaf8e87168096683212fa66d3ddf415ad6b22b
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000713"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="1fcc6-103">Web API 2’de Eylem Sonuçları</span><span class="sxs-lookup"><span data-stu-id="1fcc6-103">Action Results in Web API 2</span></span>

<span data-ttu-id="1fcc6-104">Bu konu, ASP.NET Web API 'sinin geri dönüş değerini bir denetleyici eyleminden bir HTTP yanıt iletisine nasıl dönüştürdüğü açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="1fcc6-105">Bir Web API denetleyicisi eylemi aşağıdakilerden herhangi birini döndürebilir:</span><span class="sxs-lookup"><span data-stu-id="1fcc6-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="1fcc6-106">void</span><span class="sxs-lookup"><span data-stu-id="1fcc6-106">void</span></span>
2. <span data-ttu-id="1fcc6-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="1fcc6-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="1fcc6-108">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="1fcc6-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="1fcc6-109">Diğer bir tür</span><span class="sxs-lookup"><span data-stu-id="1fcc6-109">Some other type</span></span>

<span data-ttu-id="1fcc6-110">Bunların ne olduğuna bağlı olarak, Web API 'SI, HTTP yanıtı oluşturmak için farklı bir mekanizma kullanır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="1fcc6-111">Dönüş türü</span><span class="sxs-lookup"><span data-stu-id="1fcc6-111">Return type</span></span> | <span data-ttu-id="1fcc6-112">Web API 'sinin yanıtı nasıl oluşturur</span><span class="sxs-lookup"><span data-stu-id="1fcc6-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="1fcc6-113">void</span><span class="sxs-lookup"><span data-stu-id="1fcc6-113">void</span></span> | <span data-ttu-id="1fcc6-114">Boş 204 döndürün (Içerik yok)</span><span class="sxs-lookup"><span data-stu-id="1fcc6-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="1fcc6-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="1fcc6-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="1fcc6-116">Doğrudan bir HTTP yanıt iletisine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="1fcc6-117">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="1fcc6-117">**IHttpActionResult**</span></span> | <span data-ttu-id="1fcc6-118">Bir **HttpResponseMessage**oluşturmak Için **ExecuteAsync** çağrısı YAPıN ve ardından bir http yanıt iletisine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="1fcc6-119">Diğer tür</span><span class="sxs-lookup"><span data-stu-id="1fcc6-119">Other type</span></span> | <span data-ttu-id="1fcc6-120">Serileştirilmiş dönüş değerini yanıt gövdesine yazın; 200 döndürün (Tamam).</span><span class="sxs-lookup"><span data-stu-id="1fcc6-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="1fcc6-121">Bu konunun geri kalanında her bir seçenek daha ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="1fcc6-122">void</span><span class="sxs-lookup"><span data-stu-id="1fcc6-122">void</span></span>

<span data-ttu-id="1fcc6-123">Dönüş türü ise `void`, Web API 'si yalnızca 204 (içerik yok) durum koduna sahip bir boş http yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="1fcc6-124">Örnek denetleyici:</span><span class="sxs-lookup"><span data-stu-id="1fcc6-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="1fcc6-125">HTTP yanıtı:</span><span class="sxs-lookup"><span data-stu-id="1fcc6-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="1fcc6-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="1fcc6-126">HttpResponseMessage</span></span>

<span data-ttu-id="1fcc6-127">Eylem bir [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)döndürürse, Web API 'si, yanıtı doldurmak Için **HttpResponseMessage** nesnesinin özelliklerini kullanarak döndürülen değeri doğrudan bir http yanıt iletisine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="1fcc6-128">Bu seçenek, yanıt iletisi üzerinde çok fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="1fcc6-129">Örneğin, aşağıdaki denetleyici eylemi Cache-Control üst bilgisini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="1fcc6-130">Yanıtıyla</span><span class="sxs-lookup"><span data-stu-id="1fcc6-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="1fcc6-131">Bir etki alanı modelini **Createresbir** yöntemine geçirirseniz, Web API 'si, serileştirilmiş modeli yanıt gövdesine yazmak için bir [medya biçimlendirici](../formats-and-model-binding/media-formatters.md) kullanır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="1fcc6-132">Web API 'SI, biçimlendirici 'yi seçmek için istekteki Accept üst bilgisini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="1fcc6-133">Daha fazla bilgi için bkz. [Içerik anlaşması](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="1fcc6-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="1fcc6-134">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="1fcc6-134">IHttpActionResult</span></span>

<span data-ttu-id="1fcc6-135">**Ihttpactionresult** ARABIRIMI Web API 2 ' de tanıtılmıştı.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="1fcc6-136">Temelde, bir **HttpResponseMessage** fabrikası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="1fcc6-137">**Ihttpactionresult** arabirimini kullanmanın bazı avantajları aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1fcc6-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="1fcc6-138">Denetleyicileriniz için [birim testini](../testing-and-debugging/unit-testing-controllers-in-web-api.md) basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="1fcc6-139">Ayrı sınıflara HTTP yanıtları oluşturmak için ortak mantığı taşımaktır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="1fcc6-140">, Yanıtı oluşturan alt düzey ayrıntıları gizleyerek, denetleyici eyleminin amacını daha net hale getirir.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="1fcc6-141">**Ihttpactionresult** , zaman uyumsuz olarak bir **HttpResponseMessage** örneği oluşturan **ExecuteAsync**tek bir yöntem içerir.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="1fcc6-142">Bir denetleyici eylemi bir **ıhttpactionresult**döndürürse, Web API 'Si bir **HttpResponseMessage**oluşturmak için **ExecuteAsync** yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="1fcc6-143">Daha sonra **HttpResponseMessage** 'YI bir http yanıt iletisine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="1fcc6-144">Bir düz metin yanıtı oluşturan **ıhttpactionresult** öğesinin basit bir uygulaması aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1fcc6-144">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="1fcc6-145">Örnek denetleyici eylemi:</span><span class="sxs-lookup"><span data-stu-id="1fcc6-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="1fcc6-146">Yanıtıyla</span><span class="sxs-lookup"><span data-stu-id="1fcc6-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="1fcc6-147">Daha sık, **[System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** ad alanında tanımlanan **ıhttpactionresult** uygulamalarını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-147">More often, you use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="1fcc6-148">**Apicontroller** sınıfı, bu yerleşik eylem sonuçlarını döndüren yardımcı yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="1fcc6-149">Aşağıdaki örnekte, istek mevcut bir ürün KIMLIĞIYLE eşleşmezse, denetleyici bir 404 (bulunamadı) yanıtı oluşturmak için [Apicontroller. NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="1fcc6-150">Aksi takdirde, denetleyici, ürünü içeren bir 200 (Tamam) yanıtı oluşturan [Apicontroller. ok](https://msdn.microsoft.com/library/dn314591.aspx)öğesini çağırır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="1fcc6-151">Diğer dönüş türleri</span><span class="sxs-lookup"><span data-stu-id="1fcc6-151">Other Return Types</span></span>

<span data-ttu-id="1fcc6-152">Diğer tüm dönüş türleri için Web API 'SI, dönüş değerini seri hale getirmek için bir [medya biçimlendirici](../formats-and-model-binding/media-formatters.md) kullanır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="1fcc6-153">Web API 'SI, serileştirilmiş değeri yanıt gövdesine yazar.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="1fcc6-154">Yanıt durum kodu 200 ' dir (Tamam).</span><span class="sxs-lookup"><span data-stu-id="1fcc6-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="1fcc6-155">Bu yaklaşımın bir dezavantajı, 404 gibi doğrudan bir hata kodu döndürmemelidir.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="1fcc6-156">Ancak, hata kodları için bir **Httpresponseexception** oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="1fcc6-157">Daha fazla bilgi için bkz. [ASP.NET Web API 'de özel durum işleme](../error-handling/exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="1fcc6-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="1fcc6-158">Web API 'SI, biçimlendirici 'yi seçmek için istekteki Accept üst bilgisini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1fcc6-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="1fcc6-159">Daha fazla bilgi için bkz. [Içerik anlaşması](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="1fcc6-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="1fcc6-160">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="1fcc6-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="1fcc6-161">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="1fcc6-161">Example response</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
