---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: (VB) bir UpdatePanel denetimine animasyon ekleme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. İçeriği için bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: a7c40ebe359e21602d9f1de8205e1a7c808acc85
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59384259"
---
# <a name="animating-an-updatepanel-control-vb"></a>Bir UpdatePanel Denetimine Animasyon Ekleme (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)

> ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. UpdatePanel içeriğini için yoğun animasyon framework kullanan özel genişletici var: UpdatePanelAnimation. Bu öğreticide, bu tür animasyonu UpdatePanel için ayarlanacak gösterilmektedir.


## <a name="overview"></a>Genel Bakış

ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. İçeriği için bir `UpdatePanel`, yoğun animasyon framework kullanan özel genişletici var: `UpdatePanelAnimation`. Bu öğreticide gibi animasyon için ayarlama işlemi gösterilmektedir bir `UpdatePanel`.

## <a name="steps"></a>Adımlar

İlk adım zamanki dahil etmektir `ScriptManager` sayfasında ASP.NET AJAX kitaplığı yüklenir ve Denetim Araç Seti kullanılabilir:

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

Bu senaryoda animasyon için bir ASP.NET uygulanacak `Wizard` bulunan web denetimi bir `UpdatePanel`. (İsteğe bağlı) üç adım geri göndermeler tetiklemek için yeterli seçenekleri sağlar:

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

İşaretleme için gerekli `UpdatePanelAnimationExtender` denetimi için kullanılan biçimlendirme oldukça benzer `AnimationExtender`. İçinde `TargetControlID` sağladığımız özniteliği `ID` , `UpdatePanel` animasyon uygulamak için; içinde `UpdatePanelAnimationExtender` denetimi `<Animations>` öğesi XML biçimlendirme için animation(s) tutar. Ancak bir fark vardır: Comparison için olaylar ve olay işleyicileri miktarı sınırlıdır `AnimationExtender`. İçin `UpdatePanels`, yalnızca iki tanesi var:

- `<OnUpdated>` UpdatePanel ne zaman güncelleştirildiğini
- `<OnUpdating>` UpdatePanel güncelleştirme başladığında

Bu senaryoda, yeni içeriği `UpdatePanel` (sonra geri gönderme) belirerek. Bu, için gerekli biçimlendirme.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

Bir geri gönderme UpdatePanel içinde olduğunda, artık yeni panel içerikleri yavaşça.


[![Sonraki sihirbaz adımı Soluklaşan](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)

Sonraki sihirbaz adımı Soluklaşan ([tam boyutlu görüntüyü görmek için tıklatın](animating-an-updatepanel-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](changing-an-animation-using-client-side-code-vb.md)
> [İleri](dynamically-controlling-updatepanel-animations-vb.md)
