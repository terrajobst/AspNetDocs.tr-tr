---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: Bir ASP.NET Web Pages (Razor) sitesindeki varlıkları paketleme ve küçültme | Microsoft Docs
author: microsoft
description: Paketleme ve küçültme, sitenizi daha hızlı hale getirmek için kullanabileceğiniz yollardır. Paketleme, birden çok JavaScript (. js) dosyasını veya birden çok geçişli stil sayfasını (...) birleştirmenizi sağlar.
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 5e42111ad71ec65581e56c73822e23ecd5fcbd58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635711"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="0246b-104">ASP.NET Web Sayfaları (Razor) Sitesinde Varlıkları Paketleme ve Küçültme</span><span class="sxs-lookup"><span data-stu-id="0246b-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="0246b-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="0246b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0246b-106">Paketleme ve küçültme, sitenizi daha hızlı hale getirmek için kullanabileceğiniz yollardır.</span><span class="sxs-lookup"><span data-stu-id="0246b-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="0246b-107">Paketleme, birden çok JavaScript ( *. js*) dosyasını veya birden çok geçişli stil sayfası ( *. css*) dosyasını birleştirerek tek seferde bir birim olarak indirilebilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0246b-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="0246b-108">Minınterout, daha fazla bilgi edinmek için boşluk kullanır ve indirilen dosyaları mümkün olduğunca küçük hale getirmek için diğer sıkıştırma türlerini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="0246b-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="0246b-109">ASP.NET Web Pages 2 ' nin RC sürümü, gerekli öğeleri içeren paket, Microsoft WebMatrix 'te henüz kullanılamadığından paketleme ve küçültmeye yönelik desteği desteklemez.</span><span class="sxs-lookup"><span data-stu-id="0246b-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="0246b-110">Bu sorundan dolayı özür dileriz.</span><span class="sxs-lookup"><span data-stu-id="0246b-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="0246b-111">ASP.NET Web Pages 2 ve WebMatrix 2 ' nin son sürümünde paketin kullanılabilir olması beklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="0246b-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
