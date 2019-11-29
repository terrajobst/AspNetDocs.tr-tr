---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: UpdatePanel olmayan bir açılan denetimden geri göndermeler işleme (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Su 'ta geri gönderme gerçekleştiğinde...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598757"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a><span data-ttu-id="b9ea5-104">UpdatePanel Olmadan Bir Açılan Denetimden Gelen Geri Göndermeleri İşleme (C#)</span><span class="sxs-lookup"><span data-stu-id="b9ea5-104">Handling Postbacks from A Popup Control Without an UpdatePanel (C#)</span></span>

<span data-ttu-id="b9ea5-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="b9ea5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b9ea5-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b9ea5-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span></span>

> <span data-ttu-id="b9ea5-107">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="b9ea5-108">Bu tür bir panelde geri gönderme gerçekleştiğinde ve sayfada birkaç panel varsa, hangi panelin tıklandığını tespit etmek zordur.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="b9ea5-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="b9ea5-109">Overview</span></span>

<span data-ttu-id="b9ea5-110">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="b9ea5-111">Bu tür bir panelde geri gönderme gerçekleştiğinde ve sayfada birkaç panel varsa, hangi panelin tıklandığını tespit etmek zordur.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="b9ea5-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="b9ea5-112">Steps</span></span>

<span data-ttu-id="b9ea5-113">Bir geri gönderme ile `PopupControl` kullanırken, ancak sayfada `UpdatePanel` olmadan Denetim araç seti, açılan pencereyi tetikleyen ve geri göndermeye neden olan istemci öğenin belirlenmesi için bir yol sunmaz.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="b9ea5-114">Ancak küçük bir püf konusu senaryo için geçici çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="b9ea5-115">İlki, temel kurulum şudur: her iki metin kutusu de aynı açılan pencereyi bir takvimle tetikler.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="b9ea5-116">İki `PopupControlExtenders` metin kutularını ve açılan pencereyi birlikte getirin.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="b9ea5-117">Temel düşünce, açılan pencereyi başlatan metin kutusunu tutan &lt;`form`&gt; öğesine gizli form alanı eklemektir:</span><span class="sxs-lookup"><span data-stu-id="b9ea5-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="b9ea5-118">Sayfa yüklendiğinde, JavaScript kodu her iki metin kutusuna da bir olay işleyicisi ekler: Kullanıcı bir metin kutusunu tıkladığında, adı gizli form alanına yazılır:</span><span class="sxs-lookup"><span data-stu-id="b9ea5-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

<span data-ttu-id="b9ea5-119">Sunucu tarafı kodunda, gizli alanın değeri okunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="b9ea5-120">Gizli form alanları işlemek için önemsiz olduğundan, gizli değeri doğrulamaya yönelik bir beyaz liste yaklaşımı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="b9ea5-121">Doğru metin kutusu tanımlandıktan sonra takvimdeki Tarih buna yazılır.</span><span class="sxs-lookup"><span data-stu-id="b9ea5-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

<span data-ttu-id="b9ea5-122">[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b9ea5-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="b9ea5-123">Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b9ea5-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span></span>

<span data-ttu-id="b9ea5-124">[bir tarihe tıklamak ![metin kutusuna koyar](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b9ea5-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="b9ea5-125">Bir tarihe tıklamak, metin kutusuna koyar ([tam boyutlu görüntüyü görüntülemek Için tıklayın](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b9ea5-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b9ea5-126">[Önceki](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [İleri](using-multiple-popup-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b9ea5-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
[Next](using-multiple-popup-controls-vb.md)</span></span>
