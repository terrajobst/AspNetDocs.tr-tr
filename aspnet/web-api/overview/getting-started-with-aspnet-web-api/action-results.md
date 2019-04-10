---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Eylem sonuçlarını Web API 2 - ASP.NET 4.x
author: MikeWasson
description: Nasıl ASP.NET Web API dönüş değeri bir denetleyici eylemi bir HTTP yanıt iletisine ASP.NET'te dönüştürür açıklar 4.x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 87f71938a5c5f38d3a456ba9339540f67e236e1a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400899"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="669c6-103">Web API 2’de Eylem Sonuçları</span><span class="sxs-lookup"><span data-stu-id="669c6-103">Action Results in Web API 2</span></span>

<span data-ttu-id="669c6-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="669c6-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="669c6-105">Bu konuda, nasıl ASP.NET Web API dönüş değeri bir denetleyici eylemi bir HTTP yanıt iletisine dönüştürür açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="669c6-105">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="669c6-106">Bir Web API denetleyici eylemi aşağıdakilerden herhangi birini geri dönebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="669c6-106">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="669c6-107">void</span><span class="sxs-lookup"><span data-stu-id="669c6-107">void</span></span>
2. **<span data-ttu-id="669c6-108">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="669c6-108">HttpResponseMessage</span></span>**
3. **<span data-ttu-id="669c6-109">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="669c6-109">IHttpActionResult</span></span>**
4. <span data-ttu-id="669c6-110">Başka bir türü</span><span class="sxs-lookup"><span data-stu-id="669c6-110">Some other type</span></span>

<span data-ttu-id="669c6-111">Bu bağlı olarak getirilen, Web API'si, HTTP yanıtı oluşturmak için farklı bir mekanizma kullanır.</span><span class="sxs-lookup"><span data-stu-id="669c6-111">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="669c6-112">Dönüş türü</span><span class="sxs-lookup"><span data-stu-id="669c6-112">Return type</span></span> | <span data-ttu-id="669c6-113">Web API'si yanıtı nasıl oluşturur?</span><span class="sxs-lookup"><span data-stu-id="669c6-113">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="669c6-114">void</span><span class="sxs-lookup"><span data-stu-id="669c6-114">void</span></span> | <span data-ttu-id="669c6-115">Boş dönüş 204 (içerik yok)</span><span class="sxs-lookup"><span data-stu-id="669c6-115">Return empty 204 (No Content)</span></span> |
| **<span data-ttu-id="669c6-116">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="669c6-116">HttpResponseMessage</span></span>** | <span data-ttu-id="669c6-117">Bir HTTP yanıt iletisi doğrudan dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="669c6-117">Convert directly to an HTTP response message.</span></span> |
| **<span data-ttu-id="669c6-118">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="669c6-118">IHttpActionResult</span></span>** | <span data-ttu-id="669c6-119">Çağrı **ExecuteAsync** oluşturmak için bir **HttpResponseMessage**, ardından bir HTTP yanıt iletisi dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="669c6-119">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="669c6-120">Diğer tür</span><span class="sxs-lookup"><span data-stu-id="669c6-120">Other type</span></span> | <span data-ttu-id="669c6-121">Yanıt gövdesine seri hale getirilmiş dönüş değeri yazabilirsiniz. 200 (Tamam) döndürür.</span><span class="sxs-lookup"><span data-stu-id="669c6-121">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="669c6-122">Bu konunun geri kalanında her bir seçenek daha ayrıntılı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="669c6-122">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="669c6-123">void</span><span class="sxs-lookup"><span data-stu-id="669c6-123">void</span></span>

<span data-ttu-id="669c6-124">Dönüş türü ise `void`, Web API'sini yalnızca boş bir HTTP yanıtının durum kodu 204 (içerik yok) döndürür.</span><span class="sxs-lookup"><span data-stu-id="669c6-124">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="669c6-125">Örnek denetleyicisi:</span><span class="sxs-lookup"><span data-stu-id="669c6-125">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="669c6-126">HTTP yanıtı:</span><span class="sxs-lookup"><span data-stu-id="669c6-126">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="669c6-127">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="669c6-127">HttpResponseMessage</span></span>

<span data-ttu-id="669c6-128">Eylem döndürürse bir [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API'si dönüştürür dönüş değeri doğrudan bir HTTP yanıt iletisine, özelliklerini kullanarak **HttpResponseMessage** doldurmak için nesne yanıt.</span><span class="sxs-lookup"><span data-stu-id="669c6-128">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="669c6-129">Bu seçenek birçok yanıt iletisi üzerinde denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="669c6-129">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="669c6-130">Örneğin, aşağıdaki denetleyici eylemi Cache-Control üst bilgisi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="669c6-130">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="669c6-131">Yanıt:</span><span class="sxs-lookup"><span data-stu-id="669c6-131">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="669c6-132">Bir etki alanı modeline geçirirseniz **CreateResponse** yöntemi, Web API'sini kullanan bir [medya biçimlendiricisi](../formats-and-model-binding/media-formatters.md) serileştirilmiş modeli yanıt gövdesine yazılacak.</span><span class="sxs-lookup"><span data-stu-id="669c6-132">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="669c6-133">Web API'si, biçimlendirici seçmek için istekte Accept üst bilgisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="669c6-133">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="669c6-134">Daha fazla bilgi için [içerik anlaşması](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="669c6-134">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="669c6-135">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="669c6-135">IHttpActionResult</span></span>

<span data-ttu-id="669c6-136">**Ihttpactionresult** arabirimi, Web API 2'de tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="669c6-136">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="669c6-137">Esas olarak tanımlayan bir **HttpResponseMessage** üreteci.</span><span class="sxs-lookup"><span data-stu-id="669c6-137">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="669c6-138">Kullanmanın bazı avantajları şunlardır **Ihttpactionresult** arabirimi:</span><span class="sxs-lookup"><span data-stu-id="669c6-138">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="669c6-139">Basitleştirir [birim testi](../testing-and-debugging/unit-testing-controllers-in-web-api.md) denetleyicilerinizi.</span><span class="sxs-lookup"><span data-stu-id="669c6-139">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="669c6-140">HTTP yanıt ayrı sınıflara oluşturmak için sık kullanılan mantıksal taşır.</span><span class="sxs-lookup"><span data-stu-id="669c6-140">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="669c6-141">Yanıt oluşturmak, alt düzey ayrıntıları gizleyerek amacı, NET, denetleyici eylemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="669c6-141">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="669c6-142">**Ihttpactionresult** içeren tek bir yöntem **ExecuteAsync**, zaman uyumsuz olarak oluşturan bir **HttpResponseMessage** örneği.</span><span class="sxs-lookup"><span data-stu-id="669c6-142">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="669c6-143">Bir denetleyici eylemi döndürürse bir **Ihttpactionresult**, Web API'si çağıran **ExecuteAsync** yöntemi oluşturmak için bir **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="669c6-143">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="669c6-144">Bunu dönüştürür **HttpResponseMessage** içine bir HTTP yanıt iletisi.</span><span class="sxs-lookup"><span data-stu-id="669c6-144">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="669c6-145">İşte basit bir uygulaması **Ihttpactionresult** düz metin yanıtı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="669c6-145">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="669c6-146">Örnek denetleyici eylem:</span><span class="sxs-lookup"><span data-stu-id="669c6-146">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="669c6-147">Yanıt:</span><span class="sxs-lookup"><span data-stu-id="669c6-147">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="669c6-148">Daha sık kullanacağınız **Ihttpactionresult** tanımlanan uygulamaları **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="669c6-148">More often, you will use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="669c6-149">**ApiController** sınıfı, bu yerleşik eylem sonuçları döndüren yardımcı yöntemler tanımlar.</span><span class="sxs-lookup"><span data-stu-id="669c6-149">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="669c6-150">Aşağıdaki örnekte, istek var olan bir ürün kimliği eşleşmiyorsa denetleyicisi çağıran [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) 404 (bulunamadı) yanıt oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="669c6-150">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="669c6-151">Aksi takdirde, denetleyiciyi çağıran [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), ürün, 200 (Tamam) bir yanıt oluşturan içerir.</span><span class="sxs-lookup"><span data-stu-id="669c6-151">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="669c6-152">Diğer dönüş türleri</span><span class="sxs-lookup"><span data-stu-id="669c6-152">Other Return Types</span></span>

<span data-ttu-id="669c6-153">Diğer tüm dönüş türleri için Web API'si kullanan bir [medya biçimlendiricisi](../formats-and-model-binding/media-formatters.md) dönüş değeri serileştirmek için.</span><span class="sxs-lookup"><span data-stu-id="669c6-153">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="669c6-154">Web API'si, yanıt gövdesine seri hale getirilmiş değer yazar.</span><span class="sxs-lookup"><span data-stu-id="669c6-154">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="669c6-155">Yanıt durum kodu 200 (Tamam) ' dir.</span><span class="sxs-lookup"><span data-stu-id="669c6-155">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="669c6-156">Bu yaklaşımın bir dezavantajı, 404 gibi bir hata kodu doğrudan döndüremez ' dir.</span><span class="sxs-lookup"><span data-stu-id="669c6-156">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="669c6-157">Ancak, oluşturabilecek bir **HttpResponseException** hata kodları.</span><span class="sxs-lookup"><span data-stu-id="669c6-157">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="669c6-158">Daha fazla bilgi için [ASP.NET Web API'de özel durum işleme](../error-handling/exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="669c6-158">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="669c6-159">Web API'si, biçimlendirici seçmek için istekte Accept üst bilgisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="669c6-159">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="669c6-160">Daha fazla bilgi için [içerik anlaşması](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="669c6-160">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="669c6-161">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="669c6-161">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="669c6-162">Örnek yanıt:</span><span class="sxs-lookup"><span data-stu-id="669c6-162">Example response:</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
