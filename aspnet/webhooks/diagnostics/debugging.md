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
# <a name="aspnet-webhooks-debugging"></a>ASP.NET Web kancaları hata ayıklaması  

## <a name="debugging-in-azure"></a>Azure 'da hata ayıklama

Azure 'da çalışırken Web uygulamanızda hata ayıklamak için lütfen [Visual Studio 'yu kullanarak Azure App Service bir Web uygulamasının sorun giderme](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)öğreticisine bakın.

## <a name="debugging-with-source-and-symbols"></a>Kaynak ve simgelerle hata ayıklama

Kendi kodunuzda hata ayıklamanın yanı sıra, doğrudan Microsoft ASP.NET Web kancalarını ve tüm .NET sürümlerini ayıklamak mümkündür. Bu, yerel olarak veya uzaktan hata ayıklaması yapıp olmasanız da geçerlidir. İlk olarak, Visual Studio 'Yu **hata ayıklama** ve sonra **Seçenekler ve ayarlar**'a giderek kaynak ve sembolleri bulmak için yapılandırın. Aşağıdaki gibi seçenekleri ayarlayın:

![Seçenekler ve ayarlar](_static/SourceSymbols.png)

Sonra kaynak ve sembolleri indirmek için [symbolsource.org](http://symbolsource.org) 'e bir bağlantı ekleyin. Yukarıdaki menünün **semboller** sekmesine gidin ve aşağıdakini bir sembol konumu olarak ekleyin:

```
http://srv.symbolsource.org/pdb/Public
```

Ayrıca, Önbellek dizininin kısa bir ada sahip olduğundan emin olun; Aksi takdirde dosya adları çok uzun sürebilir, bu da simgelerin yüklenmesine neden olur. Örnek yol:

```
C:\SymCache
```

Ayarlar şuna benzer görünmelidir:

![Seçenekler sembol dosya konumu örneği](_static/SymSource.png)
