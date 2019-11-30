---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio kullanarak ASP.NET Web dağıtımı: veritabanı güncelleştirmesi dağıtma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636825"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="743e5-103">Visual Studio kullanarak ASP.NET Web dağıtımı: veritabanı güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="743e5-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>

<span data-ttu-id="743e5-104">[Tom Dykstra](https://github.com/tdykstra) tarafından</span><span class="sxs-lookup"><span data-stu-id="743e5-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="743e5-105">Başlatıcı projesi indir</span><span class="sxs-lookup"><span data-stu-id="743e5-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="743e5-106">Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir.</span><span class="sxs-lookup"><span data-stu-id="743e5-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="743e5-107">Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="743e5-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="743e5-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="743e5-108">Overview</span></span>

<span data-ttu-id="743e5-109">Bu öğreticide, bir veritabanı değişikliği ve ilgili kod değişiklikleri yapar, değişiklikleri Visual Studio 'da test edin ve ardından bu güncelleştirmeyi test, hazırlama ve üretim ortamlarına dağıtın.</span><span class="sxs-lookup"><span data-stu-id="743e5-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="743e5-110">Öğreticide ilk olarak Code First Migrations tarafından yönetilen bir veritabanını güncelleştirme ve daha sonra dbDacFx sağlayıcısı kullanılarak bir veritabanının nasıl güncelleşmekte olduğu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="743e5-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="743e5-111">Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="743e5-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="743e5-112">Code First Migrations kullanarak bir veritabanı güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="743e5-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="743e5-113">Bu bölümde, `Student` ve `Instructor` varlıkları için `Person` taban sınıfına bir Doğum tarihi sütunu eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="743e5-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="743e5-114">Ardından, eğitmen verilerini görüntüleyen sayfayı yeni sütunu görüntüleyecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="743e5-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="743e5-115">Son olarak, değişiklikleri test, hazırlama ve üretime dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="743e5-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="743e5-116">Uygulama veritabanındaki bir tabloya sütun ekleme</span><span class="sxs-lookup"><span data-stu-id="743e5-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="743e5-117">*Contosouniversity. dal* projesinde, *Person.cs* açın ve `Person` sınıfının sonuna aşağıdaki özelliği ekleyin (bundan sonra iki kapatma küme ayracı olmalıdır):</span><span class="sxs-lookup"><span data-stu-id="743e5-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="743e5-118">Sonra, `Seed` yöntemini yeni sütun için bir değer sağlayacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="743e5-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="743e5-119">*Migrations\configuration.cs* ' i açın ve `var instructors = new List<Instructor>` başlayan kod bloğunu, Doğum tarihi bilgilerini içeren aşağıdaki kod bloğu ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="743e5-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="743e5-120">Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="743e5-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="743e5-121">ContosoUniversity. DAL ' nin hala **varsayılan proje**olarak seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="743e5-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="743e5-122">**Paket Yöneticisi konsolu** penceresinde, **varsayılan proje**olarak **contosouniversity. dal** ' ı seçin ve aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="743e5-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="743e5-123">Bu komut tamamlandığında, Visual Studio yeni `DbMigration` sınıfını tanımlayan sınıf dosyasını açar ve `Up` yönteminde yeni sütunu oluşturan kodu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743e5-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="743e5-124">`Up` yöntemi, değişikliği uygularken sütunu oluşturur ve `Down` yöntemi, değişikliği geri aldığınızda sütunu siler.</span><span class="sxs-lookup"><span data-stu-id="743e5-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="743e5-126">Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresine aşağıdaki komutu girin (contosouniversity. dal projesinin hala seçili olduğundan emin olun):</span><span class="sxs-lookup"><span data-stu-id="743e5-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="743e5-127">Entity Framework `Up` yöntemini çalıştırır ve sonra `Seed` metodunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="743e5-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="743e5-128">Eğitmenler sayfasında yeni sütunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="743e5-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="743e5-129">ContosoUniversity projesinde, *eğitmenler. aspx* ' i açın ve Doğum tarihini göstermek için yeni bir şablon alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="743e5-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="743e5-130">İşe alma tarihi ve Office ataması için olanlar arasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="743e5-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="743e5-131">(Kod girintileme eşitlenmemiş ise, CTRL + K tuşlarına basabilir ve sonra dosyayı otomatik olarak yeniden biçimlendirmek için CTRL-D ' ye basabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="743e5-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="743e5-132">Uygulamayı çalıştırın ve **eğitmenler** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="743e5-133">Sayfa yüklendiğinde, yeni Doğum tarihi alanına sahip olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="743e5-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![Doğum tarihi olan eğitmenler sayfası](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="743e5-135">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="743e5-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="743e5-136">Veritabanı güncelleştirmesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="743e5-136">Deploy the database update</span></span>

1. <span data-ttu-id="743e5-137">**Çözüm Gezgini** contosouniversity projesini seçin.</span><span class="sxs-lookup"><span data-stu-id="743e5-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="743e5-138">Web 'de **Yayımla** araç çubuğunda, **Test** yayımlama profili ' ne tıklayın ve ardından **Web 'i Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="743e5-139">(Araç çubuğu devre dışıysa, **Çözüm Gezgini**' de contosouniversity projesini seçin.)</span><span class="sxs-lookup"><span data-stu-id="743e5-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="743e5-140">Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı giriş sayfasında açılır.</span><span class="sxs-lookup"><span data-stu-id="743e5-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="743e5-141">Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için **eğitmenler** sayfasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="743e5-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="743e5-142">Uygulama bu sayfanın veritabanına erişmeye çalıştığında, Code First veritabanı şemasını güncelleştirir ve `Seed` metodunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="743e5-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="743e5-143">Sayfa görüntülendiğinde, içindeki tarihlerle birlikte beklenen **Doğum tarihi** sütununu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="743e5-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="743e5-144">Web 'de **Yayımla** araç çubuğunda, **hazırlama** yayımlama profili ' ne tıklayın ve ardından **Web 'i Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="743e5-145">Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için hazırlama aşamasında **eğitmenler** sayfasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="743e5-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="743e5-146">Web 'de **Yayımla** araç çubuğunda, **Üretim** yayımlama profili ' ne tıklayın ve ardından **Web 'i Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="743e5-147">Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için üretimde **eğitmenler** sayfasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="743e5-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="743e5-148">Bir veritabanı değişikliğini içeren gerçek bir üretim uygulaması güncelleştirmesi için, önceki öğreticide gördüğünüz gibi *app\_offline. htm*' yi kullanarak dağıtım sırasında uygulamayı çevrimdışı duruma de çevrimdışına almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="743e5-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="743e5-149">DbDacFx sağlayıcısını kullanarak bir veritabanı güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="743e5-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="743e5-150">Bu bölümde, üyelik veritabanındaki *Kullanıcı* tablosuna bir *Açıklama* sütunu ekler ve her bir kullanıcı için açıklamaları görüntülemenize ve düzenlemenize olanak tanıyan bir sayfa oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="743e5-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="743e5-151">Ardından, değişiklikleri test, hazırlama ve üretime dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743e5-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="743e5-152">Üyelik veritabanındaki bir tabloya sütun ekleme</span><span class="sxs-lookup"><span data-stu-id="743e5-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="743e5-153">Visual Studio 'da **SQL Server Nesne Gezgini**açın.</span><span class="sxs-lookup"><span data-stu-id="743e5-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="743e5-154">Expand **(LocalDB) \v11.0**, **veritabanları**' nı genişletin, **ASPNET-ContosoUniversity** ( **ASPNET-contosouniversity-prod**) öğesini genişletin ve ardından **Tablolar**' ı genişletin.</span><span class="sxs-lookup"><span data-stu-id="743e5-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="743e5-155">**SQL Server** düğümü altında **(LocalDB) \v11.0** görmüyorsanız, **SQL Server** düğümüne sağ tıklayıp **SQL Server Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="743e5-156">**Sunucuya Bağlan** Iletişim kutusunda **sunucu adı**olarak *(LocalDB) \v11.0* girin ve ardından **Bağlan**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="743e5-157">**ASPNET-Contosoüniversitesi**' ni görmüyorsanız, projeyi çalıştırın ve *yönetici* kimlik bilgilerini (parola *devpwd*) kullanarak oturum açın ve **SQL Server Nesne Gezgini** penceresini yenileyin.</span><span class="sxs-lookup"><span data-stu-id="743e5-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="743e5-158">**Kullanıcılar** tablosuna sağ tıklayın ve sonra **Tasarımcı görüntüle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![SSOX Görünüm Tasarımcısı](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="743e5-160">Tasarımcıda bir *Açıklama* sütunu ekleyin ve bunu *nvarchar (128)* ve null yapılabilir yapın ve ardından **Güncelleştir**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![Açıklama sütunu ekleme](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="743e5-162">**Veritabanı güncelleştirmelerini Önizle** kutusunda **veritabanını güncelleştir**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![Veritabanı güncelleştirmelerini Önizle](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="743e5-164">Yeni sütunu göstermek ve düzenlemek için bir sayfa oluşturun</span><span class="sxs-lookup"><span data-stu-id="743e5-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="743e5-165">**Çözüm Gezgini**, contosouniversity projesindeki **Hesap** klasörüne sağ tıklayın, **Ekle**' ye ve ardından **Yeni öğe**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="743e5-166">**Ana sayfayı kullanarak yeni bir Web formu** oluşturun ve bunu *UserInfo. aspx*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="743e5-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="743e5-167">Varsayılan *site. Master* dosyasını ana sayfa olarak kabul edin.</span><span class="sxs-lookup"><span data-stu-id="743e5-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="743e5-168">Aşağıdaki işaretlemeyi `MainContent` `Content` öğesine kopyalayın (3 `Content` öğelerinden son):</span><span class="sxs-lookup"><span data-stu-id="743e5-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="743e5-169">*UserInfo. aspx* sayfasına sağ tıklayın ve **Tarayıcıda görüntüle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="743e5-170">*Yönetici* Kullanıcı kimlik bilgilerinizle (parola *devpwd*) oturum açın ve sayfanın düzgün çalıştığını doğrulamak için bir kullanıcıya bazı yorumlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="743e5-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![UserInfo sayfası](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="743e5-172">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="743e5-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="743e5-173">Veritabanı güncelleştirmesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="743e5-173">Deploy the database update</span></span>

<span data-ttu-id="743e5-174">DbDacFx sağlayıcısını kullanarak dağıtmak için, yayımlama profilinde **veritabanını güncelleştir** seçeneğini belirlemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="743e5-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="743e5-175">Bununla birlikte, bu seçeneği kullandığınızda ilk dağıtım için bazı ek SQL betikleri da yapılandırmış olursunuz: Bunlar hala profilde bulunur ve bunların yeniden çalıştırılmasını engellemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="743e5-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="743e5-176">ContosoUniversity projesine sağ tıklayıp **Yayımla**' ya tıklayarak **Web 'i Yayımla** Sihirbazı ' nı açın.</span><span class="sxs-lookup"><span data-stu-id="743e5-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="743e5-177">**Test** profilini seçin.</span><span class="sxs-lookup"><span data-stu-id="743e5-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="743e5-178">**Ayarlar** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="743e5-179">**DefaultConnection**altında **veritabanını güncelleştir**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="743e5-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="743e5-180">İlk dağıtım için çalıştırmak üzere yapılandırdığınız ek betikleri devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="743e5-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="743e5-181">**Veritabanı güncelleştirmelerini Yapılandır**öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="743e5-182">**Veritabanı güncelleştirmelerini Yapılandır** iletişim kutusunda, *ver. SQL* ve *ASPNET-Data-dev. SQL*' ın yanındaki onay kutularını temizleyin.</span><span class="sxs-lookup"><span data-stu-id="743e5-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="743e5-183">**Kapat**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="743e5-183">Click **Close**.</span></span>
6. <span data-ttu-id="743e5-184">**Önizleme** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="743e5-185">**DefaultConnection**'un **veritabanları** ve sağ tarafındaki **veritabanı önizleme** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![Veritabanı önizlemesi](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="743e5-187">Önizleme penceresi, veritabanı şemasının kaynak veritabanının şemasıyla eşleşmesini sağlamak için hedef veritabanında çalıştırılacak betiği gösterir.</span><span class="sxs-lookup"><span data-stu-id="743e5-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="743e5-188">Komut dosyası, yeni sütunu ekleyen bir ALTER TABLE komutu içerir.</span><span class="sxs-lookup"><span data-stu-id="743e5-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="743e5-189">**Veritabanı önizlemesi** iletişim kutusunu kapatın ve ardından **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="743e5-190">Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı giriş sayfasında açılır.</span><span class="sxs-lookup"><span data-stu-id="743e5-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="743e5-191">Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için UserInfo sayfasını (giriş sayfası URL 'sine *Hesap/UserInfo. aspx* ekleyin) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="743e5-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="743e5-192">*Yönetici* ve *devpwd*girerek oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="743e5-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="743e5-193">Tablolardaki veriler varsayılan olarak dağıtılır ve çalıştırmak için bir veri dağıtım betiği yapılandırmadıysanız, geliştirmede eklediğiniz yorumu bulamayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="743e5-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="743e5-194">Değişikliğin veritabanına dağıtıldığını ve sayfanın doğru şekilde çalıştığını doğrulamak için şimdi hazırlama aşamasında yeni bir yorum ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743e5-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="743e5-195">Hazırlama ve üretime dağıtmak için aynı yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="743e5-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="743e5-196">Ek betikleri devre dışı bırakmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="743e5-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="743e5-197">Test profiliyle karşılaştırılan tek fark, hazırlama ve üretim profillerindeki yalnızca bir betiği devre dışı bırakacağından yalnızca *ASPNET-prod-Data. SQL*' i çalıştıracak şekilde yapılandırılmanızdır.</span><span class="sxs-lookup"><span data-stu-id="743e5-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="743e5-198">Hazırlama ve üretim için kimlik bilgileri yönetici ve prodpwd ' dir.</span><span class="sxs-lookup"><span data-stu-id="743e5-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="743e5-199">Bir veritabanı değişikliğini içeren gerçek bir üretim uygulaması güncelleştirmesi için, [önceki öğreticide](deploying-a-code-update.md)gördüğünüz şekilde, uygulamayı yayımlamadan ve silmeden önce *çevrimdışı. htm\_* yükleme sırasında uygulamayı çevrimdışı olarak da çevrimdışına almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="743e5-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="743e5-200">Özet</span><span class="sxs-lookup"><span data-stu-id="743e5-200">Summary</span></span>

<span data-ttu-id="743e5-201">Artık Code First Migrations ve dbDacFx sağlayıcısını kullanarak bir veritabanı değişikliği içeren bir uygulama güncelleştirmesi dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="743e5-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![Doğum tarihi olan eğitmenler sayfası](deploying-a-database-update/_static/image8.png)

![UserInfo sayfası](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="743e5-204">Sonraki öğreticide, komut satırını kullanarak dağıtımların nasıl yürütüleceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="743e5-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="743e5-205">[Önceki](deploying-a-code-update.md)
> [İleri](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="743e5-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
