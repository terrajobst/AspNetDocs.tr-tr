---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: Repeater denetimiyle HoverMenu kullanma (VB) | Microsoft Docs
author: wenz
description: 'AJAX denetim araç setinde HoverMenu denetimi basit bir açılan efekt sağlar: fare işaretçisi bir öğenin üzerine geldiğinde, bir açılan pencere bir öğe üzerinde görünür...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9386aa2fe3a6174bbed52218337107733cb1fa99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621578"
---
# <a name="using-hovermenu-with-a-repeater-control-vb"></a>Repeater Denetimiyle HoverMenu Kullanma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)

> AJAX denetim araç setinde HoverMenu denetimi basit bir açılan efekt sağlar: fare işaretçisi bir öğenin üzerine geldiğinde, belirtilen konumda bir açılan pencere görüntülenir. Bu denetimi bir yineleyici içinde kullanmak da mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde `HoverMenu` denetimi basit bir açılan efekti sağlar: fare işaretçisi bir öğenin üzerine geldiğinde, belirtilen konumda bir açılan pencere görüntülenir. Bu denetimi bir yineleyici içinde kullanmak da mümkündür.

## <a name="steps"></a>Adımlar

Birincisi, bir veri kaynağı gereklidir. Bu örnek, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express sürümünü kullanır. Veritabanı, Visual Studio yüklemesinin (Express Edition dahil) isteğe bağlı bir parçasıdır ve [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir. AdventureWorks veritabanı SQL Server 2005 örnek ve örnek veritabanlarının bir parçasıdır ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D ısplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) kullanmaktır ve `AdventureWorks.mdf` veritabanı dosyasını eklemektir.

Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır. Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

Ardından, sayfaya bir veri kaynağı ekleyin. Sınırlı miktarda veri kullanmak için, AdventureWorks veritabanının satıcı tablosunda yalnızca ilk beş girişi seçersiniz. Veri kaynağını oluşturmak için Visual Studio Yardımcısı 'nı kullanıyorsanız, geçerli sürümdeki bir hatanın `Purchasing`tablo adını (`Vendor`) ön eki olmadığını unutmayın. Aşağıdaki biçimlendirme doğru söz dizimini göstermektedir:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

Artık `HoverMenuExtender` Play 'e geliyor. Böylece veri kaynağındaki her öğe kendi açılan penceresini alır. Bu, Extender 'ın `<ItemTemplate>` bölümü içine alınmalıdır. Biçimlendirme şu şekildedir:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

Artık veri kaynağındaki her öğe, 50 milisaniyelik (`PopDelay` özniteliği) gecikmeden sonra sağ tarafta (`PopupPosition` özniteliği) bir açılan pencere görüntüler.

[![Repeater 'daki her öğenin yanında bulunan vurgulu menü görüntülenir](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)

Yineleyici menü, Repeater 'daki her öğenin yanında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](using-hovermenu-with-a-repeater-control-cs.md)
