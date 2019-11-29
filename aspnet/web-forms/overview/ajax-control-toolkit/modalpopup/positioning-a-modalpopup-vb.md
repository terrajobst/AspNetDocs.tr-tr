---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: Bir ModalPopup konumlandırma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak denetim bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: fb79a08a339588ed8adc4b4236911819ea9286b4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598983"
---
# <a name="positioning-a-modalpopup-vb"></a>Bir ModalPopup’ı Konumlandırma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)

> AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak denetim, açılan pencereyi konumlandırmak için yerleşik bir işlevsellik sunmaz.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak denetim, açılan pencereyi konumlandırmak için yerleşik bir işlevsellik sunmaz.

## <a name="steps"></a>Adımlar

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için `ScriptManager`. Denetim, sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin. Açılan pencereyi kapatmak için bir düğme kullanılır:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

Açılan pencere her gösterildiğinde sayfada belirli bir yerde konumlandırılmalıdır. Bu görev için, istemci tarafı bir JavaScript işlevi oluşturulur. Önce panele erişmeyi dener. Bu işlem başarılı olursa, panelin konumu CSS ve JavaScript kullanılarak ayarlanır (açılan menünün konumunu ' de değiştirin). Ancak `ModalPopupExtender` denetimi de açılan pencereyi konumlandırmaya çalışır. Bu nedenle, JavaScript kodu bir saniyede her onuncu açılan pencereyi sürekli konumlandırır.

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

Gördüğünüz gibi, JavaScript yönteminin dönüş `setTimeout()` değeri genel bir değişkende kaydedilir. Bu, `clearTimeout()` yöntemi kullanılarak, isteğe bağlı açılan pencerenin tekrarlanmış konumunu durdurmaya izin verir:

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

Artık her şey, her zaman uygun olduğunda tarayıcının bu işlevleri çağırmasını sağlamak için kullanılabilir. Düğme tıklandığında paneli tetikleyen `movePanel()` JavaScript işlevi çağrılmalıdır:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

`stopMoving()` işlevi, açılan pencere kapatıldığında oynat ' a gelir ve bu, `ModalPopupExtender` denetiminde tetiklenebilir:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]

[![, belirlenen konumda kalıcı açılan pencere görüntülenir](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)

Belirlenen konumda kalıcı açılan pencere görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](positioning-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](handling-postbacks-from-a-modalpopup-vb.md)
