---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: Model ekleme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540308"
---
# <a name="adding-a-model"></a><span data-ttu-id="eed90-104">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="eed90-104">Adding a Model</span></span>

<span data-ttu-id="eed90-105">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="eed90-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="eed90-106">[Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="eed90-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="eed90-107">Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.</span><span class="sxs-lookup"><span data-stu-id="eed90-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="eed90-108">Bu bölümde, bir veritabanında film yönetmeye yönelik bazı sınıflar ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="eed90-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="eed90-109">Bu sınıflar, ASP.NET MVC uygulamasının bir parçası&quot; &quot;modeli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="eed90-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="eed90-110">Bu model sınıflarını tanımlamak ve bunlarla çalışmak için [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) olarak bilinen .NET Framework veri erişim teknolojisini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="eed90-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="eed90-111">Entity Framework (genellikle EF olarak adlandırılır) *Code First*adlı bir geliştirme paradigmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="eed90-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="eed90-112">Code First basit sınıflar yazarak model nesneleri oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="eed90-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="eed90-113">(Bunlar ayrıca, &quot;düz eski CLR nesnelerinden POCO sınıfları olarak da bilinir.&quot;) Daha sonra veritabanı, çok temiz ve hızlı bir geliştirme iş akışını sağlayan sınıflarınızda anında oluşturulmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="eed90-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="eed90-114">Model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="eed90-114">Adding Model Classes</span></span>

<span data-ttu-id="eed90-115">**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="eed90-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="eed90-116">Film&quot;&quot;*sınıf* adını girin.</span><span class="sxs-lookup"><span data-stu-id="eed90-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="eed90-117">Aşağıdaki beş özelliği `Movie` sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="eed90-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="eed90-118">Bir veritabanındaki filmleri göstermek için `Movie` sınıfını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="eed90-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="eed90-119">Bir `Movie` nesnesinin her örneği, bir veritabanı tablosundaki bir satıra karşılık gelir ve `Movie` sınıfının her özelliği tablodaki bir sütunla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="eed90-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="eed90-120">Aynı dosyada, aşağıdaki `MovieDBContext` sınıfını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="eed90-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="eed90-121">`MovieDBContext` sınıfı, bir veritabanında `Movie` sınıf örneklerinin getirmeyi, depolanmasını ve güncelleştirilmesini işleyen Entity Framework film veritabanı bağlamını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="eed90-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="eed90-122">`MovieDBContext`, Entity Framework tarafından belirtilen `DbContext` taban sınıftan türetilir.</span><span class="sxs-lookup"><span data-stu-id="eed90-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="eed90-123">`DbContext` ve `DbSet`başvuramayacak şekilde, dosyanın en üstüne aşağıdaki `using` ifadesini eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="eed90-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="eed90-124">Tamamlanmış *Movie.cs* dosyası aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="eed90-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="eed90-125">(Gerekmeyen bazı using deyimleri kaldırılmıştır.)</span><span class="sxs-lookup"><span data-stu-id="eed90-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="eed90-126">Bağlantı Dizesi Oluşturma ve SQL Server LocalDB ile Çalışma</span><span class="sxs-lookup"><span data-stu-id="eed90-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="eed90-127">Oluşturduğunuz `MovieDBContext` sınıf veritabanına bağlanma ve `Movie` nesneleri veritabanı kayıtlarına eşleme görevini işler.</span><span class="sxs-lookup"><span data-stu-id="eed90-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="eed90-128">Tek bir soru sorabilirsiniz, ancak hangi veritabanının bağlanacağı de bu şekilde belirlenir.</span><span class="sxs-lookup"><span data-stu-id="eed90-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="eed90-129">Bunu, uygulamanın *Web. config* dosyasına bağlantı bilgilerini ekleyerek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eed90-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="eed90-130">Uygulama kök *Web. config* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="eed90-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="eed90-131">( *Görünümler* klasöründeki *Web. config* dosyası değil.) Kırmızı renkle özetlenen *Web. config* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="eed90-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="eed90-132">Aşağıdaki bağlantı dizesini *Web. config* dosyasındaki `<connectionStrings>` öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eed90-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="eed90-133">Aşağıdaki örnek, *Web. config* dosyasının yeni bağlantı dizesi eklenmiş bir bölümünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="eed90-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="eed90-134">Bu küçük miktarda kod ve XML, film verilerini göstermek ve bir veritabanında depolamak için yazmanız gereken her şey vardır.</span><span class="sxs-lookup"><span data-stu-id="eed90-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="eed90-135">Daha sonra, film verilerini göstermek ve kullanıcıların yeni film listeleri oluşturmasına izin vermek için kullanabileceğiniz yeni bir `MoviesController` sınıfı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="eed90-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="eed90-136">[Önceki](adding-a-view.md)
> [İleri](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="eed90-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
