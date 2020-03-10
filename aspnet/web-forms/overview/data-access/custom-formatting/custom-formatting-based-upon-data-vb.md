---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
title: Verileri temel alan özel biçimlendirme (VB) | Microsoft Docs
author: rick-anderson
description: GridView, DetailsView veya FormView 'un biçimini, kendisine bağlı verilere göre ayarlamak birden çok şekilde gerçekleştirilebilir. Bu öğreticide l...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: df5a1525-386f-4632-972c-57b199870bc3
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 268dc763ef6954903f721a3015daaf10bf9bccb1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78596714"
---
# <a name="custom-formatting-based-upon-data-vb"></a>Verileri Temel Alan Özel Biçimlendirme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe) veya [PDF 'yi indirin](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)

> GridView, DetailsView veya FormView 'un biçimini, kendisine bağlı verilere göre ayarlamak birden çok şekilde gerçekleştirilebilir. Bu öğreticide, veri bağlama biçimlendirmesinin veri sınırlama ve Rowtik olay işleyicilerinin kullanımı aracılığıyla nasıl gerçekleştirileceğini inceleyeceğiz.

## <a name="introduction"></a>Giriş

GridView, DetailsView ve FormView denetimlerinin görünümü, stille ilgili bir özellikler aracılığıyla özelleştirilebilir. `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`ve `Height`gibi özellikler, diğerleri arasında, işlenen denetimin genel görünümünü de dikte edin. `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`ve diğer özellikler de dahil olmak üzere, aynı stil ayarlarının belirli bölümlere uygulanmasını sağlar. Benzer şekilde, bu stil ayarları alan düzeyinde uygulanabilir.

Çoğu senaryoda, biçimlendirme gereksinimleri, görünen verilerin değerine bağlıdır. Örneğin, stok ürünlerinin dışına ilgi çekmek için ürün bilgilerini içeren bir rapor, `UnitsInStock` ve `UnitsOnOrder` alanları her ikisi de 0 ' a eşit olan ürünler için arka plan rengini sarı olarak ayarlayabilir. Daha pahalı ürünlerin vurgulanmasını sağlamak için bu ürünlerin fiyatlarını, kalın yazı tipinde $75,00 ' den fazla maliyetlendirmeye yönelik olarak göstermek isteyebilir.

GridView, DetailsView veya FormView 'un biçimini, kendisine bağlı verilere göre ayarlamak birden çok şekilde gerçekleştirilebilir. Bu öğreticide, `DataBound` ve `RowDataBound` olay işleyicilerini kullanarak veri bağlantılı biçimlendirmeyi nasıl gerçekleştireceğinizi inceleyeceğiz. Sonraki öğreticide, alternatif bir yaklaşım keşfedeceğiz.

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>DetailsView denetiminin`DataBound`olay Işleyicisini kullanma

Veriler bir DetailsView 'a bağlandığında, bir veri kaynağı denetiminden ya da denetimin `DataSource` özelliğine programlı olarak veri atayarak ve `DataBind()` metodunu çağırarak, aşağıdaki adım dizisi gerçekleşir:

1. Veri Web denetiminin `DataBinding` olayı ateşlenir.
2. Veriler veri Web denetimine bağlanır.
3. Veri Web denetiminin `DataBound` olayı ateşlenir.

Özel mantık, bir olay işleyicisi aracılığıyla 1 ve 3 adımından hemen sonra eklenebilir. `DataBound` olayı için bir olay işleyicisi oluşturarak, veri Web denetimine bağlanan verileri program aracılığıyla tespit edebilir ve biçimlendirmeyi gerektiği gibi ayarlayabilirsiniz. Bu durumda, bir ürünle ilgili genel bilgileri listelemek için bir DetailsView oluşturalım, ancak $75,00 ' i aşarsa ***kalın, italik yazı tipinde*** `UnitPrice` değeri görüntülenecektir.

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>1\. Adım: ürün bilgilerini bir DetailsView 'da görüntüleme

`CustomFormatting` klasöründeki `CustomColors.aspx` sayfasını açın, bir DetailsView denetimini araç kutusundan Tasarımcı üzerine sürükleyin, `ID` özellik değerini `ExpensiveProductsPriceInBoldItalic`olarak ayarlayın ve `ProductsBLL` sınıfının `GetProducts()` yöntemini çağıran yeni bir ObjectDataSource denetimine bağlayın. Bunu gerçekleştirmeye yönelik ayrıntılı adımlar, önceki öğreticilerde ayrıntılı olarak incelendiğimiz için burada gözardı edilir.

ObjectDataSource 'u DetailsView 'a bağladıktan sonra, alan listesini değiştirmek için bir dakikanızı ayırın. `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`ve `Discontinued` BoundFields alanlarını kaldırmayı ve kalan BoundFields alanlarını yeniden adlandırmasını kabul ediyorum. Ayrıca `Width` ve `Height` ayarlarını temizledi. DetailsView yalnızca tek bir kayıt görüntülediğinden, son kullanıcının tüm ürünleri görüntülemesine izin vermek için sayfalama 'yi etkinleştirmemiz gerekir. Bunu, DetailsView 'un akıllı etiketindeki sayfalama etkinleştir onay kutusunu işaretleyerek yapın.

[Şekil 1 ![: DetailsView 'un akıllı etiketinde sayfalama etkinleştir onay kutusunu Işaretleyin](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)

**Şekil 1**: Şekil 1: DetailsView 'un akıllı etiketindeki disk belleğini etkinleştir onay kutusunu işaretleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](custom-formatting-based-upon-data-vb/_static/image3.png))

Bu değişikliklerden sonra, DetailsView biçimlendirmesi şu şekilde olur:

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample1.aspx)]

Bu sayfayı tarayıcınızda test etmek için bir dakikanızı ayırın.

[DetailsView denetimi tek seferde bir ürün görüntülüyor ![](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)

**Şekil 2**: DetailsView denetimi aynı anda bir ürünü görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](custom-formatting-based-upon-data-vb/_static/image6.png))

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>2\. Adım: programlı olarak veri sınırlama olay Işleyicisindeki verilerin değerini belirleme

`UnitPrice` değeri $75,00 ' den fazla olan ürünler için kalın, italik yazı tipinde fiyat görüntülemek için, önce `UnitPrice` değerini programlı bir şekilde belirleyebilmemiz gerekir. DetailsView için, `DataBound` olay işleyicisinde bu gerçekleştirilebilir. Olay işleyicisini oluşturmak için tasarımcıda DetailsView öğesine tıklayıp Özellikler penceresi gidin. Bunu getirmek için F4 tuşuna basın, görünür değilse, Görünüm menüsüne gidin ve Özellikler penceresi menü seçeneğini belirleyin. Özellikler penceresi, diğer bir deyişle, DetailsView 'un olaylarını listelemek için şimşek simgesine tıklayın. Sonra, `DataBound` olayına çift tıklayın ya da oluşturmak istediğiniz olay işleyicisinin adını yazın.

![Veri bağlama olayı için bir olay Işleyicisi oluşturun](custom-formatting-based-upon-data-vb/_static/image7.png)

**Şekil 3**: `DataBound` olayı Için bir olay işleyicisi oluşturma

> [!NOTE]
> Ayrıca, ASP.NET sayfasının kod bölümünden bir olay işleyicisi de oluşturabilirsiniz. Sayfanın üst kısmında iki açılan liste bulacaksınız. Sol aşağı açılan listeden nesneyi ve sağ açılan listeden bir işleyici oluşturmak istediğiniz olayı seçin ve Visual Studio otomatik olarak uygun olay işleyicisini oluşturur.

Bunun yapılması olay işleyicisini otomatik olarak oluşturur ve sizi eklendiği kod bölümüne götürür. Bu noktada şunları göreceksiniz:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample2.vb)]

DetailsView 'a bağlantılı verilere `DataItem` özelliği aracılığıyla erişilebilir. Denetimlerimizi, kesin türü belirtilmiş bir DataRow örnekleri koleksiyonundan oluşan kesin türü belirtilmiş bir DataTable 'a bağlamamız gerektiğini geri çekin. DataTable, DetailsView 'a bağlandığında DataTable 'daki ilk DataRow, DetailsView 'un `DataItem` özelliğine atanır. Özellikle, `DataItem` özelliğine `DataRowView` bir nesne atanır. `DataRowView``Row` özelliğini, aslında `ProductsRow` bir örnek olan temel alınan DataRow nesnesine erişim sağlamak için kullanabiliriz. Bu `ProductsRow` örneğine sahip olduktan sonra, yalnızca nesnenin özellik değerlerini inceleyerek kararımızı yapabiliriz.

Aşağıdaki kod, DetailsView denetimine bağlanıp `UnitPrice` değerin $75,00 ' den büyük olup olmadığını nasıl belirleyeceğini göstermektedir:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample3.vb)]

> [!NOTE]
> `UnitPrice` veritabanında `NULL` bir değere sahip olduğundan, önce `ProductsRow``UnitPrice` özelliğine erişmeden önce bir `NULL` değeriyle ilgilentireceğiz emin olun. Bu denetim, `NULL` bir değere sahip olduğunda `UnitPrice` özelliğine erişmeye çalışdığımızda, `ProductsRow` nesnesinin bir [StrongTypingException özel durumu](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)oluşturması nedeniyle önemlidir.

## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>3\. Adım: DetailsView 'da BirimFiyat değerini biçimlendirme

Bu noktada, DetailsView 'a bağlı `UnitPrice` değerinin $75,00 ' ı aşan bir değere sahip olup olmadığını tespit edebiliyoruz, ancak henüz DetailsView 'un biçimlendirmesini uygun şekilde nasıl ayarlayabiliriz. DetailsView 'da bir satırın tamamına ilişkin biçimlendirmeyi değiştirmek için `DetailsViewID.Rows(index)`kullanarak satıra programlı bir şekilde erişin; belirli bir hücreyi değiştirmek için `DetailsViewID.Rows(index).Cells(index)`kullanın. Satır veya hücreye bir başvurduktan sonra, stili ilgili özelliklerini ayarlayarak görünümünü ayarlayabiliriz.

Bir satıra programlı bir şekilde erişmek için, 0 ' dan başlayan satırın dizinini bilmeniz gerekir. `UnitPrice` satır, DetailsView 'un dizinine bir dizin vererek ve `ExpensiveProductsPriceInBoldItalic.Rows(4)`kullanılarak programlı bir şekilde erişilebilir hale getirmek için kullanılan beşinci satırdır. Bu noktada, aşağıdaki kodu kullanarak tüm satırın içeriğinin kalın, italik yazı tipinde görüntülenmesini sağlayabilirsiniz:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample4.vb)]

Ancak bu, hem etiketi (fiyat) hem *de* kalın ve italik değerlerini yapar. Yalnızca kalın ve italik değerlerini yapmak istediğimiz takdirde, bu biçimlendirmeyi satırdaki ikinci hücreye uygulamanız gerekir ve bu biçimlendirme aşağıdakiler kullanılarak gerçekleştirilebilir:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample5.vb)]

Öğreticilerimiz, yukarıda gösterilen biçimlendirme ve stille ilgili bilgiler arasında temiz bir ayrım sağlamak için stil sayfaları kullandığından, yukarıda gösterildiği gibi belirli stil özelliklerini ayarlamak yerine bir CSS sınıfı kullanalım. `Styles.css` stil sayfasını açın ve aşağıdaki tanıma sahip `ExpensivePriceEmphasis` adlı yeni bir CSS sınıfı ekleyin:

[!code-css[Main](custom-formatting-based-upon-data-vb/samples/sample6.css)]

Ardından, `DataBound` olay işleyicisinde, hücrenin `CssClass` özelliğini `ExpensivePriceEmphasis`olarak ayarlayın. Aşağıdaki kod, `DataBound` olay işleyicisini tamamen gösterir:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample7.vb)]

$75,00 ' den küçük olan Chai 'yi görüntülerken, Fiyat normal bir yazı tipinde görüntülenir (bkz. Şekil 4). Bununla birlikte, $97,00 fiyatı bulunan mishi Koin NIU görüntülenirken, Fiyat kalın, italik yazı tipinde görüntülenir (bkz. Şekil 5).

[$75,00 ' den küçük ![fiyatlar normal bir yazı tipinde görüntülenir](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)

**Şekil 4**: $75,00 'den düşük fiyatlar normal bir yazı tipinde görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](custom-formatting-based-upon-data-vb/_static/image10.png))

[![pahalı ürünlerin fiyatları kalın, Italik yazı tipinde görüntülenir](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)

**Şekil 5**: pahalı ürünlerin fiyatları kalın, Italik yazı tipiyle görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](custom-formatting-based-upon-data-vb/_static/image13.png))

## <a name="using-the-formview-controlsdataboundevent-handler"></a>FormView denetiminin`DataBound`olay Işleyicisini kullanma

Bir FormView 'a göre temel alınan verileri belirleme adımları, bir DetailsView ile aynı `DataBound` bir olay işleyicisi oluşturur, `DataItem` özelliğini denetime göre uygun nesne türüne dönüştürmek ve devam etmek için kullanılır. FormView ve DetailsView, bununla birlikte farklılık gösterir, ancak kullanıcı arabiriminin görünümü nasıl güncelleştirilir.

FormView bir BoundFields içermiyor ve bu nedenle `Rows` koleksiyonu eksik. Bunun yerine, bir FormView statik HTML, Web denetimleri ve veri bağlama söz dizimi karışımı içerebilen şablonlardan oluşur. Bir FormView 'un stilini ayarlamak genellikle FormView 'un şablonlarındaki bir veya daha fazla Web denetiminin stilini ayarlamayı içerir.

Bunu göstermek için, önceki örnekteki gibi ürünleri listelemek üzere bir FormView kullanalım, ancak bu süre 10 ' dan küçük veya buna eşit bir kırmızı yazı tipiyle görüntülenen hisse senedi ile stoktaki birimleri yalnızca ürün adını ve birimleri görüntülerimize izin verir.

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>4\. Adım: ürün bilgilerini bir FormView 'da görüntüleme

DetailsView 'un altındaki `CustomColors.aspx` sayfasına bir FormView ekleyin ve `ID` özelliğini `LowStockedProductsInRed`olarak ayarlayın. FormView öğesini, önceki adımdan oluşturulan ObjectDataSource denetimine bağlayın. Bu, FormView için bir `ItemTemplate`, `EditItemTemplate`ve `InsertItemTemplate` oluşturur. `EditItemTemplate` ve `InsertItemTemplate` kaldırın ve `ItemTemplate`, her biri uygun şekilde adlandırılmış etiket denetimlerinde yalnızca `ProductName` ve `UnitsInStock` değerlerini içerecek şekilde kolaylaştırın. Önceki örnekteki DetailsView 'da olduğu gibi, FormView 'un akıllı etiketinde de sayfalama etkinleştir onay kutusunu işaretleyin.

Bu düzenlemeleriniz sonrasında, FormView 'un biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample8.aspx)]

`ItemTemplate` şunu içerdiğini unutmayın:

- **STATIK HTML** "Product:" ve "Stock Units:" metinleriyle birlikte `<br />` ve `<b>` öğeleri.
- **Web** , `ProductNameLabel` ve `UnitsInStockLabel`iki etiket denetimini denetler.
- **Veri bağlama söz dizimi** `<%# Bind("ProductName") %>` ve `<%# Bind("UnitsInStock") %>` söz dizimi, değerleri bu alanlardan etiket denetimleri ' `Text` özelliklerine atar.

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>5\. Adım: programlı olarak veri sınırlama olay Işleyicisindeki verilerin değerini belirleme

FormView 'un işaretlemesi tamamlanarak bir sonraki adım, `UnitsInStock` değerinin 10 ' dan küçük veya ona eşit olup olmadığını programlı bir şekilde belirlemektir. Bu, DetailsView ile aynı şekilde tam olarak gerçekleştirilir. FormView 'un `DataBound` olayı için bir olay işleyicisi oluşturarak başlayın.

![Veri bağlama olay Işleyicisini oluşturma](custom-formatting-based-upon-data-vb/_static/image14.png)

**Şekil 6**: `DataBound` olay işleyicisini oluşturma

Olay işleyicisinde, FormView 'un `DataItem` özelliğini bir `ProductsRow` örneğine atayın ve `UnitsInPrice` değerinin kırmızı bir yazı tipinde görüntülemesi gerekip gerekmediğini saptayın.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample9.vb)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>6\. Adım: FormView 'un ItemTemplate 'te UnitsInStockLabel etiketi denetimini biçimlendirme

Son adım, değeri 10 veya daha küçükse kırmızı bir yazı tipinde görüntülenecek `UnitsInStock` değerini biçimlendirmadır. Bunu gerçekleştirmek için, `ItemTemplate` `UnitsInStockLabel` denetimine programlı bir şekilde erişmesi ve onun stil özelliklerini metnin kırmızı renkte gösterilmesi için ayarlamanız gerekir. Şablondaki bir Web denetimine erişmek için aşağıdaki gibi `FindControl("controlID")` yöntemi kullanın:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample10.vb)]

Örneğimiz için `ID` değeri `UnitsInStockLabel`olan bir etiket denetimine erişmek istiyoruz, bu nedenle şunları kullanacağız:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample11.vb)]

Web denetimine programlı bir başvurduktan sonra, stille ilgili özellikleri gerektiği gibi değiştirebiliriz. Önceki örnekte olduğu gibi, `Styles.css` `LowUnitsInStockEmphasis`adlı bir CSS sınıfı oluşturduğdum. Bu stili etiket Web denetimine uygulamak için `CssClass` özelliğini uygun şekilde ayarlayın.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample12.vb)]

> [!NOTE]
> `FindControl("controlID")` kullanarak Web denetimine erişen bir şablonu biçimlendirme söz dizimi ve ardından stil ilişkili özellikleri ayarlamak, DetailsView veya GridView denetimlerinde [Templatefields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) kullanılırken de kullanılabilir. Sonraki öğreticimizde TemplateFields ' i inceleyeceğiz.

Şekil 7 ' den büyük bir ürün görüntülenirken, Şekil 8 ' deki ürünün değeri 10 ' dan daha düşük olduğunda, bu FormView, `UnitsInStock`.

[Stoğa yeterince büyük birimlere sahip ürünler Için ![özel biçimlendirme uygulanmaz](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)

**Şekil 7**: stokta yeterince büyük birimlere sahip ürünler Için özel biçimlendirme uygulanmaz ([tam boyutlu görüntüyü görüntülemek için tıklatın](custom-formatting-based-upon-data-vb/_static/image17.png))

[Hisse senedi numarası ![birimler, 10 veya daha az değere sahip olan ürünler için kırmızı renkte gösterilir](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)

**Şekil 8**: stok numarasında birimler, 10 veya daha az değere sahip ürünler için kırmızı renkle gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](custom-formatting-based-upon-data-vb/_static/image20.png))

## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>GridView 'un`RowDataBound`olayı ile biçimlendirme

Daha önce, DetailsView ve FormView 'un, veri bağlama sırasında ilerleme durumunu denetleme adımlarının sırasını inceliyoruz. Bu adımları bir kez Yenileyici olarak bir kez daha inceleyelim.

1. Veri Web denetiminin `DataBinding` olayı ateşlenir.
2. Veriler veri Web denetimine bağlanır.
3. Veri Web denetiminin `DataBound` olayı ateşlenir.

Bu üç basit adım, DetailsView ve FormView için yeterlidir çünkü yalnızca tek bir kayıt görüntüler. GridView için, buna (yalnızca ilki değil) ait *Tüm* kayıtları görüntüleyen GridView için adım 2 ' nin bir bit daha vardır.

2\. adımda GridView, veri kaynağını numaralandırır ve her kayıt için bir `GridViewRow` örneği oluşturur ve geçerli kaydı buna bağlar. GridView 'a eklenen her `GridViewRow` için iki olay oluşur:

- `GridViewRow` oluşturulduktan sonra **`RowCreated`** ateşlenir
- **`RowDataBound`** geçerli kayıt `GridViewRow`bağlandıktan sonra harekete geçirilir.

GridView için, veri bağlama aşağıdaki adım dizisiyle daha doğru şekilde açıklanmıştır:

1. GridView 'un `DataBinding` olayı ateşlenir.
2. Veriler GridView 'a bağlanır.   
  
   Veri kaynağındaki her kayıt için 

    1. `GridViewRow` nesnesi oluşturma
    2. `RowCreated` olayını harekete geçirme
    3. Kaydı `GridViewRow` bağlayın
    4. `RowDataBound` olayını harekete geçirme
    5. `GridViewRow` `Rows` koleksiyonuna ekleyin
3. GridView 'un `DataBound` olayı ateşlenir.

GridView 'un bireysel kayıtlarının biçimini özelleştirmek için, `RowDataBound` olayı için bir olay işleyicisi oluşturuyoruz. Bunu göstermek için, her bir ürünün adını, kategorisini ve fiyatını listeleyen `CustomColors.aspx` sayfasına, fiyatları sarı bir arka plan rengiyle $10,00 ' den küçük olan ürünleri vurgulayan bir GridView ekleyelim.

## <a name="step-7-displaying-product-information-in-a-gridview"></a>7\. Adım: ürün bilgilerini bir GridView 'da görüntüleme

Önceki örnekteki FormView 'un altına bir GridView ekleyin ve `ID` özelliğini `HighlightCheapProducts`olarak ayarlayın. Sayfadaki tüm ürünleri döndüren bir ObjectDataSource zaten var, GridView 'u bu sayfaya bağlayın. Son olarak, GridView 'un BoundFields alanlarını yalnızca ürünlerin adlarını, kategorilerini ve fiyatlarını içerecek şekilde düzenleyin. Bu düzenlemelerin ardından GridView 'un biçimlendirmesi şöyle görünmelidir:

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample13.aspx)]

Şekil 9 ' da bir tarayıcıdan görüntülendiklerinde bu noktaya yönelik ilerleme durumu gösterilmektedir.

[GridView ![her ürünün adını, kategorisini ve fiyatını listeler](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)

**Şekil 9**: GridView, her bir ürünün adını, kategorisini ve fiyatını listeler ([tam boyutlu görüntüyü görüntülemek için tıklatın](custom-formatting-based-upon-data-vb/_static/image23.png))

## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>8\. Adım: program aracılığıyla Rowveriye bağlı olay Işleyicisindeki verilerin değerini belirleme

`ProductsDataTable` GridView 'a bağlandığında `ProductsRow` örnekleri numaralandırılır ve her `ProductsRow` `GridViewRow` oluşturulur. `GridViewRow``DataItem` özelliği, GridView 'un `RowDataBound` olay işleyicisi oluşturulduktan sonra belirli `ProductRow`atanır. GridView 'a yönelik her ürünün `UnitPrice` değerini öğrenmek için, GridView 'un `RowDataBound` olayı için bir olay işleyicisi oluşturuyoruz. Bu olay işleyicisinde, geçerli `GridViewRow` `UnitPrice` değerini inceleyebilir ve bu satır için bir biçimlendirme kararı verebilir.

Bu olay işleyicisi, FormView ve DetailsView ile aynı adım serisi kullanılarak oluşturulabilir.

![GridView 'un Rowveriye bağlı olayı için bir olay Işleyicisi oluşturun](custom-formatting-based-upon-data-vb/_static/image24.png)

**Şekil 10**: GridView 'un `RowDataBound` olayı Için bir olay işleyicisi oluşturma

Olay işleyicisini bu şekilde oluşturmak, aşağıdaki kodun ASP.NET sayfasının kod bölümüne otomatik olarak eklenmesine neden olur:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample14.vb)]

`RowDataBound` olayı tetiklendiğinde, olay işleyicisi ikinci parametresi olarak, `Row`adında bir özelliği olan `GridViewRowEventArgs`türünde bir nesne olarak geçirilir. Bu özellik, yalnızca veri bağlanan `GridViewRow` bir başvuru döndürür. `GridViewRow` ile bağlantılı `ProductsRow` örneğine erişmek için `DataItem` özelliğini şu şekilde kullanıyoruz:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample15.vb)]

`RowDataBound` olay işleyicisiyle çalışırken, GridView 'un farklı tipte satırlardan oluştuğunu ve bu olayın *Tüm* satır türleri için tetiklendiğini aklınızda bulundurmanız önemlidir. `GridViewRow`türü `RowType` özelliği tarafından belirlenebilir ve olası değerlerden birine sahip olabilir:

- GridView 'un bir kaydına bağlanan bir satır `DataRow` `DataSource`
- GridView 'un `DataSource` boş olması durumunda gösterilecek satırı `EmptyDataRow`
- altbilgi satırını `Footer`; GridView 'un `ShowFooter` özelliği `True` olarak ayarlandıysa görüntülenir
- üst bilgi satırını `Header`; GridView 'ın Showwheader özelliği `True` olarak ayarlandıysa gösterilir (varsayılan)
- sayfalama arabirimini görüntüleyen satır, sayfalama uygulayan GridView için `Pager`
- `Separator` GridView için kullanılmaz, ancak DataList ve Repeater denetimleri için `RowType` özellikleri tarafından kullanılır, gelecek öğreticilerde ele alacağız iki veri Web denetimi

`EmptyDataRow`, `Header`, `Footer`ve `Pager` satırları `DataSource` kaydıyla ilişkili olmadığından, her zaman `Nothing` özellikleri için bir `DataItem` değeri olur. Bu nedenle, geçerli `GridViewRow``DataItem` özelliğiyle çalışmayı denemeden önce, önce bir `DataRow`ilgilentireceğiz emin olmanız gerekir. Bu, `GridViewRow``RowType` özelliği şöyle denetlenerek gerçekleştirilebilir:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample16.vb)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>9\. Adım: BirimFiyat değeri $10,00 ' den az olduğunda sarı satırı vurgulama

Son adım, söz konusu satırın `UnitPrice` değerinin $10,00 ' den küçük olması halinde tüm `GridViewRow` program aracılığıyla vurgulayacağız. GridView 'un satırlarına veya hücrelerine erişme söz dizimi, tüm satıra erişmek için `GridViewID.Rows(index)` DetailsView ile aynıdır, `GridViewID.Rows(index).Cells(index)` belirli bir hücreye erişin. Ancak `RowDataBound` olay işleyicisi veri bağlantılı `GridViewRow` ne zaman tetiklendiği zaman GridView 'un `Rows` koleksiyonuna eklenmemiştir. Bu nedenle, satır koleksiyonunu kullanarak `RowDataBound` olay işleyicisindeki geçerli `GridViewRow` örneğine erişemezsiniz.

`GridViewID.Rows(index)`yerine, `e.Row`kullanarak `RowDataBound` olay işleyicisindeki geçerli `GridViewRow` örneğe başvuracağız. Diğer bir deyişle, kullanacağımız `RowDataBound` olay işleyicisinden geçerli `GridViewRow` örneğini vurgulamak için:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample17.vb)]

`GridViewRow``BackColor` özelliğini doğrudan ayarlamak yerine CSS sınıflarının kullanılmasına bakalım. Arka plan rengini sarı olarak ayarlayan `AffordablePriceEmphasis` adlı bir CSS sınıfı oluşturdum. Tamamlanan `RowDataBound` olay işleyicisi aşağıdaki gibidir:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample18.vb)]

[En uygun maliyetli ürünlerin sarı vurgulanmış ![](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)

**Şekil 11**: en uygun maliyetli ürünler sarı renkle vurgulanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](custom-formatting-based-upon-data-vb/_static/image27.png))

## <a name="summary"></a>Özet

Bu öğreticide, denetime bağlı verilere göre GridView, DetailsView ve FormView biçimlerini nasıl biçimlentireceğiz. Bunu gerçekleştirmek için, temel alınan verilerin, gerektiğinde bir biçimlendirme değişikliğine göre inceedildiği `DataBound` veya `RowDataBound` olayları için bir olay işleyicisi oluşturduk. Bir DetailsView veya FormView 'a bağlantılı verilere erişmek için, `DataBound` olay işleyicisindeki `DataItem` özelliğini kullanıyoruz. GridView için, her bir `GridViewRow` örneğinin `DataItem` özelliği, `RowDataBound` olay işleyicisinde bulunan bu satıra bağlanan verileri içerir.

Veri Web denetiminin biçimlendirmesini programlı olarak ayarlamaya yönelik sözdizimi, Web denetimine ve biçimlendirilecek verilerin nasıl görüntüleneceğini gösterir. DetailsView ve GridView denetimlerinde, satırlara ve hücrelere bir sıralı dizin tarafından erişilebilir. Şablonlar kullanan FormView için `FindControl("controlID")` yöntemi genellikle şablon içinden bir Web denetimi bulmak için kullanılır.

Sonraki öğreticide, GridView ve DetailsView ile şablonları kullanma bölümüne bakacağız. Ayrıca, temel alınan verilere göre biçimlendirmeyi özelleştirmek için başka bir teknik de görüyoruz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler E.R. Gilmore, dennıs Patterson ve Ramiz Cager. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](displaying-summary-information-in-the-gridview-s-footer-cs.md)
> [İleri](using-templatefields-in-the-gridview-control-vb.md)
