---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Entity Framework 4,0 ve ObjectDataSource denetimini kullanma, 3. Bölüm: sıralama ve filtreleme | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, Entity Framework 4,0 öğretici serisi ile çalışmaya başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631672"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="f54f3-104">Entity Framework 4,0 ve ObjectDataSource denetimini kullanma, 3. Bölüm: sıralama ve filtreleme</span><span class="sxs-lookup"><span data-stu-id="f54f3-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>

<span data-ttu-id="f54f3-105">[Tom Dykstra](https://github.com/tdykstra) tarafından</span><span class="sxs-lookup"><span data-stu-id="f54f3-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="f54f3-106">Bu öğretici serisi, [Entity Framework 4,0 öğretici serisi Ile çalışmaya](https://asp.net/entity-framework/tutorials#Getting%20Started) başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f54f3-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="f54f3-107">Önceki öğreticileri tamamlamadıysanız, bu öğretici için bir başlangıç noktası olarak, oluşturduğunuz [uygulamayı indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) .</span><span class="sxs-lookup"><span data-stu-id="f54f3-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="f54f3-108">Ayrıca, tüm öğretici serileri tarafından oluşturulan [uygulamayı da indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) .</span><span class="sxs-lookup"><span data-stu-id="f54f3-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="f54f3-109">Öğreticiler hakkında sorularınız varsa, bunları [ASP.NET Entity Framework forumuna](https://forums.asp.net/1227.aspx)gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f54f3-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>

<span data-ttu-id="f54f3-110">Önceki öğreticide, Entity Framework ve `ObjectDataSource` denetimini kullanan n katmanlı bir Web uygulamasına depo modelini uyguladık.</span><span class="sxs-lookup"><span data-stu-id="f54f3-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="f54f3-111">Bu öğreticide, sıralama ve filtreleme ve ana ayrıntı senaryolarını işleme işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f54f3-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="f54f3-112">Aşağıdaki geliştirmeleri *Departmanlar. aspx* sayfasına ekleyeceksiniz:</span><span class="sxs-lookup"><span data-stu-id="f54f3-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="f54f3-113">Kullanıcıların departmanları ada göre seçmesine izin veren bir metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f54f3-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="f54f3-114">Kılavuzda gösterilen her departman için kurslar listesi.</span><span class="sxs-lookup"><span data-stu-id="f54f3-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="f54f3-115">Sütun başlıklarına tıklayarak sıralama özelliği.</span><span class="sxs-lookup"><span data-stu-id="f54f3-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="f54f3-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f54f3-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="f54f3-117">GridView sütunlarını sıralama özelliği ekleme</span><span class="sxs-lookup"><span data-stu-id="f54f3-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="f54f3-118">*Departmanlar. aspx* sayfasını açın ve `DepartmentsObjectDataSource`adlı `ObjectDataSource` denetimine bir `SortParameterName="sortExpression"` özniteliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f54f3-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="f54f3-119">(Daha sonra, `sortExpression`adlı bir parametre alan `GetDepartments` yöntemi oluşturacaksınız.) Denetimin açılış etiketiyle ilgili biçimlendirme şimdi aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="f54f3-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="f54f3-120">`GridView` denetiminin açılış etiketine `AllowSorting="true"` özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f54f3-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="f54f3-121">Denetimin açılış etiketiyle ilgili biçimlendirme şimdi aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="f54f3-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="f54f3-122">*Departments.aspx.cs*' de, `Page_Load` yönteminden `GridView` denetiminin `Sort` yöntemini çağırarak varsayılan sıralama düzenini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="f54f3-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="f54f3-123">İş mantığı sınıfında veya depo sınıfında sıralama ya da filtre uygulayan bir kod ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f54f3-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="f54f3-124">İş mantığı sınıfında bunu yaparsanız sıralama veya filtreleme işi, veri veritabanından alındıktan sonra yapılır, çünkü iş mantığı sınıfı depo tarafından döndürülen bir `IEnumerable` nesnesiyle çalışır.</span><span class="sxs-lookup"><span data-stu-id="f54f3-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="f54f3-125">Depo sınıfına sıralama ve filtreleme kodu ekler ve bunu bir LINQ ifadesi veya nesne sorgusu `IEnumerable` nesnesine dönüştürüldükten sonra yaparsanız, komutlarınız işlenmek üzere veritabanına geçirilir, bu da genellikle daha etkilidir.</span><span class="sxs-lookup"><span data-stu-id="f54f3-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="f54f3-126">Bu öğreticide, sıralama ve filtrelemeyi, işleme veritabanı tarafından (yani depodaki) yapılmasına neden olacak şekilde uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f54f3-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="f54f3-127">Sıralama yeteneği eklemek için depo arabirimine ve depo sınıflarına ek olarak, iş mantığı sınıfına yeni bir yöntem eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f54f3-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="f54f3-128">*ISchoolRepository.cs* dosyasında, döndürülen departmanlar listesini sıralamak için kullanılacak bir `sortExpression` parametresi alan yeni bir `GetDepartments` yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="f54f3-129">`sortExpression` parametresi, sıralanacak sütunu ve sıralama yönünü belirler.</span><span class="sxs-lookup"><span data-stu-id="f54f3-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="f54f3-130">Yeni yöntemin kodunu *SchoolRepository.cs* dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="f54f3-131">Yeni yöntemi çağırmak için mevcut parametresiz `GetDepartments` yöntemini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="f54f3-132">Test projesinde, *MockSchoolRepository.cs*öğesine aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="f54f3-133">Bu yönteme bağımlı olan herhangi bir birim testini, sıralanmış bir liste döndüleyecekseniz, listeyi döndürmeden önce sıralamalısınız.</span><span class="sxs-lookup"><span data-stu-id="f54f3-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="f54f3-134">Bu öğreticide olduğu gibi test oluşturmayacağız, bu nedenle yöntem yalnızca sıralanmamış departmanlar listesini döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="f54f3-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="f54f3-135">*SchoolBL.cs* dosyasında, iş mantığı sınıfına aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="f54f3-136">Bu kod, sıralama parametresini depo yöntemine geçirir.</span><span class="sxs-lookup"><span data-stu-id="f54f3-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="f54f3-137">*Departmanlar. aspx* sayfasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f54f3-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="f54f3-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f54f3-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="f54f3-139">Artık herhangi bir sütun başlığına tıklayarak bu sütuna göre sıralama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f54f3-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="f54f3-140">Sütun zaten sırlanmışsa, başlığa tıklamak sıralama yönünü tersine çevirir.</span><span class="sxs-lookup"><span data-stu-id="f54f3-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="f54f3-141">Arama kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="f54f3-141">Adding a Search Box</span></span>

<span data-ttu-id="f54f3-142">Bu bölümde, bir arama metin kutusu ekleyecek, bir denetim parametresi kullanarak `ObjectDataSource` denetimine bağlayacaksınız ve Filtrelemeyi desteklemek için iş mantığı sınıfına bir yöntem ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="f54f3-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="f54f3-143">*Departmanlar. aspx* sayfasını açın ve başlık ve ilk `ObjectDataSource` denetimi arasına aşağıdaki biçimlendirmeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="f54f3-144">`DepartmentsObjectDataSource`adlı `ObjectDataSource` denetiminde şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="f54f3-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="f54f3-145">`SearchTextBox` denetiminde girilen değeri alan `nameSearchString` adlı bir parametre için `SelectParameters` öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f54f3-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="f54f3-146">`SelectMethod` öznitelik değerini `GetDepartmentsByName`olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f54f3-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="f54f3-147">(Bu yöntemi daha sonra oluşturacaksınız.)</span><span class="sxs-lookup"><span data-stu-id="f54f3-147">(You'll create this method later.)</span></span>

<span data-ttu-id="f54f3-148">`ObjectDataSource` denetimine yönelik biçimlendirme artık aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="f54f3-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="f54f3-149">*ISchoolRepository.cs*' de, hem `sortExpression` hem de `nameSearchString` parametrelerini alan bir `GetDepartmentsByName` yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="f54f3-150">*SchoolRepository.cs*' de aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="f54f3-151">Bu kod, arama dizesini içeren öğeleri seçmek için bir `Where` yöntemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="f54f3-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="f54f3-152">Arama dizesi boşsa, tüm kayıtlar seçilir.</span><span class="sxs-lookup"><span data-stu-id="f54f3-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="f54f3-153">Yöntem çağrılarını bunun gibi bir bildirimde belirttiğinizde (`Include`, sonra `OrderBy`, sonra da `Where`), `Where` yönteminin her zaman en son olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f54f3-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="f54f3-154">Yeni yöntemi çağırmak için bir `sortExpression` parametresi alan mevcut `GetDepartments` yöntemini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="f54f3-155">Test projesindeki *MockSchoolRepository.cs* içinde aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="f54f3-156">*SchoolBL.cs*' de aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="f54f3-157">*Departmanlar. aspx* sayfasını çalıştırın ve seçim mantığının çalıştığından emin olmak için bir arama dizesi girin.</span><span class="sxs-lookup"><span data-stu-id="f54f3-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="f54f3-158">Metin kutusunu boş bırakın ve tüm kayıtların döndürüldüğünden emin olmak için bir arama deneyin.</span><span class="sxs-lookup"><span data-stu-id="f54f3-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="f54f3-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f54f3-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="f54f3-160">Her kılavuz satırı için ayrıntı sütunu ekleme</span><span class="sxs-lookup"><span data-stu-id="f54f3-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="f54f3-161">Ardından, kılavuzun sağ hücresinde görünen her bir departmanın tüm kurslarını görmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="f54f3-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="f54f3-162">Bunu yapmak için, iç içe geçmiş bir `GridView` denetimini kullanacaksınız ve `Department` varlığının `Courses` gezinti özelliğinden verileri veri yoluyla vereceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f54f3-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="f54f3-163">*Departmanlar. aspx* ' i açın ve `GridView` denetimi için biçimlendirme içinde `RowDataBound` olayı için bir işleyici belirtin.</span><span class="sxs-lookup"><span data-stu-id="f54f3-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="f54f3-164">Denetimin açılış etiketiyle ilgili biçimlendirme şimdi aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="f54f3-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="f54f3-165">`Administrator` şablonu alanından sonra yeni bir `TemplateField` öğesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="f54f3-166">Bu biçimlendirme bir kurs listesinin kurs numarasını ve başlığını gösteren bir iç içe `GridView` denetimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f54f3-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="f54f3-167">`RowDataBound` işleyicisinde kodda bir veri kaynağı oluşturacağından bir veri kaynağı belirtmez.</span><span class="sxs-lookup"><span data-stu-id="f54f3-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="f54f3-168">*Departments.aspx.cs* ' i açın ve `RowDataBound` olayı için aşağıdaki işleyiciyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f54f3-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="f54f3-169">Bu kod, olay bağımsız değişkenlerinden `Department` varlığını alır, `Courses` gezinti özelliğini bir `List` koleksiyonuna dönüştürür ve iç içe `GridView` koleksiyona databinds.</span><span class="sxs-lookup"><span data-stu-id="f54f3-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="f54f3-170">*SchoolRepository.cs* dosyasını açın ve `GetDepartmentsByName` yönteminde oluşturduğunuz nesne sorgusunda `Include` yöntemini çağırarak `Courses` gezinti özelliği için Eager yükleme belirtin.</span><span class="sxs-lookup"><span data-stu-id="f54f3-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="f54f3-171">`GetDepartmentsByName` yöntemindeki `return` deyimleri artık aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="f54f3-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="f54f3-172">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f54f3-172">Run the page.</span></span> <span data-ttu-id="f54f3-173">Daha önce eklediğiniz sıralama ve filtreleme özelliğine ek olarak, GridView denetimi artık her departman için iç içe geçmiş kurs ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f54f3-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="f54f3-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f54f3-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="f54f3-175">Bu, sıralamaya, filtrelemeye ve ana ayrıntı senaryolarına giriş işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="f54f3-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="f54f3-176">Sonraki öğreticide eşzamanlılık işleme yöntemini göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f54f3-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f54f3-177">[Önceki](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [İleri](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="f54f3-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
