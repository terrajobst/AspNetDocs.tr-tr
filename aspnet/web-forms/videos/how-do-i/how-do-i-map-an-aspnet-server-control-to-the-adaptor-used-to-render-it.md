---
uid: web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
title: '[Nasıl yapılır:] ASP.NET sunucu denetimini, Işlemek için kullanılan bağdaştırıcıya eşleyin | Microsoft Docs'
author: rick-anderson
description: Bu videoda, bir denetim bağdaştırıcısının, ASP.NET sunucu denetimine yönelik farklı işleyiciler sağlamak için, aslında c...
ms.author: riande
ms.date: 06/19/2008
ms.assetid: d4b498ef-8e1c-4fa2-9c35-1f32f20bb9b7
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
msc.type: video
ms.openlocfilehash: 757c90fac3345b448513fb4c7cd946a3d10f3f89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585815"
---
# <a name="how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it"></a><span data-ttu-id="2e684-103">[Nasıl yapılır:] Bir ASP.NET sunucu denetimini, onu Işlemek için kullanılan bağdaştırıcıya eşleyin</span><span class="sxs-lookup"><span data-stu-id="2e684-103">[How Do I:] Map an ASP.NET Server Control to the Adaptor Used to Render It</span></span>

<span data-ttu-id="2e684-104">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="2e684-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="2e684-105">Bu videoda, bir denetim bağdaştırıcısının, denetimin kendisini değiştirmeden bir ASP.NET sunucu denetimi için farklı işleyiciler sağlamak üzere nasıl kullanılacağı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2e684-105">In this video Chris Pels will show how to use a control adaptor to provide different renderings for an ASP.NET server control without actually changing the control itself.</span></span> <span data-ttu-id="2e684-106">Bu videoda, bir ASP.NET sel liste denetimi, her liste öğesini geleneksel UL öğeleri yerine DıV öğeleri kullanılarak yatay olarak görüntüleyecek şekilde uyarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2e684-106">In this video, an ASP.NET BulletList control will be adapted to display each list item horizontally using DIV elements instead of the traditional UL elements.</span></span> <span data-ttu-id="2e684-107">İlk olarak, WebControlAdaptor ' ı devralan bir sınıf oluşturma ve ardından yeni liste biçimini oluşturmak için kodu uygulama bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="2e684-107">First, see how to create a class that inherits WebControlAdaptor and then implements the code to render the new list format.</span></span> <span data-ttu-id="2e684-108">Daha sonra, yeni denetim bağdaştırıcısını. browser tanım dosyasındaki ASP.NET sunucu denetimiyle eşlemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e684-108">Next, learn how to map the new control adaptor to the ASP.NET server control in the .browser definition file.</span></span> <span data-ttu-id="2e684-109">Daha sonra bir Web sitesindeki sayfalarda yeni denetim bağdaştırıcısını nasıl kullanacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e684-109">Then see how to use the new control adaptor on pages in a web site.</span></span> <span data-ttu-id="2e684-110">Son olarak, bir denetim bağdaştırıcısının tüm tarayıcılarla veya belirli tarayıcı türleriyle nasıl ilişkilendirilebilen hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2e684-110">Finally, learn how a control adaptor can be associated with either all browsers or specific types of browsers.</span></span>

[<span data-ttu-id="2e684-111">&#9654;Videoyu izleyin (23 dakika)</span><span class="sxs-lookup"><span data-stu-id="2e684-111">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it)
