---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: $Select kullanarak $expand, dosyalar ve $value ASP.NET Web API 2 odata'da - ASP.NET 4.x
author: MikeWasson
description: $ İçin genel bakış ve kod örneklerine genişletin, $select, ve $value seçenekleri OData Web API 2'de ASP.NET 4.x.
ms.author: riande
ms.date: 10/11/2013
ms.custom: seoapril2019
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: 8b5d3e87c679a31f1908aa648219ae5c6b701a1f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400704"
---
# <a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a><span data-ttu-id="4551c-103">$Select kullanarak $expand ve ASP.NET Web API 2 OData $value</span><span class="sxs-lookup"><span data-stu-id="4551c-103">Using $select, $expand, and $value in ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="4551c-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4551c-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="4551c-105">$ İçin genel bakış ve kod örneklerine genişletin, $select, ve $value seçenekleri OData Web API 2'de ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="4551c-105">Overview and code samples for the $expand, $select, and $value options in OData Web API 2 for ASP.NET 4.x.</span></span> <span data-ttu-id="4551c-106">Bu seçenekler, bir istemcinin sunucudan geri alır gösterimini kontrol sağlar.</span><span class="sxs-lookup"><span data-stu-id="4551c-106">These options allow a client to control the representation that it gets back from the server.</span></span>

- <span data-ttu-id="4551c-107">**$expand** yanıt satır içi olarak ilgili varlıkları neden olur.</span><span class="sxs-lookup"><span data-stu-id="4551c-107">**$expand** causes related entities to be included inline in the response.</span></span>
- <span data-ttu-id="4551c-108">**$select** yanıta dahil edilecek özellik kümesini seçer.</span><span class="sxs-lookup"><span data-stu-id="4551c-108">**$select** selects a subset of properties to include in the response.</span></span>
- <span data-ttu-id="4551c-109">**$value** ham bir özelliğin değerini alır.</span><span class="sxs-lookup"><span data-stu-id="4551c-109">**$value** gets the raw value of a property.</span></span>

## <a name="example-schema"></a><span data-ttu-id="4551c-110">Şema örneği</span><span class="sxs-lookup"><span data-stu-id="4551c-110">Example Schema</span></span>

<span data-ttu-id="4551c-111">Bu makalede üç varlıklar tanımlayan bir OData hizmeti kullanacağım: Ürün, tedarikçi ve kategorisi.</span><span class="sxs-lookup"><span data-stu-id="4551c-111">For this article, I'll use an OData service that defines three entities: Product, Supplier, and Category.</span></span> <span data-ttu-id="4551c-112">Her ürünün bir kategori ve bir tedarikçi vardır.</span><span class="sxs-lookup"><span data-stu-id="4551c-112">Each product has one category and one supplier.</span></span>

![](using-select-expand-and-value/_static/image1.png)

<span data-ttu-id="4551c-113">Varlık modelleri tanımlayan C# sınıfları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4551c-113">Here are the C# classes that define the entity models:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

<span data-ttu-id="4551c-114">Dikkat `Product` sınıfı tanımlar için gezinme özelliklerinin `Supplier` ve `Category`.</span><span class="sxs-lookup"><span data-stu-id="4551c-114">Notice that the `Product` class defines navigation properties for the `Supplier` and `Category`.</span></span> <span data-ttu-id="4551c-115">`Category` Sınıfı, her kategoride ürünleri için bir gezinti özelliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4551c-115">The `Category` class defines a navigation property for the products in each category.</span></span>

<span data-ttu-id="4551c-116">Bu şema için bir OData uç noktası oluşturmak için Visual Studio 2013 yapı iskelesi açıklandığı kullanın [ASP.NET Web API OData uç noktası oluşturma](odata-v3/creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="4551c-116">To create an OData endpoint for this schema, use the Visual Studio 2013 scaffolding, as described in [Creating an OData Endpoint in ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span></span> <span data-ttu-id="4551c-117">Ürün, kategori ve tedarikçi ayrı denetleyicileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4551c-117">Add separate controllers for Product, Category, and Supplier.</span></span>

## <a name="enabling-expand-and-select"></a><span data-ttu-id="4551c-118">Etkinleştirme $genişletin ve $select</span><span class="sxs-lookup"><span data-stu-id="4551c-118">Enabling $expand and $select</span></span>

<span data-ttu-id="4551c-119">Visual Studio 2013'te Web API OData yapı iskelesi, otomatik olarak $expand destekler ve $select bir denetleyiciyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4551c-119">In Visual Studio 2013, the Web API OData scaffolding creates a controller that automatically supports $expand and $select.</span></span> <span data-ttu-id="4551c-120">Başvuru için işte desteklemeyi $ı gereksinimleri genişletin ve bir denetleyicide $select.</span><span class="sxs-lookup"><span data-stu-id="4551c-120">For reference, here are the requirements to support $expand and $select in a controller.</span></span>

<span data-ttu-id="4551c-121">Koleksiyon denetleyiciye ait `Get` yöntemi döndürmelidir bir **Iqueryable**.</span><span class="sxs-lookup"><span data-stu-id="4551c-121">For collections, the controller's `Get` method must return an **IQueryable**.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

<span data-ttu-id="4551c-122">Tek varlıklar için dönüş bir **SingleResult&lt;T&gt;**, burada T, bir **Iqueryable** , sıfır veya bir varlık içeriyor.</span><span class="sxs-lookup"><span data-stu-id="4551c-122">For single entities, return a **SingleResult&lt;T&gt;**, where T is an **IQueryable** that contains zero or one entities.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

<span data-ttu-id="4551c-123">Ayrıca, tasarlamanız, `Get` yöntemleriyle **[Queryable]** , önceki kod parçacıklarında gösterildiği gibi öznitelik.</span><span class="sxs-lookup"><span data-stu-id="4551c-123">Also, decorate your `Get` methods with the **[Queryable]** attribute, as shown in the previous code snippets.</span></span> <span data-ttu-id="4551c-124">Alternatif olarak, çağrı **EnableQuerySupport** üzerinde **HttpConfiguration** başlangıçta nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4551c-124">Alternatively, call **EnableQuerySupport** on the **HttpConfiguration** object at startup.</span></span> <span data-ttu-id="4551c-125">(Daha fazla bilgi için [OData sorgu seçenekleri etkinleştirme](supporting-odata-query-options.md#enable).)</span><span class="sxs-lookup"><span data-stu-id="4551c-125">(For more information, see [Enabling OData Query Options](supporting-odata-query-options.md#enable).)</span></span>

## <a name="using-expand"></a><span data-ttu-id="4551c-126">Kullanarak $genişletin</span><span class="sxs-lookup"><span data-stu-id="4551c-126">Using $expand</span></span>

<span data-ttu-id="4551c-127">Bir OData varlık veya koleksiyon sorguladığınızda, varsayılan yanıt ilgili varlıkları içermez.</span><span class="sxs-lookup"><span data-stu-id="4551c-127">When you query an OData entity or collection, the default response does not include related entities.</span></span> <span data-ttu-id="4551c-128">Örneğin, varsayılan yanıt kategorileri varlık kümesi için şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="4551c-128">For example, here is the default response for the Categories entity set:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

<span data-ttu-id="4551c-129">Gördüğünüz gibi kategori varlık ürünleri Gezinti bağlantısı olmasına rağmen yanıt herhangi bir ürün içermez.</span><span class="sxs-lookup"><span data-stu-id="4551c-129">As you can see, the response does not include any products, even though the Category entity has a Products navigation link.</span></span> <span data-ttu-id="4551c-130">Ancak istemcinin kullanabileceği $ her kategori için ürünlerin listesini almak için genişletin.</span><span class="sxs-lookup"><span data-stu-id="4551c-130">However, the client can use $expand to get the list of products for each category.</span></span> <span data-ttu-id="4551c-131">$Expand seçeneği isteğinin sorgu dizesinde geçer:</span><span class="sxs-lookup"><span data-stu-id="4551c-131">The $expand option goes in the query string of the request:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

<span data-ttu-id="4551c-132">Artık sunucu ürünleri, satır içi kategorileri ile olmak üzere her kategori için içerir.</span><span class="sxs-lookup"><span data-stu-id="4551c-132">Now the server will include the products for each category, inline with the categories.</span></span> <span data-ttu-id="4551c-133">Yanıt yükünde şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="4551c-133">Here is the response payload:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

<span data-ttu-id="4551c-134">"Value" dizisindeki her giriş için bir ürün listesini içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4551c-134">Notice that each entry in the "value" array contains a Products list.</span></span>

<span data-ttu-id="4551c-135">$ Seçeneği alır bir virgülle ayrılmış listesi genişletilecek Gezinti özelliklerini genişletin.</span><span class="sxs-lookup"><span data-stu-id="4551c-135">The $expand option takes a comma-separated list of navigation properties to expand.</span></span> <span data-ttu-id="4551c-136">Aşağıdaki isteği kategorisi hem bir ürünün sağlayıcısına genişletir.</span><span class="sxs-lookup"><span data-stu-id="4551c-136">The following request expands both the category and the supplier for a product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

<span data-ttu-id="4551c-137">Yanıt gövdesi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="4551c-137">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

<span data-ttu-id="4551c-138">Gezinme özelliğinin birden fazla düzeyde genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4551c-138">You can expand more than one level of navigation property.</span></span> <span data-ttu-id="4551c-139">Aşağıdaki örnek, bir kategorideki tüm ürünleri ve her ürün için tedarikçi içerir.</span><span class="sxs-lookup"><span data-stu-id="4551c-139">The following example includes all the products for a category and also the supplier for each product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

<span data-ttu-id="4551c-140">Yanıt gövdesi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="4551c-140">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

<span data-ttu-id="4551c-141">Varsayılan olarak, Web API 2 en büyük genişletme derinliği sınırlar.</span><span class="sxs-lookup"><span data-stu-id="4551c-141">By default, Web API limits the maximum expansion depth to 2.</span></span> <span data-ttu-id="4551c-142">Engelleyen istemci gibi karmaşık istekler göndermesini `$expand=Orders/OrderDetails/Product/Supplier/Region`, sorgu ve büyük yanıtları oluşturmak için yetersiz gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="4551c-142">That prevents the client from sending complex requests like `$expand=Orders/OrderDetails/Product/Supplier/Region`, which might be inefficient to query and create large responses.</span></span> <span data-ttu-id="4551c-143">Varsayılan geçersiz kılmak için ayarlanmış **MaxExpansionDepth** özelliği **[Queryable]** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="4551c-143">To override the default, set the **MaxExpansionDepth** property on the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

<span data-ttu-id="4551c-144">Seçeneğini genişletin $ hakkında daha fazla bilgi için bkz: [sistem sorgusu ($expand) seçeneği genişletin](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) resmi OData belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="4551c-144">For more information about the $expand option, see [Expand System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) in the official OData documentation.</span></span>

## <a name="using-select"></a><span data-ttu-id="4551c-145">$Select kullanma</span><span class="sxs-lookup"><span data-stu-id="4551c-145">Using $select</span></span>

<span data-ttu-id="4551c-146">$Select seçeneği, yanıt gövdesinde dahil edilecek özellik kümesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4551c-146">The $select option specifies a subset of properties to include in the response body.</span></span> <span data-ttu-id="4551c-147">Örneğin, yalnızca adı ve her ürünün fiyatı almak için aşağıdaki sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4551c-147">For example, to get only the name and price of each product, use the following query:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

<span data-ttu-id="4551c-148">Yanıt gövdesi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="4551c-148">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

<span data-ttu-id="4551c-149">$Select birleştirebilir ve $, aynı sorgu içinde genişletin.</span><span class="sxs-lookup"><span data-stu-id="4551c-149">You can combine $select and $expand in the same query.</span></span> <span data-ttu-id="4551c-150">$Select seçeneğinde genişletilmiş özelliği eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4551c-150">Make sure to include the expanded property in the $select option.</span></span> <span data-ttu-id="4551c-151">Örneğin, aşağıdaki isteği, üretici ve ürün adını alır.</span><span class="sxs-lookup"><span data-stu-id="4551c-151">For example, the following request gets the product name and supplier.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

<span data-ttu-id="4551c-152">Yanıt gövdesi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="4551c-152">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

<span data-ttu-id="4551c-153">Genişletilmiş bir özellik içinde özelliklerini de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4551c-153">You can also select the properties within an expanded property.</span></span> <span data-ttu-id="4551c-154">Aşağıdaki isteği ürünleri genişletir ve kategori adı artı ürün adını seçer.</span><span class="sxs-lookup"><span data-stu-id="4551c-154">The following request expands Products and selects category name plus product name.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

<span data-ttu-id="4551c-155">Yanıt gövdesi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="4551c-155">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

<span data-ttu-id="4551c-156">$Select seçeneği hakkında daha fazla bilgi için bkz. [sistem sorgusu seçeneği seçin ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) resmi OData belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="4551c-156">For more information about the $select option, see [Select System Query Option ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) in the official OData documentation.</span></span>

## <a name="getting-individual-properties-of-an-entity-value"></a><span data-ttu-id="4551c-157">Tek bir varlık ($value) özelliklerini alma</span><span class="sxs-lookup"><span data-stu-id="4551c-157">Getting Individual Properties of an Entity ($value)</span></span>

<span data-ttu-id="4551c-158">Bir varlıktan tek bir özellik almak bir OData istemcisi için iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="4551c-158">There are two ways for an OData client to get an individual property from an entity.</span></span> <span data-ttu-id="4551c-159">İstemci değeri OData biçiminde alın veya özelliğin ham değeri alır.</span><span class="sxs-lookup"><span data-stu-id="4551c-159">The client can either get the value in OData format, or get the raw value of the property.</span></span>

<span data-ttu-id="4551c-160">Aşağıdaki isteği OData biçiminde bir özelliğini alır.</span><span class="sxs-lookup"><span data-stu-id="4551c-160">The following request gets a property in OData format.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

<span data-ttu-id="4551c-161">JSON biçiminde bir yanıt örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="4551c-161">Here is an example response in JSON format:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

<span data-ttu-id="4551c-162">Ham özelliğin değerini almak için $value URİ'ye ekler:</span><span class="sxs-lookup"><span data-stu-id="4551c-162">To get the raw value of the property, append $value to the URI:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

<span data-ttu-id="4551c-163">Yanıtı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4551c-163">Here is the response.</span></span> <span data-ttu-id="4551c-164">İçerik türü "text/plain" JSON olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4551c-164">Notice that the content type is "text/plain", not JSON.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

<span data-ttu-id="4551c-165">OData denetleyiciniz bu sorguları desteklemek için adında bir yöntem ekleyin `GetProperty`burada `Property` özelliğin adıdır.</span><span class="sxs-lookup"><span data-stu-id="4551c-165">To support these queries in your OData controller, add a method named `GetProperty`, where `Property` is the name of the property.</span></span> <span data-ttu-id="4551c-166">Örneğin, Name özelliği alınacak yöntemin adlı `GetName`.</span><span class="sxs-lookup"><span data-stu-id="4551c-166">For example, the method to get the Name property would be named `GetName`.</span></span> <span data-ttu-id="4551c-167">Yöntemi, bu özelliğin değeri döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4551c-167">The method should return the value of that property:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
