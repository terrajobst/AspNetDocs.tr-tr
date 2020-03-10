---
uid: web-api/overview/security/individual-accounts-in-web-api
title: ASP.NET Web API 2,2 ' de bireysel hesaplarla ve yerel oturum açmayla bir Web API 'sinin güvenliğini sağlama | Microsoft Docs
author: MikeWasson
description: Bu konu, bir üyelik veritabanında kimlik doğrulaması yapmak için OAuth2 kullanarak bir Web API 'sinin nasıl güvenli hale alınacağını gösterir. Visual Studio 201 öğreticisinde kullanılan yazılım sürümleri...
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555197"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a>ASP.NET Web API 2,2 ' de bireysel hesaplarla ve yerel oturum açmayla bir Web API 'sinin güvenliğini sağlama

, [Mike te son](https://github.com/MikeWasson)

[Örnek uygulamayı indir](https://github.com/MikeWasson/LocalAccountsApp)

> Bu konu, bir üyelik veritabanında kimlik doğrulaması yapmak için OAuth2 kullanarak bir Web API 'sinin nasıl güvenli hale alınacağını gösterir.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - [Visual Studio 2013 Güncelleştirme 3](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [Web API 2,2](../releases/whats-new-in-aspnet-web-api-22.md)
> - [ASP.NET Identity 2,1](../../../identity/index.md)

Visual Studio 2013, Web API 'SI proje şablonu, kimlik doğrulama için size üç seçenek sunar:

- **Bireysel hesaplar.** Uygulama bir üyelik veritabanı kullanır.
- **Kurumsal hesaplar.** Kullanıcılar Azure Active Directory, Office 365 veya şirket içi Active Directory kimlik bilgileriyle oturum açabilirler.
- **Windows kimlik doğrulaması.** Bu seçenek, Intranet uygulamalarına yöneliktir ve Windows kimlik doğrulaması IIS modülünü kullanır.

Bu seçenekler hakkında daha fazla bilgi için, bkz. [Visual Studio 2013 ASP.NET Web projeleri oluşturma](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth).

Bireysel hesaplar bir kullanıcının oturum açması için iki yol sunar:

- **Yerel oturum açma**. Kullanıcı, siteye kaydolur, bir Kullanıcı adı ve parola girer. Uygulama, parola karmasını üyelik veritabanına depolar. Kullanıcı oturum açtığında, ASP.NET Identity sistem parolayı doğrular.
- **Sosyal oturum açma**. Kullanıcı, Facebook, Microsoft veya Google gibi bir dış hizmetle oturum açar. Uygulama yine de üyelik veritabanında kullanıcı için bir giriş oluşturur, ancak herhangi bir kimlik bilgisi depolamaz. Kullanıcı, dış hizmette oturum açarak kimliğini doğrular.

Bu makale, yerel oturum açma senaryosuna bakar. Hem yerel hem de sosyal oturum açma için Web API 'SI isteklerin kimliğini doğrulamak için OAuth2 kullanır. Ancak, kimlik bilgisi akışları yerel ve sosyal oturum açma için farklıdır.

Bu makalede, kullanıcının oturum açmasına ve bir Web API 'sine kimliği doğrulanmış AJAX çağrıları gönderebilmesine olanak tanıyan basit bir uygulama gösterilmektedir. Örnek kodu [buradan](https://github.com/MikeWasson/LocalAccountsApp)indirebilirsiniz. Readme, Visual Studio 'da örneğin sıfırdan nasıl oluşturulacağını açıklar.

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

Örnek uygulama, AJAX istekleri göndermek için veri bağlama ve jQuery için altını gizleme. js kullanır. AJAX çağrılarına odaklanacağız, bu nedenle bu makale için altını gizleme. js ' yi bilmeniz gerekmez.

Bu şekilde şunları açıklayacağım:

- İstemci tarafında uygulamanın yaptığı işlem.
- Sunucuda neler oluyor.
- Ortadaki HTTP trafiği.

İlk olarak bazı OAuth2 terminolojisi tanımlamamız gerekir.

- *Kaynak*. Korunabilen verilerin bir parçası.
- *Kaynak sunucu*. Kaynağı barındıran sunucu.
- *Kaynak sahibi*. Kaynağa erişim izni veren varlık. (Genellikle kullanıcı.)
- *İstemci*: kaynağa erişmek isteyen uygulama. Bu makalede, istemci bir web tarayıcısıdır.
- *Erişim belirteci*. Kaynağa erişim izni veren bir belirteç.
- *Taşıyıcı belirteci*. Belirli bir erişim belirteci türü, başka birinin belirtecini kullanabileceği özelliği. Diğer bir deyişle, bir istemcinin bir taşıyıcı belirteç kullanması için şifreleme anahtarı veya diğer gizli anahtar gerekmez. Bu nedenle, taşıyıcı belirteçlerinin yalnızca bir HTTPS üzerinden kullanılması ve görece kısa süre sonu süreleri olması gerekir.
- *Yetkilendirme sunucusu*. Erişim belirteçleri veren bir sunucu.

Bir uygulama hem yetkilendirme sunucusu hem de kaynak sunucusu olarak görev yapabilir. Web API proje şablonu bu düzene uyar.

## <a name="local-login-credential-flow"></a>Yerel oturum açma kimlik bilgisi akışı

Yerel oturum açma için Web API, OAuth2 içinde tanımlanan [kaynak sahibi parola akışını](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) kullanır.

1. Kullanıcı istemciye bir ad ve parola girer.
2. İstemci bu kimlik bilgilerini yetkilendirme sunucusuna gönderir.
3. Yetkilendirme sunucusu kimlik bilgilerini doğrular ve bir erişim belirteci döndürür.
4. Korumalı bir kaynağa erişmek için, istemci, HTTP isteğinin yetkilendirme üst bilgisinde erişim belirtecini içerir.

![](individual-accounts-in-web-api/_static/image3.png)

Web API proje şablonunda **bireysel Hesapları** seçtiğinizde, proje Kullanıcı kimlik bilgilerini ve sorun belirteçlerini doğrulayan bir yetkilendirme sunucusu içerir. Aşağıdaki diyagramda, Web API bileşenleri açısından aynı kimlik bilgisi akışı gösterilmektedir.

![](individual-accounts-in-web-api/_static/image4.png)

Bu senaryoda, Web API denetleyicileri kaynak sunucu olarak davranır. Bir kimlik doğrulama filtresi, erişim belirteçlerini doğrular ve **[Yetkilendir]** özniteliği bir kaynağı korumak için kullanılır. Bir denetleyici veya eylem **[Yetkilendir]** özniteliğine sahip olduğunda, bu denetleyiciye veya eyleme yapılan tüm isteklerin kimliği doğrulanmalıdır. Aksi takdirde, yetkilendirme reddedilir ve Web API 'SI bir 401 (yetkisiz) hatası döndürür.

Yetkilendirme sunucusu ve kimlik doğrulama filtresi, her ikisi de OAuth2 ayrıntılarını işleyen bir [Owın ara yazılım](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) bileşenine çağrı gerçekleştirir. Bu öğreticinin ilerleyen kısımlarında tasarımı daha ayrıntılı olarak açıklayacağım.

## <a name="sending-an-unauthorized-request"></a>Yetkisiz bir Istek gönderiliyor

Başlamak için uygulamayı çalıştırın ve **API çağrısı** düğmesine tıklayın. İstek tamamlandığında, **sonuç** kutusunda bir hata mesajı görmeniz gerekir. Bunun nedeni, isteğin bir erişim belirteci içermediği için isteğin yetkisiz olması.

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

**API çağrısı** düğmesi, BIR Web API denetleyicisi eylemi çağıran ~/api/Values 'A bir AJAX isteği gönderir. AJAX isteğini gönderen JavaScript kodunun bölümü aşağıda verilmiştir. Örnek uygulamada, JavaScript uygulama kodunun hepsi, Scripts\app.exe dosyasında bulunur.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

Kullanıcı oturum açana kadar, hiçbir taşıyıcı belirteç yoktur ve bu nedenle istekte yetkilendirme üst bilgisi yoktur. Bu, isteğin bir 401 hatası döndürmesine neden olur.

HTTP isteği aşağıda verilmiştir. (HTTP trafiğini yakalamak için [Fiddler](http://www.telerik.com/fiddler) kullandım.)

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

HTTP yanıtı:

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

Yanıtın, sınama için güçlük ayarlanmış bir WWW-Authenticate üst bilgisi içerdiğine dikkat edin. Bu, sunucunun bir taşıyıcı belirteci beklediğini gösterir.

## <a name="register-a-user"></a>Kullanıcı kaydetme

Uygulamanın **Kaydet** bölümünde bir e-posta ve parola girin ve **Kaydet** düğmesine tıklayın.

Bu örnek için geçerli bir e-posta adresi kullanmanız gerekmez, ancak gerçek bir uygulama adresi doğrulayacağından emin olun. (Bkz. [oturum açma, e-posta onayı ve parola sıfırlama ile güvenli ASP.NET MVC 5 Web uygulaması oluşturma](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) Parola için, büyük harf, küçük harf, sayı ve alfa sayısal olmayan karakter içeren "Parola1!" gibi bir şey kullanın. Uygulamanın basit kalmasını sağlamak için, istemci tarafı doğrulaması kalmadı, bu nedenle parola biçimiyle ilgili bir sorun oluşursa 400 (Hatalı Istek) hatası alırsınız.

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

**Kaydet** düğmesi ~/api/Account/Register/öğesine bir post isteği gönderir. İstek gövdesi, adı ve parolayı tutan bir JSON nesnesidir. İsteği gönderen JavaScript kodu aşağıda verilmiştir:

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

HTTP isteği:

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

HTTP yanıtı:

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

Bu istek `AccountController` sınıfı tarafından işlenir. Dahili olarak, `AccountController` üyelik veritabanını yönetmek için ASP.NET Identity kullanır.

Uygulamayı Visual Studio 'dan yerel olarak çalıştırırsanız, Kullanıcı hesapları AspNetUsers tablosunda LocalDB 'de depolanır. Visual Studio 'da tabloları görüntülemek için **Görünüm** menüsüne tıklayın, **Sunucu Gezgini**ve ardından **veri bağlantıları**' nı seçin.

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a>Erişim belirteci al

Şimdiye kadar hiç OAuth yapmadık, ancak artık bir erişim belirteci istediğimiz zaman, OAuth yetkilendirme sunucusunu eylemde göreceğiz. Örnek uygulamanın **oturum açma** alanında, e-posta ve parolayı girin ve **oturum aç**' a tıklayın.

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

**Oturum aç** düğmesi, belirteç uç noktasına bir istek gönderir. İsteğin gövdesi aşağıdaki biçimde, URL kodlu verileri içerir:

- verme\_türü: "Password"
- Kullanıcı adı: kullanıcının e-posta&gt; &lt;
- parola: parola &lt;&gt;

AJAX isteğini gönderen JavaScript kodu aşağıda verilmiştir:

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

İstek başarılı olursa, yetkilendirme sunucusu yanıt gövdesinde bir erişim belirteci döndürür. API 'ye istek gönderirken daha sonra kullanmak için belirteci oturum depolama alanında depoladığımızda dikkat edin. Bazı kimlik doğrulama biçimlerinden farklı olarak (tanımlama bilgisi tabanlı kimlik doğrulaması gibi) tarayıcı, sonraki isteklere erişim belirtecini otomatik olarak içermez. Uygulamanın bu şekilde açık olması gerekir. [CSRF güvenlik açıklarını](preventing-cross-site-request-forgery-csrf-attacks.md)sınırlayan için bu iyi bir şeydir.

HTTP isteği:

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

İsteğin kullanıcının kimlik bilgilerini içerdiğini görebilirsiniz. Aktarım Katmanı Güvenliği sağlamak için HTTPS kullanmanız *gerekir* .

HTTP yanıtı:

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

Okunabilirlik için, JSON 'u girintili hale aldım ve erişim belirtecini kırptım ve bu çok uzun.

`access_token`, `token_type`ve `expires_in` özellikleri OAuth2 spec tarafından tanımlanır. Diğer Özellikler (`userName`, `.issued`ve `.expires`) yalnızca bilgilendirme amaçlıdır. Bu ek özellikleri ekleyen kodu,/Providers/ApplicationOAuthProvider.cs dosyasındaki `TokenEndpoint` yönteminde bulabilirsiniz.

## <a name="send-an-authenticated-request"></a>Kimliği doğrulanmış bir Istek gönder

Artık bir taşıyıcı Belirtecimiz olduğuna göre, API 'ye kimliği doğrulanmış bir istek yapabiliriz. Bu, istekteki yetkilendirme üst bilgisi ayarlanarak yapılır. Bunu görmek için **API 'Yi çağır** düğmesine tekrar tıklayın.

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

HTTP isteği:

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

HTTP yanıtı:

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a>Oturumu Kapat

Tarayıcı kimlik bilgilerini veya erişim belirtecini önbelleğe içermediğinden, oturum açma işlemi, bu belirteci oturum depolama alanından kaldırarak yalnızca "Foral" olarak belirlenir:

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a>Bireysel hesaplar proje şablonunu anlama

ASP.NET Web uygulaması proje şablonunda **tek tek hesapları** seçtiğinizde, proje şunları içerir:

- Bir OAuth2 yetkilendirme sunucusu.
- Kullanıcı hesaplarını yönetmek için bir Web API uç noktası
- Kullanıcı hesaplarını depolamak için bir EF modeli.

Bu özellikleri uygulayan ana uygulama sınıfları şunlardır:

- `AccountController`. Kullanıcı hesaplarını yönetmek için bir Web API uç noktası sağlar. `Register` eylem, bu öğreticide kullandığımız tek bir işlemdir. Sınıftaki diğer yöntemler parola sıfırlamayı, sosyal oturum açmaları ve diğer işlevleri destekler.
- `ApplicationUser`,/models/ıdentitymodels.csiçinde tanımlanır. Bu sınıf, üyelik veritabanındaki kullanıcı hesapları için EF modelidir.
- `ApplicationUserManager`,/App\_start/ıdentityconfig. cs ' de tanımlanan bu sınıf, [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) 'dan türetilir ve yeni bir Kullanıcı oluşturma, parolaları doğrulama, vb. gibi Kullanıcı hesapları üzerinde işlem gerçekleştirir ve veritabanında yapılan değişiklikleri otomatik olarak devam ettirir.
- `ApplicationOAuthProvider`. Bu nesne, OWıN ara yazılımını takar ve ara yazılım tarafından oluşturulan olayları işler. [Oauthauthorizationserverprovider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)öğesinden türetilir.

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a>Yetkilendirme sunucusunu yapılandırma

StartupAuth.cs ' de, aşağıdaki kod OAuth2 yetkilendirme sunucusunu yapılandırır.

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

`TokenEndpointPath` özelliği, yetkilendirme sunucusu uç noktasının URL yoludur. Bu, uygulamanın taşıyıcı belirteçlerini almak için kullandığı URL.

`Provider` özelliği, OWıN ara yazılım içine takılan ve ara yazılım tarafından oluşturulan olayları işleyen bir sağlayıcıyı belirtir.

Uygulama bir belirteç almak istediğinde temel akış aşağıda verilmiştir:

1. Uygulama, bir erişim belirteci almak için ~/Tokenöğesine bir istek gönderir.
2. OAuth ara yazılımı, sağlayıcıda `GrantResourceOwnerCredentials` çağırır.
3. Sağlayıcı, kimlik bilgilerini doğrulamak ve bir talep kimliği oluşturmak için `ApplicationUserManager` çağırır.
4. Bu başarılı olursa, sağlayıcı belirteci oluşturmak için kullanılan bir kimlik doğrulama bileti oluşturur.

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

OAuth ara yazılımı Kullanıcı hesaplarıyla ilgili herhangi bir şeyi bilmez. Sağlayıcı, ara yazılım ile ASP.NET Identity arasında iletişim kurar. Yetkilendirme sunucusunu uygulama hakkında daha fazla bilgi için bkz. [Owın OAuth 2,0 yetkilendirme sunucusu](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md).

### <a name="configuring-web-api-to-use-bearer-tokens"></a>Web API 'sini taşıyıcı belirteçleri kullanacak şekilde yapılandırma

`WebApiConfig.Register` yönteminde aşağıdaki kod, Web API işlem hattı için kimlik doğrulamasını ayarlar:

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

**Hostauthenticationfilter** sınıfı, taşıyıcı belirteçleri kullanarak kimlik doğrulamaya izin verir.

**Suppressdefaulthostauthentication** yöntemi, Web API 'sine, Istek Web API ardışık DÜZENINE, IIS veya owın ara yazılım tarafından ulaşmadan önce gerçekleşen herhangi bir kimlik doğrulamasını yok saymasını söyler. Bu şekilde, Web API 'sini yalnızca taşıyıcı belirteçleri kullanarak kimlik doğrulaması yapacak şekilde kısıtlayabiliriz.

> [!NOTE]
> Özellikle, uygulamanızın MVC bölümü, kimlik bilgilerini bir tanımlama bilgisinde depolayan Forms kimlik doğrulaması kullanabilir. Tanımlama bilgisi tabanlı kimlik doğrulaması, CSRF saldırılarını engellemek için, Anti-forgery belirteçleri kullanılmasını gerektirir. Web API 'Lerine yönelik bir sorun olduğundan, Web API 'sinin istemciye karşı koruma belirtecini gönderebilmesi için kullanışlı bir yol yoktur. (Bu sorun hakkında daha fazla bilgi için bkz. [Web API 'de CSRF saldırılarını engellemeyi](preventing-cross-site-request-forgery-csrf-attacks.md).) **Suppressdefaulthostauthentication** çağrısı, Web API 'sinin tanımlama bilgilerinde depolanan kimlik bilgilerinden CSRF saldırılarına karşı savunmasız olmamasını sağlar.

İstemci korunan bir kaynağı istediğinde, Web API ardışık düzeninde ne olur:

1. **Hostauthentication** filtresi, belirteci doğrulamak için OAuth ara yazılımını çağırır.
2. Ara yazılım, belirteci bir talep kimliğine dönüştürür.
3. Bu noktada isteğin *kimliği doğrulanır* , ancak *yetkilendirilmemiştir*.
4. Yetkilendirme filtresi, talep kimliğini inceler. Talepler bu kaynak için kullanıcıyı yetkilendirirse, istek yetkilendirilir. Varsayılan olarak, **[Yetkilendir]** özniteliği kimliği doğrulanan tüm istekleri yetkilendirmez. Bununla birlikte, role veya diğer taleplere göre yetkilendirme yapabilirsiniz. Daha fazla bilgi için bkz. [Web API 'Sinde kimlik doğrulama ve yetkilendirme](authentication-and-authorization-in-aspnet-web-api.md).
5. Önceki adımlar başarılı olursa, denetleyici korunan kaynağı döndürür. Aksi halde, istemci 401 (yetkisiz) bir hata alır.

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Identity](../../../identity/index.md)
- [VS2013 RC IÇIN Spa şablonundaki güvenlik özelliklerini anlama](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx). Hongys Sun MSDN blog gönderisi.
- [Web API 'Si bireysel hesaplar şablonunun dışına çıkarak – Bölüm 2: yerel hesaplar](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/). Dominick Baier tarafından blog gönderisi.
- [OWIN Ile ana bilgisayar kimlik doğrulaması ve Web API 'si](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/). `SuppressDefaultHostAuthentication` ve `HostAuthenticationFilter` Brock Allen hakkında iyi bir açıklama.
- [VS 2013 şablonlarında ASP.NET Identity profil bilgilerini özelleştirme](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx). Pranav Oystogi tarafından MSDN blog gönderisi.
- [ASP.NET Identity Içindeki UserManager sınıfına yönelik istek yaşam süresi yönetimine göre](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx). Suby MSDN blog gönderisi, `UserManager` sınıfının iyi bir açıklaması ile Joshi 'e sahiptir.
