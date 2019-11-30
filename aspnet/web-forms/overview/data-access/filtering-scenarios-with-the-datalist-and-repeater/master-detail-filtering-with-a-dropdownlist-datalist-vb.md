---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: DropDownList Ile ana/ayrıntı filtreleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, ana/ayrıntı raporlarının ' Ana ' kayıtları ve bir DataList ' i Displ için görüntülemek üzere DropDownLists kullanarak tek bir Web sayfasında nasıl görüntüleneceğini görüyoruz.
ms.author: riande
ms.date: 07/18/2007
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 537f8e76bc0cbfa759a014b63ae5f68b5d3ca64d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74630022"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>Bir DropDownList ile Ana/Ayrıntı Filtreleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe) veya [PDF 'yi indirin](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)

> Bu öğreticide, "Ayrıntılar" görüntülemek için "ana" kayıtları ve bir DataList listesini görüntülemek için DropDownLists kullanarak ana/ayrıntı raporlarının tek bir Web sayfasında nasıl görüntüleneceğini görüyoruz.

## <a name="introduction"></a>Giriş

İlk olarak bir [DropDownList öğreticisi ile önceki ana/ayrıntı filtrelemesinde](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) bir GridView kullanarak oluşturduğumuz ana/ayrıntı raporu, bazı "ana" kayıt kümesini göstererek başlar. Kullanıcı daha sonra Ana kayıtlardan birinin detayına gidebilir ve bu sayede ana kaydın "ayrıntılarını" görüntülüyor olabilir. Ana/ayrıntı raporları, bire çok ilişkileri görselleştirmede ve özellikle "geniş" tablolarda (çok sayıda sütun içeren) ayrıntılı bilgiler görüntülemek için ideal bir seçimdir. Önceki öğreticilerdeki GridView ve DetailsView denetimlerini kullanarak ana/ayrıntı raporlarının nasıl uygulanacağını araştırtık. Bu öğreticide ve sonraki iki adımda bu kavramları yeniden inceleyeceğiz, ancak bunun yerine DataList ve Repeater denetimlerini kullanmaya odaklanacağız.

Bu öğreticide, "Ayrıntılar" kayıtları bir DataList 'te görüntülenecek şekilde "ana" kayıtları içeren bir DropDownList kullanma bölümüne bakacağız.

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>1\. Adım: ana/ayrıntılı öğretici Web sayfalarını ekleme

Bu öğreticiye başlamadan önce, bu öğretici için ihtiyaç duyduğumuz klasörü ve ASP.NET sayfalarını ve DataList ve Repeater denetimlerini kullanarak ana/ayrıntı raporlarıyla ilgili bir sonraki iki sayfayı eklemek için bir dakikanızı atalım. `DataListRepeaterFiltering`adlı projede yeni bir klasör oluşturarak başlayın. Ardından, aşağıdaki beş ASP.NET sayfasını bu klasöre ekleyin ve bunların tümünün ana sayfayı kullanacak şekilde yapılandırıldığından `Site.master`:

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`

![DataListRepeaterFiltering klasörü oluşturma ve öğretici ASP.NET sayfalarını ekleme](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

**Şekil 1**: `DataListRepeaterFiltering` bir klasör oluşturun ve öğretici ASP.NET sayfaları ekleyin

Sonra, `Default.aspx` sayfasını açın ve `SectionLevelTutorialListing.ascx` Kullanıcı denetimini `UserControls` klasöründen tasarım yüzeyine sürükleyin. [Ana sayfalarda ve site gezinti](../introduction/master-pages-and-site-navigation-vb.md) öğreticisinde oluşturduğumuz bu kullanıcı denetimi, site haritasını numaralandırır ve bir madde işaretli listenin geçerli bölümündeki öğreticileri görüntüler.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)

**Şekil 2**: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))

Madde işaretli listenin oluşturacağımız ana/ayrıntı öğreticilerini görüntülemesi için, bunları site haritasına eklememiz gerekir. `Web.sitemap` dosyasını açın ve "DataList ve Repeater ile verileri görüntüleme" site haritası düğümü işaretlemesini sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]

![Site haritasını yeni ASP.NET sayfalarını Içerecek şekilde Güncelleştir](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

**Şekil 3**: site haritasını yeni ASP.NET sayfalarını içerecek şekilde güncelleştirin

## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>2\. Adım: bir DropDownList içindeki kategorileri görüntüleme

Ana/ayrıntı raporumuz, seçilen liste öğesinin ürünlerini bir DataList 'teki sayfada daha aşağı görüntülenecek şekilde bir DropDownList içindeki kategorileri listeleyecektir. İlk görevinin önünde ve sonra, kategorilerin bir DropDownList içinde gösterilmesi gerekir. `FilterByDropDownList.aspx` sayfasını `DataListRepeaterFiltering` klasöründe açıp araç kutusundan bir DropDownList öğesini sayfanın tasarımcısına sürükleyin. Sonra, DropDownList 'in `ID` özelliğini `Categories`olarak ayarlayın. DropDownList 'in akıllı etiketindeki veri kaynağı Seç bağlantısına tıklayın ve `CategoriesDataSource`adlı yeni bir ObjectDataSource oluşturun.

[![CategoriesDataSource adlı yeni bir ObjectDataSource ekleyin](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)

**Şekil 4**: `CategoriesDataSource` adlı yeni bir ObjectDataSource ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))

Yeni ObjectDataSource 'ı, `CategoriesBLL` sınıfının `GetCategories()` yöntemini çağırdığı şekilde yapılandırın. ObjectDataSource yapılandırıldıktan sonra, hangi veri kaynağı alanının DropDownList 'de gösterilmesi gerektiğini ve hangilerinin her bir liste öğesi için değer olarak ilişkilendirilmesi gerektiğini belirtmemiz gerekir. `CategoryName` alanı görüntüleme ve her liste öğesi için değer olarak `CategoryID`.

[DropDownList 'In CategoryName alanını görüntülemesi ve değer olarak CategoryID 'yi kullanması ![](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)

**Şekil 5**: DropDownList 'In `CategoryName` alanı göstermesini ve değer olarak `CategoryID` kullanmasına[izin vermek (tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))

Bu noktada, `Categories` tablodaki kayıtlarla doldurulmuş bir DropDownList denetimine sahip olduğumuz (hepsi yaklaşık altı saniye içinde gerçekleştirilir). Şekil 6 ' da bir tarayıcıdan görüntülendiklerinde ilerleme durumunu gösterir.

[aşağı açılan liste ![geçerli Kategoriler](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)

**Şekil 6**: bir açılan listede geçerli Kategoriler listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))

## <a name="step-2-adding-the-products-datalist"></a>2\. Adım: ürün DataList 'i ekleme

Ana/ayrıntı raporumuzdaki son adım, seçili kategoriyle ilişkili ürünleri listeleriydi. Bunu gerçekleştirmek için, sayfaya bir DataList ekleyin ve `ProductsByCategoryDataSource`adlı yeni bir ObjectDataSource oluşturun. `ProductsByCategoryDataSource` denetiminin verilerini `ProductsBLL` sınıfının `GetProductsByCategoryID(categoryID)` yönteminden alması gerekir. Bu ana/ayrıntı raporu salt okunurdur, Ekle, GÜNCELLEŞTIR ve SIL sekmelerinde (yok) seçeneğini belirleyin.

[Getproductsbycategoryıd (CategoryID) yöntemini ![seçin](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)

**Şekil 7**: `GetProductsByCategoryID(categoryID)` yöntemini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))

Ileri 'ye tıkladıktan sonra, ObjectDataSource Sihirbazı bize `GetProductsByCategoryID(categoryID)` yönteminin *`categoryID`* parametresine ilişkin değerin kaynağını ister. Seçili `categories` DropDownList öğesinin değerini kullanmak için parametre kaynağını denetim ve ControlID `Categories`olarak ayarlayın.

[![CategoryID parametresini DropDownList kategorisinin değerine ayarlayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)

**Şekil 8**: *`categoryID`* parametresini `Categories` DropDownList değeri olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra Visual Studio, her bir veri alanının adını ve değerini görüntüleyen DataList için otomatik olarak bir `ItemTemplate` oluşturur. Bunun yerine, DataList 'i yalnızca ürünün adını, kategorisini, tedarikçiyi miktarını, birim başına miktarı ve her öğe arasında bir `<hr>` öğesi taşıyan bir `SeparatorTemplate` içeren bir `ItemTemplate` kullanın. [DataList ve Repeater denetimleri Ile verileri görüntüleme öğreticisiyle](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md) bir örnekteki `ItemTemplate` kullanacağım, ancak en görsel açıdan her türlü şablon işaretlemesini kullanmayı ücretsiz olarak kullanabilirsiniz.

Bu değişiklikleri yaptıktan sonra, DataList 'niz ve onun ObjectDataSource 'un biçimlendirmesi şuna benzer olmalıdır:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

Bir tarayıcıda ilerleme durumunu kontrol etmek için bir dakikanızı ayırın. Sayfa ilk ziyaret edildiğinde, seçili kategoriye (alkoller) ait olan ürünler görüntülenir (Şekil 9 ' da gösterildiği gibi), ancak DropDownList 'in değiştirilmesi verileri güncelleştirmez. Bunun nedeni, DataList 'in güncelleştirilmesi için bir geri gönderme gerçekleşmelidir. Bunu gerçekleştirmek için, DropDownList 'in `AutoPostBack` özelliğini `true` olarak ayarlayabilir veya sayfaya bir düğme web denetimi ekleyebiliriz. Bu öğreticide, DropDownList 'in `AutoPostBack` özelliğini `true`olarak ayarlamayı tercih ediyorum.

Şekil 9 ve 10, işlem içindeki ana/ayrıntı raporunu gösterir.

[Sayfa Ilk ziyaret edildiğinde ![, beden Içecek ürünleri görüntülenir](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)

**Şekil 9**: sayfayı ilk ziyaret edildiğinde, Beiçecek ürünleri görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png))

[Yeni bir ürünün seçilmesi ![(üretim) otomatik olarak bir geri göndermeye neden olur, DataList güncelleştiriliyor](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)

**Şekil 10**: yeni bir ürünün seçilmesi (üretim) otomatik olarak bir geri göndermeye neden olur, DataList 'i güncelleştirerek ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png))

## <a name="adding-a----choose-a-category----list-item"></a>"--Kategori seçme--" liste öğesi ekleme

`FilterByDropDownList.aspx` sayfası ilk kez ziyaret edildiğinde DropDownList 'in ilk liste öğesi (alkolu) varsayılan olarak seçilir ve DataList 'teki Iiçecek ürünlerini gösterir. *Bir DropDownList öğreticisi Ile ana/ayrıntı filtrelemesinde* , varsayılan olarak seçilen DropDownList için bir "--kategori seçin--" seçeneği ekledik ve seçildiği zaman veritabanındaki *Tüm* ürünlerin görüntülenmesiyle birlikte. Bu tür bir yaklaşım, ürünler bir GridView 'da listelenirken, her bir ürün satırında çok az sayıda ekran Emlak yaparken yönetilebilir. Ancak, DataList ile her bir ürünün bilgileri ekranın daha büyük bir öbeğini tüketir. Yine de bir "--kategori seçin--" seçeneği eklemeye ve varsayılan olarak seçili olmasına izin verlim, ancak seçili olduğunda tüm ürünleri göstermesini sağlamak yerine, bir ürün göstermemesi için yapılandıralim.

DropDownList 'e yeni bir liste öğesi eklemek için Özellikler penceresi gidin ve `Items` özelliğindeki üç noktaya tıklayın. `Text` "--kategori seçin--" ve `Value` `0`yeni bir liste öğesi ekleyin.

![Özel](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

**Şekil 11**: "--Kategori seçme--" liste öğesi ekleme

Alternatif olarak, aşağıdaki işaretlemeyi DropDownList öğesine ekleyerek liste öğesini ekleyebilirsiniz:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

Ayrıca, `false` (varsayılan) olarak ayarlanmış olması nedeniyle DropDownList denetiminin `AppendDataBoundItems` `true` olarak ayarlanmaları gerekir, çünkü Kategoriler, tüm el ile eklenen liste öğelerinin üzerine yazar.

![AppendDataBoundItems özelliğini true olarak ayarlayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

**Şekil 12**: `AppendDataBoundItems` özelliğini true olarak ayarlayın

"--Bir kategori seçin--" liste öğesi için `0` değer seçtiğimiz nedeni, sistemde bir `0`değeri olan hiçbir kategori olmadığından, "--Kategori Seç--" liste öğesi seçildiğinde hiçbir ürün kaydı döndürülmeyecektir. Bunu doğrulamak için, bir tarayıcı aracılığıyla sayfayı ziyaret etmek için bir dakikanızı ayırın. Şekil 13 ' ün gösterdiği gibi, "--kategori seçin--" liste öğesi seçilidir ve hiçbir ürün gösterilmez.

[![](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)

**Şekil 13**: "--kategori seçin--" liste öğesi seçildiğinde, hiçbir ürün gösterilmez ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png))

"--Kategori seçin--" seçeneği belirlendiğinde ürünlerin *Tümünü* görüntülemeyi tercih ediyorsanız, bunun yerine `-1` değerini kullanın. Kurnaz okuyucusu, *bir DropDownList öğreticisi ile ana/ayrıntı filtrelemesinde* geri dönecektir `ProductsBLL` sınıfın `GetProductsByCategoryID(categoryID)` yöntemini güncelleştirdik, böylece bir `-1` *`categoryID`* değeri geçirildiğinde tüm ürün kayıtları döndürülür.

## <a name="summary"></a>Özet

Hiyerarşik olarak ilgili verileri görüntülerken, genellikle kullanıcının hiyerarşinin en üstündeki verileri kullanarak başlayabileceği ana/ayrıntı raporlarını kullanarak verileri sunmak ve ayrıntılarda ayrıntıya inmek için yardımcı olur. Bu öğreticide, seçilen kategorinin ürünlerini gösteren basit bir ana/ayrıntı raporu oluşturmayı inceledik. Bu, kategorilerin listesi için bir DropDownList ve seçilen kategoriye ait ürünler için bir DataList kullanılarak gerçekleştirildi.

Sonraki öğreticide, ana ve ayrıntı kayıtlarını iki sayfa boyunca ayırmayı inceleyeceğiz. İlk sayfada, ayrıntıları görüntülemek için bir bağlantı ile "ana" kayıtlarının bir listesi görüntülenir. Bağlantıyı tıklatmak, kullanıcıyı ikinci sayfaya, seçili ana kaydın ayrıntılarını görüntüleyecek şekilde gösterir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler...

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider olarak gözden geçiren, Randy SCHMIDT idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
> [İleri](master-detail-filtering-acess-two-pages-datalist-vb.md)
