---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: Listeden bir animasyon seçme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Çerçeve ayrıca allo...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 694416532b558291ff6ab57a442058b53d6167e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536115"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a><span data-ttu-id="6f92f-104">Bir Listeden Animasyon Seçme (VB)</span><span class="sxs-lookup"><span data-stu-id="6f92f-104">Picking One Animation Out Of a List (VB)</span></span>

<span data-ttu-id="6f92f-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="6f92f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6f92f-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="6f92f-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span></span>

> <span data-ttu-id="6f92f-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="6f92f-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6f92f-108">Framework Ayrıca programcı 'nin bazı JavaScript kodunun değerlendirmesine bağlı olarak bir animasyon listesinden bir animasyon seçmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6f92f-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="6f92f-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="6f92f-109">Overview</span></span>

<span data-ttu-id="6f92f-110">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="6f92f-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6f92f-111">Framework Ayrıca programcı 'nin bazı JavaScript kodunun değerlendirmesine bağlı olarak bir animasyon listesinden bir animasyon seçmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6f92f-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="6f92f-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="6f92f-112">Steps</span></span>

<span data-ttu-id="6f92f-113">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="6f92f-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

<span data-ttu-id="6f92f-114">Animasyon, şunun gibi görünen bir metin paneline uygulanır:</span><span class="sxs-lookup"><span data-stu-id="6f92f-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

<span data-ttu-id="6f92f-115">Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="6f92f-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

<span data-ttu-id="6f92f-116">Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory sağlayarak sayfaya `AnimationExtender` ekleyin `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="6f92f-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

<span data-ttu-id="6f92f-117">`<Animations>` düğümü içinde, sayfa tam olarak yüklendikten sonra animasyonları çalıştırmak için `<OnLoad>` kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f92f-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="6f92f-118">`<Case>` öğesi, normal animasyonlardan biri yerine yürütmeye gelir.</span><span class="sxs-lookup"><span data-stu-id="6f92f-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="6f92f-119">SelectScript özniteliğinin değeri değerlendirilir; dönüş değeri sayısal olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6f92f-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="6f92f-120">Bu sayıya bağlı olarak, &lt;Case&gt; içindeki alt animasyonlardan biri yürütülür.</span><span class="sxs-lookup"><span data-stu-id="6f92f-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="6f92f-121">Örneğin, Selectscrıpt 2 olarak değerlendirilirse, Denetim araç seti &lt;Case&gt; içinde üçüncü animasyonu çalıştırır (sayım 0 ' dan başlar).</span><span class="sxs-lookup"><span data-stu-id="6f92f-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="6f92f-122">Aşağıdaki biçimlendirme üç alt animasyonu tanımlar: genişliği yeniden boyutlandırma, yüksekliği yeniden boyutlandırma ve genişleme. JavaScript kodu (`Math.floor(3 * Math.random())`), üç animasyondan birinin çalışması için 0 ile 2 arasında bir sayı seçer:</span><span class="sxs-lookup"><span data-stu-id="6f92f-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]

<span data-ttu-id="6f92f-123">[mümkün olan üç animasyondan birini ![: panel daha geniştir](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f92f-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span></span>

<span data-ttu-id="6f92f-124">Olası üç animasyondan biri: panel daha geniştir ([tam boyutlu görüntüyü görüntülemek Için tıklatın](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6f92f-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6f92f-125">[Önceki](animation-depending-on-a-condition-vb.md)
> [İleri](animating-in-response-to-user-interaction-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6f92f-125">[Previous](animation-depending-on-a-condition-vb.md)
[Next](animating-in-response-to-user-interaction-vb.md)</span></span>
