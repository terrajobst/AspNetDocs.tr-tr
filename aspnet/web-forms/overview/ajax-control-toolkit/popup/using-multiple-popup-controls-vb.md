---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: Birden çok açılan denetim kullanma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Ayrıca, d... kullanımı da mümkündür.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: e1f4ff64e9fdf48ea63b75c97acd53a64b5ab5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611626"
---
# <a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="e542e-104">Birden Çok Açılan Denetim Kullanma (VB)</span><span class="sxs-lookup"><span data-stu-id="e542e-104">Using Multiple Popup Controls (VB)</span></span>

<span data-ttu-id="e542e-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="e542e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e542e-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e542e-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="e542e-107">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="e542e-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="e542e-108">Tek sayfada birden fazla açılan denetim kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e542e-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="e542e-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="e542e-109">Overview</span></span>

<span data-ttu-id="e542e-110">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="e542e-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="e542e-111">Tek sayfada birden fazla açılan denetim kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e542e-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="e542e-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="e542e-112">Steps</span></span>

<span data-ttu-id="e542e-113">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="e542e-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="e542e-114">Sonra, açılan pencere olarak işlev gören bir panel ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e542e-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="e542e-115">Geçerli senaryoda, panel bir `Calendar` denetimi içerir.</span><span class="sxs-lookup"><span data-stu-id="e542e-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="e542e-116">Takvimin geri göndermeler nedeniyle oluşan sayfa yenilemelerinden kaçınmak için, panel bir `UpdatePanel` denetimine yerleştirilir:</span><span class="sxs-lookup"><span data-stu-id="e542e-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="e542e-117">Sayfada Ayrıca iki metin kutusu de bulunur.</span><span class="sxs-lookup"><span data-stu-id="e542e-117">The page also contains two text boxes.</span></span> <span data-ttu-id="e542e-118">Her metin kutusu için, Takvim açılır penceresi metin kutusu etkinleştirildikten sonra görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e542e-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="e542e-119">Şimdi iki metin kutusunun her birini bir `PopupControlExtender`genişletin.</span><span class="sxs-lookup"><span data-stu-id="e542e-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="e542e-120">`TargetControlID` özniteliği, Extender 'a bağlı denetimin KIMLIĞINI sağlar.</span><span class="sxs-lookup"><span data-stu-id="e542e-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="e542e-121">`PopupControlID` özniteliği açılan bölmenin KIMLIĞINI içerir.</span><span class="sxs-lookup"><span data-stu-id="e542e-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="e542e-122">Bu durumda, her iki Extender da aynı paneli gösterir, ancak farklı paneller de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e542e-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="e542e-123">Artık bir metin alanının içine tıkladığınızda alanın altında bir takvim görünür ve bir tarih seçmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e542e-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="e542e-124">(Seçili tarihin metin kutularına geri alınması farklı bir öğreticide ele alınacaktır.)</span><span class="sxs-lookup"><span data-stu-id="e542e-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="e542e-125">[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e542e-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="e542e-126">Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-multiple-popup-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e542e-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e542e-127">[Önceki](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [İleri](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e542e-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
