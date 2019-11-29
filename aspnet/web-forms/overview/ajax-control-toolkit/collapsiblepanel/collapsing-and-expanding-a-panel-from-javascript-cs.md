---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: JavaScript 'ten bir paneli daraltma ve genişletme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde CollapsiblePanel denetimi bir paneli genişletir ve içeriğini daraltma ve bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: bed14d82394d28336493bec10e31ddb4d411a192
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599459"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-c"></a><span data-ttu-id="21ab6-103">JavaScript’ten Bir Paneli Daraltma ve Genişletme (C#)</span><span class="sxs-lookup"><span data-stu-id="21ab6-103">Collapsing and Expanding a Panel from JavaScript (C#)</span></span>

<span data-ttu-id="21ab6-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="21ab6-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="21ab6-105">[Kodu indirin](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="21ab6-105">[Download Code](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span></span>

> <span data-ttu-id="21ab6-106">ASP.NET AJAX denetim araç setinde CollapsiblePanel denetimi bir paneli genişletir ve içeriğini daraltma ve yeniden genişletme özelliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="21ab6-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="21ab6-107">Bu iki eylem özel JavaScript kodundan de tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="21ab6-107">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="21ab6-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="21ab6-108">Overview</span></span>

<span data-ttu-id="21ab6-109">ASP.NET AJAX denetim araç setinde CollapsiblePanel denetimi bir paneli genişletir ve içeriğini daraltma ve yeniden genişletme özelliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="21ab6-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="21ab6-110">Bu iki eylem özel JavaScript kodundan de tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="21ab6-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="21ab6-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="21ab6-111">Steps</span></span>

<span data-ttu-id="21ab6-112">İlk olarak, yeni bir ASP.NET sayfası oluşturun ve `ScriptManager` bir `<form>` öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="21ab6-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="21ab6-113">Bu, Denetim araç seti için gerekli olan ASP.NET AJAX kitaplığını yükler:</span><span class="sxs-lookup"><span data-stu-id="21ab6-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="21ab6-114">Ardından, daraltma/genişletme efektinin görünebilmesi için bazı metinlere sahip bir panel oluşturun:</span><span class="sxs-lookup"><span data-stu-id="21ab6-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="21ab6-115">Gördüğünüz gibi, panel burada gösterilen bir CSS sınıfına başvurur (ve temelde bir arka plan rengi ve panelin genişliğini tanımlar):</span><span class="sxs-lookup"><span data-stu-id="21ab6-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

<span data-ttu-id="21ab6-116">`CollapsiblePanelExtender` denetimi `TargetControlID` özniteliğini gerektirir, böylece araç seti, istek üzerine hangi bölmenin daraltılacak veya genişletileceğini bilir:</span><span class="sxs-lookup"><span data-stu-id="21ab6-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

<span data-ttu-id="21ab6-117">Ne yazık ki genişletici, paneli daraltma veya genişletme için belirli bir API kullanıma sunmuyor, ancak belgelenmemiş bazı yöntemler yapılacak.</span><span class="sxs-lookup"><span data-stu-id="21ab6-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="21ab6-118">İlk olarak, sayfaya üç HTML düğmesi ekleyin ve ardından panelin içeriğini daraltmak veya genişletmek için istemci tarafı JavaScript 'i tetikler:</span><span class="sxs-lookup"><span data-stu-id="21ab6-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="21ab6-119">İstemci tarafı JavaScript kodunda (`<script type="text/javascript">`ile başlatılır), `CollapsiblePanelExtender`erişmek için `$find()` yönteminin kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21ab6-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="21ab6-120">`$find("cpe")`, buna bir başvuru döndürür.</span><span class="sxs-lookup"><span data-stu-id="21ab6-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="21ab6-121">Bu noktada, belirli yöntemler el ile görevi çözebilir.</span><span class="sxs-lookup"><span data-stu-id="21ab6-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="21ab6-122">Paneli açma (genişletme) yöntemi `_doOpen()`olarak adlandırılır; Aşağıdaki kod, ilk düğme tıklandığında çağrılan `doOpen()` işlevini uygular:</span><span class="sxs-lookup"><span data-stu-id="21ab6-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

<span data-ttu-id="21ab6-123">Paneli kapatmak veya daraltma için `_doClose()` yönteminin yürütülmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="21ab6-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="21ab6-124">Bu nedenle, Kullanıcı ikinci düğmeye tıkladığında aşağıdaki JavaScript kodu çağrılır:</span><span class="sxs-lookup"><span data-stu-id="21ab6-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

<span data-ttu-id="21ab6-125">Üçüncü düğme, panelin durumunu daraltıldı ve bunun tersini yapar.</span><span class="sxs-lookup"><span data-stu-id="21ab6-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="21ab6-126">`CollapsiblePanelExtender`, tam olarak bunu yapan ve panelin durumunu tersine getiren `toggle()` yöntemini kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="21ab6-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="21ab6-127">Ancak, `toggle()` yöntemi tarafından dahili olarak kullanılan başka bir yaklaşım da vardır: `CollapsiblePanelExtender()` `get_Collapsed()` yöntemi, bölmenin daraltılıp daraltılmadığını söyler.</span><span class="sxs-lookup"><span data-stu-id="21ab6-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="21ab6-128">Bu işlevin dönüş değerine bağlı olarak, panel daha sonra genişletilir (`_doOpen()` yöntemi) veya daraltılmış (`_doClose()`) yöntemi:</span><span class="sxs-lookup"><span data-stu-id="21ab6-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]

<span data-ttu-id="21ab6-129">[üçüncü düğme ![bölmenin durumunu değiştirir: daraltılan ve geriye doğru](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="21ab6-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="21ab6-130">Üçüncü düğme, panelin durumunu, daraltılan ve geri ([tam boyutlu görüntüyü görüntülemek Için tıklatın](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png)) olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="21ab6-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="21ab6-131">Next</span><span class="sxs-lookup"><span data-stu-id="21ab6-131">Next</span></span>](collapsing-and-expanding-a-panel-from-javascript-vb.md)
