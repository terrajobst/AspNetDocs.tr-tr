---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
title: Toplu güncelleştirme (VB) | Microsoft Docs
author: rick-anderson
description: Tek bir işlemde birden çok veritabanı kaydını güncelleştirmeyi öğrenin. Kullanıcı arabirimi katmanında her bir satırın düzenlenebildiği bir GridView oluşturacağız. Veride...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: d191a204-d7ea-458d-b81c-0b9049ecb55f
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
msc.type: authoredcontent
ms.openlocfilehash: f0bb83b17585876dd6d28a5893a223cce15da31d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591045"
---
# <a name="batch-updating-vb"></a>Toplu Güncelleştirme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_VB.zip) veya [PDF 'yi indirin](batch-updating-vb/_static/datatutorial64vb1.pdf)

> Tek bir işlemde birden çok veritabanı kaydını güncelleştirmeyi öğrenin. Kullanıcı arabirimi katmanında her bir satırın düzenlenebildiği bir GridView oluşturacağız. Veri erişim katmanında, tüm güncelleştirmelerin başarılı veya tüm güncelleştirmelerin geri alındığından emin olmak için bir işlem içindeki birden çok güncelleştirme işlemini sardık.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](wrapping-database-modifications-within-a-transaction-vb.md) , veritabanı işlemleri için destek eklemek üzere veri erişim katmanını genişletmeyi gördük. Veritabanı işlemleri, bir dizi veri değiştirme deyimlerinin tek bir atomik işlem olarak değerlendirilip tüm değişikliklerin başarısız olacağını veya tümünün başarılı olacağını güvence altına alır. Bu alt düzey DAL işlevselliği sayesinde, toplu veri değiştirme arabirimlerini oluşturmak için ilgilenmeniz bizim için hazır hale gelmiştir.

Bu öğreticide her bir satırın düzenlenebildiği bir GridView oluşturacağız (bkz. Şekil 1). Her satır düzenleme arabiriminde işlendiği için, Düzenle, Güncelleştir ve Iptal düğmeleri sütunu için gerekli değildir. Bunun yerine sayfada iki güncelleştirme ürünü düğmesi bulunur, tıklandığı zaman GridView satırlarını numaralandırın ve veritabanını güncelleştirebilirsiniz.

[GridView 'daki her satır ![düzenlenebilir](batch-updating-vb/_static/image1.gif)](batch-updating-vb/_static/image1.png)

**Şekil 1**: GridView 'Daki her satır düzenlenebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image2.png))

Haydi başlayın!

> [!NOTE]
> [Toplu güncelleştirmeler gerçekleştirme](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) öğreticisinde, DataList denetimini kullanarak bir toplu iş düzenlemesi arabirimi oluşturduk. Bu öğretici, ' deki bir GridView kullanan ve toplu güncelleştirme bir işlemin kapsamı içinde gerçekleştirilen bir öncekinden farklıdır. Bu Öğreticiyi tamamladıktan sonra, önceki öğreticiye geri dönmeli ve önceki öğreticide eklenen veritabanı işlemi ile ilgili işlevselliği kullanmak için onu güncelleştirmeniz önerilir.

## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>Tüm GridView satırlarını düzenlenebilir yapma adımları inceleniyor

Veri öğreticisini [ekleme, güncelleştirme ve silmeye genel bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) konusunda açıklandığı gibi, GridView, temel alınan verilerinin satır başına düzenlenmesine yönelik yerleşik destek sunar. Dahili olarak, GridView, [`EditIndex` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx)aracılığıyla hangi satırın düzenlenebilir olduğunu not edin. GridView kendi veri kaynağına bağladığından, satırın dizininin `EditIndex`değerine eşit olup olmadığını görmek için her bir satırı kontrol eder. Bu durumda, satır s alanları kendi düzen arabirimleri kullanılarak işlenir. BoundFields için, düzen arabirimi, `Text` özelliğine, BoundField s `DataField` özelliği tarafından belirtilen veri alanının değeri atanmış olan bir TextBox. TemplateFields için, `EditItemTemplate` `ItemTemplate`yerine kullanılır.

Kullanıcı bir satır Düzenle düğmesine tıkladığında düzenleme iş akışının başlayacağını geri çekin. Bu, bir geri göndermeye neden olur, GridView s `EditIndex` özelliğini tıklanmış satır s dizinine ayarlar ve verileri kılavuza yeniden bağlar. Bir satır s Iptal düğmesine tıklandığında, geri göndermede `EditIndex`, verileri kılavuza yeniden bağlanmadan önce `-1` bir değere ayarlanır. GridView s satırları dizin oluşturmaya başladıktan sonra, `EditIndex` `-1` ayarı GridView 'un salt okuma modunda görüntülenmesine etkisi vardır.

`EditIndex` özelliği satır başına düzenlemede iyi işlem yapıyor, ancak toplu düzenlemeyle ilgili tasarlanmamıştır. GridView 'un tamamını düzenlenebilir hale getirmek için, her satırı düzenleme arabirimini kullanarak işlememiz gerekir. Bunu yapmanın en kolay yolu, her düzenlenebilir alanın, `ItemTemplate`tanımlı düzenleme arabirimiyle birlikte TemplateField olarak uygulandığını oluşturmaktır.

Sonraki birkaç adımda tamamen düzenlenebilir bir GridView oluşturacağız. Adım 1 ' de, GridView ve ObjectDataSource oluşturup BoundFields ve CheckBoxField 'ı TemplateFields 'e dönüştürerek başlayacağız. Adım 2 ve 3 ' te, TemplateFields `EditItemTemplate` öğeleri `ItemTemplate` s ' ye taşıyacağız.

## <a name="step-1-displaying-product-information"></a>1\. Adım: ürün bilgilerini görüntüleme

Satırların düzenlenebildiği bir GridView oluşturma konusunda endişelenmemiz için öncelikle ürün bilgilerini görüntüleyerek başlayın. `BatchData` klasöründeki `BatchUpdate.aspx` sayfasını açın ve araç kutusundan Tasarımcı üzerine bir GridView sürükleyin. GridView s `ID` `ProductsGrid` ve akıllı etiketinden `ProductsDataSource`adlı yeni bir ObjectDataSource 'a bağlamayı seçin. `ProductsBLL` sınıf s `GetProducts` yönteminden verileri almak için ObjectDataSource 'ı yapılandırın.

[![, ObjectDataSource 'ı ProductsBLL sınıfını kullanacak şekilde yapılandırma](batch-updating-vb/_static/image2.gif)](batch-updating-vb/_static/image3.png)

**Şekil 2**: `ProductsBLL` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image4.png))

[GetProducts metodunu kullanarak ürün verilerini alma ![](batch-updating-vb/_static/image3.gif)](batch-updating-vb/_static/image5.png)

**Şekil 3**: `GetProducts` yöntemi kullanarak ürün verilerini alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image6.png))

GridView gibi, ObjectDataSource 'un değişiklik özellikleri satır başına olarak çalışacak şekilde tasarlanmıştır. Bir kayıt kümesini güncelleştirmek için, verileri toplu olarak izleyen ve BLL 'e ileten ASP.NET Page for Code arka plan sınıfında bir kod yazmanız gerekir. Bu nedenle, ObjectDataSource 'un GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden açılan listeleri (hiçbiri) ayarlayın. Sihirbazı tamamladığınızda son ' a tıklayın.

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](batch-updating-vb/_static/image4.gif)](batch-updating-vb/_static/image7.png)

**Şekil 4**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinden açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image8.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, ObjectDataSource tarafından bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](batch-updating-vb/samples/sample1.aspx)]

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamlamak, Visual Studio 'Nun, GridView 'daki ürün verileri alanları için BoundFields ve CheckBoxField oluşturmasına neden olur. Bu öğreticide, s yalnızca kullanıcının ürün adını, kategorisini, fiyatını ve Discontinued durumunu görüntülemesine ve düzenlemesine izin verir. `ProductName`, `CategoryName`, `UnitPrice`ve `Discontinued` alanları hariç tümünü kaldırın ve ilk üç alanın `HeaderText` özelliklerini sırasıyla ürün, kategori ve fiyat olarak yeniden adlandırın. Son olarak, GridView s akıllı etiketinde Sayfalamayı Etkinleştir ve sıralamayı etkinleştir onay kutularını işaretleyin.

Bu noktada GridView üç BoundFields (`ProductName`, `CategoryName`ve `UnitPrice`) ve bir CheckBoxField (`Discontinued`) içerir. Bu dört alanı TemplateFields 'e dönüştürmemiz ve daha sonra TemplateField `EditItemTemplate` düzen arabirimini `ItemTemplate`olarak taşımanız gerekir.

> [!NOTE]
> [Veri değişikliği arabirimini özelleştirme](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) öğreticisinde templatefields oluşturmayı ve özelleştirmeyi araştırıyoruz. BoundFields ve CheckBoxField değerlerini TemplateFields 'e dönüştürme ve `ItemTemplate` s 'de kendi düzen arabirimlerini tanımlama adımlarını inceleyeceğiz, ancak takıldıysanız veya bir yenileyici gerekiyorsa, bu önceki öğreticiye geri başvurmaktan çekinmeyin.

GridView s akıllı etiketinden sütunları düzenle bağlantısına tıklayarak alanlar iletişim kutusunu açın. Ardından, her bir alanı seçin ve bu alanı bir TemplateField öğesine Dönüştür bağlantısına tıklayın.

![Mevcut BoundFields ve CheckBoxField 'ı TemplateFields 'e Dönüştür](batch-updating-vb/_static/image5.gif)

**Şekil 5**: mevcut boundfields ve CheckBoxField 'ı Templatefields 'e Dönüştür

Artık her bir alan bir TemplateField olduğuna göre, `EditItemTemplate` s ' den `ItemTemplate` s öğesine kadar olan geçiş arabirimini taşımaya hazır hale gelmiştir.

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>2\. Adım:`ProductName`,`UnitPrice`ve`Discontinued`düzen arabirimlerini oluşturma

`ProductName`, `UnitPrice`ve `Discontinued` düzen arabirimlerinin oluşturulması, bu adımın konusu olduğunu ve her bir arabirim TemplateField s `EditItemTemplate`zaten tanımlandığından oldukça basittir. `CategoryName` düzen arabirimini oluşturmak, uygulanabilir kategorilerin bir DropDownList 'i oluşturmamız gerektiğinden biraz daha karmaşıktır. Bu `CategoryName` düzen arabirimi adım 3 ' te bir grup değildir.

S `ProductName` TemplateField ile başlayalım. GridView s akıllı etiketinden Şablonları Düzenle bağlantısına tıklayın ve `ProductName` TemplateField `EditItemTemplate`' a gidin. Metin kutusunu seçin, panoya kopyalayın ve sonra `ProductName` TemplateField s `ItemTemplate`yapıştırın. TextBox s `ID` özelliğini `ProductName`olacak şekilde değiştirin.

Sonra, kullanıcının her bir ürün adı için bir değer sağladığından emin olmak için `ItemTemplate` bir RequiredFieldValidator ekleyin. `ControlToValidate` özelliğini ProductName olarak ayarlayın, `ErrorMessage` özelliği ürünün adını sağlamanız gerekir. ve \*`Text` özelliği. Bu `ItemTemplate`eklemeler yapıldıktan sonra, ekranınızın Şekil 6 ' ya benzer olması gerekir.

[![ProductName TemplateField artık bir TextBox ve bir RequiredFieldValidator Içeriyor](batch-updating-vb/_static/image6.gif)](batch-updating-vb/_static/image9.png)

**Şekil 6**: `ProductName` TemplateField artık bir TextBox ve bir RequiredFieldValidator içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image10.png))

`UnitPrice` Editing arabirimi için, metin kutusunu `EditItemTemplate` `ItemTemplate`kopyalayarak başlayın. Sonra, TextBox ' ın önüne bir $ yerleştirip, `ID` özelliğini BirimFiyat ve `Columns` özelliğini 8 olarak ayarlayın.

Ayrıca, Kullanıcı tarafından girilen değerin $0,00 ' den büyük veya buna eşit geçerli bir para birimi değeri olduğundan emin olmak için `UnitPrice` s `ItemTemplate` bir CompareValidator ekleyin. Validator `ControlToValidate` özelliğini UnitPrice olarak ayarlayın, `ErrorMessage` özelliği için geçerli bir para birimi değeri girmeniz gerekir. Lütfen herhangi bir para birimi simgesini \*, `Type` özelliğini `Currency``Text`, `Operator` özelliğini `GreaterThanEqual``ValueToCompare` ve özelliğini 0 olarak atlayın.

[![, girilen fiyatın negatif olmayan bir para birimi değeri olduğundan emin olmak için bir CompareValidator ekleyin](batch-updating-vb/_static/image7.gif)](batch-updating-vb/_static/image11.png)

**Şekil 7**: girilen fiyatın negatif olmayan bir para birimi değeri olduğundan emin olmak Için bir CompareValidator ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image12.png))

`Discontinued` TemplateField alanı için `ItemTemplate`önceden tanımlanmış onay kutusunu kullanabilirsiniz. `ID`, `True`olarak `Enabled` özelliğini Discontinued olarak ayarlamanız yeterlidir.

## <a name="step-3-creating-thecategorynameediting-interface"></a>3\. Adım:`CategoryName`Editing arabirimini oluşturma

`CategoryName` TemplateField s `EditItemTemplate` içindeki Düzenle arabirimi `CategoryName` veri alanının değerini gösteren bir TextBox içerir. Bunu olası kategorileri listeleyen bir DropDownList ile değiştirdiğinizden ihtiyacımız var.

> [!NOTE]
> [Veri değişikliği arabirimini özelleştirme](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) öğreticisini özelleştirmek, bir şablonu özelleştirme hakkında daha kapsamlı ve eksiksiz bir tartışma Içerir ve metin kutusu yerine bir DropDownList içerir. Buradaki adımlar tamamlandıktan sonra, bu işlemler özellikle bir şekilde sunulur. DropDownList kategorilerini oluşturma ve yapılandırma hakkında daha ayrıntılı bir bakış için [veri değişikliği arabirimini özelleştirme](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) öğreticisine bakın.

Araç kutusundan bir DropDownList öğesini `CategoryName` TemplateField s `ItemTemplate`üzerine sürükleyin, `ID` `Categories`olarak ayarlar. Bu noktada, genellikle yeni bir ObjectDataSource oluşturarak DropDownLists veri kaynağını akıllı etiketiyle tanımlayacağız. Bununla birlikte, bu, her GridView satırı için oluşturulan ObjectDataSource örneği ile sonuçlanacaktır `ItemTemplate`içindeki ObjectDataSource 'ı ekler. Bunun yerine, ObjectDataSource 'yi GridView s TemplateFields dışındaki oluşturmalarına izin verin. Şablon düzenlemesini sonlandırın ve araç kutusundan bir ObjectDataSource 'ı `ProductsDataSource` ObjectDataSource 'un altında tasarımcı üzerine sürükleyin. Yeni ObjectDataSource `CategoriesDataSource` adlandırın ve `CategoriesBLL` Class s `GetCategories` metodunu kullanacak şekilde yapılandırın.

[![, ObjectDataSource 'un CategoriesBLL sınıfını kullanacak şekilde yapılandırılması](batch-updating-vb/_static/image8.gif)](batch-updating-vb/_static/image13.png)

**Şekil 8**: ObjectDataSource 'ı `CategoriesBLL` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image14.png))

[GetCategories metodunu kullanarak kategori verilerini alma ![](batch-updating-vb/_static/image9.gif)](batch-updating-vb/_static/image15.png)

**Şekil 9**: `GetCategories` yöntemi kullanarak kategori verilerini alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image16.png))

Bu ObjectDataSource yalnızca verileri almak için kullanıldığından, GÜNCELLEŞTIR ve SIL sekmelerinde açılan listeleri (None) olarak ayarlayın. Sihirbazı tamamladığınızda son ' a tıklayın.

[GÜNCELLEŞTIRME ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](batch-updating-vb/_static/image10.gif)](batch-updating-vb/_static/image17.png)

**Şekil 10**: GÜNCELLEŞTIR ve Sil sekmelerinde açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image18.png))

Sihirbazı tamamladıktan sonra, `CategoriesDataSource` s bildirime dayalı biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](batch-updating-vb/samples/sample2.aspx)]

Oluşturulan ve yapılandırılan `CategoriesDataSource` `CategoryName` TemplateField s `ItemTemplate` ve DropDownList s akıllı etiketinde veri kaynağı Seç bağlantısına tıklayın. Veri kaynağı Yapılandırma sihirbazında, ilk açılan listeden `CategoriesDataSource` seçeneğini belirleyin ve ekran için `CategoryName` ve değer olarak `CategoryID` ' yı seçin.

[DropDownList 'i CategoriesDataSource 'a bağlama ![](batch-updating-vb/_static/image11.gif)](batch-updating-vb/_static/image19.png)

**Şekil 11**: DropDownList 'i `CategoriesDataSource` bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image20.png))

Bu noktada `Categories` DropDownList tüm kategorileri listeler, ancak GridView satırına bağlantılı ürün için uygun kategoriyi henüz otomatik olarak seçmeyin. Bunu gerçekleştirmek için `Categories` DropDownList s `SelectedValue` ürün s `CategoryID` değerine ayarlamanız gerekir. DropDownList s akıllı etiketinden DataBindings 'i düzenle bağlantısına tıklayın ve `SelectedValue` özelliğini Şekil 12 ' de gösterildiği gibi `CategoryID` Data alanı ile ilişkilendirin.

![Product s CategoryID değerini DropDownList s SelectedValue özelliğine bağlayın](batch-updating-vb/_static/image12.gif)

**Şekil 12**: ürün s `CategoryID` değerini DropDownList s `SelectedValue` özelliğine bağlama

Son bir sorun kalır: ürünün `CategoryID` bir değeri belirtilmemişse, `SelectedValue` veri bağlama deyimlerinin bir özel durumla sonuçlanacaktır. Bunun nedeni, DropDownList 'in yalnızca kategoriler için öğeler içermesi ve `CategoryID`için `NULL` veritabanı değeri olan ürünler için bir seçenek sunmamaktadır. Bu sorunu gidermek için, DropDownList s `AppendDataBoundItems` özelliğini `True` olarak ayarlayın ve DropDownList 'e yeni bir öğe ekleyerek bildirime dayalı sözdiziminden `Value` özelliğini atlayarak. Diğer bir deyişle, `Categories` DropDownList s bildirime dayalı sözdiziminin aşağıdaki gibi göründüğünden emin olun:

[!code-aspx[Main](batch-updating-vb/samples/sample3.aspx)]

`<asp:ListItem Value="">`--Select One--`Value` özniteliğini açık bir şekilde boş bir dizeye nasıl ayarlayabileceğinizi aklınızda edin. `NULL` durumunu işlemek için bu ek DropDownList öğesinin neden gerekli olduğu ve `Value` özelliğinin boş bir dizeye atanmasının ne kadar önemli olduğunu hakkında daha ayrıntılı bir tartışma için [veri değişikliği arabirimini özelleştirme](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) öğreticisine geri bakın.

> [!NOTE]
> Burada, gereken olası bir performans ve ölçeklenebilirlik sorunu vardır. Her satırda, veri kaynağı olarak `CategoriesDataSource` kullanan bir DropDownList bulunduğundan, `CategoriesBLL` sınıf s `GetCategories` yöntemi sayfa ziyaret başına *n* kez adlandırılır; burada *n* , GridView 'daki satır sayısıdır. Bu *n* `GetCategories` çağrısı, veritabanına *n* sorgu ile sonuçlanır. Veritabanı üzerindeki bu etki, döndürülen kategorilerin istek başına önbellekte ya da SQL önbellek bağımlılığı veya çok kısa bir süre tabanlı süre sonu kullanılarak önbelleğe alma katmanında önbelleğe alınarak azaltılabilir. İstek başına önbelleğe alma seçeneği hakkında daha fazla bilgi için, bkz. [Istek başına önbellek deposu`HttpContext.Items`](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx).

## <a name="step-4-completing-the-editing-interface"></a>4\. Adım: düzen arabirimini tamamlama

İlerleme durumunu görüntülemek için, ' i duraklatmadan GridView s şablonlarında birkaç değişiklik yaptık. Bir tarayıcıdan ilerleme durumunu görüntülemek için bir dakikanızı ayırın. Şekil 13 ' te gösterildiği gibi, her satır, onun `ItemTemplate`kullanılarak işlenir ve bu da hücre s Editing arabirimini içerir.

[Her GridView satırı ![düzenlenebilir](batch-updating-vb/_static/image13.gif)](batch-updating-vb/_static/image21.png)

**Şekil 13**: her GridView satırı düzenlenebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image22.png))

Bu noktada ilgilenmemiz gereken birkaç küçük biçimlendirme sorunu vardır. İlk olarak, `UnitPrice` değerinin dört ondalık noktası içerdiğini unutmayın. Bunu yapmak için, `UnitPrice` TemplateField s `ItemTemplate` geri dönüp metin kutusu s akıllı etiketinden, DataBindings 'i düzenle bağlantısına tıklayın. Sonra, `Text` özelliğinin bir sayı olarak biçimlendirilmesi gerektiğini belirtin.

![Metin özelliğini bir sayı olarak biçimlendirin](batch-updating-vb/_static/image14.gif)

**Şekil 14**: `Text` özelliğini sayı olarak biçimlendirme

İkincisi, `Discontinued` sütunundaki onay kutusunu ortalamasına izin ver (sola hizalı olmasını yerine). GridView s akıllı etiketinden sütunları Düzenle ' ye tıklayın ve sol alt köşedeki alanlar listesinden `Discontinued` TemplateField ' ı seçin. `ItemStyle` detaya gidin ve şekil 15 ' te gösterildiği gibi `HorizontalAlign` özelliğini Center olarak ayarlayın.

![Discontinued onay kutusunu Ortala](batch-updating-vb/_static/image15.gif)

**Şekil 15**: `Discontinued` onay kutusunu ortalayın

Sonra, sayfaya bir ValidationSummary denetimi ekleyin ve `ShowMessageBox` özelliğini `True` ve `ShowSummary` özelliğini `False`olarak ayarlayın. Ayrıca, tıklandığında Kullanıcı değişikliklerinin güncelleştirilmesini sağlayacak olan düğme Web denetimlerini de ekleyin. Özellikle, GridView 'un üzerinde bir tane olmak üzere iki düğme web denetimi ekleyin, her iki denetimi de ürünleri güncelleştirmek için `Text` özellikleri.

GridView s Düzenle arabirimi TemplateFields `ItemTemplate` s içinde tanımlandığından, `EditItemTemplate` s gereksiz olduğundan silinebilir.

Yukarıda bahsedilen biçimlendirme değişikliklerini yaptıktan sonra, düğme denetimlerini ekleyerek ve gereksiz `EditItemTemplate` s 'yi kaldırarak, sayfa oluşturma sözdiziminizin aşağıdaki gibi görünmesi gerekir:

[!code-aspx[Main](batch-updating-vb/samples/sample4.aspx)]

Şekil 16, düğme Web denetimleri eklendikten ve biçimlendirme değişiklikleri yapıldıktan sonra bir tarayıcı aracılığıyla görüntülendiğinde bu sayfayı gösterir.

[Sayfa ![artık Iki güncelleştirme ürünü düğmesi Içerir](batch-updating-vb/_static/image16.gif)](batch-updating-vb/_static/image23.png)

**Şekil 16**: sayfa artık Iki güncelleştirme ürünü düğmesi içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-updating-vb/_static/image24.png))

## <a name="step-5-updating-the-products"></a>5\. Adım: ürünleri güncelleştirme

Bir Kullanıcı bu sayfayı ziyaret ettiğinde, değişiklikleri yapar ve ardından iki güncelleştirme ürünü düğmesinden birine tıklamaları gerekir. Bu noktada, her satır için Kullanıcı tarafından girilen değerleri bir `ProductsDataTable` örneğine kaydetmeniz ve sonra bu `ProductsDataTable` örneğini DAL s `UpdateWithTransaction` yöntemine geçirecek bir BLL yöntemine iletmemiz gerekir. [Önceki öğreticide](wrapping-database-modifications-within-a-transaction-vb.md)oluşturduğumuz `UpdateWithTransaction` yöntemi, değişiklik toplu işinin atomik bir işlem olarak güncelleştirilmesini sağlar.

`BatchUpdate.aspx.vb` `BatchUpdate` adlı bir yöntem oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](batch-updating-vb/samples/sample5.vb)]

Bu yöntem, BLL s `GetProducts` yöntemine yapılan bir çağrı aracılığıyla `ProductsDataTable` tüm ürünleri geri alarak başlatılır. Ardından `ProductGrid` GridView s [`Rows` koleksiyonunu](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)numaralandırır. `Rows` koleksiyonu, GridView 'da görünen her satır için bir [`GridViewRow` örneği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewrow.aspx) içerir. Sayfa başına en fazla on satır gösterdiğimiz için, GridView s `Rows` koleksiyonda on öğeden fazla öğe olmayacaktır.

Her satır için `ProductID` `DataKeys` koleksiyonundan bir şekilde belirlenir ve `ProductsDataTable`uygun `ProductsRow` seçilir. Program aracılığıyla dört adet TemplateField giriş denetimine başvurulur ve bunların değerleri `ProductsRow` örnek s özelliklerine atanır. Her bir GridView satır s değeri `ProductsDataTable`güncelleştirmek için kullanıldıktan sonra, bu, önceki öğretic`UpdateWithTransaction` ide gördüğünüz gibi BLL s `UpdateWithTransaction` yöntemine geçirilir.

Bu öğretici için kullanılan Batch güncelleştirme algoritması, ürün bilgilerinin değiştirilip değiştirilmediğine bakılmaksızın GridView 'daki bir satıra karşılık gelen `ProductsDataTable` her satırı güncelleştirir. Bu görünmeyen güncelleştirmeler genellikle bir performans sorunu olsa da, veritabanı tablosunda yapılan değişiklikleri yeniden denetlebiliyorsanız, bu değişiklikler gereksiz kayıtlara yol açabilir. [Toplu güncelleştirmeler gerçekleştirme](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) öğreticisine geri döndüğünüzde, DataList ve yalnızca Kullanıcı tarafından değiştirilen kayıtları güncelleştirecek kod içeren bir toplu güncelleştirme arabirimi araştırdık. İsterseniz bu öğreticide kodu güncelleştirmek için [toplu güncelleştirmeler gerçekleştirmekten](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) yararlanabilirsiniz.

> [!NOTE]
> Veri kaynağı GridView 'a akıllı etiketi aracılığıyla bağlarken, Visual Studio veri kaynağı s birincil anahtar değerlerini otomatik olarak GridView s `DataKeyNames` özelliğine atar. Adım 1 ' de özetlenen GridView 'un akıllı etiketi aracılığıyla ObjectDataSource 'u GridView 'a bağladıysanız, her bir satır için `ProductID` değerine `DataKeys` koleksiyonu aracılığıyla erişmek için GridView s `DataKeyNames` özelliğini el ile ProductID olarak ayarlamanız gerekecektir.

`BatchUpdate` kullanılan kod BLL s `UpdateProduct` yöntemlerinde kullanılanlara benzerdir; `UpdateProduct` yöntemlerinde yalnızca tek bir `ProductRow` örneği, mimariden alınan asıl farktır. `ProductRow` özelliklerini atayan kod, genel bir düzende olduğu gibi, `BatchUpdate`içindeki `For Each` döngüsünde bulunan `UpdateProducts` yöntemleri ve kodla aynıdır.

Bu öğreticiyi tamamlayabilmeniz için, güncelleştirme ürünleri düğmelerinden herhangi biri tıklandığında `BatchUpdate` yönteminin çağrılması gerekir. Bu iki düğme denetiminin `Click` olayları için olay işleyicileri oluşturun ve olay işleyicilerinde aşağıdaki kodu ekleyin:

[!code-vb[Main](batch-updating-vb/samples/sample6.vb)]

`BatchUpdate`için ilk çağrı yapılır. Ardından [`ClientScript` özelliği](https://msdn.microsoft.com/library/system.web.ui.page.clientscript(VS.80).aspx) , güncelleştirilmiş ürünleri okuyan bir MessageBox görüntüleyen JavaScript eklemek için kullanılır.

Bu kodu sınamak için bir dakikanızı alın. Tarayıcı aracılığıyla `BatchUpdate.aspx` ziyaret edin, bir dizi satırı düzenleyin ve güncelleştirme ürünleri düğmelerinden birine tıklayın. Hiç giriş doğrulama hatası olmadığı varsayılarak, güncelleştirilmiş ürünleri okuyan bir MessageBox görmeniz gerekir. Güncelleştirmenin kararlılığını doğrulamak için, `UnitPrice` 1234,56 değerine izin vermeyen bir rastgele `CHECK` kısıtlaması eklemeyi göz önünde bulundurun. `BatchUpdate.aspx`, bir dizi kaydı düzenleyin ve ürün `UnitPrice` değerinden birini yasak değere (1234,56) ayarladığınızdan emin olun. Bu, toplu işlem sırasında orijinal değerlerine geri alındığında diğer değişikliklerle ürünleri Güncelleştir ' e tıkladığınızda bir hatayla sonuçlanır.

## <a name="an-alternativebatchupdatemethod"></a>Alternatif bir`BatchUpdate`yöntemi

Az önce incelediğimiz `BatchUpdate` yöntemi BLL s `GetProducts` yönteminden *Tüm* ürünleri alır ve ardından GridView içinde görünen kayıtları güncelleştirir. GridView, sayfalama kullanmıyorsa bu yaklaşım idealdir, ancak varsa yüzlerce, binlerce veya onlarca binlerce ürün, ancak GridView içinde yalnızca on satır olabilir. Böyle bir durumda, veritabanındaki tüm ürünlerin yalnızca 10 ' u değiştirmek ideal olandan düşüktür.

Bu tür durumlar için, bunun yerine aşağıdaki `BatchUpdateAlternate` yöntemini kullanmayı göz önünde bulundurun:

[!code-vb[Main](batch-updating-vb/samples/sample7.vb)]

`BatchMethodAlternate`, `products`adlı yeni bir boş `ProductsDataTable` oluşturarak başlar. Ardından, GridView s `Rows` koleksiyonu ve her satır için BLL s `GetProductByProductID(productID)` yöntemini kullanarak belirli ürün bilgilerini alır. Alınan `ProductsRow` örneğinin özellikleri `BatchUpdate`aynı şekilde güncelleştirilir, ancak satırı güncelleştirdikten sonra DataTable s [`ImportRow(DataRow)` yöntemi](https://msdn.microsoft.com/library/system.data.datatable.importrow(VS.80).aspx)aracılığıyla `products` `ProductsDataTable` içeri aktarılır.

`For Each` döngüsü tamamlandıktan sonra, `products` GridView 'daki her satır için bir `ProductsRow` örneği içerir. `ProductsRow` örneklerinin her biri `products` eklenmiş olduğundan (güncelleştirilmiş yerine), `UpdateWithTransaction` yöntemine bir şekilde geçirirseniz, `ProductsTableAdapter` kayıtların her birini veritabanına eklemeye çalışacaktır. Bunun yerine, bu satırların her birinin değiştirildiğini (eklenmemiş) belirtmemiz gerekir.

Bu, BLL adlı `UpdateProductsWithTransaction`yeni bir yöntem eklenerek gerçekleştirilebilir. Aşağıda gösterilen `UpdateProductsWithTransaction`, `ProductsDataTable` `ProductsRow` örneklerinin her birinin `RowState` `Modified` ve ardından `ProductsDataTable` DAL s `UpdateWithTransaction` yöntemine geçirir.

[!code-vb[Main](batch-updating-vb/samples/sample8.vb)]

## <a name="summary"></a>Özet

GridView, yerleşik satır başına düzenleme özellikleri sağlar, ancak tamamen düzenlenebilir arabirimler oluşturma desteği yoktur. Bu öğreticide gördüğünüz gibi, bu tür arabirimler mümkündür ancak biraz iş gerektirir. Her satırın düzenlenebildiği bir GridView oluşturmak için, GridView s alanlarını TemplateFields 'e dönüştürmemiz ve `ItemTemplate` s içinde düzenleme arabirimini tanımlamanız gerekir. Ayrıca, Update All-Type düğme Web denetimlerini, GridView 'dan ayrı olarak sayfaya eklenmelidir. Bu düğmeler `Click` olay işleyicilerinin GridView s `Rows` koleksiyonunu numaralandırması, değişiklikleri bir `ProductsDataTable`depolaması ve güncelleştirilmiş bilgileri uygun BLL yöntemine geçirmesi gerekir.

Sonraki öğreticide toplu silme için bir arabirim oluşturma hakkında bilgi edineceksiniz. Özellikle, her GridView satırı bir onay kutusu içerir ve tüm tür düğmelerini güncelleştirmek yerine seçili satırları sil düğmelerini kullanacağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, bir Murphy ve David suru olarak eklenmiştir. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](wrapping-database-modifications-within-a-transaction-vb.md)
> [İleri](batch-deleting-vb.md)
