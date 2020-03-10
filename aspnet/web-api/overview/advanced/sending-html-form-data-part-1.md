---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: "ASP.NET Web API 'sinde HTML form verileri gönderme: form-urlencoded Data-ASP.NET 4. x"
author: MikeWasson
description: Bu makalede, form-urlencoded verilerinin ASP.NET 4. x ile bir Web API denetleyicisine nasıl nakledileceği gösterilmektedir
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557605"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="b18d2-103">ASP.NET Web API 'sinde HTML form verileri gönderme: form-urlencoded Data</span><span class="sxs-lookup"><span data-stu-id="b18d2-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="b18d2-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b18d2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="b18d2-105">1\. kısım: form-urlencoded verileri</span><span class="sxs-lookup"><span data-stu-id="b18d2-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="b18d2-106">Bu makalede, form-urlencoded verilerinin bir Web API denetleyicisine nasıl nakledileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="b18d2-107">HTML formlarına genel bakış</span><span class="sxs-lookup"><span data-stu-id="b18d2-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="b18d2-108">Karmaşık türler gönderiliyor</span><span class="sxs-lookup"><span data-stu-id="b18d2-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="b18d2-109">AJAX aracılığıyla form verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="b18d2-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="b18d2-110">Basit türler gönderiliyor</span><span class="sxs-lookup"><span data-stu-id="b18d2-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="b18d2-111">[Tamamlanmış projeyi indirin](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span><span class="sxs-lookup"><span data-stu-id="b18d2-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="b18d2-112">HTML formlarına genel bakış</span><span class="sxs-lookup"><span data-stu-id="b18d2-112">Overview of HTML Forms</span></span>

<span data-ttu-id="b18d2-113">HTML formları, verileri sunucuya göndermek için GET veya POST kullanır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="b18d2-114">**Form** öğesinin **Method** özniteliği http yöntemini verir:</span><span class="sxs-lookup"><span data-stu-id="b18d2-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="b18d2-115">Varsayılan yöntem Al ' dır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-115">The default method is GET.</span></span> <span data-ttu-id="b18d2-116">Form GET kullanıyorsa, form verileri URI 'de bir sorgu dizesi olarak kodlanır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="b18d2-117">Form POST kullanıyorsa, form verileri istek gövdesine yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="b18d2-118">Postalanan veriler için, **Enctype** özniteliği istek gövdesinin biçimini belirtir:</span><span class="sxs-lookup"><span data-stu-id="b18d2-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="b18d2-119">Enctype</span><span class="sxs-lookup"><span data-stu-id="b18d2-119">enctype</span></span> | <span data-ttu-id="b18d2-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b18d2-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b18d2-121">Application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="b18d2-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="b18d2-122">Form verileri, bir URI sorgu dizesine benzer şekilde ad/değer çiftleri olarak kodlanır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="b18d2-123">Bu, POST için varsayılan biçimdir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="b18d2-124">multipart/form-Data</span><span class="sxs-lookup"><span data-stu-id="b18d2-124">multipart/form-data</span></span> | <span data-ttu-id="b18d2-125">Form verileri çok parçalı bir MIME iletisi olarak kodlanır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="b18d2-126">Sunucuya bir dosya yüklüyorsanız bu biçimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="b18d2-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="b18d2-127">Bu makalenin 1. bölümü, x-www-form-urlencoded biçimine bakar.</span><span class="sxs-lookup"><span data-stu-id="b18d2-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="b18d2-128">[Bölüm 2](sending-html-form-data-part-2.md) çok parçalı MIME tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b18d2-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="b18d2-129">Karmaşık türler gönderiliyor</span><span class="sxs-lookup"><span data-stu-id="b18d2-129">Sending Complex Types</span></span>

<span data-ttu-id="b18d2-130">Genellikle, çeşitli form denetimlerinden alınan değerlerden oluşan karmaşık bir tür gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="b18d2-131">Bir durum güncelleştirmesini temsil eden aşağıdaki modeli göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="b18d2-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="b18d2-132">GÖNDERI aracılığıyla `Update` nesnesini kabul eden bir Web API denetleyicisi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="b18d2-133">Bu denetleyici [eylem tabanlı yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)kullanır, bu nedenle yol şablonu &quot;API/{Controller}/{Action}/{id}&quot;.</span><span class="sxs-lookup"><span data-stu-id="b18d2-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="b18d2-134">İstemci, verileri/api/Updates/Complex&quot;&quot;nakleder.</span><span class="sxs-lookup"><span data-stu-id="b18d2-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>

<span data-ttu-id="b18d2-135">Şimdi, kullanıcıların bir durum güncelleştirmesi göndermesi için bir HTML formu yazalım.</span><span class="sxs-lookup"><span data-stu-id="b18d2-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="b18d2-136">Form üzerindeki **Action** özniteliğinin Controller eylemizin URI 'si olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b18d2-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="b18d2-137">Aşağıda, bazı değerlerin girildiği form verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b18d2-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="b18d2-138">Kullanıcı Gönder ' e tıkladığında tarayıcı aşağıdakine benzer bir HTTP isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="b18d2-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="b18d2-139">İstek gövdesinin, ad/değer çiftleri olarak biçimlendirilen form verilerini içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b18d2-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="b18d2-140">Web API 'SI, ad/değer çiftlerini otomatik olarak `Update` sınıfının bir örneğine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="b18d2-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="b18d2-141">AJAX aracılığıyla form verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="b18d2-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="b18d2-142">Kullanıcı bir form gönderdiğinde, tarayıcı geçerli sayfadan uzağa gider ve yanıt iletisinin gövdesini işler.</span><span class="sxs-lookup"><span data-stu-id="b18d2-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="b18d2-143">Yanıt bir HTML sayfası olduğunda bu tamam.</span><span class="sxs-lookup"><span data-stu-id="b18d2-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="b18d2-144">Ancak, bir Web API 'SI ile yanıt gövdesi genellikle boştur veya JSON gibi yapılandırılmış verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="b18d2-145">Bu durumda, bir AJAX isteği kullanarak form verilerinin gönderilmesi daha anlamlı hale gelir, böylece sayfa yanıtı işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="b18d2-146">Aşağıdaki kod, form verilerinin jQuery kullanılarak nasıl nakledileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="b18d2-147">JQuery **Gönder** işlevi form eyleminin yerine yeni bir işlev koyar.</span><span class="sxs-lookup"><span data-stu-id="b18d2-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="b18d2-148">Bu, Gönder düğmesinin varsayılan davranışını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="b18d2-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="b18d2-149">Serileştirme işlevi, form verilerini ad/değer çiftlerine seri **hale** getirir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="b18d2-150">Form verilerini sunucuya göndermek için `$.post()`çağırın.</span><span class="sxs-lookup"><span data-stu-id="b18d2-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="b18d2-151">İstek tamamlandığında, `.success()` veya `.error()` işleyicisi kullanıcıya uygun bir ileti gösterir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="b18d2-152">Basit türler gönderiliyor</span><span class="sxs-lookup"><span data-stu-id="b18d2-152">Sending Simple Types</span></span>

<span data-ttu-id="b18d2-153">Önceki bölümlerde, bir model sınıfının örneğine bir Web API 'SI seri durumdan çıkarılan karmaşık bir tür gönderdik.</span><span class="sxs-lookup"><span data-stu-id="b18d2-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="b18d2-154">Ayrıca, bir dize gibi basit türler de gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b18d2-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="b18d2-155">Basit bir tür göndermeden önce, bunun yerine değeri karmaşık bir türde kaydırmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="b18d2-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="b18d2-156">Bu, sunucu tarafında model doğrulamanın avantajlarından yararlanmanızı sağlar ve gerekirse modelinizi genişletmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>

<span data-ttu-id="b18d2-157">Basit bir tür göndermek için temel adımlar aynıdır, ancak iki hafif farklılık vardır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="b18d2-158">İlk olarak, denetleyicide, parametre adını **Frombody** özniteliğiyle tasarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="b18d2-159">Web API 'SI varsayılan olarak istek URI 'sinden basit türler almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="b18d2-160">**Frombody** özniteliği, Web API 'sinin istek gövdesinden değeri okumasını söyler.</span><span class="sxs-lookup"><span data-stu-id="b18d2-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="b18d2-161">Web API 'SI, yanıt gövdesini en çok bir kez okur. bu nedenle, bir eylemin yalnızca bir parametresi istek gövdesinden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="b18d2-162">İstek gövdesinden birden çok değer almanız gerekiyorsa, karmaşık bir tür tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b18d2-162">If you need to get multiple values from the request body, define a complex type.</span></span>

<span data-ttu-id="b18d2-163">İkinci olarak, istemcinin değeri aşağıdaki biçimle gönderebilmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b18d2-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="b18d2-164">Özel olarak, basit bir tür için ad/değer çiftinin ad kısmı boş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b18d2-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="b18d2-165">Tüm tarayıcılar bunu HTML formları için desteklemez, ancak bu biçimi komut dosyasında aşağıdaki gibi oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="b18d2-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="b18d2-166">Örnek bir form aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b18d2-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="b18d2-167">Form değerini göndermek için komut dosyası aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="b18d2-168">Önceki betikten tek fark, **Post** işlevine geçirilen bağımsız değişkendir.</span><span class="sxs-lookup"><span data-stu-id="b18d2-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="b18d2-169">Basit türden bir diziyi göndermek için aynı yaklaşımı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b18d2-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="b18d2-170">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b18d2-170">Additional Resources</span></span>

[<span data-ttu-id="b18d2-171">Bölüm 2: dosya yükleme ve çok parçalı MIME</span><span class="sxs-lookup"><span data-stu-id="b18d2-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
