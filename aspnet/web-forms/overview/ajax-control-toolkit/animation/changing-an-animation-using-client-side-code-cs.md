---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: Istemci tarafı kod kullanarak bir animasyonu değiştirme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon Ayrıca,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606973"
---
# <a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="a72e4-104">İstemci Tarafı Kod Kullanarak Bir Animasyonu Değiştirme (C#)</span><span class="sxs-lookup"><span data-stu-id="a72e4-104">Changing an Animation Using Client-Side Code (C#)</span></span>

<span data-ttu-id="a72e4-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="a72e4-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a72e4-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a72e4-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="a72e4-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="a72e4-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a72e4-108">Animasyon özel istemci tarafı JavaScript kodu kullanılarak da değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a72e4-108">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="a72e4-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="a72e4-109">Overview</span></span>

<span data-ttu-id="a72e4-110">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="a72e4-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a72e4-111">Animasyon özel istemci tarafı JavaScript kodu kullanılarak da değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a72e4-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="a72e4-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="a72e4-112">Steps</span></span>

<span data-ttu-id="a72e4-113">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="a72e4-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="a72e4-114">Animasyon, şunun gibi görünen bir metin paneline uygulanır:</span><span class="sxs-lookup"><span data-stu-id="a72e4-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="a72e4-115">Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a72e4-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="a72e4-116">Gerçek animasyon bir HTML düğmesi tarafından başlatılır:</span><span class="sxs-lookup"><span data-stu-id="a72e4-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="a72e4-117">Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a72e4-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="a72e4-118">`AnimationExtender` denetiminde `<Animations>` düğüm olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a72e4-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="a72e4-119">Özel JavaScript kodu, denetimle birlikte kullanılacak animasyonları sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a72e4-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="a72e4-120">`AnimationExtender`sunucu API 'sinde olduğu gibi, henüz Extender 'a animasyon atamak için kolay bir yol yoktur.</span><span class="sxs-lookup"><span data-stu-id="a72e4-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="a72e4-121">Ancak, Extender çeşitli olaylara (`OnClick`, `OnLoad`vb.) kayıtlı animasyonları okumak ve yazmak için çeşitli yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="a72e4-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="a72e4-122">Aşağıda bazı örnekler verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a72e4-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="a72e4-123">`get_*()` işlevlerinin dönüş değeri ve `set_*()` işlevlerinin bağımsız değişkeninin biçimi, XML biçimlendirmesinin ne olacağını gösteren bir nesne gösterimi sağlayan bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="a72e4-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="a72e4-124">Şu anda ' de bir nesne geçirmenin bir yolu yoktur, ancak belirli bir animasyondan (`get_OnXXXBehavior()` Yöntemler) bir nesneyi okumak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="a72e4-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="a72e4-125">Bu, düğme tarafından tetiklenen bir animasyonu temsil eden bir JSON dizesi (sınırlandırma tırnak işaretleri olmadan ve düzgün biçimlendirilmeksizin), ancak yeniden boyutlandırılırken ve aynı zamanda onu kaldırarak panele animasyon uygulayarak paneli canlandırdığında:</span><span class="sxs-lookup"><span data-stu-id="a72e4-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="a72e4-126">Aşağıdaki JavaScript kodu, bu JSON descripöğesini geçerli genişleticin `OnClick` animasyonuna atar ve bunu çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="a72e4-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

<span data-ttu-id="a72e4-127">[animasyon hemen, fare tıklaması olmadan (ve çok az biçimlendirme ile) çalışır ![](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a72e4-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="a72e4-128">Animasyon hemen, fare tıklaması olmadan (çok az biçimlendirme ile) çalışır ([tam boyutlu görüntüyü görüntülemek Için tıklatın](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a72e4-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a72e4-129">[Önceki](executing-animations-using-client-side-code-cs.md)
> [İleri](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a72e4-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
