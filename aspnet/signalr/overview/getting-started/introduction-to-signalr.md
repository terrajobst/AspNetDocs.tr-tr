---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 'ye giriş | Microsoft Docs
author: bradygaster
description: Bu makalede, SignalR 'nin ne olduğu ve oluşturmakta tasarlandığı bazı çözümlerin bazıları açıklanmaktadır.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536437"
---
# <a name="introduction-to-signalr"></a>SignalR’a Giriş

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, SignalR 'nin ne olduğu ve oluşturmakta tasarlandığı bazı çözümlerin bazıları açıklanmaktadır. 
> 
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
> 
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)'e gönderebilirsiniz.

## <a name="what-is-signalr"></a>SignalR nedir?

ASP.NET SignalR, uygulamalara gerçek zamanlı Web işlevselliği ekleme sürecini kolaylaştıran ASP.NET geliştiricileri için bir kitaplıktır. Gerçek zamanlı Web işlevselliği, sunucu kodunun bir istemcinin yeni veri istemesine beklemesini sağlamak yerine, bağlı istemciler için sunucu kodu gönderme içeriğini anında anında gönderebilme olanağıdır.

SignalR, ASP.NET uygulamanıza "gerçek zamanlı" bir Web işlevselliği sıralaması eklemek için kullanılabilir. Sohbet genellikle örnek olarak kullanıldığında, çok daha fazla şey yapabilirsiniz. Bir Kullanıcı yeni verileri görmek için bir Web sayfasını yenilediğinde veya sayfa yeni verileri almak için [uzun yoklamayı](http://en.wikipedia.org/wiki/Push_technology#Long_polling) uygularsa, SignalR kullanımı için bir adaydır. Panolar ve izleme uygulamaları, işbirliğine dayalı uygulamalar (belgelerin eşzamanlı düzenlemesi gibi), iş ilerleme durumu güncelleştirmeleri ve gerçek zamanlı formlar sayılabilir.

SignalR Ayrıca sunucudan yüksek frekanslı güncelleştirmeler gerektiren, örneğin gerçek zamanlı oyun gibi Web uygulamalarının tamamen yeni türlerini de mümkün kılıyor.

SignalR, sunucu tarafı .NET kodundan istemci tarayıcılarındaki JavaScript işlevlerini (ve diğer istemci platformları) çağıran sunucudan istemciye uzak yordam çağrıları (RPC) oluşturmaya yönelik basit bir API sağlar. SignalR ayrıca bağlantı yönetimi için API 'YI (örneğin, bağlantı ve bağlantı kesme olayları) ve gruplandırma bağlantılarını içerir.

![SignalR ile yöntemleri çağırma](introduction-to-signalr/_static/image1.png)

SignalR bağlantı yönetimini otomatik olarak işler ve aynı anda tüm bağlı istemcilere bir sohbet odası gibi iletiler yayınlamanızı sağlar. Ayrıca, belirli istemcilere iletiler gönderebilirsiniz. İstemci ve sunucu arasındaki bağlantı, her iletişim için yeniden kurulan klasik bir HTTP bağlantısının aksine kalıcıdır.

SignalR, bugün web 'de ortak olan istek-yanıt modeli yerine uzak yordam çağrılarını (RPC) kullanarak sunucu kodunun tarayıcıda istemci koduna çağırabileceği "sunucu gönderme" işlevini destekler.

SignalR uygulamaları yerleşik ve üçüncü taraf genişleme sağlayıcıları kullanarak binlerce istemciye ölçeklenebilir.

Yerleşik sağlayıcılar şunları içerir:
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

Üçüncü taraf sağlayıcıları şunları içerir:
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

SignalR, [GitHub](https://github.com/signalr)üzerinden erişilebilen açık kaynaklı bir kaynaktır.

## <a name="signalr-and-websocket"></a>SignalR ve WebSocket

SignalR, kullanılabilir olduğunda yeni WebSocket taşımasını kullanır ve gerektiğinde eski aktarımlara geri döner. Uygulamanızı doğrudan WebSocket kullanarak tamamen yazabiliyorsanız, SignalR kullanarak, uygulamanız gereken çok sayıda işlevselliğin sizin için zaten yapılması gerektiği anlamına gelir. En önemlisi bu, daha eski istemciler için ayrı bir kod yolu oluşturma konusunda endişelenmenize gerek kalmadan, uygulamanızı WebSocket 'ten yararlanmak üzere kodtabileceğiniz anlamına gelir. SignalR Ayrıca, uygulama WebSocket sürümlerinde tutarlı bir arabirim sağlayarak, SignalR, temel aktarımda yapılan değişiklikleri destekleyecek şekilde güncelleştirildiğinden WebSocket güncelleştirmeleri konusunda endişelenmenize kalkan.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>Aktarımlar ve geri göndermeler

SignalR, istemci ve sunucu arasında gerçek zamanlı çalışma yapmak için gereken aktarımlara göre soyutlamadır. Bir SignalR bağlantısı HTTP olarak başlar ve kullanılabiliyorsa bir WebSocket bağlantısına yükseltilir. WebSocket, en düşük gecikme süresine sahip olduğundan ve en alttaki özelliklere (istemci ve sunucu arasında tam çift yönlü iletişim gibi) sahip olduğundan, SignalR için ideal bir aktarımdır. Gereksinimler: WebSocket sunucunun Windows Server 2012 veya Windows 8 ve .NET Framework 4,5 kullanmasını gerektirir. Bu gereksinimler karşılanmazsa, SignalR, bağlantısını yapmak için diğer aktarımları kullanmayı dener.

### <a name="html-5-transports"></a>HTML 5 aktarımları

Bu aktarımlar [HTML 5](http://en.wikipedia.org/wiki/HTML5)desteğine bağlıdır. İstemci tarayıcısı HTML 5 standardını desteklemiyorsa, eski aktarımlar kullanılacaktır.

- **WebSocket** (hem sunucu hem de tarayıcı WebSocket destekleyebilecekleri anlamına gelebilir). WebSocket, istemci ve sunucu arasında doğru kalıcı, iki yönlü bir bağlantı kuran tek aktarımdır. Ancak, WebSocket en katı gereksinimlere da sahiptir; yalnızca Microsoft Internet Explorer, Google Chrome ve Mozilla Firefox 'un en son sürümlerinde tam olarak desteklenir ve yalnızca Opera ve Safari gibi diğer tarayıcılarda kısmi bir uygulamaya sahiptir.
- **Sunucu**tarafından gönderilen olaylar (tarayıcı, Internet Explorer hariç tüm tarayıcılar olan sunucu tarafından gönderilen olayları destekliyorsa).

### <a name="comet-transports"></a>Comet taşımaları

Aşağıdaki aktarımlar, bir tarayıcının veya başka bir istemcinin uzun süreli bir HTTP isteği tuttuğu, sunucunun istemciye özel olarak istekte bulunmaksızın veri göndermek için kullanabileceği, [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) Web uygulaması modelini temel alır.

- **Süresiz çerçeve** (yalnızca Internet Explorer için). Süresiz çerçeve, tamamlanmamış sunucudaki bir uç noktaya istek yapan gizli bir IFrame oluşturur. Sunucu daha sonra sürekli olarak yürütülen istemciye betiği gönderir ve sunucudan istemciye tek yönlü bir gerçek zamanlı bağlantı sağlar. İstemciden sunucuya bağlantı, sunucudan istemci bağlantısına ayrı bir bağlantı kullanır ve standart bir HTTP isteği gibi, gönderilmesi gereken her veri parçası için yeni bir bağlantı oluşturulur.
- **Ajax uzun yoklama**. Uzun yoklama kalıcı bir bağlantı oluşturmaz, bunun yerine sunucu yanıt verene kadar açık kalan bir istek ile sunucuyu yoklar, bu noktada bağlantı kapatılır ve hemen yeni bir bağlantı istenir. Bağlantı sıfırlarken bu bir gecikme süresine neden olabilir.

Hangi yapılandırmalardan hangilerinin desteklendiği hakkında daha fazla bilgi için bkz. [Desteklenen platformlar](supported-platforms.md).

### <a name="transport-selection-process"></a>Taşıma seçimi işlemi

Aşağıdaki listede, SignalR 'nin hangi taşımanın kullanılacağına karar vermek için kullandığı adımlar gösterilmektedir.

1. Tarayıcı Internet Explorer 8 veya daha önceki bir sürümdeyse, uzun yoklama kullanılır.
2. JSONP yapılandırıldıysa (yani, `jsonp` parametresi bağlantı başlatıldığında `true` olarak ayarlanırsa), uzun yoklama kullanılır.
3. Bir etki alanı bağlantısı yapılırsa (yani, SignalR uç noktası barındırma sayfasıyla aynı etki alanında değilse), aşağıdaki ölçütler karşılanıyorsa WebSocket kullanılacaktır:

   - İstemci CORS 'yi (çıkış noktaları arası kaynak paylaşımı) destekler. CORS 'yi destekleyen istemciler hakkında daha fazla bilgi için [caniuse.com adresindeki CORS](http://www.caniuse.com/CORS)bölümüne bakın.
   - İstemci WebSocket 'i destekliyor
   - Sunucu WebSocket 'i destekliyor

     Bu ölçütlerden herhangi biri karşılanmazsa, uzun yoklama kullanılacaktır. Etki alanları arası bağlantılar hakkında daha fazla bilgi için bkz. [etki alanları arası bağlantı oluşturma](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).
4. JSONP yapılandırılmamışsa ve bağlantı çapraz etki alanı değilse, hem istemci hem de sunucu destekliyorsa, WebSocket kullanılır.
5. İstemci veya sunucu WebSocket 'i desteklemiyorsa, varsa sunucu gönderme olayları kullanılır.
6. Sunucu gönderme olayları kullanılamıyorsa, süresiz kare denenir.
7. Süresiz çerçeve başarısız olursa uzun yoklama kullanılır.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>Taşımaları izleme

Kuruluşunuzda oturum açmayı etkinleştirerek ve konsol penceresini tarayıcınızda açarak uygulamanızın hangi aktarım türünü kullandığını belirleyebilirsiniz.

Hub 'ın bir tarayıcıdaki olayları için günlüğe kaydetmeyi etkinleştirmek üzere, istemci uygulamanıza aşağıdaki komutu ekleyin:

`$.connection.hub.logging = true;`

- Internet Explorer 'da F12 tuşuna basarak geliştirici araçlarını açın ve konsol sekmesine tıklayın.

    ![Microsoft Internet Explorer 'daki konsol](introduction-to-signalr/_static/image2.png)
- Chrome 'da, CTRL + SHIFT + J tuşlarına basarak konsolunu açın.

    ![Google Chrome 'daki konsol](introduction-to-signalr/_static/image3.png)

Konsol açık ve günlüğe kaydetme etkinken, SignalR tarafından hangi taşımanın kullanıldığını görebileceksiniz.

![Internet Explorer 'da WebSocket aktarımını gösteren konsol](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>Taşıma belirtme

Bir aktarım anlaşması, belirli bir süre ve istemci/sunucu kaynağı alır. İstemci özellikleri biliniyorsa, istemci bağlantısı başlatıldığında bir aktarım belirlenebilir. Aşağıdaki kod parçacığı, istemcinin başka bir protokolü desteklemeymediği biliniyorsa kullanılacak şekilde, Ajax uzun yoklama taşımasını kullanarak bir bağlantının başlatılmasını göstermektedir:

`connection.start({ transport: 'longPolling' });`

Bir istemcinin belirli aktarımları sırayla denemesini istiyorsanız, bir geri dönüş sırası belirtebilirsiniz. Aşağıdaki kod parçacığı WebSocket denemeyi ve doğrudan uzun yoklamaya devam eden başarısız olduğunu gösterir.

`connection.start({ transport: ['webSockets','longPolling'] });`

Aktarımları belirtmeye yönelik dize sabitleri aşağıdaki gibi tanımlanır:

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>Bağlantılar ve hub 'Lar

SignalR API 'SI istemciler ve sunucular arasında iletişim kurmak için iki model içerir: kalıcı bağlantılar ve hub 'Lar.

Bağlantı, tek alıcı, gruplandırılmış veya yayın iletileri göndermek için basit bir uç noktasını temsil eder. Kalıcı bağlantı API 'SI (PersistentConnection sınıfı tarafından .NET kodunda gösterilir), geliştiricilere, SignalR 'nin sunduğu alt düzey iletişim protokolüne doğrudan erişmesini sağlar. Bağlantılar iletişim modelinin kullanılması, Windows Communication Foundation gibi bağlantı tabanlı API 'Leri kullanmış olan geliştiricilere tanıdık gelecektir.

Hub, istemci ve sunucunuzun birbirlerine doğrudan Yöntemler çağırmasını sağlayan bağlantı API 'SI üzerinde oluşturulmuş daha yüksek düzey bir işlem hattdır. SignalR, makine sınırları arasında, MAGIC tarafından, istemcilerin sunucu üzerindeki yöntemleri kolayca yerel yöntemlerle çağırmalarına olanak sağlar ve tam tersi de geçerlidir. Hub iletişim modelinin kullanılması, .NET Remoting gibi uzaktan çağırma API 'Leri kullanmış olan geliştiricilere tanıdık gelecektir. Hub 'ın kullanılması Ayrıca yöntemlere türü kesin belirlenmiş parametreler geçirmenize izin verir ve model bağlamayı etkinleştirir.

### <a name="architecture-diagram"></a>Mimari diyagramı

Aşağıdaki diyagramda, taşıtlar, kalıcı bağlantılar ve aktarımlar için kullanılan temel teknolojiler arasındaki ilişki gösterilmektedir.

![API 'Leri, aktarımları ve istemcileri gösteren SignalR mimarisi diyagramı](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>Hub 'Lar nasıl çalışır?

Sunucu tarafı kod, istemcideki bir yöntemi çağırdığında, çağrılacak yöntemin adını ve parametrelerini içeren etkin aktarım genelinde bir paket gönderilir (bir nesne bir yöntem parametresi olarak gönderildiğinde JSON kullanılarak serileştirilir). İstemci daha sonra yöntem adıyla istemci tarafı kodda tanımlanan yöntemlerle eşleşir. Bir eşleşme varsa, istemci yöntemi serisi kaldırılan parametre verileri kullanılarak yürütülür.

Yöntem çağrısı, [Fiddler](http://fiddler2.com/) gibi araçlar kullanılarak izlenebilir. Aşağıdaki görüntüde, bir SignalR sunucusundan, Fiddler 'ın Günlükler bölmesinde bir Web tarayıcısı istemcisine gönderilen Yöntem çağrısı gösterilmektedir. Yöntem çağrısı, `MoveShapeHub`adlı bir hub 'dan gönderiliyor ve çağrılan yöntem `updateShape`olarak adlandırılır.

![SignalR trafiğini gösteren Fiddler günlüğünün görünümü](introduction-to-signalr/_static/image6.png)

Bu örnekte, hub adı `H` parametresiyle tanımlanır; Yöntem adı `M` parametresiyle tanımlanır ve yöntemine gönderilen veriler `A` parametresiyle tanımlanır. Bu iletiyi oluşturan uygulama [yüksek frekanslı gerçek zamanlı](tutorial-high-frequency-realtime-with-signalr.md) öğreticide oluşturulur.

### <a name="choosing-a-communication-model"></a>İletişim modeli seçme

Çoğu uygulama, hub API 'YI kullanmalıdır. Bağlantılar API 'SI aşağıdaki koşullarda kullanılabilir:

- Gönderilen gerçek ileti biçiminin belirtilmesi gerekir.
- Geliştirici bir mesajlaşma ile çalışmayı tercih eder ve bir uzaktan çağırma modeli yerine modeli gönderiyor.
- Mesajlaşma modeli kullanan mevcut bir uygulama, SignalR kullanmak için alınıyor.
