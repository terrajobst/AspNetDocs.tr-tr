---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 'Uygulamalı laboratuvar: Visual Studio 2013 web araçları | Microsoft Docs'
author: rick-anderson
description: Visual Studio, için mükemmel bir geliştirme ortamıdır. NET tabanlı Windows ve Web projeleri. Bu, kolayca kullanılabilecek güçlü bir metin Düzenleyicisi içerir...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622677"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="c9bbb-104">Uygulamalı Laboratuvar: Visual Studio 2013 Web Araçları</span><span class="sxs-lookup"><span data-stu-id="c9bbb-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>

<span data-ttu-id="c9bbb-105">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="c9bbb-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="c9bbb-106">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="c9bbb-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="c9bbb-107">Visual Studio, için mükemmel bir geliştirme ortamıdır. NET tabanlı Windows ve Web projeleri.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="c9bbb-108">Bu, bir proje olmadan tek başına dosyaları düzenlemek için kolayca kullanılabilecek güçlü bir metin Düzenleyicisi içerir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="c9bbb-109">Visual Studio, her dosyayı düzenlerken tam özellikli bir ayrıştırma ağacı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="c9bbb-110">Bu, Visual Studio 'Nun, geliştirme deneyimini çok daha hızlı ve daha fazla zevk hale getirerek benzersiz otomatik tamamlama ve belge tabanlı eylemler sağlamasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="c9bbb-111">Bu özellikler özellikle HTML ve CSS belgelerinde etkilidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="c9bbb-112">Bu gücün hepsi, uzantılar için de kullanılabilir ve bu da düzenleyicilerin gereksinimlerinize uyacak şekilde güçlü yeni özelliklerle genişlemelerini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="c9bbb-113">Web Essentials, Visual Studio 'Da Web ile ilgili geliştirmelerin (çoğunlukla) bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="c9bbb-114">Çok sayıda yeni IntelliSense tamamlamaları (özellikle CSS için), yeni tarayıcı bağlantısı özellikleri, JavaScript dosyaları için otomatik JSHint, HTML ve CSS için yeni uyarılar ve modern web geliştirme için gerekli olan diğer birçok özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="c9bbb-115">Tüm örnek kod ve kod parçacıkları [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-115">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="c9bbb-116">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="c9bbb-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="c9bbb-117">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="c9bbb-117">Objectives</span></span>

<span data-ttu-id="c9bbb-118">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="c9bbb-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="c9bbb-119">Zengin HTML5 kod parçacıkları ve Zen kodlama gibi Web Essentials 'ta bulunan yeni HTML düzenleyici özelliklerini kullanın</span><span class="sxs-lookup"><span data-stu-id="c9bbb-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="c9bbb-120">Renk Seçicisi ve tarayıcı matrisi araç ipucu gibi Web temelleri 'nde bulunan yeni CSS Düzenleyici özelliklerini kullanın</span><span class="sxs-lookup"><span data-stu-id="c9bbb-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="c9bbb-121">Dosyaya Ayıkla ve tüm HTML öğeleri için IntelliSense gibi Web temelleri 'nde bulunan yeni JavaScript Düzenleyici özelliklerini kullanın</span><span class="sxs-lookup"><span data-stu-id="c9bbb-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="c9bbb-122">Tarayıcı bağlantısı kullanarak tarayıcınızla ve Visual Studio arasında veri alışverişi</span><span class="sxs-lookup"><span data-stu-id="c9bbb-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c9bbb-123">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c9bbb-123">Prerequisites</span></span>

<span data-ttu-id="c9bbb-124">Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="c9bbb-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="c9bbb-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) veya üzeri</span><span class="sxs-lookup"><span data-stu-id="c9bbb-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="c9bbb-126">Web temelleri 2013</span><span class="sxs-lookup"><span data-stu-id="c9bbb-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="c9bbb-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="c9bbb-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c9bbb-128">Kurulum</span><span class="sxs-lookup"><span data-stu-id="c9bbb-128">Setup</span></span>

<span data-ttu-id="c9bbb-129">Bu uygulamalı laboratuvarda alýþtýrmalarý çalıştırmak için öncelikle ortamınızı ayarlamanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="c9bbb-130">Bir Windows Explorer penceresi açın ve laboratuvarın **kaynak** klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="c9bbb-131">Ortamınızı yapılandıracak ve bu laboratuvar için Visual Studio kod parçacıklarını yükleyecek kurulum işlemini başlatmak için **Setup. cmd** ' ye sağ tıklayın ve **yönetici olarak çalıştır** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="c9bbb-132">Kullanıcı hesabı denetimi iletişim kutusu gösterilirse, devam etmek için eylemi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="c9bbb-133">Kurulumu çalıştırmadan önce bu laboratuvarın tüm bağımlılıklarını denetlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="c9bbb-134">Kod parçacıklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-134">Using the Code Snippets</span></span>

<span data-ttu-id="c9bbb-135">Laboratuvar belgesi boyunca kod blokları eklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="c9bbb-136">Kolaylık olması için, bu kodun çoğu Visual Studio Code kod parçacığı olarak sağlanır ve bu, el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio 2013 içinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="c9bbb-137">Her alıştırma, her alıştırmanın bağımsız olarak her birini takip etmenizi sağlayan alıştırmanın **BEGIN** klasöründe bulunan bir başlangıç çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="c9bbb-138">Lütfen bir alıştırma sırasında eklenen kod parçacıklarının bu başlangıç çözümlerinde eksik olduğunu ve Alıştırmayı tamamlayana kadar çalışmadığının farkında olun.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="c9bbb-139">Bir alıştırmada kaynak kodun içinde, ilgili alıştırmada adımların tamamlanmasına neden olan koda sahip bir Visual Studio çözümü içeren bir **son** klasör de bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="c9bbb-140">Bu uygulamalı laboratuvarda çalışırken daha fazla yardıma ihtiyacınız varsa bu çözümleri kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c9bbb-141">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="c9bbb-141">Exercises</span></span>

<span data-ttu-id="c9bbb-142">Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:</span><span class="sxs-lookup"><span data-stu-id="c9bbb-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="c9bbb-143">Tarayıcı bağlantısı ve Web temel bileşenleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="c9bbb-144">Kod parçacıkları ve IntelliSense avantajlarından yararlanma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="c9bbb-145">Visual Studio 'Yu ilk kez başlattığınızda, önceden tanımlanmış ayarlar koleksiyonundan birini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="c9bbb-146">Her önceden tanımlı koleksiyon, belirli bir geliştirme stiliyle eşleşecek şekilde tasarlanmıştır ve pencere düzenlerini, düzenleyici davranışını, IntelliSense kod parçacıklarını ve iletişim kutusu seçeneklerini belirler.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="c9bbb-147">Bu laboratuvardaki yordamlarda, **genel geliştirme ayarları** koleksiyonu kullanılırken, Visual Studio 'da belirli bir görevi gerçekleştirmek için gereken eylemler açıklanır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="c9bbb-148">Geliştirme ortamınız için farklı bir ayarlar koleksiyonu seçerseniz, adımlarda dikkate almanız gereken adımlarda farklılıklar olabilir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="c9bbb-149">Alıştırma 1: tarayıcı bağlantısı ve Web temel bileşenleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="c9bbb-150">**Web temel** bileşenleri, modern web geliştirme için pek çok yararlı özellik ekleyen, genellikle Web geliştirme deneyiminin çok daha hızlı ve daha fazla zevk hale getirilmesi için kullanabileceğiniz bir Visual Studio uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="c9bbb-151">Web Essentials 'ı Visual Studio 'daki uzantı galerisinden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="c9bbb-152">**Tarayıcı bağlantısı** , VISUAL Studio IDE ve Visual Studio ile veri alışverişi yapmak için herhangi bir açık tarayıcı arasında bir kanal sağlayan yeni bir özelliktir Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="c9bbb-153">Web Essentials, tarayıcı bağlantısını, DOM nesne modelini ve Web sayfalarınızın CSS stillerini doğrudan tarayıcıdan işlemek için araçlar ile genişletir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="c9bbb-154">Bu alıştırmada, **Web Essentials** ve **tarayıcı bağlantısı** tarafından desteklenen özelliklerden bazılarını inceleyerek basit bir test sayfasını geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="c9bbb-155">Görev 1-birden çok tarayıcıda projeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="c9bbb-156">Bu görevde, Web uygulamanızı birden çok tarayıcıda çalışacak şekilde yapılandıracaksınız, bu, tarayıcılar arası testler için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="c9bbb-157">**Microsoft Visual Studio**açın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="c9bbb-158">**Dosya** menüsünde Aç ' ı seçin **| Proje/çözüm...** ve laboratuvarın **kaynak** klasöründe **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** (C:\WebCampsTK\HOL\VSWebTooling\Source) konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="c9bbb-159">**Başlat. sln** ' yi seçin ve **Aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="c9bbb-160">Visual Studio araç çubuğunda tarayıcı menüsünü genişletin ve **Bununla birlikte araştır...** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="c9bbb-161">![Menü seçeneği Ile araştır](visual-studio-2013-web-tools/_static/image1.png "İle araştır... tarayıcı menüsünde")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="c9bbb-162">*Menü seçeneği Ile araştır*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="c9bbb-163">**Ile araştır** iletişim kutusunda, **CTRL** tuşunu basılı tutarak ve **Varsayılan olarak ayarla**' ya tıklayarak **Google Chrome** ve **Internet Explorer** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="c9bbb-164">![İletişim kutusu ile araştır](visual-studio-2013-web-tools/_static/image2.png "İletişim kutusu ile araştır")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="c9bbb-165">*Birden çok varsayılan tarayıcı seçme*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="c9bbb-166">Artık Google Chrome ve Internet Explorer varsayılan tarayıcılar olarak görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="c9bbb-167">İletişim kutusunu kapatmak için **iptal** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="c9bbb-168">![Google Chrome ve Internet Explorer varsayılan tarayıcılar olarak](visual-studio-2013-web-tools/_static/image3.png "Google Chrome ve Internet Explorer varsayılan tarayıcıları")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="c9bbb-169">*Google Chrome ve Internet Explorer varsayılan tarayıcılar olarak*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9bbb-170">Varsayılan tarayıcıları yapılandırdıktan sonra, tarayıcı menüsünde **birden çok tarayıcı** seçeneği seçilidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="c9bbb-171">![Birden çok tarayıcı](visual-studio-2013-web-tools/_static/image4.png "Birden çok tarayıcı")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="c9bbb-172">Uygulamayı hata ayıklamadan çalıştırmak için **CTRL** + **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="c9bbb-173">Her iki tarayıcı penceresi açık olduğunda, her iki tarayıcıda da aynı anda güncelleştirmeleri görmek için bunlardan birini diğerinin üzerine yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="c9bbb-174">Tarayıcılar açık mavi dikdörtgenle bir Web sayfası görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="c9bbb-175">![Diğerinin üzerine bir tarayıcı yerleştirme](visual-studio-2013-web-tools/_static/image5.png "Diğerinin üzerine bir tarayıcı yerleştirme")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="c9bbb-176">*Diğerinin üzerine bir tarayıcı yerleştirme*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="c9bbb-177">Tarayıcıları kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-177">Do not close the browsers.</span></span> <span data-ttu-id="c9bbb-178">Bunları bir sonraki görevde kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="c9bbb-179">Görev 2-HTML öğeleri oluşturmak için Zen kodlaması kullanma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="c9bbb-180">**Zen kodlaması** , kodlama ve düzenleme için yüksek hızlı HTML, XML, XSL (veya başka bir yapılandırılmış kod biçimi) için bir düzenleyici eklentisidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="c9bbb-181">Bu eklentinin çekirdeği, CSS seçicilerinin HTML koduna benzer ifadeler genişletmenizi sağlayan güçlü bir kısaltma altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="c9bbb-182">Zen kodlaması, CSS stil Seçicisi sözdizimi kullanarak HTML yazmanın hızlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="c9bbb-183">Bu alıştırmada, sorunun seçeneklerini temsil eden HTML düğmelerini oluşturmak için Web Essentials tarafından sunulan Zen kodlama özelliğini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="c9bbb-184">Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="c9bbb-185">**Görünümler** | **giriş** klasöründe bulunan **Index. cshtml** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="c9bbb-186">**&lt;!--TODO: aşağıdaki kodla açıklama ekleyin--&gt;** yazın ve **Tab**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="c9bbb-187">Kod HTML olarak genişletilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="c9bbb-188">![Genişletilmiş HTML](visual-studio-2013-web-tools/_static/image6.png "Genişletilmiş HTML")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="c9bbb-189">*Genişletilmiş HTML*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9bbb-190">Zen kodlama sözdizimi hakkında daha fazla bilgi edinmek için aşağıdaki [makaleye](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)bakın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="c9bbb-191">Her iki tarayıcıyı da güncelleştirmek için **bağlı tarayıcıları Yenile** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="c9bbb-192">![Bağlı tarayıcıları Yenile](visual-studio-2013-web-tools/_static/image7.png "Bağlı tarayıcıları Yenile")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="c9bbb-193">*Bağlı tarayıcıları Yenile*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="c9bbb-194">![Internet Explorer-sayfa dört düğme ile güncelleştirildi](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-sayfa dört düğme ile güncelleştirildi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="c9bbb-195">*Internet Explorer-sayfa dört düğme ile güncelleştirildi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="c9bbb-196">![Google Chrome-sayfa dört düğme ile güncelleştirildi](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-sayfa dört düğme ile güncelleştirildi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="c9bbb-197">*Google Chrome-sayfa dört düğme ile güncelleştirildi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="c9bbb-198">Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="c9bbb-199">Düğmeleri sayfaya eklediniz, ancak yine de bir şablon sorusu eklemeniz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="c9bbb-200">Bunu yapmak için, Web Essentials 'ta **Lorem Ipsum Generator**adlı yeni bir özellik kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="c9bbb-201">**Sınıf** özniteliği **önünde** **div** öğesini bulun.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="c9bbb-202">Aşağıdaki kodu **div**öğesinin ilk alt öğesi olarak ekleyin ve **Tab**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="c9bbb-203">Kod HTML olarak genişletilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="c9bbb-204">![Lorem Ipsum otomatik olarak oluşturulur](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum otomatik olarak oluşturulur")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="c9bbb-205">*Lorem Ipsum otomatik olarak oluşturulur*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9bbb-206">Zen kodlama kapsamında artık doğrudan HTML düzenleyicisinde Lorem Ipsum kodu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="c9bbb-207">**Lorem** ve hit **sekmesini** yazmanız yeterlidir ve bir 30 sözcük Lorem Ipsum metni eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="c9bbb-208">Örneğin</span><span class="sxs-lookup"><span data-stu-id="c9bbb-208">E.g.</span></span> <span data-ttu-id="c9bbb-209">*lorem10* 10 Lorem Ipsum sözcüklerini ekler.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="c9bbb-210">Web Essentials 'ta **lorem pixel Oluşturucu**adlı başka bir yeni özellik kullanarak, sorunun en üstüne bir logo ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="c9bbb-211">Aşağıdaki **kodu, Container öğesinin ilk** alt öğesi olarak **kapsayıcı** **sınıf** değeri olarak ekleyin ve **Tab**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="c9bbb-212">Kod HTML olarak genişletilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="c9bbb-213">![Lorem piksel otomatik olarak oluşturulur](visual-studio-2013-web-tools/_static/image11.png "Lorem piksel otomatik olarak oluşturulur")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="c9bbb-214">*Lorem piksel otomatik olarak oluşturulur*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9bbb-215">Zen kodlama kapsamında, doğrudan HTML düzenleyicisinde Lorem pixel kodu da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="c9bbb-216">Yalnızca **PIX-200x200-hayvanlar** ve vuruş **sekmesine** ve bir hayvan 'nin 200x200 görüntüsüne sahip bir **img** etiketi eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="c9bbb-217">Daha fazla bilgi için [lorem pixel](http://www.lorempixel.com)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="c9bbb-218">Her iki tarayıcıyı da güncelleştirmek için **bağlı tarayıcıları Yenile** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="c9bbb-219">![Internet Explorer-otomatik olarak görüntü ve metin](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-otomatik olarak görüntü ve metin")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="c9bbb-220">*Internet Explorer-otomatik olarak görüntü ve metin*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="c9bbb-221">![Google Chrome-otomatik oluşturulan görüntü ve metin](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-otomatik oluşturulan görüntü ve metin")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="c9bbb-222">*Google Chrome-otomatik oluşturulan görüntü ve metin*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9bbb-223">Kod parçacığı eklenirken görüntü rastgele seçildiğinden, tarayıcılarda gösterilen resim farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="c9bbb-224">Tarayıcıları kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-224">Do not close the browsers.</span></span> <span data-ttu-id="c9bbb-225">Bunları bir sonraki görevde kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="c9bbb-226">Görev 3-stil özelliğini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c9bbb-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="c9bbb-227">Bu görevde, belirli DOM öğesinin oluşturulduğu konumun tam konumunu tespit etmek ve ardından Web Essentials tarafından sunulan bir renk seçici kullanarak söz konusu öğenin Color özelliğini güncellemek için tarayıcı bağlantısının **Inceleme modu** özelliğini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="c9bbb-228">Internet Explorer tarayıcısında, Inceleme modunu etkinleştirmek için **CTRL** + **alt** + **I** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="c9bbb-229">İşaretçiyi açık mavi kenarlığının üzerine taşıyın ve öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="c9bbb-230">![İşaretçiyi açık mavi kenarlık üzerine taşıma](visual-studio-2013-web-tools/_static/image14.png "İşaretçiyi açık mavi kenarlık üzerine taşıma")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="c9bbb-231">*İşaretçiyi açık mavi kenarlık üzerine taşıma*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="c9bbb-232">Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="c9bbb-233">Tarayıcıda seçtiğiniz HTML öğesinin Visual Studio HTML düzenleyicisinde de seçili olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="c9bbb-234">![Visual Studio HTML düzenleyicisinde seçili HTML öğesi](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML düzenleyicisinde seçili HTML öğesi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="c9bbb-235">*Visual Studio HTML düzenleyicisinde seçili HTML öğesi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="c9bbb-236">Şimdi, seçili öğenin stilini değiştirmek için **ön** CSS sınıfını güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="c9bbb-237">Bunu yapmak için **CTRL** +  **'** e basarak aramaya **Git** kutusunu açın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="c9bbb-238">Dosyayı açmak için **site. css** yazın ve **ENTER** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="c9bbb-239">![Dosya sitesi. css açılıyor](visual-studio-2013-web-tools/_static/image16.png "Dosya sitesi. css açılıyor")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="c9bbb-240">*Dosya sitesi. css açılıyor*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="c9bbb-241">CSS seçiciyi bulmak için **CTRL** + **F** tuşlarına basın ve **. Flip-Container. Front** yazın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-241">Press **CTRL** + **F** and type **.flip-container .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="c9bbb-242">Renk seçiciyi açmak için sınıfın Border özelliğindeki açık mavi kare öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="c9bbb-243">![Renk seçiciyi açma](visual-studio-2013-web-tools/_static/image17.png "Renk seçiciyi açma")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="c9bbb-244">*Renk seçiciyi açma*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="c9bbb-245">Köşeli çift ayraç düğmesine tıklayıp yeni bir renk seçerek renk seçiciyi genişletin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="c9bbb-246">![Renk seçiciyi genişletme](visual-studio-2013-web-tools/_static/image18.png "Renk seçiciyi genişletme")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="c9bbb-247">*Renk seçiciyi genişletme*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="c9bbb-248">Bağlı tarayıcıları yenilemek için **CTRL** + **alt** + **ENTER** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="c9bbb-249">Internet Explorer 'a geçin ve kenarlığın renginin nasıl değiştiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="c9bbb-250">![Internet Explorer-kenarlık rengi güncelleştirildi](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-kenarlık rengi güncelleştirildi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="c9bbb-251">*Internet Explorer-kenarlık rengi güncelleştirildi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="c9bbb-252">Google Chrome 'a geçin ve kenarlığın renginin nasıl değiştiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="c9bbb-253">![Google Chrome-kenarlık rengi güncelleştirildi](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-kenarlık rengi güncelleştirildi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="c9bbb-254">*Google Chrome-kenarlık rengi güncelleştirildi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="c9bbb-255">Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="c9bbb-256">**Site. css** dosyasının sonuna gidin ve **. btn** seçicisini bulmak için **CTRL** + **F** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="c9bbb-257">**-WebKit-Border-Radius** özelliğinin yeşil renkte altı çizili olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="c9bbb-258">![-WebKit-Border-yarıçap özelliği btn Seçicisi](visual-studio-2013-web-tools/_static/image21.png "-WebKit-Border-yarıçap özelliği btn Seçicisi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="c9bbb-259">*-WebKit-Border-yarıçap özelliği btn Seçicisi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="c9bbb-260">Giriş işaretini **-WebKit-Border-Radius** özelliğine yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="c9bbb-261">Özelliğin ilk sözcüğünün ilk harfinin altında mavi bir çizgi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="c9bbb-262">Bu **akıllı etikettir**.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="c9bbb-263">**CTRL** + tuşuna basın **.**</span><span class="sxs-lookup"><span data-stu-id="c9bbb-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="c9bbb-264">Öneriler menüsünü açmak için **eksik standart özelliği Ekle (kenarlık-yarıçap)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="c9bbb-265">![Eksik standart özellik önerisi Ekle](visual-studio-2013-web-tools/_static/image22.png "Eksik standart özellik önerisi Ekle")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="c9bbb-266">*Eksik standart özellik önerisi Ekle*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="c9bbb-267">**Border-Radius** özelliği CSS kuralına otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="c9bbb-268">![Eksik standart özellik eklendi](visual-studio-2013-web-tools/_static/image23.png "Eksik standart özellik eklendi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="c9bbb-269">*Eksik standart özellik eklendi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="c9bbb-270">**Tarayıcı matris araç ipucunu**göstermek için işaretçiyi **Border-Radius** özelliğinin üzerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="c9bbb-271">**Tarayıcı matrisi araç ipucu** , her tarayıcıda özelliğin kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="c9bbb-272">![Tarayıcı matrisi araç ipucu](visual-studio-2013-web-tools/_static/image24.png "Tarayıcı matrisi araç ipucu")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="c9bbb-273">*Tarayıcı matrisi araç ipucu*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="c9bbb-274">**Border-Radius** özelliğinin değerinin hala altı çizili olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="c9bbb-275">Uyarı iletisini görmek için işaretçiyi değerin üzerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="c9bbb-276">![Border-RADIUS Özellik değeri uyarısı](visual-studio-2013-web-tools/_static/image25.png "Border-RADIUS Özellik değeri uyarısı")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="c9bbb-277">*Border-RADIUS Özellik değeri uyarısı*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="c9bbb-278">Araç İpucu tarafından önerildiği şekilde **Border-Radius** özelliği değerinin birimini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="c9bbb-279">**Sınır-yarıçap** , yuvarlatılmış kenarlık köşelerinin nasıl olduğunu tanımlamaya yönelik standart bir özelliktir, **-WebKit-Border-Radius** özelliğini ve değeri CSS kuralından kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="c9bbb-280">Giriş işaretini **Word Wrap** özelliğine yerleştirin ve akıllı etiketin aşağıda da göründüğünü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="c9bbb-281">Menüyü açın ve **eksik satıcı Özellikleri Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="c9bbb-282">![Eksik satıcı özellikleri önerisi Ekle](visual-studio-2013-web-tools/_static/image26.png "Eksik satıcı özellikleri önerisi Ekle")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="c9bbb-283">*Eksik satıcı özellikleri önerisi Ekle*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="c9bbb-284">**-MS-Word-Wrap** özelliği CSS kuralına otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="c9bbb-285">![Satıcıya özgü özellik eklendi](visual-studio-2013-web-tools/_static/image27.png "Satıcıya özgü özellik eklendi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="c9bbb-286">*Satıcıya özgü özellik eklendi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="c9bbb-287">Görev 4-tarayıcıdan HTML kodu güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="c9bbb-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="c9bbb-288">Bu görevde, tarayıcı bağlantısının **tasarım modu** ÖZELLIĞINI kullanarak DOM nesnesini tarayıcıdan düzenleyebilir ve değişiklikleri Visual STUDIO 'daki HTML kaynak dosyasına aktaracaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="c9bbb-289">Google Chrome 'da tasarım modunu etkinleştirmek için **CTRL** + **alt** + **D** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="c9bbb-290">İşaretçiyi **Lorem Ipsum dolor, amet** etiketinin üzerine taşıyın ve öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="c9bbb-291">![Soruyu düzenleniyor](visual-studio-2013-web-tools/_static/image28.png "Soruyu düzenleniyor")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="c9bbb-292">*Soruyu düzenleniyor*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-292">*Editing the question*</span></span>
3. <span data-ttu-id="c9bbb-293">Bir imleç görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-293">A cursor should appear.</span></span> <span data-ttu-id="c9bbb-294">Özgün metni, *daha uzun bir soru yazarken nasıl görüneceğine benzer bir*şekilde değiştirin ve ardından tasarım modundan çıkmak için **ESC** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="c9bbb-295">![Soru düzenlendi](visual-studio-2013-web-tools/_static/image29.png "Soru düzenlendi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="c9bbb-296">*Soru düzenlendi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-296">*Question edited*</span></span>
4. <span data-ttu-id="c9bbb-297">Visual Studio 'ya geri dönün ve henüz açılmadıysa **Index. cshtml**dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="c9bbb-298">**&lt;p&gt;** öğesinin iç metninin güncelleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="c9bbb-299">![HTML sayfasında güncelleştirilmiş soru](visual-studio-2013-web-tools/_static/image30.png "HTML sayfasında güncelleştirilmiş soru")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="c9bbb-300">*HTML sayfasında güncelleştirilmiş soru*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="c9bbb-301">Görev 5-SEO Ilgili uyarıları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="c9bbb-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="c9bbb-302">**Arama motoru iyileştirmesi** (SEO), bir arama altyapısının sonuç listesinde bir Web sitesi sırası daha yüksek hale getirme işlemidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="c9bbb-303">Site ne kadar yüksek olursa ve daha tutarlı bir şekilde listeleniyorsa, sitenin ilgili arama altyapısından daha fazla ziyaretçi olur.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="c9bbb-304">Web Essentials, HTML 'yi inceleyen, bulunan sorunları raporlayan ve bunları çözmek için yardım sağlayan bir analitik araç içerir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="c9bbb-305">**Görünüm** menüsüne gidin ve **hata listesi** ' ye tıklayarak **hata listesi** penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="c9bbb-306">![Görünüm menüsündeki Hata Listesi](visual-studio-2013-web-tools/_static/image31.png "Görünüm menüsündeki Hata Listesi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="c9bbb-307">*Görünüm menüsündeki Hata Listesi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="c9bbb-308">Sayfa açıklaması için bir **&lt;meta&gt;** etiketinin eksik olduğunu BILDIREN bir SEO uyarısı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="c9bbb-309">Bu çözümü onarmak için SEO uyarı girişine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="c9bbb-310">![Hata Listesi penceresi](visual-studio-2013-web-tools/_static/image32.png "Hata Listesi penceresi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="c9bbb-311">*Hata Listesi penceresi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-311">*Error List window*</span></span>
3. <span data-ttu-id="c9bbb-312">**Web Essentials** iletişim kutusunda, bir açıklama &lt;meta&gt; etiketi eklemek için **Evet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="c9bbb-313">![Web Essentials iletişim kutusu](visual-studio-2013-web-tools/_static/image33.png "Web Essentials iletişim kutusu")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="c9bbb-314">*Web Essentials iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="c9bbb-315">**Layout. cshtml\_** Düzenleyicisi açılır ve **&lt;meta&gt;** etiketi HTML dosyasının **baş** bölümüne otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="c9bbb-316">![Meta etiketi _Layout sayfasına otomatik olarak eklendi](visual-studio-2013-web-tools/_static/image34.png "Meta etiketi _Layout sayfasına otomatik olarak eklendi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="c9bbb-317">*Meta etiketi \_düzen sayfasına otomatik olarak eklendi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="c9bbb-318">**İçerik** özniteliğinin değerini *geektest* olarak değiştirin ve dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="c9bbb-319">Alıştırma 2: kod parçacıkları ve IntelliSense 'den yararlanın</span><span class="sxs-lookup"><span data-stu-id="c9bbb-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="c9bbb-320">Web Essentials ile HTML Düzenleyicisi, ek işlevlerle genişletilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="c9bbb-321">Bu alıştırmada, Web uygulamaları geliştirirken yararlı olan bazı yeni özellikler göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="c9bbb-322">Görev 1-HTML belgelerinde IntelliSense kullanma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="c9bbb-323">Bu görevde göreceğiniz ilk yeni özelliğe **dinamik IntelliSense**denir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="c9bbb-324">Dinamik IntelliSense, kullanacağınız olası kimlikleri çıkarması için diğer etiketleri ve öznitelikleri okur.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="c9bbb-325">Bu görevde, bir etiket ve bir giriş alanı içeren yeni bir HTML form öğesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="c9bbb-326">Ardından etikete bağlamak için etiketine bir **for** özniteliği ekleyeceksiniz ve kapsamdaki girişlerin kimliklerine bağlı olarak IntelliSense önerilerini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="c9bbb-327">**Web için Visual Studio Express 2013** ve **kaynak/EX2-TakingAdvantageofCodeSnippetsandIntelliSense/BEGIN** klasöründe bulunan **BEGIN. sln** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="c9bbb-328">Alternatif olarak, önceki alıştırmada elde ettiğiniz çözüme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="c9bbb-329">**Çözüm Gezgini**' de, **Görünümler** | **giriş** klasöründe bulunan **Index. cshtml** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="c9bbb-330">Aşağıdaki formu **&lt;section&gt;** öğesi içine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="c9bbb-331">(Kod parçacığı- *VisualStudio2013WebTooling* - *EX2* - *form*)</span><span class="sxs-lookup"><span data-stu-id="c9bbb-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="c9bbb-332">Giriş etiketinin önünde, alanın açıklamasını içeren bir etiket gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="c9bbb-333">Giriş etiketinden önce aşağıdaki etiketi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="c9bbb-334">**&lt;etiketinin** **for** özniteliği&gt;bir etiketin hangi form öğesine bağlandığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="c9bbb-335">Özniteliğin değeri ilgili öğenin kimliğine eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="c9bbb-336">**For** özniteliğini **&lt;Label&gt;** öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="c9bbb-337">Aşağıdaki şekilde gösterildiği gibi, &quot;adı&quot; değeri IntelliSense kutusunda, aynı kapsamdaki öğelerin kimliğine (kapsayan **&lt;formu&gt;** ) göre açılır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="c9bbb-338">![IntelliSense 'de kimliği gösterme](visual-studio-2013-web-tools/_static/image35.png "IntelliSense 'de kimliği gösterme")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="c9bbb-339">*IntelliSense 'de kimliği gösterme*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="c9bbb-340">Son eklenen **&lt;form&gt;** öğesini ve içeriğini silin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="c9bbb-341">Görev 2-HTML kod parçacıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="c9bbb-342">HTML5, 25 ' ten fazla yeni anlam etiketi sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="c9bbb-343">Visual Studio 'Da bu etiketler için IntelliSense desteği zaten vardı, ancak Visual Studio 2013 yeni kod parçacıkları ekleyerek biçimlendirme yazmayı daha hızlı ve kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="c9bbb-344">Bu Etiketler karmaşık olmasa da, *Ses* etiketi için doğru codec geri dönüşleri ekleme gibi birkaç küçük alt tleki daha vardır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="c9bbb-345">Bu görevde, ses etiketi için HTML kod parçacıklarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="c9bbb-346">**Index. cshtml** dosyasında, aşağıdaki şekilde gösterildiği gibi **&lt;bölümü&gt;** öğesi içinde **&lt;AUD** yazın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="c9bbb-347">![Ses öğesi ekleme](visual-studio-2013-web-tools/_static/image36.png "Ses öğesi ekleme")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="c9bbb-348">*Ses öğesi ekleme*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="c9bbb-349">**Sekme** tuşuna iki kez basın ve aşağıdaki kodun sayfada nasıl eklendiği ve imlecin ilk kaynağın **src** özniteliğinde nasıl yerleştirildiği hakkında dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="c9bbb-350">**Sekme** tuşuna iki kez basarak kod parçacığı eklenir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="c9bbb-351">Ses parçacığı, gelişmiş destek için iki kaynak dosyası ile *Ses* etiketinin standart kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="c9bbb-352">İkinci satırı silin ve Webkampstv Katana göster: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)için aşağıdaki bağlantıyı kullanarak ilk satırın kaynağını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="c9bbb-353">Sonuç kodu aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="c9bbb-354">Örnek olarak, *Katanaproje. mp3* kaynak dosyası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="c9bbb-355">İsterseniz başka bir kaynak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="c9bbb-356">Dosyayı kaydetmek için **CTRL** + **S** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="c9bbb-357">Uygulamayı başlatmak için **CTRL** + **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="c9bbb-358">Uygulamaya bir ses oyuncusunun eklendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="c9bbb-359">![Internet Explorer 'da ses oynatıcı](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer 'da ses oynatıcı")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="c9bbb-360">*Internet Explorer 'da ses oynatıcı*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="c9bbb-361">![Google Chrome 'da ses oynatıcı](visual-studio-2013-web-tools/_static/image38.png "Google Chrome 'da ses oynatıcı")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="c9bbb-362">*Google Chrome 'da ses oynatıcı*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="c9bbb-363">Tarayıcıları kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-363">Do not close the browsers.</span></span> <span data-ttu-id="c9bbb-364">Bunları bir sonraki görevde kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="c9bbb-365">Görev 3-JavaScript belgelerinde IntelliSense kullanma</span><span class="sxs-lookup"><span data-stu-id="c9bbb-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="c9bbb-366">Web Essentials 2013, stil sayfaları ve HTML sayfaları, kimlikler ve sınıf adlarının bir listesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="c9bbb-367">Bu görevde, bu listelerin Web Essentials 2013 ' de JavaScript IntelliSense desteğini nasıl geliştirdikleri hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="c9bbb-368">**Index. cshtml** dosyasında, JavaScript kodu için bir **komut dosyası** etiketi tanımlamak üzere aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="c9bbb-369">**Komut dosyası** etiketinin içine, Ready geri çağırma işlevini tanımlamak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="c9bbb-370">(Kod parçacığı- *VisualStudio2013WebTooling* - *EX2* - *readyfunction*)</span><span class="sxs-lookup"><span data-stu-id="c9bbb-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="c9bbb-371">Giriş işaretini **betik** etiketine yerleştirip **CTRL** + tuşuna basın **.**</span><span class="sxs-lookup"><span data-stu-id="c9bbb-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="c9bbb-372">öneri menüsünü açmak için.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="c9bbb-373">**Dosyaya Ayıkla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="c9bbb-374">![JavaScript dosya önerisine Ayıkla](visual-studio-2013-web-tools/_static/image39.png "JavaScript dosya önerisine Ayıkla")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="c9bbb-375">*JavaScript dosya önerisine Ayıkla*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="c9bbb-376">**Farklı kaydet** penceresinde, **komut dosyaları** klasörünü seçin, **init. js** dosyasını adlandırın ve **Kaydet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="c9bbb-377">![Pencere olarak kaydet](visual-studio-2013-web-tools/_static/image40.png "Pencere olarak kaydet")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="c9bbb-378">*Pencere olarak kaydet*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9bbb-379">**İnit. js** dosyası oluşturulur ve betiğin içeriği dosyaya taşınır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="c9bbb-380">![Init. js dosyası eklenen içerikle oluşturuldu](visual-studio-2013-web-tools/_static/image41.png "Init. js dosyası eklenen içerikle oluşturuldu")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="c9bbb-381">*Init. js dosyası eklenen içerikle oluşturuldu*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="c9bbb-382">**Index. cshtml** dosyasını açın ve betik etiketinin, **init. js** dosyasına yönelik bir başvuruya göre değiştirildiğini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="c9bbb-383">![Init. js html başvurusu](visual-studio-2013-web-tools/_static/image42.png "Init. js html başvurusu")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="c9bbb-384">*Init. js html başvurusu*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="c9bbb-385">**Çözüm Gezgini** gidin ve **init. js** dosyasının çözüme otomatik olarak eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="c9bbb-386">![Çözüme dahil olan Init. js dosyası](visual-studio-2013-web-tools/_static/image43.png "Çözüme dahil olan Init. js dosyası")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="c9bbb-387">*Çözüme dahil olan Init. js dosyası*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="c9bbb-388">**Hazırlık işlevi geri** aramasını güncelleştirmek için **Init. js** dosyasına dönün.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="c9bbb-389">*Ready*öğesine geçirilen işlev geri çağırma tanımının içinde, tüm öğeleri belirli bir sınıf özniteliğine göre almak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="c9bbb-390">**GetElementsByClassName** işlev çağrısının içindeki tırnak işaretleriyle **CTRL** + **boşluk** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="c9bbb-391">![GetElementsByClassName işlevi için IntelliSense gösteriliyor](visual-studio-2013-web-tools/_static/image44.png "GetElementsByClassName işlevi için IntelliSense gösteriliyor")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="c9bbb-392">*GetElementsByClassName işlevi için IntelliSense gösteriliyor*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9bbb-393">IntelliSense 'in proje stil sayfalarında tanımlanan sınıfları gösterdiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="c9bbb-394">Oluşturduğunuz satırı aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="c9bbb-395">İmleci, **GetElementsByTagName** işlevindeki tekliflerin içinde **au** 'Dan sonra konumlandırın ve **CTRL** + **Space**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="c9bbb-396">![GetElementByTagName yöntemi için IntelliSense gösteriliyor](visual-studio-2013-web-tools/_static/image45.png "GetElementByTagName yöntemi için IntelliSense gösteriliyor")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="c9bbb-397">*GetElementsByTagName yöntemi için IntelliSense gösteriliyor*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="c9bbb-398">Listeden **&quot;ses&quot;** seçin ve **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="c9bbb-399">Sonuç aşağıdaki şekilde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="c9bbb-400">![Ses öğeleri alınıyor](visual-studio-2013-web-tools/_static/image46.png "Ses öğeleri alınıyor")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="c9bbb-401">*Ses öğeleri alınıyor*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="c9bbb-402">**Çözüm Gezgini**' de, **betikler** klasöründeki **init. js** dosyasını sağ tıklatın ve **Web Essentials** menüsünden **JavaScript dosyalarını minbelirt** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="c9bbb-403">![JavaScript dosyalarını minbelirt](visual-studio-2013-web-tools/_static/image47.png "JavaScript dosyalarını minbelirt")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="c9bbb-404">*JavaScript dosyalarını minbelirt*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="c9bbb-405">Kaynak dosya değiştiğinde otomatik olarak küçültmeye izin istendiğinde **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="c9bbb-406">![Otomatik küçültmeye yönelik uyarı etkinleştiriliyor](visual-studio-2013-web-tools/_static/image48.png "Otomatik küçültmeye yönelik uyarı etkinleştiriliyor")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="c9bbb-407">*Otomatik küçültmeye yönelik uyarı etkinleştiriliyor*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9bbb-408">**İnit. min. js** oluşturulur ve **init. js** dosyasının bir bağımlılığı olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="c9bbb-409">![Init. min. js dosyası oluşturuldu](visual-studio-2013-web-tools/_static/image49.png "Init. min. js dosyası oluşturuldu")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="c9bbb-410">*Init. min. js dosyası oluşturuldu*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="c9bbb-411">**İnit. min. js** dosyasını açın ve dosyanın küçültülmüş olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="c9bbb-412">![Init. min. js dosya içeriği](visual-studio-2013-web-tools/_static/image50.png "Init. min. js dosya içeriği")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="c9bbb-413">*Init. min. js dosya içeriği*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="c9bbb-414">**İnit. js** dosyasında, tüm ses öğelerini oynatmak Için **GetElementsByTagName** işlev çağrısının altına aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="c9bbb-415">(Kod parçacığı- *VisualStudio2013WebTooling* - *EX2* - *playaudioelements*)</span><span class="sxs-lookup"><span data-stu-id="c9bbb-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="c9bbb-416">Dosyayı kaydetmek için **CTRL** + **S** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="c9bbb-417">Küçültülmüş dosya zaten açık olduğundan, dosyanın kaynak Düzenleyici dışında değiştirildiğini söyleyen bir iletişim kutusu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="c9bbb-418">**Evet**'i tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-418">Click **Yes**.</span></span>

    <span data-ttu-id="c9bbb-419">![Microsoft Visual Studio uyarısı](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio uyarısı")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="c9bbb-420">*Microsoft Visual Studio uyarısı*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="c9bbb-421">Dosyanın yeni kodla güncelleştirildiğinden emin olmak için **Init. min. js** dosyasına dönün.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="c9bbb-422">![Init. min. js dosyası güncelleştirildi](visual-studio-2013-web-tools/_static/image52.png "Init. min. js dosyası güncelleştirildi")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="c9bbb-423">*Init. min. js dosyası güncelleştirildi*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="c9bbb-424">**Tarayıcı bağlantısı yenileme** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="c9bbb-425">Her iki tarayıcı da yenilendiğinde, önceki görevde gördüğünüz ses oyuncuları otomatik olarak yürütülmeye başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="c9bbb-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="c9bbb-426">![Görünümde ses oynatıcı dahil](visual-studio-2013-web-tools/_static/image53.png "Görünümde ses oynatıcı dahil")</span><span class="sxs-lookup"><span data-stu-id="c9bbb-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="c9bbb-427">*Görünümde ses oynatıcı dahil*</span><span class="sxs-lookup"><span data-stu-id="c9bbb-427">*Audio player included in view*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c9bbb-428">Özet</span><span class="sxs-lookup"><span data-stu-id="c9bbb-428">Summary</span></span>

<span data-ttu-id="c9bbb-429">Bu uygulamalı Laboratuvarı tamamlayarak şu şekilde nasıl yapılacağını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="c9bbb-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="c9bbb-430">Zengin HTML5 kod parçacıkları ve Zen kodlama gibi Web Essentials 'ta bulunan yeni HTML düzenleyici özelliklerini kullanın</span><span class="sxs-lookup"><span data-stu-id="c9bbb-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="c9bbb-431">Renk Seçicisi ve tarayıcı matrisi araç ipucu gibi Web temelleri 'nde bulunan yeni CSS Düzenleyici özelliklerini kullanın</span><span class="sxs-lookup"><span data-stu-id="c9bbb-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="c9bbb-432">Dosyaya Ayıkla ve tüm HTML öğeleri için IntelliSense gibi Web temelleri 'nde bulunan yeni JavaScript Düzenleyici özelliklerini kullanın</span><span class="sxs-lookup"><span data-stu-id="c9bbb-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="c9bbb-433">Tarayıcı bağlantısı kullanarak tarayıcınızla ve Visual Studio arasında veri alışverişi</span><span class="sxs-lookup"><span data-stu-id="c9bbb-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>
