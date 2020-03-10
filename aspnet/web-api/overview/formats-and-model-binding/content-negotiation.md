---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API-ASP.NET 4. x içinde içerik anlaşması
author: MikeWasson
description: ASP.NET Web API 'sinin ASP.NET 4. x için HTTP içerik anlaşmasını nasıl uyguladığını açıklar.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622271"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="09834-103">ASP.NET Web API 'de içerik anlaşması</span><span class="sxs-lookup"><span data-stu-id="09834-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="09834-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="09834-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="09834-105">Bu makalede, ASP.NET Web API 'sinin ASP.NET 4. x için içerik anlaşmasını nasıl uyguladığı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="09834-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="09834-106">HTTP belirtimi (RFC 2616), "birden fazla temsili varsa belirli bir yanıt için en iyi temsili seçme işlemi" olarak içerik anlaşmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="09834-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="09834-107">HTTP 'de içerik anlaşmasına yönelik birincil mekanizma şu istek başlıklardır:</span><span class="sxs-lookup"><span data-stu-id="09834-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="09834-108">**Kabul et:** "Application/JSON," application/xml "gibi yanıt için kabul edilebilir medya türleri veya &quot;application/vnd gibi özel bir medya türü. örnek + XML&quot;</span><span class="sxs-lookup"><span data-stu-id="09834-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="09834-109">**Accept-Charset:** UTF-8 veya ISO 8859-1 gibi hangi karakter kümeleri kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="09834-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="09834-110">**Accept-Encoding:** Gzip gibi hangi içerik kodlamaları kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="09834-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="09834-111">**Accept-Language:** Tercih edilen doğal dil ("en-US" gibi).</span><span class="sxs-lookup"><span data-stu-id="09834-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="09834-112">Sunucu ayrıca HTTP isteğinin diğer bölümlerine da bakabilirler.</span><span class="sxs-lookup"><span data-stu-id="09834-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="09834-113">Örneğin, istek bir AJAX isteği gösteren bir X-requested-with üst bilgisi içeriyorsa, Accept üst bilgisi yoksa sunucu JSON olarak varsayılan olabilir.</span><span class="sxs-lookup"><span data-stu-id="09834-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="09834-114">Bu makalede, Web API 'sinin Accept ve Accept-Charset üst bilgilerini nasıl kullandığını inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="09834-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="09834-115">(Şu anda, Accept-Encoding veya Accept-Language için yerleşik destek yoktur.)</span><span class="sxs-lookup"><span data-stu-id="09834-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="09834-116">Serileştirme</span><span class="sxs-lookup"><span data-stu-id="09834-116">Serialization</span></span>

<span data-ttu-id="09834-117">Bir Web API denetleyicisi bir kaynağı CLR türü olarak döndürürse, işlem hattı döndürülen değeri serileştirir ve HTTP yanıt gövdesine yazar.</span><span class="sxs-lookup"><span data-stu-id="09834-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="09834-118">Örneğin, aşağıdaki denetleyici eylemini göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="09834-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="09834-119">İstemci şu HTTP isteğini gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="09834-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="09834-120">Yanıt olarak, sunucunun şunları gönderebileceğini:</span><span class="sxs-lookup"><span data-stu-id="09834-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="09834-121">Bu örnekte, istemci JSON, JavaScript veya "her şeyi" (\*/\*) istedi.</span><span class="sxs-lookup"><span data-stu-id="09834-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="09834-122">Sunucu, `Product` nesnesinin JSON temsili ile yanıt verdi.</span><span class="sxs-lookup"><span data-stu-id="09834-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="09834-123">Yanıttaki Içerik türü üstbilgisinin &quot;Application/JSON&quot;olarak ayarlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="09834-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="09834-124">Bir denetleyici, bir **HttpResponseMessage** nesnesi de döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="09834-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="09834-125">Yanıt gövdesi için bir CLR nesnesi belirtmek üzere **Createres,** Extension metodunu çağırın:</span><span class="sxs-lookup"><span data-stu-id="09834-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="09834-126">Bu seçenek, yanıtın ayrıntıları üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="09834-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="09834-127">Durum kodunu ayarlayabilir, HTTP üst bilgileri ekleyebilir ve benzeri bir durumla devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09834-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="09834-128">Kaynağı serileştiren nesneye *medya biçimlendirici*denir.</span><span class="sxs-lookup"><span data-stu-id="09834-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="09834-129">Medya formatlayıcıları, **MediaTypeFormatter** sınıfından türetilir.</span><span class="sxs-lookup"><span data-stu-id="09834-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="09834-130">Web API 'si, XML ve JSON için medya biçimleri sağlar ve diğer medya türlerini desteklemek için özel biçimleri de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09834-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="09834-131">Özel bir biçimlendirici yazma hakkında daha fazla bilgi için bkz. [medya biçimleri](media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="09834-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="09834-132">Içerik anlaşması nasıl kullanılır?</span><span class="sxs-lookup"><span data-stu-id="09834-132">How Content Negotiation Works</span></span>

<span data-ttu-id="09834-133">İlk olarak, işlem hattı **HttpConfiguration** nesnesinden **ıtentnegotiator** hizmetini alır.</span><span class="sxs-lookup"><span data-stu-id="09834-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="09834-134">Ayrıca, **HttpConfiguration. biçimlendiricileri** koleksiyonundan medya formatlayıcıları listesini alır.</span><span class="sxs-lookup"><span data-stu-id="09834-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="09834-135">Sonra, işlem hattı **ıditentnegotiator. Negotiate**çağırır, geçirme:</span><span class="sxs-lookup"><span data-stu-id="09834-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="09834-136">Seri hale getirilecek nesnenin türü</span><span class="sxs-lookup"><span data-stu-id="09834-136">The type of object to serialize</span></span>
- <span data-ttu-id="09834-137">Medya formatlayıcıları koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="09834-137">The collection of media formatters</span></span>
- <span data-ttu-id="09834-138">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="09834-138">The HTTP request</span></span>

<span data-ttu-id="09834-139">**Negotiate** yöntemi iki bilgi parçası döndürür:</span><span class="sxs-lookup"><span data-stu-id="09834-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="09834-140">Kullanılacak biçimlendirici</span><span class="sxs-lookup"><span data-stu-id="09834-140">Which formatter to use</span></span>
- <span data-ttu-id="09834-141">Yanıt için medya türü</span><span class="sxs-lookup"><span data-stu-id="09834-141">The media type for the response</span></span>

<span data-ttu-id="09834-142">Bir biçimlendirici bulunmazsa, **Negotiate** yöntemi **null**DEĞERINI döndürür ve istemci http hatası 406 (kabul edilemez) alır.</span><span class="sxs-lookup"><span data-stu-id="09834-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="09834-143">Aşağıdaki kod, bir denetleyicinin içerik anlaşmasını doğrudan nasıl çağırabileceği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="09834-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="09834-144">Bu kod, işlem hattının otomatik olarak ne olduğuna eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="09834-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="09834-145">Varsayılan Içerik Negotiator</span><span class="sxs-lookup"><span data-stu-id="09834-145">Default Content Negotiator</span></span>

<span data-ttu-id="09834-146">**Defaultcontentnegotiator** sınıfı, **ıtenttrnegotiator**'ın varsayılan uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="09834-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="09834-147">Bir biçimlendirici seçmek için birkaç ölçüt kullanır.</span><span class="sxs-lookup"><span data-stu-id="09834-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="09834-148">İlk olarak, biçimlendirici türü seri hale getirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="09834-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="09834-149">Bu, **MediaTypeFormatter. CanWriteType**çağırarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="09834-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="09834-150">Ardından, içerik Negotiator her bir biçimlendirici üzerinde bakar ve HTTP isteğiyle ne kadar iyi eşleşme olduğunu değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="09834-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="09834-151">Eşleşmeyi değerlendirmek için, içerik Negotiator, biçimlendirici üzerinde iki şeyi arar:</span><span class="sxs-lookup"><span data-stu-id="09834-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="09834-152">Desteklenen medya türlerinin bir listesini içeren **Supportedmediatypes** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="09834-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="09834-153">İçerik Negotiator, istek kabul üstbilgisiyle bu listeyi eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="09834-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="09834-154">Accept üst bilgisinin aralıklar içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="09834-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="09834-155">Örneğin, "metin/düz" metin/\* veya \*/\*için bir eşleşmedir.</span><span class="sxs-lookup"><span data-stu-id="09834-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="09834-156">**MediaTypeMapping** nesnelerinin bir listesini Içeren **mediatypemappings** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="09834-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="09834-157">**MediaTypeMapping** sınıfı, medya türleriyle http isteklerini eşleştirmek için genel bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="09834-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="09834-158">Örneğin, özel bir HTTP üst bilgisini belirli bir medya türüyle eşleyebilir.</span><span class="sxs-lookup"><span data-stu-id="09834-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="09834-159">Birden çok eşleşme varsa, en yüksek kalite faktörüyle eşleşme kazanır.</span><span class="sxs-lookup"><span data-stu-id="09834-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="09834-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="09834-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="09834-161">Bu örnekte, Application/JSON 'ın kapsanan bir kalite faktörü 1,0, bu nedenle application/xml üzerinden tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="09834-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="09834-162">Hiçbir eşleşme bulunmazsa, içerik Negotiator, varsa istek gövdesinin medya türüyle eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="09834-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="09834-163">Örneğin, istek JSON verisi içeriyorsa, içerik Negotiator bir JSON biçimlendiricisi arar.</span><span class="sxs-lookup"><span data-stu-id="09834-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="09834-164">Hala eşleşme yoksa, Negotiator, türü seri hale getirmek için yalnızca ilk biçimlendirici seçer.</span><span class="sxs-lookup"><span data-stu-id="09834-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="09834-165">Bir karakter kodlaması seçme</span><span class="sxs-lookup"><span data-stu-id="09834-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="09834-166">Bir biçimlendirici seçildikten sonra, içerik Negotiator, biçimlendirici üzerindeki **Supportedencoular** özelliğine bakarak en iyi karakter kodlamasını seçer ve istekteki Accept-Charset üstbilgisine (varsa) karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="09834-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
