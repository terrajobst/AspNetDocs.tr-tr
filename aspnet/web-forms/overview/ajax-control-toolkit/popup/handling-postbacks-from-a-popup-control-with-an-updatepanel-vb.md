---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: UpdatePanel Ile bir açılan denetimden geri göndermeler işleme (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Özel dikkatli olunmalıdır...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: dd045ae56696c7944df98cf805ba812fde1bb4ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612898"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a><span data-ttu-id="8e907-104">UpdatePanel ile Bir Açılan Denetimden Gelen Geri Göndermeleri İşleme (VB)</span><span class="sxs-lookup"><span data-stu-id="8e907-104">Handling Postbacks from A Popup Control With an UpdatePanel (VB)</span></span>

<span data-ttu-id="8e907-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="8e907-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8e907-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8e907-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span></span>

> <span data-ttu-id="8e907-107">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="8e907-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="8e907-108">Bu tür bir açılan pencerede geri gönderme gerçekleşirken özel dikkatli olunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e907-108">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="overview"></a><span data-ttu-id="8e907-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="8e907-109">Overview</span></span>

<span data-ttu-id="8e907-110">AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="8e907-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="8e907-111">Bu tür bir açılan pencerede geri gönderme gerçekleşirken özel dikkatli olunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e907-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="8e907-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="8e907-112">Steps</span></span>

<span data-ttu-id="8e907-113">Geri göndermede bir `PopupControl` kullanırken, bir `UpdatePanel` geri gönderme nedeniyle oluşan sayfa yenilemeyi engelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8e907-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="8e907-114">Aşağıdaki biçimlendirme birkaç önemli öğeyi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="8e907-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="8e907-115">ASP.NET AJAX denetim araç seti 'nin çalışması için `ScriptManager` denetimi</span><span class="sxs-lookup"><span data-stu-id="8e907-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="8e907-116">Her ikisinin de bir açılan pencereyi tetikleyeceği iki `TextBox` denetimi</span><span class="sxs-lookup"><span data-stu-id="8e907-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="8e907-117">Açılan pencere olarak kullanılacak `Panel` denetimi</span><span class="sxs-lookup"><span data-stu-id="8e907-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="8e907-118">Panel içinde, bir `Calendar` denetimi bir `UpdatePanel` denetimine katıştırılır</span><span class="sxs-lookup"><span data-stu-id="8e907-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="8e907-119">Paneli metin kutularına atayan iki `PopupControlExtender` denetimi</span><span class="sxs-lookup"><span data-stu-id="8e907-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="8e907-120">`Calendar` denetiminin `OnSelectionChanged` özniteliğinin ayarlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8e907-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="8e907-121">Böylece Kullanıcı Takvim içinde bir tarih seçtiğinde, bir geri gönderme gerçekleşir ve sunucu tarafı yöntemi `c1_SelectionChanged()` yürütülür.</span><span class="sxs-lookup"><span data-stu-id="8e907-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="8e907-122">Bu yöntemde, geçerli tarih alınmalıdır ve metin kutusuna geri yazılır.</span><span class="sxs-lookup"><span data-stu-id="8e907-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="8e907-123">Bunun sözdizimi şöyledir: Ilki, sayfada `PopupControlExtender` için bir proxy nesnesi oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e907-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="8e907-124">ASP.NET AJAX denetim araç seti `GetProxyForCurrentPopup()` yöntemini sunar.</span><span class="sxs-lookup"><span data-stu-id="8e907-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="8e907-125">Bu yöntemin döndürdüğü nesne, açılan pencereyi tetikleyen denetime bir değer gönderen `Commit()` yöntemini destekler (yöntem çağrısını tetikleyen denetim değil!).</span><span class="sxs-lookup"><span data-stu-id="8e907-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="8e907-126">Aşağıdaki kod, `Commit()` yönteminin bağımsız değişkeni olarak seçilen tarihi sağlar ve kodun seçili tarihi tekrar metin kutusuna yazmasına neden olur:</span><span class="sxs-lookup"><span data-stu-id="8e907-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="8e907-127">Artık Takvim tarihine tıkladığınızda, ilişkili metin kutusunda seçilen tarih görüntülenir, bu, şu anda birçok Web sitesinde bulunan bir tarih seçici denetimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8e907-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>

<span data-ttu-id="8e907-128">[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8e907-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="8e907-129">Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8e907-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="8e907-130">[bir tarihe tıklamak ![metin kutusuna koyar](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8e907-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="8e907-131">Bir tarihe tıklamak, metin kutusuna koyar ([tam boyutlu görüntüyü görüntülemek Için tıklayın](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8e907-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8e907-132">[Önceki](using-multiple-popup-controls-vb.md)
> [İleri](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8e907-132">[Previous](using-multiple-popup-controls-vb.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span></span>
