---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: Basamaklı Dingdropdown ile liste girişlerini önceden ayarlama (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Basamakarda açılan menü denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin ilişkili değerleri anormal bir şekilde yükler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bb4a51092534e6fddbd40f868c53c58d12eef2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597904"
---
# <a name="presetting-list-entries-with-cascadingdropdown-c"></a><span data-ttu-id="f83af-103">CascadingDropDown ile Liste Girişlerini Önceden Ayarlama (C#)</span><span class="sxs-lookup"><span data-stu-id="f83af-103">Presetting List Entries with CascadingDropDown (C#)</span></span>

<span data-ttu-id="f83af-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="f83af-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f83af-105">[Kodu indirin](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f83af-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span></span>

> <span data-ttu-id="f83af-106">AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler.</span><span class="sxs-lookup"><span data-stu-id="f83af-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="f83af-107">Çok az kod ile, veriler dinamik olarak yüklendikten sonra bir liste öğesinin önceden seçilmesi mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f83af-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="overview"></a><span data-ttu-id="f83af-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="f83af-108">Overview</span></span>

<span data-ttu-id="f83af-109">AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler.</span><span class="sxs-lookup"><span data-stu-id="f83af-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="f83af-110">(Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Çok az kod ile, veriler dinamik olarak yüklendikten sonra bir liste öğesinin önceden seçilmesi mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f83af-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="f83af-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="f83af-111">Steps</span></span>

<span data-ttu-id="f83af-112">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="f83af-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="f83af-113">Ardından, bir DropDownList denetimi gereklidir:</span><span class="sxs-lookup"><span data-stu-id="f83af-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="f83af-114">Bu liste için, Web hizmeti URL 'SI ve yöntem bilgileri sağlayan bir basamaklı Dinglist genişletici eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="f83af-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="f83af-115">Basamaklı Dingdropdown genişletici, daha sonra aşağıdaki yöntem imzasıyla bir Web hizmetini zaman uyumsuz olarak çağırır:</span><span class="sxs-lookup"><span data-stu-id="f83af-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="f83af-116">Yöntemi, basamaklı Dingdropdown değeri türünde bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83af-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="f83af-117">Türün Oluşturucusu önce liste girişinin başlığını ve ardından değeri (HTML `value` özniteliği) bekler.</span><span class="sxs-lookup"><span data-stu-id="f83af-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="f83af-118">Üçüncü bağımsız değişken true olarak ayarlanırsa, tarayıcıda liste öğesi otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="f83af-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="f83af-119">Sayfanın tarayıcıda yüklenmesi, açılan listeyi üç satıcı ile doldurur, ikincisi ise önceden seçilir.</span><span class="sxs-lookup"><span data-stu-id="f83af-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>

<span data-ttu-id="f83af-120">[![liste doldurulur ve otomatik olarak önceden seçilir](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f83af-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="f83af-121">Liste doldurulur ve otomatik olarak önceden seçilir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f83af-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f83af-122">[Önceki](using-cascadingdropdown-with-a-database-cs.md)
> [İleri](using-auto-postback-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f83af-122">[Previous](using-cascadingdropdown-with-a-database-cs.md)
[Next](using-auto-postback-with-cascadingdropdown-cs.md)</span></span>
