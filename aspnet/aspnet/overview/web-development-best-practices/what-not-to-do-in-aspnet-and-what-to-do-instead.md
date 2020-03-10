---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: ASP.NET 'de ne yapacaklarınız ve bunun yerine yapılacaklar | Microsoft Docs
author: Rick-Anderson
description: Bu konu başlığı altında, insanların ASP.NET Web projeleri içinde bulunduğu birkaç yaygın hata açıklanmaktadır. Bu commo 'dan kaçınmak için yapmanız gerekenler için öneriler sağlar...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616993"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="f8c1a-104">ASP.NET’te yapılmaması gerekenler ve bunların yerine yapılması gerekenler</span><span class="sxs-lookup"><span data-stu-id="f8c1a-104">What not to do in ASP.NET, and what to do instead</span></span>

> <span data-ttu-id="f8c1a-105">Bu konu başlığı altında, insanların ASP.NET Web projeleri içinde bulunduğu birkaç yaygın hata açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-105">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="f8c1a-106">Bu, yaygın hatalardan kaçınmak için yapmanız gerekenler için öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-106">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="f8c1a-107">Bu, Norveççe Geliştirici Konferansı 'ndaki bir **edi** tarafından bir [sunumu](http://vimeo.com/68390507) temel alır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-107">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="f8c1a-108">Sorumluluk reddi</span><span class="sxs-lookup"><span data-stu-id="f8c1a-108">Disclaimer</span></span>

<span data-ttu-id="f8c1a-109">Bu konu, uygulamanızın güvenli ve verimli olmasını sağlamaya yönelik kapsamlı bir kılavuz olarak tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-109">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="f8c1a-110">Bu konuda özetlenen güvenlik ve performans için en iyi uygulamaları izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-110">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="f8c1a-111">Yalnızca .NET sınıfları ve işlemleriyle ilgili yaygın hatalardan kaçınmaya önerilir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-111">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="f8c1a-112">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="f8c1a-112">Overview</span></span>

<span data-ttu-id="f8c1a-113">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="f8c1a-113">This topic contains the following sections:</span></span>

- [<span data-ttu-id="f8c1a-114">Standartlar uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="f8c1a-114">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="f8c1a-115">Denetim bağdaştırıcıları</span><span class="sxs-lookup"><span data-stu-id="f8c1a-115">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="f8c1a-116">Denetimlerde stil özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8c1a-116">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="f8c1a-117">Sayfa ve denetim geri çağırmaları</span><span class="sxs-lookup"><span data-stu-id="f8c1a-117">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="f8c1a-118">Tarayıcı özelliği algılama</span><span class="sxs-lookup"><span data-stu-id="f8c1a-118">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="f8c1a-119">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="f8c1a-119">Security</span></span>](#security)

    - [<span data-ttu-id="f8c1a-120">İstek doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f8c1a-120">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="f8c1a-121">Tanımlama bilgisi olmayan formlar kimlik doğrulaması ve oturumu</span><span class="sxs-lookup"><span data-stu-id="f8c1a-121">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="f8c1a-122">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="f8c1a-122">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="f8c1a-123">Orta güven</span><span class="sxs-lookup"><span data-stu-id="f8c1a-123">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="f8c1a-124">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="f8c1a-124">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="f8c1a-125">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="f8c1a-125">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="f8c1a-126">Güvenilirlik ve performans</span><span class="sxs-lookup"><span data-stu-id="f8c1a-126">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="f8c1a-127">PreSendRequestHeaders ve PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="f8c1a-127">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="f8c1a-128">Web Forms ile zaman uyumsuz sayfa olayları</span><span class="sxs-lookup"><span data-stu-id="f8c1a-128">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="f8c1a-129">Yangın ve-unut Işi</span><span class="sxs-lookup"><span data-stu-id="f8c1a-129">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="f8c1a-130">Varlık gövdesi iste</span><span class="sxs-lookup"><span data-stu-id="f8c1a-130">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="f8c1a-131">Response. Redirect ve Response. End</span><span class="sxs-lookup"><span data-stu-id="f8c1a-131">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="f8c1a-132">EnableViewState ve ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="f8c1a-132">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="f8c1a-133">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="f8c1a-133">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="f8c1a-134">Uzun süre çalışan Istekler (> 110 saniye)</span><span class="sxs-lookup"><span data-stu-id="f8c1a-134">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="f8c1a-135">Standartlar uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="f8c1a-135">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="f8c1a-136">Denetim bağdaştırıcıları</span><span class="sxs-lookup"><span data-stu-id="f8c1a-136">Control adapters</span></span>

<span data-ttu-id="f8c1a-137">Öneri: Uyarlamalı işleme için denetim bağdaştırıcılarını kullanmayı durdurun ve bunun yerine CSS medya sorgularını ve standartlara uyumlu HTML 'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-137">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="f8c1a-138">Farklı cihazlar ve ortamlar için özelleştirilmiş sunu kodunu işlemek üzere .NET 2,0 ' de bulunan denetim bağdaştırıcıları tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-138">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="f8c1a-139">Artık bu Uyarlamalı işleme CSS ve HTML ile gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-139">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="f8c1a-140">Denetim bağdaştırıcılarını kullanmayı durdurup var olan bağdaştırıcıları CSS ve HTML 'ye dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-140">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="f8c1a-141">Daha fazla bilgi için bkz. [medya sorguları](http://www.w3.org/TR/css3-mediaqueries/) ve [nasıl yapılır: ASP.NET Web Forms/MVC uygulamanıza mobil sayfa ekleme](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="f8c1a-141">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="f8c1a-142">Denetimlerde stil özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8c1a-142">Style properties on controls</span></span>

<span data-ttu-id="f8c1a-143">Öneri: Denetim biçimlendirmesinde stil değerlerini ayarlamayı durdurun ve bunun yerine CSS stil sayfalarında biçimlendirme değerlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-143">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="f8c1a-144">Web sunucusu denetimleri, satır içi stil özelliklerini ayarlamak için kullanılabilecek düzinelerce özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-144">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="f8c1a-145">Örneğin, ForeColor özelliği bir denetim için metnin rengini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-145">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="f8c1a-146">CSS stil sayfaları aracılığıyla aynı etkiyi daha verimli bir şekilde gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-146">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="f8c1a-147">Stil sayfaları, stil değerlerini merkezileştirmenizi ve bu değerleri uygulamanız genelinde ayarlamaktan kaçınmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-147">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="f8c1a-148">Aşağıdaki örnek, metni kırmızı olarak ayarlayan bir CSS sınıfını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-148">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="f8c1a-149">Sonraki örnek, CSS sınıfının dinamik olarak nasıl uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-149">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="f8c1a-150">Sayfa ve denetim geri çağırmaları</span><span class="sxs-lookup"><span data-stu-id="f8c1a-150">Page and control callbacks</span></span>

<span data-ttu-id="f8c1a-151">Öneri: sayfa ve denetim geri çağırmaları kullanmayı durdurun ve bunun yerine aşağıdakilerden herhangi birini kullanın: AJAX, UpdatePanel, MVC eylem yöntemleri, Web API veya SignalR.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-151">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="f8c1a-152">Önceki ASP.NET sürümlerinde, sayfa ve denetim geri çağırma yöntemleri, bir sayfanın tamamını yenilemeksizin Web sayfasının bir bölümünü güncelleştirmenizi etkindi.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-152">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="f8c1a-153">Artık [Ajax](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) veya [SignalR](../../../signalr/index.md)aracılığıyla kısmi sayfa güncelleştirmelerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-153">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="f8c1a-154">Kolay URL 'Ler ve yönlendirme sorunları oluşmasına neden olabileceğinden, geri çağırma yöntemlerini kullanmayı durdurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-154">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="f8c1a-155">Denetimler varsayılan olarak, geri çağırma yöntemlerini etkinleştirmez, ancak bu özelliği bir denetimde etkinleştirdiyseniz, devre dışı bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-155">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="f8c1a-156">Tarayıcı özelliği algılama</span><span class="sxs-lookup"><span data-stu-id="f8c1a-156">Browser capability detection</span></span>

<span data-ttu-id="f8c1a-157">Öneri: statik tarayıcı yeteneği algılamayı kullanmayı durdurun ve bunun yerine dinamik özellik algılamayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-157">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="f8c1a-158">Önceki ASP.NET sürümlerinde, her tarayıcı için desteklenen özellikler bir XML dosyasında depolanmıştı.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-158">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="f8c1a-159">Statik arama aracılığıyla Özellik desteğini algılama en iyi yaklaşım değildir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-159">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="f8c1a-160">Şimdi, bir tarayıcının desteklenen özelliklerini [Modernizr](http://modernizr.com/)gibi bir özellik algılama çerçevesi kullanarak dinamik olarak algılayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-160">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="f8c1a-161">Özellik algılama, bir yöntemi veya özelliği kullanmayı deneyerek ve sonra tarayıcının istenen sonucu ürettiğine bakmak için desteği belirler.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-161">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="f8c1a-162">Varsayılan olarak, Modernizr, Web uygulaması şablonlarına dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-162">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="f8c1a-163">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="f8c1a-163">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="f8c1a-164">İstek doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f8c1a-164">Request validation</span></span>

<span data-ttu-id="f8c1a-165">Öneri: Kullanıcı girişini doğrulayın ve çıktıyı kullanıcılardan kodlayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-165">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="f8c1a-166">İstek doğrulama, her isteği denetleyen ve algılanan bir tehdit bulunursa isteği durduran bir ASP.NET özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-166">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="f8c1a-167">Uygulamanızı siteler arası betik saldırılarına karşı korumak için istek doğrulamasına bağlı değildir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-167">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="f8c1a-168">Bunun yerine, kullanıcıların tüm girişlerini doğrulayın ve çıktıyı kodlayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-168">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="f8c1a-169">Bazı sınırlı durumlarda, girişi doğrulamak için normal ifadeler kullanabilirsiniz, ancak daha karmaşık durumlarda değerin izin verilen değerlerle eşleşip eşleşmediğini belirten .NET sınıflarını kullanarak Kullanıcı girişini doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-169">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="f8c1a-170">Aşağıdaki örnek, bir kullanıcı tarafından girilen URI 'nin geçerli olup olmadığını anlamak için URI sınıfında statik bir yöntemin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-170">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="f8c1a-171">Ancak, URI 'yi yeterince doğrulamak için `http` veya `https`belirttiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-171">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="f8c1a-172">Aşağıdaki örnek, URI 'nin geçerli olduğunu doğrulamak için örnek yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-172">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="f8c1a-173">Kullanıcı girişini HTML olarak veya bir SQL sorgusunda Kullanıcı girişi ile birlikte işlemeden önce, kötü amaçlı kodun dahil olmamasını sağlamak için değerleri kodlayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-173">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="f8c1a-174">Biçimlendirme içindeki değeri, aşağıda gösterildiği gibi% &lt;%:%&gt; sözdizimiyle bir HTML olarak kodlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-174">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="f8c1a-175">Ya da Razor söz dizimi ' de, aşağıda gösterildiği gibi @ ile HTML kodlaması yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-175">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="f8c1a-176">Sonraki örnekte, arka plan kodundaki bir değeri HTML olarak kodlama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-176">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="f8c1a-177">Bir SQL komutları için bir değeri güvenli bir şekilde kodlamak için [Sqlparametresi](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)gibi komut parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-177">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="f8c1a-178">Tanımlama bilgisi olmayan formlar kimlik doğrulaması ve oturumu</span><span class="sxs-lookup"><span data-stu-id="f8c1a-178">Cookieless forms authentication and session</span></span>

<span data-ttu-id="f8c1a-179">Öneri: tanımlama bilgilerini gerektir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-179">Recommendation: Require cookies.</span></span>

<span data-ttu-id="f8c1a-180">Kimlik doğrulama bilgilerinin sorgu dizesinde geçirilmesi güvenli değildir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-180">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="f8c1a-181">Bu nedenle, uygulamanız kimlik doğrulaması içerdiğinde tanımlama bilgileri gerektir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-181">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="f8c1a-182">Tanımlama bilgileriniz gizli bilgileri depoluyorsa, tanımlama bilgisi için SSL istemeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-182">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="f8c1a-183">Aşağıdaki örnek, Forms kimlik doğrulamasının SSL üzerinden aktarılan bir tanımlama bilgisi gerektirdiğini Web. config dosyasında nasıl belirtmektir gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-183">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="f8c1a-184">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="f8c1a-184">EnableViewStateMac</span></span>

<span data-ttu-id="f8c1a-185">Öneri: hiçbir şekilde yanlış olarak ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-185">Recommendation: Never set to false.</span></span>

<span data-ttu-id="f8c1a-186">Varsayılan olarak, EnableViewStateMac değeri true olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-186">By default, EnableViewStateMac is set to true.</span></span> <span data-ttu-id="f8c1a-187">Uygulamanız görünüm durumunu kullanmıyor olsa da EnableViewStateMac 'i false olarak ayarlamayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-187">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="f8c1a-188">Bu değeri false olarak ayarlamak, uygulamanızı siteler arası komut dosyası oluşturma ile savunmasız hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-188">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="f8c1a-189">ASP.NET 4.5.2 'den başlayarak, çalışma zamanı **enableViewStateMac = true değerini**uygular.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-189">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="f8c1a-190">Yanlış olarak ayarlamış olsanız bile, çalışma zamanı bu değeri yoksayar ve değeri true olarak ayarlanmış şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-190">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="f8c1a-191">Daha fazla bilgi için bkz. [ASP.NET 4.5.2 ve EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8c1a-191">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="f8c1a-192">Aşağıdaki örnek, EnableViewStateMac 'i true olarak ayarlamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-192">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="f8c1a-193">Varsayılan olarak true olduğundan, bu değeri gerçekten true olarak ayarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-193">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="f8c1a-194">Ancak, uygulamanızdaki herhangi bir sayfada false olarak ayarlarsanız, bu değeri hemen düzeltmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-194">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="f8c1a-195">Orta güven</span><span class="sxs-lookup"><span data-stu-id="f8c1a-195">Medium trust</span></span>

<span data-ttu-id="f8c1a-196">Öneri: güvenlik sınırı olarak orta güvene (veya başka bir güven düzeyine) bağlı değildir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-196">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="f8c1a-197">Kısmi güven, uygulamanızı yeterince korumaz ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-197">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="f8c1a-198">Bunun yerine, tam güven kullanın ve güvenilir olmayan uygulamaları ayrı uygulama havuzlarında yalıtın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-198">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="f8c1a-199">Ayrıca, her uygulama havuzunu benzersiz bir kimlik altında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-199">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="f8c1a-200">Daha fazla bilgi için bkz. [ASP.net kısmi güven, uygulama yalıtımını garanti etmez](https://support.microsoft.com/kb/2698981).</span><span class="sxs-lookup"><span data-stu-id="f8c1a-200">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="f8c1a-201">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="f8c1a-201">&lt;appSettings&gt;</span></span>

<span data-ttu-id="f8c1a-202">Öneri: &lt;appSettings&gt; öğesinde güvenlik ayarlarını devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-202">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="f8c1a-203">AppSettings öğesi, güvenlik güncelleştirmeleri için gereken birçok değer içerir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-203">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="f8c1a-204">Bu değerleri değiştirmemelisiniz veya devre dışı bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-204">You should not change or disable these values.</span></span> <span data-ttu-id="f8c1a-205">Bir güncelleştirme dağıtımı sırasında bu değerleri devre dışı bırakmanız gerekiyorsa, dağıtımı tamamladıktan sonra hemen yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-205">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="f8c1a-206">Ayrıntılar için bkz. [ASP.net appSettings öğesi](https://msdn.microsoft.com/library/hh975440.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8c1a-206">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="f8c1a-207">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="f8c1a-207">UrlPathEncode</span></span>

<span data-ttu-id="f8c1a-208">Öneri: bunun yerine [urlencode](https://msdn.microsoft.com/library/zttxte6w.aspx) kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-208">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="f8c1a-209">UrlPathEncode yöntemi, çok özel bir tarayıcı uyumluluk sorununu çözmek için .NET Framework eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-209">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="f8c1a-210">Bir URL 'YI yeterli şekilde kodlamaz ve uygulamanızı siteler arası komut dosyası oluşturma işleminden korumaz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-210">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="f8c1a-211">Bunu uygulamanızda asla kullanmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-211">You should never use it in your application.</span></span> <span data-ttu-id="f8c1a-212">Bunun yerine, [urlencode](https://msdn.microsoft.com/library/zttxte6w.aspx)kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-212">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="f8c1a-213">Aşağıdaki örnek, bir köprü denetimi için bir kodlanmış URL 'nin sorgu dizesi parametresi olarak nasıl geçirileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-213">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="f8c1a-214">Güvenilirlik ve performans</span><span class="sxs-lookup"><span data-stu-id="f8c1a-214">Reliability and performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="f8c1a-215">PreSendRequestHeaders ve PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="f8c1a-215">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="f8c1a-216">Öneri: Bu olayları yönetilen modüllerle kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-216">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="f8c1a-217">Bunun yerine, gerekli görevi gerçekleştirmek için yerel bir IIS modülü yazın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-217">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="f8c1a-218">Bkz. [yerel kod http modülleri oluşturma](https://msdn.microsoft.com/library/ms693629.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8c1a-218">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="f8c1a-219">[PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) ve [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) olaylarını yerel IIS modülleriyle birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-219">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="f8c1a-220">`IHttpModule`uygulayan yönetilen modüllerle `PreSendRequestHeaders` ve `PreSendRequestContent` kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-220">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="f8c1a-221">Bu özelliklerin ayarlanması, zaman uyumsuz isteklerle ilgili sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-221">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="f8c1a-222">Uygulama Isteği yönlendirme (ARR) ve WebSockets birleşimi, W3wp 'in kilitlenmesine neden olabilecek erişim ihlali özel durumlarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-222">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="f8c1a-223">Örneğin, iiscore! W3_CONTEXT_BASE:: Getıblastnotification + 68 in ııscore. dll ' de bir erişim ihlali özel durumu (0xC0000005) oldu.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-223">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="f8c1a-224">Web formlarıyla zaman uyumsuz sayfa olayları</span><span class="sxs-lookup"><span data-stu-id="f8c1a-224">Asynchronous page events with web forms</span></span>

<span data-ttu-id="f8c1a-225">Öneri: Web Forms ' de, sayfa yaşam döngüsü olayları için zaman uyumsuz void yöntemleri yazmaktan kaçının ve bunun yerine zaman uyumsuz kod için [Page. RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-225">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="f8c1a-226">Bir sayfa olayını **Async** ve **void**ile işaretlediğinizde, zaman uyumsuz kodun ne zaman bittiğini belirleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-226">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="f8c1a-227">Bunun yerine, zaman uyumsuz kodu, tamamlanma durumunu izlemenize olanak verecek şekilde çalıştırmak için Page. RegisterAsyncTask kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-227">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="f8c1a-228">Aşağıdaki örnek, zaman uyumsuz kod içeren bir düğme tıklama işleyicisini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-228">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="f8c1a-229">Bu örnek, zaman uyumsuz bir görevin yalnızca Basitleştirilmiş bir örneği olarak sağlanmış olan ve önerilen bir uygulama olarak değil, zaman uyumsuz olarak bir dize değeri okumayı içerir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-229">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="f8c1a-230">Zaman uyumsuz görevler kullanıyorsanız, Web. config dosyasında http çalışma zamanı hedef çerçevesini 4,5 (veya sonraki bir sürüm) olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-230">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 (or later) in the Web.config file.</span></span> <span data-ttu-id="f8c1a-231">Hedef Framework 'ün 4,5 olarak ayarlanması, .NET 4,5 ' de eklenen yeni eşitleme bağlamını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-231">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="f8c1a-232">Bu değer, Visual Studio 'daki yeni projelerde varsayılan olarak ayarlanır, ancak var olan bir projeyle çalışıyorsanız ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-232">This value is set by default in new projects in Visual Studio, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="f8c1a-233">Yangın ve-unut işi</span><span class="sxs-lookup"><span data-stu-id="f8c1a-233">Fire-and-forget work</span></span>

<span data-ttu-id="f8c1a-234">Öneri: ASP.NET içinde bir istek işlenirken, yangın ve unutma işini başlatmaktan kaçının (ThreadPool. QueueUserWorkItem metodunu çağırmak veya bir temsilciyi tekrar tekrar çağıran bir zamanlayıcı oluşturmak).</span><span class="sxs-lookup"><span data-stu-id="f8c1a-234">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="f8c1a-235">Uygulamanız ASP.NET içinde çalışan bir yangın-ve-unut işi içeriyorsa, uygulamanız eşitlenmemiş olabilir. Herhangi bir zamanda, uygulama etki alanı yok edilebilir, böylece devam eden işlem artık uygulamanın geçerli durumuyla eşleşmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-235">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="f8c1a-236">Bu iş türünü ASP.NET dışında taşımalısınız.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-236">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="f8c1a-237">Azure 'da bir Web Işleri, Windows hizmeti veya çalışan rolü kullanarak devam eden işler gerçekleştirebilir ve bu kodu başka bir işlemden çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-237">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="f8c1a-238">Bu çalışmayı ASP.NET içinde gerçekleştirmeniz gerekiyorsa kodu çalıştırmak için [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) adlı NuGet paketini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-238">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="f8c1a-239">Varlık gövdesi iste</span><span class="sxs-lookup"><span data-stu-id="f8c1a-239">Request entity body</span></span>

<span data-ttu-id="f8c1a-240">Öneri: işleyicinin Execute olayından önce Request. form veya Request. InputStream okumaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-240">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="f8c1a-241">Request. form veya Request. InputStream öğesinden okunan en erken, işleyicinin Execute olayı sırasında.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-241">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="f8c1a-242">MVC 'de denetleyici işleyicidir ve yürütme olayı eylem yöntemi çalıştırıldığında olur.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-242">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="f8c1a-243">Web Forms, sayfa işleyicisi ve Execute olayı Page. Init olayının tetiklendiği bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-243">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="f8c1a-244">İstek varlığı gövdesini Execute olayından daha önce okuduğunuzda, isteğin işlenmesini kesintiye uğratır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-244">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="f8c1a-245">Execute olayından önce istek varlığı gövdesini okumanız gerekiyorsa, ya [Request. GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) veya [Request. GetBufferedInputStream çağrıldıktan](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-245">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="f8c1a-246">GetBufferlessInputStream kullandığınızda, istekten ham akışı alır ve tüm isteği işleme sorumluluğunu kabul edersiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-246">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="f8c1a-247">GetBufferlessInputStream çağrıldıktan sonra, Request. form ve Request. InputStream, ASP.NET tarafından doldurulmadığı için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-247">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="f8c1a-248">GetBufferedInputStream çağrıldıktan kullandığınızda, istekten akışın bir kopyasını alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-248">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="f8c1a-249">İstek. form ve Request. InputStream hala daha sonra istek içinde kullanılabilir, çünkü ASP.NET diğer kopyayı doldurur.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-249">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="f8c1a-250">Response. Redirect ve Response. End</span><span class="sxs-lookup"><span data-stu-id="f8c1a-250">Response.Redirect and Response.End</span></span>

<span data-ttu-id="f8c1a-251">Öneri: [Response. Redirect (dize)](https://msdn.microsoft.com/library/t9dwyts4.aspx)çağrıldıktan sonra iş parçacığının nasıl işlendiği farklarından haberdar olun.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-251">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="f8c1a-252">[Response. Redirect (dize)](https://msdn.microsoft.com/library/t9dwyts4.aspx) yöntemi Response. End yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-252">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="f8c1a-253">Zaman uyumlu bir işlemde, Istek. Redirect çağrısı geçerli iş parçacığının hemen iptal edilmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-253">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="f8c1a-254">Ancak, zaman uyumsuz bir işlemde, yanıt. Redirect çağrısı geçerli iş parçacığını iptal etmez, bu nedenle kod yürütmesi istek için devam eder.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-254">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="f8c1a-255">Zaman uyumsuz bir işlemde, kod yürütmeyi durdurmak için yönteminden görevi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-255">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="f8c1a-256">MVC projesinde Response. Redirect öğesini çağırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-256">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="f8c1a-257">Bunun yerine, bir RedirectResult döndürün.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-257">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="f8c1a-258">EnableViewState ve ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="f8c1a-258">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="f8c1a-259">Öneri: hangi denetimlerin görünüm durumunu kullanması üzerinde ayrıntılı denetim sağlamak için EnableViewState yerine ViewStateMode kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-259">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="f8c1a-260">Sayfa yönergesinde EnableViewState yanlış olarak ayarlandığında, sayfa içindeki tüm denetimler için Görünüm durumu devre dışı bırakılır ve etkinleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-260">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="f8c1a-261">Sayfanızda yalnızca belirli denetimler için görünüm durumunu etkinleştirmek istiyorsanız, bu sayfada ViewStateMode 'u devre dışı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-261">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="f8c1a-262">Ardından, ViewStateMode 'u yalnızca görüntüleme durumu gereken denetimlerde etkin olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-262">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="f8c1a-263">Yalnızca ihtiyacı olan denetimler için görünüm durumunu etkinleştirerek, Web sayfalarınız için Görünüm durumunun boyutunu küçültebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-263">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="f8c1a-264">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="f8c1a-264">SqlMembershipProvider</span></span>

<span data-ttu-id="f8c1a-265">Öneri: Evrensel sağlayıcıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-265">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="f8c1a-266">Geçerli proje şablonlarında, SqlMembershipProvider, bir NuGet paketi olarak kullanılabilen [ASP.net Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)ile değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-266">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="f8c1a-267">Şablonların önceki bir sürümüyle oluşturulmuş bir projede SqlMembershipProvider kullanıyorsanız, evrensel sağlayıcılara geçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-267">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="f8c1a-268">Evrensel sağlayıcılar, Entity Framework tarafından desteklenen tüm veritabanları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-268">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="f8c1a-269">Daha fazla bilgi için bkz. [ASP.net Universal Providers tanıtımı](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8c1a-269">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="f8c1a-270">Uzun süre çalışan istekler (> 110 saniye)</span><span class="sxs-lookup"><span data-stu-id="f8c1a-270">Long-running requests (>110 seconds)</span></span>

<span data-ttu-id="f8c1a-271">Öneri: bağlı istemciler için [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) veya [SignalR](../../../signalr/index.md) kullanın ve zaman uyumsuz g/ç işlemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-271">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="f8c1a-272">Uzun süre çalışan istekler, Web uygulamanızda öngörülemeyen sonuçlara ve düşük performansa neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-272">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="f8c1a-273">İstek için varsayılan zaman aşımı ayarı 110 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-273">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="f8c1a-274">Oturum durumunu uzun süre çalışan bir istekle kullanıyorsanız, ASP.NET, oturum nesnesi üzerindeki kilidi 110 saniye sonra serbest bırakacaktır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-274">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="f8c1a-275">Ancak, uygulamanız, kilit serbest bırakıldığında oturum nesnesi üzerindeki bir işlemin ortasında olabilir ve işlem başarıyla tamamlanmayabilir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-275">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="f8c1a-276">İlk istek çalışırken kullanıcıdan ikinci bir istek engellenirse ikinci istek, oturum nesnesine tutarsız bir durumda erişebilir.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-276">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="f8c1a-277">Uygulamanız engelleme (veya zaman uyumlu) g/ç işlemlerini içeriyorsa, uygulama yanıt vermemeye yönelik olur.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-277">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="f8c1a-278">Performansı artırmak için .NET Framework zaman uyumsuz g/ç işlemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-278">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="f8c1a-279">Ayrıca, istemcileri sunucusuna bağlamak için WebSockets veya SignalR kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-279">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="f8c1a-280">Bu özellikler, uzun süreli istekleri verimli bir şekilde işlemek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f8c1a-280">These features are designed to efficiently handle long-running requests.</span></span>
