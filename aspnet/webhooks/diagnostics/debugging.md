---
uid: webhooks/diagnostics/debugging
title: ASP.NET Web kancaları hata ayıklaması | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancaları hatalarını ayıklama.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640870"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="9fbf8-103">ASP.NET Web kancaları hata ayıklaması</span><span class="sxs-lookup"><span data-stu-id="9fbf8-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="9fbf8-104">Azure 'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="9fbf8-104">Debugging in Azure</span></span>

<span data-ttu-id="9fbf8-105">Azure 'da çalışırken Web uygulamanızda hata ayıklamak için lütfen [Visual Studio 'yu kullanarak Azure App Service bir Web uygulamasının sorun giderme](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="9fbf8-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="9fbf8-106">Kaynak ve simgelerle hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="9fbf8-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="9fbf8-107">Kendi kodunuzda hata ayıklamanın yanı sıra, doğrudan Microsoft ASP.NET Web kancalarını ve tüm .NET sürümlerini ayıklamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="9fbf8-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="9fbf8-108">Bu, yerel olarak veya uzaktan hata ayıklaması yapıp olmasanız da geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9fbf8-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="9fbf8-109">İlk olarak, Visual Studio 'Yu **hata ayıklama** ve sonra **Seçenekler ve ayarlar**'a giderek kaynak ve sembolleri bulmak için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9fbf8-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="9fbf8-110">Aşağıdaki gibi seçenekleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="9fbf8-110">Set the options like this:</span></span>

![Seçenekler ve ayarlar](_static/SourceSymbols.png)

<span data-ttu-id="9fbf8-112">Sonra kaynak ve sembolleri indirmek için [symbolsource.org](http://symbolsource.org) 'e bir bağlantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9fbf8-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="9fbf8-113">Yukarıdaki menünün **semboller** sekmesine gidin ve aşağıdakini bir sembol konumu olarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9fbf8-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="9fbf8-114">Ayrıca, Önbellek dizininin kısa bir ada sahip olduğundan emin olun; Aksi takdirde dosya adları çok uzun sürebilir, bu da simgelerin yüklenmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fbf8-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="9fbf8-115">Örnek yol:</span><span class="sxs-lookup"><span data-stu-id="9fbf8-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="9fbf8-116">Ayarlar şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="9fbf8-116">The settings should look similar to this:</span></span>

![Seçenekler sembol dosya konumu örneği](_static/SymSource.png)
