---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: Bir denetleyiciden modelinizin verilerine erişme | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543752"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="04721-104">Bir Denetleyiciden Modelinizin Verilerine Erişme</span><span class="sxs-lookup"><span data-stu-id="04721-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="04721-105">[Scott Hanselman](https://github.com/shanselman) tarafından</span><span class="sxs-lookup"><span data-stu-id="04721-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="04721-106">Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir.</span><span class="sxs-lookup"><span data-stu-id="04721-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="04721-107">Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="04721-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="04721-108">Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="04721-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="04721-109">Bu bölümde yeni bir MoviesController sınıfı oluşturacağız ve film verilerimizi alan ve bir görünüm şablonu kullanarak tarayıcıya geri görüntüleyen bir kod yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="04721-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="04721-110">Denetleyiciler klasörüne sağ tıklayın ve yeni bir MoviesController oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04721-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="04721-111">[![denetleyicisi ekleme](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="04721-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="04721-112">Bu işlem, projemizdeki \Controllers klasörü altında yeni bir "MoviesController.cs" dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04721-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="04721-113">Yeni doldurulan veritabanımızdan film listesini almak için MovieController 'ı güncelleştirelim.</span><span class="sxs-lookup"><span data-stu-id="04721-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="04721-114">Yalnızca 1984 Yaz 'dan sonra yayınlanan filmleri alabilmesi için bir LINQ sorgusu yaptık.</span><span class="sxs-lookup"><span data-stu-id="04721-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="04721-115">Bu film listesini geri işlemek için bir görünüm şablonu gerekecektir, bu yüzden yöntemi sağ tıklayıp oluşturmak için Görünüm Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="04721-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="04721-116">Görünüm Ekle iletişim kutusunda, film&lt;bir liste geçirdiğimiz, görünüm şablonumuza film&gt;.</span><span class="sxs-lookup"><span data-stu-id="04721-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="04721-117">Önceki sürelerden farklı olarak, Görünüm Ekle iletişim kutusunu kullandık ve "boş" bir şablon oluşturmayı tercih ediyoruz. bu kez, Visual Studio 'Nun bazı varsayılan içeriklerle ilgili bir görünüm şablonunu sizin için otomatik olarak "scafkatmayı" istediğini belirteceğiz.</span><span class="sxs-lookup"><span data-stu-id="04721-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="04721-118">"İçerik görüntüle açılan menüsünden" liste "öğesini seçerek bunu yapacağız.</span><span class="sxs-lookup"><span data-stu-id="04721-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="04721-119">Yeni bir sınıf oluşturduğunuz zaman, Görünüm Ekle Iletişim kutusunda görünmesi için uygulamanızı derlemeniz gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="04721-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![Görünüm Ekle](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="04721-121">Ekle ' ye tıkladığınızda sistem, film listemizi görüntüleyen bir görünüm için kodu otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04721-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="04721-122">Bu, daha önce Merhaba Dünya görünümünde yaptığımız gibi, &lt;H2&gt; başlığını "film listesi" gibi bir şekilde değiştirmek iyi bir zamandır.</span><span class="sxs-lookup"><span data-stu-id="04721-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="04721-123">[![filmler-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="04721-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="04721-124">Uygulamanızı çalıştırın ve adres çubuğunda/Filmler ' i ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="04721-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="04721-125">Artık, denetleyicinin içindeki temel bir sorgu kullanarak veritabanından veri aldık ve verileri, film hakkında bilgi sahibi bir görünüme döndürtik.</span><span class="sxs-lookup"><span data-stu-id="04721-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="04721-126">Bu görünümü daha sonra film listesinden dönerek ABD için bir veri tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04721-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="04721-127">[![film listesi-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="04721-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="04721-128">Bu uygulamayla ilgili düzenleme, Ayrıntılar ve silme işlevlerini uygulamayız. bu nedenle, bizim için yapı iskelesi şablonunun oluşturduğu varsayılan bağlantılara gerek kalmaz.</span><span class="sxs-lookup"><span data-stu-id="04721-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="04721-129">/Movies/Index.aspx dosyasını açın ve kaldırın.</span><span class="sxs-lookup"><span data-stu-id="04721-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="04721-130">Güncelleştirilmiş görünüm şablonumuza yönelik kaynak kodu, bu değişiklikleri yaptıktan sonra şöyle görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="04721-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="04721-131">İhtiyaç duymayacağımız bağlantıları oluşturuyor, bu nedenle bunları bu örnek için sileceğiz.</span><span class="sxs-lookup"><span data-stu-id="04721-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="04721-132">Yeni bağlantı oluşturduğumuz gibi, yeni bağlantımız da devam edeceğiz!</span><span class="sxs-lookup"><span data-stu-id="04721-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="04721-133">Uygulamamız bu sütun kaldırılmış şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="04721-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="04721-134">[![film listesi-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="04721-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="04721-135">Şimdi film verilerimizden oluşan basit bir listemiz var.</span><span class="sxs-lookup"><span data-stu-id="04721-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="04721-136">Ancak, "Yeni oluştur" bağlantısına tıkladığımızda, bağlanmadığımızda bir hata alırız!</span><span class="sxs-lookup"><span data-stu-id="04721-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="04721-137">Bir oluşturma eylemi yöntemi uygulayalim ve bir kullanıcının veritabanımızda yeni filmler girmelerini olanaklı hale olalım.</span><span class="sxs-lookup"><span data-stu-id="04721-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="04721-138">[Önceki](getting-started-with-mvc-part4.md)
> [İleri](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="04721-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
