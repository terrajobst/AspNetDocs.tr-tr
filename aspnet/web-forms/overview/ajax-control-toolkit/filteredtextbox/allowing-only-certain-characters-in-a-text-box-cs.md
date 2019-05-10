---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: Bir metin kutusu (C#) yalnızca belirli karakterlere izin verme | Microsoft Docs
author: wenz
description: Doğrulama denetimleri ASP.NET uygulamasında kullanıcı girdisi yalnızca belirli karakterlere izin verildiğini emin olabilirsiniz. Ancak bu yazmaya geçersiz kullanıcılar hala engellemez...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: 4a3a743eef80d74d37be772ea70ac609028090ee
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108451"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a>Bir Metin Kutusunda Yalnızca Belirli Karakterlere İzin Verme (C#)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)

> Doğrulama denetimleri ASP.NET uygulamasında kullanıcı girdisi yalnızca belirli karakterlere izin verildiğini emin olabilirsiniz. Ancak bu kullanıcıların geçersiz karakterleri yazmaya ve form göndermeye devam engellemez.

## <a name="overview"></a>Genel Bakış

Doğrulama denetimleri ASP.NET uygulamasında kullanıcı girdisi yalnızca belirli karakterlere izin verildiğini emin olabilirsiniz. Ancak bu kullanıcıların geçersiz karakterleri yazmaya ve form göndermeye devam engellemez.

## <a name="steps"></a>Adımlar

ASP.NET AJAX Denetim Araç Seti içeren `FilteredTextBox` genişleten bir metin kutusu denetimi. Sonra yalnızca belirli karakter kümesini alana girilebilir.

Bunun işe yaraması için önce her zaman olduğu gibi ASP.NET AJAX ihtiyacımız `ScriptManager` de ASP.NET AJAX Denetim Araç Seti tarafından kullanılan JavaScript kitaplıklarını yükler:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

Ardından, bir metin kutusu gerekir:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

Son olarak, `FilteredTextBoxExtender` denetimi, kullanıcı türüne izin verilir karakter kısıtlama üstlenir. İlk olarak ayarlamak `TargetControlID` özniteliğini `ID` , `TextBox` denetimi. Ardından, kullanılabilir birini `FilterType` değerleri:

- `Custom` Varsayılan olarak; Geçerli karakterler listesini sağlamanız gerekir
- `LowercaseLetters` yalnızca küçük harfler
- `Numbers` yalnızca rakam
- `UppercaseLetters` yalnızca büyük harfler

Varsa `Custom FilterType` kullanılan `ValidChars` özelliği ayarlanmış olmalıdır ve türü belirtilmiş olmalıdır karakterlerin listesini sağlar. Bu arada: metin, metin kutusuna yapıştırın denerseniz, tüm geçersiz karakterleri kaldırılır.

İçin biçimlendirme şöyledir `FilteredTextBoxExtender` basamak yalnızca veren denetiminin (şey de mümkün olacaktı `FilterType="Numbers"`):

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

JavaScript etkinse, bir harf girmeyi deneyin ve sayfa Çalıştır çalışmaz; Basamaklar, ancak sayfada görüntülenir. Ancak, unutmayın koruma `FilteredTextBox` sağlar madde işareti kavram değil: JavaScript etkinse, herhangi bir veri ek doğrulama anlamına gelir, yani ASP kullanmak zorunda metin kutusuna girilebilir. NET doğrulama denetimleri.

[![Yalnızca rakam girilebilir](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)

Yalnızca rakam girilebilir ([tam boyutlu görüntüyü görmek için tıklatın](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](allowing-only-certain-characters-in-a-text-box-vb.md)
