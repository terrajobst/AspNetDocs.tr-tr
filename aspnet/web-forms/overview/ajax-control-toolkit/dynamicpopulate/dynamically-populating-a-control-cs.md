---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
title: Bir denetimi dinamik olarak doldurmaC#() | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmeti (veya sayfa yöntemi) çağırır ve elde edilen değeri t üzerindeki bir hedef denetime doldurur...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e1fec43e-1daf-49d2-b0c7-7f1b930455cc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 24f88e44e0f878127314774d4e8846f80133413e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599277"
---
# <a name="dynamically-populating-a-control-c"></a>Bir Denetimi Dinamik Olarak Doldurma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)

> ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde `DynamicPopulate` denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur. Bu öğreticide nasıl ayarlanacağı gösterilmektedir.

## <a name="steps"></a>Adımlar

İlk olarak, `DynamicPopulate`tarafından çağrılacak yöntemi uygulayan bir ASP.NET Web hizmetine ihtiyacınız vardır. Web hizmeti sınıfı, `Microsoft.Web.Script.Services`içinde tanımlanan `ScriptService` özniteliğini gerektirir; Aksi takdirde ASP.NET AJAX, Web hizmeti için `DynamicPopulate`için gereken istemci tarafı JavaScript proxy 'sini oluşturamaz.

`DynamicPopulate` denetimi her bir Web hizmeti çağrısıyla bir bağlam bilgilerini gönderdiğinden, Web yönteminin `contextKey`dize türünde bir bağımsız değişken beklemesi gerekir. Aşağıdaki Web hizmeti, `contextKey` bağımsız değişkeni tarafından temsil edilen bir biçimde geçerli tarihi döndürür:

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample1.aspx)]

Web hizmeti daha sonra `DynamicPopulate.cs.asmx`olarak kaydedilir. Alternatif olarak, `DynamicPopulate` denetimi ile gerçek ASP.NET sayfasında bir sayfa yöntemi olarak `getDate()` yöntemini uygulayabilirsiniz.

Sonraki adımda yeni bir ASP.NET dosyası oluşturun. Her zaman olduğu gibi ilk adım, ASP.NET AJAX kitaplığı 'nı yüklemek ve Denetim araç takımını çalışır hale getirmek için geçerli sayfaya `ScriptManager` dahil edilir:

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample2.aspx)]

Daha sonra Web hizmeti çağrısının sonucunu gösteren bir etiket denetimi (örneğin, aynı adın HTML denetimini veya &lt;`asp:Label` /&gt; Web denetimi) ekleyin.

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample3.aspx)]

Bir HTML düğmesi (bir HTML denetimi olarak, sunucuya geri gönderme gerektirtiğimiz için), dinamik popülasyonu tetiklemek için kullanılır:

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample4.aspx)]

Son olarak, bağlantı kurmak için `DynamicPopulateExtender` denetimine ihtiyacımız var. Aşağıdaki öznitelikler ayarlanacak (belirgin olanlardan ayrı olarak, `ID` ve `runat`=`"server"`):

- Web hizmeti çağrısından sonucun nereye yerleştirileceğini `TargetControlID`
- Web hizmetinin yolunu `ServicePath` (bir sayfa yöntemi kullanmak istiyorsanız atlayın)
- Web yönteminin veya sayfa yönteminin `ServiceMethod` adı
- Web hizmetine gönderilecek bağlam bilgilerini `ContextKey`
- Web hizmeti çağrısını tetikleyen `PopulateTriggerControlID` öğesi
- Web hizmeti çağrısı sırasında hedef öğenin boş bırakılıp başlatılmayacağını `ClearContentsDuringUpdate`

Gördüğünüz gibi, denetim bazı bilgiler gerektirir, ancak her şeyi konuma koymak oldukça basit bir işlemdir. Geçerli senaryoda `DynamicPopulateExtender` denetimi için biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample5.aspx)]

Tarayıcıda ASP.NET sayfasını çalıştırın ve düğmesine tıklayın; geçerli tarihi ay-gün biçiminde alacaksınız.

[düğmeye tıklama ![sunucudan tarihi alır](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)

Düğmeye tıklama, tarihi sunucudan alır ([tam boyutlu görüntüyü görüntülemek Için tıklatın](dynamically-populating-a-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](dynamically-populating-a-control-using-javascript-code-cs.md)
