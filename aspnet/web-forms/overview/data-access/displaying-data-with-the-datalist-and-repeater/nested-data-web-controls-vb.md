---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-vb
title: İç içe veri Web denetimleri (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, başka bir yineleyici içinde iç içe geçmiş bir yineleyicisi nasıl kullanacağınızı keşfedeceğiz. Örneklerde, her ikisi de iç Yineleyici olarak nasıl doldurulacağınız gösterilmektedir...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 8b7fcf7b-722b-498d-a4e4-7c93701e0c95
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: c3c62ce4293498d3b325031ac9817f8935b183b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74629556"
---
# <a name="nested-data-web-controls-vb"></a>İç İçe Veri Web Denetimleri (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_VB.exe) veya [PDF 'yi indirin](nested-data-web-controls-vb/_static/datatutorial32vb1.pdf)

> Bu öğreticide, başka bir yineleyici içinde iç içe geçmiş bir yineleyicisi nasıl kullanacağınızı keşfedeceğiz. Örnek olarak, iç yineleyicisi hem bildirimli hem de programlı olarak nasıl doldurulacağınız gösterilmektedir.

## <a name="introduction"></a>Giriş

Statik HTML ve veri bağlama sözdiziminin yanı sıra, Şablonlar Web denetimlerini ve kullanıcı denetimlerini de içerebilir. Bu Web denetimlerine, özelliklerinin bildirime dayalı, veri bağlama söz dizimi aracılığıyla atanması veya uygun sunucu tarafı olay işleyicilerinde program aracılığıyla erişilebilir olması olabilir.

Bir şablon içindeki denetimleri gömerek, görünüm ve Kullanıcı deneyimi üzerinde özelleştirilebilir ve geliştirilebilir. Örneğin, [GridView denetim öğreticisindeki TemplateFields kullanarak](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) , bir çalışan bir giriş tarihi göstermek üzere TemplateField içinde Takvim denetimi ekleyerek GridView s görüntüsünü özelleştirmeyi gördük. [düzenlemede doğrulama denetimleri ekleme ve arabirim ekleme](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) ve [veri değişikliği arabirimi](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) öğreticilerini özelleştirme konusunda, doğrulama denetimleri, metin kutuları, Dropdownlists ve diğer Web denetimleri ekleyerek, düzenlemenin ve ekleme arabirimlerinin nasıl özelleştirileceğini gördük.

Şablonlar, diğer veri Web denetimlerini de içerebilir. Diğer bir deyişle, şablonları içinde başka bir DataList (veya Repeater veya GridView ya da DetailsView vb.) içeren bir DataList 'i olabilir. Böyle bir arabirim ile zorluk, ilgili verileri iç veri Web denetimine bağlamadır. Kullanılabilir birkaç farklı yaklaşım vardır ve bunları programlı bir şekilde kullanarak bildirim temelli seçeneklerden farklıdır.

Bu öğreticide, başka bir yineleyici içinde iç içe geçmiş bir yineleyicisi nasıl kullanacağınızı keşfedeceğiz. Dış Yineleyici, kategori adı ve açıklamasını görüntüleyerek veritabanındaki her bir kategori için bir öğe içerecektir. Her bir kategori öğesi iç Yineleyici, bu kategoriye ait her bir ürün için bilgileri (bkz. Şekil 1) madde işaretli bir listede görüntüler. Örneklerimizde iç yineleyicisi hem bildirimli hem de programlı olarak nasıl doldurulacağınız gösterilmektedir.

[Her kategori ![, ürünleriyle birlikte listelenir](nested-data-web-controls-vb/_static/image2.png)](nested-data-web-controls-vb/_static/image1.png)

**Şekil 1**: her kategori, ürünlerle birlikte listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-data-web-controls-vb/_static/image3.png))

## <a name="step-1-creating-the-category-listing"></a>1\. Adım: Kategori listesini oluşturma

İç içe geçmiş veri Web denetimlerini kullanan bir sayfa oluştururken, iç içe geçmiş denetim hakkında endişelenmeden önce en dıştaki veri Web denetimini tasarlamak, oluşturmak ve test etmek faydalı olduğunu öğreniyorum. Bu nedenle, her bir kategorinin adını ve açıklamasını listeleyen sayfaya bir yineleyici eklemek için gereken adımları izleyerek başlayalım.

`NestedControls.aspx` sayfasını `DataListRepeaterBasics` klasöründen açıp sayfaya bir yineleyici denetimi ekleyerek `ID` özelliğini `CategoryList`olarak ayarlayarak başlayın. Yineleyici s akıllı etiketinden `CategoriesDataSource`adlı yeni bir ObjectDataSource oluşturmayı seçin.

[Yeni ObjectDataSource CategoriesDataSource ![adı](nested-data-web-controls-vb/_static/image5.png)](nested-data-web-controls-vb/_static/image4.png)

**Şekil 2**: yeni ObjectDataSource `CategoriesDataSource` adlandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-data-web-controls-vb/_static/image6.png))

ObjectDataSource 'ı, verileri `CategoriesBLL` sınıf s `GetCategories` yönteminden çeker şekilde yapılandırın.

[![, ObjectDataSource 'un CategoriesBLL sınıfı s GetCategories metodunu kullanacak şekilde yapılandırılması](nested-data-web-controls-vb/_static/image8.png)](nested-data-web-controls-vb/_static/image7.png)

**Şekil 3**: `CategoriesBLL` sınıf s `GetCategories` metodunu ([tam boyutlu görüntüyü görüntülemek Için tıklayın](nested-data-web-controls-vb/_static/image9.png)) kullanmak üzere ObjectDataSource 'ı yapılandırın

Repeater ' ın şablon içeriğini belirtmek için, kaynak görünümüne gitmemiz ve bildirim temelli sözdizimini el ile girmeniz gerekir. Kategori s adını bir `<h4>` öğesinde ve kategori s açıklamasını bir paragraf öğesinde (`<p>`) görüntüleyen bir `ItemTemplate` ekleyin. Ayrıca, her kategoriyi yatay bir kuralla ayıralım (`<hr>`). Bu değişiklikleri yaptıktan sonra sayfanız, aşağıdaki gibi yineleyici ve ObjectDataSource için bildirime dayalı sözdizimi içermelidir:

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample1.aspx)]

Şekil 4 ' te bir tarayıcıdan görüntülendiklerinde ilerleme durumu gösterilmektedir.

[![her kategorinin adı ve açıklaması, yatay bir kuralla ayrılmış olarak listelenir](nested-data-web-controls-vb/_static/image11.png)](nested-data-web-controls-vb/_static/image10.png)

**Şekil 4**: her kategori adı ve açıklaması, yatay bir kuralla ayrılmış olarak listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-data-web-controls-vb/_static/image12.png))

## <a name="step-2-adding-the-nested-product-repeater"></a>2\. Adım: Iç Içe geçmiş ürün yineleyicisi ekleme

Kategori listeleme tamamlandı, bir sonraki göreviniz, uygun kategoriye ait olan ürünlerle ilgili bilgileri görüntüleyen `CategoryList` s `ItemTemplate` bir yineleyici eklemektir. Bu iç Yineleyici için verileri alabildiğimiz birçok yol vardır. Bu, kısa bir süre içinde araştıracağız. Şimdilik, s `ItemTemplate``CategoryList` Repeater ' ın içindeki ürünleri yalnızca Yineleyici olarak oluşturalım. Özellikle, ürün yineleyicisi 'nin her bir ürünü, ürün adı ve fiyat dahil olmak üzere her bir liste öğesiyle birlikte madde işaretli bir listede görüntülemesine izin verin.

Bu yineleyicisi oluşturmak için, iç yineleyicisi 'nin bildirim temelli sözdizimini ve şablonları `CategoryList` s `ItemTemplate`içine el ile girmemiz gerekir. Aşağıdaki biçimlendirmeyi `CategoryList` Yineleyici `ItemTemplate`içine ekleyin:

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>3\. Adım: kategoriye özgü ürünleri ProductsByCategoryList Repeater 'a bağlama

Bu noktada sayfayı bir tarayıcı aracılığıyla ziyaret ederseniz, herhangi bir veriyi yineleyicisi 'ne bağlamamız yaptığımız için ekranınızın Şekil 4 ' te olduğu gibi görünmesi gerekir. Uygun ürün kayıtlarını elde etmemiz ve bunları yineleyicisi 'ne bağlamak için birkaç yol vardır ve bunlardan bazıları diğerlerinden daha etkilidir. Buradaki ana zorluk, belirtilen kategori için uygun ürünleri geri almaktır.

İç Yineleyici denetimine bağlanacak verilere bildirimli olarak `CategoryList` `ItemTemplate`Repeater ' daki bir ObjectDataSource aracılığıyla ya da programlı olarak ASP.NET Page s arka plan kod sayfasından erişilebilir. Benzer şekilde, bu veriler iç Yineleyici ile iç yineleyicinin `DataSourceID` özelliği aracılığıyla ya da bildirim temelli veri bağlama söz dizimi aracılığıyla ya da program aracılığıyla `CategoryList` Yineleyici s `ItemDataBound` olay işleyic`DataBind()` `DataSource` isindeki iç Yineleyici ile başvurularak programlı bir şekilde bağlanabilir. Bu yaklaşımların her birini keşfedelim.

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>Bir ObjectDataSource denetimiyle ve`ItemDataBound`olay Işleyicisiyle verilere bildirimli olarak erişme

Bu öğretici serisi genelinde ObjectDataSource 'u kapsamlı bir şekilde kullandığımızdan, bu örneğe yönelik verilere erişim için en doğal seçenek, ObjectDataSource 'u kontrol etmek için kullanılır. `ProductsBLL` sınıfında, belirtilen *`categoryID`* ait olan ürünler hakkında bilgi döndüren bir `GetProductsByCategoryID(categoryID)` yöntemi vardır. Bu nedenle, `CategoryList` Yineleyici `ItemTemplate` bir ObjectDataSource ekleyebiliyoruz ve bu sınıf s yönteminden verilerine erişecek şekilde yapılandırabiliriz.

Ne yazık ki Yineleyici, şablonlarının Tasarım görünümü aracılığıyla düzenlenmesine izin vermez, bu nedenle bu ObjectDataSource denetimi için bildirim temelli sözdizimini el ile eklememiz gerekir. Aşağıdaki sözdizimi, bu yeni ObjectDataSource eklendikten sonra `ItemTemplate` `CategoryList` yineleyicisi 'ni gösterir (`ProductsByCategoryDataSource`):

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample3.aspx)]

ObjectDataSource yaklaşımını kullanırken, `ProductsByCategoryList` Yineleyici s `DataSourceID` özelliğini ObjectDataSource 'un (`ProductsByCategoryDataSource`) `ID` ayarlaması gerekir. Ayrıca, ObjectDataSource 'lerimizin `GetProductsByCategoryID(categoryID)` yöntemine geçirilecek *`categoryID`* değerini belirten bir `<asp:Parameter>` öğesi olduğuna dikkat edin. Ancak bu değeri nasıl belirttik? İdeal olarak, aşağıdaki gibi, veri bağlama söz dizimini kullanarak `<asp:Parameter>` öğesinin `DefaultValue` özelliğini ayarlayabiliriz:

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample4.aspx)]

Ne yazık ki, veri bağlama söz dizimi yalnızca `DataBinding` olayına sahip denetimlerde geçerlidir. `Parameter` sınıfında böyle bir olay yok ve bu nedenle yukarıdaki sözdizimi geçersizdir ve bir çalışma zamanı hatasına neden olur.

Bu değeri ayarlamak için, `CategoryList` Repeater s `ItemDataBound` olayı için bir olay işleyicisi oluşturuyoruz. Yineleyicisi 'ne bağlanan her öğe için `ItemDataBound` olayının bir kez harekete geçirilir. Bu nedenle, bu olay dış Yineleyici için her tetiklendiğinde, geçerli `CategoryID` değerini `ProductsByCategoryDataSource` ObjectDataSource s `CategoryID` parametresine atayabiliriz.

Aşağıdaki kodla `CategoryList` Repeater s `ItemDataBound` olayı için bir olay işleyicisi oluşturun:

[!code-vb[Main](nested-data-web-controls-vb/samples/sample5.vb)]

Bu olay işleyicisi, üst bilgi, alt bilgi veya ayırıcı öğe yerine bir veri öğesiyle ilgilenmemiz sağlanarak başlar. Ardından, geçerli `RepeaterItem`zaten bağlanan gerçek `CategoriesRow` örneğine başvuruyoruz. Son olarak, `ItemTemplate` ObjectDataSource 'a başvurduk ve `CategoryID` parametre değerini geçerli `RepeaterItem``CategoryID` atamalısınız.

Bu olay işleyicisiyle, her `RepeaterItem` `ProductsByCategoryList` yineleyicisi `RepeaterItem` s kategorisindeki bu ürünlere bağlanır. Şekil 5 elde edilen çıktının ekran görüntüsünü gösterir.

[Dış Yineleyici ![her kategoriyi listeler; Inner bir kategori için ürünleri listeler](nested-data-web-controls-vb/_static/image14.png)](nested-data-web-controls-vb/_static/image13.png)

**Şekil 5**: dış Yineleyici her kategoriyi listeler; Inner bir kategori için ürünleri listeler ([tam boyutlu görüntüyü görüntülemek Için tıklayın](nested-data-web-controls-vb/_static/image15.png))

## <a name="accessing-the-products-by-category-data-programmatically"></a>Program aracılığıyla kategoriye göre ürünlere erişme

Geçerli kategori için ürünleri almak üzere bir ObjectDataSource kullanmak yerine, bir `CategoryID`geçirildiğinde uygun ürün kümesini döndüren ASP.NET Page s arka plan kod sınıfında (veya `App_Code` klasöründe veya ayrı bir sınıf kitaplığı projesinde) bir yöntem oluşturarız. ASP.NET Page s kod arkasında bir yöntem olduğunu ve `GetProductsInCategory(categoryID)`adlandırdığını düşünün. Bu yöntemle birlikte, aşağıdaki bildirime dayalı sözdizimini kullanarak geçerli kategorinin ürünlerini iç Yineleyici olarak bağlayabiliriz:

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample6.aspx)]

Repeater s `DataSource` özelliği, verilerinin `GetProductsInCategory(categoryID)` yönteminden geldiğini göstermek için DataBinding sözdizimini kullanır. `Eval("CategoryID")` `Object`türünde bir değer döndürdüğünden, nesneyi `GetProductsInCategory(categoryID)` yöntemine geçirmeden önce bir `Integer` hale getiririz. Veri bağlama söz dizimi aracılığıyla buraya erişildiğine `CategoryID`, bu, `Categories` tablosundaki kayıtlarla bağlantılı olan *dış* yineleyici (`CategoryList`) `CategoryID`. Bu nedenle `CategoryID` bir veritabanı `NULL` değeri olmadığını biliyoruz. Bu, neden bir `DBNull`ile ilgilendiğinizi kontrol etmeden `Eval` metodunu daha da düzenleyebilir.

Bu yaklaşımda `GetProductsInCategory(categoryID)` yöntemi oluşturuyoruz ve sağlanan *`categoryID`* verilen uygun ürün kümesini almamız gerekir. Bunu, `ProductsBLL` sınıfı s `GetProductsByCategoryID(categoryID)` metodu tarafından döndürülen `ProductsDataTable` döndürerek yapabiliriz. `NestedControls.aspx` sayfamız için arka plan kod sınıfında `GetProductsInCategory(categoryID)` yöntemi oluşturalım. Aşağıdaki kodu kullanarak bunu yapın:

[!code-vb[Main](nested-data-web-controls-vb/samples/sample7.vb)]

Bu yöntem, yalnızca `ProductsBLL` yönteminin bir örneğini oluşturur ve `GetProductsByCategoryID(categoryID)` yönteminin sonuçlarını döndürür. Metodun `Public` veya `Protected`olarak işaretlenmesi gerektiğini unutmayın. Yöntem `Private`işaretlenmişse, ASP.NET sayfa s bildirime dayalı biçimlendirmeden erişilebilir olmayacaktır.

Bu yeni tekniği kullanmak için bu değişiklikleri yaptıktan sonra, sayfayı bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. ObjectDataSource ve `ItemDataBound` olay işleyicisi yaklaşımı kullanılırken çıkış ile aynı olmalıdır (ekran görüntüsünü görmek için Şekil 5 ' e geri dönün).

> [!NOTE]
> ASP.NET Page s arka plan kod sınıfında `GetProductsInCategory(categoryID)` yöntemi oluşturmak için Busi işi gibi görünebilir. All, bu yöntem `ProductsBLL` sınıfının bir örneğini oluşturur ve `GetProductsByCategoryID(categoryID)` yönteminin sonuçlarını döndürür. Bu yöntemi neden yalnızca iç Yineleyici içindeki veri bağlama sözdiziminden (`DataSource='<%# ProductsBLL.GetProductsByCategoryID(CType(Eval("CategoryID"), Integer)) %>'`gibi) doğrudan çağıramadınız. Bu söz dizimi, `ProductsBLL` sınıfının geçerli uygulamamız ile çalışmasa da (`GetProductsByCategoryID(categoryID)` yöntemi bir örnek yöntemi olduğundan), `ProductsBLL` statik bir `GetProductsByCategoryID(categoryID)` metodu içerecek şekilde değiştirebilir veya `Instance()` sınıfının yeni bir örneğini döndürmek için sınıfın statik `ProductsBLL` yöntemini içermesini sağlayabilirsiniz.

Bu değişiklikler, ASP.NET sayfa kodu arka plan kodundaki `GetProductsInCategory(categoryID)` yöntemi gereksinimini ortadan kaldıracak, ancak arka plan kod sınıfı yöntemi, kısa süre içinde göreceğiniz şekilde, alınan verilerle çalışma konusunda daha fazla esneklik sağlar.

## <a name="retrieving-all-of-the-product-information-at-once"></a>Tüm ürün bilgilerini aynı anda alma

`ProductsBLL` sınıf s `GetProductsByCategoryID(categoryID)` yöntemine bir çağrı yaparak inceliyoruz ve bu ürünlerin geçerli kategori için bu ürünleri elde ettiğimiz iki performans tekniği (ilk yaklaşım bir ObjectDataSource tarafından, ikinciden kod arkasındaki `GetProductsInCategory(categoryID)` yöntemi aracılığıyla). Bu yöntemin her çağrılışında Iş mantığı katmanı, `CategoryID` alanı sağlanan giriş parametresiyle eşleşen `Products` tablosundan satırları döndüren bir SQL ifadesiyle veritabanını sorgulayan veri erişim katmanına geri döner.

Sistemde bu yaklaşım, tüm kategorileri almak için tek bir veritabanı sorgusuna yönelik *n* + 1 çağrıları ve her kategoriye özgü ürünleri almak için *n* çağrısı sağlar. Ancak, tüm gerekli verileri yalnızca iki veritabanında alabilir ve tüm ürünlerin tümünü almak için bir çağrı yapın. Tüm ürünleri edindikten sonra, bu ürünleri yalnızca geçerli `CategoryID` eşleşen ürünlerin bu kategoriye ait iç Yineleyici ile bağlanacağı şekilde filtreleyebiliriz.

Bu işlevi sağlamak için, ASP.NET Page s Code-Behind sınıfındaki `GetProductsInCategory(categoryID)` yönteminde yalnızca küçük bir değişiklik yapmanız gerekir. `ProductsBLL` sınıf s `GetProductsByCategoryID(categoryID)` yönteminin sonuçlarını bir adım adım geri döndürmek yerine, bu ürünlerin *tümüne* ilk kez erişebiliriz (önceden erişilmemişse) ve ardından, geçirilen `CategoryID`göre yalnızca ürünlerin filtrelenmiş görünümünü geri alabilirsiniz.

[!code-vb[Main](nested-data-web-controls-vb/samples/sample8.vb)]

Sayfa düzeyi değişkeninin eklenmesini `allProducts`. Bu, tüm ürünlerle ilgili bilgileri barındırır ve `GetProductsInCategory(categoryID)` yöntemi ilk kez çağrıldığında doldurulur. `allProducts` nesnesinin oluşturulup doldurulduğundan emin olduktan sonra, yöntemi DataTable s sonuçlarını yalnızca `CategoryID` belirtilen `CategoryID` eşleşen satırlara erişilebilir olacak şekilde filtreler. Bu yaklaşım, veritabanına *N* + 1 ' den iki kez erişilme sayısını azaltır.

Bu geliştirme, sayfanın işlenmiş biçimlendirmesinde herhangi bir değişikliğe neden olmaz, ne de diğer yaklaşımdan daha az kayıt geri getirir. Yalnızca veritabanına yapılan çağrıların sayısını azaltır.

> [!NOTE]
> Bunlardan biri, veritabanı erişimlerini azaltmak assuredly performansı artırmak için çok sayıda neden olabilir. Ancak, bu durum olmayabilir. `CategoryID` `NULL`olan çok sayıda ürünsahipseniz, örneğin `GetProducts` yöntemine yapılan çağrı, hiçbir şekilde görüntülenmeyen bir dizi ürünü geri döndürür. Üstelik, yalnızca kategorilerin bir alt kümesini gösteriyorsanız, bu, sayfalama uygulamış olmanız durumunda olabilecek tüm ürünlerin döndürülmesi beklenebilir.

Her zaman olduğu gibi, iki tekninin performansını analiz etmek için tek SureFire ölçüsü, uygulamanızın ortak olay senaryolarınız için uyarlanmış denetimli testleri çalıştırmalıdır.

## <a name="summary"></a>Özet

Bu öğreticide, bir veri Web denetiminin başka bir şekilde nasıl iç yineleyicisi olduğunu, özellikle de bir dış yineleyicisi 'nin bir madde işaretli liste içindeki her bir kategorinin ürünlerini listeleme iç Yineleyici olan her kategori için bir öğe göstermesini gördük. İç içe bir kullanıcı arabirimi oluşturmanın ana zorluğu, doğru verileri iç veri Web denetimine bağlama ve bunlara bağlama konusunda yer alır. Bu öğreticide incelenen, iki farklı teknik mevcuttur. İlk yaklaşım, `DataSourceID` özelliği aracılığıyla iç veri Web denetimine bağlanan `ItemTemplate` dış veri Web denetimindeki bir ObjectDataSource kullandı. İkinci teknikte, ASP.NET Page s arka plan kod sınıfındaki bir yöntem aracılığıyla verilere erişilir. Bu yöntem daha sonra veri bağlama söz dizimi aracılığıyla iç veri Web denetimi s `DataSource` özelliğine bağlanabilir.

Bu öğreticide incelenen iç içe geçmiş kullanıcı arabirimi, bir yineleyici içinde iç içe geçmiş bir yineleyici kullanıyordu, bu teknikler diğer veri Web denetimlerine genişletilebilir. Bir ya da bir GridView içinde bir bir yineleyici iç içe veya bir GridView içinde bir GridView oluşturabilirsiniz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Zack Jones ve Liz Shulok. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Öncekini](showing-multiple-records-per-row-with-the-datalist-control-vb.md)
