---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: ASP.NET SignalR hub 'Ları API Kılavuzu-sunucu (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bu belgede, SignalR sürüm 1,1 için ASP.NET SignalR hub API 'sinin sunucu tarafını programlama, kod örnekleri demonstratin...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579641"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a>ASP.NET SignalR hub 'Ları API Kılavuzu-sunucu (SignalR 1. x)

by [Patrick Fletu](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belgede, SignalR sürüm 1,1 için ASP.NET SignalR hub 'ı API 'sinin sunucu tarafını programlama konusunda bir giriş ve ortak seçenekleri gösteren kod örnekleri sunulmaktadır.
> 
> SignalR hub 'Ları API 'SI, uzak yordam çağrılarını (RPC) bir sunucudan, istemcilerden ve istemcilerden sunucuya bağlı hale getirmenizi sağlar. Sunucu kodu ' nda, istemciler tarafından çağrılabilen Yöntemler tanımlar ve istemcide çalışan yöntemleri çağırabilirsiniz. İstemci kodunda, sunucudan çağrılabilen yöntemleri tanımlayabilir ve sunucuda çalışan yöntemleri çağırabilirsiniz. SignalR, sizin için istemciden sunucuya sıhhi kını ele alır.
> 
> SignalR Ayrıca kalıcı bağlantılar adlı alt düzey bir API sunar. SignalR, hub 'Lar ve sürekli bağlantılara giriş veya tam bir SignalR uygulamasının nasıl oluşturulduğunu gösteren bir öğretici için bkz. [SignalR-Başlarken](index.md).

## <a name="overview"></a>Genel bakış

Bu belgede aşağıdaki bölümler yer alır:

- [SignalR rotasını kaydetme ve SignalR seçeneklerini yapılandırma](#route)

    - [/SignalR URL 'SI](#signalrurl)
    - [SignalR seçeneklerini yapılandırma](#options)
- [Hub sınıfları oluşturma ve kullanma](#hubclass)

    - [Hub nesnesi ömrü](#transience)
    - [Camel-JavaScript istemcilerinde hub adlarının büyük küçük harfleri](#hubnames)
    - [Birden çok hub](#multiplehubs)
- [Hub sınıfında istemcilerin çağırabilmeniz için yöntemler tanımlama](#hubmethods)

    - [Camel-JavaScript istemcilerinde yöntem adlarının büyük küçük harfleri](#methodnames)
    - [Zaman uyumsuz olarak yürütme](#asyncmethods)
    - [Aşırı yüklemeleri tanımlama](#overloads)
- [Hub sınıfından istemci yöntemlerini çağırma](#callfromhub)

    - [Hangi istemcilerin RPC alacağını seçme](#selectingclients)
    - [Yöntem adları için derleme zamanı doğrulaması yok](#dynamicmethodnames)
    - [Büyük/küçük harf duyarsız Yöntem adı eşleştirme](#caseinsensitive)
    - [Zaman uyumsuz yürütme](#asyncclient)
- [Hub sınıfından grup üyeliğini yönetme](#groupsfromhub)

    - [Ekleme ve kaldırma yöntemlerinin zaman uyumsuz yürütmesi](#asyncgroupmethods)
    - [Grup üyeliği kalıcılığı](#grouppersistence)
    - [Tek Kullanıcı grupları](#singleusergroups)
- [Hub sınıfında bağlantı ömrü olaylarını işleme](#connectionlifetime)

    - [OnConnected, OnConnected ve OnConnected çağrıldığında](#onreconnected)
    - [Çağıran durum doldurulmamış](#nocallerstate)
- [Bağlam özelliğinden istemci hakkında bilgi alma](#contextproperty)
- [İstemcilerle hub sınıfı arasında durum geçirme](#passstate)
- [Hub sınıfında hataları işleme](#handleErrors)
- [İstemci yöntemlerini çağırma ve grupları hub sınıfı dışından yönetme](#callfromoutsidehub)

    - [İstemci yöntemlerini çağırma](#callingclientsoutsidehub)
    - [Grup üyeliğini yönetme](#managinggroupsoutsidehub)
- [İzlemeyi etkinleştirme](#tracing)
- [Hub ardışık düzenini özelleştirme](#hubpipeline)

İstemcilerin programtasyonu hakkındaki belgeler için aşağıdaki kaynaklara bakın:

- [SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi](index.md)
- [SignalR hub 'Ları API Kılavuzu-.NET Istemcisi](index.md)

API başvuru konularına bağlantılar, API 'nin .NET 4,5 sürümüdür. .NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a>SignalR rotasını kaydetme ve SignalR seçeneklerini yapılandırma

İstemcilerin hub 'ınıza bağlanmak için kullanacağı yolu tanımlamak için, uygulama başladığında [Maphubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) yöntemini çağırın. `MapHubs`, `System.Web.Routing.RouteCollection` sınıfı için bir [genişletme yöntemidir](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) . Aşağıdaki örnek, *küresel. asax* dosyasında SignalR hub yolunun nasıl tanımlanacağını gösterir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

Bir ASP.NET MVC uygulamasına SignalR işlevselliği ekliyorsanız, SignalR yolunun diğer yollarla önce eklendiğinden emin olun. Daha fazla bilgi için bkz. [öğretici: SignalR ve MVC 4 Ile çalışmaya](index.md)başlama.

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/SignalR URL 'SI

Varsayılan olarak, istemcilerin hub 'ınıza bağlanmak için kullanacağı yol URL 'SI "/SignalR" olarak değişir. (Bu URL 'YI otomatik olarak oluşturulan JavaScript dosyası için olan "/SignalR/Hub" URL 'siyle karıştırmayın. Oluşturulan ara sunucu hakkında daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-oluşturulan ara sunucu ve sizin için ne yapar](index.md).)

Bu temel URL 'YI SignalR için kullanılamaz hale getirmek için olağandışı durumlar olabilir; Örneğin, projenizde *SignalR* adlı bir klasörünüz var ve adı değiştirmek istemezsiniz. Bu durumda, aşağıdaki örneklerde gösterildiği gibi temel URL 'YI değiştirebilirsiniz (örnek kodda "/SignalR" değerini istediğiniz URL ile değiştirin).

**URL 'YI belirten sunucu kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

**URL 'YI belirten JavaScript istemci kodu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

**URL 'YI belirten JavaScript istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

**URL 'YI belirten .NET istemci kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>SignalR seçeneklerini yapılandırma

`MapHubs` yönteminin aşırı yüklemeleri, özel bir URL, özel bir bağımlılık Çözümleyicisi ve aşağıdaki seçenekleri belirtmenize olanak sağlar:

- Tarayıcı istemcilerinden etki alanları arası çağrıları etkinleştirin.

    Genellikle tarayıcı `http://contoso.com`bir sayfa yüklerse, SignalR bağlantısı aynı etki alanında, `http://contoso.com/signalr`. `http://contoso.com` sayfa, etki alanları arası bağlantı olan `http://fabrikam.com/signalr`bir bağlantı yapıyorsa. Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışıdır. Daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-etki alanları arası bağlantı oluşturma](index.md).
- Ayrıntılı hata iletilerini etkinleştirin.

    Hata oluştuğunda, SignalR 'nin varsayılan davranışı istemcilere ne olduğuna ilişkin ayrıntıları içermeyen bir bildirim iletisi gönderir. Kötü amaçlı kullanıcılar, uygulamanıza karşı saldırılara karşı bilgileri kullanabilabileceğinden, istemcilere ayrıntılı hata bilgileri gönderilmesi, üretimde önerilmez. Sorun giderme için, bu seçeneği kullanarak daha fazla bilgilendirici hata raporlamayı geçici olarak etkinleştirebilirsiniz.
- Otomatik olarak oluşturulan JavaScript proxy dosyalarını devre dışı bırakın.

    Varsayılan olarak, hub sınıflarınız için proxy 'leri olan bir JavaScript dosyası "/SignalR/Hub" URL 'sine yanıt olarak oluşturulur. JavaScript proxy 'lerini kullanmak istemiyorsanız veya bu dosyayı el ile oluşturmak ve istemcilerinizdeki fiziksel bir dosyaya başvurmak istiyorsanız, ara sunucu oluşturmayı devre dışı bırakmak için bu seçeneği kullanabilirsiniz. Daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-SignalR tarafından oluşturulan ara sunucu için fiziksel dosya oluşturma](index.md).

Aşağıdaki örnek, SignalR bağlantı URL 'sinin ve bu seçeneklerin `MapHubs` metoduna yapılan bir çağrıda nasıl ekleneceğini gösterir. Özel bir URL belirtmek için örnekteki "/SignalR" değerini kullanmak istediğiniz URL ile değiştirin.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>Hub sınıfları oluşturma ve kullanma

Bir hub oluşturmak için, [Microsoft. Aspnet. SignalR. hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)' dan türetilen bir sınıf oluşturun. Aşağıdaki örnekte, bir sohbet uygulaması için basit bir hub sınıfı gösterilmektedir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

Bu örnekte, bağlı bir istemci `NewContosoChatMessage` yöntemini çağırabilir ve ne zaman yapıldığında, alınan veriler tüm bağlı istemcilere göre belirlenir.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>Hub nesnesi ömrü

Hub sınıfını örnekleyemezsiniz veya kendi kodunuzda kendi kodınızdan yöntemlerini çağıramazsınız; Her şey, SignalR hub 'ı tarafından sizin için yapılır. SignalR, bir istemcinin bağlandığı, bağlantısı kesilen veya sunucuya bir yöntem çağrısı yaptığı zaman gibi bir hub işlemini her işlemesi gerektiğinde hub sınıfınızın yeni bir örneğini oluşturur.

Hub sınıfının örnekleri geçici olduğundan, bir sonraki yöntem çağrısından durumu korumak için bunları kullanamazsınız. Sunucu istemciden bir yöntem çağrısı aldığında, hub sınıfınızın yeni bir örneği iletiyi işler. Birden çok bağlantı ve yöntem çağrısı aracılığıyla durumu korumak için, veritabanı veya hub sınıfında bir statik değişken veya `Hub`türetmeyen farklı bir sınıf gibi başka bir yöntem kullanın. Hub sınıfında statik değişken gibi bir yöntemi kullanarak verileri bellekte kalıcı hale getirilürse, uygulama etki alanı geri dönüştürüldüğünde veriler kaybolur.

Hub sınıfı dışında çalışan kendi kodlarınızdan istemcilere ileti göndermek istiyorsanız, bir hub sınıfı örneği oluşturarak bunu yapamazsınız, ancak hub sınıfınız için SignalR bağlam nesnesine bir başvuru alarak bunu yapabilirsiniz. Daha fazla bilgi için, bu konunun ilerleyen kısımlarında [istemci yöntemlerini çağırma ve hub sınıfının dışından grupları yönetme](#callfromoutsidehub) konularına bakın.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>Camel-JavaScript istemcilerinde hub adlarının büyük küçük harfleri

Varsayılan olarak, JavaScript istemcileri, sınıf adının Camel-cased bir sürümünü kullanarak hub 'Lara başvurur. SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar. Önceki örneğe JavaScript kodunda `contosoChatHub` adı verilir.

**Sunucu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

**Oluşturulan proxy kullanan JavaScript istemcisi**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

İstemcilerin kullanması için farklı bir ad belirtmek istiyorsanız, `HubName` özniteliğini ekleyin. Bir `HubName` özniteliği kullandığınızda JavaScript istemcilerinde ortası örneğine bir ad değişikliği yapılmaz.

**Sunucu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

**Oluşturulan proxy kullanan JavaScript istemcisi**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>Birden çok hub

Bir uygulamada birden çok hub sınıfı tanımlayabilirsiniz. Bunu yaptığınızda bağlantı paylaşılır, ancak gruplar ayrıdır:

- Tüm istemciler hizmetinize bir SignalR bağlantısı kurmak için aynı URL 'YI kullanır ("/SignalR" veya bir tane belirtilmişse özel URL 'niz) ve bu bağlantı, hizmet tarafından tanımlanan tüm Hub 'Lar için kullanılır.

    Tek bir sınıfta tüm Hub işlevlerini tanımlamaya kıyasla birden çok Hub için performans farkı yoktur.
- Tüm Hub 'Lar aynı HTTP istek bilgilerini alır.

    Tüm Hub 'Lar aynı bağlantıyı paylaştığından, sunucunun aldığı tek HTTP istek bilgileri, SignalR bağlantısını kuran özgün HTTP isteğine gelir. Bir sorgu dizesi belirterek istemciden sunucuya bilgi geçirmek için bağlantı isteğini kullanırsanız, farklı hub 'Lara farklı sorgu dizeleri sağlayamıyorum. Tüm Hub 'Lar aynı bilgileri alır.
- Oluşturulan JavaScript proxy 'leri dosyası, tek bir dosyadaki tüm Hub 'Lara ait proxy 'leri içerir.

    JavaScript proxy 'leri hakkında daha fazla bilgi için bkz. [SignalR hub 'LARı API Kılavuzu-JavaScript istemcisi-oluşturulan ara sunucu ve sizin için ne yapar](index.md).
- Gruplar, hub 'Lar içinde tanımlanır.

    SignalR 'de, bağlı istemcilerin alt kümelerine yayınlamak için adlandırılmış grupları tanımlayabilirsiniz. Gruplar her Hub için ayrı ayrı tutulur. Örneğin, "Administrators" adlı bir grup `ContosoChatHub` sınıfınız için bir istemci kümesi içerir ve aynı grup adı `StockTickerHub` sınıfınız için farklı bir istemci kümesine başvuracaktır.

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>Hub sınıfında istemcilerin çağırabilmeniz için yöntemler tanımlama

Merkezi üzerinde istemciden çağrılabilir olmasını istediğiniz bir yöntemi ortaya çıkarmak için aşağıdaki örneklerde gösterildiği gibi bir genel yöntem bildirin.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

Herhangi C# bir yöntemde yaptığınız gibi, karmaşık türler ve diziler dahil olmak üzere bir dönüş türü ve parametreleri belirtebilirsiniz. Parametrelerde aldığınız veya çağırana geri döndürülen tüm veriler, istemci ile sunucu arasında JSON kullanılarak iletilir ve SignalR karmaşık nesnelerin ve nesne dizilerinin otomatik olarak bağlamasını işler.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>Camel-JavaScript istemcilerinde yöntem adlarının büyük küçük harfleri

Varsayılan olarak, JavaScript istemcileri, yöntem adının Camel-cased bir sürümünü kullanarak Merkez yöntemlerine başvurur. SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.

**Sunucu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**Oluşturulan proxy kullanan JavaScript istemcisi**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

İstemcilerin kullanması için farklı bir ad belirtmek istiyorsanız, `HubMethodName` özniteliğini ekleyin.

**Sunucu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**Oluşturulan proxy kullanan JavaScript istemcisi**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>Zaman uyumsuz olarak yürütme

Yöntem uzun süre çalışabilir veya bir veritabanı araması veya bir Web hizmeti çağrısı gibi beklemeyi gerektirebilecek iş yapmak için, bir [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (`void` dönüşü yerine) veya [görev&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) nesnesi (`T` dönüş türü yerine) döndürerek hub yöntemini zaman uyumsuz yapın. Yönteminden bir `Task` nesnesi döndürdüğünüzde, SignalR `Task` tamamlanmasını bekler ve sarmalanmamış sonucu istemciye geri gönderir. bu nedenle, istemcide yöntem çağrısını nasıl kodlayabilmeniz fark yoktur.

Bir hub yönteminin zaman uyumsuz yapılması, WebSocket aktarımını kullandığında bağlantının engellenmesini önler. Bir hub yöntemi zaman uyumlu olarak yürütülüyorsa ve aktarım WebSocket ise, hub yöntemi tamamlanana kadar hub üzerindeki yöntemlerin sonraki çağrıları aynı istemciden engellenir.

Aşağıdaki örnek, her iki sürümü de çağırmak için çalışan JavaScript istemci kodu tarafından zaman uyumlu veya zaman uyumsuz olarak çalışacak şekilde kodlanmış aynı yöntemi gösterir.

**K**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

**Zaman uyumsuz-ASP.NET 4,5**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**Oluşturulan proxy kullanan JavaScript istemcisi**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

ASP.NET 4,5 ' de zaman uyumsuz yöntemlerin nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [ASP.NET MVC 4 Içinde zaman uyumsuz yöntemler kullanma](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).

<a id="overloads"></a>

### <a name="defining-overloads"></a>Aşırı yüklemeleri tanımlama

Bir yöntem için aşırı yüklemeleri tanımlamak istiyorsanız, her aşırı yüklemede parametre sayısı farklı olmalıdır. Farklı parametre türleri belirterek bir aşırı yüklemeyi ayırt ediyorsanız, hub sınıfınız derlenir, ancak istemciler aşırı yüklemelerin birini çağırmaya çalıştığında, çalışma zamanında SignalR hizmeti bir özel durum oluşturur.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>Hub sınıfından istemci yöntemlerini çağırma

Sunucudan istemci yöntemlerini çağırmak için, hub sınıfınızın bir yönteminde `Clients` özelliğini kullanın. Aşağıdaki örnek, tüm bağlı istemcilerde `addNewMessageToPage` çağıran sunucu kodunu ve bir JavaScript istemcisinde yöntemi tanımlayan istemci kodunu gösterir.

**Sunucu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

**Oluşturulan proxy kullanan JavaScript istemcisi**

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

İstemci yönteminden bir dönüş değeri alamazsınız; `int x = Clients.All.add(1,1)` gibi sözdizimi çalışmıyor.

Parametreler için karmaşık türler ve diziler belirleyebilirsiniz. Aşağıdaki örnek, bir yöntem parametresinde istemciye karmaşık bir tür geçirir.

**Karmaşık bir nesne kullanarak istemci yöntemini çağıran sunucu kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

**Karmaşık nesneyi tanımlayan sunucu kodu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

**Oluşturulan proxy kullanan JavaScript istemcisi**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>Hangi istemcilerin RPC alacağını seçme

Clients özelliği, hangi istemcilerin RPC alacağını belirtmek için çeşitli seçenekler sağlayan bir [Hubconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) nesnesi döndürür:

- Bağlanan tüm istemciler.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- Yalnızca çağıran istemci.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- Çağıran istemci dışındaki tüm istemciler.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- Bağlantı KIMLIĞIYLE tanımlanan belirli bir istemci.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    Bu örnek, çağıran istemcide `addContosoChatMessageToPage` çağırır ve `Clients.Caller`ile aynı etkiye sahiptir.
- Belirtilen istemciler dışındaki tüm bağlı istemciler, bağlantı KIMLIĞIYLE tanımlanır.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- Belirtilen bir gruptaki tüm bağlı istemciler.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- Belirtilen bir gruptaki, belirtilen istemciler hariç, bağlantı KIMLIĞIYLE tanımlanan tüm bağlı istemciler.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- Çağıran istemci hariç, belirtilen bir gruptaki tüm bağlı istemciler.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>Yöntem adları için derleme zamanı doğrulaması yok

Belirttiğiniz Yöntem adı dinamik bir nesne olarak yorumlanır, yani bunun için IntelliSense veya derleme zamanı doğrulaması yoktur. İfade çalışma zamanında değerlendirilir. Yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerlerini istemciye gönderir ve istemcinin adıyla eşleşen bir yöntemi varsa, bu yöntem çağrılır ve parametre değerleri kendisine geçirilir. İstemcide eşleşen bir yöntem bulunamazsa, hiçbir hata oluşturulmaz. İstemci yöntemini çağırdığınızda SignalR 'nin arka planda istemciye ilettiği verilerin biçimi hakkında daha fazla bilgi için bkz. [SignalR 'ye giriş](index.md).

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>Büyük/küçük harf duyarsız Yöntem adı eşleştirme

Yöntem adı eşleştirme, büyük/küçük harfe duyarlıdır. Örneğin, sunucusundaki `Clients.All.addContosoChatMessageToPage`, istemcide `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`veya `addContosoChatMessageToPage` yürütülür.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>Zaman uyumsuz yürütme

Çağırdığınız yöntem zaman uyumsuz olarak yürütülür. Bir istemciye yönelik bir yöntem çağrısından sonra gelen herhangi bir kod, sonraki kod satırlarının Yöntem tamamlanmasını beklemesi gerekmediği takdirde, SignalR 'nin istemcilere veri aktarma işleminin bitmesini beklemeden hemen yürütülür. Aşağıdaki kod örnekleri, iki istemci yönteminin sırayla nasıl yürütüleceğini, .NET 4,5 ' de çalıştırılan kodu ve .NET 4 ' te çalıştırılan bir kodu kullanmayı göstermektedir.

**.NET 4,5 örneği**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

**.NET 4 örneği**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

Bir sonraki kod satırından önce istemci yöntemi bitene kadar beklemek için `await` veya `ContinueWith` kullanırsanız, bu, istemcilerin bir sonraki kod çalıştırılmadan önce iletiyi gerçekten alacağı anlamına gelmez. Bir istemci yöntemi çağrısının "tamamlama" işlemi, SignalR 'nin iletiyi göndermek için gereken her şeyi yaptığı anlamına gelir. İstemcilerin iletiyi aldığını doğrulamaya ihtiyacınız varsa, o mekanizmayı kendiniz programlayabilirsiniz. Örneğin, hub 'da bir `MessageReceived` yöntemi kod, istemci üzerindeki `addContosoChatMessageToPage` yönteminde, istemcide yapmanız gereken herhangi bir işi yaptıktan sonra `MessageReceived` çağırabilirsiniz. Hub 'daki `MessageReceived`, gerçek istemci alımı ve özgün yöntem çağrısının işlenmesine bağlı olarak herhangi bir işi yapabilirsiniz.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>Yöntem adı olarak bir dize değişkeni kullanma

Bir istemci yöntemini, yöntem adı olarak bir dize değişkeni kullanarak çağırmak istiyorsanız, `Clients.All` (veya `Clients.Others`, `Clients.Caller`, vb.) `IClientProxy` ve sonra [Invoke (MethodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)öğesini çağırın.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>Hub sınıfından grup üyeliğini yönetme

SignalR içindeki gruplar, bağlı istemcilerin belirtilen alt kümelerine ileti yayınlamak için bir yöntem sağlar. Bir grup herhangi bir sayıda istemciye sahip olabilir ve bir istemci herhangi bir sayıda grubun üyesi olabilir.

Grup üyeliğini yönetmek için, hub sınıfının `Groups` özelliği tarafından sunulan [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) ve [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemlerini kullanın. Aşağıdaki örnek, istemci kodu tarafından çağrılan ve ardından bunları çağıran JavaScript istemci kodunun ardından, hub yöntemlerinde kullanılan `Groups.Add` ve `Groups.Remove` yöntemlerini gösterir.

**Sunucu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

**Oluşturulan proxy kullanan JavaScript istemcisi**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

Açıkça grup oluşturmanız gerekmez. Aslında bir grup, bir `Groups.Add`çağrısında adını ilk kez belirttiğinizde otomatik olarak oluşturulur ve içindeki üyeliğinden son bağlantıyı kaldırdığınızda silinir.

Grup üyeliği listesi veya Grup listesi almak için API yok. SignalR bir [yayın/alt modele](http://en.wikipedia.org/wiki/Publish/subscribe)göre istemcilere ve gruplara iletiler gönderir ve sunucu grup veya grup üyelikleri listesini korumaz. Bu, bir Web grubuna düğüm eklediğiniz her durumda, SignalR 'nin koruduğu tüm durumun yeni düğüme yayılması nedeniyle ölçeklenebilirliği en üst düzeye çıkarmaya yardımcı olur.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Ekleme ve kaldırma yöntemlerinin zaman uyumsuz yürütmesi

`Groups.Add` ve `Groups.Remove` yöntemleri zaman uyumsuz olarak yürütülür. Bir gruba bir istemci eklemek ve grubu kullanarak istemciye hemen ileti göndermek istiyorsanız, `Groups.Add` yönteminin önce tamamlandığından emin olmanız gerekir. Aşağıdaki kod örneklerinde bunun nasıl yapılacağı, biri .NET 4,5 ' de çalıştırılan kodu kullanarak ve bir diğeri de .NET 4 ' te çalıştırılan kod kullanılarak gösterilmektedir

**.NET 4,5 örneği**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

**.NET 4 örneği**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>Grup üyeliği kalıcılığı

SignalR, kullanıcıları değil bağlantıları izler, bu nedenle Kullanıcı her bağlantı kurduğunda bir kullanıcının aynı grupta olmasını istiyorsanız, Kullanıcı her yeni bağlantı kurduğunda `Groups.Add` çağırmanız gerekir.

Geçici bir bağlantı kaybı sonrasında, bazı durumlarda SignalR bağlantıyı otomatik olarak geri yükleyebilir. Bu durumda, SignalR aynı bağlantıyı geri yüklüyor, yeni bir bağlantı oluşturmamalıdır ve istemcinin grup üyeliği otomatik olarak geri yüklenir. Bu durum, geçici kesme sunucu yeniden başlatma veya başarısızlık nedeniyle bile, grup üyelikleri de dahil olmak üzere her bir istemcinin bağlantı durumu istemciye yuvarlandığı için mümkündür. Bir sunucu kapalıysa ve bağlantı zaman aşımına uğramadan önce yeni bir sunucu tarafından değiştirilirse, istemci otomatik olarak yeni sunucuya yeniden bağlanabilir ve üyesi olan gruplara yeniden kaydolabilir.

Bağlantı kesilirse veya bağlantı zaman aşımına uğrarsa ya da istemcinin bağlantısı kesildiğinde (örneğin, bir tarayıcı yeni bir sayfaya gittiğinde) bir bağlantı otomatik olarak geri yüklenemediğinde, grup üyelikleri kaybedilir. Kullanıcı bir sonraki sefer bağlanışında yeni bir bağlantı olur. Aynı kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini sürdürmek için, uygulamanız kullanıcılar ve gruplar arasındaki ilişkilendirmeleri izlemek ve Kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini geri yüklemek için gerekir.

Bağlantılar ve yeniden bağlantılar hakkında daha fazla bilgi için, bu konunun ilerleyen kısımlarında yer alarak [Merkez sınıfında bağlantı ömrü olaylarını işleme](#connectionlifetime) bölümüne bakın.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>Tek Kullanıcı grupları

SignalR kullanan uygulamalar genellikle hangi kullanıcının bir ileti gönderdiğini ve hangi kullanıcıların bir ileti aldıklarını bilmek için kullanıcılar ve bağlantılar arasındaki ilişkilendirmeleri takip etmelidir. Gruplar, bunu yapmak için yaygın olarak kullanılan iki desenden birinde kullanılır.

- Tek Kullanıcı grupları.

    Kullanıcı adını Grup adı olarak belirtebilir ve Kullanıcı her bağlandığında veya yeniden bağlandığında geçerli bağlantı KIMLIĞINI gruba ekleyebilirsiniz. Gruba göndereceğiniz kullanıcıya ileti göndermek için. Bu yöntemin bir dezavantajı, grubun, kullanıcının çevrimiçi veya çevrimdışı olduğunu anlamak için bir yol sağlamamasıdır.
- Kullanıcı adlarıyla bağlantı kimlikleri arasındaki ilişkilendirmeleri izleyin.

    Her Kullanıcı adı ile bir veya daha fazla bağlantı kimliği arasında bir ilişki veya bir sözlükte veya veritabanında bir ilişki saklayabilir ve Kullanıcı her bağlanıp bağlantısı kesildiğinde depolanan verileri güncelleştirebilirsiniz. Kullanıcıya ileti göndermek için bağlantı kimliklerini belirtin. Bu yöntemin bir dezavantajı daha fazla bellek kaplar.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>Hub sınıfında bağlantı ömrü olaylarını işleme

Bağlantı ömrü olaylarının işlenmesinin tipik nedenleri, bir kullanıcının bağlanıp bağlanmadığını ve Kullanıcı adları ile bağlantı kimlikleri arasındaki ilişkilendirmeyi takip etmesidir. İstemciler bağlandığında veya bağlantıyı kestikten sonra kendi kodunuzu çalıştırmak için, aşağıdaki örnekte gösterildiği gibi hub sınıfının `OnConnected`, `OnDisconnected`ve `OnReconnected` sanal yöntemlerini geçersiz kılın.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>OnConnected, OnConnected ve OnConnected çağrıldığında

Her tarayıcı yeni bir sayfaya gittiğinde, yeni bir bağlantı kurulması gerekir. Bu, SignalR 'in, `OnDisconnected` yöntemi ve ardından `OnConnected` yöntemi tarafından yürütüleceği anlamına gelir. SignalR yeni bir bağlantı oluşturulduğunda her zaman yeni bir bağlantı KIMLIĞI oluşturur.

`OnReconnected` yöntemi, bir kablonun geçici olarak kesilmesi ve bağlantı zaman aşımına uğramadan önce yeniden bağlanması gibi, SignalR 'nin otomatik olarak kurtarabileceği bir bağlantıda geçici bir kesme olduğunda çağrılır. `OnDisconnected` yöntemi, istemcinin bağlantısı kesildiğinde çağrılır ve bir tarayıcı yeni bir sayfaya gittiğinde, SignalR otomatik olarak yeniden bağlanamaz. Bu nedenle, belirli bir istemci için olası bir olay dizisi `OnConnected`, `OnReconnected``OnDisconnected`; ya da `OnConnected``OnDisconnected`. Belirli bir bağlantı için sıra `OnConnected`, `OnDisconnected``OnReconnected` görmezsiniz.

`OnDisconnected` yöntemi, bir sunucunun kapanması ya da uygulama etki alanının geri dönüştürülmesi gibi bazı senaryolarda çağrılmaz. Başka bir sunucu satır üzerine geldiğinde veya uygulama etki alanının geri dönüşümü tamamlandığında, bazı istemciler `OnReconnected` olayı yeniden oluşturabilir ve tetiklenebilir.

Daha fazla bilgi için bkz. [SignalR 'de bağlantı ömrü olaylarını anlama ve işleme](index.md).

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>Çağıran durum doldurulmamış

Bağlantı ömrü olay işleyicisi yöntemleri sunucudan çağrılır, bu, istemcideki `state` nesnesine yerleştirdiğiniz herhangi bir durumun sunucudaki `Caller` özelliğinde doldurulmayacağı anlamına gelir. `state` nesnesi ve `Caller` özelliği hakkında daha fazla bilgi için, bu konunun ilerleyen kısımlarında [istemciler ve hub sınıfı arasında durum geçirme](#passstate) konusuna bakın.

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>Bağlam özelliğinden istemci hakkında bilgi alma

İstemci hakkında bilgi almak için, hub sınıfının `Context` özelliğini kullanın. `Context` özelliği, aşağıdaki bilgilere erişim sağlayan bir [Hubcallercontext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) nesnesi döndürür:

- Çağıran istemcinin bağlantı kimliği.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    Bağlantı KIMLIĞI, SignalR tarafından atanan bir GUID 'dir (değeri kendi kodunuzda belirtemezsiniz). Her bağlantı için bir bağlantı KIMLIĞI vardır ve uygulamanızda birden çok hub varsa, tüm Hub 'Lar tarafından aynı bağlantı KIMLIĞI kullanılır.
- HTTP üstbilgisi verileri.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    Ayrıca, `Context.Headers`HTTP üst bilgilerini de alabilirsiniz. Aynı şey için birden çok başvuru olmasının nedeni `Context.Headers` ilk olarak oluşturulmuştur, `Context.Request` özelliği daha sonra eklenmiştir ve `Context.Headers` geriye dönük uyumluluk için tutulmuştur.
- Sorgu dizesi verileri.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    `Context.QueryString`sorgu dizesi verilerini de alabilirsiniz.

    Bu özelliğe alacağınız sorgu dizesi, SignalR bağlantısını oluşturan HTTP isteğiyle birlikte kullanılmış olan bir dizedir. İstemciden sunucuya istemci hakkında verileri geçirmek için kullanışlı bir yol olan bağlantıyı yapılandırarak istemciye sorgu dizesi parametreleri ekleyebilirsiniz. Aşağıdaki örnek, oluşturulan proxy 'yi kullandığınızda JavaScript istemcisine bir sorgu dizesi eklemenin bir yolunu gösterir.

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    Sorgu dizesi parametreleri ayarlama hakkında daha fazla bilgi için, [JavaScript](index.md) ve [.net](index.md) istemcileri için API kılavuzlarını inceleyin.

    Sorgu dizesi verilerinde bağlantı için kullanılan aktarım yöntemini, SignalR tarafından dahili olarak kullanılan bazı diğer değerlerle birlikte bulabilirsiniz:

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    `transportMethod` değeri "webSockets", "serverSentEvents", "foreverFrame" veya "longPolling" olacaktır. Bu değeri `OnConnected` olay işleyicisi yönteminde denetlebileceğinizi unutmayın, bazı senaryolarda başlangıçta bağlantı için en son anlaşmalı aktarım yöntemi olmayan bir aktarım değeri alabilirsiniz. Bu durumda yöntem bir özel durum oluşturur ve daha sonra son taşıma yöntemi oluşturulduğunda yeniden çağrılacaktır.
- Özgü.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    `Context.RequestCookies`tanımlama bilgilerini de alabilirsiniz.
- Kullanıcı bilgileri.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- İstek için HttpContext nesnesi:

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    SignalR bağlantısı için `HttpContext` nesnesini almak üzere `HttpContext.Current` almak yerine bu yöntemi kullanın.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>İstemcilerle hub sınıfı arasında durum geçirme

İstemci proxy 'si, her yöntem çağrısıyla sunucuya aktarılmasını istediğiniz verileri depolayabilmeniz için bir `state` nesnesi sağlar. Sunucusunda, bu verilere istemciler tarafından çağrılan hub yöntemlerinde `Clients.Caller` özelliğindeki erişebilirsiniz. `Clients.Caller` özelliği, bağlantı ömrü olay işleyicisi yöntemleri `OnConnected`, `OnDisconnected`ve `OnReconnected`için doldurulmaz.

`state` nesnesindeki verileri oluşturma veya güncelleştirme ve `Clients.Caller` özelliği her iki yönde de kullanılabilir. Sunucudaki değerleri güncelleştirebilir ve istemciye geri geçirilir.

Aşağıdaki örnek, her yöntem çağrısıyla sunucuya iletilmek üzere durum depolayan JavaScript istemci kodunu gösterir.

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

Aşağıdaki örnek, bir .NET istemcisinde denk kodu gösterir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

Hub sınıfınız içinde, `Clients.Caller` özelliğindeki bu verilere erişebilirsiniz. Aşağıdaki örnek, önceki örnekte başvurulan durumu alan kodu gösterir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> Kalıcı duruma yönelik bu mekanizma, büyük miktarlarda veri için tasarlanmamıştır çünkü `state` veya `Clients.Caller` özelliğine yerleştirdiğiniz her şey, her yöntem çağrısı ile birlikte yuvarlama yaptığından. Kullanıcı adları veya sayaçlar gibi daha küçük öğeler için faydalıdır.

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>Hub sınıfında hataları işleme

Hub sınıfı yöntemleriniz içinde oluşan hataları işlemek için aşağıdaki yöntemlerden birini veya her ikisini kullanın:

- Yöntem kodunuzu try-catch bloklarına sarın ve özel durum nesnesini günlüğe kaydedin. Hata ayıklama amacıyla, özel durumu istemciye gönderebilirsiniz, ancak üretimde istemcilere ayrıntılı bilgi gönderilmesi için güvenlik nedenleriyle önerilmez.
- [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) yöntemini Işleyen bir hub işlem hattı modülü oluşturun. Aşağıdaki örnek, hataları kaydeden bir işlem hattı modülünü ve ardından modülü hub işlem hattına veren Global. asax dosyasındaki kodu gösterir.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

Merkez ardışık düzen modülleri hakkında daha fazla bilgi için, bu konunun ilerleyen bölümlerinde hub işlem hattını [Özelleştirme](#hubpipeline) bölümüne bakın.

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>İzlemeyi etkinleştirme

Sunucu tarafı izlemeyi etkinleştirmek için, aşağıdaki örnekte gösterildiği gibi, Web. config dosyanıza bir System. Diagnostics öğesi ekleyin:

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

Uygulamayı Visual Studio 'da çalıştırdığınızda, günlükleri **Çıkış** penceresinde görebilirsiniz.

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>İstemci yöntemlerini çağırma ve grupları hub sınıfı dışından yönetme

Hub sınıfınızın farklı bir sınıfından istemci yöntemlerini çağırmak için, Hub için SignalR bağlam nesnesine bir başvuru alın ve bunu istemci üzerindeki yöntemleri çağırmak veya grupları yönetmek için kullanın.

Aşağıdaki örnek `StockTicker` sınıfı, bağlam nesnesini alır, onu sınıfının bir örneğine depolar, sınıf örneğini statik bir özellikte depolar ve `StockTickerHub`adlı bir hub 'a bağlı istemcilerde `updateStockPrice` yöntemini çağırmak için singleton sınıfı örneğinden bağlamını kullanır.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

İçeriği uzun süreli bir nesnede birden çok kez kullanmanız gerekiyorsa, başvuruyu bir kez alın ve her seferinde yeniden almak yerine kaydedin. Bağlam bir kez alındıktan sonra, SignalR 'nin, hub yöntemlerinizin istemci yöntemi etkinleştirmeleri haline gelen aynı sıradaki istemcilere ileti göndermesi güvence altına alınır. Bir hub için SignalR bağlamını nasıl kullanacağınızı gösteren bir öğretici için, bkz. [ASP.NET SignalR Ile sunucu yayını](index.md).

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>İstemci yöntemlerini çağırma

Hangi istemcilerin RPC alacağını belirtebilirsiniz, ancak bir hub sınıfından çağrı yaparken daha az seçeneğiniz olur. Bunun nedeni, bağlamın bir istemciden gelen belirli bir çağrıyla ilişkilendirilmediği, yani `Clients.Others`veya `Clients.Caller`ya da `Clients.OthersInGroup`gibi geçerli bağlantı KIMLIĞI hakkında bilgi gerektiren tüm yöntemler kullanılamaz. Aşağıdaki seçenekler mevcuttur:

- Bağlanan tüm istemciler.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- Bağlantı KIMLIĞIYLE tanımlanan belirli bir istemci.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- Belirtilen istemciler dışındaki tüm bağlı istemciler, bağlantı KIMLIĞIYLE tanımlanır.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- Belirtilen bir gruptaki tüm bağlı istemciler.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- Belirtilen bir gruptaki, belirtilen istemciler hariç, bağlantı KIMLIĞIYLE tanımlanan tüm bağlı istemciler.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

Hub sınıfınızın metotlarından hub olmayan sınıfa çağrı yapıyorsanız, geçerli bağlantı KIMLIĞINI geçirebilir ve `Clients.Caller`, `Clients.Others`veya `Clients.OthersInGroup`benzetimini yapmak için `Clients.Client`, `Clients.AllExcept`veya `Clients.Group` ile kullanabilirsiniz. Aşağıdaki örnekte, `MoveShapeHub` sınıfı bağlantı KIMLIĞINI `Broadcaster` sınıfına geçirir `Broadcaster` sınıfının `Clients.Others`benzetimini yapabilir.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>Grup üyeliğini yönetme

Grupları yönetmek için bir hub sınıfında yaptığınız seçeneklerle aynı seçeneklere sahip olursunuz.

- Bir gruba istemci ekleme

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- Bir gruptan bir istemciyi kaldırma

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>Hub ardışık düzenini özelleştirme

SignalR, kendi kodunuzu hub işlem hattına eklemenizi sağlar. Aşağıdaki örnek, istemcisinde çağrılan her bir gelen yöntem çağrısını günlüğe kaydeden özel bir hub işlem hattı modülünü ve istemcide çağrılan giden yöntem çağrısını gösterir:

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

*Global. asax* dosyasında aşağıdaki kod, modülü hub işlem hattında çalışacak şekilde kaydeder:

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

Geçersiz kılabileceğiniz birçok farklı yöntem vardır. Tüm liste için bkz. [Hubpipelinemodule yöntemleri](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).
