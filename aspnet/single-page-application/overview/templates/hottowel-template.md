---
uid: single-page-application/overview/templates/hottowel-template
title: Etkin şablon | Microsoft Docs
author: madskristensen
description: Hottohavtemplate
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075066"
---
# <a name="hot-towel-template"></a><span data-ttu-id="9d7ac-103">Hot Towel şablonu</span><span class="sxs-lookup"><span data-stu-id="9d7ac-103">Hot Towel template</span></span>

<span data-ttu-id="9d7ac-104">[Mads Kristensen](https://github.com/madskristensen) tarafından</span><span class="sxs-lookup"><span data-stu-id="9d7ac-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="9d7ac-105">Etkin yazı MVC şablonu John Papa tarafından yazılmıştır</span><span class="sxs-lookup"><span data-stu-id="9d7ac-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="9d7ac-106">Hangi sürümün indirileceği seçin:</span><span class="sxs-lookup"><span data-stu-id="9d7ac-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="9d7ac-107">Visual Studio 2012 için sık erişimli MVC şablonu</span><span class="sxs-lookup"><span data-stu-id="9d7ac-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="9d7ac-108">Visual Studio 2013 için sık erişimli MVC şablonu</span><span class="sxs-lookup"><span data-stu-id="9d7ac-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="9d7ac-109">Etkin kısayol: yalnızca bir tane olmadan SPA 'ya gitmek istemezsiniz!</span><span class="sxs-lookup"><span data-stu-id="9d7ac-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>

<span data-ttu-id="9d7ac-110">SPA oluşturmak istiyor ancak nereden başlayacağınıza karar veremiyorum mi?</span><span class="sxs-lookup"><span data-stu-id="9d7ac-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="9d7ac-111">Etkin kısayol kullanın ve saniyeler içinde oluşturmanız gereken bir SPA ve tüm araçlara sahip olacaksınız!</span><span class="sxs-lookup"><span data-stu-id="9d7ac-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="9d7ac-112">Sık erişimli, ASP.NET ile tek sayfalı uygulama (SPA) oluşturmak için harika bir başlangıç noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="9d7ac-113">Seçtiğiniz kutudan biri, kodunuz için modüler bir yapı, gezinti, veri bağlama, zengin veri yönetimi ve basit ancak zarif stillendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="9d7ac-114">Sıcak şey, SPA 'yı oluşturmak için ihtiyacınız olan her şeyi sağlar. böylece, devam etmenize değil uygulamanıza odaklanırsınız.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="9d7ac-115">[John Papa 'nin videolarının videoları, öğreticiler ve Plurun kursu](http://johnpapa.net/spa?vsix)hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>

## <a name="application-structure"></a><span data-ttu-id="9d7ac-116">Uygulama yapısı</span><span class="sxs-lookup"><span data-stu-id="9d7ac-116">Application Structure</span></span>

<span data-ttu-id="9d7ac-117">Sık erişimli SPA, uygulamanızı tanımlayan JavaScript ve HTML dosyalarını içeren bir uygulama klasörü sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="9d7ac-118">Uygulama klasörü içinde:</span><span class="sxs-lookup"><span data-stu-id="9d7ac-118">Inside the App folder:</span></span>

- <span data-ttu-id="9d7ac-119">Durandal</span><span class="sxs-lookup"><span data-stu-id="9d7ac-119">durandal</span></span>
- <span data-ttu-id="9d7ac-120">hizmetler</span><span class="sxs-lookup"><span data-stu-id="9d7ac-120">services</span></span>
- <span data-ttu-id="9d7ac-121">ViewModel 'lar</span><span class="sxs-lookup"><span data-stu-id="9d7ac-121">viewmodels</span></span>
- <span data-ttu-id="9d7ac-122">görünümler</span><span class="sxs-lookup"><span data-stu-id="9d7ac-122">views</span></span>

<span data-ttu-id="9d7ac-123">Uygulama klasörü bir modül koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="9d7ac-124">Bu modüller işlevleri kapsüller ve diğer modüller üzerinde bağımlılıklar bildirir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="9d7ac-125">Görünümler klasörü, uygulamanız için HTML içerir ve viewmodeller klasörü, görünümler (ortak bir MVVM modeli) için sunum mantığını içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="9d7ac-126">Hizmetler klasörü, uygulamanızın HTTP veri alımı veya yerel depolama etkileşimi gibi ihtiyaç duyduğu tüm ortak hizmetleri muhafazası için idealdir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="9d7ac-127">Hizmet modüllerindeki kodu yeniden kullanmak için birden çok ViewModel kullanılması yaygındır.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="9d7ac-128">ASP.NET MVC sunucu tarafı uygulama yapısı</span><span class="sxs-lookup"><span data-stu-id="9d7ac-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="9d7ac-129">Bilinen ve güçlü ASP.NET MVC yapısında sık erişimli yapılar.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="9d7ac-130">Uygulama\_başlangıç</span><span class="sxs-lookup"><span data-stu-id="9d7ac-130">App\_Start</span></span>
- <span data-ttu-id="9d7ac-131">İçerik</span><span class="sxs-lookup"><span data-stu-id="9d7ac-131">Content</span></span>
- <span data-ttu-id="9d7ac-132">Denetleyiciler</span><span class="sxs-lookup"><span data-stu-id="9d7ac-132">Controllers</span></span>
- <span data-ttu-id="9d7ac-133">Modeller</span><span class="sxs-lookup"><span data-stu-id="9d7ac-133">Models</span></span>
- <span data-ttu-id="9d7ac-134">Komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="9d7ac-134">Scripts</span></span>
- <span data-ttu-id="9d7ac-135">Görünümler</span><span class="sxs-lookup"><span data-stu-id="9d7ac-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="9d7ac-136">Öne çıkan kitaplıklar</span><span class="sxs-lookup"><span data-stu-id="9d7ac-136">Featured Libraries</span></span>

- <span data-ttu-id="9d7ac-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="9d7ac-137">ASP.NET MVC</span></span>
- <span data-ttu-id="9d7ac-138">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="9d7ac-138">ASP.NET Web API</span></span>
- <span data-ttu-id="9d7ac-139">ASP.NET Web Iyileştirmesi-paketleme ve minbirleşme</span><span class="sxs-lookup"><span data-stu-id="9d7ac-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="9d7ac-140">[Breeze. js](http://Breezejs.com) -zengin veri yönetimi</span><span class="sxs-lookup"><span data-stu-id="9d7ac-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="9d7ac-141">[Durandal. js](http://Durandaljs.com) -gezinti ve görünüm bileşimi</span><span class="sxs-lookup"><span data-stu-id="9d7ac-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="9d7ac-142">[Altını gizleme. js](http://Knockoutjs.com) -veri bağlamaları</span><span class="sxs-lookup"><span data-stu-id="9d7ac-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="9d7ac-143">AMD ve iyileştirme ile [. js](http://requirejs.org) -modülerlik gerektir</span><span class="sxs-lookup"><span data-stu-id="9d7ac-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="9d7ac-144">[Toastr. js](http://jpapa.me/c7toastr) -açılan iletiler</span><span class="sxs-lookup"><span data-stu-id="9d7ac-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="9d7ac-145">[Twitter önyüklemesi](https://twitter.github.com/bootstrap/) -sağlam CSS stili</span><span class="sxs-lookup"><span data-stu-id="9d7ac-145">[Twitter Bootstrap](https://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="9d7ac-146">Visual Studio 2012 Hot Toceksel SPA şablonu aracılığıyla yükleme</span><span class="sxs-lookup"><span data-stu-id="9d7ac-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="9d7ac-147">Etkin kısayol, Visual Studio 2012 şablonu olarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="9d7ac-148">`File` | `New Project` ' ne tıklayıp `ASP.NET MVC 4 Web Application`' i seçmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="9d7ac-149">Sonra ' etkin olan tek sayfalı uygulama "şablonunu seçin ve çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="9d7ac-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="9d7ac-150">NuGet paketi aracılığıyla yükleme</span><span class="sxs-lookup"><span data-stu-id="9d7ac-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="9d7ac-151">Sık erişimli, var olan bir boş ASP.NET MVC projesini genişlettiğini de bir NuGet paketidir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="9d7ac-152">Yalnızca NuGet kullanarak yükleyip çalıştırmanız yeterlidir!</span><span class="sxs-lookup"><span data-stu-id="9d7ac-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="9d7ac-153">Etkin bir yerde nasıl oluşturabilirim?</span><span class="sxs-lookup"><span data-stu-id="9d7ac-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="9d7ac-154">Kod eklemeye başlamanız yeterlidir!</span><span class="sxs-lookup"><span data-stu-id="9d7ac-154">Simply start adding code!</span></span>

1. <span data-ttu-id="9d7ac-155">Kendi sunucu tarafı kodunuzu ekleyin, tercihen Entity Framework ve WebAPI (Breeze. js ile gerçekten uyumlu)</span><span class="sxs-lookup"><span data-stu-id="9d7ac-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="9d7ac-156">`App/views` klasöre görünümler ekleme</span><span class="sxs-lookup"><span data-stu-id="9d7ac-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="9d7ac-157">`App/viewmodels` klasöre viewmodeller ekleme</span><span class="sxs-lookup"><span data-stu-id="9d7ac-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="9d7ac-158">Yeni Görünümleriniz için HTML ve altını gizleme veri bağlamaları ekleme</span><span class="sxs-lookup"><span data-stu-id="9d7ac-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="9d7ac-159">`shell.js` gezinti rotalarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9d7ac-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="9d7ac-160">HTML/JavaScript için İzlenecek yol</span><span class="sxs-lookup"><span data-stu-id="9d7ac-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="9d7ac-161">Görünümler/Hottohava/index. cshtml</span><span class="sxs-lookup"><span data-stu-id="9d7ac-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="9d7ac-162">Index. cshtml, MVC uygulaması için başlangıç rotası ve görünümüdür.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="9d7ac-163">Bu, bekleeceğiniz tüm standart meta etiketlerini, CSS bağlantılarını ve JavaScript başvurularını içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="9d7ac-164">Gövde, istendiklerinde tüm içeriğin (görünümlerinizin) yerleştirileceği tek bir `<div>` içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="9d7ac-165">`@Scripts.Render`, uygulama kodunun giriş noktasını çalıştırmak için, `main.js` dosyasında bulunan. js ' yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="9d7ac-166">Uygulamanız yüklenirken giriş ekranı oluşturmayı göstermek için bir giriş ekranı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="9d7ac-167">App/Main. js</span><span class="sxs-lookup"><span data-stu-id="9d7ac-167">App/main.js</span></span>

<span data-ttu-id="9d7ac-168">`main.js` dosyası, uygulamanız yüklendikten hemen sonra çalıştırılacak kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="9d7ac-169">Bu, gezinti rotalarınızı tanımlamak, başlangıç görünümlerinizi ayarlamak ve uygulamanızın verilerini eklemek gibi Kurulum/önyükleme işlemleri gerçekleştirmek istediğiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="9d7ac-170">`main.js` dosyası, uygulamanın başlamasını sağlamak için birkaç Durandal modülünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="9d7ac-171">Define deyimleri, işlev için kullanılabilir olmaları için modüller bağımlılıklarını çözmeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="9d7ac-172">İlk olarak hata ayıklama iletileri etkinleştirilir ve bu, uygulamanın konsol penceresinde gerçekleştirdiği olaylar hakkında iletiler gönderir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="9d7ac-173">App. Start kodu, uygulamayı başlatmak için Durandal çerçevesine bildirir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="9d7ac-174">Bu kurallar, Durandal 'ın tüm görünümleri ve viewmodellerinin sırasıyla aynı adlı klasörlerde yer aldığı şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="9d7ac-175">Son olarak, `app.setRoot` KIKS, önceden tanımlanmış bir `entrance` animasyonunu kullanarak `shell` yükler.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="9d7ac-176">Görünümler</span><span class="sxs-lookup"><span data-stu-id="9d7ac-176">Views</span></span>

<span data-ttu-id="9d7ac-177">Görünümler `App/views` klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="9d7ac-178">Shell. html</span><span class="sxs-lookup"><span data-stu-id="9d7ac-178">shell.html</span></span>

<span data-ttu-id="9d7ac-179">`shell.html`, HTML 'nizin ana yerleşimini içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="9d7ac-180">Diğer görünümleriniz `shell` görünümlerinizin yanında bir yerde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="9d7ac-181">Sık kullanılan: bir başlık, içerik alanı ve bir altbilgi olmak üzere üç bölge içeren bir `shell` sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="9d7ac-182">Bu bölgelerin her biri, istendiğinde diğer görünümlerle birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="9d7ac-183">Üst bilgi ve alt bilgi için `compose` bağlamaları, sırasıyla `nav` ve `footer` görünümlerine işaret etmek üzere sık erişimli olarak sabit kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="9d7ac-184">`#content` bölüm için oluşturma bağlaması `router` modülünün etkin öğesine bağlanır.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="9d7ac-185">Diğer bir deyişle, bir gezinti bağlantısına tıkladığınızda bu alana karşılık gelen görünüm yüklenir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="9d7ac-186">NAV. html</span><span class="sxs-lookup"><span data-stu-id="9d7ac-186">nav.html</span></span>

<span data-ttu-id="9d7ac-187">`nav.html` SPA 'nın gezinti bağlantılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="9d7ac-188">Bu, örneğin, menü yapısının yerleştirilebileceği yerdir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="9d7ac-189">Bu, genellikle `shell.js`tanımladığınız gezintiyi göstermek için `router` modülüne veri bağımlıdır (altını gizleme kullanılarak).</span><span class="sxs-lookup"><span data-stu-id="9d7ac-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="9d7ac-190">Altını gizleme, veri bağlama özniteliklerini gösterir ve `shell` ViewModel 'e bağlar ve `router` modülü bir görünümden diğerine gezinmesinin ortasındaysa bir ProgressBar (Twitter önyüklemesi kullanarak) görüntülenir (bkz. `router.isNavigating`).</span><span class="sxs-lookup"><span data-stu-id="9d7ac-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="9d7ac-191">Home. html ve details. html</span><span class="sxs-lookup"><span data-stu-id="9d7ac-191">home.html and details.html</span></span>

<span data-ttu-id="9d7ac-192">Bu görünümler özel görünümler için HTML içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="9d7ac-193">`nav` görünümü menüsündeki `home` bağlantısına tıklandığında, `home` görünümü `shell` görünümünün içerik alanına yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="9d7ac-194">Bu görünümler, kendi özel görünümleriniz ile genişletilebilir veya değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="9d7ac-195">footer. html</span><span class="sxs-lookup"><span data-stu-id="9d7ac-195">footer.html</span></span>

<span data-ttu-id="9d7ac-196">`footer.html`, `shell` görünümünün altındaki altbilgide görüntülenen HTML içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="9d7ac-197">ViewModel 'lar</span><span class="sxs-lookup"><span data-stu-id="9d7ac-197">ViewModels</span></span>

<span data-ttu-id="9d7ac-198">Viewmodeller `App/viewmodels` klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="9d7ac-199">Shell. js</span><span class="sxs-lookup"><span data-stu-id="9d7ac-199">shell.js</span></span>

<span data-ttu-id="9d7ac-200">`shell` ViewModel `shell` görünümüne bağlanan özellikleri ve işlevleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="9d7ac-201">Genellikle bu, menü gezintisi bağlamalarının bulunduğu yerdir (bkz. `router.mapNav` Logic).</span><span class="sxs-lookup"><span data-stu-id="9d7ac-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="9d7ac-202">Home. js ve details. js</span><span class="sxs-lookup"><span data-stu-id="9d7ac-202">home.js and details.js</span></span>

<span data-ttu-id="9d7ac-203">Bu viewmodeller `home` görünümüne bağlanan özellikleri ve işlevleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="9d7ac-204">Ayrıca, görünüm için sunum mantığını içerir ve veriler ile görünüm arasında yapıştırıcı olur.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="9d7ac-205">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="9d7ac-205">Services</span></span>

<span data-ttu-id="9d7ac-206">Hizmetler App/Services klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="9d7ac-207">İdeal olarak, uzak verileri alma ve göndermekten sorumlu olan bir veri hizmeti modülü gibi gelecekteki hizmetlerinizin yerleştirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="9d7ac-208">günlükçü. js</span><span class="sxs-lookup"><span data-stu-id="9d7ac-208">logger.js</span></span>

<span data-ttu-id="9d7ac-209">Sık erişimli, Hizmetler klasöründe bir `logger` modülü sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="9d7ac-210">`logger` modülü, iletileri konsola ve açılan menüden kullanıcıya günlüğe kaydetmek için idealdir.</span><span class="sxs-lookup"><span data-stu-id="9d7ac-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
