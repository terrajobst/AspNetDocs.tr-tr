---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
title: Veri ekleme, güncelleştirme ve silmeye genel bakış (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, bir ObjectDataSource 'un Insert (), Update () ve Delete () yöntemlerini BLL sınıflarının yöntemlerine ve configu... ile nasıl eşleneceğini öğreneceksiniz.
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 35b40b8f-2ca8-4ab3-9c19-f361a91a3647
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 79491118ba1cbbc8c1b67ca9646a817d941f17ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78609636"
---
# <a name="an-overview-of-inserting-updating-and-deleting-data-vb"></a>Veri ekleme, güncelleştirme ve silmeye genel bakış (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_VB.exe) veya [PDF 'yi indirin](an-overview-of-inserting-updating-and-deleting-data-vb/_static/datatutorial16vb1.pdf)

> Bu öğreticide, bir ObjectDataSource 'un Insert (), Update () ve Delete () yöntemlerini BLL sınıflarının yöntemlerine eşlemeyi ve veri değiştirme özellikleri sağlamak için GridView, DetailsView ve FormView denetimlerini yapılandırmayı öğreneceksiniz.

## <a name="introduction"></a>Giriş

Son birkaç öğreticilerde, GridView, DetailsView ve FormView denetimlerini kullanarak verileri bir ASP.NET sayfasında görüntülemeyi inceledik. Bu denetimler yalnızca bunlara verilen verilerle çalışır. Genellikle, bu denetimler, ObjectDataSource gibi bir veri kaynağı denetimi kullanılarak verilere erişir. ObjectDataSource 'un ASP.NET sayfası ve temel alınan veriler arasında bir ara sunucu olarak nasıl davranması gerektiğini gördük. Bir GridView 'un verileri görüntülemesi gerektiğinde, onun ObjectDataSource 'un `Select()` yöntemini çağırır. Bu, uygun veri erişim katmanının (DAL) TableAdapter ' de bir yöntemi çağıran ve bu da Northwind veritabanına `SELECT` bir sorgu gönderen Iş mantığı katmanımızda (BLL) bir yöntemi çağıran Iş mantığı katmanımız bir yöntemi çağırır.

[İlk öğreticimizde](../introduction/creating-a-data-access-layer-cs.md)dal içinde TableAdapters oluşturduğumuzda, Visual Studio temel veritabanı tablosundan veri ekleme, güncelleştirme ve silme yöntemlerini otomatik olarak eklemiştir. Ayrıca, [bir Iş mantığı katmanı oluşturmak](../introduction/creating-a-business-logic-layer-vb.md) için bu VERI değişikliği dal yöntemlerine çağrılan BLL 'de Yöntemler tasarlıyoruz.

`Select()` metoduna ek olarak, ObjectDataSource da `Insert()`, `Update()`ve `Delete()` yöntemlerine sahiptir. `Select()` yöntemi gibi, bu üç yöntem temel bir nesne içindeki yöntemlerle eşleştirilebilir. Veri eklemek, güncelleştirmek veya silmek için yapılandırıldığında, GridView, DetailsView ve FormView denetimleri, temel alınan verileri değiştirmek için bir kullanıcı arabirimi sağlar. Bu Kullanıcı arabirimi, ObjectDataSource 'un temel nesnenin ilişkili yöntemlerini çağıran `Insert()`, `Update()`ve `Delete()` yöntemlerini çağırır (bkz. Şekil 1).

[ObjectDataSource 'un Insert (), Update () ve Delete () yöntemleri, BLL 'e bir proxy olarak görev yapar ![](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image1.png)

**Şekil 1**: ObjectDataSource 'un `Insert()`, `Update()`ve `Delete()` yöntemleri BLL 'e bir proxy olarak görev yapar ([tam boyutlu görüntüyü görüntülemek için tıklatın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image3.png))

Bu öğreticide, ObjectDataSource 'un `Insert()`, `Update()`ve `Delete()` yöntemlerini BLL içindeki sınıf yöntemlerine nasıl eşleneceğini ve veri değiştirme özellikleri sağlamak için GridView, DetailsView ve FormView denetimlerini nasıl yapılandıracağınızı öğreneceksiniz.

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>Adım 1: ekleme, güncelleştirme ve silme öğreticileri Web sayfalarını oluşturma

Verileri ekleme, güncelleştirme ve silme konusunda keşfetmeye başlamadan önce, Web sitesi projemizdeki Bu öğretici ve sonraki birkaç işlem için gereken ASP.NET sayfalarını oluşturmak için biraz zaman atalım. `EditInsertDelete`adlı yeni bir klasör ekleyerek başlayın. Ardından, aşağıdaki ASP.NET sayfalarını bu klasöre ekleyerek her bir sayfayı `Site.master` ana sayfasıyla ilişkilendirdiğinizden emin olun:

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![Veri değişikliği ile Ilgili öğreticiler için ASP.NET sayfaları ekleyin](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image4.png)

**Şekil 2**: veri değişikliği Ile ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `EditInsertDelete` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfanın Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image5.png)

**Şekil 3**: `Default.aspx` `SectionLevelTutorialListing.ascx` Kullanıcı denetimini ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image7.png))

Son olarak, sayfaları `Web.sitemap` dosyasına girdi olarak ekleyin. Özel olarak, özelleştirilmiş biçimlendirme `<siteMapNode>`sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık öğreticilerin düzenlenmesine, eklemeye ve silinmesine yönelik öğeler içerir.

![Site Haritası artık öğreticilerin düzenlenmesine, eklemeye ve silinmesine yönelik girdiler Içerir](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image8.png)

**Şekil 4**: site haritası artık öğreticilerin düzenlenmesine, eklemeye ve silinmesine yönelik girdiler içerir

## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>2\. Adım: ObjectDataSource denetimini ekleme ve yapılandırma

GridView, DetailsView ve FormView her biri veri değiştirme özelliklerine ve düzenine göre farklılık gösterdiğinden her birini ayrı ayrı inceleyelim. Ancak, her bir denetimin kendi ObjectDataSource 'u kullanmasını sağlamak yerine, yalnızca üç denetim örneklerinin paylaştığı tek bir ObjectDataSource oluşturalım.

`Basics.aspx` sayfasını açın, araç kutusu ' ndan tasarımcı üzerine bir ObjectDataSource sürükleyin ve akıllı etiketinden veri kaynağını Yapılandır bağlantısına tıklayın. `ProductsBLL`, ekleme, ekleme ve silme yöntemleri sağlayan tek BLL sınıfı olduğundan, bu sınıfı kullanmak için ObjectDataSource 'u yapılandırın.

[![, ObjectDataSource 'ı ProductsBLL sınıfını kullanacak şekilde yapılandırma](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image9.png)

**Şekil 5**: ObjectDataSource 'ı `ProductsBLL` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image11.png))

Sonraki ekranda, uygun sekmeyi seçerek ve açılan listeden yöntemi seçerek `ProductsBLL` sınıfının hangi yöntemlerin `Select()`, `Insert()`, `Update()`ve `Delete()` eşleştirildiği belirtilebilir. Şekil 6 ' da şu anda tanıdık gelmelidir, ObjectDataSource 'un `Select()` yöntemini `ProductsBLL` sınıfının `GetProducts()` yöntemiyle eşler. `Insert()`, `Update()`ve `Delete()` yöntemleri en üstteki listeden uygun sekme seçilerek yapılandırılabilir.

[![, ObjectDataSource 'un tüm ürünleri döndürmesini](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image12.png)

**Şekil 6**: ObjectDataSource 'un tüm ürünleri döndürmesini sağlamak ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image14.png))

Şekil 7, 8 ve 9, ObjectDataSource 'un GÜNCELLEŞTIRME, ekleme ve SILME sekmelerini gösterir. `Insert()`, `Update()`ve `Delete()` yöntemlerinin sırasıyla `ProductsBLL` sınıfının `UpdateProduct`, `AddProduct`ve `DeleteProduct` yöntemlerini çağırması için bu sekmeleri yapılandırın.

[![ObjectDataSource 'un Update () yöntemini ProductBLL sınıfının UpdateProduct yöntemiyle eşleyin](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image15.png)

**Şekil 7**: ObjectDataSource 'un `Update()` yöntemini `ProductBLL` sınıfının `UpdateProduct` yöntemiyle eşleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image17.png))

[![ObjectDataSource 'un Insert () metodunu ProductBLL sınıfının AddProduct yöntemine eşleyin](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image18.png)

**Şekil 8**: ObjectDataSource 'un `Insert()` yöntemini `ProductBLL` sınıfının Add `Product` yöntemine eşleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image20.png))

[![ObjectDataSource 'un Delete () yöntemini ProductBLL sınıfının DeleteProduct yöntemine eşleyin](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image21.png)

**Şekil 9**: ObjectDataSource 'un `Delete()` yöntemini `ProductBLL` sınıfının `DeleteProduct` yöntemiyle eşleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image23.png))

GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listelerin bu yöntemlerin zaten seçili olduğunu fark etmiş olabilirsiniz. Bu, `ProductsBLL`yöntemlerini süsleden `DataObjectMethodAttribute` kullanımı için teşekkürler. Örneğin, DeleteProduct yöntemi aşağıdaki imzaya sahiptir:

[!code-vb[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample2.vb)]

`DataObjectMethodAttribute` özniteliği, her yöntemin, seçme, ekleme, güncelleştirme veya silme için olup olmadığını ve varsayılan değer olup olmadığını gösterir. BLL sınıflarınızı oluştururken bu öznitelikleri atlarsanız, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden yöntemleri el ile seçmeniz gerekir.

Uygun `ProductsBLL` yöntemlerinin ObjectDataSource 'un `Insert()`, `Update()`ve `Delete()` yöntemlerine eşlendiğinden emin olduktan sonra, Sihirbazı tamamladıktan sonra son ' a tıklayın.

## <a name="examining-the-objectdatasources-markup"></a>ObjectDataSource 'un Işaretlemesini İnceleme

ObjectDataSource 'u Sihirbazı aracılığıyla yapılandırdıktan sonra, oluşturulan bildirim işaretlemesini incelemek için kaynak görünümüne gidin. `<asp:ObjectDataSource>` etiketi, temel alınan nesneyi ve çağrılacak yöntemleri belirtir. Ayrıca, `ProductsBLL` sınıfının `AddProduct`, `UpdateProduct`ve `DeleteProduct` yöntemlerine yönelik giriş parametreleriyle eşlenen `DeleteParameters`, `UpdateParameters`ve `InsertParameters` vardır:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample3.aspx)]

ObjectDataSource, ObjectDataSource, bir giriş parametresi bekleyen bir Select yöntemi çağırmak üzere yapılandırıldığında (örneğin, `GetProductsByCategoryID(categoryID)`) bir `SelectParameter` liste gibi, ilişkili yöntemlerin her bir giriş parametresi için bir parametre içerir. Kısa süre içinde, bu `DeleteParameters`, `UpdateParameters`ve `InsertParameters` değerleri, ObjectDataSource 'un `Insert()`, `Update()`veya `Delete()` yöntemi çağırmadan önce GridView, DetailsView ve FormView tarafından otomatik olarak ayarlanır. Bu değerler, gelecekteki öğreticide tartıştığımız için gerektiğinde programlama yoluyla da ayarlanabilir.

ObjectDataSource 'a yapılandırmak için Sihirbazı kullanmanın bir yan etkisi, Visual Studio 'Nun [OldValuesParameterFormatString özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx) `original_{0}`olarak ayarlamadır. Bu özellik değeri, düzenlenmekte olan verilerin orijinal değerlerini dahil etmek için kullanılır ve iki senaryoda faydalıdır:

- Bir kayıt düzenlenirken, kullanıcılar birincil anahtar değerini değiştirebilir. Bu durumda, özgün birincil anahtar değerine sahip kaydın bulunabilmesi ve değerinin uygun şekilde güncelleştirilmesini sağlamak için hem yeni birincil anahtar değeri hem de orijinal birincil anahtar değeri sağlanmalıdır.
- İyimser eşzamanlılık kullanılırken. İyimser eşzamanlılık, iki eşzamanlı kullanıcının başka bir değişiklik yaptığı değişikliğin üzerine yazılmayacağı ve gelecekteki öğreticinin konusu olduğundan emin olmak için kullanılan bir tekniktir.

`OldValuesParameterFormatString` özelliği, orijinal değerler için temeldeki nesnenin Update ve DELETE metotlarındaki giriş parametrelerinin adını gösterir. İyimser eşzamanlılık keşfettiğimiz zaman bu özelliği ve amacını daha ayrıntılı olarak ele alacağız. Ancak, BLL 'nin yöntemleri özgün değerleri beklemediği ve bu nedenle bu özelliği kaldırdığımızdan önemli olduğundan, şimdi kullanıma sundum. `OldValuesParameterFormatString` özelliği varsayılandan farklı bir değere (`{0}`) ayrıldığınızda, ObjectDataSource bir veri Web denetimi, hem `UpdateParameters` hem de `DeleteParameters` belirtilen ve özgün değer parametrelerine geçiş yapmayı deneyeceğinden, ObjectDataSource 'un `Update()` veya `Delete()` yöntemlerini çağırmayı denediğinde bir hataya neden olur.

Bu juncture 'de böyle bir kaymayın yoksa, bu özelliği ve yardımcı programını gelecekteki bir öğreticide inceleyeceğiz. Şimdilik, bu özellik bildirimini bildirime dayalı sözdiziminden kaldırmak ya da değeri varsayılan değer ({0}) olarak ayarlamanız yeterlidir.

> [!NOTE]
> Tasarım görünümü Özellikler penceresi `OldValuesParameterFormatString` özellik değerini yalnızca bir temizlerseniz, özellik bildirime dayalı sözdiziminde kalır, ancak boş bir dizeye ayarlanır. Bu, ne yazık ki yukarıda açıklanan soruna neden olur. Bu nedenle, özelliği bildirime dayalı sözdiziminden tamamen kaldırın ya da Özellikler penceresi, değeri varsayılan olan `{0}`olarak ayarlayın.

## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>3\. Adım: veri Web denetimi ekleme ve veri değişikliği için yapılandırma

ObjectDataSource, sayfaya eklendikten ve yapılandırıldıktan sonra verileri göstermek için sayfaya veri Web denetimleri eklemeye hazırız ve son kullanıcının bunu değiştirmesi için bir yol sağlar. Bu veri Web denetimleri, veri değiştirme özellikleri ve yapılandırmasında farklılık gösterdiği için GridView, DetailsView ve FormView 'e ayrı olarak bakacağız.

Bu makalenin geri kalanında göreceğiniz gibi, GridView, DetailsView ve FormView denetimleri aracılığıyla basit düzenlemeler, ekleme ve silme desteğinin eklenmesi, birkaç onay kutusunun denetlenmesi açısından oldukça basittir. Gerçek dünyada, bu tür işlevselliği yalnızca noktadan daha fazlasını sağlayan çok sayıda alt tzellikleri ve uç durumu vardır ve tıklamaları yeterlidir. Ancak, bu öğretici yalnızca uyarlaması veri değiştirme özelliklerine odaklanır. Gelecekteki öğreticiler, gerçek dünyada bir ayarda ortaya çıkabilecek kaygıları inceler.

## <a name="deleting-data-from-the-gridview"></a>GridView 'dan verileri silme

Araç kutusundan Tasarımcı üzerine bir GridView sürükleyip başlayın. Ardından, GridView 'un akıllı etiketindeki aşağı açılan listeden seçerek ObjectDataSource 'u GridView 'a bağlayın. Bu noktada, GridView 'un bildirim temelli biçimlendirme şu şekilde olacaktır:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample4.aspx)]

GridView 'un akıllı etiketiyle ObjectDataSource 'a bağlanması iki avantaja sahiptir:

- ObjectDataSource tarafından döndürülen alanların her biri için BoundFields ve CheckBoxFields otomatik olarak oluşturulur. Üstelik, BoundField ve CheckBoxField 'ın özellikleri, temel alınan alanın meta verilerine göre ayarlanır. Örneğin, `ProductID`, `CategoryName`ve `SupplierName` alanları `ProductsDataTable` salt okuma olarak işaretlenir ve bu nedenle, düzenlenirken güncelleştirilemez. Buna uyum sağlamak için, bu BoundFields ' [ReadOnly özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx) `True`olarak ayarlanır.
- [DataKeyNames özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx) , temel alınan nesnenin birincil anahtar alanları ' na atanır. Bu özellik, verileri düzenlenmek veya silmek için GridView kullanılırken gereklidir. Bu özellik, her kaydı benzersiz bir şekilde tanımlayan alanı (veya alan kümesini) gösterir. `DataKeyNames` özelliği hakkında daha fazla bilgi için, [ayrıntı ayrıntısı görünümü öğreticisiyle seçilebilir bir ana GridView kullanarak ana/ayrıntı](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) bölümüne bakın.

GridView, Özellikler penceresi veya bildirime dayalı sözdizimi aracılığıyla ObjectDataSource 'a bağlanabilir ancak bunu yapmak uygun BoundField ve `DataKeyNames` işaretlemesini el ile eklemenizi gerektirir.

GridView denetimi, satır düzeyinde Düzenle ve silme için yerleşik destek sağlar. Bir GridView 'yi silmeyi desteklemek için yapılandırmak, silme düğmelerinin bir sütununu ekler. Son Kullanıcı belirli bir satır için Sil düğmesine tıkladığında, bir geri gönderme ve GridView aşağıdaki adımları gerçekleştirir:

1. ObjectDataSource 'un `DeleteParameters` değerleri atandı
2. ObjectDataSource 'un `Delete()` yöntemi çağrıldı, belirtilen kayıt siliniyor
3. GridView, `Select()` yöntemini çağırarak kendisini ObjectDataSource 'a yeniden bağlar

`DeleteParameters` atanan değerler, silme düğmesine tıklanmış olan satırın `DataKeyNames` alan değerlerdir. Bu nedenle, bir GridView 'ın `DataKeyNames` özelliğinin doğru şekilde ayarlanması çok önemlidir. Eksik ise, `DeleteParameters` adım 1 ' de bir `Nothing` değeri atanır. Bu, sırasıyla adım 2 ' de silinen kayıtlar ile sonuçlanmaz.

> [!NOTE]
> `DataKeys` koleksiyonu, GridView s denetim durumunda depolanır, yani GridView s görünüm durumu devre dışı bırakılsa bile `DataKeys` değerlerinin geri gönderme üzerinden anımsanacak anlamına gelir. Ancak, görüntüleme durumunun, Düzenle veya silmeyi destekleyen GridViews için etkin kalacağı (varsayılan davranış) çok önemlidir. GridView s `EnableViewState` özelliğini `false`olarak ayarlarsanız, düzenleme ve silme davranışı tek bir kullanıcı için ince çalışır, ancak verileri silen eşzamanlı kullanıcılar varsa, bu eş zamanlı kullanıcıların, istemediğiniz kayıtları yanlışlıkla silmesine veya düzenlemesine olanak sağlar. Daha fazla bilgi için bkz. blog Girişmi, [Uyarı: ASP.NET 2,0 GridViews/DetailsView/formviews ile, görüntüleme ve/veya silme ve görüntüleme durumunu devre dışı bırakma desteği ve/veya silmeyi destekleyen ve](http://scottonwriting.net/sowblog/posts/10054.aspx)

Aynı uyarı, Ayrıntılar görünümleri ve form görünümleri için de geçerlidir.

GridView 'a silme özellikleri eklemek için akıllı etiketine gitmeniz ve silmeyi etkinleştir onay kutusunu işaretlemeniz yeterlidir.

![Silmeyi etkinleştir onay kutusunu işaretleyin](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image24.png)

**Şekil 10**: silmeyi etkinleştir onay kutusunu işaretleyin

Akıllı etiketteki silmeyi etkinleştir onay kutusunun işaretlenmesi GridView 'a bir CommandField ekler. CommandField, GridView 'da aşağıdaki görevlerden birini veya birkaçını gerçekleştirmeye yönelik düğmeler içeren bir sütun oluşturur: bir kayıt seçme, bir kaydı düzenlemeyle ve bir kaydı silme. [Ayrıntı ayrıntısı görünümü öğreticisiyle seçilebilir bir Master GridView kullanarak ana/ayrıntı](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) içindeki kayıtları seçerken daha önce CommandField ' i bir eylemde gördünüz.

CommandField, CommandField 'da hangi düğme serilerinin görüntülendiğini belirten bir dizi `ShowXButton` özelliği içerir. Silmeyi etkinleştir onay kutusunu işaretleyerek `ShowDeleteButton` özelliği `True` GridView 'un Columns koleksiyonuna eklenmiş olan bir CommandField.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample5.aspx)]

Bu noktada, GridView 'a silme desteği eklemekle karşılaşıyoruz! Şekil 11 ' de gösterildiği gibi, bu sayfayı bir tarayıcı aracılığıyla ziyaret ettiğinizde silme düğmelerinin bir sütunu bulunur.

[![CommandField, silme düğmelerinin bir sütununu ekler](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image25.png)

**Şekil 11**: CommandField, silme düğmelerinin bir sütununu ekler ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image27.png))

Bu öğreticiyi baştan sona oluşturuyorsanız, bu sayfayı test ederken Sil düğmesine tıkladığınızda bir özel durum oluşturulur. Bu özel durumların neden ortaya çıkarıldığına ve bunları nasıl düzelteceğinizi öğrenmek için okumaya devam edin.

> [!NOTE]
> Bu öğreticiye eşlik eden indirmeyi kullanarak takip ediyorsanız, bu sorunlar için zaten bir hesaba katılmış demektir. Ancak, oluşabilecek sorunları ve uygun geçici çözümleri belirlemenize yardımcı olmak için aşağıda listelenen ayrıntıları okumanız önerilir.

Bir ürünü silmeye çalışırken, iletisi "ObjectDataSource ' ObjectDataSource1 ' şuna benzer bir özel durum alırsınız *: ProductID, orijinal\_ProductID*,", `OldValuesParameterFormatString` özelliğini ObjectDataSource 'tan kaldırmayı unutmuş olabilirsiniz. Bu özellik, "". `OldValuesParameterFormatString` özelliği belirtildiğinde, ObjectDataSource `productID` ve `original_ProductID` giriş parametrelerini `DeleteProduct` yöntemine geçirmeye çalışır. Ancak `DeleteProduct`, bu nedenle özel durum yalnızca tek bir giriş parametresini kabul eder. `OldValuesParameterFormatString` özelliğini kaldırma (veya `{0}`olarak ayarlama), ObjectDataSource 'un özgün giriş parametresini geçirmeye kalkışmasını söyler.

[![OldValuesParameterFormatString özelliğinin temizlendiğinden emin olun](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image28.png)

**Şekil 12**: `OldValuesParameterFormatString` özelliğinin temizlendiğinden emin olun ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image30.png))

`OldValuesParameterFormatString` özelliğini kaldırmış olsanız bile, şu iletiyle bir ürün silmeye çalışırken bir özel durum alacaksınız: "*Delete IFADESINI başvuru kısıtlaması ile çakıştı ' FK\_Order\_ayrıntılar\_Ürünler '* ." Northwind veritabanı, `Order Details` ve `Products` tablo arasında bir yabancı anahtar kısıtlaması içerir, yani `Order Details` tablosunda bu için bir veya daha fazla kayıt varsa, bir ürünün sistemden silinemeyeceği anlamına gelir. Northwind veritabanındaki her üründe `Order Details`en az bir kayıt olduğundan, ürünün ilişkili sipariş ayrıntıları kayıtlarını ilk silene kadar hiçbir ürünü silemiyoruz.

[Yabancı anahtar kısıtlaması ![ürünlerin silinmesini yasaklar](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image31.png)

**Şekil 13**: yabancı anahtar kısıtlaması ürünlerin silinmesini yasaklar ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image33.png))

Öğreticimiz için `Order Details` tablosundan yalnızca tüm kayıtları silelim. Gerçek dünyada bir uygulamada şunlardan birini yapmanız gerekir:

- Sipariş ayrıntıları bilgilerini yönetmek için başka bir ekrana sahip
- `DeleteProduct` yöntemini, belirtilen ürünün sıra ayrıntılarını silme mantığını içerecek şekilde artırmak
- TableAdapter tarafından belirtilen ürünün sıra ayrıntılarının silinmesini dahil etmek için kullanılan SQL sorgusunu değiştirin

Yabancı anahtar kısıtlamasını aşmak için `Order Details` tablodaki tüm kayıtları silelim. Visual Studio 'daki Sunucu Gezgini gidin, `NORTHWND.MDF` düğümüne sağ tıklayın ve yeni sorgu ' yı seçin. Ardından, sorgu penceresinde şu SQL ifadesini çalıştırın: `DELETE FROM [Order Details]`

[Tüm kayıtları Sipariş Ayrıntıları tablosundan silmek ![](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image34.png)

**Şekil 14**: `Order Details` tablosundan tüm kayıtları silme ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image36.png))

`Order Details` tablosu kapatıldıktan sonra Sil düğmesine tıklandığında ürün hatasız olarak silinir. Sil düğmesine tıkladığınızda ürün silinmez, GridView 'ın `DataKeyNames` özelliğinin birincil anahtar alanı (`ProductID`) olarak ayarlandığından emin olun.

> [!NOTE]
> Sil düğmesine tıkladığınızda geri gönderme işlemi başarılı olur ve kayıt silinir. Bu, yanlışlıkla yanlış satırın silme düğmesine tıklamasından dolayı tehlikeli olabilir. Gelecekte bir öğreticide, bir kayıt silinirken istemci tarafı onayı ekleme hakkında bilgi edineceksiniz.

## <a name="editing-data-with-the-gridview"></a>GridView ile verileri düzenlemeyle

GridView denetimi, silme işlemiyle birlikte yerleşik satır düzeyinde yapılandırma desteği de sağlar. Düzenlemeyi desteklemek için GridView yapılandırmak, düzenleme düğmelerinin bir sütununu ekler. Son kullanıcının perspektifinden, bir satırın düzenleme düğmesine tıklamak, bu satırın düzenlenebilir hale gelmesine neden olur. Bu, hücreleri var olan değerleri içeren metin kutularına açıp Düzenle ve Iptal düğmeleri ile değiştirin. İstenen değişiklikler yapıldıktan sonra, Son Kullanıcı değişiklikleri yürütmek için Güncelleştir düğmesine tıklayabilir veya Iptal düğmesine tıklayarak bunları atabilirsiniz. Her iki durumda da Güncelleştir ' e tıkladıktan sonra GridView ' ı Iptal ettikten sonra, önceden düzenlenen durumuna geri döner.

Sayfa geliştiricisi olarak bakıldığında, Son Kullanıcı belirli bir satır için Düzenle düğmesine tıkladığında, geri gönderme ve GridView aşağıdaki adımları gerçekleştirir:

1. GridView 'ın `EditItemIndex` özelliği, Düzenle düğmesine tıklandığı satırın dizinine atanır
2. GridView, `Select()` yöntemini çağırarak kendisini ObjectDataSource 'a yeniden bağlar
3. `EditItemIndex` eşleşen satır dizini "düzenleme modunda" işlenir. Bu modda, Düzenle düğmesi güncelleştir ve Iptal düğmeleri ve `ReadOnly` özellikleri false olan BoundFields (varsayılan), `Text` özellikleri veri alanlarının değerlerine atanmış olan TextBox Web denetimleri olarak işlenir.

Bu noktada, biçimlendirme tarayıcıya döndürülür ve son kullanıcının satır verilerinde herhangi bir değişiklik yapmasına izin verilir. Kullanıcı Update düğmesine tıkladığında bir geri gönderme gerçekleşir ve GridView aşağıdaki adımları gerçekleştirir:

1. ObjectDataSource 'un `UpdateParameters` değerlere, son kullanıcı tarafından, GridView 'un düzenlenme arabirimine girilen değerler atanır
2. ObjectDataSource 'un `Update()` yöntemi çağrıldı, belirtilen kayıt güncelleştiriliyor
3. GridView, `Select()` yöntemini çağırarak kendisini ObjectDataSource 'a yeniden bağlar

Adım 1 ' deki `UpdateParameters` atanan birincil anahtar değerleri `DataKeyNames` özelliğinde belirtilen değerlerden gelir, ancak birincil olmayan anahtar değerleri düzenlenen satır için metin kutusu Web denetimlerinde bulunan metinden gelir. Silme sırasında, GridView 'un `DataKeyNames` özelliğinin doğru şekilde ayarlanması çok önemlidir. Eksik ise, `UpdateParameters` birincil anahtar değerine, 1. adımda bir `Nothing` değeri atanır. Bu, sırasıyla 2. adımda güncelleştirilmiş kayıtlar oluşmasına neden olmaz.

Düzen işlevselliği, GridView 'un akıllı etiketindeki Düzenle etkinleştir onay kutusunu işaretleyerek etkinleştirilebilir.

![Düzenle etkinleştir onay kutusunu işaretleyin](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image37.png)

**Şekil 15**: Düzenle etkinleştir onay kutusunu işaretleyin

Düzenle etkinleştir onay kutusunun işaretlenmesi bir CommandField (gerekliyse) ekler ve `ShowEditButton` özelliğini `True`olarak ayarlar. Daha önce gördüğümüz gibi, CommandField, CommandField 'da hangi düğme serilerinin görüntülendiğini belirten bir dizi `ShowXButton` özellik içerir. Düzenlemenizi etkinleştir onay kutusunun işaretlenmesi, `ShowEditButton` özelliğini var olan CommandField öğesine ekler:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample6.aspx)]

Bu, ilkel düzenlemesi desteği eklemek için gereklidir. Figure16 gösterdiği gibi, düzen arabirimi her bir BoundField 'ın `ReadOnly` özelliği `False` olarak ayarlanmış olan (varsayılan) bir metin kutusu olarak işlenir. Bu, diğer tablolara yönelik anahtarlar olan `CategoryID` ve `SupplierID`gibi alanları içerir.

[Chai s Düzenle düğmesine tıklamak ![satırı düzenleme modunda görüntüler](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image38.png)

**Şekil 16**: Chai s Düzenle düğmesine tıkladığınızda satır düzenleme modunda görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image40.png))

Kullanıcıların yabancı anahtar değerlerini doğrudan düzenlemesini isteme ek olarak, düzenleme arabiriminin arabirimi aşağıdaki yollarla desteklenmez:

- Kullanıcı, veritabanında var olmayan bir `CategoryID` veya `SupplierID` girerse, `UPDATE` yabancı anahtar kısıtlamasını ihlal eder ve bir özel durum ortaya çıkar.
- Düzen arabirimi herhangi bir doğrulama içermez. Gerekli bir değer (`ProductName`gibi) sağlamazsanız veya sayısal bir değerin beklenildiği bir dize değeri girebilirsiniz (örneğin, "çok fazla!" gibi) `UnitPrice` metin kutusuna) bir özel durum oluşturulur. Gelecekteki bir öğreticide, düzenlenen Kullanıcı arabirimine doğrulama denetimleri eklemeyi inceleyeceksiniz.
- Şu anda, salt okuma olmayan *Tüm* ürün alanları GridView 'a eklenmelidir. GridView 'dan bir alanı kaldırdığımızda, verileri güncelleştirirken `UnitPrice`söyleyin, GridView, veritabanı kaydının `UnitPrice` bir `NULL` değere değiştirecek `UnitPrice` `UpdateParameters` değerini ayarlayamaz. Benzer şekilde, `ProductName`gibi gerekli bir alan GridView 'tan kaldırılırsa, güncelleştirme aynı "*ProductName ' sütunu, yukarıda bahsedilen null değerlere izin*vermiyor" olarak da başarısız olur.
- Düzen arabirimi biçimlendirmesi, istenen kadar çok bırakır. `UnitPrice` dört ondalık noktayla gösterilir. İdeal olarak `CategoryID` ve `SupplierID` değerleri, sistemdeki kategorileri ve tedarikçileri listeleyen DropDownLists içerir.

Bunlar şimdilik ile canlı olarak sunduğumuz tüm eksiketler, ancak gelecekteki öğreticilerde değinilecek.

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>DetailsView ile veri ekleme, düzenlememe ve silme

Önceki öğreticilerde gördüğünüze göre, DetailsView denetimi aynı anda bir kayıt görüntüler ve GridView gibi, görüntülenmekte olan kaydın düzenlenmesine ve silinmesine izin verir. Son kullanıcının her ikisi de bir DetailsView 'dan öğe düzenlemeyle ve silinirken ve ASP.NET taraftan iş akışının bulunduğu deneyimle aynıdır. DetailsView, GridView 'tan farklı olduğunda, yerleşik ekleme desteği de sağlar.

GridView 'un veri değiştirme yeteneklerini göstermek için, var olan GridView 'un üzerindeki `Basics.aspx` sayfasına bir DetailsView ekleyerek başlayın ve DetailsView 'un akıllı etiketi aracılığıyla mevcut ObjectDataSource 'a bağlayın. Ardından, DetailsView 'un `Height` ve `Width` özelliklerini temizleyin ve akıllı etiketteki disk belleğini etkinleştir seçeneğini işaretleyin. Düzenle, ekleme ve silme desteğini etkinleştirmek için, akıllı etiketteki düzenlemenizi etkinleştir, ekleme ve onay kutularını silmeyi etkinleştir ' i kontrol edin.

![DetailsView 'u Düzenle, ekleniyor ve silmeyi destekleyecek şekilde yapılandırma](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image41.png)

**Şekil 17**: DetailsView 'u Düzenle, ekleniyor ve silmeyi destekleyecek şekilde yapılandırma

GridView 'da olduğu gibi, Düzenle, ekleme veya silme desteği eklemek, aşağıdaki bildirime dayalı sözdizimi gösterdiği gibi, DetailsView öğesine bir CommandField ekler:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample7.aspx)]

DetailsView için, CommandField 'ın varsayılan olarak Columns koleksiyonunun sonunda göründüğünü unutmayın. DetailsView 'un alanları satır olarak işlendiği için, CommandField, DetailsView 'un alt kısmındaki INSERT, Edit ve DELETE düğmeleriyle bir satır olarak görünür.

[DetailsView 'u Düzenle, ekleniyor ve silmeyi destekleyecek şekilde yapılandırma ![](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image42.png)

**Şekil 18**: DetailsView 'ı düzenlemesini, eklemeyi ve silmeyi destekleyecek şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image44.png))

Sil düğmesine tıklamak GridView ile aynı olay dizisini başlatır: geri gönderme; ardından DetailsView, `DataKeyNames` değerlerine göre ObjectDataSource 'un `DeleteParameters` yerleştirerek ve, ObjectDataSource 'un, gerçekten de ürünü veritabanından kaldıran `Delete()` yöntemini çağırır. DetailsView 'da düzenlemenin yanı sıra GridView ile aynı şekilde de bir daha kullanılır.

Ekleme için son kullanıcıya, tıklandığı zaman "ekleme modunda" DetailsView 'u oluşturduğu yeni bir düğme sunulur. "INSERT Mode" ile yeni düğme INSERT ve Cancel düğmeleriyle ve yalnızca `InsertVisible` özelliği `True` (varsayılan) olarak ayarlanmış olan BoundFields ile değiştirilmiştir. `ProductID`gibi otomatik artış alanları olarak tanımlanan bu veri alanları, DetailsView 'un, akıllı etiket aracılığıyla veri kaynağına bağlanırken `False` [olarak ayarlanmış.](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx)

Bir veri kaynağını akıllı etiket aracılığıyla bir DetailsView 'a bağlarken, Visual Studio `InsertVisible` özelliğini yalnızca otomatik artış alanları için `False` olarak ayarlar. `CategoryName` ve `SupplierName`gibi salt okuma alanları, `InsertVisible` özelliği açıkça `False`olarak ayarlanmadığı takdirde "ekleme modu" Kullanıcı arabiriminde görüntülenir. Bu iki alanın `InsertVisible` özelliklerini, DetailsView 'un bildirime dayalı sözdizimi aracılığıyla veya akıllı etiketteki alanları Düzenle bağlantısı aracılığıyla `False`olarak ayarlamak için bir dakikanızı ayırın. Şekil 19 `InsertVisible` özelliklerini `False` olarak ayarlamayı gösterir alanları Düzenle bağlantısına tıklayın.

[![Northwind Traders artık Acme Tea sunuyor](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image45.png)

**Şekil 19**: Northwind Traders artık Acme Tea sunuyor ([tam boyutlu görüntüyü görüntülemek için tıklatın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image47.png))

`InsertVisible` özelliklerini ayarladıktan sonra, bir tarayıcıda `Basics.aspx` sayfasını görüntüleyin ve yeni düğmesine tıklayın. Şekil 20 ' de ürün hatlarımıza yeni bir beiçecek, Acme Tea eklendiğinde DetailsView gösterilmektedir.

[![Northwind Traders artık Acme Tea sunuyor](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image48.png)

**Şekil 20**: Northwind Traders artık Acme Tea sunuyor ([tam boyutlu görüntüyü görüntülemek için tıklatın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image50.png))

Acme Tea 'nın ayrıntılarını girdikten ve Ekle düğmesine tıkladıktan sonra, `Products` veritabanı tablosuna bir geri gönderme ve yeni kayıt eklenir. Bu DetailsView, ürünleri veritabanı tablosunda bulundukları sırayla listelediğinden, yeni ürünü görmek için son ürünün sayfasına ihtiyacımız olmalıdır.

[Acme Tea için ![ayrıntıları](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image51.png)

**Şekil 21**: Acme Tea ayrıntıları ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image53.png))

> [!NOTE]
> DetailsView 'un [CurrentMode özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx) , görüntülenmekte olan arabirimi gösterir ve şu değerlerden biri olabilir: `Edit`, `Insert`veya `ReadOnly`. [DefaultMode özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx) , DetailsView 'un bir düzenleme veya ekleme işlemi tamamlandıktan sonra geri döndürdüğü modu gösterir ve kalıcı olarak düzenleme veya ekleme modunda olan bir DetailsView görüntülemek için faydalıdır.

Ve sonra, DetailsView 'un ekleme ve düzenlenme özellikleri GridView ile aynı kısıtlamalardan daha da etkilenebilir: Kullanıcı, bir TextBox aracılığıyla var olan `CategoryID` ve `SupplierID` değerlerini girmelidir; arabirimin herhangi bir doğrulama mantığı yoktur; `NULL` değerlere izin verilmeyen veya veritabanı düzeyinde belirtilen varsayılan değere sahip olmayan tüm ürün alanları ekleme arabirimine eklenmelidir ve bu şekilde devam etmelidir.

Daha sonra GridView 'un Düzenle arabirimini genişletmenin ve geliştirmesinin İncelenme teknikleri, DetailsView denetiminin düzenlemesi ve ekleme arabirimlerini de uygulanabilir.

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>Daha esnek bir veri değişikliği Kullanıcı arabirimi için FormView kullanma

FormView, veri ekleme, düzenlemenin ve silmenin yerleşik desteğini sunar, ancak alanlar yerine şablonlar kullandığından, verileri sağlamak için GridView ve DetailsView denetimleri tarafından kullanılan bir yer yoktur. değişiklik arabirimi. Bunun yerine, bu arabirim yeni bir öğe eklerken veya var olan bir öğeyi yeni, Düzenle, Sil, Ekle, Güncelleştir ve Iptal düğmeleriyle birlikte düzenleyerek Kullanıcı girişinin toplanması için Web denetimlerini uygun şablonlara el ile eklenmelidir. Neyse ki, Visual Studio, bir veri kaynağına FormView 'u akıllı etiketindeki açılan listeden bağladığınızda gerekli arabirimi otomatik olarak oluşturur.

Bu teknikleri anlamak için, `Basics.aspx` sayfasına bir FormView ekleyerek başlayın ve ardından FormView 'un akıllı etiketiyle onu zaten oluşturulan ObjectDataSource 'a bağlayın. Bu, yeni, düzenleme, silme, ekleme, güncelleştirme ve Iptal düğmeleri için kullanıcının giriş ve düğme Web denetimlerini toplamak üzere metin kutusu Web denetimleriyle birlikte düzenlenecek bir `EditItemTemplate`, `InsertItemTemplate`ve `ItemTemplate` oluşturur. Ayrıca, FormView 'un `DataKeyNames` özelliği, ObjectDataSource tarafından döndürülen nesnenin birincil anahtar alanı (`ProductID`) olarak ayarlanır. Son olarak, FormView 'un akıllı etiketindeki disk belleğini etkinleştir seçeneğini işaretleyin.

Aşağıda, FormView 'un ObjectDataSource 'a bağlandıktan sonra FormView 'un `ItemTemplate` için bildirim temelli biçimlendirme gösterilmektedir. Varsayılan olarak, her Boolean değer alanı (`Discontinued`) devre dışı CheckBox Web denetiminin `Checked` özelliğine bağlandığında, Boole olmayan her bir değer ürün alanı bir etiket Web denetiminin `Text` özelliğine bağlanır. Yeni, Düzenle ve Sil düğmelerinin tıklandığı sırada belirli FormView davranışlarını tetiklemesi için, `CommandName` değerlerinin sırasıyla `New`, `Edit`ve `Delete`olarak ayarlanması zorunludur.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample8.aspx)]

Şekil 22, bir tarayıcıdan görüntülendiklerinde FormView 'un `ItemTemplate` gösterir. Her ürün alanı, en alttaki yeni, Düzenle ve Sil düğmeleriyle listelenir.

[![, her ürün alanını yeni, Düzenle ve Sil düğmeleriyle birlikte listeler.](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image54.png)

**Şekil 22**: bu FormView `ItemTemplate`, her ürün alanını yeni, düzenleme ve silme düğmeleriyle birlikte listeler ([tam boyutlu görüntüyü görüntülemek için tıklatın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image56.png))

GridView ve DetailsView gibi, `CommandName` özelliği Delete olarak ayarlanmış olan Delete düğmesine veya herhangi bir Button, LinkButton veya ImageButton öğesine tıkladığınızda geri göndermeye neden olur, ObjectDataSource 'un `DeleteParameters`, FormView 'un `DataKeyNames` değerine göre doldurur ve ObjectDataSource 'un `Delete()` yöntemini çağırır.

Düzenle düğmesine bir geri gönderme tıklandığında ve veriler, düzenleme arabirimini işlemeden sorumlu olan `EditItemTemplate`yeniden bağlanır. Bu arabirim, Update ve Cancel düğmeleriyle birlikte verileri düzenlemenin Web denetimlerini içerir. Visual Studio tarafından oluşturulan varsayılan `EditItemTemplate`, herhangi bir otomatik artış alanı (`ProductID`) için bir etiket, her Boole olmayan değer alanı için bir TextBox ve her bir Boole değeri alanı için bir onay kutusu içerir. Bu davranış, GridView ve DetailsView denetimlerinde otomatik olarak oluşturulan BoundFields 'e çok benzer.

> [!NOTE]
> FormView 'un `EditItemTemplate` otomatik nesli ile ilgili küçük bir sorun, `CategoryName` ve `SupplierName`gibi salt okunan alanlar için TextBox Web denetimleri işleyişleridir. Bu kısa süre içinde nasıl hesaba başlayacağız.

`EditItemTemplate` metin kutusu denetimleri, `Text` özelliğinin *iki yönlü veri bağlamayı*kullanarak karşılık gelen veri alanı değerine bağlanmasını sağlar. `<%# Bind("dataField") %>`tarafından belirtilen iki yönlü veri bağlama, verileri şablona bağlarken ve kayıt ekleme veya düzenlemenin, ObjectDataSource 'un parametrelerini doldururken veri bağlamayı gerçekleştirir. Diğer bir deyişle, Kullanıcı `ItemTemplate`Düzenle düğmesine tıkladığında `Bind()` yöntemi belirtilen veri alanı değerini döndürür. Kullanıcı değişikliklerini yaptıktan ve sonra Güncelleştir ' e tıkladıktan sonra, `Bind()` kullanılarak belirtilen veri alanlarına karşılık gelen değerler, ObjectDataSource 'un `UpdateParameters`uygulanır. Alternatif olarak, `<%# Eval("dataField") %>`belirtilen tek yönlü veri bağlama yalnızca verileri şablona bağlarken veri alanı değerlerini alır ve Kullanıcı tarafından girilen değerleri geri gönderme sırasında veri kaynağının *parametrelerine döndürmez.*

Aşağıdaki bildirim temelli biçimlendirme FormView 'un `EditItemTemplate`gösterir. `Bind()` yönteminin, burada veri bağlama sözdiziminde kullanıldığını ve Update ve Cancel düğme web denetimlerinin `CommandName` özelliklerinin uygun şekilde ayarlandığını unutmayın.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample9.aspx)]

`EditItemTemplate`, bu noktada, kullanmaya çalışmamız durumunda bir özel durumun oluşturulmasına neden olur. Sorun, `CategoryName` ve `SupplierName` alanlarının `EditItemTemplate`metin kutusu Web denetimleri olarak işlendiğine yönelik bir sorundur. Bu metin kutularını etiketlere değiştirmemiz veya onları tamamen kaldırmanız gerekir. Onları yalnızca `EditItemTemplate`tamamen silelim.

Şekil 23 ' te, bir tarayıcıda düzenlenecek düzen düğmesi tıklandıktan sonra bir tarayıcı görüntülenir. `ItemTemplate` yalnızca `EditItemTemplate`kaldırdığımız için, gösterilen `SupplierName` ve `CategoryName` alanlarının artık mevcut olmadığını unutmayın. Güncelleştirme düğmesine tıklandığında, FormView, GridView ve DetailsView denetimleriyle aynı adım sırası üzerinden ilerler.

[Varsayılan olarak, EditItemTemplate her düzenlenebilir Ürün alanını bir TextBox veya onay kutusu olarak gösterir ![](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image57.png)

**Şekil 23**: varsayılan olarak `EditItemTemplate` her düzenlenebilir Ürün alanını bir metin kutusu veya onay kutusu olarak gösterir ([tam boyutlu görüntüyü görüntülemek için tıklatın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image59.png))

INSERT düğmesine tıklandığında FormView, geri gönderme `ItemTemplate`. Ancak, yeni bir kayıt eklendikçe FormView 'a hiçbir veri bağlanmadı. `InsertItemTemplate` arabirimi, INSERT ve Cancel düğmeleriyle birlikte yeni bir kayıt eklemek için Web denetimlerini içerir. Visual Studio tarafından oluşturulan varsayılan `InsertItemTemplate`, her Boolean değer alanı için bir TextBox ve otomatik olarak oluşturulan `EditItemTemplate`arabirimine benzer şekilde her bir Boolean değer alanı için bir onay kutusu içerir. TextBox denetimleri, kendi `Text` özelliğine sahiptir ve iki yönlü veri bağlamayı kullanarak karşılık gelen veri alanı değerine bağlanır.

Aşağıdaki bildirim temelli biçimlendirme FormView 'un `InsertItemTemplate`gösterir. `Bind()` yönteminin, burada veri bağlama sözdiziminde kullanıldığını ve INSERT ve Cancel düğme web denetimlerinin `CommandName` özelliklerinin uygun şekilde ayarlandığını unutmayın.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample10.aspx)]

FormView 'un `InsertItemTemplate`otomatik olarak oluşturulmasını içeren bir alt ttidir. Özellikle, metin kutusu Web denetimleri, `CategoryName` ve `SupplierName`gibi salt okunan alanlar için de oluşturulur. `EditItemTemplate`gibi, bu metin kutularını `InsertItemTemplate`kaldırdık.

Şekil 24 ' te yeni bir ürün eklenirken bir tarayıcıda FormView gösterilmektedir. `ItemTemplate` gösterilen `SupplierName` ve `CategoryName` alanlarının artık kaldırıldığımızda mevcut olmadığını unutmayın. Ekle düğmesine tıklandığında, FormView, `Products` tabloya yeni bir kayıt ekleyerek DetailsView denetimiyle aynı adımlar dizisi üzerinden ilerler. Şekil 25 ' te, Acme Coffee ürünün ayrıntıları eklendikten sonra FormView 'da gösterilir.

[InsertItemTemplate ![, FormView 'un ekleme arabirimini belirler](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image60.png)

**Şekil 24**: `InsertItemTemplate` FormView 'un ekleme arabirimini ([tam boyutlu görüntüyü görüntülemek Için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image62.png)) belirler

[Yeni ürünün ayrıntıları ![, Acme Coffee, FormView içinde görüntülenir](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image63.png)

**Şekil 25**: yeni ürünün "Acme Coffee" ayrıntıları FormView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image65.png))

Bir salt okunurdur, düzenledikten ve arabirimleri üç ayrı şablona ekleyerek, FormView bu arabirimler üzerinde DetailsView ve GridView 'dan daha fazla denetim sağlar.

> [!NOTE]
> DetailsView gibi, FormView 'un `CurrentMode` özelliği, görüntülenmekte olan arabirimi ve `DefaultMode` özelliği, FormView 'un bir düzenleme veya ekleme işlemi tamamlandıktan sonra geri döndürdüğü modu belirtir.

## <a name="summary"></a>Özet

Bu öğreticide GridView, DetailsView ve FormView kullanarak veri ekleme, düzenlemenin ve silmenin temellerini inceliyoruz. Bu denetimlerin üçü de, veri Web denetimleri ve ObjectDataSource sayesinde ASP.NET sayfasında tek bir kod satırı yazmadan kullanılabilecek bazı yerleşik veri değiştirme özellikleri sağlar. Ancak, basit nokta ve tıklama teknikleri bir oldukça büyük ve Naïve veri değişikliği Kullanıcı arabirimini işler. Doğrulama sağlamak, programlı değerler eklemek, özel durumları düzgün bir şekilde işlemek, Kullanıcı arabirimini özelleştirmek ve bu şekilde devam etmek için, sonraki birkaç öğreticiyle ele alınacaktır.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](limiting-data-modification-functionality-based-on-the-user-cs.md)
> [İleri](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
