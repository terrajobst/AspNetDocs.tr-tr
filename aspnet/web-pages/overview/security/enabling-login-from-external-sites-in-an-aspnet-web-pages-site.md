---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: ASP.NET Web Pages (Razor) sitesindeki dış siteleri kullanarak oturum açma | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, Facebook, Google, Twitter, Yahoo ve diğer siteleri kullanarak ASP.NET Web Pages (Razor) sitesinde oturum açma ve diğer bir deyişle, nasıl destekleneceği açıklanır.
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638756"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>Bir ASP.NET Web Pages (Razor) sitesinde dış siteleri kullanarak oturum açma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, Facebook, Google, Twitter, Yahoo ve diğer siteleri kullanarak ASP.NET Web sayfaları (Razor) sitenizde oturum açma, diğer bir deyişle, sitenizdeki OAuth ve OpenID desteği açıklanmaktadır.
> 
> Öğrenecekleriniz:
> 
> - WebMatrix Başlatıcı site şablonunu kullandığınızda diğer sitelerden oturum açmayı etkinleştirme.
> 
> Bu, makalesinde sunulan ASP.NET özelliğidir:
> 
> - `OAuthWebSecurity` Yardımcısı.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - WebMatrix 3

ASP.NET Web sayfaları, [OAuth](http://oauth.net/) ve [OpenID](http://openid.net/) sağlayıcıları için destek içerir. Bu sağlayıcıları kullanarak, kullanıcıların Facebook, Twitter, Microsoft ve Google 'daki mevcut kimlik bilgilerini kullanarak sitenizde oturum açmasına izin verebilirsiniz. Örneğin, Facebook hesabı kullanarak oturum açmak için kullanıcılar yalnızca bir Facebook simgesi seçerek bunları Kullanıcı bilgilerini girdikleri Facebook oturum açma sayfasına yönlendirir. Daha sonra Facebook oturum açma bilgilerini sitenizdeki hesabıyla ilişkilendirebilirler. Web sayfaları üyelik özellikleri için ilgili geliştirmelerden bazıları, kullanıcıların Web sitenizdeki tek bir hesapla birden çok oturum açma işlemi (sosyal ağ sitelerine ait oturumlar dahil) ilişkilendirebilirler.

Bu görüntüde, bir kullanıcının bir dış hesapla oturum açmasını etkinleştirmek üzere Facebook, Twitter, Google veya Microsoft simgesini seçebildiği **Başlatıcı site** şablonundan oturum açma sayfası gösterilmektedir:

![dış sağlayıcılar](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

**Başlangıç site** şablonunda birkaç satır kod satırını kaldırarak OAuth ve OpenID üyeliğini etkinleştirebilirsiniz. OAuth ve OpenID sağlayıcılarıyla çalışmak için kullandığınız yöntemler ve Özellikler `WebMatrix.Security.OAuthWebSecurity` sınıftır. **Başlatıcı site** şablonu, bir oturum açma sayfası, bir üyelik veritabanı ve kullanıcıların sitenizde yerel kimlik bilgileri veya başka bir siteden oturum açmasını sağlamak için ihtiyacınız olan tüm kod ile tam bir üyelik altyapısı içerir.

Bu bölümde, kullanıcıların dış sitelerden **Başlatıcı site** şablonunu temel alan bir siteye oturum açmasına izin veren bir örnek verilmiştir. Bir başlangıç sitesi oluşturduktan sonra, bunu yapabilirsiniz (Ayrıntılar aşağıda):

- Bir OAuth sağlayıcısı kullanan siteler (Facebook, Twitter ve Microsoft) için dış sitede bir uygulama oluşturursunuz. Bu, bu siteler için oturum açma özelliğini çağırmak üzere ihtiyacınız olan uygulama anahtarlarını sağlar.
- OpenID sağlayıcısı (Google) kullanan siteler için, bir uygulama oluşturmanız gerekmez. Bu sitelerin tümünde, oturum açmak ve geliştirici uygulamaları oluşturmak için hesabınızın olması gerekir.

    > [!NOTE]
    > Microsoft uygulamaları, çalışan bir Web sitesi için yalnızca canlı URL 'yi kabul eder, bu nedenle oturum açma işlemleri için yerel bir Web sitesi URL 'SI kullanamazsınız.
- Uygun kimlik doğrulama sağlayıcısını belirtmek ve kullanmak istediğiniz siteye bir oturum açma göndermek için Web sitenizde birkaç dosyayı düzenleyin.

Bu makalede, aşağıdaki görevler için ayrı yönergeler sağlanmaktadır:

- [Google oturumlarını etkinleştirme](#To_enable_Google_logins)
- [Facebook oturumlarını etkinleştirme](#To_enable_Facebook_logins)
- [Twitter oturumlarını etkinleştirme](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>Google oturumlarını etkinleştirme

1. WebMatrix Başlatıcı site şablonunu temel alan bir ASP.NET Web sayfaları sitesi oluşturun veya açın.
2. *\_AppStart. cshtml* sayfasını açın ve aşağıdaki kod satırının açıklamasını kaldırın. 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>Google oturum açma testi

1. Sitenizin *default. cshtml* sayfasını çalıştırın ve **oturum aç** düğmesini seçin.
2. Oturum *açma* sayfasında, **oturum açmak için başka bir hizmet kullan** bölümünde **Google** veya **Yahoo** Gönder düğmesini seçin. Bu örnek Google oturum açma bilgilerini kullanır. 

    Web sayfası, isteği Google Login sayfasına yönlendirir.

    ![Google oturum açma](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. Mevcut bir Google hesabının kimlik bilgilerini girin.
4. Google *'ın hesaptaki bilgileri kullanmasına izin vermek* isteyip istemediğinizi sorduğunda, **izin ver**' e tıklayın.

    Kod, kullanıcının kimliğini doğrulamak için Google belirtecini kullanır ve ardından Web sitenizde bu sayfaya geri döner. Bu sayfa, kullanıcıların Google oturum açmaları Web sitenizde mevcut bir hesapla ilişkilendirmelerini sağlar veya dış oturum açma bilgilerini ile ilişkilendirmek için sitenize yeni bir hesap kaydedebilir.

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. **İlişkilendir** düğmesini seçin. Tarayıcı, uygulamanızın giriş sayfasına geri döner.

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>Facebook oturumlarını etkinleştirme

1. [Facebook geliştiricileri sitesine](https://developers.facebook.com/apps) gidin (henüz oturum açmadıysanız oturum açın).
2. Yeni uygulama **Oluştur** düğmesini seçin ve ardından yeni uygulamayı adlandırmak ve oluşturmak için istemleri izleyin.
3. **Uygulamanızın Facebook ile nasıl tümleştirileceğini seçin**bölümünde, **Web sitesi** bölümünü seçin.
4. **Site URL 'si** ALANıNı sitenizin URL 'siyle (örneğin, `http://www.example.com`) girin. **Etki alanı** alanı isteğe bağlıdır; Bu, tüm etki alanı ( *example.com*gibi) için kimlik doğrulaması sağlamak için kullanabilirsiniz. 

    > [!NOTE]
    > Yerel bilgisayarınızda `http://localhost:12345` (sayının bir yerel bağlantı noktası numarası olduğu) gibi bir URL 'yi çalıştırıyorsanız, sitenizi test etmek için bu değeri **site URL 'si** alanına ekleyebilirsiniz. Ancak, yerel sitenizin bağlantı noktası numarası değiştiğinde uygulamanızın **site URL 'si** alanını güncelleştirmeniz gerekecektir.
5. **Değişiklikleri Kaydet** düğmesini seçin.
6. **Uygulamalar** sekmesini yeniden seçin ve ardından uygulamanızın başlangıç sayfasını görüntüleyin.
7. Uygulamanızın uygulama **kimliği** ve **uygulama gizli** değerlerini kopyalayın ve bunları geçici bir metin dosyasına yapıştırın. Bu değerleri, Web sitesi kodunuzda Facebook sağlayıcısına geçitirsiniz.
8. Facebook geliştirici sitesinden çıkın.

Artık Web sitenizdeki iki sayfada değişiklikler yaparsınız. böylece kullanıcılar, Facebook hesaplarını kullanarak sitede oturum açabilirler.

1. WebMatrix Başlatıcı site şablonunu temel alan bir ASP.NET Web sayfaları sitesi oluşturun veya açın.
2. *\_AppStart. cshtml* sayfasını açın ve Facebook OAuth sağlayıcısı için kodun açıklamasını kaldırın. Açıklamalı olmayan kod bloğu aşağıdakine benzer: 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. **Uygulama kimliği** değerini, Facebook uygulamasından `appId` parametresinin değeri olarak (tırnak işaretleri içinde) kopyalayın.
4. Facebook uygulamasından **uygulama gizli** değerini `appSecret` parametre değeri olarak kopyalayın.
5. Dosyayı kaydedin ve kapatın.

### <a name="testing-facebook-login"></a>Facebook oturum açma testi

1. Sitenin *default. cshtml* sayfasını çalıştırın ve **oturum aç** düğmesini seçin.
2. *Oturum açma* sayfasında, **oturum açmak için başka bir hizmet kullan** bölümünde **Facebook** simgesini seçin. 

    Web sayfası, isteği Facebook oturum açma sayfasına yönlendirir.

    ![OAuth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. Facebook hesabında oturum açın. 

    Kod, kimliğinizi doğrulamak için Facebook belirtecini kullanır ve ardından Facebook oturum açma bilgilerinizi sitenizin oturum açmayla ilişkilendirebileceğiniz bir sayfaya geri döner. Kullanıcı adınız veya e-posta adresiniz formundaki **e-posta** alanına girilir.

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. **İlişkilendir** düğmesini seçin. 

    Tarayıcı, giriş sayfasına geri döner ve oturum açarsınız.

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>Twitter oturumlarını etkinleştirme

1. [Twitter geliştiricileri sitesine](https://dev.twitter.com/)gidin.
2. **Uygulama oluştur** bağlantısını seçin ve ardından sitede oturum açın.
3. **Uygulama oluştur** formunda **ad** ve **Açıklama** alanlarını girin.
4. **Web sitesi** alanına sitenizin URL 'sini girin (örneğin, `http://www.example.com`). 

    > [!NOTE]
    > Sitenizi yerel olarak test ediyorsanız (`http://localhost:12345`gibi bir URL kullanarak) Twitter, URL 'YI kabul etmeyebilir. Ancak, yerel geri döngü IP adresini (örneğin `http://127.0.0.1:12345`) kullanabilirsiniz. Bu, uygulamanızı yerel olarak test etme işlemini basitleştirir. Ancak, yerel sitenizin bağlantı noktası numarası her değiştiğinde uygulamanızın **Web sitesi** alanını güncelleştirmeniz gerekir.
5. **Geri arama URL 'si** alanına, Web sitenizde Twitter 'da oturum açtıktan sonra geri dönmesini istediğiniz sayfa IÇIN bir URL girin. Örneğin, kullanıcıları Başlatıcı sitesinin giriş sayfasına (oturum açma durumunu tanıyacak) göndermek için, **Web sitesi** alanına girdiğiniz aynı URL 'yi girin.
6. Koşulları kabul edin ve **Twitter uygulamanızı oluştur** düğmesini seçin.
7. **Uygulamalarım** giriş sayfasında, oluşturduğunuz uygulamayı seçin.
8. **Ayrıntılar** sekmesinde, en alta kaydırın ve **erişim belirtecinden oluştur** düğmesini seçin.
9. **Ayrıntılar** sekmesinde, uygulamanız Için **tüketici anahtarı** ve **Tüketici gizli** değerlerini kopyalayın ve bunları geçici bir metin dosyasına yapıştırın. Bu değerleri, Web sitesi kodunuzda Twitter sağlayıcısına geçireceğiz.
10. Twitter sitesinden çıkın.

Artık Web sitenizdeki iki sayfada değişiklikler yaparsınız, böylece kullanıcılar kendi Twitter hesaplarını kullanarak sitede oturum açabilirler.

1. WebMatrix Başlatıcı site şablonunu temel alan bir ASP.NET Web sayfaları sitesi oluşturun veya açın.
2. *\_AppStart. cshtml* sayfasını açın ve Twitter OAuth sağlayıcısı için kodun açıklamasını kaldırın. Açıklamalı olmayan kod bloğu şuna benzer: 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. **Kullanıcı anahtarı** değerini Twitter uygulamasından `consumerKey` parametresinin değeri olarak (tırnak işaretleri içinde) kopyalayın.
4. **Kullanıcı gizli** değerini Twitter uygulamasından `consumerSecret` parametresinin değeri olarak kopyalayın.
5. Dosyayı kaydedin ve kapatın.

### <a name="testing-twitter-login"></a>Twitter oturum açma testi

1. Sitenizin *default. cshtml* sayfasını çalıştırın ve **oturum aç** düğmesini seçin.
2. Oturum *açma* sayfasında, **oturum açmak için başka bir hizmet kullan** bölümünde **Twitter** simgesini seçin. 

    Web sayfası, oluşturduğunuz uygulama için isteği Twitter oturum açma sayfasına yönlendirir.

    ![OAuth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. Twitter hesabında oturum açın.
4. Kod, kullanıcının kimliğini doğrulamak için Twitter belirtecini kullanır ve ardından sizi, oturum açma bilgilerinizi Web sitesi hesabınızla ilişkilendirebileceğiniz bir sayfaya geri döndürür. Ad veya e-posta adresiniz, formdaki **e-posta** alanına girilir.

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. **İlişkilendir** düğmesini seçin. 

    Tarayıcı, giriş sayfasına geri döner ve oturum açarsınız.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [Site Geneline Yönelik Davranışını Özelleştirme](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ASP.NET Web sayfaları sitesine güvenlik ve üyelik ekleme](https://go.microsoft.com/fwlink/?LinkID=202904)
