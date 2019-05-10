---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: UpdatePanel animasyonlarını (VB) dinamik olarak denetleme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. İçeriği için bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 136e265f36a49a1d3ed41d2a998c395fd2c4fd32
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128724"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a>UpdatePanel Animasyonlarını Dinamik Olarak Denetleme (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)

> ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. UpdatePanel içeriğini için yoğun animasyon framework kullanan özel genişletici var: UpdatePanelAnimation. Ayrıca, UpdatePanel tetikleyicilerini birlikte de çalışabilir.

## <a name="overview"></a>Genel Bakış

ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. İçeriği için bir `UpdatePanel`, yoğun animasyon framework kullanan özel genişletici var: `UpdatePanelAnimation`. Ayrıca ile birlikte çalışabilir `UpdatePanel` tetikler.

## <a name="steps"></a>Adımlar

İlk adım zamanki dahil etmektir `ScriptManager` sayfasında ASP.NET AJAX kitaplığı yüklenir ve Denetim Araç Seti kullanılabilir:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

Bu senaryoda animasyon geçerli zaman bir ekrana uygulanır. Bu bilgileri kullanarak bir etiket yazılabilir `Page_Load()` yöntemi veya aşağıdaki satır içi kod (basitleştirmek amacıyla) kullanılır:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

Ayrıca, bir düğme tetikleyicisi sürekli güncelleştirmek için oluşturulur:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

Bu kod içine yerleştirilir `<ContentTemplate>` bölümünü bir `UpdatePanel` öğesi. Bölmenin `UpdateMode` özniteliği ayarlanmalıdır `"Conditional"`, olduğundan yalnızca Tetikleyicileri bölmenin içeriği güncelleştirebilir. İçinde `<Triggers>` bölümünü `UpdatePanel`, bir zaman uyumsuz geri gönderme tetikleyici oluşturulur ve bağlı `Click` düğmesinin olayı. Bu nedenle, kullanıcı düğmesine tıklarsa `UpdatePanel` yenilenir. İçin biçimlendirme şöyledir `UpdatePanel` denetimi:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

Son olarak, `UpdatePanelAnimationExtender` yapılandırılması gerekir: Ayarlama `TargetControlID` özniteliği panel Kimliğine ve bir animasyon Genişleticisi içinde tanımlayın. Soluklaşan yapar güncelleştirilmiş zaman iyi bir visual indirimlere oluşturan mantıklı. Ardından, genişletici biçimlendirme şöyle görünebilir:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

Dosyayı tarayıcıda çalıştırın. Düğmeye tıklattığınızda, geçerli zamanı her zaman bir saniye boyunca Soldurma panelinde gösterilir.

[![Geçerli saati Soluklaşan](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)

Geçerli saati Soluklaşan ([tam boyutlu görüntüyü görmek için tıklatın](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](animating-an-updatepanel-control-vb.md)
