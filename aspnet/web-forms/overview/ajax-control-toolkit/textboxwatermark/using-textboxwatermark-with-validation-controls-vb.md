---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: Doğrulama denetimleriyle Textboxfiligran kullanma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde Textboxfiligran denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir. Bir Kullanıcı, kutuya tıkladığında ben...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 141cae26c9e52be510e2a5a8f816cbac977dcf3d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627045"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>Doğrulama Denetimleri ile TextBoxWatermark Kullanma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> AJAX denetim araç setinde Textboxfiligran denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir. Kullanıcı, kutuya tıkladığında boşaltılır. Kullanıcı metin girmeden kutudan ayrılsa, önceden doldurulmuş metin yeniden görüntülenir. Bu, aynı sayfada ASP.NET doğrulama denetimleriyle çakışmayabilir, ancak bu sorunlar ele alınabilir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde `TextBoxWatermark` denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir. Kullanıcı, kutuya tıkladığında boşaltılır. Kullanıcı metin girmeden kutudan ayrılsa, önceden doldurulmuş metin yeniden görüntülenir. Bu, aynı sayfada ASP.NET doğrulama denetimleriyle çakışmayabilir, ancak bu sorunlar ele alınabilir.

## <a name="steps"></a>Adımlar

Örneğin temel kurulumu aşağıda verilmiştir: bir `TextBox` denetim, bir `TextBoxWatermarkExtender` denetimi kullanılarak işaretlenir. Bir düğme geri göndermeyi tetikler ve daha sonra sayfadaki doğrulama denetimlerini tetiklemek için kullanılacaktır. Ayrıca, ASP.NET AJAX 'u başlatmak için bir `ScriptManager` denetimi gereklidir:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

Şimdi, form gönderildiğinde alanda metin olup olmadığını denetleyen `RequiredFieldValidator` bir denetim ekleyin. Doğrulayıcının `InitialValue` özelliği, `TextBoxWatermarkExtender` denetiminde kullanılan değere ayarlanmalıdır: form gönderildiğinde, değiştirilmemiş bir metin kutusunun değeri, içindeki filigran değeridir:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

Bununla birlikte, bu yaklaşımda bir sorun var: istemci JavaScript 'ı devre dışı bırakrsa, metin alanı filigran metniyle önceden doldurulmamışsa `RequiredFieldValidator` bir hata mesajı tetiklemez. Bu nedenle, boş bir metin kutusunu (`InitialValue` özniteliğini atlayarak) denetleyen ikinci bir `RequiredFieldValidator` denetimi gereklidir.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

Her iki doğrulayıcılar de `Display`=`"Dynamic"`kullandığından, Son Kullanıcı iki doğrulayıcıların harekete geçirildiği görsel görünümü ayırt edemez; Bunun yerine, bunlardan yalnızca biri vardı.

Son olarak, bir hata iletisi verildiyse, alandaki metnin çıktısını almak için bazı sunucu tarafı kod ekleyin:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

[Doğrulayıcı ![alanda metin yok](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

Doğrulayıcı, alanda metin yok ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](using-textboxwatermark-in-a-formview-vb.md)
