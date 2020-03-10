---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Web API 2,2 kullanarak OData v4 'da kapsama | Microsoft Docs
author: rick-anderson
description: Geleneksel olarak, bir varlığa yalnızca bir varlık kümesi içinde kapsülleniyorsa erişilebilir. Ancak OData v4 iki ek seçenek sunar, tek ve Con...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 50050e40c4c42bf6d769d077c27864ee6417d4db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525125"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="81ecf-104">Web API 2,2 kullanarak OData v4 'de kapsama</span><span class="sxs-lookup"><span data-stu-id="81ecf-104">Containment in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="81ecf-105">Jinfu tan tarafından</span><span class="sxs-lookup"><span data-stu-id="81ecf-105">by Jinfu Tan</span></span>

> <span data-ttu-id="81ecf-106">Geleneksel olarak, bir varlığa yalnızca bir varlık kümesi içinde kapsülleniyorsa erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="81ecf-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="81ecf-107">Ancak OData v4, her ikisi de hem WebAPI 2,2 ' nin desteklediği iki ek seçenek sunar.</span><span class="sxs-lookup"><span data-stu-id="81ecf-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="81ecf-108">Bu konuda, WebApi 2,2 ' de OData uç noktasında bir kapsama nasıl tanımlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="81ecf-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="81ecf-109">Kapsama hakkında daha fazla bilgi için bkz. [içerme, OData v4 ile geliyor](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span><span class="sxs-lookup"><span data-stu-id="81ecf-109">For more information about containment, see [Containment is coming with OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span></span> <span data-ttu-id="81ecf-110">Web API 'de OData v4 uç noktası oluşturmak için, bkz. [ASP.NET Web apı 2,2 kullanarak OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="81ecf-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="81ecf-111">İlk olarak, bu veri modelini kullanarak OData hizmetinde bir kapsama alanı modeli oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="81ecf-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![Veri modeli](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="81ecf-113">Hesap birçok Paymentınstruments (PI) içerir, ancak bir PI için bir varlık kümesi tanımlamadık.</span><span class="sxs-lookup"><span data-stu-id="81ecf-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="81ecf-114">Bunun yerine, PSIS 'ye yalnızca bir hesap üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="81ecf-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="81ecf-115">Bu konu başlığında kullanılan çözümü [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)adresinden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ecf-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="81ecf-116">Veri modeli tanımlama</span><span class="sxs-lookup"><span data-stu-id="81ecf-116">Defining the data model</span></span>

1. <span data-ttu-id="81ecf-117">CLR türlerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="81ecf-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="81ecf-118">`Contained` özniteliği, içerme gezintisi özellikleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="81ecf-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="81ecf-119">CLR türlerini temel alan EDM modelini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81ecf-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="81ecf-120">`ODataConventionModelBuilder`, `Contained` özniteliği ilgili gezinti özelliğine eklenirse, EDM modelinin oluşturulmasını işleymeyecektir.</span><span class="sxs-lookup"><span data-stu-id="81ecf-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="81ecf-121">Özellik bir koleksiyon türü ise, bir `GetCount(string NameContains)` işlevi de oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="81ecf-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="81ecf-122">Oluşturulan meta veriler aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="81ecf-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="81ecf-123">`ContainsTarget` özniteliği, Gezinti özelliğinin bir içerme olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="81ecf-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="81ecf-124">İçerilen varlık kümesi denetleyicisini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="81ecf-124">Define the containing entity set controller</span></span>

<span data-ttu-id="81ecf-125">Kapsanan varlıkların kendi denetleyicisi yok; eylem, kapsayan varlık kümesi denetleyicisinde tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="81ecf-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="81ecf-126">Bu örnekte, bir AccountsController vardır ancak Paymentınstrumentscontroller yoktur.</span><span class="sxs-lookup"><span data-stu-id="81ecf-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="81ecf-127">OData yolu 4 veya daha fazla kesimdeyse, yukarıdaki denetleyicideki `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` gibi yalnızca öznitelik yönlendirme işe yarar.</span><span class="sxs-lookup"><span data-stu-id="81ecf-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="81ecf-128">Aksi halde, hem öznitelik hem de geleneksel yönlendirme işe yarar: Örneğin, `GetPayInPIs(int key)` eşleşir `GET ~/Accounts(1)/PayinPIs`.</span><span class="sxs-lookup"><span data-stu-id="81ecf-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="81ecf-129">*Bu makalenin özgün içeriği için yem hu için teşekkürler.*</span><span class="sxs-lookup"><span data-stu-id="81ecf-129">*Thanks to Leo Hu for the original content of this article.*</span></span>
