---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: Basamaklı Dingdropdown kullanarak liste doldurma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Basamakarda açılan menü denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin ilişkili değerleri anormal bir şekilde yükler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 8dd9ef8a4bdf705ba4451b7fd240e4de8618221c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536010"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="d30f9-103">CascadingDropDown Kullanarak Liste Doldurma (VB)</span><span class="sxs-lookup"><span data-stu-id="d30f9-103">Filling a List Using CascadingDropDown (VB)</span></span>

<span data-ttu-id="d30f9-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="d30f9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d30f9-105">[Kodu indirin](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d30f9-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="d30f9-106">AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler.</span><span class="sxs-lookup"><span data-stu-id="d30f9-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="d30f9-107">(Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Çözecek ilk zorluk, bu denetimi kullanarak bir açılan listeyi gerçekten doldurmektir.</span><span class="sxs-lookup"><span data-stu-id="d30f9-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="d30f9-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="d30f9-108">Overview</span></span>

<span data-ttu-id="d30f9-109">AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler.</span><span class="sxs-lookup"><span data-stu-id="d30f9-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="d30f9-110">(Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Çözecek ilk zorluk, bu denetimi kullanarak bir açılan listeyi gerçekten doldurmektir.</span><span class="sxs-lookup"><span data-stu-id="d30f9-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="d30f9-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="d30f9-111">Steps</span></span>

<span data-ttu-id="d30f9-112">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="d30f9-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="d30f9-113">Ardından, bir DropDownList denetimi gereklidir:</span><span class="sxs-lookup"><span data-stu-id="d30f9-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="d30f9-114">Bu liste için, basamaklı bir açılan menü Genişleticisi eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="d30f9-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="d30f9-115">Bu işlem, bir Web hizmetine zaman uyumsuz bir istek gönderir ve ardından listede görüntülenecek girişlerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="d30f9-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="d30f9-116">Bunun çalışması için, aşağıdaki basamaklı Dingdropdown özniteliklerinin ayarlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d30f9-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="d30f9-117">`ServicePath`: liste girdilerini sunan bir Web hizmetinin URL 'SI</span><span class="sxs-lookup"><span data-stu-id="d30f9-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="d30f9-118">`ServiceMethod`: liste girdilerini teslim eden Web yöntemi</span><span class="sxs-lookup"><span data-stu-id="d30f9-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="d30f9-119">`TargetControlID`: açılan listenin KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="d30f9-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="d30f9-120">`Category`: çağrıldığında Web yöntemine gönderilen kategori bilgileri</span><span class="sxs-lookup"><span data-stu-id="d30f9-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="d30f9-121">`PromptText`: sunucudan zaman uyumsuz olarak liste verileri yüklenirken görünen metin</span><span class="sxs-lookup"><span data-stu-id="d30f9-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="d30f9-122">`CascadingDropDown` öğesi için biçimlendirme aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d30f9-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="d30f9-123">Ve VB arasındaki C# tek fark, ilişkili Web hizmetinin adıdır:</span><span class="sxs-lookup"><span data-stu-id="d30f9-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="d30f9-124">`CascadingDropDown` genişleticinizden gelen JavaScript kodu, aşağıdaki imzayla bir Web hizmeti yöntemini çağırır:</span><span class="sxs-lookup"><span data-stu-id="d30f9-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="d30f9-125">Bu nedenle, yöntemin `CascadingDropDownNameValue` türünde bir dizi döndürmesi gerekir (ASP.NET AJAX denetim araç seti tarafından tanımlanır).</span><span class="sxs-lookup"><span data-stu-id="d30f9-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="d30f9-126">`CascadingDropDownNameValue` oluşturucusunda, ilk olarak liste girişinin metni ve ardından değeri, `<option value="VALUE">NAME</option>` HTML içinde olduğu gibi belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d30f9-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="d30f9-127">Örnek veriler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d30f9-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="d30f9-128">Sayfanın tarayıcıya yüklenmesi, listenin üç satıcı ile doldurulduğu şekilde tetiklenecek.</span><span class="sxs-lookup"><span data-stu-id="d30f9-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="d30f9-129">[![liste otomatik olarak doldurulur](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d30f9-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="d30f9-130">Liste otomatik olarak doldurulur ([tam boyutlu görüntüyü görüntülemek Için tıklayın](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d30f9-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d30f9-131">[Önceki](using-auto-postback-with-cascadingdropdown-cs.md)
> [İleri](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d30f9-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
