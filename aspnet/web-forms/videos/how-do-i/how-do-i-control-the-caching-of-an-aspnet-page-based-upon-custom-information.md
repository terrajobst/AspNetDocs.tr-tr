---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[Nasıl yapılır:] Özel bilgileri temel alan bir ASP.NET sayfasının önbelleğe alınmasını denetleme | Microsoft Docs'
author: rick-anderson
description: Bu videoda, kemal 'in özel bilgilere göre bir ASP.NET sayfasını önbelleğe alma ölçütlerini nasıl denetleneceği gösterilmektedir. Örnek bir sayfa oluşturulur ve sonra O...
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624735"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="7f2f4-104">[Nasıl yapılır:] Özel bilgileri temel alan bir ASP.NET sayfasının önbelleğe alınmasını denetleme</span><span class="sxs-lookup"><span data-stu-id="7f2f4-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="7f2f4-105">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="7f2f4-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="7f2f4-106">Bu videoda, kemal 'in özel bilgilere göre bir ASP.NET sayfasını önbelleğe alma ölçütlerini nasıl denetleneceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7f2f4-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="7f2f4-107">Örnek bir sayfa oluşturulur ve ardından OutputCache yönergesi özel bir değer içeren VaryByCustom özniteliğiyle birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f2f4-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="7f2f4-108">Ardından, GetVaryCustomByString () yöntemi, özel özniteliğin işlenmesini sağlayan global. asax modülünde geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="7f2f4-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="7f2f4-109">Bu yöntemde, sayfanın önbelleğe alınmış sürümünü benzersiz bir şekilde tanımlayan bir dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="7f2f4-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="7f2f4-110">Son olarak, özel bir değer kullanarak bir Web sitesi için çeşitli yollarla nasıl önbelleğe alınacağını gösteren bir tartışma vardır.</span><span class="sxs-lookup"><span data-stu-id="7f2f4-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="7f2f4-111">&#9654;Videoyu izleyin (12 dakika)</span><span class="sxs-lookup"><span data-stu-id="7f2f4-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
