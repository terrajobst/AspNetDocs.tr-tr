---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: Dinamik olarak bir Accordion bölmesi ekleme (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle w olarak bildiriliyor...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: be48db5ea3de4af46b0f864cc9e73d2f518294a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598324"
---
# <a name="dynamically-adding-an-accordion-pane-vb"></a>Dinamik olarak bir Accordion bölmesi ekleme (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)

> AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle sayfanın kendisi içinde bildirilmiştir, ancak aynı sonucu elde etmek için sunucu tarafı kod kullanılabilir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle sayfanın kendisi içinde bildirilmiştir, ancak aynı sonucu elde etmek için sunucu tarafı kod kullanılabilir.

## <a name="steps"></a>Adımlar

Accordion denetimi, tüm önemli özellikleri sunucu tarafı koduna sunar. Diğer şeyler arasında `Panes` özelliği, Accordion oluşturan bölmeler koleksiyonuna erişim izni verir. Her bölme `AccordionPane`türü vardır. Bu nedenle, böyle bir bölme oluşturmak bu kadar basit olur:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

`AccordionPane` `HeaderContainer` özelliği, bölmenin üst bilgi bölümünde ASP.NET denetimlerine erişim sağlar; `AccordionPane` `ContentContainer` özelliği, bölmenin içerik bölümü için aynı. Bu, ASP.NET kodunun bölmelere içerik eklemesine izin verir:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

Son olarak, bölmeleri Accordion `Panes` koleksiyonuna eklenmelidir:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

Bir Accordion denetimine iki bölme ekleyen tam bir sunucu tarafı kodu aşağıda verilmiştir:

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

Yalnızca eksik olan öğe, ASP.NET `ScriptManager` denetiminin varlığına bağlı olan Accordion kendisidir:

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

Örneğin, Accordion denetiminde başvurulan iki CSS sınıfı tarayıcıya yönelik stil bilgilerini sağlar:

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]

[![Accordion içindeki veriler, sunucu tarafı kodu tarafından dinamik olarak eklendi](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)

Accordion içindeki veriler, sunucu tarafı kodu tarafından dinamik olarak eklendi ([tam boyutlu görüntüyü görüntülemek Için tıklayın](dynamically-adding-an-accordion-pane-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Öncekini](databinding-to-an-accordion-vb.md)
