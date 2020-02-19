---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: Film modeli ve tablosuna yeni alan ekleme (C#) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 40b02a2f608f07091ce6b5339688a1e6290e2e37
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457472"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a><span data-ttu-id="1064e-103">Film Modeli ve Tablosuna Yeni Alan Ekleme (C#)</span><span class="sxs-lookup"><span data-stu-id="1064e-103">Adding a New Field to the Movie Model and Table (C#)</span></span>

<span data-ttu-id="1064e-104">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="1064e-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="1064e-105">[Burada](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="1064e-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="1064e-106">Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.</span><span class="sxs-lookup"><span data-stu-id="1064e-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="1064e-107">Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir.</span><span class="sxs-lookup"><span data-stu-id="1064e-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="1064e-108">Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1064e-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="1064e-109">Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="1064e-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="1064e-110">Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1064e-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="1064e-111">Visual Studio Web Developer Express SP1 önkoşulları</span><span class="sxs-lookup"><span data-stu-id="1064e-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="1064e-112">ASP.NET MVC 3 Araçlar güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="1064e-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="1064e-113">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)</span><span class="sxs-lookup"><span data-stu-id="1064e-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="1064e-114">Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="1064e-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="1064e-115">Kaynak koduna sahip bir Visual Web C# Developer projesi, bu konuyla birlikte kullanılabilecek.</span><span class="sxs-lookup"><span data-stu-id="1064e-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="1064e-116">[Sürümü C# indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="1064e-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="1064e-117">Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.</span><span class="sxs-lookup"><span data-stu-id="1064e-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="1064e-118">Bu bölümde, model sınıflarında bazı değişiklikler yapar ve veritabanı şemasını model değişiklikleriyle eşleşecek şekilde nasıl güncelleştirebileceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1064e-118">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="1064e-119">Film modeline bir derecelendirme özelliği ekleme</span><span class="sxs-lookup"><span data-stu-id="1064e-119">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="1064e-120">Yeni bir `Rating` özelliğini varolan `Movie` sınıfına ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="1064e-120">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="1064e-121">*Movie.cs* dosyasını açın ve bunun gibi `Rating` özelliğini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1064e-121">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="1064e-122">Tüm `Movie` sınıfı artık aşağıdaki kod gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="1064e-122">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

<span data-ttu-id="1064e-123">**Hata ayıkla** &gt;**Build Movie** menü komutunu kullanarak uygulamayı yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="1064e-123">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="1064e-124">Artık `Model` sınıfını güncelleştirmiş olduğunuza göre, yeni `Rating` özelliğini desteklemek için *\Views\Movies\Index.cshtml* ve *\Views\Movies\Create.cshtml* View şablonlarını da güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1064e-124">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="1064e-125">*\Views\Movies\Index.cshtml* dosyasını açın ve **Fiyat** sütununun hemen ardından `<th>Rating</th>` bir sütun başlığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1064e-125">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="1064e-126">Sonra, `@item.Rating` değerini işlemek için şablonun sonuna yakın bir `<td>` sütunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1064e-126">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="1064e-127">Güncelleştirilmiş *Index. cshtml* görünüm şablonu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="1064e-127">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

<span data-ttu-id="1064e-128">Sonra, *\Views\Movies\Create.cshtml* dosyasını açın ve formun sonuna yakın olan aşağıdaki biçimlendirmeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1064e-128">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="1064e-129">Bu, yeni bir film oluşturulduğunda bir derecelendirme belirleyebilmeniz için bir metin kutusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1064e-129">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="1064e-130">Model ve veritabanı şeması farklılıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="1064e-130">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="1064e-131">Artık uygulama kodunu yeni `Rating` özelliğini destekleyecek şekilde güncelleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="1064e-131">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="1064e-132">Şimdi uygulamayı çalıştırın ve */filmler* URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="1064e-132">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="1064e-133">Bunu yaptığınızda, aşağıdaki hatayı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="1064e-133">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="1064e-134">Bu hatayı, uygulamadaki güncelleştirilmiş `Movie` modeli sınıfı artık var olan veritabanının `Movie` tablosunun şemasından farklı olduğu için görüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="1064e-134">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="1064e-135">(Veritabanı tablosunda `Rating` sütunu yoktur.)</span><span class="sxs-lookup"><span data-stu-id="1064e-135">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="1064e-136">Varsayılan olarak, bu öğreticide yaptığınız gibi, otomatik olarak bir veritabanı oluşturmak için Entity Framework Code First kullandığınızda Code First veritabanının şemasının oluşturulduğu model sınıflarıyla eşitlenmiş olup olmadığını izlemeye yardımcı olmak üzere veritabanına tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="1064e-136">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="1064e-137">Eşitlenmiyorsa Entity Framework bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1064e-137">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="1064e-138">Bu durum, çalışma zamanında yalnızca (hataları gizleyerek) bulabileceğiniz geliştirme zamanında sorunları izlemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1064e-138">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="1064e-139">Eşitleme denetimi özelliği, yalnızca gördüğünüz hata iletisinin görüntülenmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="1064e-139">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="1064e-140">Hatayı çözmek için iki yaklaşım vardır:</span><span class="sxs-lookup"><span data-stu-id="1064e-140">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="1064e-141">Entity Framework yeni model sınıfı şemasına göre otomatik olarak veritabanını bırakıp yeniden oluşturmayı sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1064e-141">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="1064e-142">Bu yaklaşım, model ve veritabanı şemasını bir araya getirebilmenizi sağladığından bir test veritabanı üzerinde etkin geliştirme yaparken çok kullanışlı bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="1064e-142">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="1064e-143">Bunun yanında, bu yaklaşımı bir üretim veritabanında *kullanmak istemezsiniz,* ancak bu, veritabanında var olan verileri kaybetmeniz olur.</span><span class="sxs-lookup"><span data-stu-id="1064e-143">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="1064e-144">Mevcut veritabanının şemasını model sınıflarıyla eşleşecek şekilde açıkça değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1064e-144">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="1064e-145">Bu yaklaşımın avantajı, verilerinizi tutmanızı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="1064e-145">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="1064e-146">Bu değişikliği el ile ya da bir veritabanı değişiklik betiği oluşturarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1064e-146">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="1064e-147">Bu öğreticide, ilk yaklaşımı kullanacağız — Entity Framework Code First, her zaman otomatik olarak veritabanını yeniden oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1064e-147">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="1064e-148">Model değişikliklerinde veritabanını otomatik olarak yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="1064e-148">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="1064e-149">Uygulamayı, uygulama için modeli her değiştirdiğinizde Code First otomatik olarak bırakır ve yeniden oluşturacak şekilde, uygulamayı güncelleştirelim.</span><span class="sxs-lookup"><span data-stu-id="1064e-149">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1064e-150">**Uyarı** Bu yaklaşımı, veritabanını yalnızca geliştirme veya test veritabanı kullanırken ve gerçek verileri içeren bir üretim veritabanında *hiçbir zaman* otomatik olarak bırakıp yeniden oluşturmaya yönelik olarak etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1064e-150">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="1064e-151">Bunu bir üretim sunucusunda kullanmak, veri kaybına yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="1064e-151">Using it on a production server can lead to data loss.</span></span>

<span data-ttu-id="1064e-152">**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1064e-152">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="1064e-153">"Movieınitializer" sınıfını adlandırın.</span><span class="sxs-lookup"><span data-stu-id="1064e-153">Name the class "MovieInitializer".</span></span> <span data-ttu-id="1064e-154">`MovieInitializer` sınıfını aşağıdaki kodu içerecek şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="1064e-154">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="1064e-155">`MovieInitializer` sınıfı, model tarafından kullanılan veritabanının bırakılması ve model sınıfları değiştiğinde otomatik olarak yeniden oluşturulması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1064e-155">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="1064e-156">Kod, veritabanında oluşturulduğu zaman (veya yeniden oluşturulduğunda) otomatik olarak veritabanına eklenecek bazı varsayılan verileri belirtmek için bir `Seed` yöntemi içerir.</span><span class="sxs-lookup"><span data-stu-id="1064e-156">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="1064e-157">Bu, bir model değişikliğini her seferinde el ile doldurmanıza gerek kalmadan veritabanını bazı örnek verilerle doldurmak için kullanışlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="1064e-157">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="1064e-158">`MovieInitializer` sınıfını tanımladığınıza göre, uygulama her çalıştığında model sınıflarının veritabanındaki şemadan farklı olup olmadığını kontrol etmek için bu şekilde bağlantı kurmak isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1064e-158">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="1064e-159">Bunlar ise, bir veritabanını modeliyle eşleşecek şekilde yeniden oluşturmak ve ardından veritabanını örnek verilerle doldurmak için başlatıcıyı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1064e-159">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="1064e-160">`MvcMovies` projesinin kökündeki *Global. asax* dosyasını açın:</span><span class="sxs-lookup"><span data-stu-id="1064e-160">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

<span data-ttu-id="1064e-161">*Global. asax* dosyası, proje için tüm uygulamayı tanımlayan sınıfı içerir ve uygulama ilk kez başladığında çalışan bir `Application_Start` olay işleyicisi içerir.</span><span class="sxs-lookup"><span data-stu-id="1064e-161">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="1064e-162">Şimdi dosyanın en üstüne iki using ifadesi ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="1064e-162">Let's add two using statements to the top of the file.</span></span> <span data-ttu-id="1064e-163">İlki Entity Framework ad alanına başvurur ve ikincisi `MovieInitializer` sınıfımızın yaşadığı ad alanına başvurur:</span><span class="sxs-lookup"><span data-stu-id="1064e-163">The first references the Entity Framework namespace, and the second references the namespace where our `MovieInitializer` class lives:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

<span data-ttu-id="1064e-164">Ardından, aşağıdaki gibi `Application_Start` yöntemini bulun ve yönteminin başına `Database.SetInitializer` bir çağrı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1064e-164">Then find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

<span data-ttu-id="1064e-165">Az önce eklediğiniz `Database.SetInitializer` deyimin şeması ve veritabanı eşleşmezse, `MovieDBContext` örneği tarafından kullanılan veritabanının otomatik olarak silinip yeniden oluşturulması gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1064e-165">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="1064e-166">Gördüğünüz gibi, veritabanını `MovieInitializer` sınıfında belirtilen örnek verilerle de dolduracaktır.</span><span class="sxs-lookup"><span data-stu-id="1064e-166">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="1064e-167">*Global. asax* dosyasını kapatın.</span><span class="sxs-lookup"><span data-stu-id="1064e-167">Close the *Global.asax* file.</span></span>

<span data-ttu-id="1064e-168">Uygulamayı yeniden çalıştırın ve */filmler* URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="1064e-168">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="1064e-169">Uygulama başlatıldığında, model yapısının artık veritabanı şemasıyla eşleşmediğini algılar.</span><span class="sxs-lookup"><span data-stu-id="1064e-169">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="1064e-170">Yeni model yapısıyla eşleşecek şekilde veritabanını otomatik olarak yeniden oluşturur ve veritabanını örnek filmlerle doldurur:</span><span class="sxs-lookup"><span data-stu-id="1064e-170">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

<span data-ttu-id="1064e-172">Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1064e-172">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="1064e-173">Bir derecelendirme ekleyebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1064e-173">Note that you can add a rating.</span></span>

<span data-ttu-id="1064e-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="1064e-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span></span>

<span data-ttu-id="1064e-175">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1064e-175">Click **Create**.</span></span> <span data-ttu-id="1064e-176">Yeni film, derecelendirme de dahil, artık filmler listesinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="1064e-176">The new movie, including the rating, now shows up in the movies listing:</span></span>

<span data-ttu-id="1064e-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="1064e-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span></span>

<span data-ttu-id="1064e-178">Bu bölümde, model nesnelerini nasıl değiştirebileceğiniz ve veritabanını değişikliklerle eşitlenmiş halde tutan bir şekilde gördünüz.</span><span class="sxs-lookup"><span data-stu-id="1064e-178">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="1064e-179">Ayrıca, senaryoları deneyebilmeniz için yeni oluşturulan bir veritabanını örnek verilerle doldurmanın bir yolunu öğrenmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="1064e-179">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="1064e-180">Daha sonra model sınıflarına daha zengin doğrulama mantığı ekleme ve bazı iş kurallarının uygulanmasını sağlama konusuna bakalım.</span><span class="sxs-lookup"><span data-stu-id="1064e-180">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1064e-181">[Önceki](examining-the-edit-methods-and-edit-view.md)
> [İleri](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="1064e-181">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
