---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[Nasıl yapılır:]  HTTP üstbilgisindeki bilgileri temel alan bir ASP.NET sayfasını önbelleğe alma | Microsoft Docs'
author: rick-anderson
description: Bu videoda, kemal 'in, sayfanın HTTP üstbilgisindeki bilgilere göre ASP.NET çıktı önbelleğinde nasıl saklanacağı gösterilmektedir. İlk olarak, olası HTTP hea...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624973"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="742d2-104">[Nasıl yapılır:]  HTTP üstbilgisindeki bilgileri temel alan bir ASP.NET sayfasını önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="742d2-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>

<span data-ttu-id="742d2-105">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="742d2-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="742d2-106">Bu videoda, kemal 'in, sayfanın HTTP üstbilgisindeki bilgilere göre ASP.NET çıktı önbelleğinde nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="742d2-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="742d2-107">İlk olarak, olası HTTP üst bilgisi değerleri gözden geçirilir.</span><span class="sxs-lookup"><span data-stu-id="742d2-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="742d2-108">Ardından, örnek bir sayfa oluşturulur ve ardından OutputCache yönergesi, kullanıcı tarayıcısının diline bağlı olarak önbelleğe alma işlemini denetlemek için bir "Accept-Language", bir HTTP üst bilgisi değeri içeren VaryByHeader özniteliğiyle birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="742d2-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="742d2-109">Örnek sayfa, Ingilizce olarak ayarlanan ve ardından FireFox 'ta Fransızca 'yı kullanacak şekilde ayarlanan IE 'de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="742d2-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="742d2-110">Son olarak, önbellek tanımını Web. config dosyasındaki bir CacheProfile taşıma seçeneği ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="742d2-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="742d2-111">&#9654;Videoyu izleyin (12 dakika)</span><span class="sxs-lookup"><span data-stu-id="742d2-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
