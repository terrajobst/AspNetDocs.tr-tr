---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Eylem oluşturma (C#) | Microsoft Docs
author: microsoft
description: Bir ASP.NET MVC denetleyicisine yeni bir eylem eklemeyi öğrenin. Bir yöntemin eylem olması için gereksinimler hakkında bilgi edinin.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582056"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="8491f-104">Eylem Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="8491f-104">Creating an Action (C#)</span></span>

<span data-ttu-id="8491f-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="8491f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8491f-106">Bir ASP.NET MVC denetleyicisine yeni bir eylem eklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8491f-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="8491f-107">Bir yöntemin eylem olması için gereksinimler hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="8491f-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="8491f-108">Bu öğreticinin amacı, yeni bir denetleyici eylemi oluşturmayı açıklamaktır.</span><span class="sxs-lookup"><span data-stu-id="8491f-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="8491f-109">Bir eylem yönteminin gereksinimleri hakkında bilgi edinirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8491f-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="8491f-110">Ayrıca bir yöntemin eylem olarak gösterilmesini nasıl önleyeceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8491f-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="8491f-111">Denetleyiciye eylem ekleme</span><span class="sxs-lookup"><span data-stu-id="8491f-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="8491f-112">Denetleyiciye yeni bir yöntem ekleyerek denetleyiciye yeni bir eylem eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="8491f-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="8491f-113">Örneğin, liste 1 ' deki denetleyici dizin () adlı bir eylem ve SayHello () adlı bir eylem içerir.</span><span class="sxs-lookup"><span data-stu-id="8491f-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="8491f-114">Her iki yöntem de eylem olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="8491f-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="8491f-115">**Listeleme 1-Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="8491f-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="8491f-116">Bir eylem olarak Universe sunulmak için bir yöntemin belirli gereksinimleri karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="8491f-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="8491f-117">Yöntemin ortak olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8491f-117">The method must be public.</span></span>
- <span data-ttu-id="8491f-118">Metot statik bir yöntem olamaz.</span><span class="sxs-lookup"><span data-stu-id="8491f-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="8491f-119">Yöntem bir genişletme yöntemi olamaz.</span><span class="sxs-lookup"><span data-stu-id="8491f-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="8491f-120">Yöntem bir Oluşturucu, alıcı veya ayarlayıcı olamaz.</span><span class="sxs-lookup"><span data-stu-id="8491f-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="8491f-121">Metodun açık genel türleri olamaz.</span><span class="sxs-lookup"><span data-stu-id="8491f-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="8491f-122">Yöntemi, denetleyici temel sınıfının bir yöntemi değildir.</span><span class="sxs-lookup"><span data-stu-id="8491f-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="8491f-123">Yöntem **ref** veya **Out** parametreleri içeremez.</span><span class="sxs-lookup"><span data-stu-id="8491f-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="8491f-124">Bir denetleyici eyleminin dönüş türü üzerinde hiçbir kısıtlama olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8491f-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="8491f-125">Bir denetleyici eylemi, bir dize, bir tarih saat, rastgele sınıfın bir örneği veya void döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="8491f-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="8491f-126">ASP.NET MVC Framework, bir eylem sonucu olmayan herhangi bir dönüş türünü bir dizeye dönüştürür ve dizeyi tarayıcıya işler.</span><span class="sxs-lookup"><span data-stu-id="8491f-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="8491f-127">Bu gereksinimleri ihlal etmediği herhangi bir yöntemi bir denetleyiciye eklediğinizde, yöntem bir denetleyici eylemi olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="8491f-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="8491f-128">Burada dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="8491f-128">Be careful here.</span></span> <span data-ttu-id="8491f-129">Bir denetleyici eylemi, Internet 'e bağlı olan herkes tarafından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="8491f-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="8491f-130">Örneğin, bir Deletemde Web sitesi () denetleyici eylemi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8491f-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="8491f-131">Ortak yöntemin çağrılmasını önlemek</span><span class="sxs-lookup"><span data-stu-id="8491f-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="8491f-132">Denetleyici sınıfında ortak bir yöntem oluşturmanız gerekiyorsa ve yöntemi bir denetleyici eylemi olarak göstermek istemiyorsanız, yöntemin [Nonactıon] özniteliği kullanılarak çağrılmasını engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8491f-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="8491f-133">Örneğin, liste 2 ' deki denetleyici, [Nonactıon] özniteliğiyle donatılmış Companygizlilikler () adlı bir genel yöntem içerir.</span><span class="sxs-lookup"><span data-stu-id="8491f-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="8491f-134">**Listeleme 2-Controllers\WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="8491f-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="8491f-135">Tarayıcınızın adres çubuğuna/Work/companygizlilikler yazarak Companygizlilikler () denetleyici eylemini çağırmaya çalışırsanız Şekil 1 ' de hata iletisini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="8491f-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="8491f-136">[Eylem olmayan bir yöntemi çağırmak ![](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8491f-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="8491f-137">**Şekil 01**: eylem olmayan bir yöntem çağırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-an-action-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="8491f-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8491f-138">[Önceki](creating-a-controller-cs.md)
> [İleri](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8491f-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
