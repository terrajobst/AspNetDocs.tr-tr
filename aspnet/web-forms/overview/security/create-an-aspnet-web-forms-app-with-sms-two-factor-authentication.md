---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: SMS Iki faktörlü kimlik doğrulamasıyla bir ASP.NET Web Forms uygulaması oluşturma (C#) | Microsoft Docs
author: Erikre
description: Bu öğreticide, Iki öğeli kimlik doğrulama ile bir ASP.NET Web Forms uygulamasının nasıl oluşturulacağı gösterilmektedir. Bu öğretici, CR... adlı öğreticiyi tamamlamak için tasarlandı.
ms.author: riande
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c9558aca8a655071c0c94ed66433cf721f26c011
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77466425"
---
# <a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>SMS İki Öğeli Kimlik Doğrulama özellikli bir ASP.NET Web Forms uygulaması oluşturma (C#)

by [Erik Reitan](https://github.com/Erikre)

[E-posta ve SMS Iki faktörlü kimlik doğrulamasıyla ASP.NET Web Forms uygulamasını indirin](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> Bu öğreticide, Iki öğeli kimlik doğrulama ile bir ASP.NET Web Forms uygulamasının nasıl oluşturulacağı gösterilmektedir. Bu öğretici, [Kullanıcı kaydı, e-posta onayı ve parola sıfırlama ile güvenli bir ASP.NET Web Forms uygulaması oluşturma](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)başlıklı öğreticiyi tamamlamak için tasarlandı. Ayrıca, bu öğretici Rick Anderson 'ın [MVC öğreticisini](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)temel alır.

## <a name="introduction"></a>Giriş

Bu öğretici, Visual Studio kullanarak Iki öğeli kimlik doğrulamayı destekleyen bir ASP.NET Web Forms uygulaması oluşturmak için gereken adımlarda size rehberlik eder. İki öğeli kimlik doğrulama, ek bir kullanıcı kimlik doğrulama adımıdır. Bu ek adım, oturum açma sırasında benzersiz bir kişisel kimlik numarası (PIN) oluşturur. PIN, genellikle kullanıcıya bir e-posta veya SMS iletisi olarak gönderilir. Daha sonra uygulamanızın kullanıcısı, oturum açarken ek bir kimlik doğrulama ölçüsü olarak PIN 'ı girer.

### <a name="tutorial-tasks-and-information"></a>Öğretici görevleri ve bilgileri:

- [ASP.NET Web Forms uygulaması oluşturma](#createWebForms)
- [SMS ve Iki öğeli kimlik doğrulaması kurulumu](#SMS)
- [Kayıtlı Kullanıcı için Iki öğeli kimlik doğrulamayı etkinleştir](#use2FA)
- [Ek Kaynaklar](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>ASP.NET Web Forms uygulaması oluşturma

Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın. [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya üstünü de yükler. Ayrıca, aşağıda açıklandığı gibi bir [Twilio](https://www.twilio.com/try-twilio) hesabı oluşturmanız gerekir.

> [!NOTE]
> Önemli: Bu öğreticiyi tamamlayabilmeniz için [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya sonraki bir sürümü yüklemelisiniz.

1. Yeni bir proje (**dosya** -&gt; **Yeni proje**) oluşturun ve **Yeni proje** iletişim kutusundan .NET Framework sürüm 4.5.2 ile birlikte **ASP.NET Web uygulaması** şablonunu seçin.
2. **Yeni ASP.NET projesi** iletişim kutusundan **Web Forms** şablonunu seçin. Varsayılan kimlik doğrulamasını **bireysel kullanıcı hesapları**olarak bırakın. Ardından, yeni projeyi oluşturmak için **Tamam** ' ı tıklatın.  
    Yeni ASP.NET projesi iletişim kutusu ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. Proje için Güvenli Yuva Katmanı (SSL) etkinleştirin. [Web Forms öğretici serisini kullanmaya](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)başlama konusunun **Proje Için SSL 'yi etkinleştirme** bölümünde bulunan adımları izleyin.
4. Visual Studio 'da **Paket Yöneticisi konsolu 'nu** açın (**Araçlar** -&gt; **NuGet paket** Yöneticisi -&gt; **Paket Yöneticisi konsolu**) ve aşağıdaki komutu girin:  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>SMS ve Iki öğeli kimlik doğrulaması kurulumu

Bu öğretici Twilio kullanır, ancak herhangi bir SMS sağlayıcısını kullanabilirsiniz.

1. Bir [Twilio](https://www.twilio.com/try-twilio) hesabı oluşturun.
2. Twilio hesabınızın **Pano** SEKMESINDEN **Hesap SID** 'Sini ve **kimlik doğrulama belirtecini kopyalayın.** Bunları uygulamanıza daha sonra ekleyebilirsiniz.
3. **Sayılar** sekmesinden Twilio **telefon numaranızı** da kopyalayın.
4. Twilio **HESABı SID**, **kimlik doğrulama belirteci** ve **telefon numarasını** uygulama için kullanılabilir hale getirin. Şeyleri basit tutmak için bu değerleri *Web. config* dosyasında depolayacaksınız. Azure 'a dağıtırken, verileri Web sitesi Yapılandır sekmesindeki **appSettings** bölümünde güvenli bir şekilde depolayabilirsiniz. Ayrıca, telefon numarası eklenirken yalnızca sayılar kullanılır.   
   Ayrıca, SendGrid kimlik bilgileri de ekleyebildiğinize dikkat edin. SendGrid bir e-posta bildirim hizmetidir. SendGrid 'in nasıl etkinleştirileceği hakkındaki ayrıntılar için, [Kullanıcı kaydıyla güvenli bir ASP.NET Web Forms uygulaması oluşturma, e-posta onayı ve parola sıfırlama](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md) başlıklı öğreticinin ' SendGrid 'i bağlama ' bölümüne bakın.

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin. Bu örnekte, hesap ve kimlik bilgileri *Web. config* dosyasının **appSettings** bölümünde depolanır. Azure 'da, bu değerleri Azure portal **[Yapılandır](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** sekmesinde güvenli bir şekilde depolayabilirsiniz. İlgili bilgiler için bkz. Rick Anderson 'ın, [parolaları ve diğer hassas verileri ASP.net ve Azure 'a dağıtmaya yönelik en iyi yöntemler](/aspnet/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)başlıklı konu.
5. Aşağıdaki değişiklikleri sarı olarak vurgulayarak, *Start\ıdentityconfig.cs dosyasındaki uygulama\_* `SmsService` sınıfını yapılandırın: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. Aşağıdaki `using` deyimlerini *IdentityConfig.cs* dosyasının başlangıcına ekleyin: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. Sarı renkle vurgulanmış satırları kaldırarak *Hesap/Manage. aspx* dosyasını güncelleştirin:  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. *Manage.aspx.cs* arka plan kodunun `Page_Load` işleyicisinde, aşağıdaki gibi görünmesi için sarı renkle vurgulanmış kod satırının açıklamasını kaldırın: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. *Hesap* codebehind/*TwoFactorAuthenticationSignIn.aspx.cs*, aşağıdaki kodu sarı renkle ekleyerek `Page_Load` işleyicisini güncelleştirin: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   Yukarıdaki kod değişikliğini yaparak, kimlik doğrulama seçeneklerini içeren "sağlayıcılar" DropDownList değeri ilk değere sıfırlanmaz. Bu, kullanıcının kimlik doğrulaması sırasında kullanmak üzere tüm seçenekleri başarılı bir şekilde seçmesine izin verir, yalnızca ilk değil.
10. **Çözüm Gezgini**, *default. aspx* öğesine sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.
11. Uygulamanızı test ederek, önce uygulamayı derleyin (**Ctrl**+**SHIFT**+**B**) ve ardından uygulamayı çalıştırın (**F5**) ve **Kaydet** ' i seçerek yeni bir kullanıcı hesabı oluşturun veya Kullanıcı hesabı zaten kaydedilmişse **oturum aç '** ı seçin.
12. Siz (Kullanıcı olarak) oturum açmış olduktan sonra, **Hesabı Yönet** sayfasını (manage. aspx) göstermek için gezinti ÇUBUĞUNDAKI kullanıcı kimliğine (e-posta adresi) tıklayın.  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. **Hesabı Yönet** sayfasında **telefon numarası** ' nın yanına **Ekle** ' ye tıklayın.  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. Kullandığınız telefon numarasını (Kullanıcı olarak) SMS mesajları almak istediğiniz (metin iletileri) ekleyin ve **Gönder** düğmesine tıklayın.   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    Bu noktada, uygulama Twilio ile iletişim kurmak için *Web. config* dosyasından kimlik bilgilerini kullanır. Kullanıcı hesabıyla ilişkili telefona bir SMS mesajı (kısa mesaj) gönderilecek. Twilio panosunu görüntüleyerek Twilio iletisinin gönderildiğini doğrulayabilirsiniz.
15. Birkaç saniye içinde, kullanıcı hesabıyla ilişkilendirilmiş telefon doğrulama kodunu içeren bir kısa mesaj alır. Doğrulama kodunu girin ve **Gönder**' e basın.  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>Kayıtlı Kullanıcı için Iki öğeli kimlik doğrulamayı etkinleştirme

Bu noktada, uygulamanız için iki öğeli kimlik doğrulamayı etkinleştirdiniz. Bir kullanıcının iki öğeli kimlik doğrulaması kullanabilmesi için, Kullanıcı ARABIRIMINI kullanarak ayarlarını değiştirebilir. 

1. Uygulamanızın bir kullanıcısı olarak, **Hesabı Yönet** sayfasını göstermek için gezinti ÇUBUĞUNDAKI Kullanıcı kimliği (e-posta diğer adı) öğesine tıklayarak, belirli hesabınız için iki öğeli kimlik doğrulamayı etkinleştirebilirsiniz. Ardından, hesap için iki öğeli kimlik doğrulamayı etkinleştirmek üzere bağlantıyı **Etkinleştir** bağlantısına tıklayın.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. Oturumu kapatın ve yeniden oturum açın. E-postayı etkinleştirdiyseniz, iki öğeli kimlik doğrulama için SMS veya e-posta seçeneğini belirleyebilirsiniz. E-postayı etkinleştirmediyseniz [Kullanıcı kaydıyla güvenli bir ASP.NET Web Forms uygulaması oluşturma, e-posta onayı ve parola sıfırlama](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)başlıklı öğreticiye bakın.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. Kodu girebileceğiniz Iki öğeli kimlik doğrulama sayfası görüntülenir (SMS veya e-posta üzerinden).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 **Bu tarayıcıya** göz atma onay kutusu tıklandığında, kutuyu seçtiğiniz tarayıcıyı ve cihazı kullanırken oturum açmak için iki öğeli kimlik doğrulaması kullanmanıza gerek kalmanız gerekir. Kötü amaçlı kullanıcılar cihazınıza erişim kazanabileceği sürece, iki öğeli kimlik doğrulamayı etkinleştirmek ve **Bu tarayıcıyı anımsa** ' ya tıklamak, güvenilir olmayan cihazlardan tüm erişimler için güçlü iki öğeli kimlik doğrulama korumasını sürdürirken size kullanışlı bir adım parola erişimi sağlar. Düzenli olarak kullandığınız özel cihaz üzerinde bunu yapabilirsiniz.

<a id="addRes"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Identity ile SMS ve e-posta kullanılan iki öğeli kimlik doğrulaması](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [Önerilen kaynakların ASP.NET Identity bağlantıları](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [Üyelik, OAuth ve SQL veritabanı ile bir Azure Web sitesine güvenli bir ASP.NET Web Forms uygulaması dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms öğretici serisi-OAuth 2,0 sağlayıcısı ekleme](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [ASP.NET Web Forms öğretici serisi-proje için SSL 'yi etkinleştir](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [ASP.NET Identity ile hesap onaylama ve parola kurtarma](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Facebook 'ta uygulama oluşturma ve uygulamayı projeye bağlama](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
