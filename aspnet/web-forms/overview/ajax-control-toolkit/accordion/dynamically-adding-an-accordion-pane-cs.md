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
# <a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="00c7d-104">Dinamik olarak bir Accordion bölmesi (C#) ekleme</span><span class="sxs-lookup"><span data-stu-id="00c7d-104">Dynamically Adding An Accordion Pane (C#)</span></span>

<span data-ttu-id="00c7d-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="00c7d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="00c7d-106">[Kodu indirin](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="00c7d-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="00c7d-107">AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="00c7d-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="00c7d-108">Panolar genellikle sayfanın kendisi içinde bildirilmiştir, ancak aynı sonucu elde etmek için sunucu tarafı kod kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="00c7d-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="00c7d-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="00c7d-109">Overview</span></span>

<span data-ttu-id="00c7d-110">AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="00c7d-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="00c7d-111">Panolar genellikle sayfanın kendisi içinde bildirilmiştir, ancak aynı sonucu elde etmek için sunucu tarafı kod kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="00c7d-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="00c7d-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="00c7d-112">Steps</span></span>

<span data-ttu-id="00c7d-113">Accordion denetimi, tüm önemli özellikleri sunucu tarafı koduna sunar.</span><span class="sxs-lookup"><span data-stu-id="00c7d-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="00c7d-114">Diğer şeyler arasında `Panes` özelliği, Accordion oluşturan bölmeler koleksiyonuna erişim izni verir.</span><span class="sxs-lookup"><span data-stu-id="00c7d-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="00c7d-115">Her bölme `AccordionPane`türü vardır.</span><span class="sxs-lookup"><span data-stu-id="00c7d-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="00c7d-116">Bu nedenle, böyle bir bölme oluşturmak bu kadar basit olur:</span><span class="sxs-lookup"><span data-stu-id="00c7d-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="00c7d-117">`AccordionPane` `HeaderContainer` özelliği, bölmenin üst bilgi bölümünde ASP.NET denetimlerine erişim sağlar; `AccordionPane` `ContentContainer` özelliği, bölmenin içerik bölümü için aynı.</span><span class="sxs-lookup"><span data-stu-id="00c7d-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="00c7d-118">Bu, ASP.NET kodunun bölmelere içerik eklemesine izin verir:</span><span class="sxs-lookup"><span data-stu-id="00c7d-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="00c7d-119">Son olarak, bölmeleri Accordion `Panes` koleksiyonuna eklenmelidir:</span><span class="sxs-lookup"><span data-stu-id="00c7d-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="00c7d-120">Bir Accordion denetimine iki bölme ekleyen tam bir sunucu tarafı kodu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="00c7d-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="00c7d-121">Yalnızca eksik olan öğe, ASP.NET `ScriptManager` denetiminin varlığına bağlı olan Accordion kendisidir:</span><span class="sxs-lookup"><span data-stu-id="00c7d-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="00c7d-122">Örneğin, Accordion denetiminde başvurulan iki CSS sınıfı tarayıcıya yönelik stil bilgilerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="00c7d-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

<span data-ttu-id="00c7d-123">[![Accordion içindeki veriler, sunucu tarafı kodu tarafından dinamik olarak eklendi](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="00c7d-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span></span>

<span data-ttu-id="00c7d-124">Accordion içindeki veriler, sunucu tarafı kodu tarafından dinamik olarak eklendi ([tam boyutlu görüntüyü görüntülemek Için tıklayın](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="00c7d-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="00c7d-125">[Önceki](databinding-to-an-accordion-cs.md)
> [İleri](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="00c7d-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
