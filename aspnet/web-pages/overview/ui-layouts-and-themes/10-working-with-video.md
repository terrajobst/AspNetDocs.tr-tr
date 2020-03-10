---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: Videoyu bir ASP.NET Web Pages (Razor) sitesinde görüntüleme | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde Razor söz dizimi sayfası ile ASP.NET Web sayfalarında videonun nasıl görüntüleneceği açıklanmaktadır.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628949"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a>Videoyu bir ASP.NET Web Pages (Razor) sitesinde görüntüleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, kullanıcıların sitede depolanan videoları görüntülemesine izin vermek için bir ASP.NET Web Pages (Razor) Web sitesinde video (medya) yürütücüsünün nasıl kullanılacağı açıklanmaktadır. Razor söz dizimi Web sayfaları ASP.NET, Flash ( *. swf*), Media Player ( *. wmv*) ve Silverlight ( *. xap*) videolarını oynamanızı sağlar.
> 
> Öğrenecekleriniz:
> 
> - Video oynatıcı seçme.
> - Bir Web sayfasına video ekleme.
> - Video oynatıcı özniteliklerini ayarlama.
> 
> Makalesinde sunulan ASP.NET Razor sayfaları özellikleri şunlardır:
> 
> - `Video` Yardımcısı.
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

## <a name="introduction"></a>Giriş

Sitenizde bir video göstermek isteyebilirsiniz. Bunu yapmanın bir yolu, zaten video içeren bir siteye (YouTube gibi) bağlantı kullanmaktır. Bu sitelerden bir videoyu doğrudan kendi sayfalarınıza eklemek istiyorsanız, genellikle siteden HTML biçimlendirmesi alabilir ve ardından sayfanıza kopyalayabilirsiniz. Örneğin, aşağıdaki örnek bir YouTube videosunu nasıl katıştırabileceğinizi göstermektedir:

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

Kendi web sitenizde (genel video paylaşım sitesinde değil) bir video oynatmak istiyorsanız, buna benzer katıştırılmış biçimlendirme kullanarak doğrudan buna bağlayamazsınız. Ancak, bir Medya yürütücüyü doğrudan bir sayfada işleyen `Video` Yardımcısı 'nı kullanarak sitenizdeki videoları oynatabilirsiniz.

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a>Video oynatıcı seçme

Video dosyaları için çok sayıda biçim vardır ve her biçim genellikle Player 'ı yapılandırmak için farklı bir oyuncu ve farklı bir yol gerektirir. ASP.NET Razor sayfalarında, `Video` Yardımcısı 'nı kullanarak bir Web sayfasında video oynatabilirsiniz. `Video` Yardımcısı, bir Web sayfasına video ekleme işlemini basitleştirir, çünkü bu, sayfaya video eklemek için normalde kullanılan `object` ve `embed` HTML öğelerini otomatik olarak oluşturur.

`Video` Yardımcısı aşağıdaki medya oyuncularını destekler:

- Adobe Flash
- Windows MediaPlayer
- Microsoft Silverlight

### <a name="the-flash-player"></a>Flash Player

`Video` Yardımcısı 'nın `Flash` oynatıcı, Flash videolarını ( *. swf* dosyaları) bir Web sayfasında oynaetmenize olanak tanır. En azından, video dosyasının yolunu sağlamanız gerekir. Hiçbir şey belirtmezseniz, Player geçerli Flash sürümü tarafından ayarlanan varsayılan değerleri kullanır. Tipik varsayılan ayarlar şunlardır:

- Video, varsayılan genişliği ve yüksekliği kullanılarak ve bir arka plan rengi olmadan görüntülenir.
- Sayfa yüklendiğinde video otomatik olarak oynatılır.
- Video, açıkça durduruluncaya kadar sürekli olarak döngü olur.
- Video, belirli bir boyuta sığacak şekilde videoyu kırpmak yerine videonun tamamını gösterecek şekilde ölçeklendirilir.
- Video bir pencerede oynatılır.

### <a name="the-mediaplayer-player"></a>MediaPlayer yürütücüsü

`Video` yardımcı 'nın `MediaPlayer` oynatıcı, bir Web sayfasında Windows Media videolarını ( *. wmv* dosyaları), Windows Media Audio ( *. wma* dosyaları) ve MP3 ( *. mp3* dosyaları) oynamanızı sağlar. Yürütülecek medya dosyasının yolunu dahil etmeniz gerekir; diğer tüm parametreler isteğe bağlıdır. Yalnızca bir yol belirtirseniz, oynatıcı şu şekilde geçerli MediaPlayer sürümü tarafından ayarlanan varsayılan ayarları kullanır:

- Video varsayılan genişliği ve yüksekliği kullanılarak görüntülenir.
- Sayfa yüklendiğinde video otomatik olarak oynatılır.
- Video bir kez oynatılır (döngüye almaz).
- Oynatıcı, Kullanıcı arabirimindeki denetimlerin tam kümesini görüntüler.
- Video bir pencerede oynatılır.

### <a name="the-silverlight-player"></a>Silverlight oynatıcı

`Video` Yardımcısı 'nın `Silverlight` oynatıcı, Windows Media videosunu ( *. wmv* dosyaları), Windows Media Audio ( *. wma* dosyaları) ve MP3 ( *. mp3* dosyaları) oynamanızı sağlar. Yol parametresini, Silverlight tabanlı bir uygulama paketine ( *. xap* dosyası) işaret etmek üzere ayarlamalısınız. Genişlik ve yükseklik parametrelerini de ayarlamanız gerekir. Diğer tüm parametreler isteğe bağlıdır. Video için Silverlight Player 'ı kullandığınızda, yalnızca gerekli parametreleri ayarlarsanız, Silverlight Player Videoyu arka plan rengi olmadan görüntüler.

> [!NOTE]
> Silverlight 'ı henüz bilmiyorsanız: *. xap* dosyası, bir *. xaml* dosyasındaki düzen yönergelerini, derlemelerde yönetilen kodu ve isteğe bağlı kaynakları içeren sıkıştırılmış bir dosyadır. Visual Studio 'da bir *. xap* dosyasını Silverlight uygulama projesi olarak oluşturabilirsiniz.

`Silverlight` video oynatıcı, oynatıcı için sağladığınız ayarları ve *. xap* dosyasında belirtilen ayarları kullanır.

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a>MIME türleri
> 
> Tarayıcı bir dosyayı indirdiğinde, tarayıcı dosya türünün işlenen belge için belirtilen MIME türüyle eşleştiğinden emin olur. MIME türü, bir dosyanın içerik türü veya ortam türüdür. `Video` Yardımcısı aşağıdaki MIME türlerini kullanır:
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a>Flash (. swf) videoları oynama

Bu yordam, *Sample. swf*adlı bir Flash videonun nasıl çalındığını gösterir. Yordamda, sitenizde *medya* adlı bir klasör olduğunu ve *. swf* dosyasının bu klasörde olduğunu varsaymış olursunuz.

1. ASP.NET Web yardımcıları kitaplığını, daha önce eklemediyseniz [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)başlığı altında açıklandığı gibi Web sitenize ekleyin.
2. Web sitesinde bir sayfa ekleyin ve bunu *FlashVideo. cshtml*olarak adlandırın.
3. Aşağıdaki biçimlendirmeyi sayfaya ekleyin: 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. Sayfayı bir tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) Sayfa görüntülenir ve video otomatik olarak oynatılır. 

    ![görüntüyle](10-working-with-video/_static/image1.jpg "ch08_video -1. jpg")

Bir Flash videonun `quality` parametresini `low`, `autolow`, `autohigh`, `medium`, `high`ve `best`olarak ayarlayabilirsiniz:

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

Aşağıdaki şekilde ayarlayabileceğiniz `scale` parametresini kullanarak, Flash videosunu belirli bir boyutta yürütmeye dönüştürebilirsiniz:

- `showall`. Bu, orijinal en boy oranını koruyarak videonun tamamının görünmesini sağlar. Bununla birlikte, her bir taraftaki kenarlıkların üzerine çıkabilir.
- `noorder`. Bu, özgün en boy oranını koruyarak videoyu ölçeklendirir, ancak kırpılmış olabilir.
- `exactfit`. Bu, özgün en boy oranını korumadan videonun tamamını görünür hale getirir, ancak deformasyon meydana gelebilir.

Bir `scale` parametresi belirtmezseniz, videonun tamamı görünür olur ve özgün en boy oranı herhangi bir kırpma olmadan korunur. Aşağıdaki örnek `scale` parametrenin nasıl kullanılacağını gösterir:

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

Flash Player, `windowMode`adlı bir video modu ayarını destekler. Bunu `window`, `opaque`ve `transparent`olarak ayarlayabilirsiniz. Varsayılan olarak `windowMode`, videoyu web sayfasındaki ayrı bir pencerede görüntüleyen `window`olarak ayarlanır. `opaque` ayarı, Web sayfasındaki videonun arkasındaki her şeyi gizler. `transparent` ayarı, Web sayfasının arka planının videoda görünmesini sağlar ve videonun herhangi bir kısmının saydam olduğunu varsayar.

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a>MediaPlayer ( *. wmv*) videoları oynama

Aşağıdaki yordamda, *Media* klasöründe *örnek. wmv* adlı bir pencere medya videosunu nasıl oynatacak gösterilmektedir.

1. Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.
2. *MediaPlayerVideo. cshtml*adlı yeni bir sayfa oluşturun.
3. Aşağıdaki biçimlendirmeyi sayfaya ekleyin: 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. Sayfayı bir tarayıcıda çalıştırın. Video otomatik olarak yüklenir ve oynatılır. 

    ![görüntüyle](10-working-with-video/_static/image2.jpg "ch08_video -2. jpg")

Videonun otomatik olarak kaç kez çalındığını belirten bir tamsayıya `playCount` ayarlayabilirsiniz:

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

`uiMode` parametresi, Kullanıcı arabiriminde hangi denetimlerin gösterileceğini belirtmenizi sağlar. `uiMode` `invisible`, `none`, `mini`veya `full`olarak ayarlayabilirsiniz. Bir `uiMode` parametresi belirtmezseniz, video, ekran penceresine ek olarak durum penceresi, arama çubuğu, denetim düğmeleri ve ses denetimleriyle birlikte görüntülenir. Bu denetimler, Player 'ı bir ses dosyası çalmak için kullanıyorsanız de görüntülenir. `uiMode` parametresinin nasıl kullanılacağına ilişkin bir örnek aşağıda verilmiştir:

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

Varsayılan olarak, video oynatılırken ses açık olur. `mute` parametresini true olarak ayarlayarak sesin sesini kapatabilirsiniz:

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

`volume` parametresini 0 ile 100 arasında bir değere ayarlayarak MediaPlayer videosunun ses düzeyini kontrol edebilirsiniz. Varsayılan değer 50 ' dir. Örnek buradadır:

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a>Silverlight videoları oynama

Bu yordam, *medya*adlı bir klasörde bulunan Silverlight *. xap* sayfasında bulunan videonun nasıl çalındığını gösterir.

1. Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.
2. *SilverlightVideo. cshtml*adlı yeni bir sayfa oluşturun.
3. Aşağıdaki biçimlendirmeyi sayfaya ekleyin: 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. Sayfayı bir tarayıcıda çalıştırın. 

    ![görüntüyle](10-working-with-video/_static/image3.jpg "ch08_video -3. jpg")

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[Silverlight genel bakış](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[Flash NESNESI ve ekleme etiketi öznitelikleri](http://kb2.adobe.com/cps/127/tn_12701.html)

[Windows Media Player 11 SDK PARAM etiketleri](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)
