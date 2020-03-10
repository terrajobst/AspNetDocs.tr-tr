---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: Haritaları bir ASP.NET Web Pages (Razor) sitesinde görüntüleme | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, Bing, Google, MA tarafından sunulan eşleme hizmetlerine bağlı olarak ASP.NET Web Pages (Razor) Web sitesindeki sayfalarda etkileşimli haritalar görüntüleme açıklanmaktadır.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638679"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>Haritaları bir ASP.NET Web Pages (Razor) sitesinde görüntüleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, ASP.NET Web Pages (Razor) Web sitesindeki sayfalarda, Bing, Google, Map ve Yahoo tarafından sunulan eşleme hizmetlerine bağlı olarak etkileşimli eşlemelerin nasıl görüntüleneceği açıklanır.
> 
> Öğrenecekleriniz:
> 
> - Bir adrese göre harita oluşturma.
> - Enlem ve boylam koordinatları temelinde harita oluşturma.
> - Bing Haritalar Geliştirici hesabını kaydetme ve Bing Haritalar ile kullanmak için bir anahtar alma.
> 
> Bu, makalesinde sunulan ASP.NET özelliğidir:
> 
> - `Maps` Yardımcısı.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - WebMatrix 2
>   
> 
> Bu öğretici WebMatrix 3 ile de kullanılabilir.

Web sayfalarında, `Maps` Yardımcısı 'nı kullanarak bir sayfada haritaları görüntüleyebilirsiniz. Bir adrese veya boylam ve enlem koordinatlarına göre haritalar oluşturabilirsiniz. `Maps` sınıfı Bing, Google, Mapınsize ve Yahoo gibi popüler harita altyapılarına çağrı yapmanızı sağlar.

Bir sayfaya eşleme eklemek için gereken adımlar, hangi harita altyapılarından bağımsız olarak çağrılacağını göz önüne alınır. Yalnızca Haritayı görüntülemesi için kullanılabilir yöntemler sağlayan bir JavaScript dosya başvurusu eklersiniz ve sonra `Maps` Yardımcısı yöntemlerini çağırabilirsiniz.

Kullandığınız `Maps` yardımcı yöntemine göre bir harita hizmeti seçersiniz. Bunlardan herhangi birini kullanabilirsiniz:

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>Ihtiyaç duyduğunuz parçaları yükleme

Haritaları göstermek için şu parçalara ihtiyacınız vardır:

- `Maps` Yardımcısı. Bu yardımcı ASP.NET Web yardımcıları kitaplığı sürüm 2 ' dir. Kitaplığı henüz eklemediyseniz, sitenize bir NuGet paketi olarak yükleyebilirsiniz. Ayrıntılar için bkz. [ASP.NET Web Pages sitesinde yardımcıları yükleme](https://go.microsoft.com/fwlink/?LinkId=252372). (Galeride `microsoft-web-helpers` paketini arayın.)
- JQuery kitaplığı. Birçok WebMatrix site şablonu, kendi *betik* klasörlerinde jQuery kitaplıklarını zaten içeriyor. Bu kitaplıklara sahip değilseniz, en son jQuery kitaplığını doğrudan [jQuery.org](http://jQuery.org) sitesinden indirebilirsiniz. Ya da bir şablon (örneğin, **Başlatıcı site** şablonu) kullanarak yeni bir site oluşturabilir ve ardından bu sitedeki jQuery dosyalarını geçerli sitenize kopyalayabilirsiniz.

Son olarak, Bing Haritalar 'ı kullanmak istiyorsanız, önce bir (ücretsiz) hesap oluşturmanız ve bir anahtar almanız gerekir. Bir anahtar almak için aşağıdaki adımları izleyin:

1. [Bing Haritalar Geliştirici hesabında](https://www.microsoft.com/maps/developers/web.aspx)bir hesap oluşturun. Bir Microsoft hesabı (Windows Live ID) de olmalıdır.

    **Değerlendirme/test**için anahtarı kullanmak istediğinizi belirtebilirsiniz. Kendi bilgisayarınızda WebMatrix ve IIS Express kullanarak eşleme işlevini test ediyorsanız, **site** çalışma alanına gidin ve sitenizin URL 'sini (örneğin `http://localhost:50408`, bağlantı noktası numaranız farklı olsa da) göz önünde bulabilirsiniz. Kayıt sırasında bu *localhost* adresini site olarak kullanabilirsiniz.
2. Bir hesap için kaydolduktan sonra Bing Haritalar hesap Merkezi ' ne gidin ve **anahtar oluştur veya görüntüle**' ye tıklayın:

    ![eşleme-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. Bing tarafından oluşturulan anahtarı kaydedin.

## <a name="creating-a-map-based-on-an-address-using-google"></a>Bir adrese göre harita oluşturma (Google kullanarak)

Aşağıdaki örnek, bir adresi temel alarak Haritayı işleyen bir sayfanın nasıl oluşturulacağını gösterir. Bu örnek, Google Maps 'ın nasıl kullanılacağını gösterir.

1. Sitenin kökünde *Mapaddress. cshtml* adlı bir dosya oluşturun. Bu sayfa, kendisine geçirdiğiniz bir adresi temel alan bir harita oluşturur.
2. Aşağıdaki kodu, var olan içeriğin üzerine yazarak dosyaya kopyalayın.

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    Sayfanın aşağıdaki özelliklerine dikkat edin:

    - `<head>` öğesindeki `<script>` öğesi. Örnekte `<script>` öğesi, jQuery kitaplığı, sürüm 1.6.4 'in küçültülmüş (sıkıştırılmış) bir sürümü olan *jQuery-1.6.4. min. js* dosyasına başvurur. Başvurunun *. js* dosyasının sitenizin *betikler* klasöründe olduğunu varsaydığını unutmayın. 

        > [!NOTE]
        > JQuery kitaplığı 'nın farklı bir sürümünü kullanıyorsanız, bu sürüme doğru şekilde işaret ettiğinizden emin olun.
    - Sayfanın gövdesinde `@Maps.GetGoogleHtml` çağrısı. Bir adresi eşlemek için bir adres dizesi geçirmeniz gerekir. Diğer harita motorları için yöntemler benzer bir şekilde çalışır (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).
3. Sayfayı çalıştırın ve bir adres girin. Sayfada, belirttiğiniz konumu gösteren Google Maps temelinde bir harita görüntülenir.

     ![eşleme-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>Enlem ve boylam koordinatları temelinde harita oluşturma (Bing kullanarak)

Bu örnek, koordinatları temel alarak bir haritanın nasıl oluşturulacağını gösterir. Bu örnek, Bing Haritalar 'ın nasıl kullanılacağını ve Bing anahtarınızı nasıl ekleneceğini gösterir. (Bing anahtar kullanmadan diğer eşleme altyapılarını kullanarak koordinatları temel alan bir harita oluşturabilirsiniz.)

1. Sitesinin kökünde *Mapkoordinatlar. cshtml* adlı bir dosya oluşturun ve var olan içeriği şu kod ve biçimlendirmeyle değiştirin:

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. `your-key-here`, daha önce oluşturduğunuz Bing Haritalar anahtarıyla değiştirin.
3. *Mapkoordinatlar. cshtml* sayfasını çalıştırın, enlem ve boylam koordinatlarını girin ve ardından **haritaya tıklayın!** tıklayın. (Herhangi bir koordinat bilmiyorsanız, aşağıdakileri deneyin. Bu, Microsoft Redmond kampüs üzerinde bir konumdur.)

   - Enlem: 47.6781005859375
   - Boylam:-122.158317565918

     Sayfa, belirttiğiniz koordinatlar kullanılarak görüntülenir.

     ![eşleme-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[Microsoft. Maps API başvurusu](https://msdn.microsoft.com/library/gg427611.aspx)
