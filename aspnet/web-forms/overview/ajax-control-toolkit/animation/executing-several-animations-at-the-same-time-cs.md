---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: Aynı anda birkaç animasyon yürütme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu, Severa 'yi çalıştırmaya izin verir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598121"
---
# <a name="executing-several-animations-at-the-same-time-c"></a>Aynı anda birkaç animasyon yürütme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)

> ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Paralel bir biçimde birkaç animasyonun çalıştırılmasına izin verir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Paralel bir biçimde birkaç animasyonun çalıştırılmasına izin verir.

## <a name="steps"></a>Adımlar

Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

Animasyon, şunun gibi görünen bir metin paneline uygulanır:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory `runat="server"`sağlayarak sayfaya `AnimationExtender` ekleyin:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

`<Animations>` düğümü içinde, sayfa tam olarak yüklendikten sonra animasyonları çalıştırmak için `<OnLoad>` kullanın. Genellikle `<OnLoad>` yalnızca bir animasyon kabul eder. Animasyon çerçevesi, `<Parallel>` öğesini kullanarak çeşitli animasyonları tek tek birleştirkullanmanıza olanak sağlar. `<Parallel>` içerisindeki tüm animasyonlar aynı anda yürütülür.

Bu, `AnimationExtender` denetimi için olası bir biçimlendirme, paneli kullanıma alma ve aynı anda yeniden boyutlandırma:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

Gerçekten: bu betiği çalıştırdığınızda panel görüntülenir, daha sonra yeniden boyutlandırır (genişliği solından ve yüksekliğinin sonunda olacak şekilde) ve aynı anda aşağı çıkar.

[![bölmenin genişleme ve yeniden boyutlandırılması (tarayıcının işleme altyapısı sayesinde, içeriği dahil)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)

Panel, soluklaşmakta ve yeniden boyutlandırılıyor (tarayıcının işleme altyapısında teşekkürler, içeriği dahil) ([tam boyutlu görüntüyü görüntülemek Için tıklayın](executing-several-animations-at-the-same-time-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](adding-animation-to-a-control-cs.md)
> [İleri](executing-several-animations-after-each-other-cs.md)
