---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: Bir denetime animasyon ekleme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu öğreticide nasıl yapılacağı gösterilmektedir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607170"
---
# <a name="adding-animation-to-a-control-vb"></a>Bir Denetime Animasyon Ekleme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu öğreticide, bu tür bir animasyonun nasıl ayarlanacağı gösterilmektedir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu öğreticide, bu tür bir animasyonun nasıl ayarlanacağı gösterilmektedir.

## <a name="steps"></a>Adımlar

İlk adım, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için sayfaya `ScriptManager` dahil etmek için her zamanki gibidir:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

Bu senaryodaki animasyon şuna benzer bir metin paneline uygulanacak:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfı, arka plan rengini ve genişliğini tanımlar:

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

Bir sonraki adımda `AnimationExtender`ihtiyacımız var. Bir `ID` ve olağan `runat="server"`sağladıktan sonra, `TargetControlID` özniteliği bizim örneğimizde animasyon uygulamak için denetime ayarlanmalıdır:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

Tüm animasyon bildirimli olarak Visual Studio 'nun IntelliSense tarafından tam olarak desteklenmeyen bir XML sözdizimi kullanılarak uygulanır. Kök düğüm bu düğüm dahilinde `<Animations>;`, animasyon (ler) ne zaman olacağını belirleyen çeşitli olaylara izin verilir:

- `OnClick` (fare tıklaması)
- `OnHoverOut` (fare bir denetimden çıktığında)
- `OnHoverOver` (fare bir denetimin üzerine geldiğinde `OnHoverOut` animasyonunu durduruyor)
- `OnLoad` (sayfa yüklendiğinde)
- `OnMouseOut` (fare bir denetimden çıktığında)
- `OnMouseOver` (fare, bir denetimin üzerine geldiğinde `OnMouseOut` animasyonunu durdurmadan)

Çerçeve, her biri kendi XML öğesiyle temsil edilen bir animasyon kümesiyle gelir. İşte bir seçim:

- `<Color>` (rengi değiştirme)
- `<FadeIn>` (Soluklaşan)
- `<FadeOut>` (Soluklaşan)
- `<Property>` (denetimin özelliğini değiştirme)
- `<Pulse>` (pulsating)
- `<Resize>` (boyutu değiştirme)
- `<Scale>` (boyutunu orantılı olarak değiştirme)

Bu örnekte, panel soluklaşır. Animasyon 1,5 saniye (`Duration` özniteliği) sürer ve saniyede 24 kare (animasyon adımları) (`Fps` özniteliği) görüntüler. `AnimationExtender` denetimi için tüm biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

Bu komut dosyasını çalıştırdığınızda, panel görüntülenir ve bir ve yarım saniye aşağı silinerek belirir.

[Panel ![](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

Panel soluklaşma ([tam boyutlu görüntüyü görüntülemek Için tıklayın](adding-animation-to-a-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](dynamically-controlling-updatepanel-animations-cs.md)
> [İleri](executing-several-animations-at-the-same-time-vb.md)
