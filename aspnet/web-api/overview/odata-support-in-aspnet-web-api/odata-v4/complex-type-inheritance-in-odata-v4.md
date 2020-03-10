---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: OData v4 'de ASP.NET Web API 'SI ile karmaşık tür devralma | Microsoft Docs
author: microsoft
description: OData v4 belirtimine göre, karmaşık bir tür başka bir karmaşık türden devralınabilir. (Karmaşık tür, anahtar içermeyen yapılandırılmış bir türdür.) Web API 'SI...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556310"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="038a3-104">OData v4 'de ASP.NET Web API 'SI ile karmaşık tür devralma</span><span class="sxs-lookup"><span data-stu-id="038a3-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="038a3-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="038a3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="038a3-106">OData v4 [belirtimine](http://www.odata.org/documentation/odata-version-4-0/)göre, karmaşık bir tür başka bir karmaşık türden devralınabilir.</span><span class="sxs-lookup"><span data-stu-id="038a3-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="038a3-107">( *Karmaşık* tür, anahtar içermeyen yapılandırılmış bir türdür.) Web API OData 5,3 karmaşık tür devralmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="038a3-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="038a3-108">Bu konu, karmaşık devralma türleri ile bir varlık veri modeli (EDM) oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="038a3-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="038a3-109">Tüm kaynak kodu için bkz. [OData karmaşık türü devralma örneği](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="038a3-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="038a3-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="038a3-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="038a3-111">Web API OData 5,3</span><span class="sxs-lookup"><span data-stu-id="038a3-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="038a3-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="038a3-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="038a3-113">Model hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="038a3-113">Model Hierarchy</span></span>

<span data-ttu-id="038a3-114">Karmaşık tür devralmayı göstermek için aşağıdaki sınıf hiyerarşisini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="038a3-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="038a3-115">`Shape` soyut bir karmaşık türdür.</span><span class="sxs-lookup"><span data-stu-id="038a3-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="038a3-116">`Rectangle`, `Triangle`ve `Circle` `Shape`türetilmiş karmaşık türlerdir ve `RoundRectangle` `Rectangle`türetilir.</span><span class="sxs-lookup"><span data-stu-id="038a3-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="038a3-117">`Window` bir varlık türüdür ve bir `Shape` örneği içerir.</span><span class="sxs-lookup"><span data-stu-id="038a3-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="038a3-118">Bu türleri tanımlayan CLR sınıfları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="038a3-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="038a3-119">EDM modelini oluşturma</span><span class="sxs-lookup"><span data-stu-id="038a3-119">Build the EDM Model</span></span>

<span data-ttu-id="038a3-120">EDM 'yi oluşturmak için, CLR türlerindeki devralma ilişkilerini gösteren **ODataConventionModelBuilder**kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="038a3-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="038a3-121">Ayrıca, **ODataModelBuilder**kullanarak EDM 'yi açıkça de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="038a3-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="038a3-122">Bu daha fazla kod alır, ancak EDM üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="038a3-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="038a3-123">Bu iki örnek aynı EDM şemasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="038a3-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="038a3-124">Meta veri belgesi</span><span class="sxs-lookup"><span data-stu-id="038a3-124">Metadata Document</span></span>

<span data-ttu-id="038a3-125">Karmaşık tür devralmayı gösteren OData meta veri belgesi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="038a3-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="038a3-126">Meta veri belgesinden şunları görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="038a3-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="038a3-127">`Shape` karmaşık tür soyuttur.</span><span class="sxs-lookup"><span data-stu-id="038a3-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="038a3-128">`Rectangle`, `Triangle`ve `Circle` karmaşık türün temel türü `Shape`vardır.</span><span class="sxs-lookup"><span data-stu-id="038a3-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="038a3-129">`RoundRectangle` türünün temel türü `Rectangle`vardır.</span><span class="sxs-lookup"><span data-stu-id="038a3-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="038a3-130">Karmaşık türleri atama</span><span class="sxs-lookup"><span data-stu-id="038a3-130">Casting Complex Types</span></span>

<span data-ttu-id="038a3-131">Karmaşık türlerde atama artık desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="038a3-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="038a3-132">Örneğin, aşağıdaki sorgu bir `Shape` `Rectangle`yayınlar.</span><span class="sxs-lookup"><span data-stu-id="038a3-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="038a3-133">Yanıt yükü şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="038a3-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
