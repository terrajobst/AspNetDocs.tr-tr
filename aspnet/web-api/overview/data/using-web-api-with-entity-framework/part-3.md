---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Veritabanını temel almak için Code First Migrations kullanın | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557458"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="cf07b-102">Veritabanını temel almak için Code First Migrations kullanın</span><span class="sxs-lookup"><span data-stu-id="cf07b-102">Use Code First Migrations to Seed the Database</span></span>

<span data-ttu-id="cf07b-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cf07b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="cf07b-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="cf07b-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="cf07b-105">Bu bölümde, veritabanını test verileriyle temel almak için EF 'te [Code First Migrations](https://msdn.microsoft.com/data/jj591621) kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="cf07b-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="cf07b-106">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="cf07b-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="cf07b-107">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="cf07b-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="cf07b-108">Bu komut, projenize geçişler adlı bir klasör ve geçişler klasöründe Configuration.cs adlı bir kod dosyası ekler.</span><span class="sxs-lookup"><span data-stu-id="cf07b-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="cf07b-109">Configuration.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="cf07b-110">Aşağıdaki **using** ifadesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cf07b-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="cf07b-111">Ardından aşağıdaki kodu **Configuration. tohum** yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cf07b-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="cf07b-112">Paket Yöneticisi konsolu penceresinde aşağıdaki komutları yazın:</span><span class="sxs-lookup"><span data-stu-id="cf07b-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="cf07b-113">İlk komut veritabanını oluşturan kodu oluşturur ve ikinci komut bu kodu yürütür.</span><span class="sxs-lookup"><span data-stu-id="cf07b-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="cf07b-114">Veritabanı yerel olarak, [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cf07b-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="cf07b-115">API 'YI keşfet (Isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="cf07b-115">Explore the API (Optional)</span></span>

<span data-ttu-id="cf07b-116">Uygulamayı hata ayıklama modunda çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="cf07b-117">Visual Studio IIS Express başlar ve Web uygulamanızı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="cf07b-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="cf07b-118">Daha sonra Visual Studio bir tarayıcı başlatır ve uygulamanın giriş sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="cf07b-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="cf07b-119">Visual Studio bir Web projesi çalıştırdığında, bir bağlantı noktası numarası atar.</span><span class="sxs-lookup"><span data-stu-id="cf07b-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="cf07b-120">Aşağıdaki görüntüde, bağlantı noktası numarası 50524 ' dir.</span><span class="sxs-lookup"><span data-stu-id="cf07b-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="cf07b-121">Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cf07b-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="cf07b-122">Giriş sayfası ASP.NET MVC kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="cf07b-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="cf07b-123">Sayfanın üst kısmında, "API" yazan bir bağlantı vardır.</span><span class="sxs-lookup"><span data-stu-id="cf07b-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="cf07b-124">Bu bağlantı sizi, Web API 'SI için otomatik olarak oluşturulan bir yardım sayfasına getirir.</span><span class="sxs-lookup"><span data-stu-id="cf07b-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="cf07b-125">(Bu yardım sayfasının nasıl oluşturulduğunu ve sayfaya kendi belgelerinizi nasıl ekleyebileceğiniz hakkında bilgi edinmek için bkz. [ASP.NET Web API Için yardım sayfaları oluşturma](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) İstek ve yanıt biçimi dahil olmak üzere API hakkındaki ayrıntıları görmek için yardım sayfası bağlantılarına tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf07b-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="cf07b-126">API, veritabanında CRUD işlemlerine izin vermez.</span><span class="sxs-lookup"><span data-stu-id="cf07b-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="cf07b-127">Aşağıdaki, API 'YI özetler.</span><span class="sxs-lookup"><span data-stu-id="cf07b-127">The following summarizes the API.</span></span>

| <span data-ttu-id="cf07b-128">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="cf07b-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="cf07b-129">GET api/authors</span><span class="sxs-lookup"><span data-stu-id="cf07b-129">GET api/authors</span></span> | <span data-ttu-id="cf07b-130">Tüm yazarları al.</span><span class="sxs-lookup"><span data-stu-id="cf07b-130">Get all authors.</span></span> |
| <span data-ttu-id="cf07b-131">GET api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="cf07b-131">GET api/authors/{id}</span></span> | <span data-ttu-id="cf07b-132">KIMLIĞE göre yazar alın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-132">Get an author by ID.</span></span> |
| <span data-ttu-id="cf07b-133">POST /api/authors</span><span class="sxs-lookup"><span data-stu-id="cf07b-133">POST /api/authors</span></span> | <span data-ttu-id="cf07b-134">Yeni bir yazar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cf07b-134">Create a new author.</span></span> |
| <span data-ttu-id="cf07b-135">PUT /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="cf07b-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="cf07b-136">Var olan bir yazarı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf07b-136">Update an existing author.</span></span> |
| <span data-ttu-id="cf07b-137">DELETE /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="cf07b-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="cf07b-138">Bir yazarı silin.</span><span class="sxs-lookup"><span data-stu-id="cf07b-138">Delete an author.</span></span> |

| <span data-ttu-id="cf07b-139">Kitaplar</span><span class="sxs-lookup"><span data-stu-id="cf07b-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="cf07b-140">GET /api/books</span><span class="sxs-lookup"><span data-stu-id="cf07b-140">GET /api/books</span></span> | <span data-ttu-id="cf07b-141">Tüm kitapları alın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-141">Get all books.</span></span> |
| <span data-ttu-id="cf07b-142">GET /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="cf07b-142">GET /api/books/{id}</span></span> | <span data-ttu-id="cf07b-143">KIMLIĞE göre bir kitap alın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-143">Get a book by ID.</span></span> |
| <span data-ttu-id="cf07b-144">POST /api/books</span><span class="sxs-lookup"><span data-stu-id="cf07b-144">POST /api/books</span></span> | <span data-ttu-id="cf07b-145">Yeni bir kitap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cf07b-145">Create a new book.</span></span> |
| <span data-ttu-id="cf07b-146">PUT /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="cf07b-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="cf07b-147">Mevcut bir kitabı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf07b-147">Update an existing book.</span></span> |
| <span data-ttu-id="cf07b-148">DELETE /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="cf07b-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="cf07b-149">Bir kitabı silin.</span><span class="sxs-lookup"><span data-stu-id="cf07b-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="cf07b-150">Veritabanını görüntüleme (Isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="cf07b-150">View the Database (Optional)</span></span>

<span data-ttu-id="cf07b-151">Update-database komutunu çalıştırdığınızda EF veritabanını oluşturup `Seed` yöntemi olarak çağırılır.</span><span class="sxs-lookup"><span data-stu-id="cf07b-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="cf07b-152">Uygulamayı yerel olarak çalıştırdığınızda EF, [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)kullanır.</span><span class="sxs-lookup"><span data-stu-id="cf07b-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="cf07b-153">Visual Studio 'da veritabanını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf07b-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="cf07b-154">**Görünüm** menüsünde **SQL Server Nesne Gezgini**'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="cf07b-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="cf07b-155">**Sunucuya Bağlan** iletişim kutusunda, **sunucu adı** düzenleme kutusuna "(LocalDB) \v11.0" yazın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="cf07b-156">**Kimlik doğrulama** seçeneğini "Windows kimlik doğrulaması" olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="cf07b-157">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="cf07b-158">Visual Studio, LocalDB 'ye bağlanır ve SQL Server Nesne Gezgini penceresinde var olan veritabanlarınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="cf07b-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="cf07b-159">EF 'in oluşturduğu tabloları görmek için düğümleri genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf07b-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="cf07b-160">Verileri görüntülemek için bir tabloya sağ tıklayın ve **verileri görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="cf07b-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="cf07b-161">Aşağıdaki ekran görüntüsünde kitaplar tablosu için sonuçlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cf07b-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="cf07b-162">, Veritabanının çekirdek verilerle birlikte doldurulduğunu ve tablo, yazarlar tablosunun yabancı anahtarını içerdiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cf07b-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="cf07b-163">[Önceki](part-2.md)
> [İleri](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="cf07b-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
