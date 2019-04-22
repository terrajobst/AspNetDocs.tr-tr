---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dinamik ve Kesin tür belirtilmiş görünümleri | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3235fc58fbf93cb87946f8ebd4a478eff7ce80e3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386144"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="195c7-103">Dinamik ve</span><span class="sxs-lookup"><span data-stu-id="195c7-103">Dynamic v.</span></span> <span data-ttu-id="195c7-104">Kesin Türü Belirtilmiş Görünümler</span><span class="sxs-lookup"><span data-stu-id="195c7-104">Strongly Typed Views</span></span>

<span data-ttu-id="195c7-105">Tarafından [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="195c7-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="195c7-106">ASP.NET MVC 3'te bir görünüm için bir denetleyiciden bilgi geçirmek için üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="195c7-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="195c7-107">Kesin olarak belirlenmiş model nesnesi.</span><span class="sxs-lookup"><span data-stu-id="195c7-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="195c7-108">Dinamik tür olarak (kullanarak @model dinamik)</span><span class="sxs-lookup"><span data-stu-id="195c7-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="195c7-109">Görünüm paketini kullanma</span><span class="sxs-lookup"><span data-stu-id="195c7-109">Using the ViewBag</span></span>

<span data-ttu-id="195c7-110">Ben karşılaştırın ve dinamik ve kesin türü belirtilmiş görünümleri için basit bir MVC 3 üst Blog uygulaması yazmamış.</span><span class="sxs-lookup"><span data-stu-id="195c7-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="195c7-111">Denetleyici basit bir listesini blogları ile başlar:</span><span class="sxs-lookup"><span data-stu-id="195c7-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="195c7-112">IndexNotStonglyTyped() yönteminde sağ tıklayın ve bir Razor görünüm ekleyin.</span><span class="sxs-lookup"><span data-stu-id="195c7-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="195c7-113">[![8475.NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="195c7-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="195c7-114">Emin **kesin türü belirtilmiş görünüm oluşturmak** kutunun işaretli değil.</span><span class="sxs-lookup"><span data-stu-id="195c7-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="195c7-115">Ekranda çok içermiyor:</span><span class="sxs-lookup"><span data-stu-id="195c7-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="195c7-116">Dinamik ve bir kesin türü belirtilmiş görünüm kullandığımızdan, IntelliSense bize yardımcı olmaz.</span><span class="sxs-lookup"><span data-stu-id="195c7-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="195c7-117">Tamamlanan kodu aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="195c7-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="195c7-118">[![6646.NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="195c7-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="195c7-119">Kesin türü belirtilmiş görünüm şimdi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="195c7-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="195c7-120">Denetleyici için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="195c7-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


<span data-ttu-id="195c7-121">Tam olarak aynı dönüş View(topBlogs) olduğuna dikkat edin; kesin olmayan türü belirtilmiş görünüm çağırın.</span><span class="sxs-lookup"><span data-stu-id="195c7-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="195c7-122">İçine sağ tıklayın *StonglyTypedIndex()* seçip **Görünüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="195c7-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="195c7-123">Bu süre seçin **Blog** seçin ve Model sınıfı **listesi** İskele şablon olarak.</span><span class="sxs-lookup"><span data-stu-id="195c7-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="195c7-124">[![5658.StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="195c7-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="195c7-125">Yeni Görünüm şablon içinde size IntelliSense desteği alın.</span><span class="sxs-lookup"><span data-stu-id="195c7-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="195c7-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="195c7-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="195c7-127">C# projesi indirilebilir [burada](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span><span class="sxs-lookup"><span data-stu-id="195c7-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
