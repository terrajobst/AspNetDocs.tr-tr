---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: Bir ModalPopup konumlandırma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak denetim bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: fb79a08a339588ed8adc4b4236911819ea9286b4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598983"
---
# <a name="positioning-a-modalpopup-vb"></a><span data-ttu-id="b818d-104">Bir ModalPopup’ı Konumlandırma (VB)</span><span class="sxs-lookup"><span data-stu-id="b818d-104">Positioning a ModalPopup (VB)</span></span>

<span data-ttu-id="b818d-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="b818d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b818d-106">[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b818d-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span></span>

> <span data-ttu-id="b818d-107">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="b818d-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="b818d-108">Ancak denetim, açılan pencereyi konumlandırmak için yerleşik bir işlevsellik sunmaz.</span><span class="sxs-lookup"><span data-stu-id="b818d-108">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="b818d-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="b818d-109">Overview</span></span>

<span data-ttu-id="b818d-110">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="b818d-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="b818d-111">Ancak denetim, açılan pencereyi konumlandırmak için yerleşik bir işlevsellik sunmaz.</span><span class="sxs-lookup"><span data-stu-id="b818d-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="b818d-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="b818d-112">Steps</span></span>

<span data-ttu-id="b818d-113">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için `ScriptManager`.</span><span class="sxs-lookup"><span data-stu-id="b818d-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="b818d-114">Denetim, sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="b818d-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="b818d-115">Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b818d-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="b818d-116">Açılan pencereyi kapatmak için bir düğme kullanılır:</span><span class="sxs-lookup"><span data-stu-id="b818d-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="b818d-117">Açılan pencere her gösterildiğinde sayfada belirli bir yerde konumlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b818d-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="b818d-118">Bu görev için, istemci tarafı bir JavaScript işlevi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b818d-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="b818d-119">Önce panele erişmeyi dener.</span><span class="sxs-lookup"><span data-stu-id="b818d-119">It first tries to access the panel.</span></span> <span data-ttu-id="b818d-120">Bu işlem başarılı olursa, panelin konumu CSS ve JavaScript kullanılarak ayarlanır (açılan menünün konumunu ' de değiştirin).</span><span class="sxs-lookup"><span data-stu-id="b818d-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="b818d-121">Ancak `ModalPopupExtender` denetimi de açılan pencereyi konumlandırmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b818d-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="b818d-122">Bu nedenle, JavaScript kodu bir saniyede her onuncu açılan pencereyi sürekli konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="b818d-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

<span data-ttu-id="b818d-123">Gördüğünüz gibi, JavaScript yönteminin dönüş `setTimeout()` değeri genel bir değişkende kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="b818d-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="b818d-124">Bu, `clearTimeout()` yöntemi kullanılarak, isteğe bağlı açılan pencerenin tekrarlanmış konumunu durdurmaya izin verir:</span><span class="sxs-lookup"><span data-stu-id="b818d-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

<span data-ttu-id="b818d-125">Artık her şey, her zaman uygun olduğunda tarayıcının bu işlevleri çağırmasını sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b818d-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="b818d-126">Düğme tıklandığında paneli tetikleyen `movePanel()` JavaScript işlevi çağrılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="b818d-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

<span data-ttu-id="b818d-127">`stopMoving()` işlevi, açılan pencere kapatıldığında oynat ' a gelir ve bu, `ModalPopupExtender` denetiminde tetiklenebilir:</span><span class="sxs-lookup"><span data-stu-id="b818d-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]

<span data-ttu-id="b818d-128">[![, belirlenen konumda kalıcı açılan pencere görüntülenir](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b818d-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="b818d-129">Belirlenen konumda kalıcı açılan pencere görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](positioning-a-modalpopup-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b818d-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b818d-130">Öncekini</span><span class="sxs-lookup"><span data-stu-id="b818d-130">Previous</span></span>](handling-postbacks-from-a-modalpopup-vb.md)
