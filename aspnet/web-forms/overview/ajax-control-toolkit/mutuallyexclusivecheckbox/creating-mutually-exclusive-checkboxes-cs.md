---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: Birbirini dışlayan onay kutuları oluşturmaC#() | Microsoft Docs
author: wenz
description: Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır. Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613073"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a><span data-ttu-id="699a2-104">Birbirini Dışlayan Onay Kutuları Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="699a2-104">Creating Mutually Exclusive Checkboxes (C#)</span></span>

<span data-ttu-id="699a2-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="699a2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="699a2-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="699a2-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span></span>

> <span data-ttu-id="699a2-107">Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="699a2-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="699a2-108">Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra tüm radyo düğmelerinin işaretini kaldırmak mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="699a2-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="699a2-109">Onay kutuları herhangi bir zamanda işaretlenmeyebilir, ancak birbirini dışlamayan değildir.</span><span class="sxs-lookup"><span data-stu-id="699a2-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="699a2-110">Bu öğretici her iki yaklaşımdan en iyi şekilde yararlanabilirsiniz: birbirini dışlayan onay kutuları.</span><span class="sxs-lookup"><span data-stu-id="699a2-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="699a2-111">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="699a2-111">Overview</span></span>

<span data-ttu-id="699a2-112">Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="699a2-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="699a2-113">Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra tüm radyo düğmelerinin işaretini kaldırmak mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="699a2-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="699a2-114">Onay kutuları herhangi bir zamanda işaretlenmeyebilir, ancak birbirini dışlamayan değildir.</span><span class="sxs-lookup"><span data-stu-id="699a2-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="699a2-115">Bu öğretici her iki yaklaşımdan en iyi şekilde yararlanabilirsiniz: birbirini dışlayan onay kutuları.</span><span class="sxs-lookup"><span data-stu-id="699a2-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="699a2-116">Adımlar</span><span class="sxs-lookup"><span data-stu-id="699a2-116">Steps</span></span>

<span data-ttu-id="699a2-117">ASP.NET AJAX denetim araç seti, Muluallyexclusivecheckbox genişletici öğesini içerir.</span><span class="sxs-lookup"><span data-stu-id="699a2-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="699a2-118">Bu, programcıların bir grup adına (`Key` özniteliği) herhangi bir onay kutusu atamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="699a2-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="699a2-119">Aynı grup içindeki tüm onay kutularından tek seferde yalnızca bir tane seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="699a2-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="699a2-120">Yeni bir ASP.NET sayfasına iki onay kutusu yerleştirmeye başlayalım.</span><span class="sxs-lookup"><span data-stu-id="699a2-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="699a2-121">Daha fazla olabilir, ancak bu ilkeyi göstermek için iki ikisi de vardır:</span><span class="sxs-lookup"><span data-stu-id="699a2-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

<span data-ttu-id="699a2-122">Her iki onay kutusu için de sayfada bir çoklu kullanıcı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="699a2-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="699a2-123">Her iki anahtar özniteliği de aynı değere sahip olmalıdır, ancak HTML radyo düğmesi öğelerinin değer özniteliklerinin ait oldukları grubu göstermek için aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="699a2-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="699a2-124">Extender 'ın TargetControlID özelliği, onay kutusunun KIMLIĞINE işaret eder.</span><span class="sxs-lookup"><span data-stu-id="699a2-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

<span data-ttu-id="699a2-125">Son olarak, ASP.NET AJAX denetim araç setinin tüm öğeleri için gerekli olan ASP.NET AJAX `ScriptManager` ekleyin:</span><span class="sxs-lookup"><span data-stu-id="699a2-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

<span data-ttu-id="699a2-126">Sayfayı kaydedip çalıştırın: onay kutularının her ikisini de denetleyebilir ve işaretini kaldırın, ancak her iki onay kutusu da onay kutularından denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="699a2-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="699a2-127">[![, tek seferde yalnızca bir onay kutusu denetlenebilir](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="699a2-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span></span>

<span data-ttu-id="699a2-128">Tek seferde yalnızca bir onay kutusu denetlenebilir ([tam boyutlu görüntüyü görüntülemek Için tıklatın](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="699a2-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="699a2-129">Next</span><span class="sxs-lookup"><span data-stu-id="699a2-129">Next</span></span>](creating-mutually-exclusive-checkboxes-vb.md)
