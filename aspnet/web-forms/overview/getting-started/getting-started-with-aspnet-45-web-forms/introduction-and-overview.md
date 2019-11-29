---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4,7 Web Forms ve Visual Studio 2017 ile çalışmaya başlama | Microsoft Docs
author: Erikre
description: Bu adım adım öğretici serisi, ASP.NET 4,7 ve Microsoft Visual Studio kullanarak bir ASP.NET Web Forms uygulaması oluşturmaya ilişkin temel bilgileri öğretir.
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615461"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="fde49-103">ASP.NET 4,5 Web Forms ve Visual Studio 2017 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fde49-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>

<span data-ttu-id="fde49-104">[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="fde49-104">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="fde49-105">Bu öğretici serisinde, ASP.NET 4,5 ve Microsoft Visual Studio 2017 ile bir ASP.NET Web Forms uygulamasının nasıl oluşturulacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fde49-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="fde49-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="fde49-106">Introduction</span></span>

<span data-ttu-id="fde49-107">Bu öğretici serisi, Visual Studio 2017 ve ASP.NET 4,5 kullanarak bir ASP.NET Web Forms uygulaması oluşturma konusunda size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="fde49-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="fde49-108">Çevrimiçi bir storefront Web sitesi olan **Wingtip Toys** adlı bir uygulama oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fde49-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="fde49-109">Seriler sırasında yeni ASP.NET 4,5 özellikleri vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="fde49-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="fde49-110">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="fde49-110">Target audience</span></span>

<span data-ttu-id="fde49-111">ASP.NET Web Forms yeni geliştiriciler, bu öğretici serisi için hedef kitledir.</span><span class="sxs-lookup"><span data-stu-id="fde49-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="fde49-112">Aşağıdaki alanlarda bazı bilgilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fde49-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="fde49-113">Nesne odaklı programlama (OOP) ve diller</span><span class="sxs-lookup"><span data-stu-id="fde49-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="fde49-114">Web geliştirme (HTML, CSS, JavaScript)</span><span class="sxs-lookup"><span data-stu-id="fde49-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="fde49-115">İlişkisel veritabanları</span><span class="sxs-lookup"><span data-stu-id="fde49-115">Relational databases</span></span>
- <span data-ttu-id="fde49-116">N katmanlı mimari</span><span class="sxs-lookup"><span data-stu-id="fde49-116">N-tier architecture</span></span>

<span data-ttu-id="fde49-117">Bu alanı gözden geçirmek için aşağıdaki içeriği kullanmayı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="fde49-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="fde49-118">Görsele BaşlarkenC#</span><span class="sxs-lookup"><span data-stu-id="fde49-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="fde49-119">[Web geliştirme](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, php, jQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="fde49-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="fde49-120">İlişkisel veritabanı</span><span class="sxs-lookup"><span data-stu-id="fde49-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="fde49-121">Çok katmanlı mimari</span><span class="sxs-lookup"><span data-stu-id="fde49-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="fde49-122">Uygulama özellikleri</span><span class="sxs-lookup"><span data-stu-id="fde49-122">Application features</span></span>

<span data-ttu-id="fde49-123">Bu dizide sunulan ASP.NET Web form özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fde49-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="fde49-124">Web uygulaması projesi (Web sitesi projesi değil)</span><span class="sxs-lookup"><span data-stu-id="fde49-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="fde49-125">Web Forms</span><span class="sxs-lookup"><span data-stu-id="fde49-125">Web Forms</span></span>
- <span data-ttu-id="fde49-126">Ana sayfalar, yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fde49-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="fde49-127">Yükleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fde49-127">Bootstrap</span></span>
- <span data-ttu-id="fde49-128">Entity Framework Code First, LocalDB</span><span class="sxs-lookup"><span data-stu-id="fde49-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="fde49-129">İstek doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fde49-129">Request Validation</span></span>
- <span data-ttu-id="fde49-130">Kesin tür belirtilmiş veri denetimleri</span><span class="sxs-lookup"><span data-stu-id="fde49-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="fde49-131">Model bağlama</span><span class="sxs-lookup"><span data-stu-id="fde49-131">Model Binding</span></span>
- <span data-ttu-id="fde49-132">Veri Açıklamaları</span><span class="sxs-lookup"><span data-stu-id="fde49-132">Data Annotations</span></span>
- <span data-ttu-id="fde49-133">Değer sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="fde49-133">Value Providers</span></span>
- <span data-ttu-id="fde49-134">SSL ve OAuth</span><span class="sxs-lookup"><span data-stu-id="fde49-134">SSL and OAuth</span></span>
- <span data-ttu-id="fde49-135">ASP.NET Identity, yapılandırma ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="fde49-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="fde49-136">Unobtrusive doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fde49-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="fde49-137">Yönlendirme</span><span class="sxs-lookup"><span data-stu-id="fde49-137">Routing</span></span>
- <span data-ttu-id="fde49-138">ASP.NET Hata İşleme</span><span class="sxs-lookup"><span data-stu-id="fde49-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="fde49-139">Uygulama senaryoları ve görevler</span><span class="sxs-lookup"><span data-stu-id="fde49-139">Application scenarios and tasks</span></span>

<span data-ttu-id="fde49-140">Öğretici serisi görevleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fde49-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="fde49-141">Yeni bir proje oluşturma, gözden geçirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="fde49-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="fde49-142">Veritabanı yapısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fde49-142">Creating a database structure</span></span>
- <span data-ttu-id="fde49-143">Veritabanını başlatma ve sağlama</span><span class="sxs-lookup"><span data-stu-id="fde49-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="fde49-144">Kullanıcı arabirimini stillerle, grafiklerle ve ana sayfayla özelleştirme</span><span class="sxs-lookup"><span data-stu-id="fde49-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="fde49-145">Sayfa ve gezinti ekleme</span><span class="sxs-lookup"><span data-stu-id="fde49-145">Adding pages and navigation</span></span>
- <span data-ttu-id="fde49-146">Menü ayrıntılarını ve ürün verilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="fde49-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="fde49-147">Alışveriş sepeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="fde49-147">Creating a shopping cart</span></span>
- <span data-ttu-id="fde49-148">SSL ve OAuth desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="fde49-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="fde49-149">Ödeme yöntemi ekleme</span><span class="sxs-lookup"><span data-stu-id="fde49-149">Adding a payment method</span></span>
- <span data-ttu-id="fde49-150">Uygulamaya yönetici rolü ve Kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="fde49-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="fde49-151">Belirli sayfalara ve klasöre erişimi sınırlandırma</span><span class="sxs-lookup"><span data-stu-id="fde49-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="fde49-152">Web uygulamasına bir dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="fde49-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="fde49-153">Giriş doğrulaması uygulama</span><span class="sxs-lookup"><span data-stu-id="fde49-153">Implementing input validation</span></span>
- <span data-ttu-id="fde49-154">Web uygulaması için rotalar kaydetme</span><span class="sxs-lookup"><span data-stu-id="fde49-154">Registering routes for the web application</span></span>
- <span data-ttu-id="fde49-155">Hata işleme ve hata günlüğü uygulama</span><span class="sxs-lookup"><span data-stu-id="fde49-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="fde49-156">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="fde49-156">Overview</span></span>

<span data-ttu-id="fde49-157">Bu öğretici serisi, programlama kavramlarını bildiğiniz bir kişiye yöneliktir, ancak yeni ASP.NET Web Forms.</span><span class="sxs-lookup"><span data-stu-id="fde49-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="fde49-158">Zaten ASP.NET Web Forms hakkında bilginiz varsa, bu seri yeni ASP.NET 4,5 özellikleri hakkında bilgi edinmenize yardımcı olmaya devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="fde49-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="fde49-159">Programlama kavramları ve ASP.NET Web Forms hakkında bilgi sahibi olan okuyucular için, ASP.NET Web sitesinin [Başlarken bölümünde sunulan](../../../index.md) ek Web Forms öğreticilere bakın.</span><span class="sxs-lookup"><span data-stu-id="fde49-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="fde49-160">Bu öğretici serisinde sunulan ASP.NET 4,5 aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="fde49-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="fde49-161">Birçok ASP.NET Çerçevesi (Web Forms, MVC ve Web API) [için destek](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) sunan projeler oluşturmaya yönelik basit bir kullanıcı arabirimi.</span><span class="sxs-lookup"><span data-stu-id="fde49-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="fde49-162">[Önyükleme](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), düzen, tema ve yanıt veren tasarım çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="fde49-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="fde49-163">[ASP.NET Identity](../../../../identity/index.md), tüm ASP.net çerçeveleri ile aynı ve IIS dışında Web barındırma yazılımıyla birlikte çalışarak yeni bir ASP.NET üyelik sistemidir.</span><span class="sxs-lookup"><span data-stu-id="fde49-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="fde49-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="fde49-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="fde49-165">Entity Framework bir güncelleştirme şunları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fde49-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="fde49-166">Verileri türü kesin belirlenmiş nesneler olarak alma ve işleme</span><span class="sxs-lookup"><span data-stu-id="fde49-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="fde49-167">Verilere zaman uyumsuz olarak erişin</span><span class="sxs-lookup"><span data-stu-id="fde49-167">Access data asynchronously</span></span>
  - <span data-ttu-id="fde49-168">Geçici bağlantı hatalarını işleme</span><span class="sxs-lookup"><span data-stu-id="fde49-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="fde49-169">SQL deyimlerini günlüğe kaydet</span><span class="sxs-lookup"><span data-stu-id="fde49-169">Log SQL statements</span></span>

<span data-ttu-id="fde49-170">Tüm ASP.NET 4,5 özellik listesi için, bkz. [Visual Studio 2013 Sürüm notları ASP.NET and Web Tools](../../../../visual-studio/overview/2013/release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="fde49-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="fde49-171">Wingtip Toys örnek uygulaması</span><span class="sxs-lookup"><span data-stu-id="fde49-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="fde49-172">Aşağıdaki ekran görüntüleri, bu öğretici serisinde oluşturduğunuz ASP.NET Web Forms uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="fde49-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="fde49-173">Uygulamayı Visual Studio 'da çalıştırdığınızda, aşağıdaki Web giriş sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fde49-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![Wingtip Toys-varsayılan sayfa](introduction-and-overview/_static/image1.png)

<span data-ttu-id="fde49-175">Yeni bir kullanıcı olarak kaydedebilir veya var olan bir kullanıcı olarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fde49-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="fde49-176">En üstteki gezinmede, ürün kategorilerinin ve bu kullanıcıların ürünleriyle ilişkili bağlantılar bulunur.</span><span class="sxs-lookup"><span data-stu-id="fde49-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="fde49-177">**Ürünler**' i seçerseniz, kullanılabilir tüm ürünler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fde49-177">If you select **Products**, all available products are displayed.</span></span> 

![Wingtip Toys-ürünler](introduction-and-overview/_static/image2.png)

<span data-ttu-id="fde49-179">Belirli bir ürünü seçerseniz ürün ayrıntıları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fde49-179">If you select a specific product, product details are displayed.</span></span>

![Wingtip Toys-ürün ayrıntıları](introduction-and-overview/_static/image3.png)

<span data-ttu-id="fde49-181">Bir kullanıcı olarak, Web Forms şablonu varsayılan işlevselliğiyle kaydedebilir ve oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fde49-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="fde49-182">Bu öğretici Ayrıca, mevcut bir Gmail hesabını kullanarak nasıl oturum bulunacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="fde49-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="fde49-183">Ayrıca, veritabanından ürün eklemek ve kaldırmak için yönetici olarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fde49-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys-oturum aç](introduction-and-overview/_static/image4.png)

<span data-ttu-id="fde49-185">Kullanıcı olarak oturum açtıktan sonra, alışveriş sepetine ürün ekleyebilir ve PayPal ile kullanıma alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fde49-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="fde49-186">Örnek uygulama, PayPal 'in geliştirici korumalı alanında çalışacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fde49-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="fde49-187">Gerçek para hareketi gerçekleşmez.</span><span class="sxs-lookup"><span data-stu-id="fde49-187">No actual money transaction takes place.</span></span>

![Wingtip Toys-alışveriş sepeti](introduction-and-overview/_static/image5.png)

<span data-ttu-id="fde49-189">PayPal hesabı, siparişi ve ödeme bilgilerinizi onaylar.</span><span class="sxs-lookup"><span data-stu-id="fde49-189">PayPal confirms your account, order, and payment information.</span></span>

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="fde49-191">PayPal 'den döndükten sonra, siparişinizi gözden geçirebilir ve tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fde49-191">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys-sipariş Incelemesi](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="fde49-193">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fde49-193">Prerequisites</span></span>

<span data-ttu-id="fde49-194">Başlamadan önce, aşağıdaki yazılımın bilgisayarınızda yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="fde49-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="fde49-195">[Microsoft Visual Studio 2017 veya Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fde49-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="fde49-196">.NET Framework otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fde49-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="fde49-197">Bu öğretici serisi 2017 Microsoft Visual Studio Community kullanır.</span><span class="sxs-lookup"><span data-stu-id="fde49-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="fde49-198">Bu öğretici serisini tamamlayabilmeniz için ya da Microsoft Visual Studio 2017 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fde49-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="fde49-199">Visual Studio hakkında aşağıdakileri göz önünde edin:</span><span class="sxs-lookup"><span data-stu-id="fde49-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="fde49-200">Microsoft Visual Studio 2017 ve Microsoft Visual Studio Community 2017, bu öğretici serisinin tamamında *Visual Studio* olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="fde49-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="fde49-201">Visual Studio 2017, zaten yüklü olan tüm eski sürümlerin yanına yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fde49-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="fde49-202">Önceki sürümlerde oluşturulan siteler, Visual Studio 2017 ' de açılabilir ve önceki sürümlerde açılmaya devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="fde49-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="fde49-203">Visual Studio 'Yu ilk kez başlattığınızda, *Web geliştirme* ayarlarını seçtiğiniz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="fde49-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="fde49-204">Daha fazla bilgi için bkz. [nasıl yapılır: Web geliştirme ortamı ayarlarını seçme](https://msdn.microsoft.com/library/ff521558.aspx).</span><span class="sxs-lookup"><span data-stu-id="fde49-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="fde49-205">Önkoşulları yükledikten sonra, bu öğretici serisinde sunulan Web projesini oluşturmaya başlamaya hazırsınız demektir.</span><span class="sxs-lookup"><span data-stu-id="fde49-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="fde49-206">Örnek uygulamayı indirin</span><span class="sxs-lookup"><span data-stu-id="fde49-206">Download the sample application</span></span>

 <span data-ttu-id="fde49-207">Tamamlanmış örnek uygulamayı dilediğiniz zaman MSDN örnekleri sitesinden indirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fde49-207">You can download the completed sample application at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="fde49-208">[ASP.NET 4,5 Web Forms ve Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fde49-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="fde49-209">Bu indirme aşağıdaki öğelere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fde49-209">This download has the following items:</span></span>

- <span data-ttu-id="fde49-210">*Wingtiptoys* klasöründeki örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="fde49-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="fde49-211">*Wingtiptoys* klasöründeki *wingtiptoys-varlıklar* klasöründe örnek uygulamayı oluşturmak için kullanılan kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="fde49-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="fde49-212">İndirme bir *. zip* dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="fde49-212">The download is a *.zip* file.</span></span> <span data-ttu-id="fde49-213">Bu öğretici serisinin oluşturduğu tamamlanmış projeyi görmek için. zip dosyasındaki *C#* klasörü bulun ve seçin.</span><span class="sxs-lookup"><span data-stu-id="fde49-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="fde49-214">Klasörünü, C# Visual Studio projeleriyle çalışmak için kullandığınız klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fde49-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="fde49-215">Varsayılan olarak, Visual Studio 2017 Projects klasörü:</span><span class="sxs-lookup"><span data-stu-id="fde49-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="fde49-216"><strong>C:\Users&#92;</strong>  <strong><em>&lt;Kullanıcı adı&gt;</em></strong> <strong>\source\repos</strong></span><span class="sxs-lookup"><span data-stu-id="fde49-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="fde49-217">***C#*** Klasörü ***wingtiptoys***olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="fde49-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="fde49-218">Projects klasörünüzde *wingtiptoys* adlı bir klasörünüz zaten varsa, *C#* klasörü *wingtiptoys*olarak yeniden adlandırmadan önce mevcut klasörü geçici olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="fde49-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="fde49-219">Tamamlanmış projeyi çalıştırmak için *wingtiptoys* klasörünü açın ve *wingtiptoys. sln* dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fde49-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="fde49-220">Visual Studio 2017 projeyi açar.</span><span class="sxs-lookup"><span data-stu-id="fde49-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="fde49-221">Sonra, **Çözüm Gezgini** ' de *default. aspx* dosyasına sağ tıklayın ve **Tarayıcıda görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="fde49-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="fde49-222">İçeriği gözden geçirmek için ASP.NET Web Forms bir test alın</span><span class="sxs-lookup"><span data-stu-id="fde49-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="fde49-223">Öğretici serisini tamamladıktan sonra, bilginizi test etmek ve temel kavramları zorlamak için bir test yapın.</span><span class="sxs-lookup"><span data-stu-id="fde49-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="fde49-224">Her soru, ek rehberlik için bir açıklama ve bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="fde49-224">Each question provides an explanation and links to additional guidance.</span></span>

* [<span data-ttu-id="fde49-225">ASP.NET Web Forms test</span><span class="sxs-lookup"><span data-stu-id="fde49-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="fde49-226">Öğretici desteği ve açıklamaları</span><span class="sxs-lookup"><span data-stu-id="fde49-226">Tutorial support and comments</span></span>

<span data-ttu-id="fde49-227">Sorular ve açıklamalar için, [ASP.NET 4,5 Web Forms ve Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) örnek sayfasında yer alan Q ve A bölümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="fde49-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="fde49-228">Bu öğretici serisinin açıklamaları hoş geldiniz.</span><span class="sxs-lookup"><span data-stu-id="fde49-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="fde49-229">Bu öğretici serisi güncelleniyorsa, iyileştirmeler için her çaba veya iyileştirmeleri göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fde49-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="fde49-230">Bir hata oluşursa, ilgili hata iletileri kafa çözme konusunda iyi bir açıklama olmadan kafa karıştırıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fde49-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="fde49-231">Yardım için [ASP.net forumlarını](https://forums.asp.net/)kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fde49-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="fde49-232">Diğer bir iyi kaynak, [ASP.NET 4,5 Web Forms ve Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) örnek sayfasındaki Q ve bir bölümdür.</span><span class="sxs-lookup"><span data-stu-id="fde49-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="fde49-233">Next</span><span class="sxs-lookup"><span data-stu-id="fde49-233">Next</span></span>](create-the-project.md)
