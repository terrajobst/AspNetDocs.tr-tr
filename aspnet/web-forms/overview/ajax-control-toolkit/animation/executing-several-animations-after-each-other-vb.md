---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: Birbirinden sonra birkaç animasyon yürütme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu, Severa 'yi çalıştırmaya izin verir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606896"
---
# <a name="executing-several-animations-after-each-other-vb"></a>Arka Arkaya Birkaç Animasyon Yürütme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bunlardan daha sonra birkaç animasyon çalıştırmasına izin verir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bunlardan daha sonra birkaç animasyon çalıştırmasına izin verir.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory sağlayarak sayfaya `AnimationExtender` ekleyin `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

`<Animations>` düğümü içinde, sayfa tam olarak yüklendikten sonra animasyonları çalıştırmak için `<OnLoad>` kullanın. Genellikle `<OnLoad>` yalnızca bir animasyon kabul eder. Animasyon çerçevesi, `<Sequence>` öğesini kullanarak çeşitli animasyonları tek tek birleştirkullanmanıza olanak sağlar. `<Sequence>` içindeki tüm animasyonlar, bunlardan sonra yürütülür. `AnimationExtender` denetimi için olası bir biçimlendirme aşağıda verilmiştir, önce paneli daha geniş yapıp yüksekliğini azaltır:

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

Bu betiği çalıştırdığınızda panel önce daha geniş ve daha küçük olur.

[Ilk ![genişlik artırıldı](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)

İlk genişlik artmıştır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](executing-several-animations-after-each-other-vb/_static/image3.png))

[![yükseklik azaltılır](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)

Sonra Yükseklik azaltılır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](executing-several-animations-after-each-other-vb/_static/image6.png))

> [!div class="step-by-step"]
> [Önceki](executing-several-animations-at-the-same-time-vb.md)
> [İleri](animation-depending-on-a-condition-vb.md)
