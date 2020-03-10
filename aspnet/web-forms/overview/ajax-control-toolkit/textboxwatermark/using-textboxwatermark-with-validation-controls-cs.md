---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: Doğrulama denetimleriyle Textboxfiligran kullanma (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde Textboxfiligran denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir. Bir Kullanıcı, kutuya tıkladığında ben...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: bc9498b1c5ba2f38b90706c9200ffa813a945fa9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78577842"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a><span data-ttu-id="4bc15-104">Doğrulama Denetimleri ile TextBoxWatermark Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="4bc15-104">Using TextBoxWatermark With Validation Controls (C#)</span></span>

<span data-ttu-id="4bc15-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="4bc15-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4bc15-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4bc15-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span></span>

> <span data-ttu-id="4bc15-107">AJAX denetim araç setinde Textboxfiligran denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4bc15-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="4bc15-108">Kullanıcı, kutuya tıkladığında boşaltılır.</span><span class="sxs-lookup"><span data-stu-id="4bc15-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="4bc15-109">Kullanıcı metin girmeden kutudan ayrılsa, önceden doldurulmuş metin yeniden görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4bc15-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="4bc15-110">Bu, aynı sayfada ASP.NET doğrulama denetimleriyle çakışmayabilir, ancak bu sorunlar ele alınabilir.</span><span class="sxs-lookup"><span data-stu-id="4bc15-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="overview"></a><span data-ttu-id="4bc15-111">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="4bc15-111">Overview</span></span>

<span data-ttu-id="4bc15-112">AJAX denetim araç setinde `TextBoxWatermark` denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4bc15-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="4bc15-113">Kullanıcı, kutuya tıkladığında boşaltılır.</span><span class="sxs-lookup"><span data-stu-id="4bc15-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="4bc15-114">Kullanıcı metin girmeden kutudan ayrılsa, önceden doldurulmuş metin yeniden görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4bc15-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="4bc15-115">Bu, aynı sayfada ASP.NET doğrulama denetimleriyle çakışmayabilir, ancak bu sorunlar ele alınabilir.</span><span class="sxs-lookup"><span data-stu-id="4bc15-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="4bc15-116">Adımlar</span><span class="sxs-lookup"><span data-stu-id="4bc15-116">Steps</span></span>

<span data-ttu-id="4bc15-117">Örneğin temel kurulumu aşağıda verilmiştir: bir `TextBox` denetim, bir `TextBoxWatermarkExtender` denetimi kullanılarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="4bc15-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="4bc15-118">Bir düğme geri göndermeyi tetikler ve daha sonra sayfadaki doğrulama denetimlerini tetiklemek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="4bc15-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="4bc15-119">Ayrıca, ASP.NET AJAX 'u başlatmak için bir `ScriptManager` denetimi gereklidir:</span><span class="sxs-lookup"><span data-stu-id="4bc15-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="4bc15-120">Şimdi, form gönderildiğinde alanda metin olup olmadığını denetleyen `RequiredFieldValidator` bir denetim ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4bc15-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="4bc15-121">Doğrulayıcının `InitialValue` özelliği, `TextBoxWatermarkExtender` denetiminde kullanılan değere ayarlanmalıdır: form gönderildiğinde, değiştirilmemiş bir metin kutusunun değeri, içindeki filigran değeridir:</span><span class="sxs-lookup"><span data-stu-id="4bc15-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="4bc15-122">Bununla birlikte, bu yaklaşımda bir sorun var: istemci JavaScript 'ı devre dışı bırakrsa, metin alanı filigran metniyle önceden doldurulmamışsa `RequiredFieldValidator` bir hata mesajı tetiklemez.</span><span class="sxs-lookup"><span data-stu-id="4bc15-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="4bc15-123">Bu nedenle, boş bir metin kutusunu (`InitialValue` özniteliğini atlayarak) denetleyen ikinci bir `RequiredFieldValidator` denetimi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4bc15-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="4bc15-124">Her iki doğrulayıcılar de `Display`=`"Dynamic"`kullandığından, Son Kullanıcı iki doğrulayıcıların harekete geçirildiği görsel görünümü ayırt edemez; Bunun yerine, bunlardan yalnızca biri vardı.</span><span class="sxs-lookup"><span data-stu-id="4bc15-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="4bc15-125">Son olarak, bir hata iletisi verildiyse, alandaki metnin çıktısını almak için bazı sunucu tarafı kod ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4bc15-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="4bc15-126">[Doğrulayıcı ![alanda metin yok](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4bc15-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="4bc15-127">Doğrulayıcı, alanda metin yok ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4bc15-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4bc15-128">[Önceki](using-textboxwatermark-in-a-formview-cs.md)
> [İleri](using-textboxwatermark-in-a-formview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4bc15-128">[Previous](using-textboxwatermark-in-a-formview-cs.md)
[Next](using-textboxwatermark-in-a-formview-vb.md)</span></span>
