---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 'Uygulamalı laboratuvar: sürdürülebilir Azure Web siteleri: değişikliği ve ölçeği yönetme | Microsoft Docs'
author: rick-anderson
description: Bu laboratuvarda, Microsoft Azure Web sitelerini üretime derlemeyi ve dağıtmayı nasıl kolaylaştırdığını öğrenin.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624273"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="7be11-103">Uygulamalı Laboratuvar: Sürdürülebilir Azure Web Siteleri: Değişiklikleri ve Ölçeği Yönetme</span><span class="sxs-lookup"><span data-stu-id="7be11-103">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>

<span data-ttu-id="7be11-104">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="7be11-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="7be11-105">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="7be11-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="7be11-106">Microsoft Azure Web sitelerini üretime oluşturup dağıtmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="7be11-106">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="7be11-107">Ancak uygulamanız canlı olduğunda bu işlemi siz yapmanız yeterlidir!</span><span class="sxs-lookup"><span data-stu-id="7be11-107">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="7be11-108">Değiştirme gereksinimleri, veritabanı güncelleştirmeleri, ölçek ve daha fazlasını ele almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-108">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="7be11-109">Neyse ki, sitelerinizi sorunsuz bir şekilde çalışmaya devam etmenize yardımcı olacak çok sayıda özellik ile birlikte Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7be11-109">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
>
> <span data-ttu-id="7be11-110">Azure, her boyuttaki web uygulaması için güvenli ve esnek geliştirme, dağıtım ve ölçeklendirme seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="7be11-110">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="7be11-111">Altyapıyı yönetme zahmetsiz olmayan uygulamalar oluşturmak ve dağıtmak için mevcut araçlarınızdan yararlanın.</span><span class="sxs-lookup"><span data-stu-id="7be11-111">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
>
> <span data-ttu-id="7be11-112">En sevdiğiniz geliştirme aracını kullanarak oluşturulan içeriği kolayca dağıtarak bir üretim Web uygulamasını dakikalar içinde kendiniz sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-112">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="7be11-113">Var olan bir siteyi **Git**, **GitHub**, **Bitbucket**, **TFS**ve hatta **Dropbox**desteğiyle doğrudan kaynak denetiminden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-113">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="7be11-114">En sevdiğiniz IDE 'den veya Windows 'da **PowerShell** kullanarak veya HERHANGI bir işletim sisteminde çalışan **CLI** araçlarından doğrudan bir dağıtım yapın.</span><span class="sxs-lookup"><span data-stu-id="7be11-114">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="7be11-115">Dağıtıldıktan sonra, sürekli dağıtım desteğiyle sitelerinizi sürekli güncel tutun.</span><span class="sxs-lookup"><span data-stu-id="7be11-115">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
>
> <span data-ttu-id="7be11-116">Azure, büyük veya küçük tüm veriler için ölçeklenebilir, dayanıklı bulut depolama, yedekleme ve kurtarma çözümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7be11-116">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="7be11-117">Uygulamalar bir üretim ortamına dağıtıldığında, tablolar, Bloblar ve SQL veritabanları gibi depolama hizmetleri, uygulamanızı bulutta ölçeklendirmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7be11-117">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
>
> <span data-ttu-id="7be11-118">SQL veritabanları ile uygulamanızın yeni sürümlerini dağıttığınızda üretken veritabanınızı güncel tutmanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7be11-118">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="7be11-119">**Entity Framework Code First Migrations**teşekkür ederiz, veri modelinizin geliştirilmesi ve dağıtılması, ortamınızı dakikalar içinde güncelleştirmek üzere basitleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7be11-119">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="7be11-120">Bu uygulamalı laboratuvarda, Web uygulamanızı Microsoft Azure ' de üretim ortamlarına dağıttığınızda karşılaşabileceğiniz farklı konular gösterilecektir.</span><span class="sxs-lookup"><span data-stu-id="7be11-120">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
>
> <span data-ttu-id="7be11-121">Tüm örnek kod ve kod parçacıkları [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="7be11-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>
>
> <span data-ttu-id="7be11-122">Bu konuda daha ayrıntılı bilgi için bkz. [Azure e-kitabı Ile gerçek dünyada bulut uygulamaları oluşturma](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7be11-122">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="7be11-123">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="7be11-123">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="7be11-124">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="7be11-124">Objectives</span></span>

<span data-ttu-id="7be11-125">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="7be11-125">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="7be11-126">Mevcut bir modelle Entity Framework geçişleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="7be11-126">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="7be11-127">Nesne modelini ve veritabanını Entity Framework geçişleri kullanarak uygun şekilde güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7be11-127">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="7be11-128">Git kullanarak Azure App Service dağıtma</span><span class="sxs-lookup"><span data-stu-id="7be11-128">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="7be11-129">Azure yönetim portalı 'nı kullanarak önceki bir dağıtıma geri alma</span><span class="sxs-lookup"><span data-stu-id="7be11-129">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="7be11-130">Bir Web uygulamasını ölçeklendirmek için Azure Storage 'ı kullanma</span><span class="sxs-lookup"><span data-stu-id="7be11-130">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="7be11-131">Azure Yönetim Portalı kullanarak bir Web uygulaması için otomatik ölçeklendirmeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7be11-131">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="7be11-132">Visual Studio 'da bir yük testi projesi oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7be11-132">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="7be11-133">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7be11-133">Prerequisites</span></span>

<span data-ttu-id="7be11-134">Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="7be11-134">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="7be11-135">Web veya daha büyük [için Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="7be11-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="7be11-136">.NET 2,2 için Azure SDK</span><span class="sxs-lookup"><span data-stu-id="7be11-136">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="7be11-137">GIT sürüm denetimi sistemi</span><span class="sxs-lookup"><span data-stu-id="7be11-137">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="7be11-138">Microsoft Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="7be11-138">A Microsoft Azure subscription</span></span>

    - <span data-ttu-id="7be11-139">[Ücretsiz deneme](https://aka.ms/watk-freetrial) için kaydolun</span><span class="sxs-lookup"><span data-stu-id="7be11-139">Sign up for a [Free Trial](https://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="7be11-140">MSDN veya MSDN Platformları abonesine sahip bir Visual Studio Professional, Test Professional, Premium veya Ultimate kullanıyorsanız, Azure 'da geliştirme ve test etmeye başlamak için [MSDN avantajınızı](https://aka.ms/watk-msdn) şimdi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="7be11-140">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](https://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="7be11-141">[BizSpark](https://aka.ms/watk-bizspark) üyeleri Azure avantajını Visual Studio Ultimate with MSDN aboneliklerine göre otomatik olarak alır</span><span class="sxs-lookup"><span data-stu-id="7be11-141">[BizSpark](https://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="7be11-142">[Microsoft iş ortağı ağı](https://aka.ms/watk-mpn) Cloud Essentials programı üyeleri, aylık Azure kredilerini ücretsiz olarak alır</span><span class="sxs-lookup"><span data-stu-id="7be11-142">Members of the [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="7be11-143">Kurulum</span><span class="sxs-lookup"><span data-stu-id="7be11-143">Setup</span></span>

<span data-ttu-id="7be11-144">Bu uygulamalı laboratuvarda alýþtýrmalarý çalıştırmak için öncelikle ortamınızı ayarlamanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="7be11-144">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="7be11-145">Windows Gezgini 'ni açın ve laboratuvarın **kaynak** klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="7be11-145">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="7be11-146">Ortamınızı yapılandıracak ve bu laboratuvar için Visual Studio kod parçacıklarını yükleyecek kurulum işlemini başlatmak için **Setup. cmd** ' ye sağ tıklayın ve **yönetici olarak çalıştır** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-146">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="7be11-147">Kullanıcı hesabı denetimi iletişim kutusu gösteriliyorsa, devam etmek için eylemi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-147">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="7be11-148">Kurulumu çalıştırmadan önce bu laboratuvarın tüm bağımlılıklarını denetlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7be11-148">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="7be11-149">Kod parçacıklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="7be11-149">Using the Code Snippets</span></span>

<span data-ttu-id="7be11-150">Laboratuvar belgesi boyunca kod blokları eklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="7be11-150">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="7be11-151">Kolaylık olması için, bu kodun çoğu Visual Studio Code kod parçacığı olarak sağlanır ve bu, el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio 2013 içinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-151">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="7be11-152">Her alıştırma, her alıştırmanın bağımsız olarak her birini takip etmenizi sağlayan alıştırmanın **BEGIN** klasöründe bulunan bir başlangıç çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="7be11-152">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="7be11-153">Lütfen bir alıştırma sırasında eklenen kod parçacıklarının bu başlangıç çözümlerinde eksik olduğunu ve Alıştırmayı tamamlayana kadar çalışmadığının farkında olun.</span><span class="sxs-lookup"><span data-stu-id="7be11-153">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="7be11-154">Bir alıştırmada kaynak kodun içinde, ilgili alıştırmada adımların tamamlanmasına neden olan koda sahip bir Visual Studio çözümü içeren bir **son** klasör de bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-154">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="7be11-155">Bu uygulamalı laboratuvarda çalışırken daha fazla yardıma ihtiyacınız varsa bu çözümleri kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-155">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="7be11-156">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="7be11-156">Exercises</span></span>

<span data-ttu-id="7be11-157">Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:</span><span class="sxs-lookup"><span data-stu-id="7be11-157">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="7be11-158">Entity Framework geçişleri kullanma</span><span class="sxs-lookup"><span data-stu-id="7be11-158">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="7be11-159">Bir Web uygulamasını hazırlama için dağıtma</span><span class="sxs-lookup"><span data-stu-id="7be11-159">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="7be11-160">Üretimde dağıtım geri alma gerçekleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="7be11-160">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="7be11-161">Azure Storage kullanarak ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="7be11-161">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="7be11-162">[Web Apps Için otomatik ölçeklendirmeyi kullanma](#Exercise5) (Visual Studio 2013 Ultimate Edition için isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="7be11-162">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="7be11-163">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **75 dakika**</span><span class="sxs-lookup"><span data-stu-id="7be11-163">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="7be11-164">Visual Studio 'Yu ilk kez başlattığınızda, önceden tanımlanmış ayarlar koleksiyonundan birini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-164">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="7be11-165">Her önceden tanımlı koleksiyon, belirli bir geliştirme stiliyle eşleşecek şekilde tasarlanmıştır ve pencere düzenlerini, düzenleyici davranışını, IntelliSense kod parçacıklarını ve iletişim kutusu seçeneklerini belirler.</span><span class="sxs-lookup"><span data-stu-id="7be11-165">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="7be11-166">Bu laboratuvardaki yordamlarda, **genel geliştirme ayarları** koleksiyonu kullanılırken, Visual Studio 'da belirli bir görevi gerçekleştirmek için gereken eylemler açıklanır.</span><span class="sxs-lookup"><span data-stu-id="7be11-166">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="7be11-167">Geliştirme ortamınız için farklı bir ayarlar koleksiyonu seçerseniz, adımlarda dikkate almanız gereken adımlarda farklılıklar olabilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-167">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="7be11-168">Alıştırma 1: Entity Framework geçişlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="7be11-168">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="7be11-169">Bir uygulama geliştirirken, veri modeliniz zaman içinde değişebilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-169">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="7be11-170">Bu değişiklikler, veritabanınızdaki mevcut modeli etkileyebilir (yeni bir sürüm oluşturuyorsanız) ve hataları önlemek için veritabanınızı güncel tutmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7be11-170">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="7be11-171">Modelinizdeki bu değişikliklerin izlenmesini basitleştirmek için **Entity Framework Code First Migrations** , modelinizi veritabanı şemasıyla karşılaştıran değişiklikleri otomatik olarak algılar ve veritabanınızı güncelleştirmek ve veritabanınızın yeni *sürümlerini* oluşturmak için belirli bir kod oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7be11-171">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="7be11-172">Bu alıştırmada, uygulamanız için **geçişlerinizi** etkinleştirme ve veritabanlarınızı güncelleştirmek için nasıl kolayca tespit ve değişiklik oluşturabileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7be11-172">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="7be11-173">Görev 1 – geçişleri etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7be11-173">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="7be11-174">Bu görevde, **Geek test** veritabanına **Entity Framework Code First Migrations** etkinleştirme, modeli değiştirme ve bu değişikliklerin veritabanına nasıl yansıtıldığını anlama adımlarını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-174">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="7be11-175">Visual Studio 'Yu açın ve **Source\Ex1-UsingEntityFrameworkMigrations\Begin**adresinden **geeksınav. sln** çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-175">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="7be11-176">**NuGet** paketi bağımlılıklarını indirmek ve yüklemek için çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-176">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="7be11-177">Bunu yapmak için çözüme sağ tıklayın ve **çözüm oluştur** ' a tıklayın veya **CTRL + SHIFT + B**tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-177">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="7be11-178">Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-178">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="7be11-179">**Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-179">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="7be11-180">Mevcut modeli temel alan bir ilk geçiş oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="7be11-180">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="7be11-181">![Geçişleri etkinleştirme](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Geçişleri etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="7be11-181">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="7be11-182">*Geçişleri etkinleştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-182">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-183">Bu komut, **Configuration.cs**adlı bir dosya Içeren Geek test projesine bir **geçişler** klasörü ekler.</span><span class="sxs-lookup"><span data-stu-id="7be11-183">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="7be11-184">**Yapılandırma** sınıfı, geçiş işleminin bağlam için nasıl davranacağını yapılandırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7be11-184">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="7be11-185">Geçişler etkinken, veritabanını **Geek sınavın** gerektirdiği ilk verilerle doldurmak için **yapılandırma** sınıfını güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-185">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="7be11-186">**Geçişler**altında **Configuration.cs** dosyasını, bu laboratuvarın **source\varlıklar** klasöründe bulunan ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-186">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-187">**Geçişler** her veritabanı güncelleştirmesiyle ilgili **çekirdek** yöntemini çağıracak olduğundan, kayıtların veritabanında yinelenmediğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-187">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="7be11-188">**AddOrUpdate** yöntemi yinelenen verilerin engellenmesine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7be11-188">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="7be11-189">İlk geçiş eklemek için aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-189">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-190">LocalDB örneğiniz içinde &quot;GeekQuizProd&quot; adlı bir veritabanı olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7be11-190">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="7be11-191">![Temel şema geçişi ekleniyor](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Temel şema geçişi ekleniyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-191">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="7be11-192">*Temel şema geçişi ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-192">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-193">**Geçiş geçişi** , son geçişten sonra, modelinizde yaptığınız değişikliklere dayalı olarak bir sonraki geçişi kankatacaktır.</span><span class="sxs-lookup"><span data-stu-id="7be11-193">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="7be11-194">Bu durumda, projenin ilk geçişi olduğu için, **Triviacontext** sınıfında tanımlanmış tüm tabloları oluşturmak üzere betikleri ekler.</span><span class="sxs-lookup"><span data-stu-id="7be11-194">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="7be11-195">Aşağıdaki komutu çalıştırarak veritabanını güncelleştirmek için geçişi yürütün.</span><span class="sxs-lookup"><span data-stu-id="7be11-195">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="7be11-196">Bu komut için, hedef veritabanına uygulanan SQL deyimlerini görüntülemek üzere **verbose** bayrağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="7be11-196">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="7be11-197">![İlk veritabanı oluşturuluyor](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "İlk veritabanı oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-197">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="7be11-198">*İlk veritabanı oluşturuluyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-198">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-199">**Update-Database** bekleyen geçişleri veritabanına uygular.</span><span class="sxs-lookup"><span data-stu-id="7be11-199">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="7be11-200">Bu durumda, Web. config dosyanızda tanımlanan bağlantı dizesini kullanarak veritabanını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7be11-200">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="7be11-201">**Görünüm** menüsüne gidin ve **SQL Server Nesne Gezgini**açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-201">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="7be11-202">![SQL Server Nesne Gezgini aç](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server Nesne Gezgini aç")</span><span class="sxs-lookup"><span data-stu-id="7be11-202">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="7be11-203">*SQL Server Nesne Gezgini aç*</span><span class="sxs-lookup"><span data-stu-id="7be11-203">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="7be11-204">**SQL Server Nesne Gezgini** penceresinde, **SQL Server** düğümüne sağ tıklayıp **SQL Server Ekle...** seçeneğini belirleyerek LocalDB örneğinizi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-204">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="7be11-205">![SQL Server örneği ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server örneği ekleme")</span><span class="sxs-lookup"><span data-stu-id="7be11-205">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="7be11-206">*SQL Server Nesne Gezgini SQL Server örnek ekleme*</span><span class="sxs-lookup"><span data-stu-id="7be11-206">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="7be11-207">**Sunucu adını** *(LocalDB) \v11.0* olarak ayarlayın ve **Windows kimlik doğrulamasını** kimlik doğrulama modu olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="7be11-207">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="7be11-208">Devam etmek için **Bağlan**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-208">Click **Connect** to continue.</span></span>

    <span data-ttu-id="7be11-209">![LocalDB 'ye bağlanma](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB 'ye bağlanma")</span><span class="sxs-lookup"><span data-stu-id="7be11-209">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="7be11-210">*LocalDB 'ye bağlanma*</span><span class="sxs-lookup"><span data-stu-id="7be11-210">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="7be11-211">**GeekQuizProd** veritabanını açın ve **Tablolar** düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="7be11-211">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="7be11-212">Gördüğünüz gibi, **Update-Database** komutu **triviacontext** sınıfında tanımlanmış tüm tabloları üretti.</span><span class="sxs-lookup"><span data-stu-id="7be11-212">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="7be11-213">Dbo 'yi bulun **. Triviasorular** tablosu ve Columns düğümünü açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-213">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="7be11-214">Sonraki görevde, bu tabloya yeni bir sütun ekleyecek ve **geçişleri**kullanarak veritabanını güncellendirilecektir.</span><span class="sxs-lookup"><span data-stu-id="7be11-214">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="7be11-215">![Soruların sütunları](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Soruların sütunları")</span><span class="sxs-lookup"><span data-stu-id="7be11-215">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="7be11-216">*Soruların sütunları*</span><span class="sxs-lookup"><span data-stu-id="7be11-216">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="7be11-217">Görev 2 – geçişler kullanılarak veritabanı şemasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7be11-217">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="7be11-218">Bu görevde, modelinizde bir değişikliği algılamak ve veritabanını güncelleştirmek için gerekli kodu oluşturmak üzere **Entity Framework Code First Migrations** kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-218">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="7be11-219">Yeni bir özellik ekleyerek **Triviasoruların** varlığını güncelleşirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-219">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="7be11-220">Daha sonra yeni bir geçiş oluşturmak için komutları çalıştırarak tabloya yeni bir sütun ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-220">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="7be11-221">**Çözüm Gezgini**, **modeller** klasörünün içinde bulunan **TriviaQuestion.cs** dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-221">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="7be11-222">Aşağıdaki kod parçacığında gösterildiği gibi **İpucu**adlı yeni bir özellik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-222">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="7be11-223">**Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-223">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="7be11-224">Modelimizin değişikliğini yansıtan yeni bir geçiş oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="7be11-224">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="7be11-225">![Geçiş Ekle](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Geçiş Ekle")</span><span class="sxs-lookup"><span data-stu-id="7be11-225">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="7be11-226">*Geçiş Ekle*</span><span class="sxs-lookup"><span data-stu-id="7be11-226">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-227">Geçiş dosyası, **yukarı** ve **aşağı**olmak üzere iki yöntemden oluşur.</span><span class="sxs-lookup"><span data-stu-id="7be11-227">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    >
    > - <span data-ttu-id="7be11-228">**Up** yöntemi, uygulamamız için geçerli sürümünün veritabanına hangi değişikliklerin uygulanacağını belirtmek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7be11-228">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="7be11-229">**Up** yöntemine eklediğimiz değişiklikleri tersine çevirmek için **aşağı** doğru kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7be11-229">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    >
    > <span data-ttu-id="7be11-230">Veritabanı geçişi veritabanını güncelleştirdiğinde, zaman damgası sırasındaki tüm geçişleri çalıştırır ve yalnızca son güncelleştirmeden bu yana kullanılmamış olanlar (\_MigrationHistory tablosu, hangi geçişlerin uygulandığını izler).</span><span class="sxs-lookup"><span data-stu-id="7be11-230">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="7be11-231">Tüm geçişlerin **up** metodu çağrılır ve veritabanına belirttiğimiz değişiklikleri yapar.</span><span class="sxs-lookup"><span data-stu-id="7be11-231">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="7be11-232">Önceki bir geçişe geri dönmek isterseniz, değişiklikleri ters sırada yinelemek için **azaltma** yöntemi çağırılır.</span><span class="sxs-lookup"><span data-stu-id="7be11-232">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="7be11-233">**Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-233">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="7be11-234">**Update-Database** komutunun çıktısı, aşağıdaki görüntüde gösterildiği gibi **triviasorular** tablosuna yeni bir sütun eklemek için **alter table** SQL deyimini oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="7be11-234">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="7be11-235">![Oluşturulan sütun SQL açıklaması ekle](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Oluşturulan sütun SQL açıklaması ekle")</span><span class="sxs-lookup"><span data-stu-id="7be11-235">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="7be11-236">*Oluşturulan sütun SQL açıklaması ekle*</span><span class="sxs-lookup"><span data-stu-id="7be11-236">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="7be11-237">**SQL Server Nesne Gezgini**, dbo 'yı yenileyin **. Triviasorular** tablosu ve yeni **İpucu** sütununun görüntülendiğini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="7be11-237">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="7be11-238">![Yeni Ipucu sütununu gösterme](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Yeni Ipucu sütununu gösterme")</span><span class="sxs-lookup"><span data-stu-id="7be11-238">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="7be11-239">*Yeni Ipucu sütununu gösterme*</span><span class="sxs-lookup"><span data-stu-id="7be11-239">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="7be11-240">**TriviaQuestion.cs** düzenleyicisine geri döndüğünüzde, aşağıdaki kod parçacığında gösterildiği gibi *Ipucu* özelliğine bir **StringLength** kısıtlaması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-240">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="7be11-241">**Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-241">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="7be11-242">**Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-242">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="7be11-243">**Update-Database** komutunun çıktısı, aşağıdaki görüntüde gösterildiği gibi **üç aylık** dönemin *İpucu* sütun türünü güncelleştirmek için bir **alter table** SQL deyimini oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="7be11-243">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="7be11-244">![ALTER COLUMN SQL ifadesi oluşturuldu](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "ALTER COLUMN SQL ifadesi oluşturuldu")</span><span class="sxs-lookup"><span data-stu-id="7be11-244">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="7be11-245">*ALTER COLUMN SQL ifadesi oluşturuldu*</span><span class="sxs-lookup"><span data-stu-id="7be11-245">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="7be11-246">**SQL Server Nesne Gezgini**, dbo 'yı yenileyin **. Triviasorular** tablosu ve **İpucu** sütun türünün **nvarchar (150)** olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-246">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="7be11-247">![Yeni kısıtlama gösteriliyor](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Yeni kısıtlama gösteriliyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-247">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="7be11-248">*Yeni kısıtlama gösteriliyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-248">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="7be11-249">Alıştırma 2: hazırlama için bir Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="7be11-249">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="7be11-250">**Azure App Service Web Apps** , hazırlanan yayımlamayı gerçekleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7be11-250">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="7be11-251">Hazırlanan yayımlama, her varsayılan üretim sitesi için bir hazırlama site yuvası oluşturur ve bu yuvaları bir süre sonra takas etmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7be11-251">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="7be11-252">Bu, genel kullanıma sunulmadan önce değişiklikleri doğrulamak, site içeriğini artımlı olarak bütünleştirmek ve değişiklikler beklendiği gibi çalışmıyorsa geri dönmek için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="7be11-252">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="7be11-253">Bu alıştırmada, git kaynak denetimi 'ni kullanarak **Geek test** uygulamasını Web uygulamanızın hazırlama ortamına dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-253">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="7be11-254">Bunu yapmak için, Web uygulamasını oluşturur ve yönetim portalında gerekli bileşenleri temin eder, bir **Git** deposu yapılandırır ve uygulama kaynak kodunu yerel bilgisayarınızdan hazırlama yuvasına gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-254">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="7be11-255">Ayrıca, üretim veritabanınızı önceki alıştırmada oluşturduğunuz **Code First Migrations** de güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-255">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="7be11-256">Sonra, işlemini doğrulamak için bu test ortamında uygulamayı yürütecaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-256">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="7be11-257">Beklentilerinize göre çalıştığından emin olduktan sonra, uygulamayı üretime yükseltemeirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-257">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="7be11-258">Hazırlanmış yayımlamayı etkinleştirmek için Web uygulamasının **Standart modda**olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-258">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="7be11-259">Web uygulamanızı standart moda değiştirirseniz ek ücretler tahakkuk ettiğine unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-259">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="7be11-260">Fiyatlandırma hakkında daha fazla bilgi için bkz. [App Service fiyatlandırması](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="7be11-260">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="7be11-261">Görev 1 – Azure App Service bir Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7be11-261">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="7be11-262">Bu görevde, yönetim portalından **Azure App Service** bir Web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-262">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="7be11-263">Ayrıca, uygulama verilerini kalıcı hale getirmek ve kaynak denetimi için yerel bir git deposu yapılandırmak üzere bir **SQL veritabanı** yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-263">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="7be11-264">[Azure yönetim portalı](https://manage.windowsazure.com) ' na gidin ve aboneliğinizle ilişkili Microsoft hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-264">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![Azure yönetim portalı 'nda oturum açın](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="7be11-266">*Azure yönetim portalı 'nda oturum açın*</span><span class="sxs-lookup"><span data-stu-id="7be11-266">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="7be11-267">Sayfanın alt kısmındaki komut çubuğunda **Yeni** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-267">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="7be11-268">![Yeni bir Web uygulaması oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Yeni bir Web uygulaması oluşturma")</span><span class="sxs-lookup"><span data-stu-id="7be11-268">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="7be11-269">*Yeni bir Web uygulaması oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7be11-269">*Creating a new web app*</span></span>
3. <span data-ttu-id="7be11-270">**İşlem**, **Web sitesi** ve sonra **özel oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-270">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="7be11-271">![Özel oluştur kullanarak yeni bir Web uygulaması oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Özel oluştur kullanarak yeni bir Web uygulaması oluşturma")</span><span class="sxs-lookup"><span data-stu-id="7be11-271">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="7be11-272">*Özel oluştur kullanarak yeni bir Web uygulaması oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7be11-272">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="7be11-273">**Yeni Web sitesi-özel oluştur** iletişim kutusunda, kullanılabilir bir **URL** (örn. *Geek-test*) girin, **bölge** açılan listesinden bir konum seçin ve **veritabanı** açılır listesinden **Yeni bir SQL veritabanı oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-273">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="7be11-274">Son olarak, **kaynak denetiminden yayınla** onay kutusunu seçin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-274">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![Yeni Web uygulamasını özelleştirme](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="7be11-276">*Yeni Web uygulamasını özelleştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-276">*Customizing the new web app*</span></span>
5. <span data-ttu-id="7be11-277">Veritabanı ayarları için aşağıdaki bilgileri belirtin:</span><span class="sxs-lookup"><span data-stu-id="7be11-277">Specify the following information for the database settings:</span></span>

   - <span data-ttu-id="7be11-278">**Ad** metin kutusuna bir veritabanı adı girin (örn. *geektest\_DB*)</span><span class="sxs-lookup"><span data-stu-id="7be11-278">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
   - <span data-ttu-id="7be11-279">Sunucu **açılan** listesinde, **Yeni SQL veritabanı sunucusu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-279">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="7be11-280">Alternatif olarak, var olan bir sunucuyu seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-280">Alternatively, you can select an existing server.</span></span>
   - <span data-ttu-id="7be11-281">**Veritabanı Kullanıcı adı** ve **VERITABANı parolası** kutularına SQL veritabanı sunucusu için yönetici kullanıcı adını ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="7be11-281">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="7be11-282">Zaten oluşturduğunuz bir sunucuyu seçerseniz parola istenir.</span><span class="sxs-lookup"><span data-stu-id="7be11-282">If you select a server you have already created, you will be prompted for the password.</span></span>

     ![Veritabanı ayarlarını belirtme](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     <span data-ttu-id="7be11-284">*Veritabanı ayarlarını belirtme*</span><span class="sxs-lookup"><span data-stu-id="7be11-284">*Specifying the database settings*</span></span>
6. <span data-ttu-id="7be11-285">Devam etmek için **İleri** 'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-285">Click **Next** to continue.</span></span>
7. <span data-ttu-id="7be11-286">Kullanılacak kaynak denetimi için **yerel Git deposu** ' nu seçin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-286">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-287">Dağıtım kimlik bilgileri (Kullanıcı adı ve parola) istenebilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-287">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![Git deposu oluşturuluyor](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="7be11-289">*Git deposu oluşturuluyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-289">*Creating the Git repository*</span></span>
8. <span data-ttu-id="7be11-290">Yeni Web uygulaması oluşturuluncaya kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-290">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-291">Azure, varsayılan olarak *azurewebsites.net* adresinde etki alanları sağlar, ancak Azure yönetim portalı 'nı kullanarak özel etki alanları ayarlama olasılığından de olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7be11-291">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="7be11-292">Ancak, yalnızca belirli Azure App Service modlarını kullanıyorsanız özel etki alanlarını yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-292">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    >
    > <span data-ttu-id="7be11-293">Azure App Service ücretsiz, paylaşılan, temel, standart ve Premium sürümlerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-293">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="7be11-294">Ücretsiz ve paylaşılan modda tüm Web uygulamaları çok kiracılı bir ortamda çalışır ve CPU, bellek ve ağ kullanımı için kotalar vardır.</span><span class="sxs-lookup"><span data-stu-id="7be11-294">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="7be11-295">En fazla ücretsiz uygulama sayısı planınızda değişiklik gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-295">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="7be11-296">Standart modda, standart Azure işlem kaynaklarına karşılık gelen adanmış sanal makinelerde çalışan uygulamaları seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-296">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="7be11-297">Web uygulaması modu yapılandırmasını Web uygulamanızın **Ölçek** menüsünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-297">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    >
    > <span data-ttu-id="7be11-298">![Azure App Service modları](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service modları")</span><span class="sxs-lookup"><span data-stu-id="7be11-298">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    >
    > <span data-ttu-id="7be11-299">**Paylaşılan** veya **Standart** mod kullanıyorsanız, uygulamanızın **Yapılandır** menüsüne gidip *etki alanı adları*altındaki **etki alanlarını yönet** ' e tıklayarak web uygulamanız için özel etki alanlarını yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-299">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    >
    > <span data-ttu-id="7be11-300">![Etki alanlarını yönetme](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Etki Alanlarını Yönet")</span><span class="sxs-lookup"><span data-stu-id="7be11-300">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    >
    > <span data-ttu-id="7be11-301">![Özel etki alanlarını yönetme](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Özel etki alanlarını yönetme")</span><span class="sxs-lookup"><span data-stu-id="7be11-301">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="7be11-302">Web uygulaması oluşturulduktan sonra, yeni Web uygulamasının çalıştığını denetlemek için **URL** sütununun altındaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-302">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![Yeni Web uygulamasına göz atma](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="7be11-304">*Yeni Web uygulamasına göz atma*</span><span class="sxs-lookup"><span data-stu-id="7be11-304">*Browsing to the new web app*</span></span>

    ![çalışan Web uygulaması](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="7be11-306">*çalışan Web uygulaması*</span><span class="sxs-lookup"><span data-stu-id="7be11-306">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="7be11-307">Görev 2 – üretim SQL veritabanı oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="7be11-307">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="7be11-308">Bu görevde, önceki görevde oluşturduğunuz **Azure SQL veritabanı** örneğini hedefleyen veritabanını oluşturmak için **Entity Framework Code First Migrations** kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-308">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="7be11-309">Yönetim Portalı, önceki görevde oluşturduğunuz Web uygulamasına gidin ve **panosuna**gidin.</span><span class="sxs-lookup"><span data-stu-id="7be11-309">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="7be11-310">**Pano** sayfasında, **Hızlı bakış** bölümünün altındaki **bağlantı dizelerini görüntüle** bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7be11-310">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="7be11-311">![Bağlantı dizelerini görüntüle](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "Bağlantı dizelerini görüntüle")</span><span class="sxs-lookup"><span data-stu-id="7be11-311">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="7be11-312">*Bağlantı dizelerini görüntüle*</span><span class="sxs-lookup"><span data-stu-id="7be11-312">*View connection strings*</span></span>
3. <span data-ttu-id="7be11-313">**Bağlantı dizesi** değerini kopyalayın ve iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="7be11-313">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="7be11-314">![Azure Yönetim Portalı bağlantı dizesi](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure Yönetim Portalı bağlantı dizesi")</span><span class="sxs-lookup"><span data-stu-id="7be11-314">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="7be11-315">*Azure Yönetim Portalı bağlantı dizesi*</span><span class="sxs-lookup"><span data-stu-id="7be11-315">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="7be11-316">Azure 'da SQL veritabanlarının listesini görmek için **SQL veritabanları** ' na tıklayın</span><span class="sxs-lookup"><span data-stu-id="7be11-316">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="7be11-317">![SQL veritabanı menüsü](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL veritabanı menüsü")</span><span class="sxs-lookup"><span data-stu-id="7be11-317">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="7be11-318">*SQL veritabanı menüsü*</span><span class="sxs-lookup"><span data-stu-id="7be11-318">*SQL Database menu*</span></span>
5. <span data-ttu-id="7be11-319">Önceki görevde oluşturduğunuz veritabanını bulun ve sunucusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-319">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="7be11-320">![SQL veritabanı sunucusu](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Veritabanı sunucusu")</span><span class="sxs-lookup"><span data-stu-id="7be11-320">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="7be11-321">*SQL veritabanı sunucusu*</span><span class="sxs-lookup"><span data-stu-id="7be11-321">*SQL Database server*</span></span>
6. <span data-ttu-id="7be11-322">Sunucusunun **hızlı başlangıç** sayfasında, **Yapılandır**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-322">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="7be11-323">![Menüyü Yapılandır](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Menüyü Yapılandır")</span><span class="sxs-lookup"><span data-stu-id="7be11-323">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="7be11-324">*Menüyü Yapılandır*</span><span class="sxs-lookup"><span data-stu-id="7be11-324">*Configure menu*</span></span>
7. <span data-ttu-id="7be11-325">**Izin VERILEN IP adresleri** bölümünde, IP 'Nizin SQL veritabanı sunucusuna bağlanmasını sağlamak için **izin verilen IP adresleri bağlantısına Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-325">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="7be11-326">![İzin verilen IP adresleri](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "İzin verilen IP adresleri")</span><span class="sxs-lookup"><span data-stu-id="7be11-326">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="7be11-327">*İzin verilen IP adresleri*</span><span class="sxs-lookup"><span data-stu-id="7be11-327">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="7be11-328">Adımı gerçekleştirmek için sayfanın alt kısmındaki **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-328">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="7be11-329">Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="7be11-329">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="7be11-330">**Paket Yöneticisi konsolunda**, *[bağlantı-dize]* yer tutucusunu Azure 'dan kopyaladığınız bağlantı dizesiyle değiştirerek aşağıdaki komutu yürütün</span><span class="sxs-lookup"><span data-stu-id="7be11-330">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="7be11-331">![Windows Azure SQL veritabanı 'nı hedefleyen veritabanını güncelleştir](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL veritabanı 'nı hedefleyen veritabanını güncelleştir")</span><span class="sxs-lookup"><span data-stu-id="7be11-331">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="7be11-332">*Azure SQL veritabanı 'nı hedefleyen veritabanını güncelleştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-332">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="7be11-333">Görev 3 – git kullanarak hazırlama için Geek sınavını dağıtma</span><span class="sxs-lookup"><span data-stu-id="7be11-333">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="7be11-334">Bu görevde, Web uygulamanızda hazırlanan yayımlamayı etkinleştirecektir.</span><span class="sxs-lookup"><span data-stu-id="7be11-334">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="7be11-335">Daha sonra, Geek test uygulamasını doğrudan yerel bilgisayarınızdan Web uygulamanızın hazırlama ortamına yayımlamak için git ' i kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-335">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="7be11-336">Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web uygulamasının adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-336">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![Web uygulaması yönetim sayfalarını açma](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="7be11-338">*Web uygulaması yönetim sayfalarını açma*</span><span class="sxs-lookup"><span data-stu-id="7be11-338">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="7be11-339">**Ölçek** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="7be11-339">Navigate to the **Scale** page.</span></span> <span data-ttu-id="7be11-340">**Genel** bölümünde, yapılandırma için **Standart** ' ı seçin ve komut çubuğunda **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-340">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-341">Tüm Web uygulamalarını geçerli bölgede ve abonelikte **Standart** modda çalıştırmak Için, **siteleri seçin** yapılandırması ' nda **Tümünü Seç** onay kutusunu seçili bırakın.</span><span class="sxs-lookup"><span data-stu-id="7be11-341">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="7be11-342">Aksi takdirde, **Tümünü Seç** onay kutusunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-342">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="7be11-343">![Web uygulamasını standart moda yükseltme](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Web uygulamasını standart moda yükseltme")</span><span class="sxs-lookup"><span data-stu-id="7be11-343">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="7be11-344">*Web uygulamasını standart moda yükseltme*</span><span class="sxs-lookup"><span data-stu-id="7be11-344">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="7be11-345">Değişiklikleri onaylamak için **Evet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-345">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="7be11-346">![Standart mod değişikliğini onaylama](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Web uygulaması modunun değiştirilmesine devam etme")</span><span class="sxs-lookup"><span data-stu-id="7be11-346">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="7be11-347">*Standart mod değişikliğini onaylama*</span><span class="sxs-lookup"><span data-stu-id="7be11-347">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="7be11-348">**Pano** sayfasına gidin ve **Hızlı bakış** bölümünde **hazırlanan yayımlamayı etkinleştir** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-348">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="7be11-349">![Hazırlanan yayımlamayı etkinleştirme](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Hazırlanan yayımlamayı etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="7be11-349">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="7be11-350">*Hazırlanan yayımlamayı etkinleştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-350">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="7be11-351">Hazırlanmış yayımlamayı etkinleştirmek için **Evet** ' i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7be11-351">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="7be11-352">![Hazırlanan yayımlamayı onaylama](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Aşamalı yayımlamayı etkinleştirmek için Evet 'i tıklatın")</span><span class="sxs-lookup"><span data-stu-id="7be11-352">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="7be11-353">*Hazırlanan yayımlamayı onaylama*</span><span class="sxs-lookup"><span data-stu-id="7be11-353">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="7be11-354">Web Apps listesinde, hazırlama site yuvasını göstermek için Web uygulaması adınızın solundaki işareti genişletin.</span><span class="sxs-lookup"><span data-stu-id="7be11-354">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="7be11-355">Web uygulamanızın adı ve sonra ***(hazırlama)*** bulunur.</span><span class="sxs-lookup"><span data-stu-id="7be11-355">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="7be11-356">Yönetim sayfasına gitmek için hazırlama sitesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-356">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="7be11-357">![Hazırlama Web uygulamasına gitme](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Hazırlama Web uygulamasına gitme")</span><span class="sxs-lookup"><span data-stu-id="7be11-357">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="7be11-358">*Hazırlama uygulamasına gitme*</span><span class="sxs-lookup"><span data-stu-id="7be11-358">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="7be11-359">Yönetim sayfasının diğer Web uygulamaları yönetim sayfası gibi göründüğünü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-359">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="7be11-360">**Dağıtımlar** sayfasına gidin ve **Git URL 'si** değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-360">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="7be11-361">Bu alıştırmanın ilerleyen kısımlarında kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-361">You will use it later in this exercise.</span></span>

    ![Git URL 'SI değeri kopyalanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="7be11-363">*Git URL 'SI değeri kopyalanıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-363">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="7be11-364">Yeni bir **Git Bash** konsolu açın ve aşağıdaki komutları yürütün.</span><span class="sxs-lookup"><span data-stu-id="7be11-364">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="7be11-365">*[-APPLICATION-Path]* yer tutucusunu, bu laboratuvarın **Source\ex1-deployingwebsitetostaging\begin** klasöründe bulunan **geektest** çözümünün yoluyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-365">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git başlatması ve ilk kayıt](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="7be11-367">*Git başlatması ve ilk kayıt*</span><span class="sxs-lookup"><span data-stu-id="7be11-367">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="7be11-368">Web uygulamanızı uzak **Git** deposuna göndermek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7be11-368">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="7be11-369">Yer tutucusunu, yönetim portalından edindiğiniz URL ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-369">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="7be11-370">Sizden dağıtım parolanızı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="7be11-370">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Microsoft Azure 'a gönderiliyor](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="7be11-372">*Azure 'a gönderiliyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-372">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-373">Bir Web uygulamasının FTP ana bilgisayarına veya GIT deposuna içerik dağıttığınızda, Web uygulamasının **hızlı başlangıç** veya **Pano** yönetim sayfalarından oluşturduğunuz **dağıtım kimlik bilgilerini** kullanarak kimlik doğrulaması yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-373">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="7be11-374">Dağıtım kimlik bilgilerinizi görmüyorsanız, yönetim portalı 'nı kullanarak bunları kolayca sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-374">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="7be11-375">Web uygulaması **panosu** sayfasını açın ve **dağıtım kimlik bilgilerinizi sıfırlayın** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-375">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="7be11-376">Yeni bir parola girin ve **Tamam 'a**tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-376">Provide a new password and click **OK**.</span></span> <span data-ttu-id="7be11-377">Dağıtım kimlik bilgileri, aboneliğinizle ilişkili tüm Web uygulamalarıyla birlikte kullanılmak üzere geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7be11-377">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="7be11-378">Web uygulamasının başarıyla Azure 'a itildiğini doğrulamak için yönetim portalına dönün ve **Web siteleri**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-378">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="7be11-379">Web uygulamanızı bulun ve hazırlama site yuvasını göstermek için girişi genişletin.</span><span class="sxs-lookup"><span data-stu-id="7be11-379">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="7be11-380">Yönetim sayfasına gitmek için **adına** tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-380">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="7be11-381">**Dağıtım geçmişini**görmek için **dağıtımlar** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-381">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="7be11-382">*&quot;Ilk işlemesini&quot;* **etkin bir dağıtım** olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-382">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![Etkin dağıtım](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="7be11-384">*Etkin dağıtım*</span><span class="sxs-lookup"><span data-stu-id="7be11-384">*Active deployment*</span></span>
13. <span data-ttu-id="7be11-385">Son olarak, Web uygulamasına gitmek için komut çubuğunda bulunan **Araştır** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-385">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![Web uygulamasına gözatamıyorum](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="7be11-387">*Web uygulamasına gözatamıyorum*</span><span class="sxs-lookup"><span data-stu-id="7be11-387">*Browse web app*</span></span>
14. <span data-ttu-id="7be11-388">Uygulama başarıyla dağıtılırsa Geek test oturum açma sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7be11-388">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-389">Dağıtılan uygulamanın adres URL 'SI, Web uygulamanızın adını ve ardından *hazırlamayı*içerir.</span><span class="sxs-lookup"><span data-stu-id="7be11-389">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![Hazırlama ortamında çalışan uygulama](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="7be11-391">*Hazırlama ortamında çalışan uygulama*</span><span class="sxs-lookup"><span data-stu-id="7be11-391">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="7be11-392">Uygulamayı araştırmak isterseniz, yeni bir kullanıcı kaydetmek için **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-392">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="7be11-393">Hesap ayrıntılarını bir Kullanıcı adı, e-posta adresi ve parola girerek doldurun.</span><span class="sxs-lookup"><span data-stu-id="7be11-393">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="7be11-394">Ardından, uygulama, test ilk sorusunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7be11-394">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="7be11-395">Beklenen şekilde çalıştığından emin olmak için birkaç soruyu yanıtlayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-395">Answer a few questions to make sure it is working as expected.</span></span>

    ![Uygulama kullanılmak üzere hazırlanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="7be11-397">*Uygulama kullanılmak üzere hazırlanıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-397">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="7be11-398">Görev 4 – Web uygulamasını üretime yükseltme</span><span class="sxs-lookup"><span data-stu-id="7be11-398">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="7be11-399">Artık, Web uygulamasının hazırlama ortamında düzgün çalıştığını doğruladığınıza göre, bunu üretime yükseltmeye hazırsınız demektir.</span><span class="sxs-lookup"><span data-stu-id="7be11-399">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="7be11-400">Bu görevde, hazırlama site yuvasını üretim site yuvası ile takas edersiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-400">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="7be11-401">Yönetim portalına geri dönün ve hazırlama site yuvasını seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-401">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="7be11-402">Komut çubuğunda **takas et** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-402">Click **Swap** in the command bar.</span></span>

    ![Üretime değiştirme](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="7be11-404">*Üretime değiştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-404">*Swap to production*</span></span>
2. <span data-ttu-id="7be11-405">Değiştirme işlemine devam etmek için onay iletişim kutusunda **Evet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-405">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="7be11-406">Azure, üretim sitesinin içeriğini hazırlama sitesinin içeriğiyle hemen takas eder.</span><span class="sxs-lookup"><span data-stu-id="7be11-406">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-407">Hazırlanan sürümden bazı ayarlar otomatik olarak üretim sürümüne (örn. bağlantı dizesi geçersiz kılmaları, işleyici eşlemeleri vb.) kopyalanacak, ancak diğer ayarlar değişmeyecektir (örneğin, DNS uç noktaları, SSL bağlamaları vb.).</span><span class="sxs-lookup"><span data-stu-id="7be11-407">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![Değiştirme işlemi onaylanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="7be11-409">*Değiştirme işlemi onaylanıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-409">*Confirming swap operation*</span></span>
3. <span data-ttu-id="7be11-410">Değiştirme tamamlandıktan sonra üretim yuvasını seçin ve komut çubuğunda, üretim sitesini açmak için **Araştır** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-410">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="7be11-411">Adres çubuğundaki URL 'ye dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7be11-411">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-412">Önbelleği temizlemek için tarayıcınızı yenilemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-412">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="7be11-413">Internet Explorer 'da, **CTRL + R**tuşlarına basarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-413">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![Üretim ortamında çalışan Web uygulaması](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="7be11-415">**GitBash** konsolunda, yerel git deposunun uzak URL 'sini üretim yuvasını hedefleyecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-415">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="7be11-416">Bunu yapmak için, yer tutucuları dağıtım Kullanıcı adınızla ve Web uygulamanızın adıyla değiştirerek aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7be11-416">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-417">Aşağıdaki alıştırmalarda, değişiklikleri yalnızca laboratuvarın basitliği için hazırlama yerine üretim sitesine gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-417">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="7be11-418">Gerçek dünyada bir senaryoda, üretime yükseltmeden önce hazırlama ortamındaki değişikliklerin doğrulanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-418">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="7be11-419">Alıştırma 3: üretimde dağıtım geri alma Işlemi gerçekleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="7be11-419">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="7be11-420">Hazırlama ve üretim arasında, örneğin, **ücretsiz** veya **paylaşılan** modla çalışıyorsanız, hazırlık ve üretim arasında dinamik değiştirme gerçekleştirmek için bir hazırlama yuvalarınızın olmadığı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="7be11-420">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="7be11-421">Bu senaryolarda, üretime dağıtım yapmadan önce, uygulamanızı yerel olarak veya uzak bir sitede bir test ortamında test etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-421">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="7be11-422">Ancak, üretim sitesinde test aşamasında algılanamayan bir sorun ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-422">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="7be11-423">Bu durumda, mümkün olduğunca hızlı bir şekilde uygulamanın önceki ve daha kararlı bir sürümüne kolayca geçiş mekanizması olması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7be11-423">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="7be11-424">**Azure App Service**, kaynak denetiminden sürekli dağıtım, yönetim portalı 'nda kullanılabilir yeniden **dağıtma** eylemi sayesinde bunu mümkün hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7be11-424">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="7be11-425">Azure, depoya gönderilen işlemelerle ilişkili dağıtımları izler ve istediğiniz zaman, önceki dağıtımlarınızdan herhangi birini kullanarak uygulamanızı yeniden dağıtmaya yönelik bir seçenek sağlar.</span><span class="sxs-lookup"><span data-stu-id="7be11-425">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="7be11-426">Bu alıştırmada, bir *hatayı*kasıtlı olarak gösteren **Geek test** uygulamasındaki kodda bir değişiklik gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-426">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="7be11-427">Hatayı görmek için uygulamayı üretime dağıtırsınız ve ardından önceki duruma geri dönmek için yeniden dağıtma özelliğinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-427">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="7be11-428">Görev 1 – Geek test uygulamasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7be11-428">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="7be11-429">Bu görevde, seçilen test seçeneğini veritabanından yeni bir yönteme alan mantığın bir kısmını ayıklamak için **Triviacontroller** sınıfının küçük bir kod parçasını yeniden düzenlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-429">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="7be11-430">Önceki alıştırmada **Geektest** çözümüyle Visual Studio örneğine geçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-430">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="7be11-431">**Çözüm Gezgini**, **TriviaController.cs** dosyasını **denetleyiciler** klasörü içinde açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-431">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="7be11-432">**Storeasync** yöntemini bulun ve aşağıdaki şekilde vurgulanan kodu seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-432">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![Kodu seçme](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="7be11-434">*Kodu seçme*</span><span class="sxs-lookup"><span data-stu-id="7be11-434">*Selecting the code*</span></span>
4. <span data-ttu-id="7be11-435">Seçili koda sağ tıklayın, yeniden **Düzenle** menüsünü genişletin ve **yöntemi ayıkla...** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-435">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![Kod yeni bir yöntem olarak ayıklanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="7be11-437">*Ayıklama yöntemi seçiliyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-437">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="7be11-438">**Yöntemi Ayıkla** iletişim kutusunda, yeni yöntem *matchesoption* olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-438">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![Yöntem adını belirtme](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="7be11-440">*Ayıklanan metodun adını belirtme*</span><span class="sxs-lookup"><span data-stu-id="7be11-440">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="7be11-441">Daha sonra seçili kod **Matchesoption** yöntemine ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="7be11-441">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="7be11-442">Elde edilen kod aşağıdaki kod parçacığında gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7be11-442">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="7be11-443">Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-443">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="7be11-444">Görev 2 – Geek test uygulamasını yeniden dağıtma</span><span class="sxs-lookup"><span data-stu-id="7be11-444">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="7be11-445">Artık önceki görevde yaptığınız değişiklikleri depoya göndererek, üretim ortamına yeni bir dağıtım tetikleyitecaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-445">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="7be11-446">Daha sonra, Internet Explorer tarafından sunulan **F12 geliştirme araçlarını** kullanarak bir sorun troubleshot ve ardından Azure Yönetim portalından önceki dağıtıma geri alma işlemi gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-446">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="7be11-447">Güncelleştirilmiş uygulamayı Azure App Service dağıtmak için yeni bir **Git Bash** konsolu açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-447">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="7be11-448">Değişiklikleri Azure 'a göndermek için aşağıdaki komutları yürütün.</span><span class="sxs-lookup"><span data-stu-id="7be11-448">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="7be11-449">*[-APPLICATION-Path]* yer tutucusunu **geektest** çözümünün yoluyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-449">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="7be11-450">Sizden dağıtım parolanızı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="7be11-450">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![Yeniden düzenlenmiş kodunu Azure 'a iletme](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="7be11-452">*Yeniden düzenlenmiş kodunu Azure 'a iletme*</span><span class="sxs-lookup"><span data-stu-id="7be11-452">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="7be11-453">Internet Explorer 'ı açın ve Web uygulamanıza gidin (örn. `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="7be11-453">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="7be11-454">Önceden oluşturulan kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-454">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="7be11-455">Geliştirici araçlarını başlatmak için **F12** tuşuna basın, **ağ** sekmesini seçin ve kaydetmeye başlamak için **Yürüt** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-455">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="7be11-456">![Ağ kaydı başlatılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Ağ kaydı başlatılıyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-456">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="7be11-457">*Ağ kaydı başlatılıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-457">*Starting network recording*</span></span>
5. <span data-ttu-id="7be11-458">Sınavın herhangi bir seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-458">Select any option of the quiz.</span></span> <span data-ttu-id="7be11-459">Hiçbir şeyin gerçekleşmeyecek olduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-459">You will see that nothing happens.</span></span>
6. <span data-ttu-id="7be11-460">**F12** PENCERESINDE, http post isteğine karşılık gelen GIRIŞ bir http **500** sonucunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7be11-460">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![HTTP 500 hatası](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="7be11-462">*HTTP 500 hatası*</span><span class="sxs-lookup"><span data-stu-id="7be11-462">*HTTP 500 error*</span></span>
7. <span data-ttu-id="7be11-463">**Konsol** sekmesini seçin. Hatanın ayrıntıları ile bir hata günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-463">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![Günlüğe kaydedilen hata](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="7be11-465">*Günlüğe kaydedilen hata*</span><span class="sxs-lookup"><span data-stu-id="7be11-465">*Logged error*</span></span>
8. <span data-ttu-id="7be11-466">Hatanın Ayrıntılar bölümünü bulun.</span><span class="sxs-lookup"><span data-stu-id="7be11-466">Locate the details part of the error.</span></span> <span data-ttu-id="7be11-467">Açıkça, bu hata önceki adımlarda yaptığınız kod yeniden düzenlemesi nedeniyle oluşur.</span><span class="sxs-lookup"><span data-stu-id="7be11-467">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="7be11-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span><span class="sxs-lookup"><span data-stu-id="7be11-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="7be11-469">Tarayıcıyı kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-469">Do not close the browser.</span></span>
10. <span data-ttu-id="7be11-470">Yeni bir tarayıcı örneğinde [Azure yönetim portalı](https://manage.windowsazure.com) ' na gidin ve aboneliğinizle ilişkili Microsoft hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-470">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="7be11-471">**Web siteleri** ' ni seçin ve alıştırma 2 ' de oluşturduğunuz Web uygulamasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-471">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="7be11-472">**Dağıtımlar** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="7be11-472">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="7be11-473">Gerçekleştirilen tüm yürütmelerin dağıtım geçmişinde listelendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-473">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![Mevcut dağıtımların listesi](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="7be11-475">*Mevcut dağıtımların listesi*</span><span class="sxs-lookup"><span data-stu-id="7be11-475">*List of existing deployments*</span></span>
13. <span data-ttu-id="7be11-476">Önceki yürütmeyi seçin ve komut çubuğunda yeniden **Dağıt** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-476">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![Önceki işleme yeniden dağıtılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="7be11-478">*Önceki işleme yeniden dağıtılıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-478">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="7be11-479">Onaylamanız istendiğinde **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-479">When prompted to confirm, click **Yes**.</span></span>

    ![Yeniden dağıtımı onaylama](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="7be11-481">Dağıtım tamamlandığında, Web uygulamanızla birlikte tarayıcı örneğine dönün ve **CTRL + F5**tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-481">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="7be11-482">Seçeneklerden herhangi birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-482">Click any of the options.</span></span> <span data-ttu-id="7be11-483">Ters çevir animasyonu artık alınacaktır ve sonuç (*doğru/yanlış*) görüntülenecektir.</span><span class="sxs-lookup"><span data-stu-id="7be11-483">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="7be11-484">Seçim **Git Bash** konsoluna geçin ve önceki işlemeye dönmek için aşağıdaki komutları yürütün.</span><span class="sxs-lookup"><span data-stu-id="7be11-484">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-485">Bu komutlar, hatalı işlemede gerçekleştirilen git deposundaki tüm değişiklikleri geri yükleyen yeni bir kayıt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7be11-485">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="7be11-486">Daha sonra Azure, yeni yürütmeyi kullanarak uygulamayı yeniden dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-486">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="7be11-487">Alıştırma 4: Azure Storage kullanarak ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="7be11-487">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="7be11-488">**BLOB 'lar** , büyük miktarlarda yapılandırılmamış metin veya video, ses ve görüntü gibi ikili verileri depolamanın en kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="7be11-488">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="7be11-489">Uygulamanızın statik içeriğini depolamaya taşımak, doğrudan tarayıcıya görüntü veya belge sunarak uygulamanızı ölçeklendirmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7be11-489">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="7be11-490">Bu alıştırmada, uygulamanızın statik içeriğini bir blob kapsayıcısına taşıyacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-490">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="7be11-491">Daha sonra, içeriğinizi blob kapsayıcısına yönlendirmek üzere **Web. config** dosyasına BIR **ASP.net URL yeniden yazma kuralı** eklemek için uygulamanızı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-491">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="7be11-492">Görev 1 – Azure depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7be11-492">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="7be11-493">Bu görevde, yönetim portalını kullanarak yeni bir depolama hesabı oluşturmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-493">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="7be11-494">[Azure yönetim portalı](https://manage.windowsazure.com) ' na gidin ve aboneliğinizle ilişkili Microsoft hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-494">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="7be11-495">Yeni ' yi seçin **| Veri Hizmetleri | Depolama |** Yeni bir depolama hesabı oluşturmaya başlamak için hızlı oluştur.</span><span class="sxs-lookup"><span data-stu-id="7be11-495">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="7be11-496">Hesap için benzersiz bir ad girin ve listeden bir **bölge** seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-496">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="7be11-497">Devam etmek için **depolama hesabı oluştur** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-497">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="7be11-498">![Yeni depolama hesabı oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Yeni depolama hesabı oluşturma")</span><span class="sxs-lookup"><span data-stu-id="7be11-498">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="7be11-499">*Yeni depolama hesabı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7be11-499">*Creating a new storage account*</span></span>
3. <span data-ttu-id="7be11-500">**Depolama** bölümünde, aşağıdaki adımla devam etmek için yeni depolama hesabının durumu *çevrimiçi* olarak değişene kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-500">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="7be11-501">![Depolama hesabı oluşturuldu](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Depolama hesabı oluşturuldu")</span><span class="sxs-lookup"><span data-stu-id="7be11-501">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="7be11-502">*Depolama hesabı oluşturuldu*</span><span class="sxs-lookup"><span data-stu-id="7be11-502">*Storage Account created*</span></span>
4. <span data-ttu-id="7be11-503">Depolama hesabı adına tıklayın ve ardından sayfanın üst kısmındaki **Pano** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-503">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="7be11-504">**Pano** sayfası, hesap durumu ve uygulamalarınız dahilinde kullanılabilecek hizmet uç noktaları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7be11-504">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="7be11-505">![Depolama hesabı panosunu görüntüleme](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Depolama hesabı panosunu görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="7be11-505">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="7be11-506">*Depolama hesabı panosunu görüntüleme*</span><span class="sxs-lookup"><span data-stu-id="7be11-506">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="7be11-507">Gezinti çubuğundaki **erişim tuşlarını Yönet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-507">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="7be11-508">![Erişim anahtarlarını Yönet düğmesi](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Erişim anahtarlarını Yönet düğmesi")</span><span class="sxs-lookup"><span data-stu-id="7be11-508">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="7be11-509">*Erişim anahtarlarını Yönet düğmesi*</span><span class="sxs-lookup"><span data-stu-id="7be11-509">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="7be11-510">**Erişim anahtarlarını Yönet** iletişim kutusunda, Aşağıdaki alıştırmada gerekli olacak şekilde **depolama hesabı adı** ve **birincil erişim anahtarı** ' nı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-510">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="7be11-511">Sonra iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="7be11-511">Then, close the dialog box.</span></span>

    <span data-ttu-id="7be11-512">![Erişim anahtarını Yönet iletişim kutusu](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Erişim anahtarını Yönet iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="7be11-512">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="7be11-513">*Erişim anahtarını Yönet iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="7be11-513">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="7be11-514">Görev 2 – bir varlığı Azure Blob depolamaya yükleme</span><span class="sxs-lookup"><span data-stu-id="7be11-514">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="7be11-515">Bu görevde, depolama hesabınıza bağlanmak için Visual Studio 'daki Sunucu Gezgini penceresini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-515">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="7be11-516">Daha sonra bir blob kapsayıcısı oluşturacak ve kapsayıcıya Geek test logosu içeren bir dosya yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-516">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="7be11-517">Önceki alıştırmada **Geektest** çözümüyle Visual Studio örneğine geçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-517">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="7be11-518">Menü çubuğundan **Görünüm** ' ü seçin ve ardından **Sunucu Gezgini**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-518">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="7be11-519">**Sunucu Gezgini**, **Azure** düğümüne sağ tıklayın ve **Azure 'a Bağlan...** seçeneğini belirleyin. Aboneliğinizle ilişkili Microsoft hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-519">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![Microsoft Azure'a Bağlan](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="7be11-521">*Azure'a bağlanma*</span><span class="sxs-lookup"><span data-stu-id="7be11-521">*Connect to Azure*</span></span>
4. <span data-ttu-id="7be11-522">**Azure** düğümünü genişletin, **depolama alanı** ' na sağ tıklayın ve **dış depolama Ekle...** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-522">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="7be11-523">**Yeni depolama hesabı ekle** iletişim kutusunda, önceki görevde edindiğiniz **hesap adını** ve **hesap anahtarını** girip **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-523">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    ![Yeni depolama hesabı Ekle iletişim kutusu](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="7be11-525">*Yeni depolama hesabı Ekle iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="7be11-525">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="7be11-526">Depolama hesabınız **depolama** düğümünün altında görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="7be11-526">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="7be11-527">Depolama hesabınızı genişletin, **Bloblar** ' a sağ tıklayıp **BLOB kapsayıcısı oluştur...** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-527">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="7be11-528">![Blob kapsayıcısı oluştur](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Blob kapsayıcısı oluştur")</span><span class="sxs-lookup"><span data-stu-id="7be11-528">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="7be11-529">*Blob kapsayıcısı oluştur*</span><span class="sxs-lookup"><span data-stu-id="7be11-529">*Create Blob Container*</span></span>
7. <span data-ttu-id="7be11-530">**BLOB kapsayıcısı oluştur** iletişim kutusunda, blob kapsayıcısı için bir ad girin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-530">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="7be11-531">![Blob kapsayıcısı oluştur iletişim kutusu](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Blob kapsayıcısı oluştur iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="7be11-531">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="7be11-532">*Blob kapsayıcısı oluştur iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="7be11-532">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="7be11-533">Yeni blob kapsayıcısı **Bloblar** düğümüne eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="7be11-533">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="7be11-534">Kapsayıcıyı ortak hale getirmek için kapsayıcıdaki erişim izinlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-534">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="7be11-535">Bunu yapmak için, **görüntüler** kapsayıcısını sağ tıklatın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-535">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="7be11-536">![görüntü kapsayıcısı özellikleri](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "görüntü kapsayıcısı özellikleri")</span><span class="sxs-lookup"><span data-stu-id="7be11-536">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="7be11-537">*Görüntü kapsayıcısı özellikleri*</span><span class="sxs-lookup"><span data-stu-id="7be11-537">*Images container properties*</span></span>
9. <span data-ttu-id="7be11-538">**Özellikler** penceresinde, **kapsayıcıya** **Genel okuma erişimi** ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-538">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="7be11-539">![Genel okuma erişimi Özelliği değiştiriliyor](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Genel okuma erişimi Özelliği değiştiriliyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-539">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="7be11-540">*Genel okuma erişimi Özelliği değiştiriliyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-540">*Changing public read access property*</span></span>
10. <span data-ttu-id="7be11-541">Genel erişim özelliğini değiştirmek istediğinizden emin olup istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-541">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="7be11-542">![Microsoft Visual Studio uyarısı](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio uyarısı")</span><span class="sxs-lookup"><span data-stu-id="7be11-542">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="7be11-543">*Microsoft Visual Studio uyarısı*</span><span class="sxs-lookup"><span data-stu-id="7be11-543">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="7be11-544">**Sunucu Gezgini**, **görüntüler** blob kapsayıcısını sağ tıklatın ve **BLOB kapsayıcısını görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-544">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="7be11-545">![Blob kapsayıcısını görüntüle](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob kapsayıcısını görüntüle")</span><span class="sxs-lookup"><span data-stu-id="7be11-545">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="7be11-546">*Blob kapsayıcısını görüntüle*</span><span class="sxs-lookup"><span data-stu-id="7be11-546">*View Blob Container*</span></span>
12. <span data-ttu-id="7be11-547">Görüntüler kapsayıcısının yeni bir pencerede açılması ve girişin gösterilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="7be11-547">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="7be11-548">Blob kapsayıcısına bir dosya yüklemek için **karşıya yükle** simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-548">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="7be11-549">![Girişi olmayan görüntü kapsayıcısı](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Girişi olmayan görüntü kapsayıcısı")</span><span class="sxs-lookup"><span data-stu-id="7be11-549">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="7be11-550">*Girişi olmayan görüntü kapsayıcısı*</span><span class="sxs-lookup"><span data-stu-id="7be11-550">*Images container with no entries*</span></span>
13. <span data-ttu-id="7be11-551">**Blobu karşıya yükle** iletişim kutusunda, laboratuvarın **varlıklar** klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="7be11-551">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="7be11-552">**Logo-Big. png** dosyasını seçin ve **Aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-552">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="7be11-553">Dosya karşıya yüklenene kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-553">Wait until the file is uploaded.</span></span> <span data-ttu-id="7be11-554">Karşıya yükleme tamamlandığında, dosyanın görüntüler kapsayıcısında listelenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-554">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="7be11-555">Dosya girdisine sağ tıklayıp **URL 'Yi Kopyala**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-555">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="7be11-556">![Blob URL 'sini Kopyala](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Blob dosyası URL 'sini Kopyala")</span><span class="sxs-lookup"><span data-stu-id="7be11-556">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="7be11-557">*Blob URL 'sini Kopyala*</span><span class="sxs-lookup"><span data-stu-id="7be11-557">*Copy blob URL*</span></span>
15. <span data-ttu-id="7be11-558">Internet Explorer 'ı açın ve URL 'YI yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="7be11-558">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="7be11-559">Aşağıdaki görüntü tarayıcıda gösterilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7be11-559">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="7be11-560">![Windows blob depolamadan logo-Big. png görüntüsü](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "depolamadan logo-Big. png görüntüsü")</span><span class="sxs-lookup"><span data-stu-id="7be11-560">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="7be11-561">*Azure Blob depolamadan logo-Big. png görüntüsü*</span><span class="sxs-lookup"><span data-stu-id="7be11-561">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="7be11-562">Görev 3 – Azure Blob depolama alanından statik Içerik kullanmak için çözümü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7be11-562">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="7be11-563">Bu görevde, **Web. config** dosyasına BIR ASP.net URL yeniden yazma kuralı ekleyerek Azure Blob depolama alanına (Web uygulamasında bulunan görüntü yerine) yüklenen görüntüyü kullanmak Için **geektest** çözümünü yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-563">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="7be11-564">Visual Studio 'da, **Geektest** projesi içindeki **Web. config** dosyasını açın ve **&lt;System. webserver&gt;** öğesini bulun.</span><span class="sxs-lookup"><span data-stu-id="7be11-564">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="7be11-565">Bir URL yeniden yazma kuralı eklemek için aşağıdaki kodu ekleyin ve yer tutucuyu depolama hesabınızın adıyla güncelleyerek.</span><span class="sxs-lookup"><span data-stu-id="7be11-565">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="7be11-566">(Kod parçacığı- *Websitesinproduction-EX4-UrlRewriteRule*)</span><span class="sxs-lookup"><span data-stu-id="7be11-566">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="7be11-567">URL yeniden yazma, gelen bir web isteğini kesintiye uğratan ve isteği farklı bir kaynağa yönlendirmeye yönelik bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="7be11-567">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="7be11-568">URL yeniden yazma kuralları yeniden yazma motoruna bir isteğin yeniden yönlendirilmesi gerektiğinde ve nereye yönlendirilmeleri gerektiğini söyler.</span><span class="sxs-lookup"><span data-stu-id="7be11-568">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="7be11-569">Yeniden yazma kuralı iki dizeden oluşur: istenen URL 'de (genellikle normal ifadeler kullanılarak) aranacak model ve bulunursa, deseninin yerini alacak dize.</span><span class="sxs-lookup"><span data-stu-id="7be11-569">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="7be11-570">Daha fazla bilgi için bkz. [ASP.net Içinde URL yeniden yazma](https://msdn.microsoft.com/library/ms972974.aspx).</span><span class="sxs-lookup"><span data-stu-id="7be11-570">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="7be11-571">Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-571">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="7be11-572">Güncelleştirilmiş uygulamayı Azure App Service dağıtmak için yeni bir **Git Bash** konsolu açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-572">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="7be11-573">Değişiklikleri Azure 'a göndermek için aşağıdaki komutları yürütün.</span><span class="sxs-lookup"><span data-stu-id="7be11-573">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="7be11-574">*[-APPLICATION-Path]* yer tutucusunu **geektest** çözümünün yoluyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-574">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="7be11-575">Sizden dağıtım parolanızı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="7be11-575">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Güncelleştirme Azure 'a dağıtılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="7be11-577">*Güncelleştirme Azure 'a dağıtılıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-577">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="7be11-578">Görev 4 – doğrulama</span><span class="sxs-lookup"><span data-stu-id="7be11-578">Task 4 – Verification</span></span>

<span data-ttu-id="7be11-579">Bu görevde, **Geek test** uygulamasına göz atabilmeniz Için **Internet Explorer** 'ı kullanacaksınız ve görüntülerin URL yeniden yazma kuralının çalışıp çalışmadığını ve **Azure Blob depolamada**barındırılan görüntüye yönlendirildiğini kontrol edersiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-579">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="7be11-580">Internet Explorer 'ı açın ve Web uygulamanıza gidin (örn. `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="7be11-580">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="7be11-581">Önceden oluşturulan kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7be11-581">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="7be11-582">![Görüntüyle birlikte Geek test Web uygulamasını gösterme](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Görüntüyle birlikte Geek test Web uygulamasını gösterme")</span><span class="sxs-lookup"><span data-stu-id="7be11-582">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="7be11-583">*Görüntüyle birlikte Geek test Web uygulamasını gösterme*</span><span class="sxs-lookup"><span data-stu-id="7be11-583">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="7be11-584">Geliştirici araçlarını başlatmak için **F12** tuşuna basın, **ağ** sekmesini seçin ve kaydı başlatın.</span><span class="sxs-lookup"><span data-stu-id="7be11-584">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="7be11-585">![Ağ kaydı başlatılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Ağ kaydı başlatılıyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-585">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="7be11-586">*Ağ kaydı başlatılıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-586">*Starting network recording*</span></span>
3. <span data-ttu-id="7be11-587">Web sayfasını yenilemek için **CTRL + F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7be11-587">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="7be11-588">Sayfa yükleme tamamlandıktan sonra, http **301** sonucuyla **/IMG/logo-Big.png** URL 'si için BIR http isteği ve http **200** sonucuyla birlikte `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL 'si için bir istek görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-588">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="7be11-589">![URL yeniden yönlendirmesi doğrulanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Geliştirme araçlarındaki yeniden yönlendirmeyi gösterme")</span><span class="sxs-lookup"><span data-stu-id="7be11-589">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="7be11-590">*URL yeniden yönlendirmesi doğrulanıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-590">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="7be11-591">Alıştırma 5: Web Apps için otomatik ölçeklendirmeyi kullanma</span><span class="sxs-lookup"><span data-stu-id="7be11-591">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="7be11-592">Bu alıştırma isteğe bağlıdır, çünkü yalnızca **Visual Studio 2013 Ultimate Edition**Için kullanılabilen Web yükü &amp; performans testi için destek gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7be11-592">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="7be11-593">Belirli Visual Studio 2013 özellikleri hakkında daha fazla bilgi için, sürümleri [burada](https://www.microsoft.com/visualstudio/eng/products/compare)karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="7be11-593">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>

<span data-ttu-id="7be11-594">**Azure App Service Web Apps** , **Standart modda**çalışan Web uygulamaları için otomatik ölçeklendirme özelliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7be11-594">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="7be11-595">Otomatik ölçeklendirme, Azure 'un yük 'e bağlı olarak Web uygulamanızın örnek sayısını otomatik olarak ölçeklendirmesine imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="7be11-595">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="7be11-596">Otomatik ölçeklendirme etkinleştirildiğinde Azure, Web uygulamanızın CPU 'sunu her beş dakikada bir denetler ve bu noktada gerektiğinde örnekler ekler.</span><span class="sxs-lookup"><span data-stu-id="7be11-596">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="7be11-597">CPU kullanımı düşükse, Azure, Web uygulamanızın performansının düşürülmemesini sağlamak için örnekleri iki saatte bir daha kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7be11-597">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="7be11-598">Bu alıştırmada, **Geek test** Web uygulaması Için **Otomatik ölçeklendirme** özelliğini yapılandırmak için gerekli olan adımlara gidecaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-598">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="7be11-599">Uygulama üzerinde bir örnek yükseltmesi tetikleyecek kadar CPU yükü oluşturmak için bir Visual Studio yük testi çalıştırarak bu özelliği doğrulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-599">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="7be11-600">Görev 1 – CPU ölçüsüne göre otomatik ölçeklendirmeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7be11-600">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="7be11-601">Bu görevde, alıştırma 2 ' de oluşturduğunuz Web uygulamasına yönelik otomatik ölçeklendirme özelliğini etkinleştirmek için Azure yönetim portalını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-601">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="7be11-602">[Azure yönetim portalı](https://manage.windowsazure.com/)' nda **Web siteleri** ' ni seçin ve alıştırma 2 ' de oluşturduğunuz Web uygulamasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-602">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="7be11-603">**Ölçek** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="7be11-603">Navigate to the **Scale** page.</span></span> <span data-ttu-id="7be11-604">**Kapasite** bölümünde, **ölçüm için ölçek yapılandırmasına göre** **CPU** ' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-604">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-605">CPU 'ya göre ölçeklendirilirken, Azure, CPU kullanımı değişirse uygulamanın kullandığı örneklerin sayısını dinamik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="7be11-605">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="7be11-606">![CPU 'ya göre ölçeklendirmeye seçme](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Otomatik ölçeklendirme için CPU ölçüsünü seçme")</span><span class="sxs-lookup"><span data-stu-id="7be11-606">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="7be11-607">*CPU 'ya göre ölçeklendirmeye seçme*</span><span class="sxs-lookup"><span data-stu-id="7be11-607">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="7be11-608">**Hedef CPU** yapılandırmasını **20**-yüzde **40** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-608">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-609">Bu Aralık, Web uygulamanız için Ortalama CPU kullanımını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7be11-609">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="7be11-610">Azure, Web uygulamanızı bu aralıkta tutmak için örnekler ekler veya kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7be11-610">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="7be11-611">Ölçeklendirme için kullanılan minimum ve maksimum örnek sayısı **örnek sayısı** yapılandırmasında belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7be11-611">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="7be11-612">Azure hiçbir şekilde bu sınırın üzerinde veya ötesine geçmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="7be11-612">Azure will never go above or beyond that limit.</span></span>
    >
    > <span data-ttu-id="7be11-613">Varsayılan **hedef CPU** değerleri yalnızca bu laboratuvarın amaçları doğrultusunda değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="7be11-613">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="7be11-614">CPU aralığını küçük değerlerle yapılandırarak, uygulamaya bir orta yük yerleştirildiğinde otomatik ölçeklendirmeyi tetikleme olasılığını artırırsınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-614">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="7be11-615">![Hedef CPU 'YU 20 ila %40 arasında olacak şekilde değiştirme](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Hedef CPU 'YU 20 ila %40 arasında olacak şekilde değiştirme")</span><span class="sxs-lookup"><span data-stu-id="7be11-615">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="7be11-616">*Hedef CPU 'YU 20 ila %40 arasında olacak şekilde değiştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-616">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="7be11-617">Değişiklikleri kaydetmek için komut çubuğunda **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-617">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="7be11-618">Görev 2 – Visual Studio ile yük testi</span><span class="sxs-lookup"><span data-stu-id="7be11-618">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="7be11-619">**Otomatik ölçeklendirme** yapılandırıldıktan sonra, Web UYGULAMANıZDA bazı CPU yükü oluşturmak Için Visual Studio 'Da bir **Web performansı ve yük testi projesi** oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7be11-619">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="7be11-620">**Visual Studio Ultimate 2013** açın ve dosya ' yı seçin **| Yeni | Proje..** . Yeni bir çözüm başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="7be11-620">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="7be11-621">![Yeni bir proje oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Yeni proje oluşturma")</span><span class="sxs-lookup"><span data-stu-id="7be11-621">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="7be11-622">*Yeni bir proje oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7be11-622">*Creating a new project*</span></span>
2. <span data-ttu-id="7be11-623">**Yeni proje** iletişim kutusunda, Web performansı ' nı seçin ve görsel  **C# ' ün altında yük testi projesi | Test** sekmesi. **.NET Framework 4,5** ' nin seçildiğinden emin olun, projeyi *webandloadtestproject*olarak adlandırın, bir **konum** seçin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-623">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="7be11-624">![Yeni bir Web ve yük testi projesi oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Yeni bir Web ve yük testi projesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="7be11-624">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="7be11-625">*Yeni bir Web ve yük testi projesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7be11-625">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="7be11-626">**WebTest1. webtest** içinde **WebTest1** düğümüne sağ tıklayıp **istek ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-626">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="7be11-627">![WebTest1 'e istek ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "WebTest1 'e istek ekleme")</span><span class="sxs-lookup"><span data-stu-id="7be11-627">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="7be11-628">*WebTest1 'e istek ekleme*</span><span class="sxs-lookup"><span data-stu-id="7be11-628">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="7be11-629">Yeni istek düğümünün **Özellikler** penceresinde **URL** özelliğini Web uygulamanızın URL 'sini işaret etmek üzere güncelleştirin (ör. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ).</span><span class="sxs-lookup"><span data-stu-id="7be11-629">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="7be11-630">![URL özelliğini değiştirme](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "URL özelliğini değiştirme")</span><span class="sxs-lookup"><span data-stu-id="7be11-630">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="7be11-631">*URL özelliğini değiştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-631">*Changing the Url property*</span></span>
5. <span data-ttu-id="7be11-632">**WebTest1. webtest** penceresinde, **WebTest1** öğesine sağ tıklayın ve **döngü Ekle...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-632">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="7be11-633">![WebTest1 'e döngü ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "WebTest1 'e döngü ekleme")</span><span class="sxs-lookup"><span data-stu-id="7be11-633">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="7be11-634">*WebTest1 'e döngü ekleme*</span><span class="sxs-lookup"><span data-stu-id="7be11-634">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="7be11-635">**Koşullu kural ve Döngülenecek öğe Ekle** iletişim kutusunda, **for döngüsü** kuralını seçin ve aşağıdaki özellikleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7be11-635">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

   1. <span data-ttu-id="7be11-636">**Sonlandırma değeri:** 1000</span><span class="sxs-lookup"><span data-stu-id="7be11-636">**Terminating value:** 1000</span></span>
   2. <span data-ttu-id="7be11-637">**Bağlam parametresi adı:** İden</span><span class="sxs-lookup"><span data-stu-id="7be11-637">**Context Parameter Name:** Iterator</span></span>
   3. <span data-ttu-id="7be11-638">**Artış değeri:** 1</span><span class="sxs-lookup"><span data-stu-id="7be11-638">**Increment Value:** 1</span></span>

      <span data-ttu-id="7be11-639">![For döngüsü kuralını seçme ve özellikleri güncelleştirme](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "For döngüsü kuralını seçme ve özellikleri güncelleştirme")</span><span class="sxs-lookup"><span data-stu-id="7be11-639">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

      <span data-ttu-id="7be11-640">*For döngüsü kuralını seçme ve özellikleri güncelleştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-640">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="7be11-641">**Döngüdeki öğeler** bölümünde, döngünün ilk ve son öğesi olarak daha önce oluşturduğunuz isteği seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-641">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="7be11-642">Devam etmek için **Tamam** 'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-642">Click **OK** to continue.</span></span>

    <span data-ttu-id="7be11-643">![Döngünün ilk ve son öğelerini seçme](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Döngünün ilk ve son öğelerini seçme")</span><span class="sxs-lookup"><span data-stu-id="7be11-643">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="7be11-644">*Döngünün ilk ve son öğelerini seçme*</span><span class="sxs-lookup"><span data-stu-id="7be11-644">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="7be11-645">**Çözüm Gezgini**, **webandloadtestproject** projesine sağ tıklayın, **Ekle** menüsünü ve **Yük testi seç...** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="7be11-645">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="7be11-646">![WebAndLoadTestProject projesine yük testi ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject projesine yük testi ekleme")</span><span class="sxs-lookup"><span data-stu-id="7be11-646">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="7be11-647">*WebAndLoadTestProject projesine yük testi ekleme*</span><span class="sxs-lookup"><span data-stu-id="7be11-647">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="7be11-648">**Yeni Yük Testi Sihirbazı** Iletişim kutusunda **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-648">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="7be11-649">![Yeni Yük Testi Sihirbazı](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "Yeni Yük Testi Sihirbazı")</span><span class="sxs-lookup"><span data-stu-id="7be11-649">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="7be11-650">*Yeni Yük Testi Sihirbazı*</span><span class="sxs-lookup"><span data-stu-id="7be11-650">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="7be11-651">**Senaryo** sayfasında **düşünme süreleri kullanmayın** ' ı seçin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-651">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="7be11-652">![Düşünme sürelerini kullanmayı seçme](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Düşünme sürelerini kullanmayı seçme")</span><span class="sxs-lookup"><span data-stu-id="7be11-652">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="7be11-653">*Düşünme sürelerini kullanmayı seçme*</span><span class="sxs-lookup"><span data-stu-id="7be11-653">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="7be11-654">**Yük kalıbı** sayfasında, **sabit yükleme** seçeneğinin seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7be11-654">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="7be11-655">**Kullanıcı sayısı** ayarını **250** Kullanıcı olarak değiştirin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-655">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="7be11-656">![Kullanıcı sayısını 250 olarak değiştirme](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Kullanıcı sayısını 250 olarak değiştirme")</span><span class="sxs-lookup"><span data-stu-id="7be11-656">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="7be11-657">*Kullanıcı sayısını 250 olarak değiştirme*</span><span class="sxs-lookup"><span data-stu-id="7be11-657">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="7be11-658">**Test karışımı modeli** sayfasında, **sıralı test sırasına göre** ' yi seçin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-658">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="7be11-659">![Test karışımı modelini seçme](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Test karışımı modelini seçme")</span><span class="sxs-lookup"><span data-stu-id="7be11-659">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="7be11-660">*Test karışımı modelini seçme*</span><span class="sxs-lookup"><span data-stu-id="7be11-660">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="7be11-661">**Test karışımı modeli** sayfasında, karışıma bir test eklemek için **Ekle...** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-661">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="7be11-662">![Test karışımına test ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Test karışımına test ekleme")</span><span class="sxs-lookup"><span data-stu-id="7be11-662">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="7be11-663">*Test karışımına test ekleme*</span><span class="sxs-lookup"><span data-stu-id="7be11-663">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="7be11-664">**Testleri Ekle** iletişim kutusunda, **Seçili testler** listesine test eklemek için **WebTest1** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-664">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="7be11-665">Devam etmek için **Tamam** 'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-665">Click **OK** to continue.</span></span>

    <span data-ttu-id="7be11-666">![WebTest1 testi ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "WebTest1 testi ekleme")</span><span class="sxs-lookup"><span data-stu-id="7be11-666">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="7be11-667">*WebTest1 testi ekleme*</span><span class="sxs-lookup"><span data-stu-id="7be11-667">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="7be11-668">**Test karışımı** sayfasına geri döndüğünüzde **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-668">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="7be11-669">![Test karışımı sayfası Tamamlanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Test karışımı sayfası Tamamlanıyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-669">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="7be11-670">*Test karışımı sayfası Tamamlanıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-670">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="7be11-671">**Ağ karışımı** sayfasında, **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-671">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="7be11-672">![Ağ karışımı sayfasında ileri 'ye tıklama](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Ağ karışımı sayfasında ileri 'ye tıklama")</span><span class="sxs-lookup"><span data-stu-id="7be11-672">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="7be11-673">*Ağ karışımı sayfasında ileri 'ye tıklama*</span><span class="sxs-lookup"><span data-stu-id="7be11-673">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="7be11-674">**Tarayıcı karışımı** sayfasında, tarayıcı türü olarak **Internet Explorer 10,0** ' ı seçin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-674">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="7be11-675">![Tarayıcı türünü seçme](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Tarayıcı türünü seçme")</span><span class="sxs-lookup"><span data-stu-id="7be11-675">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="7be11-676">*Tarayıcı türünü seçme*</span><span class="sxs-lookup"><span data-stu-id="7be11-676">*Selecting the browser type*</span></span>
18. <span data-ttu-id="7be11-677">**Sayaç kümeleri** sayfasında, **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-677">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="7be11-678">![Sayaç kümeleri sayfasında Ileri 'ye tıklama](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Sayaç kümeleri sayfasında Ileri 'ye tıklama")</span><span class="sxs-lookup"><span data-stu-id="7be11-678">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="7be11-679">*Sayaç kümeleri sayfasında Ileri 'ye tıklama*</span><span class="sxs-lookup"><span data-stu-id="7be11-679">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="7be11-680">**Ayarları Çalıştır** sayfasında, **Yük testi süresini** **5 dakikaya** ayarlayın ve **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-680">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="7be11-681">![Yük testi süresini 5 dakikaya ayarlama](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Yük testi süresini 5 dakikaya ayarlama")</span><span class="sxs-lookup"><span data-stu-id="7be11-681">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="7be11-682">*Yük testi süresini 5 dakikaya ayarlama*</span><span class="sxs-lookup"><span data-stu-id="7be11-682">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="7be11-683">**Çözüm Gezgini**, test ayarlarını araştırmak için **yerel. Settings** dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-683">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="7be11-684">Varsayılan olarak, Visual Studio Testleri çalıştırmak için yerel bilgisayarınızı kullanır.</span><span class="sxs-lookup"><span data-stu-id="7be11-684">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-685">Alternatif olarak, test projenizi **Azure test Plans**kullanarak bulutta yük testlerini çalıştıracak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-685">Alternatively, you can configure your test project to run the load tests in the cloud using **Azure Test Plans**.</span></span> <span data-ttu-id="7be11-686">Azure Test Plans, daha gerçekçi bir yükü taklit eden, CPU kapasitesi, kullanılabilir bellek ve ağ bant genişliği gibi yerel ortam kısıtlamalarını önyükleyen bulut tabanlı bir yük testi hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="7be11-686">Azure Test Plans provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory, and network bandwidth.</span></span> <span data-ttu-id="7be11-687">Yük testlerini çalıştırmak için Azure Test Plans kullanma hakkında daha fazla bilgi için bkz. [Yük testi senaryoları](/azure/devops/test/load-test/overview?view=vsts).</span><span class="sxs-lookup"><span data-stu-id="7be11-687">For more information about using Azure Test Plans to run load tests, see [Load testing scenarios](/azure/devops/test/load-test/overview?view=vsts).</span></span>

    ![Test ayarları](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="7be11-689">Görev 3 – otomatik ölçeklendirme doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7be11-689">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="7be11-690">Şimdi, önceki görevde oluşturduğunuz yük testini yürütülecektir ve Web uygulamanızın yük altında nasıl davrandığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7be11-690">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="7be11-691">**Çözüm Gezgini**, yük testini açmak için **LoadTest1. LoadTest** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-691">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="7be11-692">![LoadTest1. LoadTest açılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "LoadTest1. LoadTest açılıyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-692">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="7be11-693">*LoadTest1. LoadTest açılıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-693">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="7be11-694">**LoadTest1. LoadTest** penceresinde, yük testini çalıştırmak için araç kutusundaki ilk düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7be11-694">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="7be11-695">![Yük testini çalıştırma](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Yük testini çalıştırma")</span><span class="sxs-lookup"><span data-stu-id="7be11-695">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="7be11-696">*Yük testini çalıştırma*</span><span class="sxs-lookup"><span data-stu-id="7be11-696">*Running the load test*</span></span>
3. <span data-ttu-id="7be11-697">Yük testi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7be11-697">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-698">Yük testi, istekleri Web uygulamasına aynı anda gönderen birden çok kullanıcıyı benzetir.</span><span class="sxs-lookup"><span data-stu-id="7be11-698">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="7be11-699">Test çalışırken, herhangi bir hata, uyarı veya yük testi çalıştırla ilgili diğer bilgileri algılamak için kullanılabilir sayaçları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-699">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="7be11-700">![Yük testi çalışıyor](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Yük testi tamamlanana kadar bekleniyor")</span><span class="sxs-lookup"><span data-stu-id="7be11-700">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="7be11-701">*Yük testi çalışıyor*</span><span class="sxs-lookup"><span data-stu-id="7be11-701">*Load test running*</span></span>
4. <span data-ttu-id="7be11-702">Test tamamlandıktan sonra, yönetim portalına geri dönün ve Web uygulamanızın **Ölçek** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="7be11-702">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="7be11-703">**Kapasite** bölümünde, grafikte yeni bir örneğin otomatik olarak dağıtıldığını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7be11-703">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![Yeni örnek otomatik olarak dağıtıldı](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="7be11-705">*Yeni örnek otomatik olarak dağıtıldı*</span><span class="sxs-lookup"><span data-stu-id="7be11-705">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7be11-706">Değişikliklerin grafikte görünmesi birkaç dakika sürebilir (sayfayı yenilemek için **CTRL + F5** tuşlarına basın).</span><span class="sxs-lookup"><span data-stu-id="7be11-706">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="7be11-707">Herhangi bir değişiklik görmüyorsanız, aşağıdakileri deneyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7be11-707">If you do not see any changes, you can try the following:</span></span>
    >
    > - <span data-ttu-id="7be11-708">Yük testinin süresini artırın (ör. **10 dakika**)</span><span class="sxs-lookup"><span data-stu-id="7be11-708">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="7be11-709">Web uygulamanızın otomatik ölçeklendirme yapılandırmasındaki **hedef CPU** aralığının maksimum ve en düşük değerlerini azaltın</span><span class="sxs-lookup"><span data-stu-id="7be11-709">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="7be11-710">Yük testini bulutta **Azure test Plans**ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7be11-710">Run the load test in the cloud with **Azure Test Plans**.</span></span> <span data-ttu-id="7be11-711">[Buradan](/azure/devops/test/load-test/index?view=vsts) daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="7be11-711">More information [here](/azure/devops/test/load-test/index?view=vsts)</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="7be11-712">Özet</span><span class="sxs-lookup"><span data-stu-id="7be11-712">Summary</span></span>

<span data-ttu-id="7be11-713">Bu uygulamalı laboratuvarda, uygulamanızı ayarlamayı ve Azure 'da üretim Web uygulamalarına dağıtmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-713">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="7be11-714">**Entity Framework Code First Migrations**kullanarak veritabanlarınızı algılayıp güncelleştirerek ve sonra **Git** kullanarak sitenizin yeni sürümlerini dağıtarak ve sitenizin en son kararlı sürümüne geri dönme gerçekleştirerek çalışmaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-714">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="7be11-715">Ayrıca, statik içeriğinizi bir blob kapsayıcısına taşımak için depolamayı kullanarak uygulamanızı nasıl ölçeklendirebileceğinizi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="7be11-715">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
