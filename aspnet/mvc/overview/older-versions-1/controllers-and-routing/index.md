---
uid: mvc/overview/older-versions-1/controllers-and-routing/index
title: Denetleyiciler ve yönlendirme | Microsoft Docs
author: rick-anderson
description: Bu öğretici kümesinde, ASP.NET yönlendirmesi hakkında ASP.NET MVC denetleyici eylemleri için tarayıcı istekleri eşler öğrenin.
ms.author: riande
ms.date: 09/28/2011
ms.assetid: 124df537-428c-4861-b6c2-4830c094fe0c
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing
msc.type: chapter
ms.openlocfilehash: 62e8c3c7451373829e2e8fbf65e37a14cfea54df
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123301"
---
# <a name="controllers-and-routing"></a><span data-ttu-id="ad717-103">Denetleyiciler ve Yönlendirme</span><span class="sxs-lookup"><span data-stu-id="ad717-103">Controllers and Routing</span></span>

> <span data-ttu-id="ad717-104">Bu öğretici kümesinde, ASP.NET yönlendirmesi hakkında ASP.NET MVC denetleyici eylemleri için tarayıcı istekleri eşler öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ad717-104">In this tutorial set, you learn about ASP.NET routing, which maps browser requests to ASP.NET MVC controller actions.</span></span>

- [<span data-ttu-id="ad717-105">ASP.NET MVC Yönlendirmesine Genel Bakış (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-105">ASP.NET MVC Routing Overview (C#)</span></span>](asp-net-mvc-routing-overview-cs.md)
- [<span data-ttu-id="ad717-106">Eylem Filtrelerini Anlama (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-106">Understanding Action Filters (C#)</span></span>](understanding-action-filters-cs.md)
- [<span data-ttu-id="ad717-107">Çıktı Önbelleğe Alma ile Performansı İyileştirme (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-107">Improving Performance with Output Caching (C#)</span></span>](improving-performance-with-output-caching-cs.md)
- [<span data-ttu-id="ad717-108">Önbelleğe Alınmış Bir Sayfaya Dinamik İçerik Ekleme (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-108">Adding Dynamic Content to a Cached Page (C#)</span></span>](adding-dynamic-content-to-a-cached-page-cs.md)
- [<span data-ttu-id="ad717-109">Denetleyici Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-109">Creating a Controller (C#)</span></span>](creating-a-controller-cs.md)
- [<span data-ttu-id="ad717-110">Eylem Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-110">Creating an Action (C#)</span></span>](creating-an-action-cs.md)
- [<span data-ttu-id="ad717-111">ASP.NET MVC Yönlendirmesine Genel Bakış (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-111">ASP.NET MVC Routing Overview (VB)</span></span>](asp-net-mvc-routing-overview-vb.md)
- [<span data-ttu-id="ad717-112">Eylem Filtrelerini Anlama (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-112">Understanding Action Filters (VB)</span></span>](understanding-action-filters-vb.md)
- [<span data-ttu-id="ad717-113">Çıktı Önbelleğe Alma ile Performansı İyileştirme (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-113">Improving Performance with Output Caching (VB)</span></span>](improving-performance-with-output-caching-vb.md)
- [<span data-ttu-id="ad717-114">Önbelleğe Alınmış Bir Sayfaya Dinamik İçerik Ekleme (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-114">Adding Dynamic Content to a Cached Page (VB)</span></span>](adding-dynamic-content-to-a-cached-page-vb.md)
- [<span data-ttu-id="ad717-115">Denetleyici Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-115">Creating a Controller (VB)</span></span>](creating-a-controller-vb.md)
- [<span data-ttu-id="ad717-116">Eylem Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-116">Creating an Action (VB)</span></span>](creating-an-action-vb.md)
- [<span data-ttu-id="ad717-117">ASP.NET MVC Denetleyicisine Genel Bakış (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-117">ASP.NET MVC Controller Overview (C#)</span></span>](aspnet-mvc-controllers-overview-cs.md)
- [<span data-ttu-id="ad717-118">Özel Rotalar Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-118">Creating Custom Routes (C#)</span></span>](creating-custom-routes-cs.md)
- [<span data-ttu-id="ad717-119">Rota Kısıtlaması Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-119">Creating a Route Constraint (C#)</span></span>](creating-a-route-constraint-cs.md)
- [<span data-ttu-id="ad717-120">Özel Rota Kısıtlaması Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="ad717-120">Creating a Custom Route Constraint (C#)</span></span>](creating-a-custom-route-constraint-cs.md)
- [<span data-ttu-id="ad717-121">ASP.NET MVC Denetleyicisine Genel Bakış (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-121">ASP.NET MVC Controller Overview (VB)</span></span>](asp-net-mvc-controller-overview-vb.md)
- [<span data-ttu-id="ad717-122">Özel Rotalar Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-122">Creating Custom Routes (VB)</span></span>](creating-custom-routes-vb.md)
- [<span data-ttu-id="ad717-123">Rota Kısıtlaması Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-123">Creating a Route Constraint (VB)</span></span>](creating-a-route-constraint-vb.md)
- [<span data-ttu-id="ad717-124">Özel Rota Kısıtlaması Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="ad717-124">Creating a Custom Route Constraint (VB)</span></span>](creating-a-custom-route-constraint-vb.md)
