---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: OData v4 'de ASP.NET Web API 2,2 kullanılarak varlık Ilişkileri | Microsoft Docs
author: MikeWasson
description: 'Çoğu veri kümesi varlıklar arasındaki ilişkileri tanımlar: müşterilerin siparişleri vardır; Kitaplar yazar. ürünlerin tedarikçileri vardır. OData kullanarak, istemciler üzerinde gezinerişebilir...'
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598695"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="abf91-104">ASP.NET Web API 2,2 kullanarak OData v4 'de varlık Ilişkileri</span><span class="sxs-lookup"><span data-stu-id="abf91-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="abf91-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="abf91-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="abf91-106">Çoğu veri kümesi varlıklar arasındaki ilişkileri tanımlar: müşterilerin siparişleri vardır; Kitaplar yazar. ürünlerin tedarikçileri vardır.</span><span class="sxs-lookup"><span data-stu-id="abf91-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="abf91-107">OData kullanarak, istemciler varlık ilişkilerine gidebilir.</span><span class="sxs-lookup"><span data-stu-id="abf91-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="abf91-108">Bir ürün verildiğinde, tedarikçiyi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abf91-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="abf91-109">Ayrıca ilişkiler oluşturabilir veya kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abf91-109">You can also create or remove relationships.</span></span> <span data-ttu-id="abf91-110">Örneğin, tedarikçiyi bir ürün için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abf91-110">For example, you can set the supplier for a product.</span></span>
>
> <span data-ttu-id="abf91-111">Bu öğreticide, ASP.NET Web API kullanılarak OData v4 'de bu işlemlerin nasıl destekleyeceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="abf91-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="abf91-112">Öğretici, [ASP.NET Web API 2 kullanarak bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md)öğreticisinde derleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="abf91-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="abf91-113">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="abf91-113">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="abf91-114">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="abf91-114">Web API 2.1</span></span>
> - <span data-ttu-id="abf91-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="abf91-115">OData v4</span></span>
> - <span data-ttu-id="abf91-116">Visual Studio 2013 (Visual Studio 2017 'yi [buraya](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)indirin)</span><span class="sxs-lookup"><span data-stu-id="abf91-116">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="abf91-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="abf91-117">Entity Framework 6</span></span>
> - <span data-ttu-id="abf91-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="abf91-118">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="abf91-119">Öğretici sürümleri</span><span class="sxs-lookup"><span data-stu-id="abf91-119">Tutorial versions</span></span>
>
> <span data-ttu-id="abf91-120">OData sürüm 3 için bkz. [OData v3 'de varlık Ilişkilerini destekleme](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span><span class="sxs-lookup"><span data-stu-id="abf91-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="abf91-121">Tedarikçi varlığı ekleme</span><span class="sxs-lookup"><span data-stu-id="abf91-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="abf91-122">Öğretici, [ASP.NET Web API 2 kullanarak bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md)öğreticisinde derleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="abf91-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="abf91-123">İlk olarak, ilgili bir varlığına ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="abf91-123">First, we need a related entity.</span></span> <span data-ttu-id="abf91-124">Modeller klasörüne `Supplier` adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="abf91-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="abf91-125">`Product` sınıfına bir gezinti özelliği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="abf91-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="abf91-126">`ProductsContext` sınıfına yeni bir **Dbset** ekleyin, böylece Entity Framework tedarikçinin tablosunu veritabanına dahil eder.</span><span class="sxs-lookup"><span data-stu-id="abf91-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="abf91-127">WebApiConfig.cs ' de, varlık veri modeline ayarlanmış bir &quot;Suppliers&quot; varlık ekleyin:</span><span class="sxs-lookup"><span data-stu-id="abf91-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="abf91-128">Bir tedarikçiler denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="abf91-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="abf91-129">Controllers klasörüne bir `SuppliersController` sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="abf91-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="abf91-130">Bu denetleyiciye CRUD işlemlerinin nasıl ekleneceğini göstermiyorum.</span><span class="sxs-lookup"><span data-stu-id="abf91-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="abf91-131">Adımlar, ürünler denetleyicisi ile aynıdır (bkz. [OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md)).</span><span class="sxs-lookup"><span data-stu-id="abf91-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="abf91-132">Ilgili varlıkları alma</span><span class="sxs-lookup"><span data-stu-id="abf91-132">Getting Related Entities</span></span>

<span data-ttu-id="abf91-133">Bir ürünün tedarikçilerini almak için istemci bir GET isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="abf91-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="abf91-134">Bu isteği desteklemek için, `ProductsController` sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="abf91-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="abf91-135">Bu yöntem varsayılan adlandırma kuralını kullanır</span><span class="sxs-lookup"><span data-stu-id="abf91-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="abf91-136">Yöntem adı: GetX, burada X, gezinti özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="abf91-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="abf91-137">Parametre adı: *anahtar*</span><span class="sxs-lookup"><span data-stu-id="abf91-137">Parameter name: *key*</span></span>

<span data-ttu-id="abf91-138">Bu adlandırma kuralını izlerseniz, Web API 'SI, HTTP isteğini denetleyici yöntemiyle otomatik olarak eşler.</span><span class="sxs-lookup"><span data-stu-id="abf91-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="abf91-139">Örnek HTTP isteği:</span><span class="sxs-lookup"><span data-stu-id="abf91-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="abf91-140">Örnek HTTP yanıtı:</span><span class="sxs-lookup"><span data-stu-id="abf91-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="abf91-141">İlişkili bir koleksiyon alınıyor</span><span class="sxs-lookup"><span data-stu-id="abf91-141">Getting a related collection</span></span>

<span data-ttu-id="abf91-142">Önceki örnekte, bir ürünün bir tedarikçisi vardır.</span><span class="sxs-lookup"><span data-stu-id="abf91-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="abf91-143">Bir gezinti özelliği de bir koleksiyonu döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="abf91-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="abf91-144">Aşağıdaki kod, bir tedarikçinin ürünlerini alır:</span><span class="sxs-lookup"><span data-stu-id="abf91-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="abf91-145">Bu durumda, yöntemi **SingleResult&lt;t** yerine bir **ıqueryable** döndürür&gt;</span><span class="sxs-lookup"><span data-stu-id="abf91-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="abf91-146">Örnek HTTP isteği:</span><span class="sxs-lookup"><span data-stu-id="abf91-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="abf91-147">Örnek HTTP yanıtı:</span><span class="sxs-lookup"><span data-stu-id="abf91-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="abf91-148">Varlıklar arasında Ilişki oluşturma</span><span class="sxs-lookup"><span data-stu-id="abf91-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="abf91-149">OData, mevcut iki varlık arasında ilişki oluşturmayı veya kaldırmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="abf91-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="abf91-150">OData v4 terminolojisinde, ilişki&quot;bir &quot;başvurudur.</span><span class="sxs-lookup"><span data-stu-id="abf91-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="abf91-151">(OData v3 'de ilişkiye bir *bağlantı*adı verilir.</span><span class="sxs-lookup"><span data-stu-id="abf91-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="abf91-152">Protokol farkları Bu öğreticiye göre farklılık görmez.)</span><span class="sxs-lookup"><span data-stu-id="abf91-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="abf91-153">Bir başvurunun, `/Entity/NavigationProperty/$ref`form ile kendi URI 'SI vardır.</span><span class="sxs-lookup"><span data-stu-id="abf91-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="abf91-154">Örneğin, bir ürün ve tedarikçiyle ilgili başvurunun ele aldığı URI aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="abf91-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="abf91-155">İstemci bir ilişki eklemek için bu adrese bir POST veya PUT isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="abf91-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="abf91-156">Gezinti özelliği `Product.Supplier`gibi tek bir varlık ise koyun.</span><span class="sxs-lookup"><span data-stu-id="abf91-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="abf91-157">Gezinti özelliği `Supplier.Products`gibi bir koleksiyon ise, gönder.</span><span class="sxs-lookup"><span data-stu-id="abf91-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="abf91-158">İsteğin gövdesi, ilişkide diğer varlığın URI 'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="abf91-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="abf91-159">Örnek bir istek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="abf91-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="abf91-160">Bu örnekte, istemci, KIMLIK = 6 olan ürün `Supplier` için $ref URI 'si olan `/Products(6)/Supplier/$ref`için bir PUT isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="abf91-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="abf91-161">İstek başarılı olursa, sunucu bir 204 (Içerik yok) yanıtı gönderir:</span><span class="sxs-lookup"><span data-stu-id="abf91-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="abf91-162">`Product`bir ilişki eklemek için denetleyici yöntemi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="abf91-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="abf91-163">*NavigationProperty* parametresi ayarlanacak ilişkiyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="abf91-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="abf91-164">(Varlıkta birden fazla gezinti özelliği varsa, daha fazla `case` deyimi ekleyebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="abf91-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="abf91-165">*Bağlantı* parametresi, tedarikçinin URI 'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="abf91-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="abf91-166">Web API 'SI, bu parametrenin değerini almak için istek gövdesini otomatik olarak ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="abf91-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="abf91-167">Tedarikçiyi aramak için, *bağlantı* parametresinin bir PARÇASı olan kimliğe (veya anahtara) ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="abf91-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="abf91-168">Bunu yapmak için aşağıdaki yardımcı yöntemi kullanın:</span><span class="sxs-lookup"><span data-stu-id="abf91-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="abf91-169">Temelde, bu yöntem, URI yolunu kesimlere bölmek için OData kitaplığını kullanır, anahtarı içeren segmenti bulur ve anahtarı doğru türe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="abf91-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="abf91-170">Varlıklar arasındaki Ilişkiyi silme</span><span class="sxs-lookup"><span data-stu-id="abf91-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="abf91-171">İstemci bir ilişkiyi silmek için $ref URI 'sine bir HTTP DELETE isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="abf91-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="abf91-172">Bir ürün ve tedarikçi arasındaki ilişkiyi silmek için denetleyici yöntemi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="abf91-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="abf91-173">Bu durumda `Product.Supplier`, 1 ' den fazla ilişkinin &quot;1&quot; sonuna kadar olan, `null``Product.Supplier` ayarlayarak ilişkiyi kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abf91-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="abf91-174">Bir ilişkinin &quot;çok&quot; sonunda, istemci hangi ilgili varlığın kaldırılacağını belirtmelidir.</span><span class="sxs-lookup"><span data-stu-id="abf91-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="abf91-175">Bunu yapmak için istemci, isteğin sorgu dizesinde ilgili varlığın URI 'sini gönderir.</span><span class="sxs-lookup"><span data-stu-id="abf91-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="abf91-176">Örneğin, "Product 1" öğesini "Tedarikçi 1" öğesinden kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="abf91-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="abf91-177">Web API 'de bunu desteklemek için `DeleteRef` metoduna fazladan bir parametre dahil etmemiz gerekir.</span><span class="sxs-lookup"><span data-stu-id="abf91-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="abf91-178">Bir ürünü `Supplier.Products` ilişkisinden kaldırmak için denetleyici yöntemi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="abf91-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="abf91-179">*Anahtar* parametresi, tedarikçinin anahtarıdır ve *relatedkey* parametresi, `Products` ilişkisinden kaldırılacak ürünün anahtarıdır.</span><span class="sxs-lookup"><span data-stu-id="abf91-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="abf91-180">Web API 'sinin anahtarı otomatik olarak sorgu dizesinden aldığından emin olmanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="abf91-180">Note that Web API automatically gets the key from the query string.</span></span>
