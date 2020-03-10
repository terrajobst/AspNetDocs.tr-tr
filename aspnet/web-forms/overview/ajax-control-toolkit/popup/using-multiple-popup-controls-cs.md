---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: Birden çok açılan denetim kullanmaC#() | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Ayrıca, d... kullanımı da mümkündür.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612653"
---
# <a name="using-multiple-popup-controls-c"></a><span data-ttu-id="1534b-104">Birden Çok Açılan Denetim Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="1534b-104">Using Multiple Popup Controls (C#)</span></span>

<span data-ttu-id="1534b-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="1534b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1534b-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1534b-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="1534b-107">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="1534b-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="1534b-108">Tek sayfada birden fazla açılan denetim kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="1534b-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="1534b-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="1534b-109">Overview</span></span>

<span data-ttu-id="1534b-110">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="1534b-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="1534b-111">Tek sayfada birden fazla açılan denetim kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="1534b-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="1534b-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="1534b-112">Steps</span></span>

<span data-ttu-id="1534b-113">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="1534b-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="1534b-114">Sonra, açılan pencere olarak işlev gören bir panel ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1534b-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="1534b-115">Geçerli senaryoda, panel bir `Calendar` denetimi içerir.</span><span class="sxs-lookup"><span data-stu-id="1534b-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="1534b-116">Takvimin geri göndermeler nedeniyle oluşan sayfa yenilemelerinden kaçınmak için, panel bir `UpdatePanel` denetimine yerleştirilir:</span><span class="sxs-lookup"><span data-stu-id="1534b-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="1534b-117">Sayfada Ayrıca iki metin kutusu de bulunur.</span><span class="sxs-lookup"><span data-stu-id="1534b-117">The page also contains two text boxes.</span></span> <span data-ttu-id="1534b-118">Her metin kutusu için, Takvim açılır penceresi metin kutusu etkinleştirildikten sonra görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1534b-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="1534b-119">Şimdi iki metin kutusunun her birini bir `PopupControlExtender`genişletin.</span><span class="sxs-lookup"><span data-stu-id="1534b-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="1534b-120">`TargetControlID` özniteliği, Extender 'a bağlı denetimin KIMLIĞINI sağlar.</span><span class="sxs-lookup"><span data-stu-id="1534b-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="1534b-121">`PopupControlID` özniteliği açılan bölmenin KIMLIĞINI içerir.</span><span class="sxs-lookup"><span data-stu-id="1534b-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="1534b-122">Bu durumda, her iki Extender da aynı paneli gösterir, ancak farklı paneller de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="1534b-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="1534b-123">Artık bir metin alanının içine tıkladığınızda alanın altında bir takvim görünür ve bir tarih seçmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1534b-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="1534b-124">(Seçili tarihin metin kutularına geri alınması farklı bir öğreticide ele alınacaktır.)</span><span class="sxs-lookup"><span data-stu-id="1534b-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="1534b-125">[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1534b-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="1534b-126">Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-multiple-popup-controls-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1534b-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1534b-127">Next</span><span class="sxs-lookup"><span data-stu-id="1534b-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
