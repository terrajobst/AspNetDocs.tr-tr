---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
title: DropDownList Ile ana/ayrıntı filtreleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, bir DropDownList denetimindeki ana kayıtları ve bir GridView 'da seçilen liste öğesinin ayrıntılarını göreceksiniz.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: ea44717e-ab2e-46cd-a692-e4a9c0de194c
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 62cd296a3f36e1779666a6b5db15b0ce2488d0e4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640224"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>Bir DropDownList ile Ana/Ayrıntı Filtreleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_7_VB.exe) veya [PDF 'yi indirin](master-detail-filtering-with-a-dropdownlist-vb/_static/datatutorial07vb1.pdf)

> Bu öğreticide, bir DropDownList denetimindeki ana kayıtları ve bir GridView 'da seçilen liste öğesinin ayrıntılarını göreceksiniz.

## <a name="introduction"></a>Giriş

Ortak bir rapor türü, raporun ilk "ana" kayıt kümesini göstererek başladığı *ana/ayrıntı raporlarıdır*. Kullanıcı daha sonra Ana kayıtlardan birinin detayına gidebilir ve bu sayede ana kaydın "ayrıntılarını" görüntülüyor olabilir. Ana/ayrıntı raporları, tüm kategorileri gösteren bir rapor ve sonra bir kullanıcının belirli bir kategoriyi seçmesini ve ilişkili ürünlerini görüntülemesini sağlamak gibi bir-çok ilişkiyi görselleştirmeye yönelik ideal bir seçimdir. Ayrıca, ana/ayrıntı raporları, özellikle "geniş" tablolardan (çok sütun içeren) ayrıntılı bilgileri görüntülemek için yararlıdır. Örneğin, ana/ayrıntı raporunun "ana" düzeyi, veritabanındaki ürünlerin yalnızca ürün adını ve birim fiyatını gösterebilir ve belirli bir üründe ayrıntıya gitme ek ürün alanlarını (kategori, tedarikçi, birim başına miktar vb.) gösterebilir.

Ana/ayrıntı raporunun uygulanbileceği birçok yol vardır. Bu ve sonraki üç öğreticilerde, çeşitli ana/ayrıntı raporlarına bakacağız. Bu öğreticide, bir [DropDownList denetimindeki](https://msdn.microsoft.com/library/dtx91y0z.aspx) ana kayıtları ve bir GridView 'da seçilen liste öğesinin ayrıntılarını göreceksiniz. Özellikle, Bu öğreticinin ana/ayrıntı raporu, kategori ve ürün bilgilerini listeler.

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>1\. Adım: bir DropDownList içindeki kategorileri görüntüleme

Ana/ayrıntı raporumuz, seçilen liste öğesinin ürünlerini bir GridView 'daki sayfada daha aşağı görüntülenecek şekilde bir DropDownList içindeki kategorileri listeleyecektir. İlk görevinin önünde ve sonra, kategorilerin bir DropDownList içinde gösterilmesi gerekir. `Filtering` klasöründeki `FilterByDropDownList.aspx` sayfasını açın, araç kutusu 'ndaki bir DropDownList 'e sayfanın tasarımcısına sürükleyin ve `ID` özelliğini `Categories`olarak ayarlayın. Sonra, DropDownList 'in akıllı etiketindeki veri kaynağı Seç bağlantısına tıklayın. Bu, veri kaynağı Yapılandırma Sihirbazı 'nı görüntüler.

[DropDownList 'in veri kaynağını belirtmek ![](master-detail-filtering-with-a-dropdownlist-vb/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image1.png)

**Şekil 1**: DropDownList 'In veri kaynağını belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image3.png))

`CategoriesBLL` sınıfının `GetCategories()` yöntemini çağıran `CategoriesDataSource` adlı yeni bir ObjectDataSource eklemeyi seçin.

[![CategoriesDataSource adlı yeni bir ObjectDataSource ekleyin](master-detail-filtering-with-a-dropdownlist-vb/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image4.png)

**Şekil 2**: `CategoriesDataSource` adlı yeni bir ObjectDataSource ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image6.png))

[Kategorilerbll sınıfını kullanmayı ![seçin](master-detail-filtering-with-a-dropdownlist-vb/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image7.png)

**Şekil 3**: `CategoriesBLL` sınıfını kullanmayı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image9.png))

[![, GetCategories () yöntemini kullanmak için ObjectDataSource 'ı yapılandırma](master-detail-filtering-with-a-dropdownlist-vb/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image10.png)

**Şekil 4**: `GetCategories()` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image12.png))

ObjectDataSource yapılandırıldıktan sonra yine de, DropDownList 'de hangi veri kaynağı alanının gösterileceğini ve hangi birinin liste öğesi için değer olarak ilişkilendirilmesi gerektiğini belirtmemiz gerekir. `CategoryName` alanı görüntüleme ve her liste öğesi için değer olarak `CategoryID`.

[DropDownList 'In CategoryName alanını görüntülemesi ve değer olarak CategoryID 'yi kullanması ![](master-detail-filtering-with-a-dropdownlist-vb/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image13.png)

**Şekil 5**: DropDownList 'In `CategoryName` alanı göstermesini ve değer olarak `CategoryID` kullanmasına[izin vermek (tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image15.png))

Bu noktada, `Categories` tablodaki kayıtlarla doldurulmuş bir DropDownList denetimine sahip olduğumuz (hepsi yaklaşık altı saniye içinde gerçekleştirilir). Şekil 6 ' da bir tarayıcıdan görüntülendiklerinde ilerleme durumunu gösterir.

[aşağı açılan liste ![geçerli Kategoriler](master-detail-filtering-with-a-dropdownlist-vb/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image16.png)

**Şekil 6**: bir açılan listede geçerli Kategoriler listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image18.png))

## <a name="step-2-adding-the-products-gridview"></a>2\. Adım: ürünü ekleme GridView

Ana/ayrıntı raporumuzdaki ilgili son adım, seçili kategoriyle ilişkili ürünleri listelerimize göre belirlenir. Bunu gerçekleştirmek için, sayfaya bir GridView ekleyin ve `productsDataSource`adlı yeni bir ObjectDataSource oluşturun. `productsDataSource` denetiminin verilerini `ProductsBLL` sınıfının `GetProductsByCategoryID(categoryID)` yönteminden Cull yapın.

[Getproductsbycategoryıd (CategoryID) yöntemini ![seçin](master-detail-filtering-with-a-dropdownlist-vb/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image19.png)

**Şekil 7**: `GetProductsByCategoryID(categoryID)` yöntemini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image21.png))

Bu yöntemi seçtikten sonra, ObjectDataSource Sihirbazı yöntemin *`categoryID`* parametresine ilişkin değeri ister. Seçili `categories` DropDownList öğesinin değerini kullanmak için parametre kaynağını denetim ve ControlID `Categories`olarak ayarlayın.

[![CategoryID parametresini DropDownList kategorisinin değerine ayarlayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image22.png)

**Şekil 8**: *`categoryID`* parametresini `Categories` DropDownList değeri olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image24.png))

Bir tarayıcıda ilerleme durumunu kontrol etmek için bir dakikanızı ayırın. Sayfayı ilk ziyaret edildiğinde, bu ürünler seçili kategoriye (alkoller) ait (Şekil 9 ' da gösterildiği gibi) görüntülenir, ancak DropDownList 'in değiştirilmesi verileri güncelleştirmez. Bunun nedeni, GridView 'in güncelleştirilmesi için bir geri gönderme oluşması gerekir. Bunu gerçekleştirmek için iki seçeneğiniz vardır (hiçbiri hiçbir kod yazmak zorunda değildir):

- **Kategori DropDownList**[AutoPostBack özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**true olarak ayarlayın.** (Bunu, DropDownList 'in akıllı etiketinde AutoPostBack seçeneğini etkinleştir seçeneğini işaretleyerek gerçekleştirebilirsiniz.) Bu, DropDownList 'in seçili öğesi Kullanıcı tarafından değiştirildiğinde bir geri gönderme tetikleyecektir. Bu nedenle, Kullanıcı DropDownList 'den yeni bir kategori seçtiğinde geri gönderme, yeni seçilen kategorinin ürünleriyle güncelleştirilir. (Bu öğreticide kullandığım yaklaşım budur.)
- **DropDownList 'in yanına bir düğme web denetimi ekleyin.** `Text` özelliğini Yenile veya benzer bir şekilde ayarlayın. Bu yaklaşımda, kullanıcının yeni bir kategori seçip düğmesine tıklamalıdır. Düğmeye tıkladığınızda geri göndermeye neden olur ve GridView, seçilen kategorinin bu ürünlerini listelemek için güncelleştirilecek.

Şekil 9 ve 10, işlem içindeki ana/ayrıntı raporunu gösterir.

[Sayfa Ilk ziyaret edildiğinde ![, beden Içecek ürünleri görüntülenir](master-detail-filtering-with-a-dropdownlist-vb/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image25.png)

**Şekil 9**: sayfayı ilk ziyaret edildiğinde, Beiçecek ürünleri görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image27.png))

[Yeni bir ürünün seçilmesi ![(üretim) otomatik olarak bir geri göndermeye neden olur, GridView güncelleştiriliyor](master-detail-filtering-with-a-dropdownlist-vb/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image28.png)

**Şekil 10**: yeni bir ürünün seçilmesi (üretim) otomatik olarak bir geri göndermeye neden olur, GridView güncelleştiriliyor ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image30.png))

## <a name="adding-a----choose-a-category----list-item"></a>"--Kategori seçme--" liste öğesi ekleme

`FilterByDropDownList.aspx` sayfası ilk kez ziyaret edildiğinde, kategori DropDownList 'in ilk liste öğesi (alkolu) varsayılan olarak seçilidir ve GridView 'daki Iiçecek ürünlerini gösterir. İlk kategorinin ürünlerini göstermek yerine, "--kategori seçin--" gibi bir DropDownList öğesi seçilmelidir.

DropDownList 'e yeni bir liste öğesi eklemek için Özellikler penceresi gidin ve `Items` özelliğindeki üç noktaya tıklayın. `Text` "--kategori seçin--" ve `Value` `-1`yeni bir liste öğesi ekleyin.

[![ekleyin--Kategori seçin--liste öğesi](master-detail-filtering-with-a-dropdownlist-vb/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image31.png)

**Şekil 11**: Ekle--Kategori seçin--liste öğesi ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image33.png))

Alternatif olarak, aşağıdaki işaretlemeyi DropDownList öğesine ekleyerek liste öğesini ekleyebilirsiniz:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample1.aspx)]

Ayrıca, Kategoriler denetimin DropDownList 'e bağlandığı, `AppendDataBoundItems` doğru değilse, el ile eklenen liste öğelerinin üzerine yazabiledikleri için DropDownList denetiminin `AppendDataBoundItems` true olarak ayarlanmaları gerekir.

![AppendDataBoundItems özelliğini true olarak ayarlayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image34.png)

**Şekil 12**: `AppendDataBoundItems` özelliğini true olarak ayarlayın

Bu değişikliklerden sonra, ilk olarak "--kategori seçin--" seçeneği seçilidir ve hiçbir ürün gösterilmez.

[Ilk sayfa yükleme ![hiçbir ürün gösterilmez](master-detail-filtering-with-a-dropdownlist-vb/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image35.png)

**Şekil 13**: Ilk sayfa yükleme sayfasında hiçbir ürün gösterilmez ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image37.png))

"--Kategori Seç--" liste öğesi seçili olduğu için hiçbir ürünün görüntülenmediği nedeni, değeri `-1` ve veritabanında `-1``CategoryID` bir ürün yok. İstediğiniz davranış bu ise, bu noktada işiniz istenir! Bununla birlikte, "--Kategori Seç--" liste öğesi seçili olduğunda kategorilerin *Tümünü* göstermek istiyorsanız, `ProductsBLL` sınıfına geri dönün ve `GetProductsByCategoryID(categoryID)` yöntemini, geçirilen *`categoryID`* parametresi sıfırdan küçükse `GetProducts()` yöntemini çağırır şekilde özelleştirin:

[!code-vb[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample2.vb)]

Burada kullanılan teknik, [bildirim temelli parametreler](../basic-reporting/declarative-parameters-cs.md) öğreticisinde tüm tedarikçileri geri göstermek için kullandığımız yaklaşıma benzer, ancak bu örnekte, tüm kayıtların `Nothing`aksine alınması gerektiğini göstermek için bir `-1` değeri kullanıyoruz. Bunun nedeni, `GetProductsByCategoryID(categoryID)` yönteminin *`categoryID`* parametresinin, bir dize giriş parametresine geçirdiğimiz bildirim temelli parametreler öğreticisinde iletilen tamsayı değeri olmasını bekler.

Şekil 14 ' te, "--kategori seçin--" seçeneği belirlendiğinde `FilterByDropDownList.aspx` ekran görüntüsü gösterilir. Burada, tüm ürünler varsayılan olarak görüntülenir ve Kullanıcı, belirli bir kategoriyi seçerek ekranı daraltabilirler.

[Tüm ürünlerin ![artık varsayılan olarak listelenmiştir](master-detail-filtering-with-a-dropdownlist-vb/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image38.png)

**Şekil 14**: tüm ürünler artık varsayılan olarak listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image40.png))

## <a name="summary"></a>Özet

Hiyerarşik olarak ilgili verileri görüntülerken, genellikle kullanıcının hiyerarşinin en üstündeki verileri kullanarak başlayabileceği ana/ayrıntı raporlarını kullanarak verileri sunmak ve ayrıntılarda ayrıntıya inmek için yardımcı olur. Bu öğreticide, seçilen kategorinin ürünlerini gösteren basit bir ana/ayrıntı raporu oluşturmayı inceledik. Bu, kategorilerin listesi için bir DropDownList ve seçilen kategoriye ait ürünler için bir GridView kullanılarak gerçekleştirildi.

[Sonraki öğreticide](master-detail-filtering-with-two-dropdownlists-vb.md) , Iki Dropdownlists kullanarak DropDownList arabirimini bir adım daha devam eteceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
> [İleri](master-detail-filtering-with-two-dropdownlists-vb.md)
