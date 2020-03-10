---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: Basamaklı Dingdropdown kullanarak liste doldurma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Basamakarda açılan menü denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin ilişkili değerleri anormal bir şekilde yükler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 8dd9ef8a4bdf705ba4451b7fd240e4de8618221c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536010"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a>CascadingDropDown Kullanarak Liste Doldurma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)

> AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler. (Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Çözecek ilk zorluk, bu denetimi kullanarak bir açılan listeyi gerçekten doldurmektir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler. (Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Çözecek ilk zorluk, bu denetimi kullanarak bir açılan listeyi gerçekten doldurmektir.

## <a name="steps"></a>Adımlar

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

Ardından, bir DropDownList denetimi gereklidir:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

Bu liste için, basamaklı bir açılan menü Genişleticisi eklenmiştir. Bu işlem, bir Web hizmetine zaman uyumsuz bir istek gönderir ve ardından listede görüntülenecek girişlerin bir listesini döndürür. Bunun çalışması için, aşağıdaki basamaklı Dingdropdown özniteliklerinin ayarlanması gerekir:

- `ServicePath`: liste girdilerini sunan bir Web hizmetinin URL 'SI
- `ServiceMethod`: liste girdilerini teslim eden Web yöntemi
- `TargetControlID`: açılan listenin KIMLIĞI
- `Category`: çağrıldığında Web yöntemine gönderilen kategori bilgileri
- `PromptText`: sunucudan zaman uyumsuz olarak liste verileri yüklenirken görünen metin

`CascadingDropDown` öğesi için biçimlendirme aşağıda verilmiştir. Ve VB arasındaki C# tek fark, ilişkili Web hizmetinin adıdır:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

`CascadingDropDown` genişleticinizden gelen JavaScript kodu, aşağıdaki imzayla bir Web hizmeti yöntemini çağırır:

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

Bu nedenle, yöntemin `CascadingDropDownNameValue` türünde bir dizi döndürmesi gerekir (ASP.NET AJAX denetim araç seti tarafından tanımlanır). `CascadingDropDownNameValue` oluşturucusunda, ilk olarak liste girişinin metni ve ardından değeri, `<option value="VALUE">NAME</option>` HTML içinde olduğu gibi belirtilmelidir. Örnek veriler aşağıda verilmiştir:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

Sayfanın tarayıcıya yüklenmesi, listenin üç satıcı ile doldurulduğu şekilde tetiklenecek.

[![liste otomatik olarak doldurulur](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)

Liste otomatik olarak doldurulur ([tam boyutlu görüntüyü görüntülemek Için tıklayın](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](using-auto-postback-with-cascadingdropdown-cs.md)
> [İleri](using-cascadingdropdown-with-a-database-vb.md)
