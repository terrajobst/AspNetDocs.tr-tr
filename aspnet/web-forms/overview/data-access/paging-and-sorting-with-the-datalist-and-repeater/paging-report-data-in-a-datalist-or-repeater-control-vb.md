---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-vb
title: DataList veya Repeater denetiminde rapor verilerini sayfalama (VB) | Microsoft Docs
author: rick-anderson
description: DataList veya Repeater, otomatik sayfalama veya sıralama desteği sunmaz, ancak bu öğretici, DataList veya Repeater 'a sayfalama desteğinin nasıl ekleneceğini gösterir,...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: bbd6b7f7-b98a-48b4-93f3-341d6a4f53c0
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c65ca1f263e41748d99323dbdf1c28fdd077246
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74570019"
---
# <a name="paging-report-data-in-a-datalist-or-repeater-control-vb"></a>DataList veya Repeater Denetiminde Rapor Verilerini Sayfalama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_VB.exe) veya [PDF 'yi indirin](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial44vb1.pdf)

> DataList veya Repeater, otomatik sayfalama veya sıralama desteği sunurken, bu öğreticide, çok daha esnek disk belleği ve veri görüntüleme arabirimlerine olanak tanıyan DataList veya Repeater 'a disk belleği desteğinin nasıl ekleneceği gösterilmektedir.

## <a name="introduction"></a>Giriş

Sayfalama ve sıralama, verileri çevrimiçi bir uygulamada görüntülerken iki çok yaygın özelliklerdir. Örneğin, çevrimiçi bir kitaplığı 'nda ASP.NET kitaplar aranırken, bu tür kitaplar bulunabilir, ancak arama sonuçlarını listeleyen rapor her sayfa için yalnızca on eşleşme listeler. Üstelik, sonuçlar başlık, Fiyat, sayfa sayısı, yazar adı vb. ile sıralanabilir. [Sayfalama ve sıralama rapor verileri](../paging-and-sorting/paging-and-sorting-report-data-vb.md) öğreticisinde anlatıldığı gibi, GridView, DetailsView ve FormView denetimlerinin hepsi, bir CheckBox 'ın Tick 'i üzerinde etkinleştirilebilen yerleşik sayfalama desteği sağlar. GridView Ayrıca sıralama desteğini de içerir.

Ne yazık ki, DataList veya Repeater otomatik sayfalama veya sıralama desteği sunmaz. Bu öğreticide, DataList veya Repeater 'a sayfalama desteğinin nasıl ekleneceğini inceleyeceğiz. Sayfalama arabirimini el ile oluşturmalı, kayıtların uygun sayfasını görüntülemelidir ve geri göndermeler genelinde ziyaret edilen sayfanın geri unutması gerekir. Bu, GridView, DetailsView veya FormView ile daha fazla zaman ve kod alıp, DataList ve Repeater çok daha esnek disk belleği ve veri görüntüleme arabirimine izin verir.

> [!NOTE]
> Bu öğretici, özellikle sayfalama üzerinde odaklanır. Sonraki öğreticide sıralama özellikleri eklemek için dikkat eteceğiz.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>1\. Adım: sayfalama ve sıralama öğreticisi Web sayfalarını ekleme

Bu öğreticiye başlamadan önce, bu öğreticide ve bir sonraki adımda gereken ASP.NET sayfalarını eklemek için ilk olarak bir süre sürme. `PagingSortingDataListRepeater`adlı projede yeni bir klasör oluşturarak başlayın. Ardından, aşağıdaki beş ASP.NET sayfasını bu klasöre ekleyin ve bunların tümünün ana sayfayı kullanacak şekilde yapılandırıldığından `Site.master`:

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`

![Bir Pagingsortingveriistrepeater klasörü oluşturma ve öğretici ASP.NET sayfaları ekleme](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**Şekil 1**: `PagingSortingDataListRepeater` bir klasör oluşturun ve öğretici ASP.NET sayfaları ekleyin

Sonra, `Default.aspx` sayfasını açın ve `SectionLevelTutorialListing.ascx` Kullanıcı denetimini `UserControls` klasöründen tasarım yüzeyine sürükleyin. [Ana sayfalarda ve site gezinti](../introduction/master-pages-and-site-navigation-vb.md) öğreticisinde oluşturduğumuz bu kullanıcı denetimi, site haritasını numaralandırır ve bu öğreticileri madde işaretli bir listenin geçerli bölümünde görüntüler.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)

**Şekil 2**: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image4.png))

Madde işaretli listenin oluşturacağımız sayfalama ve sıralama öğreticilerini görüntülemesi için, bunları site haritasına eklememiz gerekir. `Web.sitemap` dosyasını açın ve düzenledikten sonra DataList site haritası düğüm işaretlemesi ile sildikten sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample1.xml)]

![Site haritasını yeni ASP.NET sayfalarını Içerecek şekilde Güncelleştir](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)

**Şekil 3**: site haritasını yeni ASP.NET sayfalarını içerecek şekilde güncelleştirin

## <a name="a-review-of-paging"></a>Sayfalama Incelemesi

Önceki öğreticilerde GridView, DetailsView ve FormView denetimlerinde verilerin nasıl ekleneceğini gördük. Bu üç denetim, yalnızca denetim s akıllı etiketinde sayfalama etkinleştir seçeneği denetlenerek uygulanabilen, *varsayılan sayfalama* adlı basit bir sayfalama biçimi sunar. Varsayılan sayfalama ile, ilk sayfada bir veri sayfası istendiğinde veya Kullanıcı farklı bir veri sayfasına gittiğinde, GridView, DetailsView veya FormView denetimi ObjectDataSource 'un *Tüm* verilerini yeniden ister. Daha sonra istenen sayfa dizini ve sayfa başına görüntülenecek kayıt sayısı verilen belirli kayıt kümesini görüntüler. [Sayfalama ve rapor verilerini sıralama](../paging-and-sorting/paging-and-sorting-report-data-vb.md) öğreticisinde ayrıntılarda varsayılan sayfalama ele alınmıştır.

Varsayılan sayfalama, her sayfanın tüm kayıtlarını yeniden istemesi olduğundan, yeterince büyük miktarlarda veri ile sayfalama yapılırken pratik değildir. Örneğin, 10 sayfa boyutuyla 50.000 kayıt ile sayfalama düşünün. Kullanıcı yeni bir sayfaya her taşınışında, yalnızca on tane görüntülenmese de, tüm 50.000 kayıtlarının veritabanından alınması gerekir.

*Özel sayfalama* , varsayılan sayfalama 'nin performans sorunlarını yalnızca istenen sayfada görüntülenecek kayıtların kesin alt kümesini yakalayıp çözer. Özel sayfalama uygularken, doğru kayıt kümesini etkin bir şekilde döndürecek SQL sorgusunu yazmanız gerekir. SQL Server 2005 s New [`ROW_NUMBER()` anahtar sözcüğünü](http://www.4guysfromrolla.com/webtech/010406-1.shtml) [, büyük miktarlarda veri öğreticisi aracılığıyla verimli bir şekilde sayfalama](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) bölümünde kullanarak bu tür bir sorgunun nasıl oluşturulacağını gördük.

DataList veya Repeater denetimlerinde varsayılan sayfalama uygulamak için [`PagedDataSource` sınıfını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx) içeriği sayfalanmış `ProductsDataTable` etrafında bir sarmalayıcı olarak kullanabiliriz. `PagedDataSource` sınıfı, herhangi bir sıralanabilir nesne ve [`PageSize`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx) ve her sayfa ve geçerli sayfa dizini için kaç kayıt gösterileceğini belirten [`CurrentPageIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx) özelliklerine atanabilecek bir `DataSource` özelliğine sahiptir. Bu özellikler ayarlandıktan sonra, `PagedDataSource` herhangi bir veri Web denetiminin veri kaynağı olarak kullanılabilir. `PagedDataSource`, numaralandırıldıktan sonra, `PageSize` ve `CurrentPageIndex` özelliklerine göre yalnızca iç `DataSource` kayıtlarının uygun alt kümesini döndürür. Şekil 4 `PagedDataSource` sınıfının işlevlerini gösterir.

![PagedDataSource, sıralanabilir bir nesneyi disk belleğine alınabilen bir arabirimle kaydırır](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image6.png)

**Şekil 4**: `PagedDataSource`, sıralanabilir bir nesneyi disk belleğine alınabilen bir arabirimle sarmalar

`PagedDataSource` nesnesi doğrudan Iş mantığı katmanından oluşturulup yapılandırılabilir ve bir ObjectDataSource aracılığıyla bir DataList veya Repeater 'a bağlanabilir ya da doğrudan ASP.NET Page s arka plan kod sınıfında oluşturulabilir ve yapılandırılabilir. İkinci yaklaşım kullanılırsa, ObjectDataSource 'u kullanarak ve disk belleğine alınmış verileri DataList ya da yineleyici olarak programlı bir şekilde bağlamanız gerekir.

`PagedDataSource` nesnesi, özel sayfalama desteklemek için de özelliklere sahiptir. Ancak, görüntülenecek kesin kayıtları döndüren özel disk belleği için tasarlanan `ProductsBLL` sınıfında BLL yöntemlerine zaten sahip olduğumuz için özel sayfalama için bir `PagedDataSource` kullanmayı atlayabilirsiniz.

Bu öğreticide, uygun şekilde yapılandırılmış bir `PagedDataSource` nesnesini döndüren `ProductsBLL` sınıfına yeni bir yöntem ekleyerek bir DataList 'te varsayılan sayfalama uygulama bölümüne bakacağız. Sonraki öğreticide, özel sayfalama kullanma hakkında bilgi edineceksiniz.

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>2\. Adım: Iş mantığı katmanına varsayılan bir sayfalama yöntemi ekleme

`ProductsBLL` sınıfı şu anda tüm ürün `GetProducts()` bilgilerini döndürmek için bir yönteme sahiptir ve bir başlangıç dizini `GetProductsPaged(startRowIndex, maximumRows)`bir ürünlerin belirli bir alt kümesini döndürmek için bir yöntem içerir. Varsayılan sayfalama ile, GridView, DetailsView ve FormView denetimleri tüm ürünleri almak için `GetProducts()` yöntemini kullanır, ancak yalnızca doğru kayıt alt kümesini göstermek için bir `PagedDataSource` dahili olarak kullanır. Bu işlevselliği DataList ve Repeater denetimleriyle çoğaltmak için BLL 'de bu davranışı taklit eden yeni bir yöntem oluşturabileceğiz.

İki tamsayı giriş parametresi `GetProductsAsPagedDataSource` adlı `ProductsBLL` sınıfına bir yöntem ekleyin:

- görüntülenecek sayfanın dizinini `pageIndex`, sıfır olarak dizinlenir ve
- sayfa başına görüntülenecek kayıt sayısını `pageSize`.

`GetProductsAsPagedDataSource`, *Tüm* kayıtları `GetProducts()`alarak başlatılır. Daha sonra, `CurrentPageIndex` ve `PageSize` özelliklerini, geçirilen `pageIndex` ve `pageSize` parametrelerinin değerlerine ayarlayarak bir `PagedDataSource` nesnesi oluşturur. Yöntemi şu yapılandırılmış `PagedDataSource`döndürerek sonlanır:

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>3\. Adım: varsayılan sayfalama kullanarak bir DataList 'te ürün bilgilerini görüntüleme

`ProductsBLL` sınıfına eklenen `GetProductsAsPagedDataSource` yöntemi ile, artık varsayılan sayfalama sağlayan bir DataList veya Repeater oluşturarız. ' I `PagingSortingDataListRepeater` klasöründeki `Paging.aspx` sayfasını açıp araç kutusundan bir DataList ' i sürükleyin, DataList s `ID` özelliğini `ProductsDefaultPaging`olarak ayarlar. DataList s akıllı etiketinden `ProductsDefaultPagingDataSource` adlı yeni bir ObjectDataSource oluşturun ve `GetProductsAsPagedDataSource` yöntemini kullanarak verileri alması için yapılandırın.

[![bir ObjectDataSource oluşturun ve bunu GetProductsAsPagedDataSource () metodunu kullanacak şekilde yapılandırın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**Şekil 5**: bir ObjectDataSource oluşturun ve `GetProductsAsPagedDataSource` `()` metodunu kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image9.png))

GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ayarlayın.

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerindeki açılan listeleri (hiçbiri) ![ayarla](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**Şekil 6**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinden açılan listeleri (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image12.png))

`GetProductsAsPagedDataSource` yöntemi iki giriş parametresi gerektirdiğinden, sihirbaz bize bu parametre değerlerinin kaynağını ister.

Sayfa dizini ve sayfa boyutu değerleri geri göndermeler genelinde hatırlanmalıdır. Bunlar Görünüm durumunda depolanabilir, QueryString 'de kalıcı hale getirilir, oturum değişkenlerinde depolanabilir veya başka bir teknik kullanılarak hatırlanır. Bu öğreticide, belirli bir veri sayfası için yer işareti çalıştırılmasına izin vermenin avantajlarından yararlanan QueryString kullanacağız.

Özellikle, sırasıyla `pageIndex` ve `pageSize` parametreleri için (bkz. Şekil 7) QueryString alanlarını ve pageSize alanlarını kullanın. Bir Kullanıcı bu sayfayı ilk kez ziyaret ettiğinde QueryString değerleri mevcut olmadığından, bu parametrelerin varsayılan değerlerini ayarlamak için bir dakikanızı ayırın. `pageIndex`için varsayılan değeri 0 (ilk veri sayfasını gösterir) `pageSize` ve varsayılan değer olan 4 ' e ayarlayın.

[![, pageIndex ve pageSize parametrelerinin kaynağı olarak QueryString kullanın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**Şekil 7**: `pageIndex` ve `pageSize` parametreleri için kaynak olarak QueryString kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image15.png))

ObjectDataSource yapılandırıldıktan sonra Visual Studio, DataList için otomatik olarak bir `ItemTemplate` oluşturur. `ItemTemplate` yalnızca ürün adı, kategori ve tedarikçinin gösterilmesi için özelleştirin. Ayrıca, DataList s `RepeatColumns` özelliğini 2 ' ye, `Width` %100 ' e ve `ItemStyle` s `Width` %50 ' e ayarlayın. Bu genişlik ayarları, iki sütun için eşit aralıklar sağlar.

Bu değişiklikleri yaptıktan sonra, DataList ve ObjectDataSource s işaretlemesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

> [!NOTE]
> Bu öğreticide herhangi bir güncelleştirme veya silme işlevi gerçekleştirmediğinden, işlenen sayfa boyutunu azaltmak için DataList s görünüm durumunu devre dışı bırakabilirsiniz.

Bu sayfayı bir tarayıcı üzerinden ilk kez ziyaret edildiğinde `pageIndex` ve `pageSize` QueryString parametreleri sağlanmaz. Bu nedenle, varsayılan değer olan 0 ve 4 kullanılır. Şekil 8 ' de gösterildiği gibi, bu, ilk dört ürünü görüntüleyen bir DataList ile sonuçlanır.

[![Ilk dört ürün listelenir](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image16.png)

**Şekil 8**: Ilk dört ürün listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image18.png))

Bir sayfalama arabirimi olmadan, bir kullanıcının ikinci veri sayfasına gidebilmesi için şu anda basit bir yol yoktur. 4\. adımda bir sayfalama arabirimi oluşturacağız. Şimdilik, sayfalama yalnızca QueryString içindeki disk belleği ölçütlerini belirterek doğrudan kullanılabilir. Örneğin, ikinci sayfayı görüntülemek için, tarayıcı adres çubuğundaki URL 'YI `Paging.aspx` `Paging.aspx?pageIndex=2` olarak değiştirin ve ENTER tuşuna basın. Bu, verilerin ikinci sayfasının görüntülenmesine neden olur (bkz. Şekil 9).

[Verilerin Ikinci sayfası ![görüntülenir](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image19.png)

**Şekil 9**: verilerin Ikinci sayfası görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image21.png))

## <a name="step-4-creating-the-paging-interface"></a>4\. Adım: sayfalama arabirimini oluşturma

Uygulanabilecek birçok farklı disk belleği arabirimi vardır. GridView, DetailsView ve FormView denetimleri aşağıdakiler arasından seçim yapabileceğiniz dört farklı arabirim sağlar:

- **Daha sonra, önceki** kullanıcılar bir kerede bir sayfayı bir sonraki ya da önceki birine taşıyabilir.
- **Ardından, önceki** ve önceki düğmelere ek olarak, bu arabirim, son veya son sayfaya geçmek için Ilk ve son düğmeleri içerir.
- **Sayısal** olarak belirli bir sayfaya hızlı bir şekilde geçebilmesine izin veren disk belleği arabirimindeki sayfa numaralarını sayısal olarak listeler.
- Ilk olarak sayısal sayfa numaralarına ek olarak **sayısal, en** son veya son sayfaya geçme düğmelerini içerir.

DataList ve Repeater için, bir sayfalama arabirimine karar verirken ve uygulamayı uygulamaktan sorumludur. Bu, sayfada gerekli Web denetimlerinin oluşturulmasını ve belirli bir sayfalama arabirimi düğmesine tıklandığında istenen sayfayı görüntülemeyi içerir. Ayrıca, bazı sayfalama arabirimi denetimlerinin devre dışı bırakılması gerekebilir. Örneğin, sonraki, önceki, Ilk, son arabirim kullanılarak verilerin ilk sayfasını görüntülerken, hem Ilk hem de önceki düğmeler devre dışı bırakılır.

Bu öğretici için, s sonraki, önceki, son, son arabirimini kullanalım. Sayfaya dört düğme web denetimi ekleyin ve `ID` s `FirstPage`, `PrevPage`, `NextPage`ve `LastPage`olarak ayarlayın. `Text` özelliklerini önce &lt;&lt;, önceki &lt;, sonraki &gt;ve son &gt;&gt; olarak ayarlayın.

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample4.aspx)]

Sonra, bu düğmelerin her biri için `Click` bir olay işleyicisi oluşturun. Kısa bir süre içinde, istenen sayfayı göstermek için gereken kodu ekleyeceğiz.

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>Disk belleğine alınan toplam kayıt sayısını anımsama

Disk belleği arabiriminden bağımsız olarak, disk belleğine alınan toplam kayıt sayısını hesaplamakta ve hatırlamamız gerekir. Toplam satır sayısı (sayfa boyutuyla birlikte), kaç tane veri sayfasının disk belleğine alınacağını belirler. Bu, hangi disk belleği arabirim denetimlerinin ekleneceğini veya etkinleştirildiğini belirler. Bir sonraki, önceki, Ilk, en son arabirimde, sayfa sayısı iki şekilde kullanılır:

- Son sayfayı görüntülediğimiz ve bu durumda bir sonraki ve son düğmelerin devre dışı bırakıldığı saptanmayı anlamak için.
- Kullanıcı son düğmeye tıkladığında, dizini sayfa sayısından bir daha az olan son sayfaya kadar bir kez saymanız gerekir.

Sayfa sayısı, sayfa boyutuna bölünen toplam satır sayısının tavan değeri olarak hesaplanır. Örneğin, sayfa başına dört kayıtla 79 kayıt ile sayfalama yapıyorsanız sayfa sayısı 20 ' dir (79/4 ' ün tavan değeri). Sayısal disk belleği arabirimini kullandığımızda, bu bilgiler bize kaç sayısal sayfa düğmesi görüntüleneceğini bildirir; sayfalama arabirimimiz Ileri veya son düğmelerini içeriyorsa, sayfa sayısı Ileri veya son düğmelerin ne zaman devre dışı bırakılacağını belirlemekte kullanılır.

Sayfalama arabirimi son bir düğmeyi içeriyorsa, son düğme tıklandığında son sayfa dizinini belirleyebilmemiz için, disk belleğine alınan toplam kayıt sayısının geri göndermeler arasında hatırlanması zorunludur. Bunu kolaylaştırmak için, ASP.NET Page on Code-Behind sınıfında, durumu görüntülemek için değerini devam eden bir `TotalRowCount` özelliği oluşturun:

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

`TotalRowCount`ek olarak, sayfa dizinine, sayfa boyutuna ve sayfa sayısına kolayca erişmek için salt okuma sayfa düzeyi özellikler oluşturmak için bir dakikanızı alın:

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample6.vb)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>Disk belleğine alınan toplam kayıt sayısını belirleme

ObjectDataSource 'un `Select()` yönteminden döndürülen `PagedDataSource` nesnesi, DataList 'te yalnızca bir alt kümesi görüntülense de, *Tüm* ürün kayıtları içinde bulunur. `PagedDataSource` s [`Count` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx) yalnızca DataList 'te görüntülenecek öğe sayısını döndürür; [`DataSourceCount` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx) , `PagedDataSource`içindeki toplam öğe sayısını döndürür. Bu nedenle, ASP.NET Page s `TotalRowCount` özelliğini `PagedDataSource` s `DataSourceCount` özelliğinin değeri olarak atamanız gerekir.

Bunu gerçekleştirmek için, ObjectDataSource s `Selected` olayı için bir olay işleyicisi oluşturun. `Selected` olay işleyicisinde, bu örnekte bulunan ObjectDataSource s `Select()` yönteminin dönüş değerine eriştik `PagedDataSource`.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

## <a name="displaying-the-requested-page-of-data"></a>Istenen veri sayfasını görüntüleme

Kullanıcı, sayfalama arabirimindeki düğmelerden birine tıkladığında, istenen veri sayfasını görüntülemesi gerekir. Sayfalama parametreleri QueryString aracılığıyla belirtildiğinden, kullanıcı tarayıcısının tarayıcı `Paging.aspx` sayfasını uygun sayfalama parametreleriyle yeniden istemesi için `Response.Redirect(url)` istenen veri sayfasını görüntülemek için kullanın. Örneğin, verilerin ikinci sayfasını göstermek için kullanıcıyı `Paging.aspx?pageIndex=1`yönlendiririz.

Bunu kolaylaştırmak için, kullanıcıyı `Paging.aspx?pageIndex=sendUserToPageIndex`yeniden yönlendiren bir `RedirectUser(sendUserToPageIndex)` yöntemi oluşturun. Ardından, bu yöntemi dört düğmeden `Click` olay işleyicilerinden çağırın. `FirstPage` `Click` olay işleyicisinde, ilk sayfaya göndermek için `RedirectUser(0)`çağırın; `PrevPage` `Click` olay işleyicisinde, sayfa dizini olarak `PageIndex - 1` kullanın; vb.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample8.vb)]

`Click` olay işleyicileri tamamlandıktan sonra, DataList s kayıtları, düğmelere tıklanarak kullanılarak disk belleğine alınabilir. Denemek için bir dakikanızı ayırın!

## <a name="disabling-paging-interface-controls"></a>Sayfalama arabirimi denetimlerini devre dışı bırakma

Şu anda, görüntülenen sayfadan bağımsız olarak tüm dört düğme etkindir. Ancak, ilk ve önceki düğmeleri, verilerin ilk sayfasını gösterirken ve son sayfayı gösterirken Ileri ve son düğmeleri devre dışı bırakmak istiyoruz. ObjectDataSource 'un `Select()` yöntemi tarafından döndürülen `PagedDataSource` nesnesi, verilerin ilk veya son sayfasını görüntülüyor olup olmadığınızı anlamak üzere inceleyebileceğiniz Özellikler [`IsFirstPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx) ve [`IsLastPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx) .

Aşağıdaki öğeleri `Selected` olay işleyicisine ekleyin:

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

Bu ek olarak, ilk sayfa görüntülenirken Ilk ve önceki düğmeler devre dışı bırakılır, ancak son sayfa görüntülenirken Ileri ve son düğmeler devre dışı bırakılır.

Kullanıcıya şu anda görüntüledikleri sayfayı ve toplam sayfa sayısını bildirerek sayfalama arabirimini tamamlayalım. Sayfaya bir etiket Web denetimi ekleyin ve `ID` özelliğini `CurrentPageNumber`olarak ayarlayın. ' Nin seçilen olay işleyicisindeki `Text` özelliğini, görüntülenen geçerli sayfayı (`PageIndex + 1`) ve toplam sayfa sayısını (`PageCount`) içermesi için ayarlayın.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample10.vb)]

Şekil 10 ' da ilk kez ziyaret edildiğinde `Paging.aspx` gösterilmektedir. QueryString boş olduğundan, DataList varsayılan olarak ilk dört ürünü gösterir; Ilk ve önceki düğmeler devre dışı bırakılmıştır. Ileri ' ye tıkladığınızda sonraki dört kayıt gösterilir (bkz. Şekil 11); Ilk ve önceki düğmeler artık etkinleştirilmiştir.

[Verilerin Ilk sayfası ![görüntülenir](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image22.png)

**Şekil 10**: Ilk veri sayfası görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image24.png))

[Verilerin Ikinci sayfası ![görüntülenir](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image25.png)

**Şekil 11**: verilerin Ikinci sayfası görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image27.png))

> [!NOTE]
> Sayfalama arabirimi, kullanıcının sayfa başına kaç sayfa görüntüleneceğini belirtmesini sağlayarak daha da geliştirilebilir. Örneğin, bir DropDownList, 5, 10, 25, 50 ve hepsi gibi sayfa boyutu seçeneklerini listelemek için eklenebilir. Bir sayfa boyutu seçildikten sonra, kullanıcının `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`yeniden yönlendirilmesi gerekir. Bu geliştirmeyi, okuyucu için bir alıştırma olarak Uygulamam.

## <a name="using-custom-paging"></a>Özel sayfalama kullanma

DataList, verimsiz varsayılan sayfalama tekniğinin kullanıldığı verileri aracılığıyla sayfalar. Yeterince büyük miktarlarda veri sayfalaması yaparken özel sayfalama kullanılması zorunludur. Uygulama ayrıntıları biraz farklı olsa da, DataList 'te özel sayfalama uygulamanın arkasındaki kavramlar varsayılan sayfalama ile aynıdır. Özel sayfalama ile `ProductBLL` Class s `GetProductsPaged` metodunu kullanın (`GetProductsAsPagedDataSource`yerine). [Büyük miktarlarda veri öğreticisi aracılığıyla verimli sayfalama](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) bölümünde anlatıldığı gibi, `GetProductsPaged` başlangıç satırı dizinini ve döndürülecek en fazla satır sayısını geçirmelidir. Bu parametreler, varsayılan disk sayfalamada kullanılan `pageIndex` ve `pageSize` parametreleri gibi QueryString aracılığıyla korunabilir.

Özel sayfalama ile `PagedDataSource` olmadığından, verilerin ilk veya son sayfasını yeniden görüntülüyor olup olmadığınızı anlamak için alternatif tekniklerin kullanılması gerekir. `ProductsBLL` sınıfındaki `TotalNumberOfProducts()` yöntemi, üzerinden disk belleğine alınan ürünlerin toplam sayısını döndürür. Verilerin ilk sayfasının görüntülendiğini anlamak için, sıfır ise başlangıç satırı dizinini inceleyin, sonra ilk sayfa görüntülenir. Başlangıç satırı dizini ve döndürülecek en fazla satır sayısı, disk belleğine alınan toplam kayıt sayısından büyükse veya buna eşitse son sayfa görüntülenir.

Bir sonraki öğreticide özel disk belleğini daha ayrıntılı bir şekilde uygulamayı inceleyeceğiz.

## <a name="summary"></a>Özet

DataList veya Repeater, GridView, DetailsView ve FormView denetimlerinde bulunan çok sayıda sayfalama desteğini sunurken, bu işlevsellik minimum çabayla eklenebilir. Varsayılan sayfalama uygulamanın en kolay yolu, tüm ürün kümesini bir `PagedDataSource` içinde sarmanız ve sonra `PagedDataSource` DataList veya Repeater 'a bağlamalıdır. Bu öğreticide, `PagedDataSource`döndürmek için `ProductsBLL` sınıfına `GetProductsAsPagedDataSource` yöntemi ekledik. `ProductsBLL` sınıfı, özel disk belleği `GetProductsPaged` ve `TotalNumberOfProducts`için gereken yöntemleri zaten içeriyor.

Özel sayfalama veya varsayılan sayfalama için bir `PagedDataSource` tüm kayıtların görüntüleneceği kesin kayıt kümesini alma ile birlikte, sayfalama arabirimini de el ile eklemeniz gerekir. Bu öğreticide, dört düğme web denetimi ile bir sonraki, önceki, Ilk, son arabirim oluşturduk. Ayrıca, geçerli sayfa numarasını ve toplam sayfa sayısını görüntüleyen bir etiket denetimi eklenmiştir.

Sonraki öğreticide, DataList ve Repeater 'a sıralama desteği ekleme hakkında bilgi edineceksiniz. Ayrıca, hem disk belleğine alınmış hem de sıralanmış bir DataList oluşturma (varsayılan ve özel sayfalama kullanan örneklerle birlikte) hakkında bilgi edineceksiniz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Liz Shulok, Ken peşinatlı PISA ve Bernadette Leigh. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](sorting-data-in-a-datalist-or-repeater-control-cs.md)
> [İleri](sorting-data-in-a-datalist-or-repeater-control-vb.md)
