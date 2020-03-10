---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: bir ASP.NET MVC uygulamasındaki Entity Framework sıralama, filtreleme ve sayfalama ekleme | Microsoft Docs'
author: tdykstra
description: Bu öğreticide, **öğrenciler** dizin sayfasına sıralama, filtreleme ve sayfalama işlevselliği eklersiniz. Ayrıca basit bir gruplama sayfası da oluşturursunuz.
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616041"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="ddc9c-104">Öğretici: bir ASP.NET MVC uygulamasındaki Entity Framework sıralama, filtreleme ve sayfalama ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-104">Tutorial: Add sorting, filtering, and paging with the Entity Framework in an ASP.NET MVC application</span></span>

<span data-ttu-id="ddc9c-105">[Önceki öğreticide](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), `Student` varlıkların temel CRUD işlemleri için bir dizi Web sayfası uyguladık.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-105">In the [previous tutorial](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="ddc9c-106">Bu öğreticide, **öğrenciler** dizin sayfasına sıralama, filtreleme ve sayfalama işlevselliği eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-106">In this tutorial you add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="ddc9c-107">Ayrıca basit bir gruplama sayfası da oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-107">You also create a simple grouping page.</span></span>

<span data-ttu-id="ddc9c-108">Aşağıdaki görüntüde, işiniz bittiğinde sayfanın nasıl görüneceğine ilişkin bir gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-108">The following image shows what the page will look like when you're done.</span></span> <span data-ttu-id="ddc9c-109">Sütun başlıkları, kullanıcının sütuna göre sıralamak için tıkladığı bağlantılardır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-109">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="ddc9c-110">Sütun başlığına tıklanması artan ve azalan sıralama düzeni arasında sürekli olarak geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-110">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="ddc9c-112">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ddc9c-113">Sütun sıralama bağlantıları Ekle</span><span class="sxs-lookup"><span data-stu-id="ddc9c-113">Add column sort links</span></span>
> * <span data-ttu-id="ddc9c-114">Arama kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-114">Add a Search box</span></span>
> * <span data-ttu-id="ddc9c-115">Sayfalama Ekle</span><span class="sxs-lookup"><span data-stu-id="ddc9c-115">Add paging</span></span>
> * <span data-ttu-id="ddc9c-116">Hakkında bir sayfa oluşturun</span><span class="sxs-lookup"><span data-stu-id="ddc9c-116">Create an About page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddc9c-117">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ddc9c-117">Prerequisites</span></span>

* [<span data-ttu-id="ddc9c-118">Temel CRUD İşlevselliği Uygulama</span><span class="sxs-lookup"><span data-stu-id="ddc9c-118">Implementing Basic CRUD Functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a><span data-ttu-id="ddc9c-119">Sütun sıralama bağlantıları Ekle</span><span class="sxs-lookup"><span data-stu-id="ddc9c-119">Add column sort links</span></span>

<span data-ttu-id="ddc9c-120">Öğrenci dizini sayfasına sıralama eklemek için `Student` denetleyicisinin `Index` yöntemini değiştireceksiniz ve `Student` dizin görünümüne kod eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="ddc9c-121">Dizin yöntemine sıralama işlevi ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-121">Add sorting functionality to the Index method</span></span>

- <span data-ttu-id="ddc9c-122">*Controllers\studentcontroller.cs*içinde `Index` yöntemini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="ddc9c-123">Bu kod, URL 'deki sorgu dizesinden bir `sortOrder` parametresi alır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="ddc9c-124">Sorgu dizesi değeri, ASP.NET MVC tarafından eylem yöntemine bir parametre olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="ddc9c-125">Parametresi, "Name" veya "Date" adlı bir dizedir, isteğe bağlı olarak alt çizgi ve azalan sıra belirtmek için "desc" dizesi gelir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-125">The parameter is a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="ddc9c-126">Varsayılan sıralama düzeni artan.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-126">The default sort order is ascending.</span></span>

<span data-ttu-id="ddc9c-127">Dizin sayfası ilk kez istendiğinde sorgu dizesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="ddc9c-128">Öğrenciler `LastName`göre artan sırada görüntülenir. Bu, varsayılan olarak, `switch` deyimindeki karşı bir durum tarafından oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="ddc9c-129">Kullanıcı bir sütun başlığı köprüsüne tıkladığında, sorgu dizesinde uygun `sortOrder` değeri sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="ddc9c-130">İki `ViewBag` değişkeni, görünümün sütun başlığı köprülerini uygun sorgu dizesi değerleriyle yapılandırabilmesi için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="ddc9c-131">Bunlar Üçlü ifadelerdir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-131">These are ternary statements.</span></span> <span data-ttu-id="ddc9c-132">Birincisi, `sortOrder` parametresi null veya boş ise `ViewBag.NameSortParm` "ad\_desc" olarak ayarlanmalıdır; Aksi takdirde, boş bir dizeye ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="ddc9c-133">Bu iki deyim, görünümün sütun başlığı köprülerini şu şekilde ayarlamaya olanak tanır:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="ddc9c-134">Geçerli sıralama düzeni</span><span class="sxs-lookup"><span data-stu-id="ddc9c-134">Current sort order</span></span> | <span data-ttu-id="ddc9c-135">Son ad Köprüsü</span><span class="sxs-lookup"><span data-stu-id="ddc9c-135">Last Name Hyperlink</span></span> | <span data-ttu-id="ddc9c-136">Tarih Köprüsü</span><span class="sxs-lookup"><span data-stu-id="ddc9c-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ddc9c-137">Artan son ad</span><span class="sxs-lookup"><span data-stu-id="ddc9c-137">Last Name ascending</span></span> | <span data-ttu-id="ddc9c-138">descending</span><span class="sxs-lookup"><span data-stu-id="ddc9c-138">descending</span></span> | <span data-ttu-id="ddc9c-139">ascending</span><span class="sxs-lookup"><span data-stu-id="ddc9c-139">ascending</span></span> |
| <span data-ttu-id="ddc9c-140">Azalan son ad</span><span class="sxs-lookup"><span data-stu-id="ddc9c-140">Last Name descending</span></span> | <span data-ttu-id="ddc9c-141">ascending</span><span class="sxs-lookup"><span data-stu-id="ddc9c-141">ascending</span></span> | <span data-ttu-id="ddc9c-142">ascending</span><span class="sxs-lookup"><span data-stu-id="ddc9c-142">ascending</span></span> |
| <span data-ttu-id="ddc9c-143">Artan Tarih</span><span class="sxs-lookup"><span data-stu-id="ddc9c-143">Date ascending</span></span> | <span data-ttu-id="ddc9c-144">ascending</span><span class="sxs-lookup"><span data-stu-id="ddc9c-144">ascending</span></span> | <span data-ttu-id="ddc9c-145">descending</span><span class="sxs-lookup"><span data-stu-id="ddc9c-145">descending</span></span> |
| <span data-ttu-id="ddc9c-146">Azalan Tarih</span><span class="sxs-lookup"><span data-stu-id="ddc9c-146">Date descending</span></span> | <span data-ttu-id="ddc9c-147">ascending</span><span class="sxs-lookup"><span data-stu-id="ddc9c-147">ascending</span></span> | <span data-ttu-id="ddc9c-148">ascending</span><span class="sxs-lookup"><span data-stu-id="ddc9c-148">ascending</span></span> |

<span data-ttu-id="ddc9c-149">Yöntemi, sıralama yapılacak sütunu belirtmek için [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) kullanır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-149">The method uses [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) to specify the column to sort by.</span></span> <span data-ttu-id="ddc9c-150">Kod, `switch` ifadesinden önce bir <xref:System.Linq.IQueryable%601> değişkeni oluşturur, `switch` ifadesinde değiştirir ve `switch` deyimden sonra `ToList` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-150">The code creates an <xref:System.Linq.IQueryable%601> variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="ddc9c-151">`IQueryable` değişkenleri oluşturup değiştirirken veritabanına hiçbir sorgu gönderilmez.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="ddc9c-152">Sorgu, `ToList`gibi bir yöntemi çağırarak `IQueryable` nesnesini bir koleksiyona dönüştürene kadar yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="ddc9c-153">Bu nedenle, bu kod `return View` ifadeye kadar Yürütülmeyen tek bir sorgu ile sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="ddc9c-154">Her sıralama düzeni için farklı LINQ deyimleri yazmanın alternatif olarak, dinamik olarak bir LINQ deyimi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-154">As an alternative to writing different LINQ statements for each sort order, you can dynamically create a LINQ statement.</span></span> <span data-ttu-id="ddc9c-155">Dinamik LINQ hakkında daha fazla bilgi için bkz. [DYNAMIC LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span><span class="sxs-lookup"><span data-stu-id="ddc9c-155">For information about dynamic LINQ, see [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="ddc9c-156">Öğrenci dizini görünümüne sütun başlığı köprüleri ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-156">Add column heading hyperlinks to the Student index view</span></span>

1. <span data-ttu-id="ddc9c-157">*Views\student\ındex.cshtml*içinde, başlık satırı için `<tr>` ve `<th>` öğelerini vurgulanan kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-157">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   <span data-ttu-id="ddc9c-158">Bu kod, uygun sorgu dizesi değerleriyle köprüler ayarlamak için `ViewBag` özelliklerindeki bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-158">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

2. <span data-ttu-id="ddc9c-159">Sıralamayı doğrulamak için sayfayı çalıştırın ve **son ad** ve **kayıt tarihi** sütun başlıklarına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-159">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

   <span data-ttu-id="ddc9c-160">**Son ad** başlığına tıkladıktan sonra, öğrenciler azalan son ad sırasıyla görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-160">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

## <a name="add-a-search-box"></a><span data-ttu-id="ddc9c-161">Arama kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-161">Add a Search box</span></span>

<span data-ttu-id="ddc9c-162">Öğrenciler dizin sayfasına filtre eklemek için, görünüme bir metin kutusu ve Gönder düğmesi ekleyeceksiniz ve `Index` yönteminde ilgili değişiklikleri yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-162">To add filtering to the Students index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="ddc9c-163">Metin kutusu, ilk ad ve soyadı alanlarında arama yapmak için bir dize girmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-163">The text box lets you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="ddc9c-164">Dizin yöntemine filtreleme işlevi ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-164">Add filtering functionality to the Index method</span></span>

- <span data-ttu-id="ddc9c-165">*Controllers\studentcontroller.cs*içinde `Index` yöntemini aşağıdaki kodla değiştirin (değişiklikler vurgulanır):</span><span class="sxs-lookup"><span data-stu-id="ddc9c-165">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="ddc9c-166">Kod, `Index` yöntemine bir `searchString` parametresi ekler.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-166">The code adds a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="ddc9c-167">Arama dizesi değeri, dizin görünümüne ekleyeceğiniz bir metin kutusundan alınır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-167">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="ddc9c-168">Ayrıca, LINQ ifadesine yalnızca adı veya soyadı olan, arama dizesini içeren öğrencileri seçen bir `where` yan tümcesi ekler.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-168">It also adds a `where` clause to the LINQ statement that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="ddc9c-169"><xref:System.Linq.Queryable.Where%2A> yan tümcesini ekleyen deyimi, yalnızca aranacak bir değer varsa yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-169">The statement that adds the <xref:System.Linq.Queryable.Where%2A> clause executes only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="ddc9c-170">Çoğu durumda, bir Entity Framework varlık kümesinde veya bir bellek içi koleksiyonda uzantı yöntemi olarak aynı yöntemi çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-170">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="ddc9c-171">Sonuçlar normalde aynıdır, ancak bazı durumlarda farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-171">The results are normally the same but in some cases may be different.</span></span>
>
> <span data-ttu-id="ddc9c-172">Örneğin, `Contains` yönteminin .NET Framework uygulanması, buna boş bir dize geçirdiğinizde tüm satırları döndürür, ancak SQL Server Compact 4,0 Entity Framework sağlayıcısı boş dizeler için sıfır satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-172">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="ddc9c-173">Bu nedenle örnekteki kod (`Where` deyimin `if` bir deyimin içine yerleştirilmesi), tüm SQL Server sürümleri için aynı sonuçları elde ettiğinizden emin olmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-173">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="ddc9c-174">Ayrıca, `Contains` yönteminin .NET Framework uygulanması, varsayılan olarak büyük/küçük harfe duyarlı bir karşılaştırma gerçekleştirir, ancak Entity Framework SQL Server sağlayıcılar varsayılan olarak büyük/küçük harfe duyarsız karşılaştırmalar yapar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-174">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="ddc9c-175">Bu nedenle, testi açık büyük/küçük harfe duyarsız hale getirmek için `ToUpper` yöntemini çağırmak, daha sonra kodu bir `IQueryable` nesnesi yerine `IEnumerable` bir koleksiyon döndürecek şekilde değiştirdiğinizde sonuçların değişmemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-175">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="ddc9c-176">(Bir `IEnumerable` koleksiyonunda `Contains` yöntemini çağırdığınızda .NET Framework uygulamasını alırsınız; bunu bir `IQueryable` nesnesi üzerinde çağırdığınızda, veritabanı sağlayıcısı uygulamasını alırsınız.)</span><span class="sxs-lookup"><span data-stu-id="ddc9c-176">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>
>
> <span data-ttu-id="ddc9c-177">Null işleme, farklı veritabanı sağlayıcıları için veya bir `IEnumerable` koleksiyonu kullandığınızda ile karşılaştırıldığında `IQueryable` bir nesne kullandığınızda da farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-177">Null handling may also be different for different database providers or when you use an `IQueryable` object compared to when you use an `IEnumerable` collection.</span></span> <span data-ttu-id="ddc9c-178">Örneğin, bazı senaryolarda `table.Column != 0` gibi `Where` bir koşul, değer olarak `null` olan sütunları döndürmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-178">For example, in some scenarios a `Where` condition such as `table.Column != 0` may not return columns that have `null` as the value.</span></span> <span data-ttu-id="ddc9c-179">Varsayılan olarak, null değerler arasındaki eşitlik, bellekte çalışır şekilde veritabanında çalışır, ancak bu davranışı yapılandırmak için, EF6 içinde [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) bayrağını ayarlayabilir veya EF Core [Userelationalnulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) metodunu çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-179">By default, EF generates additional SQL operators to make equality between null values work in the database like it works in memory, but you can set the [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) flag in EF6 or call the [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) method in EF Core to configure this behavior.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="ddc9c-180">Öğrenci dizini görünümüne arama kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-180">Add a search box to the Student index view</span></span>

1. <span data-ttu-id="ddc9c-181">*Views\student\ındex.cshtml*içinde, bir başlık, metin kutusu ve bir **arama** düğmesi oluşturmak için, açılan `table` etiketinden hemen önce vurgulanan kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-181">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. <span data-ttu-id="ddc9c-182">Sayfayı çalıştırın, bir arama dizesi girin ve filtreleme 'nin çalıştığını doğrulamak için **Ara** ' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-182">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

   <span data-ttu-id="ddc9c-183">URL 'nin "bir" arama dizesi içermediğini, yani bu sayfaya yer işareti eklerseniz, yer işaretini kullandığınızda filtrelenmiş listeyi almadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-183">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="ddc9c-184">Bu, tüm listeyi sıralacağından, sütun sıralama bağlantıları için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-184">This applies also to the column sort links, as they will sort the whole list.</span></span> <span data-ttu-id="ddc9c-185">**Arama** düğmesini daha sonra öğreticide daha sonra filtre ölçütlerine yönelik Sorgu dizelerini kullanacak şekilde değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-185">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging"></a><span data-ttu-id="ddc9c-186">Sayfalama Ekle</span><span class="sxs-lookup"><span data-stu-id="ddc9c-186">Add paging</span></span>

<span data-ttu-id="ddc9c-187">Öğrenciler dizin sayfasına sayfalama eklemek için **Pagedlist. Mvc** NuGet paketini yükleyerek başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-187">To add paging to the Students index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="ddc9c-188">Daha sonra `Index` yönteminde başka değişiklikler yapar ve `Index` görünümüne sayfalama bağlantıları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-188">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="ddc9c-189">**Pagedlist. Mvc** , ASP.NET MVC için çok iyi sayfalama ve sıralama paketlerinden biridir ve burada kullanılması, diğer seçeneklerin bir önerisi olarak değil yalnızca örnek olarak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-189">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span>

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="ddc9c-190">PagedList. MVC NuGet paketini yükler</span><span class="sxs-lookup"><span data-stu-id="ddc9c-190">Install the PagedList.MVC NuGet package</span></span>

<span data-ttu-id="ddc9c-191">NuGet **pagedlist. Mvc** paketi, **pagedlist** paketini otomatik olarak bir bağımlılık olarak yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-191">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="ddc9c-192">**Pagedlist** paketi, `IQueryable` ve `IEnumerable` koleksiyonları için `PagedList` bir koleksiyon türü ve genişletme yöntemleri yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-192">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="ddc9c-193">Uzantı yöntemleri `IQueryable` veya `IEnumerable``PagedList` koleksiyonda tek bir veri sayfası oluşturur ve `PagedList` koleksiyonu, sayfalama işlemini kolaylaştıran çeşitli özellikler ve yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-193">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="ddc9c-194">**Pagedlist. Mvc** paketi, sayfalama düğmelerini görüntüleyen bir sayfalama Yardımcısı yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-194">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

1. <span data-ttu-id="ddc9c-195">**Araçlar** menüsünde, **NuGet Paket Yöneticisi** ' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-195">From the **Tools** menu, select **NuGet Package Manager** and then **Package Manager Console**.</span></span>

2. <span data-ttu-id="ddc9c-196">**Paket Yöneticisi konsol** penceresinde, **paket kaynağının** **NuGet.org** olduğundan ve **varsayılan projenin** **contosouniversity**olduğundan emin olun ve ardından şu komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-196">In the **Package Manager Console** window, make sure the **Package source** is **nuget.org** and the **Default project** is **ContosoUniversity**, and then enter the following command:</span></span>

   ```text
   Install-Package PagedList.Mvc
   ```

3. <span data-ttu-id="ddc9c-197">Projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-197">Build the project.</span></span>

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="ddc9c-198">Dizin yöntemine sayfalama işlevselliği ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-198">Add paging functionality to the Index method</span></span>

1. <span data-ttu-id="ddc9c-199">*Controllers\studentcontroller.cs*içinde, `PagedList` ad alanı için `using` bir ifade ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-199">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. <span data-ttu-id="ddc9c-200">`Index` yöntemini aşağıdaki kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-200">Replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   <span data-ttu-id="ddc9c-201">Bu kod bir `page` parametresi, geçerli bir sıralama düzeni parametresi ve Yöntem imzasına geçerli bir filtre parametresi ekler:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-201">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="ddc9c-202">Sayfa ilk kez görüntülenirken veya Kullanıcı bir sayfalama veya sıralama bağlantısına tıklamamışsa, tüm parametreler null olur.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-202">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters are null.</span></span> <span data-ttu-id="ddc9c-203">Bir sayfalama bağlantısına tıklandıysanız, `page` değişkeni görüntülenecek sayfa numarasını içerir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-203">If a paging link is clicked, the `page` variable contains the page number to display.</span></span>

   <span data-ttu-id="ddc9c-204">`ViewBag` özelliği geçerli sıralama düzeni ile görünüm sağlar, çünkü bu sıralama sırasını sayfalama sırasında aynı tutmak için disk belleği bağlantılarına dahil edilmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-204">A `ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   <span data-ttu-id="ddc9c-205">`ViewBag.CurrentFilter`başka bir özellik, geçerli filtre dizesiyle görünüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-205">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="ddc9c-206">Bu değer, disk belleği sırasında filtre ayarlarını korumak için disk belleği bağlantılarına dahil olmalıdır ve sayfa yeniden görüntülenirken metin kutusuna geri yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-206">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="ddc9c-207">Arama dizesi sayfalama sırasında değiştirilmişse, yeni filtre farklı verilerin görüntülenmesini sağladığından sayfanın 1 olarak sıfırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-207">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="ddc9c-208">Metin kutusuna bir değer girildiğinde ve Gönder düğmesine basıldığında arama dizesi değişir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-208">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="ddc9c-209">Bu durumda `searchString` parametresi null değildir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-209">In that case, the `searchString` parameter is not null.</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   <span data-ttu-id="ddc9c-210">Yöntemin sonunda, öğrenciler `IQueryable` nesnesindeki `ToPagedList` uzantısı yöntemi, öğrenci sorgusunu, sayfalama destekleyen bir koleksiyon türünde tek bir öğrenciler sayfasına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-210">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="ddc9c-211">Bu tek bir öğrenci sayfası daha sonra görünüme geçirilir:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-211">That single page of students is then passed to the view:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   <span data-ttu-id="ddc9c-212">`ToPagedList` yöntemi bir sayfa numarası alır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-212">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="ddc9c-213">İki soru işareti, [null birleşim işlecini](/dotnet/csharp/language-reference/operators/null-coalescing-operator)temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-213">The two question marks represent the [null-coalescing operator](/dotnet/csharp/language-reference/operators/null-coalescing-operator).</span></span> <span data-ttu-id="ddc9c-214">Null birleşim işleci, Nullable bir tür için varsayılan değeri tanımlar; `(page ?? 1)` ifadesi bir değere sahipse `page` değerini döndürür veya `page` null ise 1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-214">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="ddc9c-215">Öğrenci dizini görünümüne sayfalama bağlantıları ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-215">Add paging links to the Student index view</span></span>

1. <span data-ttu-id="ddc9c-216">*Views\student\ındex.cshtml*içinde, var olan kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-216">In *Views\Student\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="ddc9c-217">Değişiklikler vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-217">The changes are highlighted.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   <span data-ttu-id="ddc9c-218">Sayfanın üst kısmındaki `@model` ifade, görünümün artık `List` nesnesi yerine `PagedList` bir nesne aldığından emin olarak belirtir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-218">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

   <span data-ttu-id="ddc9c-219">`PagedList.Mvc` için `using` deyimleri, sayfalama düğmelerinin MVC Yardımcısı 'na erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-219">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

   <span data-ttu-id="ddc9c-220">Kod, bir [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) aşırı yüklemesi kullanarak [FormMethod. Get](/previous-versions/aspnet/dd460179(v=vs.100))belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-220">The code uses an overload of [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) that allows it to specify [FormMethod.Get](/previous-versions/aspnet/dd460179(v=vs.100)).</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   <span data-ttu-id="ddc9c-221">Varsayılan [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) , form VERILERINI bir gönderiyle gönderir, yani Parametreler, URL 'de sorgu dizeleri olarak değil http ileti gövdesinde geçirilir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-221">The default [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="ddc9c-222">HTTP GET belirttiğinizde, form verileri URL 'ye sorgu dizeleri olarak geçirilir ve bu da kullanıcıların URL 'ye yer işareti eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-222">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="ddc9c-223">[Http get kullanımı Için W3C yönergeleri](http://www.w3.org/2001/tag/doc/whenToUseGet.html) , eylem bir güncelleştirmeye neden olmadığında Al ' ın kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-223">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) recommend that you should use GET when the action does not result in an update.</span></span>

   <span data-ttu-id="ddc9c-224">Metin kutusu geçerli arama dizesiyle başlatılır, böylece yeni bir sayfaya tıkladığınızda geçerli arama dizesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-224">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   <span data-ttu-id="ddc9c-225">Sütun üst bilgisi bağlantıları, kullanıcının filtre sonuçları içinde sıralama yapabilmesi için geçerli arama dizesini denetleyiciye geçirmek için sorgu dizesini kullanır:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-225">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   <span data-ttu-id="ddc9c-226">Geçerli sayfa ve toplam sayfa sayısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-226">The current page and total number of pages are displayed.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   <span data-ttu-id="ddc9c-227">Görüntülenecek sayfa yoksa, "sayfa 0/0" görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-227">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="ddc9c-228">(Bu durumda, `Model.PageNumber` 1 olduğu ve `Model.PageCount` 0 olduğu için sayfa numarası sayfa sayısından daha büyük olur.)</span><span class="sxs-lookup"><span data-stu-id="ddc9c-228">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

   <span data-ttu-id="ddc9c-229">Sayfalama düğmeleri `PagedListPager` Yardımcısı tarafından görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-229">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   <span data-ttu-id="ddc9c-230">`PagedListPager` Yardımcısı, URL 'Ler ve stil oluşturma da dahil olmak üzere özelleştirebilmeniz gereken birkaç seçenek sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-230">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="ddc9c-231">Daha fazla bilgi için GitHub sitesindeki [Troyıgocode/PagedList](https://github.com/TroyGoode/PagedList) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-231">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

2. <span data-ttu-id="ddc9c-232">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-232">Run the page.</span></span>

   <span data-ttu-id="ddc9c-233">Disk belleğinin çalıştığından emin olmak için farklı sıralama emirlerindeki disk belleği bağlantılarına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-233">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="ddc9c-234">Daha sonra bir arama dizesi girin ve sayfalama ve filtreleme ile doğru şekilde çalıştığını doğrulamak için sayfalama işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-234">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page"></a><span data-ttu-id="ddc9c-235">Hakkında bir sayfa oluşturun</span><span class="sxs-lookup"><span data-stu-id="ddc9c-235">Create an About page</span></span>

<span data-ttu-id="ddc9c-236">Contoso Üniversitesi web sitesinin hakkında sayfasında, her bir kayıt tarihi için kaç öğrenciye kaydolduğunu görüntüleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-236">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="ddc9c-237">Bu, gruplar üzerinde gruplandırma ve basit hesaplamalar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-237">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="ddc9c-238">Bunu gerçekleştirmek için aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-238">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="ddc9c-239">Görünüme geçirmeniz gereken veriler için bir görünüm modeli sınıfı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-239">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="ddc9c-240">`Home` denetleyicisindeki `About` yöntemini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-240">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="ddc9c-241">`About` görünümünü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-241">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="ddc9c-242">Görünüm modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddc9c-242">Create the View Model</span></span>

<span data-ttu-id="ddc9c-243">Proje klasöründe bir *Viewmodeller* klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-243">Create a *ViewModels* folder in the project folder.</span></span> <span data-ttu-id="ddc9c-244">Bu klasörde, *EnrollmentDateGroup.cs* bir sınıf dosyası ekleyin ve şablon kodunu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-244">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="ddc9c-245">Ana denetleyiciyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-245">Modify the Home Controller</span></span>

1. <span data-ttu-id="ddc9c-246">*HomeController.cs*' de, dosyanın en üstüne aşağıdaki `using` deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-246">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. <span data-ttu-id="ddc9c-247">Sınıf için açma küme ayracından hemen sonra veritabanı bağlamı için bir sınıf değişkeni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-247">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. <span data-ttu-id="ddc9c-248">`About` yöntemini aşağıdaki kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-248">Replace the `About` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   <span data-ttu-id="ddc9c-249">LINQ deyimleri, öğrenci varlıklarını kayıt tarihine göre gruplandırır, her bir gruptaki varlıkların sayısını hesaplar ve sonuçları bir `EnrollmentDateGroup` View model nesneleri koleksiyonunda depolar.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-249">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

4. <span data-ttu-id="ddc9c-250">`Dispose` yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-250">Add a `Dispose` method:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="ddc9c-251">Hakkında görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-251">Modify the About View</span></span>

1. <span data-ttu-id="ddc9c-252">*Views\home\about.exe* dosyasındaki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-252">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. <span data-ttu-id="ddc9c-253">Uygulamayı çalıştırın ve **hakkında** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-253">Run the app and click the **About** link.</span></span>

   <span data-ttu-id="ddc9c-254">Her kayıt tarihi için öğrenci sayısı bir tabloda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-254">The count of students for each enrollment date displays in a table.</span></span>

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a><span data-ttu-id="ddc9c-256">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="ddc9c-256">Get the code</span></span>

[<span data-ttu-id="ddc9c-257">Tamamlanmış projeyi indirin</span><span class="sxs-lookup"><span data-stu-id="ddc9c-257">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="ddc9c-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ddc9c-258">Additional resources</span></span>

<span data-ttu-id="ddc9c-259">Diğer Entity Framework kaynaklarına bağlantılar, [ASP.NET Data Access-önerilen kaynaklar](../../../../whitepapers/aspnet-data-access-content-map.md)bölümünde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-259">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddc9c-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ddc9c-260">Next steps</span></span>

<span data-ttu-id="ddc9c-261">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="ddc9c-261">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ddc9c-262">Sütun sıralama bağlantıları Ekle</span><span class="sxs-lookup"><span data-stu-id="ddc9c-262">Add column sort links</span></span>
> * <span data-ttu-id="ddc9c-263">Arama kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="ddc9c-263">Add a Search box</span></span>
> * <span data-ttu-id="ddc9c-264">Sayfalama Ekle</span><span class="sxs-lookup"><span data-stu-id="ddc9c-264">Add paging</span></span>
> * <span data-ttu-id="ddc9c-265">Hakkında bir sayfa oluşturun</span><span class="sxs-lookup"><span data-stu-id="ddc9c-265">Create an About page</span></span>

<span data-ttu-id="ddc9c-266">Bağlantı dayanıklılığı ve komut yakalaşmayı nasıl kullanacağınızı öğrenmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="ddc9c-266">Advance to the next article to learn how to use connection resiliency and command interception.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ddc9c-267">Bağlantı dayanıklılığı ve komut yakaalımı</span><span class="sxs-lookup"><span data-stu-id="ddc9c-267">Connection resiliency and command interception</span></span>](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
