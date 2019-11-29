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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611382"
---
# <a name="using-postbacks-with-reorderlist-c"></a>ReorderList ile Geri Gönderme Kullanma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)

> AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar. Liste yeniden sıralandığında, bir geri gönderme değişikliğin sunucusunu bilgilendirir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde `ReorderList` denetimi, Kullanıcı tarafından sürükleme ve bırakma yoluyla yeniden sıralanabilir bir liste sağlar. Liste yeniden sıralandığında, bir geri gönderme değişikliğin sunucusunu bilgilendirir.

## <a name="steps"></a>Adımlar

`ReorderList` denetimi için birkaç olası veri kaynağı vardır. Bunlardan biri `XmlDataSource` bir denetim kullanmaktır:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

Bu XML 'i bir `ReorderList` denetimine bağlamak ve geri gönderileri etkinleştirmek için aşağıdaki özniteliklerin ayarlanması gerekir:

- `DataSourceID`: veri kaynağının KIMLIĞI
- `SortOrderField`: sıralama yapılacak Özellik
- `AllowReorder`: kullanıcının liste öğelerini yeniden sıralayıp izin verip vermediği
- `PostBackOnReorder`: liste yeniden düzenlendiğinde geri gönderme oluşturulup oluşturulmayacağını belirtir

Denetim için uygun biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

`ReorderList` denetimi içinde, veri kaynağındaki belirli veriler `Eval()` yöntemi kullanılarak bağlanabilir:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

Sayfada rastgele bir konumda, son yeniden sipariş oluştuğunda bir etiket bilgileri tutar:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

Bu etiket, geri gönderme işlemi için sunucu tarafı kodundaki metinle doldurulmuştur:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

Son olarak, ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada yer almalıdır:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

[Her yeniden sıralama ![geri gönderme tetikler](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

Her yeniden sıralama bir geri göndermeyi tetikler ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-postbacks-with-reorderlist-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](drag-and-drop-via-reorderlist-cs.md)
