---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: Animasyon sırasında eylemleri devre dışı bırakma (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Ayrıca eylemi destekler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536241"
---
# <a name="disabling-actions-during-animation-vb"></a>Animasyon Sırasında Eylemleri Devre Dışı Bırakma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Ayrıca, fare tıklamaları gibi eylemleri de destekler. Ancak fare tıklaması bir animasyon başlattığında animasyon sırasında fare tıklamalarını devre dışı bırakmak tercih edilir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Ayrıca, fare tıklamaları gibi eylemleri de destekler. Ancak fare tıklaması bir animasyon başlattığında animasyon sırasında fare tıklamalarını devre dışı bırakmak tercih edilir.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

Animasyon, şöyle bir HTML düğmesine uygulanacak:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

Bir Web denetimi yerine bir HTML denetimi kullanıldığını unutmayın; bu, düğmenin geri gönderme oluşturmasını istemedik; Yalnızca bizim için istemci tarafı animasyonunu başlatacaktır.

Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

`<Animations>` düğümü içinde, `<OnClick>` fare tıklamasını işlemek için doğru öğedir. Ancak, düğme animasyon sırasında da tıklanmalıdır. `<EnableAction>` öğesi bundan yararlanabilir. `Enabled="false"` ayarlamak, animasyonun bir parçası olarak düğmeyi devre dışı bırakır. Birkaç ayrı animasyon (düğmeyi ve gerçek animasyonları devre dışı bırakarak) kullandığından `<Parallel>` öğesi, tek animasyonları bir araya birleştirmek için gereklidir. `AnimationExtender`için tüm biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

Ayrıca, listenin sonunda aşağıdaki XML öğesini kullanarak Animasyondan sonra düğme için yeniden etkinleştirmek mümkün olacaktır:

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

Ancak verilen senaryoda, düğme silinerek ve animasyonun sonunda görünmediğinden bu durum gereksizdir.

[![animasyon çalıştıktan hemen sonra düğme devre dışı bırakılır](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)

Animasyon çalıştıktan hemen sonra düğme devre dışı bırakılır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](disabling-actions-during-animation-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](animating-in-response-to-user-interaction-vb.md)
> [İleri](triggering-an-animation-in-another-control-vb.md)
