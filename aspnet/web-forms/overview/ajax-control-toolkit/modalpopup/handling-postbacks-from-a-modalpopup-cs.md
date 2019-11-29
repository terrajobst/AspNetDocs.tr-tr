---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: ModalPopup (C#) Ile geri göndermeler işleme Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Bir POS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599093"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a>ModalPopup’tan Gelen Geri Göndermeleri İşleme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)

> AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Açılan pencere içinden bir geri gönderme oluşturulduğunda özel dikkatli olunmalıdır.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Açılan pencere içinden bir geri gönderme oluşturulduğunda özel dikkatli olunmalıdır.

## <a name="steps"></a>Adımlar

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin. Bu şekilde, Kullanıcı bir ad ve e-posta adresi girebilir. Açılan pencereyi kapatmak ve bilgileri kaydetmek için bir düğme kullanılır. `OnClick` özniteliğinin, bu düğmeye tıklandığında geri gönderme işleminin gerçekleşmesini sağlamak için ayarlandığını unutmayın:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

Sayfanın kendisi tam olarak aynı bilgiler için iki etiketten oluşur: ad ve e-posta adresi. Kalıcı açılan pencereyi tetiklemek için bir düğme kullanılır:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

Açılan pencerenin görünmesini sağlamak için `ModalPopupExtender` denetimini ekleyin. `PopupControlID` özniteliğini bölmenin KIMLIĞINE ayarlayın ve düğmenin KIMLIĞINE `TargetControlID`:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

Artık, kalıcı açılan pencerenin içindeki `Save` düğmesine tıklandığında, sunucu tarafı `SaveData()` yöntemi yürütülür. Burada, girilen verileri bir veri deposuna kaydedebilirsiniz. Basitlik sağlamak için yeni veriler yalnızca etiketin çıktıdır:

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

Ayrıca, kalıcı açılan pencerede bulunan TextBox denetimleri geçerli ad ve e-posta ile doldurulmalıdır. Ancak bu yalnızca geri gönderme gerçekleşmediğinde gereklidir. Bir geri gönderme işlemi varsa, ASP.NET ViewState özelliği, metin kutularını uygun değerlerle otomatik olarak doldurur.

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

[![kalıcı açılan pencere geri göndermeye neden olur](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)

Kalıcı açılan pencere geri göndermeye neden olur ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](using-modalpopup-with-a-repeater-control-cs.md)
> [İleri](positioning-a-modalpopup-cs.md)
