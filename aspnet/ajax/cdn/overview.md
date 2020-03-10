---
uid: ajax/cdn/overview
title: Microsoft Ajax Content Delivery Network | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 92fa428608d4ac2bf56d3c6dc9c50f1449295869
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544515"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="c050f-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="c050f-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="c050f-103">Üretim uygulamaları, CDN varlıklarına sabit bir bağımlılık alamaz.</span><span class="sxs-lookup"><span data-stu-id="c050f-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="c050f-104">Uygulamalar başvurulan CDN varlığını test etmelidir ve CDN kullanılabilir olmadığında bir geri dönüş varlığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c050f-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="c050f-105">Microsoft Ajax CDN 'nin, bir Azure CDN kullanarak yukarıdaki ve sonraki bir SLA 'sı yoktur.</span><span class="sxs-lookup"><span data-stu-id="c050f-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="c050f-106">Microsoft Ajax CDN ile ilgili sorunları bildirmek için [Bu GitHub sorununu](https://github.com/dotnet/AspNetDocs/issues/116) kullanın.</span><span class="sxs-lookup"><span data-stu-id="c050f-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="c050f-107">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="c050f-107">Table of Contents</span></span>

<span data-ttu-id="c050f-108">**[ajax.microsoft.com, ajax.aspnetcdn.com olarak yeniden adlandırıldı](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="c050f-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="c050f-109">**[Visual Studio. vsdoc desteği](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="c050f-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="c050f-110">**[CDN 'den ASP.NET AJAX kullanma](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="c050f-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="c050f-111">**[CDN 'den jQuery kullanma](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="c050f-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="c050f-112">**[CDN 'den jQuery kullanıcı arabirimini kullanma](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="c050f-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="c050f-113">**[CDN 'deki üçüncü taraf dosyaları](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="c050f-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="c050f-114">CDN üzerinde jQuery yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="c050f-115">CDN üzerinde jQuery geçişi sürümleri</span><span class="sxs-lookup"><span data-stu-id="c050f-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="c050f-116">CDN üzerinde jQuery kullanıcı arabirimi yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="c050f-117">CDN üzerinde jQuery doğrulama yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="c050f-118">CDN üzerinde jQuery Mobile yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="c050f-119">CDN üzerinde jQuery şablonları yayınlar</span><span class="sxs-lookup"><span data-stu-id="c050f-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="c050f-120">CDN üzerinde jQuery Cycle yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="c050f-121">CDN üzerinde jQuery DataTable yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="c050f-122">CDN 'de Modernizr yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="c050f-123">CDN 'de Jshınt yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="c050f-124">CDN 'deki sürümleri altını gizleme</span><span class="sxs-lookup"><span data-stu-id="c050f-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="c050f-125">CDN 'de globalize sürümleri</span><span class="sxs-lookup"><span data-stu-id="c050f-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="c050f-126">CDN 'deki yanıt verme yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="c050f-127">CDN 'de önyükleme yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="c050f-128">CDN 'de önyükleme TouchCarousel sürümleri</span><span class="sxs-lookup"><span data-stu-id="c050f-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="c050f-129">CDN 'de hakökü. js yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="c050f-130">CDN 'de ASP.NET Web Forms ve Ajax sürümleri</span><span class="sxs-lookup"><span data-stu-id="c050f-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="c050f-131">CDN 'de ASP.NET MVC yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="c050f-132">CDN üzerinde ASP.NET SignalR yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="c050f-133">Microsoft Ajax Content Delivery Network (CDN), jQuery gibi popüler üçüncü taraf JavaScript kitaplıklarını barındırır ve bunları Web uygulamalarınıza kolayca eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c050f-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="c050f-134">Örneğin, ajax.aspnetcdn.com 'e işaret eden sayfanıza bir &lt;betik&gt; etiketi ekleyerek bu CDN üzerinde barındırılan jQuery kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c050f-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="c050f-135">CDN 'den yararlanarak, Ajax uygulamalarınızın performansını önemli ölçüde artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c050f-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="c050f-136">CDN içeriği dünyanın dört bir yanındaki sunucularda önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="c050f-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="c050f-137">Ayrıca, CDN, tarayıcıların farklı etki alanlarında bulunan Web siteleri için önbelleğe alınmış üçüncü taraf JavaScript dosyalarını yeniden kullanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c050f-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="c050f-138">CDN, Güvenli Yuva Katmanı kullanarak bir Web sayfasına ihtiyacınız olması durumunda SSL 'yi (HTTPS) destekler.</span><span class="sxs-lookup"><span data-stu-id="c050f-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="c050f-139">CDN, karşıya yüklenen ve size lisanslanan aşağıdaki üçüncü taraf komut dosyası kitaplıklarını bu kitaplıkların sahiplerine barındırır:</span><span class="sxs-lookup"><span data-stu-id="c050f-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="c050f-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="c050f-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="c050f-141">jQuery kullanıcı arabirimi (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="c050f-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="c050f-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="c050f-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="c050f-143">jQuery doğrulaması (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="c050f-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="c050f-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="c050f-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="c050f-145">jQuery DataTable (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="c050f-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="c050f-146">Microsoft Ajax CDN, Microsoft tarafından karşıya yüklenen aşağıdaki kitaplıkları da içerir:</span><span class="sxs-lookup"><span data-stu-id="c050f-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="c050f-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="c050f-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="c050f-148">ASP.NET MVC JavaScript dosyaları</span><span class="sxs-lookup"><span data-stu-id="c050f-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="c050f-149">ASP.NET SignalR JavaScript dosyaları</span><span class="sxs-lookup"><span data-stu-id="c050f-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="c050f-150">Microsoft, bu CDN 'de barındırılan herhangi bir üçüncü taraf kitaplıklarının sahipliğini talep etmez.</span><span class="sxs-lookup"><span data-stu-id="c050f-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="c050f-151">Kitaplıkların telif hakkı sahipleri bu kitaplıkları sizin için lisanslardır.</span><span class="sxs-lookup"><span data-stu-id="c050f-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="c050f-152">Bu tür kitaplıkları indirmeniz ve kullanmanız gereken haklar yalnızca ilgili telif hakkı sahipleri tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="c050f-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="c050f-153">Bunlar Microsoft kitaplıkları olmadığından, bu CDN 'de barındırılan üçüncü taraf kitaplıkları için Microsoft hiçbir garanti veya fikri mülkiyet hakları lisansı (zımni patent hakları dahil) sağlar.</span><span class="sxs-lookup"><span data-stu-id="c050f-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="c050f-154">JavaScript kitaplığınızı ve kitaplığınız, en üst JavaScript kitaplıklarından ((a) popüler olan bu kitaplıkların http://trends.builtwith.com) veya uzantıları/eklentileri bölümünde listelendiği gibi, ya da (b) ASP.NET üzerinde kullanım için yararlı olduğundan, lütfen AjaxCDNSubmission@Microsoft.combaşvurun.</span><span class="sxs-lookup"><span data-stu-id="c050f-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="c050f-155">ajax.microsoft.com, ajax.aspnetcdn.com olarak yeniden adlandırıldı</span><span class="sxs-lookup"><span data-stu-id="c050f-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="c050f-156">Microsoft.com etki alanı adını kullanmak için kullanılan CDN, aspnetcdn.com etki alanı adını kullanacak şekilde değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c050f-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="c050f-157">Bu değişiklik performansı artırmak için yapılmıştır çünkü bir tarayıcı microsoft.com etki alanına başvurduğu zaman, her istekle birlikte bu etki alanındaki herhangi bir tanımlama bilgisini gönderir.</span><span class="sxs-lookup"><span data-stu-id="c050f-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="c050f-158">Microsoft.com performansının dışındaki bir etki alanı adına yeniden adlandırarak, %25 ' e kadar artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="c050f-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="c050f-159">Note ajax.microsoft.com çalışmaya devam edecektir ancak ajax.aspnetcdn.com önerilir.</span><span class="sxs-lookup"><span data-stu-id="c050f-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="c050f-160">Eski biçim: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="c050f-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="c050f-161">Yeni biçim: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="c050f-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="c050f-162">Visual Studio. vsdoc desteği</span><span class="sxs-lookup"><span data-stu-id="c050f-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="c050f-163">. Vsdoc dosyalarını Visual Studio 2008 ile düzgün şekilde kullanmak için, VS 2008 SP1 'in yüklü olduğundan ve vsdoc dosyalarının düzeltmesinin yüklü olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c050f-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="c050f-164">Bunları buradan öğrenebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c050f-164">You can get these from here:</span></span>

- [<span data-ttu-id="c050f-165">Visual Studio 2008 SP1 'i indirin</span><span class="sxs-lookup"><span data-stu-id="c050f-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 SP1 'i indirin")
- [<span data-ttu-id="c050f-166">Visual Studio 2008 SP1 için. vsdoc düzeltmesini indirin</span><span class="sxs-lookup"><span data-stu-id="c050f-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 SP1 için. vsdoc düzeltmesini indirin")

<span data-ttu-id="c050f-167">Visual Studio 2010, ek düzeltme ekleri olmadan. vsdoc dosyalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="c050f-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="c050f-168">CDN 'den ASP.NET AJAX kullanma</span><span class="sxs-lookup"><span data-stu-id="c050f-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="c050f-169">ASP.NET 4 kullanırken, tüm ASP.NET Framework betikleri isteklerini CDN 'ye yeniden yönlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c050f-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="c050f-170">Yerel Web sunucunuz yerine CDN 'den betikler alma, genel ASP.NET Web sitelerinin performansını önemli ölçüde iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c050f-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="c050f-171">Tüm ASP.NET Framework betik isteklerini Microsoft Ajax CDN 'ye yönlendirmek için ScriptManager EnableCDN özelliğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="c050f-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="c050f-172">CDN 'den jQuery kullanma</span><span class="sxs-lookup"><span data-stu-id="c050f-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="c050f-173">Aşağıdaki betik öğesini bir sayfaya ekleyerek, Web uygulamanızda CDN üzerinde barındırılan jQuery betiklerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c050f-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="c050f-174">CDN, jQuery betiğinin mini kullanılan sürümünü de içerir ve bu, aşağıdaki öğeyi kullanarak edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c050f-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="c050f-175">Sayfanızın, CDN 'nin kullanılamaz olması durumunda kendi web sitenizde yerel bir yoldan jQuery yüklemeye geri dönüşü sağlamak için, CDN 'e başvuran öğeden hemen sonra aşağıdaki öğeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c050f-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="c050f-176">Aşağıdaki örnek sayfa, bir düğmeye tıklandığında bir div öğesinin içeriğini göstermek için jQuery kitaplığının CDN sürümünü (yerel bir kopyaya geri dönüş ile) kullanır.</span><span class="sxs-lookup"><span data-stu-id="c050f-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="c050f-177">JQuery hakkında daha fazla bilgi alabilir ve [jQuery Web sitesini](http://jquery.com/) ziyaret ederek jQuery 'in yerel bir kopyasını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c050f-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="c050f-178">CDN 'den jQuery kullanıcı arabirimini kullanma</span><span class="sxs-lookup"><span data-stu-id="c050f-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="c050f-179">CDN, jQuery kullanıcı arabirimi kitaplığını da barındırır.</span><span class="sxs-lookup"><span data-stu-id="c050f-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="c050f-180">JQuery kullanıcı arabirimi kitaplığı, ASP.NET uygulamalarınızda kullanabileceğiniz zengin bir pencere öğesi ve efekt kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="c050f-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="c050f-181">Örneğin, aşağıdaki sayfada bir ASP.NET Web Forms uygulaması bağlamında bir açılır takvimi göstermek için jQuery UI DatePicker nasıl kullanabileceğiniz gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c050f-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="c050f-182">Klavyenizi kullanarak metin kutusuna odağı taşıdığınızda bir takvim görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="c050f-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![DatePicker ile oluşturulan açılan takvim](overview/_static/image1.png)

<span data-ttu-id="c050f-184">Yukarıdaki kodda CDN 'den üç dosya eklemeniz gerektiğini unutmayın:</span><span class="sxs-lookup"><span data-stu-id="c050f-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="c050f-185">JQuery kitaplığı &mdash; jQuery kitaplığı, jQuery kitaplığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c050f-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="c050f-186">JQuery kullanıcı arabirimi kitaplığını eklemeden önce jQuery kitaplığını sayfanıza eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c050f-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="c050f-187">JQuery kullanıcı arabirimi kitaplığı &mdash; jQuery UI kitaplığı, Yukarıdaki sayfada kullanılan tüm jQuery kullanıcı arabirimi efektlerini ve DatePicker pencere öğesi gibi pencere öğelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c050f-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="c050f-188">JQuery kullanıcı ARABIRIMI farklı temaları desteklediğinden jQuery kullanıcı arabirimi teması &mdash;.</span><span class="sxs-lookup"><span data-stu-id="c050f-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="c050f-189">Yukarıdaki sayfa, Redmond temasını içeri aktarmak için CSS dosyasının bir bağlantısını içerir.</span><span class="sxs-lookup"><span data-stu-id="c050f-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="c050f-190">Tüm standart jQuery UI temaları CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c050f-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="c050f-191">Her temanın küçük resimlerini görüntülemek için [Bu sayfayı ziyaret edin](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.10") .</span><span class="sxs-lookup"><span data-stu-id="c050f-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="c050f-192">JQuery kullanıcı arabirimi kitaplığı hakkında daha fazla bilgi edinmek için resmi [jQuery kullanıcı arabirimi Web sitesini](http://jQueryUI.com "jQuery kullanıcı arabirimi Web sitesi")ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="c050f-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="c050f-193">CDN 'deki üçüncü taraf dosyaları</span><span class="sxs-lookup"><span data-stu-id="c050f-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="c050f-194">CDN, en popüler üçüncü taraf JavaScript kitaplıklarından bazılarını barındırır.</span><span class="sxs-lookup"><span data-stu-id="c050f-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="c050f-195">Microsoft, bu CDN 'de barındırılan herhangi bir üçüncü taraf kitaplıklarının sahipliğini talep etmez.</span><span class="sxs-lookup"><span data-stu-id="c050f-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="c050f-196">Kitaplıkların telif hakkı sahipleri bu kitaplıkları sizin için lisanslardır.</span><span class="sxs-lookup"><span data-stu-id="c050f-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="c050f-197">Bu tür kitaplıkları indirmeniz ve kullanmanız gereken haklar yalnızca ilgili telif hakkı sahipleri tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="c050f-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="c050f-198">Bunlar Microsoft kitaplıkları olmadığından, bu CDN 'de barındırılan üçüncü taraf kitaplıkları için Microsoft hiçbir garanti veya fikri mülkiyet hakları lisansı (zımni patent hakları dahil) sağlar.</span><span class="sxs-lookup"><span data-stu-id="c050f-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="c050f-199">CDN üzerinde jQuery yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="c050f-200">JQuery 'in aşağıdaki sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-341"></a><span data-ttu-id="c050f-201">jQuery sürümü 3.4.1</span><span class="sxs-lookup"><span data-stu-id="c050f-201">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="c050f-202">jQuery sürümü 3.4.0</span><span class="sxs-lookup"><span data-stu-id="c050f-202">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="c050f-203">jQuery sürümü 3.3.1</span><span class="sxs-lookup"><span data-stu-id="c050f-203">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="c050f-204">jQuery sürümü 3.2.1</span><span class="sxs-lookup"><span data-stu-id="c050f-204">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="c050f-205">jQuery sürümü 3.2.0</span><span class="sxs-lookup"><span data-stu-id="c050f-205">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="c050f-206">jQuery sürümü 3.1.1</span><span class="sxs-lookup"><span data-stu-id="c050f-206">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="c050f-207">jQuery sürümü 3.1.0</span><span class="sxs-lookup"><span data-stu-id="c050f-207">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="c050f-208">jQuery sürümü 3.0.0</span><span class="sxs-lookup"><span data-stu-id="c050f-208">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="c050f-209">jQuery sürümü 2.2.4</span><span class="sxs-lookup"><span data-stu-id="c050f-209">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="c050f-210">jQuery sürümü 2.2.3</span><span class="sxs-lookup"><span data-stu-id="c050f-210">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="c050f-211">jQuery sürümü 2.2.2</span><span class="sxs-lookup"><span data-stu-id="c050f-211">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="c050f-212">jQuery sürümü 2.2.1</span><span class="sxs-lookup"><span data-stu-id="c050f-212">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="c050f-213">jQuery sürümü 2.2.0</span><span class="sxs-lookup"><span data-stu-id="c050f-213">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="c050f-214">jQuery sürümü 2.1.4</span><span class="sxs-lookup"><span data-stu-id="c050f-214">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="c050f-215">jQuery sürümü 2.1.3</span><span class="sxs-lookup"><span data-stu-id="c050f-215">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="c050f-216">jQuery sürümü 2.1.2 'yi</span><span class="sxs-lookup"><span data-stu-id="c050f-216">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="c050f-217">jQuery sürümü 2.1.1</span><span class="sxs-lookup"><span data-stu-id="c050f-217">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="c050f-218">jQuery sürümü 2.1.0</span><span class="sxs-lookup"><span data-stu-id="c050f-218">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="c050f-219">jQuery sürümü 2.0.3</span><span class="sxs-lookup"><span data-stu-id="c050f-219">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="c050f-220">jQuery sürümü 2.0.2</span><span class="sxs-lookup"><span data-stu-id="c050f-220">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="c050f-221">jQuery sürüm 2.0.1</span><span class="sxs-lookup"><span data-stu-id="c050f-221">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="c050f-222">jQuery sürümü 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c050f-222">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="c050f-223">jQuery sürümü 1.12.4</span><span class="sxs-lookup"><span data-stu-id="c050f-223">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="c050f-224">jQuery sürümü 1.12.3</span><span class="sxs-lookup"><span data-stu-id="c050f-224">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="c050f-225">jQuery sürümü 1.12.2</span><span class="sxs-lookup"><span data-stu-id="c050f-225">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="c050f-226">jQuery sürümü 1.12.1</span><span class="sxs-lookup"><span data-stu-id="c050f-226">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="c050f-227">jQuery sürümü 1.12.0</span><span class="sxs-lookup"><span data-stu-id="c050f-227">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="c050f-228">jQuery sürümü 1.11.3</span><span class="sxs-lookup"><span data-stu-id="c050f-228">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="c050f-229">jQuery sürümü 1.11.2</span><span class="sxs-lookup"><span data-stu-id="c050f-229">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="c050f-230">jQuery sürümü 1.11.1</span><span class="sxs-lookup"><span data-stu-id="c050f-230">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="c050f-231">jQuery sürümü 1.11.0</span><span class="sxs-lookup"><span data-stu-id="c050f-231">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="c050f-232">jQuery sürümü 1.10.2</span><span class="sxs-lookup"><span data-stu-id="c050f-232">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="c050f-233">jQuery sürümü 1.10.1</span><span class="sxs-lookup"><span data-stu-id="c050f-233">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="c050f-234">jQuery sürümü 1.10.0</span><span class="sxs-lookup"><span data-stu-id="c050f-234">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="c050f-235">jQuery sürümü 1.9.1</span><span class="sxs-lookup"><span data-stu-id="c050f-235">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="c050f-236">jQuery sürümü 1.9.0</span><span class="sxs-lookup"><span data-stu-id="c050f-236">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="c050f-237">jQuery sürümü 1.8.3 birden fazla</span><span class="sxs-lookup"><span data-stu-id="c050f-237">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="c050f-238">jQuery sürümü 1.8.2</span><span class="sxs-lookup"><span data-stu-id="c050f-238">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="c050f-239">jQuery sürümü 1.8.1</span><span class="sxs-lookup"><span data-stu-id="c050f-239">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="c050f-240">jQuery sürümü 1.8.0</span><span class="sxs-lookup"><span data-stu-id="c050f-240">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="c050f-241">jQuery sürümü 1.7.2</span><span class="sxs-lookup"><span data-stu-id="c050f-241">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="c050f-242">jQuery sürümü 1.7.1</span><span class="sxs-lookup"><span data-stu-id="c050f-242">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="c050f-243">jQuery sürüm 1,7</span><span class="sxs-lookup"><span data-stu-id="c050f-243">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="c050f-244">jQuery sürümü 1.6.4</span><span class="sxs-lookup"><span data-stu-id="c050f-244">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="c050f-245">jQuery sürümü 1.6.3</span><span class="sxs-lookup"><span data-stu-id="c050f-245">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="c050f-246">jQuery sürümü 1.6.2</span><span class="sxs-lookup"><span data-stu-id="c050f-246">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="c050f-247">jQuery sürümü 1.6.1</span><span class="sxs-lookup"><span data-stu-id="c050f-247">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="c050f-248">jQuery sürüm 1,6</span><span class="sxs-lookup"><span data-stu-id="c050f-248">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="c050f-249">jQuery sürümü 1.5.2 planlama</span><span class="sxs-lookup"><span data-stu-id="c050f-249">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="c050f-250">jQuery sürümü 1.5.1</span><span class="sxs-lookup"><span data-stu-id="c050f-250">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="c050f-251">jQuery sürüm 1,5</span><span class="sxs-lookup"><span data-stu-id="c050f-251">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="c050f-252">jQuery sürümü 1.4.4</span><span class="sxs-lookup"><span data-stu-id="c050f-252">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="c050f-253">jQuery sürümü 1.4.3</span><span class="sxs-lookup"><span data-stu-id="c050f-253">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="c050f-254">jQuery sürümü 1.4.2</span><span class="sxs-lookup"><span data-stu-id="c050f-254">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="c050f-255">jQuery sürümü 1.4.1</span><span class="sxs-lookup"><span data-stu-id="c050f-255">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="c050f-256">jQuery sürüm 1,4</span><span class="sxs-lookup"><span data-stu-id="c050f-256">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="c050f-257">jQuery sürümü 1.3.2</span><span class="sxs-lookup"><span data-stu-id="c050f-257">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="c050f-258">CDN üzerinde jQuery geçişi sürümleri</span><span class="sxs-lookup"><span data-stu-id="c050f-258">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="c050f-259">JQuery geçişi 'nin aşağıdaki sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-259">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="c050f-260">jQuery geçişi sürüm 3.0.0</span><span class="sxs-lookup"><span data-stu-id="c050f-260">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="c050f-261">jQuery geçişi sürüm 1.2.1</span><span class="sxs-lookup"><span data-stu-id="c050f-261">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="c050f-262">jQuery geçişi sürüm 1.2.0</span><span class="sxs-lookup"><span data-stu-id="c050f-262">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="c050f-263">jQuery geçişi sürüm 1.1.1</span><span class="sxs-lookup"><span data-stu-id="c050f-263">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="c050f-264">jQuery geçişi sürüm 1.1.0</span><span class="sxs-lookup"><span data-stu-id="c050f-264">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="c050f-265">jQuery geçişi sürüm 1.0.0</span><span class="sxs-lookup"><span data-stu-id="c050f-265">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="c050f-266">CDN üzerinde jQuery kullanıcı arabirimi yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-266">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="c050f-267">JQuery kullanıcı arabirimi kitaplığı 'nın aşağıdaki sürümleri bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c050f-267">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="c050f-268">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c050f-268">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="c050f-269">jQuery kullanıcı arabirimi 1.12.1</span><span class="sxs-lookup"><span data-stu-id="c050f-269">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.12.1")
- [<span data-ttu-id="c050f-270">jQuery kullanıcı arabirimi 1.12.0</span><span class="sxs-lookup"><span data-stu-id="c050f-270">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.12.0")
- [<span data-ttu-id="c050f-271">jQuery kullanıcı arabirimi 1.11.4</span><span class="sxs-lookup"><span data-stu-id="c050f-271">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.4")
- [<span data-ttu-id="c050f-272">jQuery kullanıcı arabirimi 1.11.3</span><span class="sxs-lookup"><span data-stu-id="c050f-272">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.3")
- [<span data-ttu-id="c050f-273">jQuery kullanıcı arabirimi 1.11.2</span><span class="sxs-lookup"><span data-stu-id="c050f-273">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.2")
- [<span data-ttu-id="c050f-274">jQuery kullanıcı arabirimi 1.11.1</span><span class="sxs-lookup"><span data-stu-id="c050f-274">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.1")
- [<span data-ttu-id="c050f-275">jQuery kullanıcı arabirimi 1.11.0</span><span class="sxs-lookup"><span data-stu-id="c050f-275">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.0")
- [<span data-ttu-id="c050f-276">jQuery kullanıcı arabirimi 1.10.4</span><span class="sxs-lookup"><span data-stu-id="c050f-276">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.4")
- [<span data-ttu-id="c050f-277">jQuery kullanıcı arabirimi 1.10.3</span><span class="sxs-lookup"><span data-stu-id="c050f-277">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.3")
- [<span data-ttu-id="c050f-278">jQuery kullanıcı arabirimi 1.10.2</span><span class="sxs-lookup"><span data-stu-id="c050f-278">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.2")
- [<span data-ttu-id="c050f-279">jQuery kullanıcı arabirimi 1.10.1</span><span class="sxs-lookup"><span data-stu-id="c050f-279">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.1")
- [<span data-ttu-id="c050f-280">jQuery kullanıcı arabirimi 1.10.0</span><span class="sxs-lookup"><span data-stu-id="c050f-280">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.0")
- [<span data-ttu-id="c050f-281">jQuery kullanıcı arabirimi 1.9.2</span><span class="sxs-lookup"><span data-stu-id="c050f-281">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.2")
- [<span data-ttu-id="c050f-282">jQuery kullanıcı arabirimi 1.9.1</span><span class="sxs-lookup"><span data-stu-id="c050f-282">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.1")
- [<span data-ttu-id="c050f-283">jQuery kullanıcı arabirimi 1.9.0</span><span class="sxs-lookup"><span data-stu-id="c050f-283">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.0")
- [<span data-ttu-id="c050f-284">jQuery kullanıcı arabirimi 1.8.24</span><span class="sxs-lookup"><span data-stu-id="c050f-284">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.24")
- [<span data-ttu-id="c050f-285">jQuery kullanıcı arabirimi 1.8.23</span><span class="sxs-lookup"><span data-stu-id="c050f-285">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.23")
- [<span data-ttu-id="c050f-286">jQuery kullanıcı arabirimi 1.8.22</span><span class="sxs-lookup"><span data-stu-id="c050f-286">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.22")
- [<span data-ttu-id="c050f-287">jQuery kullanıcı arabirimi 1.8.21</span><span class="sxs-lookup"><span data-stu-id="c050f-287">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.21")
- [<span data-ttu-id="c050f-288">jQuery kullanıcı arabirimi 1.8.20</span><span class="sxs-lookup"><span data-stu-id="c050f-288">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.20")
- [<span data-ttu-id="c050f-289">jQuery kullanıcı arabirimi 1.8.19</span><span class="sxs-lookup"><span data-stu-id="c050f-289">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.19")
- [<span data-ttu-id="c050f-290">jQuery kullanıcı arabirimi 1.8.18</span><span class="sxs-lookup"><span data-stu-id="c050f-290">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.18")
- [<span data-ttu-id="c050f-291">jQuery kullanıcı arabirimi 1.8.17</span><span class="sxs-lookup"><span data-stu-id="c050f-291">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.17")
- [<span data-ttu-id="c050f-292">jQuery kullanıcı arabirimi 1.8.16</span><span class="sxs-lookup"><span data-stu-id="c050f-292">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.16")
- [<span data-ttu-id="c050f-293">jQuery kullanıcı arabirimi 1.8.15</span><span class="sxs-lookup"><span data-stu-id="c050f-293">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.15")
- [<span data-ttu-id="c050f-294">jQuery kullanıcı arabirimi 1.8.14</span><span class="sxs-lookup"><span data-stu-id="c050f-294">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.14")
- [<span data-ttu-id="c050f-295">jQuery kullanıcı arabirimi 1.8.13</span><span class="sxs-lookup"><span data-stu-id="c050f-295">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.13")
- [<span data-ttu-id="c050f-296">jQuery kullanıcı arabirimi 1.8.12</span><span class="sxs-lookup"><span data-stu-id="c050f-296">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.12")
- [<span data-ttu-id="c050f-297">jQuery kullanıcı arabirimi 1.8.11</span><span class="sxs-lookup"><span data-stu-id="c050f-297">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.11")
- [<span data-ttu-id="c050f-298">jQuery kullanıcı arabirimi 1.8.10</span><span class="sxs-lookup"><span data-stu-id="c050f-298">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.10")
- [<span data-ttu-id="c050f-299">jQuery kullanıcı arabirimi 1.8.9</span><span class="sxs-lookup"><span data-stu-id="c050f-299">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.9")
- [<span data-ttu-id="c050f-300">jQuery kullanıcı arabirimi 1.8.8</span><span class="sxs-lookup"><span data-stu-id="c050f-300">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.8")
- [<span data-ttu-id="c050f-301">jQuery kullanıcı arabirimi 1.8.7</span><span class="sxs-lookup"><span data-stu-id="c050f-301">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.7")
- [<span data-ttu-id="c050f-302">jQuery kullanıcı arabirimi 1.8.6</span><span class="sxs-lookup"><span data-stu-id="c050f-302">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.6")
- [<span data-ttu-id="c050f-303">jQuery Kullanıcı Arabirimi 1.8.5</span><span class="sxs-lookup"><span data-stu-id="c050f-303">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery Kullanıcı Arabirimi 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="c050f-304">CDN üzerinde jQuery doğrulama yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-304">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="c050f-305">[JQuery doğrulama](https://jqueryvalidation.org/ "jQuery doğrulama eklentisi") eklentisinin aşağıdaki SÜRÜMLERI bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c050f-305">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="c050f-306">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c050f-306">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="c050f-307">jQuery Validate 1.19.1</span><span class="sxs-lookup"><span data-stu-id="c050f-307">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery doğrulama 1.19.1")
- [<span data-ttu-id="c050f-308">jQuery Validate 1.19.0</span><span class="sxs-lookup"><span data-stu-id="c050f-308">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery doğrulama 1.19.0")
- [<span data-ttu-id="c050f-309">jQuery Validate 1.17.0</span><span class="sxs-lookup"><span data-stu-id="c050f-309">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery doğrulama 1.17.0")
- [<span data-ttu-id="c050f-310">jQuery Validate 1.16.0</span><span class="sxs-lookup"><span data-stu-id="c050f-310">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Doğrulaması 1.16.0")
- [<span data-ttu-id="c050f-311">jQuery Validate 1.15.1</span><span class="sxs-lookup"><span data-stu-id="c050f-311">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Doğrulaması 1.15.1")
- [<span data-ttu-id="c050f-312">jQuery Validate 1.15.0</span><span class="sxs-lookup"><span data-stu-id="c050f-312">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Doğrulaması 1.15.0")
- [<span data-ttu-id="c050f-313">jQuery Validate 1.14.0</span><span class="sxs-lookup"><span data-stu-id="c050f-313">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Doğrulaması 1.14.0")
- [<span data-ttu-id="c050f-314">jQuery Validate 1.13.1</span><span class="sxs-lookup"><span data-stu-id="c050f-314">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Doğrulaması 1.13.1")
- [<span data-ttu-id="c050f-315">jQuery Validate 1.13.0</span><span class="sxs-lookup"><span data-stu-id="c050f-315">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Doğrulaması 1.13.0")
- [<span data-ttu-id="c050f-316">jQuery Validate 1.12.0</span><span class="sxs-lookup"><span data-stu-id="c050f-316">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Doğrulaması 1.12.0")
- [<span data-ttu-id="c050f-317">jQuery Validate 1.11.1</span><span class="sxs-lookup"><span data-stu-id="c050f-317">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Doğrulaması 1.11.1")
- [<span data-ttu-id="c050f-318">jQuery Validate 1.11.0</span><span class="sxs-lookup"><span data-stu-id="c050f-318">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Doğrulaması 1.11.0")
- [<span data-ttu-id="c050f-319">jQuery Validate 1.10.0</span><span class="sxs-lookup"><span data-stu-id="c050f-319">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Doğrulaması 1.10.0")
- [<span data-ttu-id="c050f-320">jQuery doğrulaması 1,9</span><span class="sxs-lookup"><span data-stu-id="c050f-320">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate sürümü 1.9")
- [<span data-ttu-id="c050f-321">jQuery Validate 1.8.1</span><span class="sxs-lookup"><span data-stu-id="c050f-321">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate sürümü 1.8.1")
- [<span data-ttu-id="c050f-322">jQuery doğrulaması 1,8</span><span class="sxs-lookup"><span data-stu-id="c050f-322">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate sürümü 1.8")
- [<span data-ttu-id="c050f-323">jQuery doğrulaması 1,7</span><span class="sxs-lookup"><span data-stu-id="c050f-323">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate sürümü 1.7")
- [<span data-ttu-id="c050f-324">jQuery Doğrulama 1.6</span><span class="sxs-lookup"><span data-stu-id="c050f-324">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Doğrulama 1.6")
- [<span data-ttu-id="c050f-325">jQuery Doğrulama 1.5.5</span><span class="sxs-lookup"><span data-stu-id="c050f-325">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Doğrulama 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="c050f-326">CDN üzerinde jQuery Mobile yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-326">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="c050f-327">JQuery mobile Library 'in aşağıdaki sürümleri bu CDN 'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c050f-327">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="c050f-328">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c050f-328">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="c050f-329">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="c050f-329">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.5")
- [<span data-ttu-id="c050f-330">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="c050f-330">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.2")
- [<span data-ttu-id="c050f-331">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="c050f-331">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.1")
- [<span data-ttu-id="c050f-332">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="c050f-332">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.0")
- [<span data-ttu-id="c050f-333">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="c050f-333">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.2")
- [<span data-ttu-id="c050f-334">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="c050f-334">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.1")
- [<span data-ttu-id="c050f-335">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="c050f-335">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.0")
- [<span data-ttu-id="c050f-336">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="c050f-336">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.2.0")
- [<span data-ttu-id="c050f-337">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="c050f-337">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.2")
- [<span data-ttu-id="c050f-338">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="c050f-338">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.1")
- [<span data-ttu-id="c050f-339">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="c050f-339">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.0")
- [<span data-ttu-id="c050f-340">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="c050f-340">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="c050f-341">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="c050f-341">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0.1")
- [<span data-ttu-id="c050f-342">jQuery Mobile 1,0</span><span class="sxs-lookup"><span data-stu-id="c050f-342">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0")
- [<span data-ttu-id="c050f-343">jQuery Mobile 1,0 RC 2</span><span class="sxs-lookup"><span data-stu-id="c050f-343">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="c050f-344">jQuery Mobile 1,0 RC 1</span><span class="sxs-lookup"><span data-stu-id="c050f-344">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="c050f-345">jQuery Mobile 1,0 Beta 3</span><span class="sxs-lookup"><span data-stu-id="c050f-345">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="c050f-346">CDN üzerinde jQuery şablonları yayınlar</span><span class="sxs-lookup"><span data-stu-id="c050f-346">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="c050f-347">JQuery şablonları eklentisinin aşağıdaki sürümleri bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c050f-347">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="c050f-348">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c050f-348">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="c050f-349">jQuery Şablonları Beta 1</span><span class="sxs-lookup"><span data-stu-id="c050f-349">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Şablonları Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="c050f-350">CDN üzerinde jQuery Cycle yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-350">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="c050f-351">JQuery Cycle eklentisinin aşağıdaki sürümleri bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c050f-351">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="c050f-352">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c050f-352">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="c050f-353">jQuery Döngüsü 2.99</span><span class="sxs-lookup"><span data-stu-id="c050f-353">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Döngüsü 2.99")
- [<span data-ttu-id="c050f-354">jQuery Döngüsü 2.94</span><span class="sxs-lookup"><span data-stu-id="c050f-354">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Döngüsü 2.94")
- [<span data-ttu-id="c050f-355">jQuery Döngüsü 2.88</span><span class="sxs-lookup"><span data-stu-id="c050f-355">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Döngüsü 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="c050f-356">CDN üzerinde jQuery DataTable yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-356">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="c050f-357">JQuery DataTable eklentisinin aşağıdaki sürümleri bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c050f-357">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="c050f-358">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c050f-358">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="c050f-359">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="c050f-359">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="c050f-360">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="c050f-360">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="c050f-361">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="c050f-361">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="c050f-362">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="c050f-362">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="c050f-363">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="c050f-363">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="c050f-364">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="c050f-364">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="c050f-365">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="c050f-365">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="c050f-366">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="c050f-366">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="c050f-367">CDN 'de Modernizr yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-367">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="c050f-368">Aşağıdaki [Modernizr](http://www.modernizr.com "Modernize") sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-368">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="c050f-369">CDN 'de Jshınt yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-369">JSHint Releases on the CDN</span></span>

<span data-ttu-id="c050f-370">Aşağıdaki [Jshınt](http://www.jshint.com "JSHint") sürümleri CDN 'de barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-370">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="c050f-371">CDN 'deki sürümleri altını gizleme</span><span class="sxs-lookup"><span data-stu-id="c050f-371">Knockout Releases on the CDN</span></span>

<span data-ttu-id="c050f-372">Aşağıdaki [altını gizleme](http://www.knockoutjs.com "Renkleri") sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-372">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="c050f-373">CDN 'de globalize sürümleri</span><span class="sxs-lookup"><span data-stu-id="c050f-373">Globalize Releases on the CDN</span></span>

<span data-ttu-id="c050f-374">Aşağıdaki [globalize](https://github.com/jquery/globalize "Globalize") sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-374">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="c050f-375">Globalize sürümü 1.0.0</span><span class="sxs-lookup"><span data-stu-id="c050f-375">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="c050f-376">Globalize sürümü 0.1.1</span><span class="sxs-lookup"><span data-stu-id="c050f-376">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="c050f-377">tüm kültürler</span><span class="sxs-lookup"><span data-stu-id="c050f-377">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="c050f-378">"{Culture-Code}" öğesini istenen kültür koduyla değiştirin, örn. globalize. Culture. en-GB. js = = Microsoft tarafından CDN = = bu kitaplıklar Microsoft tarafından karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="c050f-378">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="c050f-379">CDN 'deki yanıt verme yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-379">Respond Releases on the CDN</span></span>

<span data-ttu-id="c050f-380">Aşağıdaki [yanıt verme](https://github.com/scottjehl/Respond "Yanıtlama") sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-380">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="c050f-381">Yanıt 1.4.2 sürümü</span><span class="sxs-lookup"><span data-stu-id="c050f-381">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="c050f-382">Yanıt 1.4.1 sürümü</span><span class="sxs-lookup"><span data-stu-id="c050f-382">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="c050f-383">Yanıt 1.4.0 sürümü</span><span class="sxs-lookup"><span data-stu-id="c050f-383">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="c050f-384">Yanıt 1.3.0 sürümü</span><span class="sxs-lookup"><span data-stu-id="c050f-384">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="c050f-385">Yanıt 1.2.0 sürümü</span><span class="sxs-lookup"><span data-stu-id="c050f-385">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="c050f-386">CDN 'de önyükleme yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-386">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="c050f-387">Aşağıdaki [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") Bootstrap sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-387">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="c050f-388">Önyükleme sürümü 4.4.1</span><span class="sxs-lookup"><span data-stu-id="c050f-388">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="c050f-389">Önyükleme sürümü 4.3.1</span><span class="sxs-lookup"><span data-stu-id="c050f-389">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="c050f-390">Önyükleme sürümü 4.2.1</span><span class="sxs-lookup"><span data-stu-id="c050f-390">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="c050f-391">Önyükleme sürümü 4.1.1</span><span class="sxs-lookup"><span data-stu-id="c050f-391">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="c050f-392">Önyükleme sürümü 4.0.0</span><span class="sxs-lookup"><span data-stu-id="c050f-392">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="c050f-393">Önyükleme sürümü 3.4.1</span><span class="sxs-lookup"><span data-stu-id="c050f-393">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="c050f-394">Önyükleme sürümü 3.4.0</span><span class="sxs-lookup"><span data-stu-id="c050f-394">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="c050f-395">Önyükleme sürümü 3.3.7</span><span class="sxs-lookup"><span data-stu-id="c050f-395">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="c050f-396">Önyükleme sürümü 3.3.6</span><span class="sxs-lookup"><span data-stu-id="c050f-396">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="c050f-397">Önyükleme sürümü 3.3.5</span><span class="sxs-lookup"><span data-stu-id="c050f-397">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="c050f-398">Önyükleme sürümü 3.3.4</span><span class="sxs-lookup"><span data-stu-id="c050f-398">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="c050f-399">Önyükleme sürümü 3.3.2</span><span class="sxs-lookup"><span data-stu-id="c050f-399">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="c050f-400">Önyükleme sürümü 3.3.1</span><span class="sxs-lookup"><span data-stu-id="c050f-400">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="c050f-401">Önyükleme sürümü 3.3.0</span><span class="sxs-lookup"><span data-stu-id="c050f-401">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="c050f-402">Önyükleme sürümü 3.2.0</span><span class="sxs-lookup"><span data-stu-id="c050f-402">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="c050f-403">Önyükleme sürümü 3.1.1</span><span class="sxs-lookup"><span data-stu-id="c050f-403">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="c050f-404">Önyükleme sürümü 3.1.0</span><span class="sxs-lookup"><span data-stu-id="c050f-404">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="c050f-405">Önyükleme sürümü 3.0.3</span><span class="sxs-lookup"><span data-stu-id="c050f-405">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="c050f-406">Önyükleme sürümü 3.0.2</span><span class="sxs-lookup"><span data-stu-id="c050f-406">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="c050f-407">Önyükleme sürümü 3.0.1</span><span class="sxs-lookup"><span data-stu-id="c050f-407">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="c050f-408">Önyükleme sürümü 3.0.0</span><span class="sxs-lookup"><span data-stu-id="c050f-408">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="c050f-409">Önyükleme sürümü 2.3.2</span><span class="sxs-lookup"><span data-stu-id="c050f-409">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="c050f-410">Önyükleme sürümü 2.3.1</span><span class="sxs-lookup"><span data-stu-id="c050f-410">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="c050f-411">CDN 'de önyükleme TouchCarousel sürümleri</span><span class="sxs-lookup"><span data-stu-id="c050f-411">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="c050f-412">[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel sürümlerinin AŞAĞıDAKI sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-412">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="c050f-413">Bootstrap TouchCarousel sürümü 0.8.0</span><span class="sxs-lookup"><span data-stu-id="c050f-413">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="c050f-414">CDN 'de hakökü. js yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-414">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="c050f-415">[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") hayoz. js sürümlerinin AŞAĞıDAKI sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-415">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="c050f-416">Hayoz. js sürüm 2.0.4</span><span class="sxs-lookup"><span data-stu-id="c050f-416">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="c050f-417">CDN 'de ASP.NET Web Forms ve Ajax sürümleri</span><span class="sxs-lookup"><span data-stu-id="c050f-417">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="c050f-418">ASP.NET Ajax Kitaplığı 'nın aşağıdaki sürümleri CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c050f-418">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="c050f-419">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c050f-419">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="c050f-420">ASP.NET Web Forms ve Ajax sürümü 4.5.2</span><span class="sxs-lookup"><span data-stu-id="c050f-420">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms ve Ajax 4.5.2")
- [<span data-ttu-id="c050f-421">ASP.NET Web Forms ve Ajax sürüm 4</span><span class="sxs-lookup"><span data-stu-id="c050f-421">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms ve Ajax 4")
- [<span data-ttu-id="c050f-422">ASP.NET AJAX sürüm 3,5</span><span class="sxs-lookup"><span data-stu-id="c050f-422">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="c050f-423">CDN 'de ASP.NET MVC yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-423">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="c050f-424">Aşağıdaki ASP.NET MVC JavaScript dosyaları bu CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-424">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="c050f-425">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="c050f-425">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="c050f-426">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="c050f-426">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="c050f-427">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="c050f-427">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="c050f-428">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="c050f-428">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="c050f-429">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="c050f-429">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="c050f-430">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="c050f-430">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="c050f-431">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="c050f-431">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="c050f-432">CDN üzerinde ASP.NET SignalR yayınları</span><span class="sxs-lookup"><span data-stu-id="c050f-432">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="c050f-433">Aşağıdaki ASP.NET SignalR JavaScript dosyaları bu CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="c050f-433">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="c050f-434">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="c050f-434">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="c050f-435">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="c050f-435">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="c050f-436">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="c050f-436">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="c050f-437">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="c050f-437">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="c050f-438">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="c050f-438">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="c050f-439">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="c050f-439">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="c050f-440">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="c050f-440">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="c050f-441">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c050f-441">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="c050f-442">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="c050f-442">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="c050f-443">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="c050f-443">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="c050f-444">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="c050f-444">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="c050f-445">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="c050f-445">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="c050f-446">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="c050f-446">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="c050f-447">CDN için kullanım koşulları hakkında daha fazla bilgi için bkz. [Microsoft Ajax CDN kullanım koşulları](https://www.asp.net/terms-of-use "Microsoft Ajax CDN kullanım koşulları").</span><span class="sxs-lookup"><span data-stu-id="c050f-447">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
