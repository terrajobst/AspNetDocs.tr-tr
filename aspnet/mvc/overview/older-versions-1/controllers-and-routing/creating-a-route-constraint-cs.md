---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: Yol kısıtlaması oluşturma (C#) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther, normal ifadelerle yol kısıtlamaları oluşturarak tarayıcı isteklerinin yollarla nasıl eşleştiğini nasıl denetleyebileceğinizi göstermektedir.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582014"
---
# <a name="creating-a-route-constraint-c"></a><span data-ttu-id="6d7fe-103">Rota Kısıtlaması Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="6d7fe-103">Creating a Route Constraint (C#)</span></span>

<span data-ttu-id="6d7fe-104">ile [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="6d7fe-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="6d7fe-105">Bu öğreticide, Stephen Walther, normal ifadelerle yol kısıtlamaları oluşturarak tarayıcı isteklerinin yollarla nasıl eşleştiğini nasıl denetleyebileceğinizi göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="6d7fe-106">Belirli bir rota ile eşleşen Tarayıcı isteklerini kısıtlamak için yol kısıtlamalarını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="6d7fe-107">Bir yol kısıtlaması belirtmek için normal bir ifade kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="6d7fe-108">Örneğin, yolu Global. asax dosyanızda liste 1 ' de tanımladığınızı düşünün.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="6d7fe-109">**Listeleme 1-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="6d7fe-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="6d7fe-110">Listeleme 1, ürün adlı bir rota içerir.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="6d7fe-111">Tarayıcı isteklerini, liste 2 ' de bulunan ProductController ile eşlemek için ürün yolunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="6d7fe-112">**Listeleme 2-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="6d7fe-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="6d7fe-113">Ürün denetleyicisi tarafından açığa çıkarılan ayrıntılar () eyleminin ProductID adlı tek bir parametreyi kabul ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="6d7fe-114">Bu parametre bir tamsayı parametresidir.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="6d7fe-115">Liste 1 ' de tanımlanan yol aşağıdaki URL 'Lerden hiçbiriyle eşleşir:</span><span class="sxs-lookup"><span data-stu-id="6d7fe-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="6d7fe-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="6d7fe-116">/Product/23</span></span>
- <span data-ttu-id="6d7fe-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="6d7fe-117">/Product/7</span></span>

<span data-ttu-id="6d7fe-118">Ne yazık ki yol aşağıdaki URL 'Lerle aynı olacaktır:</span><span class="sxs-lookup"><span data-stu-id="6d7fe-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="6d7fe-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="6d7fe-119">/Product/blah</span></span>
- <span data-ttu-id="6d7fe-120">/Product/Apple</span><span class="sxs-lookup"><span data-stu-id="6d7fe-120">/Product/apple</span></span>

<span data-ttu-id="6d7fe-121">Ayrıntılar () eylemi bir tamsayı parametresi beklediği için, bir tamsayı değeri dışında bir istek içeren bir isteğin yapılması hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="6d7fe-122">Örneğin, tarayıcınıza/Product/Apple URL 'sini yazarsanız Şekil 1 ' de hata sayfasını alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="6d7fe-123">[Yeni proje iletişim kutusunu ![](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6d7fe-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="6d7fe-124">**Şekil 01**: bir sayfa açılımı görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-route-constraint-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6d7fe-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>

<span data-ttu-id="6d7fe-125">Gerçekten ne yapmak istiyorsunuz, yalnızca uygun bir ProductID tamsayı içeren URL 'Leri eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="6d7fe-126">Rota ile eşleşen URL 'Leri kısıtlamak için bir yol tanımlarken bir kısıtlama kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="6d7fe-127">Listeleme 3 ' teki değiştirilen ürün yolu, yalnızca tamsayılarla eşleşen bir normal ifade kısıtlaması içerir.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="6d7fe-128">**Listeleme 3-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="6d7fe-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="6d7fe-129">\D + normal ifadesi bir veya daha fazla tamsayılarla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="6d7fe-130">Bu kısıtlama, ürün yolunun aşağıdaki URL 'Lerle eşleşmesini sağlar:</span><span class="sxs-lookup"><span data-stu-id="6d7fe-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="6d7fe-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="6d7fe-131">/Product/3</span></span>
- <span data-ttu-id="6d7fe-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="6d7fe-132">/Product/8999</span></span>

<span data-ttu-id="6d7fe-133">Şu URL 'Ler değil:</span><span class="sxs-lookup"><span data-stu-id="6d7fe-133">But not the following URLs:</span></span>

- <span data-ttu-id="6d7fe-134">/Product/Apple</span><span class="sxs-lookup"><span data-stu-id="6d7fe-134">/Product/apple</span></span>
- <span data-ttu-id="6d7fe-135">/Ürün</span><span class="sxs-lookup"><span data-stu-id="6d7fe-135">/Product</span></span>

- <span data-ttu-id="6d7fe-136">Bu tarayıcı istekleri başka bir yol tarafından işlenecek veya eşleşen yollar yoksa, *kaynak bulunamadı* hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6d7fe-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6d7fe-137">[Önceki](creating-custom-routes-cs.md)
> [İleri](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6d7fe-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
