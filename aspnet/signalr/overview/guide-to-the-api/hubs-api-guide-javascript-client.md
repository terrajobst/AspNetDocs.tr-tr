---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi | Microsoft Docs
author: bradygaster
description: Bu belgede, browsers ve Windows Mağazası (WinJS) Applicat gibi JavaScript istemcilerinde SignalR sürüm 2 için hub API 'sini kullanma hakkında bir giriş sunulmaktadır...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536661"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belgede, browsers ve Windows Mağazası (WinJS) uygulamaları gibi JavaScript istemcilerinde SignalR sürüm 2 için hub API 'sinin kullanılmasına bir giriş sunulmaktadır.
>
> SignalR hub 'Ları API 'SI, uzak yordam çağrılarını (RPC) bir sunucudan, istemcilerden ve istemcilerden sunucuya bağlı hale getirmenizi sağlar. Sunucu kodu ' nda, istemciler tarafından çağrılabilen Yöntemler tanımlar ve istemcide çalışan yöntemleri çağırabilirsiniz. İstemci kodunda, sunucudan çağrılabilen yöntemleri tanımlayabilir ve sunucuda çalışan yöntemleri çağırabilirsiniz. SignalR, sizin için istemciden sunucuya sıhhi kını ele alır.
>
> SignalR Ayrıca kalıcı bağlantılar adlı alt düzey bir API sunar. SignalR, hub 'Lar ve kalıcı bağlantılara giriş için bkz. [SignalR 'ye giriş](../getting-started/introduction-to-signalr.md).
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
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

## <a name="overview"></a>Genel bakış

Bu belgede aşağıdaki bölümler yer alır:

- [Oluşturulan ara sunucu ve sizin için ne yapar](#genproxy)

    - [Oluşturulan ara sunucu ne zaman kullanılır?](#cantusegenproxy)
- [İstemci kurulumu](#clientsetup)

    - [Dinamik olarak oluşturulan ara sunucuya başvurma](#dynamicproxy)
    - [SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma](#manualproxy)
- [Bağlantı kurma](#establishconnection)

    - [$. Connection. hub, $. hubConnection () tarafından oluşturulan nesnedir.](#connequivalence)
    - [Start yönteminin zaman uyumsuz yürütmesi](#asyncstart)
- [Etki alanları arası bağlantı kurma](#crossdomain)
- [Bağlantıyı yapılandırma](#configureconnection)

    - [Sorgu dizesi parametrelerini belirtme](#querystring)
    - [Taşıma yöntemini belirtme](#transport)
- [Hub sınıfı için proxy alma](#getproxy)
- [İstemcide sunucunun çağırabir yöntemi tanımlama](#callclient)
- [İstemciden sunucu yöntemlerini çağırma](#callserver)
- [Bağlantı ömrü olaylarını işleme](#connectionlifetime)
- [Hataları işleme](#handleerrors)
- [İstemci tarafı günlük kaydını etkinleştirme](#logging)

Sunucu veya .NET istemcilerini programlama hakkında belgeler için aşağıdaki kaynaklara bakın:

- [SignalR hub 'Ları API Kılavuzu-sunucu](hubs-api-guide-server.md)
- [SignalR hub 'Ları API Kılavuzu-.NET Istemcisi](hubs-api-guide-net-client.md)

SignalR 2 sunucu bileşeni yalnızca .NET 4,5 ' de kullanılabilir (ancak .NET 4,0 ' de SignalR 2 için bir .NET istemcisi vardır).

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>Oluşturulan ara sunucu ve sizin için ne yapar

Bir JavaScript istemcisini, bir SignalR hizmeti ile iletişim kurmak için, SignalR 'nin sizin için oluşturduğu bir ara sunucu olmadan veya olmadan iletişim kurmaya programlayabilirsiniz. Proxy 'nin ne için yaptığı, bağlanmak için kullandığınız kodun sözdizimini basitleştirecek, sunucunun çağırdığı yöntemleri yazacak ve sunucuda Yöntemler çağıracaklarınız.

Sunucu yöntemlerini çağırmak için kod yazdığınızda, oluşturulan ara sunucu, yerel bir işlev yürütüyorsunuz gibi görünen sözdizimini kullanmanıza olanak sağlar: `invoke('serverMethod', arg1, arg2)`yerine `serverMethod(arg1, arg2)` yazabilirsiniz. Oluşturulan proxy sözdizimi, bir sunucu yöntemi adını yanlış yazdığınız takdirde anında ve okunaklı bir istemci tarafı hatası da sunar. Proxy 'leri tanımlayan dosyayı el ile oluşturursanız, sunucu yöntemlerini çağıran kod yazmak için IntelliSense desteği de alabilirsiniz.

Örneğin, sunucusunda aşağıdaki hub sınıfına sahip olduğunuzu varsayalım:

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

Aşağıdaki kod örnekleri, sunucuda `NewContosoChatMessage` yöntemi çağırmak ve sunucudan `addContosoChatMessageToPage` yönteminin çağırmaları almak için hangi JavaScript kodunun göründüğünü gösterir.

**Oluşturulan ara sunucu ile**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**Oluşturulan proxy olmadan**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>Oluşturulan ara sunucu ne zaman kullanılır?

Sunucunun çağırdığı bir istemci yöntemi için birden çok olay işleyicisini kaydetmek istiyorsanız, oluşturulan proxy 'yi kullanamazsınız. Aksi takdirde, oluşturulan proxy 'yi kullanmayı seçebilirsiniz veya kodlama tercihinizi temel alan değil ' i seçebilirsiniz. Kullanmayı tercih ederseniz, istemci kodunuzda bir `script` öğesinde "SignalR/Hub" URL 'sine başvurmanız gerekmez.

<a id="clientsetup"></a>

## <a name="client-setup"></a>İstemci kurulumu

JavaScript istemcisi jQuery ve SignalR Core JavaScript dosyasına başvurular gerektirir. JQuery sürümü 1.6.4 veya 1.7.2, 1.8.2 veya 1.9.1 gibi büyük bir sonraki sürüm olmalıdır. Oluşturulan proxy 'yi kullanmaya karar verirseniz, SignalR tarafından oluşturulan ara sunucu JavaScript dosyası için de bir başvuruya ihtiyacınız vardır. Aşağıdaki örnek, başvuruların oluşturulan proxy 'yi kullanan bir HTML sayfasında nasıl görünebileceğini gösterir.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

Bu başvuruların bu sıraya dahil edilmesi gerekir: öncelikle jQuery, SignalR Core ve SignalR proxy 'lerinin son.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>Dinamik olarak oluşturulan ara sunucuya başvurma

Yukarıdaki örnekte, SignalR tarafından oluşturulan proxy 'nin başvurusu, fiziksel bir dosyaya değil, dinamik olarak oluşturulan JavaScript koduna sahiptir. SignalR, anında ara sunucu için JavaScript kodunu oluşturur ve "/SignalR/Hub" URL 'sine yanıt olarak istemciye hizmet verir. `MapSignalR` yönteminizin sunucusunda SignalR bağlantıları için farklı bir temel URL belirttiyseniz, dinamik olarak oluşturulan ara sunucu dosyasının URL 'SI, "/Hub" a eklenmiş olan özel URL 'niz olur.

> [!NOTE]
> Windows 8 (Windows Mağazası) JavaScript istemcileri için, dinamik olarak oluşturulan bir yerine fiziksel proxy dosyasını kullanın. Daha fazla bilgi için, bu konunun ilerleyen bölümlerinde [SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma](#manualproxy) konusuna bakın.

Bir ASP.NET MVC 4 veya 5 Razor görünümünde, proxy dosyası başvurunuz içindeki uygulama köküne başvurmak için tilde kullanın:

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

MVC 5 ' te SignalR kullanma hakkında daha fazla bilgi için bkz. [SignalR ve MVC 5 Ile çalışmaya](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)başlama.

Bir ASP.NET MVC 3 Razor görünümünde, proxy dosyası başvurunuz için `Url.Content` kullanın:

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

Bir ASP.NET Web Forms uygulamasında, proxy dosyası başvurunuz için `ResolveClientUrl` kullanın veya bir uygulama kökü göreli yolu (tilde ile başlayarak) kullanarak ScriptManager aracılığıyla kaydedin:

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

Genel bir kural olarak, CSS veya JavaScript dosyaları için kullandığınız "/SignalR/Hub" URL 'sini belirtmek için aynı yöntemi kullanın. Bir URL 'YI bir tilde kullanmadan belirtirseniz, bazı senaryolarda uygulamanız IIS Express kullanarak Visual Studio 'da test ettiğinizde doğru çalışacaktır ancak tam IIS 'e dağıtırken 404 hatasıyla başarısız olur. Daha fazla bilgi için MSDN sitesindeki [ASP.NET Web projeleri Için Visual Studio 'Daki Web sunucularındaki](https://msdn.microsoft.com/library/58wxa9w5.aspx) **kök düzeyindeki kaynaklara başvuruları çözme** konusuna bakın.

Visual Studio 2017 ' de bir Web projesini hata ayıklama modunda çalıştırdığınızda ve tarayıcınız olarak Internet Explorer kullanıyorsanız, proxy dosyasını **betikler**altında **Çözüm Gezgini** görebilirsiniz.

Dosyanın içeriğini görmek için **hub 'lara**çift tıklayın. Visual Studio 2012 veya 2013 ve Internet Explorer kullanmıyorsanız veya hata ayıklama modunda değilseniz, "/SignalR/Hub" URL 'sine giderek dosyanın içeriğini de alabilirsiniz. Örneğin, siteniz `http://localhost:56699`çalışıyorsa tarayıcınızda `http://localhost:56699/SignalR/hubs` gidin.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>SignalR tarafından oluşturulan ara sunucu için fiziksel bir dosya oluşturma

Dinamik olarak oluşturulan ara sunucuya alternatif olarak, proxy koduna sahip ve bu dosyaya başvuran bir fiziksel dosya oluşturabilirsiniz. Bu işlemi, önbelleğe alma veya paketleme davranışında denetim için ya da sunucu yöntemlerine yapılan çağrıları kodaktardığınızda IntelliSense 'i almak isteyebilirsiniz.

Bir proxy dosyası oluşturmak için aşağıdaki adımları gerçekleştirin:

1. [Microsoft. Aspnet. SignalR. utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet paketini yükler.
2. Bir komut istemi açın ve SignalR. exe dosyasını içeren *Araçlar* klasörüne gidin. Araçlar klasörü şu konumdadır:

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. Aşağıdaki komutu girin:

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *. Dll* dosyanızın yolu, genellikle proje klasörünüzdeki *bin* klasörüdür.

    Bu komut, *SignalR. exe*ile aynı klasörde *Server. js* adlı bir dosya oluşturur.
4. *Server. js* dosyasını projenize uygun bir klasöre yerleştirin, uygulamanız için uygun şekilde yeniden adlandırın ve "SignalR/hub 'lar" başvurusunun yerine buna bir başvuru ekleyin.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Bağlantı kurma

Bir bağlantı kurmadan önce, bir bağlantı nesnesi oluşturmanız, bir ara sunucu oluşturmanız ve sunucudan çağrılabilecek yöntemler için olay işleyicilerini kaydetmeniz gerekir. Proxy ve olay işleyicileri ayarlandığında, `start` yöntemini çağırarak bağlantıyı kurun.

Oluşturulan proxy 'yi kullanıyorsanız, oluşturulan proxy kodu sizin için yaptığından, bağlantı nesnesini kendi kodunuzda oluşturmanız gerekmez.

<a id="nogenconnection"></a>

**Bağlantı kurma (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**Bağlantı kurma (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/SignalR" URL 'sini kullanır. Farklı bir temel URL belirtme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-/SignalR URL 'si](hubs-api-guide-server.md#signalrurl).

Varsayılan olarak, hub konumu geçerli sunucusudur; farklı bir sunucuya bağlanıyorsanız, aşağıdaki örnekte gösterildiği gibi `start` yöntemi çağrılmadan önce URL 'YI belirtin:

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> Normalde, bağlantıyı kurmak için `start` yöntemi çağrılmadan önce olay işleyicilerini kaydedersiniz. Bağlantıyı kurduktan sonra bazı olay işleyicilerini kaydetmek istiyorsanız bunu yapabilirsiniz, ancak `start` yöntemi çağrılmadan önce olay işleyicilerden en az birini kaydetmeniz gerekir. Bunun bir nedeni, bir uygulamada birçok hub olabilir, ancak yalnızca bunlardan birine kullanacaksanız, her hub 'da `OnConnected` olayını tetiklemeniz istemezsiniz. Bağlantı oluşturulduğunda, bir hub proxy üzerinde istemci yönteminin bulunması, SignalR 'nin `OnConnected` olayını tetiklemesine söyleme yöntemidir. `start` yöntemi çağrılmadan önce herhangi bir olay işleyicisini kaydetmezseniz, Hub üzerinde Yöntemler çağırabileceksiniz, ancak hub 'ın `OnConnected` yöntemi çağrılmaz ve sunucudan hiçbir istemci yöntemi çağrılmaz.

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$. Connection. hub, $. hubConnection () tarafından oluşturulan nesnedir.

Örneklerden görebileceğiniz gibi, oluşturulan proxy 'yi kullandığınızda `$.connection.hub` bağlantı nesnesine başvurur. Bu, oluşturulan proxy 'yi kullanmadığınız zaman `$.hubConnection()` çağırarak elde ettiğiniz nesnedir. Oluşturulan proxy kodu, aşağıdaki ifadeyi yürüterek bağlantıyı sizin için oluşturur:

![Oluşturulan proxy dosyasında bağlantı oluşturma](hubs-api-guide-javascript-client/_static/image3.png)

Oluşturulan proxy 'yi kullanırken, oluşturulan proxy 'yi kullanmadığınız sırada bir bağlantı nesnesiyle yapabileceğiniz `$.connection.hub` her şeyi yapabilirsiniz.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>Start yönteminin zaman uyumsuz yürütmesi

`start` yöntemi zaman uyumsuz olarak yürütülür. Bir [jQuery ertelenmiş nesnesi](http://api.jquery.com/category/deferred-object/)döndürür; bu, `pipe`, `done`ve `fail`gibi yöntemleri çağırarak geri çağırma işlevleri ekleyebileceðiniz anlamına gelir. Bağlantı kurulduktan sonra, örneğin bir sunucu yöntemine yapılan çağrı gibi yürütmek istediğiniz kod varsa, bu kodu bir geri çağırma işlevine koyun veya bir geri çağırma işlevinden çağırın. `.done` geri çağırma yöntemi, bağlantı kurulduktan sonra ve sunucudaki `OnConnected` olay işleyicisi yönteminde bulunan herhangi bir kod yürütmeyi bitirdiğinde yürütülür.

Yukarıdaki örnekteki "Şimdi bağlandı" ifadesini, `start` yöntem çağrısından (`.done` bir geri çağırmadan değil) sonraki kod satırı olarak yerleştirirseniz, aşağıdaki örnekte gösterildiği gibi `console.log` satırı bağlantı oluşturulmadan önce yürütülür:

![Bağlantı kurulduktan sonra çalışan kodu yazmanın yanlış yolu](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>Etki alanları arası bağlantı kurma

Genellikle tarayıcı `http://contoso.com`bir sayfa yüklerse, SignalR bağlantısı aynı etki alanında, `http://contoso.com/signalr`. `http://contoso.com` sayfa, etki alanları arası bağlantı olan `http://fabrikam.com/signalr`bir bağlantı yapıyorsa. Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışıdır.

SignalR 1. x içinde, çapraz etki alanı istekleri tek bir EnableCrossDomain bayrağıyla denetlenir. Bu bayrak hem JSONP hem de CORS isteklerini denetlediniz. Daha fazla esneklik için, tüm CORS desteği, SignalR 'nin sunucu bileşeninden kaldırılmıştır (JavaScript istemcileri tarayıcının desteklediği algılanırsa CORS 'yi yine de kullanır) ve bu senaryoları desteklemek için yeni OWıN ara yazılımı kullanılabilir hale getirilir.

İstemci üzerinde JSONP gerekliyse (eski tarayıcılarda etki alanları arası istekleri desteklemek için), aşağıda gösterildiği gibi, `HubConfiguration` `true`nesnesindeki `EnableJSONP` ayarlanarak açıkça etkinleştirilmesi gerekecektir. JSONP, CORS 'den daha az güvenli olduğu için varsayılan olarak devre dışıdır.

**Projenize Microsoft. Owin. CORS ekleme:** Bu kitaplığı yüklemek için, Paket Yöneticisi konsolunda aşağıdaki komutu çalıştırın:

`Install-Package Microsoft.Owin.Cors`

Bu komut, paketin 2.1.0 sürümünü projenize ekler.

### <a name="calling-usecors"></a>UseCors çağrılıyor

 Aşağıdaki kod parçacığı, SignalR 2 ' de etki alanları arası bağlantıların nasıl uygulanacağını gösterir.

**SignalR 2 ' de etki alanları arası istekleri uygulama**

Aşağıdaki kod, bir SignalR 2 projesinde CORS veya JSONP 'nin nasıl etkinleştirileceğini göstermektedir. Bu kod örneği, `MapSignalR`yerine `Map` ve `RunSignalR` kullanır, böylece CORS ara yazılımı yalnızca CORS desteği gerektiren SignalR istekleri için çalışır (`MapSignalR`' de belirtilen yoldaki tüm trafik için değil.) Eşleme, uygulamanın tamamı yerine belirli bir URL öneki için çalıştırılması gereken diğer tüm ara yazılımlar için de kullanılabilir.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - Kodunuzda `jQuery.support.cors` true olarak ayarlama.
>
>     ![JQuery. support. CORS 'yi true olarak ayarlama](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR CORS kullanımını işler. `jQuery.support.cors` true olarak ayarlamak, SignalR 'nin tarayıcının CORS 'yi desteklediğini varsaymasına neden olduğundan JSONP 'yi devre dışı bırakır.
> - Bir localhost URL 'sine bağlanırken, Internet Explorer 10 bir etki alanları arası bağlantıyı düşünmez, bu nedenle sunucuda etki alanları arası bağlantıları etkinleştirmemiş olsanız bile, uygulama IE 10 ile yerel olarak çalışacaktır.
> - Internet Explorer 9 ile etki alanları arası bağlantıları kullanma hakkında daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)bakın.
> - Chrome ile etki alanları arası bağlantıları kullanma hakkında daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)bakın.
> - Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/SignalR" URL 'sini kullanır. Farklı bir temel URL belirtme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-/SignalR URL 'si](hubs-api-guide-server.md#signalrurl).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Bağlantıyı yapılandırma

Bir bağlantı kurmadan önce sorgu dizesi parametreleri belirtebilir veya taşıma yöntemini belirtebilirsiniz.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Sorgu dizesi parametrelerini belirtme

İstemci bağlandığı zaman sunucuya veri göndermek istiyorsanız, bağlantı nesnesine sorgu dizesi parametreleri ekleyebilirsiniz. Aşağıdaki örneklerde, istemci kodunda bir sorgu dizesi parametresinin nasıl ayarlanacağı gösterilmektedir.

**Start metodunu çağırmadan önce bir sorgu dizesi değeri ayarlayın (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**Start metodunu çağırmadan önce bir sorgu dizesi değeri ayarlayın (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

Aşağıdaki örnek, sunucu kodundaki bir sorgu dizesi parametresinin nasıl okunacağını gösterir.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Taşıma yöntemini belirtme

Bağlantı sürecinin bir parçası olarak, bir SignalR istemcisi normalde sunucu ve istemci tarafından desteklenen en iyi aktarımı tespit etmek üzere sunucuyla görüşür. Kullanmak istediğiniz taşımayı zaten biliyorsanız, `start` yöntemini çağırdığınızda Transport metodunu belirterek bu anlaşma sürecini atlayabilirsiniz.

**Taşıma yöntemini belirten istemci kodu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**Taşıma yöntemini belirten istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

Alternatif olarak, SignalR 'nin bunları denemesini istediğiniz sırada birden çok taşıma yöntemi belirtebilirsiniz:

**Özel bir taşıma geri dönüş şeması belirten istemci kodu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**Özel bir taşıma geri dönüş şeması belirten istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

Taşıma yöntemini belirtmek için aşağıdaki değerleri kullanabilirsiniz:

- WebSockets
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

Aşağıdaki örneklerde, bir bağlantı tarafından hangi taşıma yönteminin kullanıldığını nasıl bulacağınız gösterilmektedir.

**Bir bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**Bir bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

Sunucu kodundaki aktarım yöntemini denetleme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-bağlam özelliğinden istemci hakkında bilgi alma](hubs-api-guide-server.md#contextproperty). Aktarımlar ve geri göndermeler hakkında daha fazla bilgi için bkz. [SignalR 'ye giriş-aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>Hub sınıfı için proxy alma

Oluşturduğunuz her bağlantı nesnesi bir veya daha fazla hub sınıfı içeren bir SignalR hizmetine bağlantı hakkındaki bilgileri kapsüller. Bir hub sınıfıyla iletişim kurmak için kendi oluşturduğunuz (oluşturulan proxy kullanmıyorsanız) veya sizin için oluşturulan bir ara sunucu nesnesi kullanırsınız.

İstemci üzerinde, proxy adı hub sınıfı adının Camel bir sürümüdür. SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.

**Sunucudaki hub sınıfı**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**Hub için üretilen istemci ara sunucusuna bir başvuru alın**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**Hub sınıfı için istemci ara sunucusu oluşturma (oluşturulan proxy olmadan)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

Hub sınıfınızı bir `HubName` özniteliğiyle süslemek isterseniz, büyük/küçük harf durumunu değiştirmeden tam adı kullanın.

**HubName özniteliğine sahip sunucudaki hub sınıfı**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**Hub için üretilen istemci ara sunucusuna bir başvuru alın**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**Hub sınıfı için istemci ara sunucusu oluşturma (oluşturulan proxy olmadan)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>İstemcide sunucunun çağırabir yöntemi tanımlama

Sunucunun bir hub 'dan çağıracaı bir yöntemi tanımlamak için, oluşturulan proxy 'nin `client` özelliğini kullanarak hub proxy 'sine bir olay işleyicisi ekleyin veya oluşturulan proxy kullanmıyorsanız `on` yöntemini çağırın. Parametreler karmaşık nesneler olabilir.

Bağlantıyı kurmak için `start` yöntemini çağırmadan önce olay işleyicisini ekleyin. (`start` yöntemini çağırdıktan sonra olay işleyicileri eklemek istiyorsanız, bu belgede daha önce [bir bağlantı kurma](#establishconnection) bölümündeki nota bakın ve oluşturulan proxy 'yi kullanmadan bir yöntemi tanımlamak için gösterilen sözdizimini kullanın.)

Yöntem adı eşleştirme, büyük/küçük harfe duyarlıdır. Örneğin, sunucusundaki `Clients.All.addContosoChatMessageToPage`, istemcide `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`veya `addcontosochatmessagetopage` yürütülür.

**İstemci üzerinde yöntemi tanımlama (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**İstemci üzerinde yöntemi tanımlamanın alternatif yolu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**İstemci üzerinde yöntemi tanımlayın (oluşturulan ara sunucu olmadan veya başlangıç yöntemini çağırdıktan sonra eklenirken)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**İstemci yöntemini çağıran sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

Aşağıdaki örnekler, bir yöntem parametresi olarak karmaşık bir nesne içerir.

**İstemci üzerinde karmaşık bir nesne alan (oluşturulan ara sunucu ile) yöntemi tanımlayın**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**İstemci üzerinde karmaşık bir nesne alan (oluşturulan proxy olmadan) yöntemi tanımlayın**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**Karmaşık nesneyi tanımlayan sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**Karmaşık bir nesne kullanarak istemci yöntemini çağıran sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>İstemciden sunucu yöntemlerini çağırma

İstemciden bir sunucu yöntemi çağırmak için, oluşturulan proxy 'yi kullanmıyorsanız, oluşturulan ara sunucunun `server` özelliğini veya hub proxy üzerinde `invoke` yöntemini kullanın. Dönüş değeri veya parametreleri karmaşık nesneler olabilir.

Hub üzerindeki yöntem adının Camel bir sürümünü geçirin. SignalR, JavaScript kodunun JavaScript kurallarına uyum sağlamak için bu değişikliği otomatik olarak yapar.

Aşağıdaki örneklerde, dönüş değeri olmayan bir sunucu yönteminin nasıl çağrılacağını ve dönüş değerine sahip bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir.

**HubMethodName özniteliği olmayan sunucu yöntemi**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**Bir parametreye geçirilen karmaşık nesneyi tanımlayan sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

Hub yöntemini bir `HubMethodName` özniteliğiyle Süsleriniz durumunda bu adı, büyük/küçük harf olmadan kullanın.

HubMethodName özniteliğiyle **sunucu yöntemi**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

Yukarıdaki örneklerde, dönüş değeri olmayan bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir. Aşağıdaki örneklerde, dönüş değeri olan bir sunucu yönteminin nasıl çağrılacağını gösterilmektedir.

**Dönüş değerine sahip bir yöntem için sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

Dönüş değeri **için kullanılan hisse senedi sınıfı**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Bağlantı ömrü olaylarını işleme

SignalR, işleyebilmeniz için aşağıdaki bağlantı ömrü olaylarını sağlar:

- `starting`: bağlantı üzerinden herhangi bir veri gönderilmeden önce tetiklenir.
- `received`: bağlantıda herhangi bir veri alındığında tetiklenir. Alınan verileri sağlar.
- `connectionSlow`: istemci yavaş veya sık bir bırakma bağlantısı algıladığında tetiklenir.
- `reconnecting`: temeldeki aktarım yeniden bağlanmaya başladığında tetiklenir.
- `reconnected`: temeldeki aktarım yeniden bağlandığında tetiklenir.
- `stateChanged`: bağlantı durumu değiştiğinde tetiklenir. Eski durumu ve yeni durumu (bağlanma, bağlanma, yeniden bağlanma veya bağlantısı kesildi) sağlar.
- `disconnected`: bağlantının bağlantısı kesildiğinde tetiklenir.

Örneğin, dikkat çekici gecikmelere neden olabilecek bağlantı sorunları olduğunda uyarı iletilerini göstermek istiyorsanız `connectionSlow` olayını işleyin.

**Connectionlow olayını işle (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**Connectionlow olayını işle (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

Daha fazla bilgi için bkz. [SignalR 'de bağlantı ömrü olaylarını anlama ve işleme](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Hataları işleme

SignalR JavaScript istemcisi, için bir işleyici ekleyebileceğiniz bir `error` olayı sağlar. Ayrıca, bir sunucu yöntemi çağrısından kaynaklanan hatalara yönelik bir işleyici eklemek için Fail metodunu kullanabilirsiniz.

Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, bir hatadan sonra SignalR 'nin döndürdüğü özel durum nesnesi hata hakkında en az bilgi içerir. Örneğin, `newContosoChatMessage` çağrısı başarısız olursa, hata nesnesindeki hata iletisi, güvenlik nedenleriyle, üretim aşamasındaki istemcilere ayrıntılı hata iletileri gönderilmesi "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" içerir, ancak sorun giderme amacıyla ayrıntılı hata iletileri etkinleştirmek istiyorsanız, sunucuda aşağıdaki kodu kullanın.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

Aşağıdaki örnek, hata olayı için nasıl işleyicinin ekleneceğini gösterir.

**Hata işleyicisi ekleme (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**Hata işleyicisi ekleme (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

Aşağıdaki örnek, bir yöntem çağrısından bir hatanın nasıl işleneceğini gösterir.

**Yöntem çağrısından bir hata işleme (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**Yöntem çağrısından bir hata işleme (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

Bir yöntem çağrısı başarısız olursa, `error` olayı da oluşturulur, bu nedenle `error` yöntemi işleyicisindeki kodunuz ve `.fail` Yöntem geri çağırması yürütülür.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>İstemci tarafı günlük kaydını etkinleştirme

Bir bağlantıda istemci tarafı günlüğe kaydetmeyi etkinleştirmek için, bağlantıyı kurmak üzere `start` yöntemini çağırmadan önce bağlantı nesnesindeki `logging` özelliğini ayarlayın.

**Günlüğe kaydetmeyi etkinleştirme (oluşturulan ara sunucu ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**Günlüğe kaydetmeyi etkinleştir (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

Günlükleri görmek için tarayıcınızın geliştirici araçlarını açın ve konsol sekmesine gidin. Bunun nasıl yapılacağını gösteren adım adım yönergeleri ve ekran görüntülerini gösteren bir öğretici için, bkz. [ASP.NET SignalR Ile sunucu yayını-günlüğü etkinleştirme](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).
