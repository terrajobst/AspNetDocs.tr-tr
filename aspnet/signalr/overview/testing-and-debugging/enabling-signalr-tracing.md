---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: SignalR Izlemeyi etkinleştirme | Microsoft Docs
author: bradygaster
description: Bu belgede, SignalR sunucuları ve istemcileri için izlemenin nasıl etkinleştirileceği ve yapılandırılacağı açıklanmaktadır. İzleme, olaylar hakkında tanılama bilgilerini görüntülemenize olanak sağlar...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578836"
---
# <a name="enabling-signalr-tracing"></a>SignalR İzlemeyi Etkinleştirme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belgede, SignalR sunucuları ve istemcileri için izlemenin nasıl etkinleştirileceği ve yapılandırılacağı açıklanmaktadır. İzleme, SignalR uygulamanızda olaylarla ilgili tanılama bilgilerini görüntülemenize olanak sağlar.
>
> Bu konu, ilk başta Patrick Fleti tarafından yazılmıştır.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET Framework 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
>
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

İzleme etkinleştirildiğinde, bir SignalR uygulaması olaylar için günlük girişleri oluşturur. Olayları hem istemciden hem de sunucudan günlüğe kaydedebilirsiniz. Sunucu günlüğü bağlantısı, genişleme sağlayıcısı ve ileti veri yolu olaylarını izleme. İstemci üzerindeki izleme, bağlantı olaylarını günlüğe kaydeder. SignalR 2,1 ve üzeri sürümlerde, istemci üzerindeki izleme, hub çağırma iletilerinin tam içeriğini günlüğe kaydeder.

## <a name="contents"></a>İçindekiler

- [Sunucuda izlemeyi etkinleştirme](#server)

    - [Sunucu olaylarını metin dosyalarına kaydetme](#server_text)
    - [Sunucu olaylarını olay günlüğüne kaydetme](#server_eventlog)
- [.NET istemcisinde izlemeyi etkinleştirme (Windows Masaüstü uygulamaları)](#net_client)

    - [Masaüstü istemci olaylarını konsola kaydetme](#desktop_console)
    - [Masaüstü istemci olaylarını bir metin dosyasına kaydetme](#desktop_text)
- [Windows Phone 8 istemcilerde izlemeyi etkinleştirme](#phone)

    - [İstemci olaylarını Windows Phone Kullanıcı arabirimine kaydetme](#phone_ui)
    - [İstemci olaylarını Windows Phone hata ayıklama konsoluna kaydetme](#phone_debug)
- [JavaScript istemcisinde izlemeyi etkinleştirme](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>Sunucuda izlemeyi etkinleştirme

Uygulamanın yapılandırma dosyası (proje türüne bağlı olarak App. config veya Web. config) içindeki sunucuda izlemeyi etkinleştirirsiniz. Hangi olay kategorilerini günlüğe kaydetmek istediğinizi belirtirsiniz. Yapılandırma dosyasında, olayları bir metin dosyasına, Windows olay günlüğüne veya [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)uygulamasını kullanarak özel bir günlüğe günlüğe kaydetmek isteyip istemediğinizi de belirtirsiniz.

Sunucu olay kategorileri aşağıdaki ileti türlerini içerir:

| Kaynak | İletiler |
| --- | --- |
| SignalR. SqlMessageBus | SQL Ileti veri yolu genişleme sağlayıcısı kurulumu, veritabanı işlemi, hata ve zaman aşımı olayları |
| SignalR. ServiceBusMessageBus | Service Bus genişleme sağlayıcısı konu oluşturma ve abonelik, hata ve mesajlaşma olayları |
| SignalR. RedisMessageBus | Redsıs genişleme sağlayıcı bağlantısı, bağlantı kesilmesi ve hata olayları |
| SignalR. ScaleoutMessageBus | Genişleme mesajlaşma olayları |
| SignalR. taşımalar. WebSocketTransport | WebSocket aktarım bağlantısı, bağlantı kesilmesi, mesajlaşma ve hata olayları |
| SignalR. taşımalar. ServerSentEventsTransport | ServerSentEvents aktarım bağlantısı, bağlantı kesme, mesajlaşma ve hata olayları |
| SignalR. taşımalar. ForeverFrameTransport | ForeverFrame aktarım bağlantısı, bağlantı kesilmesi, mesajlaşma ve hata olayları |
| SignalR.Transports.LongPollingTransport | Uzun Gplipop aktarım bağlantısı, bağlantı kesilmesi, mesajlaşma ve hata olayları |
| SignalR. taşımalar. TransportHeartBeat | Aktarım bağlantısı, bağlantı kesilmesi ve KeepAlive olayları |
| SignalR. ReflectedHubDescriptorProvider | Merkez bulma olayları |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>Sunucu olaylarını metin dosyalarına kaydetme

Aşağıdaki kod, her olay kategorisi için izlemenin nasıl etkinleştirileceğini gösterir. Bu örnek, uygulamayı metin dosyalarına olayları günlüğe kaydetmek üzere yapılandırır.

**İzlemeyi etkinleştirmek için XML sunucusu kodu**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

Yukarıdaki kodda `SignalRSwitch` girdisi, belirtilen günlüğe gönderilen olaylar için [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) kullanılan öğesini belirtir. Bu durumda, tüm hata ayıklama ve izleme iletilerinin kaydedildiği `Verbose` olarak ayarlanır.

Aşağıdaki çıktıda, yukarıdaki yapılandırma dosyası kullanılarak bir uygulama için `transports.log.txt` dosyasındaki girişler gösterilmektedir. Yeni bir bağlantı, kaldırılan bir bağlantı ve aktarım sinyali olayları gösterir.

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>Sunucu olaylarını olay günlüğüne kaydetme

Olayları bir metin dosyası yerine olay günlüğüne kaydetmek için `sharedListeners` düğümündeki girişlerin değerlerini değiştirin. Aşağıdaki kod, sunucu olaylarının olay günlüğüne nasıl günlüğe alınacağını gösterir:

**Olay günlüğüne olayları günlüğe kaydetmek için XML sunucusu kodu**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

Olaylar uygulama günlüğüne kaydedilir ve aşağıda gösterildiği gibi Olay Görüntüleyicisi aracılığıyla kullanılabilir:

![SignalR günlüklerini gösteren Olay Görüntüleyicisi](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> Olay günlüğünü kullanırken, bulunan ileti sayısını korumak için **TraceLevel** . **Error** ' u ayarlayın.

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>.NET istemcisinde izlemeyi etkinleştirme (Windows Masaüstü uygulamaları)

.NET istemcisi, bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)uygulamasını kullanarak olayları konsola, bir metin dosyasına veya özel bir günlüğe kaydedebilir.

.NET istemcisinde günlüğe kaydetmeyi etkinleştirmek için, bağlantının `TraceLevel` özelliğini bir [Tracelevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) değerine ve `TraceWriter` özelliğini geçerli bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) örneğine ayarlayın.

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>Masaüstü istemci olaylarını konsola kaydetme

Aşağıdaki C# kod, .net istemcisindeki olaylarının konsola nasıl günlüğe alınacağını gösterir:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>Masaüstü istemci olaylarını bir metin dosyasına kaydetme

Aşağıdaki C# kod, .net istemcisindeki olayların bir metin dosyasına nasıl günlüğe alınacağını gösterir:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

Aşağıdaki çıktıda, yukarıdaki yapılandırma dosyası kullanılarak bir uygulama için `ClientLog.txt` dosyasındaki girişler gösterilmektedir. Sunucuya bağlanan istemciyi ve `addMessage`adlı bir istemci yöntemini çağıran hub 'ı gösterir:

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>Windows Phone 8 istemcilerde izlemeyi etkinleştirme

Windows Phone uygulamalar için SignalR uygulamaları, masaüstü uygulamaları ile aynı .NET istemcisini kullanır, ancak [Console. out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) ve [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) ile bir dosyaya yazma kullanılamaz. Bunun yerine, izleme için özel bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) uygulamasının oluşturulması gerekir.

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>İstemci olaylarını Windows Phone Kullanıcı arabirimine kaydetme

[SignalR kod temeli](https://github.com/SignalR/SignalR/archive/master.zip) , `TextBlockWriter`adlı özel bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) uygulamasını kullanarak, izleme çıkışını bir [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) öğesine yazan Windows Phone bir örnek içerir. Bu sınıf, **Samples/Microsoft. Aspnet. SignalR. Client. WP8. Samples** projesinde bulunabilir. Bir `TextBlockWriter`örneği oluştururken geçerli [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)içinde geçirin ve izleme çıktısı için kullanılacak bir [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) oluşturacak bir [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) oluşturun:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

Daha sonra, izleme çıktısı, geçirilen [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) içinde oluşturulan yeni bir [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) öğesine yazılır:

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>İstemci olaylarını Windows Phone hata ayıklama konsoluna kaydetme

Kullanıcı arabirimi yerine hata ayıklama konsoluna çıkış göndermek için, hata ayıklama penceresine yazan bir [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) uygulamasını oluşturun ve bunu bağlantınızın [tracewriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) özelliğine atayın:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

İzleme bilgileri, Visual Studio 'daki hata ayıklama penceresine yazılır:

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>JavaScript istemcisinde izlemeyi etkinleştirme

Bir bağlantıda istemci tarafı günlüğe kaydetmeyi etkinleştirmek için, bağlantıyı kurmak üzere `start` yöntemini çağırmadan önce bağlantı nesnesindeki `logging` özelliğini ayarlayın.

**Tarayıcı konsolunda izlemeyi etkinleştirmeye yönelik istemci JavaScript kodu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**Tarayıcı konsolunda izlemeyi etkinleştirmeye yönelik istemci JavaScript kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

İzleme etkinleştirildiğinde, JavaScript istemcisi olayları tarayıcı konsoluna kaydeder. Tarayıcı konsoluna erişmek için bkz. [aktarımları izleme](../getting-started/introduction-to-signalr.md#MonitoringTransports).

Aşağıdaki ekran görüntüsünde, izlemenin etkinleştirildiği bir SignalR JavaScript istemcisi gösterilmektedir. Tarayıcı konsolundaki bağlantı ve hub çağırma olaylarını gösterir:

![Tarayıcı konsolundaki SignalR izleme olayları](enabling-signalr-tracing/_static/image4.png)
