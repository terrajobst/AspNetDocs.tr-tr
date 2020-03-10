---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: Ana sayfaları ve partileri kullanarak Kullanıcı arabirimini yeniden kullanma | Microsoft Docs
author: microsoft
description: Adım 7 ' de, kısmi görünüm şablonları ve ana sayfalar kullanarak kod yinelemeyi ortadan kaldırmak için görünüm Şablonlarımızda ' Kuru prensibi ' uygulayabildiğimiz yöntemlere bakar.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580334"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>Ana Sayfaları ve Kısmi Bölümleri Kullanarak Kullanıcı Arabirimini Yeniden Kullanma

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) adım 7 ' dir.
> 
> Adım 7, kısmi görünüm şablonları ve ana sayfalar kullanarak kod yinelemeyi ortadan kaldırmak için görünüm Şablonlarımızda "Kuru prensibi" uygulayabildiğimiz yöntemlere bakar.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-7-partials-and-master-pages"></a>Nerdakşam yemeği 7. Adım: partileri ve ana sayfalar

Design felsefeleri ASP.NET MVC emayraçlarından biri, "kendinizi Yinelemeyin" prensibi (genellikle "kuru" olarak adlandırılır). KURUTMA tasarımı, uygulamanın daha hızlı derlenmesi ve bakımının daha kolay hale gelmesini sağlayan kod ve mantık çoğaltmasını ortadan kaldırmaya yardımcı olur.

Nerdakşam yemeği senaryolarımızın birkaç bölümünde uygulanan kurutma ilkesini zaten gördük. Birkaç örnek: doğrulama mantığımız, denetleyicimizde hem düzenleme hem de oluşturma senaryolarında uygulanmasını sağlayan model katmanımız içinde uygulanır; Düzenleme, Ayrıntılar ve silme eylemi yöntemlerinde "NotFound" görünüm şablonunu yeniden kullanıyoruz; Görünüm şablonlarımızla bir kural adlandırma modelini kullanıyoruz. Bu, View () yardımcı yöntemini çağırdığımız sırada adı açıkça belirtme ihtiyacını ortadan kaldırır; hem düzenleme hem de oluşturma eylemi senaryoları için DinnerFormViewModel sınıfını yeniden kullanacağız.

Şimdi de, kod çoğaltmayı da ortadan kaldırmak için görünüm Şablonlarımızda "Kuru prensibi" uygulayabildiğimiz yöntemlere göz atalım.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>Düzenleme ve oluşturma görünüm şablonlarımızı yeniden ziyaret edin

Şu anda, akşam yemeği form Kullanıcı arabirimimizi görüntülemek için iki farklı görünüm şablonu kullanıyoruz: "Edit. aspx" ve "Create. aspx". Bunların hızlı bir şekilde karşılaştırılması, ne kadar benzer olduğunu vurgular. Aşağıda, oluşturma formu şöyle görünür:

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

"Düzenleme" formumuz şöyle görünür:

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

Farklılık büyük bir fark değil mi? Başlık ve başlık metni dışında, form düzeni ve giriş denetimleri de aynıdır.

"Edit. aspx" ve "Create. aspx" şablonlarını açdığımızda, aynı form düzeni ve giriş denetimi kodu içerdiğini bulacağız. Bu yineleme, yeni bir akşam yemeği özelliği oluşturduğumuza veya değiştirdiğimiz her yerde değişiklik yapmak için gereken bir şey olduğu anlamına gelir.

### <a name="using-partial-view-templates"></a>Kısmi görünüm şablonları kullanma

ASP.NET MVC, bir sayfanın alt bölümü için Görünüm işleme mantığını kapsüllemek üzere kullanılabilecek "kısmi görünüm" şablonları tanımlama yeteneğini destekler. "Partileri", Görünüm işleme mantığını bir kez tanımlamak için kullanışlı bir yol sağlar ve bunu bir uygulama genelinde birden fazla yerde yeniden kullanın.

Edit. aspx ve Create. aspx görünüm şablonu çoğalttığımız "kurma" konusunda yardımcı olmak için, form düzeni ve giriş öğelerini her ikisi için de kapsülleyen "DinnerForm. ascx" adlı kısmi bir görünüm şablonu oluşturarız. Bunu,/views/dinetleri dizinimize sağ tıklayıp "Ekle-&gt;görünümü" menü komutunu seçerek yapacağız:

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

"Görünüm Ekle" iletişim kutusu görüntülenir. "DinnerForm" oluşturmak istediğimiz yeni görünümü adlandırın, iletişim kutusunda "kısmi görünüm oluştur" onay kutusunu işaretleyin ve bunu bir DinnerFormViewModel sınıfı geçitireceğiz belirtir:

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

"Ekle" düğmesine tıkladığımızda, Visual Studio "\Views\dıntik" dizininde bizimle ilgili yeni bir "DinnerForm. ascx" görünüm şablonu oluşturacaktır.

Daha sonra, Edit. aspx/Create. aspx görünüm şablonlarımızdan yinelenen form düzeni/giriş denetimi kodunu yeni "DinnerForm. ascx" kısmi görünüm şablonumuza kopyalayabilir/yapıştırabilirsiniz:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

Daha sonra, DinnerForm kısmi şablonunu çağırmak ve form yinelemesi kaldırmak için düzenleme ve oluşturma görünüm şablonlarımızı güncelleştirebiliriz. Bunu, görünüm şablonlarımız içinde HTML. RenderPartial ("DinnerForm") çağırarak yapabiliriz:

##### <a name="createaspx"></a>. Aspx oluştur

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

HTML. RenderPartial çağrılırken istediğiniz kısmi şablonun yolunu açıkça niteleyebilirsiniz (örneğin: ~ views/dinler/DinnerForm. ascx "). Yukarıdaki kodumuza karşın, ASP.NET MVC içindeki kural tabanlı adlandırma düzeninden faydalanır ve yalnızca "DinnerForm" öğesini işlemek için kısmi ad olarak belirttik. Bunu yaptığımızda, MVC ilk olarak kural tabanlı görünümler dizininde görünür (Bu, DinnersController için/views/dinlenebilir). Kısmi şablonu bulamazsa, bu durumda/Views/Shared dizininde arama yapılır.

HTML. RenderPartial () yalnızca kısmi görünümün adı ile çağrıldığında, ASP.NET MVC, çağıran görünüm şablonu tarafından kullanılan model ve ViewData sözlük nesnelerini kısmi görünüme geçicektir. Alternatif olarak, kullanılacak kısmi görünüm için alternatif bir model nesnesi ve/veya ViewData sözlüğü geçirmenize olanak sağlayan HTML. RenderPartial () öğesinin aşırı yüklenmiş sürümleri vardır. Bu, yalnızca tam model/ViewModel 'in bir alt kümesini geçirmek istediğiniz senaryolar için yararlıdır.

| **Kenar konusu: neden%%&gt; &lt;% =%&gt;&lt;değil?** |
| --- |
| Yukarıdaki kod ile fark etmiş olabileceğiniz hafif şeylerden biri, HTML. RenderPartial () çağrılırken &lt;% =%&gt; bloğu yerine%%&gt; bloğunu kullandığımızda &lt;. ASP.NET içindeki% =%&gt; blokları, bir geliştiricinin belirtilen bir değeri (örneğin: &lt;% = "Hello"%&gt; "Hello") işlemesini istediğini gösterir. &lt; Bunun yerine &lt;%%&gt; blokları, geliştiricinin kod yürütmek istediğini ve bunların içindeki tüm işlenmiş çıkışın açıkça yapılması gerektiğini belirtir (örneğin: &lt;% Response. Write ("Hello")%&gt;. Yukarıdaki HTML. RenderPartial kodu ile &lt;%%&gt; bloğunu kullandığımızda, HTML. RenderPartial () yönteminin bir dize döndürmediği ve bunun yerine içeriği doğrudan çağıran görünüm şablonunun çıkış akışına çıktısı almamız gerekir. Bunu performansı verimlilik nedenleriyle yapar ve bunu yaparak, (potansiyel olarak çok büyük) geçici bir dize nesnesi oluşturma gereksinimini ortadan kaldırır. Bu, bellek kullanımını azaltır ve genel uygulama verimini geliştirir. HTML. RenderPartial () kullanılırken yaygın bir hata, çağrının sonuna noktalı virgül eklemeyi unutmak için &lt;%%&gt; bloğunun içinde. Örneğin, bu kod bir derleyici hatasına neden olur: &lt;% HTML. RenderPartial ("DinnerForm")%&gt; yazmanız gerekir: &lt;% HTML. RenderPartial ("DinnerForm"); %&gt; bunun nedeni,%%&gt; bloklarının &lt;bağımsız kod deyimleri olması ve kod deyimlerinin kullanılması C# için noktalı virgül ile sonlandırılmalıdır. |

### <a name="using-partial-view-templates-to-clarify-code"></a>Kodu netleştirmek için kısmi görünüm şablonları kullanma

Birden çok yerde Görünüm işleme mantığını çoğaltmaktan kaçınmak için "DinnerForm" kısmi görünüm şablonunu oluşturduk. Bu, kısmi görünüm şablonları oluşturmanın en yaygın nedenidir.

Bazen yalnızca tek bir yerde çağrıldıklarında bile kısmi görünümler oluşturmak mantıklı olur. Çok karmaşık görünüm şablonları, genellikle görünüm işleme mantığı ayıklandığında ve kısmi şablonlarda bir veya daha fazla şekilde bölümlendiğinde okunması çok daha kolay hale gelebilir.

Örneğin, projemizdeki site. master dosyasından aşağıdaki kod parçacığını göz önünde bulundurun (kısa süre içinde ekleyeceğiz). Kod görece düz olarak okunabilir – kısmi olarak, ekranın sağ üst köşesinde bir oturum açma/kapatma bağlantısı görüntüleme mantığı "LogOnUserControl" kısmi içinde kapsüllenir.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

Bir görünüm şablonu içindeki HTML/kod işaretlemesini anlamaya çalışırken ne olursa olsun, bir kısmı ayıklanmışsa daha açık olup olmadığını ve iyi adlandırılmış kısmi görünümlere yeniden düzenlenmiş göz önünde bulundurun.

### <a name="master-pages"></a>Ana Sayfalar

ASP.NET MVC, kısmi görünümleri desteklemeye ek olarak, bir sitenin ortak düzen ve üst düzey HTML 'ini tanımlamak için kullanılabilecek "Ana sayfa" şablonları oluşturma özelliğini de destekler. İçerik yer tutucusu denetimleri daha sonra, görünümler tarafından geçersiz kılınabilen veya "doldurulan" değiştirilebilir bölgeleri belirlemek için ana sayfaya eklenebilir. Bu, bir uygulama genelinde ortak bir düzen uygulamak için çok etkili (ve kuru) bir yol sağlar.

Varsayılan olarak, yeni ASP.NET MVC projelerinin otomatik olarak bunlara eklenmiş bir ana sayfa şablonu vardır. Bu ana sayfa "site. Master" olarak adlandırılmıştır ve \Views\Shared\ klasörü içinde bulunur:

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

Varsayılan site. master dosyası aşağıdaki gibi görünür. Üst kısımdaki gezinme için bir menü ile birlikte sitenin dış HTML 'sini tanımlar. İki değiştirilebilir içerik yer tutucu denetimi içerir – biri başlık için, diğeri ise sayfanın birincil içeriğinin değiştirilmeleridir:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

Nerdakşam yemeği uygulamamız için oluşturduğumuz tüm Görünüm şablonları ("Listeleme", "Ayrıntılar", "Düzenle", "oluşturma", "NotFound" vb.) Bu site. Master şablonunu temel alır. Bu, "Görünüm Ekle" iletişim kutusunu kullanarak Görünümlerimizi oluşturduğumuzda, varsayılan olarak en üstteki &lt;% @ Page%&gt; yönergesine eklenen "MasterPageFile" özniteliği aracılığıyla belirtilir:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

Bunun anlamı, site. Master içeriğini değiştirebilmemiz ve değişikliklerin otomatik olarak uygulanmasını ve görünüm şablonlarımızdan herhangi birini oluşturduğumuzda kullanılmasını sağlayabilir.

Sitemizi "My MVC Uygulamam" yerine "Nerdakşam yemeği" olması için sitemizi ana başlık bölümünü güncelleştirelim. Ayrıca, ilk sekmenin "akşam yemeği bul" (HomeController dizini () eylem yöntemi tarafından işlenir) ve "akşam yemeği ana bilgisayarı" adlı yeni bir sekme ekleyebilmesini sağlamak için gezinti menümüzü güncelleştirelim:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Site. Master dosyasını kaydettiğimde ve tarayıcımızı yenilediğimde, üst bilgi değişikliklerimizi uygulamamız içindeki tüm görünümlerde göstereceğiz. Örneğin:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

*/Dinners/Edit/[kimlik]* URL 'si ile:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>Sonraki adım

Partileri ve ana sayfalar, görünümleri düzgün bir şekilde düzenlemenizi sağlayan çok esnek seçenekler sağlar. İçeriği ve kodu çoğaltmaktan kaçınmanıza ve görünüm şablonlarınızı okumayı ve bakımını daha kolay hale getirmenize yardımcı olduklarını göreceksiniz.

Şimdi, daha önce oluşturduğumuz listeleme senaryosunu yeniden ziyaret edin ve ölçeklenebilir sayfalama desteğini etkinleştirin.

> [!div class="step-by-step"]
> [Önceki](use-viewdata-and-implement-viewmodel-classes.md)
> [İleri](implement-efficient-data-paging.md)
