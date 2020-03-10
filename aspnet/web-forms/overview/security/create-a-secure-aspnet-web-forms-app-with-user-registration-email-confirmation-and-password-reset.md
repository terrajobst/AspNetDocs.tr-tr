---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: Kullanıcı kaydıyla güvenli bir ASP.NET Web Forms uygulaması oluşturma, e-posta onayı ve parola sıfırlamaC#() | Microsoft Docs
author: Erikre
description: Bu öğreticide, Kullanıcı kaydıyla bir ASP.NET Web Forms uygulamasının nasıl oluşturulacağı, e-posta onayı ve parola sıfırlama ASP.NET Identity üyesini kullanarak nasıl oluşturulacağı gösterilmektedir...
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: af3653bc164810126bc3bf8f1b1794d75642d807
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78625155"
---
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a>Kullanıcı kaydı, e-posta onayı ve parola sıfırlama özellikli, güvenli bir ASP.NET Web Forms uygulaması oluşturma (C#)

by [Erik Reitan](https://github.com/Erikre)

> Bu öğreticide, Kullanıcı kaydı, e-posta onayı ve parola sıfırlama ile ASP.NET Identity üyelik sistemi kullanılarak bir ASP.NET Web Forms uygulamasının nasıl oluşturulacağı gösterilmektedir. Bu öğretici Rick Anderson 'ın [MVC öğreticisini](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)temel alır.

## <a name="introduction"></a>Giriş

Bu öğretici, Kullanıcı kaydı, e-posta onayı ve parola sıfırlama ile güvenli bir Web Forms uygulaması oluşturmak için Visual Studio ve ASP.NET 4,5 kullanarak bir ASP.NET Web Forms uygulaması oluşturmak için gereken adımlarda size rehberlik eder.

### <a name="tutorial-tasks-and-information"></a>Öğretici görevleri ve bilgileri:

- [ASP.NET Web Forms uygulaması oluşturma](#createWebForms)
- [SendGrid 'i bağlama](#SG)
- [Oturum açmadan önce e-posta onayı gerektir](#require)
- [Parola kurtarma ve sıfırlama](#reset)
- [E-posta onay bağlantısını yeniden gönder](#rsend)
- [Uygulama sorunlarını giderme](#dbg)
- [Ek Kaynaklar](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>ASP.NET Web Forms uygulaması oluşturma

Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın. [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya üstünü de yükler.

> [!NOTE]
> Uyarı: Bu öğreticiyi tamamlayabilmeniz için [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya sonraki bir sürümü yüklemelisiniz.

1. Yeni proje (**dosya** -&gt; **Yeni proje**) oluşturun ve **Yeni proje** iletişim kutusundan **ASP.NET Web uygulaması** şablonunu ve en son .NET Framework sürümünü seçin.
2. **Yeni ASP.NET projesi** iletişim kutusundan **Web Forms** şablonunu seçin. Varsayılan kimlik doğrulamasını **bireysel kullanıcı hesapları**olarak bırakın. Uygulamayı Azure 'da barındırmak istiyorsanız, **Konağı bulutta** bırakın onay kutusunu işaretleyin.   
 Ardından, yeni projeyi oluşturmak için **Tamam** ' ı tıklatın.  
    Yeni ASP.NET projesi iletişim kutusu ![](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)
3. Proje için Güvenli Yuva Katmanı (SSL) etkinleştirin. [Web Forms öğretici serisini kullanmaya](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)başlama konusunun **Proje Için SSL 'yi etkinleştirme** bölümünde bulunan adımları izleyin.
4. Uygulamayı çalıştırın, **Kaydet** bağlantısına tıklayın ve yeni bir Kullanıcı kaydedin. Bu noktada e-postadaki tek doğrulama, e-posta adresinin doğru biçimlendirildiğinden emin olmak için [[Emadresi]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) özniteliğini temel alır. E-posta onayı eklemek için kodu değiştirirsiniz. Tarayıcı penceresini kapatın.
5. Visual Studio 'nun **Sunucu Gezgini** ( -&gt; **Sunucu Gezgini** **görüntüleyin** ), **veri bağlantısı \ defaultconnection\tables\aspnetusers**konumuna gidin, sağ tıklayın ve **tablo tanımını aç**' ı seçin. 

    Aşağıdaki görüntüde `AspNetUsers` tablo şeması gösterilmektedir:

    ![AspNetUsers tablosu şeması](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. **Sunucu Gezgini**, **aspnetusers** tablosuna sağ tıklayın ve **tablo verilerini göster**' i seçin.  
  
    ![AspNetUsers tablosu verileri](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 Bu noktada kayıtlı Kullanıcı için e-posta onaylanmamıştır.
7. Satırı tıklatın ve Sil ' i seçerek kullanıcıyı silin. Bu e-postayı bir sonraki adımda tekrar ekleyecek ve e-posta adresine bir onay iletisi göndereceğiz.

## <a name="email-confirmation"></a>E-posta onayı

Yeni bir kullanıcı kaydı sırasında e-postayı, başka birinin taklit etmeyeceğinden emin olmak için (diğer bir deyişle, başka birinin e-postasına kaydolmayan) doğrulamak en iyi uygulamadır. Bir tartışma forumu olduğunu varsayalım, `"bob@cpandl.com"` `"joe@contoso.com"`olarak kaydolmasını engellemek isteyebilirsiniz. E-posta onayı olmadan `"joe@contoso.com"`, uygulamanızdan istenmeyen e-posta alabilir. Emre 'nin yanlışlıkla `"bib@cpandl.com"` olarak kaydolduğunu ve olduğunu fark etmemiş olduğunu varsayalım, uygulamanın doğru e-postası olmadığından parola kurtarma kullanamayacak. E-posta onayı yalnızca botlardan sınırlı koruma sağlar ve belirlenen istenmeyen posta gönderenlerin korumasını sağlamaz.

Genellikle yeni kullanıcıların e-posta, SMS metin iletisi veya başka bir mekanizmadan onaylanmadan önce Web sitenize veri almasını engellemek istersiniz. Aşağıdaki bölümlerde, e-posta onayını etkinleştireceğiz ve yeni kayıtlı kullanıcıların e-postaları onaylanana kadar oturum açmasını önleyecek şekilde kodu değiştireceğiz. Bu öğreticide, SendGrid e-posta hizmetini kullanacaksınız.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid 'i bağlama

Bu öğretici yazıldıktan sonra SendGrid bu API 'YI değiştirdi. Geçerli SendGrid yönergeleri için bkz. [SendGrid](http://sendgrid.com/) veya [Hesap onaylama ve parola kurtarmayı etkinleştirme](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery).

Bu öğretici yalnızca [SendGrid](http://sendgrid.com/)aracılığıyla e-posta bildirimi Eklemeyi gösterir, ancak SMTP ve diğer mekanizmaları kullanarak e-posta gönderebilirsiniz ( [ek kaynaklara](#addRes)bakın).

1. Visual Studio 'da **Paket Yöneticisi konsolu 'nu** açın (**Araçlar** -&gt; **NuGet paket** Yöneticisi -&gt; **Paket Yöneticisi konsolu**) ve aşağıdaki komutu girin:  
    `Install-Package SendGrid`
2. [Azure SendGrid kaydolma sayfasına](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) gidin ve ücretsiz SendGrid hesabına kaydolun. Ayrıca, doğrudan [SendGrid 'in sitesinde](http://www.sendgrid.com)ücretsiz bir SendGrid hesabına kaydolabilirsiniz.
3. **Çözüm Gezgini** *uygulama\_başlangıç* klasöründeki *IdentityConfig.cs* dosyasını açın ve aşağıdaki kodu sarı olarak vurgulanmış şekilde `EmailService` sınıfına **ekleyin:**

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. Ayrıca, *IdentityConfig.cs* dosyasının başlangıcına aşağıdaki `using` deyimlerini ekleyin: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. Bu örneği basit tutmak için, *Web. config* dosyasının `appSettings` bölümünde e-posta hizmeti hesap değerlerini depolayacaksınız. Aşağıdaki XML vurgulanmış olan XML 'i, projenizin kökündeki *Web. config* dosyasına ekleyin:

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin. Bu örnekte, hesap ve kimlik bilgileri *Web. config* dosyasının **AppSetting** bölümünde depolanır. Azure 'da, bu değerleri Azure portal **[Yapılandır](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** sekmesinde güvenli bir şekilde depolayabilirsiniz. İlgili bilgiler için bkz. Rick Anderson 'ın [, parolaları ve diğer hassas verileri ASP.net ve Azure 'a dağıtmaya yönelik en iyi yöntemler](https://go.microsoft.com/fwlink/?LinkId=513141)başlıklı konuya bakın.
6. Uygulamanızdan e-posta gönderebilmeniz için, SendGrid kimlik doğrulama değerlerinizi (Kullanıcı adı ve parola) yansıtacak şekilde e-posta hizmeti değerlerini ekleyin. SendGrid 'i girdiğiniz e-posta adresi yerine SendGrid hesap adınızı kullandığınızdan emin olun.

### <a name="enable-email-confirmation"></a>E-posta onayını etkinleştir

 E-posta onayını etkinleştirmek için, aşağıdaki adımları kullanarak kayıt kodunu değiştirirsiniz.  

1. *Hesap* klasöründe, *register.aspx.cs* arka plan kodunu açın ve aşağıdaki vurgulanan değişiklikleri etkinleştirmek için `CreateUser_Click` yöntemini güncelleştirin: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. **Çözüm Gezgini**, *default. aspx* öğesine sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.
3. F5 tuşuna basarak uygulamayı çalıştırın **.** Sayfa görüntülendikten sonra kayıt sayfasını göstermek için **Kaydet** bağlantısına tıklayın.
4. E-postanızı ve parolanızı girip, SendGrid aracılığıyla e-posta iletisi göndermek için **Kaydet** düğmesine tıklayın.  
   Projenizin ve kodunuzun geçerli durumu, kullanıcının, hesaplarını onaylamadıklarında bile, kayıt formunu tamamladıktan sonra oturum açmasına izin verir.
5. E-posta hesabınızı denetleyin ve e-postanızı onaylamak için bağlantıya tıklayın.  
   Kayıt formunu gönderdikten sonra oturumunuz açılır.  
    ![Örnek Web sitesi-oturum açıldı](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>Oturum açmadan önce e-posta onayı gerektir

E-posta hesabını onaylasanız da bu noktada, tam olarak oturum açmak için doğrulama e-postasında bulunan bağlantıya tıklamanızın gerekli değildir. Aşağıdaki bölümde, oturum açmadan önce yeni kullanıcıların onaylanmış bir e-postaya sahip olmasını gerektiren kodu değiştirirsiniz (kimliği doğrulanmış).

1. Visual Studio 'nun **Çözüm Gezgini** , *hesaplar* klasöründe yer alan *register.aspx.cs* kodundaki `CreateUser_Click` olayını aşağıdaki vurgulanan değişikliklerle güncelleştirin: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. *Login.aspx.cs* kodundaki `LogIn` yöntemini aşağıdaki vurgulanan değişikliklerle güncelleştirin: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a>Uygulamayı çalıştırma

 Bir kullanıcının e-posta adresinin onaylanmış olup olmadığını denetlemek için kodu uyguladığınıza göre, hem **kayıt** hem de **oturum açma** sayfalarında işlevselliği kontrol edebilirsiniz. 

1. Test etmek istediğiniz e-posta diğer adını içeren **Aspnetusers** tablosundaki tüm hesapları silin.
2. Uygulamayı çalıştırın (**F5**) ve e-posta adresinizi onaylaana kadar Kullanıcı olarak kaydolamadığınızdan emin olun.
3. Yeni hesabınızı yeni gönderilmiş e-posta yoluyla onaylamadan önce yeni hesapla oturum açmaya çalışın.  
 Oturum açamayabilirsiniz ve onaylanan bir e-posta hesabınız olması gerektiğini göreceksiniz.
4. E-posta adresinizi onaylayın, uygulamada oturum açın.

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a>Parola kurtarma ve sıfırlama

1. Visual Studio 'da, yöntemin aşağıdaki gibi görünmesi için *Hesap* klasöründe yer alan *forgot.aspx.cs* kodundaki `Forgot` yönteminden açıklama karakterlerini kaldırın: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. *Login. aspx* sayfasını açın. **Logbilgilendirme** bölümünün sonundaki biçimlendirmeyi aşağıda vurgulanan şekilde değiştirin: 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. *Login.aspx.cs* arka plan kodunu açın ve `Page_Load` olay işleyicisinden sarı renkle vurgulanmış olan aşağıdaki kod satırını açıklama satırı yapın: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. F5 tuşuna basarak uygulamayı çalıştırın **.** Sayfa görüntülendikten sonra **oturum aç** bağlantısına tıklayın.
5. Parolayı **unuttum** sayfasını göstermek Için **parolanızı unuttum?** bağlantısına tıklayın.
6. E-posta adresinizi girin ve **Gönder** düğmesine tıklayarak adresinize bir e-posta gönderin, bu da parolanızı sıfırlamanıza olanak tanır.   
   E-posta hesabınızı denetleyin ve **Parolayı Sıfırla** sayfasını göstermek için bağlantıya tıklayın.
7. **Parolayı Sıfırla** sayfasında, e-postanızı, parolanızı ve onaylanan parolayı girin. Ardından **Sıfırla** düğmesine basın.  
   Parolanızı başarıyla sıfırladıktan sonra **Parola değişti** sayfası görüntülenir. Artık yeni parolanızla oturum açabilirsiniz.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>E-posta onay bağlantısını yeniden gönder

Bir Kullanıcı yeni bir yerel hesap oluşturduktan sonra, oturum açmadan önce kullanmaları gereken bir onay bağlantısına e-posta gönderilir. Kullanıcı onay e-postasını yanlışlıkla silerse veya e-posta hiçbir daha ulaşmadıysa, onay bağlantısının yeniden gönderilmesi gerekir. Aşağıdaki kod değişiklikleri, bunun nasıl etkinleştirileceğini gösterir.

1. Visual Studio 'da **login.aspx.cs** arka plan kodunu açın ve `LogIn` olay işleyicisinden sonra aşağıdaki olay işleyicisini ekleyin:   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. Sarı renkle vurgulanmış kodu aşağıdaki gibi değiştirerek *login.aspx.cs* kodundaki `LogIn` olay işleyicisini değiştirin: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. Sarı renkle vurgulanmış kodu aşağıdaki gibi ekleyerek *login. aspx* sayfasını güncelleştirin: 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. Test etmek istediğiniz e-posta diğer adını içeren **Aspnetusers** tablosundaki tüm hesapları silin.
5. Uygulamayı çalıştırın (**F5**) ve e-posta adresinizi kaydedin.
6. Yeni hesabınızı yeni gönderilmiş e-posta yoluyla onaylamadan önce yeni hesapla oturum açmaya çalışın.  
   Oturum açamayabilirsiniz ve onaylanan bir e-posta hesabınız olması gerektiğini göreceksiniz. Ayrıca, artık e-posta hesabınıza bir onay iletisi gönderebilirsiniz.
7. E-posta adresinizi ve parolanızı girip yeniden **Gönder onay** düğmesine basın.
8. E-posta adresinizi yeni gönderilen e-posta iletisine göre onaylamadan, uygulamada oturum açın.

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a>Uygulama sorunlarını giderme

Kimlik bilgilerinizi doğrulama bağlantısını içeren bir e-posta almazsanız:

- Önemsiz veya istenmeyen posta klasörünüzü kontrol edin.
- SendGrid hesabınızda oturum açın ve [e-posta etkinliği bağlantısına](https://sendgrid.com/logs/index)tıklayın.
- SendGrid Kullanıcı hesabınızın adını, SendGrid hesabınızın e-posta adresiniz yerine bir *Web. config* değeri olarak kullandıklarından emin olun.

<a id="addRes"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [Önerilen kaynakların ASP.NET Identity bağlantıları](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [ASP.NET Identity ile hesap onaylama ve parola kurtarma](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Web Forms öğretici serisi-OAuth 2,0 sağlayıcısı ekleme](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [Üyelik, OAuth ve SQL veritabanı ile güvenli bir ASP.NET Web Forms uygulamasını dağıtın Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms öğretici serisi-proje için SSL 'yi etkinleştir](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
