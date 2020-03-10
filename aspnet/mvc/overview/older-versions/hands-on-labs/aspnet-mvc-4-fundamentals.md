---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 temelleri | Microsoft Docs
author: rick-anderson
description: Bu uygulamalı laboratuvar, ASP.NET MV 'ın nasıl kullanılacağı hakkında adım adım bir öğretici uygulama olan MVC (model görünüm denetleyicisi) müzik mağazasını temel alır.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598821"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="46564-103">ASP.NET MVC 4 Temelleri</span><span class="sxs-lookup"><span data-stu-id="46564-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="46564-104">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="46564-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="46564-105">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="46564-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="46564-106">Bu uygulamalı laboratuvar, ASP.NET MVC ve Visual Studio 'Nun nasıl kullanılacağını anlatan bir öğretici uygulaması olan MVC (model görünüm denetleyicisi) müzik mağazasını temel alır.</span><span class="sxs-lookup"><span data-stu-id="46564-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="46564-107">Laboratuvarın tamamında, bu teknolojilerin birlikte kullanılması basitlik, ancak gücünü öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="46564-108">Basit bir uygulamayla başlayacaksınız ve tamamen işlevsel bir ASP.NET MVC 4 Web uygulamasına sahip olana kadar bu uygulamayı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="46564-109">Bu laboratuvar ASP.NET MVC 4 ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="46564-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="46564-110">Öğretici uygulamasının ASP.NET MVC 3 sürümünü araştırmak isterseniz, bunu [MVC-müzik-Store](https://github.com/evilDave/MVC-Music-Store)' da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="46564-111">Bu uygulamalı laboratuvar, geliştiricinin HTML ve JavaScript gibi web geliştirme teknolojilerinde deneyimle karşılaşdığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="46564-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="46564-112">Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit sürümlerinde](https://aka.ms/webcamps-training-kit)kullanılabilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="46564-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="46564-113">Bu laboratuvara özgü proje, [ASP.NET MVC 4 temelleri](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)adresinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="46564-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="46564-114">Müzik Mağazası uygulaması</span><span class="sxs-lookup"><span data-stu-id="46564-114">The Music Store application</span></span>

<span data-ttu-id="46564-115">Bu laboratuvarda oluşturulacak müzik deposu Web uygulaması üç ana bölümden oluşur: alışveriş, kullanıma alma ve yönetim.</span><span class="sxs-lookup"><span data-stu-id="46564-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="46564-116">Ziyaretçiler, albümlere göre Albümler 'e göz atabilir, sepetlerine Albümler ekleyebilir, bunların seçimini gözden geçirebilir ve son olarak oturum açmaya ve siparişi tamamlamaya devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="46564-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="46564-117">Ayrıca, mağaza yöneticileri, kullanılabilir albümleri ve bunların ana özelliklerini yönetebilecektir.</span><span class="sxs-lookup"><span data-stu-id="46564-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="46564-118">![Müzik Mağazası ekranları](aspnet-mvc-4-fundamentals/_static/image1.png "Müzik Mağazası ekranları")</span><span class="sxs-lookup"><span data-stu-id="46564-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="46564-119">*Müzik Mağazası ekranları*</span><span class="sxs-lookup"><span data-stu-id="46564-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="46564-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="46564-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="46564-121">Müzik deposu uygulaması, bir uygulamayı üç ana bileşene ayıran mimari bir **model olan model görünüm denetleyicisi (MVC)** kullanılarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="46564-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="46564-122">**Modeller**: model nesneleri, uygulamanın etki alanı mantığını uygulayan parçalarından oluşur.</span><span class="sxs-lookup"><span data-stu-id="46564-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="46564-123">Genellikle model nesneleri ayrıca bir veritabanında model durumunu alır ve depolar.</span><span class="sxs-lookup"><span data-stu-id="46564-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="46564-124">**Görünümler:** Görünümler, uygulamanın kullanıcı arabirimini (UI) görüntüleyen bileşenlerdir.</span><span class="sxs-lookup"><span data-stu-id="46564-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="46564-125">Bu UI, genellikle model verilerinden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="46564-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="46564-126">Bir örnek, bir albüm nesnesinin geçerli durumuna bağlı olarak metin kutularını ve bir açılan listeyi görüntüleyen Albümler düzenleme görünümüdür.</span><span class="sxs-lookup"><span data-stu-id="46564-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="46564-127">**Denetleyiciler:** Denetleyiciler kullanıcı etkileşimini işleyen, modeli düzenleyen ve son olarak Kullanıcı arabirimini işlemek için bir görünüm seçtiğiniz bileşenlerdir.</span><span class="sxs-lookup"><span data-stu-id="46564-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="46564-128">Bir MVC uygulamasında, görünüm yalnızca bilgileri görüntüler; denetleyici ise kullanıcı girişini ve etkileşimini işler ve bunlara yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="46564-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="46564-129">MVC deseninin uygulamanın farklı yönlerini (Giriş mantığı, iş mantığı ve Kullanıcı arabirimi mantığı) ayıran uygulamalar oluşturmanıza yardımcı olur. bu öğeler arasında gevşek bir bağlantısı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="46564-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="46564-130">Bu ayrım, uygulamanın her seferinde bir kısmına odaklanmanıza olanak verdiğinden, bir uygulama oluşturduğunuzda karmaşıklığı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="46564-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="46564-131">Ayrıca, MVC deseninin uygulamaları test etmek için test odaklı geliştirme (TDD) kullanımını teşvik ve ayrıca uygulamaları test etmek kolaylaşır.</span><span class="sxs-lookup"><span data-stu-id="46564-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="46564-132">**ASP.NET MVC** framework, ASP.NET MVC tabanlı Web uygulamaları oluşturmak için ASP.NET Web Forms düzenine bir alternatif sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="46564-133">**ASP.NET MVC** Framework, çekirdek .NET Framework 'ün tüm gücünden yararlanmak için ana sayfalar ve üyelik tabanlı kimlik doğrulama gibi mevcut ASP.NET özellikleriyle tümleşik olan hafif ve yüksek düzeyde bir sunum çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="46564-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="46564-134">Zaten kullandığınız tüm kitaplıklar ASP.NET MVC 4 ' te de kullanılabildiğinden, ASP.NET Web Forms zaten biliyorsanız, bu faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="46564-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="46564-135">Ayrıca, bir MVC uygulamasının üç ana bileşeni arasında gevşek bir dağıtım paralel geliştirmeyi de yükseltir.</span><span class="sxs-lookup"><span data-stu-id="46564-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="46564-136">Örneğin, bir geliştirici görünümde çalışırken, ikinci bir geliştirici denetleyici mantığı üzerinde çalışabilir ve üçüncü bir geliştirici modeldeki iş mantığına odaklanabilir.</span><span class="sxs-lookup"><span data-stu-id="46564-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="46564-137">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="46564-137">Objectives</span></span>

<span data-ttu-id="46564-138">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="46564-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="46564-139">Müzik Mağazası uygulaması öğreticisini temel alarak sıfırdan bir ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="46564-140">URL 'Leri işlemek için sitenin ana sayfasına ve ana işlevselliğine göz atmak üzere denetleyiciler ekleyin</span><span class="sxs-lookup"><span data-stu-id="46564-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="46564-141">Stili ile birlikte görüntülenecek içeriği özelleştirmek için bir görünüm ekleyin</span><span class="sxs-lookup"><span data-stu-id="46564-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="46564-142">Veri ve etki alanı mantığını içerecek ve yönetecek model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="46564-143">Denetleyici eylemlerden görünüm şablonlarına bilgi geçirmek için model görüntüleme modelini kullanın</span><span class="sxs-lookup"><span data-stu-id="46564-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="46564-144">Internet uygulamaları için ASP.NET MVC 4 yeni şablonunu keşfet</span><span class="sxs-lookup"><span data-stu-id="46564-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="46564-145">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="46564-145">Prerequisites</span></span>

<span data-ttu-id="46564-146">Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="46564-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="46564-147">[Web Için Visual Studio 2012 Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku)</span><span class="sxs-lookup"><span data-stu-id="46564-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="46564-148">Kurulum</span><span class="sxs-lookup"><span data-stu-id="46564-148">Setup</span></span>

<span data-ttu-id="46564-149">**Kod parçacıklarını yükleme**</span><span class="sxs-lookup"><span data-stu-id="46564-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="46564-150">Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="46564-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="46564-151">Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="46564-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="46564-152">Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek C: kod parçacıkları&quot;kullanarak](#AppendixC) bu belgedeki eke başvurabilirsiniz &quot;.</span><span class="sxs-lookup"><span data-stu-id="46564-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="46564-153">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="46564-153">Exercises</span></span>

<span data-ttu-id="46564-154">Bu uygulamalı laboratuvar aşağıdaki alýþtýrmalardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="46564-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="46564-155">Alıştırma 1: MusicStore ASP.NET MVC web uygulaması projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="46564-156">Alıştırma 2: denetleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="46564-157">Alıştırma 3: bir denetleyiciye parametre geçirme</span><span class="sxs-lookup"><span data-stu-id="46564-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="46564-158">Alıştırma 4: görünüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="46564-159">Alıştırma 5: bir görünüm modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="46564-160">Alıştırma 6: görünümdeki parametreleri kullanma</span><span class="sxs-lookup"><span data-stu-id="46564-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="46564-161">Alıştırma 7: ASP.NET MVC 4 yeni şablonu etrafında bir lap</span><span class="sxs-lookup"><span data-stu-id="46564-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="46564-162">Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="46564-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="46564-163">Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="46564-164">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.</span><span class="sxs-lookup"><span data-stu-id="46564-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="46564-165">Alıştırma 1: MusicStore ASP.NET MVC web uygulaması projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="46564-166">Bu alıştırmada, Web için Visual Studio 2012 Express ve ana klasör kuruluşunun yanı sıra bir ASP.NET MVC uygulaması oluşturmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="46564-167">Ayrıca, yeni bir denetleyici eklemeyi ve uygulamanın giriş sayfasında basit bir dize görüntülemeyi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="46564-168">Görev 1-ASP.NET MVC web uygulaması projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="46564-169">Bu görevde, MVC Visual Studio şablonunu kullanarak boş bir ASP.NET MVC uygulama projesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="46564-170">**Web için vs Express**başlatın.</span><span class="sxs-lookup"><span data-stu-id="46564-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="46564-171">**Dosya** menüsünde **Yeni proje**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="46564-172">**Yeni proje** iletişim kutusunda, **Visual C#,** **Web** Template List altında bulunan **ASP.NET MVC 4 Web uygulaması** proje türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="46564-173">**Adı** *Mvcmusicstore*olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="46564-174">Çözümün konumunu, bu alıştırmanın kaynak klasöründeki yeni bir **Başlangıç** klasörü içinde ayarlayın, örneğin **[-hol-Path] \Source\ex01-creatingmusicstoreproject\begın**.</span><span class="sxs-lookup"><span data-stu-id="46564-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="46564-175">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-175">Click **OK**.</span></span>

    <span data-ttu-id="46564-176">![Yeni proje oluştur Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image2.png "Yeni proje oluştur Iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="46564-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="46564-177">*Yeni proje oluştur Iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="46564-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="46564-178">**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **temel** şablonu seçin ve **Görünüm altyapısının** **seçili olduğundan emin olun.**</span><span class="sxs-lookup"><span data-stu-id="46564-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="46564-179">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-179">Click **OK**.</span></span>

    <span data-ttu-id="46564-180">![Yeni ASP.NET MVC 4 projesi Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image3.png "Yeni ASP.NET MVC 4 projesi Iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="46564-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="46564-181">*Yeni ASP.NET MVC 4 projesi Iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="46564-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="46564-182">Görev 2-çözüm yapısını keşfetme</span><span class="sxs-lookup"><span data-stu-id="46564-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="46564-183">ASP.NET MVC Framework, MVC modelini destekleyen Web uygulamaları oluşturmanıza yardımcı olan bir Visual Studio proje şablonu içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="46564-184">Bu şablon, gerekli klasörler, öğe şablonları ve yapılandırma dosyası girişleriyle yeni bir ASP.NET MVC web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46564-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="46564-185">Bu görevde, ilgili öğeleri ve bunların ilişkilerini anlamak için çözüm yapısını inceleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="46564-186">ASP.NET MVC çerçevesi varsayılan olarak yapılandırma&quot; yaklaşımına &quot;bir kural kullandığından ve klasör adlandırma kurallarına göre bazı varsayılan varsayımlar yaptığından, aşağıdaki klasörler tüm ASP.NET MVC uygulamasına dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="46564-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="46564-187">Proje oluşturulduktan sonra, sağ taraftaki Çözüm Gezgini oluşturulan klasör yapısını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="46564-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="46564-188">![Çözüm Gezgini MVC klasör yapısı ASP.NET](aspnet-mvc-4-fundamentals/_static/image4.png "Çözüm Gezgini MVC klasör yapısı ASP.NET")</span><span class="sxs-lookup"><span data-stu-id="46564-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="46564-189">*Çözüm Gezgini MVC klasör yapısı ASP.NET*</span><span class="sxs-lookup"><span data-stu-id="46564-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="46564-190">**Denetleyici**.</span><span class="sxs-lookup"><span data-stu-id="46564-190">**Controllers**.</span></span> <span data-ttu-id="46564-191">Bu klasör denetleyici sınıflarını içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="46564-192">MVC tabanlı bir uygulamada, denetleyiciler son kullanıcı etkileşimini işlemekten, modeli işlemeye ve sonunda Kullanıcı arabirimini işlemek için bir görünüm seçmeye sorumludur.</span><span class="sxs-lookup"><span data-stu-id="46564-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="46564-193">MVC çerçevesi, tüm denetleyicilerin adlarının &quot;denetleyicisi&quot;(örneğin, HomeController, LoginController veya ProductController) bitmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="46564-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="46564-194">**Modeller**.</span><span class="sxs-lookup"><span data-stu-id="46564-194">**Models**.</span></span> <span data-ttu-id="46564-195">Bu klasör, MVC web uygulaması için uygulama modelini temsil eden sınıflar için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="46564-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="46564-196">Bu genellikle nesneleri tanımlayan kodu ve veri deposuyla etkileşim kurma mantığını içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="46564-197">Genellikle, gerçek model nesneleri ayrı sınıf kitaplıklarında olacaktır.</span><span class="sxs-lookup"><span data-stu-id="46564-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="46564-198">Ancak, yeni bir uygulama oluşturduğunuzda, sınıfları dahil edebilir ve ardından bunları geliştirme döngüsünün sonraki bir noktasında ayrı sınıf kitaplıklarına taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="46564-199">**Görünümler**.</span><span class="sxs-lookup"><span data-stu-id="46564-199">**Views**.</span></span> <span data-ttu-id="46564-200">Bu klasör, uygulamanın kullanıcı arabirimini görüntülemekten sorumlu olan görünümler için önerilen konumdur.</span><span class="sxs-lookup"><span data-stu-id="46564-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="46564-201">Görünümler, işleme görünümleriyle ilgili diğer dosyalara ek olarak. aspx,. ascx,. cshtml ve. Master dosyalarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="46564-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="46564-202">Görünümler klasörü her denetleyici için bir klasör içerir; klasör, denetleyici adı ön eki ile adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="46564-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="46564-203">Örneğin, **HomeController**adlı bir denetleyiciniz varsa, görünümler klasörü Home adlı bir klasör içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="46564-204">Varsayılan olarak, ASP.NET MVC çerçevesi bir görünüm yüklediğinde, Views\controllerName klasöründe istenen görünüm adına sahip bir. aspx dosyası arar (**Görünümler [ControllerName] [action]. aspx**) veya Razor görünümleri Için (**Görünümler [ControllerName] [action]. cshtml**).</span><span class="sxs-lookup"><span data-stu-id="46564-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="46564-205">Daha önce listelenen klasörlere ek olarak, MVC web uygulaması genel URL yönlendirme varsayılanlarını ayarlamak için **Global. asax** dosyasını kullanır ve uygulamayı yapılandırmak için **Web. config** dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="46564-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="46564-206">Görev 3-HomeController ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="46564-207">MVC çerçevesini kullanmayan ASP.NET uygulamalarında, Kullanıcı etkileşimi sayfalar etrafında düzenlenir ve bu sayfalardaki olayları oluşturma ve işleme.</span><span class="sxs-lookup"><span data-stu-id="46564-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="46564-208">Buna karşılık, ASP.NET MVC uygulamalarıyla Kullanıcı etkileşimi denetleyiciler ve eylem yöntemleri etrafında düzenlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="46564-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="46564-209">Diğer taraftan, ASP.NET MVC çerçevesi, denetleyicileri olarak adlandırılan sınıflarla URL 'Leri eşler.</span><span class="sxs-lookup"><span data-stu-id="46564-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="46564-210">Denetleyiciler gelen istekleri işler, Kullanıcı giriş ve etkileşimlerini işler, uygun uygulama mantığını yürütür ve istemciye geri gönderme (HTML görüntüleme, bir dosyayı indirme, farklı bir URL 'ye yönlendirme vb.) yanıtını belirleme.</span><span class="sxs-lookup"><span data-stu-id="46564-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="46564-211">HTML görüntüleme durumunda, bir denetleyici sınıfı genellikle istek için HTML biçimlendirmesi oluşturmak üzere ayrı bir görünüm bileşeni çağırır.</span><span class="sxs-lookup"><span data-stu-id="46564-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="46564-212">Bir MVC uygulamasında, görünüm yalnızca bilgileri görüntüler; denetleyici ise kullanıcı girişini ve etkileşimini işler ve bunlara yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="46564-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="46564-213">Bu görevde, müzik deposu sitesinin giriş sayfasına URL 'Leri işleyecek bir denetleyici sınıfı ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="46564-214">Çözüm Gezgini içindeki **denetleyiciler** klasörüne sağ tıklayın, **Ekle** ve sonra **Denetleyici** komutu ' nı seçin:</span><span class="sxs-lookup"><span data-stu-id="46564-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="46564-215">![Denetleyici komutu ekleme](aspnet-mvc-4-fundamentals/_static/image5.png "Denetleyici komutu ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="46564-216">*Denetleyici komutu Ekle*</span><span class="sxs-lookup"><span data-stu-id="46564-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="46564-217">**Denetleyici Ekle** iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="46564-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="46564-218">Denetleyiciyi *HomeController* olarak adlandırın ve **Ekle**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="46564-219">![Denetleyici Ekle Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image6.png "Denetleyici Ekle Iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="46564-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="46564-220">*Denetleyici Ekle Iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="46564-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="46564-221">**HomeController.cs** dosyası **denetleyiciler** klasöründe oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="46564-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="46564-222">**HomeController** 'ın Dizin eyleminde bir dize döndürmesini sağlamak Için, **index** metodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="46564-223">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex1 HomeController dizini*)</span><span class="sxs-lookup"><span data-stu-id="46564-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="46564-224">Görev 4-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46564-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="46564-225">Bu görevde, uygulamayı bir Web tarayıcısında deneyirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="46564-226">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="46564-227">Proje derlenir ve yerel IIS Web sunucusu başlatılır.</span><span class="sxs-lookup"><span data-stu-id="46564-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="46564-228">Yerel IIS Web sunucusu, Web sunucusunun URL 'sini işaret eden bir Web tarayıcısını otomatik olarak açar.</span><span class="sxs-lookup"><span data-stu-id="46564-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="46564-229">![Web tarayıcısında çalışan uygulama](aspnet-mvc-4-fundamentals/_static/image7.png "Web tarayıcısında çalışan uygulama")</span><span class="sxs-lookup"><span data-stu-id="46564-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="46564-230">*Web tarayıcısında çalışan uygulama*</span><span class="sxs-lookup"><span data-stu-id="46564-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="46564-231">Yerel IIS Web sunucusu, bir rastgele boş bağlantı noktası numarasında Web sitesini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="46564-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="46564-232">Yukarıdaki şekilde, site `http://localhost:50103/`çalışıyor, bu nedenle 50103 numaralı bağlantı noktasını kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="46564-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="46564-233">Bağlantı noktası numaranız farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="46564-233">Your port number may vary.</span></span>
2. <span data-ttu-id="46564-234">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="46564-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="46564-235">Alıştırma 2: denetleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="46564-236">Bu alıştırmada, müzik Mağazası uygulamasının basit işlevlerini uygulamak için denetleyiciyi nasıl güncelleştireceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="46564-237">Bu denetleyici, aşağıdaki belirli isteklerin her birini işlemek için eylem yöntemleri tanımlayacaktır:</span><span class="sxs-lookup"><span data-stu-id="46564-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="46564-238">Müzik deposundaki müzik tarzlarındaki bir listeleme sayfası</span><span class="sxs-lookup"><span data-stu-id="46564-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="46564-239">Belirli bir tarz için tüm müzik albümlerini listeleyen bir tarayıcı sayfası</span><span class="sxs-lookup"><span data-stu-id="46564-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="46564-240">Belirli bir müzik albümünden ilgili bilgileri gösteren Ayrıntılar sayfası</span><span class="sxs-lookup"><span data-stu-id="46564-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="46564-241">Bu alıştırma kapsamında, bu eylemler şimdi yalnızca bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="46564-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="46564-242">Görev 1-yeni bir StoreController sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="46564-243">Bu görevde yeni bir denetleyici ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="46564-244">Zaten açık değilse **2012 Web için vs Express**başlatın.</span><span class="sxs-lookup"><span data-stu-id="46564-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="46564-245">**Dosya** menüsünde **Proje Aç**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="46564-246">Proje Aç iletişim kutusunda **Source\ex02-creatingacontroller\begin**öğesine göz atın, **Başlat. sln** ' yi seçin ve **Aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="46564-247">Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="46564-248">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="46564-249">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="46564-250">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="46564-251">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="46564-252">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="46564-253">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="46564-254">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="46564-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="46564-255">Yeni denetleyiciyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-255">Add the new controller.</span></span> <span data-ttu-id="46564-256">Bunu yapmak için Çözüm Gezgini içindeki **denetleyiciler** klasörüne sağ tıklayın, **Ekle** ve sonra **Denetleyici** komutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="46564-257">**Denetleyici adını** *storecontroller*olarak değiştirin ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="46564-258">![Denetleyici Ekle Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image8.png "Denetleyici Ekle Iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="46564-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="46564-259">*Denetleyici Ekle Iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="46564-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="46564-260">Görev 2-StoreController 'ın eylemlerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="46564-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="46564-261">Bu görevde, **Eylemler**olarak adlandırılan denetleyici yöntemlerini değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="46564-262">Eylemler, URL isteklerini işlemekten ve tarayıcıya geri gönderilmesi gereken içeriği veya URL 'YI çağıran kullanıcıya göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="46564-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="46564-263">**Storecontroller** sınıfının bir **Dizin** yöntemi zaten var.</span><span class="sxs-lookup"><span data-stu-id="46564-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="46564-264">Müzik mağazasının tüm tarzını listeleyen sayfayı uygulamak için bu laboratuvarın ilerleyen kısımlarında kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="46564-265">Şimdilik, **index** metodunu Store. Index ()&quot;bir dize &quot;döndüren aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="46564-266">(Kod parçacığı- *ASP.NET MVC 4 temelleri-EX2 StoreController dizini*)</span><span class="sxs-lookup"><span data-stu-id="46564-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="46564-267">**Gezinme** ve **ayrıntı** yöntemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="46564-268">Bunu yapmak için **Storecontroller**öğesine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="46564-269">(Kod parçacığı- *ASP.NET MVC 4 temelleri-EX2 StoreController BrowseAndDetails*)</span><span class="sxs-lookup"><span data-stu-id="46564-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="46564-270">Görev 3-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46564-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="46564-271">Bu görevde, uygulamayı bir Web tarayıcısında deneyirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="46564-272">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="46564-273">Proje **giriş** sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="46564-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="46564-274">Her eylemin uygulamasını doğrulamak için URL 'YI değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="46564-275">**/Store**.</span><span class="sxs-lookup"><span data-stu-id="46564-275">**/Store**.</span></span> <span data-ttu-id="46564-276">**Store. Index ()&quot;'dan&quot;Merhaba** görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="46564-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="46564-277">**/Store/zat**.</span><span class="sxs-lookup"><span data-stu-id="46564-277">**/Store/Browse**.</span></span> <span data-ttu-id="46564-278">**Store. Gözatacaksınız&quot;Merhaba. ()&quot;** görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="46564-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="46564-279">**/Store/details**.</span><span class="sxs-lookup"><span data-stu-id="46564-279">**/Store/Details**.</span></span> <span data-ttu-id="46564-280">**Store&quot;Hello. Details ()&quot;** görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="46564-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="46564-281">![Storegözatmaya göz atma](aspnet-mvc-4-fundamentals/_static/image9.png "Storegözatmaya göz atma")</span><span class="sxs-lookup"><span data-stu-id="46564-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="46564-282">*Tarama/Store/zat*</span><span class="sxs-lookup"><span data-stu-id="46564-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="46564-283">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="46564-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="46564-284">Alıştırma 3: bir denetleyiciye parametre geçirme</span><span class="sxs-lookup"><span data-stu-id="46564-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="46564-285">Bu aşamada, denetleyicilerden sabit dizeler döndürmüştür.</span><span class="sxs-lookup"><span data-stu-id="46564-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="46564-286">Bu alıştırmada, URL 'yi ve QueryString 'yi kullanarak bir denetleyiciye parametreleri nasıl geçitireceğinizi öğrenirsiniz ve sonra Yöntem eylemlerinin bir metinle tarayıcıya yanıt vermesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="46564-287">Görev 1-StoreController 'a tarz parametresi ekleniyor</span><span class="sxs-lookup"><span data-stu-id="46564-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="46564-288">Bu görevde, **Storecontroller**Içindeki **gözatam** eylemi yöntemine parametreleri göndermek için **QueryString** kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="46564-289">Zaten açık değilse, **Web için vs Express**başlatın.</span><span class="sxs-lookup"><span data-stu-id="46564-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="46564-290">**Dosya** menüsünde **Proje Aç**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="46564-291">Proje Aç iletişim kutusunda **Source\ex03-passingparameterstoacontroller\begin**öğesine göz atın, **BEGIN. sln** ' yi seçin ve **Aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="46564-292">Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="46564-293">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="46564-294">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="46564-295">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="46564-296">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="46564-297">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="46564-298">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="46564-299">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="46564-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="46564-300">**Storecontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="46564-300">Open **StoreController** class.</span></span> <span data-ttu-id="46564-301">Bunu yapmak için, **Çözüm Gezgini**, **denetleyiciler** klasörünü genişletin ve **StoreController.cs**öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="46564-302">Belirli bir tarz için istek için bir dize parametresi ekleyerek, **gözatıcı** yöntemini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="46564-303">ASP.NET MVC, çağrıldığında otomatik olarak herhangi bir QueryString veya form post parametrelerini bu eylem yöntemine iletir.</span><span class="sxs-lookup"><span data-stu-id="46564-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="46564-304">Bunu yapmak için, aşağıdaki kodla birlikte, **Gözatılacak** yöntemi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="46564-305">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="46564-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="46564-306">Kullanıcıların JavaScript 'i/Store/gözatmaya benzer bir bağlantıyla ekleme almasını engelleyecek şekilde **HttpUtility. HtmlEncode** yardımcı programı yöntemini kullanıyorsunuz **musunuz? Tarz =&lt;betiği&gt;Window. Location = '[http://hackersite.com](http://hackersite.com)'&lt;/scrıpt&gt;** .</span><span class="sxs-lookup"><span data-stu-id="46564-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="46564-307">Daha fazla açıklama için lütfen [Bu MSDN makalesini](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="46564-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="46564-308">Görev 2-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46564-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="46564-309">Bu görevde, uygulamayı bir Web tarayıcısında dener ve **tarz** parametresini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="46564-310">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="46564-311">Proje **giriş** sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="46564-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="46564-312">URL 'YI */Store/zat değiştirin mi? Tarzı = disco* , eylemin tarz parametresini aldığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="46564-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="46564-313">![Göz atma StoreBrowseGenre = disco](aspnet-mvc-4-fundamentals/_static/image10.png "Göz atma StoreBrowseGenre = disco")</span><span class="sxs-lookup"><span data-stu-id="46564-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="46564-314">*/Store/zat Gözatılıyor musunuz? Tarz = disco*</span><span class="sxs-lookup"><span data-stu-id="46564-314">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="46564-315">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="46564-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="46564-316">Görev 3-URL 'ye gömülü bir ID parametresi ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="46564-317">Bu görevde, **Storecontroller**'ın **Ayrıntılar** eylem yöntemine bir **ID** parametresi geçirmek için **URL 'yi** kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="46564-318">ASP.NET MVC 'nin varsayılan yönlendirme kuralı, eylem yöntemi adından sonra, **ID**adlı bir parametre olarak bir URL 'nin segmentini değerlendirmek için kullanılır. Eylem yönteminizin ID adlı parametresi varsa, ASP.NET MVC URL segmentini otomatik olarak parametre olarak size iletir.</span><span class="sxs-lookup"><span data-stu-id="46564-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="46564-319">URL **deposu/Ayrıntılar/5**' de, **kimlik** **5**olarak yorumlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="46564-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="46564-320">**Storecontroller**öğesinin **Details** metodunu, **ID**adlı bir **int** parametresi ekleyerek değiştirin. Bunu yapmak için, **Details** yöntemini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="46564-321">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex3 StoreController ayrıntıları yöntemi*)</span><span class="sxs-lookup"><span data-stu-id="46564-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="46564-322">Görev 4-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46564-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="46564-323">Bu görevde, uygulamayı bir Web tarayıcısında deney, **kimlik** parametresini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="46564-324">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="46564-325">Proje **giriş** sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="46564-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="46564-326">İşlemin ID parametresini aldığını doğrulamak için URL 'YI */Store/details/5* olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="46564-327">![StoreDetails5 gözatma](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 gözatma")</span><span class="sxs-lookup"><span data-stu-id="46564-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="46564-328">*Tarama/Store/Details/5*</span><span class="sxs-lookup"><span data-stu-id="46564-328">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="46564-329">Alıştırma 4: görünüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="46564-330">Şimdiye kadar, denetleyici eylemlerinden dizeler döndürmüştür.</span><span class="sxs-lookup"><span data-stu-id="46564-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="46564-331">Bu, denetleyicilerin nasıl çalıştığını anlamak için kullanışlı bir yoldur, ancak gerçek Web uygulamalarınızın nasıl derlendiğini değildir.</span><span class="sxs-lookup"><span data-stu-id="46564-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="46564-332">Görünümler, şablon dosyaları kullanımıyla tarayıcıya geri HTML oluşturmaya yönelik daha iyi bir yaklaşım sağlayan bileşenlerdir.</span><span class="sxs-lookup"><span data-stu-id="46564-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="46564-333">Bu alıştırmada, genel HTML içeriği için bir şablon kurmak üzere bir düzen ana sayfası eklemeyi öğrenirsiniz, sitenin görünümünü ve hisyi iyileştirmek için bir stil sayfası ve son olarak HomeController 'ın HTML döndürmesini sağlayan bir görünüm şablonu.</span><span class="sxs-lookup"><span data-stu-id="46564-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a><span data-ttu-id="46564-334">Görev 1-\_Layout. cshtml dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="46564-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="46564-335">**~/Views/Shared/\_Layout. cshtml** dosyası, Web sitesinin tamamında kullanılacak ortak HTML için bir şablon ayarlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="46564-336">Bu görevde, ana sayfa ve depolama alanı bağlantılarıyla ortak bir üst bilgiyle bir düzen ana sayfası ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="46564-337">Zaten açık değilse, **Web için vs Express**başlatın.</span><span class="sxs-lookup"><span data-stu-id="46564-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="46564-338">**Dosya** menüsünde **Proje Aç**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="46564-339">Proje Aç iletişim kutusunda **Source\ex04-creatingaview\begin**öğesine göz atın, **BEGIN. sln** ' yi seçin ve **Aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="46564-340">Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="46564-341">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="46564-342">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="46564-343">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="46564-344">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="46564-345">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="46564-346">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="46564-347">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="46564-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="46564-348"><strong>\_Layout. cshtml</strong> dosyası sitedeki tüm sayfalar için HTML kapsayıcı düzeni içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="46564-349">HTML yanıtı için <strong>&lt;html&gt;</strong> öğesini ve <strong>&lt;baş&gt;</strong> ve <strong>&lt;gövde&gt;</strong> öğelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="46564-350">HTML gövdesi içindeki <strong>@RenderBody()</strong> , şablonları görüntüleme, Dinamik içerikle doldurabilebilecekler bölgelerini belirler.</span><span class="sxs-lookup"><span data-stu-id="46564-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="46564-351">(C#)</span><span class="sxs-lookup"><span data-stu-id="46564-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="46564-352">Sitedeki tüm sayfalarda giriş sayfası ve depolama alanı bağlantılarıyla ortak bir üst bilgi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="46564-353">Bunu yapmak için, aşağıdaki kodu gövde&gt; deyimin altına ekleyin &lt;.</span><span class="sxs-lookup"><span data-stu-id="46564-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="46564-354">(C#)</span><span class="sxs-lookup"><span data-stu-id="46564-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="46564-355">Her sayfanın gövde bölümünü işlemek için bir div ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="46564-356"><strong>@RenderBody()</strong> şu vurgulanmış kodla değiştirin: (C#)</span><span class="sxs-lookup"><span data-stu-id="46564-356">Replace <strong>@RenderBody()</strong> with the following highlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="46564-357">Emin misiniz?</span><span class="sxs-lookup"><span data-stu-id="46564-357">Did you know?</span></span> <span data-ttu-id="46564-358">Visual Studio 2012, yaygın olarak kullanılan kodu HTML, kod dosyaları ve daha fazlasını eklemenizi kolaylaştıran kod parçacıkları içerir!</span><span class="sxs-lookup"><span data-stu-id="46564-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="46564-359">**&lt;div&gt;** yazarak deneyin ve tüm **div** etiketi eklemek için **Tab** tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="46564-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="46564-360">Görev 2-CSS stil sayfası ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="46564-361">Boş proje şablonu, yalnızca temel formları ve doğrulama iletilerini göstermek için kullanılan stilleri içeren çok kolay bir CSS dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="46564-362">Sitenin görünüm ve hisde gelişmesini sağlamak için ek CSS ve görüntüler (büyük olasılıkla tasarımcı tarafından sağlanıyor) kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="46564-363">Bu görevde, sitenin stillerini tanımlamak için bir CSS stil sayfası ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="46564-364">CSS dosyası ve görüntüleri, bu laboratuvarın **Source\assets\content** klasörüne dahildir.</span><span class="sxs-lookup"><span data-stu-id="46564-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="46564-365">Bunları uygulamaya eklemek için, bir **Windows Gezgini** penceresinden içeriğini aşağıda gösterildiği gibi Web için Visual Studio Express **Çözüm Gezgini** sürükleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="46564-366">![Stil içeriğini sürükleme](aspnet-mvc-4-fundamentals/_static/image12.png "Stil içeriğini sürükleme")</span><span class="sxs-lookup"><span data-stu-id="46564-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="46564-367">*Stil içeriğini sürükleme*</span><span class="sxs-lookup"><span data-stu-id="46564-367">*Dragging style contents*</span></span>
2. <span data-ttu-id="46564-368">**Site. css** dosyasını ve var olan bazı görüntüleri değiştirmeyi onaylamanız istenir bir uyarı iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="46564-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="46564-369">**Tüm öğelere Uygula** ' yı Işaretleyin ve **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="46564-370">Görev 3-görünüm şablonu ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="46564-371">Bu görevde, Bu alıştırmada eklenen düzen ana sayfasını ve CSS 'yi kullanacak HTML yanıtı oluşturmak için bir görünüm şablonu ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="46564-372">Sitenin giriş sayfasına göz atarken bir görünüm şablonu kullanmak için önce bir dize döndürmek yerine, **HomeController Dizin** yönteminin bir **Görünüm**döndürdüğünü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="46564-373">**HomeController** sınıfını açın ve bir **ActionResult**döndürecek şekilde **Dizin** metodunu değiştirin ve **() görünümünü**geri döndürün.</span><span class="sxs-lookup"><span data-stu-id="46564-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="46564-374">(Kod parçacığı- *ASP.NET MVC 4 temelleri-EX4 HomeController dizini*)</span><span class="sxs-lookup"><span data-stu-id="46564-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="46564-375">Şimdi uygun bir görünüm şablonu eklemeniz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="46564-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="46564-376">Bunu yapmak için, **Dizin** eylemi yönteminin içine sağ tıklayın ve **Görünüm Ekle** **' yi** seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="46564-377">Bu işlem, **Görünüm Ekle** iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="46564-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="46564-378">![Dizin yönteminin içinden bir görünüm ekleme](aspnet-mvc-4-fundamentals/_static/image13.png "Dizin yönteminin içinden bir görünüm ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="46564-379">*Dizin yönteminin içinden bir görünüm ekleme*</span><span class="sxs-lookup"><span data-stu-id="46564-379">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="46564-380">Görünüm **Ekle** iletişim kutusu bir görünüm şablonu dosyası oluşturacak şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="46564-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="46564-381">Varsayılan olarak, bu iletişim kutusu şablonu kullanacak eylem yöntemiyle eşleşecek şekilde görünüm şablonunun adını önceden doldurur.</span><span class="sxs-lookup"><span data-stu-id="46564-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="46564-382">HomeController içindeki **Dizin** eylemi yöntemi Içinde **Görünüm Ekle** bağlam menüsünü kullandığınız için, **Görünüm Ekle** Iletişim kutusunun varsayılan görünüm adı olarak dizini vardır.</span><span class="sxs-lookup"><span data-stu-id="46564-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="46564-383">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="46564-383">Click **Add**.</span></span>

    <span data-ttu-id="46564-384">![Görünüm Ekle Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image14.png "Görünüm Ekle Iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="46564-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="46564-385">*Görünüm Ekle Iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="46564-385">*Add View Dialog*</span></span>
4. <span data-ttu-id="46564-386">Visual Studio, **Views\home** klasörünün Içinde bir **Index. cshtml** görünüm şablonu oluşturur ve ardından açar.</span><span class="sxs-lookup"><span data-stu-id="46564-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="46564-387">![Ana Dizin görünümü oluşturuldu](aspnet-mvc-4-fundamentals/_static/image15.png "Ana Dizin görünümü oluşturuldu")</span><span class="sxs-lookup"><span data-stu-id="46564-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="46564-388">*Ana Dizin görünümü oluşturuldu*</span><span class="sxs-lookup"><span data-stu-id="46564-388">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="46564-389">**Index. cshtml** dosyasının adı ve konumu geçerlidir ve varsayılan ASP.NET MVC adlandırma kurallarına uyar.</span><span class="sxs-lookup"><span data-stu-id="46564-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="46564-390">\Views\**Home*\* klasörü, denetleyici adıyla (**giriş** denetleyicisi) eşleşir.</span><span class="sxs-lookup"><span data-stu-id="46564-390">The folder \Views\**Home*\* matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="46564-391">Görünüm şablonu adı (**Dizin**), görünümü görüntüleyen denetleyici eylemi yöntemiyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="46564-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="46564-392">Bu şekilde, ASP.NET MVC bir görünüm döndürmek için bu adlandırma kuralını kullanırken bir görünüm şablonunun adını veya konumunu açıkça belirtmek zorunda kalmaktan kaçınır.</span><span class="sxs-lookup"><span data-stu-id="46564-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="46564-393">Oluşturulan görünüm şablonu, daha önce tanımlanan **\_Layout. cshtml** şablonunu temel alır.</span><span class="sxs-lookup"><span data-stu-id="46564-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="46564-394">ViewBag. title özelliğini **Home**olarak güncelleştirin ve ana içeriği aşağıdaki kodda gösterildiği gibi **giriş sayfası**olacak şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="46564-395">Çözüm Gezgini **Mvcmusicstore** projesini seçin ve **F5** tuşuna basarak uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="46564-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="46564-396">Görev 4: doğrulama</span><span class="sxs-lookup"><span data-stu-id="46564-396">Task 4: Verification</span></span>

<span data-ttu-id="46564-397">Önceki alıştırmada bulunan tüm adımları doğru bir şekilde gerçekleştirdiğinizi doğrulamak için aşağıdaki gibi ilerleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="46564-398">Uygulama bir tarayıcıda açıldığında şunları unutmayın:</span><span class="sxs-lookup"><span data-stu-id="46564-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="46564-399">HomeController 'ın Dizin eylemi yöntemi, görünüm şablonu standart adlandırma kuralına uyduğundan, ' ın **Return View ()** olarak adlandırılan kod olsa da **\Views\home\ındex.cshtml** görünüm şablonunu buldu ve görüntülendi.</span><span class="sxs-lookup"><span data-stu-id="46564-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="46564-400">Giriş sayfasında **\Views\home\ındex.cshtml** görünüm şablonu içinde tanımlanan hoş geldiniz iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="46564-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="46564-401">Giriş sayfası **\_Layout. cshtml** şablonunu kullanıyor ve bu nedenle hoş geldiniz iletisi standart site HTML düzeni içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="46564-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="46564-402">![Tanımlı LayoutPage ve Style kullanarak giriş dizini görünümü](aspnet-mvc-4-fundamentals/_static/image16.png "Tanımlı LayoutPage ve Style kullanarak giriş dizini görünümü")</span><span class="sxs-lookup"><span data-stu-id="46564-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="46564-403">*Tanımlı LayoutPage ve Style kullanarak giriş dizini görünümü*</span><span class="sxs-lookup"><span data-stu-id="46564-403">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="46564-404">Alıştırma 5: bir görünüm modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="46564-405">Şimdiye kadar, görünümleriniz, sabit kodlanmış HTML 'yi görüntülemelidir, ancak dinamik Web uygulamaları oluşturmak için, görünüm şablonu denetleyiciden bilgi almalıdır.</span><span class="sxs-lookup"><span data-stu-id="46564-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="46564-406">Bu amaç için kullanılan yaygın bir teknik, denetleyicinin uygun HTML yanıtını oluşturmak için gereken tüm bilgileri paketetmesine olanak tanıyan **ViewModel** deseninin yer aldığı bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="46564-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="46564-407">Bu alıştırmada, ViewModel sınıfı oluşturmayı ve gerekli özellikleri eklemeyi öğreneceksiniz: depodaki tür tarzların sayısı ve bu tarzların listesi.</span><span class="sxs-lookup"><span data-stu-id="46564-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="46564-408">Ayrıca, StoreController 'ı oluşturulan ViewModel kullanacak şekilde güncelleyebilir ve son olarak, sayfada bahsedilen özellikleri görüntüleyecek yeni bir görünüm şablonu oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="46564-409">Görev 1-ViewModel sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="46564-410">Bu görevde, Depo tarzı listeleme senaryosunu uygulayacak bir ViewModel sınıfı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="46564-411">Zaten açık değilse, **Web için vs Express**başlatın.</span><span class="sxs-lookup"><span data-stu-id="46564-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="46564-412">**Dosya** menüsünde **Proje Aç**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="46564-413">Proje Aç iletişim kutusunda **Source\ex05-creatingaviewmodel\begın**konumuna gidin, **BEGIN. sln** ' yi seçin ve **Aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="46564-414">Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="46564-415">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="46564-416">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="46564-417">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="46564-418">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="46564-419">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="46564-420">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="46564-421">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="46564-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="46564-422">ViewModel tutmak için **Viewmodeller** klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46564-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="46564-423">Bunu yapmak için, en üst düzey **Mvcmusicstore** projesine sağ tıklayın, **Ekle** ve **Yeni klasör**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="46564-424">![Yeni klasör ekleme](aspnet-mvc-4-fundamentals/_static/image17.png "Yeni klasör ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="46564-425">*Yeni klasör ekleme*</span><span class="sxs-lookup"><span data-stu-id="46564-425">*Adding a new folder*</span></span>
4. <span data-ttu-id="46564-426">Klasör *Viewmodellerini*adlandırın.</span><span class="sxs-lookup"><span data-stu-id="46564-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="46564-427">![Çözüm Gezgini Viewmodeller klasörü](aspnet-mvc-4-fundamentals/_static/image18.png "Çözüm Gezgini Viewmodeller klasörü")</span><span class="sxs-lookup"><span data-stu-id="46564-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="46564-428">*Çözüm Gezgini Viewmodeller klasörü*</span><span class="sxs-lookup"><span data-stu-id="46564-428">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="46564-429">**ViewModel** sınıfı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46564-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="46564-430">Bunu yapmak için, kısa süre önce oluşturulan **Viewmodeller** klasörüne sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="46564-431">**Kod**altında, **sınıf** öğesini seçin ve dosyayı *StoreIndexViewModel.cs*olarak adlandırın, ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="46564-432">![Yeni sınıf ekleme](aspnet-mvc-4-fundamentals/_static/image19.png "Yeni sınıf ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="46564-433">*Yeni sınıf ekleme*</span><span class="sxs-lookup"><span data-stu-id="46564-433">*Adding a new Class*</span></span>

    <span data-ttu-id="46564-434">![Storeındexviewmodel sınıfı oluşturuluyor](aspnet-mvc-4-fundamentals/_static/image20.png "Storeındexviewmodel sınıfı oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="46564-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="46564-435">*Storeındexviewmodel sınıfı oluşturuluyor*</span><span class="sxs-lookup"><span data-stu-id="46564-435">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="46564-436">Görev 2-ViewModel sınıfına özellikler ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="46564-437">Beklenen HTML yanıtını oluşturmak için StoreController 'dan görünüm şablonuna geçirilecek iki parametre vardır: depodaki tür tarzların sayısı ve bu tarzların bir listesi.</span><span class="sxs-lookup"><span data-stu-id="46564-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="46564-438">Bu görevde, bu 2 özellikleri **Storeındexviewmodel** sınıfına ekleyeceksiniz: **numberoftarzlar** (bir tamsayı) ve **tarzlar** (dizeler listesi).</span><span class="sxs-lookup"><span data-stu-id="46564-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="46564-439">**Storeındexviewmodel** sınıfına **numberoftarzlar** ve **tarzlar** özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="46564-440">Bunu yapmak için, aşağıdaki 2 satırı sınıf tanımına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="46564-441">(Kod parçacığı- *ASP.NET MVC 4 temelleri-eX5 Storeındexviewmodel özellikleri*)</span><span class="sxs-lookup"><span data-stu-id="46564-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="46564-442">**{Get; set;}** gösterimi, otomatik olarak C#uygulanan özellikler özelliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="46564-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="46564-443">Bir destek alanı bildirmek zorunda kalmadan özelliğin avantajlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="46564-444">Görev 3-StoreController 'ı Storeındexviewmodel kullanacak şekilde güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="46564-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="46564-445">**Storeındexviewmodel** sınıfı, bir yanıt oluşturmak Için **Storecontroller**'ın **Dizin** yönteminden bir görünüm şablonuna geçmesi gereken bilgileri saklar.</span><span class="sxs-lookup"><span data-stu-id="46564-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="46564-446">Bu görevde **Storecontroller** 'ı **Storeındexviewmodel**kullanacak şekilde güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="46564-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="46564-447">**Storecontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="46564-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="46564-448">![StoreController sınıfı açılıyor](aspnet-mvc-4-fundamentals/_static/image21.png "StoreController sınıfı açılıyor")</span><span class="sxs-lookup"><span data-stu-id="46564-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="46564-449">*StoreController sınıfı açılıyor*</span><span class="sxs-lookup"><span data-stu-id="46564-449">*Opening StoreController class*</span></span>
2. <span data-ttu-id="46564-450">**Storecontroller**'Dan **Storeındexviewmodel** sınıfını kullanmak için **storecontroller** kodunun en üstüne aşağıdaki ad alanını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="46564-451">(Kod parçacığı- *ASP.NET MVC 4 temelleri-eX5 Storeındexviewmodel Viewmodeller kullanarak*)</span><span class="sxs-lookup"><span data-stu-id="46564-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="46564-452">**Storecontroller**'ın **Dizin** eylemi yöntemini, bir **storeındexviewmodel** nesnesi oluşturacak ve doldurabilmesi ve sonra bir HTML yanıtı oluşturacak şekilde bir görünüm şablonuna geçirmek üzere değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="46564-453">Laboratuvar &quot;ASP.NET MVC modellerini ve veri erişimi&quot; bir veritabanından mağaza tarzları listesini alan kodu yazarsınız.</span><span class="sxs-lookup"><span data-stu-id="46564-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="46564-454">Aşağıdaki kodda **Storeındexviewmodel**' i doldurmayacak bir kukla veri tarzı **listesi** oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="46564-455">**Storeındexviewmodel** nesnesini oluşturup ayarladıktan sonra, **görüntüleme** yöntemine bir bağımsız değişken olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="46564-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="46564-456">Bu, görünüm şablonunun bir HTML yanıtı oluşturmak için bu nesneyi kullanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="46564-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="46564-457">**Index** metodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="46564-458">(Kod parçacığı- *ASP.NET MVC 4 temelleri-eX5 StoreController Dizin yöntemi*)</span><span class="sxs-lookup"><span data-stu-id="46564-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="46564-459">Hakkında bilginiz varsa C#, **bunu kullanmanın,** **ViewModel** değişkeninin geç bağlantılı olduğunu varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="46564-460">Doğru değil- C# derleyici, **ViewModel** 'In **storeındexviewmodel**türünde olduğunu belirlemek için değişkene ne atacağınızı temel alarak tür çıkarımı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="46564-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="46564-461">Ayrıca, yerel **ViewModel** değişkenini bir **storeındexviewmodel** türü olarak derlerken derleme zamanı denetimi ve Visual Studio kod Düzenleyicisi desteği alırsınız.</span><span class="sxs-lookup"><span data-stu-id="46564-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="46564-462">Görev 4-Storeındexviewmodel kullanan bir görünüm şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="46564-463">Bu görevde, bir tür listesi görüntülemek için denetleyiciden geçirilen bir Storeındexviewmodel nesnesi kullanacak bir görünüm şablonu oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="46564-464">Yeni görünüm şablonunu oluşturmadan önce, **görünümü Ekle Iletişim kutusu** **Storeındexviewmodel** sınıfı hakkında bilgi sahibi olacak şekilde projeyi derlim.</span><span class="sxs-lookup"><span data-stu-id="46564-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="46564-465">**Build** menü öğesini seçerek projeyi derleyin ve ardından **MvcMusicStore**' u oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46564-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="46564-466">![Projeyi oluşturma](aspnet-mvc-4-fundamentals/_static/image22.png "Projeyi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="46564-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="46564-467">*Projeyi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="46564-467">*Building the project*</span></span>
2. <span data-ttu-id="46564-468">Yeni bir görünüm şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46564-468">Create a new View template.</span></span> <span data-ttu-id="46564-469">Bunu yapmak için, **Dizin** yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="46564-470">![Görünüm Ekleme](aspnet-mvc-4-fundamentals/_static/image23.png "Görünüm Ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="46564-471">*Görünüm Ekleme*</span><span class="sxs-lookup"><span data-stu-id="46564-471">*Adding a View*</span></span>
3. <span data-ttu-id="46564-472">Dosya **Ekle Iletişim kutusu** **storecontroller**'dan çağrıldığı için, bir **\Views\store\ındex.cshtml** dosyasında görünüm şablonunu varsayılan olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="46564-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="46564-473">Kesin olarak **yazılmış görünüm oluştur** onay kutusunu işaretleyin ve ardından **model sınıfı**olarak **storeındexviewmodel** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="46564-474">Ayrıca, seçilen görünüm altyapısının **Razor**olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="46564-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="46564-475">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="46564-475">Click **Add**.</span></span>

    <span data-ttu-id="46564-476">![Görünüm Ekle Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image24.png "Görünüm Ekle Iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="46564-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="46564-477">*Görünüm Ekle Iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="46564-477">*Add View Dialog*</span></span>

    <span data-ttu-id="46564-478">**\Views\store\ındex.cshtml** görünüm şablonu dosyası oluşturulup açılır.</span><span class="sxs-lookup"><span data-stu-id="46564-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="46564-479">Son adımda **Görünüm Ekle** iletişim kutusuna sunulan bilgilere bağlı olarak, görünüm şablonu, bir HTML yanıtı oluşturmak için kullanılacak veriler olarak bir **Storeındexviewmodel** örneği bekler.</span><span class="sxs-lookup"><span data-stu-id="46564-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="46564-480">Şablonun ' de C#bir `ViewPage<musicstore.viewmodels.storeindexviewmodel>` devraldığını fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="46564-481">Görev 5-görünüm şablonunu güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="46564-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="46564-482">Bu görevde, sayfa içindeki sıra sayısını ve bunların adlarını almak için son görevde oluşturulan görünüm şablonunu güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="46564-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="46564-483">Görünüm şablonu içinde kodu yürütmek için @ söz dizimini (genellikle &quot;kodu nugal&quot;olarak adlandırılır) kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="46564-484">**Index. cshtml** dosyasında, **Mağaza** klasörü içinde, kodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. <span data-ttu-id="46564-485">**Storeındexviewmodel** içinde tarz listesinin üzerinde döngü yapın ve **foreach** döngüsü kullanarak bir HTML **&lt;ul&gt;** listesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46564-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="46564-486">(C#)</span><span class="sxs-lookup"><span data-stu-id="46564-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="46564-487">**F5** tuşuna basarak uygulamayı çalıştırın ve **/Store**'a gidin.</span><span class="sxs-lookup"><span data-stu-id="46564-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="46564-488">**Storeındexviewmodel** nesnesine **storecontroller** ' dan görünüm şablonuna geçirilen tarzlar listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="46564-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="46564-489">![Tarzın bir listesini görüntülemeyi görüntüle](aspnet-mvc-4-fundamentals/_static/image26.png "Tarzın bir listesini görüntülemeyi görüntüle")</span><span class="sxs-lookup"><span data-stu-id="46564-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="46564-490">*Tarzın bir listesini görüntülemeyi görüntüle*</span><span class="sxs-lookup"><span data-stu-id="46564-490">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="46564-491">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="46564-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="46564-492">Alıştırma 6: görünümdeki parametreleri kullanma</span><span class="sxs-lookup"><span data-stu-id="46564-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="46564-493">Alıştırma 3 ' te, parametreleri denetleyiciye geçirme hakkında daha fazla öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="46564-494">Bu alıştırmada, bu parametreleri görünüm şablonunda nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="46564-495">Bu amaçla, ilk olarak verilerinizi ve etki alanı mantığınızı yönetmenize yardımcı olacak sınıfların model olarak tanıtılcaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="46564-496">Ayrıca, URL yolları kodlaması gibi şeyleri endişelenmeden ASP.NET MVC uygulamasının içindeki sayfalara bağlantılar oluşturmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="46564-497">Görev 1-model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="46564-498">Denetleyiciden görünüme bilgi geçirmek için oluşturulan ViewModel aksine, model sınıfları veri ve etki alanı mantığını içerecek ve yönetecek şekilde oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="46564-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="46564-499">Bu görevde, şu kavramları temsil eden iki model sınıfı ekleyeceksiniz: **tarz** ve **Albüm**.</span><span class="sxs-lookup"><span data-stu-id="46564-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="46564-500">Zaten açık değilse, **Web için vs Express** başlatın</span><span class="sxs-lookup"><span data-stu-id="46564-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="46564-501">**Dosya** menüsünde **Proje Aç**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="46564-502">Proje Aç iletişim kutusunda **Source\ex06-usingparametersinview\begin**öğesine göz atın, **BEGIN. sln** ' yi seçin ve **Aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="46564-503">Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="46564-504">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="46564-505">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="46564-506">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="46564-507">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="46564-508">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="46564-509">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="46564-510">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="46564-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="46564-511">Bir **tarz** model sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="46564-512">Bunu yapmak için **Çözüm Gezgini** **modeller** klasörüne sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="46564-513">**Kod**altında, **sınıf** öğesini seçin ve dosyayı *genre.cs*olarak adlandırın, ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="46564-514">![Sınıf ekleme](aspnet-mvc-4-fundamentals/_static/image27.png "Sınıf ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="46564-515">*Yeni öğe ekleme*</span><span class="sxs-lookup"><span data-stu-id="46564-515">*Adding a new item*</span></span>

    <span data-ttu-id="46564-516">![Tarz model sınıfı Ekle](aspnet-mvc-4-fundamentals/_static/image28.png "Tarz model sınıfı Ekle")</span><span class="sxs-lookup"><span data-stu-id="46564-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="46564-517">*Tarz model sınıfı Ekle*</span><span class="sxs-lookup"><span data-stu-id="46564-517">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="46564-518">Tarz sınıfına bir **Name** özelliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="46564-519">Bunu yapmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-519">To do this, add the following code:</span></span>

    <span data-ttu-id="46564-520">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 tarzı*)</span><span class="sxs-lookup"><span data-stu-id="46564-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="46564-521">Önceki yordamın aynısını takip eden bir **Albüm** sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="46564-522">Bunu yapmak için **Çözüm Gezgini** **modeller** klasörüne sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="46564-523">**Kod**altında, **sınıf** öğesini seçin ve dosyayı *Album.cs*olarak adlandırın, ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="46564-524">Albüm sınıfına iki özellik ekleyin: **tarz** ve **başlık**.</span><span class="sxs-lookup"><span data-stu-id="46564-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="46564-525">Bunu yapmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-525">To do this, add the following code:</span></span>

    <span data-ttu-id="46564-526">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 albüm*)</span><span class="sxs-lookup"><span data-stu-id="46564-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="46564-527">Görev 2-StoreBrowseViewModel ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="46564-528">Bu görevde bir **StoreBrowseViewModel** , seçilen bir tarz Ile eşleşen albümleri göstermek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="46564-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="46564-529">Bu görevde, bu sınıfı oluşturacak ve ardından **tarzını** ve **albümün**listesini işlemek için iki özellik ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="46564-530">Bir **StoreBrowseViewModel** sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="46564-531">Bunu yapmak için **Çözüm Gezgini** **viewmodeller** klasörüne sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="46564-532">**Kod**altında, **sınıf** öğesini seçin ve dosyayı *StoreBrowseViewModel.cs*olarak adlandırın, ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="46564-533">**StoreBrowseViewModel** sınıfındaki modellere bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="46564-534">Bunu yapmak için şu ad alanını kullanarak şunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="46564-535">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 UsingModel*)</span><span class="sxs-lookup"><span data-stu-id="46564-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="46564-536">**StoreBrowseViewModel** sınıfına iki özellik ekleyin: **tarz** ve **Albümler**.</span><span class="sxs-lookup"><span data-stu-id="46564-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="46564-537">Bunu yapmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-537">To do this, add the following code:</span></span>

    <span data-ttu-id="46564-538">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 ModelProperties*)</span><span class="sxs-lookup"><span data-stu-id="46564-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="46564-539">**Liste&lt;albüm&gt;** nedir?: Bu tanım, bu **listedeki** öğelerin ait olduğu türü **(veya** alt öğelerinden herhangi biri **) kısıtlayan t** **&gt;türü&lt;** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="46564-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="46564-540">Sınıf veya yöntem bildirilmeden ve istemci kodu tarafından örneklendirilene kadar bir veya daha fazla türün belirtimini erteleme sınıfları ve yöntemleri tasarlayabilme özelliği, C# **Genel türler**adlı dilin bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="46564-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="46564-541">**Liste&lt;t&gt;** , **ArrayList** türünün genel eşdeğeridir ve **System. Collections. Generic** ad alanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="46564-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="46564-542">**Genel türleri** kullanmanın avantajlarından biri, tür belirtilmesinden bu yana, bir **ArrayList**Ile yaptığınız gibi öğeleri **albüme** atama gibi tür denetleme işlemlerine gerek duymamak zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="46564-543">Görev 3-StoreController 'da yeni ViewModel kullanma</span><span class="sxs-lookup"><span data-stu-id="46564-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="46564-544">Bu görevde, yeni **StoreBrowseViewModel**kullanmak Için **Storecontroller**'ın **gezinme** ve **Ayrıntılar** eylem yöntemlerini değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="46564-545">**Storecontroller** sınıfındaki modeller klasörüne bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="46564-546">Bunu yapmak için, **Çözüm Gezgini** **denetleyiciler** klasörünü genişletin ve **storecontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="46564-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="46564-547">Ardından aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-547">Then add the following code:</span></span>

    <span data-ttu-id="46564-548">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 UsingModelInController*)</span><span class="sxs-lookup"><span data-stu-id="46564-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="46564-549">**StoreViewBrowseController** sınıfını kullanmak Için, **gezinme** eylemi yöntemini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="46564-550">Kukla verilerle bir tarz ve iki yeni albümler nesnesi oluşturacaksınız (bir sonraki uygulamalı laboratuvarda bir veritabanından gerçek veriler kullanacaksınız).</span><span class="sxs-lookup"><span data-stu-id="46564-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="46564-551">Bunu yapmak için, aşağıdaki kodla birlikte, **Gözatılacak** yöntemi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="46564-552">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="46564-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="46564-553">**Ayrıntılar** eylem yöntemini **StoreViewBrowseController** sınıfını kullanacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="46564-554">**Görünüme**döndürülecek yeni bir **Albüm** nesnesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="46564-555">Bunu yapmak için, **Details** yöntemini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="46564-556">(Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 Ayrıntılar yöntemi*)</span><span class="sxs-lookup"><span data-stu-id="46564-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="46564-557">Görev 4-bir tarayıcı görünümü şablonu ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="46564-558">Bu görevde, belirli bir tarz için bulunan albümleri göstermek üzere bir **tarama** görünümü ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="46564-559">Yeni görünüm şablonunu oluşturmadan önce, **görünümü Ekle** iletişim kutusunun kullanılacak **ViewModel** sınıfını bilmesi için projeyi derlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="46564-560">**Build** menü öğesini seçerek projeyi derleyin ve ardından **MvcMusicStore**' u oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46564-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="46564-561">Bir **tarama** görünümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-561">Add a **Browse** View.</span></span> <span data-ttu-id="46564-562">Bunu yapmak için **Storecontroller** 'ın **gözatmaya** yönelik eylem yöntemine sağ tıklayın ve **Görünüm Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="46564-563">**Görünüm Ekle** Iletişim kutusunda görünüm adının **gözatmasını**doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="46564-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="46564-564">**Türü kesin belirlenmiş görünüm oluştur** onay kutusunu Işaretleyin ve **model sınıfı** açılan listesinden **StoreBrowseViewModel** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="46564-565">Diğer alanları varsayılan değerlerine bırakın.</span><span class="sxs-lookup"><span data-stu-id="46564-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="46564-566">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-566">Then click **Add**.</span></span>

    <span data-ttu-id="46564-567">![Bir tarama görünümü ekleme](aspnet-mvc-4-fundamentals/_static/image29.png "Bir tarama görünümü ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="46564-568">*Bir tarama görünümü ekleme*</span><span class="sxs-lookup"><span data-stu-id="46564-568">*Adding a Browse View*</span></span>
4. <span data-ttu-id="46564-569">Görünüm şablonuna geçirilen **StoreBrowseViewModel** nesnesine erişmek için, denetimin bilgilerini görüntülemek üzere **Gözat. cshtml** 'yi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="46564-570">Bunu yapmak için içeriği şu şekilde değiştirin: (C#)</span><span class="sxs-lookup"><span data-stu-id="46564-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="46564-571">5\. Görev-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46564-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="46564-572">Bu görevde **, Gezinme yönteminin** Albümler **'e gözatamıyorum** eylemini alacağını test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="46564-573">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="46564-574">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="46564-574">The project starts in the Home page.</span></span> <span data-ttu-id="46564-575">URL 'YI **/Store/zat değiştirin mi? Tarz = disco** , eylemin Iki albüm döndürdüğünden emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="46564-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="46564-576">![Store disco albümlerine göz atma](aspnet-mvc-4-fundamentals/_static/image30.png "Store disco albümlerine göz atma")</span><span class="sxs-lookup"><span data-stu-id="46564-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="46564-577">*Store disco albümlerine göz atma*</span><span class="sxs-lookup"><span data-stu-id="46564-577">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="46564-578">Görev 6-belirli bir albüm hakkındaki bilgileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="46564-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="46564-579">Bu görevde, belirli bir albüm hakkındaki bilgileri görüntülemek için **Mağaza/Ayrıntılar** görünümünü uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="46564-580">Bu uygulamalı laboratuvarda, albüm hakkında görüntülenecek her şey zaten **Görünüm** şablonunda yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="46564-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="46564-581">Bu nedenle, bir **storebir ViewModel** sınıfı oluşturmak yerine, albümü kendisine geçirerek geçerli **StoreBrowseViewModel** şablonunu kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="46564-582">Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="46564-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="46564-583">**Storecontroller**'ın **Ayrıntılar** eylem yöntemi için yeni bir **Ayrıntılar** görünümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="46564-584">Bunu yapmak için **Storecontroller** sınıfında **Details** yöntemine sağ tıklayın ve **Görünüm Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="46564-585">**Görünüm Ekle** Iletişim kutusunda **görünüm adının** **Ayrıntılar**olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="46564-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="46564-586">**Türü kesin belirlenmiş görünüm oluştur** onay kutusunu Işaretleyin ve **model sınıfı** açılır listesinden **Albüm** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="46564-587">Diğer alanları varsayılan değerlerine bırakın.</span><span class="sxs-lookup"><span data-stu-id="46564-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="46564-588">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-588">Then click **Add**.</span></span> <span data-ttu-id="46564-589">Bu, **\Views\store\details.cshtml** dosyasını oluşturur ve açar.</span><span class="sxs-lookup"><span data-stu-id="46564-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="46564-590">![Ayrıntı görünümü ekleme](aspnet-mvc-4-fundamentals/_static/image31.png "Ayrıntı görünümü ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="46564-591">*Ayrıntı görünümü ekleme*</span><span class="sxs-lookup"><span data-stu-id="46564-591">*Adding a Details View*</span></span>
3. <span data-ttu-id="46564-592">View şablonuna geçirilen **Albüm** nesnesine erişerek albümün bilgilerini görüntülemek için **details. cshtml** dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="46564-593">Bunu yapmak için içeriği şu şekilde değiştirin: (C#)</span><span class="sxs-lookup"><span data-stu-id="46564-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="46564-594">Görev 7-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46564-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="46564-595">Bu **görevde, Ayrıntılar görünümünün,** **Ayrıntılar eylem** yönteminden albümün bilgilerini alacağını test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="46564-596">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="46564-597">Proje **giriş** sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="46564-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="46564-598">Albümün bilgilerini doğrulamak için URL 'YI **/Store/details/5** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="46564-599">![Albümler 'e göz atma ayrıntısı](aspnet-mvc-4-fundamentals/_static/image32.png "Albümler 'e göz atma ayrıntısı")</span><span class="sxs-lookup"><span data-stu-id="46564-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="46564-600">*Albümün ayrıntısına göz atma*</span><span class="sxs-lookup"><span data-stu-id="46564-600">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="46564-601">Görev 8-sayfalar arasında bağlantı ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="46564-602">Bu görevde, her tarz adında uygun **/Store/gözatam** URL 'sine bağlantı sağlamak Için mağaza görünümünde bir bağlantı ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="46564-603">Bu şekilde, bir tarz üzerine tıkladığınızda, **disco**örneği için **/Store/gözatmaya? tarzı = disco** URL 'sine gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="46564-604">Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="46564-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="46564-605">**Tarayıcı** sayfasına bir bağlantı eklemek için **Dizin** sayfasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="46564-606">Bunu yapmak için, **Çözüm Gezgini** **Görünümler** klasörünü ve ardından **Mağaza** klasörünü genişletin ve **Index. cshtml** sayfasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="46564-607">Seçili tarzın seçili olduğunu gösteren bir tarayıcı görünümüne bağlantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="46564-608">Bunu yapmak için, **&lt;li&gt;** etiketleri içinde aşağıdaki vurgulanmış kodu değiştirin: (C#)</span><span class="sxs-lookup"><span data-stu-id="46564-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="46564-609">başka bir yaklaşım, aşağıdaki gibi bir kod ile doğrudan sayfaya bağlanıyor:</span><span class="sxs-lookup"><span data-stu-id="46564-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="46564-610">&lt;a href =&quot;/Store/gözatmaya? tarzı =@genreName&quot;&gt;@genreName&lt;/a&gt;</span><span class="sxs-lookup"><span data-stu-id="46564-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="46564-611">Bu yaklaşım işe yarar olsa da, sabit kodlanmış bir dizeye bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="46564-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="46564-612">Denetleyiciyi daha sonra yeniden adlandırırsanız, bu yönergeyi el ile değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="46564-613">Daha iyi bir alternatif, bir **HTML yardımcı** yöntemi kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="46564-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="46564-614">ASP.NET MVC, bu gibi görevler için kullanılabilen bir HTML yardımcı yöntemi içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="46564-615">**HTML. ActionLink ()** yardımcı YÖNTEMI, URL yollarının düzgün şekilde URL kodlamalı olduğundan emin olmak için html **&lt;&gt;** bağlantıları oluşturmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="46564-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="46564-616">HTML. ActionLink çeşitli aşırı yüklemeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="46564-616">Html.ActionLink has several overloads.</span></span> <span data-ttu-id="46564-617">Bu alıştırmada, üç parametre alan bir tane kullanacaksınız:</span><span class="sxs-lookup"><span data-stu-id="46564-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="46564-618">Bağlantı metni, bu tarz adı görüntülenecektir</span><span class="sxs-lookup"><span data-stu-id="46564-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="46564-619">Denetleyici eylem adı (**tarama**)</span><span class="sxs-lookup"><span data-stu-id="46564-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="46564-620">Ad (**tarz**) ve değer (**tarzı adı**) belirterek rota parametre değerleri</span><span class="sxs-lookup"><span data-stu-id="46564-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="46564-621">Görev 9-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46564-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="46564-622">Bu görevde, her bir tarzı uygun **/Store/gözatam** URL 'sine yönelik bir bağlantıyla birlikte görüntülendiğini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="46564-623">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="46564-624">Proje giriş sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="46564-624">The project starts in the Home page.</span></span> <span data-ttu-id="46564-625">Her bir tarzı uygun **/Store/gözam** URL 'sine bağlabildiğini doğrulamak için **/Store** URL 'sini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="46564-626">![Göz atma sayfası bağlantıları ile tarzlara göz atma](aspnet-mvc-4-fundamentals/_static/image33.png "Göz atma sayfası bağlantıları ile tarzlara göz atma")</span><span class="sxs-lookup"><span data-stu-id="46564-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="46564-627">*Göz atma sayfası bağlantıları ile tarzlara göz atma*</span><span class="sxs-lookup"><span data-stu-id="46564-627">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="46564-628">Görev 10-değerleri geçirmek için dinamik ViewModel koleksiyonu kullanma</span><span class="sxs-lookup"><span data-stu-id="46564-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="46564-629">Bu görevde, modelde değişiklik yapmadan denetleyiciyi ve görünümü arasında değerleri geçirmek için basit ve güçlü bir yöntem öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="46564-630">ASP.NET MVC 4, herhangi bir dinamik değere atanabilecek ve denetleyicilerin ve görünümlerin içinde erişilebilen &quot;ViewModel&quot;koleksiyonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="46564-631">Artık, denetleyiciden görünüme&quot; &quot;**starred tarzları** listesini geçirmek Için ViewBag dinamik toplamayı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46564-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="46564-632">Mağaza dizini görünümü **ViewModel** 'e erişir ve bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="46564-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="46564-633">Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="46564-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="46564-634">ViewModel koleksiyonunda yıldızlı tarzının bir listesini oluşturmak için **StoreController.cs** ve **dizini** Değiştir metodunu açın:</span><span class="sxs-lookup"><span data-stu-id="46564-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="46564-635">Özelliklere erişmek için **ViewBag [&quot;starred&quot;]** sözdizimini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="46564-636">&quot;, bu laboratuvarın **Source\assets\ımages** klasörüne **startred. png&quot;** yıldız simgesi dahildir.</span><span class="sxs-lookup"><span data-stu-id="46564-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="46564-637">Uygulamayı uygulamaya eklemek için, **Windows Gezgini** penceresinden içeriğini aşağıda gösterildiği gibi Visual Web Developer Express içindeki **Çözüm Gezgini** sürükleyin:</span><span class="sxs-lookup"><span data-stu-id="46564-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="46564-638">![Çözüme yıldızlı resim ekleme](aspnet-mvc-4-fundamentals/_static/image34.png "Çözüme yıldızlı resim ekleme")</span><span class="sxs-lookup"><span data-stu-id="46564-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="46564-639">*Çözüme yıldızlı resim ekleme*</span><span class="sxs-lookup"><span data-stu-id="46564-639">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="46564-640">**Store/Index. cshtml** görünümünü açın ve içeriği değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="46564-641">**ViewBag** koleksiyonundaki &quot;yıldızlı&quot; özelliğini okuyacaksınız ve geçerli tarz adının listede olup olmadığını sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="46564-642">Bu durumda, tarz bağlantısına doğrudan bir yıldız simgesi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="46564-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="46564-643">(C#)</span><span class="sxs-lookup"><span data-stu-id="46564-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="46564-644">Görev 11-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46564-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="46564-645">Bu görevde, yıldızlı tarzının bir yıldız simgesi göstermesini test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="46564-646">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="46564-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="46564-647">Proje **giriş** sayfasında başlar.</span><span class="sxs-lookup"><span data-stu-id="46564-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="46564-648">Tüm öne çıkan tarzın daha önce bir etiket içerdiğini doğrulamak için URL 'YI **/Store** olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46564-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="46564-649">![Yıldızlı öğeleriyle tarzlara göz atma](aspnet-mvc-4-fundamentals/_static/image35.png "Yıldızlı öğeleriyle tarzlara göz atma")</span><span class="sxs-lookup"><span data-stu-id="46564-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="46564-650">*Yıldızlı öğeleriyle tarzlara göz atma*</span><span class="sxs-lookup"><span data-stu-id="46564-650">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="46564-651">Alıştırma 7: ASP.NET MVC 4 yeni şablonu etrafında bir lap</span><span class="sxs-lookup"><span data-stu-id="46564-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="46564-652">Bu alıştırmada, yeni şablonun en ilgili özelliklerine göz önünde bulundurularak ASP.NET MVC 4 proje şablonlarındaki geliştirmeleri araştıracaktır.</span><span class="sxs-lookup"><span data-stu-id="46564-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="46564-653">Görev 1: ASP.NET MVC 4 Internet uygulaması şablonunu keşfetme</span><span class="sxs-lookup"><span data-stu-id="46564-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="46564-654">Zaten açık değilse, **Web için vs Express** başlatın</span><span class="sxs-lookup"><span data-stu-id="46564-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="46564-655">Dosyayı seçin **| Yeni | Proje** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="46564-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="46564-656">**Yeni proje** Iletişim kutusunda **görseli C#seçin |** Sol bölme ağacındaki Web şablonu ve **ASP.NET MVC 4 Web uygulamasını**seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="46564-657">Projeyi *MusicStore* olarak **adlandırın** ve *başlamak*için **çözüm adını** güncelleştirin, ardından bir konum seçin (veya varsayılanı bırakın) ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="46564-658">![Yeni bir ASP.NET MVC 4 projesi oluşturma](aspnet-mvc-4-fundamentals/_static/image36.png "Yeni bir ASP.NET MVC 4 projesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="46564-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="46564-659">*Yeni bir ASP.NET MVC 4 projesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="46564-659">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="46564-660">**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** proje şablonunu seçin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="46564-661">Görünüm altyapısı olarak Razor veya ASPX seçeneklerinden birini belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="46564-662">![Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma](aspnet-mvc-4-fundamentals/_static/image37.png "Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma")</span><span class="sxs-lookup"><span data-stu-id="46564-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="46564-663">*Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma*</span><span class="sxs-lookup"><span data-stu-id="46564-663">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="46564-664">Razor söz dizimi, ASP.NET MVC 3 ' te tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="46564-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="46564-665">Amacı, bir dosyada gereken karakter ve tuş vuruşlarının sayısını en aza indirmektir ve hızlı ve akıcı bir kodlama iş akışını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="46564-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="46564-666">Razor, mevcut C#/vb (veya diğer) dil becerilerini kullanır ve harıka bir HTML oluşturma iş akışı sağlayan bir şablon biçimlendirme sözdizimi sunar.</span><span class="sxs-lookup"><span data-stu-id="46564-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="46564-667">**F5** tuşuna basarak çözümü çalıştırın ve yenilenen şablonu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="46564-668">Aşağıdaki özelliklere bakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46564-668">You can check out the following features:</span></span>

    1. <span data-ttu-id="46564-669">**Modern stil şablonları**</span><span class="sxs-lookup"><span data-stu-id="46564-669">**Modern-style templates**</span></span>

        <span data-ttu-id="46564-670">Şablonlar, daha modern görünümlü daha fazla stil sunarak yenilendi.</span><span class="sxs-lookup"><span data-stu-id="46564-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="46564-671">![ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar")</span><span class="sxs-lookup"><span data-stu-id="46564-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="46564-672">*ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar*</span><span class="sxs-lookup"><span data-stu-id="46564-672">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="46564-673">**Uyarlamalı Işleme**</span><span class="sxs-lookup"><span data-stu-id="46564-673">**Adaptive Rendering**</span></span>

        <span data-ttu-id="46564-674">Tarayıcı penceresini yeniden boyutlandırın ve sayfa düzeninin yeni pencere boyutuna dinamik olarak nasıl uyum sağlayadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="46564-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="46564-675">Bu şablonlar, hiçbir özelleştirme yapmadan hem masaüstü hem de mobil platformlarda düzgün şekilde işlemek için uyarlamalı işleme tekniğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="46564-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="46564-676">![Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu](aspnet-mvc-4-fundamentals/_static/image39.png "Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu")</span><span class="sxs-lookup"><span data-stu-id="46564-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="46564-677">*Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu*</span><span class="sxs-lookup"><span data-stu-id="46564-677">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="46564-678">Hata ayıklayıcıyı durdurmak ve Visual Studio 'ya dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="46564-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="46564-679">Artık çözümü keşfedebiliyor ve proje şablonunda ASP.NET MVC 4 tarafından tanıtılan yeni özelliklerden bazılarını kullanıma sunabileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="46564-680">![ASP.NET MVC4-Internet-uygulama-proje-şablon](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 Internet uygulaması proje şablonu")</span><span class="sxs-lookup"><span data-stu-id="46564-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="46564-681">*ASP.NET MVC 4 Internet uygulaması proje şablonu*</span><span class="sxs-lookup"><span data-stu-id="46564-681">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="46564-682">**HTML5 işaretleme**</span><span class="sxs-lookup"><span data-stu-id="46564-682">**HTML5 markup**</span></span>

       <span data-ttu-id="46564-683">Yeni Tema işaretlemesini öğrenmek için şablon görünümlerine gözatıp. Örneğin, **giriş** klasörü içinde **. cshtml** görünümünü açın.</span><span class="sxs-lookup"><span data-stu-id="46564-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="46564-684">![Razor ve HTML5 işaretlemesini kullanarak yeni şablon](aspnet-mvc-4-fundamentals/_static/image41.png "Razor ve HTML5 işaretlemesini kullanarak yeni şablon")</span><span class="sxs-lookup"><span data-stu-id="46564-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="46564-685">*Razor ve HTML5 işaretlemesini kullanarak yeni şablon*</span><span class="sxs-lookup"><span data-stu-id="46564-685">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="46564-686">**JavaScript kitaplıkları dahil**</span><span class="sxs-lookup"><span data-stu-id="46564-686">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="46564-687">**jQuery**: jQuery, HTML belgesi geçiş, olay işleme, animasyon uygulama ve Ajax etkileşimlerini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="46564-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="46564-688">**jQuery kullanıcı arabirimi**: Bu kitaplık, jQuery JavaScript kitaplığının üzerine inşa olan alt düzey etkileşim ve animasyon, gelişmiş etkiler ve ayrılabilir pencere öğeleri için soyutlamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="46564-689">[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)' de jQuery ve jQuery kullanıcı arabirimi hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="46564-690">**Altını gizleme koutjs**: ASP.NET MVC 4 varsayılan şablonu artık JAVASCRIPT ve HTML kullanarak zengin ve yüksek oranda yanıt veren Web uygulamaları oluşturmanıza olanak tanıyan bir JavaScript MVVM çerçevesi olan **altını gizleme**özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="46564-691">ASP.NET MVC 3 gibi, jQuery ve jQuery kullanıcı arabirimi kitaplıkları da ASP.NET MVC 4 ' te de bulunur.</span><span class="sxs-lookup"><span data-stu-id="46564-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="46564-692">Bu bağlantıdaki altını gizleme ( [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)) kitaplığı hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="46564-693">**Modernizr**: Bu kitaplık otomatik olarak ÇALıŞARAK, HTML5 ve CSS3 teknolojilerini kullanırken sitenizi eski tarayıcılarla uyumlu hale getirir.</span><span class="sxs-lookup"><span data-stu-id="46564-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="46564-694">Bu bağlantıda Modernizr Kitaplığı hakkında daha fazla bilgi edinebilirsiniz: [http://www.modernizr.com/](http://www.modernizr.com/).</span><span class="sxs-lookup"><span data-stu-id="46564-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="46564-695">**Çözüme dahil SimpleMembership**</span><span class="sxs-lookup"><span data-stu-id="46564-695">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="46564-696">SimpleMembership, önceki ASP.NET rolü ve üyelik sağlayıcısı sisteminin yerini alacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="46564-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="46564-697">Geliştiricinin web sayfalarını daha esnek bir şekilde güvenli hale getirmeye daha kolay bir şekilde bir çok yeni özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="46564-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="46564-698">Internet şablonu, SimpleMembership tümleştirmeye yönelik birkaç şey ayarlamış. Örneğin, AccountController OAuthWebSecurity 'yi (OAuth hesabı kaydı, oturum açma, yönetim, vs.) ve web güvenliği 'ni kullanmaya hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="46564-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="46564-699">![Çözüme dahil SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "Çözüme dahil SimpleMembership")</span><span class="sxs-lookup"><span data-stu-id="46564-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="46564-700">*Çözüme dahil SimpleMembership*</span><span class="sxs-lookup"><span data-stu-id="46564-700">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="46564-701">MSDN 'de [Oauthwebsecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="46564-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="46564-702">Ek olarak, bu uygulamayı Microsoft Azure Web siteleri ' ne ek [B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixB)için de dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="46564-703">Özet</span><span class="sxs-lookup"><span data-stu-id="46564-703">Summary</span></span>

<span data-ttu-id="46564-704">Bu uygulamalı Laboratuvarı tamamlayarak ASP.NET MVC 'nin temellerini öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="46564-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="46564-705">MVC uygulamasının temel öğeleri ve bunların nasıl etkileşimde bulunduğu</span><span class="sxs-lookup"><span data-stu-id="46564-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="46564-706">ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="46564-707">URL ve QueryString aracılığıyla geçirilen parametreleri işlemek için denetleyicileri ekleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46564-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="46564-708">Genel HTML içeriği için şablon ayarlamak üzere bir düzen ana sayfası ekleme, HTML içeriğini görüntülemek için görünüm ve görüntüleme şablonunu iyileştirmek üzere bir stil sayfası.</span><span class="sxs-lookup"><span data-stu-id="46564-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="46564-709">Dinamik bilgileri görüntülemek için görünüm şablonuna Özellikler geçirmek için ViewModel deseninin nasıl kullanılacağı</span><span class="sxs-lookup"><span data-stu-id="46564-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="46564-710">Görünüm şablonunda denetleyicilere geçirilen parametreleri kullanma</span><span class="sxs-lookup"><span data-stu-id="46564-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="46564-711">ASP.NET MVC uygulamasının içindeki sayfalara bağlantı ekleme</span><span class="sxs-lookup"><span data-stu-id="46564-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="46564-712">Bir görünümde dinamik özellikler ekleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="46564-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="46564-713">ASP.NET MVC 4 proje şablonlarındaki geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="46564-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="46564-714">Ek A: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="46564-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="46564-715">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="46564-716">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="46564-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="46564-717">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin.</span><span class="sxs-lookup"><span data-stu-id="46564-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="46564-718">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="46564-719">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-719">Click on **Install Now**.</span></span> <span data-ttu-id="46564-720">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="46564-721">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="46564-722">![Visual Studio Express yüklensin](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="46564-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="46564-723">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="46564-723">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="46564-724">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="46564-726">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="46564-726">*Accepting the license terms*</span></span>
5. <span data-ttu-id="46564-727">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-727">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="46564-729">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="46564-729">*Installation progress*</span></span>
6. <span data-ttu-id="46564-730">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-730">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="46564-732">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="46564-732">*Installation completed*</span></span>
7. <span data-ttu-id="46564-733">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="46564-734">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="46564-736">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="46564-736">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="46564-737">Ek B: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="46564-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="46564-738">Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="46564-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="46564-739">Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="46564-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="46564-740">[Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="46564-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="46564-741">Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="46564-742">[Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-742">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="46564-743">![Windows Azure portal oturum açın](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure portal oturum açın")</span><span class="sxs-lookup"><span data-stu-id="46564-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="46564-744">*Windows Azure 'da oturum açma Yönetim Portalı*</span><span class="sxs-lookup"><span data-stu-id="46564-744">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="46564-745">Komut çubuğunda **Yeni** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="46564-746">![Yeni bir Web sitesi oluşturma](aspnet-mvc-4-fundamentals/_static/image49.png "Yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="46564-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="46564-747">*Yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="46564-747">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="46564-748">**İşlem** | **Web sitesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="46564-749">Sonra **hızlı oluştur** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="46564-750">Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="46564-751">Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="46564-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="46564-752">Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="46564-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="46564-753">Bir veritabanı ayarlamaya yönelik adımları içermez.</span><span class="sxs-lookup"><span data-stu-id="46564-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="46564-754">![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](aspnet-mvc-4-fundamentals/_static/image50.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="46564-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="46564-755">*Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="46564-755">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="46564-756">Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="46564-757">Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="46564-758">Yeni Web sitesinin çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="46564-759">![Yeni Web sitesine göz atma](aspnet-mvc-4-fundamentals/_static/image51.png "Yeni Web sitesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="46564-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="46564-760">*Yeni Web sitesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="46564-760">*Browsing to the new web site*</span></span>

    <span data-ttu-id="46564-761">![Web sitesi çalışıyor](aspnet-mvc-4-fundamentals/_static/image52.png "Web sitesi çalışıyor")</span><span class="sxs-lookup"><span data-stu-id="46564-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="46564-762">*Web sitesi çalışıyor*</span><span class="sxs-lookup"><span data-stu-id="46564-762">*Web site running*</span></span>
6. <span data-ttu-id="46564-763">Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="46564-764">![Web sitesi yönetim sayfalarını açma](aspnet-mvc-4-fundamentals/_static/image53.png "Web sitesi yönetim sayfalarını açma")</span><span class="sxs-lookup"><span data-stu-id="46564-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="46564-765">*Web sitesi yönetim sayfalarını açma*</span><span class="sxs-lookup"><span data-stu-id="46564-765">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="46564-766">**Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="46564-767">*Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="46564-768">Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="46564-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="46564-769">**Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="46564-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="46564-770">![Web sitesi yayımlama profili indiriliyor](aspnet-mvc-4-fundamentals/_static/image54.png "Web sitesi yayımlama profili indiriliyor")</span><span class="sxs-lookup"><span data-stu-id="46564-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="46564-771">*Web sitesi yayımlama profili indiriliyor*</span><span class="sxs-lookup"><span data-stu-id="46564-771">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="46564-772">Yayımlama profili dosyasını bilinen bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="46564-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="46564-773">Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="46564-774">![Yayımlama profili dosyası kaydediliyor](aspnet-mvc-4-fundamentals/_static/image55.png "Yayımlama profili kaydediliyor")</span><span class="sxs-lookup"><span data-stu-id="46564-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="46564-775">*Yayımlama profili dosyası kaydediliyor*</span><span class="sxs-lookup"><span data-stu-id="46564-775">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="46564-776">Görev 2-veritabanı sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46564-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="46564-777">Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="46564-778">SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="46564-779">Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="46564-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="46564-780">SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="46564-781">Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="46564-782">**Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın.</span><span class="sxs-lookup"><span data-stu-id="46564-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="46564-783">Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="46564-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="46564-784">![SQL veritabanı sunucu panosu](aspnet-mvc-4-fundamentals/_static/image56.png "SQL veritabanı sunucu panosu")</span><span class="sxs-lookup"><span data-stu-id="46564-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="46564-785">*SQL veritabanı sunucu panosu*</span><span class="sxs-lookup"><span data-stu-id="46564-785">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="46564-786">Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46564-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="46564-787">Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](aspnet-mvc-4-fundamentals/_static/image57.png) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![Istemci IP adresi ekleniyor](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="46564-789">*Istemci IP adresi ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="46564-789">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="46564-790">**ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Değişiklikleri Onayla](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="46564-792">*Değişiklikleri Onayla*</span><span class="sxs-lookup"><span data-stu-id="46564-792">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="46564-793">Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="46564-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="46564-794">ASP.NET MVC 4 çözümüne geri dönün.</span><span class="sxs-lookup"><span data-stu-id="46564-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="46564-795">**Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="46564-796">![Uygulama yayımlanıyor](aspnet-mvc-4-fundamentals/_static/image60.png "Uygulamayı Yayımlama")</span><span class="sxs-lookup"><span data-stu-id="46564-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="46564-797">*Web sitesi yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="46564-797">*Publishing the web site*</span></span>
2. <span data-ttu-id="46564-798">İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="46564-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="46564-799">![Yayımlama profilini içeri aktarma](aspnet-mvc-4-fundamentals/_static/image61.png "Yayımlama profilini içeri aktarma")</span><span class="sxs-lookup"><span data-stu-id="46564-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="46564-800">*Yayımlama profili içeri aktarılıyor*</span><span class="sxs-lookup"><span data-stu-id="46564-800">*Importing publish profile*</span></span>
3. <span data-ttu-id="46564-801">**Bağlantıyı doğrula**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-801">Click **Validate Connection**.</span></span> <span data-ttu-id="46564-802">Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="46564-803">Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="46564-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="46564-804">![Bağlantı doğrulanıyor](aspnet-mvc-4-fundamentals/_static/image62.png "Bağlantı doğrulanıyor")</span><span class="sxs-lookup"><span data-stu-id="46564-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="46564-805">*Bağlantı doğrulanıyor*</span><span class="sxs-lookup"><span data-stu-id="46564-805">*Validating connection*</span></span>
4. <span data-ttu-id="46564-806">**Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="46564-807">![Web dağıtımı yapılandırması](aspnet-mvc-4-fundamentals/_static/image63.png "Web dağıtımı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="46564-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="46564-808">*Web dağıtımı yapılandırması*</span><span class="sxs-lookup"><span data-stu-id="46564-808">*Web deploy configuration*</span></span>
5. <span data-ttu-id="46564-809">Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="46564-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="46564-810">**Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.</span><span class="sxs-lookup"><span data-stu-id="46564-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="46564-811">**Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="46564-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="46564-812">**Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="46564-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="46564-813">Yeni bir veritabanı adı yazın, örneğin: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="46564-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="46564-814">![Hedef bağlantı dizesi yapılandırılıyor](aspnet-mvc-4-fundamentals/_static/image64.png "Hedef bağlantı dizesi yapılandırılıyor")</span><span class="sxs-lookup"><span data-stu-id="46564-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="46564-815">*Hedef bağlantı dizesi yapılandırılıyor*</span><span class="sxs-lookup"><span data-stu-id="46564-815">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="46564-816">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-816">Then click **OK**.</span></span> <span data-ttu-id="46564-817">Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="46564-818">![Veritabanı oluşturma](aspnet-mvc-4-fundamentals/_static/image65.png "Veritabanı dizesi oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="46564-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="46564-819">*Veritabanı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="46564-819">*Creating the database*</span></span>
7. <span data-ttu-id="46564-820">Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="46564-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="46564-821">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-821">Then click **Next**.</span></span>

    <span data-ttu-id="46564-822">![SQL veritabanı 'na işaret eden bağlantı dizesi](aspnet-mvc-4-fundamentals/_static/image66.png "SQL veritabanı 'na işaret eden bağlantı dizesi")</span><span class="sxs-lookup"><span data-stu-id="46564-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="46564-823">*SQL veritabanı 'na işaret eden bağlantı dizesi*</span><span class="sxs-lookup"><span data-stu-id="46564-823">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="46564-824">**Önizleme** sayfasında **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="46564-825">![Web uygulaması yayımlanıyor](aspnet-mvc-4-fundamentals/_static/image67.png "Web uygulaması yayımlanıyor")</span><span class="sxs-lookup"><span data-stu-id="46564-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="46564-826">*Web uygulaması yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="46564-826">*Publishing the web application*</span></span>
9. <span data-ttu-id="46564-827">Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.</span><span class="sxs-lookup"><span data-stu-id="46564-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="46564-828">![Windows Azure 'da yayımlanan uygulama](aspnet-mvc-4-fundamentals/_static/image68.png "Windows Azure 'da yayımlanan uygulama")</span><span class="sxs-lookup"><span data-stu-id="46564-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="46564-829">*Windows Azure 'da yayımlanan uygulama*</span><span class="sxs-lookup"><span data-stu-id="46564-829">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="46564-830">Ek C: kod parçacıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="46564-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="46564-831">Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46564-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="46564-832">Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="46564-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="46564-833">![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-fundamentals/_static/image69.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")</span><span class="sxs-lookup"><span data-stu-id="46564-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="46564-834">*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*</span><span class="sxs-lookup"><span data-stu-id="46564-834">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="46564-835">***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***</span><span class="sxs-lookup"><span data-stu-id="46564-835">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="46564-836">Kodu eklemek istediğiniz yere imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="46564-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="46564-837">Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).</span><span class="sxs-lookup"><span data-stu-id="46564-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="46564-838">IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="46564-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="46564-839">Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="46564-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="46564-840">Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="46564-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="46564-841">![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-fundamentals/_static/image70.png "Kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="46564-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="46564-842">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="46564-842">*Start typing the snippet name*</span></span>

<span data-ttu-id="46564-843">![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-fundamentals/_static/image71.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="46564-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="46564-844">*Vurgulanan parçacığı seçmek için Tab tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="46564-844">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="46564-845">![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-fundamentals/_static/image72.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")</span><span class="sxs-lookup"><span data-stu-id="46564-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="46564-846">*Sekmeye tekrar basın ve kod parçacığı genişletilir*</span><span class="sxs-lookup"><span data-stu-id="46564-846">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="46564-847">***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="46564-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="46564-848">Kod parçacığını eklemek istediğiniz yere sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46564-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="46564-849">Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="46564-850">Listeden tıklatarak ilgili kod parçacığını seçin.</span><span class="sxs-lookup"><span data-stu-id="46564-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="46564-851">![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-fundamentals/_static/image73.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")</span><span class="sxs-lookup"><span data-stu-id="46564-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="46564-852">*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*</span><span class="sxs-lookup"><span data-stu-id="46564-852">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="46564-853">![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-fundamentals/_static/image74.png "Listeden tıklatarak ilgili kod parçacığını seçin")</span><span class="sxs-lookup"><span data-stu-id="46564-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="46564-854">*Listeden tıklatarak ilgili kod parçacığını seçin*</span><span class="sxs-lookup"><span data-stu-id="46564-854">*Pick the relevant snippet from the list, by clicking on it*</span></span>
