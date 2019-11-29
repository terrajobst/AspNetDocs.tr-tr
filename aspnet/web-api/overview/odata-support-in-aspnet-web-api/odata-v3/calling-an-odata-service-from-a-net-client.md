---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: Bir .NET Istemcisinden OData hizmetini çağırma (C#) | Microsoft Docs
author: MikeWasson
description: Bu öğreticide, bir C# istemci uygulamasından bir OData hizmetinin nasıl çağrılacağını gösterilmektedir. Öğretici Visual Studio 2013 kullanılan yazılım sürümleri (Visual S ile birlikte çalışarak...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600374"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="ca383-104">Bir .NET İstemcisinden OData Hizmetine Çağrı Yapma (C#)</span><span class="sxs-lookup"><span data-stu-id="ca383-104">Calling an OData Service From a .NET Client (C#)</span></span>

<span data-ttu-id="ca383-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ca383-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ca383-106">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="ca383-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="ca383-107">Bu öğreticide, bir C# istemci uygulamasından bir OData hizmetinin nasıl çağrılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ca383-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ca383-108">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="ca383-108">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="ca383-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (Visual Studio 2012 ile birlikte geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="ca383-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="ca383-110">WCF Veri Hizmetleri İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="ca383-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/library/cc668772.aspx)
> - <span data-ttu-id="ca383-111">Web API 2.</span><span class="sxs-lookup"><span data-stu-id="ca383-111">Web API 2.</span></span> <span data-ttu-id="ca383-112">(Örnek OData hizmeti Web API 2 kullanılarak oluşturulmuştur, ancak istemci uygulaması Web API 'sine bağımlı değildir.)</span><span class="sxs-lookup"><span data-stu-id="ca383-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>

<span data-ttu-id="ca383-113">Bu öğreticide, OData hizmetini çağıran bir istemci uygulaması oluşturma konusunda adım adım göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca383-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="ca383-114">OData hizmeti aşağıdaki varlıkları kullanıma sunar:</span><span class="sxs-lookup"><span data-stu-id="ca383-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="ca383-115">Aşağıdaki makalelerde, Web API 'de OData hizmetinin nasıl uygulanacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="ca383-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="ca383-116">(Ancak, bu öğreticiyi anlamak için bunları okumanız gerekmez.)</span><span class="sxs-lookup"><span data-stu-id="ca383-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="ca383-117">Web API 2 ' de OData uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca383-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="ca383-118">Web API 2 ' de OData varlık Ilişkileri</span><span class="sxs-lookup"><span data-stu-id="ca383-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="ca383-119">Web API 2’de OData Eylemleri</span><span class="sxs-lookup"><span data-stu-id="ca383-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="ca383-120">Hizmet proxy 'Si oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca383-120">Generate the Service Proxy</span></span>

<span data-ttu-id="ca383-121">İlk adım bir hizmet proxy 'si oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca383-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="ca383-122">Hizmet proxy 'si OData hizmetine erişim yöntemlerini tanımlayan bir .NET sınıfıdır.</span><span class="sxs-lookup"><span data-stu-id="ca383-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="ca383-123">Proxy, Yöntem çağrılarını HTTP isteklerine çevirir.</span><span class="sxs-lookup"><span data-stu-id="ca383-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="ca383-124">Visual Studio 'da OData hizmeti projesini açarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="ca383-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="ca383-125">Hizmeti IIS Express ' de yerel olarak çalıştırmak için CTRL + F5 tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="ca383-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="ca383-126">Yerel adresi, Visual Studio 'Nun atadığı bağlantı noktası numarası dahil olmak üzere unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ca383-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="ca383-127">Proxy 'yi oluştururken bu adrese ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="ca383-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="ca383-128">Ardından, Visual Studio 'nun başka bir örneğini açın ve bir konsol uygulaması projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca383-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="ca383-129">Konsol uygulaması OData istemci uygulamamız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ca383-129">The console application will be our OData client application.</span></span> <span data-ttu-id="ca383-130">(Ayrıca, projeyi hizmetle aynı çözüme da ekleyebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="ca383-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="ca383-131">Kalan adımlar konsol projesine başvurur.</span><span class="sxs-lookup"><span data-stu-id="ca383-131">The remaining steps refer the console project.</span></span>

<span data-ttu-id="ca383-132">Çözüm Gezgini, **Başvurular** ' a sağ tıklayın ve **hizmet başvurusu Ekle**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ca383-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="ca383-133">**Hizmet başvurusu Ekle** iletişim kutusunda, OData hizmetinin adresini yazın:</span><span class="sxs-lookup"><span data-stu-id="ca383-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="ca383-134">Burada *bağlantı* noktası numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="ca383-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="ca383-135">**Ad alanı**Için "ProductService" yazın.</span><span class="sxs-lookup"><span data-stu-id="ca383-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="ca383-136">Bu seçenek, proxy sınıfının ad alanını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca383-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="ca383-137">**Git**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca383-137">Click **Go**.</span></span> <span data-ttu-id="ca383-138">Visual Studio, hizmette varlıkları saptamak için OData meta veri belgesini okur.</span><span class="sxs-lookup"><span data-stu-id="ca383-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="ca383-139">Projeniz için proxy sınıfını eklemek üzere **Tamam** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca383-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="ca383-140">Hizmet proxy sınıfının bir örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca383-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="ca383-141">`Main` yönteminizin içinde, proxy sınıfının yeni bir örneğini aşağıdaki gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ca383-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="ca383-142">Yine, hizmetinizin çalıştığı gerçek bağlantı noktası numarasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="ca383-143">Hizmetinizi dağıttığınızda, canlı hizmetin URI 'sini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ca383-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="ca383-144">Proxy 'yi güncelleştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ca383-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="ca383-145">Aşağıdaki kod, istek URI 'Lerini konsol penceresine yazdıran bir olay işleyicisi ekler.</span><span class="sxs-lookup"><span data-stu-id="ca383-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="ca383-146">Bu adım gerekli değildir, ancak her sorgu için URI 'Leri görmek ilginç olur.</span><span class="sxs-lookup"><span data-stu-id="ca383-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="ca383-147">Hizmeti sorgulama</span><span class="sxs-lookup"><span data-stu-id="ca383-147">Query the Service</span></span>

<span data-ttu-id="ca383-148">Aşağıdaki kod, OData hizmetinden ürünlerin listesini alır.</span><span class="sxs-lookup"><span data-stu-id="ca383-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="ca383-149">HTTP isteğini göndermek veya yanıtı ayrıştırmak için herhangi bir kod yazmanıza gerek olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ca383-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="ca383-150">**Foreach** döngüsünde `Container.Products` koleksiyonunu Numaralandırdığınızda proxy sınıfı bunu otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="ca383-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="ca383-151">Uygulamayı çalıştırdığınızda, çıkış aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ca383-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="ca383-152">KIMLIĞE göre bir varlık almak için bir `where` yan tümcesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="ca383-153">Bu konunun geri kalanında, yalnızca hizmeti çağırmak için gereken kod olan `Main` işlevinin tamamını göstermiyorum.</span><span class="sxs-lookup"><span data-stu-id="ca383-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="ca383-154">Sorgu seçeneklerini Uygula</span><span class="sxs-lookup"><span data-stu-id="ca383-154">Apply Query Options</span></span>

<span data-ttu-id="ca383-155">OData filtrelemeye, sıralamaya, sayfa verilerine ve benzeri şekilde kullanılabilecek [sorgu seçeneklerini](../supporting-odata-query-options.md) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca383-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="ca383-156">Hizmet proxy 'sinde, çeşitli LINQ ifadelerini kullanarak bu seçenekleri uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca383-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="ca383-157">Bu bölümde kısa örnekler göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca383-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="ca383-158">Daha fazla ayrıntı için MSDN 'de [LINQ hususları (WCF veri Hizmetleri)](https://msdn.microsoft.com/library/ee622463.aspx) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="ca383-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="ca383-159">Filtreleme ($filter)</span><span class="sxs-lookup"><span data-stu-id="ca383-159">Filtering ($filter)</span></span>

<span data-ttu-id="ca383-160">Filtrelemek için bir `where` yan tümcesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="ca383-161">Aşağıdaki örnek ürün kategorisine göre filtreliyor.</span><span class="sxs-lookup"><span data-stu-id="ca383-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="ca383-162">Bu kod, aşağıdaki OData sorgusuna karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="ca383-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="ca383-163">Proxy 'nin `where` yan tümcesini OData `$filter` ifadesine dönüştürtiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ca383-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="ca383-164">Sıralama ($orderby)</span><span class="sxs-lookup"><span data-stu-id="ca383-164">Sorting ($orderby)</span></span>

<span data-ttu-id="ca383-165">Sıralamak için bir `orderby` yan tümcesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="ca383-166">Aşağıdaki örnek fiyata göre, en yüksekten en düşüğe göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="ca383-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="ca383-167">Buna karşılık gelen OData isteği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ca383-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="ca383-168">İstemci tarafı sayfalama ($skip ve $top)</span><span class="sxs-lookup"><span data-stu-id="ca383-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="ca383-169">Büyük varlık kümelerinde istemci, sonuçların sayısını sınırlamak isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="ca383-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="ca383-170">Örneğin, bir istemci tek seferde 10 girdi gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="ca383-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="ca383-171">Bu, *istemci tarafı sayfalama*olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="ca383-171">This is called *client-side paging*.</span></span> <span data-ttu-id="ca383-172">(Sunucunun sonuç sayısını sınırlayan [sunucu tarafı sayfalama](../supporting-odata-query-options.md#server-paging)da vardır.) İstemci tarafı sayfalama gerçekleştirmek için LINQ **Skip** ve **Al** yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="ca383-173">Aşağıdaki örnek ilk 40 sonucunu atlar ve sonraki 10 ' un sürer.</span><span class="sxs-lookup"><span data-stu-id="ca383-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="ca383-174">Buna karşılık gelen OData isteği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ca383-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="ca383-175">Seç ($select) ve genişlet ($expand)</span><span class="sxs-lookup"><span data-stu-id="ca383-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="ca383-176">İlgili varlıkları eklemek için `DataServiceQuery<t>.Expand` yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="ca383-177">Örneğin, her bir `Product`için `Supplier` eklemek için:</span><span class="sxs-lookup"><span data-stu-id="ca383-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="ca383-178">Buna karşılık gelen OData isteği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ca383-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="ca383-179">Yanıtın şeklini değiştirmek için LINQ **Select** yan tümcesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="ca383-180">Aşağıdaki örnek, başka hiçbir özellik olmadan yalnızca her bir ürünün adını alır.</span><span class="sxs-lookup"><span data-stu-id="ca383-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="ca383-181">Buna karşılık gelen OData isteği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ca383-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="ca383-182">Bir SELECT yan tümcesi, ilgili varlıkları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ca383-182">A select clause can include related entities.</span></span> <span data-ttu-id="ca383-183">Bu durumda, **Expand**çağırmayın; Bu durumda ara sunucu genişletmeyi otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="ca383-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="ca383-184">Aşağıdaki örnek, her bir ürünün adını ve tedarikçiyi alır.</span><span class="sxs-lookup"><span data-stu-id="ca383-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="ca383-185">Buna karşılık gelen OData isteği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ca383-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="ca383-186">**$Expand** seçeneğini içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ca383-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="ca383-187">$Select ve $expand hakkında daha fazla bilgi için bkz. [Web API 2 ' de $SELECT, $expand ve $value kullanma](../using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="ca383-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="ca383-188">Yeni varlık Ekle</span><span class="sxs-lookup"><span data-stu-id="ca383-188">Add a New Entity</span></span>

<span data-ttu-id="ca383-189">Bir varlık kümesine yeni bir varlık eklemek için, *EntitySet* 'in varlık kümesinin adı olduğu `AddToEntitySet`çağırın.</span><span class="sxs-lookup"><span data-stu-id="ca383-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="ca383-190">Örneğin, `AddToProducts` `Products` varlık kümesine yeni bir `Product` ekler.</span><span class="sxs-lookup"><span data-stu-id="ca383-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="ca383-191">Proxy oluşturduğunuzda WCF Veri Hizmetleri, bu kesin türü belirtilmiş **AddTo** yöntemlerini otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ca383-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="ca383-192">İki varlık arasında bir bağlantı eklemek için **AddLink** ve **SetLink** yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="ca383-193">Aşağıdaki kod yeni bir tedarikçi ve yeni bir ürün ekler ve bunlar arasında bağlantılar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ca383-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="ca383-194">Gezinti özelliği bir koleksiyon olduğunda **AddLink** kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="ca383-195">Bu örnekte, tedarikçide `Products` koleksiyonuna bir ürün ekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="ca383-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="ca383-196">Gezinti özelliği tek bir varlık olduğunda **SetLink** kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca383-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="ca383-197">Bu örnekte, üründe `Supplier` özelliğini ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="ca383-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="ca383-198">Güncelleştirme/düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="ca383-198">Update / Patch</span></span>

<span data-ttu-id="ca383-199">Bir varlığı güncelleştirmek için **UpdateObject** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ca383-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="ca383-200">**SaveChanges**öğesini çağırdığınızda güncelleştirme gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca383-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="ca383-201">Varsayılan olarak, WCF bir HTTP BIRLEŞTIRME isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="ca383-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="ca383-202">**Patchonupdate** SEÇENEĞI, WCF 'ye bunun yerıne BIR http Patch göndermesini söyler.</span><span class="sxs-lookup"><span data-stu-id="ca383-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="ca383-203">Düzeltme Eki neden BIRLEŞMELIDIR?</span><span class="sxs-lookup"><span data-stu-id="ca383-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="ca383-204">Özgün HTTP 1,1 belirtimi ([RCF 2616](http://tools.ietf.org/html/rfc2616)), "Kısmi güncelleştirme" semantiğine sahip HERHANGI bir http yöntemi tanımlamıyor.</span><span class="sxs-lookup"><span data-stu-id="ca383-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="ca383-205">Kısmi güncelleştirmeleri desteklemek için, OData belirtimi MERGE metodunu tanımladı.</span><span class="sxs-lookup"><span data-stu-id="ca383-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="ca383-206">2010 ' de, [RFC 5789](http://tools.ietf.org/html/rfc5789) kısmi GÜNCELLEŞTIRMELER için Patch metodunu tanımladı.</span><span class="sxs-lookup"><span data-stu-id="ca383-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="ca383-207">Bu [blog gönderisine](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) ait geçmişin WCF veri Hizmetleri blogundan bazılarını okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca383-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="ca383-208">Bugün, düzeltme eki BIRLEŞTIRME üzerinden tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="ca383-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="ca383-209">Web API 'SI yapı iskelesi tarafından oluşturulan OData denetleyicisi her iki yöntemi de destekler.</span><span class="sxs-lookup"><span data-stu-id="ca383-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>

<span data-ttu-id="ca383-210">Tüm varlığı (PUT semantiğini) değiştirmek istiyorsanız, **Replaceonupdate** seçeneğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="ca383-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="ca383-211">Bu, WCF 'nin bir HTTP PUT isteği göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca383-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="ca383-212">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="ca383-212">Delete an Entity</span></span>

<span data-ttu-id="ca383-213">Bir varlığı silmek için **DeleteObject**çağırın.</span><span class="sxs-lookup"><span data-stu-id="ca383-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="ca383-214">OData eylemini çağırma</span><span class="sxs-lookup"><span data-stu-id="ca383-214">Invoke an OData Action</span></span>

<span data-ttu-id="ca383-215">OData 'de, [Eylemler](odata-actions.md) , varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="ca383-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="ca383-216">OData meta veri belgesinde eylemler açıklanmakta olsa da, proxy sınıfı kendileri için kesin tür belirtilmiş Yöntemler oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="ca383-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="ca383-217">Genel **Execute** metodunu kullanarak yine de bir OData eylemi çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca383-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="ca383-218">Ancak, parametrelerin ve dönüş değerinin veri türlerini bilmeniz gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="ca383-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="ca383-219">Örneğin, `RateProduct` eylemi `Int32` türü "derecelendirme" adlı parametreyi alır ve bir `double`döndürür.</span><span class="sxs-lookup"><span data-stu-id="ca383-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="ca383-220">Aşağıdaki kod, bu eylemin nasıl çağıralınacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca383-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="ca383-221">Daha fazla bilgi için bkz.[hizmet işlemlerini ve eylemleri çağırma](https://msdn.microsoft.com/library/hh230677.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca383-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/library/hh230677.aspx).</span></span>

<span data-ttu-id="ca383-222">Bir seçenek, kapsayıcıyı çağıran türü kesin belirlenmiş bir yöntem sağlamak için **kapsayıcı** sınıfını genişletmenin bir seçenektir:</span><span class="sxs-lookup"><span data-stu-id="ca383-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
