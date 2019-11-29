---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
title: DataList veya Repeater denetiminde verileri sıralama (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, verileri DataList ve Repeater ' da sıralama desteğinin yanı sıra, verilerini oluşturabilen bir DataList veya Repeater oluşturmayı inceleyeceğiz...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: f52c302a-1b7c-46fe-8a13-8412c95cbf6d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 66a09c637d33c812b39e0ce85a552bd71665a2e1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634658"
---
# <a name="sorting-data-in-a-datalist-or-repeater-control-c"></a>DataList veya Repeater Denetiminde Verileri Sıralama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_CS.exe) veya [PDF 'yi indirin](sorting-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial45cs1.pdf)

> Bu öğreticide, veri Sayfalanmış ve sıralanmış bir DataList veya Repeater oluşturma desteğinin yanı sıra DataList ve Repeater ' da sıralama desteğinin nasıl ekleneceğini inceleyeceğiz.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](paging-report-data-in-a-datalist-or-repeater-control-cs.md) , bir DataList 'e disk belleği desteğinin nasıl ekleneceğini inceliyoruz. `PagedDataSource` nesnesi döndüren `ProductsBLL` sınıfında (`GetProductsAsPagedDataSource`) yeni bir yöntem oluşturduk. DataList veya Repeater 'a bağlandığında, DataList veya Repeater yalnızca istenen veri sayfasını görüntüler. Bu teknik, yerleşik varsayılan sayfalama işlevlerini sağlamak için GridView, DetailsView ve FormView denetimleri tarafından dahili olarak kullanılan ile benzerdir.

GridView, sayfalama desteğinin yanı sıra, kullanıma hazır sıralama desteğini de içerir. DataList veya Repeater, yerleşik sıralama işlevselliği sağlar; Ancak, sıralama özellikleri bir kod ile eklenebilir. Bu öğreticide, veri Sayfalanmış ve sıralanmış bir DataList veya Repeater oluşturma desteğinin yanı sıra DataList ve Repeater ' da sıralama desteğinin nasıl ekleneceğini inceleyeceğiz.

## <a name="a-review-of-sorting"></a>Sıralamayı gözden geçirme

[Sayfalama ve rapor verilerini sıralama](../paging-and-sorting/paging-and-sorting-report-data-cs.md) öğreticisinde gördüğünüz gibi, GridView denetimi kullanıma hazır sıralama desteği sunar. Her GridView alanı, verilerin sıralanma ölçütü olan veri alanını gösteren ilişkili bir `SortExpression`sahip olabilir. GridView s `AllowSorting` özelliği `true`olarak ayarlandığında, bir `SortExpression` özellik değerine sahip her GridView alanının üst bilgisi bir LinkButton olarak işlenir. Bir Kullanıcı belirli bir GridView alanı üst bilgisine tıkladığında, bir geri gönderme gerçekleşir ve veriler, tıklanan alana göre sıralanır `SortExpression`.

GridView denetiminin, verilerin sıralandığı GridView alanının `SortExpression` depolayan bir `SortExpression` özelliği de vardır. Ayrıca, `SortDirection` özellik verilerin artan veya azalan düzende sıralanacağını belirtir (bir Kullanıcı belirli bir GridView alanı üst bilgi bağlantısını art arda iki kez tıklarsa sıralama düzeni değiştirilebilir).

GridView, veri kaynağı denetimine bağlandığında, `SortExpression` ve `SortDirection` özelliklerini veri kaynağı denetimine bırakır. Veri kaynağı denetimi verileri alır ve sonra sağlanan `SortExpression` ve `SortDirection` özelliklerine göre sıralar. Verileri sıraladıktan sonra veri kaynağı denetimi GridView 'a geri döndürür.

Bu işlevselliği DataList veya Yineleyici denetimleriyle çoğaltmak için şunları yapmanız gerekir:

- Sıralama arabirimi oluşturma
- Sıralama yapılacak veri alanını ve artan veya azalan düzende sıralama yapılıp yapılmayacağını unutmayın
- ObjectDataSource 'a verileri belirli bir veri alanına göre sıralamayı bildirin

3 ve 4. adımlarda bu üç görevi ele alacağız. Bunun ardından, bir DataList veya Repeater içinde hem sayfalama hem de sıralama desteğinin nasıl ekleneceğini inceleyeceğiz.

## <a name="step-2-displaying-the-products-in-a-repeater"></a>2\. Adım: bir yineleyici içinde ürünleri görüntüleme

Sıralama ile ilgili işlevlerden herhangi birini uygulama konusunda endişelenmemiz için önce bir yineleyici denetimindeki ürünleri listeleyerek başlayalım. `PagingSortingDataListRepeater` klasöründeki `Sorting.aspx` sayfasını açarak başlayın. Web sayfasına bir yineleyici denetimi ekleyin, `ID` özelliğini `SortableProducts`olarak ayarlar. Yineleyicisi 'nin akıllı etiketinde `ProductsDataSource` adlı yeni bir ObjectDataSource oluşturun ve `ProductsBLL` sınıf s `GetProducts()` yönteminden verileri almak üzere yapılandırın. Ekle, GÜNCELLEŞTIR ve SIL sekmelerinde açılan listelerden (hiçbiri) seçeneğini belirleyin.

[![bir ObjectDataSource oluşturun ve bunu GetProductsAsPagedDataSource () metodunu kullanacak şekilde yapılandırın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**Şekil 1**: bir ObjectDataSource oluşturun ve `GetProductsAsPagedDataSource()` metodunu kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image3.png))

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image4.png)

**Şekil 2**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinden açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image6.png))

DataList ile farklı olarak, Visual Studio bir veri kaynağına bağlamadan sonra Yineleyici denetimi için otomatik olarak bir `ItemTemplate` oluşturmaz. Ayrıca, yineleyici denetimi ' nin akıllı etiketinde DataList 'te bulunan Şablonları Düzenle seçeneği bulunmadığından bu `ItemTemplate` bildirimli olarak eklememiz gerekir. Ürünlerin adı, tedarikçisini ve kategorisini görüntüleyen önceki öğreticiden aynı `ItemTemplate` kullanmasına izin verin.

`ItemTemplate`eklendikten sonra, Repeater ve ObjectDataSource 'un bildirim temelli işaretlemesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample1.aspx)]

Şekil 3 ' te Bu sayfa bir tarayıcı aracılığıyla görüntülenirken gösterilmektedir.

[Her ürün adı, sağlayıcı ve kategori ![görüntülenir](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**Şekil 3**: her ürün adı, sağlayıcı ve kategori görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image9.png))

## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>3\. Adım: verileri sıralamak için ObjectDataSource 'ı sıralama

Yineleyicisi 'nde görünen verileri sıralamak için, verilerin sıralanması gereken sıralama ifadesinin ObjectDataSource 'u bilgilendirmemiz gerekir. ObjectDataSource, verilerini almadan önce bir sıralama ifadesi belirtmemizi sağlayan bir fırsat sunan [`Selecting` olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx)tetikler. `Selecting` olay işleyicisi, [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)türünde [`Arguments`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx) adında bir özelliğe sahip [`ObjectDataSourceSelectingEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx)türünde bir nesne geçirdi. `DataSourceSelectArguments` sınıfı, veri tüketiciden veri kaynağı denetimine verilerle ilgili istekleri geçirmek için tasarlanmıştır ve bir [`SortExpression` özelliği](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx)içerir.

ASP.NET sayfasından ObjectDataSource 'a sıralama bilgilerini geçirmek için, `Selecting` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu kullanın:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

*SortExpression* değerine, verileri sıralamak için veri alanının adı atanmalıdır (örneğin, ProductName). Sıralama yönü ile ilgili bir özellik yoktur, bu nedenle verileri azalan düzende sıralamak isterseniz, bir dizeyi (örneğin, ÜrünAdı DESC), *SortExpression* değerine ekleyin.

Devam edin ve *SortExpression* için farklı sabit kodlanmış değerler deneyin ve sonuçları bir tarayıcıda test edin. Şekil 4 ' te gösterildiği gibi, bir program, *SortExpression*olarak bir açıklama kullanırken, ürünler ters alfabetik sırada adına göre sıralanır.

[![ürünleri, ters alfabetik sırada adına göre sıralanır](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**Şekil 4**: Ürünler ada göre ters alfabetik sırada sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image12.png))

## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>4\. Adım: sıralama arabirimini oluşturma ve sıralama Ifadesini ve yönünü anımsama

GridView 'da sıralama desteğini açmak, her sıralanabilir alanın üst bilgi metnini, tıklandığı sırada verileri uygun şekilde sıralayan bir LinkButton öğesine dönüştürür. Bu tür bir sıralama arabirimi, verileri sütunlarda uygun şekilde yerleştirildiği GridView için anlamlı hale getirir. Ancak, DataList ve Repeater denetimleri için farklı bir sıralama arabirimi gerekir. Verilerin listesi için ortak bir sıralama arabirimi (bir veri kılavuzunun aksine), verilerin sıralanabilecek alanları sağlayan bir açılan listesidir. Bu öğretici için bu tür bir arabirim uygulayalım.

`SortableProducts` Yineleyici üzerine bir DropDownList Web denetimi ekleyin ve `ID` özelliğini `SortBy`olarak ayarlayın. Özellikler penceresi, ListItem Koleksiyonu düzenleyicisini açmak için `Items` özelliğindeki üç noktaya tıklayın. Verileri `ProductName`, `CategoryName`ve `SupplierName` alanlarına göre sıralamak için `ListItem` s ekleyin. Ayrıca, ürünleri ters alfabetik sırada adına göre sıralamak için bir `ListItem` ekleyin.

`ListItem` `Text` özellikleri herhangi bir değere (ad gibi) ayarlanabilir, ancak `Value` özellikleri veri alanının adı olarak ayarlanmalıdır (örneğin, ProductName). Sonuçları azalan düzende sıralamak için, açıklama dizesini, ÜrünAdı DESC gibi veri alanı adına ekleyin.

![Sıralanabilir veri alanlarının her biri için bir ListItem ekleyin](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**Şekil 5**: her sıralanabilir veri alanı için `ListItem` ekleme

Son olarak, DropDownList 'in sağına bir düğme web denetimi ekleyin. Yenilemek için `ID` `RefreshRepeater` ve `Text` özelliğini ayarlayın.

`ListItem` s oluşturup Yenile düğmesini ekledikten sonra, DropDownList ve düğme bildirim temelli sözdizimi şuna benzer olmalıdır:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

DropDownList 'in sıralanması tamamlandıktan sonra, bir sonraki `Selecting` olay işleyicisini, bir sabit kodlanmış sıralama ifadesinin aksine seçili `SortBy``ListItem` s `Value` özelliğini kullanacak şekilde güncelleştirmemiz gerekir.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample4.cs)]

Bu noktada, ilk olarak sayfa ilk kez ziyaret edildiğinde, `SortBy` `ListItem` varsayılan olarak seçilen `ProductName` veri alanı tarafından ilk olarak sıralanır. Şekil 6 ' ya bakın. Kategori gibi farklı bir sıralama seçeneği seçmek ve Yenile ' ye tıklamak, Şekil 7 ' nin gösterdiği gibi, bir geri göndermeye ve verileri kategori adına göre yeniden sıralamaya neden olur.

[Ürünlerin başlangıçta adına göre sıralandığı ![](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)

**Şekil 6**: Ürünler başlangıçta adına göre sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image16.png))

[![ürünler artık kategoriye göre sıralanır](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)

**Şekil 7**: ürünler artık kategoriye göre sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image19.png))

> [!NOTE]
> Yineleme düğmesine tıklamak, yineleyici s görünüm durumu devre dışı bırakıldığı için verilerin otomatik olarak yeniden sıralanmasını sağlar, böylece yineleyicisi 'nin her geri göndermede veri kaynağına yeniden bağlanmasına neden olur. Yineleyici s görünüm durumunu devre dışı bıraktıysanız, sıralama açılan listesinin değiştirilmesi sıralama düzeninde hiçbir etkisi olmayacaktır. Bu sorunu gidermek için, Yenile düğmesine `Click` olayı için bir olay işleyicisi oluşturun ve yineleyiciyi veri kaynağına yeniden bağlayın (Repeater s `DataBind()` yöntemini çağırarak).

## <a name="remembering-the-sort-expression-and-direction"></a>Sıralama Ifadesini ve yönünü anımsama

Sıralamayan ilgili geri göndermeler gerçekleşebileceği bir sayfada sıralanabilir bir DataList veya Repeater oluştururken sıralama ifadesinin ve yönünün geri göndermeler arasında hatırlandığından emin olun. Örneğin, bu öğreticideki yineleyicisi 'ni her ürünle birlikte bir Sil düğmesi içerecek şekilde güncelleştirdiğimiz hakkında düşünün. Kullanıcı Sil düğmesine tıkladığında, seçili ürünü silmek için bazı kodlar çalıştırın ve ardından verileri yineleyicisi 'ne yeniden bağlayın. Sıralama ayrıntıları geri gönderme boyunca kalıcı değilse, ekranda görüntülenen veriler orijinal sıralama sırasına geri döndürülür.

Bu öğretici için, DropDownList sıralama ifadesini ve yönünü ABD için görünüm durumuna dolaylı olarak kaydeder. Farklı bir sıralama arabirimi kullandığımızda, her zaman sıralama düzenini, geri göndermeler genelinde sıralamayı anımsamak için gereken çeşitli sıralama seçeneklerinin sağlandığı, deyin ve LinkButtons. Bu, sıralama parametrelerini QueryString içindeki sıralama parametresini ekleyerek veya başka bir durum kalıcılığı tekniğinin yanı sıra sayfa s Görünüm durumunda depolayarak gerçekleştirilebilir.

Bu öğreticideki gelecekteki örneklerde, sayfa s Görünüm durumunda sıralama ayrıntılarının nasıl kalıcı hale getirilecektir.

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>5\. Adım: varsayılan sayfalama kullanan bir DataList 'e sıralama desteği ekleme

[Önceki öğreticide](paging-report-data-in-a-datalist-or-repeater-control-cs.md) , bir DataList ile nasıl varsayılan sayfalama uygulanacağını inceliyoruz. Bu önceki örneği, disk belleğine alınan verileri sıralama yeteneğini kapsayacak şekilde genişletmenize izin verir. `PagingSortingDataListRepeater` klasöründeki `SortingWithDefaultPaging.aspx` ve `Paging.aspx` sayfalarını açarak başlayın. `Paging.aspx` sayfasında, sayfa bildirim temelli işaretlemesini görüntülemek için kaynak düğmesine tıklayın. Seçili metni kopyalayın (bkz. Şekil 8) ve `<asp:Content>` etiketleri arasında `SortingWithDefaultPaging.aspx` bildirime dayalı biçimlendirmeye yapıştırın.

[![, ASP: Content&gt; etiketleri disk belleği. aspx 'ten SortingWithDefaultPaging. aspx 'e &lt;](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)

**Şekil 8**: `Paging.aspx` `<asp:Content>` etiketlerinde bildirime dayalı işaretlemeyi `SortingWithDefaultPaging.aspx` çoğaltın ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image22.png))

Bildirim temelli biçimlendirmeyi kopyaladıktan sonra, `Paging.aspx` Page for Code-Behind sınıfındaki yöntemleri ve özellikleri `SortingWithDefaultPaging.aspx`için arka plan kod sınıfına kopyalayın. Sonra, `SortingWithDefaultPaging.aspx` sayfasını bir tarayıcıda görüntülemek için bir dakikanızı ayırın. Aynı işlevselliği ve görünümü `Paging.aspx`göstermelidir.

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>ProductsBLL 'yi, varsayılan bir sayfalama ve sıralama yöntemi Içerecek şekilde geliştirme

Önceki öğreticide, bir `PagedDataSource` nesnesi döndüren `ProductsBLL` sınıfında bir `GetProductsAsPagedDataSource(pageIndex, pageSize)` yöntemi oluşturduk. Bu `PagedDataSource` nesnesi *Tüm* ürünlerle doldurulmuştur (BLL s `GetProducts()` yöntemi aracılığıyla), ancak DataList 'e bağlandığında yalnızca belirtilen *pageIndex* ve *PageSize* giriş parametrelerine karşılık gelen kayıtlar görüntülenmediğinde.

Bu öğreticide daha önce, ObjectDataSource s `Selecting` olay işleyicisinden sıralama ifadesini belirterek sıralama desteği ekledik. Bu, ObjectDataSource, `GetProducts()` yöntemi tarafından döndürülen `ProductsDataTable` gibi sıralanabilen bir nesne döndürüldüğünde iyi bir şekilde çalışacaktır. Ancak, `GetProductsAsPagedDataSource` yöntemi tarafından döndürülen `PagedDataSource` nesnesi, iç veri kaynağının sıralanmasını desteklemez. Bunun yerine, `PagedDataSource`*yerleştirmeden önce* `GetProducts()` yönteminden döndürülen sonuçları sıralamak gerekir.

Bunu gerçekleştirmek için, `GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)``ProductsBLL` sınıfında yeni bir yöntem oluşturun. `GetProducts()` yöntemi tarafından döndürülen `ProductsDataTable` sıralamak için, varsayılan `DataTableView``Sort` özelliğini belirtin:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

`GetProductsSortedAsPagedDataSource` yöntemi, önceki öğreticide oluşturulan `GetProductsAsPagedDataSource` yönteminden biraz farklıdır. Özellikle, `GetProductsSortedAsPagedDataSource` ek bir giriş parametresi `sortExpression` kabul eder ve bu değeri `ProductDataTable` s `DefaultView``Sort` özelliğine atar. Daha sonra `PagedDataSource` nesne veri kaynağına daha sonra kod satırı `ProductDataTable` s `DefaultView`atanır.

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>GetProductsSortedAsPagedDataSource metodunu çağırma ve SortExpression giriş parametresinin değerini belirleme

`GetProductsSortedAsPagedDataSource` yöntemi tamamlandıktan sonra, bir sonraki adım bu parametre için değer sağlamaktır. `SortingWithDefaultPaging.aspx` ObjectDataSource Şu anda `GetProductsAsPagedDataSource` yöntemini çağırmak için yapılandırılmıştır ve `SelectParameters` koleksiyonunda belirtilen iki `QueryStringParameters`üzerinden iki giriş parametresini geçirir. Bu iki `QueryStringParameters`, `GetProductsAsPagedDataSource` yöntemi olan *pageIndex* ve *pageSize* parametrelerinin kaynağının `pageIndex` ve `pageSize`QueryString alanlarından geldiği anlamına gelir.

Yeni `GetProductsSortedAsPagedDataSource` yöntemini çağırabilmesi için ObjectDataSource s `SelectMethod` özelliğini güncelleştirin. Daha sonra, *SortExpression* giriş parametresine `sortExpression`QueryString alanından erişilmesi için yeni bir `QueryStringParameter` ekleyin. `QueryStringParameter` s `DefaultValue` ProductName olarak ayarlayın.

Bu değişikliklerden sonra, ObjectDataSource tarafından bildirim temelli biçimlendirme şöyle görünmelidir:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample6.aspx)]

Bu noktada, `SortingWithDefaultPaging.aspx` sayfası sonuçlarını ürün adına göre alfabetik olarak sıralar (bkz. Şekil 9). Bunun nedeni, varsayılan olarak ProductName 'in bir değerinin `GetProductsSortedAsPagedDataSource` yöntemi, *SortExpression* parametresi olarak geçirilir.

[Varsayılan olarak ![, sonuçlar ProductName 'e göre sıralanır](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)

**Şekil 9**: varsayılan olarak, sonuçlar `ProductName` göre sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image25.png))

`SortingWithDefaultPaging.aspx?sortExpression=CategoryName` gibi `sortExpression` QueryString alanını el ile eklerseniz, sonuçlar belirtilen `sortExpression`göre sıralanır. Ancak, farklı bir veri sayfasına geçerken bu `sortExpression` parametresi QueryString 'a dahil edilmez. Aslında, Ileri veya son sayfa düğmelerine tıklanması `Paging.aspx`! ' a geri dönerek! Ayrıca, şu anda sıralama arabirimi yok. Bir kullanıcının disk belleğine alınan verilerin sıralama düzenini değiştirme yöntemi, QueryString 'in doğrudan bir şekilde işlenmesiyle yapılabilir.

## <a name="creating-the-sorting-interface"></a>Sıralama arabirimi oluşturma

İlk olarak, kullanıcıyı `SortingWithDefaultPaging.aspx` (`Paging.aspx`yerine) göndermek ve `sortExpression` değerini QueryString öğesine eklemek için `RedirectUser` yöntemini güncelleştirmeniz gerekir. Ayrıca, salt okunurdur, sayfa düzeyinde adlandırılmış `SortExpression` özelliği de ekleyeceğiz. Bu özellik, önceki öğreticide oluşturulan `PageIndex` ve `PageSize` özelliklerine benzer şekilde, varsa `sortExpression` QueryString alanının değerini ve aksi durumda varsayılan değeri (ProductName) döndürür.

Şu anda `RedirectUser` yöntemi, görüntülenecek sayfanın dizinini yalnızca tek bir giriş parametresi kabul eder. Ancak, Kullanıcı QueryString içinde belirtilenden farklı bir sıralama ifadesi kullanarak kullanıcıyı belirli bir veri sayfasına yönlendirmek istediğimiz zamanlar olabilir. Kısa bir süre içinde, Bu sayfa için sıralama arabirimini oluşturacağız, bu da verileri belirtilen bir sütuna göre sıralamak için bir dizi düğme web denetimi içerir. Bu düğmelerden birine tıklandığında, uygun sıralama ifadesi değerini geçirerek kullanıcıyı yeniden yönlendirmek istiyoruz. Bu işlevi sağlamak için `RedirectUser` yönteminin iki sürümünü oluşturun. İlki görüntülenecek sayfa dizinini kabul etmelidir, ikincisi ise sayfa dizinini ve sıralama ifadesini kabul eder.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

Bu öğreticideki ilk örnekte, bir DropDownList kullanarak sıralama arabirimi oluşturduk. Bu örnekte, bir `ProductName`, bir `CategoryName`ve `SupplierName`için bir tane olmak üzere DataList 'in üzerine yerleştirilmiş üç düğme web denetimini kullanalım. Üç düğme web denetimini ekleyin, `ID` ve `Text` özelliklerini uygun şekilde ayarlar:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample8.aspx)]

Sonra, her biri için bir `Click` olay işleyicisi oluşturun. Olay işleyicileri, uygun sıralama ifadesini kullanarak kullanıcıyı ilk sayfaya döndüren `RedirectUser` yöntemini çağırmalıdır.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

Sayfa ilk kez ziyaret edildiğinde, veriler ürün adına alfabetik olarak sıralanır (Şekil 9 ' a geri bakın). İkinci veri sayfasına ilerlemek için Ileri düğmesine tıklayın ve kategoriye göre sırala düğmesine tıklayın. Bu, ilk veri sayfasına, kategori adına göre sıralanmış olarak döndürür (bkz. Şekil 10). Benzer şekilde, Tedarikçiye göre sırala düğmesine tıklamak, verilerin ilk sayfasından başlayarak tedarikçiye göre verileri sıralar. Sıralama seçeneği, verilerin sayfalandırılmış olduğu şekilde hatırlanır. Şekil 11 kategoriye göre sıraladıktan sonra sayfayı gösterir ve ardından verilerin on üç sayfasına ilerleden sonra.

[Ürünlerin kategoriye göre sıralandığı ![](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)

**Şekil 10**: Ürünler kategoriye göre sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image28.png))

[![sıralama Ifadesi veriler üzerinde sayfalama yapılırken hatırlanır](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image29.png)

**Şekil 11**: sıralama Ifadesi veriler üzerinde Sayfalandığınızda[hatırlanır (tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image31.png))

## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>Adım 6: bir yineleyici içindeki kayıtlar aracılığıyla özel sayfalama

DataList örneği, 1. adımda, verileri veri aracılığıyla verimsiz varsayılan sayfalama tekniğini kullanarak incelendi. Yeterince büyük miktarlarda veri sayfalaması yaparken özel sayfalama kullanılması zorunludur. [Büyük miktarlarda veri aracılığıyla etkili bir şekilde disk belleği](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) dosyası ve [özel](../paging-and-sorting/sorting-custom-paged-data-cs.md) disk belleği veri öğreticilerini sıralayarak, özel sayfalama kullanmak ve özel disk belleğine alınan verileri sıralamak için BLL 'de varsayılan ve özel sayfalama ve oluşturulan Yöntemler arasındaki farkları inceledik. Özellikle, bu iki önceki öğreticilerde, `ProductsBLL` sınıfına aşağıdaki üç yöntemi ekledik:

- `GetProductsPaged(startRowIndex, maximumRows)`, *StartRowIndex* 'ten başlayan ve *MaximumRows*'ı aşmayan belirli bir kayıt alt kümesini döndürür.
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)`, belirtilen *SortExpression* giriş parametresine göre sıralanan kayıtların belirli bir alt kümesini döndürür.
- `TotalNumberOfProducts()`, `Products` veritabanı tablosundaki toplam kayıt sayısını sağlar.

Bu yöntemler, DataList veya Repeater denetimi kullanılarak verileri verimli bir şekilde sayfa halinde sıralamak ve sıralamak için kullanılabilir. Bunu göstermek için, özel sayfalama desteğiyle bir yineleyici denetimi oluşturarak başlayalım. daha sonra sıralama özellikleri ekleyeceğiz.

`PagingSortingDataListRepeater` klasöründeki `SortingWithCustomPaging.aspx` sayfasını açın ve sayfaya bir yineleyici ekleyerek `ID` özelliğini `Products`olarak ayarlayarak. Yineleyici s akıllı etiketinden `ProductsDataSource`adlı yeni bir ObjectDataSource oluşturun. `ProductsBLL` sınıf s `GetProductsPaged` yönteminden verileri seçmek üzere yapılandırın.

[![, ObjectDataSource 'ı ProductsBLL Class s GetProductsPaged metodunu kullanacak şekilde yapılandırma](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image32.png)

**Şekil 12**: `ProductsBLL` Class s `GetProductsPaged` metodunu ([tam boyutlu görüntüyü görüntülemek Için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image34.png)) kullanmak üzere ObjectDataSource 'ı yapılandırın

GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden açılan listeleri (yok) ayarlayın ve ardından Ileri düğmesine tıklayın. Veri kaynağı Yapılandırma Sihirbazı şimdi `GetProductsPaged` yöntemi için *StartRowIndex* ve *MaximumRows* giriş parametrelerinin kaynaklarını ister. Gerçekte, bu giriş parametreleri yok sayılır. Bunun yerine, *StartRowIndex* ve *MaximumRows* değerleri, yalnızca bu öğretici 'Nin Ilk tanıtımı içinde *SortExpression* 'ı belirttiğimiz gibi, ObjectDataSource s `Selecting` olay işleyicisindeki `Arguments` özelliği aracılığıyla geçirilir. Bu nedenle, sihirbazda parametre kaynak açılan listelerini None ' da ayarlı olarak bırakın.

[Parametre kaynaklarını None olarak ayarlanmış ![bırak](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image35.png)

**Şekil 13**: parametre kaynaklarını yok olarak ayarlanmış bırakın ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image37.png))

> [!NOTE]
> ObjectDataSource `EnablePaging` özelliğini `true`*olarak ayarlamayın.* Bu, ObjectDataSource 'un kendi *StartRowIndex* ve *maximumrows* parametrelerini `SelectMethod` s var olan parametre listesine otomatik olarak dahil edememesine neden olur. `EnablePaging` özelliği, özel disk belleğine alınmış verileri bir GridView, DetailsView veya FormView denetimine bağlarken faydalıdır çünkü bu denetimler yalnızca `EnablePaging` özelliği `true`olduğunda kullanılabilir olan ObjectDataSource 'tan belirli davranışları bekliyor. DataList ve Repeater için sayfalama desteğini el ile eklememiz gerektiğinden, gerekli işlevselliğe doğrudan ASP.NET sayfamız dahilinde olacak şekilde, bu özelliği `false` (varsayılan) olarak bırakın.

Son olarak, ürün adı, kategori ve tedarikçinin gösterilmesi için Yineleyici s `ItemTemplate` tanımlayın. Bu değişikliklerden sonra, yineleyici ve ObjectDataSource 'lar bildirime dayalı sözdizimi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample10.aspx)]

Bir tarayıcı aracılığıyla sayfayı ziyaret etmek ve hiçbir kaydın döndürülmediğini göz önünde ayırın. Bunun nedeni, henüz *StartRowIndex* ve *MaximumRows* parametre değerlerini belirtmemiz ve Bu nedenle, 0 değerleri her ikisi için ' de geçirilir. Bu değerleri belirtmek için, ObjectDataSource s `Selecting` olayı için bir olay işleyicisi oluşturun ve bu parametre değerlerini sırasıyla 0 ve 5 sabit kodlanmış değerler olarak ayarlayın:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample11.cs)]

Bu değişiklik ile, sayfa bir tarayıcı aracılığıyla görüntülenirken ilk beş ürünü gösterir.

[Ilk beş kayıt ![görüntülenir](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image38.png)

**Şekil 14**: Ilk beş kayıt görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image40.png))

> [!NOTE]
> Şekil 14 ' te listelenen ürünlerin, etkin özel disk belleği sorgusunu gerçekleştiren `GetProductsPaged` saklı yordamı, sonuçları `ProductName`olarak sipariş ettiğinden ürün adına göre sıralanması önerilir.

Kullanıcının sayfalarda ilerleyebilmesi için başlangıç satırı dizinini ve en yüksek satırları takip etmemiz ve bu değerleri geri göndermeler genelinde unutmamanız gerekir. Varsayılan disk belleği örneğinde, bu değerleri kalıcı hale getirmek için QueryString alanlarını kullandınız; Bu tanıtımda, bu bilgileri sayfa s Görünüm durumunda kalıcı hale getirin. Aşağıdaki iki özelliği oluşturun:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample12.cs)]

Ardından, seçme olay işleyicisindeki kodu, sabit kodlu 0 ve 5 değerleri yerine `StartRowIndex` ve `MaximumRows` özelliklerini kullanacak şekilde güncelleştirin:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample13.cs)]

Bu noktada sayfamızda hala yalnızca ilk beş kayıt gösteriliyor. Ancak, bu özelliklerle birlikte sayfalama arabirimimizi oluşturmaya hazırız.

## <a name="adding-the-paging-interface"></a>Sayfalama arabirimi ekleme

Verilerin hangi sayfada görüntülendiğini ve toplam sayfa olduğunu gösteren etiket Web denetimi de dahil olmak üzere varsayılan disk belleği örneğinde kullanılan Ilk, önceki, sonraki, son sayfalama arabirimini kullanalım. Dört düğme web denetimini ve etiketini, yineleyicisi altına ekleyin.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample14.aspx)]

Sonra, dört düğme için `Click` olay işleyicileri oluşturun. Bu düğmelerden birine tıklandığında `StartRowIndex` güncelleştirmemiz ve verileri yineleyicisi 'ne yeniden bağlamanız gerekir. Ilk, önceki ve sonraki düğmelerin kodu yeterince basittir, ancak son düğme için verilerin son sayfası için başlangıç satırı dizinini nasıl belirliyoruz? Bu dizini hesaplamak ve bir sonraki ve son düğmelerin etkinleştirilip etkinleştirilmeyeceğini belirleyebilmemiz için toplamda kaç kaydın sayfalanmakta olduğunu bilmemiz gerekir. Bunu, `ProductsBLL` sınıf s `TotalNumberOfProducts()` metodunu çağırarak belirleyebiliriz. Bir `TotalNumberOfProducts()` yönteminin sonuçlarını döndüren `TotalRowCount` adlı salt okunurdur, sayfa düzeyi özelliği oluşturalım:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample15.cs)]

Bu özellik ile artık son sayfa başlangıç satırı dizinini belirleyebiliriz. Özellikle, `TotalRowCount` eksi 1 ' in tamsayı sonucu `MaximumRows`, `MaximumRows`ile çarpılır. Artık dört sayfalama arabirimi düğmesi için `Click` olay işleyicilerini yazabiliriz:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample16.cs)]

Son olarak, son sayfayı görüntülerken verilerin ilk sayfasını ve sonraki ve son düğmeleri görüntülerken sayfalama arabirimindeki Ilk ve önceki düğmeleri devre dışı bıraktık. Bunu gerçekleştirmek için, ObjectDataSource s `Selecting` olay işleyicisine aşağıdaki kodu ekleyin:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample17.cs)]

Bu `Click` olay işleyicilerini ve kodu, geçerli başlangıç satırı dizinine göre disk belleği arabirimi öğelerini etkinleştirmek veya devre dışı bırakmak üzere ekledikten sonra, sayfayı bir tarayıcıda test edin. Şekil 15 ' te gösterildiği gibi, ilk ve önceki düğmeler devre dışı bırakılır. Ileri ' ye tıkladığınızda ikinci veri sayfası gösterilir. son ' a tıkladığınızda son sayfa görüntülenir (bkz. Şekil 16 ve 17). Verilerin son sayfasını görüntülerken, hem Ileri hem de son düğmelerin devre dışı bırakılması.

[Ürünlerin Ilk sayfası görüntülenirken Önceki ve son düğmelerin devre dışı bırakılması ![](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image41.png)

**Şekil 15**: ürünlerin Ilk sayfası görüntülenirken Önceki ve son düğmeler devre dışıdır ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image43.png))

[Ürünlerin Ikinci sayfası ![görüntülenir](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image44.png)

**Şekil 16**: ürünlerin Ikinci sayfası görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image46.png))

[Son tık![verinin son sayfasını görüntüler](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image47.png)

**Şekil 17**: son ' a tıkladığınızda verilerin son sayfası görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image49.png))

## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>7\. Adım: özel disk belleğine alınmış yineleyicisi ile sıralama desteğini ekleme

Özel sayfalama uygulandığına göre, sıralama desteğini eklemeye hazırız. `ProductsBLL` sınıf s `GetProductsPagedAndSorted` yöntemi `GetProductsPaged`olarak aynı *StartRowIndex* ve *MaximumRows* giriş parametrelerine sahiptir, ancak ek bir *SortExpression* giriş parametresine izin verir. `SortingWithCustomPaging.aspx``GetProductsPagedAndSorted` yöntemi kullanmak için aşağıdaki adımları gerçekleştirmemiz gerekir:

1. `GetProductsPaged` ObjectDataSource `SelectMethod` özelliğini `GetProductsPagedAndSorted`olarak değiştirin.
2. ObjectDataSource s `SelectParameters` koleksiyonuna bir *SortExpression* `Parameter` nesnesi ekleyin.
3. Sayfa s görünüm durumu ile geri alma boyunca değerini devam eden bir özel, sayfa düzeyi `SortExpression` özelliği oluşturun.
4. ObjectDataSource s `Selecting` olay işleyicisini, sayfa düzeyi `SortExpression` özelliğinin değerini, ObjectDataSource 'un *SortExpression* parametresini atamak için güncelleştirin.
5. Sıralama arabirimini oluşturun.

ObjectDataSource `SelectMethod` özelliğini güncelleştirerek ve bir *SortExpression* `Parameter`ekleyerek başlayın. *SortExpression* `Parameter` s `Type` özelliğinin `String`olarak ayarlandığından emin olun. Bu ilk iki görevi tamamladıktan sonra, ObjectDataSource tarafından bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample18.aspx)]

Daha sonra, değeri görünüm durumuna serileştirilmiş bir sayfa düzeyi `SortExpression` özelliğine ihtiyacımız var. Sıralama ifadesi değeri ayarlanmamışsa, varsayılan olarak ProductName kullanın:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample19.cs)]

ObjectDataSource `GetProductsPagedAndSorted` yöntemi çağırmadan önce, *SortExpression* `Parameter` `SortExpression` özelliğinin değerine ayarlamanız gerekir. `Selecting` olay işleyicisine aşağıdaki kod satırını ekleyin:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample20.cs)]

Her şey sıralama arabirimini uygulamaktır. Son örnekte yaptığımız gibi, kullanıcının sonuçları ürün adına, kategoriye veya tedarikçiye göre sıralamasına izin veren üç düğme web denetimi kullanılarak sıralama arabirimine sahip olmam gerekir.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample21.aspx)]

Bu üç düğme denetimi için `Click` olay işleyicileri oluşturun. Olay işleyicisinde `StartRowIndex` 0 olarak sıfırlayın, `SortExpression` uygun değere ayarlayın ve verileri yineleyicisi 'ne yeniden bağlayın:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample22.cs)]

İşte bu kadar! Özel sayfalama ve sıralama uygulanmış bir dizi adım olsa da, adımlar varsayılan sayfalama için gerekenlere çok benzer. Şekil 18, kategoriye göre sıralandığında verilerin son sayfasını görüntülerken ürünleri gösterir.

[Verilerin son sayfasını kategoriye göre sıralanmış olarak ![görüntülenir](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image50.png)

**Şekil 18**: kategoriye göre sıralanmış verilerin son sayfası görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image52.png))

> [!NOTE]
> Önceki örneklerde, "tedarikçisine göre sıralama sıralama ifadesi olarak kullanılmıştır. Ancak, özel disk belleği uygulamasının kullanılması için CompanyName ' i kullanmanız gerekir. Bunun nedeni, özel sayfalama `GetProductsPagedAndSorted` uygulamaktan sorumlu saklı yordamın sıralama ifadesini `ROW_NUMBER()` anahtar sözcüğüne geçirmesidir, `ROW_NUMBER()` anahtar sözcüğü bir diğer ad yerine gerçek sütun adını gerektirir. Bu nedenle, sıralama ifadesi için `SELECT` sorgusunda (`SupplierName`) kullanılan diğer ad yerine `CompanyName` (`Suppliers` tablosundaki sütunun adı) kullanılmalıdır.

## <a name="summary"></a>Özet

DataList veya Repeater, yerleşik sıralama desteği sunmaz, ancak bir bit kod ve özel sıralama arabirimi ile bu tür işlevler eklenebilir. Sıralamayı uygularken, sayfalama ifadesi, ObjectDataSource s `Select` yöntemine geçirilen `DataSourceSelectArguments` nesnesi aracılığıyla belirtilebilir. Bu `DataSourceSelectArguments` nesne s `SortExpression` özelliği, ObjectDataSource s `Selecting` olay işleyicisine atanabilir.

Zaten disk belleği desteği sağlayan bir DataList veya Repeater öğesine sıralama özellikleri eklemek için en kolay yaklaşım, Iş mantığı katmanını sıralama ifadesi kabul eden bir yöntemi içerecek şekilde özelleştirmenin bir yoludur. Bu bilgiler daha sonra ObjectDataSource `SelectParameters`bir parametre aracılığıyla geçirilebilir.

Bu öğreticide, sayfalama, DataList ve Repeater denetimleriyle sıralama ile ilgili İnceleme işlemi tamamlanır. Bir sonraki ve son öğreticimiz, öğe temelinde özel, Kullanıcı tarafından başlatılan bir işlevsellik sağlamak için DataList ve Repeater s şablonlarına nasıl düğme Web denetimleri ekleneceğini inceleyeceksiniz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren, David suru idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](paging-report-data-in-a-datalist-or-repeater-control-cs.md)
> [İleri](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
