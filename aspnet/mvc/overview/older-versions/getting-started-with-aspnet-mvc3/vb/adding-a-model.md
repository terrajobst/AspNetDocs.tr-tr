---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: Model ekleme (VB) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e69d59aed4d74f08f1c653c4965b128c4dbe20ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540525"
---
# <a name="adding-a-model-vb"></a><span data-ttu-id="3ccce-103">Model Ekleme (VB)</span><span class="sxs-lookup"><span data-stu-id="3ccce-103">Adding a Model (VB)</span></span>

<span data-ttu-id="3ccce-104">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="3ccce-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="3ccce-105">Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir.</span><span class="sxs-lookup"><span data-stu-id="3ccce-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="3ccce-106">Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3ccce-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="3ccce-107">Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="3ccce-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="3ccce-108">Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3ccce-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="3ccce-109">Visual Studio Web Developer Express SP1 önkoşulları</span><span class="sxs-lookup"><span data-stu-id="3ccce-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="3ccce-110">ASP.NET MVC 3 Araçlar güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="3ccce-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="3ccce-111">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)</span><span class="sxs-lookup"><span data-stu-id="3ccce-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="3ccce-112">Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="3ccce-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="3ccce-113">Bu konuyla birlikte VB.NET kaynak koduna sahip bir Visual Web Developer projesi mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="3ccce-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="3ccce-114">[Vb.NET sürümünü indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="3ccce-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="3ccce-115">İsterseniz C#, Bu öğreticinin [ C# sürümüne](../cs/adding-a-model.md) geçin.</span><span class="sxs-lookup"><span data-stu-id="3ccce-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="3ccce-116">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="3ccce-116">Adding a Model</span></span>

<span data-ttu-id="3ccce-117">Bu bölümde, bir veritabanında film yönetmeye yönelik bazı sınıflar ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3ccce-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="3ccce-118">Bu sınıflar, ASP.NET MVC uygulamasının "model" bir parçası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3ccce-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="3ccce-119">Bu model sınıflarını tanımlamak ve bunlarla çalışmak için Entity Framework olarak bilinen .NET Framework veri erişim teknolojisini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3ccce-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="3ccce-120">Entity Framework (genellikle EF olarak adlandırılır) *Code First*adlı bir geliştirme paradigmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="3ccce-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="3ccce-121">Code First basit sınıflar yazarak model nesneleri oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ccce-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="3ccce-122">(Bunlar, "düz eski CLR nesnelerinden" POCO sınıfları olarak da bilinir.) Daha sonra veritabanı, çok temiz ve hızlı bir geliştirme iş akışını sağlayan sınıflarınızda anında oluşturulmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="3ccce-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="3ccce-123">Model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="3ccce-123">Adding Model Classes</span></span>

<span data-ttu-id="3ccce-124">**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3ccce-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="3ccce-125">Sınıfı "film" olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3ccce-125">Name the class "Movie".</span></span>

<span data-ttu-id="3ccce-126">Aşağıdaki beş özelliği `Movie` sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3ccce-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="3ccce-127">Bir veritabanındaki filmleri göstermek için `Movie` sınıfını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="3ccce-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="3ccce-128">Bir `Movie` nesnesinin her örneği, bir veritabanı tablosundaki bir satıra karşılık gelir ve `Movie` sınıfının her özelliği tablodaki bir sütunla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="3ccce-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="3ccce-129">Aynı dosyada, aşağıdaki `MovieDBContext` sınıfını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3ccce-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="3ccce-130">`MovieDBContext` sınıfı, bir veritabanında `Movie` sınıf örneklerinin getirmeyi, depolanmasını ve güncelleştirilmesini işleyen Entity Framework film veritabanı bağlamını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3ccce-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="3ccce-131">`MovieDBContext`, Entity Framework tarafından belirtilen `DbContext` taban sınıftan türetilir.</span><span class="sxs-lookup"><span data-stu-id="3ccce-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="3ccce-132">`DbContext` ve `DbSet`hakkında daha fazla bilgi için bkz. [Entity Framework Için üretkenlik iyileştirmeleri](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="3ccce-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="3ccce-133">`DbContext` ve `DbSet`başvuramayacak şekilde, dosyanın en üstüne aşağıdaki `imports` ifadesini eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3ccce-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="3ccce-134">Tüm *Movie. vb* dosyası aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3ccce-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="3ccce-135">Bağlantı dizesi oluşturma ve SQL Server Compact çalışma</span><span class="sxs-lookup"><span data-stu-id="3ccce-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="3ccce-136">Oluşturduğunuz `MovieDBContext` sınıf veritabanına bağlanma ve `Movie` nesneleri veritabanı kayıtlarına eşleme görevini işler.</span><span class="sxs-lookup"><span data-stu-id="3ccce-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="3ccce-137">Tek bir soru sorabilirsiniz, ancak hangi veritabanının bağlanacağı de bu şekilde belirlenir.</span><span class="sxs-lookup"><span data-stu-id="3ccce-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="3ccce-138">Bunu, uygulamanın *Web. config* dosyasına bağlantı bilgilerini ekleyerek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ccce-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="3ccce-139">Uygulama kök *Web. config* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="3ccce-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="3ccce-140">( *Görünümler* klasöründeki *Web. config* dosyası değil.) Aşağıdaki görüntüde hem *Web. config* dosyaları gösterilmektedir; *Web. config* dosyasını daire içinde kırmızı olarak açın.</span><span class="sxs-lookup"><span data-stu-id="3ccce-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="3ccce-141">Aşağıdaki bağlantı dizesini *Web. config* dosyasındaki `<connectionStrings>` öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3ccce-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="3ccce-142">Aşağıdaki örnek, *Web. config* dosyasının yeni bağlantı dizesi eklenmiş bir bölümünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="3ccce-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="3ccce-143">Bu küçük miktarda kod ve XML, film verilerini göstermek ve bir veritabanında depolamak için yazmanız gereken her şey vardır.</span><span class="sxs-lookup"><span data-stu-id="3ccce-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="3ccce-144">Daha sonra, film verilerini göstermek ve kullanıcıların yeni film listeleri oluşturmasına izin vermek için kullanabileceğiniz yeni bir `MoviesController` sınıfı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3ccce-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3ccce-145">[Önceki](adding-a-view.md)
> [İleri](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="3ccce-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
