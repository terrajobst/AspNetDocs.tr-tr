---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: Bir DropShadow 'un Z dizinini ayarlama (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir. Bununla birlikte, bu gölge bazen diğer denetimlerle çelişmekte...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 12bc7f0430f1f30ff964cd9547ee1e9b0aa7423c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613885"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a><span data-ttu-id="ecdcc-104">Bir DropShadow’un Z Dizinini Ayarlama (C#)</span><span class="sxs-lookup"><span data-stu-id="ecdcc-104">Adjusting the Z-Index of a DropShadow (C#)</span></span>

<span data-ttu-id="ecdcc-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="ecdcc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ecdcc-106">[Kodu indirin](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ecdcc-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span></span>

> <span data-ttu-id="ecdcc-107">AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="ecdcc-108">Ancak bu gölge bazen diğer denetimlerle (örneğin, ASP.NET menü denetimi) çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="ecdcc-109">Bir menü girdisi açıldığında, bu gölge arkasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="overview"></a><span data-ttu-id="ecdcc-110">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="ecdcc-110">Overview</span></span>

<span data-ttu-id="ecdcc-111">AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="ecdcc-112">Ancak bu gölge bazen diğer denetimlerle (örneğin, ASP.NET menü denetimi) çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="ecdcc-113">Bir menü girdisi açıldığında, bu gölge arkasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="ecdcc-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="ecdcc-114">Steps</span></span>

<span data-ttu-id="ecdcc-115">Kod, panelin, efektin görünür olması için yeterli metin içermesi için yeterli metin içeren panelin kendisiyle yorum yapar:</span><span class="sxs-lookup"><span data-stu-id="ecdcc-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

<span data-ttu-id="ecdcc-116">Başka bir panel `panelShadow` panelinden doğrudan yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="ecdcc-117">Menü girişlerinin `dropShadow` panel) üzerinde görünmesi için yatay yönlendirmeye sahip bir menü içerir (veya bunun yerine: altında):</span><span class="sxs-lookup"><span data-stu-id="ecdcc-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

<span data-ttu-id="ecdcc-118">Sonra, `panelShadow` panelini bir gölge efektiyle genişletmek için `DropShadowExtender` eklenir:</span><span class="sxs-lookup"><span data-stu-id="ecdcc-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

<span data-ttu-id="ecdcc-119">Son olarak, ASP.NET AJAX `ScriptManager` denetimi denetim araç setinin çalışmasını sağlar:</span><span class="sxs-lookup"><span data-stu-id="ecdcc-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

<span data-ttu-id="ecdcc-120">Bu betiği çalıştırdığınızda, menü girdileri panelin altında görünür.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="ecdcc-121">Ancak menü, öğelerin diğer panelin önünde görünmesini sağlamak için yalnızca iki şey tanımlamanız gereken `panel` CSS sınıfını kullanır:</span><span class="sxs-lookup"><span data-stu-id="ecdcc-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="ecdcc-122">Göreli konumlandırma</span><span class="sxs-lookup"><span data-stu-id="ecdcc-122">Relative positioning</span></span>
- <span data-ttu-id="ecdcc-123">Pozitif bir z dizini</span><span class="sxs-lookup"><span data-stu-id="ecdcc-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

<span data-ttu-id="ecdcc-124">Daha sonra, `DropShadowExtender` denetimi menü denetimiyle daha uzun bir süre çakışmaz.</span><span class="sxs-lookup"><span data-stu-id="ecdcc-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>

<span data-ttu-id="ecdcc-125">[![önce: menü girdisi görünür değil](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ecdcc-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span></span>

<span data-ttu-id="ecdcc-126">Önce: menü girdisi görünür değil ([tam boyutlu görüntüyü görüntülemek Için tıklayın](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ecdcc-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span></span>

<span data-ttu-id="ecdcc-127">[![sonra: menü girdisi görüntülenir](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ecdcc-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span></span>

<span data-ttu-id="ecdcc-128">Sonra: menü girdisi görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ecdcc-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ecdcc-129">Next</span><span class="sxs-lookup"><span data-stu-id="ecdcc-129">Next</span></span>](manipulating-dropshadow-properties-from-client-code-cs.md)
