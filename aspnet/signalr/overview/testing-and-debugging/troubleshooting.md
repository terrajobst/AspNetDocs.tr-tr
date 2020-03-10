---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: SignalR sorunlarını giderme | Microsoft Docs
author: bradygaster
description: Bu makalede, SignalR uygulamaları geliştirmeyle ilgili yaygın sorunlar açıklanmaktadır.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: bcd273d839aed64ad2712eb503dd1942a2d4e355
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578829"
---
# <a name="signalr-troubleshooting"></a>SignalR Sorunlarını Giderme

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belgede, SignalR ile ilgili genel sorun giderme sorunları açıklanmaktadır.
>
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

Bu belge aşağıdaki bölümleri içerir.

- [İstemci ve sunucu arasındaki Yöntemler sessizce başarısız oluyor](#connection)
- [Etkin olmayan bir istemciyi algılamak için IIS WebSockets to ping/pong olarak yapılandırma](#pong)
- [Diğer bağlantı sorunları](#other)
- [Derleme ve sunucu tarafı hataları](#server)
- [Visual Studio sorunları](#vs)
- [Internet Information Services sorunları](#iis)
- [Microsoft Azure sorunları](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>İstemci ve sunucu arasındaki Yöntemler sessizce başarısız oluyor

Bu bölümde, istemci ve sunucu arasındaki yöntem çağrısının anlamlı bir hata iletisi olmadan başarısız olması olası nedenleri açıklanmaktadır. Bir SignalR uygulamasında, sunucuda istemcinin uyguladığı yöntemler hakkında bilgi bulunmamaktadır; sunucu bir istemci yöntemini çağırdığında, yöntem adı ve parametre verileri istemciye gönderilir ve yöntem yalnızca sunucunun belirtildiği biçimde varsa yürütülür. İstemcide eşleşen bir yöntem bulunamazsa hiçbir şey olmaz ve sunucuda hiçbir hata iletisi oluşturulmaz.

Çağrılmayan istemci yöntemlerini daha fazla araştırmak için, sunucudan hangi çağrıların geldiğini görmek üzere Hub üzerinde Start yöntemini çağırmadan önce günlüğe kaydetmeyi açabilirsiniz. Bir JavaScript uygulamasında günlüğe kaydetmeyi etkinleştirmek için bkz. [istemci tarafı günlük kaydını etkinleştirme (JavaScript istemci sürümü)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging). Bir .NET istemci uygulamasında günlüğe kaydetmeyi etkinleştirmek için bkz. [istemci tarafı günlük kaydını etkinleştirme (.NET istemci sürümü)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>Yanlış yazılmış Yöntem, yanlış Yöntem imzası veya yanlış hub adı

Çağrılan bir yöntemin adı veya imzası, istemcide uygun bir yöntemle tam olarak eşleşmiyorsa, çağrı başarısız olur. Sunucu tarafından çağrılan yöntem adının istemcideki yöntemin adıyla eşleştiğini doğrulayın. Ayrıca, SignalR, JavaScript 'e uygun olduğu gibi Camel-cased yöntemlerini kullanarak hub proxy 'sini oluşturur, bu nedenle sunucu üzerinde `SendMessage` adlı bir yöntem istemci proxy 'sinde `sendMessage` çağırılır. Sunucu tarafı kodunuzda `HubName` özniteliğini kullanıyorsanız, kullanılan adın istemcide hub oluşturmak için kullanılan adla eşleştiğini doğrulayın. `HubName` özniteliğini kullanmazsanız, bir JavaScript istemcisindeki hub 'ın adının ChatHub yerine chatHub gibi bir Camel-cased olduğunu doğrulayın.

### <a name="duplicate-method-name-on-client"></a>İstemcide yinelenen Yöntem adı

İstemcide yalnızca büyük/küçük harfe göre farklılık gösteren bir yinelenen Yöntem olmadığından emin olun. İstemci uygulamanızın `sendMessage`adlı bir yöntemi varsa, ayrıca `SendMessage` adlı bir yöntemin de olmadığını doğrulayın.

### <a name="missing-json-parser-on-the-client"></a>İstemcide eksik JSON ayrıştırıcısı

SignalR, sunucu ile istemci arasındaki çağrıları seri hale getirmek için bir JSON ayrıştırıcısı bulunmasını gerektirir. İstemcinizin yerleşik bir JSON ayrıştırıcısı yoksa (Internet Explorer 7 gibi), uygulamanıza bir tane eklemeniz gerekir. JSON ayrıştırıcısı [buradan](http://nuget.org/packages/json2)indirebilirsiniz.

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Hub ve PersistentConnection söz dizimini karıştırma

SignalR iki iletişim modeli kullanır: hub 'Lar ve PersistentConnections. Bu iki iletişim modelini çağırma söz dizimi, istemci kodunda farklıdır. Sunucu kodunuzda bir hub eklediyseniz, tüm istemci kodunuzun uygun hub sözdizimini kullandığını doğrulayın.

**JavaScript istemcisinde bir PersistentConnection oluşturan JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**Bir JavaScript istemcisinde hub proxy oluşturan JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**C#bir yolu PersistentConnection ile eşleyen sunucu kodu**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C#birden çok uygulamanız varsa, bir yolu hub 'a veya birden çok hub 'a eşleyen sunucu kodu**

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a>Abonelikler eklenmeden önce bağlantı başlatıldı

Sunucudan çağrılabilecek Yöntemler proxy 'ye eklendikten sonra hub 'ın bağlantısı başlatılırsa, iletiler alınmaz. Aşağıdaki JavaScript kodu hub 'ı düzgün olarak başlatmayacak:

**Hub iletilerinin alınmasına izin vermeyecek hatalı JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

Bunun yerine, Start çağrılmadan önce Yöntem aboneliklerini ekleyin:

**Bir hub 'a abonelikleri doğru şekilde ekleyen JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>Hub proxy 'sinde eksik Yöntem adı

Sunucuda tanımlanan yöntemin istemcide abone olduğunu doğrulayın. Sunucu, yöntemi tanımlasa da, istemci proxy 'sine yine de eklenmelidir. Yöntemler istemci proxy 'sine aşağıdaki yollarla eklenebilir (metodun doğrudan hub değil, hub 'ın `client` üyesine eklendiğini unutmayın):

**Bir hub proxy 'sine yöntemler ekleyen JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>Hub veya hub yöntemleri ortak olarak bildirilmemiş

İstemcide görünür olması için, hub uygulamasının ve yöntemlerinin `public`olarak bildirilmelidir.

### <a name="accessing-hub-from-a-different-application"></a>Farklı bir uygulamadan hub 'a erişme

SignalR hub 'Larına yalnızca SignalR istemcileri uygulayan uygulamalar üzerinden erişilebilir. SignalR diğer iletişim kitaplıklarıyla (SOAP veya WCF Web Hizmetleri gibi) birlikte çalışamaz.) Hedef platformunuz için uygun bir SignalR istemcisi yoksa, sunucunun uç noktasına doğrudan erişemezsiniz.

### <a name="manually-serializing-data"></a>Verileri el ile serileştirme

SignalR, yöntem parametrelerinizi seri hale getirmek için otomatik olarak JSON kullanır; bunu yapmanız gerekmez.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>Uzak hub yöntemi, OnConnected işlevindeki istemcide yürütülmedi

Bu davranış tasarım gereğidir. `OnDisconnected` çağrıldığında, hub, daha fazla hub yönteminin çağrılmasına izin verilmeyen `Disconnected` durumuna zaten girdi.

**C#Onbağlantısız olayda kodu doğru şekilde yürüten sunucu kodu**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a>OnDisconnect tutarlı zamanlarda tetikmedi

Bu davranış tasarım gereğidir. Bir Kullanıcı etkin bir SignalR bağlantısı olan bir sayfadan uzaklaşmaya çalıştığında, SignalR istemcisi sunucuya istemci bağlantısının durdurulduğunu bildirmek için bir en iyi çaba denemesi yapar. SignalR istemcisinin en iyi çaba denemesi sunucuya erişemediğinde, sunucu daha sonra `OnDisconnected` olayın tetikleneceği zamanda, yapılandırılabilir bir `DisconnectTimeout` sonra bağlantıyı atacaktır. SignalR istemcisinin en iyi çaba denemesi başarılı olursa `OnDisconnected` olay hemen başlatılır.

`DisconnectTimeout` ayarını ayarlama hakkında daha fazla bilgi için bkz. [bağlantı ömrü olaylarını işleme: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout).

### <a name="connection-limit-reached"></a>Bağlantı sınırına ulaşıldı

Windows 7 gibi bir istemci işletim sisteminde IIS 'nin tam sürümünü kullanırken, 10 bağlantı sınırı uygulanır. İstemci işletim sistemi kullanırken, bu sınırı önlemek için IIS Express kullanın.

### <a name="cross-domain-connection-not-set-up-properly"></a>Etki alanları arası bağlantı düzgün ayarlanmadı

Bir etki alanı bağlantısı (SignalR URL 'SI barındırma sayfasıyla aynı etki alanında olmayan bir bağlantı) doğru ayarlanmamışsa, bağlantı hata iletisi olmadan başarısız olabilir. Etki alanları arası iletişimin nasıl etkinleştirileceği hakkında bilgi için bkz. [etki alanları arası bağlantı oluşturma](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>NTLM (Active Directory) kullanılarak bağlantı .NET istemcisinde çalışmıyor

Bağlantı düzgün yapılandırılmamışsa, bir .NET istemci uygulamasındaki bağlantı etki alanı güvenliği kullanan bir bağlantı başarısız olabilir. Bir etki alanı ortamında SignalR kullanmak için, önkoşul bağlantısı özelliğini aşağıdaki gibi ayarlayın:

**C#bağlantı kimlik bilgilerini uygulayan istemci kodu**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a>Etkin olmayan bir istemciyi algılamak için IIS WebSockets to ping/pong olarak yapılandırma

SignalR sunucuları, istemcinin etkin olup olmadığını bilmez ve bağlantı hatalarıyla ilgili WebSocket 'den, diğer bir deyişle `OnClose` geri çağırmadan bildirimleri kullanır. Bu soruna yönelik bir çözüm, IIS WebSockets 'i sizin için ping/pong yapmak üzere yapılandırmaktır. Bu, bağlantınızın beklenmedik şekilde kesintiye karşı kapanmasını sağlar. Daha fazla bilgi için [Bu StackOverflow Post](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss)bölümüne bakın.

<a id="other"></a>

## <a name="other-connection-issues"></a>Diğer bağlantı sorunları

Bu bölümde, bir bağlantı sırasında oluşan belirli belirtilerin veya hata iletilerinin nedenleri ve çözümleri açıklanmaktadır.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>"Verilerin gönderilebilmesi için önce başlangıç çağrılmalıdır" hatası

Bu hata genellikle, kod, bağlantı başlatılmadan önce SignalR nesnelerine başvuruyorsa görülür. İşleyiciler için kablolanın ve sunucu üzerinde tanımlanan yöntemleri çağıran LIKE bağlantısı, bağlantı tamamlandıktan sonra eklenmelidir. `Start` çağrısının zaman uyumsuz olduğunu unutmayın, bu nedenle çağrıdan sonra kod, tamamlanmadan önce yürütülür. Bir bağlantının tamamen başlatıldıktan sonra işleyiciler eklemenin en iyi yolu, bunları başlangıç yöntemine parametre olarak geçirilen bir geri çağırma işlevine koymasıdır:

**SignalR nesnelerine başvuran olay işleyicilerini doğru şekilde ekleyen JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

Bu hata, SignalR nesnelerine hala başvurulurken bir bağlantı durdurulduğunda da görülür.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301 kalıcı olarak taşındı" veya "302 geçici olarak taşındı" hatası

Bu hata, proje SignalR adlı bir klasör içeriyorsa, otomatik olarak oluşturulan ara sunucu ile müdahale edecek şekilde görülebilir. Bu hatayı önlemek için, uygulamanızda `SignalR` adlı bir klasör kullanmayın veya otomatik proxy oluşturmayı kapatın. Daha fazla ayrıntı için [oluşturulan ara sunucuya ve ne işe yönelik](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) olarak bakın.

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET veya Silverlight istemcisinde "403 Yasak" hatası

Bu hata, etki alanları arası iletişimin düzgün şekilde etkinleştirilmediği etki alanı ortamlarında oluşabilir. Etki alanları arası iletişimin nasıl etkinleştirileceği hakkında bilgi için bkz. [etki alanları arası bağlantı oluşturma](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain). Bir Silverlight istemcisinde etki alanları arası bağlantı kurmak için bkz. [Silverlight istemcilerinden etki alanları arası bağlantılar](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).

### <a name="404-not-found-error"></a>"404 bulunamadı" hatası

Bu sorunun çeşitli nedenleri vardır. Aşağıdakilerin tümünü doğrulayın:

- **Hub proxy adresi başvurusu doğru biçimlendirilmedi:** Bu hata genellikle oluşturulan Merkez ara sunucu adresinin başvurusu doğru biçimlendirilmediyse görülür. Hub adresi başvurusunun düzgün şekilde yapıldığını doğrulayın. Ayrıntılar için [dinamik olarak oluşturulan ara sunucuya nasıl başvurulacağını](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) öğrenin.
- **Hub yolunu eklemeden önce uygulamaya rotalar ekleniyor:** Uygulamanız başka rotalar kullanıyorsa, eklenen ilk yolun `MapSignalR`çağrısı olduğunu doğrulayın.
- **Uzantısız URL 'ler için güncelleştirme olmadan IIS 7 veya 7,5 kullanma:** Sunucunun `/signalr/hubs`hub tanımlarına erişim sağlayabilmesi için IIS 7 veya 7,5 ' nin kullanılması, uzantısız eşle URL 'lerinin güncelleştirilmesini gerektirir. Güncelleştirme [burada](https://support.microsoft.com/kb/980368)bulunabilir.
- **IIS önbelleği güncel değil veya bozuk:** Önbellek içeriğinin güncel olmadığından emin olmak için, önbelleği temizlemek için bir PowerShell penceresinde aşağıdaki komutu girin:

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a>"500 iç sunucu hatası"

Bu, çok çeşitli nedenleri olabilecek çok sayıda genel hatadır. Hatanın ayrıntıları sunucunun olay günlüğünde görünmelidir veya sunucu hata ayıklaması aracılığıyla bulunabilir. Daha ayrıntılı hata bilgileri, sunucuda ayrıntılı hataları etkinleştirerek elde edilebilir. Daha fazla bilgi için bkz. [hub sınıfında hataları işleme](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).

Bu hata, bir güvenlik duvarı veya ara sunucu düzgün yapılandırılmamışsa, istek üstbilgilerinin yeniden yazılmasına neden olduğunda da yaygın olarak görülür. Çözüm, güvenlik duvarı veya proxy üzerinde 80 bağlantı noktası etkinleştirildiğinden emin olmak için kullanılır.

### <a name="unexpected-response-code-500"></a>"Beklenmeyen yanıt kodu: 500"

Uygulamada kullanılan .NET Framework sürümü, Web. config dosyasında belirtilen sürümle eşleşmezse bu hata oluşabilir. Çözüm, .NET 4,5 'nin hem uygulama ayarlarında hem de Web. config dosyasında kullanıldığını doğrulamadır.

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError: &lt;hubType&gt; tanımsız" hatası

`MapSignalR` çağrısı düzgün şekilde yapılmazlarsa bu hata oluşur. Daha fazla bilgi için bkz. [SignalR ara yazılımını kaydetme ve SignalR seçeneklerini yapılandırma](../guide-to-the-api/hubs-api-guide-server.md#route) .

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException Kullanıcı kodu tarafından işlenmedi

Yöntemlerinizi göndereceğiniz parametrelerin serileştirilebilir olmayan türler (Dosya tutamaçları veya veritabanı bağlantıları gibi) içermediği doğrulayın. İstemciye gönderilmesini istemediğiniz bir sunucu tarafı nesnesi üzerinde Üyeler kullanmanız gerekiyorsa (güvenlik veya serileştirme nedenleri için) `JSONIgnore` özniteliğini kullanın.

### <a name="protocol-error-unknown-transport-error"></a>"Protokol hatası: bilinmeyen aktarım" hatası

İstemci, SignalR 'nin kullandığı aktarımları desteklemiyorsa bu hata ortaya çıkabilir. SignalR ile hangi tarayıcıların kullanılabileceği hakkında bilgi için bkz. [taşıma ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports) .

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript hub ara sunucusu oluşturma devre dışı bırakıldı."

Bu hata, `signalr/hubs`konumundaki dinamik olarak oluşturulan ara sunucuya bir başvuru da dahil olmak üzere `DisableJavaScriptProxies` ayarlandıysa oluşur. Proxy 'yi el ile oluşturma hakkında daha fazla bilgi için bkz. [oluşturulan ara sunucu ve sizin için ne yapar](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"Bağlantı KIMLIĞI yanlış biçimde" veya "etkin bir SignalR bağlantısı sırasında Kullanıcı kimliği değiştirilemiyor" hatası

Kimlik doğrulaması kullanılıyorsa ve bağlantı durdurulmadan önce istemci günlüğe kaydedildiğinde bu hata görünebilir. Çözüm, istemciyi günlüğe kaydetmeden önce SignalR bağlantısını durdurmaktır.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"Yakalanamayan hata: SignalR: jQuery bulunamadı. Lütfen SignalR. JS dosyasından önce jQuery 'e başvurulduğundan emin olun "hata

SignalR JavaScript istemcisi jQuery 'yi çalıştırmak için gereklidir. JQuery başvurusunun doğru olduğunu, kullanılan yolun geçerli olduğunu ve jQuery 'e başvurunun SignalR başvurusundan önce olduğunu doğrulayın.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"Yakalanamayan TypeError: '&lt;özelliği&gt;' tanımsız" hatası okunamıyor

Bu hata, jQuery veya hub proxy 'sinin düzgün şekilde başvurulmasına neden olur. JQuery ve hub proxy 'sine yönelik başvurunun doğru olduğunu, kullanılan yolun geçerli olduğunu ve jQuery 'e başvurunun, hub proxy 'sine yönelik başvurudan önce olduğunu doğrulayın. Hub proxy 'sine yönelik varsayılan başvuru aşağıdaki gibi görünmelidir:

**Hub proxy 'sine doğru şekilde başvuran HTML istemci tarafı kodu**

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"RuntimeBinderException Kullanıcı kodu tarafından işlenmemiş" hatası

Yanlış `Hub.On` aşırı yüklemesi kullanıldığında bu hata ortaya çıkabilir. Yöntemin bir dönüş değeri varsa, dönüş türü genel bir tür parametresi olarak belirtilmelidir:

**İstemci üzerinde tanımlanan Yöntem (oluşturulan proxy olmadan)**

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>Bağlantı KIMLIĞI tutarsız veya sayfa yükleri arasındaki bağlantı sonları

Bu davranış tasarım gereğidir. Hub nesnesi sayfa nesnesinde barındırıldığından, sayfa yenilendiğinde hub yok edilir. Çok sayfalı bir uygulamanın, sayfa yüklemeleri arasında tutarlı olmaları için kullanıcılar ve bağlantı kimlikleri arasındaki ilişkilendirmeyi koruması gerekir. Bağlantı kimlikleri sunucuda `ConcurrentDictionary` nesne veya veritabanında depolanabilir.

### <a name="value-cannot-be-null-error"></a>"Değer null olamaz" hatası

İsteğe bağlı parametrelere sahip sunucu tarafı yöntemleri şu anda desteklenmiyor; isteğe bağlı parametre atlanırsa, yöntemi başarısız olur. Daha fazla bilgi için bkz. [Isteğe bağlı parametreler](https://github.com/SignalR/SignalR/issues/324).

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox hata&gt;&lt;adresi" sunucu ile bağlantı kuramıyor "

WebSocket aktarımının anlaşması başarısız olursa ve bunun yerine başka bir aktarım kullanılıyorsa, bu hata iletisi Firebug 'da görülebilir. Bu davranış tasarım gereğidir.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>"Uzak sertifika, .NET istemci uygulamasındaki doğrulama yordamına göre geçersiz" hatası

Sunucunuz için özel istemci sertifikaları gerekiyorsa, istek yapılmadan önce bağlantı için bir X509Certificate ekleyebilirsiniz. `Connection.AddClientCertificate`kullanarak sertifikayı bağlantıya ekleyin.

### <a name="connection-drops-after-authentication-times-out"></a>Kimlik doğrulama zaman aşımına uğraydıktan sonra bağlantı düşer

Bu davranış tasarım gereğidir. Bağlantı etkin durumdayken kimlik doğrulama bilgileri değiştirilemez; kimlik bilgilerini yenilemek için bağlantı durdurulmalıdır ve yeniden başlatılmalıdır.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>JQuery Mobile kullanılırken OnConnected iki kez çağırılır

jQuery Mobile 'ın `initializePage` işlevi, her sayfadaki betikleri yeniden yürütülmesine zorlar ve bu nedenle ikinci bir bağlantı oluşturur. Bu soruna yönelik çözümler şunlardır:

- JavaScript dosyanızı önce jQuery Mobile başvurusunu ekleyin.
- `$.mobile.autoInitializePage = false`ayarlayarak `initializePage` işlevini devre dışı bırakın.
- Bağlantıyı başlatmadan önce sayfanın başlatılmasını bekleyin.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>İletiler, gönderilen sunucu olayları kullanılarak Silverlight uygulamalarında gecikiyor

Silverlight üzerinde sunucu gönderme olayları kullanılırken iletiler gecikir. Bunun yerine uzun yoklama kullanılmasına zorlamak için, bağlantıyı başlatırken aşağıdakileri kullanın:

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>Süresiz çerçeve protokolü kullanılarak "izin reddedildi"

Bu bilinen bir sorundur ve [burada](https://github.com/SignalR/SignalR/issues/1963)açıklanmıştır. Bu belirti, en son JQuery kitaplığı kullanılarak görülebilir; geçici çözüm, uygulamanızın JQuery 1.8.2 sürümüne indirgenmesini sağlar.

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a>"InvalidOperationException: geçerli bir Web yuva isteği değil.

WebSocket protokolü kullanıldığında bu hata oluşabilir, ancak ağ proxy 'si istek üstbilgilerini değiştiriyor olabilir. Çözüm, proxy 'yi 80 numaralı bağlantı noktasında WebSocket 'ye izin verecek şekilde yapılandırmaktır.

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a>"Özel durum: &lt;Yöntem adı&gt; yöntemi çözümlenemedi" istemci, sunucuda yöntemi çağırdığında

Bu hata, dizi gibi bir JSON yükünde keşfedilmemiş veri türlerinin kullanılmasına neden olabilir. Geçici çözüm, örneğin IList gibi JSON tarafından keşfedilen bir veri türünü kullanmaktır. Daha fazla bilgi için bkz. [.net Client, dizi parametreleriyle hub yöntemlerini çağıramadı](https://github.com/SignalR/SignalR/issues/2672).

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>Derleme ve sunucu tarafı hataları

 Aşağıdaki bölümde, derleyici ve sunucu tarafı çalışma zamanı hatalarına yönelik olası çözümler yer almaktadır.

### <a name="reference-to-hub-instance-is-null"></a>Hub örneğine başvuru null

Her bağlantı için bir hub örneği oluşturulduğundan, kodunuzda bir hub örneği oluşturamazsınız. Hub 'ın dışında bir hub 'daki yöntemleri çağırmak için, hub bağlamına bir başvuru elde etmek üzere bkz. [istemci yöntemlerini çağırma ve hub sınıfı dışından grupları yönetme](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) .

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext. Current. Session null

Bu davranış tasarım gereğidir. SignalR, oturum durumunu etkinleştirmek çift yönlü mesajlaşmayı bozduğundan, ASP.NET oturum durumunu desteklemez.

### <a name="no-suitable-method-to-override"></a>Geçersiz kılınacak uygun yöntem yok

Eski belgelerden veya bloglardan kod kullanıyorsanız bu hatayı görebilirsiniz. Değiştirilmiş veya kullanım dışı olan yöntemlerin adlarına başvurduğunuzdan emin olun (`OnConnectedAsync`gibi).

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>Hostcontexwesions. WebSocketServerUrl null

Bu davranış tasarım gereğidir. Bu üye kullanımdan kaldırılmıştır ve kullanılmamalıdır.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"' SignalR. hub ' adlı bir yol zaten yol koleksiyonunda" hata

Bu hata, uygulamanız tarafından `MapSignalR` iki kez çağrılırsa görülür. Bazı örnek uygulamalar doğrudan başlangıç sınıfında `MapSignalR` çağırır; diğer bir deyişle, çağrı bir sarmalayıcı sınıfında yapılır. Uygulamanızın her ikisini de yapamadığından emin olun.

### <a name="websocket-is-not-used"></a>WebSocket kullanılmıyor

Sunucunuzun ve istemcilerinizin WebSocket gereksinimlerini karşıladığını doğruladıysanız ( [Desteklenen platformlar](../getting-started/supported-platforms.md) belgesinde listelenmiştir), sunucunuzda WebSocket 'i etkinleştirmeniz gerekir. Bu işlemi gerçekleştirmek için yönergeler [burada](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)bulunabilir.

### <a name="connection-is-undefined"></a>$. bağlantı tanımsız

Bu hata, bir sayfadaki betiklerin düzgün şekilde yüklenmediğini veya hub proxy 'sine erişilemediğini veya yanlış erişildiğini gösterir. Sayfanızdaki betik başvurularının projenizde yüklü betiklerine karşılık geldiğini ve sunucu çalışırken bir tarayıcıda/SignalR/hub 'lara erişildiğini doğrulayın.

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a>Dinamik bir ifade derlemek için gereken bir veya daha fazla tür bulunamıyor

Bu hata `Microsoft.CSharp` kitaplığının eksik olduğunu gösterir. Bunları **derlemeler-&gt;Framework** sekmesine ekleyin.

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a>Çağıran duruma, Visual Basic veya kesin olarak belirlenmiş bir hub 'da, Istemci veya tür çağıranlarından erişilemez; "' String ' türünden ' ' String ' türüne dönüştürme geçerli değil" hatası

Visual Basic veya türü kesin belirlenmiş bir hub 'da arayan durumuna erişmek için, `Clients.Caller`yerine `Clients.CallerState` özelliğini (SignalR 2,1 ' de tanıtılan) kullanın.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio sorunları

Bu bölümde, Visual Studio 'da karşılaşılan sorunlar açıklanmaktadır.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>Betik belgeleri düğümü Çözüm Gezgini görünmüyor

Öğreticilerimizden bazıları hata ayıklama sırasında Çözüm Gezgini ' deki "betik belgeleri" düğümüne yönlendirir. Bu düğüm JavaScript hata ayıklayıcısı tarafından üretilir ve yalnızca Internet Explorer 'da tarayıcı istemcilerinde hata ayıklanırken görüntülenir; Chrome veya Firefox kullanılıyorsa düğüm görüntülenmez. JavaScript hata ayıklayıcı, Silverlight hata ayıklayıcısı gibi başka bir istemci hata ayıklayıcısı çalışıyorsa de çalışmaz.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR, Visual Studio 2008 veya önceki sürümlerde çalışmıyor

Bu davranış tasarım gereğidir. SignalR için .NET Framework 4 veya üzeri gerekir; Bu, SignalR uygulamalarının Visual Studio 2010 veya sonraki sürümlerde geliştirilmesi gerekir. SignalR sunucu bileşeni .NET Framework 4,5 gerektirir.

<a id="iis"></a>

## <a name="iis-issues"></a>IIS sorunları

Bu bölüm Internet Information Services sorunları içerir.

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a>SignalR, Visual Studio geliştirme sunucusunda çalışmaktadır, ancak IIS 'de yoktur

SignalR IIS 7,0 ve 7,5 ' de desteklenir, ancak uzantısız URL 'Ler için destek eklenmelidir. Uzantısız URL 'Ler için destek eklemek için bkz. [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)

SignalR 'nin sunucuya ASP.NET yüklenmesi gerekir (ASP.NET IIS 'de varsayılan olarak yüklü değildir). ASP.NET yüklemek için bkz. [ASP.net İndirmeleri](https://www.asp.net/downloads).

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a>Microsoft Azure sorunları

Bu bölüm Microsoft Azure sorunları içerir.

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a>Azure çalışan rolünde SignalR barındırırken FileLoadException

SignalR 'yi bir Azure Worker rolünde barındırmak, "Microsoft. Owin, Version = 2.0.0.0" dosyası veya derlemesi yüklenemedi "özel durumuna neden olabilir. Bu, NuGet ile ilgili bilinen bir sorundur; Bağlama yeniden yönlendirmeleri, Azure çalışan rolü projelerinde otomatik olarak eklenmez. Bunu onarmak için bağlama yeniden yönlendirmelerini el ile ekleyebilirsiniz. Aşağıdaki satırları, çalışan rolü projeniz için `app.config` dosyasına ekleyin.

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>Konu adları değiştirildikten sonra iletiler Azure arkadüzleminden alınmaz

Azure arkadüzlemi tarafından kullanılan konular dahili olarak saklanır; Kullanıcı tarafından yapılandırılabilir olmaları amaçlanmamıştır.
