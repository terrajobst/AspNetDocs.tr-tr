---
uid: webhooks/receiving/dependencies
title: ASP.NET Web kancaları alıcı bağımlılıkları | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancalarına alıcı bağımlılıkları ve bağımlılık ekleme.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637286"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="f3d94-103">ASP.NET Web kancaları alıcı bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="f3d94-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="f3d94-104">Microsoft ASP.NET Web kancaları, bağımlılık ekleme göz önünde bulundurularak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f3d94-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="f3d94-105">Sistemdeki birçok bağımlılık, bir bağımlılık ekleme altyapısı kullanılarak alternatif uygulamalarla değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="f3d94-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="f3d94-106">Alıcı bağımlılıklarının listesi için bkz. [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) .</span><span class="sxs-lookup"><span data-stu-id="f3d94-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="f3d94-107">Hiçbir bağımlılık kaydedilmemişse, varsayılan bir uygulama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f3d94-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="f3d94-108">Varsayılan uygulamaların listesi için bkz. [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) .</span><span class="sxs-lookup"><span data-stu-id="f3d94-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
