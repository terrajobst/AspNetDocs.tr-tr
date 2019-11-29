---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: Kullanıcı etkileşimine yanıt olarak animasyon ekleme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonlar yıldız alabilir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 629d79505cebd49c2f05333bfbf78166f80fc6cb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607052"
---
# <a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="0a71b-104">Kullanıcı Etkileşimine Karşılık Olarak Animasyon Ekleme (VB)</span><span class="sxs-lookup"><span data-stu-id="0a71b-104">Animating in Response To User Interaction (VB)</span></span>

<span data-ttu-id="0a71b-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="0a71b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0a71b-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0a71b-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="0a71b-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="0a71b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0a71b-108">Animasyonlar otomatik olarak başlayabilir veya Kullanıcı etkileşimi tarafından, ör. fareyle tıklanarak tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="0a71b-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="0a71b-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="0a71b-109">Overview</span></span>

<span data-ttu-id="0a71b-110">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="0a71b-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0a71b-111">Animasyonlar otomatik olarak başlayabilir veya Kullanıcı etkileşimi tarafından, ör. fareyle tıklanarak tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="0a71b-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="0a71b-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="0a71b-112">Steps</span></span>

<span data-ttu-id="0a71b-113">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="0a71b-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="0a71b-114">Animasyon, şunun gibi görünen bir metin paneline uygulanır:</span><span class="sxs-lookup"><span data-stu-id="0a71b-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="0a71b-115">Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="0a71b-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="0a71b-116">Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0a71b-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="0a71b-117">`<Animations>` düğümü içinde, animasyonu Kullanıcı etkileşimi aracılığıyla başlatmaya yönelik beş yol vardır (eksik öğe, tüm sayfa tam olarak yüklendikten sonra yürütülür `<OnLoad>`):</span><span class="sxs-lookup"><span data-stu-id="0a71b-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="0a71b-118">`<OnClick>` (denetime fare tıklaması)</span><span class="sxs-lookup"><span data-stu-id="0a71b-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="0a71b-119">`<OnHoverOut>` (fare, denetimi bırakır)</span><span class="sxs-lookup"><span data-stu-id="0a71b-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="0a71b-120">`<OnHoverOver>` (fare bir denetimin üzerine geldiğinde `<OnHoverOut>` animasyonunu durduruyor)</span><span class="sxs-lookup"><span data-stu-id="0a71b-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="0a71b-121">`<OnMouseOut>` (fare bir denetimi bırakır)</span><span class="sxs-lookup"><span data-stu-id="0a71b-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="0a71b-122">`<OnMouseOver>` (fare, bir denetimin üzerine geldiğinde `<OnMouseOut>` animasyonunu durdurmaz)</span><span class="sxs-lookup"><span data-stu-id="0a71b-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="0a71b-123">Bu senaryoda `<OnClick>` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a71b-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="0a71b-124">Kullanıcı panele tıkladığında, yeniden boyutlandırılır ve aynı anda silinir.</span><span class="sxs-lookup"><span data-stu-id="0a71b-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

<span data-ttu-id="0a71b-125">[fare tıklaması ![animasyonu başlatır](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0a71b-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="0a71b-126">Fare tıklaması animasyonu başlatır ([tam boyutlu görüntüyü görüntülemek Için tıklatın](animating-in-response-to-user-interaction-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0a71b-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0a71b-127">[Önceki](picking-one-animation-out-of-a-list-vb.md)
> [İleri](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0a71b-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
