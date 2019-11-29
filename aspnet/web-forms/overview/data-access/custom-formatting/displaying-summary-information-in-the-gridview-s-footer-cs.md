---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
title: GridView 'un altbilgisinde Özet bilgilerini görüntüleme (C#) | Microsoft Docs
author: rick-anderson
description: Özet bilgileri genellikle raporun alt kısmında bir Özet satırında görüntülenir. GridView denetimi, hücreleri için bir alt bilgi satırı içerebilir...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d50edc31-9286-4c6a-8635-be09e72752a4
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: b258a2bdeaea8da4e9c5c5d8043b167d94e1e817
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617002"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-c"></a>GridView'ın Alt Bilgisinde Özet Bilgiler Görüntüleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe) veya [PDF 'yi indirin](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)

> Özet bilgileri genellikle raporun alt kısmında bir Özet satırında görüntülenir. GridView denetimi, hücrelere program aracılığıyla toplu veri ekleyebilmemiz için bir altbilgi satırı içerebilir. Bu öğreticide, bu alt bilgi satırında toplam verileri görüntüleme hakkında bilgi edineceksiniz.

## <a name="introduction"></a>Giriş

Bir Kullanıcı, her bir ürünün fiyatlarını, Stokdaki birimleri, siparişteki birimleri ve yeniden sipariş düzeylerini görmenin yanı sıra, ortalama fiyat, Stoktaki toplam birim sayısı gibi toplu bilgilerle da ilgileniyor olabilir. Bu tür özet bilgiler genellikle raporun alt kısmında bir Özet satırında görüntülenir. GridView denetimi, hücrelere program aracılığıyla toplu veri ekleyebilmemiz için bir altbilgi satırı içerebilir.

Bu görev bize üç zorluk gösterir:

1. GridView 'un altbilgi satırını görüntülemesi için yapılandırma
2. Özet verileri belirleme; diğer bir deyişle, stokta ortalama fiyatı veya toplam birim sayısını nasıl hesapladık?
3. Özet verileri alt bilgi satırındaki uygun hücrelere ekleme

Bu öğreticide, bu zorlukları nasıl aşabileceksiniz. Özellikle, seçilen kategorinin ürünlerini GridView 'da görüntülenen bir açılan listedeki kategorileri listeleyen bir sayfa oluşturacağız. GridView, bu kategorideki ürünlerin stok ve toplam birim sayısını gösteren bir altbilgi satırı içerir.

[![Özet bilgileri GridView 'un altbilgi satırında görüntülenir](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)

**Şekil 1**: Özet bilgiler GridView 'un altbilgi satırında görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png))

Bu öğreticide, ürün ana/ayrıntı arabirimine yönelik kategorisi bulunan bu öğretici, [bir DropDownList öğreticisi ile önceki ana/ayrıntı filtrelemesinde](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) ele alınan kavramların üzerine oluşturulur. Henüz önceki öğreticide çalışmadıysanız, bununla devam etmeden önce lütfen bunu yapın.

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>1\. Adım: DropDownList ve Products GridView kategorilerini ekleme

GridView 'un altbilgisine Özet bilgiler eklemekle kendimize ile ilgili olarak önce, ilk olarak ana/ayrıntı raporunu oluşturalım. Bu ilk adımı tamamladıktan sonra Özet verileri ekleme bölümüne bakacağız.

`CustomFormatting` klasöründeki `SummaryDataInFooter.aspx` sayfasını açarak başlayın. Bir DropDownList denetimi ekleyin ve `ID` `Categories`olarak ayarlayın. Ardından, DropDownList 'in akıllı etiketindeki veri kaynağı Seç bağlantısına tıklayın ve `CategoriesBLL` sınıfının `GetCategories()` yöntemini çağıran `CategoriesDataSource` adlı yeni bir ObjectDataSource eklemeyi tercih edin.

[![CategoriesDataSource adlı yeni bir ObjectDataSource ekleyin](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)

**Şekil 2**: `CategoriesDataSource` adlı yeni bir ObjectDataSource ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png))

[![ObjectDataSource, CategoriesBLL sınıfının GetCategories () yöntemini çağırır](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)

**Şekil 3**: ObjectDataSource 'un `CategoriesBLL` sınıfın `GetCategories()` metodunu çağırmasını[sağlar (tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png))

ObjectDataSource yapılandırıldıktan sonra sihirbaz, hangi veri alanı değerinin gösterilmesi gerektiğini ve DropDownList 'ın `ListItem` s değerine karşılık gelmesi gerektiğini belirtmemiz gereken DropDownList 'in veri kaynağı Yapılandırma Sihirbazı 'na geri döndürür. `CategoryName` alanın görüntülenmesini ve `CategoryID` değer olarak kullanılmasını kullanın.

[![, sırasıyla, ListItems ve CategoryID alanlarını, ListItems için metin ve değer olarak kullanın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)

**Şekil 4**: `CategoryName` ve `CategoryID` alanlarını sırasıyla `Text` ve `ListItem` `Value` olarak kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png))

Bu noktada, sistemdeki kategorileri listeleyen bir DropDownList (`Categories`) vardır. Şimdi seçili kategoriye ait olan ürünleri listeleyen bir GridView eklememiz gerekiyor. Ancak bunu yapmadan önce, DropDownList 'in akıllı etiketindeki AutoPostBack seçeneğini etkinleştir onay kutusunu işaretleyin. *Bir DropDownList öğreticisi Ile ana/ayrıntı filtrelemesinde* açıklandığı gibi, dropdownlist 'in `AutoPostBack` özelliğini `true` olarak ayarlayarak, DropDownList değeri her değiştirildiğinde sayfa geri gönderilir. Bu, yeni seçilen kategori için bu ürünleri gösteren GridView 'un yenilenmesini sağlar. `AutoPostBack` özelliği `false` (varsayılan) olarak ayarlandıysa, kategorinin değiştirilmesi geri göndermeye neden olmaz ve bu nedenle listelenen ürünleri güncelleştirmez.

[![DropDownList 'in akıllı etiketindeki AutoPostBack 'ı etkinleştir onay kutusunu Işaretleyin](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)

**Şekil 5**: DropDownList 'In akıllı etiketindeki AutoPostBack 'ı etkinleştir onay kutusunu işaretleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png))

Seçili Kategori için ürünleri göstermek üzere sayfaya bir GridView denetimi ekleyin. GridView 'un `ID` `ProductsInCategory` olarak ayarlayın ve `ProductsInCategoryDataSource`adlı yeni bir ObjectDataSource 'a bağlayın.

[ProductsInCategoryDataSource adlı yeni bir ObjectDataSource eklemek ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)

**Şekil 6**: `ProductsInCategoryDataSource` adlı yeni bir ObjectDataSource ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png))

`ProductsBLL` sınıfının `GetProductsByCategoryID(categoryID)` yöntemini çağırabilmesi için ObjectDataSource 'ı yapılandırın.

[![ObjectDataSource, Getproductsbycategoryıd (CategoryID) yöntemini çağırsın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)

**Şekil 7**: ObjectDataSource 'un `GetProductsByCategoryID(categoryID)` yöntemini çağırmasına[izin vermek (tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png))

`GetProductsByCategoryID(categoryID)` yöntemi bir giriş parametresi kullandığından, sihirbazın son adımında parametre değerinin kaynağını belirteceğiz. Seçili kategoriden bu ürünleri göstermek için, parametrenin `Categories` DropDownList 'den çektiği bir parametreye sahip olması gerekir.

[Seçili kategoriler DropDownList öğesinden CategoryID parametre değerini Al ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)

**Şekil 8**: Seçili kategoriler DropDownList öğesinden *`categoryID`* parametre değerini Al ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png))

Sihirbazı tamamladıktan sonra GridView, her bir ürün özelliği için bir BoundField öğesine sahip olur. Bu BoundFields alanlarını yalnızca `ProductName`, `UnitPrice`, `UnitsInStock`ve `UnitsOnOrder` BoundFields görüntülenmesini sağlayacak şekilde temizleyelim. Kalan BoundFields (`UnitPrice` para birimi olarak biçimlendirme gibi) alan düzeyindeki ayarları ekleyebilirsiniz. Bu değişiklikleri yaptıktan sonra, GridView 'un bildirim temelli işaretleme aşağıdakine benzer şekilde görünmelidir:

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample1.aspx)]

Bu noktada, seçilen kategoriye ait olan ürünler için adı, birim fiyatını, stok sayısını ve birimleri izleyen, tam olarak çalışan bir ana/ayrıntı raporunuz vardır.

[Seçili kategoriler DropDownList öğesinden CategoryID parametre değerini Al ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)

**Şekil 9**: Seçili kategoriler DropDownList öğesinden *`categoryID`* parametre değerini Al ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png))

## <a name="step-2-displaying-a-footer-in-the-gridview"></a>2\. Adım: GridView 'da bir altbilgi görüntüleme

GridView denetimi hem bir üst bilgi hem de altbilgi satırını gösterebilir. Bu satırlar, `ShowHeader` değerlerine ve `ShowFooter` özelliklerine göre, sırasıyla `true` ve `ShowFooter` `false``ShowHeader` olacak şekilde görüntülenir. GridView 'a bir altbilgi eklemek için `ShowFooter` özelliğini `true`olarak ayarlayın.

[GridView 'ın ShowFooter özelliğini true olarak ayarlamak ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)

**Şekil 10**: GridView 'un `ShowFooter` özelliğini `true` olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png))

Alt bilgi satırı, GridView 'da tanımlanan her alan için bir hücreye sahiptir; Ancak, bu hücreler varsayılan olarak boştur. Sürmekte olan ilerlemeyi bir tarayıcıda görüntülemek için bir dakikanızı ayırın. `ShowFooter` özelliği artık `true`olarak ayarlandığından, GridView boş bir altbilgi satırı içerir.

[GridView ![şimdi bir altbilgi satırı Içeriyor](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)

**Şekil 11**: GridView şimdi bir altbilgi satırı içeriyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png))

Şekil 11 ' deki altbilgi satırı, beyaz bir arka plana sahip olduğu için kullanıma hazır değildir. `Styles.css`, koyu kırmızı bir arka plan belirten `FooterStyle` CSS sınıfı oluşturalım ve sonra bu CSS sınıfını GridView 'in `FooterStyle``CssClass` özelliğine atamak için `DataWebControls` temasının `GridView.skin` dış görünüm dosyasını yapılandıralim. Kaplamalar ve temalar üzerinde fırçaya ihtiyacınız varsa, [ObjectDataSource Ile verileri görüntüleme öğreticisiyle](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) geri bakın.

`Styles.css`için aşağıdaki CSS sınıfını ekleyerek başlayın:

[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample2.css)]

`FooterStyle` CSS sınıfı, `HeaderStyle` sınıfına stil olarak benzerdir, ancak `HeaderStyle`arka plan rengi, daha koyu ve metin kalın yazı tipinde görüntülenir. Ayrıca, altbilginin metni ortalarken, altbilgide metin sağa hizalanır.

Ardından, bu CSS sınıfını her GridView 'un altbilgisi ile ilişkilendirmek için `DataWebControls` temasından `GridView.skin` dosyasını açın ve `FooterStyle``CssClass` özelliğini ayarlayın. Bu eklendikten sonra dosyanın biçimlendirmesi şöyle görünmelidir:

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample3.aspx)]

Aşağıdaki ekran görüntüsünde gösterildiği gibi bu değişiklik, altbilginin daha net bir şekilde kullanıma hazır olmasını sağlar.

[GridView 'un altbilgi satırı ![artık bir Redrtın arka plan rengine sahiptir](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)

**Şekil 12**: GridView 'un altbilgi satırı artık bir Redrtın arka plan rengine sahiptir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png))

## <a name="step-3-computing-the-summary-data"></a>3\. Adım: Özet verileri hesaplama

GridView 'un altbilgisi görüntülenirken, bize bakan bir sonraki zorluk özet verileri hesaplama. Bu toplu bilgileri hesaplamak için iki yol vardır:

1. Bir SQL sorgusu aracılığıyla belirli bir kategori için özet verileri hesaplamak üzere veritabanına ek bir sorgu yayınlıyoruz. SQL, verilerin özetlenmesi gereken verileri belirtmek için bir `GROUP BY` yan tümcesiyle birlikte bir dizi toplama işlevi içerir. Aşağıdaki SQL sorgusu gerekli bilgileri geri getirecek:  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample4.sql)]

    Kuşkusuz, bu sorguyu doğrudan `SummaryDataInFooter.aspx` sayfasından vermek istemezsiniz, ancak `ProductsTableAdapter` ve `ProductsBLL`bir yöntem oluşturarak bunun yerine.
2. Bu bilgileri, veri öğreticisine [dayalı özel biçimlendirme](custom-formatting-based-upon-data-cs.md) bölümünde açıklandığı gibi GridView 'a eklendikçe, gridview 'un `RowDataBound` olay Işleyicisi, veri sınırına ulaşıldıktan sonra GridView 'a eklenen her satır için bir kez ateşlenir. Bu olay için bir olay işleyicisi oluşturarak, toplamak istediğimiz değerlerin bir çalışan toplamını saklayabiliriz. Son veri satırı GridView 'a bağlandıktan sonra, ortalamayı hesaplamak için gereken toplamlar ve bilgiler vardır.

Genellikle, veritabanına bir yolculuğa ve veri erişim katmanında ve Iş mantığı katmanında Özet işlevselliği uygulamak için gereken çabaya bir yaklaşım kaydederek ikinci yaklaşımı kullandım, ancak her iki yaklaşım da yeterli olacaktır. Bu öğretici için ikinci seçeneği kullanalım ve `RowDataBound` olay işleyicisini kullanarak çalışan toplamı takip edelim.

Tasarımcıda GridView 'u seçerek, Özellikler penceresi için bir `RowDataBound` olay işleyicisi oluşturun ve `RowDataBound` olayına çift tıklayın. Bu işlem, `SummaryDataInFooter.aspx` sayfasının arka plan kod sınıfında `ProductsInCategory_RowDataBound` adlı yeni bir olay işleyicisi oluşturur.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample5.cs)]

Çalışan bir toplam sağlamak için, olay işleyicisinin kapsamı dışında değişkenleri tanımlamanız gerekir. Aşağıdaki dört sayfa düzeyi değişkeni oluşturun:

- `_totalUnitPrice``decimal` tür
- `_totalNonNullUnitPriceCount``int` tür
- `_totalUnitsInStock``int` tür
- `_totalUnitsOnOrder``int` tür

Daha sonra, `RowDataBound` olay işleyicisinde karşılaşılan her bir veri satırı için bu üç değişkeni artırmak üzere kodu yazın.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample6.cs)]

`RowDataBound` olay işleyicisi, bir DataRow ile ilgilendiğimiz doğrulayarak başlar. Bu, oluşturulduktan sonra, `e.Row` `GridViewRow` nesnesine daha önce bağlanan `Northwind.ProductsRow` örneği `product`değişkenine depolanır. Daha sonra, toplam değişken sayısı geçerli ürüne karşılık gelen değerler (bir veritabanı `NULL` değeri içermeyeceği varsayılarak) tarafından artırılır. Ortalama fiyat bu iki sayının bölümü olduğundan, hem çalışan `UnitPrice` toplam ve`NULL` olmayan `UnitPrice` kaydı sayısını izliyoruz.

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>4\. Adım: Özet verileri altbilgisinde görüntüleme

Özet veriler toplamı ile, son adım bunu GridView 'un altbilgi satırında görüntülemektir. Bu görev, `RowDataBound` olay işleyicisi aracılığıyla programlı bir şekilde gerçekleştirilebilir. `RowDataBound` olay işleyicisinin altbilgi satırı da dahil olmak üzere GridView 'a bağlanan *her* satır için harekete geçdiğine geri çekin. Bu nedenle, aşağıdaki kodu kullanarak alt bilgi satırındaki verileri göstermek için olay işleyicimizi daha iyi bir şekilde artırabilir:

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample7.cs)]

Tüm veri satırları eklendikten sonra alt bilgi satırı GridView 'a eklendiğinden, özet verileri alt bilgide görüntülemeye hazırımız sürenin, çalışan toplam hesaplamaların tamamlanacaktır. Son adım, bu değerleri altbilginin hücrelerinde ayarlamaya yönelik olur.

Belirli bir altbilgi hücresinde metin göstermek için, `Cells` dizin oluşturma işleminin 0 ' dan başladığı `e.Row.Cells[index].Text = value`kullanın. Aşağıdaki kod, ortalama fiyatı (ürün sayısına bölünen toplam fiyat) hesaplar ve GridView 'un uygun alt bilgi hücrelerine göre stok ve birim cinsinden toplam birim sayısı ile birlikte görüntüler.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample8.cs)]

Şekil 13, bu kod eklendikten sonra raporu gösterir. `ToString("c")`, ortalama fiyat özeti bilgilerinin para birimi gibi nasıl biçimlendirileceğini aklınızda bir şekilde nasıl yol açar.

[GridView 'un altbilgi satırı ![artık bir Redrtın arka plan rengine sahiptir](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)

**Şekil 13**: GridView 'un altbilgi satırı artık bir Redrtın arka plan rengine sahiptir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png))

## <a name="summary"></a>Özet

Özet verileri görüntülemek ortak bir rapor gereksinimidir ve GridView denetimi, bu bilgileri Altbilgi satırına eklemeyi kolaylaştırır. GridView 'un `ShowFooter` özelliği `true` olarak ayarlandığında altbilgi satırı görüntülenir ve içindeki metin `RowDataBound` olay işleyicisi aracılığıyla programlı bir şekilde ayarlanır. Özet verilerin hesaplanması, özet verileri programlı bir şekilde hesaplamak için veritabanını yeniden sorgulamak ya da ASP.NET sayfasının arka plan kod sınıfındaki kodu kullanarak yapılabilir.

Bu öğretici, GridView, DetailsView ve FormView denetimleriyle özel biçimlendirme incelemesini yerine getiriyor. Sonraki öğreticimiz, aynı denetimleri kullanarak veri ekleme, güncelleştirme ve silmeye yönelik araştırmayla oynanır.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](using-the-formview-s-templates-cs.md)
> [İleri](custom-formatting-based-upon-data-vb.md)
