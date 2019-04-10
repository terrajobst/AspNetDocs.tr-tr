---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: (VB) ReorderList ile geri gönderme kullanma | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti ReorderList denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar. Listeyi yeniden her bir SAS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 22c7eecb841ff67196d21e6efeeda63a3456c5cb
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409089"
---
# <a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="d7991-104">ReorderList ile Geri Gönderme Kullanma (VB)</span><span class="sxs-lookup"><span data-stu-id="d7991-104">Using Postbacks with ReorderList (VB)</span></span>

<span data-ttu-id="d7991-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d7991-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d7991-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d7991-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="d7991-107">AJAX Denetim Araç Seti ReorderList denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7991-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="d7991-108">Listeyi yeniden olduğunda, bir geri gönderme sunucunun değişikliği bildirmek.</span><span class="sxs-lookup"><span data-stu-id="d7991-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="d7991-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d7991-109">Overview</span></span>

<span data-ttu-id="d7991-110">`ReorderList` AJAX Denetim Araç Seti denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7991-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="d7991-111">Listeyi yeniden olduğunda, bir geri gönderme sunucunun değişikliği bildirmek.</span><span class="sxs-lookup"><span data-stu-id="d7991-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="d7991-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="d7991-112">Steps</span></span>

<span data-ttu-id="d7991-113">Birkaç olası veri kaynağı için `ReorderList` denetimi.</span><span class="sxs-lookup"><span data-stu-id="d7991-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="d7991-114">Biridir kullanmak için bir `XmlDataSource` denetimi:</span><span class="sxs-lookup"><span data-stu-id="d7991-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="d7991-115">Bu XML bağlamak amacıyla bir `ReorderList` denetimi ve etkinleştirme Geri göndermeler, aşağıdaki öznitelikleri ayarlanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="d7991-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- `DataSourceID`<span data-ttu-id="d7991-116">: Veri kaynağı kimliği</span><span class="sxs-lookup"><span data-stu-id="d7991-116">: The ID of the data source</span></span>
- `SortOrderField`<span data-ttu-id="d7991-117">: Sıralama ölçütü olarak özelliği</span><span class="sxs-lookup"><span data-stu-id="d7991-117">: The property to sort by</span></span>
- `AllowReorder`<span data-ttu-id="d7991-118">: Liste öğeleri yeniden sıralamak kullanıcı izin verilip verilmeyeceğini</span><span class="sxs-lookup"><span data-stu-id="d7991-118">: Whether to allow the user to reorder the list elements</span></span>
- `PostBackOnReorder`<span data-ttu-id="d7991-119">: Listenin düzenlenmeyecek her bir geri gönderme oluşturulup oluşturulmayacağını</span><span class="sxs-lookup"><span data-stu-id="d7991-119">: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="d7991-120">Denetim için uygun biçimlendirmesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d7991-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="d7991-121">İçinde `ReorderList` denetimi, veri kaynağındaki belirli veri bağımlı kullanarak `Eval()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d7991-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="d7991-122">Son yeniden sıralama oluştuğunda rastgele bir konumda sayfasında, bilgileri bir etiket tutar:</span><span class="sxs-lookup"><span data-stu-id="d7991-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="d7991-123">Bu etiket, metin işleme geri gönderme sunucu tarafı kodu ile doldurulur:</span><span class="sxs-lookup"><span data-stu-id="d7991-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="d7991-124">Son olarak, ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` sayfada denetim yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7991-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


[![E<span data-ttu-id="d7991-125">ACH yeniden sıralama, bir geri gönderme tetikler]</span><span class="sxs-lookup"><span data-stu-id="d7991-125">ach reordering triggers a postback]</span></span>(using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

<span data-ttu-id="d7991-126">Bir geri gönderme her sipariş tetikler ([tam boyutlu görüntüyü görmek için tıklatın](using-postbacks-with-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d7991-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d7991-127">[Önceki](drag-and-drop-via-reorderlist-cs.md)
> [İleri](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d7991-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
