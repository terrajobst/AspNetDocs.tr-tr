---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: ModalPopup (C#) Ile geri göndermeler işleme Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Bir POS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554063"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a><span data-ttu-id="cf140-104">ModalPopup’tan Gelen Geri Göndermeleri İşleme (C#)</span><span class="sxs-lookup"><span data-stu-id="cf140-104">Handling Postbacks from a ModalPopup (C#)</span></span>

<span data-ttu-id="cf140-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="cf140-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cf140-106">[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="cf140-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span></span>

> <span data-ttu-id="cf140-107">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="cf140-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="cf140-108">Açılan pencere içinden bir geri gönderme oluşturulduğunda özel dikkatli olunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cf140-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="cf140-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="cf140-109">Overview</span></span>

<span data-ttu-id="cf140-110">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="cf140-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="cf140-111">Açılan pencere içinden bir geri gönderme oluşturulduğunda özel dikkatli olunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cf140-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="cf140-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="cf140-112">Steps</span></span>

<span data-ttu-id="cf140-113">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="cf140-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="cf140-114">Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cf140-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="cf140-115">Bu şekilde, Kullanıcı bir ad ve e-posta adresi girebilir.</span><span class="sxs-lookup"><span data-stu-id="cf140-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="cf140-116">Açılan pencereyi kapatmak ve bilgileri kaydetmek için bir düğme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cf140-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="cf140-117">`OnClick` özniteliğinin, bu düğmeye tıklandığında geri gönderme işleminin gerçekleşmesini sağlamak için ayarlandığını unutmayın:</span><span class="sxs-lookup"><span data-stu-id="cf140-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="cf140-118">Sayfanın kendisi tam olarak aynı bilgiler için iki etiketten oluşur: ad ve e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="cf140-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="cf140-119">Kalıcı açılan pencereyi tetiklemek için bir düğme kullanılır:</span><span class="sxs-lookup"><span data-stu-id="cf140-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

<span data-ttu-id="cf140-120">Açılan pencerenin görünmesini sağlamak için `ModalPopupExtender` denetimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cf140-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="cf140-121">`PopupControlID` özniteliğini bölmenin KIMLIĞINE ayarlayın ve düğmenin KIMLIĞINE `TargetControlID`:</span><span class="sxs-lookup"><span data-stu-id="cf140-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

<span data-ttu-id="cf140-122">Artık, kalıcı açılan pencerenin içindeki `Save` düğmesine tıklandığında, sunucu tarafı `SaveData()` yöntemi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="cf140-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="cf140-123">Burada, girilen verileri bir veri deposuna kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf140-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="cf140-124">Basitlik sağlamak için yeni veriler yalnızca etiketin çıktıdır:</span><span class="sxs-lookup"><span data-stu-id="cf140-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

<span data-ttu-id="cf140-125">Ayrıca, kalıcı açılan pencerede bulunan TextBox denetimleri geçerli ad ve e-posta ile doldurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cf140-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="cf140-126">Ancak bu yalnızca geri gönderme gerçekleşmediğinde gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cf140-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="cf140-127">Bir geri gönderme işlemi varsa, ASP.NET ViewState özelliği, metin kutularını uygun değerlerle otomatik olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="cf140-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

<span data-ttu-id="cf140-128">[![kalıcı açılan pencere geri göndermeye neden olur](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cf140-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="cf140-129">Kalıcı açılan pencere geri göndermeye neden olur ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cf140-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cf140-130">[Önceki](using-modalpopup-with-a-repeater-control-cs.md)
> [İleri](positioning-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="cf140-130">[Previous](using-modalpopup-with-a-repeater-control-cs.md)
[Next](positioning-a-modalpopup-cs.md)</span></span>
