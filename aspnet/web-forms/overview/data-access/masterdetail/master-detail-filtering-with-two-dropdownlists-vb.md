---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
title: Iki DropDownLists Ile ana/ayrıntı filtreleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğretici, istenen üst ve alt üst öğeyi seçmek için iki DropDownList denetimi kullanarak üçüncü bir katman eklemek üzere ana/ayrıntı ilişkisini genişletir.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11ae4f64-01ba-4823-95f4-a2fe1f84f7d7
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
msc.type: authoredcontent
ms.openlocfilehash: 166d6a7664a326361dc2a3f115eddb988cd39d20
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528499"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-vb"></a>İki DropDownList ile Ana/Ayrıntı Filtreleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_8_VB.exe) veya [PDF 'yi indirin](master-detail-filtering-with-two-dropdownlists-vb/_static/datatutorial08vb1.pdf)

> Bu öğretici, istenen üst ve alt üst kayıtları seçmek için iki DropDownList denetimi kullanarak üçüncü bir katman eklemek üzere ana/ayrıntı ilişkisini genişletir.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](master-detail-filtering-with-a-dropdownlist-vb.md) , Kategoriler ve seçili kategoriye ait ürünleri gösteren bir GridView ile doldurulmuş tek bir DropDownList kullanarak basit bir ana/Ayrıntılar raporunun nasıl görüntüleneceğini inceledik. Bu rapor stili, bire çok ilişkisine sahip kayıtları görüntülerken iyi çalışır ve birden çok çoktan çoğa ilişki içeren senaryolarda kolayca çalışmak üzere genişletilebilir. Örneğin, bir sipariş giriş sisteminin müşterilere, siparişlere ve sipariş satırı öğelerine karşılık gelen tabloları vardır. Belirli bir müşterinin birden çok öğeden oluşan her sipariş ile birden çok siparişi olabilir. Bu tür veriler kullanıcıya iki DropDownLists ve bir GridView ile sunulabilir. İlk DropDownList, veritabanındaki her müşteri için bir liste öğesine, ikinci birinin içerikleri seçili müşteri tarafından yerleştirilmiş olan emirlerle aynı olacaktır. GridView, seçili siparişten satır öğelerini listeler.

Northwind veritabanı `Customers`, `Orders`ve `Order Details` tablolarında kurallı müşteri/sipariş/sipariş ayrıntıları bilgilerini içerirken, bu tablolar mimarimizde yakalanmaz. Nonetheless, hala iki bağımlı DropDownLists kullanmayı göstermeye devam edebilir. İlk DropDownList, kategorileri ve seçili kategoriye ait olan ürünleri listeler. Daha sonra bir DetailsView seçili ürünün ayrıntılarını listeler.

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>Adım 1: kategorileri oluşturma ve doldurma DropDownList

İlk hedefiniz, kategorileri listeleyen DropDownList 'i eklemektir. Bu adımlar, önceki öğreticide ayrıntılı olarak incelendi, ancak tamamlanma açısından burada özetlenmiştir.

`Filtering` klasöründeki `MasterDetailsDetails.aspx` sayfasını açın, sayfaya bir DropDownList ekleyin, `ID` özelliğini `Categories`olarak ayarlayın ve ardından akıllı etiketinde veri kaynağını Yapılandır bağlantısına tıklayın. Veri kaynağı Yapılandırma Sihirbazı ' ndan yeni bir veri kaynağı eklemeyi seçin.

[DropDownList için yeni bir veri kaynağı eklemek ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image1.png)

**Şekil 1**: DropDownList için yeni bir veri kaynağı ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image3.png))

Yeni veri kaynağı doğal olarak bir ObjectDataSource olmalıdır. Bu yeni ObjectDataSource `CategoriesDataSource` adlandırın ve `CategoriesBLL` nesnenin `GetCategories()` metodunu çağırmasını sağlayabilirsiniz.

[Kategorilerbll sınıfını kullanmayı ![seçin](master-detail-filtering-with-two-dropdownlists-vb/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image4.png)

**Şekil 2**: `CategoriesBLL` sınıfını kullanmayı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image6.png))

[![, GetCategories () yöntemini kullanmak için ObjectDataSource 'ı yapılandırma](master-detail-filtering-with-two-dropdownlists-vb/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image7.png)

**Şekil 3**: `GetCategories()` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image9.png))

ObjectDataSource yapılandırıldıktan sonra hala `Categories` DropDownList içinde hangi veri kaynağı alanının görüntüleneceğini ve hangilerinin liste öğesi için değer olarak yapılandırılması gerektiğini belirtmemiz gerekir. `CategoryName` alanını görüntüleme ve `CategoryID` her liste öğesi için değer olarak ayarlayın.

[DropDownList 'In CategoryName alanını görüntülemesi ve değer olarak CategoryID 'yi kullanması ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image10.png)

**Şekil 4**: DropDownList 'In `CategoryName` alanı göstermesini ve değer olarak `CategoryID` kullanmasına[izin vermek (tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image12.png))

Bu noktada, `Categories` tablosundaki kayıtlarla doldurulmuş bir DropDownList Control (`Categories`) vardır. Kullanıcı DropDownList 'den yeni bir kategori seçtiğinde adım 2 ' de oluşturacağımız ürün DropDownList 'sini yenilemek için bir geri gönderme işleminin gerçekleşmesini istiyoruz. Bu nedenle, `categories` DropDownList 'in akıllı etiketindeki AutoPostBack 'ı etkinleştir seçeneğini işaretleyin.

[![DropDownList için AutoPostBack 'ı etkinleştirin](master-detail-filtering-with-two-dropdownlists-vb/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image13.png)

**Şekil 5**: `Categories` DropDownList Için AutoPostBack 'ı etkinleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image15.png))

## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>2\. Adım: seçili kategorinin ürünlerini Ikinci bir DropDownList içinde görüntüleme

`Categories` DropDownList tamamlandıysa, sonraki adımınız seçili kategoriye ait bir ürün DropDownList 'ı görüntülemektir. Bunu gerçekleştirmek için, `ProductsByCategory`adlı sayfaya başka bir DropDownList ekleyin. `Categories` DropDownList 'de olduğu gibi, `ProductsByCategoryDataSource`adlı `ProductsByCategory` DropDownList için yeni bir ObjectDataSource oluşturun.

[![ProductsByCategory DropDownList için yeni bir veri kaynağı ekleme](master-detail-filtering-with-two-dropdownlists-vb/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image16.png)

**Şekil 6**: `ProductsByCategory` DropDownList için yeni bir veri kaynağı ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image18.png))

[![ProductsByCategoryDataSource adlı yeni bir ObjectDataSource oluşturma](master-detail-filtering-with-two-dropdownlists-vb/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image19.png)

**Şekil 7**: `ProductsByCategoryDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image21.png))

`ProductsByCategory` DropDownList 'in yalnızca seçili kategoriye ait olan ürünleri görüntülemesi gerektiğinden, ObjectDataSource `ProductsBLL` nesnesinden `GetProductsByCategoryID(categoryID)` yöntemini çağırsın.

[ProductsBLL sınıfını kullanmayı ![seçin](master-detail-filtering-with-two-dropdownlists-vb/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image22.png)

**Şekil 8**: `ProductsBLL` sınıfını kullanmayı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image24.png))

[ObjectDataSource 'ı Getproductsbycategoryıd (CategoryID) yöntemini kullanacak şekilde yapılandırma ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image25.png)

**Şekil 9**: `GetProductsByCategoryID(categoryID)` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image27.png))

Sihirbazın son adımında *`categoryID`* parametresinin değerini belirtmemiz gerekir. Bu parametreyi `Categories` DropDownList öğesinden seçili öğeye atayın.

[![kategorisinden CategoryID parametre değerini çekin](master-detail-filtering-with-two-dropdownlists-vb/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image28.png)

**Şekil 10**: `Categories` DropDownList öğesinden *`categoryID`* parametre değerini çekme ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image30.png))

Yapılandırılmış ObjectDataSource ile, her şey, DropDownList öğelerinin görüntüleme ve değeri için hangi veri kaynağı alanlarının kullanılacağını belirtmektir. `ProductName` alanını görüntüleyin ve `ProductID` alanını değer olarak kullanın.

[DropDownList 'in ListItems değerinin metin ve değer özellikleri için kullanılan veri kaynağı alanlarını belirtin ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image31.png)

**Şekil 11**: DropDownList 'in `ListItem` s ' `Text` ve `Value` özellikleri Için kullanılan veri kaynağı alanlarını belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image33.png))

ObjectDataSource ve `ProductsByCategory` DropDownList 'in yapılandırıldığı sayfada iki DropDownList görüntülenir: İkincisi, seçili kategoriye ait olan ürünleri listelediğinden, ilki tüm kategorileri listelecektir. Kullanıcı ilk DropDownList 'den yeni bir kategori seçtiğinde, geri gönderme yapılır ve ikinci DropDownList, yeni seçilen kategoriye ait olan ürünleri gösterecek şekilde yeniden bağlanacaktır. Şekil 12 ve 13 bir tarayıcıdan görüntülendiğinde `MasterDetailsDetails.aspx` eylem içinde göster.

[Sayfayı Ilk ziyaret eden ![, Içecek kategorisi seçilir](master-detail-filtering-with-two-dropdownlists-vb/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image34.png)

**Şekil 12**: sayfayı ilk ziyaret edildiğinde, Içecek kategorisi seçilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image36.png))

[Farklı bir kategori seçmek ![, yeni kategorinin ürünlerini görüntüler](master-detail-filtering-with-two-dropdownlists-vb/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image37.png)

**Şekil 13**: farklı bir kategori seçilmesi yeni kategorinin ürünlerini görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image39.png))

Şu anda `productsByCategory` DropDownList, değiştirildiğinde geri göndermeye neden *olmaz* . Ancak, seçilen ürünün ayrıntılarını (3. adım) göstermek için bir DetailsView eklediğimiz bir kez geri gönderme gerçekleşmemiz gerekir. Bu nedenle, `productsByCategory` DropDownList 'in akıllı etiketindeki AutoPostBack seçeneğini etkinleştir onay kutusunu işaretleyin.

[productsByCategory DropDownList için AutoPostBack özelliğini etkinleştirmek ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image40.png)

**Şekil 14**: `productsByCategory` DropDownList Için AutoPostBack özelliğini etkinleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image42.png))

## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>3\. Adım: seçili ürünün ayrıntılarını göstermek için bir DetailsView kullanma

Son adım, bir DetailsView içindeki seçili ürüne ilişkin ayrıntıları görüntülemektir. Bunu gerçekleştirmek için, sayfaya bir DetailsView ekleyin, `ID` özelliğini `ProductDetails`olarak ayarlayın ve bunun için yeni bir ObjectDataSource oluşturun. Bu ObjectDataSource 'un, *`productID`* parametresi değeri Için `ProductsByCategory` DropDownList 'in seçili değerini kullanarak verilerini `ProductsBLL` sınıfının `GetProductByProductID(productID)` yönteminden çekmek üzere yapılandırın.

[ProductsBLL sınıfını kullanmayı ![seçin](master-detail-filtering-with-two-dropdownlists-vb/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image43.png)

**Şekil 15**: `ProductsBLL` sınıfını kullanmayı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image45.png))

[GetProductByProductID (ProductID) yöntemini kullanmak için ObjectDataSource 'ı yapılandırma ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image46.png)

**Şekil 16**: `GetProductByProductID(productID)` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image48.png))

[![ProductsByCategory DropDownList öğesinden ProductID parametre değerini çekin](master-detail-filtering-with-two-dropdownlists-vb/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image49.png)

**Şekil 17**: `ProductsByCategory` DropDownList öğesinden *`productID`* parametre değerini çekme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image51.png))

`ProductDetails` DetailsView içindeki kullanılabilir alanlardan birini görüntülemeyi seçebilirsiniz. `ProductID`, `SupplierID`ve `CategoryID` alanları kaldırmak ve kalan alanları yeniden oluşturup biçimledim. Ayrıca, DetailsView 'un `Height` ve `Width` özelliklerini temizlerim ve DetailsView 'un, verileri belirtilen bir boyutla sınırlandırmak yerine en iyi şekilde görüntülemesi için gereken genişliğe genişlemesine izin verir. Tam biçimlendirme aşağıda görünür:

[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample1.aspx)]

Bir tarayıcıda `MasterDetailsDetails.aspx` sayfasını denemek için bir dakikanızı ayırın. İlk bakışta her şeyin istendiği gibi çalıştığını, ancak hafif bir sorun olduğunu fark edebilirsiniz. Yeni bir kategori seçtiğinizde `ProductsByCategory` DropDownList, seçili kategori için bu ürünleri içerecek şekilde güncelleştirilir, ancak DetailsView `ProductDetails` önceki ürün bilgilerini göstermeye devam eder. DetailsView, seçili kategori için farklı bir ürün seçerken güncelleştirilir. Ayrıca, yeterince kapsamlı bir test yaparsanız, sürekli olarak yeni kategoriler (`Categories` DropDownList 'den meşrular ' ı seçme, sonra da koşullu) ve sonra da diğer her kategori seçimi, `ProductDetails` DetailsView 'un yenilenmesine neden olur.

Bu sorunu gidermek için, belirli bir örneğe bakalım. Sayfayı ilk kez ziyaret ettiğinizde, Içecek kategorisi seçilir ve ilgili ürünler `ProductsByCategory` DropDownList 'e yüklenir. Chai seçili ürün ve ayrıntılar, Şekil 18 ' de gösterildiği gibi `ProductDetails` DetailsView içinde görüntülenir.

[![seçili ürünün ayrıntıları bir DetailsView içinde görüntülenir](master-detail-filtering-with-two-dropdownlists-vb/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image52.png)

**Şekil 18**: seçili ürünün ayrıntıları bir DetailsView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image54.png))

Kategori seçimini Alkollardan koşullu olarak değiştirirseniz, bir geri gönderme gerçekleşir ve `ProductsByCategory` DropDownList, buna göre güncelleştirilir, ancak DetailsView yine de Chai 'nin ayrıntılarını görüntüler.

[![daha önce seçilen ürünün ayrıntıları hala gösteriliyor](master-detail-filtering-with-two-dropdownlists-vb/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image55.png)

**Şekil 19**: daha önce seçilen ürünün ayrıntıları hala görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image57.png))

Listeden yeni bir ürün seçmek, DetailsView 'ı beklendiği gibi yeniler. Ürünü değiştirdikten sonra yeni bir kategori seçerseniz, DetailsView yeniden yenilenmez. Ancak, yeni bir ürün seçmek yerine yeni bir kategori seçtiyseniz, DetailsView yenilenir. Dünyayı burada bulabilirsiniz?

Sorun, sayfanın yaşam döngüsünün bir zamanlama sorunudur. Her sayfa istendiğinde, işleme kadar birkaç adım üzerinden ilerler. Bu adımlardan birinde, ObjectDataSource, `SelectParameters` değerlerinden herhangi birinin değişip değişmediğini görmek için denetimi denetler. Bu durumda, ObjectDataSource 'a bağlanan veri Web denetimi, görüntüsünü yenilemesi gerektiğini bilir. Örneğin, yeni bir kategori seçildiğinde `ProductsByCategoryDataSource` ObjectDataSource, parametre değerlerinin değiştiğini algılar ve `ProductsByCategory` DropDownList 'in kendisini yeniden bağladığını algılar ve seçili kategori için ürünleri elde eder.

Bu durumda ortaya çıkan sorun, sayfa yaşam döngüsünün, nesne veri kaynaklarının değiştirilen parametreleri denetlemesini, ilişkili veri Web denetimlerinin yeniden bağlamasının *önce* meydana gelmesinden kaynaklanır. Bu nedenle, yeni bir kategori seçerken `ProductsByCategoryDataSource` ObjectDataSource, parametre değerindeki bir değişikliği algılar. Ancak `ProductDetails` DetailsView tarafından kullanılan ObjectDataSource, `ProductsByCategory` DropDownList 'in henüz yeniden bağlanamadığı için bu tür bir değişikliği yapmaz. Yaşam döngüsünün ilerleyen kısımlarında `ProductsByCategory` DropDownList, yeni seçilen kategori için ürünleri yakalayıp. `ProductsByCategory` DropDownList 'in değeri değiştiği sırada, `ProductDetails` DetailsView 'un ObjectDataSource, parametre değeri denetimini zaten tamamladınız; Bu nedenle, DetailsView önceki sonuçları görüntüler. Bu etkileşim şekil 20 ' de gösterilmiştir.

[ProductDetails DetailsView 'un ObjectDataSource, değişiklikleri kontrol ettikten sonra ProductsByCategory DropDownList değeri değişikliklerini ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image58.png)

**Şekil 20**: `ProductsByCategory` DropDownList değeri, `ProductDetails` DetailsView 'un ObjectDataSource değişiklikler Için denetim kurulduktan sonra değişir ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image60.png))

Bu sorunu gidermek için, `ProductsByCategory` DropDownList bağlandıktan sonra `ProductDetails` DetailsView 'ı açıkça yeniden bağlamanız gerekir. Bunu, `ProductsByCategory` DropDownList 'in `DataBound` olayı tetiklendiğinde `ProductDetails` DetailsView 'un `DataBind()` yöntemini çağırarak gerçekleştirebiliriz. Aşağıdaki olay işleyici kodunu `MasterDetailsDetails.aspx` sayfanın arka plan kod sınıfına ekleyin (olay işleyicisi ekleme hakkında bir tartışma için "[ObjectDataSource 'un parametre değerlerini programlı olarak ayarlama](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)" bölümüne bakın):

[!code-vb[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample2.vb)]

`ProductDetails` DetailsView 'un `DataBind()` yöntemine yönelik bu açık çağrıdan sonra öğretici beklendiği gibi çalışmaktadır. Şekil 21 bu sorunun nasıl değiştiğini vurgular.

[ProductDetails DetailsView ![, ProductsByCategory DropDownList 'in veri bağlama olayı tetiklendiğinde](master-detail-filtering-with-two-dropdownlists-vb/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image61.png)

**Şekil 21**: `ProductsByCategory` DropDownList 'In `DataBound` olayı tetiklendiğinde `ProductDetails` DetailsView açıkça yenilenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-with-two-dropdownlists-vb/_static/image63.png))

## <a name="summary"></a>Özet

DropDownList, ana ve ayrıntı kayıtları arasında bire çok ilişki olduğu ana/ayrıntı raporlarında ideal bir kullanıcı arabirimi öğesi görevi görür. Önceki öğreticide, Seçili Kategori tarafından görünen ürünleri filtrelemek için tek bir DropDownList 'in nasıl kullanılacağını gördük. Bu öğreticide, ürünlerin GridView 'u bir DropDownList ile değiştirdik ve seçilen ürünün ayrıntılarını göstermek için bir DetailsView kullandınız. Bu öğreticide ele alınan kavramlar, müşteriler, siparişler ve sipariş öğeleri gibi birden çok bire çok ilişkiyi kapsayan veri modellerine kolayca genişletilebilir. Genel olarak, bire çok ilişkilerde "bir" varlıkların her biri için her zaman bir DropDownList ekleyebilirsiniz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](master-detail-filtering-with-a-dropdownlist-vb.md)
> [İleri](master-detail-filtering-across-two-pages-vb.md)
