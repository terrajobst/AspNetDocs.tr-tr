---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-vb
title: Yeni kayıt eklerken karşıya dosya yükleme seçeneği ekleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, kullanıcının metin verileri girmesine ve ikili dosyaları yüklemesine izin veren bir Web arabirimi oluşturma işleminin nasıl yapılacağı gösterilmektedir. Kullanılabilir seçenekleri göstermek için...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 5776281d-4637-4d1e-a65b-2621d2cade44
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-vb
msc.type: authoredcontent
ms.openlocfilehash: 8edaf1754eddd7b03f1c323d1bee13238582fc99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78588055"
---
# <a name="including-a-file-upload-option-when-adding-a-new-record-vb"></a>Yeni Kayıt Eklerken Karşıya Dosya Yükleme Seçeneği Ekleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_VB.exe) veya [PDF 'yi indirin](including-a-file-upload-option-when-adding-a-new-record-vb/_static/datatutorial56vb1.pdf)

> Bu öğreticide, kullanıcının metin verileri girmesine ve ikili dosyaları yüklemesine izin veren bir Web arabirimi oluşturma işleminin nasıl yapılacağı gösterilmektedir. İkili verileri depolamak için kullanılabilen seçenekleri göstermek için, diğeri dosya sisteminde depolanırken bir dosya veritabanına kaydedilir.

## <a name="introduction"></a>Giriş

Önceki iki öğreticide, uygulama veri modeliyle ilişkili ikili verileri depolama tekniklerini araştırırken, dosyaları istemciden Web sunucusuna göndermek için dosya yükleme denetiminin nasıl kullanılacağı ve bu ikili verilerin bir veri W 'da nasıl görüntüleneceği gördünüz. EB denetimi. Yine de karşıya yüklenen verileri veri modeliyle ilişkilendirme hakkında konuşuyoruz, ancak.

Bu öğreticide, yeni bir kategori eklemek için bir Web sayfası oluşturacağız. Kategori adı ve açıklaması için metin kutularına ek olarak, bu sayfanın yeni kategori s resmi ve bir broşür için bir tane olmak üzere iki dosya yükleme denetimini içermesi gerekir. Karşıya yüklenen resim, yeni kayıt s `Picture` sütununda doğrudan depolanacak, ancak broşür yeni kayıt s `BrochurePath` sütununda kaydedilen dosyanın yoluyla `~/Brochures` klasöre kaydedilir.

Bu yeni Web sayfasını oluşturmadan önce mimariyi güncelleştirmeniz gerekir. `CategoriesTableAdapter` s ana sorgusu `Picture` sütununu almaz. Sonuç olarak, otomatik olarak oluşturulan `Insert` yönteminin yalnızca `CategoryName`, `Description`ve `BrochurePath` alanları için girişleri vardır. Bu nedenle, TableAdapter 'ta dört `Categories` alanı için istemde bulunan ek bir yöntem oluşturuyoruz. Iş mantığı katmanındaki `CategoriesBLL` sınıfının de güncellenmesi gerekir.

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>1\. Adım:`CategoriesTableAdapter``InsertWithPicture`yöntemi ekleme

[Veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-vb.md) öğreticisinde geri `CategoriesTableAdapter` oluşturduğumuz, bunu ana sorguya göre otomatik olarak `INSERT`, `UPDATE`ve `DELETE` deyimlerini oluşturacak şekilde yapılandırdık. Üstelik, TableAdapter 'ın `Insert`, `Update`ve `Delete`' i oluşturan VERITABANı doğrudan yaklaşımını benimseme konusunda talimat verdik. Bu yöntemler, otomatik olarak oluşturulan `INSERT`, `UPDATE`ve `DELETE` deyimlerini yürütür ve sonuç olarak ana sorgu tarafından döndürülen sütunlara göre giriş parametrelerini kabul eder. [Dosyaları karşıya yükleme](uploading-files-vb.md) öğreticisinde, `BrochurePath` sütununu kullanmak için `CategoriesTableAdapter` s ana sorgusunu genişlettik.

`CategoriesTableAdapter` s ana sorgusu `Picture` sütununa başvurmadığından, yeni bir kayıt eklememiz veya mevcut bir kaydı `Picture` sütunu için bir değer ile güncelleştirebiliriz. Bu bilgileri yakalamak için, TableAdapter 'ta ikili verilerle bir kayıt eklemek için kullanılan yeni bir yöntem oluşturabilir ya da otomatik olarak oluşturulan `INSERT` ifadesini özelleştirebiliriz. Otomatik olarak oluşturulan `INSERT` deyimin özelleştirilmesi sorunu, özelleştirmelerimizin üzerine, sihirbaz tarafından geçersiz kılınmasından risklidir. Örneğin, `Picture` sütununun kullanımını dahil etmek için `INSERT` ifadesini özelleştirdiğinizi düşünün. Bu, TableAdapter s `Insert` yöntemini, kategori s Picture s ikili verileri için ek bir giriş parametresi içerecek şekilde güncelleştirir. Daha sonra bu DAL yöntemini kullanmak için Iş mantığı katmanında bir yöntem oluşturabilir ve bu BLL metodunu sunum katmanı üzerinden çağırabilirsiniz ve her şey wonderfully çalışacaktır. Diğer bir deyişle, TableAdapter Yapılandırma Sihirbazı aracılığıyla TableAdapter 'ı yapılandırdığımızda. Sihirbaz tamamlandıktan hemen sonra, `INSERT` deyimindeki özelleştirmelerimiz üzerine yazılır, `Insert` yöntemi eski biçimine döndürülür ve kodumuz artık derlenmeyebilir!

> [!NOTE]
> Bu annoyance, ad-hoc SQL deyimleri yerine saklı yordamlar kullanılırken bir sorun değildir. Gelecekteki bir öğreticide, veri erişim katmanında geçici SQL deyimleri yerine saklı yordamlar kullanılarak araştırılacak.

Bunun yerine, otomatik olarak oluşturulan SQL deyimlerini özelleştirmek yerine, bu olası headache 'i önlemek için TableAdapter için yeni bir yöntem oluşturun. `InsertWithPicture`adlı bu yöntem, `CategoryName`, `Description`, `BrochurePath`ve `Picture` sütunlarının değerlerini kabul eder ve tüm dört değeri yeni bir kayıtta depolayan bir `INSERT` ifadesini yürütür.

Türü belirtilmiş veri kümesini açın ve tasarımcıdan `CategoriesTableAdapter` s başlığına sağ tıklayıp bağlam menüsünden sorgu Ekle ' yi seçin. Bu, TableAdapter sorgusunun veritabanına nasıl erişmesi gerektiğini bize sorarak başlayan TableAdapter sorgu Yapılandırma Sihirbazı 'nı başlatır. SQL deyimlerini kullan ' ı seçin ve Ileri ' ye tıklayın. Sonraki adım, oluşturulacak sorgu türünü sorar. `Categories` tabloya yeni bir kayıt eklemek için bir sorgu oluşturduğumuz için, Ekle ' yi seçin ve Ileri ' ye tıklayın.

[![Ekle seçeneğini belirleyin](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image1.png)

**Şekil 1**: Ekle seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image2.png))

Artık `INSERT` SQL ifadesini belirtmemiz gerekir. Sihirbaz, TableAdapter s ana sorgusuna karşılık gelen bir `INSERT` ifadesini otomatik olarak önerir. Bu durumda, `CategoryName`, `Description`ve `BrochurePath` değerlerini ekleyen bir `INSERT` deyimidir. `Picture` sütunun bir `@Picture` parametresiyle birlikte dahil edilmesini sağlamak için ifadeyi güncelleştirin, örneğin:

[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample1.sql)]

Sihirbazın son ekranında yeni TableAdapter metodunu adlandırma bize sorulur. `InsertWithPicture` girin ve son ' a tıklayın.

[![yeni TableAdapter metodunu ınsertwithpicture olarak adlandırın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image3.png)

**Şekil 2**: yeni TableAdapter metodunu adlandırma `InsertWithPicture` ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image4.png))

## <a name="step-2-updating-the-business-logic-layer"></a>2\. Adım: Iş mantığı katmanını güncelleştirme

Sunum katmanı yalnızca veri erişim katmanına doğrudan gitmek yerine yalnızca Iş mantığı katmanıyla arabirim gerektirdiğinden, yeni oluşturduğumuz DAL yöntemini (`InsertWithPicture`) çağıran bir BLL yöntemi oluşturuyoruz. Bu öğreticide, giriş üç `String` ve bir `Byte` dizisi olarak kabul eden `InsertWithPicture` adlı `CategoriesBLL` sınıfında bir yöntem oluşturun. `String` giriş parametreleri, kategori s adı, açıklaması ve broşür dosya yolu için, `Byte` dizisi ise kategori s resminin ikili içeriğine yöneliktir. Aşağıdaki kodda gösterildiği gibi, bu BLL yöntemi karşılık gelen DAL yöntemini çağırır:

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample2.vb)]

> [!NOTE]
> `InsertWithPicture` metodunu BLL 'e eklemeden önce, yazılan veri kümesini kaydettiğinizden emin olun. `CategoriesTableAdapter` sınıfı kodu, türü belirtilmiş veri kümesine göre otomatik olarak oluşturulduğundan, yaptığınız değişiklikleri ilk olarak yazılan veri kümesine kaydedemezsiniz `Adapter` özelliği `InsertWithPicture` yöntemi hakkında bilgi vermez.

## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>3\. Adım: mevcut kategorileri ve bunların Ikili verilerini listeleme

Bu öğreticide, son kullanıcının sisteme yeni bir kategori eklemesine izin veren bir sayfa oluşturacak ve yeni kategori için bir resim ve broşür sağlamamız gerekir. [Önceki öğreticide](displaying-binary-data-in-the-data-web-controls-vb.md) , her bir kategorinin adını, açıklamasını, resmini ve bir bağlantıyı, onun broşürini indirmek için bir bağlantı görüntüleyecek bir TemplateField ve ImageField Içeren bir GridView kullandık. Bu öğreticide, her iki mevcut kategoriyi listeleyen ve yenilerini oluşturulmasına izin veren bir sayfa oluşturmak için bu işlevselliği çoğaltmasına izin verin.

`BinaryData` klasöründen `DisplayOrDownload.aspx` sayfasını açarak başlayın. Kaynak görünümüne gidin ve GridView ve ObjectDataSource öğelerinin bildirime dayalı sözdizimini kopyalayın ve `UploadInDetailsView.aspx``<asp:Content>` öğesi içinde yapıştırın. Ayrıca, `DisplayOrDownload.aspx` arka plan kod sınıfından `UploadInDetailsView.aspx``GenerateBrochureLink` yöntemi kopyalamayı unutmayın.

[![DisplayOrDownload. aspx konumundan Uploadındetailsview. aspx ' e bildirim temelli sözdizimini kopyalayıp yapıştırın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image5.png)

**Şekil 3**: `DisplayOrDownload.aspx` bildirime dayalı sözdizimini kopyalayıp `UploadInDetailsView.aspx` yapıştırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image6.png))

Bildirim temelli sözdizimini ve `GenerateBrochureLink` yöntemini `UploadInDetailsView.aspx` sayfasına kopyaladıktan sonra, her şeyin doğru şekilde kopyalandığından emin olmak için sayfayı bir tarayıcı üzerinden görüntüleyin. Broşür ve kategori s resmini indirmek için bir bağlantı içeren sekiz kategorinin listelendiği bir GridView görmeniz gerekir.

[![her kategoriyi Ikili verilerle birlikte görmeniz gerekir](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image7.png)

**Şekil 4**: artık her kategoriyi Ikili verilerle birlikte görmeniz gerekir ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image8.png))

## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>4\. Adım: eklemeyi desteklemek için`CategoriesDataSource`yapılandırma

`Categories` GridView tarafından kullanılan `CategoriesDataSource` ObjectDataSource Şu anda veri ekleme özelliği sağlamıyor. Bu veri kaynağı denetimini eklemeyi desteklemek için, `Insert` yöntemini temel alınan nesnesindeki bir yönteme eşliyoruz gerekir, `CategoriesBLL`. Özellikle, bu dosyayı adım 2 ' de geri eklediğimiz `CategoriesBLL` yöntemiyle eşlemek istiyoruz `InsertWithPicture`.

Başlat ' ın akıllı etiketinden veri kaynağını Yapılandır bağlantısına tıklayarak başlayın. İlk ekranda, veri kaynağının ile birlikte çalışmak üzere yapılandırıldığı nesne gösterilir `CategoriesBLL`. Bu ayarı olduğu gibi bırakın ve veri yöntemlerini tanımla ekranına ilerlemek için Ileri ' ye tıklayın. Ekle sekmesine gidin ve açılan listeden `InsertWithPicture` yöntemini seçin. Sihirbazı tamamladığınızda son ' a tıklayın.

[![ınsertwithpicture metodunu kullanmak için ObjectDataSource 'ı yapılandırma](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image9.png)

**Şekil 5**: `InsertWithPicture` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image10.png))

> [!NOTE]
> Sihirbaz tamamlandıktan sonra Visual Studio, veri Web denetimleri alanlarını yeniden oluşturacak alanları ve anahtarları yenilemek isteyip istemediğinizi sorabilir. Evet ' i seçmek, yapmış olduğunuz tüm alan özelleştirmelerinin üzerine yazacak şekilde Hayır ' ı seçin.

Sihirbazı tamamladıktan sonra, ObjectDataSource artık `InsertMethod` özelliği için bir değer ve dört Kategori sütunu için `InsertParameters` ve aşağıdaki bildirime dayalı biçimlendirme gösterilmektedir:

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>5\. Adım: ekleme arabirimi oluşturma

[Veri ekleme, güncelleştirme ve silme konusunda genel bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)kapsamında, DetailsView denetimi, eklemeyi destekleyen bir veri kaynağı denetimiyle çalışırken kullanılabilecek bir yerleşik ekleme arabirimi sağlar. Ekleme arabirimini kalıcı olarak işleyecek GridView 'un bu sayfaya bir DetailsView denetimi ekleyelim, böylece bir kullanıcının kolayca yeni bir kategori eklemesine izin verilir. DetailsView 'a yeni bir kategori eklendiğinde, bunun altındaki GridView otomatik olarak yenilenir ve yeni kategoriyi görüntüler.

Araç kutusundan GridView 'un üzerindeki tasarımcı üzerine bir DetailsView sürükleyip `ID` özelliğini `NewCategory` ve `Height` ve `Width` özellik değerlerini temizleyerek başlatın. DetailsView 'un akıllı etiketinde, mevcut `CategoriesDataSource` bağlayın ve sonra eklemeyi etkinleştir onay kutusunu işaretleyin.

[DetailsView öğesini Kategorilerverikaynağına bağlamak ve ekleme özelliğini etkinleştirmek ![](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image11.png)

**Şekil 6**: DetailsView 'ı `CategoriesDataSource` bağlayın ve eklemeyi etkinleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image12.png))

DetailsView 'u ekleme arabiriminde kalıcı olarak işlemek için `DefaultMode` özelliğini `Insert`olarak ayarlayın.

DetailsView 'un `BrochurePath` özelliği `CategoryID` olarak ayarlandığı için, `InsertVisible` BoundField `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`ve `False`beş BoundFields olduğunu unutmayın. Bu BoundFields, ObjectDataSource 'un verileri almak için çağırdığı `GetCategories()` yöntemi tarafından döndürülen sütunlar olduklarından oluşur. Bununla birlikte, ekleme için kullanıcının `NumberOfProducts`bir değer belirtmesini istiyorum. Üstelik, bu kullanıcıların yeni kategori için bir resim yüklemesine ve broşür için bir PDF 'YI karşıya yüklemesine izin vermemiz gerekir.

DetailsView `NumberOfProducts` BoundField öğesini tamamen kaldırın ve ardından `CategoryName` ve `BrochurePath` BoundFields `HeaderText` özelliklerini sırasıyla kategori ve broşür olarak güncelleştirin. Sonra, `BrochurePath` BoundField öğesini TemplateField öğesine dönüştürün ve resme yeni bir TemplateField ekleyin, bu yeni TemplateField değerini bir resim `HeaderText` olarak verir. `Picture` TemplateField alanını `BrochurePath` TemplateField ve CommandField arasında olacak şekilde taşıyın.

![DetailsView 'u Kategorilerverikaynağına bağlayın ve eklemeyi etkinleştirin](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image7.gif)

**Şekil 7**: DetailsView 'ı `CategoriesDataSource` bağlayın ve eklemeyi etkinleştirin

Alanları Düzenle iletişim kutusu aracılığıyla `BrochurePath` BoundField öğesini bir TemplateField 'a dönüştürdüyseniz, TemplateField bir `ItemTemplate`, `EditItemTemplate`ve `InsertItemTemplate`içerir. Ancak yalnızca `InsertItemTemplate` gereklidir, bu nedenle diğer iki şablonu kaldırmayı ücretsiz olarak hissetmekten çekinmeyin. Bu noktada, DetailsView 'un bildirime dayalı sözdizimi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>Broşür ve resim alanları için dosya yükleme denetimleri ekleme

Şu anda `BrochurePath` TemplateField `InsertItemTemplate` bir TextBox içerir, ancak `Picture` TemplateField herhangi bir şablon içermez. Bu iki TemplateField s `InsertItemTemplate`, dosya yükleme denetimlerini kullanacak şekilde güncelleştirmemiz gerekiyor.

DetailsView 'un akıllı etiketinde Şablonları Düzenle seçeneğini belirleyin ve ardından açılan listeden `BrochurePath` TemplateField `InsertItemTemplate` ' ı seçin. TextBox ' ı kaldırın ve ardından araç kutusundan bir dosya yükleme denetimini şablona sürükleyin. Dosya karşıya yükleme denetim s `ID` `BrochureUpload`olarak ayarlayın. Benzer şekilde, `Picture` TemplateField s `InsertItemTemplate`bir dosya karşıya yükleme denetimi ekleyin. Bu dosya yükleme denetim s `ID` `PictureUpload`olarak ayarlayın.

[InsertItemTemplate 'e dosya yükleme denetimi ekleme ![](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image13.png)

**Şekil 8**: `InsertItemTemplate` bir dosya yükleme denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image14.png))

Bu eklemeleri yaptıktan sonra, iki TemplateField bildirim sözdizimi şu şekilde olur:

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample5.aspx)]

Bir Kullanıcı yeni bir kategori eklediğinde, broşür ve resmin doğru dosya türünde olduğundan emin olmak istiyoruz. Broşür için kullanıcının bir PDF sağlaması gerekir. Resimde, kullanıcının bir resim dosyasını karşıya yüklemesi gerekir, ancak *herhangi* bir görüntü dosyası ya da yalnızca belirli bir türdeki (örneğin, GIF 'Ler veya jpgs) görüntü dosyaları izin veririz. Farklı dosya türlerine izin vermek için, `Categories` şemayı, bu türün `DisplayCategoryPicture.aspx`içindeki `Response.ContentType` aracılığıyla istemciye gönderilebilmesi için dosya türünü yakalayan bir sütun içerecek şekilde genişletmemiz gerekir. Böyle bir sütun olmadığı için, kullanıcıların yalnızca belirli bir görüntü dosyası türü sağlaması için akıllıca olur. `Categories` tablo var olan görüntüler bit eşlemlerdir, ancak JPGs Web üzerinden sunulan görüntüler için daha uygun bir dosya biçimidir.

Bir Kullanıcı yanlış bir dosya türünü karşıya yüklediğinde, eklemeyi iptal etmemiz ve sorunu belirten bir ileti görüntülemesi gerekir. DetailsView 'un altına bir etiket Web denetimi ekleyin. `ID` özelliğini `UploadWarning`olarak ayarlayın, `Text` özelliğini temizleyin, `CssClass` özelliğini uyarı olarak ayarlayın ve `Visible` ve `EnableViewState` özelliklerini `False`. `Warning` CSS sınıfı `Styles.css` tanımlanır ve metni büyük, kırmızı, italik, kalın yazı tipiyle işler.

> [!NOTE]
> İdeal olarak, `CategoryName` ve `Description` BoundFields alanları TemplateFields 'e, eklenen arabirimleri de özelleştirilmiş olarak dönüştürülür. Örneğin, `Description` ekleme arabirimi, büyük olasılıkla çok satırlı bir metin kutusuyla daha uygun olabilir. `CategoryName` sütunu `NULL` değerlerini kabul etmediğinden, kullanıcının yeni kategori s adı için bir değer sağladığından emin olmak için bir RequiredFieldValidator eklenmelidir. Bu adımlar, okuyucuya bir alıştırma olarak kalır. Veri değiştirme arabirimlerini genişletmekten derinlemesine bir bakış için [veri değiştirme arabirimini özelleştirmek](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) üzere geri bakın.

## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>6\. Adım: karşıya yüklenen broşürü Web sunucusu s dosya sistemine kaydetme

Kullanıcı yeni bir kategorinin değerlerini girdiğinde ve Ekle düğmesine tıkladığında, bir geri gönderme gerçekleşir ve iş akışı kaldırılıyor. İlk olarak, DetailsView [`ItemInserting` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx) ateşlenir. Ardından, ObjectDataSource s `Insert()` yöntemi çağrılır ve bu, `Categories` tablosuna yeni bir kaydın eklenmesine neden olur. Bundan sonra, DetailsView [`ItemInserted` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx) ateşlenir.

ObjectDataSource `Insert()` yöntemi çağrılmadan önce, önce uygun dosya türlerinin Kullanıcı tarafından karşıya yüklendiğinden emin olunması ve sonra Broşür PDF 'YI Web sunucusu s dosya sistemine kaydetmeniz gerekir. DetailsView `ItemInserting` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample6.vb)]

Olay işleyicisi, DetailsView 'un şablonlarından `BrochureUpload` FileUpload denetimine başvurulduğunda başlar. Daha sonra, bir broşür karşıya yüklenmişse karşıya yüklenen dosya uzantıları incelenir. Uzantı yoksa. PDF, sonra bir uyarı görüntülenir, ekleme iptal edilir ve olay işleyicisinin yürütülmesi sona erer.

> [!NOTE]
> Karşıya yüklenen dosya uzantısına bağlı olarak, karşıya yüklenen dosyanın bir PDF belgesi olduğundan emin olmak için bir,-Fire yöntemi değildir. Kullanıcının uzantısı `.Brochure`geçerli bir PDF belgesi olabilir ya da PDF olmayan bir belge alınmış ve bir `.pdf` uzantısı vermiş olabilir. Dosya türünü daha yaratacağı doğrulamak için dosyanın ikili içeriğinin programlı bir şekilde incelenmesi gerekir. Ancak, bu tür kapsamlı yaklaşımlar genellikle fazla sonlandırılmalıdır; uzantının çoğu senaryo için yeterli olup olmadığı denetleniyor.

[Dosyaları karşıya](uploading-files-vb.md) yükleme öğreticisinde açıklandığı gibi, bir kullanıcının karşıya yüklenmesi başka bir veritabanının üzerine yazılmaması için dosyaları dosya sistemine kaydederken dikkatli olunmalıdır. Bu öğretici için karşıya yüklenen dosyayla aynı adı kullanmayı deneyeceğiz. `~/Brochures` dizininde aynı dosya adıyla bir dosya zaten varsa, benzersiz bir ad bulunana kadar sonuna bir sayı eklenir. Örneğin, Kullanıcı `Meats.pdf`adlı bir broşür dosyasını karşıya yüklediğinde, ancak `~/Brochures` klasöründe `Meats.pdf` adında bir dosya zaten varsa, kaydedilen dosya adını `Meats-1.pdf`olarak değiştireceksiniz. Bu varsa, benzersiz bir dosya adı bulunana kadar `Meats-2.pdf`, vb. deneyeceğiz.

Aşağıdaki kod, belirtilen dosya adına sahip bir dosyanın zaten mevcut olup olmadığını anlamak için [`File.Exists(path)` yöntemini](https://msdn.microsoft.com/library/system.io.file.exists.aspx) kullanır. Bu durumda, çakışma bulunana kadar broşür için yeni dosya adları denemeye devam eder.

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample7.vb)]

Geçerli bir dosya adı bulunduğunda, dosyanın dosya sistemine kaydedilmesi gerekir ve bu dosya adının veritabanına yazılması için ObjectDataSource s `brochurePath``InsertParameter` değerinin güncelleştirilmesi gerekir. *Karşıya yükleme dosyaları* öğreticisinde geri döndüğünüzde dosya, FileUpload denetim s `SaveAs(path)` yöntemi kullanılarak kaydedilebilir. ObjectDataSource s `brochurePath` parametresini güncelleştirmek için `e.Values` koleksiyonunu kullanın.

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample8.vb)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>7\. Adım: karşıya yüklenen resmi veritabanına kaydetme

Karşıya yüklenen resmi yeni `Categories` kaydına depolamak için, karşıya yüklenen ikili içeriği, DetailsView s `ItemInserting` olayında ObjectDataSource s `picture` parametresine atamamız gerekir. Ancak, bu atamayı yapmadan önce karşıya yüklenen resmin başka bir görüntü türü değil, bir JPG olduğundan emin olmanız gerekir. Adım 6 ' da olduğu gibi, ' ın türünü belirlemek için karşıya yüklenen resim dosyası uzantısını kullanmasına izin verin.

`Categories` tablosu `Picture` sütunu için `NULL` değerlere izin verdiğinden, tüm kategorilerin Şu anda bir resmi vardır. Bu sayfa aracılığıyla yeni bir kategori eklerken kullanıcıya bir resim sağlamaya izin verin. Aşağıdaki kod, bir resmin karşıya yüklenmiş ve uygun bir uzantıya sahip olduğundan emin olmak için kontrol eder.

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample9.vb)]

Bu kod 6. adımdaki koddan *önce* yerleştirilmelidir, böylece resim karşıya yükleme ile ilgili bir sorun varsa, broşür dosyası dosya sistemine kaydedilmeden önce olay işleyicisi sonlandırılır.

Uygun bir dosyanın karşıya yüklendiğini varsayarak, karşıya yüklenen ikili içeriği resim parametresi s değerine aşağıdaki kod satırıyla atayın:

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample10.vb)]

## <a name="the-completeiteminsertingevent-handler"></a>Tüm`ItemInserting`olay Işleyicisi

Tamamlanma için, `ItemInserting` olay işleyicisi tamamen aşağıda verilmiştir:

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample11.vb)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>8\. Adım:`DisplayCategoryPicture.aspx`sayfasını Düzeltme

Son birkaç adımda oluşturulan ekleme arabirimini ve `ItemInserting` olay işleyicisini test etmek için bir süre bekleyin. `UploadInDetailsView.aspx` sayfasını bir tarayıcıda ziyaret edin ve bir kategori eklemeyi deneyin, ancak resmi atlayın veya JPG olmayan bir resim ya da PDF olmayan bir broşür belirtin. Bu durumların hiçbirinde, bir hata iletisi görüntülenir ve ekleme iş akışı iptal edilir.

[Geçersiz bir dosya türü karşıya yüklenirse bir uyarı Iletisi ![görüntülenir](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image15.png)

**Şekil 9**: geçersiz bir dosya türü karşıya yüklenirse bir uyarı iletisi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image16.png))

Sayfanın karşıya yükleneceğini ve PDF olmayan ya da JPG olmayan dosyaları kabul etmeyeceği doğrulandıktan sonra, geçerli bir JPG resmine sahip yeni bir kategori ekleyerek, broşür alanını boş bırakın. Ekle düğmesine tıkladıktan sonra, sayfa geri gönderilir ve yeni bir kayıt, `Categories` tablosuna doğrudan veritabanında depolanan karşıya yüklenen resim ikili içeriğiyle birlikte eklenir. GridView güncellenir ve yeni eklenen kategori için bir satır gösterir, ancak Şekil 10 ' un gösterdiği gibi, yeni kategorinin resmi doğru işlenmez.

[Yeni kategorinin resim ![görüntülenmiyor](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image17.png)

**Şekil 10**: yeni kategori resmi görüntülenmiyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image18.png))

Yeni resmin görüntülenmediği nedeni, belirtilen bir kategori resmini döndüren `DisplayCategoryPicture.aspx` sayfasının, OLE üst bilgisi olan bit eşlemleri işleyecek şekilde yapılandırılmasının nedeni. Bu 78 bayt üst bilgisi, istemciye geri gönderilmeden önce `Picture` sütundan ikili içeriklerden çıkarılır. Ancak yeni kategoride karşıya yüklediğiniz JPG dosyası bu OLE başlığına sahip değil; Bu nedenle, geçerli ve gerekli baytlar Image s binary verilerinden kaldırılıyor.

`Categories` tablosunda hem OLE üst bilgileri hem de JPGs olan bit eşlemler olduğundan, OLE üst bilgisinin orijinal sekiz kategoriye göre olması ve daha yeni kategori kayıtları için bu kadar bu kadar bu kadar bu kadar bu kadar bu kadar bu kadar bu kadar bu kadar bu kadar devam edebilmesi için `DisplayCategoryPicture.aspx` güncelleştirme Sonraki öğreticimizde, var olan bir kayıt görüntüsünü güncelleştirmeyi inceleyeceğiz ve tüm eski kategori resimlerini JPGs olacak şekilde güncelleştireceğiz. Şimdilik, yalnızca özgün sekiz kategori için OLE üstbilgilerini eklemek üzere `DisplayCategoryPicture.aspx` ' de aşağıdaki kodu kullanın:

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample12.vb)]

Bu değişiklik ile, JPG görüntüsü artık GridView 'da doğru şekilde işlenir.

[Yeni kategoriler için JPG görüntülerinin ![doğru şekilde Işlendiğine](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image19.png)

**Şekil 11**: yeni KATEGORILER Için jpg resimleri doğru işlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image20.png))

## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>9\. Adım: bir özel durum durumunda broşürü silme

Web sunucusu s dosya sisteminde ikili verileri depolamanın güçlüklerinden biri, veri modeli ve onun ikili verileri arasında bir bağlantı kesmeyi sunmakta. Bu nedenle, bir kayıt silindiğinde dosya sistemindeki karşılık gelen ikili verilerin de kaldırılması gerekir. Bu, ekleme sırasında da oynatılmasına gelebilir. Aşağıdaki senaryoyu göz önünde bulundurun: bir Kullanıcı, geçerli bir resim ve broşür belirten yeni bir kategori ekler. Ekle düğmesine tıklandıktan sonra, bir geri gönderme gerçekleşir ve DetailsView `ItemInserting` olay ateşlenir ve bu da broşür Web sunucusu s dosya sistemine kaydediliyor. Daha sonra, `CategoriesTableAdapter` s `InsertWithPicture` yöntemini çağıran `CategoriesBLL` sınıf s `InsertWithPicture` yöntemini çağıran ObjectDataSource s `Insert()` yöntemi çağrılır.

Şimdi, veritabanı çevrimdışıysa veya `INSERT` SQL deyimindeki bir hata varsa ne olur? Açıkça ekleme başarısız olur, bu nedenle veritabanına yeni bir kategori satırı eklenmez. Ancak yine de karşıya yüklenen broşür dosyası Web sunucusu s dosya sisteminde oturduk! Bu dosyanın, ekleme iş akışı sırasında bir özel durum durumunda silinmesi gerekir.

Daha önce [bir ASP.NET sayfa öğreticisindeki BLL ve dal düzeyi özel durumları işleme](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) konusunda anlatıldığı gibi, bir özel durum, mimarinin derinliğinden farklı katmanlar aracılığıyla kabarcıklanmasını. Sunum katmanında, DetailsView `ItemInserted` olayından bir özel durumun oluşup oluşmadığını belirleyebiliriz. Bu olay işleyicisi, `InsertParameters`ObjectDataSource 'un değerlerini de sağlar. Bu nedenle, bir özel durum olup olmadığını denetleyen `ItemInserted` olayı için bir olay işleyicisi oluşturuyoruz ve bu durumda, ObjectDataSource s `brochurePath` parametresi tarafından belirtilen dosyayı siler:

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample13.vb)]

## <a name="summary"></a>Özet

İkili veri içeren kayıtları eklemek için Web tabanlı bir arabirim sağlamak üzere gerçekleştirilmesi gereken birkaç adım vardır. İkili veriler doğrudan veritabanına depolanıyorsa, bu durumda, ikili verilerin eklendiği durumu işlemek için belirli yöntemler ekleyerek mimariyi güncelleştirmeniz gerekir. Mimari güncelleştirildikten sonra, bir sonraki adım, her bir ikili veri alanı için bir dosya karşıya yükleme denetimi içerecek şekilde özelleştirilmiş bir DetailsView kullanılarak gerçekleştirilebilen ekleme arabirimini oluşturmaktır. Karşıya yüklenen veriler daha sonra Web sunucusu s dosya sistemine kaydedilebilir veya DetailsView s `ItemInserting` olay işleyicisinde bir veri kaynağı parametresine atanabilir.

İkili verileri dosya sistemine kaydetmek, verileri doğrudan veritabanına kaydetmeye kıyasla daha fazla planlama gerektirir. Bir Kullanıcı yüklemesinin karşıya yüklenmesini önlemek için bir adlandırma düzeni seçilmelidir. Ayrıca, veritabanı ekleme başarısız olursa karşıya yüklenen dosyayı silmek için ek adımların alınması gerekir.

Artık, bir broşür ve resimle sisteme yeni kategoriler ekleyebilme olanağı sunuyoruz, ancak mevcut bir kategorinin ikili verilerinin nasıl güncelleştireceğiz veya silinen bir kategorinin ikili verilerinin nasıl doğru şekilde kaldırılacağı hakkında daha fazla bakıyoruz. Sonraki öğreticide bu iki konuyu araştıracağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Gardner, Teresa Murphy ve Bernadette Leigh. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](displaying-binary-data-in-the-data-web-controls-vb.md)
> [İleri](updating-and-deleting-existing-binary-data-vb.md)
