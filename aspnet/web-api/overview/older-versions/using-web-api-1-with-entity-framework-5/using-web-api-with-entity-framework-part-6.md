---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: '6\. Bölüm: ürün ve sipariş denetleyicileri oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600024"
---
# <a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="60e25-102">6\. Bölüm: ürün ve sipariş denetleyicileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="60e25-102">Part 6: Creating Product and Order Controllers</span></span>

<span data-ttu-id="60e25-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="60e25-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="60e25-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="60e25-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="60e25-105">Ürün denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="60e25-105">Add a Products Controller</span></span>

<span data-ttu-id="60e25-106">Yönetici denetleyicisi, yönetici ayrıcalıklarına sahip kullanıcılar içindir.</span><span class="sxs-lookup"><span data-stu-id="60e25-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="60e25-107">Diğer yandan müşteriler ürünleri görüntüleyebilir, ancak oluşturamaz, güncelleştiremez veya silemez.</span><span class="sxs-lookup"><span data-stu-id="60e25-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="60e25-108">Post, put ve DELETE yöntemlerine erişimi kolayca kısıtlayabiliriz ve Get yöntemlerinin açık bırakılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="60e25-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="60e25-109">Ancak bir ürün için döndürülen verilere göz atın:</span><span class="sxs-lookup"><span data-stu-id="60e25-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="60e25-110">`ActualCost` özelliği müşterilere görünür olmamalıdır!</span><span class="sxs-lookup"><span data-stu-id="60e25-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="60e25-111">Çözüm, müşterilere görünür olması gereken özelliklerin bir alt kümesini içeren bir *veri aktarımı nesnesi* (DTO) tanımlamaktır.</span><span class="sxs-lookup"><span data-stu-id="60e25-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="60e25-112">Örnekleri `ProductDTO` için LINQ for Project `Product` örnekleri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="60e25-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="60e25-113">Modeller klasörüne `ProductDTO` adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="60e25-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="60e25-114">Şimdi denetleyiciyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="60e25-114">Now add the controller.</span></span> <span data-ttu-id="60e25-115">Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="60e25-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="60e25-116">**Ekle**' yi ve ardından **Denetleyici**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="60e25-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="60e25-117">**Denetleyici Ekle** iletişim kutusunda, denetleyiciyi &quot;productscontroller&quot;olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="60e25-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="60e25-118">**Şablon**altında **boş API denetleyicisi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="60e25-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="60e25-119">Kaynak dosyadaki her şeyi aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="60e25-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="60e25-120">Denetleyici hala veritabanını sorgulamak için `OrdersContext` kullanır.</span><span class="sxs-lookup"><span data-stu-id="60e25-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="60e25-121">Ancak `Product` örnekleri doğrudan döndürmek yerine, onları `ProductDTO` örneklerine eklemek için `MapProducts` çağırdık:</span><span class="sxs-lookup"><span data-stu-id="60e25-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="60e25-122">`MapProducts` yöntemi bir **IQueryable**döndürür, bu nedenle sonucu diğer sorgu parametreleriyle oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60e25-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="60e25-123">Bunu sorguya bir **WHERE** yan tümcesi ekleyen `GetProduct` yönteminde görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="60e25-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="60e25-124">Sipariş denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="60e25-124">Add an Orders Controller</span></span>

<span data-ttu-id="60e25-125">Daha sonra, kullanıcıların sipariş oluşturmalarına ve görüntülemesine imkan tanıyan bir denetleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="60e25-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="60e25-126">Başka bir DTO ile başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="60e25-126">We'll start with another DTO.</span></span> <span data-ttu-id="60e25-127">Çözüm Gezgini, modeller klasörüne sağ tıklayın ve `OrderDTO` adlı bir sınıf ekleyerek aşağıdaki uygulamayı kullanın:</span><span class="sxs-lookup"><span data-stu-id="60e25-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="60e25-128">Şimdi denetleyiciyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="60e25-128">Now add the controller.</span></span> <span data-ttu-id="60e25-129">Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="60e25-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="60e25-130">**Ekle**' yi ve ardından **Denetleyici**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="60e25-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="60e25-131">**Denetleyici Ekle** iletişim kutusunda aşağıdaki seçenekleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="60e25-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="60e25-132">**Denetleyici adı**bölümünde "orderscontroller" yazın.</span><span class="sxs-lookup"><span data-stu-id="60e25-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="60e25-133">**Şablon**altında, "Entity Framework kullanarak okuma/yazma EYLEMLERI ile API denetleyicisi ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="60e25-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="60e25-134">**Model sınıfı**altında &quot;Order (productstore. modeller)&quot;öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="60e25-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="60e25-135">**Veri bağlamı sınıfı**altında &quot;OrdersContext (productstore. modeller)&quot;öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="60e25-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="60e25-136">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="60e25-136">Click **Add**.</span></span> <span data-ttu-id="60e25-137">Bu, OrdersController.cs adlı bir dosya ekler.</span><span class="sxs-lookup"><span data-stu-id="60e25-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="60e25-138">Sonra, denetleyicinin varsayılan uygulamasını değiştirmemiz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="60e25-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="60e25-139">İlk olarak, `PutOrder` ve `DeleteOrder` yöntemlerini silin.</span><span class="sxs-lookup"><span data-stu-id="60e25-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="60e25-140">Bu örnekte, müşteriler mevcut siparişleri değiştiremez veya silemez.</span><span class="sxs-lookup"><span data-stu-id="60e25-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="60e25-141">Gerçek bir uygulamada, bu durumları işlemek için çok sayıda arka uç mantığına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="60e25-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="60e25-142">(Örneğin, sipariş zaten sevk edildi mı?)</span><span class="sxs-lookup"><span data-stu-id="60e25-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="60e25-143">`GetOrders` yöntemini yalnızca kullanıcıya ait olan siparişleri döndürecek şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="60e25-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="60e25-144">`GetOrder` yöntemini aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="60e25-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="60e25-145">Bu yöntemde yaptığımız değişiklikler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="60e25-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="60e25-146">Dönüş değeri, bir `Order`yerine bir `OrderDTO` örneğidir.</span><span class="sxs-lookup"><span data-stu-id="60e25-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="60e25-147">Sıraya yönelik veritabanını sorgulıyoruz, ilgili `OrderDetail` ve `Product` varlıklarını getirmek için [dbquery. Include](https://msdn.microsoft.com/library/gg696395) metodunu kullanırız.</span><span class="sxs-lookup"><span data-stu-id="60e25-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="60e25-148">Bir projeksiyon kullanarak sonucu düzettik.</span><span class="sxs-lookup"><span data-stu-id="60e25-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="60e25-149">HTTP yanıtı, miktarları olan bir ürün dizisi içerir:</span><span class="sxs-lookup"><span data-stu-id="60e25-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="60e25-150">Bu biçim, istemcilerin iç içe geçmiş varlıklar (sipariş, Ayrıntılar ve ürünler) içeren özgün nesne grafiğinden daha kolay kullanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="60e25-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="60e25-151">`PostOrder`göz önünde bulundurmanız gereken son yöntem.</span><span class="sxs-lookup"><span data-stu-id="60e25-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="60e25-152">Bu yöntem şu anda bir `Order` örneği alır.</span><span class="sxs-lookup"><span data-stu-id="60e25-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="60e25-153">Ancak, bir istemci şöyle bir istek gövdesi gönderirse ne olacağını düşünün:</span><span class="sxs-lookup"><span data-stu-id="60e25-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="60e25-154">Bu iyi yapılandırılmış bir sıradır ve Entity Framework, veritabanını veritabanına eklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="60e25-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="60e25-155">Ancak daha önce mevcut olmayan bir ürün varlığını içerir.</span><span class="sxs-lookup"><span data-stu-id="60e25-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="60e25-156">İstemci, veritabanımızda yeni bir ürün oluşturdu!</span><span class="sxs-lookup"><span data-stu-id="60e25-156">The client just created a new product in our database!</span></span> <span data-ttu-id="60e25-157">Bu, Koala yatak için bir sipariş görtiklerinde departmanı karşılama bölümünün bir şaşırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="60e25-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="60e25-158">Moral, bir POST veya PUT isteğinde kabul ettiğiniz veriler hakkında gerçekten dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="60e25-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="60e25-159">Bu sorundan kaçınmak için `PostOrder` yöntemini bir `OrderDTO` örneği alacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="60e25-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="60e25-160">`Order`oluşturmak için `OrderDTO` kullanın.</span><span class="sxs-lookup"><span data-stu-id="60e25-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="60e25-161">`ProductID` ve `Quantity` özelliklerini kullandığımızda, istemcinin ürün adı veya fiyat için gönderdiği tüm değerleri yok saydığımızda dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="60e25-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="60e25-162">Ürün KIMLIĞI geçerli değilse, veritabanındaki yabancı anahtar kısıtlamasını ihlal eder ve gerektiğinde ekleme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="60e25-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="60e25-163">İşte `PostOrder` yöntemi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="60e25-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="60e25-164">Son olarak, denetleyiciye **Yetkilendir** özniteliğini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="60e25-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="60e25-165">Artık yalnızca kayıtlı kullanıcılar sipariş oluşturabilir veya görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="60e25-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="60e25-166">[Önceki](using-web-api-with-entity-framework-part-5.md)
> [İleri](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="60e25-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
