---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: Model bağlama ve web forms ile verileri alma ve görüntüleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisinde, model bağlama kullanarak bir ASP.NET Web formları projesi ile temel yönlerini gösterir. Model bağlama veri etkileşimi daha fazla düz - sağlar...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 08cb65f9ef8f5c36070454e011f41554d81f333f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131535"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="2b408-104">Model bağlama ve web forms ile verileri alma ve görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2b408-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="2b408-105">Bu öğretici serisinde, model bağlama kullanarak bir ASP.NET Web formları projesi ile temel yönlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b408-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="2b408-106">Model bağlama, daha doğru verilerle ilgili kaynak nesne (örneğin, ObjectDataSource veya SqlDataSource) daha veri etkileşim sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b408-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="2b408-107">Bu seri, tanıtım malzemeleri ile başlar ve sonraki öğreticilerde için daha gelişmiş kavramlar taşır.</span><span class="sxs-lookup"><span data-stu-id="2b408-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="2b408-108">Model bağlama deseni, tüm veri erişim teknolojisi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="2b408-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="2b408-109">Bu öğreticide, Entity Framework kullanır, ancak en tanıdık veri erişim teknolojisi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b408-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="2b408-110">GridView, ListView, DetailsView veya FormView denetimi gibi bir verilere bağlı sunucu denetimden seçme, güncelleştirme, silme ve veri oluşturmak için kullanabileceğiniz yöntemler adlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="2b408-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="2b408-111">Bu öğreticide, SelectMethod için bir değer belirtmeniz.</span><span class="sxs-lookup"><span data-stu-id="2b408-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="2b408-112">Bu yöntem içinde veri almak için mantığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b408-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="2b408-113">Sonraki öğreticide UpdateMethod, DeleteMethod ve InsertMethod değerleri ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2b408-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="2b408-114">Yapabilecekleriniz [indirme](https://go.microsoft.com/fwlink/?LinkId=286116) tam projede C# veya Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="2b408-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="2b408-115">İndirilebilir kod, Visual Studio 2012 ve sonraki sürümlerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="2b408-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="2b408-116">Bu öğreticide gösterilen Visual Studio 2017 şablonundan biraz farklıdır Visual Studio 2012 şablonu kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b408-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="2b408-117">Öğreticide uygulamayı Visual Studio'da çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2b408-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="2b408-118">Ayrıca, bir barındırma sağlayıcısı uygulamayı dağıtmak ve internet üzerinden hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b408-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="2b408-119">Microsoft'un sunduğu en fazla 10 web siteleri için ücretsiz bir web barındırma bir</span><span class="sxs-lookup"><span data-stu-id="2b408-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="2b408-120">[Ücretsiz Azure deneme hesabı](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="2b408-120">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="2b408-121">Visual Studio web projesini Azure App Service Web Apps'e dağıtma hakkında daha fazla bilgi için bkz: [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md) serisi.</span><span class="sxs-lookup"><span data-stu-id="2b408-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="2b408-122">Bu öğretici ayrıca SQL Server veritabanınızı Azure SQL veritabanı'na dağıtmak için Entity Framework Code First Migrations kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b408-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2b408-123">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="2b408-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="2b408-124">Microsoft Visual Studio 2017 veya Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="2b408-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="2b408-125">Bu öğreticide Visual Studio 2012 ve Visual Studio 2013 ile de çalışır, ancak kullanıcı arabirimi ve proje şablonu bazı farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="2b408-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="2b408-126">Derleme</span><span class="sxs-lookup"><span data-stu-id="2b408-126">What you'll build</span></span>

<span data-ttu-id="2b408-127">Bu öğreticide, gerekir:</span><span class="sxs-lookup"><span data-stu-id="2b408-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="2b408-128">Üniversite öğrencileri eğitim kayıtlı yansıtan veri nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b408-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="2b408-129">Derleme nesnelerden veritabanı tabloları</span><span class="sxs-lookup"><span data-stu-id="2b408-129">Build database tables from the objects</span></span>
* <span data-ttu-id="2b408-130">Veritabanı test verileri ile doldurma</span><span class="sxs-lookup"><span data-stu-id="2b408-130">Populate the database with test data</span></span>
* <span data-ttu-id="2b408-131">Bir web formunda veri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2b408-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="2b408-132">Projeyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b408-132">Create the project</span></span>

1. <span data-ttu-id="2b408-133">Visual Studio 2017'de oluşturma bir **ASP.NET Web uygulaması (.NET Framework)** adlı proje **ContosoUniversityModelBinding**.</span><span class="sxs-lookup"><span data-stu-id="2b408-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![Proje oluşturma](retrieving-data/_static/image19.png)

2. <span data-ttu-id="2b408-135">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2b408-135">Select **OK**.</span></span> <span data-ttu-id="2b408-136">Bir şablon seçmek için iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2b408-136">The dialog box to select a template appears.</span></span>

   ![Web formları seçin](retrieving-data/_static/image3.png)

3. <span data-ttu-id="2b408-138">Seçin **Web Forms** şablonu.</span><span class="sxs-lookup"><span data-stu-id="2b408-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="2b408-139">Gerekirse, kimlik doğrulaması değiştirin **bireysel kullanıcı hesapları**.</span><span class="sxs-lookup"><span data-stu-id="2b408-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="2b408-140">Seçin **Tamam** projeyi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2b408-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="2b408-141">Site görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="2b408-141">Modify site appearance</span></span>

   <span data-ttu-id="2b408-142">Site görünümünü özelleştirmek için bazı değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="2b408-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="2b408-143">Site.Master dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2b408-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="2b408-144">Görüntülenecek başlığını değiştirme **Contoso University** değil **My ASP.NET Application**.</span><span class="sxs-lookup"><span data-stu-id="2b408-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="2b408-145">Üst bilgi metni değiştirme **uygulama adı** için **Contoso University**.</span><span class="sxs-lookup"><span data-stu-id="2b408-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="2b408-146">Uygun olanları site için Gezinti üst bilgi bağlantıları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2b408-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="2b408-147">Kaldırmak için bağlantıları **hakkında** ve **kişi** ve bunun yerine, bağlantı bir **Öğrenciler** oluşturacağınız sayfası.</span><span class="sxs-lookup"><span data-stu-id="2b408-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="2b408-148">Site.Master kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2b408-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="2b408-149">Öğrenci verileri görüntülemek için bir web formu ekleyin</span><span class="sxs-lookup"><span data-stu-id="2b408-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="2b408-150">İçinde **Çözüm Gezgini**, projenize sağ tıklayın, **Ekle** ardından **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="2b408-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="2b408-151">İçinde **Yeni Öğe Ekle** iletişim kutusunda **ana sayfa ile Web formu** şablon ve adlandırın **Students.aspx**.</span><span class="sxs-lookup"><span data-stu-id="2b408-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![sayfası oluşturma](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="2b408-153">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="2b408-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="2b408-154">Web formun ana sayfa seçin **Site.Master**.</span><span class="sxs-lookup"><span data-stu-id="2b408-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="2b408-155">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2b408-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="2b408-156">Veri modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="2b408-156">Add the data model</span></span>

<span data-ttu-id="2b408-157">İçinde **modelleri** klasör adında bir sınıf ekleyin **UniversityModels.cs**.</span><span class="sxs-lookup"><span data-stu-id="2b408-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="2b408-158">Sağ **modelleri**seçin **Ekle**, ardından **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="2b408-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="2b408-159">**Yeni Öğe Ekle** iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="2b408-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="2b408-160">Soldaki menüden **kod**, ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="2b408-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![Model sınıfı oluşturma](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="2b408-162">Sınıf adı **UniversityModels.cs** seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2b408-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="2b408-163">Bu dosyadaki tanımlamak `SchoolContext`, `Student`, `Enrollment`, ve `Course` gibi sınıfları:</span><span class="sxs-lookup"><span data-stu-id="2b408-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="2b408-164">`SchoolContext` Sınıf türetilir `DbContext`, veritabanı bağlantısını yönetir ve verileri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="2b408-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="2b408-165">İçinde `Student` sınıfı, uygulanan öznitelikleri duyuru `FirstName`, `LastName`, ve `Year` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2b408-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="2b408-166">Bu öğreticide, veri doğrulama için bu öznitelikler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2b408-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="2b408-167">Kodu basitleştirmek için yalnızca şu özellikler veri doğrulama öznitelikleri ile işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="2b408-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="2b408-168">Gerçek bir projede doğrulama öznitelikleri doğrulama gerektiren tüm özellikler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2b408-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="2b408-169">UniversityModels.cs kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2b408-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="2b408-170">Sınıflara göre veritabanı ayarlama</span><span class="sxs-lookup"><span data-stu-id="2b408-170">Set up the database based on classes</span></span>

<span data-ttu-id="2b408-171">Bu öğreticide [Code First Migrations](https://docs.microsoft.com/en-us/ef/ef6/modeling/code-first/migrations/) nesneleri oluşturmak ve tabloları veritabanı.</span><span class="sxs-lookup"><span data-stu-id="2b408-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/en-us/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="2b408-172">Bu tablolar, Öğrenciler ve bunların dersler hakkında bilgi depolar.</span><span class="sxs-lookup"><span data-stu-id="2b408-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="2b408-173">Seçin **Araçları** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="2b408-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="2b408-174">İçinde **Paket Yöneticisi Konsolu**, şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2b408-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="2b408-175">Komut başarıyla tamamlandıktan geçişleri etkin olmadığını bildiren bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2b408-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![migrations'ı etkinleştirme](retrieving-data/_static/image8.png)

      <span data-ttu-id="2b408-177">Adlı bir dosya bildirim *Configuration.cs* oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="2b408-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="2b408-178">`Configuration` Sınıfında bir `Seed` yöntemi test verileri ile veritabanı tablolarını önceden doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b408-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="2b408-179">Veritabanı önceden doldurun</span><span class="sxs-lookup"><span data-stu-id="2b408-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="2b408-180">Configuration.cs açın.</span><span class="sxs-lookup"><span data-stu-id="2b408-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="2b408-181">Aşağıdaki kodu ekleyin `Seed` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2b408-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="2b408-182">Ayrıca, bir `using` bildirimi `ContosoUniversityModelBinding. Models` ad alanı.</span><span class="sxs-lookup"><span data-stu-id="2b408-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="2b408-183">Configuration.cs kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2b408-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="2b408-184">Paket Yöneticisi Konsolu'nda komutu Çalıştır **ekleme geçiş ilk**.</span><span class="sxs-lookup"><span data-stu-id="2b408-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="2b408-185">Komutunu çalıştırın **veritabanını Güncelleştir**.</span><span class="sxs-lookup"><span data-stu-id="2b408-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="2b408-186">Bu komutu çalıştırırken özel durum alırsanız `StudentID` ve `CourseID` değerleri farklı olabilir `Seed` yöntemi değerleri.</span><span class="sxs-lookup"><span data-stu-id="2b408-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="2b408-187">Bu veritabanı tabloları açın ve varolan değerleri Bul `StudentID` ve `CourseID`.</span><span class="sxs-lookup"><span data-stu-id="2b408-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="2b408-188">Bu değerleri dengeli dağıtım için kod ekleyin `Enrollments` tablo.</span><span class="sxs-lookup"><span data-stu-id="2b408-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="2b408-189">Bir GridView denetimi ekleme</span><span class="sxs-lookup"><span data-stu-id="2b408-189">Add a GridView control</span></span>

<span data-ttu-id="2b408-190">Doldurulmuş veritabanı verileri, artık bu verileri almak ve görüntülemek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="2b408-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="2b408-191">Open Students.aspx.</span><span class="sxs-lookup"><span data-stu-id="2b408-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="2b408-192">Bulun `MainContent` yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="2b408-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="2b408-193">Bu yer tutucu içinde ekleyin bir **GridView** bu kodu içeren bir denetim.</span><span class="sxs-lookup"><span data-stu-id="2b408-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="2b408-194">Dikkat edilecek noktalar:</span><span class="sxs-lookup"><span data-stu-id="2b408-194">Things to note:</span></span>
   * <span data-ttu-id="2b408-195">Değeri ayarlamak için bildirim `SelectMethod` GridView öğesinde bulunan özellik.</span><span class="sxs-lookup"><span data-stu-id="2b408-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="2b408-196">Bu değer sonraki adımda oluşturacağınız GridView verileri almak için kullanılan yöntemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="2b408-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="2b408-197">`ItemType` Özelliği `Student` daha önce oluşturduğunuz sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2b408-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="2b408-198">Bu ayar, sınıf özelliklerini biçimlendirmede başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b408-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="2b408-199">Örneğin, `Student` sınıfında adlı bir koleksiyon `Enrollments`.</span><span class="sxs-lookup"><span data-stu-id="2b408-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="2b408-200">Kullanabileceğiniz `Item.Enrollments` Bu koleksiyonu alma ve ardından [LINQ söz dizimi](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) kredisi toplam kayıtlı her öğrencinin almak için.</span><span class="sxs-lookup"><span data-stu-id="2b408-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="2b408-201">Students.aspx kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2b408-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="2b408-202">Verileri almak için kod ekleyin</span><span class="sxs-lookup"><span data-stu-id="2b408-202">Add code to retrieve data</span></span>

   <span data-ttu-id="2b408-203">Belirtilen yöntem Students.aspx arka plan kod dosyasında, ekleme `SelectMethod` değeri.</span><span class="sxs-lookup"><span data-stu-id="2b408-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="2b408-204">Open Students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="2b408-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="2b408-205">Ekleme `using` deyimleri için `ContosoUniversityModelBinding. Models` ve `System.Data.Entity` ad alanları.</span><span class="sxs-lookup"><span data-stu-id="2b408-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="2b408-206">Belirtilen için yöntem ekleme `SelectMethod`:</span><span class="sxs-lookup"><span data-stu-id="2b408-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="2b408-207">`Include` Yan tümce sorgu performansını artırır, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2b408-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="2b408-208">Olmadan `Include` yan tümcesi, verileri kullanarak alınır [ *yavaş Yükleniyor*](https://en.wikipedia.org/wiki/Lazy_loading), ayrı bir sorgu her zaman veritabanına göndermeden kapsamaktadır ilgili veriler alınır.</span><span class="sxs-lookup"><span data-stu-id="2b408-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="2b408-209">İle `Include` yan tümcesi, veri kullanarak alınır *istekli yükleme*, tek veritabanı sorgusu başka bir deyişle, tüm ilgili verileri alır.</span><span class="sxs-lookup"><span data-stu-id="2b408-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="2b408-210">İlgili verileri kullanılmaz, daha fazla veri alındığından istekli yükleme verimli değildir.</span><span class="sxs-lookup"><span data-stu-id="2b408-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="2b408-211">Her kayıt için ilgili verileri görüntülendiğinden ancak bu durumda, istekli yükleme, en iyi performansı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b408-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="2b408-212">İlgili verileri yüklenirken performans değerlendirmeleri hakkında daha fazla bilgi için bkz: **Lazy Eager ve açık, ilgili veri yükleme** konusundaki [bir ASP.NET Entity Framework ile ilgili verileri okuma MVC uygulama](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2b408-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="2b408-213">Varsayılan olarak, veri anahtarı olarak işaretlenmiş özelliğinin değerlere göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="2b408-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="2b408-214">Ekleyebileceğiniz bir `OrderBy` yan tümcesini farklı bir sıralama değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="2b408-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="2b408-215">Bu örnekte, varsayılan `StudentID` özelliği, sıralama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2b408-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="2b408-216">İçinde [sıralama, sayfalama ve filtreleme veri](sorting-paging-and-filtering-data.md) makalesi, kullanıcı sıralamak için sütun seçmek için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2b408-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="2b408-217">Students.aspx.cs kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2b408-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="2b408-218">Uygulamanızı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2b408-218">Run your application</span></span> 

<span data-ttu-id="2b408-219">Web uygulamanızı çalıştırın (**F5**) gidin **Öğrenciler** sayfasında, şunları görüntüler:</span><span class="sxs-lookup"><span data-stu-id="2b408-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![verileri göster](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="2b408-221">Model bağlama yöntemleri otomatik olarak oluşturulmasını</span><span class="sxs-lookup"><span data-stu-id="2b408-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="2b408-222">Bu öğretici serisinin ile çalışırken, projenize öğreticinin kodu yalnızca kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b408-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="2b408-223">Ancak, bu yaklaşımın bir dezavantajı, model bağlama yöntemleri için kod otomatik olarak oluşturmak için Visual Studio tarafından sağlanan özellik, uyumlu olmayan bir duruma gelebilir emin olur.</span><span class="sxs-lookup"><span data-stu-id="2b408-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="2b408-224">Otomatik kod oluşturma kendi projeleri üzerinde çalışıyorsanız, zaman ve nasıl bir işlem uygulanacağı bir fikir elde Yardım kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b408-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="2b408-225">Otomatik kod oluşturma özelliği bu bölümde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2b408-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="2b408-226">Bu bölümde, yalnızca bilgi amaçlıdır ve projenizde uygulamak için gereken herhangi bir kod içermiyor.</span><span class="sxs-lookup"><span data-stu-id="2b408-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="2b408-227">İçin bir değer ayarlarken `SelectMethod`, `UpdateMethod`, `InsertMethod`, veya `DeleteMethod` seçebileceğiniz özellikleri biçimlendirme kodda **yeni yöntem oluşturma** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="2b408-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![bir yöntem oluşturma](retrieving-data/_static/image18.png)

<span data-ttu-id="2b408-229">Visual Studio yalnızca arka plan kod uygun imzaya sahip bir yöntem oluşturur, ancak aynı zamanda işlemi gerçekleştirmek için uygulama kodu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2b408-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="2b408-230">İlk ayarlarsanız `ItemType` otomatik kod oluşturma kullanmadan önce özelliğini sunan, işlemleri için türü oluşturulan kod kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b408-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="2b408-231">Örneğin, ayarlarken `UpdateMethod` özelliği, aşağıdaki kodu otomatik olarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="2b408-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="2b408-232">Yeniden, bu kod projenize eklenmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2b408-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="2b408-233">Sonraki öğreticide, güncelleştirme, silme ve yeni veri eklemek için yöntemleri uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="2b408-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="2b408-234">Özet</span><span class="sxs-lookup"><span data-stu-id="2b408-234">Summary</span></span>

<span data-ttu-id="2b408-235">Bu öğreticide, oluşturulan veri modeli sınıfları ve bu sınıflardan bir veritabanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2b408-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="2b408-236">Veritabanı tablolarını test verileri ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="2b408-236">You filled the database tables with test data.</span></span> <span data-ttu-id="2b408-237">Model bağlama veritabanından veri almak için kullanılır ve ardından verileri GridView içinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2b408-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="2b408-238">Sonraki [öğretici](updating-deleting-and-creating-data.md) bu dizide, güncelleştirme, silme ve verileri oluşturma etkinleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b408-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2b408-239">Next</span><span class="sxs-lookup"><span data-stu-id="2b408-239">Next</span></span>](updating-deleting-and-creating-data.md)
