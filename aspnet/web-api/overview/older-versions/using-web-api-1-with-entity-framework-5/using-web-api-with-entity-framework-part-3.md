---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: '3\. kısım: yönetici denetleyicisi oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600038"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="ddb8c-102">3\. kısım: yönetici denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddb8c-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="ddb8c-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ddb8c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ddb8c-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="ddb8c-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="ddb8c-105">Yönetici denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="ddb8c-105">Add an Admin Controller</span></span>

<span data-ttu-id="ddb8c-106">Bu bölümde, ürünlerde CRUD (oluşturma, okuma, güncelleştirme ve silme) işlemlerini destekleyen bir Web API denetleyicisi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="ddb8c-107">Denetleyici, veritabanı katmanıyla iletişim kurmak için Entity Framework kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="ddb8c-108">Bu denetleyici yalnızca yöneticiler tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="ddb8c-109">Müşteriler, ürünlere başka bir denetleyici üzerinden erişir.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="ddb8c-110">Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="ddb8c-111">**Ekle** ve sonra **Denetleyici**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="ddb8c-112">**Denetleyici Ekle** iletişim kutusunda denetleyiciyi `AdminController`adlandırın.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="ddb8c-113">**Şablon**altında Entity Framework&quot;kullanarak okuma/yazma eylemleri Ile &quot;API denetleyicisi ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="ddb8c-114">**Model sınıfı**altında "Product (productstore. modeller)" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="ddb8c-115">**Veri bağlamı**altında "yeni veri bağlamı&gt;&lt;" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="ddb8c-116">**Model sınıfı** açılır liste herhangi bir model sınıfı göstermezse, projeyi derlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="ddb8c-117">Entity Framework yansıma kullanır, bu nedenle derlenen derlemeye ihtiyaç duyuyor.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>

<span data-ttu-id="ddb8c-118">"&lt;yeni veri bağlamı&gt;" seçildiğinde, **Yeni veri bağlamı** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="ddb8c-119">Veri bağlamını `ProductStore.Models.OrdersContext`olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="ddb8c-120">**Yeni veri bağlamı** iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="ddb8c-121">**Denetleyici Ekle** Iletişim kutusunda **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="ddb8c-122">Projeye eklenen:</span><span class="sxs-lookup"><span data-stu-id="ddb8c-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="ddb8c-123">**DbContext**'ten türetilen `OrdersContext` adlı bir sınıf.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="ddb8c-124">Bu sınıf, POCO modelleri ve veritabanı arasında Tutkallamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="ddb8c-125">`AdminController`adlı bir Web API denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="ddb8c-126">Bu denetleyici `Product` örneklerine CRUD işlemlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="ddb8c-127">Entity Framework iletişim kurmak için `OrdersContext` sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="ddb8c-128">Web. config dosyasında yeni bir veritabanı bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="ddb8c-129">OrdersContext.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="ddb8c-130">Oluşturucunun, veritabanı bağlantı dizesinin adını belirttiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="ddb8c-131">Bu ad, Web. config dosyasına eklenen bağlantı dizesine başvurur.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="ddb8c-132">Aşağıdaki özellikleri `OrdersContext` sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ddb8c-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="ddb8c-133">Bir **Dbset** , sorgulanabilen bir varlık kümesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="ddb8c-134">`OrdersContext` sınıfı için tüm liste aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ddb8c-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="ddb8c-135">`AdminController` sınıfı, temel CRUD işlevlerini uygulayan beş yöntemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="ddb8c-136">Her yöntem, istemcinin çağırabileceği bir URI 'ye karşılık gelir:</span><span class="sxs-lookup"><span data-stu-id="ddb8c-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="ddb8c-137">Controller yöntemi</span><span class="sxs-lookup"><span data-stu-id="ddb8c-137">Controller Method</span></span> | <span data-ttu-id="ddb8c-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ddb8c-138">Description</span></span> | <span data-ttu-id="ddb8c-139">{1&gt;URI&lt;1}</span><span class="sxs-lookup"><span data-stu-id="ddb8c-139">URI</span></span> | <span data-ttu-id="ddb8c-140">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="ddb8c-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ddb8c-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="ddb8c-141">GetProducts</span></span> | <span data-ttu-id="ddb8c-142">Tüm ürünleri alır.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-142">Gets all products.</span></span> | <span data-ttu-id="ddb8c-143">API/ürünler</span><span class="sxs-lookup"><span data-stu-id="ddb8c-143">api/products</span></span> | <span data-ttu-id="ddb8c-144">Al</span><span class="sxs-lookup"><span data-stu-id="ddb8c-144">GET</span></span> |
| <span data-ttu-id="ddb8c-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="ddb8c-145">GetProduct</span></span> | <span data-ttu-id="ddb8c-146">KIMLIĞE göre bir ürün bulur.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-146">Finds a product by ID.</span></span> | <span data-ttu-id="ddb8c-147">API/ürünler/*kimlik*</span><span class="sxs-lookup"><span data-stu-id="ddb8c-147">api/products/*id*</span></span> | <span data-ttu-id="ddb8c-148">Al</span><span class="sxs-lookup"><span data-stu-id="ddb8c-148">GET</span></span> |
| <span data-ttu-id="ddb8c-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="ddb8c-149">PutProduct</span></span> | <span data-ttu-id="ddb8c-150">Bir ürünü güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-150">Updates a product.</span></span> | <span data-ttu-id="ddb8c-151">API/ürünler/*kimlik*</span><span class="sxs-lookup"><span data-stu-id="ddb8c-151">api/products/*id*</span></span> | <span data-ttu-id="ddb8c-152">KONUR</span><span class="sxs-lookup"><span data-stu-id="ddb8c-152">PUT</span></span> |
| <span data-ttu-id="ddb8c-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="ddb8c-153">PostProduct</span></span> | <span data-ttu-id="ddb8c-154">Yeni bir ürün oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-154">Creates a new product.</span></span> | <span data-ttu-id="ddb8c-155">API/ürünler</span><span class="sxs-lookup"><span data-stu-id="ddb8c-155">api/products</span></span> | <span data-ttu-id="ddb8c-156">Yayınla</span><span class="sxs-lookup"><span data-stu-id="ddb8c-156">POST</span></span> |
| <span data-ttu-id="ddb8c-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="ddb8c-157">DeleteProduct</span></span> | <span data-ttu-id="ddb8c-158">Bir ürünü siler.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-158">Deletes a product.</span></span> | <span data-ttu-id="ddb8c-159">API/ürünler/*kimlik*</span><span class="sxs-lookup"><span data-stu-id="ddb8c-159">api/products/*id*</span></span> | <span data-ttu-id="ddb8c-160">DELETE</span><span class="sxs-lookup"><span data-stu-id="ddb8c-160">DELETE</span></span> |

<span data-ttu-id="ddb8c-161">Her yöntem, veritabanını sorgulamak için `OrdersContext` çağırır.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="ddb8c-162">Değişiklikleri veritabanında kalıcı hale getirmek için koleksiyonu değiştiren Yöntemler (PUT, POST ve DELETE) çağrısı `db.SaveChanges`.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="ddb8c-163">Denetleyiciler her HTTP isteği için oluşturulur ve sonra, bir yöntem döndürülmadan önce değişiklikleri kalıcı hale getirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="ddb8c-164">Veritabanı başlatıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="ddb8c-164">Add a Database Initializer</span></span>

<span data-ttu-id="ddb8c-165">Entity Framework, veritabanını başlangıçta doldurmanıza ve modeller değiştiğinde veritabanını otomatik olarak yeniden oluşturmaya olanak tanıyan iyi bir özelliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="ddb8c-166">Bu özellik geliştirme sırasında faydalıdır, çünkü modelleri değiştirseniz bile, her zaman test verilerinize sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="ddb8c-167">Çözüm Gezgini, modeller klasörüne sağ tıklayın ve `OrdersContextInitializer`adlı yeni bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="ddb8c-168">Aşağıdaki uygulamada yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="ddb8c-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="ddb8c-169">**Dropcreatedatabaseifmodelchanges** sınıfından devralarak, model sınıflarını her değiştirtiğimiz zaman veritabanını Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="ddb8c-170">Entity Framework veritabanını oluşturduğunda (veya yeniden oluşturduğunda) tabloları doldurmak için **çekirdek** yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="ddb8c-171">Örnek bir sipariş ve örnek bir sipariş eklemek için **çekirdek** yöntemi kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="ddb8c-172">Bu özellik test için idealdir, ancak bir model sınıfı değiştirirse verilerinizi kaybedeceğinizi, üretim ortamında **Dropcreatedatabaseifmodelchanges** sınıfını kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="ddb8c-173">Ardından, Global. asax dosyasını açın ve aşağıdaki kodu **uygulama\_başlangıç** yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ddb8c-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="ddb8c-174">Denetleyiciye Istek gönderme</span><span class="sxs-lookup"><span data-stu-id="ddb8c-174">Send a Request to the Controller</span></span>

<span data-ttu-id="ddb8c-175">Bu noktada hiçbir istemci kodu yazmadınız, ancak Web API 'sini bir Web tarayıcısı veya [Fiddler](http://www.fiddler2.com/fiddler2/)gıbı bir http hata ayıklama aracı kullanarak çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="ddb8c-176">Visual Studio 'da hata ayıklamayı başlatmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="ddb8c-177">Web tarayıcınız `http://localhost:*portnum*/`için açılır; burada *portnum* , bir bağlantı noktası numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="ddb8c-178">"`http://localhost:*portnum*/api/admin`öğesine HTTP isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="ddb8c-179">Entity Framework veritabanının oluşturulması ve sağlaması gerektiğinden, ilk isteğin tamamlanabilmesi yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddb8c-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="ddb8c-180">Yanıt aşağıdakine benzer bir şey olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ddb8c-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="ddb8c-181">[Önceki](using-web-api-with-entity-framework-part-2.md)
> [İleri](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="ddb8c-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
