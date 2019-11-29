---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
title: TableAdapter 'ı birleştirmeleri kullanacak şekilde güncelleştirme (VB) | Microsoft Docs
author: rick-anderson
description: Bir veritabanıyla çalışırken, birden çok tabloya yayılan veriler istemek yaygındır. İki farklı tablodan veri almak için, her birini kullanabiliriz...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: e624a3e0-061b-4efc-8b0e-5877f9ff6714
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c94baa99b126cdd24d69afc3d02bfe8b069419b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74604180"
---
# <a name="updating-the-tableadapter-to-use-joins-vb"></a>TableAdapter’ı JOIN Kullanacak Biçimde Güncelleştirme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_VB.zip) veya [PDF 'yi indirin](updating-the-tableadapter-to-use-joins-vb/_static/datatutorial69vb1.pdf)

> Bir veritabanıyla çalışırken, birden çok tabloya yayılan veriler istemek yaygındır. İki farklı tablodan verileri almak için bağıntılı bir alt sorgu veya bir JOIN işlemi kullanabilirsiniz. Bu öğreticide, ana sorgusunda JOIN içeren bir TableAdapter oluşturmayı aramadan önce bağıntılı alt sorguları ve JOIN sözdizimini karşılaştırıyoruz.

## <a name="introduction"></a>Giriş

İlişkisel veritabanlarında, çalışma konusunda ilgilendiğiniz veriler genellikle birden çok tablo arasında yayılır. Örneğin, ürün bilgilerini görüntülerken her bir ürüne karşılık gelen her bir kategori ve sağlayıcı adını listelemek istiyoruz. `Products` tabloda `CategoryID` ve `SupplierID` değerleri bulunur, ancak gerçek kategori ve tedarikçi adları sırasıyla `Categories` ve `Suppliers` tablolarında bulunur.

Başka bir ilişkili tablodan bilgi almak için, *bağıntılı alt sorgular* veya `JOIN`*s*kullanabilirsiniz. Bağıntılı alt sorgu, dış sorgudaki sütunlara başvuran iç içe bir `SELECT` sorgusudur. Örneğin, [veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-vb.md) öğreticisinde, her ürün için kategori ve Tedarikçi adlarını döndürmek üzere `ProductsTableAdapter` s ana sorgusunda iki bağıntılı alt sorgu kullandık. `JOIN`, iki farklı tablodan ilgili satırları birleştiren bir SQL yapısıdır. Her ürünle birlikte kategori bilgilerini göstermek için [SqlDataSource denetim öğreticisi Ile verileri sorgulama](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb.md) `JOIN` kullandık.

`JOIN` s 'yi TableAdapters ile kullanmanın yanı sıra, ilişkili `INSERT`, `UPDATE`ve `DELETE` deyimlerini otomatik olarak oluşturmak için TableAdapter s sihirbazının sınırlamalarından kaynaklanır. Daha belirgin bir şekilde, TableAdapter s ana sorgusu herhangi bir `JOIN` s içeriyorsa, TableAdapter `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özellikleri için geçici SQL deyimlerini veya saklı yordamları otomatik olarak oluşturamaz.

Bu öğreticide, ana sorgusunda `JOIN` s 'yi içeren bir TableAdapter oluşturmayı keşfetmeye başlamadan önce bağıntılı alt sorguları ve `JOIN` s 'leri daha fazla karşılaştıracağız.

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>Bağıntılı alt sorgular ve`JOIN` s karşılaştırması ve karşıt

`Northwind` veri kümesindeki ilk öğreticide oluşturulan `ProductsTableAdapter`, her bir ürüne karşılık gelen her bir kategoriyi ve tedarikçi adını geri getirmek için bağıntılı alt sorguları kullandığını hatırlayın. `ProductsTableAdapter` s ana sorgusu aşağıda gösterilmiştir.

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample1.sql)]

İki bağıntılı alt sorgu-`(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)` ve `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)`-, dış `SELECT` deyimlerinin sütun listesinde ek bir sütun olarak her ürün için tek bir değer döndüren `SELECT` sorgulardır.

Alternatif olarak, bir `JOIN` her ürün tedarikçisine ve kategori adına döndürmek için de kullanılabilir. Aşağıdaki sorgu yukarıdaki ile aynı çıktıyı döndürür, ancak alt sorgular yerine `JOIN` s kullanır:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample2.sql)]

`JOIN`, bir tablodaki kayıtları, bazı ölçütlere göre başka bir tablodaki kayıtlarla birleştirir. Yukarıdaki sorguda, örneğin, `LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID` her ürün kaydını `CategoryID` değeri ürün s `CategoryID` değeri ile eşleşen kategori kaydıyla birleştirmeye SQL Server söyler. Birleştirilmiş sonuç, her ürün için karşılık gelen kategori alanlarıyla (`CategoryName`) çalışmamızı sağlar.

> [!NOTE]
> `JOIN` s 'ler, ilişkisel veritabanlarından veri sorgulanırken yaygın olarak kullanılır. `JOIN` söz dizimine yeni bir bit kullanıyorsanız veya kullanımı için bir bit kullanmanız gerekiyorsa, [w3 okullarından](http://www.w3schools.com/) [SQL JOIN öğreticisini](http://www.w3schools.com/sql/sql_join.asp) önerdim. Ayrıca, [SQL Books Online](https://msdn.microsoft.com/library/ms130214.aspx)'ın [`JOIN` temel bilgiler](https://msdn.microsoft.com/library/ms191517.aspx) ve [alt sorgu temelleri](https://msdn.microsoft.com/library/ms189575.aspx) bölümleri de okunuyor.

`JOIN` s ve bağıntılı alt sorgular her ikisi de diğer tablolardan ilgili verileri almak için kullanıldığından, birçok geliştirici kafa çekmesini ve hangi yaklaşımın kullanılacağını merak ediyor. En çok kabaca aynı şeyi söylediği için, daha önce sundum olan tüm SQL Gurus 'ları, SQL Server kabaca özdeş yürütme planları üretecektir. Bu durumda, sizin ve takımınızın en rahat olduğu tekniğin kullanılması önerilir. Bu uzmanlardan sonra bu uzmanlar, bağıntılı alt sorgular üzerinde `JOIN` s tercihini hemen ifade ettikten sonra ele aldığını belirtir.

Yazılan veri kümelerini kullanarak bir veri erişim katmanı oluştururken araçlar, alt sorgular kullanılırken daha iyi çalışır. Özellikle, TableAdapter s Sihirbazı, ana sorgu herhangi bir `JOIN` s içeriyorsa karşılık gelen `INSERT`, `UPDATE`ve `DELETE` deyimlerini otomatik olarak oluşturmaz, ancak bağıntılı alt sorgular kullanıldığında bu deyimleri otomatik olarak oluşturur.

Bu eksiklikleri araştırmak için `~/App_Code/DAL` klasöründe geçici olarak yazılmış bir veri kümesi oluşturun. TableAdapter Yapılandırma Sihirbazı sırasında, geçici SQL deyimlerini kullanmayı seçin ve aşağıdaki `SELECT` sorguyu girin (bkz. Şekil 1):

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample3.sql)]

[![birleşimler Içeren bir ana sorgu girin](updating-the-tableadapter-to-use-joins-vb/_static/image2.png)](updating-the-tableadapter-to-use-joins-vb/_static/image1.png)

**Şekil 1**: `JOIN` s Içeren bir ana sorgu girin ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image3.png))

Varsayılan olarak TableAdapter, ana sorguya göre otomatik olarak `INSERT`, `UPDATE`ve `DELETE` deyimlerini oluşturacaktır. Gelişmiş düğmesine tıklarsanız, bu özelliğin etkin olduğunu görebilirsiniz. Bu ayara rağmen, ana sorgu bir `JOIN`içerdiğinden TableAdapter `INSERT`, `UPDATE`ve `DELETE` deyimlerini oluşturamayacak.

![Birleşimler Içeren bir ana sorgu girin](updating-the-tableadapter-to-use-joins-vb/_static/image4.png)

**Şekil 2**: `JOIN` s Içeren bir ana sorgu girin

Sihirbazı tamamladığınızda son ' a tıklayın. Bu noktada, DataSet s Designer, `SELECT` Query s sütun listesinde döndürülen her bir alan için sütun içeren bir DataTable içeren tek bir TableAdapter içerir. Bu, Şekil 3 ' ün gösterdiği gibi `CategoryName` ve `SupplierName`içerir.

![DataTable, sütun listesinde döndürülen her alan için bir sütun Içerir](updating-the-tableadapter-to-use-joins-vb/_static/image5.png)

**Şekil 3**: DataTable, sütun listesinde döndürülen her alan Için bir sütun içerir

DataTable uygun sütunlara sahip olsa da TableAdapter `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özellikleri için değerler eksiktir. Bunu onaylamak için, tasarımcıda TableAdapter 'a tıklayın ve ardından Özellikler penceresi gidin. `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özelliklerinin (None) olarak ayarlandığını görürsünüz.

[InsertCommand, UpdateCommand ve DeleteCommand özellikleri ![(yok) olarak ayarlanır](updating-the-tableadapter-to-use-joins-vb/_static/image7.png)](updating-the-tableadapter-to-use-joins-vb/_static/image6.png)

**Şekil 4**: `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özellikleri (yok) olarak ayarlanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image8.png))

Bu eksiklikleri geçici olarak çözmek için, Özellikler penceresi aracılığıyla `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özelliklerinin SQL deyimlerini ve parametrelerini el ile sağlayabiliriz. Alternatif olarak, TableAdapter s ana sorgusunu hiçbir `JOIN` *s 'yi içerecek* şekilde yapılandırarak başlayabiliriz. Bu, `INSERT`, `UPDATE`ve `DELETE` deyimlerinin ABD için otomatik olarak oluşturulmasını sağlar. Sihirbazı tamamladıktan sonra, `JOIN` sözdizimini içermesi için TableAdapter s `SelectCommand` Özellikler penceresi el ile güncelleştirebilirsiniz.

Bu yaklaşım çalışırken, TableAdapter s ana sorgusunun sihirbaz aracılığıyla yeniden yapılandırıldığı, otomatik olarak oluşturulan `INSERT`, `UPDATE`ve `DELETE` deyimlerinin yeniden oluşturulduğu her seferinde geçici SQL sorguları kullanılırken çok Brittle. Diğer bir deyişle, TableAdapter 'a sağ tıklıyoruz, bağlam menüsünden Yapılandır ' ı seçip Sihirbazı yeniden tamamladıktan sonra, daha sonra yaptığımız tüm özelleştirmeler kaybedilir.

TableAdapter s otomatik olarak oluşturulan `INSERT`, `UPDATE`ve `DELETE` deyimlerinin britttayeti, neyse ki geçici SQL deyimleriyle sınırlıdır. TableAdapter saklı yordamlar kullanıyorsa, `SelectCommand`, `InsertCommand`, `UpdateCommand`veya `DeleteCommand` saklı yordamları özelleştirebilir ve, saklı yordamların değiştirilmesini sağlamak zorunda kalmadan TableAdapter Yapılandırma Sihirbazı 'nı yeniden çalıştırabilirsiniz.

Sonraki birkaç adımda, başlangıçta, ilgili INSERT, Update ve delete saklı yordamlarının otomatik olarak üretilebilmesi için `JOIN` s 'yi atlayacak bir ana sorgu kullanan bir TableAdapter oluşturacağız. Daha sonra, ilgili tablolardan ek sütunları döndüren bir `JOIN` kullanması için `SelectCommand` güncelleştireceğiz. Son olarak, karşılık gelen bir Iş mantığı katman sınıfı oluşturacağız ve TableAdapter 'ı bir ASP.NET Web sayfasında kullanmayı gösteririz.

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>1\. Adım: Basitleştirilmiş ana sorgu kullanarak TableAdapter oluşturma

Bu öğreticide, `NorthwindWithSprocs` veri kümesindeki `Employees` tablo için bir TableAdapter ve kesin olarak yazılmış bir DataTable ekleyeceğiz. `Employees` tablosu, çalışan s Manager 'ın `EmployeeID` belirtilen bir `ReportsTo` alanı içerir. Örneğin, çalışan Anne Dodsworth 'un, Steven Uludağ 'ın `EmployeeID` `ReportTo` değeri 5 ' tir. Sonuç olarak, Anne, Steven ve yöneticisini raporlar. Her çalışan `ReportsTo` değerini raporlamaya birlikte, yönetici adlarını da almak da isteyebilirsiniz. Bu, bir `JOIN`kullanılarak gerçekleştirilebilir. Ancak, ilk olarak TableAdapter oluştururken bir `JOIN` kullanmak, sihirbazın ilgili ekleme, güncelleştirme ve silme yeteneklerini otomatik olarak oluşturmasını da ister. Bu nedenle, ana sorgusu hiç `JOIN` s içermeyen bir TableAdapter oluşturarak başlayacağız. Ardından, adım 2 ' de, yönetici adını bir `JOIN`aracılığıyla almak için ana sorgu saklı yordamını güncelleştireceğiz.

`~/App_Code/DAL` klasöründe `NorthwindWithSprocs` veri kümesini açarak başlayın. Tasarımcıya sağ tıklayın, bağlam menüsünden Ekle seçeneğini belirleyin ve TableAdapter menü öğesini seçin. Bu, TableAdapter Yapılandırma Sihirbazı 'nı başlatır. Şekil 5 ' te gösterildiği gibi, sihirbazın yeni saklı yordamlar oluşturmasını ve Ileri ' ye tıkladığını gösterir. TableAdapter s sihirbazından yeni saklı yordamlar oluşturmaya yönelik Yenileyici için, [yazılan veri kümesi s TableAdapters öğreticisi Için yeni saklı yordamlar oluşturma](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) bölümüne bakın.

[![yeni saklı yordamlar oluştur seçeneğini belirleyin](updating-the-tableadapter-to-use-joins-vb/_static/image10.png)](updating-the-tableadapter-to-use-joins-vb/_static/image9.png)

**Şekil 5**: Yeni saklı yordamlar oluştur seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image11.png))

TableAdapter s ana sorgusu için aşağıdaki `SELECT` ifadesini kullanın:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample4.sql)]

Bu sorgu hiçbir `JOIN` s içermediğinden, TableAdapter Sihirbazı ilgili `INSERT`, `UPDATE`ve `DELETE` deyimleriyle otomatik olarak saklı yordamlar oluşturacak ve ana sorguyu yürütmek için bir saklı yordam oluşturacaktır.

Aşağıdaki adım, TableAdapter saklı yordamlarını ad etmemizi sağlar. Şekil 6 ' da gösterildiği gibi `Employees_Select`, `Employees_Insert`, `Employees_Update`ve `Employees_Delete`adlarını kullanın.

[![TableAdapter saklı yordamlarını adlandırın](updating-the-tableadapter-to-use-joins-vb/_static/image13.png)](updating-the-tableadapter-to-use-joins-vb/_static/image12.png)

**Şekil 6**: TableAdapter s saklı yordamlarını adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image14.png))

Son adım, TableAdapter s yöntemlerini adı etmemizi ister. Yöntem adları olarak `Fill` ve `GetEmployees` kullanın. Ayrıca, güncelleştirmeleri doğrudan veritabanına göndermek için oluşturma yöntemlerini de bırakın (GenerateDBDirectMethods) onay kutusunun işaretli olduğundan emin olun.

[TableAdapter s yöntemlerinin Fill ve GetEmployees adına ![adı](updating-the-tableadapter-to-use-joins-vb/_static/image16.png)](updating-the-tableadapter-to-use-joins-vb/_static/image15.png)

**Şekil 7**: TableAdapter s metotlarını `Fill` ve `GetEmployees` adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image17.png))

Sihirbazı tamamladıktan sonra, veritabanında saklı yordamları incelemek için bir dakikanızı ayırın. Dört yeni tane görmeniz gerekir: `Employees_Select`, `Employees_Insert`, `Employees_Update`ve `Employees_Delete`. Sonra, `EmployeesDataTable` ve yeni oluşturulan `EmployeesTableAdapter` inceleyin. DataTable, ana sorgu tarafından döndürülen her alan için bir sütun içerir. TableAdapter ' a tıklayın ve ardından Özellikler penceresi gidin. `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özelliklerinin ilgili saklı yordamları çağırmak üzere doğru şekilde yapılandırıldığını görürsünüz.

[TableAdapter ![INSERT, Update ve DELETE özelliklerini Içerir](updating-the-tableadapter-to-use-joins-vb/_static/image19.png)](updating-the-tableadapter-to-use-joins-vb/_static/image18.png)

**Şekil 8**: TableAdapter INSERT, Update ve DELETE özelliklerini içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image20.png))

Ekleme, güncelleştirme ve silme saklı yordamları otomatik olarak oluşturulur ve `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özellikleri doğru şekilde yapılandırıldıysa, her çalışan Yöneticisi hakkında ek bilgi döndürmek için `SelectCommand` s saklı yordamını özelleştirmeye hazırız. Özellikle, bir `JOIN` kullanmak ve Manager s `FirstName` ve `LastName` değerlerini döndürmek için `Employees_Select` saklı yordamını güncelleştirmemiz gerekir. Saklı yordam güncelleştirildikten sonra DataTable 'ı bu ek sütunları içerecek şekilde güncelleştirmemiz gerekir. 2 ve 3. adımlarda bu iki görevi ele alacağız.

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>2\. Adım: saklı yordamı bir`JOIN` Içerecek şekilde özelleştirme

Sunucu Gezgini giderek başlayın, Northwind veritabanı s saklı yordamları klasörünün detayına gidin ve `Employees_Select` saklı yordamını açın. Bu saklı yordamı görmüyorsanız, saklı yordamlar klasörüne sağ tıklayın ve Yenile ' yi seçin. Saklı yordamı, yöneticinin ilk ve son adını döndürmek için bir `LEFT JOIN` kullanacak şekilde güncelleştirin:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample5.sql)]

`SELECT` ifadesini güncelleştirdikten sonra, Dosya menüsüne gidip kaydet `Employees_Select`' i seçerek değişiklikleri kaydedin. Alternatif olarak, araç çubuğundaki Kaydet simgesine tıklayabilir veya CTRL + S ' ye basabilirsiniz. Değişikliklerinizi kaydettikten sonra, Sunucu Gezgini `Employees_Select` saklı yordamına sağ tıklayın ve Yürüt ' ü seçin. Bu işlem, saklı yordamı çalıştırır ve sonuçlarını çıkış penceresinde gösterir (bkz. Şekil 9).

[![saklı yordam sonuçları Çıkış Penceresi görüntülenir](updating-the-tableadapter-to-use-joins-vb/_static/image22.png)](updating-the-tableadapter-to-use-joins-vb/_static/image21.png)

**Şekil 9**: saklı yordam sonuçları çıkış penceresi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image23.png))

## <a name="step-3-updating-the-datatable-s-columns"></a>3\. Adım: DataTable s sütunlarını güncelleştirme

Bu noktada, `Employees_Select` saklı yordamı `ManagerFirstName` ve `ManagerLastName` değerler döndürür, ancak `EmployeesDataTable` bu sütunlar eksik. Bu eksik sütunlar DataTable 'a iki şekilde eklenebilir:

- Veri kümesi tasarımcısında DataTable üzerinde **el ile** sağ tıklayın ve Ekle menüsünde sütun ' u seçin. Daha sonra sütunu verebilir ve özelliklerini uygun şekilde ayarlayabilirsiniz.
- **Otomatik olarak** -TableAdapter Yapılandırma Sihirbazı, DataTable s sütunlarını `SelectCommand` saklı yordamının döndürdüğü alanları yansıtacak şekilde güncelleştirir. Geçici SQL deyimlerini kullanırken, `SelectCommand` artık bir `JOIN`içerdiğinden, sihirbaz `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özelliklerini de kaldırır. Ancak saklı yordamlar kullanılırken bu komut özellikleri değişmeden kalır.

Bir ayrıntılar DataList ve [dosya karşıya yükleme](../working-with-binary-files/uploading-files-vb.md) [Içeren bir ana kayıt listesi listesini kullanarak ana/ayrıntı](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) dahil olmak üzere önceki öğreticilere DataTable sütunlarını el ile eklemeyi araştırdık. bu işleme sonraki öğreticimizde daha ayrıntılı bir şekilde bakacağız. Bununla birlikte, bu öğretici için TableAdapter Yapılandırma Sihirbazı aracılığıyla otomatik yaklaşımı kullanalım.

`EmployeesTableAdapter` sağ tıklayıp bağlam menüsünden Yapılandır ' ı seçerek başlayın. Bu, seçme, ekleme, güncelleştirme ve silme için kullanılan saklı yordamları, dönüş değerleri ve parametreleriyle birlikte (varsa) listeleyen TableAdapter Yapılandırma Sihirbazı 'nı getirir. Şekil 10 Bu Sihirbazı gösterir. Burada `Employees_Select` saklı yordamının artık `ManagerFirstName` ve `ManagerLastName` alanlarını döndürdüğünü görebiliriz.

[![sihirbaz Employees_Select saklı yordamının güncelleştirilmiş sütun listesini gösterir](updating-the-tableadapter-to-use-joins-vb/_static/image25.png)](updating-the-tableadapter-to-use-joins-vb/_static/image24.png)

**Şekil 10**: sihirbaz `Employees_Select` saklı yordamının güncelleştirilmiş sütun listesini gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image26.png))

Son ' a tıklayarak Sihirbazı doldurun. Veri kümesi tasarımcısına dönmesinden sonra, `EmployeesDataTable` iki ek sütun içerir: `ManagerFirstName` ve `ManagerLastName`.

[EmployeesDataTable ![Iki yeni sütun Içerir](updating-the-tableadapter-to-use-joins-vb/_static/image28.png)](updating-the-tableadapter-to-use-joins-vb/_static/image27.png)

**Şekil 11**: `EmployeesDataTable` Iki yeni sütun içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image29.png))

Güncelleştirilmiş `Employees_Select` saklı yordamının geçerli olduğunu ve TableAdapter 'ın INSERT, Update ve DELETE özelliklerini hala işlevsel olduğunu anlamak için, kullanıcıların çalışanları görüntülemesine ve silmesine izin veren bir Web sayfası oluşturmasına izin verin. Bununla birlikte, böyle bir sayfa oluşturmadan önce, `NorthwindWithSprocs` veri kümesindeki çalışanlarla çalışmak üzere Iş mantığı katmanında yeni bir sınıf oluşturmanız gerekir. 4\. adımda bir `EmployeesBLLWithSprocs` sınıfı oluşturacağız. 5\. adımda bu sınıfı bir ASP.NET sayfasından kullanacağız.

## <a name="step-4-implementing-the-business-logic-layer"></a>4\. Adım: Iş mantığı katmanını uygulama

`EmployeesBLLWithSprocs.vb`adlı `~/App_Code/BLL` klasörde yeni bir sınıf dosyası oluşturun. Bu sınıf, var olan `EmployeesBLL` sınıfının semantiğini taklit eder, yalnızca bu yeni bir tane daha az yöntem sağlar ve `NorthwindWithSprocs` veri kümesini kullanır (`Northwind` veri kümesi yerine). Aşağıdaki kodu `EmployeesBLLWithSprocs` sınıfına ekleyin.

[!code-vb[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample6.vb)]

`EmployeesBLLWithSprocs` sınıf s `Adapter` özelliği `NorthwindWithSprocs` veri `EmployeesTableAdapter`kümesinin bir örneğini döndürür. Bu, sınıf s `GetEmployees` ve `DeleteEmployee` yöntemleri tarafından kullanılır. `GetEmployees` yöntemi, `Employees_Select` saklı yordamını çağıran ve sonuçlarını bir `EmployeeDataTable`dolduran `EmployeesTableAdapter` s karşılık gelen `GetEmployees` yöntemini çağırır. `DeleteEmployee` yöntemi benzer şekilde `Employees_Delete` saklı yordamını çağıran `EmployeesTableAdapter` s `Delete` yöntemini çağırır.

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>5\. Adım: sunu katmanındaki verilerle çalışma

`EmployeesBLLWithSprocs` sınıfı tamamlandıktan sonra, ASP.NET sayfası aracılığıyla çalışan verileriyle çalışmaya hazırız. `AdvancedDAL` klasöründeki `JOINs.aspx` sayfasını açın ve araç kutusu 'ndaki bir GridView 'u `ID` özelliğini `Employees`olarak ayarlayarak tasarımcı üzerine sürükleyin. Ardından, GridView s akıllı etiketinden, Kılavuzu `EmployeesDataSource`adlı yeni bir ObjectDataSource denetimine bağlayın.

ObjectDataSource 'u `EmployeesBLLWithSprocs` sınıfını kullanacak şekilde yapılandırın ve SEÇIM ve SILME sekmelerinden, `GetEmployees` ve `DeleteEmployee` yöntemlerinin açılan listelerden seçildiğinden emin olun. ObjectDataSource 'un yapılandırmasını gerçekleştirmek için son ' a tıklayın.

[![, bir EmployeesBLLWithSprocs sınıfını kullanacak şekilde yapılandırma](updating-the-tableadapter-to-use-joins-vb/_static/image31.png)](updating-the-tableadapter-to-use-joins-vb/_static/image30.png)

**Şekil 12**: `EmployeesBLLWithSprocs` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image32.png))

[![ObjectDataSource, GetEmployees ve DeleteEmployee yöntemlerini kullanır](updating-the-tableadapter-to-use-joins-vb/_static/image34.png)](updating-the-tableadapter-to-use-joins-vb/_static/image33.png)

**Şekil 13**: ObjectDataSource 'un `GetEmployees` ve `DeleteEmployee` yöntemlerini kullanmasını[sağlar (tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image35.png))

Visual Studio, `EmployeesDataTable` s sütunlarının her biri için GridView 'a bir BoundField ekler. `Title`, `LastName`, `FirstName`, `ManagerFirstName`ve `ManagerLastName` dışındaki tüm bu BoundFields alanlarını kaldırın ve son dört BoundFields `HeaderText` özelliklerini sırasıyla soyadı, Ilk adı, yönetici adı ve yönetici soyadı olarak yeniden adlandırın.

Kullanıcıların bu sayfadan çalışanları silmesine izin vermek için iki şey yapmanız gerekir. İlk olarak, GridView 'a akıllı etiketinden silmeyi etkinleştir seçeneğini işaretleyerek, silme özelliği sağlamayı söyleyin. İkincisi, ObjectDataSource 'un `OldValuesParameterFormatString` özelliğini, ObjectDataSource Sihirbazı (`original_{0}`) tarafından ayarlanan değerden varsayılan değer (`{0}`) olarak değiştirin. Bu değişiklikleri yaptıktan sonra, GridView ve ObjectDataSource 'un bildirim temelli biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample7.aspx)]

Sayfayı bir tarayıcı aracılığıyla ziyaret ederek test edin. Şekil 14 ' te gösterildiği gibi, sayfada her bir çalışan ve onun yönetici adı (bir tane olduğu varsayılarak) listelenir.

[Employees_Select saklı yordamında KATıLMAYı ![, yöneticinin adını döndürür](updating-the-tableadapter-to-use-joins-vb/_static/image37.png)](updating-the-tableadapter-to-use-joins-vb/_static/image36.png)

**Şekil 14**: `Employees_Select` saklı yordamındaki `JOIN`, yönetici adını ([tam boyutlu görüntüyü görüntülemek Için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image38.png)) döndürür

Sil düğmesine tıklamak, `Employees_Delete` saklı yordamının yürütülmesinde yürütülen iş akışını silme işlemini başlatır. Ancak, bir yabancı anahtar kısıtlaması ihlali nedeniyle saklı yordamdaki denenen `DELETE` deyimleri başarısız olur (bkz. Şekil 15). Özellikle, her çalışanın `Orders` tablodaki bir veya daha fazla kaydı vardır ve bu da silmenin başarısız olmasına neden olur.

[Karşılık gelen siparişlerin bulunduğu bir çalışanın silinmesi ![yabancı anahtar kısıtlaması Ihlaline neden olur](updating-the-tableadapter-to-use-joins-vb/_static/image40.png)](updating-the-tableadapter-to-use-joins-vb/_static/image39.png)

**Şekil 15**: karşılık gelen siparişleri olan bir çalışanın silinmesi yabancı anahtar kısıtlaması ihlaline neden olur ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-the-tableadapter-to-use-joins-vb/_static/image41.png))

Bir çalışanın silinmesine izin vermek için şunları yapabilirsiniz:

- Yabancı anahtar kısıtlamasını Cascade silmeleri olarak güncelleştir,
- Silmek istediğiniz çalışanların `Orders` tablosundan kayıtları el ile silin veya
- `Employees` kaydını silmeden önce `Orders` tablosundan ilgili kayıtları silmek için `Employees_Delete` saklı yordamını güncelleştirin. Bu tekniği, [yazılan veri kümesi s TableAdapters öğreticisi Için mevcut saklı yordamları kullanma konusunda](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) ele aldık.

Bunu okuyucu için bir alıştırma olarak bırakıyorum.

## <a name="summary"></a>Özet

İlişkisel veritabanları ile çalışırken, sorguların verileri birden çok, ilişkili tablodan çekmesini yaygındır. Bağıntılı alt sorgular ve `JOIN` s bir sorgudaki ilgili tablolardan verilere erişmek için iki farklı teknik sağlar. Önceki öğreticilerde, TableAdapter `JOIN` s içeren sorgular için `INSERT`, `UPDATE`ve `DELETE` deyimlerini otomatik olarak üretireceğiz için bağıntılı alt sorguları en yaygın olarak kullandık. Bu değerler el ile sağlanırken, TableAdapter Yapılandırma Sihirbazı tamamlandığında, geçici SQL deyimleri kullanılırken tüm özelleştirmeler üzerine yazılır.

Neyse ki, saklı yordamlar kullanılarak oluşturulan TableAdapters, ad-hoc SQL deyimleriyle oluşturulan aynı briı ile karşılaşmaz. Bu nedenle, ana sorgusu saklı yordamları kullanırken `JOIN` kullanan bir TableAdapter oluşturmak uygulanabilir. Bu öğreticide, böyle bir TableAdapter oluşturmayı nasıl oluşturacağınız gördük. İlişkili ekleme, güncelleştirme ve silme saklı yordamlarının otomatik olarak oluşturulması için TableAdapter s ana sorgusu için `JOIN`seyrek `SELECT` bir sorgu kullanarak başladık. TableAdapter 'ın ilk yapılandırması tamamlandıktan sonra, bir `JOIN` kullanmak ve `EmployeesDataTable` s sütunlarını güncelleştirmek için TableAdapter Yapılandırma Sihirbazı 'nı yeniden çalıştırdık `SelectCommand` saklı yordamını genişlettik.

TableAdapter Yapılandırma Sihirbazı 'nı yeniden çalıştırmak, `EmployeesDataTable` sütunlarını `Employees_Select` saklı yordamının döndürdüğü veri alanlarını yansıtacak şekilde otomatik olarak güncelleştirirler. Alternatif olarak, bu sütunları DataTable 'a el ile de ekledik. Sonraki öğreticide DataTable 'a el ile sütun ekleme hakkında araştıracağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Kiton Geisenow, David suru ve TeReSaN Murphy. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [İleri](adding-additional-datatable-columns-vb.md)
