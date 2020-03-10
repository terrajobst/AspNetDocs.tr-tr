---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: Bir ASP.NET Web Pages (Razor) sitesi için ziyaretçi bilgilerini (Analytics) izleme | Microsoft Docs
author: Rick-Anderson
description: Web sitenizi aldıktan sonra, Web sitesi trafiğinizi çözümlemek isteyebilirsiniz.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525188"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>Bir ASP.NET Web Pages (Razor) sitesi için ziyaretçi bilgilerini (Analytics) izleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesindeki sayfalara Web sitesi analizi eklemek için bir yardımcı 'nın nasıl kullanılacağı açıklanır.
> 
> Öğrenecekleriniz:
> 
> - Bir analiz sağlayıcısına Web sitesi trafiğiniz hakkında bilgi gönderme.
> 
> Makalesinde sunulan ASP.NET programlama özellikleri şunlardır:
> 
> - `Analytics` Yardımcısı.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - ASP.NET Web yardımcıları kitaplığı (NuGet paketi)

Analytics, Web sitenizdeki trafiği ölçtüğünden kişilerin siteyi nasıl kullandığını anlayabilmeniz için genel bir terimdir. Google, Yahoo, StatCounter ve diğer hizmetler de dahil olmak üzere birçok analiz hizmeti mevcuttur.

Analytics 'in çalışma şekli, analiz sağlayıcısına sahip bir hesap için kaydolup izlemek istediğiniz siteyi kaydetmenizi sağlar. Sağlayıcı size hesabınız için bir KIMLIK veya izleme kodu içeren bir JavaScript kodu kod parçacığı gönderir. JavaScript kod parçacığını izlemek istediğiniz sitede Web sayfalarına eklersiniz. (Analiz parçacığını genellikle sitenizdeki her sayfada görüntülenen bir alt bilgiye veya Düzen sayfasına veya diğer HTML biçimlendirmesine eklersiniz.) Kullanıcılar bu JavaScript parçacıklarında birini içeren bir sayfa talep edildiğinde, kod parçacığı geçerli sayfa hakkındaki bilgileri analiz sağlayıcısına gönderir ve Bu sayfa hakkındaki çeşitli ayrıntıları kaydeder.

Sitenizin istatistiklerine bakmak istediğinizde, analiz sağlayıcısının Web sitesinde oturum açın. Daha sonra, siteniz hakkındaki tüm rapor türlerini görüntüleyebilirsiniz, örneğin:

- Tek tek sayfaların sayfa görüntüleme sayısı. Bu, siteden kaç kişinin ziyaret ettiğini ve sitenizdeki hangi sayfaların en popüler olduğunu size bildirir.
- Belirli sayfalarda ne kadar zaman harcadığını. Bu, giriş sayfanızın insanların ilgisini tutmasına bakılmaksızın size bir şeyler söyleyebilir.
- Sitenizi ziyaret etmeden önce insanların hangi siteler üzerinde olduğunu. Bu, trafiğinizin bağlantılardan, aramalardan, vb. olduğunu anlamanıza yardımcı olur.
- İnsanlar sitenizi ziyaret ettiğinde ve ne kadar süreceğine ilişkin kişiler.
- Ziyaretçilerinizin hangi ülkeleri öğrendiklerdir.
- Ziyaretçilerinizin kullandığı tarayıcılar ve işletim sistemleri.

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>Bir sayfaya analiz eklemek için yardımcı kullanma

ASP.NET Web sayfaları, analiz için kullanılan JavaScript parçacıklarını yönetmeyi kolaylaştıran çeşitli analiz yardımcıları (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`ve `Analytics.GetStatCounterHtml`) içerir. JavaScript kodunun nasıl ve nereye yerleştirileceğini öğrenmek yerine, tüm yapmanız gereken bir sayfaya yardımcı eklemektir. Sağlamanız gereken tek bilgi, hesap adınız, KIMLIĞINIZ veya izleme kodunuz olur. (StatCounter için, birkaç ek değer de sağlamanız gerekir.)

Bu yordamda, `GetGoogleHtml` yardımcısını kullanan bir düzen sayfası oluşturacaksınız. Diğer analiz sağlayıcılarından birine sahip bir hesabınız zaten varsa, bunun yerine bu hesabı kullanabilir ve gereken hafif ayarlamaları yapabilirsiniz.

> [!NOTE]
> Bir analiz hesabı oluşturduğunuzda, izlemek istediğiniz sitenin URL 'sini kaydedersiniz. Yerel bilgisayarınızdaki her şeyi test ediyorsanız, gerçek trafiği izmeyeceksiniz (tek trafik sizin olur), bu nedenle site istatistiklerini kaydedemeyecek ve görüntüleyemeyeceksiniz. Ancak bu yordamda bir sayfaya nasıl analiz Yardımcısı ekleyeceğiniz gösterilmektedir. Sitenizi yayımladığınızda, canlı site analiz sağlayıcınıza bilgi gönderir.

1. ASP.NET Web yardımcıları kitaplığını, daha önce eklemediyseniz [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)başlığı altında açıklandığı gibi Web sitenize ekleyin.
2. Google Analytics ile bir hesap oluşturun ve hesap adını kaydedin.
3. *Analytics. cshtml* adlı bir düzen sayfası oluşturun ve aşağıdaki biçimlendirmeyi ekleyin:

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > Çağrısı, Web sayfanızın gövdesinde (`</body>` etiketinden önce) `Analytics` Yardımcısı 'na yerleştirmeniz gerekir. Aksi takdirde, tarayıcı betiği çalıştırmaz.

    Farklı bir analiz sağlayıcısı kullanıyorsanız, bunun yerine aşağıdaki yardımcıların birini kullanın:

    - (Yahoo) `@Analytics.GetYahooHtml("myaccount")`
    - (StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`
4. `myaccount`, 1. adımda oluşturduğunuz hesabın, KIMLIğIN veya izleme kodunun adıyla değiştirin.
5. Sayfayı tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.)
6. Tarayıcıda, sayfa kaynağını görüntüleyin. İşlenmiş analiz kodunu görebileceksiniz:

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. Google Analytics sitesinde oturum açın ve sitenizin istatistiklerini inceleyin. Sayfayı canlı bir sitede çalıştırıyorsanız, sayfanıza ziyaretinizi günlüğe kaydeden bir giriş görürsünüz.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [Google Analytics sitesi](https://www.google.com/analytics/)
- [Yahoo! Web Analytics sitesi](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter sitesi](http://statcounter.com/)
