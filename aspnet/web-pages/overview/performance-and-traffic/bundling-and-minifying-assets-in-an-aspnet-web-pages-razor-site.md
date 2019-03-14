---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: Paketleme ve küçültme varlıklar bir ASP.NET Web sayfaları (Razor) sitesinde | Microsoft Docs
author: microsoft
description: Paketleme ve küçültme sitenizi daha hızlı hale getirmek için yolları açıklanmıştır. Paketleme sağlar, birden fazla JavaScript (.js) dosyası veya birden çok geçişli stil sayfası (...) birleştirme
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 7d2cb2fe311b8aff20bfb378b329286701ed5b7d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076638"
---
<a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="cb364-104">ASP.NET Web Sayfaları (Razor) Sitesinde Varlıkları Paketleme ve Küçültme</span><span class="sxs-lookup"><span data-stu-id="cb364-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="cb364-105">tarafından [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="cb364-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="cb364-106">Paketleme ve küçültme sitenizi daha hızlı hale getirmek için yolları açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cb364-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="cb364-107">Paketleme birden çok JavaScript birleştirmek sağlar (*.js*) dosyaları veya birden çok geçişli stil sayfası (*.css*) bir birim yerine teker teker olarak indirilebilir dosyalar.</span><span class="sxs-lookup"><span data-stu-id="cb364-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="cb364-108">Küçültme, boşluk sıkıştırır ve diğer türleri küçük olarak indirilen dosyaları bir mümkün hale getirmek için sıkıştırma gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="cb364-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="cb364-109">ASP.NET Web Pages 2 RC sürümü gereken öğeleri içeren paket henüz Microsoft Webmatrix'te kullanılabilir olmadığı için paketleme ve küçültme desteklemez.</span><span class="sxs-lookup"><span data-stu-id="cb364-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="cb364-110">Bu rahatsızlıktan dolayı özür dileriz.</span><span class="sxs-lookup"><span data-stu-id="cb364-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="cb364-111">Paket, ASP.NET Web sayfaları 2 ve WebMatrix 2 son sürümünde kullanılabilir olması beklenir.</span><span class="sxs-lookup"><span data-stu-id="cb364-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
