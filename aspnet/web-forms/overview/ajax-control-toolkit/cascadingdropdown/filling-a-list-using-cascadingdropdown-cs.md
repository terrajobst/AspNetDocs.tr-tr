---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: (C#) CascadingDropDown kullanarak liste doldurma | Microsoft Docs
author: wenz
description: Bir DropDownList yükleri değişiklikleri anoth değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: a9a3bf12b721c8f5eec21f3090142e40e74b0b9c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395653"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="2a176-103">CascadingDropDown Kullanarak Liste Doldurma (C#)</span><span class="sxs-lookup"><span data-stu-id="2a176-103">Filling a List Using CascadingDropDown (C#)</span></span>

<span data-ttu-id="2a176-104">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2a176-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2a176-105">[Kodu indir](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="2a176-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="2a176-106">Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir.</span><span class="sxs-lookup"><span data-stu-id="2a176-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="2a176-107">(Örneği için BİZE durumları listesini bir liste sağlar ve sonraki listesi, bu durumda bulunan büyük şehirlerin ile doldurulur.) Çözmek için ilk testten bu denetimi kullanarak bir açılan listedeki gerçekten doldurmaktır.</span><span class="sxs-lookup"><span data-stu-id="2a176-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>


## <a name="overview"></a><span data-ttu-id="2a176-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2a176-108">Overview</span></span>

<span data-ttu-id="2a176-109">Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir.</span><span class="sxs-lookup"><span data-stu-id="2a176-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="2a176-110">(Örneği için BİZE durumları listesini bir liste sağlar ve sonraki listesi, bu durumda bulunan büyük şehirlerin ile doldurulur.) Çözmek için ilk testten bu denetimi kullanarak bir açılan listedeki gerçekten doldurmaktır.</span><span class="sxs-lookup"><span data-stu-id="2a176-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="2a176-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="2a176-111">Steps</span></span>

<span data-ttu-id="2a176-112">ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):</span><span class="sxs-lookup"><span data-stu-id="2a176-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="2a176-113">Ardından, bir DropDownList denetimi gereklidir:</span><span class="sxs-lookup"><span data-stu-id="2a176-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="2a176-114">Bu liste için CascadingDropDown genişletici eklenir.</span><span class="sxs-lookup"><span data-stu-id="2a176-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="2a176-115">Ardından listede görüntülenecek girişlerinin listesini döndürür bir web hizmetini zaman uyumsuz bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="2a176-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="2a176-116">Bunun işe yaraması için aşağıdaki CascadingDropDown öznitelikleri ayarlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a176-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="2a176-117">`ServicePath`: Liste girişlerini sunan bir web hizmeti URL'si</span><span class="sxs-lookup"><span data-stu-id="2a176-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="2a176-118">`ServiceMethod`: Liste girişlerini sunan web yöntemi</span><span class="sxs-lookup"><span data-stu-id="2a176-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="2a176-119">`TargetControlID`: Aşağı açılan liste kimliği</span><span class="sxs-lookup"><span data-stu-id="2a176-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="2a176-120">`Category`: Web yöntemi çağrıldığında gönderilen kategori bilgileri</span><span class="sxs-lookup"><span data-stu-id="2a176-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="2a176-121">`PromptText`: Zaman uyumsuz olarak sunucudan liste verilerini yüklerken görüntülenecek metin</span><span class="sxs-lookup"><span data-stu-id="2a176-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="2a176-122">İçin biçimlendirme şöyledir `CascadingDropDown` öğesi.</span><span class="sxs-lookup"><span data-stu-id="2a176-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="2a176-123">C# ve VB arasındaki tek fark ilişkili web hizmeti adıdır:</span><span class="sxs-lookup"><span data-stu-id="2a176-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="2a176-124">Gelen JavaScript kodu `CascadingDropDown` genişletici imzayla bir web hizmeti yöntemi çağırır:</span><span class="sxs-lookup"><span data-stu-id="2a176-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="2a176-125">Önemli bir yönüdür yöntemi türünde bir dizi döndürmek gerekir, bu nedenle `CascadingDropDownNameValue` (ASP.NET AJAX Denetim Araç Seti tarafından tanımlanır).</span><span class="sxs-lookup"><span data-stu-id="2a176-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="2a176-126">İçinde `CascadingDropDownNameValue` oluşturucusu, liste girdinin metin ve değerini sağlanmalıdır, ilk gibi `<option value="VALUE">NAME</option>` HTML yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a176-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="2a176-127">Bazı örnek veriler şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="2a176-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="2a176-128">Tarayıcı sayfa yükleme üç satıcıları ile doldurulacak liste tetikler.</span><span class="sxs-lookup"><span data-stu-id="2a176-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>


<span data-ttu-id="2a176-129">[![Liste otomatik olarak doldurulur.](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2a176-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="2a176-130">Liste otomatik olarak doldurulur ([tam boyutlu görüntüyü görmek için tıklatın](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2a176-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2a176-131">Next</span><span class="sxs-lookup"><span data-stu-id="2a176-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
