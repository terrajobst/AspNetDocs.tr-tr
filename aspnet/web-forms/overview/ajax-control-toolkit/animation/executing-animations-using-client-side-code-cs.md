---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: Istemci tarafı kodu kullanarak animasyonları yürütme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon yürütme...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: b6ba1553b9c8c51d5d6ae1679e53f9cc1d17b769
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598184"
---
# <a name="executing-animations-using-client-side-code-c"></a>Animasyonları İstemci Tarafı Kod Kullanarak Yürütme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon yürütme, özel istemci tarafı JavaScript kodu kullanılarak da tetiklenebilir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon yürütme, özel istemci tarafı JavaScript kodu kullanılarak da tetiklenebilir.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

`<Animations>` düğümü içinde Kullanıcı panele tıkladıktan sonra animasyonları çalıştırmak için `<OnClick>` kullanın. Paralel olarak yürütülecek iki animasyon ekleyin:

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

Tanıtım için, bu animasyon (ve Denetim araç seti kullanılarak oluşturulan diğer animasyonlar), sayfa çalıştıktan sonra JavaScript kodu kullanılarak yürütülür. Tüm bunların ilki `AnimationExtender` denetimine erişmesi gerekir. ASP.NET AJAX kitaplığı bu görev için `$find()` işlevi sağlar:

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

`AnimationExtender` denetimi, XML biçimlendirmesinde kullanılan olay işleyicileriyle aynı adlara sahip yöntemler de dahil olmak üzere zengin bir API 'yi kullanıma sunar: `OnClick()`, `OnLoad()`, vb. Örneğin, `OnClick()` yönteminin bir çağrısı, animasyonu `AnimationExtender` denetiminin `<OnClick>` öğesi içinde yürütür:

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

Bu, sayfa tam olarak yüklendikten sonra, sayfa ve dahil edilen tüm JavaScript kitaplıkları yüklendikten sonra, ASP.NET AJAX tarafından çağrılan `pageLoad()` işlevi adının kullanıldığına ilişkin tam istemci tarafı JavaScript kodu ' nu aşağıda bulabilirsiniz.

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]

[animasyon, fare tıklaması olmadan hemen çalıştırılır ![](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)

Animasyon hemen çalışır, fare tıklaması olmadan ([tam boyutlu görüntüyü görüntülemek Için tıklatın](executing-animations-using-client-side-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](modifying-animations-from-the-server-side-cs.md)
> [İleri](changing-an-animation-using-client-side-code-cs.md)
