---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-cs
title: Rol tabanlı yetkilendirme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğretici, rol çerçevesinin bir kullanıcının rollerini güvenlik bağlamıyla nasıl ilişkilendirdiğini gösteren bir görünüm ile başlar. Ardından rol tabanlı URL 'YI nasıl uygulayacağınızı inceler...
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 4d9b63fa-c3d4-4e85-82b1-26ae3ba3ca1c
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-cs
msc.type: authoredcontent
ms.openlocfilehash: 46153ab310bdee814baaa53c372fb92f8a23ce11
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627731"
---
# <a name="role-based-authorization-c"></a>Rol Tabanlı Yetkilendirme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.11.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_cs.pdf)

> Bu öğretici, rol çerçevesinin bir kullanıcının rollerini güvenlik bağlamıyla nasıl ilişkilendirdiğini gösteren bir görünüm ile başlar. Ardından rol tabanlı URL yetkilendirme kurallarının nasıl uygulanacağını inceler. Bunun ardından, görüntülenen verileri ve bir ASP.NET sayfası tarafından sunulan işlevselliği değiştirmek için bildirim temelli ve programlı bir yöntem kullanma hakkında bakacağız.

## <a name="introduction"></a>Giriş

<a id="_msoanchor_1"> </a> [*Kullanıcı tabanlı yetkilendirme*](../membership/user-based-authorization-cs.md) öğreticisinde, kullanıcıların belirli bir sayfa kümesini ziyaret edebileceklerini belirtmek için URL yetkilendirmesini nasıl kullanacağınızı gördük. `Web.config`yalnızca çok sayıda biçimlendirme sayesinde, ASP.NET yalnızca kimliği doğrulanmış kullanıcıların bir sayfayı ziyaret etmesini izin verebilir. Ya da yalnızca Tito ve Bob kullanıcılarına izin verildiğini veya Sam hariç tüm kimliği doğrulanmış kullanıcılara izin verildiğini göstereceğiz.

URL yetkilendirmesinin yanı sıra, görüntülenecek verileri denetlemeye yönelik bildirim temelli ve programlama tekniklerine ve ziyaret eden kullanıcıyı temel alan bir sayfa tarafından sunulan işlevselliğe baktık. Özellikle, geçerli dizinin içeriğini listelenen bir sayfa oluşturduk. Herkes bu sayfayı ziyaret edebilir, ancak yalnızca kimliği doğrulanmış kullanıcılar dosyaların içeriğini görüntüleyebilir ve dosyaları silebilir.

Kullanıcı tarafından Kullanıcı bazında yetkilendirme kuralları uygulamak, gece, nightmbir muhasebe 'ye kadar büyüyebilir. Daha sürdürülebilir bir yaklaşım rol tabanlı yetkilendirmeyi kullanmaktır. İyi haberler, yetkilendirme kurallarını uygulamak için elden çıkarmada bulunan araçların, Kullanıcı hesapları için yaptıkları gibi rollerle aynı şekilde çalışmasını sağlığımızı de unutmayın. URL Yetkilendirme kuralları, kullanıcılar yerine roller belirtebilir. Kimliği doğrulanmış ve anonim kullanıcılar için farklı çıktılar işleyen LoginView denetimi, oturum açmış kullanıcının rollerine göre farklı içerikleri görüntüleyecek şekilde yapılandırılabilir. Ve rol API 'SI, oturum açmış kullanıcının rollerinin belirlenmesi için yöntemler içerir.

Bu öğretici, rol çerçevesinin bir kullanıcının rollerini güvenlik bağlamıyla nasıl ilişkilendirdiğini gösteren bir görünüm ile başlar. Ardından rol tabanlı URL yetkilendirme kurallarının nasıl uygulanacağını inceler. Bunun ardından, görüntülenen verileri ve bir ASP.NET sayfası tarafından sunulan işlevselliği değiştirmek için bildirim temelli ve programlı bir yöntem kullanma hakkında bakacağız. Haydi başlayın!

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>Rollerin bir kullanıcının güvenlik Içeriğiyle nasıl Ilişkilendirildiğini anlama

Bir istek, ASP.NET işlem hattına her girdiğinde, istek sahibi tanımlayan bilgileri içeren bir güvenlik bağlamı ile ilişkilendirilir. Form kimlik doğrulaması kullanılırken kimlik belirteci olarak bir kimlik doğrulama bileti kullanılır. <a id="_msoanchor_2"> </a> [*Form kimlik doğrulaması*](../introduction/an-overview-of-forms-authentication-cs.md) ve <a id="_msoanchor_3"> </a> [*Forms kimlik doğrulaması yapılandırması ve gelişmiş konular*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) öğreticilerine genel bakış konusunda anlatıldığı gibi `FormsAuthenticationModule`, istek sahibinin kimliğini belirlemekten sorumludur ve bu, [`AuthenticateRequest` olay](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)sırasında yapılır.

Geçerli, zaman aşımı olmayan bir kimlik doğrulama bileti bulunursa `FormsAuthenticationModule`, istek sahibinin kimliğini belirlemek için onu çözer. Yeni bir `GenericPrincipal` nesnesi oluşturur ve bunu `HttpContext.User` nesnesine atar. `GenericPrincipal`gibi bir sorumlunun amacı, kimliği doğrulanmış kullanıcının adını ve hangi rollerin ait olduğunu belirlemektir. Bu amaç, tüm Principal nesnelerinin bir `Identity` özelliğine ve bir `IsInRole(roleName)` yöntemine sahip olduğunu bulmasıdır. Ancak `FormsAuthenticationModule`, rol bilgilerini kaydetme ile ilgilenmez ve oluşturduğu `GenericPrincipal` nesnesi herhangi bir rol belirtmez.

Rol çerçevesi etkinleştirilmişse, `FormsAuthenticationModule` sonrasında [`RoleManagerModule`](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx) http modülü adımları ve `AuthenticateRequest` olayından sonra başlatılan [`PostAuthenticateRequest` olayı](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)sırasında kimliği doğrulanmış kullanıcının rollerini tanımlar. İstek kimliği doğrulanmış bir kullanıcıdan ise `RoleManagerModule`, `FormsAuthenticationModule` tarafından oluşturulan `GenericPrincipal` nesnesinin üzerine yazar ve onu bir [`RolePrincipal` nesnesiyle](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)değiştirir. `RolePrincipal` sınıfı, kullanıcının hangi rollere ait olduğunu belirlemek için roller API 'sini kullanır.

Şekil 1, form kimlik doğrulaması ve rol çatısı kullanılırken ASP.NET işlem hattı iş akışını gösterir. `FormsAuthenticationModule` önce yürütülür, kullanıcıyı kimlik doğrulama bileti aracılığıyla tanımlar ve yeni bir `GenericPrincipal` nesnesi oluşturur. Sonra, `RoleManagerModule` adımları ve `GenericPrincipal` nesnesinin `RolePrincipal` nesne üzerine yazar.

Anonim kullanıcı siteyi ziyaret ederse, `FormsAuthenticationModule` ne de `RoleManagerModule` bir asıl nesne oluşturur.

[Form kimlik doğrulaması ve rol çatısı kullanılırken kimliği doğrulanmış bir kullanıcı için ASP.NET işlem hattı olaylarını ![](role-based-authorization-cs/_static/image2.png)](role-based-authorization-cs/_static/image1.png)

**Şekil 1**: form kimlik doğrulaması ve rol çatısı kullanılırken kimliği doğrulanmış bir kullanıcı için ASP.net Işlem hattı olayları ([tam boyutlu görüntüyü görüntülemek için tıklatın](role-based-authorization-cs/_static/image3.png))

### <a name="caching-role-information-in-a-cookie"></a>Tanımlama bilgisinde rol bilgilerini önbelleğe alma

`RolePrincipal` nesnesinin `IsInRole(roleName)` yöntemi, kullanıcının *roleName*'in bir üyesi olup olmadığını belirlemesi için Kullanıcı rollerini almak üzere `Roles.GetRolesForUser` çağırır. `SqlRoleProvider`kullanılırken, bu, rol deposu veritabanına yönelik bir sorgu ile sonuçlanır. Rol tabanlı URL Yetkilendirme kuralları kullanılırken, rol tabanlı URL Yetkilendirme kuralları tarafından korunan bir sayfaya `RolePrincipal``IsInRole` yöntemi her istekte çağrılır. Her istekte veritabanında rol bilgilerini aramak yerine, roller çerçevesi kullanıcının bir tanımlama bilgisinde Kullanıcı rollerini önbelleğe alma seçeneği içerir.

Rol çerçevesi kullanıcının bir tanımlama bilgisinde Kullanıcı rollerini önbelleğe almak üzere yapılandırılmışsa `RoleManagerModule`, ASP.NET işlem hattının [`EndRequest` olayı](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)sırasında tanımlama bilgisini oluşturur. Bu tanımlama bilgisi, `RolePrincipal` nesnesi oluşturulduğunda `PostAuthenticateRequest`sonraki isteklerde kullanılır. Tanımlama bilgisi geçerliyse ve süresi dolmamışsa, tanımlama bilgisindeki veriler ayrıştırılır ve Kullanıcı rollerini doldurmak için kullanılır. böylece, `RolePrincipal` kullanıcının rollerini belirlemede `Roles` sınıfına bir çağrı yapmak için sahip olmaya sahip olma. Şekil 2 Bu iş akışını gösterir.

[![, performansı artırmak için kullanıcının rol bilgileri bir tanımlama bilgisinde depolanabilir](role-based-authorization-cs/_static/image5.png)](role-based-authorization-cs/_static/image4.png)

**Şekil 2**: kullanıcının rol bilgileri, performansı artırmak Için bir tanımlama bilgisinde depolanabilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](role-based-authorization-cs/_static/image6.png))

Rol önbelleği tanımlama bilgisi mekanizması varsayılan olarak devre dışıdır. Bu, `Web.config``<roleManager>` yapılandırma işaretlemesi aracılığıyla etkinleştirilebilir. <a id="_msoanchor_4"> </a> [*Rolleri oluşturma ve yönetme*](creating-and-managing-roles-cs.md) öğreticisinde rol sağlayıcılarını belirlemek için [`<roleManager>` öğesini](https://msdn.microsoft.com/library/ms164660.aspx) kullanarak anlatıldık, bu nedenle uygulamanızın `Web.config` dosyasında bu öğeye zaten sahip olmanız gerekir. Rol önbelleği tanımlama bilgisi ayarları `<roleManager>` öğesinin öznitelikleri olarak belirtilir ve tablo 1 ' de özetlenir.

> [!NOTE]
> Tablo 1 ' de listelenen yapılandırma ayarları, sonuçta elde edilen rol önbelleği tanımlama bilgisinin özelliklerini belirtir. Tanımlama bilgileri, nasıl çalıştıkları ve çeşitli özellikleri hakkında daha fazla bilgi için [Bu tanımlama bilgileri öğreticisini](http://www.quirksmode.org/js/cookies.html)okuyun.

| <strong>Özellik</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>Açıklama</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              Tanımlama bilgisi önbelleklemesi kullanılıp kullanılmayacağını belirten bir Boole değeri. `false` değerini varsayılan olarak alır.                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     Rol önbelleği tanımlama bilgisinin adı. Varsayılan değer ". ASPXROLES ".                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                Rol adı tanımlama bilgisinin yolu. Path özniteliği, bir geliştiricinin bir tanımlama bilgisinin kapsamını belirli bir dizin hiyerarşisine sınırlandırmalarını sağlar. Varsayılan değer "/" ' dir ve bu, tarayıcıya kimlik doğrulama bileti tanımlama bilgisini, etki alanına yapılan herhangi bir isteğe gönderilmek üzere bildirir.                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               Rol önbelleği tanımlama bilgisini korumak için kullanılan teknikleri gösterir. İzin verilen değerler şunlardır: `All` (varsayılan); `Encryption`; `None`; ve `Validation`. Bu koruma düzeyleri hakkında daha fazla bilgi <a id="_anchor_5"> </a>için [*form kimlik doğrulaması yapılandırması ve gelişmiş konular*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) öğreticisindeki 3. adıma geri bakın.                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   Kimlik doğrulama tanımlama bilgisini iletmek için bir SSL bağlantısının gerekli olup olmadığını belirten bir Boolean değer. Varsayılan değer `false` şeklindedir.                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  Tek bir oturum sırasında kullanıcının siteyi ziyaret ettiği her seferinde tanımlama bilgisinin zaman aşımının sıfırlanıp sıfırlanmayacağını belirten bir Boole değeri. Varsayılan değer `false` şeklindedir. Bu değer yalnızca `createPersistentCookie` `true`olarak ayarlandığında geçerlidir.                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         Kimlik doğrulama anahtarı tanımlama bilgisinin süresinin dolacağı süreyi dakika olarak belirtir. Varsayılan değer `30` şeklindedir. Bu değer yalnızca `createPersistentCookie` `true`olarak ayarlandığında geçerlidir.                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   Rol önbelleği tanımlama bilgisinin bir oturum tanımlama bilgisi veya kalıcı tanımlama bilgisi olup olmadığını belirten bir Boolean değer. `false` (varsayılan), tarayıcı kapalıyken silinen bir oturum tanımlama bilgisi kullanılır. `true`, kalıcı bir tanımlama bilgisi kullanılır; Bu, `cookieSlidingExpiration`değerine bağlı olarak, oluşturulduktan sonra veya önceki ziyaretden sonra geçecek süre sonu `cookieTimeout`.                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 Tanımlama bilgisinin etki alanı değerini belirtir. Varsayılan değer boş bir dizedir ve bu, tarayıcının verildiği etki alanını kullanmasına neden olur (örneğin, www.yourdomain.com). Bu durumda, admin.yourdomain.com gibi alt etki alanlarına istek yapıldığında tanımlama bilgisi gönderilmez. Tanımlama bilgisinin tüm alt etki alanlarına geçirilmesini istiyorsanız, `domain` özniteliğini özelleştirmeniz gerekir, bu, "yourdomain.com" olarak ayarlanıyor.                                                                                                                                                 |
|    `maxCachedResults`     | Tanımlama bilgisinde önbelleğe alınan en fazla rol adı sayısını belirtir. Varsayılan değer 25 ' tir. `RoleManagerModule`, `maxCachedResults` rollerden fazlasına ait olan kullanıcılar için tanımlama bilgisi oluşturmaz. Sonuç olarak, `RolePrincipal` nesnesinin `IsInRole` yöntemi kullanıcının rollerini öğrenmek için `Roles` sınıfını kullanacaktır. `maxCachedResults` nedeni, birçok kullanıcı aracısının 4.096 bayttan daha büyük tanımlama bilgilerine izin vermediği için oluşur. Bu nedenle bu sınır, bu boyut sınırlamasını aşmadan daha fazla azaltıyordu. Son derece uzun rol adlarınız varsa, daha küçük bir `maxCachedResults` değeri belirtmeyi düşünmek isteyebilirsiniz. aksine, son derece kısa rol adlarınız varsa, büyük olasılıkla bu değeri artırabilirsiniz. |

**Tablo 1:** Rol önbelleği tanımlama bilgisi yapılandırma seçenekleri

Uygulamamızı kalıcı olmayan rol önbelleği tanımlama bilgilerini kullanacak şekilde yapılandıralim. Bunu gerçekleştirmek için `Web.config` `<roleManager>` öğesini aşağıdaki tanımlama bilgisiyle ilgili öznitelikleri içerecek şekilde güncelleştirin:

[!code-xml[Main](role-based-authorization-cs/samples/sample1.xml)]

`<roleManager>` öğesini üç öznitelik ekleyerek güncelleştirdim: `cacheRolesInCookie`, `createPersistentCookie`ve `cookieProtection`. `cacheRolesInCookie` `true`olarak ayarlayarak `RoleManagerModule` artık kullanıcının rollerini her istekte Kullanıcı rolü bilgilerini aramak yerine bir tanımlama bilgisinde otomatik olarak önbelleğe alır. `createPersistentCookie` ve `cookieProtection` özniteliklerini sırasıyla `false` ve `All`olarak ayarlayacağım. Teknik olarak, bu özniteliklerin değerlerini varsayılan değerlerine atadıktan sonra belirtmem gerekmez, ancak kalıcı tanımlama bilgileri kullanmadığımı ve tanımlama bilgisinin hem şifreli hem de doğrulanan olduğunu açıkça ortadan kaldırmak için bunları buraya yerleştirdim.

İşte bu kadar kolay! Henceileri, rol çerçevesi kullanıcıların tanımlama bilgilerinde kullanıcı rollerini önbelleğe alacak. Kullanıcının tarayıcısı tanımlama bilgilerini desteklemiyorsa veya kendi tanımlama bilgileri silinirse veya kaybolursa, bu durum büyük bir anlaşma değildir. `RolePrincipal` nesnesi, hiçbir tanımlama bilgisinin (veya geçersiz veya zaman aşımına uğramamış bir) kullanılabilir olması durumunda `Roles` sınıfını kullanır.

> [!NOTE]
> Microsoft 'un düzenleri &amp; uygulamalar grubu, kalıcı rol önbelleği tanımlama bilgilerini kullanarak etkilenmeden. Rol önbelleği tanımlama bilgisinin sahibi rol üyeliğini kanıtlamak için yeterli olduğundan, bir korsan bir şekilde geçerli bir kullanıcının tanımlama bilgisine erişim elde edebiliyorsanız, bu kullanıcının kimliğine bürünebilir. Tanımlama bilgisinin Kullanıcı tarayıcısında kalıcı olması durumunda bu oluşma olasılığı artar. Bu güvenlik önerisi ve diğer güvenlik sorunları hakkında daha fazla bilgi için, [ASP.NET 2,0 güvenlik sorusu listesine](https://msdn.microsoft.com/library/ms998375.aspx)bakın.

## <a name="step-1-defining-role-based-url-authorization-rules"></a>1\. Adım: rol tabanlı URL Yetkilendirme kuralları tanımlama

<a id="_msoanchor_6"> </a> [*Kullanıcı tabanlı yetkilendirme*](../membership/user-based-authorization-cs.md) öğreticisinde açıklandığı gibi, URL yetkilendirmesi bir kullanıcı veya rol temelinde bir sayfa kümesine erişimi kısıtlamak için bir yol sunar. URL Yetkilendirme kuralları, `<allow>` ve `<deny>` alt öğeleri ile [`<authorization>` öğesi](https://msdn.microsoft.com/library/8d82143t.aspx) kullanılarak `Web.config` yazılır. Önceki öğreticilerde ele alınan kullanıcı ile ilgili yetkilendirme kurallarına ek olarak, her bir `<allow>` ve `<deny>` alt öğesi de şunlar olabilir:

- Belirli bir rol
- Bir virgülle ayrılmış rol listesi

Örneğin, URL Yetkilendirme kuralları Yöneticiler ve süper yönetici rollerindeki bu kullanıcılara erişim verir, ancak diğerlerinin erişimine izin vermez:

[!code-xml[Main](role-based-authorization-cs/samples/sample2.xml)]

Yukarıdaki İşaretlemede `<allow>` öğesi, Yöneticiler ve denetim rollerinin izin verildiğini belirtir; `<deny>` öğesi *Tüm* kullanıcıların reddedildiğini söyler.

`ManageRoles.aspx`, `UsersAndRoles.aspx`ve `CreateUserWizardWithRoles.aspx` sayfaları yalnızca Yöneticiler rolündeki kullanıcıların erişimine açık olsa da, `RoleBasedAuthorization.aspx` sayfası tüm ziyaretçilerin erişimine devam ederken uygulamamızı yapılandıralim.

Bunu gerçekleştirmek için, `Roles` klasörüne bir `Web.config` dosyası ekleyerek başlayın.

[![roller dizinine Web. config dosyası ekleyin](role-based-authorization-cs/_static/image8.png)](role-based-authorization-cs/_static/image7.png)

**Şekil 3**: `Roles` dizinine bir `Web.config` dosyası ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image9.png))

Sonra, `Web.config`için aşağıdaki yapılandırma işaretlemesini ekleyin:

[!code-xml[Main](role-based-authorization-cs/samples/sample3.xml)]

`<system.web>` bölümündeki `<authorization>` öğesi, yalnızca Yöneticiler rolündeki kullanıcıların `Roles` dizinindeki ASP.NET kaynaklarına erişebileceğini gösterir. `<location>` öğesi `RoleBasedAuthorization.aspx` sayfası için alternatif bir URL Yetkilendirme kuralları kümesi tanımlar ve tüm kullanıcıların sayfayı ziyaret etmesini sağlar.

Değişikliklerinizi `Web.config`kaydettikten sonra, Yöneticiler rolünde olmayan bir kullanıcı olarak oturum açın ve ardından korumalı sayfalardan birini ziyaret etmeyi deneyin. `UrlAuthorizationModule`, istenen kaynağı ziyaret etme izniniz yok olarak algılanır; Sonuç olarak, `FormsAuthenticationModule` oturum açma sayfasına yönlendirecektir. Oturum açma sayfası bundan sonra `UnauthorizedAccess.aspx` sayfasına yönlendirecektir (bkz. Şekil 4). Oturum açma sayfasından `UnauthorizedAccess.aspx` için bu son yeniden yönlendirme, <a id="_msoanchor_7"> </a> [*Kullanıcı tabanlı yetkilendirme*](../membership/user-based-authorization-cs.md) öğreticisinin 2. adımında oturum açma sayfasına eklediğimiz kod nedeniyle oluşur. Özellikle, oturum açma sayfası bir `ReturnUrl` parametresi içeriyorsa, kimliği doğrulanmış tüm kullanıcıları `UnauthorizedAccess.aspx` otomatik olarak yeniden yönlendirir. Bu parametre, kullanıcının, görüntüleme yetkisine sahip olduğu bir sayfayı görüntülemeyi denemeden sonra oturum açma sayfasında geldiğini gösterir.

[![yalnızca Yöneticiler rolündeki kullanıcılar korunan sayfaları görüntüleyebilir](role-based-authorization-cs/_static/image11.png)](role-based-authorization-cs/_static/image10.png)

**Şekil 4**: yalnızca Yöneticiler rolündeki kullanıcılar korunan sayfaları görüntüleyebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](role-based-authorization-cs/_static/image12.png))

Oturumu kapatın ve yöneticiler rolünde olan bir kullanıcı olarak oturum açın. Artık üç korumalı sayfayı görüntüleyebilmelisiniz.

[![Tito, Administrators rolünde olduğu için UsersAndRoles. aspx sayfasını ziyaret edebilir](role-based-authorization-cs/_static/image14.png)](role-based-authorization-cs/_static/image13.png)

**Şekil 5**: Tito, Administrators rolünde olduğu Için `UsersAndRoles.aspx` sayfasını ziyaret edebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image15.png))

> [!NOTE]
> URL yetkilendirme kurallarını belirtirken – roller veya kullanıcılar için, kuralların bir kerede bir kez çözümlendiğini aklınızda tutmanız önemlidir. Eşleşme bulunduğunda, eşleşme bir `<allow>` veya `<deny>` öğesinde bulunmuna bağlı olarak, Kullanıcı erişim izni verilir veya reddedilir. **Hiçbir eşleşme bulunmazsa, kullanıcıya erişim verilir.** Sonuç olarak, bir veya daha fazla kullanıcı hesabına erişimi kısıtlamak isterseniz, URL yetkilendirme yapılandırmasındaki son öğe olarak bir `<deny>` öğesi kullanmanız zorunludur. **URL yetkilendirme kurallarınız bir**`<deny>`**öğesi içermiyorsa, tüm kullanıcılara erişim izni verilir.** URL yetkilendirme kurallarının nasıl çözümlenmesiyle ilgili daha ayrıntılı bir tartışma için, <a id="_msoanchor_8"> </a> [*Kullanıcı tabanlı yetkilendirme*](../membership/user-based-authorization-cs.md) öğreticisinin "`UrlAuthorizationModule` erişim vermek veya erişimi reddetmek için yetkilendirme kurallarını kullanma" bölümüne bakın.

## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>2\. Adım: Şu anda oturum açmış olan kullanıcının rollerine göre Işlevselliği sınırlandırma

URL yetkilendirmesi, hangi kimliklerin izin verileceğini ve hangilerinin belirli bir sayfayı (veya bir klasör ve alt klasörlerindeki tüm sayfaları) görüntülemesini sağlayan çok parçalı yetkilendirme kuralları belirtmeyi kolaylaştırır. Ancak belirli durumlarda, tüm kullanıcıların bir sayfayı ziyaret etmesini sağlamak isteyebilir, ancak ziyaret eden kullanıcının rollerine göre sayfanın işlevlerini sınırlayabilirsiniz. Bu, kullanıcının rolüne bağlı olarak verileri göstermeyi veya gizlemeyi veya belirli bir role ait kullanıcılara ek işlevler sunmayı gerektirebilir.

Bu tür ince ve rol tabanlı yetkilendirme kuralları, bildirimli veya programlı olarak (ya da ikisinin bir birleşimi aracılığıyla) uygulanabilir. Sonraki bölümde, LoginView denetimi aracılığıyla bildirim temelli ince bir yetkilendirmeyi nasıl uygulayacağınızı öğreneceksiniz. Bundan sonra, programlama tekniklerini keşfedecektir. Ancak, ince grenlik yetkilendirme kuralları uygulamaya bakmadan önce, işlevselliği ziyaret eden kullanıcının rolüne bağlı olan bir sayfa oluşturmanız gerekir.

Bir GridView 'da sistemdeki tüm Kullanıcı hesaplarını listeleyen bir sayfa oluşturalım. GridView, her kullanıcının Kullanıcı adını, e-posta adresini, son oturum açma tarihini ve kullanıcı hakkındaki açıklamaları içerir. GridView, her kullanıcının bilgilerini görüntülemenin yanı sıra düzenleme ve silme özelliklerini de içerir. İlk olarak bu sayfayı tüm kullanıcılar için kullanılabilen Düzenle ve Sil işlevselliğiyle oluşturacağız. "LoginView denetimini kullanma" ve "programlı Işlevselliği sınırlandırma" bölümlerinde, ziyaret eden kullanıcının rolüne bağlı olarak bu özelliklerin nasıl etkinleştirileceğini veya devre dışı bırakılacağını inceleyeceğiz.

> [!NOTE]
> Derlemek üzere yaptığımız ASP.NET sayfası, Kullanıcı hesaplarını göstermek için bir GridView denetimi kullanır. Bu öğretici serisi form kimlik doğrulaması, yetkilendirme, Kullanıcı hesapları ve rollere odaklandığından, GridView denetiminin iç çalışmalarını ele almak çok fazla zaman harcamayı istemiyorum. Bu öğretici, bu sayfayı ayarlamaya yönelik belirli adım adım yönergeler sağlarken, belirli seçimlerin neden yapıldığına ilişkin ayrıntıları veya işlenen çıktıda belirli özellikler hangi etkilerle olduğunu anlamaz. GridView denetimini kapsamlı bir şekilde incelemek için *[ASP.NET 2,0 öğretici serisinde verilerle çalışmalarımı](../../data-access/index.md)* inceleyin.

`Roles` klasöründeki `RoleBasedAuthorization.aspx` sayfasını açarak başlayın. Sayfadan tasarımcı üzerine bir GridView sürükleyin ve `ID` `UserGrid`olarak ayarlayın. Kısa bir süre içinde `Membership.GetAllUsers` yöntemi çağıran ve elde edilen `MembershipUserCollection` nesnesini GridView 'a bağlayan kodu yazacağız. `MembershipUserCollection`, sistemdeki her kullanıcı hesabı için bir `MembershipUser` nesnesi içerir; `MembershipUser` nesneler `UserName`, `Email`, `LastLoginDate`gibi özelliklere sahiptir.

Kullanıcı hesaplarını kılavuza bağlayan kodu yazmadan önce, öncelikle GridView 'un alanlarını tanımlayalim. GridView 'un akıllı etiketinden sonra, alanlar iletişim kutusunu (bkz. Şekil 6) başlatmak için "Sütunları Düzenle" bağlantısına tıklayın. Buradan sol alt köşedeki "alanları otomatik oluştur" onay kutusunun işaretini kaldırın. Bu GridView 'un, özellikleri düzenlemesini ve silmeyi ve silme özelliklerini içermesini istiyoruz. bir CommandField ekleyin ve `ShowEditButton` ve `ShowDeleteButton` özelliklerini doğru olarak ayarlayın. Sonra, `UserName`, `Email`, `LastLoginDate`ve `Comment` özelliklerini görüntülemek için dört alan ekleyin. İki salt okuma özelliği için bir BoundField kullanın (`UserName` ve `LastLoginDate`) ve TemplateFields (`Email` ve `Comment`).

İlk BoundField 'ın `UserName` özelliğini görüntülemesi gerekir; `HeaderText` ve `DataField` özelliklerini "UserName" olarak ayarlayın. Bu alan düzenlenemeyecek, `ReadOnly` özelliğini true olarak ayarlayın. `HeaderText` "Last Login" ve `DataField` "LastLoginDate" olarak ayarlayarak `LastLoginDate` BoundField öğesini yapılandırın. Yalnızca tarihin görüntülenmesi için (Tarih ve saat yerine) bu BoundField 'un çıkışını biçimlendirelim. Bunu gerçekleştirmek için, bu BoundField 'ın `HtmlEncode` özelliğini false olarak ve `DataFormatString` özelliğini "{0:d}" olarak ayarlayın. Ayrıca `ReadOnly` özelliğini true olarak ayarlayın.

İki TemplateField 'ın `HeaderText` özelliklerini "e-posta" ve "Açıklama" olarak ayarlayın.

[GridView 'un alanları alanlar Iletişim kutusu aracılığıyla yapılandırılabilir ![](role-based-authorization-cs/_static/image17.png)](role-based-authorization-cs/_static/image16.png)

**Şekil 6**: GridView 'un alanları alanlar Iletişim kutusu aracılığıyla yapılandırılabilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image18.png))

Artık, "e-posta" ve "Açıklama" TemplateFields için `ItemTemplate` ve `EditItemTemplate` tanımlamanız gerekir. `ItemTemplate` s 'ye bir etiket Web denetimi ekleyin ve `Text` özelliklerini sırasıyla `Email` ve `Comment` özelliklerine bağlayın.

"E-posta" TemplateField alanı için `EditItemTemplate` `Email` adlı bir metin kutusu ekleyin ve `Text` özelliğini iki yönlü veri bağlamayı kullanarak `Email` özelliğine bağlayın. E-posta özelliğini düzenleyen bir ziyaretçinin geçerli bir e-posta adresi girdiğinden emin olmak için `EditItemTemplate` bir RequiredFieldValidator ve RegularExpressionValidator ekleyin. "Açıklama" TemplateField için, `EditItemTemplate``Comment` adlı çok satırlı bir metin kutusunu ekleyin. TextBox 'ın `Columns` ve `Rows` özelliklerini sırasıyla 40 ve 4 olarak ayarlayın ve ardından `Text` özelliğini, iki yönlü veri bağlamayı kullanarak `Comment` özelliğine bağlayın.

Bu TemplateFields yapılandırıldıktan sonra, bildirimsel işaretlemesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](role-based-authorization-cs/samples/sample4.aspx)]

Kullanıcı hesabını düzenlediğinizde veya silerken kullanıcının `UserName` özellik değerini bilmeleri gerekir. Bu bilgilerin GridView 'un `DataKeys` koleksiyonuyla kullanılabilmesi için GridView 'un `DataKeyNames` özelliğini "UserName" olarak ayarlayın.

Son olarak, sayfaya bir ValidationSummary denetimi ekleyin ve `ShowMessageBox` özelliğini true ve `ShowSummary` özelliğini false olarak ayarlayın. Bu ayarlarla, Kullanıcı eksik veya geçersiz bir e-posta adresiyle Kullanıcı hesabını düzenlemeye çalışırsa, ValidationSummary bir istemci tarafı uyarısı görüntüler.

[!code-aspx[Main](role-based-authorization-cs/samples/sample5.aspx)]

Bu sayfanın bildirim temelli işaretlemesini şimdi tamamladık. Sonraki göreviniz, Kullanıcı hesaplarının kümesini GridView 'a bağlayavidir. `Membership.GetAllUsers` tarafından döndürülen `MembershipUserCollection` `UserGrid` GridView 'a bağlayan `RoleBasedAuthorization.aspx` sayfasının arka plan kod sınıfına `BindUserGrid` adlı bir yöntem ekleyin. İlk sayfadaki `Page_Load` olay işleyicisinden bu yöntemi çağırın.

[!code-csharp[Main](role-based-authorization-cs/samples/sample6.cs)]

Bu kodla birlikte, sayfayı bir tarayıcıdan ziyaret edin. Şekil 7 ' de gösterildiği gibi, sistemdeki her bir kullanıcı hesabı hakkında bilgi listelemesi görmeniz gerekir.

[UserGrid GridView ![sistemdeki her kullanıcı hakkında bilgi listeler](role-based-authorization-cs/_static/image20.png)](role-based-authorization-cs/_static/image19.png)

**Şekil 7**: GridView `UserGrid`, sistemdeki her kullanıcı hakkında bilgileri listeler ([tam boyutlu görüntüyü görüntülemek için tıklatın](role-based-authorization-cs/_static/image21.png))

> [!NOTE]
> `UserGrid` GridView, sayfalama olmayan bir arabirimdeki tüm kullanıcıları listeler. Bu basit kılavuz arabirimi birçok düzine veya daha fazla kullanıcı olduğu senaryolar için uygun değildir. Bir seçenek, GridView 'ı sayfalamayı etkinleştirecek şekilde yapılandırmaktır. `Membership.GetAllUsers` yönteminin iki aşırı yüklemesi vardır: giriş parametresi yok kabul eden ve tüm kullanıcıları ve sayfa dizini ve sayfa boyutu için tamsayı değerleri alan bir tane döndüren ve yalnızca belirtilen kullanıcıların alt kümesini döndüren bir tane. İkinci aşırı yükleme, Kullanıcı hesaplarının yalnızca tam alt kümesini değil, bunların *tümünün* yerine daha verimli bir şekilde sayfa eklemek için kullanılabilir. Binlerce Kullanıcı hesabınız varsa, örneğin, yalnızca Kullanıcı adı seçili bir karakterle başlayan kullanıcıları gösteren filtre tabanlı bir arabirim göz önünde bulundurmanız isteyebilirsiniz. [`Membership.FindUsersByName method`](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) , filtre tabanlı bir kullanıcı arabirimi oluşturmak için idealdir. Gelecek öğreticide böyle bir arabirim oluşturmaya bakacağız.

GridView denetimi, denetim, SqlDataSource veya ObjectDataSource gibi doğru şekilde yapılandırılmış bir veri kaynağı denetimine bağlandığında, yerleşik Düzenle ve silme desteği sunar. Ancak, GridView `UserGrid`, verilerine programlı bir şekilde bağlanır; Bu nedenle, bu iki görevi gerçekleştirmek için kod yazmanız gerekir. Özellikle, bir ziyaretçi GridView 'un Düzenle, Iptal, güncelleştirme veya silme düğmelerine tıkladığı zaman harekete geçirilen GridView 'un `RowEditing`, `RowCancelingEdit`, `RowUpdating`ve `RowDeleting` olayları için olay işleyicileri oluşturuyoruz.

GridView 'un `RowEditing`, `RowCancelingEdit`ve `RowUpdating` olayları için olay işleyicileri oluşturarak başlayın ve ardından aşağıdaki kodu ekleyin:

[!code-csharp[Main](role-based-authorization-cs/samples/sample7.cs)]

`RowEditing` ve `RowCancelingEdit` olay işleyicileri, GridView 'un `EditIndex` özelliğini ayarlamak ve ardından Kullanıcı hesapları listesini kılavuza yeniden bağlamanız yeterlidir. İlginç şeyler `RowUpdating` olay işleyicisinde meydana gelir. Bu olay işleyicisi, verilerin geçerli olduğundan emin olarak başlar ve sonra düzenlenen Kullanıcı hesabının `UserName` değerini `DataKeys` koleksiyonundan daha büyük bir değere dönüştürür. İki TemplateFields ' `EditItemTemplate` s içindeki `Email` ve `Comment` metin kutularına programlı olarak başvurulur. `Text` özellikleri düzenlenen e-posta adresini ve yorumunu içerir.

Üyelik API 'SI aracılığıyla bir kullanıcı hesabını güncelleştirmek için öncelikle `Membership.GetUser(userName)`çağrısı aracılığıyla yaptığımız Kullanıcı bilgilerini alması gerekir. Döndürülen `MembershipUser` nesnenin `Email` ve `Comment` özellikleri, daha sonra, düzen arabiriminden iki metin kutularına girilen değerlerle güncellenir. Son olarak, bu değişiklikler [`Membership.UpdateUser`](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)çağrısıyla kaydedilir. `RowUpdating` olay işleyicisi, GridView 'un önceden düzenlenen arabirimine geri dönerek tamamlanır.

Sonra, `RowDeleting` olay işleyicisini oluşturun ve ardından aşağıdaki kodu ekleyin:

[!code-csharp[Main](role-based-authorization-cs/samples/sample8.cs)]

Yukarıdaki olay işleyicisi, GridView 'un `DataKeys` koleksiyonundan `UserName` değeri ile başlar; Bu `UserName` değer daha sonra üyelik sınıfının [`DeleteUser` yöntemine](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)geçirilir. `DeleteUser` yöntemi, ilgili üyelik verileri (Bu kullanıcının ait olduğu roller gibi) dahil olmak üzere, sistemden Kullanıcı hesabını siler. Kullanıcı silindikten sonra, kılavuzun `EditIndex`-1 olarak ayarlanır (başka bir satır düzenleme modundayken kullanıcının Sil ' i tıklamış olması durumunda) ve `BindUserGrid` yöntemi çağırılır.

> [!NOTE]
> Sil düğmesi Kullanıcı hesabını silmeden önce kullanıcıdan bir onay sıralaması gerektirmez. Yanlışlıkla silinmekte olan bir hesabın olasılığını azaltmak için bir kullanıcı onayı formu eklemenizi öneririz. Bir eylemi onaylamaya yönelik en kolay yollarından biri, istemci tarafı onaylama iletişim kutusunu kullanmaktır. Bu teknik hakkında daha fazla bilgi için bkz. [silerken Istemci tarafı onaylama ekleme](https://asp.net/learn/data-access/tutorial-42-cs.aspx).

Bu sayfanın beklendiği gibi çalıştığını doğrulayın. Herhangi bir kullanıcının e-posta adresini ve açıklamasını düzenleyebilmeniz ve herhangi bir kullanıcı hesabını silmeniz gerekir. `RoleBasedAuthorization.aspx` sayfasına tüm kullanıcılar tarafından erişilebildiği için, tüm Kullanıcı ve anonim ziyaretçiler, bu sayfayı ziyaret edebilir ve Kullanıcı hesaplarını düzenleyebilir ve silebilir! Bu sayfayı yalnızca, süper Yöneticiler ve yöneticiler rollerinin bir kullanıcının e-posta adresini ve açıklamasını düzenleyebilmesi ve yalnızca yöneticilerin bir kullanıcı hesabını silebilmesi için güncelleştirelim.

"LoginView denetimini kullanma" bölümü, kullanıcının rolüne özgü yönergeleri göstermek için LoginView denetimini kullanma bölümüne bakar. Yöneticiler rolündeki bir kişi bu sayfayı ziyaret ederse, kullanıcıları düzenleme ve silmeye yönelik yönergeler gösterilecektir. Süper vizörler rolündeki bir Kullanıcı bu sayfaya ulaşırsa, kullanıcıları düzenlemeyle ilgili yönergeler gösterilecektir. Ziyaretçi anonimse veya süper yönetici ya da yöneticiler rolünde değilse, Kullanıcı hesabı bilgilerini düzenleyemediğini veya silememeyi açıklayan bir ileti görüntüleriz. "Program aracılığıyla kısıtlama Işlevselliği" bölümünde, kullanıcı rolüne bağlı olarak Düzenle ve Sil düğmelerini programlı bir şekilde gösteren veya gizleyen kodu yazacağız.

### <a name="using-the-loginview-control"></a>LoginView denetimini kullanma

Geçmiş öğreticilerde gördüğünüze göre, LoginView denetimi, kimliği doğrulanmış ve anonim kullanıcılar için farklı arabirimleri görüntülemek için yararlıdır, ancak LoginView denetimi kullanıcının rollerine göre farklı biçimlendirme görüntülemek için de kullanılabilir. Şimdi ziyaret eden kullanıcının rolüne göre farklı yönergeler görüntülemek için bir LoginView denetimi kullanalım.

`UserGrid` GridView 'un üstüne bir LoginView ekleyerek başlayın. Daha önce anlatıldığı gibi, LoginView denetiminin iki yerleşik şablonu vardır: `AnonymousTemplate` ve `LoggedInTemplate`. Bu şablonların her ikisinde de Kullanıcı bilgilerini düzenleyemediğini veya silmediğini bildiren kısa bir ileti girin.

[!code-aspx[Main](role-based-authorization-cs/samples/sample9.aspx)]

`AnonymousTemplate` ve `LoggedInTemplate`ek olarak, LoginView denetimi role özgü Şablonlar olan *RoleGroups*içerebilir. Her RoleGroup, RoleGroup 'un hangi rollere uygulanacağını belirten `Roles`tek bir özellik içerir. `Roles` özelliği tek bir role ("Administrators" gibi) veya virgülle ayrılmış bir rol listesi ("Yöneticiler, süper vizörler" gibi) olarak ayarlanabilir.

RoleGroups 'u yönetmek için denetimin akıllı etiketindeki "RoleGroups 'u Düzenle" bağlantısına tıklayarak RoleGroup koleksiyon düzenleyicisini açın. İki yeni RoleGroups ekleyin. İlk RoleGroup 'un `Roles` özelliğini "Administrators" ve ikincisi "Supervizors" olarak ayarlayın.

[RoleGroup koleksiyon Düzenleyicisi aracılığıyla LoginView 'ın role özgü şablonlarını yönetmek ![](role-based-authorization-cs/_static/image23.png)](role-based-authorization-cs/_static/image22.png)

**Şekil 8**: RoleGroup koleksiyon Düzenleyicisi aracılığıyla LoginView 'ın role özgü şablonlarını yönetme ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image24.png))

RoleGroup koleksiyon düzenleyicisini kapatmak için Tamam ' ı tıklatın; Bu, LoginView 'ın bildirim temelli işaretlemesini, RoleGroup koleksiyon düzenleyicisinde tanımlanan her RoleGroup için `<asp:RoleGroup>` alt öğesi olan bir `<RoleGroups>` bölümü içerecek şekilde güncelleştirir. Ayrıca, başlangıçta yalnızca `AnonymousTemplate` ve `LoggedInTemplate` listelenen "görünümler" açılan listesi, artık eklenen RoleGroups 'u da içerir.

Rol gruplarını, Kullanıcı hesaplarının nasıl düzenleneceği konusunda yönergeler ve yöneticiler rolündeki kullanıcılar düzenleme ve silmeye yönelik yönergeler görüntülenirken, bu sayede rol gruplarını düzenleyin. Bu değişiklikleri yaptıktan sonra, LoginView 'ın bildirim temelli biçimlendirmesi aşağıdakine benzer olmalıdır.

[!code-aspx[Main](role-based-authorization-cs/samples/sample10.aspx)]

Bu değişiklikleri yaptıktan sonra sayfayı kaydedin ve tarayıcı aracılığıyla ziyaret edin. Önce sayfayı anonim kullanıcı olarak ziyaret edin. "Sistemde oturum açmadınız" iletisi gösterilmelidir. Bu nedenle, herhangi bir kullanıcı bilgisini düzenleyemez veya silemezsiniz. " Daha sonra kimliği doğrulanmış bir kullanıcı olarak oturum açın, ancak bunlar veya Yöneticiler rolünde değildir. Bu kez, "süper vizörlerin veya Yöneticiler rollerinin bir üyesi değilsiniz" iletisini görmeniz gerekir. Bu nedenle, herhangi bir kullanıcı bilgisini düzenleyemez veya silemezsiniz. "

Ardından, ana bilgisayar rolünün üyesi olan bir kullanıcı olarak oturum açın. Bu kez,, role özgü ana bilgisayar iletisini görmeniz gerekir (bkz. Şekil 9). Yöneticiler rolünde bir kullanıcı olarak oturum açarsanız, Yöneticiler rolüne özgü iletiyi görmeniz gerekir (bkz. Şekil 10).

[![deneme tarafı, role özgü ana bilgisayar Iletisini göstermiştir](role-based-authorization-cs/_static/image26.png)](role-based-authorization-cs/_static/image25.png)

**Şekil 9**: deneme tarafı, rol özel iletisini ([tam boyutlu görüntüyü görüntülemek Için tıklayın](role-based-authorization-cs/_static/image27.png)) gösteriliyor

[![Tito, Yöneticiler rolüne özgü Ileti olarak gösteriliyor](role-based-authorization-cs/_static/image29.png)](role-based-authorization-cs/_static/image28.png)

**Şekil 10**: Tito, Yöneticiler rolüne özgü ileti ([tam boyutlu görüntüyü görüntülemek Için tıklayın](role-based-authorization-cs/_static/image30.png)) gösteriliyor

Şekil 9 ve 10 ' da ekran görüntüleri olarak, birden çok şablon olsa bile, LoginView yalnızca bir şablon oluşturur. Deneme ve Tito kullanıcıları oturum açmış, ancak LoginView, `LoggedInTemplate`değil yalnızca eşleşen RoleGroup 'u işler. Ayrıca, Tito hem Yöneticiler hem de süper yönetici rollerine aittir, ancak LoginView denetimi, Yöneticiler rolüne özel şablonu bir tane yerine işler.

Şekil 11 ' de, hangi şablonun işleneceğini belirlemek için LoginView denetimi tarafından kullanılan iş akışı gösterilmektedir. Birden fazla RoleGroup belirtilmişse, LoginView şablonunun eşleşen *ilk* RoleGroup 'u işlediğini unutmayın. Diğer bir deyişle, Supervisors RoleGroup 'u ilk RoleGroup ve Administrators olarak ikinci olarak yerleştirdiyseniz, bu sayfayı ziyaret edildiğinde, Gözevizler iletisini görür.

[Hangi şablonun Işleneceğini belirlemek için LoginView denetiminin Iş akışını ![](role-based-authorization-cs/_static/image32.png)](role-based-authorization-cs/_static/image31.png)

**Şekil 11**: LoginView denetiminin hangi şablonun işleneceğini belirlemek Için iş akışı ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image33.png))

### <a name="programmatically-limiting-functionality"></a>Işlevselliği programlı bir şekilde sınırlandırma

LoginView denetimi, sayfayı ziyaret eden kullanıcının rolüne bağlı olarak farklı yönergeler görüntülediğinde, Düzenle ve Iptal düğmeleri tümü görünür kalır. Anonim ziyaretçiler ve Yöneticiler rolü olmayan kullanıcılar için düzenleme ve silme düğmelerini program aracılığıyla gizlemeniz gerekir. Yönetici olmayan herkes için Sil düğmesini gizlemeniz gerekir. Bunu gerçekleştirmek için, programlı olarak CommandField 'ın Düzenle ve Sil LinkButtons 'a başvuran ve gerekirse `Visible` özelliklerini `false`olarak ayarlayan bir kod yazacağız.

Bir CommandField içindeki denetimlere programlı olarak başvuru yapmanın en kolay yolu, önce onu bir şablona dönüştürmelidir. Bunu gerçekleştirmek için, GridView 'un akıllı etiketindeki "Sütunları Düzenle" bağlantısına tıklayın, geçerli alanlar listesinden CommandField ' ı seçin ve "Bu alanı TemplateField 'a Dönüştür" bağlantısına tıklayın. Bu, CommandField öğesini bir `ItemTemplate` ve `EditItemTemplate`bir TemplateField öğesine dönüştürür. `ItemTemplate`, Update ve DELETE LinkButtons ' a sahip olsa da, `EditItemTemplate` güncelleştirmeyi ve Iptal et düğmelerini barındırır.

[![CommandField 'ı TemplateField 'A dönüştürmek](role-based-authorization-cs/_static/image35.png)](role-based-authorization-cs/_static/image34.png)

**Şekil 12**: CommandField 'ı TemplateField 'a Dönüştür ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image36.png))

`ID` özelliklerini sırasıyla `EditButton` ve `DeleteButton`değerlerine ayarlayarak `ItemTemplate`LinkButtons 'ı Düzenle ve Sil ' i güncelleştirin.

[!code-aspx[Main](role-based-authorization-cs/samples/sample11.aspx)]

GridView 'a veri bağlandığında, GridView `DataSource` özelliğindeki kayıtları numaralandırır ve buna karşılık gelen bir `GridViewRow` nesnesi oluşturur. Her `GridViewRow` nesne oluşturulduğunda, `RowCreated` olay tetiklenir. Yetkisiz kullanıcılara yönelik düzenleme ve silme düğmelerini gizlemek için, bu olay için bir olay işleyicisi oluşturmanız ve programlı olarak Düzenle ve Sil LinkButtons 'a başvurması ve bunlara göre `Visible` özelliklerini ayarlamamız gerekir.

`RowCreated` olayı bir olay işleyicisi oluşturun ve ardından aşağıdaki kodu ekleyin:

[!code-csharp[Main](role-based-authorization-cs/samples/sample12.cs)]

Üst bilgi, alt bilgi, sayfalayıcı arabirimi vb. dahil olmak üzere *Tüm* GridView satırları için `RowCreated` olayının tetiklendiği göz önünde bulundurun. Düzenleme modunda olmayan bir veri satırıyla uğraşıyorsanız, düzenleme ve silme Linkdüğmelerine yalnızca program aracılığıyla başvurmak istiyoruz (düzenleme modundaki satır Düzenle ve Sil yerine Update ve Cancel düğmeleri olduğundan). Bu denetim `if` ifadesiyle işlenir.

Düzenleme modunda olmayan bir veri satırıyla uğraşıyorsanız, Linkve Delete LinkButtons 'a başvurulur ve `Visible` özellikleri `User` nesnenin `IsInRole(roleName)` yöntemi tarafından döndürülen Boole değerlerine göre ayarlanır. Kullanıcı nesnesi, `RoleManagerModule`tarafından oluşturulan sorumluya başvurur; Sonuç olarak, `IsInRole(roleName)` yöntemi geçerli ziyaretçinin *roleName*' e ait olup olmadığını anlamak IÇIN roller API 'sini kullanır.

> [!NOTE]
> Doğrudan rol sınıfını kullandık, `User.IsInRole(roleName)` çağrısını [`Roles.IsUserInRole(roleName)` yöntemine](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)yapılan çağrıdan değiştirin. Rol API 'sini doğrudan kullanmaktan daha verimli olduğundan, bu örnekte asıl nesnenin `IsInRole(roleName)` yöntemini kullanmaya karar verdim. Bu öğreticide daha önce, rol yöneticisini kullanıcının bir tanımlama bilgisinde Kullanıcı rollerini önbelleğe almak üzere yapılandırdık. Bu önbelleğe alınmış tanımlama bilgisi verileri yalnızca birincil öğenin `IsInRole(roleName)` yöntemi çağrıldığında kullanılır; Roller API 'sine doğrudan yapılan çağrılar, her zaman rol deposuna bir seyahat içerir. Roller bir tanımlama bilgisinde önbelleğe alınmasa bile, asıl nesnenin `IsInRole(roleName)` yöntemini çağırmak genellikle daha etkilidir çünkü bu, sonuçları önbellekte bir istek sırasında çağrıldığında ilk kez çağrılır. Diğer yandan rol API 'SI, herhangi bir önbelleğe alma gerçekleştirmez. `RowCreated` olayı, GridView 'daki her satır için bir kez tetiklendiğinden, `User.IsInRole(roleName)` kullanmak rol `Roles.IsUserInRole(roleName)` deposuna yalnızca bir seyahat içerir *. burada* *n* , kılavuzda görünen kullanıcı hesabı sayısıdır.

Bu sayfayı ziyaret eden kullanıcı Yöneticiler veya süper vizörler rolünde ise Düzenle düğmesinin `Visible` özelliği `true` olarak ayarlanır; Aksi takdirde, `false`olarak ayarlanır. Delete düğmesinin `Visible` özelliği, yalnızca kullanıcı Yöneticiler rolünde ise `true` olarak ayarlanır.

Bu sayfayı bir tarayıcı ile test edin. Sayfayı anonim ziyaretçi ya da yönetici olmayan bir kullanıcı olarak ziyaret ederseniz, CommandField boştur; Yine de, düzenleme veya silme düğmeleri olmadan ince bir pahalıdır olarak mevcuttur.

> [!NOTE]
> Yönetici olmayan ve yönetici olmayan bir sayfayı ziyaret edildiğinde CommandField 'ı tamamen gizlemek mümkündür. Bunu okuyucu için bir alıştırma olarak bırakıyorum.

[Düzenleme ve silme düğmeleri ![, süper olmayan ve yönetici olmayan bileşenler için gizlenir](role-based-authorization-cs/_static/image38.png)](role-based-authorization-cs/_static/image37.png)

**Şekil 13**: düzenleme ve silme düğmeleri, süper olmayan ve yönetici olmayan ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image39.png)) için gizlidir

Ana bilgisayarlar rolüne ait olan bir Kullanıcı (Yöneticiler rolüne değil) ziyaret ederse yalnızca Düzenle düğmesini görür.

[![, ana bilgisayarlar için Düzenle düğmesi kullanılabilir durumdayken Sil düğmesi gizlidir](role-based-authorization-cs/_static/image41.png)](role-based-authorization-cs/_static/image40.png)

**Şekil 14**: Düzenle düğmesi üst yöneticiler için kullanılabilir olduğunda, Sil düğmesi gizlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image42.png))

Bir yönetici ziyaret ederse, hem düzenleme hem de silme düğmelerine erişimi vardır.

[![Düzenle ve Sil düğmeleri yalnızca Yöneticiler için kullanılabilir](role-based-authorization-cs/_static/image44.png)](role-based-authorization-cs/_static/image43.png)

**Şekil 15**: Düzenle ve Sil düğmeleri yalnızca Yöneticiler için kullanılabilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](role-based-authorization-cs/_static/image45.png))

## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>3\. Adım: sınıflara ve yöntemlere rol tabanlı yetkilendirme kuralları uygulama

2\. adımda, kullanıcılar ve yöneticiler rollerinin kullanıcıları için düzenleme yeteneklerini sınırlandırdık ve yalnızca yöneticilere yönelik özellikleri silebiliyoruz. Bu, programlı teknikler aracılığıyla yetkisiz kullanıcılar için ilişkili kullanıcı arabirimi öğelerini gizleyerek elde edildi. Bu tür ölçüler, yetkisiz bir kullanıcının ayrıcalıklı bir eylem gerçekleştiremeyeceği garantisi vermez. Daha sonra eklenen veya yetkisiz kullanıcılar için gizlemeyi unutmuş olan kullanıcı arabirimi öğeleri olabilir. Veya bir korsan, istenen yöntemi yürütmek için ASP.NET sayfasını almanın başka bir yolunu da bulabilir.

Belirli bir işlevselliğe yetkisiz bir kullanıcı tarafından erişilememesini sağlamanın kolay bir yolu, bu sınıfı veya yöntemi [`PrincipalPermission` özniteliğiyle](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)tasarlamanız sağlamaktır. .NET çalışma zamanı bir sınıfı kullandığında veya yöntemlerinden birini yürüttüğünde, geçerli güvenlik bağlamının izin aldığından emin olmak için kontrol eder. `PrincipalPermission` özniteliği, bu kuralları tanımlayabilmemiz için bir mekanizma sağlar.

<a id="_msoanchor_9"> </a> [*Kullanıcı tabanlı yetkilendirme*](../membership/user-based-authorization-cs.md) öğreticisinde `PrincipalPermission` özniteliğini geri kullanmaya baktık. Özellikle, GridView 'un `SelectedIndexChanged` ve `RowDeleting` olay işleyicisini yalnızca kimliği doğrulanmış kullanıcılar ve sırasıyla yürütülebilmeleri için nasıl süsletireceğiz gördük. `PrincipalPermission` özniteliği, yalnızca rollerle birlikte kullanılabilir.

`PrincipalPermission`, GridView 'un `RowUpdating` ve `RowDeleting` olay işleyicilerinde, yetkili olmayan kullanıcılar için yürütmeyi yasaklamak için bu özniteliği kullanmayı görelim. Tüm yapmanız gereken, her bir işlev tanımının uygun özniteliğini eklemektir:

[!code-csharp[Main](role-based-authorization-cs/samples/sample13.cs)]

`RowUpdating` olay işleyicisinin özniteliği, yalnızca Yöneticiler veya süper yönetici rollerindeki kullanıcıların olay işleyicisini yürütemeyeceğini belirler. burada, `RowDeleting` olay işleyicisindeki öznitelik, Yöneticiler rolündeki kullanıcılara yürütmeyi sınırlar.

> [!NOTE]
> `PrincipalPermission` özniteliği, `System.Security.Permissions` ad alanındaki bir sınıf olarak temsil edilir. Bu ad alanını içeri aktarmak için arka plan kod sınıfı dosyanızın üst kısmına bir `using System.Security.Permissions` deyim eklediğinizden emin olun.

Yönetici olmayan `RowDeleting` olay işleyicisini yürütmeyi denerse veya yönetici olmayan ya da yönetici olmayan bir `RowUpdating` olay işleyicisini yürütmeye çalışırsa, .NET çalışma zamanı bir `SecurityException`yükseltir.

[![güvenlik bağlamının yöntemi yürütme yetkisi yoksa bir SecurityException atılır](role-based-authorization-cs/_static/image47.png)](role-based-authorization-cs/_static/image46.png)

**Şekil 16**: güvenlik bağlamının yöntemi yürütme yetkisi yoksa bir `SecurityException` oluşturulur ([tam boyutlu görüntüyü görüntülemek için tıklatın](role-based-authorization-cs/_static/image48.png))

ASP.NET sayfalarına ek olarak, birçok uygulamanın Iş mantığı ve veri erişimi katmanları gibi çeşitli katmanları içeren bir mimarisi de vardır. Bu katmanlar genellikle sınıf kitaplıkları olarak uygulanır ve iş mantığı ve verilerle ilgili işlevleri gerçekleştirmek için sınıflar ve yöntemler sunar. `PrincipalPermission` özniteliği, bu katmanlara de yetkilendirme kuralları uygulamak için faydalıdır.

Sınıflarda ve yöntemlerde yetkilendirme kurallarını tanımlamak için `PrincipalPermission` özniteliğini kullanma hakkında daha fazla bilgi için, [`PrincipalPermissionAttributes`kullanarak iş ve veri katmanlarına yetkilendirme kuralları ekleme ](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx) [Scott Guthrie](https://weblogs.asp.net/scottgu/)'nin Blog girdisine bakın.

## <a name="summary"></a>Özet

Bu öğreticide, Kullanıcı rollerine göre kaba ve ince yetkilendirme kuralları belirtme konusunda baktık. ASP.net. NET ' in URL yetkilendirmesi özelliği, sayfa geliştiricisinin hangi sayfaların hangi kimliklere izin verileceğini veya hangilerinin reddedildiğini belirlemesine izin verir. <a id="_msoanchor_10"> </a> [*Kullanıcı tabanlı yetkilendirme*](../membership/user-based-authorization-cs.md) öğreticisinde geri döndüğünüzde, URL Yetkilendirme kuralları Kullanıcı tarafından Kullanıcı temelinde uygulanabilir. Bu öğretici, Bu öğreticinin 1. adımında gördüğünüz gibi rol temelinde da uygulanabilir.

İnce bir yetkilendirme kuralı, bildirimli olarak veya programlı bir şekilde uygulanabilir. 2\. adımda, ziyaret eden kullanıcının rollerine göre farklı çıktılar işlemek için LoginView denetiminin RoleGroups özelliğini kullanma hakkında baktık. Ayrıca, bir kullanıcının belirli bir role ait olup olmadığını ve sayfa işlevselliğinin uygun şekilde nasıl ayarlanacağını anlamak için yol gösteren yolları da inceledik.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [`PrincipalPermissionAttributes` kullanarak Iş ve veri katmanlarına yetkilendirme kuralları ekleme](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 2.0 'ın üyeliğini, rollerini ve profilini İnceleme: rollerle çalışma](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [ASP.NET 2,0 için güvenlik sorusu listesi](https://msdn.microsoft.com/library/ms998375.aspx)
- [`<roleManager>` öğesi için teknik belgeler](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler...

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler suchi Banerjee ve Teresa Murphy ' i içerir. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Önceki](assigning-roles-to-users-cs.md)
> [İleri](creating-and-managing-roles-vb.md)
