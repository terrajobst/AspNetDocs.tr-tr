---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: Web hizmeti arka ucu ile sayısal bir yukarı/aşağı denetimi oluşturma (C#) | Microsoft Docs
author: wenz
description: Bir kullanıcının bir onay kutusuna değer yazmalarına izin vermek yerine, sayısal bir yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde bulunur) daha fazla c... anlamına gelebilir.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 816a840b9e93b95a049c3a4cb792e9deeab28983
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598895"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a>Web Hizmeti Arka Ucuna Sahip Sayısal Yukarı/Aşağı Denetimi Oluşturma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)

> Bir kullanıcının onay kutusuna değer yazmalarına izin vermek yerine, sayısal bir yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde bulunur) daha rahat bir şekilde kanıtlayabilecek. Varsayılan olarak, NumericUpDown denetimi her zaman bir değeri 1 artırır veya düşürür, ancak bir Web hizmeti daha fazla esneklik sağlar.

## <a name="overview"></a>Genel bakış

Bir kullanıcının onay kutusuna değer yazmalarına izin vermek yerine, sayısal bir yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde bulunur) daha rahat bir şekilde kanıtlayabilecek. Varsayılan olarak, `NumericUpDown` denetimi her zaman bir değeri 1 artırır veya düşürür, ancak bir Web hizmeti daha fazla esneklik sağlar.

## <a name="steps"></a>Adımlar

ASP.NET AJAX denetim araç seti, bir metin kutusuna otomatik olarak iki düğme ekleyen `NumericUpDown` Genişletici ' i içerir: bir tane, değerini azaltmak için bir tane. Ancak denetim Ayrıca bir Web hizmeti çağrısını (veya sayfa yöntemi çağrısını) destekler. Yukarı veya aşağı düğmesine tıklandığında, JavaScript kodu Web sunucusuna bağlanır ve bir yöntemi bu yerde yürütür. Yöntem imzası aşağıdakilerden biridir:

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

`current` bağımsız değişkeni, metin kutusundaki geçerli değerdir; `tag` özniteliği, `NumericUpDown` genişletici 'in bir özelliği olarak ayarlanmakta olan ek bağlam verileri (ancak gerekli değildir).

Bu örnekte, sayısal yukarı/aşağı denetimi yalnızca iki üsleri olan değerlere izin veriyor: 1, 2, 4, 8, 16, 32, 64, vb. Bu nedenle, kullanıcının değeri arttırmak istediğinde yürütülen Yöntem eski değeri Double olmalıdır; diğer yöntem değeri iki ile bölmelidir. Web hizmetinin tamamı aşağıda verilmiştir:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

Son olarak, yeni bir ASP.NET sayfası oluşturun. Her zamanki gibi, bir `ScriptManager` denetimine, `TextBox` denetimine ve `NumericUpDownExtender` denetimine ihtiyacınız vardır. İkincisi için, Web hizmeti bilgilerini sağlamanız gerekir:

- aşağı Web yönteminin veya sayfa yönteminin `ServiceDownMethod` adı
- Web hizmetinin yolunu aşağı hizmet yöntemiyle `ServiceDownPath`; bir sayfa yöntemi kullanıyorsanız, atlayın
- up Web yönteminin veya sayfa yönteminin `ServiceUpMethod` adı
- up hizmeti yöntemiyle Web hizmetinin yolunu `ServiceUpPath`; bir sayfa yöntemi kullanıyorsanız, atlayın

Sayfa için tüm biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

Sayfayı çalıştırırsanız, üstteki düğmeye tıkladığınızda metin kutusundaki değerin her zaman iki katına çıkar ve alt düğmeye tıkladığınızda bu değeri yarıya iner.

[![yalnızca 2 ' nin üssü olan sayılar görüntülenir](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)

Yalnızca 2 ' nin üssü olan sayılar görüntülenir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
