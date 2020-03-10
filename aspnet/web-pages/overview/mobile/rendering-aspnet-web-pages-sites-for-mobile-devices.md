---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: Mobil cihazlar için ASP.NET Web Pages (Razor) sitelerini işleme | Microsoft Docs
author: Rick-Anderson
description: 'Bu makalede, mobil cihazlarda uygun şekilde işlenecek bir ASP.NET Web Pages (Razor) sitesinde sayfaların nasıl oluşturulacağı açıklanır. Ne öğreneceksiniz: nasıl yapılır...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563569"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="3050b-104">Mobil cihazlar için ASP.NET Web Pages (Razor) sitelerini işleme</span><span class="sxs-lookup"><span data-stu-id="3050b-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="3050b-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="3050b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3050b-106">Bu makalede, mobil cihazlarda uygun şekilde işlenecek bir ASP.NET Web Pages (Razor) sitesinde sayfaların nasıl oluşturulacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="3050b-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="3050b-107">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="3050b-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3050b-108">Bir sayfanın özellikle mobil cihazlarda tasarlanmasını belirtmek için adlandırma kuralı kullanma.</span><span class="sxs-lookup"><span data-stu-id="3050b-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3050b-109">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="3050b-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3050b-110">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="3050b-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="3050b-111">Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3050b-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="3050b-112">ASP.NET Web sayfaları, mobil veya diğer cihazlarda içerik işlemeye yönelik özel ekranlar oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3050b-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="3050b-113">Bir ASP.NET Web sayfaları sitesinde cihaza özgü sayfa oluşturmanın en kolay yolu, şöyle bir dosya adlandırma deseninin kullanılması: *filename. Mobile. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="3050b-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="3050b-114">Bir sayfanın iki sürümünü (örneğin, *Dosyam. cshtml* adlı bir tane ve *Dosyam. Mobile. cshtml*adlı bir tane) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3050b-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="3050b-115">Çalışma zamanında, bir mobil cihaz *Dosyam. cshtml*istediğinde, ASP.net *Dosyam. Mobile. cshtml*içindeki içeriği işler.</span><span class="sxs-lookup"><span data-stu-id="3050b-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="3050b-116">Aksi takdirde, *Dosyam. cshtml* işlenir.</span><span class="sxs-lookup"><span data-stu-id="3050b-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="3050b-117">Aşağıdaki örnekte, mobil cihazlar için bir içerik sayfası ekleyerek mobil işlemenin nasıl etkinleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3050b-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="3050b-118">*Sayfa1. cshtml* içerik ve bir gezinti kenar çubuğu içerir.</span><span class="sxs-lookup"><span data-stu-id="3050b-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="3050b-119">*Sayfa1. Mobile. cshtml* aynı içeriği içerir, ancak kenar çubuğunu atlar.</span><span class="sxs-lookup"><span data-stu-id="3050b-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="3050b-120">Bir ASP.NET Web Pages sitesinde, *Sayfa1. cshtml* adlı bir dosya oluşturun ve geçerli içeriği aşağıdaki biçimlendirme ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3050b-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="3050b-121">*Sayfa1. Mobile. cshtml* adlı bir dosya oluşturun ve var olan içeriği aşağıdaki biçimlendirme ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3050b-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="3050b-122">Sayfanın mobil sürümünün, daha küçük bir ekran üzerinde daha iyi işleme için gezinti bölümünü atladığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3050b-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="3050b-123">Bir masaüstü tarayıcısı çalıştırın ve *Sayfa1. cshtml*'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="3050b-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="3050b-124">mobilesites ![-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3050b-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="3050b-125">Bir mobil tarayıcı (veya bir mobil cihaz öykünücüsü) çalıştırın ve *Sayfa1. cshtml*'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="3050b-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="3050b-126">( *. Mobile eklemeyin.*</span><span class="sxs-lookup"><span data-stu-id="3050b-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="3050b-127">URL 'nin bir parçası olarak.) İstek *Sayfa1. cshtml*'ye olsa da ASP.net, *Sayfa1. Mobile. cshtml*işler.</span><span class="sxs-lookup"><span data-stu-id="3050b-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="3050b-129">Mobil sayfaları test etmek için masaüstü bilgisayarda çalışan bir mobil cihaz simülatörü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3050b-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="3050b-130">Bu araç, Web sayfalarını mobil cihazlara (genellikle çok daha küçük bir görüntüleme alanı ile) baktıkları gibi test etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3050b-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="3050b-131">Bir Benzetici örneği, Mozilla Firefox için [Kullanıcı Aracısı değiştirici eklentisinin](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) , çeşitli mobil tarayıcıları Firefox Masaüstü sürümünden öykünmenizi sağlayan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="3050b-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="3050b-132">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3050b-132">Additional Resources</span></span>

<span data-ttu-id="3050b-133">[Windows Phone öykünücü](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="3050b-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
