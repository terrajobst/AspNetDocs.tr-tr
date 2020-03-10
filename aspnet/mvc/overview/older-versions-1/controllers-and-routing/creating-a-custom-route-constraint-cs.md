---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
title: Özel yol kısıtlaması oluşturma (C#) | Microsoft Docs
author: StephenWalther
description: Stephen Walther nasıl özel bir yol kısıtlaması oluşturacağınızı gösterir. Bir yolun w ile eşleştirilmesini engelleyen basit bir özel kısıtlama uyguladık...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: a4f4bf4e-abcc-4650-8f43-527e48b52fe6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 98d5839e3d2623665770ccc5689c28f9eb29c8f6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601453"
---
# <a name="creating-a-custom-route-constraint-c"></a><span data-ttu-id="fcf5f-104">Özel Rota Kısıtlaması Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="fcf5f-104">Creating a Custom Route Constraint (C#)</span></span>

<span data-ttu-id="fcf5f-105">ile [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="fcf5f-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="fcf5f-106">Stephen Walther nasıl özel bir yol kısıtlaması oluşturacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="fcf5f-107">Uzak bir bilgisayardan bir tarayıcı isteği yapıldığında bir yolun eşleştirilmesini engelleyen basit bir özel kısıtlama uyguladık.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>

<span data-ttu-id="fcf5f-108">Bu öğreticinin amacı, özel bir yol kısıtlaması oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="fcf5f-109">Özel bir yol kısıtlaması, bir özel koşul eşleştirilmediği takdirde bir yolun eşleştirilmesini engellemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="fcf5f-110">Bu öğreticide, bir localhost yol kısıtlaması oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="fcf5f-111">Localhost yol kısıtlaması yalnızca yerel bilgisayardan yapılan isteklerle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="fcf5f-112">Internet üzerinden gelen uzak istekler eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="fcf5f-113">IRouteConstraint arabirimini uygulayarak özel bir yol kısıtlaması uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="fcf5f-114">Bu, tek bir yöntemi açıklayan son derece basit bir arabirimdir:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="fcf5f-115">Yöntemi bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-115">The method returns a Boolean value.</span></span> <span data-ttu-id="fcf5f-116">False değerini döndürmediyseniz, kısıtlama ile ilişkili yol tarayıcı isteğiyle eşleşmez.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-116">If you return false, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="fcf5f-117">Localhost kısıtlaması, liste 1 ' de bulunur.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="fcf5f-118">**Listeleme 1-LocalhostConstraint.cs**</span><span class="sxs-lookup"><span data-stu-id="fcf5f-118">**Listing 1 - LocalhostConstraint.cs**</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="fcf5f-119">Listeleme 1 ' deki kısıtlama, HttpRequest sınıfı tarafından kullanıma sunulan IsLocal özelliğinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="fcf5f-120">Bu özellik, isteğin IP adresi 127.0.0.1 olduğunda ya da isteğin IP 'si sunucunun IP adresiyle aynı olduğunda true değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="fcf5f-121">Global. asax dosyasında tanımlanan bir yol içinde özel bir kısıtlama kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="fcf5f-122">Liste 2 ' deki Global. asax dosyası, yerel sunucudan istekte bulunmadıkları takdirde herkesin Yönetici sayfası istemesini engellemek için localhost kısıtlamasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="fcf5f-123">Örneğin, uzak bir sunucudan yapıldığında/Admin/DeleteAll için bir istek başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="fcf5f-124">**Listeleme 2-Global. asax**</span><span class="sxs-lookup"><span data-stu-id="fcf5f-124">**Listing 2 - Global.asax**</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="fcf5f-125">Localhost kısıtlaması, yönetici yolunun tanımında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="fcf5f-126">Bu yol, uzak bir tarayıcı isteğiyle eşleşmeyecek.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="fcf5f-127">Bununla birlikte, Global. asax dosyasında tanımlanan diğer yolların de aynı istekle eşleşeceğini fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="fcf5f-128">Bir kısıtlamanın, belirli bir yolun, Global. asax dosyasında tanımlı tüm yolların değil, bir istekle eşleşmesini önlediği anlaşılması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="fcf5f-129">Varsayılan yolun, liste 2 ' deki Global. asax dosyasından yorumdığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="fcf5f-130">Varsayılan yolu eklerseniz, varsayılan yol, yönetici denetleyicisi istekleriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="fcf5f-131">Bu durumda, uzak kullanıcılar, istekleri yönetici rotayla eşleşmese de yönetici denetleyicisinin eylemlerini çağırmaya devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fcf5f-132">[Önceki](creating-a-route-constraint-cs.md)
> [İleri](asp-net-mvc-controller-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fcf5f-132">[Previous](creating-a-route-constraint-cs.md)
[Next](asp-net-mvc-controller-overview-vb.md)</span></span>
