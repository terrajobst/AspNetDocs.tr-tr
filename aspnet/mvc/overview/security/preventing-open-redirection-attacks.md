---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: Açık yeniden yönlendirme saldırılarını önlerC#() | Microsoft Docs
author: jongalloway
description: Bu öğreticide, ASP.NET MVC uygulamalarınızda açık yeniden yönlendirme saldırılarını nasıl engelleyebileceğiniz açıklanır. Bu öğreticide yapılan değişiklikler anlatılmaktadır...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538173"
---
# <a name="preventing-open-redirection-attacks-c"></a>Açık Yeniden Yönlendirme Saldırılarını Önleme (C#)

[Jon Galloway](https://github.com/jongalloway) tarafından

> Bu öğreticide, ASP.NET MVC uygulamalarınızda açık yeniden yönlendirme saldırılarını nasıl engelleyebileceğiniz açıklanır. Bu öğreticide, ASP.NET MVC 3 ' teki AccountController 'da yapılmış değişiklikler ele alınmaktadır ve bu değişiklikleri var olan ASP.NET MVC 1,0 ve 2 uygulamalarınıza nasıl uygulayabileceğinizi gösterir.

## <a name="what-is-an-open-redirection-attack"></a>Açık yeniden yönlendirme saldırısı nedir?

QueryString veya form verileri gibi istek aracılığıyla belirtilen bir URL 'ye yeniden yönlendiren herhangi bir Web uygulaması, kullanıcıları harici, kötü amaçlı bir URL 'ye yönlendirmek için ile oynanmış olabilir. Bu değişikliklere açık yeniden yönlendirme saldırısı denir.

Uygulamanızın mantığı belirtilen bir URL 'ye yeniden yönlendirdiğinde, yeniden yönlendirme URL 'sinin değiştirilmediğini doğrulamanız gerekir. Hem ASP.NET MVC 1,0 hem de ASP.NET MVC 2 için varsayılan AccountController 'da kullanılan oturum açma yeniden yönlendirme saldırılarına karşı savunmasızdır. Neyse ki, ASP.NET MVC 3 önizlemesindeki düzeltmeleri kullanmak için mevcut uygulamalarınızı güncelleştirmek kolaydır.

Güvenlik açığını anlamak için, varsayılan ASP.NET MVC 2 Web uygulaması projesinde oturum açmanın nasıl çalıştığına bakalım. Bu uygulamada, [Yetkilendir] özniteliğine sahip bir denetleyici eylemi ziyaret edilmeye çalışılması yetkisiz kullanıcıları/Account/LogOn görünümüne yönlendirir. Bu/Account/LogOn öğesine yeniden yönlendirme, kullanıcının başarıyla oturum açtıktan sonra ilk olarak istenen URL 'ye dönebilmesi için bir returnUrl QueryString parametresi içerir.

Aşağıdaki ekran görüntüsünde, oturum açmamadığında/Account/ChangePassword görünümüne erişme denemesinin,/Account/LogOn ' a yeniden yönlendirmeye neden olduğunu görebiliriz? ReturnUrl =% 2fAccount% 2fChangePassword% 2F.

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**Şekil 01**: açık bir yeniden yönlendirme ile oturum açma sayfası

ReturnUrl QueryString parametresi doğrulanmamış olduğundan, bir saldırgan, bir açık yeniden yönlendirme saldırısı gerçekleştirmek üzere parametreye herhangi bir URL adresi eklemek için bunu değiştirebilir. Bunu göstermek için, ReturnUrl parametresini [http://bing.com](http://bing.com)olarak değiştirebiliriz. bu nedenle, sonuçta elde edilen oturum açma URL 'si/Account/LogOn olacaktır. ReturnUrl =<http://www.bing.com/>. Sitede başarıyla oturum açtıktan sonra [http://bing.com](http://bing.com)'a yönlendirilirsiniz. Bu yeniden yönlendirme doğrulanmaz, bunun yerine kullanıcıyı ikna eden bir kötü amaçlı siteyi işaret edebilir.

### <a name="a-more-complex-open-redirection-attack"></a>Daha karmaşık bir açık yeniden yönlendirme saldırısı

Açık yeniden yönlendirme saldırıları özellikle tehlikelidir çünkü bir saldırgan, belirli bir Web sitesinde oturum açmaya çalıştığımız bir [kimlik avı saldırısından](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)etkilenmenizi sağlar. Örneğin, bir saldırgan, parolalarını yakalama girişiminde Web sitesi kullanıcılarına kötü amaçlı e-postalar gönderebilir. Bu, Nerdakşam yemeği sitesinde nasıl çalıştığınızın bir bakalım. (Canlı Nerdakşam yemeği sitesinin açık yeniden yönlendirme saldırılarına karşı koruma için güncelleştirildiğini unutmayın.)

İlk olarak bir saldırgan, sahte sayfasına yeniden yönlendirme içeren Nerdakşam yemeği ' de oturum açma sayfasına bir bağlantı gönderir:

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

Dönüş URL 'sinin nerddiner.com 'e işaret ettiğini ve bu akşam yemeği sözcüğünün "n" eksik olduğunu unutmayın. Bu örnekte, bu, saldırganın denetlediği bir etki alanıdır. Yukarıdaki bağlantıya erişirken, meşru NerdDinner.com oturum açma sayfasına yönlendirilirsiniz.

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**Şekil 02**: açık bir yeniden yönlendirme ile nerdakşam yemeği oturum açma sayfası

Doğru oturum açdığımızda, ASP.NET MVC AccountController 'ın oturum açma eylemi, bizurl QueryString parametresinde belirtilen URL 'ye yeniden yönlendirir. Bu durumda, saldırganın girdiği, [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)bir URL 'dir. Son derece watchful, özellikle de saldırgan, sahte sayfasının meşru oturum açma sayfasına benzer şekilde göründüğünden emin olma konusunda dikkatli oluyoruz. Bu oturum açma sayfası, yeniden oturum açdığımızda bir hata iletisi içerir. Clumsy US, parolamız yanlış olmalıdır.

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**Şekil 03**: sahte Nerdakşam yemeği oturum açma ekranı

Kullanıcı adı ve parolamı yeniden yazdığımızda, sahte oturum açma sayfası bilgileri kaydeder ve bize yasal NerdDinner.com sitesine geri gönderir. Bu noktada, NerdDinner.com sitesinin kimliği zaten doğrulanır, bu nedenle sahte oturum açma sayfası doğrudan bu sayfaya yeniden yönlendirebilir. Nihai sonuç, saldırganın Kullanıcı adı ve parola sağlamasıdır ve kendisine sağladığımız farkında değildir.

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>AccountController oturum açma eyleminde güvenlik açığı bulunan koda bakıyor

ASP.NET MVC 2 uygulamasındaki oturum açma eyleminin kodu aşağıda gösterilmiştir. Başarılı bir oturum açma işlemi sırasında, denetleyicinin returnUrl 'ye bir yeniden yönlendirme döndürdüğünden emin olmanız gerektiğini unutmayın. ReturnUrl parametresine karşı hiçbir doğrulamanın gerçekleştirilmediğini görebilirsiniz.

**Listeleme 1 – ASP.NET MVC 2 oturum açma eylemi `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

Şimdi ASP.NET MVC 3 oturum açma eyleminde yapılan değişikliklere göz atalım. Bu kod, System. Web. Mvc. URL yardımcı sınıfında `IsLocalUrl()`adlı yeni bir yöntem çağırarak returnUrl parametresini doğrulamak üzere değiştirilmiştir.

**Listeleme 2 – ASP.NET MVC 3 oturum açma eylemi `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

Bu, return URL parametresini doğrulamak üzere değiştirilmiştir. Web. Mvc. URL yardımcı sınıfında yeni bir yöntemi çağırarak, `IsLocalUrl()`.

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>ASP.NET MVC 1,0 ve MVC 2 uygulamalarınızı koruma

Ilocalurl () yardımcı yöntemini ekleyerek ve returnUrl parametresini doğrulamak üzere oturum açma eylemini güncelleştirerek var olan ASP.NET MVC 1,0 ve 2 uygulamalarımızda ASP.NET MVC 3 değişikliklerinden faydalanabilir.

URL Yardımcısı IsLocalUrl () yöntemi aslında yalnızca System. Web. Web sayfalarındaki bir yönteme çağrı yaparak bu doğrulama, ASP.NET Web sayfaları uygulamaları tarafından da kullanılır.

**Listeleme 3 – ASP.NET MVC 3 UrlHelper `class` ıslocalurl () yöntemi**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

Iurllocaltohost yöntemi, liste 4 ' te gösterildiği gibi gerçek doğrulama mantığını içerir.

**System. Web. Web sayfası Requesısesions sınıfından 4 – ısurllocaltohost () yöntemini listeleme**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

ASP.NET MVC 1,0 veya 2 uygulamamızda, AccountController 'a bir ılocalurl () yöntemi ekleyeceğiz, ancak mümkünse onu ayrı bir yardımcı sınıfa eklemeniz önerilir. Ilocalurl () ASP.NET MVC 3 sürümünde AccountController içinde çalışacak şekilde iki küçük değişiklik yapacağız. İlk olarak, denetleyicilerde ortak metotların denetleyici eylemleri olarak erişilebilir olduğundan, bunu bir genel yöntemden özel bir yönteme değiştireceksiniz. İkincisi, URL konağını uygulama konağına göre denetleyen çağrıyı değiştireceksiniz. Bu çağrı UrlHelper sınıfında yerel bir RequestContext alanını kullanır. Bunu kullanmak yerine. RequestContext. HttpContext. Request. URL. Host, bunu kullanacağız. İstek. URL. Host. Aşağıdaki kod, ASP.NET MVC 1,0 ve 2 uygulamalarında bir Controller sınıfıyla birlikte kullanılacak olan Modified ılocalurl () yöntemini gösterir.

**Kod 5 – IsLocalUrl () yöntemi, MVC denetleyici sınıfıyla kullanılmak üzere değiştirilmiştir**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

Artık ıslocalurl () yöntemi olduğuna göre, aşağıdaki kodda gösterildiği gibi returnUrl parametresini doğrulamak için oturum açma eylemmizden bu işlemi çağırabiliriz.

**Listeleme 6 – returnUrl parametresini doğrulayan, güncelleştirilmiş oturum açma yöntemi**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

Artık bir dış dönüş URL 'SI kullanarak oturum açmaya çalışırken açık bir yeniden yönlendirme saldırısı test eteceğiz. /Account/LogOn komutunu kullanalım. ReturnUrl = yeniden<http://www.bing.com/>.

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**Şekil 04**: güncelleştirilmiş oturum açma eylemini test etme

Başarıyla oturum açtıktan sonra dış URL yerine giriş/Dizin denetleyicisi eylemine yönlendirilirsiniz.

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**Şekil 05**: açık yeniden yönlendirme saldırısı Ertelenen

## <a name="summary"></a>Özet

Yeniden yönlendirme URL 'Leri bir uygulamanın URL 'sinde parametre olarak geçirildiğinde, açık yeniden yönlendirme saldırıları gerçekleşebilir. ASP.NET MVC 3 şablonu, açık yeniden yönlendirme saldırılarına karşı korumaya yönelik kodu içerir. Bu kodu, ASP.NET MVC 1,0 ve 2 uygulamalarında bazı değişikliklerle ekleyebilirsiniz. ASP.NET 1,0 ve 2 uygulamalarında oturum açarken açık yeniden yönlendirme saldırılarına karşı koruma sağlamak için bir IsLocalUrl () yöntemi ekleyin ve oturum açma eyleminde returnUrl parametresini doğrulayın.
