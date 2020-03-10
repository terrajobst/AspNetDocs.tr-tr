---
uid: web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
title: '[Nasıl yapılır:] Web hizmetlerini kullanarak kalıcı Iletişim deseninin uygulanması mı istiyorsunuz? | Microsoft Docs'
author: JoeStagner
description: Geleneksel bir Web sitesinde tarayıcı ve sunucu devam eden bir iletişim kurmaz, ancak yalnızca bir işlem gerçekleştiren kullanıcıya yanıt olarak iletişim kurar...
ms.author: riande
ms.date: 08/22/2007
ms.assetid: 424c06cd-6d61-43cd-a1f2-d1a6b62e47b1
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
msc.type: video
ms.openlocfilehash: de2eb281cd4bab46635af480ac2e8f07f60f1591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628753"
---
# <a name="how-do-i-implement-the-persistent-communications-pattern-using-web-services"></a><span data-ttu-id="5a11d-104">[Nasıl yapılır:] Web hizmetlerini kullanarak kalıcı Iletişim deseninin uygulanması mı istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="5a11d-104">[How Do I:] Implement the Persistent Communications Pattern using Web Services?</span></span>

<span data-ttu-id="5a11d-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="5a11d-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="5a11d-106">Geleneksel bir Web sitesinde tarayıcı ve sunucu devam eden bir iletişim bulundurmaz, ancak yalnızca kullanıcıya bir eylem gerçekleştirerek yanıt olarak iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="5a11d-106">In a traditional Web site the browser and the server do not maintain an ongoing communication, but communicate only in response to the user performing an action.</span></span> <span data-ttu-id="5a11d-107">Sayfanın uygulama kapsayıcısı haline geldiği modern bir Web sitesinde, tarayıcı ve sunucu için, bir eylem yapmadan, sayfa güncelleştirmelerinin gerçekleşebileceği bir iletişim sağlamak için avantaj sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="5a11d-107">In a modern Web site where the page becomes an application container, it can be advantageous for the browser and the server to maintain an ongoing communication so that page updates can occur without the user performing an action.</span></span> <span data-ttu-id="5a11d-108">Bu, AJAX için kalıcı Iletişim kalıbı olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="5a11d-108">This is known as the Persistent Communications Pattern for AJAX.</span></span> <span data-ttu-id="5a11d-109">ASP.NET AJAX, Web geliştiricilerinin kalıcı Iletişim modelini uygulaması için iki ana yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a11d-109">ASP.NET AJAX provides two main ways for Web developers to implement the Persistent Communications Pattern.</span></span> <span data-ttu-id="5a11d-110">Önceki bir videoda, uygulamanın temeli olarak ASP.NET AJAX UpdatePanel 'ın nasıl kullanılacağını gördük.</span><span class="sxs-lookup"><span data-stu-id="5a11d-110">In an earlier video we saw how to use the ASP.NET AJAX UpdatePanel as the basis of the implementation.</span></span> <span data-ttu-id="5a11d-111">Bu videoda, bir ASP.NET AJAX UpdatePanel gereksinimini ortadan kaldıran bir Web hizmetine JavaScrpt çağrısını kullanarak aynı deseninin nasıl uygulanacağını öğreniyoruz.</span><span class="sxs-lookup"><span data-stu-id="5a11d-111">In this video we learn how to implement the same pattern using a JavaScrpt call to a Web service, which removes the need for an ASP.NET AJAX UpdatePanel.</span></span>

[<span data-ttu-id="5a11d-112">&#9654;Videoyu izleyin (16 dakika)</span><span class="sxs-lookup"><span data-stu-id="5a11d-112">&#9654; Watch video (16 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-the-persistent-communications-pattern-using-web-services)

> [!div class="step-by-step"]
> <span data-ttu-id="5a11d-113">[Önceki](how-do-i-localize-an-aspnet-ajax-application.md)
> [İleri](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span><span class="sxs-lookup"><span data-stu-id="5a11d-113">[Previous](how-do-i-localize-an-aspnet-ajax-application.md)
[Next](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span></span>
