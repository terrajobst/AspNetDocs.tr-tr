---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: Kaydırıcı denetimini veri bağlama (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Geçerli pozitif durumlar bağlamak mümkündür...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598291"
---
# <a name="databinding-the-slider-control-vb"></a><span data-ttu-id="227ac-104">Kaydırıcı Denetiminde Veri Bağlama (VB)</span><span class="sxs-lookup"><span data-stu-id="227ac-104">Databinding the Slider Control (VB)</span></span>

<span data-ttu-id="227ac-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="227ac-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="227ac-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="227ac-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span></span>

> <span data-ttu-id="227ac-107">AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="227ac-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="227ac-108">Kaydırıcısının geçerli konumunu başka bir ASP.NET denetimine bağlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="227ac-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="overview"></a><span data-ttu-id="227ac-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="227ac-109">Overview</span></span>

<span data-ttu-id="227ac-110">AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="227ac-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="227ac-111">Kaydırıcısının geçerli konumunu başka bir ASP.NET denetimine bağlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="227ac-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="227ac-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="227ac-112">Steps</span></span>

<span data-ttu-id="227ac-113">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="227ac-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

<span data-ttu-id="227ac-114">Sonra, sayfaya iki `TextBox` denetimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="227ac-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="227ac-115">Biri bir grafik kaydırıcısının içine dönüştürülecek ve diğeri kaydırıcının konumunu tutacaktır.</span><span class="sxs-lookup"><span data-stu-id="227ac-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

<span data-ttu-id="227ac-116">Sonraki adım zaten son adımdır.</span><span class="sxs-lookup"><span data-stu-id="227ac-116">The next step is already the final step.</span></span> <span data-ttu-id="227ac-117">ASP.NET AJAX denetim araç setinde `SliderExtender` denetimi, ilk metin kutusunun bir kaydırıcısını açar ve kaydırıcı konumu değiştiğinde ikinci metin kutusunu otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="227ac-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="227ac-118">Bunun çalışması için, `SliderExtender``TargetControlID` özniteliği ilk metin kutusunun KIMLIĞI olarak ayarlanmalıdır; `BoundControlID` özniteliğin ikinci metin kutusunun KIMLIĞINE ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="227ac-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

<span data-ttu-id="227ac-119">Tarayıcıda görebileceğiniz gibi, veri bağlama her iki yönde de çalışacaktır: metin kutusuna yeni bir değer girildiğinde kaydırıcının konumunu günceller.</span><span class="sxs-lookup"><span data-stu-id="227ac-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="227ac-120">İkinci metin kutusunu salt okunurdur yaparsanız, metin alanına zayıf bir koruma ekleyebilirsiniz, böylece Kullanıcı burada değeri el ile güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="227ac-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>

<span data-ttu-id="227ac-121">[![kaydırıcı ve metin kutusu eşitlenmiş](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="227ac-121">[![Slider and text box are in sync](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="227ac-122">Kaydırıcı ve metin kutusu eşitlenmiş ([tam boyutlu görüntüyü görüntülemek Için tıklayın](databinding-the-slider-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="227ac-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="227ac-123">Öncekini</span><span class="sxs-lookup"><span data-stu-id="227ac-123">Previous</span></span>](using-the-slider-control-with-auto-postback-vb.md)
