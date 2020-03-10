---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: Bir koşula bağlı animasyon (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonun olup olmadığı...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598352"
---
# <a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="404da-104">Bir Koşula Bağlı Animasyon (C#)</span><span class="sxs-lookup"><span data-stu-id="404da-104">Animation Depending On a Condition (C#)</span></span>

<span data-ttu-id="404da-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="404da-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="404da-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="404da-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="404da-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="404da-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="404da-108">Bir animasyonun çalıştırılıp çalıştırılmayacağı veya yüklenmediğini, bazı JavaScript kodu biçimindeki bir koşula de bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="404da-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="404da-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="404da-109">Overview</span></span>

<span data-ttu-id="404da-110">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="404da-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="404da-111">Bir animasyonun çalıştırılıp çalıştırılmayacağı veya yüklenmediğini, bazı JavaScript kodu biçimindeki bir koşula de bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="404da-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="404da-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="404da-112">Steps</span></span>

<span data-ttu-id="404da-113">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="404da-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="404da-114">Animasyon, şunun gibi görünen bir metin paneline uygulanır:</span><span class="sxs-lookup"><span data-stu-id="404da-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="404da-115">Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="404da-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="404da-116">Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory sağlayarak sayfaya `AnimationExtender` ekleyin `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="404da-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="404da-117">`<Animations>` düğümü içinde, sayfa tam olarak yüklendikten sonra animasyonları çalıştırmak için `<OnLoad>` kullanın.</span><span class="sxs-lookup"><span data-stu-id="404da-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="404da-118">`<Condition>` öğesi, normal animasyonlardan biri yerine yürütmeye gelir.</span><span class="sxs-lookup"><span data-stu-id="404da-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="404da-119">`ConditionScript` özniteliğinin değeri olarak belirtilen JavaScript kodu çalışma zamanında yürütülür.</span><span class="sxs-lookup"><span data-stu-id="404da-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="404da-120">True olarak değerlendirilirse animasyon yürütülür, aksi takdirde değildir.</span><span class="sxs-lookup"><span data-stu-id="404da-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="404da-121">Aşağıdaki biçimlendirme, her biri rastgele bir durum olan %50 ' de yürütülen iki animasyon sağlar.</span><span class="sxs-lookup"><span data-stu-id="404da-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="404da-122">`<OnLoad>`içinde yalnızca bir animasyon olabileceğinden, iki `<Condition>` animasyonları `<Sequence>` öğesi kullanılarak birlikte birleştirilir:</span><span class="sxs-lookup"><span data-stu-id="404da-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="404da-123">`ConditionScript` özniteliğinde küçüktür işareti (`<`) kaçışın () olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="404da-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="404da-124">Bu betiği çalıştırdığınızda, herhangi bir animasyon çalıştırması ya da iki ya da her ikisi de olamaz.</span><span class="sxs-lookup"><span data-stu-id="404da-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>

<span data-ttu-id="404da-125">[![panel, yeniden boyutlandırmadan soluklaşmakta, bu nedenle ikinci animasyon çalışır, ilki](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="404da-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span></span>

<span data-ttu-id="404da-126">Panel, yeniden boyutlandırmadan soluklaşmakta, bu nedenle ikinci animasyon çalışır, ilki değil ([tam boyutlu görüntüyü görüntülemek Için tıklatın](animation-depending-on-a-condition-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="404da-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="404da-127">[Önceki](executing-several-animations-after-each-other-cs.md)
> [İleri](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="404da-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
