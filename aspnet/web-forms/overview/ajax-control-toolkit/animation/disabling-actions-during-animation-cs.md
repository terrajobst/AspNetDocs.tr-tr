---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
title: Animasyon sırasında eylemleri devre dışıC#bırakma () | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Ayrıca eylemi destekler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 918026b4-2f63-421d-8546-df12856960a8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
msc.type: authoredcontent
ms.openlocfilehash: e91205ad2f9e6ee1fdd869ceb7587c3a82754772
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599722"
---
# <a name="disabling-actions-during-animation-c"></a><span data-ttu-id="5928b-104">Animasyon Sırasında Eylemleri Devre Dışı Bırakma (C#)</span><span class="sxs-lookup"><span data-stu-id="5928b-104">Disabling Actions during Animation (C#)</span></span>

<span data-ttu-id="5928b-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="5928b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5928b-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5928b-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span></span>

> <span data-ttu-id="5928b-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="5928b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5928b-108">Ayrıca, fare tıklamaları gibi eylemleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="5928b-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="5928b-109">Ancak fare tıklaması bir animasyon başlattığında animasyon sırasında fare tıklamalarını devre dışı bırakmak tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="5928b-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="5928b-110">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="5928b-110">Overview</span></span>

<span data-ttu-id="5928b-111">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="5928b-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5928b-112">Ayrıca, fare tıklamaları gibi eylemleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="5928b-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="5928b-113">Ancak fare tıklaması bir animasyon başlattığında animasyon sırasında fare tıklamalarını devre dışı bırakmak tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="5928b-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="5928b-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="5928b-114">Steps</span></span>

<span data-ttu-id="5928b-115">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="5928b-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample1.aspx)]

<span data-ttu-id="5928b-116">Animasyon, şöyle bir HTML düğmesine uygulanacak:</span><span class="sxs-lookup"><span data-stu-id="5928b-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample2.aspx)]

<span data-ttu-id="5928b-117">Bir Web denetimi yerine bir HTML denetimi kullanıldığını unutmayın; bu, düğmenin geri gönderme oluşturmasını istemedik; Yalnızca bizim için istemci tarafı animasyonunu başlatacaktır.</span><span class="sxs-lookup"><span data-stu-id="5928b-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="5928b-118">Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5928b-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample3.aspx)]

<span data-ttu-id="5928b-119">`<Animations>` düğümü içinde, `<OnClick>` fare tıklamasını işlemek için doğru öğedir.</span><span class="sxs-lookup"><span data-stu-id="5928b-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="5928b-120">Ancak, düğme animasyon sırasında da tıklanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5928b-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="5928b-121">`<EnableAction>` öğesi bundan yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5928b-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="5928b-122">`Enabled="false"` ayarlamak, animasyonun bir parçası olarak düğmeyi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="5928b-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="5928b-123">Birkaç ayrı animasyon (düğmeyi ve gerçek animasyonları devre dışı bırakarak) kullandığından `<Parallel>` öğesi, tek animasyonları bir araya birleştirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5928b-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="5928b-124">`AnimationExtender`için tüm biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5928b-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample4.aspx)]

<span data-ttu-id="5928b-125">Ayrıca, listenin sonunda aşağıdaki XML öğesini kullanarak Animasyondan sonra düğme için yeniden etkinleştirmek mümkün olacaktır:</span><span class="sxs-lookup"><span data-stu-id="5928b-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-cs/samples/sample5.xml)]

<span data-ttu-id="5928b-126">Ancak verilen senaryoda, düğme silinerek ve animasyonun sonunda görünmediğinden bu durum gereksizdir.</span><span class="sxs-lookup"><span data-stu-id="5928b-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="5928b-127">[![animasyon çalıştıktan hemen sonra düğme devre dışı bırakılır](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5928b-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span></span>

<span data-ttu-id="5928b-128">Animasyon çalıştıktan hemen sonra düğme devre dışı bırakılır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](disabling-actions-during-animation-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5928b-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5928b-129">[Önceki](animating-in-response-to-user-interaction-cs.md)
> [İleri](triggering-an-animation-in-another-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="5928b-129">[Previous](animating-in-response-to-user-interaction-cs.md)
[Next](triggering-an-animation-in-another-control-cs.md)</span></span>
