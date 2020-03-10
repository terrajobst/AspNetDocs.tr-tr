---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: Birbirinden sonra birkaç animasyon yürütme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bu, Severa 'yi çalıştırmaya izin verir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598135"
---
# <a name="executing-several-animations-after-each-other-vb"></a><span data-ttu-id="35f07-104">Arka Arkaya Birkaç Animasyon Yürütme (VB)</span><span class="sxs-lookup"><span data-stu-id="35f07-104">Executing Several Animations after Each Other (VB)</span></span>

<span data-ttu-id="35f07-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="35f07-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="35f07-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="35f07-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span></span>

> <span data-ttu-id="35f07-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="35f07-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="35f07-108">Bunlardan daha sonra birkaç animasyon çalıştırmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="35f07-108">It allows to run several animations one after the other.</span></span>

## <a name="overview"></a><span data-ttu-id="35f07-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="35f07-109">Overview</span></span>

<span data-ttu-id="35f07-110">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="35f07-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="35f07-111">Bunlardan daha sonra birkaç animasyon çalıştırmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="35f07-111">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="35f07-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="35f07-112">Steps</span></span>

<span data-ttu-id="35f07-113">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="35f07-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

<span data-ttu-id="35f07-114">Animasyon, şunun gibi görünen bir metin paneline uygulanır:</span><span class="sxs-lookup"><span data-stu-id="35f07-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

<span data-ttu-id="35f07-115">Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="35f07-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

<span data-ttu-id="35f07-116">Daha sonra, bir `ID`, `TargetControlID` özniteliği ve obligatory sağlayarak sayfaya `AnimationExtender` ekleyin `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="35f07-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

<span data-ttu-id="35f07-117">`<Animations>` düğümü içinde, sayfa tam olarak yüklendikten sonra animasyonları çalıştırmak için `<OnLoad>` kullanın.</span><span class="sxs-lookup"><span data-stu-id="35f07-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="35f07-118">Genellikle `<OnLoad>` yalnızca bir animasyon kabul eder.</span><span class="sxs-lookup"><span data-stu-id="35f07-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="35f07-119">Animasyon çerçevesi, `<Sequence>` öğesini kullanarak çeşitli animasyonları tek tek birleştirkullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="35f07-119">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="35f07-120">`<Sequence>` içindeki tüm animasyonlar, bunlardan sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="35f07-120">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="35f07-121">`AnimationExtender` denetimi için olası bir biçimlendirme aşağıda verilmiştir, önce paneli daha geniş yapıp yüksekliğini azaltır:</span><span class="sxs-lookup"><span data-stu-id="35f07-121">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

<span data-ttu-id="35f07-122">Bu betiği çalıştırdığınızda panel önce daha geniş ve daha küçük olur.</span><span class="sxs-lookup"><span data-stu-id="35f07-122">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="35f07-123">[Ilk ![genişlik artırıldı](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="35f07-123">[![First the width is increased](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span></span>

<span data-ttu-id="35f07-124">İlk genişlik artmıştır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](executing-several-animations-after-each-other-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="35f07-124">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image3.png))</span></span>

<span data-ttu-id="35f07-125">[![yükseklik azaltılır](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="35f07-125">[![Then the height is decreased](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span></span>

<span data-ttu-id="35f07-126">Sonra Yükseklik azaltılır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](executing-several-animations-after-each-other-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="35f07-126">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="35f07-127">[Önceki](executing-several-animations-at-the-same-time-vb.md)
> [İleri](animation-depending-on-a-condition-vb.md)</span><span class="sxs-lookup"><span data-stu-id="35f07-127">[Previous](executing-several-animations-at-the-same-time-vb.md)
[Next](animation-depending-on-a-condition-vb.md)</span></span>
