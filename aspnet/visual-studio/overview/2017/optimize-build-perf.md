---
uid: visual-studio/overview/2017/optimize-build-perf
title: Çözüm için derleme performansını iyileştirme
author: AngelosP
description: Çözüm için derleme performansını iyileştirme
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622642"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="90b3a-103">Çözüm için derleme performansını iyileştirme</span><span class="sxs-lookup"><span data-stu-id="90b3a-103">Optimize build performance for solution</span></span>

<span data-ttu-id="90b3a-104">Visual Studio 2017 15,8 veya üzeri bir menü öğesi içerir: **çözüm Için derleme performansını iyileştirmek** \*\* > derleme > \*\* **ASP.NET derlemesi** .</span><span class="sxs-lookup"><span data-stu-id="90b3a-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![Yeni menü öğesinin ekran görüntüsü](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="90b3a-106">ASP.NET, görünümlerini çalışma zamanında derler, yani bir ASP.NET projesi derleyicinin kopyasıyla birlikte taşınır.</span><span class="sxs-lookup"><span data-stu-id="90b3a-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="90b3a-107">Ancak, derleyicinin kopyası Visual Studio 'nun kopyasıyla eşleşmediği zaman, derleme performansı Artımlı derleme başına 1-3 saniye sırasıyla etkilenir.</span><span class="sxs-lookup"><span data-stu-id="90b3a-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="90b3a-108">Bu özellik, projenin derleyicisinin kopyasını Visual Studio ile eşleşecek şekilde güncelleştirir, genellikle artımlı derlemeleri hızlandırır.</span><span class="sxs-lookup"><span data-stu-id="90b3a-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="90b3a-109">**Bu yalnızca ASP.NET Framework 4.7.1 veya sonraki projeler için geçerlidir, ASP.NET Core için geçerli değildir.**</span><span class="sxs-lookup"><span data-stu-id="90b3a-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
