---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
title: DetailsView denetiminde TemplateFields kullanma (VB) | Microsoft Docs
author: rick-anderson
description: GridView ile kullanılabilen aynı TemplateFields özellikleri, DetailsView denetimiyle de mevcuttur. Bu öğreticide bir ürün görüntüliyoruz...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0b91d5f8-127d-4f6a-b204-f2e2b35ef703
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
msc.type: authoredcontent
ms.openlocfilehash: e96f954c27ae1c8ccc18a9c40fe7e541b487c1cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78595587"
---
# <a name="using-templatefields-in-the-detailsview-control-vb"></a>DetailsView Denetiminde TemplateField Kullanma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_13_VB.exe) veya [PDF 'yi indirin](using-templatefields-in-the-detailsview-control-vb/_static/datatutorial13vb1.pdf)

> GridView ile kullanılabilen aynı TemplateFields özellikleri, DetailsView denetimiyle de mevcuttur. Bu öğreticide, TemplateFields içeren bir DetailsView kullanarak bir ürünü tek seferde görüntüleriz.

## <a name="introduction"></a>Giriş

TemplateField, verileri oluşturma sırasında BoundField, CheckBoxField, HyperLinkField ve diğer veri alanı denetimlerinden daha yüksek bir esneklik sunar. [Önceki öğreticide](using-templatefields-in-the-gridview-control-vb.md) , Için bir GridView 'Da TemplateField ' i kullanmayı inceledik:

- Birden çok veri alanı değerini tek bir sütunda görüntüleyin. Özellikle, `FirstName` ve `LastName` alanları tek bir GridView sütununda birleştirilmiştir.
- Veri alanı değerini ifade etmek için alternatif bir Web denetimi kullanın. Takvim denetimi kullanarak `HiredDate` değerinin nasıl gösterileceğini gördük.
- Temel alınan verileri temel alarak durum bilgilerini gösterir. `Employees` tablosu, bir çalışanın iş üzerinde bulunduğu gün sayısını döndüren bir sütun içermediğinden, bu bilgileri önceki öğreticide yer alan GridView örneğinde TemplateField ve biçimlendirme yöntemi kullanımıyla görüntüleyebiliyoruz.

GridView ile kullanılabilen aynı TemplateFields özellikleri, DetailsView denetimiyle de mevcuttur. Bu öğreticide, iki TemplateField içeren bir DetailsView kullanarak bir ürünü tek seferde görüntüleriz. İlk TemplateField, `UnitPrice`, `UnitsInStock`ve `UnitsOnOrder` veri alanlarını tek bir DetailsView satırında birleştirir. İkinci TemplateField, `Discontinued` alanının değerini görüntüler, ancak `Discontinued` `True`ve "Hayır" ise "Evet" i göstermek için bir biçimlendirme yöntemi kullanacaktır.

[Gösterimi özelleştirmek için Iki TemplateField ![kullanılır](using-templatefields-in-the-detailsview-control-vb/_static/image2.png)](using-templatefields-in-the-detailsview-control-vb/_static/image1.png)

**Şekil 1**: ekranı özelleştirmek Için Iki templatefields kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image3.png))

Haydi başlayın!

## <a name="step-1-binding-the-data-to-the-detailsview"></a>1\. Adım: verileri DetailsView 'a bağlama

Önceki öğreticide açıklandığı gibi, TemplateFields ile çalışırken, yalnızca BoundFields içeren DetailsView denetimi oluşturularak başlamak ve ardından yeni TemplateFields veya mevcut BoundFields alanlarını gerektiğinde TemplateFields 'e dönüştürmek daha kolay olur . Bu nedenle, tasarımcı aracılığıyla sayfaya bir DetailsView ekleyerek ve ürünlerin listesini döndüren bir ObjectDataSource 'a bağlayarak bu öğreticiyi başlatın. Bu adımlar, her bir ürünün Boole olmayan değer alanları ve bir Boole değeri alanı (Discontinued) için bir CheckBoxField içeren bir DetailsView oluşturacak.

`DetailsViewTemplateField.aspx` sayfasını açın ve araç kutusundan bir DetailsView öğesini tasarımcı üzerine sürükleyin. DetailsView 'un akıllı etiketiyle `ProductsBLL` sınıfın `GetProducts()` yöntemini çağıran yeni bir ObjectDataSource denetimi eklemeyi seçin.

[GetProducts () yöntemini çağıran yeni bir ObjectDataSource denetimi eklemek ![](using-templatefields-in-the-detailsview-control-vb/_static/image5.png)](using-templatefields-in-the-detailsview-control-vb/_static/image4.png)

**Şekil 2**: `GetProducts()` yöntemini çağıran yeni bir ObjectDataSource denetimi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image6.png))

Bu rapor için `ProductID`, `SupplierID`, `CategoryID`ve `ReorderLevel` BoundFields alanlarını kaldırın. Sonra, `CategoryName` ve `SupplierName` BoundFields `ProductName` BoundField öğesinden hemen sonra görünmesini sağlamak için BoundFields alanlarını yeniden sıralayın. Aynı gördüğünüz gibi, BoundFields için `HeaderText` özelliklerini ve biçimlendirme özelliklerini ayarlamayı ücretsiz hale gelmekten çekinmeyin. GridView ile benzer şekilde, bu BoundField düzey düzenlemeler alanlar iletişim kutusu aracılığıyla (DetailsView 'un akıllı etiketindeki alanları Düzenle bağlantısına tıklayarak erişilebilir) veya bildirime dayalı sözdizimi aracılığıyla gerçekleştirilebilir. Son `Width` `Height` olarak, DetailsView denetiminin, görüntülenecek verilere göre genişlemesine izin vermek ve akıllı etiketteki sayfalama etkinleştir onay kutusunu işaretleyin.

Bu değişiklikleri yaptıktan sonra, DetailsView denetiminizin bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample1.aspx)]

Sayfayı bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Bu noktada, ürünün adını, kategorisini, tedarikçisine, fiyatı, stoktaki birimleri, sırasıyla birimleri ve Discontinued durumunu gösteren satırlar içeren tek bir ürün (Chai) görmeniz gerekir.

[![bir dizi BoundFields kullanılarak ürünün ayrıntıları gösteriliyor](using-templatefields-in-the-detailsview-control-vb/_static/image8.png)](using-templatefields-in-the-detailsview-control-vb/_static/image7.png)

**Şekil 3**: ürünün ayrıntıları bir dizi Boundfields kullanılarak gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image9.png))

## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>2\. Adım: fiyatı, stoktaki birimleri ve sıralı birimleri tek bir satırda birleştirme

DetailsView `UnitPrice`, `UnitsInStock`ve `UnitsOnOrder` alanları için bir satıra sahiptir. Yeni bir TemplateField ekleyerek veya mevcut `UnitPrice`, `UnitsInStock`ve `UnitsOnOrder` BoundFields alanlarından birini TemplateField 'a dönüştürerek, bu veri alanlarını TemplateField ile tek bir satırda birleştirebiliriz. Var olan BoundFields 'i dönüştürmeyi kişisel olarak tercih ediyorum, yeni bir TemplateField ekleyerek alıştırma yapmanızı sağlar.

Alanlar iletişim kutusunu açmak için DetailsView 'un akıllı etiketindeki alanları Düzenle bağlantısına tıklayarak başlayın. Sonra, yeni bir TemplateField ekleyin ve `HeaderText` özelliğini "Price and Inventory" olarak ayarlayın ve yeni TemplateField ' ı `UnitPrice` BoundField ' ın üzerine yerleştirilmelidir.

[![DetailsView denetimine yeni bir TemplateField ekleyin](using-templatefields-in-the-detailsview-control-vb/_static/image11.png)](using-templatefields-in-the-detailsview-control-vb/_static/image10.png)

**Şekil 4**: DetailsView denetimine yeni bir TemplateField ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image12.png))

Bu yeni TemplateField, şu anda `UnitPrice`, `UnitsInStock`ve `UnitsOnOrder` BoundFields içinde görüntülenen değerleri içereceğinden, onları kaldıralım.

Bu adım için son görev, bu fiyat ve Inventory TemplateField için `ItemTemplate` işaretlemesini tanımlamak, bu, DetailsView 'un tasarımcıda şablon düzenlemesi aracılığıyla veya denetimin bildirim temelli söz dizimi aracılığıyla elde edilebilir. GridView 'da olduğu gibi, DetailsView 'un şablon düzenleme arabirimine akıllı etiketteki Şablonları Düzenle bağlantısına tıklanarak erişilebilir. Buradan, açılan listeden düzenlenecek şablonu seçebilir ve araç kutusundan herhangi bir Web denetimi ekleyebilirsiniz.

Bu öğreticide, Price ve Inventory TemplateField 'ın `ItemTemplate`bir etiket denetimi ekleyerek başlayın. Ardından, etiket Web denetiminin akıllı etiketindeki DataBindings bağlantısını düzenle bağlantısına tıklayın ve `Text` özelliğini `UnitPrice` alanına bağlayın.

[Etiketin text özelliğini UnitPrice veri alanına bağlama ![](using-templatefields-in-the-detailsview-control-vb/_static/image14.png)](using-templatefields-in-the-detailsview-control-vb/_static/image13.png)

**Şekil 5**: etiketin `Text` özelliğini `UnitPrice` Data alanına bağlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image15.png))

## <a name="formatting-the-price-as-a-currency"></a>Fiyatı para birimi olarak biçimlendirme

Bu ek olarak, Web denetim fiyatı ve Inventory TemplateField etiketi artık seçilen ürünün fiyatını görüntüler. Şekil 6 ' da, bir tarayıcıdan görüntülendiklerinde ilerimizin ekran görüntüsünü gösterir.

[![Price ve Inventory TemplateField, fiyatı gösterir](using-templatefields-in-the-detailsview-control-vb/_static/image17.png)](using-templatefields-in-the-detailsview-control-vb/_static/image16.png)

**Şekil 6**: Price ve Inventory TemplateField, fiyatı gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image18.png))

Ürünün fiyatı para birimi olarak biçimlendirmediğini unutmayın. Bir BoundField ile, `HtmlEncode` özelliği `False` ve `DataFormatString` özelliği `{0:formatSpecifier}`olarak ayarlanarak biçimlendirme mümkündür. Ancak, bir TemplateField için, veri bağlama sözdiziminde veya uygulamanın kodunda (ASP.NET sayfasının arka plan kod sınıfında olduğu gibi) tanımlanmış bir biçimlendirme yönteminin kullanımı aracılığıyla herhangi bir biçimlendirme yönergelerinin belirtilmesi gerekir.

Etiket Web denetiminde kullanılan veri bağlama söz dizimi için biçimlendirme belirtmek için, etiketin akıllı etiketindeki DataBindings 'i düzenle bağlantısına tıklayarak DataBindings iletişim kutusuna dönün. Biçimlendirme talimatlarını doğrudan biçim açılan listesine yazabilir veya tanımlı biçim dizelerinden birini seçebilirsiniz. BoundField 'un `DataFormatString` özelliği gibi, biçimlendirme `{0:formatSpecifier}`kullanılarak belirtilir.

`UnitPrice` alanı için, uygun aşağı açılan liste değerini seçerek veya `{0:C}` el ile yazarak belirtilen para birimi biçimlendirmesini kullanın.

[Fiyatı para birimi olarak Biçimlendir ![](using-templatefields-in-the-detailsview-control-vb/_static/image20.png)](using-templatefields-in-the-detailsview-control-vb/_static/image19.png)

**Şekil 7**: fiyatı para birimi olarak biçimlendirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image21.png))

Bildirimli olarak, biçimlendirme belirtimi `Bind` veya `Eval` yöntemlerine ikinci bir parametre olarak belirtilir. Tasarımcı aracılığıyla yapılan ayarlar, bildirim temelli biçimlendirmede aşağıdaki veri bağlama ifadesinde oluşur:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>Geri kalan veri alanları TemplateField 'a ekleniyor

Bu noktada, Price ve Inventory TemplateField alanındaki `UnitPrice` veri alanını görüntüleyip biçimlendirdik, ancak yine de `UnitsInStock` ve `UnitsOnOrder` alanlarını görüntülemesi gerekiyor. Bunları, fiyatın altındaki bir satırda ve parantez içinde gösterelim. Tasarımcıda şablon düzenlemesi arabiriminden, imlecinizin şablon içinde konumlandırılırken ve görüntülenecek metni yazarak bu tür biçimlendirme eklenebilir. Alternatif olarak, bu biçimlendirme doğrudan bildirime dayalı sözdizimine girilebilir.

Price ve Inventory TemplateField 'ın fiyat ve envanter bilgilerini şöyle görüntüleyeceği şekilde statik biçimlendirme, etiket Web denetimleri ve veri bağlama sözdizimini ekleyin:

*Fiyatı*  
(**Stok/sıra:** *unitsınstock* / *UnitsOnOrder*)

Bu görevi gerçekleştirdikten sonra, DetailsView 'un bildirime dayalı biçimlendirmesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample3.aspx)]

Bu değişikliklerle fiyat ve envanter bilgilerini tek bir DetailsView satırına birleştiriyoruz.

[![fiyat ve envanter bilgileri tek bir satırda görüntülenir](using-templatefields-in-the-detailsview-control-vb/_static/image23.png)](using-templatefields-in-the-detailsview-control-vb/_static/image22.png)

**Şekil 8**: fiyat ve envanter bilgileri tek bir satırda görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image24.png))

## <a name="step-3-customizing-the-discontinued-field-information"></a>3\. Adım: Discontinued alan bilgilerini özelleştirme

`Products` tablonun `Discontinued` sütunu, ürünün sonlandırılmadığını belirten bir bit değeridir. Bir DetailsView (veya GridView) bir veri kaynağı denetimine bağlarken, `Discontinued`gibi Boolean değer alanları CheckBoxFields olarak uygulanır, ancak `ProductID`, `ProductName`vb. gibi Boole olmayan değer alanları, BoundFields olarak uygulanır. CheckBoxField, veri alanının değeri true ise ve aksi takdirde işaretlenmediğinde işaretli devre dışı onay kutusu olarak işler.

Bunun yerine, ürünün sonlandırılmadığını belirten bir metin görüntülenmesini isteyebileceğiniz CheckBoxField 'ı göstermek yerine. Bunu gerçekleştirmek için, DetailsView ' dan CheckBoxField ' ı kaldırabilir ve sonra `DataField` özelliği `Discontinued`olarak ayarlanmış olan bir BoundField ekleyebilirsiniz. Bunu yapmak için bir dakikanızı ayırın. Bu değişiklikten sonra DetailsView, Discontinued ürünleri için "true" metnini ve hala etkin olan ürünler için "false" metnini gösterir.

[Doğru dizeleri ![ve Discontinued durumunu göstermek için false kullanılır](using-templatefields-in-the-detailsview-control-vb/_static/image26.png)](using-templatefields-in-the-detailsview-control-vb/_static/image25.png)

**Şekil 9**: doğru ve yanlış dizeleri, Discontinued durumunu görüntülemek için kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image27.png))

"True" veya "false" dizelerinin kullanılmasını belirttiğimiz, ancak bunun yerine "YES" ve "NO" gibi bir düşünün. Bu tür özelleştirmeler, bir TemplateField ve bir biçimlendirme yönteminin yardımıyla gerçekleştirilebilir. Biçimlendirme yöntemi herhangi bir sayıda giriş parametresini alabilir, ancak şablona eklemek için HTML (dize olarak) döndürmelidir.

Bir `Northwind.ProductsRow` nesnesini giriş parametresi olarak kabul eden ve bir dize döndüren `DetailsViewTemplateField.aspx` sayfanın arka plan kod sınıfı `DisplayDiscontinuedAsYESorNO` bir biçimlendirme yöntemi ekleyin. Önceki öğreticide anlatıldığı gibi, bu yöntemin şablondan erişilebilir olması için `Protected` veya `Public` olarak işaretlenmesi *gerekir* .

[!code-vb[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample4.vb)]

Bu yöntem, giriş parametresini (`discontinued`) denetler ve "Evet", "Hayır" ise "Evet `True`" döndürür.

> [!NOTE]
> Önceki öğreticide incelenen biçimlendirme yönteminde, `NULL` s içerebilen bir veri alanına geçirdiğimiz ve bu nedenle çalışanın `HiredDate` Özellik değerinin `EmployeesRow``HiredDate` özelliğine erişmeden önce bir veritabanı `NULL` değeri olup olmadığını kontrol etmek için gerekli olduğunu anımsayın. `Discontinued` sütununda hiçbir şekilde veritabanı `NULL` değerlerinin atanmayacağı için bu tür bir denetim gerekli değildir. Üstelik, yöntemin bir `ProductsRow` örneği veya `Object`türünde bir parametre kabul etmesi yerine bir Boole giriş parametresi kabul edebiliyor.

Bu biçimlendirme yöntemi tamamlandığına göre, hepsi TemplateField 'ın `ItemTemplate`çağırmalıdır. TemplateField 'ı oluşturmak için, `Discontinued` BoundField öğesini kaldırın ve yeni bir TemplateField ekleyin ya da `Discontinued` BoundField öğesini TemplateField olarak dönüştürün. Ardından, bildirim temelli biçimlendirme görünümünden TemplateField ' ı, geçerli `ProductRow` örneğinin `Discontinued` özelliğinin değerini geçirerek yalnızca `DisplayDiscontinuedAsYESorNO` yöntemini çağıran bir ItemTemplate 'i içerecek şekilde düzenleyin. Buna `Eval` yöntemi aracılığıyla erişilebilir. Özel olarak, TemplateField 'ın biçimlendirmesi şöyle görünmelidir:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample5.aspx)]

Bu, DetailsView işlenirken `DisplayDiscontinuedAsYESorNO` yönteminin çağrılmasına neden olur, `ProductRow` örneğinin `Discontinued` değeri geçer. `Eval` yöntemi `Object`türünde bir değer döndürdüğünden, ancak `DisplayDiscontinuedAsYESorNO` yöntemi `Boolean`türünde bir giriş parametresi beklediği için, `Eval` yöntemleri dönüş değeri değerini `Boolean`olarak atamalısınız. `DisplayDiscontinuedAsYESorNO` yöntemi, aldığı değere bağlı olarak "Evet" veya "Hayır" döndürür. Döndürülen değer bu DetailsView satırında görüntülenir (bkz. Şekil 10).

[![Evet veya artık Discontinued satırında HIÇBIR değer gösterilmemektedir](using-templatefields-in-the-detailsview-control-vb/_static/image29.png)](using-templatefields-in-the-detailsview-control-vb/_static/image28.png)

**Şekil 10**: Evet veya artık Discontinued satırında gösterilmemiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-detailsview-control-vb/_static/image30.png))

## <a name="summary"></a>Özet

DetailsView denetimindeki TemplateField, diğer alan denetimlerinde kullanılabilir olandan daha yüksek bir esneklik sağlar ve şu durumlarda idealdir:

- Birden çok veri alanının bir GridView sütununda gösterilmesi gerekir
- Veriler, düz metin yerine bir Web denetimi kullanılarak en iyi şekilde ifade edilir
- Çıktı, meta verileri görüntüleme veya verileri yeniden biçimlendirme gibi temel verilere bağlıdır

TemplateFields, DetailsView 'un temel aldığı verilerin görüntülenmesinde daha fazla esneklik kullanılmasına izin verirken, her bir alan bir HTML `<table>`satır olarak işlendiği için DetailsView çıktısı yine de bir bit boxy 'yi önemli ölçüde artırır.

FormView denetimi, işlenmiş çıktıyı yapılandırırken daha fazla esneklik sunar. FormView, alan içermez, ancak yalnızca bir dizi şablon (`ItemTemplate`, `EditItemTemplate`, `HeaderTemplate`vb.) içerir. Sonraki öğreticimizde, işlenmiş düzende daha fazla denetim elde etmek için FormView 'un nasıl kullanılacağını öğreneceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider, gözden geçirenle. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](using-templatefields-in-the-gridview-control-vb.md)
> [İleri](using-the-formview-s-templates-vb.md)
