---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
title: Onay kutularının GridView sütununu ekleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğretici, kullanıcıya G 'nin birden çok satırını seçmenin sezgisel bir yolunu sağlamak için bir GridView denetimine onay kutuları sütununun nasıl ekleneceğini inceler...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 39253d05-75c0-41c7-b9d4-a6c58ecf69ce
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: c620b2eac5844d4030c1309b45e7d6a72d1f386a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592297"
---
# <a name="adding-a-gridview-column-of-checkboxes-vb"></a>Onay Kutularından Oluşan GridView Sütunu Ekleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_VB.exe) veya [PDF 'yi indirin](adding-a-gridview-column-of-checkboxes-vb/_static/datatutorial52vb1.pdf)

> Bu öğretici, kullanıcıya GridView 'un birden çok satırını seçmenin sezgisel bir yolunu sağlamak için bir GridView denetimine onay kutularından oluşan bir sütun ekleme hakkında bakar.

## <a name="introduction"></a>Giriş

Önceki öğreticide, belirli bir kaydı seçme amacıyla GridView 'a bir radyo düğmeleri sütununun nasıl ekleneceğini inceliyoruz. Radyo düğmelerinin bir sütunu, Kullanıcı kılavuzdan en çok bir öğe seçmeye sınırlı olduğunda uygun bir kullanıcı arabirimidir. Ancak, bazen kullanıcının kılavuzdan rastgele sayıda öğe seçmesine izin vermek isteyebilirsiniz. Örneğin, Web tabanlı e-posta istemcileri, genellikle onay kutusu sütunuyla ileti listesini görüntüler. Kullanıcı rastgele sayıda ileti seçebilir ve sonra e-postaları başka bir klasöre taşıma veya silme gibi bazı eylemler gerçekleştirebilir.

Bu öğreticide, onay kutusu sütunu eklemeyi ve geri gönderme sırasında hangi onay kutularının denetlendiğini öğreneceğiz. Özellikle, Web tabanlı e-posta istemcisi kullanıcı arabirimine benzer bir örnek oluşturacağız. Örneğimiz, her satırda onay kutusu bulunan `Products` veritabanı tablosundaki ürünleri listelemek için bir Sayfalanmış GridView içerir (bkz. Şekil 1). Seçili ürünleri Sil düğmesi tıklandığında seçili olan ürünler silinir.

[Her ürün satırına ![onay kutusu dahildir](adding-a-gridview-column-of-checkboxes-vb/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image1.png)

**Şekil 1**: her ürün satırında bir onay kutusu bulunur ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image2.png))

## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>1\. Adım: ürün bilgilerini listeleyen bir sayfalama GridView ekleme

Onay kutularının bir sütununu ekleme konusunda kaygılanmadan önce, ilk olarak sayfalama 'yi destekleyen bir GridView 'da ürünlerin listelenmesine odaklanın. `EnhancedGridView` klasöründeki `CheckBoxField.aspx` sayfasını açıp araç kutusundan bir GridView sürükleyip `ID` `Products`olarak ayarlayarak başlayın. Sonra, GridView öğesini `ProductsDataSource`adlı yeni bir ObjectDataSource 'a bağlamayı seçin. ObjectDataSource 'u, verileri döndürmek için `GetProducts()` metodunu çağırarak `ProductsBLL` sınıfını kullanacak şekilde yapılandırın. Bu GridView salt okunurdur, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden açılan listeleri (hiçbiri) ayarlayın.

[![ProductsDataSource adlı yeni bir ObjectDataSource oluşturma](adding-a-gridview-column-of-checkboxes-vb/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image3.png)

**Şekil 2**: `ProductsDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image4.png))

[GetProducts () yöntemini kullanarak verileri almak için ObjectDataSource 'ı yapılandırma ![](adding-a-gridview-column-of-checkboxes-vb/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image5.png)

**Şekil 3**: `GetProducts()` metodunu kullanarak verileri almak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image6.png))

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](adding-a-gridview-column-of-checkboxes-vb/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image7.png)

**Şekil 4**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinden açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image8.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio, ürünle ilgili veri alanları için otomatik olarak BoundColumns ve bir CheckBoxColumn oluşturur. Önceki öğreticide yaptığımız gibi, `ProductName`, `CategoryName`ve `UnitPrice` BoundFields alanlarını kaldırın ve `HeaderText` özelliklerini ürün, kategori ve fiyat olarak değiştirin. `UnitPrice` BoundField değerini, değeri bir para birimi olarak biçimlendirilecek şekilde yapılandırın. Ayrıca, GridView 'ı akıllı etiketten sayfalama etkinleştir onay kutusunu işaretleyerek sayfalamayı destekleyecek şekilde yapılandırın.

Ayrıca, seçili ürünleri silmek için Kullanıcı arabirimini de ekleyelim. GridView 'un altına bir düğme web denetimi ekleyin, `ID` seçili ürünleri silmek için `DeleteSelectedProducts` ve `Text` özelliğini olarak ayarlayarak. Gerçekten veritabanındaki ürünleri silmek yerine, bu örnekte yalnızca silinecek ürünleri belirten bir ileti görüntüleriz. Buna uyum sağlamak için düğmenin altına bir etiket Web denetimi ekleyin. KIMLIĞINI `DeleteResults`olarak ayarlayın, `Text` özelliğini temizleyin ve `Visible` ve `EnableViewState` özelliklerini `False`olarak ayarlayın.

Bu değişiklikleri yaptıktan sonra GridView, ObjectDataSource, düğme ve etiket bildirim temelli biçimlendirme, aşağıdakine benzer olmalıdır:

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample1.aspx)]

Sayfayı tarayıcıda görüntülemek için bir dakikanızı ayırın (bkz. Şekil 5). Bu noktada, ilk on ürünün adını, kategorisini ve fiyatını görmeniz gerekir.

[![Ilk on ürünün adı, kategorisi ve fiyatı listelenmiştir](adding-a-gridview-column-of-checkboxes-vb/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image9.png)

**Şekil 5**: Ilk on ürünün adı, kategorisi ve fiyatı listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image10.png))

## <a name="step-2-adding-a-column-of-checkboxes"></a>2\. Adım: onay kutularının bir sütununu ekleme

ASP.NET 2,0 bir CheckBoxField içerdiğinden, bir GridView öğesine CheckBox sütunu eklemek için kullanılabileceğini düşünebilir. Ne yazık ki, CheckBoxField bir Boolean veri alanıyla çalışacak şekilde tasarlandığından, bu durum değildir. Diğer bir deyişle, CheckBoxField ' ı kullanmak için, işlenmiş onay kutusunun işaretli olup olmadığını belirlemek için değeri bulunan temel alınan veri alanını belirtmemiz gerekir. CheckBoxField 'ı yalnızca Denetlenmemiş onay kutularının bir sütununu içerecek şekilde kullanmıyoruz.

Bunun yerine, bir TemplateField eklemesi ve `ItemTemplate`onay kutusu Web denetimi eklemeniz gerekir. Devam edin ve `Products` GridView 'a bir TemplateField ekleyin ve ilk (en soldaki) alanı yapın. GridView s akıllı etiketinde, şablonları düzenle bağlantısına tıklayın ve ardından araç kutusu Web denetimi ' nden `ItemTemplate`sürükleyin. Bu CheckBox s `ID` özelliğini `ProductSelector`olarak ayarlayın.

[![TemplateField s ItemTemplate 'e ProductSelector adlı bir CheckBox Web denetimi ekleyin](adding-a-gridview-column-of-checkboxes-vb/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image11.png)

**Şekil 6**: TemplateField s `ItemTemplate` `ProductSelector` adlı CheckBox Web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image12.png))

TemplateField ve CheckBox Web denetimi eklendiğinde, her satır artık bir onay kutusu içerir. Şekil 7 ' de, TemplateField ve onay kutusu eklendikten sonra bir tarayıcıdan görüntülendiklerinde Bu sayfa gösterilir.

[![her ürün satırına artık bir onay kutusu dahildir](adding-a-gridview-column-of-checkboxes-vb/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image13.png)

**Şekil 7**: her ürün satırı artık bir onay kutusu içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image14.png))

## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>3\. Adım: geri göndermede hangi onay kutularının denetlendiğini belirleme

Bu noktada, bir onay kutusu sütunudur, ancak geri göndermede hangi onay kutularının denetleneceğini belirlemenin bir yolu yoktur. Seçili ürünleri Sil düğmesine tıklandığında, bu ürünleri silmek için hangi onay kutularının denetlendiğini bilmeniz gerekir.

GridView s [`Rows` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx) , GridView 'daki veri satırlarına erişim sağlar. Bu satırlarda yineleyebilir, CheckBox denetimine programlı bir şekilde erişebilir ve sonra onay kutusunun seçili olup olmadığını anlamak için `Checked` özelliğine başvurabilirsiniz.

`DeleteSelectedProducts` Button Web Control s `Click` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample2.vb)]

`Rows` özelliği, GridView s veri satırlarını oluşturan `GridViewRow` örneklerinin bir koleksiyonunu döndürür. Buradaki `For Each` döngüsü bu koleksiyonu numaralandırır. Her `GridViewRow` nesnesi için, satır s onay kutusuna `row.FindControl("controlID")`kullanılarak programlı bir şekilde erişilir. Onay kutusu işaretliyse, satır s karşılık gelen `ProductID` değeri `DataKeys` koleksiyonundan alınır. Bu alıştırmada, `DeleteResults` etiketinde bilgilendirici bir ileti görüntüyoruz, bunun yerine, çalışan bir uygulamada, `ProductsBLL` sınıf s `DeleteProduct(productID)` yöntemine çağrı yapacağız.

Bu olay işleyicisinin eklenmesiyle, seçili ürünleri Sil düğmesine tıklamak artık seçili ürünlerin `ProductID` s ' ini gösterir.

[Seçilen ürünleri Sil düğmesine tıklandığında ![seçilen ürünlere tıklandı](adding-a-gridview-column-of-checkboxes-vb/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image15.png)

**Şekil 8**: Seçili ürünleri Sil düğmesine tıklandığında seçili ürünler `ProductID` s listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image16.png))

## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>4\. Adım: tümünü Işaretle ve tüm düğmelerin Işaretini kaldır

Bir Kullanıcı geçerli sayfadaki tüm ürünleri silmek isterse on onay kutularından her birini denetmaları gerekir. Tıklandığı zaman kılavuzdaki tüm onay kutularını seçen bir tümünü Işaretle düğmesi ekleyerek bu işlemin hızlandırıyoruz. Tüm Seçimleri Kaldır düğmesi eşit bir şekilde yararlı olacaktır.

Sayfaya iki düğme web denetimi ekleyin, GridView 'un üzerine yerleştirebilirsiniz. İlk tek s `ID` `CheckAll` ve `Text` özelliğini tümünü denetlemek için ayarlayın; ikinci bir s `ID` `UncheckAll` ve `Text` özelliğini tüm seçimini kaldırmak için ayarlayın.

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample3.aspx)]

Sonra, çağrıldığında `ToggleCheckState(checkState)` adlı arka plan kod sınıfında bir yöntem oluşturun, `Products` GridView s `Rows` koleksiyonunu numaralandırır ve her CheckBox s `Checked` özelliğini geçirilen *CheckState* parametresinin değerine ayarlar.

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample4.vb)]

Sonra, `CheckAll` ve `UncheckAll` düğmeleri için `Click` olay işleyicileri oluşturun. `CheckAll` s olay işleyicisinde, yalnızca `ToggleCheckState(True)`çağırın; `UncheckAll`' de, `ToggleCheckState(False)`çağırın.

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample5.vb)]

Bu kodla, tümünü Işaretle düğmesine tıklamak geri göndermeye neden olur ve GridView 'daki tüm onay kutularını kontrol eder. Benzer şekilde, Işaretini Kaldır ' a tıklamak tüm onay kutularının seçimini kaldırır. Şekil 9, tümünü denetle düğmesi işaretli olduktan sonra ekranı gösterir.

[Tümünü denetle düğmesine tıklamak ![tüm onay kutularını seçer](adding-a-gridview-column-of-checkboxes-vb/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image17.png)

**Şekil 9**: Tümünü işaretle düğmesine tıklamak tüm onay kutularını seçer ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-checkboxes-vb/_static/image18.png))

> [!NOTE]
> CheckBox sütununun bir sütununu görüntülerken, tüm onay kutularını seçmek veya seçmek için bir yaklaşım, üst bilgi satırındaki bir onay kutusu aracılığıyla yapılır. Üstelik, tüm uygulama için geçerli denetim/onay Işareti geri gönderme gerektirir. Onay kutuları, tam olarak istemci tarafı komut dosyası aracılığıyla denetlenebilir veya işaretlenmemiş olabilir, böylece bir snappier Kullanıcı deneyimi sağlar. Bir başlık satırı onay kutusunu tümünü Işaretle ve tüm ayrıntıları kaldır seçeneklerinin yanı sıra, istemci tarafı teknikleriyle ilgili bir tartışmayla birlikte, istemci tarafı [komut dosyası ve tümünü denetle onay kutularını kullanarak bir GridView 'Daki tüm onay kutularını](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)kontrol edin.

## <a name="summary"></a>Özet

Kullanıcıların devam etmeden önce GridView 'dan rastgele sayıda satır seçmesini sağlamak zorunda olduğu durumlarda, onay kutularının bir sütununu eklemek tek seçenektir. Bu öğreticide gördüğünüz gibi, GridView içindeki onay kutuları sütununu da içeren bir CheckBox Web denetimiyle TemplateField eklenmesi gerekir. Bir Web denetimi kullanarak (önceki öğreticide yaptığımız gibi, doğrudan şablonda ekleme biçimlendirme), ASP.NET hangi onay kutularının olduğunu ve geri gönderme sırasında denetlenmediğini otomatik olarak anımsar. Ayrıca, belirli bir onay kutusunun işaretli olup olmadığını ve denetlenen durumu değiştirmeyi öğrenmek için koddaki onay kutularına programlı bir şekilde erişebilirler.

Bu öğretici ve en son bir satır seçici sütununu GridView 'a eklemeyi incelemiştir. Bir sonraki öğreticimizde GridView 'a ekleme özelliği ekleyebilmemiz için bir iş sayesinde nasıl bir iş olduğunu inceleyeceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](adding-a-gridview-column-of-radio-buttons-vb.md)
> [İleri](inserting-a-new-record-from-the-gridview-s-footer-vb.md)
