---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
title: Ayrıntılar DetailView (C#) ile seçilebilir bir ana GridView kullanan ana/ayrıntı | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, satırları her bir ürünün adını ve fiyatını içeren bir GridView bulunur ve bir Seç düğmesi. Bir particu için seçme düğmesine tıklanması...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0f982827-f8f9-420d-b36b-57b23f5aa519
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
msc.type: authoredcontent
ms.openlocfilehash: 04c427341f063729bd23b416a96f5acb20702792
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621067"
---
# <a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-c"></a>Ayrıntılar DetailView’u ile Seçilebilir Bir Ana GridView Kullanan Ana/Ayrıntı (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_10_CS.exe) veya [PDF 'yi indirin](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/datatutorial10cs1.pdf)

> Bu öğreticide, satırları her bir ürünün adını ve fiyatını içeren bir GridView bulunur ve bir Seç düğmesi. Belirli bir ürünün Seç düğmesine tıklamak, tam ayrıntılarının aynı sayfada bir DetailsView denetiminde görüntülenmesine neden olur.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](master-detail-filtering-across-two-pages-cs.md) , iki Web sayfası kullanarak bir ana/ayrıntı raporu oluşturmayı öğrendiniz: tedarikçiler listesini görüntüdiğimiz bir "ana" Web sayfası. ve seçilen tedarikçi tarafından verilen ürünleri listelenen bir "Ayrıntılar" Web sayfası. Bu iki sayfa rapor biçimi tek bir sayfada dar olabilir. Bu öğreticide, satırları her bir ürünün adını ve fiyatını içeren bir GridView bulunur ve bir Seç düğmesi. Belirli bir ürünün Seç düğmesine tıklamak, tam ayrıntılarının aynı sayfada bir DetailsView denetiminde görüntülenmesine neden olur.

[Seç düğmesine tıklamak ![ürünün ayrıntılarını görüntüler](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image1.png)

**Şekil 1**: Seç düğmesine tıkladığınızda ürünün ayrıntıları görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image3.png))

## <a name="step-1-creating-a-selectable-gridview"></a>1\. Adım: seçilebilir bir GridView oluşturma

İki sayfalı ana/ayrıntı raporunda, her ana kaydın tıklandığı sırada kullanıcıyı, tıklanmış satırın QueryString içindeki `SupplierID` değerini geçirerek ayrıntılar sayfasına gönderdiği bir köprü içerdiği şekilde geri çekin. Bu tür bir köprü, her GridView satırına bir Hyperlinkalanı kullanılarak eklenmiştir. Tek sayfalı ana/Ayrıntılar raporu için, tıklandığı sırada ayrıntıları gösteren her GridView satırı için bir düğmeye ihtiyacımız olacak. GridView denetimi, geri göndermeye neden olan her satır için bir seçim düğmesi içerecek şekilde yapılandırılabilir ve söz konusu satırı GridView 'in [SelectedRow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)olarak işaretler.

`Filtering` klasöründeki `DetailsBySelecting.aspx` sayfasına bir GridView denetimi ekleyerek başlayın ve `ID` özelliğini `ProductsGrid`olarak ayarlar. Sonra, `ProductsBLL` sınıfının `GetProducts()` yöntemini çağıran `AllProductsDataSource` adlı yeni bir ObjectDataSource ekleyin.

[![AllProductsDataSource adlı bir ObjectDataSource oluşturma](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image4.png)

**Şekil 2**: `AllProductsDataSource` adlı bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image6.png))

[ProductsBLL sınıfını kullanmak ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image7.png)

**Şekil 3**: `ProductsBLL` sınıfını kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image9.png))

[![GetProducts () yöntemini çağırmak için ObjectDataSource 'ı yapılandırma](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image10.png)

**Şekil 4**: `GetProducts()` yöntemini çağırmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image12.png))

GridView 'un alanlarını, `ProductName` ve `UnitPrice` BoundFields alanlarını kaldırarak düzenleyin. Ayrıca, bu BoundFields 'i bir para birimi olarak `UnitPrice` biçimlendirme ve BoundFields `HeaderText` özelliklerini değiştirme gibi gerektiği şekilde özelleştirebilirsiniz. Bu adımlar, GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklanarak veya bildirim temelli sözdizimini el ile yapılandırarak grafiksel olarak gerçekleştirilebilir.

[![ProductName ve BirimFiyat BoundFields alanlarını kaldırın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image13.png)

**Şekil 5**: tüm `ProductName` ve `UnitPrice` boundfields alanlarını kaldırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image15.png))

GridView için son biçimlendirme:

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample1.aspx)]

Sonra, GridView 'u seçilebilir olarak işaretlememiz gerekir ve bu, her satıra bir SELECT düğmesi ekler. Bunu gerçekleştirmek için GridView 'un akıllı etiketindeki seçimi etkinleştir onay kutusunu işaretleyin.

[GridView 'un satırlarını seçilebilir hale getirmek ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image16.png)

**Şekil 6**: GridView 'un satırlarını seçilebilir hale getirme ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image18.png))

Seçim etkinleştirme seçeneğinin işaretlenmesi, `ProductsGrid` GridView öğesine `ShowSelectButton` özelliği true olarak ayarlanmış bir CommandField ekler. Bu, Şekil 6 ' da gösterildiği gibi, GridView 'un her satırı için bir seçme düğmesi ile sonuçlanır. Varsayılan olarak, seçme düğmeleri LinkButtons olarak işlenir, ancak CommandField 'ın `ButtonType` özelliği aracılığıyla bunun yerine düğmeler veya ImageButton kullanabilirsiniz.

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample2.aspx)]

Bir GridView satırının Select düğmesine tıklandığında bir geri gönderme işlemi başarılı olduğunda ve GridView 'un `SelectedRow` özelliği güncellenir. GridView, `SelectedRow` özelliğine ek olarak [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx), [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx)ve [SelectedDataKey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx) özelliklerini de sağlar. `SelectedIndex` özelliği, seçili satırın dizinini döndürür, ancak `SelectedValue` ve `SelectedDataKey` özellikleri GridView 'un [DataKeyNames özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)temel alan değerler döndürür.

`DataKeyNames` özelliği, bir veya daha fazla veri alanı değerini her satırla ilişkilendirmek için kullanılır ve genellikle her bir GridView satırı ile temel alınan verilerden bilgileri benzersiz bir şekilde tanımlamak için kullanılır. `SelectedValue` özelliği, seçili satırın ilk `DataKeyNames` veri alanının değerini döndürür; burada `SelectedDataKey` `DataKey` özelliği, bu satır için belirtilen veri anahtarı alanları için tüm değerleri içerir.

Tasarımcı aracılığıyla bir GridView, DetailsView veya FormView 'a veri kaynağı bağladığınızda `DataKeyNames` özelliği otomatik olarak tanımlayıcı veri alanları olarak ayarlanır. Bu özellik, önceki öğreticilerde sizin için otomatik olarak ayarlansa da, örnekler `DataKeyNames` özelliği belirtilmeden çalışırdı. Bununla birlikte, bu öğreticideki seçilebilir GridView için ve ekleme, güncelleştirme ve silme konusunda incelendiğimiz gelecekteki öğreticiler için `DataKeyNames` özelliği düzgün şekilde ayarlanmalıdır. GridView 'un `DataKeyNames` özelliğinin `ProductID`olarak ayarlandığından emin olmak için bir dakikanızı ayırın.

Bundan sonra ilerleme durumunu bir tarayıcıdan görüntüleyelim. GridView 'un tüm ürünlerin adını ve fiyatını bir SELECT LinkButton ile birlikte listelediğinden emin olmanız gerektiğini unutmayın. Seç düğmesine tıklamak geri göndermeye neden olur. 2\. adımda, seçilen ürünün ayrıntılarını görüntüleyerek bir DetailsView 'un bu geri göndermeye nasıl yanıt vereceğini göreceksiniz.

[Her ürün satırı ![bir SELECT LinkButton Içerir](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image19.png)

**Şekil 7**: her ürün satırı bir SELECT LinkButton içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image21.png))

### <a name="highlighting-the-selected-row"></a>Seçili satırı vurgulama

`ProductsGrid` GridView, seçili satır için görsel stili dikte etmek üzere kullanılabilecek bir `SelectedRowStyle` özelliğine sahiptir. Doğru şekilde kullanıldığında, bu, GridView 'un hangi satırının seçili olduğunu daha net bir şekilde göstererek kullanıcının deneyimini iyileştirebilir. Bu öğreticide, seçili satırın sarı bir arka planla vurgulanmasını sağlayın.

Önceki öğreticilerimizden itibaren olduğu gibi, Aesthetic Characteristics ile ilgili ayarları CSS sınıfları olarak tanımlanmış tutmak için çaba gösterelim. Bu nedenle, `SelectedRowStyle`adlı `Styles.css` yeni bir CSS sınıfı oluşturun.

[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample3.css)]

Bu CSS sınıfını öğretici serimizin *Tüm* gridviews 'ın `SelectedRowStyle` özelliğine uygulamak için, `DataWebControls` temasının `GridView.skin` kaplamayı aşağıda gösterildiği gibi `SelectedRowStyle` ayarlarını içerecek şekilde düzenleyin:

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample4.aspx)]

Bu ek olarak, seçili GridView satırı artık sarı bir arka plan rengiyle vurgulanır.

[GridView 'un SelectedRowStyle özelliğini kullanarak seçili satırın görünümünü özelleştirmek ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image22.png)

**Şekil 8**: GridView 'un `SelectedRowStyle` özelliğini kullanarak seçili satırın görünümünü özelleştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image24.png))

## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>2\. Adım: seçili ürünün ayrıntılarını bir DetailsView 'da görüntüleme

`ProductsGrid` GridView tamamlandığına göre, her şey seçilen belirli ürün hakkında bilgi görüntüleyen bir DetailsView eklemektir. GridView 'un üzerine bir DetailsView denetimi ekleyin ve `ProductDetailsDataSource`adlı yeni bir ObjectDataSource oluşturun. Bu DetailsView 'un seçili ürünle ilgili belirli bilgileri göstermesini istediğimiz için, `ProductDetailsDataSource` `ProductsBLL` sınıfının `GetProductByProductID(productID)` metodunu kullanacak şekilde yapılandırın.

[ProductsBLL sınıfının GetProductByProductID (ProductID) yöntemini çağır ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image25.png)

**Şekil 9**: `ProductsBLL` sınıfının `GetProductByProductID(productID)` metodunu çağırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image27.png))

GridView denetiminin `SelectedValue` özelliğinden *`productID`* parametresinin değerini elde edin. Daha önce anlatıldığı gibi, GridView 'un `SelectedValue` özelliği seçili satır için ilk veri anahtarı değerini döndürür. Bu nedenle, GridView 'ın `DataKeyNames` özelliğinin `ProductID`olarak ayarlanması zorunludur, böylece seçilen satırın `ProductID` değeri `SelectedValue`tarafından döndürülür.

[![ProductID parametresini GridView 'un SelectedValue özelliğine ayarlayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image28.png)

**Şekil 10**: *`productID`* parametresini GridView 'un `SelectedValue` özelliğine ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image30.png))

`productDetailsDataSource` ObjectDataSource doğru şekilde yapılandırıldıktan ve DetailsView 'a bağlandıktan sonra, bu öğretici tamamlanmıştır! Sayfa ilk kez ziyaret edildiğinde, GridView 'un `SelectedValue` özelliği `null`döndürür. `NULL` `ProductID` değeri olan bir ürün olmadığından, `GetProductByProductID(productID)` yöntemi tarafından hiçbir kayıt döndürülmez, yani DetailsView gösterilmez (bkz. Şekil 11). Bir GridView satırının seçme düğmesine tıklandıktan sonra, bir geri gönderme ve DetailsView yenilenir. GridView 'un `SelectedValue` özelliği seçili satırın `ProductID` geri döndürürse, `GetProductByProductID(productID)` yöntemi söz konusu ürünle ilgili bilgileri içeren bir `ProductsDataTable` döndürür ve DetailsView bu ayrıntıları gösterir (bkz. Şekil 12).

[Ilk ziyaret edildiğinde ![yalnızca GridView görüntülenir](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image31.png)

**Şekil 11**: ilk ziyaret edildiğinde, yalnızca GridView görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image33.png))

[bir satırı seçtikten sonra ![ürünün ayrıntıları görüntülenir](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image34.png)

**Şekil 12**: bir satır seçildikten sonra ürünün ayrıntıları görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image36.png))

## <a name="summary"></a>Özet

Bu ve önceki üç öğreticilerde, ana/ayrıntı raporlarını görüntülemek için çeşitli teknikler gördük. Bu öğreticide, aynı sayfada seçili ana kayıtla ilgili ayrıntıları göstermek üzere ana kayıtları ve bir DetailsView 'u barındırmak için seçilebilir bir GridView kullanmayı inceledik. Önceki öğreticilerde, DropDownLists kullanarak ana/ayrıntı raporlarının nasıl görüntüleneceğini ve bir Web sayfasında ana kayıtları ve başka bir sayfada ayrıntı kayıtlarını görüntülemeyi inceledik.

Bu öğreticide, ana/ayrıntı raporlarının incelemesi sonlanır. Sonraki öğreticiden başlayarak, GridView, DetailsView ve FormView ile özelleştirilmiş biçimlendirme araştırmasına başlayacağız. Bu denetimlerin görünüşünü, bunlara bağlı verilere göre nasıl özelleştireceğinizi, GridView 'un altbilgisinde verilerin nasıl özetleyeceğini ve düzen üzerinde daha fazla denetim elde etmek için şablonların nasıl kullanılacağını inceleyeceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](master-detail-filtering-across-two-pages-cs.md)
> [İleri](master-detail-filtering-with-a-dropdownlist-vb.md)
