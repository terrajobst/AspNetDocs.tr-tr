---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
title: Türü belirtilmiş DataSet 'in TableAdapters (C#) Için yeni saklı yordamlar oluşturuluyor | Microsoft Docs
author: rick-anderson
description: Önceki öğreticilerde, kodlarımızda SQL deyimleri oluşturdunuz ve bu bildirimleri yürütülecek veritabanına geçirdik. Alternatif bir yaklaşım, s... kullanmaktır.
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 751282ca-5870-4d66-84e4-6cefae23eb4a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
msc.type: authoredcontent
ms.openlocfilehash: db0d83a0fd1f1f175001d20844b298be0cf7e1cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78533714"
---
# <a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-c"></a>Türü Belirtilmiş DataSet'in TableAdapter’ları için Yeni Saklı Yordam Oluşturma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_CS.zip) veya [PDF 'yi indirin](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/datatutorial67cs1.pdf)

> Önceki öğreticilerde, kodlarımızda SQL deyimleri oluşturdunuz ve bu bildirimleri yürütülecek veritabanına geçirdik. Alternatif bir yaklaşım, SQL deyimlerinin veritabanında önceden tanımlandığı saklı yordamları kullanmaktır. Bu öğreticide, TableAdapter sihirbazının bizimle ilgili yeni saklı yordamlar üretme hakkında bilgi edineceksiniz.

## <a name="introduction"></a>Giriş

Bu öğreticiler için veri erişim katmanı (DAL) yazılan veri kümelerini kullanır. [Veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-cs.md) öğreticisinde açıklandığı gibi, yazılı veri kümeleri kesin türü belirtilmiş DataTable ve TableAdapters oluşur. DataTable, veri erişimi işini gerçekleştirmek için temel alınan veritabanıyla TableAdapters arabirimi iken, sistemdeki mantıksal varlıkları temsil eder. Bu, DataTable 'ı verilerle doldurmayı, skaler veriler döndüren sorguları yürütmeyi ve veritabanından kayıtları eklemeyi, güncelleştirmeyi ve silmeyi içerir.

TableAdapters tarafından yürütülen SQL komutları, `SELECT columnList FROM TableName`veya saklı yordamlar gibi geçici SQL deyimlerine sahip olabilir. Mimarimizde TableAdapters, geçici SQL deyimlerini kullanır. Ancak birçok geliştirici ve veritabanı yöneticisi, güvenlik, bakım ve güncelleştirmeme nedenleriyle, geçici SQL deyimlerine yönelik saklı yordamları tercih eder. Diğerleri esneklik için geçici SQL deyimlerini tercih edebilir. Kendi çalışmamda, saklı yordamları geçici SQL deyimleri üzerinden tercih ediyorum, ancak önceki öğreticileri basitleştirmek için geçici SQL deyimlerini kullanmayı seçti.

TableAdapter tanımlarken veya yeni yöntemler eklerken, TableAdapter s Sihirbazı yeni saklı yordamlar oluşturmayı veya diğer saklı yordamları, geçici SQL deyimlerini kullanacak şekilde kullanmayı kolaylaştırır. Bu öğreticide, TableAdapter s sihirbazının saklı yordamları otomatik olarak oluşturmasını inceleyeceğiz. Sonraki öğreticide, TableAdapter s yöntemlerinin mevcut veya el ile oluşturulmuş saklı yordamları kullanmak üzere nasıl yapılandırılacağı ele alınacaktır.

> [!NOTE]
> Bkz. ramiz Howard 'ın blog girişi, [saklı yordamları henüz kullanmıyor?](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/) ve [Frans Bouma](https://weblogs.asp.net/fbouma/) s blog girdisi saklı yordamları, SAKLı yordamların ve geçici SQL 'in avantajlarını ve dezavantajları Için [kötü, M kay?](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx)

## <a name="stored-procedure-basics"></a>Saklı yordam temelleri

İşlevler tüm programlama dillerinin ortak bir yapısıdır. İşlev, işlev çağrıldığında yürütülen deyimler koleksiyonudur. İşlevler, giriş parametrelerini kabul edebilir ve isteğe bağlı olarak bir değer döndürebilir. *[Saklı yordamlar](http://en.wikipedia.org/wiki/Stored_procedure)* , programlama dillerinde işlevlerle birçok benzerlikler paylaşan veritabanı yapılarıdır. Saklı yordam, saklı yordam çağrıldığında yürütülen bir T-SQL deyimleri kümesinden oluşur. Saklı yordam, sıfır-çok giriş parametresini kabul edebilir ve `SELECT` sorgulardan yalnızca skaler değerler, çıkış parametreleri veya en yaygın sonuç kümesi döndürebilir.

> [!NOTE]
> Saklı yordamlar, sprocs veya SPs olarak adlandırılan zamanlardır.

Saklı yordamlar [`CREATE PROCEDURE`](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) t-SQL deyimleri kullanılarak oluşturulur. Örneğin, aşağıdaki T-SQL betiği, `@CategoryID` adında tek bir parametre alan `GetProductsByCategoryID` adlı bir saklı yordam oluşturur ve eşleşen bir `UnitPrice`değeri olan `Discontinued` tablosundaki bu sütunların `ProductID`, `ProductName`, `Products` ve `CategoryID` alanlarını döndürür:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample1.sql)]

Bu saklı yordam oluşturulduktan sonra, aşağıdaki sözdizimi kullanılarak çağrılabilir:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample2.sql)]

> [!NOTE]
> Sonraki öğreticide, Visual Studio IDE aracılığıyla saklı yordamlar oluşturmayı inceleyeceğiz. Bununla birlikte, bu öğreticide, TableAdapter sihirbazının sizin için saklı yordamları otomatik olarak oluşturmasına izin vereceğiz.

Yalnızca verilerin döndürülmesinin yanı sıra, saklı yordamlar genellikle tek bir işlemin kapsamı içinde birden çok veritabanı komutu gerçekleştirmek için kullanılır. Örneğin, `DeleteCategory`adlı saklı yordam, `@CategoryID` bir parametre alabilir ve iki `DELETE` deyimi gerçekleştirebilir: Birincisi, biri ilgili ürünleri silmek ve ikinci bir, belirtilen kategoriyi silmek için. Saklı yordam içindeki birden çok deyim bir işlem içinde otomatik olarak *sarmalanmaz* . Saklı yordamın birden çok komutun atomik bir işlem olarak değerlendirildiğinden emin olmak için ek T-SQL komutlarının verilmesi gerekir. Saklı yordam s komutlarının sonraki öğreticide bir işlemin kapsamı içinde nasıl sarılacağını inceleyeceğiz.

Bir mimaride saklı yordamları kullanırken, veri erişim katmanı s yöntemleri, geçici bir SQL ifadesini vermek yerine belirli bir saklı yordamı çağırır. Bu, uygulama mimarisi içinde tanımlanması yerine yürütülen (veritabanında) SQL deyimlerinin konumunu merkezileştirir. Bu merkezileşmeyi argugu sorguları bulmayı, çözümlemeyi ve ayarlamayı kolaylaştırır ve veritabanının nerede ve nasıl kullanıldığına ilişkin daha net bir resim sunar.

Saklı yordam temelleri hakkında daha fazla bilgi için, Bu öğreticinin sonundaki daha fazla okuma bölümünde yer alan kaynaklara bakın.

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>1\. Adım: Gelişmiş veri erişim katmanı senaryoları Web sayfaları oluşturma

Saklı yordamları kullanarak bir DAL oluşturmaya yönelik tartışmayla karşılaşmadan önce, Web sitesi projemizdeki bu ve sonraki birkaç öğreticiden ASP.NET sayfaları oluşturmak için önce bir süre sürme. `AdvancedDAL`adlı yeni bir klasör ekleyerek başlayın. Ardından, aşağıdaki ASP.NET sayfalarını bu klasöre ekleyerek her bir sayfayı `Site.master` ana sayfasıyla ilişkilendirdiğinizden emin olun:

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`

![Gelişmiş veri erişim katmanı senaryoları öğreticileri için ASP.NET sayfaları ekleme](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image1.png)

**Şekil 1**: Gelişmiş veri erişim katmanı senaryoları öğreticileri Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `AdvancedDAL` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image2.png)

**Şekil 2**: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image4.png))

Son olarak, bu sayfaları `Web.sitemap` dosyasına girdi olarak ekleyin. Özel olarak, toplu verilerle çalıştıktan sonra aşağıdaki biçimlendirmeyi ekleyin `<siteMapNode>`:

[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample3.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menüde artık gelişmiş DAL senaryoları öğreticilerinin öğeleri bulunur.

![Site Haritası artık gelişmiş DAL senaryoları öğreticilerinin girdilerini Içerir](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image5.png)

**Şekil 3**: site haritası artık gelişmiş dal senaryoları öğreticilerinin girdilerini içerir

## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>2\. Adım: Yeni saklı yordamlar oluşturmak için TableAdapter Yapılandırma

Geçici SQL deyimleri yerine saklı yordamlar kullanan bir veri erişim katmanı oluşturmayı göstermek için, `NorthwindWithSprocs.xsd`adlı `~/App_Code/DAL` klasörde yeni bir türü belirtilmiş veri kümesi oluşturulmasına izin verin. Bu işlemi önceki öğreticilerde ayrıntılandırmış olduğumuz için buradaki adımlara hızla devam edeceğiz. Yazılı bir veri kümesi oluşturma ve yapılandırma konusunda daha fazla adım adım yönergeler varsa, [veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-cs.md) öğreticisine geri bakın.

`DAL` klasöre sağ tıklayıp, yeni öğe Ekle ' yi seçerek ve Şekil 4 ' te gösterildiği gibi veri kümesi şablonunu seçerek projeye yeni bir veri kümesi ekleyin.

[![NorthwindWithSprocs. xsd adlı projeye yeni bir türü belirtilmiş veri kümesi ekleyin](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image6.png)

**Şekil 4**: `NorthwindWithSprocs.xsd` adlı projeye yeni bir türü belirtilmiş veri kümesi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image8.png))

Bu, yeni türü belirtilmiş veri kümesini oluşturur, Tasarımcısını açar, yeni bir TableAdapter oluşturur ve TableAdapter Yapılandırma Sihirbazı 'nı başlatır. TableAdapter Yapılandırma Sihirbazı 'Nın ilk adımı, birlikte çalışmak üzere veritabanını seçmenizi ister. Northwind veritabanına bağlantı dizesinin açılan listede listelenmesi gerekir. Bunu seçin ve Ileri ' ye tıklayın.

Bu sonraki ekrandan, TableAdapter 'ın veritabanına nasıl erişmesi gerektiğini seçebiliriz. Önceki öğreticilerde, ilk seçeneği seçtik ve SQL deyimlerini kullanın. Bu öğretici için ikinci seçeneği seçin, yeni saklı yordamlar oluşturun ve Ileri ' ye tıklayın.

[![TableAdapter 'a yeni saklı yordamlar oluşturmasını bildirin](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image9.png)

**Şekil 5**: TableAdapter 'A yeni saklı yordamlar oluşturmasını bildirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image11.png))

Geçici SQL deyimlerini kullanmakla tıpkı, aşağıdaki adımda TableAdapter s ana sorgusunun `SELECT` deyimini sağlamamız istenir. Ancak, burada doğrudan bir geçici sorgu gerçekleştirmek için girilen `SELECT` ifadesini kullanmak yerine, TableAdapter s Sihirbazı bu `SELECT` sorgusunu içeren bir saklı yordam oluşturacaktır.

Bu TableAdapter için aşağıdaki `SELECT` sorgusunu kullanın:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample4.sql)]

[![SELECT sorgusunu girin](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image12.png)

**Şekil 6**: `SELECT` sorgusunu girin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image14.png))

> [!NOTE]
> Yukarıdaki sorgu, `Northwind` türü belirtilmiş veri kümesindeki `ProductsTableAdapter` ana sorgusundan biraz farklılık gösterir. `Northwind` yazılan veri kümesindeki `ProductsTableAdapter` her bir ürün kategorisi ve tedarikçinin kategori adını ve şirket adını geri getirmek için iki bağıntılı alt sorgu içerdiğini hatırlayın. Bu ilgili verileri [birleştirme öğreticisini kullanmak için](updating-the-tableadapter-to-use-joins-cs.md) bir sonraki güncelleştirmede, bu ilişkili verilerin Bu TableAdapter 'a eklenmesinde bakacağız.

Gelişmiş Seçenekler düğmesine tıklamanız için bir dakikanızı ayırın. Burada, sihirbazın TableAdapter için INSERT, Update ve delete deyimleri oluşturup üretmeyeceğini, iyimser eşzamanlılık kullanılıp kullanılmayacağını ve ekleme ve güncelleştirme sonrasında veri tablosunun yenilenmesi gerekip gerekmediğini belirtebilirsiniz. INSERT, Update ve delete deyimlerini oluştur seçeneği varsayılan olarak denetlenir. İşaretli bırakın. Bu öğreticide, iyimser eşzamanlılık kullan seçeneğini işaretlenmemiş olarak bırakın.

Otomatik olarak TableAdapter Sihirbazı tarafından oluşturulan saklı yordamlara sahip olduğunda, veri tablosunu Yenile seçeneğinin yoksayıldığını görünür. Bu onay kutusunun işaretli olup olmadığına bakılmaksızın, saklı yordamlar ekleme ve güncelleştirme, adım 3 ' te göreceğiniz şekilde hemen eklemiş olan veya yalnızca güncelleştirilmiş kaydı alır.

![INSERT, Update ve delete deyimlerini oluştur seçeneğini Işaretlenmiş olarak bırak](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image15.png)

**Şekil 7**: INSERT, Update ve delete deyimlerini oluştur seçeneğini işaretli bırakın

> [!NOTE]
> İyimser eşzamanlılık kullan seçeneği işaretliyse, sihirbaz, diğer alanlarda değişiklik yaptıysanız verilerin güncelleştirilmesini önleyen `WHERE` yan tümcesine ek koşullar ekler. TableAdapter 'ın yerleşik iyimser eşzamanlılık denetimi özelliğini kullanma hakkında daha fazla bilgi için bkz. [Iyimser eşzamanlılık öğreticisi uygulama](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) .

`SELECT` sorgusunu girdikten ve INSERT, Update ve delete deyimlerini oluştur seçeneğinin işaretli olduğunu doğruladıktan sonra Ileri ' ye tıklayın. Şekil 8 ' de gösterilen bu sonraki ekran, sihirbazın veri seçme, ekleme, güncelleştirme ve silme için oluşturulacağı saklı yordamların adlarını ister. Bu saklı yordam adlarını `Products_Select`, `Products_Insert`, `Products_Update`ve `Products_Delete`olarak değiştirin.

[![saklı yordamları yeniden adlandır](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image16.png)

**Şekil 8**: saklı yordamları yeniden adlandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image18.png))

T-SQL ' i r-SQL ' i kullanarak dört saklı yordam oluşturmak için kullanılacak olan SQL betiğini Önizle düğmesine tıklayın. SQL betiği Önizleme iletişim kutusunda betiği bir dosyaya kaydedebilir veya panoya kopyalayabilirsiniz.

![Saklı yordamları oluşturmak için kullanılan SQL betiğini önizleyin](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image19.png)

**Şekil 9**: saklı yordamları oluşturmak IÇIN kullanılan SQL betiğini önizleyin

Saklı yordamları adlandırdıktan sonra TableAdapter 'a karşılık gelen yöntemleri adlandırmak için Ileri ' ye tıklayın. Geçici SQL deyimlerini kullanırken olduğu gibi, var olan bir DataTable 'ı dolduran veya yenisini döndüren yöntemler de oluşturabilirsiniz. Ayrıca, TableAdapter 'ın kayıtları eklemek, güncelleştirmek ve silmek için DB-Direct modelini içerip içermediğini de belirtebilirsiniz. Üç onay kutusu işaretli bırakın, ancak bir DataTable yöntemi Return The `GetProducts` (Şekil 10 ' da gösterildiği gibi) olarak yeniden adlandırın.

[Yöntemler Fill ve GetProducts adına ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image20.png)

**Şekil 10**: yöntemleri `Fill` ve `GetProducts` adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image22.png))

Sihirbazın gerçekleştireceği adımların özetini görmek için Ileri ' ye tıklayın. Son düğmesine tıklayarak Sihirbazı doldurun. Sihirbaz tamamlandıktan sonra, artık `ProductsDataTable`içermesi gereken DataSet s Designer 'a döndürülecektir.

[![DataSet s Designer yeni eklenen ProductsDataTable 'ı gösterir](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image23.png)

**Şekil 11**: DataSet s Designer yeni eklenen `ProductsDataTable` gösterir ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image25.png))

## <a name="step-3-examining-the-newly-created-stored-procedures"></a>3\. Adım: yeni oluşturulan saklı yordamları Inceleme

2\. adımda kullanılan TableAdapter Sihirbazı, verileri seçme, ekleme, güncelleştirme ve silmeye yönelik saklı yordamları otomatik olarak oluşturdu. Bu saklı yordamlar, Sunucu Gezgini gidip veritabanı saklı yordamları klasöründe ayrıntıya giderek Visual Studio aracılığıyla görüntülenebilir veya değiştirilebilir. Şekil 12 ' de gösterildiği gibi, Northwind veritabanı dört yeni saklı yordam içerir: `Products_Delete`, `Products_Insert`, `Products_Select`ve `Products_Update`.

![2\. adımda oluşturulan dört saklı yordam, veritabanı s saklı yordamları klasöründe bulunabilir](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image26.png)

**Şekil 12**: adım 2 ' de oluşturulan dört saklı yordam veritabanı s saklı yordamları klasöründe bulunabilir

> [!NOTE]
> Sunucu Gezgini görmüyorsanız, Görünüm menüsüne gidin ve Sunucu Gezgini seçeneğini belirleyin. 2\. adımda eklenen ürünle ilgili saklı yordamları görmüyorsanız, saklı yordamlar klasörüne sağ tıklayıp Yenile ' yi seçerek.

Saklı yordamı görüntülemek veya değiştirmek için Sunucu Gezgini adına çift tıklayın veya alternatif olarak, saklı yordama sağ tıklayıp Aç ' ı seçin. Şekil 13 açıldığında, `Products_Delete` saklı yordamını gösterir.

[![saklı yordamlar, Visual Studio Içinden açılabilir ve değiştirilebilir](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image27.png)

**Şekil 13**: saklı yordamlar, Visual Studio içinden açılabilir ve değiştirilebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image29.png))

Hem `Products_Delete` hem de `Products_Select` saklı yordamların içeriği oldukça basittir. Diğer yandan `Products_Insert` ve `Products_Update` saklı yordamları, `INSERT` ve `UPDATE` deyimlerinden sonra bir `SELECT` deyimi gerçekleştirdiklerinde daha yakından bir denetim garanti altına alır. Örneğin, aşağıdaki SQL `Products_Insert` saklı yordamını oluşturur:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample5.sql)]

Saklı yordam, TableAdapter s sihirbazında belirtilen `SELECT` sorgusunun döndürdüğü `Products` sütunları giriş parametresi olarak kabul eder ve bu değerler bir `INSERT` ifadesinde kullanılır. `INSERT` deyimden sonra, yeni eklenen kaydın `Products` sütun değerlerini (`ProductID`dahil) döndürmek için `SELECT` bir sorgu kullanılır. Bu yenileme özelliği, yeni eklenen `ProductRow` örneklerine `ProductID` Özellikler ' i veritabanı tarafından atanan otomatik artan değerlerle otomatik olarak güncelleştirdiğinde, toplu güncelleştirme modelini kullanarak yeni bir kayıt eklerken faydalıdır.

Aşağıdaki kod bu özelliği gösterir. Bu, `NorthwindWithSprocs` türü belirtilmiş veri kümesi için oluşturulmuş bir `ProductsTableAdapter` ve `ProductsDataTable` içerir. `ProductsRow` bir örnek oluşturup, değerlerini sağlayarak ve TableAdapter s `Update` yöntemi çağırarak `ProductsDataTable`geçirerek veritabanına yeni bir ürün eklenir. Dahili olarak, TableAdapter s `Update` yöntemi, geçirilen DataTable 'daki `ProductsRow` örnekleri numaralandırır (Bu örnekte yalnızca bir tane eklemiş olduğumuz) ve uygun INSERT, Update veya delete komutunu gerçekleştirir. Bu durumda, `Products` tabloya yeni bir kayıt ekleyen ve yeni eklenen kaydın ayrıntılarını döndüren `Products_Insert` saklı yordamı yürütülür. `ProductsRow` örneği `ProductID` değeri daha sonra güncellenir. `Update` yöntemi tamamlandıktan sonra, yeni eklenen kayıt s `ProductID` değerine `ProductsRow` s `ProductID` özelliği aracılığıyla erişebiliriz.

[!code-csharp[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample6.cs)]

Benzer `Products_Update` saklı yordam, `UPDATE` deyimlerinden sonra bir `SELECT` ifadesini içerir.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample7.sql)]

Bu saklı yordamın `ProductID`için iki giriş parametresi içerdiğini unutmayın: `@Original_ProductID` ve `@ProductID`. Bu işlevsellik, birincil anahtarın değiştirilebileceği senaryolara olanak sağlar. Örneğin, bir çalışan veritabanında, her çalışan kaydı, çalışan sosyal güvenlik numarasını birincil anahtar olarak kullanabilir. Mevcut bir çalışan sosyal güvenlik numarasını değiştirmek için, hem yeni sosyal güvenlik numarası hem de özgün bir değer sağlanmalıdır. `Products` tablosu için, `ProductID` sütunu bir `IDENTITY` sütunu olduğundan ve hiçbir şekilde değiştirilmemesi gerektiğinden, bu tür işlevler gerekli değildir. Aslında, `Products_Update` saklı yordamındaki `UPDATE` deyimleri, sütun listesine `ProductID` sütununu dahil eder. Bu nedenle, `@Original_ProductID` `UPDATE` deyimi s `WHERE` yan tümcesinde kullanıldığında, `Products` tablo için gereksiz ve `@ProductID` parametresiyle değiştirilebilir. Saklı yordam parametrelerinde değişiklik yaparken, bu saklı yordamı kullanan TableAdapter yönteminin da güncelleştirilmesini önemli olur.

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>4\. Adım: saklı yordam parametrelerini değiştirme ve TableAdapter 'ı güncelleştirme

`@Original_ProductID` parametresi gereksiz olduğundan, bunu `Products_Update` saklı yordamdan tamamen kaldıralım. `Products_Update` saklı yordamını açın, `@Original_ProductID` parametresini silin ve `UPDATE` deyimin `WHERE` yan tümcesinde `@Original_ProductID` olarak kullanılan parametre adını `@ProductID`olarak değiştirin. Bu değişiklikleri yaptıktan sonra, saklı yordamın içindeki T-SQL aşağıdaki gibi görünmelidir:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample8.sql)]

Bu değişiklikleri veritabanına kaydetmek için, araç çubuğunda Kaydet simgesine tıklayın veya CTRL + S tuşlarına basın. Bu noktada, `Products_Update` saklı yordamı bir `@Original_ProductID` giriş parametresi beklemez, ancak TableAdapter böyle bir parametreyi geçirecek şekilde yapılandırılmıştır. TableAdapter 'ın, veri kümesi Tasarımcısı ' nda TableAdapter ' ı seçip Özellikler penceresi ve `UpdateCommand` s `Parameters` koleksiyonundaki üç nokta işaretine tıklayarak `Products_Update` saklı yordama göndereceği parametreleri görebilirsiniz. Bu, Şekil 14 ' te gösterilen parametreler koleksiyon Düzenleyicisi iletişim kutusunu getirir.

![Parameters koleksiyonu Düzenleyicisi, Products_Update saklı yordamına geçirilen parametreleri listeler](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image30.png)

**Şekil 14**: parametreler koleksiyonu düzenleyicisi, `Products_Update` saklı yordamına geçirilen parametreleri listeler

Üye listesinden `@Original_ProductID` parametresini seçip Kaldır düğmesine tıklayarak bu parametreyi buradan kaldırabilirsiniz.

Alternatif olarak, tasarımcıda TableAdapter ' a sağ tıklayıp Yapılandır ' ı seçerek tüm yöntemler için kullanılan parametreleri yenileyebilirsiniz. Bu işlem, seçme, ekleme, güncelleştirme ve silme için kullanılan saklı yordamları, saklı yordamların alması beklenen parametrelerle birlikte listeleyerek TableAdapter Yapılandırma Sihirbazı 'nı getirir. Güncelleştirme açılır listesine tıklarsanız, artık `@Original_ProductID` dahil olmayan `Products_Update` saklı yordamların beklenen giriş parametrelerini görebilirsiniz (bkz. Şekil 15). TableAdapter tarafından kullanılan parametre koleksiyonunu otomatik olarak güncelleştirmek için son ' a tıklamanız yeterlidir.

[![bunun yerine, yöntem parametre koleksiyonlarını yenilemek için TableAdapter s Yapılandırma Sihirbazı 'nı kullanabilirsiniz](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image31.png)

**Şekil 15**: Alternatif olarak, kendi yöntem parametre koleksiyonlarını yenilemek için TableAdapter s Yapılandırma Sihirbazı 'nı kullanabilirsiniz ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image33.png))

## <a name="step-5-adding-additional-tableadapter-methods"></a>5\. Adım: ek TableAdapter yöntemleri ekleme

2\. adım gösterildiği gibi yeni bir TableAdapter oluştururken, ilgili saklı yordamların otomatik olarak oluşturulması kolaylaşır. Bir TableAdapter 'a başka yöntemler eklerken de aynı değer geçerlidir. Bunu göstermek için, s adım 2 ' de oluşturulan `ProductsTableAdapter` bir `GetProductByProductID(productID)` yöntemi eklemesine izin verin. Bu yöntem, `ProductID` bir değer alacak ve belirtilen ürünle ilgili ayrıntıları döndürecek.

TableAdapter ' a sağ tıklayıp bağlam menüsünden sorgu Ekle ' yi seçerek başlayın.

![TableAdapter 'a yeni bir sorgu ekleme](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image34.png)

**Şekil 16**: TableAdapter 'a yeni bir sorgu ekleme

Bu işlem, TableAdapter sorgu Yapılandırma Sihirbazı ' nı başlatacak ve bu, önce TableAdapter 'in veritabanına nasıl erişmesi gerektiğini sorar. Yeni bir saklı yordamın oluşturulmasını sağlamak için yeni bir saklı yordam oluştur seçeneğini belirleyin ve Ileri ' ye tıklayın.

[![yeni bir saklı yordam oluştur seçeneğini belirleyin](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image35.png)

**Şekil 17**: yeni bir saklı yordam oluştur seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image37.png))

Sonraki ekranda, çalıştırılacak sorgunun türünü, bir dizi satırı mı yoksa tek bir skalar değeri mi döndüreceğini veya bir `UPDATE`, `INSERT`veya `DELETE` bildirisini mi belirleyebileceğimizi öğreneceksiniz. `GetProductByProductID(productID)` yöntemi bir satır döndürdüğünden, satırı döndüren seç seçeneğinin seçili olduğunu ve sonraki düğmesine basın.

[![satır döndüren Seç seçeneğini belirleyin](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image38.png)

**Şekil 18**: SATıRı döndüren Seç seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image40.png))

Sonraki ekranda, yalnızca saklı yordamın adını (`dbo.Products_Select`) listeleyen TableAdapter s ana sorgusu görüntülenir. Saklı yordam adını, belirtilen bir ürün için tüm ürün alanlarını döndüren aşağıdaki `SELECT` ifadesiyle değiştirin:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample9.sql)]

[Saklı yordam adını bir SELECT sorgusuyla değiştirin ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image41.png)

**Şekil 19**: saklı yordam adını bir `SELECT` sorgusuyla değiştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image43.png))

Sonraki ekranda, oluşturulacak saklı yordamın adını yazmanız istenir. `Products_SelectByProductID` adı girin ve Ileri ' ye tıklayın.

[Yeni saklı yordamın adını ![Products_SelectByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image44.png)

**Şekil 20**: `Products_SelectByProductID` yeni saklı yordamı adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image46.png))

Sihirbazın son adımı, oluşturulan yöntem adlarını değiştirememize ve bir DataTable deseninin doldurulması, bir DataTable deseninin mi, yoksa her ikisinin de mi kullanılacağını belirtebileceğimizi sağlar. Bu yöntem için her iki seçeneği işaretli bırakın, ancak `FillByProductID` ve `GetProductByProductID`olarak yöntemleri yeniden adlandırın. Sihirbazın gerçekleştireceği adımların özetini görüntülemek için Ileri ' ye tıklayın ve Sihirbazı tamamlamak için son ' a tıklayın.

[TableAdapter s yöntemlerini Fillbyproductıd ve GetProductByProductID olarak yeniden adlandırın ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image47.png)

**Şekil 21**: TableAdapter s yöntemlerini `FillByProductID` ve `GetProductByProductID` olarak yeniden adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image49.png))

Sihirbazı tamamladıktan sonra TableAdapter yeni bir yönteme sahiptir `GetProductByProductID(productID)`, çağrıldığında, yeni oluşturulan `Products_SelectByProductID` saklı yordamı yürütür. Saklı yordamlar klasöründe ayrıntıya giderek ve `Products_SelectByProductID` açarak Sunucu Gezgini bu yeni saklı yordamı görüntülemek için bir dakikanızı ayırın (bunu görmüyorsanız, saklı yordamlar klasörüne sağ tıklayın ve Yenile ' yi seçin).

`SelectByProductID` saklı yordamının giriş parametresi olarak `@ProductID` aldığını ve sihirbazda girdiğimiz `SELECT` ifadesini yürüttüğünü unutmayın.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>6\. Adım: Iş mantığı katman sınıfı oluşturma

Eğitim Serisi boyunca, sunum katmanının tüm çağrılarını Iş mantığı katmanına (BLL) yaptığı bir katmanlı mimariyi sürdürmek için çaba duyuyoruz. Bu tasarım kararına uyacak şekilde, sunum katmanından ürün verilerine erişebilmek için önce yeni tür belirtilmiş veri kümesi için bir BLL sınıfı oluşturmanız gerekir.

`~/App_Code/BLL` klasöründe `ProductsBLLWithSprocs.cs` adlı yeni bir sınıf dosyası oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample11.cs)]

Bu sınıf, önceki öğreticilerden `ProductsBLL` sınıfı semantiğini taklit eder, ancak `NorthwindWithSprocs` veri kümesinden `ProductsTableAdapter` ve `ProductsDataTable` nesnelerini kullanır. Örneğin, sınıf dosyasının başlangıcında `ProductsBLL` `using NorthwindTableAdapters` bir ifadeye sahip olmak yerine, `ProductsBLLWithSprocs` sınıfı `using NorthwindWithSprocsTableAdapters`kullanır. Benzer şekilde, bu sınıfta kullanılan `ProductsDataTable` ve `ProductsRow` nesnelerine `NorthwindWithSprocs` ad alanı ön eki eklenir. `ProductsBLLWithSprocs` sınıfı, tek bir ürün örneğini eklemek, güncelleştirmek ve silmek için iki veri erişim yöntemi, `GetProducts` ve `GetProductByProductID`ve yöntemleri sağlar.

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>7\. Adım: sunum katmanından`NorthwindWithSprocs`veri kümesiyle çalışma

Bu noktada, temel alınan veritabanı verilerine erişmek ve bunları değiştirmek için saklı yordamları kullanan bir DAL oluşturduk. Ayrıca, ürün ekleme, güncelleştirme ve silme yöntemleriyle birlikte tüm ürünleri veya belirli bir ürünü almak için yöntemler içeren bir ilkel BLL sunuyoruz. Bu öğreticiyi kapatmak için s 'nin kayıtları görüntülemek, güncelleştirmek ve silmek için BLL s `ProductsBLLWithSprocs` sınıfını kullanan bir ASP.NET sayfası oluşturmasına izin verin.

`AdvancedDAL` klasöründeki `NewSprocs.aspx` sayfasını açın ve araç kutusu 'ndan bir GridView 'u `Products`adlandırarak tasarımcı üzerine sürükleyin. GridView s akıllı etiketinden, `ProductsDataSource`adlı yeni bir ObjectDataSource 'a bağlamayı seçin. ObjectDataSource 'u, Şekil 22 ' de gösterildiği gibi `ProductsBLLWithSprocs` sınıfını kullanacak şekilde yapılandırın.

[![, bu ObjectDataSource 'ı ProductsBLLWithSprocs sınıfını kullanacak şekilde yapılandırma](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image50.png)

**Şekil 22**: ObjectDataSource 'ı `ProductsBLLWithSprocs` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image52.png))

Seç sekmesindeki açılan listede iki seçenek bulunur `GetProducts` ve `GetProductByProductID`. GridView 'daki tüm ürünleri göstermek istediğimize göre `GetProducts` yöntemini seçin. GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listelerin her biri yalnızca bir yöntem içermelidir. Bu açılan listelerin her birinde uygun yöntemin seçili olduğundan emin olun ve ardından son ' a tıklayın.

ObjectDataSource Sihirbazı tamamlandıktan sonra Visual Studio, ürün verileri alanları için BoundFields ve bir CheckBoxField öğesini GridView 'a ekler. Akıllı etiketteki düzenlemenizi etkinleştir ve silmeyi etkinleştir seçeneklerini işaretleyerek, GridView s yerleşik düzenlemesini ve silme özelliklerini açın.

[Sayfa ![, Düzenle ve silme desteği etkinken bir GridView Içeriyor](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image53.png)

**Şekil 23**: sayfa, Düzenle ve silme desteğinin etkin olduğu bir GridView içeriyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image55.png))

Önceki öğreticilerde anlatıldığı gibi, ObjectDataSource 'un Sihirbazı tamamlandığında, Visual Studio `OldValuesParameterFormatString` özelliğini özgün\_{0}olarak ayarlar. Veri değiştirme özelliklerinin BLL 'lerimizde yöntemler tarafından beklenen parametrelere düzgün şekilde çalışması için, bu değerin varsayılan {0} olarak döndürülmesi gerekir. Bu nedenle, `OldValuesParameterFormatString` özelliğini {0} olarak ayarladığınızdan emin olun veya özelliği bildirime dayalı sözdiziminden tamamen kaldırın.

Veri kaynağı Yapılandırma Sihirbazı ' nı tamamladıktan sonra, GridView 'da yapılandırmayı ve silmeyi ve ObjectDataSource `OldValuesParameterFormatString` özelliğini varsayılan değerine döndürmekten sonra, sayfanın bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample12.aspx)]

Bu noktada, oluşturma arabirimini doğrulama içerecek şekilde özelleştirerek, `CategoryID` ve `SupplierID` sütunlarının DropDownLists olarak işlemesini, vb. Ayrıca Sil düğmesine bir istemci tarafı onayı ekleyebiliriz ve bu geliştirmeleri uygulamak için zaman atalım. Bununla birlikte, bu konular önceki öğreticilerde ele alındıklarından, bunları burada yeniden ele vermeyecektir.

GridView 'u geliştirip kullanmadığına bakılmaksızın, sayfa s Core özelliklerini bir tarayıcıda test edin. Şekil 24 ' ün gösterdiği gibi, sayfada satır başına düzen ve silme yetenekleri sağlayan bir GridView 'daki ürünler listelenir.

[Ürünlerin GridView 'dan görüntülenebilmesini, düzenlenmesini ve silinebilmesini ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image56.png)

**Şekil 24**: Ürünler GridView 'dan görüntülenebilir, düzenlenebilir ve silinebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image58.png))

## <a name="summary"></a>Özet

Türü belirtilmiş bir veri kümesindeki TableAdapters, geçici SQL deyimlerini kullanarak veya saklı yordamlar aracılığıyla veritabanındaki verilere erişebilir. Saklı yordamlarla çalışırken, mevcut saklı yordamlar kullanılabilir veya TableAdapter sihirbazına bir `SELECT` sorgusuna dayalı olarak yeni saklı yordamlar oluşturulabilir. Bu öğreticide, saklı yordamların bizim için otomatik olarak nasıl oluşturulduğunu araştırıyoruz.

Otomatik olarak oluşturulan saklı yordamlara sahip olmanın zaman tasarrufu sağlar, sihirbaz tarafından oluşturulan saklı yordamın kendi üzerinde oluşturduğumuza göre Hizalanmadığını belirli durumlar vardır. `@Original_ProductID` parametresi çok fazla olsa da, `@Original_ProductID` ve `@ProductID` giriş parametrelerini beklenen `Products_Update` saklı yordamı bir örnektir.

Birçok senaryoda, saklı yordamlar zaten oluşturulmuş olabilir veya saklı yordam komutları üzerinde daha fazla denetime sahip olmak için bunları el ile oluşturmak isteyebilirsiniz. Her iki durumda da, TableAdapter 'ın yöntemleri için mevcut saklı yordamları kullanmasını söylemek istiyoruz. Bunu bir sonraki öğreticide nasıl gerçekleştireceğinizi inceleyeceğiz.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Saklı yordamlar oluşturma ve sürdürme](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [Saklı yordamdan skalar verileri alma](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [SQL Server saklı yordam temelleri](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [Saklı yordamlar: genel bakış](http://www.sqlteam.com/item.asp?ItemID=563)
- [Saklı yordam yazma](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren, Lücü Geisenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
