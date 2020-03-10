---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-vb
title: DataList denetimi ile satır başına birden çok kayıt gösteriliyor (VB) | Microsoft Docs
author: rick-anderson
description: Bu kısa öğreticide, DataList 'in düzeninin RepeatColumns ve RepeatDirection özellikleri aracılığıyla nasıl özelleştirileceğini keşfedeceğiz.
ms.author: riande
ms.date: 09/13/2006
ms.assetid: f555c531-bf33-4699-9987-42dbfef23c1f
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 17283dae192896fbaa48f1d7fe49afdbaf4c9a02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78611344"
---
# <a name="showing-multiple-records-per-row-with-the-datalist-control-vb"></a>DataList Denetimi ile Satır Başına Birden Çok Kayıt Gösterme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_VB.exe) veya [PDF 'yi indirin](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/datatutorial31vb1.pdf)

> Bu kısa öğreticide, DataList 'in düzeninin RepeatColumns ve RepeatDirection özellikleri aracılığıyla nasıl özelleştirileceğini keşfedeceğiz.

## <a name="introduction"></a>Giriş

Son iki öğreticilerde görtiğimiz DataList örnekleri, tek sütunlu HTML `<table>`bir satır olarak veri kaynağından her bir kaydı işlemiştir. Bu varsayılan DataList davranışından, veri kaynağı öğelerinin çok sütunlu, çok satırlı bir tabloya yayılması gibi DataList görüntüsünü özelleştirmek çok kolaydır. Üstelik, tüm veri kaynağı öğelerinin tek satırlık, çok sütunlu bir DataList 'te görüntülenmesini olanaklı hale gelir.

DataList s mizanpajını `RepeatColumns` ve `RepeatDirection` özellikleriyle özelleştirebiliriz, bu, sırasıyla kaç sütun oluşturulduğunu ve bu öğelerin dikey veya yatay olarak düzenlendiğini gösterir. Şekil 1, örneğin, ürün bilgilerini üç sütunlu bir tabloda görüntüleyen bir DataList gösterir.

[DataList ![her satır Için üç ürün gösterir](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image1.png)

**Şekil 1**: DataList, her satır Için üç ürün gösterir ([tam boyutlu görüntüyü görüntülemek için tıklatın](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image3.png))

Her satır için birden çok veri kaynağı öğesi göstererek DataList, yatay ekran alanını daha etkili bir şekilde kullanabilir. Bu kısa öğreticide, bu iki DataList özelliğini keşfedeceğiz.

## <a name="step-1-displaying-product-information-in-a-datalist"></a>1\. Adım: ürün bilgilerini bir DataList 'te görüntüleme

`RepeatColumns` ve `RepeatDirection` özelliklerini incelemeden önce, ilk olarak sayfamızda Standart tek sütunlu, çok satırlı Tablo düzeni kullanılarak ürün bilgilerini listeleyen bir DataList oluşturalım. Bu örnekte, aşağıdaki biçimlendirmeyi kullanarak s ürün adını, kategorisini ve fiyatını görüntüler.

[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-vb/samples/sample1.html)]

Önceki örneklerde bir DataList 'e veri bağlamayı gördük, bu nedenle bu adımları hızla taşıyacağım. `RepeatColumnAndDirection.aspx` sayfasını `DataListRepeaterBasics` klasöründen açıp araç kutusundan bir DataList ' ten tasarımcı üzerine sürükleyin. DataList s akıllı etiketinden yeni bir ObjectDataSource oluşturmayı ve bu uygulamayı `ProductsBLL` sınıf s `GetProducts` yönteminden verileri çekmesini ve sihirbazın s ekleme, GÜNCELLEŞTIRME ve SILME sekmelerinden (None) seçeneğini seçmeyi tercih edin.

Yeni ObjectDataSource 'u oluşturup DataList 'e bağladıktan sonra Visual Studio otomatik olarak her bir ürün verileri alanının adını ve değerini görüntüleyen bir `ItemTemplate` oluşturur. `Text` özelliklerine değer atamak için uygun veri bağlama söz dizimini kullanan etiket denetimleriyle, *ürün adı*, *Kategori adı*ve *Fiyat* metni ' ni kullanarak doğrudan bildirim temelli biçimlendirme veya şablon düzenleme seçeneğinden `ItemTemplate` ayarlayın. `ItemTemplate`güncelleştirildikten sonra, sayfa için bildirim temelli biçimlendirmenin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-vb/samples/sample2.aspx)]

`UnitPrice`için `Eval` veri bağlama söz dizimine bir Biçim belirleyicisi dahil etdin ve döndürülen değeri para birimi olarak biçimlendirdim `Eval("UnitPrice", "{0:C}").`

Bir tarayıcıda sayfanızı ziyaret etmek için bir dakikanızı ayırın. Şekil 2 ' de gösterildiği gibi, DataList tek sütunlu, çok satırlı bir ürün tablosu olarak işlenir.

[Varsayılan olarak, DataList tek sütunlu, çok satırlı bir tablo olarak Işler ![](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image4.png)

**Şekil 2**: varsayılan olarak, DataList tek sütunlu, çok satırlı bir tablo olarak işlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image6.png))

## <a name="step-2-changing-the-datalist-s-layout-direction"></a>2\. Adım: DataList s düzen yönünü değiştirme

DataList için varsayılan davranış, öğelerini tek sütunlu, çok satırlı bir tabloda dikey olarak düzenlerken, bu davranış DataList s [`RepeatDirection` özelliği](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)aracılığıyla kolayca değiştirilebilir. `RepeatDirection` özelliği iki olası değerden birini kabul edebilir: `Horizontal` veya `Vertical` (varsayılan).

`RepeatDirection` özelliğini `Vertical` `Horizontal`olarak değiştirerek, DataList, kayıtlarını tek bir satırda işler ve veri kaynağı öğesi başına bir sütun oluşturur. Bu etkiyi göstermek için, tasarımcıda DataList ' e tıklayın ve ardından Özellikler penceresi `RepeatDirection` özelliğini `Vertical` ' den `Horizontal`olarak değiştirin. Böylece tasarımcı, DataList s yerleşimini ayarlar, tek satırlı, çok sütunlu bir arabirim oluşturur (bkz. Şekil 3).

[RepeatDirection özelliği ![, DataList öğelerinin nasıl düzenlendiğini belirler](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image7.png)

**Şekil 3**: `RepeatDirection` özelliği, DataList öğelerinin nasıl düzenlendiğini belirler ([tam boyutlu görüntüyü görüntülemek için tıklayın](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image9.png))

Küçük miktarlarda veri görüntülerken, tek satırlık, çok sütunlu bir tablo, ekranın gerçek durumunu en üst düzeye çıkarmak için ideal bir yol olabilir. Ancak, daha büyük hacimler için, tek bir satır çok sayıda sütun gerektirir, bu da bu öğeleri ekranda ekranın sağına sığdırabilecek şekilde gönderir. Şekil 4 ' te, tek satırlık bir DataList 'te işlendiğinde ürünler gösterilmektedir. Birçok ürün (80 ' den fazla) olduğundan, her bir ürün hakkındaki bilgileri görüntülemek için kullanıcının en sağa kaydırmasına sahip olması gerekir.

[Çok büyük veri kaynakları Için ![DataList, tek bir sütun olarak yatay kaydırma gerektirir](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image10.png)

**Şekil 4**: yeterince büyük veri kaynakları için tek bir DataList sütunu yatay kaydırma gerektirir ([tam boyutlu görüntüyü görüntülemek için tıklayın](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image12.png))

## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>3\. Adım: verileri çok sütunlu, çok satırlı bir tabloda görüntüleme

Çok sütunlu, çok satırlı bir DataList oluşturmak için [`RepeatColumns` özelliğini](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx) görüntülenecek sütun sayısına ayarlamanız gerekir. Varsayılan olarak, `RepeatColumns` özelliği 0 olarak ayarlanır; Bu, DataList 'in tüm öğelerini tek bir satırda veya sütunda (`RepeatDirection` özelliğinin değerine bağlı olarak) görüntülemesine neden olur.

Örneğimizde, her tablo satırı için üç ürün gösterelim. Bu nedenle, `RepeatColumns` özelliğini 3 olarak ayarlayın. Bu değişikliği yaptıktan sonra sonuçları bir tarayıcıda görüntülemek için bir dakikanızı ayırın. Şekil 5 ' i gösterdiği gibi, ürünler artık üç sütunlu, çok satırlı bir tabloda listelenir.

[her satır için ![üç ürün görüntülenir](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image13.png)

**Şekil 5**: her satır Için üç ürün görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image15.png))

`RepeatDirection` özelliği, DataList 'teki öğelerin nasıl düzenlendiğini etkiler. Şekil 5 ' te `RepeatDirection` özelliği `Horizontal`olarak ayarlanan sonuçlar gösterilmektedir. İlk üç ürünün Chai, Chang ve Aniseed Syrup 'un soldan sağa ve yukarıdan aşağıya doğru düzenlendiğini unutmayın. Sonraki üç ürün (Chef Anton s Cajun mevsimlik ile başlayarak) ilk üçü altında bir satırda görüntülenir. `RepeatDirection` özelliğini `Vertical`olarak değiştirme, ancak Şekil 6 ' da gösterildiği gibi, bu ürünleri yukarıdan aşağıya doğru olarak düzenler.

[Burada ![, ürünler dikey olarak düzenlenir](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image16.png)

**Şekil 6**: burada, ürünler dikey olarak düzenlenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image18.png))

Elde edilen tabloda görüntülenecek satır sayısı, DataList 'e bağlı toplam kayıt sayısına bağlıdır. Tam olarak, veri kaynağı öğelerinin toplam sayısının `RepeatColumns` Özellik değeri tarafından bölünen üst öğesi. `Products` tabloda Şu anda 84 ürün olduğundan, bu, 3 ' ü bölünebilen 28 satır vardır. Veri kaynağındaki öğe sayısı ve `RepeatColumns` Özellik değeri bölünemez ise, son satır veya sütunda boş hücreler olur. `RepeatDirection` `Vertical`olarak ayarlanırsa, son sütunda boş hücreler olacaktır; `RepeatDirection` `Horizontal`, son satırda boş hücreler olur.

## <a name="summary"></a>Özet

DataList, varsayılan olarak öğelerini tek sütunlu, çok satırlı bir tabloda listeler ve tek bir TemplateField içeren bir GridView 'un düzenine sahiptir. Bu varsayılan düzen kabul edilebilir olsa da, satır başına birden çok veri kaynağı öğesi görüntüleyerek ekran ile gerçek zamanlı olarak en üst düzeye çıkarabilirsiniz. Bunu yapmak, DataList s `RepeatColumns` özelliğini her satır için görüntülenecek sütun sayısıyla ayarlamanın bir önemi olur. Ayrıca, DataList s `RepeatDirection` özelliği, çok sütunlu, çok satırlı tablo içeriğinin yatay olarak soldan sağa, yukarıdan aşağıya veya dikey olarak yukarıdan aşağıya doğru bir şekilde düzenlenip düzenlenmeyeceğini belirtmek için kullanılabilir.

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider olarak gözden geçiren John suru idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
> [İleri](nested-data-web-controls-vb.md)
