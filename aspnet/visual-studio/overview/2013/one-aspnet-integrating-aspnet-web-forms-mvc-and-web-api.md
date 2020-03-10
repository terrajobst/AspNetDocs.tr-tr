---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: "Uygulamalı laboratuvar: One ASP.NET: ASP.NET Web Forms, MVC ve Web API 'sini tümleştirme | Microsoft Docs"
author: rick-anderson
description: ASP.NET, MVC, Web API 'SI ve diğerleri gibi özel teknolojiler kullanarak Web siteleri, uygulamalar ve hizmetler oluşturmaya yönelik bir çerçevedir. Genişletme ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623202"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a><span data-ttu-id="d635e-104">Uygulamalı Laboratuvar: Tek ASP.NET: ASP.NET Web Forms, MVC ve Web API’yi Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d635e-104">Hands On Lab: One ASP.NET: Integrating ASP.NET Web Forms, MVC and Web API</span></span>

<span data-ttu-id="d635e-105">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="d635e-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="d635e-106">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="d635e-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="d635e-107">ASP.NET, MVC, Web API 'SI ve diğerleri gibi özel teknolojiler kullanarak Web siteleri, uygulamalar ve hizmetler oluşturmaya yönelik bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="d635e-107">ASP.NET is a framework for building Web sites, apps and services using specialized technologies such as MVC, Web API and others.</span></span> <span data-ttu-id="d635e-108">Genişletme ASP.NET, oluşturulduktan ve bu teknolojilerin tümleşik olması gerektiğinden, **bir ASP.net**üzerinde çalışan son çalışmalar vardır.</span><span class="sxs-lookup"><span data-stu-id="d635e-108">With the expansion ASP.NET has seen since its creation and the expressed need to have these technologies integrated, there have been recent efforts in working towards **One ASP.NET**.</span></span>
> 
> <span data-ttu-id="d635e-109">Visual Studio 2013, bir uygulama oluşturmanıza ve tüm ASP.NET teknolojilerini tek bir projede kullanmanıza imkan tanıyan yeni bir birleştirilmiş proje sistemi kullanıma sunuyor.</span><span class="sxs-lookup"><span data-stu-id="d635e-109">Visual Studio 2013 introduces a new unified project system which lets you build an application and use all the ASP.NET technologies in one project.</span></span> <span data-ttu-id="d635e-110">Bu özellik projenin başlangıcında bir teknoloji seçme gereksinimini ortadan kaldırır ve bunun yerine birden çok ASP.NET Framework 'ün bir proje içinde kullanımını teşvik eder.</span><span class="sxs-lookup"><span data-stu-id="d635e-110">This feature eliminates the need to pick one technology at the start of a project and stick with it, and instead encourages the use of multiple ASP.NET frameworks within one project.</span></span>
> 
> <span data-ttu-id="d635e-111">Tüm örnek kod ve kod parçacıkları [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="d635e-111">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="d635e-112">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="d635e-112">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="d635e-113">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="d635e-113">Objectives</span></span>

<span data-ttu-id="d635e-114">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="d635e-114">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="d635e-115">**Bir ASP.net** proje türünü temel alan bir Web sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-115">Create a Web site based on the **One ASP.NET** project type</span></span>
- <span data-ttu-id="d635e-116">**MVC** ve **Web apı** gibi farklı **ASP.net** çerçeveleri aynı projede kullanın</span><span class="sxs-lookup"><span data-stu-id="d635e-116">Use different **ASP.NET** frameworks like **MVC** and **Web API** in the same project</span></span>
- <span data-ttu-id="d635e-117">Bir **ASP.net** uygulamasının ana bileşenlerini tanımla</span><span class="sxs-lookup"><span data-stu-id="d635e-117">Identify the main components of an **ASP.NET** application</span></span>
- <span data-ttu-id="d635e-118">Model sınıflarınıza göre CRUD işlemleri gerçekleştirmek üzere otomatik olarak denetleyiciler ve görünümler oluşturmak için **ASP.net Scafkatlama** çerçevesinden yararlanın</span><span class="sxs-lookup"><span data-stu-id="d635e-118">Take advantage of the **ASP.NET Scaffolding** framework to automatically create Controllers and Views to perform CRUD operations based on your model classes</span></span>
- <span data-ttu-id="d635e-119">Her iş için doğru aracı kullanarak makine ve insanlarca okunabilir biçimlerde aynı bilgi kümesini kullanıma sunun</span><span class="sxs-lookup"><span data-stu-id="d635e-119">Expose the same set of information in machine- and human-readable formats using the right tool for each job</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="d635e-120">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d635e-120">Prerequisites</span></span>

<span data-ttu-id="d635e-121">Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="d635e-121">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="d635e-122">Web veya daha büyük [için Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="d635e-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="d635e-123">Visual Studio 2013 Güncelleştirme 1</span><span class="sxs-lookup"><span data-stu-id="d635e-123">Visual Studio 2013 Update 1</span></span>](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="d635e-124">Kurulum</span><span class="sxs-lookup"><span data-stu-id="d635e-124">Setup</span></span>

<span data-ttu-id="d635e-125">Bu uygulamalı laboratuvarda alýþtýrmalarý çalıştırmak için öncelikle ortamınızı ayarlamanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="d635e-125">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="d635e-126">Windows Gezgini 'ni açın ve laboratuvarın **kaynak** klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="d635e-126">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="d635e-127">Ortamınızı yapılandıracak ve bu laboratuvar için Visual Studio kod parçacıklarını yükleyecek kurulum işlemini başlatmak için **Setup. cmd** ' ye sağ tıklayın ve **yönetici olarak çalıştır** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d635e-127">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="d635e-128">Kullanıcı hesabı denetimi iletişim kutusu gösterilirse, devam etmek için eylemi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-128">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="d635e-129">Kurulumu çalıştırmadan önce bu laboratuvarın tüm bağımlılıklarını denetlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d635e-129">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="d635e-130">Kod parçacıklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="d635e-130">Using the Code Snippets</span></span>

<span data-ttu-id="d635e-131">Laboratuvar belgesi boyunca kod blokları eklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="d635e-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="d635e-132">Kolaylık olması için, bu kodun çoğu Visual Studio Code kod parçacığı olarak sağlanır ve bu, el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio 2013 içinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-132">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="d635e-133">Her alıştırma, her alıştırmanın bağımsız olarak her birini takip etmenizi sağlayan alıştırmanın **BEGIN** klasöründe bulunan bir başlangıç çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="d635e-133">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="d635e-134">Lütfen bir alıştırma sırasında eklenen kod parçacıklarının bu başlangıç çözümlerinde eksik olduğunu ve Alıştırmayı tamamlayana kadar çalışmadığının farkında olun.</span><span class="sxs-lookup"><span data-stu-id="d635e-134">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="d635e-135">Bir alıştırmada kaynak kodun içinde, ilgili alıştırmada adımların tamamlanmasına neden olan koda sahip bir Visual Studio çözümü içeren bir **son** klasör de bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-135">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="d635e-136">Bu uygulamalı laboratuvarda çalışırken daha fazla yardıma ihtiyacınız varsa bu çözümleri kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-136">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="d635e-137">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="d635e-137">Exercises</span></span>

<span data-ttu-id="d635e-138">Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:</span><span class="sxs-lookup"><span data-stu-id="d635e-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="d635e-139">Yeni bir Web Forms projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-139">Creating a New Web Forms Project</span></span>](#Exercise1)
2. [<span data-ttu-id="d635e-140">Yapı Iskelesi kullanarak MVC denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-140">Creating an MVC Controller Using Scaffolding</span></span>](#Exercise2)
3. [<span data-ttu-id="d635e-141">Yapı Iskelesi kullanarak Web API denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-141">Creating a Web API Controller Using Scaffolding</span></span>](#Exercise3)

<span data-ttu-id="d635e-142">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**</span><span class="sxs-lookup"><span data-stu-id="d635e-142">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="d635e-143">Visual Studio 'Yu ilk kez başlattığınızda, önceden tanımlanmış ayarlar koleksiyonundan birini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d635e-143">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="d635e-144">Her önceden tanımlı koleksiyon, belirli bir geliştirme stiliyle eşleşecek şekilde tasarlanmıştır ve pencere düzenlerini, düzenleyici davranışını, IntelliSense kod parçacıklarını ve iletişim kutusu seçeneklerini belirler.</span><span class="sxs-lookup"><span data-stu-id="d635e-144">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="d635e-145">Bu laboratuvardaki yordamlarda, **genel geliştirme ayarları** koleksiyonu kullanılırken, Visual Studio 'da belirli bir görevi gerçekleştirmek için gereken eylemler açıklanır.</span><span class="sxs-lookup"><span data-stu-id="d635e-145">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="d635e-146">Geliştirme ortamınız için farklı bir ayarlar koleksiyonu seçerseniz, adımlarda dikkate almanız gereken adımlarda farklılıklar olabilir.</span><span class="sxs-lookup"><span data-stu-id="d635e-146">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a><span data-ttu-id="d635e-147">Alıştırma 1: yeni bir Web Forms projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-147">Exercise 1: Creating a New Web Forms Project</span></span>

<span data-ttu-id="d635e-148">Bu alıştırmada, aynı uygulamadaki Web Forms, MVC ve Web API bileşenlerini kolayca tümleştirmenize olanak tanıyan **ASP.net** Birleşik proje deneyimini kullanarak Visual Studio 2013 yeni bir Web Forms sitesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-148">In this exercise you will create a new Web Forms site in Visual Studio 2013 using the **One ASP.NET** unified project experience, which will allow you to easily integrate Web Forms, MVC and Web API components in the same application.</span></span> <span data-ttu-id="d635e-149">Sonra oluşturulan çözümü keşfedebilir ve parçalarını tanımlayabilir, son olarak Web sitesini çalışır durumda görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d635e-149">You will then explore the generated solution and identify its parts, and finally you will see the Web site in action.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a><span data-ttu-id="d635e-150">Görev 1 – bir ASP.NET deneyimini kullanarak yeni bir site oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-150">Task 1 – Creating a New Site Using the One ASP.NET Experience</span></span>

<span data-ttu-id="d635e-151">Bu görevde, Visual Studio 'da **bir ASP.net** proje türüne göre yeni bir Web sitesi oluşturmaya başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-151">In this task you will start creating a new Web site in Visual Studio based on the **One ASP.NET** project type.</span></span> <span data-ttu-id="d635e-152">**Bir ASP.net** tüm ASP.NET teknolojilerini birleştirir ve bunları istediğiniz gibi karıştırma ve eşleştirme seçeneği sunar.</span><span class="sxs-lookup"><span data-stu-id="d635e-152">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="d635e-153">Daha sonra uygulamanız içinde yan yana Web Forms, MVC ve Web API 'sinin farklı bileşenlerini tanıyacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-153">You will then recognize the different components of Web Forms, MVC and Web API that live side by side within your application.</span></span>

1. <span data-ttu-id="d635e-154">**Web için Visual Studio Express 2013** ' i açın ve dosya ' yı seçin **| Yeni proje...** Yeni bir çözüm başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="d635e-154">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    ![Yeni proje oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    <span data-ttu-id="d635e-156">*Yeni bir proje oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d635e-156">*Creating a New Project*</span></span>
2. <span data-ttu-id="d635e-157">**Yeni proje** iletişim kutusunda, görsel  **C# altında ASP.NET Web uygulaması ' nı seçin | Web** sekmesine ve **.NET Framework 4,5** ' nin seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d635e-157">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab, and make sure **.NET Framework 4.5** is selected.</span></span> <span data-ttu-id="d635e-158">Projeyi *Myhybridsite*olarak adlandırın, bir **konum** seçin ve **Tamam 'a**tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-158">Name the project *MyHybridSite*, choose a **Location** and click **OK**.</span></span>

    ![Yeni ASP.NET Web uygulaması projesi](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    <span data-ttu-id="d635e-160">*Yeni bir ASP.NET Web uygulaması projesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d635e-160">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="d635e-161">**Yeni ASP.NET projesi** iletişim kutusunda **Web Forms** şablonunu seçin ve **MVC** ve **Web API 'si** seçeneklerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d635e-161">In the **New ASP.NET Project** dialog box, select the **Web Forms** template and select the **MVC** and **Web API** options.</span></span> <span data-ttu-id="d635e-162">Ayrıca, **kimlik doğrulama** seçeneğinin **bireysel kullanıcı hesapları**olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d635e-162">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="d635e-163">Devam etmek için **Tamam** 'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-163">Click **OK** to continue.</span></span>

    ![Web API ve MVC bileşenleri dahil Web Forms şablonuyla yeni bir proje oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    <span data-ttu-id="d635e-165">*Web API ve MVC bileşenleri dahil Web Forms şablonuyla yeni bir proje oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d635e-165">*Creating a new project with the Web Forms template, including Web API and MVC components*</span></span>
4. <span data-ttu-id="d635e-166">Artık oluşturulan çözümün yapısını inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-166">You can now explore the structure of the generated solution.</span></span>

    ![Oluşturulan çözümü keşfetme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    <span data-ttu-id="d635e-168">*Oluşturulan çözümü keşfetme*</span><span class="sxs-lookup"><span data-stu-id="d635e-168">*Exploring the generated solution*</span></span>

    1. <span data-ttu-id="d635e-169">**Hesap:** Bu klasör, kaydedilecek Web formu sayfalarını içerir, oturum açın ve uygulamanın kullanıcı hesaplarını yönetir.</span><span class="sxs-lookup"><span data-stu-id="d635e-169">**Account:** This folder contains the Web Form pages to register, log in to and manage the application's user accounts.</span></span> <span data-ttu-id="d635e-170">Bu klasör, Web Forms projesi şablonunun yapılandırması sırasında **bireysel kullanıcı hesapları** kimlik doğrulaması seçeneği belirlendiğinde eklenir.</span><span class="sxs-lookup"><span data-stu-id="d635e-170">This folder is added when the **Individual User Accounts** authentication option is selected during the configuration of the Web Forms project template.</span></span>
    2. <span data-ttu-id="d635e-171">**Modeller:** Bu klasör, uygulama verilerinizi temsil eden sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="d635e-171">**Models:** This folder will contain the classes that represent your application data.</span></span>
    3. <span data-ttu-id="d635e-172">**Denetleyiciler** ve **Görünümler**: Bu klasörler **ASP.NET MVC** ve **ASP.NET Web API** bileşenleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d635e-172">**Controllers** and **Views**: These folders are required for the **ASP.NET MVC** and **ASP.NET Web API** components.</span></span> <span data-ttu-id="d635e-173">MVC ve Web API teknolojilerini bir sonraki alıştırmada keşfedecektir.</span><span class="sxs-lookup"><span data-stu-id="d635e-173">You will explore the MVC and Web API technologies in the next exercises.</span></span>
    4. <span data-ttu-id="d635e-174">**Default. aspx**, **Contact. aspx** ve **About. aspx** dosyaları, uygulamanıza özgü sayfaları oluşturmak için başlangıç noktaları olarak kullanabileceğiniz önceden tanımlanmış Web formu sayfalarıdır.</span><span class="sxs-lookup"><span data-stu-id="d635e-174">The **Default.aspx**, **Contact.aspx** and **About.aspx** files are pre-defined Web Form pages that you can use as starting points to build the pages specific to your application.</span></span> <span data-ttu-id="d635e-175">Bu dosyaların programlama mantığı, bir &quot;. aspx. vb&quot; veya &quot;. aspx.cs&quot; uzantısına (kullanılan dile bağlı olarak) sahip &quot;arka plan kod&quot; dosyası olarak adlandırılan ayrı bir dosyada yer alır.</span><span class="sxs-lookup"><span data-stu-id="d635e-175">The programming logic of those files resides in a separate file referred to as the &quot;code-behind&quot; file, which has an &quot;.aspx.vb&quot; or &quot;.aspx.cs&quot; extension (depending on the language used).</span></span> <span data-ttu-id="d635e-176">Arka plan kod mantığı sunucuda çalışır ve sayfanız için HTML çıktısını dinamik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d635e-176">The code-behind logic runs on the server and dynamically produces the HTML output for your page.</span></span>
    5. <span data-ttu-id="d635e-177">**Site. Master** ve **site. Mobile. Master** sayfaları, uygulamadaki tüm sayfaların görünüm ve yapısını ve standart davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d635e-177">The **Site.Master** and **Site.Mobile.Master** pages define the look and feel and the standard behavior of all the pages in the application.</span></span>
5. <span data-ttu-id="d635e-178">Sayfanın içeriğini araştırmak için **default. aspx** dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-178">Double-click the **Default.aspx** file to explore the content of the page.</span></span>

    ![Default. aspx sayfasını keşfetme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    <span data-ttu-id="d635e-180">*Default. aspx sayfasını keşfetme*</span><span class="sxs-lookup"><span data-stu-id="d635e-180">*Exploring the Default.aspx page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d635e-181">Dosyanın en üstündeki **sayfa** yönergesi Web Forms sayfasının özniteliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d635e-181">The **Page** directive at the top of the file defines the attributes of the Web Forms page.</span></span> <span data-ttu-id="d635e-182">Örneğin, **MasterPageFile** özniteliği ana sayfanın yolunu belirtir-bu durumda, *site. Master* sayfası ve **Inherits** özniteliği, sayfanın devralması için arka plan kod sınıfını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d635e-182">For example, the **MasterPageFile** attribute specifies the path to the master page -in this case, the *Site.Master* page- and the **Inherits** attribute defines the code-behind class for the page to inherit.</span></span> <span data-ttu-id="d635e-183">Bu sınıf, **codebehind** özniteliği tarafından belirlenen dosyada bulunur.</span><span class="sxs-lookup"><span data-stu-id="d635e-183">This class is located in the file determined by the **CodeBehind** attribute.</span></span>
    > 
    > <span data-ttu-id="d635e-184">**ASP: Content** Control, sayfanın gerçek içeriğini (metin, biçimlendirme ve denetimler) tutar ve ana sayfada bir **ASP: ContentPlaceHolder** denetimiyle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="d635e-184">The **asp:Content** control holds the actual content of the page (text, markup and controls) and is mapped to a **asp:ContentPlaceHolder** control on the master page.</span></span> <span data-ttu-id="d635e-185">Bu durumda, sayfa içeriği *site. Master* sayfasında tanımlanan *mainContent* denetimi içinde işlenir.</span><span class="sxs-lookup"><span data-stu-id="d635e-185">In this case, the page content will be rendered inside the *MainContent* control defined in the *Site.Master* page.</span></span>
6. <span data-ttu-id="d635e-186">**Uygulama\_Başlat** klasörünü genişletin ve **WebApiConfig.cs** dosyasına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d635e-186">Expand the **App\_Start** folder and notice the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="d635e-187">Visual Studio, projenizi bir ASP.NET şablonuyla yapılandırırken Web API 'SI eklemiş olduğunuzdan, bu dosyayı oluşturulan çözümde içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="d635e-187">Visual Studio included that file in the generated solution because you included Web API when configuring your project with the One ASP.NET template.</span></span>
7. <span data-ttu-id="d635e-188">**WebApiConfig.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d635e-188">Open the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="d635e-189">*WebApiConfig* SıNıFıNDA, http YOLLARıNı **Web API DENETLEYICILERIYLE**eşleyen Web API 'siyle ilişkili yapılandırmayı bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-189">In the *WebApiConfig* class you will find the configuration associated with Web API, which maps HTTP routes to **Web API controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. <span data-ttu-id="d635e-190">**RouteConfig.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d635e-190">Open the **RouteConfig.cs** file.</span></span> <span data-ttu-id="d635e-191">*RegisterRoutes* yönteminin IÇINDE, http yollarını **MVC denetleyicileriyle**eşleyen MVC ile ilişkili yapılandırmayı bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-191">Inside the *RegisterRoutes* method you will find the configuration associated with MVC, which maps HTTP routes to **MVC controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="d635e-192">Görev 2 – çözümü çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d635e-192">Task 2 – Running the Solution</span></span>

<span data-ttu-id="d635e-193">Bu görevde, oluşturulan çözümü çalıştıracak, uygulamanın URL yeniden yazma ve yerleşik kimlik doğrulama gibi bazı özelliklerini keşfedecektir.</span><span class="sxs-lookup"><span data-stu-id="d635e-193">In this task you will run the generated solution, explore the app and some of its features, like URL rewriting and built-in authentication.</span></span>

1. <span data-ttu-id="d635e-194">Çözümü çalıştırmak için **F5** tuşuna basın veya araç çubuğunda bulunan **Başlat** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-194">To run the solution, press **F5** or click the **Start** button located on the toolbar.</span></span> <span data-ttu-id="d635e-195">Uygulama giriş sayfası tarayıcıda açılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d635e-195">The application home page should open in the browser.</span></span>

    ![Çözümü çalıştırma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. <span data-ttu-id="d635e-197">Web Forms sayfalarının çağrıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d635e-197">Verify that the Web Forms pages are being invoked.</span></span> <span data-ttu-id="d635e-198">Bunu yapmak için, adres çubuğundaki URL 'ye **/Contact.aspx** ekleyin ve **ENTER**'a basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-198">To do this, append **/contact.aspx** to the URL in the address bar and press **Enter**.</span></span>

    ![Kolay URL’ler](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    <span data-ttu-id="d635e-200">*Kolay URL 'Ler*</span><span class="sxs-lookup"><span data-stu-id="d635e-200">*Friendly URLs*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d635e-201">Gördüğünüz gibi URL, **/Contact**olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="d635e-201">As you can see, the URL changes to **/contact**.</span></span> <span data-ttu-id="d635e-202">**ASP.NET 4**' ten başlayarak, URL yönlendirme özellikleri Web Forms eklendi, bu nedenle *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* yerine *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* gibi URL 'leri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-202">Starting from **ASP.NET 4**, URL routing capabilities were added to Web Forms, so you can write URLs like *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* instead of *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span></span> <span data-ttu-id="d635e-203">Daha fazla bilgi için [URL yönlendirmeye](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="d635e-203">For more information refer to [URL Routing](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span></span>
3. <span data-ttu-id="d635e-204">Artık uygulamayla tümleştirilmiş kimlik doğrulama akışını araştıracaktır.</span><span class="sxs-lookup"><span data-stu-id="d635e-204">You will now explore the authentication flow integrated into the application.</span></span> <span data-ttu-id="d635e-205">Bunu yapmak için sayfanın sağ üst köşesindeki **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-205">To do this, click **Register** in the upper-right corner of the page.</span></span>

    ![Yeni Kullanıcı kaydetme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    <span data-ttu-id="d635e-207">*Yeni Kullanıcı kaydetme*</span><span class="sxs-lookup"><span data-stu-id="d635e-207">*Registering a new user*</span></span>
4. <span data-ttu-id="d635e-208">**Kaydet** sayfasında, bir **Kullanıcı adı** ve **parola**girin ve ardından **Kaydet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-208">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    ![Kayıt sayfası](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    <span data-ttu-id="d635e-210">*Kayıt sayfası*</span><span class="sxs-lookup"><span data-stu-id="d635e-210">*Register page*</span></span>
5. <span data-ttu-id="d635e-211">Uygulama yeni hesabı kaydeder ve kullanıcının kimliği doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="d635e-211">The application registers the new account, and the user is authenticated.</span></span>

    ![Kullanıcının kimliği doğrulandı](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    <span data-ttu-id="d635e-213">*Kullanıcının kimliği doğrulandı*</span><span class="sxs-lookup"><span data-stu-id="d635e-213">*User authenticated*</span></span>
6. <span data-ttu-id="d635e-214">Visual Studio 'ya geri dönün ve hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-214">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a><span data-ttu-id="d635e-215">Alıştırma 2: yapı Iskelesi kullanarak MVC denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-215">Exercise 2: Creating an MVC Controller Using Scaffolding</span></span>

<span data-ttu-id="d635e-216">Bu alıştırmada, tek bir kod satırı yazmadan CRUD işlemleri gerçekleştirmeye yönelik eylemlerle ve Razor görünümleriyle ASP.NET MVC 5 denetleyicisi oluşturmak için Visual Studio tarafından sunulan ASP.NET Scafkatlama çerçevesinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-216">In this exercise you will take advantage of the ASP.NET Scaffolding framework provided by Visual Studio to create an ASP.NET MVC 5 controller with actions and Razor views to perform CRUD operations, without writing a single line of code.</span></span> <span data-ttu-id="d635e-217">Yapı iskelesi işlemi, SQL veritabanında veri bağlamını ve veritabanı şemasını oluşturmak için Entity Framework Code First kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="d635e-217">The scaffolding process will use Entity Framework Code First to generate the data context and the database schema in the SQL database.</span></span>

<span data-ttu-id="d635e-218">**Entity Framework Code First hakkında**</span><span class="sxs-lookup"><span data-stu-id="d635e-218">**About Entity Framework Code First**</span></span>

<span data-ttu-id="d635e-219">Entity Framework (EF), ilişkisel bir depolama şemasını kullanarak doğrudan programlama yerine kavramsal bir uygulama modeliyle programlama yoluyla veri erişimi uygulamaları oluşturmanıza olanak sağlayan bir nesne ilişkisel Eşleyici 'dir (ORM).</span><span class="sxs-lookup"><span data-stu-id="d635e-219">Entity Framework (EF) is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span>

<span data-ttu-id="d635e-220">Entity Framework Code First modelleme iş akışı, sorgu, değişiklik izleme ve güncelleştirme işlevlerini gerçekleştirirken EF 'in kullandığı modeli göstermek için kendi etki alanı sınıflarınızı kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d635e-220">The Entity Framework Code First modeling workflow allows you to use your own domain classes to represent the model that EF relies on when performing querying, change-tracking and updating functions.</span></span> <span data-ttu-id="d635e-221">Code First geliştirme iş akışını kullanarak, bir veritabanı oluşturarak veya bir şema belirterek uygulamanıza başlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d635e-221">Using the Code First development workflow, you do not need to begin your application by creating a database or specifying a schema.</span></span> <span data-ttu-id="d635e-222">Bunun yerine, uygulamanız için en uygun etki alanı modeli nesnelerini tanımlayan standart .NET sınıfları yazabilir ve Entity Framework veritabanı sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d635e-222">Instead, you can write standard .NET classes that define the most appropriate domain model objects for your application, and Entity Framework will create the database for you.</span></span>

> [!NOTE]
> <span data-ttu-id="d635e-223">[Buradan](../../../entity-framework.md)Entity Framework hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-223">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a><span data-ttu-id="d635e-224">Görev 1 – yeni model oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-224">Task 1 – Creating a New Model</span></span>

<span data-ttu-id="d635e-225">Artık, MVC denetleyicisi ve görünümleri oluşturmak için yapı iskelesi işlemi tarafından kullanılan model olacak bir **kişi** sınıfı tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-225">You will now define a **Person** class, which will be the model used by the scaffolding process to create the MVC controller and the views.</span></span> <span data-ttu-id="d635e-226">Bir **kişi** modeli sınıfı oluşturarak başlayacaksınız ve DENETLEYICIDEKI CRUD işlemleri, yapı iskelesi özellikleri kullanılarak otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d635e-226">You will start by creating a **Person** model class, and the CRUD operations in the controller will be automatically created using scaffolding features.</span></span>

1. <span data-ttu-id="d635e-227">**Web için Visual Studio Express 2013** ve **kaynak/EX2-Mvcscafkat/başlangıç** klasöründe bulunan **myhybridsite. sln** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="d635e-227">Open **Visual Studio Express 2013 for Web** and the **MyHybridSite.sln** solution located in the **Source/Ex2-MvcScaffolding/Begin** folder.</span></span> <span data-ttu-id="d635e-228">Alternatif olarak, önceki alıştırmada elde ettiğiniz çözüme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-228">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="d635e-229">**Çözüm Gezgini**, **Myhybridsite** projesinin **modeller** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Sınıf.** ...</span><span class="sxs-lookup"><span data-stu-id="d635e-229">In **Solution Explorer**, right-click the **Models** folder of the **MyHybridSite** project and select **Add | Class...**.</span></span>

    ![Kişi modeli sınıfı ekleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    <span data-ttu-id="d635e-231">*Kişi modeli sınıfı ekleme*</span><span class="sxs-lookup"><span data-stu-id="d635e-231">*Adding the Person model class*</span></span>
3. <span data-ttu-id="d635e-232">**Yeni öğe Ekle** iletişim kutusunda dosyayı *Person.cs* olarak adlandırın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-232">In the **Add New Item** dialog box, name the file *Person.cs* and click **Add**.</span></span>

    ![Kişi modeli sınıfı oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    <span data-ttu-id="d635e-234">*Kişi modeli sınıfı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d635e-234">*Creating the Person model class*</span></span>
4. <span data-ttu-id="d635e-235">**Person.cs** dosyasının içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d635e-235">Replace the content of the **Person.cs** file with the following code.</span></span> <span data-ttu-id="d635e-236">Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-236">Press **CTRL + S** to save the changes.</span></span>

    <span data-ttu-id="d635e-237">(Kod parçacığı- *BringingTogetherOneAspNet-EX2-PersonClass*)</span><span class="sxs-lookup"><span data-stu-id="d635e-237">(Code Snippet - *BringingTogetherOneAspNet - Ex2 - PersonClass*)</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. <span data-ttu-id="d635e-238">**Çözüm Gezgini**, **Myhybridsite** projesine sağ tıklayın ve **Oluştur**' u seçin ya da projeyi derlemek için **CTRL + SHIFT + B** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-238">In **Solution Explorer**, right-click the **MyHybridSite** project and select **Build**, or press **CTRL + SHIFT + B** to build the project.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a><span data-ttu-id="d635e-239">Görev 2 – MVC denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-239">Task 2 – Creating an MVC Controller</span></span>

<span data-ttu-id="d635e-240">Artık **kişi** modeli oluşturduğumuzdan, **kışı**için CRUD denetleyicisi eylemlerini ve görünümlerini oluşturmak üzere Entity Framework ile ASP.NET MVC scafkatlaması kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-240">Now that the **Person** model is created, you will use ASP.NET MVC scaffolding with Entity Framework to create the CRUD controller actions and views for **Person**.</span></span>

1. <span data-ttu-id="d635e-241">**Çözüm Gezgini**, **Myhybridsite** projesinin **denetleyiciler** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Yeni yapı Iskelesi öğesi...** .</span><span class="sxs-lookup"><span data-stu-id="d635e-241">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![Yeni bir scafkatlanmış denetleyici oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    <span data-ttu-id="d635e-243">*Yeni bir Scafkatlanmış denetleyici oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d635e-243">*Creating a new Scaffolded Controller*</span></span>
2. <span data-ttu-id="d635e-244">**Yapı Iskelesi Ekle** iletişim kutusunda, **Entity Framework kullanarak, görünümler Içeren MVC 5 denetleyici '** yi seçin ve ardından Ekle ' ye tıklayın **.**</span><span class="sxs-lookup"><span data-stu-id="d635e-244">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework** and then click **Add.**</span></span>

    ![Görünümler ve Entity Framework MVC 5 denetleyicisi seçiliyor](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    <span data-ttu-id="d635e-246">*Görünümler ve Entity Framework MVC 5 denetleyicisi seçiliyor*</span><span class="sxs-lookup"><span data-stu-id="d635e-246">*Selecting MVC 5 Controller with views and Entity Framework*</span></span>
3. <span data-ttu-id="d635e-247">*Mvcpersoncontroller* 'ı **Denetleyici adı**olarak ayarlayın, **zaman uyumsuz denetleyici eylemleri kullan** seçeneğini belirleyin ve **model sınıfı**olarak **Person (myhybridsite. modeller)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d635e-247">Set *MvcPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** as the **Model class**.</span></span>

    ![Yapı iskelesi ile MVC denetleyicisi ekleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    <span data-ttu-id="d635e-249">*Yapı iskelesi ile MVC denetleyicisi ekleme*</span><span class="sxs-lookup"><span data-stu-id="d635e-249">*Adding an MVC controller with scaffolding*</span></span>
4. <span data-ttu-id="d635e-250">**Veri bağlamı sınıfı**altında **Yeni veri bağlamı...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-250">Under **Data context class**, click **New data context...**.</span></span>

    ![Yeni bir veri bağlamı oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    <span data-ttu-id="d635e-252">*Yeni bir veri bağlamı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d635e-252">*Creating a new data context*</span></span>
5. <span data-ttu-id="d635e-253">**Yeni veri bağlamı** iletişim kutusunda yeni veri *bağlamı ' nı adlandırın ve* **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-253">In the **New Data Context** dialog box, name the new data context *PersonContext* and click **Add**.</span></span>

    ![Yeni Personbu bağlamı oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    <span data-ttu-id="d635e-255">*Yeni Personya bağlamı türü oluşturuluyor*</span><span class="sxs-lookup"><span data-stu-id="d635e-255">*Creating the new PersonContext type*</span></span>
6. <span data-ttu-id="d635e-256">Yeni denetleyiciyi yapı iskelesi içeren bir **kişiye** oluşturmak için **Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-256">Click **Add** to create the new controller for **Person** with scaffolding.</span></span> <span data-ttu-id="d635e-257">Daha sonra, Visual Studio denetleyici eylemlerini, kişi veri bağlamını ve Razor görünümlerini oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="d635e-257">Visual Studio will then generate the controller actions, the Person data context and the Razor views.</span></span>

    ![Yapı iskelesi ile MVC denetleyicisi oluşturduktan sonra](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    <span data-ttu-id="d635e-259">*Yapı iskelesi ile MVC denetleyicisi oluşturduktan sonra*</span><span class="sxs-lookup"><span data-stu-id="d635e-259">*After creating the MVC controller with scaffolding*</span></span>
7. <span data-ttu-id="d635e-260">**MvcPersonController.cs** dosyasını **denetleyiciler** klasöründe açın.</span><span class="sxs-lookup"><span data-stu-id="d635e-260">Open the **MvcPersonController.cs** file in the **Controllers** folder.</span></span> <span data-ttu-id="d635e-261">CRUD eylem yöntemlerinin otomatik olarak oluşturulduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d635e-261">Notice that the CRUD action methods have been generated automatically.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > <span data-ttu-id="d635e-262">Önceki adımlarda bulunan scafkatlama seçeneklerinde **zaman uyumsuz denetleyici eylemleri kullan** onay kutusunu seçerek, Visual Studio kişi veri bağlamına erişimi olan tüm eylemler için zaman uyumsuz eylem yöntemleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d635e-262">By selecting the **Use async controller actions** check box from the scaffolding options in the previous steps, Visual Studio generates asynchronous action methods for all actions that involve access to the Person data context.</span></span> <span data-ttu-id="d635e-263">İstek işlenirken Web sunucusunun iş gerçekleştirmesini engellemeyi önlemek için uzun süre çalışan, CPU olmayan istekler için zaman uyumsuz eylem yöntemleri kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="d635e-263">It is recommended that you use asynchronous action methods for long-running, non-CPU bound requests to avoid blocking the Web server from performing work while the request is being processed.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="d635e-264">Görev 3 – çözümü çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d635e-264">Task 3 – Running the Solution</span></span>

<span data-ttu-id="d635e-265">Bu görevde, **kişi** görünümlerinin beklendiği gibi çalıştığını doğrulamak için çözümü yeniden çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-265">In this task, you will run the solution again to verify that the views for **Person** are working as expected.</span></span> <span data-ttu-id="d635e-266">Veritabanına başarıyla kaydedildiğini doğrulamak için yeni bir kişi ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-266">You will add a new person to verify that it is successfully saved to the database.</span></span>

1. <span data-ttu-id="d635e-267">Çözümü çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-267">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="d635e-268">**/Mvcperson**'a gidin.</span><span class="sxs-lookup"><span data-stu-id="d635e-268">Navigate to **/MvcPerson**.</span></span> <span data-ttu-id="d635e-269">Kişilerin listesini gösteren yapı iskelesi görünümü.</span><span class="sxs-lookup"><span data-stu-id="d635e-269">The scaffolded view that shows the list of people should appear.</span></span>
3. <span data-ttu-id="d635e-270">Yeni bir kişi eklemek için **Yeni oluştur** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-270">Click **Create New** to add a new person.</span></span>

    ![Scafkatlanmış MVC görünümlerine gitme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    <span data-ttu-id="d635e-272">*Scafkatlanmış MVC görünümlerine gitme*</span><span class="sxs-lookup"><span data-stu-id="d635e-272">*Navigating to the scaffolded MVC views*</span></span>
4. <span data-ttu-id="d635e-273">**Oluştur** görünümünde, kişi Için bir **ad** ve **yaş** girin ve **Oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-273">In the **Create** view, provide a **Name** and an **Age** for the person, and click **Create**.</span></span>

    ![Yeni bir kişi ekleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    <span data-ttu-id="d635e-275">*Yeni bir kişi ekleme*</span><span class="sxs-lookup"><span data-stu-id="d635e-275">*Adding a new person*</span></span>
5. <span data-ttu-id="d635e-276">Yeni kişi listeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="d635e-276">The new person is added to the list.</span></span> <span data-ttu-id="d635e-277">Öğe listesinde, **Ayrıntılar** ' a tıklayarak kişinin Ayrıntılar görünümünü görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="d635e-277">In the element list, click **Details** to display the person's details view.</span></span> <span data-ttu-id="d635e-278">Ardından, **Ayrıntılar** görünümünde liste görünümüne geri dönmek Için **listeye geri dön** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-278">Then, in the **Details** view, click **Back to List** to go back to the list view.</span></span>

    ![Kişinin Ayrıntılar görünümü](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    <span data-ttu-id="d635e-280">*Kişinin Ayrıntılar görünümü*</span><span class="sxs-lookup"><span data-stu-id="d635e-280">*Person's details view*</span></span>
6. <span data-ttu-id="d635e-281">Kişiyi silmek için **Sil** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-281">Click the **Delete** link to delete the person.</span></span> <span data-ttu-id="d635e-282">İşlemi doğrulamak için **Sil** görünümünde **Sil** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-282">In the **Delete** view, click **Delete** to confirm the operation.</span></span>

    ![Bir kişiyi silme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    <span data-ttu-id="d635e-284">*Bir kişiyi silme*</span><span class="sxs-lookup"><span data-stu-id="d635e-284">*Deleting a person*</span></span>
7. <span data-ttu-id="d635e-285">Visual Studio 'ya geri dönün ve hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a><span data-ttu-id="d635e-286">Alıştırma 3: yapı Iskelesi kullanarak Web API denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-286">Exercise 3: Creating a Web API Controller Using Scaffolding</span></span>

<span data-ttu-id="d635e-287">Web API çerçevesi, ASP.NET yığınının bir parçasıdır ve HTTP hizmetlerini uygulamayı daha kolay hale getirmek, genel olarak JSON veya XML biçimli veriler gönderip almak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d635e-287">The Web API framework is part of the ASP.NET Stack and designed to make implementing HTTP services easier, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span>

<span data-ttu-id="d635e-288">Bu alıştırmada, bir Web API denetleyicisi oluşturmak için ASP.NET Scafkatmayı yeniden kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-288">In this exercise, you will use ASP.NET Scaffolding again to generate a Web API controller.</span></span> <span data-ttu-id="d635e-289">Aynı kişi verilerini JSON biçiminde sağlamak için önceki alıştırmada aynı **kişiyi** ve **personcontext** sınıflarını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-289">You will use the same **Person** and **PersonContext** classes from the previous exercise to provide the same person data in JSON format.</span></span> <span data-ttu-id="d635e-290">Aynı kaynakları aynı ASP.NET uygulamasının farklı şekillerde nasıl kullanıma sunabileceğiniz hakkında bilgi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-290">You will see how you can expose the same resources in different ways within the same ASP.NET application.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a><span data-ttu-id="d635e-291">Görev 1 – Web API denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-291">Task 1 – Creating a Web API Controller</span></span>

<span data-ttu-id="d635e-292">Bu görevde, kişi verilerini JSON gibi makine tüketilebilir bir biçimde kullanıma sunmayacak yeni bir **Web API denetleyicisi** oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-292">In this task you will create a new **Web API Controller** that will expose the person data in a machine-consumable format like JSON.</span></span>

1. <span data-ttu-id="d635e-293">Zaten açık değilse, **Web için Visual Studio Express 2013** ' i açın ve **kaynak/Ex3-WebAPI/BEGIN** klasöründe bulunan **myhybridsite. sln** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="d635e-293">If not already opened, open **Visual Studio Express 2013 for Web** and open the **MyHybridSite.sln** solution located in the **Source/Ex3-WebAPI/Begin** folder.</span></span> <span data-ttu-id="d635e-294">Alternatif olarak, önceki alıştırmada elde ettiğiniz çözüme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-294">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d635e-295">Alıştırma 3 ' ten başla çözümüyle başlarsanız, çözümü derlemek için **CTRL + SHIFT + B** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-295">If you start with the Begin solution from Exercise 3, press **CTRL + SHIFT + B** to build the solution.</span></span>
2. <span data-ttu-id="d635e-296">**Çözüm Gezgini**, **Myhybridsite** projesinin **denetleyiciler** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Yeni yapı Iskelesi öğesi...** .</span><span class="sxs-lookup"><span data-stu-id="d635e-296">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![Yeni bir scafkatlanmış denetleyici oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    <span data-ttu-id="d635e-298">*Yeni bir scafkatlanmış denetleyici oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d635e-298">*Creating a new scaffolded Controller*</span></span>
3. <span data-ttu-id="d635e-299">**Yapı Iskelesi Ekle** iletişim kutusunda sol bölmedeki **Web API 'si** ' ni, sonra da **Eylemler ile Web API 2 denetleyicisi '** ni, orta bölmedeki Entity Framework kullanarak ve ardından Ekle ' yi seçin **.**</span><span class="sxs-lookup"><span data-stu-id="d635e-299">In the **Add Scaffold** dialog box, select **Web API** in the left pane, then **Web API 2 Controller with actions, using Entity Framework** in the middle pane and then click **Add.**</span></span>

    <span data-ttu-id="d635e-300">![Eylemler ve Entity Framework Web API 2 denetleyicisi seçme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Eylemler ve Entity Framework Web API 2 denetleyicisi seçme")</span><span class="sxs-lookup"><span data-stu-id="d635e-300">![Selecting Web API 2 Controller with actions and Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Selecting Web API 2 Controller with actions and Entity Framework")</span></span>

    <span data-ttu-id="d635e-301">*Eylemler ve Entity Framework Web API 2 denetleyicisi seçme*</span><span class="sxs-lookup"><span data-stu-id="d635e-301">*Selecting Web API 2 Controller with actions and Entity Framework*</span></span>
4. <span data-ttu-id="d635e-302">*Apipersoncontroller* 'ı **Denetleyici adı**olarak ayarlayın, **zaman uyumsuz denetleyici eylemleri kullan** seçeneğini belirleyin ve sırasıyla **model** ve **veri bağlamı** sınıfları olarak **Person (MyHybridSite. modeller** ) ve **personcontext (myhybridsite. modeller)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d635e-302">Set *ApiPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** and **PersonContext (MyHybridSite.Models)** as the **Model** and **Data context** classes respectively.</span></span> <span data-ttu-id="d635e-303">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-303">Then click **Add**.</span></span>

    <span data-ttu-id="d635e-304">![Yapı iskelesi ile Web API denetleyicisi ekleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Yapı iskelesi ile Web API denetleyicisi ekleme")</span><span class="sxs-lookup"><span data-stu-id="d635e-304">![Adding a Web API Controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Adding a Web API controller with scaffolding")</span></span>

    <span data-ttu-id="d635e-305">*Yapı iskelesi ile Web API denetleyicisi ekleme*</span><span class="sxs-lookup"><span data-stu-id="d635e-305">*Adding a Web API controller with scaffolding*</span></span>
5. <span data-ttu-id="d635e-306">Daha sonra Visual Studio, verileriniz ile çalışmak için dört CRUD eylemleriyle **Apipersoncontroller** sınıfını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d635e-306">Visual Studio will then generate the **ApiPersonController** class with the four CRUD actions to work with your data.</span></span>

    <span data-ttu-id="d635e-307">![Web API denetleyicisini yapı iskelesi ile oluşturduktan sonra](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "Web API denetleyicisini yapı iskelesi ile oluşturduktan sonra")</span><span class="sxs-lookup"><span data-stu-id="d635e-307">![After creating the Web API controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "After creating the Web API controller with scaffolding")</span></span>

    <span data-ttu-id="d635e-308">*Web API denetleyicisini yapı iskelesi ile oluşturduktan sonra*</span><span class="sxs-lookup"><span data-stu-id="d635e-308">*After creating the Web API controller with scaffolding*</span></span>
6. <span data-ttu-id="d635e-309">**ApiPersonController.cs** dosyasını açın ve *getkişiler* eylem yöntemini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="d635e-309">Open the **ApiPersonController.cs** file and inspect the *GetPeople* action method.</span></span> <span data-ttu-id="d635e-310">Bu yöntem, kişi verilerini almak için **Personcontext** türünün DB alanını sorgular.</span><span class="sxs-lookup"><span data-stu-id="d635e-310">This method queries the db field of **PersonContext** type in order to get the people data.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. <span data-ttu-id="d635e-311">Şimdi yöntem tanımının üzerindeki açıklamaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d635e-311">Now notice the comment above the method definition.</span></span> <span data-ttu-id="d635e-312">Bir sonraki görevde kullanacağınız bu eylemi sunan URI 'yi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d635e-312">It provides the URI that exposes this action which you will use in the next task.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="d635e-313">Varsayılan olarak, Web API 'si, MVC denetleyicileriyle çakışmaları önlemek için */API* yoluna sorguları yakalamak üzere yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d635e-313">By default, Web API is configured to catch the queries to the */api* path to avoid collisions with MVC controllers.</span></span> <span data-ttu-id="d635e-314">Bu ayarı değiştirmeniz gerekiyorsa, [ASP.NET Web API 'de yönlendirme](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)' ye başvurun.</span><span class="sxs-lookup"><span data-stu-id="d635e-314">If you need to change this setting, refer to [Routing in ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="d635e-315">Görev 2 – çözümü çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d635e-315">Task 2 – Running the Solution</span></span>

<span data-ttu-id="d635e-316">Bu görevde, Web API denetleyicisinden tam yanıtı incelemek için Internet Explorer **F12 geliştirici araçları** ' nı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-316">In this task you will use the Internet Explorer **F12 developer tools** to inspect the full response from the Web API controller.</span></span> <span data-ttu-id="d635e-317">Uygulama verilerinize ilişkin daha fazla bilgi almak için ağ trafiğini nasıl yakalayabileceğiniz hakkında bilgi alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-317">You will see how you can capture network traffic to get more insight into your application data.</span></span>

> [!NOTE]
> <span data-ttu-id="d635e-318">Visual Studio araç çubuğunda bulunan **Başlat** düğmesinde **Internet Explorer** 'ın seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d635e-318">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer seçeneği](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> <span data-ttu-id="d635e-320">**F12 geliştirici araçları** , bu uygulamalı laboratuvarda kapsanmayan geniş bir işlevsellik kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d635e-320">The **F12 developer tools** have a wide set of functionality that is not covered in this hands-on-lab.</span></span> <span data-ttu-id="d635e-321">Hakkında daha fazla bilgi edinmek istiyorsanız, [F12 geliştirici araçlarını kullanma](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="d635e-321">If you want to learn more about it, refer to [Using the F12 developer tools](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span></span>

1. <span data-ttu-id="d635e-322">Çözümü çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-322">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d635e-323">Bu görevi doğru bir şekilde takip edebilmek için uygulamanızın verileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d635e-323">In order to follow this task correctly, your application needs to have data.</span></span> <span data-ttu-id="d635e-324">Veritabanınız boşsa, çalışma 2 ' de görev 3 ' e geri dönerek MVC görünümlerini kullanarak yeni bir kişi oluşturma hakkındaki adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-324">If your database is empty, you can go back to Task 3 in Exercise 2 and follow the steps on how to create a new person using the MVC views.</span></span>
2. <span data-ttu-id="d635e-325">Tarayıcıda, **Geliştirici Araçları** panelini açmak için **F12** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-325">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="d635e-326">**CTRL** + **4** ' e basın veya **ağ** simgesine tıklayın ve sonra ağ trafiğini yakalamaya başlamak için yeşil ok düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-326">Press **CTRL** + **4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="d635e-327">![Web API ağı yakalama başlatılıyor](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API ağı yakalama başlatılıyor")</span><span class="sxs-lookup"><span data-stu-id="d635e-327">![Initiating Web API network capture](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="d635e-328">*Web API ağı yakalama başlatılıyor*</span><span class="sxs-lookup"><span data-stu-id="d635e-328">*Initiating Web API network capture*</span></span>
3. <span data-ttu-id="d635e-329">Tarayıcı adres çubuğundaki URL 'ye **API/ApiPerson** ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d635e-329">Append **api/ApiPerson** to the URL in the browser's address bar.</span></span> <span data-ttu-id="d635e-330">Şimdi **Apipersoncontroller**'dan Yanıtın ayrıntılarını inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-330">You will now inspect the details of the response from the **ApiPersonController**.</span></span>

    <span data-ttu-id="d635e-331">![Web API aracılığıyla kişi verilerini alma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Web API aracılığıyla kişi verilerini alma")</span><span class="sxs-lookup"><span data-stu-id="d635e-331">![Retrieving person data through Web API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Retrieving person data through Web API")</span></span>

    <span data-ttu-id="d635e-332">*Web API aracılığıyla kişi verilerini alma*</span><span class="sxs-lookup"><span data-stu-id="d635e-332">*Retrieving person data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d635e-333">İndirme işlemi tamamlandıktan sonra indirilen dosyayla bir eylem yapmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="d635e-333">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="d635e-334">Geliştirici araç penceresi aracılığıyla yanıt içeriğini izleyebilmek için iletişim kutusunu açık bırakın.</span><span class="sxs-lookup"><span data-stu-id="d635e-334">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
4. <span data-ttu-id="d635e-335">Şimdi yanıtın gövdesini inceleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-335">Now you will inspect the body of the response.</span></span> <span data-ttu-id="d635e-336">Bunu yapmak için **Ayrıntılar** sekmesine tıklayın ve ardından **yanıt gövdesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-336">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="d635e-337">İndirilen verilerin, **kişi** sınıfına karşılık gelen özellik **kimliği**, **ad** ve **yaşa** sahip bir nesne listesi olup olmadığını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-337">You can check that the downloaded data is a list of objects with the properties **Id**, **Name** and **Age** that correspond to the **Person** class.</span></span>

    <span data-ttu-id="d635e-338">![Web API yanıt gövdesini görüntüleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Web API yanıt gövdesini görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="d635e-338">![Viewing Web API Response Body](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Viewing Web API Response Body")</span></span>

    <span data-ttu-id="d635e-339">*Web API yanıt gövdesini görüntüleme*</span><span class="sxs-lookup"><span data-stu-id="d635e-339">*Viewing Web API Response Body*</span></span>

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a><span data-ttu-id="d635e-340">Görev 3 – Web API Yardım sayfaları ekleme</span><span class="sxs-lookup"><span data-stu-id="d635e-340">Task 3 – Adding Web API Help Pages</span></span>

<span data-ttu-id="d635e-341">Bir Web API 'SI oluşturduğunuzda, diğer geliştiricilerin API 'nizi nasıl çağırabileceğini bilmesi için bir yardım sayfası oluşturmak yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d635e-341">When you create a Web API, it is useful to create a help page so that other developers will know how to call your API.</span></span> <span data-ttu-id="d635e-342">Belge sayfalarını el ile oluşturup güncelleştirebilirsiniz, ancak bakım işleri yapmak zorunda kalmamak için bunları otomatik oluşturmak daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="d635e-342">You could create and update the documentation pages manually, but it is better to auto-generate them to avoid having to do maintenance work.</span></span> <span data-ttu-id="d635e-343">Bu görevde, çözüme otomatik olarak Web API Yardım sayfaları oluşturmak için bir NuGet paketi kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d635e-343">In this task you will use a Nuget package to automatically generate Web API help pages to the solution.</span></span>

1. <span data-ttu-id="d635e-344">Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-344">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="d635e-345">**Paket Yöneticisi konsolu** penceresinde aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="d635e-345">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > <span data-ttu-id="d635e-346">**Microsoft. Aspnet. WebApi. helppage** paketi gerekli derlemeleri yüklüyor ve **Areas/helppage** klasörü altındakı yardım sayfaları için MVC görünümleri ekliyor.</span><span class="sxs-lookup"><span data-stu-id="d635e-346">The **Microsoft.AspNet.WebApi.HelpPage** package installs the necessary assemblies and adds MVC Views for the help pages under the **Areas/HelpPage** folder.</span></span>

    <span data-ttu-id="d635e-347">![HelpPage alanı](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage alanı")</span><span class="sxs-lookup"><span data-stu-id="d635e-347">![HelpPage Area](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage Area")</span></span>

    <span data-ttu-id="d635e-348">*HelpPage alanı*</span><span class="sxs-lookup"><span data-stu-id="d635e-348">*HelpPage Area*</span></span>
3. <span data-ttu-id="d635e-349">Varsayılan olarak, yardım sayfalarında belgeler için yer tutucu dizeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="d635e-349">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="d635e-350">Belgeleri oluşturmak için XML belge açıklamalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d635e-350">You can use XML documentation comments to create the documentation.</span></span> <span data-ttu-id="d635e-351">Bu özelliği etkinleştirmek için, **Areas/yardım sayfası/uygulama\_başlangıç** klasöründe bulunan **HelpPageConfig.cs** dosyasını açın ve aşağıdaki satırın açıklamasını kaldırın:</span><span class="sxs-lookup"><span data-stu-id="d635e-351">To enable this feature, open the **HelpPageConfig.cs** file located in the **Areas/HelpPage/App\_Start** folder and uncomment the following line:</span></span>

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. <span data-ttu-id="d635e-352">**Çözüm Gezgini**, **Myhybridsite**projesine sağ tıklayın, **Özellikler** ' i seçin ve **derleme** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-352">In **Solution Explorer**, right-click the project **MyHybridSite**, select **Properties** and click the **Build** tab.</span></span>

    <span data-ttu-id="d635e-353">![Derleme sekmesi](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Derleme bölümü")</span><span class="sxs-lookup"><span data-stu-id="d635e-353">![Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Build section")</span></span>

    <span data-ttu-id="d635e-354">*Derleme sekmesi*</span><span class="sxs-lookup"><span data-stu-id="d635e-354">*Build tab*</span></span>
5. <span data-ttu-id="d635e-355">**Çıkış**' ın altında, **XML belge dosyası**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="d635e-355">Under **Output**, select **XML documentation file**.</span></span> <span data-ttu-id="d635e-356">Düzenle kutusunda **App\_Data/XmlDocument. xml**yazın.</span><span class="sxs-lookup"><span data-stu-id="d635e-356">In the edit box, type **App\_Data/XmlDocument.xml**.</span></span>

    <span data-ttu-id="d635e-357">![Derleme sekmesindeki çıkış bölümü](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Derleme sekmesindeki çıkış bölümü")</span><span class="sxs-lookup"><span data-stu-id="d635e-357">![Output section in Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Output section in build tab")</span></span>

    <span data-ttu-id="d635e-358">*Derleme sekmesindeki çıkış bölümü*</span><span class="sxs-lookup"><span data-stu-id="d635e-358">*Output section in Build tab*</span></span>
6. <span data-ttu-id="d635e-359">Değişiklikleri kaydetmek için **CTRL** + **S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-359">Press **CTRL** + **S** to save the changes.</span></span>
7. <span data-ttu-id="d635e-360">**ApiPersonController.cs** dosyasını **denetleyiciler** klasöründen açın.</span><span class="sxs-lookup"><span data-stu-id="d635e-360">Open the **ApiPersonController.cs** file from the **Controllers** folder.</span></span>
8. <span data-ttu-id="d635e-361">*GetPerson* yöntemi imzası ile *//Al API/apiperson* açıklaması arasına yeni bir satır girin ve ardından üç eğik çizgi yazın.</span><span class="sxs-lookup"><span data-stu-id="d635e-361">Enter a new line between the *GetPeople* method signature and the *// GET api/ApiPerson* comment, and then type three forward slashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d635e-362">Visual Studio, yöntem belgelerini tanımlayan XML öğelerini otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="d635e-362">Visual Studio automatically inserts the XML elements which define the method documentation.</span></span>
9. <span data-ttu-id="d635e-363">*Getkişilerim* yöntemi için bir Özet metni ve dönüş değeri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d635e-363">Add a summary text and the return value for the *GetPeople* method.</span></span> <span data-ttu-id="d635e-364">Aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="d635e-364">It should look like the following.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. <span data-ttu-id="d635e-365">Çözümü çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d635e-365">Press **F5** to run the solution.</span></span>
11. <span data-ttu-id="d635e-366">Yardım sayfasına gitmek için, adres çubuğundaki URL 'ye **/help** ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d635e-366">Append **/help** to the URL in the address bar to browse to the help page.</span></span>

    <span data-ttu-id="d635e-367">![ASP.NET Web API Yardım sayfası](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Yardım sayfası")</span><span class="sxs-lookup"><span data-stu-id="d635e-367">![ASP.NET Web API Help Page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Help Page")</span></span>

    <span data-ttu-id="d635e-368">*ASP.NET Web API Yardım sayfası*</span><span class="sxs-lookup"><span data-stu-id="d635e-368">*ASP.NET Web API Help Page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d635e-369">Sayfanın ana içeriği, denetleyiciye göre gruplandırılan bir API tablosudur.</span><span class="sxs-lookup"><span data-stu-id="d635e-369">The main content of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="d635e-370">Tablo girdileri, **IApiExplorer** arabirimi kullanılarak dinamik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d635e-370">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="d635e-371">Bir API denetleyicisi ekler veya güncelleştirirseniz, uygulamayı bir sonraki derişinizde tablo otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d635e-371">If you add or update an API controller, the table will be automatically updated the next time you build the application.</span></span>
    > 
    > <span data-ttu-id="d635e-372">API sütunu, HTTP yöntemini ve göreli URI **'yi** listeler.</span><span class="sxs-lookup"><span data-stu-id="d635e-372">The **API** column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="d635e-373">**Açıklama** sütunu, yöntemin belgelerinden ayıklanmış olan bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="d635e-373">The **Description** column contains information that has been extracted from the method's documentation.</span></span>
12. <span data-ttu-id="d635e-374">Yöntem tanımının üstüne eklediğiniz açıklamanın Açıklama sütununda görüntülendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-374">Note that the description you added above the method definition is displayed in the description column.</span></span>

    <span data-ttu-id="d635e-375">![API yöntemi açıklaması](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API yöntemi açıklaması")</span><span class="sxs-lookup"><span data-stu-id="d635e-375">![API method description](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API method description")</span></span>

    <span data-ttu-id="d635e-376">*API yöntemi açıklaması*</span><span class="sxs-lookup"><span data-stu-id="d635e-376">*API method description*</span></span>
13. <span data-ttu-id="d635e-377">Örnek yanıt gövdeleri dahil olmak üzere daha ayrıntılı bilgiler içeren bir sayfaya gitmek için API yöntemlerinden birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d635e-377">Click one of the API methods to navigate to a page with more detailed information, including sample response bodies.</span></span>

    <span data-ttu-id="d635e-378">![Ayrıntı bilgileri sayfası](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Ayrıntı bilgileri sayfası")</span><span class="sxs-lookup"><span data-stu-id="d635e-378">![Detail Information page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Detail Information page")</span></span>

    <span data-ttu-id="d635e-379">*Ayrıntılı bilgi sayfası*</span><span class="sxs-lookup"><span data-stu-id="d635e-379">*Detailed information page*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="d635e-380">Özet</span><span class="sxs-lookup"><span data-stu-id="d635e-380">Summary</span></span>

<span data-ttu-id="d635e-381">Bu uygulamalı Laboratuvarı tamamlayarak şu şekilde nasıl yapılacağını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="d635e-381">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="d635e-382">Visual Studio 2013 bir ASP.NET deneyimini kullanarak yeni bir Web uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="d635e-382">Create a new Web application using the One ASP.NET Experience in Visual Studio 2013</span></span>
- <span data-ttu-id="d635e-383">Birden çok ASP.NET teknolojilerini tek bir projede tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d635e-383">Integrate multiple ASP.NET technologies into one single project</span></span>
- <span data-ttu-id="d635e-384">ASP.NET Scafkatlaması kullanarak model sınıflarınızda MVC denetleyicileri ve görünümleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-384">Generate MVC controllers and views from your model classes using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="d635e-385">Entity Framework aracılığıyla zaman uyumsuz programlama ve veri erişimi gibi özellikleri kullanan Web API denetleyicileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="d635e-385">Generate Web API controllers, which use features such as Async Programming and data access through Entity Framework</span></span>
- <span data-ttu-id="d635e-386">Denetleyicileriniz için otomatik olarak Web API Yardım sayfaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="d635e-386">Automatically generate Web API Help Pages for your controllers</span></span>
