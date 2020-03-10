---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: Birbirini dışlayan onay kutuları oluşturmaC#() | Microsoft Docs
author: wenz
description: Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır. Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613073"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a>Birbirini Dışlayan Onay Kutuları Oluşturma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)

> Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır. Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra tüm radyo düğmelerinin işaretini kaldırmak mümkün değildir. Onay kutuları herhangi bir zamanda işaretlenmeyebilir, ancak birbirini dışlamayan değildir. Bu öğretici her iki yaklaşımdan en iyi şekilde yararlanabilirsiniz: birbirini dışlayan onay kutuları.

## <a name="overview"></a>Genel bakış

Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır. Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra tüm radyo düğmelerinin işaretini kaldırmak mümkün değildir. Onay kutuları herhangi bir zamanda işaretlenmeyebilir, ancak birbirini dışlamayan değildir. Bu öğretici her iki yaklaşımdan en iyi şekilde yararlanabilirsiniz: birbirini dışlayan onay kutuları.

## <a name="steps"></a>Adımlar

ASP.NET AJAX denetim araç seti, Muluallyexclusivecheckbox genişletici öğesini içerir. Bu, programcıların bir grup adına (`Key` özniteliği) herhangi bir onay kutusu atamasını sağlar. Aynı grup içindeki tüm onay kutularından tek seferde yalnızca bir tane seçilebilir.

Yeni bir ASP.NET sayfasına iki onay kutusu yerleştirmeye başlayalım. Daha fazla olabilir, ancak bu ilkeyi göstermek için iki ikisi de vardır:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

Her iki onay kutusu için de sayfada bir çoklu kullanıcı olmalıdır. Her iki anahtar özniteliği de aynı değere sahip olmalıdır, ancak HTML radyo düğmesi öğelerinin değer özniteliklerinin ait oldukları grubu göstermek için aynı olması gerekir. Extender 'ın TargetControlID özelliği, onay kutusunun KIMLIĞINE işaret eder.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

Son olarak, ASP.NET AJAX denetim araç setinin tüm öğeleri için gerekli olan ASP.NET AJAX `ScriptManager` ekleyin:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

Sayfayı kaydedip çalıştırın: onay kutularının her ikisini de denetleyebilir ve işaretini kaldırın, ancak her iki onay kutusu da onay kutularından denetlenebilir.

[![, tek seferde yalnızca bir onay kutusu denetlenebilir](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)

Tek seferde yalnızca bir onay kutusu denetlenebilir ([tam boyutlu görüntüyü görüntülemek Için tıklatın](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](creating-mutually-exclusive-checkboxes-vb.md)
