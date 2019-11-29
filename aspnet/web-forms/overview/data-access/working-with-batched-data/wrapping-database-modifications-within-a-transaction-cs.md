---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
title: Bir Işlem içindeki veritabanı değişikliklerini sarmalamaC#() | Microsoft Docs
author: rick-anderson
description: Bu öğretici, veri toplu işlerini güncelleştirme, silme ve ekleme konusunda görünen dört ilkidir. Bu öğreticide veritabanı işlemlerinin nasıl izin vereceğinizi öğreniyoruz...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: b45fede3-c53a-4ea1-824b-20200808dbae
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
msc.type: authoredcontent
ms.openlocfilehash: da69e466a5b506b869dc8fc0624f3e6a479199a8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74624645"
---
# <a name="wrapping-database-modifications-within-a-transaction-c"></a>Veritabanı Değişikliklerini Bir İşlemin İçinde Sarmalama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_CS.zip) veya [PDF 'yi indirin](wrapping-database-modifications-within-a-transaction-cs/_static/datatutorial63cs1.pdf)

> Bu öğretici, veri toplu işlerini güncelleştirme, silme ve ekleme konusunda görünen dört ilkidir. Bu öğreticide, veritabanı işlemlerinin toplu iş değişikliklerinin bir atomik işlem olarak nasıl gerçekleştirilebildiğini öğrenir, bu da tüm adımların başarılı veya tüm adımların başarısız olmasını sağlar.

## <a name="introduction"></a>Giriş

Veri öğreticisini [ekleme, güncelleştirme ve silmeye Ilişkin genel bakışa](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) Başlarken, GridView, satır düzeyinde Düzenle ve silme için yerleşik destek sağlar. Fareyle birkaç tıklamayla, bir kod satırı yazmadan zengin veri değişikliği arabirimi oluşturmak mümkündür. bu nedenle, her satır için Düzenle ve siliniyor içeriklerde olduğu sürece. Ancak, bazı senaryolarda bu yeterli değildir ve kullanıcılara bir kayıt kümesini düzenleme veya silme olanağı sağlamamız gerekir.

Örneğin, çoğu Web tabanlı e-posta istemcisi, her satırın e-posta bilgilerini (konu, gönderen ve benzeri) içeren bir onay kutusu içerdiği her iletiyi listelemek için bir kılavuz kullanır. Bu arabirim, kullanıcının birden çok iletiyi denetleyerek ve sonra seçili Iletileri Sil düğmesine tıklayarak silmesine izin verir. Toplu düzenleme arabirimi, kullanıcıların birçok farklı kaydı yaygın olarak düzenleyebildiği durumlarda idealdir. Kullanıcının Düzenle ' ye tıklaması, değişiklik yapması ve ardından değiştirilmesi gereken her kayıt için Güncelleştir ' e tıklaması yerine, bir Batch düzenleme arabirimi her bir satırı düzenleme arabirimiyle işler. Kullanıcı değiştirilmesi gereken satır kümesini hızlıca değiştirebilir ve sonra Tümünü Güncelleştir düğmesine tıklayarak bu değişiklikleri kaydeder. Bu öğretici kümesinde, verilerin toplu olarak eklenmesi, düzenlenmesine ve silinmesine yönelik arabirimlerin nasıl oluşturulacağını inceleyeceğiz.

Toplu işlem gerçekleştirirken, toplu işteki bazı işlemlerden bazılarının başarılı olması durumunda başarısız olması gerekip gerekmediğini belirleme açısından önemlidir. Toplu işi silme arabirimi-seçili olan ilk kayıt başarıyla silinirse ne olması gerekir, ancak ikinci biri başarısız olursa, yabancı anahtar kısıtlaması ihlali nedeniyle ne olur? İlk kaydın silinmesi geri alınır mi yoksa ilk kaydın silinme için kabul edilebilir mi?

Toplu işlemin bir [atomik işlem](http://en.wikipedia.org/wiki/Atomic_operation)olarak değerlendirilmesini istiyorsanız, tüm adımların başarılı veya adımların tümü başarısız olursa, veri erişim katmanının [veritabanı işlemlerine](http://en.wikipedia.org/wiki/Database_transaction)yönelik destek içerecek şekilde artırılması gerekir. Veritabanı işlemleri, işlemin şemsiye altında yürütülen `INSERT`, `UPDATE`ve `DELETE` deyimlerinin kararlılığını garanti eder ve tüm modern veritabanı sistemleri tarafından desteklenen bir özelliktir.

Bu öğreticide, veritabanı işlemlerini kullanmak için DAL genişletme bölümüne bakacağız. Sonraki öğreticiler, toplu iş ekleme, güncelleştirme ve silme arabirimleri için Web sayfalarını uygulamayı inceler. Haydi başlayın!

> [!NOTE]
> Toplu işlemdeki verileri değiştirirken, kararlılık her zaman gerekli değildir. Bazı senaryolarda, bir Web tabanlı e-posta istemcisinden bir e-posta kümesini silerken, bazı veri değişikliklerinin başarılı olması ve aynı toplu işteki diğer kişilerin başarısız olması kabul edilebilir. Silme işlemi boyunca bir veritabanı hatası algıladığında, bu, hata olmadan işlenen kayıtların silinmesini de kabul eder. Bu gibi durumlarda, DAL veritabanı işlemlerini destekleyecek şekilde değiştirilmemelidir. Ancak, kararlılık 'in çok önemli olduğu diğer toplu işlem senaryoları vardır. Bir müşteri fonlarını bir banka hesabından diğerine taşıdıkça iki işlem gerçekleştirilmelidir: fonlar ilk hesaptan düşülmeli ve sonra ikincisine eklenmelidir. Bankanın ilk adımı başarılı bir şekilde gerçekleştiremeyebilir, ancak ikinci adım başarısız olsa da, müşterileri daha iyi bir şekilde daha fazla olmaz. Bu öğreticide ilerleyerek ve veritabanı işlemlerini desteklemek için DAL geliştirmeleri uygulayıp, bunları Batch ekleme, güncelleştirme ve silme toplu işlemlerinde kullanmayı planlamıyorsanız, aşağıdaki üç öğreticide oluşturacağız.

## <a name="an-overview-of-transactions"></a>Işlemlere genel bakış

Çoğu veritabanı, birden çok veritabanı komutunun tek bir mantıksal iş biriminde gruplandırılmasına olanak sağlayan *işlemler*için destek içerir. Bir işlemi oluşturan veritabanı komutlarının atomik olduğu garanti edilir, yani tüm komutların başarısız olduğu veya tümünün başarılı olacağı anlamına gelir.

Genel olarak, işlemler SQL deyimleriyle aşağıdaki model kullanılarak uygulanır:

1. İşlemin başlangıcını belirtir.
2. İşlemi oluşturan SQL deyimlerini yürütün.
3. 2\. adımdaki deyimlerden birinde bir hata varsa, işlemi geri alın.
4. 2\. adımdaki tüm deyimler hata olmadan tamamlandıysanız, işlemi yürütün.

İşlemin oluşturulması, yürütülmesi ve geri dönmesi için kullanılan SQL deyimleri, SQL betikleri yazarken veya saklı yordamlar oluştururken el ile veya ADO.NET ya da [`System.Transactions` ad alanındaki](https://msdn.microsoft.com/library/system.transactions.aspx)sınıfların kullanılmasıyla programlama yoluyla el ile girilebilir. Bu öğreticide, yalnızca ADO.NET kullanarak işlem yönetimini inceleyeceğiz. Gelecekteki bir öğreticide, veri erişim katmanında saklı yordamların nasıl kullanılacağına göz atacağız. Bu durumda, işlemleri oluşturmak, geri almak ve yürütmek için SQL deyimlerini keşfedeceğiz. Bu sırada daha fazla bilgi için [SQL Server saklı yordamlarındaki Işlemleri yönetme](http://www.4guysfromrolla.com/webtech/080305-1.shtml) konusuna bakın.

> [!NOTE]
> `System.Transactions` ad alanındaki [`TransactionScope` sınıfı](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx) , geliştiricilerin bir işlem kapsamındaki bir deyim serisini programlama yoluyla sarmasını ve bir Microsoft SQL Server veritabanı, Oracle veritabanı ve bir Web hizmeti gibi iki farklı veritabanı ya da heterojen veri deposu türleri gibi birden çok kaynağı içeren karmaşık işlemler için destek içerir. ADO.NET sınıfı `TransactionScope` yerine bu öğreticide ADO.NET işlemleri kullanmaya karar verdim ve çoğu durumda, çok daha az kaynak kullanımı. Ayrıca, bazı senaryolarda `TransactionScope` sınıfı Microsoft Dağıtılmış İşlem Düzenleyicisi (MSDTC) kullanır. MSDTC 'nin içindeki yapılandırma, uygulama ve performans sorunları, Bu öğreticilerin kapsamını özelleştirilmiş ve gelişmiş bir konuyla ve bunların ötesinde kolaylaştırır.

ADO.NET ' de SqlClient sağlayıcısıyla çalışırken işlemler, bir [`SqlTransaction` nesnesi](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx)döndüren [`SqlConnection` sınıf](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) s [`BeginTransaction` yöntemine](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx)yapılan bir çağrıyla başlatılır. İşlemi oluşturan veri değiştirme deyimleri `try...catch` bir blok içine yerleştirilir. `try` bloğundaki bir ifadede bir hata oluşursa, yürütme, işlemin `SqlTransaction` nesne s [`Rollback` yöntemi](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx)aracılığıyla geri aktargetirilebileceği `catch` bloğuna aktarılır. Tüm deyimler başarıyla tamamlandıysanız, `try` bloğunun sonundaki `SqlTransaction` nesne s [`Commit` yöntemine](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx) yapılan bir çağrı işlemi kaydeder. Aşağıdaki kod parçacığında bu desenler gösterilmektedir. Ek sözdizimi ve ADO.NET ile işlem kullanma örnekleri için [işlem Ile veritabanı tutarlılığını koruma](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx) konusuna bakın.

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample1.cs)]

Varsayılan olarak, bir türü belirtilmiş veri kümesindeki TableAdapters işlemleri kullanmaz. Bir işlemin kapsamı içinde bir dizi veri değişikliği deyimi gerçekleştirmek için yukarıdaki kalıbı kullanan ek yöntemler dahil olmak üzere TableAdapter sınıflarını geliştirmemiz gereken işlemler için destek sağlamak üzere. 2\. adımda, bu yöntemleri eklemek için kısmi sınıfların nasıl kullanılacağını öğreneceğiz.

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>1\. Adım: toplu veri Web sayfalarıyla çalışmayı oluşturma

Veritabanı işlemlerini desteklemek için DAL 'nin nasıl geliştirdiğine yönelik keşfetmeye başlamadan önce, bu öğretici için ihtiyaç duyduğumuz ASP.NET Web sayfalarını ve bu öğreticiyi izleyen üç işlem için ilk olarak bir süre sürme. `BatchData` adlı yeni bir klasör ekleyerek başlayın ve ardından her sayfayı `Site.master` ana sayfayla ilişkilendirerek aşağıdaki ASP.NET sayfalarını ekleyin.

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`

![SqlDataSource ile Ilgili öğreticiler için ASP.NET sayfaları ekleyin](wrapping-database-modifications-within-a-transaction-cs/_static/image1.gif)

**Şekil 1**: SqlDataSource Ile ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `Default.aspx` kendi bölümünde öğreticileri listelemek için `SectionLevelTutorialListing.ascx` Kullanıcı denetimini kullanacaktır. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](wrapping-database-modifications-within-a-transaction-cs/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image1.png)

**Şekil 2**: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](wrapping-database-modifications-within-a-transaction-cs/_static/image2.png))

Son olarak, bu dört sayfayı `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, site haritasını özelleştirdikten sonra aşağıdaki biçimlendirmeyi ekleyin `<siteMapNode>`:

[!code-xml[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample2.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menüde artık toplu veri öğreticileri ile çalışma için öğeler yer almaktadır.

![Site Haritası artık toplu veri öğreticileri ile çalışmaya yönelik girişleri Içerir](wrapping-database-modifications-within-a-transaction-cs/_static/image3.gif)

**Şekil 3**: site haritasında artık toplu veri öğreticileri ile çalışmaya yönelik girişler yer almaktadır

## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>2\. Adım: veri erişim katmanını, veritabanı Işlemlerini destekleyecek şekilde güncelleştirme

İlk öğreticide geri değindiğimiz gibi, [bir veri erişim katmanı oluştururken](../introduction/creating-a-data-access-layer-cs.md), Içindeki türü belirtilmiş veri kümesi DataTable ve TableAdapters ' den oluşur. TableAdapters, veritabanından verileri veri okuma, DataTable üzerinde yapılan değişikliklerle veritabanını güncelleştirme, vb. gibi verileri bir veritabanına dönüştürür. TableAdapters 'in, Batch Update ve DB-Direct olarak adlandırılan verileri güncelleştirmek için iki desen sunmaya yönelik olduğunu hatırlayın. Batch Update düzeniyle, TableAdapter bir DataSet, DataTable veya DataRow koleksiyonu iletilir. Bu veriler, her Inserted, Modified veya Deleted satırı için numaralandırılır, `InsertCommand`, `UpdateCommand`veya `DeleteCommand` yürütülür. DB-Direct düzeniyle, TableAdapter, tek bir kaydı eklemek, güncelleştirmek veya silmek için gereken sütunların değerlerini geçti. Daha sonra DB doğrudan model yöntemi, uygun `InsertCommand`, `UpdateCommand`veya `DeleteCommand` ifadesini yürütmek için bu geçirilen değerleri kullanır.

Kullanılan güncelleştirme düzeniyle bağımsız olarak, TableAdapters otomatik oluşturulan Yöntemler işlemleri kullanmaz. Varsayılan olarak, TableAdapter tarafından gerçekleştirilen her bir INSERT, Update veya delete tek bir ayrık işlem olarak değerlendirilir. Örneğin, veritabanına on kayıt eklemek için BLL içindeki bazı kodlar tarafından DB-Direct deseninin kullanıldığını düşünün. Bu kod, TableAdapter s `Insert` yöntemini on kez çağırırdı. İlk beş ekleme başarılı, ancak altıncı bir özel durumla sonuçlanmış ise, ilk beş kayıt veritabanında kalır. Benzer şekilde, bir DataTable içindeki eklenen, değiştirilen ve silinen satırlarda ekleme, güncelleştirme ve silme işlemleri gerçekleştirmek için toplu güncelleştirme düzeninde kullanılırsa, ilk birkaç değişiklik başarılı olduysa ancak daha sonra bir hatayla karşılaştıysa, bu, önceki değişiklikleri tamamlandı, veritabanında kalır.

Belirli senaryolarda, bir dizi değişiklik genelinde kararlılık sağlamak istiyoruz. Bunu gerçekleştirmek için, bir işlemin şemsiye altında `InsertCommand`, `UpdateCommand`ve `DeleteCommand` çalıştıran yeni yöntemler ekleyerek TableAdapter 'ı el ile genişletmelidir. [Veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-cs.md) bölümünde, yazılan veri kümesi içindeki DataTable işlevlerinin işlevselliğini uzatmak için [kısmi sınıflar](http://en.wikipedia.org/wiki/Partial_type) kullanma konusunda baktık. Bu teknik, TableAdapters ile de kullanılabilir.

Yazılan veri kümesi `Northwind.xsd` `App_Code` klasör s `DAL` alt klasöründe bulunur. `TransactionSupport` adlı `DAL` klasörde bir alt klasör oluşturun ve `ProductsTableAdapter.TransactionSupport.cs` adlı yeni bir sınıf dosyası ekleyin (bkz. Şekil 4). Bu dosya, bir işlem kullanarak veri değişiklikleri gerçekleştirmeye yönelik yöntemleri içeren `ProductsTableAdapter` kısmi uygulamasını tutacaktır.

![TransactionSupport adlı bir klasör ve ProductsTableAdapter.TransactionSupport.cs adlı bir sınıf dosyası ekleyin](wrapping-database-modifications-within-a-transaction-cs/_static/image4.gif)

**Şekil 4**: `TransactionSupport` adlı bir klasör ve `ProductsTableAdapter.TransactionSupport.cs` adlı bir sınıf dosyası ekleyin

`ProductsTableAdapter.TransactionSupport.cs` dosyasına aşağıdaki kodu girin:

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample3.cs)]

Burada sınıf bildiriminde `partial` anahtar sözcüğü, içinde eklenen üyelerin `NorthwindTableAdapters` ad alanındaki `ProductsTableAdapter` sınıfına ekleneceğini belirtir. Dosyanın en üstündeki `using System.Data.SqlClient` bildirimine göz önünde edin. TableAdapter, SqlClient sağlayıcısını kullanacak şekilde yapılandırıldığından, kendi komutlarını veritabanına vermek için bir [`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx) nesnesi kullanır. Sonuç olarak, işlemi başlatmak ve sonra yürütmek ya da geri almak için `SqlTransaction` sınıfını kullandık. Microsoft SQL Server dışında bir veri deposu kullanıyorsanız, uygun sağlayıcıyı kullanmanız gerekir.

Bu yöntemler, bir işlemi başlatmak, geri almak ve yürütmek için gereken yapı taşlarını sağlar. Bunlar `public`işaretlenir, bu, DAL içindeki başka bir sınıftan veya BLL gibi mimarideki başka bir katmandan `ProductsTableAdapter`kullanılmasını sağlar. `BeginTransaction` TableAdapter iç `SqlConnection` açar (gerekirse), işlemi başlatır ve `Transaction` özelliğine atar ve işlemi iç `SqlDataAdapter` s `SqlCommand` nesnelerine ekler. `CommitTransaction` ve `RollbackTransaction` iç `Rollback` nesnesini kapatmadan önce, sırasıyla `Transaction` nesne s `Commit` ve `Connection` Yöntemleri çağırın.

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>3\. Adım: bir Işlemin şemsiye altında verileri güncelleştirmek ve silmek için yöntemler ekleme

Bu yöntemler tamamlansa, bir işlemin şemsiye altında bir dizi komut gerçekleştiren `ProductsDataTable` veya BLL 'e Yöntemler eklemeye hazırız. Aşağıdaki yöntem bir işlem kullanarak bir `ProductsDataTable` örneğini güncelleştirmek için Batch güncelleştirme modelini kullanır. `BeginTransaction` yöntemini çağırarak bir işlem başlatır ve sonra veri değiştirme deyimlerini vermek için bir `try...catch` bloğu kullanır. `Adapter` nesne `Update` yöntemine yapılan çağrı bir özel durumla sonuçlanırsa, yürütme hareketin geri alındığı ve özel durumun yeniden oluşturulduğu `catch` bloğuna aktarılır. `Update` yönteminin, sağlanan `ProductsDataTable` satırları numaralandırarak ve gerekli `InsertCommand`, `UpdateCommand`ve `DeleteCommand` işlemlerini gerçekleştirerek Batch güncelleştirme modelini uyguladığını unutmayın. Bu komutlardan herhangi biri bir hata ile sonuçlanırsa işlem, işlem ömrü boyunca yapılan önceki değişiklikleri geri alarak geri alınır. `Update` deyimin hatasız tamamlanabilmesi gerekir, işlem tamamen işlenir.

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample4.cs)]

`UpdateWithTransaction` yöntemini `ProductsTableAdapter.TransactionSupport.cs`parçalı sınıfı aracılığıyla `ProductsTableAdapter` sınıfına ekleyin. Alternatif olarak, bu yöntem bazı küçük sözdizimsel değişikliklerle Iş mantığı katmanı s `ProductsBLL` sınıfına eklenebilir. Yani, `this.BeginTransaction()`, `this.CommitTransaction()`ve `this.RollbackTransaction()` içindeki anahtar sözcüğünün `Adapter` ile değiştirilmeleri gerekir (`Adapter`, `ProductsBLL` türünde `ProductsTableAdapter`bir özelliğin adı olduğunu hatırlayın).

`UpdateWithTransaction` yöntemi Batch güncelleştirme modelini kullanır, ancak aşağıdaki yöntemin gösterdiği gibi bir dizi VERITABANı doğrudan çağrısı da bir işlemin kapsamı içinde kullanılabilir. `DeleteProductsWithTransaction` yöntemi, silinecek `ProductID` s olan `int`türünde bir `List<T>` girdi olarak kabul eder. Yöntemi, `BeginTransaction` çağrısı yoluyla işlemi başlatır ve sonra `try` bloğunda, her `ProductID` değeri için DB-Direct model `Delete` yöntemini çağıran sağlanan liste boyunca yinelenir. `Delete` çağrılarından herhangi biri başarısız olursa, denetim işlemin geri alındığı ve özel durumun yeniden oluşturulduğu `catch` bloğuna aktarılır. `Delete` yapılan tüm çağrılar başarılı olursa işlem gerçekleştirilir. Bu yöntemi `ProductsBLL` sınıfına ekleyin.

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample5.cs)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>Birden çok TableAdapters arasında Işlem uygulama

Bu öğreticide incelenen işlemle ilgili kod, `ProductsTableAdapter` birden çok deyimin atomik bir işlem olarak işlenmesine izin verir. Ancak, farklı veritabanı tablolarında birden fazla değişiklik otomatik olarak gerçekleştirilmesi gerekiyorsa ne olur? Örneğin, bir kategoriyi silerken, önce geçerli ürünlerini başka bir kategoriye yeniden atamak isteyebilirsiniz. Bu iki adım, ürünleri yeniden atayarak ve kategoriyi silmenin atomik bir işlem olarak yürütülmesi gerekir. Ancak `ProductsTableAdapter` yalnızca `Products` tablosunu değiştirme yöntemleri içerir ve `CategoriesTableAdapter` yalnızca `Categories` tablosunu değiştirme yöntemlerini içerir. Bu nedenle bir işlem hem TableAdapters?

Bir seçenek, `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` adlı `CategoriesTableAdapter` bir yöntem eklemektir ve bu yöntemin, her ikisi de ürünleri yeniden atar ve saklı yordamda tanımlanan bir işlemin kapsamındaki kategoriyi sildiği bir saklı yordam çağırmasıdır. Daha sonraki bir öğreticide saklı yordamlarda işlem başlatma, işleme ve geri alma işlemlerine bakacağız.

Başka bir seçenek de `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` yöntemini içeren DAL içinde yardımcı sınıf oluşturmaktır. Bu yöntem `CategoriesTableAdapter` ve `ProductsTableAdapter` bir örneğini oluşturur ve sonra bu iki TableAdapters `Connection` özelliklerini aynı `SqlConnection` örneğine ayarlar. Bu noktada, iki TableAdapters birini `BeginTransaction`çağrısı olan işlemi başlatır. Ürünleri yeniden atama ve kategoriyi silme TableAdapters yöntemleri, işlemin yürütüldüğü veya geri alındığı bir `try...catch` bloğunda çağrılır.

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>4\. Adım:`UpdateWithTransaction`yöntemini Iş mantığı katmanına ekleme

3\. adımda, DAL içindeki `ProductsTableAdapter` bir `UpdateWithTransaction` yöntemi ekledik. BLL 'ye karşılık gelen bir yöntem ekleyeceğiz. Sunum katmanı `UpdateWithTransaction` yöntemi çağırmak için doğrudan DAL 'ye çağrı yapmış olsa da bu öğreticiler, sunum katmanından DAL oluşturan katmanlı bir mimari tanımlamaya çalışır. Bu nedenle, behooves bizimle bu yaklaşıma devam etmemizi sağlar.

`ProductsBLL` sınıf dosyasını açın ve yalnızca karşılık gelen DAL yöntemine çağıran `UpdateWithTransaction` adlı bir yöntem ekleyin. `ProductsBLL`Şu anda, yeni eklediğiniz ve adım 3 ' te eklenen `DeleteProductsWithTransaction`olan `UpdateWithTransaction`iki yeni yöntem olmalıdır.

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample6.cs)]

> [!NOTE]
> Bu yöntemler, doğrudan ASP.NET Pages arka plan kod sınıflarından bu yöntemleri çağırabiletireceğiz için `ProductsBLL` sınıfındaki diğer yöntemlere atanan `DataObjectMethodAttribute` özniteliğini içermez. Bu `DataObjectMethodAttribute`, ObjectDataSource 'un veri kaynağını Yapılandır sihirbazında ve hangi sekmenin (SELECT, UPDATE, INSERT veya DELETE) altında görünmesi gerektiğini işaretlemek için kullanıldığını unutmayın. GridView, toplu iş düzenlemesi veya silme için yerleşik bir destek olmadığından, kod içermeyen bildirim yaklaşımını kullanmak yerine bu yöntemleri programlı bir şekilde çağırmamız gerekir.

## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>5\. Adım: veritabanı verilerini sunu katmanından otomatik olarak güncelleştirme

İşlemin toplu bir kayıt güncelleştirmesinde olduğu etkiyi göstermek için, bir GridView içindeki tüm ürünleri listeleyen bir kullanıcı arabirimi oluşturun ve tıklandığı zaman, ürün `CategoryID` değerleri yeniden atar. Özellikle, bazı birkaç ürüne geçerli bir `CategoryID` değeri atanarak, diğer bir deyişle mevcut olmayan bir `CategoryID` değerine atanmadığından, kategori yeniden ataması devam edecektir. `CategoryID` var olan bir `CategoryID`kategoriyle eşleşmeyen bir ürünle veritabanını güncelleştirmeye çalışarız, yabancı anahtar kısıtlaması ihlali oluşur ve bir özel durum oluşturulur. Bu örnekte, bir işlem kullanılırken, yabancı anahtar kısıtlaması ihlalinden kaynaklanan özel durum, önceki geçerli `CategoryID` değişikliklerinin geri alınmasına neden olur. Ancak, bir işlem kullanmadığınız zaman, ilk kategorilerdeki değişiklikler kalır.

`Transactions.aspx` sayfasını `BatchData` klasöründen açarak başlatın ve araç kutusundan bir GridView 'ı tasarımcı üzerine sürükleyin. `ID` `Products` ve akıllı etiketinden `ProductsDataSource`adlı yeni bir ObjectDataSource bağlayın. `ProductsBLL` sınıf s `GetProducts` yönteminden verileri çekmek için ObjectDataSource 'ı yapılandırın. Bu, salt okunurdur bir GridView olacaktır, bu nedenle GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden (yok) açılır listeleri ayarlayın ve son ' a tıklayın.

[![Şekil 5: ObjectDataSource 'ı ProductsBLL Class s GetProducts metodunu kullanacak şekilde yapılandırma](wrapping-database-modifications-within-a-transaction-cs/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image3.png)

**Şekil 5**: Şekil 5: `ProductsBLL` Class s `GetProducts` metodunu ([tam boyutlu görüntüyü görüntülemek Için tıklayın](wrapping-database-modifications-within-a-transaction-cs/_static/image4.png)) kullanmak üzere ObjectDataSource 'ı yapılandırın

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](wrapping-database-modifications-within-a-transaction-cs/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image5.png)

**Şekil 6**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinden açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](wrapping-database-modifications-within-a-transaction-cs/_static/image6.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio, ürün verileri alanları için BoundFields ve bir CheckBoxField oluşturacaktır. `ProductID`, `ProductName`, `CategoryID`ve `CategoryName` hariç tüm bu alanları kaldırın ve `ProductName` ve `CategoryName` BoundFields `HeaderText` özellikleri sırasıyla ürün ve kategori olarak yeniden adlandırın. Akıllı etikette, sayfalama etkinleştir seçeneğini işaretleyin. Bu değişiklikleri yaptıktan sonra, GridView ve ObjectDataSource 'lar bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample7.aspx)]

Sonra, GridView 'un üstüne üç düğme web denetimi ekleyin. İlk düğme s metin özelliğini kılavuz Yenile, kategorileri değiştirmek için ikinci s (Işlem Ile) ve üçüncü bir tane Kategoriler (Işlem olmadan) olacak şekilde ayarlayın.

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample8.aspx)]

Bu noktada, Visual Studio 'daki Tasarım görünümü Şekil 7 ' de gösterilen ekran görüntüsüne benzer şekilde görünmelidir.

[Sayfada bir GridView ve üç düğme web denetimi Içeren ![](wrapping-database-modifications-within-a-transaction-cs/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image7.png)

**Şekil 7**: sayfa bir GridView ve üç düğme web denetimi içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](wrapping-database-modifications-within-a-transaction-cs/_static/image8.png))

Üç düğme `Click` olayının her biri için olay işleyicileri oluşturun ve aşağıdaki kodu kullanın:

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample9.cs)]

Yenileme düğmesi s `Click` olay işleyicisi, `Products` GridView s `DataBind` metodunu çağırarak verileri GridView 'a yeniden bağlar.

İkinci olay işleyicisi, ürünleri `CategoryID` öğeleri yeniden atar ve bir işlemin şemsiye altında veritabanı güncelleştirmelerini gerçekleştirmek için BLL 'den yeni işlem yöntemini kullanır. Her ürünün `CategoryID` rastgele `ProductID`aynı değere ayarlandığını unutmayın. Bu ürünler geçerli `CategoryID` s ile eşlenecek `ProductID` değerler içerdiğinden, ilk birkaç ürün için bu işlem sorunsuz çalışacaktır. Ancak `ProductID` s çok büyük bir süre sonra başlatıldıktan sonra, `ProductID` s ve `CategoryID` s 'nin bu coarızalımesi artık geçerli değildir.

Üçüncü `Click` olay işleyicisi, ürünleri `CategoryID` öğeleri aynı şekilde güncelleştirir, ancak `ProductsTableAdapter` s varsayılan `Update` yöntemini kullanarak güncelleştirmeyi veritabanına gönderir. Bu `Update` yöntemi bir işlem içindeki komut serisini sarmaz, bu nedenle bu değişiklikler ilk karşılaşılan yabancı anahtar kısıtlaması ihlali hatası devam edecek.

Bu davranışı göstermek için bu sayfayı bir tarayıcı aracılığıyla ziyaret edin. Başlangıçta, Şekil 8 ' de gösterildiği gibi ilk veri sayfasını görmeniz gerekir. Sonra, kategorileri Değiştir (Işlem Ile) düğmesine tıklayın. Bu, geri göndermeye neden olur ve tüm ürünlerin `CategoryID` değerlerini güncelleştirmeye çalışır, ancak yabancı anahtar kısıtlaması ihlaline neden olur (bkz. Şekil 9).

[![ürünleri sayfalanabilir GridView 'da görüntülenir](wrapping-database-modifications-within-a-transaction-cs/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image9.png)

**Şekil 8**: ürünler bir sayfalanabilir GridView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](wrapping-database-modifications-within-a-transaction-cs/_static/image10.png))

[![Kategoriler bir yabancı anahtar kısıtlaması Ihlaline neden olur](wrapping-database-modifications-within-a-transaction-cs/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image11.png)

**Şekil 9**: kategorileri yeniden atama yabancı anahtar kısıtlaması ihlaline neden olur ([tam boyutlu görüntüyü görüntülemek için tıklayın](wrapping-database-modifications-within-a-transaction-cs/_static/image12.png))

Şimdi tarayıcı geri düğmesine basın ve ardından kılavuza Yenile düğmesine tıklayın. Verileri yenilemeden sonra, Şekil 8 ' de gösterildiği gibi tam olarak aynı çıktıyı görmeniz gerekir. Diğer bir deyişle, bazı `CategoryID` ürünlerden bazıları yasal değerler olarak değiştirilse ve veritabanında güncelleştirilene karşın, yabancı anahtar kısıtlaması ihlali oluştuğunda geri alınır.

Şimdi kategorileri Değiştir (Işlem olmadan) düğmesini tıklatmaya çalışın. Bu, aynı yabancı anahtar kısıtlaması ihlali hatasına neden olur (bkz. Şekil 9), ancak bu sefer `CategoryID` değerleri geçerli bir değer olarak değiştirilen ürünler geri alınmaz. Tarayıcınızın geri düğmesine ve ardından Kılavuz Yenile düğmesine basın. Şekil 10 ' da gösterildiği gibi, ilk sekiz ürünün `CategoryID` s ' i yeniden atandı. Örneğin, Şekil 8 ' de, Chang 1 ' in `CategoryID` vardı, ancak Şekil 10 ' da 2 ' ye yeniden atandı.

[![bazı ürünlerin CategoryID değerlerinin güncelleştirildiği sırada güncelleştirilmiş olması](wrapping-database-modifications-within-a-transaction-cs/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image13.png)

**Şekil 10**: bazı ürün `CategoryID` değerleri, diğerleri oluşturulmazken güncelleştirildi ([tam boyutlu görüntüyü görüntülemek için tıklayın](wrapping-database-modifications-within-a-transaction-cs/_static/image14.png))

## <a name="summary"></a>Özet

Varsayılan olarak, TableAdapter s yöntemleri yürütülen veritabanı deyimlerini bir işlemin kapsamı içinde sarmaz, ancak küçük bir çalışmalarla bir işlem oluşturacak, kaydedilecek ve geri alacak Yöntemler ekleyebiliriz. Bu öğreticide `ProductsTableAdapter` sınıfında üç tür yöntem oluşturduk: `BeginTransaction`, `CommitTransaction`ve `RollbackTransaction`. Bu yöntemlerin bir dizi veri değiştirme deyimini atomik hale getirmek için bir `try...catch` bloğuyla birlikte nasıl kullanılacağını gördük. Özellikle, sağlanan bir `ProductsDataTable`satırlarda gerekli değişiklikleri gerçekleştirmek için Batch güncelleştirme modelini kullanan `ProductsTableAdapter``UpdateWithTransaction` yöntemi oluşturduk. Ayrıca, `DeleteProductsWithTransaction` yöntemini, giriş olarak `ProductID` değerleri `List` kabul eden ve her `Delete` için DB-Direct model yöntemini çağıran BLL içindeki `ProductsBLL` sınıfına ekledik. Her iki yöntem de bir işlem oluşturarak ve sonra veri değiştirme deyimlerini bir `try...catch` bloğu içinde yürütülerek başlar. Bir özel durum oluşursa, işlem geri alınır, aksi takdirde işlenir.

5\. adım, işlem toplu iş güncelleştirmelerinin bir işlem kullanmak için ihmal edilen toplu güncelleştirmeler ile ilgili etkisini Sonraki üç öğreticide, bu öğreticide bulunan temel üzerine oluşturacağız ve toplu güncelleştirme, silme ve ekleme işlemlerini gerçekleştirmek için Kullanıcı arabirimleri oluşturacağız.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Işlemlerle veritabanı tutarlılığını sürdürme](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [SQL Server saklı yordamlarda Işlemleri yönetme](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [İşlemler kolaylaştırıldı: `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope ve DataAdapter](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [.NET ' te Oracle Database Işlemleri kullanma](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Gardner, Tepton Giesenow ve Teresa Murphy. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](batch-updating-cs.md)
