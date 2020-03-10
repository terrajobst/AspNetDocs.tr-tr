---
uid: signalr/overview/older-versions/handling-connection-lifetime-events
title: SignalR 1. x içinde bağlantı ömrü olaylarını anlama ve Işleme Microsoft Docs
author: bradygaster
description: Bu makalede, hub API 'SI tarafından kullanıma sunulan olayların nasıl kullanılacağı açıklanır.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: e608e263-264d-448b-b0eb-6eeb77713b22
msc.legacyurl: /signalr/overview/older-versions/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 2fb671e730a1d41c07b350bf1d64ac1d0b1be55c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536906"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr-1x"></a>SignalR 1. x içinde bağlantı ömrü olaylarını anlama ve Işleme

by [Patrick Fletu](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, işleyebilmeniz gereken SignalR bağlantısı, yeniden bağlanma ve bağlantı kesme olayları ve yapılandırabileceğiniz zaman aşımı ve KeepAlive ayarları hakkında genel bir bakış sunulmaktadır.
> 
> Makalede, bir SignalR ve bağlantı ömrü olayları hakkında bilgi sahibi olduğunuz varsayılmaktadır. SignalR 'ye giriş için bkz. [SignalR-genel bakış-](index.md)Başlarken. Bağlantı ömrü olaylarının listesi için aşağıdaki kaynaklara bakın:
> 
> - [Hub sınıfında bağlantı ömrü olaylarını işleme](index.md)
> - [JavaScript istemcilerinde bağlantı ömrü olaylarını işleme](index.md)
> - [.NET istemcilerindeki bağlantı ömrü olaylarını işleme](index.md)

## <a name="overview"></a>Genel bakış

Bu makale aşağıdaki bölümleri içerir:

- [Bağlantı ömrü terimleri ve senaryoları](#terminology)

    - [SignalR bağlantıları, aktarım bağlantıları ve fiziksel bağlantılar](#signalrvstransport)
    - [Taşıma bağlantısının kesilmesi senaryoları](#transportdisconnect)
    - [İstemci bağlantısının kesilmesi senaryoları](#clientdisconnect)
    - [Sunucu bağlantısı kesme senaryoları](#serverdisconnect)
- [Zaman aşımı ve KeepAlive ayarları](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [DisconnectTimeout](#disconnecttimeout)
    - [Alı](#keepalive)
    - [Zaman aşımı ve KeepAlive ayarlarını değiştirme](#changetimeout)
- [Kullanıcıya, bağlantısı kesilme hakkında bildirme](#notifydisconnect)
- [Sürekli yeniden bağlanma](#continuousreconnect)
- [Sunucu kodundaki bir istemcinin bağlantısını kesme](#disconnectclientfromserver)

API başvuru konularına bağlantılar, API 'nin .NET 4,5 sürümüdür. .NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>Bağlantı ömrü terimleri ve senaryoları

Bir SignalR hub 'ındaki `OnReconnected` olay işleyicisi, belirli bir istemci için `OnDisconnected` sonra doğrudan `OnConnected` sonra çalıştırılabilir. Bağlantı kesilmesi olmadan bir yeniden bağlantınızın olması, SignalR 'de "bağlantı" sözcüğünün kullanıldığı birkaç yol olmasının nedenidir.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR bağlantıları, aktarım bağlantıları ve fiziksel bağlantılar

Bu makale, *SignalR bağlantıları*, *Aktarım bağlantıları*ve *fiziksel bağlantılar*arasında ayrım sağlayacaktır:

- **SignalR bağlantısı** , bir istemci ile sunucu URL 'si arasındaki, SIGNALR API 'si tarafından tutulan ve BIR bağlantı kimliğiyle benzersiz bir ilişki anlamına gelir. Bu ilişkiyle ilgili veriler SignalR tarafından korunur ve bir aktarım bağlantısı kurmak için kullanılır. İstemci `Stop` yöntemini çağırdığında ilişki sonlanır ve SignalR veya bir zaman aşımı sınırına ulaşıldığında, SignalR kayıp bir aktarım bağlantısını yeniden kurmaya çalışırken bu verilerin bir kısmını keser.
- **Aktarım bağlantısı** , bir istemci ile sunucu arasındaki, dört aktarım API 'si ile korunan bir mantıksal ilişki anlamına gelir: WebSockets, sunucu tarafından gönderilen olaylar, süresiz çerçeve veya uzun yoklama. SignalR bir aktarım bağlantısı oluşturmak için aktarım API 'sini kullanır ve aktarım API 'SI, aktarım bağlantısı oluşturmak için fiziksel bir ağ bağlantısının varlığına bağlıdır. SignalR bunu sonlandırdığında veya aktarım API 'SI fiziksel bağlantının kopuk olduğunu algıladığında aktarım bağlantısı sona erer.
- **Fiziksel bağlantı** , bir istemci bilgisayarı ile sunucu bilgisayarı arasındaki iletişimi kolaylaştıran fiziksel ağ bağlantıları--kablolar, kablosuz sinyaller, yönlendiriciler vb. anlamına gelir. Bir aktarım bağlantısı kurmak için fiziksel bağlantı bulunmalı ve bir SignalR bağlantısı kurmak için bir aktarım bağlantısı kurulması gerekir. Bununla birlikte, fiziksel bağlantının kesilmesi, bu konunun ilerleyen kısımlarında açıklanacak olan aktarım bağlantısını veya SignalR bağlantısını her zaman hemen sonlandırmaz.

Aşağıdaki diyagramda, SignalR bağlantısı hub API 'SI ve PersistentConnection API SignalR katmanı tarafından temsil edilir. aktarım bağlantısı, aktarımlar katmanıyla temsil edilir ve fiziksel bağlantı, sunucu arasındaki çizgilerle gösterilir ve istemciler.

![SignalR mimarisi diyagramı](handling-connection-lifetime-events/_static/image1.png)

Bir SignalR istemcisinde `Start` yöntemini çağırdığınızda, bir sunucuya fiziksel bağlantı kurmak için ihtiyaç duyduğunuz tüm bilgileri içeren SignalR istemci kodu sağladığınızda. SignalR istemci kodu, bir HTTP isteği oluşturmak ve dört taşıma yönteminden birini kullanan fiziksel bir bağlantı kurmak için bu bilgileri kullanır. Aktarım bağlantısı başarısız olursa veya sunucu başarısız olursa, istemci hala aynı SignalR URL 'sine yönelik yeni bir aktarım bağlantısını otomatik olarak yeniden oluşturmak için gereken bilgileri içerdiğinden, SignalR bağlantısı hemen kaybolur. Bu senaryoda, Kullanıcı uygulamasından bir müdahale yoktur ve SignalR istemci kodu yeni bir aktarım bağlantısı kurduğunda yeni bir SignalR bağlantısı başlatılmaz. SignalR bağlantısının sürekliliği, `Start` yöntemini çağırdığınızda oluşturulan bağlantı KIMLIĞININ değişmemesi durumunda yansıtılmıştır.

Hub 'daki `OnReconnected` olay işleyicisi, kaybedildikten sonra bir aktarım bağlantısı otomatik olarak yeniden oluşturulduğunda yürütülür. `OnDisconnected` olay işleyicisi bir SignalR bağlantısının sonunda yürütülür. Bir SignalR bağlantısı aşağıdaki yollarla bitebilirler:

- İstemci `Stop` yöntemini çağırırsa sunucuya bir Dur iletisi gönderilir ve hem istemci hem de sunucu, SignalR bağlantısını hemen sona erdir.
- İstemci ve sunucu arasındaki bağlantı kaybolduktan sonra istemci yeniden bağlanmaya çalışır ve sunucu istemcinin yeniden bağlanmasını bekler. Yeniden bağlantı girişimleri başarısız olursa ve kesme zaman aşımı süresi sona erdiğinde, hem istemci hem de sunucu SignalR bağlantısını sonlandırır. İstemci yeniden bağlanmaya çalışmayı durduruyor ve sunucu, SignalR bağlantısının temsilini ortadan kaldırmaktadır.
- İstemci, `Stop` yöntemini çağırma şansı olmadan çalışmayı durdursa, sunucu istemcinin yeniden bağlanmasını bekler ve ardından kesme zaman aşımı süresinden sonra SignalR bağlantısını sonlandırır.
- Sunucu çalışmayı durdurduktan sonra, istemci yeniden bağlanmaya çalışır (aktarım bağlantısını yeniden oluşturun) ve ardından kesme zaman aşımı süresinden sonra SignalR bağlantısını sonlandırır.

Herhangi bir bağlantı sorunu olmadığında ve Kullanıcı uygulaması `Stop` yöntemini çağırarak SignalR bağlantısını sonlandırıyorsa, SignalR bağlantısı ve aktarım bağlantısı aynı anda başlar ve biter. Aşağıdaki bölümlerde diğer senaryolar daha ayrıntılı olarak açıklanır.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>Taşıma bağlantısının kesilmesi senaryoları

Fiziksel bağlantılar yavaş olabilir veya bağlantıda kesintiler olabilir. Kesinti uzunluğu gibi faktörlere bağlı olarak, aktarım bağlantısı bırakılmış olabilir. SignalR daha sonra aktarım bağlantısını yeniden kurmaya çalışır. Bazen aktarım bağlantısı API 'SI kesintiyi algılar ve aktarım bağlantısını bırakır ve SignalR bağlantının kaybolduğunu hemen bulur. Diğer senaryolarda, aktarım bağlantısı API 'SI veya SignalR, bağlantının kaybedildiğinden hemen haberdar değildir. Uzun yoklama haricinde tüm aktarımlar için, SignalR istemcisi, aktarım API 'sinin algılayamayacağı bağlantı kaybını denetlemek için *KeepAlive* adlı bir işlev kullanır. Uzun yoklama bağlantıları hakkında daha fazla bilgi için bu konunun ilerleyen bölümlerindeki [zaman aşımı ve KeepAlive ayarları](#timeoutkeepalive) bölümüne bakın.

Bir bağlantı etkin olmadığında, sunucu, düzenli aralıklarla istemciye bir canlı tutma paketi gönderir. Bu makalenin yazıldığı tarihten itibaren, varsayılan sıklık her 10 saniyedir. İstemciler, bu paketleri dinleyerek bir bağlantı sorunu olup olmadığını söyleyebilir. Beklendiğinde bir KeepAlive paketi alınmadığında, istemci kısa bir süre sonra yavaşlık veya kesintiler gibi bağlantı sorunları olduğunu varsaymaz. KeepAlive, daha uzun bir süre sonra alınmadıysa, istemci bağlantının bırakılmakta olduğunu varsayar ve yeniden bağlanmaya çalışmaya başlar.

Aşağıdaki diyagramda, aktarım API 'SI tarafından hemen tanınmayan fiziksel bağlantıyla ilgili sorunlar olduğunda tipik bir senaryoda oluşturulan istemci ve sunucu olayları gösterilmektedir. Diyagram aşağıdaki durumlar için geçerlidir:

- Taşıma WebSockets, süresiz çerçeve veya sunucu tarafından gönderilen olaylardır.
- Fiziksel ağ bağlantısında farklı bir kesinti dönemi vardır.
- Aktarım API 'SI kesintileri bilmez, bu nedenle SignalR bunları algılamak için canlı tutma işlevselliğine bağımlıdır.

![Aktarım bağlantılarını kaldır](handling-connection-lifetime-events/_static/image2.png)

İstemci yeniden bağlanma moduna geçtiğinde ancak bağlantı kesme zaman aşımı sınırı içinde bir aktarım bağlantısı kuramazsa, sunucu SignalR bağlantısını sonlandırır. Bu gerçekleştiğinde sunucu, hub 'ın `OnDisconnected` yöntemini yürütür ve istemcinin daha sonra bağlanmayı yönetmesi durumunda istemciye göndermek için bir bağlantı kesme iletisi sıraya alır. İstemci daha sonra yeniden bağlanırsa, bağlantıyı kes komutunu alır ve `Stop` yöntemini çağırır. Bu senaryoda, istemci yeniden bağlandığında `OnReconnected` yürütülmez ve istemci `Stop`çağırdığında `OnDisconnected` yürütülmez. Aşağıdaki diyagramda bu senaryo gösterilmektedir.

![Aktarım kesintilerini-sunucu zaman aşımı](handling-connection-lifetime-events/_static/image3.png)

İstemcide ortaya çıkarılan SignalR bağlantı ömrü olayları şunlardır:

- istemci olayı `ConnectionSlow`.

    En son ileti veya KeepAlive ping alındıktan sonra canlı tutma zaman aşımı süresi için önceden ayarlanmış bir oran geçtiğinde tetiklenir. Varsayılan canlı tutma zaman aşımı uyarı dönemi, KeepAlive zaman aşımının 2/3 ' dir. Canlı tutma zaman aşımı 20 saniyedir, bu nedenle uyarı yaklaşık 13 saniye içinde gerçekleşir.

    Varsayılan olarak, sunucu her 10 saniyede bir KeepAlive ping gönderir ve istemci, her 2 saniyede bir KeepAlive ping isteği gönderir (KeepAlive zaman aşımı değeri ve KeepAlive zaman aşımı uyarı değeri arasındaki fark).

    Aktarım API 'sinin bağlantısının kesilmesi durumunda, canlı tutma zaman aşımı uyarı süresi geçmeden önce SignalR bağlantısının kesilmesi hakkında bilgi alabilirsiniz. Bu durumda `ConnectionSlow` olayı oluşturulmaz ve SignalR doğrudan `Reconnecting` olayına gider.
- istemci olayı `Reconnecting`.

    (A) aktarım API 'SI bağlantının kaybolduğunu algıladığında veya (b) son ileti veya KeepAlive ping alındıktan sonra canlı tutma zaman aşımı süresi geçtiğinde tetiklenir. SignalR istemci kodu yeniden bağlanmaya çalışıyor. Bir aktarım bağlantısı kesildiğinde uygulamanızın bazı işlemleri yapması istiyorsanız bu olayı işleyebilirsiniz. Varsayılan canlı tutma zaman aşımı süresi 20 saniyedir.

    SignalR yeniden bağlanma modundayken istemci kodunuz bir hub yöntemi çağırmaya çalışırsa, SignalR komutu göndermeyi dener. Çoğu zaman, bu tür denemeler başarısız olur, ancak bazı durumlarda başarılı olabilir. Sunucu tarafından gönderilen olaylar, süresiz çerçeve ve uzun yoklama aktarımları için, SignalR iki iletişim kanalı kullanır, biri istemcinin iletileri göndermek için kullandığı bir ileti ve iletiyi almak için kullandığı bir tane. Alma için kullanılan kanal kalıcı olarak açılır ve fiziksel bağlantı kesintiye uğradığında kapalı olur. Gönderme için kullanılan kanal kullanılabilir durumda kalır, bu nedenle fiziksel bağlantı geri yüklenirse, alma kanalının yeniden kurulması için istemciden sunucuya bir yöntem çağrısı başarılı olabilir. SignalR, almak için kullanılan kanalı yeniden açıncaya kadar dönüş değeri alınmaz.
- istemci olayı `Reconnected`.

    Aktarım bağlantısı yeniden kurulduğunda tetiklenir. Hub 'daki `OnReconnected` olay işleyicisi yürütülür.
- istemci olayı `Closed` (JavaScript 'te`disconnected` olayı).

    SignalR istemci kodu aktarım bağlantısını kaybetmeden sonra yeniden bağlanmaya çalışırken kesme zaman aşımı süresi dolduğunda tetiklenir. Varsayılan bağlantı kesme zaman aşımı 30 saniyedir. (Bu olay, `Stop` yöntemi çağrıldığı için bağlantı sona erdiğinde da tetiklenir.)

Aktarım API 'SI tarafından algılanmayan aktarım bağlantısı kesintileri; canlı tutma zaman aşımı uyarısı süresinden daha uzun bir süre için sunucudan canlı tutma pinglerinin alımına hiçbir bağlantı ömrü olaylarının oluşturulmasına neden olmayabilir.

Bazı ağ ortamları, boştaki bağlantıları kasıtlı olarak kapatır ve canlı tutma paketlerine ait başka bir işlev, bu ağların bir SignalR bağlantısının kullanımda olduğunu bilmesini sağlayarak bunu önlemeye yardımcı olur. Olağanüstü durumlarda, varsayılan canlı tutma ping işlemleri, kapalı bağlantıları engellemek için yeterli olmayabilir. Bu durumda, canlı tutma pingleri daha sık gönderilmek üzere yapılandırabilirsiniz. Daha fazla bilgi için bu konunun ilerleyen kısımlarında [zaman aşımı ve KeepAlive ayarları](#timeoutkeepalive) bölümüne bakın.

> [!NOTE] 
> 
> [!IMPORTANT]
> Burada açıklanan olay sırası garanti edilmez. SignalR her zaman, bu düzene göre öngörülebilir bir şekilde bağlantı ömrü olayları oluşturma girişiminde bulunur, ancak ağ olaylarının çok çeşitli çeşitlemeleri ve taşıma API 'Leri gibi temel iletişim çerçevelerinin bunları işlemesi gibi birçok yol vardır. Örneğin, istemci yeniden bağlandığında `Reconnected` olayı görüntülenmeyebilir veya bağlantı kurma girişimi başarısız olduğunda sunucudaki `OnConnected` işleyicisi çalıştırılabilir. Bu konu, yalnızca belirli tipik koşullarda normalde üretilmekte olan etkileri açıklamaktadır.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>İstemci bağlantısının kesilmesi senaryoları

Bir tarayıcı istemcisinde, bir SignalR bağlantısını koruyan SignalR istemci kodu bir Web sayfasının JavaScript bağlamında çalışır. Bu nedenle, bir sayfadan diğerine gittiğinizde SignalR bağlantısının bitmesi ve birden çok tarayıcı penceresi veya sekmeden bağlanıyorsanız birden çok bağlantı kimliğiyle birden çok bağlantınız olması neden vardır. Kullanıcı bir tarayıcı penceresini veya sekmeyi kapattığında veya yeni bir sayfaya gittiğinde veya sayfayı yenilediğinde, SignalR istemci kodu bu tarayıcı olayını sizin için işletiğinden ve `Stop` yöntemi çağırdığından, SignalR bağlantısı hemen sona erer. Bu senaryolarda veya uygulamanız `Stop` yöntemini çağırdığında, `OnDisconnected` olay işleyicisi sunucuda hemen yürütülür ve istemci `Closed` olayını başlatır (olay, JavaScript 'te `disconnected` olarak adlandırılır).

Bir istemci uygulaması veya üzerinde çalıştığı bilgisayar kilitlenirse veya uyku moduna geçtiğinde (örneğin, Kullanıcı dizüstü bilgisayarı kapattığında), sunucu ne olduğunu bilgilenmez. Sunucu bildiği kadar, istemcinin kaybı bağlantı kesintiden kaynaklanabilir ve istemci yeniden bağlanmaya çalışıyor olabilir. Bu nedenle, bu senaryolarda sunucu istemciye yeniden bağlanma şansı vermesini bekler ve `OnDisconnected`, bağlantı kesme zaman aşımı süresi dolana kadar (varsayılan olarak yaklaşık 30 saniye) yürütülmez. Aşağıdaki diyagramda bu senaryo gösterilmektedir.

![İstemci bilgisayar hatası](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>Sunucu bağlantısı kesme senaryoları

Bir sunucu çevrimdışı olduğunda, yeniden başlatılır, başarısız olur, uygulama etki alanı geri dönüştürme, vb.--sonuç, kayıp bir bağlantıya benzer olabilir veya aktarım API 'SI ile SignalR, sunucunun hemen olduğunu biliyor olabilir ve SignalR `ConnectionSlow` olayını oluşturmadan yeniden bağlanmaya başlayabilir. İstemci yeniden bağlama moduna geçtiğinde ve sunucu kurtarıldığında veya yeniden başlatılırsa veya bağlantı kesme zaman aşımı süresi dolmadan önce yeni bir sunucu çevrimiçi hale getirildiyse, istemci geri yüklenen veya yeni sunucuya yeniden bağlanır. Bu durumda, SignalR bağlantısı istemci üzerinde devam eder ve `Reconnected` olay oluşur. İlk sunucuda `OnDisconnected` hiçbir şekilde yürütülmez ve yeni sunucuda `OnReconnected` yürütülür, ancak bu sunucuda daha önce `OnConnected` bu istemci için hiçbir şekilde yürütülmedi. (Bir yeniden başlatma veya uygulama etki alanı geri dönüştürme sonrasında istemci aynı sunucuya yeniden bağlanırsa, bu, sunucu yeniden başlatıldığında önceki bağlantı etkinlikinden bellek olmadığından, bu efekt aynıdır.) Aşağıdaki diyagramda, taşıma API 'sinin kayıp bağlantıyı hemen haberdar ettiğini varsayar, bu nedenle `ConnectionSlow` olayı oluşturulmaz.

![Sunucu hatası ve yeniden bağlantı](handling-connection-lifetime-events/_static/image5.png)

Bir sunucu, bağlantı kesme zaman aşımı süresi içinde kullanılabilir duruma gelmezse, SignalR bağlantısı sona erer. Bu senaryoda, istemci üzerinde `Closed` olayı (JavaScript istemcilerinde`disconnected`) tetiklenir ancak sunucuda `OnDisconnected` hiçbir şekilde çağrılmaz. Aşağıdaki diyagramda, aktarım API 'sinin kayıp bağlantıyı bilmeyeceği varsayılmaktadır. bu nedenle, SignalR KeepAlive işlevselliği tarafından algılanır ve `ConnectionSlow` olay tetiklenir.

![Sunucu hatası ve zaman aşımı](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Zaman aşımı ve KeepAlive ayarları

Varsayılan `ConnectionTimeout`, `DisconnectTimeout`ve `KeepAlive` değerleri çoğu senaryo için uygundur, ancak ortamınız özel gereksinimleriniz varsa bu değiştirilebilir. Örneğin, ağ ortamınız 5 saniye boyunca boşta olan bağlantıları kapatırsa, KeepAlive değerini azaltmayı düşünebilirsiniz.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>connectionTimeout

Bu ayar, bir aktarım bağlantısının açık olarak ayrılma ve kapatmadan önce yanıt beklerken yeni bir bağlantı açılmadan önce bir yanıt beklediği süreyi temsil eder. Varsayılan değer 110 saniyedir.

Bu ayar yalnızca, normal olarak yalnızca uzun yoklama taşıması için geçerli olan KeepAlive işlevselliği devre dışı bırakıldığında geçerlidir. Aşağıdaki diyagramda, bu ayarın uzun bir yoklama aktarımı bağlantısında etkileri gösterilmektedir.

![Uzun yoklama taşıma bağlantısı](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>DisconnectTimeout

Bu ayar, `Disconnected` olayını oluşturmadan önce bir aktarım bağlantısı kaybedildikten sonra beklenecek süreyi temsil eder. Varsayılan değer 30 saniyedir. `DisconnectTimeout`ayarladığınızda, `KeepAlive` otomatik olarak `DisconnectTimeout` değerinin 1/3 olarak ayarlanır.

<a id="keepalive"></a>

### <a name="keepalive"></a>Alı

Bu ayar, boştaki bir bağlantı üzerinden bir KeepAlive paketi gönderilmeden önce beklenecek süreyi temsil eder. Varsayılan değer 10 saniyedir. Bu değer, `DisconnectTimeout` değerinin 1/3 ' inden büyük olmamalıdır.

Hem `DisconnectTimeout` hem de `KeepAlive`ayarlamak istiyorsanız `DisconnectTimeout`sonra `KeepAlive` ayarlayın. Aksi takdirde, `DisconnectTimeout` otomatik olarak zaman aşımı değerinin 1/3 `KeepAlive` ayarlandığında `KeepAlive` ayarınız üzerine yazılır.

Canlı tutma işlevini devre dışı bırakmak istiyorsanız `KeepAlive` null olarak ayarlayın. Canlı tutma işlevleri uzun yoklama taşıması için otomatik olarak devre dışıdır.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>Zaman aşımı ve KeepAlive ayarlarını değiştirme

Bu ayarların varsayılan değerlerini değiştirmek için, aşağıdaki örnekte gösterildiği gibi, bunları *Global. asax* dosyanızdaki `Application_Start` olarak ayarlayın. Örnek kodda gösterilen değerler varsayılan değerlerle aynıdır.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>Kullanıcıya, bağlantısı kesilme hakkında bildirme

Bazı uygulamalarda, bağlantı sorunları olduğunda kullanıcıya bir ileti görüntülenmesini isteyebilirsiniz. Bunun nasıl ve ne zaman yapılacağı konusunda birkaç seçeneğiniz vardır. Aşağıdaki kod örnekleri, oluşturulan proxy kullanan bir JavaScript istemcisi içindir.

- SignalR bağlantı sorunlarından haberdar olduğu anda, yeniden bağlanma moduna geçmeden önce bir iletiyi göstermek için `connectionSlow` olayını işleyin.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- SignalR 'nin bir bağlantısının kesilmesi olduğu ve yeniden bağlama moduna aldığı durumlarda ileti görüntülemesi için `reconnecting` olayını işleyin.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- Yeniden bağlanma girişimi zaman aşımına uğradığından bir iletiyi göstermek için `disconnected` olayını işleyin. Bu senaryoda, sunucu ile yeniden bağlantı kurmayı sağlayan tek yol, yeni bir bağlantı KIMLIĞI oluşturacak `Start` yöntemini çağırarak SignalR bağlantısını yeniden başlatmaktan daha kolay olacaktır. Aşağıdaki kod örneği, `Stop` yönteminin çağrılmasından kaynaklanan SignalR bağlantısına normal bir uçtan sonra değil, bildirimi yalnızca yeniden bağlama zaman aşımından sonra yayıntığınızdan emin olmak için bir bayrak kullanır.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>Sürekli yeniden bağlanma

Bazı uygulamalarda, kaybolduktan sonra otomatik olarak yeniden bağlantı kurmak isteyebilirsiniz ve yeniden bağlanma girişimi zaman aşımına uğradı. Bunu yapmak için, `Closed` olay işleyicinizden (JavaScript istemcilerinde`disconnected` olay işleyiciden) `Start` yöntemi çağırabilirsiniz. Sunucu veya fiziksel bağlantı kullanılamadığında bunu çok sık yapmamak için `Start` çağrılmadan önce bir süre beklemeniz gerekebilir. Aşağıdaki kod örneği, oluşturulan proxy kullanan bir JavaScript istemcisi içindir.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

Mobil istemcilerde farkında olabilecek olası bir sorun, sunucu veya fiziksel bağlantı kullanılamadığında sürekli yeniden bağlanma girişimlerinin gereksiz pil boşaltmasına neden olabilir.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>Sunucu kodundaki bir istemcinin bağlantısını kesme

SignalR sürüm 1.1.1, istemcilerin bağlantısını kesmek için yerleşik bir sunucu API 'SI içermez. [Gelecekte bu işlevselliği eklemeye yönelik planlar](https://github.com/SignalR/SignalR/issues/2101)vardır. Geçerli SignalR sürümünde, bir istemcinin sunucudan bağlantısının en kolay yolu, istemcide bir bağlantı kesme yöntemi uygulamak ve bu yöntemi sunucudan çağırmanız kullanmaktır. Aşağıdaki kod örneğinde, oluşturulan proxy 'yi kullanan bir JavaScript istemcisi için bir bağlantı kesme yöntemi gösterilmektedir.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> Güvenlik-istemcilerin bağlantısının kesilmesinin veya sunulan yerleşik API 'nin bu yöntemi, kötü amaçlı kod çalıştıran güvenliği olmayan istemcilerin senaryosuna yöneliktir, çünkü istemciler yeniden bağlanır veya güvenliği çıkarılan kod `stopClient` yöntemi kaldırabilir ya da BT 'nin yaptığı şeyi değiştirebilir. Durum bilgisi olmayan hizmet reddi (DOS) korumasını uygulamak için uygun yer, çerçeve veya sunucu katmanında değil, ön uç altyapısında değildir.
