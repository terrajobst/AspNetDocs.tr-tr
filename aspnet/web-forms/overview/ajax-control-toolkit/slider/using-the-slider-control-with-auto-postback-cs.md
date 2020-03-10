---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: Otomatik geri gönderme (C#) Ile kaydırıcı denetimini kullanma | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcı için bir oto gönder...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553622"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a>Otomatik geri gönderme (C#) Ile kaydırıcı denetimini kullanma

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)

> AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcıyı, değeri değiştiğinde AutoPostBack hale getirmek mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcıyı, değeri değiştiğinde AutoPostBack hale getirmek mümkündür.

## <a name="steps"></a>Adımlar

Kaydırıcıyı bir değişikliğe göre otomatik olarak geri göndermeye olanak tanımak için, her iki metin kutusu da `AutoPostBack="true"`: kaydırıcı olacak metin kutusu ve kaydırıcının konumunu tutan metin kutusu. Bunun için gereken biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

ASP.NET AJAX denetim araç setinde `SliderExtender` denetimi, kaydırıcı işlevlerini iki metin kutusuna atar:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

Daha sonra bir geri gönderme kullanıcıyı bilgilendirmek için ek bir etiket öğesi kullanılacaktır:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

Son olarak, ASP.NET AJAX 'un `ScriptManager` denetimi, Denetim araç seti 'nin çalışması için gerekli JavaScript 'ı yükler:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

Artık kaydırıcı geri gönderilir; sunucu tarafında bu olay yakalanıp şu şekilde olabilir:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

[kaydırıcıyı taşımak ![bir geri gönderme tetikler](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)

Kaydırıcıyı hareket ettirmek bir geri gönderme tetikliyor ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-the-slider-control-with-auto-postback-cs/_static/image3.png))

[daha sonra ![, bu değişikliğin tarihi etikette yazılır](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)

Daha sonra, bu değişikliğin tarihi etikette yazılır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-the-slider-control-with-auto-postback-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Next](databinding-the-slider-control-cs.md)
