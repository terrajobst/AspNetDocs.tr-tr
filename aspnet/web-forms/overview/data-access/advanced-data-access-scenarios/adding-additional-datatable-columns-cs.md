---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-cs
title: Ek DataTable sütunları ekleme (C#) | Microsoft Docs
author: rick-anderson
description: Türü belirtilmiş veri kümesi oluşturmak için TableAdapter Sihirbazı kullanılırken, karşılık gelen DataTable, ana veritabanı sorgusunun döndürdüğü sütunları içerir. Ancak...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 615f3361-f21f-4338-8bc1-fce8ae071de9
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-cs
msc.type: authoredcontent
ms.openlocfilehash: a96f254aa54e7077456ac1a9bd6c5e2a17619d96
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74610635"
---
# <a name="adding-additional-datatable-columns-c"></a>Ek DataTable Sütunları Ekleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_CS.zip) veya [PDF 'yi indirin](adding-additional-datatable-columns-cs/_static/datatutorial70cs1.pdf)

> Türü belirtilmiş veri kümesi oluşturmak için TableAdapter Sihirbazı kullanılırken, karşılık gelen DataTable, ana veritabanı sorgusunun döndürdüğü sütunları içerir. Ancak DataTable 'ın ek sütunları içermesi gerektiğinde durumlar vardır. Bu öğreticide, ek DataTable sütunları gerektiğinde saklı yordamların neden önerildiğini öğreniyoruz.

## <a name="introduction"></a>Giriş

Türü belirtilmiş bir veri kümesine TableAdapter eklenirken, karşılık gelen DataTable s şeması TableAdapter s ana sorgusuyla belirlenir. Örneğin, ana sorgu *a*, *b*ve *c*veri alanlarını döndürürse DataTable, *a*, *b*ve *c*adında üç karşılık gelen sütuna sahip olur. Bir TableAdapter, ana sorgusuna ek olarak, bazı parametreye göre verilerin bir alt kümesini döndüren ek sorgular içerebilir. Örneğin, tüm ürünlerle ilgili bilgileri döndüren `ProductsTableAdapter` s ana sorgusunun yanı sıra, sağlanan bir parametreye göre belirli ürün bilgilerini döndüren `GetProductsByCategoryID(categoryID)` ve `GetProductByProductID(productID)`gibi yöntemleri de içerir.

Tüm TableAdapter s yöntemlerinin, ana sorguda belirtenlerden farklı veya daha az veri alanı döndürmesi halinde DataTable s şemasına sahip olan model, TableAdapter 'ın ana sorgusunu yansıtmaktadır. Bir TableAdapter yönteminin ek veri alanları döndürmesi gerekiyorsa DataTable s şemasını uygun şekilde genişlettik. [Ayrıntılar DataList öğreticisi Ile madde Işaretli ana kayıt listesi kullanan ana/ayrıntı](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) öğesinde, ana `NumberOfProducts`sorguda tanımlanan `CategoryID`, `CategoryName`ve `Description` veri alanlarını ve her bir kategoriyle ilişkili ürün sayısını bildiren ek bir veri alanını döndüren `CategoriesTableAdapter` bir yöntem ekledik. Bu yeni yöntemden `NumberOfProducts` veri alanı değerini yakalamak için `CategoriesDataTable` el ile yeni bir sütun ekledik.

[Dosyaları karşıya yükleme](../working-with-binary-files/uploading-files-cs.md) öğreticisinde açıklandığı gibi, geçici SQL deyimlerini kullanan ve veri alanları ana sorguyla tam olarak eşleşmeyen yöntemlere sahip olan TableAdapters ile mükemmel bir dikkatli olunması gerekir. TableAdapter Yapılandırma Sihirbazı yeniden çalıştırıldığında, tüm TableAdapter s yöntemlerinin, veri alanı listesinin ana sorguyla eşleşmesi için güncelleştirilecek. Sonuç olarak, özelleştirilmiş sütun listelerine sahip tüm yöntemler ana sorgu s sütun listesine döner ve beklenen verileri döndürmez. Saklı yordamlar kullanılırken bu sorun ortaya çıkar.

Bu öğreticide, bir DataTable s şemasının ek sütunları içerecek şekilde nasıl genişletileceğini inceleyeceğiz. Bu öğreticide, ad hoc SQL deyimleri kullanılırken TableAdapter 'ın britliği nedeniyle, saklı yordamları kullanacağız. Bir TableAdapter 'ı saklı yordamları kullanacak şekilde yapılandırma hakkında daha fazla bilgi için, [yazılan veri kümesi s TableAdapters Için yeni saklı yordamlar oluşturma](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) ve [yazılan veri kümesi s TableAdapters öğreticileri Için mevcut saklı yordamları kullanma](https://data-access/tutorials/using-existing-stored-procedures-for-the-typed-dataset-amp-rsquo-s-tableadapters-cs) bölümüne bakın.

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>1\. Adım:`ProductsDataTable``PriceQuartile`sütununu ekleme

*Yazılan veri kümesi s TableAdapters öğreticisi Için yeni saklı yordamlar oluşturma* bölümünde `NorthwindWithSprocs`adlı türü belirtilmiş bir veri kümesi oluşturduk. Bu veri kümesi şu anda iki DataTable içeriyor: `ProductsDataTable` ve `EmployeesDataTable`. `ProductsTableAdapter` aşağıdaki üç yönteme sahiptir:

- `GetProducts`-`Products` tablosundan tüm kayıtları döndüren ana sorgu
- `GetProductsByCategoryID(categoryID)`-belirtilen *CategoryID*'ye sahip tüm ürünleri döndürür.
- `GetProductByProductID(productID)`-belirtilen *ProductID*ile belirli bir ürünü döndürür.

Ana sorgu ve iki ek yöntem, tüm sütunlar `Products` tablosundan aynı veri alanı kümesini döndürür. Bağıntılı alt sorgular yok veya `Categories` veya `Suppliers` tablolarından ilgili verileri çekiyor `JOIN`. Bu nedenle, `ProductsDataTable` `Products` tablosundaki her alan için karşılık gelen bir sütuna sahiptir.

Bu öğreticide, s `ProductsTableAdapter`, tüm ürünleri döndüren `GetProductsWithPriceQuartile` adlı bir yöntem ekleyelim. Standart ürün verileri alanlarına ek olarak, `GetProductsWithPriceQuartile` ürün fiyatı 'nın hangi dörttebirde düştüğünü belirten bir `PriceQuartile` veri alanı da içerecektir. Örneğin, Fiyatları En pahalı %25 ' te olan ürünlerin 1 değeri `PriceQuartile` olacaktır, ancak fiyatları alt %25 ' in altında olan değerler 4 olur. Ancak, bu bilgileri döndürmek için saklı yordam oluşturma konusunda kaygılanmadan önce, `GetProductsWithPriceQuartile` yöntemi kullanıldığında `PriceQuartile` sonuçları tutacak bir sütun eklemek için önce `ProductsDataTable` güncelleştirmeniz gerekir.

`NorthwindWithSprocs` veri kümesini açın ve `ProductsDataTable`sağ tıklayın. Bağlam menüsünden Ekle ' yi ve ardından sütun Seç ' i seçin.

[![ProductsDataTable 'a yeni bir sütun ekleyin](adding-additional-datatable-columns-cs/_static/image2.png)](adding-additional-datatable-columns-cs/_static/image1.png)

**Şekil 1**: `ProductsDataTable` yeni bir sütun ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image3.png))

Bu, `System.String`türünde Sütun1 adlı DataTable öğesine yeni bir sütun ekler. Bu sütun adını, 1 ile 4 arasında bir sayı tutmak için kullanılabilmek için PriceQuartile ve türü `System.Int32` olarak güncelleştirmemiz gerekiyor. `ProductsDataTable` yeni eklenen sütununu seçin ve Özellikler penceresi `Name` özelliğini PriceQuartile ve `DataType` özelliği `System.Int32`olarak ayarlayın.

[Yeni sütun adı ve veri türü özelliklerini ayarlamak ![](adding-additional-datatable-columns-cs/_static/image5.png)](adding-additional-datatable-columns-cs/_static/image4.png)

**Şekil 2**: yeni sütun s `Name` ve `DataType` özelliklerini ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image6.png))

Şekil 2 ' de gösterildiği gibi, sütundaki değerlerin benzersiz olması, sütunun bir otomatik artış sütunu olması, veritabanı `NULL` değerlerine izin verilip verilmeyeceğini ve bu şekilde ayarlanamayacağını belirten ek özellikler vardır. Bu değerleri varsayılan değerlerine ayarlı bırakın.

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>2\. Adım:`GetProductsWithPriceQuartile`yöntemi oluşturma

Artık `ProductsDataTable` `PriceQuartile` sütununu içerecek şekilde güncelleştirildiğinden `GetProductsWithPriceQuartile` metodunu oluşturmaya hazırız. TableAdapter ' a sağ tıklayıp bağlam menüsünden sorgu Ekle ' yi seçerek başlayın. Bu, ilk olarak, geçici SQL deyimlerini veya yeni ya da varolan bir saklı yordamı kullanmak istediğimizi bize isteyen TableAdapter sorgu Yapılandırma Sihirbazı 'nı getirir. Fiyat dörtteverileri döndüren bir saklı yordamımız olmadığı için, TableAdapter 'ın Bu saklı yordamı bizim için oluşturmasına izin verin. Yeni saklı yordam oluştur seçeneğini belirleyin ve Ileri ' ye tıklayın.

[![TableAdapter sihirbazına, bizim Için saklı yordam oluşturma konusunda talimat](adding-additional-datatable-columns-cs/_static/image8.png)](adding-additional-datatable-columns-cs/_static/image7.png)

**Şekil 3**: TableAdapter 'A Için saklı yordam oluşturma Sihirbazı 'nı bildirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image9.png))

Şekil 4 ' te gösterilen sonraki ekranda, sihirbaz bize ne tür bir sorgu ekleneceğini sorar. `GetProductsWithPriceQuartile` Yöntem, `Products` tablosundan tüm sütunları ve kayıtları döndürdüğünden, satırları döndüren Seç seçeneğini belirleyin ve Ileri ' ye tıklayın.

[sorgumuz ![, birden çok satır döndüren bir SELECT deyimidir](adding-additional-datatable-columns-cs/_static/image11.png)](adding-additional-datatable-columns-cs/_static/image10.png)

**Şekil 4**: sorgumuz birden çok satır döndüren bir `SELECT` ifade olacaktır ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image12.png))

Sonraki `SELECT` sorgu sorulur. Sihirbaza aşağıdaki sorguyu girin:

[!code-sql[Main](adding-additional-datatable-columns-cs/samples/sample1.sql)]

Yukarıdaki sorgu SQL Server 2005 s yeni [`NTILE` işlevini](https://msdn.microsoft.com/library/ms175126.aspx) kullanarak, grupların `UnitPrice` değerleri azalan sırada sıralanan dört gruba bölünür.

Ne yazık ki Sorgu Tasarımcısı, `OVER` anahtar sözcüğünü ayrıştırmayı bilmez ve yukarıdaki sorguyu ayrıştırırken bir hata gösterir. Bu nedenle, Sorgu Tasarımcısı kullanmadan yukarıdaki sorguyu doğrudan sihirbazdaki metin kutusuna girin.

> [!NOTE]
> NTILE ve SQL Server 2005 s diğer derecelendirme işlevleri hakkında daha fazla bilgi için, [SQL Server 2005 Books Online](https://msdn.microsoft.com/library/ms189798.aspx)'daki Microsoft SQL Server 2005 ve [Derecelendirme Işlevleri](https://msdn.microsoft.com/library/ms189798.aspx) [ile derecelendirilen sonuçları döndürme](http://www.4guysfromrolla.com/webtech/010406-1.shtml) bölümüne bakın.

`SELECT` sorguyu girdikten ve Ileri 'ye tıkladıktan sonra sihirbaz, oluşturacak saklı yordam için bir ad sağlamamızı ister. Yeni saklı yordamı `Products_SelectWithPriceQuartile` adlandırın ve Ileri ' ye tıklayın.

[Saklı yordamın adını ![Products_SelectWithPriceQuartile](adding-additional-datatable-columns-cs/_static/image14.png)](adding-additional-datatable-columns-cs/_static/image13.png)

**Şekil 5**: saklı yordamın `Products_SelectWithPriceQuartile` adlandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image15.png))

Son olarak, TableAdapter yöntemlerini adlandırma sorulur. Her ikisini de bir DataTable doldur ve bir DataTable onay kutusu işaretli olarak bırakın ve `FillWithPriceQuartile` ve `GetProductsWithPriceQuartile`yöntemleri adlandırın.

[TableAdapter s yöntemlerine ad ![ve son ' a tıklayın](adding-additional-datatable-columns-cs/_static/image17.png)](adding-additional-datatable-columns-cs/_static/image16.png)

**Şekil 6**: TableAdapter s yöntemlerini adlandırın ve son ' a tıklayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image18.png))

`SELECT` sorgusu ve adlı saklı yordam ve TableAdapter yöntemleri ile, Sihirbazı tamamladıktan sonra son ' a tıklayın. Bu noktada, `OVER` SQL yapısı veya bildiriminin desteklenmediğini söyleyen sihirbazdan bir uyarı veya iki nokta alabilirsiniz. Bu uyarılar yoksayılabilir.

Sihirbazı tamamladıktan sonra TableAdapter `FillWithPriceQuartile` ve `GetProductsWithPriceQuartile` yöntemlerini içermeli ve veritabanı `Products_SelectWithPriceQuartile`adlı bir saklı yordam içermelidir. TableAdapter 'ın gerçekten bu yeni yöntemi içerdiğini ve saklı yordamın veritabanına doğru bir şekilde eklendiğini doğrulamak için bir dakikanızı ayırın. Veritabanı denetlenirken, saklı yordamı görmüyorsanız saklı yordamlar klasörüne sağ tıklayıp Yenile ' yi seçin.

![TableAdapter 'a yeni bir yöntem eklendiğini doğrulayın](adding-additional-datatable-columns-cs/_static/image19.png)

**Şekil 7**: TableAdapter 'a yeni bir yöntemin eklendiğini doğrulayın

[![veritabanının Products_SelectWithPriceQuartile saklı yordamını Içerdiğinden emin olun](adding-additional-datatable-columns-cs/_static/image21.png)](adding-additional-datatable-columns-cs/_static/image20.png)

**Şekil 8**: veritabanının `Products_SelectWithPriceQuartile` saklı yordamını içerdiğinden emin olun ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image22.png))

> [!NOTE]
> Ad-hoc SQL deyimleri yerine saklı yordamları kullanmanın avantajlarından biri, TableAdapter Yapılandırma Sihirbazı 'nı yeniden çalıştırmanın saklı yordamlar sütun listelerini değiştirmeyecektir. Bunu, TableAdapter ' a sağ tıklayıp, bağlam menüsünden Yapılandır seçeneğini belirleyerek Sihirbazı başlatın ve ardından işlemi gerçekleştirmek için son ' a tıklayın. Sonra veritabanına gidin ve `Products_SelectWithPriceQuartile` saklı yordamını görüntüleyin. Sütun listesinin değiştirilmediğini unutmayın. Geçici SQL deyimlerini kullandık, TableAdapter Yapılandırma Sihirbazı 'nı yeniden çalıştırmak, bu sorgu sütun listesini ana sorgu sütun listesiyle eşleşecek şekilde geri döndüyordu ve bu nedenle `GetProductsWithPriceQuartile` yöntemi tarafından kullanılan sorgudan NTILE deyimini kaldırır.

Veri erişim katmanı s `GetProductsWithPriceQuartile` yöntemi çağrıldığında, TableAdapter `Products_SelectWithPriceQuartile` saklı yordamını yürütür ve döndürülen her kayıt için `ProductsDataTable` bir satır ekler. Saklı yordam tarafından döndürülen veri alanları `ProductsDataTable` s sütunlarına eşlenir. Saklı yordamda döndürülen bir `PriceQuartile` veri alanı olduğundan, değeri `ProductsDataTable` s `PriceQuartile` sütununa atanır.

Sorguları `PriceQuartile` veri alanı döndürmeyen TableAdapter metotları için, `PriceQuartile` sütun s değeri, `DefaultValue` özelliği tarafından belirtilen değerdir. Şekil 2 ' de gösterildiği gibi, bu değer varsayılan `DBNull`olarak ayarlanır. Farklı bir varsayılan değeri tercih ediyorsanız, `DefaultValue` özelliğini uygun şekilde ayarlamanız yeterlidir. `DefaultValue` değerin `DataType` geçerli olduğundan emin olun (örneğin, `PriceQuartile` sütunu için `System.Int32`).

Bu noktada, bir DataTable 'a ek sütun eklemek için gerekli adımları gerçekleştirdik. Bu ek sütunun beklendiği gibi çalıştığını doğrulamak için, her bir ürün adı, Fiyat ve fiyat dörttebirliğini görüntüleyen bir ASP.NET sayfası oluşturalım. Bunu yapmadan önce, önce Iş mantığı katmanını, DAL s `GetProductsWithPriceQuartile` metoduna çağıran bir yöntemi içerecek şekilde güncelleştirmeniz gerekir. Adım 3 ' te BLL 'yi güncelleştireceğiz ve 4. adımda ASP.NET sayfasını oluşturacağız.

## <a name="step-3-augmenting-the-business-logic-layer"></a>3\. Adım: Iş mantığı katmanını genişletme

Sunum katmanından yeni `GetProductsWithPriceQuartile` yöntemini kullanmadan önce, önce BLL 'ye karşılık gelen bir yöntemi eklememiz gerekir. `ProductsBLLWithSprocs` sınıfı dosyasını açın ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](adding-additional-datatable-columns-cs/samples/sample2.cs)]

`ProductsBLLWithSprocs`diğer veri alma yöntemlerine benzer şekilde, `GetProductsWithPriceQuartile` yöntemi yalnızca DAL s 'nin karşılık gelen `GetProductsWithPriceQuartile` yöntemini çağırır ve sonuçlarını döndürür.

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>4\. Adım: fiyat DÖRTTEBİRLİK bilgilerini bir ASP.NET Web sayfasında görüntüleme

BLL ekleme tamamlandıktan sonra, her ürün için fiyat dörttebirliğini gösteren bir ASP.NET sayfası oluşturmaya yeniden hazırlıyoruz. `AdvancedDAL` klasöründeki `AddingColumns.aspx` sayfasını açın ve araç kutusu 'ndaki bir GridView 'u `ID` özelliğini `Products`olarak ayarlayarak tasarımcı üzerine sürükleyin. GridView s akıllı etiketinden `ProductsDataSource`adlı yeni bir ObjectDataSource 'a bağlayın. `ProductsBLLWithSprocs` sınıf s `GetProductsWithPriceQuartile` metodunu kullanmak için ObjectDataSource 'ı yapılandırın. Bu, salt okunurdur bir ızgara olacağı için GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden (hiçbiri) açılan listeleri ayarlayın.

[![, bu ObjectDataSource 'ı ProductsBLLWithSprocs sınıfını kullanacak şekilde yapılandırma](adding-additional-datatable-columns-cs/_static/image24.png)](adding-additional-datatable-columns-cs/_static/image23.png)

**Şekil 9**: `ProductsBLLWithSprocs` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image25.png))

[GetProductsWithPriceQuartile yönteminden ürün bilgilerini almak ![](adding-additional-datatable-columns-cs/_static/image27.png)](adding-additional-datatable-columns-cs/_static/image26.png)

**Şekil 10**: `GetProductsWithPriceQuartile` yönteminden ürün bilgilerini alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image28.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio yöntem tarafından döndürülen her bir veri alanı için GridView 'a bir BoundField veya CheckBoxField ekler. Bu veri alanlarından biri, 1. adımdaki `ProductsDataTable` eklediğimiz sütundur `PriceQuartile`.

`ProductName`, `UnitPrice`ve `PriceQuartile` BoundFields alanlarını kaldırarak GridView s alanlarını düzenleyin. `UnitPrice` BoundField değerini bir para birimi olarak biçimlendirmek ve `UnitPrice` ve `PriceQuartile` BoundFields değerlerini sırasıyla sağa ve merkeze hizalı şekilde yapılandırın. Son olarak, kalan BoundFields özelliklerini sırasıyla ürün, Fiyat ve fiyat dörttebirliği olarak `HeaderText` güncelleştirin. Ayrıca, GridView s akıllı etiketinden sıralamayı etkinleştir onay kutusunu işaretleyin.

Bu değişikliklerden sonra, GridView ve ObjectDataSource 'lar bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](adding-additional-datatable-columns-cs/samples/sample3.aspx)]

Şekil 11 bir tarayıcı aracılığıyla ziyaret edildiğinde bu sayfayı gösterir. Başlangıçta ürünlerin, her ürün uygun bir `PriceQuartile` değer atadığına göre azalan sırada fiyatlara göre sıralandığına unutmayın. Tabii ki bu veriler, Fiyat dörttebir sütun değeri, yine de ücretle ilgili olarak ürün sırasını yansıtarak diğer ölçütlere göre sıralanabilir (bkz. Şekil 12).

[Ürünlerin fiyatlarına göre sıralandığı ![](adding-additional-datatable-columns-cs/_static/image30.png)](adding-additional-datatable-columns-cs/_static/image29.png)

**Şekil 11**: Ürünler fiyatlarına göre sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image31.png))

[Ürünlerin adlarına göre sıralanmış ![](adding-additional-datatable-columns-cs/_static/image33.png)](adding-additional-datatable-columns-cs/_static/image32.png)

**Şekil 12**: Ürünler adlarına göre sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-additional-datatable-columns-cs/_static/image34.png))

> [!NOTE]
> Birkaç satır kod ile GridView 'u, `PriceQuartile` değerlerine göre ürün satırlarını görüntüleyecek şekilde artırabilir. İlk dörttebir açık yeşil, ikinci dörttebir açık sarı ve benzeri olan bu ürünleri renkleriz. Bu işlevi eklemek için bir dakikanızı ayırın. GridView biçimlendirme üzerinde bir yenileyici gerekiyorsa, veri öğreticisine [göre özel biçimlendirmeye](../custom-formatting/custom-formatting-based-upon-data-cs.md) başvurun.

## <a name="an-alternative-approach---creating-another-tableadapter"></a>Alternatif bir yaklaşım-başka bir TableAdapter oluşturma

Bu öğreticide gördüğümüz gibi, ana sorgu tarafından yazılanlar dışındaki veri alanlarını döndüren bir TableAdapter 'a bir yöntem eklerken DataTable 'a ilgili sütunları ekleyebiliriz. Bununla birlikte, bu tür bir yaklaşım, yalnızca TableAdapter 'ta farklı veri alanları döndüren ve bu alternatif veri alanları ana sorgudan çok fazla farklılık yapamadığına yönelik az sayıda yöntem varsa iyi bir şekilde çalışacaktır.

DataTable 'a sütun eklemek yerine, farklı veri alanları döndüren ilk TableAdapter içindeki yöntemleri içeren veri kümesine başka bir TableAdapter ekleyebilirsiniz. Bu öğreticide, `PriceQuartile` sütununu `ProductsDataTable` eklemek yerine (yalnızca `GetProductsWithPriceQuartile` yöntemi tarafından kullanıldığı), `ProductsWithPriceQuartileTableAdapter` adlı veri kümesine ana sorgu olarak `Products_SelectWithPriceQuartile` saklı yordamını kullanan başka bir TableAdapter ekledik. ASP.NET, Fiyat DÖRTTEBİRLİK ile ürün bilgilerini almak için gereken sayfalar `ProductsWithPriceQuartileTableAdapter`kullanır, ancak `ProductsTableAdapter`kullanmaya devam edemeyebilir.

Yeni bir TableAdapter ekleyerek, DataTable 'lar bir daha açık kalır ve sütunları, TableAdapter s yöntemlerinin döndürdüğü veri alanlarını tam olarak yansıtır. Ancak, ek TableAdapters yinelenen görevleri ve işlevleri ortaya çıkarabilir. Örneğin, `PriceQuartile` sütununu görüntülenen ASP.NET sayfaları ekleme, güncelleştirme ve silme desteğini sağlamak için de gerekliyse, `ProductsWithPriceQuartileTableAdapter` `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özellikleri düzgün şekilde yapılandırılmış olmalıdır. Bu özellikler `ProductsTableAdapter` s 'yi yansıtarak, bu yapılandırma ek bir adım sunar. Üstelik, `ProductsTableAdapter` ve `ProductsWithPriceQuartileTableAdapter` sınıfları aracılığıyla bir ürünü güncelleştirmek, silmek veya veritabanına eklemek için kullanabileceğiniz iki yol vardır.

Bu öğreticinin indirilmesi, `NorthwindWithSprocs` veri kümesinde bu alternatif yaklaşımda bir `ProductsWithPriceQuartileTableAdapter` sınıfı içerir.

## <a name="summary"></a>Özet

Çoğu senaryoda, bir TableAdapter içindeki yöntemlerin hepsi aynı veri alanı kümesini döndürür, ancak belirli bir yöntemin veya ikisinin de ek bir alan döndürmesi gerekebilir. Örneğin, [Ayrıntılar DataList öğreticisi Ile madde Işaretli ana kayıt listesi kullanan ana/ayrıntı](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) öğesinde, ana sorgu s veri alanlarına ek olarak, her bir kategoriyle ilişkili ürün sayısını bildiren bir `NumberOfProducts` alanı döndürtiğimiz `CategoriesTableAdapter` bir yöntem ekledik. Bu öğreticide, ana sorgu s veri alanlarının yanı sıra `PriceQuartile` bir alan döndüren `ProductsTableAdapter` bir yöntem eklemeye baktık. TableAdapter s yöntemleri tarafından döndürülen ek veri alanlarını yakalamak için DataTable 'a ilgili sütunları eklememiz gerekir.

DataTable 'a sütunları el ile eklemeyi planlıyorsanız, TableAdapter 'ın saklı yordamları kullanması önerilir. TableAdapter geçici SQL deyimlerini kullanıyorsa, TableAdapter Yapılandırma Sihirbazı tüm yöntemler veri alanı listelerini her çalıştırışında, ana sorgu tarafından döndürülen veri alanlarına geri döner. Bu sorun, saklı yordamlara genişlemez ve bu nedenle bu öğreticide kullanılması önerilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider olarak gözden geçirenler, Randy SCHMIDT, Jacky Goor, Bernadette Leigh ve Tepton Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](updating-the-tableadapter-to-use-joins-cs.md)
> [İleri](working-with-computed-columns-cs.md)
