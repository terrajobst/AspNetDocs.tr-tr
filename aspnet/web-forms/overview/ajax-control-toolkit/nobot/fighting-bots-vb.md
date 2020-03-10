---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
title: Fighting botları (VB) | Microsoft Docs
author: wenz
description: Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri. ASP.NET AJAX con içindeki NoBot denetimi...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9803150-452d-4521-97e3-d75d5599383c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
msc.type: authoredcontent
ms.openlocfilehash: a8ca71b96cb84c97b1a60ae6a3d1a129cd1b0b10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627395"
---
# <a name="fighting-bots-vb"></a><span data-ttu-id="97acc-104">Mücadele Botları (VB)</span><span class="sxs-lookup"><span data-stu-id="97acc-104">Fighting Bots (VB)</span></span>

<span data-ttu-id="97acc-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="97acc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="97acc-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="97acc-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span></span>

> <span data-ttu-id="97acc-107">Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri.</span><span class="sxs-lookup"><span data-stu-id="97acc-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="97acc-108">ASP.NET AJAX denetim araç setinde NoBot denetimi, bu botların filifine yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="97acc-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="overview"></a><span data-ttu-id="97acc-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="97acc-109">Overview</span></span>

<span data-ttu-id="97acc-110">Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri.</span><span class="sxs-lookup"><span data-stu-id="97acc-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="97acc-111">ASP.NET AJAX denetim araç setinde NoBot denetimi, bu botların filifine yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="97acc-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="97acc-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="97acc-112">Steps</span></span>

<span data-ttu-id="97acc-113">En az bir yaygın yaklaşım, bilgisayarlara ve ınsanlara bilgi vermek için CAPTCHAs tamamen otomatikleştirilmiş ortak bir test olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="97acc-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="97acc-114">Bir BT testi başlangıçta, birisinin bir iletişim ortağının insan veya makine olduğunu belirlemek için ihtiyaç duyduğu bir sınamadır.</span><span class="sxs-lookup"><span data-stu-id="97acc-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="97acc-115">Web 'de, bir CAPTCHA genellikle üzerinde bazı bozuk harfler içeren bir görüntüden oluşur.</span><span class="sxs-lookup"><span data-stu-id="97acc-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="97acc-116">Fikir, görüntüdeki harfleri yalnızca bir insan okuyabileceğinden, OCR algoritmalarının başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="97acc-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="97acc-117">Bu yaklaşımın çeşitli avantajları ve dezavantajları vardır ancak bunun bir tartışması, Bu öğreticinin kapsamının dışındadır.</span><span class="sxs-lookup"><span data-stu-id="97acc-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="97acc-118">Ancak, ASP.NET AJAX denetim araç setinde benzer bir yaklaşım sağlayan bir denetim vardır: `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="97acc-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="97acc-119">Bir CAPTCHA 'dan daha kolay bir şekilde ele `NoBot` alınmıştır, ancak çok daha kolay olan Bloglar gibi web sitelerinde çok daha kolay bir şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="97acc-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="97acc-120">`NoBot`, şu koşullardan en az biri karşılandığında geçerli ASP.NET Web formunun geri göndermasını karşılar:</span><span class="sxs-lookup"><span data-stu-id="97acc-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="97acc-121">Tarayıcı bir JavaScript bulmaca 'yi çözemez (JavaScript devre dışı bırakıldığında örnek için)</span><span class="sxs-lookup"><span data-stu-id="97acc-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="97acc-122">Kullanıcı formu hızlı bir şekilde gönderdi</span><span class="sxs-lookup"><span data-stu-id="97acc-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="97acc-123">İstemci IP adresi, belirli bir süre içinde formu çok sık gönderdi.</span><span class="sxs-lookup"><span data-stu-id="97acc-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="97acc-124">Bu koşulları denetlemek için, `NoBot` denetimi bu öznitelikleri gerektirir (tümü isteğe bağlıdır):</span><span class="sxs-lookup"><span data-stu-id="97acc-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="97acc-125">geri göndermeler arasındaki en az saniye miktarı `ResponseMinimumDelaySeconds`</span><span class="sxs-lookup"><span data-stu-id="97acc-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="97acc-126">bir IP 'den gelen geri göndermeler ölçülere göre `CutoffWindowSeconds` zaman aralığının uzunluğu</span><span class="sxs-lookup"><span data-stu-id="97acc-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="97acc-127">zaman aralığı başına en fazla saniye miktarı `CutoffMaximumInstances`</span><span class="sxs-lookup"><span data-stu-id="97acc-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="97acc-128">Aşağıdaki biçimlendirme, geri göndermeler arasında en az iki saniyelik bir gecikme süresi ve 30 saniyelik bir Aralık içinde yalnızca beş geri yükleme veya daha az yer olduğunu talep etmek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="97acc-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample1.aspx)]

<span data-ttu-id="97acc-129">Her zamanki gibi, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için `ScriptManager` sayfaya dahil ettiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="97acc-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample2.aspx)]

<span data-ttu-id="97acc-130">Çoğu denetim `NoBot` sunucu tarafında gerçekleşdiğinden, bu doğrulamaların sonucunu denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="97acc-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="97acc-131">Bu, `NoBot``IsValid()` yöntemi çağırarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="97acc-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="97acc-132">`NoBotState`türünde olan bir bağımsız değişken (`out` parametresi/`ByRef` parametresi olarak) vardır.</span><span class="sxs-lookup"><span data-stu-id="97acc-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="97acc-133">Dize temsili, denetimin başarısız olma nedenini içerir ve aksi takdirde `Valid`.</span><span class="sxs-lookup"><span data-stu-id="97acc-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="97acc-134">Aşağıdaki kod `NoBot`sonucuna göre bir ileti verir:</span><span class="sxs-lookup"><span data-stu-id="97acc-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample3.aspx)]

<span data-ttu-id="97acc-135">Son olarak, göndermek için bir form ve ileti çıkarmak için bir etiket öğesi gerekir ve işiniz bitti!</span><span class="sxs-lookup"><span data-stu-id="97acc-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample4.aspx)]

<span data-ttu-id="97acc-136">Bu betiği çalıştırıp JavaScript 'ı devre dışı bıraktıktan veya ilk iki saniyede formu gönderdiğinizde ya da biçimi otuz saniye içinde yedi kez gönderdiğinizde bir hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="97acc-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="97acc-137">Ancak, yalnızca% 90-95 ' un JavaScript 'in etkin olduğu için bu denetimi daha seyrek kullanın, bu nedenle kullanıcıların% 5-10 ' u `NoBot`test eder.</span><span class="sxs-lookup"><span data-stu-id="97acc-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>

<span data-ttu-id="97acc-138">[Bu hata iletisine ![bir bot neden olmuş olabilir](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="97acc-138">[![This error message could have been caused by a bot](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span></span>

<span data-ttu-id="97acc-139">Bu hata iletisi bir bot 'tan kaynaklanmış olabilir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](fighting-bots-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="97acc-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="97acc-140">Öncekini</span><span class="sxs-lookup"><span data-stu-id="97acc-140">Previous</span></span>](fighting-bots-cs.md)
