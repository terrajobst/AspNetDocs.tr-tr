---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: Bir ASP.NET Web Pages (Razor) sitesi için ziyaretçi bilgilerini (Analytics) izleme | Microsoft Docs
author: Rick-Anderson
description: Web sitenizi aldıktan sonra, Web sitesi trafiğinizi çözümlemek isteyebilirsiniz.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525188"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="012aa-103">Bir ASP.NET Web Pages (Razor) sitesi için ziyaretçi bilgilerini (Analytics) izleme</span><span class="sxs-lookup"><span data-stu-id="012aa-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="012aa-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="012aa-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="012aa-105">Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesindeki sayfalara Web sitesi analizi eklemek için bir yardımcı 'nın nasıl kullanılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="012aa-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="012aa-106">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="012aa-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="012aa-107">Bir analiz sağlayıcısına Web sitesi trafiğiniz hakkında bilgi gönderme.</span><span class="sxs-lookup"><span data-stu-id="012aa-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="012aa-108">Makalesinde sunulan ASP.NET programlama özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="012aa-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="012aa-109">`Analytics` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="012aa-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="012aa-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="012aa-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="012aa-111">ASP.NET Web sayfaları (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="012aa-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="012aa-112">ASP.NET Web yardımcıları kitaplığı (NuGet paketi)</span><span class="sxs-lookup"><span data-stu-id="012aa-112">ASP.NET Web Helpers Library (NuGet package)</span></span>

<span data-ttu-id="012aa-113">Analytics, Web sitenizdeki trafiği ölçtüğünden kişilerin siteyi nasıl kullandığını anlayabilmeniz için genel bir terimdir.</span><span class="sxs-lookup"><span data-stu-id="012aa-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="012aa-114">Google, Yahoo, StatCounter ve diğer hizmetler de dahil olmak üzere birçok analiz hizmeti mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="012aa-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="012aa-115">Analytics 'in çalışma şekli, analiz sağlayıcısına sahip bir hesap için kaydolup izlemek istediğiniz siteyi kaydetmenizi sağlar. Sağlayıcı size hesabınız için bir KIMLIK veya izleme kodu içeren bir JavaScript kodu kod parçacığı gönderir.</span><span class="sxs-lookup"><span data-stu-id="012aa-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="012aa-116">JavaScript kod parçacığını izlemek istediğiniz sitede Web sayfalarına eklersiniz. (Analiz parçacığını genellikle sitenizdeki her sayfada görüntülenen bir alt bilgiye veya Düzen sayfasına veya diğer HTML biçimlendirmesine eklersiniz.) Kullanıcılar bu JavaScript parçacıklarında birini içeren bir sayfa talep edildiğinde, kod parçacığı geçerli sayfa hakkındaki bilgileri analiz sağlayıcısına gönderir ve Bu sayfa hakkındaki çeşitli ayrıntıları kaydeder.</span><span class="sxs-lookup"><span data-stu-id="012aa-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="012aa-117">Sitenizin istatistiklerine bakmak istediğinizde, analiz sağlayıcısının Web sitesinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="012aa-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="012aa-118">Daha sonra, siteniz hakkındaki tüm rapor türlerini görüntüleyebilirsiniz, örneğin:</span><span class="sxs-lookup"><span data-stu-id="012aa-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="012aa-119">Tek tek sayfaların sayfa görüntüleme sayısı.</span><span class="sxs-lookup"><span data-stu-id="012aa-119">The number of page views for individual pages.</span></span> <span data-ttu-id="012aa-120">Bu, siteden kaç kişinin ziyaret ettiğini ve sitenizdeki hangi sayfaların en popüler olduğunu size bildirir.</span><span class="sxs-lookup"><span data-stu-id="012aa-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="012aa-121">Belirli sayfalarda ne kadar zaman harcadığını.</span><span class="sxs-lookup"><span data-stu-id="012aa-121">How long people spend on specific pages.</span></span> <span data-ttu-id="012aa-122">Bu, giriş sayfanızın insanların ilgisini tutmasına bakılmaksızın size bir şeyler söyleyebilir.</span><span class="sxs-lookup"><span data-stu-id="012aa-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="012aa-123">Sitenizi ziyaret etmeden önce insanların hangi siteler üzerinde olduğunu.</span><span class="sxs-lookup"><span data-stu-id="012aa-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="012aa-124">Bu, trafiğinizin bağlantılardan, aramalardan, vb. olduğunu anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="012aa-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="012aa-125">İnsanlar sitenizi ziyaret ettiğinde ve ne kadar süreceğine ilişkin kişiler.</span><span class="sxs-lookup"><span data-stu-id="012aa-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="012aa-126">Ziyaretçilerinizin hangi ülkeleri öğrendiklerdir.</span><span class="sxs-lookup"><span data-stu-id="012aa-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="012aa-127">Ziyaretçilerinizin kullandığı tarayıcılar ve işletim sistemleri.</span><span class="sxs-lookup"><span data-stu-id="012aa-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="012aa-129">Bir sayfaya analiz eklemek için yardımcı kullanma</span><span class="sxs-lookup"><span data-stu-id="012aa-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="012aa-130">ASP.NET Web sayfaları, analiz için kullanılan JavaScript parçacıklarını yönetmeyi kolaylaştıran çeşitli analiz yardımcıları (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`ve `Analytics.GetStatCounterHtml`) içerir.</span><span class="sxs-lookup"><span data-stu-id="012aa-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="012aa-131">JavaScript kodunun nasıl ve nereye yerleştirileceğini öğrenmek yerine, tüm yapmanız gereken bir sayfaya yardımcı eklemektir.</span><span class="sxs-lookup"><span data-stu-id="012aa-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="012aa-132">Sağlamanız gereken tek bilgi, hesap adınız, KIMLIĞINIZ veya izleme kodunuz olur.</span><span class="sxs-lookup"><span data-stu-id="012aa-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="012aa-133">(StatCounter için, birkaç ek değer de sağlamanız gerekir.)</span><span class="sxs-lookup"><span data-stu-id="012aa-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="012aa-134">Bu yordamda, `GetGoogleHtml` yardımcısını kullanan bir düzen sayfası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="012aa-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="012aa-135">Diğer analiz sağlayıcılarından birine sahip bir hesabınız zaten varsa, bunun yerine bu hesabı kullanabilir ve gereken hafif ayarlamaları yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="012aa-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="012aa-136">Bir analiz hesabı oluşturduğunuzda, izlemek istediğiniz sitenin URL 'sini kaydedersiniz.</span><span class="sxs-lookup"><span data-stu-id="012aa-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="012aa-137">Yerel bilgisayarınızdaki her şeyi test ediyorsanız, gerçek trafiği izmeyeceksiniz (tek trafik sizin olur), bu nedenle site istatistiklerini kaydedemeyecek ve görüntüleyemeyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="012aa-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="012aa-138">Ancak bu yordamda bir sayfaya nasıl analiz Yardımcısı ekleyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="012aa-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="012aa-139">Sitenizi yayımladığınızda, canlı site analiz sağlayıcınıza bilgi gönderir.</span><span class="sxs-lookup"><span data-stu-id="012aa-139">When you publish your site, the live site will send information to your analytics provider.</span></span>

1. <span data-ttu-id="012aa-140">ASP.NET Web yardımcıları kitaplığını, daha önce eklemediyseniz [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)başlığı altında açıklandığı gibi Web sitenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="012aa-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="012aa-141">Google Analytics ile bir hesap oluşturun ve hesap adını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="012aa-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="012aa-142">*Analytics. cshtml* adlı bir düzen sayfası oluşturun ve aşağıdaki biçimlendirmeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="012aa-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="012aa-143">Çağrısı, Web sayfanızın gövdesinde (`</body>` etiketinden önce) `Analytics` Yardımcısı 'na yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="012aa-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="012aa-144">Aksi takdirde, tarayıcı betiği çalıştırmaz.</span><span class="sxs-lookup"><span data-stu-id="012aa-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="012aa-145">Farklı bir analiz sağlayıcısı kullanıyorsanız, bunun yerine aşağıdaki yardımcıların birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="012aa-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="012aa-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="012aa-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="012aa-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="012aa-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="012aa-148">`myaccount`, 1. adımda oluşturduğunuz hesabın, KIMLIğIN veya izleme kodunun adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="012aa-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="012aa-149">Sayfayı tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="012aa-149">Run the page in the browser.</span></span> <span data-ttu-id="012aa-150">(Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.)</span><span class="sxs-lookup"><span data-stu-id="012aa-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="012aa-151">Tarayıcıda, sayfa kaynağını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="012aa-151">In the browser, view the page source.</span></span> <span data-ttu-id="012aa-152">İşlenmiş analiz kodunu görebileceksiniz:</span><span class="sxs-lookup"><span data-stu-id="012aa-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="012aa-153">Google Analytics sitesinde oturum açın ve sitenizin istatistiklerini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="012aa-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="012aa-154">Sayfayı canlı bir sitede çalıştırıyorsanız, sayfanıza ziyaretinizi günlüğe kaydeden bir giriş görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="012aa-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="012aa-155">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="012aa-155">Additional Resources</span></span>

- [<span data-ttu-id="012aa-156">Google Analytics sitesi</span><span class="sxs-lookup"><span data-stu-id="012aa-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="012aa-157">Yahoo! Web Analytics sitesi</span><span class="sxs-lookup"><span data-stu-id="012aa-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="012aa-158">StatCounter sitesi</span><span class="sxs-lookup"><span data-stu-id="012aa-158">StatCounter site</span></span>](http://statcounter.com/)
