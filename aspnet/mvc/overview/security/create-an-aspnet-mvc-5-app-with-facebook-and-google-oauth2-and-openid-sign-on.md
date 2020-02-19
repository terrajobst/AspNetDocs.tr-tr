---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma (C#) ile MVC 5 uygulaması oluşturun | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, kullanıcıların bir dış ön kimlik bilgileriyle OAuth 2,0 kullanarak oturum açmasını sağlayan bir ASP.NET MVC 5 Web uygulamasının nasıl oluşturulacağı gösterilmektedir...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457693"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Facebook, Twitter, LinkedIn ve Google OAuth2 Oturum Açma Özellikli Bir ASP.NET MVC 5 Uygulaması Oluşturma (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticide, kullanıcıların bir dış kimlik doğrulama sağlayıcısından (Facebook, Twitter, LinkedIn, Microsoft veya Google gibi) kimlik bilgileriyle [OAuth 2,0](http://oauth.net/2/) kullanarak oturum açmasını sağlayan BIR ASP.NET MVC 5 Web uygulaması oluşturma yöntemi gösterilmektedir. Kolaylık olması için, bu öğretici Facebook ve Google kimlik bilgileriyle çalışmaya odaklanır.
> 
> Bu kimlik bilgilerini Web sitelerinizde etkinleştirmek, milyonlarca kullanıcının zaten bu dış sağlayıcıları olan hesapları olduğundan önemli bir avantaj sağlar. Bu kullanıcılar yeni bir kimlik bilgileri kümesi oluşturup hatırlamaları zorunda olmadıkları takdirde sitenize kaydolmak için daha fazla işlem yapılabilir.
> 
> Ayrıca bkz. [ASP.NET MVC 5 UYGULAMASı SMS ve e-posta Iki öğeli kimlik doğrulaması](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).
> 
> Öğretici Ayrıca, Kullanıcı için profil verilerinin nasıl ekleneceğini ve rol eklemek için üyelik API 'sinin nasıl kullanılacağını gösterir. Bu öğretici [Rick Anderson](https://blogs.msdn.com/rickAndy) tarafından yazılmıştır (lütfen Twitter 'da şu adımları izleyin: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).

<a id="start"></a>
## <a name="getting-started"></a>Başlarken

Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın. Visual Studio [2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390521) veya üstünü yükler. Dropbox, GitHub, LinkedIn, Instagram, buffer, Salesforce, STEHAR, Stack Exchange, Tripit, Twitch, Twitter, Yahoo! ve daha birçok konuda yardım almak için bu [örnek projeye](https://github.com/matthewdunsdon/oauthforaspnet)bakın.

> [!NOTE]
> Google OAuth 2 ' i kullanmak ve SSL uyarıları olmadan yerel olarak hata ayıklamak için Visual Studio [2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390521) veya üstünü yüklemelisiniz.

**Başlangıç** sayfasından **Yeni proje** ' ye tıklayın veya menüyü ve ardından **Dosya**' yı ve ardından **Yeni proje**' yi seçin.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>Ilk uygulamanızı oluşturma

**Yeni proje**' ye tıklayın, ardından sol taraftaki **görsel C#**  ' i **seçin ve sonra** **ASP.NET Web uygulaması**' nı seçin. Projenizi "MvcAuth" olarak adlandırın ve ardından **Tamam**' a tıklayın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

**Yeni ASP.NET projesi** Iletişim kutusunda **MVC**' ye tıklayın. Kimlik doğrulaması **ayrı kullanıcı hesapları**değilse, **kimlik doğrulamasını Değiştir** düğmesine tıklayın ve **bireysel kullanıcı hesapları**' nı seçin. **Bulutta ana bilgisayar**denetlenerek, uygulamanın Azure 'da barındırmak çok kolay olacaktır.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

**Bulutta ana bilgisayar**' ı seçtiyseniz, Yapılandır iletişim kutusunu doldurun.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>En son OWıN ara yazılım sürümüne güncelleştirmek için NuGet kullanın

[Owın ara yazılımını](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)güncelleştirmek için NuGet paket yöneticisini kullanın. Soldaki menüden **güncelleştirmeler** ' i seçin. **Tümünü Güncelleştir** düğmesine tıklayabilirsiniz veya yalnızca owın paketleri için arama yapabilirsiniz (bir sonraki görüntüde gösterilmektedir):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

Aşağıdaki görüntüde yalnızca OWıN paketleri gösteriliyor:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

Paket Yöneticisi konsolundan (PMC), tüm paketleri güncelleştirecek `Update-Package` komutunu girebilirsiniz.

Uygulamayı çalıştırmak için **F5** veya **CTRL + F5** tuşlarına basın. Aşağıdaki görüntüde, bağlantı noktası numarası 1234 ' dir. Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görürsünüz.

Tarayıcı pencerenizin boyutuna bağlı olarak, **giriş**, **hakkında**, **Iletişim kurma**, **kayıt** ve **oturum açma** bağlantılarını görmek için gezinti simgesine tıklamanız gerekebilir.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>Projede SSL ayarlama

Google ve Facebook gibi kimlik doğrulama sağlayıcılarına bağlanmak için IIS-Express ' i SSL kullanacak şekilde ayarlamanız gerekecektir. Oturum açtıktan sonra SSL 'yi kullanmaya devam etmek ve HTTP 'ye geri dönmek önemlidir, oturum açma tanımlama bilgileriniz yalnızca Kullanıcı adınız ve parolanız olarak gizli olur ve SSL kullanmadan, bunu kablolu olarak düz metin halinde gönderiyoruz. Bunun yanı sıra, MVC işlem hattı çalıştırılmadan önce el sıkışma gerçekleştirme ve kanalı güvenli hale getirme (HTTP 'den daha yavaş olan HTTP 'den yavaş olan), bu nedenle oturum açtıktan sonra HTTP 'ye yeniden yönlendirme geçerli istek veya gelecekteki istekleri çok daha hızlı.

1. **Çözüm Gezgini**, **mvcauth** projesine tıklayın.
2. Proje özelliklerini göstermek için F4 tuşuna basın. Alternatif olarak, **Görünüm** menüsünden **Özellikler penceresi**' ni seçebilirsiniz.
3. **SSL etkin** ' i true olarak değiştirin.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. SSL URL 'sini kopyalayın (başka bir SSL projesi oluşturmadığınız müddetçe `https://localhost:44300/` olur).
5. **Çözüm Gezgini**, **mvcauth** projesine sağ tıklayın ve **Özellikler**' i seçin.
6. **Web** sekmesini seçin ve ardından SSL URL 'Sini **proje URL** 'si kutusuna yapıştırın. Dosyayı kaydedin (CTL + S). Facebook ve Google kimlik doğrulama uygulamalarını yapılandırmak için bu URL 'ye ihtiyacınız olacak.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. Tüm isteklerin HTTPS kullanması gerektiğini gerektirmek için `Home` denetleyiciye [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) özniteliğini ekleyin. Daha güvenli bir yaklaşım uygulamaya [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtresini eklemektir. Uygulamayı SSL ile koruma &quot;bölümüne bakın ve öğreticimde Yetkilendir özniteliği&quot; [kimlik doğrulama ve SQL DB ile bir ASP.NET MVC uygulaması oluşturun ve Azure App Service 'e dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Ana denetleyicinin bir bölümü aşağıda gösterilmiştir.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Uygulamayı çalıştırmak için CTRL+F5'e basın. Sertifikayı geçmişte yüklediyseniz, bu bölümün geri kalanını atlayabilir ve [OAuth 2 Için Google uygulaması oluşturmaya ve uygulamayı projeye bağlamaya](#goog)geçebilirsiniz, aksi takdirde, IIS Express oluşturduğu otomatik olarak imzalanan sertifikaya güvenmek için yönergeleri izleyin.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. **Güvenlik uyarısı** iletişim kutusunu okuyun ve ardından localhost 'u temsil eden sertifikayı yüklemek istiyorsanız **Evet** ' e tıklayın.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE *giriş* sayfasını gösterır ve SSL uyarısı yoktur.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome sertifikayı da kabul eder ve HTTPS içeriğini uyarı olmadan gösterir. Firefox kendi sertifika deposunu kullanır, bu nedenle bir uyarı görüntüler. Uygulamamız için **riskleri anladım**' ı güvenle deneyebilirsiniz.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>OAuth 2 için Google App oluşturma ve uygulamayı projeye bağlama

> [!WARNING]
> Geçerli Google OAuth yönergeleri için bkz. [ASP.NET Core Google kimlik doğrulamasını yapılandırma](/aspnet/core/security/authentication/social/google-logins).

1. [Google geliştiricileri konsoluna](https://console.developers.google.com/)gidin.
2. Daha önce bir proje oluşturmadıysanız, sol sekmede **kimlik bilgileri** ' ni seçin ve ardından **Oluştur**' u seçin.
3. Sol sekmede **kimlik bilgileri**' ne tıklayın.
4. **Kimlik bilgileri oluştur** ' a tıklayın, **OAuth istemci kimliği**. 

    1. **ISTEMCI kimliği oluştur** iletişim kutusunda, uygulama türü Için varsayılan **Web uygulamasını** saklayın.
    2. **Yetkili JavaScript** kaynakları ' nı yukarıda KULLANDıĞıNıZ SSL URL 'sine ayarlayın (başka bir SSL projesi oluşturmadığınız müddetçe`https://localhost:44300/`)
    3. **Yetkilendirilmiş yeniden YÖNLENDIRME URI** 'sini şu şekilde ayarlayın:  
         `https://localhost:44300/signin-google`
5. OAuth onay ekranı menü öğesine tıklayın, ardından e-posta adresinizi ve ürün adınızı ayarlayın. Formu tamamladığınızda **Kaydet**' e tıklayın.
6. Kitaplık menü öğesine tıklayın, **Google + API**ara ' ya tıklayın, ardından Etkinleştir ' e basın.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   Aşağıdaki görüntüde etkin API 'Ler gösterilmektedir.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Google API 'Leri API Manager 'dan, **ISTEMCI kimliğini**edinmek Için **kimlik bilgileri** sekmesini ziyaret edin. Bir JSON dosyasını uygulama gizli dizileri ile kaydetmek için indirin. **ClientID** ve **clientsecret** dosyalarını kopyalayıp *App_Start* klasöründeki *Startup.auth.cs* dosyasında bulunan `UseGoogleAuthentication` yöntemine yapıştırın. Aşağıda gösterilen **ClientID** ve **ClientSecret** değerleri, örnekler ve çalışmalardır.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin. Hesap ve kimlik bilgileri, örneği basit tutmak için yukarıdaki koda eklenir. [ASP.net ve Azure App Service için parola ve diğer hassas verileri dağıtmaya yönelik en iyi uygulamalar](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)bölümüne bakın.
8. Uygulamayı derlemek ve çalıştırmak için **CTRL + F5** tuşlarına basın. **Oturum aç** bağlantısına tıklayın.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. **Oturum açmak için başka bir hizmet kullan**' ın altında **Google**' a tıklayın.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > Yukarıdaki adımlardan herhangi birini kaçırırsanız, bir HTTP 401 hatası alacaksınız. Yukarıdaki adımları yeniden denetleyin. Gerekli bir ayarı (örneğin, **ürün adı**) kaçırırsanız, eksik öğeyi ekleyin ve kaydedin; kimlik doğrulamasının çalışması birkaç dakika sürebilir.
10. Kimlik bilgilerinizi gireceğiniz Google sitesine yönlendirilirsiniz.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. Kimlik bilgilerinizi girdikten sonra, yeni oluşturduğunuz Web uygulamasına izin vermeniz istenir:
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. **Kabul et**' e tıklayın. Şimdi, Google hesabınızı kaydedebileceğiniz MvcAuth uygulamasının **kayıt** sayfasına yeniden yönlendirilirsiniz. Gmail hesabınız için kullanılan yerel e-posta kayıt adını değiştirme seçeneğiniz vardır, ancak genellikle varsayılan e-posta diğer adını (yani, kimlik doğrulaması için kullandığınız hesap) korumak istersiniz. **Kaydol**' a tıklayın.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Facebook 'ta uygulama oluşturma ve uygulamayı projeye bağlama

> [!WARNING]
> Güncel Facebook OAuth2 kimlik doğrulama yönergeleri için bkz. [Facebook kimlik doğrulamasını yapılandırma](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>Üyelik verilerini İnceleme

**Görünüm** menüsünde **Sunucu Gezgini**' a tıklayın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

**DefaultConnection (MvcAuth)** öğesini genişletin, **Tablolar**' ı genişletin, **Aspnetusers** öğesine sağ tıklayıp **tablo verilerini göster**' e tıklayın

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers tablosu verileri](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>Kullanıcı sınıfına profil verileri ekleme

Bu bölümde, aşağıdaki görüntüde gösterildiği gibi, kayıt sırasında kullanıcı verilerine Doğum tarihi ve giriş şehir ekleyeceksiniz.

![ev Town ve bday ile Reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

*Models\ıdentitymodels.cs* dosyasını açın ve Doğum tarihi ve ev Town özellikleri ekleyin:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

*Models\accountviewmodels.cs* dosyasını açın ve `ExternalLoginConfirmationViewModel`Doğum tarihi ve giriş kasayı özelliklerini ayarlayın.

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

*Controllers\accountcontroller.cs* dosyasını açın ve şu şekilde gösterildiği gibi `ExternalLoginConfirmation` Action yöntemine Doğum tarihi ve ev Town kodu ekleyin:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

*Views\Account\ExternalLoginConfirmation.cshtml* dosyasına Doğum tarihi ve ev Town ekleyin:

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

Üyelik veritabanını silin, böylece Facebook hesabınızı uygulamanız ile kaydedebilir ve yeni Doğum tarihi ile ev kasaprofili bilgilerini ekleyebildiğinizi doğrulayabilirsiniz.

**Çözüm Gezgini**, **tüm dosyaları göster** simgesine tıklayın ve ardından *Ekle\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;. mdf* öğesine sağ tıklayın ve **Sil**' e tıklayın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu** (PMC) seçeneğine tıklayın. PMC 'de aşağıdaki komutları girin.

1. Geçişi etkinleştir
2. Geçiş geçişi Init
3. Güncelleştirme-veritabanı

Uygulamayı çalıştırın ve FaceBook ve Google kullanarak oturum açın ve bazı kullanıcıları kaydedin.

## <a name="examine-the-membership-data"></a>Üyelik verilerini İnceleme

**Görünüm** menüsünde **Sunucu Gezgini**' a tıklayın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

**Aspnetusers** öğesine sağ tıklayın ve **tablo verilerini göster**' e tıklayın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

`HomeTown` ve `BirthDate` alanları aşağıda gösterilmiştir.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>Uygulamanızı günlüğe kaydetme ve başka bir hesapla oturum açma

Uygulamanızda Facebook ile oturum açın ve ardından farklı bir Facebook hesabıyla (aynı tarayıcıyı kullanarak) yeniden oturum açmayı denerseniz, kullandığınız önceki Facebook hesabında hemen oturum açarsınız. Başka bir hesap kullanmak için Facebook 'a gitmeniz ve Facebook 'ta oturumunuzu açmanız gerekir. Aynı kural diğer 3. taraf kimlik doğrulama sağlayıcıları için de geçerlidir. Alternatif olarak, farklı bir tarayıcı kullanarak başka bir hesapla oturum açabilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar

Yahoo ve LinkedIn yönergeleri için Jerrie Pelser tarafından [OWıN Için Yahoo ve LinkedIn OAuth güvenlik sağlayıcılarının tanıtımı](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) konusuna bakın. Sosyal oturum açma düğmelerini etkinleştirmek için bkz. ASP.NET MVC 5 için Jerrie 'nin oldukça sosyal oturum açma düğmeleri.

Öğreticimi izleyin, [kimlik doğrulama ve SQL DB ile ASP.NET MVC uygulaması oluşturun ve](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)bu öğreticiyi devam eden Azure App Service için dağıtın ve şunları gösterir:

1. Uygulamanızı Azure 'a dağıtma.
2. Uygulamanızı rollerle güvenli hale getirme.
3. [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) ve [Yetkilendirme](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filtreleriyle uygulamanızın güvenliğini sağlama.
4. Kullanıcı ve rolleri eklemek için üyelik API 'sini kullanma.

Lütfen bu öğreticiyi beğentireceğiniz ve neleri iyileştireceğiz hakkında geri bildirimde bulunun. Ayrıca, [kodu nasıl kullanacağınızı göster hakkında](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)yeni konular da isteyebilirsiniz. Hatta, ASP.NET 'e eklenecek yeni özellikler isteyebilir ve oylayabilirsiniz. Örneğin, [Kullanıcı ve rolleri oluşturup yönetmek](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use) için bir araç için oy verebilirsiniz.

ASP.NET dış kimlik doğrulama hizmetlerinin nasıl çalıştığı hakkında iyi bir açıklama için bkz. Robert McMurray 'ın [dış kimlik doğrulama hizmetleri](https://asp.net/web-api/overview/security/external-authentication-services). Robert 's makalesi, Microsoft ve Twitter kimlik doğrulamasını etkinleştirme konusunda da ayrıntıya gider. Tom Dykstra 'ın mükemmel [EF/MVC öğreticisi](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Entity Framework nasıl çalışalınacağını göstermektedir.
