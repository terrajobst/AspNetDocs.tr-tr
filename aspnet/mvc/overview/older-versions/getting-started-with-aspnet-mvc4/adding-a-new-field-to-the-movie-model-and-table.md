---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: Film modeli ve tablosuna yeni alan ekleme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457706"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a><span data-ttu-id="ea3d1-104">Film Modeli ve Tablosuna Yeni Alan Ekleme</span><span class="sxs-lookup"><span data-stu-id="ea3d1-104">Adding a New Field to the Movie Model and Table</span></span>

<span data-ttu-id="ea3d1-105">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="ea3d1-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="ea3d1-106">[Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="ea3d1-107">Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="ea3d1-108">Bu bölümde, değişikliğin veritabanına uygulanması için model sınıflarında bazı değişiklikleri geçirmek üzere Entity Framework Code First Migrations kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-108">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="ea3d1-109">Varsayılan olarak, bu öğreticide yaptığınız gibi, otomatik olarak bir veritabanı oluşturmak için Entity Framework Code First kullandığınızda Code First veritabanının şemasının oluşturulduğu model sınıflarıyla eşitlenmiş olup olmadığını izlemeye yardımcı olmak üzere veritabanına tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-109">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="ea3d1-110">Eşitlenmiyorsa Entity Framework bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-110">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="ea3d1-111">Bu durum, çalışma zamanında yalnızca (hataları gizleyerek) bulabileceğiniz geliştirme zamanında sorunları izlemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-111">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="ea3d1-112">Model değişiklikleri için Code First Migrations ayarlama</span><span class="sxs-lookup"><span data-stu-id="ea3d1-112">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="ea3d1-113">Visual Studio 2012 kullanıyorsanız, veritabanı aracını açmak için Çözüm Gezgini *film. mdf* dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-113">If you are using Visual Studio 2012, double click the *Movies.mdf* file from Solution Explorer to open the database tool.</span></span> <span data-ttu-id="ea3d1-114">Web için Visual Studio Express Veritabanı Gezgini gösterir, Visual Studio 2012 Sunucu Gezgini gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-114">Visual Studio Express for Web will show Database Explorer, Visual Studio 2012 will show Server Explorer.</span></span> <span data-ttu-id="ea3d1-115">Visual Studio 2010 kullanıyorsanız SQL Server Nesne Gezgini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-115">If you are using Visual Studio 2010, use SQL Server Object Explorer.</span></span>

<span data-ttu-id="ea3d1-116">Veritabanı aracında (Veritabanı Gezgini, Sunucu Gezgini veya SQL Server Nesne Gezgini), filmler veritabanını bırakmak için `MovieDBContext` ' a sağ tıklayın ve **Sil** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-116">In the database tool (Database Explorer, Server Explorer or SQL Server Object Explorer), right click on `MovieDBContext` and select **Delete** to drop the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

<span data-ttu-id="ea3d1-117">Çözüm Gezgini için geri gidin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-117">Navigate back to Solution Explorer.</span></span> <span data-ttu-id="ea3d1-118">Filmler veritabanını kaldırmak için *filmler. mdf* dosyasına sağ tıklayın ve **Sil** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-118">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

<span data-ttu-id="ea3d1-119">Hata olmadığından emin olmak için uygulamayı derleyin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-119">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="ea3d1-120">**Araçlar** menüsünden **NuGet Paket Yöneticisi**’ne ve ardından **Paket Yöneticisi Konsolu**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-120">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![Paket Man 'ı Ekle](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

<span data-ttu-id="ea3d1-122">`PM>` isteminde **Paket Yöneticisi konsolu** penceresinde "Enable-geçişler-ContextTypeName MvcMovie. modeller. MovieDBContext" yazın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-122">In the **Package Manager Console** window at the `PM>` prompt enter "Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext".</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

<span data-ttu-id="ea3d1-123">**Enable-geçişler** komutu (yukarıda gösterilmiştir) yeni bir *geçişler* klasöründe bir *Configuration.cs* dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-123">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

<span data-ttu-id="ea3d1-124">Visual Studio, *Configuration.cs* dosyasını açar.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-124">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="ea3d1-125">*Configuration.cs* dosyasındaki `Seed` yöntemini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-125">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

<span data-ttu-id="ea3d1-126">`Movie` altındaki kırmızı dalgalı çizgiye sağ tıklayın ve ardından **mvcmovie. modeller** **kullanarak** **Çözümle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-126">Right click on the red squiggly line under `Movie` and select **Resolve** then **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

<span data-ttu-id="ea3d1-127">Bunun yapılması Aşağıdaki using ifadesini ekler:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-127">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="ea3d1-128">Code First Migrations her geçişten sonra `Seed` yöntemini çağırır (yani, Paket Yöneticisi konsolundaki **Update-Database** ' i çağırarak) ve bu yöntem önceden eklenmiş satırları güncelleştirir veya henüz yoksa onları ekler.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-128">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>

<span data-ttu-id="ea3d1-129">**Projeyi derlemek IÇIN CTRL-SHIFT-B tuşlarına basın.** (Bu noktada derlenmezseniz aşağıdaki adımlar başarısız olur.)</span><span class="sxs-lookup"><span data-stu-id="ea3d1-129">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if your don't build at this point.)</span></span>

<span data-ttu-id="ea3d1-130">Sonraki adım, ilk geçiş için bir `DbMigration` sınıfı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-130">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="ea3d1-131">Bu geçiş, yeni bir veritabanı oluşturur. bu nedenle, önceki bir adımda bulunan *Movie. mdf* dosyasını silmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-131">This migration to creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="ea3d1-132">**Paket Yöneticisi konsolu** penceresinde, ilk geçişi oluşturmak için "Add-geçiş Initial" komutunu girin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-132">In the **Package Manager Console** window, enter the command "add-migration Initial" to create the initial migration.</span></span> <span data-ttu-id="ea3d1-133">"Initial" adı rasgele olur ve oluşturulan geçiş dosyasını adlandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-133">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

<span data-ttu-id="ea3d1-134">Code First Migrations, *geçişler* klasöründe başka bir sınıf dosyası oluşturur ( *{datestamp}\_Initial.cs* ) ve bu sınıf veritabanı şemasını oluşturan kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-134">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="ea3d1-135">Geçiş dosya adı, sıralamaya yardımcı olması için zaman damgasıyla önceden düzeltilir.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-135">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="ea3d1-136">*{DateStamp}\_Initial.cs* dosyasını Inceleyin, film DB için film tablosu oluşturma yönergelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-136">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the Movies table for the Movie DB.</span></span> <span data-ttu-id="ea3d1-137">Aşağıdaki yönergelerdeki veritabanını güncelleştirdiğinizde, bu *{dateStamp}\_Initial.cs* dosyası ÇALıŞACAKTıR ve DB şemasını oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-137">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="ea3d1-138">Ardından, VERITABANıNı test verileriyle doldurmak için **çekirdek** yöntemi çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-138">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="ea3d1-139">**Paket Yöneticisi konsolunda**, veritabanını oluşturmak ve **çekirdek** yöntemini çalıştırmak için "Update-Database" komutunu girin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-139">In the **Package Manager Console**, enter the command "update-database" to create the database and run the **Seed** method.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

<span data-ttu-id="ea3d1-140">Bir tablonun zaten var olduğunu ve oluşturulamayabileceğini belirten bir hata alırsanız, veritabanını sildikten sonra ve `update-database`çalıştırmadan önce uygulamayı çalıştırmanızdan kaynaklanıyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-140">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="ea3d1-141">Bu durumda, *filmler. mdf* dosyasını yeniden silin ve `update-database` komutunu yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-141">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="ea3d1-142">Yine de bir hata alırsanız, geçişler klasörünü ve içeriğini silin ve ardından bu sayfanın üst kısmındaki yönergelerden başlayın (yani, *filmler. mdf* dosyasını silin ve ardından geçişlere devam edin).</span><span class="sxs-lookup"><span data-stu-id="ea3d1-142">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span>

<span data-ttu-id="ea3d1-143">Uygulamayı çalıştırın ve */filmler* URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-143">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="ea3d1-144">Çekirdek veriler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-144">The seed data is displayed.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="ea3d1-145">Film modeline bir derecelendirme özelliği ekleme</span><span class="sxs-lookup"><span data-stu-id="ea3d1-145">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="ea3d1-146">Yeni bir `Rating` özelliğini varolan `Movie` sınıfına ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-146">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="ea3d1-147">*Models\movie.cs* dosyasını açın ve bunun gibi `Rating` özelliğini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-147">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

<span data-ttu-id="ea3d1-148">Tüm `Movie` sınıfı artık aşağıdaki kod gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-148">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

<span data-ttu-id="ea3d1-149">**Derlemeyi** &gt;**Build filmi** oluştur menü komutunu kullanarak veya CTRL-SHIFT-B tuşlarına basarak uygulamayı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-149">Build the application using the **Build** &gt;**Build Movie** menu command or by pressing CTRL-SHIFT-B.</span></span>

<span data-ttu-id="ea3d1-150">Artık `Model` sınıfını güncelleştirmiş olduğunuza göre, yeni `Rating` özelliğini tarayıcı görünümünde görüntülemek için *\Views\Movies\Index.cshtml* ve *\Views\Movies\Create.cshtml* View şablonlarını da güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-150">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to display the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="ea3d1-151"><em>\Views\Movies\Index.cshtml</em> dosyasını açın ve <strong>Fiyat</strong> sütununun hemen ardından `<th>Rating</th>` bir sütun başlığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-151">Open the<em>\Views\Movies\Index.cshtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="ea3d1-152">Sonra, `@item.Rating` değerini işlemek için şablonun sonuna yakın bir `<td>` sütunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-152">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="ea3d1-153">Güncelleştirilmiş <em>Index. cshtml</em> görünüm şablonu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-153">Below is what the updated <em>Index.cshtml</em> view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

<span data-ttu-id="ea3d1-154">Sonra, *\Views\Movies\Create.cshtml* dosyasını açın ve formun sonuna yakın olan aşağıdaki biçimlendirmeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-154">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="ea3d1-155">Bu, yeni bir film oluşturulduğunda bir derecelendirme belirleyebilmeniz için bir metin kutusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-155">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

<span data-ttu-id="ea3d1-156">Artık uygulama kodunu yeni `Rating` özelliğini destekleyecek şekilde güncelleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-156">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="ea3d1-157">Şimdi uygulamayı çalıştırın ve */filmler* URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-157">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="ea3d1-158">Bunu yaptığınızda, aşağıdaki hatalardan birini görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-158">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

<span data-ttu-id="ea3d1-159">Bu hatayı, uygulamadaki güncelleştirilmiş `Movie` modeli sınıfı artık var olan veritabanının `Movie` tablosunun şemasından farklı olduğu için görüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-159">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="ea3d1-160">(Veritabanı tablosunda `Rating` sütunu yoktur.)</span><span class="sxs-lookup"><span data-stu-id="ea3d1-160">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="ea3d1-161">Hatayı çözmek için birkaç yaklaşım vardır:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-161">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="ea3d1-162">Entity Framework yeni model sınıfı şemasına göre otomatik olarak veritabanını bırakıp yeniden oluşturmayı sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-162">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="ea3d1-163">Bu yaklaşım, bir test veritabanı üzerinde etkin geliştirme yaparken çok kullanışlıdır; modeli ve veritabanı şemasını birlikte hızla gelişmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-163">This approach is very convenient when doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="ea3d1-164">Bunun yanında, bu yaklaşımı bir üretim veritabanında *kullanmak istemezsiniz,* ancak bu, veritabanında var olan verileri kaybetmeniz olur.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-164">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="ea3d1-165">Bir veritabanının test verileriyle otomatik olarak çekirdeği oluşturmak için bir başlatıcı kullanılması, genellikle bir uygulama geliştirmenin üretken bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-165">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="ea3d1-166">Entity Framework veritabanı başlatıcıları hakkında daha fazla bilgi için bkz. Tom Dykstra 's [ASP.NET MVC/Entity Framework öğreticisi](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="ea3d1-166">For more information on Entity Framework database initializers, see Tom Dykstra's [ASP.NET MVC/Entity Framework tutorial](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="ea3d1-167">Mevcut veritabanının şemasını model sınıflarıyla eşleşecek şekilde açıkça değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-167">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="ea3d1-168">Bu yaklaşımın avantajı, verilerinizi tutmanızı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-168">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="ea3d1-169">Bu değişikliği el ile ya da bir veritabanı değişiklik betiği oluşturarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-169">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="ea3d1-170">Veritabanı şemasını güncelleştirmek için Code First Migrations kullanın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-170">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="ea3d1-171">Bu öğretici için Code First Migrations kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-171">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="ea3d1-172">Çekirdek yöntemini yeni sütun için bir değer sağlayacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-172">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="ea3d1-173">Migrations\Configuration.cs dosyasını açın ve her bir film nesnesine bir derecelendirme alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-173">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

<span data-ttu-id="ea3d1-174">Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın ve aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-174">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration AddRatingMig`

<span data-ttu-id="ea3d1-175">`add-migration` komutu, geçiş çerçevesinin geçerli film modelini geçerli film DB şemasıyla incelemesini ve VERITABANıNı yeni modele geçirmek için gerekli kodu oluşturmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-175">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="ea3d1-176">Addrampamig rastgele ve geçiş dosyasını adlandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-176">The AddRatingMig is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="ea3d1-177">Geçiş adımı için anlamlı bir ad kullanılması yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-177">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="ea3d1-178">Bu komut tamamlandığında, Visual Studio yeni `DbMigration` türetilen sınıfı tanımlayan sınıf dosyasını açar ve `Up` yönteminde yeni sütunu oluşturan kodu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-178">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

<span data-ttu-id="ea3d1-179">Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresinde "Güncelleştir-veritabanı" komutunu girin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-179">Build the solution, and then enter the "update-database" command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="ea3d1-180">Aşağıdaki görüntüde, **Paket Yöneticisi konsol** penceresinde çıkış gösterilmektedir (ön bekleyen Addesmig tarih damgası farklı olacaktır.)</span><span class="sxs-lookup"><span data-stu-id="ea3d1-180">The following image shows the output in the **Package Manager Console** window (The date stamp prepending AddRatingMig will be different.)</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

<span data-ttu-id="ea3d1-181">Uygulamayı yeniden çalıştırın ve/filmler URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-181">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="ea3d1-182">Yeni derecelendirme alanını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-182">You can see the new Rating field.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

<span data-ttu-id="ea3d1-183">Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-183">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="ea3d1-184">Bir derecelendirme ekleyebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-184">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

<span data-ttu-id="ea3d1-186">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-186">Click **Create**.</span></span> <span data-ttu-id="ea3d1-187">Yeni film, derecelendirme de dahil, artık filmler listesinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="ea3d1-187">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

<span data-ttu-id="ea3d1-189">Ayrıca, düzenleme, Ayrıntılar ve Searchındex görünüm şablonlarına `Rating` alanını da eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-189">You should also add the `Rating` field to the Edit, Details and SearchIndex view templates.</span></span>

<span data-ttu-id="ea3d1-190">**Paket Yöneticisi konsol** penceresinde "Güncelleştir-veritabanı" komutunu tekrar girebilir ve şema modelle eşleştiğinden hiçbir değişiklik yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-190">You could enter the "update-database" command in the **Package Manager Console** window again and no changes would be made, because the schema matches the model.</span></span>

<span data-ttu-id="ea3d1-191">Bu bölümde, model nesnelerini nasıl değiştirebileceğiniz ve veritabanını değişikliklerle eşitlenmiş halde tutan bir şekilde gördünüz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-191">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="ea3d1-192">Ayrıca, senaryoları deneyebilmeniz için yeni oluşturulan bir veritabanını örnek verilerle doldurmanın bir yolunu öğrenmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-192">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="ea3d1-193">Daha sonra model sınıflarına daha zengin doğrulama mantığı ekleme ve bazı iş kurallarının uygulanmasını sağlama konusuna bakalım.</span><span class="sxs-lookup"><span data-stu-id="ea3d1-193">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ea3d1-194">[Önceki](examining-the-edit-methods-and-edit-view.md)
> [İleri](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="ea3d1-194">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
