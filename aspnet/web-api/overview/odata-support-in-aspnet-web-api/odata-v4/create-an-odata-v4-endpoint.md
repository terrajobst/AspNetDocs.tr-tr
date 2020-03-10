---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2,2 kullanarak OData v4 uç noktası oluşturma | Microsoft Docs
author: MikeWasson
description: Açık Veri Protokolü (OData) Web için bir veri erişim protokolüdür. OData, CRUD işlemleri aracılığıyla veri kümelerini sorgulamak ve işlemek için Tekdüzen bir yol sağlar...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598737"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="e4a5f-104">ASP.NET Web API 'SI kullanarak OData v4 uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4a5f-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="e4a5f-105">Açık Veri Protokolü (OData) Web için bir veri erişim protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="e4a5f-106">OData, CRUD işlemleri (oluşturma, okuma, güncelleştirme ve silme) aracılığıyla veri kümelerini sorgulamak ve işlemek için Tekdüzen bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="e4a5f-107">ASP.NET Web API 'SI hem v3 hem de v4 protokolünü destekler.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="e4a5f-108">V3 uç noktasıyla yan yana çalışan bir v4 uç noktasına bile sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="e4a5f-109">Bu öğreticide, CRUD işlemlerini destekleyen bir OData v4 uç noktası oluşturma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e4a5f-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="e4a5f-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="e4a5f-111">Web API 5,2</span><span class="sxs-lookup"><span data-stu-id="e4a5f-111">Web API 5.2</span></span>
> - <span data-ttu-id="e4a5f-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="e4a5f-112">OData v4</span></span>
> - <span data-ttu-id="e4a5f-113">Visual Studio 2017 (Visual Studio 2017 [buraya](https://visualstudio.microsoft.com/downloads/)indirin)</span><span class="sxs-lookup"><span data-stu-id="e4a5f-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="e4a5f-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="e4a5f-114">Entity Framework 6</span></span>
> - <span data-ttu-id="e4a5f-115">.NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="e4a5f-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="e4a5f-116">Öğretici sürümleri</span><span class="sxs-lookup"><span data-stu-id="e4a5f-116">Tutorial versions</span></span>
>
> <span data-ttu-id="e4a5f-117">OData sürüm 3 için bkz. [OData v3 uç noktası oluşturma](../odata-v3/creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="e4a5f-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="e4a5f-118">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4a5f-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="e4a5f-119">Visual Studio 'da, **Dosya** menüsünden **Yeni** &gt; **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="e4a5f-120">**Yüklü** &gt;  **C# Visual** &gt; **Web**' i genişletin ve **ASP.NET Web uygulaması (.NET Framework)** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="e4a5f-121">Projeyi &quot;ProductService&quot;olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="e4a5f-122">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-122">Select **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="e4a5f-123">**Boş** şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-123">Select the **Empty** template.</span></span> <span data-ttu-id="e4a5f-124">**İçin klasör ve çekirdek başvuruları Ekle**altında **Web API 'si**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="e4a5f-125">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="e4a5f-126">OData paketlerini yükler</span><span class="sxs-lookup"><span data-stu-id="e4a5f-126">Install the OData packages</span></span>

<span data-ttu-id="e4a5f-127">**Araçlar** menüsünde **NuGet Paket Yöneticisi** &gt; **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="e4a5f-128">Paket Yöneticisi konsol penceresinde, şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e4a5f-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="e4a5f-129">Bu komut en son OData NuGet paketlerini yükleme.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="e4a5f-130">Bir model sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="e4a5f-130">Add a model class</span></span>

<span data-ttu-id="e4a5f-131">*Model* , uygulamanızdaki bir veri varlığını temsil eden bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="e4a5f-132">Çözüm Gezgini modeller klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="e4a5f-133">Bağlam menüsünden &gt; **sınıfı** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="e4a5f-134">Kurala göre, model sınıfları modeller klasörüne yerleştirilir, ancak bu kuralı kendi projelerinizde izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>

<span data-ttu-id="e4a5f-135">`Product`sınıfı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-135">Name the class `Product`.</span></span> <span data-ttu-id="e4a5f-136">Product.cs dosyasında, demirbaş kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e4a5f-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="e4a5f-137">`Id` özelliği varlık anahtarıdır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="e4a5f-138">İstemciler, varlıkları anahtara göre sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-138">Clients can query entities by key.</span></span> <span data-ttu-id="e4a5f-139">Örneğin, KIMLIĞI 5 olan ürünü almak için URI `/Products(5)`.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="e4a5f-140">`Id` özelliği, arka uç veritabanında da birincil anahtar olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="e4a5f-141">Entity Framework etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e4a5f-141">Enable Entity Framework</span></span>

<span data-ttu-id="e4a5f-142">Bu öğreticide, arka uç veritabanını oluşturmak için Entity Framework (EF) Code First kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="e4a5f-143">Web API OData, EF gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-143">Web API OData does not require EF.</span></span> <span data-ttu-id="e4a5f-144">Veritabanı varlıklarını modellerle çevirebilirler herhangi bir veri erişim katmanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-144">Use any data-access layer that can translate database entities into models.</span></span>

<span data-ttu-id="e4a5f-145">İlk olarak, EF için NuGet paketini yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="e4a5f-146">**Araçlar** menüsünde **NuGet Paket Yöneticisi** &gt; **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="e4a5f-147">Paket Yöneticisi konsol penceresinde, şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e4a5f-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="e4a5f-148">Web. config dosyasını açın ve aşağıdaki bölümü, **configSections** öğesinden sonra **yapılandırma** öğesinin içine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="e4a5f-149">Bu ayar, LocalDB veritabanı için bir bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="e4a5f-150">Bu veritabanı, uygulamayı yerel olarak çalıştırdığınızda kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="e4a5f-151">Ardından modeller klasörüne `ProductsContext` adlı bir sınıf ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e4a5f-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="e4a5f-152">Oluşturucuda, `"name=ProductsContext"` bağlantı dizesinin adını verir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="e4a5f-153">OData uç noktasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e4a5f-153">Configure the OData endpoint</span></span>

<span data-ttu-id="e4a5f-154">Start/WebApiConfig. cs\_dosya uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="e4a5f-155">Aşağıdaki **using** deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e4a5f-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="e4a5f-156">Ardından **register** yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e4a5f-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="e4a5f-157">Bu kod iki şeyi yapar:</span><span class="sxs-lookup"><span data-stu-id="e4a5f-157">This code does two things:</span></span>

- <span data-ttu-id="e4a5f-158">Bir Varlık Veri Modeli (EDM) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="e4a5f-159">Bir yol ekler.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-159">Adds a route.</span></span>

<span data-ttu-id="e4a5f-160">EDM, verilerin soyut bir modelidir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="e4a5f-161">EDM, hizmet meta verileri belgesi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="e4a5f-162">**ODataConventionModelBuilder** sınıfı varsayılan adlandırma kurallarını kullanarak bir EDM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="e4a5f-163">Bu yaklaşım için en az kod gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-163">This approach requires the least code.</span></span> <span data-ttu-id="e4a5f-164">EDM üzerinde daha fazla denetim istiyorsanız, özellik, anahtar ve gezinti özelliklerini açıkça ekleyerek EDM oluşturmak için **ODataModelBuilder** sınıfını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="e4a5f-165">Bir *yol* , Web API 'sine http isteklerini uç noktaya nasıl yönlendirildiğini söyler.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="e4a5f-166">OData v4 yolu oluşturmak için, **MapODataServiceRoute** genişletme yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="e4a5f-167">Uygulamanızda birden çok OData uç noktası varsa, her biri için ayrı bir yol oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="e4a5f-168">Her rotaya benzersiz bir yol adı ve ön ek verin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="e4a5f-169">OData denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="e4a5f-169">Add the OData controller</span></span>

<span data-ttu-id="e4a5f-170">*Denetleyici* , http isteklerini işleyen bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="e4a5f-171">OData hizmetinizde her bir varlık kümesi için ayrı bir denetleyici oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="e4a5f-172">Bu öğreticide, `Product` varlığı için bir denetleyici oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="e4a5f-173">Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın ve &gt; **sınıfı** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="e4a5f-174">`ProductsController`sınıfı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="e4a5f-175">OData v3 için Bu öğreticinin sürümü, **denetleyiciyi Ekle** yapı iskelesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="e4a5f-176">Şu anda OData v4 için bir yapı iskelesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-176">Currently, there is no scaffolding for OData v4.</span></span>

<span data-ttu-id="e4a5f-177">ProductsController.cs içindeki ortak kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="e4a5f-178">Denetleyici, EF kullanarak veritabanına erişmek için `ProductsContext` sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="e4a5f-179">Denetleyicinin **Productscontext**'i atmak için **Dispose** metodunu geçersiz kıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="e4a5f-180">Bu, denetleyicinin başlangıç noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-180">This is the starting point for the controller.</span></span> <span data-ttu-id="e4a5f-181">Ardından, tüm CRUD işlemleri için yöntemler ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="e4a5f-182">Varlık kümesini sorgulama</span><span class="sxs-lookup"><span data-stu-id="e4a5f-182">Query the entity set</span></span>

<span data-ttu-id="e4a5f-183">`ProductsController`için aşağıdaki yöntemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="e4a5f-184">`Get` yönteminin parametresiz sürümü tüm ürünler koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="e4a5f-185">*Anahtar* parametresine sahip `Get` yöntemi bir ürünü anahtarıyla arar (Bu durumda, `Id` özelliği).</span><span class="sxs-lookup"><span data-stu-id="e4a5f-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="e4a5f-186">**[Enablequery]** özniteliği, istemcilerin $filter, $sort ve $Page gibi sorgu seçeneklerini kullanarak sorguyu değiştirmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="e4a5f-187">Daha fazla bilgi için bkz. [OData sorgu seçeneklerini destekleme](../supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="e4a5f-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="e4a5f-188">Varlık kümesine varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="e4a5f-188">Add an entity to the entity set</span></span>

<span data-ttu-id="e4a5f-189">İstemcilerin veritabanına yeni bir ürün eklemesini sağlamak için aşağıdaki yöntemi `ProductsController`ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="e4a5f-190">Varlığı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e4a5f-190">Update an entity</span></span>

<span data-ttu-id="e4a5f-191">OData, bir varlığı güncelleştirmek için iki farklı semantiğini destekler, yama ve PUT.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="e4a5f-192">Düzeltme Eki kısmi bir güncelleştirme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-192">PATCH performs a partial update.</span></span> <span data-ttu-id="e4a5f-193">İstemci yalnızca güncelleştirilecek özellikleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="e4a5f-194">PUT, tüm varlığın yerini alır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="e4a5f-195">PUT 'in dezavantajı, istemcinin, değişmeyen değerler de dahil olmak üzere varlıktaki tüm özelliklerin değerlerini gönderebilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="e4a5f-196">[OData özelliği](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) , düzeltme ekinin tercih edildiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="e4a5f-197">Her durumda, hem düzeltme eki hem de PUT yöntemlerinin kodu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e4a5f-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="e4a5f-198">Düzeltme durumunda, denetleyici değişiklikleri izlemek için **Delta&lt;t&gt;** türünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="e4a5f-199">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="e4a5f-199">Delete an entity</span></span>

<span data-ttu-id="e4a5f-200">İstemcilerin bir ürünü veritabanından silmesini sağlamak için aşağıdaki yöntemi `ProductsController`ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e4a5f-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
