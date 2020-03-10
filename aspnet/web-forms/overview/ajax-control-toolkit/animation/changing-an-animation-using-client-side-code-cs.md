---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: Istemci tarafı kod kullanarak bir animasyonu değiştirme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon Ayrıca,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598219"
---
# <a name="changing-an-animation-using-client-side-code-c"></a>İstemci Tarafı Kod Kullanarak Bir Animasyonu Değiştirme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon özel istemci tarafı JavaScript kodu kullanılarak da değiştirilebilir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyon özel istemci tarafı JavaScript kodu kullanılarak da değiştirilebilir.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

Gerçek animasyon bir HTML düğmesi tarafından başlatılır:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

`AnimationExtender` denetiminde `<Animations>` düğüm olmadığını unutmayın. Özel JavaScript kodu, denetimle birlikte kullanılacak animasyonları sağlamak için kullanılır.

`AnimationExtender`sunucu API 'sinde olduğu gibi, henüz Extender 'a animasyon atamak için kolay bir yol yoktur. Ancak, Extender çeşitli olaylara (`OnClick`, `OnLoad`vb.) kayıtlı animasyonları okumak ve yazmak için çeşitli yöntemler sunar. İşte bazı örnekler:

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

`get_*()` işlevlerinin dönüş değeri ve `set_*()` işlevlerinin bağımsız değişkeninin biçimi, XML biçimlendirmesinin ne olacağını gösteren bir nesne gösterimi sağlayan bir JSON dizesidir. Şu anda ' de bir nesne geçirmenin bir yolu yoktur, ancak belirli bir animasyondan (`get_OnXXXBehavior()` Yöntemler) bir nesneyi okumak mümkündür.

Bu, düğme tarafından tetiklenen bir animasyonu temsil eden bir JSON dizesi (sınırlandırma tırnak işaretleri olmadan ve düzgün biçimlendirilmeksizin), ancak yeniden boyutlandırılırken ve aynı zamanda onu kaldırarak panele animasyon uygulayarak paneli canlandırdığında:

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

Aşağıdaki JavaScript kodu, bu JSON descripöğesini geçerli genişleticin `OnClick` animasyonuna atar ve bunu çalıştırır:

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

[animasyon hemen, fare tıklaması olmadan (ve çok az biçimlendirme ile) çalışır ![](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)

Animasyon hemen, fare tıklaması olmadan (çok az biçimlendirme ile) çalışır ([tam boyutlu görüntüyü görüntülemek Için tıklatın](changing-an-animation-using-client-side-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](executing-animations-using-client-side-code-cs.md)
> [İleri](animating-an-updatepanel-control-cs.md)
