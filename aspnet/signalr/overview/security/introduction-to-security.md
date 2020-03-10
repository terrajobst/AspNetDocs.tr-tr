---
uid: signalr/overview/security/introduction-to-security
title: SignalR güvenliğine giriş | Microsoft Docs
author: bradygaster
description: Bir SignalR uygulaması geliştirirken göz önünde bulundurmanız gereken güvenlik sorunlarını açıklar.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558578"
---
# <a name="introduction-to-signalr-security"></a>SignalR Güvenliğine Giriş

, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, bir SignalR uygulaması geliştirirken göz önünde bulundurmanız gereken güvenlik sorunları açıklanmaktadır.
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

SignalR, kullanıcıların kimliğini doğrulamak için herhangi bir özellik sağlamıyor. Bunun yerine, SignalR özelliklerini bir uygulama için mevcut kimlik doğrulama yapısıyla tümleştirin. Kullanıcılarınızın normalde uygulamanızda olduğu gibi kimlik doğrulaması yapabilir ve SignalR kodunuzda kimlik doğrulamanın sonuçlarıyla çalışırsınız. Örneğin, ASP.NET Forms kimlik doğrulaması ile kullanıcılarınızın kimliğini doğrulayabilir ve sonra merkezinizdeki bir yöntemi çağırmak için hangi kullanıcıların veya rollerin yetkilendirileceğini zorlayabilirsiniz. Hub 'ınızda, Kullanıcı adı gibi kimlik doğrulama bilgilerini veya bir kullanıcının bir role ait olup olmadığını istemciye geçirebilirsiniz.

SignalR, hangi kullanıcıların bir hub veya metoda erişimi olduğunu belirtmek için [Yetkilendir](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) özniteliği sağlar. Yetkilendir özniteliğini bir hub 'da veya belirli yöntemlere uygularsınız. Yetkilendirme özniteliği olmadan, hub 'daki tüm ortak Yöntemler hub 'a bağlı bir istemci tarafından kullanılabilir. Hub 'lar hakkında daha fazla bilgi için bkz. [SignalR hub 'ları Için kimlik doğrulaması ve yetkilendirme](hub-authorization.md).

`Authorize` özniteliğini hub 'lara uygularsınız, ancak kalıcı bağlantılara uygulanmaz. `PersistentConnection` kullanırken yetkilendirme kurallarını zorlamak için `AuthorizeRequest` metodunu geçersiz kılmanız gerekir. Kalıcı bağlantılar hakkında daha fazla bilgi için bkz. [SignalR kalıcı bağlantıları Için kimlik doğrulaması ve yetkilendirme](persistent-connection-authorization.md).

<a id="connectiontoken"></a>

### <a name="connection-token"></a>Bağlantı belirteci

SignalR, gönderenin kimliğini doğrulayarak kötü amaçlı komutları yürütme riskini azaltır. Her istek için, istemci ve sunucu kimliği doğrulanmış kullanıcılar için bağlantı kimliği ve Kullanıcı adı içeren bir bağlantı belirteci iletir. Bağlantı kimliği, her bağlı istemciyi benzersiz şekilde tanımlar. Sunucu yeni bir bağlantı oluşturulduğunda bağlantı kimliğini rastgele oluşturur ve bağlantı süresince o kimliği sürdürür. Web uygulaması için kimlik doğrulama mekanizması Kullanıcı adını sağlar. SignalR, bağlantı belirtecini korumak için şifreleme ve dijital imza kullanır.

![](introduction-to-security/_static/image2.png)

Her istek için sunucu, isteğin belirtilen kullanıcıdan geldiğinden emin olmak için belirtecin içeriğini doğrular. Kullanıcı adı bağlantı kimliğine karşılık gelmelidir. SignalR hem bağlantı kimliğini hem de Kullanıcı adını doğrulayarak kötü niyetli bir kullanıcının başka bir kullanıcıyı kolayca taklit etmesini engeller. Sunucu bağlantı belirtecini doğrulayamazsa istek başarısız olur.

![](introduction-to-security/_static/image4.png)

Bağlantı kimliği doğrulama işleminin bir parçası olduğundan, bir kullanıcının bağlantı kimliğini diğer kullanıcılara açığa çıkarmamalıdır veya bir tanımlama bilgisinde olduğu gibi istemci üzerindeki değeri depolamamalısınız.

#### <a name="connection-tokens-vs-other-token-types"></a>Bağlantı belirteçleri ve diğer belirteç türleri

Bağlantı belirteçleri, oturum belirteçleri veya kimlik doğrulama belirteçleri gibi göründüğünden, bazen güvenlik araçları tarafından işaretlenir çünkü bu, sunulduklarında risk doğurur.

SignalR 'nin bağlantı belirteci bir kimlik doğrulama belirteci değil. Bu isteği yapan kullanıcının bağlantıyı oluşturan kullanıcının aynı olduğunu doğrulamak için kullanılır. ASP.NET SignalR bağlantıların sunucular arasında taşınmasına izin verdiğinden bağlantı belirteci gereklidir. Belirteç, bağlantıyı belirli bir kullanıcıyla ilişkilendirir, ancak isteği yapan kullanıcının kimliğini vermez. Bir SignalR isteğinin düzgün şekilde doğrulanabilmesi için, tanımlama bilgisi veya taşıyıcı belirteci gibi kullanıcı kimliğini belirten başka bir belirteci olmalıdır. Ancak, bağlantı belirtecinin kendisi isteğin bu kullanıcı tarafından yapıldığı bir talep yapmaz, yalnızca belirteçte olan bağlantı KIMLIĞI o kullanıcıyla ilişkilendirilir.

Bağlantı belirteci kendi kendine kimlik doğrulama talebi sağladığından, "oturum" veya "kimlik doğrulama" belirteci olarak kabul edilmez. İsteğin kullanıcı kimliği ve belirteçte olan kimlik eşleşmediğinden, belirli bir kullanıcının bağlantı belirtecini farklı bir kullanıcı olarak (veya kimliği doğrulanmamış bir istek) kimliği doğrulanmış bir istekte ele almak başarısız olur.

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

1. Kullanıcı, Forms kimlik doğrulaması kullanarak www.example.com 'de oturum açar.
2. Sunucu, kullanıcının kimliğini doğrular. Sunucudan gelen yanıt bir kimlik doğrulama tanımlama bilgisi içerir.
3. Oturum açmadan, Kullanıcı kötü amaçlı bir Web sitesi ziyaret ettiğinde. Bu kötü amaçlı site aşağıdaki HTML biçimini içerir:

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   Form eyleminin kötü amaçlı siteye değil, güvenlik açığı bulunan siteye gönderdiğine dikkat edin. Bu, CSRF 'nin "siteler arası" parçasıdır.
4. Kullanıcı Gönder düğmesine tıklar. Tarayıcı, istekle kimlik doğrulama tanımlama bilgisini içerir.
5. İstek, example.com sunucusunda kullanıcının kimlik doğrulama içeriğiyle çalışır ve kimliği doğrulanmış bir kullanıcının yapmasına izin verilen her şeyi yapabilir.

Bu örnek, kullanıcının form düğmesine tıklayabilmesine rağmen, kötü amaçlı sayfa yalnızca SignalR uygulamanıza yönelik bir AJAX isteği gönderen bir betiği kolayca çalıştırabilir. Üstelik, SSL kullanmak CSRF saldırılarına engel değildir çünkü kötü amaçlı site "https://" isteği gönderebilir.

Genellikle, tarayıcılar tüm ilgili tanımlama bilgilerini hedef Web sitesine gönderdikleri için kimlik bilgilerini kullanan Web sitelerine karşı CSRF saldırıları mümkündür. Ancak, CSRF saldırıları, tanımlama bilgilerini kötüye ile sınırlı değildir. Örneğin, temel ve Özet kimlik doğrulaması da savunmasız olacaktır. Kullanıcı temel veya Özet kimlik doğrulamasıyla oturum açtıktan sonra, oturum sona erene kadar tarayıcı kimlik bilgilerini otomatik olarak gönderir.

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR tarafından alınan CSRF azaltmaları

SignalR, kötü amaçlı bir sitenin uygulamanıza yönelik geçerli istekler oluşturmasını engellemek için aşağıdaki adımları alır. SignalR bu adımları varsayılan olarak alır, kodunuzda herhangi bir işlem yapmanız gerekmez.

- **Etki alanları arası Istekleri devre dışı bırak** SignalR, kullanıcıların bir dış etki alanından bir SignalR uç noktası aramasını engellemek için etki alanları arası istekleri devre dışı bırakır. SignalR bir dış etki alanındaki tüm istekleri geçersiz olarak değerlendirir ve isteği engeller. Bu varsayılan davranışı tutmanızı öneririz; Aksi takdirde, kötü amaçlı bir site kullanıcıların sitenize komut göndermesini sağlayabilir. Çapraz etki alanı istekleri kullanmanız gerekiyorsa bkz. [etki alanları arası bağlantı oluşturma](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .
- **Bağlantı belirtecini tanımlama bilgisine değil sorgu dizesinde geçir** SignalR bağlantı belirtecini tanımlama bilgisi olarak değil sorgu dizesi değeri olarak geçirir. Tarayıcı, kötü amaçlı kod ile karşılaşıldığında bağlantı belirtecini yanlışlıkla iletebileceğinden bağlantı belirtecini bir tanımlama bilgisinde depolamak güvenli değildir. Ayrıca, bağlantı belirtecinin sorgu dizesinde geçirilmesi, bağlantı belirtecinin geçerli bağlantının ötesinde kalıcı olmasını önler. Bu nedenle, kötü niyetli bir Kullanıcı başka bir kullanıcının kimlik doğrulama kimlik bilgileri altında istek yapamaz.
- **Bağlantı belirtecini doğrula** [Bağlantı belirteci](#connectiontoken) bölümünde açıklandığı gibi, sunucu, kimliği doğrulanmış her kullanıcıyla ilişkili bağlantı kimliğini bilir. Sunucu, Kullanıcı adıyla eşleşmeyen bir bağlantı kimliğinden gelen isteği işlemez. Kötü amaçlı Kullanıcı Kullanıcı adını ve geçerli rastgele oluşturulan bağlantı kimliğini bilmemiz gerektiğinden, kötü niyetli bir kullanıcının geçerli bir isteği tahmin etmesi olası değildir. Bağlantı sona erdikten hemen sonra bu bağlantı kimliği geçersiz hale gelir. Anonim kullanıcıların herhangi bir hassas bilgilere erişimi olmamalıdır.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR güvenlik önerileri

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>Güvenli Yuva katmanları (SSL) protokolü

SSL protokolü, istemci ve sunucu arasında veri aktarımını güvenli hale getirmek için şifrelemeyi kullanır. SignalR uygulamanız, istemci ve sunucu arasında hassas bilgiler gönderiyorsa, aktarım için SSL kullanın. SSL ayarlama hakkında daha fazla bilgi için bkz. [IIS 7 ' de SSL ayarlama](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>Grupları bir güvenlik mekanizması olarak kullanmayın

Gruplar ilgili kullanıcıları toplamanın kolay bir yoludur, ancak gizli bilgilere erişimin sınırlandırılmasının güvenli bir mekanizması değildir. Bu özellikle, kullanıcılar yeniden bağlanma sırasında gruplara otomatik olarak katılabileceği durumlarda geçerlidir. Bunun yerine, ayrıcalıklı kullanıcıları bir role eklemeyi ve bir hub yöntemine erişimi yalnızca o rolün üyelerine sınırlamayı göz önünde bulundurun. Bir role göre erişimi kısıtlama örneği için bkz. [SignalR hub 'ları Için kimlik doğrulaması ve yetkilendirme](hub-authorization.md). Yeniden bağlanıldığında, gruplara kullanıcı erişimini denetleme örneği için bkz. [gruplarla çalışma](../guide-to-the-api/working-with-groups.md).

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>İstemcilerden gelen girişi güvenle işleme

Kötü amaçlı bir kullanıcının diğer kullanıcılara betik gönderemediğinden emin olmak için, diğer istemcilere yayın için tasarlanan istemcilerden gelen tüm girişleri kodlamanız gerekir. SignalR uygulamanızda birçok farklı türde istemci olabileceğinden, iletileri sunucu yerine alıcı istemcilerde kodlamanız gerekir. Bu nedenle, HTML kodlaması bir Web istemcisi için geçerlidir, ancak diğer istemci türlerine yönelik değildir. Örneğin, bir sohbet iletisini görüntüleyen Web istemcisi yöntemi, `html()` işlevini çağırarak kullanıcı adını ve iletisini güvenle işleyebilir.

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
