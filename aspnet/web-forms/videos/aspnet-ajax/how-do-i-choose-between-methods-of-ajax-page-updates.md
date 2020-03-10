---
uid: web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
title: '[Nasıl yapılır:] AJAX sayfa güncelleştirme yöntemleri arasında seçim yapılsın mı? | Microsoft Docs'
author: JoeStagner
description: Bu videoda Joe Stagner, bir ASP.NET uygulamasında AJAX stili sayfa güncelleştirmeleri gerçekleştirmenin iki birincil yöntemini karşılaştırır. İlk yöntem bir upd kullanmaktır...
ms.author: riande
ms.date: 07/09/2007
ms.assetid: a5e33a7d-ccb2-483f-a955-3d39f72ba4ec
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
msc.type: video
ms.openlocfilehash: 56e3ebfbe0b5af4234791136725de79e38171cc1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523669"
---
# <a name="how-do-i-choose-between-methods-of-ajax-page-updates"></a><span data-ttu-id="9f14e-105">[Nasıl yapılır:] AJAX sayfa güncelleştirme yöntemleri arasında seçim yapılsın mı?</span><span class="sxs-lookup"><span data-stu-id="9f14e-105">[How Do I:] Choose Between Methods of AJAX Page Updates?</span></span>

<span data-ttu-id="9f14e-106">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="9f14e-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="9f14e-107">Bu videoda Joe Stagner, bir ASP.NET uygulamasında AJAX stili sayfa güncelleştirmeleri gerçekleştirmenin iki birincil yöntemini karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="9f14e-107">In this video Joe Stagner compares the two primary methods of performing AJAX-style page updates in an ASP.NET application.</span></span> <span data-ttu-id="9f14e-108">İlk yöntem, istemci tarafında veya sunucu tarafında herhangi bir ek kodun yazılması gereken bir UpdatePanel kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="9f14e-108">The first method is to use an UpdatePanel, where no additional code needs to be written on either the client side or the server side.</span></span> <span data-ttu-id="9f14e-109">UpdatePanel kullanmanın avantajı, her şeyin otomatik olarak çalışmadır.</span><span class="sxs-lookup"><span data-stu-id="9f14e-109">The benefit of using the UpdatePanel is that everything works automatically.</span></span> <span data-ttu-id="9f14e-110">Ceza, istemci, AJAX isteğine ve yanıtına çok fazla veri eklenmesini gerektirir ve sunucuda tam sayfa yaşam döngüsünün yürütülmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9f14e-110">The penalty is that at the client it requires a lot of data to be included in the AJAX request and response, and at the server it requires a full page lifecycle to be executed.</span></span> <span data-ttu-id="9f14e-111">İkinci yöntem, ek kodun hem istemci tarafında hem de sunucu tarafında yazılması gereken ağ geri çağırmaları kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="9f14e-111">The second method is to use network callbacks, where additional code needs to be written on both the client side and the server side.</span></span> <span data-ttu-id="9f14e-112">Ağ geri çağırmaları kullanmanın avantajı, istemci, AJAX isteğine ve yanıtına çok az verinin dahil edilmesini gerektirir ve sunucuda yalnızca çağrılan hizmet yönteminin yürütülmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f14e-112">The benefit of using network callbacks is that at the client it requires very little data to be included in the AJAX request and response, and at the server it requires only the called service method to be executed.</span></span> <span data-ttu-id="9f14e-113">Sızlığı, gerekli kodu yazmak için gereken zaman ve çabadır.</span><span class="sxs-lookup"><span data-stu-id="9f14e-113">The penality is the time and effort it takes to write the necessary code.</span></span> <span data-ttu-id="9f14e-114">Ali, AJAX stili sayfa güncelleştirmelerinin iki birincil yöntemi arasında seçim yaparken göz önünde bulundurmanız gereken şeyi ele alarak videoyu yerine eriyor.</span><span class="sxs-lookup"><span data-stu-id="9f14e-114">Joe concludes the video by discussing what you should consider when choosing between the two primary methods of AJAX-style page updates.</span></span> <span data-ttu-id="9f14e-115">(Bu videoda, ASP.NET AJAX videosunu kullanmaya [nasıl başladım](how-do-i-get-started-with-aspnet-ajax.md) ve [ASP.NET AJAX videosu Ile Istemci tarafı ağ geri çağırmaları nasıl](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) yaparım?) kodu kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9f14e-115">(This video uses the code from the [How Do I Get Started with ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) video and the [How Do I Make Client-Side Network Callbacks with ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) video.)</span></span>

[<span data-ttu-id="9f14e-116">&#9654;Videoyu izleyin (11 dakika)</span><span class="sxs-lookup"><span data-stu-id="9f14e-116">&#9654; Watch video (11 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-choose-between-methods-of-ajax-page-updates)

> [!div class="step-by-step"]
> <span data-ttu-id="9f14e-117">[Önceki](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
> [İleri](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span><span class="sxs-lookup"><span data-stu-id="9f14e-117">[Previous](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
[Next](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span></span>
