---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: JavaScript 'ten bir paneli daraltma ve genişletme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde CollapsiblePanel denetimi bir paneli genişletir ve içeriğini daraltma ve bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599347"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a>JavaScript’ten Bir Paneli Daraltma ve Genişletme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)

> ASP.NET AJAX denetim araç setinde CollapsiblePanel denetimi bir paneli genişletir ve içeriğini daraltma ve yeniden genişletme özelliğini sağlar. Bu iki eylem özel JavaScript kodundan de tetiklenebilir.

## <a name="overview"></a>Genel bakış

ASP.NET AJAX denetim araç setinde CollapsiblePanel denetimi bir paneli genişletir ve içeriğini daraltma ve yeniden genişletme özelliğini sağlar. Bu iki eylem özel JavaScript kodundan de tetiklenebilir.

## <a name="steps"></a>Adımlar

İlk olarak, yeni bir ASP.NET sayfası oluşturun ve `ScriptManager` bir `<form>` öğesine ekleyin. Bu, Denetim araç seti için gerekli olan ASP.NET AJAX kitaplığını yükler:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

Ardından, daraltma/genişletme efektinin görünebilmesi için bazı metinlere sahip bir panel oluşturun:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

Gördüğünüz gibi, panel burada gösterilen bir CSS sınıfına başvurur (ve temelde bir arka plan rengi ve panelin genişliğini tanımlar):

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

`CollapsiblePanelExtender` denetimi `TargetControlID` özniteliğini gerektirir, böylece araç seti, istek üzerine hangi bölmenin daraltılacak veya genişletileceğini bilir:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

Ne yazık ki genişletici, paneli daraltma veya genişletme için belirli bir API kullanıma sunmuyor, ancak belgelenmemiş bazı yöntemler yapılacak. İlk olarak, sayfaya üç HTML düğmesi ekleyin ve ardından panelin içeriğini daraltmak veya genişletmek için istemci tarafı JavaScript 'i tetikler:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

İstemci tarafı JavaScript kodunda (`<script type="text/javascript">`ile başlatılır), `CollapsiblePanelExtender`erişmek için `$find()` yönteminin kullanılması gerekir. `$find("cpe")`, buna bir başvuru döndürür. Bu noktada, belirli yöntemler el ile görevi çözebilir.

Paneli açma (genişletme) yöntemi `_doOpen()`olarak adlandırılır; Aşağıdaki kod, ilk düğme tıklandığında çağrılan `doOpen()` işlevini uygular:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

Paneli kapatmak veya daraltma için `_doClose()` yönteminin yürütülmesi gerekir. Bu nedenle, Kullanıcı ikinci düğmeye tıkladığında aşağıdaki JavaScript kodu çağrılır:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

Üçüncü düğme, panelin durumunu daraltıldı ve bunun tersini yapar. `CollapsiblePanelExtender`, tam olarak bunu yapan ve panelin durumunu tersine getiren `toggle()` yöntemini kullanıma sunar. Ancak, `toggle()` yöntemi tarafından dahili olarak kullanılan başka bir yaklaşım da vardır: `CollapsiblePanelExtender()` `get_Collapsed()` yöntemi, bölmenin daraltılıp daraltılmadığını söyler. Bu işlevin dönüş değerine bağlı olarak, panel daha sonra genişletilir (`_doOpen()` yöntemi) veya daraltılmış (`_doClose()`) yöntemi:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

[üçüncü düğme ![bölmenin durumunu değiştirir: daraltılan ve geriye doğru](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)

Üçüncü düğme, panelin durumunu, daraltılan ve geri ([tam boyutlu görüntüyü görüntülemek Için tıklatın](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)) olarak değiştirir.

> [!div class="step-by-step"]
> [Öncekini](collapsing-and-expanding-a-panel-from-javascript-cs.md)
