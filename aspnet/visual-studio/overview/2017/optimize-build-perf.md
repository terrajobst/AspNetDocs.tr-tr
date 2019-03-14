---
uid: visual-studio/overview/2017/optimize-build-perf
title: Çözüm için derleme performansını iyileştirme
author: AngelosP
description: Çözüm için derleme performansını iyileştirme
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073803"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="0e075-103">Çözüm için derleme performansını iyileştirme</span><span class="sxs-lookup"><span data-stu-id="0e075-103">Optimize build performance for solution</span></span>

<span data-ttu-id="0e075-104">Visual Studio 2017 15,8 veya daha sonra bir menü öğesini ekleyin: **Derleme** > **ASP.NET derleme** > **çözüm derleme performansını iyileştirme**.</span><span class="sxs-lookup"><span data-stu-id="0e075-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![Yeni menü öğesinin ekran görüntüsü](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="0e075-106">ASP.NET, ASP.NET projesi ile bir kopyasını derleyici taşıyan anlamına gelir. çalışma zamanında görünümlerini derler.</span><span class="sxs-lookup"><span data-stu-id="0e075-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="0e075-107">Visual Studio'nun kopyalama, kopyalama derleyicinin eşleşmediğinde ancak bir geliştirici makinesinde yapı performansını Artımlı derleme başına 1-3 saniye bazında etkilenir.</span><span class="sxs-lookup"><span data-stu-id="0e075-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="0e075-108">Bu özellik, yalnızca artımlı derlemeleri genellikle hızlandıran projenizin kopyasını Visual Studio'nun eşleştirmek için derleyicinin güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="0e075-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="0e075-109">**ASP.NET Framework 4.7.1 uygulanabilir veya daha sonra yalnızca projeleri, ASP.NET Core için geçerli değildir.**</span><span class="sxs-lookup"><span data-stu-id="0e075-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
