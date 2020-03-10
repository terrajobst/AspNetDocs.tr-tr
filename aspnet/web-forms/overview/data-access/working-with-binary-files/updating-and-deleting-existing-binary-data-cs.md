---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-cs
title: Mevcut Ikili verileri güncelleştirme ve silme (C#) | Microsoft Docs
author: rick-anderson
description: Önceki öğreticilerde, GridView denetiminin metin verilerini düzenlemeyi ve silmeyi basit hale getiren gördük. Bu öğreticide, GridView denetiminin nasıl yaptığımız de anlatılmaktadır...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 35798f21-1606-434b-83f8-30166906ef49
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e37381ee48fcda8e0e10374aa7a6ae53c3cc77c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587824"
---
# <a name="updating-and-deleting-existing-binary-data-c"></a>Mevcut İkili Verileri Güncelleştirme ve Silme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_CS.exe) veya [PDF 'yi indirin](updating-and-deleting-existing-binary-data-cs/_static/datatutorial57cs1.pdf)

> Önceki öğreticilerde, GridView denetiminin metin verilerini düzenlemeyi ve silmeyi basit hale getiren gördük. Bu öğreticide, GridView denetiminin, ikili verilerin veritabanına kaydedilip kaydedilmediğini veya dosya sisteminde depolanıp saklanmadığını, ikili verileri düzenleme ve silme olanağı da sağlar.

## <a name="introduction"></a>Giriş

Son üç öğreticide, ikili verilerle çalışmaya yönelik çok sayıda işlevselliği ekledik. `Categories` tabloya bir `BrochurePath` sütunu ekleyerek ve mimariyi uygun şekilde güncelleştirdik. Ayrıca, bir görüntü dosyasının ikili içeriğini tutan kategori tablo s `Picture` sütunuyla çalışmak üzere veri erişim katmanı ve Iş mantığı katmanı yöntemleri ekledik. Bir GridView 'da ikili verileri, bir `<img>` öğesinde gösterilen kategori s resmine sahip ve kullanıcıların yeni bir kategori eklemesine ve kendi broşür ve resim verilerini yüklemesine izin veren bir DetailsView ekledi.

Tüm bunlar geçerli kategorileri düzenleme ve silme olanağıdır. Bu öğreticide, GridView s yerleşik düzenleme ve silme özelliklerini kullanarak gerçekleştireceğiz. Bir kategoriyi düzenlediğinizde, Kullanıcı isteğe bağlı olarak yeni bir resim yükleyebilir ya da kategorinin mevcut olanı kullanmaya devam etmesine izin verebilir. Broşür için, mevcut broşürden birini veya yeni bir broşürü karşıya yüklemeyi seçebilir ya da kategorinin artık onunla ilişkili bir broşürü olmadığını belirtebilirsiniz. Haydi başlayın!

## <a name="step-1-updating-the-data-access-layer"></a>1\. Adım: veri erişim katmanını güncelleştirme

DAL, `Insert`, `Update`ve `Delete` yöntemlerine otomatik olarak üretilmiş, ancak bu yöntemler, `Picture` sütununu içermeyen `CategoriesTableAdapter` s ana sorgusuna göre oluşturulmuştur. Bu nedenle, `Insert` ve `Update` yöntemleri, kategori s resmine yönelik ikili verileri belirtmek için parametreler içermez. [Önceki öğreticide](including-a-file-upload-option-when-adding-a-new-record-cs.md)yaptığımız gibi, ikili verileri belirtirken `Categories` tablosunu güncelleştirmek için yeni bir TableAdapter yöntemi oluşturuyoruz.

Türü belirtilmiş veri kümesini açın ve tasarımcı 'dan `CategoriesTableAdapter` s başlığına sağ tıklayıp bağlam menüsünden sorgu Ekle ' yi seçerek TableAdapter sorgu Yapılandırma Sihirbazı 'nı başlatın. Bu sihirbaz, TableAdapter sorgusunun veritabanına nasıl eriştiğimizi isteyerek başlar. SQL deyimlerini kullan ' ı seçin ve Ileri ' ye tıklayın. Sonraki adım, oluşturulacak sorgu türünü sorar. `Categories` tabloya yeni bir kayıt eklemek için bir sorgu oluşturuyoruz, GÜNCELLEŞTIR ' i seçin ve Ileri ' ye tıklayın.

[![GÜNCELLEŞTIRME seçeneğini belirleyin](updating-and-deleting-existing-binary-data-cs/_static/image1.gif)](updating-and-deleting-existing-binary-data-cs/_static/image1.png)

**Şekil 1**: Güncelleştir seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image2.png))

Artık `UPDATE` SQL ifadesini belirtmemiz gerekir. Sihirbaz, TableAdapter s ana sorgusuna (`CategoryName`, `Description`ve `BrochurePath` değerlerini güncelleştiren bir `UPDATE`) karşılık gelen otomatik olarak bir ifade önerir. `Picture` sütununun bir `@Picture` parametresiyle birlikte dahil edilmesini sağlamak için ifadeyi değiştirin, örneğin:

[!code-sql[Main](updating-and-deleting-existing-binary-data-cs/samples/sample1.sql)]

Sihirbazın son ekranında yeni TableAdapter metodunu adlandırma bize sorulur. `UpdateWithPicture` girin ve son ' a tıklayın.

[![yeni TableAdapter metodunu UpdateWithPicture olarak adlandırın](updating-and-deleting-existing-binary-data-cs/_static/image2.gif)](updating-and-deleting-existing-binary-data-cs/_static/image3.png)

**Şekil 2**: yeni TableAdapter metodunu adlandırma `UpdateWithPicture` ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image4.png))

## <a name="step-2-adding-the-business-logic-layer-methods"></a>2\. Adım: Iş mantığı katman yöntemlerini ekleme

DAL güncellenmesinin yanı sıra, bir kategoriyi güncelleştirmek ve silmek için yöntemler eklemek üzere BLL 'yi güncelleştirmemiz gerekir. Bunlar, sunum katmanından çağrılacak yöntemlerdir.

Bir kategoriyi silmek için `CategoriesTableAdapter` s otomatik olarak oluşturulan `Delete` metodunu kullanabiliriz. `CategoriesBLL` sınıfına aşağıdaki yöntemi ekleyin:

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample2.cs)]

Bu öğreticide, bir kategoriyi güncelleştirmek için ikili resim verilerini bekleyen ve `CategoriesTableAdapter` yeni eklenen `UpdateWithPicture` yöntemi ve yalnızca `CategoryName`, `Description`ve `BrochurePath` değerlerini kabul eden ve `CategoriesTableAdapter` Class s otomatik olarak oluşturulan `Update` ifadesini kullanan iki yöntem oluşturalım. İki yöntem kullanılarak yapılan bir Kullanıcı, bazı durumlarda bir kullanıcının kategori s resmini diğer alanlarıyla birlikte güncelleştirmek isteyebilir ve bu durumda kullanıcının yeni resmi karşıya yüklemesi gerekecektir. Karşıya yüklenen Picture s ikili verileri daha sonra `UPDATE` bildiriminde kullanılabilir. Diğer durumlarda, Kullanıcı yalnızca güncelleştirme, örneğin adı ve açıklama ile ilgileniyor olabilir. Ancak `UPDATE` deyimin `Picture` sütununun ikili verilerini de beklediğinde, bu bilgileri de sağlamanız gerekir. Bu, düzenlenen kayıt için resim verilerini geri getirmek üzere veritabanına fazladan bir seyahat gerektirir. Bu nedenle, iki `UPDATE` yöntemi istiyoruz. Iş mantığı katmanı, kategori güncelleştirilirken resim verilerinin sağlanıp sağlanana göre hangisinin kullanılacağını belirleyecek.

Bunu kolaylaştırmak için, `CategoriesBLL` sınıfına, her ikisi de adlı `UpdateCategory`iki yöntem ekleyin. Birincisi, giriş parametreleri olarak üç `string` s, `byte` dizisi ve bir `int` kabul etmelidir; İkincisi, yalnızca üç `string` ve bir `int`. `string` giriş parametreleri kategori adı, açıklama ve broşür dosya yolu için, `byte` dizisi kategori s resminin ikili içeriğine yöneliktir ve `int` güncelleştirilecek kaydın `CategoryID` tanımlar. Geçirilen `byte` dizisi `null`ise ilk aşırı yükün ikinci kez harekete geçirdiğine dikkat edin:

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample3.cs)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>3\. Adım: ekleme ve görüntüleme Işlevinin üzerine kopyalama

[Önceki öğreticide](including-a-file-upload-option-when-adding-a-new-record-cs.md) , GridView 'daki tüm kategorileri listelenmiş `UploadInDetailsView.aspx` adlı bir sayfa oluşturduk ve sisteme yeni kategoriler eklemek Için bir DetailsView sağladık. Bu öğreticide, GridView 'ı düzen ve silme desteğini kapsayacak şekilde genişleteceğiz. `UploadInDetailsView.aspx`' den çalışmaya devam etmek yerine, bu öğretici değişikliklerini aynı klasörden `UpdatingAndDeleting.aspx` sayfasında `~/BinaryData`. Bildirime dayalı işaretlemeyi ve kodu `UploadInDetailsView.aspx` kopyalayıp `UpdatingAndDeleting.aspx`yapıştırın.

`UploadInDetailsView.aspx` sayfasını açarak başlayın. Şekil 3 ' te gösterildiği gibi, `<asp:Content>` öğesi içindeki bildirim temelli sözdiziminin tümünü kopyalayın. Sonra `UpdatingAndDeleting.aspx` açın ve bu biçimlendirmeyi `<asp:Content>` öğesi içinde yapıştırın. Benzer şekilde, kodu `UploadInDetailsView.aspx` Page for Code Behind sınıfından `UpdatingAndDeleting.aspx`.

[![, Uploadındetailsview. aspx dosyasından bildirim temelli biçimlendirmeyi kopyalayın](updating-and-deleting-existing-binary-data-cs/_static/image3.gif)](updating-and-deleting-existing-binary-data-cs/_static/image5.png)

**Şekil 3**: `UploadInDetailsView.aspx` bildirim temelli biçimlendirmeyi kopyalama ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image6.png))

Bildirim temelli biçimlendirmenin ve kodun üzerine kopyaladıktan sonra `UpdatingAndDeleting.aspx`ziyaret edin. Aynı çıktıyı görmeniz ve önceki öğreticide `UploadInDetailsView.aspx` sayfasıyla aynı kullanıcı deneyimine sahip olmanız gerekir.

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>4\. Adım: ObjectDataSource ve GridView 'a silme desteğini ekleme

Veri öğreticisini [ekleme, güncelleştirme ve silmeye genel bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) konusunda anlatıldığı gibi, GridView, yerleşik silme özellikleri sağlar ve bu özellik, altta yatan veri kaynağı silmeyi destekliyorsa, bir onay kutusunun Tick değerinde etkinleştirilebilir. Şu anda GridView 'un bağlı olduğu ObjectDataSource (`CategoriesDataSource`) silmeyi desteklemez.

Bu sorunu gidermek için, ObjectDataSource 'un akıllı etiketindeki veri kaynağını Yapılandır seçeneğine tıklayarak Sihirbazı başlatın. İlk ekran, ObjectDataSource 'un `CategoriesBLL` sınıfıyla çalışacak şekilde yapılandırıldığını gösterir. Ileri düğmesine basın. Şu anda yalnızca ObjectDataSource s `InsertMethod` ve `SelectMethod` özellikleri belirtilmiş. Ancak sihirbaz, GÜNCELLEŞTIR ve SIL sekmelerinde bulunan aşağı açılan listeleri sırasıyla `UpdateCategory` ve `DeleteCategory` yöntemleriyle otomatik olarak doldurmuş. Bunun nedeni, `CategoriesBLL` sınıfında bu yöntemleri güncelleştirme ve silme için varsayılan yöntemler olarak `DataObjectMethodAttribute` kullanarak işaretliyoruz.

Şimdilik, GÜNCELLEŞTIRME sekmesi aşağı açılan listesini (yok) olarak ayarlayın, ancak SIL sekme s açılır listesini `DeleteCategory`olarak ayarlayın. Güncelleştirme desteği eklemek için adım 6 ' da Bu sihirbaza geri döneceğiz.

[![silme işlemini DeleteCategory metodunu kullanacak şekilde yapılandırın](updating-and-deleting-existing-binary-data-cs/_static/image4.gif)](updating-and-deleting-existing-binary-data-cs/_static/image7.png)

**Şekil 4**: `DeleteCategory` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image8.png))

> [!NOTE]
> Sihirbaz tamamlandıktan sonra Visual Studio, veri Web denetimleri alanlarını yeniden oluşturacak alanları ve anahtarları yenilemek isteyip istemediğinizi sorabilir. Evet ' i seçmek, yapmış olduğunuz tüm alan özelleştirmelerinin üzerine yazacak şekilde Hayır ' ı seçin.

ObjectDataSource artık `DeleteMethod` özelliği için bir değer ve bir `DeleteParameter`de içerir. Yöntemi belirtmek için Sihirbazı kullanırken, Visual Studio 'Nun ObjectDataSource `OldValuesParameterFormatString` özelliğini `original_{0}`olarak, Update ve Delete Yöntem etkinleştirmeleri ile ilgili sorunlara neden olduğunu hatırlayın. Bu nedenle, bu özelliği tamamen temizleyin veya `{0}`varsayılana sıfırlayın. Bu ObjectDataSource özelliğinde belleğinizin yenilenmesi gerekiyorsa, [verileri ekleme, güncelleştirme ve silmeye Ilişkin genel bakışa](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) bakın.

Sihirbazı tamamladıktan ve `OldValuesParameterFormatString`düzelttikten sonra, ObjectDataSource tarafından bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample4.aspx)]

ObjectDataSource yapılandırıldıktan sonra, GridView s akıllı etiketinden silmeyi etkinleştir onay kutusunu işaretleyerek GridView 'a silme özellikleri ekleyin. Bu, GridView 'a `ShowDeleteButton` özelliği `true`olarak ayarlanmış bir CommandField ekler.

[GridView 'da silme desteğini etkinleştirmek ![](updating-and-deleting-existing-binary-data-cs/_static/image5.gif)](updating-and-deleting-existing-binary-data-cs/_static/image9.png)

**Şekil 5**: GridView 'Da silme desteğini etkinleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image10.png))

Silme işlevini test etmek için bir dakikanızı ayırın. `Products` tablo s `CategoryID` ve `Categories` tablo `CategoryID`s arasında bir yabancı anahtar vardır; bu nedenle ilk sekiz kategorinin birini silmeye çalışırsanız yabancı anahtar kısıtlaması ihlali özel durumu alırsınız. Bu işlevi test etmek için, hem bir broşür hem de resim sağlayan yeni bir kategori ekleyin. Şekil 6 ' da gösterilen test kategorim, `Test.pdf` adlı bir test broşürü dosyası ve bir test resmi içerir. Şekil 7 ' de test kategorisi eklendikten sonra GridView gösterilmektedir.

[Broşür ve görüntüyle bir test kategorisi eklemek ![](updating-and-deleting-existing-binary-data-cs/_static/image6.gif)](updating-and-deleting-existing-binary-data-cs/_static/image11.png)

**Şekil 6**: broşür ve görüntüyle bir test kategorisi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image12.png))

[Test kategorisini ekledikten sonra ![GridView içinde görüntülenir](updating-and-deleting-existing-binary-data-cs/_static/image7.gif)](updating-and-deleting-existing-binary-data-cs/_static/image13.png)

**Şekil 7**: test kategorisini ekledikten sonra GridView içinde görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image14.png))

Visual Studio 'da Çözüm Gezgini yenileyin. Artık `~/Brochures` klasöründe yeni bir dosya görmeniz gerekir `Test.pdf` (bkz. Şekil 8).

Sonra, test kategorisi satırındaki Sil bağlantısına tıklayın, sayfanın geri göndermeye ve `CategoriesBLL` sınıf s `DeleteCategory` yönteminin tetiklenmesine neden olur. Bu, DAL s `Delete` yöntemini çağırır ve uygun `DELETE` bildiriminin veritabanına gönderilmesine neden olur. Veriler daha sonra GridView 'a yeniden bağlanır ve işaretleme, test kategorisi artık mevcut olmayan istemciye geri gönderilir.

Silme iş akışı, `Categories` tablosundan test kategorisi kaydını başarıyla kaldırırken, Web sunucusu s dosya sisteminden broşür dosyasını kaldırmadı. Çözüm Gezgini yenileyin ve `Test.pdf` `~/Brochures` klasörde hala oturmakta olduğunu görürsünüz.

![Test. PDF dosyası Web sunucusu s dosya sisteminden silinmedi](updating-and-deleting-existing-binary-data-cs/_static/image8.gif)

**Şekil 8**: `Test.pdf` dosyası Web sunucusu s dosya sisteminden silinmedi

## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>5\. Adım: silinen kategori broşür dosyasını kaldırma

Veritabanına dış ikili verileri depolamanın altlarından biri, ilişkili veritabanı kaydı silindiğinde bu dosyaları temizlemek için ek adımların alınması gerekir. GridView ve ObjectDataSource, Delete komutu gerçekleştirildikten sonra ve sonra başlatılan olayları sağlar. Aslında hem ön hem de eylem sonrası olaylar için olay işleyicileri oluşturuyoruz. `Categories` kaydı silinmeden önce, PDF dosyasının yolunu belirlememiz gerekir, ancak bazı özel durumlar olması ve kategorinin silinmemesi durumunda kategori silinmeden önce PDF 'YI silmek istemiyorum.

GridView s [`RowDeleting` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx) , ObjectDataSource s Delete komutu çağrılmadan önce ateşlenir, bu, [`RowDeleted` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx) sonrasında ateşlenir. Aşağıdaki kodu kullanarak bu iki olay için olay işleyicileri oluşturun:

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample5.cs)]

`RowDeleting` olay işleyicisinde, silinmekte olan satırın `CategoryID`, bu olay işleyiciden `e.Keys` koleksiyonu aracılığıyla erişilebilen GridView s `DataKeys` koleksiyonundan yapılır. Sonra, `CategoriesBLL` sınıf s `GetCategoryByCategoryID(categoryID)`, silinmekte olan kayıt hakkında bilgi döndürmek için çağrılır. Döndürülen `CategoriesDataRow` nesnesinin`NULL``BrochurePath` olmayan bir değeri varsa, dosyanın `RowDeleted` olay işleyicisinde silinebilmesi için `deletedCategorysPdfPath` sayfa değişkeninde depolanır.

> [!NOTE]
> `RowDeleting` olay işleyicisinde silinmekte olan `Categories` kaydı için `BrochurePath` ayrıntılarını almak yerine, `BrochurePath` GridView s `DataKeyNames` özelliğine başka bir şekilde eklemiş ve `e.Keys` koleksiyonu aracılığıyla kayıt s değerine erişmiş olabilir. Bunun yapılması, GridView s görünüm durumu boyutunu biraz artırır, ancak gereken kod miktarını azaltır ve veritabanına bir seyahat kaydeder.

Temel alınan Delete komutu çağırdıktan sonra, GridView s `RowDeleted` olay işleyicisi ateşlenir. Verileri silmenin hiçbir özel durum yoksa ve `deletedCategorysPdfPath`için bir değer varsa, PDF dosya sisteminden silinir. Bu ek kodun, resmiyle ilişkili kategori s ikili verilerini temizlemek için gerekli olmadığına unutmayın. Çünkü resim verileri doğrudan veritabanında depolandığından, `Categories` satırı silindiğinde bu kategori resim verileri de silinir.

İki olay işleyicisini ekledikten sonra bu test çalışmasını yeniden çalıştırın. Kategori silinirken ilişkili PDF de silinir.

Mevcut bir kayıtla ilişkili ikili verilerin güncelleştirilmesi bazı ilginç sorunlar sağlar. Bu öğreticinin geri kalanında, broşür ve resme güncelleştirme özellikleri ekleme işlemi yapılır. Adım 6, adım 7 ' de resmi güncelleştirirken broşür bilgilerini güncelleştirme tekniklerini inceler.

## <a name="step-6-updating-a-category-s-brochure"></a>6\. Adım: Kategori broşürü güncelleştirme

Veri öğreticisini [ekleme, güncelleştirme ve silmeye genel bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) konusunda açıklandığı gibi, GridView, temel alınan veri kaynağı uygun şekilde yapılandırıldıysa bir CheckBox 'ın Tick 'i tarafından uygulanabilecek yerleşik satır düzeyinde yapılandırma desteği sunar. Şu anda, `CategoriesDataSource` ObjectDataSource henüz güncelleştirme desteğini içerecek şekilde yapılandırılmadı, bu nedenle ' de bunu eklemesini sağlar.

ObjectDataSource 'un veri kaynağını Yapılandır bağlantısına tıklayın ve ikinci adıma ilerleyin. `CategoriesBLL`kullanılan `DataObjectMethodAttribute` nedeniyle, GÜNCELLEŞTIRME açılır listesi, dört giriş parametresini kabul eden `UpdateCategory` aşırı yüklemesiyle otomatik olarak doldurulmalıdır (tüm sütunlar için, ancak `Picture`). Bunu, beş parametreli aşırı yüklemeyi kullanacak şekilde değiştirin.

[![, bir resim parametresi Içeren UpdateCategory metodunu kullanmak için ObjectDataSource 'u yapılandırma](updating-and-deleting-existing-binary-data-cs/_static/image9.gif)](updating-and-deleting-existing-binary-data-cs/_static/image15.png)

**Şekil 9**: `Picture` Için bir parametre Içeren `UpdateCategory` yöntemi kullanmak üzere ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image16.png))

ObjectDataSource artık `UpdateMethod` özelliği ve karşılık gelen `UpdateParameter` s için bir değer içerir. Adım 4 ' te belirtildiği gibi, Visual Studio, veri kaynağı Yapılandırma Sihirbazı 'nı kullanırken ObjectDataSource s `OldValuesParameterFormatString` özelliğini `original_{0}` olarak ayarlar. Bu, Update ve Delete yöntemi etkinleştirmeleri ile ilgili sorunlara neden olur. Bu nedenle, bu özelliği tamamen temizleyin veya `{0}`varsayılana sıfırlayın.

Sihirbazı tamamladıktan ve `OldValuesParameterFormatString`düzelttikten sonra, ObjectDataSource tarafından bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample6.aspx)]

GridView s yerleşik Düzenle özelliklerini açmak için GridView s akıllı etiketinde Düzenle özelliğini etkinleştir seçeneğini işaretleyin. Bu, CommandField s `ShowEditButton` özelliğini `true`olarak ayarlar, böylece bir düzenleme düğmesi eklenmesine (ve düzenlenmekte olan satır için Update ve Cancel düğmelerine) sahiptir.

[GridView 'ı düzenlemesini destekleyecek şekilde yapılandırma ![](updating-and-deleting-existing-binary-data-cs/_static/image10.gif)](updating-and-deleting-existing-binary-data-cs/_static/image17.png)

**Şekil 10**: GridView 'ı düzenlemesini destekleyecek şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image18.png))

Sayfayı tarayıcıda ziyaret edin ve satır s düzenleme düğmelerinden birine tıklayın. `CategoryName` ve `Description` BoundFields, metin kutuları olarak işlenir. `BrochurePath` TemplateField bir `EditItemTemplate`eksiktir, bu nedenle, `ItemTemplate` bir bağlantı bağlantısını göstermeye devam eder. `Picture` ImageField, `Text` özelliğine `CategoryID`ImageField s `DataImageUrlField` değerinin atandığı bir TextBox olarak işlenir.

[GridView ![BrochurePath için bir Editing arabirimi eksik](updating-and-deleting-existing-binary-data-cs/_static/image11.gif)](updating-and-deleting-existing-binary-data-cs/_static/image19.png)

**Şekil 11**: GridView `BrochurePath` Için bir düzenleyen arabirimi yok ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image20.png))

## <a name="customizing-thebrochurepaths-editing-interface"></a>`BrochurePath`s Editing arabirimini özelleştirme

Kullanıcının şunları yapmasına izin veren `BrochurePath` TemplateField alanı için bir düzen arabirimi oluşturuyoruz.

- Kategori broşürleri olduğu gibi bırakın,
- Yeni bir broşür yükleyerek kategori broşürleri güncelleştirin veya
- Kategori broşürleri tamamen kaldırın (kategorinin artık ilişkili bir broşürü olmaması durumunda).

Ayrıca, `Picture` ImageField s Editing arabirimini güncelleştirmemiz gerekir, ancak adım 7 ' de bunu kullanacağız.

GridView s akıllı etiketinde Şablonları Düzenle bağlantısına tıklayın ve açılan listeden `BrochurePath` TemplateField `EditItemTemplate` ' ı seçin. Bu şablona bir RadioButtonList Web denetimi ekleyin, `ID` özelliğini `BrochureOptions` ve `AutoPostBack` özelliği `true`olarak ayarlar. Özellikler penceresi, `ListItem` koleksiyonu düzenleyicisini getirecek `Items` özelliğindeki üç noktaya tıklayın. Aşağıdaki üç seçeneği sırasıyla `Value` s 1, 2 ve 3 ile ekleyin:

- Geçerli broşürü kullan
- Geçerli broşürü kaldır
- Yeni Broşür yükle

İlk `ListItem` s `Selected` özelliğini `true`olarak ayarlayın.

![RadioButtonList için üç ListItems ekleyin](updating-and-deleting-existing-binary-data-cs/_static/image12.gif)

**Şekil 12**: RadioButtonList ' ye üç `ListItem` s ekleme

RadioButtonList altına `BrochureUpload`adlı bir dosya yükleme denetimi ekleyin. `Visible` özelliğini `false`olarak ayarlayın.

[EditItemTemplate 'e RadioButtonList ve FileUpload denetimi ekleme ![](updating-and-deleting-existing-binary-data-cs/_static/image13.gif)](updating-and-deleting-existing-binary-data-cs/_static/image21.png)

**Şekil 13**: `EditItemTemplate` bir RadioButtonList ve FileUpload denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image22.png))

Bu RadioButtonList Kullanıcı için üç seçenek sağlar. Bu düşünce, dosya yükleme denetiminin yalnızca son seçenek olan yeni Broşür yükle seçeneğinin seçili olması durumunda görüntülencedir. Bunu gerçekleştirmek için, RadioButtonList s `SelectedIndexChanged` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample7.cs)]

RadioButtonList ve FileUpload denetimleri bir şablon içinde olduğundan, bu denetimlere programlı olarak erişmek için bir kod yazmanız gerekir. `SelectedIndexChanged` olay işleyicisine `sender` giriş parametresinde RadioButtonList başvurusu geçirilir. Dosya karşıya yükleme denetimini almak için, RadioButtonList s üst denetimini almanız ve `FindControl("controlID")` yöntemi buradan kullanmanız gerekir. Hem RadioButtonList hem de FileUpload denetimlerine bir başvurduktan sonra, FileUpload Control s `Visible` özelliği yalnızca RadioButtonList s `SelectedValue` eşitse `true` olarak ayarlanır. Bu, karşıya yükleme yeni broşürü `ListItem``Value`.

Bu kodla birlikte, düzen arabirimini test etmek için bir dakikanızı ayırın. Bir satır için Düzenle düğmesine tıklayın. Başlangıçta geçerli broşüri kullan seçeneği seçilmelidir. Seçili dizinin değiştirilmesi geri göndermeye neden olur. Üçüncü seçenek işaretliyse, dosya yükleme denetimi görüntülenir, aksi takdirde gizlidir. Şekil 14 ' te Düzenle düğmesi ilk tıklandığında düzenleme arabirimi gösterilir; Şekil 15, yeni broşür karşıya yükle seçeneği seçildikten sonra arabirimi gösterir.

[Başlangıçta ![geçerli broşürü kullan seçeneği seçilidir](updating-and-deleting-existing-binary-data-cs/_static/image14.gif)](updating-and-deleting-existing-binary-data-cs/_static/image23.png)

**Şekil 14**: başlangıçta geçerli broşürü kullan seçeneği seçilidir ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image24.png))

[Yeni Broşür yükle seçeneğinin seçilmesi ![dosya yükleme denetimini görüntüler](updating-and-deleting-existing-binary-data-cs/_static/image15.gif)](updating-and-deleting-existing-binary-data-cs/_static/image25.png)

**Şekil 15**: yeni Broşür yükle seçeneğinin belirlenmesi, FileUpload denetimini görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image26.png))

## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>Broşür dosyasını kaydetme ve`BrochurePath`sütunu güncelleştirme

GridView s Update düğmesine tıklandığında `RowUpdating` olayı ateşlenir. ObjectDataSource s Update komutu çağrılır ve ardından GridView s `RowUpdated` olayı ateşlenir. Silme iş akışında olduğu gibi, bu olayların her ikisi için de olay işleyicileri oluşturuyoruz. `RowUpdating` olay işleyicisinde, `BrochureOptions` RadioButtonList ' nin `SelectedValue` göre hangi eylemin yapılacağını belirlememiz gerekir:

- `SelectedValue` 1 ise, aynı `BrochurePath` ayarını kullanmaya devam etmek istiyoruz. Bu nedenle, ObjectDataSource `brochurePath` parametresini güncelleştirilmekte olan kaydın mevcut `BrochurePath` değerine ayarlamanız gerekir. ObjectDataSource s `brochurePath` parametresi `e.NewValues["brochurePath"] = value`kullanılarak ayarlanabilir.
- `SelectedValue` 2 ise, kayıt s `BrochurePath` değerini `NULL`olarak ayarlamak istiyoruz. Bu, ObjectDataSource `brochurePath` parametresi `Nothing`olarak ayarlanarak gerçekleştirilebilir ve bu, `UPDATE` ifadesinde kullanılan bir veritabanı `NULL` sonuçlanır. Kaldırılmakta olan mevcut bir broşür dosyası varsa, var olan dosyayı silmemiz gerekir. Ancak, bunu yalnızca güncelleştirme özel durum oluşturulmadan tamamlanırsa bunu yapmak istiyoruz.
- `SelectedValue` 3 ise, kullanıcının bir PDF dosyasını karşıya yükleyip dosya sistemine kaydetmesini ve kayıt s `BrochurePath` sütun değerini güncelleştirdiğinden emin olmak istiyoruz. Ayrıca, değiştirilmekte olan mevcut bir broşür dosyası varsa, önceki dosyayı silmemiz gerekir. Ancak, bunu yalnızca güncelleştirme özel durum oluşturulmadan tamamlanırsa bunu yapmak istiyoruz.

RadioButtonList s `SelectedValue` 3 olduğunda tamamlanması gereken adımlar, DetailsView 'un `ItemInserting` olay işleyicisi tarafından kullanılanlarla neredeyse aynıdır. Bu olay işleyicisi, [önceki öğreticide](including-a-file-upload-option-when-adding-a-new-record-cs.md)eklediğimiz DetailsView denetiminden yeni bir kategori kaydı eklendiğinde yürütülür. Bu nedenle, bu işlevselliği ayrı yöntemlere yeniden düzenleme behooves. Özellikle, yaygın işlevselliği iki yönteme taşıdım:

- `ProcessBrochureUpload(FileUpload, out bool)`, bir dosya yükleme denetim örneği ve silme veya düzenleme işleminin devam edip etmediğini veya bazı doğrulama hataları nedeniyle iptal edilip edilmeyeceğini belirten bir çıkış Boole değeri kabul eder. Bu yöntem, kaydedilen dosyanın yolunu veya kaydedilmiş bir dosya yoksa `null` döndürür.
- `DeleteRememberedBrochurePath`, `deletedCategorysPdfPath` `null`değilse, sayfa değişkeni `deletedCategorysPdfPath` yol tarafından belirtilen dosyayı siler.

Bu iki yöntemin kodu aşağıda verilmiştir. Önceki öğreticiden `ProcessBrochureUpload` ve DetailsView 'un `ItemInserting` olay işleyicisi arasındaki benzerliğini aklınızda edin. Bu öğreticide, bu yeni yöntemleri kullanmak için DetailsView 'un olay işleyicilerini güncelleştirdim. DetailsView 'un olay işleyicilerindeki değişiklikleri görmek için bu öğreticiyle ilişkili kodu indirin.

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample8.cs)]

Aşağıdaki kodun gösterdiği gibi, GridView s `RowUpdating` ve `RowUpdated` olay işleyicileri `ProcessBrochureUpload` ve `DeleteRememberedBrochurePath` yöntemlerini kullanır:

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample9.cs)]

`RowUpdating` olay işleyicisinin, `BrochureOptions` RadioButtonList s `SelectedValue` özellik değerine göre uygun eylemi gerçekleştirmek için bir dizi koşullu deyim kullandığını aklınızda edin.

Bu kodla birlikte, bir kategoriyi düzenleyebilir ve geçerli broşürü kullanımını, bir broşür veya yenisini yüklemeyi seçebilirsiniz. Devam edin ve deneyin. `RowUpdating` ve `RowUpdated` olay işleyicilerinde kesme noktaları ayarlayın ve iş akışını bir fikir alın.

## <a name="step-7-uploading-a-new-picture"></a>7\. Adım: yeni bir resim yükleme

`Picture` ImageField s Editing Interface, `DataImageUrlField` özelliğinden alınan değerle doldurulmuş bir TextBox olarak işler. Düzen iş akışı sırasında, GridView bir parametreyi bir parametre adı, ImageField s `DataImageUrlField` özelliğinin değerini ve parametre s değerini, Editing arabirimindeki metin kutusuna girilen değere geçirir. Bu davranış, görüntü dosya sistemine bir dosya olarak kaydedildiğinde ve `DataImageUrlField` görüntünün tam URL 'sini içerdiğinde uygundur. Bu gibi durumlarda, düzen arabirimi, kullanıcının değiştirebileceği ve veritabanına geri kaydedildiği görüntü s URL 'sini metin kutusu içinde görüntüler. Verilen bu varsayılan arabirim, kullanıcının yeni bir görüntü yüklemesine izin vermez, ancak görüntünün URL 'sini geçerli değerden diğerine değiştirmesine izin verir. Ancak, bu öğreticide, `Picture` ikili veriler doğrudan veritabanında depolandığından ve `DataImageUrlField` özelliği yalnızca `CategoryID`tutuyor olduğundan, ImageField 'ın varsayılan düzenlenme arabirimi yeterli değildir.

Bir Kullanıcı bir ImageField ile bir satırı düzenlediğinde öğreticimize ne olduğunu daha iyi anlamak için aşağıdaki örneği göz önünde bulundurun: bir Kullanıcı, `CategoryID` 10 içeren bir satırı düzenleyerek, `Picture` ImageField 'ın 10 değeriyle bir TextBox olarak işlenmesine neden olur. Kullanıcının bu metin kutusundaki değeri 50 olarak değiştirdiği ve Güncelleştir düğmesine tıkladığı hakkında düşünün. Bir geri gönderme gerçekleşir ve GridView başlangıçta 50 değeriyle `CategoryID` adlı bir parametre oluşturur. Ancak, GridView bu parametreyi (ve `CategoryName` ve `Description` parametrelerini) göndermeden önce, `DataKeys` koleksiyonundan değerleri ekler. Bu nedenle, `CategoryID` parametresi, temel alınan `CategoryID` değeri olan 10 ' un geçerli satırı ile geçersiz kılar. Kısa bir deyişle, ImageField s `DataImageUrlField` özelliğinin ve kılavuz s `DataKey` değerinin adları aynı olduğundan, ImageField s düzen arabirimi bu öğreticide düzenlenen iş akışını etkilemez.

ImageField, veritabanı verilerini temel alan bir görüntünün görüntülenmesini kolaylaştırırken, düzen arabiriminde bir metin kutusu sağlamak istemedik. Bunun yerine, son kullanıcının kategori resmini değiştirmek için kullanabileceği bir dosya karşıya yükleme denetimi sunmak istiyoruz. `BrochurePath` değerinden farklı olarak, bu öğreticiler için her kategorinin bir resme sahip olması gerektiğine karar veririz. Bu nedenle, kullanıcının ilişkili bir resim olmadığını göstermesi gerekmez ve kullanıcının yeni bir resim yükleyip geçerli resmi olduğu gibi bırakabilir.

ImageField s Editing arabirimini özelleştirmek için onu TemplateField 'a dönüştürmemiz gerekiyor. GridView s akıllı etiketinde sütunları düzenle bağlantısına tıklayın, ImageField ' ı seçin ve bu alanı TemplateField ' a Dönüştür bağlantısına tıklayın.

![ImageField 'ı TemplateField 'A Dönüştür](updating-and-deleting-existing-binary-data-cs/_static/image16.gif)

**Şekil 16**: ImageField 'ı TemplateField 'a dönüştürme

ImageField 'ı bu şekilde bir TemplateField 'a dönüştürmek, iki şablon içeren bir TemplateField oluşturur. Aşağıdaki bildirim temelli sözdiziminin gösterdiği gibi, `ItemTemplate`, `ImageUrl` özelliği, ImageField s `DataImageUrlField` ve `DataImageUrlFormatString` özelliklerine göre veri bağlama söz dizimi kullanılarak atanan bir görüntü Web denetimi içerir. `EditItemTemplate`, `Text` özelliği `DataImageUrlField` özelliği tarafından belirtilen değere bağlantılı olan bir TextBox içerir.

[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample10.aspx)]

Bir dosya yükleme denetimi kullanmak için `EditItemTemplate` güncelleştirmemiz gerekiyor. GridView s akıllı etiketinde Şablonları Düzenle bağlantısına tıklayın ve ardından açılan listeden `Picture` TemplateField `EditItemTemplate` ' ı seçin. Şablonda bunu bir TextBox görürsünüz. Sonra, bir dosya yükleme denetimini araç kutusundan şablona sürükleyin ve `ID` `PictureUpload`olarak ayarlayarak. Ayrıca kategori resmini değiştirmek Için metin ekleyin, yeni bir resim belirtin. Kategorinin görünümünü aynı tutmak için, bu alanı şablon için de boş bırakın.

[EditItemTemplate 'e dosya yükleme denetimi ekleme ![](updating-and-deleting-existing-binary-data-cs/_static/image17.gif)](updating-and-deleting-existing-binary-data-cs/_static/image27.png)

**Şekil 17**: `EditItemTemplate` bir dosya yükleme denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image28.png))

Düzen arabirimini özelleştirdikten sonra, ilerlemenizi bir tarayıcıda görüntüleyin. Bir satırı salt okuma modunda görüntülerken, kategori s resmi daha önce olduğu gibi gösterilir, ancak Düzenle düğmesine tıklamak resim sütununu bir dosya olarak bir FileUpload denetimiyle metin olarak işler.

[![, düzen arabirimi bir dosya yükleme denetimi Içerir](updating-and-deleting-existing-binary-data-cs/_static/image18.gif)](updating-and-deleting-existing-binary-data-cs/_static/image29.png)

**Şekil 18**: düzen arabirimi bir dosya karşıya yükleme denetimi içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](updating-and-deleting-existing-binary-data-cs/_static/image30.png))

ObjectDataSource 'un, resim için ikili verileri bir `byte` dizisi olarak kabul eden `CategoriesBLL` sınıf s `UpdateCategory` yöntemini çağırmak üzere yapılandırıldığını unutmayın. Ancak, bu dizide bir `null` değeri varsa, diğer `UpdateCategory` aşırı yükleme çağrılır. Bu, `Picture` sütununu değiştirmediğinde `UPDATE` SQL ifadesini veren, bu nedenle kategorinin geçerli resmini bozulmadan bırakır. Bu nedenle, GridView s `RowUpdating` olay işleyicisinde program aracılığıyla `PictureUpload` FileUpload denetimine başvurabilmek ve bir dosyanın karşıya yüklenip yüklenmediğini belirlemeniz gerekir. Bunlardan biri karşıya yüklenemediğinden `picture` parametresi için bir değer *belirtmek istemiyorum.* Diğer taraftan, bir dosya `PictureUpload` Fıleupload denetimine yüklenmişse, bunun JPG dosyası olduğundan emin olmak istiyoruz. Bu durumda, ikili içeriğini `picture` parametresi aracılığıyla ObjectDataSource 'a gönderebiliriz.

Adım 6 ' da kullanılan kodda olduğu gibi, burada gereken kodun çoğu, DetailsView `ItemInserting` olay işleyicisinde zaten mevcuttur. Bu nedenle, ortak işlevleri yeni bir yönteme yeniden düzenlenmiş, `ValidPictureUpload`ve `ItemInserting` olay işleyicisini bu yöntemi kullanacak şekilde güncelleştirdim.

Aşağıdaki kodu GridView s `RowUpdating` olay işleyicisinin başlangıcına ekleyin. Bu kod, geçersiz bir resim dosyası yüklenirse, broşürün Web sunucusu dosya sistemine kaydedilmesini istediğimiz için, bu kodun, broşür dosyasını kaydeden koddan önce geldiği önemli öneme sahiptir.

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample11.cs)]

`ValidPictureUpload(FileUpload)` yöntemi, tek giriş parametresi olarak bir FileUpload denetimini alır ve karşıya yüklenen dosyanın JPG olduğundan emin olmak için karşıya yüklenen dosya uzantısını denetler; yalnızca bir resim dosyası karşıya yüklenirse çağrılır. Karşıya dosya yüklenayarlanmamışsa, resim parametresi ayarlı değildir ve bu nedenle `null`varsayılan değerini kullanır. Bir resim karşıya yüklenmişse ve `ValidPictureUpload` `true`döndürürse `picture` parametresine karşıya yüklenen görüntünün ikili verileri atanır; Yöntem `false`döndürürse, güncelleştirme iş akışı iptal edilir ve olay işleyicisinin çıkış yapılır.

`ValidPictureUpload(FileUpload)` yöntemi kodu, DetailsView 'un `ItemInserting` olay işleyicisinden şu şekildedir:

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample12.cs)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>8\. Adım: özgün Kategoriler resimlerini JPGs ile değiştirme

Özgün sekiz kategori resimlerinin bir OLE üst bilgisinde kaydırılan bit eşlem dosyaları olduğunu hatırlayın. Artık var olan bir kayıt görüntüsünü düzenleme özelliğini eklediğimiz için, bu bit eşlemleri JPGs ile değiştirmek için bir dakikanızı ayırın. Geçerli kategori resimlerini kullanmaya devam etmek istiyorsanız, aşağıdaki adımları uygulayarak bunları JPGs 'e dönüştürebilirsiniz:

1. Bit eşlem görüntülerini sabit sürücünüze kaydedin. Tarayıcınızda `UpdatingAndDeleting.aspx` sayfasını ziyaret edin ve ilk sekiz kategorinin her biri için görüntüye sağ tıklayıp resmi kaydetmeyi seçin.
2. Görüntüyü istediğiniz görüntü Düzenleyicinizde açın. Örneğin, Microsoft Paint 'i kullanabilirsiniz.
3. Bit eşlemi JPG görüntüsü olarak kaydedin.
4. Kategori s resmini, JPG dosyasını kullanarak, düzen arabirimi aracılığıyla güncelleştirin.

Bir kategoriyi düzenledikten ve JPG görüntüsünü karşıya yükledikten sonra, `DisplayCategoryPicture.aspx` sayfası ilk sekiz kategorinin resimlerinden ilk 78 baytı kullandığından, görüntü tarayıcıda işlenmez. OLE üst bilgisini gerçekleştiren kodu kaldırarak bunu düzeltir. Bunu yaptıktan sonra, `DisplayCategoryPicture.aspx``Page_Load` olay işleyicisi yalnızca aşağıdaki koda sahip olmalıdır:

[!code-vb[Main](updating-and-deleting-existing-binary-data-cs/samples/sample13.vb)]

> [!NOTE]
> `UpdatingAndDeleting.aspx` sayfa ekleme ve oluşturma arabirimleri biraz daha iş kullanabilir. DetailsView ve GridView 'daki `CategoryName` ve `Description` BoundFields, TemplateFields 'e dönüştürülmelidir. `CategoryName` `NULL` değerlere izin vermediğinden, bir RequiredFieldValidator eklenmelidir. `Description` metin kutusu büyük olasılıkla çok satırlı bir metin kutusuna dönüştürülebilmelidir. Bu son aşağı dokunmalar sizin için bir alıştırma olarak bırakıyorum.

## <a name="summary"></a>Özet

Bu öğreticide, ikili verilerle çalışma hakkındaki görünüm tamamlanır. Bu öğreticide ve önceki üç adımda, ikili verilerin dosya sisteminde veya doğrudan veritabanı içinde nasıl depolanabileceğini gördük. Bir Kullanıcı sabit sürücüsünden bir dosya seçerek ve dosyayı dosya sisteminde depolanabilen veya veritabanına eklenebilen Web sunucusuna yükleyerek sisteme ikili veriler sağlar. ASP.NET 2,0, bu tür bir arabirim sağlayan bir dosya yükleme denetimini sürükleyip bırakma işlemini kolaylaştırıyor. Ancak, [karşıya yükleme dosyaları](uploading-files-cs.md) öğreticisinde belirtildiği gibi, dosya karşıya yükleme denetimi yalnızca görece küçük dosya yüklemeleri için uygundur ve ideal olarak bir megabayt aşmaz. Ayrıca, karşıya yüklenen verileri temel alınan veri modeliyle ilişkilendirmeyi ve var olan kayıtlardan ikili verilerin nasıl düzenleneceğini ve silineceğini de araştırıyoruz.

Önümüzdeki öğreticilerimiz çeşitli önbelleğe alma tekniklerini anlatıyor. Önbelleğe alma, pahalı işlemlerden sonuçları alarak ve bunları daha hızlı erişilebilen bir konumda depolayarak, uygulamanın genel performansını artırmak için bir yol sağlar.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni bir Murphy idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](including-a-file-upload-option-when-adding-a-new-record-cs.md)
> [İleri](uploading-files-vb.md)
