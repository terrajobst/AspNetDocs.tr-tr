---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: JavaScript kodu kullanarak bir denetimi dinamik olarak doldurmaC#() | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmeti (veya sayfa yöntemi) çağırır ve elde edilen değeri t üzerindeki bir hedef denetime doldurur...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 24dc358427dec3ffcba16d00041c9a2db657e7e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599252"
---
# <a name="dynamically-populating-a-control-using-javascript-code-c"></a><span data-ttu-id="629c3-103">JavaScript Kodu Kullanarak Bir Denetimi Dinamik Olarak Doldurma (C#)</span><span class="sxs-lookup"><span data-stu-id="629c3-103">Dynamically Populating a Control Using JavaScript Code (C#)</span></span>

<span data-ttu-id="629c3-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="629c3-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="629c3-105">[Kodu indirin](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="629c3-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span></span>

> <span data-ttu-id="629c3-106">ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur.</span><span class="sxs-lookup"><span data-stu-id="629c3-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="629c3-107">Özel istemci tarafı JavaScript kodu kullanılarak popülasyonun tetiklenmesi de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="629c3-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="629c3-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="629c3-108">Overview</span></span>

<span data-ttu-id="629c3-109">ASP.NET AJAX denetim araç setinde `DynamicPopulate` denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur.</span><span class="sxs-lookup"><span data-stu-id="629c3-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="629c3-110">Özel istemci tarafı JavaScript kodu kullanılarak popülasyonun tetiklenmesi de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="629c3-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="629c3-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="629c3-111">Steps</span></span>

<span data-ttu-id="629c3-112">İlk olarak, `DynamicPopulateExtender` denetimi tarafından çağrılacak yöntemi uygulayan bir ASP.NET Web hizmetine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="629c3-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="629c3-113">Web hizmeti, `DynamicPopulate` denetimi her bir Web hizmeti çağrısıyla bir dizi bağlam bilgisi gönderdiğinden, `contextKey`olarak adlandırılan `getDate()` dize türünde bir bağımsız değişken bekleyen yöntemi uygular.</span><span class="sxs-lookup"><span data-stu-id="629c3-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="629c3-114">Üç biçimden birindeki geçerli tarihi alan kod (dosya `DynamicPopulate.cs.asmx`) aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="629c3-114">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

<span data-ttu-id="629c3-115">Sonraki adımda, yeni bir ASP.NET sitesi oluşturun ve ASP.NET AJAX ScriptManager denetimiyle başlayın:</span><span class="sxs-lookup"><span data-stu-id="629c3-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

<span data-ttu-id="629c3-116">Ardından, daha sonra Web hizmeti çağrısının sonucunu gösterecek bir etiket denetimi (örneğin, aynı ada sahip HTML denetimini veya `<asp:Label />` Web denetimini kullanarak) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="629c3-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

<span data-ttu-id="629c3-117">Daha sonra, bir `DynamicPopulateExtender` denetimi ekleyin ve Web hizmeti bilgilerini, hedef denetimi sağlayın, ancak bunun daha sonra, özel JavaScript kullanılarak yapılacak şekilde bu işlemi tetikleyecek olan denetimin adını değil,</span><span class="sxs-lookup"><span data-stu-id="629c3-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

<span data-ttu-id="629c3-118">Şimdi JavaScript bölümüne.</span><span class="sxs-lookup"><span data-stu-id="629c3-118">Now to the JavaScript part.</span></span> <span data-ttu-id="629c3-119">ASP.NET AJAX kitaplığı tarafından tanımlanan `$find()` işlevi, `DynamicPopulateExtender`gibi ASP.NET AJAX denetim araç setinin sunucu tarafı nesnelerine bir başvuru döndürür.</span><span class="sxs-lookup"><span data-stu-id="629c3-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="629c3-120">Geçerli dosyada, `$find("dpe")` sayfadaki bir `DynamicPopulateExtender` denetimine bir başvuru döndürür.</span><span class="sxs-lookup"><span data-stu-id="629c3-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="629c3-121">Dinamik popülasyon işlemini tetikleyen `populate()` adlı bir yöntemi kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="629c3-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="629c3-122">`populate()` yöntemi bir bağımsız değişken gerektiriyor: `getDate()` Web metoduna bağımsız değişken olarak kullanılacak bağlam anahtarı.</span><span class="sxs-lookup"><span data-stu-id="629c3-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="629c3-123">Örneğin, `$find("dpe").populate("format1")`, etiketi ay-gün biçiminde geçerli tarihle dolduracaktır.</span><span class="sxs-lookup"><span data-stu-id="629c3-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="629c3-124">Örneği biraz daha esnek hale getirmek için Kullanıcı artık birkaç tarih biçimi arasından seçim yapabilir.</span><span class="sxs-lookup"><span data-stu-id="629c3-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="629c3-125">Bunların her biri için bir radyo düğmesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="629c3-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="629c3-126">Kullanıcı radyo düğmesine tıkladığında, JavaScript kodu etiketi seçilen tarih biçimiyle dinamik olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="629c3-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="629c3-127">Bu radyo düğmeleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="629c3-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

<span data-ttu-id="629c3-128">Radyo düğmesi bağlamında, JavaScript ifadesi `this.value`, geçerli düğmenin değerini ifade eder ve bu da `getDate()` yönteminin birlikte çalışabileceği bilgilerle tamamen aynı olur.</span><span class="sxs-lookup"><span data-stu-id="629c3-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>

<span data-ttu-id="629c3-129">[düğmeye tıklama ![, belirtilen biçimde sunucudan tarihi alır](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="629c3-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="629c3-130">Düğmeye tıkladığınızda, belirtilen biçimdeki tarihi sunucudan alır ([tam boyutlu görüntüyü görüntülemek Için tıklatın](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="629c3-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="629c3-131">[Önceki](dynamically-populating-a-control-cs.md)
> [İleri](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span><span class="sxs-lookup"><span data-stu-id="629c3-131">[Previous](dynamically-populating-a-control-cs.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span></span>
