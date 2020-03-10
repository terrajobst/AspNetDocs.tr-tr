---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET Web sayfalarına giriş-tutarlı bir düzen oluşturma | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ASP.NET Web sayfaları kullanan bir sitedeki Sayfalar için tutarlı bir görünüm oluşturmak üzere mizanpajları nasıl kullanabileceğiniz gösterilmektedir. Bunu tamamladığınızı varsaymaktadır...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526693"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a>ASP.NET Web sayfalarına giriş-tutarlı bir düzen oluşturma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğreticide, ASP.NET Web sayfaları kullanan bir sitedeki Sayfalar için tutarlı bir görünüm oluşturmak üzere *mizanpajları* nasıl kullanabileceğiniz gösterilmektedir. [ASP.NET Web sayfalarındaki veritabanı verilerini silerek](https://go.microsoft.com/fwlink/?LinkId=251584)seriyi tamamladığınız varsayılır.
> 
> Öğrenecekleriniz:
> 
> - Düzen sayfası ne olur?
> - Düzen sayfalarını dinamik içerikle birleştirme.
> - Değerleri bir düzen sayfasına geçirme.

## <a name="about-layouts"></a>Düzenler hakkında

Şimdiye kadar oluşturduğunuz sayfaların hepsi, tek başına sayfaları tamamlanmıştır. Hepsi aynı siteye aittir, ancak ortak bir öğe veya standart görünüm içermez.

Çoğu sitede tutarlı bir görünüm ve düzen vardır. Örneğin, [Microsoft.com/Web](https://www.microsoft.com/web/) sitesine giderseniz ve sonra da sayfaların tümünün bir genel düzene ve görsel temaya bağlı olduğunu görürsünüz:

![Üstbilginin, gezinti alanının, içerik alanının ve altbilginin yerleşimini gösteren Microsoft.com/web site sayfası](layouts/_static/image1.png)

Bu düzeni oluşturmanın *verimsiz* bir yolu, sayfalarınızın her birinde ayrı bir üst bilgi, gezinti çubuğu ve alt bilgi tanımlamak olacaktır. Her seferinde aynı biçimlendirmeyi çoğaltmaktan olursunuz. Bir şeyi değiştirmek isterseniz (örneğin, alt bilgiyi güncelleştirmek), her bir sayfayı ayrı olarak değiştirmeniz gerekir.

Bu, *Düzen sayfalarının* geldiği yerdir. ASP.NET Web sayfalarında, sitenizdeki sayfalar için genel bir kapsayıcı sağlayan bir düzen sayfası tanımlayabilirsiniz. Örneğin, Düzen sayfası üstbilgiyi, gezinti alanını ve altbilgiyi içerebilir. Düzen sayfası, ana içeriğin gittiği bir yer tutucu içerir.

Daha sonra, yalnızca bu sayfa için biçimlendirmeyi ve kodu içeren bireysel içerik sayfalarını tanımlayabilirsiniz. İçerik sayfalarının HTML sayfalarının tamamı olması gerekmez; `<body>` bir öğesi olması bile gerekmez. Ayrıca, ASP.NET içeriğini hangi düzen sayfasına göstermek istediğinizi söyleyen bir kod satırı da vardır. Bu ilişkinin nasıl çalıştığını kabaca gösteren bir resim aşağıdadır:

![İki içerik sayfası ve bu sayfaların sığması için bir düzen sayfası gösteren kavramsal diyagram](layouts/_static/image2.png)

Bu etkileşim, işlem sırasında gördüğünüz zaman anlaşılması kolay bir işlemdir. Bu öğreticide, film sayfalarınızı bir düzen kullanacak şekilde değiştireceksiniz.

## <a name="adding-a-layout-page"></a>Düzen sayfası ekleme

Ana içerik için bir üst bilgi, alt bilgi ve bir alanı olan tipik bir sayfa düzeni tanımlayan bir düzen sayfası oluşturarak başlayacaksınız. Webpagesfilmlerini sitesinde, *\_Layout. cshtml*ADLı bir cshtml sayfası ekleyin.

Önde gelen alt çizgi (`_`) karakteri önemlidir. Bir sayfanın adı alt çizgiyle başlıyorsa, ASP.NET bu sayfayı tarayıcıya doğrudan göndermez. Bu kural, siteniz için gerekli olan, ancak kullanıcıların doğrudan isteyememesi gereken sayfaları tanımlamanızı sağlar.

Sayfadaki içeriği aşağıdaki gibi değiştirin:

[!code-html[Main](layouts/samples/sample1.html)]

Görebileceğiniz gibi, bu biçimlendirme yalnızca, sayfada üç bölümü ve üç bölümü tutacak bir `<div>` öğesini tanımlamak için `<div>` öğelerini kullanan HTML 'dir. Alt bilgi, sayfada bu konumdaki geçerli yılı işleyecek Razor kodu: `@DateTime.Now.Year`bir bit içerir.

*Filmler. css*adlı bir stil sayfasının bağlantısı olduğuna dikkat edin. Stil sayfası, öğelerin fiziksel düzeninin ayrıntılarının tanımlanacaktır. Bunu bir süre içinde oluşturacaksınız.

Bu *\_Layout. cshtml* sayfasındaki tek olağan dışı özellik `@Render.Body()` satırdır. Bu düzen başka bir sayfayla birleştirildiğinde içeriğin gideceleceği yer tutucudur.

## <a name="adding-a-css-file"></a>. Css dosyası ekleme

Sayfadaki öğelerin gerçek düzenlemesini (görünüm) tanımlamanın tercih edilen yolu, geçişli stil sayfası (CSS) kuralları kullanmaktır. Bu nedenle, yeni düzeniniz için kurallara sahip bir *. css* dosyası oluşturacaksınız.

WebMatrix 'te sitenizin kökünü seçin. Ardından şeridin **dosyalar** sekmesinde, **Yeni** düğmesinin altındaki oka ve ardından **Yeni klasör**' e tıklayın.

![Şeritte Yeni ' yeni klasör ' seçeneği.](layouts/_static/image3.png)

Yeni klasör *stillerini*adlandırın.

![' Styles ' yeni klasörünü adlandırma](layouts/_static/image4.png)

Yeni *Stiller* klasörünün Içinde, *filmler. css*adlı bir dosya oluşturun.

![Yeni bir filmler. css dosyası oluşturma](layouts/_static/image5.png)

Yeni *. css* dosyasının içeriğini aşağıdakiler ile değiştirin:

[!code-css[Main](layouts/samples/sample2.css)]

İki şeyi aklınızda bulundurmanız dışında bu CSS kuralları hakkında çok daha fazla bilgi vermeyiz. Bir tane, yazı tiplerinin ve boyutların ayarlanmasına ek olarak, kuralların üst bilgi, alt bilgi ve ana içerik alanının konumunu oluşturmak için mutlak konumlandırmayı kullanmasına de olanak sağlar. CSS 'ye konumlandırmayı yeni başladıysanız W3Schools sitesinde [CSS konumlandırma](http://www.w3schools.com/css/css_positioning.asp) öğreticisini okuyabilirsiniz.

Diğer bir deyişle, en altta, *filmler. cshtml* dosyasında ilk olarak tanımlanmış stil kurallarını kopyaladık. Bu kurallar, tabloya şeritler ekleyen biçimlendirme `WebGrid` Yardımcısı oluşturmak için [ASP.NET Web Pages öğreticisi kullanılarak verileri görüntüleme](https://go.microsoft.com/fwlink/?LinkId=251580) öğreticisinde kullanılmıştır. (Stil tanımları için bir *. css* dosyası kullanacaksanız, içindeki tüm site için stil kurallarını da koyabilirsiniz.)

## <a name="updating-the-movies-file-to-use-the-layout"></a>Film dosyasını düzeni kullanmak üzere güncelleştirme

Artık yeni düzeni kullanmak için sitenizdeki mevcut dosyaları güncelleştirebilirsiniz. *Filmler. cshtml* dosyasını açın. En üstte, kodun ilk satırı olarak aşağıdakileri ekleyin:

[!code-csharp[Main](layouts/samples/sample3.cs)]

Sayfa artık bu şekilde başlatılır:

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

Bu bir kod satırı, *film* sayfası çalıştırıldığında, onun *\_Layout. cshtml* dosyası ile birleştirildiğini ASP.net söyler.

*Filmler. cshtml* dosyası artık bir düzen sayfası kullandığından, *\_Layout. cshtml* dosyası tarafından ele alınan *filmler. cshtml* sayfasından biçimlendirmeyi kaldırabilirsiniz. `<!DOCTYPE>`, `<html>`ve `<body>` etiketleri açıp kapatmak için yararlanın. Artık bir *. css* dosyasında bu kurallara sahip olduğunuz için kılavuzun stil kurallarını içeren tüm `<head>` öğesi ve içeriğini alın. Bu sırada, var olan `<h1>` öğesini bir `<h2>` öğesiyle değiştirin; Düzen sayfasında zaten bir `<h1>` öğesidir. `<h2>` metni "filmleri Listele" olarak değiştirin.

Normalde, bu tür değişiklikleri içerik sayfasında yapmanız gerekmez. Sitenizi bir düzen sayfasıyla başlattığınızda, ile başlamak için bu öğeler olmadan içerik sayfaları oluşturursunuz. Bu durumda, tek başına bir sayfayı düzen kullanan bir sayfaya dönüştürüyorsunuz, bu yüzden Temizleme biraz daha vardır.

İşiniz bittiğinde, *filmler. cshtml* sayfası aşağıdakine benzer şekilde görünür:

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a>Düzeni test etme

Artık düzenin neye benzediklerine bakabilirsiniz. WebMatrix 'te, *filmler. cshtml* sayfasına sağ tıklayın ve **tarayıcıda Başlat**' ı seçin. Tarayıcı sayfayı görüntülediğinde bu sayfada şöyle görünür:

![Düzen kullanılarak işlenen filmler sayfası](layouts/_static/image6.png)

ASP.NET, filmler. cshtml sayfasının içeriğini `RenderBody` yönteminin olduğu *\_Layout. cshtml* sayfasına birleştirmiştir. Kuşkusuz *\_Layout. cshtml* sayfası, sayfanın görünümünü tanımlayan bir *. css* dosyasına başvurur.

## <a name="updating-the-addmovie-page-to-use-the-layout"></a>Düzen kullanmak için AddMovie sayfasını güncelleştirme

Düzenlerinizin gerçek avantajı, bunları sitenizdeki tüm sayfalar için kullanabilmeniz olabilir. *Addmovie. cshtml* sayfasını açın.

*Addmovie. cshtml* sayfasının, doğrulama hata iletilerinin görünümünü tanımlamak için BAŞLANGıÇTA bazı CSS kurallarına sahip olduğunu unutmayın. Siteniz için artık bir *. css* dosyanız olduğundan, bu kuralları *. css* dosyasına taşıyabilirsiniz. Bunları *Addmovie. cshtml* dosyasından kaldırın ve bunları *filmle. css* dosyasının altına ekleyin. Aşağıdaki kuralları taşııyorsunuz:

[!code-css[Main](layouts/samples/sample6.css)]

Şimdi de,. cshtml için yaptığınız *Addmovie. cshtml* dosyasında aynı değişiklik türlerini yapın. *cshtml* — `Layout="~/_Layout.cshtml;` ekleyin ve artık gereksiz olan HTML işaretlemesini kaldırın. `<h1>` öğesini `<h2>`olarak değiştirin. İşiniz bittiğinde, sayfa şu örneğe benzer şekilde görünür:

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

Sayfayı çalıştırın. Şimdi şu şekilde görünür:

![' Film ekleme ' sayfası düzen kullanılarak işlendi](layouts/_static/image7.png)

Sitedeki sayfalarda benzer değişiklikler yapmak istiyorsunuz — *Editmovie. cshtml* ve *deletemovie. cshtml*. Ancak, bunu yapmadan önce mizanpajda çok daha esnek hale getiren başka bir değişiklik yapabilirsiniz.

## <a name="passing-title-information-to-the-layout-page"></a>Başlık bilgilerini düzen sayfasına geçirme

Oluşturduğunuz *\_Layout. cshtml* sayfasının "film Sitem" olarak ayarlanmış bir `<title>` öğesi vardır. Çoğu tarayıcı bu öğenin içeriğini bir sekmede metin olarak görüntüler:

![Bir tarayıcı sekmesinde görünen sayfanın &lt;başlığı&gt; öğesi](layouts/_static/image8.png)

Bu başlık bilgileri geneldir. Başlık metninin geçerli sayfaya daha özgü olmasını istediğinizi varsayalım. (Başlık metni, sayfanızın hakkında ne olduğunu belirlemek için arama motorları tarafından da kullanılır.) *Film. cshtml* veya *addmovie. cshtml* gibi bir içerik sayfasından düzen sayfasına bilgi geçirebilir ve sonra bu bilgileri, düzen sayfasının ne yaptığını özelleştirmek için kullanabilirsiniz.

*Filmler. cshtml* sayfasını yeniden açın. Üstteki kodda aşağıdaki satırı ekleyin:

[!code-csharp[Main](layouts/samples/sample8.cs)]

`Page` nesnesi tüm *. cshtml* sayfalarında kullanılabilir ve bu amaçla, yani bir sayfa ile düzeni arasında bilgi paylaşmak için kullanılır.

*\_Layout. cshtml* sayfasını açın. `<title>` öğesini şu biçimlendirme gibi görünecek şekilde değiştirin:

[!code-html[Main](layouts/samples/sample9.html)]

Bu kod, sayfada bu konumda `Page.Title` özelliğindeki her şeyi işler.

*Filmler. cshtml* sayfasını çalıştırın. Bu kez tarayıcı sekmesi `Page.Title`değeri olarak ne geçtiğini gösterir:

![Dinamik olarak oluşturulan başlığı gösteren bir tarayıcı sekmesi](layouts/_static/image9.png)

İsterseniz, sayfa kaynağını tarayıcıda görüntüleyin. `<title>` öğesinin `<title>List Movies</title>`olarak işlendiğine bakabilirsiniz.

> [!TIP] 
> 
> **Sayfa nesnesi**
> 
> `Page` yararlı bir özelliği dinamik bir nesne — `Title` özelliği sabit veya ayrılmış bir ad değildir. `Page` nesnesinin bir değeri için *herhangi* bir ad kullanabilirsiniz. Örneğin, `Page.CurrentName` veya `Page.MyPage`adlı bir özellik kullanarak başlığı kolayca geçirtiniz. Tek kısıtlama, adının özelliklerin adlandırılması için normal kurallara uymalıdır. (Örneğin, ad bir boşluk içeremez.)
> 
> `Page` nesnesini kullanarak istediğiniz sayıda değeri geçirebilirsiniz. Film bilgilerini düzen sayfasına geçirmek isterseniz, `Page.MovieTitle` ve `Page.Genre` ve `Page.MovieYear`gibi bir değer kullanarak değerleri geçirebilirsiniz. (Veya bilgileri depolamak için oluşturduğunuz diğer adlar.) Tek gereksinim — büyük olasılıkla açık olan — içerik sayfasında ve Düzen sayfasında aynı adları kullanmanız gerekir.
> 
> `Page` nesnesini kullanarak geçirdiğiniz bilgiler, yalnızca Düzen sayfasında görüntülenecek metinle sınırlı değildir. Düzen sayfasına bir değer geçirebilir ve ardından Düzen sayfasındaki kod, sayfanın bir bölümünün görüntülenip görüntülenmeyeceğini, hangi *CSS* dosyasının kullanılacağını vb. karar vermek için bu değeri kullanabilir. `Page` nesnesinde geçirdiğiniz değerler, kodda kullandığınız diğer değerler gibidir. Yalnızca değerler içerik sayfasında olur ve düzen sayfasına geçirilir.

*Addmovie. cshtml* sayfasını açın ve *addmovie. cshtml* sayfası için bir başlık sağlayan kodun en üstüne bir satır ekleyin:

[!code-csharp[Main](layouts/samples/sample10.cs)]

*Addmovie. cshtml* sayfasını çalıştırın. Yeni başlığı burada görebilirsiniz:

![Dinamik olarak oluşturulan ' film ekleme ' başlığını gösteren bir tarayıcı sekmesi](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a>Yerleşimi kullanmak için kalan sayfaları güncelleştirme

Artık sitenizdeki diğer sayfaları, yeni düzeni kullanacak şekilde tamamlayabilmeniz gerekir. Sırasıyla *Editmovie. cshtml* ve *deletemovie. cshtml* dosyasını açın ve her birinde aynı değişiklikleri yapın.

Düzen sayfasına bağlanan kod satırını ekleyin:

[!code-csharp[Main](layouts/samples/sample11.cs)]

Sayfanın başlığını ayarlamak için bir satır ekleyin:

[!code-csharp[Main](layouts/samples/sample12.cs)]

veya:

[!code-csharp[Main](layouts/samples/sample13.cs)]

Tüm gereksiz HTML işaretlemesini kaldır — temel olarak yalnızca `<body>` öğesi içindeki bitleri bırakın (artı en üstteki kod bloğu).

`<h1>` öğesini bir `<h2>` öğesi olacak şekilde değiştirin.

Bu değişiklikleri yaptığınızda, her birini test edin ve doğru şekilde görüntülendiğinden ve başlığın doğru olduğundan emin olun.

## <a name="parting-thoughts-about-layout-pages"></a>Düzen sayfaları hakkında düşünce

Bu öğreticide, bir *\_Layout. cshtml* sayfası oluşturdunuz ve içeriği başka bir sayfadan birleştirmek için `RenderBody` metodunu kullandınız. Bu, Web sayfalarında düzenleri kullanmaya yönelik temel bir modeldir.

Düzen sayfalarında burada kapsamadığımız ek özellikler vardır. Örneğin, düzen sayfalarını iç içe geçirebilirsiniz — bir düzen sayfası başka bir başvuruya başvurabilir. İç içe yerleştirilmiş düzenler, farklı düzenleri gerektiren bir sitenin alt bölümleri ile çalışıyorsanız yararlı olabilir. Ayrıca, Düzen sayfasında adlandırılmış bölümleri ayarlamak için ek Yöntemler (örneğin, `RenderSection`) kullanabilirsiniz.

Düzen sayfaları ve *. css* dosyalarının birleşimi güçlüdür. Sonraki öğretici serisinde gördüğünüz gibi, WebMatrix 'te önceden oluşturulmuş işlevselliğe sahip bir site sağlayan bir *şablonu*temel alan bir site oluşturabilirsiniz. Şablonlar, harika görünen ve menüler gibi özelliklere sahip siteler oluşturmak için Düzen sayfalarının ve CSS 'nin iyi bir şekilde kullanılmasını sağlar. Aşağıda, düzen sayfaları ve CSS kullanan özellikleri gösteren bir şablonu temel alan bir sitedeki giriş sayfasının ekran görüntüsü verilmiştir:

![Üst bilgi, gezinti alanı, içerik alanı, isteğe bağlı bölüm ve oturum açma bağlantıları gösteren WebMatrix site şablonu tarafından oluşturulan düzen](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a>Film sayfası için komple liste (Düzen sayfası kullanmak üzere güncelleştirildi)

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a>Film Ekle sayfası için sayfa listesini tamamlar (düzen için güncelleştirildi)

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a>Filmi Sil sayfasının sayfa listesini tamamlar (düzen için güncelleştirildi)

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a>Filmi Düzenle sayfasının sayfa listesini tamamlar (düzen için güncelleştirildi)

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a>Sonraki adımda

Bir sonraki öğreticide, herkesin görebilmesi için sitenizi Internet 'Te nasıl yayımlayacağınızı öğreneceksiniz.

## <a name="additional-resources"></a>Ek Kaynaklar

- [Tutarlı bir görünüm oluşturma](https://go.microsoft.com/fwlink/?LinkID=202891) — mizanpajlarla çalışma hakkında daha ayrıntılı bilgi sağlayan bir makale. Ayrıca, içeriğin bazılarını gösteren veya gizleyen bir düzen sayfasına bir değer geçme işlemini açıklar.
- [Razor Ile Iç Içe yerleştirilmiş düzen sayfaları](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike brind blogları, düzen sayfalarının iç içe geçme bir örneğidir. (Sayfaların indirilmesini içerir.)

> [!div class="step-by-step"]
> [Önceki](deleting-data.md)
> [İleri](publishing.md)
