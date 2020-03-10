---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012 ' de ASP.NET ve Web geliştirme yenilikleri | Microsoft Docs
author: rick-anderson
description: Visual Studio 'nun yeni sürümü, Web teknolojileriyle çalışırken deneyim ve performansı iyileştirmeye odaklanan birkaç geliştirme sunar...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525937"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a><span data-ttu-id="d9585-103">Visual Studio 2012'de ASP.NET ve Web Geliştirme Yenilikleri</span><span class="sxs-lookup"><span data-stu-id="d9585-103">What's New in ASP.NET and Web Development in Visual Studio 2012</span></span>

<span data-ttu-id="d9585-104">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="d9585-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="d9585-105">Visual Studio 'nun yeni sürümü, Web teknolojileriyle çalışırken deneyim ve performansı iyileştirmeye odaklanmış bir dizi geliştirme sunar.</span><span class="sxs-lookup"><span data-stu-id="d9585-105">The new version of Visual Studio introduces a number of enhancements focused on improving the experience and performance when working with Web technologies.</span></span> <span data-ttu-id="d9585-106">CSS, JavaScript ve HTML için Visual Studio düzenleyicileri, IntelliSense ve otomatik girintileme gibi en çok isteğe bağlı kod yardımlarının çoğunu kapsayacak şekilde tamamen yeniden belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="d9585-106">Visual Studio Editors for CSS, JavaScript and HTML have been completely revamped to include many of the most in-demand code aids, such as IntelliSense and automatic indentation.</span></span> <span data-ttu-id="d9585-107">Performans, paketleme ve küçültmeye yönelik özellikler artık sayfa yükleme süresini kolayca azaltmak için yerleşik özellikler olarak tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="d9585-107">Regarding performance, bundling and minification are now integrated as built-in features to easily reduce page load time.</span></span>
> 
> <span data-ttu-id="d9585-108">Visual Studio, en son Web sitesi teknolojileriyle çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9585-108">Visual Studio enables you to work with the latest website technologies.</span></span> <span data-ttu-id="d9585-109">Ayrıca, yeni HTML5 öğelerinden ve özelliklerden yararlanarak sitenizin istemci platformundan bağımsız olarak çalıştığından emin olmak için tarayıcılar arası CSS3 kod parçacıklarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-109">You can use cross-browser CSS3 Snippets to make sure your site works regardless of the client platform while also taking advantage of the new HTML5 elements and features.</span></span>
> 
> <span data-ttu-id="d9585-110">JavaScript kodu yazma ve profil oluşturma, bu Visual Studio sürümü ile daha kolay olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d9585-110">Writing and profiling JavaScript code should be easier with this Visual Studio version.</span></span> <span data-ttu-id="d9585-111">IntelliSense listeleri, tümleşik XML belgeleri ve gezinti özellikleri artık JavaScript kodu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d9585-111">IntelliSense lists, integrated XML documentation and navigation features are now available for JavaScript code.</span></span> <span data-ttu-id="d9585-112">Artık JavaScript kataloğu elinizin altında.</span><span class="sxs-lookup"><span data-stu-id="d9585-112">You now have the JavaScript catalog at your fingertips.</span></span> <span data-ttu-id="d9585-113">Ayrıca, betiklerle ECMAScript5 uyumluluğunu denetleyebilir ve sözdizimi hatalarını erken bir aşamada tespit edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-113">Additionally, you can check ECMAScript5 compliance with your scripts and detect syntax errors at an early stage.</span></span>
> 
> <span data-ttu-id="d9585-114">Son olarak, bu Visual Studio sürümü yerleşik paketlemeyi ve küçültmeye göre kullanır.</span><span class="sxs-lookup"><span data-stu-id="d9585-114">Last but not least, this Visual Studio version implements built-in bundling and minification.</span></span> <span data-ttu-id="d9585-115">Betik dosyalarınız ve stil sayfaları, sitenin daha hızlı bir şekilde gerçekleşmesini sağlayacak şekilde paketlenecek ve sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="d9585-115">Your script files and style sheets will be packed and compressed so that the site performs faster.</span></span>
> 
> <span data-ttu-id="d9585-116">Bu laboratuvar, daha önce kaynak klasörde sunulan örnek bir Web uygulamasına küçük değişiklikler uygulayarak açıklanan geliştirmeler ve yeni özellikler konusunda size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="d9585-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="d9585-117">Tüm örnek kod ve kod parçacıkları [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="d9585-117">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="d9585-118">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="d9585-118">Objectives</span></span>

<span data-ttu-id="d9585-119">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="d9585-119">In this hands on lab, you will learn how to:</span></span>

- <span data-ttu-id="d9585-120">CSS düzenleyicisinde yeni özellikleri ve geliştirmeleri kullanın</span><span class="sxs-lookup"><span data-stu-id="d9585-120">Use the new features and improvements in the CSS editor</span></span>
- <span data-ttu-id="d9585-121">HTML düzenleyicisinde yeni özellikleri ve geliştirmeleri kullanın</span><span class="sxs-lookup"><span data-stu-id="d9585-121">Use the new features and improvements in the HTML editor</span></span>
- <span data-ttu-id="d9585-122">JavaScript düzenleyicisinde yeni özellikleri ve geliştirmeleri kullanın</span><span class="sxs-lookup"><span data-stu-id="d9585-122">Use the new features and improvements in the JavaScript editor</span></span>
- <span data-ttu-id="d9585-123">Paketlemeyi ve küçültmeye göre yapılandırma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="d9585-123">Configure and use bundling and minification</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="d9585-124">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d9585-124">Prerequisites</span></span>

- <span data-ttu-id="d9585-125">[Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).</span><span class="sxs-lookup"><span data-stu-id="d9585-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="d9585-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (Kurulum betikleri Için, Windows 8 ve windows Server 2008 R2 'de zaten yüklü)</span><span class="sxs-lookup"><span data-stu-id="d9585-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (for setup scripts - already installed on Windows 8 and Windows Server 2008 R2)</span></span>
- <span data-ttu-id="d9585-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) veya HTML5 uyumlu tarayıcı</span><span class="sxs-lookup"><span data-stu-id="d9585-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) - or an HTML5 compliant browser</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="d9585-128">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="d9585-128">Exercises</span></span>

<span data-ttu-id="d9585-129">Laboratuvar için bu uygulamalı, aşağıdaki alıştırmaları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9585-129">This hands on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="d9585-130">Alıştırma 1: CSS düzenleyicideki yenilikler</span><span class="sxs-lookup"><span data-stu-id="d9585-130">Exercise 1: What's New in the CSS Editor</span></span>](#Exercise1)
2. [<span data-ttu-id="d9585-131">Alıştırma 2: HTML Düzenleyicinizdeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="d9585-131">Exercise 2: What's New in the HTML Editor</span></span>](#Exercise2)
3. [<span data-ttu-id="d9585-132">Alıştırma 3: JavaScript düzenleyicideki yenilikler</span><span class="sxs-lookup"><span data-stu-id="d9585-132">Exercise 3: What's New in the JavaScript Editor</span></span>](#Exercise3)
4. [<span data-ttu-id="d9585-133">Alıştırma 4: paketleme ve Minbirleşme</span><span class="sxs-lookup"><span data-stu-id="d9585-133">Exercise 4: Bundling and Minification</span></span>](#Exercise4)

<span data-ttu-id="d9585-134">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.</span><span class="sxs-lookup"><span data-stu-id="d9585-134">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a><span data-ttu-id="d9585-135">Alıştırma 1: CSS düzenleyicideki yenilikler</span><span class="sxs-lookup"><span data-stu-id="d9585-135">Exercise 1: What's New in the CSS Editor</span></span>

<span data-ttu-id="d9585-136">Web geliştiricileri, CSS düzenlemeyle ilgili birçok zorluklara alışkın olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d9585-136">Web developers should be familiar with many of the difficulties related to CSS editing.</span></span> <span data-ttu-id="d9585-137">CSS stillendirme en büyük sorunlarından biri tarayıcılar arası uyumlulukta olur.</span><span class="sxs-lookup"><span data-stu-id="d9585-137">One of the biggest issues of CSS styling is cross-browser compatibility.</span></span> <span data-ttu-id="d9585-138">Bu, genellikle sitenize Stil uygulandıktan sonra başka bir tarayıcı veya cihazda açtığınızda farklı göründüğünü fark etmeksizin meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="d9585-138">It often happens that, after applying styles to your site, you notice that it looks different if you open it in another browser or device.</span></span> <span data-ttu-id="d9585-139">Bu nedenle, bu görsel sorunları düzeltmek için önemli bir zaman harcayabilir ve son olarak bir tarayıcıda çalıştığını fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-139">Therefore, you may spend a considerable time on fixing those visual issues to realize that, when you finally make it work in one browser, it is broken in the others.</span></span>

<span data-ttu-id="d9585-140">Visual Studio artık geliştiricilerin CSS stil sayfalarını etkin bir şekilde erişmesine, çalışmasına ve düzenlenmesine yardımcı olan özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="d9585-140">Visual Studio now includes features that help developers access, work and organize CSS style sheets effectively.</span></span> <span data-ttu-id="d9585-141">Bu alıştırmada, etkin bir kuruluş ve sürüm için yeni özellikleri ve tarayıcılar arası uyumluluk için CSS3 kod parçacıklarını karşılamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9585-141">Throughout this exercise, you will meet the new features for an effective organization and edition, as well as the CSS3 Code Snippets for cross-browser compatibility.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a><span data-ttu-id="d9585-142">Görev 1-yeni düzenleyici özellikleri</span><span class="sxs-lookup"><span data-stu-id="d9585-142">Task 1 - New Editor Features</span></span>

<span data-ttu-id="d9585-143">Bu görevde, CSS düzenleyicisinin yeni özelliklerini keşfedeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-143">In this task, you will discover the new features of the CSS Editor.</span></span> <span data-ttu-id="d9585-144">Bu yeni düzenleyici, yeni akıllı girintileme, geliştirilmiş kod açıklamaları ve geliştirilmiş IntelliSense listesinden yararlanarak üretkenliğinizi artırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d9585-144">This new editor will help you increase your productivity by taking advantage of the new smart indentation, the improved code comments and the enhanced IntelliSense list.</span></span>

1. <span data-ttu-id="d9585-145">**Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-145">Start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="d9585-146">Çözüm Gezgini, **Stiller** klasörünün altında bulunan **site. css** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-146">In Solution Explorer, open the **Site.css** file located under the **Styles** folder.</span></span> <span data-ttu-id="d9585-147">**Metin düzenleyici** araçlarının araç çubuğunda göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9585-147">Make sure the **Text Editor** tools are visible on the toolbar.</span></span> <span data-ttu-id="d9585-148">Bunu yapmak için, | **araç çubuklarını** **görüntüle** menü seçeneğini belirleyin ve **metin Düzenleyicisi** seçeneklerini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-148">To do that, select the **View** | **Toolbars** menu option, and check the **Text Editor** options.</span></span> <span data-ttu-id="d9585-149">Bu yeni sürüm, **yorum** düğmesi (![açıklama düğmesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)) **ve açıklama düğmesi** (![Açıklama düğmesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)) CSS Düzenleyicisi için de etkinleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9585-149">You will notice that, since this new version, the **Comment** button (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) and the **Uncomment** button (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png) ) are also enabled for the CSS editor.</span></span>

    <span data-ttu-id="d9585-150">![Düzenleyici ve CSS araçlarını etkinleştirme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Düzenleyici ve CSS araçlarını etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="d9585-150">![Enabling Editor and CSS Tools](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Enabling Editor and CSS Tools")</span></span>

    <span data-ttu-id="d9585-151">*Düzenleyici ve CSS araçlarını etkinleştirme*</span><span class="sxs-lookup"><span data-stu-id="d9585-151">*Enabling Editor and CSS Tools*</span></span>
3. <span data-ttu-id="d9585-152">Kodu kaydırın ve herhangi bir CSS sınıfı tanımını seçin.</span><span class="sxs-lookup"><span data-stu-id="d9585-152">Scroll the code and select any CSS class definition.</span></span> <span data-ttu-id="d9585-153">Seçili satırları \*\*açıklamaya yönelik açıklama (![** yorum-düğme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-153">Click the **Comment** (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) button to comment the selected lines.</span></span> <span data-ttu-id="d9585-154">Ardından, değişiklikleri geri almak için **Açıklama** (![açıklama/adım](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-154">Then, click the **Uncomment** (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) button to undo the changes.</span></span>
4. <span data-ttu-id="d9585-155">**Daraltma** (![daraltma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) **) ve metnin** sol kenar boşluğunda bulunan (![Genişlet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)) düğmeleri ' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-155">Click the **Collapse** (![collapse](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) and **Expand** (![expand](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) buttons located on the left margin of the text.</span></span> <span data-ttu-id="d9585-156">Artık, daha temiz bir görünüm sağlamak için kullandığınız stilleri gizleyebildiğinize dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-156">Notice that you can now hide the styles you don't use to have a cleaner view.</span></span>

    <span data-ttu-id="d9585-157">![CSS sınıflarını daraltma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "CSS sınıflarını daraltma")</span><span class="sxs-lookup"><span data-stu-id="d9585-157">![Collapsing CSS classes](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Collapsing CSS classes")</span></span>

    <span data-ttu-id="d9585-158">*CSS sınıflarını daraltma*</span><span class="sxs-lookup"><span data-stu-id="d9585-158">*Collapsing CSS classes*</span></span>
5. <span data-ttu-id="d9585-159">Akıllı girintileme özelliğinin etkinleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9585-159">Make sure that the smart indentation feature is enabled.</span></span> <span data-ttu-id="d9585-160">**Araçlar** | **Seçenekler** menü seçeneğini belirleyin ve ardından ekranın sol bölmesindeki **metin düzenleyici** | **CSS** | **biçimlendirme** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d9585-160">Select the **Tools** | **Options** menu option, and then select the **Text Editor** | **CSS** | **Formatting** page in the left pane of the screen.</span></span> <span data-ttu-id="d9585-161">**Hiyerarşik girintileme** seçeneğini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-161">Check the **Hierarchical indentation** option.</span></span>

    <span data-ttu-id="d9585-162">![Hiyerarşik girintileme etkinleştiriliyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Hiyerarşik girintileme etkinleştiriliyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-162">![Enabling hierarchical indentation](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Enabling hierarchical indentation")</span></span>

    <span data-ttu-id="d9585-163">*Hiyerarşik girintileme etkinleştiriliyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-163">*Enabling hierarchical indentation*</span></span>
6. <span data-ttu-id="d9585-164">Ana sınıf tanımını (. Main) bulun ve div öğelerine bir stil ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-164">Locate the main class definition (.main) and append a style to the div elements.</span></span> <span data-ttu-id="d9585-165">Kodun otomatik olarak hizalandığını fark edersiniz. Bu, kullanıcıların üst sınıfları bir bakışta bulmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d9585-165">You will notice that the code aligns automatically, helping users to find the parent classes at a glance.</span></span>

    <span data-ttu-id="d9585-166">CSS</span><span class="sxs-lookup"><span data-stu-id="d9585-166">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    <span data-ttu-id="d9585-167">![CSS 'de hiyerarşik hizalama](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS 'de hiyerarşik hizalama")</span><span class="sxs-lookup"><span data-stu-id="d9585-167">![Hierarchical alignment in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchical alignment in CSS")</span></span>

    <span data-ttu-id="d9585-168">*CSS 'de hiyerarşik hizalama*</span><span class="sxs-lookup"><span data-stu-id="d9585-168">*Hierarchical alignment in CSS*</span></span>
7. <span data-ttu-id="d9585-169">**. Main div** sınıfı içinde, kenarlığın sonundaki imleci bulun **: 0px;** ve IntelliSense listesini göstermek için **ENTER** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-169">Inside **.main div** class, locate the cursor at the end of **border: 0px;** and press **Enter** to display the IntelliSense list.</span></span> <span data-ttu-id="d9585-170">**Üste** yazmaya başlayın ve siz yazarken listenin nasıl filtrelendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-170">Start typing **top** and notice how the list is filtered as you type.</span></span> <span data-ttu-id="d9585-171">Listede, sözcüğün herhangi bir bölümünde **üst** olan öğeler görüntülenir (Visual Studio 'nun önceki sürümlerinde, liste terimle *başlayan* öğelere göre filtrelenir).</span><span class="sxs-lookup"><span data-stu-id="d9585-171">The list will display the elements that contain **top** at any part of the word (In prior versions of Visual Studio, the list is filtered by the items that *begin* with the term).</span></span>

    <span data-ttu-id="d9585-172">![CSS 'de IntelliSense geliştirmeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS 'de IntelliSense geliştirmeleri")</span><span class="sxs-lookup"><span data-stu-id="d9585-172">![IntelliSense enhancements in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "IntelliSense enhancements in CSS")</span></span>

    <span data-ttu-id="d9585-173">*CSS 'de IntelliSense geliştirmeleri*</span><span class="sxs-lookup"><span data-stu-id="d9585-173">*IntelliSense enhancements in CSS*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a><span data-ttu-id="d9585-174">Görev 2-renk seçici</span><span class="sxs-lookup"><span data-stu-id="d9585-174">Task 2 - The Color Picker</span></span>

<span data-ttu-id="d9585-175">Bu görevde, Visual Studio IntelliSense ile tümleştirilmiş yeni CSS renk seçiciyi keşfedeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-175">In this task, you will discover the new CSS Color Picker integrated into Visual Studio IntelliSense.</span></span>

1. <span data-ttu-id="d9585-176">**Site. css ' de,** üstbilgi sınıfı tanımını (. Header) bulun ve imleci &quot;:&quot; ve Bu kod satırındaki &quot; karakter &quot;# **.**</span><span class="sxs-lookup"><span data-stu-id="d9585-176">In **Site.css,** locate the header class definition (.header) and place the cursor next to **background-color** attribute, between the &quot;:&quot; and &quot;#&quot; characters on that line of code **.**</span></span>

    <span data-ttu-id="d9585-177">![İmleci bulma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "İmleci bulma")</span><span class="sxs-lookup"><span data-stu-id="d9585-177">![Locating the cursor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Locating the cursor")</span></span>

    <span data-ttu-id="d9585-178">*İmleci bulma*</span><span class="sxs-lookup"><span data-stu-id="d9585-178">*Locating the cursor*</span></span>
2. <span data-ttu-id="d9585-179">**İki nokta üst üste** (:) ve renk seçiciyi göstermek için yeniden yazın.</span><span class="sxs-lookup"><span data-stu-id="d9585-179">Delete the **colon** (:) and write it again to display the color picker.</span></span> <span data-ttu-id="d9585-180">Göreceğiniz ilk renklerin sitenizin en sık kullanılan renkleriyle olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-180">Notice that the first colors you will see are the most frequent colors of your site.</span></span> <span data-ttu-id="d9585-181">Beyaz renge tıklarsanız, HTML renk kodu (#fff), stil sayfasındaki geçerli renk kodunun yerini alır.</span><span class="sxs-lookup"><span data-stu-id="d9585-181">If you click the white color, its HTML color code (#fff) will replace the current color code in the stylesheet.</span></span>

    <span data-ttu-id="d9585-182">![Renk seçici](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Renk seçici")</span><span class="sxs-lookup"><span data-stu-id="d9585-182">![Color picker](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span></span>

    <span data-ttu-id="d9585-183">*Renk seçici*</span><span class="sxs-lookup"><span data-stu-id="d9585-183">*Color picker*</span></span>
3. <span data-ttu-id="d9585-184">Renk degradesini göstermek için renk seçicisindeki **genişletme** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)) düğmesine basın ve ardından farklı bir renk seçmek için gradyan imlecini sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-184">Press the **Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) button on the color picker to display the color gradient, and then drag the gradient cursor to select a different color.</span></span> <span data-ttu-id="d9585-185">Bundan sonra, **damlalık** düğmesine tıklayın ve ekrandaki herhangi bir rengi seçin.</span><span class="sxs-lookup"><span data-stu-id="d9585-185">After that, click the **Eyedropper** button and select any color from the screen.</span></span> <span data-ttu-id="d9585-186">İmleci taşırken arka plan rengi değerinin dinamik olarak değiştiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-186">Notice that background color value changes dynamically while you move the cursor.</span></span>

    <span data-ttu-id="d9585-187">![Renk seçici gradyanı](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Renk seçici gradyanı")</span><span class="sxs-lookup"><span data-stu-id="d9585-187">![Color picker gradient](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Color picker gradient")</span></span>

    <span data-ttu-id="d9585-188">*Renk seçici gradyanı*</span><span class="sxs-lookup"><span data-stu-id="d9585-188">*Color picker gradient*</span></span>
4. <span data-ttu-id="d9585-189">**Opaklık kaydırıcısının** saydamlığını azaltmak için seçiciyi çubuğun ortasına taşıyın.</span><span class="sxs-lookup"><span data-stu-id="d9585-189">In the **Opacity** slider, move the selector to the center of the bar to reduce the opacity.</span></span> <span data-ttu-id="d9585-190">Arka plan rengi değerinin artık ölçeğini RGBA olarak değiştirdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-190">Notice that background-color value now changes its scale to RGBA.</span></span>

    <span data-ttu-id="d9585-191">![Renk seçici geçirgenliği](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Renk seçici geçirgenliği")</span><span class="sxs-lookup"><span data-stu-id="d9585-191">![Color picker Opacity](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Color picker Opacity")</span></span>

    <span data-ttu-id="d9585-192">*Renk seçici geçirgenliği*</span><span class="sxs-lookup"><span data-stu-id="d9585-192">*Color picker Opacity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-193">CSS3 ' deki RGBA (kırmızı, yeşil, mavi, alfa) renk tanımı, tek bir öğe için renk opaklık değerini tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9585-193">The RGBA (Red, Green, Blue, Alpha) color definition in CSS3 enables you to define the color opacity value for a single item.</span></span> <span data-ttu-id="d9585-194">**Opaklığın** aksine, RGBA renkleri **-** benzer bir CSS özniteliği de en son tarayıcılarla uyumludur.</span><span class="sxs-lookup"><span data-stu-id="d9585-194">Unlike **opacity -** a similar CSS attribute **-** RGBA colors are also compatible with the latest browsers.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a><span data-ttu-id="d9585-195">Görev 3-CSS uyumlu kod parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d9585-195">Task 3 - CSS Compatible Code Snippets</span></span>

<span data-ttu-id="d9585-196">Bu görevde, Web sitenizde bazı özellikler uygulamak için tarayıcılar arası uyumlu CSS3 parçacıklarını nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-196">In this task, you will learn how to use cross-browser compatible CSS3 snippets in order to implement some features in your website.</span></span>

1. <span data-ttu-id="d9585-197">**Site. css** dosyasında **üst bilgi** CSS sınıf tanımını (. Header) bulun ve imleci **/\*Border Radius /\*** yeni bir kod parçacığı eklemek için buraya yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9585-197">In the **Site.css** file, locate the **header** CSS class definition (.header) and place the cursor below the **/\*border radius\*/** placeholder to add a new snippet.</span></span> <span data-ttu-id="d9585-198">IntelliSense listesini göstermek için **ENTER** tuşuna basın ve listeyi filtrelemek için **RADIUS** yazın.</span><span class="sxs-lookup"><span data-stu-id="d9585-198">Press **Enter** to display the IntelliSense list and type **radius** to filter the list.</span></span> <span data-ttu-id="d9585-199">Bir çift tıklama ile listeden **Border-Radius** seçeneğini seçin ve ardından parçacığı eklemek için **sekme** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-199">Select the **border-radius** option from the list with a double click, and then press the **TAB** key to insert the snippet.</span></span> <span data-ttu-id="d9585-200">Sonra, piksel cinsinden bir yarıçap boyutu yazın ve **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-200">Then, type a radius size in pixels and press **Enter**.</span></span> <span data-ttu-id="d9585-201">Örneğin, **15 piksel**yazın.</span><span class="sxs-lookup"><span data-stu-id="d9585-201">For instance, type **15px**.</span></span>

    <span data-ttu-id="d9585-202">Kod parçacığı tarafından eklenen CSS3 öznitelikleri, Mozilla ve WebKit tabanlı tarayıcılar dahil olmak üzere çoğu HTML5 uyumluluk tarayıcılarında yuvarlatılmış kenarlıkları işler.</span><span class="sxs-lookup"><span data-stu-id="d9585-202">The CSS3 attributes added by the snippet will render rounded borders in most HTML5 compliance browsers, including Mozilla and WebKit-based browsers.</span></span>

    <span data-ttu-id="d9585-203">![Border-Radius parçacığı kullanma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Border-Radius parçacığı kullanma")</span><span class="sxs-lookup"><span data-stu-id="d9585-203">![Using a border-radius snippet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Using a border-radius snippet")</span></span>

    <span data-ttu-id="d9585-204">*Border-Radius parçacığı kullanma*</span><span class="sxs-lookup"><span data-stu-id="d9585-204">*Using a border-radius snippet*</span></span>
2. <span data-ttu-id="d9585-205">Sayfa stilinde (. Page) aynı **Kenarlık** parçacıklarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-205">Apply the same **border** snippets in the page style (.page).</span></span>

    <span data-ttu-id="d9585-206">CSS</span><span class="sxs-lookup"><span data-stu-id="d9585-206">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. <span data-ttu-id="d9585-207">Çözümü çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-207">Press **F5** to run the solution.</span></span> <span data-ttu-id="d9585-208">Her sayfanın artık kenarlığı yuvarlatılmış olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-208">Notice that each page now has rounded borders.</span></span>

    <span data-ttu-id="d9585-209">![Yuvarlak köşeler](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Yuvarlak köşeler")</span><span class="sxs-lookup"><span data-stu-id="d9585-209">![Rounded corners](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Rounded corners")</span></span>

    <span data-ttu-id="d9585-210">*Yuvarlak köşeler*</span><span class="sxs-lookup"><span data-stu-id="d9585-210">*Rounded corners*</span></span>
4. <span data-ttu-id="d9585-211">Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="d9585-211">Close the browser and return to Visual Studio.</span></span>
5. <span data-ttu-id="d9585-212">**Stiller** klasörünün altında bulunan **Custom. css** dosyasını açın ve imleci **div. Images ul li img** Class tanımının içine yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9585-212">Open the **Custom.css** file located under the **Styles** folder and place the cursor inside **div.images ul li img** class definition.</span></span>
6. <span data-ttu-id="d9585-213">IntelliSense listesini göstermek için ENTER tuşuna basın, **Box-Shadow** yazın ve varsayılan gölge kod parçacığını sınıf tanımının içine eklemek için **Tab** tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-213">Press enter to display the IntelliSense list, type **box-shadow** and press the **TAB** key twice to insert the default shadow code snippet inside the class definition.</span></span> <span data-ttu-id="d9585-214">Gölge değerlerini **10px 10px 5px #888**olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-214">Set the shadow values to **10px 10px 5px #888**.</span></span> <span data-ttu-id="d9585-215">Ardından **Border-Radius** yazın ve kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-215">Then, type **border-radius** and insert the code snippet.</span></span> <span data-ttu-id="d9585-216">Yarıçap boyutunu ayarlamak için **15 piksel** yazın ve **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-216">Type **15px** to set radius size and press **ENTER**.</span></span>

    <span data-ttu-id="d9585-217">![Gölgeli yuvarlak köşeler](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Gölgeli yuvarlak köşeler")</span><span class="sxs-lookup"><span data-stu-id="d9585-217">![Rounded corners with shadow](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Rounded corners with shadow")</span></span>

    <span data-ttu-id="d9585-218">*Gölgeli yuvarlak köşeler*</span><span class="sxs-lookup"><span data-stu-id="d9585-218">*Rounded corners with shadow*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-219">Bu anda, Mozilla ve WebKit (Chrome, Safari, Konkeror) tarayıcılarını desteklemek için ilgili önek (Moz, WebKit, o) ile birlikte Shadow özniteliği eklenir.</span><span class="sxs-lookup"><span data-stu-id="d9585-219">At this moment, the shadow attribute is inserted with the corresponding prefix (moz, webkit, o) to support Mozilla and Webkit (Chrome, Safari, Konkeror) browsers.</span></span>
7. <span data-ttu-id="d9585-220">Yeni bir sınıf **div oluşturun. bu görüntüleri ul li img:** **div. Images ul li img** Class tanımının altına gelin ve imleci köşeli ayracın içine yerleştirin **.**</span><span class="sxs-lookup"><span data-stu-id="d9585-220">Create a new class **div.images ul li img:hover** below the **div.images ul li img** class definition and place the cursor inside the brackets **.**</span></span>

    <span data-ttu-id="d9585-221">CSS</span><span class="sxs-lookup"><span data-stu-id="d9585-221">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. <span data-ttu-id="d9585-222">Dönüştürme kod parçacığını eklemek için **Dönüştür** yazın ve **Tab** tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-222">Type **transform** and press the **TAB** key twice in order to insert the transform snippet.</span></span> <span data-ttu-id="d9585-223">Ardından, görüntülerin üzerine gelindiğinde döndürme açısı değerini değiştirmek için **döndürme (-15deg)** girin.</span><span class="sxs-lookup"><span data-stu-id="d9585-223">Then, enter **rotate(-15deg)** to change the rotation angle value when images are hovered.</span></span>

    <span data-ttu-id="d9585-224">CSS</span><span class="sxs-lookup"><span data-stu-id="d9585-224">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. <span data-ttu-id="d9585-225">**F5** tuşuna basarak çözümü ÇALıŞTıRıN ve CSS3 sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="d9585-225">Press **F5** to run the solution and browse to the CSS3 page.</span></span> <span data-ttu-id="d9585-226">Görüntülerin köşeleri ve kutu gölgeleri yuvarlatılmış olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-226">Notice that the images have rounded corners and box shadows.</span></span> <span data-ttu-id="d9585-227">Fareyi görüntülerin üzerine getirin ve döndürmeyi izleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-227">Hover the mouse over the images and watch them rotate.</span></span>

    <span data-ttu-id="d9585-228">![Görüntü döndürme parçacığı dönüştürme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Görüntü döndürme parçacığı dönüştürme")</span><span class="sxs-lookup"><span data-stu-id="d9585-228">![Transform snippet rotating an image](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transform snippet rotating an image")</span></span>

    <span data-ttu-id="d9585-229">*Görüntü döndürme parçacığı dönüştürme*</span><span class="sxs-lookup"><span data-stu-id="d9585-229">*Transform snippet rotating an image*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-230">Internet Explorer 10 kullanıyorsanız ve gölgeleri göremiyorsanız, belge modunun ıE10 standartları olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9585-230">If you are using Internet Explorer 10 and cannot see the shadows, make sure the document mode is set to IE10 standards.</span></span> <span data-ttu-id="d9585-231">Internet Explorer Geliştirici Araçları 'nı açmak için **F12** tuşuna basın ve IE10 standartlarına geçmek Için **belge modu** ' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-231">Press **F12** to open Internet Explorer developer tools and click **Document Mode** to change to IE10 standards.</span></span>

    ![yaklaşık-US](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a><span data-ttu-id="d9585-233">Alıştırma 2: HTML Düzenleyicinizdeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="d9585-233">Exercise 2: What's New in the HTML Editor</span></span>

<span data-ttu-id="d9585-234">Visual Studio 'Nun gelişmiş bir HTML Düzenleyicisi vardır.</span><span class="sxs-lookup"><span data-stu-id="d9585-234">Visual Studio has an improved HTML editor.</span></span> <span data-ttu-id="d9585-235">Bu sürüme dahil olan geliştirmelerden bazıları HTML belgelerindeki akıllı girintileme, HTML5 parçacıkları, HTML başlangıç ve bitiş etiketi eşleştirmesi ve HTML doğrulaması ' na sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d9585-235">Some of the enhancements included in this version are smart indentation in HTML documents, HTML5 snippets, HTML start and end tag matching, and HTML validation.</span></span> <span data-ttu-id="d9585-236">Bu alıştırmada, Web sitesi biçimlendirmesinde çalışırken bu değişikliklerin akıcı bir şekilde nasıl iyileştirebileceğinizi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-236">Throughout this exercise, you will see how these changes improve your fluency when working in the website markup.</span></span>

<span data-ttu-id="d9585-237">CSS Düzenleyicisi gibi, HTML Düzenleyicisi de geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d9585-237">Like the CSS editor, the HTML editor was also improved.</span></span> <span data-ttu-id="d9585-238">Bu geliştirmelerin çoğu, Web geliştiricisi ömrünü daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="d9585-238">Most of these improvements are small ones that make the Web developer's life easier.</span></span> <span data-ttu-id="d9585-239">HTML belgesi DOCTYPE 'ı hedeflemek ve doğrulamak için kod parçacıkları, akıllı girintileme, eşleşen başlangıç ve bitiş etiketleri gibi şeyler bu geliştirmelerden bazılarıdır.</span><span class="sxs-lookup"><span data-stu-id="d9585-239">Things like more code snippets for HTML5, smart indentation, matching start and end tags when editing and validation targeting the HTML document DOCTYPE are some of these improvements.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a><span data-ttu-id="d9585-240">Görev 1-Iyileştirilmiş DOCTYPE doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d9585-240">Task 1 - Improved DOCTYPE Validation</span></span>

<span data-ttu-id="d9585-241">Bu, tanım ana sayfada olsa da, HTML Düzenleyicisi artık sayfanızın DOCTYPE 'ı kontrol edebilir.</span><span class="sxs-lookup"><span data-stu-id="d9585-241">The HTML editor now has the ability to check the DOCTYPE of your page, even though the definition might be in the master page.</span></span> <span data-ttu-id="d9585-242">Sayfanızın DOCTYPE öğesine bağlı olarak, HTML Düzenleyicisi doğru kurallar kümesiyle doğrulanır ve IntelliSense listesini, DOCTYPE öğelerini ele alacak şekilde filtreleyecek.</span><span class="sxs-lookup"><span data-stu-id="d9585-242">Depending on the DOCTYPE of your page, the HTML editor will validate with the correct set of rules and will filter the IntelliSense list considering the DOCTYPE elements.</span></span>

<span data-ttu-id="d9585-243">Bu görevde, HTML Düzenleyicisi davranışının uygun şekilde nasıl değiştiği görmek için bir sayfanın DOCTYPE öğesini değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-243">In this task, you will change the DOCTYPE of a page to see how the HTML editor behavior changes accordingly.</span></span>

1. <span data-ttu-id="d9585-244">Zaten açık değilse, **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-244">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="d9585-245">**Site. Master** sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-245">Open the **Site.Master** page.</span></span>
3. <span data-ttu-id="d9585-246">Doğrulama araç çubuğunun hedef şemasına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-246">Notice the Target Schema for Validation Toolbar.</span></span> <span data-ttu-id="d9585-247">HTML düzenleyicisinin davranış şekli (doğrulama, IntelliSense, vb.), seçilen doctype öğesine uyacak şekilde düzgün şekilde değişir.</span><span class="sxs-lookup"><span data-stu-id="d9585-247">The way the HTML editor behaves (Validation, IntelliSense, etc.) will properly change to fit the Doctype selected.</span></span>

    <span data-ttu-id="d9585-248">![HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın")</span><span class="sxs-lookup"><span data-stu-id="d9585-248">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="d9585-249">*HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın*</span><span class="sxs-lookup"><span data-stu-id="d9585-249">*Use Doctype in HTML Source Editing toolbar*</span></span>
4. <span data-ttu-id="d9585-250">Hedef şemayı HTML 4,01 olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d9585-250">Change the Target Schema to HTML 4.01.</span></span>

    <span data-ttu-id="d9585-251">![HTML kaynak düzenlemesi araç çubuğunda DOCTYPE 'ı değiştirme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML kaynak düzenlemesi araç çubuğunda DOCTYPE 'ı değiştirme")</span><span class="sxs-lookup"><span data-stu-id="d9585-251">![Changing Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Changing Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="d9585-252">*HTML kaynak düzenlemesi araç çubuğunda DOCTYPE 'ı değiştirme*</span><span class="sxs-lookup"><span data-stu-id="d9585-252">*Changing Doctype in HTML Source Editing toolbar*</span></span>
5. <span data-ttu-id="d9585-253">İmleci **gövde** öğesinin altına YERLEŞTIRIN ve HTML5 öğesinin adını yazmaya başlayın (örneğin, **video**).</span><span class="sxs-lookup"><span data-stu-id="d9585-253">Place the cursor under the **body** element, and start typing the name of an HTML5 element (for example, **video**).</span></span> <span data-ttu-id="d9585-254">Öğesinin IntelliSense listesinde mevcut olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-254">Notice that the element is not available in the IntelliSense list.</span></span>

    <span data-ttu-id="d9585-255">![HTML5 öğeleri listelenmemiş](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 öğeleri listelenmemiş")</span><span class="sxs-lookup"><span data-stu-id="d9585-255">![HTML5 elements not listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 elements not listed")</span></span>

    <span data-ttu-id="d9585-256">*HTML5 öğeleri listelenmemiş*</span><span class="sxs-lookup"><span data-stu-id="d9585-256">*HTML5 elements not listed*</span></span>
6. <span data-ttu-id="d9585-257">Doğrulama araç çubuğunun hedef şemasında yapılan değişiklikleri geri almak için, açılan listeden DOCTYPE: XHTML5 öğesini seçerek.</span><span class="sxs-lookup"><span data-stu-id="d9585-257">Undo the changes to the Target Schema for Validation Toolbar, picking DOCTYPE: XHTML5 from the dropdown list.</span></span>

    <span data-ttu-id="d9585-258">![HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın")</span><span class="sxs-lookup"><span data-stu-id="d9585-258">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="d9585-259">*HTML kaynak düzenlemesi araç çubuğunda DOCTYPE 'ı Sıfırla*</span><span class="sxs-lookup"><span data-stu-id="d9585-259">*Reset Doctype in HTML Source Editing toolbar*</span></span>
7. <span data-ttu-id="d9585-260">İmleci **gövde** öğesinin altına YERLEŞTIRIN ve HTML5 öğesini yeniden yazmaya başlayın (örneğin, **video**gibi).</span><span class="sxs-lookup"><span data-stu-id="d9585-260">Place the cursor under the **body** element and start typing an HTML5 element again (For example, like **video**).</span></span> <span data-ttu-id="d9585-261">HTML5 öğelerinin artık IntelliSense listesinde kullanılabilir olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-261">Notice that the HTML5 elements are now available in the IntelliSense list.</span></span>

    <span data-ttu-id="d9585-262">![Listelenen HTML5 öğeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "Listelenen HTML5 öğeleri")</span><span class="sxs-lookup"><span data-stu-id="d9585-262">![HTML5 elements being listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "HTML5 elements being listed")</span></span>

    <span data-ttu-id="d9585-263">*Listelenen HTML5 öğeleri*</span><span class="sxs-lookup"><span data-stu-id="d9585-263">*HTML5 elements being listed*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a><span data-ttu-id="d9585-264">Görev 2-başlangıç/bitiş etiketleri otomatik güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d9585-264">Task 2 - Start/End Tags Automatic Update</span></span>

<span data-ttu-id="d9585-265">Visual Studio artık, düzenlemekte olduğunuz öğenin HTML açılış veya kapanış etiketlerini birbirleriyle eşleşecek şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d9585-265">Visual Studio now updates the HTML opening or closing tags of the element that you are editing to match each other.</span></span> <span data-ttu-id="d9585-266">Bu yeni özellik, HTML etiketlerini düzenlenirken üretkenliğinizi artırır.</span><span class="sxs-lookup"><span data-stu-id="d9585-266">This new feature will improve your productivity when editing HTML tags.</span></span>

1. <span data-ttu-id="d9585-267">**Default. aspx** sayfasında, başlıklı bir **H3** öğesi ekleyin (örneğin, Visual Studio 2012 Rok!).</span><span class="sxs-lookup"><span data-stu-id="d9585-267">On the **Default.aspx** page, add an **H3** element with a title (for example, Visual Studio 2012 Rocks!).</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. <span data-ttu-id="d9585-268">**H3** etiketini değiştirin ve **H2** veya H1 yazın **.**</span><span class="sxs-lookup"><span data-stu-id="d9585-268">Change the **H3** tag and type **H2** or **H1.**</span></span>

    <span data-ttu-id="d9585-269">Bitiş etiketinin otomatik olarak güncelleştirdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-269">Notice that the end tag automatically updates.</span></span> <span data-ttu-id="d9585-270">Başlangıç etiketinin de aynı şekilde güncelleştii görmek için bitiş etiketini de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-270">You can also modify the end tag to see that the start tag updates accordingly too.</span></span>

    <span data-ttu-id="d9585-271">![Bitiş etiketinin otomatik güncelleştirilmesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Bitiş etiketinin otomatik güncelleştirilmesi")</span><span class="sxs-lookup"><span data-stu-id="d9585-271">![Automatic update of the end tag](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatic update of the end tag")</span></span>

    <span data-ttu-id="d9585-272">*Bitiş etiketinin otomatik güncelleştirilmesi*</span><span class="sxs-lookup"><span data-stu-id="d9585-272">*Automatic update of the end tag*</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a><span data-ttu-id="d9585-273">Görev 3-yeni HTML5 kod parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d9585-273">Task 3 - New HTML5 Code Snippets</span></span>

<span data-ttu-id="d9585-274">Visual Studio artık birkaç HTML5 kod parçacığı içerir.</span><span class="sxs-lookup"><span data-stu-id="d9585-274">Visual Studio now includes several HTML5 code snippets.</span></span> <span data-ttu-id="d9585-275">Bu görevde, bu kod parçacıklarında bazılarını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d9585-275">In this task, you will use some of these snippets.</span></span>

1. <span data-ttu-id="d9585-276">Web sitesi klasörünün köküne **Ses** adlı yeni bir klasör ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-276">Add a new folder named **audio** to the root of the web site folder.</span></span> <span data-ttu-id="d9585-277">Windows Gezgini 'ni açın ve tüm ses dosyalarını **WhatsNewASPNET. sln** çözümünün **Ses** klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-277">Open Windows Explorer and copy any audio file into the **audio** folder of the **WhatsNewASPNET.sln** solution.</span></span>
2. <span data-ttu-id="d9585-278">**Default. aspx** sayfasında, Web11 Rosin!! altındaki imleci bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-278">In the **Default.aspx** page, locate the cursor under the Web11 Rocks!!</span></span> <span data-ttu-id="d9585-279">Üst bilgi.</span><span class="sxs-lookup"><span data-stu-id="d9585-279">Header.</span></span> <span data-ttu-id="d9585-280">**Ses** YAZıN ve Tab tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-280">Type **audio** and press the TAB key.</span></span>

    <span data-ttu-id="d9585-281">Yeni HTML Düzenleyicisi HTML5 içeriğine yönelik kod parçacıklarını içerir.</span><span class="sxs-lookup"><span data-stu-id="d9585-281">The new HTML editor includes code snippets for HTML5 content.</span></span> <span data-ttu-id="d9585-282">HTML5 parçacıklarını etkinleştirmek için uygun DOCTYPE tanımını kullanmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-282">Remember to use the proper DOCTYPE definition to enable the HTML5 snippets.</span></span>

    <span data-ttu-id="d9585-283">![HTML5 kod parçacıkları ekleme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "HTML5 kod parçacıkları ekleme")</span><span class="sxs-lookup"><span data-stu-id="d9585-283">![Inserting HTML5 Code Snippets](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Inserting HTML5 Code Snippets")</span></span>

    <span data-ttu-id="d9585-284">*HTML5 kod parçacıkları ekleme*</span><span class="sxs-lookup"><span data-stu-id="d9585-284">*Inserting HTML5 Code Snippets*</span></span>
3. <span data-ttu-id="d9585-285">Ses kaynağını, var olan bir ses dosyasına işaret etmek üzere güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9585-285">Update the audio source to point to an existing audio file.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > <span data-ttu-id="d9585-286">Bu çözüme ses dosyası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9585-286">You will need to add the audio file to the solution.</span></span>
4. <span data-ttu-id="d9585-287">Siteyi çalıştırmak ve sesi oynatmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-287">Press **F5** to run the site and play the audio.</span></span>

    <span data-ttu-id="d9585-288">![Ses denetimini çalıştırma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Ses denetimini çalıştırma")</span><span class="sxs-lookup"><span data-stu-id="d9585-288">![Running the audio control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Running the audio control")</span></span>

    <span data-ttu-id="d9585-289">*Ses denetimini çalıştırma*</span><span class="sxs-lookup"><span data-stu-id="d9585-289">*Running the audio control*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-290">Visual Studio 'da video, şekil vb. dahil olmak üzere daha fazla kod parçacığı de deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-290">You can also try more snippets included in Visual Studio, such as video, figure, etc.</span></span>
5. <span data-ttu-id="d9585-291">Şimdi sayfanın bazı bölümünde bir denetim eklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-291">Now, try to insert a control in some part of the page.</span></span> <span data-ttu-id="d9585-292">Örneğin, bir **GridView** denetimi eklemeyi deneyin, ancak **&lt;oyutlandır** yazmak yerine **GV&lt;** yazmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-292">For example, try to insert a **GridView** control, but instead of typing **&lt;Gri,** start typing **&lt;GV**.</span></span> <span data-ttu-id="d9585-293">IntelliSense listesinde **ASP: GridView** denetimi gösterildiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-293">Notice that the IntelliSense list shows the **asp:GridView** control.</span></span>

    <span data-ttu-id="d9585-294">HTML düzenleyicisinde IntelliSense artık başlık büyük-küçük harf araması ve kısmi eşleştirme (terimi içeren tüm öğeleri alma) sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9585-294">IntelliSense in the HTML Editor now provides title-casing search, as well as partial matching (retrieving all elements that contains the term).</span></span>

    <span data-ttu-id="d9585-295">![IntelliSense listeleriyle GridView ekleme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "IntelliSense listeleriyle GridView ekleme")</span><span class="sxs-lookup"><span data-stu-id="d9585-295">![Inserting a GridView with IntelliSense lists](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Inserting a GridView with IntelliSense lists")</span></span>

    <span data-ttu-id="d9585-296">*IntelliSense listeleriyle GridView ekleme*</span><span class="sxs-lookup"><span data-stu-id="d9585-296">*Inserting a GridView with IntelliSense lists*</span></span>

    <span data-ttu-id="d9585-297">**&lt;Grid** yazarsanız, terimiyle eşleşen tüm öğeleri alırsınız, ancak Visual Studio **GridView** denetimini önerir:</span><span class="sxs-lookup"><span data-stu-id="d9585-297">If you type **&lt;grid** you will get all the items that match the term, but Visual Studio will suggest the **gridview** control:</span></span>

    <span data-ttu-id="d9585-298">![IntelliSense listeleriyle bir GridView ekleme ve kısmi eşleştirme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "IntelliSense listeleriyle bir GridView ekleme ve kısmi eşleştirme")</span><span class="sxs-lookup"><span data-stu-id="d9585-298">![Inserting a GridView with IntelliSense lists and partial matching](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Inserting a GridView with IntelliSense lists and partial matching")</span></span>

    <span data-ttu-id="d9585-299">*IntelliSense listeleriyle bir GridView ekleme ve kısmi eşleştirme*</span><span class="sxs-lookup"><span data-stu-id="d9585-299">*Inserting a GridView with IntelliSense lists and partial matching*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a><span data-ttu-id="d9585-300">Görev 4-HTML Düzenleyicisi akıllı etiketleri</span><span class="sxs-lookup"><span data-stu-id="d9585-300">Task 4 - HTML Editor Smart Tags</span></span>

<span data-ttu-id="d9585-301">HTML düzenleyicisinde başka bir geliştirme de Akıllı Etiketler özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d9585-301">Another improvement in the HTML Editor is the Smart Tags feature.</span></span> <span data-ttu-id="d9585-302">Akıllı Etiketler, genel veya yinelenen geliştirme görevlerini denetim başına temelinde gerçekleştirmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d9585-302">Smart tags make it easy to perform common or repetitive development tasks on a per-control basis.</span></span> <span data-ttu-id="d9585-303">Bu özellik HTML tasarımcısında zaten kullanılabilir, ancak HTML düzenleyicisinde mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="d9585-303">This feature was already available in the HTML Designer, but not in the HTML Editor.</span></span>

1. <span data-ttu-id="d9585-304">**Site. Master** ' i açın ve **ASP: Menu** öğesini bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-304">Open **Site.Master** and locate the **asp:Menu** element.</span></span> <span data-ttu-id="d9585-305">İmleci başlangıç etiketine yerleştirin ve küçük glifin öğenin altında görüntülendiğini unutmayın. akıllı görevler menüsünü açmak için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-305">Place the cursor on the start tag and notice that the small glyph displayed at the bottom of the element - click it to open the smart tasks menu.</span></span> <span data-ttu-id="d9585-306">Menü denetimiyle ilgili bazı görevlere hızlı erişiminizin olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-306">Notice that you have quick access to some tasks related to the Menu control.</span></span>

    <span data-ttu-id="d9585-307">![Menü denetimi için akıllı görevler](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Menü denetimi için akıllı görevler")</span><span class="sxs-lookup"><span data-stu-id="d9585-307">![Smart tasks for the Menu control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Smart tasks for the Menu control")</span></span>

    <span data-ttu-id="d9585-308">*Menü denetimi için akıllı görevler*</span><span class="sxs-lookup"><span data-stu-id="d9585-308">*Smart tasks for the Menu control*</span></span>

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a><span data-ttu-id="d9585-309">Görev 5-akıllı girintileme</span><span class="sxs-lookup"><span data-stu-id="d9585-309">Task 5 - Smart Indentation</span></span>

<span data-ttu-id="d9585-310">HTML 'deki en iyi uygulamalardan biri, kodu okunabilir tutmak için iç içe geçmiş öğeleri girintileyerek.</span><span class="sxs-lookup"><span data-stu-id="d9585-310">One of the best practices in HTML is indenting the nested elements to keep the code readable.</span></span> <span data-ttu-id="d9585-311">Visual Studio 2012 ' de, kodu yazarken düzenleyicinin öğeleri otomatik olarak girintiettiğini fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-311">In Visual Studio 2012, you will notice that the editor automatically indents the elements while you are writing the code.</span></span>

> [!NOTE]
> <span data-ttu-id="d9585-312">Visual Studio 'nun önceki sürümünde, akıllı girintileme, XML düzenleyicisinde kullanılabilir ancak HTML düzenleyicisinde yok.</span><span class="sxs-lookup"><span data-stu-id="d9585-312">In previous version of Visual Studio, smart indentation was available in the XML editor but not in the HTML editor.</span></span>

1. <span data-ttu-id="d9585-313">HTML düzenleyicisinde girintileme yapılandırmasının akıllı girintileme olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9585-313">Make sure that the Indenting configuration on the HTML Editor is set to Smart Indentation.</span></span> <span data-ttu-id="d9585-314">Bunu yapmak için **araçları seçin | Seçenekler** menü seçeneği ve sonra **metin düzenleyiciyi seçin | HTML |** Ekranın sol bölmesindeki sekmeler sayfası.</span><span class="sxs-lookup"><span data-stu-id="d9585-314">To do that, select the **Tools | Options** menu option and then select the **Text Editor | HTML | Tabs** page in the left pane of the screen.</span></span> <span data-ttu-id="d9585-315">Akıllı girintileme seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-315">Select the Smart indentation option.</span></span>

    <span data-ttu-id="d9585-316">![HTML Düzenleyicisi ayarları](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Düzenleyicisi ayarları")</span><span class="sxs-lookup"><span data-stu-id="d9585-316">![HTML Editor settings](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Editor settings")</span></span>

    <span data-ttu-id="d9585-317">*HTML Düzenleyicisi ayarları*</span><span class="sxs-lookup"><span data-stu-id="d9585-317">*HTML Editor settings*</span></span>
2. <span data-ttu-id="d9585-318">**Default. aspx** sayfasında, Audio öğesinin altındaki tüm içeriği kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d9585-318">On the **Default.aspx** page, remove all the content under the audio element.</span></span>
3. <span data-ttu-id="d9585-319">İmleci açma **sesi** öğesinin sonuna yerleştirin ve **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-319">Place the cursor at the end of the opening **audio** element and hit **ENTER**.</span></span>

    <span data-ttu-id="d9585-320">İmlecin yeni konumunun ek bir girintileme düzeyine sahip olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-320">Notice that the new position of cursor has an additional indentation level.</span></span>

    <span data-ttu-id="d9585-321">![HTML düzenleyicisinde akıllı girintileme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML düzenleyicisinde akıllı girintileme")</span><span class="sxs-lookup"><span data-stu-id="d9585-321">![Smart indentation in the HTML Editor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Smart indentation in the HTML Editor")</span></span>

    <span data-ttu-id="d9585-322">*HTML düzenleyicisinde akıllı girintileme*</span><span class="sxs-lookup"><span data-stu-id="d9585-322">*Smart indentation in the HTML Editor*</span></span>
4. <span data-ttu-id="d9585-323">Kaldırdığınız içerikle ses etiketini geri yükleyin veya değişiklikleri kaydetmeden **default. aspx** ' i kapatın.</span><span class="sxs-lookup"><span data-stu-id="d9585-323">Restore the audio tag with the content you have removed, or close **Default.aspx** without saving the changes.</span></span>

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a><span data-ttu-id="d9585-324">Görev 6-Kullanıcı denetimine Ayıkla</span><span class="sxs-lookup"><span data-stu-id="d9585-324">Task 6 - Extract to User Control</span></span>

<span data-ttu-id="d9585-325">Visual Studio 'ya eklenen ve kodun bir bölümünü bir işleve ayıklama gibi yeniden düzenleme araçları, geliştirme ve mevcut kodu yeniden düzenleme işlemlerini kolaylaştıran harika özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="d9585-325">The Refactoring tools included in Visual Studio, such as extracting a portion of code to a function, are great features that facilitate the improvement and the refactoring the existing code.</span></span> <span data-ttu-id="d9585-326">ASP.NET sayfaları için karşılık gelen, bir kullanıcı denetimine HTML kodunun ayıklanması olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d9585-326">The counterpart for ASP.NET pages would be the extraction of HTML code to a User Control.</span></span> <span data-ttu-id="d9585-327">Bunu el ile yapmak, yeni bir kullanıcı denetimi oluşturma, kod bölümünü Kullanıcı denetimine taşıma, Kullanıcı denetimi için bir etiket öneki kaydetme ve son olarak sayfalardaki Kullanıcı denetiminin örneğini oluşturma gibi çeşitli adımları kapsar.</span><span class="sxs-lookup"><span data-stu-id="d9585-327">Doing it manually would involve several steps, like creating a new User Control, moving the code section to the User Control, registering a tag prefix for the User Control, and, finally, instantiating the User Control on the pages.</span></span> <span data-ttu-id="d9585-328">Şimdi, yeni *kullanıcıya Ayıkla denetim* aracı sizin için tüm bu adımları otomatik olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d9585-328">Now, the new *Extract to User Control* tool automatically performs all those steps for you.</span></span>

<span data-ttu-id="d9585-329">Bu görevde, seçilen koddan yeni bir kullanıcı denetimi oluşturmak için yeni bir kullanıcı denetimi bağlama işlemini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d9585-329">In this task, you will use the new Extract to User Control contextual operation to generate a new user control from the selected code.</span></span>

1. <span data-ttu-id="d9585-330">**Default. aspx** sayfasında **H2** ve **Audio** öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="d9585-330">On the **Default.aspx** page, select the **H2** and **audio** elements.</span></span>
2. <span data-ttu-id="d9585-331">Sağ tıklayın ve **Kullanıcı denetimine Ayıkla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="d9585-331">Right click and select **Extract to User Control**.</span></span>

    <span data-ttu-id="d9585-332">![Kullanıcıya Ayıkla Denetim menüsü seçeneği](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Kullanıcıya Ayıkla Denetim menüsü seçeneği")</span><span class="sxs-lookup"><span data-stu-id="d9585-332">![Extract to User Control menu option](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Extract to User Control menu option")</span></span>

    <span data-ttu-id="d9585-333">*Kullanıcıya Ayıkla Denetim menüsü seçeneği*</span><span class="sxs-lookup"><span data-stu-id="d9585-333">*Extract to User Control menu option*</span></span>
3. <span data-ttu-id="d9585-334">Yeni Kullanıcı denetimi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="d9585-334">Type a name for the new user control.</span></span> <span data-ttu-id="d9585-335">Örneğin, **Jukebox. ascx**' i ve ardından **Tamam**' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d9585-335">For instance, **Jukebox.ascx**, and then click **OK**.</span></span>

    <span data-ttu-id="d9585-336">![Ayıklanan Kullanıcı denetimini kaydetme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Ayıklanan Kullanıcı denetimini kaydetme")</span><span class="sxs-lookup"><span data-stu-id="d9585-336">![Saving the extracted user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Saving the extracted user control")</span></span>

    <span data-ttu-id="d9585-337">*Ayıklanan Kullanıcı denetimini kaydetme*</span><span class="sxs-lookup"><span data-stu-id="d9585-337">*Saving the extracted user control*</span></span>
4. <span data-ttu-id="d9585-338">Seçili kodun bir kullanıcı denetimine ayıklandığına ve seçili kodun özgün konumunun yeni kullanıcı denetiminin bir örneğiyle değiştirildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-338">Notice that the selected code was extracted to a user control and the original location of the selected code was replaced with an instance of the new user control.</span></span>

    <span data-ttu-id="d9585-339">![Sayfa Yeni Kullanıcı denetimini kullanacak şekilde otomatik olarak güncelleştirildi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Sayfa Yeni Kullanıcı denetimini kullanacak şekilde otomatik olarak güncelleştirildi")</span><span class="sxs-lookup"><span data-stu-id="d9585-339">![Page automatically updated to use the new user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Page automatically updated to use the new user control")</span></span>

    <span data-ttu-id="d9585-340">*Sayfa Yeni Kullanıcı denetimini kullanacak şekilde otomatik olarak güncelleştirildi*</span><span class="sxs-lookup"><span data-stu-id="d9585-340">*Page automatically updated to use the new user control*</span></span>
5. <span data-ttu-id="d9585-341">Sayfayı çalıştırmak için **F5** tuşuna basın ve denetimin çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-341">Press **F5** to run the page and verify that the control works.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a><span data-ttu-id="d9585-342">Alıştırma 3: JavaScript düzenleyicideki yenilikler</span><span class="sxs-lookup"><span data-stu-id="d9585-342">Exercise 3: What's New in the JavaScript Editor</span></span>

<span data-ttu-id="d9585-343">Özellikle uygulamanız boyutu büyümeye başladığı ve uzun dosyalarla ve yüzlerce işlevlerle ilgilenirken JavaScript kodu yazmak veya düzenlenmesinin kolay bir görev değildir.</span><span class="sxs-lookup"><span data-stu-id="d9585-343">Writing or editing JavaScript code is not an easy task, especially when your application starts to grow in size and you find yourself dealing with long files and hundreds of functions.</span></span> <span data-ttu-id="d9585-344">Betik geliştiricilerinin genellikle kod okunabilirliğini sürdürmek ve dosyalar arasında gezinmek için bazı ek işler yapması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9585-344">Script developers usually have to do some extra work to maintain code legibility and navigate across files.</span></span> <span data-ttu-id="d9585-345">JQuery gibi JavaScript kitaplıklarının dahil edilmesi halinde, kod uzunluğu nedeniyle betik gezintisi bir sınama haline geldi.</span><span class="sxs-lookup"><span data-stu-id="d9585-345">With the inclusion of JavaScript libraries like jQuery, script navigation has become a challenge itself because of the code length.</span></span>

<span data-ttu-id="d9585-346">Visual Studio, kod modunu erişilebilir ve düzenlenebilir hale getirmek için Promise ile JavaScript düzenleyicisini yeniledi.</span><span class="sxs-lookup"><span data-stu-id="d9585-346">Visual Studio has renewed the JavaScript editor with the promise to make the code mode accessible and organized.</span></span> <span data-ttu-id="d9585-347">C# Veya vb düzenleyicilerinde zaten var olan birçok Visual Studio özelliği artık JavaScript düzenleyicisinde uygulandı: yazarken tanıma, otomatik girintileme, belgeler ve doğrulama bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="d9585-347">Many Visual Studio features that already existed in C# or VB editors are now implemented in the JavaScript editor: Go To Definition, automatic indentation, documentation and validation when you are writing.</span></span> <span data-ttu-id="d9585-348">Yenilenen IntelliSense listesinde, JavaScript işlev kataloğuna parmaklarınızın ucunda olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d9585-348">With the renewed IntelliSense list you will have the JavaScript function catalog at your fingertips.</span></span>

<span data-ttu-id="d9585-349">Bu alıştırmada, JavaScript Düzenleyicisi 'nin yeni özellik ve iyileştirmelerinden bazılarını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-349">In this exercise, you will learn some of the new features and improvements of JavaScript editor.</span></span> <span data-ttu-id="d9585-350">Örnek dosyalara gözatıp, JavaScript programlarınızın Visual Studio 2012 içinde daha verimli olmasını sağlayacak yeni özelliklerden her birini keşfedeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-350">You will browse sample files and discover each of the new characteristics that will make your JavaScript programming more efficient within Visual Studio 2012.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a><span data-ttu-id="d9585-351">Görev 1-JavaScript Düzenleyicisi yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="d9585-351">Task 1 - JavaScript Editor New Features</span></span>

<span data-ttu-id="d9585-352">Bu görev sizi, kodunuzun düzenlenmesine ve daha iyi bir kullanıcı deneyimi getirmeye odaklanarak yeni JavaScript Düzenleyicisi özelliklerinden bazılarını tanıtacaktır.</span><span class="sxs-lookup"><span data-stu-id="d9585-352">This task will introduce you to some of the new JavaScript editor features, which focus on organizing your code and bringing a better user experience.</span></span>

1. <span data-ttu-id="d9585-353">Zaten açık değilse, **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-353">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="d9585-354">Uygulamayı çalıştırmak için **F5** tuşuna basın, ardından gezinti çubuğundaki JavaScript bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-354">Press **F5** to run the application, then click the JavaScript link in the navigation bar.</span></span> <span data-ttu-id="d9585-355">Sayfayı birkaç kez yenileyin ve sayacın nasıl artısaymadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-355">Refresh the page several times and check how the counter increments.</span></span>

    <span data-ttu-id="d9585-356">![Sayfa sayacı](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Sayfa sayacı")</span><span class="sxs-lookup"><span data-stu-id="d9585-356">![Page counter](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page counter")</span></span>

    <span data-ttu-id="d9585-357">*Sayfa sayacı*</span><span class="sxs-lookup"><span data-stu-id="d9585-357">*Page counter*</span></span>
3. <span data-ttu-id="d9585-358">Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="d9585-358">Close the browser and go back to Visual Studio.</span></span>
4. <span data-ttu-id="d9585-359">**JavaScript. aspx** sayfasını açın ve **&lt;betiği&gt;** bloğunu (aşağıda gösterilmiştir) bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-359">Open the **JavaScript.aspx** page and locate the **&lt;script&gt;** block (shown below).</span></span>

    <span data-ttu-id="d9585-360">Aşağıdaki kod, sayfanın geçerli kullanıcı tarafından ziyaret edilme sayısını depolayan *Pageloadcount* değişkenini depolamak için HTML5 yerel depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="d9585-360">The following code uses HTML5 local storage to store a *pageLoadCount* variable that stores the number of times the page has been visited by the current user.</span></span> <span data-ttu-id="d9585-361">Yerel depolama, HTML5 standardına göre sunulan bir istemci tarafı anahtar-değer veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="d9585-361">Local Storage is a client-side key-value database introduced with the HTML5 standard.</span></span> <span data-ttu-id="d9585-362">Veriler, kullanıcının tarayıcısının içindeki yerel makineye kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d9585-362">The data is saved on the local machine, inside the user's browser.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="d9585-363">Sonraki adımlarla devam etmeden önce DOCTYPE 'ın XHTML5 olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9585-363">Ensure the DOCTYPE is set to XHTML5 before proceeding with the next steps.</span></span>
5. <span data-ttu-id="d9585-364">Kodu düzenleyin ve JavaScript için IntelliSense 'in yerel depolama gibi HTML5 özellikleri ve bunların iç yöntemleri içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-364">Edit the code and notice that IntelliSense for JavaScript includes HTML5 features, like local storage, and their inner methods.</span></span>

    <span data-ttu-id="d9585-365">![JavaScript 'te HTML5 JavaScript özellikleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript 'te HTML5 JavaScript özellikleri")</span><span class="sxs-lookup"><span data-stu-id="d9585-365">![HTML5 JavaScript features in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript features in JavaScript")</span></span>

    <span data-ttu-id="d9585-366">*JavaScript 'te HTML5 JavaScript özellikleri*</span><span class="sxs-lookup"><span data-stu-id="d9585-366">*HTML5 JavaScript features in JavaScript*</span></span>
6. <span data-ttu-id="d9585-367">Betik kodundan herhangi bir açma köşeli ayracı ( **{** ) tıklatın ve köşeli ayracın vurgulandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-367">Click any opening bracket (**{**) from the scripting code and notice that the brackets are highlighted.</span></span>

    <span data-ttu-id="d9585-368">![Köşeli ayraçlar vurgulanır](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Köşeli ayraçlar vurgulanır")</span><span class="sxs-lookup"><span data-stu-id="d9585-368">![Brackets are highlighted](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Brackets are highlighted")</span></span>

    <span data-ttu-id="d9585-369">*Köşeli ayraçlar vurgulanır*</span><span class="sxs-lookup"><span data-stu-id="d9585-369">*Brackets are highlighted*</span></span>
7. <span data-ttu-id="d9585-370">**Testautoalign ()** işlevinin açıklamasını kaldırın (üç satırı seçin ve **CTRL** + **K**kullanabilirsiniz; **CTRL** + **U**) ve işlev kodu içindeki imleci bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-370">Uncomment the function **testAutoAlign()** (select the three lines and you can use **CTRL** + **K**; **CTRL** + **U**) and locate the cursor inside the function code.</span></span> <span data-ttu-id="d9585-371">İkinci bir satırı eklemek için ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-371">Press enter to append a second line.</span></span> <span data-ttu-id="d9585-372">Kodun artık **hizalandığını** ve **Otomatik girintili**olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-372">Notice that the code is now **aligned** and **auto-indented**.</span></span>

    <span data-ttu-id="d9585-373">![JavaScript kodu otomatik hizalı](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript kodu otomatik hizalı")</span><span class="sxs-lookup"><span data-stu-id="d9585-373">![JavaScript code is auto aligned](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript code is auto aligned")</span></span>

    <span data-ttu-id="d9585-374">*JavaScript kodu otomatik hizalı*</span><span class="sxs-lookup"><span data-stu-id="d9585-374">*JavaScript code is auto aligned*</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a><span data-ttu-id="d9585-375">Görev 2-JavaScript doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="d9585-375">Task 2 - Validating JavaScript</span></span>

<span data-ttu-id="d9585-376">Bu görevde, ECMAScript5 Standard için yeni JavaScript doğrulamasını keşfedeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-376">In this task, you will discover the new JavaScript validation for the ECMAScript5 standard.</span></span> <span data-ttu-id="d9585-377">Bu özellik uyumlu JavaScript kodu yazmanıza yardımcı olur, ancak site dağıtımından önce betik oluşturma sorunlarını önler.</span><span class="sxs-lookup"><span data-stu-id="d9585-377">This feature will help you to write compliant JavaScript code, while preventing scripting issues before site deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="d9585-378">Visual Studio 2010 ECMAStript3 uyumluluğunu uyguladık, Visual Studio 2012 ECMAScript5 uyumluluğu sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9585-378">Visual Studio 2010 implemented ECMAStript3 compliance, while Visual Studio 2012 provides ECMAScript5 compliance.</span></span>

1. <span data-ttu-id="d9585-379">**Scripts\custom** proje klasörünün altında bulunan **ECMA5script5. js** ' i açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-379">Open **ECMA5script5.js** located under the **Scripts\custom** project folder.</span></span> <span data-ttu-id="d9585-380">Artık ECMAScript5 Standard için doğrulamayı test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-380">You will now test validation for ECMAScript5 standard.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    <span data-ttu-id="d9585-381">ECMAScript5 **katı modu**sağlayan, dosyanın ilk satırında **katı** &quot; yönü &quot; kullanıma alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-381">You can check out the &quot; **use strict** &quot; direction in the first line of the file, which enables ECMAScript5 **strict mode**.</span></span> <span data-ttu-id="d9585-382">Bu mod, önceki sürümden belirsizlikleri açıklığa kavuşturtiren dilin bir alt kümesiyle oluşur ve alıcıları ve ayarlayıcılar, JSON için kitaplık desteği ve nesne özellikleri üzerinde daha fazla yansıma gibi bazı yeni özellikler ekler.</span><span class="sxs-lookup"><span data-stu-id="d9585-382">This mode consists in a subset of the language that clarifies ambiguities from the past edition, and adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.</span></span>
2. <span data-ttu-id="d9585-383">Zaten açılmadıysa **hata listesi** açın (**Görünüm** menüsü | **Hata listesi**).</span><span class="sxs-lookup"><span data-stu-id="d9585-383">Open the **Error List** if not already opened (**View** menu | **Error List**).</span></span> <span data-ttu-id="d9585-384">**İşlev** bildiriminin altı çizili olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-384">Notice the **function** declaration is underlined.</span></span> <span data-ttu-id="d9585-385">Bunun nedeni, ECMA5 standart işlevlerinin dil yapıları içinde yer alamaz.</span><span class="sxs-lookup"><span data-stu-id="d9585-385">This is because in ECMA5 standard functions cannot be nested inside language structures.</span></span> <span data-ttu-id="d9585-386">Aşağıdaki hata listesinde, uyarı ayrıntılarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d9585-386">In the error list below you will see the warning details.</span></span>

    <span data-ttu-id="d9585-387">![JavaScript doğrulama hata iletisi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript doğrulama hata iletisi")</span><span class="sxs-lookup"><span data-stu-id="d9585-387">![JavaScript validation error message](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript validation error message")</span></span>

    <span data-ttu-id="d9585-388">*JavaScript doğrulama hata iletisi*</span><span class="sxs-lookup"><span data-stu-id="d9585-388">*JavaScript validation error message*</span></span>
3. <span data-ttu-id="d9585-389">**&quot;katı&quot;yönünü kullanın** ve hataların kaybolduğunu, ancak uyarıların kaldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-389">Comment out the **&quot;use strict&quot;** direction and notice that errors disappear, but the warnings remain.</span></span>
4. <span data-ttu-id="d9585-390">Dosyanın son satırına, **&quot;test&quot;** gibi bir dize yazın (dize olarak göstermek için tırnak işaretleri ekleyin).</span><span class="sxs-lookup"><span data-stu-id="d9585-390">In the last line of the file, write any string like **&quot;test&quot;** (include the quotation marks to indicate it is as string).</span></span> <span data-ttu-id="d9585-391">IntelliSense listesini göstermek için dizenin yanına bir nokta yazın ve **Kırp** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-391">Write a period next to the string to display the IntelliSense list, and select the **trim** option.</span></span>

    <span data-ttu-id="d9585-392">ECMAScript5 Standard 'da, dize değerleri ve değişkenleri, trim, büyük harfler, ara ve Değiştir gibi tanımlanmış dize yöntemlerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d9585-392">In ECMAScript5 standard, string values and variables also have string methods defined, like trim, uppercase, search and replace.</span></span>

    <span data-ttu-id="d9585-393">![JavaScript 'te IntelliSense listesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript 'te IntelliSense listesi")</span><span class="sxs-lookup"><span data-stu-id="d9585-393">![IntelliSense list in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "IntelliSense list in JavaScript")</span></span>

    <span data-ttu-id="d9585-394">*JavaScript 'te IntelliSense listesi*</span><span class="sxs-lookup"><span data-stu-id="d9585-394">*IntelliSense list in JavaScript*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a><span data-ttu-id="d9585-395">Görev 3-JavaScript için XML belgeleri</span><span class="sxs-lookup"><span data-stu-id="d9585-395">Task 3 - XML Documentation for JavaScript</span></span>

<span data-ttu-id="d9585-396">Bu görevde JavaScript 'te XML belgeleri için Visual Studio özelliklerini araştıracaktır.</span><span class="sxs-lookup"><span data-stu-id="d9585-396">In this task, you will explore Visual Studio features for XML documentation in JavaScript.</span></span> <span data-ttu-id="d9585-397">JavaScript IntelliSense listesinin şimdi her bir işlevin XML belgelerini gösterdiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d9585-397">You will see the JavaScript IntelliSense list now shows the XML documentation of each function.</span></span> <span data-ttu-id="d9585-398">Ayrıca, gezinme özelliğini JavaScript 'te keşfedeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-398">Additionally, you will discover the navigation feature in JavaScript.</span></span>

1. <span data-ttu-id="d9585-399">**Betikler/özel** proje klasöründe bulunan **xmlDoc. js** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-399">Open **XMLDoc.js** file located in **Scripts/custom** project folder.</span></span> <span data-ttu-id="d9585-400">Bu dosya JavaScript işlevlerinin her birinde XML belgelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d9585-400">This file contains XML documentation on each of the JavaScript functions.</span></span>

    <span data-ttu-id="d9585-401">![IntelliSense ile tümleştirilmiş JavaScript XML belgeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "IntelliSense ile tümleştirilmiş JavaScript XML belgeleri")</span><span class="sxs-lookup"><span data-stu-id="d9585-401">![JavaScript XML documentation integrated to IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML documentation integrated to IntelliSense")</span></span>

    <span data-ttu-id="d9585-402">*IntelliSense ile tümleştirilmiş JavaScript XML belgeleri*</span><span class="sxs-lookup"><span data-stu-id="d9585-402">*JavaScript XML documentation integrated to IntelliSense*</span></span>
2. <span data-ttu-id="d9585-403">**XmlDoc. js** dosyasındaki **Add** işlevi altında, **Test**adlı yeni bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9585-403">Below **add** function in **XMLDoc.js** file, create a new function named **test**.</span></span>
3. <span data-ttu-id="d9585-404">**Test** işlevinde, iki parametre alan **çarpma** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d9585-404">In the **test** function, call the **multiply** function that receives two parameters.</span></span> <span data-ttu-id="d9585-405">Araç ipucu kutusunda **çarpma** işlevi belgelerinin gösterildiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-405">Notice the tooltip box is showing the **multiply** function documentation.</span></span>

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    <span data-ttu-id="d9585-406">![JavaScript işlevleri için XML belgeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript işlevleri için XML belgeleri")</span><span class="sxs-lookup"><span data-stu-id="d9585-406">![XML documentation for JavaScript functions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "XML documentation for JavaScript functions")</span></span>

    <span data-ttu-id="d9585-407">*JavaScript işlevleri için XML belgeleri*</span><span class="sxs-lookup"><span data-stu-id="d9585-407">*XML documentation for JavaScript functions*</span></span>
4. <span data-ttu-id="d9585-408">İşlev çağrısı ifadesini doldurun ve döndürülen değer üzerinde IntelliSense listesini açmak için bir *nokta* yazın.</span><span class="sxs-lookup"><span data-stu-id="d9585-408">Complete the function call statement and type a *dot* to open the IntelliSense list on the returned value.</span></span> <span data-ttu-id="d9585-409">Visual Studio 'Nun belgelerde **döndürülen** değeri algılayarak değeri sayı olarak kabul ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-409">Notice that Visual Studio is detecting the **return** value in the documentation, treating the value as a number.</span></span>

    <span data-ttu-id="d9585-410">![Dönüş türleri için XML belgeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "Dönüş türleri için XML belgeleri")</span><span class="sxs-lookup"><span data-stu-id="d9585-410">![XML documentation for return types](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "XML documentation for return types")</span></span>

    <span data-ttu-id="d9585-411">*Dönüş türleri için XML belgeleri*</span><span class="sxs-lookup"><span data-stu-id="d9585-411">*XML documentation for return types*</span></span>
5. <span data-ttu-id="d9585-412">Şimdi, Add işlevi için bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-412">Now, insert a call to add function.</span></span> <span data-ttu-id="d9585-413">JavaScript düzenleyicisinin artık işlev aşırı yüklerini desteklediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-413">Notice that the JavaScript editor now supports function overloads.</span></span> <span data-ttu-id="d9585-414">Bir işlev adı yazdığınızda, belgelerde belirtilen kullanılabilir aşırı yüklerden birini seçebileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-414">When you write a function name, you will be able to select any of the available overloads specified in the documentation.</span></span>

    <span data-ttu-id="d9585-415">![Aşırı yüklemeler için XML belgeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "Aşırı yüklemeler için XML belgeleri")</span><span class="sxs-lookup"><span data-stu-id="d9585-415">![XML documentation for overloads](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "XML documentation for overloads")</span></span>

    <span data-ttu-id="d9585-416">*Aşırı yüklemeler için XML belgeleri*</span><span class="sxs-lookup"><span data-stu-id="d9585-416">*XML documentation for overloads*</span></span>
6. <span data-ttu-id="d9585-417">**Sayfaydefinition. js** dosyasını açın ve **$ (). html ()** işlev çağrısını bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-417">Open **GotoDefinition.js** file and locate the **$().html()** function call.</span></span> <span data-ttu-id="d9585-418">**HTML**üzerinde imleci bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-418">Locate the cursor on **html**.</span></span>
7. <span data-ttu-id="d9585-419">**F12** tuşuna basın ve tanıma gidin.</span><span class="sxs-lookup"><span data-stu-id="d9585-419">Press **F12** and navigate to the definition.</span></span> <span data-ttu-id="d9585-420">Artık **bul** aracını kullanmadan JavaScript kodunuza erişip erişebileceğinizi fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-420">Notice you can now access and browse your JavaScript code without using the **Find** tool.</span></span>
8. <span data-ttu-id="d9585-421">Kod dosyasının alt kısmındaki imza bloğundan önce jQuery yönergesinin üzerindeki imleci bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-421">Locate the cursor on the jQuery instruction prior to the signature block at the bottom of the code file.</span></span> <span data-ttu-id="d9585-422">**F12**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-422">Press **F12**.</span></span> <span data-ttu-id="d9585-423">JQuery kitaplık dosyasına gitmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9585-423">You will navigate to the jQuery library file.</span></span> <span data-ttu-id="d9585-424">Ayrıca, **F12**kullanarak jQuery dosyaları arasında gezinmeniz fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-424">Notice you can also navigate across the jQuery files using **F12**.</span></span>

    <span data-ttu-id="d9585-425">![JQuery tanımlarına gitme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "JQuery tanımlarına gitme")</span><span class="sxs-lookup"><span data-stu-id="d9585-425">![Navigating to jQuery definitions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Navigating to jQuery definitions")</span></span>

    <span data-ttu-id="d9585-426">*JQuery tanımlarına gitme*</span><span class="sxs-lookup"><span data-stu-id="d9585-426">*Navigating to jQuery definitions*</span></span>

> [!NOTE]
> <span data-ttu-id="d9585-427">Dosyayı kaydetmeden önce, Sayfaydefinition. js ' nin sözdizimi hatası olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9585-427">Make sure that GotoDefinition.js has no syntax errors before saving the file.</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a><span data-ttu-id="d9585-428">Alıştırma 4: paketleme ve Minbirleşme</span><span class="sxs-lookup"><span data-stu-id="d9585-428">Exercise 4: Bundling and Minification</span></span>

<span data-ttu-id="d9585-429">Web siteleriniz kaç kez bir JavaScript veya CSS dosyası içeriyor?</span><span class="sxs-lookup"><span data-stu-id="d9585-429">How many times do your websites include more than one JavaScript or CSS file?</span></span> <span data-ttu-id="d9585-430">Bu, paketleme ve küçültme, dosya boyutunu azaltmaya ve sitenin daha hızlı gerçekleşmesini sağlamaya yardımcı olan çok yaygın bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="d9585-430">This is a very common scenario where bundling and minification can help to reduce the file size and make the site perform faster.</span></span> <span data-ttu-id="d9585-431">ASP.NET 4,5 ' deki yeni paketleme özelliği, bir dizi JS veya CSS dosyasını tek bir öğe halinde paketler ve içeriği (gerekmeyen boş alanları kaldırmak, açıklamaları kaldırmak ve tanımlayıcıları azaltmak) için boyutunu azaltır.</span><span class="sxs-lookup"><span data-stu-id="d9585-431">The new bundling feature in ASP.NET 4.5 packs a set of JS or CSS files into a single element, and reduces its size by minifying the content ( i.e. removing not required blank spaces, removing comments, reducing identifiers ).</span></span>

<span data-ttu-id="d9585-432">ASP.NET 4,5 ' de paketleme ve küçültme, çalışma zamanında gerçekleştirilir, böylece işlem Kullanıcı aracısını tanımlayabilir (örneğin, IE, Mozilla, vb.) ve bu nedenle Kullanıcı tarayıcısını hedefleyerek (örneğin, Mozilla 'e özgü olan öğeleri kaldırma) sıkıştırma işlemini geliştirebilirsiniz istek IE 'den geldiğinde).</span><span class="sxs-lookup"><span data-stu-id="d9585-432">Bundling and minification in ASP.NET 4.5 is performed at runtime, so that the process can identify the user agent (for example IE, Mozilla, etc), and thus, improve the compression by targeting the user browser (for instance, removing stuff that is Mozilla specific when the request comes from IE).</span></span>

<span data-ttu-id="d9585-433">Bu alıştırmada, ASP.NET 4,5 ' de farklı paketleme ve küçültme türlerini nasıl etkinleştireceğinizi ve kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-433">In this exercise, you will learn how to enable and use the different types of bundling and minification in ASP.NET 4.5.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a><span data-ttu-id="d9585-434">Görev 1-NuGet 'den paketleme ve Minbirleşme paketini yükleme</span><span class="sxs-lookup"><span data-stu-id="d9585-434">Task 1 - Installing the Bundling and Minification Package from NuGet</span></span>

1. <span data-ttu-id="d9585-435">Zaten açık değilse, **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-435">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="d9585-436">NuGet Paket Yöneticisi konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-436">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="d9585-437">Bunu yapmak için, **diğer Windows** | **paket Yöneticisi konsolu** | menü **görünümünü** kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9585-437">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>

    <span data-ttu-id="d9585-438">![Paket Yöneticisi file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole açılıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Paket Yöneticisi konsolunu açma")</span><span class="sxs-lookup"><span data-stu-id="d9585-438">![Opening the package manager file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Opening the package manager console")</span></span>

    <span data-ttu-id="d9585-439">*Paket Yöneticisi konsolunu açma*</span><span class="sxs-lookup"><span data-stu-id="d9585-439">*Opening the package manager console*</span></span>
3. <span data-ttu-id="d9585-440">**Paket Yöneticisi konsolunda** **Install-Package Microsoft. Web. Optimization** yazın ve **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-440">In the **Package Manager Console,** type **Install-Package Microsoft.Web.Optimization** and press **ENTER**.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a><span data-ttu-id="d9585-441">Görev 2-varsayılan demeti</span><span class="sxs-lookup"><span data-stu-id="d9585-441">Task 2 - Default Bundles</span></span>

<span data-ttu-id="d9585-442">Paketleme ve minmate kullanmanın en basit yolu, varsayılan paketleri etkinleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="d9585-442">The simplest way to use bundling and minification is to enable the default bundles.</span></span> <span data-ttu-id="d9585-443">Bu yöntem, bir klasördeki JS ve CSS dosyaları için paketlenmiş ve küçültülmüş sürüme başvuru yapmanızı sağlamak için kuralları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d9585-443">This method uses conventions to let you reference the bundled and minified version for the JS and CSS files in a folder.</span></span>

<span data-ttu-id="d9585-444">Bu görevde, paketlenmiş ve küçültülmüş JS ve CSS dosyalarını nasıl etkinleştirip başvurulacağını ve elde edilen çıktıyı görüntülemenize öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-444">In this task, you will learn how to enable and reference the bundled and minified JS and CSS files and view the resulting output.</span></span>

1. <span data-ttu-id="d9585-445">Zaten açık değilse, **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-445">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="d9585-446">**Çözüm Gezgini**, **Styles**, **scripts\custom** ve **scripts\demeti** klasörlerini genişletin.</span><span class="sxs-lookup"><span data-stu-id="d9585-446">In the **Solution Explorer**, expand the **Styles**, **Scripts\custom** and **Scripts\bundle** folders.</span></span>

    <span data-ttu-id="d9585-447">Uygulamanın birden fazla CSS ve JS dosyası kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-447">Notice that the application is using more than one CSS and JS file.</span></span>

    <span data-ttu-id="d9585-448">![Uygulamada birden çok stil sayfaları ve JavaScript dosyası](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Uygulamada birden çok stil sayfaları ve JavaScript dosyası")</span><span class="sxs-lookup"><span data-stu-id="d9585-448">![Multiple Stylesheets and JavaScript files in the application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Multiple Stylesheets and JavaScript files in the application")</span></span>

    <span data-ttu-id="d9585-449">*Uygulamada birden çok stil sayfaları ve JavaScript dosyası*</span><span class="sxs-lookup"><span data-stu-id="d9585-449">*Multiple Stylesheets and JavaScript files in the application*</span></span>
3. <span data-ttu-id="d9585-450">**Global.asax.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-450">Open the **Global.asax.cs** file.</span></span>

    <span data-ttu-id="d9585-451">Yeni **Microsoft. Web. Optimization** ad alanının, dosyanın başlangıcında yorum oluşturulduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-451">Notice that the new **Microsoft.Web.Optimization** namespace is commented out at the beginning of the file.</span></span> <span data-ttu-id="d9585-452">Paketleme ve küçültmeye yönelik özellikleri eklemek için using yönergesinin açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d9585-452">Uncomment the using directive to include the bundling and minification features.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. <span data-ttu-id="d9585-453">**Uygulama\_start** metodunu bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-453">Locate the **Application\_Start** method.</span></span>

    <span data-ttu-id="d9585-454">Bu yöntemde, aşağıdaki kod parçacığında gösterildiği gibi Enabledefaultdemeti çağrısının açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d9585-454">In this method, uncomment the EnableDefaultBundles call as shown in the snippet below.</span></span> <span data-ttu-id="d9585-455">Bu, söz konusu klasörün yolunu ve &quot;CSS&quot; ya da &quot;JS&quot; sonekini kullanarak bir klasördeki CSS dosyalarının paketlenmiş bir koleksiyonuna başvurmamızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9585-455">This enables us to reference a bundled collection of CSS files in a folder by using the path to that folder, plus the &quot;CSS&quot; or the &quot;JS&quot; suffix.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. <span data-ttu-id="d9585-456">**Optimizasyon. aspx** dosyasını açın ve **headcontent**denetiminin içerik denetimini bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-456">Open the **Optimization.aspx** file and locate the content control for **HeadContent**.</span></span>

    <span data-ttu-id="d9585-457">CSS dosyalarına ve JS dosyalarına başvurulan tek bir etiket olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-457">Notice the CSS files and the JS files have a single referenced tag.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > <span data-ttu-id="d9585-458">Bu kod tanıtım amaçlıdır.</span><span class="sxs-lookup"><span data-stu-id="d9585-458">This code is for demo purposes.</span></span> <span data-ttu-id="d9585-459">İdeal olarak, site. master dosyasındaki paketlerdir.</span><span class="sxs-lookup"><span data-stu-id="d9585-459">Ideally, you will reference the bundles in the Site.Master file.</span></span> <span data-ttu-id="d9585-460">Bu örnek kodda, bazı paketlenmiş dosyalara da site. master dosyası tarafından başvurulduğunu ve bu son başvurunun gereksiz olduğunu fark edersiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-460">In this sample code, you will find that some of the bundled files are also being referenced by the Site.Master file, making this last reference redundant.</span></span>
6. <span data-ttu-id="d9585-461">Bağlantıların, sırasıyla Styles ve Scripts\custom klasöründen tüm CSS veya JS dosyalarını almak için **href** özniteliğinde paketleme kurallarını kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-461">Notice that the links are using the bundling conventions in the **href** attribute to get all the CSS or JS files from the Styles and Scripts\custom folder respectively.</span></span>

    <span data-ttu-id="d9585-462">**Komut dosyaları/özel** klasör IÇINDEKI tüm JS dosyalarını paketleyip daha fazla kullanmak için aşağıda gösterildiği gibi **komut dosyalarını/özel/JS** yolunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-462">You can use the path **Scripts/custom/JS** as shown below to bundle and minify all the JS files inside a **Scripts/custom** folder.</span></span> <span data-ttu-id="d9585-463">Varsayılan değer olan varsayılan davranıştır.</span><span class="sxs-lookup"><span data-stu-id="d9585-463">This is the default behavior with the default bundles.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. <span data-ttu-id="d9585-464">**Styles\site.exe** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-464">Open the **Styles\Site.css** file.</span></span>

    <span data-ttu-id="d9585-465">Özgün CSS dosyasının girintili kod, boş alanlar ve dosyayı büyüten Yorumlar içerdiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-465">Notice that the original CSS file contains indented code, blank spaces and comments that enlarge the file.</span></span> <span data-ttu-id="d9585-466">(Ayrıca, JavaScript dosyası boş boşluklar ve açıklamalar içerir).</span><span class="sxs-lookup"><span data-stu-id="d9585-466">(Also the JavaScript file contains blank spaces and comments).</span></span>

    <span data-ttu-id="d9585-467">![Betikler klasöründeki özgün CSS dosyalarından biri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Betikler klasöründeki özgün CSS dosyalarından biri")</span><span class="sxs-lookup"><span data-stu-id="d9585-467">![One of the original CSS files in the Scripts folder](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "One of the original CSS files in the Scripts folder")</span></span>

    <span data-ttu-id="d9585-468">*Betikler klasöründeki özgün CSS dosyalarından biri*</span><span class="sxs-lookup"><span data-stu-id="d9585-468">*One of the original CSS files in the Scripts folder*</span></span>
8. <span data-ttu-id="d9585-469">**F5** tuşuna basarak uygulamayı çalıştırın ve **iyileştirme** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="d9585-469">Press **F5** to run the application and navigate to the **Optimization** page.</span></span>
9. <span data-ttu-id="d9585-470">Dosyayı indirmek ve açmak için **CSS paketi** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-470">Click on the **CSS Bundle** link to download and open the file.</span></span>

    <span data-ttu-id="d9585-471">Küçültülmüş olan paketlenmiş dosyaya göz atın.</span><span class="sxs-lookup"><span data-stu-id="d9585-471">Check out the minified bundled file.</span></span> <span data-ttu-id="d9585-472">Tüm boş boşlukların, yorumların ve girintileme karakterlerinin kaldırıldığını, daha küçük bir dosya oluşturduğunu fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-472">You will notice that all the blank spaces, comments and indentation characters have been removed, generating a smaller file.</span></span>

    <span data-ttu-id="d9585-473">![Paketlenmiş CSS dosyaları](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Paketlenmiş CSS dosyaları")</span><span class="sxs-lookup"><span data-stu-id="d9585-473">![Bundled CSS files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS files")</span></span>

    <span data-ttu-id="d9585-474">*Paketlenmiş CSS dosyaları*</span><span class="sxs-lookup"><span data-stu-id="d9585-474">*Bundled CSS files*</span></span>
10. <span data-ttu-id="d9585-475">Şimdi, JavaScript paketlenmiş dosyasını açmak için **js paket** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-475">Now click the **JS Bundle** link to open the JavaScript bundled file.</span></span> <span data-ttu-id="d9585-476">Gezgin uyarısını güvenle yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-476">You can safely disregard the explorer warning.</span></span> <span data-ttu-id="d9585-477">**Özel** klasör altındaki JavaScript dosyalarının da paketlenmiş ve küçültülmüş olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-477">Notice the JavaScript files under the **custom** folder are also bundled and minified.</span></span>

    <span data-ttu-id="d9585-478">![Paketlenmiş JavaScript dosyaları](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Paketlenmiş JavaScript dosyaları")</span><span class="sxs-lookup"><span data-stu-id="d9585-478">![Bundled JavaScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript files")</span></span>

    <span data-ttu-id="d9585-479">*Paketlenmiş JavaScript dosyaları*</span><span class="sxs-lookup"><span data-stu-id="d9585-479">*Bundled JavaScript files*</span></span>

    <span data-ttu-id="d9585-480">CSS veya JS dosyaları için sıkıştırmayı etkinleştirmek, önceki ASP.NET sürümünde çok daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="d9585-480">Enabling compression for CSS or JS files was much more complicated in previous ASP.NET version.</span></span> <span data-ttu-id="d9585-481">Artık gördüğünüz gibi, paketlemeyi etkinleştirmek için *Global. asax* dosyasına bir satır eklemeniz ve sonra sitenizdeki paketlenmiş dosyalara başvurmanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="d9585-481">Now, as you have seen, you just need to add one line in the *Global.asax* file to enable bundling, and then reference the bundled files from your site.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a><span data-ttu-id="d9585-482">Görev 3-statik demeti</span><span class="sxs-lookup"><span data-stu-id="d9585-482">Task 3 - Static Bundles</span></span>

<span data-ttu-id="d9585-483">Statik paket yaklaşımı, kullanılacak dosya kümesini, başvuruyu ve kullanılacak minbirleşme yöntemini özelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9585-483">The static bundle approach allows you to customize the set of files to bundle, the reference and the minification method that will be used.</span></span>

<span data-ttu-id="d9585-484">Bu görevde, bir statik paketi, paketleyip daha sonra ayarlanacak belirli bir dosya kümesini tanımlayacak şekilde yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="d9585-484">In this task, you will configure a static bundle to define a specific set of files to bundle and minify.</span></span>

1. <span data-ttu-id="d9585-485">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="d9585-485">Close the browser.</span></span>
2. <span data-ttu-id="d9585-486">**Global.asax.cs** dosyasını açın ve **uygulama\_start** metodunu bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-486">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
3. <span data-ttu-id="d9585-487">Aşağıdaki kodda gösterildiği gibi statik paket kodunun açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d9585-487">Uncomment the static bundle code as shown in the code below.</span></span>

    <span data-ttu-id="d9585-488">&quot; **~/Staticdemeti**&quot; sanal yol ile başvurulacak bir statik paket tanımlıyor ve tüm belirtilen dosyaları **AddFile** yöntemiyle birlikte kullanmak Için **jsminbelirt** komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9585-488">You are defining a static bundle that will be referenced with the &quot;**~/StaticBundle**&quot; virtual path and use **JsMinify** for minification of all the specified files with the **AddFile** method.</span></span> <span data-ttu-id="d9585-489">Son olarak, statik demeti **paketleme** ve olanaklı hale getirecek olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d9585-489">Finally, you are adding the static bundle to the **BundleTable** and enabling it.</span></span>

    <span data-ttu-id="d9585-490">Dosyaların aynı yerde olmadığına dikkat edin; Bu, varsayılan paketlemeye göre başka bir avantajdır.</span><span class="sxs-lookup"><span data-stu-id="d9585-490">Notice that the files are not located in the same place; this is another advantage over the default bundling.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. <span data-ttu-id="d9585-491">**Optimizasyon. aspx** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-491">Open the **Optimization.aspx** file.</span></span>

    <span data-ttu-id="d9585-492">**STATIK js demeti** bağlantısının, Global.asax.cs dosyasındaki statik paketi yapılandırırken bildirdiğiniz yolu kullandığını ve **/staticdemeti**olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-492">Notice that the link to **Static JS Bundle** is using the path you have declared when you configured the static bundle in the Global.asax.cs file: **/StaticBundle**.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. <span data-ttu-id="d9585-493">Uygulamayı çalıştırmak için **F5** tuşuna basın ve ardından **iyileştirme** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="d9585-493">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
6. <span data-ttu-id="d9585-494">Dosyayı açmak için **STATIC js paket** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-494">Click on the **Static JS Bundle** link to open the file.</span></span>

    <span data-ttu-id="d9585-495">Küçültülmüş olan paketlenmiş JavaScript dosyasının, &quot;/Staticdemeti&quot;yolu altındaki statik paket dosyasında yapılandırılan tüm JavaScript dosyaları için çıkış olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-495">Notice that the minified bundled JavaScript file is the output for all the JavaScript files configured in the static bundle file under the path &quot;/StaticBundle&quot;.</span></span>

    <span data-ttu-id="d9585-496">![Statik JavaScript dosyaları demeti](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Statik JavaScript dosyaları demeti")</span><span class="sxs-lookup"><span data-stu-id="d9585-496">![Static JavaScript files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Static JavaScript files bundle")</span></span>

    <span data-ttu-id="d9585-497">*Statik JavaScript dosyaları demeti*</span><span class="sxs-lookup"><span data-stu-id="d9585-497">*Static JavaScript files bundle*</span></span>
7. <span data-ttu-id="d9585-498">Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="d9585-498">Close the browser and return to Visual Studio.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a><span data-ttu-id="d9585-499">Görev 4-dinamik klasör demeti</span><span class="sxs-lookup"><span data-stu-id="d9585-499">Task 4 - Dynamic Folder Bundles</span></span>

<span data-ttu-id="d9585-500">Bu görevde, dinamik klasör paketlerini yapılandırmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-500">In this task, you will learn how to configure dynamic folder bundles.</span></span> <span data-ttu-id="d9585-501">Dinamik paket oluşturma işleminin gücü, statik JavaScript 'in yanı sıra JavaScript 'e derlenen dillerdeki diğer dosyaları da dahil edebilir ve bu nedenle, paket yürütülmeden önce bazı işlemler yapılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d9585-501">The power of dynamic bundling is that you can include static JavaScript, as well as other files in languages that compiles into JavaScript, and thus, require some processing before the bundling is executed.</span></span>

<span data-ttu-id="d9585-502">Bu örnekte, CofeeScript içinde yazılmış dosyalar için dinamik bir paket oluşturmak üzere **Dynamicfolderdemeti** sınıfını nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-502">In this example, you will learn how to use the **DynamicFolderBundle** class to create a dynamic bundle for files written in CofeeScript.</span></span> <span data-ttu-id="d9585-503">CofeeScript, JavaScript 'e derlenen ve JavaScript kodunu yazmak, JavaScript 'in kısaltma ve okunabilirliğini geliştirmek için daha basit bir sözdizimi sağlayan bir programlama dilidir.</span><span class="sxs-lookup"><span data-stu-id="d9585-503">CofeeScript is a programming language that compiles into JavaScript and provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability.</span></span>

1. <span data-ttu-id="d9585-504">**Global.asax.cs** dosyasını açın ve **uygulama\_start** metodunu bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-504">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
2. <span data-ttu-id="d9585-505">Aşağıdaki kodda gösterildiği gibi dinamik paket kodunun açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d9585-505">Uncomment the dynamic bundle code as shown in the code below.</span></span>

    <span data-ttu-id="d9585-506">Yalnızca &quot; **. kahve**&quot; uzantısı (CoffeeScript dosyaları) olan dosyalara uygulanacak olan **CoffeeMinify** özel minbirleşme işlemcisini kullanacak dinamik bir klasör paketi tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9585-506">You are defining a dynamic folder bundle that will use the **CoffeeMinify** custom minification processor that will only apply to the files with the &quot;**.coffee**&quot; extension (CoffeeScript files).</span></span> <span data-ttu-id="d9585-507">'\*. kahve ' gibi bir klasör içinde paketedilecek dosyaları seçmek için bir arama kalıbı kullanacağınızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-507">Notice that you can use a search pattern to select the files to bundle within a folder, like '\*.coffee'.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. <span data-ttu-id="d9585-508">NuGet Paket Yöneticisi konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-508">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="d9585-509">Bunu yapmak için, **diğer Windows** | **paket Yöneticisi konsolu** | menü **görünümünü** kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9585-509">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>
4. <span data-ttu-id="d9585-510">**Paket Yöneticisi konsolunda** **Install-Package CoffeeSharp** yazın ve **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d9585-510">In the **Package Manager Console,** type **Install-Package CoffeeSharp** and press **ENTER**.</span></span>
5. <span data-ttu-id="d9585-511">**Çözüm Gezgini** penceresindeki **tüm dosyaları göster** düğmesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="d9585-511">Click the **Show All Files** button in the **Solution Explorer** window</span></span>

    <span data-ttu-id="d9585-512">![Tüm dosyalar gösteriliyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Tüm dosyalar gösteriliyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-512">![Showing all files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Showing all files")</span></span>

    <span data-ttu-id="d9585-513">*Tüm dosyalar gösteriliyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-513">*Showing all files*</span></span>
6. <span data-ttu-id="d9585-514">**Çözüm Gezgini** **CoffeeMinify.cs** dosyasına sağ tıklayın ve **projeye dahil et** ' i seçin</span><span class="sxs-lookup"><span data-stu-id="d9585-514">Right click the **CoffeeMinify.cs** file in the **Solution Explorer** and select **Include in Project**</span></span>

    <span data-ttu-id="d9585-515">![CoffeeMinify.cs dosyasını projeye dahil et](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "CoffeeMinify.cs dosyasını projeye dahil et")</span><span class="sxs-lookup"><span data-stu-id="d9585-515">![Include the CoffeeMinify.cs file in the project](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Include the CoffeeMinify.cs file in the project")</span></span>

    <span data-ttu-id="d9585-516">*CoffeeMinify.cs dosyasını projeye dahil et*</span><span class="sxs-lookup"><span data-stu-id="d9585-516">*Include the CoffeeMinify.cs file in the project*</span></span>
7. <span data-ttu-id="d9585-517">**CoffeeMinify.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-517">Open the **CoffeeMinify.cs** file.</span></span>

    <span data-ttu-id="d9585-518">Bu sınıf, CoffeeScript kod derlemesinden kaynaklanan JavaScript çıkışını minmek için Jsminbelirt 'ten devralır.</span><span class="sxs-lookup"><span data-stu-id="d9585-518">This class inherits from JsMinify to minify the JavaScript output resulting from the CoffeeScript code compilation.</span></span> <span data-ttu-id="d9585-519">Önce JavaScript kodunu oluşturmak için CoffeeScript derleyicisini çağırır ve sonra ortaya çıkan kodu minsminbelirt. Process yöntemine gönderir.</span><span class="sxs-lookup"><span data-stu-id="d9585-519">It calls the CoffeeScript compiler to generate the JavaScript code first, and then it sends it to the JsMinify.Process method to minify the resulting code.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. <span data-ttu-id="d9585-520">**Betikler/paket** klasöründen **Script1. kahve** ve **Script2. kahve** dosyalarını açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-520">Open the **Script1.coffee** and **Script2.coffee** files from the **Scripts/bundle** folder.</span></span>

    <span data-ttu-id="d9585-521">Bu dosyalar, CoffeeMinify sınıfı ile paketleme gerçekleştirilirken derlenecek CoffeScript kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="d9585-521">These files will include the CoffeScript code to be compiled while performing the bundling with the CoffeeMinify class.</span></span>

    <span data-ttu-id="d9585-522">Kolaylık sağlamak için, belirtilen CoffeeScript dosyaları yalnızca CoffeeScript örnek kodu dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d9585-522">For simplicity purposes, the CoffeeScript files provided are only including CoffeeScript sample code.</span></span> <span data-ttu-id="d9585-523">Yorumlar, Jsminbelirt işlemi tarafından dışlanır.</span><span class="sxs-lookup"><span data-stu-id="d9585-523">The comments are excluded by the JsMinify process.</span></span>

    <span data-ttu-id="d9585-524">![CoffeeScript dosyaları](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript dosyaları")</span><span class="sxs-lookup"><span data-stu-id="d9585-524">![CoffeeScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript files")</span></span>

    <span data-ttu-id="d9585-525">*CoffeeScript dosyaları*</span><span class="sxs-lookup"><span data-stu-id="d9585-525">*CoffeeScript files*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-526">[Cofeescript](https://github.com/jashkenas/coffeescript/) , JavaScript kodu yazmak, JavaScript 'in breçekimi ve okunabilirliğini geliştirmek için daha basit bir sözdizimi sağlar ve dizi kavrama ve model eşleştirme gibi diğer özellikleri de ekler.</span><span class="sxs-lookup"><span data-stu-id="d9585-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability, as well as adding other features like array comprehension and pattern matching.</span></span>
9. <span data-ttu-id="d9585-527">**Optimizasyon. aspx** dosyasını açın ve paket bağlantılarını bulun.</span><span class="sxs-lookup"><span data-stu-id="d9585-527">Open the **Optimization.aspx** file and locate the bundle links.</span></span>

    <span data-ttu-id="d9585-528">**Dınamık js demeti** bağlantısının, dinamik klasör paketi için yapılandırdığınız **/Coffee** sonekini kullanarak **betikler/paket** klasörüne başvurduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9585-528">Notice that the link to **Dynamic JS Bundle** is referencing the **Scripts/bundle** folder by using the **/Coffee** suffix you configured for the dynamic folder bundle.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. <span data-ttu-id="d9585-529">Uygulamayı çalıştırmak için **F5** tuşuna basın ve ardından **iyileştirme** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="d9585-529">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
11. <span data-ttu-id="d9585-530">Oluşturulan dosyayı açmak için **dınamık js paketi** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-530">Click on the **Dynamic JS Bundle** link to open the generated file.</span></span>

    <span data-ttu-id="d9585-531">Bu pakete eklenen içeriğin yalnızca **. kahve** dosyaları içerdiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-531">Notice that the content that was included in this bundle only contains **.coffee** files.</span></span> <span data-ttu-id="d9585-532">Ayrıca, CoffeeScript kodunun JavaScript 'e derlendiğini ve açıklamalı hatların kaldırıldığını de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-532">You can also see that the CoffeeScript code was compiled to JavaScript and the commented-out lines has been removed.</span></span>

    <span data-ttu-id="d9585-533">![Dinamik JS dosya demeti](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dinamik JS dosya demeti")</span><span class="sxs-lookup"><span data-stu-id="d9585-533">![Dynamic JS files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dynamic JS files bundle")</span></span>

    <span data-ttu-id="d9585-534">*Dinamik JS dosya demeti*</span><span class="sxs-lookup"><span data-stu-id="d9585-534">*Dynamic JS files bundle*</span></span>

> [!NOTE]
> <span data-ttu-id="d9585-535">Ek olarak, bu uygulamayı Microsoft Azure Web siteleri ' ne ek [B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixB)için de dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-535">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="d9585-536">Özet</span><span class="sxs-lookup"><span data-stu-id="d9585-536">Summary</span></span>

<span data-ttu-id="d9585-537">Bu laboratuvar, Visual Studio 2012 ' de ASP.NET ve Web geliştirme 'daki yenilikleri ve Visual Studio 2012 ' deki çeşitli geliştirmelerden nasıl yararlanabilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9585-537">This lab helps you to understand what New in ASP.NET and Web Development in Visual Studio 2012 is and how to take advantage of the variety of enhancements in Visual Studio 2012.</span></span>

<span data-ttu-id="d9585-538">Bu uygulamalı Laboratuvarı tamamlayarak, CSS, JavaScript ve HTML için Visual Studio 2012 düzenleyicilerde yeni özellik ve geliştirmeleri nasıl kullanacağınızı öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-538">By completing this Hands-On Lab, you have learnt how to use the new features and improvements in Visual Studio 2012 Editors for CSS, JavaScript and HTML.</span></span> <span data-ttu-id="d9585-539">Ayrıca, Visual Studio 2012 'nin yerleşik paketleme ve küçültmeye nasıl uyguladığı hakkında bilgi edinirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-539">In addition, you have learnt how Visual Studio 2012 implements built-in bundling and minification.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="d9585-540">Ek A: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="d9585-540">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="d9585-541">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-541">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="d9585-542">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9585-542">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="d9585-543">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin.</span><span class="sxs-lookup"><span data-stu-id="d9585-543">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="d9585-544">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-544">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="d9585-545">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-545">Click on **Install Now**.</span></span> <span data-ttu-id="d9585-546">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-546">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="d9585-547">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-547">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="d9585-548">![Visual Studio Express yüklensin](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="d9585-548">![Install Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="d9585-549">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="d9585-549">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="d9585-550">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-550">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    <span data-ttu-id="d9585-552">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="d9585-552">*Accepting the license terms*</span></span>
5. <span data-ttu-id="d9585-553">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-553">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    <span data-ttu-id="d9585-555">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="d9585-555">*Installation progress*</span></span>
6. <span data-ttu-id="d9585-556">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-556">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    <span data-ttu-id="d9585-558">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="d9585-558">*Installation completed*</span></span>
7. <span data-ttu-id="d9585-559">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-559">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="d9585-560">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-560">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    <span data-ttu-id="d9585-562">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="d9585-562">*VS Express for Web tile*</span></span>

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="d9585-563">Ek B: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="d9585-563">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="d9585-564">Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9585-564">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="d9585-565">Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9585-565">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="d9585-566">[Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d9585-566">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-567">Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-567">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="d9585-568">[Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-568">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="d9585-569">![Windows Azure portal oturum açın](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Windows Azure portal oturum açın")</span><span class="sxs-lookup"><span data-stu-id="d9585-569">![Log on to Windows Azure portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="d9585-570">*Windows Azure 'da oturum açma Yönetim Portalı*</span><span class="sxs-lookup"><span data-stu-id="d9585-570">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="d9585-571">Komut çubuğunda **Yeni** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-571">Click **New** on the command bar.</span></span>

    <span data-ttu-id="d9585-572">![Yeni bir Web sitesi oluşturma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="d9585-572">![Creating a new Web Site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="d9585-573">*Yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d9585-573">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="d9585-574">**İşlem** | **Web sitesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-574">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="d9585-575">Sonra **hızlı oluştur** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-575">Then select **Quick Create** option.</span></span> <span data-ttu-id="d9585-576">Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-576">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-577">Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="d9585-577">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="d9585-578">Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9585-578">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="d9585-579">Bir veritabanı ayarlamaya yönelik adımları içermez.</span><span class="sxs-lookup"><span data-stu-id="d9585-579">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="d9585-580">![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="d9585-580">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="d9585-581">*Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d9585-581">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="d9585-582">Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-582">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="d9585-583">Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-583">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="d9585-584">Yeni Web sitesinin çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d9585-584">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="d9585-585">![Yeni Web sitesine göz atma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Yeni Web sitesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="d9585-585">![Browsing to the new web site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="d9585-586">*Yeni Web sitesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="d9585-586">*Browsing to the new web site*</span></span>

    <span data-ttu-id="d9585-587">![Web sitesi çalışıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web sitesi çalışıyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-587">![Web site running](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web site running")</span></span>

    <span data-ttu-id="d9585-588">*Web sitesi çalışıyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-588">*Web site running*</span></span>
6. <span data-ttu-id="d9585-589">Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-589">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="d9585-590">![Web sitesi yönetim sayfalarını açma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Web sitesi yönetim sayfalarını açma")</span><span class="sxs-lookup"><span data-stu-id="d9585-590">![Opening the web site management pages](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="d9585-591">*Web sitesi yönetim sayfalarını açma*</span><span class="sxs-lookup"><span data-stu-id="d9585-591">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="d9585-592">**Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-592">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-593">*Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="d9585-593">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="d9585-594">Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d9585-594">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="d9585-595">**Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d9585-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="d9585-596">![Web sitesi yayımlama profili indiriliyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Web sitesi yayımlama profili indiriliyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-596">![Downloading the web site publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="d9585-597">*Web sitesi yayımlama profili indiriliyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-597">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="d9585-598">Yayımlama profili dosyasını bilinen bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="d9585-598">Download the publish profile file to a known location.</span></span> <span data-ttu-id="d9585-599">Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-599">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="d9585-600">![Yayımlama profili dosyası kaydediliyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Yayımlama profili kaydediliyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-600">![Saving the publish profile file](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Saving the publish profile")</span></span>

    <span data-ttu-id="d9585-601">*Yayımlama profili dosyası kaydediliyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-601">*Saving the publish profile file*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="d9585-602">Görev 2-veritabanı sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d9585-602">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="d9585-603">Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9585-603">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="d9585-604">SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-604">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="d9585-605">Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d9585-605">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="d9585-606">SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-606">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="d9585-607">Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9585-607">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="d9585-608">**Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın.</span><span class="sxs-lookup"><span data-stu-id="d9585-608">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="d9585-609">Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-609">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="d9585-610">![SQL veritabanı sunucu panosu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL veritabanı sunucu panosu")</span><span class="sxs-lookup"><span data-stu-id="d9585-610">![SQL Database Server Dashboard](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="d9585-611">*SQL veritabanı sunucu panosu*</span><span class="sxs-lookup"><span data-stu-id="d9585-611">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="d9585-612">Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9585-612">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="d9585-613">Bunu yapmak için **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="d9585-613">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes.</span></span> <span data-ttu-id="d9585-614">Kural için bir ad girin ve Add-Client-ip-Address-ok-Button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) düğmesine ![tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-614">Enter a name for the rule and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) button.</span></span>

    ![Istemci IP adresi ekleniyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    <span data-ttu-id="d9585-616">*Istemci IP adresi ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-616">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="d9585-617">**ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-617">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Değişiklikleri Onayla](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    <span data-ttu-id="d9585-619">*Değişiklikleri Onayla*</span><span class="sxs-lookup"><span data-stu-id="d9585-619">*Confirm Changes*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="d9585-620">Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="d9585-620">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="d9585-621">ASP.NET MVC 4 çözümüne geri dönün.</span><span class="sxs-lookup"><span data-stu-id="d9585-621">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="d9585-622">**Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="d9585-622">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="d9585-623">![Uygulama yayımlanıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Uygulamayı Yayımlama")</span><span class="sxs-lookup"><span data-stu-id="d9585-623">![Publishing the Application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publishing the Application")</span></span>

    <span data-ttu-id="d9585-624">*Web sitesi yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-624">*Publishing the web site*</span></span>
2. <span data-ttu-id="d9585-625">İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="d9585-625">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="d9585-626">![Yayımlama profilini içeri aktarma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Yayımlama profilini içeri aktarma")</span><span class="sxs-lookup"><span data-stu-id="d9585-626">![Importing the publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Importing the publish profile")</span></span>

    <span data-ttu-id="d9585-627">*Yayımlama profili içeri aktarılıyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-627">*Importing publish profile*</span></span>
3. <span data-ttu-id="d9585-628">**Bağlantıyı doğrula**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-628">Click **Validate Connection**.</span></span> <span data-ttu-id="d9585-629">Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-629">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9585-630">Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="d9585-630">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="d9585-631">![Bağlantı doğrulanıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Bağlantı doğrulanıyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-631">![Validating connection](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Validating connection")</span></span>

    <span data-ttu-id="d9585-632">*Bağlantı doğrulanıyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-632">*Validating connection*</span></span>
4. <span data-ttu-id="d9585-633">**Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-633">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="d9585-634">![Web dağıtımı yapılandırması](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web dağıtımı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="d9585-634">![Web deploy configuration](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy configuration")</span></span>

    <span data-ttu-id="d9585-635">*Web dağıtımı yapılandırması*</span><span class="sxs-lookup"><span data-stu-id="d9585-635">*Web deploy configuration*</span></span>
5. <span data-ttu-id="d9585-636">Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="d9585-636">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="d9585-637">**Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.</span><span class="sxs-lookup"><span data-stu-id="d9585-637">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="d9585-638">**Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="d9585-638">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="d9585-639">**Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="d9585-639">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="d9585-640">Yeni bir veritabanı adı yazın, örneğin: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="d9585-640">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="d9585-641">![Hedef bağlantı dizesi yapılandırılıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Hedef bağlantı dizesi yapılandırılıyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-641">![Configuring destination connection string](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="d9585-642">*Hedef bağlantı dizesi yapılandırılıyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-642">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="d9585-643">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-643">Then click **OK**.</span></span> <span data-ttu-id="d9585-644">Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-644">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="d9585-645">![Veritabanı oluşturma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Veritabanı dizesi oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-645">![Creating the database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Creating the database string")</span></span>

    <span data-ttu-id="d9585-646">*Veritabanı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d9585-646">*Creating the database*</span></span>
7. <span data-ttu-id="d9585-647">Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d9585-647">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="d9585-648">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-648">Then click **Next**.</span></span>

    <span data-ttu-id="d9585-649">![SQL veritabanı 'na işaret eden bağlantı dizesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "SQL veritabanı 'na işaret eden bağlantı dizesi")</span><span class="sxs-lookup"><span data-stu-id="d9585-649">![Connection string pointing to SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="d9585-650">*SQL veritabanı 'na işaret eden bağlantı dizesi*</span><span class="sxs-lookup"><span data-stu-id="d9585-650">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="d9585-651">**Önizleme** sayfasında **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9585-651">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="d9585-652">![Web uygulaması yayımlanıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Web uygulaması yayımlanıyor")</span><span class="sxs-lookup"><span data-stu-id="d9585-652">![Publishing the web application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publishing the web application")</span></span>

    <span data-ttu-id="d9585-653">*Web uygulaması yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="d9585-653">*Publishing the web application*</span></span>
9. <span data-ttu-id="d9585-654">Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.</span><span class="sxs-lookup"><span data-stu-id="d9585-654">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="d9585-655">![Windows Azure 'da yayımlanan uygulama](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Windows Azure 'da yayımlanan uygulama")</span><span class="sxs-lookup"><span data-stu-id="d9585-655">![Application published to Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="d9585-656">*Windows Azure 'da yayımlanan uygulama*</span><span class="sxs-lookup"><span data-stu-id="d9585-656">*Application published to Windows Azure*</span></span>
