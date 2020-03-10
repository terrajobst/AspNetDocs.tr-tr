---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC yönlendirmeye genel bakış (VB) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther, ASP.NET MVC çerçevesinin Tarayıcı isteklerini denetleyici eylemlerine nasıl eşlediğini gösterir.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601537"
---
# <a name="aspnet-mvc-routing-overview-vb"></a><span data-ttu-id="169d2-103">ASP.NET MVC Yönlendirmesine Genel Bakış (VB)</span><span class="sxs-lookup"><span data-stu-id="169d2-103">ASP.NET MVC Routing Overview (VB)</span></span>

<span data-ttu-id="169d2-104">ile [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="169d2-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="169d2-105">Bu öğreticide, Stephen Walther, ASP.NET MVC çerçevesinin Tarayıcı isteklerini denetleyici eylemlerine nasıl eşlediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="169d2-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>

<span data-ttu-id="169d2-106">Bu öğreticide, *ASP.net yönlendirme*adlı her ASP.NET MVC uygulamasının önemli bir özelliğine sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="169d2-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="169d2-107">ASP.NET yönlendirme modülü, gelen tarayıcı isteklerini belirli MVC denetleyici eylemlerine eşlemeden sorumludur.</span><span class="sxs-lookup"><span data-stu-id="169d2-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="169d2-108">Bu öğreticinin sonunda standart yol tablosunun istekleri denetleyici eylemlerine nasıl eşlediğini anlamış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="169d2-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="169d2-109">Varsayılan yol tablosunu kullanma</span><span class="sxs-lookup"><span data-stu-id="169d2-109">Using the Default Route Table</span></span>

<span data-ttu-id="169d2-110">Yeni bir ASP.NET MVC uygulaması oluşturduğunuzda uygulama zaten ASP.NET yönlendirme kullanmak üzere yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="169d2-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="169d2-111">ASP.NET yönlendirme iki yerde kurulumlardır.</span><span class="sxs-lookup"><span data-stu-id="169d2-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="169d2-112">İlk olarak, ASP.NET yönlendirme uygulamanızın Web yapılandırma dosyasında (Web. config dosyası) etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="169d2-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="169d2-113">Yapılandırma dosyasında yönlendirmeyle ilgili dört bölüm vardır: System. Web. httpModules bölümü, System. Web. httpHandlers bölümü, System. webserver. Modules bölümü ve System. webserver. Handlers bölümü.</span><span class="sxs-lookup"><span data-stu-id="169d2-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="169d2-114">Bu bölüm yönlendirmenin artık çalışmadığı için, bu bölümleri silmemeye dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="169d2-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="169d2-115">İkinci ve daha önemlisi, uygulamanın Global. asax dosyasında bir yol tablosu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="169d2-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="169d2-116">Global. asax dosyası, ASP.NET uygulama yaşam döngüsü olayları için olay işleyicileri içeren özel bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="169d2-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="169d2-117">Yol tablosu, uygulama başlatma olayı sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="169d2-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="169d2-118">Listeleme 1 ' deki dosya, bir ASP.NET MVC uygulaması için varsayılan Global. asax dosyasını içerir.</span><span class="sxs-lookup"><span data-stu-id="169d2-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="169d2-119">**Listeleme 1-Global. asax. vb**</span><span class="sxs-lookup"><span data-stu-id="169d2-119">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

<span data-ttu-id="169d2-120">MVC uygulaması ilk kez başlatıldığında, uygulama\_Start () yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="169d2-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="169d2-121">Bu yöntem, sırasıyla RegisterRoutes () yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="169d2-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="169d2-122">RegisterRoutes () yöntemi yol tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="169d2-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="169d2-123">Varsayılan yol tablosu, tek bir yol içerir (varsayılan olarak adlandırılır).</span><span class="sxs-lookup"><span data-stu-id="169d2-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="169d2-124">Varsayılan yol bir URL 'nin ilk segmentini bir denetleyici adına, bir URL 'nin ikinci kesimini bir denetleyici eylemine ve üçüncü segmenti **ID**adlı bir parametreye eşler.</span><span class="sxs-lookup"><span data-stu-id="169d2-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="169d2-125">Web tarayıcınızın adres çubuğuna aşağıdaki URL 'YI girdiğinizi varsayın:</span><span class="sxs-lookup"><span data-stu-id="169d2-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="169d2-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="169d2-126">/Home/Index/3</span></span>

<span data-ttu-id="169d2-127">Varsayılan yol bu URL 'YI aşağıdaki parametrelerle eşler:</span><span class="sxs-lookup"><span data-stu-id="169d2-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="169d2-128">denetleyici = ana</span><span class="sxs-lookup"><span data-stu-id="169d2-128">controller = Home</span></span>

- <span data-ttu-id="169d2-129">eylem = Dizin</span><span class="sxs-lookup"><span data-stu-id="169d2-129">action = Index</span></span>

- <span data-ttu-id="169d2-130">kimlik = 3</span><span class="sxs-lookup"><span data-stu-id="169d2-130">id = 3</span></span>

<span data-ttu-id="169d2-131">/Home/Index/3 URL 'sini istediğinizde, aşağıdaki kod yürütülür:</span><span class="sxs-lookup"><span data-stu-id="169d2-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="169d2-132">HomeController.Index(3)</span><span class="sxs-lookup"><span data-stu-id="169d2-132">HomeController.Index(3)</span></span>

<span data-ttu-id="169d2-133">Varsayılan yol, üç parametre için varsayılan değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="169d2-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="169d2-134">Bir denetleyici belirtmezseniz, denetleyici parametresi varsayılan olarak **giriş**değerini alır.</span><span class="sxs-lookup"><span data-stu-id="169d2-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="169d2-135">Bir eylem belirtmezseniz, eylem parametresi varsayılan değer **dizinine**göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="169d2-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="169d2-136">Son olarak, bir kimlik belirtmezseniz, ID parametresi varsayılan olarak boş bir dize olur.</span><span class="sxs-lookup"><span data-stu-id="169d2-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="169d2-137">Varsayılan yolun, URL 'Leri denetleyici eylemlerine nasıl eşlediğini gösteren bazı örneklere bakalım.</span><span class="sxs-lookup"><span data-stu-id="169d2-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="169d2-138">Tarayıcınızın adres çubuğuna aşağıdaki URL 'YI girdiğinizi varsayın:</span><span class="sxs-lookup"><span data-stu-id="169d2-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="169d2-139">/Home</span><span class="sxs-lookup"><span data-stu-id="169d2-139">/Home</span></span>

<span data-ttu-id="169d2-140">Varsayılan yol parametresi Varsayılanları nedeniyle, bu URL 'YI girmek, liste 2 ' deki HomeController sınıfının Index () yönteminin çağrılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="169d2-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="169d2-141">**Listeleme 2-HomeController. vb**</span><span class="sxs-lookup"><span data-stu-id="169d2-141">**Listing 2 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

<span data-ttu-id="169d2-142">Liste 2 ' de HomeController sınıfı, ID adlı tek bir parametreyi kabul eden Index () adlı bir yöntemi içerir. /Home URL 'SI, dizin () yönteminin ID parametresinin değeri olarak Nothing değeri ile çağrılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="169d2-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with the value Nothing as the value of the Id parameter.</span></span>

<span data-ttu-id="169d2-143">MVC çerçevesinin denetleyici eylemlerini çağırdığı şekilde,/Home URL 'SI, liste 3 ' teki HomeController sınıfının Index () yöntemiyle de eşleşir.</span><span class="sxs-lookup"><span data-stu-id="169d2-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="169d2-144">**Kod 3-HomeController. vb (parametre olmadan dizin eylemi)**</span><span class="sxs-lookup"><span data-stu-id="169d2-144">**Listing 3 - HomeController.vb (Index action with no parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

<span data-ttu-id="169d2-145">Listeleme 3 ' teki Index () yöntemi herhangi bir parametre kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="169d2-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="169d2-146">/Home URL 'SI, bu dizin () yönteminin çağrılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="169d2-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="169d2-147">/Home/Index/3 URL 'SI de bu yöntemi çağırır (kimlik yoksayıldı).</span><span class="sxs-lookup"><span data-stu-id="169d2-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="169d2-148">/Home URL 'SI, liste 4 ' teki HomeController sınıfının Index () yöntemiyle de eşleşir.</span><span class="sxs-lookup"><span data-stu-id="169d2-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="169d2-149">**4-HomeController. vb dosyasını (null yapılabilir parametresiyle Dizin eylemi) listeleme**</span><span class="sxs-lookup"><span data-stu-id="169d2-149">**Listing 4 - HomeController.vb (Index action with nullable parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

<span data-ttu-id="169d2-150">Liste 4 ' te, Index () yönteminde bir tamsayı parametresi vardır.</span><span class="sxs-lookup"><span data-stu-id="169d2-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="169d2-151">Parametre null yapılabilir bir parametre olduğundan (değer Nothing olabilir), dizin () bir hata oluşturulmadan çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="169d2-151">Because the parameter is a nullable parameter (can have the value Nothing), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="169d2-152">Son olarak, kod parametresi null atanabilir bir parametre *olmadığından* , ana sayfa URL 'si olan 5. liste ile dizin () yöntemini çağırmak özel duruma neden olur.</span><span class="sxs-lookup"><span data-stu-id="169d2-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="169d2-153">Index () yöntemini çağırmaya çalışırsanız Şekil 1 ' de hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="169d2-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="169d2-154">**Listeleme 5-HomeController. vb (kimlik parametresiyle Dizin eylemi)**</span><span class="sxs-lookup"><span data-stu-id="169d2-154">**Listing 5 - HomeController.vb (Index action with Id parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

<span data-ttu-id="169d2-155">[bir parametre değeri bekleyen bir denetleyici eylemini çağırma ![](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="169d2-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="169d2-156">**Şekil 01**: parametre değeri bekleyen bir denetleyici eylemi çağırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](asp-net-mvc-routing-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="169d2-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="169d2-157">Diğer yandan,/Home/Index/3 URL 'SI, kod 5 ' teki Dizin denetleyicisi eylemiyle sorunsuz bir şekilde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="169d2-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="169d2-158">/Home/Index/3 isteği, dizin () yönteminin 3 değerine sahip bir kimlik parametresiyle çağrılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="169d2-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="169d2-159">Özet</span><span class="sxs-lookup"><span data-stu-id="169d2-159">Summary</span></span>

<span data-ttu-id="169d2-160">Bu öğreticinin amacı size ASP.NET yönlendirme hakkında kısa bir giriş sunmaktır.</span><span class="sxs-lookup"><span data-stu-id="169d2-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="169d2-161">Yeni bir ASP.NET MVC uygulamasıyla aldığınız varsayılan yol tablosunu inceledik.</span><span class="sxs-lookup"><span data-stu-id="169d2-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="169d2-162">Varsayılan yolun URL 'Leri denetleyici eylemlerine nasıl eşlediğini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="169d2-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="169d2-163">[Önceki](creating-an-action-cs.md)
> [İleri](understanding-action-filters-vb.md)</span><span class="sxs-lookup"><span data-stu-id="169d2-163">[Previous](creating-an-action-cs.md)
[Next](understanding-action-filters-vb.md)</span></span>
