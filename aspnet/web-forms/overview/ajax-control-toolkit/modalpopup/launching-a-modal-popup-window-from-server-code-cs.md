---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: Sunucu kodundan (C#) kalıcı bir açılan pencere başlatılıyor | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak bazı senaryolar bu t... gerektirir.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: fec0ce2cdd24333f65201301718440e1a09d930e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613297"
---
# <a name="launching-a-modal-popup-window-from-server-code-c"></a>Sunucu Kodundan Kalıcı Açılan Pencere Başlatma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)

> AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak bazı senaryolar, sunucu tarafında kalıcı açılan pencerenin açılmasını gerektirir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak bazı senaryolar, sunucu tarafında kalıcı açılan pencerenin açılmasını gerektirir.

## <a name="steps"></a>Adımlar

Birincisi, ModalPopup denetiminin nasıl çalıştığını göstermek için bir ASP.NET Button Web denetimi gereklidir. Yeni bir sayfada &lt;form&gt; öğesi içinde böyle bir düğme ekleyin:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

Ardından, oluşturmak istediğiniz açılan pencere için biçimlendirmenin olması gerekir. Bunu bir `<asp:Panel>` denetimi olarak tanımlayın ve bir düğme denetimi içerdiğinden emin olun. ModalPopup denetimi, bu tür bir düğmeyi açılan pencereyi kapatacak şekilde işlevleri sunar; Aksi takdirde, bir yol açmanın kolay bir yolu yoktur.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

Daha sonra, ASP.NET AJAX araç kümesinden ModalPopup denetimini sayfaya ekleyin. Denetimi yükleyen düğme için özellikleri, ortadan kaldırdıkları düğmeyi ve gerçek açılan pencerenin KIMLIĞINI ayarlayın.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

ASP.NET AJAX 'ı temel alan tüm Web sayfalarında olduğu gibi Komut dosyası Yöneticisi, farklı hedef tarayıcılar için gerekli JavaScript kitaplıklarını yüklemek üzere gereklidir:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

Örneği tarayıcıda çalıştırın. Düğmeye tıkladığınızda, kalıcı açılan pencere görünür. Sunucu tarafı kod kullanarak aynı etkiye ulaşmak için yeni bir düğme gereklidir:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

Gördüğünüz gibi, düğmesine bir tıklama geri gönderme oluşturur ve `ServerButton_Click()` yöntemi sunucuda yürütülür. Bu yöntemde `launchModal()` adlı bir JavaScript işlevi, sayfa yüklendikten sonra JavaScript işlevi yürütülür:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

`launchModal()` işi ModalPopup görüntülemektir. Tüm HTML sayfası yüklendikten sonra `launchModal()` işlevi yürütülür. Ancak, ASP.NET AJAX Framework henüz tam olarak yüklenmemiştir. Bu nedenle, `launchModal()` işlevi yalnızca ModalPopup denetiminin daha sonra gösterilmesi gereken bir değişken ayarlar:

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

`pageLoad()` JavaScript işlevi, ASP.NET AJAX tam olarak yüklendikten sonra yürütülen özel bir işlevdir. Bu nedenle, ModalPopup denetimini göstermek için bu işleve kod ekleyeceğiz, ancak yalnızca `launchModal()` daha önce çağrılırsa:

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

`$find()` işlevi sayfada adlandırılmış bir öğe arıyor ve sunucu tarafı KIMLIĞINI parametre olarak bekler. Bu nedenle, `$find("mpe")` ModalPopup denetiminin istemci temsilini döndürür; `show()` yöntemi, açılan pencerenin görünmesine izin verir.

[düğme tıklandığında kalıcı açılan pencere ![görünür](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)

Düğme tıklandığında kalıcı açılan pencere görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](using-modalpopup-with-a-repeater-control-cs.md)
