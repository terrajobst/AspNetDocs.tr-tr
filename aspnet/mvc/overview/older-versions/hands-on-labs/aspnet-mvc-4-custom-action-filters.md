---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 özel eylem filtreleri | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC, bir eylem yöntemi çağrılmadan önce veya sonra filtreleme mantığını yürütmek için eylem filtreleri sağlar. Eylem filtreleri özel öznitelikler Tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579697"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="0e5f5-104">ASP.NET MVC 4 Özel Eylem Filtreleri</span><span class="sxs-lookup"><span data-stu-id="0e5f5-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="0e5f5-105">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="0e5f5-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="0e5f5-106">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="0e5f5-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="0e5f5-107">ASP.NET MVC, bir eylem yöntemi çağrılmadan önce veya sonra filtreleme mantığını yürütmek için eylem filtreleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="0e5f5-108">Eylem filtreleri, denetleyicinin eylem yöntemlerine eylem öncesi ve eylem sonrası davranışı eklemek için bildirim sağlayan özel özniteliklerdir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="0e5f5-109">Bu uygulamalı laboratuvarda, yük denetleyicisi isteklerini yakalamak ve bir sitenin etkinliğini bir veritabanı tablosuna kaydetmek için MvcMusicStore çözümüne özel bir eylem filtresi özniteliği oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="0e5f5-110">Herhangi bir denetleyiciye veya eyleme ekleyerek günlüğe kaydetme filtrenizi ekleyebileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="0e5f5-111">Son olarak, ziyaretçilerin listesini gösteren günlük görünümünü görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="0e5f5-112">Bu uygulamalı laboratuvar, **ASP.NET MVC**'nin temel bilgisine sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="0e5f5-113">Daha önce **ASP.NET MVC** kullandıysanız, **ASP.NET MVC 4 temel** uygulamalı laboratuvarına gitmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="0e5f5-114">Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit yayımlarından](https://aka.ms/webcamps-training-kit)erişilebilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="0e5f5-115">Bu laboratuvara özgü proje, [ASP.NET MVC 4 özel eylem filtrelerinde](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="0e5f5-116">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="0e5f5-116">Objectives</span></span>

<span data-ttu-id="0e5f5-117">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="0e5f5-118">Filtreleme yeteneklerini genişletmek için özel eylem filtresi özniteliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e5f5-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="0e5f5-119">Belirli bir düzeye ekleme yaparak özel filtre özniteliği uygulama</span><span class="sxs-lookup"><span data-stu-id="0e5f5-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="0e5f5-120">Özel eylem filtrelerini küresel olarak kaydetme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="0e5f5-121">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0e5f5-121">Prerequisites</span></span>

<span data-ttu-id="0e5f5-122">Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="0e5f5-123">[Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="0e5f5-124">Kurulum</span><span class="sxs-lookup"><span data-stu-id="0e5f5-124">Setup</span></span>

<span data-ttu-id="0e5f5-125">**Kod parçacıklarını yükleme**</span><span class="sxs-lookup"><span data-stu-id="0e5f5-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="0e5f5-126">Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="0e5f5-127">Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="0e5f5-128">Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek C: kod parçacıkları&quot;kullanarak](#AppendixC) bu belgedeki eke başvurabilirsiniz &quot;.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="0e5f5-129">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="0e5f5-129">Exercises</span></span>

<span data-ttu-id="0e5f5-130">Bu uygulamalı laboratuvar aşağıdaki alýþtýrmalardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="0e5f5-131">Alıştırma 1: günlük eylemleri</span><span class="sxs-lookup"><span data-stu-id="0e5f5-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="0e5f5-132">Alıştırma 2: birden çok eylem filtresini yönetme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="0e5f5-133">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **30 dakika**.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="0e5f5-134">Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="0e5f5-135">Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="0e5f5-136">Alıştırma 1: günlük eylemleri</span><span class="sxs-lookup"><span data-stu-id="0e5f5-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="0e5f5-137">Bu alıştırmada, ASP.NET MVC 4 filtre sağlayıcılarını kullanarak özel bir eylem günlüğü filtresi oluşturmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="0e5f5-138">Bu amaçla, MusicStore sitesinde seçili denetleyicilere tüm etkinlikleri kaydedecek bir günlüğe kaydetme filtresi uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="0e5f5-139">Filtre **ActionFilterAttributeclass** öğesini genişletir ve her isteği yakalamak ve sonra günlüğe kaydetme eylemlerini gerçekleştirmek Için **OnActionExecuting** metodunu geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="0e5f5-140">HTTP istekleri, çalıştırılan Yöntemler, sonuçlar ve parametreler hakkındaki bağlam bilgileri ASP.NET MVC **ActionExecutingContext** sınıfı tarafından sağlanacaktır **.**</span><span class="sxs-lookup"><span data-stu-id="0e5f5-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="0e5f5-141">ASP.NET MVC 4 ' te özel bir filtre oluşturmadan kullanabileceğiniz varsayılan filtre sağlayıcıları da vardır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="0e5f5-142">ASP.NET MVC 4, aşağıdaki filtre türlerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="0e5f5-143">**Yetkilendirme** filtresi, kimlik doğrulaması gerçekleştirme veya isteğin özelliklerini doğrulama gibi bir eylem yönteminin yürütülüp yürütülmeyeceğini belirten güvenlik kararları verir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="0e5f5-144">Eylem yöntemi yürütmesini sarmalayan **eylem** filtresi.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="0e5f5-145">Bu filtre, eylem yöntemine ek veri sağlama, dönüş değerini İnceleme veya eylem yönteminin yürütülmesini iptal etme gibi ek işlemler gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="0e5f5-146">ActionResult nesnesinin yürütülmesini sarmalayan **sonuç** filtresi.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="0e5f5-147">Bu filtre, HTTP yanıtını değiştirme gibi sonucun ek işlemesini gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="0e5f5-148">Yetkilendirme filtreleriyle başlayıp sonuç yürütülene kadar, eylem yönteminde bir yerde oluşturulan işlenmeyen bir özel durum varsa yürütülen **özel durum** filtresi.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="0e5f5-149">Özel durum filtreleri, günlüğe kaydetme veya hata sayfası görüntüleme gibi görevler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="0e5f5-150">Filtreler sağlayıcıları hakkında daha fazla bilgi için lütfen şu MSDN bağlantısını ziyaret edin: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="0e5f5-151">MVC müzik deposu Uygulama günlüğü özelliği hakkında</span><span class="sxs-lookup"><span data-stu-id="0e5f5-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="0e5f5-152">Bu müzik deposu çözümünde, Şu alanlarla, **ActionLog**adlı site günlüğü için yeni bir veri modeli tablosu vardır: bir isteği alan denetleyicinin adı, eylem, istemci IP 'Si ve zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="0e5f5-153">![Veri modeli. ActionLog tablosu.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Veri modeli. ActionLog tablosu.")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="0e5f5-154">*Veri modeli-ActionLog tablosu*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="0e5f5-155">Çözüm, **Mvcmusicmağazalarında/görünümlerde/ActionLog**dizininde bulunan eylem günlüğü için BIR ASP.NET MVC görünümü sağlar:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="0e5f5-156">![Eylem günlüğü görünümü](aspnet-mvc-4-custom-action-filters/_static/image2.png "Eylem günlüğü görünümü")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="0e5f5-157">*Eylem günlüğü görünümü*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-157">*Action Log view*</span></span>

<span data-ttu-id="0e5f5-158">Bu yapı söz konusu olduğunda, tüm işler denetleyicinin isteğini kesintiye uğratma ve özel filtreleme kullanılarak günlüğe kaydetme işlemlerini gerçekleştirmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="0e5f5-159">Görev 1-bir denetleyicinin Isteğini yakalamak için özel bir filtre oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e5f5-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="0e5f5-160">Bu görevde, günlüğe kaydetme mantığını içerecek bir özel filtre öznitelik sınıfı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="0e5f5-161">Bu amaçla, ASP.NET MVC **ActionFilterAttribute** sınıfını genişletecektir ve **IActionFilter**arabirimini uygulamalısınız.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="0e5f5-162">**ActionFilterAttribute** tüm öznitelik filtrelerinin taban sınıfıdır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="0e5f5-163">Bu, denetleyici eyleminin yürütmeden sonra ve öncesinde belirli bir mantığı yürütmek için aşağıdaki yöntemleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="0e5f5-164">**OnActionExecuting**(ActionExecutingContext filtercontext): eylem yöntemi çağrılmadan hemen önce.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="0e5f5-165">**Onactionyürütüldü**(ActionExecutedContext filtercontext): eylem yöntemi çağrıldıktan sonra ve sonuç yürütülmeden önce (oluşturma tamamlanmadan önce).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="0e5f5-166">**OnResultExecuting**(ResultExecutingContext filtercontext): sonuç yürütülmeden hemen önce (görüntü işleme öncesi).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="0e5f5-167">**OnResultExecuted**(ResultExecutedContext filtercontext): sonuç yürütüldükten sonra (görünüm işlendiğinde).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="0e5f5-168">Bu yöntemlerin herhangi birini türetilmiş bir sınıfa geçersiz kılarak kendi filtreleme kodunuzu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>

1. <span data-ttu-id="0e5f5-169">**\Source\ex01-loggingactions\begin** klasöründe bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="0e5f5-170">Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="0e5f5-171">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="0e5f5-172">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="0e5f5-173">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0e5f5-174">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0e5f5-175">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0e5f5-176">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="0e5f5-177">Daha fazla bilgi için şu makaleye bakın: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="0e5f5-178">Filtreler klasörüne yeni C# bir sınıf ekleyin ve *CustomActionFilter.cs*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="0e5f5-179">Bu klasör tüm özel filtreleri depolayacaktır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="0e5f5-180">**CustomActionFilter.cs** açın ve **System. Web. Mvc** ve **Mvcmusicstore. model** ad alanlarına bir başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="0e5f5-181">(Kod parçacığı- *ASP.NET MVC 4 özel eylem filtreleri-Ex1-CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="0e5f5-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="0e5f5-182">**ActionFilterAttribute** ' dan **CustomActionFilter** sınıfını devralma ve **CustomActionFilter** sınıfını **IActionFilter** arabirimini uygulamasına getirme.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="0e5f5-183">**CustomActionFilter** sınıfının, **OnActionExecuting** metodunu geçersiz kılmasını ve filtrenin yürütmesini günlüğe kaydetmek için gerekli mantığı eklemesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="0e5f5-184">Bunu yapmak için, aşağıdaki vurgulanmış kodu **CustomActionFilter** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="0e5f5-185">(Kod parçacığı- *ASP.NET MVC 4 özel eylem filtreleri-Ex1-LoggingActions*)</span><span class="sxs-lookup"><span data-stu-id="0e5f5-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="0e5f5-186">**OnActionExecuting** yöntemi yeni bir ActionLog kaydı eklemek için **Entity Framework** kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="0e5f5-187">Bu, **filtre bağlamından**bağlam bilgileriyle yeni bir varlık örneği oluşturur ve doldurur.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="0e5f5-188">[MSDN](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)'de **ControllerContext** sınıfı hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="0e5f5-189">Görev 2-mağaza denetleyicisi sınıfına bir kod yakalayıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="0e5f5-190">Bu görevde, ekleme bu özel filtreyi, günlüğe kaydedilecek tüm denetleyici sınıfları ve denetleyici eylemlerine göre ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="0e5f5-191">Bu alıştırmanın amacına yönelik olarak, mağaza denetleyicisi sınıfının günlüğü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="0e5f5-192">**Actionlogfilterattribute** özel filtresinden **yürütülen onactionthe** yöntemi, eklenen bir öğe çağrıldığında çalışır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="0e5f5-193">Belirli bir denetleyici yöntemini ele almak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="0e5f5-194">**Mvcmusicstore\controllers** konumundaki **storecontroller** ' i açın ve **Filtreler** ad alanına bir başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="0e5f5-195">Sınıf bildiriminden önce **[CustomActionFilter]** özniteliğini ekleyerek özel filtre **CustomActionFilter** ' yi **storecontroller** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="0e5f5-196">Bir filtre bir denetleyici sınıfına eklendiğinde, tüm eylemleri de eklenir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="0e5f5-197">Filtreyi yalnızca bir eylemler kümesi için uygulamak istiyorsanız, her birine **[CustomActionFilter]** ekleme yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="0e5f5-198">Görev 3-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0e5f5-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="0e5f5-199">Bu görevde, günlüğe kaydetme filtresinin çalıştığını test edersiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="0e5f5-200">Uygulamayı başlatacak ve mağazayı ziyaret edecek ve sonra günlüğe kaydedilen etkinlikleri kontrol edersiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="0e5f5-201">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="0e5f5-202">Günlük görünümü başlangıç durumunu görmek için **/ActionLog** adresine gidin:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="0e5f5-203">![Sayfa etkinlikten önce günlük izleyici durumu](aspnet-mvc-4-custom-action-filters/_static/image3.png "Sayfa etkinlikten önce günlük izleyici durumu")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="0e5f5-204">*Sayfa etkinlikten önce günlük izleyici durumu*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="0e5f5-205">Varsayılan olarak, menü için mevcut tarzlar alınırken oluşturulan bir öğeyi her zaman gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="0e5f5-206">Kolaylık sağlamak için, uygulama her çalıştırıldığında **ActionLog** tablosunu temizliyoruz, böylece yalnızca belirli bir görevin doğrulamasının günlükleri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="0e5f5-207">Mağaza denetleyicisi içinde yürütülen tüm eylemler için bir geçmiş günlüğü kaydetmek üzere **oturum\_start** yönteminden ( **Global. asax** sınıfında) aşağıdaki kodu kaldırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="0e5f5-208">Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="0e5f5-209">**/ActionLog** ' a gidin ve günlük boşsa, sayfayı yenilemek için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="0e5f5-210">Ziyaretlerinizin izlendiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="0e5f5-211">![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image4.png "Etkinlik günlüğe kaydedilen eylem günlüğü")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0e5f5-212">*Etkinlik günlüğe kaydedilen eylem günlüğü*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="0e5f5-213">Alıştırma 2: birden çok eylem filtresini yönetme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="0e5f5-214">Bu alıştırmada, StoreController sınıfına ikinci bir özel eylem filtresi ekleyecek ve her iki filtrenin de gerçekleştirileceği belirli bir sırayı tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="0e5f5-215">Daha sonra, filtreyi Global olarak kaydetmek için kodu güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="0e5f5-216">Filtrelerin yürütme sırası tanımlanırken dikkate almanız gereken farklı seçenekler vardır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="0e5f5-217">Örneğin, Order özelliği ve filtrelerin kapsam:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="0e5f5-218">Filtrelerin her biri için bir **kapsam** tanımlayabilirsiniz, örneğin, **Denetleyici kapsamında**çalıştırmak için tüm eylem filtrelerini ve **genel kapsamda**çalıştırılacak tüm yetkilendirme filtrelerini kapsam yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="0e5f5-219">Kapsamların tanımlı bir yürütme sırası vardır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="0e5f5-220">Ayrıca, her eylem filtresinin, filtrenin kapsamındaki yürütme sırasını belirlemede kullanılan bir Order özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="0e5f5-221">Özel eylem filtreleri yürütme sırası hakkında daha fazla bilgi için lütfen şu MSDN makalesini ziyaret edin: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="0e5f5-222">Görev 1: yeni bir özel eylem filtresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e5f5-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="0e5f5-223">Bu görevde, StoreController sınıfına eklenecek yeni bir özel eylem filtresi oluşturacaksınız ve filtrelerin yürütme sırasının nasıl yönetileceğini öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="0e5f5-224">**\Source\Ex02-ManagingMultipleActionFilters\Begin** klasöründe bulunan **Başlangıç** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="0e5f5-225">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="0e5f5-226">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0e5f5-227">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="0e5f5-228">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="0e5f5-229">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="0e5f5-230">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0e5f5-231">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0e5f5-232">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="0e5f5-233">Daha fazla bilgi için şu makaleye bakın: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="0e5f5-234">Filtreler klasörüne yeni C# bir sınıf ekleyin ve *MyNewCustomActionFilter.cs* olarak adlandırın</span><span class="sxs-lookup"><span data-stu-id="0e5f5-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="0e5f5-235">**MyNewCustomActionFilter.cs** açın ve **System. Web. Mvc** ve **Mvcmusicstore. modeller** ad alanına bir başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="0e5f5-236">(Kod parçacığı- *ASP.NET MVC 4 özel eylem filtreleri-EX2-MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="0e5f5-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="0e5f5-237">Varsayılan sınıf bildirimini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="0e5f5-238">(Kod parçacığı- *ASP.NET MVC 4 özel eylem filtreleri-EX2-MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="0e5f5-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="0e5f5-239">Bu özel eylem filtresi, bir önceki alıştırmada oluşturduğdan neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="0e5f5-240">Ana fark, hangi filtrenin günlüğe kaydedildiğini belirlemek için bu yeni sınıf ' adı ile güncelleştirilmiş *&quot;&quot;özniteliği tarafından kaydedilen* sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify which filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="0e5f5-241">2\. görev: StoreController sınıfına yeni bir kod yakalayıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="0e5f5-242">Bu görevde, StoreController sınıfına yeni bir özel filtre ekleyecek ve iki filtrenin birlikte nasıl çalıştığını doğrulamak için çözümü çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="0e5f5-243">**Mvcmusicstore\controllers** dizininde bulunan **storecontroller** sınıfını açın ve aşağıdaki kodda gösterildiği gibi yeni özel filtre MyNewCustomActionFilter **storecontroller** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="0e5f5-244">Şimdi, bu iki özel eylem filtrelerinin nasıl çalıştığını görmek için uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="0e5f5-245">Bunu yapmak için **F5** tuşuna basın ve uygulama başlatılana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="0e5f5-246">Günlük görünümü başlangıç durumunu görmek için **/ActionLog** ' a gidin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="0e5f5-247">![Sayfa etkinlikten önce günlük izleyici durumu](aspnet-mvc-4-custom-action-filters/_static/image5.png "Sayfa etkinlikten önce günlük izleyici durumu")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="0e5f5-248">*Sayfa etkinlikten önce günlük izleyici durumu*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="0e5f5-249">Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="0e5f5-250">Bu süreyi denetleyin; ziyaretleriniz iki kez izleniyor: **Storagecontroller** sınıfına eklediğiniz her bir özel eylem filtresi için bir kez.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="0e5f5-251">![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image6.png "Etkinlik günlüğe kaydedilen eylem günlüğü")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0e5f5-252">*Etkinlik günlüğe kaydedilen eylem günlüğü*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="0e5f5-253">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="0e5f5-254">Görev 3: filtre sıralamasını yönetme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="0e5f5-255">Bu görevde, Order özelliğini kullanarak filtrelerin yürütme sırasını yönetmeyi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-255">In this task, you will learn how to manage the filters' execution order by using the Order property.</span></span>

1. <span data-ttu-id="0e5f5-256">**Mvcmusicstore\controllers** yolunda bulunan **storecontroller** sınıfını açın ve **Order** özelliğini aşağıda gösterildiği gibi her iki filtrede de belirtin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="0e5f5-257">Şimdi, Order özelliğinin değerine bağlı olarak filtrelerin nasıl yürütüleceğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="0e5f5-258">En küçük sıra değeri (**CustomActionFilter**) ile filtrenin yürütülen ilk bir değer olduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="0e5f5-259">**F5** tuşuna basın ve uygulama başlatılana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="0e5f5-260">Günlük görünümü başlangıç durumunu görmek için **/ActionLog** ' a gidin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="0e5f5-261">![Sayfa etkinlikten önce günlük izleyici durumu](aspnet-mvc-4-custom-action-filters/_static/image7.png "Sayfa etkinlikten önce günlük izleyici durumu")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="0e5f5-262">*Sayfa etkinlikten önce günlük izleyici durumu*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="0e5f5-263">Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="0e5f5-264">Bu zamanın, ilk olarak filtrelerin ' Order value: **CustomActionFilter** logs ' filtreleri tarafından sıralanmış olarak izlendiğini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="0e5f5-265">![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image8.png "Etkinlik günlüğe kaydedilen eylem günlüğü")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0e5f5-266">*Etkinlik günlüğe kaydedilen eylem günlüğü*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="0e5f5-267">Şimdi, filtrelerin sıra değerini güncelleyerek günlüğe kaydetme sırasının nasıl değiştiğini doğrulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="0e5f5-268">**Storecontroller** sınıfında, aşağıda gösterildiği gibi filtrelerin sıra değerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="0e5f5-269">**F5**tuşuna basarak uygulamayı yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="0e5f5-270">Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="0e5f5-271">Bu zamanın, **MyNewCustomActionFilter** filtresi tarafından oluşturulan günlüklerin önce göründüğünü kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="0e5f5-272">![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image9.png "Etkinlik günlüğe kaydedilen eylem günlüğü")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0e5f5-273">*Etkinlik günlüğe kaydedilen eylem günlüğü*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="0e5f5-274">Görev 4: filtreleri küresel olarak kaydetme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="0e5f5-275">Bu görevde, yeni filtreyi (**MyNewCustomActionFilter**) genel bir filtre olarak kaydetmek için çözümü güncelleşolursunuz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="0e5f5-276">Bunu yaptığınızda, uygulama yalnızca önceki görevde olduğu gibi, yalnızca StoreController içinde değil, uygulamada gerçekleştirilen tüm eylemler tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-276">By doing this, it will be triggered by all the actions performed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="0e5f5-277">**Storecontroller** sınıfında [ **MyNewCustomActionFilter]** özniteliğini ve Order özelliğini **[CustomActionFilter]** öğesinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="0e5f5-278">Aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="0e5f5-279">**Global. asax** dosyasını açın ve **uygulama\_start** metodunu bulun.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="0e5f5-280">Uygulamanın her başladığı her seferinde, **Filterconfig** sınıfında **registerglobalfilters** metodunu çağırarak genel filtrelerin kaydedildiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="0e5f5-281">![Global. asax içinde genel filtreleri kaydetme](aspnet-mvc-4-custom-action-filters/_static/image10.png "Global. asax içinde genel filtreleri kaydetme")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="0e5f5-282">*Global. asax içinde genel filtreleri kaydetme*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="0e5f5-283">**FilterConfig.cs** dosyasını **uygulama\_başlangıç** klasörü içinde açın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="0e5f5-284">System. Web. Mvc kullanarak bir başvuru ekleyin MvcMusicStore. Filters; kullanma uzayına.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="0e5f5-285">Özel filtrenizi ekleyerek **Registerglobalfilters** metodunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="0e5f5-286">Bunu yapmak için vurgulanan kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="0e5f5-287">**F5**tuşuna basarak uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="0e5f5-288">Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="0e5f5-289">Artık **[MyNewCustomActionFilter]** ' ın HomeController ve ActionLogController 'e de eklenmiş olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="0e5f5-290">![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image11.png "Etkinlik günlüğe kaydedilen eylem günlüğü")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0e5f5-291">*Genel etkinlik günlüğe kaydedilen eylem günlüğü*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="0e5f5-292">Ek olarak, bu uygulamayı Microsoft Azure Web siteleri ' ne ek [B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixB)için de dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="0e5f5-293">Özet</span><span class="sxs-lookup"><span data-stu-id="0e5f5-293">Summary</span></span>

<span data-ttu-id="0e5f5-294">Bu uygulamalı Laboratuvarı tamamlayarak özel eylemleri yürütmek için bir eylem filtresinin nasıl genişletileceğini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="0e5f5-295">Ayrıca, sayfa denetleyicilerinize herhangi bir filtrenin nasıl ekleneceğini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="0e5f5-296">Aşağıdaki kavramlar kullanıldı:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-296">The following concepts were used:</span></span>

- <span data-ttu-id="0e5f5-297">ASP.NET MVC ActionFilterAttribute sınıfıyla özel eylem filtreleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e5f5-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="0e5f5-298">ASP.NET MVC denetleyicilerine filtre ekleme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="0e5f5-299">Order özelliğini kullanarak filtre sıralamasını yönetme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="0e5f5-300">Filtreleri küresel olarak kaydetme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="0e5f5-301">Ek A: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="0e5f5-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="0e5f5-302">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="0e5f5-303">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="0e5f5-304">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) kısmına gidin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-304">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="0e5f5-305">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="0e5f5-306">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-306">Click on **Install Now**.</span></span> <span data-ttu-id="0e5f5-307">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="0e5f5-308">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="0e5f5-309">![Visual Studio Express yüklensin](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="0e5f5-310">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="0e5f5-311">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="0e5f5-313">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="0e5f5-314">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-314">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="0e5f5-316">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-316">*Installation progress*</span></span>
6. <span data-ttu-id="0e5f5-317">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-317">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="0e5f5-319">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-319">*Installation completed*</span></span>
7. <span data-ttu-id="0e5f5-320">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="0e5f5-321">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="0e5f5-323">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0e5f5-324">Ek B: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="0e5f5-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="0e5f5-325">Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="0e5f5-326">Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e5f5-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="0e5f5-327">[Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e5f5-328">Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="0e5f5-329">[Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-329">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="0e5f5-330">![Windows Azure portal oturum açın](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure portal oturum açın")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="0e5f5-331">*Windows Azure 'da oturum açma Yönetim Portalı*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="0e5f5-332">Komut çubuğunda **Yeni** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="0e5f5-333">![Yeni bir Web sitesi oluşturma](aspnet-mvc-4-custom-action-filters/_static/image18.png "Yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="0e5f5-334">*Yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="0e5f5-335">**İşlem** | **Web sitesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="0e5f5-336">Sonra **hızlı oluştur** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="0e5f5-337">Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e5f5-338">Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="0e5f5-339">Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="0e5f5-340">Bir veritabanı ayarlamaya yönelik adımları içermez.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="0e5f5-341">![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](aspnet-mvc-4-custom-action-filters/_static/image19.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="0e5f5-342">*Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="0e5f5-343">Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="0e5f5-344">Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="0e5f5-345">Yeni Web sitesinin çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="0e5f5-346">![Yeni Web sitesine göz atma](aspnet-mvc-4-custom-action-filters/_static/image20.png "Yeni Web sitesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="0e5f5-347">*Yeni Web sitesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="0e5f5-348">![Web sitesi çalışıyor](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web sitesi çalışıyor")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="0e5f5-349">*Web sitesi çalışıyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-349">*Web site running*</span></span>
6. <span data-ttu-id="0e5f5-350">Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="0e5f5-351">![Web sitesi yönetim sayfalarını açma](aspnet-mvc-4-custom-action-filters/_static/image22.png "Web sitesi yönetim sayfalarını açma")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="0e5f5-352">*Web sitesi yönetim sayfalarını açma*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="0e5f5-353">**Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e5f5-354">*Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="0e5f5-355">Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="0e5f5-356">**Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="0e5f5-357">![Web sitesi yayımlama profili indiriliyor](aspnet-mvc-4-custom-action-filters/_static/image23.png "Web sitesi yayımlama profili indiriliyor")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="0e5f5-358">*Web sitesi yayımlama profili indiriliyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="0e5f5-359">Yayımlama profili dosyasını bilinen bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="0e5f5-360">Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="0e5f5-361">![Yayımlama profili dosyası kaydediliyor](aspnet-mvc-4-custom-action-filters/_static/image24.png "Yayımlama profili kaydediliyor")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="0e5f5-362">*Yayımlama profili dosyası kaydediliyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="0e5f5-363">Görev 2-veritabanı sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0e5f5-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="0e5f5-364">Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="0e5f5-365">SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="0e5f5-366">Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="0e5f5-367">SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="0e5f5-368">Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="0e5f5-369">**Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="0e5f5-370">Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="0e5f5-371">![SQL veritabanı sunucu panosu](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL veritabanı sunucu panosu")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="0e5f5-372">*SQL veritabanı sunucu panosu*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="0e5f5-373">Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="0e5f5-374">Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](aspnet-mvc-4-custom-action-filters/_static/image26.png) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![Istemci IP adresi ekleniyor](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="0e5f5-376">*Istemci IP adresi ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="0e5f5-377">**ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Değişiklikleri Onayla](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="0e5f5-379">*Değişiklikleri Onayla*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0e5f5-380">Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="0e5f5-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="0e5f5-381">ASP.NET MVC 4 çözümüne geri dönün.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="0e5f5-382">**Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="0e5f5-383">![Uygulama yayımlanıyor](aspnet-mvc-4-custom-action-filters/_static/image29.png "Uygulamayı Yayımlama")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="0e5f5-384">*Web sitesi yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="0e5f5-385">İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="0e5f5-386">![Yayımlama profilini içeri aktarma](aspnet-mvc-4-custom-action-filters/_static/image30.png "Yayımlama profilini içeri aktarma")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="0e5f5-387">*Yayımlama profili içeri aktarılıyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="0e5f5-388">**Bağlantıyı doğrula**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-388">Click **Validate Connection**.</span></span> <span data-ttu-id="0e5f5-389">Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e5f5-390">Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="0e5f5-391">![Bağlantı doğrulanıyor](aspnet-mvc-4-custom-action-filters/_static/image31.png "Bağlantı doğrulanıyor")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="0e5f5-392">*Bağlantı doğrulanıyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-392">*Validating connection*</span></span>
4. <span data-ttu-id="0e5f5-393">**Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="0e5f5-394">![Web dağıtımı yapılandırması](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web dağıtımı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="0e5f5-395">*Web dağıtımı yapılandırması*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="0e5f5-396">Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="0e5f5-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="0e5f5-397">**Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="0e5f5-398">**Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="0e5f5-399">**Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="0e5f5-400">Yeni bir veritabanı adı yazın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-400">Type a new database name.</span></span>

     <span data-ttu-id="0e5f5-401">![Hedef bağlantı dizesi yapılandırılıyor](aspnet-mvc-4-custom-action-filters/_static/image33.png "Hedef bağlantı dizesi yapılandırılıyor")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="0e5f5-402">*Hedef bağlantı dizesi yapılandırılıyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="0e5f5-403">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-403">Then click **OK**.</span></span> <span data-ttu-id="0e5f5-404">Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="0e5f5-405">![Veritabanı oluşturma](aspnet-mvc-4-custom-action-filters/_static/image34.png "Veritabanı dizesi oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="0e5f5-406">*Veritabanı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-406">*Creating the database*</span></span>
7. <span data-ttu-id="0e5f5-407">Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="0e5f5-408">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-408">Then click **Next**.</span></span>

    <span data-ttu-id="0e5f5-409">![SQL veritabanı 'na işaret eden bağlantı dizesi](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL veritabanı 'na işaret eden bağlantı dizesi")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="0e5f5-410">*SQL veritabanı 'na işaret eden bağlantı dizesi*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="0e5f5-411">**Önizleme** sayfasında **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="0e5f5-412">![Web uygulaması yayımlanıyor](aspnet-mvc-4-custom-action-filters/_static/image36.png "Web uygulaması yayımlanıyor")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="0e5f5-413">*Web uygulaması yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="0e5f5-414">Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="0e5f5-415">Ek C: kod parçacıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="0e5f5-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="0e5f5-416">Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="0e5f5-417">Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="0e5f5-418">![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-custom-action-filters/_static/image37.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="0e5f5-419">*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="0e5f5-420">***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***</span><span class="sxs-lookup"><span data-stu-id="0e5f5-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="0e5f5-421">Kodu eklemek istediğiniz yere imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="0e5f5-422">Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="0e5f5-423">IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="0e5f5-424">Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="0e5f5-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="0e5f5-425">Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="0e5f5-426">![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-custom-action-filters/_static/image38.png "Kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="0e5f5-427">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="0e5f5-428">![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-custom-action-filters/_static/image39.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="0e5f5-429">*Vurgulanan parçacığı seçmek için Tab tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="0e5f5-430">![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-custom-action-filters/_static/image40.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="0e5f5-431">*Sekmeye tekrar basın ve kod parçacığı genişletilir*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="0e5f5-432">***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="0e5f5-433">Kod parçacığını eklemek istediğiniz yere sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="0e5f5-434">Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="0e5f5-435">Listeden tıklatarak ilgili kod parçacığını seçin.</span><span class="sxs-lookup"><span data-stu-id="0e5f5-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="0e5f5-436">![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-custom-action-filters/_static/image41.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="0e5f5-437">*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="0e5f5-438">![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-custom-action-filters/_static/image42.png "Listeden tıklatarak ilgili kod parçacığını seçin")</span><span class="sxs-lookup"><span data-stu-id="0e5f5-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="0e5f5-439">*Listeden tıklatarak ilgili kod parçacığını seçin*</span><span class="sxs-lookup"><span data-stu-id="0e5f5-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
