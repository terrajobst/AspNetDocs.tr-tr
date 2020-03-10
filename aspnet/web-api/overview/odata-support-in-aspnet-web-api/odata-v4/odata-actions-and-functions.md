---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: ASP.NET Web API 2,2 kullanılarak OData v4 'deki eylemler ve Işlevler | Microsoft Docs
author: MikeWasson
description: OData 'de, Eylemler ve işlevler, varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur. Bu öğreticide nasıl yapılacağı gösterilmektedir...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556226"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="2260b-104">ASP.NET Web API 2,2 kullanılarak OData v4 'deki eylemler ve Işlevler</span><span class="sxs-lookup"><span data-stu-id="2260b-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="2260b-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2260b-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="2260b-106">OData 'de, Eylemler ve işlevler, varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="2260b-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="2260b-107">Bu öğreticide, Web API 2,2 kullanılarak bir OData v4 uç noktasına eylemler ve işlevlerin nasıl ekleneceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2260b-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="2260b-108">Öğretici, [ASP.NET Web API 2 kullanarak bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md) öğreticisinde derleme</span><span class="sxs-lookup"><span data-stu-id="2260b-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2260b-109">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="2260b-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="2260b-110">Web API 2,2</span><span class="sxs-lookup"><span data-stu-id="2260b-110">Web API 2.2</span></span>
> - <span data-ttu-id="2260b-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="2260b-111">OData v4</span></span>
> - <span data-ttu-id="2260b-112">Visual Studio 2013 (Visual Studio 2017 'yi [buraya](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)indirin)</span><span class="sxs-lookup"><span data-stu-id="2260b-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="2260b-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2260b-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="2260b-114">Öğretici sürümleri</span><span class="sxs-lookup"><span data-stu-id="2260b-114">Tutorial versions</span></span>
>
> <span data-ttu-id="2260b-115">OData sürüm 3 için bkz. [ASP.NET Web API 2 ' de OData eylemleri](../odata-v3/odata-actions.md).</span><span class="sxs-lookup"><span data-stu-id="2260b-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="2260b-116">*Eylemler* ve *işlevler* arasındaki fark, eylemlerin yan etkileri olabilir ve işlevleri değildir.</span><span class="sxs-lookup"><span data-stu-id="2260b-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="2260b-117">Hem eylemler hem de işlevler veri döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="2260b-117">Both actions and functions can return data.</span></span> <span data-ttu-id="2260b-118">Bazı eylemler için kullanımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2260b-118">Some uses for actions include:</span></span>

- <span data-ttu-id="2260b-119">Karmaşık işlemler.</span><span class="sxs-lookup"><span data-stu-id="2260b-119">Complex transactions.</span></span>
- <span data-ttu-id="2260b-120">Aynı anda birkaç varlığı düzenleme.</span><span class="sxs-lookup"><span data-stu-id="2260b-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="2260b-121">Yalnızca bir varlığın belirli özelliklerine yönelik güncelleştirmelere izin verme.</span><span class="sxs-lookup"><span data-stu-id="2260b-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="2260b-122">Varlık olmayan verileri gönderme.</span><span class="sxs-lookup"><span data-stu-id="2260b-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="2260b-123">İşlevler, doğrudan bir varlığa veya koleksiyona karşılık gelen bilgileri döndürmek için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="2260b-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="2260b-124">Bir eylem (veya işlev) tek bir varlığı veya koleksiyonu hedefleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2260b-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="2260b-125">OData terminolojisinde bu *bağlamadır*.</span><span class="sxs-lookup"><span data-stu-id="2260b-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="2260b-126">Ayrıca, hizmette statik işlemler olarak çağrılan &quot;ilişkisiz&quot; eylemlere/işlevlere sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2260b-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="2260b-127">Örnek: eylem ekleme</span><span class="sxs-lookup"><span data-stu-id="2260b-127">Example: Adding an Action</span></span>

<span data-ttu-id="2260b-128">Bir ürünü derecelendirmek için bir eylem tanımlayalim.</span><span class="sxs-lookup"><span data-stu-id="2260b-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="2260b-129">Bu öğretici, [ASP.NET Web API 2 kullanarak bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md) öğreticisinde derleme</span><span class="sxs-lookup"><span data-stu-id="2260b-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="2260b-130">İlk olarak, derecelendirmeleri temsil etmek için bir `ProductRating` modeli ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2260b-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="2260b-131">Ayrıca, `ProductsContext` sınıfına bir **Dbset** ekleyin, bu sayede EF veritabanında bir derecelendirme tablosu oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="2260b-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="2260b-132">Eylemi EDM öğesine ekleyin</span><span class="sxs-lookup"><span data-stu-id="2260b-132">Add the Action to the EDM</span></span>

<span data-ttu-id="2260b-133">WebApiConfig.cs içinde aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2260b-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="2260b-134">**EntityTypeConfiguration. Action** yöntemi varlık veri modeli 'NE (EDM) bir eylem ekler.</span><span class="sxs-lookup"><span data-stu-id="2260b-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="2260b-135">**Parameter** yöntemi eylem için türü belirlenmiş bir parametre belirtir.</span><span class="sxs-lookup"><span data-stu-id="2260b-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="2260b-136">Bu kod ayrıca EDM için ad alanını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2260b-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="2260b-137">Eylem için URI tam eylem adını içerdiğinden, ad alanı önemlidir:</span><span class="sxs-lookup"><span data-stu-id="2260b-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="2260b-138">Tipik bir IIS yapılandırmasında, bu URL 'deki nokta IIS 'nin 404 hatasını döndürmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="2260b-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="2260b-139">Bunu, Web. config dosyanıza aşağıdaki bölümü ekleyerek çözebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2260b-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="2260b-140">Eylem için bir denetleyici yöntemi ekleme</span><span class="sxs-lookup"><span data-stu-id="2260b-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="2260b-141">&quot;hız&quot; eylemini etkinleştirmek için aşağıdaki yöntemi `ProductsController`ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2260b-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="2260b-142">Yöntem adının eylem adıyla eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2260b-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="2260b-143">**[HttpPost]** özniteliği, YÖNTEMIN BIR http post yöntemi olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="2260b-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="2260b-144">İstemci, eylemi çağırmak için aşağıdakine benzer bir HTTP POST isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="2260b-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="2260b-145">&quot;ücret&quot; eylemi ürün örneklerine bağlanır, bu nedenle eylem URI 'si varlık URI 'sine eklenen tam eylem adıdır.</span><span class="sxs-lookup"><span data-stu-id="2260b-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="2260b-146">(EDM ad alanını &quot;ProductService&quot;olarak belirlediğimiz için tam olarak nitelenmiş eylem adı &quot;ProductService. Rate&quot;.)</span><span class="sxs-lookup"><span data-stu-id="2260b-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="2260b-147">İsteğin gövdesi bir JSON yükü olarak eylem parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="2260b-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="2260b-148">Web API 'si, JSON yükünü otomatik olarak bir **ODataActionParameters** nesnesine dönüştürür; bu yalnızca parametre değerlerinin bir sözlüğüdür.</span><span class="sxs-lookup"><span data-stu-id="2260b-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="2260b-149">Denetleyici yönteminizin parametrelerine erişmek için bu sözlüğü kullanın.</span><span class="sxs-lookup"><span data-stu-id="2260b-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="2260b-150">İstemci eylem parametrelerini yanlış biçimde gönderirse **ModelState. IsValid** değeri false 'tur.</span><span class="sxs-lookup"><span data-stu-id="2260b-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="2260b-151">Denetleyici yönteminizin bu bayrağını işaretleyin ve **IsValid** yanlış ise bir hata döndürün.</span><span class="sxs-lookup"><span data-stu-id="2260b-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="2260b-152">Örnek: bir Işlev ekleme</span><span class="sxs-lookup"><span data-stu-id="2260b-152">Example: Adding a Function</span></span>

<span data-ttu-id="2260b-153">Şimdi en pahalı ürünü döndüren bir OData işlevi ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="2260b-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="2260b-154">Daha önce olduğu gibi ilk adım, EDM öğesine işlevi ekliyor.</span><span class="sxs-lookup"><span data-stu-id="2260b-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="2260b-155">WebApiConfig.cs içinde aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2260b-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="2260b-156">Bu durumda, işlevi ayrı ürün örnekleri yerine ürünler koleksiyonuna bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2260b-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="2260b-157">İstemciler bir GET isteği göndererek işlevi çağırır:</span><span class="sxs-lookup"><span data-stu-id="2260b-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="2260b-158">Bu işlev için Controller yöntemi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2260b-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="2260b-159">Yöntem adının işlev adıyla eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2260b-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="2260b-160">**[HttpGet]** özniteliği, YÖNTEMIN BIR http get yöntemi olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="2260b-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="2260b-161">HTTP yanıtı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2260b-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="2260b-162">Örnek: Ilişkisiz bir Işlev ekleme</span><span class="sxs-lookup"><span data-stu-id="2260b-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="2260b-163">Önceki örnek bir koleksiyona bağlamıştı.</span><span class="sxs-lookup"><span data-stu-id="2260b-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="2260b-164">Bu sonraki örnekte, *ilişkisiz* bir işlev oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="2260b-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="2260b-165">İlişkisiz işlevler, hizmette statik işlemler olarak çağrılır.</span><span class="sxs-lookup"><span data-stu-id="2260b-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="2260b-166">Bu örnekteki işlev, belirli bir posta kodu için satış vergisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="2260b-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="2260b-167">WebApiConfig dosyasında, EDM öğesine işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2260b-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="2260b-168">**İşlev** , varlık türü veya koleksiyon yerine doğrudan **ODataModelBuilder**üzerinde çağrıldığımızda dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2260b-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="2260b-169">Bu, model Oluşturucu işlevinin ilişkisiz olduğunu söyler.</span><span class="sxs-lookup"><span data-stu-id="2260b-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="2260b-170">İşlevi uygulayan Controller yöntemi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2260b-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="2260b-171">Bu yöntemi hangi Web API denetleyicisine yerleştirdiğinizden bağımsız değildir.</span><span class="sxs-lookup"><span data-stu-id="2260b-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="2260b-172">`ProductsController`yerleştirebilir veya ayrı bir denetleyici tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2260b-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="2260b-173">**[ODataRoute]** ÖZNITELIĞI işlevin URI şablonunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2260b-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="2260b-174">Örnek bir istemci isteği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2260b-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="2260b-175">HTTP yanıtı:</span><span class="sxs-lookup"><span data-stu-id="2260b-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
