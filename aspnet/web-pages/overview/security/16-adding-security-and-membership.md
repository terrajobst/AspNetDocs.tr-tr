---
uid: web-pages/overview/security/16-adding-security-and-membership
title: Bir ASP.NET Web Pages (Razor) sitesine güvenlik ve üyelik ekleme | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde, bazı sayfaların yalnızca oturum açan kişiler tarafından kullanılabilmesi için Web sitenizin güvenliğini nasıl güvence altına aldığınız gösterilmektedir. (Ayrıca, nasıl sayfa oluşturulacağını de göreceksiniz...
ms.author: riande
ms.date: 02/24/2014
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: 0be3e767a42939a3c343f6d4a730eb1d9a6b367c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628389"
---
# <a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>Bir ASP.NET Web Pages (Razor) sitesine güvenlik ve üyelik ekleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bazı sayfalardan yalnızca oturum açan kişiler için kullanılabilir olması için bir ASP.NET Web sayfaları (Razor) Web sitesinin nasıl güvenliğini sağlayabileceğiniz açıklanmaktadır. (Ayrıca, herkesin erişebileceği sayfalar oluşturmayı da göreceksiniz.)
> 
> **Şunları öğreneceksiniz:** 
> 
> - Bazı sayfalarda yalnızca üyelere erişimi sınırlayabilmeniz için kayıt sayfası ve oturum açma sayfası olan bir Web sitesi oluşturma.
> - Ortak ve yalnızca üye sayfalar oluşturma.
> - Sitenizde farklı güvenlik izinleri olan gruplar olan roller ve bir role Kullanıcı atama.
> - Otomatik programların (botların) üye hesapları oluşturmasını engellemek için CAPTCHA kullanma.
>   
> 
> Makalesinde sunulan ASP.NET özellikleri şunlardır:
> 
> - WebMatrix **Başlatıcı site** şablonu.
> - `WebSecurity` Yardımcısı ve `Roles` sınıfı.
> - `ReCaptcha` Yardımcısı.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - WebMatrix 3
> - ASP.NET Web yardımcıları kitaplığı

Web sitenizi, kullanıcıların oturum &#8212; açabilmeleri için ayarlayabilirsiniz, böylece site *üyeliği*destekler. Bu pek çok nedenden dolayı yararlı olabilir. Örneğin, sitenizde yalnızca üyeler için kullanılabilir olan sayfalar bulunabilir. Bazı durumlarda, size geri bildirim göndermek veya bir yorum bırakmak için kullanıcıların oturum açmasını isteyebilirsiniz.

Web siteniz üyeliği desteklese de, kullanıcıların sitedeki bazı sayfaları kullanmadan önce oturum açması gerekmez. Oturum açmamış kullanıcılar *Anonim Kullanıcı*olarak bilinir.

Bir Kullanıcı Web sitenize kaydedebilir ve sonra sitede oturum açabilir. Web sitesi, kullanıcıların iddia ettikleri kim olduğunu onaylamak için bir Kullanıcı adı (e-posta adresi) ve parola gerektirir. Bu işlem, oturum açma ve kullanıcının kimliğini onaylama *kimlik doğrulaması*olarak bilinir.

Güvenlik ve üyeliği farklı yollarla ayarlayabilirsiniz:

- WebMatrix kullanıyorsanız, **Başlatıcı site** şablonunu temel alan yeni bir site oluşturmak daha kolay bir yoldur. Bu şablon, güvenlik ve üyelik için zaten yapılandırılmış ve zaten bir kayıt sayfası, oturum açma sayfası ve benzeri.

    Şablon tarafından oluşturulan sitede, kullanıcıların Facebook, Google veya Twitter gibi bir dış siteyi kullanarak oturum açmasına izin vermek için bir seçenek de vardır.
- Mevcut bir siteye güvenlik eklemek istiyorsanız veya **Başlatıcı site** şablonunu kullanmak istemiyorsanız, kendi kayıt sayfanızı, oturum açma sayfanızı ve benzerlerini oluşturabilirsiniz.

Bu makalede, **Başlatıcı site** şablonunu kullanarak güvenlik ekleme &mdash; ilk seçeneğe odaklanılır. Ayrıca, kendi güvenlerinizi uygulama hakkında bazı temel bilgiler sağlar ve bunun nasıl yapılacağı hakkında daha fazla bilgi için bağlantılar sağlar. Ayrıca, ayrı bir makalede daha ayrıntılı olarak açıklanan dış oturum açma işlemlerinin nasıl etkinleştirileceği hakkında bilgiler de vardır.

## <a name="creating-website-security-using-the-starter-site-template"></a>Başlatıcı site şablonunu kullanarak Web sitesi güvenliği oluşturma

WebMatrix 'te, aşağıdakileri içeren bir Web sitesi oluşturmak için **Başlangıç site** şablonunu kullanabilirsiniz:

- Üyelerinize yönelik kullanıcı adlarını ve parolaları depolamak için kullanılan bir veritabanı.
- Anonim (yeni) Kullanıcıların kaydedebileceği bir kayıt sayfası.
- Oturum açma ve oturum kapatma sayfası.
- Parola kurtarma ve sıfırlama sayfası.

Aşağıdaki yordamda sitesini oluşturma ve yapılandırma açıklanmaktadır.

1. WebMatrix 'i başlatın ve **hızlı başlangıç** sayfasında **şablondan site**' yi seçin.
2. **Başlatıcı site** şablonunu seçin ve ardından **Tamam**' a tıklayın. WebMatrix yeni bir site oluşturur.
3. Sol bölmede **dosyalar** çalışma alanı Seçici ' ye tıklayın.
4. Web sitenizin kök klasöründe, genel ayarları içermesi için kullanılan özel bir dosya olan *\_AppStart. cshtml* dosyasını açın. `//` karakterleri kullanılarak açıklama eklenen bazı deyimleri içerir:

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    Bu deyimler, e-posta göndermek için kullanılabilen `WebMail` yardımcısını yapılandırır. Üyelik sistemi, kullanıcılar kaydolduklarında veya parolalarını değiştirmek istediklerinde onay iletileri göndermek üzere e-posta kullanabilir. (Örneğin, kullanıcılar kaydolduktan sonra kayıt işlemini bitirebilmek için tıklabilecekleri bir bağlantı içeren bir e-posta alırlar.)

    E-posta gönderme, bir [ASP.NET Web sayfaları sitesine e-posta ekleme](https://go.microsoft.com/fwlink/?LinkId=202899)bölümünde açıklandığı gıbı bir SMTP sunucusuna erişim gerektirir. E-posta ayarlarını, e-posta gönderebilen her sayfaya tekrar tekrar kodlamamaları için bu Merkezi *\_AppStart. cshtml* dosyasında depolayacaksınız. (Bir kayıt veritabanını ayarlamak için SMTP ayarlarını yapılandırmanız gerekmez; kullanıcıları e-posta diğer adından doğrulamak ve kullanıcıların unutulan bir parolayı sıfırlamasını sağlamak istiyorsanız SMTP ayarları gerekir.)
5. Her birinin önüne `//` kaldırarak deyimlerin açıklamasını kaldırın.

    E-posta onayını ayarlamak istemiyorsanız, bu adımı ve sonraki adımı atlayabilirsiniz. SMTP değerleri ayarlanmamışsa, yeni hesap onay e-postası olmadan hemen kullanılabilir.
6. Koddaki aşağıdaki e-postayla ilgili ayarları değiştirin:

   - `WebMail.SmtpServer`, erişiminiz olan SMTP sunucusunun adına ayarlayın.
   - `WebMail.EnableSsl` `true`olarak ayarlı bırakın. Bu ayar, SMTP sunucusuna, onları şifreleyerek gönderilen kimlik bilgilerini korur.
   - `WebMail.UserName`, SMTP sunucusu hesabınızın kullanıcı adına ayarlayın.
   - SMTP sunucusu hesabınızın parolasını `WebMail.Password` ayarlayın.
   - `WebMail.From` kendi e-posta adresinizi ayarlayın. Bu, iletinin gönderildiği e-posta adresidir.

     > [!NOTE] 
     > 
     > **İpucu** Bu özelliklerin değerleri hakkında daha fazla bilgi için bkz. [ASP.NET Web Pages Için site genelinde davranışı özelleştirme](https://go.microsoft.com/fwlink/?LinkID=202906)bölümünde [e-posta ayarlarını yapılandırma](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings) .
7. *AppStart. cshtml\_* kaydedin ve kapatın.
8. *Varsayılan. cshtml* sayfasını bir tarayıcıda çalıştırın.

    ![Güvenlik-üyelik-2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > Bir özelliğin `ExtendedMembershipProvider`bir örneği olması gerektiğini söyleyen bir hata görürseniz, site ASP.NET Web sayfaları üyelik sistemi (SimpleMembership) kullanmak üzere yapılandırılmamış olabilir. Bu durum bazen bir barındırma sağlayıcısının sunucusu yerel sunucunuzda farklı yapılandırılmışsa meydana gelebilir. Bu hatayı onarmak için, aşağıdaki öğeyi sitenin *Web. config* dosyasına ekleyin:
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > Bu öğeyi `<configuration>` öğesinin bir alt öğesi olarak ve `<system.web>` öğesinin bir eşi olarak ekleyin.
9. Sayfanın sağ üst köşesinde, **Kaydet** bağlantısına tıklayın. *Register. cshtml* sayfası görüntülenir.
10. Bir Kullanıcı adı ve parola girin ve ardından **Kaydet**' e tıklayın.

    ![Güvenlik-üyelik-3](16-adding-security-and-membership/_static/image2.png)

    Web sitesini **Başlatıcı site** şablonundan oluşturduğunuzda, sitenin *App\_Data* klasöründe *startersite. sdf* adlı bir veritabanı oluşturulmuştur. Kayıt sırasında kullanıcı bilgileriniz veritabanına eklenir. SMTP değerlerini ayarlarsanız, kayıt işlemi tamamlayabilmeniz için kullandığınız e-posta adresine bir ileti gönderilir.

    ![Güvenlik-üyelik-4](16-adding-security-and-membership/_static/image3.png)
11. E-posta programınıza gidin ve onay kodunuz ve site köprüsü olacak iletiyi bulun.
12. Hesabınızı etkinleştirmek için köprüye tıklayın. Onay Köprüsü bir kayıt onay sayfası açar.

    ![Güvenlik-üyelik-5](16-adding-security-and-membership/_static/image4.png)
13. **Oturum aç** bağlantısına tıklayın ve ardından kaydettiğiniz hesabı kullanarak oturum açın.

      Oturum açtıktan sonra, **oturum açma** ve **kayıt** bağlantıları bir oturum **kapatma** bağlantısıyla değiştirilmiştir. Oturum açma adınız bağlantı olarak görüntülenir. (Bağlantı, parolanızı değiştirebileceğiniz bir sayfaya gitmenizi sağlar.)

      ![Güvenlik-üyelik-6](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > Varsayılan olarak, ASP.NET Web sayfaları, kimlik bilgilerini açık metin (insan tarafından okunabilen metin olarak) olarak sunucuya gönderir. Bir üretim sitesi, sunucusuyla değiştirilen hassas bilgileri şifrelemek için güvenli HTTP ( *Güvenli Yuva Katmanı* veya SSL olarak da bilinir) kullanmalıdır. Önceki örnekte olduğu gibi `WebMail.EnableSsl=true` ayarlayarak SSL kullanarak göndermek için e-posta iletileri gerekli olabilir. SSL hakkında daha fazla bilgi için bkz. [Web Iletişimlerini güvenli hale getirme: sertifikalar, SSL ve https://](https://go.microsoft.com/fwlink/?LinkId=208660).

## <a name="additional-membership-functionality-in-the-site"></a>Sitedeki ek üyelik Işlevselliği

Siteniz, kullanıcıların hesaplarını yönetmesine imkan tanıyan diğer işlevleri içerir. Kullanıcılar şunları yapabilir:

- Parolalarını değiştirin. Oturum açtıktan sonra, Kullanıcı adına (bir bağlantı olan) tıklabilirler. Bu, bunları yeni bir parola (*Account/ChangePassword. cshtml*) oluşturabileceğiniz bir sayfaya götürür.
- Unutulan bir parolayı kurtarın. Oturum açma sayfasında, kullanıcıları bir e-posta adresi girebilecekleri bir sayfaya (*Account/ForgotPassword. cshtml*) alan bir bağlantı (**parolanızı mı unuttunuz?** ) vardır. Site, yeni bir parola (*Account/passwordreset. cshtml*) ayarlamak için tıklayabilecekleri bir e-posta iletisi gönderir.

Ayrıca, daha sonra açıklandığı gibi kullanıcıların bir dış site kullanarak da oturum açabilmenizi sağlayabilirsiniz.

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>Yalnızca üye sayfası oluşturma

Bu süre boyunca, herkes Web sitenizdeki herhangi bir sayfaya gözatabilirler. Ancak, yalnızca oturum açan kişiler (yani, Üyeler) için kullanılabilir sayfalara sahip olmak isteyebilirsiniz. ASP.NET, yalnızca oturum açmış üyeler tarafından erişilebilen sayfalar oluşturmanızı sağlar. Genellikle, anonim kullanıcılar yalnızca üye sayfasına erişmeyi denediğinde, bunları oturum açma sayfasına yönlendirirsiniz.

Bu yordamda, yalnızca oturum açmış kullanıcılar için kullanılabilir olan sayfaları içerecek bir klasör oluşturacaksınız.

1. Sitesinin kökünde yeni bir klasör oluşturun. (Şeritte, **Yeni** ' nin altındaki oka ve ardından **Yeni klasör**' i seçin.)
2. Yeni klasör *üyelerini*adlandırın.
3. *Üyeler* klasörünün içinde yeni bir sayfa oluşturun ve bunu *membersınformation. cshtml*olarak adlandırın.
4. Mevcut içeriği şu kod ve biçimlendirmeyle değiştirin:

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    Bu kod, Kullanıcı oturum açmışsa `true` döndüren `WebSecurity` nesnesinin `IsAuthenticated` özelliğini sınar. Kullanıcı oturum açmadıysa, kod, kullanıcıyı *Hesap* klasöründeki *login. cshtml* sayfasına göndermek için `Response.Redirect` çağırır.

    Yeniden yönlendirmenin URL 'SI, geçerli sayfanın yolunu ayarlamak için `Request.Url.LocalPath` kullanan `returnUrl` bir sorgu dizesi değeri içerir. Sorgu dizesindeki `returnUrl` değerini şu şekilde ayarlarsanız (ve dönüş URL 'SI bir yerel yoldaysa), oturum açma sayfası oturum açtıktan sonra kullanıcıları bu sayfaya döndürür.

    Kod ayrıca, Düzen sayfası olarak *\_SiteLayout. cshtml* sayfasını da ayarlar. (Düzen sayfaları hakkında daha fazla bilgi için bkz. [ASP.NET Web Pages sitelerinde tutarlı düzen oluşturma](https://go.microsoft.com/fwlink/?LinkId=202891).)
5. Siteyi çalıştırın. Hala oturum açtıysanız sayfanın üst kısmındaki **Oturumu Kapat** düğmesine tıklayın.
6. Tarayıcıda */members/membersınformation*sayfasını isteyin. Örneğin, URL şöyle görünebilir:

    `http://localhost:38366/Members/MembersInformation`

    (Bağlantı noktası numarası (38366) büyük olasılıkla URL 'niz içinde farklı olacaktır.)

    Oturum açmadığınızda *login. cshtml* sayfasına yönlendirilirsiniz.
7. Daha önce oluşturduğunuz hesabı kullanarak oturum açın. *Membersınformation* sayfasına geri yönlendirilirsiniz. Oturum açtığınızdan, bu kez sayfa içeriğini görürsünüz.

Birden çok sayfaya erişimin güvenliğini sağlamak için bunu yapabilirsiniz:

- Her sayfaya güvenlik denetimini ekleyin.
- Korumalı sayfaları tutan klasörde bir *\_PageStart. cshtml* sayfası oluşturun ve güvenlik denetimini buraya ekleyin. *\_PageStart. cshtml* sayfası, klasördeki tüm sayfalar için genel sayfa türü olarak davranır. Bu teknik, [ASP.NET Web sayfaları Için site genelinde davranışı özelleştirme konusunda](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access)daha ayrıntılı olarak açıklanmıştır.

## <a name="creating-security-for-groups-of-users-roles"></a>Kullanıcı grupları (roller) için güvenlik oluşturma

Sitenizin çok sayıda üyesi varsa, bir sayfa görmeinizden önce her kullanıcının iznini tek tek denetlemek verimli değildir. Bunun yerine, bireysel üyelerin ait olduğu grupları veya *rolleri*oluşturmak için kullanabilirsiniz. Ardından, izinleri role göre denetleyebilirsiniz. Bu bölümde, bir &quot;yönetici&quot; rolü oluşturacak ve ardından bu role sahip olan kullanıcılar tarafından erişilebilen bir sayfa oluşturacaksınız.

ASP.NET üyelik sistemi, rolleri destekleyecek şekilde ayarlanmıştır. Ancak, üyelik kaydı ve oturum açmanın aksine, **Başlatıcı site** şablonu rolleri yönetmenize yardımcı olan sayfalar içermez. (Rolleri yönetmek, Kullanıcı görevi yerine bir yönetim görevidir.) Ancak, WebMatrix 'teki üyelik veritabanına doğrudan gruplar ekleyebilirsiniz.

1. WebMatrix 'te **veritabanları** çalışma alanı seçicisine tıklayın.
2. Sol bölmede, *Startersite. sdf* düğümünü açın, **Tablolar** düğümünü açın ve ardından *Web sayfaları\_roller* tablosuna çift tıklayın.

    ![Güvenlik-üyelik-7](16-adding-security-and-membership/_static/image6.png)
3. &quot;admin&quot;adlı bir rol ekleyin. *RoleID* alanı otomatik olarak doldurulur. (Birincil anahtardır ve [ASP.NET Web sayfaları sitelerinde bir veritabanıyla çalışmaya giriş](https://go.microsoft.com/fwlink/?LinkId=202893)bölümünde açıklandığı gibi bir belirleme alanı olarak ayarlanmıştır.)
4. *RoleID* alanı için değerin ne olduğunu bir yere göz atın. (Bu, tanımladığınız ilk rollükdür, 1 olur.)

    ![Güvenlik-üyelik-8](16-adding-security-and-membership/_static/image7.png)
5. *Web sayfası\_rolleri* tablosunu kapatın.
6. *USERPROFILE* tablosunu açın.
7. Tablodaki bir veya daha fazla kullanıcının Kullanıcı *kimliği* değerini bir yere ve ardından tabloyu kapatmaya dikkat edin.
8. *Web sayfalarını\_Userınroles* tablosunu açın ve tabloya bir *UserID* ve *RoleID* değeri girin. Örneğin, Kullanıcı 2 ' yi &quot;yönetici&quot; rolüne koymak için şu değerleri girersiniz:

    ![Güvenlik-üyelik-9](16-adding-security-and-membership/_static/image8.png)
9. *Web sayfalarını\_Usersınroles* tablosunu kapatın.

    Artık rollere sahip olduğunuza göre, bu roldeki kullanıcılar tarafından erişilebilen bir sayfa yapılandırabilirsiniz.
10. Web sitesi kök klasöründe, *Adminerror. cshtml* adlı yeni bir sayfa oluşturun ve var olan içeriği aşağıdaki kodla değiştirin. Bu, kullanıcıların bir sayfaya erişimine izin verilmediği durumlarda yeniden yönlendirileceği sayfa olacaktır.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. Web sitesi kök klasöründe, *Adminonly. cshtml* adlı yeni bir sayfa oluşturun ve mevcut kodu şu kodla değiştirin:

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    `Roles.IsUserInRole` yöntemi, geçerli kullanıcı belirtilen rolün üyesiyse (Bu durumda "Yönetici" rolü) `true` döndürür.
12. *Varsayılan. cshtml* 'yi bir tarayıcıda çalıştırın, ancak oturum açın. (Zaten oturum açtıysanız, oturumunuzu açın.)
13. Tarayıcının adres çubuğunda, URL 'ye *yalnızca adminadd* . (Başka bir deyişle, *Adminonly. cshtml* dosyasını isteyin.) Şu anda &quot;yönetici&quot; rolünde bir kullanıcı olarak oturum açmadığınızı, *Adminerror. cshtml* sayfasına yönlendirilirsiniz.
14. *Default. cshtml* ' ye dönün ve &quot;yönetici&quot; rolüne eklediğiniz kullanıcı olarak oturum açın.
15. *Adminonly. cshtml* sayfasına gidin. Bu kez sayfayı görürsünüz.

## <a name="preventing-automated-programs-from-joining-your-website"></a>Otomatikleştirilmiş programların Web sitenize katılmasını önlemek

Oturum açma sayfası otomatik programları (bazen *Web robots* veya *botları*olarak adlandırılır) Web siteniz ile Kaydolmayacak şekilde durdurmaz. Bu yordamda, kayıt sayfası için bir ReCaptcha testinin nasıl etkinleştirileceği açıklanmaktadır.

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. Web sitenizi ReCaptcha.Net adresinden kaydedin ([http://recaptcha.net](http://recaptcha.net)). Kayıt tamamlandığında, bir ortak anahtar ve özel anahtar alırsınız.
2. Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.
3. *Hesap* klasöründe, *register. cshtml*adlı dosyayı açın.
4. Sayfanın üst kısmındaki kodda aşağıdaki satırları bulun ve `//` açıklama karakterlerini kaldırarak açıklamaları kaldırın:

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. `PRIVATE_KEY` kendi ReCaptcha özel anahtarınızla değiştirin.
6. Sayfanın biçimlendirmesinde, `@*` kaldırın ve sayfa biçimlendirmesinde aşağıdaki satırların etrafına `*@` yorum yapın:

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. `PUBLIC_KEY` anahtarını anahtarınızla değiştirin.
8. Henüz kaldırmadıysanız, "CAPTCHA doğrulamasını etkinleştirmek Için..." ile başlayan metin içeren `<div>` öğesini kaldırın. (Tüm `<div>` öğesini ve içeriğini kaldırın.)

9. *Varsayılan. cshtml* 'yi bir tarayıcıda çalıştırın. Sitede oturum açtıysanız, **oturum kapatma** bağlantısına tıklayın.
10. **Kayıt bağlantısına tıklayın** ve CAPTCHA testini kullanarak kaydı test edin.

     ![Güvenlik-üyelik-10](16-adding-security-and-membership/_static/image9.png)

`ReCaptcha` Yardımcısı hakkında daha fazla bilgi için bkz. [BIR CATPCHA kullanarak otomatik programların (botların) ASP.NET Web sitenizi kullanmasını engelleyin](https://go.microsoft.com/fwlink/?LinkId=251967).

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>Dış site kullanarak kullanıcıların oturum açmasına izin verme

**Başlatıcı site** şablonu, kullanıcıların Facebook, Windows Live, Twitter, Google veya Yahoo kullanarak oturum açmasına izin veren kod ve biçimlendirmeyi içerir. Bu işlev varsayılan olarak etkin değildir. Bu dış sağlayıcıları kullanarak kullanıcıların oturum açmasına izin verme kullanımı için genel yordam bu şekilde belirlenir:

- Hangi dış sitelerden desteklemek istediğinize karar verin.
- Gerekirse, bu siteye gidin ve bir oturum açma uygulaması ayarlayın. (Örneğin, Facebook oturumlarına izin vermek için bunu yapmanız gerekir.)
- Sitenizde sağlayıcıyı yapılandırın. Çoğu durumda, *\_AppStart. cshtml* dosyasındaki bazı kodların açıklamalarını oluşturmanız yeterlidir.
- Kayıt sayfasına, kullanıcıların oturum açmak için dış siteye bağlantı eklemesini sağlayan biçimlendirme ekleyin. Genellikle gereken biçimlendirmeyi kopyalayabilir ve metni biraz değiştirebilirsiniz.

[Bir ASP.NET Web Pages sitesindeki dış sitelerden oturum açmayı etkinleştirme](https://go.microsoft.com/fwlink/?LinkId=251969)konusunda adım adım yönergeleri bulabilirsiniz.

Kullanıcı başka bir siteden oturum açtıktan sonra, kullanıcı sitenize geri döner ve bu oturum açma bilgilerini siteyle *ilişkilendirir* . Aslında bu, sitenizde kullanıcının dış oturum açması için bir Üyelik girişi oluşturur. Bu, dış oturum açma ile üyelik (roller gibi) için normal tesislerini kullanmanıza olanak sağlar.

## <a name="adding-security-to-an-existing-website"></a>Mevcut bir Web sitesine güvenlik ekleme

Bu makalede daha önce bahsedilen yordam, Web sitesi güvenliğinin temeli olarak **Başlatıcı site** şablonunu kullanmaya dayanır. Başlangıç **sitesi** şablonundan başlayabilmeniz veya ilgili sayfaları bu şablona dayalı bir siteden kopyalamak için pratik değilse, kendi sitenizde aynı güvenlik türünü kendiniz kodlayarak uygulayabilirsiniz. Aynı sayfa türlerini (kayıt, oturum açma vb.) oluşturun ve ardından üyeliği ayarlamak için yardımcıları ve sınıfları kullanın.

Temel işlem, [ASP.net Razor güvenliği uygulamak için en temel yol](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)gönderisine Web günlüğünde açıklanmıştır. İşin çoğu, `WebSecurity` Yardımcısı 'nın aşağıdaki yöntemleri ve özellikleri kullanılarak yapılır:

- [Websecurty. UserExists](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx), [WebSecurity. CreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx). Bu yöntemler, birisinin zaten kayıtlı olup olmadığını ve bunları kaydetmenizi belirlemenizi sağlar.
- [Websecurty. IsAuthenticated](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx). Bu özellik geçerli kullanıcının oturum açıp açmamadığını belirlemenizi sağlar. Bu, kullanıcıları oturum açmadıysa oturum açma sayfasına yeniden yönlendirmek için kullanışlıdır.
- [WebSecurity. Login](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx), [WebSecurity. Logout](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx). Bu yöntemler bir kullanıcıyı oturum açıp günlüğe kaydeder.
- [WebSecurity. CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx). Bu özellik geçerli kullanıcının oturum açma adını (Kullanıcı oturum açtıysa) görüntülemek için yararlıdır.
- [WebSecurity. ConfirmAccount](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx). Bu yöntem, kayıt için e-posta onayını ayarlarsanız yararlı olur. (Ayrıntılar, blog gönderisine [ASP.NET Web sayfaları güvenliği için onay özelliğini kullanarak](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)açıklanmaktadır.)

Rolleri yönetmek için, blog girişinde açıklandığı gibi [rolleri](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx) ve [Üyelik](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx) sınıflarını kullanabilirsiniz.

## <a name="additional-resources"></a>Ek Kaynaklar

- [Site Geneline Yönelik Davranışını Özelleştirme](https://go.microsoft.com/fwlink/?LinkId=202906)
- [Web Iletişimlerinin güvenliğini sağlama: sertifikalar, SSL ve https://](https://go.microsoft.com/fwlink/?LinkId=208660)
- [ASP.net Razor güvenliği uygulamak için en temel yol](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240) ve [ASP.NET Web sayfaları güvenliği Için onay özelliğini kullanma](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267). Bunlar, ASP.NET üyelik özelliklerinin **Başlatıcı site** şablonunu kullanmadan nasıl uygulanacağını açıklayan blog postalardır.
- [Bir ASP.NET Web Sayfaları Sitesinde Dış Sitelerden Oturum Açmayı Etkinleştirme](https://go.microsoft.com/fwlink/?LinkId=251969)
- [WebSecurity Class API başvurusu](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99)) (MSDN)
- [Simpleleroleprovider sınıfı API başvurusu](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99)) (MSDN)
- [Simplelemembershipprovider sınıfı API başvurusu](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99)) (MSDN)
