---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: Model bağlama ve Web formlarıyla verileri filtrelemek için sorgu dizesi değerlerini kullanma | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639099"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a><span data-ttu-id="684f4-104">Model bağlama ve Web formlarıyla verileri filtrelemek için sorgu dizesi değerlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="684f4-104">Using query string values to filter data with model binding and web forms</span></span>

<span data-ttu-id="684f4-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="684f4-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="684f4-106">Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="684f4-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="684f4-107">Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir.</span><span class="sxs-lookup"><span data-stu-id="684f4-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="684f4-108">Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.</span><span class="sxs-lookup"><span data-stu-id="684f4-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="684f4-109">Bu öğreticide, sorgu dizesinde bir değerin nasıl geçirileceğini ve model bağlama yoluyla verileri almak için bu değerin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="684f4-109">This tutorial shows how to pass a value in the query string and use that value to retrieve data through model binding.</span></span>
> 
> <span data-ttu-id="684f4-110">Bu öğreticide, serinin [önceki](retrieving-data.md) bölümlerinde oluşturulan projede derleme yapılır.</span><span class="sxs-lookup"><span data-stu-id="684f4-110">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="684f4-111">Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="684f4-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="684f4-112">İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="684f4-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="684f4-113">Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="684f4-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="684f4-114">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="684f4-114">What you'll build</span></span>

<span data-ttu-id="684f4-115">Bu öğreticide şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="684f4-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="684f4-116">Bir öğrenciye yönelik kayıtlı kursları göstermek için yeni bir sayfa ekleyin</span><span class="sxs-lookup"><span data-stu-id="684f4-116">Add a new page to show the enrolled courses for a student</span></span>
2. <span data-ttu-id="684f4-117">Sorgu dizesindeki bir değere göre seçili öğrenci için kayıtlı kursları alın</span><span class="sxs-lookup"><span data-stu-id="684f4-117">Retrieve the enrolled courses for the selected student based on a value in the query string</span></span>
3. <span data-ttu-id="684f4-118">Kılavuz görünümünden yeni sayfaya sorgu dizesi değeri olan bir köprü ekleyin</span><span class="sxs-lookup"><span data-stu-id="684f4-118">Add a hyperlink with a query string value from the grid view to the new page</span></span>

<span data-ttu-id="684f4-119">Bu öğreticideki adımlar, bir açılan listede Kullanıcı seçimine bağlı olarak görüntülenen öğrencileri filtrelemek için daha önceki [öğreticide](sorting-paging-and-filtering-data.md) yaptığınız şekilde oldukça benzerdir.</span><span class="sxs-lookup"><span data-stu-id="684f4-119">The steps in this tutorial are fairly similar to what you did in the earlier [tutorial](sorting-paging-and-filtering-data.md) to filter the displayed students based on the user selection in a drop down list.</span></span> <span data-ttu-id="684f4-120">Bu öğreticide, parametre değerinin bir denetimden geldiğini belirtmek için Select yöntemindeki **Denetim** özniteliğini kullandınız.</span><span class="sxs-lookup"><span data-stu-id="684f4-120">In that tutorial, you used the **Control** attribute in the select method to specify that the parameter value comes from a control.</span></span> <span data-ttu-id="684f4-121">Bu öğreticide, parametre değerinin sorgu dizesinden geldiğini belirtmek için Select yönteminde **QueryString** özniteliğini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="684f4-121">In this tutorial, you'll use the **QueryString** attribute in the select method to specify that the parameter value comes from the query string.</span></span>

## <a name="add-new-page-for-displaying-a-students-courses"></a><span data-ttu-id="684f4-122">Öğrencinin kurslarını görüntülemek için yeni sayfa ekle</span><span class="sxs-lookup"><span data-stu-id="684f4-122">Add new page for displaying a student's courses</span></span>

<span data-ttu-id="684f4-123">Site. Master ana sayfasını kullanan yeni bir Web formu ekleyin ve sayfa **kurslarını**adlandırın.</span><span class="sxs-lookup"><span data-stu-id="684f4-123">Add a new web form that uses the Site.master master page, and name the page **Courses**.</span></span>

<span data-ttu-id="684f4-124">**Kurslar. aspx** dosyasında seçili öğrenci için kursları görüntülemek üzere bir kılavuz görünümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="684f4-124">In the **Courses.aspx** file, add a grid view to display the courses for the selected student.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a><span data-ttu-id="684f4-125">Select metodunu tanımlama</span><span class="sxs-lookup"><span data-stu-id="684f4-125">Define the select method</span></span>

<span data-ttu-id="684f4-126">**Courses.aspx.cs**' de, Select yöntemini Grid görünümünün **SelectMethod** özelliğinde belirttiğiniz adla eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="684f4-126">In **Courses.aspx.cs**, you will add the select method with the name you specified in the grid view's **SelectMethod** property.</span></span> <span data-ttu-id="684f4-127">Bu yöntemde, öğrencinin kurslarını almak için sorgu tanımlayacaksınız ve parametrenin parametreyle aynı ada sahip bir sorgu dizesi değerinden geldiğini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="684f4-127">In that method, you'll define the query for retrieving a student's courses, and specify that the parameter comes from a query string value with the same name as the parameter.</span></span>

<span data-ttu-id="684f4-128">İlk olarak, aşağıdaki **using** deyimlerini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="684f4-128">First, you must add the following **using** statements.</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

<span data-ttu-id="684f4-129">Ardından, aşağıdaki kodu Courses.aspx.cs öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="684f4-129">Then, add the following code to Courses.aspx.cs:</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

<span data-ttu-id="684f4-130">QueryString özniteliği, bu yöntemdeki parametreye otomatik olarak Studentitıd adlı bir sorgu dizesi atanır.</span><span class="sxs-lookup"><span data-stu-id="684f4-130">The QueryString attribute means that a query string value named StudentID is automatically assigned to the parameter in this method.</span></span>

## <a name="add-hyperlink-with-query-string-value"></a><span data-ttu-id="684f4-131">Sorgu dizesi değeri olan köprü ekleme</span><span class="sxs-lookup"><span data-stu-id="684f4-131">Add hyperlink with query string value</span></span>

<span data-ttu-id="684f4-132">Öğrenciler. aspx üzerinde kılavuz görünümünde, yeni kurslar sayfanıza bağlanan bir köprü alanı ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="684f4-132">In the grid view on Students.aspx, you will add a hyperlink field that links to your new Courses page.</span></span> <span data-ttu-id="684f4-133">Köprü, öğrencinin kimliğiyle bir sorgu dizesi değeri içerecektir.</span><span class="sxs-lookup"><span data-stu-id="684f4-133">The hyperlink will include a query string value with the student's id.</span></span>

<span data-ttu-id="684f4-134">Öğrenciler. aspx ' te, toplam krediler için alanın hemen altındaki kılavuz görünümü sütunlarına aşağıdaki alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="684f4-134">In Students.aspx, add the following field to the grid view columns just below the field for Total Credits.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

<span data-ttu-id="684f4-135">Uygulamayı çalıştırın ve kılavuz görünümünün şimdi kurslar bağlantısını içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="684f4-135">Run the application and notice that the grid view now includes the Courses link.</span></span>

![Köprü Ekle](using-query-string-values-to-retrieve-data/_static/image1.png)

<span data-ttu-id="684f4-137">Bağlantılardan birine tıkladığınızda, öğrencinin kayıtlı kurslarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="684f4-137">When you click one of the links, you'll see that student's enrolled courses.</span></span>

![kursları göster](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="684f4-139">Sonuç</span><span class="sxs-lookup"><span data-stu-id="684f4-139">Conclusion</span></span>

<span data-ttu-id="684f4-140">Bu öğreticide, sorgu dizesi değeri olan bir bağlantı eklediniz.</span><span class="sxs-lookup"><span data-stu-id="684f4-140">In this tutorial, you added a link with a query string value.</span></span> <span data-ttu-id="684f4-141">Select yöntemindeki parametre değeri için bu sorgu dizesi değerini kullandınız.</span><span class="sxs-lookup"><span data-stu-id="684f4-141">You used that query string value for the parameter value in the select method.</span></span>

<span data-ttu-id="684f4-142">Sonraki [öğreticide](adding-business-logic-layer.md), kodu arka plan kod dosyalarından iş mantığı katmanına ve veri erişim katmanına taşıyacaksınız.</span><span class="sxs-lookup"><span data-stu-id="684f4-142">In the next [tutorial](adding-business-logic-layer.md), you will move the code from the code-behind files into a business logic layer and a data access layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="684f4-143">[Önceki](integrating-jquery-ui.md)
> [İleri](adding-business-logic-layer.md)</span><span class="sxs-lookup"><span data-stu-id="684f4-143">[Previous](integrating-jquery-ui.md)
[Next](adding-business-logic-layer.md)</span></span>
