---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: Yineleyici denetimiyle ModalPopup kullanma (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Bu contenr kullanmak da mümkündür...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 980f023c9e8256ad5323aaa6cbb6918b04e18974
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613157"
---
# <a name="using-modalpopup-with-a-repeater-control-c"></a>Repeater Denetimiyle ModalPopup Kullanma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)

> AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Bu denetimi bir yineleyici içinde kullanmak da mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Bu denetimi bir yineleyici içinde kullanmak da mümkündür.

## <a name="steps"></a>Adımlar

Birincisi, bir veri kaynağı gereklidir. Bu örnek, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express sürümünü kullanır. Veritabanı, Visual Studio yüklemesinin (Express Edition dahil) isteğe bağlı bir parçasıdır ve [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir. AdventureWorks veritabanı SQL Server 2005 örnek ve örnek veritabanlarının bir parçasıdır ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D ısplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) kullanmaktır ve `AdventureWorks.mdf` veritabanı dosyasını eklemektir. Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır. Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir. ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

Ardından, sayfaya bir veri kaynağı ekleyin. Sınırlı miktarda veri kullanmak için, AdventureWorks veritabanının satıcı tablosunda yalnızca ilk beş girişi seçersiniz. Veri kaynağını oluşturmak için Visual Studio Yardımcısı 'nı kullanıyorsanız, geçerli sürümdeki bir hatanın `Purchasing`tablo adını (`Vendor`) ön eki olmadığını unutmayın. Aşağıdaki biçimlendirme doğru söz dizimini göstermektedir:

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin. Açılan pencereyi kapatmak için bir `Button` denetimi içerir:

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

Açılan pencerenin yineleyicisi içinde çalışmasını sağlamak için, `ModalPopupExtender` denetiminin yineleyicisi 'nin `<ItemTemplate>` bölümü içine konmalıdır. Bu nedenle, panel yineleyicisi 'nin dışındadır, ancak genişletici içindedir. Yineleyicisi için biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

Ardından, veri kaynağındaki her öğe, onun yanında, kalıcı açılan pencereyi tetikleyen bir düğme ile görüntülenir.

[![, her veri kaynağı girdisi için kalıcı açılan pencere tetiklenebilir](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)

Her veri kaynağı girişi için kalıcı açılan pencere tetiklenebilir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](launching-a-modal-popup-window-from-server-code-cs.md)
> [İleri](handling-postbacks-from-a-modalpopup-cs.md)
