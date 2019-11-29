---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: Parolanın gücünü test etme (VB) | Microsoft Docs
author: wenz
description: Parolaların neredeyse her yerde olması gerekir; böylece yavaş kullanıcılar, kolayca kesintiye uğramaları kolay olan basit parolalar seçlidirler. ASP. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: b614e1788eeafc175dd792ec6d3e4619f9ea2b7a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606241"
---
# <a name="testing-the-strength-of-a-password-vb"></a>Bir Parolanın Güçlülüğünü Test Etme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)

> Parolaların neredeyse her yerde olması gerekir; böylece yavaş kullanıcılar, kolayca kesintiye uğramaları kolay olan basit parolalar seçlidirler. ASP.NET AJAX denetim araç setinde Passwordkuvveti denetimi bir parolanın ne kadar iyi olduğunu denetleyebilir.

## <a name="overview"></a>Genel bakış

Parolaların neredeyse her yerde olması gerekir; böylece yavaş kullanıcılar, kolayca kesintiye uğramaları kolay olan basit parolalar seçlidirler. ASP.NET AJAX denetim araç setinde `PasswordStrength` denetimi bir parolanın ne kadar iyi olduğunu denetleyebilir.

## <a name="steps"></a>Adımlar

`PasswordStrength` denetimi bir metin kutusunu genişletir ve içindeki parolanın yeterince iyi olup olmadığını denetler. Öznitelikler aracılığıyla çok sayıda seçenek sunar; Bunlardan bazıları şunlardır:

- Parolada gereken en az sayısal karakter sayısı `MinimumNumericCharacters`
- Parolada gereken en az sayıda simge karakteri (harf ve rakam değil) `MinimumSymbolCharacters`
- en az parola uzunluğu `PreferredPasswordLength`
- parolanın hem büyük hem de küçük harf karakter kullanması gerekip gerekmediğini `RequiresUpperAndLowerCaseCharacters`

`StrengthIndicatorType`, metin (değer `"Text"`) veya bir tür ilerleme çubuğu (değer `"BarIndicator"`) olarak parolanın gücünü sunma bilgilerini sağlar. `DisplayPosition` özniteliğinde, bilgilerin nerede göründüğünü yapılandırırsınız. Burada, ASP.NET AJAX `ScriptManager` denetimi, `PasswordStrength` denetimi ve kurs, kullanıcının bir parola girebileceği bir metin kutusu gibi bir örnek verilmiştir. Tanıtım için ikinci form alanı, bir parola alanı değil normal metin alanıdır ve bu sayede, yazarken geliştirme sırasında bakabilirsiniz.

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

Sayfayı çalıştırın ve dışarıda yazın: yalnızca küçük harfler, büyük harfler, rakamlar ve semboller girdikten sonra parola ayırıcı olarak kabul edilir.

[parolayı artık (oldukça) iyi ![](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

Artık parola (oldukça) iyi ([tam boyutlu görüntüyü görüntülemek Için tıklatın](testing-the-strength-of-a-password-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](testing-the-strength-of-a-password-cs.md)
