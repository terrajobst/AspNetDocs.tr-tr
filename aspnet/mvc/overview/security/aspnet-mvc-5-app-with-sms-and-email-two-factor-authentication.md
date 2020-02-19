---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: SMS ve e-posta Iki öğeli kimlik doğrulaması ile ASP.NET MVC 5 uygulaması | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, Iki öğeli kimlik doğrulama ile bir ASP.NET MVC 5 Web uygulaması oluşturma gösterilmektedir. Güvenli bir ASP.NET MVC 5 Web uygulaması oluşturmayı ile tamamlamalısınız...
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457602"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>SMS ve e-posta iki öğeli kimlik doğrulaması özellikli ASP.NET MVC 5 uygulaması

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticide, Iki öğeli kimlik doğrulama ile bir ASP.NET MVC 5 Web uygulaması oluşturma gösterilmektedir. Devam etmeden önce [, oturum açma, e-posta onayı ve parola sıfırlama ile güvenli bir ASP.NET MVC 5 Web uygulaması oluşturma](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) işleminin tamamlanmış olması gerekir. Tamamlanmış uygulamayı [buradan](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)indirebilirsiniz. Bu indirme, e-posta veya SMS sağlayıcısı ayarlamadan e-posta onayını ve SMS 'yi test etmenize olanak sağlayan hata ayıklama yardımcıları içerir.
> 
> Bu öğretici [Rick Anderson](https://blogs.msdn.com/rickAndy) tarafından yazılmıştır (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).

- [ASP.NET MVC uygulaması oluşturma](#createMvc)
- [Iki öğeli kimlik doğrulaması için SMS 'yi ayarlama](#SMS)
- [Iki öğeli kimlik doğrulamayı etkinleştir](#enable2)
- [Ek Kaynaklar](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC uygulaması oluşturma

Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın. [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya üstünü yükler.

> [!NOTE]
> Uyarı: devam etmeden önce [oturum açma, e-posta onayı ve parola sıfırlama ile güvenli bir ASP.NET MVC 5 Web uygulaması oluşturma](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) işleminin tamamlanmış olması gerekir. Bu öğreticiyi tamamlayabilmeniz için [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya sonraki bir sürümü yüklemelisiniz.

1. Yeni bir ASP.NET Web projesi oluşturun ve MVC şablonunu seçin. Web Forms Ayrıca ASP.NET Identity destekler, böylece bir Web Forms uygulamasındaki benzer adımları izleyebilirsiniz.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. Varsayılan kimlik doğrulamasını **bireysel kullanıcı hesapları**olarak bırakın. Uygulamayı Azure 'da barındırmak isterseniz onay kutusunu işaretli bırakın. Öğreticide daha sonra Azure 'a dağıtacağız. [Bir Azure hesabını ücretsiz olarak açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
3. [PROJEYI SSL kullanacak şekilde](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)ayarlayın.

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
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   Adrestir  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   {1&gt;Ad Alanı:&lt;1}  
    `ASPSMSX2`
3. **SMS sağlayıcısı Kullanıcı kimlik bilgileri alınıyor**  
  
   Twilio  
   Twilio hesabınızın **Pano** SEKMESINDEN **Hesap SID** 'sini ve **kimlik doğrulama belirtecini**kopyalayın.  
  
   ASPSMS:  
   Hesap ayarlarınızda **userKey** ' e gidin ve kendi kendine tanımlı **parolanızla**birlikte kopyalayın.  
  
   Daha sonra bu değerleri anahtarlar içindeki *Web. config* dosyasında depolayacağız `"SMSAccountIdentification"` ve `"SMSAccountPassword"`.
4. **SenderId/oluşturana belirtme**  
  
   Twilio  
   **Sayılar** sekmesinden Twilio telefon numaranızı kopyalayın.  
  
   ASPSMS:  
   **Kilit açma/kaldırma** menüsünde, bir veya daha fazla kaynaktan yararlanın veya alfasayısal bir kaynağı (tüm ağlar tarafından desteklenmez) seçin.  
  
   Daha sonra bu değeri, anahtar `"SMSAccountFrom"` içindeki *Web. config* dosyasında depolayacağız.
5. **SMS sağlayıcısı kimlik bilgileri uygulamaya aktarılıyor**  
  
   Kimlik bilgilerini ve gönderici telefon numarasını uygulama için kullanılabilir hale getirin. Şeyleri basit tutmak için bu değerleri *Web. config* dosyasında depolayacağız. Azure 'a dağıtırken, verileri Web sitesi Yapılandır sekmesindeki **uygulama ayarları** bölümünde güvenli bir şekilde depolayabiliriz. 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin. Hesap ve kimlik bilgileri, örneği basit tutmak için yukarıdaki koda eklenir. [ASP.net ve Azure 'a parola ve diğer hassas verileri dağıtmaya yönelik en iyi uygulamalar](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)bölümüne bakın.
6. **SMS sağlayıcısına veri aktarımı uygulama**  
  
   *Uygulama\_Start\ıdentityconfig.cs* dosyasını `SmsService` sınıfını yapılandırın.  
  
   Kullanılan SMS sağlayıcısına bağlı olarak **Twilio** ya da **aspsms** bölümünü etkinleştirin: 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. *Views\manage\ındex.cshtml* Razor görünümünü güncelleştirin: (Note: çıkış kodundaki açıklamaları kaldırın, aşağıdaki kodu kullanın.)  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. `ManageController` içindeki `EnableTwoFactorAuthentication` ve `DisableTwoFactorAuthentication` eylemi yöntemlerinin[[Validateantiforgerytoken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) özniteliğine sahip olduğunu doğrulayın:  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. Uygulamayı çalıştırın ve önceden kaydolduğunuz hesapla oturum açın.
10. `Manage` denetleyicisindeki `Index` Action metodunu etkinleştiren Kullanıcı KIMLIĞINIZ ' ne tıklayın.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. Ekle'yi tıklatın.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. `AddPhoneNumber` Action yöntemi, SMS iletilerini alabilen bir telefon numarası girmek için bir iletişim kutusu görüntüler.

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. Birkaç saniye içinde doğrulama koduna sahip bir kısa mesaj alacaksınız. Girin ve **Gönder**' e basın.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. Yönet görünümü telefon numaranızı eklendiğini gösterir.

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>İki öğeli kimlik doğrulamayı etkinleştirme

Şablon tarafından oluşturulan uygulamada, iki öğeli kimlik doğrulamayı (2FA) etkinleştirmek için Kullanıcı arabirimini kullanmanız gerekir. 2FA 'yı etkinleştirmek için, gezinti çubuğundaki kullanıcı KIMLIĞINIZ (e-posta diğer adı) seçeneğine tıklayın.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

2FA 'yı etkinleştir ' e tıklayın.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

Oturumu kapatın ve yeniden oturum açın. E-postayı etkinleştirdiyseniz ( [önceki öğreticime](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)bakın),/FA için SMS veya e-postayı seçebilirsiniz.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

Kodu doğrula sayfası görüntülenir (SMS veya e-posta).

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

**Bu tarayıcıya** göz atma onay kutusunun tıklanması, kutuyu seçtiğiniz tarayıcı ve cihazı kullanırken oturum açmak için 2FA kullanmaya gerek duymasını da muaf tutacaktır. Kötü amaçlı kullanıcılar cihazınıza erişim sağlayabilmediği sürece, 2FA 'yı etkinleştirmek ve **Bu tarayıcıyı anımsa** ' ya tıklamak, güvenilir olmayan cihazlardan tüm erişimler için güçlü bir adım parola erişimi sağlar. Düzenli olarak kullandığınız özel cihaz üzerinde bunu yapabilirsiniz.

Bu öğretici, yeni bir ASP.NET MVC uygulamasında 2FA 'yı etkinleştirmeye yönelik hızlı bir giriş sağlar. [ASP.NET Identity Ile SMS ve e-posta kullanarak öğreticimin iki öğeli kimlik doğrulaması](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) , örneğin arkasındaki kodla ilgili ayrıntılara gider.

<a id="addRes"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Identity Ile SMS ve e-posta kullanarak iki öğeli kimlik doğrulama](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Iki öğeli kimlik doğrulama ile ilgili ayrıntılara gider
- [Önerilen kaynakların ASP.NET Identity bağlantıları](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [ASP.NET Identity Ile hesap onaylama ve parola kurtarma](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Parola kurtarma ve hesap onaylama hakkında daha fazla ayrıntıya gider.
- [Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Bu öğreticide, Facebook ve Google OAuth 2 yetkilendirmesi ile ASP.NET MVC 5 uygulamasının nasıl yazılacağı gösterilmektedir. Ayrıca, kimlik veritabanına nasıl ek veri ekleneceğini gösterir.
- [Üyelik, OAuth ve SQL veritabanı Ile Azure Web 'e güvenli bir ASP.NET MVC uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Bu öğreticide, Azure dağıtımı, rollerle uygulamanızı güvenli hale getirme, Kullanıcı ve rolleri eklemek için üyelik API 'sini kullanma ve ek güvenlik özellikleri eklenir.
- [OAuth 2 için Google App oluşturma ve uygulamayı projeye bağlama](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook 'ta uygulama oluşturma ve uygulamayı projeye bağlama](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [Projede SSL ayarlama](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [C# Ve ASP.NET MVC geliştirme ortamınızı ayarlama](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
