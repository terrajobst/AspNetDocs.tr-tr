---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: "[Nasıl yapılır:] ASP.NET sayfasında HTML 'yi değiştirmek için, yanıt. Filter özelliğini kullanın | Microsoft Docs"
author: rick-anderson
description: Bu videoda Chris Pters, bir sayfaya gönderilen HTML 'yi kesme ve değiştirme için, yanıt. Filter özelliğinin nasıl kullanılacağını gösterir. İlk olarak, bir örnek sayfa oluşturulur...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602818"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="11424-104">[Nasıl yapılır:] ASP.NET sayfasında HTML 'yi değiştirmek için, yanıt. Filter özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="11424-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>

<span data-ttu-id="11424-105">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="11424-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="11424-106">Bu videoda Chris Pters, bir sayfaya gönderilen HTML 'yi kesme ve değiştirme için, yanıt. Filter özelliğinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="11424-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="11424-107">İlk olarak, bir örnek sayfa, bazı basit metinle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="11424-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="11424-108">Daha sonra, geçerli akışın Kullanıcı tarayıcısına gönderilmesi için değiştirme akışı görevi gören özel bir akış sınıfı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="11424-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="11424-109">Bu özel akış sınıfında, sayfanın içeriği akıştan alınır, değiştirilir ve yanıt akışına yazılır.</span><span class="sxs-lookup"><span data-stu-id="11424-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="11424-110">Bu özel akış sınıfında, yazma yöntemi temel yanıt akışındaki HTML 'yi değiştirecek şekilde özelleştirildiğinden kullanıcının tarayıcısına ne gönderileceğini değiştirmiş olur.</span><span class="sxs-lookup"><span data-stu-id="11424-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="11424-111">Son olarak, yeni Stream sınıfı,\_sayfadaki yükleme olayındaki Response. Filter özelliğine atanır, böylece sayfa içeriğini değiştirme mekanizması sağlanır.</span><span class="sxs-lookup"><span data-stu-id="11424-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="11424-112">&#9654;Videoyu izleyin (13 dakika)</span><span class="sxs-lookup"><span data-stu-id="11424-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
