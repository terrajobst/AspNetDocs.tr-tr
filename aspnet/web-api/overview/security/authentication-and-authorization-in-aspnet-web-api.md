---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API 'sinde kimlik doğrulaması ve yetkilendirme | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'sinde kimlik doğrulamaya ve yetkilendirmeye genel bir bakış sunar.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598646"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>ASP.NET Web API'de Kimlik Doğrulama ve Yetkilendirme

, [Mike te son](https://github.com/MikeWasson)

Bir Web API 'SI oluşturdunuz, ancak şimdi ona erişimi denetlemek istiyorsunuz. Bu makale dizisinde, yetkisiz kullanıcılardan bir Web API 'sinin güvenliğini sağlamaya yönelik bazı seçeneklere bakacağız. Bu seri, hem kimlik doğrulamasını hem de yetkilendirmeyi kapsar.

- *Kimlik doğrulaması* , kullanıcının kimliğini öğrenmektir. Örneğin, Gamze Kullanıcı adı ve parolasıyla oturum açar ve sunucu çiğdem kimlik doğrulaması için parolayı kullanır.
- *Yetkilendirme* , bir kullanıcının bir eylem gerçekleştirmesine izin verilip verilmediği konusunda karar verebilir. Örneğin, Gamze 'nin bir kaynağı almak için izni vardır ancak kaynağı oluşturmamalıdır.

Serideki ilk makale, ASP.NET Web API 'sinde kimlik doğrulamaya ve yetkilendirmeye genel bir bakış sunar. Diğer konular, Web API 'SI için ortak kimlik doğrulama senaryolarını anlatmaktadır.

> [!NOTE]
> Bu seriyi inceleyen ve değerli geri bildirimleri sağlayan kişiler için teşekkürler: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.

## <a name="authentication"></a>Kimlik doğrulaması

Web API 'SI, kimlik doğrulamasının konakta gerçekleştiğini varsayar. Web barındırma için, ana bilgisayar IIS 'dir ve kimlik doğrulaması için HTTP modüllerini kullanır. Projenizi IIS veya ASP.NET 'te yerleşik olarak bulunan kimlik doğrulama modüllerinden birini kullanacak şekilde yapılandırabilir veya özel kimlik doğrulaması gerçekleştirmek için kendi HTTP modülünüzü yazabilirsiniz.

Ana bilgisayar kullanıcının kimliğini doğruladığında, kodun çalıştığı güvenlik bağlamını temsil eden bir [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) nesnesi olan bir *sorumlu*oluşturur. Ana bilgisayar, **iş parçacığının. CurrentPrincipal**öğesini ayarlayarak sorumluyu geçerli iş parçacığına iliştirir. Asıl öğe, kullanıcıyla ilgili bilgiler içeren ilişkili bir **kimlik** nesnesi içerir. Kullanıcının kimliği doğrulandıysa, **Identity. IsAuthenticated** özelliği **true**değerini döndürür. Anonim istekler için, **IsAuthenticated** , **false**döndürür. Sorumlular hakkında daha fazla bilgi için bkz. [rol tabanlı güvenlik](https://msdn.microsoft.com/library/shz8h065.aspx).

### <a name="http-message-handlers-for-authentication"></a>Kimlik doğrulaması için HTTP Ileti Işleyicileri

Kimlik doğrulaması için konağın kullanılması yerine, kimlik doğrulama mantığını bir [http ileti işleyicisine](../advanced/http-message-handlers.md)koyabilirsiniz. Bu durumda, ileti işleyicisi HTTP isteğini inceler ve sorumluyu ayarlar.

Kimlik doğrulaması için ileti işleyicilerini ne zaman kullanmalısınız? Aşağıda bazı dengeler verilmiştir:

- HTTP modülü, ASP.NET ardışık düzeni üzerinden geçen tüm istekleri görür. İleti işleyicisi yalnızca Web API 'sine yönlendirilen istekleri görür.
- Belirli bir rotaya bir kimlik doğrulama düzeni uygulamanıza olanak sağlayan yönlendirme başına ileti işleyicileri ayarlayabilirsiniz.
- HTTP modülleri IIS 'e özeldir. İleti işleyicileri ana bilgisayar belirsiz olduğundan, hem Web barındırma hem de kendiliğinden barındırma ile kullanılabilir.
- HTTP modülleri, IIS günlüğe kaydetme, denetleme vb. için de yer alır.
- HTTP modülleri, ardışık düzende daha önce çalışır. Kimlik doğrulamasını bir ileti işleyicisinde işletin, bu, işleyici çalışana kadar küme almaz. Ayrıca, yanıt ileti işleyiciden ayrıldığında, sorumlu önceki sorumluya geri döner.

Genellikle, kendi kendine barındırmayı desteklemeniz gerekmiyorsa, HTTP modülü daha iyi bir seçenektir. Kendi kendine barındırmayı desteklemeniz gerekiyorsa bir ileti işleyicisini düşünün.

### <a name="setting-the-principal"></a>Sorumluyu ayarlama

Uygulamanız herhangi bir özel kimlik doğrulama mantığı gerçekleştirirse, sorumluyu iki yerde ayarlamanız gerekir:

- **Thread. CurrentPrincipal**. Bu özellik, .NET 'teki iş parçacığının sorumlusunu ayarlamaya yönelik standart bir yoldur.
- **HttpContext. Current. User**. Bu özellik ASP.NET 'e özgüdür.

Aşağıdaki kod, sorumlunun nasıl ayarlanacağını göstermektedir:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Web barındırma için, sorumluyu her iki yerde de ayarlamanız gerekir; Aksi takdirde güvenlik bağlamı tutarsız hale gelebilir. Ancak, kendi kendine barındırma için **HttpContext. Current** null. Kodunuzun konağın belirsiz olduğundan emin olmak için, gösterildiği gibi **HttpContext. Current**öğesine atamadan önce null değerini denetleyin.

## <a name="authorization"></a>Yetkilendirme

Yetkilendirme, daha sonra işlem hattında denetleyiciye yaklaşarak gerçekleşir. Bu, kaynaklara erişim izni verdiğinizde daha ayrıntılı seçimler yapmanızı sağlar.

- *Yetkilendirme filtreleri* , denetleyici eyleminden önce çalışır. İstek yetkilendirilmezse, filtre bir hata yanıtı döndürür ve eylem çağrılmaz.
- Bir denetleyici eylemi içinde, **Apicontroller. User** özelliğinden geçerli sorumluyu alabilirsiniz. Örneğin, bir kaynak listesini Kullanıcı adına göre filtreleyerek yalnızca o kullanıcıya ait olan kaynakları geri alabilirsiniz.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>[Yetkilendir] özniteliğini kullanma

Web API 'SI, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)yerleşik bir yetkilendirme filtresi sağlar. Bu filtre, kullanıcının kimliğinin doğrulandığını denetler. Aksi takdirde, eylemi çağırmadan HTTP durum kodu 401 (yetkilendirilmemiş) döndürür.

Filtreyi denetleyici düzeyinde küresel olarak veya tek tek eylemler düzeyinde uygulayabilirsiniz.

**Küresel**: her Web API denetleyicisine erişimi kısıtlamak için, genel filtre listesine **AuthorizeAttribute** filtresini ekleyin:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**Denetleyici**: belirli bir denetleyicinin erişimini kısıtlamak için, filtreyi denetleyiciye bir öznitelik olarak ekleyin:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**Eylem**: belirli eylemlerin erişimini kısıtlamak için, eylem yöntemine özniteliği ekleyin:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

Alternatif olarak, `[AllowAnonymous]` özniteliğini kullanarak denetleyiciyi kısıtlayabilir ve sonra belirli eylemlere anonim erişime izin verebilirsiniz. Aşağıdaki örnekte `Post` yöntemi kısıtlıdır, ancak `Get` yöntemi anonim erişime izin verir.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

Önceki örneklerde, filtre tüm kimliği doğrulanmış kullanıcıların kısıtlı yöntemlere erişmesine izin verir; yalnızca anonim kullanıcılar tutulur. Ayrıca, erişimi belirli kullanıcılara veya belirli rollerdeki kullanıcılara sınırlayabilirsiniz:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API denetleyicileri için **AuthorizeAttribute** filtresi **System. Web. http** ad alanında bulunur. **System. Web. Mvc** ad alanında, Web API denetleyicileriyle uyumlu olmayan MVC denetleyicileri için benzer bir filtre vardır.

### <a name="custom-authorization-filters"></a>Özel Yetkilendirme filtreleri

Özel bir yetkilendirme filtresi yazmak için, bu türlerden birini türetebilirsiniz:

- **AuthorizeAttribute**. Geçerli kullanıcıya ve kullanıcının rollerine göre yetkilendirme mantığını gerçekleştirmek için bu sınıfı genişletin.
- **Authorizationfilterattribute**. Geçerli Kullanıcı veya role dayalı olması gereken zaman uyumlu yetkilendirme mantığını gerçekleştirmek için bu sınıfı genişletin.
- **IAuthorizationFilter**. Zaman uyumsuz yetkilendirme mantığını gerçekleştirmek için bu arabirimi uygulayın; Örneğin, yetkilendirme mantığınızın zaman uyumsuz g/ç veya ağ çağrıları yapıyorsa. (Yetkilendirme mantığınızın CPU ile sınırlı olması durumunda, bir zaman uyumsuz yöntem yazmanıza gerek olmadığından **Authorizationfilterattribute**'tan türemek daha basittir.)

Aşağıdaki diyagramda **AuthorizeAttribute** sınıfının sınıf hiyerarşisi gösterilmektedir.

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>Denetleyici eylemi Içinde yetkilendirme

Bazı durumlarda, bir isteğin devam etmesini sağlayabilir, ancak durumu sorumlu temelinde değiştirebilirsiniz. Örneğin, döndürülen bilgiler kullanıcının rolüne bağlı olarak değişebilir. Bir denetleyici yöntemi içinde, **Apicontroller. User** özelliğinden geçerli sorumluyu alabilirsiniz.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
