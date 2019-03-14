---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: Bir ASP.NET MVC 5 uygulamasının yaşam döngüsü | Microsoft Docs
author: cephalin
description: Bir ASP.NET MVC 5 uygulamasının yaşam döngüsü grafikleri bir PDF belgesini indirin. Bu yaşam döngüsü belge MVC yaşam döngüsü üst düzey bir görünümünü sağlar bir...
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: 5523217ae5674ac4e5898a150f9e5f0ae3a70d26
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072630"
---
<a name="lifecycle-of-an-aspnet-mvc-5-application"></a><span data-ttu-id="99c35-104">Bir ASP.NET MVC 5 Uygulamasının Yaşam Döngüsü</span><span class="sxs-lookup"><span data-stu-id="99c35-104">Lifecycle of an ASP.NET MVC 5 Application</span></span>
====================
<span data-ttu-id="99c35-105">tarafından [Cephas Bağla](https://github.com/cephalin)</span><span class="sxs-lookup"><span data-stu-id="99c35-105">by [Cephas Lin](https://github.com/cephalin)</span></span>

[<span data-ttu-id="99c35-106">PDF belgesini indirin</span><span class="sxs-lookup"><span data-stu-id="99c35-106">Download PDF Document</span></span>](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

<span data-ttu-id="99c35-107">Burada HTTP almasını her ASP.NET MVC 5 uygulamasının yaşam döngüsü İstek HTTP yanıtı göndermeyi grafikleri istemciye bir PDF belgesini indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99c35-107">Here you can download a PDF document that charts the lifecycle of every ASP.NET MVC 5 application, from receiving the HTTP request to sending the HTTP response back to the client.</span></span> <span data-ttu-id="99c35-108">ASP.NET MVC Acemi olanlar için eğitim bir aracı hem de de olarak bir başvuru uygulaması belirli yönlerini detaya gitmek için ihtiyacınız olanlar için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="99c35-108">It is designed both as an educational tool for those who are new to ASP.NET MVC and also as a reference for those who need to drill into specific aspects of the application.</span></span> <span data-ttu-id="99c35-109">PDF belgesinin aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="99c35-109">The PDF document has the following features:</span></span>

- <span data-ttu-id="99c35-110">İlgili [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) MVC tümleştirir burada anlamanıza yardımcı olması için aşamaları [ASP.NET uygulama yaşam döngüsü](https://msdn.microsoft.com/library/bb470252.aspx).</span><span class="sxs-lookup"><span data-stu-id="99c35-110">Relevant [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) stages to help you understand where MVC integrates into the [ASP.NET application lifecycle](https://msdn.microsoft.com/library/bb470252.aspx).</span></span>
- <span data-ttu-id="99c35-111">Burada isteği işleme işlem hattı, her bir MVC uygulaması geçtiği ana aşamaları anlayabilmeniz MVC uygulama yaşam döngüsünün üst düzey bir görünüm.</span><span class="sxs-lookup"><span data-stu-id="99c35-111">A high-level view of the MVC application lifecycle, where you can understand the major stages that every MVC application passes through in the request processing pipeline.</span></span>  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- <span data-ttu-id="99c35-112">İstek işleme Ardışık düzenin ayrıntılara inmesi aşağı gösteren ayrıntılı görünüm.</span><span class="sxs-lookup"><span data-stu-id="99c35-112">A detail view that shows drills down into the details of the request processing pipeline.</span></span> <span data-ttu-id="99c35-113">Üst düzey Görünüm ve çeşitli aşamaları yaşam döngüleri ayrıntılarını nasıl toplanır görmek için ayrıntılı görünüm karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99c35-113">You can compare the high-level view and the detail view to see how the lifecycles details are collected into the various stages.</span></span> <span data-ttu-id="99c35-114">[PDF'yi indirin](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) daha büyük bir görmek için.</span><span class="sxs-lookup"><span data-stu-id="99c35-114">[Download PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) to see a larger view.</span></span>
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- <span data-ttu-id="99c35-115">Yerleştirme ve tüm geçersiz kılınabilir yöntemleri üzerinde bir amacı [denetleyicisi](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) istek işleme ardışık düzeninde nesne.</span><span class="sxs-lookup"><span data-stu-id="99c35-115">Placement and purpose of all overridable methods on the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) object in the request processing pipeline.</span></span> <span data-ttu-id="99c35-116">Olabilir veya herhangi bir yöntemi geçersiz kılmak için gerek olmayabilir, ancak uygulama yaşam döngüsü içindeki rollerine için istediğinize etkisi uygun yaşam döngüsü aşamasında kod yazmaya başlayabilmeniz için önceden anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="99c35-116">You may or may not have the need to override any one method, but it is important for you to understand their role in the application lifecycle so that you can write code at the appropriate life cycle stage for the effect you intend.</span></span>
- <span data-ttu-id="99c35-117">Akıl yukarı diyagramları gösteren nasıl her filtre türü (kimlik doğrulaması, yetkilendirme, eylem ve sonuç) çağrılır.</span><span class="sxs-lookup"><span data-stu-id="99c35-117">Blown-up diagrams showing how each of the filter types (authentication, authorization, action, and result) is invoked.</span></span>
- <span data-ttu-id="99c35-118">Ayrıntılar görünümünde her ilgi çekici bir kullanışlı bir makale veya blog bağlantı.</span><span class="sxs-lookup"><span data-stu-id="99c35-118">Link to a useful article or blog from each point of interest in the detail view.</span></span>


## <a name="next-steps"></a><span data-ttu-id="99c35-119">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="99c35-119">Next Steps</span></span>

<span data-ttu-id="99c35-120">Bu belge, gereksinimi karşılar mı?</span><span class="sxs-lookup"><span data-stu-id="99c35-120">Does this document meet your need?</span></span> <span data-ttu-id="99c35-121">Görüşleriniz bizim için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="99c35-121">We'd appreciate your feedback.</span></span> <span data-ttu-id="99c35-122">Uygulamanızda, ASP.NET MVC yaşam döngüsü üzerinde herhangi bir sorunuz varsa [Stackoverflow](http://stackoverflow.com/help) ve [ASP.NET MVC forumları](https://forums.asp.net/1146.aspx) istemek için mükemmel yerlerdir.</span><span class="sxs-lookup"><span data-stu-id="99c35-122">If you have any question on the ASP.NET MVC lifecycle in your application, [Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are great places to ask.</span></span> <span data-ttu-id="99c35-123">İzleyin [bana](https://twitter.com/Cephas_MSFT) my en yeni öğreticiler güncelleştirmeleri alabilmeniz için Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="99c35-123">Follow [me](https://twitter.com/Cephas_MSFT) on twitter so you can get updates on my latest tutorials.</span></span>