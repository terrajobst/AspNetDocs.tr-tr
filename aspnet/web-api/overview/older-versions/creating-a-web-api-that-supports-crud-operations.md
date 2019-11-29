---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: ASP.NET Web API 1-ASP.NET 4. x içinde CRUD Işlemlerini etkinleştirme
author: MikeWasson
description: Öğreticide, ASP.NET 4. x için ASP.NET Web API 'sini kullanarak bir HTTP hizmetindeki CRUD işlemlerini destekleme işlemi gösterilmektedir.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600333"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="bd1d8-103">ASP.NET Web API 1 ' de CRUD Işlemlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bd1d8-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="bd1d8-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bd1d8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="bd1d8-105">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="bd1d8-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="bd1d8-106">Bu öğreticide, ASP.NET 4. x için ASP.NET Web API 'sini kullanarak bir HTTP hizmetindeki CRUD işlemlerini destekleme işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bd1d8-107">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="bd1d8-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="bd1d8-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="bd1d8-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="bd1d8-109">Web API 1 (Ayrıca Web API 2 ile birlikte çalışarak)</span><span class="sxs-lookup"><span data-stu-id="bd1d8-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="bd1d8-110">CRUD, dört temel veritabanı işlemi olan &quot;oluşturma, okuma, güncelleştirme ve&quot; silme işlemlerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="bd1d8-111">Birçok HTTP hizmeti Ayrıca REST veya REST API 'Ler aracılığıyla CRUD işlemlerini modelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="bd1d8-112">Bu öğreticide, ürünlerin listesini yönetmek için çok basit bir Web API 'SI oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="bd1d8-113">Her ürün bir ad, Fiyat ve kategori (&quot;Toys&quot; veya &quot;donanım&quot;), ayrıca bir ürün KIMLIĞI içerir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="bd1d8-114">Ürünler API 'SI aşağıdaki yöntemleri ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="bd1d8-115">Eylem</span><span class="sxs-lookup"><span data-stu-id="bd1d8-115">Action</span></span> | <span data-ttu-id="bd1d8-116">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="bd1d8-116">HTTP method</span></span> | <span data-ttu-id="bd1d8-117">Göreli URI</span><span class="sxs-lookup"><span data-stu-id="bd1d8-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd1d8-118">Tüm ürünlerin bir listesini alın</span><span class="sxs-lookup"><span data-stu-id="bd1d8-118">Get a list of all products</span></span> | <span data-ttu-id="bd1d8-119">Al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-119">GET</span></span> | <span data-ttu-id="bd1d8-120">/api/Products</span><span class="sxs-lookup"><span data-stu-id="bd1d8-120">/api/products</span></span> |
| <span data-ttu-id="bd1d8-121">KIMLIĞE göre ürün al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-121">Get a product by ID</span></span> | <span data-ttu-id="bd1d8-122">Al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-122">GET</span></span> | <span data-ttu-id="bd1d8-123">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="bd1d8-123">/api/products/*id*</span></span> |
| <span data-ttu-id="bd1d8-124">Kategoriye göre bir ürün al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-124">Get a product by category</span></span> | <span data-ttu-id="bd1d8-125">Al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-125">GET</span></span> | <span data-ttu-id="bd1d8-126">/api/Products? kategori =*Kategori*</span><span class="sxs-lookup"><span data-stu-id="bd1d8-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="bd1d8-127">Yeni ürün oluştur</span><span class="sxs-lookup"><span data-stu-id="bd1d8-127">Create a new product</span></span> | <span data-ttu-id="bd1d8-128">Yayınla</span><span class="sxs-lookup"><span data-stu-id="bd1d8-128">POST</span></span> | <span data-ttu-id="bd1d8-129">/api/Products</span><span class="sxs-lookup"><span data-stu-id="bd1d8-129">/api/products</span></span> |
| <span data-ttu-id="bd1d8-130">Bir ürünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bd1d8-130">Update a product</span></span> | <span data-ttu-id="bd1d8-131">KONUR</span><span class="sxs-lookup"><span data-stu-id="bd1d8-131">PUT</span></span> | <span data-ttu-id="bd1d8-132">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="bd1d8-132">/api/products/*id*</span></span> |
| <span data-ttu-id="bd1d8-133">Bir ürünü silme</span><span class="sxs-lookup"><span data-stu-id="bd1d8-133">Delete a product</span></span> | <span data-ttu-id="bd1d8-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="bd1d8-134">DELETE</span></span> | <span data-ttu-id="bd1d8-135">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="bd1d8-135">/api/products/*id*</span></span> |

<span data-ttu-id="bd1d8-136">URI 'lerden bazılarının, yoldaki ürün KIMLIĞINI içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="bd1d8-137">Örneğin, KIMLIĞI 28 olan ürünü almak için, istemci `http://hostname/api/products/28`için bir GET isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="bd1d8-138">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bd1d8-138">Resources</span></span>

<span data-ttu-id="bd1d8-139">Products API 'SI iki kaynak türü için URI tanımlar:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="bd1d8-140">Kaynak</span><span class="sxs-lookup"><span data-stu-id="bd1d8-140">Resource</span></span> | <span data-ttu-id="bd1d8-141">{1&gt;URI&lt;1}</span><span class="sxs-lookup"><span data-stu-id="bd1d8-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="bd1d8-142">Tüm ürünlerin listesi.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-142">The list of all the products.</span></span> | <span data-ttu-id="bd1d8-143">/api/Products</span><span class="sxs-lookup"><span data-stu-id="bd1d8-143">/api/products</span></span> |
| <span data-ttu-id="bd1d8-144">Tek bir ürün.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-144">An individual product.</span></span> | <span data-ttu-id="bd1d8-145">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="bd1d8-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="bd1d8-146">Yöntemler</span><span class="sxs-lookup"><span data-stu-id="bd1d8-146">Methods</span></span>

<span data-ttu-id="bd1d8-147">Dört ana HTTP yöntemi (GET, PUT, POST ve DELETE) şu şekilde CRUD işlemlerine eşlenebilir:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="bd1d8-148">GET, kaynağın belirtilen URI 'de temsilini alır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="bd1d8-149">GET 'in sunucu üzerinde hiçbir yan etkisi olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="bd1d8-150">Güncelleştirme bir kaynağı belirtilen bir URI 'ye YERLEŞTIRIN.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="bd1d8-151">Ayrıca, sunucu istemcilerin yeni URI 'Ler belirlemesine izin veriyorsa belirtilen bir URI 'de yeni bir kaynak oluşturmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="bd1d8-152">Bu öğretici için, API PUT aracılığıyla oluşturmayı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="bd1d8-153">GÖNDERI yeni bir kaynak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-153">POST creates a new resource.</span></span> <span data-ttu-id="bd1d8-154">Sunucu, yeni nesnenin URI 'sini atar ve bu URI 'yi yanıt iletisinin bir parçası olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="bd1d8-155">DELETE, belirtilen URI 'de bir kaynağı siler.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="bd1d8-156">Note: PUT yöntemi tüm ürün varlığının yerini alır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="bd1d8-157">Diğer bir deyişle, istemcinin güncelleştirilmiş ürünün tüm gösterimini gönderebilmesi beklenir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="bd1d8-158">Kısmi güncelleştirmeleri desteklemek istiyorsanız, düzeltme eki yöntemi tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="bd1d8-159">Bu öğretici, düzeltme eki uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="bd1d8-160">Yeni bir Web API projesi oluştur</span><span class="sxs-lookup"><span data-stu-id="bd1d8-160">Create a New Web API Project</span></span>

<span data-ttu-id="bd1d8-161">Visual Studio 'Yu çalıştırarak başlatın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="bd1d8-162">Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="bd1d8-163">**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="bd1d8-164">**Görsel C#** bölümünde **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="bd1d8-165">Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="bd1d8-166">Projeyi &quot;ProductStore&quot; olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="bd1d8-167">**Yeni ASP.NET MVC 4 proje** Iletişim kutusunda **Web API 'si** ' ni seçin ve **Tamam**' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="bd1d8-168">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="bd1d8-168">Adding a Model</span></span>

<span data-ttu-id="bd1d8-169">*Model* , uygulamanızdaki verileri temsil eden bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="bd1d8-170">ASP.NET Web API 'sinde, kesin türü belirtilmiş CLR nesnelerini modeller olarak kullanabilirsiniz ve istemci için otomatik olarak XML veya JSON olarak serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="bd1d8-171">ProductStore API 'SI için verilerimiz ürünlerden oluşur. bu nedenle `Product`adlı yeni bir sınıf oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="bd1d8-172">Çözüm Gezgini zaten görünmüyorsa, **Görünüm** menüsüne tıklayın ve **Çözüm Gezgini**öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="bd1d8-173">Çözüm Gezgini **modeller** klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="bd1d8-174">Bağlam menüsünden **Ekle**' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="bd1d8-175">Sınıfı ürün&quot;&quot;adlandırın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="bd1d8-176">Aşağıdaki özellikleri `Product` sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="bd1d8-177">Depo ekleme</span><span class="sxs-lookup"><span data-stu-id="bd1d8-177">Adding a Repository</span></span>

<span data-ttu-id="bd1d8-178">Ürünlerin bir koleksiyonunu depoladık.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-178">We need to store a collection of products.</span></span> <span data-ttu-id="bd1d8-179">Koleksiyonu hizmet uygulamamızda ayırmak iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="bd1d8-180">Bu şekilde, hizmet sınıfını yeniden yazmadan yedekleme deposunu değiştirebiliriz.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="bd1d8-181">Bu tür tasarıma *Depo* deseninin adı verilir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="bd1d8-182">Depo için genel bir arabirim tanımlayarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="bd1d8-183">Çözüm Gezgini **modeller** klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="bd1d8-184">**Ekle**' yi ve ardından **Yeni öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="bd1d8-185">**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve C# düğümü genişletin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="bd1d8-186">Altında C# **kod**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-186">Under C#, select **Code**.</span></span> <span data-ttu-id="bd1d8-187">Kod şablonları listesinde **arabirim**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="bd1d8-188">&quot;ıproductrepository&quot;arabirimini adlandırın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="bd1d8-189">Aşağıdaki uygulamayı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="bd1d8-190">Şimdi, &quot;ProductRepository adlı modeller klasörüne başka bir sınıf ekleyin. Bu sınıf&quot;, `IProductRepository` arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="bd1d8-191">Aşağıdaki uygulamayı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="bd1d8-192">Depo, listeyi yerel bellekte tutar.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="bd1d8-193">Bu bir öğretici için Tamam, ancak gerçek bir uygulamada, verileri harici olarak veya bulut depolama alanında depoladığınızda.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="bd1d8-194">Depo deseninin daha sonra uygulanması daha kolay hale gelir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="bd1d8-195">Web API denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="bd1d8-195">Adding a Web API Controller</span></span>

<span data-ttu-id="bd1d8-196">ASP.NET MVC ile çalıştıysanız, denetleyicilerle zaten bilgi sahibisiniz.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="bd1d8-197">ASP.NET Web API 'sinde, *Denetleyici* ISTEMCIDEN gelen http isteklerini işleyen bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="bd1d8-198">Yeni proje Sihirbazı, projeyi oluştururken sizin için iki denetleyici oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="bd1d8-199">Bunları görmek için Çözüm Gezgini içindeki Denetleyiciler klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="bd1d8-200">HomeController geleneksel bir ASP.NET MVC denetleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="bd1d8-201">Site için HTML sayfalarının sunulmasından sorumludur ve doğrudan Web API 'imizle ilgili değildir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="bd1d8-202">ValuesController örnek bir WebAPI Controller.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="bd1d8-203">Çözüm Gezgini ' de dosyaya sağ tıklayıp Sil ' i seçerek ValuesController 'ı silin **.**</span><span class="sxs-lookup"><span data-stu-id="bd1d8-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="bd1d8-204">Şimdi yeni bir denetleyiciyi şu şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="bd1d8-205">**Çözüm Gezgini**, denetleyiciler klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="bd1d8-206">**Ekle** ' yi ve ardından **Denetleyici**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="bd1d8-207">**Denetleyici ekleme** Sihirbazı ' nda, denetleyiciyi &quot;productscontroller&quot;olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="bd1d8-208">**Şablon** açılan LISTESINDE **boş API denetleyicisi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="bd1d8-209">Ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="bd1d8-210">Denetleyicilerinizi denetleyiciler adlı bir klasöre koymak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="bd1d8-211">Klasör adı önemli değildir; kaynak dosyalarınızı düzenlemek için kullanışlı bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="bd1d8-212">**Denetleyici ekleme** Sihirbazı, denetleyiciler klasöründe ProductsController.cs adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="bd1d8-213">Bu dosya henüz açık değilse, açmak için dosyaya çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="bd1d8-214">Aşağıdaki **using** ifadesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="bd1d8-215">**Iproductrepository** örneğini tutan bir alan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="bd1d8-216">Denetleyiciyi, denetleyicinin belirli bir `IProductRepository`uygulamasına bağladığından, denetleyicinin `new ProductRepository()` çağrılması en iyi tasarım değildir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="bd1d8-217">Daha iyi bir yaklaşım için bkz. [Web API bağımlılığı çözümleyici 'Yi kullanma](../advanced/dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="bd1d8-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="bd1d8-218">Kaynak alma</span><span class="sxs-lookup"><span data-stu-id="bd1d8-218">Getting a Resource</span></span>

<span data-ttu-id="bd1d8-219">ProductStore API 'SI, birkaç &quot;okuma&quot; eylemini HTTP GET yöntemleri olarak kullanıma sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="bd1d8-220">Her eylem, `ProductsController` sınıfındaki bir yönteme karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="bd1d8-221">Eylem</span><span class="sxs-lookup"><span data-stu-id="bd1d8-221">Action</span></span> | <span data-ttu-id="bd1d8-222">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="bd1d8-222">HTTP method</span></span> | <span data-ttu-id="bd1d8-223">Göreli URI</span><span class="sxs-lookup"><span data-stu-id="bd1d8-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd1d8-224">Tüm ürünlerin bir listesini alın</span><span class="sxs-lookup"><span data-stu-id="bd1d8-224">Get a list of all products</span></span> | <span data-ttu-id="bd1d8-225">Al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-225">GET</span></span> | <span data-ttu-id="bd1d8-226">/api/Products</span><span class="sxs-lookup"><span data-stu-id="bd1d8-226">/api/products</span></span> |
| <span data-ttu-id="bd1d8-227">KIMLIĞE göre ürün al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-227">Get a product by ID</span></span> | <span data-ttu-id="bd1d8-228">Al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-228">GET</span></span> | <span data-ttu-id="bd1d8-229">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="bd1d8-229">/api/products/*id*</span></span> |
| <span data-ttu-id="bd1d8-230">Kategoriye göre bir ürün al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-230">Get a product by category</span></span> | <span data-ttu-id="bd1d8-231">Al</span><span class="sxs-lookup"><span data-stu-id="bd1d8-231">GET</span></span> | <span data-ttu-id="bd1d8-232">/api/Products? kategori =*Kategori*</span><span class="sxs-lookup"><span data-stu-id="bd1d8-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="bd1d8-233">Tüm ürünlerin listesini almak için, bu yöntemi `ProductsController` sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="bd1d8-234">Yöntem adı &quot;Get&quot;ile başlar, bu sayede istekleri almak üzere eşlenir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="bd1d8-235">Ayrıca, yönteminin parametresi olmadığından, yol içinde *&quot;kimliği&quot;* segment IÇERMEYEN bir URI ile eşlenir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="bd1d8-236">KIMLIĞE göre bir ürün almak için, bu yöntemi `ProductsController` sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="bd1d8-237">Bu yöntem adı ayrıca &quot;al&quot;başlar, ancak yönteminde *ID*adlı bir parametre bulunur. Bu parametre, URI yolunun &quot;ID&quot; kesimine eşlenir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="bd1d8-238">ASP.NET Web API çerçevesi, KIMLIĞI parametresinin doğru veri türüne (**int**) otomatik olarak dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="bd1d8-239">GetProduct metodu, *kimlik* geçerli değilse **httpresponseexception** türünde bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="bd1d8-240">Bu özel durum Framework tarafından 404 (bulunamadı) hatası olarak çevrilecek.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="bd1d8-241">Son olarak, kategoriye göre ürün bulmak için bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="bd1d8-242">İstek URI 'sinin bir sorgu dizesi varsa, Web API 'SI, denetleyici yöntemindeki parametrelerle sorgu parametrelerini eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="bd1d8-243">Bu nedenle, "API/Products? Category =*category*" BIÇIMINDEKI bir URI bu yöntemle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="bd1d8-244">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd1d8-244">Creating a Resource</span></span>

<span data-ttu-id="bd1d8-245">Sonra, yeni bir ürün oluşturmak için `ProductsController` sınıfına bir yöntem ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="bd1d8-246">Yöntemin basit bir uygulamasıdır:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="bd1d8-247">Bu yöntemle ilgili iki şeyi göz önünde bulundurmanız gerekenler:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-247">Note two things about this method:</span></span>

- <span data-ttu-id="bd1d8-248">Yöntem adı &quot;Post...&quot;ile başlar.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="bd1d8-249">Yeni bir ürün oluşturmak için istemci bir HTTP POST isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="bd1d8-250">Yöntemi ürün türünde bir parametre alır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="bd1d8-251">Web API 'sinde, karmaşık türlere sahip parametrelerin, istek gövdesinden serisi kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="bd1d8-252">Bu nedenle, istemcinin, XML veya JSON biçiminde bir ürün nesnesinin seri hale getirilmiş gösterimini göndermesini bekledik.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="bd1d8-253">Bu uygulama çalışır, ancak tam olarak tamamlanmaz.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="bd1d8-254">İdeal olarak, HTTP yanıtının aşağıdakileri içermesini istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="bd1d8-255">**Yanıt kodu:** Varsayılan olarak, Web API çerçevesi yanıt durum kodunu 200 (Tamam) olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="bd1d8-256">Ancak, HTTP/1.1 protokolüne göre, bir POST isteği bir kaynak oluşturulmasına neden olduğunda, sunucu 201 (oluşturuldu) durumuyla yanıt vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="bd1d8-257">**Konum:** Sunucu bir kaynak oluşturduğunda, yanıtın konum üst bilgisinde yeni kaynağın URI 'sini içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="bd1d8-258">ASP.NET Web API 'SI, HTTP yanıt iletisini işlemeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="bd1d8-259">Geliştirilmiş uygulama aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="bd1d8-260">Yöntemin dönüş türünün artık **HttpResponseMessage**olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="bd1d8-261">Bir ürün yerine bir **HttpResponseMessage** döndürerek, durum kodu ve konum üstbilgisi dahil olmak üzere http yanıt iletisinin ayrıntılarını denetleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="bd1d8-262">**Createres,** yöntemi bir **HttpResponseMessage** oluşturur ve Product nesnesinin serileştirilmiş bir gösterimini yanıt iletisi olan gövdeye otomatik olarak yazar.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="bd1d8-263">Bu örnek `Product`doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="bd1d8-264">Model doğrulama hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de model doğrulaması](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="bd1d8-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="bd1d8-265">Kaynak güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="bd1d8-265">Updating a Resource</span></span>

<span data-ttu-id="bd1d8-266">Bir ürünü PUT ile güncelleştirmek basittir:</span><span class="sxs-lookup"><span data-stu-id="bd1d8-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="bd1d8-267">Yöntem adı &quot;put...&quot;ile başlar, bu nedenle Web API 'SI istekleri koymak için onunla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="bd1d8-268">Yöntemi iki parametre alır, ürün KIMLIĞI ve güncelleştirilmiş ürün.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="bd1d8-269">*ID* parametresi URI yolundan alınır ve *ürün* parametresi, istek gövdesinden seri durumdan çıkarılacak.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="bd1d8-270">Varsayılan olarak, ASP.NET Web API çerçevesi, istek gövdesinden yol ve karmaşık türlerden basit parametre türlerini alır.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="bd1d8-271">Kaynak silme</span><span class="sxs-lookup"><span data-stu-id="bd1d8-271">Deleting a Resource</span></span>

<span data-ttu-id="bd1d8-272">Bir kaynağı silmek için bir "Sil..." tanımlayın yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="bd1d8-273">SILME isteği başarılı olursa, durumu açıklayan bir varlık gövdesiyle 200 (Tamam) durumunu döndürebilir; durum 202 (kabul edildi) silme hala bekliyor; veya varlık gövdesi olmayan bir durum 204 (Içerik yok).</span><span class="sxs-lookup"><span data-stu-id="bd1d8-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="bd1d8-274">Bu durumda `DeleteProduct` yöntemi `void` bir dönüş türüne sahiptir, bu nedenle ASP.NET Web API bunu otomatik olarak 204 (Içerik yok) durum koduna dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="bd1d8-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
