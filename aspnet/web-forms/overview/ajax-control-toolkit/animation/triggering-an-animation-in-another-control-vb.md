---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: Başka bir denetimde animasyon tetikleme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Genellikle, bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575020"
---
# <a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="d8bfd-104">Başka bir Denetimde Animasyon Tetikleme (VB)</span><span class="sxs-lookup"><span data-stu-id="d8bfd-104">Triggering an Animation in another Control (VB)</span></span>

<span data-ttu-id="d8bfd-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="d8bfd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d8bfd-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d8bfd-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="d8bfd-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d8bfd-108">Genellikle, bir animasyon başlatmak Kullanıcı etkileşimi tarafından aynı denetimle tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="d8bfd-109">Bununla birlikte, bir denetimle etkileşim kurmak ve daha sonra başka bir denetimi animasyon eklemek de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-109">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="overview"></a><span data-ttu-id="d8bfd-110">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="d8bfd-110">Overview</span></span>

<span data-ttu-id="d8bfd-111">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d8bfd-112">Genellikle, bir animasyon başlatmak Kullanıcı etkileşimi tarafından aynı denetimle tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="d8bfd-113">Bununla birlikte, bir denetimle etkileşim kurmak ve daha sonra başka bir denetimi animasyon eklemek de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="d8bfd-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="d8bfd-114">Steps</span></span>

<span data-ttu-id="d8bfd-115">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="d8bfd-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="d8bfd-116">Animasyon, şunun gibi görünen bir metin paneline uygulanır:</span><span class="sxs-lookup"><span data-stu-id="d8bfd-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="d8bfd-117">Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d8bfd-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="d8bfd-118">Panelin animasyon bölmesine başlamak için bir HTML düğmesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="d8bfd-119">Kullanıcı söz konusu düğmeye tıkladığında geri gönderme istemediğimiz için, `<input type="button" />` `<asp:Button />` üzerinde favoured olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="d8bfd-120">Daha sonra, `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak `AnimationExtender` sayfaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="d8bfd-121">Düğmenin kimliğine (animasyonu tetikleyen öğe) değil, panelin kimliğine `TargetControlID` ayarlanması önemlidir (canlandırılan öğe)</span><span class="sxs-lookup"><span data-stu-id="d8bfd-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="d8bfd-122">`<Animations>` düğümü içinde, animasyonları her zamanki gibi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="d8bfd-123">Düğmeleri değil, panelin değiştirilmesini sağlamak için, `AnimationExtender`içindeki her animasyon öğesi için `AnimationTarget` özniteliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="d8bfd-124">`AnimationTarget` değeri, kursun panelin KIMLIĞIDIR.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="d8bfd-125">Bu şekilde, animasyonlar tetikleyici düğmesiyle değil, panel ile gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="d8bfd-126">Bu senaryo için `AnimationExtender` biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d8bfd-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="d8bfd-127">Bireysel animasyonların göründüğü özel sıralamayı aklınızda yapın.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="d8bfd-128">Birincisi, animasyon çalıştıktan sonra düğme devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="d8bfd-129">`<EnableAction>` öğesinde `AnimationTarget` özniteliği olmadığından, bu animasyon kaynak denetimine uygulanır: düğme.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="d8bfd-130">Sonraki iki animasyon adımı paralel (`<Parallel>` öğe) olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="d8bfd-131">Her ikisinin de `AnimationTarget` öznitelikleri `"Panel1"`olarak ayarlanmıştır, böylece düğme değil paneli canlandırın.</span><span class="sxs-lookup"><span data-stu-id="d8bfd-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>

<span data-ttu-id="d8bfd-132">[düğme üzerinde fare tıklaması ![panel animasyonunu başlatır](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d8bfd-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="d8bfd-133">Düğmeye tıkladığınızda fare tıklaması panel animasyonunu başlatır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](triggering-an-animation-in-another-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d8bfd-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d8bfd-134">[Önceki](disabling-actions-during-animation-vb.md)
> [İleri](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d8bfd-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
