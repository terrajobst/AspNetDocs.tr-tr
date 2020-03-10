---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Nerdakşam yemeği öğreticisine giriş | Microsoft Docs
author: shanselman
description: Yeni bir çerçeve öğrenmenin en iyi yolu, onunla bir şey oluşturmak. Bu öğreticide, ASP.NE kullanarak küçük, ancak tamamlanmış bir uygulama oluşturma işlemi gösterilmektedir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580579"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="a9168-104">NerdDinner Öğreticisine Giriş</span><span class="sxs-lookup"><span data-stu-id="a9168-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="a9168-105">[Scott Hanselman](https://github.com/shanselman) tarafından</span><span class="sxs-lookup"><span data-stu-id="a9168-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="a9168-106">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="a9168-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="a9168-107">Yeni bir çerçeve öğrenmenin en iyi yolu, onunla bir şey oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="a9168-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="a9168-108">Bu öğreticide, ASP.NET MVC 1 kullanarak küçük, ancak tamamlanmış bir uygulamanın nasıl oluşturulacağı ve bunun arkasındaki temel kavramlardan bazıları tanıtılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a9168-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="a9168-109">ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="a9168-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="a9168-110">Nerdakşam yemeği öğreticisi</span><span class="sxs-lookup"><span data-stu-id="a9168-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="a9168-111">Yeni bir çerçeve öğrenmenin en iyi yolu, onunla bir şey oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="a9168-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="a9168-112">Bu öğreticide, ASP.NET MVC kullanarak küçük, ancak tamamlanmış bir uygulama oluşturma ve bunun arkasındaki temel kavramlardan bazıları tanıtılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a9168-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="a9168-113">Derleyeceğiz uygulama "Nerdakşam yemeği" olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a9168-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="a9168-114">Nerdakşam yemeği, kullanıcıların dinleleri çevrimiçi bulma ve düzenleme konusunda kolay bir yol sunar:</span><span class="sxs-lookup"><span data-stu-id="a9168-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="a9168-115">Nerdakşam yemeği, kayıtlı kullanıcıların dinlayıcıları oluşturmalarına, düzenlemesine ve silmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9168-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="a9168-116">Uygulama genelinde tutarlı bir doğrulama ve iş kuralları kümesi uygular:</span><span class="sxs-lookup"><span data-stu-id="a9168-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="a9168-117">Ziyaretçiler, yaklaşan ön anlar için arama yapmak üzere AJAX tabanlı bir eşleme kullanabilir:</span><span class="sxs-lookup"><span data-stu-id="a9168-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="a9168-118">Bir akşam yemeği 'ya tıkladığınızda, bu kişiler hakkında daha fazla bilgi sağlayabilecekleri bir ayrıntı sayfasına götürür:</span><span class="sxs-lookup"><span data-stu-id="a9168-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="a9168-119">Dinner 'e katılmakla ilgileniyorsanız, sitede oturum açabilir veya kaydolarlar:</span><span class="sxs-lookup"><span data-stu-id="a9168-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="a9168-120">Daha sonra olaya katılmak için AJAX tabanlı bir RSVP bağlantısına tıklabilirler:</span><span class="sxs-lookup"><span data-stu-id="a9168-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="a9168-121">Nerdakşam yemeği uygulama</span><span class="sxs-lookup"><span data-stu-id="a9168-121">Implementing NerdDinner</span></span>

<span data-ttu-id="a9168-122">Yeni bir ASP.NET MVC projesi oluşturmak için Visual Studio içindeki File-&gt;New Project komutunu kullanarak Nerdakşam yemeği uygulamamıza başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="a9168-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="a9168-123">Daha sonra özellik ve özellik artımlı olarak ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="a9168-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="a9168-124">Şu şekilde ele alacağız:</span><span class="sxs-lookup"><span data-stu-id="a9168-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="a9168-125">Yeni bir ASP.NET MVC projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9168-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="a9168-126">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9168-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="a9168-127">İş kuralı doğrulamaları ile model oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9168-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="a9168-128">Bir listeleme/Ayrıntılar Kullanıcı arabirimi uygulamak için denetleyicileri ve görünümleri kullanma</span><span class="sxs-lookup"><span data-stu-id="a9168-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="a9168-129">CRUD (oluşturma, okuma, güncelleştirme, silme) veri formu girişi desteği sağlama</span><span class="sxs-lookup"><span data-stu-id="a9168-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="a9168-130">ViewData kullanma ve ViewModel sınıfları uygulama</span><span class="sxs-lookup"><span data-stu-id="a9168-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="a9168-131">Ana sayfaları ve partileri kullanarak Kullanıcı arabirimini yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="a9168-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="a9168-132">Verimli veri sayfalamayı uygulama</span><span class="sxs-lookup"><span data-stu-id="a9168-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="a9168-133">Kimlik doğrulama ve yetkilendirme kullanarak uygulamaları güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="a9168-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="a9168-134">Dinamik güncelleştirmeleri sunmak için AJAX kullanma</span><span class="sxs-lookup"><span data-stu-id="a9168-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="a9168-135">Eşleme senaryolarını uygulamak için AJAX kullanma</span><span class="sxs-lookup"><span data-stu-id="a9168-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="a9168-136">Otomatik birim testini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a9168-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="a9168-137">Bu bölümde anlatıyoruz her adımı tamamlayarak Nerdakşam yemeği 'nin kendi kopyasını sıfırdan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9168-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="a9168-138">Alternatif olarak, kaynak kodun tamamlanmış bir sürümünü buradan indirebilirsiniz: [GitHub 'Da Nerdakşam yemeği](https://github.com/AspNetMVPSamples/NerdDinner).</span><span class="sxs-lookup"><span data-stu-id="a9168-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="a9168-139">Ayrıca, öğreticiyi çevrimdışı olarak okumak istiyorsanız [Bu öğreticinin ÜCRETSIZ PDF sürümünü de indirebilirsiniz](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) .</span><span class="sxs-lookup"><span data-stu-id="a9168-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="a9168-140">Uygulamayı derlemek için Visual Studio 2008 veya ücretsiz Visual Web Developer 2008 Express kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9168-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="a9168-141">Veritabanı için SQL Server ya da ücretsiz SQL Server Express kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9168-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="a9168-142">ASP.NET MVC, Visual Web Developer 2008 Express ve SQL Server Express (tümü ücretsiz) sürümünü kullanarak [Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx) v2 yükleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a9168-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="a9168-143">Şimdi başlayalım....</span><span class="sxs-lookup"><span data-stu-id="a9168-143">Now let's get started....</span></span>

<span data-ttu-id="a9168-144">Nerdakşam yemeği 'nin ne olduğunu eklediğimiz için, sıvayıp sitemizi oluşturalım ve kod yazalım.</span><span class="sxs-lookup"><span data-stu-id="a9168-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="a9168-145">Nerdakşam yemeği uygulamasını oluşturmak için Visual Studio içinde dosya&gt;yeni proje 'yi kullanarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="a9168-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a9168-146">Next</span><span class="sxs-lookup"><span data-stu-id="a9168-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
