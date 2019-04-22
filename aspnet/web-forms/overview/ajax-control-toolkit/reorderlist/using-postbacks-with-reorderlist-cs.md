---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: (C#) ReorderList ile geri gönderme kullanma | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti ReorderList denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar. Listeyi yeniden her bir SAS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 6f8f74b74080104980e1db866d695fe7c6d9d5fc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59393359"
---
# <a name="using-postbacks-with-reorderlist-c"></a><span data-ttu-id="a6401-104">ReorderList ile Geri Gönderme Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="a6401-104">Using Postbacks with ReorderList (C#)</span></span>

<span data-ttu-id="a6401-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a6401-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a6401-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a6401-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span></span>

> <span data-ttu-id="a6401-107">AJAX Denetim Araç Seti ReorderList denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6401-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="a6401-108">Listeyi yeniden olduğunda, bir geri gönderme sunucunun değişikliği bildirmek.</span><span class="sxs-lookup"><span data-stu-id="a6401-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="a6401-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a6401-109">Overview</span></span>

<span data-ttu-id="a6401-110">`ReorderList` AJAX Denetim Araç Seti denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6401-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="a6401-111">Listeyi yeniden olduğunda, bir geri gönderme sunucunun değişikliği bildirmek.</span><span class="sxs-lookup"><span data-stu-id="a6401-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="a6401-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="a6401-112">Steps</span></span>

<span data-ttu-id="a6401-113">Birkaç olası veri kaynağı için `ReorderList` denetimi.</span><span class="sxs-lookup"><span data-stu-id="a6401-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="a6401-114">Biridir kullanmak için bir `XmlDataSource` denetimi:</span><span class="sxs-lookup"><span data-stu-id="a6401-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="a6401-115">Bu XML bağlamak amacıyla bir `ReorderList` denetimi ve etkinleştirme Geri göndermeler, aşağıdaki öznitelikleri ayarlanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="a6401-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="a6401-116">`DataSourceID`: Veri kaynağı kimliği</span><span class="sxs-lookup"><span data-stu-id="a6401-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="a6401-117">`SortOrderField`: Sıralama ölçütü olarak özelliği</span><span class="sxs-lookup"><span data-stu-id="a6401-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="a6401-118">`AllowReorder`: Liste öğeleri yeniden sıralamak kullanıcı izin verilip verilmeyeceğini</span><span class="sxs-lookup"><span data-stu-id="a6401-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="a6401-119">`PostBackOnReorder`: Listenin düzenlenmeyecek her bir geri gönderme oluşturulup oluşturulmayacağını</span><span class="sxs-lookup"><span data-stu-id="a6401-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="a6401-120">Denetim için uygun biçimlendirmesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a6401-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="a6401-121">İçinde `ReorderList` denetimi, veri kaynağındaki belirli veri bağımlı kullanarak `Eval()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a6401-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

<span data-ttu-id="a6401-122">Son yeniden sıralama oluştuğunda rastgele bir konumda sayfasında, bilgileri bir etiket tutar:</span><span class="sxs-lookup"><span data-stu-id="a6401-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="a6401-123">Bu etiket, metin işleme geri gönderme sunucu tarafı kodu ile doldurulur:</span><span class="sxs-lookup"><span data-stu-id="a6401-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

<span data-ttu-id="a6401-124">Son olarak, ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` sayfada denetim yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="a6401-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]


<span data-ttu-id="a6401-125">[![Bir geri gönderme tetikleyen her yeniden sıralama](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a6401-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="a6401-126">Bir geri gönderme her sipariş tetikler ([tam boyutlu görüntüyü görmek için tıklatın](using-postbacks-with-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a6401-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a6401-127">Next</span><span class="sxs-lookup"><span data-stu-id="a6401-127">Next</span></span>](drag-and-drop-via-reorderlist-cs.md)
