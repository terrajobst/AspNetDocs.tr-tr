---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: UpdatePanel denetimine animasyon ekleme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir... öğesinin içeriği için
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536381"
---
# <a name="animating-an-updatepanel-control-c"></a>Bir UpdatePanel Denetimine Animasyon Ekleme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir UpdatePanel 'ın içeriği için animasyon çerçevesinde yoğun bir şekilde yararlanan özel bir genişletici vardır: UpdatePanelAnimation. Bu öğreticide, bir UpdatePanel için böyle bir animasyonun nasıl ayarlanacağı gösterilmektedir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir `UpdatePanel`içeriği için animasyon çerçevesine yoğun bir şekilde dayanan özel bir genişletici vardır: `UpdatePanelAnimation`. Bu öğreticide, `UpdatePanel`için bu animasyonun nasıl ayarlanacağı gösterilmektedir.

## <a name="steps"></a>Adımlar

İlk adım, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için sayfaya `ScriptManager` dahil etmek için her zamanki gibidir:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

Bu senaryodaki animasyon, bir `UpdatePanel`bulunan bir ASP.NET `Wizard` Web denetimine uygulanır. Üç (rastgele) adım geri gönderileri tetiklemeye yetecek kadar seçenek sağlar:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

`UpdatePanelAnimationExtender` denetimi için gereken biçimlendirme, `AnimationExtender`kullanılan biçimlendirmeye oldukça benzerdir. `TargetControlID` özniteliğinde, hareketlendirmek için `UpdatePanel` `ID` sağlıyoruz; `UpdatePanelAnimationExtender` denetimi içinde, `<Animations>` öğesi animasyon (ler) için XML biçimlendirmesi barındırır. Ancak bir farklılık vardır: olayların miktarı ve olay işleyicileri `AnimationExtender`karşılaştırma ile sınırlıdır. `UpdatePanels`için, bunlardan yalnızca ikisi mevcuttur:

- UpdatePanel güncelleştirildiği zaman `<OnUpdated>`
- UpdatePanel güncelleştirmeye başladığında `<OnUpdating>`

Bu senaryoda, `UpdatePanel` (geri gönderimin ardından) yeni içerikleri soluklaşır. Bunun için gereken biçimlendirme budur:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

Artık UpdatePanel içinde bir geri gönderme gerçekleşdiğinde, panelin yeni içerikleri düzgün şekilde zayıflaşır.

[Sonraki sihirbaz adımının ![](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

Sonraki sihirbaz adımı ([tam boyutlu görüntüyü görüntülemek Için tıklayın](animating-an-updatepanel-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](changing-an-animation-using-client-side-code-cs.md)
> [İleri](dynamically-controlling-updatepanel-animations-cs.md)
