---
uid: signalr/overview/older-versions/hub-authorization
title: SignalR hub 'Ları için kimlik doğrulaması ve yetkilendirme (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bu konuda, hangi kullanıcıların veya rollerin hub yöntemlerine erişebileceğini nasıl kısıtlayabileceği açıklanmaktadır.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558536"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a>SignalR Hub’ları için Kimlik Doğrulaması ve Yetkilendirme (SignalR 1.x)

, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konuda, hangi kullanıcıların veya rollerin hub yöntemlerine erişebileceğini nasıl kısıtlayabileceği açıklanmaktadır.

## <a name="overview"></a>Genel bakış

Bu konu aşağıdaki bölümleri içermektedir:

- [Yetkilendir özniteliği](#authorizeattribute)
- [Tüm Hub 'lar için kimlik doğrulaması gerektir](#requireauth)
- [Özelleştirilmiş yetkilendirme](#custom)
- [Kimlik doğrulama bilgilerini istemcilere geçir](#passauth)
- [.NET istemcileri için kimlik doğrulama seçenekleri](#authoptions)

    - [Forms kimlik doğrulaması ile tanımlama bilgisi](#cookie)
    - [Windows Kimlik Doğrulaması](#windows)
    - [Bağlantı üst bilgisi](#header)
    - [Sertifika](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>Yetkilendir özniteliği

SignalR, bir hub veya yönteme hangi kullanıcıların veya rollerin erişebileceğini belirtmek için [Yetkilendir](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) özniteliği sağlar. Bu öznitelik `Microsoft.AspNet.SignalR` ad alanında bulunur. `Authorize` özniteliğini bir hub 'daki bir hub 'a ya da belirli yöntemlere uygularsınız. `Authorize` özniteliğini bir hub sınıfına uyguladığınızda, belirtilen yetkilendirme gereksinimi, hub 'daki tüm yöntemlere uygulanır. Uygulayabileceğiniz farklı yetkilendirme gereksinimleri türleri aşağıda gösterilmiştir. `Authorize` özniteliği olmadan, hub 'daki tüm ortak Yöntemler hub 'a bağlı bir istemci tarafından kullanılabilir.

Web uygulamanızda "admin" adlı bir rol tanımladıysanız, yalnızca bu roldeki kullanıcıların aşağıdaki kodla bir hub 'a erişebileceğini belirtebilirsiniz.

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

Ya da bir hub 'ın tüm kullanıcılar için kullanılabilir bir yöntem içerdiğini ve yalnızca kimliği doğrulanmış kullanıcılar tarafından kullanılabilen ikinci bir yöntemi aşağıda gösterildiği gibi belirtebilirsiniz.

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

Aşağıdaki örneklerde farklı yetkilendirme senaryoları ele verilmiştir:

- `[Authorize]` – yalnızca kimliği doğrulanmış kullanıcılar
- `[Authorize(Roles = "Admin,Manager")]` – yalnızca belirtilen rollerdeki kimliği doğrulanmış kullanıcılar
- `[Authorize(Users = "user1,user2")]` – yalnızca belirtilen kullanıcı adlarına sahip kimliği doğrulanmış kullanıcılar
- `[Authorize(RequireOutgoing=false)]` – yalnızca kimliği doğrulanmış kullanıcılar hub 'ı çağırabilir, ancak sunucudan istemcilere geri çağrılar bir ileti gönderebildiği ancak diğerlerinin iletiyi alabileceği gibi yetkilendirme ile sınırlı değildir. Requiregiden özelliği, hub içindeki bireyler yöntemlerine değil, yalnızca tüm Hub 'a uygulanabilir. Requiregiden değeri false olarak ayarlandığında, yalnızca yetkilendirme gereksinimini karşılayan kullanıcılar sunucudan çağırılır.

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>Tüm Hub 'lar için kimlik doğrulaması gerektir

Uygulama başladığında [requiauthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) metodunu çağırarak uygulamanızdaki tüm Hub 'lar ve hub yöntemleri için kimlik doğrulaması yapmanız gerekebilir. Birden çok hub olduğunda ve bunların tümü için bir kimlik doğrulama gereksinimini zorlamak istediğinizde bu yöntemi kullanabilirsiniz. Bu yöntemle rol, Kullanıcı veya giden yetkilendirme belirtemezsiniz. Yalnızca hub yöntemlerine erişimin kimliği doğrulanmış kullanıcılarla kısıtlanmasını belirtebilirsiniz. Bununla birlikte, ek gereksinimler belirtmek için yine de, yetkilendirme özniteliğini hub 'lara veya yöntemlere uygulayabilirsiniz. Özniteliklerde belirttiğiniz herhangi bir gereksinim, temel kimlik doğrulaması gereksinimine ek olarak uygulanır.

Aşağıdaki örnek, tüm Hub yöntemlerini kimliği doğrulanmış kullanıcılarla kısıtlayan bir Global. asax dosyası gösterir.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

Bir SignalR isteği işlendikten sonra `RequireAuthentication()` yöntemini çağırırsanız, SignalR bir `InvalidOperationException` özel durumu oluşturur. Bu özel durum, işlem hattı çağrıldıktan sonra HubPipeline 'e modül ekleyemediği için oluşturulur. Önceki örnekte, ilk isteğin işlenmesinden önce bir kez yürütülen `Application_Start` yönteminde `RequireAuthentication` yönteminin çağrılması gösterilmektedir.

<a id="custom"></a>

## <a name="customized-authorization"></a>Özelleştirilmiş yetkilendirme

Yetkilendirmenin nasıl belirlendiğini özelleştirmeniz gerekiyorsa, `AuthorizeAttribute` türeten bir sınıf oluşturabilir ve [userauthorization](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) metodunu geçersiz kılabilirsiniz. Bu yöntem, kullanıcının isteği tamamlamaya yetkili olup olmadığını belirlemede her istek için çağrılır. Geçersiz kılınan yöntemde, yetkilendirme senaryonuz için gerekli mantığı sağlarsınız. Aşağıdaki örnek, talep tabanlı kimlik aracılığıyla yetkilendirmeyi nasıl zorlayacağı gösterilmektedir.

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>Kimlik doğrulama bilgilerini istemcilere geçir

İstemci üzerinde çalışan koddaki kimlik doğrulama bilgilerini kullanmanız gerekebilir. İstemci üzerindeki yöntemleri çağırırken gerekli bilgileri geçirirsiniz. Örneğin, bir sohbet uygulaması yöntemi, aşağıda gösterildiği gibi bir ileti gönderen kişinin kullanıcı adına bir parametre olarak geçirebilir.

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

Ya da, aşağıda gösterildiği gibi, kimlik doğrulama bilgilerini temsil eden bir nesne oluşturabilir ve bu nesneyi bir parametre olarak geçirebilirsiniz.

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

Kötü niyetli bir Kullanıcı bu istemciden gelen bir isteği taklit etmek için onu kullanabilmesi için, bir istemcinin bağlantı kimliğini asla diğer istemcilere iletmemelisiniz.

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>.NET istemcileri için kimlik doğrulama seçenekleri

Bir konsol uygulaması gibi, kimliği doğrulanmış kullanıcılarla sınırlı bir hub ile etkileşime geçen bir .NET istemciniz varsa, kimlik doğrulama bilgilerini bir tanımlama bilgisine, bağlantı başlığına veya bir sertifikaya geçirebilirsiniz. Bu bölümdeki örneklerde, kullanıcının kimliğini doğrulamak için bu farklı yöntemlerin nasıl kullanılacağı gösterilmektedir. Bunlar tam işlevli SignalR uygulamaları değildir. SignalR ile .NET istemcileri hakkında daha fazla bilgi için bkz. [hub API Kılavuzu-.NET istemcisi](../guide-to-the-api/hubs-api-guide-net-client.md).

<a id="cookie"></a>

### <a name="cookie"></a>Tanımlama Bilgisi

.NET istemciniz ASP.NET Forms kimlik doğrulaması kullanan bir hub ile etkileşime geçtiğinde, bağlantıda kimlik doğrulama tanımlama bilgisini el ile ayarlamanız gerekir. Tanımlama bilgisini, [Hubconnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) nesnesindeki `CookieContainer` özelliğine eklersiniz. Aşağıdaki örnek, bir Web sayfasından kimlik doğrulama tanımlama bilgisi alan ve bu tanımlama bilgisini bağlantıya ekleyen bir konsol uygulamasını gösterir. Örnekteki URL `https://www.contoso.com/RemoteLogin`, oluşturmanız gereken bir Web sayfasına işaret eder. Sayfa, postalanan Kullanıcı adı ve parolasını alır ve kimlik bilgileriyle kullanıcıya oturum açmaya çalışır.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

Konsol uygulaması, aşağıdaki arka plan kod dosyasını içeren boş bir sayfaya başvuruda bulunmak için kimlik bilgilerini www.contoso.com/RemoteLogin adresine gönderir.

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Windows kimlik doğrulaması

Windows kimlik doğrulamasını kullanırken, [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) özelliğini kullanarak geçerli kullanıcının kimlik bilgilerini geçirebilirsiniz. DefaultCredentials değeri için bağlantı kimlik bilgilerini ayarlarsınız.

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>Bağlantı üst bilgisi

Uygulamanız tanımlama bilgilerini kullanmıyor ise, Kullanıcı bilgilerini bağlantı üst bilgisinde geçirebilirsiniz. Örneğin, bağlantı üst bilgisinde bir belirteç geçirebilirsiniz.

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

Ardından, hub 'da kullanıcının belirtecini doğrularsınız.

<a id="certificate"></a>

### <a name="certificate"></a>Sertifika

Kullanıcıyı doğrulamak için bir istemci sertifikası geçirebilirsiniz. Bağlantıyı oluştururken sertifikayı eklersiniz. Aşağıdaki örnek, bağlantıya yalnızca bir istemci sertifikasının nasıl ekleneceğini gösterir. tam konsol uygulamasını göstermez. Sertifikayı oluşturmak için çeşitli farklı yollar sağlayan [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) sınıfını kullanır.

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
