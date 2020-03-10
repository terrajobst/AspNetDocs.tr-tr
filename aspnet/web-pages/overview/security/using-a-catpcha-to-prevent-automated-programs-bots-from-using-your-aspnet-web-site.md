---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: ASP.NET Web Razor) sitenizi kullanmalarını engellemek için CAPTCHA kullanma | Microsoft Docs
author: microsoft
description: Bu makalede otomatik programların (botlar) bir ASP.NET Web sayfalarında (Razor) görevleri gerçekleştirmesini engellemek için ReCaptcha 'nın (bir güvenlik ölçüsü) nasıl kullanılacağı açıklanmaktadır...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547049"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="91e8a-103">Botların ASP.NET Web Razor) sitenizi kullanmasını engellemek için CAPTCHA kullanma</span><span class="sxs-lookup"><span data-stu-id="91e8a-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="91e8a-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="91e8a-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="91e8a-105">Bu makalede otomatik programların (botlar) bir ASP.NET Web Pages (Razor) Web sitesinde görevleri gerçekleştirmesini engellemek için ReCaptcha 'nın (güvenlik ölçüsü) nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="91e8a-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="91e8a-106">**Şunları öğreneceksiniz:**</span><span class="sxs-lookup"><span data-stu-id="91e8a-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="91e8a-107">Sitenize CAPTCHA testi ekleme.</span><span class="sxs-lookup"><span data-stu-id="91e8a-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="91e8a-108">Makalesinde sunulan ASP.NET özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="91e8a-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="91e8a-109">`ReCaptcha` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="91e8a-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="91e8a-110">Bu makaledeki bilgiler, ASP.NET Web sayfaları 1,0 ve Web sayfaları 2 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="91e8a-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="91e8a-111">CAPTCHAs hakkında</span><span class="sxs-lookup"><span data-stu-id="91e8a-111">About CAPTCHAs</span></span>

<span data-ttu-id="91e8a-112">Sitenize herhangi bir zamanda kayıt yaptırıyorsanız veya bir ad ve URL (blog açıklaması gibi) girerseniz, sahte adların bir taşmasına sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91e8a-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="91e8a-113">Bunlar genellikle, bulabileceği her Web sitesinde URL 'Leri bırakmayı deneyen otomatik programlar (botlar) tarafından bırakılır.</span><span class="sxs-lookup"><span data-stu-id="91e8a-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="91e8a-114">(Yaygın bir mosyon, ürünlerin URL 'Lerini satış için göndermenize yöneliktir.)</span><span class="sxs-lookup"><span data-stu-id="91e8a-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="91e8a-115">Kullanıcıların, ad ve sitesini kaydederken veya girdiklerinde Kullanıcı doğrulamak için bir *CAPTCHA* kullanarak, bir kullanıcının gerçek bir kişi olduğundan ve bir bilgisayar programı olmadığından emin olmanıza yardımcı olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91e8a-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="91e8a-116">CAPTCHA, bilgisayarların ve Insanların ayrı olarak söylemek için tamamen otomatikleştirilmiş genel bir test için gelir.</span><span class="sxs-lookup"><span data-stu-id="91e8a-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="91e8a-117">CAPTCHA, kullanıcıdan bir kişinin yapması kolay ancak otomatik bir programın yapması zor olan bir şey yapması istenen bir *sınama yanıt* sınamadır.</span><span class="sxs-lookup"><span data-stu-id="91e8a-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="91e8a-118">En yaygın CAPTCHA türü, bazı bozuk harfler gördüğünüz ve bunları yazmaları istenen bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="91e8a-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="91e8a-119">(Deformasyon, botların harfleri çözmesidir.)</span><span class="sxs-lookup"><span data-stu-id="91e8a-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="91e8a-120">ReCaptcha testi ekleme</span><span class="sxs-lookup"><span data-stu-id="91e8a-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="91e8a-121">ASP.NET sayfalarında, ReCaptcha hizmetini ([http://recaptcha.net](http://recaptcha.net)) temel alan BIR CAPTCHA testini işlemek için `ReCaptcha` yardımcısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91e8a-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="91e8a-122">`ReCaptcha` Yardımcısı, kullanıcıların sayfa doğrulanmadan önce doğru şekilde girmesi gereken iki bozuk sözcüğün görüntüsünü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="91e8a-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="91e8a-123">Kullanıcı yanıtı ReCaptcha.Net hizmeti tarafından onaylanır.</span><span class="sxs-lookup"><span data-stu-id="91e8a-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="91e8a-124">Web sitenizi ReCaptcha.Net adresinden kaydedin ([http://recaptcha.net](http://recaptcha.net)).</span><span class="sxs-lookup"><span data-stu-id="91e8a-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="91e8a-125">Kayıt tamamlandığında, bir ortak anahtar ve özel anahtar alırsınız.</span><span class="sxs-lookup"><span data-stu-id="91e8a-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="91e8a-126">Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="91e8a-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="91e8a-127">Zaten bir *\_AppStart. cshtml* dosyanız yoksa bir Web sitesinin kök klasöründe *\_AppStart. cshtml*adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91e8a-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="91e8a-128">Aşağıdaki `Recaptcha` Yardımcısı ayarlarını *\_AppStart. cshtml* dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="91e8a-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="91e8a-129">Kendi ortak ve özel anahtarlarınızı kullanarak `PublicKey` ve `PrivateKey` özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="91e8a-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="91e8a-130">*\_AppStart. cshtml* dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="91e8a-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="91e8a-131">Bir Web sitesinin kök klasöründe *reCAPTCHA. cshtml*adlı yeni bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91e8a-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="91e8a-132">Var olan içeriği aşağıdaki ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="91e8a-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="91e8a-133">*ReCAPTCHA. cshtml* sayfasını bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="91e8a-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="91e8a-134">`PrivateKey` değeri geçerliyse, sayfada ReCaptcha denetimi ve bir düğme görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="91e8a-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="91e8a-135">Anahtarlar *\_AppStart. html*' de küresel olarak ayarlanmamışsa sayfada bir hata görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="91e8a-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="91e8a-136">Test için kelimeleri girin.</span><span class="sxs-lookup"><span data-stu-id="91e8a-136">Enter the words for the test.</span></span> <span data-ttu-id="91e8a-137">ReCaptcha testini geçirirseniz, bu etkiye bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="91e8a-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="91e8a-138">Aksi takdirde bir hata iletisi görürsünüz ve ReCaptcha denetimi yeniden görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="91e8a-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="91e8a-139">Bilgisayarınız ara sunucu kullanan bir etki alanında bulunuyorsa, *Web. config* dosyasının `defaultproxy` öğesini yapılandırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="91e8a-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="91e8a-140">Aşağıdaki örnek, ReCaptcha hizmetinin çalışmasını sağlamak için `defaultproxy` öğesi ile bir *Web. config* dosyası gösterir.</span><span class="sxs-lookup"><span data-stu-id="91e8a-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="91e8a-141">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="91e8a-141">Additional Resources</span></span>

- [<span data-ttu-id="91e8a-142">ASP.NET Web Pages siteleri için site genelinde davranışı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="91e8a-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="91e8a-143">ReCaptcha sitesi</span><span class="sxs-lookup"><span data-stu-id="91e8a-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
