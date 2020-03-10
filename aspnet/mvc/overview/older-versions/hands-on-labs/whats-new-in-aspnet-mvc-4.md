---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4 sürümündeki yenilikler | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4, iyi kurulan tasarım düzenlerini ve ASP.NET ve... gücünü kullanarak ölçeklenebilir, standartlara dayalı Web uygulamaları oluşturmaya yönelik bir çerçevedir.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539440"
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="e952a-103">ASP.NET MVC 4 Sürümündeki Yenilikler</span><span class="sxs-lookup"><span data-stu-id="e952a-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="e952a-104">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="e952a-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="e952a-105">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="e952a-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="e952a-106">ASP.NET MVC 4, iyi kurulan tasarım düzenlerini ve ASP.NET ve .NET Framework 'ün gücünü kullanarak ölçeklenebilir, standartlara dayalı Web uygulamaları oluşturmaya yönelik bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="e952a-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="e952a-107">Framework 'ün bu yeni, dördüncü sürümü mobil Web uygulaması geliştirmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e952a-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="e952a-108">İle başlamak için yeni bir ASP.NET MVC 4 projesi oluşturduğunuzda artık mobil cihazlara özel olarak tek başına uygulama oluşturmak için kullanabileceğiniz bir mobil uygulama proje şablonu vardır.</span><span class="sxs-lookup"><span data-stu-id="e952a-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="e952a-109">Ayrıca, ASP.NET MVC 4, jQuery. Mobile. MVC NuGet paketi aracılığıyla jQuery Mobile ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="e952a-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="e952a-110">jQuery Mobile, Windows Phone, iPhone, Android vb. dahil olmak üzere tüm popüler mobil cihaz platformlarıyla uyumlu Web uygulamaları geliştirmeye yönelik HTML5 tabanlı bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="e952a-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="e952a-111">Ancak, özelleştirmeye ihtiyacınız varsa, ASP.NET MVC 4 farklı cihazlar için farklı görünümlere sunmanızı ve cihaza özgü iyileştirmeler sağlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="e952a-112">Bu uygulamalı laboratuvarda, bir fotoğraf galerisi uygulaması oluşturmak için ASP.NET MVC 4 &quot;Internet uygulaması&quot; proje şablonuyla başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="e952a-113">Farklı mobil cihazlarla ve Masaüstü Web tarayıcılarıyla uyumlu hale getirmek için jQuery Mobile ve ASP.NET MVC 4 ' ün yeni özelliklerini kullanarak uygulamayı aşamalı olarak geliştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="e952a-114">Ayrıca, kod oluşturma için yeni kod tariflerini ve ASP.NET MVC 4 ' nın görevi&lt;ActionResult&gt; dönüş türlerini destekleyerek zaman uyumsuz eylem yöntemleri yazmanızı nasıl kolaylaştıracağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="e952a-115">Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit sürümlerinde](https://aka.ms/webcamps-training-kit)kullanılabilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="e952a-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="e952a-116">Bu laboratuvara özgü proje, [ASP.NET 4,5 '](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)deki yenilikleri Web Forms.</span><span class="sxs-lookup"><span data-stu-id="e952a-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="e952a-117">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="e952a-117">Objectives</span></span>

<span data-ttu-id="e952a-118">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="e952a-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="e952a-119">Yeni mobil uygulama projesi şablonu dahil olmak üzere, ASP.NET MVC proje şablonlarına yönelik geliştirmelerden yararlanın</span><span class="sxs-lookup"><span data-stu-id="e952a-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="e952a-120">Mobil cihazlarda ekranı geliştirmek için HTML5 Görünüm penceresi özniteliğini ve CSS medya sorgularını kullanın</span><span class="sxs-lookup"><span data-stu-id="e952a-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="e952a-121">Aşamalı geliştirmeler ve dokunarak iyileştirilmiş Web Kullanıcı arabirimi oluşturmak için jQuery Mobile kullanın</span><span class="sxs-lookup"><span data-stu-id="e952a-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="e952a-122">Mobil 'e özgü görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-122">Create mobile-specific views</span></span>
- <span data-ttu-id="e952a-123">Uygulamadaki mobil ve Masaüstü görünümleri arasında geçiş yapmak için View-değiştirici bileşenini kullanın</span><span class="sxs-lookup"><span data-stu-id="e952a-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="e952a-124">Görev desteğini kullanarak zaman uyumsuz denetleyiciler oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="e952a-125">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e952a-125">Prerequisites</span></span>

<span data-ttu-id="e952a-126">Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e952a-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="e952a-127">[Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek B](#AppendixB) 'yi okuyun).</span><span class="sxs-lookup"><span data-stu-id="e952a-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="e952a-128">[ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 yüklemesinde bulunur)</span><span class="sxs-lookup"><span data-stu-id="e952a-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="e952a-129">Windows Phone öykünücü ( [Windows Phone 7.1.1 SDK 'ya](https://www.microsoft.com/download/details.aspx?id=29233)dahil)</span><span class="sxs-lookup"><span data-stu-id="e952a-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="e952a-130">**Elektrik Plum IPhone simülatörü** ile isteğe bağlı- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) (yalnızca bir iPhone simülatörü ile Web uygulamasına gözatarken kullanılan alıştırma 3 için)</span><span class="sxs-lookup"><span data-stu-id="e952a-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="e952a-131">Kurulum</span><span class="sxs-lookup"><span data-stu-id="e952a-131">Setup</span></span>

<span data-ttu-id="e952a-132">Laboratuvar belgesi boyunca kod blokları eklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="e952a-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="e952a-133">Kolaylık olması için bu kodun çoğu, Visual Studio içinden kullanarak el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio Code kod parçacıkları olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e952a-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="e952a-134">Kod parçacıklarını yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="e952a-134">To install the code snippets:</span></span>

1. <span data-ttu-id="e952a-135">Bir Windows Explorer penceresi açın ve laboratuvarın **Source\setup** klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="e952a-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="e952a-136">Visual Studio kod parçacıklarını yüklemek için bu klasördeki **Setup. cmd** dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="e952a-137">Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek istiyorsanız, [Ek A: Ek A: kod parçacıkları&quot;kullanarak](#AppendixA) bu &quot;belgedeki eke başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="e952a-138">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="e952a-138">Exercises</span></span>

<span data-ttu-id="e952a-139">Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:</span><span class="sxs-lookup"><span data-stu-id="e952a-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="e952a-140">Yeni ASP.NET MVC 4 proje şablonları</span><span class="sxs-lookup"><span data-stu-id="e952a-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="e952a-141">Fotoğraf Galerisi Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="e952a-142">Mobil cihazlar için destek ekleme</span><span class="sxs-lookup"><span data-stu-id="e952a-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="e952a-143">Zaman uyumsuz denetleyicileri kullanma</span><span class="sxs-lookup"><span data-stu-id="e952a-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="e952a-144">Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="e952a-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="e952a-145">Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="e952a-146">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.</span><span class="sxs-lookup"><span data-stu-id="e952a-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="e952a-147">Alıştırma 1: yeni ASP.NET MVC 4 proje şablonları</span><span class="sxs-lookup"><span data-stu-id="e952a-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="e952a-148">Bu alıştırmada, ASP.NET MVC 4 proje şablonlarındaki geliştirmeleri araştıracaktır.</span><span class="sxs-lookup"><span data-stu-id="e952a-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="e952a-149">MVC 3 ' te zaten bulunan Internet uygulaması şablonuna ek olarak, bu sürüm artık mobil uygulamalar için ayrı bir şablon içerir.</span><span class="sxs-lookup"><span data-stu-id="e952a-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="e952a-150">İlk olarak, her bir şablonun ilgili bazı özelliklerine bakacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="e952a-151">Ardından, doğru yaklaşımı kullanarak, farklı platformlarda sayfanızı doğru bir şekilde işlemeye çalışmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="e952a-152">Görev 1-Internet uygulaması şablonunu keşfetme</span><span class="sxs-lookup"><span data-stu-id="e952a-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="e952a-153">**Visual Studio 'yu**açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="e952a-154">Dosyayı seçin **| Yeni | Proje** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="e952a-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="e952a-155">**Yeni proje** Iletişim kutusunda **görseli C# seçin |** Sol bölme ağacındaki Web şablonu ve **ASP.NET MVC 4 Web uygulaması** ' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="e952a-156">Projeyi **Photogallery**olarak adlandırın, bir konum seçin (veya varsayılanı bırakın) ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-157">Şimdi oluşturduğunuz PhotoGallery ASP.NET MVC 4 çözümünü daha sonra özelleştirecek.</span><span class="sxs-lookup"><span data-stu-id="e952a-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="e952a-158">![Yeni bir proje oluşturma](whats-new-in-aspnet-mvc-4/_static/image1.png "Yeni proje oluşturma")</span><span class="sxs-lookup"><span data-stu-id="e952a-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="e952a-159">*Yeni bir proje oluşturma*</span><span class="sxs-lookup"><span data-stu-id="e952a-159">*Creating a new project*</span></span>
3. <span data-ttu-id="e952a-160">**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** proje şablonunu seçin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="e952a-161">Görünüm altyapısı olarak Razor seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e952a-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="e952a-162">![Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma](whats-new-in-aspnet-mvc-4/_static/image2.png "Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma")</span><span class="sxs-lookup"><span data-stu-id="e952a-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="e952a-163">*Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma*</span><span class="sxs-lookup"><span data-stu-id="e952a-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-164">Razor söz dizimi, ASP.NET MVC 3 ' te tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e952a-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="e952a-165">Amacı, bir dosyada gereken karakter ve tuş vuruşlarının sayısını en aza indirmektir ve hızlı ve akıcı bir kodlama iş akışını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="e952a-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="e952a-166">Razor, mevcut C# /vb (veya diğer) dil becerilerini kullanır ve harıka bir HTML oluşturma iş akışı sağlayan bir şablon biçimlendirme sözdizimi sunar.</span><span class="sxs-lookup"><span data-stu-id="e952a-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="e952a-167">**F5** tuşuna basarak çözümü çalıştırın ve yenilenen şablonları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="e952a-168">Aşağıdaki özelliklere bakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e952a-168">You can check out the following features:</span></span>

    <span data-ttu-id="e952a-169">**Modern stil şablonları**</span><span class="sxs-lookup"><span data-stu-id="e952a-169">**Modern-style templates**</span></span>

    <span data-ttu-id="e952a-170">Şablonlar, daha modern görünümlü daha fazla stil sunarak yenilendi.</span><span class="sxs-lookup"><span data-stu-id="e952a-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="e952a-171">![ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 yeniden biçimlendirilmiş Şablonlar")</span><span class="sxs-lookup"><span data-stu-id="e952a-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="e952a-172">*ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar*</span><span class="sxs-lookup"><span data-stu-id="e952a-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="e952a-173">![Yeni kişi sayfası](whats-new-in-aspnet-mvc-4/_static/image4.png "Yeni kişi sayfası")</span><span class="sxs-lookup"><span data-stu-id="e952a-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="e952a-174">*Yeni kişi sayfası*</span><span class="sxs-lookup"><span data-stu-id="e952a-174">*New Contact page*</span></span>

    <span data-ttu-id="e952a-175">**Uyarlamalı Işleme**</span><span class="sxs-lookup"><span data-stu-id="e952a-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="e952a-176">Tarayıcı penceresini yeniden boyutlandırın ve sayfa düzeninin yeni pencere boyutuna dinamik olarak nasıl uyum sağlayadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="e952a-177">Bu şablonlar, hiçbir özelleştirme yapmadan hem masaüstü hem de mobil platformlarda düzgün şekilde işlemek için uyarlamalı işleme tekniğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e952a-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="e952a-178">![Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu](whats-new-in-aspnet-mvc-4/_static/image5.png "Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu")</span><span class="sxs-lookup"><span data-stu-id="e952a-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="e952a-179">*Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu*</span><span class="sxs-lookup"><span data-stu-id="e952a-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="e952a-180">**JavaScript ile daha zengin Kullanıcı arabirimi**</span><span class="sxs-lookup"><span data-stu-id="e952a-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="e952a-181">Varsayılan proje şablonlarına yönelik başka bir geliştirme, JavaScript 'in daha etkileşimli bir JavaScript sağlamak için kullanılması.</span><span class="sxs-lookup"><span data-stu-id="e952a-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="e952a-182">Şablonda kullanılan oturum açma ve kayıt bağlantıları, giriş alanlarını istemci tarafında doğrulamak için jQuery doğrulamalarının nasıl kullanılacağını muaf tutma.</span><span class="sxs-lookup"><span data-stu-id="e952a-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery doğrulaması](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="e952a-184">*jQuery doğrulaması*</span><span class="sxs-lookup"><span data-stu-id="e952a-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-185">İki günlük bölümünde, ilk bölümde siteden kayıtlı bir hesap kullanarak oturum açabildiğiniz ikinci bölümde başka bir şekilde Google (varsayılan olarak devre dışı) gibi başka bir kimlik doğrulama hizmetini kullanarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-185">Notice the two log in sections, in the first section you can log in using a registered account from the site and in the second section you can alternatively log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="e952a-186">Hata ayıklayıcıyı durdurmak ve Visual Studio 'ya dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="e952a-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="e952a-187">**Uygulama\_başlangıç** klasörü altında bulunan **AuthConfig.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="e952a-188">*OAuth* kimlik doğrulaması için Google Client 'ı kaydetmek üzere son satırdaki yorumu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e952a-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > <span data-ttu-id="e952a-189">Facebook, Twitter, Microsoft vb. gibi herhangi bir OpenID veya OAuth hizmetini kullanarak kimlik doğrulamasını kolayca etkinleştirebildiğinize dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-189">Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.</span></span>
8. <span data-ttu-id="e952a-190">**F5** tuşuna basarak çözümü çalıştırın ve oturum açma sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="e952a-190">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="e952a-191">Oturum açmak için **Google** hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-191">Select **Google** service to log in.</span></span>

    ![Günlüğü hizmette seçme](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="e952a-193">*Günlüğü hizmette seçme*</span><span class="sxs-lookup"><span data-stu-id="e952a-193">*Selecting the log in service*</span></span>
10. <span data-ttu-id="e952a-194">Google hesabınızı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-194">Log in using your Google account.</span></span>
11. <span data-ttu-id="e952a-195">Sitenin (localhost) Google hesabından bilgi almasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="e952a-195">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="e952a-196">Son olarak, Google hesabını ilişkilendirmek için sitesine kaydolmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-196">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![Google hesabınızı ilişkilendirin](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="e952a-198">*Google hesabınızı ilişkilendirme*</span><span class="sxs-lookup"><span data-stu-id="e952a-198">*Associating your Google account*</span></span>
13. <span data-ttu-id="e952a-199">Hata ayıklayıcıyı durdurmak ve Visual Studio 'ya dönmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="e952a-199">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="e952a-200">Şimdi, ASP.NET MVC 4 tarafından sunulan diğer yeni özellikleri proje şablonunda görmek için çözümü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-200">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="e952a-201">![ASP.NET MVC 4 Internet uygulaması proje şablonu](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 Internet uygulaması proje şablonu")</span><span class="sxs-lookup"><span data-stu-id="e952a-201">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="e952a-202">*ASP.NET MVC 4 Internet uygulaması proje şablonu*</span><span class="sxs-lookup"><span data-stu-id="e952a-202">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

    - <span data-ttu-id="e952a-203">**HTML 5 biçimlendirmesi**</span><span class="sxs-lookup"><span data-stu-id="e952a-203">**HTML 5 Markup**</span></span>

       <span data-ttu-id="e952a-204">Yeni Tema işaretlemesini bulmak için şablon görünümlerine gözatamazsınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-204">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="e952a-205">![. Cshtml hakkında Razor ve HTML5 biçimlendirmesi kullanan yeni şablon.](whats-new-in-aspnet-mvc-4/_static/image10.png ". Cshtml hakkında Razor ve HTML5 biçimlendirmesi kullanan yeni şablon.")</span><span class="sxs-lookup"><span data-stu-id="e952a-205">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="e952a-206">*Razor ve HTML5 işaretlemesi (About. cshtml) kullanarak yeni şablon.*</span><span class="sxs-lookup"><span data-stu-id="e952a-206">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
    - <span data-ttu-id="e952a-207">**Güncelleştirilmiş JavaScript kitaplıkları**</span><span class="sxs-lookup"><span data-stu-id="e952a-207">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="e952a-208">ASP.NET MVC 4 varsayılan şablonu artık JavaScript ve HTML kullanarak zengin ve yüksek oranda yanıt veren Web uygulamaları oluşturmanıza olanak tanıyan bir JavaScript MVVM çerçevesi olan altını gizleme özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="e952a-208">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="e952a-209">MVC3 gibi, jQuery ve jQuery kullanıcı arabirimi kitaplıkları da ASP.NET MVC 4 ' de bulunur.</span><span class="sxs-lookup"><span data-stu-id="e952a-209">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="e952a-210">Bu bağlantıdaki altını gizleme ( [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)) kitaplığı hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-210">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="e952a-211">Ayrıca, [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)' de jQuery ve jQuery kullanıcı arabirimi hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-211">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="e952a-212">Görev 2-mobil uygulama şablonunu keşfetme</span><span class="sxs-lookup"><span data-stu-id="e952a-212">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="e952a-213">ASP.NET MVC 4, mobil ve tablet tarayıcılarına yönelik Web sitelerinin geliştirilmesini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e952a-213">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="e952a-214">Bu şablon, Internet uygulama şablonuyla aynı uygulama yapısına sahiptir (denetleyici kodunun neredeyse aynı olduğuna dikkat edin), ancak stili dokunmatik tabanlı mobil cihazlarda düzgün şekilde işlenecek şekilde değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e952a-214">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="e952a-215">Dosyayı seçin **| Yeni | Proje** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="e952a-215">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="e952a-216">**Yeni proje** Iletişim kutusunda **görseli C# seçin |** Sol bölme ağacındaki Web şablonu ve **ASP.NET MVC 4 Web uygulamasını seçin.**</span><span class="sxs-lookup"><span data-stu-id="e952a-216">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="e952a-217">Projeyi **Photogallery. Mobile**olarak adlandırın, bir konum seçin (ya da varsayılan olarak bırakın) &quot;çözüme Ekle&quot; ' i seçin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-217">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="e952a-218">**Yeni ASP.NET MVC 4 projesi** iletişim kutusunda, **mobil uygulama** proje şablonunu seçin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-218">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="e952a-219">Görünüm altyapısı olarak Razor seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e952a-219">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="e952a-220">![Yeni bir ASP.NET MVC 4 mobil uygulaması oluşturma](whats-new-in-aspnet-mvc-4/_static/image11.png "Yeni bir ASP.NET MVC 4 mobil uygulaması oluşturma")</span><span class="sxs-lookup"><span data-stu-id="e952a-220">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="e952a-221">*Yeni bir ASP.NET MVC 4 mobil uygulaması oluşturma*</span><span class="sxs-lookup"><span data-stu-id="e952a-221">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="e952a-222">Artık çözümü keşfedebiliyor ve mobil için ASP.NET MVC 4 çözüm şablonu tarafından sunulan yeni özelliklerden bazılarını kullanıma sunabileceksiniz:</span><span class="sxs-lookup"><span data-stu-id="e952a-222">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="e952a-223">**jQuery mobil kitaplığı**</span><span class="sxs-lookup"><span data-stu-id="e952a-223">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="e952a-224">Mobil uygulama projesi şablonu, mobil tarayıcı uyumluluğuna yönelik açık bir kaynak kitaplığı olan jQuery mobil kitaplığını içerir.</span><span class="sxs-lookup"><span data-stu-id="e952a-224">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="e952a-225">jQuery Mobile, CSS ve JavaScript 'i destekleyen mobil tarayıcılara aşamalı geliştirme uygular.</span><span class="sxs-lookup"><span data-stu-id="e952a-225">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="e952a-226">Aşamalı geliştirme tüm tarayıcıların bir Web sayfasının temel içeriğini görüntülemesini sağlar, ancak yalnızca en güçlü tarayıcıların zengin içeriği görüntülemesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-226">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="e952a-227">JQuery Mobile stilinde bulunan JavaScript ve CSS dosyaları, mobil tarayıcıların sayfa biçimlendirmesinde herhangi bir değişiklik yapmadan ekrandaki içeriğe sığması için yardım sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-227">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="e952a-229">*şablona dahil olan jQuery mobil kitaplığı*</span><span class="sxs-lookup"><span data-stu-id="e952a-229">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="e952a-230">**HTML5 tabanlı biçimlendirme**</span><span class="sxs-lookup"><span data-stu-id="e952a-230">**HTML5 based markup**</span></span>

        ![Mobil-uygulama-şablon--HTML5-işaretleme kullanma](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="e952a-232">*HTML5 işaretlemesini kullanan mobil uygulama şablonu (login. cshtml ve index. cshtml)*</span><span class="sxs-lookup"><span data-stu-id="e952a-232">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="e952a-233">Çözümü çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-233">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="e952a-234">**Windows Phone 7 öykünücüsünü**açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-234">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="e952a-235">Telefon başlangıç ekranında Internet Explorer ' ı açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-235">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="e952a-236">Masaüstü uygulamasının başlatıldığı URL 'yi gözden geçirin ve telefondan bu URL 'ye göz atın (örneğin, `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="e952a-236">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="e952a-237">Artık oturum açma sayfasını girebilir veya hakkında sayfasına bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-237">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="e952a-238">Web sitesinin stili, mobil için yeni metro uygulamasını temel alır.</span><span class="sxs-lookup"><span data-stu-id="e952a-238">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="e952a-239">ASP.NET MVC 4 proje şablonu mobil cihazlarda doğru şekilde görüntülenirken sayfanın tüm öğelerinin görünür ve etkin olmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-239">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="e952a-240">Başlıktaki bağlantıların tıklanabileceği veya dokunacak kadar büyük olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-240">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="e952a-241">![Mobil cihazdaki proje şablonu sayfaları](whats-new-in-aspnet-mvc-4/_static/image14.png "Mobil cihazdaki proje şablonu sayfaları")</span><span class="sxs-lookup"><span data-stu-id="e952a-241">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="e952a-242">*Mobil cihazdaki proje şablonu sayfaları*</span><span class="sxs-lookup"><span data-stu-id="e952a-242">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="e952a-243">Yeni şablon **Görünüm penceresi meta etiketini**de kullanır.</span><span class="sxs-lookup"><span data-stu-id="e952a-243">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="e952a-244">Çoğu mobil tarayıcı, mobil cihazın gerçek genişliğinden daha büyük olan bir sanal tarayıcı penceresi veya &quot;Görünüm penceresi&quot;için bir genişlik tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-244">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="e952a-245">Bu, mobil tarayıcıların tüm Web sayfasını sanal görüntü içinde görüntülemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-245">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="e952a-246">**Görünüm penceresi meta etiketi** , Web geliştiricilerinin mobil cihazlarda tarayıcı alanının genişliğini, yüksekliğini ve ölçeğini ayarlamasına olanak tanır **.**</span><span class="sxs-lookup"><span data-stu-id="e952a-246">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="e952a-247">Mobil uygulamalar için ASP.NET MVC 4 şablonu, görünüm penceresinin Görünüm penceresi, cihaz ekranı genişliğine ayarlanmış olacak şekilde Düzen *\_* şablonunda (&quot;Width = cihaz-Width&quot;) Görünüm penceresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-247">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="e952a-248">Görünüm penceresi meta etiketinin varsayılan tarayıcı görünümünü değiştirmediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-248">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="e952a-249">Görünümlerde bulunan **\_Layout. cshtml**dosyasını açın **| Paylaşılan** klasör ve Görünüm penceresi meta etiketini açıklama.</span><span class="sxs-lookup"><span data-stu-id="e952a-249">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="e952a-250">Zaten açılmadıysa uygulamayı çalıştırın ve farklılıkları inceleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-250">Run the application, if not already opened, and check out the differences.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

<span data-ttu-id="e952a-251">![Görünüm penceresi meta etiketini açıklama ekleyerek site](whats-new-in-aspnet-mvc-4/_static/image15.png "Görünüm penceresi meta etiketini açıklama ekleyerek site")</span><span class="sxs-lookup"><span data-stu-id="e952a-251">![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")</span></span>

<span data-ttu-id="e952a-252">*Görünüm penceresi meta etiketini açıklama ekleyerek site*</span><span class="sxs-lookup"><span data-stu-id="e952a-252">*The site after commenting the viewport meta tag*</span></span>
10. <span data-ttu-id="e952a-253">Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-253">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="e952a-254">Görünüm penceresi meta etiketinin açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e952a-254">Uncomment the viewport meta tag.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="e952a-255">Görev 3-Uyarlamalı Işleme kullanma</span><span class="sxs-lookup"><span data-stu-id="e952a-255">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="e952a-256">Bu görevde, bir Web sayfasını herhangi bir özelleştirme olmadan aynı anda mobil cihazlarda ve Web tarayıcılarında doğru bir şekilde işlemek için başka bir yöntem öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-256">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="e952a-257">Zaten benzer bir amaçla Görünüm penceresi meta etiketi kullandınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-257">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="e952a-258">Artık başka bir güçlü yöntemi karşılamanız gerekir: *Uyarlamalı işleme*.</span><span class="sxs-lookup"><span data-stu-id="e952a-258">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="e952a-259">Uyarlamalı işleme, bir sayfaya uygulanan stili özelleştirmek için **CSS3 medya sorguları** kullanan bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="e952a-259">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="e952a-260">Medya sorguları, bir stil sayfası içindeki koşulları tanımlar ve belirli bir koşulun altına CSS stillerini gruplandırarak.</span><span class="sxs-lookup"><span data-stu-id="e952a-260">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="e952a-261">Yalnızca koşul true olduğunda, stil, belirtilen nesnelere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e952a-261">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="e952a-262">Uyarlamalı işleme tekniği tarafından sağlanan esneklik, siteyi farklı cihazlarda görüntülemek için herhangi bir özelleştirmeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-262">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="e952a-263">Stili seçmek için mantıksal kod yazmadan tek bir stil sayfasında istediğiniz kadar stil tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-263">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="e952a-264">Bu nedenle, sayfa stillerinin uyarlanmasıyla ilgili olarak, yinelenen kod miktarını ve işleme amaçları için mantığı azaltır.</span><span class="sxs-lookup"><span data-stu-id="e952a-264">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="e952a-265">Öte yandan, CSS dosyalarınızın boyutu büyük ölçüde büyürken bant genişliği tüketimi artar.</span><span class="sxs-lookup"><span data-stu-id="e952a-265">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="e952a-266">Uyarlamalı işleme tekniğini kullanarak, **Tarayıcınız ne olursa olsun siteniz düzgün şekilde görüntülenecektir.**</span><span class="sxs-lookup"><span data-stu-id="e952a-266">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="e952a-267">Ancak, bant genişliği ekstra yükünün bir sorun olup olmadığını göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-267">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="e952a-268">Bir medya sorgusunun temel biçimi: @media \[kapsamı: ALL | Avuçiçi | Yazdır | projeksiyon | ekran\] ([özellik: değer] ve... [özellik: değer])</span><span class="sxs-lookup"><span data-stu-id="e952a-268">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>

<span data-ttu-id="e952a-269">Medya sorgularının örnekleri: &gt; **@media All ve (max-width: 1000px) ve (min-width: 700px) {}:** 700px ve 1000px tüm çözünürlükler için.</span><span class="sxs-lookup"><span data-stu-id="e952a-269">Examples of media queries: &gt;**@media all and (max-width: 1000px) and (min-width: 700px) {}:** For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="e952a-270">**@media Screen ve (min-width: 400px) ve (max-width: 700px) {...}:** Yalnızca ekranlar için.</span><span class="sxs-lookup"><span data-stu-id="e952a-270">**@media screen and (min-width: 400px) and (max-width: 700px) { ... }:** Only for screens.</span></span> <span data-ttu-id="e952a-271">Çözüm 400 ile 700px arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e952a-271">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="e952a-272">**@media Portatif ve (min-width: 20em), ekran ve (min-width: 20em) {...}:** Avuçiçi bilgisayarlar (mobil ve cihazlar) ve ekranlar için.</span><span class="sxs-lookup"><span data-stu-id="e952a-272">**@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:** For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="e952a-273">En küçük genişlik 20em 'den büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e952a-273">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="e952a-274">Bu konuda, [W3C sitesinde](http://www.w3.org/TR/css3-mediaqueries/)hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-274">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>

<span data-ttu-id="e952a-275">Artık, ASP.NET MVC 4 varsayılan Web sitesi şablonunun okunabilirliğini iyileştirmek için uyarlamalı işlemenin nasıl çalıştığını araştıracaktır.</span><span class="sxs-lookup"><span data-stu-id="e952a-275">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="e952a-276">Görev 1 ' de oluşturduğunuz **Photogallery. sln** çözümünü açın ve **Photogallery** projesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-276">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="e952a-277">Çözümü çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-277">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="e952a-278">Tarayıcının genişliğini yeniden boyutlandırın, pencereleri yarı veya orijinal boyutunun bir çeyreğinin bir çeyrekten daha az olacak şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-278">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="e952a-279">Başlıktaki öğelerle ne olduğunu fark edin: bazı öğeler üstbilginin görünür alanında görünmez.</span><span class="sxs-lookup"><span data-stu-id="e952a-279">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="e952a-280">**İçerik** proje klasöründe bulunan Visual Studio Çözüm Gezgini 'nden **site. css** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-280">Open **Site.css** file from the Visual Studio Solution explorer, located in **Content** project folder.</span></span> <span data-ttu-id="e952a-281">Visual Studio tümleşik arama 'yı açmak için **CTRL + F** tuşlarına basın ve **CSS medya sorgusunu**bulmak için `@media` yazın.</span><span class="sxs-lookup"><span data-stu-id="e952a-281">Press **CTRL + F** to open Visual Studio integrated search, and write `@media` to locate the **CSS media query**.</span></span>

    <span data-ttu-id="e952a-282">Bu şablonda tanımlanan medya sorgusu koşulu şu şekilde çalışıyor: tarayıcının pencere boyutu **850 px**altındaysa, uygulanan CSS kuralları bu medya bloğunda tanımlananlardır.</span><span class="sxs-lookup"><span data-stu-id="e952a-282">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="e952a-283">![Medya sorgusu bulunuyor](whats-new-in-aspnet-mvc-4/_static/image16.png "Medya sorgusu bulunuyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-283">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="e952a-284">*Medya sorgusu bulunuyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-284">*Locating the media query*</span></span>
4. <span data-ttu-id="e952a-285">Uyarlamalı işlemeyi devre dışı bırakmak için 850 piksel olarak ayarlanan max-width öznitelik değerini **10**piksel ile değiştirin ve değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-285">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="e952a-286">Tarayıcıya dönün ve yaptığınız değişikliklerle sayfayı yenilemek için **CTRL + F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-286">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="e952a-287">Pencerenin genişliğini ayarlarken her iki sayfada da farklılıklara dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-287">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="e952a-288">![Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır](whats-new-in-aspnet-mvc-4/_static/image17.png "Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır")</span><span class="sxs-lookup"><span data-stu-id="e952a-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="e952a-289">*Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır*</span><span class="sxs-lookup"><span data-stu-id="e952a-289">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="e952a-290">Şimdi mobil cihazlarda neler olduğunu göz atalım:</span><span class="sxs-lookup"><span data-stu-id="e952a-290">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="e952a-291">![Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır](whats-new-in-aspnet-mvc-4/_static/image18.png "Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır")</span><span class="sxs-lookup"><span data-stu-id="e952a-291">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="e952a-292">*Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır*</span><span class="sxs-lookup"><span data-stu-id="e952a-292">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="e952a-293">Sayfa bir Web tarayıcısında işlendiğinde yapılan değişikliklerin çok önemli olmadığına fark edilse de, bir mobil cihaz kullanırken farklar daha belirgin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="e952a-293">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="e952a-294">Görüntünün sol tarafında, özel stilin okunabilirliğini iyileştirildiğini görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="e952a-294">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="e952a-295">Uyarlamalı işleme, bir Web sitesine koşullu stil uygulamayı ve bir düzenlidir yaklaşımıyla ortak stil sorunlarını çözmeye daha kolay hale getirmek için birçok daha fazla senaryoda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e952a-295">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="e952a-296">Görünüm penceresi meta etiketi ve CSS medya sorguları ASP.NET MVC 4 ' e özgü değildir, bu sayede herhangi bir Web uygulamasında bu özelliklerden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-296">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="e952a-297">Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-297">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="e952a-298">Alıştırma 2: Fotoğraf Galerisi Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-298">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="e952a-299">Bu alıştırmada, fotoğrafları göstermek için bir fotoğraf galerisi uygulaması üzerinde çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-299">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="e952a-300">ASP.NET MVC 4 proje şablonuyla başlayacaksınız ve sonra bir hizmetten fotoğraf alıp giriş sayfasında görüntülenecek bir özellik ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-300">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="e952a-301">Aşağıdaki alıştırmada, mobil cihazlarda görüntülenme şeklini iyileştirmek için bu çözümü güncelleştirecek olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e952a-301">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="e952a-302">Görev 1-bir sahte fotoğraf hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-302">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="e952a-303">Bu görevde, galeride görüntülenecek içeriği almak için fotoğraf hizmeti 'nin bir türünü oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-303">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="e952a-304">Bunu yapmak için, her fotoğrafın verileriyle yalnızca bir JSON dosyası döndüren yeni bir denetleyici ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-304">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="e952a-305">Henüz açılmadıysa **Visual Studio 'yu** açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-305">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="e952a-306">Dosyayı seçin **| Yeni | Proje** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="e952a-306">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="e952a-307">**Yeni proje** Iletişim kutusunda **görseli C# seçin |** Sol bölme ağacındaki Web şablonu ve **ASP.NET MVC 4 Web uygulaması** ' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-307">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="e952a-308">Projeyi **Photogallery**olarak adlandırın, bir konum seçin (veya varsayılanı bırakın) ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-308">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="e952a-309">Alternatif olarak, **alıştırma 1** ' den mevcut ASP.NET MVC 4 **Internet uygulaması** çözümünüzden çalışmaya devam edebilir ve sonraki adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-309">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="e952a-310">**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** proje şablonunu seçin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-310">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="e952a-311">Görünüm altyapısı olarak Razor seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e952a-311">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="e952a-312">**Çözüm Gezgini**, projenizin **uygulama\_veri** klasörüne sağ tıklayın ve Ekle ' yi seçin **| Mevcut öğe**.</span><span class="sxs-lookup"><span data-stu-id="e952a-312">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="e952a-313">Bu laboratuvarın **Source\assets\app\_Data** klasörüne göz atın ve **Fotoğraflar. JSON** dosyasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-313">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="e952a-314">**Photocontroller**adlı yeni bir denetleyici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e952a-314">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="e952a-315">Bunu yapmak için, **denetleyiciler** klasörüne sağ tıklayın, **Ekle** ' ye gidin ve denetleyici ' yi seçin **.**</span><span class="sxs-lookup"><span data-stu-id="e952a-315">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="e952a-316">Denetleyicinin adını doldurun, **boş MVC denetleyicisi** şablonunu bırakın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-316">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="e952a-317">![PhotoController ekleniyor](whats-new-in-aspnet-mvc-4/_static/image19.png "PhotoController ekleniyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-317">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="e952a-318">*PhotoController ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-318">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="e952a-319">**Index** metodunu aşağıdaki **Galeri** eylemiyle değiştirin ve son zamanlarda projeye eklemiş olduğunuz JSON dosyasındaki içeriği döndürün.</span><span class="sxs-lookup"><span data-stu-id="e952a-319">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="e952a-320">(Kod parçacığı- *ASP.NET MVC 4 Lab-Ex02-Gallery eylemi*)</span><span class="sxs-lookup"><span data-stu-id="e952a-320">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. <span data-ttu-id="e952a-321">Çözümü çalıştırmak için **F5** tuşuna basın ve ardından, şu URL 'ye giderek, bu çözümü test etmek IÇIN aşağıdaki URL 'ye gidin: `http://localhost:[port]/photo/gallery` ([port] değeri uygulamanın başlatıldığı geçerli bağlantı noktasına bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="e952a-321">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="e952a-322">Bu URL 'ye yönelik isteğin, **Fotoğraflar. JSON** dosyasının içeriğini alması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-322">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="e952a-323">![Moclenmiş fotoğraf hizmetini test etme](whats-new-in-aspnet-mvc-4/_static/image20.png "Moclenmiş fotoğraf hizmetini test etme")</span><span class="sxs-lookup"><span data-stu-id="e952a-323">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="e952a-324">*Moclenmiş fotoğraf hizmetini test etme*</span><span class="sxs-lookup"><span data-stu-id="e952a-324">*Testing the mocked photo service*</span></span>

<span data-ttu-id="e952a-325">Gerçek bir uygulamada, Fotoğraf Galerisi hizmetini uygulamak için [ASP.NET Web API 'sini](../../../../web-api/index.md) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-325">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="e952a-326">ASP.NET Web API; tarayıcılar ve mobil cihazlar dahil olmak üzere, geniş bir yelpazedeki istemcilere erişen HTTP hizmetlerini oluşturmayı kolaylaştıran bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="e952a-326">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="e952a-327">ASP.NET Web API; .NET Framework üzerinde RESTful uygulamaları geliştirmek için ideal bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="e952a-327">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="e952a-328">Görev 2-fotoğraf galerisini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e952a-328">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="e952a-329">Bu görevde, bu alıştırmanın ilk görevinde oluşturduğunuz moclenmiş hizmeti kullanarak fotoğraf galerisini görüntülemek için giriş sayfasını güncelleşceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-329">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="e952a-330">Model dosyaları ekleyecek ve Galeri görünümlerini güncellerimize sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e952a-330">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="e952a-331">Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-331">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="e952a-332">**Modeller** klasöründe **fotoğraf** sınıfını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e952a-332">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="e952a-333">Bunu yapmak için **modeller** klasörüne sağ tıklayın, **Ekle** ' yi seçin ve **sınıf**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-333">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="e952a-334">Ardından, adı **Photo.cs** olarak ayarlayın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-334">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="e952a-335">Aşağıdaki üyeleri **fotoğraf** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-335">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="e952a-336">(Kod parçacığı- *ASP.NET MVC 4 Lab-Ex02-Photo Model*)</span><span class="sxs-lookup"><span data-stu-id="e952a-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. <span data-ttu-id="e952a-337">**HomeController.cs** dosyasını **denetleyiciler** klasöründen açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-337">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="e952a-338">Aşağıdaki using deyimlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-338">Add the following using statements.</span></span>

    <span data-ttu-id="e952a-339">(Kod parçacığı- *ASP.NET MVC 4 laboratuvar-Ex02-HomeController kullanımlar*)</span><span class="sxs-lookup"><span data-stu-id="e952a-339">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. <span data-ttu-id="e952a-340">Galeri verilerini almak için **HttpClient** kullanmak üzere **Dizin** eylemini güncelleştirin ve ardından Görünüm modelinde kaldırmak için **JavaScriptSerializer** kullanın.</span><span class="sxs-lookup"><span data-stu-id="e952a-340">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="e952a-341">(Kod parçacığı- *ASP.NET MVC 4 laboratuvar-Ex02-Dizin eylemi*)</span><span class="sxs-lookup"><span data-stu-id="e952a-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. <span data-ttu-id="e952a-342">**Views\home** klasörünün altında bulunan **Index. cshtml** dosyasını açın ve tüm içeriği aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-342">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="e952a-343">Bu kod, hizmetten alınan tüm fotoğraflarda döngü gösterir ve sıralanmamış bir liste halinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e952a-343">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="e952a-344">(Kod parçacığı- *ASP.NET MVC 4 laboratuvar-Ex02-fotoğraf listesi*)</span><span class="sxs-lookup"><span data-stu-id="e952a-344">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. <span data-ttu-id="e952a-345">**Çözüm Gezgini**projenizin **içerik** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Mevcut öğe**.</span><span class="sxs-lookup"><span data-stu-id="e952a-345">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="e952a-346">Bu laboratuvarın **Source\assets\content** klasörüne göz atın ve **site. css** dosyasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-346">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="e952a-347">Onun yerini onaylamanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="e952a-347">You will have to confirm its replacement.</span></span> <span data-ttu-id="e952a-348">**Site. css** dosyası açıksa, dosyayı da yeniden yüklemeyi onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-348">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="e952a-349">Dosya Gezgini 'ni açın ve bu laboratuvarın **Source\varlıklar** klasörü altında bulunan tüm **Fotoğraflar** klasörünü Çözüm Gezgini ' deki projenizin kök klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-349">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="e952a-350">Uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e952a-350">Run the application.</span></span> <span data-ttu-id="e952a-351">Şimdi, galerideki fotoğrafları görüntüleyen giriş sayfasını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-351">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="e952a-352">![Fotoğraf Galerisi](whats-new-in-aspnet-mvc-4/_static/image21.png "Fotoğraf Galerisi")</span><span class="sxs-lookup"><span data-stu-id="e952a-352">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="e952a-353">*Fotoğraf Galerisi*</span><span class="sxs-lookup"><span data-stu-id="e952a-353">*Photo Gallery*</span></span>
11. <span data-ttu-id="e952a-354">Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-354">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="e952a-355">Alıştırma 3: mobil cihazlar için destek ekleme</span><span class="sxs-lookup"><span data-stu-id="e952a-355">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="e952a-356">ASP.NET MVC 4 ' teki temel güncelleştirmelerden biri, mobil geliştirme için destedir.</span><span class="sxs-lookup"><span data-stu-id="e952a-356">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="e952a-357">Bu alıştırmada, önceki alıştırmada oluşturduğunuz PhotoGallery çözümünü genişleterek mobil uygulamalar için ASP.NET MVC 4 yeni özelliklerini keşfedecektir.</span><span class="sxs-lookup"><span data-stu-id="e952a-357">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="e952a-358">Görev 1-ASP.NET MVC 4 uygulamasına jQuery Mobile yükleme</span><span class="sxs-lookup"><span data-stu-id="e952a-358">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="e952a-359">**Kaynak/Ex3-MobileSupport/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-359">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="e952a-360">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-360">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="e952a-361">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-361">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e952a-362">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-362">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e952a-363">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-363">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e952a-364">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-364">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e952a-365">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-365">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e952a-366">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-366">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e952a-367">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="e952a-367">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="e952a-368">**Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu** menü seçeneği ' ne tıklayarak **Paket Yöneticisi konsolunu** açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-368">Open the **Package Manager Console** by clicking the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="e952a-369">![NuGet Paket Yöneticisi konsolu açılıyor](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet Paket Yöneticisi konsolu açılıyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-369">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="e952a-370">*NuGet Paket Yöneticisi konsolu açılıyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-370">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="e952a-371">Paket Yöneticisi konsolunda **jQuery. Mobile. Mvc** paketini yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e952a-371">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="e952a-372">jQuery Mobile, dokunmatik iyileştirilmiş Web Kullanıcı arabirimi oluşturmaya yönelik açık kaynak bir kitaplıktır.</span><span class="sxs-lookup"><span data-stu-id="e952a-372">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="e952a-373">JQuery. Mobile. MVC NuGet paketi, ASP.NET MVC 4 uygulamasıyla jQuery Mobile kullanma yardımcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="e952a-373">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-374">Aşağıdaki komutu çalıştırarak, jQuery. Mobile. MVC kitaplığını NuGet 'den indirilecektir.</span><span class="sxs-lookup"><span data-stu-id="e952a-374">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="e952a-375">PM</span><span class="sxs-lookup"><span data-stu-id="e952a-375">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="e952a-376">Bu komut, jQuery Mobile ve bazı yardımcı dosyalarını aşağıdakiler de dahil olmak üzere kurar:</span><span class="sxs-lookup"><span data-stu-id="e952a-376">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="e952a-377">**Görünümler/paylaşılan/\_Layout. Mobile. cshtml**: daha küçük bir ekran Için Iyileştirilmiş jQuery Mobile tabanlı bir düzen.</span><span class="sxs-lookup"><span data-stu-id="e952a-377">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="e952a-378">Web sitesi bir mobil tarayıcıdan istek aldığında, özgün düzen (\_Layout. cshtml) bu ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="e952a-378">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="e952a-379">Bir görünüm-değiştirici bileşeni: **Görünümler/paylaşılan/\_Viewdeğiştirici. cshtml** kısmi görünümden ve **ViewSwitcherController.cs** denetleyicisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="e952a-379">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="e952a-380">Bu bileşen, kullanıcıların sayfanın masaüstü sürümüne geçiş kurmasını sağlamak için mobil tarayıcılarda bir bağlantı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e952a-380">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="e952a-381">![Mobil desteğe sahip Fotoğraf Galerisi projesi](whats-new-in-aspnet-mvc-4/_static/image23.png "Mobil desteğe sahip Fotoğraf Galerisi projesi")</span><span class="sxs-lookup"><span data-stu-id="e952a-381">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="e952a-382">*Mobil desteğe sahip Fotoğraf Galerisi projesi*</span><span class="sxs-lookup"><span data-stu-id="e952a-382">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="e952a-383">Mobil paketleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e952a-383">Register the Mobile bundles.</span></span> <span data-ttu-id="e952a-384">Bunu yapmak için, **Global.asax.cs** dosyasını açın ve aşağıdaki satırı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-384">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="e952a-385">(Kod parçacığı- *ASP.NET MVC 4 Lab-Ex03-mobil paketleri kaydet*)</span><span class="sxs-lookup"><span data-stu-id="e952a-385">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. <span data-ttu-id="e952a-386">Bir Masaüstü Web tarayıcısı kullanarak uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e952a-386">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="e952a-387">Başlangıç menüsünde bulunan **Windows Phone 7 öykünücüsünü** açın **| Tüm Programlar | Windows Phone SDK 7,1 | Windows Phone öykünücü.**</span><span class="sxs-lookup"><span data-stu-id="e952a-387">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="e952a-388">Telefon başlangıç ekranında Internet Explorer ' ı açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-388">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="e952a-389">Uygulamanın başlatıldığı URL 'yi inceleyin ve telefon tarayıcısıyla bu URL 'ye göz atın (örn. `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="e952a-389">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="e952a-390">JQuery. Mobile. MVC, projenizde mobil cihazlar için iyileştirilmiş görünümleri gösteren yeni varlıklar oluşturduğu için, uygulamanızın Windows Phone öykünücüsünde farklı görünmeyeceğini fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-390">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="e952a-391">Telefonun en üstünde yer alan ve Masaüstü görünümüne geçiş yapan bağlantıyı gösteren iletiyi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e952a-391">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="e952a-392">Ayrıca, yüklediğiniz paket tarafından oluşturulan **\_Layout. Mobile. cshtml** düzeni, uygulamaya farklı bir düzen de dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="e952a-392">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-393">Şimdiye kadar, mobil görünüme geri dönmek için bir bağlantı yoktur.</span><span class="sxs-lookup"><span data-stu-id="e952a-393">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="e952a-394">Daha sonraki sürümlere dahil edilecek.</span><span class="sxs-lookup"><span data-stu-id="e952a-394">It will be included in later versions.</span></span>

    <span data-ttu-id="e952a-395">![Fotoğraf Galerisi giriş sayfasının mobil görünümü](whats-new-in-aspnet-mvc-4/_static/image24.png "Fotoğraf Galerisi giriş sayfasının mobil görünümü")</span><span class="sxs-lookup"><span data-stu-id="e952a-395">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="e952a-396">*Fotoğraf Galerisi giriş sayfasının mobil görünümü*</span><span class="sxs-lookup"><span data-stu-id="e952a-396">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="e952a-397">Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-397">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="e952a-398">Görev 2-mobil görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-398">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="e952a-399">Bu görevde, mobil cihazlarda daha iyi bir görünüm için içerik uyarlanmasını içeren dizin görünümünün bir mobil sürümünü oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-399">In this task, you will create a mobile version of the index view with content adapted for better appearance in mobile devices.</span></span>

1. <span data-ttu-id="e952a-400">**Views\home\ındex.cshtml** görünümünü kopyalayın ve bir kopya oluşturmak üzere yapıştırın, yeni dosyayı **Index. Mobile. cshtml**olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e952a-400">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="e952a-401">Yeni oluşturulan **Index. Mobile. cshtml** görünümünü açın ve mevcut &lt;ul&gt; etiketini bu kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-401">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="e952a-402">Bunu yaparak jQuery 'ten mobil temaları kullanmak için jQuery Mobile Data Not &lt;ul&gt; etiketini güncelleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-402">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > <span data-ttu-id="e952a-403">Dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="e952a-403">Notice that:</span></span>
    > 
    > - <span data-ttu-id="e952a-404">**ListView** olarak ayarlanan **veri rolü** özniteliği, ListView stillerini kullanarak listeyi işler.</span><span class="sxs-lookup"><span data-stu-id="e952a-404">The **data-role** attribute set to **listview** will render the list using the listview styles.</span></span>
    > 
    > - <span data-ttu-id="e952a-405">**Data-ınmetinözniteliği** true olarak ayarlandığında, listeyi yuvarlatılmış kenarlık ve kenar boşluğu ile gösterir.</span><span class="sxs-lookup"><span data-stu-id="e952a-405">The **data-inset** attribute set to true will show the list with rounded border and margin.</span></span>
    > 
    > - <span data-ttu-id="e952a-406">**Data-Filter** özniteliği **true** olarak ayarlanan bir arama kutusu oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="e952a-406">The **data-filter** attribute set to **true** will generate a search box.</span></span>
    > 
    > <span data-ttu-id="e952a-407">Proje belgelerindeki jQuery mobil kuralları hakkında daha fazla bilgi edinebilirsiniz: [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span><span class="sxs-lookup"><span data-stu-id="e952a-407">You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span></span>
3. <span data-ttu-id="e952a-408">Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-408">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="e952a-409">**Windows Phone öykünücüye** geçin ve siteyi yenileyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-409">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="e952a-410">Galeri listesinin yeni görünümünü ve en üstte bulunan yeni arama kutusunu fark edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-410">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="e952a-411">Ardından, fotoğraf galerisinde bir arama başlatmak için arama kutusuna (örneğin, **TULIP**) bir sözcük yazın.</span><span class="sxs-lookup"><span data-stu-id="e952a-411">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="e952a-412">![Filtre ile ListView stili kullanan Galeri](whats-new-in-aspnet-mvc-4/_static/image25.png "Filtre ile ListView stili kullanan Galeri")</span><span class="sxs-lookup"><span data-stu-id="e952a-412">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="e952a-413">*Filtre ile ListView stili kullanan Galeri*</span><span class="sxs-lookup"><span data-stu-id="e952a-413">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="e952a-414">Özetlemek gerekirse, mobil&quot; sonekiyle &quot;Dizin görünümünün bir kopyasını oluşturmak için bir görünüm Oluşturucu tarifi kullandınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-414">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="e952a-415">Bu sonek, bir mobil cihazdan oluşturulan her isteğin, dizinin bu kopyasını kullanacağını ASP.NET MVC 4 ' ü gösterir.</span><span class="sxs-lookup"><span data-stu-id="e952a-415">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="e952a-416">Ayrıca, mobil cihazlarda site görünümünü geliştirmek için, Dizin görünümünün mobil sürümünü jQuery Mobile kullanacak şekilde güncelleştirmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e952a-416">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="e952a-417">Visual Studio 'ya geri dönün ve **içerik** klasörünün altında bulunan **site. Mobile. css** ' i açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-417">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="e952a-418">Resmin sağ tarafında görünmesini sağlamak için fotoğraf başlığının konumlandırılmasını düzeltir.</span><span class="sxs-lookup"><span data-stu-id="e952a-418">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="e952a-419">Bunu yapmak için, aşağıdaki kodu **site. Mobile. css** dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-419">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="e952a-420">CSS</span><span class="sxs-lookup"><span data-stu-id="e952a-420">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="e952a-421">Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-421">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="e952a-422">**Windows Phone öykünücüye** dönün ve siteyi yenileyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-422">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="e952a-423">Fotoğraf başlığının hemen düzgün şekilde konumlandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-423">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="e952a-424">![Resmin sağ tarafında konumlandırılmış başlık](whats-new-in-aspnet-mvc-4/_static/image26.png "Resmin sağ tarafında konumlandırılmış başlık")</span><span class="sxs-lookup"><span data-stu-id="e952a-424">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="e952a-425">*Resmin sağ tarafında konumlandırılmış başlık*</span><span class="sxs-lookup"><span data-stu-id="e952a-425">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="e952a-426">Görev 3-jQuery mobil temaları</span><span class="sxs-lookup"><span data-stu-id="e952a-426">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="e952a-427">JQuery Mobile 'daki her düzen ve pencere öğesi, sitelere ve uygulamalara tam bir birleştirilmiş görsel tasarım teması uygulamayı olanaklı kılan yeni bir nesne odaklı CSS çerçevesi etrafında tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e952a-427">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="e952a-428">jQuery Mobile 'ın varsayılan teması, hızlı başvuru için harfler verilen (a, b, c, d, e) 5 renk örneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="e952a-428">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="e952a-429">Bu görevde, mobil düzeni varsayılandan farklı bir tema kullanacak şekilde güncelleşitecaksınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-429">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="e952a-430">Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="e952a-430">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="e952a-431">**Views\shared**konumunda bulunan **\_Layout. Mobile. cshtml** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-431">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="e952a-432">Veri-rolü &quot;sayfa&quot; olarak ayarlanan div öğesini bulun ve **veri temasını** &quot;**e**&quot;olarak güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-432">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. <span data-ttu-id="e952a-433">Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-433">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="e952a-434">**Windows Phone öykünücüsünde** siteyi yenileyin ve yeni renkler düzenine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-434">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="e952a-435">![Farklı renk düzenine sahip mobil düzen](whats-new-in-aspnet-mvc-4/_static/image27.png "Farklı renk düzenine sahip mobil düzen")</span><span class="sxs-lookup"><span data-stu-id="e952a-435">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="e952a-436">*Farklı renk düzenine sahip mobil düzen*</span><span class="sxs-lookup"><span data-stu-id="e952a-436">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="e952a-437">Görev 4-görünüm-değiştirici bileşenini ve tarayıcı geçersiz kılma özelliklerini kullanma</span><span class="sxs-lookup"><span data-stu-id="e952a-437">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="e952a-438">Mobil olarak iyileştirilmiş Web sayfalarına yönelik bir kural, metnin masaüstü görünümü veya tam site modu gibi, kullanıcıların sayfanın masaüstü sürümüne geçmelerini sağlayan bir bağlantı eklemektir.</span><span class="sxs-lookup"><span data-stu-id="e952a-438">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="e952a-439">JQuery. Mobile. MVC paketi, bu amaç için **\_Layout. Mobile. cshtml** görünümünde kullanılan bir örnek **Görünüm-değiştirici** bileşeni içerir.</span><span class="sxs-lookup"><span data-stu-id="e952a-439">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="e952a-440">![Masaüstü görünümüne geçiş bağlantısı](whats-new-in-aspnet-mvc-4/_static/image28.png "Masaüstü görünümüne geçiş bağlantısı")</span><span class="sxs-lookup"><span data-stu-id="e952a-440">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="e952a-441">*Masaüstü görünümüne geçiş bağlantısı*</span><span class="sxs-lookup"><span data-stu-id="e952a-441">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="e952a-442">Görünüm değiştirici, **tarayıcı geçersiz kılma**adlı yeni bir özellik kullanır.</span><span class="sxs-lookup"><span data-stu-id="e952a-442">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="e952a-443">Bu özellik, uygulamanızın istekleri gerçekten geldiğini farklı bir tarayıcıdan (Kullanıcı Aracısı) geliyormuş gibi işleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-443">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="e952a-444">Bu görevde, jQuery. Mobile. MVC tarafından eklenen bir görünüm değiştiricisinden örnek uygulama ve ASP.NET MVC 4 ' teki yeni tarayıcı geçersiz kılma özellikleri araştırılacak.</span><span class="sxs-lookup"><span data-stu-id="e952a-444">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="e952a-445">Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="e952a-445">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="e952a-446">**Views\shared** klasörünün altında bulunan **\_Layout. Mobile. cshtml** görünümünü açın ve görünüm-değiştirici bileşenine kısmi bir görünüm olarak başvurulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-446">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="e952a-447">![Görünüm-değiştirici bileşeni kullanarak mobil düzen](whats-new-in-aspnet-mvc-4/_static/image29.png "Görünüm-değiştirici bileşeni kullanarak mobil düzen")</span><span class="sxs-lookup"><span data-stu-id="e952a-447">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="e952a-448">*Görünüm-değiştirici bileşeni kullanarak mobil düzen*</span><span class="sxs-lookup"><span data-stu-id="e952a-448">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="e952a-449">**\_Viewdeğiştirici. cshtml** kısmi görünümünü açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-449">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="e952a-450">Kısmi görünüm, Web isteğinin kaynağını tespit etmek ve masaüstüne ya da mobil görünümlere geçiş yapmak için karşılık gelen bağlantıyı göstermek için **ViewContext. HttpContext. GetOverriddenBrowser ()** yeni yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e952a-450">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="e952a-451">**GetOverriddenBrowser** yöntemi, istek için ayarlanmış olan kullanıcı aracısına karşılık gelen bir **HttpBrowserCapabilitiesBase** örneği döndürür (gerçek veya geçersiz kılındı).</span><span class="sxs-lookup"><span data-stu-id="e952a-451">The **GetOverriddenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="e952a-452">Bu değeri, **ımobiledevice**gibi özellikleri almak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-452">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="e952a-453">![Viewdeğiştirici kısmi görünümü](whats-new-in-aspnet-mvc-4/_static/image30.png "Viewdeğiştirici kısmi görünümü")</span><span class="sxs-lookup"><span data-stu-id="e952a-453">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="e952a-454">*Viewdeğiştirici kısmi görünümü*</span><span class="sxs-lookup"><span data-stu-id="e952a-454">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="e952a-455">**Denetleyiciler** klasöründe bulunan **ViewSwitcherController.cs** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-455">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="e952a-456">Bu SwitchView eyleminin, Viewdeğiştirici bileşenindeki bağlantı tarafından çağrıldığını ve yeni HttpContext yöntemlerine dikkat ettiğini göz atın.</span><span class="sxs-lookup"><span data-stu-id="e952a-456">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="e952a-457">**HttpContext. ClearOverriddenBrowser ()** yöntemi, geçerli istek için geçersiz kılınan Kullanıcı aracılarını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e952a-457">The **HttpContext.ClearOverriddenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="e952a-458">**HttpContext. SetOverriddenBrowser ()** yöntemi, belirtilen Kullanıcı aracısını kullanarak isteğin gerçek Kullanıcı Aracısı değerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="e952a-458">The **HttpContext.SetOverriddenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="e952a-459">![Viewdeğiştirici denetleyicisi](whats-new-in-aspnet-mvc-4/_static/image31.png "Viewdeğiştirici denetleyicisi")</span><span class="sxs-lookup"><span data-stu-id="e952a-459">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="e952a-460">*Viewdeğiştirici denetleyicisi*</span><span class="sxs-lookup"><span data-stu-id="e952a-460">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="e952a-461">Tarayıcı geçersiz kılma, jQuery. Mobile. MVC paketini yüklemeseniz bile bulunan ASP.NET MVC 4 ' ün temel bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="e952a-461">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="e952a-462">Ancak, bu özellik yalnızca görünüm, düzen ve kısmi görünümü etkiler ve Isteğin. Browser nesnesine bağlı olan özelliklerden hiçbirini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="e952a-462">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="e952a-463">5\. görev-masaüstü görünümünde View-değiştirici ekleme</span><span class="sxs-lookup"><span data-stu-id="e952a-463">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="e952a-464">Bu görevde, masaüstü mizanpajını görünüm-değiştirici dahil olacak şekilde güncelleşirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-464">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="e952a-465">Bu, mobil kullanıcıların Masaüstü görünümüne gözatarken mobil görünüme geri gitmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-465">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="e952a-466">**Windows Phone öykünücüsünde**siteyi yenileyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-466">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="e952a-467">Galerinin en üstündeki **Masaüstü görünümü** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-467">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="e952a-468">Mobil görünüme geri dönebilmeniz için masaüstü görünümünde bir görünüm değiştirici olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-468">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="e952a-469">Visual Studio 'ya geri dönün ve **\_Layout. cshtml** görünümünü açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-469">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="e952a-470">Oturum açma bölümünü bulun ve **\_LogOnPartial** kısmi görünümü altında **\_viewdeğiştirici** kısmi görünümünü işlemek için bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-470">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="e952a-471">Ardından, değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-471">Then, press **CTRL + S** to save the changes.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. <span data-ttu-id="e952a-472">Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-472">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="e952a-473">Windows Phone öykünücüsünde sayfayı yenileyin ve yakınlaştırmak için ekrana çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-473">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="e952a-474">Giriş sayfasında artık mobil 'den Masaüstü görünümüne geçiş yapan **Mobil görünüm** bağlantısı gösterildiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-474">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="e952a-475">![Masaüstü görünümünde işlenen değiştirici görüntüle](whats-new-in-aspnet-mvc-4/_static/image32.png "Masaüstü görünümünde işlenen değiştirici görüntüle")</span><span class="sxs-lookup"><span data-stu-id="e952a-475">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="e952a-476">*Masaüstü görünümünde işlenen değiştirici görüntüle*</span><span class="sxs-lookup"><span data-stu-id="e952a-476">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="e952a-477">Mobil görünüme yeniden geçin **ve sayfaya gidin** (http://localhost[bağlantı noktası]/Home/About).</span><span class="sxs-lookup"><span data-stu-id="e952a-477">Switch to the Mobile view again and browse to **About** page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="e952a-478">Bir about. Mobile. cshtml görünümü oluşturmamış olsanız bile, mobil düzen (\_Layout. Mobile. cshtml) kullanılarak hakkında sayfasının görüntülendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-478">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="e952a-479">![Sayfa hakkında](whats-new-in-aspnet-mvc-4/_static/image33.png "Sayfa hakkında")</span><span class="sxs-lookup"><span data-stu-id="e952a-479">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="e952a-480">*Sayfa hakkında*</span><span class="sxs-lookup"><span data-stu-id="e952a-480">*About page*</span></span>
8. <span data-ttu-id="e952a-481">Son olarak, siteyi bir Masaüstü Web tarayıcısında açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-481">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="e952a-482">Önceki güncelleştirmelerden hiçbirinin masaüstü görünümünden etkilenmediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-482">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="e952a-483">![PhotoGallery masaüstü görünümü](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery masaüstü görünümü")</span><span class="sxs-lookup"><span data-stu-id="e952a-483">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="e952a-484">*PhotoGallery masaüstü görünümü*</span><span class="sxs-lookup"><span data-stu-id="e952a-484">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="e952a-485">Görev 6-yeni görüntü modları oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-485">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="e952a-486">Yeni görüntü modları özelliği, bir uygulamanın isteği oluşturan tarayıcıya bağlı olarak görünüm seçmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-486">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="e952a-487">Örneğin, bir masaüstü tarayıcısı giriş sayfasını isterse, uygulama **Views\home\ındex.cshtml** şablonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="e952a-487">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="e952a-488">Daha sonra, bir mobil tarayıcı giriş sayfasını isterse, uygulama **Views\Home\Index.Mobile.cshtml** şablonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="e952a-488">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="e952a-489">Bu görevde iPhone cihazları için özelleştirilmiş bir düzen oluşturacaksınız ve iPhone cihazlarından gelen isteklerin benzetimini yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-489">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="e952a-490">Bunu yapmak için, bir iPhone öykünücüsü/Simülatörü ( [elektrik mobil simülatörü](http://www.electricplum.com/)gibi) veya Kullanıcı aracısını değiştiren eklentilerle bir tarayıcı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-490">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="e952a-491">Bir iPhone tarayıcısı için bir Safari tarayıcısında Kullanıcı Aracısı dizesinin nasıl ayarlanacağı hakkında yönergeler için, bkz. Safari 'nin, David Alison blogundan [IE 'Yi nasıl öngörün](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) .</span><span class="sxs-lookup"><span data-stu-id="e952a-491">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="e952a-492">**Bu görevin isteğe bağlı olduğuna ve bunu yürütmeden laboratuvar genelinde devam edebildiğinize dikkat edin.**</span><span class="sxs-lookup"><span data-stu-id="e952a-492">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="e952a-493">Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-493">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="e952a-494">**Global.asax.cs** açın ve aşağıdaki using ifadesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-494">Open **Global.asax.cs** and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. <span data-ttu-id="e952a-495">Aşağıdaki Vurgulanan kodu uygulama\_start yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-495">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="e952a-496">(Kod parçacığı- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*)</span><span class="sxs-lookup"><span data-stu-id="e952a-496">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

<span data-ttu-id="e952a-497">**&quot;iPhone&quot;adlı yeni bir Defaultdisplaymode** , her gelen istek için eşleştirilecek statik **displaymodeprovider. Instance. Modes** statik listesi içinde kaydettiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-497">You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request.</span></span> <span data-ttu-id="e952a-498">Gelen istek iPhone&quot;&quot;dize içeriyorsa, ASP.NET MVC adı &quot;iPhone&quot; sonekini içeren görünümleri bulur.</span><span class="sxs-lookup"><span data-stu-id="e952a-498">If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix.</span></span> <span data-ttu-id="e952a-499">0 parametresi, belirtilen yeni mod olduğunu gösterir; Örneğin, bu görünüm mobil cihazlardan gelen isteklerle eşleşen genel &quot;. mobil&quot; kuralından daha özeldir.</span><span class="sxs-lookup"><span data-stu-id="e952a-499">The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.</span></span>

<span data-ttu-id="e952a-500">Bu kod çalıştıktan sonra, bir iPhone tarayıcısı bir istek oluşturduğunda, uygulamanız sonraki adımlarda oluşturacağınız **Views\shared\\_Layout. iPhone. cshtml** mizanpajını kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="e952a-500">After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.</span></span>

> [!NOTE]
> <span data-ttu-id="e952a-501">İPhone isteğini test etmenin bu şekilde tanıtım amaçlarıyla basitleştirilmesi ve her iPhone Kullanıcı Aracısı dizesi için beklenen şekilde çalışmayabilir (örneğin, test büyük/küçük harfe duyarlıdır).</span><span class="sxs-lookup"><span data-stu-id="e952a-501">This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).</span></span>

4. <span data-ttu-id="e952a-502">**Views\shared** klasöründe **\_Layout. Mobile. cshtml** dosyasının bir kopyasını oluşturun ve kopyayı &quot; **\_Layout. iPhone. cshtml**&quot;olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e952a-502">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.cshtml**&quot;.</span></span>
5. <span data-ttu-id="e952a-503">Önceki adımda oluşturduğunuz **\_Layout. iPhone. cshtml** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-503">Open **\_Layout.iPhone.cshtml** you created in the previous step.</span></span>
6. <span data-ttu-id="e952a-504">Data-Role özniteliği **Page** olarak ayarlanan div öğesini bulun ve **veri teması** özniteliğini **bir**&quot;&quot;olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-504">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

<span data-ttu-id="e952a-505">Artık ASP.NET MVC 4 uygulamanızda 3 düzenimize sahipsiniz:</span><span class="sxs-lookup"><span data-stu-id="e952a-505">Now you have 3 layouts in your ASP.NET MVC 4 application:</span></span>

1. <span data-ttu-id="e952a-506">**\_Layout. cshtml**: masaüstü tarayıcıları için kullanılan varsayılan düzen.</span><span class="sxs-lookup"><span data-stu-id="e952a-506">**\_Layout.cshtml**: default layout used for desktop browsers.</span></span>
2. <span data-ttu-id="e952a-507">**\_Layout. Mobile. cshtml**: mobil cihazlar için kullanılan varsayılan düzen.</span><span class="sxs-lookup"><span data-stu-id="e952a-507">**\_Layout.mobile.cshtml**: default layout used for mobile devices.</span></span>
3. <span data-ttu-id="e952a-508">**\_Layout. iPhone. cshtml**: \_düzeninden ayırt etmek için farklı bir renk şeması kullanarak iPhone cihazları için özel düzen. Mobile. cshtml.</span><span class="sxs-lookup"><span data-stu-id="e952a-508">**\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.</span></span>
7. <span data-ttu-id="e952a-509">**F5** tuşuna basarak uygulamayı çalıştırın ve **Windows Phone öykünücüsünde**siteye gidin.</span><span class="sxs-lookup"><span data-stu-id="e952a-509">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="e952a-510">Bir **iPhone simülatörü** açın (iPhone simülatörü yükleyip yapılandırma hakkında yönergeler için bkz. [Ek C](#AppendixC) ) ve siteye nasıl gözatacağınız.</span><span class="sxs-lookup"><span data-stu-id="e952a-510">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="e952a-511">Her telefonun belirli bir şablonu kullandığını fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-511">Notice that each phone is using the specific template.</span></span>

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="e952a-513">*Her mobil cihaz için farklı görünümler kullanma*</span><span class="sxs-lookup"><span data-stu-id="e952a-513">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="e952a-514">Alıştırma 4: zaman uyumsuz denetleyicileri kullanma</span><span class="sxs-lookup"><span data-stu-id="e952a-514">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="e952a-515">Microsoft .NET Framework 4,5, .NET programlama 'de zaman uyumsuzluğu için yeni bir temel sağlamak üzere C# ve Visual Basic yeni dil özellikleri sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e952a-515">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="e952a-516">Bu yeni temel, zaman uyumsuz programlamayı, ve ile benzer şekilde, tamamen zaman uyumlu programlama olarak sunar.</span><span class="sxs-lookup"><span data-stu-id="e952a-516">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="e952a-517">Artık **AsyncController** sınıfını kullanarak ASP.NET MVC 4 ' e zaman uyumsuz eylem yöntemleri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-517">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="e952a-518">Uzun süre çalışan, CPU olmayan istekler için zaman uyumsuz eylem yöntemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-518">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="e952a-519">Bu, istek işlenirken Web sunucusunun iş gerçekleştirmesini engellemeyi önler.</span><span class="sxs-lookup"><span data-stu-id="e952a-519">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="e952a-520">AsyncController sınıfı genellikle uzun süre çalışan Web hizmeti çağrıları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e952a-520">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="e952a-521">Bu alıştırmada, ASP.NET MVC 4 ' te zaman uyumsuz işlemin temelleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e952a-521">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="e952a-522">Daha ayrıntılı bilgi edinmek istiyorsanız aşağıdaki makaleye göz atabilirsiniz: [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="e952a-522">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="e952a-523">Görev 1-zaman uyumsuz denetleyici uygulama</span><span class="sxs-lookup"><span data-stu-id="e952a-523">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="e952a-524">**Kaynak/EX4-Async/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-524">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="e952a-525">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-525">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="e952a-526">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-526">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e952a-527">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-527">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e952a-528">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-528">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e952a-529">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-529">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e952a-530">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-530">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e952a-531">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-531">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e952a-532">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="e952a-532">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="e952a-533">**HomeController.cs** sınıfını **denetleyiciler** klasöründen açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-533">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="e952a-534">Aşağıdaki using ifadesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-534">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. <span data-ttu-id="e952a-535">Incontroller sınıfını **AsyncController**'dan devralacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-535">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="e952a-536">AsyncController 'dan türetilen denetleyiciler, zaman uyumsuz istekleri işlemek için ASP.NET özelliğini etkinleştirir ve zaman uyumlu eylem yöntemlerine hala hizmet verebilir.</span><span class="sxs-lookup"><span data-stu-id="e952a-536">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. <span data-ttu-id="e952a-537">**Zaman uyumsuz** anahtar sözcüğünü **Dizin** yöntemine ekleyin ve **&lt;ActionResult&gt;tür görevi** döndürün.</span><span class="sxs-lookup"><span data-stu-id="e952a-537">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > <span data-ttu-id="e952a-538">**Async** anahtar sözcüğü .NET Framework 4,5 'nin sağladığı yeni anahtar sözcüklerden biridir; derleyiciye bu yöntemin zaman uyumsuz kod içerdiğini söyler.</span><span class="sxs-lookup"><span data-stu-id="e952a-538">The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code.</span></span> <span data-ttu-id="e952a-539">Bir **görev** nesnesi, gelecekte bir noktada tamamlayaetkileyebilecek zaman uyumsuz bir işlemi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e952a-539">A **Task** object represents an asynchronous operation that may complete at some point in the future.</span></span>
6. <span data-ttu-id="e952a-540">İstemcisini değiştirin **.** Aşağıda gösterildiği gibi await anahtar sözcüğünü kullanan tam zaman uyumsuz sürümle GetAsync () çağrısı.</span><span class="sxs-lookup"><span data-stu-id="e952a-540">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="e952a-541">(Kod parçacığı- *ASP.NET MVC 4 Lab-Ex04-GetAsync*)</span><span class="sxs-lookup"><span data-stu-id="e952a-541">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="e952a-542">Önceki sürümde, sonuç döndürülünceye kadar iş parçacığını engellemek için **görev** nesnesinden **Result** özelliğini kullanıyorsunuz (eşitleme sürümü).</span><span class="sxs-lookup"><span data-stu-id="e952a-542">In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).</span></span>
    > 
    > <span data-ttu-id="e952a-543">**Await** anahtar sözcüğünü eklemek, derleyiciye yöntem çağrısından döndürülen görevin zaman uyumsuz olarak beklemesini söyler.</span><span class="sxs-lookup"><span data-stu-id="e952a-543">Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call.</span></span> <span data-ttu-id="e952a-544">Bu, kodun geri kalanının yalnızca beklenen Yöntem tamamlandıktan sonra geri çağırma olarak yürütülebileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e952a-544">This means that the rest of the code will be executed as a callback only after the awaited method completes.</span></span> <span data-ttu-id="e952a-545">Başka bir şey, bu işi yapmak için try-catch bloğunu değiştirmeniz gerekmez: arka planda veya ön planda gerçekleşen özel durumlar, çerçeve tarafından sunulan bir işleyici kullanılarak hiçbir ek iş olmadan yakalanacaktır.</span><span class="sxs-lookup"><span data-stu-id="e952a-545">Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.</span></span>
7. <span data-ttu-id="e952a-546">Satırları aşağıda gösterildiği gibi yeni kodla değiştirerek zaman uyumsuz uygulamayla devam edecek şekilde kodu değiştirin</span><span class="sxs-lookup"><span data-stu-id="e952a-546">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="e952a-547">(Kod parçacığı- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*)</span><span class="sxs-lookup"><span data-stu-id="e952a-547">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. <span data-ttu-id="e952a-548">Uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e952a-548">Run the application.</span></span> <span data-ttu-id="e952a-549">Önemli bir değişiklik olmadığını fark edeceksiniz, ancak kodunuz iş parçacığı havuzundan bir iş parçacığını engellemez ve bu da sunucu kaynaklarını daha iyi bir şekilde kullanımını ve performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="e952a-549">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-550">Laboratuvardaki yeni zaman uyumsuz programlama özellikleri hakkında daha fazla bilgi edinebilirsiniz &quot; **.net 4,5 ' de zaman uyumsuz programlama C# ve** Visual Studio eğitim paketine dahil Visual Basic&quot;.</span><span class="sxs-lookup"><span data-stu-id="e952a-550">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="e952a-551">Görev 2-Iptal belirteçleriyle zaman aşımlarını Işleme</span><span class="sxs-lookup"><span data-stu-id="e952a-551">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="e952a-552">Görev örnekleri döndüren zaman uyumsuz eylem metotları zaman aşımlarını de destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="e952a-552">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="e952a-553">Bu görevde, bir iptal belirteci kullanarak bir zaman aşımı senaryosunu işlemek için Dizin yöntemi kodunu güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="e952a-553">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="e952a-554">Visual Studio 'ya geri dönün ve hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-554">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="e952a-555">Aşağıdaki using ifadesini **HomeController.cs** dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-555">Add the following using statement to the **HomeController.cs** file.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. <span data-ttu-id="e952a-556">Dizin eylemini bir **CancellationToken** bağımsız değişkeni alacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-556">Update the Index action to receive a **CancellationToken** argument.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. <span data-ttu-id="e952a-557">İptal belirtecini geçirmek için **GetAsync** çağrısını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-557">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="e952a-558">(Kod parçacığı- *ASP.NET MVC 4 Lab-Ex04-CancellationToken Ile Sendadsync*)</span><span class="sxs-lookup"><span data-stu-id="e952a-558">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. <span data-ttu-id="e952a-559">*Dizin* yöntemini bir **AsyncTimeout** özniteliğiyle birlikte 500 milisaniyeye ve bir **zaman** aşımı görünümüne yönlendirerek **Taskolaydexception** işleyecek şekilde yapılandırılmış bir **HandleError** özniteliği süsleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-559">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="e952a-560">(Kod parçacığı- *ASP.NET MVC 4 Lab-Ex04-Attributes*)</span><span class="sxs-lookup"><span data-stu-id="e952a-560">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. <span data-ttu-id="e952a-561">**Photocontroller** sınıfını açın ve uzun süre çalışan bir görevin benzetimini yapmak için yürütme 1000 milisaniyesini (1 saniye) geciktirmek üzere **Galeri** yöntemini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-561">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 milliseconds (1 second) to simulate a long running task.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. <span data-ttu-id="e952a-562">**Web. config** dosyasını açın ve aşağıdaki öğeyi ekleyerek özel hataları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-562">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. <span data-ttu-id="e952a-563">**Views\shared** adlandırılmış **zaman aşımına uğradı** bölümünde yeni bir görünüm oluşturun ve varsayılan düzeni kullanın.</span><span class="sxs-lookup"><span data-stu-id="e952a-563">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="e952a-564">Çözüm Gezgini, **Views\shared** klasörüne sağ tıklayın ve **Ekle | ' yi seçin. Görüntüleyin**.</span><span class="sxs-lookup"><span data-stu-id="e952a-564">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="e952a-565">![Her mobil cihaz için farklı görünümler kullanma](whats-new-in-aspnet-mvc-4/_static/image36.png "Her mobil cihaz için farklı görünümler kullanma")</span><span class="sxs-lookup"><span data-stu-id="e952a-565">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="e952a-566">*Her mobil cihaz için farklı görünümler kullanma*</span><span class="sxs-lookup"><span data-stu-id="e952a-566">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="e952a-567">**Zaman aşımına uğradı** görünümü içeriğini aşağıda gösterildiği gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-567">Update the **TimedOut** view content as shown below.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. <span data-ttu-id="e952a-568">Uygulamayı çalıştırın ve kök URL 'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="e952a-568">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="e952a-569">Bir **iş 1000 parçacığı** eklediyseniz, **AsyncTimeout** özniteliği tarafından oluşturulan bir zaman aşımı hatası alırsınız ve **HandleError** özniteliğiyle elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-569">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="e952a-570">![Zaman aşımı özel durumu işlendi](whats-new-in-aspnet-mvc-4/_static/image37.png "Zaman aşımı özel durumu işlendi")</span><span class="sxs-lookup"><span data-stu-id="e952a-570">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="e952a-571">*Zaman aşımı özel durumu işlendi*</span><span class="sxs-lookup"><span data-stu-id="e952a-571">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="e952a-572">Ayrıca, [Ek D: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixD)için bu uygulamayı Microsoft Azure Web siteleri ' ne de dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-572">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="e952a-573">Özet</span><span class="sxs-lookup"><span data-stu-id="e952a-573">Summary</span></span>

<span data-ttu-id="e952a-574">Bu uygulamalı laboratuvarda, ASP.NET MVC 4 ' te yeni özelliklerden bazılarını gözlemlediniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-574">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="e952a-575">Aşağıdaki kavramlar tartışılır:</span><span class="sxs-lookup"><span data-stu-id="e952a-575">The following concepts have been discussed:</span></span>

- <span data-ttu-id="e952a-576">Yeni mobil uygulama projesi şablonu dahil olmak üzere, ASP.NET MVC proje şablonlarına yönelik geliştirmelerden yararlanın</span><span class="sxs-lookup"><span data-stu-id="e952a-576">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="e952a-577">Mobil cihazlarda ekranı geliştirmek için HTML5 Görünüm penceresi özniteliğini ve CSS medya sorgularını kullanın</span><span class="sxs-lookup"><span data-stu-id="e952a-577">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="e952a-578">Aşamalı geliştirmeler ve dokunarak iyileştirilmiş Web Kullanıcı arabirimi oluşturmak için jQuery Mobile kullanın</span><span class="sxs-lookup"><span data-stu-id="e952a-578">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="e952a-579">Mobil 'e özgü görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-579">Create mobile-specific views</span></span>
- <span data-ttu-id="e952a-580">Uygulamadaki mobil ve Masaüstü görünümleri arasında geçiş yapmak için View-değiştirici bileşenini kullanın</span><span class="sxs-lookup"><span data-stu-id="e952a-580">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="e952a-581">Görev desteğini kullanarak zaman uyumsuz denetleyiciler oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-581">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="e952a-582">Ek A: kod parçacıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="e952a-582">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="e952a-583">Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-583">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="e952a-584">Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="e952a-584">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="e952a-585">![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](whats-new-in-aspnet-mvc-4/_static/image38.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")</span><span class="sxs-lookup"><span data-stu-id="e952a-585">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="e952a-586">*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*</span><span class="sxs-lookup"><span data-stu-id="e952a-586">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="e952a-587">***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***</span><span class="sxs-lookup"><span data-stu-id="e952a-587">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="e952a-588">Kodu eklemek istediğiniz yere imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-588">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="e952a-589">Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).</span><span class="sxs-lookup"><span data-stu-id="e952a-589">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="e952a-590">IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-590">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="e952a-591">Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="e952a-591">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="e952a-592">Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="e952a-592">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="e952a-593">![Kod parçacığı adını yazmaya başlayın](whats-new-in-aspnet-mvc-4/_static/image39.png "Kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="e952a-593">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="e952a-594">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="e952a-594">*Start typing the snippet name*</span></span>

<span data-ttu-id="e952a-595">![Vurgulanan parçacığı seçmek için Tab tuşuna basın](whats-new-in-aspnet-mvc-4/_static/image40.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="e952a-595">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="e952a-596">*Vurgulanan parçacığı seçmek için Tab tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="e952a-596">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="e952a-597">![Sekmeye tekrar basın ve kod parçacığı genişletilir](whats-new-in-aspnet-mvc-4/_static/image41.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")</span><span class="sxs-lookup"><span data-stu-id="e952a-597">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="e952a-598">*Sekmeye tekrar basın ve kod parçacığı genişletilir*</span><span class="sxs-lookup"><span data-stu-id="e952a-598">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="e952a-599">***Fareyi kullanarak bir kod parçacığı eklemek için (C#, VISUAL BASIC ve XML)***</span><span class="sxs-lookup"><span data-stu-id="e952a-599">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="e952a-600">Kod parçacığını eklemek istediğiniz yere sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-600">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="e952a-601">Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-601">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="e952a-602">Listeden tıklatarak ilgili kod parçacığını seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-602">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="e952a-603">![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](whats-new-in-aspnet-mvc-4/_static/image42.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")</span><span class="sxs-lookup"><span data-stu-id="e952a-603">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="e952a-604">*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*</span><span class="sxs-lookup"><span data-stu-id="e952a-604">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="e952a-605">![Listeden tıklatarak ilgili kod parçacığını seçin](whats-new-in-aspnet-mvc-4/_static/image43.png "Listeden tıklatarak ilgili kod parçacığını seçin")</span><span class="sxs-lookup"><span data-stu-id="e952a-605">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="e952a-606">*Listeden tıklatarak ilgili kod parçacığını seçin*</span><span class="sxs-lookup"><span data-stu-id="e952a-606">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="e952a-607">Ek B: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="e952a-607">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="e952a-608">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-608">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="e952a-609">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="e952a-609">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="e952a-610">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin.</span><span class="sxs-lookup"><span data-stu-id="e952a-610">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="e952a-611">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, *Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012* &quot;ürünü açabilir ve bunu arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-611">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="e952a-612">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-612">Click on **Install Now**.</span></span> <span data-ttu-id="e952a-613">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-613">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="e952a-614">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-614">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="e952a-615">![Visual Studio Express yüklensin](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="e952a-615">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="e952a-616">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="e952a-616">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="e952a-617">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-617">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="e952a-619">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="e952a-619">*Accepting the license terms*</span></span>
5. <span data-ttu-id="e952a-620">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-620">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="e952a-622">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="e952a-622">*Installation progress*</span></span>
6. <span data-ttu-id="e952a-623">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-623">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="e952a-625">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="e952a-625">*Installation completed*</span></span>
7. <span data-ttu-id="e952a-626">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-626">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="e952a-627">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-627">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="e952a-629">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="e952a-629">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="e952a-630">Ek C: WebMatrix 2 ve iPhone simülatörü yükleme</span><span class="sxs-lookup"><span data-stu-id="e952a-630">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="e952a-631">Sitenizi sanal bir iPhone cihazında çalıştırmak için, iPhone&quot;için bir elektrik mobil simülasyonu &quot;WebMatrix uzantısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-631">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="e952a-632">Ayrıca, Visual Studio 2012 ' den Benzetici çalıştırmak için aynı uzantıyı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-632">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="e952a-633">Görev 1-WebMatrix yükleme 2</span><span class="sxs-lookup"><span data-stu-id="e952a-633">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="e952a-634">[[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)gidin.</span><span class="sxs-lookup"><span data-stu-id="e952a-634">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="e952a-635">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, bunu açıp &quot;*WebMatrix 2*&quot;ürünü arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-635">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*WebMatrix 2*&quot;.</span></span>
2. <span data-ttu-id="e952a-636">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-636">Click on **Install Now**.</span></span> <span data-ttu-id="e952a-637">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-637">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="e952a-638">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-638">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="e952a-639">![WebMatrix 'i yükler 2](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 'i yükler 2")</span><span class="sxs-lookup"><span data-stu-id="e952a-639">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="e952a-640">*WebMatrix 'i yükler 2*</span><span class="sxs-lookup"><span data-stu-id="e952a-640">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="e952a-641">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-641">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="e952a-642">![Lisans koşullarını kabul etme](whats-new-in-aspnet-mvc-4/_static/image50.png "Lisans koşullarını kabul etme")</span><span class="sxs-lookup"><span data-stu-id="e952a-642">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="e952a-643">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="e952a-643">*Accepting the license terms*</span></span>
5. <span data-ttu-id="e952a-644">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-644">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="e952a-645">![Yükleme ilerleme durumu](whats-new-in-aspnet-mvc-4/_static/image51.png "Yükleme ilerleme durumu")</span><span class="sxs-lookup"><span data-stu-id="e952a-645">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="e952a-646">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="e952a-646">*Installation progress*</span></span>
6. <span data-ttu-id="e952a-647">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-647">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="e952a-648">![Yükleme tamamlandı](whats-new-in-aspnet-mvc-4/_static/image52.png "Yükleme tamamlandı")</span><span class="sxs-lookup"><span data-stu-id="e952a-648">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="e952a-649">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="e952a-649">*Installation completed*</span></span>
7. <span data-ttu-id="e952a-650">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-650">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="e952a-651">Görev 2-iPhone simülatör uzantısını yükleme</span><span class="sxs-lookup"><span data-stu-id="e952a-651">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="e952a-652">**WebMatrix** 'i çalıştırın ve mevcut Web sitesini açın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e952a-652">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="e952a-653">**Giriş** şeridinde **Çalıştır** düğmesine tıklayın ve **Yeni Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-653">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="e952a-654">![Yeni WebMatrix uzantısı ekleniyor](whats-new-in-aspnet-mvc-4/_static/image53.png "Yeni WebMatrix uzantısı ekleniyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-654">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="e952a-655">*Yeni WebMatrix uzantısı ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-655">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="e952a-656">**IPhone simülatörü** ' **ni seçin ve ardından**</span><span class="sxs-lookup"><span data-stu-id="e952a-656">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="e952a-657">![WebMatrix uzantılarına göz atma](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix uzantılarına göz atma")</span><span class="sxs-lookup"><span data-stu-id="e952a-657">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="e952a-658">*WebMatrix uzantılarına göz atma*</span><span class="sxs-lookup"><span data-stu-id="e952a-658">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="e952a-659">Paket ayrıntıları ' nda, uzantı yüklemesine devam etmek için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-659">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="e952a-660">![iPhone simülatörü uzantısı](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone simülatörü uzantısı")</span><span class="sxs-lookup"><span data-stu-id="e952a-660">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="e952a-661">*iPhone simülatörü uzantısı*</span><span class="sxs-lookup"><span data-stu-id="e952a-661">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="e952a-662">Uzantıyı okuyun ve kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e952a-662">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="e952a-663">![WebMatrix uzantısı EULA 'Sı](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix uzantısı EULA 'Sı")</span><span class="sxs-lookup"><span data-stu-id="e952a-663">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="e952a-664">*WebMatrix uzantısı EULA 'Sı*</span><span class="sxs-lookup"><span data-stu-id="e952a-664">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="e952a-665">Şimdi, iPhone simülatörü seçeneğini kullanarak Web sitenizi WebMatrix 'ten çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-665">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="e952a-666">![İPhone kullanarak çalıştırma](whats-new-in-aspnet-mvc-4/_static/image57.png "İPhone kullanarak çalıştırma")</span><span class="sxs-lookup"><span data-stu-id="e952a-666">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="e952a-667">*İPhone kullanarak çalıştırma*</span><span class="sxs-lookup"><span data-stu-id="e952a-667">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="e952a-668">Görev 3-Visual Studio 2012 ' i iPhone simülatörü çalıştırmak için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e952a-668">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="e952a-669">**Visual Studio 2012** ' i açın ve herhangi bir Web sitesi açın veya yeni bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e952a-669">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="e952a-670">Çalıştır düğmesinden aşağı oka tıklayın ve **Ile araştır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-670">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="e952a-671">![İle araştır](whats-new-in-aspnet-mvc-4/_static/image58.png "İle araştır")</span><span class="sxs-lookup"><span data-stu-id="e952a-671">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="e952a-672">*İle araştır*</span><span class="sxs-lookup"><span data-stu-id="e952a-672">*Browse with*</span></span>
3. <span data-ttu-id="e952a-673">&quot;&quot; iletişim kutusunda **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-673">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="e952a-674">&quot;Program Ekle&quot; iletişim kutusunda aşağıdaki değerleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="e952a-674">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="e952a-675">**Program**: C:\Users\*{CurrentUser} \* \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(yolu uygun şekilde güncelleştirin)*</span><span class="sxs-lookup"><span data-stu-id="e952a-675">**Program**: C:\Users\*{CurrentUser}\*\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)*</span></span>
   - <span data-ttu-id="e952a-676">**Bağımsız değişkenler**: &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="e952a-676">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="e952a-677">**Kolay ad**: IPhone simülatörü</span><span class="sxs-lookup"><span data-stu-id="e952a-677">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="e952a-678">![Program Ekle](whats-new-in-aspnet-mvc-4/_static/image59.png "Program Ekle")</span><span class="sxs-lookup"><span data-stu-id="e952a-678">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="e952a-679">*Gezinmek için Program Ekle*</span><span class="sxs-lookup"><span data-stu-id="e952a-679">*Add program to browse with*</span></span>
5. <span data-ttu-id="e952a-680">**Tamam** ' a tıklayın ve iletişim kutularını kapatın.</span><span class="sxs-lookup"><span data-stu-id="e952a-680">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="e952a-681">Artık, Web uygulamalarınızı Visual Studio 2012 ' den iPhone simülatörü ' nden çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-681">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="e952a-682">![İPhone simülatörü ile tarayın](whats-new-in-aspnet-mvc-4/_static/image60.png "İPhone simülatörü ile tarayın")</span><span class="sxs-lookup"><span data-stu-id="e952a-682">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="e952a-683">*İPhone simülatörü ile tarayın*</span><span class="sxs-lookup"><span data-stu-id="e952a-683">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="e952a-684">Ek D: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="e952a-684">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="e952a-685">Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e952a-685">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="e952a-686">Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e952a-686">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="e952a-687">[Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e952a-687">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-688">Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-688">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="e952a-689">[Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-689">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="e952a-690">![Windows Azure portal oturum açın](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure portal oturum açın")</span><span class="sxs-lookup"><span data-stu-id="e952a-690">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="e952a-691">*Windows Azure 'da oturum açma Yönetim Portalı*</span><span class="sxs-lookup"><span data-stu-id="e952a-691">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="e952a-692">Komut çubuğunda **Yeni** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-692">Click **New** on the command bar.</span></span>

    <span data-ttu-id="e952a-693">![Yeni bir Web sitesi oluşturma](whats-new-in-aspnet-mvc-4/_static/image62.png "Yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="e952a-693">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="e952a-694">*Yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="e952a-694">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="e952a-695">**İşlem** | **Web sitesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-695">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="e952a-696">Sonra **hızlı oluştur** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-696">Then select **Quick Create** option.</span></span> <span data-ttu-id="e952a-697">Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-697">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-698">Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="e952a-698">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="e952a-699">Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e952a-699">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="e952a-700">Bir veritabanı ayarlamaya yönelik adımları içermez.</span><span class="sxs-lookup"><span data-stu-id="e952a-700">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="e952a-701">![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](whats-new-in-aspnet-mvc-4/_static/image63.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="e952a-701">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="e952a-702">*Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="e952a-702">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="e952a-703">Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-703">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="e952a-704">Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-704">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="e952a-705">Yeni Web sitesinin çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e952a-705">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="e952a-706">![Yeni Web sitesine göz atma](whats-new-in-aspnet-mvc-4/_static/image64.png "Yeni Web sitesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="e952a-706">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="e952a-707">*Yeni Web sitesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="e952a-707">*Browsing to the new web site*</span></span>

    <span data-ttu-id="e952a-708">![Web sitesi çalışıyor](whats-new-in-aspnet-mvc-4/_static/image65.png "Web sitesi çalışıyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-708">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="e952a-709">*Web sitesi çalışıyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-709">*Web site running*</span></span>
6. <span data-ttu-id="e952a-710">Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-710">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="e952a-711">![Web sitesi yönetim sayfalarını açma](whats-new-in-aspnet-mvc-4/_static/image66.png "Web sitesi yönetim sayfalarını açma")</span><span class="sxs-lookup"><span data-stu-id="e952a-711">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="e952a-712">*Web sitesi yönetim sayfalarını açma*</span><span class="sxs-lookup"><span data-stu-id="e952a-712">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="e952a-713">**Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-713">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-714">*Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="e952a-714">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="e952a-715">Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="e952a-715">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="e952a-716">**Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e952a-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="e952a-717">![Web sitesi yayımlama profili indiriliyor](whats-new-in-aspnet-mvc-4/_static/image67.png "Web sitesi yayımlama profili indiriliyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-717">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="e952a-718">*Web sitesi yayımlama profili indiriliyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-718">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="e952a-719">Yayımlama profili dosyasını bilinen bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="e952a-719">Download the publish profile file to a known location.</span></span> <span data-ttu-id="e952a-720">Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-720">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="e952a-721">![Yayımlama profili dosyası kaydediliyor](whats-new-in-aspnet-mvc-4/_static/image68.png "Yayımlama profili kaydediliyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-721">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="e952a-722">*Yayımlama profili dosyası kaydediliyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-722">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="e952a-723">Görev 2-veritabanı sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e952a-723">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="e952a-724">Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-724">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="e952a-725">SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-725">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="e952a-726">Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e952a-726">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="e952a-727">SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-727">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="e952a-728">Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e952a-728">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="e952a-729">**Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın.</span><span class="sxs-lookup"><span data-stu-id="e952a-729">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="e952a-730">Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-730">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="e952a-731">![SQL veritabanı sunucu panosu](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL veritabanı sunucu panosu")</span><span class="sxs-lookup"><span data-stu-id="e952a-731">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="e952a-732">*SQL veritabanı sunucu panosu*</span><span class="sxs-lookup"><span data-stu-id="e952a-732">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="e952a-733">Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e952a-733">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="e952a-734">Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](whats-new-in-aspnet-mvc-4/_static/image70.png) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-734">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![Istemci IP adresi ekleniyor](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="e952a-736">*Istemci IP adresi ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-736">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="e952a-737">**ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-737">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Değişiklikleri Onayla](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="e952a-739">*Değişiklikleri Onayla*</span><span class="sxs-lookup"><span data-stu-id="e952a-739">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="e952a-740">Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="e952a-740">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="e952a-741">ASP.NET MVC 4 çözümüne geri dönün.</span><span class="sxs-lookup"><span data-stu-id="e952a-741">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="e952a-742">**Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="e952a-742">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="e952a-743">![Uygulama yayımlanıyor](whats-new-in-aspnet-mvc-4/_static/image73.png "Uygulamayı Yayımlama")</span><span class="sxs-lookup"><span data-stu-id="e952a-743">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="e952a-744">*Web sitesi yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-744">*Publishing the web site*</span></span>
2. <span data-ttu-id="e952a-745">İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="e952a-745">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="e952a-746">![Yayımlama profilini içeri aktarma](whats-new-in-aspnet-mvc-4/_static/image74.png "Yayımlama profilini içeri aktarma")</span><span class="sxs-lookup"><span data-stu-id="e952a-746">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="e952a-747">*Yayımlama profili içeri aktarılıyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-747">*Importing publish profile*</span></span>
3. <span data-ttu-id="e952a-748">**Bağlantıyı doğrula**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-748">Click **Validate Connection**.</span></span> <span data-ttu-id="e952a-749">Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-749">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e952a-750">Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="e952a-750">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="e952a-751">![Bağlantı doğrulanıyor](whats-new-in-aspnet-mvc-4/_static/image75.png "Bağlantı doğrulanıyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-751">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="e952a-752">*Bağlantı doğrulanıyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-752">*Validating connection*</span></span>
4. <span data-ttu-id="e952a-753">**Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-753">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="e952a-754">![Web dağıtımı yapılandırması](whats-new-in-aspnet-mvc-4/_static/image76.png "Web dağıtımı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="e952a-754">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="e952a-755">*Web dağıtımı yapılandırması*</span><span class="sxs-lookup"><span data-stu-id="e952a-755">*Web deploy configuration*</span></span>
5. <span data-ttu-id="e952a-756">Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="e952a-756">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="e952a-757">**Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.</span><span class="sxs-lookup"><span data-stu-id="e952a-757">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="e952a-758">**Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="e952a-758">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="e952a-759">**Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="e952a-759">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="e952a-760">Yeni bir veritabanı adı yazın, örneğin: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="e952a-760">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="e952a-761">![Hedef bağlantı dizesi yapılandırılıyor](whats-new-in-aspnet-mvc-4/_static/image77.png "Hedef bağlantı dizesi yapılandırılıyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-761">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="e952a-762">*Hedef bağlantı dizesi yapılandırılıyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-762">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="e952a-763">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-763">Then click **OK**.</span></span> <span data-ttu-id="e952a-764">Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-764">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="e952a-765">![Veritabanı oluşturma](whats-new-in-aspnet-mvc-4/_static/image78.png "Veritabanı dizesi oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-765">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="e952a-766">*Veritabanı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="e952a-766">*Creating the database*</span></span>
7. <span data-ttu-id="e952a-767">Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e952a-767">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="e952a-768">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-768">Then click **Next**.</span></span>

    <span data-ttu-id="e952a-769">![SQL veritabanı 'na işaret eden bağlantı dizesi](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL veritabanı 'na işaret eden bağlantı dizesi")</span><span class="sxs-lookup"><span data-stu-id="e952a-769">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="e952a-770">*SQL veritabanı 'na işaret eden bağlantı dizesi*</span><span class="sxs-lookup"><span data-stu-id="e952a-770">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="e952a-771">**Önizleme** sayfasında **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e952a-771">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="e952a-772">![Web uygulaması yayımlanıyor](whats-new-in-aspnet-mvc-4/_static/image80.png "Web uygulaması yayımlanıyor")</span><span class="sxs-lookup"><span data-stu-id="e952a-772">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="e952a-773">*Web uygulaması yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="e952a-773">*Publishing the web application*</span></span>
9. <span data-ttu-id="e952a-774">Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.</span><span class="sxs-lookup"><span data-stu-id="e952a-774">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="e952a-775">![Windows Azure 'da yayımlanan uygulama](whats-new-in-aspnet-mvc-4/_static/image81.png "Windows Azure 'da yayımlanan uygulama")</span><span class="sxs-lookup"><span data-stu-id="e952a-775">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="e952a-776">*Windows Azure 'da yayımlanan uygulama*</span><span class="sxs-lookup"><span data-stu-id="e952a-776">*Application published to Windows Azure*</span></span>
