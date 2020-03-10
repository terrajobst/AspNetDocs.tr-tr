---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: 'Nasıl yapılır: MVC uygulaması için özel HTML Yardımcısı oluşturma? | Microsoft Docs'
author: rick-anderson
description: Bu videoda, bir MVC uygulamasında standart kümesinde kullanılamayan özel bir HtmlHelper oluşturmayı gösterir. Birincisi, örnek bir MVC Applica...
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559047"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="ce496-105">Nasıl yapılır: MVC uygulaması için özel HTML Yardımcısı oluşturma?</span><span class="sxs-lookup"><span data-stu-id="ce496-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>

<span data-ttu-id="ce496-106">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="ce496-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="ce496-107">Bu videoda, bir MVC uygulamasında standart kümesinde kullanılamayan özel bir HtmlHelper oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ce496-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="ce496-108">İlk olarak, özel HtmlHelper 'ı test etmek için bir demo denetleyicisi ve görünümüyle örnek bir MVC uygulaması oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ce496-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="ce496-109">Daha sonra, özel HtmlHelper uygulamasını temsil eden bir genişletme yöntemi olan bir ortak işlevle bir modül oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ce496-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="ce496-110">Özel yardımcı, sayfada `<img>` Etiketler oluşturmak ve görüntü etiketi için ID, URL ve alt metin gibi birkaç gelen parametreyi alır.</span><span class="sxs-lookup"><span data-stu-id="ce496-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="ce496-111">Daha sonra, tamamlanan `<img>` etiketi belirtilen bilgilerle döndürmek için bu mantık işlevine eklenir.</span><span class="sxs-lookup"><span data-stu-id="ce496-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="ce496-112">Ardından, bir görüntüyü göstermek için demo sayfasında özel HtmlHelper kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ce496-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="ce496-113">Son olarak, özel HtmlHelper, farklı `<img>` etiketleri daha kolay bir şekilde oluşturmak için esneklik sağlayan birden çok Oluşturucu geçersiz kılma işlemleri içerecek şekilde genişletilir.</span><span class="sxs-lookup"><span data-stu-id="ce496-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="ce496-114">&#9654;Videoyu izleyin (18 dakika)</span><span class="sxs-lookup"><span data-stu-id="ce496-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="ce496-115">[Önceki](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [İleri](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="ce496-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>
