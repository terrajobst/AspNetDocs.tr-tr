---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner Öğreticisine giriş | Microsoft Docs
author: shanselman
description: Yeni bir çerçeve öğrenmenin en iyi yolu olan bir şey oluşturmaktır. Bu öğreticide ASP.NE kullanarak küçük ancak tam bir uygulama oluşturma hakkında bilgi vermektedir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: ebd49295ea165ba4ef1a25398cff7dddcfa54f11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392202"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="17ffd-104">NerdDinner Öğreticisine Giriş</span><span class="sxs-lookup"><span data-stu-id="17ffd-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="17ffd-105">tarafından [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="17ffd-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="17ffd-106">PDF'yi indirin</span><span class="sxs-lookup"><span data-stu-id="17ffd-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="17ffd-107">Yeni bir çerçeve öğrenmenin en iyi yolu olan bir şey oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="17ffd-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="17ffd-108">Bu öğretici, küçük bir derleme, ancak tamamlamak, ASP.NET MVC 1'i kullanarak uygulama hakkında bilgi vermektedir ve bazı ardındaki temel kavramları tanıtır.</span><span class="sxs-lookup"><span data-stu-id="17ffd-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="17ffd-109">ASP.NET MVC 3 kullanıyorsanız, takip ettiğiniz öneririz [MVC 3 ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticiler.</span><span class="sxs-lookup"><span data-stu-id="17ffd-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-tutorial"></a><span data-ttu-id="17ffd-110">NerdDinner Öğreticisine</span><span class="sxs-lookup"><span data-stu-id="17ffd-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="17ffd-111">Yeni bir çerçeve öğrenmenin en iyi yolu olan bir şey oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="17ffd-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="17ffd-112">Bu öğretici, küçük bir derleme, ancak tamamlamak, ASP.NET MVC kullanarak uygulama hakkında bilgi vermektedir ve bazı ardındaki temel kavramları tanıtır.</span><span class="sxs-lookup"><span data-stu-id="17ffd-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="17ffd-113">Uygulama oluşturmak için kullanacağız "NerdDinner" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="17ffd-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="17ffd-114">NerdDinner çevrimiçi azalma bulun ve bu kişiler için kolay bir yol sağlar:</span><span class="sxs-lookup"><span data-stu-id="17ffd-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="17ffd-115">NerdDinner kayıtlı kullanıcıların oluşturma, düzenleme ve silme azalma sağlar.</span><span class="sxs-lookup"><span data-stu-id="17ffd-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="17ffd-116">Uygulamanın tamamında tutarlı özellik kümesi doğrulama ve iş kuralları zorunlu kılar:</span><span class="sxs-lookup"><span data-stu-id="17ffd-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="17ffd-117">Ziyaretçiler, bunları tutulmakta yaklaşan azalma aramak için bir AJAX tabanlı eşleme kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17ffd-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="17ffd-118">Bir Akşam Yemeği tıklayarak bunları ayrıntıları sayfasına nereden öğrenebilir hakkında daha fazla sürer:</span><span class="sxs-lookup"><span data-stu-id="17ffd-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="17ffd-119">Bunlar dinner katılan içinde ilgileniyorsanız oturum açma veya sitesine kaydolun:</span><span class="sxs-lookup"><span data-stu-id="17ffd-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="17ffd-120">Bunlar, ardından etkinliğine katılın için bir AJAX tabanlı RSVP bağlantısına tıklayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17ffd-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="17ffd-121">NerdDinner uygulama</span><span class="sxs-lookup"><span data-stu-id="17ffd-121">Implementing NerdDinner</span></span>

<span data-ttu-id="17ffd-122">Dosya - kullanarak NerdDinner uygulamamız başlamak kullanacağız&gt;yepyeni bir ASP.NET MVC projesi oluşturmak için Visual Studio'da yeni proje komutu.</span><span class="sxs-lookup"><span data-stu-id="17ffd-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="17ffd-123">Ardından artımlı olarak işlevleri ve özellikleri ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="17ffd-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="17ffd-124">Süreç boyunca şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="17ffd-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="17ffd-125">Yeni bir ASP.NET MVC projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="17ffd-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="17ffd-126">Bir veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="17ffd-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="17ffd-127">Nasıl iş kuralı doğrulamaları ile model oluşturma</span><span class="sxs-lookup"><span data-stu-id="17ffd-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="17ffd-128">Denetleyicileri ve görünümleri listeleme/Ayrıntılar kullanıcı Arabirimi uygulamak için kullanma</span><span class="sxs-lookup"><span data-stu-id="17ffd-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="17ffd-129">Nasıl CRUD (oluşturma, okuma, güncelleştirme ve silme) veri formu giriş desteği</span><span class="sxs-lookup"><span data-stu-id="17ffd-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="17ffd-130">ViewData kullanma ve ViewModel sınıfları uygulama</span><span class="sxs-lookup"><span data-stu-id="17ffd-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="17ffd-131">Ana sayfaları ve kısmi bölümleri kullanarak kullanıcı arabirimini yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="17ffd-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="17ffd-132">Verimli veri sayfalama uygulama</span><span class="sxs-lookup"><span data-stu-id="17ffd-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="17ffd-133">Kimlik doğrulama ve yetkilendirme kullanarak uygulamaların güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="17ffd-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="17ffd-134">AJAX dinamik güncelleştirmeler sunma konusunda</span><span class="sxs-lookup"><span data-stu-id="17ffd-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="17ffd-135">AJAX kullanarak eşleme senaryoları gerçekleştirmeyi öğrenin</span><span class="sxs-lookup"><span data-stu-id="17ffd-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="17ffd-136">Otomatik birim testi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="17ffd-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="17ffd-137">NerdDinner kopyasına oluşturabileceğinizi her tamamlayarak sıfırdan adım Biz bu bölümdeki gözden geçirme.</span><span class="sxs-lookup"><span data-stu-id="17ffd-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="17ffd-138">Alternatif olarak, kaynak kodu buraya tamamlanmış bir sürümünü indirebilirsiniz: [GitHub üzerinde NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner).</span><span class="sxs-lookup"><span data-stu-id="17ffd-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="17ffd-139">Ayrıca isteğe bağlı olarak ayrıca [Bu öğretici ücretsiz bir PDF sürümünü indirin](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) öğretici çevrimdışı okumak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="17ffd-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="17ffd-140">Uygulamayı oluşturmak için Visual Studio 2008 ya da ücretsiz Visual Web Developer 2008 Express kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17ffd-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="17ffd-141">Veritabanı için SQL Server veya ücretsiz SQL Server Express kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17ffd-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="17ffd-142">ASP.NET MVC, Visual Web Developer 2008 Express ve SQL Server'ın V2 kullanarak Express (tüm ücretsiz) yükleyebilirsiniz [Microsoft Web Platformu yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="17ffd-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="17ffd-143">Şimdi başlayalım...</span><span class="sxs-lookup"><span data-stu-id="17ffd-143">Now let's get started....</span></span>

<span data-ttu-id="17ffd-144">NerdDinner nedir ele aldığımız, şimdi bizim kollarınızı sıvayın ve biraz kod yazalım.</span><span class="sxs-lookup"><span data-stu-id="17ffd-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="17ffd-145">Şu dosya - kullanarak başlarsınız&gt;NerdDinner uygulama oluşturmak için Visual Studio'da yeni proje.</span><span class="sxs-lookup"><span data-stu-id="17ffd-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="17ffd-146">Next</span><span class="sxs-lookup"><span data-stu-id="17ffd-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
