---
uid: web-api/overview/security/external-authentication-services
title: ASP.NET Web API 'SI (C#) Ile dış kimlik doğrulama hizmetleri Microsoft Docs
author: rmcmurray
description: ASP.NET Web API 'sinde dış kimlik doğrulama hizmetlerinin kullanımını açıklar.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555477"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a>ASP.NET Web API 'SI (C#) Ile dış kimlik doğrulama hizmetleri

Visual Studio 2017 ve ASP.NET 4.7.2, birden çok OAuth/OpenID ve sosyal medya kimlik doğrulama hizmeti içeren dış kimlik doğrulama hizmetleriyle tümleştirilecek [tek sayfalı uygulamalar](../../../single-page-application/index.md) (Spa) ve [Web API](../../index.md) hizmetlerinin güvenlik seçeneklerini genişletin: Microsoft hesapları, Twitter, Facebook ve Google.  

### <a name="in-this-walkthrough"></a>Bu Izlenecek yolda

- [Dış kimlik doğrulama hizmetlerini kullanma](#USING)
- [Örnek Web uygulaması oluşturma](#SAMPLE)
- [Facebook kimlik doğrulamasını etkinleştirme](#FACEBOOK)
- [Google kimlik doğrulamasını etkinleştirme](#GOOGLE)
- [Microsoft kimlik doğrulamasını etkinleştirme](#MICROSOFT)
- [Twitter kimlik doğrulamasını etkinleştirme](#TWITTER)
- [Ek Bilgiler](#MOREINFO)

    - [Dış kimlik doğrulama hizmetlerini birleştirme](#COMBINE)
    - [Tam etki alanı adını kullanmak için IIS Express yapılandırma](#FQDN)
    - [Microsoft kimlik doğrulaması için uygulama ayarlarınızı edinme](#OBTAIN)
    - [İsteğe bağlı: yerel kaydı devre dışı bırak](#DISABLE)

### <a name="prerequisites"></a>Önkoşullar

Bu yönergedeki örnekleri izlemek için aşağıdakilere sahip olmanız gerekir:

- Visual Studio 2017
- Aşağıdaki sosyal medya kimlik doğrulama hizmetlerinden biri için uygulama tanımlayıcısı ve gizli anahtarı olan bir geliştirici hesabı:

  - Microsoft hesapları ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))
  - Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))
  - Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))
  - Google ([https://developers.google.com/](https://developers.google.com))

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>Dış kimlik doğrulama hizmetlerini kullanma

Web geliştiricileri için şu anda kullanılabilir olan dış kimlik doğrulama hizmetlerinin her biri, yeni Web uygulamaları oluştururken geliştirme süresini azaltmaya yardımcı olur. Web kullanıcıları genellikle popüler Web Hizmetleri ve sosyal medya web siteleri için birkaç mevcut hesaba sahiptir, bu nedenle bir Web uygulaması kimlik doğrulama hizmetlerini bir dış Web hizmetinden veya sosyal medya web sitesinden uygularsa, , bir kimlik doğrulama uygulamasının oluşturulması için harcanacak. Bir dış kimlik doğrulama hizmeti kullanmak, son kullanıcıların Web uygulamanız için başka bir hesap oluşturmak zorunda kalmadan ve ayrıca başka bir Kullanıcı adı ve parola hatırlamasını sağlar.

Geçmişte, geliştiricilerin iki seçeneği vardı: kendi kimlik doğrulama uygulamasını oluşturun veya bir dış kimlik doğrulama hizmetini uygulamalarıyla tümleştirmeyi öğrenin. En temel düzeyde aşağıdaki diyagramda, bir Kullanıcı Aracısı (Web tarayıcısı) için bir dış kimlik doğrulama hizmeti kullanmak üzere yapılandırılmış bir Web uygulamasından bilgi isteyen basit bir istek akışı gösterilmektedir:

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

Önceki diyagramda, Kullanıcı Aracısı (veya bu örnekteki Web tarayıcısı), Web tarayıcısını bir dış kimlik doğrulama hizmetine yönlendiren bir Web uygulamasına istek yapar. Kullanıcı Aracısı kimlik bilgilerini dış kimlik doğrulama hizmetine gönderir ve Kullanıcı aracısının kimliği başarıyla doğrulandıktan sonra, dış kimlik doğrulama hizmeti, Kullanıcı aracısını bir belirteç formuyla, Kullanıcı Aracısı Web uygulamasına gönderilir. Web uygulaması, Kullanıcı aracısının dış kimlik doğrulama hizmeti tarafından başarıyla doğrulandığını doğrulamak için belirtecini kullanır ve Web uygulaması, Kullanıcı Aracısı hakkında daha fazla bilgi toplamak için belirteci kullanabilir. Uygulama, Kullanıcı aracısının bilgilerini işlemeyi tamamladıktan sonra, Web uygulaması, yetkilendirme ayarlarına bağlı olarak kullanıcı aracısına uygun yanıtı döndürür.

Bu ikinci örnekte, Kullanıcı Aracısı Web uygulaması ve dış yetkilendirme sunucusu ile anlaşır ve Web uygulaması, Kullanıcı hakkında ek bilgi almak için dış yetkilendirme sunucusuyla ek iletişim gerçekleştirir Aracısı

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

Visual Studio 2017 ve ASP.NET 4.7.2, aşağıdaki kimlik doğrulama hizmetleri için yerleşik tümleştirme sağlayarak, dış kimlik doğrulama hizmetleriyle tümleştirmeyi daha kolay hale getirir:

- Facebook
- Google
- Microsoft hesapları (Windows Live ID hesapları)
- Twitter

Bu yönergedeki örneklerde, Visual Studio 2017 ile birlikte gelen yeni ASP.NET Web uygulaması şablonunu kullanarak desteklenen dış kimlik doğrulama hizmetlerinin her birinin nasıl yapılandırılacağı gösterilir.

> [!NOTE]
> Gerekirse, FQDN 'nizi dış kimlik doğrulama hizmetinizin ayarlarına eklemeniz gerekebilir. Bu gereksinim, uygulama ayarlarınızda FQDN 'nin istemcileriniz tarafından kullanılan FQDN ile eşleşmesini gerektiren bazı dış kimlik doğrulama hizmetleri için güvenlik kısıtlamalarını temel alır. (Bunun adımları her dış kimlik doğrulama hizmeti için büyük ölçüde farklılık gösterir; bu gerekli olup olmadığını ve bu ayarların nasıl yapılandırılacağını öğrenmek için her bir dış kimlik doğrulama hizmetine yönelik belgelere başvurmanız gerekir.) Bu ortamın test edilmesi için bir FQDN kullanmak üzere IIS Express yapılandırmanız gerekiyorsa, bu kılavuzda daha sonra [tam etki alanı adı kullanmak için IIS Express yapılandırma](#FQDN) bölümüne bakın.

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a>Örnek Web uygulaması oluşturma

Aşağıdaki adımlar, ASP.NET Web uygulaması şablonunu kullanarak örnek bir uygulama oluşturma konusunda size yol açacağından, bu kılavuzda daha sonra bu örnek uygulamayı dış kimlik doğrulama hizmetlerinin her biri için kullanacaksınız.

Visual Studio 2017 ' u başlatın ve başlangıç sayfasından **Yeni proje** ' yi seçin. Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

**Yeni proje** iletişim kutusu görüntülendiğinde, **yüklü** ' ı seçin ve **görsel C#** ' i genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET Web uygulaması (.NET Framework)** öğesini seçin. Projeniz için bir ad girin ve **Tamam**' a tıklayın.

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

**Yeni ASP.NET projesi** görüntülendiğinde **tek sayfalı uygulama** şablonunu seçin ve **proje oluştur**' a tıklayın.

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

Visual Studio 2017, projenizi oluşturduğundan bekleyin.

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

Visual Studio 2017, projenizi oluşturmayı tamamladığında, **uygulama\_başlangıç** klasöründe bulunan *Startup.auth.cs* dosyasını açın.

Projeyi ilk oluşturduğunuzda, *Startup.auth.cs* dosyasında dış kimlik doğrulama hizmetlerinden hiçbiri etkinleştirilmemiştir; Aşağıda, kodunuzun neye benzebileceği, bir dış kimlik doğrulama hizmetini ve ASP.NET uygulamanızla Microsoft hesapları, Twitter, Facebook veya Google kimlik doğrulamasını kullanabilmeniz için gereken tüm ayarları vurgulayabileceğiniz bölümler verilmiştir:

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

Web uygulamanızı derlemek ve hata ayıklamak için F5 tuşuna bastığınızda, hiçbir dış kimlik doğrulama hizmeti tanımlanmayacak olduğunu göreceğiniz bir oturum açma ekranı görüntülenir.

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

Aşağıdaki bölümlerde, Visual Studio 2017 ' de ASP.NET ile birlikte sunulan dış kimlik doğrulama hizmetlerinin her birini nasıl etkinleştireceğinizi öğreneceksiniz.

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>Facebook kimlik doğrulamasını etkinleştirme

Facebook kimlik doğrulamasının kullanılması için bir Facebook Geliştirici hesabı oluşturmanız gerekir ve projeniz, Facebook 'tan çalışması için bir uygulama KIMLIĞI ve gizli anahtar gerektirir. Facebook Geliştirici hesabı oluşturma ve uygulama KIMLIĞINIZI ve gizli anahtarınızı alma hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).

Uygulama KIMLIĞI ve gizli anahtarı aldıktan sonra, Web uygulamanız için Facebook kimlik doğrulamasını etkinleştirmek üzere aşağıdaki adımları kullanın:

1. Projeniz Visual Studio 2017 ' de açıldığında, *Startup.auth.cs* dosyasını açın.

2. Kodun Facebook kimlik doğrulaması bölümünü bulun:

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. Vurgulanan kod satırlarının açıklamalarını kaldırmak için &quot;//&quot; karakterleri kaldırın ve ardından uygulama KIMLIĞINIZI ve gizli anahtarınızı ekleyin. Bu parametreleri ekledikten sonra projenizi yeniden derleyebilirsiniz:

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. Web uygulamanızı Web tarayıcınızda açmak için F5 tuşuna bastığınızda Facebook 'un bir dış kimlik doğrulama hizmeti olarak tanımlandığını görürsünüz:

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. **Facebook** düğmesine tıkladığınızda, tarayıcınız Facebook oturum açma sayfasına yönlendirilir:

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. Facebook kimlik bilgilerinizi girdikten ve **oturum aç**' a tıkladıktan sonra, Web tarayıcınız Web uygulamanıza geri yönlendirilir ve bu, Facebook hesabınızla Ilişkilendirmek istediğiniz **Kullanıcı adını** ister:

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. Kullanıcı adınızı girdikten ve **Kaydol** düğmesine tıkladıktan sonra, Web uygulamanız Facebook hesabınız için varsayılan **giriş sayfasını** görüntüleyecektir:

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>Google kimlik doğrulamasını etkinleştirme

Google kimlik doğrulamasının kullanılması için bir Google Geliştirici hesabı oluşturmanız gerekir ve projenizin çalışması için Google 'dan bir uygulama KIMLIĞI ve gizli anahtar gerekir. Google Geliştirici hesabı oluşturma ve uygulama KIMLIĞINIZI ve gizli anahtarınızı alma hakkında bilgi için bkz. [https://developers.google.com](https://developers.google.com).

Web uygulamanızda Google kimlik doğrulamasını etkinleştirmek için aşağıdaki adımları kullanın:

1. Projeniz Visual Studio 2017 ' de açıldığında, *Startup.auth.cs* dosyasını açın.

2. Kodun Google Authentication bölümünü bulun:

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. Vurgulanan kod satırlarının açıklamalarını kaldırmak için &quot;//&quot; karakterleri kaldırın ve ardından uygulama KIMLIĞINIZI ve gizli anahtarınızı ekleyin. Bu parametreleri ekledikten sonra projenizi yeniden derleyebilirsiniz:

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. Web uygulamanızı Web tarayıcınızda açmak için F5 tuşuna bastığınızda, Google 'ın dış kimlik doğrulama hizmeti olarak tanımlandığını görürsünüz:

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. **Google** düğmesine tıkladığınızda, tarayıcınız Google oturum açma sayfasına yönlendirilir:

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. Google kimlik bilgilerinizi girdikten ve **oturum aç**' a tıkladıktan sonra Google, Web uygulamanızın Google hesabınıza erişmek için gereken izinlere sahip olduğunu doğrulamanızı ister:

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. **Kabul et**' e tıkladığınızda, Web tarayıcınız Web uygulamanıza geri yönlendirilir ve bu, Google hesabınızla Ilişkilendirmek istediğiniz **Kullanıcı adını** ister:

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. Kullanıcı adınızı girdikten ve **Kaydol** düğmesine tıkladıktan sonra, Web uygulamanız Google hesabınız için varsayılan **giriş sayfasını** görüntüleyecektir:

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>Microsoft kimlik doğrulamasını etkinleştirme

Microsoft kimlik doğrulaması, bir geliştirici hesabı oluşturmanızı gerektirir ve çalışması için istemci KIMLIĞI ve istemci gizli anahtarı gerektirir. Bir Microsoft Geliştirici hesabı oluşturma ve istemci KIMLIĞINIZI ve istemci gizli anahtarını alma hakkında bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).

Tüketici anahtarınızı ve tüketici gizli anahtarını aldıktan sonra, Web uygulamanız için Microsoft kimlik doğrulamasını etkinleştirmek üzere aşağıdaki adımları kullanın:

1. Projeniz Visual Studio 2017 ' de açıldığında, *Startup.auth.cs* dosyasını açın.

2. Kodun Microsoft kimlik doğrulama bölümünü bulun:

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. Vurgulanan kod satırlarının açıklamalarını kaldırmak için &quot;//&quot; karakterleri kaldırın ve ardından istemci KIMLIĞINIZI ve istemci gizli anahtarını ekleyin. Bu parametreleri ekledikten sonra projenizi yeniden derleyebilirsiniz:

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. Web uygulamanızı Web tarayıcınızda açmak için F5 tuşuna bastığınızda, Microsoft 'un bir dış kimlik doğrulama hizmeti olarak tanımlandığını görürsünüz:

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. **Microsoft** düğmesine tıkladığınızda, tarayıcınız Microsoft oturum açma sayfasına yönlendirilir:

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. Microsoft kimlik bilgilerinizi girdikten ve **oturum aç**' a tıkladıktan sonra, web uygulamanızın Microsoft hesabı erişim izinleri olduğunu doğrulamanız istenir:

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. **Evet**' e tıkladığınızda, Web tarayıcınız Web uygulamanıza geri yönlendirilir ve bu, Microsoft hesabı Ilişkilendirmek istediğiniz **Kullanıcı adını** ister:

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. Kullanıcı adınızı girdikten ve **Kaydol** düğmesine tıkladıktan sonra, web uygulamanız Microsoft hesabı varsayılan **giriş sayfasını** görüntüleyecektir:

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>Twitter kimlik doğrulamasını etkinleştirme

Twitter kimlik doğrulaması bir geliştirici hesabı oluşturmanızı gerektirir ve çalışması için bir tüketici anahtarı ve tüketici parolası gerektirir. Twitter geliştirici hesabı oluşturma ve tüketici anahtarınızı ve tüketici gizli anahtarını alma hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).

Tüketici anahtarınızı ve tüketici gizli anahtarını aldıktan sonra, Web uygulamanız için Twitter kimlik doğrulamasını etkinleştirmek üzere aşağıdaki adımları kullanın:

1. Projeniz Visual Studio 2017 ' de açıldığında, *Startup.auth.cs* dosyasını açın.

2. Kodun Twitter kimlik doğrulaması bölümünü bulun:

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. Vurgulanan kod satırlarının açıklamalarını kaldırmak için &quot;//&quot; karakterleri kaldırın ve ardından tüketici anahtarınızı ve tüketici gizli anahtarını ekleyin. Bu parametreleri ekledikten sonra projenizi yeniden derleyebilirsiniz:

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. Web uygulamanızı Web tarayıcınızda açmak için F5 tuşuna bastığınızda, Twitter 'nın bir dış kimlik doğrulama hizmeti olarak tanımlandığını görürsünüz:

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. **Twitter** düğmesine tıkladığınızda, tarayıcınız Twitter oturum açma sayfasına yönlendirilir:

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. Twitter kimlik bilgilerinizi girdikten ve **uygulamayı Yetkilendir**' e tıkladıktan sonra, Web tarayıcınız Web uygulamanıza yeniden yönlendirilir ve bu, Twitter hesabınızla Ilişkilendirmek istediğiniz **Kullanıcı adını** ister:

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. Kullanıcı adınızı girdikten ve **Kaydol** düğmesine tıkladıktan sonra, Web uygulamanız Twitter hesabınız için varsayılan **giriş sayfasını** görüntüleyecektir:

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>Ek Bilgiler

OAuth ve OpenID kullanan uygulamalar oluşturma hakkında daha fazla bilgi için aşağıdaki URL 'Lere bakın:

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>Dış kimlik doğrulama hizmetlerini birleştirme

Daha fazla esneklik için, aynı anda birden çok dış kimlik doğrulama hizmeti tanımlayabilirsiniz. Bu, Web uygulamanızın kullanıcılarının etkinleştirilmiş dış kimlik doğrulama hizmetlerinden herhangi birinden bir hesap kullanmasına izin verir:

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a>Tam etki alanı adını kullanmak için IIS Express yapılandırma

Bazı dış kimlik doğrulama sağlayıcıları, `http://localhost:port/`gibi bir HTTP adresi kullanarak uygulamanızı test etmeyi desteklemez. Bu sorunu geçici olarak çözmek için, ana bilgisayar dosyanıza statik bir tam etki alanı adı (FQDN) eşlemesi ekleyebilir ve Visual Studio 2017 ' de proje seçeneklerinizi, test/hata ayıklama için FQDN kullanacak şekilde yapılandırabilirsiniz. Bunu yapmak için aşağıdaki adımları kullanın:

- Ana bilgisayar dosyanıza eşlenen statik bir FQDN ekleyin:

  1. Windows 'da yükseltilmiş bir komut istemi açın.
  2. Şu komutu yazın:

      <kbd>Not defteri%WinDir%\system32\drivers\etc\hosts</kbd>
  3. HOSTS dosyasına aşağıdakine benzer bir giriş ekleyin:

      <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
  4. HOSTS dosyanızı kaydedin ve kapatın.

- Visual Studio projenizi FQDN kullanacak şekilde yapılandırın:

  1. Projeniz Visual Studio 2017 ' de açıldığında, **Proje** menüsüne tıklayın ve ardından projenizin özelliklerini seçin. Örneğin, **WebApplication1 özelliklerini**seçebilirsiniz.
  2. **Web** sekmesini seçin.
  3. <strong>Proje URL 'si</strong>için FQDN 'nizi girin. Örneğin, ana bilgisayar dosyanıza eklediğiniz FQDN eşlemesiyle <kbd><http://www.wingtiptoys.com></kbd> girersiniz.

- Uygulamanız için FQDN kullanmak üzere IIS Express yapılandırın:

    1. Windows 'da yükseltilmiş bir komut istemi açın.
    2. IIS Express klasörünüze geçmek için aşağıdaki komutu yazın:

        <kbd>CD/d &quot;%ProgramFiles%\IIS Express&quot;</kbd>
    3. FQDN 'yi uygulamanıza eklemek için aşağıdaki komutu yazın:

        <kbd>Appcmd. exe set config-Section: System. applicationHost/Sites/+&quot;[ad = ' WebApplication1 ']. Bindings. [Protocol = ' http ', bindingInformation = ' *: 80: www. wingtiptoys. com ']&quot;/Commit: apphost</kbd>

  Burada **WebApplication1** , projenizin adı ve **bindingInformation** , testiniz için kullanmak istediğiniz bağlantı noktası numarasını ve FQDN 'yi içerir.

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>Microsoft kimlik doğrulaması için uygulama ayarlarınızı edinme

Microsoft kimlik doğrulaması için bir uygulamayı Windows Live 'a bağlama basit bir işlemdir. Bir uygulamayı Windows Live 'a henüz bağladıysanız, aşağıdaki adımları kullanabilirsiniz:

1. [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) gidin ve istendiğinde Microsoft hesabı adınızı ve parolanızı girip **oturum aç**' a tıklayın:

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. **Uygulama Ekle** ' yi seçin ve sorulduğunda uygulamanızın adını girin ve ardından **Oluştur**' a tıklayın:

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. **Ad** ' ın altında uygulamanızı seçin ve uygulamanın Özellikler sayfası görüntülenir.

4. Uygulamanız için yeniden yönlendirme etki alanını girin. **Uygulama kimliği** ' ni kopyalayın ve **Uygulama parolaları**' nın altında **parola oluştur**' u seçin. Görüntülenen parolayı kopyalayın. Uygulama KIMLIĞI ve parolası, istemci KIMLIĞINIZ ve istemci gizli anahtarı. **Tamam** ' ı ve ardından **Kaydet**' i seçin.

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>İsteğe bağlı: yerel kaydı devre dışı bırak

Geçerli ASP.NET yerel kayıt işlevselliği otomatik programların (botların) üye hesaplarını oluşturmasını engellemez; Örneğin, [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)gibi bir bot önleme ve doğrulama teknolojisi kullanarak. Bu nedenle, oturum açma sayfasındaki yerel oturum açma formunu ve kayıt bağlantısını kaldırmanız gerekir. Bunu yapmak için, projenizdeki *login. cshtml sayfasını\_* açın ve ardından yerel oturum açma paneli ve kayıt bağlantısı için satırları açıklama olarak inceleyin. Sonuç sayfası aşağıdaki kod örneği gibi görünmelidir:

[!code-html[Main](external-authentication-services/samples/sample10.html)]

Yerel oturum açma paneli ve kayıt bağlantısı devre dışı bırakıldıktan sonra, oturum açma sayfanız yalnızca etkinleştirdiğiniz dış kimlik doğrulama sağlayıcılarını görüntüler:

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
