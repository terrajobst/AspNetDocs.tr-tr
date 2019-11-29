---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
title: DataList ve Repeater 'ı verileri temel alarak biçimlendirme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, ile biçimlendirme işlevleri kullanarak DataList ve Repeater denetimlerinin görünümünü nasıl biçimlendirdiğimiz hakkında örnek adım adım göstereceğiz...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 83e3d759-82b8-41e6-8d62-f0f4b3edec41
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 68de3450ed97fc7bd0efb27e089d9db8e3e85fb0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633193"
---
# <a name="formatting-the-datalist-and-repeater-based-upon-data-c"></a>DataList ve Repeater’ı Verileri Temel Alarak Biçimlendirme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_CS.exe) veya [PDF 'yi indirin](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/datatutorial30cs1.pdf)

> Bu öğreticide, şablonlar içindeki biçimlendirme işlevlerini kullanarak ya da veri bağlama olayını işleyerek DataList ve Repeater denetimlerinin görünümünü nasıl biçimlendirdiğimiz hakkında örnekler bulacaksınız.

## <a name="introduction"></a>Giriş

Önceki öğreticide gördüğünüz gibi DataList, görünümünü etkileyen bir dizi stille ilgili özellik sunar. Özellikle, DataList s `HeaderStyle`, `ItemStyle`, `AlternatingItemStyle`ve `SelectedItemStyle` özelliklerine varsayılan CSS sınıflarının nasıl atanacağını gördük. Bu dört özelliğe ek olarak, DataList `Font`, `ForeColor`, `BackColor`ve `BorderWidth`gibi diğer stille ilgili birçok özelliği içerir. Yineleyici denetimi stille ilgili herhangi bir özellik içermiyor. Bu tür stil ayarları, yineleyici s şablonlarındaki biçimlendirme dahilinde doğrudan yapılmalıdır.

Genellikle, verilerin biçimlendirilmesi, verilerin kendine bağlıdır. Örneğin, ürünler listelenirken, ürün bilgilerini açık gri yazı tipi renginde göstermek isteyebilir veya sıfır ise `UnitsInStock` değerini vurgulamak isteyebilirsiniz. Önceki öğreticilerde gördüğünüz gibi, GridView, DetailsView ve FormView, görünümlerini verilerine göre biçimlendirmek için iki farklı yol sunar:

- **`DataBound` olay** , veriler her bir öğeye bağlandıktan sonra tetiklenen uygun `DataBound` olayı için bir olay işleyicisi oluşturur (GridView için `RowDataBound` olayıdır; DataList ve Repeater için `ItemDataBound` olayıdır). Bu olay işleyicisinde, yalnızca bağlanan veriler incelenir ve yapılan kararlar değiştirilebilir. Bu tekniği, veri öğreticisine [göre özel biçimlendirme](../custom-formatting/custom-formatting-based-upon-data-cs.md) içinde inceledik.
- **Şablonlarındaki işlevleri** , DetailsView veya GridView denetimlerinde templatefields kullanırken veya FormView denetimindeki bir şablonda biçimlendirmek için, ASP.net Page s Code-Behind sınıfına, Iş mantığı katmanına veya Web uygulamasından erişilebilen herhangi bir sınıf kitaplığına biçimlendirme işlevi ekleyebiliriz. Bu biçimlendirme işlevi rastgele sayıda giriş parametresini kabul edebilir, ancak şablonda işlenecek HTML 'yi döndürmelidir. Biçimlendirme işlevleri ilk olarak [GridView denetim öğreticisindeki TemplateFields kullanılarak](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) incelendi.

Bu biçimlendirme tekniklerinin her ikisi de DataList ve Repeater denetimleri ile kullanılabilir. Bu öğreticide her iki denetim için de her iki tekniği kullanan örneklerde adım adım ilerleriz.

## <a name="using-theitemdataboundevent-handler"></a>`ItemDataBound`olay Işleyicisini kullanma

Veriler bir DataList 'e bağlandığında, bir veri kaynağı denetiminden ya da denetim s `DataSource` özelliğine veri atayarak ve `DataBind()` metodunu çağırarak, DataList s `DataBinding` olayı ateşlenir, numaralandırılan veri kaynağı ve her veri kaydı DataList 'e bağlanır. Veri kaynağındaki her kayıt için DataList, geçerli kayda bağlanan bir [`DataListItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.aspx) nesnesi oluşturur. Bu işlem sırasında, DataList iki olay oluşturur:

- `DataListItem` oluşturulduktan sonra **`ItemCreated`** ateşlenir
- **`ItemDataBound`** geçerli kayıt `DataListItem` bağlandıktan sonra ateşlenir

Aşağıdaki adımlarda, DataList denetimi için veri bağlama işlemi ana hatlarıyla verilmiştir.

1. DataList s [`DataBinding` olayı](https://msdn.microsoft.com/library/system.web.ui.control.databinding.aspx) ateşlenir
2. Veriler DataList 'e bağlanır  
  
   Veri kaynağındaki her kayıt için 

    1. `DataListItem` nesnesi oluşturma
    2. [`ItemCreated` olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemcreated.aspx) harekete geçirme
    3. Kaydı `DataListItem` bağlayın
    4. [`ItemDataBound` olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx) harekete geçirme
    5. `DataListItem` `Items` koleksiyonuna ekleyin

Yineleyici denetimine veri bağlarken, tam olarak aynı adım dizisi üzerinden ilerler. Tek fark, `DataListItem` örnekleri oluşturulması yerine Repeater 'ın [`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)s kullanır.

> [!NOTE]
> Kurnaz okuyucusu, GridView 'un verilere bağlanması halinde DataList ve Repeater verileri veriye bağlandığında, transpire olan adım sırası arasında hafif bir anomali olduğunu fark etmiş olabilir. Veri bağlama işleminin kuyruk sonunda, GridView `DataBound` olayını oluşturur; Ancak, DataList veya Repeater denetiminin böyle bir olayı yoktur. Bunun nedeni, DataList ve Repeater denetimlerinin, ön ve son düzey olay işleyicisi deseninin ortak hale gelmesi için ASP.NET 1. x zaman diliminde yeniden oluşturulmuş olmasından kaynaklanır.

GridView ile tıpkı, verileri temel alan biçimlendirme için bir seçenek, `ItemDataBound` olayı için bir olay işleyicisi oluşturmaktır. Bu olay işleyicisi, `DataListItem` veya `RepeaterItem` daha önce bağlanan verileri inceleyebilir ve denetimin biçimlendirmesini gerektiği şekilde etkiler.

DataList denetimi için tüm öğe için biçimlendirme değişiklikleri, standart `Font`, `ForeColor`, `BackColor`, `CssClass`vb. dahil olmak üzere `DataListItem` s stiliyle ilgili özellikler kullanılarak uygulanabilir. DataList s şablonundaki belirli Web denetimlerinin biçimlendirmesini etkilemek için, bu Web denetimlerinin stilini programlı bir şekilde erişmesi ve bunları değiştirmesi gerekir. Bu geri alma, veri öğreticisine *göre özel biçimlendirme* içinde nasıl gerçekleştirileceğini gördük. Yineleyici denetimi gibi, `RepeaterItem` sınıfında stille ilgili özellikler yoktur; Bu nedenle, `ItemDataBound` olay işleyicisindeki bir `RepeaterItem` yapılan tüm stille ilgili değişiklikler, programlı olarak şablon içindeki Web denetimlerine erişerek ve güncelleştirerek yapılmalıdır.

DataList ve Repeater 'ın `ItemDataBound` biçimlendirme tekniği neredeyse aynı olduğundan, örneğimiz DataList 'i kullanmaya odaklanacaktır.

## <a name="step-1-displaying-product-information-in-the-datalist"></a>1\. Adım: ürün bilgilerini DataList 'te görüntüleme

Biçimlendirme hakkında kaygılanmadan önce, ilk olarak ürün bilgilerini göstermek için DataList kullanan bir sayfa oluşturalım. [Önceki öğreticide](displaying-data-with-the-datalist-and-repeater-controls-cs.md) , `ItemTemplate` her ürünün adı, kategorisi, tedarikçisini, birim başına miktarı ve fiyatı Içeren bir DataList oluşturduk. Bu öğreticide bu işlevselliği tekrarlamasına izin verin. Bunu gerçekleştirmek için, DataList ve ObjectDataSource 'u sıfırdan yeniden oluşturabilir ya da bu denetimleri önceki öğreticide oluşturulan sayfadan (`Basics.aspx`) kopyalayabilir ve Bu öğreticinin sayfasına yapıştırabilirsiniz (`Formatting.aspx`).

DataList ve ObjectDataSource işlevlerini `Basics.aspx` `Formatting.aspx`' den çoğaltdıktan sonra, DataList s `ID` özelliğini `DataList1` ' den daha açıklayıcı bir `ItemDataBoundFormattingExample`değiştirmek için bir dakikanızı ayırın. Sonra, DataList 'i bir tarayıcıda görüntüleyin. Şekil 1 ' de gösterildiği gibi, her ürün arasındaki tek biçimlendirme farkı, arka plan renginin farklı olduğundan emin olur.

[![, DataList denetiminde listelenen ürünler](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image1.png)

**Şekil 1**: Ürünler DataList denetiminde listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image3.png))

Bu öğreticide, bir fiyata $20,00 ' dan düşük bir fiyata sahip olan tüm ürünlerin hem adı hem de birim fiyatı sarıya sahip olacağı şekilde DataList 'i biçimlendirmeye izin verin.

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>2\. Adım: program aracılığıyla ıtemveriye bağlı olay Işleyicisindeki verilerin değerini belirleme

Yalnızca $20,00 altında bir fiyata sahip olan ürünlere özel biçimlendirme uygulanmadığından, her ürün fiyatını belirleyebilmelidir. DataList 'e veri bağlarken DataList, veri kaynağındaki kayıtları numaralandırır ve her kayıt için, veri kaynağı kaydını `DataListItem`bağlayan bir `DataListItem` örneği oluşturur. Belirli kayıt s verileri geçerli `DataListItem` nesnesine bağladıktan sonra, DataList s `ItemDataBound` olayı tetiklenir. Bu olay için geçerli `DataListItem` veri değerlerini incelemek üzere bir olay işleyicisi oluşturabilir ve bu değerlere bağlı olarak, gereken biçimlendirme değişikliklerini yapabilirsiniz.

DataList için `ItemDataBound` bir olay oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample1.cs)]

DataList `ItemDataBound` olay işleyicisi 'nin arkasındaki kavram ve anlambilim, veri öğreticisine *bağlı olarak özel biçimlendirme* içindeki GridView s `RowDataBound` olay işleyicisi tarafından kullanılanlarla aynı olsa da, söz dizimi biraz farklılık gösterir. `ItemDataBound` olayı tetiklendiğinde, verilere yalnızca `DataListItem` bağlantılı olan `e.Item`, GridView s `RowDataBound` olay işleyicisi ile olduğu gibi `e.Row`yerine, ilgili olay işleyicisine geçirilir. DataList ' `ItemDataBound` olay işleyicisi, üst bilgi satırları, alt bilgi satırları ve ayırıcı satırları dahil olmak üzere DataList 'e eklenen *her* satır için ateşlenir. Ancak, ürün bilgileri yalnızca veri satırlarına bağlanır. Bu nedenle, DataList 'e bağlanan verileri incelemek için `ItemDataBound` olayını kullanırken, ilk olarak bir veri öğesiyle çalıştık olduğundan emin olunması gerekir. Bu, [aşağıdaki sekiz değerden](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listitemtype.aspx)birine sahip olabilen `DataListItem` s [`ItemType` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx)denetlenerek gerçekleştirilebilir:

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

Hem `Item` hem de `AlternatingItem``DataListItem`, DataList verileri öğelerini makeon. `Item` veya `AlternatingItem`ile çalıştık, geçerli `DataListItem`bağlanan gerçek `ProductsRow` örneğine erişeceğiz. `DataListItem` s [`DataItem` özelliği](https://msdn.microsoft.com/system.web.ui.webcontrols.datalistitem.dataitem.aspx) , `Row` özelliği gerçek `ProductsRow` nesnesine bir başvuru sunan `DataRowView` nesnesine bir başvuru içerir.

Sonra, `ProductsRow` örnek s `UnitPrice` özelliğini denetliyoruz. Products tablosu `UnitPrice` alanı `NULL` değerlere izin verdiğinden, `UnitPrice` özelliğine erişmeyi denemeden önce, `IsUnitPriceNull()` yöntemini kullanarak bir `NULL` değeri olup olmadığını kontrol etmemiz gerekir. `UnitPrice` değer `NULL`değilse, daha sonra $20,00 ' den daha az olup olmadığını kontrol eteceğiz. Gerçekten $20,00 altındaysa, özel biçimlendirmeyi uygulamanız gerekir.

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>3\. Adım: ürün adı ve fiyatını vurgulama

Bir ürün fiyatının $20,00 ' den küçük olduğunu öğrendikten sonra, bunların hepsi, adını ve fiyatını vurgulayabilmelidir. Bunu gerçekleştirmek için öncelikle ürün adı ve fiyatını görüntüleyen `ItemTemplate` etiket denetimlerine programlı bir şekilde başvurulmalıdır. Ardından, bunların sarı bir arka plan görüntülemesi gerekir. Bu biçimlendirme bilgileri, Etiketler `BackColor` Özellikler (`LabelID.BackColor = Color.Yellow`) ile doğrudan değiştirilerek uygulanabilir. ideal olarak, görüntüleme ile ilgili tüm önemli bilgiler geçişli stil sayfaları ile ifade edilmelidir. Aslında, veri öğreticisine *bağlı olarak özel biçimlendirme* içinde oluşturulan ve bahsedilen `Styles.css` - `AffordablePriceEmphasis`tanımlanan biçimlendirme içeren bir stil sayfası zaten var.

Biçimlendirmeyi uygulamak için aşağıdaki kodda gösterildiği gibi, iki etiketli Web denetimlerini `CssClass` özellikleri `AffordablePriceEmphasis`olarak ayarlamanız yeterlidir:

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample2.cs)]

`ItemDataBound` olay işleyicisi tamamlandığında `Formatting.aspx` sayfasını bir tarayıcıda yeniden ziyaret edin. Şekil 2 ' de gösterildiği gibi, $20,00 altındaki fiyata sahip olan ürünlerin hem adı hem de fiyatı vurgulanır.

[$20,00 ' den küçük olan ürünler ![vurgulanır](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image4.png)

**Şekil 2**: $20,00 ' den küçük ürünler vurgulanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image6.png))

> [!NOTE]
> DataList bir HTML `<table>`olarak işlendiği için, `DataListItem` örnekleri, öğenin tamamına belirli bir stil uygulamak üzere ayarlanbilen stille ilgili özelliklere sahiptir. Örneğin, fiyatı $20,00 ' den az olduğunda öğenin sarı *tamamını* vurgulamak Istiyorsam, etiketlere başvuran kodu değiştirmiş ve `CssClass` özelliklerini aşağıdaki kod satırıyla ayarlayabiliriz: `e.Item.CssClass = "AffordablePriceEmphasis"` (bkz. Şekil 3).

Yineleyicisi denetimini oluşturan `RepeaterItem` s, ancak bu tür stil düzeyi özellikleri sunmaz. Bu nedenle, Yineleyici için özel biçimlendirme uygulamak, Şekil 2 ' de olduğu gibi, yineleyici s şablonları içindeki Web denetimlerine stil özellikleri uygulanmasını gerektirir.

[![ürün öğesinin tamamı, $20,00 altındaki ürünler için vurgulanır](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image7.png)

**Şekil 3**: tüm ürün öğesi $20,00 altındaki ürünler için vurgulanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image9.png))

## <a name="using-formatting-functions-from-within-the-template"></a>Şablon Içinden biçimlendirme Işlevlerini kullanma

*GridView denetim öğreticisindeki TemplateFields kullanarak* , GridView s satırlarıyla bağlantılı verilere göre özel biçimlendirme uygulamak Için bir GridView TemplateField içinde biçimlendirme işlevinin nasıl kullanılacağını gördük. Biçimlendirme işlevi, bir şablondan çağrılabilen ve onun yerine yayınlanılacak HTML döndüren bir yöntemdir. Biçimlendirme işlevleri ASP.NET Page s kod arkasında bulunabilir veya `App_Code` klasöründe veya ayrı bir sınıf kitaplığı projesinde sınıf dosyalarında merkezi hale getirilmiş olabilir. Biçimlendirme işlevini ASP.NET Page s Code-Behind sınıfından taşımak, birden çok ASP.NET sayfasında veya diğer ASP.NET Web uygulamalarında aynı biçimlendirme işlevini kullanmayı planlıyorsanız idealdir.

Biçimlendirme işlevlerini göstermek için, ürün bilgileri ürün bilgilerinin yanında, ürün adı ' nın yanında [DISCONTINUED] metin içermesini sağlar. Ayrıca, $20,00 ' den küçük bir fiyata (`ItemDataBound` olay işleyicisi örneğinde yaptığımız gibi) sahip olmanız gerekir; Fiyat $20,00 veya daha yüksekse, gerçek fiyatı göstermemelidir, ancak bunun yerine metin olarak bir fiyat teklifi arayın. Şekil 4 ' te, bu biçimlendirme kuralları uygulanmış ürünlerin listesinin ekran görüntüsü gösterilmektedir.

[Pahalı ürünler Için ![Fiyat, metin ile, bir fiyat teklifi için çağrı ile değiştirilmiştir](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image10.png)

**Şekil 4**: pahalı ürünler için Fiyat, metin ile değiştirilmiştir, lütfen bir fiyat teklifini arayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image12.png))

## <a name="step-1-create-the-formatting-functions"></a>1\. Adım: biçimlendirme Işlevlerini oluşturma

Bu örnekte, bir tane olmak üzere iki biçimlendirme işlevi gerekir, biri, ürün adını, gerekirse metin ile ve $20,00 ' den az veya metin olduğunda vurgulanan bir fiyat görüntüleyen başka bir fiyat teklifi için çağırın. Bu işlevleri ASP.NET Page s arka plan kod sınıfında oluşturalım ve `DisplayProductNameAndDiscontinuedStatus` ve `DisplayPrice`olarak adlandırma. Her iki yöntemin de bir dize olarak işlenmesi için HTML döndürmesi ve ASP.NET Page s bildirime dayalı sözdizimi bölümünden çağrılması için `Protected` (veya `Public`) olarak işaretlenmesi gerekir. Bu iki yöntemin kodu aşağıda verilmiştir:

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample3.cs)]

`DisplayProductNameAndDiscontinuedStatus` yöntemi, `productName` ve `discontinued` veri alanlarının değerlerini skaler değerler olarak kabul eder, ancak `DisplayPrice` yöntemi bir `ProductsRow` skalar değer yerine bir `unitPrice` örneği kabul eder. Her iki yaklaşım da çalışacaktır; Ancak, biçimlendirme işlevi, veritabanı `NULL` değerleri içerebilen skaler değerlerle çalışıyorsa (`UnitPrice`gibi, ne `ProductName` ne de `Discontinued` izin `NULL` ver), bu skaler girdileri işlemek için özel dikkatli olunmalıdır.

Özellikle, gelen değer beklenen veri türü yerine `DBNull` bir örnek olabileceğinden, giriş parametresi `Object` türünde olmalıdır. Ayrıca, gelen değerin bir veritabanı `NULL` değeri olup olmadığını belirlemekte bir denetim yapılmalıdır. Diğer bir deyişle, `DisplayPrice` yönteminin fiyatı skaler bir değer olarak kabul etmesini istediyseniz, aşağıdaki kodu kullanmak zorunda olduğumuz:

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample4.cs)]

`unitPrice` giriş parametresinin `Object` türünde olduğunu ve koşullu deyimin `unitPrice` `DBNull` olması durumunda ascermesi olarak değiştirildiğini unutmayın. Ayrıca, `unitPrice` giriş parametresi bir `Object`olarak geçirildiğinden, bunun ondalık bir değere dönüştürülmesi gerekir.

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>2\. Adım: DataList s ItemTemplate 'ten biçimlendirme Işlevini çağırma

Biçimlendirme işlevleri ASP.NET Page s Code-Behind sınıfına eklendikten sonra, bu biçimlendirme işlevlerini DataList `ItemTemplate`' den çağırmalar. Bir şablondan biçimlendirme işlevini çağırmak için, işlev çağrısını veri bağlama söz dizimi içine yerleştirin:

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample5.aspx)]

DataList s `ItemTemplate` `ProductNameLabel` etiketi Web denetimi şu anda `Text` özelliğini `<%# Eval("ProductName") %>`sonucunu atayarak ürün s adını görüntülüyor. Bu durumda, adı ve [DISCONTINUED] metnini göstermek için, bildirim temelli sözdizimini, `Text` özelliğini `DisplayProductNameAndDiscontinuedStatus` yönteminin değerine atayacağı şekilde güncelleştirin. Bunu yaparken, `Eval("columnName")` sözdizimini kullanarak ürün adı ve Discontinued değerlerini geçirmemiz gerekir. `Eval` `Object`türünde bir değer döndürür, ancak `DisplayProductNameAndDiscontinuedStatus` yöntemi `String` ve `Boolean`türünde giriş parametrelerini bekler; Bu nedenle, `Eval` yönteminin döndürdüğü değerleri beklenen giriş parametresi türlerine (şöyle) atamalısınız:

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample6.aspx)]

Fiyatı görüntülemek için, yalnızca ürün adı ve [DISCONTINUED] metnini görüntüleme yaptığımız gibi, `UnitPriceLabel` etiket s `Text` özelliğini `DisplayPrice` yönteminin döndürdüğü değere ayarlayabiliriz. Ancak, `UnitPrice` skaler giriş parametresi olarak geçirmek yerine, tüm `ProductsRow` örneğini geçeceğiz:

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample7.aspx)]

Biçimlendirme işlevlerine yapılan çağrılar sayesinde, ilerleme durumunu tarayıcıda görüntülemek için bir dakikanızı ayırın. Ekranınızda Şekil 5 ' e benzer bir şekilde, "DISCONTINUED] metni de dahil olmak üzere, ücretlendirilmesi gereken ürünler ile $20,00 ' den fazla maliyetten daha fazla ücret ödemelidir.

[Pahalı ürünler Için ![Fiyat, metin ile, bir fiyat teklifi için çağrı ile değiştirilmiştir](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image13.png)

**Şekil 5**: pahalı ürünler için Fiyat, metin ile değiştirilmiştir, lütfen bir fiyat teklifini arayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image15.png))

## <a name="summary"></a>Özet

Verileri temel alan DataList veya Repeater denetiminin içeriğini biçimlendirmek iki teknik kullanılarak gerçekleştirilebilir. İlk yöntem, veri kaynağındaki her bir kayıt yeni bir `DataListItem` veya `RepeaterItem`bağlantılı olduğundan harekete `ItemDataBound` olayı için bir olay işleyicisi oluşturmaktır. `ItemDataBound` olay işleyicisinde, geçerli öğe verileri incelenebilir ve sonra biçimlendirme şablonun içeriğine veya `DataListItem` s için öğenin tamamına uygulanabilir.

Alternatif olarak, biçimlendirme işlevleri aracılığıyla özel biçimlendirme gerçekleştirilebilir. Biçimlendirme işlevi, yerinde göstermek için HTML döndüren DataList veya Repeater s şablonlarından çağrılabilen bir yöntemdir. Genellikle, biçimlendirme işlevi tarafından döndürülen HTML, geçerli öğeye bağlanmakta olan değerlere göre belirlenir. Bu değerler, skaler değerler olarak veya öğeye bağlanmakta olan nesnenin tamamına (`ProductsRow` örneği gibi) geçirerek biçimlendirme işlevine geçirilebilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Yaakov Ellis, Randy SCHMIDT ve Liz Shulok. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](displaying-data-with-the-datalist-and-repeater-controls-cs.md)
> [İleri](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
