---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC yürütme Işlemini anlama | Microsoft Docs
author: microsoft
description: ASP.NET MVC çerçevesinin bir tarayıcı isteği adım adım nasıl işlem kullandığını öğrenin.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541519"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="de316-103">ASP.NET MVC Yürütme İşlemini Anlama</span><span class="sxs-lookup"><span data-stu-id="de316-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="de316-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="de316-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="de316-105">ASP.NET MVC çerçevesinin bir tarayıcı isteği adım adım nasıl işlem kullandığını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="de316-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="de316-106">ASP.NET MVC tabanlı bir Web uygulamasına yönelik istekler, ilk olarak HTTP modülü olan **UrlRoutingModule** nesnesinden geçer.</span><span class="sxs-lookup"><span data-stu-id="de316-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="de316-107">Bu modül, isteği ayrıştırır ve yol seçimini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="de316-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="de316-108">**UrlRoutingModule** nesnesi, geçerli istekle eşleşen ilk yol nesnesini seçer.</span><span class="sxs-lookup"><span data-stu-id="de316-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="de316-109">(Yol nesnesi, **RouteBase**uygulayan bir sınıftır ve genellikle **yol** sınıfının bir örneğidir.) Hiçbir yol eşleşmezse, **UrlRoutingModule** nesnesi hiçbir şey yapmaz ve isteğin normal ASP.NET veya IIS istek işlemeye geri dönmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="de316-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="de316-110">Seçili **yol** nesnesinden **UrlRoutingModule** nesnesi, **yol** nesnesiyle ilişkili **IRouteHandler** nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="de316-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="de316-111">Genellikle, bir MVC uygulamasında bu bir **MvcRouteHandler**örneği olacaktır.</span><span class="sxs-lookup"><span data-stu-id="de316-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="de316-112">**IRouteHandler** örneği bir **IHttpHandler** nesnesi oluşturur ve onu **IHttpContext** nesnesine geçirir.</span><span class="sxs-lookup"><span data-stu-id="de316-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="de316-113">Varsayılan olarak, MVC için **IHttpHandler** örneği **MvcHandler** nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="de316-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="de316-114">**MvcHandler** nesnesi daha sonra isteği işleyecek olan denetleyiciyi seçer.</span><span class="sxs-lookup"><span data-stu-id="de316-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="de316-115">ASP.NET MVC web uygulaması IIS 7,0 ' de çalıştığında, MVC projeleri için dosya adı uzantısı gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="de316-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="de316-116">Ancak, IIS 6,0 ' de, işleyici. Mvc dosya adı uzantısını ASP.NET ISAPI DLL 'SI ile eşlemenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="de316-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="de316-117">Modül ve işleyici, ASP.NET MVC çerçevesinin giriş noktalarıdır.</span><span class="sxs-lookup"><span data-stu-id="de316-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="de316-118">Aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="de316-118">They perform the following actions:</span></span>

- <span data-ttu-id="de316-119">MVC web uygulamasında uygun denetleyiciyi seçin.</span><span class="sxs-lookup"><span data-stu-id="de316-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="de316-120">Belirli bir denetleyici örneği edinin.</span><span class="sxs-lookup"><span data-stu-id="de316-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="de316-121">Denetleyicinin **Execute** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="de316-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="de316-122">Aşağıda bir MVC web projesi yürütme aşamaları listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="de316-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="de316-123">Uygulama için ilk isteği al</span><span class="sxs-lookup"><span data-stu-id="de316-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="de316-124">Global. asax dosyasında, **route** nesneleri **RouteTable** nesnesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="de316-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="de316-125">Yönlendirme gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="de316-125">Perform routing</span></span> 

    - <span data-ttu-id="de316-126">**UrlRoutingModule** modülü, daha sonra bir **RequestContext** (**IHttpContext**) nesnesi oluşturmak için kullanılan **RouteData** nesnesini oluşturmak için **RouteTable** koleksiyonundaki ilk eşleşen **yol** nesnesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="de316-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="de316-127">MVC istek işleyicisi oluştur</span><span class="sxs-lookup"><span data-stu-id="de316-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="de316-128">**MvcRouteHandler** nesnesi, **MvcHandler** sınıfının bir örneğini oluşturur ve onu **RequestContext** örneğine geçirir.</span><span class="sxs-lookup"><span data-stu-id="de316-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="de316-129">Denetleyici oluştur</span><span class="sxs-lookup"><span data-stu-id="de316-129">Create controller</span></span> 

    - <span data-ttu-id="de316-130">**MvcHandler** nesnesi, ile denetleyici örneğini oluşturmak Için **IControllerFactory** nesnesini (genellikle **DefaultControllerFactory** sınıfının bir örneği) tanımlamak üzere **RequestContext** örneğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="de316-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="de316-131">Denetleyiciyi yürütme- **MvcHandler** örneği Controller for **Execute** metodunu çağırır.</span><span class="sxs-lookup"><span data-stu-id="de316-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="de316-132">Eylemi çağır</span><span class="sxs-lookup"><span data-stu-id="de316-132">Invoke action</span></span> 

    - <span data-ttu-id="de316-133">Çoğu denetleyici **Controller** temel sınıfından devralınır.</span><span class="sxs-lookup"><span data-stu-id="de316-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="de316-134">Bunu yapan denetleyiciler için, denetleyici ile ilişkili olan **ControllerActionInvoker** nesnesi, denetleyici sınıfının hangi eylem yöntemini çağırılacağını belirler ve ardından bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="de316-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="de316-135">Sonucu Yürüt</span><span class="sxs-lookup"><span data-stu-id="de316-135">Execute result</span></span> 

    - <span data-ttu-id="de316-136">Tipik bir eylem yöntemi kullanıcı girişi alabilir, uygun yanıt verilerini hazırlayabilir ve sonuç türünü döndürerek sonucu yürütebilir.</span><span class="sxs-lookup"><span data-stu-id="de316-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="de316-137">Yürütülemeyen yerleşik sonuç türleri şunlardır: **ViewResult** (bir görünüm oluşturur ve en sık kullanılan sonuç türü olan), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**ve **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="de316-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
