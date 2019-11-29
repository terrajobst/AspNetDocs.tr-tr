---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: UpdatePanel denetimine animasyon ekleme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir... öğesinin içeriği için
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599928"
---
# <a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="3a1f3-104">Bir UpdatePanel Denetimine Animasyon Ekleme (C#)</span><span class="sxs-lookup"><span data-stu-id="3a1f3-104">Animating an UpdatePanel Control (C#)</span></span>

<span data-ttu-id="3a1f3-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="3a1f3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3a1f3-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3a1f3-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="3a1f3-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="3a1f3-108">Bir UpdatePanel 'ın içeriği için animasyon çerçevesinde yoğun bir şekilde yararlanan özel bir genişletici vardır: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="3a1f3-109">Bu öğreticide, bir UpdatePanel için böyle bir animasyonun nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="3a1f3-110">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="3a1f3-110">Overview</span></span>

<span data-ttu-id="3a1f3-111">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="3a1f3-112">Bir `UpdatePanel`içeriği için animasyon çerçevesine yoğun bir şekilde dayanan özel bir genişletici vardır: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="3a1f3-113">Bu öğreticide, `UpdatePanel`için bu animasyonun nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="3a1f3-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="3a1f3-114">Steps</span></span>

<span data-ttu-id="3a1f3-115">İlk adım, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için sayfaya `ScriptManager` dahil etmek için her zamanki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3a1f3-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="3a1f3-116">Bu senaryodaki animasyon, bir `UpdatePanel`bulunan bir ASP.NET `Wizard` Web denetimine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="3a1f3-117">Üç (rastgele) adım geri gönderileri tetiklemeye yetecek kadar seçenek sağlar:</span><span class="sxs-lookup"><span data-stu-id="3a1f3-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="3a1f3-118">`UpdatePanelAnimationExtender` denetimi için gereken biçimlendirme, `AnimationExtender`kullanılan biçimlendirmeye oldukça benzerdir.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="3a1f3-119">`TargetControlID` özniteliğinde, hareketlendirmek için `UpdatePanel` `ID` sağlıyoruz; `UpdatePanelAnimationExtender` denetimi içinde, `<Animations>` öğesi animasyon (ler) için XML biçimlendirmesi barındırır.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="3a1f3-120">Ancak bir farklılık vardır: olayların miktarı ve olay işleyicileri `AnimationExtender`karşılaştırma ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="3a1f3-121">`UpdatePanels`için, bunlardan yalnızca ikisi mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="3a1f3-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="3a1f3-122">UpdatePanel güncelleştirildiği zaman `<OnUpdated>`</span><span class="sxs-lookup"><span data-stu-id="3a1f3-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="3a1f3-123">UpdatePanel güncelleştirmeye başladığında `<OnUpdating>`</span><span class="sxs-lookup"><span data-stu-id="3a1f3-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="3a1f3-124">Bu senaryoda, `UpdatePanel` (geri gönderimin ardından) yeni içerikleri soluklaşır.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="3a1f3-125">Bunun için gereken biçimlendirme budur:</span><span class="sxs-lookup"><span data-stu-id="3a1f3-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="3a1f3-126">Artık UpdatePanel içinde bir geri gönderme gerçekleşdiğinde, panelin yeni içerikleri düzgün şekilde zayıflaşır.</span><span class="sxs-lookup"><span data-stu-id="3a1f3-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="3a1f3-127">[Sonraki sihirbaz adımının ![](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3a1f3-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="3a1f3-128">Sonraki sihirbaz adımı ([tam boyutlu görüntüyü görüntülemek Için tıklayın](animating-an-updatepanel-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3a1f3-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3a1f3-129">[Önceki](changing-an-animation-using-client-side-code-cs.md)
> [İleri](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="3a1f3-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
