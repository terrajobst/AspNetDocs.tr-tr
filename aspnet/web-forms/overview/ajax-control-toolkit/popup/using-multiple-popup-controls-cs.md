---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: Birden çok açılan denetim kullanmaC#() | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Ayrıca, d... kullanımı da mümkündür.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612653"
---
# <a name="using-multiple-popup-controls-c"></a>Birden Çok Açılan Denetim Kullanma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)

> AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Tek sayfada birden fazla açılan denetim kullanmak da mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Tek sayfada birden fazla açılan denetim kullanmak da mümkündür.

## <a name="steps"></a>Adımlar

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

Sonra, açılan pencere olarak işlev gören bir panel ekleyin. Geçerli senaryoda, panel bir `Calendar` denetimi içerir. Takvimin geri göndermeler nedeniyle oluşan sayfa yenilemelerinden kaçınmak için, panel bir `UpdatePanel` denetimine yerleştirilir:

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

Sayfada Ayrıca iki metin kutusu de bulunur. Her metin kutusu için, Takvim açılır penceresi metin kutusu etkinleştirildikten sonra görüntülenir.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

Şimdi iki metin kutusunun her birini bir `PopupControlExtender`genişletin. `TargetControlID` özniteliği, Extender 'a bağlı denetimin KIMLIĞINI sağlar. `PopupControlID` özniteliği açılan bölmenin KIMLIĞINI içerir. Bu durumda, her iki Extender da aynı paneli gösterir, ancak farklı paneller de mümkündür.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

Artık bir metin alanının içine tıkladığınızda alanın altında bir takvim görünür ve bir tarih seçmenizi sağlar. (Seçili tarihin metin kutularına geri alınması farklı bir öğreticide ele alınacaktır.)

[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)

Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-multiple-popup-controls-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
