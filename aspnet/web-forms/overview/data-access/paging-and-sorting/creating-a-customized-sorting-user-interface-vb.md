---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
title: Özelleştirilmiş sıralama Kullanıcı arabirimi oluşturma (VB) | Microsoft Docs
author: rick-anderson
description: Sıralanmış verilerin uzun bir listesini görüntülerken, ayırıcı satırlara bakarak ilgili verileri gruplamak çok faydalı olabilir. Bu öğreticide nasıl ye...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: f3897a74-cc6a-4032-8f68-465f155e296a
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 66127630560141cd795beb15f525a7fba85f3993
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607310"
---
# <a name="creating-a-customized-sorting-user-interface-vb"></a>Özelleştirilmiş Sıralama Kullanıcı Arabirimi Oluşturma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_VB.exe) veya [PDF 'yi indirin](creating-a-customized-sorting-user-interface-vb/_static/datatutorial27vb1.pdf)

> Sıralanmış verilerin uzun bir listesini görüntülerken, ayırıcı satırlara bakarak ilgili verileri gruplamak çok faydalı olabilir. Bu öğreticide, böyle bir sıralama Kullanıcı arabirimi oluşturma hakkında bilgi edineceksiniz.

## <a name="introduction"></a>Giriş

Sıralanmış sütunda yalnızca birkaç farklı değerin bulunduğu bir veri sıralanmış verilerin uzun bir listesini görüntülerken, Son Kullanıcı tam olarak fark sınırlarının meydana gelir. Örneğin, veritabanında 81 ürün vardır, ancak yalnızca dokuz farklı kategori seçeneği vardır (sekiz benzersiz kategori ve `NULL` seçeneği). Deniz yiyecek kategorisi kapsamında yer alan ürünleri incelemek isteyen bir kullanıcının durumunu göz önünde bulundurun. Tek bir GridView 'daki *Tüm* ürünleri listeleyen bir sayfadan, Kullanıcı en iyi sonuçları kategoriye göre sıralamak ve bu da tüm deniz yiyecek ürünlerini birlikte gruplamak için karar verebilir. Kategoriye göre sıraladıktan sonra, kullanıcının, deniz yiyecek tarafından gruplanmış ürünlerin nerede başlayıp bitebileceği konusunda arama yapması gerekir. Sonuçlar kategori adına göre alfabetik olarak sıralandığından, deniz yiyecek ürünlerini bulma zor değildir, ancak yine de kılavuzdaki öğelerin listesini yakından taramak istiyor.

Sıralanmış gruplar arasındaki sınırları vurgulamada yardımcı olması için birçok Web sitesi bu gruplar arasında bir ayırıcı ekleyen bir kullanıcı arabirimi sağlar. Şekil 1 ' de gösterilenler gibi ayırıcılar, bir kullanıcının belirli bir grubu daha hızlı bulmasına ve sınırlarını tanımlamasına olanak sağlar ve verilerde farklı grupların mevcut olduğunu belirlemektir.

[Her kategori grubu açıkça tanımlanmış ![](creating-a-customized-sorting-user-interface-vb/_static/image2.png)](creating-a-customized-sorting-user-interface-vb/_static/image1.png)

**Şekil 1**: her kategori grubu açıkça tanımlanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-customized-sorting-user-interface-vb/_static/image3.png))

Bu öğreticide, böyle bir sıralama Kullanıcı arabirimi oluşturma hakkında bilgi edineceksiniz.

## <a name="step-1-creating-a-standard-sortable-gridview"></a>1\. Adım: Standart, sıralanabilir bir GridView oluşturma

Gelişmiş sıralama arabirimini sağlamak için GridView 'un nasıl geliştiğini araştırmadan önce, ilk olarak ürünleri listeleyen standart, sıralanabilir bir GridView oluşturmaya izin verin. `PagingAndSorting` klasöründeki `CustomSortingUI.aspx` sayfasını açarak başlayın. Sayfaya bir GridView ekleyin, `ID` özelliğini `ProductList`olarak ayarlayın ve yeni bir ObjectDataSource 'a bağlayın. ObjectDataSource, kayıt seçmek için `ProductsBLL` sınıf s `GetProducts()` metodunu kullanacak şekilde yapılandırın.

Daha sonra, GridView 'u yalnızca `ProductName`, `CategoryName`, `SupplierName`ve `UnitPrice` BoundFields ve Discontinued CheckBoxField 'ı içermesi için yapılandırın. Son olarak, GridView 'u akıllı etiketteki sıralamayı etkinleştir onay kutusunu işaretleyerek (veya `AllowSorting` özelliğini `true`olarak ayarlayarak) sıralamayı destekleyecek şekilde yapılandırın. Bu eklemeleri `CustomSortingUI.aspx` sayfasına yaptıktan sonra, bildirime dayalı biçimlendirme aşağıdakine benzer şekilde görünmelidir:

[!code-aspx[Main](creating-a-customized-sorting-user-interface-vb/samples/sample1.aspx)]

Sürmekte olan ilerimizi bir tarayıcıda görüntülemek için bir dakikanızı ayırın. Şekil 2, verileri kategoriye göre alfabetik sırada sıralandığında sıralanabilir GridView 'ı gösterir.

[Sıralanabilir GridView s verileri kategoriye göre sıralanmıştır ![](creating-a-customized-sorting-user-interface-vb/_static/image5.png)](creating-a-customized-sorting-user-interface-vb/_static/image4.png)

**Şekil 2**: sıralanabilir GridView s verileri kategoriye göre sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-customized-sorting-user-interface-vb/_static/image6.png))

## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>2\. Adım: ayırıcı satırları ekleme tekniklerini keşfetme

Genel, sıralanabilir GridView tamamlandığına göre, her bir benzersiz sıralı gruptan önce GridView 'da ayırıcı satırları ekleyebileceksiniz. Ancak bu satırlar GridView 'a nasıl eklenebilir? Temel olarak, GridView s satırlarını yineliyoruz, sıralanan sütundaki değerler arasında farklılıkların nerede gerçekleşeceğini saptamalıdır ve ardından uygun ayırıcı satırı eklersiniz. Bu sorunu düşünürken, çözümün GridView s `RowDataBound` olay işleyicisinde bir yerde yer aldığı doğal görünür. Veri öğreticisini temel alan [özel biçimlendirme](../custom-formatting/custom-formatting-based-upon-data-vb.md) bölümünde anlatıldığı gibi, bu olay işleyicisi genellikle satır s verilerine göre satır düzeyinde biçimlendirme uygulanırken kullanılır. Ancak, bu olay işleyicisinden program aracılığıyla GridView 'a eklenemediğinden `RowDataBound` olay işleyicisi burada çözüm değildir. GridView s `Rows` koleksiyonu, aslında salt okunurdur.

GridView 'a ek satırlar eklemek için üç seçenek vardır:

- Bu meta veri ayırıcı satırlarını GridView 'a bağlanan gerçek verilere ekleyin
- GridView verileri bağladıktan sonra, GridView s denetim koleksiyonuna ek `TableRow` örnekleri ekleyin
- GridView denetimini genişleten ve GridView s yapısını oluşturmaktan sorumlu bu yöntemleri geçersiz kılan özel bir sunucu denetimi oluşturun

Bu işlevsellik birçok Web sayfasında veya birkaç Web sitesinde gerekliyse, özel sunucu denetimi oluşturmak en iyi yaklaşım olacaktır. Ancak, tam olarak bir kod ve GridView 'un iç işleyişi derinliklerinde tam bir keşif yapılır. Bu nedenle bu seçeneği bu öğreticide kabul eteceğiz.

Diğer iki seçenek de, GridView 'a bağlanacak gerçek verilere ayırıcı satırları ekleme ve GridView s denetim koleksiyonunu bağladıktan sonra düzenleme-bir tartışmayı farklı hale

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>GridView 'a bağlantılı verilere satır ekleme

GridView bir veri kaynağına bağlandığında, veri kaynağı tarafından döndürülen her kayıt için bir `GridViewRow` oluşturur. Bu nedenle, GridView 'a bağlamadan önce veri kaynağına ayırıcı kayıtlar ekleyerek gerekli ayırıcı satırları ekleyebiliriz. Şekil 3 ' te bu kavram gösterilmektedir.

![Bir teknik, veri kaynağına ayırıcı satırları eklemeyi Içerir](creating-a-customized-sorting-user-interface-vb/_static/image7.png)

**Şekil 3**: bir teknik, veri kaynağına ayırıcı satırları eklemeyi içerir

Özel bir ayırıcı kaydı olmadığından, ayırıcı kayıtları tırnak içinde kullanıyorum; Bunun yerine, veri kaynağındaki belirli bir kaydın normal bir veri satırı yerine bir ayırıcı görevi gören bir şekilde bayrak atamamız gerekir. Örneklerimizde, `ProductRows`oluşan GridView 'a `ProductsDataTable` bir örnek bağlamamız gerekir. `CategoryID` özelliğini `-1` olarak ayarlayarak (böyle bir değer normal olarak bulunmadığından) bir kaydı ayırıcı satır olarak bayrakla işaretliyoruz.

Bu tekniği kullanmak için aşağıdaki adımları gerçekleştirmeniz gerekir:

1. GridView 'a bağlanacak verileri program aracılığıyla alma (bir `ProductsDataTable` örneği)
2. GridView s `SortExpression` ve `SortDirection` özelliklerine göre verileri sıralayın
3. Sıralanmış sütundaki farkların nerede olduğunu arayarak `ProductsDataTable``ProductsRows` yineleyin
4. Her grup sınırında, DataTable 'a `ProductsRow` bir ayırıcı kaydı ekleyin, bu `CategoryID` `-1` olarak ayarlanmıştır (veya bir kaydı bir ayırıcı kayıt olarak işaretlemek için herhangi bir atama olduğuna karar verdi)
5. Ayırıcı satırları ekleme sonra programlı olarak verileri GridView 'a bağlayın

Bu beş adıma ek olarak, GridView s `RowDataBound` olayı için de bir olay işleyicisi sağlamanız gerekir. Burada her bir `DataRow` denetliyoruz ve `CategoryID` ayarı `-1`olan bir ayırıcı satır olup olmadığını saptadık. Öyleyse, büyük olasılıkla biçimini veya hücrede görüntülenecek metni ayarlamak istiyoruz.

Ekleme için bu tekniği kullanarak sıralama grubu sınırları, GridView s `Sorting` olayına bir olay işleyicisi sağlamanız ve `SortExpression` ve `SortDirection` değerlerinin izlenmesini sağlamak için yukarıda özetlenen bir daha fazla iş gerektirir.

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>GridView s denetim koleksiyonunu, veri sınırına geçtikten sonra düzenleme

GridView 'a bağlamadan önce verileri mesajlaşma yerine, veri GridView 'a *bağlandıktan sonra* ayırıcı satırları ekleyebiliriz. Veri bağlama işlemi, her biri bir hücre koleksiyonundan oluşan bir satır koleksiyonundan oluşan `Table` bir örnek olan GridView s denetim hiyerarşisini oluşturur. Özellikle, GridView s denetim koleksiyonu, kendi kökünde bir `Table` nesnesi, GridView öğesine göre `DataSource` her bir kayıt için bir `GridViewRow` (`TableRow` sınıfından türetilir) ve `TableCell` her veri alanı için her `GridViewRow` örneğindeki bir `DataSource`nesnesi içerir.

Her sıralama grubu arasına ayırıcı satırlar eklemek için, oluşturulduktan sonra bu denetim hiyerarşisini doğrudan işleyebiliriz. GridView s denetim hiyerarşisinin, sayfanın işlendiği zamana göre son kez oluşturulduğundan emin olabilirsiniz. Bu nedenle, bu yaklaşım `Page` sınıf s `Render` yöntemini geçersiz kılar, bu noktada GridView s son denetim hiyerarşisi gereken ayırıcı satırları içerecek şekilde güncelleştirilir. Şekil 4 ' te bu işlem gösterilmektedir.

[Alternatif bir tekniğe ![GridView s denetim hiyerarşisini yönetir](creating-a-customized-sorting-user-interface-vb/_static/image9.png)](creating-a-customized-sorting-user-interface-vb/_static/image8.png)

**Şekil 4**: alternatif bir teknik, GridView s denetim hiyerarşisini yönetir ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-a-customized-sorting-user-interface-vb/_static/image10.png))

Bu öğreticide, sıralama Kullanıcı deneyimini özelleştirmek için bu son yaklaşımı kullanacağız.

> [!NOTE]
> Bu öğreticide kullandığım kod, [Teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx) blog girişinde sunulan örneğe dayanır ve [GridView sıralama gruplandırmasına sahip bir bit yürütüyordu](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx).

## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>3\. Adım: GridView s denetim hiyerarşisine ayırıcı satırları ekleme

Yalnızca denetim hiyerarşisi oluşturulduktan ve bu sayfada son kez oluşturulduktan sonra yalnızca GridView s denetim hiyerarşisine ayırıcı satırları eklemek istiyoruz. bu ekleme işlemini sayfa yaşam döngüsünün sonuna, ancak gerçek GridView c 'den önce yapmak istiyoruz oncontrol hiyerarşisi HTML olarak işlendi. Bunu gerçekleştirebilmemiz mümkün olan en son nokta, aşağıdaki yöntem imzasını kullanarak arka plan kod sınıfında geçersiz kılabildikleri `Page` sınıf s `Render` olayıdır:

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample2.vb)]

`Page` sınıf özgün `Render` yöntemi çağrıldığında `base.Render(writer)` sayfadaki denetimlerin her biri işlenir ve bu da denetim hiyerarşisine göre biçimlendirme oluşturulur. Bu nedenle, her ikisi de `base.Render(writer)`çağırdığımızda, sayfanın işlenmesi ve GridView s denetim hiyerarşisini `base.Render(writer)`çağrılmadan önce işlememiz ve bu sayede, ayırıcı satırların, işlenmeden önce GridView s denetim hiyerarşisine eklenmesi gerekir.

Sıralama grubu üstbilgilerini eklemek için ilk olarak kullanıcının verilerin sıralanmasını istediğinden emin olmanız gerekir. Varsayılan olarak, GridView s içerikleri sıralanmaz ve bu nedenle herhangi bir grup sıralama üst bilgisi girmemiz gerekmez.

> [!NOTE]
> GridView 'un sayfa ilk yüklendiğinde belirli bir sütuna göre sıralanmasını istiyorsanız, ilk sayfada GridView s `Sort` yöntemini çağırın (sonraki geri göndermeler üzerinde değil). Bunu gerçekleştirmek için, bu çağrıyı bir `if (!Page.IsPostBack)` koşullu içindeki `Page_Load` olay işleyicisine ekleyin. `Sort` yöntemi hakkında daha fazla bilgi için [sayfalama ve rapor veri](paging-and-sorting-report-data-vb.md) öğreticisi bilgilerini sıralama bölümüne bakın.

Verilerin sıralandığı varsayılarak, bir sonraki göreviniz, verilerin hangi sütun tarafından sıralanacağını belirlemektir ve sonra bu sütun s değerlerinde farklılık gösteren satırları tarar. Aşağıdaki kod, verilerin sıralanmasını ve verilerin sıralandığı sütunu bulmasını sağlar:

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample3.vb)]

GridView henüz sıralanmışsa, GridView s `SortExpression` özelliği ayarlanmayacak. Bu nedenle, yalnızca bu özellikte bir değer varsa, ayırıcı satırları eklemek istiyoruz. Bunu yaparsanız, bir sonraki, verilerin sıralandığı sütunun dizinini belirlememiz gerekir. Bu, `SortExpression` özelliği GridView s `SortExpression` özelliğine eşit olan sütunu arayarak GridView s `Columns` koleksiyonu aracılığıyla gerçekleştirilir. Sütun s dizinine ek olarak, ayırıcı satırları görüntülerken kullanılan `HeaderText` özelliğini de sunuyoruz.

Verilerin sıralandığı sütunun diziniyle birlikte, son adım GridView 'un satırlarını numaralandırmalıdır. Her satır için, sıralanan sütun s değerinin, önceki satır sıralı sütun değerinden farklı olup olmadığını belirlememiz gerekir. Bu durumda, denetim hiyerarşisine yeni bir `GridViewRow` örneği ekleyebilmemiz gerekir. Bu, aşağıdaki kodla gerçekleştirilir:

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample4.vb)]

Bu kod, GridView s denetim hiyerarşisinin kökünde bulunan `Table` nesnesine programlı olarak başvurarak ve `lastValue`adlı bir dize değişkeni oluşturarak başlar. `lastValue`, sıradaki sütun değerini önceki satır ile karşılaştırmak için kullanılır. Ardından, GridView s `Rows` koleksiyonu numaralandırılır ve her satır için sıralanmış sütunun değeri `currentValue` değişkeninde depolanır.

> [!NOTE]
> Belirli bir satır sıralı sütun değerini öğrenmek için `Text` özelliğini kullanın. Bu, BoundFields için iyi çalışır, ancak TemplateFields, CheckBoxFields vb. için istendiği gibi çalışmayacaktır. Diğer GridView alanları için kısa süre içinde nasıl hesaba bakacağız.

`currentValue` ve `lastValue` değişkenleri karşılaştırılır. Farklıysa, denetim hiyerarşisine yeni bir ayırıcı satırı eklememiz gerekir. Bu, `Table` nesne s `Rows` koleksiyonundaki `GridViewRow` dizininin belirlenmesi, yeni `GridViewRow` ve `TableCell` örneklerin oluşturulması ve ardından `TableCell` ve `GridViewRow` denetim hiyerarşisine eklenmesi ile gerçekleştirilir.

`TableCell` ayırıcı satırı, GridView 'un tüm genişliğini kapsayacak şekilde biçimlendirilir, `SortHeaderRowStyle` CSS sınıfı kullanılarak biçimlendirilir ve hem sıralama grubu adını (kategori gibi) hem de grup s değerini (alkoller gibi) göstermek için `Text` özelliğine sahiptir. Son olarak, `lastValue` `currentValue`değerine güncellenir.

Sıralama grubu üst bilgi satırı `SortHeaderRowStyle` biçimlendirmek için kullanılan CSS sınıfı `Styles.css` dosyasında belirtilmelidir. Size her türlü stil ayarı kullanmayı ücretsiz olarak kullanabilirsiniz; Şunları kullandım:

[!code-css[Main](creating-a-customized-sorting-user-interface-vb/samples/sample5.css)]

Geçerli kodla sıralama arabirimi, herhangi bir BoundField tarafından sıralandığında sıralama grubu üst bilgilerini ekler (tedarikçiye göre sıralandığında bir ekran görüntüsü gösterir). Ancak, diğer herhangi bir alan türüne göre (örneğin, CheckBoxField veya TemplateField) sıralama yaparken, sıralama grubu üst bilgileri nerede bulunur (bkz. Şekil 6).

[Sıralama arabirimine ![, BoundFields 'e göre sıralarken sıralama grubu üst bilgilerini Içerir](creating-a-customized-sorting-user-interface-vb/_static/image12.png)](creating-a-customized-sorting-user-interface-vb/_static/image11.png)

**Şekil 5**: sıralama arabirimi, boundfields 'e göre sıralarken sıralama grubu üstbilgilerini içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-customized-sorting-user-interface-vb/_static/image13.png))

[CheckBoxField sıralanırken sıralama grubu üst bilgileri eksik ![](creating-a-customized-sorting-user-interface-vb/_static/image15.png)](creating-a-customized-sorting-user-interface-vb/_static/image14.png)

**Şekil 6**: bir CheckBoxField sıralanırken sıralama grubu başlıkları eksik ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-customized-sorting-user-interface-vb/_static/image16.png))

Bir CheckBoxField tarafından sıralandığında sıralama grubu üst bilgilerinin eksik olmasının nedeni, kodun Şu anda her satır için sıralanmış sütunun değerini belirlemede yalnızca `TableCell` s `Text` özelliğini kullanmalardır. CheckBoxFields için `TableCell` s `Text` özelliği boş bir dizedir; Bunun yerine, değer `TableCell` s `Controls` koleksiyonu içinde bulunan bir CheckBox Web denetimi aracılığıyla kullanılabilir.

BoundFields dışındaki alan türlerini işlemek için, `TableCell` s `Controls` koleksiyonundaki onay kutusunun varlığını denetlemek üzere `currentValue` değişkeninin atandığı kodu geliştirmemiz gerekir. `currentValue = gvr.Cells(sortColumnIndex).Text`kullanmak yerine, bu kodu aşağıdaki kodla değiştirin:

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample6.vb)]

Bu kod, `Controls` koleksiyonunda herhangi bir denetim olup olmadığını anlamak için geçerli satır için `TableCell` sıralanmış sütunu inceler. Varsa ve ilk denetim bir onay kutusu ise, CheckBox s `Checked` özelliğine bağlı olarak `currentValue` değişkeni Evet veya Hayır olarak ayarlanır. Aksi takdirde, değer `TableCell` s `Text` özelliğinden alınır. Bu mantık, GridView 'da mevcut olabilecek herhangi bir TemplateFields için sıralamayı işlemek üzere çoğaltılabilir.

Yukarıdaki kod ek olarak, sıralama grubu üstbilgileri artık Discontinued CheckBoxField tarafından sıralandığında mevcuttur (bkz. Şekil 7).

[![, bir CheckBoxField sıralanırken artık sıralama grubu üst bilgileri mevcuttur](creating-a-customized-sorting-user-interface-vb/_static/image18.png)](creating-a-customized-sorting-user-interface-vb/_static/image17.png)

**Şekil 7**: bir CheckBoxField sıralaması yaparken sıralama grubu üstbilgileri artık mevcuttur ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-customized-sorting-user-interface-vb/_static/image19.png))

> [!NOTE]
> `CategoryID`, `SupplierID`veya `UnitPrice` alanları için `NULL` veritabanı değerlerine sahip ürünleriniz varsa, bu değerler GridView 'da varsayılan olarak boş dizeler olarak görünür, yani bu ürünler için, `NULL` değerleri olan bu ürünlerin ayırıcı satır s metni kategori gibi okuyacaktır: (yani, kategoriden sonra hiçbir ad yok: iş kolları gibi). Burada bir değer görüntülenmesini istiyorsanız, BoundFields [`NullDisplayText` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx) görüntülenmesini istediğiniz metin olarak ayarlayabilir ya da `currentValue` ayırıcı satır s `Text` özelliğine atarken Render yöntemine bir koşullu ifade ekleyebilirsiniz.

## <a name="summary"></a>Özet

GridView sıralama arabirimini özelleştirmek için birçok yerleşik seçenek içermez. Ancak, düşük düzeyde bir kod ile, daha özelleştirilmiş bir arabirim oluşturmak için GridView s denetim hiyerarşisi ince ayar mümkündür. Bu öğreticide, farklı grupları ve bu grup sınırlarını daha kolay bir şekilde tanımlayan, sıralanabilir bir GridView için sıralama grubu ayırıcı satırı eklemeyi gördük. Özelleştirilmiş sıralama arabirimleri hakkında daha fazla örnek için, [Scott Guthrie](https://weblogs.asp.net/scottgu/) s ' nin [birkaç ASP.NET 2,0 GridView sıralama ipucu ve püf](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx) günlüğü girişini inceleyin.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Öncekini](sorting-custom-paged-data-vb.md)
