---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX denetim araç seti ile çalışmaya başlama (VB) | Microsoft Docs
author: microsoft
description: AJAX denetim araç setini kullanmaya başlamak için bilmeniz gereken her şey hakkında bilgi edinin.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613486"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="50cde-103">AJAX Denetim Araç Seti ile Çalışmaya Başlama (VB)</span><span class="sxs-lookup"><span data-stu-id="50cde-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="50cde-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="50cde-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="50cde-105">AJAX denetim araç setini kullanmaya başlamak için bilmeniz gereken her şey hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="50cde-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="50cde-106">AJAX denetim araç seti, ASP.NET uygulamalarınızda kullanabileceğiniz 30 ' dan fazla ücretsiz denetim içerir.</span><span class="sxs-lookup"><span data-stu-id="50cde-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="50cde-107">Bu öğreticide, AJAX denetim araç setini indirme ve araç seti denetimlerini Visual Studio/Visual Web Developer Express araç kutusu 'na ekleme hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="50cde-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="50cde-108">AJAX denetim araç seti indiriliyor</span><span class="sxs-lookup"><span data-stu-id="50cde-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="50cde-109">[AJAX denetim araç seti](http://devexpress.com/act) , ASP.net community ve ASP.net ekibinin üyeleri tarafından geliştirilen açık kaynaklı bir projem.</span><span class="sxs-lookup"><span data-stu-id="50cde-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>

<span data-ttu-id="50cde-110">[AJAX denetim araç setini Indirmek ![](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="50cde-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span></span>

<span data-ttu-id="50cde-111">**Şekil 01**: AJAX denetim araç seti indiriliyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="50cde-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>

<span data-ttu-id="50cde-112">Dosyayı indirdikten sonra dosyanın engellemesini kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="50cde-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="50cde-113">Dosyaya sağ tıklayın, Özellikler ' i seçin ve **Engellemeyi kaldır** düğmesine tıklayın (bkz. Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="50cde-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="50cde-114">[AJAX denetim araç seti ZIP dosyasının engellemesini kaldırma ![](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="50cde-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span></span>

<span data-ttu-id="50cde-115">**Şekil 02**: AJAX denetim araç seti ZIP dosyasının engellemesini kaldırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="50cde-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>

<span data-ttu-id="50cde-116">Dosyanın engellemesini kaldırdıktan sonra, dosyayı açabilir: dosyaya sağ tıklayıp **Tümünü Ayıkla** menü seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="50cde-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="50cde-117">Şimdi, araç takımını Visual Studio/Visual Web Developer araç kutusu 'na eklemeye hazırız.</span><span class="sxs-lookup"><span data-stu-id="50cde-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="50cde-118">Araç kutusuna AJAX denetim araç seti ekleme</span><span class="sxs-lookup"><span data-stu-id="50cde-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="50cde-119">AJAX denetim araç takımını kullanmanın en kolay yolu, araç takımını Visual Studio/Visual Web Developer araç kutusu 'na eklemektir (bkz. Şekil 3).</span><span class="sxs-lookup"><span data-stu-id="50cde-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="50cde-120">Bu şekilde, yalnızca bir araç seti denetimini kullanmak istediğinizde bir sayfaya sürükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50cde-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="50cde-121">[Araç kutusu 'nda ![AJAX denetim araç seti görüntülenir](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="50cde-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span></span>

<span data-ttu-id="50cde-122">**Şekil 03**: araç kutusu 'Nda AJAX denetim araç seti görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="50cde-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>

<span data-ttu-id="50cde-123">İlk olarak, araç kutusu 'na bir AJAX denetim araç seti sekmesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="50cde-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="50cde-124">Şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="50cde-124">Follow these steps.</span></span>

1. <span data-ttu-id="50cde-125">Yeni Web sitesi olan menü seçenek dosyasını seçerek yeni bir ASP.NET Web sitesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="50cde-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="50cde-126">Dosyayı düzenleyicide açmak için Çözüm Gezgini penceresindeki default. aspx dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="50cde-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="50cde-127">Genel sekmesinin altındaki araç kutusu ' na sağ tıklayın ve **Sekme Ekle** menü seçeneğini belirleyin (bkz. Şekil 4).</span><span class="sxs-lookup"><span data-stu-id="50cde-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="50cde-128">AJAX denetim araç seti adlı yeni bir sekme girin.</span><span class="sxs-lookup"><span data-stu-id="50cde-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="50cde-129">[Yeni sekme ekleme ![](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="50cde-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span></span>

<span data-ttu-id="50cde-130">**Şekil 04**: yeni sekme ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="50cde-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>

<span data-ttu-id="50cde-131">Ardından, AJAX denetim araç seti denetimlerini yeni sekmeye eklemeniz gerekir. şu adımları Izleyin:</span><span class="sxs-lookup"><span data-stu-id="50cde-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="50cde-132">AJAX denetim araç seti sekmesinin altına sağ tıklayın ve öğe seçin menü seçeneğini belirleyin **(bkz. Şekil 5)** .</span><span class="sxs-lookup"><span data-stu-id="50cde-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="50cde-133">AJAX denetim araç takımını sıkıştırmışın ve AjaxControlToolkit. dll derlemesini seçebileceğiniz konuma göz atın.</span><span class="sxs-lookup"><span data-stu-id="50cde-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="50cde-134">[araç kutusuna eklenecek öğeleri seçin ![](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="50cde-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span></span>

<span data-ttu-id="50cde-135">**Şekil 05**: araç kutusuna eklenecek öğeleri seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="50cde-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>

<span data-ttu-id="50cde-136">Bu adımları tamamladıktan sonra araç kutusu denetimleri araç kutusunda görünür.</span><span class="sxs-lookup"><span data-stu-id="50cde-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="50cde-137">Araç setinin yeni bir sürümüne yükseltme</span><span class="sxs-lookup"><span data-stu-id="50cde-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="50cde-138">Araç setinin eski bir sürümünü kullanıyorsanız ve şu anda daha sonraki bir sürüme geçiş yapmanız gerekiyorsa önerilen adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="50cde-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="50cde-139">İkili dosyalar-Web sitesi bin klasörünüzdeki AjaxControlToolkit. dll derlemesinin eski sürümünü silin.</span><span class="sxs-lookup"><span data-stu-id="50cde-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="50cde-140">Araç kutusu öğeleri-AJAX denetim araç seti sekmesini silin ve aşağıdaki adımları izleyerek, bu sekmeyi, AjaxControlToolkit. dll derlemesinin yeni sürümü ile yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="50cde-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="50cde-141">[Önceki](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [İleri](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="50cde-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
