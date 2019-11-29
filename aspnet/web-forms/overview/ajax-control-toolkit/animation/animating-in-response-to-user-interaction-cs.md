---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: Kullanıcı etkileşimine (C#) yanıt olarak animasyon ekleme | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonlar yıldız alabilir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599868"
---
# <a name="animating-in-response-to-user-interaction-c"></a>Kullanıcı Etkileşimine Karşılık Olarak Animasyon Ekleme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonlar otomatik olarak başlayabilir veya Kullanıcı etkileşimi tarafından, ör. fareyle tıklanarak tetiklenebilir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonlar otomatik olarak başlayabilir veya Kullanıcı etkileşimi tarafından, ör. fareyle tıklanarak tetiklenebilir.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

`<Animations>` düğümü içinde, animasyonu Kullanıcı etkileşimi aracılığıyla başlatmaya yönelik beş yol vardır (eksik öğe, tüm sayfa tam olarak yüklendikten sonra yürütülür `<OnLoad>`):

- `<OnClick>` (denetime fare tıklaması)
- `<OnHoverOut>` (fare, denetimi bırakır)
- `<OnHoverOver>` (fare bir denetimin üzerine geldiğinde `<OnHoverOut>` animasyonunu durduruyor)
- `<OnMouseOut>` (fare bir denetimi bırakır)
- `<OnMouseOver>` (fare, bir denetimin üzerine geldiğinde `<OnMouseOut>` animasyonunu durdurmaz)

Bu senaryoda `<OnClick>` kullanılır. Kullanıcı panele tıkladığında, yeniden boyutlandırılır ve aynı anda silinir.

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

[fare tıklaması ![animasyonu başlatır](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

Fare tıklaması animasyonu başlatır ([tam boyutlu görüntüyü görüntülemek Için tıklatın](animating-in-response-to-user-interaction-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](picking-one-animation-out-of-a-list-cs.md)
> [İleri](disabling-actions-during-animation-cs.md)
