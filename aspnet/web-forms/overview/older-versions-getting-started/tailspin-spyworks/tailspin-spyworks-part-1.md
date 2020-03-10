---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: '1\. kısım: Dosya-> Yeni proje | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 1\. bölüm, genel bakış ve dosya/yeni proje içerir.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636131"
---
# <a name="part-1-file--new-project"></a><span data-ttu-id="28225-104">1\. Bölüm: Dosya -> Yeni Proje</span><span class="sxs-lookup"><span data-stu-id="28225-104">Part 1: File-> New Project</span></span>

<span data-ttu-id="28225-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="28225-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="28225-106">Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="28225-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="28225-107">Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="28225-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="28225-108">Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="28225-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="28225-109">1\. bölüm, genel bakış ve dosya/yeni proje içerir.</span><span class="sxs-lookup"><span data-stu-id="28225-109">Part 1 covers Overview and File/New Project.</span></span>

## <a id="_Toc260221666"></a><span data-ttu-id="28225-110">Bakýþ</span><span class="sxs-lookup"><span data-stu-id="28225-110">Overview</span></span>

<span data-ttu-id="28225-111">Bu öğretici, ASP.NET WebForms 'e giriş niteliğindedir.</span><span class="sxs-lookup"><span data-stu-id="28225-111">This tutorial is an introduction to ASP.NET WebForms.</span></span> <span data-ttu-id="28225-112">Yavaş başlayacağız, bu nedenle başlangıç düzeyi Web geliştirme deneyimi sorunsuz.</span><span class="sxs-lookup"><span data-stu-id="28225-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="28225-113">Oluşturmakta olduğumuz uygulama basit bir çevrimiçi depodır.</span><span class="sxs-lookup"><span data-stu-id="28225-113">The application we'll be building is a simple on-line store.</span></span>

![](tailspin-spyworks-part-1/_static/image1.jpg)

<span data-ttu-id="28225-114">Ziyaretçiler ürüne kategoriye göre gözatabilirler:</span><span class="sxs-lookup"><span data-stu-id="28225-114">Visitors can browse Products by Category:</span></span>

![](tailspin-spyworks-part-1/_static/image2.jpg)

<span data-ttu-id="28225-115">Tek bir ürünü görüntüleyebilir ve bu uygulamayı sepetlerinden ekleyebilirler:</span><span class="sxs-lookup"><span data-stu-id="28225-115">They can view a single product and add it to their cart:</span></span>

![](tailspin-spyworks-part-1/_static/image3.jpg)

<span data-ttu-id="28225-116">Sepetlerinde, artık istedikleri öğeleri kaldırarak kendi sepetini gözden geçirebilir:</span><span class="sxs-lookup"><span data-stu-id="28225-116">They can review their cart, removing any items they no longer want:</span></span>

![](tailspin-spyworks-part-1/_static/image4.jpg)

<span data-ttu-id="28225-117">Kullanıma almaya devam etmek, bunları şunları isteyecek</span><span class="sxs-lookup"><span data-stu-id="28225-117">Proceeding to Checkout will prompt them to</span></span>

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

<span data-ttu-id="28225-118">Sipariş ettikten sonra basit bir onay ekranı görürler:</span><span class="sxs-lookup"><span data-stu-id="28225-118">After ordering, they see a simple confirmation screen:</span></span>

![](tailspin-spyworks-part-1/_static/image7.jpg)

<span data-ttu-id="28225-119">Visual Studio 2010 ' de yeni bir ASP.NET WebForms projesi oluşturarak başlayacağız ve tamamen çalışan bir uygulama oluşturmak için artımlı olarak Özellikler ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="28225-119">We'll begin by creating a new ASP.NET WebForms project in Visual Studio 2010, and we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="28225-120">Bu şekilde, veritabanı erişimi, liste ve kılavuz görünümlerini, veri güncelleştirme sayfalarını, veri doğrulamayı, tutarlı sayfa düzeni, AJAX, doğrulama, Kullanıcı üyeliği ve daha fazlasını kapsayan ana sayfaları kullanarak ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="28225-120">Along the way, we'll cover database access, list and grid views, data update pages, data validation, using master pages for consistent page layout, AJAX, validation, user membership, and more.</span></span>

<span data-ttu-id="28225-121">Adımları adım adım takip edebilir veya tamamlanmış uygulamayı [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/) adresinden indirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="28225-121">You can follow along step by step, or you can download the completed application from [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span></span>

<span data-ttu-id="28225-122">[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)'Den visual Studio 2010 veya ücretsiz Visual Web Developer 2010 ' i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28225-122">You can use either Visual Studio 2010 or the free Visual Web Developer 2010 from [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="28225-123">Uygulamayı derlemek için, veritabanını barındırmak üzere SQL Server veya ücretsiz SQL Server Express kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28225-123">To build the application, you can use either SQL Server or the free SQL Server Express to host the database.</span></span>

## <a id="_Toc260221667"></a><span data-ttu-id="28225-124">Dosya/yeni proje</span><span class="sxs-lookup"><span data-stu-id="28225-124">File / New Project</span></span>

<span data-ttu-id="28225-125">Visual Studio 'da Dosya menüsünden yeni projeyi seçerek başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="28225-125">We'll start by selecting the New Project from the File menu in Visual Studio.</span></span> <span data-ttu-id="28225-126">Bu, yeni proje iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="28225-126">This brings up the New Project dialog.</span></span>

![](tailspin-spyworks-part-1/_static/image8.jpg)

<span data-ttu-id="28225-127">Sol taraftaki görsel C# /Web şablonları grubunu seçeceğiz ve ardından Orta sütundaki "ASP.NET Web uygulaması" şablonunu seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="28225-127">We'll select the Visual C# / Web Templates group on the left, and then choose the "ASP.NET Web Application" template in the center column.</span></span> <span data-ttu-id="28225-128">Projenizi TailspinSpyworks olarak adlandırın ve Tamam düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="28225-128">Name your project TailspinSpyworks and press the OK button.</span></span>

![](tailspin-spyworks-part-1/_static/image9.jpg)

<span data-ttu-id="28225-129">Bu, projemizi oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="28225-129">This will create our project.</span></span> <span data-ttu-id="28225-130">Aşağıda, uygulamamızda bulunan klasörlere sağ taraftaki Çözüm Gezgini göz atalım.</span><span class="sxs-lookup"><span data-stu-id="28225-130">Let's take a look at the folders that are included in our application in the Solution Explorer on the right side.</span></span>

![](tailspin-spyworks-part-1/_static/image10.jpg)

<span data-ttu-id="28225-131">Boş çözüm tamamen boş değildir; temel bir klasör yapısı ekler:</span><span class="sxs-lookup"><span data-stu-id="28225-131">The Empty Solution isn't completely empty – it adds a basic folder structure:</span></span>

![](tailspin-spyworks-part-1/_static/image1.png)

<span data-ttu-id="28225-132">ASP.NET 4 varsayılan proje şablonu tarafından uygulanan kurallara göz önünde edin.</span><span class="sxs-lookup"><span data-stu-id="28225-132">Note the conventions implemented by the ASP.NET 4 default project template.</span></span>

- <span data-ttu-id="28225-133">"Account" klasörü ASP için temel bir kullanıcı arabirimi uygular. NET 'in üyelik alt sistemi.</span><span class="sxs-lookup"><span data-stu-id="28225-133">The "Account" folder implements a basic user interface for ASP.NET's membership subsystem.</span></span>
- <span data-ttu-id="28225-134">"Betikler" klasörü, istemci tarafı JavaScript dosyaları için depo görevi görür ve çekirdek jQuery. js dosyaları varsayılan olarak kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="28225-134">The "Scripts" folder serves as the repository for client side JavaScript files and the core jQuery .js files are made available by default.</span></span>
- <span data-ttu-id="28225-135">"Stiller" klasörü, Web sitesi görsellerimizi (CSS stil sayfaları) düzenlemek için kullanılır</span><span class="sxs-lookup"><span data-stu-id="28225-135">The "Styles" folder is used to organize our web site visuals (CSS Style Sheets)</span></span>

<span data-ttu-id="28225-136">Uygulamamızı çalıştırmak ve default. aspx sayfasını işlemek için F5 'e bastığımda, aşağıdakileri görtik.</span><span class="sxs-lookup"><span data-stu-id="28225-136">When we press F5 to run our application and render the default.aspx page we see the following.</span></span>

![](tailspin-spyworks-part-1/_static/image11.jpg)

<span data-ttu-id="28225-137">İlk uygulama geliştirmemiz, default WebForms şablonundaki Style. css dosyasını, Tailspin Spyworks uygulamamız için istediğimiz görsel güvenlerle birlikte işleyecek olan CSS sınıflarıyla ve ilişkili resim dosyalarıyla değiştirecek.</span><span class="sxs-lookup"><span data-stu-id="28225-137">Our first application enhancement will be to replace the Style.css file from the default WebForms template with the CSS classes and associated image files that will render the visual asthetics that we want for our Tailspin Spyworks application.</span></span>

<span data-ttu-id="28225-138">Bunu yaptıktan sonra default. aspx sayfamız bu şekilde işlenir.</span><span class="sxs-lookup"><span data-stu-id="28225-138">After doing so our default.aspx page renders like this.</span></span>

![](tailspin-spyworks-part-1/_static/image12.jpg)

<span data-ttu-id="28225-139">Sayfanın sağ üst kısmındaki görüntü bağlantılarına ve ana sayfaya eklenen menü öğelerine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="28225-139">Notice the image links at the top right of the page and the menu items that have been added to the master page.</span></span> <span data-ttu-id="28225-140">Yalnızca "oturum aç" ve "hesap" bağlantıları, var olan sayfalara (varsayılan şablon tarafından oluşturulan) ve uygulamamız oluşturduğumuzdan uyguladığımız sayfaların geri kalanına işaret eder.</span><span class="sxs-lookup"><span data-stu-id="28225-140">Only the "Sign In" and "Account" links point to pages that exist (generated by the default template) and the rest of the pages we will implement as we build our application.</span></span>

<span data-ttu-id="28225-141">Ana sayfayı stiller dizinine de konumlandırıyoruz.</span><span class="sxs-lookup"><span data-stu-id="28225-141">We're also going to relocate the Master Page to the Styles directory.</span></span> <span data-ttu-id="28225-142">Bu yalnızca bir tercih olsa da, uygulamamızı gelecekte "Skinable" olarak yapmaya karar verirse, bu işlemleri biraz daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="28225-142">Though this is only a preference it may make things a little easier if we decide to make our application "skinable" in the future.</span></span>

<span data-ttu-id="28225-143">Bunu yaptıktan sonra, varsayılan ASP.NET WebForms sayfaları tarafından oluşturulan tüm. aspx dosyalarındaki ana sayfa başvurularını değiştirmemiz gerekir.</span><span class="sxs-lookup"><span data-stu-id="28225-143">After doing this we'll need to change the master page references in all the .aspx files generated by the default ASP.NET WebForms pages.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="28225-144">Next</span><span class="sxs-lookup"><span data-stu-id="28225-144">Next</span></span>](tailspin-spyworks-part-2.md)
