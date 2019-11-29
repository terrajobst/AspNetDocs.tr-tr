---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: Otomatik geri gönderme Ile kaydırıcı denetimini kullanma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcı için bir oto gönder...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598531"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a>Otomatik geri gönderme Ile kaydırıcı denetimini kullanma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)

> AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcıyı, değeri değiştiğinde AutoPostBack hale getirmek mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcıyı, değeri değiştiğinde AutoPostBack hale getirmek mümkündür.

## <a name="steps"></a>Adımlar

Kaydırıcıyı bir değişikliğe göre otomatik olarak geri göndermeye olanak tanımak için, her iki metin kutusu da `AutoPostBack="true"`: kaydırıcı olacak metin kutusu ve kaydırıcının konumunu tutan metin kutusu. Bunun için gereken biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

ASP.NET AJAX denetim araç setinde `SliderExtender` denetimi, kaydırıcı işlevlerini iki metin kutusuna atar:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

Daha sonra bir geri gönderme kullanıcıyı bilgilendirmek için ek bir etiket öğesi kullanılacaktır:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

Son olarak, ASP.NET AJAX 'un `ScriptManager` denetimi, Denetim araç seti 'nin çalışması için gerekli JavaScript 'ı yükler:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

Artık kaydırıcı geri gönderilir; sunucu tarafında bu olay yakalanıp şu şekilde olabilir:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

[kaydırıcıyı taşımak ![bir geri gönderme tetikler](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)

Kaydırıcıyı hareket ettirmek bir geri gönderme tetikliyor ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-the-slider-control-with-auto-postback-vb/_static/image3.png))

[daha sonra ![, bu değişikliğin tarihi etikette yazılır](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)

Daha sonra, bu değişikliğin tarihi etikette yazılır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-the-slider-control-with-auto-postback-vb/_static/image6.png))

> [!div class="step-by-step"]
> [Önceki](databinding-the-slider-control-cs.md)
> [İleri](databinding-the-slider-control-vb.md)
