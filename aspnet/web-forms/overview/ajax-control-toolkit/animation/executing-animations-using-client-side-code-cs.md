---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: Istemci tarafı kodu kullanarak animasyonları yürütme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon yürütme...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: b6ba1553b9c8c51d5d6ae1679e53f9cc1d17b769
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598184"
---
# <a name="executing-animations-using-client-side-code-c"></a><span data-ttu-id="9efe9-104">Animasyonları İstemci Tarafı Kod Kullanarak Yürütme (C#)</span><span class="sxs-lookup"><span data-stu-id="9efe9-104">Executing Animations Using Client-Side Code (C#)</span></span>

<span data-ttu-id="9efe9-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="9efe9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9efe9-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="9efe9-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span></span>

> <span data-ttu-id="9efe9-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="9efe9-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="9efe9-108">Animasyon yürütme, özel istemci tarafı JavaScript kodu kullanılarak da tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="9efe9-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="9efe9-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="9efe9-109">Overview</span></span>

<span data-ttu-id="9efe9-110">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="9efe9-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="9efe9-111">Animasyon yürütme, özel istemci tarafı JavaScript kodu kullanılarak da tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="9efe9-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="9efe9-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="9efe9-112">Steps</span></span>

<span data-ttu-id="9efe9-113">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="9efe9-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="9efe9-114">Animasyon, şunun gibi görünen bir metin paneline uygulanır:</span><span class="sxs-lookup"><span data-stu-id="9efe9-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="9efe9-115">Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="9efe9-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="9efe9-116">Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9efe9-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="9efe9-117">`<Animations>` düğümü içinde Kullanıcı panele tıkladıktan sonra animasyonları çalıştırmak için `<OnClick>` kullanın.</span><span class="sxs-lookup"><span data-stu-id="9efe9-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="9efe9-118">Paralel olarak yürütülecek iki animasyon ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9efe9-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

<span data-ttu-id="9efe9-119">Tanıtım için, bu animasyon (ve Denetim araç seti kullanılarak oluşturulan diğer animasyonlar), sayfa çalıştıktan sonra JavaScript kodu kullanılarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="9efe9-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="9efe9-120">Tüm bunların ilki `AnimationExtender` denetimine erişmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9efe9-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="9efe9-121">ASP.NET AJAX kitaplığı bu görev için `$find()` işlevi sağlar:</span><span class="sxs-lookup"><span data-stu-id="9efe9-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

<span data-ttu-id="9efe9-122">`AnimationExtender` denetimi, XML biçimlendirmesinde kullanılan olay işleyicileriyle aynı adlara sahip yöntemler de dahil olmak üzere zengin bir API 'yi kullanıma sunar: `OnClick()`, `OnLoad()`, vb.</span><span class="sxs-lookup"><span data-stu-id="9efe9-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="9efe9-123">Örneğin, `OnClick()` yönteminin bir çağrısı, animasyonu `AnimationExtender` denetiminin `<OnClick>` öğesi içinde yürütür:</span><span class="sxs-lookup"><span data-stu-id="9efe9-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

<span data-ttu-id="9efe9-124">Bu, sayfa tam olarak yüklendikten sonra, sayfa ve dahil edilen tüm JavaScript kitaplıkları yüklendikten sonra, ASP.NET AJAX tarafından çağrılan `pageLoad()` işlevi adının kullanıldığına ilişkin tam istemci tarafı JavaScript kodu ' nu aşağıda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9efe9-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]

<span data-ttu-id="9efe9-125">[animasyon, fare tıklaması olmadan hemen çalıştırılır ![](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9efe9-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="9efe9-126">Animasyon hemen çalışır, fare tıklaması olmadan ([tam boyutlu görüntüyü görüntülemek Için tıklatın](executing-animations-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9efe9-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9efe9-127">[Önceki](modifying-animations-from-the-server-side-cs.md)
> [İleri](changing-an-animation-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9efe9-127">[Previous](modifying-animations-from-the-server-side-cs.md)
[Next](changing-an-animation-using-client-side-code-cs.md)</span></span>
