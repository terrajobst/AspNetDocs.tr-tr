---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: SQL Server veritabanı güncelleştirmesi dağıtma-11/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621072"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="13d0e-103">Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: SQL Server veritabanı güncelleştirmesi dağıtma-11/12</span><span class="sxs-lookup"><span data-stu-id="13d0e-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>

<span data-ttu-id="13d0e-104">[Tom Dykstra](https://github.com/tdykstra) tarafından</span><span class="sxs-lookup"><span data-stu-id="13d0e-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="13d0e-105">Başlatıcı projesi indir</span><span class="sxs-lookup"><span data-stu-id="13d0e-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="13d0e-106">Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="13d0e-107">Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13d0e-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="13d0e-108">Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="13d0e-109">Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Windows Azure Web sitelerine nasıl dağıtılacağını gösterir. bkz. [ASP.NET Web Deployment for Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="13d0e-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="13d0e-110">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="13d0e-110">Overview</span></span>

<span data-ttu-id="13d0e-111">Bu öğreticide, bir veritabanı güncelleştirmesinin tam bir SQL Server veritabanına nasıl dağıtılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="13d0e-112">Code First Migrations, veritabanını güncelleştirme işinin tümünü yaptığından, işlem [veritabanı güncelleştirme](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) öğreticisinde SQL Server Compact için yaptığınız işlemle neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="13d0e-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="13d0e-113">Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="13d0e-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="13d0e-114">Tabloya yeni sütun ekleme</span><span class="sxs-lookup"><span data-stu-id="13d0e-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="13d0e-115">Öğreticinin bu bölümünde, bir veritabanı değişikliği ve ilgili kod değişiklikleri yapıp, bunları test ve üretim ortamlarına dağıtmaya hazırlanmaya yönelik olarak Visual Studio 'da test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="13d0e-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="13d0e-116">Değişiklik, `Instructor` varlığına `OfficeHours` bir sütun eklenmesini ve yeni bilgilerin **eğitmenler** Web sayfasında görüntülenmesini içerir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="13d0e-117">ContosoUniversity. DAL projesinde *Instructor.cs* öğesini açın ve `HireDate` ve `Courses` özellikleri arasına aşağıdaki özelliği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="13d0e-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="13d0e-118">Yeni sütunu test verileriyle birleştirmek için Başlatıcı sınıfını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="13d0e-119">*Migrations\configuration.cs* ' i açın ve `var instructors = new List<Instructor>` başlayan kod bloğunu yeni sütunu içeren aşağıdaki kod bloğu ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="13d0e-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="13d0e-120">ContosoUniversity projesinde, *eğitmenler. aspx* ' i açın ve ilk `GridView` denetimindeki kapatma `</Columns>` etiketinden hemen önce, Office saatleri için yeni bir şablon alanı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="13d0e-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="13d0e-121">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="13d0e-121">Build the solution.</span></span>

<span data-ttu-id="13d0e-122">**Paket Yöneticisi konsol** penceresini açın ve **varsayılan proje**olarak contosouniversity. dal ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="13d0e-123">Aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="13d0e-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="13d0e-124">Uygulamayı çalıştırın ve **eğitmenler** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="13d0e-125">Entity Framework, veritabanını yeniden oluşturduğundan ve test verileriyle kullandığından, sayfanın yüklenmesi normalden biraz daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="13d0e-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="13d0e-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="13d0e-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="13d0e-127">Veritabanı güncelleştirmesini test ortamına dağıtma</span><span class="sxs-lookup"><span data-stu-id="13d0e-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="13d0e-128">Code First Migrations kullandığınızda, SQL Server bir veritabanı değişikliğini dağıtma yöntemi SQL Server Compact ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="13d0e-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="13d0e-129">Ancak, SQL Server Compact, hala SQL Server geçirilecek şekilde ayarlandığından test yayımlama profilini değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="13d0e-130">İlk adım, önceki öğreticide oluşturduğunuz bağlantı dizesi dönüştürmelerinin kaldırılması olur.</span><span class="sxs-lookup"><span data-stu-id="13d0e-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="13d0e-131">Bunlara geçiş için **Package/PUBLISH SQL** sekmesini yapılandırmadan önce yaptığınız gibi, yayımlama profilinde bağlantı dizesi dönüştürmeleri belirtebileceğiniz SQL Server için bunlar artık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="13d0e-132">*Web. test. config* dosyasını açın ve `connectionStrings` öğesini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="13d0e-133">*Web. test. config* dosyasında kalan tek dönüşüm, `appSettings` öğesindeki `Environment` değeri içindir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="13d0e-134">Şimdi yayımlama profilini güncelleştirebilir ve test ortamında yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13d0e-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="13d0e-135">Web 'i **Yayımla** sihirbazını açın ve ardından **profil** sekmesine geçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="13d0e-136">**Test** yayımlama profilini seçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="13d0e-137">**Ayarlar** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="13d0e-138">**Yeni veritabanı yayımlama iyileştirmelerini etkinleştir**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="13d0e-139">**SchoolContext**için bağlantı dizesi kutusuna, önceki öğreticideki *Web. test. config* dönüştürme dosyasında kullandığınız değeri girin:</span><span class="sxs-lookup"><span data-stu-id="13d0e-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="13d0e-140">**Code First Migrations Yürüt ' ü seçin (uygulama başlatma üzerinde çalışır)** .</span><span class="sxs-lookup"><span data-stu-id="13d0e-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="13d0e-141">(Visual Studio sürümünüz içinde, onay kutusu **Code First Migrations uygulanabilir**olarak etiketlenir.)</span><span class="sxs-lookup"><span data-stu-id="13d0e-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="13d0e-142">**DefaultConnection**bağlantı dizesi kutusunda, önceki öğreticideki *Web. test. config* dönüştürme dosyasında kullandığınız değeri girin:</span><span class="sxs-lookup"><span data-stu-id="13d0e-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="13d0e-143">**Güncelleştirme veritabanını** işaretsiz bırak.</span><span class="sxs-lookup"><span data-stu-id="13d0e-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="13d0e-144">**Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-144">Click **Publish**.</span></span>

<span data-ttu-id="13d0e-145">Visual Studio, kod değişikliklerini test ortamına dağıtır ve tarayıcıyı Contoso Üniversitesi giriş sayfasında açar.</span><span class="sxs-lookup"><span data-stu-id="13d0e-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="13d0e-146">Eğitmenler sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-146">Select the Instructors page.</span></span>

<span data-ttu-id="13d0e-147">Uygulama bu sayfayı çalıştırdığında veritabanına erişmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="13d0e-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="13d0e-148">Code First Migrations veritabanının güncel olup olmadığını denetler ve en son geçişin henüz uygulandığını bulur.</span><span class="sxs-lookup"><span data-stu-id="13d0e-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="13d0e-149">Code First Migrations en son geçişi uygular, `Seed` yöntemini çalıştırır ve ardından sayfa normal şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="13d0e-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="13d0e-150">Yeni Office saatleri sütununu, sağlanan verilerle birlikte görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="13d0e-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="13d0e-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="13d0e-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="13d0e-152">Veritabanı güncelleştirmesini üretim ortamına dağıtma</span><span class="sxs-lookup"><span data-stu-id="13d0e-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="13d0e-153">Üretim ortamı için yayımlama profilini de değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="13d0e-154">Bu durumda, güncelleştirilmiş bir. publishsettings dosyasını içeri aktararak var olan profili kaldırır ve yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13d0e-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="13d0e-155">Güncelleştirilmiş dosya, Cytanium adresindeki SQL Server veritabanı için bağlantı dizesini içerir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="13d0e-156">Test ortamına dağıtırken gördüğünüz gibi, artık *Web. Production. config* dönüştürme dosyasında bağlantı dizesi dönüştürmeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="13d0e-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="13d0e-157">Bu dosyayı açın ve `connectionStrings` öğesini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="13d0e-158">Geri kalan dönüşümler, `appSettings` öğesindeki `Environment` değeri ve ELMAH hata raporlarına erişimi kısıtlayan `location` öğesi içindir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="13d0e-159">Üretim için yeni bir yayımlama profili oluşturmadan önce, güncelleştirilmiş bir. publishsettings dosyasını [Üretim ortamında dağıtım](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) öğreticisinde daha önce yaptığınız şekilde indirin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="13d0e-160">(Cytanium Denetim Masası 'nda **Web siteleri**' ne ve ardından **contosouniversity.com** Web sitesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="13d0e-161">**Web yayımlama** sekmesini seçin ve ardından **Bu web sitesi Için yayımlama profilini indir**' e tıklayın.) Bunu yaptığınız neden,. publishsettings dosyasında veritabanı bağlantı dizesini seçmektir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="13d0e-162">Hala SQL Server Compact kullandığınızdan ve henüz Cytanium adresinde SQL Server veritabanı oluşturmadığından, bağlantı dizesi dosyayı ilk kez indirdikten sonra kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="13d0e-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="13d0e-163">Artık yayımlama profilini güncelleştirebilir ve üretim ortamında yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13d0e-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="13d0e-164">Web 'i **Yayımla** sihirbazını açın ve ardından **profil** sekmesine geçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="13d0e-165">**Profilleri Yönet**' e tıklayın ve ardından üretim profilini silin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="13d0e-166">Bu değişikliği kaydetmek için **Web 'ı Yayımla** Sihirbazı 'nı kapatın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="13d0e-167">Web 'i **Yayımla** Sihirbazı 'nı yeniden açın ve ardından **içeri aktar**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="13d0e-168">Geçici bir URL kullanıyorsanız, **bağlantı** SEKMESINDE **hedef URL** 'yi uygun değere değiştirin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="13d0e-169">**İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-169">Click **Next**.</span></span>

<span data-ttu-id="13d0e-170">**Ayarlar** sekmesinde, **Yeni veritabanı yayımlama iyileştirmelerini etkinleştir**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="13d0e-171">**SchoolContext**için bağlantı dizesi açılan listesinde, Cytanium bağlantı dizesini seçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="13d0e-173">**Code First geçişleri Yürüt ' ü seçin (uygulama başlatma üzerinde çalışır)** .</span><span class="sxs-lookup"><span data-stu-id="13d0e-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="13d0e-174">**DefaultConnection**için bağlantı dizesi açılan listesinde Cytanium bağlantı dizesini seçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="13d0e-175">**Profil** sekmesini seçin, **profilleri Yönet**' e tıklayın ve profili "contosouniversity.com-Web dağıtımı" iken "üretim" olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="13d0e-176">Değişikliği kaydetmek için yayımlama profilini kapatın ve sonra yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="13d0e-177">**Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-177">Click **Publish**.</span></span> <span data-ttu-id="13d0e-178">(Gerçek bir üretim web sitesi için, *uygulamayı çevrimdışı. htm\_* kopyalayın ve yayımlamadan önce proje klasörünüze yerleştirip dağıtım tamamlandığında kaldırabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="13d0e-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="13d0e-179">Visual Studio, kod değişikliklerini test ortamına dağıtır ve tarayıcıyı Contoso Üniversitesi giriş sayfasında açar.</span><span class="sxs-lookup"><span data-stu-id="13d0e-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="13d0e-180">Eğitmenler sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="13d0e-180">Select the Instructors page.</span></span>

<span data-ttu-id="13d0e-181">Code First Migrations, veritabanını test ortamında olduğu gibi güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="13d0e-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="13d0e-182">Yeni Office saatleri sütununu, sağlanan verilerle birlikte görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="13d0e-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="13d0e-184">Bir SQL Server veritabanı kullanarak veritabanı değişikliğini içeren bir uygulama güncelleştirmesini başarıyla dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="13d0e-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="13d0e-185">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="13d0e-185">More Information</span></span>

<span data-ttu-id="13d0e-186">Bu, bir ASP.NET Web uygulamasını bir üçüncü taraf barındırma sağlayıcısına dağıtmaya yönelik bu öğretici serisini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="13d0e-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="13d0e-187">Bu öğreticilerde ele alınan konuların herhangi biri hakkında daha fazla bilgi için MSDN Web sitesindeki [ASP.NET dağıtım Içerik haritasına](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) bakın.</span><span class="sxs-lookup"><span data-stu-id="13d0e-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="13d0e-188">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="13d0e-188">Acknowledgements</span></span>

<span data-ttu-id="13d0e-189">Bu öğretici serisinin içeriğine önemli bir katkı yapan kişiler için teşekkür ederiz:</span><span class="sxs-lookup"><span data-stu-id="13d0e-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="13d0e-190">Alberto Poblacion, MVP &amp; MCT, Ispanya</span><span class="sxs-lookup"><span data-stu-id="13d0e-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="13d0e-191">Jarod Ferguson, veri platformu geliştirme MVP, Birleşik Devletler</span><span class="sxs-lookup"><span data-stu-id="13d0e-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="13d0e-192">Harsh Mittal, Microsoft</span><span class="sxs-lookup"><span data-stu-id="13d0e-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="13d0e-193">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="13d0e-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="13d0e-194">Mike Pope, Microsoft</span><span class="sxs-lookup"><span data-stu-id="13d0e-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="13d0e-195">Mohit Srivastava, Microsoft</span><span class="sxs-lookup"><span data-stu-id="13d0e-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="13d0e-196">Raffaele Rialdi, Italya</span><span class="sxs-lookup"><span data-stu-id="13d0e-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="13d0e-197">Rick Anderson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="13d0e-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="13d0e-198">[Sayılan diyez, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="13d0e-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="13d0e-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="13d0e-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="13d0e-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="13d0e-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="13d0e-201">Srđan Božović, Sırbistan</span><span class="sxs-lookup"><span data-stu-id="13d0e-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="13d0e-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="13d0e-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="13d0e-203">[Önceki](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [İleri](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="13d0e-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
