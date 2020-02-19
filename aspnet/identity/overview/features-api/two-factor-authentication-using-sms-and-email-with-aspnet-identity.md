---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: ASP.NET Identity-ASP.NET 4. x ile SMS ve e-posta kullanarak iki öğeli kimlik doğrulama
author: HaoK
description: Bu öğreticide, SMS ve email kullanarak Iki öğeli kimlik doğrulamasının (2FA) nasıl ayarlanacağı gösterilmektedir. Bu makale, Rick Anderson (@RickAndMSFT), PR... tarafından yazılmıştır.
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 527b4392846e60dae0b216fdeabf21fd6618e4d7
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456744"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a>ASP.NET Identity ile SMS ve e-posta kullanarak iki öğeli kimlik doğrulama

, [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [suwith Joshi](https://github.com/suhasj)

> Bu öğreticide, SMS ve email kullanarak Iki öğeli kimlik doğrulamasının (2FA) nasıl ayarlanacağı gösterilmektedir.
> 
> Bu makale, Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung ve suwith Joshi tarafından yazılmıştır. NuGet örneği öncelikle Hao Kung tarafından yazılmıştır.

Bu konuda aşağıdakiler ele alınmaktadır:

- [Kimlik örneği oluşturma](#build)
- [Iki öğeli kimlik doğrulaması için SMS 'yi ayarlama](#SMS)
- [Iki öğeli kimlik doğrulamayı etkinleştir](#enable2)
- [Iki öğeli kimlik doğrulama sağlayıcısını kaydetme](#reg)
- [Sosyal ve yerel oturum açma hesaplarını birleştirme](#combine)
- [Deneme yanılma saldırılarına karşı hesap kilitleme](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>Kimlik örneği oluşturma

Bu bölümde, birlikte çalışacağımız bir örneği indirmek için NuGet kullanacaksınız. Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın. Visual Studio [2013 güncelleştirme 2](https://go.microsoft.com/fwlink/?LinkId=390521) veya üstünü yükler.

> [!NOTE]
> Uyarı: Bu öğreticiyi tamamlayabilmeniz için Visual Studio [2013 güncelleştirme 2](https://go.microsoft.com/fwlink/?LinkId=390521) ' nı yüklemelisiniz.

1. Yeni ***boş*** bir ASP.NET Web projesi oluşturun.
2. Paket Yöneticisi konsolunda aşağıdaki komutları girin:  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   Bu öğreticide, SMS için e-posta ve [Twilio](https://www.twilio.com/) ya da [aspsms](https://www.aspsms.com/asp.net/identity/testcredits/) 'Yi göndermek için [SendGrid](http://sendgrid.com/) kullanacağız. `Identity.Samples` paketi, ile çalışduğumuz kodu yüklüyor.
3. [PROJEYI SSL kullanacak şekilde](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)ayarlayın.
4. *Isteğe bağlı*: SendGrid 'i bağlamak ve ardından uygulamayı çalıştırmak ve bir e-posta hesabı kaydettirmek Için [e-posta onaylama öğreticimin](account-confirmation-and-password-recovery-with-aspnet-identity.md) içindeki yönergeleri izleyin.
5. *Isteğe bağlı:* Örnek e-posta bağlantısı onay kodunu (hesap denetleyicisindeki `ViewBag.Link` kodu) kaldırın. Bkz. `DisplayEmail` ve `ForgotPasswordConfirmation` eylem yöntemleri ve Razor görünümleri).
6. *Isteğe bağlı:* `ViewBag.Status` kodunu Manage ve Account denetleyicilerinden ve *Views\account\verifycode. cshtml* ve *Views\manage\doğrulamaları Yphonenumber.exe* Razor görünümlerinden kaldırın. Alternatif olarak, bu uygulamanın, e-posta ve SMS iletileri yedeklemek ve göndermek zorunda kalmadan yerel olarak nasıl çalıştığını test etmek için `ViewBag.Status` görüntüsünü koruyabilirsiniz.

> [!NOTE]
> Uyarı: Bu örnekteki güvenlik ayarlarından herhangi birini değiştirirseniz, üretimlerin uygulamanın, yapılan değişiklikleri açıkça çağıran bir güvenlik denetimine gitmesi gerekir.

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a>Iki öğeli kimlik doğrulaması için SMS 'yi ayarlama

Bu öğreticide, Twilio veya ASPSMS 'nin kullanılmasıyla ilgili yönergeler sağlanır ancak başka herhangi bir SMS sağlayıcısını kullanabilirsiniz.

1. **SMS sağlayıcısıyla Kullanıcı hesabı oluşturma**  
  
   Bir [Twilio](https://www.twilio.com/try-twilio) veya [aspsms](https://www.aspsms.com/asp.net/identity/testcredits/) hesabı oluşturun.
2. **Ek paketler yükleme veya hizmet başvuruları ekleme**  
  
   Twilio  
   Paket Yöneticisi konsolunda aşağıdaki komutu girin:  
    `Install-Package Twilio`  
  
   ASPSMS:  
   Aşağıdaki hizmet başvurusunun eklenmesi gerekir:  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   Adrestir  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   {1&gt;Ad Alanı:&lt;1}  
    `ASPSMSX2`
3. **SMS sağlayıcısı Kullanıcı kimlik bilgileri alınıyor**  
  
   Twilio  
   Twilio hesabınızın **Pano** SEKMESINDEN **Hesap SID** 'sini ve **kimlik doğrulama belirtecini**kopyalayın.  
  
   ASPSMS:  
   Hesap ayarlarınızda **userKey** ' e gidin ve kendi kendine tanımlı **parolanızla**birlikte kopyalayın.  
  
   Bu değerleri daha sonra `SMSAccountIdentification` ve `SMSAccountPassword` değişkenlerde depolayacağız.
4. **SenderId/oluşturana belirtme**  
  
   Twilio  
   **Sayılar** sekmesinden Twilio telefon numaranızı kopyalayın.  
  
   ASPSMS:  
   **Kilit açma/kaldırma** menüsünde, bir veya daha fazla kaynaktan yararlanın veya alfasayısal bir kaynağı (tüm ağlar tarafından desteklenmez) seçin.  
  
   Daha sonra bu değeri `SMSAccountFrom` değişkende depolayacağız.
5. **SMS sağlayıcısı kimlik bilgileri uygulamaya aktarılıyor**  
  
   Kimlik bilgilerini ve gönderici telefon numarasını uygulama için kullanılabilir yap:

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin. Hesap ve kimlik bilgileri, örneği basit tutmak için yukarıdaki koda eklenir. Bkz. Jon Aton 'ın [ASP.NET MVC: kaynak denetiminden özel ayarları koruyun](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).
6. **SMS sağlayıcısına veri aktarımı uygulama**  
  
   *Uygulama\_Start\ıdentityconfig.cs* dosyasını `SmsService` sınıfını yapılandırın.  
  
   Kullanılan SMS sağlayıcısına bağlı olarak **Twilio** ya da **aspsms** bölümünü etkinleştirin: 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. Uygulamayı çalıştırın ve önceden kaydolduğunuz hesapla oturum açın.
8. `Manage` denetleyicisindeki `Index` Action metodunu etkinleştiren Kullanıcı KIMLIĞINIZ ' ne tıklayın.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. Ekle'yi tıklatın.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. Birkaç saniye içinde doğrulama koduna sahip bir kısa mesaj alacaksınız. Girin ve **Gönder**' e basın.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. Yönet görünümü telefon numaranızı eklendiğini gösterir.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>Kodu inceleme

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

`Manage` denetleyicisindeki `Index` Action yöntemi, önceki eyleminizi temel alarak durum iletisini ayarlar ve yerel parolanızı değiştirme veya yerel hesap ekleme bağlantılarını sağlar. `Index` yöntemi Ayrıca bu tarayıcı için durumu veya 2FA telefon numaranızı, dış oturum açma bilgilerini, 2FA 'yı etkin ve unutmayın. Başlık çubuğundaki kullanıcı KIMLIĞINIZE (e-posta) tıkladığınızda bir ileti geçmez. **Telefon numarasına tıkladığınızda:** bağlantı geçişlerini `Message=RemovePhoneSuccess` bir sorgu dizesi olarak kaldırın.  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

`AddPhoneNumber` Action yöntemi, SMS iletilerini alabilen bir telefon numarası girmek için bir iletişim kutusu görüntüler.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

**Doğrulama kodu gönder** düğmesine tıkladığınızda telefon numarası HTTP POST `AddPhoneNumber` eylem yöntemine gönderilir.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

`GenerateChangePhoneNumberTokenAsync` yöntemi, SMS iletisinde ayarlanacak güvenlik belirtecini oluşturur. SMS hizmeti yapılandırılmışsa, belirteç dize olarak gönderilir &quot;güvenlik kodunuz &lt;Token&gt;&quot;. `SmsService.SendAsync` yöntemi zaman uyumsuz olarak çağrılır, ardından uygulama, doğrulama kodunu girebileceğiniz `VerifyPhoneNumber` eylem yöntemine (aşağıdaki iletişim kutusunu gösterir) yönlendirilir.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

Kodu girdikten ve Gönder ' e tıkladığınızda, kod HTTP POST `VerifyPhoneNumber` eylem yöntemine gönderilir.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

`ChangePhoneNumberAsync` yöntemi, postalanan güvenlik kodunu denetler. Kod doğruysa, telefon numarası `AspNetUsers` tablosunun `PhoneNumber` alanına eklenir. Bu çağrı başarılı olursa `SignInAsync` yöntemi çağrılır:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

`isPersistent` parametresi, kimlik doğrulama oturumunun birden çok istek arasında kalıcı olup olmadığını belirler.

Güvenlik profilinizi değiştirdiğinizde, *Aspnetusers* tablosunun `SecurityStamp` alanında yeni bir güvenlik damgası oluşturulur ve depolanır. `SecurityStamp` alanının güvenlik tanımlama bilgisinden farklı olduğunu aklınızda yapın. Güvenlik tanımlama bilgisi `AspNetUsers` tabloda (veya kimlik DB 'de başka herhangi bir yerde) depolanmaz. Güvenlik tanımlama bilgisi belirteci, [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) kullanılarak kendinden imzalanır ve `UserId, SecurityStamp` ile sona erme saati bilgileriyle oluşturulur.

Tanımlama bilgisi ara yazılımı her istek için tanımlama bilgisini denetler. `Startup` sınıfındaki `SecurityStampValidator` yöntemi DB 'ye rastla ve `validateInterval`belirtilen şekilde güvenlik damgasını düzenli olarak denetler. Bu, güvenlik profilinizi değiştirmediğiniz müddetçe her 30 dakikada bir gerçekleşir (örneğimizde). Veritabanı gelişlerini en aza indirmek için 30 dakikalık Aralık seçildi.

Güvenlik profilinde herhangi bir değişiklik yapıldığında `SignInAsync` yönteminin çağrılması gerekir. Güvenlik profili değiştiğinde, veritabanı `SecurityStamp` alanı güncelleştirir ve `SignInAsync` yöntemi çağrılmadan, *yalnızca* owın ardışık düzeni veritabanını (`validateInterval`) aşana kadar oturum açmış olursunuz. `SignInAsync` yöntemini hemen döndürecek şekilde değiştirerek ve tanımlama bilgisi `validateInterval` özelliğini 30 dakikadan 5 saniyeye ayarlayarak bunu test edebilirsiniz:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

Yukarıdaki kod değişiklikleriyle güvenlik profilinizi değiştirebilirsiniz (örneğin, **Iki faktörün durumunu etkin**olarak değiştirerek) ve `SecurityStampValidator.OnValidateIdentity` yöntemi başarısız olduğunda 5 saniye içinde oturumunuz açılır. `SignInAsync` yönteminde dönüş satırını kaldırın, başka bir güvenlik profili değişikliği yapın ve oturumu açmadınız. `SignInAsync` yöntemi yeni bir güvenlik tanımlama bilgisi oluşturur.

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>İki öğeli kimlik doğrulamayı etkinleştirme

Örnek uygulamada, iki öğeli kimlik doğrulamayı (2FA) etkinleştirmek için Kullanıcı arabirimini kullanmanız gerekir. 2FA 'yı etkinleştirmek için, gezinti çubuğundaki kullanıcı KIMLIĞINIZ (e-posta diğer adı) seçeneğine tıklayın.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
2FA 'yı etkinleştir ' e tıklayın.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) Oturumu kapatın ve yeniden oturum açın. E-postayı etkinleştirdiyseniz ( [önceki öğreticime](account-confirmation-and-password-recovery-with-aspnet-identity.md)bakın),/FA için SMS veya e-postayı seçebilirsiniz.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) Kodu doğrula sayfası görüntülenir (SMS veya e-posta).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) **Bu tarayıcıya** göz atma onay kutusunun tıklanması, bu bilgisayar ve tarayıcıyla oturum açmak için 2FA kullanmanıza gerek duymasını da muaf tutacaktır. 2FA 'yı etkinleştirmek ve **Bu tarayıcıya** tıklanması, bilgisayarınıza erişimi olmadığı sürece hesabınıza erişmeye çalışan kötü amaçlı kullanıcılardan güçlü bir 2FA koruması sunacaktır. Bunu, düzenli olarak kullandığınız tüm özel makineler için yapabilirsiniz. **Bu tarayıcıyı aklınızda**bulundurarak, düzenli olarak kullanmayan BILGISAYARLARDAN 2FA 'nın ek güvenliğine sahip olursunuz ve kendi bilgisayarlarınızda 2FA 'yı kullanmaya gerek kalmadan rahatlığını elde edersiniz. 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>Iki öğeli kimlik doğrulama sağlayıcısını kaydetme

Yeni bir MVC projesi oluşturduğunuzda, *IdentityConfig.cs* dosyası iki öğeli kimlik doğrulama sağlayıcısını kaydetmek için aşağıdaki kodu içerir:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>2FA için telefon numarası ekleyin

`Manage` denetleyicisindeki `AddPhoneNumber` Action yöntemi bir güvenlik belirteci oluşturur ve bunu verdiğiniz telefon numarasına gönderir.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

Belirteci gönderdikten sonra, `VerifyPhoneNumber` Action yöntemine yeniden yönlendirilir. burada, kodu 2FA için kaydetmek üzere kodu girebilirsiniz. Telefon numarasını doğrulayana kadar SMS 2FA kullanılmaz.

## <a name="enabling-2fa"></a>2FA 'yı etkinleştirme

`EnableTFA` Action yöntemi 2FA 'yı sunar:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

`SignInAsync`, 2FA 'yı etkinleştir güvenlik profilinde bir değişiklik olduğundan, bunun çağrılması gerektiğini aklınızda olun. 2FA etkinleştirildiğinde, kullanıcının kaydoldukları 2FA yaklaşımlarını (örnekteki SMS ve e-posta) kullanarak oturum açması için 2FA kullanması gerekir.

QR kod oluşturucuları gibi daha fazla 2FA sağlayıcısı ekleyebilir veya size kendinizinkini yazabilirsiniz (bkz. [ASP.NET Identity Google Authenticator kullanma](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).

> [!NOTE]
> 2FA kodları [zamana bağlı bir kerelik parola algoritması](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) kullanılarak oluşturulur ve kodlar altı dakika için geçerlidir. Kodu girmek için altı dakikadan fazla süre alırsanız geçersiz bir kod hata iletisi alırsınız.

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>Sosyal ve yerel oturum açma hesaplarını birleştirme

E-posta bağlantısına tıklayarak Yerel ve sosyal hesapları birleştirebilirsiniz. Aşağıdaki dizide &quot;RickAndMSFT@gmail.com&quot; önce yerel bir oturum açma olarak oluşturulur, ancak önce hesabı önce bir sosyal oturum günlüğü olarak oluşturabilir, sonra da yerel bir oturum açma ekleyebilirsiniz.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

**Yönet** bağlantısına tıklayın. Bu hesapla ilişkili 0 harici (sosyal oturumlar) ' a göz önüne alın.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

Başka bir oturum açma hizmetine bağlantıyı tıklatın ve uygulama isteklerini kabul edin. İki hesap birleştirildi, herhangi bir hesapla oturum açabilirsiniz. Kullanıcılarınızın, sosyal oturum açma kimlik doğrulaması hizmeti kapatılmış veya sosyal hesaplarına erişimi kaybetmiş olması olasılığına karşı yerel hesaplar eklemesini isteyebilirsiniz.

Aşağıdaki görüntüde, Tom bir sosyal oturum günlüğü (dış oturum açmalarından görebileceğiniz **: 1** gösterilen sayfada görebilirsiniz).

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

**Parola Seç** ' e tıkladığınızda, aynı hesapla ilişkili bir yerel günlük eklemenize izin verir.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>Deneme yanılma saldırılarına karşı hesap kilitleme

Kullanıcı kilitlemeyi etkinleştirerek, uygulamanızdaki hesapları sözlük saldırılarına karşı koruyabilirsiniz. `ApplicationUserManager Create` yönteminde aşağıdaki kod kilitleme yapılandırmasını yapılandırır:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

Yukarıdaki kod yalnızca iki öğeli kimlik doğrulaması için kilitlemeyi sunar. Hesap denetleyicisinin `Login` yönteminde `shouldLockout` true olarak değiştirerek oturum açma işlemleri için kilitlemeyi etkinleştirebiliriz, ancak hesabı [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) oturum açma saldırılarına açık hale getiren oturum açma işlemleri için oturumu açmamız önerilir. Örnek kodda, `ApplicationDbInitializer Seed` yönteminde oluşturulan yönetici hesabı için kilitleme devre dışıdır:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>Kullanıcının onaylanmış bir e-posta hesabına sahip olmasını gerektirme

Aşağıdaki kod, oturum açabilmeleri için bir kullanıcının doğrulanan bir e-posta hesabına sahip olmasını gerektirir:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>SignInManager 'ın 2FA gereksinimini denetlemesi

Hem yerel oturum açma hem de sosyal oturum açma, 2FA 'nın etkin olup olmadığını denetler. 2FA etkinleştirilmişse, `SignInManager` oturum açma yöntemi `SignInStatus.RequiresVerification`döndürür ve Kullanıcı, günlüğü sırayla tamamlayacak kodu girmek zorunda olabilecekleri `SendCode` eylem yöntemine yönlendirilir. Kullanıcı yerel tanımlama bilgisinde RememberMe ayarlandıysa, `SignInManager` `SignInStatus.Success` döndürür ve 2FA 'ya gitmeleri gerekmez.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

Aşağıdaki kod `SendCode` Action yöntemini gösterir. Kullanıcı için etkinleştirilen tüm 2FA yöntemleriyle bir [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) oluşturulur. [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) , kullanıcının 2FA yaklaşımını seçmesini sağlayan [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) Helper 'a geçirilir (genellikle e-posta ve SMS).

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

Kullanıcı 2FA yaklaşımını gönderdikten sonra, `HTTP POST SendCode` Action yöntemi çağrılır, `SignInManager` 2FA kodunu gönderir ve Kullanıcı oturum açma işlemini tamamlamaya yönelik kodu girebilecekleri `VerifyCode` Action yöntemine yönlendirilir.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>2FA kilitleme

Oturum açma parolası denemesi hatalarında hesap kilitlemeyi ayarlayabilseniz de bu yaklaşım, oturum açma bilgilerinizi [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) kilitlenmelerinden kaynaklanabilmesini sağlar. Hesap kilitlemeyi yalnızca 2FA ile kullanmanızı öneririz. `ApplicationUserManager` oluşturulduğunda, örnek kod 2FA kilitleme ve `MaxFailedAccessAttemptsBeforeLockout` beş olarak ayarlanır. Kullanıcı oturum açtıktan sonra (yerel hesap veya sosyal hesap aracılığıyla), 2FA 'da başarısız olan her girişim depolanır ve en fazla deneme sayısına ulaşıldığında Kullanıcı beş dakika boyunca kilitlenir (kilitleme süresini `DefaultAccountLockoutTimeSpan`) olarak ayarlayabilirsiniz.

<a id="addRes"></a>

## <a name="additional-resources"></a>Ek Kaynaklar

- [Önerilen kaynakları ASP.NET Identity](../getting-started/aspnet-identity-recommended-resources.md) Kimlik bloglarının, videoların, öğreticilerin ve harika bağlantıların tüm listesini listeleyin.
- [Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Ayrıca, profil bilgilerinin kullanıcılar tablosuna nasıl ekleneceğini gösterir.
- [ASP.NET MVC ve kimlik 2,0:](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) John Aton 'un temellerini anlama.
- [ASP.NET Identity ile hesap onaylama ve parola kurtarma](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Identity’ye Giriş](../getting-started/introduction-to-aspnet-identity.md)
- Pranav Oystogi tarafından [RTM ASP.NET Identity 2.0.0 duyurusu](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) .
- [ASP.NET Identity 2,0: John Aton tarafından hesap doğrulama ve Iki öğeli yetkilendirme ayarlama](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) .
