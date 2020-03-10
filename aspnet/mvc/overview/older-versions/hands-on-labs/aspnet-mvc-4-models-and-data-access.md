---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 modeller ve veri erişimi | Microsoft Docs
author: rick-anderson
description: "Note: Bu uygulamalı laboratuvar, ASP.NET MVC 'nin temel bilgisine sahip olduğunuzu varsayar. Daha önce ASP.NET MVC kullandıysanız, ASP.NET MVC 4 ' ün üzerinde gitmeniz önerilir..."
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560202"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="7c314-104">ASP.NET MVC 4 Modelleri ve Veri Erişimi</span><span class="sxs-lookup"><span data-stu-id="7c314-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="7c314-105">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="7c314-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="7c314-106">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="7c314-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="7c314-107">Bu uygulamalı laboratuvar, **ASP.NET MVC**'nin temel bilgisine sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="7c314-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="7c314-108">Daha önce **ASP.NET MVC** kullandıysanız, **ASP.NET MVC 4 temel** uygulamalı laboratuvarına gitmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="7c314-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="7c314-109">Bu laboratuvar, daha önce kaynak klasörde sunulan örnek bir Web uygulamasına küçük değişiklikler uygulayarak açıklanan geliştirmeler ve yeni özellikler konusunda size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="7c314-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="7c314-110">Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit sürümlerinde](https://aka.ms/webcamps-training-kit)kullanılabilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="7c314-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="7c314-111">Bu laboratuvara özgü proje, [ASP.NET MVC 4 modelleriyle ve veri erişiminde](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7c314-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="7c314-112">**ASP.NET MVC temelleri** uygulamalı laboratuvarda, denetleyicilerden görünüm şablonlarına sabit kodlanmış veriler geçirdik.</span><span class="sxs-lookup"><span data-stu-id="7c314-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="7c314-113">Ancak gerçek bir Web uygulaması oluşturmak için gerçek bir veritabanı kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="7c314-114">Bu uygulamalı laboratuvar, müzik mağazası uygulaması için gereken verileri depolamak ve almak üzere bir veritabanı altyapısını nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c314-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="7c314-115">Bunu gerçekleştirmek için, var olan bir veritabanıyla başlayıp Varlık Veri Modeli oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="7c314-116">Bu laboratuvarda, **Database First** yaklaşımı ve **Code First** yaklaşımını karşılacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="7c314-117">Ancak, **model First** yaklaşımını de kullanabilir, araçları kullanarak aynı modeli oluşturabilir ve sonra veritabanını buradan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="7c314-118">![Database First ve Model First karşılaştırması](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First ve Model First karşılaştırması")</span><span class="sxs-lookup"><span data-stu-id="7c314-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="7c314-119">*Database First ve Model First karşılaştırması*</span><span class="sxs-lookup"><span data-stu-id="7c314-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="7c314-120">Modeli oluşturduktan sonra, depolama görünümlerinde, sabit kodlanmış veriler yerine veritabanından alınan verileri sağlamak için StoreController 'da uygun ayarlamaları yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="7c314-121">StoreController görünüm şablonlarına aynı ViewModel döndürmesini sağladığından, veriler veritabanından geldiği halde görünüm şablonlarına herhangi bir değişiklik yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7c314-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="7c314-122">**Code First yaklaşımı**</span><span class="sxs-lookup"><span data-stu-id="7c314-122">**The Code First Approach**</span></span>

<span data-ttu-id="7c314-123">Code First yaklaşım, genellikle Framework ile bağlanmış sınıfları oluşturmadan kodu koddan tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="7c314-124">Önce kod içinde, model nesneleri POCOs ile tanımlanır, &quot;düz eski CLR nesneleri&quot;.</span><span class="sxs-lookup"><span data-stu-id="7c314-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="7c314-125">POCOs, devralma gerektirmeyen ve arabirimleri uygulamayan basit düz sınıflardır.</span><span class="sxs-lookup"><span data-stu-id="7c314-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="7c314-126">Veritabanından otomatik olarak veritabanı oluşturabilir veya var olan bir veritabanını kullanabilir ve koddan sınıf eşlemesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="7c314-127">Bu yaklaşımı kullanmanın avantajları,, POCOs sınıfları eşleme çerçevesiyle ilişkili olmadığından, modelin Kalıcılık çerçevesinden (Bu durumda Entity Framework) bağımsız kaldığı bir avantajdır.</span><span class="sxs-lookup"><span data-stu-id="7c314-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="7c314-128">Bu laboratuvar, ASP.NET MVC 4 ' ü ve bu uygulamalı laboratuvarda gösterilen özelliklere uyacak şekilde özelleştirilmiş ve küçültülmüş bir müzik deposu örnek uygulaması sürümünü temel alır.</span><span class="sxs-lookup"><span data-stu-id="7c314-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="7c314-129">Tüm **müzik deposu** öğreticisi uygulamasını araştırmak isterseniz, bunu [MVC-müzik-mağaza](https://github.com/evilDave/MVC-Music-Store)' da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="7c314-130">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7c314-130">Prerequisites</span></span>

<span data-ttu-id="7c314-131">Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c314-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="7c314-132">[Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).</span><span class="sxs-lookup"><span data-stu-id="7c314-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="7c314-133">Kurulum</span><span class="sxs-lookup"><span data-stu-id="7c314-133">Setup</span></span>

<span data-ttu-id="7c314-134">**Kod parçacıklarını yükleme**</span><span class="sxs-lookup"><span data-stu-id="7c314-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="7c314-135">Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7c314-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="7c314-136">Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c314-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="7c314-137">Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek C: kod parçacıkları&quot;kullanarak](#AppendixC) bu belgedeki eke başvurabilirsiniz &quot;.</span><span class="sxs-lookup"><span data-stu-id="7c314-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="7c314-138">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="7c314-138">Exercises</span></span>

<span data-ttu-id="7c314-139">Bu uygulamalı laboratuvar aşağıdaki alýþtýrmalardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="7c314-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="7c314-140">Alıştırma 1: veritabanı ekleme</span><span class="sxs-lookup"><span data-stu-id="7c314-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="7c314-141">Alıştırma 2: Code First kullanarak veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c314-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="7c314-142">Alıştırma 3: veritabanını parametrelerle sorgulama</span><span class="sxs-lookup"><span data-stu-id="7c314-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="7c314-143">Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="7c314-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="7c314-144">Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="7c314-145">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **35 dakika**.</span><span class="sxs-lookup"><span data-stu-id="7c314-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="7c314-146">Alıştırma 1: veritabanı ekleme</span><span class="sxs-lookup"><span data-stu-id="7c314-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="7c314-147">Bu alıştırmada, verileri tüketmek için MusicStore uygulamasının tablolarıyla bir veritabanını nasıl ekleyeceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="7c314-148">Veritabanı modeliyle oluşturulduktan ve çözüme eklendikten sonra, sabit kodlanmış değerler kullanmak yerine, veritabanından alınan verileri görüntüleme şablonuna sağlamak için StoreController sınıfını değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="7c314-149">Görev 1-veritabanı ekleme</span><span class="sxs-lookup"><span data-stu-id="7c314-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="7c314-150">Bu görevde, bir daha önceden oluşturulmuş bir veritabanını MusicStore uygulamasının ana tablolarıyla çözüme ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="7c314-151">**Kaynak/Ex1-AddingADatabaseDBFirst/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="7c314-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="7c314-152">Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c314-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="7c314-153">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7c314-154">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="7c314-155">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7c314-156">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="7c314-157">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="7c314-158">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="7c314-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="7c314-159">**Mvcmusicstore** veritabanı dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="7c314-160">Bu uygulamalı laboratuvarda, **Mvcmusicstore. mdf**adlı önceden oluşturulmuş bir veritabanını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="7c314-161">Bunu yapmak için, **uygulama\_veri** klasörüne sağ tıklayın, **Ekle** ' nin üzerine gelin ve **var olan öğe**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="7c314-162">**\Source\varlıklar** ' a göz atın ve **Mvcmusicstore. mdf** dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="7c314-163">![Varolan bir öğe ekleniyor](aspnet-mvc-4-models-and-data-access/_static/image2.png "Varolan bir öğe ekleniyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="7c314-164">*Varolan bir öğe ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="7c314-165">![MvcMusicStore. mdf veritabanı dosyası](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore. mdf veritabanı dosyası")</span><span class="sxs-lookup"><span data-stu-id="7c314-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="7c314-166">*MvcMusicStore. mdf veritabanı dosyası*</span><span class="sxs-lookup"><span data-stu-id="7c314-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="7c314-167">Veritabanı projeye eklendi.</span><span class="sxs-lookup"><span data-stu-id="7c314-167">The database has been added to the project.</span></span> <span data-ttu-id="7c314-168">Veritabanı çözüm içinde bulunduğunda bile, farklı bir veritabanı sunucusunda barındırıldığından bu dosyayı sorgulayabilir ve güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="7c314-169">![MvcMusicStore veritabanı Çözüm Gezgini](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore veritabanı Çözüm Gezgini")</span><span class="sxs-lookup"><span data-stu-id="7c314-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="7c314-170">*MvcMusicStore veritabanı Çözüm Gezgini*</span><span class="sxs-lookup"><span data-stu-id="7c314-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="7c314-171">Veritabanıyla olan bağlantıyı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-171">Verify the connection to the database.</span></span> <span data-ttu-id="7c314-172">Bunu yapmak için, bir bağlantı kurmak üzere **Mvcmusicstore. mdf** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="7c314-173">![MvcMusicStore. mdf 'e bağlanılıyor](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore. mdf 'e bağlanılıyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="7c314-174">*MvcMusicStore. mdf 'e bağlanılıyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="7c314-175">Görev 2-veri modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c314-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="7c314-176">Bu görevde, önceki görevde eklenen veritabanıyla etkileşim kurmak için bir veri modeli oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="7c314-177">Veritabanını temsil edecek bir veri modeli oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c314-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="7c314-178">Bunu yapmak için, Çözüm Gezgini **modeller** klasörüne sağ tıklayın, **Ekle** ' nin üzerine gelin ve ardından **Yeni öğe**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="7c314-179">**Yeni öğe Ekle** Iletişim kutusunda **veri** şablonu ' nu ve ardından **ADO.net varlık veri modeli** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="7c314-180">Veri modeli adını **StoreDB. edmx** olarak değiştirin ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="7c314-181">![StoreDB ADO.NET Varlık Veri Modeli ekleme](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET Varlık Veri Modeli ekleme")</span><span class="sxs-lookup"><span data-stu-id="7c314-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="7c314-182">*StoreDB ADO.NET Varlık Veri Modeli ekleme*</span><span class="sxs-lookup"><span data-stu-id="7c314-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="7c314-183">**Varlık veri modeli Sihirbazı** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7c314-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="7c314-184">Bu sihirbaz, model katmanının oluşturulmasında size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="7c314-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="7c314-185">Modelin yakın zamanda eklenen mevcut veritabanına göre oluşturulması gerektiğinden, **veritabanından oluştur** ' u seçin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-185">Since the model should be created based on the existing database recently added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="7c314-186">![Model içeriğini seçme](aspnet-mvc-4-models-and-data-access/_static/image7.png "Model içeriğini seçme")</span><span class="sxs-lookup"><span data-stu-id="7c314-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="7c314-187">*Model içeriğini seçme*</span><span class="sxs-lookup"><span data-stu-id="7c314-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="7c314-188">Bir veritabanından model oluştururken, kullanılacak bağlantıyı belirtmeniz gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="7c314-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="7c314-189">**Yeni bağlantı**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="7c314-190">**Microsoft SQL Server veritabanı dosyası** ' nı seçin ve **devam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="7c314-191">![Veri kaynağını seçin](aspnet-mvc-4-models-and-data-access/_static/image8.png "Veri kaynağını seçin")</span><span class="sxs-lookup"><span data-stu-id="7c314-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="7c314-192">*Veri kaynağı seç iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="7c314-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="7c314-193">**Araştır** ' a tıklayın ve **App\_Data** klasöründe bulduğunuz **mvcmusicstore. mdf** veritabanını seçip **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="7c314-194">![Bağlantı özellikleri](aspnet-mvc-4-models-and-data-access/_static/image9.png "Bağlantı özellikleri")</span><span class="sxs-lookup"><span data-stu-id="7c314-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="7c314-195">*Bağlantı özellikleri*</span><span class="sxs-lookup"><span data-stu-id="7c314-195">*Connection properties*</span></span>
6. <span data-ttu-id="7c314-196">Oluşturulan sınıf, varlık bağlantı dizesiyle aynı ada sahip olmalıdır, bu nedenle adını **Musicstoreentities** olarak değiştirin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="7c314-197">![Veri bağlantısı seçiliyor](aspnet-mvc-4-models-and-data-access/_static/image10.png "Veri bağlantısı seçiliyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="7c314-198">*Veri bağlantısı seçiliyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="7c314-199">Kullanılacak veritabanı nesnelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-199">Choose the database objects to use.</span></span> <span data-ttu-id="7c314-200">Varlık modeli yalnızca veritabanının tablolarını kullanacak şekilde, **Tablolar** seçeneğini belirleyip **modeldeki yabancı anahtar sütunlarını dahil et ' in** ve ayrıca **üretilen nesne adları** seçeneklerinin de seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7c314-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="7c314-201">Model ad alanını **Mvcmusicstore. model** olarak değiştirip **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="7c314-202">![Veritabanı nesnelerini seçme](aspnet-mvc-4-models-and-data-access/_static/image11.png "Veritabanı nesnelerini seçme")</span><span class="sxs-lookup"><span data-stu-id="7c314-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="7c314-203">*Veritabanı nesnelerini seçme*</span><span class="sxs-lookup"><span data-stu-id="7c314-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c314-204">Bir güvenlik uyarısı iletişim kutusu gösteriliyorsa, şablonu çalıştırmak ve model varlıkları için sınıflar oluşturmak üzere **Tamam** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="7c314-205">Veritabanına yönelik bir varlık diyagramı görüntülenir, ancak her bir tabloyu veritabanına eşleyen ayrı bir sınıf oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7c314-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="7c314-206">Örneğin, **Albümler** tablosu, tablodaki her sütunun bir sınıf özelliği ile eşleşmeyeceği bir **Albüm** sınıfı tarafından temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="7c314-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="7c314-207">Bu, veritabanındaki satırları temsil eden nesneleri sorgulamanızı ve bunlarla çalışmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="7c314-208">![Varlık diyagramı](aspnet-mvc-4-models-and-data-access/_static/image12.png "Varlık diyagramı")</span><span class="sxs-lookup"><span data-stu-id="7c314-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="7c314-209">*Varlık diyagramı*</span><span class="sxs-lookup"><span data-stu-id="7c314-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c314-210">T4 şablonları (. tt), varlık sınıfları oluşturmak için kodu çalıştırır ve aynı ada sahip mevcut sınıfların üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="7c314-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="7c314-211">Bu örnekte, sınıfların &quot;albüm&quot;, &quot;tarz&quot; ve &quot;sanatçı&quot; oluşturulan kodla üzerine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="7c314-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="7c314-212">Görev 3-uygulamayı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c314-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="7c314-213">Bu görevde, model oluşturma, **Albüm**, **tarz** ve **sanatçı** model sınıflarını kaldırmakla birlikte, projenin yeni veri modeli sınıflarını kullanarak başarılı bir şekilde yapıdığına yönelik olarak kontrol edersiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="7c314-214">**Build** menü öğesini seçerek projeyi derleyin ve ardından **MvcMusicStore**' u oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c314-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="7c314-215">![Projeyi oluşturma](aspnet-mvc-4-models-and-data-access/_static/image13.png "Projeyi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="7c314-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="7c314-216">*Projeyi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7c314-216">*Building the project*</span></span>
2. <span data-ttu-id="7c314-217">Proje başarıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7c314-217">The project builds successfully.</span></span> <span data-ttu-id="7c314-218">Neden hala çalışıyor?</span><span class="sxs-lookup"><span data-stu-id="7c314-218">Why does it still work?</span></span> <span data-ttu-id="7c314-219">Veritabanı tablolarında, kaldırılan sınıflar **albümü** ve **tarzında**kullanmakta olduğunuz özellikleri içeren alanlar bulunduğundan, bu BT işe yarar.</span><span class="sxs-lookup"><span data-stu-id="7c314-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="7c314-220">![Derlemeler başarılı oldu](aspnet-mvc-4-models-and-data-access/_static/image14.png "Derlemeler başarılı oldu")</span><span class="sxs-lookup"><span data-stu-id="7c314-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="7c314-221">*Derlemeler başarılı oldu*</span><span class="sxs-lookup"><span data-stu-id="7c314-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="7c314-222">Tasarımcı varlıkları diyagram biçiminde görüntülüyor olsa da gerçekte C# sınıflardır.</span><span class="sxs-lookup"><span data-stu-id="7c314-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="7c314-223">Çözüm Gezgini **StoreDB. edmx** düğümünü genişletin ve ardından **StoreDB.tt**yeni oluşturulan varlıkları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7c314-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="7c314-224">![Oluşturulan dosyalar](aspnet-mvc-4-models-and-data-access/_static/image15.png "Oluşturulan dosyalar")</span><span class="sxs-lookup"><span data-stu-id="7c314-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="7c314-225">*Oluşturulan dosyalar*</span><span class="sxs-lookup"><span data-stu-id="7c314-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="7c314-226">Görev 4-veritabanını sorgulama</span><span class="sxs-lookup"><span data-stu-id="7c314-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="7c314-227">Bu görevde, sabit kodlanmış veriler kullanmak yerine, bilgileri almak için veritabanını sorgulayan için StoreController sınıfını güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c314-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="7c314-228">**Controllers\storecontroller.cs** dosyasını açın ve aşağıdaki alanı sınıfına, **StoreDB**adlı bir **musicstoreentities** sınıfının örneğini tutacak şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c314-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="7c314-229">(Kod parçacığı- *modeller ve veri erişimi-Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="7c314-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="7c314-230">**Musicstoreentities** sınıfı, veritabanındaki her tablo için bir koleksiyon özelliği sunar.</span><span class="sxs-lookup"><span data-stu-id="7c314-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="7c314-231">Tüm **albümlerle**bir tarzın alınması için **gözatmayı** eylem yöntemini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="7c314-232">(Kod parçacığı- *modeller ve veri erişimi-Ex1 Store tarama*)</span><span class="sxs-lookup"><span data-stu-id="7c314-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="7c314-233">Bu koleksiyonlara karşı kesin türü belirtilmiş sorgu ifadeleri yazmak için **LINQ** (dil ile tümleşik sorgu) adlı bir .NET özelliği kullanıyorsunuz. Bu, veritabanına karşı kod yürütecek ve programlayabileceğiniz nesneleri döndürmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="7c314-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="7c314-234">LINQ hakkında daha fazla bilgi için lütfen [MSDN sitesini](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="7c314-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="7c314-235">Tüm tarzları almak için **Dizin** eylemi yöntemini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="7c314-236">(Kod parçacığı- *modeller ve veri erişimi-Ex1 Store dizini*)</span><span class="sxs-lookup"><span data-stu-id="7c314-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="7c314-237">Tüm tarzları almak ve koleksiyonu bir listeye dönüştürmek için **Dizin** eylemi yöntemini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="7c314-238">(Kod parçacığı- *modeller ve veri erişimi-Ex1 Store GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="7c314-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="7c314-239">5\. Görev-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7c314-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="7c314-240">Bu görevde, depolama dizini sayfasında artık sabit kodlanmış olanlar yerine veritabanında depolanan tarzların görüntüleneceğini kontrol edersiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="7c314-241">**Storecontroller** daha önce olduğu gibi aynı varlıkları döndürdüğü için, bu kez verilerin veritabanından geldiği halde görünüm şablonunu değiştirme gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="7c314-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="7c314-242">Çözümü yeniden derleyin ve uygulamayı çalıştırmak için **F5** 'e basın.</span><span class="sxs-lookup"><span data-stu-id="7c314-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7c314-243">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-243">The project starts in the Home page.</span></span> <span data-ttu-id="7c314-244">**Tarzın** menüsünün artık sabit kodlanmış bir liste olmadığını ve verilerin doğrudan veritabanından alındığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="7c314-246">*Veritabanından Tarzya göz atma*</span><span class="sxs-lookup"><span data-stu-id="7c314-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="7c314-247">Şimdi herhangi bir tarzya gidin ve albümlerin veritabanından doldurulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="7c314-248">![Veritabanından Albümler 'e göz atma](aspnet-mvc-4-models-and-data-access/_static/image17.png "Veritabanından Albümler 'e göz atma")</span><span class="sxs-lookup"><span data-stu-id="7c314-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="7c314-249">*Veritabanından Albümler 'e göz atma*</span><span class="sxs-lookup"><span data-stu-id="7c314-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="7c314-250">Alıştırma 2: Code First kullanarak veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c314-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="7c314-251">Bu alıştırmada, MusicStore uygulamasının tablolarıyla bir veritabanı oluşturmak ve verilere erişmek için Code First yaklaşımını nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="7c314-252">Model oluşturulduktan sonra, tek kodlanmış değerler kullanmak yerine, veritabanından alınan verileri görünüm şablonuna sağlamak için StoreController 'ı değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="7c314-253">1\. Alıştırmayı tamamladıysanız ve Database First yaklaşımıyla zaten çalıştıysanız, artık farklı bir işlemle aynı sonuçların nasıl alınacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="7c314-254">Alıştırma 1 ile ortak olan görevler, okumanız daha kolay hale getirmek için işaretlendi.</span><span class="sxs-lookup"><span data-stu-id="7c314-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="7c314-255">Alıştırma 1 ' i tamamlamadıysanız, ancak Code First yaklaşımı öğrenmek istiyorsanız, bu alıştırmaya başlayabilir ve konunun tam kapsamına ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="7c314-256">Görev 1-örnek verileri doldurma</span><span class="sxs-lookup"><span data-stu-id="7c314-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="7c314-257">Bu görevde, Ilk önce kod kullanılarak oluşturulduğu zaman veritabanını örnek verilerle dolduracaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-257">In this task, you will populate the database with sample data when it is initially created using Code-First.</span></span>

1. <span data-ttu-id="7c314-258">**Kaynak/EX2-Creatingadatabasecodefırst/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="7c314-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="7c314-259">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="7c314-260">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c314-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="7c314-261">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7c314-262">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="7c314-263">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7c314-264">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="7c314-265">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="7c314-266">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="7c314-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="7c314-267">**Modeller** klasörüne **sampleData.cs** dosyasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="7c314-268">Bunu yapmak için **modeller** klasörüne sağ tıklayın, **Ekle** ' nin üzerine gelin ve **var olan öğe**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="7c314-269">**\Source\varlıklar** ' a göz atın ve **sampleData.cs** dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="7c314-270">![Örnek veri doldurma kodu](aspnet-mvc-4-models-and-data-access/_static/image18.png "Örnek veri doldurma kodu")</span><span class="sxs-lookup"><span data-stu-id="7c314-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="7c314-271">*Örnek veri doldurma kodu*</span><span class="sxs-lookup"><span data-stu-id="7c314-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="7c314-272">**Global.asax.cs** dosyasını açın ve aşağıdaki *using* deyimlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="7c314-273">(Kod parçacığı- *modeller ve veri erişimi-EX2 Global asax kullanımlar*)</span><span class="sxs-lookup"><span data-stu-id="7c314-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="7c314-274">**Uygulama\_Start ()** yönteminde, veritabanı başlatıcısı 'nı ayarlamak için aşağıdaki satırı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="7c314-275">(Kod parçacığı- *modeller ve veri erişimi-EX2 Global asax Setbaşlatıcısı*)</span><span class="sxs-lookup"><span data-stu-id="7c314-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="7c314-276">Görev 2-veritabanı bağlantısını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7c314-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="7c314-277">Projemizde zaten bir veritabanı eklediğine göre, **Web. config** dosyasına bağlantı dizesini yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c314-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="7c314-278">**Web. config dosyasına**bir bağlantı dizesi ekleyin. Bunu yapmak için, proje kökünde **Web. config** dosyasını açın ve DefaultConnection adlı bağlantı dizesini **&lt;connectionStrings&gt;** bölümünde yer alan bu satırla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7c314-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="7c314-279">![Web. config dosyası konumu](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web. config dosyası konumu")</span><span class="sxs-lookup"><span data-stu-id="7c314-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="7c314-280">*Web. config dosyası konumu*</span><span class="sxs-lookup"><span data-stu-id="7c314-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="7c314-281">Görev 3-modelle çalışma</span><span class="sxs-lookup"><span data-stu-id="7c314-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="7c314-282">Veritabanı bağlantısını zaten yapılandırdığınıza göre, modeli veritabanı tabloları ile bağlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="7c314-283">Bu görevde, Code First veritabanıyla bağlantılı olacak bir sınıf oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="7c314-284">Değiştirilmesi gereken var olan bir POCO model sınıfı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="7c314-285">Alıştırma 1 ' i tamamladıysanız, bu adımın bir sihirbaz tarafından gerçekleştirildiğini aklınızda görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7c314-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="7c314-286">Code First yaparak, veri varlıklarına bağlanacak sınıfları el ile oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c314-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="7c314-287">**Model** proje klasöründen poco model sınıfı **tarzını** açın ve bir ID ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="7c314-288">**Genreıd**adlı bir int özelliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c314-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="7c314-289">(Kod parçacığı- *modeller ve veri erişimi-Ex2 Code First tarz*)</span><span class="sxs-lookup"><span data-stu-id="7c314-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="7c314-290">Code First kuralları ile çalışmak için, sınıf tarzında otomatik olarak algılanacak bir birincil anahtar özelliği olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7c314-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="7c314-291">Bu [MSDN makalesinde](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)Code First kuralları hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="7c314-292">Şimdi, **model** proje klasöründen poco model sınıfı **albümünü** açın ve yabancı anahtarları ekleyin, **genreıd** ve **ArtistId**adlarıyla Özellikler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c314-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="7c314-293">Bu sınıf zaten birincil anahtar için **Genreıd** 'ye sahip.</span><span class="sxs-lookup"><span data-stu-id="7c314-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="7c314-294">(Kod parçacığı- *modeller ve veri erişimi-Ex2 Code First albüm*)</span><span class="sxs-lookup"><span data-stu-id="7c314-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="7c314-295">POCO modeli sınıf **sanatçısını** açın ve **ArtistId** özelliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="7c314-296">(Kod parçacığı- *modeller ve veri erişimi-Ex2 Code First sanatçı*)</span><span class="sxs-lookup"><span data-stu-id="7c314-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="7c314-297">**Modeller** proje klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Sınıf**.</span><span class="sxs-lookup"><span data-stu-id="7c314-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="7c314-298">Dosyayı **MusicStoreEntities.cs**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="7c314-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="7c314-299">Ardından Ekle ' ye tıklayın **.**</span><span class="sxs-lookup"><span data-stu-id="7c314-299">Then, click **Add.**</span></span>

    <span data-ttu-id="7c314-300">![Sınıf ekleme](aspnet-mvc-4-models-and-data-access/_static/image20.png "Sınıf ekleme")</span><span class="sxs-lookup"><span data-stu-id="7c314-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="7c314-301">*Yeni öğe ekleme*</span><span class="sxs-lookup"><span data-stu-id="7c314-301">*Adding a new item*</span></span>

    <span data-ttu-id="7c314-302">![Class2 ekleme](aspnet-mvc-4-models-and-data-access/_static/image21.png "Class2 ekleme")</span><span class="sxs-lookup"><span data-stu-id="7c314-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="7c314-303">*Sınıf ekleme*</span><span class="sxs-lookup"><span data-stu-id="7c314-303">*Adding a class*</span></span>
5. <span data-ttu-id="7c314-304">Az önce oluşturduğunuz, **MusicStoreEntities.cs**ve **System. Data. Entity** ve **System. Data. Entity. Infrastructure**ad alanlarını içeren sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="7c314-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="7c314-305">Sınıf bildirimini **DbContext** sınıfını genişletmek için değiştirin: bir public **dbset** bildirin ve **onmodeloluþturma** metodunu geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="7c314-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="7c314-306">Bu adımdan sonra modelinize Entity Framework ile bağlantı oluşturacak bir etki alanı sınıfı alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="7c314-307">Bunu yapmak için, sınıf kodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7c314-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="7c314-308">(Kod parçacığı- *modeller ve veri erişimi-Ex2 Code First MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="7c314-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="7c314-309">Entity Framework **DbContext** ve **DBSET** Ile poco sınıf tarzında sorgulama yapabileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="7c314-310">**Onmodeloluþturma** yöntemini genişleterek, tarzın bir veritabanı tablosuna nasıl eşleneceğini **kodda** belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="7c314-311">Bu MSDN makalesinde DBContext ve DBSet hakkında daha fazla bilgi edinebilirsiniz: [bağlantı](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="7c314-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="7c314-312">Görev 4-veritabanını sorgulama</span><span class="sxs-lookup"><span data-stu-id="7c314-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="7c314-313">Bu görevde, sabit kodlanmış veriler kullanmak yerine, bunu veritabanından alacak şekilde StoreController sınıfını güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c314-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="7c314-314">Bu görev, alıştırma 1 ile yaygındır.</span><span class="sxs-lookup"><span data-stu-id="7c314-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="7c314-315">Alıştırma 1 ' i tamamladıysanız, bu adımların her iki yaklaşıma (önce veritabanı veya önce kod) aynı olduğunu aklınızda olursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c314-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="7c314-316">Bunlar, verilerin modelle bağlantılı olduğu şekilde farklılık gösteren, ancak veri varlıklarına erişim, denetleyiciden henüz saydamdır.</span><span class="sxs-lookup"><span data-stu-id="7c314-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>

1. <span data-ttu-id="7c314-317">**Controllers\storecontroller.cs** dosyasını açın ve aşağıdaki alanı sınıfına, **StoreDB**adlı bir **musicstoreentities** sınıfının örneğini tutacak şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c314-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="7c314-318">(Kod parçacığı- *modeller ve veri erişimi-Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="7c314-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="7c314-319">**Musicstoreentities** sınıfı, veritabanındaki her tablo için bir koleksiyon özelliği sunar.</span><span class="sxs-lookup"><span data-stu-id="7c314-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="7c314-320">Tüm **albümlerle**bir tarzın alınması için **gözatmayı** eylem yöntemini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="7c314-321">(Kod parçacığı- *modeller ve veri erişimi-EX2 Store tarama*)</span><span class="sxs-lookup"><span data-stu-id="7c314-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="7c314-322">Bu koleksiyonlara karşı kesin türü belirtilmiş sorgu ifadeleri yazmak için **LINQ** (dil ile tümleşik sorgu) adlı bir .NET özelliği kullanıyorsunuz. Bu, veritabanına karşı kod yürütecek ve programlayabileceğiniz nesneleri döndürmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="7c314-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="7c314-323">LINQ hakkında daha fazla bilgi için lütfen [MSDN sitesini](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="7c314-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="7c314-324">Tüm tarzları almak için **Dizin** eylemi yöntemini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="7c314-325">(Kod parçacığı- *modeller ve veri erişimi-EX2 Store dizini*)</span><span class="sxs-lookup"><span data-stu-id="7c314-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="7c314-326">Tüm tarzları almak ve koleksiyonu bir listeye dönüştürmek için **Dizin** eylemi yöntemini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="7c314-327">(Kod parçacığı- *modeller ve veri erişimi-EX2 Store GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="7c314-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="7c314-328">5\. Görev-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7c314-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="7c314-329">Bu görevde, depolama dizini sayfasında artık sabit kodlanmış olanlar yerine veritabanında depolanan tarzların görüntüleneceğini kontrol edersiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="7c314-330">**Storecontroller** daha önce olduğu gibi aynı **Storeındexviewmodel** döndürdüğü için görünüm şablonunu değiştirmeniz gerekmez, ancak bu kez veriler veritabanından gelir.</span><span class="sxs-lookup"><span data-stu-id="7c314-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="7c314-331">Çözümü yeniden derleyin ve uygulamayı çalıştırmak için **F5** 'e basın.</span><span class="sxs-lookup"><span data-stu-id="7c314-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7c314-332">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-332">The project starts in the Home page.</span></span> <span data-ttu-id="7c314-333">**Tarzın** menüsünün artık sabit kodlanmış bir liste olmadığını ve verilerin doğrudan veritabanından alındığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="7c314-335">*Veritabanından Tarzya göz atma*</span><span class="sxs-lookup"><span data-stu-id="7c314-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="7c314-336">Şimdi herhangi bir tarzya gidin ve albümlerin veritabanından doldurulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="7c314-337">![Veritabanından Albümler 'e göz atma](aspnet-mvc-4-models-and-data-access/_static/image23.png "Veritabanından Albümler 'e göz atma")</span><span class="sxs-lookup"><span data-stu-id="7c314-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="7c314-338">*Veritabanından Albümler 'e göz atma*</span><span class="sxs-lookup"><span data-stu-id="7c314-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="7c314-339">Alıştırma 3: veritabanını parametrelerle sorgulama</span><span class="sxs-lookup"><span data-stu-id="7c314-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="7c314-340">Bu alıştırmada, parametreleri kullanarak veritabanını sorgulamayı ve sorgu sonucu şekillendirmenin nasıl kullanıldığını, verileri daha verimli bir şekilde alan bir özellik olan veritabanı erişimlerini azaltan bir özelliği öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="7c314-341">Sorgu sonucu şekillendirme hakkında daha fazla bilgi için aşağıdaki [MSDN makalesini](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="7c314-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="7c314-342">Görev 1-veritabanından albümleri almak için StoreController değiştiriliyor</span><span class="sxs-lookup"><span data-stu-id="7c314-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="7c314-343">Bu görevde, belirli bir tarz albümleri almak için **Storecontroller** sınıfını veritabanına erişecek şekilde değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="7c314-344">Database-First yaklaşımını kullanmak istiyorsanız, Code-First yaklaşımını veya **Source\ex3-queryingthedatabasewithparametersdbfirst\begin** klasörünü kullanmak istiyorsanız **Source\ex3-queryingthedatabasewithparameterscodefırst\begin** klasöründe bulunan **BEGIN** Solution ' i açın.</span><span class="sxs-lookup"><span data-stu-id="7c314-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="7c314-345">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="7c314-346">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c314-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="7c314-347">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7c314-348">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="7c314-349">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7c314-350">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="7c314-351">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="7c314-352">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="7c314-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="7c314-353">**Tarayıcı** eylemi yöntemini değiştirmek Için **storecontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="7c314-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="7c314-354">Bunu yapmak için, **Çözüm Gezgini**, **denetleyiciler** klasörünü genişletin ve **StoreController.cs**öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="7c314-355">Belirli bir tarz için Albümler almak üzere, **tarama** eylemi yöntemini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="7c314-356">Bunu yapmak için aşağıdaki kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7c314-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="7c314-357">(Kod parçacığı- *modeller ve veri erişimi-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="7c314-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="7c314-358">Varlığın bir koleksiyonunu doldurmak için, **dahil etme** yöntemini kullanarak albümleri de almak istediğinizi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c314-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="7c314-359">Kullanabilirsiniz. LINQ içinde **Single ()** uzantısı bu durumda, bir albüm için yalnızca bir tarz beklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="7c314-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="7c314-360">**Single ()** yöntemi bir lambda ifadesini parametre olarak alır. Bu durumda, adı tanımlı değerle eşleşen tek bir tarz nesneyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c314-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="7c314-361">Ayrıca, bir tarz nesne alındığında, yüklemek istediğiniz diğer ilgili varlıkların yanı sıra, yüklenmesini istediğinizi belirtmenize olanak tanıyan bir özellikten faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="7c314-362">Bu özelliğe **sorgu sonucu şekillendirme**adı verilir ve bilgileri almak için veritabanına erişmek için gereken sürelerin sayısını azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="7c314-363">Bu senaryoda, aldığınız tarz için albümleri önceden getirmek isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="7c314-364">Sorgu, ilgili Albümler de istediğinizi belirtmek için **tarzlar. Include (&quot;albümler&quot;)** içerir.</span><span class="sxs-lookup"><span data-stu-id="7c314-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="7c314-365">Tek bir veritabanı isteğinde hem tarz hem de albüm verilerini alacak olduğundan, bu daha verimli bir uygulamayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="7c314-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="7c314-366">Görev 2-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7c314-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="7c314-367">Bu görevde, uygulamayı çalıştıracaksınız ve veritabanından belirli bir tarz Albümler elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="7c314-368">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7c314-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7c314-369">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-369">The project starts in the Home page.</span></span> <span data-ttu-id="7c314-370">Sonuçların veritabanından alındığını doğrulamak için, URL 'YI **/Store/zat? tarzı = pop** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="7c314-371">![Tarza göre gözatma](aspnet-mvc-4-models-and-data-access/_static/image24.png "Tarza göre gözatma")</span><span class="sxs-lookup"><span data-stu-id="7c314-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="7c314-372">*/Store/gözatmaya? tarz = pop 'a göz atma*</span><span class="sxs-lookup"><span data-stu-id="7c314-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="7c314-373">Görev 3-bir kimliğe göre Albümler 'e erişme</span><span class="sxs-lookup"><span data-stu-id="7c314-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="7c314-374">Bu görevde, bir önceki prosedürü kendi kimliğine göre albümleri alacak şekilde tekrarlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="7c314-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="7c314-375">Gerekirse, Visual Studio 'ya dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="7c314-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="7c314-376">**Ayrıntılar** eylem yöntemini değiştirmek Için **storecontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="7c314-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="7c314-377">Bunu yapmak için, **Çözüm Gezgini**, **denetleyiciler** klasörünü genişletin ve **StoreController.cs**öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="7c314-378">**Kimlik**bilgilerini temel alarak Albümler ayrıntılarını almak için **Ayrıntılar** eylem yöntemini değiştirin. Bunu yapmak için aşağıdaki kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7c314-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="7c314-379">(Kod parçacığı- *modeller ve veri erişimi-Ex3 StoreController ayrıntıları yöntemi*)</span><span class="sxs-lookup"><span data-stu-id="7c314-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="7c314-380">Görev 4-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7c314-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="7c314-381">Bu görevde, uygulamayı bir Web tarayıcısında çalıştıracaksınız ve kendi kimliğine göre albüm ayrıntılarını edinirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="7c314-382">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7c314-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7c314-383">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-383">The project starts in the Home page.</span></span> <span data-ttu-id="7c314-384">URL 'YI **/Store/details/51** olarak değiştirin veya sonuçların veritabanından alındığını doğrulamak için bir albüm seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="7c314-385">![Gözatma ayrıntıları](aspnet-mvc-4-models-and-data-access/_static/image25.png "Gözatma ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="7c314-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="7c314-386">*/Store/Details/51 öğesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="7c314-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="7c314-387">Ek olarak, bu uygulamayı Microsoft Azure Web siteleri ' ne ek [B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixB)için de dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="7c314-388">Özet</span><span class="sxs-lookup"><span data-stu-id="7c314-388">Summary</span></span>

<span data-ttu-id="7c314-389">Bu uygulamalı Laboratuvarı tamamlayarak, **Database First** yaklaşımını ve **Code First** YAKLAŞıMıNı kullanarak, ASP.NET MVC modellerinin ve veri erişiminin temellerini öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="7c314-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="7c314-390">Verileri kullanmak için çözüme bir veritabanı ekleme</span><span class="sxs-lookup"><span data-stu-id="7c314-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="7c314-391">Denetimleri, sabit kodlanmış bir yerine veritabanından alınan verilerle görüntüleme şablonları sağlamak üzere güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7c314-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="7c314-392">Parametreleri kullanarak veritabanını sorgulama</span><span class="sxs-lookup"><span data-stu-id="7c314-392">How to query the database using parameters</span></span>
- <span data-ttu-id="7c314-393">Veritabanı erişimleri sayısını azaltan, verileri daha verimli bir şekilde alan bir özellik olan sorgu sonucu şekillendirme 'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="7c314-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="7c314-394">Veritabanını modeliyle bağlamak için Microsoft Entity Framework 'de hem Database First hem de Code First yaklaşımları kullanma</span><span class="sxs-lookup"><span data-stu-id="7c314-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="7c314-395">Ek A: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="7c314-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="7c314-396">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="7c314-397">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c314-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="7c314-398">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin.</span><span class="sxs-lookup"><span data-stu-id="7c314-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="7c314-399">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="7c314-400">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-400">Click on **Install Now**.</span></span> <span data-ttu-id="7c314-401">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="7c314-402">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="7c314-403">![Visual Studio Express yüklensin](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="7c314-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="7c314-404">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="7c314-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="7c314-405">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="7c314-407">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="7c314-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="7c314-408">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-408">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="7c314-410">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="7c314-410">*Installation progress*</span></span>
6. <span data-ttu-id="7c314-411">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-411">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="7c314-413">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="7c314-413">*Installation completed*</span></span>
7. <span data-ttu-id="7c314-414">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="7c314-415">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="7c314-417">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="7c314-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="7c314-418">Ek B: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="7c314-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="7c314-419">Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c314-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="7c314-420">Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c314-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="7c314-421">[Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7c314-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c314-422">Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="7c314-423">[Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-423">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="7c314-424">![Windows Azure portal oturum açın](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure portal oturum açın")</span><span class="sxs-lookup"><span data-stu-id="7c314-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="7c314-425">*Windows Azure 'da oturum açma Yönetim Portalı*</span><span class="sxs-lookup"><span data-stu-id="7c314-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="7c314-426">Komut çubuğunda **Yeni** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="7c314-427">![Yeni bir Web sitesi oluşturma](aspnet-mvc-4-models-and-data-access/_static/image32.png "Yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="7c314-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="7c314-428">*Yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7c314-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="7c314-429">**İşlem** | **Web sitesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="7c314-430">Sonra **hızlı oluştur** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="7c314-431">Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c314-432">Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="7c314-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="7c314-433">Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c314-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="7c314-434">Bir veritabanı ayarlamaya yönelik adımları içermez.</span><span class="sxs-lookup"><span data-stu-id="7c314-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="7c314-435">![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](aspnet-mvc-4-models-and-data-access/_static/image33.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="7c314-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="7c314-436">*Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7c314-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="7c314-437">Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="7c314-438">Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="7c314-439">Yeni Web sitesinin çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="7c314-440">![Yeni Web sitesine göz atma](aspnet-mvc-4-models-and-data-access/_static/image34.png "Yeni Web sitesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="7c314-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="7c314-441">*Yeni Web sitesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="7c314-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="7c314-442">![Web sitesi çalışıyor](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web sitesi çalışıyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="7c314-443">*Web sitesi çalışıyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-443">*Web site running*</span></span>
6. <span data-ttu-id="7c314-444">Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="7c314-445">![Web sitesi yönetim sayfalarını açma](aspnet-mvc-4-models-and-data-access/_static/image36.png "Web sitesi yönetim sayfalarını açma")</span><span class="sxs-lookup"><span data-stu-id="7c314-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="7c314-446">*Web sitesi yönetim sayfalarını açma*</span><span class="sxs-lookup"><span data-stu-id="7c314-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="7c314-447">**Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c314-448">*Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="7c314-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="7c314-449">Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="7c314-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="7c314-450">**Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7c314-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="7c314-451">![Web sitesi yayımlama profili indiriliyor](aspnet-mvc-4-models-and-data-access/_static/image37.png "Web sitesi yayımlama profili indiriliyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="7c314-452">*Web sitesi yayımlama profili indiriliyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="7c314-453">Yayımlama profili dosyasını bilinen bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="7c314-454">Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="7c314-455">![Yayımlama profili dosyası kaydediliyor](aspnet-mvc-4-models-and-data-access/_static/image38.png "Yayımlama profili kaydediliyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="7c314-456">*Yayımlama profili dosyası kaydediliyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="7c314-457">Görev 2-veritabanı sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7c314-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="7c314-458">Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c314-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="7c314-459">SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="7c314-460">Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7c314-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="7c314-461">SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="7c314-462">Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="7c314-463">**Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın.</span><span class="sxs-lookup"><span data-stu-id="7c314-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="7c314-464">Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="7c314-465">![SQL veritabanı sunucu panosu](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL veritabanı sunucu panosu")</span><span class="sxs-lookup"><span data-stu-id="7c314-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="7c314-466">*SQL veritabanı sunucu panosu*</span><span class="sxs-lookup"><span data-stu-id="7c314-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="7c314-467">Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c314-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="7c314-468">Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](aspnet-mvc-4-models-and-data-access/_static/image40.png) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![Istemci IP adresi ekleniyor](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="7c314-470">*Istemci IP adresi ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="7c314-471">**ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Değişiklikleri Onayla](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="7c314-473">*Değişiklikleri Onayla*</span><span class="sxs-lookup"><span data-stu-id="7c314-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="7c314-474">Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="7c314-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="7c314-475">ASP.NET MVC 4 çözümüne geri dönün.</span><span class="sxs-lookup"><span data-stu-id="7c314-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="7c314-476">**Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="7c314-477">![Uygulama yayımlanıyor](aspnet-mvc-4-models-and-data-access/_static/image43.png "Uygulamayı Yayımlama")</span><span class="sxs-lookup"><span data-stu-id="7c314-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="7c314-478">*Web sitesi yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="7c314-479">İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="7c314-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="7c314-480">![Yayımlama profilini içeri aktarma](aspnet-mvc-4-models-and-data-access/_static/image44.png "Yayımlama profilini içeri aktarma")</span><span class="sxs-lookup"><span data-stu-id="7c314-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="7c314-481">*Yayımlama profili içeri aktarılıyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="7c314-482">**Bağlantıyı doğrula**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-482">Click **Validate Connection**.</span></span> <span data-ttu-id="7c314-483">Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c314-484">Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="7c314-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="7c314-485">![Bağlantı doğrulanıyor](aspnet-mvc-4-models-and-data-access/_static/image45.png "Bağlantı doğrulanıyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="7c314-486">*Bağlantı doğrulanıyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-486">*Validating connection*</span></span>
4. <span data-ttu-id="7c314-487">**Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="7c314-488">![Web dağıtımı yapılandırması](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web dağıtımı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="7c314-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="7c314-489">*Web dağıtımı yapılandırması*</span><span class="sxs-lookup"><span data-stu-id="7c314-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="7c314-490">Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7c314-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="7c314-491">**Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.</span><span class="sxs-lookup"><span data-stu-id="7c314-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="7c314-492">**Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="7c314-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="7c314-493">**Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="7c314-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="7c314-494">Yeni bir veritabanı adı yazın.</span><span class="sxs-lookup"><span data-stu-id="7c314-494">Type a new database name.</span></span>

     <span data-ttu-id="7c314-495">![Hedef bağlantı dizesi yapılandırılıyor](aspnet-mvc-4-models-and-data-access/_static/image47.png "Hedef bağlantı dizesi yapılandırılıyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="7c314-496">*Hedef bağlantı dizesi yapılandırılıyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="7c314-497">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-497">Then click **OK**.</span></span> <span data-ttu-id="7c314-498">Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="7c314-499">![Veritabanı oluşturma](aspnet-mvc-4-models-and-data-access/_static/image48.png "Veritabanı dizesi oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="7c314-500">*Veritabanı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7c314-500">*Creating the database*</span></span>
7. <span data-ttu-id="7c314-501">Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7c314-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="7c314-502">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-502">Then click **Next**.</span></span>

    <span data-ttu-id="7c314-503">![SQL veritabanı 'na işaret eden bağlantı dizesi](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL veritabanı 'na işaret eden bağlantı dizesi")</span><span class="sxs-lookup"><span data-stu-id="7c314-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="7c314-504">*SQL veritabanı 'na işaret eden bağlantı dizesi*</span><span class="sxs-lookup"><span data-stu-id="7c314-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="7c314-505">**Önizleme** sayfasında **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="7c314-506">![Web uygulaması yayımlanıyor](aspnet-mvc-4-models-and-data-access/_static/image50.png "Web uygulaması yayımlanıyor")</span><span class="sxs-lookup"><span data-stu-id="7c314-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="7c314-507">*Web uygulaması yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="7c314-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="7c314-508">Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.</span><span class="sxs-lookup"><span data-stu-id="7c314-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="7c314-509">Ek C: kod parçacıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="7c314-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="7c314-510">Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c314-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="7c314-511">Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="7c314-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="7c314-512">![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-models-and-data-access/_static/image51.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")</span><span class="sxs-lookup"><span data-stu-id="7c314-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="7c314-513">*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*</span><span class="sxs-lookup"><span data-stu-id="7c314-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="7c314-514">***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***</span><span class="sxs-lookup"><span data-stu-id="7c314-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="7c314-515">Kodu eklemek istediğiniz yere imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c314-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="7c314-516">Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).</span><span class="sxs-lookup"><span data-stu-id="7c314-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="7c314-517">IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="7c314-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="7c314-518">Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="7c314-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="7c314-519">Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="7c314-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="7c314-520">![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-models-and-data-access/_static/image52.png "Kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="7c314-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="7c314-521">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="7c314-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="7c314-522">![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-models-and-data-access/_static/image53.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="7c314-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="7c314-523">*Vurgulanan parçacığı seçmek için Tab tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="7c314-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="7c314-524">![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-models-and-data-access/_static/image54.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")</span><span class="sxs-lookup"><span data-stu-id="7c314-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="7c314-525">*Sekmeye tekrar basın ve kod parçacığı genişletilir*</span><span class="sxs-lookup"><span data-stu-id="7c314-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="7c314-526">***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="7c314-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="7c314-527">Kod parçacığını eklemek istediğiniz yere sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c314-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="7c314-528">Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="7c314-529">Listeden tıklatarak ilgili kod parçacığını seçin.</span><span class="sxs-lookup"><span data-stu-id="7c314-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="7c314-530">![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-models-and-data-access/_static/image55.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")</span><span class="sxs-lookup"><span data-stu-id="7c314-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="7c314-531">*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*</span><span class="sxs-lookup"><span data-stu-id="7c314-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="7c314-532">![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-models-and-data-access/_static/image56.png "Listeden tıklatarak ilgili kod parçacığını seçin")</span><span class="sxs-lookup"><span data-stu-id="7c314-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="7c314-533">*Listeden tıklatarak ilgili kod parçacığını seçin*</span><span class="sxs-lookup"><span data-stu-id="7c314-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
