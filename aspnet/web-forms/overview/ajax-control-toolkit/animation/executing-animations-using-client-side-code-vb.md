---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: Istemci tarafı kod kullanarak animasyonları yürütme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon yürütme...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575508"
---
# <a name="executing-animations-using-client-side-code-vb"></a>Animasyonları İstemci Tarafı Kod Kullanarak Yürütme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon yürütme, özel istemci tarafı JavaScript kodu kullanılarak da tetiklenebilir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon yürütme, özel istemci tarafı JavaScript kodu kullanılarak da tetiklenebilir.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

`<Animations>` düğümü içinde Kullanıcı panele tıkladıktan sonra animasyonları çalıştırmak için `<OnClick>` kullanın. Paralel olarak yürütülecek iki animasyon ekleyin:

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

Tanıtım için, bu animasyon (ve Denetim araç seti kullanılarak oluşturulan diğer animasyonlar), sayfa çalıştıktan sonra JavaScript kodu kullanılarak yürütülür. Tüm bunların ilki `AnimationExtender` denetimine erişmesi gerekir. ASP.NET AJAX kitaplığı bu görev için `$find()` işlevi sağlar:

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

`AnimationExtender` denetimi, XML biçimlendirmesinde kullanılan olay işleyicileriyle aynı adlara sahip yöntemler de dahil olmak üzere zengin bir API 'yi kullanıma sunar: `OnClick()`, `OnLoad()`, vb. Örneğin, `OnClick()` yönteminin bir çağrısı, animasyonu `AnimationExtender` denetiminin `<OnClick>` öğesi içinde yürütür:

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

Bu, sayfa tam olarak yüklendikten sonra, sayfa ve dahil edilen tüm JavaScript kitaplıkları yüklendikten sonra, ASP.NET AJAX tarafından çağrılan `pageLoad()` işlevi adının kullanıldığına ilişkin tam istemci tarafı JavaScript kodu ' nu aşağıda bulabilirsiniz.

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

[animasyon, fare tıklaması olmadan hemen çalıştırılır ![](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)

Animasyon hemen çalışır, fare tıklaması olmadan ([tam boyutlu görüntüyü görüntülemek Için tıklatın](executing-animations-using-client-side-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](modifying-animations-from-the-server-side-vb.md)
> [İleri](changing-an-animation-using-client-side-code-vb.md)
