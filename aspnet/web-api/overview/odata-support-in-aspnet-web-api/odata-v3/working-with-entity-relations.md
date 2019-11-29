---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: OData v3 'de Web API 2 ile varlık Ilişkilerini destekleme | Microsoft Docs
author: MikeWasson
description: 'Çoğu veri kümesi varlıklar arasındaki ilişkileri tanımlar: müşterilerin siparişleri vardır; Kitaplar yazar. ürünlerin tedarikçileri vardır. OData kullanarak, istemciler üzerinde gezinerişebilir...'
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600307"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="9edcf-104">OData v3 'de Web API 2 ile varlık Ilişkilerini destekleme</span><span class="sxs-lookup"><span data-stu-id="9edcf-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>

<span data-ttu-id="9edcf-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9edcf-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="9edcf-106">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="9edcf-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="9edcf-107">Çoğu veri kümesi varlıklar arasındaki ilişkileri tanımlar: müşterilerin siparişleri vardır; Kitaplar yazar. ürünlerin tedarikçileri vardır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="9edcf-108">OData kullanarak, istemciler varlık ilişkilerine gidebilir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="9edcf-109">Bir ürün verildiğinde, tedarikçiyi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9edcf-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="9edcf-110">Ayrıca ilişkiler oluşturabilir veya kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9edcf-110">You can also create or remove relationships.</span></span> <span data-ttu-id="9edcf-111">Örneğin, tedarikçiyi bir ürün için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9edcf-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="9edcf-112">Bu öğreticide, ASP.NET Web API 'sinde bu işlemleri nasıl destekleyeceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="9edcf-113">Öğretici, [Web API 2 Ile OData v3 uç noktası oluşturma](creating-an-odata-endpoint.md)öğreticisinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9edcf-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9edcf-114">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="9edcf-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="9edcf-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="9edcf-115">Web API 2</span></span>
> - <span data-ttu-id="9edcf-116">OData sürüm 3</span><span class="sxs-lookup"><span data-stu-id="9edcf-116">OData Version 3</span></span>
> - <span data-ttu-id="9edcf-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="9edcf-117">Entity Framework 6</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="9edcf-118">Tedarikçi varlığı ekleme</span><span class="sxs-lookup"><span data-stu-id="9edcf-118">Add a Supplier Entity</span></span>

<span data-ttu-id="9edcf-119">İlk olarak OData akışınıza yeni bir varlık türü eklememiz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="9edcf-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="9edcf-120">`Supplier` sınıfı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="9edcf-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="9edcf-121">Bu sınıf, varlık anahtarı için bir dize kullanır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="9edcf-122">Uygulamada, bir tamsayı anahtar kullanmaktan daha az ortak olabilir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="9edcf-123">Ancak, OData 'in diğer anahtar türlerini tamsayıların yanı sıra nasıl işleyeceğini de öğrenecektir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="9edcf-124">Sonra, `Product` sınıfına bir `Supplier` özelliği ekleyerek bir ilişki oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="9edcf-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="9edcf-125">`ProductServiceContext` sınıfına yeni bir **Dbset** ekleyin, böylece Entity Framework `Supplier` tablosunu veritabanına dahil eder.</span><span class="sxs-lookup"><span data-stu-id="9edcf-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="9edcf-126">WebApiConfig.cs ' de, EDM modeline bir "Suppliers" varlığı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9edcf-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="9edcf-127">Gezinti özellikleri</span><span class="sxs-lookup"><span data-stu-id="9edcf-127">Navigation Properties</span></span>

<span data-ttu-id="9edcf-128">Bir ürünün tedarikçilerini almak için istemci bir GET isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="9edcf-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="9edcf-129">Burada "Tedarikçi" `Product` türünde bir gezinti özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="9edcf-130">Bu durumda `Supplier` tek bir öğe anlamına gelir, ancak bir gezinti özelliği de bir koleksiyon (bire çok veya çoktan çoğa ilişki) döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="9edcf-131">Bu isteği desteklemek için, `ProductsController` sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9edcf-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="9edcf-132">*Anahtar* parametresi ürünün anahtarıdır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="9edcf-133">Yöntemi bu durumda bir `Supplier` örneği&#8212;olan ilgili varlığı döndürür.</span><span class="sxs-lookup"><span data-stu-id="9edcf-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="9edcf-134">Yöntem adı ve parametre adı her ikisi de önemlidir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="9edcf-135">Genel olarak, gezinti özelliği "X" olarak adlandırılmışsa, "GetX" adlı bir yöntem eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="9edcf-136">Yöntem, üst öğenin anahtarının veri türüyle eşleşen "*Key*" adlı bir parametre almalıdır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="9edcf-137">*Anahtar* parametresine **[Fromodatauri]** özniteliğini eklemek de önemlidir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="9edcf-138">Bu öznitelik, Web API 'sini istek URI 'sinden anahtar ayrıştırdığında OData sözdizimi kurallarını kullanmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="9edcf-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="9edcf-139">Bağlantı oluşturma ve silme</span><span class="sxs-lookup"><span data-stu-id="9edcf-139">Creating and Deleting Links</span></span>

<span data-ttu-id="9edcf-140">OData iki varlık arasında ilişki oluşturmayı veya kaldırmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9edcf-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="9edcf-141">OData terminolojisinde ilişki bir "bağlantıdır".</span><span class="sxs-lookup"><span data-stu-id="9edcf-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="9edcf-142">Her bağlantının *varlık*/$Links/*varlık*biçiminde bir URI 'si vardır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="9edcf-143">Örneğin, üründen tedarikçiye bağlantı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="9edcf-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="9edcf-144">Yeni bir bağlantı oluşturmak için, istemci bağlantı URI 'sine bir POST isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="9edcf-145">İsteğin gövdesi, hedef varlığın URI 'sidir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="9edcf-146">Örneğin, "CTSO" anahtarına sahip bir tedarikçi olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="9edcf-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="9edcf-147">"Product (1)" öğesinden "tedarikçisine (' CTSO ')" bir bağlantı oluşturmak için, istemci aşağıdakine benzer bir istek gönderir:</span><span class="sxs-lookup"><span data-stu-id="9edcf-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="9edcf-148">Bir bağlantıyı silmek için, istemci bağlantı URI 'sine bir DELETE isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="9edcf-149">**Bağlantı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="9edcf-149">**Creating Links**</span></span>

<span data-ttu-id="9edcf-150">Bir istemcinin ürün-tedarikçi bağlantıları oluşturmasını sağlamak için, `ProductsController` sınıfına aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9edcf-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="9edcf-151">Bu yöntem üç parametre alır:</span><span class="sxs-lookup"><span data-stu-id="9edcf-151">This method takes three parameters:</span></span>

- <span data-ttu-id="9edcf-152">*anahtar*: ana varlığa yönelik anahtar (ürün)</span><span class="sxs-lookup"><span data-stu-id="9edcf-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="9edcf-153">*NavigationProperty*: Gezinti özelliğinin adı.</span><span class="sxs-lookup"><span data-stu-id="9edcf-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="9edcf-154">Bu örnekte, geçerli olan tek gezinti özelliği "Tedarikçi" dir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="9edcf-155">*bağlantı*: Ilgili varlığın OData URI 'si.</span><span class="sxs-lookup"><span data-stu-id="9edcf-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="9edcf-156">Bu değer, istek gövdesinden alınır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-156">This value is taken from the request body.</span></span> <span data-ttu-id="9edcf-157">Örneğin, bağlantı URI 'SI "`http://localhost/odata/Suppliers('CTSO')`, yani, ID = ' CTSO ' olan tedarikçide olabilir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="9edcf-158">Yöntemi, tedarikçiyi aramak için bağlantıyı kullanır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="9edcf-159">Eşleşen Tedarikçi bulunursa, yöntemi `Product.Supplier` özelliğini ayarlar ve sonucu veritabanına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9edcf-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="9edcf-160">En zor bölümü, bağlantı URI 'sini ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="9edcf-161">Temel olarak, bu URI 'ye bir GET isteği gönderme sonucunun benzetimini yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="9edcf-162">Aşağıdaki yardımcı yöntemi bunun nasıl yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="9edcf-163">Yöntemi, Web API yönlendirme işlemini çağırır ve ayrıştırılmış OData yolunu temsil eden bir **ODataPath** örneğini geri alır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="9edcf-164">Bir bağlantı URI 'SI için segmentlerin biri varlık anahtarı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="9edcf-165">(Değilse, istemci hatalı bir URI gönderdi.)</span><span class="sxs-lookup"><span data-stu-id="9edcf-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="9edcf-166">**Bağlantılar siliniyor**</span><span class="sxs-lookup"><span data-stu-id="9edcf-166">**Deleting Links**</span></span>

<span data-ttu-id="9edcf-167">Bir bağlantıyı silmek için `ProductsController` sınıfına aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9edcf-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="9edcf-168">Bu örnekte, gezinti özelliği tek bir `Supplier` varlıktır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="9edcf-169">Gezinti özelliği bir koleksiyon ise, bir bağlantıyı silmenin URI 'SI ilgili varlık için bir anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="9edcf-170">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9edcf-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="9edcf-171">Bu istek, müşteri 1 ' den sipariş 1 ' i kaldırır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="9edcf-172">Bu durumda, DeleteLink yöntemi aşağıdaki imzaya sahip olacaktır:</span><span class="sxs-lookup"><span data-stu-id="9edcf-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="9edcf-173">*RelatedKey* parametresi ilgili varlık için anahtarı verir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="9edcf-174">Bu nedenle `DeleteLink` yönteminde, *anahtar* parametresine göre birincil varlığı bulun, *RelatedKey* parametresiyle ilgili varlığı bulun ve ardından ilişkilendirmeyi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9edcf-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="9edcf-175">Veri modelinize bağlı olarak her iki `DeleteLink`sürümünü de uygulamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="9edcf-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="9edcf-176">Web API 'SI, istek URI 'sine bağlı olarak doğru sürümü çağırır.</span><span class="sxs-lookup"><span data-stu-id="9edcf-176">Web API will call the correct version based on the request URI.</span></span>
