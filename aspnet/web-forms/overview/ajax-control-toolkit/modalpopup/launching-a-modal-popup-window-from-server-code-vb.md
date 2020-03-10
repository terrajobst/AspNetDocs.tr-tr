---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: Sunucu kodundan kalıcı açılan pencere başlatma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak bazı senaryolar bu t... gerektirir.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 1368a78d35ac6461bbc2e852e468f42eef2c0d2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613276"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a><span data-ttu-id="fef8e-104">Sunucu Kodundan Kalıcı Açılan Pencere Başlatma (VB)</span><span class="sxs-lookup"><span data-stu-id="fef8e-104">Launching a Modal Popup Window from Server Code (VB)</span></span>

<span data-ttu-id="fef8e-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="fef8e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fef8e-106">[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fef8e-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span></span>

> <span data-ttu-id="fef8e-107">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="fef8e-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="fef8e-108">Ancak bazı senaryolar, sunucu tarafında kalıcı açılan pencerenin açılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fef8e-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="overview"></a><span data-ttu-id="fef8e-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="fef8e-109">Overview</span></span>

<span data-ttu-id="fef8e-110">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="fef8e-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="fef8e-111">Ancak bazı senaryolar, sunucu tarafında kalıcı açılan pencerenin açılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fef8e-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="fef8e-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="fef8e-112">Steps</span></span>

<span data-ttu-id="fef8e-113">Birincisi, ModalPopup denetiminin nasıl çalıştığını göstermek için bir ASP.NET Button Web denetimi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fef8e-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="fef8e-114">Yeni bir sayfada &lt;form&gt; öğesi içinde böyle bir düğme ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fef8e-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

<span data-ttu-id="fef8e-115">Ardından, oluşturmak istediğiniz açılan pencere için biçimlendirmenin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fef8e-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="fef8e-116">Bunu bir `<asp:Panel>` denetimi olarak tanımlayın ve bir düğme denetimi içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="fef8e-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="fef8e-117">ModalPopup denetimi, bu tür bir düğmeyi açılan pencereyi kapatacak şekilde işlevleri sunar; Aksi takdirde, bir yol açmanın kolay bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="fef8e-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

<span data-ttu-id="fef8e-118">Daha sonra, ASP.NET AJAX araç kümesinden ModalPopup denetimini sayfaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fef8e-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="fef8e-119">Denetimi yükleyen düğme için özellikleri, ortadan kaldırdıkları düğmeyi ve gerçek açılan pencerenin KIMLIĞINI ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fef8e-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

<span data-ttu-id="fef8e-120">ASP.NET AJAX 'ı temel alan tüm Web sayfalarında olduğu gibi Komut dosyası Yöneticisi, farklı hedef tarayıcılar için gerekli JavaScript kitaplıklarını yüklemek üzere gereklidir:</span><span class="sxs-lookup"><span data-stu-id="fef8e-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

<span data-ttu-id="fef8e-121">Örneği tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fef8e-121">Run the example in the browser.</span></span> <span data-ttu-id="fef8e-122">Düğmeye tıkladığınızda, kalıcı açılan pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="fef8e-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="fef8e-123">Sunucu tarafı kod kullanarak aynı etkiye ulaşmak için yeni bir düğme gereklidir:</span><span class="sxs-lookup"><span data-stu-id="fef8e-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

<span data-ttu-id="fef8e-124">Gördüğünüz gibi, düğmesine bir tıklama geri gönderme oluşturur ve `ServerButton_Click()` yöntemi sunucuda yürütülür.</span><span class="sxs-lookup"><span data-stu-id="fef8e-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="fef8e-125">Bu yöntemde `launchModal()` adlı bir JavaScript işlevi, sayfa yüklendikten sonra JavaScript işlevi yürütülür:</span><span class="sxs-lookup"><span data-stu-id="fef8e-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

<span data-ttu-id="fef8e-126">`launchModal()` işi ModalPopup görüntülemektir.</span><span class="sxs-lookup"><span data-stu-id="fef8e-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="fef8e-127">Tüm HTML sayfası yüklendikten sonra `launchModal()` işlevi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="fef8e-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="fef8e-128">Ancak, ASP.NET AJAX Framework henüz tam olarak yüklenmemiştir.</span><span class="sxs-lookup"><span data-stu-id="fef8e-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="fef8e-129">Bu nedenle, `launchModal()` işlevi yalnızca ModalPopup denetiminin daha sonra gösterilmesi gereken bir değişken ayarlar:</span><span class="sxs-lookup"><span data-stu-id="fef8e-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

<span data-ttu-id="fef8e-130">`pageLoad()` JavaScript işlevi, ASP.NET AJAX tam olarak yüklendikten sonra yürütülen özel bir işlevdir.</span><span class="sxs-lookup"><span data-stu-id="fef8e-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="fef8e-131">Bu nedenle, ModalPopup denetimini göstermek için bu işleve kod ekleyeceğiz, ancak yalnızca `launchModal()` daha önce çağrılırsa:</span><span class="sxs-lookup"><span data-stu-id="fef8e-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

<span data-ttu-id="fef8e-132">`$find()` işlevi sayfada adlandırılmış bir öğe arıyor ve sunucu tarafı KIMLIĞINI parametre olarak bekler.</span><span class="sxs-lookup"><span data-stu-id="fef8e-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="fef8e-133">Bu nedenle, `$find("mpe")` ModalPopup denetiminin istemci temsilini döndürür; `show()` yöntemi, açılan pencerenin görünmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="fef8e-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>

<span data-ttu-id="fef8e-134">[düğme tıklandığında kalıcı açılan pencere ![görünür](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fef8e-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="fef8e-135">Düğme tıklandığında kalıcı açılan pencere görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fef8e-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fef8e-136">[Önceki](positioning-a-modalpopup-cs.md)
> [İleri](using-modalpopup-with-a-repeater-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fef8e-136">[Previous](positioning-a-modalpopup-cs.md)
[Next](using-modalpopup-with-a-repeater-control-vb.md)</span></span>
