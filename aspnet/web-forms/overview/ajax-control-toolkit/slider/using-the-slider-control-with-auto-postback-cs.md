---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: Otomatik geri gönderme (C#) Ile kaydırıcı denetimini kullanma | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcı için bir oto gönder...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598375"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="2fd76-104">Otomatik geri gönderme (C#) Ile kaydırıcı denetimini kullanma</span><span class="sxs-lookup"><span data-stu-id="2fd76-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="2fd76-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="2fd76-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2fd76-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="2fd76-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="2fd76-107">AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fd76-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="2fd76-108">Kaydırıcıyı, değeri değiştiğinde AutoPostBack hale getirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="2fd76-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="2fd76-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="2fd76-109">Overview</span></span>

<span data-ttu-id="2fd76-110">AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fd76-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="2fd76-111">Kaydırıcıyı, değeri değiştiğinde AutoPostBack hale getirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="2fd76-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="2fd76-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="2fd76-112">Steps</span></span>

<span data-ttu-id="2fd76-113">Kaydırıcıyı bir değişikliğe göre otomatik olarak geri göndermeye olanak tanımak için, her iki metin kutusu da `AutoPostBack="true"`: kaydırıcı olacak metin kutusu ve kaydırıcının konumunu tutan metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2fd76-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="2fd76-114">Bunun için gereken biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2fd76-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="2fd76-115">ASP.NET AJAX denetim araç setinde `SliderExtender` denetimi, kaydırıcı işlevlerini iki metin kutusuna atar:</span><span class="sxs-lookup"><span data-stu-id="2fd76-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="2fd76-116">Daha sonra bir geri gönderme kullanıcıyı bilgilendirmek için ek bir etiket öğesi kullanılacaktır:</span><span class="sxs-lookup"><span data-stu-id="2fd76-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="2fd76-117">Son olarak, ASP.NET AJAX 'un `ScriptManager` denetimi, Denetim araç seti 'nin çalışması için gerekli JavaScript 'ı yükler:</span><span class="sxs-lookup"><span data-stu-id="2fd76-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="2fd76-118">Artık kaydırıcı geri gönderilir; sunucu tarafında bu olay yakalanıp şu şekilde olabilir:</span><span class="sxs-lookup"><span data-stu-id="2fd76-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

<span data-ttu-id="2fd76-119">[kaydırıcıyı taşımak ![bir geri gönderme tetikler](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2fd76-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="2fd76-120">Kaydırıcıyı hareket ettirmek bir geri gönderme tetikliyor ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2fd76-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>

<span data-ttu-id="2fd76-121">[daha sonra ![, bu değişikliğin tarihi etikette yazılır](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="2fd76-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="2fd76-122">Daha sonra, bu değişikliğin tarihi etikette yazılır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2fd76-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2fd76-123">Next</span><span class="sxs-lookup"><span data-stu-id="2fd76-123">Next</span></span>](databinding-the-slider-control-cs.md)
