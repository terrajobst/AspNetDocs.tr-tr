---
uid: signalr/overview/older-versions/introduction-to-security
title: SignalR güvenliğine giriş (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bir SignalR uygulaması geliştirirken göz önünde bulundurmanız gereken güvenlik sorunlarını açıklar.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 715a4059-d307-4631-abbb-c789c95d6eb4
msc.legacyurl: /signalr/overview/older-versions/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 34172c0a2a15a7ab0d782704d5831ce236f5c989
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536731"
---
# <a name="introduction-to-signalr-security-signalr-1x"></a>SignalR Güvenliğine Giriş (SignalR 1.x)

, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, bir SignalR uygulaması geliştirirken göz önünde bulundurmanız gereken güvenlik sorunları açıklanmaktadır.

## <a name="overview"></a>Genel bakış

Bu belgede aşağıdaki bölümler yer alır:

- [SignalR güvenlik kavramları](#concepts)

    - [Kimlik Doğrulaması ve Yetkilendirme](#authentication)
    - [Bağlantı belirteci](#connectiontoken)
    - [Yeniden bağlanıldığında grupları yeniden birleştirme](#rejoingroup)
- [SignalR, siteler arası Istek sahteciliği nasıl engeller](#csrf)
- [SignalR güvenlik önerileri](#recommendations)

    - [Güvenli Yuva katmanları (SSL) protokolü](#ssl)
    - [Grupları bir güvenlik mekanizması olarak kullanmayın](#groupsecurity)
    - [İstemcilerden gelen girişi güvenle işleme](#input)
    - [Etkin bağlantıyla Kullanıcı durumunda değişiklik mutabık kılma](#reconcile)
    - [Otomatik olarak oluşturulan JavaScript proxy dosyaları](#autogen)
    - [Özel durumlar](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR güvenlik kavramları

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>Kimlik doğrulaması ve yetkilendirme

SignalR, bir uygulamanın mevcut kimlik doğrulama yapısıyla tümleştirilecek şekilde tasarlanmıştır. Kullanıcıların kimliğini doğrulamak için herhangi bir özellik sağlamaz. Bunun yerine, uygulamanızda normalde yaptığınız gibi kullanıcıların kimliğini doğrular ve ardından SignalR kodunuzda kimlik doğrulamanın sonuçlarıyla çalışırsınız. Örneğin, ASP.NET Forms kimlik doğrulaması ile kullanıcılarınızın kimliğini doğrulayabilir ve sonra merkezinizdeki bir yöntemi çağırmak için hangi kullanıcıların veya rollerin yetkilendirileceğini zorlayabilirsiniz. Hub 'ınızda, Kullanıcı adı gibi kimlik doğrulama bilgilerini veya bir kullanıcının bir role ait olup olmadığını istemciye geçirebilirsiniz.

SignalR, hangi kullanıcıların bir hub veya metoda erişimi olduğunu belirtmek için [Yetkilendir](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) özniteliği sağlar. Yetkilendir özniteliğini bir hub 'da veya belirli yöntemlere uygularsınız. Yetkilendirme özniteliği olmadan, hub 'daki tüm ortak Yöntemler hub 'a bağlı bir istemci tarafından kullanılabilir. Hub 'lar hakkında daha fazla bilgi için bkz. [SignalR hub 'ları Için kimlik doğrulaması ve yetkilendirme](../security/hub-authorization.md).

`Authorize` özniteliği yalnızca Hub 'larla kullanılır. `PersistentConnection` kullanırken yetkilendirme kurallarını zorlamak için `AuthorizeRequest` metodunu geçersiz kılmanız gerekir. Kalıcı bağlantılar hakkında daha fazla bilgi için bkz. [SignalR kalıcı bağlantıları Için kimlik doğrulaması ve yetkilendirme](../security/persistent-connection-authorization.md).

<a id="connectiontoken"></a>

### <a name="connection-token"></a>Bağlantı belirteci

SignalR, gönderenin kimliğini doğrulayarak kötü amaçlı komutları yürütme riskini azaltır. Kimliği doğrulanmış kullanıcılar için bağlantı kimliği ve Kullanıcı adı içeren bir bağlantı belirteci, istemci ile sunucu arasında her istek için geçirilir. Bağlantı kimliği, yeni bir bağlantı oluşturulduğunda sunucu tarafından rastgele oluşturulan ve bağlantı süresince kalıcı olan benzersiz bir tanımlayıcıdır. Kullanıcı adı, Web uygulaması için kimlik doğrulama mekanizması tarafından sağlanır. Bağlantı belirteci, şifreleme ve dijital imza ile korunur.

![](introduction-to-security/_static/image2.png)

Her istek için sunucu, isteğin belirtilen kullanıcıdan geldiğinden emin olmak için belirtecin içeriğini doğrular. Kullanıcı adı bağlantı kimliğine karşılık gelmelidir. SignalR hem bağlantı kimliğini hem de Kullanıcı adını doğrulayarak kötü niyetli bir kullanıcının başka bir kullanıcıyı kolayca taklit etmesini engeller. Sunucu bağlantı belirtecini doğrulayamazsa istek başarısız olur.

![](introduction-to-security/_static/image4.png)

Bağlantı kimliği doğrulama işleminin bir parçası olduğundan, bir kullanıcının bağlantı kimliğini diğer kullanıcılara açığa çıkarmamalıdır veya bir tanımlama bilgisinde olduğu gibi istemci üzerindeki değeri depolamamalısınız.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>Yeniden bağlanıldığında grupları yeniden birleştirme

Varsayılan olarak, SignalR uygulaması, bağlantı zaman aşımına uğramadan önce bir bağlantının düşürülme ve yeniden oluşturulması gibi geçici bir kesintiden yeniden bağlanıldığında bir kullanıcıyı uygun gruplara otomatik olarak yeniden atar. Yeniden bağlanıldığında, istemci bağlantı kimliği ve atanan grupları içeren bir grup belirteci geçirir. Grup belirteci dijital olarak imzalanır ve şifrelenir. İstemci, bir yeniden bağlantıdan sonra aynı bağlantı kimliğini korur; Bu nedenle, yeniden bağlanan istemciden geçirilen bağlantı kimliğinin, istemci tarafından kullanılan bir önceki bağlantı kimliğiyle eşleşmesi gerekir. Bu doğrulama, kötü niyetli bir kullanıcının yeniden bağlanıldığında yetkisiz gruplara katılması için istekleri geçmesini engeller.

Ancak, Grup belirtecinin süre sonu olmadığı unutulmamalıdır. Bir Kullanıcı geçmişte bir gruba aitdi, ancak bu gruptan yasaklanmış ise, bu kullanıcı yasaklanmış grubu içeren bir grup belirtecini taklit edebilir. Hangi kullanıcıların hangi gruplara ait olduğunu güvenli bir şekilde yönetmeniz gerekiyorsa, bu verileri sunucuda (örneğin,) bir veritabanında depolamanız gerekir. Ardından, uygulamanıza bir kullanıcının bir gruba ait olup olmadığını doğrulayan bir mantığı ekleyin. Grup üyeliğini doğrulama örneği için bkz. [gruplarla çalışma](../guide-to-the-api/working-with-groups.md).

Grupları otomatik olarak yeniden birleştirme işlemi yalnızca geçici bir kesinti sonrasında bağlantı yeniden bağlandığında geçerlidir. Kullanıcının bağlantısı kesilirse veya uygulama yeniden başlatıldıktan sonra, uygulamanız bu kullanıcının doğru gruplara nasıl ekleneceğini ele almalıdır. Daha fazla bilgi için bkz. [gruplarla çalışma](../guide-to-the-api/working-with-groups.md).

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR, siteler arası Istek sahteciliği nasıl engeller

Siteler arası Istek forgery (CSRF), kötü niyetli bir sitenin kullanıcının şu anda oturum açtığı bir güvenlik açığı olan siteye istek gönderdiği bir saldırıya neden olur. SignalR, kötü amaçlı bir sitenin SignalR uygulamanız için geçerli bir istek oluşturması için son derece olası bir durum oluşturarak CSRF 'yi önler.

### <a name="description-of-csrf-attack"></a>CSRF saldırısı açıklaması

CSRF saldırılarına bir örnek aşağıda verilmiştir:

1. Kullanıcı, Forms kimlik doğrulaması kullanarak `www.example.com`oturum açar.
2. Sunucu, kullanıcının kimliğini doğrular. Sunucudan gelen yanıt bir kimlik doğrulama tanımlama bilgisi içerir.
3. Oturum açmadan, Kullanıcı kötü amaçlı bir Web sitesi ziyaret ettiğinde. Bu kötü amaçlı site aşağıdaki HTML biçimini içerir: 

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   Form eyleminin kötü amaçlı siteye değil, güvenlik açığı bulunan siteye gönderdiğine dikkat edin. Bu, CSRF 'nin "siteler arası" parçasıdır.
4. Kullanıcı Gönder düğmesine tıklar. Tarayıcı, istekle kimlik doğrulama tanımlama bilgisini içerir.
5. İstek, example.com sunucusunda kullanıcının kimlik doğrulama içeriğiyle çalışır ve kimliği doğrulanmış bir kullanıcının yapmasına izin verilen her şeyi yapabilir.

Bu örnek, kullanıcının form düğmesine tıklayabilmesine rağmen, kötü amaçlı sayfa yalnızca SignalR uygulamanıza yönelik bir AJAX isteği gönderen bir betiği kolayca çalıştırabilir. Üstelik, SSL kullanmak CSRF saldırılarına engel değildir çünkü kötü amaçlı site "https://" isteği gönderebilir.

Genellikle, tarayıcılar tüm ilgili tanımlama bilgilerini hedef Web sitesine gönderdikleri için kimlik bilgilerini kullanan Web sitelerine karşı CSRF saldırıları mümkündür. Ancak, CSRF saldırıları, tanımlama bilgilerini kötüye ile sınırlı değildir. Örneğin, temel ve Özet kimlik doğrulaması da savunmasız olacaktır. Kullanıcı temel veya Özet kimlik doğrulamasıyla oturum açtıktan sonra, oturum sona erene kadar tarayıcı kimlik bilgilerini otomatik olarak gönderir.

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR tarafından alınan CSRF azaltmaları

SignalR, kötü amaçlı bir sitenin SignalR uygulamanıza geçerli istekler oluşturmasını engellemek için aşağıdaki adımları alır. Bu adımlar varsayılan olarak alınır ve kodunuzda herhangi bir işlem gerektirmez.

- **Etki alanları arası istekleri devre dışı bırak**  
 Varsayılan olarak, kullanıcıların bir SignalR uygulamasında dış etki alanından bir SignalR uç noktası aramasını engellemek için, çapraz etki alanı istekleri bir SignalR uygulamasında devre dışıdır. Dış etki alanından gelen her türlü istek otomatik olarak geçersiz kabul edilir ve engellenir. Bu varsayılan davranışı tutmanız önerilir; Aksi takdirde, kötü amaçlı bir site kullanıcıların sitenize komut göndermesini sağlayabilir. Çapraz etki alanı istekleri kullanmanız gerekiyorsa bkz. [etki alanları arası bağlantı oluşturma](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .
- **Bağlantı belirtecini tanımlama bilgisine değil sorgu dizesinde geçir**  
 SignalR bağlantı belirtecini tanımlama bilgisi olarak değil sorgu dizesi değeri olarak geçirir. Bağlantı belirtecini bir tanımlama bilgisi olarak depolamadığınızda, kötü amaçlı kod ile karşılaşıldığında bağlantı belirteci yanlışlıkla tarayıcı tarafından iletilmez. Ayrıca, bağlantı belirteci geçerli bağlantının ötesinde kalıcı değildir. Bu nedenle, kötü niyetli bir Kullanıcı başka bir kullanıcının kimlik doğrulama kimlik bilgileri altında istek yapamaz.
- **Bağlantı belirtecini doğrula**  
 [Bağlantı belirteci](#connectiontoken) bölümünde açıklandığı gibi, sunucu, kimliği doğrulanmış her kullanıcıyla ilişkili bağlantı kimliğini bilir. Sunucu, Kullanıcı adıyla eşleşmeyen bir bağlantı kimliğinden gelen isteği işlemez. Kötü amaçlı Kullanıcı Kullanıcı adını ve geçerli rastgele oluşturulan bağlantı kimliğini bilmemiz gerektiğinden, kötü niyetli bir kullanıcının geçerli bir isteği tahmin etmesi olası değildir. Bağlantı sona erdikten hemen sonra bu bağlantı kimliği geçersiz hale gelir. Anonim kullanıcıların herhangi bir hassas bilgilere erişimi olmamalıdır.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR güvenlik önerileri

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>Güvenli Yuva katmanları (SSL) protokolü

SSL protokolü, istemci ve sunucu arasında veri aktarımını güvenli hale getirmek için şifrelemeyi kullanır. SignalR uygulamanız, istemci ve sunucu arasında hassas bilgiler gönderiyorsa, aktarım için SSL kullanın. SSL ayarlama hakkında daha fazla bilgi için bkz. [IIS 7 ' de SSL ayarlama](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>Grupları bir güvenlik mekanizması olarak kullanmayın

Gruplar ilgili kullanıcıları toplamanın kolay bir yoludur, ancak gizli bilgilere erişimin sınırlandırılmasının güvenli bir mekanizması değildir. Bu özellikle, kullanıcılar yeniden bağlanma sırasında gruplara otomatik olarak katılabileceği durumlarda geçerlidir. Bunun yerine, ayrıcalıklı kullanıcıları bir role eklemeyi ve bir hub yöntemine erişimi yalnızca o rolün üyelerine sınırlamayı göz önünde bulundurun. Bir role göre erişimi kısıtlama örneği için bkz. [SignalR hub 'ları Için kimlik doğrulaması ve yetkilendirme](../security/hub-authorization.md). Yeniden bağlanıldığında, gruplara kullanıcı erişimini denetleme örneği için bkz. [gruplarla çalışma](../guide-to-the-api/working-with-groups.md).

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>İstemcilerden gelen girişi güvenle işleme

Diğer istemcilere yayın için tasarlanan istemcilerden gelen tüm girişler, kötü niyetli bir kullanıcının diğer kullanıcılara betik gönderemediğinden emin olmak için kodlanmalıdır. SignalR uygulamanızda birçok farklı türde istemci olabileceğinden, iletileri sunucu yerine alıcı istemcilere kodlamak en iyisidir. Bu nedenle, HTML kodlaması bir Web istemcisi için geçerlidir, ancak diğer istemci türlerine yönelik değildir. Örneğin, bir sohbet iletisini görüntüleyen Web istemcisi yöntemi, `html()` işlevini çağırarak kullanıcı adını ve iletisini güvenle işleyebilir.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>Etkin bağlantıyla Kullanıcı durumunda değişiklik mutabık kılma

Etkin bağlantı varken kullanıcının kimlik doğrulama durumu değişirse, "Kullanıcı kimliği etkin bir SignalR bağlantısı sırasında değiştiremeyecektir." şeklinde bir hata alır. Bu durumda, bağlantı kimliği ve Kullanıcı adının koordine olduğundan emin olmak için uygulamanızın sunucuya yeniden bağlanması gerekir. Örneğin, uygulamanız etkin bir bağlantı varken kullanıcının oturumu açmasına izin veriyorsa, bağlantı için Kullanıcı adı artık sonraki istek için geçirilen adla eşleşmez. Kullanıcı oturumu kapatmadan önce bağlantıyı durdurup yeniden başlatmanız gerekir.

Ancak, çoğu uygulamanın bağlantıyı el ile durdurmanız ve yeniden başlatmanız gerektiğini unutmayın. Uygulamanız, bir Web Forms uygulaması veya MVC uygulamasındaki varsayılan davranış gibi, Kullanıcı oturum kapatıldıktan sonra ayrı bir sayfaya yeniden yönlendirirse veya oturum kapatıldıktan sonra geçerli sayfayı yenileirse, etkin bağlantının bağlantısı otomatik olarak kesilir ve ek eylem gerektirir.

Aşağıdaki örnek, Kullanıcı durumu değiştiğinde bir bağlantının nasıl durdurulacağını ve başlatılacağını gösterir.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

Ya da sitenizin form kimlik doğrulaması ile kayan süre sonu kullanıyorsa ve kimlik doğrulama tanımlama bilgisinin geçerli tutulması için bir etkinlik yoksa kullanıcının kimlik doğrulaması durumu değişebilir. Bu durumda, Kullanıcı oturumu kapatılır ve Kullanıcı adı bağlantı belirtecindeki Kullanıcı adıyla eşleşmez. Kimlik doğrulama tanımlama bilgisinin geçerli tutulması için, Web sunucusunda düzenli aralıklarla bir kaynak isteyen bir betik ekleyerek bu sorunu çözebilirsiniz. Aşağıdaki örnek, her 30 dakikada bir kaynağın nasıl isteneceğini gösterir.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>Otomatik olarak oluşturulan JavaScript proxy dosyaları

Her bir kullanıcı için JavaScript ara sunucu dosyasına tüm Hub 'ları ve yöntemleri dahil etmek istemiyorsanız, dosyanın otomatik olarak oluşturulmasını devre dışı bırakabilirsiniz. Birden çok hub ve yöntemlere sahipseniz ancak her kullanıcının tüm yöntemlerin farkında olmasını istemiyorsanız bu seçeneği belirleyebilirsiniz. **Enablejavascriptproxy 'leri** **false**olarak ayarlayarak otomatik oluşturmayı devre dışı bırakabilirsiniz.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

JavaScript proxy dosyaları hakkında daha fazla bilgi için bkz. [oluşturulan ara sunucu ve sizin için ne yapar](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy). <a id="exceptions"></a>

### <a name="exceptions"></a>Özel Durumlar

Nesneler, istemcilere hassas bilgiler sergilebileceğinden, istemcilere özel durum nesneleri geçirmekten kaçınmalısınız. Bunun yerine, ilgili hata iletisini görüntüleyen istemcisinde bir yöntemi çağırın.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
