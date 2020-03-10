---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: Özel rotalar oluşturma (VB) | Microsoft Docs
author: microsoft
description: Özel yolların bir ASP.NET MVC uygulamasına nasıl ekleneceğini öğrenin. Bu öğreticide, Global. asax dosyasındaki varsayılan yol tablosunu değiştirme hakkında bilgi edineceksiniz.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 22b44e9e575c9d404881a23ee735bb0c8b7109e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601299"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="3bb76-104">Özel Rotalar Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="3bb76-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="3bb76-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="3bb76-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3bb76-106">Özel yolların bir ASP.NET MVC uygulamasına nasıl ekleneceğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3bb76-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="3bb76-107">Bu öğreticide, Global. asax dosyasındaki varsayılan yol tablosunu değiştirme hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bb76-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="3bb76-108">Bu öğreticide, bir ASP.NET MVC uygulamasına özel bir yol eklemeyi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bb76-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="3bb76-109">Global. asax dosyasındaki varsayılan yol tablosunu özel bir yol ile nasıl değiştireceğinizi öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bb76-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="3bb76-110">ASP.NET MVC uygulamalarında, varsayılan yol tablosu yalnızca iyi çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="3bb76-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="3bb76-111">Ancak, özel yönlendirme gereksinimleriniz olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bb76-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="3bb76-112">Bu durumda, özel bir yol oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bb76-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="3bb76-113">Örneğin, bir blog uygulaması oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="3bb76-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="3bb76-114">Şuna benzeyen gelen istekleri işlemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3bb76-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="3bb76-115">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="3bb76-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="3bb76-116">Bir Kullanıcı bu isteği girdiğinde, 12/25/2009 tarihine karşılık gelen blog girişini döndürmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="3bb76-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="3bb76-117">Bu tür bir isteği işlemek için özel bir yol oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bb76-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="3bb76-118">Liste 1 ' deki Global. asax dosyası,/Archive/*Giriş tarihi*gibi görünen Istekleri işleyen blog adlı yeni bir özel yol içerir.</span><span class="sxs-lookup"><span data-stu-id="3bb76-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="3bb76-119">**Listeleme 1-Global. asax (özel rota ile)**</span><span class="sxs-lookup"><span data-stu-id="3bb76-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="3bb76-120">Yol tablosuna eklediğiniz yolların sırası önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3bb76-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="3bb76-121">Yeni özel Blog Rotamız var olan varsayılan yolun önüne eklenir.</span><span class="sxs-lookup"><span data-stu-id="3bb76-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="3bb76-122">Siparişi tersine aldıysanız, varsayılan yol özel yol yerine her zaman çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3bb76-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="3bb76-123">Özel blog yolu,/Archive/. ile başlayan tüm istekler ile eşleşir</span><span class="sxs-lookup"><span data-stu-id="3bb76-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="3bb76-124">Bu nedenle, aşağıdaki URL 'Lerin tümüyle eşleşir:</span><span class="sxs-lookup"><span data-stu-id="3bb76-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="3bb76-125">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="3bb76-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="3bb76-126">/Archive/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="3bb76-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="3bb76-127">/Archive/apple</span><span class="sxs-lookup"><span data-stu-id="3bb76-127">/Archive/apple</span></span>

<span data-ttu-id="3bb76-128">Özel yol, gelen isteği arşiv adlı bir denetleyiciye eşler ve giriş () eylemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3bb76-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="3bb76-129">Entry () yöntemi çağrıldığında, giriş tarihi entryDate adlı bir parametre olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="3bb76-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="3bb76-130">Blog özel yolunu, döküm 2 ' de denetleyicisiyle birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bb76-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="3bb76-131">**Listeleme 2-ArchiveController. vb**</span><span class="sxs-lookup"><span data-stu-id="3bb76-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="3bb76-132">Liste 2 ' deki entry () yönteminin DateTime türünde bir parametreyi kabul ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3bb76-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="3bb76-133">MVC çerçevesi, giriş tarihini URL 'den otomatik olarak bir tarih saat değerine dönüştürecek kadar akıllıdır.</span><span class="sxs-lookup"><span data-stu-id="3bb76-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="3bb76-134">URL 'deki giriş tarihi parametresi bir tarih saat değerine dönüştürülemiyorsa bir hata oluşur (bkz. Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="3bb76-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="3bb76-135">**Şekil 1-parametre dönüştürülürken hata oluştu**</span><span class="sxs-lookup"><span data-stu-id="3bb76-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="3bb76-136">[Yeni proje iletişim kutusunu ![](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3bb76-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="3bb76-137">**Şekil 01**: parametre dönüştürülürken hata ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-routes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="3bb76-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="3bb76-138">Özet</span><span class="sxs-lookup"><span data-stu-id="3bb76-138">Summary</span></span>

<span data-ttu-id="3bb76-139">Bu öğreticinin amacı, nasıl özel bir rota oluşturacağınızı göstermektir.</span><span class="sxs-lookup"><span data-stu-id="3bb76-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="3bb76-140">Web günlüğü girdilerini temsil eden Global. asax dosyasındaki yol tablosuna nasıl özel bir yol ekleneceğini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="3bb76-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="3bb76-141">Blog girdilerine yönelik isteklerin ArchiveController adlı bir denetleyiciye ve girdi () adlı bir denetleyici eylemine nasıl eşleneceğini tartıştık.</span><span class="sxs-lookup"><span data-stu-id="3bb76-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3bb76-142">[Önceki](asp-net-mvc-controller-overview-vb.md)
> [İleri](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3bb76-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
