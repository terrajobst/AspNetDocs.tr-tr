---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: (VB) istemci kodundan DropShadow özelliklerini düzenleme | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti DropShadow denetiminde gölge paneliyle genişletir. Bu genişletici özelliklerini kullanarak istemci JavaScrip da değiştirilebilir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: c9b0946568063b9e5cf1454bd7a57c43304c3543
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59390317"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a>İstemci Kodundan DropShadow Özelliklerini Düzenleme (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)

> AJAX Denetim Araç Seti DropShadow denetiminde gölge paneliyle genişletir. Bu genişletici özelliklerinin, istemci JavaScript kodunu kullanarak da değiştirilebilir.


## <a name="overview"></a>Genel Bakış

AJAX Denetim Araç Seti DropShadow denetiminde gölge paneliyle genişletir. Bu genişletici özelliklerinin, istemci JavaScript kodunu kullanarak da değiştirilebilir.

## <a name="steps"></a>Adımlar

Kod, bazı satırlık metin içeren bir paneli ile başlar:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

İlişkili CSS sınıfının Masası iyi arka plan rengi verir:

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

`DropShadowExtender` Panel gölge etkisi, % 50 olarak belirlenmiş opaklık ile genişletmek için eklenir:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

Ardından, ASP.NET AJAX `ScriptManager` denetimi çalışmak Denetim Araç Seti sağlar:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

Başka bir panel gölge opaklığını ayarlamak için iki JavaScript bağlantılar içeriyor: eksi bağlantı gölgenin opaklık azaltır, artı bağlantıyı da artar.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

JavaScript işlevinin `changeOpacity()` sonra ilk bulmalıdır `DropShadowExtender` sayfasında denetimi. ASP.NET AJAX tanımlar `$find()` tam olarak bu görev için yöntemi. Ardından, `get_Opacity()` yöntemi geçerli opaklığını alır `set_Opacity()` yöntemini ayarlar. JavaScript kodu ardından geçerli opaklık değerini geçirir `<label>` öğe:

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]


[![İstemci tarafında opaklık değiştirilir](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)

İstemci tarafında opaklık değiştirildiğinde ([tam boyutlu görüntüyü görmek için tıklatın](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](adjusting-the-z-index-of-a-dropshadow-vb.md)
