---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: UpdatePanel animasyonlarını dinamik olarak denetlemeC#() | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir... öğesinin içeriği için
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536206"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a><span data-ttu-id="9add2-104">UpdatePanel Animasyonlarını Dinamik Olarak Denetleme (C#)</span><span class="sxs-lookup"><span data-stu-id="9add2-104">Dynamically Controlling UpdatePanel Animations (C#)</span></span>

<span data-ttu-id="9add2-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="9add2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9add2-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="9add2-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span></span>

> <span data-ttu-id="9add2-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="9add2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="9add2-108">Bir UpdatePanel 'ın içeriği için animasyon çerçevesinde yoğun bir şekilde yararlanan özel bir genişletici vardır: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="9add2-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="9add2-109">Ayrıca, UpdatePanel tetikleyicilerle birlikte çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="9add2-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="9add2-110">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="9add2-110">Overview</span></span>

<span data-ttu-id="9add2-111">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="9add2-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="9add2-112">Bir `UpdatePanel`içeriği için animasyon çerçevesine yoğun bir şekilde dayanan özel bir genişletici vardır: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="9add2-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="9add2-113">Ayrıca, `UpdatePanel` tetikleyicilerle birlikte çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="9add2-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="9add2-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="9add2-114">Steps</span></span>

<span data-ttu-id="9add2-115">İlk adım, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için sayfaya `ScriptManager` dahil etmek için her zamanki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9add2-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

<span data-ttu-id="9add2-116">Bu senaryodaki animasyon geçerli saatin görüntüsüne uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9add2-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="9add2-117">Bu bilgiler `Page_Load()` yöntemi kullanılarak bir etikete yazılabilir veya (basitlik sağlamak için) aşağıdaki satır içi kod kullanılır:</span><span class="sxs-lookup"><span data-stu-id="9add2-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

<span data-ttu-id="9add2-118">Ayrıca, zaman güncellemenin tetiklenmesi için bir düğme oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="9add2-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

<span data-ttu-id="9add2-119">Bu kod daha sonra bir `UpdatePanel` öğesinin `<ContentTemplate>` bölümüne konur.</span><span class="sxs-lookup"><span data-stu-id="9add2-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="9add2-120">Panelin `UpdateMode` özniteliği `"Conditional"`olarak ayarlanmalıdır, çünkü yalnızca Tetikleyiciler panelin içeriğini güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="9add2-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="9add2-121">`UpdatePanel``<Triggers>` bölümünde, zaman uyumsuz bir geri gönderme tetikleyicisi oluşturulur ve düğmenin `Click` olayına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="9add2-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="9add2-122">Bu nedenle, Kullanıcı düğmeye tıkladığında `UpdatePanel` yenilenir.</span><span class="sxs-lookup"><span data-stu-id="9add2-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="9add2-123">`UpdatePanel` denetimi için biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9add2-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

<span data-ttu-id="9add2-124">Son olarak, `UpdatePanelAnimationExtender` yapılandırılması gerekir: `TargetControlID` özniteliğini panelin KIMLIĞI olarak ayarlayın ve Extender içinde bir animasyon tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9add2-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="9add2-125">' Deki soldurma, güncelleştirilmiş sürede iyi bir görsel vurgu oluşturan anlamda anlamlı hale gelir.</span><span class="sxs-lookup"><span data-stu-id="9add2-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="9add2-126">Daha sonra genişletici biçimlerinizin şöyle görünebiliriz:</span><span class="sxs-lookup"><span data-stu-id="9add2-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

<span data-ttu-id="9add2-127">Dosyayı tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9add2-127">Run the file in the browser.</span></span> <span data-ttu-id="9add2-128">Düğmeye tıkladığınızda, geçerli saat panelde gösterilir, her zaman bir saniye boyunca geçişi yapılır.</span><span class="sxs-lookup"><span data-stu-id="9add2-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="9add2-129">[geçerli zaman ![](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9add2-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span></span>

<span data-ttu-id="9add2-130">Şu anki Saat Soldurma ([tam boyutlu görüntüyü görüntülemek Için tıklayın](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9add2-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9add2-131">[Önceki](animating-an-updatepanel-control-cs.md)
> [İleri](adding-animation-to-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9add2-131">[Previous](animating-an-updatepanel-control-cs.md)
[Next](adding-animation-to-a-control-vb.md)</span></span>
