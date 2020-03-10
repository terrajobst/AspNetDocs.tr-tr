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
# <a name="katana-samples"></a>Katana Örnekleri

[Microsoft](https://github.com/microsoft) tarafından

## <a name="katana-samples"></a>Katana Örnekleri

**ASP.net rotalar örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
Bazı uygulamalarda, Asp.Net Route tablosundaki owın bileşenlerini OWıN olmayan bileşenlerle yan yana bağlamak isteyeceksiniz. Bu örnek, Microsoft. Owin. Host. SystemWeb tarafından sunulan RouteCollection genişletme yöntemlerinin MapOwinPath ve MapOwinRoute 'ın nasıl kullanılacağını gösterir.

**Dallanma Işlem hatları örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWıN istek işleme ardışık düzenleri doğrusal olması gerekmez, istekleri farklı yollarla işlemek için dallandıramazlar. Bu örnek, istek yollarına veya üst bilgiler gibi diğer istek verilerine göre dallanma işlem hattının nasıl oluşturulacağını gösterir. Bu bileşenler, Microsoft. Owin. Mapping NuGet paketinde bulunur.

**Özel sunucu örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
Kendi kendine barındırma sırasında özel bir OWıN sunucusunun nasıl kullanılacağını gösterir.

**Gömülü örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
Bazı OWIN sunucuları kendi işleminizin içinde çalıştırılabilir (&quot;kendi kendine barındırılan&quot;). Bu örnek, Microsoft. Owin. Hosting NuGet paketi tarafından sunulan araçları kullanarak OWıN uygulamasının nasıl başlatılacağını göstermektedir.

**HelloWorld örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN, çeşitli sunucular arasında uygulama taşınabilirliği sağlayan bir HTTP Sunucusu API soyutlamasıdır. Bu örnek, ham OWıN soyutlaması etrafında bazı **basit sarmalayıcıları** kullanarak bir Merhaba Dünya uygulamasının nasıl yazılacağını ve ASP.NET gibi bir Web sunucusunda çalıştırmayı gösterir.

**Merhaba Dünya RAW OWIN örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
Bu örnek, **Ham** owın soyutlaması kullanılarak bir Merhaba Dünya uygulamasının nasıl yazılacağını ve ASP.NET gibi bir Web sunucusunda nasıl çalıştırılacağını gösterir.

**SignalR örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
OWıN/Katana kullanarak SignalR 'nin nasıl kendine barındırılacağını gösterir. Self-hosting SignalR hakkında daha fazla bilgi için bkz. [öğretici: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

**Statik dosyalar örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
OWıN/Katana kullanarak statik dosyalar için HTTP isteklerinin nasıl destekleyeceği gösterir.

**Web apı** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
Bu örnek, OWıN 'ın IIS 'de nasıl barındıralınacağını ve OWıN ardışık düzenine Web API 'SI nasıl ekleneceğini gösterir.

**Web yuvası örnek** | [kaynak kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
[System .net. WebSockets. WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) sınıfını kullanarak Owin Içindeki Web yuvalarını desteklemeyi gösterir.
