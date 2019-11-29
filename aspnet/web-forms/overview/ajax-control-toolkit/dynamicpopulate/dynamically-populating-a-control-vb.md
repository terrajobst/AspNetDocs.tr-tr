---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: Bir denetimi dinamik olarak doldurma (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmeti (veya sayfa yöntemi) çağırır ve elde edilen değeri t üzerindeki bir hedef denetime doldurur...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d11320f1f89bb69afe5f62751574079716124da0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599389"
---
# <a name="dynamically-populating-a-control-vb"></a><span data-ttu-id="9e028-103">Bir Denetimi Dinamik Olarak Doldurma (VB)</span><span class="sxs-lookup"><span data-stu-id="9e028-103">Dynamically Populating a Control (VB)</span></span>

<span data-ttu-id="9e028-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="9e028-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9e028-105">[Kodu indirin](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="9e028-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span></span>

> <span data-ttu-id="9e028-106">ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur.</span><span class="sxs-lookup"><span data-stu-id="9e028-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>

## <a name="overview"></a><span data-ttu-id="9e028-107">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="9e028-107">Overview</span></span>

<span data-ttu-id="9e028-108">ASP.NET AJAX denetim araç setinde `DynamicPopulate` denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur.</span><span class="sxs-lookup"><span data-stu-id="9e028-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="9e028-109">Bu öğreticide nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9e028-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="9e028-110">Adımlar</span><span class="sxs-lookup"><span data-stu-id="9e028-110">Steps</span></span>

<span data-ttu-id="9e028-111">İlk olarak, `DynamicPopulate`tarafından çağrılacak yöntemi uygulayan bir ASP.NET Web hizmetine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="9e028-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="9e028-112">Web hizmeti sınıfı, `Microsoft.Web.Script.Services`içinde tanımlanan `ScriptService` özniteliğini gerektirir; Aksi takdirde ASP.NET AJAX, Web hizmeti için `DynamicPopulate`için gereken istemci tarafı JavaScript proxy 'sini oluşturamaz.</span><span class="sxs-lookup"><span data-stu-id="9e028-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="9e028-113">`DynamicPopulate` denetimi her bir Web hizmeti çağrısıyla bir bağlam bilgilerini gönderdiğinden, Web yönteminin `contextKey`dize türünde bir bağımsız değişken beklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e028-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="9e028-114">Aşağıdaki Web hizmeti, `contextKey` bağımsız değişkeni tarafından temsil edilen bir biçimde geçerli tarihi döndürür:</span><span class="sxs-lookup"><span data-stu-id="9e028-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="9e028-115">Web hizmeti daha sonra `DynamicPopulate.vb.asmx`olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="9e028-115">The web service is then saved as `DynamicPopulate.vb.asmx`.</span></span> <span data-ttu-id="9e028-116">Alternatif olarak, `DynamicPopulate` denetimi ile gerçek ASP.NET sayfasında bir sayfa yöntemi olarak `getDate()` yöntemini uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e028-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="9e028-117">Sonraki adımda yeni bir ASP.NET dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e028-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="9e028-118">Her zaman olduğu gibi ilk adım, ASP.NET AJAX kitaplığı 'nı yüklemek ve Denetim araç takımını çalışır hale getirmek için geçerli sayfaya `ScriptManager` dahil edilir:</span><span class="sxs-lookup"><span data-stu-id="9e028-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="9e028-119">Daha sonra Web hizmeti çağrısının sonucunu gösteren bir etiket denetimi (örneğin, aynı adın HTML denetimini veya &lt;`asp:Label` /&gt; Web denetimi) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9e028-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

<span data-ttu-id="9e028-120">Bir HTML düğmesi (bir HTML denetimi olarak, sunucuya geri gönderme gerektirtiğimiz için), dinamik popülasyonu tetiklemek için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="9e028-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="9e028-121">Son olarak, bağlantı kurmak için `DynamicPopulateExtender` denetimine ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="9e028-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="9e028-122">Aşağıdaki öznitelikler ayarlanacak (belirgin olanlardan ayrı olarak, `ID` ve `runat`=`"server"`):</span><span class="sxs-lookup"><span data-stu-id="9e028-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="9e028-123">Web hizmeti çağrısından sonucun nereye yerleştirileceğini `TargetControlID`</span><span class="sxs-lookup"><span data-stu-id="9e028-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="9e028-124">Web hizmetinin yolunu `ServicePath` (bir sayfa yöntemi kullanmak istiyorsanız atlayın)</span><span class="sxs-lookup"><span data-stu-id="9e028-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="9e028-125">Web yönteminin veya sayfa yönteminin `ServiceMethod` adı</span><span class="sxs-lookup"><span data-stu-id="9e028-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="9e028-126">Web hizmetine gönderilecek bağlam bilgilerini `ContextKey`</span><span class="sxs-lookup"><span data-stu-id="9e028-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="9e028-127">Web hizmeti çağrısını tetikleyen `PopulateTriggerControlID` öğesi</span><span class="sxs-lookup"><span data-stu-id="9e028-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="9e028-128">Web hizmeti çağrısı sırasında hedef öğenin boş bırakılıp başlatılmayacağını `ClearContentsDuringUpdate`</span><span class="sxs-lookup"><span data-stu-id="9e028-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="9e028-129">Gördüğünüz gibi, denetim bazı bilgiler gerektirir, ancak her şeyi konuma koymak oldukça basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="9e028-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="9e028-130">Geçerli senaryoda `DynamicPopulateExtender` denetimi için biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e028-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="9e028-131">Tarayıcıda ASP.NET sayfasını çalıştırın ve düğmesine tıklayın; geçerli tarihi ay-gün biçiminde alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9e028-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>

<span data-ttu-id="9e028-132">[düğmeye tıklama ![sunucudan tarihi alır](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9e028-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="9e028-133">Düğmeye tıklama, tarihi sunucudan alır ([tam boyutlu görüntüyü görüntülemek Için tıklatın](dynamically-populating-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9e028-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9e028-134">[Önceki](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [İleri](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9e028-134">[Previous](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Next](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>
