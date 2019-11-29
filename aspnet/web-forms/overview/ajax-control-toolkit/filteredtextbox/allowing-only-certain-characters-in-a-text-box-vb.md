---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: Metin kutusunda yalnızca belirli karakterlere izin verme (VB) | Microsoft Docs
author: wenz
description: ASP.NET doğrulama denetimleri, Kullanıcı girişinde yalnızca belirli karakterlere izin verildiğinden emin olabilir. Ancak bu, hala kullanıcıların geçersiz yazmalarını engellemez...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 895708ebecc30c5f35e6ecd0349604bb777cbd93
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74573936"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a>Bir Metin Kutusunda Yalnızca Belirli Karakterlere İzin Verme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)

> ASP.NET doğrulama denetimleri, Kullanıcı girişinde yalnızca belirli karakterlere izin verildiğinden emin olabilir. Ancak bu, kullanıcıların geçersiz karakter yazmalarını ve formu göndermeye çalışmamasını engellemez.

## <a name="overview"></a>Genel bakış

ASP.NET doğrulama denetimleri, Kullanıcı girişinde yalnızca belirli karakterlere izin verildiğinden emin olabilir. Ancak bu, kullanıcıların geçersiz karakter yazmalarını ve formu göndermeye çalışmamasını engellemez.

## <a name="steps"></a>Adımlar

ASP.NET AJAX denetim araç seti, bir metin kutusunu genişleten `FilteredTextBox` denetimini içerir. Etkinleştirildikten sonra alana yalnızca belirli bir karakter kümesi girilebilir.

Bunun çalışması için, önce ASP.NET AJAX denetim araç seti tarafından da kullanılan JavaScript kitaplıklarını yükleyen ASP.NET AJAX `ScriptManager` her zamanki gibi gerekir:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

Ardından, bir metin kutusu gereklidir:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

Son olarak, `FilteredTextBoxExtender` denetimi kullanıcının yazmasının izin verdiği karakterlerin kısıtlanması durumunda olur. İlk olarak, `TargetControlID` özniteliğini `TextBox` denetiminin `ID` ayarlayın. Ardından, kullanılabilir `FilterType` değerlerinden birini seçin:

- `Custom` varsayılan; geçerli karakterlerin bir listesini sağlamanız gerekir
- yalnızca küçük harf `LowercaseLetters`
- yalnızca `Numbers` rakamları
- yalnızca büyük harfler `UppercaseLetters`

`Custom FilterType` kullanılırsa, `ValidChars` özelliği ayarlanmalıdır ve yazılabilir olabilecek karakterlerin bir listesini sağlamalıdır. Şu şekilde: metin kutusuna metin yapıştırmaya çalışırsanız, tüm geçersiz karakterler kaldırılır.

Yalnızca rakama izin veren `FilteredTextBoxExtender` denetimine yönelik biçimlendirme (`FilterType="Numbers"`da olabilecek bir şey) vardır:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

Sayfayı çalıştırın ve JavaScript etkinse bir harf girmeyi deneyin; bu işlem çalışmaz; sayılar, sayfada görüntülenir. Ancak, koruma `FilteredTextBox`, hiçbir madde işareti-kanıtı değildir: JavaScript etkinse, metin kutusuna herhangi bir veri girilebilir, bu nedenle ek doğrulama (örn. ASP) kullanmanız gerekir. NET 'in doğrulama denetimleri.

[![yalnızca rakamlar girilebilir](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)

Yalnızca rakamlar girilebilir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](allowing-only-certain-characters-in-a-text-box-cs.md)
