---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
title: Türü belirtilmiş DataSet 'in TableAdapters (C#) Için mevcut saklı yordamları kullanma | Microsoft Docs
author: rick-anderson
description: Önceki öğreticide, yeni saklı yordamlar oluşturmak için TableAdapter Sihirbazı 'Nı nasıl kullanacağınızı öğrendiniz. Bu öğreticide aynı TableAdapter 'ın nasıl olduğunu öğreniyoruz...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 440bef2a-1641-4238-99e3-8e2d44e7d94c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
msc.type: authoredcontent
ms.openlocfilehash: cfe03c244fb6f9f0a201aecb6eae211ab946175f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74604124"
---
# <a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-c"></a>Türü Belirtilmiş DataSet'in TableAdapter’ları için Mevcut Saklı Yordamları Kullanma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_CS.zip) veya [PDF 'yi indirin](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/datatutorial68cs1.pdf)

> Önceki öğreticide, yeni saklı yordamlar oluşturmak için TableAdapter Sihirbazı 'Nı nasıl kullanacağınızı öğrendiniz. Bu öğreticide, aynı TableAdapter sihirbazının mevcut saklı yordamlarla nasıl çalışabileceğini öğreniyoruz. Ayrıca, veritabanınıza el ile yeni saklı yordamlar eklemeyi öğreneceksiniz.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) , yazılan veri kümesi s TableAdapters 'in, ad-hoc SQL deyimleri yerine verilere erişmek için saklı yordamları kullanmak üzere nasıl yapılandırılabileceğini gördük. Özellikle, TableAdapter sihirbazının Bu saklı yordamları otomatik olarak nasıl oluşturmasını inceledik. Eski bir uygulamayı ASP.NET 2,0 ' ye taşıma veya mevcut bir veri modeli etrafında ASP.NET 2,0 Web sitesi oluştururken, veritabanının ihtiyacımız olan saklı yordamları zaten içermesi önerilir. Alternatif olarak, saklı yordamlarınızı el ile veya saklı yordamlarınızı otomatik üreten TableAdapter Sihirbazı dışında bir araç aracılığıyla oluşturmayı tercih edebilirsiniz.

Bu öğreticide, TableAdapter 'ı mevcut saklı yordamları kullanmak üzere nasıl yapılandıracağınızı inceleyeceğiz. Northwind veritabanı 'nın yalnızca küçük bir yerleşik saklı yordam kümesine sahip olduğu için, Visual Studio ortamı aracılığıyla veritabanına yeni saklı yordamları el ile eklemek için gereken adımlara de bakacağız. Haydi başlayın!

> [!NOTE]
> Işlem öğreticisindeki [sarmalama veritabanı değişikliklerine](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md) , işlemleri desteklemek için TableAdapter 'a (`BeginTransaction`, `CommitTransaction`vb.) Yöntemler ekledik. Alternatif olarak, işlemler, veri erişim katmanı kodunda hiçbir değişiklik yapılmasını gerektirmeyen bir saklı yordam içinde tamamen yönetilebilir. Bu öğreticide, bir işlem kapsamındaki saklı yordam deyimlerini yürütmek için kullanılan T-SQL komutlarını araştıracağız.

## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>1\. Adım: saklı yordamları Northwind veritabanına ekleme

Visual Studio, bir veritabanına yeni saklı yordamlar eklemenizi kolaylaştırır. Belirli bir `CategoryID` değerine sahip olanlar için `Products` tablosundan tüm sütunları döndüren Northwind veritabanına yeni bir saklı yordam ekleyelim. Sunucu Gezgini penceresinden, klasörler-veritabanı diyagramları, tabloları, görünümleri ve benzeri öğeleri görüntüleyecek şekilde Northwind veritabanını genişletin. Önceki öğreticide gördüğünüz gibi, saklı yordamlar klasörü, veritabanı mevcut saklı yordamlarını içerir. Yeni bir saklı yordam eklemek için, saklı yordamlar klasörüne sağ tıklayıp bağlam menüsünden Yeni saklı yordam Ekle seçeneğini belirlemeniz yeterlidir.

[![saklı yordamlar klasörüne sağ tıklayın ve yeni bir saklı yordam ekleyin](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image1.png)

**Şekil 1**: saklı yordamlar klasörüne sağ tıklayın ve yeni bir saklı yordam ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image3.png))

Şekil 1 ' de gösterildiği gibi, yeni saklı yordam Ekle seçeneğinin belirlenmesi, Visual Studio 'da, saklı yordamı oluşturmak için gereken SQL betiğinin ana hattını içeren bir betik penceresi açar. Bu betiği, saklı yordamın veritabanına eklendiği noktada, bu betiği dışarı ve yürütmek için işimiz olur.

Aşağıdaki betiği girin:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample1.sql)]

Bu komut dosyası yürütüldüğünde `Products_SelectByCategoryID`adlı Northwind veritabanına yeni bir saklı yordam ekler. Bu saklı yordam tek bir giriş parametresi kabul eder (`@CategoryID``int`) ve eşleşen `CategoryID` değeri olan bu ürünlerin tüm alanlarını döndürür.

Bu `CREATE PROCEDURE` betiği yürütmek ve saklı yordamı veritabanına eklemek için, araç çubuğundaki Kaydet simgesine tıklayın veya CTRL + S tuşlarına basın. Bunu yaptıktan sonra, saklı yordamlar klasörü yeni oluşturulan saklı yordamı gösteren yenilenir. Ayrıca, penceredeki komut dosyası, `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID` `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`olarak değiştirir. `CREATE PROCEDURE`, veritabanına yeni bir saklı yordam ekler ve `ALTER PROCEDURE` mevcut bir yordamı güncelleştirir. Betiğin başlangıcı `ALTER PROCEDURE`olarak değiştiği için, saklı yordamlar giriş parametreleri veya SQL deyimlerini değiştirmek ve kaydet simgesine tıklamak saklı yordamı bu değişikliklerle güncelleştirir.

Şekil 2 `Products_SelectByCategoryID` saklı yordamı kaydedildikten sonra Visual Studio 'Yu gösterir.

[![saklı yordam veritabanına Products_SelectByCategoryID eklendi](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image4.png)

**Şekil 2**: `Products_SelectByCategoryID` saklı yordam veritabanına eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image6.png))

## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>2\. Adım: TableAdapter 'ı varolan bir saklı yordamı kullanacak şekilde yapılandırma

Artık `Products_SelectByCategoryID` saklı yordam veritabanına eklendiğine göre, veri erişim katmanımızı, yöntemlerinden biri çağrıldığında bu saklı yordamı kullanacak şekilde yapılandırabiliriz. Özellikle, yeni oluşturduğumuz `Products_SelectByCategoryID` saklı yordamı çağıran `NorthwindWithSprocs` yazılan veri kümesindeki `ProductsTableAdapter` bir `GetProductsByCategoryID(categoryID)` yöntemi ekleyeceğiz.

`NorthwindWithSprocs` veri kümesini açarak başlayın. `ProductsTableAdapter` sağ tıklayın ve TableAdapter sorgu Yapılandırma Sihirbazı 'nı başlatmak için Sorgu Ekle ' yi seçin. [Önceki öğreticide](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) TableAdapter 'ın bizim için yeni bir saklı yordam oluşturmasını kabul ettik. Ancak, bu öğretici için yeni TableAdapter yöntemini mevcut `Products_SelectByCategoryID` saklı yordamına bağlamak istiyoruz. Bu nedenle, sihirbazın ilk adımından mevcut saklı yordamı kullan seçeneğini belirleyin ve ardından Ileri ' ye tıklayın.

[![varolan saklı yordamı kullan seçeneğini belirleyin](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image7.png)

**Şekil 3**: mevcut saklı yordamı kullan seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image9.png))

Aşağıdaki ekran, veritabanı saklı yordamları ile doldurulmuş bir açılan liste sağlar. Saklı bir yordamın seçilmesi sol taraftaki giriş parametrelerini ve sağ tarafta (varsa) veri alanlarını listeler. Listeden `Products_SelectByCategoryID` saklı yordamını seçin ve Ileri ' ye tıklayın.

[![Products_SelectByCategoryID saklı yordamını seçin](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image10.png)

**Şekil 4**: `Products_SelectByCategoryID` saklı yordamını seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image12.png))

Sonraki ekranda, saklı yordam tarafından ne tür verilerin döndürüldüğü ve buradaki yanıtınız TableAdapter s yöntemi tarafından döndürülen türü belirler. Örneğin, tablo verilerinin döndürüldüğünü gösteriyorsa, yöntemi saklı yordam tarafından döndürülen kayıtlarla doldurulmuş bir `ProductsDataTable` örneği döndürür. Buna karşılık, bu saklı yordamın tek bir değer döndürdüğünü gösteriyorsa, TableAdapter, saklı yordam tarafından döndürülen ilk kaydın ilk sütununda değere atanan bir `object` döndürür.

`Products_SelectByCategoryID` saklı yordam belirli bir kategoriye ait tüm ürünleri döndürdüğünden, ilk yanıt tablolu verileri seçin ve Ileri ' ye tıklayın.

[![saklı yordamın tablo verilerini döndürdüğünü gösterir](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image13.png)

**Şekil 5**: saklı yordamın tablo verilerini döndürdüğünü belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image15.png))

Her şey, hangi yöntem desenlerinin kullanılacağını ve ardından bu yöntemlerin adlarını belirtmektedir. Her ikisini de bir DataTable doldur ve işaretlenen bir DataTable seçeneklerini döndür, ancak yöntemleri `FillByCategoryID` ve `GetProductsByCategoryID`olarak yeniden adlandırın. Ardından, sihirbazın gerçekleştireceği görevlerin özetini gözden geçirmek için Ileri ' ye tıklayın. Her şey doğru görünüyorsa, son ' a tıklayın.

[![, Fillbycategoryıd ve Getproductsbycategoryıd metotlarını adlandırın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image16.png)

**Şekil 6**: yöntemleri `FillByCategoryID` ve `GetProductsByCategoryID` adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image18.png))

> [!NOTE]
> Az önce oluşturduğumuz TableAdapter yöntemleri, `FillByCategoryID` ve `GetProductsByCategoryID`, `int`türünde bir giriş parametresi bekler. Bu giriş parametresi değeri, `@CategoryID` parametresi aracılığıyla saklı yordama geçirilir. `Products_SelectByCategory` saklı yordam parametrelerini değiştirirseniz, Bu TableAdapter yöntemlerinin parametrelerini de güncelleştirmeniz gerekir. [Önceki öğreticide](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)anlatıldığı gibi bu, iki farklı şekilde yapılabilir: parametreleri parametreler koleksiyonuna el ile ekleyip kaldırarak veya TableAdapter Sihirbazı 'nı yeniden çalıştırarak.

## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>3\. Adım: BLL 'ye`GetProductsByCategoryID(categoryID)`yöntemi ekleme

`GetProductsByCategoryID` DAL yöntemi tamamlandıktan sonra, bir sonraki adım Iş mantığı katmanında bu yönteme erişim sağlamaktır. `ProductsBLLWithSprocs` sınıfı dosyasını açın ve aşağıdaki yöntemi ekleyin:

[!code-csharp[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample2.cs)]

Bu BLL yöntemi yalnızca `ProductsTableAdapter` s `GetProductsByCategoryID` yönteminden döndürülen `ProductsDataTable` döndürür. `DataObjectMethodAttribute` özniteliği, ObjectDataSource tarafından veri kaynağı Yapılandırma Sihirbazı tarafından kullanılan meta verileri sağlar. Özellikle, bu yöntem, seçme sekmesi açılan listesinde görünür.

## <a name="step-4-displaying-products-by-category"></a>4\. Adım: ürünleri kategoriye göre görüntüleme

Yeni eklenen `Products_SelectByCategoryID` saklı yordamını ve ilgili DAL ve BLL yöntemlerini test etmek için DropDownList ve GridView içeren bir ASP.NET sayfası oluşturalım. Bu, GridView seçili kategoriye ait ürünleri görüntülerken DropDownList veritabanındaki tüm kategorileri listeler.

> [!NOTE]
> Önceki öğreticilerde DropDownLists kullanarak ana/ayrıntı arabirimlerini oluşturduk. Bu tür bir ana/ayrıntı raporunu uygulamaya yönelik daha ayrıntılı bir bakış için, [bir DropDownList öğreticisi Ile ana/ayrıntı filtrelemesine](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) bakın.

`AdvancedDAL` klasöründeki `ExistingSprocs.aspx` sayfasını açın ve araç kutusundan bir DropDownList 'i tasarımcı üzerine sürükleyin. DropDownList s `ID` özelliğini `Categories` ve `AutoPostBack` özelliğini `true`olarak ayarlayın. Ardından, akıllı etiketinden sonra, `CategoriesDataSource`adlı yeni bir ObjectDataSource için DropDownList 'i bağlayın. ObjectDataSource 'ı, verileri `CategoriesBLL` sınıf s `GetCategories` yönteminden alan bir şekilde yapılandırın. GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ayarlayın.

[CategoriesBLL sınıf s GetCategories yönteminden veri alma ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image19.png)

**Şekil 7**: `CategoriesBLL` Class s `GetCategories` yönteminden verileri alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image21.png))

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image22.png)

**Şekil 8**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinden açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image24.png))

ObjectDataSource sihirbazını tamamladıktan sonra, DropDownList 'i `CategoryName` veri alanını görüntüleyecek şekilde yapılandırın ve `CategoryID` alanını her `ListItem`için `Value` olarak kullanın.

Bu noktada, DropDownList ve ObjectDataSource 'un bildirim temelli işaretlemesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample3.aspx)]

Sonra, bir GridView 'u tasarımcıya sürükleyin ve DropDownList 'in altına yerleştirebilirsiniz. GridView s `ID` `ProductsByCategory` ve akıllı etiketinden `ProductsByCategoryDataSource`adlı yeni bir ObjectDataSource 'a bağlayın. `ProductsByCategoryDataSource` ObjectDataSource 'u `ProductsBLLWithSprocs` sınıfını kullanacak şekilde yapılandırın, bu, `GetProductsByCategoryID(categoryID)` yöntemini kullanarak verilerini alır. Bu GridView yalnızca verileri göstermek için kullanılacaksa, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden (yok) açılan listeleri ayarlayın ve Ileri ' ye tıklayın.

[![, bu ObjectDataSource 'ı ProductsBLLWithSprocs sınıfını kullanacak şekilde yapılandırma](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image25.png)

**Şekil 9**: `ProductsBLLWithSprocs` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image27.png))

[Getproductsbycategoryıd (CategoryID) yönteminden veri alma ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image28.png)

**Şekil 10**: `GetProductsByCategoryID(categoryID)` yönteminden verileri alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image30.png))

SELECT sekmesinde seçilen yöntem bir parametre bekler, bu nedenle sihirbazın son adımında bize parametre kaynağı sorulur. Parametre kaynağı açılır listesini denetlemek ve ControlID açılır listesinden `Categories` denetimini seçmek için ayarlayın. Sihirbazı tamamladığınızda son ' a tıklayın.

[![CategoryID parametresinin kaynağı olarak DropDownList kategorisini kullanın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image31.png)

**Şekil 11**: `categoryID` parametresinin kaynağı olarak `Categories` DropDownList kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image33.png))

Visual Studio, ObjectDataSource 'u tamamladıktan sonra, ürün verileri alanlarının her biri için BoundFields ve bir CheckBoxField ekler. Bu alanları uygun gördüğünüz şekilde özelleştirebilirsiniz.

Sayfayı bir tarayıcıdan ziyaret edin. Sayfa ziyaret edildiğinde, Içecek kategorisi seçilir ve ilgili ürünler kılavuzda listelenir. Aşağı açılan listeyi alternatif bir kategori olarak değiştirme, 12 gösterdiği gibi, geri göndermeye neden olur ve Kılavuzu yeni seçilen kategorinin ürünleriyle yeniden yükler.

[Üretim kategorisindeki Ürünler ![görüntülenir](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image34.png)

**Şekil 12**: üretim kategorisindeki Ürünler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image36.png))

## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>5\. Adım: saklı yordam deyimlerini bir Işlemin kapsamı Içinde sarmalama

Işlem öğreticisindeki [sarmalama veritabanı değişikliklerine](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md) bir işlem kapsamında bir dizi veritabanı değiştirme deyimi gerçekleştirmeye yönelik teknikler tartışıyoruz. İşlemin şemsiye altında gerçekleştirilen değişikliklerin tümünün başarılı olduğunu veya tümünün başarısız olduğunu, Atomicity 'i garanti altına çekin. İşlemleri kullanma teknikleri şunları içerir:

- `System.Transactions` ad alanındaki sınıfları kullanarak,
- Veri erişim katmanının `SqlTransaction`gibi ADO.NET sınıfları kullanmasını ve
- T-SQL işlem komutları doğrudan saklı yordam içinde ekleniyor

Işlem öğreticisindeki *sarmalama veritabanı değişiklikleri* , DAL içindeki ADO.NET sınıflarını kullandı. Bu öğreticinin geri kalanında, bir saklı yordamın içinden T-SQL komutları kullanılarak bir işlemin nasıl yönetileceği incelenir.

Bir işlemi el ile başlatmak, yürütmek ve geri almak için üç ana SQL komutu sırasıyla `BEGIN TRANSACTION`, `COMMIT TRANSACTION`ve `ROLLBACK TRANSACTION`. ADO.NET yaklaşımıyla olduğu gibi, saklı bir yordam içinden işlemleri kullanırken aşağıdaki kalıbı uygulamanız gerekir:

1. İşlemin başlangıcını belirtir.
2. İşlemi oluşturan SQL deyimlerini yürütün.
3. 2\. adımdaki deyimlerden birinde bir hata varsa, işlemi geri alın
4. 2\. adımdaki tüm deyimler hata olmadan tamamlandıysanız, işlemi yürütün.

Bu model, aşağıdaki şablon kullanılarak T-SQL sözdiziminde uygulanabilir:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample4.sql)]

Şablon, SQL Server 2005 için yeni bir yapı olan `TRY...CATCH` bloğu tanımlayarak başlar. İçindeki C#`try...catch` bloklarla benzer şekılde, SQL `TRY...CATCH` bloğu `TRY` bloğundaki deyimleri yürütür. Herhangi bir ifade bir hata harekete geçirirse denetim hemen `CATCH` bloğuna aktarılır.

İşlemi oluşturan SQL deyimlerini yürüten bir hata yoksa, `COMMIT TRANSACTION` deyimi değişiklikleri kaydeder ve işlemi tamamlar. Ancak, deyimlerden biri bir hatayla sonuçlanırsa, `CATCH` bloğundaki `ROLLBACK TRANSACTION`, veritabanının işlemin başlangıcından önceki durumuna geri döner. Saklı yordam Ayrıca, bir `SqlException` uygulamada oluşturulmasına neden olan [raerror komutunu](https://msdn.microsoft.com/library/ms178592.aspx)kullanarak bir hata oluşturur.

> [!NOTE]
> `TRY...CATCH` bloğu SQL Server 2005 ' de yeni olduğundan, Microsoft SQL Server eski sürümlerini kullanıyorsanız yukarıdaki şablon çalışmayacaktır. SQL Server 2005 kullanmıyorsanız, diğer SQL Server sürümleriyle çalışacak bir şablon için [SQL Server saklı yordamlarındaki Işlemleri yönetme](http://www.4guysfromrolla.com/webtech/080305-1.shtml) bölümüne bakın.

Somut bir örneğe bakalım. `Categories` ve `Products` tabloları arasında bir yabancı anahtar kısıtlaması bulunur, yani `Products` tablosundaki her `CategoryID` alanının `CategoryID` tablosundaki bir `Categories` değere eşlenmesi gerekir. İlişkili ürünlere sahip bir kategoriyi silmeye çalışmak gibi bu kısıtlamayı ihlal eden herhangi bir eylem, yabancı anahtar kısıtlaması ihlaline neden olur. Bunu doğrulamak için, Ikili verilerle çalışma bölümünde (`~/BinaryData/UpdatingAndDeleting.aspx`) var olan Ikili verileri güncelleştirme ve silme ' yi yeniden ziyaret edin. Bu sayfa, sistem içindeki her kategoriyi Düzenle ve Sil düğmeleriyle birlikte listeler (bkz. Şekil 13), ancak ilişkili ürünleri (örneğin, Içecek gibi) içeren bir kategoriyi silmeye çalışırsanız, silme yabancı anahtar kısıtlaması ihlali nedeniyle başarısız olur (bkz. Şekil 14).

[![her kategori, Düzenle ve Sil düğmeleriyle bir GridView içinde görüntülenir](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image37.png)

**Şekil 13**: her kategori Düzenle ve Sil düğmeleriyle bir GridView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image39.png))

[![var olan ürünleri olan bir kategoriyi silemezsiniz](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image40.png)

**Şekil 14**: mevcut ürünlere sahip bir kategoriyi silemezsiniz ([tam boyutlu görüntüyü görüntülemek için tıklatın](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image42.png))

Bununla birlikte, kategorilerin ilişkili ürünlere sahip olup olmamasına bakılmaksızın silinmesine izin vermek istiyoruz. Ürünlerin silindiği bir kategori olması gerekir. Ayrıca, mevcut ürünlerini de silmek istiyoruz (başka bir seçenek de yalnızca ürünlerini `NULL`olarak ayarlamak `CategoryID`. Bu işlev, yabancı anahtar kısıtlamasının basamaklı kuralları aracılığıyla uygulanabilir. Alternatif olarak, `@CategoryID` girişi parametresini kabul eden bir saklı yordam oluşturuyoruz ve çağrıldığında, ilişkili ürünlerin tümünü ve ardından belirtilen kategoriyi açıkça siler.

Bu tür bir saklı yordamda ilk girişimimiz aşağıdaki gibi görünebilir:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample5.sql)]

Bu işlem, ilişkili ürünleri ve kategoriyi kesin bir şekilde silirken, bunu bir işlemin şemsiye altında yapmaz. `Categories`, belirli bir `@CategoryID` değerinin silinmesini engelleyecek başka bir yabancı anahtar kısıtlaması olduğunu düşünün. Bu sorun, kategori silmeyi denemeden önce tüm ürünlerin silineceği bir durumdur. Bu tür bir kategori için, bu saklı yordamın diğer bir tablodaki ilişkili kayıtları hala olduğundan, bu saklı yordamın tüm ürünlerini kaldıracağından emin olmanız gerekir.

Saklı yordam bir işlemin kapsamı içinde sarmalanmış ise, `Products` tablodaki silme işlemleri `Categories`başarısız silme işleminin yüzüne geri döndürülür. Aşağıdaki saklı yordam betiği, iki `DELETE` deyimi arasındaki sürekliliği güvence altına almak için bir işlem kullanır:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample6.sql)]

`Categories_Delete` saklı yordamı Northwind veritabanına eklemek için bir dakikanızı ayırın. Bir veritabanına saklı yordamlar ekleme yönergeleri için adım 1 ' e geri bakın.

## <a name="step-6-updating-thecategoriestableadapter"></a>6\. Adım:`CategoriesTableAdapter` güncelleştirme

`Categories_Delete` saklı yordamı veritabanına eklediğimiz sırada DAL, silme işlemini gerçekleştirmek için geçici SQL deyimlerini kullanmak üzere yapılandırılmıştır. `CategoriesTableAdapter` güncelleştirmemiz ve bunun yerine `Categories_Delete` saklı yordamını kullanması gerekir.

> [!NOTE]
> Bu öğreticide daha önce `NorthwindWithSprocs` veri kümesiyle çalışıyoruz. Ancak bu veri kümesi yalnızca tek bir varlığa sahiptir, `ProductsDataTable`ve kategoriler ile çalışmamız gerekir. Bu nedenle, Bu öğreticinin geri kalanında, `Northwind` veri kümesine başvuran veri erişim katmanı hakkında konuşdum ve ilk olarak [veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-cs.md) öğreticisinde oluşturduğumuz.

Northwind veri kümesini açın, `CategoriesTableAdapter`seçin ve Özellikler penceresi gidin. Özellikler penceresi, TableAdapter tarafından kullanılan `InsertCommand`, `UpdateCommand`, `DeleteCommand`ve `SelectCommand` yanı sıra adının ve bağlantı bilgilerinin listesini görüntüler. Ayrıntılarını görmek için `DeleteCommand` özelliğini genişletin. Şekil 15 ' in gösterdiği gibi, `DeleteCommand` s `CommandType` özelliği metin olarak ayarlanır, bu da metin `CommandText` özelliğindeki metni geçici bir SQL sorgusu olarak göndermesini söyler.

![Özellikler penceresinde özelliklerini görüntülemek için tasarımcıda CategoriesTableAdapter seçin](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image43.png)

**Şekil 15**: Özellikler penceresinde, özelliklerini görüntülemek için tasarımcıda `CategoriesTableAdapter` seçin

Bu ayarları değiştirmek için Özellikler penceresi (DeleteCommand) metnini seçin ve açılan listeden (yeni) seçeneğini belirleyin. Bu, `CommandText`, `CommandType`ve `Parameters` özelliklerinin ayarlarını siler. Sonra, `CommandType` özelliğini `StoredProcedure` olarak ayarlayın ve ardından `CommandText` (`dbo.Categories_Delete`) için saklı yordamın adını yazın. Bu sırada özellikleri girdiğinizden emin olun-önce `CommandType` ve `CommandText`-Visual Studio, parametreler koleksiyonunu otomatik olarak doldurur. Bu özellikleri bu sırada girmezseniz parametreler koleksiyonu Düzenleyicisi aracılığıyla parametreleri el ile eklemeniz gerekir. Her iki durumda da, doğru parametre ayarları değişikliklerinin yapıldığını doğrulamak üzere parametreler koleksiyonu düzenleyicisini açmak için parametreler özelliğindeki üç nokta işaretine tıkladığını unutmayın (bkz. Şekil 16). İletişim kutusunda herhangi bir parametre görmüyorsanız, `@CategoryID` parametresini el ile ekleyin (`@RETURN_VALUE` parametresini eklemeniz gerekmez).

![Parametre ayarlarının doğru olduğundan emin olun](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image44.png)

**Şekil 16**: parametre ayarlarının doğru olduğundan emin olun

DAL güncelleştirildikten sonra bir kategorinin silinmesi, ilişkili tüm ürünlerini otomatik olarak siler ve bu işlemi bir işlemin şemsiye altındayken yapılır. Bunu doğrulamak için, mevcut Ikili verileri güncelleştirme ve silme sayfasına dönün ve kategorilerden biri için Sil düğmesine tıklayın. Fareyle tek tıklamayla, kategori ve onunla ilişkili tüm ürünler silinir.

> [!NOTE]
> `Categories_Delete` saklı yordamı test etmeden önce, seçili kategoriyle birlikte bir dizi ürünü de silecek şekilde, veritabanınızın yedek bir kopyasını oluşturmak için bu durum akıllıca olabilir. `App_Data``NORTHWND.MDF` veritabanını kullanıyorsanız, Visual Studio 'Yu kapatın ve `App_Data` içindeki MDF ve LDF dosyalarını başka bir klasöre kopyalamanız yeterlidir. İşlevselliği test ettikten sonra, Visual Studio 'Yu kapatarak ve `App_Data` içindeki geçerli MDF ve LDF dosyalarını yedek kopyalarla değiştirerek veritabanını geri yükleyebilirsiniz.

## <a name="summary"></a>Özet

TableAdapter s Sihirbazı ABD için otomatik olarak saklı yordamlar üretirken, bu tür saklı yordamımız veya bunları el ile veya diğer araçlarla oluşturmak istediğimiz zamanlar olabilir. Bu senaryolara uyum sağlamak için TableAdapter, var olan bir saklı yordamı işaret etmek üzere de yapılandırılabilir. Bu öğreticide, saklı yordamların Visual Studio ortamı aracılığıyla bir veritabanına el ile nasıl ekleneceğini ve TableAdapter s yöntemlerini bu saklı yordamlara nasıl bağlayabileceğinizi inceledik. Ayrıca, saklı bir yordamın içinden işlemleri başlatmak, yürütmek ve geri almak için kullanılan T-SQL komutlarını ve betik düzenlerini de inceledik.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, lül Geisenow, S Ren Jacob Lauritsen ve Teresa Murphy. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
> [İleri](updating-the-tableadapter-to-use-joins-cs.md)
