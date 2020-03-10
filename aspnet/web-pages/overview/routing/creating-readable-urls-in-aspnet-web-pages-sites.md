---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: ASP.NET Web Pages (Razor) sitelerinde okunabilir URL 'Ler oluşturma | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, ASP.NET Web Pages (Razor) Web sitesinde yönlendirmeyi ve bu, SEO için daha okunaklı ve daha iyi bir URL 'yi nasıl kullanabileceğinizi açıklar. Yapabilecekleriniz...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628396"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="728f3-104">ASP.NET Web Pages (Razor) sitelerinde okunabilir URL 'Ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="728f3-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="728f3-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="728f3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="728f3-106">Bu makalede, ASP.NET Web Pages (Razor) Web sitesinde yönlendirmeyi ve bu, SEO için daha okunaklı ve daha iyi bir URL 'yi nasıl kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="728f3-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="728f3-107">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="728f3-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="728f3-108">ASP.NET daha okunabilir ve aranabilir URL 'Ler kullanmanıza imkan sağlamak için yönlendirmeyi nasıl kullanır.</span><span class="sxs-lookup"><span data-stu-id="728f3-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="728f3-109">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="728f3-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="728f3-110">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="728f3-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="728f3-111">Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="728f3-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-routing"></a><span data-ttu-id="728f3-112">Yönlendirme hakkında</span><span class="sxs-lookup"><span data-stu-id="728f3-112">About Routing</span></span>

<span data-ttu-id="728f3-113">Sitenizdeki sayfaların URL 'Leri, sitenin ne kadar iyi çalıştığıyla ilgili bir etkiye sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="728f3-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="728f3-114">&quot;kolay&quot; bir URL, kişilerin siteyi kullanmasını kolaylaştırabilir.</span><span class="sxs-lookup"><span data-stu-id="728f3-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="728f3-115">Ayrıca, site için arama motoru iyileştirmesi (SEO) konusunda da yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="728f3-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="728f3-116">ASP.NET Web siteleri, kolay URL 'Leri otomatik olarak kullanma özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="728f3-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="728f3-117">ASP.NET, yalnızca sunucusundaki bir dosyaya işaret etmek yerine kullanıcı eylemlerini tanımlayan anlamlı URL 'Ler oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="728f3-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="728f3-118">Kurgusal bir blog için bu URL 'Leri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="728f3-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="728f3-119">Bu URL 'Leri aşağıdaki olanlarla karşılaştırın:</span><span class="sxs-lookup"><span data-stu-id="728f3-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="728f3-120">İlk çifte, kullanıcının blog *. cshtml* sayfasını kullanarak Web blogunuzun görüntülendiğini ve ardından doğru kategoriyi veya tarih aralığını alan bir sorgu dizesi oluşturacağını bilmeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="728f3-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="728f3-121">İkinci örnek kümesi, anlarsınız ve oluşturmak için çok daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="728f3-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="728f3-122">İlk örnek URL 'Leri de doğrudan belirli bir dosyaya işaret eden (*blog. cshtml*).</span><span class="sxs-lookup"><span data-stu-id="728f3-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="728f3-123">Herhangi bir nedenle blog sunucudaki başka bir klasöre taşınırsa veya blog farklı bir sayfa kullanmak üzere yeniden yazıldı, bağlantılar yanlış olur.</span><span class="sxs-lookup"><span data-stu-id="728f3-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="728f3-124">İkinci URL kümesi belirli bir sayfaya işaret etmez, bu nedenle blog uygulamasının veya konumunun değişse bile URL 'Ler hala geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="728f3-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="728f3-125">ASP.NET Web sayfalarında, Yukarıdaki örneklerde olduğu gibi, daha kolay URL 'Ler oluşturabilirsiniz çünkü ASP.NET *yönlendirme*kullanır.</span><span class="sxs-lookup"><span data-stu-id="728f3-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="728f3-126">Yönlendirme bir URL 'den, isteği yerine getirebilecek bir sayfaya (veya sayfalara) mantıksal eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="728f3-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="728f3-127">Eşleme mantıksal (belirli bir dosyaya fiziksel değil) olduğundan, yönlendirme sitenizin URL 'Lerini nasıl tanımladığınız konusunda harika bir esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="728f3-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="728f3-128">Yönlendirmenin nasıl çalıştığı</span><span class="sxs-lookup"><span data-stu-id="728f3-128">How Routing Works</span></span>

<span data-ttu-id="728f3-129">ASP.NET bir isteği işlediğinde, nasıl yönlendirileceğini anlamak için URL 'YI okur.</span><span class="sxs-lookup"><span data-stu-id="728f3-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="728f3-130">ASP.NET, soldan sağa doğru bir şekilde URL 'nin bağımsız segmentlerini disk üzerindeki dosyalarla eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="728f3-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="728f3-131">Bir eşleşme varsa, URL 'de kalan herhangi bir şey *yol bilgisi*olarak sayfaya geçirilir.</span><span class="sxs-lookup"><span data-stu-id="728f3-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="728f3-132">Birisinin bu URL 'YI kullanarak bir istek yaptığı hakkında düşünün:</span><span class="sxs-lookup"><span data-stu-id="728f3-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="728f3-133">Arama şöyle gider:</span><span class="sxs-lookup"><span data-stu-id="728f3-133">The search goes like this:</span></span>

1. <span data-ttu-id="728f3-134">*/A/b/c.exe*yolunu ve adını içeren bir dosya var mı?</span><span class="sxs-lookup"><span data-stu-id="728f3-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="728f3-135">Bu durumda, bu sayfayı çalıştırın ve bu sayfaya bilgi geçirin.</span><span class="sxs-lookup"><span data-stu-id="728f3-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="728f3-136">Aksi taktirde...</span><span class="sxs-lookup"><span data-stu-id="728f3-136">Otherwise ...</span></span>
2. <span data-ttu-id="728f3-137">*/A/b/cshtml*yolu ve adı olan bir dosya var mı?</span><span class="sxs-lookup"><span data-stu-id="728f3-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="728f3-138">Bu durumda, bu sayfayı çalıştırın ve `c` değeri geçirin.</span><span class="sxs-lookup"><span data-stu-id="728f3-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="728f3-139">Aksi takdirde...</span><span class="sxs-lookup"><span data-stu-id="728f3-139">Otherwise …</span></span>
3. <span data-ttu-id="728f3-140">*/A.exe*yolu ve adı ile bir dosya var mı?</span><span class="sxs-lookup"><span data-stu-id="728f3-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="728f3-141">Bu durumda, bu sayfayı çalıştırın ve `b/c` değeri geçirin.</span><span class="sxs-lookup"><span data-stu-id="728f3-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="728f3-142">Arama, belirtilen klasörlerinde *. cshtml* dosyaları için tam eşleşme bulmazsa, ASP.NET bu dosyaları sırayla aramaya devam eder:</span><span class="sxs-lookup"><span data-stu-id="728f3-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="728f3-143">*/a/b/c/default.exe* (yol bilgisi yok).</span><span class="sxs-lookup"><span data-stu-id="728f3-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="728f3-144">*/a/b/c/Index.cshtml* (yol bilgisi yok).</span><span class="sxs-lookup"><span data-stu-id="728f3-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="728f3-145">Açık olması için, belirli sayfalara yönelik istekler (yani, *. cshtml* dosya adı uzantısını içeren istekler) yalnızca bekleyeceğiniz gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="728f3-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="728f3-146">`http://www.contoso.com/a/b.cshtml` gibi bir istek, *b. cshtml* sayfasını sorunsuz bir şekilde çalıştıracaktır.</span><span class="sxs-lookup"><span data-stu-id="728f3-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>

<span data-ttu-id="728f3-147">Bir sayfa içinde, sayfanın `UrlData` özelliği aracılığıyla yol bilgilerini alabilir, bu bir sözlük.</span><span class="sxs-lookup"><span data-stu-id="728f3-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="728f3-148">*Viewcustomers. cshtml* adlı bir dosyanız olduğunu ve sitenizin bu isteği aldığından emin olmak için:</span><span class="sxs-lookup"><span data-stu-id="728f3-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="728f3-149">Yukarıdaki kurallarda açıklandığı gibi, istek sayfanıza gidecektir.</span><span class="sxs-lookup"><span data-stu-id="728f3-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="728f3-150">Sayfanın içinde, yol bilgilerini almak ve göstermek için aşağıdaki gibi bir kod kullanabilirsiniz (Bu durumda &quot;1000&quot;):</span><span class="sxs-lookup"><span data-stu-id="728f3-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="728f3-151">Yönlendirme tam dosya adlarını içermediğinden, aynı ada ancak farklı dosya adı uzantılarına sahip sayfalarınız varsa (örneğin, *MyPage. cshtml* ve *MyPage. html*), belirsizlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="728f3-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="728f3-152">Yönlendirme ile ilgili sorunlardan kaçınmak için, sitenizde adları yalnızca kendi uzantısında farklı olan sayfalarınız olmadığından emin olmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="728f3-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="728f3-153">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="728f3-153">Additional Resources</span></span>

<span data-ttu-id="728f3-154">[WebMatrix-URL 'ler, UrlData ve SEO Için yönlendirme](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span><span class="sxs-lookup"><span data-stu-id="728f3-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="728f3-155">Mike Brind tarafından bu blog girdisi, ASP.NET Web sayfalarında yönlendirmenin nasıl çalıştığı hakkında bazı ek ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="728f3-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
