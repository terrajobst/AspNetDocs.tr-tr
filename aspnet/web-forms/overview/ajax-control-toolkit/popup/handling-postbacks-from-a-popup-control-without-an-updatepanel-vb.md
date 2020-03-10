---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: UpdatePanel olmayan bir açılan denetimden geri göndermeler işleme (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Su 'ta geri gönderme gerçekleştiğinde...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: aaecf77c1d25f2c99ef4e9948d79fc01b837169b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553986"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="e22f0-104">UpdatePanel Olmadan Bir Açılan Denetimden Gelen Geri Göndermeleri İşleme (VB)</span><span class="sxs-lookup"><span data-stu-id="e22f0-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="e22f0-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="e22f0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e22f0-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e22f0-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="e22f0-107">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="e22f0-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="e22f0-108">Bu tür bir panelde geri gönderme gerçekleştiğinde ve sayfada birkaç panel varsa, hangi panelin tıklandığını tespit etmek zordur.</span><span class="sxs-lookup"><span data-stu-id="e22f0-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="e22f0-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="e22f0-109">Overview</span></span>

<span data-ttu-id="e22f0-110">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="e22f0-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="e22f0-111">Bu tür bir panelde geri gönderme gerçekleştiğinde ve sayfada birkaç panel varsa, hangi panelin tıklandığını tespit etmek zordur.</span><span class="sxs-lookup"><span data-stu-id="e22f0-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="e22f0-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="e22f0-112">Steps</span></span>

<span data-ttu-id="e22f0-113">Bir geri gönderme ile `PopupControl` kullanırken, ancak sayfada `UpdatePanel` olmadan Denetim araç seti, açılan pencereyi tetikleyen ve geri göndermeye neden olan istemci öğenin belirlenmesi için bir yol sunmaz.</span><span class="sxs-lookup"><span data-stu-id="e22f0-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="e22f0-114">Ancak küçük bir püf konusu senaryo için geçici çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="e22f0-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="e22f0-115">İlki, temel kurulum şudur: her iki metin kutusu de aynı açılan pencereyi bir takvimle tetikler.</span><span class="sxs-lookup"><span data-stu-id="e22f0-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="e22f0-116">İki `PopupControlExtenders` metin kutularını ve açılan pencereyi birlikte getirin.</span><span class="sxs-lookup"><span data-stu-id="e22f0-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="e22f0-117">Temel düşünce, açılan pencereyi başlatan metin kutusunu tutan &lt;`form`&gt; öğesine gizli form alanı eklemektir:</span><span class="sxs-lookup"><span data-stu-id="e22f0-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="e22f0-118">Sayfa yüklendiğinde, JavaScript kodu her iki metin kutusuna da bir olay işleyicisi ekler: Kullanıcı bir metin kutusunu tıkladığında, adı gizli form alanına yazılır:</span><span class="sxs-lookup"><span data-stu-id="e22f0-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="e22f0-119">Sunucu tarafı kodunda, gizli alanın değeri okunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e22f0-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="e22f0-120">Gizli form alanları işlemek için önemsiz olduğundan, gizli değeri doğrulamaya yönelik bir beyaz liste yaklaşımı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e22f0-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="e22f0-121">Doğru metin kutusu tanımlandıktan sonra takvimdeki Tarih buna yazılır.</span><span class="sxs-lookup"><span data-stu-id="e22f0-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

<span data-ttu-id="e22f0-122">[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e22f0-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="e22f0-123">Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e22f0-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="e22f0-124">[bir tarihe tıklamak ![metin kutusuna koyar](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e22f0-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="e22f0-125">Bir tarihe tıklamak, metin kutusuna koyar ([tam boyutlu görüntüyü görüntülemek Için tıklayın](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e22f0-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e22f0-126">Öncekini</span><span class="sxs-lookup"><span data-stu-id="e22f0-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
