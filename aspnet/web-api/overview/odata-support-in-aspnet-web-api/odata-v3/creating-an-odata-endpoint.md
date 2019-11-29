---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2 ile OData v3 uç noktası oluşturma | Microsoft Docs
author: MikeWasson
description: Açık Veri Protokolü (OData) Web için bir veri erişim protokolüdür. OData, verileri yapılandırmak, verileri sorgulamak ve verileri işlemek için Tekdüzen bir yol sağlar...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600427"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="e1ea3-104">Web API 2 ile OData v3 uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ea3-104">Creating an OData v3 Endpoint with Web API 2</span></span>

<span data-ttu-id="e1ea3-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e1ea3-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="e1ea3-106">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="e1ea3-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="e1ea3-107">[Açık Veri Protokolü](http://www.odata.org/) (OData) Web için bir veri erişim protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="e1ea3-108">OData, verileri yapılandırmak, verileri sorgulamak ve veri kümesini CRUD işlemleri (oluşturma, okuma, güncelleştirme ve silme) aracılığıyla işlemek için Tekdüzen bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="e1ea3-109">OData hem AtomPub (XML) hem de JSON biçimlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="e1ea3-110">OData Ayrıca veriler hakkında meta verileri açığa çıkarmak için bir yol tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="e1ea3-111">İstemciler, veri kümesine ilişkin tür bilgilerini ve ilişkilerini saptamak için meta verileri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="e1ea3-112">ASP.NET Web API 'SI, bir veri kümesi için OData uç noktası oluşturmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="e1ea3-113">Endpoint 'in hangi OData işlemlerini desteklediğini tam olarak denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="e1ea3-114">OData dışı uç noktaları ile birlikte birden çok OData uç noktası barındırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="e1ea3-115">Veri modeliniz, arka uç iş mantığı ve veri katmanınız üzerinde tam denetim sahibi olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e1ea3-116">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="e1ea3-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="e1ea3-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e1ea3-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="e1ea3-118">Web API 2</span><span class="sxs-lookup"><span data-stu-id="e1ea3-118">Web API 2</span></span>
> - <span data-ttu-id="e1ea3-119">OData sürüm 3</span><span class="sxs-lookup"><span data-stu-id="e1ea3-119">OData Version 3</span></span>
> - <span data-ttu-id="e1ea3-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="e1ea3-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="e1ea3-121">Fiddler Web hata ayıklama proxy (Isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="e1ea3-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="e1ea3-122">Web API OData desteği [ASP.NET and Web Tools 2012,2 güncelleştirmesine](https://go.microsoft.com/fwlink/?LinkId=282650)eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="e1ea3-123">Ancak, bu öğretici Visual Studio 2013 eklenen yapı iskelesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>

<span data-ttu-id="e1ea3-124">Bu öğreticide, istemcilerin sorgulayabilirler basit bir OData uç noktası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="e1ea3-125">Uç nokta için de bir C# istemci oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="e1ea3-126">Bu Öğreticiyi tamamladıktan sonra, bir sonraki öğretici kümesinde varlık ilişkileri, Eylemler ve $expand/$select dahil daha fazla işlevsellik ekleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="e1ea3-127">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ea3-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="e1ea3-128">Varlık modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="e1ea3-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="e1ea3-129">OData denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="e1ea3-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="e1ea3-130">EDM ve rota Ekle</span><span class="sxs-lookup"><span data-stu-id="e1ea3-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="e1ea3-131">Veritabanını çekirdek olarak (Isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="e1ea3-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="e1ea3-132">OData uç noktasını keşfetme</span><span class="sxs-lookup"><span data-stu-id="e1ea3-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="e1ea3-133">OData serileştirme biçimleri</span><span class="sxs-lookup"><span data-stu-id="e1ea3-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="e1ea3-134">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ea3-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="e1ea3-135">Bu öğreticide, temel CRUD işlemlerini destekleyen bir OData uç noktası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="e1ea3-136">Uç nokta tek bir kaynak ve ürünlerin bir listesini ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="e1ea3-137">Daha sonraki öğreticiler daha fazla özellik ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="e1ea3-138">Visual Studio 'Yu başlatın ve başlangıç sayfasından **Yeni proje** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="e1ea3-139">Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="e1ea3-140">**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve görsel C# düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="e1ea3-141">**Görsel C#** bölümünde **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="e1ea3-142">**ASP.NET Web uygulaması** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="e1ea3-143">**Yeni ASP.NET projesi** Iletişim kutusunda **boş** şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="e1ea3-144">&quot;altında...&quot;klasör ve çekirdek başvuruları ekleyin, **Web API 'sini**kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="e1ea3-145">**Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="e1ea3-146">Varlık modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="e1ea3-146">Add an Entity Model</span></span>

<span data-ttu-id="e1ea3-147">*Model* , uygulamanızdaki verileri temsil eden bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="e1ea3-148">Bu öğreticide, bir ürünü temsil eden bir modele ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="e1ea3-149">Model, OData varlık türüne karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="e1ea3-150">Çözüm Gezgini modeller klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="e1ea3-151">Bağlam menüsünden **Ekle** ' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="e1ea3-152">Yeni öğe **Ekle** iletişim kutusunda, &quot;ürün&quot;adını adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="e1ea3-153">Kurala göre model sınıfları modeller klasörüne yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="e1ea3-154">Bu kuralı kendi projelerinizde izlemeniz gerekmez, ancak bu öğreticide bunu kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>

<span data-ttu-id="e1ea3-155">Product.cs dosyasında aşağıdaki sınıf tanımını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="e1ea3-156">ID özelliği varlık anahtarı olacak.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-156">The ID property will be the entity key.</span></span> <span data-ttu-id="e1ea3-157">İstemciler, ürünleri KIMLIĞE göre sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-157">Clients can query products by ID.</span></span> <span data-ttu-id="e1ea3-158">Bu alan, arka uç veritabanında da birincil anahtar olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="e1ea3-159">Projeyi şimdi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-159">Build the project now.</span></span> <span data-ttu-id="e1ea3-160">Bir sonraki adımda, ürün türünü bulmak için yansıma kullanan bazı Visual Studio yapı iskelesi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="e1ea3-161">OData denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="e1ea3-161">Add an OData Controller</span></span>

<span data-ttu-id="e1ea3-162">*Denetleyici* , http isteklerini işleyen bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="e1ea3-163">OData hizmetinde her bir varlık kümesi için ayrı bir denetleyici tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="e1ea3-164">Bu öğreticide, tek bir denetleyici oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="e1ea3-165">Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="e1ea3-166">**Ekle** ' yi ve ardından **Denetleyici**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="e1ea3-167">**İskele Ekle** iletişim kutusunda, Entity Framework&quot;kullanarak eylemleri olan &quot;Web API 2 OData denetleyicisi ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="e1ea3-168">**Denetleyici Ekle** iletişim kutusunda "ProductsController" adlı denetleyiciyi adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="e1ea3-169">Zaman uyumsuz denetleyici eylemlerini kullan&quot; onay kutusunu &quot;seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="e1ea3-170">**Model** açılan listesinde ürün sınıfını seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="e1ea3-171">**Yeni veri bağlamı...** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-171">Click the **New data context...** button.</span></span> <span data-ttu-id="e1ea3-172">Veri bağlamı türü için varsayılan adı bırakın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="e1ea3-173">Denetleyiciyi eklemek için denetleyici Ekle iletişim kutusunda Ekle ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="e1ea3-174">Note:...&quot;türü alınırken bir hata olduğunu &quot;belirten bir hata iletisi alırsanız, ürün sınıfını ekledikten sonra Visual Studio projesini derlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="e1ea3-175">Scafkatlama, sınıfını bulmak için yansıma kullanır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="e1ea3-176">Scafkatlama, projeye iki kod dosyası ekler:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="e1ea3-177">Products.cs OData uç noktasını uygulayan Web API denetleyicisini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="e1ea3-178">ProductServiceContext.cs, Entity Framework kullanarak temel veritabanını sorgulamak için yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="e1ea3-179">EDM ve rota Ekle</span><span class="sxs-lookup"><span data-stu-id="e1ea3-179">Add the EDM and Route</span></span>

<span data-ttu-id="e1ea3-180">Çözüm Gezgini ' de, uygulama\_Başlat klasörünü genişletin ve WebApiConfig.cs adlı dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="e1ea3-181">Bu sınıf, Web API 'SI için yapılandırma kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="e1ea3-182">Bu kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="e1ea3-183">Bu kod iki şeyi yapar:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-183">This code does two things:</span></span>

- <span data-ttu-id="e1ea3-184">OData uç noktası için bir Varlık Veri Modeli (EDM) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="e1ea3-185">Uç nokta için bir yol ekler.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="e1ea3-186">EDM, verilerin soyut bir modelidir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="e1ea3-187">EDM, meta veri belgesini oluşturmak ve hizmet için URI 'Leri tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="e1ea3-188">**ODataConventionModelBuilder** , EDM varsayılan adlandırma kuralları kümesini kullanarak bir EDM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="e1ea3-189">Bu yaklaşım için en az kod gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-189">This approach requires the least code.</span></span> <span data-ttu-id="e1ea3-190">EDM üzerinde daha fazla denetim istiyorsanız, özellik, anahtar ve gezinti özelliklerini açıkça ekleyerek EDM oluşturmak için **ODataModelBuilder** sınıfını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="e1ea3-191">**EntitySet** YÖNTEMI, EDM öğesine bir varlık kümesi ekler:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="e1ea3-192">"Products" dizesi varlık kümesinin adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="e1ea3-193">Denetleyicinin adı, varlık kümesinin adı ile aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="e1ea3-194">Bu öğreticide, varlık kümesi "Ürünler" olarak adlandırılmıştır ve denetleyicinin adı `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="e1ea3-195">"ProductSet" varlık kümesini adlandırdıysanız, denetleyiciyi `ProductSetController`olarak adlandırmış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="e1ea3-196">Bir uç noktanın birden çok varlık kümesine sahip olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="e1ea3-197">Her varlık kümesi için **EntitySet&lt;t&gt;** çağırın ve ardından karşılık gelen bir denetleyici tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="e1ea3-198">**MapODataRoute** yöntemi OData uç noktası için bir yol ekler.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="e1ea3-199">İlk parametre yol için kolay bir addır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="e1ea3-200">Hizmetinizin istemcileri bu adı görmez.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="e1ea3-201">İkinci parametre uç noktanın URI önekidir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="e1ea3-202">Bu kod verildiğinde, Products varlık kümesi URI 'SI http://<em>hostname</em>/OData/Products. olur.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="e1ea3-203">Uygulamanız birden fazla OData uç noktasına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="e1ea3-204">Her uç nokta için, <strong>MapODataRoute</strong> çağırın ve benzersiz bir yol adı ve BENZERSIZ bir URI öneki sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="e1ea3-205">Veritabanını çekirdek olarak (Isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="e1ea3-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="e1ea3-206">Bu adımda, veritabanını bazı test verileriyle temel almak için Entity Framework kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="e1ea3-207">Bu adım isteğe bağlıdır, ancak OData uç noktanızı hemen test etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="e1ea3-208">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="e1ea3-209">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="e1ea3-210">Bu, geçişler adlı bir klasör ve Configuration.cs adlı bir kod dosyası ekler.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="e1ea3-211">Bu dosyayı açın ve `Configuration.Seed` yöntemine aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="e1ea3-212">Paket Yöneticisi konsolu penceresinde aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="e1ea3-213">Bu komutlar veritabanını oluşturan kodu oluşturur ve ardından bu kodu yürütür.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="e1ea3-214">OData uç noktasını keşfetme</span><span class="sxs-lookup"><span data-stu-id="e1ea3-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="e1ea3-215">Bu bölümde, uç noktalara istek göndermek ve yanıt iletilerini incelemek için [Fiddler Web hata ayıklama proxy](http://www.fiddler2.com) 'sini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="e1ea3-216">Bu, bir OData uç noktasının yeteneklerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="e1ea3-217">Visual Studio 'da hata ayıklamayı başlatmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="e1ea3-218">Varsayılan olarak, Visual Studio tarayıcınızı `http://localhost:*port*`için açar, burada *bağlantı noktası* proje ayarlarında yapılandırılan bağlantı noktası numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="e1ea3-219">Proje ayarlarındaki bağlantı noktası numarasını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="e1ea3-220">Çözüm Gezgini, projeye sağ tıklayın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="e1ea3-221">Özellikler penceresinde **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="e1ea3-222">**Proje URL 'si**altında bağlantı noktası numarasını girin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="e1ea3-223">Hizmet belgesi</span><span class="sxs-lookup"><span data-stu-id="e1ea3-223">Service Document</span></span>

<span data-ttu-id="e1ea3-224">*Hizmet belgesi* , OData uç noktası için varlık kümelerinin bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="e1ea3-225">Hizmet belgesini almak için, hizmetin kök URI 'sine bir GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="e1ea3-226">Fiddler 'ı kullanarak, **Oluşturucu** SEKMESINE aşağıdaki URI 'yi girin: `http://localhost:port/odata/`, *bağlantı* noktası numarası.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="e1ea3-227">**Yürüt** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-227">Click the **Execute** button.</span></span> <span data-ttu-id="e1ea3-228">Fiddler uygulamanıza bir HTTP GET isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="e1ea3-229">Yanıtı Web oturumları listesinde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="e1ea3-230">Her şey çalışıyorsa, durum kodu 200 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="e1ea3-231">Inspector sekmesinde yanıt iletisinin ayrıntılarını görmek için Web oturumları listesinde yanıta çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="e1ea3-232">Ham HTTP yanıt iletisi aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="e1ea3-233">Varsayılan olarak, Web API 'SI, AtomPub biçimindeki hizmet belgesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="e1ea3-234">JSON istemek için, HTTP isteğine aşağıdaki üstbilgiyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="e1ea3-235">HTTP yanıtı şu anda bir JSON yükü içeriyor:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="e1ea3-236">Hizmet meta verileri belgesi</span><span class="sxs-lookup"><span data-stu-id="e1ea3-236">Service Metadata Document</span></span>

<span data-ttu-id="e1ea3-237">*Hizmet meta verileri belgesi* , kavramsal şema tanım DILI (csdl) adı VERILEN bir xml dili kullanılarak hizmetin veri modelini açıklar.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="e1ea3-238">Meta veri belgesi, hizmette verilerin yapısını gösterir ve istemci kodu oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="e1ea3-239">Meta veri belgesini almak için `http://localhost:port/odata/$metadata`için bir GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="e1ea3-240">Bu öğreticide gösterilen uç nokta için meta veriler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="e1ea3-241">Varlık kümesi</span><span class="sxs-lookup"><span data-stu-id="e1ea3-241">Entity Set</span></span>

<span data-ttu-id="e1ea3-242">Products varlık kümesini almak için `http://localhost:port/odata/Products`için bir GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="e1ea3-243">Varlık</span><span class="sxs-lookup"><span data-stu-id="e1ea3-243">Entity</span></span>

<span data-ttu-id="e1ea3-244">Tek bir ürün almak için, `http://localhost:port/odata/Products(1)`için bir GET isteği gönderin, burada "1" ürün KIMLIĞIDIR.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="e1ea3-245">OData serileştirme biçimleri</span><span class="sxs-lookup"><span data-stu-id="e1ea3-245">OData Serialization Formats</span></span>

<span data-ttu-id="e1ea3-246">OData birkaç serileştirme biçimini destekler:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="e1ea3-247">Atom pub (XML)</span><span class="sxs-lookup"><span data-stu-id="e1ea3-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="e1ea3-248">JSON "Light" (OData v3 'de kullanıma sunuldu)</span><span class="sxs-lookup"><span data-stu-id="e1ea3-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="e1ea3-249">JSON "verbose" (OData v2)</span><span class="sxs-lookup"><span data-stu-id="e1ea3-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="e1ea3-250">Varsayılan olarak, Web API 'SI AtomPubJSON "Light" biçimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="e1ea3-251">AtomPub biçimini almak için Accept üst bilgisini "Application/atom + xml" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="e1ea3-252">Örnek bir yanıt gövdesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="e1ea3-253">Atom biçiminin belirgin bir dezavantajına bakabilirsiniz: Bu, JSON ışığının daha ayrıntılıdır.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="e1ea3-254">Ancak, AtomPub 'yi anlayan bir istemciniz varsa, istemci bu biçimi JSON üzerinden tercih edebilir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="e1ea3-255">Aynı varlığın JSON hafif sürümü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="e1ea3-256">JSON light biçimi, OData protokolünün 3. sürümünde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="e1ea3-257">Geriye dönük uyumluluk için, bir istemci eski "ayrıntılı" JSON biçimini talep edebilir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="e1ea3-258">Ayrıntılı JSON istemek için Accept üst bilgisini `application/json;odata=verbose`olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="e1ea3-259">Verbose sürümü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e1ea3-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="e1ea3-260">Bu biçim yanıt gövdesinde daha fazla meta veri getirir. Bu, bir oturumun tamamına çok fazla yük eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="e1ea3-261">Ayrıca, nesneyi "d" adlı bir özellikte sarmalayarak bir yöneltme düzeyi ekler.</span><span class="sxs-lookup"><span data-stu-id="e1ea3-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1ea3-262">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e1ea3-262">Next Steps</span></span>

- [<span data-ttu-id="e1ea3-263">Varlık Ilişkileri ekleme</span><span class="sxs-lookup"><span data-stu-id="e1ea3-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="e1ea3-264">OData eylemleri ekleme</span><span class="sxs-lookup"><span data-stu-id="e1ea3-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="e1ea3-265">Bir .NET Istemcisinden OData hizmetini çağırma</span><span class="sxs-lookup"><span data-stu-id="e1ea3-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
