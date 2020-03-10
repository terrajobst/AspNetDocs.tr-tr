---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: Basamaklı Dingdropdown ile otomatik geri gönderme kullanma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Basamakarda açılan menü denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin ilişkili değerleri anormal bir şekilde yükler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 5dea23a20aba00af5109f05f18365b89e409a131
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535926"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a>CascadingDropDown ile Otomatik Geri Gönderme Kullanma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)

> AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler. Ancak, basamaklı Dingdropdown denetimini kullanırken, ASP. Veriye zaman uyumsuz olarak veri yüklemesi (gereksiz) geri gönderme oluşturduğundan, NET 'in DropDownList denetiminin AutoPostBack özelliği çalışmaz. Bazı JavaScript kodları ile bu etkilerden kaçınılabilir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler. (Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Ancak, basamaklı Dingdropdown denetimini kullanırken, ASP. Veriye zaman uyumsuz olarak veri yüklemesi (gereksiz) geri gönderme oluşturduğundan, NET 'in DropDownList denetiminin AutoPostBack özelliği çalışmaz. Bazı JavaScript kodları ile bu etkilerden kaçınılabilir.

## <a name="steps"></a>Adımlar

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak &lt;`form`&gt; öğesi içinde):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

Ardından, bir DropDownList denetimi gereklidir:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

Bu liste için, Web hizmeti URL 'SI ve yöntem bilgileri sağlayan bir basamaklı Dinglist genişletici eklenmiştir:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

Basamaklı Dingdropdown genişletici, daha sonra aşağıdaki yöntem imzasıyla bir Web hizmetini zaman uyumsuz olarak çağırır:

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

Yöntemi, basamaklı Dingdropdown değeri türünde bir dizi döndürür. Türün Oluşturucusu önce liste girişinin başlığını ve ardından değeri (HTML `value` özniteliği) bekler.

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

Sayfanın tarayıcıda yüklenmesi, açılan listeyi üç satıcı ile doldurur, ikincisi ise önceden seçilir. Ayrıca, ASP.NET `__doPostBack()` JavaScript yöntemini tanımlar. Sayfa yüklendikten sonra, bu JavaScript çağrısı açılan listeye eklenir, ancak yalnızca içinde öğeler varsa. Listede hiçbir öğe yoksa, Denetim araç seti Şu anda onları yüklüyor, bu nedenle JavaScript kodu bir zaman aşımı kullanır ve yarım saniye içinde yeniden dener.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

Bu şekilde, geri gönderme yalnızca listede gerçekten öğeler olduğunda ve Kullanıcı bir giriş seçtiğinde yürütülür.

[bir liste öğesinin seçilmesi ![geri göndermeye neden olur](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)

Bir liste öğesi seçilmesi geri göndermeye neden olur ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](presetting-list-entries-with-cascadingdropdown-vb.md)
