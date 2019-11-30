---
uid: webhooks/receiving/dependencies
title: ASP.NET Web kancaları alıcı bağımlılıkları | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancalarına alıcı bağımlılıkları ve bağımlılık ekleme.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564866"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET Web kancaları alıcı bağımlılıkları

Microsoft ASP.NET Web kancaları, bağımlılık ekleme göz önünde bulundurularak tasarlanmıştır. Sistemdeki birçok bağımlılık, bir bağımlılık ekleme altyapısı kullanılarak alternatif uygulamalarla değiştirilebilir.

Alıcı bağımlılıklarının listesi için bkz. [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) . Hiçbir bağımlılık kaydedilmemişse, varsayılan bir uygulama kullanılır. Varsayılan uygulamaların listesi için bkz. [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) .
