---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
title: SqlDataSource ile Iyimser eşzamanlılık uygulama (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, iyimser eşzamanlılık denetiminin temel bileşenleri inceliyoruz ve ardından SqlDataSource denetimini kullanarak nasıl uygulanacağını keşfedebilirsiniz.
ms.author: riande
ms.date: 02/20/2007
ms.assetid: a8fa72ee-8328-4854-a419-c1b271772303
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 431734b5245c20ac840147cf0827fa7f8d1e4d17
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598054"
---
# <a name="implementing-optimistic-concurrency-with-the-sqldatasource-vb"></a>SqlDataSource ile İyimser Eşzamanlılık Uygulama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_VB.exe) veya [PDF 'yi indirin](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/datatutorial50vb1.pdf)

> Bu öğreticide, iyimser eşzamanlılık denetiminin temel bileşenleri inceliyoruz ve ardından SqlDataSource denetimini kullanarak nasıl uygulanacağını keşfedebilirsiniz.

## <a name="introduction"></a>Giriş

Önceki öğreticide, SqlDataSource denetimine ekleme, güncelleştirme ve silme yeteneklerini nasıl ekleyeceğiniz incelendi. Kısacası, bu özellikleri, `UpdateCommand`, `DeleteCommand` ve `InsertParameters`koleksiyonlardaki uygun parametrelerle birlikte denetim s `InsertCommand`, `UpdateParameters`veya `DeleteParameters` özelliklerinde karşılık gelen `INSERT`, `UPDATE`veya `DELETE` SQL deyimlerinin belirtilmesi gerekiyordu. Bu özellikler ve koleksiyonlar el ile belirtiken, veri kaynağı Yapılandırma Sihirbazı s Gelişmiş düğmesi, bu ifadeleri `SELECT` bildirimine göre otomatik olarak oluşturacak `INSERT`, `UPDATE`ve `DELETE` deyimler onay kutusu sunar.

`INSERT`oluşturma, `UPDATE`ve `DELETE` deyimleriyle birlikte, gelişmiş SQL oluşturma seçenekleri iletişim kutusu, iyimser eşzamanlılık seçeneğini kullanın (bkz. Şekil 1). İşaretlendiğinde, otomatik olarak oluşturulan `UPDATE` ve `DELETE` deyimlerdeki `WHERE` yan tümceleri yalnızca, kullanıcının verileri kılavuza en son yüklemesinden bu yana temel alınan veritabanı verileri değiştirilmemişse güncelleştirme veya silme işlemleri için değiştirilir.

![Gelişmiş SQL oluşturma seçenekleri Iletişim kutusundan Iyimser eşzamanlılık desteği ekleyebilirsiniz](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.gif)

**Şekil 1**: Gelişmiş SQL oluşturma seçenekleri Iletişim kutusundan Iyimser eşzamanlılık desteği ekleyebilirsiniz

[Iyimser eşzamanlılık](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) öğreticisini uygulayarak, iyimser eşzamanlılık denetiminin temellerini ve bunu ObjectDataSource 'a eklemeyi inceledik. Bu öğreticide, iyimser eşzamanlılık denetiminin temel bileşenleri ile iletişime geçeceğiz ve ardından SqlDataSource kullanarak nasıl uygulanacağını araştırıyoruz.

## <a name="a-recap-of-optimistic-concurrency"></a>Iyimser eşzamanlılık bir üst sınırı

Birden çok, eşzamanlı kullanıcının aynı verileri düzenlemesine veya silmesine izin veren Web uygulamaları için, bir kullanıcının yanlışlıkla başka bir değişikliği geçersiz yazabilecekleri bir olasılık vardır. [Iyimser eşzamanlılık](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) öğreticisini uygulamak için aşağıdaki örneği sağladım:

İki kullanıcı olan Jisun ve Sam, ziyaretçilerin bir GridView denetimiyle ürünleri güncelleştirmesine ve silmesine izin veren bir uygulamada bir sayfa ziyaret ettiğini düşünün. Her ikisi de aynı anda Chai için Düzenle düğmesine tıklayın. Jisa ürün adını Chai Tea olarak değiştirir ve Güncelleştir düğmesine tıklar. Net sonuç, *Tüm* ürün öğeleri güncelleştirilebilir alanları ayarlayan veritabanına gönderilen bir `UPDATE` deyimidir (jıse yalnızca bir alan, `ProductName`). Bu noktada, veritabanı Chai Tea, kategori Içnoktaları, tedarikçi Exotic Litids ve bu ürüne yönelik olarak, bu ürünün bu değerlerini içerir. Ancak, Sam s ekranındaki GridView, hala, düzenlenebilir GridView satırındaki ürün adını Chai olarak gösterir. Jisun değişikliklerinin işlendiği birkaç saniye sonra, Sam kategoriyi koşullu olarak güncelleştirir ve Güncelleştir ' i tıklatır. Bu, ürün adını Chai olarak ayarlayan veritabanına gönderilen `UPDATE` bildirimine, karşılık gelen koşullu kategori KIMLIĞINE `CategoryID` ve bu şekilde devam eder. Ürün adında yapılan jisun değişikliklerinin üzerine yazıldı.

Şekil 2 bu etkileşimi gösterir.

[Iki kullanıcı aynı anda bir kaydı güncelleştirirken ![bir kullanıcının diğer s değişikliklerinin üzerine yazılmasına neden olacak değişiklikler](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.png)

**Şekil 2**: Iki kullanıcı aynı anda bir kaydı güncelleştirirken, bir kullanıcının diğer öğeleri üzerine yazılmasına yönelik değişiklikler ([tam boyutlu görüntüyü görüntülemek için tıklatın](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.png))

Bu senaryonun katlamayı engellemek için bir [eşzamanlılık denetimi](http://en.wikipedia.org/wiki/Concurrency_control) formu uygulanmalıdır. [İyimser eşzamanlılık](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) Bu öğreticinin odağı, şu anda eşzamanlılık çakışmaları olabileceğinden varsayımını ve sonra bu tür çakışmaların büyük çoğunluğunu görmemesi durumunda işe yarar. Bu nedenle, bir çakışma ortaya çıkarsa, iyimser eşzamanlılık denetimi kullanıcıya, farklı bir kullanıcı aynı verileri değiştirdiği için yaptıkları değişikliklerin kaydedimeyeceğini bildirir.

> [!NOTE]
> Birçok eşzamanlılık çakışması olacağını veya bu çakışmaların tolerandışı olduğunu varsaymayan uygulamalar için, bunun yerine Kötümser eşzamanlılık denetimi kullanılabilir. Kötümser eşzamanlılık denetimi hakkında daha kapsamlı bir tartışma için [Iyimser eşzamanlılık](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) öğreticisine geri dönün.

İyimser eşzamanlılık denetimi, güncelleştirilmesi veya silinmekte olan kaydın güncelleştirme ya da silme işlemi başladığında yaptığı gibi aynı değerlere sahip olduğundan emin olarak çalışarak işe yarar. Örneğin, düzenlenebilir bir GridView 'da Düzenle düğmesine tıkladığınızda, kayıt değerleri veritabanından okunmalıdır ve metin kutuları ve diğer Web denetimlerinde görüntülenir. Bu orijinal değerler GridView tarafından kaydedilir. Daha sonra Kullanıcı, değişiklikleri yaptıktan ve Update düğmesine tıkladıktan sonra, kullanılan `UPDATE` deyimin özgün değerleri ve yeni değerleri dikkate almalıdır ve yalnızca kullanıcının düzenlemesini başlattığı özgün değerler veritabanında hala aynı değerlerle aynıysa temel alınan veritabanı kaydını güncelleştirin. Şekil 3 ' te bu olay dizisi gösterilmektedir.

[Güncelleştirme veya silme Işleminin başarılı olması için ![, özgün değerler geçerli veritabanı değerlerine eşit olmalıdır](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.png)

**Şekil 3**: güncelleştirme veya silme işleminin başarılı olması Için, özgün değerler geçerli veritabanı değerlerine eşit olmalıdır ([tam boyutlu görüntüyü görüntülemek için tıklatın](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.png))

İyimser eşzamanlılığı uygulamaya yönelik çeşitli yaklaşımlar vardır (bir dizi seçeneğe kısa bir bakış için bkz. [Peter a. Bromberg](http://peterbromberg.net/)'ın [Iyimser eşzamanlılık güncelleştirme mantığı](http://www.eggheadcafe.com/articles/20050719.asp) ). SqlDataSource tarafından kullanılan teknik (ve veri erişim katmanımızda kullanılan ADO.NET türü belirtilmiş veri kümelerinde), tüm özgün değerleri bir karşılaştırma dahil etmek için `WHERE` yan tümcesini geliştirir. Örneğin, aşağıdaki `UPDATE` deyimleriyle, bir ürünün adını ve fiyatını yalnızca geçerli veritabanı değerleri GridView 'daki kayıt güncelleştirilirken başlangıçta alınan değerlere eşitse günceller. `@ProductName` ve `@UnitPrice` parametreleri Kullanıcı tarafından girilen yeni değerleri içerir, ancak Düzenle düğmesine tıklandığında `@original_ProductName` ve `@original_UnitPrice` ilk olarak GridView 'a yüklenmiş olan değerleri içerir:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample1.sql)]

Bu öğreticide göreceğiniz gibi, SqlDataSource ile iyimser eşzamanlılık denetimini etkinleştirmek, bir CheckBox denetimi yapmak kadar basittir.

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>1\. Adım: Iyimser eşzamanlılık destekleyen bir SqlDataSource oluşturma

`SqlDataSource` klasöründen `OptimisticConcurrency.aspx` sayfasını açarak başlayın. Araç kutusundan bir SqlDataSource denetimini tasarımcı üzerine sürükleyin, `ID` özelliğini `ProductsDataSourceWithOptimisticConcurrency`olarak ayarlar. Sonra, denetim öğeleri akıllı etiketinden veri kaynağını Yapılandır bağlantısına tıklayın. Sihirbazın ilk ekranından `NORTHWINDConnectionString` çalışmayı seçip Ileri ' ye tıklayın.

[![NORTHWINDConnectionString ile çalışmayı seçme](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.png)

**Şekil 4**: `NORTHWINDConnectionString` ile çalışmayı seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.png))

Bu örnekte, kullanıcıların `Products` tablosunu düzenlemesini sağlayan bir GridView ekleyeceğiz. Bu nedenle, select Ifadesini Yapılandır ekranında, açılan listeden `Products` tablosunu seçin ve Şekil 5 ' te gösterildiği gibi `ProductID`, `ProductName`, `UnitPrice`ve `Discontinued` sütunlarını seçin.

[Products tablosundan ![ProductID, ProductName, UnitPrice ve Discontinued sütunlarını döndürün](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.png)

**Şekil 5**: `Products` tablosundan `ProductID`, `ProductName`, `UnitPrice`ve `Discontinued` sütunlarını ([tam boyutlu görüntüyü görüntülemek Için tıklayın](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.png)) döndürün

Sütunları seçtikten sonra Gelişmiş düğmesine tıklayarak Gelişmiş SQL oluşturma seçenekleri iletişim kutusunu açın. `INSERT`, `UPDATE`ve `DELETE` deyimlerini oluşturun ve iyimser eşzamanlılık onay kutularını kullanın ve Tamam 'a tıklayın (bir ekran görüntüsü için Şekil 1 ' e geri bakın). Ileri ' ye ve ardından son ' a tıklayarak Sihirbazı doldurun.

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, elde edilen `DeleteCommand` ve `UpdateCommand` özelliklerini ve `DeleteParameters` ve `UpdateParameters` koleksiyonlarını incelemek için bir dakikanızı ayırın. Bunu yapmanın en kolay yolu, sayfanın bildirim temelli sözdizimini görmek için sol alt köşedeki kaynak sekmesine tıklamanız olur. `UpdateCommand` bir değeri bulacaksınız:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample2.sql)]

`UpdateParameters` koleksiyonunda yedi parametre ile:

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample3.aspx)]

Benzer şekilde, `DeleteCommand` özelliği ve `DeleteParameters` koleksiyonu aşağıdaki gibi görünmelidir:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample4.sql)]

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample5.aspx)]

`UpdateCommand` ve `DeleteCommand` özelliklerinin `WHERE` yan tümcelerini genişletmenin yanı sıra (ve ilgili parametre koleksiyonlarına ek parametreler eklemek), iyimser eşzamanlılık kullan seçeneğini belirlemek diğer iki özelliği ayarlar:

- [`ConflictDetection` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx) `OverwriteChanges` (varsayılan) olan `CompareAllValues` olarak değiştirir
- [`OldValuesParameterFormatString` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx) {0} (varsayılan) olarak orijinal\_{0} değiştirir.

Data Web Control, SqlDataSource s `Update()` veya `Delete()` metodunu çağırdığında, özgün değerleri geçirir. SqlDataSource s `ConflictDetection` özelliği `CompareAllValues`olarak ayarlandıysa, bu özgün değerler komuta eklenir. `OldValuesParameterFormatString` özelliği, bu özgün değer parametreleri için kullanılan adlandırma modelini sağlar. Veri kaynağını yapılandırma Sihirbazı özgün\_{0} kullanır ve `UpdateCommand` ve `DeleteCommand` özellikleri ve `UpdateParameters` ve `DeleteParameters` koleksiyonlarında her bir özgün parametreyi adlandırır.

> [!NOTE]
> SqlDataSource denetim ekleme özelliklerini kullandığımızdan, `InsertCommand` özelliğini ve `InsertParameters` koleksiyonunu kaldırmayı ücretsiz olarak hissettik.

## <a name="correctly-handlingnullvalues"></a>`NULL`değerlerini doğru şekilde Işleme

Ne yazık ki, iyimser eşzamanlılık kullanılırken genişletilmiş `UPDATE` ve `DELETE` deyimleri veri kaynağını yapılandırma Sihirbazı tarafından otomatik olarak oluşturulur `NULL` değerler içeren *kayıtlarla çalışmaz.* Nedenini görmek için, SqlDataSource s `UpdateCommand`göz önünde bulundurun:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample6.sql)]

`Products` tablosundaki `UnitPrice` sütununda `NULL` değeri olabilir. Belirli bir kaydın `UnitPrice`için `NULL` bir değeri varsa, `NULL = NULL` her zaman false döndürdüğünden `[UnitPrice] = @original_UnitPrice` `WHERE` yan tümce bölümü *her zaman* false olarak değerlendirilir. Bu nedenle, `UPDATE` ve `DELETE` deyimleri `WHERE` yan tümceleri güncelleştirmek veya silmek için herhangi bir satır döndürülmeyeceği için `NULL` değerleri içeren kayıtlar düzenlenemez veya silinemez.

> [!NOTE]
> Bu hata ilk olarak Microsoft 'a, SqlDataSource 'da 2004 Haziran ayında [yanlış SQL deyimleri oluşturuyor](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937) ve ASP.net 'in bir sonraki sürümünde düzeltilmesi planlanacaktır.

Bunu yapmak için, `NULL` değerlerine sahip olan **Tüm** sütunlar için hem `UpdateCommand` hem de `DeleteCommand` özelliklerde `WHERE` yan tümceleri el ile güncelleştirmemiz gerekir. Genel olarak `[ColumnName] = @original_ColumnName` şu şekilde değiştirin:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample7.sql)]

Bu değişiklik bildirime dayalı biçimlendirme aracılığıyla doğrudan, Özellikler penceresi UpdateQuery veya DeleteQuery seçenekleri aracılığıyla ya da veri yapılandırma içindeki özel bir SQL deyimi veya saklı yordam belirleme seçeneğinde GÜNCELLEŞTIRME ve SILME sekmeleri aracılığıyla yapılabilir Kaynak Sihirbazı. Bu değişiklik, `UpdateCommand` ve `DeleteCommand` s `WHERE` yan tümcesindeki `NULL` değerleri içerebilen *her* sütun için yapılmalıdır.

Bunu örneğimize uygulamak aşağıdaki değiştirilen `UpdateCommand` ve `DeleteCommand` değerlerine neden olur:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>2\. Adım: düzenleme ve silme seçenekleriyle GridView ekleme

İyimser eşzamanlılığı destekleyecek şekilde yapılandırılmış SqlDataSource ile, bu eşzamanlılık denetimini kullanan sayfaya bir veri Web denetimi eklemektir. Bu öğreticide, s için hem düzenleme hem de silme işlevselliği sağlayan bir GridView ekleyelim. Bunu gerçekleştirmek için araç kutusundan Tasarımcı üzerine bir GridView sürükleyin ve `ID` `Products`olarak ayarlayın. GridView s akıllı etiketinden, 1. adımda eklenen `ProductsDataSourceWithOptimisticConcurrency` SqlDataSource denetimine bağlayın. Son olarak, düzenlemenizi etkinleştir ve akıllı etiketteki silme seçeneklerini etkinleştir seçeneğini işaretleyin.

[GridView 'ı SqlDataSource 'a bağlamak ve Düzenle ve silmeyi etkinleştirmek ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.png)

**Şekil 6**: GridView 'ı SqlDataSource 'a bağlayın ve düzenlemenizi ve silmeyi etkinleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image10.png))

GridView eklendikten sonra, `ProductID` BoundField ' ı kaldırarak ve `ProductName` BoundField s `HeaderText` özelliğini ürün olarak değiştirerek ve `HeaderText` özelliğinin yalnızca fiyatı olacak şekilde `UnitPrice` BoundField güncelleyerek görünümünü yapılandırın. İdeal olarak, `ProductName` değeri için bir RequiredFieldValidator ve `UnitPrice` değeri için bir CompareValidator (düzgün şekilde biçimlendirilen bir sayısal değer olduğundan emin olmak için) için bir RequiredFieldValidator eklemek üzere, düzen arabirimini geliştirdik. Daha ayrıntılı bir bakış için bkz. [veri değişikliği arabirimi](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) öğreticisini özelleştirme, GridView s Düzenle arabirimini özelleştirmeye bakın.

> [!NOTE]
> GridView 'dan SqlDataSource 'a geçirilen özgün değerler görüntüleme durumunda depolandığından, GridView s görünüm durumu etkinleştirilmelidir.

GridView 'da bu değişiklikleri yaptıktan sonra GridView ve SqlDataSource bildirim temelli biçimlendirme aşağıdakine benzer olmalıdır:

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample9.aspx)]

İyimser eşzamanlılık denetimini çalışırken görmek için iki tarayıcı penceresi açın ve `OptimisticConcurrency.aspx` sayfasını her ikisine de yükleyin. Her iki tarayıcıda da ilk ürünün düzenleme düğmelerine tıklayın. Tek bir tarayıcıda ürün adını değiştirin ve Güncelleştir ' e tıklayın. Tarayıcı geri göndermeye ve GridView, yeni düzenlenen kayıt için yeni ürün adını gösterecek şekilde ön düzenleme moduna geri döner.

İkinci tarayıcı penceresinde, fiyatı değiştirin (ancak ürün adını özgün değeri olarak bırakın) ve Güncelleştir ' e tıklayın. Geri göndermede, kılavuz, ön Düzenle moduna geri döner, ancak fiyata yapılan değişiklik kaydedilmez. İkinci tarayıcı, eski fiyata sahip olan ilk yeni ürün adıyla aynı değeri gösterir. İkinci tarayıcı penceresinde yapılan değişiklikler kayboldu. Üstelik, bir eşzamanlılık ihlalinin gerçekleşmediğini belirten bir özel durum veya ileti olmadığından, değişiklikler sessizce kaybedilir.

[Ikinci tarayıcı penceresindeki değişiklikler sessizce kayboldu ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image11.png)

**Şekil 7**: Ikinci tarayıcı penceresindeki değişiklikler sessizce kayboldu ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image12.png))

İkinci tarayıcı değişikliklerinin neden yürütülmedi, `UPDATE` deyimi `WHERE` yan tümcesi tüm kayıtları filtreledi ve bu nedenle herhangi bir satırı etkilemediği için oldu. `UPDATE` deyiminize tekrar göz atalım:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample10.sql)]

İkinci tarayıcı penceresi kaydı güncelleştirdiğinde, `WHERE` yan tümcesinde belirtilen özgün ürün adı, var olan ürün adı ile eşleşmiyor (ilk tarayıcı tarafından değiştirildiğinden). Bu nedenle, deyimin `[ProductName] = @original_ProductName` false değerini döndürür ve `UPDATE` hiçbir kaydı etkilemez.

> [!NOTE]
> Aynı şekilde çalışma öğesini silin. İki tarayıcı penceresi açıkken, belirli bir ürünü tek bir düzenleyerek ve sonra değişiklikleri kaydederek başlayın. Değişiklikleri tek bir tarayıcıda kaydettikten sonra, diğer üründe aynı ürünün Sil düğmesine tıklayın. Özgün değerler `DELETE` deyimi s `WHERE` yan tümcesinde eşleşmediğinden, silme işlemi sessizce başarısız olur.

İkinci tarayıcı penceresinde Son Kullanıcı perspektifinden, güncelleştirme düğmesine tıkladıktan sonra kılavuz, ön Düzenle moduna geri döner, ancak değişiklikleri kaybedilir. Ancak, değişikliklerinin hiçbir görsel geri bildirimi yok. İdeal olarak, bir Kullanıcı değişikliklerinin eşzamanlılık ihlaline karşı kaybolması durumunda onlara bildirimde bulunur ve belki de Kılavuzu düzenleme modunda tutabilirsiniz. Bunun nasıl yapılacağını göz atalım.

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>3\. Adım: bir eşzamanlılık Ihlalinin ne zaman gerçekleştiğini belirleme

Bir eşzamanlılık ihlali yaptığı değişiklikleri reddettiğinde, bir eşzamanlılık ihlali oluştuğunda kullanıcıyı uyarmak iyi olacaktır. Kullanıcıyı uyarmak için, `ConcurrencyViolationMessage` adlı sayfanın en üstüne, `Text` özelliği şu iletiyi görüntüleyen bir etiket Web denetimi ekleyelim: başka bir kullanıcı tarafından aynı anda güncelleştirilmiş bir kaydı güncelleştirmeye veya silmeye çalıştınız. Lütfen diğer kullanıcının değişikliklerini gözden geçirin ve sonra güncelleştirmenizi veya silmeyi yeniden yapın. Etiketi Control s `CssClass` özelliğini, bir kırmızı, italik, kalın ve büyük yazı tipinde metin görüntüleyen `Styles.css` tanımlanmış bir CSS sınıfı olan uyarı olarak ayarlayın. Son olarak, etiket s `Visible` ve `EnableViewState` özelliklerini `False`olarak ayarlayın. Bu, yalnızca `Visible` özelliğini açıkça `True`olarak ayarlamış olduğumuz geri göndermeler haricinde etiketi gizler.

[Uyarıyı göstermek için sayfaya bir etiket denetimi eklemek ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image13.png)

**Şekil 8**: uyarıyı görüntülemek için sayfaya bir etiket denetimi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image14.png))

Bir güncelleştirme veya silme gerçekleştirirken, GridView s `RowUpdated` ve `RowDeleted` olay işleyicileri, veri kaynağı denetimi istenen güncelleştirmeyi veya silmeyi gerçekleştirdikten sonra harekete geçmektedir. Bu olay işleyicilerinden işlemden kaç satır etkilendiğini belirleyebiliriz. Sıfır satır etkileniyorsa, `ConcurrencyViolationMessage` etiketini göstermek istiyoruz.

Hem `RowUpdated` hem de `RowDeleted` olayları için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample11.vb)]

Her iki olay işleyicilerinde de `e.AffectedRows` özelliğini denetliyoruz ve 0 ' a eşitse, `ConcurrencyViolationMessage` Label s `Visible` özelliğini `True`olarak ayarlayın. `RowUpdated` olay işleyicisinde, GridView 'un, `KeepInEditMode` özelliğini true olarak ayarlayarak düzenleme modunda kalmasını de sağlarız. Bunu yaparken, verileri kılavuza yeniden bağlamanız gerekir, böylece diğer Kullanıcı verileri, düzen arabirimine yüklenir. Bu, GridView s `DataBind()` yöntemi çağırarak gerçekleştirilir.

Şekil 9 ' da gösterildiği gibi, bu iki olay işleyicileriyle bir eşzamanlılık ihlali meydana geldiğinde çok dikkat çekici bir ileti görüntülenir.

[![bir Ileti eşzamanlılık Ihlalinin Yüzinde görüntülenir](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image15.png)

**Şekil 9**: bir Ileti eşzamanlılık Ihlali tarafında görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image16.png))

## <a name="summary"></a>Özet

Birden çok eş zamanlı kullanıcının aynı verileri düzenlemekte olabileceği bir Web uygulaması oluştururken, eşzamanlılık denetim seçeneklerini göz önünde bulundurmanız önemlidir. Varsayılan olarak, ASP.NET Data Web denetimleri ve veri kaynağı denetimleri herhangi bir eşzamanlılık denetimi kullanmaz. Bu öğreticide gördüğünüz gibi, SqlDataSource ile iyimser eşzamanlılık denetimini uygulamak nispeten hızlı ve kolaydır. SqlDataSource, otomatik olarak düzenlenen `UPDATE` ve `DELETE` deyimlerine genişletilmiş `WHERE` yan tümceleri eklemek için yasalların çoğunu işler, ancak `NULL` değerlerini doğru şekilde Işleme bölümünde anlatıldığı gibi, `NULL` değer sütunlarını işlemek için birkaç alt tledide vardır.

Bu öğretici, SqlDataSource incelemesini yerine eriyor. Kalan öğreticilerimiz, ObjectDataSource ve katmanlı mimari kullanılarak verilerle çalışmaya geri dönecektir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Öncekini](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
