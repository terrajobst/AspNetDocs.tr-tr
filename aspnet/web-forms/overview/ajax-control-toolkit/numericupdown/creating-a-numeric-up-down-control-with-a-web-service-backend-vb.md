---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: Web hizmeti arka ucu ile sayısal bir yukarı/aşağı denetimi oluşturma (VB) | Microsoft Docs
author: wenz
description: Bir kullanıcının bir onay kutusuna değer yazmalarına izin vermek yerine, sayısal bir yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde bulunur) daha fazla c... anlamına gelebilir.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 2bf6e1b27180589d39e308de62b5be1f47fa8fe2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612996"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a><span data-ttu-id="a130a-103">Web Hizmeti Arka Ucuna Sahip Sayısal Yukarı/Aşağı Denetimi Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="a130a-103">Creating a Numeric Up/Down Control with a Web Service Backend (VB)</span></span>

<span data-ttu-id="a130a-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="a130a-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a130a-105">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a130a-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span></span>

> <span data-ttu-id="a130a-106">Bir kullanıcının onay kutusuna değer yazmalarına izin vermek yerine, sayısal bir yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde bulunur) daha rahat bir şekilde kanıtlayabilecek.</span><span class="sxs-lookup"><span data-stu-id="a130a-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="a130a-107">Varsayılan olarak, NumericUpDown denetimi her zaman bir değeri 1 artırır veya düşürür, ancak bir Web hizmeti daha fazla esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="a130a-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="a130a-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="a130a-108">Overview</span></span>

<span data-ttu-id="a130a-109">Bir kullanıcının onay kutusuna değer yazmalarına izin vermek yerine, sayısal bir yukarı/aşağı denetimi (Windows ve diğer işletim sistemlerinde bulunur) daha rahat bir şekilde kanıtlayabilecek.</span><span class="sxs-lookup"><span data-stu-id="a130a-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="a130a-110">Varsayılan olarak, `NumericUpDown` denetimi her zaman bir değeri 1 artırır veya düşürür, ancak bir Web hizmeti daha fazla esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="a130a-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="a130a-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="a130a-111">Steps</span></span>

<span data-ttu-id="a130a-112">ASP.NET AJAX denetim araç seti, bir metin kutusuna otomatik olarak iki düğme ekleyen `NumericUpDown` Genişletici ' i içerir: bir tane, değerini azaltmak için bir tane.</span><span class="sxs-lookup"><span data-stu-id="a130a-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="a130a-113">Ancak denetim Ayrıca bir Web hizmeti çağrısını (veya sayfa yöntemi çağrısını) destekler.</span><span class="sxs-lookup"><span data-stu-id="a130a-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="a130a-114">Yukarı veya aşağı düğmesine tıklandığında, JavaScript kodu Web sunucusuna bağlanır ve bir yöntemi bu yerde yürütür.</span><span class="sxs-lookup"><span data-stu-id="a130a-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="a130a-115">Yöntem imzası aşağıdakilerden biridir:</span><span class="sxs-lookup"><span data-stu-id="a130a-115">The method signature is the following one:</span></span>

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

<span data-ttu-id="a130a-116">`current` bağımsız değişkeni, metin kutusundaki geçerli değerdir; `tag` özniteliği, `NumericUpDown` genişletici 'in bir özelliği olarak ayarlanmakta olan ek bağlam verileri (ancak gerekli değildir).</span><span class="sxs-lookup"><span data-stu-id="a130a-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="a130a-117">Bu örnekte, sayısal yukarı/aşağı denetimi yalnızca iki üsleri olan değerlere izin veriyor: 1, 2, 4, 8, 16, 32, 64, vb.</span><span class="sxs-lookup"><span data-stu-id="a130a-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="a130a-118">Bu nedenle, kullanıcının değeri arttırmak istediğinde yürütülen Yöntem eski değeri Double olmalıdır; diğer yöntem değeri iki ile bölmelidir.</span><span class="sxs-lookup"><span data-stu-id="a130a-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="a130a-119">Web hizmetinin tamamı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a130a-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

<span data-ttu-id="a130a-120">Son olarak, yeni bir ASP.NET sayfası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a130a-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="a130a-121">Her zamanki gibi, bir `ScriptManager` denetimine, `TextBox` denetimine ve `NumericUpDownExtender` denetimine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="a130a-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="a130a-122">İkincisi için, Web hizmeti bilgilerini sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a130a-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="a130a-123">aşağı Web yönteminin veya sayfa yönteminin `ServiceDownMethod` adı</span><span class="sxs-lookup"><span data-stu-id="a130a-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="a130a-124">Web hizmetinin yolunu aşağı hizmet yöntemiyle `ServiceDownPath`; bir sayfa yöntemi kullanıyorsanız, atlayın</span><span class="sxs-lookup"><span data-stu-id="a130a-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="a130a-125">up Web yönteminin veya sayfa yönteminin `ServiceUpMethod` adı</span><span class="sxs-lookup"><span data-stu-id="a130a-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="a130a-126">up hizmeti yöntemiyle Web hizmetinin yolunu `ServiceUpPath`; bir sayfa yöntemi kullanıyorsanız, atlayın</span><span class="sxs-lookup"><span data-stu-id="a130a-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="a130a-127">Sayfa için tüm biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a130a-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

<span data-ttu-id="a130a-128">Sayfayı çalıştırırsanız, üstteki düğmeye tıkladığınızda metin kutusundaki değerin her zaman iki katına çıkar ve alt düğmeye tıkladığınızda bu değeri yarıya iner.</span><span class="sxs-lookup"><span data-stu-id="a130a-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>

<span data-ttu-id="a130a-129">[![yalnızca 2 ' nin üssü olan sayılar görüntülenir](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a130a-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span></span>

<span data-ttu-id="a130a-130">Yalnızca 2 ' nin üssü olan sayılar görüntülenir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a130a-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a130a-131">Öncekini</span><span class="sxs-lookup"><span data-stu-id="a130a-131">Previous</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
