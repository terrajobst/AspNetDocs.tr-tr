---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: Bir UpdatePanel denetimine (C#) animasyon ekleme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. İçeriği için bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 36d1166e1bd2b4c97b3cf3dd0bc3a7e8010a9443
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393699"
---
# <a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="fc127-104">Bir UpdatePanel Denetimine Animasyon Ekleme (C#)</span><span class="sxs-lookup"><span data-stu-id="fc127-104">Animating an UpdatePanel Control (C#)</span></span>

<span data-ttu-id="fc127-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fc127-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fc127-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="fc127-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="fc127-107">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="fc127-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fc127-108">UpdatePanel içeriğini için yoğun animasyon framework kullanan özel genişletici var: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="fc127-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="fc127-109">Bu öğreticide, bu tür animasyonu UpdatePanel için ayarlanacak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fc127-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>


## <a name="overview"></a><span data-ttu-id="fc127-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="fc127-110">Overview</span></span>

<span data-ttu-id="fc127-111">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="fc127-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fc127-112">İçeriği için bir `UpdatePanel`, yoğun animasyon framework kullanan özel genişletici var: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="fc127-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="fc127-113">Bu öğreticide gibi animasyon için ayarlama işlemi gösterilmektedir bir `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="fc127-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="fc127-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="fc127-114">Steps</span></span>

<span data-ttu-id="fc127-115">İlk adım zamanki dahil etmektir `ScriptManager` sayfasında ASP.NET AJAX kitaplığı yüklenir ve Denetim Araç Seti kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="fc127-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="fc127-116">Bu senaryoda animasyon için bir ASP.NET uygulanacak `Wizard` bulunan web denetimi bir `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="fc127-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="fc127-117">(İsteğe bağlı) üç adım geri göndermeler tetiklemek için yeterli seçenekleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="fc127-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="fc127-118">İşaretleme için gerekli `UpdatePanelAnimationExtender` denetimi için kullanılan biçimlendirme oldukça benzer `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="fc127-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="fc127-119">İçinde `TargetControlID` sağladığımız özniteliği `ID` , `UpdatePanel` animasyon uygulamak için; içinde `UpdatePanelAnimationExtender` denetimi `<Animations>` öğesi XML biçimlendirme için animation(s) tutar.</span><span class="sxs-lookup"><span data-stu-id="fc127-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="fc127-120">Ancak bir fark vardır: Comparison için olaylar ve olay işleyicileri miktarı sınırlıdır `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="fc127-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="fc127-121">İçin `UpdatePanels`, yalnızca iki tanesi var:</span><span class="sxs-lookup"><span data-stu-id="fc127-121">For `UpdatePanels`, only two of them exist:</span></span>

- `<OnUpdated>` <span data-ttu-id="fc127-122">UpdatePanel ne zaman güncelleştirildiğini</span><span class="sxs-lookup"><span data-stu-id="fc127-122">when the UpdatePanel has been updated</span></span>
- `<OnUpdating>` <span data-ttu-id="fc127-123">UpdatePanel güncelleştirme başladığında</span><span class="sxs-lookup"><span data-stu-id="fc127-123">when the UpdatePanel starts updating</span></span>

<span data-ttu-id="fc127-124">Bu senaryoda, yeni içeriği `UpdatePanel` (sonra geri gönderme) belirerek.</span><span class="sxs-lookup"><span data-stu-id="fc127-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="fc127-125">Bu, için gerekli biçimlendirme.</span><span class="sxs-lookup"><span data-stu-id="fc127-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="fc127-126">Bir geri gönderme UpdatePanel içinde olduğunda, artık yeni panel içerikleri yavaşça.</span><span class="sxs-lookup"><span data-stu-id="fc127-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>


[![T<span data-ttu-id="fc127-127">He sonraki sihirbaz adımı yavaş giriş]</span><span class="sxs-lookup"><span data-stu-id="fc127-127">he next wizard step is fading in]</span></span>(animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

<span data-ttu-id="fc127-128">Sonraki sihirbaz adımı Soluklaşan ([tam boyutlu görüntüyü görmek için tıklatın](animating-an-updatepanel-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fc127-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fc127-129">[Önceki](changing-an-animation-using-client-side-code-cs.md)
> [İleri](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="fc127-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
