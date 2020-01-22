---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: Hesap onaylama & parola kurtarma-ASP.NET Identity (C#)-ASP.NET 4. x
author: HaoK
description: Bu öğreticiyi gerçekleştirmeden önce, oturum açma, e-posta onayı ve parola sıfırlama ile güvenli bir ASP.NET MVC 5 Web uygulaması oluşturma işlemi gerçekleştirmeniz gerekir. Bu öğretici...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 4b2c88280df39aa81d60f9508910e8fe5d6db6b8
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519121"
---
# <a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>ASP.NET Identity (C#) ile hesap onaylama ve parola kurtarma

> Bu öğreticiyi gerçekleştirmeden önce [, oturum açma, e-posta onayı ve parola sıfırlama ile güvenli bir ASP.NET MVC 5 Web uygulaması oluşturma](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)işlemi gerçekleştirmeniz gerekir. Bu öğretici daha fazla ayrıntı içerir ve yerel hesap onayı için e-posta ayarlamayı ve kullanıcıların ASP.NET Identity unutulan parolalarını sıfırlamasına izin vermeyi gösterir.

Yerel bir kullanıcı hesabı, kullanıcının hesap için bir parola oluşturmasını ve bu parolanın Web uygulamasında depolanmasını (güvenli şekilde) gerektirir. ASP.NET Identity Ayrıca, kullanıcının uygulama için parola oluşturmasını gerektirmeyen sosyal hesapları da destekler. [Sosyal hesaplar](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) , kullanıcıların kimliğini doğrulamak için üçüncü taraf (örneğin, Google, Twitter, Facebook veya Microsoft) kullanır. Bu konuda aşağıdakiler ele alınmaktadır:

- [Bir ASP.NET MVC uygulaması oluşturun](#createMvc) ve ASP.NET Identity özellikleri gezin.
- [Kimlik örneğini oluşturma](#build)
- [E-posta onayını ayarlama](#email)

Yeni kullanıcılar, bir yerel hesap oluşturan e-posta diğer adlarını kaydeder.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

Kaydet düğmesinin seçilmesi, e-posta adreslerine doğrulama belirteci içeren bir onay e-postası gönderir.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

Kullanıcıya, hesabı için bir onay belirteci içeren bir e-posta gönderilir.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

Bağlantıyı seçtiğinizde hesap onaylanır.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>Parola kurtarma/sıfırlama

Parolasını unulayan yerel kullanıcıların, e-posta hesaplarına gönderilen bir güvenlik belirteci olabilir ve bunların parolalarını sıfırlamalarını sağlar.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
Kullanıcı yakında parolasını sıfırlamasına izin veren bir bağlantı içeren bir e-posta alır.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
Bağlantıyı seçtiğinizde sıfırlama sayfasına gidecektir.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
**Sıfırla** düğmesinin seçilmesi parolanın sıfırlandığını onaylanır.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>ASP.NET web uygulaması oluşturma

[Visual Studio 2017](https://visualstudio.microsoft.com/)' i yükleyip çalıştırarak başlayın.

1. Yeni bir ASP.NET Web projesi oluşturun ve MVC şablonunu seçin. Web Forms ASP.NET Identity da destekler, böylece bir Web Forms uygulamasında benzer adımları izleyebilirsiniz.
2. Kimlik doğrulamasını **bireysel kullanıcı hesaplarıyla**değiştirin.
3. Uygulamayı çalıştırın, **Kaydet** bağlantısını seçin ve bir Kullanıcı kaydedin. Bu noktada, e-postadaki tek doğrulama [[Emapostaadresi]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) özniteliğiyle aynıdır.
4. Sunucu Gezgini ' de **veri bağlantısı \ Defaultconnection\tables\aspnetusers**' a gidin, sağ tıklayın ve **tablo tanımını aç**' ı seçin.

    Aşağıdaki görüntüde `AspNetUsers` şeması gösterilmektedir:

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. **Aspnetusers** tablosuna sağ tıklayın ve **tablo verilerini göster**' i seçin.  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   Bu noktada e-posta onaylanmamıştır.

ASP.NET Identity için varsayılan veri deposu Entity Framework, ancak başka veri depoları kullanmak ve ek alanlar eklemek için yapılandırabilirsiniz. Bu öğreticinin sonundaki [ek kaynaklar](#addRes) bölümüne bakın.

[Owın başlangıç sınıfı](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) ( *Startup.cs* ), uygulama başlatıldığında çağrılır ve *App\_Start\Startup.auth.cs*' de, owın ardışık düzenini yapılandıran ve ASP.NET Identity Başlatan `ConfigureAuth` yöntemini çağırır. İnceleme `ConfigureAuth` yöntemi. Her `CreatePerOwinContext` çağrısı, belirtilen türden bir örnek oluşturmak için her istek için bir kez çağrılacak bir geri çağırma (`OwinContext`kaydedilir) kaydeder. Her türde (`ApplicationDbContext, ApplicationUserManager`) oluşturucuda ve `Create` yönteminde bir kesme noktası ayarlayabilir ve bunların her istekte çağrıldığından emin olabilirsiniz. `ApplicationDbContext` ve `ApplicationUserManager` bir örneği, uygulama genelinde erişilebilen OWIN bağlamında saklanır. Tanımlama bilgisi ara yazılımı aracılığıyla OWıN ardışık düzeninde kancalar ASP.NET Identity. Daha fazla bilgi için, bkz. [ASP.NET Identity Içindeki UserManager için istek ömrü yönetimi](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx).

Güvenlik profilinizi değiştirdiğinizde, *Aspnetusers* tablosunun `SecurityStamp` alanında yeni bir güvenlik damgası oluşturulur ve depolanır. `SecurityStamp` alanının güvenlik tanımlama bilgisinden farklı olduğunu aklınızda yapın. Güvenlik tanımlama bilgisi `AspNetUsers` tabloda (veya kimlik DB 'de başka herhangi bir yerde) depolanmaz. Güvenlik tanımlama bilgisi belirteci, [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) kullanılarak kendinden imzalanır ve `UserId, SecurityStamp` ile sona erme saati bilgileriyle oluşturulur.

Tanımlama bilgisi ara yazılımı her istek için tanımlama bilgisini denetler. `Startup` sınıfındaki `SecurityStampValidator` yöntemi DB 'ye rastla ve `validateInterval`belirtilen şekilde güvenlik damgasını düzenli olarak denetler. Bu, güvenlik profilinizi değiştirmediğiniz müddetçe her 30 dakikada bir gerçekleşir (örneğimizde). Veritabanı gelişlerini en aza indirmek için 30 dakikalık Aralık seçildi. Daha fazla ayrıntı için bkz. [iki öğeli kimlik doğrulama öğreticisi](index.md) .

Koddaki açıklamalara göre `UseCookieAuthentication` yöntemi, tanımlama bilgisi kimlik doğrulamasını destekler. `SecurityStamp` alanı ve ilişkili kod, uygulamanıza ek bir güvenlik katmanı sağlar, parolanızı değiştirdiğinizde, oturum açtığınız tarayıcıdan oturumunuz açılır. `SecurityStampValidator.OnValidateIdentity` yöntemi, bir parolayı değiştirirken veya dış oturum açma kullandığınızda kullanılan Kullanıcı oturum açtığında uygulamanın güvenlik belirtecini doğrulamasını sağlar. Bu, eski parolayla oluşturulan belirteçlerin (tanımlama bilgilerinin) geçersiz kılındığından emin olmak için gereklidir. Örnek projede, kullanıcılar parolasını değiştirirseniz, Kullanıcı için yeni bir belirteç oluşturulursa, önceki belirteçler geçersiz kılınır ve `SecurityStamp` alanı güncellenir.

Kimlik sistemi, kullanıcıların güvenlik profili değiştiğinde uygulamanızı yapılandırmanıza izin verir (örneğin, Kullanıcı parolasını değiştirdiğinde veya ilişkili oturum açma değişikliklerini (Facebook, Google, Microsoft hesabı vb. gibi), Kullanıcı tüm oturumunuzu açtı tarayıcı örnekleri. Örneğin, aşağıdaki görüntüde tek bir düğme seçerek kullanıcının tüm tarayıcı örneklerinin (Bu durumda, IE, Firefox ve Chrome) oturumunu açmasını sağlayan [tek bir SignOut örnek](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) uygulaması gösterilmektedir. Alternatif olarak, örnek yalnızca belirli bir tarayıcı örneğinin oturumunu kapatmanıza izin verir.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

[Tek SignOut örnek](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) uygulaması, ASP.NET Identity güvenlik belirtecini yeniden oluşturmanız için nasıl izin verdiğini gösterir. Bu, eski parolayla oluşturulan belirteçlerin (tanımlama bilgilerinin) geçersiz kılındığından emin olmak için gereklidir. Bu özellik, uygulamanız için ek bir güvenlik katmanı sağlar; parolanızı değiştirdiğinizde, bu uygulamada oturum açmış olduğunuz yerde oturumunuz açılır.

*Start\ıdentityconfig.cs dosyası\_uygulaması* `ApplicationUserManager`, `EmailService` ve `SmsService` sınıflarını içerir. `EmailService` ve `SmsService` sınıfları `IIdentityMessageService` arabirimini uygular, bu nedenle e-posta ve SMS 'yi yapılandırmak için her sınıfta ortak yöntemlere sahip olursunuz. Bu öğretici yalnızca [SendGrid](http://sendgrid.com/)aracılığıyla e-posta bildirimi Eklemeyi gösterir, ancak SMTP ve diğer mekanizmaları kullanarak e-posta gönderebilirsiniz.

`Startup` sınıfı ayrıca sosyal oturumlar (Facebook, Twitter vb.) eklemek için Boiler levhası içerir. daha fazla bilgi için bkz. [Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma ile ilgili öğretici MVC 5 uygulaması](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) .

Kullanıcı kimlik bilgilerini içeren `ApplicationUserManager` sınıfını inceleyin ve aşağıdaki özellikleri yapılandırır:

- Parola gücü gereksinimleri.
- Kullanıcı kilidi (denemeler ve zaman).
- İki öğeli kimlik doğrulaması (2FA). Başka bir öğreticide 2FA ve SMS 'yi kapsayacağız.
- E-posta ve SMS hizmetlerini birleştirme. (SMS 'yi başka bir öğreticide ele alacağız).

`ApplicationUserManager` sınıfı, genel `UserManager<ApplicationUser>` sınıfından türetilir. `ApplicationUser` [ıdentityuser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx)'tan türetilir. `IdentityUser` genel `IdentityUser` sınıfından türetiliyor:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

Yukarıdaki özellikler, yukarıda gösterilen `AspNetUsers` tablosundaki özelliklerle kesişmelidir.

`IUser` genel bağımsız değişkenleri, birincil anahtar için farklı türler kullanarak bir sınıfı türetmeye olanak tanır. Dizeden int veya GUID olarak birincil anahtarın nasıl değiştirileceğini gösteren [Changepk](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) örneğine bakın.

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser` (`public class ApplicationUserManager : UserManager<ApplicationUser>`), *Models\ıdentitymodels.cs* 'de şöyle tanımlanmıştır:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

Yukarıdaki vurgulanan kod bir [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)oluşturur. ASP.NET Identity ve OWıN tanımlama bilgisi kimlik doğrulaması talep tabanlıdır, bu nedenle Framework uygulamanın kullanıcı için bir `ClaimsIdentity` oluşturmasını gerektirir. `ClaimsIdentity` kullanıcının adı, yaşı ve kullanıcının ait olduğu roller gibi tüm taleplerle ilgili bilgiler içerir. Ayrıca bu aşamada Kullanıcı için daha fazla talep ekleyebilirsiniz.

OWIN `AuthenticationManager.SignIn` yöntemi `ClaimsIdentity` geçer ve kullanıcının işaretini yapar:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) , `ApplicationUser` sınıfına nasıl ek özellikler ekleyebileceğiniz gösterilmektedir.

## <a name="email-confirmation"></a>E-posta onayı

Yeni bir kullanıcının, başka birinin kimliğine bürünmediğinden emin olmak için (diğer bir deyişle, başka birinin e-postasına kaydolmadığını) doğrulamak iyi bir fikirdir. Bir tartışma forumu olduğunu varsayalım, `"bob@example.com"` `"joe@contoso.com"`olarak kaydolmasını engellemek isteyebilirsiniz. E-posta onayı olmadan `"joe@contoso.com"`, uygulamanızdan istenmeyen e-posta alabilir. Emre 'nin yanlışlıkla `"bib@example.com"` olarak kaydolduğunu ve olduğunu fark etmemiş olduğunu varsayalım, uygulamanın doğru e-postası olmadığından parola kurtarma kullanamayacak. E-posta onayı yalnızca botlardan sınırlı koruma sağlar ve belirlenen istenmeyen posta gönderenlerin korumasını sağlamaz, kaydolmak için kullanabilecekleri birçok çalışma e-posta diğer adı vardır. Aşağıdaki örnekte, Kullanıcı, hesabı onaylanana kadar parolasını değiştiremez (ile kaydoldukları e-posta hesabındaki bir onay bağlantısını seçerek). Bu iş akışını diğer senaryolara uygulayabilirsiniz. Örneğin, yönetici tarafından oluşturulan yeni hesaplara parolayı onaylamak ve sıfırlamak için bir bağlantı göndermek, kullanıcı profilini değiştirdiklerinde e-posta göndermek ve daha fazlasını yapmak için bir bağlantı göndermek. Genellikle yeni kullanıcıların e-posta, SMS mesajı veya başka bir mekanizma tarafından onaylanmadan önce Web sitenize veri göndermeleri önlemektir. <a id="build"></a>

## <a name="build-a-more-complete-sample"></a>Daha kapsamlı bir örnek oluşturun

Bu bölümde, birlikte çalışacağımız daha kapsamlı bir örnek indirmek için NuGet kullanacaksınız.

1. Yeni ***boş*** bir ASP.NET Web projesi oluşturun.
2. Paket Yöneticisi konsolunda aşağıdaki komutları girin: 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   Bu öğreticide, e-posta göndermek için [SendGrid](http://sendgrid.com/) kullanacağız. `Identity.Samples` paketi, ile çalışduğumuz kodu yüklüyor.
3. [PROJEYI SSL kullanacak şekilde](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)ayarlayın.
4. Uygulamayı çalıştırarak, **kayıt bağlantısını seçerek ve kayıt formu** naklederek yerel hesap oluşturmayı test edin.
5. E-posta onayını taklit eden tanıtım e-posta bağlantısını seçin.
6. Örnek e-posta bağlantısı onay kodunu (hesap denetleyicisindeki `ViewBag.Link` kodu) kaldırın. Bkz. `DisplayEmail` ve `ForgotPasswordConfirmation` eylem yöntemleri ve Razor görünümleri).

> [!WARNING]
> Bu örnekteki güvenlik ayarlarından herhangi birini değiştirirseniz, üretimlerin uygulamanın, yapılan değişiklikleri açıkça çağıran bir güvenlik denetimine gitmesi gerekir.

## <a name="examine-the-code-in-app_startidentityconfigcs"></a>\_Start\ıdentityconfig.cs uygulamasındaki kodu inceleyin

Örnek, bir hesabın nasıl oluşturulduğunu ve *yönetici* rolüne nasıl ekleneceğini gösterir. Örnekteki e-postayı, yönetici hesabı için kullandığınız e-postayla değiştirmelisiniz. Hemen bir yönetici hesabı oluşturmanın en kolay yolu `Seed` yönteminde programlı olarak kullanılır. Gelecekte kullanıcılar ve roller oluşturmanıza ve yönetmenize imkan tanıyan bir araç da sunacağız. Örnek kod, kullanıcılar ve roller oluşturmanıza ve yönetmenize izin verir, ancak önce rolleri ve kullanıcı yönetici sayfalarını çalıştırmak için bir Yönetici hesabınızın olması gerekir. Bu örnekte, VERITABANı çalıştırıldığında yönetici hesabı oluşturulur.

Parolayı değiştirin ve adı e-posta bildirimleri alabileceğiniz bir hesapla değiştirin.

> [!WARNING]
> Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin.

Daha önce belirtildiği gibi, başlangıç sınıfındaki `app.CreatePerOwinContext` çağrısı, uygulama DB içeriğinin, Kullanıcı yöneticisinin ve rol yöneticisi sınıflarının `Create` yöntemine geri çağrılar ekler. OWIN işlem hattı her bir istek için bu sınıflarda `Create` yöntemini çağırır ve her bir sınıfın bağlamını depolar. Hesap denetleyicisi, Kullanıcı yöneticisini HTTP bağlamından (OWıN bağlamını içerir) kullanıma sunar:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

Bir kullanıcı yerel bir hesabı kaydettiğinde `HTTP Post Register` yöntemi çağrılır:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

Yukarıdaki kod, girilen e-posta ve parolayı kullanarak yeni bir kullanıcı hesabı oluşturmak için model verilerini kullanır. E-posta diğer adı veri deposunda ise, hesap oluşturma başarısız olur ve form yeniden görüntülenir. `GenerateEmailConfirmationTokenAsync` yöntemi bir güvenli onay belirteci oluşturur ve ASP.NET Identity veri deposunda depolar. [URL. Action](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx) yöntemi, `UserId` ve onay belirtecini içeren bir bağlantı oluşturur. Bu bağlantı daha sonra kullanıcıya e-posta ile Kullanıcı hesabını onaylamak için e-posta uygulamasındaki bağlantıda seçim yapabilir.

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>E-posta onayını ayarlama

[Azure SendGrid kaydolma sayfasına](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) gidin ve ücretsiz hesap için kaydolun. SendGrid 'i yapılandırmak için aşağıdakine benzer bir kod ekleyin:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> E-posta istemcileri genellikle yalnızca metin iletilerini kabul eder (HTML yok). İletiyi metin ve HTML olarak sağlamalısınız. Yukarıdaki SendGrid örneğinde, bu, yukarıda gösterilen `myMessage.Text` ve `myMessage.Html` koduyla yapılır.

Aşağıdaki kod, `message.Body` yalnızca bağlantıyı döndürdüğü [MailMessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) sınıfını kullanarak e-postanın nasıl gönderileceğini gösterir.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin. Hesap ve kimlik bilgileri appSetting 'de depolanır. Azure 'da, bu değerleri Azure portal **[Yapılandır](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** sekmesinde güvenli bir şekilde depolayabilirsiniz. [ASP.net ve Azure 'a parola ve diğer hassas verileri dağıtmaya yönelik en iyi uygulamalar](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)bölümüne bakın.

SendGrid kimlik bilgilerinizi girin, uygulamayı çalıştırın, bir e-posta diğer adı ile kaydolun e-postalarınızın onaylama bağlantısını seçebilir. Bunu [Outlook.com](http://outlook.com) e-posta hesabınızla nasıl yapılacağını görmek için bkz. John Aton 'ın [ C# Outlook.com SMTP ana bilgisayarı için SMTP yapılandırması](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx) ve[ASP.NET Identity 2,0: hesap doğrulaması ve iki öğeli yetkilendirme](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) gönderilerini ayarlama.

Kullanıcı **Kaydet** düğmesini seçtiğinde, e-posta adreslerine doğrulama belirteci içeren bir onay e-postası gönderilir.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

Kullanıcıya, hesabı için bir onay belirteci içeren bir e-posta gönderilir.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>Kodu inceleme

Aşağıdaki kodda `POST ForgotPassword` metodu gösterilmektedir.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

Kullanıcı e-postası onaylanmazsa Yöntem sessizce başarısız olur. Geçersiz bir e-posta adresi için bir hata nakledilmişse, kötü amaçlı kullanıcılar bu bilgileri kullanarak saldırılara yönelik geçerli kullanıcı kimliği (e-posta diğer adları) bulabilir.

Aşağıdaki kod, Kullanıcı tarafından gönderilen e-postadaki onay bağlantısını seçtiğinde çağrılan hesap denetleyicisindeki `ConfirmEmail` yöntemini gösterir:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

Unutulan parola belirteci kullanıldığında, geçersiz kılınır. `Create` yönteminde aşağıdaki kod değişikliği ( *uygulamada\_Start\ıdentityconfig.cs* ) belirteçleri 3 saat içinde dolacak şekilde ayarlar.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

Yukarıdaki kodla, Unutulan parolanın ve e-posta onayı belirteçlerinin süresi 3 saat içinde dolacak. Varsayılan `TokenLifespan` bir gündür.

Aşağıdaki kod, e-posta onay yöntemini gösterir:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 Uygulamanızı daha güvenli hale getirmek için ASP.NET Identity Iki öğeli kimlik doğrulamayı (2FA) destekler. Bkz. ASP.NET Identity 2,0: John Aton tarafından [hesap doğrulaması ve Iki öğeli yetkilendirme ayarlama](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) . Oturum açma parolası denemesi hatalarında hesap kilitlemeyi ayarlayabilseniz de bu yaklaşım, oturum açma bilgilerinizi [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) kilitlenmelerinden kaynaklanabilmesini sağlar. Hesap kilitlemeyi yalnızca 2FA ile kullanmanızı öneririz.  
<a id="addRes"></a>

## <a name="additional-resources"></a>Ek kaynaklar

- [ASP.NET Identity için Özel Depolama Sağlayıcılarına Genel Bakış](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Ayrıca, profil bilgilerinin kullanıcılar tablosuna nasıl ekleneceğini gösterir.
- [ASP.NET MVC ve kimlik 2,0:](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) John Aton 'un temellerini anlama.
- [ASP.NET Identity’ye Giriş](../getting-started/introduction-to-aspnet-identity.md)
- Pranav Oystogi tarafından [RTM ASP.NET Identity 2.0.0 duyurusu](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) .
