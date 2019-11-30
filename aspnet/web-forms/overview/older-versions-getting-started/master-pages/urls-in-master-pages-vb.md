---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-vb
title: Ana sayfalardaki URL 'Ler (VB) | Microsoft Docs
author: rick-anderson
description: Ana sayfadaki URL 'Lerin, ana sayfa dosyası içerik sayfasından farklı bir göreli dizinde olması nedeniyle nasıl kesintiye uğrasatığına yöneliktir. Yeniden temellendiriliyor...
ms.author: riande
ms.date: 06/10/2008
ms.assetid: 43d1e83c-0092-4dcf-977c-e709c4dce7c3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 01627988f68bb619969a5fe3cfaae68fe70b5d4f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588229"
---
# <a name="urls-in-master-pages-vb"></a>Ana Sayfalardaki URL'ler (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_VB.pdf)

> Ana sayfadaki URL 'Lerin, ana sayfa dosyası içerik sayfasından farklı bir göreli dizinde olması nedeniyle nasıl kesintiye uğrasatığına yöneliktir. Bildirim temelli sözdiziminde ~ ile URL 'Leri yeniden temellendiriliyor ve ResolveUrl ve ResolveClientUrl programlama programlı bir şekilde kullanılıyor. (Ayrıca şuna göz atın:

## <a name="introduction"></a>Giriş

Şimdiye kadar görtiğimiz tüm örneklerde, ana ve içerik sayfaları aynı klasörde (Web sitesinin kök klasörü) bulunur. Ancak ana ve içerik sayfalarının aynı klasörde olması neden yoktur. Alt klasörlerde kesinlikle içerik sayfaları oluşturabilirsiniz. Benzer şekilde, sitenizin ana sayfalarını yerleştirdiğiniz bir `~/MasterPages/` klasörü oluşturabilirsiniz.

Farklı klasörlerde ana ve içerik sayfalarının yerleştirilmesi ile ilgili olası bir sorun, bozuk URL 'Ler içerir. Ana sayfa, köprülerde, resimlerde veya diğer öğelerde göreli URL 'Ler içeriyorsa, farklı bir klasörde bulunan içerik sayfaları için bağlantı geçersiz olur. Bu öğreticide, bu sorunun kaynağını ve geçici çözümleri inceleyeceğiz.

## <a name="the-problem-with-relative-urls"></a>Göreli URL 'lerle ilgili sorun

Web sayfasındaki bir URL, işaret ettiği kaynağın konumu Web sayfasının klasör yapısındaki konumuyla göreli ise *göreli BIR URL* olarak kabul edilir. Önde gelen eğik çizgi (`/`) veya protokolle (`http://`gibi) başlamadığı tüm URL 'ler, URL 'YI içeren Web sayfasının konumuna bağlı olarak tarayıcı tarafından çözümlendiği için görelidir.

Örneğin, Web sitemiz tek bir görüntü dosyası olan bir `~/Images/` klasöre sahiptir `PoweredByASPNET.gif`. Ana sayfa dosyası `Site.master`, aşağıdaki biçimlendirmeye sahip `footerContent` bölgesinde bir `<img>` öğesine sahiptir:

[!code-html[Main](urls-in-master-pages-vb/samples/sample1.html)]

`<img>` öğesindeki `src` özniteliği değeri, `/` veya `http://`başlamadığı için göreli bir URL 'dir. Kısacası `src` öznitelik değeri, tarayıcıya `PoweredByASPNET.gif`adlı bir dosyanın `Images` alt klasörüne bakmasını söyler.

Bir içerik sayfası ziyaret edildiğinde Yukarıdaki biçimlendirme doğrudan tarayıcıya gönderilir. `About.aspx` ziyaret edip tarayıcıya gönderilen HTML kaynağını görüntülemek için bir dakikanızı ayırın. Ana sayfada tam olarak aynı biçimlendirmenin tarayıcıya gönderildiğini görürsünüz.

[!code-html[Main](urls-in-master-pages-vb/samples/sample2.html)]

İçerik sayfası kök klasördeyse (`About.aspx`olduğu gibi), kök klasöre göre bir `Images` alt klasörü olduğundan her şey beklendiği gibi çalışıyor. Ancak, içerik sayfası ana sayfadan farklı bir klasörken, bu işlemler kesilir. Bunu göstermek için `Admin`adlı bir alt klasör oluşturun. Sonra, `Admin` klasöre `Default.aspx` adlı bir içerik sayfası ekleyin ve yeni sayfayı `Site.master` ana sayfasına bağlamayı unutmayın.

> [!NOTE]
> [*Ana sayfada başlık, meta etiketler ve DIĞER HTML üst bilgilerini belirtme*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) öğreticisinde, içerik sayfasının başlığını (açıkça atanmamışsa) otomatik olarak ayarlamış `BasePage` adlı özel bir temel sayfa sınıfı oluşturduk. Yeni oluşturulan sayfanın arka plan kod sınıfının `BasePage`, bu işlevselliği kullanabilmesi için türemesini unutmayın.

Bu içerik sayfasını oluşturduktan sonra, Çözüm Gezgini Şekil 1 ' e benzer görünmelidir.

![Projeye yeni bir klasör ve ASP.NET sayfası eklendi](urls-in-master-pages-vb/_static/image1.png)

**Şekil 01**: projeye yeni bir klasör ve ASP.NET sayfası eklendi

Sonra, `Web.sitemap` dosyasını bu ders için yeni bir `<siteMapNode>` girişi içerecek şekilde güncelleştirin. Aşağıdaki XML, bir üçüncü `<siteMapNode>` öğesinin eklenmesini de içeren tüm `Web.sitemap` işaretlemesini gösterir.

[!code-xml[Main](urls-in-master-pages-vb/samples/sample3.xml)]

Yeni oluşturulan `Default.aspx` sayfasında, `Site.master`dört Contentfour öğesine karşılık gelen dört Içerik denetimi olmalıdır. Içerik denetimine, ContentPlaceHolder `MainContent` başvuran bir metin ekleyin ve ardından sayfayı bir tarayıcıdan ziyaret edin. Şekil 2 ' de gösterildiği gibi tarayıcı `PoweredByASPNET.gif` resim dosyasını bulamaz. Burada neler olacak?

`~/Admin/Default.aspx` içerik sayfası, `About.aspx` sayfası olduğu gibi `footerContent` bölge için aynı HTML 'i de gönderdi:

[!code-html[Main](urls-in-master-pages-vb/samples/sample4.html)]

`<img>` öğenin `src` özniteliği göreli bir URL olduğundan, tarayıcı web sayfasının klasör konumuna göre bir `Images` klasörü aramaya çalışır. Diğer bir deyişle, tarayıcı `Admin/Images/PoweredByASPNET.gif`resim dosyasını arıyor.

[PoweredByASPNET. gif görüntü dosyası bulunamıyor ![](urls-in-master-pages-vb/_static/image3.png)](urls-in-master-pages-vb/_static/image2.png)

**Şekil 02**: `PoweredByASPNET.gif` resim dosyası bulunamıyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](urls-in-master-pages-vb/_static/image4.png))

### <a name="replacing-relative-urls-with-absolute-urls"></a>Göreli URL 'Leri mutlak URL 'lerle değiştirme

Göreli bir URL 'nin tersi, eğik çizgiyle (`/`) veya `http://`gibi bir protokolle başlayan *mutlak BIR URL*'dir. Mutlak bir URL, bilinen bir sabit noktadan bir kaynağın konumunu belirttiğinden, Web sayfasının klasör yapısındaki konumundan bağımsız olarak, herhangi bir Web sayfasında aynı mutlak URL geçerli olur.

Şekil 2 ' de gösterilen bozuk görüntüyü onarmak için `<img>` öğenin `src` özniteliğini göreli bir URL yerine mutlak bir URL kullanacak şekilde güncelleştirmemiz gerekir. Doğru mutlak URL 'yi öğrenmek için Web sitenizdeki Web sayfalarından birini ziyaret edin ve adres çubuğunu inceleyin. Şekil 2 ' de adres çubuğu gösterdiği gibi, Web uygulaması için tam yol `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_VB/`. Bu nedenle, `<img>` öğenin `src` özniteliğini aşağıdaki iki mutlak URL 'Lerden birine güncelleştirebiliriz:

- `/ASPNET_MasterPages_Tutorial_04_VB/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_VB/Images/PoweredByASPNET.gif`

Yukarıda gösterilen formlardan birini kullanarak `<img>` öğenin `src` özniteliğini mutlak bir URL 'ye güncelleştirmek için bir dakikanızı ayırın ve ardından bir tarayıcıdan `~/Admin/Default.aspx` sayfasını ziyaret edin. Bu sefer tarayıcı `PoweredByASPNET.gif` resim dosyasını doğru bir şekilde bulup görüntüleyecektir (bkz. Şekil 3).

[PoweredByASPNET. gif görüntüsünü ![artık gösteriliyor](urls-in-master-pages-vb/_static/image6.png)](urls-in-master-pages-vb/_static/image5.png)

**Şekil 03**: `PoweredByASPNET.gif` resim artık görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](urls-in-master-pages-vb/_static/image7.png))

Mutlak URL 'de sabit kodlama çalışırken, HTML 'nizi Web sitesinin sunucu ve klasör konumuna sıkı bir şekilde bağar, bu da değişebilir. `http://localhost:3908/...` formun mutlak URL 'sini kullanmak, Visual Studio 'nun yerleşik ASP.NET Geliştirme Web sunucusu her başlatıldığında localhost 'tan önceki bağlantı noktası numarası otomatik olarak seçildiğinden Brittle. Benzer şekilde, `http://localhost` bölümü yalnızca yerel olarak test edilirken geçerlidir. Kod bir üretim sunucusuna dağıtıldıktan sonra, URL tabanı `http://www.yourserver.com`gibi başka bir şeye değişecektir. Formdaki mutlak URL, bu uygulama yolunun geliştirme ve üretim sunucuları arasında farklı olduğu için aynı britttasyon 'dan da fazla `/ASPNET_MasterPages_Tutorial_04_VB/...`.

İyi haber, ASP.NET çalışma zamanında geçerli bir göreli URL oluşturmak için bir yöntem sunar.

## <a name="usingandresolveclienturl"></a>`~`ve`ResolveClientUrl` kullanma

ASP.NET, mutlak bir URL yazmak yerine, sayfa geliştiricilerinin Web uygulamasının kökünü göstermek için tilde (`~`) kullanmasına izin verir. Örneğin, bu öğreticide daha önce `Admin` klasöründeki `Default.aspx` sayfasına başvurmak için metinde `~/Admin/Default.aspx` gösterimini kullandım. `~`, `Admin` klasörünün Web uygulamasının kökünün bir alt klasörü olduğunu gösterir.

`Control` sınıfının [`ResolveClientUrl` yöntemi](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx) bir URL alır ve denetimin bulunduğu Web sayfasına uygun GÖRELI bir URL 'ye değiştirir. Örneğin, `About.aspx` `ResolveClientUrl("~/Images/PoweredByASPNET.gif")` çağrısı `Images/PoweredByASPNET.gif`döndürür. Ancak `~/Admin/Default.aspx`' den çağırmak, `../Images/PoweredByASPNET.gif`döndürür.

> [!NOTE]
> Tüm ASP.NET Server denetimleri `Control` sınıfından türetiğinden, tüm sunucu denetimlerinin `ResolveClientUrl` metoduna erişimi vardır. `Page` sınıfı, `Control` sınıfından türetiliyor, yani bu yöntemi doğrudan ASP.NET sayfalarınızın arka plan kod sınıflarından kullanabilirsiniz.

### <a name="usingin-the-declarative-markup"></a>Bildirim temelli biçimlendirmede`~`kullanma

Birçok ASP.NET Web denetimi, URL ile ilgili özellikleri içerir: HyperLink denetimi bir `NavigateUrl` özelliğine sahiptir; Görüntü denetiminin bir `ImageUrl` özelliği vardır; vb. İşlendiğinde, bu denetimler URL ile ilgili özellik değerlerini `ResolveClientUrl`'e iletir. Sonuç olarak, bu özellikler Web uygulamasının kökünü göstermek için bir `~` içeriyorsa, URL geçerli bir göreli URL olarak değiştirilir.

Yalnızca ASP.NET Server denetimlerinin URL ile ilgili özelliklerinde `~` dönüştürdüğünü aklınızda bulundurun. `<img src="~/Images/PoweredByASPNET.gif" />`gibi statik HTML biçimlendirmesinde bir `~` görünürse, ASP.NET altyapısı, HTML içeriğinin geri kalanı ile birlikte `~` tarayıcıya gönderir. Tarayıcı `~` URL 'nin bir parçası olduğunu varsayar. Örneğin, tarayıcı biçimlendirmeyi alırsa `<img src="~/Images/PoweredByASPNET.gif" />` resim `PoweredByASPNET.gif`dosyasını içeren bir alt klasör `Images` `~` adında bir alt klasör olduğunu varsayar.

`Site.master`resim işaretlemesini onarmak için, var olan `<img>` öğesini bir ASP.NET Image Web denetimiyle değiştirin. Görüntü Web denetiminin `ID` `PoweredByImage`, `ImageUrl` özelliğini `~/Images/PoweredByASPNET.gif`ve `AlternateText` özelliğini "ASP.NET!" olarak güçlendirerek ayarlayın.

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample5.aspx)]

Ana sayfada bu değişikliği yaptıktan sonra `~/Admin/Default.aspx` sayfasını yeniden ziyaret edin. Bu kez `PoweredByASPNET.gif` resim dosyası sayfada görüntülenir (bkz. Şekil 3). Görüntü Web denetimi işlendiğinde, `ImageUrl` özellik değerini çözümlemek için `ResolveClientUrl` yöntemini kullanır. `~/Admin/Default.aspx`, aşağıdaki HTML kaynağı kod parçacığında gösterildiği gibi, `ImageUrl` uygun bir göreli URL 'ye dönüştürülür:

[!code-html[Main](urls-in-master-pages-vb/samples/sample6.html)]

> [!NOTE]
> URL tabanlı Web denetimi özelliklerinde kullanılmasına ek olarak, `~` `Response.Redirect` ve `Server.MapPath` yöntemleri çağrılırken de kullanılabilir. Ayrıca, `ResolveClientUrl` yöntemi, gerekirse doğrudan bir ASP.NET veya ana sayfanın bildirim temelli işaretten çağrılabilir; [biçimlendirme `ResolveClientUrl` kullanarak](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)bkz. [Fritz soğan](https://www.pluralsight.com/blogs/fritz/)günlüğü girişi.

## <a name="fixing-the-master-pages-remaining-relative-urls"></a>Ana sayfanın kalan göreli URL 'Leri düzeltiliyor

Yalnızca düzelttiğimiz `footerContent` `<img>` öğesine ek olarak ana sayfa, ilgilenmeniz gereken bir veya daha fazla göreli URL içerir. `topContent` bölge, `Default.aspx`işaret eden "Ana sayfa öğreticileri" bağlantısını içerir.

[!code-html[Main](urls-in-master-pages-vb/samples/sample7.html)]

Bu URL göreli olduğundan, kullanıcıyı ziyaret ettikleri içerik sayfasının klasöründe `Default.aspx` sayfasına gönderir. Bu bağlantının kök klasördeki `Default.aspx` her zaman işaret edebilmesi için, `~` gösterimini kullanabilmeniz için `<a>` öğesini bir köprü Web denetimiyle değiştirmeniz gerekir.

`<a>` öğesi işaretlemesini kaldırın ve onun yerine bir köprü denetimi ekleyin. Köprünün `ID` `lnkHome`, `NavigateUrl` özelliğini `~/Default.aspx`ve `Text` özelliğini "Ana sayfa öğreticileri" olarak ayarlayın.

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample8.aspx)]

İşte bu kadar! Bu noktada ana sayfamızda tüm URL 'Ler, ana sayfa ve içerik sayfasının bulunduğu klasörlere bakılmaksızın bir içerik sayfası tarafından işlendiğinde doğru bir şekilde temel alınır.

### <a name="automatic-url-resolution-in-theheadsection"></a>`<head>`bölümünde otomatik URL çözümlemesi

[*Ana sayfaları kullanarak site genelinde düzen oluşturma*](creating-a-site-wide-layout-using-master-pages-vb.md) öğreticisinde, `<head>` bölgesindeki `Styles.css` dosyasına bir `<link>` ekledik:

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample9.aspx)]

`<link>` öğenin `href` özniteliği göreli olsa da, çalışma zamanında otomatik olarak uygun bir yola dönüştürülür. [*Ana sayfa öğreticisindeki başlık, meta etiketler ve DIĞER HTML üst bilgilerini belirtme*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) konusunda anlatıldığı gibi, `<head>` bölgesi aslında sunucu tarafında bir denetimdir ve bu da, işlendiğinde iç denetimlerin içeriğini değiştirmesine olanak sağlar.

Bunu doğrulamak için `~/Admin/Default.aspx` sayfasını ziyaret edin ve tarayıcıya gönderilen HTML kaynağını görüntüleyin. Aşağıdaki kod parçacığında gösterildiği gibi, `<link>` öğenin `href` özniteliği uygun göreli bir URL 'ye `../Styles.css`otomatik olarak değiştirilmiştir.

[!code-html[Main](urls-in-master-pages-vb/samples/sample10.html)]

## <a name="summary"></a>Özet

Ana sayfalar genellikle bağlantılar, görüntüler ve bir URL aracılığıyla belirtilmesi gereken diğer dış kaynakları içerir. Ana sayfa ve içerik sayfaları aynı klasörde bulunmayabilir, göreli URL 'Lerin kullanılması önemlidir. Sabit kodlanmış mutlak URL 'Ler kullanılması mümkün olsa da, bu, Web uygulamasına mutlak URL 'YI sıkı bir şekilde bağar. Mutlak URL değişirse (genellikle bir Web uygulamasını taşırken veya dağıttığınızda), geri dönüp mutlak URL 'Leri güncelleştirmeniz gerekir.

İdeal yaklaşım, uygulama kökünü göstermek için tilde (`~`) kullanmaktır. URL ile ilgili özellikler içeren ASP.NET Web denetimleri, `~` çalışma zamanında uygulama köküne eşler. Dahili olarak, Web denetimleri, geçerli bir göreli URL oluşturmak için `Control` sınıfının `ResolveClientUrl` yöntemini kullanır. Bu yöntem, her sunucu denetiminden (`Page` sınıfı dahil) herkese açık ve kullanılabilir hale gelir. böylece, gerekirse arka plan kod sınıflarınızda program aracılığıyla kullanabilirsiniz.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET 'deki ana sayfalar](http://www.odetocode.com/Articles/419.aspx)
- [Ana sayfada URL yeniden Temellendiriliyor](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [Biçimlendirme içinde `ResolveClientUrl` kullanma](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)
> [İleri](control-id-naming-in-content-pages-vb.md)
