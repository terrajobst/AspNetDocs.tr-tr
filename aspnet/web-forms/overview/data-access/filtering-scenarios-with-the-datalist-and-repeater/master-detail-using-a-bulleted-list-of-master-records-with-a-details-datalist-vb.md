---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
title: Ayrıntılar DataList 'i ile madde Işaretli ana kayıt listesi kullanan ana/ayrıntı (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, önceki öğreticinin iki sayfalı ana/ayrıntı raporunu tek bir sayfa halinde sıkıştıracağız. Bu, t üzerinde kategori adlarının madde işaretli bir listesini gösterir...
ms.author: riande
ms.date: 10/17/2006
ms.assetid: ee20742f-6fb7-49a0-a009-058fe363aacb
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 81d72c666925e89729464e7ea696bde8d323e277
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78605961"
---
# <a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb"></a>Bir Ayrıntılar DataList’i ile Madde İşaretli Ana Kayıt Listesi Kullanan Ana/Ayrıntı (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_VB.exe) veya [PDF 'yi indirin](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/datatutorial35vb1.pdf)

> Bu öğreticide, önceki öğreticinin iki sayfalı ana/ayrıntı raporunu, ekranın sol tarafındaki kategori adlarının madde işaretli bir listesini ve ekranın sağ tarafında seçilen kategorinin ürünlerini gösteren tek bir sayfada sıkıştıracağız.

## <a name="introduction"></a>Giriş

[Yukarıdaki öğreticide](master-detail-filtering-acess-two-pages-datalist-vb.md) , ana/ayrıntı raporunu iki sayfada nasıl ayıracağız. Ana sayfada, madde işaretli kategori listesini işlemek için bir yineleyici denetimi kullandık. Her kategori adı, tıklandığı zaman, kullanıcıyı, iki sütunlu bir DataList 'in seçili kategoriye ait bu ürünleri gösteren ayrıntılar sayfasına götürebileceği bir köprüdür.

Bu öğreticide, iki sayfalı öğreticiyi tek bir sayfada sıkıştıracağız ve her kategori adı bir LinkButton olarak işlenilerek ekranın sol tarafındaki kategori adlarından oluşan bir liste listesi gösteriliyor. Bir geri gönderinin bulunduğu kategori adı bağlantı düğmelerinden birine tıkladığınızda seçili kategori ürünlerini ekranın sağ tarafında iki sütunlu bir DataList 'e bağlar. Her bir kategorinin adını görüntülemenin yanı sıra, soldaki Yineleyici belirli bir kategori için kaç tane toplam ürünün olduğunu gösterir (bkz. Şekil 1).

[![kategori adı ve toplam ürün sayısı solda görüntülenir](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image1.png)

**Şekil 1**: Kategori s adı ve toplam ürün sayısı solda görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image3.png))

## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>1\. Adım: bir yineleyici ekranın sol bölümünde görüntüleme

Bu öğreticide, seçili kategori ürünlerinin solunda sol tarafta yer alan kategori listesi bulunması gerekir. Bir Web sayfasındaki içerikler standart HTML öğeleri paragraf etiketleri, bölünemez boşluklar, `<table>` s, vb. veya basamaklı stil sayfası (CSS) teknikleri kullanılarak konumlandırılmış olabilir. Bu nedenle tüm öğreticilerimiz, konumlandırma için CSS tekniklerini kullandı. Ana [sayfalarda ve site gezinti](../introduction/master-pages-and-site-navigation-vb.md) öğreticisindeki ana sayfamızda Gezinti Kullanıcı arabirimini oluşturduğumuzda, gezinti listesi ve ana içerik için tam piksel sapmasını belirten *mutlak konumlandırmayı*kullandık. Alternatif olarak, CSS, bir öğeyi diğerinin sağına veya soluna *kayan*bir şekilde konumlandırmak için kullanılabilir. Seçilen kategorinin sol tarafında, DataList 'in sol tarafında bulunan Repeater ' ın solunda görünmesini sağlayabilirsiniz.

`DataListRepeaterFiltering` klasöründen `CategoriesAndProducts.aspx` sayfasını açın ve bir yineleyici ve DataList sayfasına ekleyin. Yineleyicisi `ID`, `CategoryProducts`için `Categories` ve DataList 'leri olarak ayarlayın. Kaynak görünümüne gidin ve yineleyici ve DataList denetimlerini kendi `<div>` öğelerine yerleştirin. Diğer bir deyişle, Repeater öğesini önce bir `<div>` öğesi ve sonra DataList ' i doğrudan Repeater ' dan sonra kendi `<div>` öğesi içine alın. Bu noktadaki biçimlerinizin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample1.aspx)]

Yineleyicisi 'nin DataList 'in soluna kayan olması için `float` CSS style özniteliğini kullanmanız gerekir, örneğin:

[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample2.html)]

`float: left;` ikinci öğenin solundaki ilk `<div>` öğeyi float. `width` ve `padding-right` ayarları, ilk `<div>` s `width` ve `<div>` öğesi içeriği ve sağ kenar boşluğu arasına ne kadar doldurma ekleneceğini gösterir. CSS 'deki kayan öğeler hakkında daha fazla bilgi için [Floatutorial](http://css.maxdesign.com.au/floatutorial/)bakın.

Stil ayarını doğrudan ilk `<p>` öğesi `style` özniteliğiyle belirtmek yerine, bunun yerine `FloatLeft`adlı `Styles.css` yeni bir CSS sınıfı oluşturun:

[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample3.css)]

Ardından `<div>` `<div class="FloatLeft">`ile değiştirebilirsiniz.

CSS sınıfını ekledikten ve `CategoriesAndProducts.aspx` sayfasında işaretlemeyi yapılandırdıktan sonra tasarımcıya gidin. DataList 'in sol tarafında kayan olan yineleyicisi görmeniz gerekir (Şu anda, henüz veri kaynaklarını veya şablonlarını yapılandırmamız daha sonra yalnızca gri kutular olarak görünür olsa da).

[Yineleyicisi 'nin DataList 'in soluna doğru ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image4.png)

**Şekil 2**: Repeater, DataList 'in soluna eklenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image6.png))

## <a name="step-2-determining-the-number-of-products-for-each-category"></a>2\. Adım: her bir kategorinin ürün sayısını belirleme

Yineleyicileri ve DataList 'i çevreleyen biçimlendirme tamamlandıktan sonra, kategori verilerini Yineleyici denetimine bağlamaya hazırız. Ancak, Şekil 1 ' deki kategori madde listesi, her bir kategorinin adına ek olarak kategori ile ilişkili ürünlerin sayısını da görüntülemesi gereken her bir kategori için de görünür. Bu bilgilere erişmek için şunlardan birini yapabilirsiniz:

- **Bu bilgileri ASP.NET Page s arka plan kod sınıfından öğrenin.** Belirli bir *`categoryID`* verildiğinde, `ProductsBLL` sınıf s `GetProductsByCategoryID(categoryID)` metodunu çağırarak ilişkili ürünlerin sayısını belirleyebiliriz. Bu yöntem, `Count` özelliği, belirtilen *`categoryID`* ürünlerin sayısı olan `ProductsRow` kaç tane olduğunu belirten `ProductsDataTable` nesnesini döndürür. Yineleyici için, Repeater ile bağlantılı her bir kategori için `ProductsBLL` sınıf s `GetProductsByCategoryID(categoryID)` yöntemini çağıran ve çıktıda sayısını içeren bir `ItemDataBound` olay işleyicisi oluşturarız.
- **Türü belirtilmiş veri kümesindeki `CategoriesDataTable` bir `NumberOfProducts` sütunu içerecek şekilde güncelleştirin.** Daha sonra bu bilgileri eklemek için `CategoriesDataTable` `GetCategories()` yöntemini güncelleştirebilir veya `GetCategories()` olduğu gibi bırakabilir ve `GetCategoriesAndNumberOfProducts()`adlı yeni bir `CategoriesDataTable` yöntemi oluşturabilirsiniz.

Bu tekniklerin her ikisini de keşfedelim. Veri erişim katmanını güncelleştirmek zorunda olduğumuz için ilk yaklaşım uygulamanız daha basittir; Bununla birlikte, veritabanıyla daha fazla iletişim gerektirir. `ItemDataBound` olay işleyicisindeki `ProductsBLL` Class s `GetProductsByCategoryID(categoryID)` yöntemine yapılan çağrı, Repeater ' da görünen her bir kategori için ek bir veritabanı çağrısı ekler. Bu teknikle, n *+ 1 veritabanı çağrısı vardır;* burada *n* , yineleyici içinde görüntülenen kategorilerin sayısıdır. İkinci yaklaşımla, ürün sayısı `CategoriesBLL` sınıf s `GetCategories()` (veya `GetCategoriesAndNumberOfProducts()`) yönteminden her bir kategori hakkında bilgi ile döndürülür ve bu sayede veritabanına bir yolculuğa neden olur.

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>Itemveriye bağlı olay Işleyicisindeki ürünlerin sayısını belirleme

Yineleyici s `ItemDataBound` olay işleyicisindeki her bir kategorinin ürün sayısını belirlemek, var olan veri erişim katmanımız üzerinde herhangi bir değişiklik yapılmasını gerektirmez. Tüm değişiklikler doğrudan `CategoriesAndProducts.aspx` sayfası içinde yapılabilir. Yineleyici s akıllı etiketi aracılığıyla `CategoriesDataSource` adlı yeni bir ObjectDataSource ekleyerek başlayın. Sonra, `CategoriesBLL` sınıf s `GetCategories()` yönteminden verilerini alması için `CategoriesDataSource` ObjectDataSource 'u yapılandırın.

[![, CategoriesBLL sınıfı s GetCategories () yöntemini kullanmak için ObjectDataSource 'ı yapılandırma](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image7.png)

**Şekil 3**: `CategoriesBLL` sınıf s `GetCategories()` metodunu ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image9.png)) kullanmak üzere ObjectDataSource 'ı yapılandırın

`Categories` Yineleyici içindeki her öğenin tıklatılabilir olması gerekir ve tıklandığında, `CategoryProducts` DataList 'in seçili kategori için bu ürünleri görüntülemesine neden olur. Bu, her kategoriye bir köprü yapılarak, aynı sayfaya (`CategoriesAndProducts.aspx`) bağlanarak ve önceki öğreticide gördüğdiğimiz gibi QueryString aracılığıyla `CategoryID` geçirerek gerçekleştirilebilir. Bu yaklaşımın avantajı, belirli bir kategorinin ürünlerini görüntüleyen bir sayfanın, bir arama altyapısı tarafından yer işareti eklenmiş ve dizine alınmış olması olabilir.

Alternatif olarak, her bir kategoriyi Bu öğreticide kullanacağımız yaklaşım olan bir LinkButton yapabiliriz. LinkButton Kullanıcı tarayıcısında köprü olarak işlenir, ancak tıklandığı zaman geri gönderme yapılır; geri gönderme sırasında, DataList s ObjectDataSource 'un seçili kategoriye ait ürünleri görüntülemesi için yenilenmesi gerekir. Bu öğreticide, bir köprü kullanmak LinkButton kullanmaktan daha mantıklı olur; Ancak, LinkButton kullanmanın daha avantajlı olduğu başka senaryolar da olabilir. Köprü yaklaşımı Bu örnek için ideal olacaktır, bunun yerine LinkButton öğesini kullanmayı göz atalım. Göreceğiniz gibi, LinkButton 'ın kullanılması, bir köprüyle sonuçlanmayacak bazı güçlükleri ortaya koymaktadır. Bu nedenle, bu öğreticide bir LinkButton kullanılması bu zorlukları vurgulayacak ve köprü yerine LinkButton kullanmak isteyebileceğiniz senaryolar için çözüm sağlamaya yardımcı olur.

> [!NOTE]
> Bu öğreticiyi, LinkButton yerine bir HyperLink denetimi veya `<a>` öğesi kullanarak tekrarlamanız önerilir.

Aşağıdaki biçimlendirme yineleyici ve ObjectDataSource için bildirime dayalı sözdizimini gösterir. Yineleyicisi 'nin şablonlarının her öğe için LinkButton olarak bir madde işaretli liste işlemesini unutmayın:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample4.aspx)]

> [!NOTE]
> Bu öğreticide, Repeater 'ın görünüm durumunun etkin olması gerekir (`EnableViewState="False"` yineleyicisi 'nin bildirime dayalı sözdiziminden atlandığını aklınızda). 3\. adımda, DataList s ObjectDataSource s `SelectParameters` koleksiyonunu güncelleştirilebilmemiz için Yineleyici s `ItemCommand` olayı için bir olay işleyicisi oluşturacağız. Yineleyiciye `ItemCommand`, ancak görünüm durumu devre dışıysa tetiklenmeyecektir. Bir yineleyici s `ItemCommand` olayının tetiklenmesi için neden görünüm durumunun etkin olması gerektiğini öğrenmek için ASP.NET sorusunun ve [çözümünün](http://scottonwriting.net/sowBlog/posts/1268.aspx) [bir bölümünü](http://scottonwriting.net/sowblog/posts/1263.aspx) inceleyin.

`ViewCategory` `ID` özellik değerine sahip LinkButton, `Text` özellik kümesine sahip değil. Kategori adını yalnızca göstermek istiyorduk, metin özelliğini bildirimli olarak, veri bağlama söz dizimi ile şöyle ayarlayacağız:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample5.aspx)]

Ancak, hem *kategori adını hem de söz* konusu kategoriye ait ürünlerin sayısını göstermek istiyoruz. Bu bilgiler, aşağıdaki kodda gösterildiği gibi, `ProductBLL` sınıf s `GetCategoriesByProductID(categoryID)` yöntemine çağrı yaparak ve sonuçta elde edilen `ProductsDataTable`kaç kayıt döndürüldüğünü belirleyerek Yineleyici s `ItemDataBound` olay işleyicisinden elde edilebilir:

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample6.vb)]

Bir veri öğesiyle (`ItemType` `Item` veya `AlternatingItem`) çalıştık ve sonra geçerli `RepeaterItem`zaten bağlanan `CategoriesRow` örneğine başvuru yaptığımız olduğundan emin olarak başladık. Daha sonra, `ProductsBLL` sınıfının bir örneğini oluşturarak, `GetCategoriesByProductID(categoryID)` metodunu çağırarak ve `Count` özelliği kullanılarak döndürülen kayıt sayısını belirleyerek bu kategoriye yönelik ürünlerin sayısını belirliyoruz. Son olarak, ItemTemplate 'teki `ViewCategory` LinkButton, `Text` özelliği *CategoryName* (*numberofproductsincategory*) olarak ayarlanır ve burada *numberofproductsincategory* sıfır ondalık basamakla bir sayı olarak biçimlendirilir.

> [!NOTE]
> Alternatif olarak, kategori s `CategoryName` ve `CategoryID` değerlerini kabul eden ve kategori içindeki ürünlerin sayısıyla birleştirilmiş `CategoryName` döndüren (`GetCategoriesByProductID(categoryID)` yöntemi çağırarak belirlendiği şekilde) bir *biçimlendirme işlevi* ekledik. Bu tür biçimlendirme işlevinin sonuçları, `ItemDataBound` olay işleyicisi gereksinimini değiştiren LinkButton s Text özelliğine bildirimli olarak atanabilir. Biçimlendirme işlevlerini kullanma hakkında daha fazla bilgi için [, GridView denetimindeki TemplateFields kullanma](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) veya veri öğreticilerine [göre DataList ve Repeater 'ı biçimlendirme](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md) bölümüne bakın.

Bu olay işleyicisini ekledikten sonra sayfayı bir tarayıcı ile test etmek için bir dakikanızı ayırın. Her kategorinin bir madde işaretli listede nasıl listelendiğine, kategori adı ve kategori ile ilişkili ürün sayısının görüntülenmesine bakın (bkz. Şekil 4).

[Her kategorinin adı ve ürün sayısı ![görüntülenir](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image10.png)

**Şekil 4**: her kategori adı ve ürün sayısı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image12.png))

## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>`CategoriesDataTable`ve`CategoriesTableAdapter`her bir kategorinin ürün sayısını Içerecek şekilde güncelleştiriliyor

Yineleyicisi 'ne bağladığından her bir kategorinin ürün sayısını belirlemek yerine, bu bilgileri yerel olarak dahil etmek üzere veri erişim katmanındaki `CategoriesDataTable` ve `CategoriesTableAdapter` ayarlayarak bu işlemi kolaylaştırabilir. Bunu başarmak için, ilişkili ürünlerin sayısını tutmak üzere `CategoriesDataTable` yeni bir sütun eklememiz gerekir. DataTable 'a yeni bir sütun eklemek için, yazılan veri kümesini (`App_Code\DAL\Northwind.xsd`) açın, değiştirilecek DataTable öğesine sağ tıklayın ve Ekle/sütun ' u seçin. `CategoriesDataTable` yeni bir sütun ekleyin (bkz. Şekil 5).

[Kategorilerverikaynağına yeni bir sütun eklemek ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image13.png)

**Şekil 5**: `CategoriesDataSource` yeni bir sütun ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image15.png))

Bu, yalnızca farklı bir ada yazarak değiştirebileceğiniz `Column1`adlı yeni bir sütun ekler. Bu yeni sütunu `NumberOfProducts`olarak yeniden adlandırın. Daha sonra, bu sütun özelliklerini yapılandırmamız gerekir. Yeni sütununa tıklayın ve Özellikler penceresi gidin. Şekil 6 ' da gösterildiği gibi, sütun s `DataType` özelliğini `System.String` `System.Int32` olarak değiştirin ve `ReadOnly` özelliğini `True`olarak ayarlayın.

![Yeni sütunun DataType ve ReadOnly özelliklerini ayarla](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image16.png)

**Şekil 6**: yeni sütunun `DataType` ve `ReadOnly` özelliklerini ayarlayın

`CategoriesDataTable` artık bir `NumberOfProducts` sütununa sahip olsa da, değeri karşılık gelen herhangi bir TableAdapter s sorgusunun hiçbirinde ayarlı değildir. Kategori bilgilerinin alındığı her seferinde bu bilgilerin döndürülmesini istiyorsanız bu bilgileri döndürmek için `GetCategories()` yöntemini güncelleştirebiliriz. Ancak, nadir örneklerde (yalnızca bu öğreticide olduğu gibi) kategorilerin ilişkili ürün sayısını almak için, `GetCategories()` olduğu gibi bırakabilir ve bu bilgileri döndüren yeni bir yöntem oluşturabilirsiniz. `GetCategoriesAndNumberOfProducts()`adlı yeni bir yöntem oluşturarak bu ikinci yaklaşımı kullanalım.

Bu yeni `GetCategoriesAndNumberOfProducts()` yöntemi eklemek için, `CategoriesTableAdapter` sağ tıklayıp yeni sorgu ' yı seçin. Bu, önceki öğreticilerde çok sayıda kez kullandığımız TableAdapter sorgu Yapılandırma Sihirbazı 'nı getirir. Bu yöntem için, sorgunun satırları döndüren bir geçici SQL ifadesini kullandığını belirterek sihirbazı başlatın.

[![geçici bir SQL Ifadesini kullanarak yöntem oluşturma](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image17.png)

**Şekil 7**: GEÇICI bir SQL Ifadesini kullanarak yöntemi oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image19.png))

[SQL deyimindeki satırları döndüren ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image20.png)

**Şekil 8**: SQL Ifadesinin satırları döndürmesi ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image22.png))

Sonraki sihirbaz ekranı, sorgunun kullanması için bizi ister. Her bir kategorinin `CategoryID`, `CategoryName`ve `Description` alanlarının yanı sıra kategori ile ilişkili ürünlerin sayısını döndürmek için aşağıdaki `SELECT` ifadesini kullanın:

[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample7.sql)]

[Kullanılacak sorguyu belirtmek ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image23.png)

**Şekil 9**: kullanılacak sorguyu belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image25.png))

Kategorisiyle ilişkili ürün sayısını hesaplayan alt sorgunun `NumberOfProducts`olarak diğer adı olduğunu unutmayın. Bu adlandırma eşleşmesi, bu alt sorgunun döndürdüğü değerin `CategoriesDataTable` s `NumberOfProducts` sütunuyla ilişkilendirilmesine neden olur.

Bu sorguyu girdikten sonra, son adım yeni yöntemin adını seçmekte. DataTable Fill ve sırasıyla bir DataTable desenleri döndüren `FillWithNumberOfProducts` ve `GetCategoriesAndNumberOfProducts` kullanın.

[Yeni TableAdapter s yöntemleri FillWithNumberOfProducts ve GetCategoriesAndNumberOfProducts ![adı](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image26.png)

**Şekil 10**: yeni TableAdapter s yöntemlerini `FillWithNumberOfProducts` ve `GetCategoriesAndNumberOfProducts` adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image28.png))

Bu noktada, veri erişim katmanı kategori başına ürün sayısını içerecek şekilde genişletilmiştir. Tüm sunum katmanımız, farklı bir Iş mantığı katmanı aracılığıyla DAL için tüm çağrıları yönlendirdiğinden, `CategoriesBLL` sınıfına karşılık gelen bir `GetCategoriesAndNumberOfProducts` yöntemi eklememiz gerekir:

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample8.vb)]

DAL ve BLL ile, bu verileri `CategoriesAndProducts.aspx``Categories` yineleyicisi 'ne bağlamayı yeniden hazırlarız! Zaten Yineleyici için `ItemDataBound` olay Işleyicisi bölümünde ürün sayısını belirleme için bir ObjectDataSource oluşturduysanız, bu ObjectDataSource 'u silin ve yineleyici s `DataSourceID` özellik ayarını kaldırın; Ayrıca, ASP.NET arka plan kod sınıfında `Handles Categories.OnItemDataBound` sözdizimini kaldırarak olay işleyicisindeki yineleyicinin `ItemDataBound` olayını kaldırır.

Yineleyici, özgün durumuna geri döndüğünüzde, yineleyici s akıllı etiketi aracılığıyla `CategoriesDataSource` adlı yeni bir ObjectDataSource ekleyin. ObjectDataSource 'u `CategoriesBLL` sınıfını kullanacak şekilde yapılandırın, ancak bunun yerine `GetCategories()` metodunu kullanmasını sağlamak yerine `GetCategoriesAndNumberOfProducts()` kullanın (bkz. Şekil 11).

[![, GetCategoriesAndNumberOfProducts metodunu kullanmak için ObjectDataSource 'u yapılandırma](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image29.png)

**Şekil 11**: `GetCategoriesAndNumberOfProducts` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image31.png))

Daha sonra, LinkButton s `Text` özelliğinin veri bağlama söz dizimi kullanılarak bildirimli olarak atanması ve hem `CategoryName` hem de `NumberOfProducts` veri alanlarını içermesi için `ItemTemplate` güncelleştirin. Yineleyici ve `CategoriesDataSource` ObjectDataSource için tüm bildirim temelli biçimlendirme şu şekilde yapılır:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample9.aspx)]

DAL, bir `NumberOfProducts` sütunu içerecek şekilde güncelleştirilerek işlenen çıktı, `ItemDataBound` olay işleyicisi yaklaşımını (kategori adlarını ve ürün sayısını gösteren yineleyicinin ekran görüntüsünü görmek için yeniden) ile aynıdır.

## <a name="step-3-displaying-the-selected-category-s-products"></a>3\. Adım: Seçili Kategori ürünlerini görüntüleme

Bu noktada, kategorilerin listesini her bir kategorideki ürünlerin sayısıyla birlikte görüntüleyen `Categories` Yineleyici vardır. Yineleyicisi, tıklandığı her bir kategori için bir LinkButton kullanır ve bu aşamada `CategoryProducts` DataList 'te seçili kategori için bu ürünleri görüntülemesi gerekir.

Bizimle ilgili bir zorluk, DataList 'in seçili kategori için yalnızca bu ürünleri görüntülemesini sağlar. [Ayrıntılar DetailsView Ile seçilebilir bir ana GridView kullanan ana/ayrıntı](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) için, seçili satır s ayrıntıları aynı sayfada bir DetailsView 'da görüntülenirken, satırları seçilebilecek bir GridView oluşturmayı gördünüz. GridView s ObjectDataSource, `ProductsBLL` s `GetProducts()` yöntemini kullanan tüm ürünlerle ilgili bilgileri geri döndürdü. DetailsView, `GetProductsByProductID(productID)` yöntemi kullanılarak seçili ürünle ilgili bilgiler almıştır. *`productID`* parametre değeri, GridView s `SelectedValue` özelliğinin değeriyle ilişkilendirerek bildirimli olarak sağlandı. Ne yazık ki, yineleyicisi bir `SelectedValue` özelliğine sahip değildir ve bir parametre kaynağı olarak görev alamaz.

> [!NOTE]
> Bu, bir yineleyici içinde LinkButton kullanılırken görünen güçlüklerden biridir. Bunun yerine QueryString aracılığıyla `CategoryID` geçirmek için bir köprü kullandık, bu QueryString alanını parametre değeri için kaynak olarak kullanabiliriz.

Yineleyicisi için `SelectedValue` özelliğinin bulunmaması konusunda endişelenmemiz için önce DataList 'i bir ObjectDataSource 'a bağlasa ve `ItemTemplate`belirteceğiz.

DataList s akıllı etiketinden, `CategoryProductsDataSource` adlı yeni bir ObjectDataSource eklemeyi ve `ProductsBLL` sınıf s `GetProductsByCategoryID(categoryID)` metodunu kullanacak şekilde yapılandırmayı tercih edin. Bu öğreticideki DataList bir salt okuma arabirimi sağladığından, ekleme, GÜNCELLEŞTIRME ve SILME sekmelerinden (hiçbiri) açılan listeleri ayarlamayı ücretsiz olarak hissetmeniz yeterlidir.

[![, ProductsBLL Class s Getproductsbycategoryıd (CategoryID) metodunu kullanacak şekilde yapılandırma](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image32.png)

**Şekil 12**: `ProductsBLL` Class s `GetProductsByCategoryID(categoryID)` metodunu kullanacak şekilde ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image34.png))

`GetProductsByCategoryID(categoryID)` yöntemi bir giriş parametresi ( *`categoryID`* ) beklediği Için, veri kaynağını yapılandırma Sihirbazı, parametre kaynağını belirtmemizi sağlar. Kategorilerin bir GridView veya DataList içinde listelenmesi gerekiyordu. parametre kaynağı açılır listesini, veri Web denetiminin `ID` kontrol etmek ve ControlID olarak ayarlayacağız. Ancak, yineleyicisi bir `SelectedValue` özelliğine sahip olmadığından parametre kaynağı olarak kullanılamaz. Onay ederseniz, ControlID açılır listesinin yalnızca bir denetim `ID``CategoryProducts`, DataList 'in `ID` içerdiğini göreceksiniz.

Şimdilik, parametre kaynağı açılır listesini hiçbiri olarak ayarlayın. Yineleyicisi 'nde bir Category LinkButton tıklandığında bu parametre değerini programlı olarak atamaya başlayacağız.

[CategoryID parametresi için bir parametre kaynağı belirtmeyin ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image35.png)

**Şekil 13**: *`categoryID`* parametresi Için bir parametre kaynağı belirtmeyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image37.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio, DataList s `ItemTemplate`otomatik olarak oluşturur. Bu varsayılan `ItemTemplate`, önceki öğreticide kullandığımız şablonla değiştirin; Ayrıca, DataList s `RepeatColumns` özelliğini 2 olarak ayarlayın. Bu değişiklikleri yaptıktan sonra, DataList 'niz ve ilişkili ObjectDataSource için bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample10.aspx)]

Şu anda `CategoryProductsDataSource` ObjectDataSource *`categoryID`* parametresi hiçbir zaman ayarlanmamaktadır, bu nedenle sayfa görüntülenirken hiçbir ürün gösterilmez. Bu parametre değerinin, yineleyici içindeki tıklanan kategorinin `CategoryID` göre ayarlanmış olması gerekir. Bu iki zorluk sergiler: ilk olarak, yineleyici `ItemTemplate` bir LinkButton 'ın ne zaman tıklandığını nasıl belirliyoruz; İkinci olarak, LinkButton 'a tıklandığı karşılık gelen kategorinin `CategoryID` nasıl belirleyebiliriz?

Düğme ve ImageButton denetimleri gibi LinkButton, bir `Click` olayına ve bir [`Command` olayına](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx)sahiptir. `Click` olay, LinkButton öğesine tıklandığına işaret etmek üzere tasarlanmıştır. Ancak, LinkButton ' ın tıklandığını belirten ek olarak, olay işleyicisine bazı ek bilgiler iletmemiz gerekir. Bu durumda, LinkButton s [`CommandName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx) ve [`CommandArgument`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx) özelliklerine bu ek bilgiler atanabilir. Daha sonra LinkButton tıklandığında, `Command` olayı başlatılır (`Click` olayı yerine) ve olay işleyicisi `CommandName` ve `CommandArgument` özelliklerinin değerlerini iletilir.

Yineleyicisi içindeki bir şablon içinden `Command` bir olay tetiklendiğinde, Repeater s [`ItemCommand` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx) ateşlenir ve tıklanan LinkButton (veya Button veya ImageButton) `CommandName` ve `CommandArgument` değerleri geçirilir. Bu nedenle, yineleyici içindeki bir kategori LinkButton 'ın ne zaman tıklandığını anlamak için aşağıdakileri yapmanız gerekir:

1. Repeater s `ItemTemplate` LinkButton 'ın `CommandName` özelliğini bir değere ayarlayın (ListProducts kullandım). Bu `CommandName` değerini ayarlayarak LinkButton s `Command` olayı LinkButton tıklandığında ateşlenir.
2. LinkButton s `CommandArgument` özelliğini geçerli öğe s `CategoryID`değerine ayarlayın.
3. Yineleyici s `ItemCommand` olayı için bir olay işleyicisi oluşturun. Olay işleyicisinde `CategoryProductsDataSource` ObjectDataSource s `CategoryID` parametresini, geçirilen `CommandArgument`değerine ayarlayın.

Yineleyici kategoriler için aşağıdaki `ItemTemplate` biçimlendirmesi 1 ve 2. adımları uygular. `CommandArgument` değere veri bağlama söz dizimi kullanılarak `CategoryID` veri öğesi için nasıl atandığını aklınızda kullanın:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample11.aspx)]

`ItemCommand` olay işleyicisi oluştururken, yineleyici içinde *herhangi* bir düğme, LinkButton veya ImageButton tarafından oluşturulan *herhangi bir* `Command` olayı `ItemCommand` olayının tetiklenmesine neden olacağı için, her zaman ilk önce gelen `CommandName` değerini denetleyemedi. Şu anda yalnızca bir LinkButton 'a Şu anda sahipsiniz (veya ekibimizin başka bir geliştirici), tıklandığı zaman aynı `ItemCommand` olay işleyicisini oluşturan Yineleyici için ek düğme Web denetimleri ekleyebilirler. Bu nedenle, `CommandName` özelliğini her zaman denetlediğinizden ve yalnızca beklenen değerle eşleşiyorsa programlama mantığınızla devam eden en iyi seçenektir.

Geçirilen `CommandName` değerinin ListProducts 'a eşit olduğundan emin olduktan sonra olay işleyicisi, `CategoryProductsDataSource` ObjectDataSource s `CategoryID` parametresini geçirilen `CommandArgument`değerine atar. `SelectParameters` ObjectDataSource 'ta bu değişiklik otomatik olarak DataList 'in kendisini veri kaynağına yeniden bağlamasını ve yeni seçilen kategorinin ürünlerini göstermesini sağlar.

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample12.vb)]

Bu eklemeler sayesinde öğreticimiz tamamlanmıştır! Bir tarayıcıda test etmek için bir dakikanızı ayırın. Şekil 14, sayfayı ilk ziyaret eden ekranı gösterir. Bir kategori henüz seçilememiştir, hiçbir ürün gösterilmez. Bir kategoriye tıkladığınızda (örneğin,), ürün kategorisindeki bu ürünleri iki sütunlu görünümde görüntüler (bkz. Şekil 15).

[![sayfa Ilk ziyaret edildiğinde hiçbir ürün gösterilmez](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image38.png)

**Şekil 14**: sayfa Ilk ziyaret edildiğinde hiçbir ürün gösterilmez ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image40.png))

[Üretim kategorisine tıklanması ![, doğru eşleşen ürünleri listeler](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image41.png)

**Şekil 15**: üretim kategorisine tıkladığınızda sağdaki eşleşen ürünler listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image43.png))

## <a name="summary"></a>Özet

Bu öğreticide ve önceki bir adımda gördüğümüz ana/ayrıntı raporları iki sayfada dağıtılabilir veya bir tane üzerinde birleştirilebilir. Bununla birlikte, tek bir sayfada ana/ayrıntı raporunu görüntülemek, sayfada ana ve ayrıntı kayıtlarının ne kadar en iyi şekilde yerleşmekte zorluk gösterilmesini sağlar. *Ayrıntı DetailsView Ile seçilebilir bir ana GridView kullanan ana/ayrıntı* bölümünde, Ayrıntılar kayıtları ana kayıtların üzerinde görüntülenir; Bu öğreticide, ana kayıtları ayrıntıların sol tarafında yüzer olması için CSS tekniklerini kullandık.

Ana/ayrıntı raporlarının yanı sıra, her bir kategori ile ilişkili ürün sayısını ve bir bağlantı düğmesine (veya düğmeye veya ImageButton) bir yineleyici içinden tıklandığı zaman sunucu tarafı mantığın nasıl alınacağını keşfettik.

Bu öğretici, DataList ve Repeater ile ana/ayrıntı raporlarının incelemesini tamamlar. Sonraki öğreticilerimiz, DataList denetimine nasıl özellik ekleneceğini ve bu yeteneklerin nasıl ekleneceğini gösterir.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- CSS ile kayan CSS öğeleri hakkında [Floatutorial](http://css.maxdesign.com.au/floatutorial/) bir öğretici
- CSS ile öğeleri konumlandırma hakkında daha fazla bilgi [konumlandırma](http://www.brainjar.com/css/positioning/)
- `<table>` s ve diğer HTML öğelerini konumlandırma için kullanarak [HTML Ile Içerik yerleştirme](http://www.w3schools.com/html/html_layout.asp)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni, Zack Jones idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Öncekini](master-detail-filtering-acess-two-pages-datalist-vb.md)
