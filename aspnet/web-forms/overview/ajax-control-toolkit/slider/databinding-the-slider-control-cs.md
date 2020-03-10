---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: Kaydırıcı denetimini (C#) DataBinding | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Geçerli pozitif durumlar bağlamak mümkündür...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ef547573f17f3265ad72717d3d3bbc622fd6894e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553720"
---
# <a name="databinding-the-slider-control-c"></a>Kaydırıcı Denetiminde Veri Bağlama (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)

> AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcısının geçerli konumunu başka bir ASP.NET denetimine bağlamak mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde kaydırıcı denetimi, fare kullanılarak denetlenebilecek bir grafik kaydırıcı sağlar. Kaydırıcısının geçerli konumunu başka bir ASP.NET denetimine bağlamak mümkündür.

## <a name="steps"></a>Adımlar

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

Sonra, sayfaya iki `TextBox` denetimi ekleyin. Biri bir grafik kaydırıcısının içine dönüştürülecek ve diğeri kaydırıcının konumunu tutacaktır.

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

Sonraki adım zaten son adımdır. ASP.NET AJAX denetim araç setinde `SliderExtender` denetimi, ilk metin kutusunun bir kaydırıcısını açar ve kaydırıcı konumu değiştiğinde ikinci metin kutusunu otomatik olarak güncelleştirir. Bunun çalışması için, `SliderExtender``TargetControlID` özniteliği ilk metin kutusunun KIMLIĞI olarak ayarlanmalıdır; `BoundControlID` özniteliğin ikinci metin kutusunun KIMLIĞINE ayarlanması gerekir.

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

Tarayıcıda görebileceğiniz gibi, veri bağlama her iki yönde de çalışacaktır: metin kutusuna yeni bir değer girildiğinde kaydırıcının konumunu günceller. İkinci metin kutusunu salt okunurdur yaparsanız, metin alanına zayıf bir koruma ekleyebilirsiniz, böylece Kullanıcı burada değeri el ile güncelleştirebilir.

[![kaydırıcı ve metin kutusu eşitlenmiş](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)

Kaydırıcı ve metin kutusu eşitlenmiş ([tam boyutlu görüntüyü görüntülemek Için tıklayın](databinding-the-slider-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](using-the-slider-control-with-auto-postback-cs.md)
> [İleri](using-the-slider-control-with-auto-postback-vb.md)
