---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: Istemci kodundan DropShadow özelliklerini düzenleme (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir. Bu genişleticin özellikleri, istemci Javano kullanılarak da değiştirilebilir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613801"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="88c4a-104">İstemci Kodundan DropShadow Özelliklerini Düzenleme (VB)</span><span class="sxs-lookup"><span data-stu-id="88c4a-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>

<span data-ttu-id="88c4a-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="88c4a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="88c4a-106">[Kodu indirin](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="88c4a-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="88c4a-107">AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir.</span><span class="sxs-lookup"><span data-stu-id="88c4a-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="88c4a-108">Bu genişleticin özellikleri, istemci JavaScript kodu kullanılarak da değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="88c4a-108">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="88c4a-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="88c4a-109">Overview</span></span>

<span data-ttu-id="88c4a-110">AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir.</span><span class="sxs-lookup"><span data-stu-id="88c4a-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="88c4a-111">Bu genişleticin özellikleri, istemci JavaScript kodu kullanılarak da değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="88c4a-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="88c4a-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="88c4a-112">Steps</span></span>

<span data-ttu-id="88c4a-113">Kod, bazı metin satırları içeren bir panelle başlar:</span><span class="sxs-lookup"><span data-stu-id="88c4a-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="88c4a-114">İlişkili CSS sınıfı, paneli iyi bir arka plan rengi sağlar:</span><span class="sxs-lookup"><span data-stu-id="88c4a-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="88c4a-115">`DropShadowExtender`, paneli bir gölge efektiyle genişletmek için eklenir, opaklık %50 olarak ayarlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="88c4a-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="88c4a-116">Ardından, ASP.NET AJAX `ScriptManager` denetimi denetim araç setinin çalışmasını sağlar:</span><span class="sxs-lookup"><span data-stu-id="88c4a-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="88c4a-117">Diğer bir panel, gölge geçirgenliğini ayarlamak için iki JavaScript bağlantısı içerir: eksi bağlantı, gölgenin saydamlığını düşürür, artı bağlantısı onu arttırır.</span><span class="sxs-lookup"><span data-stu-id="88c4a-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="88c4a-118">JavaScript işlevi `changeOpacity()` önce sayfada `DropShadowExtender` denetimini bulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="88c4a-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="88c4a-119">ASP.NET AJAX, tam olarak bu görevin `$find()` yöntemini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="88c4a-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="88c4a-120">Ardından `get_Opacity()` yöntemi geçerli opaklığı alır, `set_Opacity()` yöntemi bunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="88c4a-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="88c4a-121">JavaScript kodu daha sonra `<label>` öğesinde geçerli opaklık değerini koyar:</span><span class="sxs-lookup"><span data-stu-id="88c4a-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

<span data-ttu-id="88c4a-122">[![opaklık istemci tarafında değiştirildi](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="88c4a-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="88c4a-123">Opaklık, istemci tarafında değişir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="88c4a-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="88c4a-124">Öncekini</span><span class="sxs-lookup"><span data-stu-id="88c4a-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
