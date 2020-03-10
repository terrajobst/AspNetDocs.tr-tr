---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: Bir ASP.NET Web Pages (Razor) sitesinde yardımcı yükleme | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde yardımcı 'nın nasıl yükleneceği açıklanır. Yardımcı, başına kod ve biçimlendirme içeren yeniden kullanılabilir bir bileşendir...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638588"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="e7416-104">Bir ASP.NET Web Pages (Razor) sitesinde yardımcı yükleme</span><span class="sxs-lookup"><span data-stu-id="e7416-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="e7416-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="e7416-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e7416-106">Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde yardımcı 'nın nasıl yükleneceği açıklanır.</span><span class="sxs-lookup"><span data-stu-id="e7416-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="e7416-107">*Yardımcı* , sıkıcı veya karmaşık olabilecek bir görevi gerçekleştirmek için kod ve biçimlendirme içeren yeniden kullanılabilir bir bileşendir.</span><span class="sxs-lookup"><span data-stu-id="e7416-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="e7416-108">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="e7416-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="e7416-109">WebMatrix 3 kullanılarak oluşturulan bir Web sitesine yardımcı nasıl yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e7416-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e7416-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="e7416-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e7416-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="e7416-111">WebMatrix 3</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="e7416-112">Yardımcıların Özeti</span><span class="sxs-lookup"><span data-stu-id="e7416-112">Overview of Helpers</span></span>

<span data-ttu-id="e7416-113">Kullanıcıların genellikle Web sayfalarında yapmak istedikleri bazı görevler çok fazla kod gerektirir veya ek bilgi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e7416-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="e7416-114">Veriler için bir grafik görüntülemeyi örnek olarak içerir. sayfaya Twitter "Izle" düğmesi koyma; Web siteinizden e-posta gönderme; görüntüleri kırpma veya yeniden boyutlandırma; siteniz için PayPal 'yi kullanma.</span><span class="sxs-lookup"><span data-stu-id="e7416-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="e7416-115">Bu tür şeyleri daha kolay hale getirmek için ASP.NET Web sayfaları, *yardımcıları*kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7416-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="e7416-116">Yardımcılar, bir site için yüklediğiniz ve yalnızca bir satır veya iki Razor kodu kullanarak tipik görevleri gerçekleştirmenize olanak sağlayan bileşenlerdir.</span><span class="sxs-lookup"><span data-stu-id="e7416-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="e7416-117">ASP.NET Web sayfalarının içinde yerleşik olarak bulunan birkaç yardımcıları vardır.</span><span class="sxs-lookup"><span data-stu-id="e7416-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="e7416-118">Ancak, NuGet Paket Yöneticisi kullanılarak sağlanan paketlerde (eklentiler) birçok yardımcı vardır.</span><span class="sxs-lookup"><span data-stu-id="e7416-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="e7416-119">NuGet, yüklenecek bir paket seçmenizi sağlar ve yükleme ayrıntılarının tamamını ele alır.</span><span class="sxs-lookup"><span data-stu-id="e7416-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="e7416-120">WebMatrix 3 ' te yardımcı yükleme</span><span class="sxs-lookup"><span data-stu-id="e7416-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="e7416-121">WebMatrix 3 ' te **NuGet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7416-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![WebMatrix 'te NuGet Galerisi iletişim kutusu](installing-helpers/_static/image1.png)
2. <span data-ttu-id="e7416-123">Bu, NuGet paket yöneticisini başlatır ve kullanılabilir paketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e7416-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="e7416-124">Arama kutusuna, yüklemek istediğiniz yardımcı için bir anahtar sözcük girin.</span><span class="sxs-lookup"><span data-stu-id="e7416-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![WebMatrix 'te NuGet Galerisi iletişim kutusu](installing-helpers/_static/image2.png)
3. <span data-ttu-id="e7416-126">Paketi seçin ve ardından **yükler**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7416-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="e7416-127">Paketi yüklemek isteyip istemediğiniz sorulduğunda **Evet** ' e tıklayın ve koşulları kabul etmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e7416-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="e7416-128">İlk kez bir yardımcı yüklüyorsanız NuGet, yardımcı 'yı oluşturan kod için Web sitenizde klasörler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e7416-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="e7416-129">Bir yardımcıyı kaldırmak için, **Galeri** düğmesine tıklayın, **yüklü** sekmesine tıklayın ve kaldırmak istediğiniz paketi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7416-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="e7416-130">Twitter yardımcısını yükleme</span><span class="sxs-lookup"><span data-stu-id="e7416-130">Installing the Twitter helper</span></span>

<span data-ttu-id="e7416-131">Twitter API 'sinin en son sürümü, NuGet aracılığıyla yüklediğiniz Twitter Yardımcısı ile uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="e7416-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="e7416-132">Bunun yerine, projenizde Twitter yardımcısını ayarlama hakkında bilgi edinmek için [WebMatrix Ile Twitter Yardımcısı](twitter-helper.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="e7416-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="e7416-133">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e7416-133">Additional Resources</span></span>

[<span data-ttu-id="e7416-134">ASP.NET Web sayfalarına giriş 2-Programlama Temelleri</span><span class="sxs-lookup"><span data-stu-id="e7416-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="e7416-135">WebMatrix ile Twitter Yardımcısı</span><span class="sxs-lookup"><span data-stu-id="e7416-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
