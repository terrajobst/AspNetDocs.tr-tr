---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: Bir denetleyiciden modelinizin verilerine erişme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456172"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="a4d95-104">Bir Denetleyiciden Modelinizin Verilerine Erişme</span><span class="sxs-lookup"><span data-stu-id="a4d95-104">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="a4d95-105">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="a4d95-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="a4d95-106">[Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="a4d95-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="a4d95-107">Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="a4d95-108">Bu bölümde, yeni bir `MoviesController` sınıfı oluşturacak ve film verilerini alan ve bir görünüm şablonu kullanarak tarayıcıda görüntüleyen kodu yazılacak.</span><span class="sxs-lookup"><span data-stu-id="a4d95-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="a4d95-109">Sonraki adıma geçmeden önce **uygulamayı derleyin** .</span><span class="sxs-lookup"><span data-stu-id="a4d95-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="a4d95-110">*Denetleyiciler* klasörüne sağ tıklayın ve yeni bir `MoviesController` denetleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4d95-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="a4d95-111">Aşağıdaki seçenekler, uygulamanızı derlene kadar görünmez.</span><span class="sxs-lookup"><span data-stu-id="a4d95-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="a4d95-112">Aşağıdaki seçenekleri belirleyin:</span><span class="sxs-lookup"><span data-stu-id="a4d95-112">Select the following options:</span></span>

- <span data-ttu-id="a4d95-113">Denetleyici adı: **MoviesController**.</span><span class="sxs-lookup"><span data-stu-id="a4d95-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="a4d95-114">(Bu varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a4d95-114">(This is the default.</span></span> <span data-ttu-id="a4d95-115">)</span><span class="sxs-lookup"><span data-stu-id="a4d95-115">)</span></span>
- <span data-ttu-id="a4d95-116">Şablon: **Entity Framework kullanarak okuma/yazma eylemleri ve görünümleri olan MVC denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="a4d95-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="a4d95-117">Model Sınıfı: **Film (MvcMovie. modeller)** .</span><span class="sxs-lookup"><span data-stu-id="a4d95-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="a4d95-118">Veri bağlamı sınıfı: **Moviedbcontext (MvcMovie. modeller)** .</span><span class="sxs-lookup"><span data-stu-id="a4d95-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="a4d95-119">Görünümler: **Razor (cshtml)** .</span><span class="sxs-lookup"><span data-stu-id="a4d95-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="a4d95-120">(Varsayılan.)</span><span class="sxs-lookup"><span data-stu-id="a4d95-120">(The default.)</span></span>

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="a4d95-122">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4d95-122">Click **Add**.</span></span> <span data-ttu-id="a4d95-123">Visual Studio Express aşağıdaki dosya ve klasörleri oluşturur:</span><span class="sxs-lookup"><span data-stu-id="a4d95-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="a4d95-124">Projenin *Controllers* klasöründeki *bir MoviesController.cs* dosyası.</span><span class="sxs-lookup"><span data-stu-id="a4d95-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="a4d95-125">Projenin *Görünümler* klasöründeki *filmler* klasörü.</span><span class="sxs-lookup"><span data-stu-id="a4d95-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="a4d95-126">Yeni *Views\filmlerini* klasöründeki *. cshtml, delete. cshtml, details. cshtml, Edit. cshtml*ve *Index. cshtml* oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4d95-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="a4d95-127">ASP.NET MVC 4, sizin için CRUD (oluşturma, okuma, güncelleştirme ve silme) eylem yöntemlerini ve görünümlerini otomatik olarak oluşturdu (CRUD eylem yöntemlerinin ve görünümlerinin otomatik olarak oluşturulması yapı iskelesi olarak bilinir).</span><span class="sxs-lookup"><span data-stu-id="a4d95-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="a4d95-128">Artık, film girişleri oluşturmanızı, listelemenizi, düzenlemenizi ve silmenizi sağlayan tam işlevli bir Web uygulamanız vardır.</span><span class="sxs-lookup"><span data-stu-id="a4d95-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="a4d95-129">Uygulamayı çalıştırın ve tarayıcınızın adres çubuğundaki URL 'ye */filmler* ekleyerek `Movies` denetleyiciye gidin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="a4d95-130">Uygulama varsayılan yönlendirmeye bağlı olduğundan ( *Global. asax* dosyasında tanımlı), tarayıcı isteği `http://localhost:xxxxx/Movies`, `Movies` denetleyicisinin varsayılan `Index` eylem yöntemine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="a4d95-131">Diğer bir deyişle, tarayıcı istek `http://localhost:xxxxx/Movies` `http://localhost:xxxxx/Movies/Index`tarayıcı isteğiyle aynı şekilde aynıdır.</span><span class="sxs-lookup"><span data-stu-id="a4d95-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="a4d95-132">Henüz hiç eklemediğiniz için sonuç, filmlerin boş bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="a4d95-133">Film oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4d95-133">Creating a Movie</span></span>

<span data-ttu-id="a4d95-134">**Yeni oluştur** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-134">Select the **Create New** link.</span></span> <span data-ttu-id="a4d95-135">Bir film hakkındaki ayrıntıları girin ve ardından **Oluştur** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4d95-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="a4d95-136">**Oluştur** düğmesine tıkladığınızda form, film bilgilerinin veritabanına kaydedildiği sunucuya gönderilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4d95-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="a4d95-137">Daha sonra, yeni oluşturulan filmi listede görebileceğiniz */filmler* URL 'sine yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d95-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="a4d95-138">![Indexwhenharrymet](accessing-your-models-data-from-a-controller/_static/image4.png "Indexwhenharrymet")</span><span class="sxs-lookup"><span data-stu-id="a4d95-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="a4d95-139">Birkaç film girişi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4d95-139">Create a couple more movie entries.</span></span> <span data-ttu-id="a4d95-140">Tüm işlevsel olan **düzenleme**, **Ayrıntılar**ve **silme** bağlantılarını deneyin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="a4d95-141">Oluşturulan kodu İnceleme</span><span class="sxs-lookup"><span data-stu-id="a4d95-141">Examining the Generated Code</span></span>

<span data-ttu-id="a4d95-142">*Controllers\MoviesController.cs* dosyasını açın ve oluşturulan `Index` yöntemini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="a4d95-143">`Index` yöntemi ile birlikte film denetleyicisi 'nin bir bölümü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="a4d95-144">`MoviesController` sınıfından aşağıdaki satır, daha önce açıklandığı gibi bir film veritabanı bağlamını başlatır.</span><span class="sxs-lookup"><span data-stu-id="a4d95-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="a4d95-145">Film veritabanı bağlamını kullanarak filmleri sorgulayabilir, düzenleyebilir ve silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d95-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="a4d95-146">`Movies` denetleyicisine yapılan bir istek, film veritabanının `Movies` tablosundaki tüm girişleri döndürür ve sonra sonuçları `Index` görünümüne geçirir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="a4d95-147">Türü kesin belirlenmiş modeller ve @model anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="a4d95-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="a4d95-148">Bu öğreticide daha önce, bir denetleyicinin `ViewBag` nesnesini kullanarak bir görünüm şablonuna nasıl veri veya nesne geçirekullanabileceğinizi gördünüz.</span><span class="sxs-lookup"><span data-stu-id="a4d95-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="a4d95-149">`ViewBag`, bir görünüme bilgi geçirmek için uygun, geç bağlanan bir yol sağlayan dinamik bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="a4d95-150">ASP.NET MVC, kesin olarak belirlenmiş verileri veya nesneleri bir görünüm şablonuna geçirme özelliği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4d95-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="a4d95-151">Bu kesin türü belirtilmiş yaklaşım, Visual Studio düzenleyicisinde kodunuzun ve daha zengin IntelliSense 'in derleme zamanı denetimini daha iyi bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="a4d95-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="a4d95-152">Visual Studio 'daki scafkatlama mekanizması, `MoviesController` sınıfıyla bu yaklaşımı kullandı ve yöntem ve görünümleri oluştururken şablonları görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="a4d95-153">*Controllers\MoviesController.cs* dosyasında, oluşturulan `Details` yöntemini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="a4d95-154">`Details` yöntemi ile birlikte film denetleyicisi 'nin bir bölümü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="a4d95-155">Bir `Movie` bulunursa, Ayrıntılar görünümüne `Movie` modelinin bir örneği geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="a4d95-156">*Views\Movies\Details.cshtml* dosyasının içeriğini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="a4d95-157">Görünüm şablonu dosyasının üst kısmına bir `@model` ifadesini ekleyerek, görünümün beklediği nesne türünü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d95-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="a4d95-158">Film denetleyicisini oluştururken, Visual Studio *details. cshtml* dosyasının en üstüne aşağıdaki `@model` ifadesini otomatik olarak dahil edin:</span><span class="sxs-lookup"><span data-stu-id="a4d95-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="a4d95-159">Bu `@model` yönergesi, kesin olarak belirlenmiş bir `Model` nesnesi kullanarak denetleyicinin görünüme geçirildiği filme erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4d95-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="a4d95-160">Örneğin, *details. cshtml* şablonunda, kod her bir film alanını `DisplayNameFor` geçirir ve türü kesin belirlenmiş `Model` nesnesi olan HTML Yardımcıları [için Display.](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx)</span><span class="sxs-lookup"><span data-stu-id="a4d95-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="a4d95-161">Oluşturma ve düzenleme yöntemleri ve Görünüm şablonları da bir film modeli nesnesi iletir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="a4d95-162">*Index. cshtml* görünüm şablonunu ve *MoviesController.cs* dosyasındaki `Index` yöntemini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="a4d95-163">[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) , `Index` eylem yönteminde `View` Helper metodunu çağırdığında kodun bir nesne nasıl oluşturduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d95-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="a4d95-164">Kod daha sonra bu `Movies` listesini denetleyiciden görünüme geçirir:</span><span class="sxs-lookup"><span data-stu-id="a4d95-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="a4d95-165">Film denetleyicisini oluştururken, Visual Studio Express *Index. cshtml* dosyasının en üstüne aşağıdaki `@model` ifadesini otomatik olarak dahil edin:</span><span class="sxs-lookup"><span data-stu-id="a4d95-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="a4d95-166">Bu `@model` yönergesi, kesin olarak belirlenmiş bir `Model` nesnesi kullanarak denetleyicinin görünüme geçirildiği film listesine erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4d95-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="a4d95-167">Örneğin, *Index. cshtml* şablonunda kod, türü kesin belirlenmiş `Model` nesnesi üzerinde `foreach` bir bildiri gerçekleştirerek filmlerde döngü yapılır:</span><span class="sxs-lookup"><span data-stu-id="a4d95-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="a4d95-168">`Model` nesne kesin olarak yazıldığı için (bir `IEnumerable<Movie>` nesnesi olarak), döngüdeki her bir `item` nesnesi `Movie`olarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="a4d95-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="a4d95-169">Diğer avantajlar arasında bu, kod Düzenleyicisi 'nde kodun derleme zamanı denetimini ve tam IntelliSense desteğini elde ettiğiniz anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="a4d95-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="a4d95-171">SQL Server LocalDB ile çalışma</span><span class="sxs-lookup"><span data-stu-id="a4d95-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="a4d95-172">Entity Framework Code First, belirtilen veritabanı bağlantı dizesinin henüz mevcut olmayan bir `Movies` veritabanına işaret ettiği algılandı, bu nedenle veritabanını otomatik olarak oluşturdu Code First.</span><span class="sxs-lookup"><span data-stu-id="a4d95-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="a4d95-173">Uygulamasının oluşturulduğunu, *uygulama\_veri* klasörüne bakarak doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d95-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="a4d95-174">*Filmler. mdf* dosyasını görmüyorsanız, **Çözüm Gezgini** araç çubuğunda **tüm dosyaları göster** düğmesine tıklayın, **Yenile** düğmesine tıklayın ve ardından *uygulama\_verileri* klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="a4d95-175">*Film. mdf* ' ye çift TıKLAYARAK **veritabanı Gezginini**açın ve ardından Filmler tablosunu görmek için **Tablolar** klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="a4d95-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="a4d95-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="a4d95-177">Veritabanı Gezgini görünmezse, **Araçlar** menüsünde **veritabanına Bağlan**' ı seçin ve ardından **veri kaynağı seç** iletişim kutusunu iptal edin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="a4d95-178">Bu, veritabanı Gezginini açmaya zorlanır.</span><span class="sxs-lookup"><span data-stu-id="a4d95-178">This will force open the database explorer.</span></span>

> [!NOTE]
> <span data-ttu-id="a4d95-179">VWD veya Visual Studio 2010 kullanıyorsanız ve aşağıdakilerden birine benzer bir hata alırsanız:</span><span class="sxs-lookup"><span data-stu-id="a4d95-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="a4d95-180">' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES. veritabanı Sürüm 706 olduğundan, MDF açılamıyor.</span><span class="sxs-lookup"><span data-stu-id="a4d95-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="a4d95-181">Bu sunucu sürüm 655 ve öncesini destekler.</span><span class="sxs-lookup"><span data-stu-id="a4d95-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="a4d95-182">Düşürme yolu desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a4d95-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="a4d95-183">&quot;InvalidOperation özel durumu, Kullanıcı kodu tarafından yakalanmıştı&quot; sağlanan SqlConnection bir ilk katalog belirtmiyor.</span><span class="sxs-lookup"><span data-stu-id="a4d95-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="a4d95-184">[SQL Server veri araçları](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) ve [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)'yi yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4d95-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="a4d95-185">Önceki sayfada belirtilen `MovieDBContext` bağlantı dizesini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a4d95-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>

<span data-ttu-id="a4d95-186">`Movies` tabloya sağ tıklayıp **tablo verilerini göster** ' i seçerek oluşturduğunuz verileri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="a4d95-187">`Movies` tabloya sağ tıklayıp **tablo tanımını aç** ' ı seçerek Entity Framework Code First sizin için oluşturduğu tablo yapısını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="a4d95-188">`Movies` tablosu şemasının, daha önce oluşturduğunuz `Movie` sınıfa nasıl eşlendiğini fark edin.</span><span class="sxs-lookup"><span data-stu-id="a4d95-188">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="a4d95-189">Entity Framework Code First, bu şemayı `Movie` sınıfınızı temel alarak sizin için otomatik olarak oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="a4d95-189">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="a4d95-190">İşiniz bittiğinde, *Moviedbcontext* ' i sağ tıklatıp **Bağlantıyı kapat**' ı seçerek bağlantıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="a4d95-190">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="a4d95-191">(Bağlantıyı kapatmazsanız, projeyi bir sonraki çalıştırışınızda bir hata alabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="a4d95-191">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

<span data-ttu-id="a4d95-192">Artık veritabanını ve bir basit liste sayfasını, içeriği görüntüleme sayfasına sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d95-192">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="a4d95-193">Sonraki öğreticide, iskele eklenen kodun geri kalanını inceleyeceğiz ve bu veritabanında film aramanızı sağlayan bir `SearchIndex` yöntemi ve bir `SearchIndex` görünümü ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="a4d95-193">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a4d95-194">[Önceki](adding-a-model.md)
> [İleri](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="a4d95-194">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
