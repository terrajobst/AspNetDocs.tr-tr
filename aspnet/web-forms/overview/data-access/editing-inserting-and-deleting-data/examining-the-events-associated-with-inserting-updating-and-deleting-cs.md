---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
title: Ekleme, güncelleştirme ve silme (C#) Ile ilişkili olayları İnceleme | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, bir ASP.NET Data Web denetiminin INSERT, Update veya delete işleminden önce, sırasında ve sonrasında oluşan olayları kullanmayı inceleyeceğiz. W...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: dab291a0-a8b5-46fa-9dd8-3d35b249201f
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: a8c1388b73524a8bb918b67aa265db894c07636f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78609153"
---
# <a name="examining-the-events-associated-with-inserting-updating-and-deleting-c"></a>Ekleme, Güncelleştirme ve Silme ile İlişkili Olayları İnceleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_CS.exe) veya [PDF 'yi indirin](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/datatutorial17cs1.pdf)

> Bu öğreticide, bir ASP.NET Data Web denetiminin INSERT, Update veya delete işleminden önce, sırasında ve sonrasında oluşan olayları kullanmayı inceleyeceğiz. Ayrıca, düzen arabirimini yalnızca ürün alanlarının bir alt kümesini güncelleştirmek üzere nasıl özelleştireceğiz.

## <a name="introduction"></a>Giriş

GridView, DetailsView veya FormView denetimlerinin özelliklerini, düzenlemesini veya silmeyi kullandığınızda, Son Kullanıcı yeni bir kayıt ekleme veya var olan bir kaydı güncelleştirme ya da silme işlemini tamamladığında transpire çeşitli adımlar. [Önceki öğreticide](an-overview-of-inserting-updating-and-deleting-data-cs.md)anlatıldığı gibi, GridView 'da bir satır düzenlendiğinde Düzenle düğmesi Update ve Cancel düğmeleriyle değiştirilmiştir ve Boundfields, Textboxes. Son Kullanıcı verileri güncelleştirdikten ve Güncelleştir ' i tıkladıktan sonra geri gönderme sırasında aşağıdaki adımlar gerçekleştirilir:

1. GridView, ObjectDataSource 'un `UpdateParameters`, Kullanıcı tarafından girilen değerlerle birlikte, düzenlenen kaydın benzersiz tanımlayıcı alanları (`DataKeyNames` özelliği aracılığıyla) ile doldurur
2. GridView, ObjectDataSource 'un `Update()` yöntemini çağırır, bu da temel nesnede uygun yöntemi (`ProductsDAL.UpdateProduct`, önceki öğreticimizde) çağırır.
3. Artık güncelleştirilmiş değişiklikleri içeren temel alınan veriler GridView 'a yeniden bağlanır

Bu adım sırası sırasında, gereken durumlarda özel mantık eklemek için olay işleyicileri oluşturmamızı sağlayan birkaç olay tetikmize olanak sağlar. Örneğin, 1. adımdan önce GridView 'un `RowUpdating` olayı ateşlenir. Bu noktada, bazı doğrulama hatası varsa güncelleştirme isteğini iptal edebilirsiniz. `Update()` yöntemi çağrıldığında, ObjectDataSource 'un `Updating` olayı harekete geçirilir, bu da `UpdateParameters`herhangi birinin değerlerini ekleme veya özelleştirme fırsatı sağlar. ObjectDataSource 'un temel alınan nesnesinin yöntemi yürütmeyi tamamladıktan sonra, ObjectDataSource 'un `Updated` olayı tetiklenir. `Updated` olayına yönelik bir olay işleyicisi, kaç satır etkilendiğine ve bir özel durumun oluşup oluşmadığını gösteren güncelleştirme işlemiyle ilgili ayrıntıları inceleyebilir. Son olarak, adım 2 ' den sonra GridView 'un `RowUpdated` olayı ateşlenir; Bu olay için bir olay işleyicisi, az önce gerçekleştirilen güncelleştirme işlemiyle ilgili ek bilgileri inceleyebilir.

Şekil 1 ' de bir GridView güncelleştirilirken bu olay serisi ve adımlar gösterilmektedir. Şekil 1 ' deki olay deseninin bir GridView ile güncelleştirilmesi benzersiz değildir. GridView, DetailsView veya FormView 'dan veri ekleme, güncelleştirme veya silme, hem veri Web denetimi hem de ObjectDataSource için aynı sırada ön ve son düzey olay dizisini Precipitates.

[GridView 'daki verileri güncelleştirirken başlatılan bir dizi ön ve son olay ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image1.png)

**Şekil 1**: bir GridView 'Daki verileri güncelleştirirken başlatılan ön ve son olaylar serisi ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image3.png))

Bu öğreticide, ASP.NET Data Web denetimlerinin yerleşik ekleme, güncelleştirme ve silme yeteneklerini genişletmek için bu olayları kullanmayı inceleyeceğiz. Ayrıca, düzen arabirimini yalnızca ürün alanlarının bir alt kümesini güncelleştirmek üzere nasıl özelleştireceğiz.

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>1\. Adım: ürünün`ProductName`ve`UnitPrice`alanlarını güncelleştirme

Önceki öğreticideki düzen arabirimlerinde, salt okuma olmayan *Tüm* ürün alanları dahil ediliyordu. GridView 'dan bir alan kaldırırız `QuantityPerUnit`-verileri güncelleştirirken veri Web denetimi ObjectDataSource 'un `QuantityPerUnit` `UpdateParameters` değerini ayarlayamaz. ObjectDataSource daha sonra `UpdateProduct` Iş mantığı katmanı (BLL) yöntemine `null` bir değer geçiriyordu, bu da düzenlenen veritabanı kaydının `QuantityPerUnit` sütununu `NULL` bir değer olarak değiştirir. Benzer şekilde, `ProductName`gibi gerekli bir alan, düzen arabiriminden kaldırılırsa, güncelleştirme "*ÜrünAdı" sütunu null değerlere izin*vermez "özel durumuna neden olmaz. Bu davranışın nedeni, ObjectDataSource 'un, her ürün alanı için bir giriş parametresi beklenen `ProductsBLL` sınıfının `UpdateProduct` yöntemini çağırmak üzere yapılandırılmasından kaynaklanır. Bu nedenle, ObjectDataSource 'un `UpdateParameters` koleksiyonu yöntemin giriş parametrelerinin her biri için bir parametre içeriyordu.

Son kullanıcının alanların bir alt kümesini yalnızca güncelleştirmesine izin veren bir veri Web denetimi sağlamak istiyorsam, ObjectDataSource 'un `Updating` olay işleyicisindeki eksik `UpdateParameters` değerlerini programlı olarak ayarlamanız veya alanların yalnızca bir alt kümesini bekleyen bir BLL yöntemi oluşturmanız ve çağırmanız gerekir. Bu ikinci yaklaşımı inceleyelim.

Özellikle, düzenlenebilir bir GridView içinde yalnızca `ProductName` ve `UnitPrice` alanlarını görüntüleyen bir sayfa oluşturalım. Bu GridView 'un düzenlenme arabirimi yalnızca kullanıcının, `ProductName` ve `UnitPrice`iki görüntülenmiş alanı güncelleştirmesine izin verir. Bu düzen arabirimi yalnızca bir ürünün alanlarının alt kümesini sağladığından, var olan BLL 'nin `UpdateProduct` yöntemini kullanan ve eksik ürün alanı değerleri `Updating` olay işleyicisinde program aracılığıyla ayarlanmış olan bir ObjectDataSource oluşturmanız gerekir ya da GridView içinde tanımlı alanların yalnızca alt kümesini bekleyen yeni bir BLL yöntemi oluşturuyoruz. Bu öğreticide, ikinci seçeneği kullanalım ve `UpdateProduct` yönteminin yalnızca üç giriş parametresi içinde yer aldığı bir aşırı yüklemesi oluşturalım: `productName`, `unitPrice`ve `productID`:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample1.cs)]

Özgün `UpdateProduct` yöntemi gibi, bu aşırı yükleme, veritabanında belirtilen `ProductID`bir ürün olup olmadığını denetleyerek başlatılır. Aksi takdirde, ürün bilgilerini güncelleştirme isteğinin başarısız olduğunu belirten `false`döndürür. Aksi takdirde, mevcut ürün kaydının `ProductName` ve `UnitPrice` alanlarını uygun şekilde güncelleştirir ve `ProductsRow` örneğini geçirerek TableAdapter `Update()` yöntemini çağırarak güncelleştirmeyi kaydeder.

`ProductsBLL` sınıfımızın bu eklenmesiyle, Basitleştirilmiş GridView arabirimini oluşturmaya hazırız. `EditInsertDelete` klasöründeki `DataModificationEvents.aspx` açın ve sayfaya bir GridView ekleyin. Yeni bir ObjectDataSource oluşturun ve bu `ProductsBLL` sınıfını `GetProducts` `Select()` yöntemi eşleme ile, `UpdateProduct` ve `productName`giriş parametrelerini alan `unitPrice`aşırı yüküne eşleyerek `Update()` yöntemi ile kullanacak şekilde yapılandırın.`productID` Şekil 2 ' de, ObjectDataSource 'un `Update()` yöntemini `ProductsBLL` sınıfının yeni `UpdateProduct` yöntem aşırı yüklemesiyle eşlerken veri kaynağı oluşturma Sihirbazı gösterilmektedir.

[![ObjectDataSource 'un Update () yöntemini yeni UpdateProduct Overload ile eşleyin](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image4.png)

**Şekil 2**: ObjectDataSource 'un `Update()` yöntemini yeni `UpdateProduct` aşırı yüklemeye eşleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image6.png))

Örneğimizin başlangıçta yalnızca verileri düzenleyebilme, kayıt ekleme veya silme yeteneğine ihtiyacı olduğu için, ObjectDataSource 'un `Insert()` ve `Delete()` yöntemlerinin INSERT ve DELETE sekmelerine giderek ve açılan listeden (hiçbiri) seçim yaparak `ProductsBLL` sınıfının yöntemlerinden herhangi birine eşlenmediğini açıkça belirten bir süre ayırın.

[INSERT ve DELETE sekmeleri için açılan listeden (yok) ![seçin](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image7.png)

**Şekil 3**: ekleme ve silme sekmeleri Için açılan listeden (hiçbiri) seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image9.png))

Bu Sihirbazı tamamladıktan sonra GridView 'un akıllı etiketindeki Düzenle özelliğini etkinleştir onay kutusunu işaretleyin.

Veri kaynağı oluşturma Sihirbazı ' nın tamamlanmasını ve GridView 'a bağlamayı kullanarak, Visual Studio her iki denetim için bildirime dayalı sözdizimini oluşturmuştur. Aşağıda gösterilen ObjectDataSource 'un bildirim temelli işaretlemesini incelemek için kaynak görünümüne gidin:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample2.aspx)]

ObjectDataSource 'un `Insert()` ve `Delete()` yöntemleri için hiçbir eşleşme olmadığından, `InsertParameters` veya `DeleteParameters` bölümü yoktur. Ayrıca, `Update()` yöntemi yalnızca üç giriş parametresini kabul eden `UpdateProduct` yöntemi aşırı yüküne eşlendiğinden `UpdateParameters` bölümünde yalnızca üç `Parameter` örneği bulunur.

ObjectDataSource 'un `OldValuesParameterFormatString` özelliğinin `original_{0}`olarak ayarlandığını unutmayın. Bu özellik, veri kaynağı Yapılandırma Sihirbazı kullanılırken Visual Studio tarafından otomatik olarak ayarlanır. Ancak, BLL yöntemlerimiz özgün `ProductID` değerinin geçirilmesini beklemediğinden, bu özellik atamasını ObjectDataSource 'un bildirime dayalı sözdiziminden tamamen kaldırın.

> [!NOTE]
> Tasarım görünümü Özellikler penceresi `OldValuesParameterFormatString` özellik değerini yalnızca bir temizlerseniz, özellik bildirime dayalı sözdiziminde kalır, ancak boş bir dizeye ayarlanır. Özelliği bildirime dayalı sözdiziminden tamamen kaldırın ya da Özellikler penceresi, değeri varsayılan, `{0}`olarak ayarlayın.

ObjectDataSource, ürünün adı, fiyatı ve KIMLIĞI için yalnızca `UpdateParameters` sahip olsa da, Visual Studio ürün alanlarının her biri için GridView 'a bir BoundField veya CheckBoxField ekledi.

[GridView ![, ürün alanlarının her biri için bir BoundField veya CheckBoxField Içeriyor](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image10.png)

**Şekil 4**: GridView, ürün alanlarının her biri Için bir BoundField veya CheckBoxField içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image12.png))

Son Kullanıcı bir ürünü düzenlediğinde ve Update düğmesine tıkladığında, GridView salt okunmayan alanları numaralandırır. Ardından, ObjectDataSource 'un `UpdateParameters` koleksiyonundaki karşılık gelen parametrenin değerini Kullanıcı tarafından girilen değere ayarlar. Karşılık gelen bir parametre yoksa, GridView koleksiyona bir tane ekler. Bu nedenle, GridView 'umuz tüm ürün alanları için BoundFields ve CheckBoxFields içeriyorsa, ObjectDataSource bu parametrelerin tümünde geçen `UpdateProduct` aşırı yüklemeyi çağırarak, ObjectDataSource 'un bildirim temelli biçimlendirmesinin yalnızca üç giriş parametresi (bkz. Şekil 5) belirttiğinden emin olur. Benzer şekilde, GridView 'da bir `UpdateProduct` aşırı yüklemesi için giriş parametrelerine karşılık gelen salt okunurdur ürün alanlarının bir birleşimi varsa, güncelleştirilmeye çalışıldığında bir özel durum oluşur.

[GridView ![, ObjectDataSource 'un UpdateParameters koleksiyonuna parametreler ekleyecek](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image13.png)

**Şekil 5**: GridView, ObjectDataSource 'un `UpdateParameters` koleksiyonuna parametreler ekler ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image15.png))

ObjectDataSource 'un yalnızca ürünün adını, fiyatını ve KIMLIĞINI alan `UpdateProduct` aşırı yüklemeyi çağırdığından emin olmak için GridView 'un yalnızca `ProductName` ve `UnitPrice`için düzenlenebilir alanlara sahip olacak şekilde kısıtlanması gerekir. Bu, diğer BoundFields ve CheckBoxFields alanları kaldırılarak gerçekleştirilebilir, bu diğer alanlar ' `ReadOnly` özelliği `true`veya bunun bir birleşimiyle oluşur. Bu öğreticide, `ProductName` ve `UnitPrice` BoundFields dışındaki tüm GridView alanlarını kaldıralım ve sonrasında GridView 'un bildirim temelli biçimlendirmesinin şöyle görünelim:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample3.aspx)]

`UpdateProduct` aşırı yüklemesi üç giriş parametresi beklediği halde, GridView 'da yalnızca iki BoundField vardır. Bunun nedeni `productID` giriş parametresinin birincil anahtar değeri olması ve düzenlenmiş satır için `DataKeyNames` özelliğinin değeri üzerinden geçirilmesi.

GridView bizim `UpdateProduct` aşırı yüklemesiyle birlikte, bir kullanıcının diğer ürün alanlarını kaybetmeden yalnızca bir ürünün adını ve fiyatını düzenlemesine izin verir.

[![arabirim yalnızca ürünün adını ve fiyatını düzenlemenizi sağlar](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image16.png)

**Şekil 6**: arabirim yalnızca ürünün adını ve fiyatını düzenlemenizi sağlar ([tam boyutlu görüntüyü görüntülemek için tıklatın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image18.png))

> [!NOTE]
> Önceki öğreticide anlatıldığı gibi, GridView s görünüm durumunun etkinleştirilmesi (varsayılan davranış) açısından önemli değildir. GridView s `EnableViewState` özelliğini `false`olarak ayarlarsanız, eşzamanlı kullanıcıların kayıtları yanlışlıkla silmesini veya düzenlemesini sağlamak için bir risk çalıştırırsınız. Daha fazla bilgi için bkz. [Uyarı: ASP.NET 2,0 GridViews/DetailsView/formviews ile, görüntüleme ve/veya silme ve görünüm durumunu devre dışı bırakma desteği](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx) .

## <a name="improving-theunitpriceformatting"></a>`UnitPrice`biçimlendirmesini geliştirme

Şekil 6 ' da gösterilen GridView örneği çalışırken, `UnitPrice` alanı hiçbir para birimi sembolü bulunmayan ve dört ondalık basamağa sahip bir fiyat görüntüsüne neden olarak biçimlendirilmez. Düzenlenemeyen satırlara bir para birimi biçimlendirme uygulamak için, `UnitPrice` BoundField 'un `DataFormatString` özelliğini `{0:c}` ve `HtmlEncode` özelliğine `false`olarak ayarlamanız yeterlidir.

[![BirimFiyat 'ın DataFormatString ve HtmlEncode özelliklerini uygun şekilde ayarlayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image19.png)

**Şekil 7**: `UnitPrice``DataFormatString` ve `HtmlEncode` özelliklerini uygun şekilde ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image21.png))

Bu değişiklik ile, düzenlenemeyen satırlar fiyatı para birimi olarak biçimlendirir; Ancak düzenlenen satır, yine para birimi simgesi olmadan ve dört ondalık basamakla değeri görüntüler.

[Düzenlenebilir olmayan satırları ![artık para birimi değerleri olarak biçimlendirilir](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image22.png)

**Şekil 8**: düzenlenemeyen satırlar artık para birimi değeri olarak biçimlendirilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image24.png))

`DataFormatString` özelliğinde belirtilen biçimlendirme yönergeleri, BoundField 'un `ApplyFormatInEditMode` özelliği `true` olarak ayarlanarak, düzen arabirimine uygulanabilir (varsayılan değer `false`). Bu özelliği `true`olarak ayarlamak için bir dakikanızı ayırın.

[![UnitPrice öğesinin ApplyFormatInEditMode özelliğini true olarak ayarla](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image25.png)

**Şekil 9**: `UnitPrice` BoundField 'ın `ApplyFormatInEditMode` özelliğini `true` olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image27.png))

Bu değişiklik ile düzenlenen satırda görünen `UnitPrice` değeri de para birimi olarak biçimlendirilir.

[Düzenlenmiş satırın BirimFiyat değeri artık para birimi olarak biçimlendirildi ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image28.png)

**Şekil 10**: düzenlenmiş satırın `UnitPrice` değeri artık para birimi olarak biçimlendirilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image30.png))

Ancak, bir ürünün $19,00 gibi bir metin kutusundaki para birimi simgesiyle güncelleştirilmesi bir `FormatException`oluşturur. GridView, Kullanıcı tarafından sağlanan değerleri ObjectDataSource 'un `UpdateParameters` koleksiyonuna atamaya çalıştığında, "$19,00" `UnitPrice` dizesini parametrenin gerektirdiği `decimal` dönüştüremiyor (bkz. Şekil 11). Bu sorunu gidermek için, GridView 'un `RowUpdating` olayı için bir olay işleyicisi oluşturabilir ve Kullanıcı tarafından sağlanan `UnitPrice` para birimi biçimli `decimal`olarak ayrıştırılabilir.

GridView 'un `RowUpdating` olayı, ikinci parametresi olarak kabul eder; bu, sözlüklerinin `UpdateParameters` koleksiyonuna atanmak [üzere, Kullanıcı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx)tarafından sağlanan değerleri tutan özelliklerinden biri olarak bir `NewValues` sözlüğü içerir. `RowUpdating` olay işleyicisindeki aşağıdaki kod satırlarına sahip para birimi biçimi kullanılarak, `NewValues` koleksiyonundaki mevcut `UnitPrice` değerini bir ondalık değer ayrıştırılabiliriz:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample4.cs)]

Kullanıcı `UnitPrice` bir değer ("$19,00" gibi) sağladıysa, Decimal ile hesaplanan ondalık değer ile bu değerin üzerine yazılır [. ayrıştırma](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx), değer para birimi olarak ayrıştırılıyor. Bu, herhangi bir para birimi sembolü, virgül, ondalık noktası vb. olaydaki ondalığı doğru bir şekilde ayrıştırır ve [System. Globalization](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx) ad alanındaki [NumberStyles sabit](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx) listesini kullanır.

Şekil 11 ' de, Kullanıcı tarafından sağlanan `UnitPrice`para birimi simgelerinden kaynaklanan sorun ve GridView 'un `RowUpdating` olay işleyicisinin bu girişi doğru şekilde ayrıştırmak için nasıl kullanılabileceğini gösterir.

[Düzenlenmiş satırın BirimFiyat değeri artık para birimi olarak biçimlendirildi ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image31.png)

**Şekil 11**: düzenlenmiş satırın `UnitPrice` değeri artık para birimi olarak biçimlendirilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image33.png))

## <a name="step-2-prohibitingnull-unitprices"></a>2\. Adım:`NULL UnitPrices` engelleme

Veritabanı `Products` tablosunun `UnitPrice` sütununda `NULL` değerlere izin verecek şekilde yapılandırıldığında, bu sayfayı ziyaret eden kullanıcıların bir `NULL` `UnitPrice` değer belirtmesini engellemek isteyebilirsiniz. Diğer bir deyişle, bir Kullanıcı, sonuçları veritabanına kaydetmek yerine bir ürün satırını düzenlenirken `UnitPrice` bir değer giremezse, bu sayfada, düzenlenen tüm ürünlerin belirtilen fiyata sahip olması gerektiğini bildiren bir ileti görüntülenmesini istiyoruz.

GridView 'un `RowUpdating` olay `Cancel` işleyicisine geçirilen `GridViewUpdateEventArgs` nesnesi, `true`olarak ayarlanırsa güncelleştirme işlemini sonlandırır. `RowUpdating` olay işleyicisini `true` `e.Cancel` ayarlamaya ve `NewValues` koleksiyondaki `UnitPrice` değerinin neden `null`olduğunu açıklayan bir ileti görüntüleyecek şekilde genişletelim.

`MustProvideUnitPriceMessage`adlı sayfaya bir etiket Web denetimi ekleyerek başlayın. Bu etiket denetimi, Kullanıcı bir ürünü güncelleştirirken bir `UnitPrice` değer belirtmediğinde görüntülenir. Etiketin `Text` özelliğini "ürün için bir fiyat sağlamalısınız" olarak ayarlayın. Ayrıca, aşağıdaki tanım ile `Styles.css` adlı `Warning` yeni bir CSS sınıfı oluşturdum:

[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample5.css)]

Son olarak, etiketin `CssClass` özelliğini `Warning`olarak ayarlayın. Bu noktada, tasarımcı, Şekil 12 ' de gösterildiği gibi, uyarı iletisini GridView üzerinde kırmızı, kalın, italik, çok büyük yazı tipi boyutunda göstermelidir.

[GridView 'un üstüne bir etiket ![eklendi](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image34.png)

**Şekil 12**: GridView üzerine bir etiket eklenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image36.png))

Varsayılan olarak, bu etiket gizli olmalıdır, bu nedenle `Visible` özelliğini `Page_Load` olay işleyicisindeki `false` olarak ayarlayın:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample6.cs)]

Kullanıcı `UnitPrice`belirtmeden bir ürünü güncelleştirmeyi denerse, güncelleştirmeyi iptal etmek ve uyarı etiketini göstermek istiyoruz. GridView 'un `RowUpdating` olay işleyicisini aşağıdaki şekilde güçlendirin:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample7.cs)]

Bir Kullanıcı bir fiyat belirtmeden bir ürünü kaydetmeye çalışırsa, güncelleştirme iptal edilir ve yararlı bir ileti görüntülenir. Veritabanı (ve iş mantığı) `NULL` `UnitPrice` s için izin verdiğinden, bu özel ASP.NET sayfası değildir.

[![bir Kullanıcı BirimFiyat boş bırakılamaz](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image37.png)

**Şekil 13**: Kullanıcı `UnitPrice` boş bırakılamaz ([tam boyutlu görüntüyü görüntülemek için tıklatın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image39.png))

Şimdiye kadar, ObjectDataSource 'un `UpdateParameters` koleksiyonuna atanan parametre değerlerini programlı bir şekilde değiştirmek ve güncelleştirme işlemini tamamen iptal etmek için GridView 'un `RowUpdating` olayını nasıl kullanacağınızı gördünüz. Bu kavramlar, DetailsView ve FormView denetimlerine geçer ve ayrıca ekleme ve silme için de geçerlidir.

Bu görevler, `Inserting`, `Updating`ve `Deleting` olayları için olay işleyicileri aracılığıyla ObjectDataSource düzeyinde de yapılabilir. Bu olaylar, temel alınan nesnenin ilişkili yöntemi çağrılmadan önce harekete geçilendir ve giriş parametreleri koleksiyonunu değiştirmek veya işlemi geri almak için son şans fırsatı sağlamaktır. Bu üç olaya yönelik olay işleyicileri, iki ilgilendiğiniz iki özelliği olan [ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx) türünde bir nesne geçirmiştir:

- `true`olarak ayarlanırsa, gerçekleştirilen [işlemi iptal eder](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx).
- Olay işleyicisinin `Inserting`, `Updating`veya `Deleting` olay için olup olmadığına bağlı olarak, `InsertParameters`, `UpdateParameters`veya `DeleteParameters`koleksiyonu olan [InputParameters](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx)

Ekler düzeyindeki parametre değerleriyle çalışmayı göstermek için, sayfamızda kullanıcıların yeni bir ürün eklemesine izin veren bir DetailsView ekleyelim. Bu DetailsView, veritabanına hızlı bir şekilde yeni bir ürün eklemek için bir arabirim sağlamak üzere kullanılacaktır. Yeni bir ürün eklerken tutarlı bir kullanıcı arabirimini korumak için, kullanıcının yalnızca `ProductName` ve `UnitPrice` alanlarına değer girmesine izin versin. Varsayılan olarak, DetailsView 'un ekleme arabiriminde sağlanmayan değerler bir `NULL` veritabanı değerine ayarlanır. Ancak, daha kısa bir süre içinde göreceğiniz gibi, ObjectDataSource 'un `Inserting` olayını farklı varsayılan değerler eklemek için kullanabiliriz.

## <a name="step-3-providing-an-interface-to-add-new-products"></a>3\. Adım: yeni ürünler eklemek için arabirim sağlama

Araç kutusundan bir DetailsView 'u GridView 'un üzerindeki tasarımcı üzerine sürükleyin, `Height` ve `Width` özelliklerini temizleyin ve sayfada zaten mevcut olan ObjectDataSource 'a bağlayın. Bu, ürün alanlarının her biri için bir BoundField veya CheckBoxField ekler. Yeni ürünler eklemek için bu DetailsView 'u kullanmak istediğimize göre akıllı etiketten eklemeyi etkinleştir seçeneğini denetliyoruz. Ancak, ObjectDataSource 'un `Insert()` yöntemi `ProductsBLL` sınıftaki bir yönteme eşlenmediği için bu tür bir seçenek yoktur (veri kaynağını yapılandırırken bu eşlemeyi (yok) belirlediğimiz hatırlayın. Şekil 3).

ObjectDataSource 'u yapılandırmak için, Sihirbazı başlatarak, veri kaynağını akıllı etiketinden yapılandırın bağlantısını seçin. İlk ekran, ObjectDataSource 'un bağlandığı temel nesneyi değiştirmenize olanak sağlar; `ProductsBLL`olarak ayarlı bırakın. Sonraki ekranda, ObjectDataSource 'un yöntemlerinden temel alınan nesnenin eşlemeleri listelenir. Açıkça `Insert()` ve `Delete()` yöntemlerinin herhangi bir yöntemle eşlenmediğine rağmen, ekleme ve SILME sekmelerine giderseniz, bir eşlemenin orada olduğunu görürsünüz. Bunun nedeni, `ProductsBLL``AddProduct` ve `DeleteProduct` yöntemlerinin sırasıyla `Insert()` ve `Delete()`için varsayılan yöntemler olduğunu göstermek için `DataObjectMethodAttribute` özniteliğini kullanmasına yöneliktir. Bu nedenle, başka bir değer açık olarak belirtilmediği takdirde ObjectDataSource Sihirbazı her çalıştırdığınızda bunları seçer.

`AddProduct` yöntemine işaret eden `Insert()` yöntemini bırakın, ancak SIL sekmesinin açılan listesini (None) olarak ayarlayın.

[INSERT sekmesinin açılan listesini AddProduct yöntemine ayarlayın ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image40.png)

**Şekil 14**: INSERT sekmesinin açılan listesini `AddProduct` yöntemine ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image42.png))

[SIL sekmesinin açılan listesini (yok) olarak ayarlamak ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image43.png)

**Şekil 15**: delete sekmesinin açılan listesini (yok) olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image45.png))

Bu değişiklikleri yaptıktan sonra, ObjectDataSource 'un bildirime dayalı sözdizimi, aşağıda gösterildiği gibi bir `InsertParameters` koleksiyonu içerecek şekilde genişletilir:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample8.aspx)]

Sihirbazın yeniden çalıştırılması `OldValuesParameterFormatString` özelliğini geri ekledi. Varsayılan değere ayarlayarak (`{0}`) veya bildirim temelli sözdiziminden tamamen kaldırarak bu özelliği temizlemek için bir dakikanızı ayırın.

Ekleme özellikleri sağlayan ObjectDataSource sayesinde, DetailsView 'un akıllı etiketi artık eklemeyi etkinleştir onay kutusunu içerecektir; Tasarımcıya dönün ve bu seçeneği işaretleyin. Daha sonra, DetailsView, yalnızca iki BoundFields-`ProductName` ve `UnitPrice`-ve CommandField olacak şekilde aşağı doğru. Bu noktada, DetailsView 'un bildirime dayalı sözdizimi şöyle görünmelidir:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample9.aspx)]

Şekil 16 Bu noktada bir tarayıcı aracılığıyla görüntülenirken bu sayfayı gösterir. Gördüğünüz gibi, DetailsView ilk ürünün adını ve fiyatını (Chai) listeler. Ancak, kullanıcının veritabanına hızlı bir şekilde yeni bir ürün eklemesi için bir yol sağlayan ekleme arabirimidir.

[DetailsView ![Şu anda salt okunurdur modda Işlenmiştir](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image46.png)

**Şekil 16**: DetailsView Şu anda salt okunurdur modda işlenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image48.png))

DetailsView 'ı ekleme modunda göstermek için `DefaultMode` özelliğini `Inserting`olarak ayarlamanız gerekir. Bu, ilk kez ziyaret edildiğinde DetailsView 'ı ekleme modunda işler ve yeni bir kayıt ekledikten sonra orada tutar. Şekil 17 ' de gösterildiği gibi, DetailsView Bu şekilde yeni bir kayıt eklemeye yönelik hızlı bir arabirim sağlar.

[DetailsView ![, hızlı bir şekilde yeni bir ürün eklemek için bir arabirim sağlar](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image49.png)

**Şekil 17**: DetailsView, hızlı bir şekilde yeni bir ürün eklemek Için bir arabirim sağlar ([tam boyutlu görüntüyü görüntülemek için tıklatın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image51.png))

Kullanıcı bir ürün adı ve fiyat girdiğinde (örneğin, şekil 17 ' de olduğu gibi "Acme su" ve 1,99 gibi) ve Ekle ' ye tıkladıktan sonra veritabanına eklenen yeni bir ürün kaydında bir geri gönderme ve ekleme iş akışı girer. DetailsView, Şekil 18 ' de gösterildiği gibi ekleme arabirimini korur ve GridView, yeni ürünü dahil etmek için veri kaynağına otomatik olarak yeniden bağlanır.

![Ürün](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image52.png)

**Şekil 18**: "Acme su" ürünü veritabanına eklendi

Şekil 18 ' deki GridView gösterilmediğinden, DetailsView arabiriminden (`CategoryID`, `SupplierID`, `QuantityPerUnit`vb.) bulunmayan ürün alanları `NULL` veritabanı değerleri atanır. Aşağıdaki adımları gerçekleştirerek bunu görebilirsiniz:

1. Visual Studio 'da Sunucu Gezgini git
2. `NORTHWND.MDF` veritabanı düğümünü genişletme
3. `Products` veritabanı tablosu düğümüne sağ tıklayın
4. Tablo verilerini göster ' i seçin

Bu, `Products` tablosundaki tüm kayıtları listeler. Şekil 19 ' da gösterildiği gibi, yeni ürünümüzün `ProductID`, `ProductName`ve `UnitPrice` dışındaki tüm sütunlarının `NULL` değerleri vardır.

[DetailsView 'da sağlanmayan ürün alanlarına ![NULL değerler atandı](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image53.png)

**Şekil 19**: DetailsView 'Da sağlanmayan ürün alanları `NULL` değerler atanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image55.png))

En iyi varsayılan seçenek olmadığından veya veritabanı sütununun kendisi `NULL` izin vermediğinden `NULL`, bu sütun değerlerinden biri veya daha fazlası için `NULL` dışında bir varsayılan değer sağlamak isteyebilir. Bunu gerçekleştirmek için, DetailsView 'un `InputParameters` koleksiyonunun parametrelerinin değerlerini programlı bir şekilde ayarlayabiliriz. Bu atama, DetailsView 'un `ItemInserting` olayı ya da ObjectDataSource 'un `Inserting` olayı için olay işleyicisinde yapılabilir. Veri Web Denetim düzeyinde ön ve son düzey olayları kullanmaya zaten baktığı için, bu kez ObjectDataSource 'un olaylarını kullanmayı inceleyelim.

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>4\. Adım:`CategoryID`ve`SupplierID`parametrelere değer atama

Bu öğreticide, bu arabirim aracılığıyla yeni bir ürün eklerken uygulamamız için `CategoryID` ve `SupplierID` değerinin 1 olarak atanması gerekir. Daha önce belirtildiği gibi, ObjectDataSource, veri değiştirme işlemi sırasında harekete geçen bir dizi ön ve son düzey olay içerir. `Insert()` yöntemi çağrıldığında, ObjectDataSource önce `Inserting` olayını oluşturur, sonra `Insert()` yönteminin eşlendiği yöntemini çağırır ve son olarak `Inserted` olayını başlatır. `Inserting` olay işleyicisi, giriş parametrelerini ince ayar için bir son fırsat sağlar veya işlemi geri yüklemeyi iptal eder.

> [!NOTE]
> Gerçek dünyada bir uygulamada büyük olasılıkla kullanıcının kategori ve tedarikçiyi belirtmesini sağlamak ya da bu değeri, bazı ölçütlere veya iş mantığına göre (1. KIMLIK belirlemek yerine) sizin için seçmesini isteyebilirsiniz. Bunun ne olursa olsun, bu örnekte, bir giriş parametresinin değerini, ObjectDataSource 'un ön seviye olayından programlama yoluyla nasıl ayarlayabileceği gösterilmektedir.

ObjectDataSource 'un `Inserting` olayı için bir olay işleyicisi oluşturmak için bir dakikanızı ayırın. Olay işleyicisinin ikinci giriş parametresinin, parametre koleksiyonuna (`InputParameters`) ve işlemi iptal etmek için bir özelliğe (`Cancel`) erişimi olan `ObjectDataSourceMethodEventArgs`türünde bir nesne olduğuna dikkat edin.

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample10.cs)]

Bu noktada, `InputParameters` özelliği,, DetailsView 'tan atanan değerlerle ObjectDataSource 'un `InsertParameters` koleksiyonunu içerir. Bu parametrelerden birinin değerini değiştirmek için yalnızca şunu kullanın: `e.InputParameters["paramName"] = value`. Bu nedenle `CategoryID` ayarlamak ve 1 değerlerine `SupplierID` için, `Inserting` olay işleyicisini aşağıdaki gibi olacak şekilde ayarlayın:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample11.cs)]

Bu kez yeni bir ürün eklenirken (Acme soda gibi), yeni ürünün `CategoryID` ve `SupplierID` sütunları 1 olarak ayarlanır (bkz. Şekil 20).

[![yeni ürünlerin CategoryID ve SupplierID değerleri 1 olarak ayarlanmıştır](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image56.png)

**Şekil 20**: yeni ürünlerin artık `CategoryID` ve `SupplierID` değerleri 1 olarak ayarlanmış ([tam boyutlu görüntüyü görüntülemek için tıklatın](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image58.png))

## <a name="summary"></a>Özet

Oluşturma, ekleme ve silme işlemleri sırasında hem veri Web denetimi hem de ObjectDataSource, bir dizi ön ve son düzey olay üzerinden devam edecek. Bu öğreticide, ön seviye olayları inceledi ve veri Web denetiminden ve ObjectDataSource 'un olaylarından her ikisi de veri değiştirme işlemini nasıl iptal edebileceğinizi gördünüz. Sonraki öğreticide, son düzey olaylar için olay işleyicileri oluşturma ve kullanma bölümüne bakacağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Jackie Goor ve Liz Shulok. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](an-overview-of-inserting-updating-and-deleting-data-cs.md)
> [İleri](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
