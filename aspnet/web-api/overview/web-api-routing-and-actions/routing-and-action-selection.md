---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API 'de yönlendirme ve eylem seçimi | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554889"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="045ed-102">ASP.NET Web API 'sinde yönlendirme ve eylem seçimi</span><span class="sxs-lookup"><span data-stu-id="045ed-102">Routing and Action Selection in ASP.NET Web API</span></span>

<span data-ttu-id="045ed-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="045ed-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="045ed-104">Bu makalede, ASP.NET Web API 'sinin bir denetleyicideki belirli bir eyleme HTTP isteğini nasıl yönlendirdiğini açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="045ed-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="045ed-105">Yönlendirmeye yönelik üst düzey bir genel bakış için bkz. [ASP.NET Web API 'de yönlendirme](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="045ed-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="045ed-106">Bu makale, yönlendirme sürecinin ayrıntılarına bakar.</span><span class="sxs-lookup"><span data-stu-id="045ed-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="045ed-107">Bir Web API projesi oluşturur ve bazı isteklerin istediğiniz şekilde yönlendirilmeyeceğini görürseniz, bu makalede yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="045ed-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="045ed-108">Yönlendirme üç ana aşamaya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="045ed-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="045ed-109">URI ile bir yol şablonuna eşleme.</span><span class="sxs-lookup"><span data-stu-id="045ed-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="045ed-110">Denetleyici seçiliyor.</span><span class="sxs-lookup"><span data-stu-id="045ed-110">Selecting a controller.</span></span>
3. <span data-ttu-id="045ed-111">Bir eylem seçme.</span><span class="sxs-lookup"><span data-stu-id="045ed-111">Selecting an action.</span></span>

<span data-ttu-id="045ed-112">İşlemin bazı parçalarını kendi özel davranışlarınız ile değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="045ed-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="045ed-113">Bu makalede, varsayılan davranışı açıklıyorum.</span><span class="sxs-lookup"><span data-stu-id="045ed-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="045ed-114">Sonda, davranışı özelleştirebileceğiniz yerleri de göz önünde koydum.</span><span class="sxs-lookup"><span data-stu-id="045ed-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="045ed-115">Rota şablonları</span><span class="sxs-lookup"><span data-stu-id="045ed-115">Route Templates</span></span>

<span data-ttu-id="045ed-116">Bir yol şablonu bir URI yoluna benzer, ancak küme ayraçları ile gösterilen yer tutucu değerlerine sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="045ed-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="045ed-117">Bir yol oluşturduğunuzda, yer tutucuların bazıları veya tümü için varsayılan değer sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="045ed-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="045ed-118">Ayrıca, bir URI segmentinin bir yer tutucu ile nasıl eşleşeceğini kısıtlayan kısıtlamalar da sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="045ed-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="045ed-119">Çerçeve, URI yolundaki kesimleri şablonla eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="045ed-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="045ed-120">Şablondaki değişmez değerler tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="045ed-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="045ed-121">Bir yer tutucu, kısıtlama belirtmediğiniz müddetçe herhangi bir değerle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="045ed-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="045ed-122">Çerçeve, URI 'nin ana bilgisayar adı veya sorgu parametreleri gibi diğer bölümleriyle eşleşmez.</span><span class="sxs-lookup"><span data-stu-id="045ed-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="045ed-123">Framework, yol tablosundaki URI ile eşleşen ilk yolu seçer.</span><span class="sxs-lookup"><span data-stu-id="045ed-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="045ed-124">İki özel yer tutucu vardır: "{Controller}" ve "{Action}".</span><span class="sxs-lookup"><span data-stu-id="045ed-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="045ed-125">"{Controller}" denetleyicinin adını sağlar.</span><span class="sxs-lookup"><span data-stu-id="045ed-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="045ed-126">"{Action}", eylemin adını sağlar.</span><span class="sxs-lookup"><span data-stu-id="045ed-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="045ed-127">Web API 'de, her zamanki kural "{Action}" öğesini atlayamaz.</span><span class="sxs-lookup"><span data-stu-id="045ed-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="045ed-128">Varsayılanları</span><span class="sxs-lookup"><span data-stu-id="045ed-128">Defaults</span></span>

<span data-ttu-id="045ed-129">Varsayılan değer sağlarsanız, yol, bu kesimleri eksik olan bir URI ile eşleştirecektir.</span><span class="sxs-lookup"><span data-stu-id="045ed-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="045ed-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="045ed-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="045ed-131">URI 'Ler `http://localhost/api/products/all` ve `http://localhost/api/products` önceki rotayla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="045ed-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="045ed-132">İkinci URI 'de, eksik `{category}` kesimine `all`varsayılan değer atanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="045ed-133">Yol sözlüğü</span><span class="sxs-lookup"><span data-stu-id="045ed-133">Route Dictionary</span></span>

<span data-ttu-id="045ed-134">Çerçeve bir URI için eşleşme bulursa, her yer tutucunun değerini içeren bir sözlük oluşturur.</span><span class="sxs-lookup"><span data-stu-id="045ed-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="045ed-135">Anahtarlar, küme ayraçları dahil değil yer tutucu adlarıdır.</span><span class="sxs-lookup"><span data-stu-id="045ed-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="045ed-136">Değerler URI yolundan veya varsayılandan alınır.</span><span class="sxs-lookup"><span data-stu-id="045ed-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="045ed-137">Sözlük **ıhttproutedata** nesnesinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="045ed-138">Bu rota eşleştirme aşamasında, özel "{Controller}" ve "{Action}" yer tutucuları, diğer yer tutucuları gibi değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="045ed-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="045ed-139">Yalnızca diğer değerlerle sözlükte depolanırlar.</span><span class="sxs-lookup"><span data-stu-id="045ed-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="045ed-140">Varsayılan, RouteParameter özel değerine sahip olabilir **. Isteğe bağlı**.</span><span class="sxs-lookup"><span data-stu-id="045ed-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="045ed-141">Bir yer tutucu bu değere atanmışsa, değer yol sözlüğüne eklenmez.</span><span class="sxs-lookup"><span data-stu-id="045ed-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="045ed-142">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="045ed-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="045ed-143">"API/Products" URI yolu için yol sözlüğü şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="045ed-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="045ed-144">Denetleyici: "Ürünler"</span><span class="sxs-lookup"><span data-stu-id="045ed-144">controller: "products"</span></span>
- <span data-ttu-id="045ed-145">Kategori: "tümü"</span><span class="sxs-lookup"><span data-stu-id="045ed-145">category: "all"</span></span>

<span data-ttu-id="045ed-146">Bununla birlikte, "API/Products/Toys/123" için yol sözlüğü şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="045ed-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="045ed-147">Denetleyici: "Ürünler"</span><span class="sxs-lookup"><span data-stu-id="045ed-147">controller: "products"</span></span>
- <span data-ttu-id="045ed-148">Kategori: "Toys"</span><span class="sxs-lookup"><span data-stu-id="045ed-148">category: "toys"</span></span>
- <span data-ttu-id="045ed-149">Kimlik: "123"</span><span class="sxs-lookup"><span data-stu-id="045ed-149">id: "123"</span></span>

<span data-ttu-id="045ed-150">Varsayılanlar, yol şablonunda hiçbir yerde görünmeyen bir değer içerebilir.</span><span class="sxs-lookup"><span data-stu-id="045ed-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="045ed-151">Yol eşleşiyorsa, bu değer sözlükte depolanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="045ed-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="045ed-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="045ed-153">URI yolu "api/root/8" ise, sözlük iki değer içerir:</span><span class="sxs-lookup"><span data-stu-id="045ed-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="045ed-154">Denetleyici: "müşteriler"</span><span class="sxs-lookup"><span data-stu-id="045ed-154">controller: "customers"</span></span>
- <span data-ttu-id="045ed-155">Kimlik: "8"</span><span class="sxs-lookup"><span data-stu-id="045ed-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="045ed-156">Denetleyici seçme</span><span class="sxs-lookup"><span data-stu-id="045ed-156">Selecting a Controller</span></span>

<span data-ttu-id="045ed-157">Denetleyici seçimi **IHttpControllerSelector. SelectController** yöntemi tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="045ed-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="045ed-158">Bu yöntem bir **HttpRequestMessage** örneği alır ve bir **httpcontrollerdescriptor**döndürür.</span><span class="sxs-lookup"><span data-stu-id="045ed-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="045ed-159">Varsayılan uygulama **DefaultHttpControllerSelector** sınıfı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="045ed-160">Bu sınıf, basit bir algoritma kullanır:</span><span class="sxs-lookup"><span data-stu-id="045ed-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="045ed-161">"Denetleyici" anahtarı için yol sözlüğüne bakın.</span><span class="sxs-lookup"><span data-stu-id="045ed-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="045ed-162">Bu anahtar için değeri alın ve denetleyicinin tür adını almak için "Controller" dizesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="045ed-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="045ed-163">Bu tür adıyla bir Web API denetleyicisi arayın.</span><span class="sxs-lookup"><span data-stu-id="045ed-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="045ed-164">Örneğin, yol sözlüğü anahtar-değer çifti "denetleyici" = "Ürünler" içeriyorsa, denetleyici türü "ProductsController" olur.</span><span class="sxs-lookup"><span data-stu-id="045ed-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="045ed-165">Eşleşen bir tür veya birden fazla eşleşme yoksa, çerçeve istemciye bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="045ed-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="045ed-166">3\. adım için, **DefaultHttpControllerSelector** Web API denetleyici türlerinin listesini almak Için **ıhttpcontrollertyperesolver** arabirimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="045ed-167">**Ihttpcontrollertyperesolver** 'in varsayılan uygulaması, (a) **ıhttpcontroller**uygulayan tüm genel sınıfları döndürür, (b) soyut değildir ve (c) "Controller" ile biten bir ada sahiptir.</span><span class="sxs-lookup"><span data-stu-id="045ed-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="045ed-168">Eylem seçimi</span><span class="sxs-lookup"><span data-stu-id="045ed-168">Action Selection</span></span>

<span data-ttu-id="045ed-169">Denetleyiciyi seçtikten sonra Framework, **ıhttpactionselector. SelectAction** yöntemini çağırarak eylemi seçer.</span><span class="sxs-lookup"><span data-stu-id="045ed-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="045ed-170">Bu yöntem bir **HttpControllerContext** alır ve bir **HttpActionDescriptor**döndürür.</span><span class="sxs-lookup"><span data-stu-id="045ed-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="045ed-171">Varsayılan uygulama **ApiControllerActionSelector** sınıfı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="045ed-172">Bir eylem seçmek için, aşağıdakilere bakar:</span><span class="sxs-lookup"><span data-stu-id="045ed-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="045ed-173">İsteğin HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="045ed-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="045ed-174">Varsa, yol şablonunda "{Action}" yer tutucusu.</span><span class="sxs-lookup"><span data-stu-id="045ed-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="045ed-175">Denetleyicideki eylemlerin parametreleri.</span><span class="sxs-lookup"><span data-stu-id="045ed-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="045ed-176">Seçim algoritmasına bakmadan önce, denetleyici eylemleriyle ilgili bazı şeyleri anladık.</span><span class="sxs-lookup"><span data-stu-id="045ed-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="045ed-177">**Denetleyicideki hangi Yöntemler "eylemler" olarak değerlendirilir?**</span><span class="sxs-lookup"><span data-stu-id="045ed-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="045ed-178">Bir eylem seçerken, çerçeve yalnızca denetleyicideki ortak örnek yöntemlerine bakar.</span><span class="sxs-lookup"><span data-stu-id="045ed-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="045ed-179">Ayrıca, ["özel ad"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) yöntemlerini (oluşturucular, olaylar, operatör aşırı yüklemeleri vs.) ve **Apicontroller** sınıfından devralınan yöntemleri dışlar.</span><span class="sxs-lookup"><span data-stu-id="045ed-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="045ed-180">**HTTP yöntemleri.**</span><span class="sxs-lookup"><span data-stu-id="045ed-180">**HTTP Methods.**</span></span> <span data-ttu-id="045ed-181">Framework yalnızca isteğin HTTP yöntemiyle eşleşen eylemleri seçer, şöyle belirlenir:</span><span class="sxs-lookup"><span data-stu-id="045ed-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="045ed-182">HTTP yöntemini bir özniteliğiyle belirtebilirsiniz: **Acceptverbs**, **httpdelete**, **HttpGet**, **httphead**, **HttpOptions**, **httppatch**, **HttpPost**veya **httpput**.</span><span class="sxs-lookup"><span data-stu-id="045ed-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="045ed-183">Aksi halde, denetleyici yönteminin adı "Get", "Post", "put", "Delete", "Head", "Options" veya "Patch" ile başlıyorsa ve bu HTTP yöntemini desteklediği kurala göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="045ed-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="045ed-184">Yukarıdakilerden hiçbiri, yöntemi GÖNDERIYI destekler.</span><span class="sxs-lookup"><span data-stu-id="045ed-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="045ed-185">**Parametre bağlamaları.**</span><span class="sxs-lookup"><span data-stu-id="045ed-185">**Parameter Bindings.**</span></span> <span data-ttu-id="045ed-186">Bir parametre bağlama, Web API 'sinin bir parametre için bir değer oluşturmasıdır.</span><span class="sxs-lookup"><span data-stu-id="045ed-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="045ed-187">Parametre bağlama için varsayılan kural aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="045ed-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="045ed-188">Basit türler URI 'den alınır.</span><span class="sxs-lookup"><span data-stu-id="045ed-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="045ed-189">Karmaşık türler, istek gövdesinden alınır.</span><span class="sxs-lookup"><span data-stu-id="045ed-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="045ed-190">Basit türler [.NET Framework ilkel türler](https://msdn.microsoft.com/library/system.type.isprimitive), ayrıca **DateTime**, **Decimal**, Guid, **dize**ve **TimeSpan** **değerleri**içerir.</span><span class="sxs-lookup"><span data-stu-id="045ed-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="045ed-191">Her eylem için, en fazla bir parametre istek gövdesini okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="045ed-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="045ed-192">Varsayılan bağlama kurallarını geçersiz kılmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="045ed-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="045ed-193">Bkz. bir [çocuk altındaki WebAPI parametre bağlama](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span><span class="sxs-lookup"><span data-stu-id="045ed-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>

<span data-ttu-id="045ed-194">Bu arka plan ile eylem seçim algoritması aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="045ed-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="045ed-195">Denetleyicide HTTP istek yöntemiyle eşleşen tüm eylemlerin bir listesini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="045ed-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="045ed-196">Yol sözlüğünde bir "Action" girişi varsa, adı bu değerle eşleşmeyen eylemleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="045ed-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="045ed-197">Aşağıdaki gibi eylem parametrelerini URI ile eşleştirmeye çalışın:</span><span class="sxs-lookup"><span data-stu-id="045ed-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="045ed-198">Her eylem için, bağlamanın URI 'den parametreyi aldığı basit türde parametrelerin bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="045ed-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="045ed-199">İsteğe bağlı parametreleri dışlayın.</span><span class="sxs-lookup"><span data-stu-id="045ed-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="045ed-200">Bu listeden, yol sözlüğünde veya URI sorgu dizesinde her bir parametre adı için bir eşleşme bulmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="045ed-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="045ed-201">Eşleşmeler büyük/küçük harfe duyarlıdır ve parametre sırasına bağlı değildir.</span><span class="sxs-lookup"><span data-stu-id="045ed-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="045ed-202">Listedeki her parametrenin URI 'de eşleşen bir eylem seçin.</span><span class="sxs-lookup"><span data-stu-id="045ed-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="045ed-203">Bu ölçütlere uyan birden fazla eylem varsa, en fazla parametre eşleştirmelerle birini seçin.</span><span class="sxs-lookup"><span data-stu-id="045ed-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="045ed-204">**[Nonactıon]** özniteliğiyle eylemleri yoksayın.</span><span class="sxs-lookup"><span data-stu-id="045ed-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="045ed-205">Adım #3, büyük olasılıkla en karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="045ed-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="045ed-206">Temel düşünce, bir parametrenin değerini URI 'den, istek gövdesinden veya özel bir bağlamadan alabilir.</span><span class="sxs-lookup"><span data-stu-id="045ed-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="045ed-207">URI 'den gelen parametreler için, URI 'nin gerçekten bu parametre için bir değer (yol sözlüğü aracılığıyla) ya da sorgu dizesinde bir değer içerdiğinden emin olmak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="045ed-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="045ed-208">Örneğin, aşağıdaki eylemi göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="045ed-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="045ed-209">*ID* parametresi URI 'ye bağlanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="045ed-210">Bu nedenle, bu eylem yalnızca yol sözlüğünde veya sorgu dizesinde "ID" değeri içeren bir URI ile eşleşemez.</span><span class="sxs-lookup"><span data-stu-id="045ed-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="045ed-211">İsteğe bağlı parametreler, isteğe bağlı oldukları için bir özel durumdur.</span><span class="sxs-lookup"><span data-stu-id="045ed-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="045ed-212">İsteğe bağlı bir parametre için bağlama URI 'den değeri alamazsanız Tamam olur.</span><span class="sxs-lookup"><span data-stu-id="045ed-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="045ed-213">Karmaşık türler, farklı bir nedenden dolayı özel durumdur.</span><span class="sxs-lookup"><span data-stu-id="045ed-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="045ed-214">Karmaşık bir tür yalnızca özel bir bağlama aracılığıyla URI 'ye bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="045ed-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="045ed-215">Ancak bu durumda, parametrenin belirli bir URI 'ye bağlanıp bağlanamayacağını önceden bilemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="045ed-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="045ed-216">Bunu öğrenmek için bağlamayı çağırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="045ed-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="045ed-217">Seçim algoritmasının hedefi, herhangi bir bağlama çağırmadan önce statik açıklamadan bir eylem seçmektir.</span><span class="sxs-lookup"><span data-stu-id="045ed-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="045ed-218">Bu nedenle, karmaşık türler eşleşen algoritmadan dışlanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="045ed-219">Eylem seçildikten sonra tüm parametre bağlamaları çağrılır.</span><span class="sxs-lookup"><span data-stu-id="045ed-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="045ed-220">Özet:</span><span class="sxs-lookup"><span data-stu-id="045ed-220">Summary:</span></span>

- <span data-ttu-id="045ed-221">Eylemin, isteğin HTTP yöntemiyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="045ed-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="045ed-222">Varsa, yol sözlüğünde eylem adı "Action" girdisiyle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="045ed-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="045ed-223">İşlemin her parametresi için parametre URI 'den alınsaydı, parametre adının yol sözlüğünde ya da URI sorgu dizesinde bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="045ed-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="045ed-224">(Karmaşık türler içeren isteğe bağlı parametreler ve parametreler dışarıda bırakılır.)</span><span class="sxs-lookup"><span data-stu-id="045ed-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="045ed-225">En fazla parametre sayısını eşleştirmeye çalışın.</span><span class="sxs-lookup"><span data-stu-id="045ed-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="045ed-226">En iyi eşleşme parametresi olmayan bir yöntem olabilir.</span><span class="sxs-lookup"><span data-stu-id="045ed-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="045ed-227">Genişletilmiş örnek</span><span class="sxs-lookup"><span data-stu-id="045ed-227">Extended Example</span></span>

<span data-ttu-id="045ed-228">Yolların</span><span class="sxs-lookup"><span data-stu-id="045ed-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="045ed-229">Denetleyici:</span><span class="sxs-lookup"><span data-stu-id="045ed-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="045ed-230">HTTP isteği:</span><span class="sxs-lookup"><span data-stu-id="045ed-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="045ed-231">Rota eşleştirme</span><span class="sxs-lookup"><span data-stu-id="045ed-231">Route Matching</span></span>

<span data-ttu-id="045ed-232">URI, "DefaultApi" adlı yol ile eşleşiyor.</span><span class="sxs-lookup"><span data-stu-id="045ed-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="045ed-233">Yol sözlüğü aşağıdaki girişleri içerir:</span><span class="sxs-lookup"><span data-stu-id="045ed-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="045ed-234">Denetleyici: "Ürünler"</span><span class="sxs-lookup"><span data-stu-id="045ed-234">controller: "products"</span></span>
- <span data-ttu-id="045ed-235">Kimlik: "1"</span><span class="sxs-lookup"><span data-stu-id="045ed-235">id: "1"</span></span>

<span data-ttu-id="045ed-236">Yol sözlüğü sorgu dizesi parametreleri, "sürüm" ve "Ayrıntılar" içeremez, ancak bunlar eylem seçimi sırasında göz önünde bulundurulacaktır.</span><span class="sxs-lookup"><span data-stu-id="045ed-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="045ed-237">Denetleyici seçimi</span><span class="sxs-lookup"><span data-stu-id="045ed-237">Controller Selection</span></span>

<span data-ttu-id="045ed-238">Yol sözlüğündeki "denetleyici" girdisinden, denetleyici türü `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="045ed-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="045ed-239">Eylem seçimi</span><span class="sxs-lookup"><span data-stu-id="045ed-239">Action Selection</span></span>

<span data-ttu-id="045ed-240">HTTP isteği bir GET isteği.</span><span class="sxs-lookup"><span data-stu-id="045ed-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="045ed-241">GET 'i destekleyen denetleyici eylemleri `GetAll`, `GetById`ve `FindProductsByName`.</span><span class="sxs-lookup"><span data-stu-id="045ed-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="045ed-242">Yol sözlüğü "eylem" için bir giriş içermiyor, bu nedenle eylem adıyla eşleşmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="045ed-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="045ed-243">Ardından, eylemler için parametre adlarını eşleştirmeye çalışırız ve yalnızca GET eylemlerine bakmaya çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="045ed-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="045ed-244">Eylem</span><span class="sxs-lookup"><span data-stu-id="045ed-244">Action</span></span> | <span data-ttu-id="045ed-245">Eşleştirilecek parametreler</span><span class="sxs-lookup"><span data-stu-id="045ed-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="045ed-246">yok</span><span class="sxs-lookup"><span data-stu-id="045ed-246">none</span></span> |
| `GetById` | <span data-ttu-id="045ed-247">numarasını</span><span class="sxs-lookup"><span data-stu-id="045ed-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="045ed-248">ada</span><span class="sxs-lookup"><span data-stu-id="045ed-248">"name"</span></span> |

<span data-ttu-id="045ed-249">İsteğe bağlı bir parametre olduğu için `GetById` *Sürüm* parametresinin değerlendirilmediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="045ed-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="045ed-250">`GetAll` yöntemi, önemli ölçüde eşleşir.</span><span class="sxs-lookup"><span data-stu-id="045ed-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="045ed-251">Yol sözlüğü "ID" içerdiğinden `GetById` yöntemi de eşleşir.</span><span class="sxs-lookup"><span data-stu-id="045ed-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="045ed-252">`FindProductsByName` yöntemi eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="045ed-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="045ed-253">`GetById` yöntemi, bir parametresiyle eşleştiğinden, `GetAll`için hiçbir parametre olmadığından WINS.</span><span class="sxs-lookup"><span data-stu-id="045ed-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="045ed-254">Yöntemi aşağıdaki parametre değerleriyle çağrılır:</span><span class="sxs-lookup"><span data-stu-id="045ed-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="045ed-255">*kimlik* = 1</span><span class="sxs-lookup"><span data-stu-id="045ed-255">*id* = 1</span></span>
- <span data-ttu-id="045ed-256">*Sürüm* = 1,5</span><span class="sxs-lookup"><span data-stu-id="045ed-256">*version* = 1.5</span></span>

<span data-ttu-id="045ed-257">*Sürüm* seçim algoritmasında kullanılmasa da, PARAMETRENIN değeri URI sorgu dizesinden geliyor olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="045ed-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="045ed-258">Uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="045ed-258">Extension Points</span></span>

<span data-ttu-id="045ed-259">Web API 'SI, yönlendirme sürecinin bazı bölümleri için uzantı noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="045ed-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="045ed-260">Arabirim</span><span class="sxs-lookup"><span data-stu-id="045ed-260">Interface</span></span> | <span data-ttu-id="045ed-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="045ed-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="045ed-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="045ed-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="045ed-263">Denetleyiciyi seçer.</span><span class="sxs-lookup"><span data-stu-id="045ed-263">Selects the controller.</span></span> |
| <span data-ttu-id="045ed-264">**Ihttpcontrollertyperesolver**</span><span class="sxs-lookup"><span data-stu-id="045ed-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="045ed-265">Denetleyici türleri listesini alır.</span><span class="sxs-lookup"><span data-stu-id="045ed-265">Gets the list of controller types.</span></span> <span data-ttu-id="045ed-266">**DefaultHttpControllerSelector** bu listeden denetleyici türünü seçer.</span><span class="sxs-lookup"><span data-stu-id="045ed-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="045ed-267">**Ibirleştiricliesresolver**</span><span class="sxs-lookup"><span data-stu-id="045ed-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="045ed-268">Proje derlemelerinin listesini alır.</span><span class="sxs-lookup"><span data-stu-id="045ed-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="045ed-269">**Ihttpcontrollertyperesolver** arabirimi, denetleyici türlerini bulmak için bu listeyi kullanır.</span><span class="sxs-lookup"><span data-stu-id="045ed-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="045ed-270">**Ihttpcontrolleretkinleştirici**</span><span class="sxs-lookup"><span data-stu-id="045ed-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="045ed-271">Yeni denetleyici örnekleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="045ed-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="045ed-272">**Ihttpactionselector**</span><span class="sxs-lookup"><span data-stu-id="045ed-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="045ed-273">Eylemi seçer.</span><span class="sxs-lookup"><span data-stu-id="045ed-273">Selects the action.</span></span> |
| <span data-ttu-id="045ed-274">**Ihttpactionınvoker**</span><span class="sxs-lookup"><span data-stu-id="045ed-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="045ed-275">Eylemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="045ed-275">Invokes the action.</span></span> |

<span data-ttu-id="045ed-276">Bu arabirimlerin herhangi birine yönelik uygulamanızı sağlamak için **HttpConfiguration** nesnesindeki **Hizmetler** koleksiyonunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="045ed-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
