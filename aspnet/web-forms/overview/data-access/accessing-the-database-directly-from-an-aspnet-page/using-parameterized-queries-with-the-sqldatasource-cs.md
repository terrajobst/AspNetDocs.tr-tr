---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
title: SqlDataSource ile parametreli sorgular kullanma (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, SqlDataSource denetimine baktığımız devam ediyoruz ve parametreli sorguların nasıl tanımlanacağını öğreneceksiniz. Parametreler her iki yaprak da belirlenebilir...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9128aaac-afe2-449f-84b2-bb1d035083c4
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 241dc8c089d4faa9eb95a63684e8a56756bb302c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78552481"
---
# <a name="using-parameterized-queries-with-the-sqldatasource-c"></a>SqlDataSource ile Parametreli Sorgular Kullanma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_CS.exe) veya [PDF 'yi indirin](using-parameterized-queries-with-the-sqldatasource-cs/_static/datatutorial48cs1.pdf)

> Bu öğreticide, SqlDataSource denetimine baktığımız devam ediyoruz ve parametreli sorguların nasıl tanımlanacağını öğreneceksiniz. Parametreler hem bildirimli hem de programlı olarak belirtilebilir ve sorgu dizesi, oturum durumu, diğer denetimler ve daha fazlası gibi bir dizi konumdan alınabilir.

## <a name="introduction"></a>Giriş

Önceki öğreticide, verileri doğrudan bir veritabanından almak için SqlDataSource denetimini nasıl kullanacağınızı gördük. Veri kaynağı Yapılandırma Sihirbazı ' nı kullanarak, veritabanını seçebiliriz: bir tablo ya da görünümden döndürülecek sütunları seçme; özel bir SQL ifadesini girin; ya da bir saklı yordam kullanın. Bir tablo veya görünümden sütun seçip ya da özel bir SQL bildirisini girerek, SqlDataSource Control s `SelectCommand` özelliği elde edilen geçici SQL `SELECT` bildirimine atanır ve SqlDataSource s `Select()` yöntemi çağrıldığında (programlama yoluyla veya otomatik olarak bir veri Web denetiminden) yürütülecek olan bu `SELECT` deyimidir.

Önceki öğretici, tanıtımlar `WHERE` yan tümcelerinde kullanılan SQL `SELECT` deyimleri. `SELECT` bildiriminde, döndürülen sonuçları sınırlandırmak için `WHERE` yan tümcesi kullanılabilir. Örneğin, $50,00 'den daha fazla maliyetlendirme ürünlerin adlarını göstermek için aşağıdaki sorguyu kullanabiliriz:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample1.sql)]

Genellikle, bir `WHERE` yan tümcesinde kullanılan değerler, bir QueryString değeri, bir oturum değişkeni veya sayfadaki bir Web denetiminden kullanıcı girişi gibi bir dış kaynağa göre belirlenir. İdeal olarak, bu tür girişler *parametrelerin*kullanımı ile belirtilir. Microsoft SQL Server, parametreleri ' de olduğu gibi `@parameterName`kullanılarak gösterilir:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample2.sql)]

SqlDataSource, hem `SELECT` deyimleri hem de `INSERT`, `UPDATE`ve `DELETE` deyimleri için parametreli sorguları destekler. Ayrıca, parametre değerleri, QueryString, oturum durumu, sayfadaki denetimler ve bu şekilde bir veya program aracılığıyla atanabilir çeşitli kaynaklardan otomatik olarak alınabilir. Bu öğreticide, parametreli sorguların nasıl tanımlanacağını ve parametre değerlerinin hem bildirimli hem de programlı olarak nasıl belirtilme hakkında bilgi edineceksiniz.

> [!NOTE]
> Önceki öğreticide, SqlDataSource ile ilk 46 öğretici üzerinde seçim aracımız ve kavramsal benzerlikleri gösteren ObjectDataSource karşılaştırdık. Bu benzerlikler parametrelere de genişletilir. Iş mantığı katmanındaki yöntemlere yönelik giriş parametreleriyle eşlenen ObjectDataSource s parametreleri. SqlDataSource ile parametreler doğrudan SQL sorgusu içinde tanımlanır. Her iki denetim de `Select()`, `Insert()`, `Update()`ve `Delete()` yöntemlerine yönelik parametre koleksiyonlarına sahiptir ve her ikisi de bu parametre değerlerini önceden tanımlanmış kaynaklardan (QueryString değerleri, oturum değişkenleri vb.) doldurulmuş veya programlı olarak atanmış olabilir.

## <a name="creating-a-parameterized-query"></a>Parametreleştirilmiş Sorgu Oluşturma

SqlDataSource denetimi veri kaynağı Yapılandırma Sihirbazı, veritabanı kayıtlarını almak için yürütülecek komutu tanımlamaya yönelik üç Aven, sağlar:

- Varolan bir tablo veya görünümden sütunları seçerek,
- Özel bir SQL ifadesini girerek veya
- Saklı yordam seçerek

Varolan bir tablo veya görünümden sütun seçerken, `WHERE` yan tümcesinin parametreleri Add `WHERE` yan tümcesi iletişim kutusu aracılığıyla belirtilmelidir. Ancak, özel bir SQL deyimi oluştururken, parametreleri doğrudan `WHERE` yan tümcesine girebilirsiniz (her parametreyi göstermek için `@parameterName` kullanabilirsiniz). [Saklı yordam](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1) bir veya daha fazla SQL deyiminden oluşur ve bu deyimler parametreli olabilir. Ancak SQL deyimlerde kullanılan parametreler, saklı yordama giriş parametresi olarak geçirilmelidir.

Parametreli bir sorgu oluşturmak, SqlDataSource s `SelectCommand` nasıl belirtiğinize bağlıdır. bu yana, her üç yaklaşımdan birini göz atalım. Başlamak için `SqlDataSource` klasöründeki `ParameterizedQueries.aspx` sayfasını açın, araç kutusu 'ndaki bir SqlDataSource denetimini tasarımcı üzerine sürükleyin ve `ID` `Products25BucksAndUnderDataSource`olarak ayarlayın. Sonra, denetim öğeleri akıllı etiketinden veri kaynağını Yapılandır bağlantısına tıklayın. Kullanılacak veritabanını seçin (`NORTHWINDConnectionString`) ve Ileri ' ye tıklayın.

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>1\. Adım: tablo veya görünümden sütunları çekerken`WHERE`yan tümcesi ekleme

SqlDataSource denetimiyle veritabanından döndürülecek verileri seçerken, veri kaynağını yapılandırma Sihirbazı, var olan bir tablo veya görünümden döndürülecek sütunları yalnızca seçmemizi sağlar (bkz. Şekil 1). Bunun yapılması, SqlDataSource s `Select()` yöntemi çağrıldığında veritabanına gönderilen bir SQL `SELECT` ifadesini otomatik olarak oluşturur. Önceki öğreticide yaptığımız gibi, açılan listeden Ürünler tablosunu seçin ve `ProductID`, `ProductName`ve `UnitPrice` sütunlarını kontrol edin.

[Tablo veya görünümden döndürülecek sütunları ![seçme](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.png)

**Şekil 1**: tablo veya görünümden döndürülecek sütunları seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.png))

`SELECT` bildirimine bir `WHERE` yan tümcesi eklemek için, Add `WHERE` Clause iletişim kutusunu (bkz. Şekil 2) getiren `WHERE` düğmesine tıklayın. `SELECT` sorgusunun döndürdüğü sonuçları sınırlamak üzere bir parametre eklemek için, önce verileri filtrelemek için sütunu seçin. Sonra, filtreleme için kullanılacak işleci seçin (=, &lt;, &lt;=, &gt;, vb.). Son olarak, sorgu dizesi veya oturum durumu gibi parametre değeri kaynağını seçin. Parametresini yapılandırdıktan sonra, `SELECT` sorgusuna eklemek için Ekle düğmesine tıklayın.

Bu örnekte, s yalnızca `UnitPrice` değeri $25,00 ' den küçük veya buna eşit olan sonuçları döndürmenizi sağlar. Bu nedenle, sütun açılan listesinden `UnitPrice` seçin ve Işleç açılan listesinden &lt;= seçeneğini belirleyin. Sabit kodlanmış bir parametre değeri ($25,00 gibi) kullanırken veya parametre değeri programlı olarak belirtilebiliyorsa, kaynak açılan listesinden hiçbiri ' ni seçin. Sonra, metin kutusu 25,00 ' de sabit kodlanmış parametre değerini girin ve Ekle düğmesine tıklayarak işlemi doldurun.

[WHERE yan tümcesi Ekle Iletişim kutusundan döndürülen sonuçları sınırlayın ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.png)

**Şekil 2**: `WHERE` yan tümce Ekle Iletişim kutusundan döndürülen sonuçları sınırlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.png))

Parametre eklendikten sonra, veri kaynağını yapılandırma sihirbazına dönmek için Tamam ' a tıklayın. Sihirbazın alt kısmındaki `SELECT` deyimi artık `@UnitPrice`adlı bir parametreye sahip bir `WHERE` yan tümcesi içermelidir:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample3.sql)]

> [!NOTE]
> `WHERE` yan tümce Ekle iletişim kutusundan `WHERE` yan tümcesinde birden çok koşul belirtirseniz, sihirbaz bunları `AND` işleciyle birleştirir. `WHERE` yan tümcesine bir `OR` (`WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`gibi) eklemeniz gerekiyorsa, Özel SQL deyimi ekranından `SELECT` deyimi oluşturmanız gerekir.

SqlDataSource yapılandırmasını tamamlama (Ileri ' ye tıklayın, ardından son ' a tıklayın) ve ardından SqlDataSource s bildirim temelli işaretlemesini inceleyin. Biçimlendirme artık, `SelectCommand`parametrelere ilişkin kaynakları içeren `<SelectParameters>` bir koleksiyon içerir.

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample4.aspx)]

SqlDataSource s `Select()` yöntemi çağrıldığında, veritabanına gönderilmeden önce `SelectCommand` `@UnitPrice` parametresine `UnitPrice` parametre değeri (25,00) uygulanır. Net sonucu, `Products` tablosundan yalnızca $25,00 ' den küçük veya buna eşit olan ürünler döndürülür. Bunu onaylamak için, sayfaya bir GridView ekleyin, bu veri kaynağına bağlayın ve sonra sayfayı bir tarayıcıdan görüntüleyin. Şekil 3 ' ün doğruladığında, yalnızca $25,00 ' den küçük veya buna eşit olan ürünleri görmeniz gerekir.

[![yalnızca $25,00 ' den küçük veya buna eşit olan ürünler görüntülenir](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.png)

**Şekil 3**: yalnızca $25,00 ' den küçük veya buna eşit olan ürünler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.png))

## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>2\. Adım: özel bir SQL Ifadesine parametre ekleme

Özel bir SQL deyimi eklerken, `WHERE` yan tümcesini açıkça girebilir veya Sorgu Tasarımcısı filtre hücresinde bir değer belirtebilirsiniz. Bunu göstermek için, yalnızca fiyatları belirli bir eşikten küçük olan bir GridView 'daki ürünleri görüntülemesine izin verin. `ParameterizedQueries.aspx` sayfasına, kullanıcıdan bu eşik değerini toplamak için bir TextBox ekleyerek başlayın. TextBox s `ID` özelliğini `MaxPrice`olarak ayarlayın. Bir düğme web denetimi ekleyin ve `Text` özelliğini eşleşen ürünleri görüntüleyecek şekilde ayarlayın.

Ardından, sayfaya bir GridView sürükleyip akıllı etiketinden `ProductsFilteredByPriceDataSource`adlı yeni bir SqlDataSource oluşturmayı seçin. Veri kaynağı Yapılandırma Sihirbazı ' ndan, özel bir SQL ekstresi veya saklı yordam belirtin ekranına ilerleyin (bkz. Şekil 4) ve aşağıdaki sorguyu girin:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample5.sql)]

Sorguyu girdikten sonra (el ile veya Sorgu Tasarımcısı), Ileri ' ye tıklayın.

[![yalnızca bir parametre değerine eşit veya daha küçük olan ürünleri döndürür](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.png)

**Şekil 4**: yalnızca bir parametre değerine eşit veya daha küçük olan ürünleri Döndür ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.png))

Sorgu parametreler içerdiğinden, sihirbazdaki bir sonraki ekranda parametre değerlerinin kaynağı için bizi uyarır. Doğrudan ControlID açılan listesinden parametre kaynağı açılır listesinden denetim ' i ve `MaxPrice` (TextBox denetim s `ID` değeri) seçin. Kullanıcının `MaxPrice` metin kutusuna metin girmemiş olması durumunda kullanılacak isteğe bağlı bir varsayılan değer de girebilirsiniz. Bu süre için varsayılan bir değer girmeyin.

[MaxPrice metin kutusu s Text özelliği parametre kaynağı olarak kullanılır ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.png)

**Şekil 5**: `MaxPrice` TextBox s `Text` özelliği parametre kaynağı olarak kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.png))

Ileri ' ye ve ardından son ' a tıklayarak veri kaynağı Yapılandırma Sihirbazı ' nı doldurun. GridView, TextBox, Button ve SqlDataSource için bildirim temelli biçimlendirme aşağıda verilmiştir:

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample6.aspx)]

SqlDataSource s `<SelectParameters>` bölümündeki parametrenin, `ControlID` ve `PropertyName`gibi ek özellikler içeren bir `ControlParameter`olduğunu unutmayın. SqlDataSource s `Select()` yöntemi çağrıldığında, `ControlParameter` belirtilen Web denetimi özelliğinden değeri dönüştürür ve `SelectCommand`karşılık gelen parametreye atar. Bu örnekte, `MaxPrice` s Text özelliği `@MaxPrice` parametresi değeri olarak kullanılır.

Bu sayfayı bir tarayıcı aracılığıyla görüntülemek için bir dakikanızı alın. İlk olarak sayfayı ziyaret ettiğinizde veya `MaxPrice` metin kutusu her seferinde GridView 'da hiçbir kayıt gösterilmez.

[MaxPrice metin kutusu boş olduğunda hiçbir kayıt gösterilmiyor ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.png)

**Şekil 6**: `MaxPrice` metin kutusu boş olduğunda hiçbir kayıt gösterilmez ([tam boyutlu görüntüyü görüntülemek için tıklatın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.png))

Hiçbir ürünün gösterilmediği nedeni, varsayılan olarak bir parametre değeri için boş bir dize bir veritabanı `NULL` değerine dönüştürülememektedir. `[UnitPrice] <= NULL` karşılaştırması her zaman yanlış olarak değerlendirildiğinden, hiçbir sonuç döndürülmez.

Metin kutusuna 5,00 gibi bir değer girin ve eşleşen ürünleri görüntüle düğmesine tıklayın. Geri göndermede, SqlDataSource GridView 'a parametre kaynaklarından birinin değiştiğini bildirir. Sonuç olarak, GridView, SqlDataSource 'a yeniden bağlanır ve bu ürünleri $5,00 ' den küçük veya buna eşit olarak görüntüler.

[$5,00 ' den küçük veya eşit ürünler ![görüntülenir](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.png)

**Şekil 7**: $5,00 ' den küçük veya buna eşit ürünler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.png))

## <a name="initially-displaying-all-products"></a>İlk olarak tüm ürünleri görüntüleme

Sayfa ilk yüklendiğinde hiçbir ürün görüntülenmesi yerine *Tüm* ürünleri görüntülemek isteyebilir. `MaxPrice` metin kutusu boş olduğunda tüm ürünleri listeetmenin bir yolu, Northwind Traders 'in birim fiyatı $1.000.000 ' i aşan envanterin olmadığı bir süre olduğundan, parametre varsayılan değerini 1000000 gibi bir inanılmaz derecede yüksek değere ayarlamaya yönelik bir yoldur. Ancak, bu yaklaşım çok fazla ve diğer durumlarda çalışmayabilir.

Önceki öğreticilerde [bildirim temelli parametrelerde](../basic-reporting/declarative-parameters-cs.md) ve [ana/ayrıntı filtrelemesinde](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) , benzer bir sorunla karşılaştık. Bu mantığı Iş mantığı katmanına koymak için çözümümüz vardı. Özellikle, gelen değeri inceledi ve `NULL` veya ayrılmış bir değer ise, çağrı tüm kayıtları döndüren DAL metoduna yönlendirilir. Gelen değer normal bir filtreleme değeri ise, sağlanan değerle parametreli `WHERE` yan tümcesini kullanan bir SQL deyimi yürüten DAL yöntemine bir çağrı yapıldı.

Ne yazık ki, SqlDataSource kullanılırken mimariyi atlıyoruz. Bunun yerine, `@MaximumPrice` parametresi `NULL` veya ayrılmış bir değer ise, SQL ifadesini tüm kayıtları bir bütün olarak almak için özelleştirmemiz gerekir. Bu alıştırma için, `@MaximumPrice` parametresi `-1.0`eşitse *Tüm* kayıtların döndürüldüğünden emin olun. (`-1.0`, bir ürünün negatif bir `UnitPrice` değeri olmadığından, ayrılmış bir değer olarak çalışacaktır). Bunu gerçekleştirmek için aşağıdaki SQL ifadesini kullanabiliriz:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample7.sql)]

Bu `WHERE` yan tümcesi, `@MaximumPrice` parametresi `-1.0`eşitse *Tüm* kayıtları döndürür. Parametre değeri `-1.0`değilse, yalnızca `UnitPrice` `@MaximumPrice` parametre değerine eşit veya daha küçük olan ürünler döndürülür. `@MaximumPrice` parametresinin varsayılan değerini `-1.0`, ilk sayfa yükünde (veya `MaxPrice` metin kutusu boş olduğunda) ayarlayarak, `@MaximumPrice` `-1.0` bir değere sahip olur ve tüm ürünler görüntülenir.

[![artık MaxPrice metin kutusu boş olduğunda tüm ürünler görüntülenir](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.png)

**Şekil 8**: artık `MaxPrice` metin kutusu boş olduğunda tüm ürünler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image16.png))

Bu yaklaşımda dikkat edilecek birkaç uyarılar vardır. İlk olarak, parametre s veri türünün SQL sorgusunda BT kullanımları tarafından çıkarsanacağını unutmayın. `WHERE` yan tümcesini `@MaximumPrice = -1.0` `@MaximumPrice = -1`olarak değiştirirseniz, çalışma zamanı parametreyi bir tamsayı olarak değerlendirir. Daha sonra `MaxPrice` metin kutusunu ondalık bir değere atamaya çalışırsanız (5,00 gibi), 5,00 ' i tamsayıya dönüştüremediği için bir hata oluşur. Bu sorunu gidermek için, `WHERE` yan tümcesinde `@MaximumPrice = -1.0` kullandığınızdan emin olun veya daha iyi `ControlParameter` nesne s `Type` özelliğini Decimal olarak ayarlayın.

İkinci olarak, `OR @MaximumPrice = -1.0` `WHERE` yan tümcesine ekleyerek sorgu altyapısı `UnitPrice` (var olan olduğunu varsayarak) bir dizin kullanamaz ve bu nedenle tablo taramasına neden olur. Bu, `Products` tablosunda yeterince çok sayıda kayıt varsa performansı etkileyebilir. Daha iyi bir yaklaşım, bu mantığı bir `IF` deyimi, tüm kayıtlar döndürüldüğünden veya `WHERE` yan tümcesi yalnızca `UnitPrice` ölçütü içeren bir `Products` `WHERE` tablosundan bir `SELECT` sorgusu (bir dizin kullanılabilmesi için) bir saklı yordama taşımak olacaktır.

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>3\. Adım: Parametreli saklı yordamlar oluşturma ve kullanma

Saklı yordamlar, saklı yordamda tanımlanan SQL deyimlerinin içinde kullanılabilecek bir giriş parametreleri kümesi içerebilir. SqlDataSource 'ı giriş parametrelerini kabul eden bir saklı yordam kullanacak şekilde yapılandırırken, bu parametre değerleri, geçici SQL deyimleriyle aynı teknikler kullanılarak belirtilebilir.

SqlDataSource 'daki saklı yordamları kullanmayı görmek için, `@CategoryID` adlı bir parametreyi kabul eden `GetProductsByCategory`adlı Northwind veritabanında yeni bir saklı yordam oluşturalım ve `CategoryID` sütunu `@CategoryID`ile eşleşen ürünlerin tüm sütunlarını döndürüyor. Saklı yordam oluşturmak için Sunucu Gezgini gidin ve `NORTHWND.MDF` veritabanının detayına gidin. (Sunucu Gezgini görmüyorsanız, Görünüm menüsüne gidip Sunucu Gezgini seçeneğini belirleyerek bunu getirin.)

`NORTHWND.MDF` veritabanından, saklı yordamlar klasörüne sağ tıklayın, yeni saklı yordam Ekle ' yi seçin ve aşağıdaki sözdizimini girin:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample8.sql)]

Saklı yordamı kaydetmek için kaydet simgesine (veya CTRL + S) tıklayın. Saklı yordamı, saklı yordamlar klasöründen sağ tıklayıp Yürüt ' ü seçerek test edebilirsiniz. Bu, sonuçları çıkış penceresinde görüntülenecek olan saklı yordam parametrelerini (Bu örnekte`@CategoryID`) ister.

[bir @CategoryID 1 ile yürütüldüğünde GetProductsByCategory saklı yordamını ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image17.png)

**Şekil 9**: bir `@CategoryID` 1 ile yürütüldüğünde `GetProductsByCategory` saklı yordam ([tam boyutlu görüntüyü görüntülemek için tıklatın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image18.png))

Bir GridView içindeki Içecek kategorisindeki tüm ürünleri göstermek için bu saklı yordamı kullanalım. Sayfaya yeni bir GridView ekleyin ve `BeverageProductsDataSource`adlı yeni bir SqlDataSource 'a bağlayın. Özel bir SQL ekstresi veya saklı yordam belirtme ekranına ilerleyin, saklı yordam radyo düğmesini seçin ve açılan listeden `GetProductsByCategory` saklı yordamını seçin.

[![açılan listeden GetProductsByCategory saklı yordamını seçin](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image19.png)

**Şekil 10**: açılan listeden `GetProductsByCategory` saklı yordamını seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image20.png))

Saklı yordam bir giriş parametresini (`@CategoryID`) kabul ettiğinden, Ileri ' ye tıklamak bu parametre değerinin kaynağını belirtmemizi ister. `CategoryID` Içecek 1 ' dir, bu nedenle parametre kaynağı açılır listesini None ' a bırakın ve DefaultValue metin kutusuna 1 girin.

[![Içecek kategorisindeki ürünleri döndürmek için sabit kodlanmış 1 değerini kullanın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image21.png)

**Şekil 11**: Içecek kategorisindeki ürünleri döndürmek Için sabit kodlanmış 1 değerini kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image22.png))

Aşağıdaki bildirim temelli biçimlendirme gösterdiği gibi, bir saklı yordam kullanılırken, SqlDataSource s `SelectCommand` özelliği saklı yordamın adına ayarlanır ve [`SelectCommandType` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx) `StoredProcedure`olarak ayarlanır. böylece, `SelectCommand`, bir ad-hoc SQL deyimi yerine bir saklı yordamın adı olduğunu gösterir.

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample9.aspx)]

Sayfayı bir tarayıcıda test edin. `GetProductsByCategory` saklı yordam `Products` tablosundan tüm sütunları döndürdüğünden, *Tüm* ürün alanları görüntülenmese de, yalnızca içecek kategorisine ait olan ürünler görüntülenir. GridView 'un sütunları Düzenle iletişim kutusundan GridView 'da görünen alanları sınırlayabiliriz.

[Tüm Içecek ![görüntülenir](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image23.png)

**Şekil 12**: tüm içecek görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image24.png))

## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>4\. Adım: program aracılığıyla bir SqlDataSource s`Select()`Ifadesini çağırma

Önceki öğreticide yaptığımız örnekler ve bu öğretici, SqlDataSource denetimlerini doğrudan bir GridView 'a bağladık. Ancak SqlDataSource denetim verileri, kod içinde programlı olarak erişilebilir ve Numaralandırılabilir. Bu özellikle, verileri incelemek için sorgulayıp onu görüntülemesi gerekmiyorsa yararlı olabilir. Veritabanına bağlanmak için tüm ortak ADO.NET kodunu yazmak yerine, komutunu belirtin ve sonuçları alın, SqlDataSource 'un bu monotonous kodunu işlemesini sağlayabilirsiniz.

Program aracılığıyla SqlDataSource s verileriyle çalışmayı göstermek için, bir kullanıcının rastgele seçilmiş bir kategorinin adını ve ilişkili ürünlerini görüntüleyen bir Web sayfası oluşturma isteğinde bulunduğunu düşünün approached. Diğer bir deyişle, bir Kullanıcı bu sayfayı ziyaret ettiğinde, `Categories` tablodan bir kategoriyi rastgele seçmek, kategori adını göstermek ve ardından bu kategoriye ait ürünleri listelemek istiyoruz.

Bunu gerçekleştirmek için, biri `Categories` tablosundan rastgele bir kategori almak üzere bir tane olmak üzere iki SqlDataSource denetimine gerek duyuyor ve kategorinin ürünlerini elde etmek için başka bir tane. Bu adımda rastgele bir kategori kaydı alan SqlDataSource oluşturacağız; 5. adım, kategori ürünleri ürünlerini alan SqlDataSource 'ın görünümünü yapar.

`ParameterizedQueries.aspx` bir SqlDataSource ekleyerek başlayın ve `ID` `RandomCategoryDataSource`olarak ayarlayın. Aşağıdaki SQL sorgusunu kullanacak şekilde yapılandırın:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample10.sql)]

`ORDER BY NEWID()`, rastgele sırada sıralanan kayıtları döndürür (bkz. [kayıtları rastgele sıralamak için `NEWID()` kullanma](http://www.sqlteam.com/item.asp?ItemID=8747)). `SELECT TOP 1`, sonuç kümesindeki ilk kaydı döndürür. Bir araya getirin, bu sorgu `CategoryID` ve `CategoryName` sütun değerlerini tek ve rastgele seçilmiş bir kategoriden döndürür.

Kategori `CategoryName` değerini göstermek için sayfaya bir etiket Web denetimi ekleyin, `ID` özelliğini `CategoryNameLabel`olarak ayarlayın ve `Text` özelliğini temizleyin. Verileri bir SqlDataSource denetiminden programlı bir şekilde almak için `Select()` yöntemini çağırdık. [`Select()` yöntemi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx) , verilerin döndürülmeden önce nasıl ileti alınacağını belirten [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)türünde tek bir giriş parametresi bekler. Bu, verileri sıralama ve filtreleme ile ilgili yönergeler içerebilir ve bir SqlDataSource denetiminden veri aracılığıyla sıralama veya sayfalama sırasında veri Web denetimleri tarafından kullanılır. Bizim örneğimizde, döndürülmeden önce değiştirilecek verilere ihtiyacım yoktur ve bu nedenle `DataSourceSelectArguments.Empty` nesnesine geçiş yapılır.

`Select()` yöntemi `IEnumerable`uygulayan bir nesne döndürür. Döndürülen kesin tür, SqlDataSource Control s [`DataSourceMode` özelliğinin](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)değerine bağlıdır. Önceki öğreticide anlatıldığı gibi bu özellik `DataSet` veya `DataReader`bir değere ayarlanabilir. `DataSet`olarak ayarlanırsa, `Select()` yöntemi bir [DataView](https://msdn.microsoft.com/library/01s96x0z.aspx) nesnesi döndürür; `DataReader`olarak ayarlanırsa, [`IDataReader`](https://msdn.microsoft.com/library/system.data.idatareader.aspx)uygulayan bir nesne döndürür. `RandomCategoryDataSource` SqlDataSource 'un `DataSourceMode` özelliği `DataSet` (varsayılan) olarak ayarlandığından, bir DataView nesnesiyle çalışacağız.

Aşağıdaki kod, `RandomCategoryDataSource` SqlDataSource 'daki kayıtların bir DataView olarak nasıl alınacağını ve ilk DataView satırından `CategoryName` Column değerinin nasıl okunacağını gösterir:

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample11.cs)]

`randomCategoryView[0]` DataView içindeki ilk `DataRowView` döndürür. `randomCategoryView[0]["CategoryName"]`, bu ilk satırdaki `CategoryName` sütununun değerini döndürür. DataView 'in gevşek olarak yazılmış olduğunu unutmayın. Belirli bir sütun değerine başvurmak için sütunun adını dize olarak geçirmemiz gerekir (Bu durumda CategoryName). Şekil 13, sayfayı görüntülerken `CategoryNameLabel` görüntülenen iletiyi gösterir. Tabii ki, görünen gerçek kategori adı sayfada her ziyaret edildiğinde (geri göndermeler dahil) `RandomCategoryDataSource` SqlDataSource tarafından rastgele seçilir.

[Rastgele seçilen kategorinin adı ![görüntülenir](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image25.png)

**Şekil 13**: rastgele seçilen kategori adı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image26.png))

> [!NOTE]
> SqlDataSource denetimi `DataSourceMode` özelliği `DataReader`olarak ayarlandıysa `Select()` yönteminden dönen değerin `IDataReader`'ye dönüştürülmesi gerekir. İlk satırdaki `CategoryName` sütun değerini okumak için, şunun gibi bir kod kullanacağız:

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample12.cs)]

Bir kategoriyi rasgele seçerek, kategori s ürünlerini listeleyen GridView 'u eklemeye hazırız.

> [!NOTE]
> Kategori adını göstermek için bir etiket Web denetimi kullanmak yerine, sayfaya bir FormView veya DetailsView eklemiş ve bunu SqlDataSource 'a bağlamamız gerekir. Ancak etiketini kullanarak, SqlDataSource s `Select()` ifadesini programlı bir şekilde çağırmayı ve koddaki sonuç verileriyle çalışmayı keşfetmemize izin verilir.

## <a name="step-5-assigning-parameter-values-programmatically"></a>5\. Adım: program aracılığıyla parametre değerlerini atama

Bu öğreticide şimdiye kadar görtiğimiz örneklerin hepsi, sabit kodlanmış bir parametre değeri veya önceden tanımlanmış parametre kaynaklarından birinden (bir QueryString değeri, sayfada bir Web denetimi vb.) alınmış bir değer kullandı. Ancak, SqlDataSource denetim parametreleri de programlı bir şekilde ayarlanabilir. Geçerli örneğimizi tamamlayabilmeniz için, belirtilen kategoriye ait tüm ürünleri döndüren bir SqlDataSource gerekir. Bu SqlDataSource, `Page_Load` olay işleyicisinde `RandomCategoryDataSource` SqlDataSource tarafından döndürülen `CategoryID` sütun değerine göre ayarlanması gereken `CategoryID` bir parametreye sahip olacaktır.

Sayfaya bir GridView ekleyerek başlayın ve `ProductsByCategoryDataSource`adlı yeni bir SqlDataSource 'a bağlayın. Adım 3 ' te yaptığımız gibi, SqlDataSource öğesini `GetProductsByCategory` saklı yordamını sağlayacak şekilde yapılandırın. Parametre kaynağı açılır listesini hiçbiri olarak ayarlayın, ancak varsayılan değeri program aracılığıyla ayarlayacağız.

[![bir parametre kaynağı veya varsayılan değer belirtmeyin](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image27.png)

**Şekil 14**: parametre kaynağı veya varsayılan değer belirtmeyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image28.png))

SqlDataSource Sihirbazı 'nı tamamladıktan sonra, ortaya çıkan açıklayıcı biçimlendirme aşağıdakine benzer şekilde görünmelidir:

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample13.aspx)]

`CategoryID` parametresinin `DefaultValue` programlı olarak `Page_Load` olay işleyicisine atayabiliriz:

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample14.cs)]

Bu ek olarak, sayfa rastgele seçilmiş kategori ile ilişkili ürünleri gösteren bir GridView içerir.

[![bir parametre kaynağı veya varsayılan değer belirtmeyin](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image29.png)

**Şekil 15**: parametre kaynağı veya varsayılan değer belirtmeyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-parameterized-queries-with-the-sqldatasource-cs/_static/image30.png))

## <a name="summary"></a>Özet

SqlDataSource, sayfa geliştiricilerinin parametre değerleri sabit kodlamalı, önceden tanımlanmış parametre kaynaklarından çekilir veya programlı olarak atanabileceği parametreli sorgular tanımlamasına olanak sağlar. Bu öğreticide, hem geçici SQL sorguları hem de saklı yordamlar için veri kaynağını yapılandırma sihirbazından parametreli bir sorgu oluşturmayı gördük. Ayrıca, sabit kodlanmış parametre kaynaklarını, bir Web denetimini parametre kaynağı olarak kullanmayı ve parametre değerini programlı olarak belirtmeyi de inceledik.

ObjectDataSource gibi, SqlDataSource de temel alınan verileri değiştirmek için yetenekler sağlar. Bir sonraki öğreticide, SqlDataSource ile `INSERT`, `UPDATE`ve `DELETE` deyimlerini tanımlama bölümüne bakacağız. Bu deyimler eklendikten sonra GridView, DetailsView ve FormView denetimlerine ait olan yerleşik ekleme, düzenlemek ve silinen özellikleri kullanabilirsiniz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide müşteri adayı gözden geçirenler Scott Clyıde, Randell SCHMIDT ve Ken ön PISA. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](querying-data-with-the-sqldatasource-control-cs.md)
> [İleri](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)
