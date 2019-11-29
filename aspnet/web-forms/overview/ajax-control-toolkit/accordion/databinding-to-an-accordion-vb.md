---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: Bir Accordion 'a veri bağlama (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle w olarak bildiriliyor...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: bfb31940c0395c7ed1d5d471fb8fb686b66c59ad
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599978"
---
# <a name="databinding-to-an-accordion-vb"></a>Bir Accordion’a Veri Bağlama (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)

> AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle sayfanın kendisi içinde gösterilir, ancak bir veri kaynağına bağlama daha fazla esneklik sağlar.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle sayfanın kendisi içinde gösterilir, ancak bir veri kaynağına bağlama daha fazla esneklik sağlar.

## <a name="steps"></a>Adımlar

Birincisi, bir veri kaynağı gereklidir. Bu örnek, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express sürümünü kullanır. Veritabanı, Visual Studio yüklemesinin (Express Edition dahil) isteğe bağlı bir parçasıdır ve [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir. AdventureWorks veritabanı SQL Server 2005 örnek ve örnek veritabanlarının bir parçasıdır ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D ısplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) kullanmaktır ve `AdventureWorks.mdf` veritabanı dosyasını eklemektir.

Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır. Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

Ardından, sayfaya bir veri kaynağı ekleyin. Sınırlı miktarda veri kullanmak için, AdventureWorks veritabanının satıcı tablosunda yalnızca ilk beş girişi seçersiniz. Veri kaynağını oluşturmak için Visual Studio Yardımcısı 'nı kullanıyorsanız, geçerli sürümdeki bir hatanın `Purchasing`tablo adını (`Vendor`) ön eki olmadığını unutmayın. Aşağıdaki biçimlendirme doğru söz dizimini göstermektedir:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

Veri kaynağının adını (ID) unutmayın. Bu çok tanımlayıcı daha sonra Accordion denetiminin `DataSourceID` özelliğinde kullanılmalıdır:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

Accordion denetimi içinde, üst bilgi (`<HeaderTemplate>`) ve içerik (`<ContentTemplate>`) dahil olmak üzere, denetimin çeşitli bölümlerine yönelik şablonlar sağlayabilirsiniz. Bu öğeler içinde, `DataBinder.Eval()` yöntemi kullanarak verileri veri kaynağından çıkış yapmanız yeterlidir:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

Sayfa yüklendiğinde, veri kaynağının bu sunucu tarafı koduyla Accordion 'e bağlanması gerekir:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

Bu örneği sonuçlandırma için, Accordion denetiminde (özelliklerinde `HeaderCssClass` ve `ContentCssClass`) başvurulan iki CSS sınıfını tanımlamanız gerekir. Aşağıdaki biçimlendirmeyi sayfanın `<head>` bölümüne koyun:

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]

[Accordion içindeki verilerin ![doğrudan veri kaynağından gelir](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)

Accordion içindeki veriler doğrudan veri kaynağından gelir ([tam boyutlu görüntüyü görüntülemek Için tıklatın](databinding-to-an-accordion-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](dynamically-adding-an-accordion-pane-cs.md)
> [İleri](dynamically-adding-an-accordion-pane-vb.md)
