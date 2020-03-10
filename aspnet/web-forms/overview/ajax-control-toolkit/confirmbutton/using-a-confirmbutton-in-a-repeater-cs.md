---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: Yineleyicisi Içinde bir ConfirmButton kullanma (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ConfirmButton genişletici, Kullanıcı bir düğmeye tıkladığında (LinkButton denetimi dahil) bir Evet/Hayır açılan penceresi oluşturur. Yalnızca Evet ise...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 468a830f01c48dc39b22bc5d826f80533df65c1a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554287"
---
# <a name="using-a-confirmbutton-in-a-repeater-c"></a>Repeater’da ConfirmButton Kullanma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)

> AJAX denetim araç setinde ConfirmButton genişletici, Kullanıcı bir düğmeye tıkladığında (LinkButton denetimi dahil) bir Evet/Hayır açılan penceresi oluşturur. Yalnızca Evet düğmesine tıklandığında düğme eylemi yürütülür, aksi takdirde iptal edilir. Bu bir yineleyici içinde de mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde ConfirmButton genişletici, Kullanıcı bir düğmeye tıkladığında (LinkButton denetimi dahil) bir Evet/Hayır açılan penceresi oluşturur. Yalnızca Evet düğmesine tıklandığında düğme eylemi yürütülür, aksi takdirde iptal edilir. Bu bir yineleyici içinde de mümkündür.

## <a name="steps"></a>Adımlar

Birincisi, bir veri kaynağı gereklidir. Bu örnek, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express sürümünü kullanır. Veritabanı, Visual Studio yüklemesinin (Express Edition dahil) isteğe bağlı bir parçasıdır ve [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir. AdventureWorks veritabanı SQL Server 2005 örnek ve örnek veritabanlarının bir parçasıdır ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D ısplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) kullanmaktır ve `AdventureWorks.mdf` veritabanı dosyasını eklemektir.

Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır. Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

Ardından, bir veri kaynağı gereklidir. Basitlik sağlamak için, yalnızca AdventureWorks ' satıcıları tablosundaki ilk beş giriş alınır. Veri kaynağını oluşturmak için Visual Studio Sihirbazı 'nı kullanırken, tablo adının (`Vendors`) Şu anda `Purchasing`açık olarak öneki olmadığına unutmayın. Aşağıdaki biçimlendirme doğru bir biçimdir:

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

Bu veri kaynağı, daha sonra bir yineleyici içinde kullanılabilir. Her zamanki gibi `DataBinder.Eval()` yöntemi veri kaynağından veri alır. `ConfirmButtonExtender` denetim, veri kaynağındaki her giriş için görünmesi için yineleyicisi 'nin `<ItemTemplate>` bölümü içine yerleştirilmelidir.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]

[![veri kaynağından her girdinin yanında Onayla düğmesi görünür](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)

Veri kaynağındaki her girdinin yanında Onayla düğmesi görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](using-a-confirmbutton-in-a-repeater-vb.md)
