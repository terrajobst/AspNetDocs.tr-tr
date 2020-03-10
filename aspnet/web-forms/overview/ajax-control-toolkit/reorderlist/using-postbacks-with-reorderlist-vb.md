---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: ReorderList ile geri göndermeler kullanma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar. Liste yeniden düzenlendiğinde bir Po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 5d6075e40df2c32df6c0d801243eff98fa7790b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553741"
---
# <a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="e8f05-104">ReorderList ile Geri Gönderme Kullanma (VB)</span><span class="sxs-lookup"><span data-stu-id="e8f05-104">Using Postbacks with ReorderList (VB)</span></span>

<span data-ttu-id="e8f05-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="e8f05-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e8f05-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e8f05-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="e8f05-107">AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8f05-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="e8f05-108">Liste yeniden sıralandığında, bir geri gönderme değişikliğin sunucusunu bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="e8f05-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="e8f05-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="e8f05-109">Overview</span></span>

<span data-ttu-id="e8f05-110">AJAX denetim araç setinde `ReorderList` denetimi, Kullanıcı tarafından sürükleme ve bırakma yoluyla yeniden sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8f05-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="e8f05-111">Liste yeniden sıralandığında, bir geri gönderme değişikliğin sunucusunu bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="e8f05-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="e8f05-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="e8f05-112">Steps</span></span>

<span data-ttu-id="e8f05-113">`ReorderList` denetimi için birkaç olası veri kaynağı vardır.</span><span class="sxs-lookup"><span data-stu-id="e8f05-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="e8f05-114">Bunlardan biri `XmlDataSource` bir denetim kullanmaktır:</span><span class="sxs-lookup"><span data-stu-id="e8f05-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="e8f05-115">Bu XML 'i bir `ReorderList` denetimine bağlamak ve geri gönderileri etkinleştirmek için aşağıdaki özniteliklerin ayarlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8f05-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="e8f05-116">`DataSourceID`: veri kaynağının KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="e8f05-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="e8f05-117">`SortOrderField`: sıralama yapılacak Özellik</span><span class="sxs-lookup"><span data-stu-id="e8f05-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="e8f05-118">`AllowReorder`: kullanıcının liste öğelerini yeniden sıralayıp izin verip vermediği</span><span class="sxs-lookup"><span data-stu-id="e8f05-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="e8f05-119">`PostBackOnReorder`: liste yeniden düzenlendiğinde geri gönderme oluşturulup oluşturulmayacağını belirtir</span><span class="sxs-lookup"><span data-stu-id="e8f05-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="e8f05-120">Denetim için uygun biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e8f05-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="e8f05-121">`ReorderList` denetimi içinde, veri kaynağındaki belirli veriler `Eval()` yöntemi kullanılarak bağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="e8f05-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="e8f05-122">Sayfada rastgele bir konumda, son yeniden sipariş oluştuğunda bir etiket bilgileri tutar:</span><span class="sxs-lookup"><span data-stu-id="e8f05-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="e8f05-123">Bu etiket, geri gönderme işlemi için sunucu tarafı kodundaki metinle doldurulmuştur:</span><span class="sxs-lookup"><span data-stu-id="e8f05-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="e8f05-124">Son olarak, ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada yer almalıdır:</span><span class="sxs-lookup"><span data-stu-id="e8f05-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

<span data-ttu-id="e8f05-125">[Her yeniden sıralama ![geri gönderme tetikler](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e8f05-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="e8f05-126">Her yeniden sıralama bir geri göndermeyi tetikler ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-postbacks-with-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e8f05-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e8f05-127">[Önceki](drag-and-drop-via-reorderlist-cs.md)
> [İleri](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e8f05-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
