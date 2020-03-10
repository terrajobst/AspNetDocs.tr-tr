---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: JavaScript kodu kullanarak bir denetimi dinamik olarak doldurmaC#() | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmeti (veya sayfa yöntemi) çağırır ve elde edilen değeri t üzerindeki bir hedef denetime doldurur...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 24dc358427dec3ffcba16d00041c9a2db657e7e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535744"
---
# <a name="dynamically-populating-a-control-using-javascript-code-c"></a>JavaScript Kodu Kullanarak Bir Denetimi Dinamik Olarak Doldurma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)

> ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur. Özel istemci tarafı JavaScript kodu kullanılarak popülasyonun tetiklenmesi de mümkündür.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde `DynamicPopulate` denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur. Özel istemci tarafı JavaScript kodu kullanılarak popülasyonun tetiklenmesi de mümkündür.

## <a name="steps"></a>Adımlar

İlk olarak, `DynamicPopulateExtender` denetimi tarafından çağrılacak yöntemi uygulayan bir ASP.NET Web hizmetine ihtiyacınız vardır. Web hizmeti, `DynamicPopulate` denetimi her bir Web hizmeti çağrısıyla bir dizi bağlam bilgisi gönderdiğinden, `contextKey`olarak adlandırılan `getDate()` dize türünde bir bağımsız değişken bekleyen yöntemi uygular. Üç biçimden birindeki geçerli tarihi alan kod (dosya `DynamicPopulate.cs.asmx`) aşağıda verilmiştir:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

Sonraki adımda, yeni bir ASP.NET sitesi oluşturun ve ASP.NET AJAX ScriptManager denetimiyle başlayın:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

Ardından, daha sonra Web hizmeti çağrısının sonucunu gösterecek bir etiket denetimi (örneğin, aynı ada sahip HTML denetimini veya `<asp:Label />` Web denetimini kullanarak) ekleyin.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

Daha sonra, bir `DynamicPopulateExtender` denetimi ekleyin ve Web hizmeti bilgilerini, hedef denetimi sağlayın, ancak bunun daha sonra, özel JavaScript kullanılarak yapılacak şekilde bu işlemi tetikleyecek olan denetimin adını değil,

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

Şimdi JavaScript bölümüne. ASP.NET AJAX kitaplığı tarafından tanımlanan `$find()` işlevi, `DynamicPopulateExtender`gibi ASP.NET AJAX denetim araç setinin sunucu tarafı nesnelerine bir başvuru döndürür. Geçerli dosyada, `$find("dpe")` sayfadaki bir `DynamicPopulateExtender` denetimine bir başvuru döndürür. Dinamik popülasyon işlemini tetikleyen `populate()` adlı bir yöntemi kullanıma sunar. `populate()` yöntemi bir bağımsız değişken gerektiriyor: `getDate()` Web metoduna bağımsız değişken olarak kullanılacak bağlam anahtarı. Örneğin, `$find("dpe").populate("format1")`, etiketi ay-gün biçiminde geçerli tarihle dolduracaktır.

Örneği biraz daha esnek hale getirmek için Kullanıcı artık birkaç tarih biçimi arasından seçim yapabilir. Bunların her biri için bir radyo düğmesi görüntülenir. Kullanıcı radyo düğmesine tıkladığında, JavaScript kodu etiketi seçilen tarih biçimiyle dinamik olarak doldurur. Bu radyo düğmeleri aşağıda verilmiştir:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

Radyo düğmesi bağlamında, JavaScript ifadesi `this.value`, geçerli düğmenin değerini ifade eder ve bu da `getDate()` yönteminin birlikte çalışabileceği bilgilerle tamamen aynı olur.

[düğmeye tıklama ![, belirtilen biçimde sunucudan tarihi alır](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)

Düğmeye tıkladığınızda, belirtilen biçimdeki tarihi sunucudan alır ([tam boyutlu görüntüyü görüntülemek Için tıklatın](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](dynamically-populating-a-control-cs.md)
> [İleri](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
