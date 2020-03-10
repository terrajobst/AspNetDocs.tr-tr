---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: Basamaklı Dingdropdown (C#) kullanarak bir listeyi doldurma | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Basamakarda açılan menü denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin ilişkili değerleri anormal bir şekilde yükler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614214"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="63434-103">CascadingDropDown Kullanarak Liste Doldurma (C#)</span><span class="sxs-lookup"><span data-stu-id="63434-103">Filling a List Using CascadingDropDown (C#)</span></span>

<span data-ttu-id="63434-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="63434-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="63434-105">[Kodu indirin](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="63434-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="63434-106">AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler.</span><span class="sxs-lookup"><span data-stu-id="63434-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="63434-107">(Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Çözecek ilk zorluk, bu denetimi kullanarak bir açılan listeyi gerçekten doldurmektir.</span><span class="sxs-lookup"><span data-stu-id="63434-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="63434-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="63434-108">Overview</span></span>

<span data-ttu-id="63434-109">AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler.</span><span class="sxs-lookup"><span data-stu-id="63434-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="63434-110">(Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Çözecek ilk zorluk, bu denetimi kullanarak bir açılan listeyi gerçekten doldurmektir.</span><span class="sxs-lookup"><span data-stu-id="63434-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="63434-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="63434-111">Steps</span></span>

<span data-ttu-id="63434-112">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="63434-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="63434-113">Ardından, bir DropDownList denetimi gereklidir:</span><span class="sxs-lookup"><span data-stu-id="63434-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="63434-114">Bu liste için, basamaklı bir açılan menü Genişleticisi eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="63434-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="63434-115">Bu işlem, bir Web hizmetine zaman uyumsuz bir istek gönderir ve ardından listede görüntülenecek girişlerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="63434-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="63434-116">Bunun çalışması için, aşağıdaki basamaklı Dingdropdown özniteliklerinin ayarlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="63434-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="63434-117">`ServicePath`: liste girdilerini sunan bir Web hizmetinin URL 'SI</span><span class="sxs-lookup"><span data-stu-id="63434-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="63434-118">`ServiceMethod`: liste girdilerini teslim eden Web yöntemi</span><span class="sxs-lookup"><span data-stu-id="63434-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="63434-119">`TargetControlID`: açılan listenin KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="63434-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="63434-120">`Category`: çağrıldığında Web yöntemine gönderilen kategori bilgileri</span><span class="sxs-lookup"><span data-stu-id="63434-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="63434-121">`PromptText`: sunucudan zaman uyumsuz olarak liste verileri yüklenirken görünen metin</span><span class="sxs-lookup"><span data-stu-id="63434-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="63434-122">`CascadingDropDown` öğesi için biçimlendirme aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="63434-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="63434-123">Ve VB arasındaki C# tek fark, ilişkili Web hizmetinin adıdır:</span><span class="sxs-lookup"><span data-stu-id="63434-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="63434-124">`CascadingDropDown` genişleticinizden gelen JavaScript kodu, aşağıdaki imzayla bir Web hizmeti yöntemini çağırır:</span><span class="sxs-lookup"><span data-stu-id="63434-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="63434-125">Bu nedenle, yöntemin `CascadingDropDownNameValue` türünde bir dizi döndürmesi gerekir (ASP.NET AJAX denetim araç seti tarafından tanımlanır).</span><span class="sxs-lookup"><span data-stu-id="63434-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="63434-126">`CascadingDropDownNameValue` oluşturucusunda, ilk olarak liste girişinin metni ve ardından değeri, `<option value="VALUE">NAME</option>` HTML içinde olduğu gibi belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="63434-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="63434-127">Örnek veriler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="63434-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="63434-128">Sayfanın tarayıcıya yüklenmesi, listenin üç satıcı ile doldurulduğu şekilde tetiklenecek.</span><span class="sxs-lookup"><span data-stu-id="63434-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="63434-129">[![liste otomatik olarak doldurulur](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="63434-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="63434-130">Liste otomatik olarak doldurulur ([tam boyutlu görüntüyü görüntülemek Için tıklayın](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="63434-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="63434-131">Next</span><span class="sxs-lookup"><span data-stu-id="63434-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
