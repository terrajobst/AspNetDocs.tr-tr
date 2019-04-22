---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: Bir Web hizmeti arka ucuna sahip (VB) sayısal yukarı/aşağı denetimi oluşturma | Microsoft Docs
author: wenz
description: Bir onay kutusuna bir değer kullanıcının yapmasına izin vermek yerine bir sayısal yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde var olan) daha fazla c kanıtlamak...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 0442b5e22e44e0767825026b26ad3da55777b962
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59384272"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>Web Hizmeti Arka Ucuna Sahip Sayısal Yukarı/Aşağı Denetimi Oluşturma (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> Bir onay kutusuna bir değer kullanıcının yapmasına izin vermek yerine bir sayısal yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde var olan) gibi daha fazla kanıtlamak rahat. Varsayılan olarak, NumericUpDown denetimi her zaman artırır veya bir değer 1 ile azaltır, ancak daha fazla esneklik bir web hizmeti kanıtlar.


## <a name="overview"></a>Genel Bakış

Bir onay kutusuna bir değer kullanıcının yapmasına izin vermek yerine bir sayısal yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde var olan) gibi daha fazla kanıtlamak rahat. Varsayılan olarak, `NumericUpDown` denetimi her zaman artırır veya bir değer 1 ile azaltır, ancak daha fazla esneklik bir web hizmeti kanıtlar.

## <a name="steps"></a>Adımlar

ASP.NET AJAX Denetim Araç Seti içeren `NumericUpDown` otomatik olarak iki düğme metin kutusuna ekleyen genişletici: Bir değeri, bunu azaltmak için bir tane artırmaya yönelik. Ancak denetim bir web hizmeti çağrısı (veya sayfa yöntem çağrısının) destekler. Zaman ölçeğini artırıp düğmesine tıklandığında, JavaScript kodu web sunucusuna bağlanır ve bir yöntemi yürütür. Aşağıdaki bir yöntem imzası verilmiştir:

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

`current` Bağımsız değişkendir metin kutusundaki; geçerli değer `tag` özniteliktir özelliği olarak ayarlanabilir ek bağlam verileri `NumericUpDown` genişletici (ancak gerekli değildir).

Bu örnek, sayısal yukarı/aşağı denetimi yalnızca iki powers olan değerleri izin: 1, 2, 4, 8, 16, 32, 64 ve benzeri. Bu nedenle, değeri artırmak kullanıcı istediğinde yürütülen yöntemi çift eski değeri gerekir; başka bir yöntem değeri tarafından iki bölme gerekir. Bu nedenle tam bir web hizmeti şu şekildedir:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

Son olarak, yeni bir ASP.NET sayfası oluşturun. Her zamanki şekilde ihtiyacınız bir `ScriptManager` denetimi, bir `TextBox` denetimi ve bir `NumericUpDownExtender` denetimi. İkincisi için web hizmeti bilgileri sağlamanız gerekir:

- `ServiceDownMethod` Aşağı adını web yöntemini veya sayfa yöntemi
- `ServiceDownPath` yolu aşağı hizmet yöntemi ile web hizmetine; bir sayfa yöntemini kullanıyorsanız atla
- `ServiceUpMethod` Yukarı adını web yöntemini veya sayfa yöntemi
- `ServiceUpPath` yolu yukarı hizmet yöntemi ile web hizmetine; bir sayfa yöntemini kullanıyorsanız atla

Sayfa için tam biçimlendirmesi şöyledir:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

Sayfa çalıştırırsanız, üst düğmesine tıklayın ve daha düşük düğmesine tıkladığınızda yarıya nasıl metin kutusundaki değeri her zaman çiftler dikkat edin.


[![2'in kuvveti olan sayılar görünür](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

2'in kuvveti olan sayılar görünür ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
