---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: ReorderList ile geri göndermeler kullanma (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar. Liste yeniden düzenlendiğinde bir Po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: f83201fc6fd458e730b6bb5ffee184d303b52e90
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627234"
---
# <a name="using-postbacks-with-reorderlist-c"></a><span data-ttu-id="c136d-104">ReorderList ile Geri Gönderme Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="c136d-104">Using Postbacks with ReorderList (C#)</span></span>

<span data-ttu-id="c136d-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="c136d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c136d-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c136d-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span></span>

> <span data-ttu-id="c136d-107">AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="c136d-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="c136d-108">Liste yeniden sıralandığında, bir geri gönderme değişikliğin sunucusunu bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="c136d-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="c136d-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="c136d-109">Overview</span></span>

<span data-ttu-id="c136d-110">AJAX denetim araç setinde `ReorderList` denetimi, Kullanıcı tarafından sürükleme ve bırakma yoluyla yeniden sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="c136d-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="c136d-111">Liste yeniden sıralandığında, bir geri gönderme değişikliğin sunucusunu bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="c136d-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="c136d-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="c136d-112">Steps</span></span>

<span data-ttu-id="c136d-113">`ReorderList` denetimi için birkaç olası veri kaynağı vardır.</span><span class="sxs-lookup"><span data-stu-id="c136d-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="c136d-114">Bunlardan biri `XmlDataSource` bir denetim kullanmaktır:</span><span class="sxs-lookup"><span data-stu-id="c136d-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="c136d-115">Bu XML 'i bir `ReorderList` denetimine bağlamak ve geri gönderileri etkinleştirmek için aşağıdaki özniteliklerin ayarlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="c136d-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="c136d-116">`DataSourceID`: veri kaynağının KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="c136d-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="c136d-117">`SortOrderField`: sıralama yapılacak Özellik</span><span class="sxs-lookup"><span data-stu-id="c136d-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="c136d-118">`AllowReorder`: kullanıcının liste öğelerini yeniden sıralayıp izin verip vermediği</span><span class="sxs-lookup"><span data-stu-id="c136d-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="c136d-119">`PostBackOnReorder`: liste yeniden düzenlendiğinde geri gönderme oluşturulup oluşturulmayacağını belirtir</span><span class="sxs-lookup"><span data-stu-id="c136d-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="c136d-120">Denetim için uygun biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c136d-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="c136d-121">`ReorderList` denetimi içinde, veri kaynağındaki belirli veriler `Eval()` yöntemi kullanılarak bağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="c136d-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

<span data-ttu-id="c136d-122">Sayfada rastgele bir konumda, son yeniden sipariş oluştuğunda bir etiket bilgileri tutar:</span><span class="sxs-lookup"><span data-stu-id="c136d-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="c136d-123">Bu etiket, geri gönderme işlemi için sunucu tarafı kodundaki metinle doldurulmuştur:</span><span class="sxs-lookup"><span data-stu-id="c136d-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

<span data-ttu-id="c136d-124">Son olarak, ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada yer almalıdır:</span><span class="sxs-lookup"><span data-stu-id="c136d-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

<span data-ttu-id="c136d-125">[Her yeniden sıralama ![geri gönderme tetikler](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c136d-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="c136d-126">Her yeniden sıralama bir geri göndermeyi tetikler ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-postbacks-with-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c136d-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c136d-127">Next</span><span class="sxs-lookup"><span data-stu-id="c136d-127">Next</span></span>](drag-and-drop-via-reorderlist-cs.md)
