---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: UpdatePanel olmayan bir açılan denetimden geri göndermeler işleme (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Su 'ta geri gönderme gerçekleştiğinde...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598757"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>UpdatePanel Olmadan Bir Açılan Denetimden Gelen Geri Göndermeleri İşleme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Bu tür bir panelde geri gönderme gerçekleştiğinde ve sayfada birkaç panel varsa, hangi panelin tıklandığını tespit etmek zordur.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Bu tür bir panelde geri gönderme gerçekleştiğinde ve sayfada birkaç panel varsa, hangi panelin tıklandığını tespit etmek zordur.

## <a name="steps"></a>Adımlar

Bir geri gönderme ile `PopupControl` kullanırken, ancak sayfada `UpdatePanel` olmadan Denetim araç seti, açılan pencereyi tetikleyen ve geri göndermeye neden olan istemci öğenin belirlenmesi için bir yol sunmaz. Ancak küçük bir püf konusu senaryo için geçici çözüm sağlar.

İlki, temel kurulum şudur: her iki metin kutusu de aynı açılan pencereyi bir takvimle tetikler. İki `PopupControlExtenders` metin kutularını ve açılan pencereyi birlikte getirin.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

Temel düşünce, açılan pencereyi başlatan metin kutusunu tutan &lt;`form`&gt; öğesine gizli form alanı eklemektir:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

Sayfa yüklendiğinde, JavaScript kodu her iki metin kutusuna da bir olay işleyicisi ekler: Kullanıcı bir metin kutusunu tıkladığında, adı gizli form alanına yazılır:

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

Sunucu tarafı kodunda, gizli alanın değeri okunmalıdır. Gizli form alanları işlemek için önemsiz olduğundan, gizli değeri doğrulamaya yönelik bir beyaz liste yaklaşımı gereklidir. Doğru metin kutusu tanımlandıktan sonra takvimdeki Tarih buna yazılır.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))

[bir tarihe tıklamak ![metin kutusuna koyar](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

Bir tarihe tıklamak, metin kutusuna koyar ([tam boyutlu görüntüyü görüntülemek Için tıklayın](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Önceki](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [İleri](using-multiple-popup-controls-vb.md)
