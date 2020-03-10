---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
title: Veri Web denetimlerinde Ikili verileri görüntüleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, bir görüntü dosyası görüntüsü ve ' Indirme ' bağlantısının f 'si dahil olmak üzere bir Web sayfasında ikili verileri sunma seçeneklerine baktık...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 9201656a-e1c2-4020-824b-18fb632d2925
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 27c901af092aa990f557750dc5d2c42ba2644c02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78604106"
---
# <a name="displaying-binary-data-in-the-data-web-controls-vb"></a>Veri Web Denetimlerinde İkili Verileri Görüntüleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_VB.exe) veya [PDF 'yi indirin](displaying-binary-data-in-the-data-web-controls-vb/_static/datatutorial55vb1.pdf)

> Bu öğreticide, bir görüntü dosyası görüntüsü ve bir PDF dosyası için ' Indirme ' bağlantısının sağlanması dahil olmak üzere, bir Web sayfasında ikili verileri sunma seçeneklerine göz atacağız.

## <a name="introduction"></a>Giriş

Önceki öğreticide, ikili verileri bir uygulama temel alınan veri modeliyle ilişkilendirmek için iki tekniği araştırıyoruz ve dosyaları bir tarayıcıdan Web sunucusu s dosya sistemine yüklemek için FileUpload denetimini kullandık. Karşıya yüklenen ikili verileri veri modeliyle ilişkilendirmeyi henüz biliyoruz. Diğer bir deyişle, bir dosya karşıya yüklenip dosya sistemine kaydedildikten sonra dosyanın bir yolu uygun veritabanı kaydında depolanmalıdır. Veriler doğrudan veritabanında depolanırsa karşıya yüklenen ikili verilerin dosya sistemine kaydedilmemelidir, ancak veritabanına eklenmesi gerekir.

Verileri veri modeliyle ilişkilendirmeden önce, ilk olarak son kullanıcıya ikili verileri nasıl sağlayabilse göz atalım. Metin verilerinin sunulması yeterince basittir, ancak ikili veriler nasıl sunulacak? Bu, ikili veri türüne bağlı olarak değişir. Görüntüler için büyük olasılıkla görüntüyü göstermek istiyoruz. PDF 'Ler, Microsoft Word belgeleri, ZIP dosyaları ve diğer ikili veri türleri için bir Indirme bağlantısı sağlanması büyük olasılıkla daha uygundur.

Bu öğreticide, GridView ve DetailsView gibi veri Web denetimlerini kullanarak, ilişkili metin verileriyle birlikte ikili verileri nasıl sunduğumuz ele alınacaktır. Bir sonraki öğreticide karşıya yüklenen bir dosyayı veritabanıyla ilişkilendirirken dikkat çekeceğiz.

## <a name="step-1-providingbrochurepathvalues"></a>1\. Adım:`BrochurePath`değerleri sağlama

`Categories` tablosundaki `Picture` sütununda, çeşitli kategori görüntülerinin ikili verileri zaten var. Özellikle, her kayıt için `Picture` sütunu, bir gralı, düşük kaliteli, 16 renkli bir bit eşlem resminin ikili içeriğini barındırır. Her kategori görüntüsü 172 piksel genişliğinde ve 120 piksel yüksekliğinde ve kabaca 11 KB kullanır. Ne kadar çok, `Picture` sütunundaki ikili içerik, görüntüyü görüntülemeden önce atılması gereken 78 baytlık bir [OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding) üst bilgisi içerir. Bu üstbilgi bilgileri, Northwind veritabanının Microsoft Access 'teki köklerine sahip olduğu için mevcuttur. Access 'te ikili veriler, bu üst bilgide bulunan OLE nesnesi veri türü kullanılarak depolanır. Şimdilik, resmi görüntülemek için bu düşük kaliteli görüntülerden üstbilgileri nasıl çıkaracağız. Gelecekteki bir öğreticide, bir kategori `Picture` sütununu güncelleştirmek için bir arabirim oluşturacağız ve OLE üst bilgilerini gereksiz OLE üstbilgileri olmadan eşdeğer JPG görüntüleriyle değiştirecek şekilde değiştirin.

Önceki öğreticide, FileUpload denetimini nasıl kullanacağınızı gördük. Bu nedenle, Web sunucusu s dosya sistemine devam edebilir ve broşür dosyaları ekleyebilirsiniz. Ancak bunu yapmak, `Categories` tablosundaki `BrochurePath` sütununu güncelleştirmez. Sonraki öğreticide bunun nasıl yapılacağını inceleyeceğiz, ancak şimdilik bu sütun için el ile değer sağlamamız gerekir.

Bu öğreticide indirme sırasında, her bir kategori için bir tane olmak üzere `~/Brochures` klasörde yedi PDF Broşürü dosyası bulacaksınız. Tüm kayıtlarda ilişkili ikili veriler olmadığı durumlarda senaryoların nasıl işleneceğini göstermek için bir deniz yiyecek broşürü ekleme işlemini tamamen atladım. `Categories` tablosunu bu değerlerle güncelleştirmek için Sunucu Gezgini `Categories` düğümüne sağ tıklayın ve tablo verilerini göster ' i seçin. Ardından, Şekil 1 ' de gösterildiği gibi, bir broşürün bulunduğu her kategori için broşür dosyalarının sanal yollarını girin. Deniz yiyecek kategorisi için bir broşür olmadığından, `BrochurePath` sütun değerlerini `NULL`olarak bırakın.

[![Kategoriler tablosu s BrochurePath sütunu için değerleri el Ile girin](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.png)

**Şekil 1**: `Categories` Table s `BrochurePath` sütununun değerlerini el ile girin ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.png))

## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>2\. Adım: GridView 'da broşürler için bir Indirme bağlantısı sağlama

`Categories` tablosu için belirtilen `BrochurePath` değerleriyle birlikte, her bir kategoriyi listeleyen bir GridView oluşturmaya, kategori broşürlerinin indirileceği bir bağlantı ile yeniden hazırlandık. 4\. adımda bu GridView öğesini ayrıca kategori s görüntüsünü görüntüleyecek şekilde genişleteceğiz.

Araç kutusundan bir GridView sürükleyip `BinaryData` klasöründeki `DisplayOrDownloadData.aspx` sayfasının tasarımcısına sürükleyin. GridView s `ID`, GridView s akıllı etiketi ile `Categories` ve yeni bir veri kaynağına bağlamayı seçin. Özellikle, `CategoriesBLL` nesne s `GetCategories()` metodunu kullanarak verileri alan `CategoriesDataSource` adlı bir ObjectDataSource 'a bağlayın.

[![CategoriesDataSource adlı yeni bir ObjectDataSource oluşturma](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.png)

**Şekil 2**: `CategoriesDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.png))

[![, ObjectDataSource 'un CategoriesBLL sınıfını kullanacak şekilde yapılandırılması](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.png)

**Şekil 3**: ObjectDataSource 'ı `CategoriesBLL` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.png))

[GetCategories () yöntemini kullanarak kategorilerin listesini almak ![](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.png)

**Şekil 4**: `GetCategories()` yöntemi kullanarak kategorilerin listesini alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`ve `BrochurePath` `DataColumn` için `Categories` GridView 'a otomatik olarak bir BoundField ekler. `GetCategories()` yöntem s sorgusu bu bilgileri almadığından `NumberOfProducts` BoundField öğesini kaldırın. Ayrıca, `CategoryID` BoundField öğesini kaldırın ve `CategoryName` ve `BrochurePath` BoundFields `HeaderText` özellikleri sırasıyla kategori ve broşür olarak yeniden adlandırın. Bu değişiklikleri yaptıktan sonra, GridView ve ObjectDataSource 'lar için bildirim temelli işaretlerinizin aşağıdaki gibi görünmesi gerekir:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample1.aspx)]

Bu sayfayı bir tarayıcı üzerinden görüntüleyin (bkz. Şekil 5). Sekiz kategorinin her biri listelenir. `BrochurePath` değerleri olan yedi kategori, ilgili BoundField içinde `BrochurePath` değer olarak gösterilir. `BrochurePath`için `NULL` bir değere sahip olan deniz yiyecek, boş bir hücre görüntüler.

[![her kategorinin adı, açıklaması ve BrochurePath değeri listelenir](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.png)

**Şekil 5**: her kategori adı, açıklama ve `BrochurePath` değeri listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.png))

`BrochurePath` sütununun metnini görüntülemek yerine, broşür için bir bağlantı oluşturmak istiyoruz. Bunu gerçekleştirmek için, `BrochurePath` BoundField öğesini kaldırın ve bir HyperLinkField ile değiştirin. Yeni HyperLinkField `HeaderText` özelliğini broşür, `Text` özelliğini View broşürü ve `DataNavigateUrlFields` özelliğini `BrochurePath`olarak ayarlayın.

![BrochurePath için bir Hyperlinkalanı ekleme](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.gif)

**Şekil 6**: `BrochurePath` Için bir hyperlinkalanı ekleme

Bu, Şekil 7 ' nin gösterdiği şekilde GridView 'a bir bağlantı sütunu ekler. Bir görünüm broşürü bağlantısına tıklamak, PDF 'YI doğrudan tarayıcıda görüntüler veya bir PDF okuyucunun yüklü olup olmadığına ve tarayıcı ayarlarına bağlı olarak kullanıcıdan dosyayı indirmesini ister.

[![bir kategori broşürü, görünüm broşürü bağlantısına tıklanarak görüntülenebilir](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.png)

**Şekil 7**: bir kategori broşürü görünüm broşürü bağlantısına tıklanarak görüntülenebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.png))

[![Broşür PDF 'nin görüntülendiği kategori](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.png)

**Şekil 8**: KATEGORI broşürü PDF görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image14.png))

## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>Broşür olmadan kategoriler için görünüm broşürü metnini gizleme

Şekil 7 ' de gösterildiği gibi, `BrochurePath` Hyperlinkalanı, `BrochurePath`için`NULL` olmayan bir değer olup olmamasına bakılmaksızın, tüm kayıtlar için `Text` özellik değerini (görünüm broşürü) görüntüler. Kuşkusuz, `BrochurePath` `NULL`ise, bağlantı yalnızca metin olarak görüntülenir. Bu durumda, deniz yiyecek kategorisinde olduğu gibi (bkz. Şekil 7 ' ye geri başvurabilirsiniz). Metin görünümü broşürü gösterilmesi yerine, bu kategorilerin `BrochurePath` bir değer olmadan olması iyi olabilir. bu şekilde, hiçbir geçiş kullanılamaz.

Bu davranışı sağlamak için, içeriği `BrochurePath` değerine göre uygun çıktıyı gösteren bir sayfa yöntemine yapılan bir çağrı yoluyla oluşturulan bir TemplateField kullandık. İlk olarak bu biçimlendirme tekniğinin ardından [GridView denetim öğreticisindeki TemplateFields kullanarak](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) geri araştırıyoruz.

`BrochurePath` Hyperlinkalanını seçip sütunları Düzenle iletişim kutusunda bu alanı bir TemplateField 'a Dönüştür bağlantısına tıklayarak Hyperlinkalanını bir TemplateField 'a açın.

![HyperLinkField 'ı TemplateField 'a Dönüştür](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.gif)

**Şekil 9**: Hyperlinkalanını TemplateField 'a Dönüştür

Bu, `NavigateUrl` özelliği `BrochurePath` değerine bağlanan köprü Web denetimi içeren `ItemTemplate` bir TemplateField oluşturur. Bu biçimlendirmeyi, `BrochurePath`değerini geçirerek Yöntem `GenerateBrochureLink`çağrısıyla değiştirin:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample2.aspx)]

Daha sonra, bir `String` döndüren ve giriş parametresi olarak bir `Object` kabul eden `GenerateBrochureLink` ASP.NET Page for Code-Behind sınıfında bir `Protected` yöntemi oluşturun.

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample3.vb)]

Bu yöntem, geçirilen `Object` değerinin bir veritabanı `NULL` olup olmadığını belirler ve varsa kategorinin bir broşür olmadığını belirten bir ileti döndürür. Aksi takdirde, `BrochurePath` bir değer varsa, bu, bir köprüde görüntülenir. `BrochurePath` değerin [`ResolveUrl(url)` yöntemine](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx)geçtiğini unutmayın. Bu yöntem, `~` karakterini uygun sanal yol ile değiştirerek, geçilen *URL 'yi*çözer. Örneğin, uygulamanın kökü `/Tutorial55`, `ResolveUrl("~/Brochures/Meats.pdf")` `/Tutorial55/Brochures/Meat.pdf`döndürür.

Şekil 10 ' da bu değişiklikler uygulandıktan sonra sayfa gösterilmektedir. Deniz yiyecek kategorisi s `BrochurePath` alanının artık, kullanılabilir bir broşür olmadığını gösterir.

[bir broşür olmadan bu kategoriler için kullanılabilir bir broşür ![metin görüntülenir](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image15.png)

**Şekil 10**: bir broşür olmadan bu kategoriler için kullanılabilecek bir broşür görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image16.png))

## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>3\. Adım: Kategori s resmini göstermek için Web sayfası ekleme

Bir Kullanıcı bir ASP.NET sayfasını ziyaret ettiğinde, ASP.NET sayfa s HTML 'sini alırlar. Alınan HTML yalnızca metindir ve herhangi bir ikili veri içermez. Görüntüler, ses dosyaları, Macromedia Flash uygulamaları, katıştırılmış Windows Media Player videoları gibi ek ikili veriler, Web sunucusunda ayrı kaynaklar olarak mevcuttur. HTML, bu dosyalara başvurular içerir, ancak dosyaların gerçek içeriğini içermez.

Örneğin, HTML 'de `<img>` öğesi, görüntü dosyasına şöyle işaret eden `src` özniteliğiyle bir resme başvurmak için kullanılır:

[!code-html[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample4.html)]

Bir tarayıcı bu HTML aldığında, Web sunucusuna, daha sonra tarayıcıda görüntülenen ikili içeriğini almak için başka bir istek sağlar. Aynı kavram tüm ikili veriler için de geçerlidir. 2\. adımda, sayfa s HTML işaretlemesi kapsamında, broşür tarayıcıya gönderilmedi. Bunun yerine, işlenen HTML, tıklandığında, tarayıcıda PDF belgesini doğrudan istemesine neden olan köprüleri sağladı.

Kullanıcıların veritabanında bulunan ikili verileri indirmesini veya indirmesine izin vermek için, verileri döndüren ayrı bir Web sayfası oluşturmanız gerekir. Uygulamamız için, kategori s resmine doğrudan veritabanında depolanan yalnızca bir ikili veri alanı bulunur. Bu nedenle, çağrıldığında belirli bir kategorinin görüntü verilerini döndüren bir sayfa gerekir.

`DisplayCategoryPicture.aspx`adlı `BinaryData` klasöre yeni bir ASP.NET sayfası ekleyin. Bunu yaparken, ana sayfa seç onay kutusunu işaretlenmemiş olarak bırakın. Bu sayfa, QueryString içinde bir `CategoryID` değeri bekler ve bu kategori s `Picture` sütununun ikili verilerini döndürür. Bu sayfa ikili veriler döndürdüğünden başka hiçbir şey olmadığından, HTML bölümünde herhangi bir biçimlendirme gerekmez. Bu nedenle sol alt köşedeki kaynak sekmesine tıklayın ve `<%@ Page %>` yönergesi hariç tüm sayfa işaretlemesini kaldırın. Diğer bir deyişle, `DisplayCategoryPicture.aspx` s bildirime dayalı biçimlendirme tek bir satırdan oluşmalıdır:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample5.aspx)]

`<%@ Page %>` yönergesinde `MasterPageFile` özniteliği görürseniz, kaldırın.

Sayfa s arka plan kod sınıfında, `Page_Load` olay işleyicisine aşağıdaki kodu ekleyin:

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample6.vb)]

Bu kod, `CategoryID` QueryString değerini `categoryID`adlı bir değişkende okuyarak başlar. Ardından, resim verileri `CategoriesBLL` sınıf s `GetCategoryWithBinaryDataByCategoryID(categoryID)` yöntemine yapılan bir çağrı aracılığıyla alınır. Bu veriler `Response.BinaryWrite(data)` yöntemi kullanılarak istemciye döndürülür, ancak bu çağrılmadan önce, `Picture` sütun değeri s OLE üstbilgisinin kaldırılması gerekir. Bu, `Picture` sütunundaki miktardan daha az 78 karakter tutacak `strippedImageData` adlı bir `Byte` dizisi oluşturularak gerçekleştirilir. [`Array.Copy` yöntemi](https://msdn.microsoft.com/library/z50k9bft.aspx) , verileri 78 konumundan başlayarak `strippedImageData`kadar `category.Picture` kopyalamak için kullanılır.

`Response.ContentType` özelliği, tarayıcının nasıl işleneceğini bilmesi için döndürülmekte olan içeriğin [MIME türünü](http://en.wikipedia.org/wiki/MIME) belirtir. `Categories` tablosu `Picture` sütunu bir bit eşlem görüntüsü olduğundan, bit eşlem MIME türü burada kullanılır (görüntü/bmp). MIME türünü atlarsanız, çoğu tarayıcı görüntüyü doğru şekilde görüntüler çünkü bu, türü görüntü dosyası ikili verilerinin içeriğine göre çıkarslar. Bununla birlikte, mümkün olduğunda MIME türünü dahil etmek için bu. [MIME medya türlerinin](http://www.iana.org/assignments/media-types/)tamamını listelemek Için [Internet atanmış numaralar yetkilisi s Web sitesine](http://www.iana.org/) bakın.

Bu sayfa oluşturulduktan sonra, `DisplayCategoryPicture.aspx?CategoryID=categoryID`ziyaret ederek belirli bir kategorinin resmi görüntülenebilir. Şekil 11 ' `DisplayCategoryPicture.aspx?CategoryID=1`den görüntülenebilen Içgörüler kategorisi s resmini gösterir.

[![Içecek kategorisi resmi görüntülenir](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image17.png)

**Şekil 11**: meşrus kategorisi resmi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image18.png))

`DisplayCategoryPicture.aspx?CategoryID=categoryID`ziyaret edildiğinde, ' System. DBNull ' türündeki nesneyi ' System. Byte [] ' türüne, bu soruna neden olabilecek iki şey olduğunu okuyan bir özel durum alırsınız. İlk olarak, `Categories` tablo `Picture` sütunu `NULL` değerlere izin verir. Ancak `DisplayCategoryPicture.aspx` sayfası,`NULL` olmayan bir değer olduğunu varsayar. `CategoriesDataTable` `Picture` özelliğine bir `NULL` değeri varsa doğrudan erişilemez. `Picture` sütunu için `NULL` değerlere izin vermek istiyorsanız, aşağıdaki koşulu dahil etmek isteyebilirsiniz:

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample7.vb)]

Yukarıdaki kod, bir resim olmadan bu kategoriler için görüntülenmesini istediğiniz `Images` klasöründe `NoPictureAvailable.gif` adlı bir görüntü dosyası olduğunu varsayar.

Bu özel durum Ayrıca, ad-hoc SQL deyimlerini kullanıyorsanız ve TableAdapter s ana sorgusu için Sihirbazı yeniden çalıştırırsanız meydana gelebilen `CategoriesTableAdapter` s `GetCategoryWithBinaryDataByCategoryID` yöntemi s `SELECT` deyimi ana sorgu s sütun listesine geri döndürülemezse da bu durum oluşabilir. `GetCategoryWithBinaryDataByCategoryID` yöntemi `SELECT` deyimin `Picture` sütununu hala içerdiğinden emin olun.

> [!NOTE]
> `DisplayCategoryPicture.aspx` her ziyaret edildiğinde veritabanına erişilir ve belirtilen kategori s resim verileri döndürülür. Kullanıcının en son görüntülemesinden sonra kategori s resmi değiştirilmediyse, bu, boşa harcanacak bir çalışmadır. Neyse ki, HTTP *koşullu*olarak izin verir. Koşullu GET ile HTTP isteğini yapan istemci, istemcinin bu kaynağı Web sunucusundan en son aldığı tarihi ve saati sağlayan bir [`If-Modified-Since` http üstbilgisi](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) üzerinden gönderir. İçerik bu tarihten bu yana değiştirilmediyse, Web sunucusu [değiştirilmemiş bir durum kodu (304)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) ile yanıt verebilir ve istenen kaynak içeriğini geri göndermeye devam edebilir. Kısacası, bu teknik, istemcinin son erişiminizden bu yana değiştirilmediyse, Web sunucusunun bir kaynağın içeriğini geri göndermesini sizi maliyetinden kurtarır.

Ancak, bu davranışı uygulamak için, `Picture` sütununun en son ne zaman güncelleştirildiği ve `If-Modified-Since` üst bilgisini denetlemek için kodun yanı sıra `Categories` tabloya bir `PictureLastModified` sütunu eklemenizi gerektirir. `If-Modified-Since` üstbilgisi ve koşullu GET iş akışı hakkında daha fazla bilgi için bkz. [RSS bilgisayar korsanları Için http koşullu Get](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers) ve [ASP.NET sayfasında http istekleri gerçekleştirmeye yönelik daha ayrıntılı bir bakış](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx).

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>4\. Adım: Kategori resimlerini GridView 'da görüntüleme

Artık belirli bir kategori resmini görüntüleyen bir Web sayfası olduğuna göre, bunu [Görüntü Web denetimi](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx) veya `DisplayCategoryPicture.aspx?CategoryID=categoryID`işaret eden bir HTML `<img>` öğesi kullanarak görüntüleriz. URL 'SI veritabanı verilerine göre belirlenen görüntüler GridView veya DetailsView içinde ImageField kullanılarak görüntülenebilir. ImageField, HyperLinkField s `DataNavigateUrlFields` ve `DataNavigateUrlFormatString` özellikleri gibi çalışan `DataImageUrlField` ve `DataImageUrlFormatString` özellikleri içerir.

Her bir kategorinin resmini göstermek için bir ImageField ekleyerek `DisplayOrDownloadData.aspx` `Categories` GridView 'ı daha fazla inceleyelim. Imagealanını eklemek ve `DataImageUrlField` ve `DataImageUrlFormatString` özelliklerini sırasıyla `CategoryID` ve `DisplayCategoryPicture.aspx?CategoryID={0}`olarak ayarlamanız yeterlidir. Bu, {0} GridView Row s `CategoryID` değeri ile değiştirildiği `DisplayCategoryPicture.aspx?CategoryID={0}``src` özniteliği başvurduğu `<img>` bir öğeyi oluşturan bir GridView sütunu oluşturur.

![GridView 'a ImageField ekleyin](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.gif)

**Şekil 12**: GridView 'A ImageField ekleyin

ImageField eklendikten sonra, GridView s bildirime dayalı sözdiziminizin aşağıdaki gibi görünmesi gerekir:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample8.aspx)]

Bu sayfayı bir tarayıcı aracılığıyla görüntülemek için bir dakikanızı ayırın. Her kaydın kategori için nasıl bir resim içerdiğini göz önünde görürsünüz.

[Her satır için kategori s Picture ![görüntülenir](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image19.png)

**Şekil 13**: Kategori s resmi her satır için görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-binary-data-in-the-data-web-controls-vb/_static/image20.png))

## <a name="summary"></a>Özet

Bu öğreticide ikili verileri nasıl sunduğumuz incelendi. Verilerin nasıl sunulduğu, verilerin türüne bağlıdır. PDF Broşürü dosyaları için kullanıcıya bir görünüm broşürü bağlantısı sunuluyor, tıklandığı zaman kullanıcıyı doğrudan PDF dosyasına sağlıyoruz. Kategori s resmi için, ilk olarak veritabanından ikili verileri almak ve döndürmek için bir sayfa oluşturduk ve sonra bu sayfayı bir GridView içinde her bir kategorinin resmini görüntüleyecek şekilde kullandınız.

İkili verilerin nasıl görüntüleneceğini incelediğimiz için, ikili verilerle veritabanına yönelik ekleme, güncelleştirme ve silme işlemlerinin nasıl gerçekleştirileceğini inceliyoruz. Sonraki öğreticide karşıya yüklenen bir dosyayı karşılık gelen veritabanı kaydıyla ilişkilendirme bölümüne bakacağız. Bu öğreticide, var olan ikili verilerin nasıl güncelleştireceğiz ve ilişkili kayıt kaldırıldığında ikili verilerin nasıl silineceği de görüyoruz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, bir Murphy ve Davve Gardner. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](uploading-files-vb.md)
> [İleri](including-a-file-upload-option-when-adding-a-new-record-vb.md)
