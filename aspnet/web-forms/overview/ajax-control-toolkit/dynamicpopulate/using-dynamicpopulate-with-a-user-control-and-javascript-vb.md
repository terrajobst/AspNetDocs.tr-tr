---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: Kullanıcı denetimi ve JavaScript ile DynamicPopulate kullanma (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmeti (veya sayfa yöntemi) çağırır ve elde edilen değeri t üzerindeki bir hedef denetime doldurur...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599132"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="90d13-103">Kullanıcı Denetimi ve JavaScript ile DynamicPopulate Kullanma (VB)</span><span class="sxs-lookup"><span data-stu-id="90d13-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>

<span data-ttu-id="90d13-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="90d13-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="90d13-105">[Kodu indirin](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="90d13-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="90d13-106">ASP.NET AJAX denetim araç setinde DynamicPopulate denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur.</span><span class="sxs-lookup"><span data-stu-id="90d13-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="90d13-107">Özel istemci tarafı JavaScript kodu kullanılarak popülasyonun tetiklenmesi de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="90d13-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="90d13-108">Ancak, Extender bir kullanıcı denetiminde bulunduğunda özel dikkatli olunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90d13-108">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="overview"></a><span data-ttu-id="90d13-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="90d13-109">Overview</span></span>

<span data-ttu-id="90d13-110">ASP.NET AJAX denetim araç setinde `DynamicPopulate` denetimi bir Web hizmetini (veya sayfa yöntemini) çağırır ve ortaya çıkan değeri sayfa yenilemesi olmadan sayfadaki bir hedef denetime doldurur.</span><span class="sxs-lookup"><span data-stu-id="90d13-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="90d13-111">Özel istemci tarafı JavaScript kodu kullanılarak popülasyonun tetiklenmesi de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="90d13-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="90d13-112">Ancak, Extender bir kullanıcı denetiminde bulunduğunda özel dikkatli olunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90d13-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="90d13-113">Adımlar</span><span class="sxs-lookup"><span data-stu-id="90d13-113">Steps</span></span>

<span data-ttu-id="90d13-114">İlk olarak, `DynamicPopulateExtender` denetimi tarafından çağrılacak yöntemi uygulayan bir ASP.NET Web hizmetine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="90d13-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="90d13-115">Web hizmeti, `DynamicPopulate` denetimi her bir Web hizmeti çağrısıyla bir dizi bağlam bilgisi gönderdiğinden, `contextKey`olarak adlandırılan `getDate()` dize türünde bir bağımsız değişken bekleyen yöntemi uygular.</span><span class="sxs-lookup"><span data-stu-id="90d13-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="90d13-116">Üç biçimden birindeki geçerli tarihi alan kod (dosyalar `DynamicPopulate.vb.asmx`) aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="90d13-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="90d13-117">Sonraki adımda, ilk satırında aşağıdaki bildirimle belirtilen yeni bir kullanıcı denetimi (`.ascx` dosyası) oluşturun:</span><span class="sxs-lookup"><span data-stu-id="90d13-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="90d13-118">Sunucudan gelen verileri göstermek için bir &lt;`label`&gt; öğesi kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="90d13-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="90d13-119">Ayrıca, Kullanıcı denetim dosyasında, her biri Web hizmeti tarafından desteklenen üç tarih biçiminden birini temsil eden üç radyo düğmesini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="90d13-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="90d13-120">Kullanıcı radyo düğmelerinden birine tıkladığında tarayıcı şu şekilde görünen JavaScript kodunu yürütür:</span><span class="sxs-lookup"><span data-stu-id="90d13-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="90d13-121">Bu kod `DynamicPopulateExtender` erişir (alışılmadık KIMLIK hakkında endişelenmeyin, bu, daha sonra ele alınacaktır) ve dinamik popülasyonu verilerle tetikler.</span><span class="sxs-lookup"><span data-stu-id="90d13-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="90d13-122">Geçerli radyo düğmesi bağlamında `this.value`, `format1`, `format2` veya `format3` tam olarak Web yönteminin beklediği değeri anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="90d13-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="90d13-123">Yalnızca Kullanıcı denetiminde eksik olan tek şey, radyo düğmelerini Web hizmetine bağlayan `DynamicPopulateExtender` denetimidir.</span><span class="sxs-lookup"><span data-stu-id="90d13-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="90d13-124">Yine, denetimde kullanılan garip KIMLIĞI, `myDate`yerine `mcd1$myDate` görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90d13-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="90d13-125">Daha önce, `dpe1`yerine `DynamicPopulateExtender` erişmek için `mcd1_dpe1` kullanılan JavaScript kodu. Bu adlandırma stratejisi, bir kullanıcı denetimi içinde `DynamicPopulateExtender` kullanırken özel bir gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="90d13-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="90d13-126">Ayrıca, tüm çalışmaları yapmak için Kullanıcı denetimini belirli bir şekilde gömmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90d13-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="90d13-127">Yeni bir ASP.NET sayfası oluşturun ve az önce uygulamış olduğunuz Kullanıcı denetimi için bir etiket öneki kaydedin:</span><span class="sxs-lookup"><span data-stu-id="90d13-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="90d13-128">Ardından, ASP.NET AJAX `ScriptManager` denetimini yeni sayfaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="90d13-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="90d13-129">Son olarak, sayfasına kullanıcı denetimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90d13-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="90d13-130">Yalnızca `ID` özniteliğini (ve `runat="server"`kurs) ayarlamanız yeterlidir, ancak bunu belirli bir ada ayarlamanız gerekir: Bu, Kullanıcı denetimi içinde JavaScript kullanarak erişmek için kullanılan ön ek olduğundan `mcd1`.</span><span class="sxs-lookup"><span data-stu-id="90d13-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="90d13-131">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="90d13-131">And that's it!</span></span> <span data-ttu-id="90d13-132">Sayfa beklendiği gibi davranır: Kullanıcı radyo düğmelerinden birine tıkladığında araç setinde denetim Web hizmetini çağırır ve geçerli tarihi istenen biçimde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="90d13-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>

<span data-ttu-id="90d13-133">[radyo düğmelerinin bir kullanıcı denetiminde yer aldığı ![](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="90d13-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="90d13-134">Radyo düğmeleri bir kullanıcı denetiminde bulunur ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="90d13-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="90d13-135">Öncekini</span><span class="sxs-lookup"><span data-stu-id="90d13-135">Previous</span></span>](dynamically-populating-a-control-using-javascript-code-vb.md)
