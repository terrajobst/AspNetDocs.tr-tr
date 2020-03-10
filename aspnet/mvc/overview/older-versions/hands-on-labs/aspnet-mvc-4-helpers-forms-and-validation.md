---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 yardımcıları, formları ve doğrulaması | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 modeller ve veri erişimi uygulamalı laboratuvarda, veritabanından verileri yüklüyor ve görüntülüyor olursunuz. Bu uygulamalı laboratuvarda,...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539580"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="707cf-104">ASP.NET MVC 4 Yardımcılar, Formlar ve Doğrulama</span><span class="sxs-lookup"><span data-stu-id="707cf-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="707cf-105">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="707cf-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="707cf-106">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="707cf-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="707cf-107">**ASP.NET MVC 4 modeller ve veri erişimi** uygulamalı laboratuvarda, veritabanından verileri yüklüyor ve görüntülüyor olursunuz.</span><span class="sxs-lookup"><span data-stu-id="707cf-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="707cf-108">Bu uygulamalı laboratuvarda, **müzik deposu** uygulamasına verileri düzenleme özelliği ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="707cf-109">Bu amaç göz önünde bulundurularak öncelikle Albümler 'in oluşturma, okuma, güncelleştirme ve silme (CRUD) eylemlerini destekleyecek olan denetleyiciyi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="707cf-110">Bir HTML tablosunda Albümler özelliklerini görüntülemek için ASP.NET MVC 'nin yapı iskelesi özelliğinden yararlanarak bir dizin görünümü şablonu oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="707cf-111">Bu görünümü geliştirmek için uzun açıklamaları kesecek özel bir HTML Yardımcısı ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="707cf-112">Daha sonra, veritabanı içindeki albümleri değiştirmenize olanak sağlayacak olan düzenleme ve oluşturma görünümlerini, açılan öğeler gibi form öğelerinin yardımıyla de ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="707cf-113">Son olarak, kullanıcıların bir albümü silmesine izin verirsiniz ve ayrıca bu kişilerin girişlerini doğrulayarak yanlış veri girmesini engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="707cf-114">Bu uygulamalı laboratuvar, **ASP.NET MVC**'nin temel bilgisine sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="707cf-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="707cf-115">Daha önce **ASP.NET MVC** kullandıysanız, **ASP.NET MVC temelleri** uygulamalı laboratuvarına gitmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="707cf-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="707cf-116">Bu laboratuvar, daha önce kaynak klasörde sunulan örnek bir Web uygulamasına küçük değişiklikler uygulayarak açıklanan geliştirmeler ve yeni özellikler konusunda size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="707cf-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="707cf-117">Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit sürümlerinde](https://aka.ms/webcamps-training-kit)kullanılabilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="707cf-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="707cf-118">Bu laboratuvara özgü proje, [ASP.NET MVC 4 yardımcıları, formları ve doğrulamasında](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="707cf-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="707cf-119">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="707cf-119">Objectives</span></span>

<span data-ttu-id="707cf-120">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="707cf-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="707cf-121">CRUD işlemlerini desteklemek için bir denetleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="707cf-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="707cf-122">Bir HTML tablosunda varlık özelliklerini görüntülemek için bir dizin görünümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="707cf-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="707cf-123">Özel HTML Yardımcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="707cf-124">Düzenleme görünümü oluşturma ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="707cf-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="707cf-125">HTTP-GET veya HTTP-POST çağrılarına tepki veren eylem yöntemlerine göre ayrım yapın</span><span class="sxs-lookup"><span data-stu-id="707cf-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="707cf-126">Oluşturma görünümü ekleme ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="707cf-126">Add and customize a Create View</span></span>
- <span data-ttu-id="707cf-127">Bir varlığın silinmesini işleme</span><span class="sxs-lookup"><span data-stu-id="707cf-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="707cf-128">Kullanıcı girişini doğrulama</span><span class="sxs-lookup"><span data-stu-id="707cf-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="707cf-129">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="707cf-129">Prerequisites</span></span>

<span data-ttu-id="707cf-130">Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="707cf-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="707cf-131">[Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).</span><span class="sxs-lookup"><span data-stu-id="707cf-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="707cf-132">Kurulum</span><span class="sxs-lookup"><span data-stu-id="707cf-132">Setup</span></span>

<span data-ttu-id="707cf-133">**Kod parçacıklarını yükleme**</span><span class="sxs-lookup"><span data-stu-id="707cf-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="707cf-134">Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="707cf-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="707cf-135">Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="707cf-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="707cf-136">Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek B: kod parçacıkları&quot;kullanarak](#AppendixB) bu belgedeki eke başvurabilirsiniz &quot;.</span><span class="sxs-lookup"><span data-stu-id="707cf-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="707cf-137">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="707cf-137">Exercises</span></span>

<span data-ttu-id="707cf-138">Aşağıdaki alıştırmalarda bu uygulamalı laboratuvar yapılır:</span><span class="sxs-lookup"><span data-stu-id="707cf-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="707cf-139">Mağaza Yöneticisi denetleyicisi ve onun dizin görünümü oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="707cf-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="707cf-140">HTML Yardımcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="707cf-141">Düzenleme görünümü oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="707cf-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="707cf-142">Oluşturma görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="707cf-143">Silme Işlemi işleniyor</span><span class="sxs-lookup"><span data-stu-id="707cf-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="707cf-144">Doğrulama Ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="707cf-145">Istemci tarafında unobtrusive jQuery kullanma</span><span class="sxs-lookup"><span data-stu-id="707cf-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="707cf-146">Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="707cf-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="707cf-147">Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="707cf-148">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**</span><span class="sxs-lookup"><span data-stu-id="707cf-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="707cf-149">Alıştırma 1: mağaza yöneticisi denetleyicisi ve onun dizin görünümü oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="707cf-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="707cf-150">Bu alıştırmada, CRUD işlemlerini desteklemek için yeni bir denetleyici oluşturmayı ve son olarak ASP.NET MVC 'nin yapı iskelesi avantajlarından yararlanarak bir dizin görünümü şablonu oluşturmayı öğreneceksiniz. bir HTML tablosunda Albümler özelliklerini görüntüleme özelliği.</span><span class="sxs-lookup"><span data-stu-id="707cf-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="707cf-151">Görev 1-StoreManagerController oluşturma</span><span class="sxs-lookup"><span data-stu-id="707cf-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="707cf-152">Bu görevde, CRUD işlemlerini desteklemek için **Storemanagercontroller** adlı yeni bir denetleyici oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="707cf-153">**Kaynak/Ex1-Creatingdepotoremanagercontroller/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="707cf-154">Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="707cf-155">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="707cf-156">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="707cf-157">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="707cf-158">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="707cf-159">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="707cf-160">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="707cf-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="707cf-161">Yeni bir denetleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-161">Add a new controller.</span></span> <span data-ttu-id="707cf-162">Bunu yapmak için Çözüm Gezgini içindeki **denetleyiciler** klasörüne sağ tıklayın, **Ekle** ve sonra **Denetleyici** komutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="707cf-163">**Denetleyici** **adını** **storemanagercontroller** olarak değiştirin ve **MVC Controller seçeneğinin boş okuma/yazma eylemleri** seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="707cf-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="707cf-164">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="707cf-164">Click **Add**.</span></span>

    <span data-ttu-id="707cf-165">![Denetleyici Ekle iletişim kutusu](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Denetleyici Ekle iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="707cf-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="707cf-166">*Denetleyici Ekle Iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="707cf-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="707cf-167">Yeni bir denetleyici sınıfı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="707cf-167">A new Controller class is generated.</span></span> <span data-ttu-id="707cf-168">Okuma/yazma eylemleri eklemek için belirttiğiniz için, genel CRUD eylemleri, TODO açıklamaları doldurulmuş olarak oluşturulur ve uygulamaya özel mantık dahil etmek isteyip istemediğini sorar.</span><span class="sxs-lookup"><span data-stu-id="707cf-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="707cf-169">Görev 2-StoreManager dizinini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="707cf-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="707cf-170">Bu görevde, veritabanından Albümler listesini içeren bir görünüm döndürmek için StoreManager Dizin eylemi yöntemini özelleştirecek olursunuz.</span><span class="sxs-lookup"><span data-stu-id="707cf-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="707cf-171">StoreManagerController sınıfında, aşağıdaki *using* yönergelerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="707cf-172">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve formları ve doğrulama-Ex1, MvcMusicStore kullanarak*)</span><span class="sxs-lookup"><span data-stu-id="707cf-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="707cf-173">Bir **Musicstoreentities** örneği tutmak Için **storemanagercontroller** öğesine bir alan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="707cf-174">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="707cf-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="707cf-175">Albümler listesini içeren bir görünüm döndürmek için StoreManagerController Dizin eylemini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="707cf-176">Denetleyici eylemi mantığı, daha önce yazılan StoreController 'ın Dizin eylemine çok benzer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="707cf-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="707cf-177">Görüntülenecek tarz ve sanatçı bilgileri de dahil olmak üzere tüm albümlerini almak için LINQ kullanın.</span><span class="sxs-lookup"><span data-stu-id="707cf-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="707cf-178">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex1 StoreManagerController dizini*)</span><span class="sxs-lookup"><span data-stu-id="707cf-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="707cf-179">Görev 3-dizin görünümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="707cf-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="707cf-180">Bu görevde, **Storemanager** denetleyicisi tarafından döndürülen albüm listesini görüntülemek Için dizin görünümü şablonu oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="707cf-181">Yeni görünüm şablonunu oluşturmadan önce, **görünümü Ekle Iletişim kutusunun** kullanılacak **Albüm** sınıfını bilmesi için projeyi derlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="707cf-182">**Derlemeyi Seç | Projeyi derlemek için MvcMusicStore oluşturun** .</span><span class="sxs-lookup"><span data-stu-id="707cf-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="707cf-183">**Dizin** eylemi yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="707cf-184">Bu işlem, **Görünüm Ekle** iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="707cf-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="707cf-185">![Görünüm Ekle](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Görünüm Ekle")</span><span class="sxs-lookup"><span data-stu-id="707cf-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="707cf-186">*Dizin yönteminin içinden bir görünüm ekleme*</span><span class="sxs-lookup"><span data-stu-id="707cf-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="707cf-187">Görünüm Ekle iletişim kutusunda görünüm adının **Dizin**olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="707cf-188">Kesin olarak **belirlenmiş görünüm oluştur** seçeneğini belirleyin ve **model sınıfı** açılır listesinden **Albüm (Mvcmusicstore. modeller)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="707cf-189">**Yapı iskelesi şablonu** açılır **listesinden liste** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="707cf-190">**Görünüm altyapısını** **Razor** 'e ve diğer alanlara varsayılan değerlerini kullanarak bırakın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="707cf-191">![Dizin görünümü ekleme](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Dizin görünümü ekleme")</span><span class="sxs-lookup"><span data-stu-id="707cf-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="707cf-192">*Dizin görünümü ekleme*</span><span class="sxs-lookup"><span data-stu-id="707cf-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="707cf-193">Görev 4-dizin görünümünün scafkatlama 'ını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="707cf-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="707cf-194">Bu görevde, istediğiniz alanları görüntülemesi için ASP.NET MVC scafkatlama özelliğiyle oluşturulan basit görünüm şablonunu ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="707cf-195">ASP.NET MVC içindeki **scafkatlama** desteği, albüm modelindeki tüm alanları listeleyen basit bir görünüm şablonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="707cf-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="707cf-196">**Yapı iskelesi** , türü kesin belirlenmiş bir görünüme başlamak için hızlı bir yol sağlar: görünüm şablonunu el ile yazmak yerine, scafkatlama hızlı bir şekilde varsayılan şablon oluşturur ve oluşturulan kodu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>

1. <span data-ttu-id="707cf-197">Oluşturulan kodu gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-197">Review the code created.</span></span> <span data-ttu-id="707cf-198">Oluşturulan alanların listesi, **Yapı** verilerini görüntülemek için kullanılan aşağıdaki HTML tablosunun bir parçası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="707cf-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="707cf-199">Yalnızca **tarz**, **sanatçı**, **albüm başlığı**ve **Fiyat** alanlarını göstermek için **&lt;tablo&gt;** kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="707cf-200">Bu, **Albümkimliği** ve **Albüm sanatı URL 'si** sütunlarını siler.</span><span class="sxs-lookup"><span data-stu-id="707cf-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="707cf-201">Ayrıca, Genreıd ve ArtistId sütunlarını, **artist.Name** ve **genre.Name**'nin bağlı sınıf özelliklerini görüntüleyecek şekilde değiştirir ve **Ayrıntılar** bağlantısını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="707cf-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="707cf-202">Aşağıdaki açıklamaları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="707cf-203">5\. Görev-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="707cf-204">Bu görevde, **Storemanager** **Dizin** görünümü şablonunun önceki adımların tasarımına göre Albümler listesini görüntülediğini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="707cf-205">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-206">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-206">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-207">Bir albüm listesinin **başlık**, **sanatçı** ve **tarzlarını**göstererek görüntülendiğini doğrulamak için URL 'yi **/storemanager** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="707cf-208">![Albümler listesine göz atma](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Albümler listesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="707cf-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="707cf-209">*Albümler listesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="707cf-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="707cf-210">Alıştırma 2: HTML Yardımcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="707cf-211">StoreManager Dizin sayfasında bir olası sorun vardır: başlık ve sanatçı adı özelliklerinin ikisi de tablo biçimlendirmesini oluşturmak için yeterince uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="707cf-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="707cf-212">Bu alıştırmada, bu metni kesmek için özel bir HTML Yardımcısı eklemeyi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="707cf-213">Aşağıdaki şekilde, küçük bir tarayıcı boyutu kullanırken metnin uzunluğu nedeniyle biçimin nasıl değiştirildiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="707cf-214">![Kesilmedi metin içeren albümler listesine göz atma](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Kesilmedi metin içeren albümler listesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="707cf-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="707cf-215">*Kesilmedi metin içeren albümler listesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="707cf-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="707cf-216">Görev 1-HTML yardımcısını genişletme</span><span class="sxs-lookup"><span data-stu-id="707cf-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="707cf-217">Bu görevde, ASP.NET MVC görünümleri içinde kullanıma sunulan **HTML** nesnesine **Truncate** 'e yeni bir yöntem ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="707cf-218">Bunu yapmak için, ASP.NET MVC tarafından sunulan yerleşik **System. Web. Mvc. HtmlHelper** sınıfına bir **genişletme yöntemi** uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="707cf-219">**Uzantı yöntemleri**hakkında daha fazla bilgi için lütfen bu MSDN makalesini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="707cf-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="707cf-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span><span class="sxs-lookup"><span data-stu-id="707cf-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>

1. <span data-ttu-id="707cf-221">**Kaynak/EX2-AddingAnHTMLHelper/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="707cf-222">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="707cf-223">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="707cf-224">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="707cf-225">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="707cf-226">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="707cf-227">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="707cf-228">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="707cf-229">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="707cf-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="707cf-230">StoreManager 'ın Dizin görünümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="707cf-231">Bunu yapmak için, Çözüm Gezgini **views** klasörünü ve ardından **storemanager** ' ı genişletin ve **Index. cshtml** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="707cf-232"><strong>Truncate</strong> Helper metodunu tanımlamak için <strong>@model</strong> yönergesinin altına aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="707cf-233">Görev 2-sayfada metin kesiliyor</span><span class="sxs-lookup"><span data-stu-id="707cf-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="707cf-234">Bu görevde, görünüm şablonundaki metni kesmek için **Truncate** metodunu kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="707cf-235">StoreManager 'ın Dizin görünümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="707cf-236">Bunu yapmak için, Çözüm Gezgini **views** klasörünü ve ardından **storemanager** ' ı genişletin ve **Index. cshtml** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="707cf-237">**Sanatçı adını** ve albümün **başlığını**gösteren satırları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="707cf-238">Bunu yapmak için aşağıdaki satırları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="707cf-239">Görev 3-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="707cf-240">Bu görevde, **Storemanager** **Dizin** görünümü şablonunun albümün başlığını ve sanatçı adını kesen test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="707cf-241">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-242">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-242">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-243">**Başlık** ve **sanatçı** sütunundaki uzun metinlerin KESILDIĞINI doğrulamak için URL 'yi **/storemanager** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="707cf-244">![Kesilen başlıklar ve sanatçı adları](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Kesilen başlıklar ve sanatçı adları")</span><span class="sxs-lookup"><span data-stu-id="707cf-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="707cf-245">*Kesilen başlıklar ve sanatçı adları*</span><span class="sxs-lookup"><span data-stu-id="707cf-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="707cf-246">Alıştırma 3: düzenleme görünümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="707cf-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="707cf-247">Bu alıştırmada, Mağaza yöneticilerinin bir albümü düzenlemesine izin vermek için form oluşturmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="707cf-248">**/Storemanager/Edit/ID** URL 'ye gözatacağız (**kimliği** düzenlenecek albümün benzersiz kimliği olan kimlik), bu nedenle sunucuya http-get çağrısı yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="707cf-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="707cf-249">Denetleyici düzenleme eylemi yöntemi, veritabanından uygun albümü alır, kapsüllemek için bir **Storemanagerviewmodel** nesnesi oluşturur (sanatçı ve tarzların listesi ile birlikte) ve ardından HTML sayfasını kullanıcıya geri işlemek Için bir görünüm şablonuna geçirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="707cf-250">Bu sayfada, albüm özelliklerini düzenlemede metin kutuları ve açılan öğeler içeren bir **&lt;form&gt;** öğesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="707cf-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="707cf-251">Kullanıcı, albüm formu değerlerini güncelleştirdikten ve **Kaydet** düğmesine tıkladığında, DEĞIŞIKLIKLER bir http-post çağrısıyla **/Storemanager/Edit/ID**öğesine geri gönderilir. URL son çağrıdaki ile aynı kalsa da, ASP.NET MVC bu zamanın bir HTTP-POST olduğunu belirler ve bu nedenle farklı bir düzenleme eylemi yöntemi yürütür (bir tane **[HttpPost]** ile donatılmış).</span><span class="sxs-lookup"><span data-stu-id="707cf-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="707cf-252">Görev 1-HTTP-GET düzenleme eylemi yöntemini uygulama</span><span class="sxs-lookup"><span data-stu-id="707cf-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="707cf-253">Bu görevde, veritabanından uygun albümü ve tüm tarzların ve sanatçıların listesini almak için düzenleme eylemi yönteminin HTTP-GET sürümünü uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="707cf-254">Bu verileri, yanıtı işlemek için bir görünüm şablonuna geçirilecek son adımda tanımlanan **Storemanagerviewmodel** nesnesine göre paketleyebilir.</span><span class="sxs-lookup"><span data-stu-id="707cf-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="707cf-255">**Kaynak/Ex3-CreatingTheEditView/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="707cf-256">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="707cf-257">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="707cf-258">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="707cf-259">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="707cf-260">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="707cf-261">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="707cf-262">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="707cf-263">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="707cf-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="707cf-264">**Storemanagercontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="707cf-265">Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="707cf-266">Uygun **albümün** yanı sıra **tarzların** ve **sanatçıların** listesini almak için **http-get düzenleme** eylemi yöntemini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="707cf-267">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex3 StoreManagerController http-düzenleme EYLEMINI al*)</span><span class="sxs-lookup"><span data-stu-id="707cf-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="707cf-268">**System. Collections. Generic** listesi yerine sanatçı ve tarzlar için **System. Web. Mvc** **SelectList** öğesini kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="707cf-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="707cf-269">**SelectList** , HTML açılan listelerini doldurmak ve geçerli seçim gibi şeyleri yönetmek için temizleyici bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="707cf-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="707cf-270">Denetleyici eyleminde bu ViewModel nesnelerinin örneklendirime ve daha sonra ayarlanması, düzenleme formu senaryosunu temizleyici hale getirir.</span><span class="sxs-lookup"><span data-stu-id="707cf-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="707cf-271">Görev 2-düzenleme görünümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="707cf-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="707cf-272">Bu görevde, daha sonra albüm özelliklerini görüntüleyecek olan bir düzenleme görünümü şablonu oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="707cf-273">Düzenleme görünümünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="707cf-273">Create the Edit View.</span></span> <span data-ttu-id="707cf-274">Bunu yapmak için, eylemi **Düzenle** yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="707cf-275">Görünüm Ekle iletişim kutusunda görünüm adının **düzenlendiğini**doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="707cf-276">**Türü kesin belirlenmiş görünüm oluştur** onay kutusunu işaretleyin ve **veri sınıfı** açılır listesinden **Albüm (Mvcmusicstore. modeller)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="707cf-277">**Yapı iskelesi şablonu** açılır listesinden **Düzenle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="707cf-278">Diğer alanları varsayılan değerlerine bırakın ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="707cf-279">![Düzenleme görünümü ekleme](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Düzenleme görünümü ekleme")</span><span class="sxs-lookup"><span data-stu-id="707cf-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="707cf-280">*Düzenleme görünümü ekleme*</span><span class="sxs-lookup"><span data-stu-id="707cf-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="707cf-281">Görev 3-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="707cf-282">Bu görevde, **Storemanager** **düzenleme** görünümü sayfasının, albüm olarak geçirilmiş parametre değerlerini görüntülemesini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="707cf-283">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-284">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-284">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-285">Geçirilen albümün özelliklerinin görüntülendiğini doğrulamak için **/Storemanager/Edit/1** URL 'sini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="707cf-286">![Albümün düzenleme görünümüne göz atma](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Albümün düzenleme görünümüne göz atma")</span><span class="sxs-lookup"><span data-stu-id="707cf-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="707cf-287">*Albümün düzenleme görünümüne göz atma*</span><span class="sxs-lookup"><span data-stu-id="707cf-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="707cf-288">Görev 4-albüm Düzenleyicisi şablonunda açılan listeleri uygulama</span><span class="sxs-lookup"><span data-stu-id="707cf-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="707cf-289">Bu görevde, kullanıcının sanatçı ve tarzların listesinden seçim yapabilmesi için son görevde oluşturulan görünüm şablonuna açılan listeleri ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="707cf-290">Tüm **Albüm** alan kümesi kodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707cf-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="707cf-291">Sanatçı ve tarzların seçilmesi için işleme açılan listeleri için bir **HTML. DropDownList** Yardımcısı eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="707cf-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="707cf-292">**HTML. DropDownList** 'e geçirilen parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="707cf-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="707cf-293">Form alanının adı ( **&quot;ArtistId&quot;** ).</span><span class="sxs-lookup"><span data-stu-id="707cf-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="707cf-294">Açılan **listenin selectvalues listesi** .</span><span class="sxs-lookup"><span data-stu-id="707cf-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="707cf-295">5\. Görev-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="707cf-296">Bu görevde, **Storemanager** **düzenleme** görünümü SAYFASıNıN sanatçı ve tarz kimliği metin alanları yerine açılan listeleri görüntülediğini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="707cf-297">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-298">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-298">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-299">Sanatçı ve tarz KIMLIĞI metin alanları yerine açılan listeleri görüntülediğini doğrulamak için URL 'YI **/Storemanager/Edit/1** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="707cf-300">![Açılır liste ile albümün düzenleme görünümüne göz atma](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Açılır liste ile albümün düzenleme görünümüne göz atma")</span><span class="sxs-lookup"><span data-stu-id="707cf-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="707cf-301">*Albümün düzenleme görünümüne göz atma, bu sefer açılan listeleri*</span><span class="sxs-lookup"><span data-stu-id="707cf-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="707cf-302">Görev 6-HTTP-POST düzenleme eylem yöntemini uygulama</span><span class="sxs-lookup"><span data-stu-id="707cf-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="707cf-303">Artık düzenleme görünümü beklendiği gibi görüntülediğine göre, albüme yapılan değişiklikleri kaydetmek için HTTP-POST düzenleme eylemi yöntemini uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="707cf-304">Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="707cf-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="707cf-305">**Storemanagercontroller** ' i **denetleyiciler** klasöründen açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="707cf-306">**Http-post düzenleme** eylemi yöntemi kodunu aşağıdaki kodla değiştirin (yerine geçecek yöntemin iki parametre alan aşırı yüklenmiş sürümü olduğunu unutmayın):</span><span class="sxs-lookup"><span data-stu-id="707cf-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="707cf-307">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex3 StoreManagerController http-düzenleme sonrası eylemi*)</span><span class="sxs-lookup"><span data-stu-id="707cf-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="707cf-308">Bu yöntem, Kullanıcı görünümün **Kaydet** düğmesine tıkladığında ve veritabanında kalıcı hale getirmek için form değerlerini sunucuya geri gönderirse yürütülür.</span><span class="sxs-lookup"><span data-stu-id="707cf-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="707cf-309">Dekoratör **[HttpPost]** , YÖNTEMIN bu http-post senaryolarında kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="707cf-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="707cf-310">Yöntemi bir **Albüm** nesnesi alır.</span><span class="sxs-lookup"><span data-stu-id="707cf-310">The method takes an **Album** object.</span></span> <span data-ttu-id="707cf-311">ASP.NET MVC, albüm nesnesini, postalanan &lt;form&gt; değerlerinden otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="707cf-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="707cf-312">Yöntemi şu adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="707cf-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="707cf-313">Model geçerliyse:</span><span class="sxs-lookup"><span data-stu-id="707cf-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="707cf-314">Bağlam içindeki albüm girişini, değiştirilen bir nesne olarak işaretlemek için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="707cf-315">Değişiklikleri kaydedin ve dizin görünümüne yeniden yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="707cf-316">Model geçerli değilse, ViewBag 'i **Genreıd** ve **ArtistId**ile doldurur ve bu durumda kullanıcının gerekli bir güncelleştirmeyi gerçekleştirmesini sağlamak için alınan albüm nesnesiyle birlikte görünümü döndürür.</span><span class="sxs-lookup"><span data-stu-id="707cf-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="707cf-317">Görev 7-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="707cf-318">Bu görevde, **Storemanager düzenleme** görünümü sayfasının güncelleştirilmiş albüm verilerini veritabanına kaydettiğini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="707cf-319">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-320">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-320">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-321">URL 'YI **/Storemanager/Edit/1**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="707cf-322">Albüm başlığını **yüklenecek** şekilde değiştirin ve **Kaydet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="707cf-323">Albümün başlığının, Albümler listesinde gerçekten değiştirildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="707cf-324">![Bir albümü güncelleştirme](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Bir albümü güncelleştirme")</span><span class="sxs-lookup"><span data-stu-id="707cf-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="707cf-325">*Bir albümü güncelleştirme*</span><span class="sxs-lookup"><span data-stu-id="707cf-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="707cf-326">Alıştırma 4: oluşturma görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="707cf-327">Artık **Storemanagercontroller** **düzenleme** özelliğini desteklediğine göre, Bu alıştırmada, Mağaza yöneticilerinin uygulamaya yeni albümler eklemesine Izin vermek için create VIEW şablonu ekleme hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="707cf-328">Düzenleme işlevselliğiyle yaptığınız gibi, **Storemanagercontroller** sınıfı içinde iki ayrı yöntem kullanarak oluşturma senaryosunu uygulayacaksınız:</span><span class="sxs-lookup"><span data-stu-id="707cf-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="707cf-329">Mağaza yöneticileri ilk olarak **/Storemanager/Create** URL 'yi ziyaret ettiğinde bir eylem yöntemi boş bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="707cf-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="707cf-330">İkinci bir eylem yöntemi, mağaza yöneticisinin form içindeki **Kaydet** düğmesine tıkladığı ve DEĞERLERI bir http-post olarak **/Storemanager/Create** URL 'sine geri gönderdiği senaryoyu işleymeyecektir.</span><span class="sxs-lookup"><span data-stu-id="707cf-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="707cf-331">Görev 1-HTTP-GET Create action metodunu uygulama</span><span class="sxs-lookup"><span data-stu-id="707cf-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="707cf-332">Bu görevde, tüm tarzların ve sanatçıların bir listesini almak için Create ACTION yönteminin HTTP-GET sürümünü uygulayacaksınız, bu verileri bir **Storemanagerviewmodel** nesnesine paketleyip, daha sonra bir görünüm şablonuna geçirilecek.</span><span class="sxs-lookup"><span data-stu-id="707cf-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="707cf-333">**Kaynak/EX4-AddingACreateView/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="707cf-334">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="707cf-335">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="707cf-336">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="707cf-337">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="707cf-338">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="707cf-339">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="707cf-340">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="707cf-341">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="707cf-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="707cf-342">**Storemanagercontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="707cf-343">Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="707cf-344">**Oluşturma** eylemi Yöntem kodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707cf-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="707cf-345">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-EX4 StoreManagerController http-oluşturma EYLEMINI al*)</span><span class="sxs-lookup"><span data-stu-id="707cf-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="707cf-346">Görev 2-oluştur görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="707cf-347">Bu görevde, yeni (boş) bir albüm formu görüntüleyen oluştur görünüm şablonunu ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="707cf-348">**Oluşturma** eylemi yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="707cf-349">Bu işlem, Görünüm Ekle iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="707cf-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="707cf-350">Görünüm Ekle iletişim kutusunda görünüm adının **Oluştur**' u doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="707cf-351">**Türü kesin belirlenmiş görünüm oluştur** seçeneğini belirleyin ve **model sınıfı** açılır listesinden **Albüm (Mvcmusicstore. modeller)** öğesini seçin ve **Yapı iskelesi şablonu** açılır listesinden **Oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="707cf-352">Diğer alanları varsayılan değerlerine bırakın ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="707cf-353">![Oluşturma görünümü ekleme](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-Create-View. png")</span><span class="sxs-lookup"><span data-stu-id="707cf-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="707cf-354">*Oluşturma görünümü ekleme*</span><span class="sxs-lookup"><span data-stu-id="707cf-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="707cf-355">**Genreıd** ve **ArtistId** alanlarını aşağıda gösterildiği gibi bir açılan liste kullanacak şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="707cf-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="707cf-356">Görev 3-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="707cf-357">Bu görevde, **Storemanager** **oluşturma** görünümü sayfasının boş bir albüm formu görüntülediğini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="707cf-358">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-359">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-359">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-360">URL 'YI **/Storemanager/Create**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="707cf-361">Yeni albüm özelliklerini doldurmak için boş bir form görüntülendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="707cf-362">![Boş bir formla görünüm oluştur](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Boş bir formla görünüm oluştur")</span><span class="sxs-lookup"><span data-stu-id="707cf-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="707cf-363">*Boş bir formla görünüm oluştur*</span><span class="sxs-lookup"><span data-stu-id="707cf-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="707cf-364">Görev 4-HTTP-POST oluşturma eylemi yöntemi uygulama</span><span class="sxs-lookup"><span data-stu-id="707cf-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="707cf-365">Bu görevde, Kullanıcı **Kaydet** düğmesine tıkladığında çağrılacak olan Create ACTıON yönteminin http-post sürümünü uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="707cf-366">Yöntemi, yeni albümü veritabanına kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="707cf-367">Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="707cf-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="707cf-368">**Storemanagercontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="707cf-369">Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="707cf-370">**Http-post oluşturma** eylemi yöntemi kodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707cf-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="707cf-371">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-EX4 StoreManagerController http-oluşturma sonrası eylem*)</span><span class="sxs-lookup"><span data-stu-id="707cf-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="707cf-372">Oluşturma eylemi, önceki düzenleme eylemi yöntemine oldukça benzer, ancak nesneyi değiştirilmiş olarak ayarlamak yerine bağlamına ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="707cf-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="707cf-373">5\. Görev-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="707cf-374">Bu görevde, **Storemanager oluşturma** görünümü sayfasının yeni bir albüm oluşturup ardından Storemanager dizin görünümüne yönlendirmenizi sağlayan bir test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="707cf-375">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-376">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-376">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-377">URL 'YI **/Storemanager/Create**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="707cf-378">Tüm form alanlarını, aşağıdaki şekilde olduğu gibi yeni bir albüm için verilerle birlikte doldurabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="707cf-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="707cf-379">![Albüm oluşturma](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Albüm oluşturma")</span><span class="sxs-lookup"><span data-stu-id="707cf-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="707cf-380">*Albüm oluşturma*</span><span class="sxs-lookup"><span data-stu-id="707cf-380">*Creating an Album*</span></span>
3. <span data-ttu-id="707cf-381">Yeni oluşturduğunuz albümü içeren StoreManager dizin görünümüne yönlendirildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="707cf-382">![Yeni albüm oluşturuldu](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "Yeni albüm oluşturuldu")</span><span class="sxs-lookup"><span data-stu-id="707cf-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="707cf-383">*Yeni albüm oluşturuldu*</span><span class="sxs-lookup"><span data-stu-id="707cf-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="707cf-384">Alıştırma 5: Işlemeyi silme</span><span class="sxs-lookup"><span data-stu-id="707cf-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="707cf-385">Albümleri silme özelliği henüz uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="707cf-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="707cf-386">Bu alıştırmada ilgili olacak.</span><span class="sxs-lookup"><span data-stu-id="707cf-386">This is what this exercise will be about.</span></span> <span data-ttu-id="707cf-387">Daha önce olduğu gibi, **Storemanagercontroller** sınıfı içinde iki ayrı yöntem kullanarak silme senaryosunu uygulayacaksınız:</span><span class="sxs-lookup"><span data-stu-id="707cf-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="707cf-388">Bir eylem yönteminde bir onay formu görüntülenir</span><span class="sxs-lookup"><span data-stu-id="707cf-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="707cf-389">İkinci bir eylem yöntemi, form gönderimini işleyecek</span><span class="sxs-lookup"><span data-stu-id="707cf-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="707cf-390">Görev 1-HTTP-GET silme eylemini uygulama yöntemi</span><span class="sxs-lookup"><span data-stu-id="707cf-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="707cf-391">Bu görevde, albümün bilgilerini almak için silme eylemi yönteminin HTTP-Al sürümünü uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="707cf-392">**Kaynak/eX5-el Lingsilme/başlangıç/** klasör konumunda bulunan **Başlangıç** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="707cf-393">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="707cf-394">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="707cf-395">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="707cf-396">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="707cf-397">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="707cf-398">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="707cf-399">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="707cf-400">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="707cf-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="707cf-401">**Storemanagercontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="707cf-402">Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="707cf-403">Denetleyiciyi Sil eylemi, önceki depo ayrıntıları denetleyicisi eylemiyle tamamen aynıdır: URL 'de belirtilen **kimliği** kullanarak **Albüm** nesnesini veritabanından sorgular ve uygun **görünümü**döndürür.</span><span class="sxs-lookup"><span data-stu-id="707cf-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="707cf-404">Bunu yapmak için, HTTP-GET **Delete** ACTION yöntemi kodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707cf-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="707cf-405">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-eX5 Işleme SILME http-silme EYLEMINI al*)</span><span class="sxs-lookup"><span data-stu-id="707cf-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="707cf-406">**Silme** eylemi yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="707cf-407">Bu işlem, Görünüm Ekle iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="707cf-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="707cf-408">Görünüm Ekle iletişim kutusunda görünüm adının **silme**olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="707cf-409">Kesin olarak **belirlenmiş görünüm oluştur** seçeneğini belirleyin ve **model sınıfı** açılır listesinden **Albüm (Mvcmusicstore. modeller)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="707cf-410">**Yapı iskelesi şablonu** açılır listesinden **Sil** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="707cf-411">Diğer alanları varsayılan değerlerine bırakın ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="707cf-412">![Silme görünümü ekleme](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Silme görünümü ekleme")</span><span class="sxs-lookup"><span data-stu-id="707cf-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="707cf-413">*Silme görünümü ekleme*</span><span class="sxs-lookup"><span data-stu-id="707cf-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="707cf-414">Şablonu Sil, modeldeki tüm alanları gösterir.</span><span class="sxs-lookup"><span data-stu-id="707cf-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="707cf-415">Yalnızca albümün başlığını gösterebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-415">You will show only the album's title.</span></span> <span data-ttu-id="707cf-416">Bunu yapmak için, görünümün içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707cf-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="707cf-417">Görev 2-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="707cf-418">Bu görevde, **Storemanager** **silme** görünümü sayfasının bir onay silme formu görüntülediğini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="707cf-419">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-420">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-420">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-421">URL 'YI **/Storemanager**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="707cf-422">**Sil ' e** tıklayarak silinecek bir albüm seçin ve yeni görünümün karşıya yüklendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="707cf-423">![Bir albümü silme](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Bir albümü silme")</span><span class="sxs-lookup"><span data-stu-id="707cf-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="707cf-424">*Bir albümü silme*</span><span class="sxs-lookup"><span data-stu-id="707cf-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="707cf-425">Görev 3-HTTP-Delete silme eyleminin uygulanması yöntemi</span><span class="sxs-lookup"><span data-stu-id="707cf-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="707cf-426">Bu görevde, Kullanıcı **Sil** düğmesine tıkladığında çağrılacak silme EYLEMI yönteminin http-post sürümünü uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="707cf-427">Yöntemi, veritabanındaki albümü silmelidir.</span><span class="sxs-lookup"><span data-stu-id="707cf-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="707cf-428">Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="707cf-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="707cf-429">**Storemanagercontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="707cf-430">Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="707cf-431">**Http-post Delete** ACTION yöntemi kodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707cf-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="707cf-432">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-eX5 Işleme SILME http-SILME sonrası eylemi*)</span><span class="sxs-lookup"><span data-stu-id="707cf-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="707cf-433">Görev 4-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="707cf-434">Bu görevde, **Storemanager silme** görünümü sayfasının bir albümü silmesine ve sonra Storemanager dizin görünümüne yönlendirmenize olanak tanıyan test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="707cf-435">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-436">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-436">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-437">URL 'YI **/Storemanager**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="707cf-438">Sil ' e tıklayarak silinecek bir albümü seçin **.**</span><span class="sxs-lookup"><span data-stu-id="707cf-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="707cf-439">**Sil** düğmesine tıklayarak silmeyi onaylayın:</span><span class="sxs-lookup"><span data-stu-id="707cf-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="707cf-440">![Bir albümü silme](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Bir albümü silme")</span><span class="sxs-lookup"><span data-stu-id="707cf-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="707cf-441">*Bir albümü silme*</span><span class="sxs-lookup"><span data-stu-id="707cf-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="707cf-442">**Dizin** sayfasında görünmediğinden albümün silindiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="707cf-443">Alıştırma 6: doğrulama ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="707cf-444">Şu anda, yerinde oluşturduğunuz oluşturma ve düzenleme formları herhangi bir tür doğrulama gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="707cf-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="707cf-445">Kullanıcı gerekli bir alanı boş bırakır veya fiyat alanında harfler yazarsanız, alacağınız ilk hata veritabanından alınır.</span><span class="sxs-lookup"><span data-stu-id="707cf-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="707cf-446">Model sınıfınıza veri ek açıklamaları ekleyerek uygulamaya doğrulama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="707cf-447">Veri ek açıklamaları, model özelliklerine uygulanmasını istediğiniz kuralların açıklanarak ASP.NET MVC, kullanıcılara uygun iletileri zorlamaya ve görüntülemeye yönelik bir işlem gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="707cf-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="707cf-448">Görev 1-veri ek açıklamaları ekleme</span><span class="sxs-lookup"><span data-stu-id="707cf-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="707cf-449">Bu görevde, uygun olduğunda oluşturma ve düzenleme sayfasının doğrulama iletilerini görüntülemesi için, albüm modeline veri ek açıklamaları ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="707cf-450">Basit bir model sınıfı için, bir veri ek açıklaması eklemek, **System. ComponentModel. DataAnnotation**için bir **using** açıklaması eklenerek ve ardından uygun özelliklere bir **[Required]** özniteliği yerleştirerek işlenir.</span><span class="sxs-lookup"><span data-stu-id="707cf-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="707cf-451">Aşağıdaki örnek, **ad** özelliğini görünümünde gerekli bir alan haline getirir.</span><span class="sxs-lookup"><span data-stu-id="707cf-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="707cf-452">Bu, Varlık Veri Modeli oluşturulduğu bu uygulama gibi durumlarda biraz daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="707cf-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="707cf-453">Doğrudan model sınıflarına veri ek açıklamaları eklediyseniz, modeli veritabanından güncelleştirirseniz bunların üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="707cf-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="707cf-454">Bunun yerine, ek açıklamaları tutmak için var olan ve **[Metadatatype]** özniteliğini kullanan model sınıflarıyla ilişkili olan meta veri kısmi sınıflarının kullanımını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="707cf-455">**Kaynak/Ex6-AddingValidation/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="707cf-456">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="707cf-457">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="707cf-458">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="707cf-459">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="707cf-460">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="707cf-461">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="707cf-462">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="707cf-463">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="707cf-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="707cf-464">**Modeller** klasöründen **Album.cs** öğesini açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="707cf-465">**Album.cs** içeriğini vurgulanan kodla değiştirin, böylece aşağıdakine benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="707cf-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="707cf-466">Satır **[DisplayFormat (ConvertEmptyStringToNull = false)]** , veri alanı veri kaynağında güncellendiğinde, modeldeki boş dizelerin null olarak dönüştürülmeyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="707cf-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="707cf-467">Bu ayar, Entity Framework veri ek açıklaması alanları doğrulamaktan önce modele null değerler atarken bir özel durumu ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="707cf-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="707cf-468">(Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex6 albüm meta verileri kısmi sınıfı*)</span><span class="sxs-lookup"><span data-stu-id="707cf-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="707cf-469">Bu **albümün** kısmi sınıfı, veri ek açıklamaları Için **albümümetadata** sınıfına Işaret eden bir **metadatatype** özniteliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="707cf-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="707cf-470">Bunlar, albüm modeline ek açıklama eklemek için kullandığınız bazı veri ek açıklama öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="707cf-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="707cf-471">Gerekli-özelliğin gerekli bir alan olduğunu belirtir</span><span class="sxs-lookup"><span data-stu-id="707cf-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="707cf-472">DisplayName-form alanlarında ve doğrulama iletilerinde kullanılacak metni tanımlar</span><span class="sxs-lookup"><span data-stu-id="707cf-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="707cf-473">DisplayFormat-veri alanlarının nasıl görüntülendiğini ve biçimlendirildiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="707cf-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="707cf-474">StringLength-dize alanı için maksimum uzunluğu tanımlar</span><span class="sxs-lookup"><span data-stu-id="707cf-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="707cf-475">Range-sayısal bir alan için en yüksek ve en küçük değeri verir</span><span class="sxs-lookup"><span data-stu-id="707cf-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="707cf-476">ScaffoldColumn-düzenleyici formlarından alanları gizlemeye Izin verir</span><span class="sxs-lookup"><span data-stu-id="707cf-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="707cf-477">Görev 2-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="707cf-478">Bu görevde, son görevde seçilen görünen adları kullanarak sayfaların oluşturulması ve düzenlenmesi alanlarını doğruladığını test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="707cf-479">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="707cf-480">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-480">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-481">URL 'YI **/Storemanager/Create**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="707cf-482">Görünen adların, kısmi sınıftaki **(albümle Ilgili** **Albüm sanatı URL 'si** gibi) eşleşen olanlarla eşleştiğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="707cf-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="707cf-483">Formu doldurmadan **Oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="707cf-484">Karşılık gelen doğrulama iletilerini almanızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="707cf-485">![Oluştur sayfasındaki doğrulanan alanlar](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Oluştur sayfasındaki doğrulanan alanlar")</span><span class="sxs-lookup"><span data-stu-id="707cf-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="707cf-486">*Oluştur sayfasındaki doğrulanan alanlar*</span><span class="sxs-lookup"><span data-stu-id="707cf-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="707cf-487">Aynı olduğunu, **düzenleme** sayfasıyla aynı olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="707cf-488">URL 'YI **/Storemanager/Edit/1** olarak değiştirin ve görünen adların kısmi sınıftaki ( **albüm için albümünüz yerine albüm sanatı URL 'si** **gibi) eşleşip**eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="707cf-489">**Başlığı** ve **fiyat** alanlarını boşaltın ve **Kaydet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="707cf-490">Karşılık gelen doğrulama iletilerini almanızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-490">Verify that you get the corresponding validation messages.</span></span>

    ![Düzenleme sayfasında doğrulanan alanlar](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="707cf-492">*Düzenleme sayfasında doğrulanan alanlar*</span><span class="sxs-lookup"><span data-stu-id="707cf-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="707cf-493">Alıştırma 7: Istemci tarafında unobtrusive jQuery kullanma</span><span class="sxs-lookup"><span data-stu-id="707cf-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="707cf-494">Bu alıştırmada, istemci tarafında MVC 4 unobtrusive doğrulamasını nasıl etkinleştireceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="707cf-495">Unobtrusive jQuery, satır içi istemci betikleri dahil etmek yerine sunucuda eylem yöntemlerini çağırmak için Data-Ajax ön eki JavaScript 'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="707cf-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="707cf-496">Görev 1-Obtrusive jQuery 'ı etkinleştirmeden önce uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="707cf-497">Bu görevde, her iki doğrulama modelini de karşılaştırmak için jQuery 'i eklemeden önce uygulamayı çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="707cf-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="707cf-498">**Kaynak/Ex7-UnobtrusivejQueryValidation/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="707cf-499">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="707cf-500">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="707cf-501">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="707cf-502">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="707cf-503">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="707cf-504">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="707cf-505">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="707cf-506">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="707cf-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="707cf-507">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="707cf-508">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-508">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-509">Doğrulama iletilerini aldığını doğrulamak için **/Storemanager/Create** ' e gözatıp Formu doldurmadan **Oluştur** ' a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="707cf-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="707cf-510">![İstemci doğrulaması devre dışı](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "İstemci doğrulaması devre dışı")</span><span class="sxs-lookup"><span data-stu-id="707cf-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="707cf-511">*İstemci doğrulaması devre dışı*</span><span class="sxs-lookup"><span data-stu-id="707cf-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="707cf-512">Tarayıcıda, HTML kaynak kodunu açın:</span><span class="sxs-lookup"><span data-stu-id="707cf-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="707cf-513">Görev 2-Obtrusive Istemci doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="707cf-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="707cf-514">Bu görevde, varsayılan olarak tüm New ASP.NET MVC 4 projelerinde false olarak ayarlanmış olan **Web. config** dosyasından jQuery **unobtrusive istemci doğrulamasını** etkinleştirecektir.</span><span class="sxs-lookup"><span data-stu-id="707cf-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="707cf-515">Bunlara ek olarak, jQuery 'in Istemci doğrulaması işini sorunsuz hale getirmek için gerekli betiklerin başvurularını eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="707cf-516">Proje kökünde **Web. config** dosyasını açın ve **ClientValidationEnabled** ve **Unobtrusivejavascriptenabled** anahtarları değerlerinin **true**olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="707cf-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="707cf-517">Aynı sonuçları almak için Global.asax.cs adresindeki kodla istemci doğrulamasını da etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="707cf-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="707cf-518">**HtmlHelper. ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="707cf-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="707cf-519">Ek olarak, özel bir davranışa sahip olmak için herhangi bir denetleyiciye ClientValidationEnabled özniteliğini de atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="707cf-520">**Views\storemanager**'da **Create. cshtml** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="707cf-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="707cf-521">Aşağıdaki betik dosyalarının **jQuery. Validate** ve **jQuery. Validate. unobtrusive**' &quot; **~/paketles/jqueryval**&quot; demeti aracılığıyla görünümde başvurulduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="707cf-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view through the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="707cf-522">Tüm bu jQuery kitaplıkları MVC 4 yeni projelere dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="707cf-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="707cf-523">Projenin **/Scripts** klasöründe daha fazla kitaplık bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="707cf-524">Bu doğrulama kitaplıklarının çalışmasını sağlamak için jQuery Framework kitaplığına bir başvuru eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="707cf-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="707cf-525">Bu başvuru **\_Layout. cshtml** dosyasına zaten eklendiğinden, bu görünümü bu görünüme eklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="707cf-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="707cf-526">Görev 3-uygulamayı unobtrusive doğrulamasını kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="707cf-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="707cf-527">Bu görevde, Kullanıcı yeni bir albüm oluşturduğunda **Storemanager** oluşturma görünüm şablonu jQuery kitaplıklarını kullanarak istemci tarafı doğrulaması gerçekleştireceğini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="707cf-528">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="707cf-529">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="707cf-529">The project starts in the Home page.</span></span> <span data-ttu-id="707cf-530">Doğrulama iletilerini aldığını doğrulamak için **/Storemanager/Create** ' e gözatıp Formu doldurmadan **Oluştur** ' a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="707cf-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="707cf-531">![JQuery özellikli istemci doğrulaması](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "JQuery özellikli istemci doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="707cf-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="707cf-532">*JQuery özellikli istemci doğrulaması*</span><span class="sxs-lookup"><span data-stu-id="707cf-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="707cf-533">Tarayıcıda, oluştur görünümü için kaynak kodunu açın:</span><span class="sxs-lookup"><span data-stu-id="707cf-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="707cf-534">Her istemci doğrulama kuralı için unobtrusive jQuery, Data-Val-*RuleName*=&quot;*Message*&quot;olan bir öznitelik ekliyor.</span><span class="sxs-lookup"><span data-stu-id="707cf-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="707cf-535">Aşağıda, istemci doğrulaması gerçekleştirmek için, bir Untastrusjquery 'ın HTML giriş alanına eklediği etiketlerin listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="707cf-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="707cf-536">Veri-Val</span><span class="sxs-lookup"><span data-stu-id="707cf-536">Data-val</span></span>
   > - <span data-ttu-id="707cf-537">Veri-değer-sayı</span><span class="sxs-lookup"><span data-stu-id="707cf-537">Data-val-number</span></span>
   > - <span data-ttu-id="707cf-538">Veri Val aralığı</span><span class="sxs-lookup"><span data-stu-id="707cf-538">Data-val-range</span></span>
   > - <span data-ttu-id="707cf-539">Veri-değer-aralığı-min/Data-Val-Range-Max</span><span class="sxs-lookup"><span data-stu-id="707cf-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="707cf-540">Veri-Val-gerekli</span><span class="sxs-lookup"><span data-stu-id="707cf-540">Data-val-required</span></span>
   > - <span data-ttu-id="707cf-541">Veri-değer uzunluğu</span><span class="sxs-lookup"><span data-stu-id="707cf-541">Data-val-length</span></span>
   > - <span data-ttu-id="707cf-542">Veri-değer-Uzunluk-Max/Data-Val-length-min</span><span class="sxs-lookup"><span data-stu-id="707cf-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="707cf-543">Tüm veri değerleri model **veri ek açıklaması**ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="707cf-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="707cf-544">Daha sonra, sunucu tarafında çalışan tüm mantık istemci tarafında çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="707cf-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="707cf-545">Örneğin, Price özniteliği modelde aşağıdaki veri ek açıklamasına sahiptir:</span><span class="sxs-lookup"><span data-stu-id="707cf-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="707cf-546">Unobtrusive jQuery kullandıktan sonra, oluşturulan kod:</span><span class="sxs-lookup"><span data-stu-id="707cf-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="707cf-547">Özet</span><span class="sxs-lookup"><span data-stu-id="707cf-547">Summary</span></span>

<span data-ttu-id="707cf-548">Bu uygulamalı Laboratuvarı tamamlayarak, kullanıcıların veritabanında depolanan verileri aşağıdakilerin kullanımıyla nasıl değiştirdiklerini öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="707cf-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="707cf-549">Dizin, oluşturma, düzenleme, silme gibi denetleyici eylemleri</span><span class="sxs-lookup"><span data-stu-id="707cf-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="707cf-550">ASP.NET MVC 'nin bir HTML tablosunda özellikleri görüntülemek için yapı iskelesi özelliği</span><span class="sxs-lookup"><span data-stu-id="707cf-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="707cf-551">Kullanıcı deneyimini geliştirmek için özel HTML Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="707cf-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="707cf-552">HTTP-GET veya HTTP-POST çağrılarına tepki veren eylem yöntemleri</span><span class="sxs-lookup"><span data-stu-id="707cf-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="707cf-553">Oluşturma ve düzenleme gibi benzer görünüm şablonlarına yönelik paylaşılan bir düzenleyici şablonu</span><span class="sxs-lookup"><span data-stu-id="707cf-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="707cf-554">Açılan öğeler gibi form öğeleri</span><span class="sxs-lookup"><span data-stu-id="707cf-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="707cf-555">Model doğrulaması için veri ek açıklamaları</span><span class="sxs-lookup"><span data-stu-id="707cf-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="707cf-556">JQuery unobtrusive kitaplığı kullanarak istemci tarafı doğrulaması</span><span class="sxs-lookup"><span data-stu-id="707cf-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="707cf-557">Ek A: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="707cf-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="707cf-558">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="707cf-559">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="707cf-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="707cf-560">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin.</span><span class="sxs-lookup"><span data-stu-id="707cf-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="707cf-561">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="707cf-562">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-562">Click on **Install Now**.</span></span> <span data-ttu-id="707cf-563">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="707cf-564">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="707cf-565">![Visual Studio Express yüklensin](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="707cf-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="707cf-566">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="707cf-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="707cf-567">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="707cf-569">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="707cf-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="707cf-570">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-570">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="707cf-572">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="707cf-572">*Installation progress*</span></span>
6. <span data-ttu-id="707cf-573">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-573">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="707cf-575">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="707cf-575">*Installation completed*</span></span>
7. <span data-ttu-id="707cf-576">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="707cf-577">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="707cf-579">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="707cf-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="707cf-580">Ek B: kod parçacıklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="707cf-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="707cf-581">Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707cf-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="707cf-582">Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="707cf-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="707cf-583">![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")</span><span class="sxs-lookup"><span data-stu-id="707cf-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="707cf-584">*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*</span><span class="sxs-lookup"><span data-stu-id="707cf-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="707cf-585">***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***</span><span class="sxs-lookup"><span data-stu-id="707cf-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="707cf-586">Kodu eklemek istediğiniz yere imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="707cf-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="707cf-587">Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).</span><span class="sxs-lookup"><span data-stu-id="707cf-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="707cf-588">IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="707cf-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="707cf-589">Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="707cf-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="707cf-590">Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="707cf-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="707cf-591">![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="707cf-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="707cf-592">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="707cf-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="707cf-593">![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="707cf-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="707cf-594">*Vurgulanan parçacığı seçmek için Tab tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="707cf-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="707cf-595">![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")</span><span class="sxs-lookup"><span data-stu-id="707cf-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="707cf-596">*Sekmeye tekrar basın ve kod parçacığı genişletilir*</span><span class="sxs-lookup"><span data-stu-id="707cf-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="707cf-597">***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="707cf-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="707cf-598">Kod parçacığını eklemek istediğiniz yere sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707cf-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="707cf-599">Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="707cf-600">Listeden tıklatarak ilgili kod parçacığını seçin.</span><span class="sxs-lookup"><span data-stu-id="707cf-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="707cf-601">![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")</span><span class="sxs-lookup"><span data-stu-id="707cf-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="707cf-602">*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*</span><span class="sxs-lookup"><span data-stu-id="707cf-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="707cf-603">![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Listeden tıklatarak ilgili kod parçacığını seçin")</span><span class="sxs-lookup"><span data-stu-id="707cf-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="707cf-604">*Listeden tıklatarak ilgili kod parçacığını seçin*</span><span class="sxs-lookup"><span data-stu-id="707cf-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
