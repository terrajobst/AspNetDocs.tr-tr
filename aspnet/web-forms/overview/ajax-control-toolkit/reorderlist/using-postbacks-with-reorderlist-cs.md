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
# <a name="using-postbacks-with-reorderlist-c"></a>ReorderList ile Geri Gönderme Kullanma (C#)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)

> AJAX Denetim Araç Seti ReorderList denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar. Listeyi yeniden olduğunda, bir geri gönderme sunucunun değişikliği bildirmek.


## <a name="overview"></a>Genel Bakış

`ReorderList` AJAX Denetim Araç Seti denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar. Listeyi yeniden olduğunda, bir geri gönderme sunucunun değişikliği bildirmek.

## <a name="steps"></a>Adımlar

Birkaç olası veri kaynağı için `ReorderList` denetimi. Biridir kullanmak için bir `XmlDataSource` denetimi:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

Bu XML bağlamak amacıyla bir `ReorderList` denetimi ve etkinleştirme Geri göndermeler, aşağıdaki öznitelikleri ayarlanmalıdır:

- `DataSourceID`: Veri kaynağı kimliği
- `SortOrderField`: Sıralama ölçütü olarak özelliği
- `AllowReorder`: Liste öğeleri yeniden sıralamak kullanıcı izin verilip verilmeyeceğini
- `PostBackOnReorder`: Listenin düzenlenmeyecek her bir geri gönderme oluşturulup oluşturulmayacağını

Denetim için uygun biçimlendirmesi şöyledir:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

İçinde `ReorderList` denetimi, veri kaynağındaki belirli veri bağımlı kullanarak `Eval()` yöntemi:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

Son yeniden sıralama oluştuğunda rastgele bir konumda sayfasında, bilgileri bir etiket tutar:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

Bu etiket, metin işleme geri gönderme sunucu tarafı kodu ile doldurulur:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

Son olarak, ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` sayfada denetim yerleştirin:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]


[![Bir geri gönderme tetikleyen her yeniden sıralama](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

Bir geri gönderme her sipariş tetikler ([tam boyutlu görüntüyü görmek için tıklatın](using-postbacks-with-reorderlist-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](drag-and-drop-via-reorderlist-cs.md)
