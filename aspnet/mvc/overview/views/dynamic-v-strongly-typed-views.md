---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dinamik ve Türü kesin belirlenmiş görünümler | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455691"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="c0788-103">Dinamik ve</span><span class="sxs-lookup"><span data-stu-id="c0788-103">Dynamic v.</span></span> <span data-ttu-id="c0788-104">Kesin Türü Belirtilmiş Görünümler</span><span class="sxs-lookup"><span data-stu-id="c0788-104">Strongly Typed Views</span></span>

<span data-ttu-id="c0788-105">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="c0788-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="c0788-106">Bir denetleyiciden ASP.NET MVC 3 ' teki bir görünüme bilgi geçirmenin üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="c0788-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="c0788-107">Türü kesin belirlenmiş bir model nesnesi.</span><span class="sxs-lookup"><span data-stu-id="c0788-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="c0788-108">Dinamik bir tür olarak (@model dinamik kullanarak)</span><span class="sxs-lookup"><span data-stu-id="c0788-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="c0788-109">ViewBag kullanma</span><span class="sxs-lookup"><span data-stu-id="c0788-109">Using the ViewBag</span></span>

<span data-ttu-id="c0788-110">Dinamik ve kesin belirlenmiş görünümleri karşılaştırmak ve karşılaştırmak için basit bir MVC 3 üst Blog uygulaması yazdım.</span><span class="sxs-lookup"><span data-stu-id="c0788-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="c0788-111">Denetleyici basit bir blog listesi ile başlar:</span><span class="sxs-lookup"><span data-stu-id="c0788-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="c0788-112">Indexnotstonglytyped () metodunu sağ tıklatın ve bir Razor görünümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0788-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="c0788-113">[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c0788-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="c0788-114">**Kesin belirlenmiş görünüm oluştur** kutusunun işaretli olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="c0788-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="c0788-115">Elde edilen görünüm çok fazla içermez:</span><span class="sxs-lookup"><span data-stu-id="c0788-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="c0788-116">Kesin olarak belirlenmiş bir görünüm değil, dinamik olarak kullanılan bir görünüm kullandığından, IntelliSense bize yardımcı olmaz.</span><span class="sxs-lookup"><span data-stu-id="c0788-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="c0788-117">Tamamlanan kod aşağıda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c0788-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="c0788-118">[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c0788-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="c0788-119">Artık türü kesin belirlenmiş bir görünüm ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="c0788-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="c0788-120">Denetleyiciye aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c0788-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

<span data-ttu-id="c0788-121">Tam olarak aynı dönüş görünümüne (Topblogları) dikkat edin; kesin olmayan türsüz bir görünüm olarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="c0788-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="c0788-122">*Stonglytypedındex ()* içinde sağ tıklayın ve **Görünüm Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c0788-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="c0788-123">Bu kez **Blog** model sınıfını seçin ve Scaffold şablonu olarak **list** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c0788-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="c0788-124">[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c0788-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="c0788-125">Yeni görünüm şablonunun içinde IntelliSense desteği alırız.</span><span class="sxs-lookup"><span data-stu-id="c0788-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="c0788-126">[![7002. IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c0788-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="c0788-127">C# projesi [buradan](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c0788-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
