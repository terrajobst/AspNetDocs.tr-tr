---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 ile çalışmaya başlama (C#)-ASP.NET 4.x
author: MikeWasson
description: Kod ile öğretici. ASP.NET Web API, bir web ürünlerin listesini döndüren API oluşturmak için kullanın.
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5e3c049ba4349301c3c2d173d4311b3d0883bf68
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59401757"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="de2d7-104">ASP.NET Web API 2 (C#) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="de2d7-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="de2d7-105">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="de2d7-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="de2d7-106">Projeyi yükle</span><span class="sxs-lookup"><span data-stu-id="de2d7-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="de2d7-107">Bu öğreticide, bir web ürünlerin listesini döndüren API oluşturmak için ASP.NET Web API kullanır.</span><span class="sxs-lookup"><span data-stu-id="de2d7-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="de2d7-108">HTTP web sayfaları yalnızca hizmet vermek için değil.</span><span class="sxs-lookup"><span data-stu-id="de2d7-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="de2d7-109">Ayrıca veri ve hizmetlerinizi kullanıma API'leri oluşturmaya yönelik güçlü bir platform HTTP'dir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="de2d7-110">Basit, esnek ve her yerde karşılaşılan HTTP'dir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="de2d7-111">İstemciler, tarayıcılar, mobil cihazları ve geleneksel masaüstü uygulamaları gibi çok geniş bir yelpazede HTTP Hizmetleri ulaşabilmeniz için bir HTTP kitaplığı kadar aklınıza gelebilecek neredeyse herhangi bir platform sahiptir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="de2d7-112">ASP.NET Web API'si, .NET Framework üzerinde web API'leri oluşturmaya yönelik bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="de2d7-113">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="de2d7-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="de2d7-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="de2d7-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="de2d7-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="de2d7-115">Web API 2</span></span>

<span data-ttu-id="de2d7-116">Bkz: [ASP.NET Core ve Windows için Visual Studio ile web API'si oluşturma](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) Bu öğreticinin daha yeni bir sürümü için.</span><span class="sxs-lookup"><span data-stu-id="de2d7-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="de2d7-117">Bir Web API projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="de2d7-117">Create a Web API Project</span></span>

<span data-ttu-id="de2d7-118">Bu öğreticide, bir web ürünlerin listesini döndüren API oluşturmak için ASP.NET Web API kullanır.</span><span class="sxs-lookup"><span data-stu-id="de2d7-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="de2d7-119">Ön uç web sayfası, sonuçları görüntülemek için jQuery kullanır.</span><span class="sxs-lookup"><span data-stu-id="de2d7-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="de2d7-120">Visual Studio'yu başlatın ve seçin **yeni proje** gelen **Başlat** sayfası.</span><span class="sxs-lookup"><span data-stu-id="de2d7-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="de2d7-121">Veya **dosya** menüsünde **yeni** ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="de2d7-122">İçinde **şablonları** bölmesinde **yüklü şablonlar** genişletin **Visual C#** düğümü.</span><span class="sxs-lookup"><span data-stu-id="de2d7-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="de2d7-123">Altında **Visual C#** seçin **Web**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="de2d7-124">Proje şablonları listesinde seçin **ASP.NET Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="de2d7-125">"ProductsApp" Projeyi adlandırın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="de2d7-126">İçinde **yeni ASP.NET projesi** iletişim kutusunda **boş** şablonu.</span><span class="sxs-lookup"><span data-stu-id="de2d7-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="de2d7-127">Altında &quot;klasörleri ekleyin ve çekirdek başvuruları&quot;, kontrol **Web API**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="de2d7-128">**Tamam**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="de2d7-129">Kullanarak bir Web API projesi oluşturabilirsiniz &quot;Web API&quot; şablonu.</span><span class="sxs-lookup"><span data-stu-id="de2d7-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="de2d7-130">API Yardım sayfaları sağlamak için ASP.NET MVC Web API şablonu kullanır.</span><span class="sxs-lookup"><span data-stu-id="de2d7-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="de2d7-131">MVC olmadan Web API gösterilecek istediğinden Bu öğretici için boş şablonu kullanıyorum.</span><span class="sxs-lookup"><span data-stu-id="de2d7-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="de2d7-132">Genel olarak, ASP.NET MVC, Web API'sini kullanmak için bilmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="de2d7-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>


## <a name="adding-a-model"></a><span data-ttu-id="de2d7-133">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="de2d7-133">Adding a Model</span></span>

<span data-ttu-id="de2d7-134">A *modeli* uygulamanızdaki verileri temsil eden bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="de2d7-135">ASP.NET Web API'si, JSON, XML veya başka bir biçime modelinizi otomatik serileştir ve HTTP yanıt iletisinin gövdesine serileştirilmiş veriler yazın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="de2d7-136">Bir istemci serileştirme biçimi okuyabilirsiniz sürece, nesne seri durumdan çıkarabiliyorsa.</span><span class="sxs-lookup"><span data-stu-id="de2d7-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="de2d7-137">Çoğu istemci, XML veya JSON ayrıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="de2d7-138">Ayrıca, istemci HTTP isteğine bir Accept üst bilgisi ayarlayarak istediği hangi biçimi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="de2d7-139">Bir ürünü temsil eden basit bir modeli oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="de2d7-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="de2d7-140">Çözüm Gezgini görünür değilse, **görünümü** menü ve select **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="de2d7-141">Çözüm Gezgini'nde modeller klasörü sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="de2d7-142">Bağlam menüsünden seçin **Ekle** seçip **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="de2d7-143">Sınıf adı &quot;ürün&quot;.</span><span class="sxs-lookup"><span data-stu-id="de2d7-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="de2d7-144">Aşağıdaki özellikleri `Product` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="de2d7-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="de2d7-145">Denetleyici Ekleme</span><span class="sxs-lookup"><span data-stu-id="de2d7-145">Adding a Controller</span></span>

<span data-ttu-id="de2d7-146">Web API'de bir *denetleyicisi* HTTP isteklerini işleyen bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="de2d7-147">Ürünlerin listesini ya da kimliği ile belirtilen tek bir ürün döndürebilen bir denetleyici ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="de2d7-148">ASP.NET MVC kullandıysanız denetleyicileriyle bilginiz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="de2d7-149">Web API denetleyicisi, MVC denetleyicileri için benzerdir, ancak devralınan **ApiController** sınıfı yerine **denetleyicisi** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="de2d7-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="de2d7-150">İçinde **Çözüm Gezgini**, denetleyicileri klasörü sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="de2d7-151">Seçin **Ekle** seçip **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="de2d7-152">İçinde **İskele Ekle** iletişim kutusunda **Web API denetleyicisi – boş**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="de2d7-153">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="de2d7-154">İçinde **denetleyici Ekle** iletişim kutusunda, denetleyici adı &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="de2d7-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="de2d7-155">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="de2d7-156">Yapı iskelesinde denetleyicileri klasöründeki ProductsController.cs adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="de2d7-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="de2d7-157">Denetleyicilerinizi denetleyicileri adlı klasöre koyun gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="de2d7-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="de2d7-158">Klasör adı, kaynak dosyalarınızı düzenlemek için yalnızca bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="de2d7-158">The folder name is just a convenient way to organize your source files.</span></span>


<span data-ttu-id="de2d7-159">Bu dosya zaten açık değilse, açmak için dosyaya çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="de2d7-160">Bu dosyadaki kodu aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="de2d7-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="de2d7-161">Örneği basit tutmak için ürünleri sabit bir dizi denetleyici sınıfı içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="de2d7-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="de2d7-162">Elbette, gerçek bir uygulamada, veritabanını sorgulama veya başka bir dış veri kaynağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="de2d7-163">Denetleyici ürünleri döndüren iki yöntemi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="de2d7-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="de2d7-164">`GetAllProducts` Yöntemi ürünlerin tam listesini döndüren bir **IEnumerable&lt;ürün&gt;**  türü.</span><span class="sxs-lookup"><span data-stu-id="de2d7-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="de2d7-165">`GetProduct` Kendi kimliği tarafından tek bir ürün şuna yöntemi</span><span class="sxs-lookup"><span data-stu-id="de2d7-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="de2d7-166">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="de2d7-166">That's it!</span></span> <span data-ttu-id="de2d7-167">Sahip olduğunuz çalışma web API'si.</span><span class="sxs-lookup"><span data-stu-id="de2d7-167">You have a working web API.</span></span> <span data-ttu-id="de2d7-168">Denetleyicisindeki her yöntem için en az bir URI'leri karşılık gelmektedir:</span><span class="sxs-lookup"><span data-stu-id="de2d7-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="de2d7-169">Denetleyici yöntemi</span><span class="sxs-lookup"><span data-stu-id="de2d7-169">Controller Method</span></span> | <span data-ttu-id="de2d7-170">URI</span><span class="sxs-lookup"><span data-stu-id="de2d7-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="de2d7-171">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="de2d7-171">GetAllProducts</span></span> | <span data-ttu-id="de2d7-172">/ api/ürünleri</span><span class="sxs-lookup"><span data-stu-id="de2d7-172">/api/products</span></span> |
| <span data-ttu-id="de2d7-173">GetProduct</span><span class="sxs-lookup"><span data-stu-id="de2d7-173">GetProduct</span></span> | <span data-ttu-id="de2d7-174">/API'si/ürünler/*kimliği*</span><span class="sxs-lookup"><span data-stu-id="de2d7-174">/api/products/*id*</span></span> |

<span data-ttu-id="de2d7-175">İçin `GetProduct` yöntemi *kimliği* URI'de bir yer tutucudur.</span><span class="sxs-lookup"><span data-stu-id="de2d7-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="de2d7-176">Örneğin, 5 Kimliğine sahip bir ürün almak için URI değil `api/products/5`.</span><span class="sxs-lookup"><span data-stu-id="de2d7-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="de2d7-177">Web API HTTP istekleri için denetleyici yöntemleri nasıl yönlendirdiğini hakkında daha fazla bilgi için bkz. [ASP.NET Web API'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="de2d7-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="de2d7-178">Javascript ve jQuery ile Web API çağırma</span><span class="sxs-lookup"><span data-stu-id="de2d7-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="de2d7-179">Bu bölümde, web API'sini çağırmak için AJAX kullanan bir HTML sayfasına ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="de2d7-180">AJAX çağrılarını ve sayfa sonuçları ile güncelleştirmek için jQuery kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="de2d7-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="de2d7-181">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **Ekle**, ardından **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="de2d7-182">İçinde **Yeni Öğe Ekle** iletişim kutusunda **Web** düğümünde **Visual C#** ve ardından **HTML sayfası** öğesi.</span><span class="sxs-lookup"><span data-stu-id="de2d7-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="de2d7-183">Sayfayı adlandırın &quot;index.html&quot;.</span><span class="sxs-lookup"><span data-stu-id="de2d7-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="de2d7-184">Bu dosyadaki her şeyi aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="de2d7-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="de2d7-185">JQuery almak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="de2d7-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="de2d7-186">Bu örnekte, kullandım [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span><span class="sxs-lookup"><span data-stu-id="de2d7-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="de2d7-187">Nden de indirebilirsiniz [ http://jquery.com/ ](http://jquery.com/)ve "Web API'si" ASP.NET proje şablonu, jQuery de içerir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="de2d7-188">Ürünlerin listesini alma</span><span class="sxs-lookup"><span data-stu-id="de2d7-188">Getting a List of Products</span></span>

<span data-ttu-id="de2d7-189">Ürünlerin listesini almak için bir HTTP GET isteği gönderme &quot;/api/ürünleri&quot;.</span><span class="sxs-lookup"><span data-stu-id="de2d7-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="de2d7-190">JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) işlevi bir AJAX isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="de2d7-191">Yanıt için JSON nesne dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-191">For response contains array of JSON objects.</span></span> <span data-ttu-id="de2d7-192">`done` İşlevi istek başarılı olursa çağrılan bir geri çağırma işlemini belirtir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="de2d7-193">Geri çağırma içinde ürün bilgileri DOM güncelleştiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="de2d7-194">Bir ürün Kimliğine göre alma</span><span class="sxs-lookup"><span data-stu-id="de2d7-194">Getting a Product By ID</span></span>

<span data-ttu-id="de2d7-195">Kimliğe göre bir ürün almak için bir HTTP GET isteği gönderme &quot;/API'si/ürünler/*kimliği*&quot;burada *kimliği* ürün kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="de2d7-196">Hala diyoruz `getJSON` AJAX isteği, ancak bu kez göndermek için biz kimliği URI isteğinde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="de2d7-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="de2d7-197">Bu istek yanıtı tek bir ürün JSON gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="de2d7-198">Uygulamayı Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="de2d7-198">Running the Application</span></span>

<span data-ttu-id="de2d7-199">Uygulamada hata ayıklamaya başlamak için F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="de2d7-200">Web sayfasını aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="de2d7-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="de2d7-201">Kimliğe göre bir ürün almak için kimliği girin ve ara:</span><span class="sxs-lookup"><span data-stu-id="de2d7-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="de2d7-202">Geçersiz kimlik girerseniz, sunucunun bir HTTP hata döndürür:</span><span class="sxs-lookup"><span data-stu-id="de2d7-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="de2d7-203">HTTP istek ve yanıt görüntülemek için F12'ı kullanma</span><span class="sxs-lookup"><span data-stu-id="de2d7-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="de2d7-204">Bir HTTP hizmeti ile çalışırken, HTTP isteği görmek ve iletileri istek çok kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="de2d7-205">Internet Explorer 9'da F12 geliştirici araçlarını kullanarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="de2d7-206">Internet Explorer 9'dan basın **F12** Araçları'nı açın.</span><span class="sxs-lookup"><span data-stu-id="de2d7-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="de2d7-207">Tıklayın **ağ** sekmesi ve ENTER tuşuna **Yakalamayı Başlat**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="de2d7-208">Artık a basın ve web sayfasına dönün **F5** web sayfasını yeniden yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="de2d7-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="de2d7-209">Internet Explorer tarayıcı ve web sunucusu arasında HTTP trafiğini yakalar.</span><span class="sxs-lookup"><span data-stu-id="de2d7-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="de2d7-210">Özet görünümü, bir sayfa için tüm ağ trafiğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="de2d7-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="de2d7-211">Göreli URI'si girişini bulun "API/Ürünler /".</span><span class="sxs-lookup"><span data-stu-id="de2d7-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="de2d7-212">Bu girdiyi seçin ve tıklayın **ayrıntılı görünümüne gidin**.</span><span class="sxs-lookup"><span data-stu-id="de2d7-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="de2d7-213">Ayrıntılı görünümde gövdeleri ve istek ve yanıt üst bilgileri görüntülemek için sekme bulunur.</span><span class="sxs-lookup"><span data-stu-id="de2d7-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="de2d7-214">Örneğin, tıklarsanız **istek üst** sekmesinde istemci istenen görebilirsiniz &quot;application/json&quot; Accept üstbilgisindeki.</span><span class="sxs-lookup"><span data-stu-id="de2d7-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="de2d7-215">Yanıt gövdesi sekmesini tıklatırsanız, nasıl ürün listesi JSON için seri duruma görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="de2d7-216">Diğer tarayıcılarda benzer işlevselliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="de2d7-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="de2d7-217">Başka bir kullanışlı bir araçtır [Fiddler](http://www.fiddler2.com/fiddler2/), bir web proxy hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="de2d7-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="de2d7-218">Fiddler, HTTP trafiğini görüntülemek için ve ayrıca HTTP istekleri oluşturmak için istek HTTP üstbilgilerini üzerinde tam denetim imkanı sağlayan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="de2d7-219">Azure üzerinde çalışan bu uygulamayı bakın</span><span class="sxs-lookup"><span data-stu-id="de2d7-219">See this App Running on Azure</span></span>

<span data-ttu-id="de2d7-220">Canlı web uygulaması olarak çalışan tamamlanmış site görmek ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="de2d7-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="de2d7-221">Aşağıdaki düğmeye tıklayarak Azure hesabınızda bir tam sürümü uygulama dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="de2d7-222">Bu çözüm, Azure'a dağıtmak için bir Azure hesabına ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="de2d7-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="de2d7-223">Bir hesap zaten yoksa, aşağıdaki seçenekleriniz:</span><span class="sxs-lookup"><span data-stu-id="de2d7-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="de2d7-224">[Ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -KREDİLERİ edinin, ücretli Azure hizmetlerini denemek için kullanabileceğiniz ve hatta kullanıldıktan sonra en fazla hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de2d7-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="de2d7-225">[MSDN abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN aboneliğiniz size kredi verir, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.</span><span class="sxs-lookup"><span data-stu-id="de2d7-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de2d7-226">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="de2d7-226">Next Steps</span></span>

- <span data-ttu-id="de2d7-227">POST, PUT ve DELETE işlemleri destekleyen ve bir veritabanına yazar HTTP hizmetine daha eksiksiz bir örnek için bkz: [Entity Framework 6 ile Web API 2 kullanarak](../data/using-web-api-with-entity-framework/part-1.md).</span><span class="sxs-lookup"><span data-stu-id="de2d7-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="de2d7-228">Bir HTTP hizmetine üzerine esnektir, hızlı yanıt veren web uygulamaları oluşturma hakkında daha fazla bilgi için bkz. [ASP.NET tek sayfalık uygulaması](../../../single-page-application/index.md).</span><span class="sxs-lookup"><span data-stu-id="de2d7-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="de2d7-229">Visual Studio web projesini Azure App Service'e dağıtma hakkında daha fazla bilgi için bkz: [Azure App Service'te ASP.NET web uygulaması oluşturma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span><span class="sxs-lookup"><span data-stu-id="de2d7-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
