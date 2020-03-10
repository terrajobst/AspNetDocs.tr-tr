---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: Model bağlama ve Web formlarıyla verileri sıralama, sayfalama ve filtreleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548064"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="f6bbf-104">Model bağlama ve Web formlarıyla verileri sıralama, sayfalama ve filtreleme</span><span class="sxs-lookup"><span data-stu-id="f6bbf-104">Sorting, paging, and filtering data with model binding and web forms</span></span>

<span data-ttu-id="f6bbf-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="f6bbf-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f6bbf-106">Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="f6bbf-107">Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="f6bbf-108">Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="f6bbf-109">Bu öğretici, model bağlama aracılığıyla verilerin nasıl sıralanması, sayfalama ve filtrelemesinin ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="f6bbf-110">Bu öğreticide, serinin ilk [bölümünde](retrieving-data.md) oluşturulan proje oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="f6bbf-111">Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="f6bbf-112">İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="f6bbf-113">Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="f6bbf-114">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="f6bbf-114">What you'll build</span></span>

<span data-ttu-id="f6bbf-115">Bu öğreticide şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f6bbf-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="f6bbf-116">Verilerin sıralanmasını ve Sayfalamayı Etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f6bbf-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="f6bbf-117">Kullanıcı tarafından seçime bağlı olarak verilerin filtrelenmesini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f6bbf-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="f6bbf-118">Sıralama Ekle</span><span class="sxs-lookup"><span data-stu-id="f6bbf-118">Add sorting</span></span>

<span data-ttu-id="f6bbf-119">GridView 'da sıralamayı etkinleştirmek çok kolaydır.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="f6bbf-120">Öğrenci. aspx dosyasında, GridView 'da **Allowsıralamayı** **true** olarak ayarlamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="f6bbf-121">DataField 'in otomatik olarak kullanıldığı için her sütun için bir **SortExpression** değeri ayarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="f6bbf-122">GridView, verileri seçili değere göre sıralamayı dahil etmek için sorguyu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="f6bbf-123">Aşağıdaki vurgulanan kod, sıralamayı etkinleştirmek için yapmanız gereken ek eki gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="f6bbf-124">Web uygulamasını çalıştırın ve farklı sütunlardaki değerlere göre öğrenci kayıtlarını sıralamayı test edin.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![öğrencileri Sırala](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="f6bbf-126">Sayfalama Ekle</span><span class="sxs-lookup"><span data-stu-id="f6bbf-126">Add paging</span></span>

<span data-ttu-id="f6bbf-127">Sayfalama özelliğinin etkinleştirilmesi de çok kolaydır.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="f6bbf-128">GridView 'da, **AllowPaging** özelliğini **true** olarak ayarlayın ve **PageSize** özelliğini her sayfada görüntülenmesini istediğiniz kayıt sayısı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="f6bbf-129">Bu öğreticide, 4 olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="f6bbf-130">Web uygulamasını çalıştırın ve şimdi kayıtların tek bir sayfada 4 ' ten fazla kayıt görüntülenmeksizin birden çok sayfanın üzerine bölündiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![Sayfalama Ekle](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="f6bbf-132">Ertelenmiş sorgu yürütme, uygulama verimliliğini geliştirir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="f6bbf-133">GridView, tüm veri kümesini almak yerine yalnızca geçerli sayfanın kayıtlarını almak için sorguyu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="f6bbf-134">Kayıtları Kullanıcı seçimine göre filtrele</span><span class="sxs-lookup"><span data-stu-id="f6bbf-134">Filter records by user selection</span></span>

<span data-ttu-id="f6bbf-135">Model bağlama, bir model bağlama yönteminde bir parametre için değer ayarlamayı tanımlamanızı sağlayan birkaç öznitelik ekler.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="f6bbf-136">Bu öznitelikler **System. Web. ModelBinding** ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="f6bbf-137">Bunlara aşağıdakiler dahildir:</span><span class="sxs-lookup"><span data-stu-id="f6bbf-137">They include:</span></span>

- <span data-ttu-id="f6bbf-138">Denetim</span><span class="sxs-lookup"><span data-stu-id="f6bbf-138">Control</span></span>
- <span data-ttu-id="f6bbf-139">Tanımlama Bilgisi</span><span class="sxs-lookup"><span data-stu-id="f6bbf-139">Cookie</span></span>
- <span data-ttu-id="f6bbf-140">Form</span><span class="sxs-lookup"><span data-stu-id="f6bbf-140">Form</span></span>
- <span data-ttu-id="f6bbf-141">Profil</span><span class="sxs-lookup"><span data-stu-id="f6bbf-141">Profile</span></span>
- <span data-ttu-id="f6bbf-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="f6bbf-142">QueryString</span></span>
- <span data-ttu-id="f6bbf-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="f6bbf-143">RouteData</span></span>
- <span data-ttu-id="f6bbf-144">Oturum</span><span class="sxs-lookup"><span data-stu-id="f6bbf-144">Session</span></span>
- <span data-ttu-id="f6bbf-145">UserProfile</span><span class="sxs-lookup"><span data-stu-id="f6bbf-145">UserProfile</span></span>
- <span data-ttu-id="f6bbf-146">ViewState</span><span class="sxs-lookup"><span data-stu-id="f6bbf-146">ViewState</span></span>

<span data-ttu-id="f6bbf-147">Bu öğreticide, GridView 'da görüntülenecek kayıtları filtrelemek için bir denetimin değerini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="f6bbf-148">Daha önce oluşturduğunuz sorgu yöntemine **Denetim** özniteliğini ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="f6bbf-149">[Sonraki](using-query-string-values-to-retrieve-data.md) bir öğreticide, parametre değerinin bir sorgu dizesi değerinden geldiğini belirtmek için **QueryString** özniteliğini bir parametreye uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="f6bbf-150">İlk olarak, ValidationSummary 'nin üzerinde gösterilen öğrencileri filtrelemek için bir açılır liste ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="f6bbf-151">Arka plan kod dosyasında, select metodunu, denetimden bir değer alacak şekilde değiştirin ve parametrenin adını değeri sağlayan denetimin adı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="f6bbf-152">Denetim özniteliğini çözümlemek için **System. Web. ModelBinding** ad alanı için bir **using** ifadesini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="f6bbf-153">Aşağıdaki kod, döndürülen verileri açılan liste değerine göre filtrelemek için Select yöntemini yeniden çalıştı ' ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="f6bbf-154">Bir parametre önüne bir denetim özniteliği eklemek, bu parametrenin değerinin aynı ada sahip bir denetimden geldiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="f6bbf-155">Öğrenciler listesini filtrelemek için Web uygulamasını çalıştırın ve açılan listeden farklı değerler seçin.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![öğrencileri filtrele](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="f6bbf-157">Sonuç</span><span class="sxs-lookup"><span data-stu-id="f6bbf-157">Conclusion</span></span>

<span data-ttu-id="f6bbf-158">Bu öğreticide, verileri sıralamayı ve sayfalama 'yi etkinleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="f6bbf-159">Ayrıca, verileri bir denetimin değerine göre filtrelemeyi de etkinleştirmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="f6bbf-160">Sonraki [öğreticide](integrating-jquery-ui.md) , jQuery UI pencere öğesini dinamik veri şablonuyla TÜMLEŞTIREREK Kullanıcı arabirimini geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6bbf-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f6bbf-161">[Önceki](updating-deleting-and-creating-data.md)
> [İleri](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="f6bbf-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
