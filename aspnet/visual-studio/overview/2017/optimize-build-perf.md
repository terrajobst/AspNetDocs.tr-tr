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
# <a name="optimize-build-performance-for-solution"></a>Çözüm için derleme performansını iyileştirme

Visual Studio 2017 15,8 veya üzeri bir menü öğesi içerir: **çözüm Için derleme performansını iyileştirmek** ** > derleme > ** **ASP.NET derlemesi** .

![Yeni menü öğesinin ekran görüntüsü](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET, görünümlerini çalışma zamanında derler, yani bir ASP.NET projesi derleyicinin kopyasıyla birlikte taşınır. Ancak, derleyicinin kopyası Visual Studio 'nun kopyasıyla eşleşmediği zaman, derleme performansı Artımlı derleme başına 1-3 saniye sırasıyla etkilenir. Bu özellik, projenin derleyicisinin kopyasını Visual Studio ile eşleşecek şekilde güncelleştirir, genellikle artımlı derlemeleri hızlandırır.

**Bu yalnızca ASP.NET Framework 4.7.1 veya sonraki projeler için geçerlidir, ASP.NET Core için geçerli değildir.**
