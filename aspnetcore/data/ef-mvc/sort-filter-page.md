---
title: 'Öğretici: Sıralama, filtreleme ve sayfalama - EF çekirdekli ASP.NET MVC Ekle'
description: Bu öğreticide, Öğrenciler dizin sayfasına sıralama, filtreleme ve sayfalama işlevselliğinin ekleyeceksiniz. Basit gruplandırma yapan bir sayfa da oluşturacaksınız.
author: rick-anderson
ms.author: tdykstra
ms.date: 02/04/2019
ms.topic: tutorial
uid: data/ef-mvc/sort-filter-page
ms.openlocfilehash: 51b6b08d2410652f93427371aec299eb4c8789f1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072033"
---
# <a name="tutorial-add-sorting-filtering-and-paging---aspnet-mvc-with-ef-core"></a><span data-ttu-id="19c01-104">Öğretici: Sıralama, filtreleme ve sayfalama - EF çekirdekli ASP.NET MVC Ekle</span><span class="sxs-lookup"><span data-stu-id="19c01-104">Tutorial: Add sorting, filtering, and paging - ASP.NET MVC with EF Core</span></span>

<span data-ttu-id="19c01-105">Önceki öğreticide, bir dizi web sayfaları için Öğrenci varlıkları temel CRUD işlemleri için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="19c01-105">In the previous tutorial, you implemented a set of web pages for basic CRUD operations for Student entities.</span></span> <span data-ttu-id="19c01-106">Bu öğreticide, Öğrenciler dizin sayfasına sıralama, filtreleme ve sayfalama işlevselliğinin ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="19c01-106">In this tutorial you'll add sorting, filtering, and paging functionality to the Students Index page.</span></span> <span data-ttu-id="19c01-107">Basit gruplandırma yapan bir sayfa da oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="19c01-107">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="19c01-108">Aşağıdaki çizim, hazır olduğunuzda sayfanın nasıl görüneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="19c01-108">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="19c01-109">Sütun başlıkları, kullanıcının sütuna göre sıralamak için tıklayabileceği bağlantılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="19c01-109">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="19c01-110">Bir sütun başlığına tekrar tekrar tıklayarak, artan veya azalan sıralama düzeni arasında geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="19c01-110">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Öğrenciler dizin sayfası](sort-filter-page/_static/paging.png)

<span data-ttu-id="19c01-112">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="19c01-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="19c01-113">Sütun sıralama bağlantılar ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-113">Add column sort links</span></span>
> * <span data-ttu-id="19c01-114">Bir arama kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-114">Add a Search box</span></span>
> * <span data-ttu-id="19c01-115">Disk belleği Öğrenciler dizine Ekle</span><span class="sxs-lookup"><span data-stu-id="19c01-115">Add paging to Students Index</span></span>
> * <span data-ttu-id="19c01-116">Disk belleği dizin yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="19c01-116">Add paging to Index method</span></span>
> * <span data-ttu-id="19c01-117">Disk belleği bağlantılar ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-117">Add paging links</span></span>
> * <span data-ttu-id="19c01-118">Hakkında sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="19c01-118">Create an About page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19c01-119">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="19c01-119">Prerequisites</span></span>

* [<span data-ttu-id="19c01-120">Bir ASP.NET Core MVC web uygulamasında EF Core ile CRUD işlevselliği uygulama</span><span class="sxs-lookup"><span data-stu-id="19c01-120">Implement CRUD Functionality with EF Core in an ASP.NET Core MVC web app</span></span>](crud.md)

## <a name="add-column-sort-links"></a><span data-ttu-id="19c01-121">Sütun sıralama bağlantılar ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-121">Add column sort links</span></span>

<span data-ttu-id="19c01-122">Öğrenci dizin sayfasına sıralama eklemek için değiştireceksiniz `Index` Öğrenciler denetleyicinin yöntemi ve kodu Öğrenci dizin görünümüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="19c01-122">To add sorting to the Student Index page, you'll change the `Index` method of the Students controller and add code to the Student Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="19c01-123">İşlevleri sıralama için dizin yöntemi ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-123">Add sorting Functionality to the Index method</span></span>

<span data-ttu-id="19c01-124">İçinde *StudentsController.cs*, değiştirin `Index` yöntemini aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="19c01-124">In *StudentsController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly)]

<span data-ttu-id="19c01-125">Bu kod alır bir `sortOrder` URL'ye sorgu dizesi parametresi.</span><span class="sxs-lookup"><span data-stu-id="19c01-125">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="19c01-126">Sorgu dizesi değerini eylem yönteminin bir parametresi olarak ASP.NET Core MVC tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="19c01-126">The query string value is provided by ASP.NET Core MVC as a parameter to the action method.</span></span> <span data-ttu-id="19c01-127">Parametre "Name" veya "Tarih", ardından isteğe bağlı olarak bir alt çizgi ve azalan düzende belirtmek için "desc" dizesi bir dize olur.</span><span class="sxs-lookup"><span data-stu-id="19c01-127">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="19c01-128">Varsayılan sıralama artan düzendedir.</span><span class="sxs-lookup"><span data-stu-id="19c01-128">The default sort order is ascending.</span></span>

<span data-ttu-id="19c01-129">Dizin Sayfası istendi, ilk kez hiçbir sorgu dizesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="19c01-129">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="19c01-130">Öğrenciler artan düzende başarısızlık durumunda tarafından belirlenen varsayılan olan soyadına göre görüntülenen `switch` deyimi.</span><span class="sxs-lookup"><span data-stu-id="19c01-130">The students are displayed in ascending order by last name, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="19c01-131">Kullanıcı uygun sütun başlığına köprü tıkladığında `sortOrder` değeri, sorgu dizesinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="19c01-131">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="19c01-132">İki `ViewData` öğelerini (NameSortParm ve DateSortParm) sütun başlığı köprüler uygun sorgu dize değerleri ile yapılandırmak için Görünüm tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="19c01-132">The two `ViewData` elements (NameSortParm and DateSortParm) are used by the view to configure the column heading hyperlinks with the appropriate query string values.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly&highlight=3-4)]

<span data-ttu-id="19c01-133">Üçlü deyimleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="19c01-133">These are ternary statements.</span></span> <span data-ttu-id="19c01-134">Olmadığını birincinin belirtir `sortOrder` parametresi null veya boş NameSortParm "name_desc için" olarak ayarlanmalıdır; Aksi takdirde, boş bir dize olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19c01-134">The first one specifies that if the `sortOrder` parameter is null or empty, NameSortParm should be set to "name_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="19c01-135">Bu iki deyimden sütun başlığı köprüler şu şekilde ayarlayın görünümün etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="19c01-135">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

|  <span data-ttu-id="19c01-136">Geçerli bir sıralama düzeni</span><span class="sxs-lookup"><span data-stu-id="19c01-136">Current sort order</span></span>  | <span data-ttu-id="19c01-137">Son adı köprü</span><span class="sxs-lookup"><span data-stu-id="19c01-137">Last Name Hyperlink</span></span> | <span data-ttu-id="19c01-138">Tarih köprü</span><span class="sxs-lookup"><span data-stu-id="19c01-138">Date Hyperlink</span></span> |
|:--------------------:|:-------------------:|:--------------:|
| <span data-ttu-id="19c01-139">Adı artan en son</span><span class="sxs-lookup"><span data-stu-id="19c01-139">Last Name ascending</span></span>  | <span data-ttu-id="19c01-140">descending</span><span class="sxs-lookup"><span data-stu-id="19c01-140">descending</span></span>          | <span data-ttu-id="19c01-141">ascending</span><span class="sxs-lookup"><span data-stu-id="19c01-141">ascending</span></span>      |
| <span data-ttu-id="19c01-142">Son azalan düzende ad</span><span class="sxs-lookup"><span data-stu-id="19c01-142">Last Name descending</span></span> | <span data-ttu-id="19c01-143">ascending</span><span class="sxs-lookup"><span data-stu-id="19c01-143">ascending</span></span>           | <span data-ttu-id="19c01-144">ascending</span><span class="sxs-lookup"><span data-stu-id="19c01-144">ascending</span></span>      |
| <span data-ttu-id="19c01-145">Artan tarihi</span><span class="sxs-lookup"><span data-stu-id="19c01-145">Date ascending</span></span>       | <span data-ttu-id="19c01-146">ascending</span><span class="sxs-lookup"><span data-stu-id="19c01-146">ascending</span></span>           | <span data-ttu-id="19c01-147">descending</span><span class="sxs-lookup"><span data-stu-id="19c01-147">descending</span></span>     |
| <span data-ttu-id="19c01-148">Azalan düzende tarihi</span><span class="sxs-lookup"><span data-stu-id="19c01-148">Date descending</span></span>      | <span data-ttu-id="19c01-149">ascending</span><span class="sxs-lookup"><span data-stu-id="19c01-149">ascending</span></span>           | <span data-ttu-id="19c01-150">ascending</span><span class="sxs-lookup"><span data-stu-id="19c01-150">ascending</span></span>      |

<span data-ttu-id="19c01-151">Yöntemi, LINQ to Entities göre sıralamak için sütun belirtmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="19c01-151">The method uses LINQ to Entities to specify the column to sort by.</span></span> <span data-ttu-id="19c01-152">Kod oluşturur bir `IQueryable` switch deyiminden önce değişkeni değiştirir, bu, switch ifadesi ve çağrıları `ToListAsync` sonrasına `switch` deyimi.</span><span class="sxs-lookup"><span data-stu-id="19c01-152">The code creates an `IQueryable` variable before the switch statement, modifies it in the switch statement, and calls the `ToListAsync` method after the `switch` statement.</span></span> <span data-ttu-id="19c01-153">Ne zaman oluşturma ve değiştirme `IQueryable` değişkenleri, sorgu veritabanına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="19c01-153">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="19c01-154">Sorgu dönüştürmeniz kadar yürütülen değil `IQueryable` nesne gibi bir yöntem çağırarak koleksiyonuna `ToListAsync`.</span><span class="sxs-lookup"><span data-stu-id="19c01-154">The query isn't executed until you convert the `IQueryable` object into a collection by calling a method such as `ToListAsync`.</span></span> <span data-ttu-id="19c01-155">Bu nedenle, bu kod, kadar yürütülmez tek bir sorgu sonuçları `return View` deyimi.</span><span class="sxs-lookup"><span data-stu-id="19c01-155">Therefore, this code results in a single query that's not executed until the `return View` statement.</span></span>

<span data-ttu-id="19c01-156">Bu kod, çok sayıda sütun ayrıntılı alabilir.</span><span class="sxs-lookup"><span data-stu-id="19c01-156">This code could get verbose with a large number of columns.</span></span> <span data-ttu-id="19c01-157">[Bu serideki son öğretici](advanced.md#dynamic-linq) adını geçirmenize olanak tanıyan kodunun nasıl yazılacağını gösterir `OrderBy` bir dize değişkeni sütunu.</span><span class="sxs-lookup"><span data-stu-id="19c01-157">[The last tutorial in this series](advanced.md#dynamic-linq) shows how to write code that lets you pass the name of the `OrderBy` column in a string variable.</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="19c01-158">Öğrenci dizini görünümü için sütun başlığını köprüler ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-158">Add column heading hyperlinks to the Student Index view</span></span>

<span data-ttu-id="19c01-159">Değiştirin *Views/Students/Index.cshtml*, sütun başlığını köprüler eklemek için aşağıdaki kod ile.</span><span class="sxs-lookup"><span data-stu-id="19c01-159">Replace the code in *Views/Students/Index.cshtml*, with the following code to add column heading hyperlinks.</span></span> <span data-ttu-id="19c01-160">Değiştirilen satırlar vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="19c01-160">The changed lines are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index2.cshtml?highlight=16,22)]

<span data-ttu-id="19c01-161">Bilgiler, bu kodu kullanan `ViewData` uygun sorgu köprülerle ayarlamak için özellikler dize değerleri.</span><span class="sxs-lookup"><span data-stu-id="19c01-161">This code uses the information in `ViewData` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="19c01-162">Uygulamayı çalıştırın, seçin **Öğrenciler** sekmesine ve tıklayın **Soyadı** ve **kayıt tarihi** sütun başlıkları, sıralama doğrulamak için çalışır.</span><span class="sxs-lookup"><span data-stu-id="19c01-162">Run the app, select the **Students** tab, and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![Öğrenciler dizin sayfası adı sırayla](sort-filter-page/_static/name-order.png)

## <a name="add-a-search-box"></a><span data-ttu-id="19c01-164">Bir arama kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-164">Add a Search box</span></span>

<span data-ttu-id="19c01-165">Öğrenciler dizin sayfasına filtre eklemek için görünümü için metin kutusu ve bir Gönder düğmesi ekleyin ve karşılık gelen değişiklik `Index` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="19c01-165">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="19c01-166">Metin kutusunda, ad ve soyadı alanları aramak için bir dize girin olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="19c01-166">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="19c01-167">Filtreleme işlevselliği dizin yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="19c01-167">Add filtering functionality to the Index method</span></span>

<span data-ttu-id="19c01-168">İçinde *StudentsController.cs*, değiştirin `Index` yöntemini aşağıdaki kodla (değişiklikleri vurgulanır).</span><span class="sxs-lookup"><span data-stu-id="19c01-168">In *StudentsController.cs*, replace the `Index` method with the following code (the changes are highlighted).</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilter&highlight=1,5,9-13)]

<span data-ttu-id="19c01-169">Eklediğiniz bir `searchString` parametresi `Index` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="19c01-169">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="19c01-170">Dizin görünümüne ekleyeceksiniz bir metin kutusundan arama dizesi değeri alındı.</span><span class="sxs-lookup"><span data-stu-id="19c01-170">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="19c01-171">LINQ deyime where ekledik, ad ve Soyadı arama dizesini içeren Öğrenciler seçer yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="19c01-171">You've also added to the LINQ statement a where clause that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="19c01-172">Where ekler deyimi yan tümcesi yalnızca aramak için bir değer ise yürütülür.</span><span class="sxs-lookup"><span data-stu-id="19c01-172">The statement that adds the where clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="19c01-173">Burada, aradığınız `Where` metodunda bir `IQueryable` nesne ve filtre, sunucuda işlenir.</span><span class="sxs-lookup"><span data-stu-id="19c01-173">Here you are calling the `Where` method on an `IQueryable` object, and the filter will be processed on the server.</span></span> <span data-ttu-id="19c01-174">Bazı senaryolarda, çağırma `Where` yöntemi olarak bir genişletme yöntemi bir bellek içi koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="19c01-174">In some scenarios you might be calling the `Where` method as an extension method on an in-memory collection.</span></span> <span data-ttu-id="19c01-175">(Örneğin, başvuru değiştirmeniz varsayalım `_context.Students` bir EF, bu nedenle, bunun yerine `DbSet` döndüren bir depo yöntemin başvurduğu bir `IEnumerable` koleksiyonu.) Sonuç, normalde aynı kalır ancak bazı durumlarda farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="19c01-175">(For example, suppose you change the reference to `_context.Students` so that instead of an EF `DbSet` it references a repository method that returns an `IEnumerable` collection.) The result would normally be the same but in some cases may be different.</span></span>
>
><span data-ttu-id="19c01-176">Örneğin, .NET Framework uygulamasını `Contains` yöntemi varsayılan olarak büyük küçük harfe duyarlı bir karşılaştırma yapar, ancak SQL Server'da bu SQL Server örneğinin harmanlama ayarı tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="19c01-176">For example, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but in SQL Server this is determined by the collation setting of the SQL Server instance.</span></span> <span data-ttu-id="19c01-177">Bu ayar için büyük küçük harf duyarsız varsayar.</span><span class="sxs-lookup"><span data-stu-id="19c01-177">That setting defaults to case-insensitive.</span></span> <span data-ttu-id="19c01-178">Çağırabilir `ToUpper` yöntemini test açıkça büyük küçük harf duyarsız sağlamak için:  *Where(s => s.LastName.ToUpper().Contains(searchString.ToUpper())*.</span><span class="sxs-lookup"><span data-stu-id="19c01-178">You could call the `ToUpper` method to make the test explicitly case-insensitive:  *Where(s => s.LastName.ToUpper().Contains(searchString.ToUpper())*.</span></span> <span data-ttu-id="19c01-179">Emin döndüren bir depoyu daha sonra kullanmak için kodu değiştirirseniz sonuçları aynı kalmasını bir `IEnumerable` koleksiyonu yerine bir `IQueryable` nesne.</span><span class="sxs-lookup"><span data-stu-id="19c01-179">That would ensure that results stay the same if you change the code later to use a repository which returns   an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="19c01-180">(Çağırdığınızda `Contains` metodunda bir `IEnumerable` koleksiyonu, .NET Framework uygulaması alın; çağırdığınızda, üzerinde bir `IQueryable` nesne veritabanı sağlayıcısı uygulamasını edinin.) Ancak, bu çözüm için bir performans cezası yoktur.</span><span class="sxs-lookup"><span data-stu-id="19c01-180">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.) However, there's a performance penalty for this solution.</span></span> <span data-ttu-id="19c01-181">`ToUpper` Kod TSQL seçin deyiminin WHERE yan tümcesinde bir işlev yerleştirecek.</span><span class="sxs-lookup"><span data-stu-id="19c01-181">The `ToUpper` code would put a function in the WHERE clause of the TSQL SELECT statement.</span></span> <span data-ttu-id="19c01-182">Bu, iyileştirici dizin kullanmasını önler.</span><span class="sxs-lookup"><span data-stu-id="19c01-182">That would prevent the optimizer from using an index.</span></span> <span data-ttu-id="19c01-183">SQL çoğunlukla olarak büyük küçük harf duyarsız yüklü olduğu düşünüldüğünde, kaçınmanız en iyisidir `ToUpper` büyük/küçük harfe veri deposuna aktarana kadar kodu.</span><span class="sxs-lookup"><span data-stu-id="19c01-183">Given that SQL is mostly installed as case-insensitive, it's best to avoid the `ToUpper` code until you migrate to a case-sensitive data store.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="19c01-184">Bir arama kutusu Öğrenci dizini görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-184">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="19c01-185">İçinde *Views/Student/Index.cshtml*, resim yazısı, bir metin kutusu oluşturmak için bir etiket hemen açılış tablo önce vurgulanmış kodu ekleyin ve bir **arama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="19c01-185">In *Views/Student/Index.cshtml*, add the highlighted code immediately before the opening table tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index3.cshtml?range=9-23&highlight=5-13)]

<span data-ttu-id="19c01-186">Bu kod `<form>` [etiket Yardımcısı](xref:mvc/views/tag-helpers/intro) arama metin kutusu ve düğme.</span><span class="sxs-lookup"><span data-stu-id="19c01-186">This code uses the `<form>` [tag helper](xref:mvc/views/tag-helpers/intro) to add the search text box and button.</span></span> <span data-ttu-id="19c01-187">Varsayılan olarak, `<form>` etiketi Yardımcısı parametreleri HTTP ileti gövdesini ve URL'yi içinde değil sorgu dizeleri geçirilir, yani bir GÖNDERİ ile form verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="19c01-187">By default, the `<form>` tag helper submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="19c01-188">HTTP GET belirttiğinizde, form verilerini URL'ye sorgu dizeleri kullanıcıların yer işareti URL'si sağlayan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="19c01-188">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="19c01-189">Kullanmanız gereken W3C yönergeleri önerilen eylemi bir güncelleştirmeye neden olmaz, alın.</span><span class="sxs-lookup"><span data-stu-id="19c01-189">The W3C guidelines recommend that you should use GET when the action doesn't result in an update.</span></span>

<span data-ttu-id="19c01-190">Uygulamayı çalıştırın, seçin **Öğrenciler** sekmesinde, bir arama dizesi girin ve filtreleme çalışıp çalışmadığını doğrulamak için Ara'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="19c01-190">Run the app, select the **Students** tab, enter a search string, and click Search to verify that filtering is working.</span></span>

![Filtreleme ile Öğrenciler dizin sayfası](sort-filter-page/_static/filtering.png)

<span data-ttu-id="19c01-192">URL arama dizesi içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="19c01-192">Notice that the URL contains the search string.</span></span>

```html
http://localhost:5813/Students?SearchString=an
```

<span data-ttu-id="19c01-193">Bu sayfaya yer işareti, yer işareti kullandığınızda filtrelenmiş liste elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="19c01-193">If you bookmark this page, you'll get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="19c01-194">Ekleme `method="get"` için `form` etikettir neyin neden oluşturulacak sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="19c01-194">Adding `method="get"` to the `form` tag is what caused the query string to be generated.</span></span>

<span data-ttu-id="19c01-195">Bu aşamada bir sütun başlığını sıralama bağlantı tıklarsanız girdiğiniz filtre değeri kaybedeceksiniz **arama** kutusu.</span><span class="sxs-lookup"><span data-stu-id="19c01-195">At this stage, if you click a column heading sort link you'll lose the filter value that you entered in the **Search** box.</span></span> <span data-ttu-id="19c01-196">Sonraki bölümde, çözeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="19c01-196">You'll fix that in the next section.</span></span>

## <a name="add-paging-to-students-index"></a><span data-ttu-id="19c01-197">Disk belleği Öğrenciler dizine Ekle</span><span class="sxs-lookup"><span data-stu-id="19c01-197">Add paging to Students Index</span></span>

<span data-ttu-id="19c01-198">Disk belleği Öğrenciler dizin sayfasına eklemek için oluşturacağınız bir `PaginatedList` kullanan sınıf `Skip` ve `Take` yerine her zaman tablonun tüm satırlarının alınırken sunucu üzerindeki verileri filtrelemek için deyimleri.</span><span class="sxs-lookup"><span data-stu-id="19c01-198">To add paging to the Students Index page, you'll create a `PaginatedList` class that uses `Skip` and `Take` statements to filter data on the server instead of always retrieving all rows of the table.</span></span> <span data-ttu-id="19c01-199">Sonra ek değişiklik yapacaksınız `Index` yöntemi ve disk belleği düğmeleri ekleme `Index` görünümü.</span><span class="sxs-lookup"><span data-stu-id="19c01-199">Then you'll make additional changes in the `Index` method and add paging buttons to the `Index` view.</span></span> <span data-ttu-id="19c01-200">Aşağıdaki çizim, disk belleği düğme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="19c01-200">The following illustration shows the paging buttons.</span></span>

![disk belleği bağlantılarla Öğrenciler dizin sayfası](sort-filter-page/_static/paging.png)

<span data-ttu-id="19c01-202">Proje klasöründe oluşturma `PaginatedList.cs`ve sonra şablon kodunu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="19c01-202">In the project folder, create `PaginatedList.cs`, and then replace the template code with the following code.</span></span>

[!code-csharp[](intro/samples/cu/PaginatedList.cs)]

<span data-ttu-id="19c01-203">`CreateAsync` Yöntemi bu kodda sayfa boyutu ve sayfa numarası alır ve uygun geçerlidir `Skip` ve `Take` deyimleriyle `IQueryable`.</span><span class="sxs-lookup"><span data-stu-id="19c01-203">The `CreateAsync` method in this code takes page size and page number and applies the appropriate `Skip` and `Take` statements to the `IQueryable`.</span></span> <span data-ttu-id="19c01-204">Zaman `ToListAsync` üzerinde çağrılır `IQueryable`, yalnızca istenen sayfayı içeren bir liste döndürür.</span><span class="sxs-lookup"><span data-stu-id="19c01-204">When `ToListAsync` is called on the `IQueryable`, it will return a List containing only the requested page.</span></span> <span data-ttu-id="19c01-205">Özellikleri `HasPreviousPage` ve `HasNextPage` etkinleştirmek veya devre dışı bırakmak için kullanılabilir **önceki** ve **sonraki** düğmeleri sayfalama.</span><span class="sxs-lookup"><span data-stu-id="19c01-205">The properties `HasPreviousPage` and `HasNextPage` can be used to enable or disable **Previous** and **Next** paging buttons.</span></span>

<span data-ttu-id="19c01-206">A `CreateAsync` yöntemi oluşturmak için bir oluşturucu yerine kullanılır `PaginatedList<T>` oluşturucular zaman uyumsuz kod çalıştırılamaz nesne.</span><span class="sxs-lookup"><span data-stu-id="19c01-206">A `CreateAsync` method is used instead of a constructor to create the `PaginatedList<T>` object because constructors can't run asynchronous code.</span></span>

## <a name="add-paging-to-index-method"></a><span data-ttu-id="19c01-207">Disk belleği dizin yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="19c01-207">Add paging to Index method</span></span>

<span data-ttu-id="19c01-208">İçinde *StudentsController.cs*, değiştirin `Index` yöntemini aşağıdaki kod ile.</span><span class="sxs-lookup"><span data-stu-id="19c01-208">In *StudentsController.cs*, replace the `Index` method with the following code.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilterPage&highlight=1-5,7,11-18,45-46)]

<span data-ttu-id="19c01-209">Bu kod, yöntem imzası için sayfa sayı parametresi, geçerli bir sıralama sipariş parametresi ve geçerli bir filtre parametresi ekler.</span><span class="sxs-lookup"><span data-stu-id="19c01-209">This code adds a page number parameter, a current sort order parameter, and a current filter parameter to the method signature.</span></span>

```csharp
public async Task<IActionResult> Index(
    string sortOrder,
    string currentFilter,
    string searchString,
    int? page)
```

<span data-ttu-id="19c01-210">Kullanıcı bir disk belleği veya bağlantı sıralama taşınmadığından seçeneğine tıkladıysanız, tüm parametreleri null veya ilk kez sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="19c01-210">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span>  <span data-ttu-id="19c01-211">Disk belleği bağlantıya tıkladıysanız, sayfa değişkenini görüntülemek için sayfa numarasını içerir.</span><span class="sxs-lookup"><span data-stu-id="19c01-211">If a paging link is clicked, the page variable will contain the page number to display.</span></span>

<span data-ttu-id="19c01-212">`ViewData` CurrentSort adlı bir öğe sıralama sırasında disk belleği aynı tutulabilmesi için disk belleği bağlantıları bu eklenmelidir çünkü geçerli sıralama düzenini görünümüyle sağlar.</span><span class="sxs-lookup"><span data-stu-id="19c01-212">The `ViewData` element named CurrentSort provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging.</span></span>

<span data-ttu-id="19c01-213">`ViewData` GeçerliFiltre adlı öğesi, geçerli bir filtre dizesi görünümüyle sağlar.</span><span class="sxs-lookup"><span data-stu-id="19c01-213">The `ViewData` element named CurrentFilter provides the view with the current filter string.</span></span> <span data-ttu-id="19c01-214">Bu değer sırasında disk belleği filtre ayarlarını sürdürmek için disk belleği bağlantıları eklenmelidir ve sayfası görüntülendiğinde, metin kutusuna geri yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="19c01-214">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span>

<span data-ttu-id="19c01-215">Arama dizesi sırasında disk belleği değiştirilirse, yeni filtre görüntülemek için farklı veri kaybına neden çünkü sayfa 1'e sıfırlanması gereken.</span><span class="sxs-lookup"><span data-stu-id="19c01-215">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="19c01-216">Arama dizesi, metin kutusuna girilen değer ve Gönder düğmesine basıldığında değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="19c01-216">The search string is changed when a value is entered in the text box and the Submit button is pressed.</span></span> <span data-ttu-id="19c01-217">Bu durumda, `searchString` parametresi null değil.</span><span class="sxs-lookup"><span data-stu-id="19c01-217">In that case, the `searchString` parameter isn't null.</span></span>

```csharp
if (searchString != null)
{
    page = 1;
}
else
{
    searchString = currentFilter;
}
```

<span data-ttu-id="19c01-218">Sonunda `Index` yöntemi `PaginatedList.CreateAsync` yöntemi disk belleği destekleyen bir koleksiyon türü Öğrenci tek sayfalık Öğrenci sorgu dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="19c01-218">At the end of the `Index` method, the `PaginatedList.CreateAsync` method converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="19c01-219">Öğrenciler, tek sayfalık ardından görünüme iletilir.</span><span class="sxs-lookup"><span data-stu-id="19c01-219">That single page of students is then passed to the view.</span></span>

```csharp
return View(await PaginatedList<Student>.CreateAsync(students.AsNoTracking(), page ?? 1, pageSize));
```

<span data-ttu-id="19c01-220">`PaginatedList.CreateAsync` Yöntemi, bir sayfa numarasını alır.</span><span class="sxs-lookup"><span data-stu-id="19c01-220">The `PaginatedList.CreateAsync` method takes a page number.</span></span> <span data-ttu-id="19c01-221">İki soru işareti null birleşim işleci temsil eder.</span><span class="sxs-lookup"><span data-stu-id="19c01-221">The two question marks represent the null-coalescing operator.</span></span> <span data-ttu-id="19c01-222">Boş değer atanabilir bir tür için varsayılan bir değer null birleşim işleci tanımlar; ifade `(page ?? 1)` anlamına gelir dönüş değerini `page` bir değere sahip veya 1 döndürür, `page` null.</span><span class="sxs-lookup"><span data-stu-id="19c01-222">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

## <a name="add-paging-links"></a><span data-ttu-id="19c01-223">Disk belleği bağlantılar ekleme</span><span class="sxs-lookup"><span data-stu-id="19c01-223">Add paging links</span></span>

<span data-ttu-id="19c01-224">İçinde *Views/Students/Index.cshtml*, mevcut kodu şu kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="19c01-224">In *Views/Students/Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="19c01-225">Değişiklikler vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="19c01-225">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index.cshtml?highlight=1,27,30,33,61-79)]

<span data-ttu-id="19c01-226">`@model` Sayfanın üstündeki deyimi belirtir görünüme artık alır bir `PaginatedList<T>` yerine Nesne bir `List<T>` nesne.</span><span class="sxs-lookup"><span data-stu-id="19c01-226">The `@model` statement at the top of the page specifies that the view now gets a `PaginatedList<T>` object instead of a `List<T>` object.</span></span>

<span data-ttu-id="19c01-227">Sütun üst bilgisi bağlantıları, kullanıcının içinde filtre sonuçlarını sıralayabilirsiniz, böylece geçerli arama dizesinin denetleyiciye geçirilecek sorgu dizesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="19c01-227">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

```html
<a asp-action="Index" asp-route-sortOrder="@ViewData["DateSortParm"]" asp-route-currentFilter ="@ViewData["CurrentFilter"]">Enrollment Date</a>
```

<span data-ttu-id="19c01-228">Disk belleği düğmeler tarafından etiket Yardımcıları görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="19c01-228">The paging buttons are displayed by tag helpers:</span></span>

```html
<a asp-action="Index"
   asp-route-sortOrder="@ViewData["CurrentSort"]"
   asp-route-page="@(Model.PageIndex - 1)"
   asp-route-currentFilter="@ViewData["CurrentFilter"]"
   class="btn btn-default @prevDisabled">
   Previous
</a>
```

<span data-ttu-id="19c01-229">Uygulamayı çalıştırın ve öğrenciler sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="19c01-229">Run the app and go to the Students page.</span></span>

![disk belleği bağlantılarla Öğrenciler dizin sayfası](sort-filter-page/_static/paging.png)

<span data-ttu-id="19c01-231">Disk belleği works emin olmak için farklı sıralamalar sayfalama bağlantıları tıklatın.</span><span class="sxs-lookup"><span data-stu-id="19c01-231">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="19c01-232">Ardından bir arama dizesi girin ve yeniden disk belleği de doğru sıralama ve filtreleme ile çalıştığını doğrulamak için disk belleği'ni deneyin.</span><span class="sxs-lookup"><span data-stu-id="19c01-232">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page"></a><span data-ttu-id="19c01-233">Hakkında sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="19c01-233">Create an About page</span></span>

<span data-ttu-id="19c01-234">Contoso University Web sitesinin için **hakkında** sayfasında, her kayıt tarihi için kaç Öğrenciler kaydedilmiş görüntüleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="19c01-234">For the Contoso University website's **About** page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="19c01-235">Bu gruplar üzerinde gruplandırma ve basit hesaplama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="19c01-235">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="19c01-236">Bunu yapmak için aşağıdakileri:</span><span class="sxs-lookup"><span data-stu-id="19c01-236">To accomplish this, you'll do the following:</span></span>

* <span data-ttu-id="19c01-237">Görünüme iletmek için gereken verileri için bir görünüm modeli sınıfı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19c01-237">Create a view model class for the data that you need to pass to the view.</span></span>

* <span data-ttu-id="19c01-238">Giriş denetleyicisine hakkında yöntemi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="19c01-238">Modify the About method in the Home controller.</span></span>

* <span data-ttu-id="19c01-239">Hakkında görünümü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="19c01-239">Modify the About view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="19c01-240">Görünüm modeli oluşturun</span><span class="sxs-lookup"><span data-stu-id="19c01-240">Create the view model</span></span>

<span data-ttu-id="19c01-241">Oluşturma bir *SchoolViewModels* klasöründe *modelleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="19c01-241">Create a *SchoolViewModels* folder in the *Models* folder.</span></span>

<span data-ttu-id="19c01-242">Yeni klasörde bir sınıf dosyası ekleyin *EnrollmentDateGroup.cs* ve şablon kodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="19c01-242">In the new folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/EnrollmentDateGroup.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="19c01-243">Giriş denetleyicisini değiştirmek</span><span class="sxs-lookup"><span data-stu-id="19c01-243">Modify the Home Controller</span></span>

<span data-ttu-id="19c01-244">İçinde *HomeController.cs*, aşağıdaki using deyimlerini dosyanın üstüne:</span><span class="sxs-lookup"><span data-stu-id="19c01-244">In *HomeController.cs*, add the following using statements at the top of the file:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings1)]

<span data-ttu-id="19c01-245">Hemen sınıfı için açılış kaşlı ayracından sonra veritabanı bağlamı için bir sınıf değişkeni ekleyin ve ASP.NET Core DI bağlam örneğini alın:</span><span class="sxs-lookup"><span data-stu-id="19c01-245">Add a class variable for the database context immediately after the opening curly brace for the class, and get an instance of the context from ASP.NET Core DI:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_AddContext&highlight=3,5,7)]

<span data-ttu-id="19c01-246">Değiştirin `About` yöntemini aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="19c01-246">Replace the `About` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseDbSet)]

<span data-ttu-id="19c01-247">LINQ deyiminden Öğrenci varlıkları kayıt tarihe göre gruplar, her grupta varlık sayısını hesaplar ve sonuçları bir koleksiyonda depolar `EnrollmentDateGroup` model nesneleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="19c01-247">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>
> [!NOTE]
> <span data-ttu-id="19c01-248">Entity Framework Core 1.0 sürümünde, sonuç kümesinin tamamı istemciye döndürülür ve gruplandırma istemcide gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="19c01-248">In the 1.0 version of Entity Framework Core, the entire result set is returned to the client, and grouping is done on the client.</span></span> <span data-ttu-id="19c01-249">Bazı senaryolarda bu performans sorunlarını oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19c01-249">In some scenarios this could create performance problems.</span></span> <span data-ttu-id="19c01-250">Veri hacimleri üretim performansını test edin ve gerekirse, ham SQL sunucu üzerinde gruplandırma yapmak için kullanın emin olun.</span><span class="sxs-lookup"><span data-stu-id="19c01-250">Be sure to test performance with production volumes of data, and if necessary use raw SQL to do the grouping on the server.</span></span> <span data-ttu-id="19c01-251">Ham SQL kullanma hakkında daha fazla bilgi için bkz: [bu serinin son öğreticide](advanced.md).</span><span class="sxs-lookup"><span data-stu-id="19c01-251">For information about how to use raw SQL, see [the last tutorial in this series](advanced.md).</span></span>

### <a name="modify-the-about-view"></a><span data-ttu-id="19c01-252">Değiştirme görünümü hakkında</span><span class="sxs-lookup"><span data-stu-id="19c01-252">Modify the About View</span></span>

<span data-ttu-id="19c01-253">Değiştirin *Views/Home/About.cshtml* dosyasındaki kodu aşağıdaki kodla:</span><span class="sxs-lookup"><span data-stu-id="19c01-253">Replace the code in the *Views/Home/About.cshtml* file with the following code:</span></span>

[!code-html[](intro/samples/cu/Views/Home/About.cshtml)]

<span data-ttu-id="19c01-254">Uygulamayı çalıştırın ve hakkında sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="19c01-254">Run the app and go to the About page.</span></span> <span data-ttu-id="19c01-255">Bir tablodaki her kayıt tarihi için Öğrenci sayısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="19c01-255">The count of students for each enrollment date is displayed in a table.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="19c01-256">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="19c01-256">Get the code</span></span>

[<span data-ttu-id="19c01-257">İndirme veya tamamlanmış uygulamanın görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="19c01-257">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="next-steps"></a><span data-ttu-id="19c01-258">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19c01-258">Next steps</span></span>

<span data-ttu-id="19c01-259">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="19c01-259">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="19c01-260">Eklenen sütun sıralama bağlantıları</span><span class="sxs-lookup"><span data-stu-id="19c01-260">Added column sort links</span></span>
> * <span data-ttu-id="19c01-261">Bir arama kutusu eklendi</span><span class="sxs-lookup"><span data-stu-id="19c01-261">Added a Search box</span></span>
> * <span data-ttu-id="19c01-262">Öğrenciler dizine eklenen disk belleği</span><span class="sxs-lookup"><span data-stu-id="19c01-262">Added paging to Students Index</span></span>
> * <span data-ttu-id="19c01-263">Dizin yönteme eklenen disk belleği</span><span class="sxs-lookup"><span data-stu-id="19c01-263">Added paging to Index method</span></span>
> * <span data-ttu-id="19c01-264">Disk belleği bağlantılar eklendi</span><span class="sxs-lookup"><span data-stu-id="19c01-264">Added paging links</span></span>
> * <span data-ttu-id="19c01-265">Hakkında bir sayfa oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="19c01-265">Created an About page</span></span>

<span data-ttu-id="19c01-266">Veri modeli değişikliklerini migrations'ı kullanarak işleme hakkında bilgi edinmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="19c01-266">Advance to the next article to learn how to handle data model changes by using migrations.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="19c01-267">Veri modeli değişikliklerini işlemek</span><span class="sxs-lookup"><span data-stu-id="19c01-267">Handle data model changes</span></span>](migrations.md)
