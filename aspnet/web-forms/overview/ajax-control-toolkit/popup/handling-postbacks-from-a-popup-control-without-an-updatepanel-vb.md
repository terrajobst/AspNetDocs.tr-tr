---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: UpdatePanel olmayan bir açılan denetimden geri göndermeler işleme (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Su 'ta geri gönderme gerçekleştiğinde...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: aaecf77c1d25f2c99ef4e9948d79fc01b837169b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553986"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a>UpdatePanel Olmadan Bir Açılan Denetimden Gelen Geri Göndermeleri İşleme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)

> AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Bu tür bir panelde geri gönderme gerçekleştiğinde ve sayfada birkaç panel varsa, hangi panelin tıklandığını tespit etmek zordur.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Bu tür bir panelde geri gönderme gerçekleştiğinde ve sayfada birkaç panel varsa, hangi panelin tıklandığını tespit etmek zordur.

## <a name="steps"></a>Adımlar

Bir geri gönderme ile `PopupControl` kullanırken, ancak sayfada `UpdatePanel` olmadan Denetim araç seti, açılan pencereyi tetikleyen ve geri göndermeye neden olan istemci öğenin belirlenmesi için bir yol sunmaz. Ancak küçük bir püf konusu senaryo için geçici çözüm sağlar.

İlki, temel kurulum şudur: her iki metin kutusu de aynı açılan pencereyi bir takvimle tetikler. İki `PopupControlExtenders` metin kutularını ve açılan pencereyi birlikte getirin.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

Temel düşünce, açılan pencereyi başlatan metin kutusunu tutan &lt;`form`&gt; öğesine gizli form alanı eklemektir:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

Sayfa yüklendiğinde, JavaScript kodu her iki metin kutusuna da bir olay işleyicisi ekler: Kullanıcı bir metin kutusunu tıkladığında, adı gizli form alanına yazılır:

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

Sunucu tarafı kodunda, gizli alanın değeri okunmalıdır. Gizli form alanları işlemek için önemsiz olduğundan, gizli değeri doğrulamaya yönelik bir beyaz liste yaklaşımı gereklidir. Doğru metin kutusu tanımlandıktan sonra takvimdeki Tarih buna yazılır.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)

Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))

[bir tarihe tıklamak ![metin kutusuna koyar](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)

Bir tarihe tıklamak, metin kutusuna koyar ([tam boyutlu görüntüyü görüntülemek Için tıklayın](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))

> [!div class="step-by-step"]
> [Öncekini](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
