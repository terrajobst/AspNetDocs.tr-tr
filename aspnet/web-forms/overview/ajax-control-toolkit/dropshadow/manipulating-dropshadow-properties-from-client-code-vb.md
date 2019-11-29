---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: Istemci kodundan DropShadow özelliklerini düzenleme (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir. Bu genişleticin özellikleri, istemci Javano kullanılarak da değiştirilebilir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574025"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a>İstemci Kodundan DropShadow Özelliklerini Düzenleme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)

> AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir. Bu genişleticin özellikleri, istemci JavaScript kodu kullanılarak da değiştirilebilir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir. Bu genişleticin özellikleri, istemci JavaScript kodu kullanılarak da değiştirilebilir.

## <a name="steps"></a>Adımlar

Kod, bazı metin satırları içeren bir panelle başlar:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

İlişkili CSS sınıfı, paneli iyi bir arka plan rengi sağlar:

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

`DropShadowExtender`, paneli bir gölge efektiyle genişletmek için eklenir, opaklık %50 olarak ayarlanmıştır:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

Ardından, ASP.NET AJAX `ScriptManager` denetimi denetim araç setinin çalışmasını sağlar:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

Diğer bir panel, gölge geçirgenliğini ayarlamak için iki JavaScript bağlantısı içerir: eksi bağlantı, gölgenin saydamlığını düşürür, artı bağlantısı onu arttırır.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

JavaScript işlevi `changeOpacity()` önce sayfada `DropShadowExtender` denetimini bulmalıdır. ASP.NET AJAX, tam olarak bu görevin `$find()` yöntemini tanımlar. Ardından `get_Opacity()` yöntemi geçerli opaklığı alır, `set_Opacity()` yöntemi bunu ayarlar. JavaScript kodu daha sonra `<label>` öğesinde geçerli opaklık değerini koyar:

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

[![opaklık istemci tarafında değiştirildi](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)

Opaklık, istemci tarafında değişir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](adjusting-the-z-index-of-a-dropshadow-vb.md)
