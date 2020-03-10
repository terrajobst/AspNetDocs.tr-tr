---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR hub 'Ları API Kılavuzu-.NET Istemcisi (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bu belge, .NET istemcilerindeki SignalR sürüm 2 için Windows Mağazası (WinRT), WPF, Silverlight ve dezavantajlar gibi hub API 'leri kullanma hakkında bir giriş sağlar.
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 2b22b53c405a865f91b04e677f60b82dd46dbf9b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623804"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a>ASP.NET SignalR hub 'Ları API Kılavuzu-.NET Istemcisi (SignalR 1. x)

by [Patrick Fletu](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belge, .NET istemcilerindeki SignalR sürüm 2 için Windows Mağazası (WinRT), WPF, Silverlight ve konsol uygulamaları gibi hub API 'leri kullanma hakkında bir giriş sağlar.
> 
> SignalR hub 'Ları API 'SI, uzak yordam çağrılarını (RPC) bir sunucudan, istemcilerden ve istemcilerden sunucuya bağlı hale getirmenizi sağlar. Sunucu kodu ' nda, istemciler tarafından çağrılabilen Yöntemler tanımlar ve istemcide çalışan yöntemleri çağırabilirsiniz. İstemci kodunda, sunucudan çağrılabilen yöntemleri tanımlayabilir ve sunucuda çalışan yöntemleri çağırabilirsiniz. SignalR, sizin için istemciden sunucuya sıhhi kını ele alır.
> 
> SignalR Ayrıca kalıcı bağlantılar adlı alt düzey bir API sunar. SignalR, hub 'Lar ve sürekli bağlantılara giriş veya tam bir SignalR uygulamasının nasıl oluşturulduğunu gösteren bir öğretici için bkz. [SignalR-Başlarken](../getting-started/index.md).

## <a name="overview"></a>Genel bakış

Bu belgede aşağıdaki bölümler yer alır:

- [İstemci kurulumu](#clientsetup)
- [Bağlantı kurma](#establishconnection)

    - [Silverlight istemcilerinden etki alanları arası bağlantılar](#slcrossdomain)
- [Bağlantıyı yapılandırma](#configureconnection)

    - [WPF istemcilerinde en fazla eşzamanlı bağlantı sayısını ayarlama](#maxconnections)
    - [Sorgu dizesi parametrelerini belirtme](#querystring)
    - [Taşıma yöntemini belirtme](#transport)
    - [HTTP üst bilgilerini belirtme](#httpheaders)
    - [İstemci sertifikalarını belirtme](#clientcertificate)
- [Merkez proxy oluşturma](#proxy)
- [İstemcide sunucunun çağırabir yöntemi tanımlama](#callclient)

    - [Parametreleri olmayan Yöntemler](#clientmethodswithoutparms)
    - [Parametre türlerini belirterek parametreleri olan Yöntemler](#clientmethodswithparmtypes)
    - [Parametreleri için dinamik nesneler belirten parametrelere sahip Yöntemler](#clientmethodswithdynamparms)
    - [Bir işleyiciyi kaldırma](#removehandler)
- [İstemciden sunucu yöntemlerini çağırma](#callserver)
- [Bağlantı ömrü olaylarını işleme](#connectionlifetime)
- [Hataları işleme](#handleerrors)
- [İstemci tarafı günlük kaydını etkinleştirme](#logging)
- [Sunucunun çağıra, istemci yöntemleri için WPF, Silverlight ve konsol uygulama kodu örnekleri](#wpfsl)

Örnek bir .NET istemci projeleri için aşağıdaki kaynaklara bakın:

- [Gustavo-Ermenistan ta/SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com (WinRT, Silverlight, konsol uygulama örnekleri) üzerinde örnekler.
- [Inmıanedödüller/SignalR-Moveshail Mo/moveshape. Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GITHUB.com (WPF örneği).
- [SignalR/Microsoft. Aspnet. SignalR. Client. Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (konsol uygulaması örneği).

Sunucu veya JavaScript istemcilerini programmaya yönelik belgeler için aşağıdaki kaynaklara bakın:

- [SignalR hub 'Ları API Kılavuzu-sunucu](../guide-to-the-api/hubs-api-guide-server.md)
- [SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi](../guide-to-the-api/hubs-api-guide-javascript-client.md)

API başvuru konularına bağlantılar, API 'nin .NET 4,5 sürümüdür. .NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.

<a id="clientsetup"></a>

## <a name="client-setup"></a>İstemci kurulumu

[Microsoft. Aspnet. SignalR. Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet paketini ( [Microsoft. Aspnet. SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) paketini değil) yükler. Bu paket, .NET 4 ve .NET 4,5 için WinRT, Silverlight, WPF, konsol uygulaması ve Windows Phone istemcilerini destekler.

İstemci üzerindeki SignalR sürümü, sunucuda sahip olduğunuz sürümden farklıysa, SignalR genellikle farka uyum sağlayabilir. Örneğin, SignalR sürüm 2,0 yayımlanmışsa ve sunucuya yüklüyorsanız, sunucu 1.1. x yüklü olan istemcileri ve 2,0 yüklü istemcileri destekleyecektir. Sunucu üzerindeki sürüm ve istemcideki sürüm arasındaki fark çok harika ise, istemci bir bağlantı kurmaya çalıştığında SignalR bir `InvalidOperationException` özel durumu oluşturur. Hata iletisi "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Bağlantı kurma

Bir bağlantı kurmadan önce, bir `HubConnection` nesnesi oluşturmanız ve proxy oluşturmanız gerekir. Bağlantıyı kurmak için `HubConnection` nesnesinde `Start` yöntemini çağırın.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> JavaScript istemcileri için, bağlantıyı kurmak üzere `Start` yöntemini çağırmadan önce en az bir olay işleyicisini kaydetmeniz gerekir. .NET istemcileri için bu gerekli değildir. JavaScript istemcileri için, oluşturulan proxy kodu, sunucuda var olan tüm Hub 'Lar için otomatik olarak proxy oluşturur ve bir işleyiciyi kaydetmek, istemcinizin hangi hub 'Ları kullandığını belirtebilmeniz anlamına gelir. Ancak, bir .NET istemcisi için hub proxy 'leri el ile oluşturursunuz. SignalR, için proxy oluşturduğunuz herhangi bir hub kullandığınızı varsayar.

Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/SignalR" URL 'sini kullanır. Farklı bir temel URL belirtme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-/SignalR URL 'si](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).

`Start` yöntemi zaman uyumsuz olarak yürütülür. Sonraki kod satırlarının bağlantı kurulana kadar yürütülmediği konusunda emin olmak için, bir ASP.NET 4,5 zaman uyumsuz yönteminde `await` kullanın veya zaman uyumlu bir yöntemde `.Wait()`. WinRT istemcisinde `.Wait()` kullanmayın.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

`HubConnection` sınıfı iş parçacığı güvenlidir.

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Silverlight istemcilerinden etki alanları arası bağlantılar

Silverlight istemcilerinden etki alanları arası bağlantıları etkinleştirme hakkında daha fazla bilgi için bkz. [bir hizmeti etki alanı sınırları genelinde kullanılabilir hale getirme](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Bağlantıyı yapılandırma

Bir bağlantı kurmadan önce, aşağıdaki seçeneklerden herhangi birini belirtebilirsiniz:

- Eşzamanlı bağlantı sınırı.
- Sorgu dizesi parametreleri.
- Taşıma yöntemi.
- HTTP üstbilgileri.
- İstemci sertifikaları.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>WPF istemcilerinde en fazla eşzamanlı bağlantı sayısını ayarlama

WPF istemcilerinde, en fazla eş zamanlı bağlantı sayısını varsayılan 2 değerinden artırmanız gerekebilir. Önerilen değer 10 ' dur.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

Daha fazla bilgi için bkz. [ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Sorgu dizesi parametrelerini belirtme

İstemci bağlandığı zaman sunucuya veri göndermek istiyorsanız, bağlantı nesnesine sorgu dizesi parametreleri ekleyebilirsiniz. Aşağıdaki örnekte, istemci kodunda bir sorgu dizesi parametresinin nasıl ayarlanacağı gösterilmektedir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

Aşağıdaki örnek, sunucu kodundaki bir sorgu dizesi parametresinin nasıl okunacağını gösterir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Taşıma yöntemini belirtme

Bağlantı sürecinin bir parçası olarak, bir SignalR istemcisi normalde sunucu ve istemci tarafından desteklenen en iyi aktarımı tespit etmek üzere sunucuyla görüşür. Kullanmak istediğiniz taşımayı zaten biliyorsanız, bu anlaşma işlemini atlayabilirsiniz. Taşıma yöntemini belirtmek için, başlangıç yöntemine bir taşıma nesnesi geçirin. Aşağıdaki örnek, istemci kodunda taşıma yönteminin nasıl kullanılacağını gösterir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

[Microsoft. Aspnet. SignalR. Client. taşımalar](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) ad alanı, taşımayı belirtmek için kullanabileceğiniz aşağıdaki sınıfları içerir.

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [Websockettransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (yalnızca hem sunucu hem de istemci .NET 4,5 ' i kullanırken kullanılabilir.)
- Otomatik [Aktarım](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (hem istemci hem de sunucu tarafından desteklenen en iyi aktarımı otomatik olarak seçer. Bu, varsayılan aktarımdır. Bunu `Start` yöntemine geçirmek, hiçbir şeyi geçirmeyen aynı etkiye sahiptir.)

Yalnızca tarayıcılar tarafından kullanıldığından, ForeverFrame taşıması bu listeye dahil edilmez.

Sunucu kodundaki aktarım yöntemini denetleme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-bağlam özelliğinden istemci hakkında bilgi alma](../guide-to-the-api/hubs-api-guide-server.md#contextproperty). Aktarımlar ve geri göndermeler hakkında daha fazla bilgi için bkz. [SignalR 'ye giriş-aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>HTTP üst bilgilerini belirtme

HTTP üst bilgilerini ayarlamak için bağlantı nesnesindeki `Headers` özelliğini kullanın. Aşağıdaki örnek, bir HTTP üst bilgisinin nasıl ekleneceğini gösterir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>İstemci sertifikalarını belirtme

İstemci sertifikaları eklemek için bağlantı nesnesindeki `AddClientCertificate` yöntemini kullanın.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>Merkez proxy oluşturma

İstemcideki bir hub 'ın sunucudan çağırabildiği ve sunucudaki bir hub 'da Yöntemler çağırabileceği yöntemleri tanımlamak için bağlantı nesnesi üzerinde `CreateHubProxy` çağırarak Hub için bir ara sunucu oluşturun. `CreateHubProxy` ' a geçirdiğiniz dize, hub sınıfınızın adı veya sunucu üzerinde bir tane kullanılmışsa `HubName` özniteliğiyle belirtilen addır. Ad eşleştirme büyük küçük harfe duyarlıdır.

**Sunucudaki hub sınıfı**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**Hub sınıfı için istemci ara sunucusu oluşturma**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

Hub sınıfınızı bir `HubName` özniteliğiyle süslemek istiyorsanız, bu adı kullanın.

**Sunucudaki hub sınıfı**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

**Hub sınıfı için istemci ara sunucusu oluşturma**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

Proxy nesnesi iş parçacığı güvenlidir. Aslında `HubConnection.CreateHubProxy` aynı `hubName`birden çok kez çağırırsanız, önbelleğe alınmış `IHubProxy` nesnesini alırsınız.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>İstemcide sunucunun çağırabir yöntemi tanımlama

Sunucunun çağırakullanabileceği bir yöntemi tanımlamak için, bir olay işleyicisini kaydetmek üzere proxy 'nin `On` yöntemini kullanın.

Yöntem adı eşleştirme, büyük/küçük harfe duyarlıdır. Örneğin, sunucusundaki `Clients.All.UpdateStockPrice`, istemcide `updateStockPrice`, `updatestockprice`veya `UpdateStockPrice` yürütülür.

Farklı istemci platformları, Kullanıcı arabirimini güncelleştirmek için yöntem kodu yazma konusunda farklı gereksinimlere sahiptir. Gösterilen örnekler, WinRT (Windows Mağazası .NET) istemcileri içindir. WPF, Silverlight ve konsol uygulaması örnekleri, [Bu konunun ilerleyen kısımlarında ayrı bir bölümde](#wpfsl)sunulmaktadır.

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>Parametreleri olmayan Yöntemler

İşlemekte olduğunuz yöntemin parametreleri yoksa, `On` yönteminin genel olmayan aşırı yüklemesini kullanın:

**Parametre olmadan istemci yöntemini çağıran sunucu kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**Parametresiz sunucudan çağrılan yöntem için WinRT Istemci kodu ([Bu konunun ilerleyen kısımlarında bulunan WPF ve Silverlight örneklerine bakın](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Parametre türlerini belirterek parametreleri olan Yöntemler

İşlemekte olduğunuz yöntemin parametreleri varsa, `On` yönteminin genel türleri olarak parametre türlerini belirtin. 8 ' e kadar parametre belirtmenizi sağlayan `On` yönteminin genel aşırı yüklemeleri vardır (Windows Phone 7 üzerinde 4). Aşağıdaki örnekte, `UpdateStockPrice` yöntemine bir parametre gönderilir.

**İstemci yöntemini bir parametre ile çağıran sunucu kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**Parametresi için kullanılan hisse senedi sınıfı**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

**Parametresi ile sunucudan çağrılan bir yöntem için WinRT Istemci kodu ([Bu konunun ilerleyen kısımlarında yer alarak WPF ve Silverlight örneklerine bakın](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Parametreleri için dinamik nesneler belirten parametrelere sahip Yöntemler

Parametreleri `On` yönteminin genel türleri olarak belirtmeye alternatif olarak, parametreleri dinamik nesneler olarak belirtebilirsiniz:

**İstemci yöntemini bir parametre ile çağıran sunucu kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**Parametresi için kullanılan hisse senedi sınıfı**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

**Parametresi için dinamik bir nesne kullanan ve parametresi için bir parametre içeren sunucudan çağrılan bir yöntem için WinRT Istemci kodu ([Bu konunun ilerleyen kısımlarında yer almaktadır WPF ve Silverlight örnekleri](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>Bir işleyiciyi kaldırma

Bir işleyiciyi kaldırmak için `Dispose` yöntemini çağırın.

**Sunucudan çağrılan bir yöntem için istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**İşleyiciyi kaldırmak için istemci kodu**

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>İstemciden sunucu yöntemlerini çağırma

Sunucuda bir yöntemi çağırmak için hub proxy üzerinde `Invoke` yöntemi kullanın.

Sunucu yönteminin dönüş değeri yoksa, `Invoke` yönteminin genel olmayan aşırı yüklemesini kullanın.

**Dönüş değeri olmayan bir yöntem için sunucu kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**Dönüş değeri olmayan bir yöntemi çağıran istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

Sunucu yönteminin bir dönüş değeri varsa, dönüş türünü `Invoke` yönteminin genel türü olarak belirtin.

**Dönüş değerine sahip ve karmaşık bir tür parametresi alan bir yöntem için sunucu kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**Parametre ve dönüş değeri için kullanılan hisse senedi sınıfı**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

**Bir ASP.NET 4,5 zaman uyumsuz yönteminde dönüş değeri olan ve karmaşık tür parametresi alan bir yöntemi çağıran istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**Bir dönüş değeri olan ve bir karmaşık tür parametresi alan ve bir zaman uyumlu yöntemde olan bir yöntemi çağıran istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

`Invoke` yöntemi zaman uyumsuz olarak yürütülür ve bir `Task` nesnesi döndürüyor. `await` veya `.Wait()`belirtmezseniz, bir sonraki kod satırı, çağırabileceğiniz yöntemin yürütmeyi bitirinceye kadar yürütülür.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Bağlantı ömrü olaylarını işleme

SignalR, işleyebilmeniz için aşağıdaki bağlantı ömrü olaylarını sağlar:

- `Received`: bağlantıda herhangi bir veri alındığında tetiklenir. Alınan verileri sağlar.
- `ConnectionSlow`: istemci yavaş veya sık bir bırakma bağlantısı algıladığında tetiklenir.
- `Reconnecting`: temeldeki aktarım yeniden bağlanmaya başladığında tetiklenir.
- `Reconnected`: temeldeki aktarım yeniden bağlandığında tetiklenir.
- `StateChanged`: bağlantı durumu değiştiğinde tetiklenir. Eski durumu ve yeni durumu sağlar. Bağlantı durumu değerleri hakkında daha fazla bilgi için bkz. [ConnectionState numaralandırması](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).
- `Closed`: bağlantının bağlantısı kesildiğinde tetiklenir.

Örneğin, önemli olmayan hatalar için uyarı iletileri göstermek istiyorsanız, ancak bağlantının yavaşlılığını veya sık olarak düşürülmesi gibi aralıklı bağlantı sorunlarına neden olursa `ConnectionSlow` olayını işleyin.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

Daha fazla bilgi için bkz. [SignalR 'de bağlantı ömrü olaylarını anlama ve işleme](../guide-to-the-api/handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Hataları işleme

Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, bir hatadan sonra SignalR 'nin döndürdüğü özel durum nesnesi hata hakkında en az bilgi içerir. Örneğin, `newContosoChatMessage` çağrısı başarısız olursa, hata nesnesindeki hata iletisi, güvenlik nedenleriyle, üretim aşamasındaki istemcilere ayrıntılı hata iletileri gönderilmesi "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" içerir, ancak sorun giderme amacıyla ayrıntılı hata iletileri etkinleştirmek istiyorsanız, sunucuda aşağıdaki kodu kullanın.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

SignalR 'nin yükselten hataları işlemek için bağlantı nesnesi üzerinde `Error` olayı için bir işleyici ekleyebilirsiniz.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

Yöntem etkinleştirmeleri içindeki hataları işlemek için, kodu bir try-catch bloğunda sarın.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>İstemci tarafı günlük kaydını etkinleştirme

İstemci tarafı günlük kaydını etkinleştirmek için, bağlantı nesnesindeki `TraceLevel` ve `TraceWriter` özelliklerini ayarlayın.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>Sunucunun çağıra, istemci yöntemleri için WPF, Silverlight ve konsol uygulama kodu örnekleri

Daha önce sunucunun, WinRT istemcilerine uygulama çağırabilecek istemci yöntemleri tanımlamak için gösterilen kod örnekleri. Aşağıdaki örnekler WPF, Silverlight ve konsol uygulama istemcileri için eşdeğer kodu gösterir.

### <a name="methods-without-parameters"></a>Parametreleri olmayan Yöntemler

**Parametre olmadan sunucudan çağrılan yöntem için WPF istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Parametresiz sunucudan çağrılan yöntem için Silverlight istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**Parametre olmadan sunucudan çağrılan yöntem için konsol uygulaması istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Parametre türlerini belirterek parametreleri olan Yöntemler

**Bir parametre ile sunucudan çağrılan bir yöntem için WPF istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Bir parametre ile sunucudan çağrılan bir yöntem için Silverlight istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**Bir parametre ile sunucudan çağrılan bir yöntem için konsol uygulaması istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Parametreleri için dinamik nesneler belirten parametrelere sahip Yöntemler

**Parametresi için dinamik bir nesne kullanarak, bir parametresiyle sunucudan çağrılan bir yöntem için WPF istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Parametresi için dinamik bir nesne kullanarak, bir parametresiyle sunucudan çağrılan bir yöntem için Silverlight istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**Parametresi için dinamik bir nesne kullanarak, bir parametresiyle sunucudan çağrılan bir yöntemin konsol uygulama istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
