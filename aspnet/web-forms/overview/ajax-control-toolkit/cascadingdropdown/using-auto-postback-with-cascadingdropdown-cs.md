---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: Basamaklı Dingdropdown ile otomatik geri gönderme kullanma (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Basamakarda açılan menü denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin ilişkili değerleri anormal bir şekilde yükler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574521"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a><span data-ttu-id="b68e0-103">CascadingDropDown ile Otomatik Geri Gönderme Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="b68e0-103">Using Auto-Postback with CascadingDropDown (C#)</span></span>

<span data-ttu-id="b68e0-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="b68e0-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b68e0-105">[Kodu indirin](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b68e0-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span></span>

> <span data-ttu-id="b68e0-106">AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler.</span><span class="sxs-lookup"><span data-stu-id="b68e0-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="b68e0-107">Ancak, basamaklı Dingdropdown denetimini kullanırken, ASP. Veriye zaman uyumsuz olarak veri yüklemesi (gereksiz) geri gönderme oluşturduğundan, NET 'in DropDownList denetiminin AutoPostBack özelliği çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="b68e0-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="b68e0-108">Bazı JavaScript kodları ile bu etkilerden kaçınılabilir.</span><span class="sxs-lookup"><span data-stu-id="b68e0-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="b68e0-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="b68e0-109">Overview</span></span>

<span data-ttu-id="b68e0-110">AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler.</span><span class="sxs-lookup"><span data-stu-id="b68e0-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="b68e0-111">(Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Ancak, basamaklı Dingdropdown denetimini kullanırken, ASP. Veriye zaman uyumsuz olarak veri yüklemesi (gereksiz) geri gönderme oluşturduğundan, NET 'in DropDownList denetiminin AutoPostBack özelliği çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="b68e0-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="b68e0-112">Bazı JavaScript kodları ile bu etkilerden kaçınılabilir.</span><span class="sxs-lookup"><span data-stu-id="b68e0-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="b68e0-113">Adımlar</span><span class="sxs-lookup"><span data-stu-id="b68e0-113">Steps</span></span>

<span data-ttu-id="b68e0-114">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak &lt;`form`&gt; öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="b68e0-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="b68e0-115">Ardından, bir DropDownList denetimi gereklidir:</span><span class="sxs-lookup"><span data-stu-id="b68e0-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="b68e0-116">Bu liste için, Web hizmeti URL 'SI ve yöntem bilgileri sağlayan bir basamaklı Dinglist genişletici eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="b68e0-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="b68e0-117">Basamaklı Dingdropdown genişletici, daha sonra aşağıdaki yöntem imzasıyla bir Web hizmetini zaman uyumsuz olarak çağırır:</span><span class="sxs-lookup"><span data-stu-id="b68e0-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="b68e0-118">Yöntemi, basamaklı Dingdropdown değeri türünde bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="b68e0-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="b68e0-119">Türün Oluşturucusu önce liste girişinin başlığını ve ardından değeri (HTML `value` özniteliği) bekler.</span><span class="sxs-lookup"><span data-stu-id="b68e0-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="b68e0-120">Sayfanın tarayıcıda yüklenmesi, açılan listeyi üç satıcı ile doldurur, ikincisi ise önceden seçilir.</span><span class="sxs-lookup"><span data-stu-id="b68e0-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="b68e0-121">Ayrıca, ASP.NET `__doPostBack()` JavaScript yöntemini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b68e0-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="b68e0-122">Sayfa yüklendikten sonra, bu JavaScript çağrısı açılan listeye eklenir, ancak yalnızca içinde öğeler varsa.</span><span class="sxs-lookup"><span data-stu-id="b68e0-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="b68e0-123">Listede hiçbir öğe yoksa, Denetim araç seti Şu anda onları yüklüyor, bu nedenle JavaScript kodu bir zaman aşımı kullanır ve yarım saniye içinde yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="b68e0-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

<span data-ttu-id="b68e0-124">Bu şekilde, geri gönderme yalnızca listede gerçekten öğeler olduğunda ve Kullanıcı bir giriş seçtiğinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="b68e0-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="b68e0-125">[bir liste öğesinin seçilmesi ![geri göndermeye neden olur](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b68e0-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="b68e0-126">Bir liste öğesi seçilmesi geri göndermeye neden olur ([tam boyutlu görüntüyü görüntülemek Için tıklatın](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b68e0-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b68e0-127">[Önceki](presetting-list-entries-with-cascadingdropdown-cs.md)
> [İleri](filling-a-list-using-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b68e0-127">[Previous](presetting-list-entries-with-cascadingdropdown-cs.md)
[Next](filling-a-list-using-cascadingdropdown-vb.md)</span></span>
