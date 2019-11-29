---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Birbirini dışlayan onay kutuları oluşturma (VB) | Microsoft Docs
author: wenz
description: Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır. Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: f33936dd4d71f6bbf08f02966eefe44c8c152eba
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606484"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a>Birbirini Dışlayan Onay Kutuları Oluşturma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır. Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra tüm radyo düğmelerinin işaretini kaldırmak mümkün değildir. Onay kutuları herhangi bir zamanda işaretlenmeyebilir, ancak birbirini dışlamayan değildir. Bu öğretici her iki yaklaşımdan en iyi şekilde yararlanabilirsiniz: birbirini dışlayan onay kutuları.

## <a name="overview"></a>Genel bakış

Bir seçenek kümesinden yalnızca biri seçilebilir olduğunda, radyo düğmeleri genellikle kullanılır. Bir dezavantajı vardır, ancak bir grup içindeki bir radyo düğmesi seçildikten sonra tüm radyo düğmelerinin işaretini kaldırmak mümkün değildir. Onay kutuları herhangi bir zamanda işaretlenmeyebilir, ancak birbirini dışlamayan değildir. Bu öğretici her iki yaklaşımdan en iyi şekilde yararlanabilirsiniz: birbirini dışlayan onay kutuları.

## <a name="steps"></a>Adımlar

ASP.NET AJAX denetim araç seti, Muluallyexclusivecheckbox genişletici öğesini içerir. Bu, programcıların bir grup adına (`Key` özniteliği) herhangi bir onay kutusu atamasını sağlar. Aynı grup içindeki tüm onay kutularından tek seferde yalnızca bir tane seçilebilir.

Yeni bir ASP.NET sayfasına iki onay kutusu yerleştirmeye başlayalım. Daha fazla olabilir, ancak bu ilkeyi göstermek için iki ikisi de vardır:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

Her iki onay kutusu için de sayfada bir çoklu kullanıcı olmalıdır. Her iki anahtar özniteliği de aynı değere sahip olmalıdır, ancak HTML radyo düğmesi öğelerinin değer özniteliklerinin ait oldukları grubu göstermek için aynı olması gerekir. Extender 'ın TargetControlID özelliği, onay kutusunun KIMLIĞINE işaret eder.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

Son olarak, ASP.NET AJAX denetim araç setinin tüm öğeleri için gerekli olan ASP.NET AJAX `ScriptManager` ekleyin:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

Sayfayı kaydedip çalıştırın: onay kutularının her ikisini de denetleyebilir ve işaretini kaldırın, ancak her iki onay kutusu da onay kutularından denetlenebilir.

[![, tek seferde yalnızca bir onay kutusu denetlenebilir](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

Tek seferde yalnızca bir onay kutusu denetlenebilir ([tam boyutlu görüntüyü görüntülemek Için tıklatın](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](creating-mutually-exclusive-checkboxes-cs.md)
