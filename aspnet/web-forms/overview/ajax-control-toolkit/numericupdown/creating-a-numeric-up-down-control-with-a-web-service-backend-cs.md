---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: Web hizmeti arka ucuna sahip (C#) sayısal yukarı/aşağı denetimi oluşturma | Microsoft Docs
author: wenz
description: Bir onay kutusuna bir değer kullanıcının yapmasına izin vermek yerine bir sayısal yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde var olan) daha fazla c kanıtlamak...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: ffefed61e259994990315d17a545ef74074092a6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073869"
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="6461d-103">Web Hizmeti Arka Ucuna Sahip Sayısal Yukarı/Aşağı Denetimi Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="6461d-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>
====================
<span data-ttu-id="6461d-104">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6461d-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6461d-105">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6461d-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="6461d-106">Bir onay kutusuna bir değer kullanıcının yapmasına izin vermek yerine bir sayısal yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde var olan) gibi daha fazla kanıtlamak rahat.</span><span class="sxs-lookup"><span data-stu-id="6461d-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="6461d-107">Varsayılan olarak, NumericUpDown denetimi her zaman artırır veya bir değer 1 ile azaltır, ancak daha fazla esneklik bir web hizmeti kanıtlar.</span><span class="sxs-lookup"><span data-stu-id="6461d-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="6461d-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6461d-108">Overview</span></span>

<span data-ttu-id="6461d-109">Bir onay kutusuna bir değer kullanıcının yapmasına izin vermek yerine bir sayısal yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde var olan) gibi daha fazla kanıtlamak rahat.</span><span class="sxs-lookup"><span data-stu-id="6461d-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="6461d-110">Varsayılan olarak, `NumericUpDown` denetimi her zaman artırır veya bir değer 1 ile azaltır, ancak daha fazla esneklik bir web hizmeti kanıtlar.</span><span class="sxs-lookup"><span data-stu-id="6461d-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="6461d-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="6461d-111">Steps</span></span>

<span data-ttu-id="6461d-112">ASP.NET AJAX Denetim Araç Seti içeren `NumericUpDown` otomatik olarak iki düğme metin kutusuna ekleyen genişletici: Bir değeri, bunu azaltmak için bir tane artırmaya yönelik.</span><span class="sxs-lookup"><span data-stu-id="6461d-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="6461d-113">Ancak denetim bir web hizmeti çağrısı (veya sayfa yöntem çağrısının) destekler.</span><span class="sxs-lookup"><span data-stu-id="6461d-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="6461d-114">Zaman ölçeğini artırıp düğmesine tıklandığında, JavaScript kodu web sunucusuna bağlanır ve bir yöntemi yürütür.</span><span class="sxs-lookup"><span data-stu-id="6461d-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="6461d-115">Aşağıdaki bir yöntem imzası verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="6461d-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="6461d-116">`current` Bağımsız değişkendir metin kutusundaki; geçerli değer `tag` özniteliktir özelliği olarak ayarlanabilir ek bağlam verileri `NumericUpDown` genişletici (ancak gerekli değildir).</span><span class="sxs-lookup"><span data-stu-id="6461d-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="6461d-117">Bu örnek, sayısal yukarı/aşağı denetimi yalnızca iki powers olan değerleri izin: 1, 2, 4, 8, 16, 32, 64 ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="6461d-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="6461d-118">Bu nedenle, değeri artırmak kullanıcı istediğinde yürütülen yöntemi çift eski değeri gerekir; başka bir yöntem değeri tarafından iki bölme gerekir.</span><span class="sxs-lookup"><span data-stu-id="6461d-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="6461d-119">Bu nedenle tam bir web hizmeti şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="6461d-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="6461d-120">Son olarak, yeni bir ASP.NET sayfası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6461d-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="6461d-121">Her zamanki şekilde ihtiyacınız bir `ScriptManager` denetimi, bir `TextBox` denetimi ve bir `NumericUpDownExtender` denetimi.</span><span class="sxs-lookup"><span data-stu-id="6461d-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="6461d-122">İkincisi için web hizmeti bilgileri sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6461d-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="6461d-123">`ServiceDownMethod` Aşağı adını web yöntemini veya sayfa yöntemi</span><span class="sxs-lookup"><span data-stu-id="6461d-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="6461d-124">`ServiceDownPath` yolu aşağı hizmet yöntemi ile web hizmetine; bir sayfa yöntemini kullanıyorsanız atla</span><span class="sxs-lookup"><span data-stu-id="6461d-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="6461d-125">`ServiceUpMethod` Yukarı adını web yöntemini veya sayfa yöntemi</span><span class="sxs-lookup"><span data-stu-id="6461d-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="6461d-126">`ServiceUpPath` yolu yukarı hizmet yöntemi ile web hizmetine; bir sayfa yöntemini kullanıyorsanız atla</span><span class="sxs-lookup"><span data-stu-id="6461d-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="6461d-127">Sayfa için tam biçimlendirmesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6461d-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="6461d-128">Sayfa çalıştırırsanız, üst düğmesine tıklayın ve daha düşük düğmesine tıkladığınızda yarıya nasıl metin kutusundaki değeri her zaman çiftler dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6461d-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


<span data-ttu-id="6461d-129">[![2'in kuvveti olan sayılar görünür](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6461d-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span></span>

<span data-ttu-id="6461d-130">2'in kuvveti olan sayılar görünür ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6461d-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6461d-131">Next</span><span class="sxs-lookup"><span data-stu-id="6461d-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
