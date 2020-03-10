---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework yapı Iskelesi ve geçişleri | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 denetleyici yöntemlerine alışkın değilseniz veya &quot;yardımcıları, formları ve doğrulama&quot; uygulamalı laboratuvarını tamamladıysanız, farkında olmanız gerekir...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598905"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="3bea7-103">ASP.NET MVC 4 Entity Framework İskele Oluşturma ve Geçişler</span><span class="sxs-lookup"><span data-stu-id="3bea7-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="3bea7-104">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="3bea7-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="3bea7-105">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="3bea7-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="3bea7-106">ASP.NET MVC 4 denetleyici yöntemlerine alışkın değilseniz veya &quot;yardımcıları, formları ve doğrulama&quot; uygulamalı laboratuvarını tamamladıysanız, uygulama arasında tekrarlandığı herhangi bir veri varlığını oluşturma, güncelleştirme, listeleme ve kaldırma mantığının birçoğunun olduğunu bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that many of the logic to create, update, list and remove any data entity it is repeated among the application.</span></span> <span data-ttu-id="3bea7-107">Bunun değil, modelinizde yapılacak birkaç sınıf varsa, her bir varlık işlemi için POST ve GET eylem yöntemlerini ve görünümlerin her birini yazmak için önemli bir zaman harcamanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="3bea7-108">Bu laboratuvarda, uygulamanızın CRUD (oluşturma, okuma, güncelleştirme ve silme) temelini otomatik olarak oluşturmak için ASP.NET MVC 4 scafkatını nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="3bea7-109">Basit bir model sınıfından başlayarak ve tek bir kod satırı yazmadan, tüm CRUD işlemlerini ve tüm gerekli görünümleri içerecek bir denetleyici oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3bea7-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="3bea7-110">Basit çözümü oluşturup çalıştırdıktan sonra, veri işleme için MVC mantığı ve görünümleri ile birlikte uygulama veritabanının oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="3bea7-111">Ayrıca, uygulamanın tamamında model güncelleştirmeleri gerçekleştirmek için Entity Framework geçişlerini kullanmanın ne kadar kolay olduğunu öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="3bea7-112">Entity Framework geçişleri, model basit adımlarla değiştirildikten sonra veritabanınızı değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="3bea7-113">Bunların hepsi göz önünde bulundurularak, ASP.NET MVC 4 ' ün en son özelliklerinden yararlanarak web uygulamalarını daha verimli bir şekilde oluşturup koruyabileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="3bea7-114">Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit yayımlarından](https://aka.ms/webcamps-training-kit)erişilebilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="3bea7-115">Bu laboratuvara özgü proje, [ASP.NET MVC 4 ' te yapı iskelesi ve geçişleri Entity Framework](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="3bea7-116">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="3bea7-116">Objectives</span></span>

<span data-ttu-id="3bea7-117">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="3bea7-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="3bea7-118">Denetleyicilerde CRUD işlemleri için ASP.NET scafkatlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="3bea7-119">Entity Framework geçişleri kullanarak veritabanı modelini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="3bea7-120">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3bea7-120">Prerequisites</span></span>

<span data-ttu-id="3bea7-121">Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3bea7-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="3bea7-122">[Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).</span><span class="sxs-lookup"><span data-stu-id="3bea7-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="3bea7-123">Kurulum</span><span class="sxs-lookup"><span data-stu-id="3bea7-123">Setup</span></span>

<span data-ttu-id="3bea7-124">**Kod parçacıklarını yükleme**</span><span class="sxs-lookup"><span data-stu-id="3bea7-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="3bea7-125">Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3bea7-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="3bea7-126">Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="3bea7-127">Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek B: kod parçacıkları&quot;kullanarak](#AppendixB) bu belgedeki eke başvurabilirsiniz &quot;.</span><span class="sxs-lookup"><span data-stu-id="3bea7-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="3bea7-128">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="3bea7-128">Exercises</span></span>

<span data-ttu-id="3bea7-129">Aşağıdaki alıştırma, bu uygulamalı Laboratuvarı yapar:</span><span class="sxs-lookup"><span data-stu-id="3bea7-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="3bea7-130">Entity Framework geçişleri ile ASP.NET MVC 4 Scafkatlaması kullanma</span><span class="sxs-lookup"><span data-stu-id="3bea7-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="3bea7-131">Bu alıştırma, Alıştırmayı tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="3bea7-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="3bea7-132">Bu çözümü, alıştırmaya yönelik ek yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>

<span data-ttu-id="3bea7-133">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **30 dakika**</span><span class="sxs-lookup"><span data-stu-id="3bea7-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="3bea7-134">Alıştırma 1: Entity Framework geçişleri ile ASP.NET MVC 4 Scafkatlama kullanma</span><span class="sxs-lookup"><span data-stu-id="3bea7-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="3bea7-135">ASP.NET MVC yapı iskelesi, CRUD işlemlerini standartlaştırılmış bir şekilde oluşturmanın hızlı bir yolunu sağlar. bu sayede uygulamanızın veritabanı katmanıyla etkileşime geçmesini sağlayan gerekli mantık oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3bea7-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="3bea7-136">Bu alıştırmada, CRUD yöntemlerini oluşturmak için önce kod ile ASP.NET MVC 4 scafkatlamayı nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="3bea7-137">Daha sonra, Entity Framework geçişlerini kullanarak modelinizin değişiklikleri uygulamayı nasıl güncelleştireceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="3bea7-138">Görev 1-yapı Iskelesi kullanarak yeni bir ASP.NET MVC 4 projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3bea7-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="3bea7-139">Zaten açık değilse, **Visual Studio 2012**' u başlatın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="3bea7-140">**Dosya Seç | Yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="3bea7-140">Select **File | New Project**.</span></span> <span data-ttu-id="3bea7-141">Yeni proje iletişim kutusunda, **görsel C# altında | Web** bölümünde **ASP.NET MVC 4 Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="3bea7-142">Projeyi **MVC4andEFMigrations** olarak adlandırın ve bu laboratuvarın **Source\ex1-usingmvc4scaffoldıngefgeçişler** klasörüne ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="3bea7-143">**Çözüm adını** **Başlangıç** olarak ayarlayın ve **çözüm için dizin oluşturma** onay işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3bea7-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="3bea7-144">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-144">Click **OK**.</span></span>

    <span data-ttu-id="3bea7-145">![Yeni ASP.NET MVC 4 projesi Iletişim kutusu](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "Yeni ASP.NET MVC 4 projesi Iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="3bea7-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="3bea7-146">*Yeni ASP.NET MVC 4 projesi Iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="3bea7-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="3bea7-147">**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** şablonunu seçin ve **Razor** 'nin seçili **Görünüm altyapısı**olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3bea7-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="3bea7-148">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="3bea7-149">![Yeni ASP.NET MVC 4 Internet uygulaması](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "Yeni ASP.NET MVC 4 Internet uygulaması")</span><span class="sxs-lookup"><span data-stu-id="3bea7-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="3bea7-150">*Yeni ASP.NET MVC 4 Internet uygulaması*</span><span class="sxs-lookup"><span data-stu-id="3bea7-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="3bea7-151">Çözüm Gezgini **modeller** ' a sağ tıklayın ve Ekle | ' yi seçin.Basit bir sınıf kişisi (POCO) oluşturmak için sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3bea7-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="3bea7-152">**Kişiyi** adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="3bea7-153">Kişi sınıfını açın ve aşağıdaki özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="3bea7-154">(Kod parçacığı- *ASP.NET MVC 4 ve Entity Framework geçişleri-Ex1 Person özellikleri*)</span><span class="sxs-lookup"><span data-stu-id="3bea7-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. <span data-ttu-id="3bea7-155">Oluştur 'a tıklayın **|** Değişiklikleri kaydetmek ve projeyi derlemek Için çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3bea7-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="3bea7-156">![Uygulamayı oluşturma](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Uygulamayı oluşturma")</span><span class="sxs-lookup"><span data-stu-id="3bea7-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="3bea7-157">*Uygulamayı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="3bea7-157">*Building the Application*</span></span>
7. <span data-ttu-id="3bea7-158">Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Denetleyici**.</span><span class="sxs-lookup"><span data-stu-id="3bea7-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="3bea7-159">Denetleyiciyi *personcontroller* olarak adlandırın ve aşağıdaki değerlerle **Yapı iskelesi seçeneklerini** doldurun.</span><span class="sxs-lookup"><span data-stu-id="3bea7-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

   1. <span data-ttu-id="3bea7-160">**Şablon** açılan listesinde, **Entity Framework seçeneğini kullanarak okuma/yazma eylemleri ve görünümleri ile MVC denetleyicisi** ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
   2. <span data-ttu-id="3bea7-161">**Model sınıfı** aşağı açılan listesinde **kişi** sınıfını seçin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
   3. <span data-ttu-id="3bea7-162">**Veri bağlamı sınıfı** listesinde **yeni veri bağlamı&lt;...&gt;** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="3bea7-163">Herhangi bir ad seçin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-163">Choose any name and click **OK**.</span></span>
   4. <span data-ttu-id="3bea7-164">**Görünümler** açılan listesinde, **Razor** 'nin seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3bea7-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

      <span data-ttu-id="3bea7-165">![Yapı iskelesi ile kişi denetleyicisi ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Yapı iskelesi ile kişi denetleyicisi ekleme")</span><span class="sxs-lookup"><span data-stu-id="3bea7-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

      <span data-ttu-id="3bea7-166">*Yapı iskelesi ile kişi denetleyicisi ekleme*</span><span class="sxs-lookup"><span data-stu-id="3bea7-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="3bea7-167">Yeni denetleyiciyi yapı iskelesi içeren bir kişiye oluşturmak için **Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="3bea7-168">Artık denetleyici eylemlerinin yanı sıra görünümleri de oluşturmuş oldunuz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="3bea7-169">![Yapı iskelesi ile kişi denetleyicisi oluşturduktan sonra](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "Yapı iskelesi ile kişi denetleyicisi oluşturduktan sonra")</span><span class="sxs-lookup"><span data-stu-id="3bea7-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="3bea7-170">*Yapı iskelesi ile kişi denetleyicisi oluşturduktan sonra*</span><span class="sxs-lookup"><span data-stu-id="3bea7-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="3bea7-171">**Personcontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-171">Open **PersonController** class.</span></span> <span data-ttu-id="3bea7-172">Tam CRUD eylem yöntemlerinin otomatik olarak oluşturulduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

   <span data-ttu-id="3bea7-173">![Kişi denetleyicisinin içinde](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Kişi denetleyicisinin içinde")</span><span class="sxs-lookup"><span data-stu-id="3bea7-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

   <span data-ttu-id="3bea7-174">*Kişi denetleyicisinin içinde*</span><span class="sxs-lookup"><span data-stu-id="3bea7-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="3bea7-175">Görev 2-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3bea7-175">Task 2- Running the application</span></span>

<span data-ttu-id="3bea7-176">Bu noktada, veritabanı henüz oluşturulmamış.</span><span class="sxs-lookup"><span data-stu-id="3bea7-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="3bea7-177">Bu görevde, uygulamayı ilk kez çalıştıracak ve CRUD işlemlerini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="3bea7-178">Veritabanı, Code First ile anında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3bea7-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="3bea7-179">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="3bea7-180">Tarayıcıda, kişi sayfasını açmak için URL 'ye **/Person** ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="3bea7-181">![Uygulamanın ilk çalıştırması](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Uygulamanın ilk çalıştırması")</span><span class="sxs-lookup"><span data-stu-id="3bea7-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="3bea7-182">*Uygulama: ilk çalıştırma*</span><span class="sxs-lookup"><span data-stu-id="3bea7-182">*Application: first run*</span></span>
3. <span data-ttu-id="3bea7-183">Artık kişi sayfalarını araştırıp CRUD işlemlerini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="3bea7-184">Yeni bir kişi eklemek için **Yeni oluştur** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="3bea7-185">Ad ve soyadı girin ve **Oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="3bea7-186">![Yeni bir kişi ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Yeni bir kişi ekleme")</span><span class="sxs-lookup"><span data-stu-id="3bea7-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="3bea7-187">*Yeni bir kişi ekleme*</span><span class="sxs-lookup"><span data-stu-id="3bea7-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="3bea7-188">Kişinin listesinde, öğeleri silebilir, düzenleyebilir veya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="3bea7-189">![kişi listesi](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "kişi listesi")</span><span class="sxs-lookup"><span data-stu-id="3bea7-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="3bea7-190">*Kişi listesi*</span><span class="sxs-lookup"><span data-stu-id="3bea7-190">*Person list*</span></span>
    3. <span data-ttu-id="3bea7-191">Kişinin ayrıntılarını açmak için **Ayrıntılar** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="3bea7-192">![Kişinin ayrıntıları](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Kişinin ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="3bea7-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="3bea7-193">*Kişinin ayrıntıları*</span><span class="sxs-lookup"><span data-stu-id="3bea7-193">*Person's details*</span></span>
4. <span data-ttu-id="3bea7-194">Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="3bea7-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="3bea7-195">Tek bir kod satırı yazmak zorunda kalmadan, uygulamanız genelinde, modelden görünümler 'e kadar tüm CRUD 'yi oluşturduğunuza dikkat edin!</span><span class="sxs-lookup"><span data-stu-id="3bea7-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="3bea7-196">Görev 3-Entity Framework geçişleri kullanarak veritabanını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3bea7-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="3bea7-197">Bu görevde veritabanını Entity Framework geçişleri kullanarak güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="3bea7-198">Entity Framework geçişleri özelliğini kullanarak, modeli değiştirme ve veritabanlarınızdaki değişiklikleri yansıtan ne kadar kolay olduğunu fark edersiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="3bea7-199">Paket Yöneticisi konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-199">Open the Package Manager Console.</span></span> <span data-ttu-id="3bea7-200">**Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-200">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="3bea7-201">Paket Yöneticisi konsolunda aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="3bea7-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="3bea7-202">PMC</span><span class="sxs-lookup"><span data-stu-id="3bea7-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="3bea7-203">![Geçişleri etkinleştirme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Geçişleri etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="3bea7-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="3bea7-204">*Geçişleri etkinleştirme*</span><span class="sxs-lookup"><span data-stu-id="3bea7-204">*Enabling migrations*</span></span>

    <span data-ttu-id="3bea7-205">Enable-Migration komutu, veritabanını başlatmak için bir komut dosyası içeren **geçişler** klasörünü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3bea7-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="3bea7-206">![Geçişler klasörü](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Geçişler klasörü")</span><span class="sxs-lookup"><span data-stu-id="3bea7-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="3bea7-207">*Geçişler klasörü*</span><span class="sxs-lookup"><span data-stu-id="3bea7-207">*Migrations folder*</span></span>
3. <span data-ttu-id="3bea7-208">**Configuration.cs** dosyasını geçişler klasöründe açın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="3bea7-209">Sınıf oluşturucusunu bulun ve **Automaticmigrationsenabled** değerini *true*olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. <span data-ttu-id="3bea7-210">Kişi sınıfını açın ve kişinin ikinci adı için bir öznitelik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="3bea7-211">Bu yeni öznitelikle, modeli değiştiriyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-211">With this new attribute, you are changing the model.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. <span data-ttu-id="3bea7-212">**Derlemeyi Seç |** Uygulamayı oluşturmak için menüdeki çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3bea7-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="3bea7-213">![Uygulamayı oluşturma](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Uygulamayı oluşturma")</span><span class="sxs-lookup"><span data-stu-id="3bea7-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="3bea7-214">*Uygulamayı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="3bea7-214">*Building the application*</span></span>
6. <span data-ttu-id="3bea7-215">Paket Yöneticisi konsolunda aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="3bea7-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="3bea7-216">PMC</span><span class="sxs-lookup"><span data-stu-id="3bea7-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="3bea7-217">Bu komut, veri nesnelerinde değişikliklere bakar ve sonra veritabanına uygun şekilde değişiklik yapmak için gerekli komutları ekler.</span><span class="sxs-lookup"><span data-stu-id="3bea7-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="3bea7-218">![İkinci adı ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "İkinci adı ekleme")</span><span class="sxs-lookup"><span data-stu-id="3bea7-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="3bea7-219">*İkinci adı ekleme*</span><span class="sxs-lookup"><span data-stu-id="3bea7-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="3bea7-220">Seçim Değişiklik güncelleştirmesiyle bir SQL betiği oluşturmak için aşağıdaki komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="3bea7-221">Bu, veritabanını el ile güncelleştirmenizi sağlar (Bu durumda gerekli değildir) veya değişiklikleri diğer veritabanlarına uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3bea7-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="3bea7-222">PMC</span><span class="sxs-lookup"><span data-stu-id="3bea7-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="3bea7-223">![SQL betiği oluşturma](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL betiği oluşturma")</span><span class="sxs-lookup"><span data-stu-id="3bea7-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="3bea7-224">*SQL betiği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="3bea7-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="3bea7-225">![SQL betiği güncelleştirmesi](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL betiği güncelleştirmesi")</span><span class="sxs-lookup"><span data-stu-id="3bea7-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="3bea7-226">*SQL betiği güncelleştirmesi*</span><span class="sxs-lookup"><span data-stu-id="3bea7-226">*SQL Script update*</span></span>
8. <span data-ttu-id="3bea7-227">Paket Yöneticisi konsolunda, veritabanını güncelleştirmek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="3bea7-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="3bea7-228">PMC</span><span class="sxs-lookup"><span data-stu-id="3bea7-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="3bea7-229">![Veritabanı güncelleştiriliyor](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Veritabanını Güncelleştirme")</span><span class="sxs-lookup"><span data-stu-id="3bea7-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="3bea7-230">*Veritabanı güncelleştiriliyor*</span><span class="sxs-lookup"><span data-stu-id="3bea7-230">*Updating the Database*</span></span>

    <span data-ttu-id="3bea7-231">Bu, **kişi** sınıfının geçerli tanımıyla eşleşecek şekilde **kişiler** tablosuna **MiddleName** sütununu ekler.</span><span class="sxs-lookup"><span data-stu-id="3bea7-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="3bea7-232">Veritabanı güncelleştirildikten sonra denetleyici klasörüne sağ tıklayın ve Ekle | ' yi seçin.Kişi denetleyicisini yeniden eklemek için denetleyici (aynı değerlerle tamamlanır).</span><span class="sxs-lookup"><span data-stu-id="3bea7-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="3bea7-233">Bu işlem, yeni özniteliği ekleyen mevcut yöntemleri ve görünümleri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="3bea7-234">![Denetleyici güncelleştirmesi ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Denetleyici güncelleştirmesi ekleme")</span><span class="sxs-lookup"><span data-stu-id="3bea7-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="3bea7-235">*Denetleyiciyi güncelleştirme*</span><span class="sxs-lookup"><span data-stu-id="3bea7-235">*Updating the controller*</span></span>
10. <span data-ttu-id="3bea7-236">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-236">Click **Add**.</span></span> <span data-ttu-id="3bea7-237">Sonra, **PersonController.cs üzerine yazma** değerlerini ve **Ilişkili görünümlerin üzerine yazın** ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

   ![Denetleyici üzerine yazma ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   <span data-ttu-id="3bea7-239">*Denetleyiciyi güncelleştirme*</span><span class="sxs-lookup"><span data-stu-id="3bea7-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="3bea7-240">Task4-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3bea7-240">Task4- Running the application</span></span>

1. <span data-ttu-id="3bea7-241">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="3bea7-242">**/Person**öğesini açın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-242">Open **/Person**.</span></span> <span data-ttu-id="3bea7-243">Verilerin korunduğu, ortadaki Ad sütununun eklendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="3bea7-244">![İkinci ad eklendi](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "İkinci ad eklendi")</span><span class="sxs-lookup"><span data-stu-id="3bea7-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="3bea7-245">*İkinci ad eklendi*</span><span class="sxs-lookup"><span data-stu-id="3bea7-245">*Middle Name added*</span></span>
3. <span data-ttu-id="3bea7-246">**Düzenle**' ye tıklarsanız, geçerli kişiye bir göbek adı ekleyebileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="3bea7-247">![Göbek adı sürümü](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Göbek adı sürümü")</span><span class="sxs-lookup"><span data-stu-id="3bea7-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="3bea7-248">Özet</span><span class="sxs-lookup"><span data-stu-id="3bea7-248">Summary</span></span>

<span data-ttu-id="3bea7-249">Bu uygulamalı laboratuvarda herhangi bir model sınıfı kullanarak ASP.NET MVC 4 yapı Iskelesi ile CRUD işlemleri oluşturmaya yönelik basit adımları öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="3bea7-250">Daha sonra, Entity Framework geçişleri kullanarak, uygulamanızda veritabanından görünümlere kadar uçtan uca güncelleştirme gerçekleştirmeyi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="3bea7-251">Ek A: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="3bea7-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="3bea7-252">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="3bea7-253">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="3bea7-254">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) kısmına gidin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-254">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="3bea7-255">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="3bea7-256">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-256">Click on **Install Now**.</span></span> <span data-ttu-id="3bea7-257">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="3bea7-258">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="3bea7-259">![Visual Studio Express yüklensin](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="3bea7-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="3bea7-260">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="3bea7-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="3bea7-261">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="3bea7-263">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="3bea7-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="3bea7-264">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-264">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="3bea7-266">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="3bea7-266">*Installation progress*</span></span>
6. <span data-ttu-id="3bea7-267">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-267">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="3bea7-269">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="3bea7-269">*Installation completed*</span></span>
7. <span data-ttu-id="3bea7-270">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="3bea7-271">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="3bea7-273">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="3bea7-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="3bea7-274">Ek B: kod parçacıklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="3bea7-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="3bea7-275">Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea7-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="3bea7-276">Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="3bea7-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="3bea7-277">![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")</span><span class="sxs-lookup"><span data-stu-id="3bea7-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="3bea7-278">*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*</span><span class="sxs-lookup"><span data-stu-id="3bea7-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="3bea7-279">***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***</span><span class="sxs-lookup"><span data-stu-id="3bea7-279">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="3bea7-280">Kodu eklemek istediğiniz yere imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="3bea7-281">Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).</span><span class="sxs-lookup"><span data-stu-id="3bea7-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="3bea7-282">IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="3bea7-283">Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="3bea7-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="3bea7-284">Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="3bea7-285">![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="3bea7-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="3bea7-286">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="3bea7-286">*Start typing the snippet name*</span></span>

<span data-ttu-id="3bea7-287">![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="3bea7-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="3bea7-288">*Vurgulanan parçacığı seçmek için Tab tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="3bea7-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="3bea7-289">![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")</span><span class="sxs-lookup"><span data-stu-id="3bea7-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="3bea7-290">*Sekmeye tekrar basın ve kod parçacığı genişletilir*</span><span class="sxs-lookup"><span data-stu-id="3bea7-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="3bea7-291">***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="3bea7-291">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="3bea7-292">Kod parçacığını eklemek istediğiniz yere sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bea7-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="3bea7-293">Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-293">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="3bea7-294">Listeden tıklatarak ilgili kod parçacığını seçin.</span><span class="sxs-lookup"><span data-stu-id="3bea7-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="3bea7-295">![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")</span><span class="sxs-lookup"><span data-stu-id="3bea7-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="3bea7-296">*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*</span><span class="sxs-lookup"><span data-stu-id="3bea7-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="3bea7-297">![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Listeden tıklatarak ilgili kod parçacığını seçin")</span><span class="sxs-lookup"><span data-stu-id="3bea7-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="3bea7-298">*Listeden tıklatarak ilgili kod parçacığını seçin*</span><span class="sxs-lookup"><span data-stu-id="3bea7-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>
