---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: Başka bir denetimde animasyon tetikleme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Genellikle, bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536073"
---
# <a name="triggering-an-animation-in-another-control-vb"></a>Başka bir Denetimde Animasyon Tetikleme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Genellikle, bir animasyon başlatmak Kullanıcı etkileşimi tarafından aynı denetimle tetiklenir. Bununla birlikte, bir denetimle etkileşim kurmak ve daha sonra başka bir denetimi animasyon eklemek de mümkündür.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Genellikle, bir animasyon başlatmak Kullanıcı etkileşimi tarafından aynı denetimle tetiklenir. Bununla birlikte, bir denetimle etkileşim kurmak ve daha sonra başka bir denetimi animasyon eklemek de mümkündür.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

Panelin animasyon bölmesine başlamak için bir HTML düğmesi kullanılır. Kullanıcı söz konusu düğmeye tıkladığında geri gönderme istemediğimiz için, `<input type="button" />` `<asp:Button />` üzerinde favoured olduğunu unutmayın.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

Daha sonra, `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak `AnimationExtender` sayfaya ekleyin. Düğmenin kimliğine (animasyonu tetikleyen öğe) değil, panelin kimliğine `TargetControlID` ayarlanması önemlidir (canlandırılan öğe)

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

`<Animations>` düğümü içinde, animasyonları her zamanki gibi yerleştirin. Düğmeleri değil, panelin değiştirilmesini sağlamak için, `AnimationExtender`içindeki her animasyon öğesi için `AnimationTarget` özniteliğini ayarlayın. `AnimationTarget` değeri, kursun panelin KIMLIĞIDIR. Bu şekilde, animasyonlar tetikleyici düğmesiyle değil, panel ile gerçekleşir. Bu senaryo için `AnimationExtender` biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

Bireysel animasyonların göründüğü özel sıralamayı aklınızda yapın. Birincisi, animasyon çalıştıktan sonra düğme devre dışı bırakılır. `<EnableAction>` öğesinde `AnimationTarget` özniteliği olmadığından, bu animasyon kaynak denetimine uygulanır: düğme. Sonraki iki animasyon adımı paralel (`<Parallel>` öğe) olarak uygulanır. Her ikisinin de `AnimationTarget` öznitelikleri `"Panel1"`olarak ayarlanmıştır, böylece düğme değil paneli canlandırın.

[düğme üzerinde fare tıklaması ![panel animasyonunu başlatır](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

Düğmeye tıkladığınızda fare tıklaması panel animasyonunu başlatır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](triggering-an-animation-in-another-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](disabling-actions-during-animation-vb.md)
> [İleri](modifying-animations-from-the-server-side-vb.md)
