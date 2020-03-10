---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR sorunlarını giderme (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bu makalede, SignalR uygulamaları geliştirmeyle ilgili yaygın sorunlar açıklanmaktadır.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579606"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR Sorunlarını Giderme (SignalR 1.x)

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belgede, SignalR ile ilgili genel sorun giderme sorunları açıklanmaktadır.

Bu belge aşağıdaki bölümleri içerir.

- [İstemci ve sunucu arasındaki Yöntemler sessizce başarısız oluyor](#connection)
- [Diğer bağlantı sorunları](#other)
- [Derleme ve sunucu tarafı hataları](#server)
- [Visual Studio sorunları](#vs)
- [Internet Information Services sorunları](#iis)
- [Azure sorunları](#azure)

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

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

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

### <a name="connection-limit-reached"></a>Bağlantı sınırına ulaşıldı

Windows 7 gibi bir istemci işletim sisteminde IIS 'nin tam sürümünü kullanırken, 10 bağlantı sınırı uygulanır. İstemci işletim sistemi kullanırken, bu sınırı önlemek için IIS Express kullanın.

### <a name="cross-domain-connection-not-set-up-properly"></a>Etki alanları arası bağlantı düzgün ayarlanmadı

Bir etki alanı bağlantısı (SignalR URL 'SI barındırma sayfasıyla aynı etki alanında olmayan bir bağlantı) doğru ayarlanmamışsa, bağlantı hata iletisi olmadan başarısız olabilir. Etki alanları arası iletişimin nasıl etkinleştirileceği hakkında bilgi için bkz. [etki alanları arası bağlantı oluşturma](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>NTLM (Active Directory) kullanılarak bağlantı .NET istemcisinde çalışmıyor

Bağlantı düzgün yapılandırılmamışsa, bir .NET istemci uygulamasındaki bağlantı etki alanı güvenliği kullanan bir bağlantı başarısız olabilir. Bir etki alanı ortamında SignalR kullanmak için, önkoşul bağlantısı özelliğini aşağıdaki gibi ayarlayın:

**C#bağlantı kimlik bilgilerini uygulayan istemci kodu**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

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
- **Hub yolunu eklemeden önce uygulamaya rotalar ekleniyor:** Uygulamanız başka rotalar kullanıyorsa, eklenen ilk yolun `MapHubs`çağrısı olduğunu doğrulayın.

### <a name="500-internal-server-error"></a>"500 iç sunucu hatası"

Bu, çok çeşitli nedenleri olabilecek çok sayıda genel hatadır. Hatanın ayrıntıları sunucunun olay günlüğünde görünmelidir veya sunucu hata ayıklaması aracılığıyla bulunabilir. Daha ayrıntılı hata bilgileri, sunucuda ayrıntılı hataları etkinleştirerek elde edilebilir. Daha fazla bilgi için bkz. [hub sınıfında hataları işleme](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError: &lt;hubType&gt; tanımsız" hatası

`MapHubs` çağrısı düzgün şekilde yapılmazlarsa bu hata oluşur. Daha fazla bilgi için bkz. [SignalR rotasını kaydetme ve SignalR seçeneklerini yapılandırma](../guide-to-the-api/hubs-api-guide-server.md#route) .

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

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"RuntimeBinderException Kullanıcı kodu tarafından işlenmemiş" hatası

Yanlış `Hub.On` aşırı yüklemesi kullanıldığında bu hata ortaya çıkabilir. Yöntemin bir dönüş değeri varsa, dönüş türü genel bir tür parametresi olarak belirtilmelidir:

**İstemci üzerinde tanımlanan Yöntem (oluşturulan proxy olmadan)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

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

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>Süresiz çerçeve protokolü kullanılarak "izin reddedildi"

Bu bilinen bir sorundur ve [burada](https://github.com/SignalR/SignalR/issues/1963)açıklanmıştır. Bu belirti, en son JQuery kitaplığı kullanılarak görülebilir; geçici çözüm, uygulamanızın JQuery 1.8.2 sürümüne indirgenmesini sağlar.

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

Bu hata, uygulamanız tarafından `MapHubs` iki kez çağrılırsa görülür. Bazı örnek uygulamalar doğrudan genel uygulama dosyasında `MapHubs` çağırır; diğer bir deyişle, çağrı bir sarmalayıcı sınıfında yapılır. Uygulamanızın her ikisini de yapamadığından emin olun.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio sorunları

Bu bölümde, Visual Studio 'da karşılaşılan sorunlar açıklanmaktadır.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>Betik belgeleri düğümü Çözüm Gezgini görünmüyor

Öğreticilerimizden bazıları hata ayıklama sırasında Çözüm Gezgini ' deki "betik belgeleri" düğümüne yönlendirir. Bu düğüm JavaScript hata ayıklayıcısı tarafından üretilir ve yalnızca Internet Explorer 'da tarayıcı istemcilerinde hata ayıklanırken görüntülenir; Chrome veya Firefox kullanılıyorsa düğüm görüntülenmez. JavaScript hata ayıklayıcı, Silverlight hata ayıklayıcısı gibi başka bir istemci hata ayıklayıcısı çalışıyorsa de çalışmaz.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR, Visual Studio 2008 veya önceki sürümlerde çalışmıyor

Bu davranış tasarım gereğidir. SignalR için .NET Framework 4 veya üzeri gerekir; Bu, SignalR uygulamalarının Visual Studio 2010 veya sonraki sürümlerde geliştirilmesi gerekir.

<a id="iis"></a>

## <a name="iis-issues"></a>IIS sorunları

Bu bölüm Internet Information Services sorunları içerir.

### <a name="web-site-crashes-after-maphubs-call"></a>MapHubs çağrısından sonra Web sitesi kilitleniyor

Bu sorun, SignalR 'nin en son sürümünde düzeltildi. Yüklemenizi NuGet kullanarak güncelleştirerek, SignalR 'nin en son yayınlanan sürümünü kullandığınızı doğrulayın.

<a id="azure"></a>

## <a name="azure-issues"></a>Azure sorunları

Bu bölüm Microsoft Azure sorunları içerir.

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>Konu adları değiştirildikten sonra iletiler Azure arkadüzleminden alınmaz

Azure arkadüzlemi tarafından kullanılan konuların Kullanıcı tarafından yapılandırılabilir olması amaçlanmamıştır.
