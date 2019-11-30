---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
title: Iki sayfa üzerinde ana/ayrıntı filtreleme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, ana/ayrıntı raporunu iki sayfada nasıl ayıracağız. ' Ana ' sayfasında bir CATEG listesini işlemek için bir yineleyici denetimi kullanıyoruz...
ms.author: riande
ms.date: 10/30/2010
ms.assetid: 68b8c023-92fa-4df6-9563-1764e16e4b04
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 545b24a66476c55aff88ac62d3a6528105fea6c0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74631381"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>İki Sayfada Ana/Ayrıntı Filtreleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_CS.exe) veya [PDF 'yi indirin](master-detail-filtering-acess-two-pages-datalist-cs/_static/datatutorial34cs1.pdf)

> Bu öğreticide, ana/ayrıntı raporunu iki sayfada nasıl ayıracağız. "Ana" sayfada, tıklandığı sırada kullanıcıyı iki sütunlu bir DataList 'in seçili kategoriye ait bu ürünleri gösterdiği "Ayrıntılar" sayfasına alacak bir yineleyici denetimi kullanıyoruz.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](master-detail-filtering-with-a-dropdownlist-datalist-cs.md) , "Ayrıntılar" göstermek için "ana" kayıtları ve bir DataList listesini göstermek üzere dropdownlists kullanarak ana/ayrıntı raporlarının tek bir Web sayfasında nasıl görüntüleneceğini gördük. Ana/ayrıntı raporlarında kullanılan diğer yaygın bir düzende, bir Web sayfasında ana kayıtlar ve diğer ayrıntılar yer alır. [Iki sayfa boyunca daha önceki ana/ayrıntı filtrelemesinde](../masterdetail/master-detail-filtering-across-two-pages-cs.md) , sistemdeki tüm tedarikçileri göstermek için GridView kullanarak bu kalıbı inceledik. Bu GridView, ikinci bir sayfaya bağlantı olarak işlenen ve QueryString içindeki `SupplierID` geçen bir Hyperlinkalanı içeriyordu. İkinci sayfa, seçili tedarikçinin sunduğu ürünleri listelemek için bir GridView kullandı.

Bu tür iki sayfalı ana/ayrıntı raporları, DataList ve Repeater denetimleri kullanılarak da gerçekleştirilebilir. Tek fark, DataList veya Repeater, HyperLinkField denetimi için destek sağlamaz. Bunun yerine, denetimin `ItemTemplate`içinde köprü Web denetimi veya bir tutturucu HTML öğesi (`<a>`) eklememiz gerekir. Köprünün `NavigateUrl` özelliği ya da bağlayıcının `href` özniteliği, bildirim temelli veya programlı yaklaşımlar kullanılarak özelleştirilebilir.

Bu öğreticide, bir yineleyici denetimi kullanarak bir sayfada bir madde işaretli listedeki kategorileri listeleyen bir örnek inceleyeceğiz. Her liste öğesi kategorinin adını ve açıklamasını, kategori adı ise ikinci bir sayfaya bağlantı olarak görüntülenecek şekilde içerecektir. Bu bağlantıya tıkladığınızda, bir DataList 'in seçili kategoriye ait bu ürünleri göstereceği ikinci sayfaya Kullanıcı tarafından gönderilir.

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>1\. Adım: kategorileri madde Işaretli bir listede görüntüleme

Ana/ayrıntı raporu oluşturmanın ilk adımı, "ana" kayıtları görüntüleyerek başlamadır. Bu nedenle ilk göreviniz, kategorileri "ana" sayfada görüntülemektir. `DataListRepeaterFiltering` klasöründeki `CategoryListMaster.aspx` sayfasını açın, bir yineleyici denetimi ekleyin ve akıllı etiketinden yeni bir ObjectDataSource eklemeyi tercih edin. Yeni ObjectDataSource 'ı, `CategoriesBLL` sınıfının `GetCategories` yönteminden verilerine erişmesi için yapılandırın (bkz. Şekil 1).

[![, ObjectDataSource 'un CategoriesBLL sınıfının GetCategories metodunu kullanacak şekilde yapılandırılması](master-detail-filtering-acess-two-pages-datalist-cs/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image1.png)

**Şekil 1**: `CategoriesBLL` sınıfının `GetCategories` metodunu kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image3.png))

Sonra, yineleyicisi 'nin şablonlarını, her kategori adını ve açıklamasını madde işaretli bir listedeki bir öğe olarak görüntüleyen şekilde tanımlayın. Ayrıntılar sayfasına her bir kategorinin bağlantısını almak henüz kaygılanmıyor. Yineleyicisi ve ObjectDataSource için bildirim temelli biçimlendirmeyi aşağıda gösterilmektedir:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample1.aspx)]

Bu biçimlendirme tamamlanmasından sonra bir tarayıcıdan ilerleme durumunu görüntülemek için bir süre bekleyin. Şekil 2 ' de gösterildiği gibi, yineleyici her kategorinin adını ve açıklamasını gösteren bir madde işaretli liste olarak işlenir.

[![her kategori bir madde Işaretli liste öğesi olarak görüntülenir](master-detail-filtering-acess-two-pages-datalist-cs/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image4.png)

**Şekil 2**: her kategori bir madde Işaretli liste öğesi olarak görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image6.png))

## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>2\. Adım: kategori adını Ayrıntılar sayfasının bir bağlantısına açma

Bir kullanıcının belirli bir kategori için "Ayrıntılar" bilgilerini görüntülemesine izin vermek için, tıklandığında her madde işaretli liste öğesine bir bağlantı eklememiz gerekir (`ProductsForCategoryDetails.aspx`). Bu ikinci sayfa daha sonra seçili kategori için bir DataList kullanılarak ürünleri görüntüler. Bağlantısını tıklamış olan kategoriyi belirleyebilmek için, tıklanan kategorinin `CategoryID` bir mekanizmadan ikinci sayfaya geçirmemiz gerekir. Skalar verileri bir sayfadan diğerine aktarmanın en basit ve en kolay yolu, bu öğreticide kullanacağımız seçenek olan QueryString ' dir. Özellikle `ProductsForCategoryDetails.aspx` sayfası, seçilen *`categoryID`* değerinin `CategoryID`adlı bir QueryString alanından geçirilmesini bekler. Örneğin, `CategoryID` 1 olan meşrubat kategorisinin ürünlerini görüntülemek için, bir Kullanıcı `ProductsForCategoryDetails.aspx?CategoryID=1`ziyaret edebilir.

Yineleyicisi 'ndeki her madde işaretli liste öğesi için bir köprü oluşturmak üzere `ItemTemplate`bir köprü Web denetimi ya da HTML Tutturucu öğesi (`<a>`) eklemeniz gerekir. Köprünün her satır için aynı görüntülendiği senaryolarda, iki yaklaşım da yeterli olacaktır. Repeaters için Tutturucu öğesini kullanmayı tercih ediyorum. Tutturucu öğesini kullanmak için, yineleyicisi 'nin ItemTemplate 'i şu şekilde güncelleştirin:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample2.aspx)]

`CategoryID` doğrudan bağlama öğesinin `href` özniteliği içinde eklenebileceğini unutmayın. Ancak bunu yapmak için, `href` özniteliği içindeki `Eval` yöntemi kendi dizesini (`"CategoryID"`) tırnak işaretleriyle ayırdığından, `href` özniteliğinin değerini kesme işareti (ve Notda tırnak işaretleriyle) sınırlandırmalıdır. Bunun yerine köprü Web denetimi de kullanılabilir:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample3.aspx)]

URL 'nin statik kısmının (`ProductsForCategoryDetails.aspx?CategoryID`), dize birleştirme kullanarak doğrudan veri bağlama söz dizimi içinde `Eval("CategoryID")` sonucuna nasıl ekleneceğini aklınızda edin.

Köprü denetimini kullanmanın bir avantajı, gerektiğinde yineleyicinin `ItemDataBound` olay işleyiciden programlı bir şekilde erişilebilmesini kullanmaktır. Örneğin, kategori adını, ilişkili ürünleri olmayan kategoriler için bağlantı yerine metin olarak göstermek isteyebilirsiniz. Böyle bir denetim `ItemDataBound` olay işleyicisinde program aracılığıyla gerçekleştirilebilir; ilişkili ürünleri olmayan kategoriler için, köprünün `NavigateUrl` özelliği boş bir dizeye ayarlanabilir ve bu nedenle, bu kategori adının bir bağlantı olarak düz metin olarak oluşturulmasına neden olur. DataList ve Repeater 'ın içeriğini `ItemDataBound` olay işleyicisi aracılığıyla programlı mantığa göre biçimlendirme hakkında daha fazla bilgi için veri öğreticisine [göre DataList ve Repeater biçimlendirme](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md) bilgilerine bakın.

Üzerinde takip ediyorsanız, sayfanızda tutturucu öğe veya köprü denetimi yaklaşımını kullanabilirsiniz. Yaklaşımdan bağımsız olarak, sayfayı bir tarayıcı aracılığıyla görüntülerken her kategori adı `ProductsForCategoryDetails.aspx`bir bağlantı olarak işlenmeli ve ilgili `CategoryID` değerini geçirerek (bkz. Şekil 3).

[Kategori adlarını şimdi ![ProductsForCategoryDetails. aspx bağlantısına bağlayın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image7.png)

**Şekil 3**: Kategori adları artık `ProductsForCategoryDetails.aspx` bağlantı kuruyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image9.png))

## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>3\. Adım: seçili kategoriye ait ürünleri listeleme

`CategoryListMaster.aspx` sayfası tamamlandığımızda, "Ayrıntılar" sayfasının `ProductsForCategoryDetails.aspx`uygulanması için ilgilenmeniz için hazırız. Bu sayfayı açın, araç kutusu ' ndan tasarımcı üzerine bir DataList sürükleyin ve `ID` özelliğini `ProductsInCategory`olarak ayarlayın. Sonra, DataList 'in akıllı etiketinden sonra sayfaya yeni bir ObjectDataSource eklemek ve `ProductsInCategoryDataSource`adlandırırken seçin. `ProductsBLL` sınıfının `GetProductsByCategoryID(categoryID)` yöntemini çağıracak şekilde yapılandırın; INSERT, UPDATE ve DELETE sekmelerindeki açılan listeleri (None) olarak ayarlayın.

[![, ObjectDataSource 'ı ProductsBLL sınıfının Getproductsbycategoryıd (CategoryID) metodunu kullanacak şekilde yapılandırın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image10.png)

**Şekil 4**: `ProductsBLL` sınıfının `GetProductsByCategoryID(categoryID)` metodunu kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image12.png))

`GetProductsByCategoryID(categoryID)` yöntemi bir giriş parametresini kabul ettiğinden ( *`categoryID`* ), veri kaynağı seçme Sihirbazı, parametrenin kaynağını belirtmek için bize bir fırsat sunar. QueryStringField `CategoryID`kullanarak parametre kaynağını QueryString olarak ayarlayın.

[![parametre kaynağı olarak CategoryID alan QueryString alanını kullanın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image13.png)

**Şekil 5**: parametre kaynağı olarak `CategoryID` QueryString alanını kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image15.png))

Önceki öğreticilerde gördüğünüz gibi, veri kaynağı seçme Sihirbazı ' nı tamamladıktan sonra, Visual Studio her bir veri alanı adını ve değerini listeleyen DataList için otomatik olarak bir `ItemTemplate` oluşturur. Bu şablonu yalnızca ürünün adını, tedarikçiyi ve fiyatını listeleyen bir ile değiştirin. Ayrıca, DataList 'in `RepeatColumns` özelliğini 2 olarak ayarlayın. Bu değişikliklerden sonra, DataList ve ObjectDataSource 'un bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample4.aspx)]

Bu sayfayı eylemde görüntülemek için `CategoryListMaster.aspx` sayfasından başlayın; sonra, Kategoriler madde işaretli listesinde bir bağlantıya tıklayın. Bunun yapılması, sorgu QueryString aracılığıyla `CategoryID` iletmek için sizi `ProductsForCategoryDetails.aspx`götürür. `ProductsForCategoryDetails.aspx` `ProductsInCategoryDataSource` ObjectDataSource, belirtilen kategori için yalnızca bu ürünleri alır ve her satır için iki ürün işleyen DataList 'te görüntüler. Şekil 6 ' da, Içecek görüntülenirken `ProductsForCategoryDetails.aspx` ekran görüntüsü gösterilir.

[Içecek ![satır başına Iki olarak görüntülenir](master-detail-filtering-acess-two-pages-datalist-cs/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image16.png)

**Şekil 6**: meşrular her satır için iki ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image18.png))

## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>4\. Adım: ProductsForCategoryDetails. aspx üzerinde kategori bilgilerini görüntüleme

Kullanıcı `CategoryListMaster.aspx`bir kategoriye tıkladığında, `ProductsForCategoryDetails.aspx` uygulanır ve seçili kategoriye ait ürünleri gösterilir. Ancak `ProductsForCategoryDetails.aspx` ' de, hangi kategorinin seçildiklerinize ilişkin görsel ipucu yok. Alkolları tıklaması gereken ancak koşullu olarak tıklanan bir Kullanıcı, `ProductsForCategoryDetails.aspx`ulaştıklarında hata sayısını yerine getirmenin bir yolu yoktur. Bu olası sorunu gidermek için, `ProductsForCategoryDetails.aspx` sayfasının üst kısmında seçili kategori (adı ve açıklaması) hakkındaki bilgileri görüntüleriz.

Bunu gerçekleştirmek için, `ProductsForCategoryDetails.aspx`Yineleyici denetiminin üstüne bir FormView ekleyin. Daha sonra, FormView 'un `CategoryDataSource` adlı akıllı etiketindeki sayfaya yeni bir ObjectDataSource ekleyin ve `CategoriesBLL` sınıfının `GetCategoryByCategoryID(categoryID)` metodunu kullanacak şekilde yapılandırın.

[Kategorilerbll sınıfının Getcategorybycategoryıd (CategoryID) yöntemi aracılığıyla kategori hakkında erişim bilgileri ![](master-detail-filtering-acess-two-pages-datalist-cs/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image19.png)

**Şekil 7**: `CategoriesBLL` sınıfının `GetCategoryByCategoryID(categoryID)` yöntemi aracılığıyla kategori hakkındaki bilgilere erişin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image21.png))

Adım 3 ' te eklenen `ProductsInCategoryDataSource` ObjectDataSource sayesinde, `CategoryDataSource`veri kaynağı Yapılandırma Sihirbazı bize `GetCategoryByCategoryID(categoryID)` yönteminin giriş parametresi için bir kaynak ister. Önceki şekilde aynı ayarları kullanın, parametre kaynağını QueryString ve QueryStringField değerini `CategoryID` olarak ayarlayıp Şekil 5 ' e geri bakın).

Sihirbazı tamamladıktan sonra, Visual Studio FormView için otomatik olarak bir `ItemTemplate`, `EditItemTemplate`ve `InsertItemTemplate` oluşturur. Salt okunurdur bir arabirim sağladığımızdan, `EditItemTemplate` ve `InsertItemTemplate`kaldırmayı ücretsiz olarak hissetmekten çekinmeyin. Ayrıca, FormView 'un `ItemTemplate`özelleştirmeyi de ücretsiz olarak kullanabilirsiniz. Gereksiz şablonları kaldırdıktan ve ItemTemplate 'i özelleştirdikten sonra, FormView ve ObjectDataSource 'un bildirime dayalı biçimlendirmesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample5.aspx)]

Şekil 8 ' de bu sayfayı bir tarayıcı aracılığıyla görüntülerken ekran görüntüsü gösterilir.

> [!NOTE]
> FormView 'a ek olarak, kullanıcıyı Kategori listesine geri alacak olan FormView 'un üzerine bir köprü denetimi de ekledik (`CategoryListMaster.aspx`). Bu bağlantıyı başka bir yere yerleştirebilirsiniz veya tamamen atlayabilirsiniz.

[![kategori bilgileri artık sayfanın en üstünde görüntülenir](master-detail-filtering-acess-two-pages-datalist-cs/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image22.png)

**Şekil 8**: kategori bilgileri artık sayfanın üstünde görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image24.png))

## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>5\. Adım: seçili kategoriye ait ürün yoksa bir Ileti görüntüleme

`CategoryListMaster.aspx` sayfası, ilişkili ürünlerin olup olmamasına bakılmaksızın sistemdeki tüm kategorileri listeler. Kullanıcı ilişkili ürünleri olmayan bir kategoriye tıklarsa, `ProductsForCategoryDetails.aspx` içindeki DataList işlenmeyecektir, çünkü veri kaynağı herhangi bir öğeye sahip olmayacaktır. Önceki öğreticilerde gördüğünüze göre GridView, veri kaynağında kayıt yoksa görüntülenecek bir kısa mesaj belirtmek için kullanılabilecek bir `EmptyDataText` özelliği sağlar. Ne yazık ki, DataList veya Repeater böyle bir özelliğe sahip değil.

Kullanıcıya seçili kategori için eşleşen bir ürün olmadığını bildiren bir ileti görüntülemek için, `Text` özelliğine eşleşen bir ürün olmadığı durumda görüntülenecek ileti atanmış olan sayfaya bir etiket denetimi eklememiz gerekir. Daha sonra, DataList 'in herhangi bir öğe içerip içermediğini temel alarak `Visible` özelliğini programlı bir şekilde ayarlayacağız.

Bunu gerçekleştirmek için, DataList 'in altına bir etiket ekleyerek başlayın. `ID` özelliğini `NoProductsMessage` ve `Text` özelliğini "Seçili Kategori için hiç ürün yok..." olarak ayarlayın. Daha sonra, bu etiketin `Visible` özelliğini, `ProductsInCategory` DataList 'e bağlı olup olmadığına bağlı olarak programlı bir şekilde ayarlayacağız. Bu atama, veriler DataList 'e bağlandıktan sonra yapılmalıdır. GridView, DetailsView ve FormView için, denetimin `DataBound` olayı için, veri bağlama işlemi tamamlandıktan sonra harekete bir olay işleyicisi oluşturuyoruz. Ancak, DataList veya Repeater 'ın kullanılabilir `DataBound` olayı yok.

Bu belirli örnekte, verilerin sayfanın `Load` olayından önce DataList 'e atandıklarından `Page_Load` olay işleyicisine etiketin `Visible` özelliğini atayabiliriz. Ancak, ObjectDataSource 'daki veriler, sayfanın yaşam döngüsünün daha sonra DataList 'e bağlanmışsa, bu yaklaşım genel durumda çalışmayacaktır. Örneğin, görüntülenen veriler başka bir denetimdeki değere dayanıyorsa (örneğin, "ana" kayıtları tutmak üzere bir DropDownList kullanarak bir ana/ayrıntı raporu görüntülerken, veriler sayfanın yaşam döngüsünde `PreRender` aşamasına kadar veri Web denetimine yeniden bağlanmayabilir.

Tüm durumlar için çalışacak bir çözüm, `Item` veya `AlternatingItem`öğe türü bağlanırken DataList 'in `ItemDataBound` (veya `ItemCreated`) olay işleyicisindeki `False` `Visible` özelliğini atacaktır. Böyle bir durumda, veri kaynağında en az bir veri öğesi olduğunu ve bu nedenle `NoProductsMessage` etiketini gizleyebileceğinizi biliyoruz. Bu olay işleyicisine ek olarak, etiketin `Visible` özelliğini `True`olarak başladığımızda, DataList 'in `DataBinding` olayı için de bir olay işleyicisine ihtiyacımız var. `DataBinding` olayı `ItemDataBound` etkinlikden önce başlatıldığından, etiketin `Visible` özelliği başlangıçta `True`olarak ayarlanır; Ancak herhangi bir veri öğesi varsa, `False`olarak ayarlanır. Aşağıdaki kod bu mantığı uygular:

[!code-csharp[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample6.cs)]

Northwind veritabanındaki tüm kategoriler bir veya daha fazla ürünle ilişkilidir. Bu özelliği test etmek için, bu öğreticide bulunan Northwind veritabanını el ile ayarladım ve (`CategoryID` = 7) üretim kategorisiyle ilişkili tüm ürünleri Mevsimyiyecek kategorisine (`CategoryID` = 8) yeniden atanıyor. Bu, yeni sorgu ' yı seçerek ve aşağıdaki `UPDATE` ifadesiyle kullanılarak Sunucu Gezgini gerçekleştirilebilir:

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample7.sql)]

Veritabanını uygun şekilde güncelleştirdikten sonra, `CategoryListMaster.aspx` sayfasına dönün ve üretim bağlantısına tıklayın. Artık üretim kategorisine ait hiçbir ürün bulunmadığından, "Seçili Kategori için hiç ürün yok..." seçeneğini görmeniz gerekir. Şekil 9 ' da gösterildiği gibi iletisi.

[Seçili kategoriye ait bir ürün yoksa bir Ileti ![görüntülenir](master-detail-filtering-acess-two-pages-datalist-cs/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image25.png)

**Şekil 9**: seçili kategoriye ait bir ürün yoksa bir ileti görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-acess-two-pages-datalist-cs/_static/image27.png))

## <a name="summary"></a>Özet

Ana/ayrıntı raporları hem ana hem de ayrıntı kayıtlarını tek bir sayfada görüntüleyebilir, ancak birçok Web sitesinde iki Web sayfasında ayrılır. Bu öğreticide, "ana" Web sayfasında bir yineleyici ve "Ayrıntılar" sayfasında listelenen ilişkili ürünler kullanılarak madde işaretli bir listede listelenen kategorilerin bulunduğu bir ana/ayrıntı raporunu nasıl uygulayacağınızı inceledik. Ana Web sayfasındaki her liste öğesi, satırın `CategoryID` değeri üzerinde geçen Ayrıntılar sayfasının bağlantısını içerir.

Ayrıntılar sayfasında, belirtilen tedarikçi için bu ürünleri almak `ProductsBLL` sınıfının `GetProductsByCategoryID(categoryID)` yöntemi aracılığıyla gerçekleştirildi. *`categoryID`* parametre değeri, parametre kaynağı olarak `CategoryID` QueryString değeri kullanılarak bildirimli olarak belirtildi. Ayrıca, ayrıntılar sayfasında, bir FormView kullanarak kategori ayrıntılarının nasıl görüntüleneceği ve seçilen kategoriye ait bir ürün yoksa bir iletinin nasıl görüntüleneceği konusunda da bakıyoruz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler...

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Zack Jones ve Liz Shulok. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](master-detail-filtering-with-a-dropdownlist-datalist-cs.md)
> [İleri](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
