---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: (VB) doğrulama denetimleri ile TextBoxWatermark kullanma | Microsoft Docs
author: wenz
description: Bir metin kutusu içinde gösterilir böylece AJAX Denetim Araç Seti TextBoxWatermark denetiminde metin kutusunu genişletir. Bir kullanıcı kutusuna tıkladığında, ben...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: d83fb53ddb40a31013bc724909fa149ce2e4c713
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59387388"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a><span data-ttu-id="d5f14-104">Doğrulama Denetimleri ile TextBoxWatermark Kullanma (VB)</span><span class="sxs-lookup"><span data-stu-id="d5f14-104">Using TextBoxWatermark With Validation Controls (VB)</span></span>

<span data-ttu-id="d5f14-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d5f14-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d5f14-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d5f14-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span></span>

> <span data-ttu-id="d5f14-107">Bir metin kutusu içinde gösterilir böylece AJAX Denetim Araç Seti TextBoxWatermark denetiminde metin kutusunu genişletir.</span><span class="sxs-lookup"><span data-stu-id="d5f14-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="d5f14-108">Kullanıcı kutusuna tıkladığında boşaltılır.</span><span class="sxs-lookup"><span data-stu-id="d5f14-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="d5f14-109">Kullanıcının metin girmeden kutusu ayrılırsa doldurulmuş metni görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d5f14-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="d5f14-110">Bu aynı sayfa üzerinde ASP.NET doğrulama denetimleri ile çakışabilir, ancak bu sorunları gidermek.</span><span class="sxs-lookup"><span data-stu-id="d5f14-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>


## <a name="overview"></a><span data-ttu-id="d5f14-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d5f14-111">Overview</span></span>

<span data-ttu-id="d5f14-112">`TextBoxWatermark` AJAX Denetim Araç Seti denetiminde metin kutusuna bir metin kutusu içinde gösterilir böylece genişletir.</span><span class="sxs-lookup"><span data-stu-id="d5f14-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="d5f14-113">Kullanıcı kutusuna tıkladığında boşaltılır.</span><span class="sxs-lookup"><span data-stu-id="d5f14-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="d5f14-114">Kullanıcının metin girmeden kutusu ayrılırsa doldurulmuş metni görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d5f14-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="d5f14-115">Bu aynı sayfa üzerinde ASP.NET doğrulama denetimleri ile çakışabilir, ancak bu sorunları gidermek.</span><span class="sxs-lookup"><span data-stu-id="d5f14-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="d5f14-116">Adımlar</span><span class="sxs-lookup"><span data-stu-id="d5f14-116">Steps</span></span>

<span data-ttu-id="d5f14-117">Temel kurulum örnek aşağıda verilmiştir: bir `TextBox` denetimi Filigran kullanarak bir `TextBoxWatermarkExtender` denetimi.</span><span class="sxs-lookup"><span data-stu-id="d5f14-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="d5f14-118">Bir düğme, bir geri gönderme tetikler ve daha sonra sayfasında doğrulama denetimlerini tetiklemek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="d5f14-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="d5f14-119">Ayrıca, bir `ScriptManager` denetimi, ASP.NET AJAX başlatmak için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="d5f14-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="d5f14-120">Şimdi ekleyin bir `RequiredFieldValidator` olup metin alanı form gönderildiğinde denetleyen denetimi.</span><span class="sxs-lookup"><span data-stu-id="d5f14-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="d5f14-121">`InitialValue` Doğrulayıcı özelliğini ayarlayın, kullanılan aynı değere `TextBoxWatermarkExtender` denetimi: Form gönderildiğinde, değişmeyen bir metin kutusu içindeki eşik değerini değeridir:</span><span class="sxs-lookup"><span data-stu-id="d5f14-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="d5f14-122">Ancak bu yaklaşım ile ilgili bir sorun yoktur: JavaScript istemci devre dışı bırakır, metin alanı filigran metni ile bu nedenle doldurulmuş değil `RequiredFieldValidator` bir hata iletisi tetiklemez.</span><span class="sxs-lookup"><span data-stu-id="d5f14-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="d5f14-123">Bu nedenle, ikinci `RequiredFieldValidator` denetimi gereklidir, bir boş metin kutusunu denetler (atlama `InitialValue` özniteliği).</span><span class="sxs-lookup"><span data-stu-id="d5f14-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="d5f14-124">Her iki doğrulayıcıları kullandığından `Display` = `"Dynamic"`, son kullanıcının hangi iki doğrulayıcıları harekete geçirildi görsel görünümünü ayırt edemez; bunun yerine, olduğu gibi yalnızca bunlardan birinin arar.</span><span class="sxs-lookup"><span data-stu-id="d5f14-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="d5f14-125">Son olarak, bir hata iletisi Doğrulayıcı verilen, alandaki metin çıktısını almak için bazı sunucu tarafı kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d5f14-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]


[![T<span data-ttu-id="d5f14-126">He Doğrulayıcı alanı metin olduğunu şeklinde hata verir]</span><span class="sxs-lookup"><span data-stu-id="d5f14-126">he validator complains that there is no text in the field]</span></span>(using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

<span data-ttu-id="d5f14-127">Doğrulayıcı alanı metin olduğunu şeklinde hata verir ([tam boyutlu görüntüyü görmek için tıklatın](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d5f14-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d5f14-128">Önceki</span><span class="sxs-lookup"><span data-stu-id="d5f14-128">Previous</span></span>](using-textboxwatermark-in-a-formview-vb.md)
