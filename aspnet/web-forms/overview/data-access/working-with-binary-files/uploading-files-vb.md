---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
title: Dosyalar karşıya yükleniyor (VB) | Microsoft Docs
author: rick-anderson
description: Kullanıcıların, ikili dosyaları (Word veya PDF belgeleri gibi), sunucunun dosya sisteminde depolanabileceği Web sitenize yüklemesine nasıl izin vereceğinizi öğrenin...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: f7c00fbd-652c-433d-8ed3-0e5168a4d4df
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e0d57ef2f1e8132f19777a7d14e94611c68adcd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615220"
---
# <a name="uploading-files-vb"></a>Karşıya Dosya Yükleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_VB.exe) veya [PDF 'yi indirin](uploading-files-vb/_static/datatutorial54vb1.pdf)

> Kullanıcıların, dosyanın dosya sisteminde veya veritabanında saklanabileceği Web sitenize ikili dosyaları (Word veya PDF belgeleri gibi) karşıya yüklemesine nasıl izin vereceğinizi öğrenin.

## <a name="introduction"></a>Giriş

Şimdiye kadar incelediğimiz tüm öğreticiler metin verileriyle özel olarak çalıştık. Ancak, birçok uygulamanın hem metin hem de ikili verileri yakalayan veri modelleri vardır. Çevrimiçi bir site, kullanıcıların profiliyle ilişkilendirmek üzere bir resmi karşıya yüklemesine izin verebilir. Bir işe alma Web sitesi, kullanıcıların özgeçmişini bir Microsoft Word veya PDF belgesi olarak karşıya yüklemesine izin verebilir.

İkili verilerle çalışma yeni bir zorluk kümesi ekler. İkili verilerin uygulamada nasıl depolanacağına karar vermelidir. Yeni kayıtları eklemek için kullanılan arabirimin, kullanıcının bilgisayarından bir dosyayı karşıya yüklemesine izin vermek için güncelleştirilmeleri ve kayıt ile ilişkili ikili verileri indirmek için bir yol sağlamak üzere ek adımların alınması gerekir. Bu öğreticide ve sonraki üç zorluk bu zorlukları nasıl ele alacağız. Bu öğreticilerin sonunda, her kategoriden bir resim ve PDF Broşürü ilişkilendiğinde tam işlevli bir uygulama oluşturacaksınız. Bu öğreticide, ikili verileri depolamak için farklı teknikler ele alacağız ve kullanıcıların bilgisayarından bir dosyayı karşıya yüklemesi ve Web sunucusu s dosya sistemine kaydedilmesini sağlama yöntemleri anlatılmaktadır.

> [!NOTE]
> Bir uygulama veri modelinin parçası olan ikili veriler bazen bir [BLOB](http://en.wikipedia.org/wiki/Binary_large_object)olarak adlandırılır, Ikili büyük nesne için bir kısaltma. Bu öğreticilerde, BLOB terimi eş anlamlı olsa da, terminoloji ikili verilerini kullanmayı seçtim.

## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>1\. Adım: Ikili veri Web sayfalarıyla çalışmayı oluşturma

İkili veriler için destek eklemeyle ilgili güçlükleri keşfetmeye başlamadan önce, Web sitesi projemizdeki Bu öğretici ve sonraki üç için gereken ASP.NET sayfalarını oluşturmak için önce bir süre sürme. `BinaryData`adlı yeni bir klasör ekleyerek başlayın. Ardından, aşağıdaki ASP.NET sayfalarını bu klasöre ekleyerek her bir sayfayı `Site.master` ana sayfasıyla ilişkilendirdiğinizden emin olun:

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`

![Ikili veri ile Ilgili öğreticiler için ASP.NET sayfaları ekleyin](uploading-files-vb/_static/image1.gif)

**Şekil 1**: ikili veri Ile ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `BinaryData` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](uploading-files-vb/_static/image2.gif)](uploading-files-vb/_static/image1.png)

**Şekil 2**: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image2.png))

Son olarak, bu sayfaları `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, GridView 'u geliştirmeyle sonra aşağıdaki biçimlendirmeyi ekleyin `<siteMapNode>`:

[!code-xml[Main](uploading-files-vb/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menüde artık Ikili veri öğreticileri ile çalışma için öğeler yer almaktadır.

![Site Haritası artık Ikili veri öğreticileri ile çalışmaya yönelik girişleri Içerir](uploading-files-vb/_static/image3.gif)

**Şekil 3**: site haritası artık Ikili veri öğreticileri ile çalışmaya yönelik girişleri içerir

## <a name="step-2-deciding-where-to-store-the-binary-data"></a>2\. Adım: Ikili verileri nerede depolayacağınıza karar verme

Uygulama veri modeliyle ilişkili ikili veriler iki konumdan birinde depolanabilir: Web sunucusu s dosya sisteminde, veritabanında depolanan dosyaya yönelik bir başvuruya sahip olan. ya da doğrudan veritabanı içinden (bkz. Şekil 4). Her yaklaşımın kendi profesyonelleri ve olumsuz yönleri vardır ve daha ayrıntılı bir tartışmayı birleşmiştir.

[![Ikili veriler dosya sisteminde veya doğrudan veritabanında depolanabilir](uploading-files-vb/_static/image4.gif)](uploading-files-vb/_static/image3.png)

**Şekil 4**: Ikili veriler dosya sisteminde veya doğrudan veritabanında depolanabilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](uploading-files-vb/_static/image4.png))

Northwind veritabanını her ürünle bir resmi ilişkilendirmek üzere uzatmak istediğinizi düşünün. Tek bir seçenek, bu görüntü dosyalarını Web sunucusu s dosya sisteminde depolamak ve yolu `Products` tablosuna kaydeder. Bu yaklaşımda, belki `varchar(200)`türünde `Products` tabloya bir `ImagePath` sütunu ekleyeceğiz. Kullanıcı Chai için bir resim yüklediğini, bu resim `~/Images/Tea.jpg`adresindeki Web sunucusu s dosya sisteminde depolanabilir; burada `~`, uygulamanın fiziksel yolunu temsil eder. Diğer bir deyişle, Web sitesinin kökü fiziksel yolda `C:\Websites\Northwind\`, `~/Images/Tea.jpg` `C:\Websites\Northwind\Images\Tea.jpg`eşdeğerdir. Resim dosyasını karşıya yükledikten sonra, `Products` tablosundaki Chai kaydını, `ImagePath` sütununun yeni görüntünün yolunu başvurduğu şekilde güncelleştirdik. Tüm ürün görüntülerinin uygulama s `Images` klasörüne yerleştirilmesi gerektiğine karar verdiğimiz durumlarda `~/Images/Tea.jpg` veya yalnızca `Tea.jpg` kullanabilirsiniz.

İkili verileri dosya sisteminde depolamanın başlıca avantajları şunlardır:

- Kısa süre içinde, doğrudan veritabanı içinde depolanan ikili verilerin depolanması ve alınması, dosya sistemi aracılığıyla verilerle çalışırken biraz daha fazla kod içerir. Ayrıca, bir kullanıcının ikili verileri görüntülemesi veya indirmesi için bu verilere yönelik bir URL ile sunulmaları gerekir. Veriler Web sunucusu s dosya sisteminde bulunuyorsa, URL basittir. Ancak veriler veritabanında depolanıyorsa, verileri alacak ve veritabanından döndürecek bir Web sayfasının oluşturulması gerekir.
- **İkili verilere daha fazla erişme** ikili verilere, verileri veritabanından çekmeyecek diğer hizmetler veya uygulamalar için erişilebilir olması gerekebilir. Örneğin, her ürünle ilişkili görüntülerin de [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol)aracılığıyla kullanıcılara açık olması gerekebilir, bu durumda ikili verileri dosya sisteminde depolamak istiyoruz.
- **Performans** ikili veriler dosya sisteminde depolanıyorsa, veritabanı sunucusu ve Web sunucusu arasındaki talep ve ağ tıkanıklığı, ikili veriler doğrudan veritabanı içinde depolanacaksa küçüktür.

İkili verileri dosya sisteminde depolamanın temel dezavantajı, verileri veritabanından ayırmasıdır. `Products` tablosundan bir kayıt silinirse, Web sunucusu s dosya sistemindeki ilişkili dosya otomatik olarak silinmez. Dosyayı silmek için ek kod yazdık veya dosya sistemi kullanılmayan, yalnız bırakılmış dosyalarla karışık olacak. Ayrıca, veritabanını yedeklerken, ilişkili ikili verilerin yedeklerini de dosya sisteminde gerçekleştirdiğinizden emin olmanız gerekir. Veritabanını başka bir siteye veya sunucuya taşımak benzer sorunlar doğurur.

Alternatif olarak, ikili veriler `varbinary`türünde bir sütun oluşturarak doğrudan bir Microsoft SQL Server 2005 veritabanında depolanabilir. Diğer değişken uzunluklu veri türleriyle benzer şekilde, bu sütunda tutulabilecek ikili verilerin maksimum uzunluğunu belirtebilirsiniz. Örneğin, en fazla 5.000 bayt ayırmak için `varbinary(5000)`; `varbinary(MAX)`, en fazla 2 GB depolama boyutuna izin verir.

İkili verileri doğrudan veritabanında depolamanın ana avantajı, ikili veriler ve veritabanı kaydı arasında sıkı bir şekilde yapılır. Bu, yedeklemeler veya veritabanını farklı bir siteye veya sunucuya taşıma gibi veritabanı yönetim görevlerini büyük ölçüde basitleştirir. Ayrıca, bir kaydın silinmesi karşılık gelen ikili verileri otomatik olarak siler. Ayrıca, ikili verileri veritabanında depolamanın daha hafif avantajları da vardır. Daha ayrıntılı bir tartışma için bkz. [ASP.NET 2,0 kullanarak Ikili dosyaları doğrudan veritabanında depolama](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx) .

> [!NOTE]
> Microsoft SQL Server 2000 ve önceki sürümlerde, `varbinary` veri türü en fazla 8.000 bayt sınırına sahipti. 2 GB 'a kadar ikili veri depolamak için, bunun yerine [`image` veri türünün](https://msdn.microsoft.com/library/ms187993.aspx) kullanılması gerekir. Ancak `MAX` SQL Server 2005 ' deki eklenmesiyle `image` veri türü kullanım dışı bırakılmıştır. Geriye dönük uyumluluk için hala desteklenmektedir, ancak Microsoft, `image` veri türünün gelecekte SQL Server bir sürümünde kaldırılacağını duyurmuştur.

Daha eski bir veri modeliyle çalışıyorsanız `image` veri türünü görebilirsiniz. Northwind veritabanı `Categories` tablosu, kategori için bir görüntü dosyasının ikili verilerini depolamak için kullanılabilecek bir `Picture` sütununa sahiptir. Northwind veritabanının Microsoft Access ve daha önceki SQL Server sürümlerindeki köklerine sahip olduğundan, bu sütun `image`türündedir.

Bu öğretici ve sonraki üç yaklaşım için her iki yaklaşımı de kullanacağız. `Categories` tabloda, kategori için bir görüntünün ikili içeriğini depolamak üzere bir `Picture` sütunu zaten var. Kategoriye bir yazdırma kalitesi, şık bir genel bakış sağlamak için kullanılabilen Web sunucusu s dosya sisteminde bir PDF 'nin yolunu depolamak üzere `BrochurePath`ek bir sütun ekleyeceğiz.

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>Adım 3:`Categories`tabloya`BrochurePath`sütununu ekleme

Şu anda Kategoriler tablosu yalnızca dört sütuna sahiptir: `CategoryID`, `CategoryName`, `Description`ve `Picture`. Bu alanlara ek olarak, (varsa) kategori broşürleri işaret edecek yeni bir tane eklememiz gerekiyor. Bu sütunu eklemek için Sunucu Gezgini gidin, tablolarda ayrıntıya gidin, `Categories` tablosuna sağ tıklayın ve tablo tanımını aç ' ı seçin (bkz. Şekil 5). Sunucu Gezgini görmüyorsanız, Görünüm menüsünden Sunucu Gezgini seçeneğini seçerek veya CTRL + ALT + S tuşlarına basın.

`BrochurePath` adlı `Categories` tabloya yeni bir `varchar(200)` sütunu ekleyin ve `NULL` s 'ye izin verir ve kaydet simgesine tıklayın (veya CTRL + S tuşlarına basın).

[Kategoriler tablosuna bir BrochurePath sütunu eklemek ![](uploading-files-vb/_static/image5.gif)](uploading-files-vb/_static/image5.png)

**Şekil 5**: `Categories` tablosuna bir `BrochurePath` sütunu ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image6.png))

## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>4\. Adım: mimariyi`Picture`ve`BrochurePath`sütunları kullanacak şekilde güncelleştirme

Veri erişim katmanındaki (DAL) `CategoriesDataTable` Şu anda dört `DataColumn` s tanımlı: `CategoryID`, `CategoryName`, `Description`ve `NumberOfProducts`. [Veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-vb.md) öğreticisinde başlangıçta bu DataTable 'ı tasarladığımızda, `CategoriesDataTable` yalnızca ilk üç sütun içeriyordu; `NumberOfProducts` sütunu, [Ayrıntılar DataList öğreticisi Ile madde Işaretli ana kayıt listesi kullanılarak ana/ayrıntıya](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) eklenmiştir.

*Veri erişim katmanı oluşturma*bölümünde açıklandığı gibi, yazılan veri kümesindeki DataTable iş nesnelerini oluşturur. TableAdapters, veritabanıyla iletişim kurmaktan ve iş nesnelerinin sorgu sonuçlarıyla doldurulmasından sorumludur. `CategoriesDataTable`, üç veri alma yöntemine sahip olan `CategoriesTableAdapter`doldurulur:

- `GetCategories()` TableAdapter s ana sorgusunu yürütür ve `Categories` tablosundaki tüm kayıtların `CategoryID`, `CategoryName`ve `Description` alanlarını döndürür. Ana sorgu, otomatik olarak oluşturulan `Insert` ve `Update` yöntemleri tarafından kullanılır.
- `GetCategoryByCategoryID(categoryID)`, `CategoryID` eşit *CategoryID*değerine sahip kategorinin `CategoryID`, `CategoryName`ve `Description` alanlarını döndürür.
- `GetCategoriesAndNumberOfProducts()`-`Categories` tablosundaki tüm kayıtlar için `CategoryID`, `CategoryName`ve `Description` alanlarını döndürür. Ayrıca, her bir kategoriyle ilişkili ürün sayısını döndürmek için bir alt sorgu kullanır.

Bu sorguların hiçbirinin `Categories` tablo s `Picture` veya `BrochurePath` sütunları döndürmediğine dikkat edin; `CategoriesDataTable` bu alanlar için `DataColumn` s de sağlar. Resim ve `BrochurePath` özellikleriyle çalışmak için, önce bunları `CategoriesDataTable` eklemeli ve ardından `CategoriesTableAdapter` sınıfını bu sütunları döndürecek şekilde güncelleştirmemiz gerekir.

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>`Picture`ve`BrochurePath``DataColumn` s ekleme

Bu iki sütunu `CategoriesDataTable`ekleyerek başlayın. `CategoriesDataTable` s üstbilgisine sağ tıklayın, bağlam menüsünden Ekle ' yi seçin ve ardından sütun seçeneğini belirleyin. Bu, DataTable dosyasında `Column1`adlı yeni bir `DataColumn` oluşturur. Bu sütunu `Picture`olarak yeniden adlandırın. Özellikler penceresi, `DataColumn` s `DataType` özelliğini `System.Byte[]` olarak ayarlayın (Bu, açılan listede bir seçenek değildir; içine yazmanız gerekir).

[![veri türü System. Byte [] olan bir DataColumn adlı resim oluşturma](uploading-files-vb/_static/image6.gif)](uploading-files-vb/_static/image7.png)

**Şekil 6**: `DataType` `System.Byte[]` olan `Picture` adlı `DataColumn` oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image8.png))

DataTable 'a başka bir `DataColumn` ekleyin, `BrochurePath` varsayılan `DataType` değeri (`System.String`) kullanarak adlandırarak.

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>TableAdapter 'tan`Picture`ve`BrochurePath`değerlerini döndürme

Bu iki `DataColumn` `CategoriesDataTable`eklenmiş olan `CategoriesTableAdapter`güncelleştirilmeye yeniden hazırlandık. Bu sütun değerlerinin her ikisi de ana TableAdapter sorgusunda döndürüyoruz, ancak `GetCategories()` yöntemi her çağrıldığında ikili verileri geri getirecek. Bunun yerine, bir ana TableAdapter sorgusunu `BrochurePath` geri getirip, belirli bir kategorinin `Picture` sütununu döndüren ek bir veri alma yöntemi oluşturacak şekilde güncelleştirmesine izin verin.

Ana TableAdapter sorgusunu güncelleştirmek için `CategoriesTableAdapter` s üstbilgisine sağ tıklayın ve bağlam menüsünden Yapılandır seçeneğini belirleyin. Bu, bir dizi geçmiş öğreticilerde görtiğimiz tablo bağdaştırıcısı yapılandırma sihirbazını getirir. `BrochurePath` geri getirip son ' a tıklayarak sorguyu güncelleştirin.

[![SELECT deyimindeki sütun listesini güncelleştirmek için de BrochurePath döndürün](uploading-files-vb/_static/image7.gif)](uploading-files-vb/_static/image9.png)

**Şekil 7**: `SELECT` deyimindeki sütun listesini, ayrıca `BrochurePath` döndürmek için güncelleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image10.png))

TableAdapter için geçici SQL deyimleri kullanılırken, ana sorgudaki sütun listesini güncelleştirmek TableAdapter içindeki tüm `SELECT` sorgu yöntemlerinin sütun listesini günceller. Bu, `GetCategoryByCategoryID(categoryID)` yönteminin `BrochurePath` sütununu döndürecek şekilde güncelleştirildiği anlamına gelir. Bu, amaçlarız olabilir. Ancak, her bir kategorinin ürün sayısını döndüren alt sorguyu kaldırarak `GetCategoriesAndNumberOfProducts()` yöntemindeki sütun listesini de güncelleştirirler! Bu nedenle, bu yöntem `SELECT` sorgusunu güncelleştirmemiz gerekiyor. `GetCategoriesAndNumberOfProducts()` yöntemine sağ tıklayın, Yapılandır ' ı seçin ve `SELECT` sorgusunu özgün değerine geri geri alın:

[!code-sql[Main](uploading-files-vb/samples/sample2.sql)]

Sonra, belirli bir kategori `Picture` sütun değeri döndüren yeni bir TableAdapter yöntemi oluşturun. `CategoriesTableAdapter` s üstbilgisine sağ tıklayın ve TableAdapter sorgu Yapılandırma Sihirbazı 'nı başlatmak için Sorgu Ekle seçeneğini belirleyin. Bu sihirbazın ilk adımı, verileri geçici bir SQL ifadesini, yeni bir saklı yordamı veya var olan bir SQL ifadesini kullanarak sorgulamak isteyip istemediğinizi sorar. SQL deyimlerini kullan ' ı seçin ve Ileri ' ye tıklayın. Bir satır döndüyoruz, ikinci adımda satırları döndüren Seç seçeneğini belirleyin.

[![SQL deyimlerini kullan seçeneğini belirleyin](uploading-files-vb/_static/image8.gif)](uploading-files-vb/_static/image11.png)

**Şekil 8**: SQL deyimlerini kullan seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image12.png))

[Sorgu Kategoriler tablosundan bir kayıt döndürdüğünden ![, satırları döndüren Seç ' i seçin](uploading-files-vb/_static/image9.gif)](uploading-files-vb/_static/image13.png)

**Şekil 9**: sorgu Kategoriler tablosundan bir kayıt döndürecek olduğundan, satırları döndüren Seç[' i seçin (tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image14.png))

Üçüncü adımda, aşağıdaki SQL sorgusunu girin ve Ileri ' ye tıklayın:

[!code-sql[Main](uploading-files-vb/samples/sample3.sql)]

Son adım, yeni yöntemin adını seçdir. DataTable Fill ve sırasıyla bir DataTable desenleri döndüren `FillCategoryWithBinaryDataByCategoryID` ve `GetCategoryWithBinaryDataByCategoryID` kullanın. Sihirbazı tamamladığınızda son ' a tıklayın.

[TableAdapter s yöntemlerinin adlarını seçin ![](uploading-files-vb/_static/image10.gif)](uploading-files-vb/_static/image15.png)

**Şekil 10**: TableAdapter s metotları için adları seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image16.png))

> [!NOTE]
> Tablo bağdaştırıcısı sorgu Yapılandırma Sihirbazı 'Nı tamamladıktan sonra, yeni komut metninin, ana sorgunun şemasından farklı bir şemaya sahip verileri döndürdüğünü bildiren bir iletişim kutusu görebilirsiniz. Kısaca, sihirbaz TableAdapter ana sorgusunun `GetCategories()` yeni oluşturduğumuz olandan farklı bir şema döndürdüğünden emin olur. Ancak bu durum, bu iletiyi yoksayabilirsiniz.

Ayrıca, geçici SQL deyimlerini kullanıyorsanız ve daha sonra TableAdapter s ana sorgusunu değiştirmek için Sihirbazı kullanırsanız, `GetCategoryWithBinaryDataByCategoryID` yöntemi `SELECT` deyim listesini ana sorgudan yalnızca bu sütunları içerecek şekilde değiştirecek (yani `Picture` sütununu sorgudan kaldıracak) göz önünde bulundurmanız gerekir.) Bu adımda daha önce `GetCategoriesAndNumberOfProducts()` yöntemi ile yaptığımız gibi `Picture` sütununu döndürecek şekilde sütun listesini el ile güncelleştirmeniz gerekir.

İki `DataColumn` `CategoriesDataTable` ve `GetCategoryWithBinaryDataByCategoryID` `CategoriesTableAdapter`yöntemine eklendikten sonra, yazılan veri kümesi tasarımcısında bu sınıfların Şekil 11 ' de ekran görüntüsü gibi görünmesi gerekir.

![Veri kümesi Tasarımcısı yeni sütunları ve yöntemi Içerir](uploading-files-vb/_static/image11.gif)

**Şekil 11**: veri kümesi Tasarımcısı yeni sütunları ve yöntemi içerir

## <a name="updating-the-business-logic-layer-bll"></a>Iş mantığı katmanını (BLL) güncelleştirme

DAL güncelleştirildiğinden, her şey, yeni `CategoriesTableAdapter` yöntemi için bir yöntem eklemek üzere Iş mantığı katmanını (BLL) artırmak için kullanılır. `CategoriesBLL` sınıfına aşağıdaki yöntemi ekleyin:

[!code-vb[Main](uploading-files-vb/samples/sample4.vb)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>5\. Adım: Istemciden Web sunucusuna dosya yükleme

İkili veriler toplanırken, bu veriler Son Kullanıcı tarafından sağlanır. Bu bilgileri yakalamak için, kullanıcının bilgisayarından Web sunucusuna bir dosya yükleyebilmeleri gerekir. Karşıya yüklenen verilerin veri modeliyle tümleşik olması gerekir. Bu, dosyayı Web sunucusu s dosya sistemine kaydetmek ve veritabanına dosya yolu eklemek ya da ikili içerikleri doğrudan veritabanına yazmak anlamına gelebilir. Bu adımda, bir kullanıcının bilgisayarından sunucusuna dosya yüklemesine nasıl izin vereceğiz bölümüne bakacağız. Sonraki öğreticide karşıya yüklenen dosyayı veri modeliyle tümleştirmek için ilgilenmeniz gerekir.

ASP.NET 2,0 s New [FileUpload Web Control](https://msdn.microsoft.com/library/ms227677(VS.80).aspx) , kullanıcıların bilgisayarından Web sunucusuna dosya gönderebilmesi için bir mekanizma sağlar. FileUpload denetimi, `type` özniteliği dosya olarak ayarlanan bir `<input>` öğesi olarak işlenir ve bu da tarayıcıların, bir e-posta kutusu olarak bir düğme olarak görüntülenmesini sağlar. Tarayıcı düğmesine tıklamak, kullanıcının bir dosya seçmesini sağlayan bir iletişim kutusu açar. Form geri gönderildiğinde, seçili dosya içerikleri geri gönderme ile birlikte gönderilir. Sunucu tarafında, karşıya yüklenen dosyayla ilgili bilgilere dosya yükleme denetim s özellikleri aracılığıyla erişilebilir.

Dosyaları karşıya yükleme işlemini göstermek için, `BinaryData` klasöründeki `FileUpload.aspx` sayfasını açın, araç kutusundan bir dosya yükleme denetimini tasarımcı üzerine sürükleyin ve denetim s `ID` özelliğini `UploadTest`olarak ayarlayın. Daha sonra, `ID` ve `Text` özelliklerini `UploadButton` ve sırasıyla seçili dosyayı karşıya yüklemek için bir Button Web Control ekleyin. Son olarak, düğmenin altına bir etiket Web denetimi yerleştirin, `Text` özelliğini temizleyin ve `ID` özelliğini `UploadDetails`olarak ayarlayın.

[ASP.NET sayfasına dosya yükleme denetimi ekleme ![](uploading-files-vb/_static/image12.gif)](uploading-files-vb/_static/image17.png)

**Şekil 12**: ASP.NET sayfasına bir dosya yükleme denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image18.png))

Şekil 13, bir tarayıcı aracılığıyla görüntülenirken bu sayfayı gösterir. Göz at düğmesine tıklanması bir dosya seçimi iletişim kutusu gösterir ve kullanıcının bilgisayarından bir dosya seçmesini sağlar. Bir dosya seçildikten sonra, seçili dosyayı karşıya yükle düğmesine tıklamak seçili dosyanın ikili içeriğini Web sunucusuna gönderen bir geri göndermeye neden olur.

[![Kullanıcı, bilgisayarından sunucusuna yüklemek için bir dosya seçebilir](uploading-files-vb/_static/image13.gif)](uploading-files-vb/_static/image19.png)

**Şekil 13**: Kullanıcı, bilgisayarından sunucusuna yüklemek Için bir dosya seçebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](uploading-files-vb/_static/image20.png))

Geri göndermede, karşıya yüklenen dosya dosya sistemine kaydedilebilir veya ikili verileri doğrudan bir akış üzerinden çalışabilir. Bu örnekte, s `~/Brochures` bir klasör oluşturur ve karşıya yüklenen dosyayı buraya kaydeder. `Brochures` klasörünü, kök dizinin bir alt klasörü olarak siteye ekleyerek başlayın. Sonra, `UploadButton` s `Click` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](uploading-files-vb/samples/sample5.vb)]

Dosya karşıya yükleme denetimi, karşıya yüklenen verilerle çalışmaya yönelik çeşitli özellikler sağlar. Örneğin, [`HasFile` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx) , bir dosyanın Kullanıcı tarafından karşıya yüklenip yüklenmediğini belirtir, ancak [`FileBytes` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx) , karşıya yüklenen ikili verilere bir bayt dizisi olarak erişim sağlar. `Click` olay işleyicisi, bir dosyanın karşıya yüklendiğinden emin olarak başlar. Bir dosya karşıya yüklenmişse, etiket karşıya yüklenen dosyanın adını, bayt cinsinden boyutunu ve içerik türünü gösterir.

> [!NOTE]
> Kullanıcının bir dosyayı karşıya yüklemediğinden emin olmak için `HasFile` özelliğini denetleyebilir ve `False`bir uyarı görüntüleyebilir veya bunun yerine [RequiredFieldValidator denetimini](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx) kullanabilirsiniz.

Dosya karşıya yükleme `SaveAs(filePath)`, yüklenen dosyayı belirtilen *FilePath*öğesine kaydeder. *FilePath* bir *sanal* *yol* (`/Brochures/SomeFile.pdf`) yerine bir *fiziksel yol* (`C:\Websites\Brochures\SomeFile.pdf`) olmalıdır. [`Server.MapPath(virtPath)` yöntemi](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx) bir sanal yol alır ve karşılık gelen fiziksel yolunu döndürür. Burada, sanal yol `~/Brochures/fileName`, burada *filename* karşıya yüklenen dosyanın adıdır. Sanal ve fiziksel yollar hakkında daha fazla bilgi edinmek ve `Server.MapPath`kullanmak için bkz. [Server. MapPath kullanma](http://www.4guysfromrolla.com/webtech/121799-1.shtml) .

`Click` olay işleyicisini tamamladıktan sonra, sayfayı bir tarayıcıda test etmek biraz zaman ayırın. E-bul düğmesine tıklayın ve sabit sürücünüzden bir dosya seçip seçili dosyayı karşıya yükle düğmesine tıklayın. Geri gönderme, seçili dosyanın içeriğini Web sunucusuna gönderir ve daha sonra `~/Brochures` klasöre kaydedilmeden önce dosya hakkındaki bilgileri görüntüler. Dosyayı karşıya yükledikten sonra Visual Studio 'ya dönün ve Çözüm Gezgini Yenile düğmesine tıklayın. Karşıya yüklediğiniz dosyayı ~/broşürler klasörüne görmeniz gerekir!

[![EvolutionValley. jpg dosyası Web sunucusuna yüklendi](uploading-files-vb/_static/image14.gif)](uploading-files-vb/_static/image21.png)

**Şekil 14**: dosya `EvolutionValley.jpg` Web sunucusuna yüklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](uploading-files-vb/_static/image22.png))

![EvolutionValley. jpg, ~/broşürler klasörüne kaydedildi](uploading-files-vb/_static/image15.gif)

**Şekil 15**: `EvolutionValley.jpg` `~/Brochures` klasörüne kaydedildi

## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>Karşıya yüklenen dosyaları dosya sistemine kaydetme ile ilgili alt tlikler

Karşıya yükleme dosyalarını Web sunucusu s dosya sistemine kaydederken değinilmesi gereken birkaç alt parametre vardır. İlk olarak, güvenlik sorunu vardır. Dosya sistemine bir dosyayı kaydetmek için, ASP.NET sayfasının yürütüldüğü güvenlik bağlamının yazma izinlerine sahip olması gerekir. ASP.NET Development Web sunucusu, geçerli kullanıcı hesabınızın bağlamı altında çalışır. Web sunucusu olarak Microsoft s Internet Information Services (IIS) kullanıyorsanız, güvenlik bağlamı IIS sürümüne ve yapılandırmasına bağlıdır.

Dosyaları dosya sistemine kaydetmenin bir diğer zorluğu, dosyaları adlandırmanın yerini alır. Şu anda sayfamız, yüklenen dosyaların tümünü, istemci s bilgisayarındaki dosyayla aynı adı kullanarak `~/Brochures` dizine kaydeder. Kullanıcı A, adı `Brochure.pdf`bir broşür karşıya yüklediğinde, dosya `~/Brochure/Brochure.pdf`olarak kaydedilir. Ancak daha sonra Kullanıcı B, aynı dosya adına (`Brochure.pdf`) sahip olacak şekilde farklı bir broşür dosyasını karşıya yüklediğinde ne olur? Şimdi yaptığımız kodla, Kullanıcı B 'nin karşıya yüklenmesi ile ilgili bir s dosyasının üzerine yazılacak.

Dosya adı çakışmalarını çözmek için çeşitli teknikler vardır. Bir seçenek, aynı ada sahip bir dosya zaten varsa karşıya yüklemeyi yasaklayadır. Bu yaklaşım ile, B kullanıcısı, `Brochure.pdf`adlı bir dosyayı karşıya yüklemeye çalıştığında, sistem dosyalarını kaydetmez ve bunun yerine, Kullanıcı B 'nin dosyayı yeniden adlandırıp tekrar denemesini bildiren bir ileti görüntüler. Başka bir yaklaşım ise, bir [genel benzersiz tanımlayıcı (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) veya karşılık gelen veritabanı kaydı birincil anahtar sütunundan değer olabilen benzersiz bir dosya adı kullanarak dosyayı kaydetmektedir (karşıya yüklemenin veri modelindeki belirli bir satırla ilişkili olduğu varsayılırsa). Sonraki öğreticide bu seçenekleri daha ayrıntılı keşfedeceğiz.

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>Çok büyük miktarlarda Ikili veri ile Ilgili sorunlar

Bu öğreticiler, yakalanan ikili verilerin boyut olarak olduğunu varsayar. Birkaç megabayt veya daha büyük miktarda ikili veri dosyası ile çalışma, Bu öğreticilerin kapsamı ötesinde yeni zorluk sergiler. Örneğin, varsayılan olarak ASP.NET, 4 MB 'den daha fazla karşıya yüklemeyi reddeder, ancak bu, `Web.config`[`<httpRuntime>` öğesi](https://msdn.microsoft.com/library/e1f13641.aspx) aracılığıyla yapılandırılabilirler. IIS, kendi dosya yükleme boyutu sınırlamalarını da uygular. Daha fazla bilgi için bkz. [IIS karşıya yükleme dosyası boyutu](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html) . Ayrıca, büyük dosyaları karşıya yüklemek için geçen süre varsayılan 110 saniye ASP.NET bir istek için bekleyecektir. Büyük dosyalarla çalışırken ortaya çıkan bellek ve performans sorunları da vardır.

Dosya karşıya yükleme denetimi, büyük dosya yüklemeleri için pratik bir şekilde yapılır. Dosya içerikleri sunucuya gönderildiğinde, son kullanıcının karşıya yüklemesinin devam eden herhangi bir onay olmadan önce beklemesi gerekir. Bu, birkaç saniye içinde karşıya yüklenebilen küçük dosyalarla ilgilenirken çok fazla soruna neden olmaz, ancak karşıya yüklenmesi dakika süreolabilecek daha büyük dosyalarla ilgilenirken bir sorun olabilir. Büyük karşıya yüklemeleri işlemeye daha uygun olan üçüncü taraf dosya yükleme denetimleri bulunur ve bu satıcıların birçoğu, daha canlı bir kullanıcı deneyimi sunan ilerleme göstergelerini ve ActiveX karşıya yükleme yöneticilerini sağlar.

Uygulamanızın büyük dosyaları işlemesi gerekiyorsa, zorlukları dikkatle araştırmanız ve belirli gereksinimleriniz için uygun çözümler bulmanız gerekir.

## <a name="summary"></a>Özet

İkili verileri yakalamak için gereken bir uygulama oluşturmak çok sayıda zorluk sağlar. Bu öğreticide, ilk iki: ikili verileri nerede depolayacağınıza karar verme ve bir kullanıcının bir Web sayfası aracılığıyla ikili içeriği karşıya yüklemesine izin verme. Sonraki üç öğreticide, karşıya yüklenen verileri veritabanındaki bir kayıtla ilişkilendirmeyi ve metin veri alanları ile birlikte ikili verilerin nasıl görüntüleneceğini öğreneceğiz.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Büyük değer veri türlerini kullanma](https://msdn.microsoft.com/library/ms178158.aspx)
- [Dosya karşıya yükleme denetimi hızlı başlangıçlarını](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [ASP.NET 2,0 FileUpload sunucu denetimi](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [Dosya karşıya yüklemelerinin koyu tarafı](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, bir Murphy ve Bernadette Leigh. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](updating-and-deleting-existing-binary-data-cs.md)
> [İleri](displaying-binary-data-in-the-data-web-controls-vb.md)
