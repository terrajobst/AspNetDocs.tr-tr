---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
title: Iyimser eşzamanlılık (C#) uygulama | Microsoft Docs
author: rick-anderson
description: Birden çok kullanıcının verileri düzenlemesine izin veren bir Web uygulaması için, aynı anda iki kullanıcının aynı verileri düzenleyebilmesi riski vardır. Bu tutori...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 56e15b33-93b8-43ad-8e19-44c6647ea05c
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
msc.type: authoredcontent
ms.openlocfilehash: 3cddb0efd28249ffc5708ece39c80581d078a5a2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617155"
---
# <a name="implementing-optimistic-concurrency-c"></a>İyimser Eşzamanlılık Uygulama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_CS.exe) veya [PDF 'yi indirin](implementing-optimistic-concurrency-cs/_static/datatutorial21cs1.pdf)

> Birden çok kullanıcının verileri düzenlemesine izin veren bir Web uygulaması için, aynı anda iki kullanıcının aynı verileri düzenleyebilmesi riski vardır. Bu öğreticide, bu riski işlemek için iyimser eşzamanlılık denetimi uygulayacağız.

## <a name="introduction"></a>Giriş

Yalnızca kullanıcıların verileri görüntülemesine izin veren Web uygulamaları veya yalnızca verileri değiştirebilen tek bir kullanıcı içeren kişiler için, iki eşzamanlı kullanıcının başka bir değişikliğin yanlışlıkla üzerine yazılmasına yönelik bir tehdit yoktur. Birden çok kullanıcının verileri güncelleştirmesine veya silmesine izin veren Web uygulamaları için, bir kullanıcının başka bir eşzamanlı kullanıcı ile çakışabilecek değişiklikler söz konusu olabilir. Herhangi bir eşzamanlılık ilkesi olmadan, iki kullanıcı aynı anda tek bir kaydı düzenliyorsa, değişiklikleri en son kaydeden Kullanıcı ilk tarafından yapılan değişiklikleri geçersiz kılar.

Örneğin, Jisun ve Sam olmak üzere iki kullanıcının her ikisi de uygulamamız tarafından bir GridView denetimi aracılığıyla ürünleri güncelleştirmesine ve silmesine izin veren bir sayfayı ziyaret ettiğini düşünün. Her ikisi de aynı anda GridView 'daki Düzenle düğmesine tıklayın. Jisun ürün adını "Chai Tea" olarak değiştirir ve Güncelleştir düğmesine tıklar. Net sonuç, *Tüm* ürünlerin güncelleştirilebilir alanlarını ayarlayan veritabanına gönderilen bir `UPDATE` deyimidir (jıse yalnızca bir alan, `ProductName`). Bu noktada, veritabanında "Chai Tea," Kategori Içecek, tedarikçinin Exotic Litids ve bu ürüne yönelik değerler vardır. Ancak, Sam ekranındaki GridView, düzenlenebilir GridView satırındaki ürün adını "Chai" olarak gösterir. Jisun değişikliklerinin işlendiği birkaç saniye sonra, Sam kategoriyi koşullu olarak güncelleştirir ve Güncelleştir ' i tıklatır. Bu, ürün adını "Chai" olarak ayarlayan veritabanına gönderilen `UPDATE` bildirimine ve buna karşılık gelen Içecek kategori KIMLIĞINE `CategoryID` neden olur. Cisun 'ın ürün adı değişikliklerinin üzerine yazıldı. Şekil 1 Bu olay serisini grafik olarak gösterir.

[Iki kullanıcı aynı anda bir kaydı güncelleştirirken ![bir kullanıcının diğer s değişikliklerinin üzerine yazılmasına neden olacak değişiklikler](implementing-optimistic-concurrency-cs/_static/image2.png)](implementing-optimistic-concurrency-cs/_static/image1.png)

**Şekil 1**: Iki kullanıcı aynı anda bir kaydı güncelleştirirken, bir kullanıcı için diğer öğeleri üzerine yazılmasına yönelik değişiklikler s ([tam boyutlu görüntüyü görüntülemek için tıklatın](implementing-optimistic-concurrency-cs/_static/image3.png))

Benzer şekilde, iki Kullanıcı bir sayfayı ziyaret ederken, bir Kullanıcı başka bir kullanıcı tarafından silindiğinde bir kaydı güncelleştirme sırasında olabilir. Ya da bir Kullanıcı bir sayfayı yüklediğinde ve Sil düğmesine tıkladıklarında, başka bir kullanıcı o kaydın içeriğini değiştirmiş olabilir.

Kullanılabilen üç [eşzamanlılık denetim](http://en.wikipedia.org/wiki/Concurrency_control) stratejisi vardır:

- **Hiçbir şey yapma** -eşzamanlı kullanıcılar aynı kaydı değiştiriyorsa, son yürütmeye izin ver (varsayılan davranış)
- [**Iyimser eşzamanlılık**](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) -Şu anda eşzamanlılık çakışmaları olabileceğinden, bu tür çakışmaların büyük çoğunluğunun ortaya çıkması gerektiğini varsayın; Bu nedenle, bir çakışma ortaya çıkarsa kullanıcıyı, farklı bir kullanıcı aynı verileri değiştirdiği için yaptıkları değişikliklerin kaydedilamayacağını bildirmeniz yeterlidir.
- **Kötümser eşzamanlılık** -eşzamanlılık çakışmalarının daha fazla olduğunu ve kullanıcıların, başka bir kullanıcının eşzamanlı etkinliği nedeniyle değişiklikleri kaydedilmediğini söylemeyeceği varsayıyoruz. Bu nedenle, bir Kullanıcı bir kaydı güncelleştirmeye başladığında, Kullanıcı değişikliklerini işleene kadar diğer kullanıcıların bu kaydı düzenlemesini veya silmesini önler

Bu nedenle, tüm öğreticilerimizin varsayılan eşzamanlılık çözümleme stratejisini kullandık. Yani, son yazma kazanalım. Bu öğreticide, iyimser eşzamanlılık denetimini nasıl uygulayacağınızı inceleyeceğiz.

> [!NOTE]
> Bu öğretici serisinde Kötümser eşzamanlılık örneklerine bakmayacağız. Kötümser eşzamanlılık nadiren kullanılır, çünkü düzgün bir şekilde yeniden bağlanmazlarsa, diğer kullanıcıların veri güncelleştirmesini engelleyebilir. Örneğin, bir Kullanıcı bir kaydı düzenlenmek üzere kilitlerse ve sonra kilidi açmadan önce bırakırsa, bu kayıt, özgün kullanıcı güncelleştirmeyi döndürünceye ve tamamlanana kadar bu kaydı güncelleştiremeyecektir. Bu nedenle, Kötümser eşzamanlılık kullanıldığı durumlarda genellikle, ulaşılırsa kilidi iptal eden bir zaman aşımı vardır. Kullanıcı sipariş işlemini tamamlarken, belirli bir zaman dilimini kısa süreli olarak kilitleyen bilet satış Web siteleri, Kötümser eşzamanlılık denetimine bir örnektir.

## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>1\. Adım: Iyimser eşzamanlılık 'ın nasıl uygulandığını belirleme

İyimser eşzamanlılık denetimi, güncelleştirilmesi veya silinmekte olan kaydın güncelleştirme ya da silme işlemi başladığında yaptığı gibi aynı değerlere sahip olduğundan emin olarak çalışarak işe yarar. Örneğin, düzenlenebilir bir GridView 'da Düzenle düğmesine tıkladığınızda, kaydın değerleri veritabanından okunmalıdır ve metin kutuları ve diğer Web denetimlerinde görüntülenir. Bu orijinal değerler GridView tarafından kaydedilir. Daha sonra Kullanıcı, değişiklikleri yaptıktan ve Güncelleştir düğmesine tıkladıktan sonra, özgün değerler ve yeni değerler Iş mantığı katmanına gönderilir ve sonra veri erişim katmanına kapanır. Veri erişim katmanı, yalnızca kullanıcının düzenlemesini başlattığı orijinal değerler veritabanında hala aynı değerlerle aynıysa kaydı güncelleştirecek bir SQL ifadesini vermelidir. Şekil 2 ' de bu olay dizisi gösterilmektedir.

[Güncelleştirme veya silme Işleminin başarılı olması için ![, özgün değerler geçerli veritabanı değerlerine eşit olmalıdır](implementing-optimistic-concurrency-cs/_static/image5.png)](implementing-optimistic-concurrency-cs/_static/image4.png)

**Şekil 2**: güncelleştirme veya silme işleminin başarılı olması Için, özgün değerler geçerli veritabanı değerlerine eşit olmalıdır ([tam boyutlu görüntüyü görüntülemek için tıklatın](implementing-optimistic-concurrency-cs/_static/image6.png))

İyimser eşzamanlılığı uygulamaya yönelik çeşitli yaklaşımlar vardır (bir dizi seçeneğe kısa bir bakış için bkz. [Peter a. Bromberg](http://peterbromberg.net/)'ın [Iyimser eşzamanlılık güncelleştirme mantığı](http://www.eggheadcafe.com/articles/20050719.asp) ). ADO.NET türü belirtilmiş veri kümesi, yalnızca bir onay kutusu ile yapılandırılabilecek bir uygulama sağlar. Türü belirtilmiş veri kümesindeki bir TableAdapter için iyimser eşzamanlılık sağlamak, TableAdapter 'ın `UPDATE` ve `DELETE` deyimlerini, `WHERE` yan tümcesindeki tüm özgün değerleri bir karşılaştırmayı içerecek şekilde genişlettiğini sağlar. Örneğin, aşağıdaki `UPDATE` deyimleriyle, bir ürünün adını ve fiyatını yalnızca geçerli veritabanı değerleri GridView 'daki kayıt güncelleştirilirken başlangıçta alınan değerlere eşitse günceller. `@ProductName` ve `@UnitPrice` parametreleri Kullanıcı tarafından girilen yeni değerleri içerir, ancak Düzenle düğmesine tıklandığında `@original_ProductName` ve `@original_UnitPrice` ilk olarak GridView 'a yüklenmiş olan değerleri içerir:

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample1.sql)]

> [!NOTE]
> Bu `UPDATE` deyimleri okunabilirlik için basitleştirildi. Uygulamada, `UnitPrice` `NULL` s 'yi `UnitPrice` ve `NULL = NULL` her zaman yanlış döndürüp döndürdüğünü kontrol `WHERE` (Bunun yerine `IS NULL`kullanmanız gerekir) yan tümcesindeki denetimi daha fazla yer alabilir.

Farklı bir temel `UPDATE` deyimin kullanılmasına ek olarak, bir TableAdapter 'ı iyimser eşzamanlılık kullanacak şekilde yapılandırmak, VERITABANı doğrudan yöntemlerinin imzasını da değiştirir. İlk öğreticimize geri çekin, [*bir veri erişim katmanı oluşturun*](../introduction/creating-a-data-access-layer-cs.md), bu veritabanı doğrudan yöntemleri, bir skalar değer listesini giriş parametresi olarak kabul eden (kesin türü belirtilmiş bir DataRow veya DataTable örneği yerine). İyimser eşzamanlılık kullanılırken, VERITABANı doğrudan `Update()` ve `Delete()` yöntemleri özgün değerler için giriş parametrelerini de içerir. Ayrıca, Batch güncelleştirme modelini (skaler değerler yerine DataRow ve DataTable kabul eden `Update()` yöntemi aşırı yüklemeleri) kullanmak için BLL içindeki kod de değiştirilmelidir.

Mevcut DAL TableAdapters, iyimser eşzamanlılık kullanacak şekilde genişletmekten (BLL 'yi uyum sağlayacak şekilde değiştirmek için), bunun yerine iyimser eşzamanlılık kullanan bir `Products` TableAdapter ekleyeceğiz `NorthwindOptimisticConcurrency`adlı yeni bir türü belirtilmiş veri kümesi oluşturalım. Bunun ardından, iyimser eşzamanlılık DALı desteklemek için uygun değişikliklere sahip `ProductsOptimisticConcurrencyBLL` bir Iş mantığı katman sınıfı oluşturacağız. Bu ön hazırlıkları başlattık eklendikten sonra, ASP.NET sayfasını oluşturmak için hazırız.

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>2\. Adım: Iyimser eşzamanlılık destekleyen bir veri erişim katmanı oluşturma

Yeni bir türü belirtilmiş veri kümesi oluşturmak için, `App_Code` klasörünün içindeki `DAL` klasörüne sağ tıklayın ve `NorthwindOptimisticConcurrency`adlı yeni bir veri kümesi ekleyin. İlk öğreticide gördüğünüz gibi, bunu yapmak, türü belirtilmiş veri kümesine yeni bir TableAdapter ekleyerek TableAdapter Yapılandırma Sihirbazı ' nı otomatik olarak başlatıyor. İlk ekranda, `Web.config``NORTHWNDConnectionString` ayarını kullanarak, aynı Northwind veritabanına bağlanacak şekilde bağlanılacak veritabanını belirtmemiz istenir.

[Aynı Northwind veritabanına bağlanmak ![](implementing-optimistic-concurrency-cs/_static/image8.png)](implementing-optimistic-concurrency-cs/_static/image7.png)

**Şekil 3**: aynı Northwind veritabanına bağlanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image9.png))

Daha sonra, verilerin nasıl sorgulanabileceğini, örneğin geçici bir SQL ifadesini, yeni bir saklı yordamı veya mevcut bir saklı yordamı kullanarak yapmanız istenir. Özgün DAL 'imizde geçici SQL sorguları kullandığımızdan, burada da bu seçeneği kullanın.

[![geçici bir SQL Ifadesini kullanarak alınacak verileri belirtin](implementing-optimistic-concurrency-cs/_static/image11.png)](implementing-optimistic-concurrency-cs/_static/image10.png)

**Şekil 4**: GEÇICI bir SQL Ifadesini kullanarak alınacak verileri belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image12.png))

Aşağıdaki ekranda, ürün bilgilerini almak için kullanılacak SQL sorgusunu girin. Özgün Dalımızda `Products` TableAdapter için kullanılan aynı SQL sorgusunu kullanalım ve bu, ürünün tedarikçisiyle ve kategori adlarıyla birlikte tüm `Product` sütunlarını döndüren bir.

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample2.sql)]

[![özgün DAL 'daki ürünler TableAdapter ' dan aynı SQL sorgusunu kullanın](implementing-optimistic-concurrency-cs/_static/image14.png)](implementing-optimistic-concurrency-cs/_static/image13.png)

**Şekil 5**: özgün DAL Içinde `Products` TableAdapter 'TAN aynı SQL sorgusunu kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image15.png))

Sonraki ekrana geçmeden önce Gelişmiş Seçenekler düğmesine tıklayın. Bu TableAdapter 'ın iyimser eşzamanlılık denetimi kullanmasını sağlamak için, "iyimser eşzamanlılık kullan" onay kutusunu işaretlemeniz yeterlidir.

[iyimser eşzamanlılık denetimini etkinleştirmek ![&quot;iyimser eşzamanlılık&quot; onay kutusunu kullanın](implementing-optimistic-concurrency-cs/_static/image17.png)](implementing-optimistic-concurrency-cs/_static/image16.png)

**Şekil 6**: "Iyimser eşzamanlılık kullan" onay kutusunu Işaretleyerek Iyimser eşzamanlılık denetimini etkinleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image18.png))

Son olarak, TableAdapter 'ın her ikisi de bir DataTable doldurdukları ve DataTable döndüren veri erişim düzenlerini kullanması gerektiğini belirtir; Ayrıca, VERITABANı doğrudan yöntemlerinin oluşturulması gerektiğini de belirtir. İlk düzenimizde kullandığımız adlandırma kurallarını yansıtmak için, GetData ' dan GetProducts öğesine bir DataTable deseninin döndürdüğü yöntem adını değiştirin.

[TableAdapter 'ın tüm veri erişim desenlerini kullanmasına ![](implementing-optimistic-concurrency-cs/_static/image20.png)](implementing-optimistic-concurrency-cs/_static/image19.png)

**Şekil 7**: TableAdapter 'ın tüm veri erişim desenlerini kullanmasını sağlamak ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image21.png))

Sihirbazı tamamladıktan sonra, veri kümesi Tasarımcısı kesin türü belirtilmiş bir DataTable ve TableAdapter `Products` içerecektir. DataTable 'ın başlık çubuğuna sağ tıklayıp bağlam menüsünden Yeniden Adlandır ' ı seçerek, DataTable 'ın `Products` `ProductsOptimisticConcurrency`olarak yeniden adlandırılması için bir dakikanızı ayırın.

[Türü belirtilmiş veri kümesine bir DataTable ve TableAdapter ![eklendi](implementing-optimistic-concurrency-cs/_static/image23.png)](implementing-optimistic-concurrency-cs/_static/image22.png)

**Şekil 8**: yazılan veri kümesine bir DataTable ve TableAdapter eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image24.png))

`ProductsOptimisticConcurrency` TableAdapter (iyimser eşzamanlılık kullanan) ve Products TableAdapter (bu değil) arasındaki `UPDATE` ve `DELETE` sorguları arasındaki farkları görmek için TableAdapter 'a tıklayın ve Özellikler penceresi gidin. `DeleteCommand` ve `UpdateCommand` özellikleri ' `CommandText` alt özellikleri ' nde, DAL güncelleştirmesi veya silme ile ilgili Yöntemler çağrıldığında veritabanına gönderilen gerçek SQL sözdizimini görebilirsiniz. `ProductsOptimisticConcurrency` TableAdapter için kullanılan `DELETE` deyimidir:

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample3.sql)]

Yani, özgün DAL olan ürün TableAdapter 'ı için `DELETE` bildiri çok basittir:

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample4.sql)]

Gördüğünüz gibi, iyimser eşzamanlılık kullanan TableAdapter için `DELETE` deyimindeki `WHERE` yan tümcesi, her bir `Product` tablosunun mevcut sütun değerleri ile GridView (veya DetailsView ya da FormView) son doldurulduğu zaman arasında bir karşılaştırma içerir. `ProductID`, `ProductName`ve `Discontinued` dışındaki tüm alanlar `NULL` değerlere sahip olduğundan, `NULL` yan tümcesindeki `WHERE` değerlerini doğru bir şekilde karşılaştırmak için ek parametreler ve denetimler dahil edilir.

ASP.NET sayfamız yalnızca ürün bilgilerini güncelleştirme ve silme sağlayacak şekilde, bu öğretici için iyimser eşzamanlılık özellikli veri kümesine ek bir DataTable ekliyoruz. Ancak, yine de `ProductsOptimisticConcurrency` TableAdapter 'a `GetProductByProductID(productID)` yöntemini eklememiz gerekir.

Bunu gerçekleştirmek için, TableAdapter 'ın başlık çubuğuna sağ tıklayın (`Fill` ve `GetProducts` yöntem adlarının üzerindeki alan) ve bağlam menüsünden sorgu Ekle ' yi seçin. Bu, TableAdapter sorgu Yapılandırma Sihirbazı 'nı başlatır. TableAdapter 'ın ilk yapılandırmasında olduğu gibi, geçici bir SQL ifadesini kullanarak `GetProductByProductID(productID)` yöntemi oluşturmayı tercih edin (bkz. Şekil 4). `GetProductByProductID(productID)` yöntemi belirli bir ürünle ilgili bilgiler döndürdüğünden, bu sorgunun satırları döndüren `SELECT` bir sorgu türü olduğunu gösterir.

[![sorgu türünü, satırları döndüren &quot;bir SELECT olarak Işaretleyin&quot;](implementing-optimistic-concurrency-cs/_static/image26.png)](implementing-optimistic-concurrency-cs/_static/image25.png)

**Şekil 9**: sorgu türünü "satırları döndüren`SELECT`" olarak işaretleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image27.png))

Bir sonraki ekranda, TableAdapter 'ın varsayılan sorgusu önceden yüklenmiş olarak SQL sorgusunun kullanılması istenir. Şekil 10 ' da gösterildiği gibi, yan tümce `WHERE ProductID = @ProductID`dahil etmek için mevcut sorguyu açın.

[![belirli bir ürün kaydını döndürmek için önceden yüklenmiş sorguya bir WHERE yan tümcesi ekleyin](implementing-optimistic-concurrency-cs/_static/image29.png)](implementing-optimistic-concurrency-cs/_static/image28.png)

**Şekil 10**: belirli bir ürün kaydını döndürmek Için önceden yüklenmiş sorguya bir `WHERE` yan tümcesi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image30.png))

Son olarak, oluşturulan yöntem adlarını `FillByProductID` ve `GetProductByProductID`olarak değiştirin.

[![, bu yöntemleri Fillbyproductıd ve GetProductByProductID olarak yeniden adlandırın](implementing-optimistic-concurrency-cs/_static/image32.png)](implementing-optimistic-concurrency-cs/_static/image31.png)

**Şekil 11**: yöntemleri `FillByProductID` ve `GetProductByProductID` olarak yeniden adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image33.png))

Bu sihirbaz tamamlandığına göre TableAdapter artık verileri almak için iki yöntem içerir: `GetProducts()`, *Tüm* ürünleri döndürür; ve, belirtilen ürünü döndüren `GetProductByProductID(productID)`.

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>3\. Adım: Iyimser eşzamanlılık özellikli DAL için Iş mantığı katmanı oluşturma

Mevcut `ProductsBLL` sınıfımızın hem Batch Update hem de DB Direct desenlerini kullanma örnekleri vardır. `AddProduct` yöntemi ve `UpdateProduct` aşırı yüklemeleri her ikisi de Batch güncelleştirme modelini kullanarak, bir `ProductRow` örneğini TableAdapter Update yöntemine geçirerek kullanır. Diğer taraftan `DeleteProduct` yöntemi, TableAdapter 'ın `Delete(productID)` yöntemini çağırarak VERITABANı doğrudan modelini kullanır.

Yeni `ProductsOptimisticConcurrency` TableAdapter ile, VERITABANı doğrudan yöntemleri artık özgün değerlerin de geçirilmesini gerektirir. Örneğin `Delete` yöntemi artık on giriş parametresi beklemektedir: özgün `ProductID`, `ProductName`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`ve `Discontinued`. Veritabanına gönderilen `DELETE` deyimin `WHERE` yan tümcesindeki bu ek giriş parametrelerinin değerlerini kullanır, yalnızca veritabanının geçerli değerleri özgün olanlara eşleniyorsa belirtilen kaydı silinir.

TableAdapter 'ın Batch güncelleştirme düzeninde kullanılan `Update` yöntemi için yöntem imzası değişmediğinden, özgün ve yeni değerleri kaydetmek için gereken kod. Bu nedenle, mevcut `ProductsBLL` sınıfımızla iyimser eşzamanlılık özellikli DAL kullanımını denemek yerine yeni DAL ile çalışmaya yönelik yeni bir Iş mantığı katman sınıfı oluşturalım.

`App_Code` klasörü içindeki `BLL` klasöre `ProductsOptimisticConcurrencyBLL` adlı bir sınıf ekleyin.

![ProductsOptimisticConcurrencyBLL sınıfını BLL klasörüne ekleme](implementing-optimistic-concurrency-cs/_static/image34.png)

**Şekil 12**: `ProductsOptimisticConcurrencyBLL` sınıfını BLL klasörüne ekleme

Sonra, `ProductsOptimisticConcurrencyBLL` sınıfına aşağıdaki kodu ekleyin:

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample5.cs)]

Sınıf bildiriminin başlangıcı üzerindeki using `NorthwindOptimisticConcurrencyTableAdapters` ifadesini aklınızda edin. `NorthwindOptimisticConcurrencyTableAdapters` ad alanı, DAL yöntemlerini sağlayan `ProductsOptimisticConcurrencyTableAdapter` sınıfını içerir. Ayrıca, Sınıf bildiriminden önce, Visual Studio 'Yu ObjectDataSource sihirbazının açılan listesine bu sınıfı dahil etmek için yönlendiren `System.ComponentModel.DataObject` özniteliğini bulacaksınız.

`ProductsOptimisticConcurrencyBLL``Adapter` özelliği, `ProductsOptimisticConcurrencyTableAdapter` sınıfının bir örneğine hızlı erişim sağlar ve orijinal BLL sınıflarımızda (`ProductsBLL`, `CategoriesBLL`, vb.) kullanılan kalıbı izler. Son olarak, `GetProducts()` yöntemi yalnızca DAL `GetProducts()` yöntemine çağrı ve veritabanındaki her ürün kaydı için bir `ProductsOptimisticConcurrencyRow` örneğiyle doldurulmuş bir `ProductsOptimisticConcurrencyDataTable` nesnesi döndürüyor.

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>Iyimser eşzamanlılık ile VERITABANı doğrudan modelini kullanarak bir ürünü silme

İyimser eşzamanlılık kullanan bir DAL için VERITABANı doğrudan modelini kullanırken, yöntemlerin yeni ve özgün değerleri geçirilmesi gerekir. Silme için yeni değer yoktur, bu nedenle yalnızca özgün değerler geçirilmesi gerekir. BLL 'de, tüm özgün parametreleri giriş parametresi olarak kabul etmemiz gerekir. `ProductsOptimisticConcurrencyBLL` sınıfında `DeleteProduct` yöntemine DB Direct metodunu kullanalım. Bu, bu yöntemin tüm on ürün verileri alanlarını giriş parametreleri olarak yapması ve bunları aşağıdaki kodda gösterildiği gibi DAL 'e iletmesinin gerektiği anlamına gelir:

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample6.cs)]

Özgün değerler-GridView 'a (veya DetailsView ya da FormView) en son yüklenen değerler, Kullanıcı Sil düğmesine tıkladığında veritabanındaki değerlerden farklıysa `WHERE` yan tümcesi hiçbir veritabanı kaydıyla eşleşmez ve hiçbir kayıt etkilenmez. Bu nedenle, TableAdapter 'ın `Delete` yöntemi `0` döndürecek ve BLL 'nin `DeleteProduct` yöntemi `false`döndürecek.

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>Toplu güncelleştirme modelini Iyimser eşzamanlılık ile kullanarak bir ürünü güncelleştirme

Daha önce belirtildiği gibi, toplu güncelleştirme deseninin `Update` yöntemi, iyimser eşzamanlılık kullanılıp kullanılmadığından bağımsız olarak aynı yöntem imzasına sahiptir. Yani `Update` yöntemi bir DataRow, bir DataRow dizisi, bir DataTable veya türü belirtilmiş veri kümesi bekler. Özgün değerleri belirtmek için ek giriş parametresi yoktur. DataTable, DataRow 'lar için özgün ve değiştirilmiş değerleri takip ettiğinden, bu mümkündür. DAL `UPDATE` ifadesini yaparken, `@original_ColumnName` parametreleri DataRow 'ın özgün değerleriyle doldurulur, ancak `@ColumnName` parametreleri DataRow tarafından değiştirilen değerlerle doldurulur.

`ProductsBLL` sınıfında (orijinal, iyimser eşzamanlılık olmayan eşzamanlılık DAL kullanır) ürün bilgilerini güncelleştirmek için Batch güncelleştirme modelini kullanırken, kodumuz aşağıdaki olay sırasını gerçekleştirir:

1. TableAdapter 'ın `GetProductByProductID(productID)` metodunu kullanarak geçerli veritabanı ürün bilgilerini bir `ProductRow` örneğine okuyun
2. 1\. adımdaki yeni değerleri `ProductRow` örneğine atayın
3. TableAdapter 'ın `Update` yöntemini çağırın, `ProductRow` örneğini geçirerek

Ancak, adım 1 ' de doldurulmuş `ProductRow`, doğrudan veritabanından doldurulduğundan, DataRow tarafından kullanılan özgün değerler veritabanında mevcut olan ve Düzen işleminin başlangıcında GridView 'a bağlanılanlar dışında, bu adım dizisi, iyimser eşzamanlılık 'yi doğru şekilde desteklemez. Bunun yerine, iyimser eşzamanlılık özellikli bir DAL kullanırken aşağıdaki adımları kullanmak için `UpdateProduct` yöntemi yüklerini değiştirmemiz gerekir:

1. TableAdapter 'ın `GetProductByProductID(productID)` metodunu kullanarak geçerli veritabanı ürün bilgilerini bir `ProductsOptimisticConcurrencyRow` örneğine okuyun
2. *Özgün* değerleri 1. adımdaki `ProductsOptimisticConcurrencyRow` örneğine atayın
3. `ProductsOptimisticConcurrencyRow` örneğinin `AcceptChanges()` yöntemini çağırın, bu, DataRow öğesine geçerli değerlerinin "orijinal" olduğunu bildirir
4. *Yeni* değerleri `ProductsOptimisticConcurrencyRow` örneğine ata
5. TableAdapter 'ın `Update` yöntemini çağırın, `ProductsOptimisticConcurrencyRow` örneğini geçirerek

1\. adım, belirtilen ürün kaydı için geçerli veritabanı değerlerinin tümünde okur. Bu `UpdateProduct` adım, *Tüm* ürün sütunlarını (Bu değerlerin 2. adımdaki üzerine yazıldığı gibi) güncelleştiren, ancak sütun değerlerinin yalnızca bir alt kümesinin giriş parametresi olarak geçirildiği bu aşırı yüklemeler için gereklidir. Özgün değerler `ProductsOptimisticConcurrencyRow` örneğine atandıktan sonra, `AcceptChanges()` yöntemi çağrılır, bu, geçerli DataRow değerlerini `UPDATE` deyimindeki `@original_ColumnName` parametrelerinde kullanılacak orijinal değerler olarak işaretler. Ardından, yeni parametre değerleri `ProductsOptimisticConcurrencyRow` atanır ve son olarak, `Update` yöntemi çağırılır, DataRow içinde geçer.

Aşağıdaki kod, tüm ürün verileri alanlarını giriş parametresi olarak kabul eden `UpdateProduct` aşırı yüklemeyi gösterir. Burada gösterilmemiş olsa da, bu öğreticide bulunan `ProductsOptimisticConcurrencyBLL` sınıfı, yalnızca ürünün adını ve fiyatını giriş parametresi olarak kabul eden bir `UpdateProduct` aşırı yüklemesi içerir.

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample7.cs)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>4\. Adım: özgün ve yeni değerleri ASP.NET sayfasından BLL yöntemlerine geçirme

DAL ve BLL ile birlikte her şey, sistemde yerleşik olarak bulunan iyimser eşzamanlılık mantığını kullanan bir ASP.NET sayfası oluşturmaktır. Özellikle, veri Web denetimi (GridView, DetailsView veya FormView) orijinal değerlerini hatırlamaları gerekir ve ObjectDataSource, her iki değer kümesini de Iş mantığı katmanına iletmelidir. Ayrıca, ASP.NET sayfası eşzamanlılık ihlallerini düzgün şekilde işleyecek şekilde yapılandırılmalıdır.

`OptimisticConcurrency.aspx` sayfasını `EditInsertDelete` klasöründen açıp tasarımcıya bir GridView ekleyerek `ID` özelliğini `ProductsGrid`olarak ayarlayarak başlayın. GridView 'un akıllı etiketinden `ProductsOptimisticConcurrencyDataSource`adlı yeni bir ObjectDataSource oluşturmayı tercih edin. Bu ObjectDataSource 'un iyimser eşzamanlılık destekleyen DAL kullanmasını istiyoruz, `ProductsOptimisticConcurrencyBLL` nesnesini kullanacak şekilde yapılandırın.

[![ObjectDataSource, ProductsOptimisticConcurrencyBLL nesnesini kullanır](implementing-optimistic-concurrency-cs/_static/image36.png)](implementing-optimistic-concurrency-cs/_static/image35.png)

**Şekil 13**: ObjectDataSource 'un `ProductsOptimisticConcurrencyBLL` nesnesini kullanmasını sağlamak ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image37.png))

Sihirbazdaki açılan listelerden `GetProducts`, `UpdateProduct`ve `DeleteProduct` yöntemlerini seçin. UpdateProduct yöntemi için, ürünün tüm veri alanlarını kabul eden aşırı yüklemeyi kullanın.

## <a name="configuring-the-objectdatasource-controls-properties"></a>ObjectDataSource denetiminin özelliklerini yapılandırma

Sihirbazı tamamladıktan sonra, ObjectDataSource 'un bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample8.aspx)]

Gördüğünüz gibi `DeleteParameters` koleksiyonu, `ProductsOptimisticConcurrencyBLL` sınıfının `DeleteProduct` yöntemindeki her on giriş parametresi için bir `Parameter` örneği içerir. Benzer şekilde, `UpdateParameters` koleksiyonu `UpdateProduct`giriş parametrelerinin her biri için bir `Parameter` örneği içerir.

Veri değişikliğini içeren önceki öğreticiler için, bu özellik BLL yönteminin, eski (veya orijinal) değerlerinin ve yeni değerlerin geçirilmesini beklediğini gösterdiği için bu noktada ObjectDataSource 'un `OldValuesParameterFormatString` özelliğini kaldırdık. Ayrıca, bu özellik değeri özgün değerler için giriş parametresi adlarını belirtir. Özgün değerleri BLL 'ye geçirdiğimiz için, bu *özelliği kaldırmayın.*

> [!NOTE]
> `OldValuesParameterFormatString` özelliğinin değeri, özgün değerleri bekleyen BLL içindeki giriş parametresi adlarıyla eşleşmelidir. Bu parametreleri `original_productName`, `original_supplierID`vb. adlandırdığımız için `OldValuesParameterFormatString` özellik değerini `original_{0}`olarak bırakabilirsiniz. Ancak, BLL yöntemlerinin giriş parametrelerinin `old_productName`, `old_supplierID`vb. gibi adları varsa `OldValuesParameterFormatString` özelliğini `old_{0}`olarak güncelleştirmeniz gerekir.

ObjectDataSource 'un özgün değerleri BLL yöntemlerine doğru şekilde geçirmesi için yapılması gereken bir son özellik ayarı vardır. ObjectDataSource, [iki değerden birine](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx)atanabilecek bir [ConflictDetection özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx) sahiptir:

- `OverwriteChanges`-varsayılan değer; özgün değerleri BLL metotlarının orijinal giriş parametrelerine göndermez
- `CompareAllValues`-özgün değerleri BLL yöntemlerine gönderir; iyimser eşzamanlılık kullanılırken bu seçeneği belirleyin

`ConflictDetection` özelliğini `CompareAllValues`olarak ayarlamak için bir dakikanızı ayırın.

## <a name="configuring-the-gridviews-properties-and-fields"></a>GridView 'un özelliklerini ve alanlarını yapılandırma

ObjectDataSource özelliklerinin düzgün şekilde yapılandırıldığından, GridView 'u ayarlamaya dikkat çekelim. İlk olarak, GridView 'un Düzenle ve silmeyi desteklemesini istediğinizden, GridView 'un akıllı etiketindeki Düzenle 'yi etkinleştir ve onay kutularını silmeyi etkinleştir ' e tıklayın. Bu, `ShowEditButton` ve `ShowDeleteButton` her ikisi de `true`olarak ayarlanan bir CommandField ekler.

`ProductsOptimisticConcurrencyDataSource` ObjectDataSource 'a bağlandığında, GridView her bir ürünün veri alanı için bir alan içerir. Böyle bir GridView düzenlenebilir olsa da, Kullanıcı deneyimi herhangi bir şeydir ancak kabul edilebilir. `CategoryID` ve `SupplierID` BoundFields, Kullanıcı tarafından KIMLIK numarası olarak uygun kategori ve tedarikçiyi girmesini gerektiren metin kutuları olarak işlenir. Sayısal alanlar için biçimlendirme olmaz ve ürün adının sağlandığından ve birim fiyatının, stoktaki birimlerin, siparişteki birimlerin ve yeniden sipariş düzeyi değerlerinin her ikisi de doğru sayısal değerler olduğundan ve daha büyük veya eşit olduğundan emin olmak için doğrulama denetimi yoktur sıfır olarak.

*Düzen denetimleri ekleme ve arabirim ekleme* ve *veri değişikliği arabirimi* öğreticilerini özelleştirme konusunda anlatıldığı gibi, Kullanıcı arabirimi, Boundfields alanları templatefields ile değiştirilerek özelleştirilebilir. Bu GridView ve Editing arabirimini aşağıdaki yollarla değiştirdim:

- `ProductID`, `SupplierName`ve `CategoryName` BoundFields kaldırıldı
- BoundField `ProductName` bir TemplateField 'a dönüştürüldü ve bir RequiredFieldValidation denetimi ekledi.
- `CategoryID` ve `SupplierID` BoundFields alanlarını TemplateFields 'e dönüştürüyordu ve metin kutuları yerine DropDownLists kullanmak için Düzenle arabirimini ayarladı. Bu TemplateFields ' `ItemTemplates`, `CategoryName` ve `SupplierName` veri alanları görüntülenir.
- `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`ve `ReorderLevel` BoundFields alanlarını TemplateFields 'e dönüştürülüp CompareValidator denetimleri ekledi.

Önceki öğreticilerde bu görevleri nasıl gerçekleştireceğinizi zaten incelediğimiz için, son bildirime dayalı sözdizimini burada listem ve uygulamayı uygulama olarak bırakmalısınız.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample9.aspx)]

Tam olarak çalışan bir örneğe sahip olmanın çok yakınlıyız. Ancak, bir yandan sorunları ortaya çıkarabilir ve sorun yaşalacak birkaç alt tzellikleri vardır. Buna ek olarak, bir eşzamanlılık ihlali oluştuğunda kullanıcıyı uyaran bir arabirim hala gereklidir.

> [!NOTE]
> Bir veri Web denetiminin özgün değerleri ObjectDataSource 'a doğru bir şekilde geçirmesi için (daha sonra BLL 'ye geçirilir), GridView 'un `EnableViewState` özelliğinin `true` (varsayılan) olarak ayarlanması çok önemlidir. Görünüm durumunu devre dışı bırakırsanız, geri gönderme sırasında özgün değerler kaybedilir.

## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>Doğru özgün değerleri ObjectDataSource 'a geçirme

GridView 'un yapılandırıldığı şekilde birkaç sorun vardır. ObjectDataSource 'un `ConflictDetection` özelliği `CompareAllValues` (bizde olduğu gibi) olarak ayarlandıysa, ObjectDataSource 'un `Update()` veya `Delete()` yöntemleri GridView (veya DetailsView ya da FormView) tarafından çağrıldığında, ObjectDataSource GridView 'in özgün değerlerini uygun `Parameter` örneklerine kopyalamaya çalışır. Bu işlemin grafik gösterimi için Şekil 2 ' ye geri bakın.

Özellikle, GridView 'un özgün değerleri, veriler GridView 'a her bağlandığında iki yönlü veri bağlama deyimlerine atanır. Bu nedenle, gerekli orijinal değerlerin hepsi iki yönlü veri bağlama aracılığıyla yakalandığından ve dönüştürülebilir bir biçimde sağlandıklarından önemlidir.

Bunun ne kadar önemli olduğunu görmek için, sayfamızı tarayıcıda ziyaret etmek için bir dakikanızı ayırın. GridView, beklendiği gibi her bir ürünü, en soldaki sütundaki Düzenle ve Sil düğmesiyle listeler.

[![ürünlerin bir GridView içinde listelenmesi](implementing-optimistic-concurrency-cs/_static/image39.png)](implementing-optimistic-concurrency-cs/_static/image38.png)

**Şekil 14**: Ürünler GridView 'da listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image40.png))

Herhangi bir ürün için Sil düğmesine tıklarsanız bir `FormatException` oluşturulur.

[bir FormatException içinde herhangi bir ürün sonucunu silmeye çalışırken ![](implementing-optimistic-concurrency-cs/_static/image42.png)](implementing-optimistic-concurrency-cs/_static/image41.png)

**Şekil 15**: bir `FormatException` herhangi bir ürün sonucunu silmeye çalışırken ([tam boyutlu görüntüyü görüntülemek için tıklatın](implementing-optimistic-concurrency-cs/_static/image43.png))

`FormatException`, ObjectDataSource özgün `UnitPrice` değerinde okumayı denediğinde tetiklenir. `ItemTemplate` bir para birimi (`<%# Bind("UnitPrice", "{0:C}") %>`) olarak biçimlendirilen `UnitPrice` sahip olduğundan, $19,95 gibi bir para birimi simgesi içerir. `FormatException`, ObjectDataSource bu dizeyi bir `decimal`dönüştürmeye çalıştığı için oluşur. Bu sorunu aşmak için birkaç seçenek vardır:

- `ItemTemplate`para birimi biçimlendirmesini kaldırın. Diğer bir deyişle, `<%# Bind("UnitPrice", "{0:C}") %>`kullanmak yerine `<%# Bind("UnitPrice") %>`kullanmanız yeterlidir. Bunun aşağı tarafı, fiyatın artık biçimlendirilmemesi durumunda olur.
- `ItemTemplate`bir para birimi olarak biçimlendirilen `UnitPrice` görüntüleyin, ancak bunu gerçekleştirmek için `Eval` anahtar sözcüğünü kullanın. `Eval` tek yönlü veri bağlamayı gerçekleştirdiğini hatırlayın. Yine de özgün değerler için `UnitPrice` değeri sağlamanız gerekir, bu nedenle `ItemTemplate`iki yönlü bir veri bağlama bildirimine ihtiyacımız var, ancak bu, `Visible` özelliği `false`olarak ayarlanmış bir etiket Web denetimine yerleştirilebilecek. ItemTemplate 'te aşağıdaki biçimlendirmeyi kullanabiliriz:

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample10.aspx)]

- `<%# Bind("UnitPrice") %>`kullanarak `ItemTemplate`para birimi biçimlendirmesini kaldırın. GridView 'ın `RowDataBound` olay işleyicisinde, `UnitPrice` değerinin görüntülendiği etiketli Web denetimine programlı bir şekilde erişin ve `Text` özelliğini biçimlendirilen sürüm olarak ayarlayın.
- `UnitPrice` para birimi olarak biçimlendirilen şekilde bırakın. GridView 'un `RowDeleting` olay işleyicisinde, var olan özgün `UnitPrice` değerini ($19,95) `Decimal.Parse`kullanarak gerçek bir ondalık değer ile değiştirin. [*Bir ASP.NET sayfa öğreticisindeki BLL ve dal düzeyi özel durumları işleme*](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) `RowUpdating` olay işleyicisinde benzer bir şeyi nasıl gerçekleştireceğinizi gördük.

Örneğimin, `Text` özelliği biçimlendirilmemiş `UnitPrice` değerine göre iki yönlü veri olan bir gizli etiket Web denetimi eklemek için ikinci yaklaşımla devam ediyorum.

Bu sorunu çözdikten sonra, herhangi bir ürün için Sil düğmesine tıklayarak yeniden deneyin. Bu kez, ObjectDataSource BLL 'nin `UpdateProduct` yöntemini çağırmayı denediğinde bir `InvalidOperationException` alırsınız.

[![ObjectDataSource, göndermek Istediği giriş parametrelerine sahip bir yöntem bulamıyor](implementing-optimistic-concurrency-cs/_static/image45.png)](implementing-optimistic-concurrency-cs/_static/image44.png)

**Şekil 16**: ObjectDataSource, göndermek Istediği giriş parametrelerine sahip bir yöntem bulamıyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image46.png))

Özel durumun iletisine baktığınızda, ObjectDataSource 'un `original_CategoryName` ve `original_SupplierName` giriş parametrelerini içeren bir BLL `DeleteProduct` yöntemi çağırmak istemektedir. Bunun nedeni, `CategoryID` ve `SupplierID` TemplateFields için `ItemTemplate`, şu anda `CategoryName` ve `SupplierName` veri alanlarıyla iki yönlü bağlama deyimleri içereceğinden oluşur. Bunun yerine, `CategoryID` ve `SupplierID` veri alanlarıyla `Bind` deyimleri dahil etmemiz gerekir. Bunu gerçekleştirmek için, var olan bind deyimlerini `Eval` deyimleriyle değiştirin ve ardından `Text` özellikleri `CategoryID` ve `SupplierID` veri alanlarına bağlı olan gizli etiket denetimleri aşağıda gösterildiği gibi iki yönlü veri bağlamayı kullanarak ekleyin:

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample11.aspx)]

Bu değişikliklerle artık ürün bilgilerini başarıyla silip düzenleyebiliyoruz! 5\. adımda eşzamanlılık ihlallerinin algılanmakta olduğunu doğrulama bölümüne bakacağız. Ancak şimdilik, tek bir kullanıcı için güncelleştirme ve silme işlemlerinin beklendiği gibi çalıştığından emin olmak için birkaç kaydı güncelleştirmeyi ve silmeyi denemek üzere birkaç dakikanızı yararlanın.

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>5\. Adım: Iyimser eşzamanlılık desteğini test etme

Eşzamanlılık ihlallerinin algılanmakta olduğunu doğrulamak için (verilerin üzerine yazılmakta olması yerine), bu sayfada iki tarayıcı penceresi açmanız gerekir. Her iki tarayıcı örneğinde de, Chai için Düzenle düğmesine tıklayın. Ardından, tarayıcıların yalnızca birinde adı "Chai Tea" olarak değiştirin ve Güncelleştir ' e tıklayın. Güncelleştirme başarılı olmalıdır ve yeni ürün adı olarak "Chai Tea" ile GridView 'u önceden düzenlenen durumuna döndürmelidir.

Öte yandan, diğer tarayıcı pencere örneğinde, ürün adı metin kutusu hala "Chai" gösterir. Bu ikinci tarayıcı penceresinde `UnitPrice` `25.00`güncelleştirin. İyimser eşzamanlılık desteği olmadan ikinci tarayıcı örneğinde Güncelleştir ' e tıklamak, ürün adını "Chai" olarak değiştirecek ve böylece ilk tarayıcı örneği tarafından yapılan değişikliklerin üzerine yazılmasına neden olur. Ancak, iyimser eşzamanlılık istihdam ile ikinci tarayıcı örneğindeki Güncelleştir düğmesine tıklamak bir [DBConcurrencyException](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx)ile sonuçlanır.

[![bir eşzamanlılık Ihlali algılandığında, bir DBConcurrencyException oluşturulur](implementing-optimistic-concurrency-cs/_static/image48.png)](implementing-optimistic-concurrency-cs/_static/image47.png)

**Şekil 17**: bir eşzamanlılık ihlali algılandığında, bir `DBConcurrencyException` oluşturulur ([tam boyutlu görüntüyü görüntülemek için tıklatın](implementing-optimistic-concurrency-cs/_static/image49.png))

`DBConcurrencyException` yalnızca DAL toplu iş güncelleştirme deseninin kullanıldığı durumlarda oluşturulur. VERITABANı doğrudan stili özel durum oluşturmaz, yalnızca hiçbir satırın etkilenmediğini belirtir. Bunu göstermek için, hem tarayıcı örneklerinin hem de kendi düzenlenme durumuna döndürün. Ardından, ilk tarayıcı örneğinde Düzenle düğmesine tıklayın ve ürün adını "Chai Tea" iken "Chai" olarak değiştirin ve Güncelleştir ' e tıklayın. İkinci tarayıcı penceresinde, Chai için Sil düğmesine tıklayın.

Sil ' e tıklandıktan sonra, sayfa geri gönderilerek, GridView, ObjectDataSource 'un `Delete()` yöntemini çağırır ve ObjectDataSource, `ProductsOptimisticConcurrencyBLL` sınıfının `DeleteProduct` yöntemine çağırarak özgün değerleri de geçirir. İkinci tarayıcı örneği için özgün `ProductName` değeri, veritabanındaki geçerli `ProductName` değeriyle eşleşmeyen "Chai Tea" dır. Bu nedenle, veritabanında `WHERE` yan tümcesinin karşıladığından bir kayıt bulunmadığından veritabanına verilen `DELETE` deyimi sıfır satırı etkiler. `DeleteProduct` yöntemi `false` döndürür ve ObjectDataSource 'un verileri GridView 'a yeniden bağlanır.

Son kullanıcının perspektifinden, ikinci tarayıcı penceresinde Chai Tea için Sil düğmesine tıkladığınızda, ekranın Flash 'a ve geri alındıktan sonra, artık "Chai" olarak listelense de (ilk tarayıcı tarafından yapılan ürün adı değişikliği). örnek). Kullanıcı Sil düğmesine yeniden tıkladığında, GridView 'un özgün `ProductName` değeri ("Chai") artık veritabanındaki değerle eşleştirirken silme işlemi başarılı olur.

Her iki durumda da, Kullanıcı deneyimi ideal bir deneyimdir. Batch güncelleştirme modelini kullanırken `DBConcurrencyException` özel durumunun Nitty-Gritty ayrıntılarını kullanıcıya göstermek istemezsiniz. Ve VERITABANı doğrudan düzeninin kullanılması, Kullanıcı komutu başarısız olduğu için biraz kafa karıştırıcı, ancak neden kesin bir belirtilemedi.

Bu iki sorunu gidermek için, sayfada bir güncelleştirme ya da silmenin neden başarısız olduğuna ilişkin bir açıklama sağlayan başlık Web denetimleri oluşturuyoruz. Batch güncelleştirme düzeninde, GridView 'un düzey sonrası olay işleyicide bir `DBConcurrencyException` özel durumun oluşup oluşmadığını tespit edebilir ve uyarı etiketini gerektiği gibi görüntüleyebilirsiniz. VERITABANı doğrudan yönteminde, BLL yönteminin dönüş değerini inceleyebilirsiniz (bir satır etkilenirse `true`, aksi takdirde `false`) ve gerektiğinde bilgilendirici bir ileti görüntüleyebilirsiniz.

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>6\. Adım: bilgilendirici Iletiler ekleme ve bunları eşzamanlılık Ihlalinin Yüzinde görüntüleme

Bir eşzamanlılık ihlali gerçekleştiğinde, bu davranış, DAL 'ın Batch güncelleştirmesi veya DB doğrudan deseninin kullanılıp kullanılmadığına bağlıdır. Öğreticimiz, güncelleştirme için kullanılan Batch güncelleştirme düzeni ve silme için kullanılan VERITABANı doğrudan deseni ile her iki deseni de kullanmaktadır. Başlamak için sayfamıza, verileri silmeye veya güncelleştirmeye çalışırken bir eşzamanlılık ihlalinin oluştuğunu açıklayan iki etiketli Web denetimi ekleyelim. Etiket denetiminin `Visible` ve `EnableViewState` özelliklerini `false`; olarak ayarlayın. Bu, `Visible` özelliğinin program aracılığıyla `true`olarak ayarlandığı belirli sayfa ziyaretlerinin dışında, bu kişilerin her sayfada gizli olmasına neden olur.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample12.aspx)]

`Visible`, `EnabledViewState`ve `Text` özelliklerini ayarlamaya ek olarak, `CssClass` özelliğini `Warning`olarak ayarlıyorum, bu da etiketin büyük, kırmızı, italik ve kalın yazı tipinde görüntülenmesine neden olur. Bu CSS `Warning` sınıfı tanımlanmış ve stillerle eklendi. css, *ekleme, güncelleştirme ve silme öğreticisi Ile Ilişkili olayları İnceleme* .

Bu Etiketler eklendikten sonra, Visual Studio 'daki tasarımcı Şekil 18 ' e benzer görünmelidir.

[Sayfaya ![Iki Etiket denetimi eklendi](implementing-optimistic-concurrency-cs/_static/image51.png)](implementing-optimistic-concurrency-cs/_static/image50.png)

**Şekil 18**: sayfaya Iki Etiket denetimi eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image52.png))

Bu etiketli Web denetimleriyle birlikte, bir eşzamanlılık ihlalinin ne zaman gerçekleştiğini belirleme hazırız. bu noktada, uygun etiketin `Visible` özelliği `true`olarak ayarlanabilir ve bilgilendirici ileti görüntülenir.

## <a name="handling-concurrency-violations-when-updating"></a>Güncelleştirme sırasında eşzamanlılık Ihlallerini işleme

Toplu güncelleştirme modelini kullanırken eşzamanlılık ihlallerinin nasıl işleneceğini göz atalım. Batch Update düzenine sahip bu tür ihlaller `DBConcurrencyException` bir özel durumun oluşturulmasına neden olduğundan, güncelleştirme işlemi sırasında bir `DBConcurrencyException` özel durumun oluşup oluşmadığını öğrenmek için ASP.NET sayfamıza kod eklememiz gerekir. Bu durumda, başka bir kullanıcı kayıt düzenlendikleri sırada ve Güncelleştir düğmesine tıklandığı zaman arasında aynı verileri değiştirdiği için, kullanıcının yaptıkları değişiklikleri kaydetmediğini açıklayan bir ileti görüntüleriz.

*Bir ASP.NET sayfa öğreticisindeki BLL ve dal düzeyi özel durumları işleme* gördük. bu tür özel durumlar, veri Web denetiminin düzey sonrası olay işleyicilerinde tespit edilebilir ve gizlenebilir. Bu nedenle, bir `DBConcurrencyException` özel durumunun oluşturulmuş olduğunu denetleyen GridView 'un `RowUpdated` olayı için bir olay işleyicisi oluşturuyoruz. Bu olay işleyicisine aşağıdaki olay işleyicisi kodunda gösterildiği gibi, güncelleştirme işlemi sırasında oluşturulan tüm özel durumlar için bir başvuru geçirilir:

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample13.cs)]

`DBConcurrencyException` bir özel durum durumunda bu olay işleyicisi `UpdateConflictMessage` etiketi denetimini görüntüler ve özel durumun işlendiğini gösterir. Bu kod yerinde olduğunda, bir kaydı güncelleştirirken bir eşzamanlılık ihlali meydana geldiğinde, başka bir kullanıcının değişikliklerinin aynı anda üzerine yazıldıklarından, kullanıcının değişiklikleri kaybedilir. Özellikle GridView, önceden düzenlenen durumuna döndürülür ve geçerli veritabanı verilerine bağlanır. Bu, GridView satırını daha önce görünmeyen diğer kullanıcının değişiklikleriyle güncelleştirir. Ayrıca, `UpdateConflictMessage` etiket denetimi kullanıcıya ne olduğunu açıklayacak. Bu olay sırası Şekil 19 ' da ayrıntılı olarak açıklanmıştır.

[![bir Kullanıcı güncelleştirmelerinin bir eşzamanlılık Ihlali durumunda kaybolması](implementing-optimistic-concurrency-cs/_static/image54.png)](implementing-optimistic-concurrency-cs/_static/image53.png)

**Şekil 19**: bir Kullanıcı güncelleştirmelerinin bir eşzamanlılık Ihlali tarafında kaybolması ([tam boyutlu görüntüyü görüntülemek için tıklatın](implementing-optimistic-concurrency-cs/_static/image55.png))

> [!NOTE]
> Alternatif olarak, GridView 'u önceden düzenlenen durumuna döndürmek yerine, geçirilen `GridViewUpdatedEventArgs` nesnesinin `KeepInEditMode` özelliğini true olarak ayarlayarak GridView 'u kendi düzen durumunda bırakabiliriz. Ancak, bu yaklaşımı kullanırsanız, diğer kullanıcının değerlerinin düzen arabirimine yüklenmesi için verileri GridView 'a yeniden bağlamak (`DataBind()` yöntemini çağırarak) gerekir. Bu öğreticiyle indirilebileceğiniz kod, `RowUpdated` olay işleyicisindeki bu iki kod satırını açıklama satırı ' na sahiptir; bir eşzamanlılık ihlalinden sonra GridView 'un düzenleme modunda kalmasını sağlamak için bu kod satırlarının açıklamasını basitçe kaldırın.

## <a name="responding-to-concurrency-violations-when-deleting"></a>Silinirken eşzamanlılık Ihlallerine yanıt verme

VERITABANı doğrudan düzeniyle, eşzamanlılık ihlali durumunda bir özel durum ortaya çıkar. Bunun yerine, WHERE yan tümcesi hiçbir kayıtla eşleşmediğinden database deyimi yalnızca kaydı etkilemez. BLL 'de oluşturulan tüm veri değiştirme yöntemleri, tam olarak bir kaydın etkilenip etkilenmediğini belirten bir Boole değeri döndürecek şekilde tasarlanmıştır. Bu nedenle, bir kayıt silinirken eşzamanlılık ihlalinin oluşup oluşmadığını öğrenmek için BLL 'nin `DeleteProduct` yönteminin dönüş değerini inceleyebilirsiniz.

Bir BLL yöntemi için dönüş değeri, ObjectDataSource 'un, olay işleyicisine geçirilen `ObjectDataSourceStatusEventArgs` nesnesinin `ReturnValue` özelliği aracılığıyla kendi düzey sonrası olay işleyicilerinde incelenebilir. `DeleteProduct` yönteminden dönüş değerini belirlemede ilgilendiğimiz için, ObjectDataSource 'un `Deleted` olayı için bir olay işleyicisi oluşturuyoruz. `ReturnValue` özelliği `object` türündedir ve bir özel durum harekete geçirilir ve yöntem bir değer döndürebilmesi için kesintiye uğrarsa `null` olabilir. Bu nedenle, öncelikle `ReturnValue` özelliğinin `null` olmadığından ve bir Boolean değer olduğundan emin olunması gerekir. Bu denetimin başarılı olduğu varsayıldığında, `ReturnValue` `false``DeleteConflictMessage` etiket denetimini gösteririz. Bu, aşağıdaki kod kullanılarak gerçekleştirilebilir:

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample14.cs)]

Eşzamanlılık ihlali durumunda kullanıcının silme isteği iptal edilir. GridView yenilenir, bu kayıt için, kullanıcının sayfayı yüklediği zamanla ve Sil düğmesine tıkladıklarında oluşan değişiklikler gösteriliyor. Böyle bir ihlal transpires, ne olduğunu açıklayan `DeleteConflictMessage` etiketi gösterilir (bkz. Şekil 20).

[![bir Kullanıcı silme işlemi eşzamanlılık Ihlali durumunda Iptal edilir](implementing-optimistic-concurrency-cs/_static/image57.png)](implementing-optimistic-concurrency-cs/_static/image56.png)

**Şekil 20**: bir Kullanıcı silme Işlemi eşzamanlılık Ihlali durumunda iptal edilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-cs/_static/image58.png))

## <a name="summary"></a>Özet

Birden çok, eşzamanlı kullanıcının verileri güncelleştirmesine veya silmesine izin veren her uygulamada eşzamanlılık ihlallerinin fırsatları vardır. Bu tür ihlaller ' de hesaba katılmaz, iki kullanıcı aynı anda aynı verileri güncelleştirirse, diğer kullanıcının değişiklik değişikliklerinin üzerine yazılır. Alternatif olarak, geliştiriciler iyimser veya Kötümser eşzamanlılık denetimi uygulayabilir. İyimser eşzamanlılık denetimi eşzamanlılık ihlallerinin seyrek olduğunu varsayar ve bir eşzamanlılık ihlali oluşturacak bir güncelleştirme ya da silme komutuna izin vermez. Kötümser eşzamanlılık denetimi eşzamanlılık ihlallerinin sık olduğunu varsayar ve tek bir kullanıcının Update ya da Delete komutunun kabul edilebilir olmadığından emin olur. Kötümser eşzamanlılık denetimiyle bir kaydın güncelleştirilmesi, kilitlenirken diğer kullanıcıların kaydı değiştirmesini veya silmesini önler.

.NET 'teki türü belirtilmiş veri kümesi, iyimser eşzamanlılık denetimini desteklemek için işlevsellik sağlar. Özellikle, veritabanına verilen `UPDATE` ve `DELETE` deyimleri tüm tablo sütunlarını içerir, böylece güncelleştirme veya silme işleminin yalnızca, kaydın geçerli verileri kullanıcının güncelleştirme veya silme gerçekleştirirken sahip olduğu özgün verilerle eşleşiyorsa meydana gelir. DAL, iyimser eşzamanlılığı destekleyecek şekilde yapılandırıldıktan sonra BLL yöntemlerinin güncellenmesi gerekir. Ayrıca, BLL içine geri çağıran ASP.NET sayfası, ObjectDataSource, veri Web denetiminden özgün değerleri alıp onları BLL 'ye geçirmeden önce yapılandırılmalıdır.

Bu öğreticide gördüğümüz gibi, bir ASP.NET Web uygulamasında iyimser eşzamanlılık denetimini uygulamak, DAL ve BLL 'yi güncelleştirmeyi ve ASP.NET sayfasına destek eklemeyi içerir. Bu eklenen iş, sizin zaman ve çabalarınızın bir temelinde yatırım yapıp uygulamadığınıza bağlıdır. Eşzamanlı kullanıcılarınızın verileri güncelliyor veya güncelleştirdikleri veriler diğerinden farklıysa eşzamanlılık denetimi bir temel sorun değildir. Ancak, sitenizde aynı verilerle çalışan birden fazla Kullanıcı düzenli olarak varsa, eşzamanlılık denetimi bir kullanıcının güncelleştirmelerinin veya silinmesinden başka birinin üzerine yazılmasına neden olacak şekilde, bir kullanıcının güncelleştirme veya silme yapılmasını önlemeye yardımcı olabilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](customizing-the-data-modification-interface-cs.md)
> [İleri](adding-client-side-confirmation-when-deleting-cs.md)
