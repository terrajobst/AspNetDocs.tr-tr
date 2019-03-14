---
uid: webhooks/receiving/dependencies
title: ASP.NET Web kancaları alıcı bağımlılıkları | Microsoft Docs
author: rick-anderson
description: Alıcı bağımlılıkları ve ASP.NET Web kancaları bağımlılık ekleme.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: c44cfe3ed310aa728a989b108c410e8786e4f514
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073263"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="fbcc0-103">ASP.NET Web kancaları alıcı bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="fbcc0-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="fbcc0-104">Microsoft ASP.NET WebHooks bağımlılık ekleme düşünülerek tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fbcc0-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="fbcc0-105">Çoğu bağımlılıkları sisteminde diğer uygulamaları ile bir bağımlılık ekleme altyapısı kullanılarak değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="fbcc0-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="fbcc0-106">Lütfen [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) alıcı bağımlılıkları listesi.</span><span class="sxs-lookup"><span data-stu-id="fbcc0-106">Please see [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="fbcc0-107">Hiçbir bağımlılık kayıtlı ise varsayılan bir uygulama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fbcc0-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="fbcc0-108">Lütfen [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) varsayılan uygulamaları listesi.</span><span class="sxs-lookup"><span data-stu-id="fbcc0-108">Please see [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
