---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 'Bölüm 7: Üyelik ve yetkilendirme | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisinde ASP.NET MVC müzik Store örnek uygulamayı oluşturmak için gerçekleştirilen tüm adımları ayrıntılı olarak açıklanmaktadır. 7. bölüm, üyelik ve yetkilendirme kapsar.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: 44205f0ef59e00ad9fb1c45fdc0ba8934b5804cc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076791"
---
<a name="part-7-membership-and-authorization"></a><span data-ttu-id="d6d2a-104">Bölüm 7: Üyelik ve Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="d6d2a-104">Part 7: Membership and Authorization</span></span>
====================
<span data-ttu-id="d6d2a-105">tarafından [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="d6d2a-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="d6d2a-106">MVC müzik Store tanıtır ve ASP.NET MVC ve Visual Studio web geliştirme için nasıl kullanılacağını adım adım anlatan bir öğretici uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="d6d2a-107">MVC müzik Store müzik albümleri çevrimiçi sattığı ve temel site yönetimi, kullanıcı oturum açma ve alışveriş sepeti işlevselliğini uygulayan bir Basit örnek deposu uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="d6d2a-108">Bu öğretici serisinde ASP.NET MVC müzik Store örnek uygulamayı oluşturmak için gerçekleştirilen tüm adımları ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="d6d2a-109">7. bölüm, üyelik ve yetkilendirme kapsar.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-109">Part 7 covers Membership and Authorization.</span></span>


<span data-ttu-id="d6d2a-110">Store Yöneticisi denetleyicimizin sitemizi ziyaret eden herkes için şu anda erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="d6d2a-111">Bu site yöneticileri erişimi kısıtlamak için değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="d6d2a-112">AccountController ve görünümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d6d2a-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="d6d2a-113">ASP.NET MVC 3 boş Web uygulaması şablonu tam ASP.NET MVC 3, Web uygulaması şablonu arasındaki tek fark, boş şablonu bir hesap denetleyicisi içermez ' dir.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="d6d2a-114">Tam bir ASP.NET MVC 3, Web uygulaması şablondan oluşturulan yeni bir ASP.NET MVC uygulamasında birkaç dosya kopyalayarak bir hesap denetleyicisi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="d6d2a-115">Tam ASP.NET MVC 3, Web uygulaması şablonunu kullanarak yeni bir ASP.NET MVC uygulaması oluşturun ve aynı dizinlerde Projemizin aşağıdaki dosyaları kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="d6d2a-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="d6d2a-116">AccountController.cs denetleyicileri dizine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="d6d2a-117">AccountModels modelleri dizine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="d6d2a-118">Görünümler dizini içinde bir hesap dizin oluşturma ve dört tüm görünümlerde kopyalayın</span><span class="sxs-lookup"><span data-stu-id="d6d2a-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="d6d2a-119">Bunlar MvcMusicStore ile başlar bu nedenle denetleyici ve Model sınıfları için ad alanı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="d6d2a-120">AccountController sınıfı MvcMusicStore.Controllers ad uzayını kullanmalı ve AccountModels sınıfı MvcMusicStore.Models ad uzayını kullanmalı.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="d6d2a-121">*Not: Bu dosyalar, biz öğreticinin başında bizim site tasarımı dosyaları kopyalanan MvcMusicStore Assets.zip indirme mevcuttur. Üyelik dosyaları kod dizininde bulunur.*</span><span class="sxs-lookup"><span data-stu-id="d6d2a-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="d6d2a-122">Güncel çözümü aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d6d2a-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="d6d2a-123">ASP.NET yapılandırma sitesi olan bir yönetici kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="d6d2a-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="d6d2a-124">Yetkilendirme Web sitemizi kılarız önce biz erişimi olan bir kullanıcı oluşturma gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="d6d2a-125">Bir kullanıcı oluşturmak için en kolay yolu, yerleşik ASP.NET yapılandırma Web sitesini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="d6d2a-126">ASP.NET yapılandırması Web sitesi, Çözüm Gezgini'nde simgesini izleyen'ı tıklatarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="d6d2a-127">Bu, bir yapılandırma Web sitesini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-127">This launches a configuration website.</span></span> <span data-ttu-id="d6d2a-128">Ana Ekran Güvenlik sekmesine tıklayın ve ardından ekranın ortasında "rollerini etkinleştir" bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="d6d2a-129">"Rolleri oluşturma ve yönetme" bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="d6d2a-130">Rol adı olarak "Yönetici" girin ve Rol Ekle düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="d6d2a-131">Geri düğmesine tıklayın ve ardından sol taraftaki oluşturma kullanıcı bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="d6d2a-132">Aşağıdaki bilgileri kullanarak soldaki kullanıcı bilgileri alanları doldurun:</span><span class="sxs-lookup"><span data-stu-id="d6d2a-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="d6d2a-133">**Alan**</span><span class="sxs-lookup"><span data-stu-id="d6d2a-133">**Field**</span></span> | <span data-ttu-id="d6d2a-134">**Değer**</span><span class="sxs-lookup"><span data-stu-id="d6d2a-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="d6d2a-135">**Kullanıcı adı**</span><span class="sxs-lookup"><span data-stu-id="d6d2a-135">**User Name**</span></span> | <span data-ttu-id="d6d2a-136">Yönetici</span><span class="sxs-lookup"><span data-stu-id="d6d2a-136">Administrator</span></span> |
| <span data-ttu-id="d6d2a-137">**Parola**</span><span class="sxs-lookup"><span data-stu-id="d6d2a-137">**Password**</span></span> | <span data-ttu-id="d6d2a-138">/ password123!</span><span class="sxs-lookup"><span data-stu-id="d6d2a-138">password123!</span></span> |
| <span data-ttu-id="d6d2a-139">**Parolayı onaylayın**</span><span class="sxs-lookup"><span data-stu-id="d6d2a-139">**Confirm Password**</span></span> | <span data-ttu-id="d6d2a-140">/ password123!</span><span class="sxs-lookup"><span data-stu-id="d6d2a-140">password123!</span></span> |
| <span data-ttu-id="d6d2a-141">**E-posta**</span><span class="sxs-lookup"><span data-stu-id="d6d2a-141">**E-mail**</span></span> | <span data-ttu-id="d6d2a-142">(herhangi bir e-posta adresi çalışır)</span><span class="sxs-lookup"><span data-stu-id="d6d2a-142">(any email address will work)</span></span> |
| <span data-ttu-id="d6d2a-143">**Güvenlik sorusu**</span><span class="sxs-lookup"><span data-stu-id="d6d2a-143">**Security Question**</span></span> | <span data-ttu-id="d6d2a-144">(istediğiniz gibi)</span><span class="sxs-lookup"><span data-stu-id="d6d2a-144">(whatever you like)</span></span> |
| <span data-ttu-id="d6d2a-145">**Güvenlik yanıtı**</span><span class="sxs-lookup"><span data-stu-id="d6d2a-145">**Security Answer**</span></span> | <span data-ttu-id="d6d2a-146">(istediğiniz gibi)</span><span class="sxs-lookup"><span data-stu-id="d6d2a-146">(whatever you like)</span></span> |

<span data-ttu-id="d6d2a-147">*Not: Elbette, istediğiniz herhangi bir parola da kullanabilirsiniz. Varsayılan parola güvenlik ayarlarını 7 karakterden daha uzun ve bir tane alfasayısal olmayan karakter içeren bir parola gerektirir.*</span><span class="sxs-lookup"><span data-stu-id="d6d2a-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="d6d2a-148">Bu kullanıcı için Yönetici rolü seçin ve kullanıcı Oluştur düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="d6d2a-149">Bu noktada, kullanıcının başarıyla oluşturulduğunu belirten bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="d6d2a-150">Artık tarayıcı penceresini kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="d6d2a-151">Rol tabanlı yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="d6d2a-151">Role-based Authorization</span></span>

<span data-ttu-id="d6d2a-152">Şimdi biz sınıftaki herhangi bir denetleyici eylemi erişmek için yönetici rolündeki kullanıcı olmalıdır belirtme [Authorize] özniteliği kullanılarak StoreManagerController erişimi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="d6d2a-153">*Not: Hem denetleyici sınıf düzeyinde hem de özel eylem yöntemleri [Authorize] özniteliği yerleştirilebilir.*</span><span class="sxs-lookup"><span data-stu-id="d6d2a-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="d6d2a-154">Artık /StoreManager için gözatma, bir oturum açma iletişim kutusunu açar:</span><span class="sxs-lookup"><span data-stu-id="d6d2a-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="d6d2a-155">Sunduğumuz yeni bir yönetici hesabıyla oturum açtıktan sonra önce albümü düzenle ekranı Git sunabiliyoruz.</span><span class="sxs-lookup"><span data-stu-id="d6d2a-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d6d2a-156">[Önceki](mvc-music-store-part-6.md)
> [İleri](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="d6d2a-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
