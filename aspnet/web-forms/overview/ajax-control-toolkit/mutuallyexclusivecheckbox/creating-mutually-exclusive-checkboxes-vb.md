---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Birbirini dışlayan onay kutuları (VB) oluşturma | Microsoft Docs
author: wenz
description: 'Radyo düğmeleri, genellikle bir seçenek kümesi yalnızca biri seçili olduğunda kullanılır. Ancak bir dezavantajı vardır: Bir radyo düğmesi grubundaki bir kez seçildiğinde...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: 5bf96cf287f2fe5f394449587c70d9fc6fb33af9
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132549"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a>Birbirini Dışlayan Onay Kutuları Oluşturma (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> Radyo düğmeleri, genellikle bir seçenek kümesi yalnızca biri seçili olduğunda kullanılır. Ancak bir dezavantajı vardır: Bir gruptaki bir radyo düğmesi seçildikten sonra tüm radyo düğmeleri işaretini mümkün değildir. Onay kutularını herhangi bir zamanda denetlenmeyen olabilir, ancak birbirini dışlamaz. Bu öğreticide her iki yaklaşım en iyi şekilde sağlanır: karşılıklı olarak birbirini dışlayan onay kutuları.

## <a name="overview"></a>Genel Bakış

Radyo düğmeleri, genellikle bir seçenek kümesi yalnızca biri seçili olduğunda kullanılır. Ancak bir dezavantajı vardır: Bir gruptaki bir radyo düğmesi seçildikten sonra tüm radyo düğmeleri işaretini mümkün değildir. Onay kutularını herhangi bir zamanda denetlenmeyen olabilir, ancak birbirini dışlamaz. Bu öğreticide her iki yaklaşım en iyi şekilde sağlanır: karşılıklı olarak birbirini dışlayan onay kutuları.

## <a name="steps"></a>Adımlar

ASP.NET AJAX Denetim Araç Seti MutuallyExclusiveCheckBox genişletici içerir. Bu, herhangi bir onay kutusu bir grup adına atanacak programcılar sağlar (`Key` özniteliği). Aynı gruptaki tüm onay kutularından birini tek tek seferde seçilebilir.

Yeni bir ASP.NET sayfasında iki onay kutularını koyarak ile başlayalım. Daha fazla da olabilir, ancak ikisini ilkesini göstermek için yeterli:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

Her iki onay kutularını MutuallyExclusiveCheckBoxExtender denetim sayfada yerleştirmeniz gerekir. Her iki anahtar öznitelik HTML radyo düğmesi öğeleri özniteliklerini ait oldukları grubu belirtmek için aynı değeri olarak aynı değere sahip olması gerekir. Kimlik onay kutusu genişletici noktalarına TargetControlID özelliği.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

Son olarak, ASP.NET AJAX dahil `ScriptManager` ASP.NET AJAX Denetim Araç Seti tüm öğeleri tarafından gerekli:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

Kaydet ve sayfayı çalıştırın: Denetleyin ve her iki onay kutularının işaretini kaldırın. ancak hiçbir zaman hem onay kutularını denetlenebilir.

[![Bir kerede yalnızca bir onay kutusu denetlenebilir](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

Tek checkbox aynı anda iade ([tam boyutlu görüntüyü görmek için tıklatın](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](creating-mutually-exclusive-checkboxes-cs.md)
