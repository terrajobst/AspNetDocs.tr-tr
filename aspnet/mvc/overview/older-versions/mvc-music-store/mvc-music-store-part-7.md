---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: '7\. Bölüm: Üyelik ve yetkilendirme | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 7 ' de üyelik ve yetkilendirme ele alınmaktadır.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539202"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="38e21-104">7\. Bölüm: Üyelik ve Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="38e21-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="38e21-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="38e21-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="38e21-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="38e21-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="38e21-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="38e21-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="38e21-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="38e21-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="38e21-109">Bölüm 7 ' de üyelik ve yetkilendirme ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="38e21-109">Part 7 covers Membership and Authorization.</span></span>

<span data-ttu-id="38e21-110">Depolama Yöneticisi denetleyicimiz Şu anda sitemizi ziyaret eden herkes tarafından erişilebilir durumda.</span><span class="sxs-lookup"><span data-stu-id="38e21-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="38e21-111">Site yöneticileri iznini kısıtlamak için bunu değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="38e21-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="38e21-112">AccountController ve görünümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="38e21-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="38e21-113">Tam ASP.NET MVC 3 Web uygulaması şablonu ve ASP.NET MVC 3 boş Web uygulaması şablonu arasındaki bir fark, boş şablonun bir hesap denetleyicisi içermediğinden emin değildir.</span><span class="sxs-lookup"><span data-stu-id="38e21-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="38e21-114">Tam ASP.NET MVC 3 Web uygulaması şablonundan oluşturulan yeni bir ASP.NET MVC uygulamasından birkaç dosya kopyalayarak bir hesap denetleyicisi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="38e21-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="38e21-115">Full ASP.NET MVC 3 Web uygulaması şablonunu kullanarak yeni bir ASP.NET MVC uygulaması oluşturun ve aşağıdaki dosyaları projemizdeki dizinlere kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="38e21-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="38e21-116">AccountController.cs 'i denetleyiciler dizininde Kopyala</span><span class="sxs-lookup"><span data-stu-id="38e21-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="38e21-117">Accountmodellerini modeller dizininde kopyalama</span><span class="sxs-lookup"><span data-stu-id="38e21-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="38e21-118">Görünümler dizini içinde bir hesap dizini oluşturun ve tüm dört görünümü ' de kopyalayın</span><span class="sxs-lookup"><span data-stu-id="38e21-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="38e21-119">Denetleyici ve model sınıflarının ad alanını MvcMusicStore ile başlayacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="38e21-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="38e21-120">AccountController sınıfı, MvcMusicStore. Controllers ad alanını kullanmalı ve Accountmodeller sınıfı MvcMusicStore. model ad alanını kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="38e21-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="38e21-121">*Note: Bu dosyalar, öğreticinin başlangıcında site tasarım dosyalarımı kopyaladığımız MvcMusicStore-Assets. zip indirimde da mevcuttur. Üyelik dosyaları kod dizininde bulunur.*</span><span class="sxs-lookup"><span data-stu-id="38e21-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="38e21-122">Güncelleştirilmiş çözüm aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="38e21-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="38e21-123">ASP.NET yapılandırma sitesiyle Yönetici Kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="38e21-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="38e21-124">Web sitemizden yetkilendirme gerektirmeden önce, erişimi olan bir kullanıcı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="38e21-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="38e21-125">Bir kullanıcı oluşturmanın en kolay yolu yerleşik ASP.NET yapılandırması Web sitesini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="38e21-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="38e21-126">Çözüm Gezgini simgesini izleyerek ASP.NET Configuration Web sitesini başlatın.</span><span class="sxs-lookup"><span data-stu-id="38e21-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="38e21-127">Bu, bir yapılandırma Web sitesi başlatır.</span><span class="sxs-lookup"><span data-stu-id="38e21-127">This launches a configuration website.</span></span> <span data-ttu-id="38e21-128">Giriş ekranındaki Güvenlik sekmesine tıklayın ve ardından ekranın ortasında "rolleri etkinleştir" bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38e21-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="38e21-129">"Rol oluşturma veya yönetme" bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38e21-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="38e21-130">Rol adı olarak "Yönetici" yazın ve rol Ekle düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="38e21-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="38e21-131">Geri düğmesine tıklayın ve ardından sol taraftaki kullanıcı oluştur bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38e21-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="38e21-132">Aşağıdaki bilgileri kullanarak sol taraftaki Kullanıcı bilgileri alanlarını girin:</span><span class="sxs-lookup"><span data-stu-id="38e21-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="38e21-133">**Alan**</span><span class="sxs-lookup"><span data-stu-id="38e21-133">**Field**</span></span> | <span data-ttu-id="38e21-134">**Değer**</span><span class="sxs-lookup"><span data-stu-id="38e21-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="38e21-135">**Kullanıcı adı**</span><span class="sxs-lookup"><span data-stu-id="38e21-135">**User Name**</span></span> | <span data-ttu-id="38e21-136">Yönetici</span><span class="sxs-lookup"><span data-stu-id="38e21-136">Administrator</span></span> |
| <span data-ttu-id="38e21-137">**Parola**</span><span class="sxs-lookup"><span data-stu-id="38e21-137">**Password**</span></span> | <span data-ttu-id="38e21-138">password123!</span><span class="sxs-lookup"><span data-stu-id="38e21-138">password123!</span></span> |
| <span data-ttu-id="38e21-139">**Parolayı Onayla**</span><span class="sxs-lookup"><span data-stu-id="38e21-139">**Confirm Password**</span></span> | <span data-ttu-id="38e21-140">password123!</span><span class="sxs-lookup"><span data-stu-id="38e21-140">password123!</span></span> |
| <span data-ttu-id="38e21-141">**Postadaki**</span><span class="sxs-lookup"><span data-stu-id="38e21-141">**E-mail**</span></span> | <span data-ttu-id="38e21-142">(herhangi bir e-posta adresi çalışacaktır)</span><span class="sxs-lookup"><span data-stu-id="38e21-142">(any email address will work)</span></span> |
| <span data-ttu-id="38e21-143">**Güvenlik sorusu**</span><span class="sxs-lookup"><span data-stu-id="38e21-143">**Security Question**</span></span> | <span data-ttu-id="38e21-144">(beğendiğiniz şey)</span><span class="sxs-lookup"><span data-stu-id="38e21-144">(whatever you like)</span></span> |
| <span data-ttu-id="38e21-145">**Güvenlik yanıtı**</span><span class="sxs-lookup"><span data-stu-id="38e21-145">**Security Answer**</span></span> | <span data-ttu-id="38e21-146">(beğendiğiniz şey)</span><span class="sxs-lookup"><span data-stu-id="38e21-146">(whatever you like)</span></span> |

<span data-ttu-id="38e21-147">*Note: Elbette istediğiniz parolayı kullanabilirsiniz. Varsayılan parola güvenlik ayarları 7 karakter uzunluğunda ve alfasayısal olmayan bir karakter içeren bir parola gerektirir.*</span><span class="sxs-lookup"><span data-stu-id="38e21-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="38e21-148">Bu Kullanıcı için yönetici rolünü seçin ve Kullanıcı Oluştur düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38e21-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="38e21-149">Bu noktada, kullanıcının başarıyla oluşturulduğunu belirten bir ileti görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="38e21-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="38e21-150">Artık tarayıcı penceresini kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38e21-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="38e21-151">Rol tabanlı yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="38e21-151">Role-based Authorization</span></span>

<span data-ttu-id="38e21-152">Artık, [Yetkilendir] özniteliğini kullanarak StoreManagerController erişimini kısıtlayabiliriz. Bu, kullanıcının sınıftaki herhangi bir denetleyiciye erişmek için yönetici rolünde olması gerektiğini belirten bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="38e21-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="38e21-153">*Note: [Yetkilendir] özniteliği belirli eylem yöntemlerine ve denetleyici sınıf düzeyinde yer alabilir.*</span><span class="sxs-lookup"><span data-stu-id="38e21-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="38e21-154">Şimdi/StoreManager 'a göz atma bir oturum açma iletişim kutusunu açar:</span><span class="sxs-lookup"><span data-stu-id="38e21-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="38e21-155">Yeni yönetici hesabımızda oturum açtıktan sonra, albüm düzenleme ekranına daha önce olduğu gibi gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38e21-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="38e21-156">[Önceki](mvc-music-store-part-6.md)
> [İleri](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="38e21-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
