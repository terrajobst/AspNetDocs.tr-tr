---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: UpdatePanel animasyonlarını (VB) dinamik olarak denetleme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. İçeriği için bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 223fad7013a53212c0c822a87bd3e2fcc0a5f17f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408959"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="706e7-104">UpdatePanel Animasyonlarını Dinamik Olarak Denetleme (VB)</span><span class="sxs-lookup"><span data-stu-id="706e7-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>

<span data-ttu-id="706e7-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="706e7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="706e7-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="706e7-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="706e7-107">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="706e7-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="706e7-108">UpdatePanel içeriğini için yoğun animasyon framework kullanan özel genişletici var: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="706e7-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="706e7-109">Ayrıca, UpdatePanel tetikleyicilerini birlikte de çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="706e7-109">It can also work together with UpdatePanel triggers.</span></span>


## <a name="overview"></a><span data-ttu-id="706e7-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="706e7-110">Overview</span></span>

<span data-ttu-id="706e7-111">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="706e7-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="706e7-112">İçeriği için bir `UpdatePanel`, yoğun animasyon framework kullanan özel genişletici var: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="706e7-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="706e7-113">Ayrıca ile birlikte çalışabilir `UpdatePanel` tetikler.</span><span class="sxs-lookup"><span data-stu-id="706e7-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="706e7-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="706e7-114">Steps</span></span>

<span data-ttu-id="706e7-115">İlk adım zamanki dahil etmektir `ScriptManager` sayfasında ASP.NET AJAX kitaplığı yüklenir ve Denetim Araç Seti kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="706e7-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="706e7-116">Bu senaryoda animasyon geçerli zaman bir ekrana uygulanır.</span><span class="sxs-lookup"><span data-stu-id="706e7-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="706e7-117">Bu bilgileri kullanarak bir etiket yazılabilir `Page_Load()` yöntemi veya aşağıdaki satır içi kod (basitleştirmek amacıyla) kullanılır:</span><span class="sxs-lookup"><span data-stu-id="706e7-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="706e7-118">Ayrıca, bir düğme tetikleyicisi sürekli güncelleştirmek için oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="706e7-118">Also, a button to trigger updating the time is created:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="706e7-119">Bu kod içine yerleştirilir `<ContentTemplate>` bölümünü bir `UpdatePanel` öğesi.</span><span class="sxs-lookup"><span data-stu-id="706e7-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="706e7-120">Bölmenin `UpdateMode` özniteliği ayarlanmalıdır `"Conditional"`, olduğundan yalnızca Tetikleyicileri bölmenin içeriği güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="706e7-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="706e7-121">İçinde `<Triggers>` bölümünü `UpdatePanel`, bir zaman uyumsuz geri gönderme tetikleyici oluşturulur ve bağlı `Click` düğmesinin olayı.</span><span class="sxs-lookup"><span data-stu-id="706e7-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="706e7-122">Bu nedenle, kullanıcı düğmesine tıklarsa `UpdatePanel` yenilenir.</span><span class="sxs-lookup"><span data-stu-id="706e7-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="706e7-123">İçin biçimlendirme şöyledir `UpdatePanel` denetimi:</span><span class="sxs-lookup"><span data-stu-id="706e7-123">Here is the markup for the `UpdatePanel` control:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="706e7-124">Son olarak, `UpdatePanelAnimationExtender` yapılandırılması gerekir: Ayarlama `TargetControlID` özniteliği panel Kimliğine ve bir animasyon Genişleticisi içinde tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="706e7-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="706e7-125">Soluklaşan yapar güncelleştirilmiş zaman iyi bir visual indirimlere oluşturan mantıklı.</span><span class="sxs-lookup"><span data-stu-id="706e7-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="706e7-126">Ardından, genişletici biçimlendirme şöyle görünebilir:</span><span class="sxs-lookup"><span data-stu-id="706e7-126">Your extender markup may then look like this:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="706e7-127">Dosyayı tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="706e7-127">Run the file in the browser.</span></span> <span data-ttu-id="706e7-128">Düğmeye tıklattığınızda, geçerli zamanı her zaman bir saniye boyunca Soldurma panelinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="706e7-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>


[![T<span data-ttu-id="706e7-129">Geçerli saati kendisinin Soluklaşan]</span><span class="sxs-lookup"><span data-stu-id="706e7-129">he current time is fading in]</span></span>(dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)

<span data-ttu-id="706e7-130">Geçerli saati Soluklaşan ([tam boyutlu görüntüyü görmek için tıklatın](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="706e7-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="706e7-131">Önceki</span><span class="sxs-lookup"><span data-stu-id="706e7-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
