---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: ModalPopup 'dan geri göndermeler işleme (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Bir POS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: df0b71b3e336a0d230869623473bdac24b3dd07b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606613"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a><span data-ttu-id="618ca-104">ModalPopup’tan Gelen Geri Göndermeleri İşleme (VB)</span><span class="sxs-lookup"><span data-stu-id="618ca-104">Handling Postbacks from a ModalPopup (VB)</span></span>

<span data-ttu-id="618ca-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="618ca-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="618ca-106">[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="618ca-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span></span>

> <span data-ttu-id="618ca-107">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="618ca-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="618ca-108">Açılan pencere içinden bir geri gönderme oluşturulduğunda özel dikkatli olunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="618ca-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="618ca-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="618ca-109">Overview</span></span>

<span data-ttu-id="618ca-110">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="618ca-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="618ca-111">Açılan pencere içinden bir geri gönderme oluşturulduğunda özel dikkatli olunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="618ca-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="618ca-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="618ca-112">Steps</span></span>

<span data-ttu-id="618ca-113">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="618ca-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="618ca-114">Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin.</span><span class="sxs-lookup"><span data-stu-id="618ca-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="618ca-115">Bu şekilde, Kullanıcı bir ad ve e-posta adresi girebilir.</span><span class="sxs-lookup"><span data-stu-id="618ca-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="618ca-116">Açılan pencereyi kapatmak ve bilgileri kaydetmek için bir düğme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="618ca-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="618ca-117">`OnClick` özniteliğinin, bu düğmeye tıklandığında geri gönderme işleminin gerçekleşmesini sağlamak için ayarlandığını unutmayın:</span><span class="sxs-lookup"><span data-stu-id="618ca-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="618ca-118">Sayfanın kendisi tam olarak aynı bilgiler için iki etiketten oluşur: ad ve e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="618ca-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="618ca-119">Kalıcı açılan pencereyi tetiklemek için bir düğme kullanılır:</span><span class="sxs-lookup"><span data-stu-id="618ca-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

<span data-ttu-id="618ca-120">Açılan pencerenin görünmesini sağlamak için `ModalPopupExtender` denetimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="618ca-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="618ca-121">`PopupControlID` özniteliğini bölmenin KIMLIĞINE ayarlayın ve düğmenin KIMLIĞINE `TargetControlID`:</span><span class="sxs-lookup"><span data-stu-id="618ca-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

<span data-ttu-id="618ca-122">Artık, kalıcı açılan pencerenin içindeki `Save` düğmesine tıklandığında, sunucu tarafı `SaveData()` yöntemi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="618ca-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="618ca-123">Burada, girilen verileri bir veri deposuna kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="618ca-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="618ca-124">Basitlik sağlamak için yeni veriler yalnızca etiketin çıktıdır:</span><span class="sxs-lookup"><span data-stu-id="618ca-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

<span data-ttu-id="618ca-125">Ayrıca, kalıcı açılan pencerede bulunan TextBox denetimleri geçerli ad ve e-posta ile doldurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="618ca-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="618ca-126">Ancak bu yalnızca geri gönderme gerçekleşmediğinde gereklidir.</span><span class="sxs-lookup"><span data-stu-id="618ca-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="618ca-127">Bir geri gönderme işlemi varsa, ASP.NET ViewState özelliği, metin kutularını uygun değerlerle otomatik olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="618ca-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

<span data-ttu-id="618ca-128">[![kalıcı açılan pencere geri göndermeye neden olur](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="618ca-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="618ca-129">Kalıcı açılan pencere geri göndermeye neden olur ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="618ca-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="618ca-130">[Önceki](using-modalpopup-with-a-repeater-control-vb.md)
> [İleri](positioning-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="618ca-130">[Previous](using-modalpopup-with-a-repeater-control-vb.md)
[Next](positioning-a-modalpopup-vb.md)</span></span>
