---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: ASP.NET Web API 2 ' de OData eylemlerini destekleme | Microsoft Docs
author: MikeWasson
description: "OData 'de, Eylemler, varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur. Eylemler için bazı kullanımlar şunlardır: Uygula..."
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556359"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="1691e-104">ASP.NET Web API 2 ' de OData eylemlerini destekleme</span><span class="sxs-lookup"><span data-stu-id="1691e-104">Supporting OData Actions in ASP.NET Web API 2</span></span>

<span data-ttu-id="1691e-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1691e-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="1691e-106">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="1691e-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="1691e-107">OData 'de, *Eylemler* , varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="1691e-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="1691e-108">Bazı eylemler için kullanımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1691e-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="1691e-109">Karmaşık işlemleri uygulama.</span><span class="sxs-lookup"><span data-stu-id="1691e-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="1691e-110">Aynı anda birkaç varlığı düzenleme.</span><span class="sxs-lookup"><span data-stu-id="1691e-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="1691e-111">Yalnızca bir varlığın belirli özelliklerine yönelik güncelleştirmelere izin verme.</span><span class="sxs-lookup"><span data-stu-id="1691e-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="1691e-112">Bir varlıkta tanımlanmayan sunucuya bilgi gönderme.</span><span class="sxs-lookup"><span data-stu-id="1691e-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1691e-113">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="1691e-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1691e-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="1691e-114">Web API 2</span></span>
> - <span data-ttu-id="1691e-115">OData sürüm 3</span><span class="sxs-lookup"><span data-stu-id="1691e-115">OData Version 3</span></span>
> - <span data-ttu-id="1691e-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="1691e-116">Entity Framework 6</span></span>

## <a name="example-rating-a-product"></a><span data-ttu-id="1691e-117">Örnek: bir ürünü derecelendirme</span><span class="sxs-lookup"><span data-stu-id="1691e-117">Example: Rating a Product</span></span>

<span data-ttu-id="1691e-118">Bu örnekte, kullanıcıların ürünlerin hızına izin vermek ve ardından her ürün için Ortalama derecelendirmeleri göstermek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1691e-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="1691e-119">Veritabanında, ürünlere girilen derecelendirmelerin bir listesini depolayacağız.</span><span class="sxs-lookup"><span data-stu-id="1691e-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="1691e-120">Entity Framework derecelendirmeleri temsil etmek için kullandığımız model aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1691e-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="1691e-121">Ancak istemcilerin bir `ProductRating` nesnesini bir "derecelendirmeler" koleksiyonuna NAKLETMESINI istemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1691e-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="1691e-122">Intuicanlı, derecelendirme, ürünler koleksiyonuyla ilişkilendirilir ve istemcinin yalnızca derecelendirme değerini göndermesinin gerekli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1691e-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="1691e-123">Bu nedenle, normal CRUD işlemlerini kullanmak yerine, bir istemcinin bir üründe çağırabileceği bir eylem tanımladık.</span><span class="sxs-lookup"><span data-stu-id="1691e-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="1691e-124">OData terminolojisinde, eylem ürün varlıklarına *bağlanır* .</span><span class="sxs-lookup"><span data-stu-id="1691e-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="1691e-125">Eylemlerin sunucuda yan etkileri vardır.</span><span class="sxs-lookup"><span data-stu-id="1691e-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="1691e-126">Bu nedenle, bunlar HTTP POST istekleri kullanılarak çağırılır.</span><span class="sxs-lookup"><span data-stu-id="1691e-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="1691e-127">Eylemler, hizmet meta verilerinde açıklanan parametrelere ve dönüş türlerine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="1691e-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="1691e-128">İstemci, parametreleri istek gövdesinde gönderir ve sunucu döndürülen değeri yanıt gövdesinde gönderir.</span><span class="sxs-lookup"><span data-stu-id="1691e-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="1691e-129">"Ürünü derecelendirin" eylemini çağırmak için, istemci aşağıdaki gibi bir URI 'ye GÖNDERI gönderir:</span><span class="sxs-lookup"><span data-stu-id="1691e-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="1691e-130">POST isteğindeki veriler yalnızca ürün derecelendirmesidir:</span><span class="sxs-lookup"><span data-stu-id="1691e-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="1691e-131">Varlık Veri Modeli eylemi bildirme</span><span class="sxs-lookup"><span data-stu-id="1691e-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="1691e-132">Web API yapılandırmanızda, eylemi varlık veri modeli (EDM) öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1691e-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="1691e-133">Bu kod, ürün varlıklarında gerçekleştirilebilecek bir eylem olarak "RateProduct" tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1691e-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="1691e-134">Ayrıca, eylemin "derecelendirme" adlı bir **int** parametre aldığını bildirir ve bir **int** değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="1691e-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="1691e-135">Eylemi denetleyiciye ekleyin</span><span class="sxs-lookup"><span data-stu-id="1691e-135">Add the Action to the Controller</span></span>

<span data-ttu-id="1691e-136">"RateProduct" eylemi ürün varlıklarına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1691e-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="1691e-137">Eylemi uygulamak için, ürünler denetleyicisine `RateProduct` adlı bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1691e-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="1691e-138">Yöntem adının EDM içindeki eylem adıyla eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1691e-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="1691e-139">Yöntemi iki parametreye sahiptir:</span><span class="sxs-lookup"><span data-stu-id="1691e-139">The method has two parameters:</span></span>

- <span data-ttu-id="1691e-140">*anahtar*: ürünün derecelendirmek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="1691e-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="1691e-141">*Parametreler*: eylem parametresi değerlerinin bir sözlüğü.</span><span class="sxs-lookup"><span data-stu-id="1691e-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="1691e-142">Varsayılan yönlendirme kurallarını kullanıyorsanız, anahtar parametrenin "Key" olarak adlandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1691e-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="1691e-143">Ayrıca, gösterildiği gibi **[Fromodatauri]** özniteliğini eklemek de önemlidir.</span><span class="sxs-lookup"><span data-stu-id="1691e-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="1691e-144">Bu öznitelik, Web API 'sini istek URI 'sinden anahtar ayrıştırdığında OData sözdizimi kurallarını kullanmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="1691e-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="1691e-145">Eylem parametrelerini almak için *Parameters* sözlüğünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="1691e-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="1691e-146">İstemci eylem parametrelerini doğru biçimde gönderirse **ModelState. IsValid** değeri true 'dur.</span><span class="sxs-lookup"><span data-stu-id="1691e-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="1691e-147">Bu durumda, **ODataActionParameters** sözlüğünü parametre değerlerini almak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1691e-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="1691e-148">Bu örnekte, `RateProduct` eylemi "derecelendirme" adlı tek bir parametre alır.</span><span class="sxs-lookup"><span data-stu-id="1691e-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="1691e-149">Eylem meta verileri</span><span class="sxs-lookup"><span data-stu-id="1691e-149">Action Metadata</span></span>

<span data-ttu-id="1691e-150">Hizmet meta verilerini görüntülemek için/OData/$metadata adresine bir GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="1691e-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="1691e-151">`RateProduct` eylemi bildiren meta verilerin bölümü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1691e-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="1691e-152">**FunctionImport** öğesi eylemi bildirir.</span><span class="sxs-lookup"><span data-stu-id="1691e-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="1691e-153">Alanların çoğu kendi kendine açıklayıcıdır, ancak iki değer de şunları belirtmekte:</span><span class="sxs-lookup"><span data-stu-id="1691e-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="1691e-154">**Ibındable** , eylemin hedef varlıkta en az bir kez çağrılabileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1691e-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="1691e-155">**Ialwaysdable** , eylemin hedef varlıkta her zaman çağrılabileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1691e-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="1691e-156">Fark, bazı eylemlerin her zaman istemciler için kullanılabilir olduğu, ancak diğer eylemlerin da varlığın durumuna bağlı olabileceği durumdur.</span><span class="sxs-lookup"><span data-stu-id="1691e-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="1691e-157">Örneğin, bir "satın alma" eylemi tanımladığınızı varsayalım.</span><span class="sxs-lookup"><span data-stu-id="1691e-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="1691e-158">Yalnızca Stokta olan bir öğeyi satın alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1691e-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="1691e-159">Öğe stokta yoksa, istemci bu eylemi çağıramıyor.</span><span class="sxs-lookup"><span data-stu-id="1691e-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="1691e-160">EDM 'yi tanımlarken, **eylem** yöntemi her zaman bağlanabilir bir eylem oluşturur:</span><span class="sxs-lookup"><span data-stu-id="1691e-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="1691e-161">Bu konunun ilerleyen kısımlarında, her zaman bağlanabilir eylemler ( *geçici* eylemler olarak da adlandırılır) hakkında konuşacağız.</span><span class="sxs-lookup"><span data-stu-id="1691e-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="1691e-162">Eylem çağrılıyor</span><span class="sxs-lookup"><span data-stu-id="1691e-162">Invoking the Action</span></span>

<span data-ttu-id="1691e-163">Şimdi bir istemcinin bu eylemi nasıl çağıracağına bakalım.</span><span class="sxs-lookup"><span data-stu-id="1691e-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="1691e-164">İstemcinin KIMLIĞI = 4 olan ürüne 2 derecelendirmesine izin vermek istediğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="1691e-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="1691e-165">İstek gövdesi için JSON biçimini kullanan örnek bir istek iletisi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1691e-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="1691e-166">Yanıt iletisi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1691e-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="1691e-167">Bir eylemi varlık kümesine bağlama</span><span class="sxs-lookup"><span data-stu-id="1691e-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="1691e-168">Önceki örnekte, eylem tek bir varlığa bağlanır: istemci tek bir ürünü ücretler.</span><span class="sxs-lookup"><span data-stu-id="1691e-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="1691e-169">Ayrıca, bir eylemi bir varlık koleksiyonuna bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1691e-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="1691e-170">Yalnızca aşağıdaki değişiklikleri yapmanız yeterlidir:</span><span class="sxs-lookup"><span data-stu-id="1691e-170">Just make the following changes:</span></span>

<span data-ttu-id="1691e-171">EDM öğesinde, varlığın **koleksiyon** özelliğine eylemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1691e-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="1691e-172">Denetleyici yönteminde, *anahtar* parametresini atlayın.</span><span class="sxs-lookup"><span data-stu-id="1691e-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="1691e-173">Artık istemci, ürünler varlık kümesinde eylemi çağırır:</span><span class="sxs-lookup"><span data-stu-id="1691e-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="1691e-174">Koleksiyon parametrelerine sahip eylemler</span><span class="sxs-lookup"><span data-stu-id="1691e-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="1691e-175">Eylemler bir değer koleksiyonu alan parametrelere sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="1691e-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="1691e-176">EDM 'da, parametreyi bildirmek için **&lt;t&gt;CollectionParameter** ' ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1691e-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="1691e-177">Bu, **int** değerlerinin bir koleksiyonunu alan "derecelendirmeler" adlı bir parametre bildirir.</span><span class="sxs-lookup"><span data-stu-id="1691e-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="1691e-178">Denetleyici yönteminde, **ODataActionParameters** nesnesinden parametre değerini almaya devam edersiniz, ancak bundan sonra değer bir **ıcollection&lt;int&gt;** değeridir:</span><span class="sxs-lookup"><span data-stu-id="1691e-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="1691e-179">Geçici eylemler</span><span class="sxs-lookup"><span data-stu-id="1691e-179">Transient Actions</span></span>

<span data-ttu-id="1691e-180">"RateProduct" örneğinde, kullanıcılar her zaman bir ürüne ücret verebilir, böylece eylem her zaman kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1691e-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="1691e-181">Ancak bazı eylemler varlığın durumuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1691e-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="1691e-182">Örneğin, bir video kiralama hizmetinde, "kullanıma alma" eylemi her zaman kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="1691e-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="1691e-183">(Bu videonun bir kopyasının kullanılabilir olup olmadığına bağlıdır.) Bu tür bir eyleme *geçici* eylem denir.</span><span class="sxs-lookup"><span data-stu-id="1691e-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="1691e-184">Hizmet meta verilerinde geçici bir **eylem, yanlış değerine eşit bir** şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="1691e-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="1691e-185">Bu aslında varsayılan değerdir, bu nedenle meta veriler şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="1691e-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="1691e-186">Bu önemlidir: bir eylem geçicidir, sunucu, eylem kullanılabilir olduğunda istemciye bunu söylemelidir.</span><span class="sxs-lookup"><span data-stu-id="1691e-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="1691e-187">Bu, varlıktaki eyleme bir bağlantı ekleyerek bunu yapar.</span><span class="sxs-lookup"><span data-stu-id="1691e-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="1691e-188">Bir film varlığına yönelik bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1691e-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="1691e-189">"#CheckOut" özelliği, kullanıma alma eyleminin bağlantısını içerir.</span><span class="sxs-lookup"><span data-stu-id="1691e-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="1691e-190">Eylem kullanılamıyorsa sunucu bağlantıyı atlar.</span><span class="sxs-lookup"><span data-stu-id="1691e-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="1691e-191">EDM 'ta geçici bir eylem bildirmek için, **geçişli Entaction** metodunu çağırın:</span><span class="sxs-lookup"><span data-stu-id="1691e-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="1691e-192">Ayrıca, belirli bir varlık için bir eylem bağlantısı döndüren bir işlev sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1691e-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="1691e-193">**HasActionLink**çağırarak bu işlevi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1691e-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="1691e-194">İşlevi bir lambda ifadesi olarak yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1691e-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="1691e-195">Eylem kullanılabiliyorsa, lambda ifadesi eyleme bir bağlantı döndürür.</span><span class="sxs-lookup"><span data-stu-id="1691e-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="1691e-196">OData seri hale getirici, varlığı serileştirtiğinde bu bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="1691e-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="1691e-197">Eylem kullanılabilir olmadığında, işlev `null`döndürür.</span><span class="sxs-lookup"><span data-stu-id="1691e-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1691e-198">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1691e-198">Additional Resources</span></span>

[<span data-ttu-id="1691e-199">OData eylemleri örneği</span><span class="sxs-lookup"><span data-stu-id="1691e-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
