---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#) Ile çalışmaya başlama-ASP.NET 4. x
author: MikeWasson
description: Kod ile öğretici. Ürünlerin bir listesini döndüren bir Web API 'SI oluşturmak için ASP.NET Web API 'sini kullanın.
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556800"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="c2ac7-104">ASP.NET Web API 2 (C#) Ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c2ac7-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="c2ac7-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c2ac7-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c2ac7-106">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="c2ac7-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="c2ac7-107">Bu öğreticide, ürünlerin listesini döndüren bir Web API 'SI oluşturmak için ASP.NET Web API kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="c2ac7-108">HTTP yalnızca Web sayfalarına hizmet vermek için değildir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="c2ac7-109">HTTP Ayrıca hizmet ve verileri kullanıma sunan API 'Leri oluşturmaya yönelik güçlü bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="c2ac7-110">HTTP basit, esnek ve ubititous.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="c2ac7-111">Düşünebildiğiniz neredeyse her platformda bir HTTP kitaplığı vardır. bu nedenle, HTTP Hizmetleri tarayıcılar, mobil cihazlar ve geleneksel masaüstü uygulamaları gibi çok sayıda istemciye ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="c2ac7-112">ASP.NET Web API 'SI, .NET Framework en üstünde Web API 'Leri oluşturmaya yönelik bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c2ac7-113">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="c2ac7-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="c2ac7-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c2ac7-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="c2ac7-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="c2ac7-115">Web API 2</span></span>

<span data-ttu-id="c2ac7-116">Bu öğreticinin daha yeni bir sürümü için [ASP.NET Core ve Windows Için Visual Studio ile Web API 'Si oluşturma](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="c2ac7-117">Web API projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2ac7-117">Create a Web API Project</span></span>

<span data-ttu-id="c2ac7-118">Bu öğreticide, ürünlerin listesini döndüren bir Web API 'SI oluşturmak için ASP.NET Web API kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="c2ac7-119">Ön uç Web sayfası, sonuçları göstermek için jQuery kullanır.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="c2ac7-120">Visual Studio 'Yu başlatın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="c2ac7-121">Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="c2ac7-122">**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="c2ac7-123">**Görsel C#** bölümünde **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="c2ac7-124">Proje şablonları listesinde **ASP.NET Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="c2ac7-125">Projeyi "ProductsApp" olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="c2ac7-126">**Yeni ASP.NET projesi** Iletişim kutusunda **boş** şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="c2ac7-127">&quot;için klasör ve temel başvurular eklemek &quot;altında, **Web API 'sini**kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="c2ac7-128">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="c2ac7-129">Ayrıca, &quot;Web API&quot; şablonunu kullanarak bir Web API projesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="c2ac7-130">Web API şablonu, API yardım sayfalarını sağlamak için ASP.NET MVC kullanır.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="c2ac7-131">Bu öğretici için boş şablon kullanıyorum çünkü Web API 'sini MVC olmadan göstermek istiyorum.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="c2ac7-132">Genel olarak, Web API 'sini kullanmak için ASP.NET MVC 'yi bilmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="c2ac7-133">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="c2ac7-133">Adding a Model</span></span>

<span data-ttu-id="c2ac7-134">*Model* , uygulamanızdaki verileri temsil eden bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="c2ac7-135">ASP.NET Web API 'SI, modelinizi JSON, XML veya başka bir biçime otomatik olarak seri hale getirilebilir ve ardından seri hale getirilmiş verileri HTTP yanıt iletisinin gövdesine yazabilir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="c2ac7-136">Bir istemci serileştirme biçimini okuyabilirler, nesne seri durumdan çıkarabilirler.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="c2ac7-137">Çoğu istemci, XML veya JSON 'yi ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="c2ac7-138">Ayrıca, istemci, HTTP istek iletisinde Accept üst bilgisini ayarlayarak hangi biçimin istediğini belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="c2ac7-139">Bir ürünü temsil eden basit bir model oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="c2ac7-140">Çözüm Gezgini zaten görünmüyorsa, **Görünüm** menüsüne tıklayın ve **Çözüm Gezgini**öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="c2ac7-141">Çözüm Gezgini modeller klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="c2ac7-142">Bağlam menüsünden **Ekle** ' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="c2ac7-143">Sınıfı ürün&quot;&quot;adlandırın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="c2ac7-144">Aşağıdaki özellikleri `Product` sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="c2ac7-145">Denetleyici Ekleme</span><span class="sxs-lookup"><span data-stu-id="c2ac7-145">Adding a Controller</span></span>

<span data-ttu-id="c2ac7-146">Web API 'sinde, *DENETLEYICI* http isteklerini işleyen bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="c2ac7-147">Ürünlerin bir listesini ya da ID tarafından belirtilen tek bir ürünü döndüren bir denetleyici ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="c2ac7-148">ASP.NET MVC kullandıysanız, denetleyicilerle zaten bilgi sahibisiniz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="c2ac7-149">Web API denetleyicileri MVC denetleyicilerine benzerdir, ancak **Controller** sınıfı yerine **Apicontroller** sınıfını devralınır.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="c2ac7-150">**Çözüm Gezgini**, denetleyiciler klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="c2ac7-151">**Ekle** ' yi ve ardından **Denetleyici**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="c2ac7-152">**Yapı Iskelesi Ekle** Iletişim kutusunda **Web API denetleyicisi-boş**seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="c2ac7-153">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="c2ac7-154">**Denetleyici Ekle** iletişim kutusunda, denetleyiciyi &quot;productscontroller&quot;olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="c2ac7-155">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="c2ac7-156">Yapı iskelesi, denetleyiciler klasöründe ProductsController.cs adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="c2ac7-157">Denetleyicilerinizi denetleyiciler adlı bir klasöre koymanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="c2ac7-158">Klasör adı, kaynak dosyalarınızı düzenlemenin yalnızca uygun bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-158">The folder name is just a convenient way to organize your source files.</span></span>

<span data-ttu-id="c2ac7-159">Bu dosya henüz açık değilse, açmak için dosyaya çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="c2ac7-160">Bu dosyadaki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="c2ac7-161">Bu örneği basit tutmak için, ürünler Controller sınıfının içindeki sabit bir dizide depolanır.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="c2ac7-162">Kuşkusuz, gerçek bir uygulamada bir veritabanını sorgulayıp başka bir dış veri kaynağı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="c2ac7-163">Denetleyici, ürünleri döndüren iki yöntemi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="c2ac7-164">`GetAllProducts` yöntemi, tüm ürün listesini **ıenumerable&lt;ürün&gt;** türü olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="c2ac7-165">`GetProduct` yöntemi, KIMLIĞINE göre tek bir ürün arar.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="c2ac7-166">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="c2ac7-166">That's it!</span></span> <span data-ttu-id="c2ac7-167">Çalışan bir Web API 'SI var.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-167">You have a working web API.</span></span> <span data-ttu-id="c2ac7-168">Denetleyicideki her yöntem bir veya daha fazla URI 'ye karşılık gelir:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="c2ac7-169">Controller yöntemi</span><span class="sxs-lookup"><span data-stu-id="c2ac7-169">Controller Method</span></span> | <span data-ttu-id="c2ac7-170">URI</span><span class="sxs-lookup"><span data-stu-id="c2ac7-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="c2ac7-171">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="c2ac7-171">GetAllProducts</span></span> | <span data-ttu-id="c2ac7-172">/api/Products</span><span class="sxs-lookup"><span data-stu-id="c2ac7-172">/api/products</span></span> |
| <span data-ttu-id="c2ac7-173">GetProduct</span><span class="sxs-lookup"><span data-stu-id="c2ac7-173">GetProduct</span></span> | <span data-ttu-id="c2ac7-174">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="c2ac7-174">/api/products/*id*</span></span> |

<span data-ttu-id="c2ac7-175">`GetProduct` yöntemi için URI 'deki *kimlik* bir yer tutucudur.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="c2ac7-176">Örneğin, KIMLIĞI 5 olan ürünü almak için URI `api/products/5`.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="c2ac7-177">Web API 'sinin denetleyici yöntemlerine HTTP isteklerini nasıl yönlendirdiğini hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="c2ac7-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="c2ac7-178">JavaScript ve jQuery ile Web API 'sini çağırma</span><span class="sxs-lookup"><span data-stu-id="c2ac7-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="c2ac7-179">Bu bölümde, Web API 'sini çağırmak için AJAX kullanan bir HTML sayfası ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="c2ac7-180">AJAX çağrılarını yapmak ve ayrıca sayfayı sonuçlarla güncelleştirmek için jQuery kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="c2ac7-181">Çözüm Gezgini, projeye sağ tıklayın ve **Ekle**' yi ve ardından **Yeni öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="c2ac7-182">**Yeni öğe Ekle** iletişim kutusunda, **görsel C#** altında **Web** düğümünü seçin ve ardından **HTML sayfası** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="c2ac7-183">Sayfayı index. html&quot;&quot;olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="c2ac7-184">Bu dosyadaki her şeyi aşağıdakiler ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="c2ac7-185">JQuery almak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="c2ac7-186">Bu örnekte, [Microsoft Ajax CDN](../../../ajax/cdn/overview.md)'yi kullandım.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="c2ac7-187">Ayrıca, [http://jquery.com/](http://jquery.com/)adresinden indirebilirsiniz ve ASP.net "Web API" proje şablonu jQuery de içerir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="c2ac7-188">Ürünlerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="c2ac7-188">Getting a List of Products</span></span>

<span data-ttu-id="c2ac7-189">Ürünlerin bir listesini almak için &quot;/api/Products&quot;bir HTTP GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="c2ac7-190">JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) IşLEVI bir AJAX isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="c2ac7-191">Yanıt için JSON nesneleri dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-191">For response contains array of JSON objects.</span></span> <span data-ttu-id="c2ac7-192">`done` işlevi, istek başarılı olursa çağrılan bir geri çağırma işlemini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="c2ac7-193">Geri aramada, DOM 'ı ürün bilgileriyle güncelleştiririz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="c2ac7-194">KIMLIĞE göre ürün alma</span><span class="sxs-lookup"><span data-stu-id="c2ac7-194">Getting a Product By ID</span></span>

<span data-ttu-id="c2ac7-195">Bir ürünü KIMLIĞE göre almak için, &quot;/api/Products/*ıd*&quot;IÇIN BIR http get isteği gönderin; burada *kimlik* ürün kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="c2ac7-196">AJAX isteğini göndermek için hala `getJSON` çağrısı yaptık, ancak bu kez KIMLIĞI istek URI 'sine yerleştirtik.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="c2ac7-197">Bu istekten gelen yanıt, tek bir ürünün JSON gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="c2ac7-198">Uygulamayı Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c2ac7-198">Running the Application</span></span>

<span data-ttu-id="c2ac7-199">Uygulamada hata ayıklamaya başlamak için F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="c2ac7-200">Web sayfası aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="c2ac7-201">KIMLIĞE göre bir ürün almak için KIMLIĞI girin ve ara ' ya tıklayın:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="c2ac7-202">Geçersiz bir KIMLIK girerseniz, sunucu bir HTTP hatası döndürür:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="c2ac7-203">HTTP Isteğini ve yanıtını görüntülemek için F12 kullanma</span><span class="sxs-lookup"><span data-stu-id="c2ac7-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="c2ac7-204">Bir HTTP hizmetiyle çalışırken, HTTP isteği ve istek iletilerini görmek çok faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="c2ac7-205">Bunu, Internet Explorer 9 ' da F12 geliştirici araçlarını kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="c2ac7-206">Internet Explorer 9 ' da, araçları açmak için **F12** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="c2ac7-207">Ağ sekmesine tıklayın ve **Yakalamayı Başlat**' **a** basın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="c2ac7-208">Şimdi Web sayfasına geri dönün ve **F5** 'e basarak Web sayfasını yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="c2ac7-209">Internet Explorer, tarayıcı ile Web sunucusu arasındaki HTTP trafiğini yakalar.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="c2ac7-210">Özet görünümü bir sayfanın tüm ağ trafiğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="c2ac7-211">Göreli URI "API/Products/" girdisini bulun.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="c2ac7-212">Bu girişi seçin ve **ayrıntılı görünüme git ' e**tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="c2ac7-213">Ayrıntı görünümünde, istek ve yanıt üst bilgilerini ve gövdeleri görüntülemek için sekmeler vardır.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="c2ac7-214">Örneğin, **istek üstbilgileri** sekmesine tıklarsanız, istemcinin Accept üst bilgisinde &quot;Application/JSON&quot; isteğinde bulunduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="c2ac7-215">Yanıt gövdesi sekmesine tıklarsanız, ürün listesinin JSON olarak serileştirilme şeklini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="c2ac7-216">Diğer Tarayıcıların benzer işlevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="c2ac7-217">Bir Web hata ayıklama proxy 'si olan diğer faydalı bir araç, [Fiddler](http://www.fiddler2.com/fiddler2/)'dir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="c2ac7-218">Fiddler 'ı kullanarak HTTP trafiğinizi görüntüleyebilir ve ayrıca, istekteki HTTP üstbilgileri üzerinde tam denetim elde etmenizi sağlayan HTTP istekleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="c2ac7-219">Bkz. Azure 'da çalışan bu uygulama</span><span class="sxs-lookup"><span data-stu-id="c2ac7-219">See this App Running on Azure</span></span>

<span data-ttu-id="c2ac7-220">Canlı bir Web uygulaması olarak çalışan tamamlanmış siteyi görmek istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="c2ac7-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="c2ac7-221">Aşağıdaki düğmeye tıklayarak uygulamanın tüm sürümünü Azure hesabınıza dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="c2ac7-222">Bu çözümü Azure 'a dağıtmak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="c2ac7-223">Henüz bir hesabınız yoksa, aşağıdaki seçeneklere sahip olursunuz:</span><span class="sxs-lookup"><span data-stu-id="c2ac7-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="c2ac7-224">[Ücretsiz bir Azure hesabı açarak](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) ücretli Azure hizmetlerini denemek için kullanabileceğiniz krediler edinin ve hatta kullanıldıktan sonra bile hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="c2ac7-225">[MSDN abonesi avantajlarınızı etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN aboneliğiniz, ücretli Azure hizmetleri için kullanabileceğiniz her ay krediler sunar.</span><span class="sxs-lookup"><span data-stu-id="c2ac7-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2ac7-226">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c2ac7-226">Next Steps</span></span>

- <span data-ttu-id="c2ac7-227">GÖNDERME, YERLEŞTIRME ve SILME eylemlerini ve veritabanına yazma işlemlerini destekleyen bir HTTP hizmetinin daha kapsamlı bir örneği için bkz. [Entity Framework 6 Ile Web API 2 kullanma](../data/using-web-api-with-entity-framework/part-1.md).</span><span class="sxs-lookup"><span data-stu-id="c2ac7-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="c2ac7-228">HTTP hizmetinin üstünde akıcı ve hızlı yanıt veren Web uygulamaları oluşturma hakkında daha fazla bilgi için bkz. [ASP.net Single Page Application](../../../single-page-application/index.md).</span><span class="sxs-lookup"><span data-stu-id="c2ac7-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="c2ac7-229">Azure App Service için bir Visual Studio Web projesi dağıtma hakkında daha fazla bilgi için, bkz. [Azure App Service Web uygulaması oluşturma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span><span class="sxs-lookup"><span data-stu-id="c2ac7-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
