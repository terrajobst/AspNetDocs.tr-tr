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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607192"
---
# <a name="dynamically-adding-an-accordion-pane-vb"></a><span data-ttu-id="bbe45-104">Dinamik olarak bir Accordion bölmesi ekleme (VB)</span><span class="sxs-lookup"><span data-stu-id="bbe45-104">Dynamically Adding An Accordion Pane (VB)</span></span>

<span data-ttu-id="bbe45-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="bbe45-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="bbe45-106">[Kodu indirin](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="bbe45-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span></span>

> <span data-ttu-id="bbe45-107">AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bbe45-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="bbe45-108">Panolar genellikle sayfanın kendisi içinde bildirilmiştir, ancak aynı sonucu elde etmek için sunucu tarafı kod kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bbe45-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="bbe45-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="bbe45-109">Overview</span></span>

<span data-ttu-id="bbe45-110">AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bbe45-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="bbe45-111">Panolar genellikle sayfanın kendisi içinde bildirilmiştir, ancak aynı sonucu elde etmek için sunucu tarafı kod kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bbe45-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="bbe45-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="bbe45-112">Steps</span></span>

<span data-ttu-id="bbe45-113">Accordion denetimi, tüm önemli özellikleri sunucu tarafı koduna sunar.</span><span class="sxs-lookup"><span data-stu-id="bbe45-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="bbe45-114">Diğer şeyler arasında `Panes` özelliği, Accordion oluşturan bölmeler koleksiyonuna erişim izni verir.</span><span class="sxs-lookup"><span data-stu-id="bbe45-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="bbe45-115">Her bölme `AccordionPane`türü vardır.</span><span class="sxs-lookup"><span data-stu-id="bbe45-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="bbe45-116">Bu nedenle, böyle bir bölme oluşturmak bu kadar basit olur:</span><span class="sxs-lookup"><span data-stu-id="bbe45-116">It is therefore trivial to create such a pane:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

<span data-ttu-id="bbe45-117">`AccordionPane` `HeaderContainer` özelliği, bölmenin üst bilgi bölümünde ASP.NET denetimlerine erişim sağlar; `AccordionPane` `ContentContainer` özelliği, bölmenin içerik bölümü için aynı.</span><span class="sxs-lookup"><span data-stu-id="bbe45-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="bbe45-118">Bu, ASP.NET kodunun bölmelere içerik eklemesine izin verir:</span><span class="sxs-lookup"><span data-stu-id="bbe45-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

<span data-ttu-id="bbe45-119">Son olarak, bölmeleri Accordion `Panes` koleksiyonuna eklenmelidir:</span><span class="sxs-lookup"><span data-stu-id="bbe45-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

<span data-ttu-id="bbe45-120">Bir Accordion denetimine iki bölme ekleyen tam bir sunucu tarafı kodu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bbe45-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

<span data-ttu-id="bbe45-121">Yalnızca eksik olan öğe, ASP.NET `ScriptManager` denetiminin varlığına bağlı olan Accordion kendisidir:</span><span class="sxs-lookup"><span data-stu-id="bbe45-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

<span data-ttu-id="bbe45-122">Örneğin, Accordion denetiminde başvurulan iki CSS sınıfı tarayıcıya yönelik stil bilgilerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="bbe45-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]

<span data-ttu-id="bbe45-123">[![Accordion içindeki veriler, sunucu tarafı kodu tarafından dinamik olarak eklendi](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bbe45-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span></span>

<span data-ttu-id="bbe45-124">Accordion içindeki veriler, sunucu tarafı kodu tarafından dinamik olarak eklendi ([tam boyutlu görüntüyü görüntülemek Için tıklayın](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="bbe45-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bbe45-125">Öncekini</span><span class="sxs-lookup"><span data-stu-id="bbe45-125">Previous</span></span>](databinding-to-an-accordion-vb.md)
