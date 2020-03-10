---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: ASP.NET Web Pages (Razor) sitelerine sosyal ağ ekleme | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde sitenizin sosyal ağ hizmetleriyle nasıl tümleştirileceği açıklanmaktadır. Bu bölümde, kullanıcıların Web sitenizi nasıl işaretleyeceğinizi/bağlayacağınızı öğreneceksiniz...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526938"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) sitelerine sosyal ağ ekleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede Facebook, Twitter, reddıt ve Digg için sosyal ağ bağlantılarının bir ASP.NET Web Pages (Razor) Web sitesindeki sayfalara nasıl ekleneceği ve Twitter akışlarının, Xbox oyuncu kartlarının ve Gravatar görüntülerinin nasıl dahil olduğu açıklanmaktadır.
> 
> Öğrenecekleriniz:
> 
> - Siteleri, sitenizi yer işaretine/bağlanmasına nasıl izin verirsiniz.
> - Twitter akışı ekleme.
> - Sayfalara Facebook **benzeri** düğme ekleme.
> - Gravatar.com görüntülerini işleme.
> - Sitenizde Xbox oyuncu kartı görüntüleme.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - ASP.NET Web Yardımcısı kitaplığı (NuGet paketi)
>   
> 
> Bu öğretici, ASP.NET Web Yardımcısı kitaplığı kullanan parçalar dışında ASP.NET Web Pages 3 ile de kullanılabilir.

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>Web sitenizi sosyal ağ sitelerinde bağlama

Sitenizde sizinle ilgili bir şey varsa, genellikle arkadaşlarınızla paylaşmak ister. Bu, insanların bir sayfayı Digg, Reddıt, Facebook, Twitter veya benzer sitelerde paylaşmak için tıklaması gereken glifleri (simgeler) görüntüleyerek kolayca yapabilirsiniz.

Bu glifleri göstermek için `LinkSharecode` yardımcısını bir sayfaya ekleyin. Sayfanızı ziyaret eden kişiler, tek bir glifi tıklatabilir. Bu sosyal ağ sitesi olan bir hesabı varsa, bu sitede sayfanıza bir bağlantı gönderebilir.

![Resim 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. ASP.NET Web yardımcıları kitaplığını, daha önce eklemediyseniz [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)başlığı altında açıklandığı gibi Web sitenize ekleyin.- *listlinkshare. cshtml* adlı bir sayfa oluşturun ve şu biçimlendirmeyi ekleyin:

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    Bu örnekte, `LinkShare` Yardımcısı çalıştığında, sayfa başlığı bir parametre olarak geçirilir ve bu da sayfa başlığını sosyal ağ sitesine geçirir. Ancak, istediğiniz herhangi bir dizeyi geçirebilirsiniz. Bu örnek ayrıca listede hangi sosyal ağ sitelerinin ekleneceğini de belirtir. Siteniz için uygun olan sosyal ağ sitelerini belirtebilirsiniz.
2. *Listlinkshare. cshtml* sayfasını bir tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.)
3. Kaydolduğunuz sitelerden biri için bir glifi tıklatın. Bağlantı sizi, bir bağlantıyı paylaşabileceğiniz seçili sosyal ağ sitesindeki sayfaya götürür. Örneğin, Reddıt bağlantısına tıklarsanız, Reddıt Web sitesindeki `submit to reddit` sayfasına yönlendirilirsiniz.

     ![Resim 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>Twitter akışı ekleme

Twitter API 'sinin geçerli sürümü ile uyumlu bir Twitter Yardımcısı kullanma hakkında daha fazla bilgi için bkz. [Twitter Yardımcısı](../ui-layouts-and-themes/twitter-helper.md). Bu örnek, kodu birçok sayfadan kolayca yeniden kullanabilmeniz için kendi yardımcınızın nasıl yazılacağını gösterir.

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>&quot; düğme gibi Facebook &quot;görüntüleme

Bazı durumlarda en iyi seçenek, kodu bir yardımcıya güvenmek yerine doğrudan sosyal ağ sağlayıcısından almanızı sağlar. Bu özellikle, sosyal ağ sağlayıcısı seçeneklerini yardımcı güncelleştirildikten daha hızlı güncelleştiriyorsa geçerlidir.

Sitenize Facebook özellikleri eklemek için (örneğin, benzer düğme), [Developers.facebook.com](https://developers.facebook.com/) sitesinden kod parçacıklarını alabilirsiniz. Facebook sitesinde, kendi araçlarını kullanarak sitenize uygun bir kod parçacığı oluşturabilirsiniz.

Aşağıdaki vurgulanan kod, developers.facebook.com sitesindeki beğen düğme aracından alınan koddur. Kendi uygulama KIMLIĞINIZI sağlamanız gerekir.

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>Gravatar görüntüsünü işleme

Bir *Gravatar* (&quot;genel olarak tanınan avatar&quot;), sizi temsil eden bir görüntü olan avatar &#8212; olarak birden çok Web sitesinde kullanılabilen bir görüntüdür. Örneğin, bir Gravatar bir kişiyi bir forum gönderisine, blog açıklamasında ve benzeri bir kişiye tanımlayabilir. ( [http://www.gravatar.com/](http://www.gravatar.com/)konumundaki gravaık Web sitesinde kendi Gravatar ' i kaydedebilirsiniz.) Web sitenizde kişilerin adları veya e-posta adreslerinin yanında bulunan görüntüleri göstermek istiyorsanız Gravatar yardımcısını kullanabilirsiniz.

Bu örnekte, kendinizi temsil eden tek bir Gravatar kullanıyorsunuz. Gravatar kullanmanın başka bir yolu da sitenize kaydolduklarında kişilerin Gravatar adresini belirtmektir. (Kullanıcıların [bir ASP.NET Web sayfaları sitesine güvenlik ve üyelik ekleme](https://go.microsoft.com/fwlink/?LinkId=202904)konusunda nasıl kayıt yapılacağını öğrenebilirsiniz.) Böylece, bu kullanıcı için bilgileri her görüntülediğinizde, yalnızca kullanıcının adını görüntüleyen Gravatar öğesini ekleyebilirsiniz.

1. Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.
2. *Gravatar. cshtml*adlı yeni bir Web sayfası oluşturun.
3. Aşağıdaki biçimlendirmeyi dosyaya ekleyin: 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    `Gravatar.GetHtml` yöntemi, sayfada Gravatar görüntüsünü görüntüler. Görüntünün boyutunu değiştirmek için, ikinci parametre olarak bir sayı ekleyebilirsiniz. Varsayılan boyut 80 ' dir. 80 'den küçük sayılar görüntüyü küçültün. 80 'den büyük sayılar görüntüyü daha büyük yapar.
4. `Gravatar.GetHtml` metotlarında, `<Your Gravatar account here>` değerini Gravatar hesabınız için kullandığınız e-posta adresiyle değiştirin. (Gravatar hesabınız yoksa, bunu yapan birisinin e-posta adresini kullanabilirsiniz.)
5. Sayfayı tarayıcınızda çalıştırın. Sayfada, belirttiğiniz e-posta adresi için iki Gravatar görüntüsü görüntülenir. İkinci görüntü birincisinden daha küçüktür. 

    ![Resim 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>Xbox Gamer kartını görüntüleme

İnsanlar Microsoft Xbox oyunları 'nı çevrimiçi olarak oynadığınızda, her kullanıcının benzersiz bir KIMLIĞI vardır. İstatistikler, her oyuncu için, saygınlığı, oyuncu puanı ve son oynatılan oyunları gösteren bir oyuncu kartı biçiminde tutulur. Bir Xbox oyuncu kullanıyorsanız, `GamerCard` Yardımcısı 'nı kullanarak, sitenizdeki sayfalarda oyuncu kartınızı gösterebilirsiniz.

1. Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.
2. *Xboxgamer. cshtml* adlı yeni bir sayfa oluşturun ve aşağıdaki biçimlendirmeyi ekleyin.

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    `GamerCard.GetHtml` özelliğini kullanarak, oyuncu kartı görüntülenecek diğer adı belirtebilirsiniz.
3. Sayfayı tarayıcınızda çalıştırın. Sayfada belirttiğiniz Xbox oyuncu kartı görüntülenir.

    ![Resim 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
