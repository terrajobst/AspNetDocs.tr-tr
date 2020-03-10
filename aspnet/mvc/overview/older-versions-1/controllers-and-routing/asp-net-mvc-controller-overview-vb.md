---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC denetleyicisine genel bakış (VB) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther sizi ASP.NET MVC denetleyicilerini tanıtır. Yeni denetleyiciler oluşturmayı ve farklı eylem türlerini geri döndürmeyi öğrenirsiniz...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601565"
---
# <a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="63887-104">ASP.NET MVC Denetleyicisine Genel Bakış (VB)</span><span class="sxs-lookup"><span data-stu-id="63887-104">ASP.NET MVC Controller Overview (VB)</span></span>

<span data-ttu-id="63887-105">ile [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="63887-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="63887-106">Bu öğreticide, Stephen Walther sizi ASP.NET MVC denetleyicilerini tanıtır.</span><span class="sxs-lookup"><span data-stu-id="63887-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="63887-107">Yeni denetleyiciler oluşturmayı ve farklı türlerde eylem sonuçları döndürmeyi öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63887-107">You learn how to create new controllers and return different types of action results.</span></span>

<span data-ttu-id="63887-108">Bu öğretici, ASP.NET MVC denetleyicileri, denetleyici eylemleri ve eylem sonuçlarının konusunu araştırır.</span><span class="sxs-lookup"><span data-stu-id="63887-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="63887-109">Bu Öğreticiyi tamamladıktan sonra, bir ziyaretçinin bir ASP.NET MVC web sitesiyle etkileşim kurma şeklini denetlemek için denetleyicilerin nasıl kullanıldığını anlamış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="63887-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="63887-110">Denetleyicileri anlama</span><span class="sxs-lookup"><span data-stu-id="63887-110">Understanding Controllers</span></span>

<span data-ttu-id="63887-111">MVC denetleyicileri bir ASP.NET MVC web sitesinde yapılan isteklere yanıt vermekten sorumludur.</span><span class="sxs-lookup"><span data-stu-id="63887-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="63887-112">Her tarayıcı isteği belirli bir denetleyiciye eşlenir.</span><span class="sxs-lookup"><span data-stu-id="63887-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="63887-113">Örneğin, tarayıcınızın adres çubuğuna aşağıdaki URL 'YI girdiğinizi varsayın:</span><span class="sxs-lookup"><span data-stu-id="63887-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="63887-114">Bu durumda, ProductController adlı bir denetleyici çağrılır.</span><span class="sxs-lookup"><span data-stu-id="63887-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="63887-115">ProductController, tarayıcı isteğine yanıt oluşturmaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="63887-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="63887-116">Örneğin, denetleyici tarayıcıya geri döndürülen belirli bir görünümü döndürebilir veya denetleyici kullanıcıyı başka bir denetleyiciye yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="63887-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="63887-117">Listeleme 1, ProductController adlı basit bir denetleyici içerir.</span><span class="sxs-lookup"><span data-stu-id="63887-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="63887-118">**Listing1-Controllers\productcontroller.exe**</span><span class="sxs-lookup"><span data-stu-id="63887-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="63887-119">Liste 1 ' den görebileceğiniz gibi, bir denetleyici yalnızca bir sınıf (Visual Basic .NET veya C# sınıf) olur.</span><span class="sxs-lookup"><span data-stu-id="63887-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="63887-120">Denetleyici, temel System. Web. Mvc. Controller sınıfından türetilen bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="63887-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="63887-121">Bir denetleyici bu temel sınıftan devraldığı için, denetleyici birkaç yararlı yöntemi ücretsiz olarak devralır (Bu yöntemleri bir süre içinde tartıştık).</span><span class="sxs-lookup"><span data-stu-id="63887-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="63887-122">Denetleyici eylemlerini anlama</span><span class="sxs-lookup"><span data-stu-id="63887-122">Understanding Controller Actions</span></span>

<span data-ttu-id="63887-123">Denetleyici, denetleyici eylemlerini kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="63887-123">A controller exposes controller actions.</span></span> <span data-ttu-id="63887-124">Eylem, tarayıcı adres çubuğuna belirli bir URL girerken çağrılan bir denetleyicide bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="63887-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="63887-125">Örneğin, aşağıdaki URL için bir istek oluşturduğunuzu düşünün:</span><span class="sxs-lookup"><span data-stu-id="63887-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="63887-126">Bu durumda, Index () yöntemi ProductController sınıfında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="63887-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="63887-127">Index () yöntemi, bir denetleyici eyleminin bir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="63887-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="63887-128">Denetleyici eyleminin bir denetleyici sınıfının ortak bir yöntemi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="63887-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="63887-129">Visual Basic.NET yöntemleri, varsayılan olarak ortak yöntemlerdir.</span><span class="sxs-lookup"><span data-stu-id="63887-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="63887-130">Bir denetleyici sınıfına eklediğiniz herhangi bir genel yöntemin otomatik olarak bir denetleyici eylemi olarak sunulduğunu unutmayın (bir denetleyici eylemi, bir tarayıcı adres çubuğuna doğru URL 'yi yazarak, Universe ' deki herkes tarafından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="63887-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="63887-131">Bir denetleyici eylemi tarafından karşılanması gereken bazı ek gereksinimler vardır.</span><span class="sxs-lookup"><span data-stu-id="63887-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="63887-132">Denetleyici eylemi olarak kullanılan bir yöntem aşırı yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="63887-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="63887-133">Ayrıca, bir denetleyici eylemi statik bir yöntem olamaz.</span><span class="sxs-lookup"><span data-stu-id="63887-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="63887-134">Bundan farklı olarak, yalnızca bir denetleyici eylemi olarak istediğiniz yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63887-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="63887-135">Eylem sonuçlarını anlama</span><span class="sxs-lookup"><span data-stu-id="63887-135">Understanding Action Results</span></span>

<span data-ttu-id="63887-136">Bir denetleyici eylemi, *eylem sonucu*olarak adlandırılan bir şeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="63887-137">Bir eylem sonucu, bir tarayıcı isteğine yanıt olarak bir denetleyici eyleminin döndürdüğü şeydir.</span><span class="sxs-lookup"><span data-stu-id="63887-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="63887-138">ASP.NET MVC çerçevesi aşağıdakiler dahil olmak üzere birkaç tür eylem sonucunu destekler:</span><span class="sxs-lookup"><span data-stu-id="63887-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="63887-139">ViewResult-HTML ve biçimlendirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63887-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="63887-140">EmptyResult-sonuç olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="63887-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="63887-141">RedirectResult-yeni bir URL 'ye yeniden yönlendirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63887-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="63887-142">JsonResult-bir AJAX uygulamasında kullanılabilecek JavaScript Nesne Gösterimi sonucunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63887-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="63887-143">JavaScriptResult-bir JavaScript betiğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63887-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="63887-144">ContentResult-bir metin sonucunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63887-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="63887-145">FileContentResult-indirilebilir bir dosyayı temsil eder (ikili içerikle birlikte).</span><span class="sxs-lookup"><span data-stu-id="63887-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="63887-146">FilePathResult-indirilebilir bir dosyayı (bir yol ile) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63887-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="63887-147">FileStreamResult-indirilebilir bir dosyayı (dosya akışı ile) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63887-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="63887-148">Bu eylem sonuçlarının hepsi temel ActionResult sınıfından devralınır.</span><span class="sxs-lookup"><span data-stu-id="63887-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="63887-149">Çoğu durumda, bir denetleyici eylemi bir ViewResult döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="63887-150">Örneğin, liste 2 ' deki Dizin denetleyicisi eyleminde bir ViewResult döndürülür.</span><span class="sxs-lookup"><span data-stu-id="63887-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="63887-151">**Listeleme 2-Controllers\bookcontroller.exe**</span><span class="sxs-lookup"><span data-stu-id="63887-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="63887-152">Bir eylem bir ViewResult döndürdüğünde, HTML tarayıcıya döndürülür.</span><span class="sxs-lookup"><span data-stu-id="63887-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="63887-153">Liste 2 ' deki Index () yöntemi, tarayıcıya dizin adlı bir görünüm döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="63887-154">Liste 2 ' deki Index () eyleminin ViewResult () döndürmediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="63887-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="63887-155">Bunun yerine, denetleyici temel sınıfının View () yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="63887-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="63887-156">Normalde, bir eylem sonucunu doğrudan döndürmeyin.</span><span class="sxs-lookup"><span data-stu-id="63887-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="63887-157">Bunun yerine, Controller temel sınıfının aşağıdaki yöntemlerinden birini çağırın:</span><span class="sxs-lookup"><span data-stu-id="63887-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="63887-158">Görüntüle-ViewResult eylem sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="63887-159">Yeniden yönlendir-bir RedirectResult eylem sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="63887-160">RedirectToAction-RedirectToRouteResult eylem sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="63887-161">RedirectToRoute-RedirectToRouteResult eylem sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="63887-162">JSON-bir JsonResult eylem sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="63887-163">JavaScriptResult-bir JavaScriptResult döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="63887-164">İçerik-bir ContentResult eylem sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="63887-165">Dosya-metoda geçirilen parametrelere bağlı olarak bir FileContentResult, FilePathResult veya FileStreamResult döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="63887-166">Bu nedenle, tarayıcıya bir görünüm döndürmek istiyorsanız, View () yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="63887-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="63887-167">Kullanıcıyı bir denetleyici eyleminden diğerine yönlendirmek istiyorsanız RedirectToAction () yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="63887-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="63887-168">Örneğin, liste 3 ' teki ayrıntılar () eylemi, kimlik parametresinin bir değere sahip olup olmadığına bağlı olarak bir görünüm görüntüler veya kullanıcıyı dizin () eylemine yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="63887-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="63887-169">**Listeleme 3-CustomerController. vb**</span><span class="sxs-lookup"><span data-stu-id="63887-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="63887-170">ContentResult eylem sonucu özeldir.</span><span class="sxs-lookup"><span data-stu-id="63887-170">The ContentResult action result is special.</span></span> <span data-ttu-id="63887-171">Bir eylem sonucunu düz metin olarak döndürmek için ContentResult eylem sonucunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63887-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="63887-172">Örneğin, liste 4 ' teki Index () yöntemi bir iletiyi düz metin olarak HTML olarak değil bir ileti döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="63887-173">**Listeleme 4-Controllers\statuscontroller.exe**</span><span class="sxs-lookup"><span data-stu-id="63887-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="63887-174">StatusController</span><span class="sxs-lookup"><span data-stu-id="63887-174">StatusController</span></span>
> 
> 
> <span data-ttu-id="63887-175">System. Web. Mvc. Controller</span><span class="sxs-lookup"><span data-stu-id="63887-175">System.Web.Mvc.Controller</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="63887-176">StatusController. Index () eylemi çağrıldığında bir görünüm döndürülmez.</span><span class="sxs-lookup"><span data-stu-id="63887-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="63887-177">Bunun yerine, "Merhaba Dünya!" RAW metni</span><span class="sxs-lookup"><span data-stu-id="63887-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="63887-178">tarayıcıya döndürülür.</span><span class="sxs-lookup"><span data-stu-id="63887-178">is returned to the browser.</span></span>

<span data-ttu-id="63887-179">Bir denetleyici eylemi bir eylem sonucu olmayan bir sonuç döndürürse (örneğin, bir tarih veya tamsayı), sonuç otomatik olarak bir ContentResult öğesine kaydırılır.</span><span class="sxs-lookup"><span data-stu-id="63887-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="63887-180">Örneğin, Listeleme 5 ' teki WorkController dizini () eylemi çağrıldığında, tarih otomatik olarak bir ContentResult olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="63887-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="63887-181">**Listeleme 5-WorkController. vb**</span><span class="sxs-lookup"><span data-stu-id="63887-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="63887-182">Listeleme 5 ' teki Index () eylemi bir DateTime nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="63887-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="63887-183">ASP.NET MVC Framework, DateTime nesnesini bir dizeye dönüştürür ve bir ContentResult içindeki DateTime değerini otomatik olarak kaydırır.</span><span class="sxs-lookup"><span data-stu-id="63887-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="63887-184">Tarayıcı Tarih ve saati düz metin olarak alır.</span><span class="sxs-lookup"><span data-stu-id="63887-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="63887-185">Özet</span><span class="sxs-lookup"><span data-stu-id="63887-185">Summary</span></span>

<span data-ttu-id="63887-186">Bu öğreticinin amacı, sizi ASP.NET MVC denetleyicileri, denetleyici eylemleri ve denetleyici eylem sonuçlarının kavramlarını tanıtmaktadır.</span><span class="sxs-lookup"><span data-stu-id="63887-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="63887-187">İlk bölümde, bir ASP.NET MVC projesine yeni denetleyiciler eklemeyi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="63887-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="63887-188">Daha sonra, bir denetleyicinin genel yöntemlerinin Universe as Controller eylemlerine nasıl sunuleceğini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="63887-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="63887-189">Son olarak, bir denetleyici eyleminden döndürülebilecek farklı eylem sonuçları türlerini tartıştık.</span><span class="sxs-lookup"><span data-stu-id="63887-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="63887-190">Özellikle, bir denetleyici eyleminden bir ViewResult, RedirectToActionResult ve ContentResult döndürme hakkında anlatıldık.</span><span class="sxs-lookup"><span data-stu-id="63887-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="63887-191">[Önceki](creating-a-custom-route-constraint-cs.md)
> [İleri](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="63887-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
