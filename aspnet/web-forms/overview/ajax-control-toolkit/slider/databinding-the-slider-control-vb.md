---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: Kaydırıcı denetimini veri bağlama (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Geçerli pozitif durumlar bağlamak mümkündür...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598291"
---
# <a name="databinding-the-slider-control-vb"></a>Kaydırıcı Denetiminde Veri Bağlama (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)

> AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcısının geçerli konumunu başka bir ASP.NET denetimine bağlamak mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcısının geçerli konumunu başka bir ASP.NET denetimine bağlamak mümkündür.

## <a name="steps"></a>Adımlar

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

Sonra, sayfaya iki `TextBox` denetimi ekleyin. Biri bir grafik kaydırıcısının içine dönüştürülecek ve diğeri kaydırıcının konumunu tutacaktır.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

Sonraki adım zaten son adımdır. ASP.NET AJAX denetim araç setinde `SliderExtender` denetimi, ilk metin kutusunun bir kaydırıcısını açar ve kaydırıcı konumu değiştiğinde ikinci metin kutusunu otomatik olarak güncelleştirir. Bunun çalışması için, `SliderExtender``TargetControlID` özniteliği ilk metin kutusunun KIMLIĞI olarak ayarlanmalıdır; `BoundControlID` özniteliğin ikinci metin kutusunun KIMLIĞINE ayarlanması gerekir.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

Tarayıcıda görebileceğiniz gibi, veri bağlama her iki yönde de çalışacaktır: metin kutusuna yeni bir değer girildiğinde kaydırıcının konumunu günceller. İkinci metin kutusunu salt okunurdur yaparsanız, metin alanına zayıf bir koruma ekleyebilirsiniz, böylece Kullanıcı burada değeri el ile güncelleştirebilir.

[![kaydırıcı ve metin kutusu eşitlenmiş](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

Kaydırıcı ve metin kutusu eşitlenmiş ([tam boyutlu görüntüyü görüntülemek Için tıklayın](databinding-the-slider-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](using-the-slider-control-with-auto-postback-vb.md)
