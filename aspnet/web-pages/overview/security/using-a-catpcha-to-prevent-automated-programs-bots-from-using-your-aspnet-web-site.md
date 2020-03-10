---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: ASP.NET Web Razor) sitenizi kullanmalarını engellemek için CAPTCHA kullanma | Microsoft Docs
author: microsoft
description: Bu makalede otomatik programların (botlar) bir ASP.NET Web sayfalarında (Razor) görevleri gerçekleştirmesini engellemek için ReCaptcha 'nın (bir güvenlik ölçüsü) nasıl kullanılacağı açıklanmaktadır...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547049"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>Botların ASP.NET Web Razor) sitenizi kullanmasını engellemek için CAPTCHA kullanma

[Microsoft](https://github.com/microsoft) tarafından

> Bu makalede otomatik programların (botlar) bir ASP.NET Web Pages (Razor) Web sitesinde görevleri gerçekleştirmesini engellemek için ReCaptcha 'nın (güvenlik ölçüsü) nasıl kullanılacağı açıklanmaktadır.
> 
> **Şunları öğreneceksiniz:** 
> 
> - Sitenize CAPTCHA testi ekleme.
> 
> Makalesinde sunulan ASP.NET özellikleri şunlardır:
> 
> - `ReCaptcha` Yardımcısı.
> 
> > [!NOTE]
> > Bu makaledeki bilgiler, ASP.NET Web sayfaları 1,0 ve Web sayfaları 2 için geçerlidir.

## <a name="about-captchas"></a>CAPTCHAs hakkında

Sitenize herhangi bir zamanda kayıt yaptırıyorsanız veya bir ad ve URL (blog açıklaması gibi) girerseniz, sahte adların bir taşmasına sahip olabilirsiniz. Bunlar genellikle, bulabileceği her Web sitesinde URL 'Leri bırakmayı deneyen otomatik programlar (botlar) tarafından bırakılır. (Yaygın bir mosyon, ürünlerin URL 'Lerini satış için göndermenize yöneliktir.)

Kullanıcıların, ad ve sitesini kaydederken veya girdiklerinde Kullanıcı doğrulamak için bir *CAPTCHA* kullanarak, bir kullanıcının gerçek bir kişi olduğundan ve bir bilgisayar programı olmadığından emin olmanıza yardımcı olabilirsiniz. CAPTCHA, bilgisayarların ve Insanların ayrı olarak söylemek için tamamen otomatikleştirilmiş genel bir test için gelir. CAPTCHA, kullanıcıdan bir kişinin yapması kolay ancak otomatik bir programın yapması zor olan bir şey yapması istenen bir *sınama yanıt* sınamadır. En yaygın CAPTCHA türü, bazı bozuk harfler gördüğünüz ve bunları yazmaları istenen bir yerdir. (Deformasyon, botların harfleri çözmesidir.)

## <a name="adding-a-recaptcha-test"></a>ReCaptcha testi ekleme

ASP.NET sayfalarında, ReCaptcha hizmetini ([http://recaptcha.net](http://recaptcha.net)) temel alan BIR CAPTCHA testini işlemek için `ReCaptcha` yardımcısını kullanabilirsiniz. `ReCaptcha` Yardımcısı, kullanıcıların sayfa doğrulanmadan önce doğru şekilde girmesi gereken iki bozuk sözcüğün görüntüsünü görüntüler. Kullanıcı yanıtı ReCaptcha.Net hizmeti tarafından onaylanır.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Web sitenizi ReCaptcha.Net adresinden kaydedin ([http://recaptcha.net](http://recaptcha.net)). Kayıt tamamlandığında, bir ortak anahtar ve özel anahtar alırsınız.
2. Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.
3. Zaten bir *\_AppStart. cshtml* dosyanız yoksa bir Web sitesinin kök klasöründe *\_AppStart. cshtml*adlı bir dosya oluşturun.
4. Aşağıdaki `Recaptcha` Yardımcısı ayarlarını *\_AppStart. cshtml* dosyasına ekleyin: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. Kendi ortak ve özel anahtarlarınızı kullanarak `PublicKey` ve `PrivateKey` özelliklerini ayarlayın.
6. *\_AppStart. cshtml* dosyasını kaydedin ve kapatın.
7. Bir Web sitesinin kök klasöründe *reCAPTCHA. cshtml*adlı yeni bir sayfa oluşturun.
8. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. *ReCAPTCHA. cshtml* sayfasını bir tarayıcıda çalıştırın. `PrivateKey` değeri geçerliyse, sayfada ReCaptcha denetimi ve bir düğme görüntülenir. Anahtarlar *\_AppStart. html*' de küresel olarak ayarlanmamışsa sayfada bir hata görüntülenir. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. Test için kelimeleri girin. ReCaptcha testini geçirirseniz, bu etkiye bir ileti görürsünüz. Aksi takdirde bir hata iletisi görürsünüz ve ReCaptcha denetimi yeniden görüntülenir.

> [!NOTE]
> Bilgisayarınız ara sunucu kullanan bir etki alanında bulunuyorsa, *Web. config* dosyasının `defaultproxy` öğesini yapılandırmanız gerekebilir. Aşağıdaki örnek, ReCaptcha hizmetinin çalışmasını sağlamak için `defaultproxy` öğesi ile bir *Web. config* dosyası gösterir.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Web Pages siteleri için site genelinde davranışı özelleştirme](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha sitesi](https://www.google.com/recaptcha)
