---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: Bir koşula bağlı animasyon (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonun olup olmadığı...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598352"
---
# <a name="animation-depending-on-a-condition-c"></a>Bir Koşula Bağlı Animasyon (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir animasyonun çalıştırılıp çalıştırılmayacağı veya yüklenmediğini, bazı JavaScript kodu biçimindeki bir koşula de bağlı olabilir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir animasyonun çalıştırılıp çalıştırılmayacağı veya yüklenmediğini, bazı JavaScript kodu biçimindeki bir koşula de bağlı olabilir.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory sağlayarak sayfaya `AnimationExtender` ekleyin `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

`<Animations>` düğümü içinde, sayfa tam olarak yüklendikten sonra animasyonları çalıştırmak için `<OnLoad>` kullanın. `<Condition>` öğesi, normal animasyonlardan biri yerine yürütmeye gelir. `ConditionScript` özniteliğinin değeri olarak belirtilen JavaScript kodu çalışma zamanında yürütülür. True olarak değerlendirilirse animasyon yürütülür, aksi takdirde değildir. Aşağıdaki biçimlendirme, her biri rastgele bir durum olan %50 ' de yürütülen iki animasyon sağlar. `<OnLoad>`içinde yalnızca bir animasyon olabileceğinden, iki `<Condition>` animasyonları `<Sequence>` öğesi kullanılarak birlikte birleştirilir:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

`ConditionScript` özniteliğinde küçüktür işareti (`<`) kaçışın () olması gerektiğini unutmayın. Bu betiği çalıştırdığınızda, herhangi bir animasyon çalıştırması ya da iki ya da her ikisi de olamaz.

[![panel, yeniden boyutlandırmadan soluklaşmakta, bu nedenle ikinci animasyon çalışır, ilki](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)

Panel, yeniden boyutlandırmadan soluklaşmakta, bu nedenle ikinci animasyon çalışır, ilki değil ([tam boyutlu görüntüyü görüntülemek Için tıklatın](animation-depending-on-a-condition-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](executing-several-animations-after-each-other-cs.md)
> [İleri](picking-one-animation-out-of-a-list-cs.md)
