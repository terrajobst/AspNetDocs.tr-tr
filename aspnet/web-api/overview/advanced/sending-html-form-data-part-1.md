---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: "ASP.NET Web API'de HTML Form verileri gönderme: Form-urlencoded verileri - ASP.NET 4.x"
author: MikeWasson
description: Bu makalede, ASP.NET ile Web API denetleyicisi form-urlencoded verileri gönderileceği gösterilmektedir 4.x
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: fb0309af11910125943737ebb721b356b7bd08bc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59418306"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="b1dcd-103">ASP.NET Web API'de HTML Form verileri gönderme: Form-urlencoded Verileri</span><span class="sxs-lookup"><span data-stu-id="b1dcd-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="b1dcd-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b1dcd-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="b1dcd-105">Bölüm 1: Form-urlencoded Verileri</span><span class="sxs-lookup"><span data-stu-id="b1dcd-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="b1dcd-106">Bu makalede, bir Web API denetleyicisi için form-urlencoded verileri gönderileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="b1dcd-107">HTML formu genel bakış</span><span class="sxs-lookup"><span data-stu-id="b1dcd-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="b1dcd-108">Karmaşık türler gönderme</span><span class="sxs-lookup"><span data-stu-id="b1dcd-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="b1dcd-109">AJAX üzerinden form verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="b1dcd-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="b1dcd-110">Gönderen basit türler</span><span class="sxs-lookup"><span data-stu-id="b1dcd-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="b1dcd-111">[Tamamlanmış projeyi indirmek](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span><span class="sxs-lookup"><span data-stu-id="b1dcd-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="b1dcd-112">HTML formu genel bakış</span><span class="sxs-lookup"><span data-stu-id="b1dcd-112">Overview of HTML Forms</span></span>

<span data-ttu-id="b1dcd-113">HTML form kullanımı alın veya veri sunucuya göndermek için gönderin.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="b1dcd-114">**Yöntemi** özniteliği **form** öğesi HTTP yöntemi sunar:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="b1dcd-115">GET için varsayılan yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-115">The default method is GET.</span></span> <span data-ttu-id="b1dcd-116">Form kullanıyorsa, formun URI sorgu dizesi olarak kodlanmış verileri alın.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="b1dcd-117">Form POST kullanıyorsa, form verilerini istek gövdesinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="b1dcd-118">Deftere nakledilen veri **Notenctype** özniteliği, istek gövdesi biçimini belirtir:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="b1dcd-119">Notenctype</span><span class="sxs-lookup"><span data-stu-id="b1dcd-119">enctype</span></span> | <span data-ttu-id="b1dcd-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b1dcd-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1dcd-121">Application/x-www-form-urlencoded işlemek</span><span class="sxs-lookup"><span data-stu-id="b1dcd-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="b1dcd-122">Ad/değer çiftleri, benzer bir URI sorgu dizesi olarak kodlanmış bir form verileri.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="b1dcd-123">Bu GÖNDERİ için varsayılan biçimidir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="b1dcd-124">multipart/form-data</span><span class="sxs-lookup"><span data-stu-id="b1dcd-124">multipart/form-data</span></span> | <span data-ttu-id="b1dcd-125">Form verileri çok parçalı MIME ileti olarak kodlanır.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="b1dcd-126">Bir dosya sunucusuna yüklüyorsanız bu biçimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="b1dcd-127">Bu makalede, bölüm 1 x-www-form-urlencoded işlemek biçimi arar.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="b1dcd-128">[2. bölüm](sending-html-form-data-part-2.md) çok parçalı MIME açıklar.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="b1dcd-129">Karmaşık türler gönderme</span><span class="sxs-lookup"><span data-stu-id="b1dcd-129">Sending Complex Types</span></span>

<span data-ttu-id="b1dcd-130">Genellikle, birden çok form denetimlerini alınan değerleri oluşan karmaşık bir tür gönderir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="b1dcd-131">Durum güncelleştirmesi temsil eden şu model göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="b1dcd-132">Kabul eden bir Web API denetleyicisi İşte bir `Update` POST aracılığıyla nesne.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="b1dcd-133">Bu denetleyicisi kullanan [eylem tabanlı yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), rota şablonu, bu nedenle &quot;API / {denetleyici} / {eylem} / {id}&quot;.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="b1dcd-134">İstemci verileri post gerçekleştireceği &quot;/api/updates/complex&quot;.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>


<span data-ttu-id="b1dcd-135">Artık kullanıcıların durumu güncelleştirmeyi göndermek bir HTML formuna yazalım.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="b1dcd-136">Dikkat **eylem** özniteliktir formdaki denetleyicisi eylemimiz URI'si.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="b1dcd-137">Girilen bazı değerler formu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="b1dcd-138">Kullanıcı gönderme tıkladığında tarayıcı bir HTTP isteği aşağıdakine benzer gönderir:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="b1dcd-139">İstek gövdesini form verileri, ad/değer çiftleri biçimlendirilmiş içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="b1dcd-140">Web API'si bir örneğine otomatik olarak ad/değer çiftleri dönüştürür `Update` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="b1dcd-141">AJAX üzerinden form verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="b1dcd-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="b1dcd-142">Kullanıcı formu gönderdiğinde, tarayıcı Geçerli sayfadan ayrılmak gider ve yanıt iletisinin gövdesini işler.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="b1dcd-143">Yanıtı HTML sayfası Tamam andır.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="b1dcd-144">Bir web API ile ancak yanıt gövdesinin genellikle geçerli boş veya JSON gibi yapılandırılmış verilerin içerir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="b1dcd-145">Bu durumda, bu istek bir AJAX kullanarak form verilerini, sayfanın yanıt işleyebilmesi göndermek için daha anlamlı olur.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="b1dcd-146">Aşağıdaki kod, jQuery kullanarak form verileri gönderileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="b1dcd-147">JQuery **gönderme** işlevi, form eylemi yeni bir işlev ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="b1dcd-148">Bu, Gönder düğmesinin varsayılan davranışı geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="b1dcd-149">**Serileştirmek** işlevi ad/değer çiftlerine form verilerini serileştirir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="b1dcd-150">Form verileri sunucuya göndermek için arama `$.post()`.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="b1dcd-151">İstek tamamlandıktan sonra `.success()` veya `.error()` işleyicisi, kullanıcı için uygun bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="b1dcd-152">Gönderen basit türler</span><span class="sxs-lookup"><span data-stu-id="b1dcd-152">Sending Simple Types</span></span>

<span data-ttu-id="b1dcd-153">Önceki bölümlerde, Web API'si için bir model sınıfının bir örneği seri durumdan bir karmaşık tür gönderdik.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="b1dcd-154">Ayrıca, bir dize gibi basit türler de gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="b1dcd-155">Basit bir tür göndermeden önce değerin bir karmaşık türü yerine sarmalama göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="b1dcd-156">Bu, sunucu tarafında model doğrulama avantajlarını sağlar ve gerekirse modelinizi genişletmek daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>


<span data-ttu-id="b1dcd-157">Basit bir tür göndermek için temel adımlar aynıdır, ancak iki küçük farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="b1dcd-158">İlk olarak, denetleyicisi, parametre adı ile tasarlamanız gerekir **FromBody** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="b1dcd-159">Varsayılan olarak, Web API'si basit türler istek URI'SİNDEN almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="b1dcd-160">**FromBody** öznitelik değeri gövdeden okunacak Web API söyler.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="b1dcd-161">Web API yanıt gövdesinin en fazla bir kez, bu nedenle yalnızca tek bir eylem parametresinin gövdeden gelebilir okur.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="b1dcd-162">Gövdeden birden çok değer almanız gerekirse, bir karmaşık tür tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-162">If you need to get multiple values from the request body, define a complex type.</span></span>


<span data-ttu-id="b1dcd-163">İkinci olarak, istemci aşağıdaki biçimde değeri göndermesi gerekiyor:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="b1dcd-164">Özellikle, ad/değer çiftinin ad bölümünü basit bir tür için boş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="b1dcd-165">Tüm tarayıcılar bu için HTML formları desteklemez, ancak, bu biçim şu şekilde oluştur:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="b1dcd-166">Bir örnek formu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="b1dcd-167">Ve form değer göndermek için komut dosyası aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="b1dcd-168">Tek fark önceki komut dosyası içine geçirilen bağımsız değişken, **sonrası** işlevi.</span><span class="sxs-lookup"><span data-stu-id="b1dcd-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="b1dcd-169">Basit bir tür dizisi göndermek için aynı yaklaşımı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b1dcd-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="b1dcd-170">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b1dcd-170">Additional Resources</span></span>

[<span data-ttu-id="b1dcd-171">Bölüm 2: Karşıya dosya yükleme ve çok parçalı MIME</span><span class="sxs-lookup"><span data-stu-id="b1dcd-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
