---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
title: Kullanıcı denetimi ve JavaScript ile DynamicPopulate kullanma (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmeti (veya sayfa yöntemi) çağırır ve elde edilen değeri t üzerindeki bir hedef denetime doldurur...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 38ac8250-8854-444c-b9ab-8998faa41c5a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: a0e6d04a5f62ab558aceb8302d94d3bf2dc8a39f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613710"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-c"></a>Kullanıcı Denetimi ve JavaScript ile DynamicPopulate Kullanma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)

> ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur. Özel istemci tarafı JavaScript kodu kullanılarak popülasyonun tetiklenmesi de mümkündür. Ancak, Extender bir kullanıcı denetiminde bulunduğunda özel dikkatli olunmalıdır.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde `DynamicPopulate` denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur. Özel istemci tarafı JavaScript kodu kullanılarak popülasyonun tetiklenmesi de mümkündür. Ancak, Extender bir kullanıcı denetiminde bulunduğunda özel dikkatli olunmalıdır.

## <a name="steps"></a>Adımlar

İlk olarak, `DynamicPopulateExtender` denetimi tarafından çağrılacak yöntemi uygulayan bir ASP.NET Web hizmetine ihtiyacınız vardır. Web hizmeti, `DynamicPopulate` denetimi her bir Web hizmeti çağrısıyla bir dizi bağlam bilgisi gönderdiğinden, `contextKey`olarak adlandırılan `getDate()` dize türünde bir bağımsız değişken bekleyen yöntemi uygular. Üç biçimden birindeki geçerli tarihi alan kod (dosya `DynamicPopulate.cs.asmx`) aşağıda verilmiştir:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample1.aspx)]

Sonraki adımda, ilk satırında aşağıdaki bildirimle belirtilen yeni bir kullanıcı denetimi (`.ascx` dosyası) oluşturun:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample2.aspx)]

Sunucudan gelen verileri göstermek için bir &lt;`label`&gt; öğesi kullanılacaktır.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample3.aspx)]

Ayrıca, Kullanıcı denetim dosyasında, her biri Web hizmeti tarafından desteklenen üç tarih biçiminden birini temsil eden üç radyo düğmesini kullanacağız. Kullanıcı radyo düğmelerinden birine tıkladığında tarayıcı şu şekilde görünen JavaScript kodunu yürütür:

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample4.ps1)]

Bu kod `DynamicPopulateExtender` erişir (alışılmadık KIMLIK hakkında endişelenmeyin, bu, daha sonra ele alınacaktır) ve dinamik popülasyonu verilerle tetikler. Geçerli radyo düğmesi bağlamında `this.value`, `format1`, `format2` veya `format3` tam olarak Web yönteminin beklediği değeri anlamına gelir.

Yalnızca Kullanıcı denetiminde eksik olan tek şey, radyo düğmelerini Web hizmetine bağlayan `DynamicPopulateExtender` denetimidir.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample5.aspx)]

Yine, denetimde kullanılan garip KIMLIĞI, `myDate`yerine `mcd1$myDate` görebilirsiniz. Daha önce, `dpe1`yerine `DynamicPopulateExtender` erişmek için `mcd1_dpe1` kullanılan JavaScript kodu. Bu adlandırma stratejisi, bir kullanıcı denetimi içinde `DynamicPopulateExtender` kullanırken özel bir gereksinimdir. Ayrıca, tüm çalışmaları yapmak için Kullanıcı denetimini belirli bir şekilde gömmeniz gerekir. Yeni bir ASP.NET sayfası oluşturun ve az önce uygulamış olduğunuz Kullanıcı denetimi için bir etiket öneki kaydedin:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample6.aspx)]

Ardından, ASP.NET AJAX `ScriptManager` denetimini yeni sayfaya ekleyin:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample7.aspx)]

Son olarak, sayfasına kullanıcı denetimini ekleyin. Yalnızca `ID` özniteliğini (ve `runat="server"`kurs) ayarlamanız yeterlidir, ancak bunu belirli bir ada ayarlamanız gerekir: Bu, Kullanıcı denetimi içinde JavaScript kullanarak erişmek için kullanılan ön ek olduğundan `mcd1`.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample8.aspx)]

Hepsi bu! Sayfa beklendiği gibi davranır: Kullanıcı radyo düğmelerinden birine tıkladığında araç setinde denetim Web hizmetini çağırır ve geçerli tarihi istenen biçimde görüntüler.

[radyo düğmelerinin bir kullanıcı denetiminde yer aldığı ![](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)

Radyo düğmeleri bir kullanıcı denetiminde bulunur ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](dynamically-populating-a-control-using-javascript-code-cs.md)
> [İleri](dynamically-populating-a-control-vb.md)
