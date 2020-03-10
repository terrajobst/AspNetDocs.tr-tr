---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: Metin kutusunda yalnızca belirli karakterlere izin verme (C#) | Microsoft Docs
author: wenz
description: ASP.NET doğrulama denetimleri, Kullanıcı girişinde yalnızca belirli karakterlere izin verildiğinden emin olabilir. Ancak bu, hala kullanıcıların geçersiz yazmalarını engellemez...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: d1e367becd574e31d24fca8545f76b1ed3c4d85e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554238"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a>Bir Metin Kutusunda Yalnızca Belirli Karakterlere İzin Verme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)

> ASP.NET doğrulama denetimleri, Kullanıcı girişinde yalnızca belirli karakterlere izin verildiğinden emin olabilir. Ancak bu, kullanıcıların geçersiz karakter yazmalarını ve formu göndermeye çalışmamasını engellemez.

## <a name="overview"></a>Genel bakış

ASP.NET doğrulama denetimleri, Kullanıcı girişinde yalnızca belirli karakterlere izin verildiğinden emin olabilir. Ancak bu, kullanıcıların geçersiz karakter yazmalarını ve formu göndermeye çalışmamasını engellemez.

## <a name="steps"></a>Adımlar

ASP.NET AJAX denetim araç seti, bir metin kutusunu genişleten `FilteredTextBox` denetimini içerir. Etkinleştirildikten sonra alana yalnızca belirli bir karakter kümesi girilebilir.

Bunun çalışması için, önce ASP.NET AJAX denetim araç seti tarafından da kullanılan JavaScript kitaplıklarını yükleyen ASP.NET AJAX `ScriptManager` her zamanki gibi gerekir:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

Ardından, bir metin kutusu gereklidir:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

Son olarak, `FilteredTextBoxExtender` denetimi kullanıcının yazmasının izin verdiği karakterlerin kısıtlanması durumunda olur. İlk olarak, `TargetControlID` özniteliğini `TextBox` denetiminin `ID` ayarlayın. Ardından, kullanılabilir `FilterType` değerlerinden birini seçin:

- `Custom` varsayılan; geçerli karakterlerin bir listesini sağlamanız gerekir
- yalnızca küçük harf `LowercaseLetters`
- yalnızca `Numbers` rakamları
- yalnızca büyük harfler `UppercaseLetters`

`Custom FilterType` kullanılırsa, `ValidChars` özelliği ayarlanmalıdır ve yazılabilir olabilecek karakterlerin bir listesini sağlamalıdır. Şu şekilde: metin kutusuna metin yapıştırmaya çalışırsanız, tüm geçersiz karakterler kaldırılır.

Yalnızca rakama izin veren `FilteredTextBoxExtender` denetimine yönelik biçimlendirme (`FilterType="Numbers"`da olabilecek bir şey) vardır:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

Sayfayı çalıştırın ve JavaScript etkinse bir harf girmeyi deneyin; bu işlem çalışmaz; sayılar, sayfada görüntülenir. Ancak, koruma `FilteredTextBox`, hiçbir madde işareti-kanıtı değildir: JavaScript etkinse, metin kutusuna herhangi bir veri girilebilir, bu nedenle ek doğrulama (örn. ASP) kullanmanız gerekir. NET 'in doğrulama denetimleri.

[![yalnızca rakamlar girilebilir](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)

Yalnızca rakamlar girilebilir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](allowing-only-certain-characters-in-a-text-box-vb.md)
