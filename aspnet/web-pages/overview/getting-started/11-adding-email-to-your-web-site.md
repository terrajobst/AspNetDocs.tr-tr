---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: ASP.NET Web Pages (Razor) sitesinden e-posta gönderme | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde, bir Web sitesinden otomatikleştirilmiş bir e-posta iletisinin nasıl gönderileceği açıklanmaktadır.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 23e9717329525fb5a0ed505c9dc94505d4f9dbbe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634717"
---
# <a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>ASP.NET Web Pages (Razor) sitesinden e-posta gönderme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, ASP.NET Web Pages (Razor) kullandığınızda bir Web sitesinden e-posta iletisinin nasıl gönderileceği açıklanır.
> 
> Öğrenecekleriniz:
> 
> - Web siteinizden bir e-posta iletisi gönderme.
> - Bir e-posta iletisine dosya iliştirme.
> 
> Bu, makalesinde sunulan ASP.NET özelliğidir:
> 
> - `WebMail` Yardımcısı.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>Web sitenizdeki e-posta Iletileri gönderme

Web siteinizden e-posta göndermeniz gerekebilecek bazı nedenler vardır. Kullanıcılara onay iletileri gönderebilir veya bildirimleri kendinize gönderebilirsiniz (örneğin, yeni bir kullanıcının kaydoldığına). `WebMail` Yardımcısı, e-posta göndermenizi kolaylaştırır.

`WebMail` Yardımcısını kullanmak için bir SMTP sunucusuna erişiminizin olması gerekir. (SMTP, *Basit Posta Aktarım Protokolü*için temsil eder.) SMTP sunucusu, yalnızca iletileri alıcının sunucusuna &#8212; ileten e-postanın giden tarafı olan bir e-posta sunucusudur. Web siteniz için bir barındırma sağlayıcısı kullanırsanız, büyük olasılıkla e-posta ile sizin de sizin SMTP sunucusu adınızın ne olduğunu söyleyebilir. Bir şirket ağı içinde çalışıyorsanız, bir yönetici veya BT departmanınız genellikle kullanabileceğiniz bir SMTP sunucusu hakkında bilgi sağlayabilir. Evde çalışıyorsanız, normal e-posta sağlayıcınızı kullanarak, SMTP sunucusunun adını size bildirebilen bile test edebilirsiniz. Genellikle şunlar gerekir:

- SMTP sunucusunun adı.
- Bağlantı noktası numarası. Bu neredeyse her zaman 25 ' tir. Ancak, ISS 'niz 587 numaralı bağlantı noktasını kullanmanızı gerektirebilir. E-posta için Güvenli Yuva Katmanı (SSL) kullanıyorsanız, farklı bir bağlantı noktası gerekebilir. E-posta sağlayıcınıza danışın.
- Kimlik bilgileri (Kullanıcı adı, parola).

Bu yordamda iki sayfa oluşturacaksınız. İlk sayfa, kullanıcıların teknik destek formu doldurulmiş gibi bir açıklama girmelerini sağlayan bir form içerir. İlk sayfa, bilgilerini ikinci bir sayfaya gönderir. İkinci sayfada, kod kullanıcının bilgilerini ayıklar ve bir e-posta iletisi gönderir. Ayrıca, sorun raporunun alındığını onaylayan bir ileti görüntüler.

![görüntüyle](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> Bu örneği basit tutmak için, kod `WebMail` Yardımcısı 'nı kullandığınız sayfada başlatır. Bununla birlikte, gerçek web siteleri için, Web sitenizdeki tüm dosyalar için `WebMail` Yardımcısı 'nı başlatmak üzere başlatma kodunu genel bir dosyaya yerleştirmek daha iyi bir fikirdir. Daha fazla bilgi için bkz. [ASP.NET Web Pages Için site genelinde davranışı özelleştirme](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).

1. Yeni bir Web sitesi oluşturun.
2. *Emailrequest. cshtml* adlı yeni bir sayfa ekleyin ve aşağıdaki biçimlendirmeyi ekleyin: 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    Form öğesinin `action` özniteliğinin *ProcessRequest. cshtml*olarak ayarlandığını unutmayın. Bu, formun geçerli sayfaya geri dönmek yerine bu sayfaya gönderildiği anlamına gelir.
3. Web sitesine *ProcessRequest. cshtml* adlı yeni bir sayfa ekleyin ve aşağıdaki kodu ve biçimlendirmeyi ekleyin:   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    Kodda, sayfaya gönderilen form alanlarının değerlerini alırsınız. Sonra, e-posta iletisini oluşturmak ve göndermek için `WebMail` Yardımcısı 'nın `Send` yöntemini çağırabilirsiniz. Bu durumda, kullanılacak değerler formdan gönderilen değerlerle birlikte birleştirdiğiniz metinden oluşur.

    Bu sayfanın kodu bir `try/catch` bloğu içindedir. Herhangi bir nedenle e-posta gönderme girişimi işe yaramazsa (örneğin, ayarlar doğru değilse) `catch` bloğundaki kod çalışır ve `errorMessage` değişkenini oluşan hata olarak ayarlar. (`try/catch` blokları veya `<text>` etiketi hakkında daha fazla bilgi için bkz. [Razor sözdizimini kullanarak ASP.NET Web sayfalarına giriş programlama](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)

    Sayfanın gövdesinde, `errorMessage` değişkeni boşsa (varsayılan), kullanıcı e-posta iletisinin gönderildiğini belirten bir ileti görür. `errorMessage` değişkeni true olarak ayarlanırsa, kullanıcı iletiyi gönderirken bir sorun olduğunu belirten bir ileti görür.

    Sayfanın bir hata iletisi görüntüleyen bölümünde ek bir test olduğunu görürsünüz: `if(debuggingFlag)`. Bu, e-posta gönderirken sorun yaşıyorsanız true olarak ayarlayabileceğiniz bir değişkendir. `debuggingFlag` true olduğunda ve e-posta gönderilirken bir sorun oluşursa, e-posta iletisini göndermeye çalıştığında rapor edilen ASP.NET gösteren ek bir hata iletisi görüntülenir. Orta uyarı, ancak: e-posta iletisi gönderemediği zaman ASP.NET raporlayan hata iletileri genel olabilir. Örneğin, ASP.NET SMTP sunucusuyla iletişim kuramadığı takdirde (örneğin, sunucu adında bir hata yaptıysanız), hata `Failure sending mail`.

    > [!NOTE] 
    > 
    > **Önemli** Bir özel durum nesnesinden hata iletisi aldığınızda (koddaki`ex`), bu iletiyi *kullanıcılara düzenli olarak iletmeyin.* Özel durum nesneleri genellikle kullanıcıların görmeme ve güvenlik açığı bile olabilecek bilgiler içerir. Bu nedenle bu kod, hata iletisini göstermek için anahtar olarak kullanılan `debuggingFlag` değişkenini ve varsayılan olarak değişkenin false olarak ayarlandığını içerir. Bu değişkeni true olarak ayarlamanız gerekir (Bu nedenle, *yalnızca* e-posta gönderilirken bir sorun yaşıyorsanız ve hata ayıklaması yapmanız gerekiyorsa, hata iletisini görüntüleriz). Sorunları düzelttikten sonra, `debuggingFlag` tekrar false olarak ayarlayın.

    Koddaki aşağıdaki e-posta ile ilgili ayarları değiştirin:

   - `your-SMTP-host`, erişiminiz olan SMTP sunucusunun adına ayarlayın.
   - `your-user-name-here`, SMTP sunucusu hesabınızın kullanıcı adına ayarlayın.
   - SMTP sunucusu hesabınızın parolasını `your-account-password` ayarlayın.
   - `your-email-address-here` kendi e-posta adresinizi ayarlayın. Bu, iletinin gönderildiği e-posta adresidir. (Bazı e-posta sağlayıcıları farklı bir `From` adresi belirtmenize izin vermez ve Kullanıcı adınızı `From` adresi olarak kullanır.)

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>E-posta ayarlarını yapılandırma
     > 
     > Bu, bazen SMTP sunucusu, bağlantı noktası numarası gibi doğru ayarlara sahip olduğunuzdan emin olmak için bir sorun olabilir. İşte birkaç ipucu:
     > 
     > - SMTP sunucusu adı genellikle `smtp.provider.com` veya `smtp.provider.net`gibi bir şeydir. Ancak, sitenizi bir barındırma sağlayıcısına yayımlarsanız, söz konusu noktada SMTP sunucu adı `localhost`olabilir. Bunun nedeni, yayımladıktan ve sitenizin sağlayıcının sunucusunda çalışıyor olması nedeniyle, e-posta sunucusu uygulamanızın perspektifinden yerel olabilir. Sunucu adlarında bu değişiklik, yayımlama işleminizin bir parçası olarak SMTP sunucu adını değiştirmeniz gerektiği anlamına gelebilir.
     > - Bağlantı noktası numarası genellikle 25 ' tir. Ancak, bazı sağlayıcılar bağlantı noktası 587 ' yı veya başka bir bağlantı noktasını kullanmanızı gerektirir.
     > - Doğru kimlik bilgilerini kullandığınızdan emin olun. Sitenizi bir barındırma sağlayıcısına yayımladıysanız, sağlayıcının özel olarak belirttiği kimlik bilgilerini e-posta için kullanın. Bunlar, yayımlamak için kullandığınız kimlik bilgilerinden farklı olabilir.
     > - Bazen kimlik bilgilerine gerek kalmaz. Kişisel ISS 'nizi kullanarak e-posta gönderiyorsanız, e-posta sağlayıcınız kimlik bilgilerinizi zaten bilir. Yayımladıktan sonra, yerel bilgisayarınızda sınama yaparken farklı kimlik bilgileri kullanmanız gerekebilir.
     > - E-posta sağlayıcınız şifrelemeyi kullanıyorsa, `WebMail.EnableSsl` `true`ayarlamanız gerekir.
4. Bir tarayıcıda *Emailrequest. cshtml* sayfasını çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.)
5. Adınızı ve sorun açıklamasını girip **Gönder** düğmesine tıklayın. Size iletinizi onaylayan ve size bir e-posta iletisi gönderen *ProcessRequest. cshtml* sayfasına yönlendirilirsiniz. 

    ![görüntüyle](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>Bir dosyayı e-posta Ile gönderme

Ayrıca, e-posta iletilerine eklenen dosyaları da gönderebilirsiniz. Bu yordamda, bir metin dosyası ve iki HTML sayfası oluşturacaksınız. Metin dosyasını bir e-posta eki olarak kullanacaksınız.

1. Web sitesinde, yeni bir metin dosyası ekleyin ve dosyayı *Dosyam. txt*olarak adlandırın.
2. Aşağıdaki metni kopyalayın ve dosyaya yapıştırın: 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. *SendFile. cshtml* adlı bir sayfa oluşturun ve aşağıdaki biçimlendirmeyi ekleyin: 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. *ProcessFile. cshtml* adlı bir sayfa oluşturun ve aşağıdaki biçimlendirmeyi ekleyin: 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. Örnekteki kodda ilgili aşağıdaki e-posta ayarlarını değiştirin:

    - `your-SMTP-host`, erişiminiz olan bir SMTP sunucusunun adına ayarlayın.
    - `your-user-name-here`, SMTP sunucusu hesabınızın kullanıcı adına ayarlayın.
    - `your-email-address-here` kendi e-posta adresinizi ayarlayın. Bu, iletinin gönderildiği e-posta adresidir.
    - SMTP sunucusu hesabınızın parolasını `your-account-password` ayarlayın.
    - `target-email-address-here` kendi e-posta adresinizi ayarlayın. (Önceki gibi, normalde başka birine e-posta gönderirsiniz, ancak test için kendinize gönderebilirsiniz.)
6. *SendFile. cshtml* sayfasını bir tarayıcıda çalıştırın.
7. Adınızı, konu satırını ve iliştirilecek metin dosyasının adını (*Dosyam. txt*) girin.
8. `Submit` düğmesine tıklayın. Daha önce olduğu gibi, iletinizi onaylayan ve size ekli dosyayı içeren bir e-posta iletisi gönderen *ProcessFile. cshtml* sayfasına yönlendirilirsiniz.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Web Sayfaları (Razor) Sorun Giderme Kılavuzu](https://go.microsoft.com/fwlink/?LinkId=253001)
- [Basit Posta Aktarım Protokolü](https://msdn.microsoft.com/library/aa480435.aspx)
- [ASP.NET Web sayfaları için site genelinde davranışı özelleştirme](https://go.microsoft.com/fwlink/?LinkId=202906)
