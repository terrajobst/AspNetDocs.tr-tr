---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 ' de öznitelik yönlendirme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554987"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="d8d1e-102">ASP.NET Web API 2 ' de öznitelik yönlendirme</span><span class="sxs-lookup"><span data-stu-id="d8d1e-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="d8d1e-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d8d1e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d8d1e-104">*Yönlendirme* , Web API 'sinin bir eyleme bir URI ile eşleşmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="d8d1e-105">Web API 2 ' de *öznitelik yönlendirme*adı verilen yeni bir yönlendirme türü desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="d8d1e-106">Adından da anlaşılacağı gibi, öznitelik yönlendirme yolları tanımlamak için öznitelikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="d8d1e-107">Öznitelik yönlendirme, Web API 'nizin URI 'Leri üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="d8d1e-108">Örneğin, kaynakların hiyerarşilerini tanımlayan URI 'Leri kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="d8d1e-109">Kural tabanlı yönlendirme olarak adlandırılan daha önceki yönlendirmenin stili hala tam olarak desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="d8d1e-110">Aslında, her iki tekniği de aynı projede birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="d8d1e-111">Bu konu, öznitelik yönlendirmeyi nasıl etkinleştireceğinizi ve öznitelik yönlendirme için çeşitli seçenekleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="d8d1e-112">Öznitelik yönlendirme kullanan bir uçtan uca öğretici için bkz. [Web API 2 ' de öznitelik yönlendirme ile REST API oluşturma](create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="d8d1e-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8d1e-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d8d1e-113">Prerequisites</span></span>

<span data-ttu-id="d8d1e-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional veya Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="d8d1e-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="d8d1e-115">Alternatif olarak, gerekli paketleri yüklemek için NuGet Paket Yöneticisi 'Ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="d8d1e-116">Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="d8d1e-117">Paket Yöneticisi konsolu penceresinde aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="d8d1e-118">Neden öznitelik yönlendirme?</span><span class="sxs-lookup"><span data-stu-id="d8d1e-118">Why Attribute Routing?</span></span>

<span data-ttu-id="d8d1e-119">Web API 'sinin ilk sürümü *kural tabanlı* yönlendirme kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="d8d1e-120">Bu yönlendirme türünde, temel olarak parametreli dizeler olan bir veya daha fazla yol şablonu tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="d8d1e-121">Çerçeve bir istek aldığında, URI ile yol şablonunda eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="d8d1e-122">(Kural tabanlı yönlendirme hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de yönlendirme](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="d8d1e-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="d8d1e-123">Kural tabanlı yönlendirmenin bir avantajı, şablonların tek bir yerde tanımlanması ve yönlendirme kurallarının tüm denetleyicilerde tutarlı bir şekilde uygulanması.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="d8d1e-124">Ne yazık ki, kural tabanlı yönlendirme, yeniden gerçekleştirilen API 'lerde ortak olan belirli URI desenlerini desteklemeyi zorlaştırır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="d8d1e-125">Örneğin, kaynaklar genellikle alt kaynaklar içerir: müşterilerin siparişi vardır, filmlerde aktörler, kitap yazarları vardır ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="d8d1e-126">Bu ilişkileri yansıtan URI 'Ler oluşturmak doğal bir şekilde yapılır:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="d8d1e-127">Bu tür URI 'nin kural tabanlı yönlendirme kullanılarak oluşturulması zordur.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="d8d1e-128">Yapılabilse de, çok sayıda denetleyiciniz veya kaynak türü varsa sonuçlar düzgün ölçeklenmez.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="d8d1e-129">Öznitelik yönlendirme ile bu URI için bir yol tanımlamak önemsiz bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="d8d1e-130">Yalnızca denetleyici eylemine bir öznitelik eklersiniz:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="d8d1e-131">Öznitelik yönlendirmenin kolay hale getiren diğer bazı desenler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="d8d1e-132">**API sürümü oluşturma**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-132">**API versioning**</span></span>

<span data-ttu-id="d8d1e-133">Bu örnekte, "/api/v1/Products" farklı bir denetleyiciye "/api/v2/Products" olarak yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="d8d1e-134">**Aşırı yüklenmiş URI kesimleri**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="d8d1e-135">Bu örnekte, "1" bir sıra numarasıdır, ancak "bekliyor" bir koleksiyonla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="d8d1e-136">**Birden çok parametre türü**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-136">**Multiple parameter types**</span></span>

<span data-ttu-id="d8d1e-137">Bu örnekte, "1" bir sıra numarasıdır, ancak "2013/06/16" bir tarihi belirtir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="d8d1e-138">Öznitelik yönlendirmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d8d1e-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="d8d1e-139">Öznitelik yönlendirmeyi etkinleştirmek için yapılandırma sırasında **MapHttpAttributeRoutes** çağırın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="d8d1e-140">Bu genişletme yöntemi **System. Web. http. HttpConfigurationExtensions** sınıfında tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="d8d1e-141">Öznitelik yönlendirme, [kural tabanlı](routing-in-aspnet-web-api.md) yönlendirme ile birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="d8d1e-142">Kural tabanlı yolları tanımlamak için **Maphttproute** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="d8d1e-143">Web API 'sini yapılandırma hakkında daha fazla bilgi için bkz. [ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)' yi yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="d8d1e-144">Note: Web API 1 ' den geçiş</span><span class="sxs-lookup"><span data-stu-id="d8d1e-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="d8d1e-145">Web API 'si 2 ' den önce, Web API proje şablonları şunun gibi kod üretti:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="d8d1e-146">Öznitelik yönlendirme etkinse, bu kod bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="d8d1e-147">Öznitelik yönlendirmeyi kullanmak için var olan bir Web API projesini yükseltirseniz, bu yapılandırma kodunu aşağıdaki şekilde güncelleştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="d8d1e-148">Daha fazla bilgi için bkz. [ASP.net Hosting Ile Web API 'Sini yapılandırma](../advanced/configuring-aspnet-web-api.md#webhost).</span><span class="sxs-lookup"><span data-stu-id="d8d1e-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="d8d1e-149">Rota öznitelikleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d8d1e-149">Adding Route Attributes</span></span>

<span data-ttu-id="d8d1e-150">Bir öznitelik kullanılarak tanımlanmış bir yol örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="d8d1e-151">&quot;müşteriler/{CustomerID}/Orders&quot; dize, yolun URI şablonudur.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="d8d1e-152">Web API 'SI, istek URI 'sini şablonla eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="d8d1e-153">Bu örnekte, "Customers" ve "Orders" değişmez kesimlerdir ve "{CustomerID}" bir değişken parametresidir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="d8d1e-154">Aşağıdaki URI 'Ler Bu şablonla eşleşir:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="d8d1e-155">Bu konunun ilerleyen kısımlarında açıklanan [kısıtlamaları](#constraints)kullanarak eşleştirmeyi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="d8d1e-156">Yol şablonundaki &quot;{CustomerID}&quot; parametresinin, yöntemindeki *CustomerID* parametresinin adıyla eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="d8d1e-157">Web API 'SI, denetleyici eylemini istediğinde, yol parametrelerini bağlamayı dener.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="d8d1e-158">Örneğin, URI `http://example.com/customers/1/orders`, Web API 'si "1" değerini eylemde *MüşteriNo* parametresine bağlamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="d8d1e-159">Bir URI şablonunda çeşitli parametreler bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="d8d1e-160">Route özniteliği olmayan herhangi bir denetleyici yöntemi kural tabanlı yönlendirme kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="d8d1e-161">Bu şekilde, aynı projede her iki yönlendirme türünü de birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d8d1e-162">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="d8d1e-162">HTTP Methods</span></span>

<span data-ttu-id="d8d1e-163">Web API 'SI Ayrıca, isteğin HTTP yöntemine (GET, POST, vb.) göre eylemleri seçer.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="d8d1e-164">Varsayılan olarak, Web API 'SI denetleyici Yöntem adının başlangıcı ile büyük/küçük harf duyarsız bir eşleşme arar.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="d8d1e-165">Örneğin, `PutCustomers` adlı bir denetleyici yöntemi bir HTTP PUT isteğiyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="d8d1e-166">Aşağıdaki özniteliklerle yöntemi tanımlayarak bu kuralı geçersiz kılabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="d8d1e-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="d8d1e-168">**HttpGet**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-168">**[HttpGet]**</span></span>
- <span data-ttu-id="d8d1e-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-169">**[HttpHead]**</span></span>
- <span data-ttu-id="d8d1e-170">**[HttpOptions]**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="d8d1e-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="d8d1e-172">**HttpPost**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-172">**[HttpPost]**</span></span>
- <span data-ttu-id="d8d1e-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="d8d1e-173">**[HttpPut]**</span></span>

<span data-ttu-id="d8d1e-174">Aşağıdaki örnekte CreateBook yöntemi HTTP POST istekleri ile eşlenir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="d8d1e-175">Standart olmayan yöntemler dahil diğer tüm HTTP yöntemleri için, HTTP yöntemlerinin bir listesini alan **Acceptverbs** özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="d8d1e-176">Rota önekleri</span><span class="sxs-lookup"><span data-stu-id="d8d1e-176">Route Prefixes</span></span>

<span data-ttu-id="d8d1e-177">Genellikle, bir denetleyicideki yolların hepsi aynı ön ekiyle başlar.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="d8d1e-178">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="d8d1e-179">**[Routeprefix]** özniteliğini kullanarak tüm denetleyici için ortak bir ön ek ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="d8d1e-180">Yol önekini geçersiz kılmak için method özniteliğinde bir tilde (~) kullanın:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="d8d1e-181">Rota öneki parametreleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="d8d1e-182">Yol kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="d8d1e-182">Route Constraints</span></span>

<span data-ttu-id="d8d1e-183">Yol kısıtlamaları, yol şablonundaki parametrelerin nasıl eşleştirilildiğini kısıtlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="d8d1e-184">Genel sözdizimi &quot;{Parameter: Constraint}&quot;.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="d8d1e-185">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="d8d1e-186">Burada, ilk yol yalnızca URI 'nin &quot;kimliği&quot; segmenti bir tamsayı ise seçilir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="d8d1e-187">Aksi takdirde, ikinci yol seçilir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="d8d1e-188">Aşağıdaki tabloda desteklenen kısıtlamalar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="d8d1e-189">Kısıtlaması</span><span class="sxs-lookup"><span data-stu-id="d8d1e-189">Constraint</span></span> | <span data-ttu-id="d8d1e-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d8d1e-190">Description</span></span> | <span data-ttu-id="d8d1e-191">Örnek</span><span class="sxs-lookup"><span data-stu-id="d8d1e-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d8d1e-192">Alfa</span><span class="sxs-lookup"><span data-stu-id="d8d1e-192">alpha</span></span> | <span data-ttu-id="d8d1e-193">Büyük veya küçük harfli Latin alfabesi karakterleriyle eşleşir (a-z, A-Z)</span><span class="sxs-lookup"><span data-stu-id="d8d1e-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="d8d1e-194">{x:harfler}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-194">{x:alpha}</span></span> |
| <span data-ttu-id="d8d1e-195">bool</span><span class="sxs-lookup"><span data-stu-id="d8d1e-195">bool</span></span> | <span data-ttu-id="d8d1e-196">Bir Boole değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-196">Matches a Boolean value.</span></span> | <span data-ttu-id="d8d1e-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-197">{x:bool}</span></span> |
| <span data-ttu-id="d8d1e-198">datetime</span><span class="sxs-lookup"><span data-stu-id="d8d1e-198">datetime</span></span> | <span data-ttu-id="d8d1e-199">Bir **Tarih saat** değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="d8d1e-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-200">{x:datetime}</span></span> |
| <span data-ttu-id="d8d1e-201">decimal</span><span class="sxs-lookup"><span data-stu-id="d8d1e-201">decimal</span></span> | <span data-ttu-id="d8d1e-202">Ondalık bir değerle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-202">Matches a decimal value.</span></span> | <span data-ttu-id="d8d1e-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-203">{x:decimal}</span></span> |
| <span data-ttu-id="d8d1e-204">çift</span><span class="sxs-lookup"><span data-stu-id="d8d1e-204">double</span></span> | <span data-ttu-id="d8d1e-205">64 bitlik bir kayan nokta değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="d8d1e-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-206">{x:double}</span></span> |
| <span data-ttu-id="d8d1e-207">float</span><span class="sxs-lookup"><span data-stu-id="d8d1e-207">float</span></span> | <span data-ttu-id="d8d1e-208">32 bitlik bir kayan nokta değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="d8d1e-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-209">{x:float}</span></span> |
| <span data-ttu-id="d8d1e-210">guid</span><span class="sxs-lookup"><span data-stu-id="d8d1e-210">guid</span></span> | <span data-ttu-id="d8d1e-211">Bir GUID değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-211">Matches a GUID value.</span></span> | <span data-ttu-id="d8d1e-212">{x:Guid}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-212">{x:guid}</span></span> |
| <span data-ttu-id="d8d1e-213">int</span><span class="sxs-lookup"><span data-stu-id="d8d1e-213">int</span></span> | <span data-ttu-id="d8d1e-214">32 bitlik bir tamsayı değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="d8d1e-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-215">{x:int}</span></span> |
| <span data-ttu-id="d8d1e-216">length</span><span class="sxs-lookup"><span data-stu-id="d8d1e-216">length</span></span> | <span data-ttu-id="d8d1e-217">Belirtilen uzunlukta veya belirtilen uzunluk aralığında olan bir dizeyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="d8d1e-218">{x:length (6)} {x:length (1, 20)}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="d8d1e-219">long</span><span class="sxs-lookup"><span data-stu-id="d8d1e-219">long</span></span> | <span data-ttu-id="d8d1e-220">64 bitlik bir tamsayı değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="d8d1e-221">{x:Long}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-221">{x:long}</span></span> |
| <span data-ttu-id="d8d1e-222">max</span><span class="sxs-lookup"><span data-stu-id="d8d1e-222">max</span></span> | <span data-ttu-id="d8d1e-223">En büyük değere sahip bir tamsayıyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="d8d1e-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-224">{x:max(10)}</span></span> |
| <span data-ttu-id="d8d1e-225">'in</span><span class="sxs-lookup"><span data-stu-id="d8d1e-225">maxlength</span></span> | <span data-ttu-id="d8d1e-226">En fazla uzunluğa sahip bir dizeyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="d8d1e-227">{x:maxlength(10)}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="d8d1e-228">min</span><span class="sxs-lookup"><span data-stu-id="d8d1e-228">min</span></span> | <span data-ttu-id="d8d1e-229">En küçük değeri olan bir tamsayıyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="d8d1e-230">{x:min (10)}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-230">{x:min(10)}</span></span> |
| <span data-ttu-id="d8d1e-231">minLength</span><span class="sxs-lookup"><span data-stu-id="d8d1e-231">minlength</span></span> | <span data-ttu-id="d8d1e-232">En az uzunluğa sahip bir dizeyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="d8d1e-233">{x:minLength (10)}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="d8d1e-234">aralık</span><span class="sxs-lookup"><span data-stu-id="d8d1e-234">range</span></span> | <span data-ttu-id="d8d1e-235">Bir değer aralığı içindeki bir tamsayıyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="d8d1e-236">{x:Range (10, 50)}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="d8d1e-237">Regex</span><span class="sxs-lookup"><span data-stu-id="d8d1e-237">regex</span></span> | <span data-ttu-id="d8d1e-238">Bir normal ifadeyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-238">Matches a regular expression.</span></span> | <span data-ttu-id="d8d1e-239">{x:Regex (^ \d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="d8d1e-240">&quot;en az&quot;gibi bazı kısıtlamaların bağımsız değişkenleri parantez içine alır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="d8d1e-241">Bir parametreye, iki nokta üst üste ile ayırarak birden çok kısıtlama uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="d8d1e-242">Özel yol kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="d8d1e-242">Custom Route Constraints</span></span>

<span data-ttu-id="d8d1e-243">**Ihttprouteconstraint** arabirimini uygulayarak özel yol kısıtlamaları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="d8d1e-244">Örneğin, aşağıdaki kısıtlama bir parametreyi sıfır olmayan bir tamsayı değerine kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="d8d1e-245">Aşağıdaki kod kısıtlamanın nasıl kaydedileceği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="d8d1e-246">Artık bu kısıtlamayı rotalarınızın içinde uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="d8d1e-247">Ayrıca, **IInlineConstraintResolver** arabirimini uygulayarak **DefaultInlineConstraintResolver** sınıfının tamamını de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="d8d1e-248">Bunun yapılması, **IInlineConstraintResolver** uygulamanız özel olarak eklemedikçe yerleşik kısıtlamaların tümünün yerini alır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="d8d1e-249">İsteğe bağlı URI parametreleri ve varsayılan değerler</span><span class="sxs-lookup"><span data-stu-id="d8d1e-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="d8d1e-250">Route parametresine bir soru işareti ekleyerek bir URI parametresini isteğe bağlı hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="d8d1e-251">Bir rota parametresi isteğe bağlıdır, yöntem parametresi için varsayılan bir değer tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="d8d1e-252">Bu örnekte, `/api/books/locale/1033` ve `/api/books/locale` aynı kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="d8d1e-253">Alternatif olarak, yol şablonu içinde aşağıdaki gibi bir varsayılan değer belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="d8d1e-254">Bu, önceki örnekle aynı şekilde neredeyse aynıdır, ancak varsayılan değer uygulandığında bir davranışın küçük bir farkı vardır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="d8d1e-255">İlk örnekte ("{LCID: int?}"), varsayılan 1033 değeri doğrudan yöntem parametresine atanır, bu nedenle parametre bu tam değere sahip olur.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="d8d1e-256">İkinci örnekte ("{LCID: int = 1033}"), varsayılan "1033" değeri model bağlama işleminden geçer.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="d8d1e-257">Varsayılan model-cilt, "1033" değerini 1033 sayısal değerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="d8d1e-258">Ancak, özel bir model Bağlayıcısı takabilirsiniz, bu da farklı bir şey olabilir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="d8d1e-259">(Çoğu durumda, işlem hattınızda özel model ciltleri yoksa, iki form da eşdeğer olacaktır.)</span><span class="sxs-lookup"><span data-stu-id="d8d1e-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="d8d1e-260">Yol adları</span><span class="sxs-lookup"><span data-stu-id="d8d1e-260">Route Names</span></span>

<span data-ttu-id="d8d1e-261">Web API 'sinde, her yolun bir adı vardır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-261">In Web API, every route has a name.</span></span> <span data-ttu-id="d8d1e-262">Yol adları bağlantı oluşturmak için faydalıdır, böylece bir HTTP yanıtında bir bağlantı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="d8d1e-263">Yol adını belirtmek için, özniteliğinde **ad** özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="d8d1e-264">Aşağıdaki örnek, yol adının nasıl ayarlanacağını ve ayrıca bir bağlantı oluştururken yol adının nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="d8d1e-265">Rota sırası</span><span class="sxs-lookup"><span data-stu-id="d8d1e-265">Route Order</span></span>

<span data-ttu-id="d8d1e-266">Framework bir yol ile bir URI ile eşleştirmeye çalıştığında, yolları belirli bir sırada değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="d8d1e-267">Sırayı belirtmek için Route özniteliğinde **Order** özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="d8d1e-268">Daha düşük değerler önce değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-268">Lower values are evaluated first.</span></span> <span data-ttu-id="d8d1e-269">Varsayılan sıra değeri sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-269">The default order value is zero.</span></span>

<span data-ttu-id="d8d1e-270">Toplam sıralama şöyle belirlenir:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="d8d1e-271">Route özniteliğinin **Order** özelliğini karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="d8d1e-272">Yol şablonundaki her bir URI segmentine bakın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="d8d1e-273">Her segment için aşağıdaki şekilde sıralayın:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="d8d1e-274">Değişmez değer kesimleri.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-274">Literal segments.</span></span>
    2. <span data-ttu-id="d8d1e-275">Parametreleri kısıtlamalarla yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="d8d1e-276">Parametreleri kısıtlama olmadan yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="d8d1e-277">Kısıtlamalarla joker karakter parametresi kesimleri.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="d8d1e-278">Kısıtlama olmadan joker karakter parametresi kesimleri.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="d8d1e-279">Bir bağ söz konusu olduğunda, rotalar yol şablonunun büyük/küçük harf duyarsız sıra dizesi karşılaştırması ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) tarafından sıralanır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="d8d1e-280">Aşağıda bir örnek vardır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-280">Here is an example.</span></span> <span data-ttu-id="d8d1e-281">Aşağıdaki denetleyiciyi tanımladığınızı varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d8d1e-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="d8d1e-282">Bu yollar aşağıdaki gibi sıralanır.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="d8d1e-283">Siparişler/Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d8d1e-283">orders/details</span></span>
2. <span data-ttu-id="d8d1e-284">Siparişler/{id}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-284">orders/{id}</span></span>
3. <span data-ttu-id="d8d1e-285">Siparişler/{customerName}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-285">orders/{customerName}</span></span>
4. <span data-ttu-id="d8d1e-286">Siparişler/{\*Date}</span><span class="sxs-lookup"><span data-stu-id="d8d1e-286">orders/{\*date}</span></span>
5. <span data-ttu-id="d8d1e-287">Siparişler/bekliyor</span><span class="sxs-lookup"><span data-stu-id="d8d1e-287">orders/pending</span></span>

<span data-ttu-id="d8d1e-288">"Details" değerinin değişmez bir kesim olduğunu ve "{id}" öncesinde göründüğünü, ancak Order özelliği 1 olduğu **için** "bekliyor" ifadesi son göründüğünü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="d8d1e-289">(Bu örnek, "details" veya "Pending" adlı bir müşteri olmadığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="d8d1e-290">Genel olarak, belirsiz yollardan kaçınmaya çalışın.</span><span class="sxs-lookup"><span data-stu-id="d8d1e-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="d8d1e-291">Bu örnekte, `GetByCustomer` için daha iyi bir yol şablonu "Customers/{customerName}")</span><span class="sxs-lookup"><span data-stu-id="d8d1e-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
