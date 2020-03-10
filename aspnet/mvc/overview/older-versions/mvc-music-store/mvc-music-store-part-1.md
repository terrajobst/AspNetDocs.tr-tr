---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: '1\. Bölüm: genel bakış ve Dosya-> Yeni proje | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 1\. bölüm, genel bakış ve Dosya > Yeni proje içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559985"
---
# <a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="0c6c1-104">1\. Bölüm: Genel Bakış ve Dosya->Yeni Proje</span><span class="sxs-lookup"><span data-stu-id="0c6c1-104">Part 1: Overview and File->New Project</span></span>

<span data-ttu-id="0c6c1-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="0c6c1-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="0c6c1-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="0c6c1-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="0c6c1-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="0c6c1-109">1\. bölüm, genel bakış ve dosya&gt;yeni proje içerir.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-109">Part 1 covers Overview and File-&gt;New Project.</span></span>

## <a name="overview"></a><span data-ttu-id="0c6c1-110">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="0c6c1-110">Overview</span></span>

<span data-ttu-id="0c6c1-111">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Web Developer 'ın nasıl kullanılacağı hakkında ayrıntılı bilgiler sunan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="0c6c1-112">Yavaş başlayacağız, bu nedenle başlangıç düzeyi Web geliştirme deneyimi sorunsuz.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="0c6c1-113">Oluşturmakta olduğumuz uygulama basit bir müzik deposudur.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="0c6c1-114">Uygulamanın üç ana bölümü vardır: alışveriş, kullanıma alma ve yönetim.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="0c6c1-115">Ziyaretçiler, tarza göre albümlere gözatabilir:</span><span class="sxs-lookup"><span data-stu-id="0c6c1-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="0c6c1-116">Tek bir albümü görüntüleyebilir ve bu kişinin sepetine eklemesini sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0c6c1-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="0c6c1-117">Sepetlerinde, artık istedikleri öğeleri kaldırarak kendi sepetini gözden geçirebilir:</span><span class="sxs-lookup"><span data-stu-id="0c6c1-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="0c6c1-118">Kullanıma almaya devam etmek, bir kullanıcı hesabı için oturum açmasını veya kaydolmasını ister.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="0c6c1-119">Hesap oluşturduktan sonra, Sevkiyat ve ödeme bilgilerini doldurarak siparişi tamamlayabilirler.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="0c6c1-120">Şeyleri basit tutmak için harika bir yükseltme çalıştırıyoruz: promosyon kodu "ÜCRETSIZ" olarak girerseniz her şey ücretsizdir!</span><span class="sxs-lookup"><span data-stu-id="0c6c1-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="0c6c1-121">Sipariş ettikten sonra basit bir onay ekranı görürler:</span><span class="sxs-lookup"><span data-stu-id="0c6c1-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="0c6c1-122">Müşterilere yönelik sayfalara ek olarak, yöneticilerin albüm, düzenleme ve silme yapabileceği Albümler listesini gösteren bir yönetici bölümü de oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="0c6c1-122">In addition to customer-facing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="0c6c1-123">1. dosya-&gt; yeni proje</span><span class="sxs-lookup"><span data-stu-id="0c6c1-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="0c6c1-124">Yazılımı yükleme</span><span class="sxs-lookup"><span data-stu-id="0c6c1-124">Installing the software</span></span>

<span data-ttu-id="0c6c1-125">Bu öğretici, ücretsiz Visual Web Developer 2010 Express (ücretsiz) kullanarak yeni bir ASP.NET MVC 3 projesi oluşturarak başlayacak ve ardından tamamen çalışan bir uygulama oluşturmak için artımlı olarak Özellikler ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="0c6c1-126">Bu şekilde, veritabanı erişimi, form gönderme senaryoları, veri doğrulama, tutarlı sayfa düzeni için ana sayfaları kullanma, sayfa güncelleştirmeleri ve doğrulama, Kullanıcı oturumu açma ve daha fazlası için AJAX kullanma gibi bilgileri ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="0c6c1-127">Adımları adım adım takip edebilir veya tamamlanan uygulamayı [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store)' dan indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="0c6c1-128">Uygulamayı derlemek için Visual Studio 2010 SP1 veya Visual Web Developer 2010 Express SP1 (Visual Studio 2010 ' in ücretsiz sürümü) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="0c6c1-129">Veritabanını barındırmak için SQL Server Compact (de ücretsiz) kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="0c6c1-130">Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="0c6c1-131">[Visual Studio Web Developer Express SP1 önkoşulları]</span><span class="sxs-lookup"><span data-stu-id="0c6c1-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="0c6c1-132">[ASP.NET MVC 3 araç güncelleştirmesi]</span><span class="sxs-lookup"><span data-stu-id="0c6c1-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="0c6c1-133">[SQL Server Compact 4,0]-çalışma zamanı ve araçlar desteği dahil</span><span class="sxs-lookup"><span data-stu-id="0c6c1-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>

### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="0c6c1-134">Yeni bir ASP.NET MVC 3 projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c6c1-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="0c6c1-135">Visual Web Developer 'daki Dosya menüsünden "yeni proje" seçeneğini belirleyerek başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="0c6c1-136">Bu, yeni proje iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="0c6c1-137">Sol taraftaki görsel C#&gt; Web şablonları grubunu seçeceğiz ve ardından Orta sütundaki "ASP.NET MVC 3 Web uygulaması" şablonunu seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="0c6c1-138">Projenizi MvcMusicStore olarak adlandırın ve Tamam düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="0c6c1-139">Bu, projemiz için bazı MVC 'ye özel ayarlar yapmamızı sağlayan bir ikincil iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="0c6c1-140">Aşağıdakileri seçin:</span><span class="sxs-lookup"><span data-stu-id="0c6c1-140">Select the following:</span></span>

<span data-ttu-id="0c6c1-141">Proje şablonu-boş seçin</span><span class="sxs-lookup"><span data-stu-id="0c6c1-141">Project Template - select Empty</span></span>

<span data-ttu-id="0c6c1-142">Görünüm altyapısı-Razor seçme</span><span class="sxs-lookup"><span data-stu-id="0c6c1-142">View Engine - select Razor</span></span>

<span data-ttu-id="0c6c1-143">HTML5 anlam işaretlemesi-işaretli kullan</span><span class="sxs-lookup"><span data-stu-id="0c6c1-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="0c6c1-144">Ayarlarınızın aşağıda gösterildiği gibi olduğunu doğrulayıp Tamam düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="0c6c1-145">Bu, projemizi oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-145">This will create our project.</span></span> <span data-ttu-id="0c6c1-146">Aşağıda, uygulamamıza eklenen klasörlere, sağ taraftaki Çözüm Gezgini göz atalım.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="0c6c1-147">Boş MVC 3 şablonu tamamen boş değil; temel bir klasör yapısı ekler:</span><span class="sxs-lookup"><span data-stu-id="0c6c1-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="0c6c1-148">ASP.NET MVC, klasör adları için bazı temel adlandırma kurallarını kullanır:</span><span class="sxs-lookup"><span data-stu-id="0c6c1-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="0c6c1-149">**Klasör**</span><span class="sxs-lookup"><span data-stu-id="0c6c1-149">**Folder**</span></span> | <span data-ttu-id="0c6c1-150">**Amaç**</span><span class="sxs-lookup"><span data-stu-id="0c6c1-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="0c6c1-151">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="0c6c1-151">**/Controllers**</span></span> | <span data-ttu-id="0c6c1-152">Denetleyiciler tarayıcıdan girişe yanıt verir, onunla ne yapacağınıza karar verir ve kullanıcıya yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="0c6c1-153">**/Views**</span><span class="sxs-lookup"><span data-stu-id="0c6c1-153">**/Views**</span></span> | <span data-ttu-id="0c6c1-154">UI şablonlarımızı tutan görünümler</span><span class="sxs-lookup"><span data-stu-id="0c6c1-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="0c6c1-155">**/Modeller**</span><span class="sxs-lookup"><span data-stu-id="0c6c1-155">**/Models**</span></span> | <span data-ttu-id="0c6c1-156">Modeller verileri tutar ve işleyebilir</span><span class="sxs-lookup"><span data-stu-id="0c6c1-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="0c6c1-157">**/Content**</span><span class="sxs-lookup"><span data-stu-id="0c6c1-157">**/Content**</span></span> | <span data-ttu-id="0c6c1-158">Bu klasör görüntülerimizi, CSS 'yi ve diğer tüm statik içerikleri barındırır</span><span class="sxs-lookup"><span data-stu-id="0c6c1-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="0c6c1-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="0c6c1-159">**/Scripts**</span></span> | <span data-ttu-id="0c6c1-160">Bu klasör JavaScript dosyalarımı barındırır</span><span class="sxs-lookup"><span data-stu-id="0c6c1-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="0c6c1-161">ASP.NET MVC çerçevesi varsayılan olarak "yapılandırma üzerinden kural" yaklaşımı kullandığından ve klasör adlandırma kurallarına göre bazı varsayılan varsayımlar yaptığından, bu klasörler boş bir ASP.NET MVC uygulamasında bile bulunur.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="0c6c1-162">Örneğin, denetleyicilerde açıkça bunu belirtmek zorunda kalmadan, denetleyiciler görünümler klasöründeki görünümleri varsayılan olarak arar.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="0c6c1-163">Varsayılan kurallara uyma, yazmanız gereken kod miktarını azaltır ve diğer geliştiricilerin projenizi anlamasına daha da kolay hale gelir.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="0c6c1-164">Uygulamamızı oluşturduğumuzdan bu kuralları daha anlatacağız.</span><span class="sxs-lookup"><span data-stu-id="0c6c1-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0c6c1-165">Next</span><span class="sxs-lookup"><span data-stu-id="0c6c1-165">Next</span></span>](mvc-music-store-part-2.md)
