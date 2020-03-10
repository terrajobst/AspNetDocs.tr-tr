---
uid: signalr/overview/performance/scaleout-in-signalr
title: SignalR 'de ölçek 'e giriş | Microsoft Docs
author: bradygaster
description: Bu konuda kullanılan yazılım sürümleri, .NET 4,5 SignalR sürüm 2 ' nin önceki sürümleri hakkında bilgi Için bu konunun önceki sürümlerini Visual Studio 2013...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 7e781fc1-1c1f-45a8-bc1d-338e96dbe9c9
msc.legacyurl: /signalr/overview/performance/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14dc22f99a43b566903c59fb23b7d419350f4a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579235"
---
# <a name="introduction-to-scaleout-in-signalr"></a>SignalR’da Ölçek Genişletmeye Giriş

, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Bu konunun önceki sürümleri
>
> SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
>
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

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

Uygulamanızı Azure 'da dağıtırsanız, [Azure Redis Cache](https://azure.microsoft.com/services/cache/)kullanarak redsıs geri düzlemi kullanmayı göz önünde bulundurun. Kendi sunucu grubunuza dağıtıyorsanız, SQL Server veya Redsıs arka düzlemleri göz önünde bulundurun.

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

- [Sunucu yayını](../getting-started/tutorial-server-broadcast-with-signalr.md) (örneğin, hisse senedi bandı): sunucu iletilerin gönderilme hızını denetlemediğinden, bu senaryo Için geri düzler iyi çalışır.
- [İstemciden istemciye](../getting-started/tutorial-getting-started-with-signalr.md) (ör. sohbet): Bu senaryoda, iletilerin sayısı istemci sayısıyla ölçeklenirken, arka uç bir performans sorunu olabilir; diğer bir deyişle, daha fazla istemci katılırken ileti hızının orantılı olarak büyümesi.
- [Yüksek frekanslı gerçek zamanlı](../getting-started/tutorial-high-frequency-realtime-with-signalr.md) (örn. gerçek zamanlı Oyunlar): Bu senaryo için bir geri düzlem önerilmez.

## <a name="enabling-tracing-for-signalr-scaleout"></a>SignalR ölçeği Için Izlemeyi etkinleştirme

Arka düzlemler için izlemeyi etkinleştirmek üzere aşağıdaki bölümleri Web. config dosyasına kök **yapılandırma** öğesinin altına ekleyin:

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
