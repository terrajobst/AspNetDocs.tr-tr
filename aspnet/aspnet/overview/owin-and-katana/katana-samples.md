---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana örnekleri | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584562"
---
# <a name="katana-samples"></a><span data-ttu-id="97db8-102">Katana Örnekleri</span><span class="sxs-lookup"><span data-stu-id="97db8-102">Katana Samples</span></span>

<span data-ttu-id="97db8-103">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="97db8-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="97db8-104">Katana Örnekleri</span><span class="sxs-lookup"><span data-stu-id="97db8-104">Katana Samples</span></span>

<span data-ttu-id="97db8-105">**ASP.net rotalar örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="97db8-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="97db8-106">Bazı uygulamalarda, Asp.Net Route tablosundaki owın bileşenlerini OWıN olmayan bileşenlerle yan yana bağlamak isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="97db8-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="97db8-107">Bu örnek, Microsoft. Owin. Host. SystemWeb tarafından sunulan RouteCollection genişletme yöntemlerinin MapOwinPath ve MapOwinRoute 'ın nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="97db8-108">**Dallanma Işlem hatları örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="97db8-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="97db8-109">OWıN istek işleme ardışık düzenleri doğrusal olması gerekmez, istekleri farklı yollarla işlemek için dallandıramazlar.</span><span class="sxs-lookup"><span data-stu-id="97db8-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="97db8-110">Bu örnek, istek yollarına veya üst bilgiler gibi diğer istek verilerine göre dallanma işlem hattının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="97db8-111">Bu bileşenler, Microsoft. Owin. Mapping NuGet paketinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="97db8-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="97db8-112">**Özel sunucu örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="97db8-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="97db8-113">Kendi kendine barındırma sırasında özel bir OWıN sunucusunun nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="97db8-114">**Gömülü örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="97db8-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="97db8-115">Bazı OWIN sunucuları kendi işleminizin içinde çalıştırılabilir (&quot;kendi kendine barındırılan&quot;).</span><span class="sxs-lookup"><span data-stu-id="97db8-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="97db8-116">Bu örnek, Microsoft. Owin. Hosting NuGet paketi tarafından sunulan araçları kullanarak OWıN uygulamasının nasıl başlatılacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="97db8-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="97db8-117">**HelloWorld örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="97db8-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="97db8-118">OWIN, çeşitli sunucular arasında uygulama taşınabilirliği sağlayan bir HTTP Sunucusu API soyutlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="97db8-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="97db8-119">Bu örnek, ham OWıN soyutlaması etrafında bazı **basit sarmalayıcıları** kullanarak bir Merhaba Dünya uygulamasının nasıl yazılacağını ve ASP.NET gibi bir Web sunucusunda çalıştırmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="97db8-120">**Merhaba Dünya RAW OWIN örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="97db8-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="97db8-121">Bu örnek, **Ham** owın soyutlaması kullanılarak bir Merhaba Dünya uygulamasının nasıl yazılacağını ve ASP.NET gibi bir Web sunucusunda nasıl çalıştırılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="97db8-122">**SignalR örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="97db8-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="97db8-123">OWıN/Katana kullanarak SignalR 'nin nasıl kendine barındırılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="97db8-124">Self-hosting SignalR hakkında daha fazla bilgi için bkz. [öğretici: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="97db8-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="97db8-125">**Statik dosyalar örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="97db8-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="97db8-126">OWıN/Katana kullanarak statik dosyalar için HTTP isteklerinin nasıl destekleyeceği gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="97db8-127">**Web apı** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="97db8-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="97db8-128">Bu örnek, OWıN 'ın IIS 'de nasıl barındıralınacağını ve OWıN ardışık düzenine Web API 'SI nasıl ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="97db8-129">**Web yuvası örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="97db8-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="97db8-130">[System .net. WebSockets. WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) sınıfını kullanarak Owin Içindeki Web yuvalarını desteklemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="97db8-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
