---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: Sunucu tarafında animasyonları değiştirme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonlar de olabilir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598002"
---
# <a name="modifying-animations-from-the-server-side-vb"></a>Sunucu tarafında animasyonları değiştirme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonlar Ayrıca sunucu tarafında değişebilir

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonlar Ayrıca sunucu tarafında değişebilir

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

Kodun geri kalanı sunucu tarafında çalışır ve biçimlendirme kullanmaz; Bunun yerine, `AnimationExtender` denetimini oluşturmak için kodu kullanır:

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

Ancak, Denetim araç seti Şu anda bireysel animasyonları oluşturmak için bir API erişimi sağlamıyor. Ancak, `AnimationExtender`animasyonları özelliğini, animasyonları bildirimli olarak atarken kullanılan XML işaretlemesini içeren bir dizeye ayarlamak mümkündür. `<Animations>` öğesi içermemesi gereken XML oluşturmak için, .NET Framework XML desteğini veya aşağıdaki kodda olduğu gibi, yalnızca dizeyi sağlamanız gerekir:

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

Son olarak, `<form runat="server">` öğesi içindeki geçerli sayfaya `AnimationExtender` denetimini ekleyin, böylece animasyon dahil edildiğinden ve çalıştığından emin olun:

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

[![animasyonu, sunucu tarafı C#/vb kodu kullanılarak oluşturulur](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)

Animasyon, sunucu tarafı C#/vb kodu kullanılarak oluşturulur ([tam boyutlu görüntüyü görüntülemek için tıklayın](modifying-animations-from-the-server-side-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](triggering-an-animation-in-another-control-vb.md)
> [İleri](executing-animations-using-client-side-code-vb.md)
