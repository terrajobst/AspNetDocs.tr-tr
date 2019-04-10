---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: (VB) bir listeden animasyon seçme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Framework ayrıca ver...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 7d8807962e5cf668358e03821d5fd3bf755a0e7d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418891"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a>Bir Listeden Animasyon Seçme (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)

> ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Framework, bir listeden animasyon animasyon, bazı JavaScript kodları değerlendirmesine bağlı olarak çekmek Programcı de sağlar.


## <a name="overview"></a>Genel Bakış

ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Framework, bir listeden animasyon animasyon, bazı JavaScript kodları değerlendirmesine bağlı olarak çekmek Programcı de sağlar.

## <a name="steps"></a>Adımlar

İlk olarak dahil `ScriptManager` sayfasında; ardından, ASP.NET AJAX kitaplığı, Denetim Araç Seti kullanmayı mümkün hale yüklenir:

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

Animasyonun bir panel şuna benzer metin uygulanır:

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

İlişkili CSS sınıfı paneli için iyi bir arka plan rengi tanımlayın ve ayrıca panelinin sabit genişlikte ayarlayın:

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

Ardından, ekleme `AnimationExtender` sayfasına sağlayan bir `ID`, `TargetControlID` özniteliği ve bömesinde `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

İçinde `<Animations>` düğümü, kullanım `<OnLoad>` animasyonları sayfanın tam yüklü silindikten sonra çalıştırılacak. Normal animasyonları birini yerine `<Case>` öğesi oyuna gelir. Kendi SelectScript özniteliğinin değerini değerlendirilir; dönüş değeri sayısal olmalıdır. Bu sayı, içinde subanimations birine bağlı olarak &lt;çalışması&gt; yürütülür. Denetim Araç Seti SelectScript 2 olarak değerlendirilirse, üçüncü animasyon içinde örneği için çalışan &lt;çalışması&gt; (sayım 0 başlar).

Aşağıdaki biçimlendirmede üç subanimations tanımlar: Genişlik, yükseklik yeniden boyutlandırma ve netleştirme yeniden boyutlandırma. JavaScript kodu (`Math.floor(3 * Math.random())`) üç animasyonları birini çalıştırın, ardından 0. ve 2 arasında bir sayı seçer:

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]


[![Oolası üç animasyonları, KD: Panel geniş alır](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)

Olası üç animasyonları biri: Panel geniş alır ([tam boyutlu görüntüyü görmek için tıklatın](picking-one-animation-out-of-a-list-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](animation-depending-on-a-condition-vb.md)
> [İleri](animating-in-response-to-user-interaction-vb.md)
