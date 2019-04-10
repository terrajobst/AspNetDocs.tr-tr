---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: Web API 2 OData v3 varlık ilişkilerini destekleme | Microsoft Docs
author: MikeWasson
description: 'Çoğu veri kümeleri, varlıkları arasındaki ilişkileri tanımlayın: Siparişler imajlarını; Books Yazar; yine de olan istiyor musunuz? Ürünler tedarikçileri sahip. OData kullanarak istemcileri üzerinden gidebilirsiniz...'
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: c78787aac83720eb9e8d6e9e0499f30a31951bc2
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393866"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="31b0a-104">Web API 2 OData v3 varlık ilişkilerini destekleme</span><span class="sxs-lookup"><span data-stu-id="31b0a-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>

<span data-ttu-id="31b0a-105">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="31b0a-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="31b0a-106">Projeyi yükle</span><span class="sxs-lookup"><span data-stu-id="31b0a-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="31b0a-107">Çoğu veri kümeleri, varlıkları arasındaki ilişkileri tanımlayın: Siparişler imajlarını; Books Yazar; yine de olan istiyor musunuz? Ürünler tedarikçileri sahip.</span><span class="sxs-lookup"><span data-stu-id="31b0a-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="31b0a-108">İstemciler, OData kullanarak, varlık ilişkileri gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b0a-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="31b0a-109">Bir ürün göz önünde bulundurulduğunda, tedarikçi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b0a-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="31b0a-110">Ayrıca, oluşturmak veya ilişkileri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="31b0a-110">You can also create or remove relationships.</span></span> <span data-ttu-id="31b0a-111">Örneğin, bir ürünün sağlayıcısına ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b0a-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="31b0a-112">Bu öğreticide, ASP.NET Web API işlemlerini desteklemek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="31b0a-113">Öğretici öğreticiyi genişletip yapılar [ile Web API 2 OData v3 uç noktası oluşturma](creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="31b0a-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="31b0a-114">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="31b0a-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="31b0a-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="31b0a-115">Web API 2</span></span>
> - <span data-ttu-id="31b0a-116">OData sürüm 3</span><span class="sxs-lookup"><span data-stu-id="31b0a-116">OData Version 3</span></span>
> - <span data-ttu-id="31b0a-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="31b0a-117">Entity Framework 6</span></span>


## <a name="add-a-supplier-entity"></a><span data-ttu-id="31b0a-118">Tedarikçi varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="31b0a-118">Add a Supplier Entity</span></span>

<span data-ttu-id="31b0a-119">İlk olarak biz bizim OData akışına yeni bir varlık türü eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="31b0a-120">Ekleyeceğiz bir `Supplier` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="31b0a-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="31b0a-121">Bu sınıf, bir dize için varlık anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="31b0a-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="31b0a-122">Uygulamada, bir tamsayı anahtarı kullanmaktan daha az yaygın olabilir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="31b0a-123">Ancak OData tamsayılar yanı sıra diğer anahtar türleri nasıl işlediğini görmeye değerindedir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="31b0a-124">Ardından, bir ilişki ekleyerek oluşturacağız bir `Supplier` özelliğini `Product` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="31b0a-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="31b0a-125">Yeni bir **olan DB** için `ProductServiceContext` sınıfının Entity Framework içermesi `Supplier` veritabanındaki tablo.</span><span class="sxs-lookup"><span data-stu-id="31b0a-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="31b0a-126">WebApiConfig.cs içinde "Tedarikçileri" varlığı için EDM modeline ekleyin:</span><span class="sxs-lookup"><span data-stu-id="31b0a-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="31b0a-127">Gezinti özellikleri</span><span class="sxs-lookup"><span data-stu-id="31b0a-127">Navigation Properties</span></span>

<span data-ttu-id="31b0a-128">Sağlayıcı için bir ürün almak için istemci bir GET isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="31b0a-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="31b0a-129">Burada "Sağlayıcı" bir gezinti özelliği açıktır `Product` türü.</span><span class="sxs-lookup"><span data-stu-id="31b0a-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="31b0a-130">Bu durumda, `Supplier` başvuran tek bir öğe, ancak bir gezinti özelliği ayrıca bir koleksiyon (bire çok veya çoka çok ilişkisi) döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="31b0a-131">Bu istek desteklemek için aşağıdaki yöntemi ekleyin. `ProductsController` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="31b0a-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="31b0a-132">*Anahtar* parametresi, ürün anahtarı.</span><span class="sxs-lookup"><span data-stu-id="31b0a-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="31b0a-133">İlgili varlık yöntemi döndürür&#8212;bu durumda, bir `Supplier` örneği.</span><span class="sxs-lookup"><span data-stu-id="31b0a-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="31b0a-134">Parametre adı ve yöntem adı önemli olduğunda.</span><span class="sxs-lookup"><span data-stu-id="31b0a-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="31b0a-135">Genel olarak, gezinme özelliğini "X" ise, "GetX" adlı bir yöntemi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="31b0a-136">Yöntem adlı bir parametre almalıdır "*anahtar*" üst öğenin anahtar veri türü ile eşleşen.</span><span class="sxs-lookup"><span data-stu-id="31b0a-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="31b0a-137">Eklenmesi önemlidir **[FromOdataUri]** özniteliğini *anahtar* parametresi.</span><span class="sxs-lookup"><span data-stu-id="31b0a-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="31b0a-138">Bu öznitelik, istek URI'si anahtarından ayrıştırırken OData sözdizimi kurallarını kullanmak için Web API'si söyler.</span><span class="sxs-lookup"><span data-stu-id="31b0a-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="31b0a-139">Oluşturma ve bağlantıları silme</span><span class="sxs-lookup"><span data-stu-id="31b0a-139">Creating and Deleting Links</span></span>

<span data-ttu-id="31b0a-140">OData iki varlıklar arasında ilişki oluşturma veya kaldırmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="31b0a-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="31b0a-141">OData terminolojisinde, ilişki bir "." bağlantıdır</span><span class="sxs-lookup"><span data-stu-id="31b0a-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="31b0a-142">Her bağlantı form bir URI'ya sahip *varlık*/$links /*varlık*.</span><span class="sxs-lookup"><span data-stu-id="31b0a-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="31b0a-143">Örneğin, ürün bağlantıdan tedarikçiye şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="31b0a-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="31b0a-144">Yeni bir bağlantı oluşturmak için istemci bağlantı URI'si için bir POST isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="31b0a-145">Hedef varlığın URI'si istek gövdesidir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="31b0a-146">Örneğin, "CTSO" anahtarına sahip bir sağlayıcı yok varsayalım.</span><span class="sxs-lookup"><span data-stu-id="31b0a-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="31b0a-147">"Product(1)" "Supplier('CTSO')" için bir bağlantı oluşturmak için istemci aşağıdaki gibi bir istek gönderir:</span><span class="sxs-lookup"><span data-stu-id="31b0a-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="31b0a-148">Bir bağlantıyı silmek için istemci bağlantı URI'si için bir silme isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

**<span data-ttu-id="31b0a-149">Bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="31b0a-149">Creating Links</span></span>**

<span data-ttu-id="31b0a-150">Ürün tedarikçi bağlantılar oluşturmak bir istemci etkinleştirmek için aşağıdaki kodu ekleyin. `ProductsController` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="31b0a-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="31b0a-151">Bu yöntem, üç parametreleri alır:</span><span class="sxs-lookup"><span data-stu-id="31b0a-151">This method takes three parameters:</span></span>

- <span data-ttu-id="31b0a-152">*Anahtar*: Üst Varlık (ürün) anahtarı</span><span class="sxs-lookup"><span data-stu-id="31b0a-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="31b0a-153">*navigationProperty*: Gezinme özelliğinin adı.</span><span class="sxs-lookup"><span data-stu-id="31b0a-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="31b0a-154">Bu örnekte, yalnızca geçerli gezinme özelliğini "Sağlayıcı" dir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="31b0a-155">*Bağlantı*: OData URI'SİNİN ilgili varlık.</span><span class="sxs-lookup"><span data-stu-id="31b0a-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="31b0a-156">Bu değer, istek gövdesinden alınır.</span><span class="sxs-lookup"><span data-stu-id="31b0a-156">This value is taken from the request body.</span></span> <span data-ttu-id="31b0a-157">Örneğin, bağlantı URI'si olabilir "`http://localhost/odata/Suppliers('CTSO')`, kimliği bir tedarikçi anlamı = 'CTSO'.</span><span class="sxs-lookup"><span data-stu-id="31b0a-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="31b0a-158">Yöntemi, tedarikçi aramak için bağlantıya kullanır.</span><span class="sxs-lookup"><span data-stu-id="31b0a-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="31b0a-159">Eşleşen tedarikçi bulunursa, yöntem ayarlar `Product.Supplier` özelliği ve sonuçları veritabanına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="31b0a-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="31b0a-160">Uygulamalarınızdaki Bölümü ' % s'bağlantı URI'si ayrıştırılıyor.</span><span class="sxs-lookup"><span data-stu-id="31b0a-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="31b0a-161">Temel olarak, bu URI'ye bir GET isteği gönderme sonucunu benzetimini yapmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="31b0a-162">Aşağıdaki yardımcı yöntemini bunun nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="31b0a-163">Bu yöntem, Web API'si yönlendirme işlemi çağırır ve geri alır bir **ODataPath** ayrıştırılmış OData yolunu temsil ettiği örneği.</span><span class="sxs-lookup"><span data-stu-id="31b0a-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="31b0a-164">Bağlantı için URI, parçaların bir varlık anahtarı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="31b0a-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="31b0a-165">(Aksi halde, hatalı bir URI istemciye gönderilen.)</span><span class="sxs-lookup"><span data-stu-id="31b0a-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

**<span data-ttu-id="31b0a-166">Bağlantıları silme</span><span class="sxs-lookup"><span data-stu-id="31b0a-166">Deleting Links</span></span>**

<span data-ttu-id="31b0a-167">Bağlantıyı silmek için aşağıdaki kodu ekleyin. `ProductsController` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="31b0a-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="31b0a-168">Bu örnekte, tek bir gezinti özelliği olan `Supplier` varlık.</span><span class="sxs-lookup"><span data-stu-id="31b0a-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="31b0a-169">Bir koleksiyon gezinme özelliği ise bir bağlantıyı silmek için URI ilgili varlık için bir anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="31b0a-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="31b0a-170">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="31b0a-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="31b0a-171">Bu istek sırası 1 müşteri 1 ' kaldırır.</span><span class="sxs-lookup"><span data-stu-id="31b0a-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="31b0a-172">Bu durumda, DeleteLink yöntemi aşağıdaki imzası olacaktır:</span><span class="sxs-lookup"><span data-stu-id="31b0a-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="31b0a-173">*RelatedKey* parametresi ilgili varlık için anahtar sağlar.</span><span class="sxs-lookup"><span data-stu-id="31b0a-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="31b0a-174">Dolayısıyla, `DeleteLink` yöntemi, birincil varlık tarafından Ara *anahtarı* parametresi, ilgili varlık tarafından bulma *relatedKey* parametresini kaldırın ve sonra ilişkilendirme.</span><span class="sxs-lookup"><span data-stu-id="31b0a-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="31b0a-175">Veri modelinizi bağlı olarak iki sürümü de uygulamanız gerekebilir `DeleteLink`.</span><span class="sxs-lookup"><span data-stu-id="31b0a-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="31b0a-176">Web API'si istek URI'SİNDEKİ göre doğru sürümü çağırır.</span><span class="sxs-lookup"><span data-stu-id="31b0a-176">Web API will call the correct version based on the request URI.</span></span>
