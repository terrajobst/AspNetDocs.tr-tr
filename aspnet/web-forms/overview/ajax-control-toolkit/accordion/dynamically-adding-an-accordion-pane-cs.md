---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: Dinamik olarak bir Accordion bölmesi (C#) ekleme | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle w olarak bildiriliyor...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 2834f56bd77c412923f4a8f382e670727f70eae4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607231"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a>Dinamik olarak bir Accordion bölmesi (C#) ekleme

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)

> AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle sayfanın kendisi içinde bildirilmiştir, ancak aynı sonucu elde etmek için sunucu tarafı kod kullanılabilir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle sayfanın kendisi içinde bildirilmiştir, ancak aynı sonucu elde etmek için sunucu tarafı kod kullanılabilir.

## <a name="steps"></a>Adımlar

Accordion denetimi, tüm önemli özellikleri sunucu tarafı koduna sunar. Diğer şeyler arasında `Panes` özelliği, Accordion oluşturan bölmeler koleksiyonuna erişim izni verir. Her bölme `AccordionPane`türü vardır. Bu nedenle, böyle bir bölme oluşturmak bu kadar basit olur:

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

`AccordionPane` `HeaderContainer` özelliği, bölmenin üst bilgi bölümünde ASP.NET denetimlerine erişim sağlar; `AccordionPane` `ContentContainer` özelliği, bölmenin içerik bölümü için aynı. Bu, ASP.NET kodunun bölmelere içerik eklemesine izin verir:

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

Son olarak, bölmeleri Accordion `Panes` koleksiyonuna eklenmelidir:

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

Bir Accordion denetimine iki bölme ekleyen tam bir sunucu tarafı kodu aşağıda verilmiştir:

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

Yalnızca eksik olan öğe, ASP.NET `ScriptManager` denetiminin varlığına bağlı olan Accordion kendisidir:

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

Örneğin, Accordion denetiminde başvurulan iki CSS sınıfı tarayıcıya yönelik stil bilgilerini sağlar:

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

[![Accordion içindeki veriler, sunucu tarafı kodu tarafından dinamik olarak eklendi](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

Accordion içindeki veriler, sunucu tarafı kodu tarafından dinamik olarak eklendi ([tam boyutlu görüntüyü görüntülemek Için tıklayın](dynamically-adding-an-accordion-pane-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](databinding-to-an-accordion-cs.md)
> [İleri](databinding-to-an-accordion-vb.md)
