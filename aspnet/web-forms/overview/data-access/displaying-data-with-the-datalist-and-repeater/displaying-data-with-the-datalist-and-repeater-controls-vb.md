---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
title: DataList ve Repeater denetimleri ile verileri görüntüleme (VB) | Microsoft Docs
author: rick-anderson
description: Önceki öğreticilerde, verileri göstermek için GridView denetimini kullandık. Bu öğreticiden başlayarak, ile ortak raporlama desenleri oluşturmayı inceleyeceğiz...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 58618954-a9ed-4ca0-8c2d-95a5ffd9c03e
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 4e7aaa1701da67aec61505b64a835ef41031bb13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626366"
---
# <a name="displaying-data-with-the-datalist-and-repeater-controls-vb"></a>DataList ve Repeater Denetimleri ile Verileri Görüntüleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe) veya [PDF 'yi indirin](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)

> Önceki öğreticilerde, verileri göstermek için GridView denetimini kullandık. Bu öğreticiden başlayarak, bu denetimlerle veri görüntüleme temelleri ile başlayarak, DataList ve Repeater denetimleriyle ortak raporlama desenleri oluşturma konusuna baktık.

## <a name="introduction"></a>Giriş

Son 28 öğreticilerinin tamamında tüm örneklerde, GridView denetimine açtık bir veri kaynağından birden çok kayıt görüntülenmesini sağladığımızda. GridView, veri kaynağındaki her kayıt için bir satır oluşturur ve kayıt s veri alanlarını sütunlarda görüntüler. GridView, verileri görüntülemeyi, sayfayı görüntülemeyi, sıralamayı, düzenlemeyi ve silmeyi kolaylaştırır; bu, görünümü bir bit kututur. Üstelik, GridView s yapısından sorumlu olan biçimlendirme sabittir. her bir kayıt için tablo satırı (`<tr>`) ve her bir alan için bir tablo hücresi (`<td>`) içeren bir HTML `<table>` vardır.

Birden çok kayıt görüntülenirken görünüm ve işlenmiş biçimlendirmede daha fazla özelleştirme sağlamak için ASP.NET 2,0, DataList ve Repeater denetimlerini (ikisi de ASP.NET sürüm 1. x içinde de mevcuttur) sunar. DataList ve Repeater denetimleri, içeriğini BoundFields, CheckBoxFields, ButtonFields, vb. yerine şablonları kullanarak işler. GridView gibi, DataList bir HTML `<table>`olarak işlenir, ancak her tablo satırı için birden çok veri kaynağı kaydının görüntülenmesine izin verir. Diğer yandan yineleyicisi, açıkça belirtdiklerinize göre ek biçimlendirme gerektirmez ve yapılan biçimlendirme üzerinde tam denetim gerektiğinde ideal bir adaydır.

Sonraki düzine veya bu öğreticilerde, verileri bu denetim şablonlarıyla görüntülemenin temel bilgileri ile başlayarak, DataList ve Repeater denetimleriyle ortak raporlama desenleri oluşturmaya bakacağız. Bu denetimlerin nasıl biçimlendirileceğini, DataList 'teki veri kaynağı kayıtlarının yerleşimini, ortak ana/Ayrıntılar senaryolarına, verileri düzenleme ve silme yollarını, kayıtları düzenleme ve silmeyi, kayıtlar arasında nasıl sayfa yapılacağını ve bu şekilde nasıl değiştirileceğini inceleyeceğiz.

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>1\. Adım: DataList ve Repeater öğretici Web sayfalarını ekleme

Bu öğreticiye başlamadan önce, bu öğretici için gereken ASP.NET sayfalarını ve DataList ve Repeater kullanarak verileri görüntüleme ile ilgili bir sonraki birkaç öğreticiyi eklemek için ilk olarak bir süre sürer. `DataListRepeaterBasics`adlı projede yeni bir klasör oluşturarak başlayın. Ardından, aşağıdaki beş ASP.NET sayfasını bu klasöre ekleyin ve bunların tümünün ana sayfayı kullanacak şekilde yapılandırıldığından `Site.master`:

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`

![DataListRepeaterBasics klasörü oluşturma ve öğretici ASP.NET sayfalarını ekleme](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image1.png)

**Şekil 1**: `DataListRepeaterBasics` bir klasör oluşturun ve öğretici ASP.NET sayfaları ekleyin

`Default.aspx` sayfasını açın ve `SectionLevelTutorialListing.ascx` Kullanıcı denetimini `UserControls` klasöründen tasarım yüzeyine sürükleyin. [Ana sayfalarda ve site gezinti](../introduction/master-pages-and-site-navigation-vb.md) öğreticisinde oluşturduğumuz bu kullanıcı denetimi, site haritasını numaralandırır ve bir madde işaretli listenin geçerli bölümündeki öğreticileri görüntüler.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image2.png)

**Şekil 2**: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png))

Madde işaretli listenin oluşturacağımız DataList ve yineleyici öğreticilerini görüntülemesi için, bunları site haritasına eklememiz gerekir. `Web.sitemap` dosyasını açın ve özel düğmeler site haritası düğüm işaretlemesini ekleme ' den sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample1.xml)]

![Site haritasını yeni ASP.NET sayfalarını Içerecek şekilde Güncelleştir](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image5.png)

**Şekil 3**: site haritasını yeni ASP.NET sayfalarını içerecek şekilde güncelleştirin

## <a name="step-2-displaying-product-information-with-the-datalist"></a>2\. Adım: DataList ile ürün bilgilerini görüntüleme

FormView 'a benzer şekilde, DataList denetimi işlenen çıktı, BoundFields, CheckBoxFields vb. yerine şablonlara bağlıdır. FormView 'un aksine, DataList bir kayıt kümesini bir dizi değil göstermek üzere tasarlanmıştır. Bu öğreticiye ürün bilgilerini bir DataList 'e bağlamayı göz atalım. `DataListRepeaterBasics` klasöründeki `Basics.aspx` sayfasını açarak başlayın. Sonra, araç kutusundan bir DataList ' i tasarımcı üzerine sürükleyin. Şekil 4 ' ün gösterdiği gibi, DataList s şablonlarını belirtmeden önce tasarımcı bunu gri bir kutu olarak görüntüler.

[![DataList 'ı araç kutusundan Tasarımcı üzerine sürükleyin](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image6.png)

**Şekil 4**: DataList 'ı araç kutusundan Tasarımcı üzerine sürükleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png))

DataList s akıllı etiketinden yeni bir ObjectDataSource ekleyin ve onu `ProductsBLL` sınıf s `GetProducts` metodunu kullanacak şekilde yapılandırın. Bu öğreticide salt okunurdur bir DataList oluşturduğumuz için, sihirbaz s INSERT, UPDATE ve DELETE sekmelerinde açılan listeyi (None) olarak ayarlayın.

[Yeni bir ObjectDataSource oluşturmayı kabul ![](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image9.png)

**Şekil 5**: yeni bir ObjectDataSource oluşturmayı tercih etme ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png))

[![, ObjectDataSource 'ı ProductsBLL sınıfını kullanacak şekilde yapılandırma](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image12.png)

**Şekil 6**: `ProductsBLL` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png))

[GetProducts metodunu kullanarak tüm ürünlerle Ilgili bilgileri almak ![](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image15.png)

**Şekil 7**: `GetProducts` yöntemi kullanarak tüm ürünlerle ilgili bilgileri alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png))

ObjectDataSource 'ı yapılandırdıktan ve akıllı etiketi aracılığıyla DataList ile ilişkilendirdikten sonra Visual Studio, DataList 'te veri kaynağı tarafından döndürülen her bir veri alanının adını ve değerini görüntüleyen bir `ItemTemplate` otomatik olarak oluşturur (aşağıdaki biçimlendirmeye bakın). Bu varsayılan `ItemTemplate` görünümü, bir veri kaynağını Tasarımcı aracılığıyla FormView 'a bağlarken otomatik olarak oluşturulan şablonlarınızla aynıdır.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample2.aspx)]

> [!NOTE]
> FormView 'un akıllı etiketi aracılığıyla bir FormView denetimine veri kaynağı bağlarken, Visual Studio 'Nun bir `ItemTemplate`, `InsertItemTemplate`ve `EditItemTemplate`oluşturduğunu hatırlayın. Ancak, DataList ile yalnızca bir `ItemTemplate` oluşturulur. Bunun nedeni, DataList 'in, FormView tarafından sunulan aynı yerleşik düzenlemeyle ve ekleme desteğiyle aynı olmasından kaynaklanır. DataList, düzenleme ve silme ile ilgili olayları içerir, düzenleme ve silme desteği bir kodla birlikte eklenebilir, ancak FormView ile birlikte basit bir hazır olmayan destek yoktur. Daha sonraki bir öğreticide DataList ile nasıl düzen ve silme desteği ekleneceğini inceleyeceğiz.

Bu şablonun görünümünü geliştirmek için biraz zaman atalım. Tüm veri alanlarını görüntülemek yerine, s yalnızca ürün adı, tedarikçi, kategori, birim başına miktar ve birim fiyat ' ı görüntüler. Ayrıca, bir `<h4>` başlığında adı görüntülemesine ve başlığın altındaki bir `<table>` kullanarak kalan alanları yerleştirelim.

Bu değişiklikleri yapmak için, DataList s akıllı etiketinden tasarımcı içindeki şablon düzenleme özelliklerini kullanarak Şablonları Düzenle bağlantısına tıklayabilir veya sayfa bildirimli sözdizimi aracılığıyla şablonu el ile değiştirebilirsiniz. Tasarımcıda Şablonları Düzenle seçeneğini kullanırsanız, elde edilen biçimlendirme aşağıdaki işaretle tam olarak eşleşmeyebilir, ancak bir tarayıcı ile görüntülendiğinde Şekil 8 ' de gösterilen ekran görüntüsüne çok benzer görünmelidir.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample3.aspx)]

> [!NOTE]
> Yukarıdaki örnekte, `Text` özelliğine, veri bağlama söz dizimi değeri atanmış olan etiket Web denetimleri kullanılmaktadır. Alternatif olarak, yalnızca veri bağlama söz dizimini yazarak etiketi tamamen kaçırdık. Diğer bir deyişle, `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />` kullanmak yerine, bildirim temelli söz dizimi `<%# Eval("CategoryName") %>`kullandık.

Ancak, etiket Web denetimlerinde ayrıldığınızda iki avantaj sunun. İlk olarak, bir sonraki öğreticide göreceğiniz gibi verileri temel alarak verileri biçimlendirmede daha kolay bir yol sunar. İkincisi, tasarımcıda Şablonları Düzenle seçeneği, bazı Web denetimleri dışında görüntülenen bildirime dayalı veri bağlama söz dizimini göstermez. Bunun yerine, Şablonları Düzenle arabirimi statik biçimlendirme ve Web denetimleriyle çalışmayı kolaylaştırmak için tasarlanmıştır ve Web denetimleri akıllı etiketleri 'nden erişilebilen, DataBindings 'i Düzenle iletişim kutusu aracılığıyla herhangi bir veri bağlama yapılacağını kabul eder.

Bu nedenle, şablonları tasarımcı aracılığıyla düzenleme seçeneği sunan DataList ile çalışırken, içeriğe düzenleme şablonları arabirimi aracılığıyla erişilebilmesi için etiket Web denetimlerini kullanmayı tercih ediyorum. Daha kısa bir süre içinde göreceğiniz gibi, Yineleyici, şablon içeriklerinin kaynak görünümünden düzenlenmesini gerektirir. Sonuç olarak, Repeater s şablonlarının oluşturulması sırasında, veri bağlı metnin görünüşünü programlama mantığına göre biçimlendirmek istiyorum gibi, genellikle etiketi Web denetimlerini atlıyorum.

[![her bir ürün çıkışı, DataList s ItemTemplate kullanılarak Işlenir](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image18.png)

**Şekil 8**: her ürün çıkışı, DataList s `ItemTemplate` kullanılarak işlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png))

## <a name="step-3-improving-the-appearance-of-the-datalist"></a>3\. Adım: DataList 'in görünüşünü geliştirme

GridView gibi, DataList, `Font`, `ForeColor`, `BackColor`, `CssClass`, `ItemStyle`, `AlternatingItemStyle`, `SelectedItemStyle`vb. gibi bir dizi stille ilgili özellikler sunar. GridView ve DetailsView denetimleriyle çalışırken, bu iki denetim için `CssClass` özellikleri ve alt özelliklerinin (`RowStyle`, `HeaderStyle`, vb.) `CssClass` özelliği için önceden tanımlanmış olan `DataWebControls` temasının dış görünüm dosyaları oluşturduk. DataList için aynı şekilde bakalım.

[ObjectDataSource Ile verileri görüntüleme](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) öğreticisinde açıklandığı gibi, bir dış görünüm dosyası bir Web denetimi için varsayılan görünümle ilgili özellikleri belirtir; bir tema, bir Web sitesi için belirli bir görünümü tanımlayan bir kaplama, CSS, resim ve JavaScript dosyaları koleksiyonudur. *ObjectDataSource Ile verileri görüntüleme* öğreticisinde, şu anda, Iki dış görünüm dosyası olan `GridView.skin` ve `DetailsView.skin`olan bir `DataWebControls` teması (`App_Themes` klasörü içinde bir klasör olarak uygulanır) oluşturduk. DataList için önceden tanımlanmış stil ayarlarını belirtmek üzere bir üçüncü Skin dosyası ekleyelim.

Bir dış görünüm dosyası eklemek için `App_Themes/DataWebControls` klasörüne sağ tıklayın, yeni öğe Ekle ' yi seçin ve listeden dış görünüm dosyası seçeneğini belirleyin. Dosyayı `DataList.skin` olarak adlandırın.

[![DataList. Skin adlı yeni bir kaplama dosyası oluşturma](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image21.png)

**Şekil 9**: `DataList.skin` adlı yeni bir dış görünüm dosyası oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png))

`DataList.skin` dosyası için aşağıdaki biçimlendirmeyi kullanın:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample4.aspx)]

Bu ayarlar, GridView ve DetailsView denetimleriyle kullanılan uygun DataList özelliklerine aynı CSS sınıflarını atar. Burada kullanılan CSS sınıfları `Styles.css` dosyasında tanımlanır ve önceki öğreticilere eklenmiştir `RowStyle``AlternatingRowStyle``DataWebControlStyle`.

Bu kaplama dosyasının eklenmesi sayesinde, DataList s görünümü tasarımcıda güncelleştirilir (yeni kaplama dosyasının etkilerini görmek için tasarımcı görünümünü yenilemeniz gerekebilir; Görünüm menüsünden Yenile ' yi seçin). Şekil 10 ' da gösterildiği gibi, değişen her ürünün açık pembe bir arka plan rengi vardır.

[![DataList. Skin adlı yeni bir kaplama dosyası oluşturma](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image24.png)

**Şekil 10**: `DataList.skin` adlı yeni bir dış görünüm dosyası oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png))

## <a name="step-4-exploring-the-datalist-s-other-templates"></a>4\. Adım: DataList 'leri diğer şablonları keşfetme

DataList, `ItemTemplate`ek olarak isteğe bağlı altı şablonu destekler:

- `HeaderTemplate`, çıkışa bir başlık satırı ekler ve bu satırı işlemek için kullanılır
- değişen öğeleri işlemek için kullanılan `AlternatingItemTemplate`
- Seçili öğeyi oluşturmak için kullanılan `SelectedItemTemplate`; Seçili öğe, dizini DataList s [`SelectedIndex` özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx) karşılık gelen öğedir
- düzenlenmekte olan öğeyi oluşturmak için kullanılan `EditItemTemplate`
- sağlanmışsa `SeparatorTemplate` her öğe arasında bir ayırıcı ekler ve bu ayırıcıyı işlemek için kullanılır
- `FooterTemplate`-sağlanmışsa, çıkışa bir altbilgi satırı ekler ve bu satırı işlemek için kullanılır

`HeaderTemplate` veya `FooterTemplate`belirtirken, DataList işlenen çıktıya ek bir üstbilgi veya altbilgi satırı ekler. GridView s üstbilgi ve altbilgi satırlarıyla benzer şekilde, bir DataList 'teki üst bilgi ve altbilgi veriye bağlanmaz. Bu nedenle, `HeaderTemplate` veya `FooterTemplate` ilişkili verilere erişmeye çalışır olan tüm veri bağlama söz dizimi boş bir dize döndürür.

> [!NOTE]
> [GridView s altbilgi öğreticisindeki Özet bilgileri görüntüleme](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) bölümünde gördüğünüz gibi, üstbilgi ve altbilgi satırları veri bağlama sözdizimini desteklemeyken, verilere özgü bilgiler gridview s `RowDataBound` olay işleyicisinden bu satırlara doğrudan eklenebilir. Bu teknik, denetim ile bağlantılı verilerden çalışan toplamları veya diğer bilgileri hesaplamak ve bu bilgiyi altbilgiye atamak için kullanılabilir. Aynı kavram DataList ve Repeater denetimlerine de uygulanabilir; Tek fark, DataList ve Repeater için `ItemDataBound` olayına yönelik bir olay işleyicisi oluşturma (`RowDataBound` olayı yerine).

Bizim örneğimizde, DataList 'in en üstünde görünen ürün bilgilerinin başlık `<h3>` başlığına sahip olmasına neden olur. Bunu gerçekleştirmek için, uygun biçimlendirmeye sahip bir `HeaderTemplate` ekleyin. Tasarımcı 'da bu, DataList s akıllı etiketinde Şablonları Düzenle bağlantısına tıklayıp açılan listeden üst bilgi şablonunu seçerek ve Stil açılır listesinden başlık 3 seçeneği belirlenerek metin yazarak gerçekleştirilebilir (bkz. Şekil 11).

[![metin ürün bilgileri ile HeaderTemplate ekleme](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image27.png)

**Şekil 11**: metin ürün bilgilerine sahip bir `HeaderTemplate` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png))

Alternatif olarak, `<asp:DataList>` etiketleri içinde aşağıdaki biçimlendirme girilerek bildirimli olarak eklenebilir:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample5.html)]

Her bir ürün listesi arasına bir boşluk eklemek için, her bölüm arasında bir çizgi içeren `SeparatorTemplate` ekler. Yatay kural etiketi (`<hr>`), böyle bir ayırıcı ekler. `SeparatorTemplate` aşağıdaki biçimlendirmeye sahip olacak şekilde oluşturun:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample6.html)]

> [!NOTE]
> `HeaderTemplate` ve `FooterTemplates`gibi, `SeparatorTemplate` veri kaynağından herhangi bir kayda bağlanamaz ve bu nedenle DataList 'e göre veri kaynağı kayıtlarına doğrudan erişemez.

Bu ekleme yapıldıktan sonra, sayfayı bir tarayıcı aracılığıyla görüntülerken, Şekil 12 ' ye benzer görünmelidir. Başlık satırına ve her ürün listesi arasındaki çizgiye göz önünde edin.

[DataList ![her ürün listesi arasında bir başlık satırı ve yatay bir kural Içerir](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image30.png)

**Şekil 12**: DataList, her ürün listesi arasında bir başlık satırı ve yatay kural içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png))

## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>5\. Adım: Yineleyici denetimiyle belirli bir biçimlendirmeyi Işleme

Şekil 12 ' den DataList örneğini ziyaret ederken tarayıcınızda bir görünüm/kaynak yaparsanız, DataList 'e bağlanan her öğe için tek bir tablo hücresi (`<td>`) içeren bir tablo satırı (`<tr>`) içeren bir HTML `<table>` yayar. Bu çıktı, aslında, tek bir TemplateField ile bir GridView 'dan yayıldıklarla aynıdır. Daha sonraki bir öğreticide göreceğiniz gibi DataList, çıktının daha fazla özelleştirilmesini sağlar ve tablo satırı başına birden çok veri kaynağı kaydını görüntülemenizi sağlar.

Yine de bir HTML `<table>`oluşturmak istemiyor musunuz? Bir veri Web denetimi tarafından oluşturulan biçimlendirme üzerinde toplam ve tam denetim için Yineleyici denetimini kullandık. DataList gibi, yineleyici şablonlar temel alınarak oluşturulur. Ancak yineleyicisi, yalnızca aşağıdaki beş şablonu sunar:

- sağlanırsa `HeaderTemplate`, belirtilen biçimlendirmeyi öğelerden önce ekler
- öğeleri işlemek için kullanılan `ItemTemplate`
- sağlanmışsa, değişen öğeleri işlemek için kullanılan `AlternatingItemTemplate`
- sağlanmışsa `SeparatorTemplate`, her öğe arasında belirtilen biçimlendirmeyi ekler
- `FooterTemplate`, belirtilen biçimlendirmeyi öğeden sonra ekler

ASP.NET 1. x ' de, verileri bazı veri kaynağından gelen madde işaretli bir listeyi görüntülemek için genellikle Yineleyici denetimi kullanılır. Böyle bir durumda `HeaderTemplate` ve `FooterTemplates`, sırasıyla, `ItemTemplate` veri bağlama söz dizimi ile `<li>` öğeleri içerdiğinde, açma ve kapatma `<ul>` etiketlerini içerir. Bu yaklaşım, [ana sayfalarda ve site gezinti](../introduction/master-pages-and-site-navigation-vb.md) öğreticisinde iki örnekte gördüğümüz için ASP.NET 2,0 ' de kullanılabilir.

- `Site.master` ana sayfasında, en üst düzey site haritası içeriğinin madde işaretli bir listesini (temel raporlama, filtreleme raporları, özelleştirilmiş biçimlendirme vb.) göstermek için bir yineleyici kullanıldı; üst düzey bölümlerin alt bölümlerini göstermek için bir diğeri, iç içe Yineleyici kullanıldı
- `SectionLevelTutorialListing.ascx`, geçerli site haritası bölümünün alt bölümlerinin madde işaretli listesini göstermek için bir yineleyici kullanıldı

> [!NOTE]
> ASP.NET 2,0, basit bir madde işaretli liste göstermek için bir veri kaynağı denetimine bağlanabilen yeni [BulletedList denetimini](https://msdn.microsoft.com/library/ms228101.aspx)tanıtır. BulletedList denetimiyle, listeyle ilgili HTML 'yi belirtmemiz gerekmez; Bunun yerine, her liste öğesi için metin olarak görüntülenecek veri alanını gösteririz.

Yineleyici, tüm verileri yakala Web denetimi görevi görür. Gerekli biçimlendirmeyi üreten mevcut bir denetim yoksa, yineleyici denetimi kullanılabilir. Yineleyicisi 'nin kullanımını anlamak için, adım 2 ' de oluşturulan ürün bilgisi DataList ' in üstünde görüntülenecek kategorilerin listesini sağlar. Özellikle, tek satırlık bir HTML `<table>`, tablodaki bir sütun olarak görüntülenmek üzere kategorilerin görüntülenmesini sağlayın.

Bunu gerçekleştirmek için, bir yineleyici denetimini araç kutusundan Tasarımcı üzerinde, ürün bilgisi DataList ' ten yukarıya sürükleyerek başlatın. DataList 'te olduğu gibi, yineleyici başlangıçta şablonlar tanımlanana kadar gri kutu olarak görüntülenir.

[Tasarımcıya Repeater eklemek ![](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image33.png)

**Şekil 13**: tasarımcıya bir yineleyici ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png))

Yineleyicisi 'nin akıllı etiketinde yalnızca bir seçenek bulunur: veri kaynağını seçin. Yeni bir ObjectDataSource oluşturmayı ve `CategoriesBLL` sınıf s `GetCategories` metodunu kullanacak şekilde yapılandırmayı tercih edin.

[Yeni bir ObjectDataSource ![oluşturma](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image36.png)

**Şekil 14**: yeni bir ObjectDataSource oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png))

[![, ObjectDataSource 'un CategoriesBLL sınıfını kullanacak şekilde yapılandırılması](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image39.png)

**Şekil 15**: `CategoriesBLL` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png))

[GetCategories yöntemini kullanarak kategorilerin tümü hakkında bilgi almak ![](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image42.png)

**Şekil 16**: `GetCategories` yöntemini kullanarak kategorilerin tümü hakkında bilgi alın ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png))

DataList 'in aksine, Visual Studio bir veri kaynağına bağladıktan sonra yineleyicisi için otomatik olarak ItemTemplate oluşturmaz. Ayrıca, Repeater 'lar şablonları tasarımcı aracılığıyla yapılandırılamaz ve bildirimli olarak belirtilmelidir.

Kategorileri her kategori için bir sütun ile tek satırlı `<table>` olarak göstermek için, aşağıdaki gibi işaretlemeleri yayan Yineleyici gerekir:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample7.html)]

`<td>Category X</td>` metin yinelenen bir bölüm olduğundan, bu, yineleyicisi tarafından ItemTemplate 'te görünür. `<table><tr>` önünde görünen biçimlendirme, son biçimlendirme-`</tr></table>`-`FooterTemplate`yerleştirileceği sırada `HeaderTemplate` yerleştirilecek. Bu şablon ayarlarını girmek için sol alt köşedeki Kaynak düğmesine tıklayarak ASP.NET sayfasının bildirim temelli kısmına gidin ve aşağıdaki söz dizimini yazın:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample8.aspx)]

Yineleyicisi, şablonları tarafından belirtilen kesin biçimlendirmeyi, hiçbir şey, hiçbir şeyi daha az bir biçimde yayar. Şekil 17, bir tarayıcı aracılığıyla görüntülenirken Repeater çıkışını gösterir.

[Tek satırlık HTML &lt;tablo ![&gt; her kategoriyi ayrı bir sütunda listeler](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image45.png)

**Şekil 17**: tek satırlık HTML `<table>` her kategoriyi ayrı bir sütunda listeler ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png))

## <a name="step-6-improving-the-appearance-of-the-repeater"></a>6\. Adım: yineleyicisi 'nin görünümünü geliştirme

Yineleyici tam olarak şablonlarının belirttiği biçimlendirmeyi gösterdiği için, Yineleyici için stille ilgili hiçbir özellik olmadığı bir beklenmedik şekilde gelmelidir. Yineleyicisi tarafından oluşturulan içeriğin görünümünü değiştirmek için, gerekli HTML veya CSS içeriğini doğrudan Yineleyici s şablonlarına el ile eklememiz gerekir.

Bizim örneğimizde, DataList 'teki değişen satırlarda olduğu gibi kategori sütunlarının alternatif arka plan rengine sahip olmasına izin verin. Bunu gerçekleştirmek için her Yineleyici öğesine `RowStyle` CSS sınıfını ve `AlternatingRowStyle` CSS sınıfına, `ItemTemplate` ve `AlternatingItemTemplate` şablonları aracılığıyla her bir yineleyicisi öğesine atamanız gerekir, örneğin:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample9.aspx)]

Ayrıca, çıkışa metin ürün kategorileriyle bir başlık satırı da ekleyelim. Sonuçta elde edilen `<table>` sütunların ne olduğunu bilmediğimiz için, tüm sütunları yayma garantisi olan bir üst bilgi satırını oluşturmanın en kolay yolu *iki* `<table>` s kullanmaktır. İlk `<table>`, üst bilgi satırı ve sistemdeki her kategori için bir sütun içeren ikinci ve tek satır `<table>` içeren bir satır içeren iki satır içerir. Diğer bir deyişle, aşağıdaki biçimlendirmeyi göstermek istiyoruz:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample10.html)]

Aşağıdaki `HeaderTemplate` ve `FooterTemplate` istenen biçimlendirmeye neden olacak:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample11.aspx)]

Şekil 18, bu değişiklikler yapıldıktan sonra yineleyicisi gösterir.

[Kategori sütunlarını arka plan rengine ![ve bir başlık satırı Içerir](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image48.png)

**Şekil 18**: Kategori sütunları arka plan rengine alternatif olarak bir başlık satırı içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png))

## <a name="summary"></a>Özet

GridView denetimi verileri görüntülemeyi, düzenlemeyi, silmeyi, sıralamayı ve sayfayı kullanarak görüntülemeyi kolaylaştırırken, görünüm çok boxy ve kılavuz benzeri olur. Görünüm üzerinde daha fazla denetim için, DataList veya Repeater denetimlerine açmanız gerekir. Bu denetimlerin her ikisi de BoundFields, CheckBoxFields vb. yerine şablonları kullanarak bir kayıt kümesi görüntüler.

`<table>` DataList, varsayılan olarak her bir veri kaynağı kaydını tek bir tablo satırında, tek bir TemplateField ile tıpkı bir GridView gibi görüntüler. Ancak, daha sonraki bir öğreticide göreceğiniz gibi DataList, her tablo satırı için birden çok kaydın görüntülenmesine izin verir. Diğer yandan yineleyicisi, kendi şablonlarında belirtilen biçimlendirmeyi kesinlikle yayar; ek biçimlendirme eklemez ve bu nedenle, verileri bir `<table>` dışındaki HTML öğelerinde (madde işaretli bir liste içinde) göstermek için yaygın olarak kullanılır.

DataList ve Repeater, işlenen çıktılarına daha fazla esneklik sunurken, GridView 'da bulunan yerleşik özelliklerin birçoğuna sahip olurlar. Yaklaşan öğreticilerde inceleyeceğiz, ancak bu özelliklerden bazıları çok fazla çaba olmadan yeniden takılabilir, ancak GridView yerine DataList veya Repeater kullanmanın, bu özellikleri uygulamak zorunda kalmadan kullanabileceğiniz özellikleri sınırlayacağını aklınızda bulundurun başınıza.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Yaakov Ellis, Liz Shulok, Randy SCHMIDT ve Stacy Park. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](nested-data-web-controls-cs.md)
> [İleri](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
