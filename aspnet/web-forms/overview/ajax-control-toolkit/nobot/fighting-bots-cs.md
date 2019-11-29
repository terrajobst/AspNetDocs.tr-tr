---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: Mücadele botları (C#) | Microsoft Docs
author: wenz
description: Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri. ASP.NET AJAX con içindeki NoBot denetimi...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: fef55edf12a024e4dd66e2a18ea371ab4dac861f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606440"
---
# <a name="fighting-bots-c"></a><span data-ttu-id="f99b7-104">Mücadele Botları (C#)</span><span class="sxs-lookup"><span data-stu-id="f99b7-104">Fighting Bots (C#)</span></span>

<span data-ttu-id="f99b7-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="f99b7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f99b7-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f99b7-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span></span>

> <span data-ttu-id="f99b7-107">Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri.</span><span class="sxs-lookup"><span data-stu-id="f99b7-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="f99b7-108">ASP.NET AJAX denetim araç setinde NoBot denetimi, bu botların filifine yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f99b7-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="overview"></a><span data-ttu-id="f99b7-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="f99b7-109">Overview</span></span>

<span data-ttu-id="f99b7-110">Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri.</span><span class="sxs-lookup"><span data-stu-id="f99b7-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="f99b7-111">ASP.NET AJAX denetim araç setinde NoBot denetimi, bu botların filifine yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f99b7-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="f99b7-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="f99b7-112">Steps</span></span>

<span data-ttu-id="f99b7-113">En az bir yaygın yaklaşım, bilgisayarlara ve ınsanlara bilgi vermek için CAPTCHAs tamamen otomatikleştirilmiş ortak bir test olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f99b7-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="f99b7-114">Bir BT testi başlangıçta, birisinin bir iletişim ortağının insan veya makine olduğunu belirlemek için ihtiyaç duyduğu bir sınamadır.</span><span class="sxs-lookup"><span data-stu-id="f99b7-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="f99b7-115">Web 'de, bir CAPTCHA genellikle üzerinde bazı bozuk harfler içeren bir görüntüden oluşur.</span><span class="sxs-lookup"><span data-stu-id="f99b7-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="f99b7-116">Fikir, görüntüdeki harfleri yalnızca bir insan okuyabileceğinden, OCR algoritmalarının başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="f99b7-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="f99b7-117">Bu yaklaşımın çeşitli avantajları ve dezavantajları vardır ancak bunun bir tartışması, Bu öğreticinin kapsamının dışındadır.</span><span class="sxs-lookup"><span data-stu-id="f99b7-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="f99b7-118">Ancak, ASP.NET AJAX denetim araç setinde benzer bir yaklaşım sağlayan bir denetim vardır: `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="f99b7-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="f99b7-119">Bir CAPTCHA 'dan daha kolay bir şekilde ele `NoBot` alınmıştır, ancak çok daha kolay olan Bloglar gibi web sitelerinde çok daha kolay bir şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="f99b7-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="f99b7-120">`NoBot`, şu koşullardan en az biri karşılandığında geçerli ASP.NET Web formunun geri göndermasını karşılar:</span><span class="sxs-lookup"><span data-stu-id="f99b7-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="f99b7-121">Tarayıcı bir JavaScript bulmaca 'yi çözemez (JavaScript devre dışı bırakıldığında örnek için)</span><span class="sxs-lookup"><span data-stu-id="f99b7-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="f99b7-122">Kullanıcı formu hızlı bir şekilde gönderdi</span><span class="sxs-lookup"><span data-stu-id="f99b7-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="f99b7-123">İstemci IP adresi, belirli bir süre içinde formu çok sık gönderdi.</span><span class="sxs-lookup"><span data-stu-id="f99b7-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="f99b7-124">Bu koşulları denetlemek için, `NoBot` denetimi bu öznitelikleri gerektirir (tümü isteğe bağlıdır):</span><span class="sxs-lookup"><span data-stu-id="f99b7-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="f99b7-125">geri göndermeler arasındaki en az saniye miktarı `ResponseMinimumDelaySeconds`</span><span class="sxs-lookup"><span data-stu-id="f99b7-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="f99b7-126">bir IP 'den gelen geri göndermeler ölçülere göre `CutoffWindowSeconds` zaman aralığının uzunluğu</span><span class="sxs-lookup"><span data-stu-id="f99b7-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="f99b7-127">zaman aralığı başına en fazla saniye miktarı `CutoffMaximumInstances`</span><span class="sxs-lookup"><span data-stu-id="f99b7-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="f99b7-128">Aşağıdaki biçimlendirme, geri göndermeler arasında en az iki saniyelik bir gecikme süresi ve 30 saniyelik bir Aralık içinde yalnızca beş geri yükleme veya daha az yer olduğunu talep etmek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="f99b7-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

<span data-ttu-id="f99b7-129">Her zamanki gibi, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için `ScriptManager` sayfaya dahil ettiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="f99b7-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

<span data-ttu-id="f99b7-130">Çoğu denetim `NoBot` sunucu tarafında gerçekleşdiğinden, bu doğrulamaların sonucunu denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f99b7-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="f99b7-131">Bu, `NoBot``IsValid()` yöntemi çağırarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="f99b7-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="f99b7-132">`NoBotState`türünde olan bir bağımsız değişken (`out` parametresi/`ByRef` parametresi olarak) vardır.</span><span class="sxs-lookup"><span data-stu-id="f99b7-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="f99b7-133">Dize temsili, denetimin başarısız olma nedenini içerir ve aksi takdirde `Valid`.</span><span class="sxs-lookup"><span data-stu-id="f99b7-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="f99b7-134">Aşağıdaki kod `NoBot`sonucuna göre bir ileti verir:</span><span class="sxs-lookup"><span data-stu-id="f99b7-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

<span data-ttu-id="f99b7-135">Son olarak, göndermek için bir form ve ileti çıkarmak için bir etiket öğesi gerekir ve işiniz bitti!</span><span class="sxs-lookup"><span data-stu-id="f99b7-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

<span data-ttu-id="f99b7-136">Bu betiği çalıştırıp JavaScript 'ı devre dışı bıraktıktan veya ilk iki saniyede formu gönderdiğinizde ya da biçimi otuz saniye içinde yedi kez gönderdiğinizde bir hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f99b7-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="f99b7-137">Ancak, yalnızca% 90-95 ' un JavaScript 'in etkin olduğu için bu denetimi daha seyrek kullanın, bu nedenle kullanıcıların% 5-10 ' u `NoBot`test eder.</span><span class="sxs-lookup"><span data-stu-id="f99b7-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>

<span data-ttu-id="f99b7-138">[Bu hata iletisine ![bir bot neden olmuş olabilir](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f99b7-138">[![This error message could have been caused by a bot](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span></span>

<span data-ttu-id="f99b7-139">Bu hata iletisi bir bot 'tan kaynaklanmış olabilir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](fighting-bots-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f99b7-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f99b7-140">Next</span><span class="sxs-lookup"><span data-stu-id="f99b7-140">Next</span></span>](fighting-bots-vb.md)
