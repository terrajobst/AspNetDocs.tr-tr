---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: UpdatePanel animasyonlarını dinamik olarak denetlemeC#() | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir... öğesinin içeriği için
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536206"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a>UpdatePanel Animasyonlarını Dinamik Olarak Denetleme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir UpdatePanel 'ın içeriği için animasyon çerçevesinde yoğun bir şekilde yararlanan özel bir genişletici vardır: UpdatePanelAnimation. Ayrıca, UpdatePanel tetikleyicilerle birlikte çalışabilir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir `UpdatePanel`içeriği için animasyon çerçevesine yoğun bir şekilde dayanan özel bir genişletici vardır: `UpdatePanelAnimation`. Ayrıca, `UpdatePanel` tetikleyicilerle birlikte çalışabilir.

## <a name="steps"></a>Adımlar

İlk adım, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için sayfaya `ScriptManager` dahil etmek için her zamanki gibidir:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

Bu senaryodaki animasyon geçerli saatin görüntüsüne uygulanır. Bu bilgiler `Page_Load()` yöntemi kullanılarak bir etikete yazılabilir veya (basitlik sağlamak için) aşağıdaki satır içi kod kullanılır:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

Ayrıca, zaman güncellemenin tetiklenmesi için bir düğme oluşturulur:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

Bu kod daha sonra bir `UpdatePanel` öğesinin `<ContentTemplate>` bölümüne konur. Panelin `UpdateMode` özniteliği `"Conditional"`olarak ayarlanmalıdır, çünkü yalnızca Tetikleyiciler panelin içeriğini güncelleştirebilir. `UpdatePanel``<Triggers>` bölümünde, zaman uyumsuz bir geri gönderme tetikleyicisi oluşturulur ve düğmenin `Click` olayına bağlanır. Bu nedenle, Kullanıcı düğmeye tıkladığında `UpdatePanel` yenilenir. `UpdatePanel` denetimi için biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

Son olarak, `UpdatePanelAnimationExtender` yapılandırılması gerekir: `TargetControlID` özniteliğini panelin KIMLIĞI olarak ayarlayın ve Extender içinde bir animasyon tanımlayın. ' Deki soldurma, güncelleştirilmiş sürede iyi bir görsel vurgu oluşturan anlamda anlamlı hale gelir. Daha sonra genişletici biçimlerinizin şöyle görünebiliriz:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

Dosyayı tarayıcıda çalıştırın. Düğmeye tıkladığınızda, geçerli saat panelde gösterilir, her zaman bir saniye boyunca geçişi yapılır.

[geçerli zaman ![](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)

Şu anki Saat Soldurma ([tam boyutlu görüntüyü görüntülemek Için tıklayın](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](animating-an-updatepanel-control-cs.md)
> [İleri](adding-animation-to-a-control-vb.md)
