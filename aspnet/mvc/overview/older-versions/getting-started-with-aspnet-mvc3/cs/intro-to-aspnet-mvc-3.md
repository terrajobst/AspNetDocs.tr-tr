---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 ' e girişC#() | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540672"
---
# <a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="df096-103">ASP.NET MVC 3 Sürümüne Giriş (C#)</span><span class="sxs-lookup"><span data-stu-id="df096-103">Intro to ASP.NET MVC 3 (C#)</span></span>

<span data-ttu-id="df096-104">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="df096-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="df096-105">[Burada](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="df096-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="df096-106">Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.</span><span class="sxs-lookup"><span data-stu-id="df096-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="df096-107">Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir.</span><span class="sxs-lookup"><span data-stu-id="df096-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="df096-108">Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="df096-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="df096-109">Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="df096-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="df096-110">Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="df096-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="df096-111">Visual Studio Web Developer Express SP1 önkoşulları</span><span class="sxs-lookup"><span data-stu-id="df096-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="df096-112">ASP.NET MVC 3 Araçlar güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="df096-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="df096-113">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)</span><span class="sxs-lookup"><span data-stu-id="df096-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="df096-114">Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="df096-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="df096-115">Kaynak koduna sahip bir Visual Web C# Developer projesi, bu konuyla birlikte kullanılabilecek.</span><span class="sxs-lookup"><span data-stu-id="df096-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="df096-116">[Sürümü C# indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="df096-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="df096-117">Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.</span><span class="sxs-lookup"><span data-stu-id="df096-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="df096-118">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="df096-118">What You'll Build</span></span>

<span data-ttu-id="df096-119">Bir veritabanından film oluşturmayı, düzenlemenizi ve listelemeyi destekleyen basit bir film listeleme uygulaması uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="df096-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="df096-120">Aşağıda, oluşturacağınız uygulamanın iki ekran görüntüsü verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="df096-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="df096-121">Bu, bir veritabanının bir filmin listesini görüntüleyen bir sayfa içerir:</span><span class="sxs-lookup"><span data-stu-id="df096-121">It includes a page that displays a list of movies from a database:</span></span>

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="df096-123">Uygulama ayrıca film eklemenize, düzenlemenize ve silmenize olanak sağlar ve bireysel kişilerle ilgili ayrıntıları görebilir.</span><span class="sxs-lookup"><span data-stu-id="df096-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="df096-124">Tüm veri girişi senaryoları, veritabanında depolanan verilerin doğru olduğundan emin olmak için doğrulama içerir.</span><span class="sxs-lookup"><span data-stu-id="df096-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="df096-125">Öğrenmeniz gereken yetenekler</span><span class="sxs-lookup"><span data-stu-id="df096-125">Skills You'll Learn</span></span>

<span data-ttu-id="df096-126">Öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="df096-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="df096-127">Yeni bir ASP.NET MVC projesi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="df096-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="df096-128">ASP.NET MVC denetleyicileri ve görünümleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="df096-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="df096-129">Entity Framework Code First paradigması kullanarak yeni bir veritabanı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="df096-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="df096-130">Verileri alma ve görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="df096-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="df096-131">Verileri düzenleme ve veri doğrulamayı etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="df096-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="df096-132">Başlarken</span><span class="sxs-lookup"><span data-stu-id="df096-132">Getting Started</span></span>

<span data-ttu-id="df096-133">Visual Web Developer 2010 Express (kısa için "Visual Web Developer") çalıştırarak başlayın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="df096-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="df096-134">Visual Web Developer, IDE veya tümleşik bir geliştirme ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="df096-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="df096-135">Belgeleri yazmak için Microsoft Word kullandığınızda olduğu gibi, uygulamalar oluşturmak için IDE kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="df096-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="df096-136">Visual Web Developer 'da, sizin için kullanabileceğiniz çeşitli seçenekleri gösteren bir araç çubuğu vardır.</span><span class="sxs-lookup"><span data-stu-id="df096-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="df096-137">Ayrıca, IDE 'de görevler gerçekleştirmek için başka bir yol sağlayan bir menü de vardır.</span><span class="sxs-lookup"><span data-stu-id="df096-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="df096-138">(Örneğin, **Başlangıç** sayfasından **Yeni proje** ' yi seçmek yerine, menüsünü kullanabilir ve **Dosya** **Yeni proje**&gt; ' ni seçebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="df096-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="df096-139">Ilk uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="df096-139">Creating Your First Application</span></span>

<span data-ttu-id="df096-140">Programlama dili olarak Visual Basic veya görseli C# kullanarak uygulamalar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df096-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="df096-141">Sol taraftaki C# görsel ' i seçin ve ardından **ASP.NET MVC 3 Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="df096-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="df096-142">Projenizi "MvcMovie" olarak adlandırın ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="df096-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="df096-143">(Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.)</span><span class="sxs-lookup"><span data-stu-id="df096-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="df096-144">**Yeni ASP.NET MVC 3 projesi** Iletişim kutusunda **Internet uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="df096-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="df096-145">**HTML5 Işaretlemesini kullan** ' a bakın ve varsayılan görünüm altyapısı olarak **Razor** ' i bırakın.</span><span class="sxs-lookup"><span data-stu-id="df096-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="df096-146">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="df096-146">Click **OK**.</span></span> <span data-ttu-id="df096-147">Visual Web Developer, az önce oluşturduğunuz ASP.NET MVC projesi için varsayılan bir şablon kullandı, bu nedenle artık herhangi bir şey yapmadan çalışan bir uygulamanız var!</span><span class="sxs-lookup"><span data-stu-id="df096-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="df096-148">Bu basit bir "Merhaba Dünya!"</span><span class="sxs-lookup"><span data-stu-id="df096-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="df096-149">Project ve uygulamanızı başlatmak için iyi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="df096-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="df096-150">**Hata Ayıkla** menüsünden **hata ayıklamayı Başlat**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="df096-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="df096-151">Hata ayıklamayı başlatmak için klavye kısayolunun F5 olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="df096-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="df096-152">F5, Visual Web Developer 'ın bir geliştirme Web sunucusu başlatmasına ve Web uygulamanızı çalıştırmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="df096-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="df096-153">Daha sonra Visual Web Developer bir tarayıcı başlatır ve uygulamanın giriş sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="df096-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="df096-154">Tarayıcının adres çubuğunun `example.com`gibi `localhost` söydiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="df096-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="df096-155">Bunun nedeni `localhost` her zaman kendi yerel bilgisayarınıza işaret ettiğinden, bu durumda yeni oluşturduğunuz uygulamayı çalıştırıyor olur.</span><span class="sxs-lookup"><span data-stu-id="df096-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="df096-156">Visual Web Developer bir Web projesi çalıştırdığında, Web sunucusu için rastgele bir bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="df096-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="df096-157">Aşağıdaki görüntüde rastgele bağlantı noktası numarası 43246 ' dir.</span><span class="sxs-lookup"><span data-stu-id="df096-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="df096-158">Uygulamayı çalıştırdığınızda, muhtemelen farklı bir bağlantı noktası numarası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="df096-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="df096-159">Bu varsayılan şablon, size iki sayfa ve temel bir oturum açma sayfası sunar.</span><span class="sxs-lookup"><span data-stu-id="df096-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="df096-160">Sonraki adım, bu uygulamanın nasıl çalıştığını değiştirmek ve işlemde ASP.NET MVC hakkında biraz bilgi sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="df096-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="df096-161">Tarayıcınızı kapatın ve bazı kodları değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="df096-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="df096-162">Next</span><span class="sxs-lookup"><span data-stu-id="df096-162">Next</span></span>](adding-a-controller.md)
