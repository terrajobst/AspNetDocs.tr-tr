---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: ModalPopup 'dan geri göndermeler işleme (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Bir POS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: df0b71b3e336a0d230869623473bdac24b3dd07b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606613"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a>ModalPopup’tan Gelen Geri Göndermeleri İşleme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)

> AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Açılan pencere içinden bir geri gönderme oluşturulduğunda özel dikkatli olunmalıdır.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Açılan pencere içinden bir geri gönderme oluşturulduğunda özel dikkatli olunmalıdır.

## <a name="steps"></a>Adımlar

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin. Bu şekilde, Kullanıcı bir ad ve e-posta adresi girebilir. Açılan pencereyi kapatmak ve bilgileri kaydetmek için bir düğme kullanılır. `OnClick` özniteliğinin, bu düğmeye tıklandığında geri gönderme işleminin gerçekleşmesini sağlamak için ayarlandığını unutmayın:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

Sayfanın kendisi tam olarak aynı bilgiler için iki etiketten oluşur: ad ve e-posta adresi. Kalıcı açılan pencereyi tetiklemek için bir düğme kullanılır:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

Açılan pencerenin görünmesini sağlamak için `ModalPopupExtender` denetimini ekleyin. `PopupControlID` özniteliğini bölmenin KIMLIĞINE ayarlayın ve düğmenin KIMLIĞINE `TargetControlID`:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

Artık, kalıcı açılan pencerenin içindeki `Save` düğmesine tıklandığında, sunucu tarafı `SaveData()` yöntemi yürütülür. Burada, girilen verileri bir veri deposuna kaydedebilirsiniz. Basitlik sağlamak için yeni veriler yalnızca etiketin çıktıdır:

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

Ayrıca, kalıcı açılan pencerede bulunan TextBox denetimleri geçerli ad ve e-posta ile doldurulmalıdır. Ancak bu yalnızca geri gönderme gerçekleşmediğinde gereklidir. Bir geri gönderme işlemi varsa, ASP.NET ViewState özelliği, metin kutularını uygun değerlerle otomatik olarak doldurur.

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

[![kalıcı açılan pencere geri göndermeye neden olur](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)

Kalıcı açılan pencere geri göndermeye neden olur ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](using-modalpopup-with-a-repeater-control-vb.md)
> [İleri](positioning-a-modalpopup-vb.md)
