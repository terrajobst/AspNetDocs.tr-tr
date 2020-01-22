---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: Oturum açma, e-posta onayı ve parola sıfırlama (C#) | ile güvenli BIR ASP.NET MVC 5 Web uygulaması oluşturma | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ASP.NET Identity üyelik sistemini kullanarak e-posta onayı ve parola sıfırlama ile bir ASP.NET MVC 5 Web uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir. CA 'nız...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 6169c972ad0f4ee2079d3638c54a5accc4b8b3de
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519355"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>Oturum açma, e-posta onayı ve parola sıfırlama özellikli, güvenli bir ASP.NET MVC 5 web uygulaması oluşturma (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

Bu öğreticide, ASP.NET Identity üyelik sistemini kullanarak e-posta onayı ve parola sıfırlama ile bir ASP.NET MVC 5 Web uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir.

.NET Core kullanan Bu öğreticinin güncelleştirilmiş bir sürümü için [ASP.NET Core 'de hesap onaylama ve parola kurtarma](/aspnet/core/security/authentication/accconfirm)bölümüne bakın.

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC uygulaması oluşturma

Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın. [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya üstünü yükler.

> [!NOTE]
> Uyarı: Bu öğreticiyi tamamlayabilmeniz için [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya sonraki bir sürümü yüklemelisiniz.

1. Yeni bir ASP.NET Web projesi oluşturun ve MVC şablonunu seçin. Web Forms Ayrıca ASP.NET Identity destekler, böylece bir Web Forms uygulamasındaki benzer adımları izleyebilirsiniz.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. Varsayılan kimlik doğrulamasını **bireysel kullanıcı hesapları**olarak bırakın. Uygulamayı Azure 'da barındırmak isterseniz onay kutusunu işaretli bırakın. Öğreticide daha sonra Azure 'a dağıtacağız. [Bir Azure hesabını ücretsiz olarak açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
3. [PROJEYI SSL kullanacak şekilde](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)ayarlayın.
4. Uygulamayı çalıştırın, **Kaydet** bağlantısına tıklayın ve bir Kullanıcı kaydedin. Bu noktada, e-postadaki tek doğrulama [[Emapostaadresi]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) özniteliğiyle aynıdır.
5. Sunucu Gezgini ' de **veri bağlantısı \ Defaultconnection\tables\aspnetusers**' a gidin, sağ tıklayın ve **tablo tanımını aç**' ı seçin.

    Aşağıdaki görüntüde `AspNetUsers` şeması gösterilmektedir:

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. **Aspnetusers** tablosuna sağ tıklayın ve **tablo verilerini göster**' i seçin.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 Bu noktada e-posta onaylanmamıştır.
7. Satıra tıklayın ve Sil ' i seçin. Bu e-postayı bir sonraki adımda tekrar ekleyecek ve bir onay e-postası göndereceğiz.

## <a name="email-confirmation"></a>E-posta onayı

Başka birinin taklit etmeyeceğinden emin olmak için yeni bir Kullanıcı kaydının e-postasını onaylamak en iyi uygulamadır. (diğer bir deyişle, başka birinin e-postasına kaydolmamaları). Bir tartışma forumu olduğunu varsayalım, `"bob@example.com"` `"joe@contoso.com"`olarak kaydolmasını engellemek isteyebilirsiniz. E-posta onayı olmadan `"joe@contoso.com"`, uygulamanızdan istenmeyen e-posta alabilir. Emre 'nin yanlışlıkla `"bib@example.com"` olarak kaydolduğunu ve olduğunu fark etmemiş olduğunu varsayalım, uygulamanın doğru e-postası olmadığından parola kurtarma kullanamayacak. E-posta onayı yalnızca botlardan sınırlı koruma sağlar ve belirlenen istenmeyen posta gönderenlerin korumasını sağlamaz, kaydolmak için kullanabilecekleri birçok çalışma e-posta diğer adı vardır.

Genellikle yeni kullanıcıların e-posta, SMS mesajı veya başka bir mekanizma tarafından onaylanmadan önce Web sitenize veri göndermeleri önlemektir. <a id="build"></a>Aşağıdaki bölümlerde, e-posta onayını etkinleştireceğiz ve yeni kayıtlı kullanıcıların e-postaları onaylanana kadar oturum açmasını önleyecek şekilde kodu değiştireceğiz.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid 'i bağlama

Bu bölümdeki yönergeler güncel değil. Bkz. güncelleştirilmiş yönergeler için [SendGrid e-posta sağlayıcısını yapılandırma](/aspnet/core/security/authentication/accconfirm#configure-email-provider) .

Bu öğretici yalnızca [SendGrid](http://sendgrid.com/)aracılığıyla e-posta bildirimi Eklemeyi gösterir, ancak SMTP ve diğer mekanizmaları kullanarak e-posta gönderebilirsiniz ( [ek kaynaklara](#addRes)bakın).

1. Paket Yöneticisi konsolunda aşağıdaki komutu girin: 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. [Azure SendGrid kaydolma sayfasına](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) gidin ve ücretsiz bir SendGrid hesabına kaydolun. *App_Start/ıdentityconfig.cs*içinde aşağıdakine benzer kod ekleyerek SendGrid 'i yapılandırın:

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

Şunları eklemeniz gerekir:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

Bu örneği basit tutmak için uygulama ayarlarını *Web. config* dosyasında depolayacağız:

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin. Hesap ve kimlik bilgileri appSetting 'de depolanır. Azure 'da, bu değerleri Azure portal **[Yapılandır](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** sekmesinde güvenli bir şekilde depolayabilirsiniz. [ASP.net ve Azure 'a parola ve diğer hassas verileri dağıtmaya yönelik en iyi uygulamalar](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)bölümüne bakın.

### <a name="enable-email-confirmation-in-the-account-controller"></a>Hesap denetleyicisinde e-posta onayını etkinleştir

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

*Views\Account\ConfirmEmail.cshtml* dosyasının doğru Razor söz dizimini içerdiğini doğrulayın. (İlk satırdaki @ karakteri eksik olabilir. )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

Uygulamayı çalıştırın ve Kaydet bağlantısına tıklayın. Kayıt formunu gönderdikten sonra oturumunuz açıldı.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

E-posta hesabınızı denetleyin ve e-postanızı onaylamak için bağlantıya tıklayın.

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>Oturum açmadan önce e-posta onayı gerektir

Şu anda bir kullanıcı kayıt formunu tamamladıktan sonra oturum açar. Genellikle e-postalarını oturum açmadan önce doğrulamak istersiniz. Aşağıdaki bölümde, yeni kullanıcıların oturum açmadan (kimliği doğrulanmış) önce onaylanan bir e-postaya sahip olmasını gerektirecek şekilde kodu değiştiririz. `HttpPost Register` yöntemini aşağıdaki vurgulanan değişikliklerle güncelleştirin:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

`SignInAsync` yöntemi yorum yaparak, Kullanıcı kayıt tarafından oturum açmamış olur. `TempData["ViewBagLink"] = callbackUrl;` satırı, e-posta göndermeden uygulama ve test kaydı [hatalarını ayıklamak](#dbg) için kullanılabilir. `ViewBag.Message`, onaylama yönergelerini göstermek için kullanılır. [İndirme örneği](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) , e-posta onayını e-posta ayarlamadan test etmek için kod içerir ve ayrıca uygulamada hata ayıklamak için de kullanılabilir.

`Views\Shared\Info.cshtml` bir dosya oluşturun ve aşağıdaki Razor işaretlemesini ekleyin:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

[Yetkilendirme özniteliğini](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) , ana denetleyicinin `Contact` Action yöntemine ekleyin. Anonim kullanıcıların erişimi yok ve kimliği doğrulanmış kullanıcıların erişimi olduğunu doğrulamak için **iletişim** bağlantısına tıklayabilirsiniz.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

`HttpPost Login` eylem yöntemini de güncelleştirmeniz gerekir:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

*Views\shared\error.exe* görünümünü şu hata iletisini görüntüleyecek şekilde güncelleştirin:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

Test etmek istediğiniz e-posta diğer adını içeren **Aspnetusers** tablosundaki tüm hesapları silin. Uygulamayı çalıştırın ve e-posta adresinizi onaylaana kadar oturum açabildiğinizi doğrulayın. E-posta adresinizi onaylayın, **iletişim** bağlantısına tıklayın.

<a id="reset"></a>
## <a name="password-recoveryreset"></a>Parola kurtarma/sıfırlama

Açıklama karakterlerini hesap denetleyicisindeki `HttpPost ForgotPassword` Action yönteminden kaldırın:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

*Views\account\login.exe* Razor görünüm dosyasında `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) ' den açıklama karakterlerini kaldırın:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

Oturum aç sayfasında artık parola sıfırlama bağlantısı gösterilir.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>E-posta onay bağlantısını yeniden gönder

Bir Kullanıcı yeni bir yerel hesap oluşturduktan sonra, oturum açmadan önce kullanmaları gereken bir onay bağlantısına e-posta gönderilir. Kullanıcı onay e-postasını yanlışlıkla silerse veya e-posta hiçbir daha ulaşmadıysa, onay bağlantısının yeniden gönderilmesi gerekir. Aşağıdaki kod değişiklikleri, bunun nasıl etkinleştirileceğini gösterir.

Aşağıdaki yardımcı yöntemi *Controllers\accountcontroller.cs* dosyasının altına ekleyin:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

Yeni yardımcıyı kullanmak için Register metodunu güncelleştirin:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

Kullanıcı hesabı onaylanmazsa parolayı yeniden göndermek için oturum açma yöntemini güncelleştirin:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>Sosyal ve yerel oturum açma hesaplarını birleştirme

E-posta bağlantısına tıklayarak Yerel ve sosyal hesapları birleştirebilirsiniz. Aşağıdaki sırada **RickAndMSFT@gmail.com** önce yerel bir oturum açma olarak oluşturulur, ancak önce hesabı önce bir sosyal oturum günlüğü olarak oluşturabilir, ardından yerel bir oturum açma ekleyebilirsiniz.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

**Yönet** bağlantısına tıklayın. Bu hesapla ilişkili **dış oturum açma sayısı: 0** ' a göz önüne alın.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

Başka bir oturum açma hizmetine bağlantıyı tıklatın ve uygulama isteklerini kabul edin. İki hesap birleştirildi, herhangi bir hesapla oturum açabilirsiniz. Kullanıcılarınızın, sosyal oturum açma kimlik doğrulaması hizmeti kapatılmış veya sosyal hesaplarına erişimi kaybetmiş olması olasılığına karşı yerel hesaplar eklemesini isteyebilirsiniz.

Aşağıdaki görüntüde, Tom bir sosyal oturum günlüğü (dış oturum açmalarından görebileceğiniz **: 1** gösterilen sayfada görebilirsiniz).

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

**Parola Seç** ' e tıkladığınızda, aynı hesapla ilişkili bir yerel günlük eklemenize izin verir.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>Daha ayrıntılı bir şekilde e-posta onayı

Öğretici [hesabı onaylama ve parola kurtarma ASP.NET Identity ile,](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) daha fazla ayrıntı için bu konuya gider.

<a id="dbg"></a>
## <a name="debugging-the-app"></a>Uygulamada hata ayıklama

Bağlantıyı içeren bir e-posta alamazsanız:

- Önemsiz veya istenmeyen posta klasörünüzü kontrol edin.
- SendGrid hesabınızda oturum açın ve [e-posta etkinliği bağlantısına](https://sendgrid.com/logs/index)tıklayın.

Doğrulama bağlantısını e-posta olmadan test etmek için [Tamamlanan örneği](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)indirin. Onay bağlantısı ve onay kodları sayfada görüntülenir.

<a id="addRes"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [Önerilen kaynakların ASP.NET Identity bağlantıları](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [ASP.NET Identity Ile hesap onaylama ve parola kurtarma](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Parola kurtarma ve hesap onaylama hakkında daha fazla ayrıntıya gider.
- [Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Bu öğreticide, Facebook ve Google OAuth 2 yetkilendirmesi ile ASP.NET MVC 5 uygulamasının nasıl yazılacağı gösterilmektedir. Ayrıca, kimlik veritabanına nasıl ek veri ekleneceğini gösterir.
- [Üyelik, OAuth ve SQL veritabanı Ile Azure 'Da güvenli bir ASP.NET MVC uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Bu öğreticide, Azure dağıtımı, rollerle uygulamanızı güvenli hale getirme, Kullanıcı ve rolleri eklemek için üyelik API 'sini kullanma ve ek güvenlik özellikleri eklenir.
- [OAuth 2 için Google App oluşturma ve uygulamayı projeye bağlama](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook 'ta uygulama oluşturma ve uygulamayı projeye bağlama](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [Projede SSL ayarlama](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
