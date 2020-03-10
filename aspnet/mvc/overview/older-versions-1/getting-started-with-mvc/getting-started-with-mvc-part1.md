---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 'ye giriş | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581587"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="15173-104">ASP.NET MVC’ye Giriş</span><span class="sxs-lookup"><span data-stu-id="15173-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="15173-105">[Scott Hanselman](https://github.com/shanselman) tarafından</span><span class="sxs-lookup"><span data-stu-id="15173-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="15173-106">Bu öğreticiyi [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)kullanarak [burada](../../getting-started/introduction/getting-started.md) kullanılabilirse, güncelleştirilmiş bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="15173-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="15173-107">Yeni öğretici, bu öğreticide birçok geliştirme sağlayan ASP.NET MVC 5 ' i kullanır.</span><span class="sxs-lookup"><span data-stu-id="15173-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="15173-108">Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir.</span><span class="sxs-lookup"><span data-stu-id="15173-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="15173-109">Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="15173-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="15173-110">Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="15173-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="15173-111">[Visual Web Developer 2010 Express 'i](https://www.microsoft.com/express/Web/)kullanarak Ilk ASP.NET MVC web uygulamamızı yapalim.</span><span class="sxs-lookup"><span data-stu-id="15173-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="15173-112">Film oluşturup listemize olanak sağlayacak küçük bir film listesi uygulaması oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="15173-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="15173-113">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="15173-113">What You'll Build</span></span>

<span data-ttu-id="15173-114">Oluşturacağınız uygulamanın iki ekran görüntüsü aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15173-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="15173-115">Çeşitli sütunlara sahip basit bir film tablosuna sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="15173-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="15173-116">[![film listesi-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="15173-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="15173-117">Böylece, listeye film ekleyebilmemiz için bir oluştur formu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="15173-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="15173-118">[Film oluşturmak ![-Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="15173-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="15173-119">Öğrenmeniz gereken yetenekler</span><span class="sxs-lookup"><span data-stu-id="15173-119">Skills You'll Learn</span></span>

<span data-ttu-id="15173-120">Bu öğreticide, Visual Studio kullanarak bir ASP.NET MVC web uygulaması oluşturma hakkında temel bilgiler verilir.</span><span class="sxs-lookup"><span data-stu-id="15173-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="15173-121">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="15173-121">You'll learn:</span></span>

- <span data-ttu-id="15173-122">Yeni bir ASP.NET MVC projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="15173-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="15173-123">SQL Server ile yeni bir veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="15173-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="15173-124">ASP.NET MVC denetleyicileri ve görünümleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="15173-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="15173-125">Verileri alma ve görüntüleme</span><span class="sxs-lookup"><span data-stu-id="15173-125">How to retrieve and display data</span></span>
- <span data-ttu-id="15173-126">Verileri düzenleme ve veri doğrulamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="15173-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="15173-127">Veritabanı şemasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="15173-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="15173-128">Başlarken</span><span class="sxs-lookup"><span data-stu-id="15173-128">Get Started</span></span>

<span data-ttu-id="15173-129">Visual Web Developer 2010 Express 'ı çalıştırarak başlayın (bunu şimdi "VWD" olarak arayarak) ve başlangıç ekranından yeni proje ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="15173-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="15173-130">Visual Web Developer, IDE veya tümleşik bir geliştirici ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="15173-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="15173-131">Belgeleri yazmak için Microsoft Word kullandığınızda olduğu gibi, uygulamalar oluşturmak için IDE kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="15173-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="15173-132">En üstteki, sizin için kullanabileceğiniz çeşitli seçenekleri ve ayrıca dosya seçmek için kullanabileceğiniz menüyü gösteren bir araç çubuğu bulunur | Yeni proje.</span><span class="sxs-lookup"><span data-stu-id="15173-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="15173-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="15173-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="15173-134">Ilk uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="15173-134">Creating Your First Application</span></span>

<span data-ttu-id="15173-135">Visual Basic veya görsel C#kullanarak uygulamalar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15173-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="15173-136">Şimdilik, sol taraftaki görsel C# ' i seçip "ASP.NET MVC 2 Web uygulaması" nı seçin.</span><span class="sxs-lookup"><span data-stu-id="15173-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="15173-137">Projenizi "Filmler" olarak adlandırın ve Tamam ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="15173-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="15173-138">[Yeni ![proje](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="15173-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="15173-139">Sağ tarafta, uygulamanızdaki tüm dosya ve klasörler gösteriliyor Çözüm Gezgini.</span><span class="sxs-lookup"><span data-stu-id="15173-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="15173-140">Ortadaki büyük pencere, kodunuzu düzenlediğiniz ve zamanınızın çoğunu geçirdiğiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="15173-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="15173-141">Visual Studio, az önce oluşturduğunuz ASP.NET MVC projesi için varsayılan bir şablon kullandı, bu nedenle artık herhangi bir şey yapmadan çalışan bir uygulamaya sahipsiniz!</span><span class="sxs-lookup"><span data-stu-id="15173-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="15173-142">Bu basit bir "Merhaba Dünya!</span><span class="sxs-lookup"><span data-stu-id="15173-142">This is a simple "Hello World!</span></span> <span data-ttu-id="15173-143">Proje ve uygulamamız için başlamak iyi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="15173-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="15173-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="15173-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="15173-145">Araç çubuğunda "Oynat" düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="15173-145">Select the "play" button to the toolbar.</span></span>

![Hata Ayıklamayı Başlat](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="15173-147">Bu, programınızı derlemek ve uygulamanızı bir Web tarayıcısında başlatmak için sağ tarafta işaret eden yeşil bir oktur.</span><span class="sxs-lookup"><span data-stu-id="15173-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="15173-148">*NOTE: klavyenizde F5 tuşuna basabilir veya "hata ayıkla" menüsünden hata ayıklamayı Başlat&gt;başlatabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="15173-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="15173-149">Bu, Visual Web Developer 'ın bir geliştirme Web sunucusu başlatmasını ve Web uygulamamızı çalıştırmasına neden olur (Bunu etkinleştirmek için yapılandırma veya el ile adım gerekmez).</span><span class="sxs-lookup"><span data-stu-id="15173-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="15173-150">Daha sonra bir tarayıcı başlatır ve uygulamanın giriş sayfasına gözatmasını sağlayacak şekilde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="15173-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="15173-151">Tarayıcının adres çubuğunun, example.com gibi değil, "localhost" olduğunu belirten bir bildirim aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15173-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="15173-152">Bunun nedeni, localhost 'un her zaman kendi yerel bilgisayarınızı gösterdiği ve bu durumda yeni oluşturduğumuz uygulamayı çalıştırdığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="15173-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="15173-153">[![giriş sayfası](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="15173-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="15173-154">Bu varsayılan şablon, size iki sayfa ve temel bir oturum açma sayfası sunar.</span><span class="sxs-lookup"><span data-stu-id="15173-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="15173-155">Bu uygulamanın nasıl çalıştığını değiştirelim ve işlemde ASP.NET MVC hakkında biraz bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15173-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="15173-156">Tarayıcınızı kapatın ve kodun değiştirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="15173-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="15173-157">Next</span><span class="sxs-lookup"><span data-stu-id="15173-157">Next</span></span>](getting-started-with-mvc-part2.md)
