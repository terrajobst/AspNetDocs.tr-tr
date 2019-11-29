---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-cs
title: Hesaplanan sütunlar ile çalışma (C#) | Microsoft Docs
author: rick-anderson
description: Veritabanı tablosu oluştururken Microsoft SQL Server, değeri genellikle başvurulan bir ifadeden hesaplanan bir hesaplanan sütun tanımlamanızı sağlar.
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 57459065-ed7c-4dfe-ac9c-54c093abc261
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-cs
msc.type: authoredcontent
ms.openlocfilehash: ad6a96f2721510c2478f707c8eed018ae797f27a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74603138"
---
# <a name="working-with-computed-columns-c"></a>Hesaplanan Sütunlar ile Çalışma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_CS.zip) veya [PDF 'yi indirin](working-with-computed-columns-cs/_static/datatutorial71cs1.pdf)

> Bir veritabanı tablosu oluştururken Microsoft SQL Server, değeri genellikle aynı veritabanı kaydındaki diğer değerlere başvuruda bulunan bir ifadeden hesaplanan bir sütun tanımlamanızı sağlar. Bu değerler veritabanında salt okunurdur ve TableAdapters ile çalışırken özel hususlar gerektirir. Bu öğreticide, hesaplanan sütunlara göre oluşan zorlukları nasıl karşılacağınızı öğreneceksiniz.

## <a name="introduction"></a>Giriş

Microsoft SQL Server, değerleri genellikle aynı tablodaki diğer sütunlardan değerlere başvuruda bulunan bir ifadeden *[hesaplanan sütunlara izin](https://msdn.microsoft.com/library/ms191250.aspx)* verir. Örnek olarak, bir zaman izleme veri modelinde `ServiceLog` adında `ServicePerformed`, `EmployeeID`, `Rate`ve `Duration`gibi sütunlar içeren bir tablo bulunabilir. Hizmet öğesi başına düşen miktar (süre ile çarpılarak) bir Web sayfası veya başka bir programlama arabirimi aracılığıyla hesaplanabilecek olsa da, bu bilgileri bildiren `AmountDue` adlı `ServiceLog` tabloya bir sütun eklemek yararlı olabilir. Bu sütun normal bir sütun olarak oluşturulabilir, ancak `Rate` veya `Duration` sütun değerleri değiştirildiğinde güncelleştirilmeleri gerekir. Daha iyi bir yaklaşım, `AmountDue` sütununu `Rate * Duration`ifade kullanarak hesaplanan bir sütun haline getirmek olacaktır. Bunun yapılması, bir sorguda başvurulduğu zaman SQL Server `AmountDue` sütun değerini otomatik olarak hesaplamasına neden olur.

Hesaplanan bir sütun değeri bir ifade tarafından belirlendiği için, bu tür sütunlar salt okunurdur ve bu nedenle `INSERT` veya `UPDATE` deyimlerine atanmış değerler olamaz. Ancak, hesaplanan sütunlar, geçici SQL deyimleri kullanan bir TableAdapter için ana sorgunun bir parçasıysa, otomatik olarak oluşturulan `INSERT` ve `UPDATE` deyimlerine otomatik olarak eklenir. Sonuç olarak, tüm hesaplanan sütunlara başvuruları kaldırmak için TableAdapter s `INSERT` ve `UPDATE` sorguları ve `InsertCommand` ve `UpdateCommand` özellikleri güncelleştirilmeleri gerekir.

Ad-hoc SQL deyimlerini kullanan bir TableAdapter ile hesaplanmış sütunlar kullanmanın bir zorluğu, TableAdapter Yapılandırma sihirbazının tamamlandığı her seferinde TableAdapter s `INSERT` ve `UPDATE` sorgularının otomatik olarak yeniden üretilme deneyiminden biridir. Bu nedenle, hesaplanan sütunlar `INSERT` el ile kaldırılır ve sihirbaz yeniden çalıştırıldığında `UPDATE` sorguları yeniden görüntülenir. Saklı yordamları kullanan TableAdapters bu Brit 'tan zarar vermese de, 3. adımda adreslendiriyoruz.

Bu öğreticide, Northwind veritabanındaki `Suppliers` tablosuna bir hesaplanan sütun ekleyecek ve ardından bu tabloyla ve hesaplanan sütunuyla çalışmak üzere ilgili bir TableAdapter oluşturacağız. TableAdapter Yapılandırma Sihirbazı kullanıldığında özelleştirmemiz kaybolmaması için TableAdapter 'ın geçici SQL deyimleri yerine saklı yordamları kullanmasına izin veririz.

Haydi başlayın!

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>1\. Adım:`Suppliers`tabloya hesaplanmış sütun ekleme

Northwind veritabanında hiç hesaplanmış sütun yok, bu nedenle bir kendimize eklemesi gerekir. Bu öğreticide, s için ilgili kişi adı, başlığı ve kullandıkları şirketi şu biçimde döndüren `FullContactName` adlı `Suppliers` tabloya bir hesaplanmış sütun ekleyelim: `ContactName` (`ContactTitle`, `CompanyName`). Bu hesaplanan sütun, tedarikçiler hakkında bilgiler görüntülenirken raporlarda kullanılabilir.

`Suppliers` tablo tanımını, Sunucu Gezgini `Suppliers` tabloya sağ tıklayıp bağlam menüsünden tablo tanımını aç ' ı seçerek başlatın. Bu, tablonun sütunlarını ve bunların veri türleri gibi özelliklerinin yanı sıra `NULL` bunlara izin verip vermeyeceklerini görüntüler. Hesaplanan bir sütun eklemek için sütunun adını tablo tanımına yazarak başlayın. Sonra, sütunun Özellikler penceresi hesaplanan sütun belirtimi bölümünün altındaki (formül) metin kutusuna ifadesini girin (bkz. Şekil 1). Hesaplanan sütunu `FullContactName` olarak adlandırın ve aşağıdaki ifadeyi kullanın:

[!code-sql[Main](working-with-computed-columns-cs/samples/sample1.sql)]

Dizelerin `+` işleci kullanılarak SQL 'de birleştirilmiş olabileceğini unutmayın. `CASE` deyimleri geleneksel programlama dilinde koşullu gibi kullanılabilir. Yukarıdaki ifadede `CASE` deyimi şöyle okunabilir: `ContactTitle` `NULL` değilse, `ContactTitle` değeri bir virgülle bitiştirilir, aksi halde hiçbir şey yayın. `CASE` deyimin yararlılığı hakkında daha fazla bilgi için bkz. [SQL `CASE` deyimlerinin gücü](http://www.4guysfromrolla.com/webtech/102704-1.shtml).

> [!NOTE]
> Burada `CASE` bir ifade kullanmak yerine `ISNULL(ContactTitle, '')`başka bir şekilde kullanılabilir. [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/library/ms184325.aspx) , null değilse *checkexpression* döndürür, aksi takdirde *replacementvalue*döndürür. `ISNULL` veya `CASE` Bu örnekte çalışacak olsa da `CASE` deyimin esnekliğinin `ISNULL`ile eşleştirilebileceği daha karmaşık senaryolar vardır.

Bu hesaplanan sütunu ekledikten sonra, ekran Şekil 1 ' de ekran görüntüsü gibi görünmelidir.

[Suppliers tablosuna FullContactName adlı bir hesaplanan sütun ![ekleyin](working-with-computed-columns-cs/_static/image2.png)](working-with-computed-columns-cs/_static/image1.png)

**Şekil 1**: `Suppliers` tabloya `FullContactName` adlı bir hesaplanan sütun ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image3.png))

Hesaplanan sütunu adlandırdıktan ve ifadesini girerek, araç çubuğundaki Kaydet simgesine tıklayarak CTRL + S tuşlarına basarak veya Dosya menüsüne gidip `Suppliers`Kaydet ' i seçerek değişiklikleri tabloya kaydedin.

Tablo kaydetme, `Suppliers` tablo s sütun listesindeki yeni eklenen sütun da dahil olmak üzere Sunucu Gezgini yenilemelidir. Ayrıca, (formül) metin kutusuna girilen ifade, gereksiz boşluğu kapsayan bir eşdeğer ifadeye otomatik olarak ayarlar, sütun adlarını köşeli ayraçlara (`[]`) ayırır ve işlem sırasını daha açık bir şekilde göstermek için parantez içerir:

[!code-sql[Main](working-with-computed-columns-cs/samples/sample2.sql)]

Microsoft SQL Server hesaplanan sütunlar hakkında daha fazla bilgi için [teknik belgelere](https://msdn.microsoft.com/library/ms191250.aspx)bakın. Ayrıca bkz. nasıl yapılır: hesaplanan sütunlar oluşturma hakkında adım adım yönergeler için [hesaplanan sütunları belirtme](https://msdn.microsoft.com/library/ms188300.aspx) .

> [!NOTE]
> Varsayılan olarak, hesaplanan sütunlar tabloda fiziksel olarak depolanmaz, ancak bunun yerine bir sorguda başvurulduğu her seferinde yeniden hesaplanır. Ancak kalıcı onay kutusunu işaretleyerek, hesaplanan sütunu tabloda fiziksel olarak depolamak için SQL Server bildirebilirsiniz. Bunun yapılması, hesaplanan sütunda bir dizinin oluşturulmasına izin verir ve bu, `WHERE` yan tümcelerinde hesaplanan sütun değerini kullanan sorguların performansını iyileştirebilir. Daha fazla bilgi için bkz. [hesaplanan sütunlarda dizin oluşturma](https://msdn.microsoft.com/library/ms189292.aspx) .

## <a name="step-2-viewing-the-computed-column-s-values"></a>2\. Adım: hesaplanan sütun değerlerini görüntüleme

Veri erişim katmanında çalışmaya başlamadan önce, s 'nin `FullContactName` değerlerini görüntülemesi için bir dakika sürme. Sunucu Gezgini, `Suppliers` tablo adına sağ tıklayın ve bağlam menüsünden Yeni sorgu ' yı seçin. Bu işlem, sorguya hangi tabloların ekleneceğini seçmenizi isteyen bir sorgu penceresi getirir. `Suppliers` tablosunu ekleyin ve Kapat ' a tıklayın. Ardından, üreticiler tablosundan `CompanyName`, `ContactName`, `ContactTitle`ve `FullContactName` sütunları kontrol edin. Son olarak, sorguyu yürütmek ve sonuçları görüntülemek için araç çubuğundaki kırmızı ünlem işareti simgesine tıklayın.

Şekil 2 ' de gösterildiği gibi sonuçlar, `CompanyName`, `ContactName`ve `ContactTitle` sütunları ldquo; biçimi kullanılarak listeleyen `FullContactName`içerir.`ContactName` (`ContactTitle`, `CompanyName`).

[FullContactName, ContactName biçimini kullanır ![(ContactTitle, CompanyName)](working-with-computed-columns-cs/_static/image5.png)](working-with-computed-columns-cs/_static/image4.png)

**Şekil 2**: `FullContactName` biçim `ContactName` (`ContactTitle`, `CompanyName`) kullanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image6.png))

## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>3\. Adım:`SuppliersTableAdapter`veri erişim katmanına ekleme

Uygulamamız içindeki Tedarikçi bilgileriyle çalışabilmek için önce DAL ' de bir TableAdapter ve DataTable oluşturmanız gerekir. İdeal olarak, bu, önceki öğreticilerde incelenen aynı basit adımlar kullanılarak gerçekleştirilir. Ancak, hesaplanan sütunlar ile çalışma, tartışarak tartışmayı hedefleyen birkaç wrınki tanıtır.

Geçici SQL deyimleri kullanan bir TableAdapter kullanıyorsanız, TableAdapter Yapılandırma Sihirbazı aracılığıyla yalnızca TableAdapter s ana sorgusunda hesaplanan sütunu dahil edebilirsiniz. Ancak, bu, hesaplanan sütunu içeren `INSERT` ve `UPDATE` deyimlerini otomatik olarak oluşturur. Bu yöntemlerden birini yürütmeye çalışırsanız, sütun, hesaplanan bir sütun olduğundan veya bir UNıON işlecinin sonucu olduğundan, *ColumnName* sütununa sahip bir `SqlException` değiştirilemez. `INSERT` ve `UPDATE` deyimleri TableAdapter s `InsertCommand` ve `UpdateCommand` özellikleriyle el ile ayarlanabilir, ancak TableAdapter Yapılandırma Sihirbazı yeniden çalıştırıldığında bu özelleştirmeler kaybedilir.

Geçici SQL deyimlerini kullanan TableAdapters brittleyeti nedeniyle, hesaplanan sütunlarla çalışırken saklı yordamları kullanmanız önerilir. Mevcut saklı yordamları kullanıyorsanız, TableAdapter 'ı, [yazılan veri kümesi s TableAdapters öğreticisi Için mevcut saklı yordamları kullanma konusunda](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) anlatıldığı gibi yapılandırmanız yeterlidir. Ancak, TableAdapter Sihirbazı sizin için saklı yordamlar oluşturuyorsa, başlangıçta ana sorgudan hesaplanan sütunları atlamak önemlidir. Ana sorguya bir hesaplanan sütun eklerseniz, TableAdapter Yapılandırma Sihirbazı sizi, işlem tamamlandıktan sonra, ilgili saklı yordamları oluşturmadığını bilgilendirecektir. Kısa bir süre önce, bir hesaplanan sütun içermeyen ana sorgu kullanarak TableAdapter 'ı yapılandırmanız ve ardından karşılık gelen saklı yordamı ve TableAdapter s `SelectCommand` hesaplanan sütunu içerecek şekilde el ile güncelleştirmeniz gerekir. Bu yaklaşım, TableAdapter 'ın`JOIN`*s* öğreticisini [kullanmak için güncelleştirmede](updating-the-tableadapter-to-use-joins-cs.md) kullanılan bir benzerine benzer.

Bu öğreticide, s için yeni bir TableAdapter ekleyelim ve saklı yordamları sizin için otomatik olarak oluşturalım. Sonuç olarak, başlangıçta `FullContactName` hesaplanmış sütunu ana sorgudan atlıyoruz.

`~/App_Code/DAL` klasöründe `NorthwindWithSprocs` veri kümesini açarak başlayın. Tasarımcıya sağ tıklayın ve bağlam menüsünden Yeni bir TableAdapter eklemeyi seçin. Bu, TableAdapter Yapılandırma Sihirbazı 'nı başlatır. Verilerin sorgulanme veritabanını belirtin (`Web.config``NORTHWNDConnectionString`) ve Ileri ' ye tıklayın. `Suppliers` tablosunu sorgulamak veya değiştirmek için bir saklı yordam oluşturmadığımız için yeni saklı yordamlar oluştur seçeneğini belirleyin, böylece sihirbaz bunları bizimle oluşturacak ve Ileri ' ye tıklacaktır.

[![yeni saklı yordamlar oluştur seçeneğini belirleyin](working-with-computed-columns-cs/_static/image8.png)](working-with-computed-columns-cs/_static/image7.png)

**Şekil 3**: Yeni saklı yordamlar oluştur seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image9.png))

Sonraki adım bize ana sorgu sorar. Her bir tedarikçi için `SupplierID`, `CompanyName`, `ContactName`ve `ContactTitle` sütunları döndüren aşağıdaki sorguyu girin. Bu sorgu, hesaplanan sütunu (`FullContactName`) tamamen atlayacağını unutmayın. Bu sütunu 4. adıma dahil etmek için ilgili saklı yordamı güncelleştireceğiz.

[!code-sql[Main](working-with-computed-columns-cs/samples/sample3.sql)]

Ana sorguyu girdikten ve Ileri 'ye tıkladıktan sonra sihirbaz, oluşturacak dört saklı yordamı adı etmemizi sağlar. Bu saklı yordamları `Suppliers_Select`, `Suppliers_Insert`, `Suppliers_Update`ve `Suppliers_Delete`Şekil 4 ' ün gösterildiği şekilde adlandırın.

[Otomatik olarak oluşturulan saklı yordamların adlarını özelleştirmek ![](working-with-computed-columns-cs/_static/image11.png)](working-with-computed-columns-cs/_static/image10.png)

**Şekil 4**: otomatik olarak oluşturulan saklı yordamların adlarını özelleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image12.png))

Sonraki sihirbaz adımı, TableAdapter s yöntemlerini adlandırma ve verilere erişmek ve verileri güncelleştirmek için kullanılan desenleri belirtmemizi sağlar. Üç onay kutusu işaretli bırakın, ancak `GetData` yöntemi `GetSuppliers`olarak yeniden adlandırın. Sihirbazı tamamladığınızda son ' a tıklayın.

[GetData yöntemini GetSuppliers olarak yeniden adlandırma ![](working-with-computed-columns-cs/_static/image14.png)](working-with-computed-columns-cs/_static/image13.png)

**Şekil 5**: `GetData` yöntemini `GetSuppliers` olarak yeniden adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image15.png))

Son ' a tıklandıktan sonra, sihirbaz dört saklı yordam oluşturur ve TableAdapter ve karşılık gelen DataTable öğesini yazılan veri kümesine ekler.

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>4\. Adım: hesaplanan sütunu TableAdapter s ana sorgusunda ekleme

Şimdi, adım 3 ' te oluşturulan TableAdapter ve DataTable `FullContactName` hesaplanan sütunu içerecek şekilde güncelleştirmeniz gerekiyor. Bu iki adımdan oluşur:

1. `FullContactName` hesaplanan sütununu döndürmek için `Suppliers_Select` saklı yordamı güncelleştiriliyor ve
2. DataTable, karşılık gelen bir `FullContactName` sütununu içerecek şekilde güncelleştiriliyor.

Sunucu Gezgini giderek ve saklı yordamlar klasörünün detayına giderek başlayın. `Suppliers_Select` saklı yordamını açın ve `SELECT` sorgusunu `FullContactName` hesaplanan sütununu içerecek şekilde güncelleştirin:

[!code-sql[Main](working-with-computed-columns-cs/samples/sample4.sql)]

Araç çubuğundaki Kaydet simgesine tıklayarak, CTRL + S tuşlarına basarak veya Dosya menüsünden `Suppliers_Select` Kaydet seçeneğini belirleyerek saklı yordamdaki değişiklikleri kaydedin.

Ardından, veri kümesi Tasarımcısına dönün, `SuppliersTableAdapter`sağ tıklayın ve bağlam menüsünden Yapılandır ' ı seçin. `Suppliers_Select` sütununun artık veri sütunları koleksiyonundaki `FullContactName` sütununu içerdiğini unutmayın.

[DataTable s sütunlarını güncelleştirmek ![TableAdapter Yapılandırma Sihirbazı 'nı çalıştırın](working-with-computed-columns-cs/_static/image17.png)](working-with-computed-columns-cs/_static/image16.png)

**Şekil 6**: DataTable s sütunlarını güncelleştirmek için TableAdapter s Yapılandırma Sihirbazı 'nı çalıştırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image18.png))

Sihirbazı tamamladığınızda son ' a tıklayın. Bu, `SuppliersDataTable`otomatik olarak karşılık gelen bir sütun ekler. TableAdapter Sihirbazı, `FullContactName` sütununun hesaplanmış bir sütun olduğunu ve bu nedenle salt okunurdur algılaması için yeterince akıllı bir değer. Sonuç olarak, sütun s `ReadOnly` özelliğini `true`olarak ayarlar. Bunu doğrulamak için `SuppliersDataTable` sütunu seçin ve sonra Özellikler penceresi gidin (bkz. Şekil 7). `FullContactName` sütun `DataType` ve `MaxLength` özelliklerinin de uygun şekilde ayarlandığını unutmayın.

[![FullContactName sütunu salt okunurdur olarak Işaretlendi](working-with-computed-columns-cs/_static/image20.png)](working-with-computed-columns-cs/_static/image19.png)

**Şekil 7**: `FullContactName` sütunu salt okunurdur ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image21.png))

## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>5\. Adım: TableAdapter 'a`GetSupplierBySupplierID`yöntemi ekleme

Bu öğreticide, sağlayıcıları güncellenebilir bir kılavuzda görüntüleyen bir ASP.NET sayfası oluşturacağız. Önceki öğreticilerde, bu belirli kaydı DAL içinden türü kesin belirlenmiş bir DataTable olarak alarak Iş mantığı katmanından tek bir kaydı güncelleştirdik, özelliklerini güncelledi ve sonra değişiklikleri veritabanı. Bu ilk adımı gerçekleştirmek için, DAL üzerinden güncellenmekte olan kaydı almak için önce DAL ' a bir `GetSupplierBySupplierID(supplierID)` yöntemi eklememiz gerekir.

Veri kümesi tasarımında `SuppliersTableAdapter` sağ tıklayın ve bağlam menüsünden sorgu Ekle seçeneğini belirleyin. Adım 3 ' te yaptığımız gibi, sihirbazın yeni saklı yordam oluştur seçeneğini belirleyerek ABD için yeni bir saklı yordam oluşturmasına izin verin (Bu sihirbaz adımının ekran görüntüsü için Şekil 3 ' e geri bakın). Bu yöntem birden çok sütunlu bir kayıt döndürecek olduğundan, satırları döndüren ve Ileri ' ye tıkladığımız bir SQL sorgusu kullanmak istediğimiz olduğunu belirtin.

[![satırları döndüren Seç seçeneğini belirleyin](working-with-computed-columns-cs/_static/image23.png)](working-with-computed-columns-cs/_static/image22.png)

**Şekil 8**: satırları döndüren Seç seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image24.png))

Sonraki adım, sorgunun bu yöntem için kullanması için bizi uyarır. Ana sorguyla, ancak belirli bir tedarikçi için aynı veri alanlarını döndüren aşağıdakini girin.

[!code-sql[Main](working-with-computed-columns-cs/samples/sample5.sql)]

Sonraki ekranda, otomatik olarak oluşturulacak saklı yordamın adı soruluyor. Bu saklı yordamı `Suppliers_SelectBySupplierID` adlandırın ve Ileri ' ye tıklayın.

[Saklı yordamın adını ![Suppliers_SelectBySupplierID](working-with-computed-columns-cs/_static/image26.png)](working-with-computed-columns-cs/_static/image25.png)

**Şekil 9**: saklı yordamın `Suppliers_SelectBySupplierID` adlandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image27.png))

Son olarak, sihirbaz bize veri erişimi desenleri ve TableAdapter için kullanılacak yöntem adlarını sorar. Her iki onay kutusu işaretli kalsın, ancak `FillBy` ve `GetDataBy` yöntemlerini sırasıyla `FillBySupplierID` ve `GetSupplierBySupplierID`olarak yeniden adlandırın.

[![ad TableAdapter metotları FillBySupplierID ve Getsupplierbysupplierıd](working-with-computed-columns-cs/_static/image29.png)](working-with-computed-columns-cs/_static/image28.png)

**Şekil 10**: TableAdapter metotlarını `FillBySupplierID` ve `GetSupplierBySupplierID` adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image30.png))

Sihirbazı tamamladığınızda son ' a tıklayın.

## <a name="step-6-creating-the-business-logic-layer"></a>6\. Adım: Iş mantığı katmanını oluşturma

Adım 1 ' de oluşturulan hesaplanmış sütunu kullanan bir ASP.NET sayfası oluşturmadan önce, BLL 'ye karşılık gelen yöntemleri eklememiz gerekir. Adım 7 ' de oluşturacağınız ASP.NET sayfamız, kullanıcıların tedarikçilerini görüntülemesine ve düzenlemesine izin verir. Bu nedenle BLL 'nin tüm tedarikçileri ve belirli bir tedarikçiyi güncelleştirmek için en az bir yöntem sağlaması gerekir.

`~/App_Code/BLL` klasöründe `SuppliersBLLWithSprocs` adlı yeni bir sınıf dosyası oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](working-with-computed-columns-cs/samples/sample6.cs)]

Diğer BLL sınıfları gibi, `SuppliersBLLWithSprocs` iki `public` yöntemi ile birlikte `SuppliersTableAdapter` sınıfının bir örneğini döndüren bir `protected` `Adapter` özelliğine sahiptir: `GetSuppliers` ve `UpdateSupplier`. `GetSuppliers` yöntemi, veri erişim katmanında karşılık gelen `GetSupplier` yöntemi tarafından döndürülen `SuppliersDataTable` çağırır ve döndürür. `UpdateSupplier` yöntemi, DAL s `GetSupplierBySupplierID(supplierID)` yöntemine yapılan bir çağrı aracılığıyla güncelleştirilmekte olan belirli bir tedarikçi hakkındaki bilgileri alır. Daha sonra `CategoryName`, `ContactName`ve `ContactTitle` özelliklerini güncelleştirir ve değiştirilen `SuppliersRow` nesnesini geçirerek veri erişim katmanı s `Update` yöntemini çağırarak bu değişiklikleri veritabanına kaydeder.

> [!NOTE]
> `SupplierID` ve `CompanyName`dışında, Suppliers tablosundaki tüm sütunlar `NULL` değerlere izin verir. Bu nedenle, geçirilen `contactName` veya `contactTitle` parametreleri `null`, sırasıyla `ContactTitle` ve `NULL` yöntemlerini kullanarak karşılık gelen `ContactName` ve `SetContactNameNull` özelliklerini `SetContactTitleNull` bir veritabanı değerine ayarlamanız gerekir.

## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>7\. Adım: sunu katmanından hesaplanan sütunla çalışma

`Suppliers` tablosuna eklenen ve DAL ve BLL 'nin buna uygun olarak güncelleştirildiği hesaplanan sütun, `FullContactName` hesaplanan sütunla çalışacak bir ASP.NET sayfası oluşturmaya hazırız. `ComputedColumns.aspx` sayfasını `AdvancedDAL` klasöründen açarak başlatın ve araç kutusundan bir GridView 'ı tasarımcı üzerine sürükleyin. GridView s `ID` özelliğini `Suppliers` ve akıllı etiketinden `SuppliersDataSource`adlı yeni bir ObjectDataSource 'a bağlayın. ObjectDataSource 'ı 6. adımda geri eklediğimiz `SuppliersBLLWithSprocs` sınıfını kullanacak şekilde yapılandırın ve Ileri ' ye tıklayın.

[SuppliersBLLWithSprocs sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ![](working-with-computed-columns-cs/_static/image32.png)](working-with-computed-columns-cs/_static/image31.png)

**Şekil 11**: `SuppliersBLLWithSprocs` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image33.png))

`SuppliersBLLWithSprocs` sınıfında tanımlanmış iki yöntem vardır: `GetSuppliers` ve `UpdateSupplier`. Bu iki yöntemin sırasıyla SELECT ve UPDATE sekmelerinde belirtildiğinden emin olun ve ObjectDataSource 'un yapılandırmasını gerçekleştirmek için son ' a tıklayın.

Veri kaynağı Yapılandırma Sihirbazı tamamlandıktan sonra Visual Studio döndürülen her veri alanı için bir BoundField ekler. `SupplierID` BoundField öğesini kaldırın ve `CompanyName`, `ContactName`, `ContactTitle`ve `FullContactName` BoundFields `HeaderText` özelliklerini sırasıyla Şirket, Iletişim adı, başlık ve tam Iletişim adı ile değiştirin. Akıllı etikette, GridView s yerleşik Düzenle özelliklerini açmak için Düzenle etkinleştir onay kutusunu işaretleyin.

GridView 'a BoundFields eklemenin yanı sıra, veri kaynağı Sihirbazı 'nın tamamlanması, Visual Studio 'Nun ObjectDataSource `OldValuesParameterFormatString` özelliğini özgün\_{0}ayarlamaya da neden olur. Bu ayarı, {0} varsayılan değerine geri döndürür.

GridView ve ObjectDataSource 'ta bu düzenlemeleri yaptıktan sonra, bunların bildirime dayalı biçimlendirmesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](working-with-computed-columns-cs/samples/sample7.aspx)]

Ardından, bu sayfayı bir tarayıcı aracılığıyla ziyaret edin. Şekil 12 ' de gösterildiği gibi, her tedarikçi, değeri yalnızca `ContactName` (`ContactTitle`, `CompanyName`) olarak biçimlendirilen diğer üç sütunun birleşimi olan `FullContactName` sütununu içeren bir kılavuzda listelenir.

[Her tedarikçinin ![kılavuzda listelenmesi](working-with-computed-columns-cs/_static/image35.png)](working-with-computed-columns-cs/_static/image34.png)

**Şekil 12**: her tedarikçi kılavuzda listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image36.png))

Belirli bir tedarikçinin Düzenle düğmesine tıklamak geri göndermeye neden olur ve bu satırın düzenleme arabiriminde oluşturulmasını ister (bkz. Şekil 13). İlk üç sütun varsayılan düzen arabiriminde işlenir-`Text` özelliği veri alanı değerine ayarlanmış bir TextBox denetimidir. Ancak `FullContactName` sütunu metin olarak kalır. Veri kaynağı Yapılandırma Sihirbazı tamamlandıktan sonra BoundFields GridView 'a eklendiğinde, `SuppliersDataTable` ilgili `FullContactName` sütununun `ReadOnly` özelliği `true`olarak ayarlandığı için `FullContactName` BoundField `ReadOnly` özelliği `true` olarak ayarlanmıştır. 4\. adımda belirtildiği gibi, TableAdapter sütunun hesaplanan bir sütun olduğunu algıladığından `FullContactName` s `ReadOnly` özelliği `true` olarak ayarlanmıştır.

[![FullContactName sütunu düzenlenebilir değil](working-with-computed-columns-cs/_static/image38.png)](working-with-computed-columns-cs/_static/image37.png)

**Şekil 13**: `FullContactName` sütunu düzenlenebilir değil ([tam boyutlu görüntüyü görüntülemek için tıklayın](working-with-computed-columns-cs/_static/image39.png))

Önceden bir veya daha fazla düzenlenebilir sütunun değerini güncelleştirip Güncelleştir ' e tıklayın. `FullContactName` s değerinin değişikliği yansıtmak için otomatik olarak nasıl güncelleştirileceğini aklınızda edin.

> [!NOTE]
> GridView Şu anda düzenlenebilir alanlar için BoundFields kullanır ve bu, varsayılan düzenleme arabirimine neden olur. `CompanyName` alanı gerekli olduğundan, bir RequiredFieldValidator içeren bir TemplateField öğesine dönüştürülmelidir. Bunu ilgilendiğiniz okuyucu için bir alıştırma olarak bırakıyorum. Bir BoundField öğesini TemplateField 'a dönüştürüp doğrulama denetimlerini ekleyerek adım adım yönergeler için, oluşturma [ve arabirim ekleme öğreticisine doğrulama denetimleri ekleme](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) öğreticisine başvurun.

## <a name="summary"></a>Özet

Tablo için şema tanımlarken, Microsoft SQL Server hesaplanan sütunların eklenmesine izin verir. Bunlar, genellikle aynı kayıttaki diğer sütunlardan değerlere başvuruda bulunan bir ifadeden değerler hesaplanan sütunlardır. Hesaplanan sütunların değerleri bir ifadeye dayalı olduğundan, salt okunurdur ve bir `INSERT` veya `UPDATE` deyiminde bir değer atanamaz. Bu, otomatik olarak karşılık gelen `INSERT`, `UPDATE`ve `DELETE` deyimlerini oluşturmaya çalışan bir TableAdapter 'ın ana sorgusunda, hesaplanan bir sütun kullanırken zorluk sergiler.

Bu öğreticide, hesaplanan sütunların karşılaştığı sorunları atlama tekniklerini ele aldık. Özellikle, TableAdapters ' deki, geçici SQL deyimlerini kullanan britttalet 'i aşmak için TableAdapter 'imizde saklı yordamlar kullandık. TableAdapter sihirbazının yeni saklı yordamlar oluşturmasına gerek kalmadan, mevcut oldukları veri değişikliği saklı yordamlarının oluşturulmasını önlediği için ana sorgunun başlangıçta hesaplanan sütunları atmız önemlidir. TableAdapter başlangıçta yapılandırıldıktan sonra, `SelectCommand` saklı yordamı, hesaplanan sütunları içerecek şekilde yeniden gösterilebilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Tepi Geisenow ve Teresa Murphy. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](adding-additional-datatable-columns-cs.md)
> [İleri](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs.md)
