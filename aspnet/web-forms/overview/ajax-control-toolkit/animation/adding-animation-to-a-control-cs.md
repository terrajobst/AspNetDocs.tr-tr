---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: Bir denetime animasyon ekleme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu öğreticide nasıl yapılacağı gösterilmektedir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: dd63157fe616c5f6874b7cca11f4ede15018df04
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614452"
---
# <a name="adding-animation-to-a-control-c"></a><span data-ttu-id="c2057-104">Bir Denetime Animasyon Ekleme (C#)</span><span class="sxs-lookup"><span data-stu-id="c2057-104">Adding Animation to a Control (C#)</span></span>

<span data-ttu-id="c2057-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="c2057-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c2057-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c2057-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="c2057-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="c2057-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c2057-108">Bu öğreticide, bu tür bir animasyonun nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c2057-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="c2057-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="c2057-109">Overview</span></span>

<span data-ttu-id="c2057-110">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="c2057-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c2057-111">Bu öğreticide, bu tür bir animasyonun nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c2057-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="c2057-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="c2057-112">Steps</span></span>

<span data-ttu-id="c2057-113">İlk adım, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için sayfaya `ScriptManager` dahil etmek için her zamanki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c2057-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="c2057-114">Bu senaryodaki animasyon şuna benzer bir metin paneline uygulanacak:</span><span class="sxs-lookup"><span data-stu-id="c2057-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="c2057-115">Panelin ilişkili CSS sınıfı, arka plan rengini ve genişliğini tanımlar:</span><span class="sxs-lookup"><span data-stu-id="c2057-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="c2057-116">Bir sonraki adımda `AnimationExtender`ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="c2057-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="c2057-117">Bir `ID` ve olağan `runat="server"`sağladıktan sonra, `TargetControlID` özniteliği bizim örneğimizde animasyon uygulamak için denetime ayarlanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="c2057-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="c2057-118">Tüm animasyon bildirimli olarak Visual Studio 'nun IntelliSense tarafından tam olarak desteklenmeyen bir XML sözdizimi kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c2057-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="c2057-119">Kök düğüm bu düğüm dahilinde `<Animations>;`, animasyon (ler) ne zaman olacağını belirleyen çeşitli olaylara izin verilir:</span><span class="sxs-lookup"><span data-stu-id="c2057-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="c2057-120">`OnClick` (fare tıklaması)</span><span class="sxs-lookup"><span data-stu-id="c2057-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="c2057-121">`OnHoverOut` (fare bir denetimden çıktığında)</span><span class="sxs-lookup"><span data-stu-id="c2057-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="c2057-122">`OnHoverOver` (fare bir denetimin üzerine geldiğinde `OnHoverOut` animasyonunu durduruyor)</span><span class="sxs-lookup"><span data-stu-id="c2057-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="c2057-123">`OnLoad` (sayfa yüklendiğinde)</span><span class="sxs-lookup"><span data-stu-id="c2057-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="c2057-124">`OnMouseOut` (fare bir denetimden çıktığında)</span><span class="sxs-lookup"><span data-stu-id="c2057-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="c2057-125">`OnMouseOver` (fare, bir denetimin üzerine geldiğinde `OnMouseOut` animasyonunu durdurmadan)</span><span class="sxs-lookup"><span data-stu-id="c2057-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="c2057-126">Çerçeve, her biri kendi XML öğesiyle temsil edilen bir animasyon kümesiyle gelir.</span><span class="sxs-lookup"><span data-stu-id="c2057-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="c2057-127">İşte bir seçim:</span><span class="sxs-lookup"><span data-stu-id="c2057-127">Here is a selection:</span></span>

- <span data-ttu-id="c2057-128">`<Color>` (rengi değiştirme)</span><span class="sxs-lookup"><span data-stu-id="c2057-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="c2057-129">`<FadeIn>` (Soluklaşan)</span><span class="sxs-lookup"><span data-stu-id="c2057-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="c2057-130">`<FadeOut>` (Soluklaşan)</span><span class="sxs-lookup"><span data-stu-id="c2057-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="c2057-131">`<Property>` (denetimin özelliğini değiştirme)</span><span class="sxs-lookup"><span data-stu-id="c2057-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="c2057-132">`<Pulse>` (pulsating)</span><span class="sxs-lookup"><span data-stu-id="c2057-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="c2057-133">`<Resize>` (boyutu değiştirme)</span><span class="sxs-lookup"><span data-stu-id="c2057-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="c2057-134">`<Scale>` (boyutunu orantılı olarak değiştirme)</span><span class="sxs-lookup"><span data-stu-id="c2057-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="c2057-135">Bu örnekte, panel soluklaşır. Animasyon 1,5 saniye (`Duration` özniteliği) sürer ve saniyede 24 kare (animasyon adımları) (`Fps` özniteliği) görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c2057-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="c2057-136">`AnimationExtender` denetimi için tüm biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c2057-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="c2057-137">Bu komut dosyasını çalıştırdığınızda, panel görüntülenir ve bir ve yarım saniye aşağı silinerek belirir.</span><span class="sxs-lookup"><span data-stu-id="c2057-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="c2057-138">[Panel ![](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c2057-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="c2057-139">Panel soluklaşma ([tam boyutlu görüntüyü görüntülemek Için tıklayın](adding-animation-to-a-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c2057-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c2057-140">Next</span><span class="sxs-lookup"><span data-stu-id="c2057-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
