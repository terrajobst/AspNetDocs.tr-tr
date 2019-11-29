---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: Bir denetime animasyon ekleme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu öğreticide nasıl yapılacağı gösterilmektedir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: dd63157fe616c5f6874b7cca11f4ede15018df04
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607105"
---
# <a name="adding-animation-to-a-control-c"></a>Bir Denetime Animasyon Ekleme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu öğreticide, bu tür bir animasyonun nasıl ayarlanacağı gösterilmektedir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu öğreticide, bu tür bir animasyonun nasıl ayarlanacağı gösterilmektedir.

## <a name="steps"></a>Adımlar

İlk adım, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için sayfaya `ScriptManager` dahil etmek için her zamanki gibidir:

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

Bu senaryodaki animasyon şuna benzer bir metin paneline uygulanacak:

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfı, arka plan rengini ve genişliğini tanımlar:

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

Bir sonraki adımda `AnimationExtender`ihtiyacımız var. Bir `ID` ve olağan `runat="server"`sağladıktan sonra, `TargetControlID` özniteliği bizim örneğimizde animasyon uygulamak için denetime ayarlanmalıdır:

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

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

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

Bu komut dosyasını çalıştırdığınızda, panel görüntülenir ve bir ve yarım saniye aşağı silinerek belirir.

[Panel ![](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)

Panel soluklaşma ([tam boyutlu görüntüyü görüntülemek Için tıklayın](adding-animation-to-a-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](executing-several-animations-at-the-same-time-cs.md)
