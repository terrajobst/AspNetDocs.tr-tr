---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Web API 2,2 kullanarak tek bir OData v4 oluşturma | Microsoft Docs
author: rick-anderson
description: Bu konu başlığı altında, Web API 2,2 ' de bir OData uç noktasında tek bir tekil nasıl tanımlanacağı gösterilmektedir.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622089"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="737d5-103">Web API 2,2 kullanarak tek bir OData v4 oluşturma</span><span class="sxs-lookup"><span data-stu-id="737d5-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="737d5-104">Zoe Luo tarafından</span><span class="sxs-lookup"><span data-stu-id="737d5-104">by Zoe Luo</span></span>

> <span data-ttu-id="737d5-105">Geleneksel olarak, bir varlığa yalnızca bir varlık kümesi içinde kapsülleniyorsa erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="737d5-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="737d5-106">Ancak OData v4, her ikisi de hem WebAPI 2,2 ' nin desteklediği iki ek seçenek sunar.</span><span class="sxs-lookup"><span data-stu-id="737d5-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="737d5-107">Bu makalede, Web API 2,2 ' de bir OData uç noktasında tekil nasıl tanımlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="737d5-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="737d5-108">Tekil nedir ve bunu kullanmanın avantajlarından faydalanmanız hakkında bilgi edinmek için, bkz. [özel varlığınızı tanımlamak için tek tek kullanma](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span><span class="sxs-lookup"><span data-stu-id="737d5-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="737d5-109">Web API 'de OData v4 uç noktası oluşturmak için, bkz. [ASP.NET Web apı 2,2 kullanarak OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="737d5-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="737d5-110">Aşağıdaki veri modelini kullanarak Web API projenizde tek bir oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="737d5-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![Veri Modeli](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="737d5-112">Tek bir adlandırılmış `Umbrella` `Company`türüne göre tanımlanır ve `Employees` adlı bir varlık kümesi `Employee`türüne göre tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="737d5-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="737d5-113">Bu öğreticide kullanılan çözüm [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)'ten indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="737d5-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="737d5-114">Veri modelini tanımlama</span><span class="sxs-lookup"><span data-stu-id="737d5-114">Define the data model</span></span>

1. <span data-ttu-id="737d5-115">CLR türlerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="737d5-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="737d5-116">CLR türlerini temel alan EDM modelini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="737d5-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="737d5-117">Burada `builder.Singleton<Company>("Umbrella")`, model oluşturucunun EDM modelinde tek bir adlandırılmış `Umbrella` oluşturmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="737d5-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="737d5-118">Oluşturulan meta veriler aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="737d5-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="737d5-119">Meta verilerden, `Employees` varlık kümesindeki Gezinti özelliğinin `Company` Singleton `Umbrella`bağlandığını görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="737d5-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="737d5-120">Yalnızca `Umbrella` `Company` türüne sahip olduğundan bağlama `ODataConventionModelBuilder`tarafından otomatik olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="737d5-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="737d5-121">Modelde belirsizlik varsa, bir gezinti özelliğini açıkça tek bir şekilde bağlamak için `HasSingletonBinding` kullanabilirsiniz. `HasSingletonBinding`, CLR tür tanımında `Singleton` özniteliği ile aynı etkiye sahiptir:</span><span class="sxs-lookup"><span data-stu-id="737d5-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="737d5-122">Tek denetleyiciyi tanımlama</span><span class="sxs-lookup"><span data-stu-id="737d5-122">Define the singleton controller</span></span>

<span data-ttu-id="737d5-123">EntitySet denetleyicisi gibi, tek denetleyici `ODataController`devralır ve tek denetleyici adı `[singletonName]Controller`olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="737d5-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="737d5-124">Farklı istek türlerini işlemek için, denetleyicide önceden tanımlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="737d5-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="737d5-125">Varsayılan olarak, WebApi 2,2 ' de **öznitelik yönlendirme** etkindir.</span><span class="sxs-lookup"><span data-stu-id="737d5-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="737d5-126">Örneğin, öznitelik yönlendirme kullanarak `Company` `Revenue` sorgulamayı işlemeye yönelik bir eylem tanımlamak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="737d5-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="737d5-127">Her bir eylem için öznitelikleri tanımlamanızı istemiyorsanız, yalnızca, [OData yönlendirme kurallarını](../odata-routing-conventions.md)izleyen eylemlerinizi tanımlamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="737d5-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="737d5-128">Tek bir sorgulama için anahtar gerekli olmadığından, tek denetleyicide tanımlanan eylemler, EntitySet denetleyicisinde tanımlanan eylemlerden biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="737d5-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="737d5-129">Başvuru için, tek denetleyicideki her eylem tanımı için yöntem imzaları aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="737d5-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="737d5-130">Temel olarak, hizmet tarafında yapmanız gereken tek şey budur.</span><span class="sxs-lookup"><span data-stu-id="737d5-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="737d5-131">[Örnek proje](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) , çözümün ve tek tek 'nın nasıl kullanılacağını gösteren OData istemcisinin tüm kodlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="737d5-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="737d5-132">İstemci, [OData v4 Istemci uygulaması oluşturma](create-an-odata-v4-client-app.md)bölümündeki adımları izleyerek oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="737d5-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="737d5-133">arasında yetersiz alanla karşılaştı.</span><span class="sxs-lookup"><span data-stu-id="737d5-133">.</span></span> 

<span data-ttu-id="737d5-134">*Bu makalenin özgün içeriği için yem hu için teşekkürler.*</span><span class="sxs-lookup"><span data-stu-id="737d5-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
