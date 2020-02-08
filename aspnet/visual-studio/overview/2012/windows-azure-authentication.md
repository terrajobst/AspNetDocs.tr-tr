---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Windows Azure kimlik doğrulaması | Microsoft Docs
author: Rick-Anderson
description: Windows Azure Active Directory için Microsoft ASP.NET araçları, Windows Azure Web sitelerinde barındırılan Web uygulamaları için kimlik doğrulamasını etkinleştirmeyi kolaylaştırır...
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: 41c4e6d02c965c10aa35b882964f4f04d9b8c44b
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075157"
---
# <a name="windows-azure-authentication"></a>Windows Azure Kimlik Doğrulaması

[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından

> Windows Azure Active Directory için Microsoft ASP.NET araçları, [Windows Azure Web sitelerinde](https://www.windowsazure.com/home/features/web-sites/)barındırılan Web uygulamaları için kimlik doğrulamasını etkinleştirmeyi kolaylaştırır. Kuruluşunuzda Office 365 kullanıcılarının kimliğini doğrulamak için Windows Azure kimlik doğrulamasını kullanabilirsiniz, şirket içi Active Directory veya kendi özel Windows Azure Active Directory etki alanında oluşturulan kullanıcılarınız tarafından eşitlenmiş kurumsal hesaplardır. Windows Azure kimlik doğrulamasının etkinleştirilmesi, uygulamanızı tek bir [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) kiracı kullanarak kullanıcıların kimliğini doğrulayacak şekilde yapılandırır.
>
> ASP.NET Windows Azure kimlik doğrulama aracı bir bulut hizmetindeki Web rolleri için desteklenmez, ancak bunu gelecekteki bir sürümde yapmanız planlanıyoruz. Windows [Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF), Windows Azure Web rollerinde desteklenir.
>
> Şirket içi Active Directory ve Windows Azure Active Directory kiracınız arasında eşitlemeyi ayarlama hakkında daha fazla bilgi için lütfen bkz. [AD FS 2,0 kullanarak çoklu oturum açmayı uygulama ve yönetme](https://technet.microsoft.com/library/jj205462.aspx).
>
> Windows Azure Active Directory şu anda [ücretsiz bir önizleme hizmeti](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)olarak sunulmaktadır.

## <a name="requirements"></a>Gereksinimler:

- Visual Studio 2012 veya [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)
- [Visual Studio 2012 Için Web Araçları uzantıları](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) veya [Visual Studio Express 2012 Için Web Araçları uzantıları](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)
- [Windows Azure Active Directory için Microsoft ASP.NET araçları – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) veya [Windows için Microsoft ASP.NET araçları Azure Active Directory – Web için Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>Visual Studio 2012 ile ASP.NET Web uygulaması oluşturma

Visual Studio 2012 ile herhangi bir Web uygulaması oluşturabilirsiniz, bu öğretici ASP.NET MVC intranet şablonunu kullanır.

1. Yeni bir ASP.NET MVC 4 Intranet uygulaması oluşturun ve tüm varsayılanları kabul edin. (Bu, bir ın **tra** net ve **ter** net projesinde değil) olmalıdır.
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>Windows Azure kimlik doğrulamasını etkinleştir (Tenet 'in genel Yöneticisi olduğunuzda)

Mevcut bir Windows Azure Active Directory kiracınız yoksa (örneğin, mevcut bir Office 365 hesabı aracılığıyla), [Yeni bir windows Azure Active Directory hesabına](https://g.microsoftonline.com/0AX00en/5)kaydolarak yeni bir kiracı oluşturabilirsiniz.

1. Proje menüsünden **Windows Azure kimlik doğrulamasını etkinleştir**' i seçin:

   ![](windows-azure-authentication/_static/image2.png)

2. Windows Azure Active Directory kiracınızın etki alanını girin (örneğin, contoso.onmicrosoft.com) ve **Etkinleştir**' e tıklayın:

![](windows-azure-authentication/_static/image3.png)

3. Web kimlik doğrulaması iletişim kutusunda Windows Azure Active Directory kiracınız için yönetici olarak oturum açın:

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>Windows Azure 'ı bir Tenet Yöneticisi olmayan bir şekilde etkinleştirin

Windows Azure Active Directory kiracınız için genel yönetici ayrıcalıklarınız yoksa, uygulamayı sağlama onay kutusunun işaretini kaldırabilirsiniz.

![](windows-azure-authentication/_static/image6.png)

İletişim kutusunda, Azure Active Directory Tenet ile uygulamayı sağlamak için gereken **etki alanı**, **uygulama sorumlusu kimliği** ve **yanıt URL 'si** görüntülenir. Bu bilgileri uygulamayı sağlamak için yeterli ayrıcalığa sahip olan birine vermeniz gerekir. Hizmet sorumlusunu el ile oluşturmak için cmdlet 'i kullanma hakkında ayrıntılı bilgi için bkz.[Windows Azure Active Directory-ASP.NET uygulaması ile çoklu oturum açmayı](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) uygulama.
Uygulama başarılı bir şekilde sağlandıktan sonra, **Web. config 'i seçili ayarlarla güncelleştirmek Için devam**' a tıklayabilirsiniz. Hazırlama işleminin gerçekleşmesini beklerken uygulamayı geliştirmeye devam etmek istiyorsanız, **Proje dosyasındaki ayarları hatırlamak Için kapat**' a tıklayabilirsiniz. Windows Azure kimlik doğrulamasını etkinleştirin ve sağlama onay kutusunun işaretini kaldırın, aynı ayarları görürsünüz ve **devam**' a tıklayıp, **Bu ayarları Web. config dosyasına uygulayabilirsiniz**.

1. Uygulamanız Windows Azure kimlik doğrulaması için yapılandırılırken bekleyin ve Windows Azure Active Directory sağlandı.
2. Uygulamanız için Windows Azure kimlik doğrulaması etkinleştirildikten sonra Kapat ' a tıklayın **.**

    ![](windows-azure-authentication/_static/image7.png)
3. Uygulamanızı çalıştırmak için F5 'e basın. Otomatik olarak oturum açma sayfasına yönlendirilmelisiniz. Uygulamada oturum açmak için temel Kullanıcı kimlik bilgilerini kullanın.

    ![](windows-azure-authentication/_static/image1.jpg)
4. Uygulamanız Şu anda otomatik olarak imzalanan bir test sertifikası kullandığından, bir tarayıcıdan sertifikanın güvenilir bir sertifika yetkilisi tarafından çıkarılmadığını bildiren bir uyarı alacaksınız.

    Bu uyarı, yerel geliştirme sırasında **Bu Web sitesine devam et** seçeneğine tıklanarak güvenle yoksayılabilir:

    ![](windows-azure-authentication/_static/image8.png)
5. Windows Azure kimlik doğrulamasını kullanarak uygulamanızda başarıyla oturum açtınız!

    ![](windows-azure-authentication/_static/image2.jpg)

Windows Azure kimlik doğrulamasını etkinleştirmek uygulamanızda aşağıdaki değişiklikleri yapar:

- Bir çapraz site Isteği forgery ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) Sınıfı ( *App\_Start\AntiXsrfConfig.cs* ), projenize eklenir.
- NuGet paketleri `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` projenize eklenir.
- Uygulamanızdaki Windows Identity Foundation ayarları, Windows Azure Active Directory kiracınızdan güvenlik belirteçlerini kabul edecek şekilde yapılandırılacaktır. *Web. config* dosyasında yapılan değişikliklerin genişletilmiş görünümünü görmek için aşağıdaki görüntüye tıklayın.

     ![](windows-azure-authentication/_static/image9.png)
- Windows Azure Active Directory kiracınızdaki uygulamanız için bir hizmet sorumlusu sağlanacak.
- HTTPS etkin.

## <a name="deploy-the-application-to-windows-azure"></a>Uygulamayı Windows Azure 'a dağıtma

Tüm yönergeler için bkz. [Windows Azure Web sitesine ASP.NET Web uygulaması dağıtma](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).

Bir Azure Web sitesinde Windows Azure kimlik doğrulamasını kullanarak bir uygulama yayımlamak için:

1. Uygulamanıza sağ tıklayıp Yayımla ' yı seçin **:**

    ![](windows-azure-authentication/_static/image3.jpg)
2. Web 'i Yayımla iletişim kutusundan Azure Web siteniz için bir yayımlama profili indirin ve içeri aktarın.

    ![](windows-azure-authentication/_static/image4.jpg)
3. **Bağlantı** sekmesi **hedef URL 'yi** (Uygulamanızın genel kullanıma yönelik URL 'si) gösterir. Bağlantınızı test etmek için **bağlantıyı doğrula** ' ya tıklayın:

    ![](windows-azure-authentication/_static/image5.jpg)
4. Bu Azure Web sitesine daha önce yayımladıysanız uygulamanızın düzgün bir şekilde yayımlanmasını sağlamak için **Hedefteki ek dosyaları Kaldır** ayarını kontrol etmeyi göz önünde bulundurun. **Windows Azure kimlik doğrulamasını etkinleştir** onay kutusunun seçili olduğuna dikkat edin.

    ![](windows-azure-authentication/_static/image10.png)
5. İsteğe bağlı: **Önizleme** sekmesinde, dağıtılan dosyaları görmek Için **önizlemeyi Başlat** ' a tıklayın.

    ![](windows-azure-authentication/_static/image6.jpg)
6. Yayımla ' ya tıklayın **.**

    Hedef konak için Windows Azure kimlik doğrulamasını etkinleştirmeniz istenir. Devam etmek için **Etkinleştir** 'e tıklayın:

    ![](windows-azure-authentication/_static/image11.png)
7. Windows Azure Active Directory kiracınız için yönetici kimlik bilgilerinizi girin:

    ![](windows-azure-authentication/_static/image7.jpg)
8. Uygulamanız başarıyla yayımlandıktan sonra yayınlanan web sitesinde bir tarayıcı açılır.

    > [!NOTE]
    > Hedef ana bilgisayar için Windows Azure kimlik doğrulamasını etkinleştirdikten sonra uygulamanızın Windows Azure Active Directory ile tam olarak sağlanması için beş dakika kadar sürebilir (genellikle daha az olmalıdır). Uygulamanızı ilk kez çalıştırdığınızda ACS50001 hatası alırsanız: ' [Realm] ' adlı bağlı olan taraf bulunamadı, birkaç dakika bekleyip uygulamayı yeniden çalıştırmayı deneyin.
9. İstendiğinde, dizininizde bir kullanıcı olarak oturum açın:

    ![](windows-azure-authentication/_static/image8.jpg)
10. Azure 'da barındırılan uygulamanızda Windows Azure kimlik doğrulamasını kullanarak başarıyla oturum açtınız.

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>Bilinen Sorunlar

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a>Windows Azure kimlik doğrulaması kullanılırken rol tabanlı yetkilendirme başarısız oluyor

Windows Azure kimlik doğrulaması, rol tabanlı yetkilendirmenin gerçekleştirilebilmesi için gerekli rol talebini Şu anda sağlamıyor. Kimliği doğrulanmış kullanıcının rolü Windows Azure Active Directory el ile alınmış olmalıdır.

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a>Windows Azure kimlik doğrulaması ile bir uygulamaya gözatılırken "ACS20016 oturum açan kullanıcının etki alanı (live.com), bu STS 'nin izin verilen etki alanıyla eşleşmez" hatası ile sonuçlanır.

Zaten bir Microsoft hesabında oturum açtıysanız (örneğin, hotmail.com, live.com, outlook.com) ve Windows Azure kimlik doğrulamasını etkinleştirmiş bir uygulamaya erişmeye çalışırsanız, Microsoft hesabınızın etki alanı nedeniyle 400 hata yanıtını alabilirsiniz Windows Azure Active Directory tarafından tanınmıyor. Uygulamada oturum açmak için önce Microsoft hesabınızda oturumunuzu açın.

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a>Windows Azure kimlik doğrulaması etkinken bir uygulamada oturum açmak ve accounts.accesscontrol.windows.net sertifikası için sertifika doğrulama hatalarına neden olmayan bir X509CertificateValidationMode

Sertifika doğrulama gerekli değildir ve devre dışı bırakılmalıdır. Verenin sertifikasının parmak izi, WSFederationAuthenticationModule tarafından onaylanır.

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a>Windows Azure kimlik doğrulamasını etkinleştirmeye çalışırken, Web kimlik doğrulaması iletişim kutusunda "ACS20016: oturum açan kullanıcının etki alanı (contoso.onmicrosoft.com), bu STS 'nin izin verilen herhangi bir etki alanıyla eşleşmiyor."

Aynı Visual Studio işleminin içinden farklı bir Windows Azure Active Directory hesabı kullanarak oturum açmış olmanız durumunda bu hatayı görebilirsiniz. Belirtilen hesaptan oturumunuzu açın veya Visual Studio 'Yu yeniden başlatın. Daha önce oturum açtıysanız ve "Oturumumu Açık tut" seçeneğini belirlediyseniz tarayıcı tanımlama bilgilerinizi temizlemeniz gerekebilir.

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a>ACS20012: istek geçerli bir WS-Federation protokol iletisi değil

Azure hizmetlerinden birine ait başka bir Microsoft KIMLIĞIYLE oturum açtıysanız bu durum oluşabilir. IE1 veya Chrome 'da InPrivate veya tüm tanımlama bilgilerini temizleme gibi özel tarayıcı penceresini kullanın.

## <a name="additional-resources"></a>Ek Kaynaklar

- [Windows Azure Active Directory için Microsoft ASP.NET araçları – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertoccı
- [Windows Azure özellikleri: kimlik](https://docs.microsoft.com/azure/active-directory/)
- [TechNet: Windows Azure Active Directory](https://technet.microsoft.com/library/hh967619.aspx)
- [Windows Azure Active Directory: kuruluşunuz için uygulama geliştirme](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Windows Azure Active Directory: birden çok kuruluş için uygulama geliştirme](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [Windows Azure Active Directory ile çoklu oturum açma uygulama](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [Windows Azure Active Directory 'de çoklu oturum açma: derin bir Dive](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertoccı
- [Çoklu oturum açmayı uygulamak ve yönetmek için AD FS 2,0 kullanın](https://technet.microsoft.com/library/jj205462.aspx)
