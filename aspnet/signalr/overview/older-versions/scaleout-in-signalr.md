---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: SignalR 1. x 'te ölçek 'e giriş | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 04/29/2013
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9bad72d31a0ebc491910ebb128b3b3a7fb537958
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536570"
---
# <a name="introduction-to-scaleout-in-signalr-1x"></a>SignalR 1.x Sürümünde Ölçek Genişletmeye Giriş

, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Genel olarak, bir Web uygulamasını ölçeklendirmenin iki yolu vardır: *ölçeği artırma* ve *genişletme*.

- Ölçeği artırma, daha fazla RAM, CPU vb. daha büyük bir sunucu (veya daha büyük bir VM) kullanmak anlamına gelir.
- Ölçeği genişletme, yükü işlemek için daha fazla sunucu ekleme anlamına gelir.

Ölçeklendirme sorunu, makinenin boyutuna göre hızlıca bir sınıra ulaşmanıza neden olur. Bunun ötesinde ölçeği ölçeklendirmeniz gerekir. Ancak, ölçeğini ölçeklendirirseniz, istemciler farklı sunuculara yönlendirilebilir. Bir sunucuya bağlı olan istemci, başka bir sunucudan gönderilen iletileri almaz.

![](scaleout-in-signalr/_static/image1.png)

Bir çözüm, *geri düzlemi*adlı bir bileşen kullanarak iletileri sunucular arasında iletmektir. Bir sırt etkin olduğunda, her bir uygulama örneği geri düzleme iletiler gönderir ve geri düzlemi bunları diğer uygulama örneklerine iletir. (Elektronik olarak, bir geri düzlemi bir paralel bağlayıcılar grubudur. Benzerleme vurguladı tarafından bir SignalR arka düzlemi birden çok sunucuyu bağlar.)

![](scaleout-in-signalr/_static/image2.png)

SignalR Şu anda üç arka düzme sunmaktadır:

- **Azure Service Bus**. Service Bus, bileşenlerin gevşek olarak bağlanmış bir şekilde ileti göndermesini sağlayan bir mesajlaşma altyapısıdır.
- **Redsıs**. Redsıs, bellek içi anahtar-değer deposudur. Redsıs, ileti göndermek için bir yayımla/abone ol ("pub/Sub") modelini destekler.
- **SQL Server**. SQL Server arka düzlemi, iletileri SQL tablolarına yazar. Geri düzlemi verimli mesajlaşma için Hizmet Aracısı kullanır. Ancak, Hizmet Aracısı etkinleştirilmemişse da bu da işe yarar.

Uygulamanızı Azure 'da dağıtırsanız, Azure Service Bus arka düzlemi kullanmayı göz önünde bulundurun. Kendi sunucu grubunuza dağıtıyorsanız, SQL Server veya Redsıs arka düzlemleri göz önünde bulundurun.

Aşağıdaki konularda her bir arka düzlem için adım adım öğreticiler yer verilmiştir:

- [Azure Service Bus ile SignalR Ölçeğini Genişletme](scaleout-with-windows-azure-service-bus.md)
- [Redis ile SignalR Ölçeğini Genişletme](scaleout-with-redis.md)
- [SQL Server ile SignalR Ölçeğini Genişletme](scaleout-with-sql-server.md)

## <a name="implementation"></a>Uygulama

SignalR 'de, her ileti bir ileti veri yolu aracılığıyla gönderilir. İleti veri yolu, yayımlama/abone olma soyutlaması sağlayan [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) arabirimini uygular. Arka düzlemler, varsayılan **IMessageBus 'ı** bu geri düzlemi için tasarlanan bir veri yolu ile değiştirerek çalışır. Örneğin, Redsıs için ileti veri yolu [Redismessagebus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)' dır ve ileti göndermek ve almak için redsıs [pub/Sub](http://redis.io/topics/pubsub) mekanizmasını kullanır.

Her sunucu örneği, veri yolu aracılığıyla geri düzleme bağlanır. Bir ileti gönderildiğinde, geri düzlemi ' ne gider ve geri düzlemi onu her sunucuya gönderir. Bir sunucu arkadüzleden bir ileti aldığında, iletiyi yerel önbelleğine koyar. Sunucu daha sonra istemcilere yerel önbelleğinden iletiler gönderir.

Her istemci bağlantısı için, istemcinin ileti akışını okurken ilerleme durumu bir imleç kullanılarak izlenir. (İmleç ileti akışındaki bir konumu temsil eder.) Bir istemci bağlantısını keser ve sonra yeniden bağlanırsa, istemcinin imleç değerinden sonra gelen iletiler için veri yoluna sorar. Bir bağlantı [uzun yoklama](../getting-started/introduction-to-signalr.md#transports)kullandığında aynı şey olur. Uzun bir yoklama isteği tamamlandıktan sonra, istemci yeni bir bağlantı açar ve imlece sonra gelen iletileri ister.

Bir istemci, yeniden bağlantı sırasında farklı bir sunucuya yönlendirilse bile imleç mekanizması işe yarar. Geri düzlemi, tüm sunucuların farkındadır ve bir istemcinin hangi sunucuya bağlanacağını fark etmez.

## <a name="limitations"></a>Sınırlamalar

Bir geri düzlemi kullanarak, en fazla ileti işleme, istemciler doğrudan tek bir sunucu düğümüne konuştuğu kadar düşüktür. Bunun nedeni, geri düzlemi her düğüme her bir düğüme ilettiğinden, geri düzlemi bir performans sorunu haline gelebilir. Bu sınırlamanın bir sorun olup olmadığı, uygulamaya bağlıdır. Örneğin, bazı tipik bir SignalR senaryosu aşağıda verilmiştir:

- [Sunucu yayını](tutorial-server-broadcast-with-aspnet-signalr.md) (örneğin, hisse senedi bandı): sunucu iletilerin gönderilme hızını denetlemediğinden, bu senaryo Için geri düzler iyi çalışır.
- [İstemciden istemciye](tutorial-getting-started-with-signalr.md) (ör. sohbet): Bu senaryoda, iletilerin sayısı istemci sayısıyla ölçeklenirken, arka uç bir performans sorunu olabilir; diğer bir deyişle, daha fazla istemci katılırken ileti hızının orantılı olarak büyümesi.
- [Yüksek frekanslı gerçek zamanlı](tutorial-high-frequency-realtime-with-signalr.md) (örn. gerçek zamanlı Oyunlar): Bu senaryo için bir geri düzlem önerilmez.

## <a name="enabling-tracing-for-signalr-scaleout"></a>SignalR ölçeği Için Izlemeyi etkinleştirme

Arka düzlemler için izlemeyi etkinleştirmek üzere aşağıdaki bölümleri Web. config dosyasına kök **yapılandırma** öğesinin altına ekleyin:

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
