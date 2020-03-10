---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
title: Rapor verilerini sayfalama ve sıralama (VB) | Microsoft Docs
author: rick-anderson
description: Sayfalama ve sıralama, verileri çevrimiçi bir uygulamada görüntülerken iki çok yaygın özelliklerdir. Bu öğreticide sıralama ekleme ve...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: b895e37e-0e69-45cc-a7e4-17ddd2e1b38d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 6785b5cd2d4d3a2c2e7f2c2fea93f5cd5e2fdf24
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78619583"
---
# <a name="paging-and-sorting-report-data-vb"></a>Rapor Verilerini Sayfalama ve Sıralama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_VB.exe) veya [PDF 'yi indirin](paging-and-sorting-report-data-vb/_static/datatutorial24vb1.pdf)

> Sayfalama ve sıralama, verileri çevrimiçi bir uygulamada görüntülerken iki çok yaygın özelliklerdir. Bu öğreticide, raporlarımıza sıralama ve sayfalama ekleme konusunda ilk bakışta daha sonra gelecek öğreticilerde derlenecektir.

## <a name="introduction"></a>Giriş

Sayfalama ve sıralama, verileri çevrimiçi bir uygulamada görüntülerken iki çok yaygın özelliklerdir. Örneğin, çevrimiçi bir kitaplığı 'nda ASP.NET kitaplar aranırken, bu tür kitaplar bulunabilir, ancak arama sonuçlarını listeleyen rapor her sayfa için yalnızca on eşleşme listeler. Üstelik, sonuçlar başlık, Fiyat, sayfa sayısı, yazar adı vb. ile sıralanabilir. Son 23 öğretici, veri eklemeye, düzenlemesine ve silmeye izin veren arabirimler de dahil olmak üzere çeşitli raporların nasıl oluşturulduğunu incelediği sürece, verileri nasıl sıraladığımızda ve gördüğünüz tek sayfalama örnekleri DetailsView ve FormView ile birlikte verilmiştir kontrollerini.

Bu öğreticide, yalnızca birkaç onay kutusu denetlenerek gerçekleştirilebilen, raporlarımıza sıralama ve sayfalama ekleme hakkında bilgi edineceksiniz. Ne yazık ki bu uyarlaması uygulamasının dezavantajları, sıralama arabiriminin bir bit olmasını sağlar ve sayfalama yordamları, büyük sonuç kümeleri aracılığıyla verimli sayfalama için tasarlanmamıştır. Gelecekteki öğreticiler, kullanıma hazır sayfalama ve sıralama çözümlerinin sınırlamalarını nasıl aşmayı keşfedecektir.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>1\. Adım: sayfalama ve sıralama öğreticisi Web sayfalarını ekleme

Bu öğreticiye başlamadan önce, bu öğretici ve sonraki üç için gereken ASP.NET sayfalarını eklemek için ilk olarak bir süre sürme. `PagingAndSorting`adlı projede yeni bir klasör oluşturarak başlayın. Ardından, aşağıdaki beş ASP.NET sayfasını bu klasöre ekleyin ve bunların tümünün ana sayfayı kullanacak şekilde yapılandırıldığından `Site.master`:

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`

![Bir PagingAndSorting klasörü oluşturma ve öğretici ASP.NET sayfaları ekleme](paging-and-sorting-report-data-vb/_static/image1.png)

**Şekil 1**: bir PagingAndSorting klasörü oluşturma ve öğretici ASP.NET sayfaları ekleme

Sonra, `Default.aspx` sayfasını açın ve `SectionLevelTutorialListing.ascx` Kullanıcı denetimini `UserControls` klasöründen tasarım yüzeyine sürükleyin. [Ana sayfalarda ve site gezinti](../introduction/master-pages-and-site-navigation-vb.md) öğreticisinde oluşturduğumuz bu kullanıcı denetimi, site haritasını numaralandırır ve bu öğreticileri madde işaretli bir listenin geçerli bölümünde görüntüler.

![SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine ekleyin](paging-and-sorting-report-data-vb/_static/image2.png)

**Şekil 2**: SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx 'e ekleme

Madde işaretli listenin oluşturacağımız sayfalama ve sıralama öğreticilerini görüntülemesi için, bunları site haritasına eklememiz gerekir. `Web.sitemap` dosyasını açın ve site haritası düğüm işaretlemesini düzenledikten, ekledikten ve sildikten sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](paging-and-sorting-report-data-vb/samples/sample1.xml)]

![Site haritasını yeni ASP.NET sayfalarını Içerecek şekilde Güncelleştir](paging-and-sorting-report-data-vb/_static/image3.png)

**Şekil 3**: site haritasını yeni ASP.NET sayfalarını içerecek şekilde güncelleştirin

## <a name="step-2-displaying-product-information-in-a-gridview"></a>2\. Adım: GridView 'da ürün bilgilerini görüntüleme

Sayfalama ve sıralama yeteneklerini gerçekten uygulamadan önce, ilk olarak ürün bilgilerini listeleyen standart, sıralanabilir olmayan, sayfalandırılmamış bir GridView oluşturmaya izin verin. Bu, bu öğreticide daha önce birkaç kez yaptığımız bir görevdir ve bu adımların tanıdık getirilmesi gerekir. `SimplePagingSorting.aspx` sayfasını açıp araç kutusundan bir GridView denetimini tasarımcı üzerine sürükleyerek, `ID` özelliğini `Products`olarak ayarlayarak başlayın. Ardından, tüm ürün bilgilerini döndürmek için ProductsBLL sınıf s `GetProducts()` yöntemini kullanan yeni bir ObjectDataSource oluşturun.

![GetProducts () yöntemini kullanarak tüm ürünlerle Ilgili bilgileri alma](paging-and-sorting-report-data-vb/_static/image4.png)

**Şekil 4**: GetProducts () yöntemini kullanarak tüm ürünlerle ilgili bilgileri alma

Bu rapor salt okunurdur bir rapor olduğundan, ObjectDataSource `Insert()`, `Update()`veya `Delete()` yöntemlerini ilgili `ProductsBLL` yöntemlerine eşlemek gerekmez; Bu nedenle, GÜNCELLEŞTIRME, ekleme ve SILME sekmeleri için açılan listeden (hiçbiri) seçeneğini belirleyin.

![GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden açılan listede (hiçbiri) seçeneğini belirleyin](paging-and-sorting-report-data-vb/_static/image5.png)

**Şekil 5**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinde açılan listede bulunan (hiçbiri) seçeneğini belirleyin

Daha sonra, GridView s alanlarını yalnızca ürün adları, tedarikçiler, Kategoriler, fiyatlar ve kullanımdan kaldırıldı durumlarının gösterilmesi için özelleştirelim. Ayrıca, `HeaderText` özelliklerini ayarlama veya fiyatı para birimi olarak biçimlendirme gibi herhangi bir alan düzeyinde biçimlendirme değişikliğini de ücretsiz hale getirebilirsiniz. Bu değişikliklerden sonra, GridView s bildirim temelli işaretlerinizin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample2.aspx)]

Şekil 6 ' da bir tarayıcıdan görüntülendiklerinde ilerleme durumunu gösterir. Sayfanın tüm ürünlerini tek bir ekranda listelediğinden, her ürün adına, kategoriye, tedarikçiye, fiyata ve Discontinued durumuna sahip olduğunu unutmayın.

[Ürünlerin her biri ![listeleniyor](paging-and-sorting-report-data-vb/_static/image7.png)](paging-and-sorting-report-data-vb/_static/image6.png)

**Şekil 6**: ürünlerin her biri listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-and-sorting-report-data-vb/_static/image8.png))

## <a name="step-3-adding-paging-support"></a>3\. Adım: sayfalama desteği ekleme

*Tüm* ürünlerin bir ekranda listelenmesi, verileri kullanan kullanıcı için bilgi yüküne yol açabilir. Sonuçları daha yönetilebilir hale getirmek için verileri daha küçük sayfalara bölebilir ve kullanıcının verileri tek seferde bir sayfada görüntülemesine izin verebilirsiniz. Bunu gerçekleştirmek için GridView s akıllı etiketinden sayfalama etkinleştir onay kutusunu işaretleyin (Bu, GridView s [`AllowPaging` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx) `true`olarak ayarlar).

[![disk belleği desteği eklemek için sayfalama etkinleştir onay kutusunu Işaretleyin](paging-and-sorting-report-data-vb/_static/image10.png)](paging-and-sorting-report-data-vb/_static/image9.png)

**Şekil 7**: sayfalama desteği eklemek Için sayfalama etkinleştir onay kutusunu işaretleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-and-sorting-report-data-vb/_static/image11.png))

Sayfalama özelliğinin etkinleştirilmesi, sayfa başına gösterilen kayıt sayısını sınırlar ve GridView 'a bir *sayfalama arabirimi* ekler. Şekil 7 ' de gösterilen varsayılan sayfalama arabirimi, bir dizi sayfa numarası olduğundan kullanıcının bir veri sayfasından diğerine hızlıca gezinmesine olanak tanır. Bu sayfalama arabirimi, son öğreticilerde DetailsView ve FormView denetimlerine disk belleği desteği eklerken tanıdık göründüğimize göre tanıdık gelmelidir.

Hem DetailsView hem de FormView denetimleri sayfa başına yalnızca tek bir kayıt gösterir. Ancak GridView, sayfa başına kaç kayıt gösterileceğini öğrenmek için [`PageSize` özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx) bakar (Bu özellik varsayılan olarak 10 değerini alır).

Bu GridView, DetailsView ve FormView s sayfalama arabirimi aşağıdaki özellikler kullanılarak özelleştirilebilir:

- `PagerStyle`, sayfalama arabirimine yönelik stil bilgisini gösterir; `BackColor`, `ForeColor`, `CssClass`, `HorizontalAlign`gibi ayarları belirtebilir.
- `PagerSettings`, sayfalama arabiriminin işlevselliğini özelleştirebileceği bir dizi özellik içerir; `PageButtonCount`, disk belleği arabirimindeki en fazla sayısal sayfa numarası sayısını belirtir (varsayılan değer 10 ' dur); [`Mode` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx) , sayfalama arabiriminin nasıl çalıştığını ve şu şekilde ayarlanamayacağını gösterir: 

    - `NextPrevious` bir sonraki ve önceki düğmeleri gösterir, bu da kullanıcının bir seferde bir sayfa Ileri veya geri geçmesine izin verir
    - `NextPreviousFirstLast` sonraki ve önceki düğmelere ek olarak, Ilk ve son düğmeler de dahil edilir ve bu da kullanıcının verilerin ilk veya son sayfasına hızlı bir şekilde taşınmasını sağlar
    - `Numeric`, bir dizi sayfa numarası gösterir ve kullanıcının her sayfaya hemen geçebilmesine izin verir
    - sayfa numaralarına ek olarak `NumericFirstLast`, Ilk ve son düğmelerini içerir ve kullanıcının verilerin ilk veya son sayfasına hızla geçmesine izin verir; Ilk/son düğmeler yalnızca tüm sayısal sayfa numaraları uygun değilse gösterilir

Üstelik, GridView, DetailsView ve FormView hepsi, görüntülenen geçerli sayfayı ve verilerin toplam sayfa sayısını gösteren `PageIndex` ve `PageCount` özelliklerini sunar. `PageIndex` özelliği 0 ' dan başlayarak dizine alınır. Bu, veri `PageIndex` ilk sayfasını görüntülemenin 0 ' a eşit olacağını belirtir. Diğer taraftan `PageCount`, 1 ' de sayma başlar, yani `PageIndex` 0 ile `PageCount - 1`arasındaki değerlerle sınırlıdır.

GridView s sayfalama arabirimimizin varsayılan görünümünü geliştirmek için bir dakikanızı ayırın. Özellikle, sayfalama arabirimine açık gri bir arka planla doğrudan hizalı izin verin. Bu özellikleri doğrudan GridView s `PagerStyle` özelliği aracılığıyla ayarlamak yerine, s `Styles.css` `PagerRowStyle` adlı bir CSS sınıfı oluşturalım ve sonra temamız aracılığıyla `PagerStyle` s `CssClass` özelliğini atamamız gerekir. `Styles.css` açarak ve aşağıdaki CSS sınıfı tanımını ekleyerek başlayın:

[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample3.css)]

Sonra, `GridView.skin` dosyasını `App_Themes` klasörü içindeki `DataWebControls` klasöründe açın. *Ana sayfalarda ve site gezinti* öğreticisinde anlatıldığı gibi, dış görünüm dosyaları bir Web denetimi için varsayılan özellik değerlerini belirtmek üzere kullanılabilir. Bu nedenle, `PagerStyle` s `CssClass` özelliğinin `PagerRowStyle`için ayarlanmasını dahil etmek için mevcut ayarları yapın. Ayrıca, sayfalama arabirimini `NumericFirstLast` disk belleği arabirimini kullanarak en fazla beş sayısal sayfa düğmesini gösterecek şekilde yapılandıralım.

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>Sayfalama Kullanıcı deneyimi

Şekil 8 ' den sonra bir tarayıcı aracılığıyla ziyaret edildiğinde, GridView s sayfalama onay kutusu işaretlendikten sonra, `PagerStyle` ve `PagerSettings` yapılandırmalarının `GridView.skin` dosyası aracılığıyla, Web sayfası görüntülenir. Yalnızca on kaydın gösterildiğini ve sayfalama arabiriminin, verilerin ilk sayfasını görüntülediğimiz olduğunu unutmayın.

[Sayfalama etkinken ![, bir seferde yalnızca kayıtların bir alt kümesi görüntülenir](paging-and-sorting-report-data-vb/_static/image13.png)](paging-and-sorting-report-data-vb/_static/image12.png)

**Şekil 8**: sayfalama etkinken, tek seferde yalnızca bir kayıt alt kümesi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-and-sorting-report-data-vb/_static/image14.png))

Kullanıcı, disk belleği arabirimindeki sayfa numaralarının birine tıkladığında, bir geri gönderme ve sayfa kayıtlarının istenen sayfa kayıtlarını göstermesini yeniden yükler. Şekil 9 ' da, son veri sayfasını görüntülemeyi tamamladıktan sonra sonuçlar gösterilir. Son sayfanın yalnızca bir kayıt içerdiğine dikkat edin; Bunun nedeni, toplamda 81 kayıt olduğundan, sayfa başına sekiz sayfa ve tek kaydına sahip bir sayfa ile sonuçlanır.

[Sayfa numarasına tıklanması ![geri göndermeye neden olur ve uygun kayıt alt kümesini gösterir](paging-and-sorting-report-data-vb/_static/image16.png)](paging-and-sorting-report-data-vb/_static/image15.png)

**Şekil 9**: sayfa numarasını tıklatmak geri göndermeye neden olur ve uygun kayıt alt kümesini gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-and-sorting-report-data-vb/_static/image17.png))

## <a name="paging-s-server-side-workflow"></a>Sayfalama s sunucu tarafı Iş akışı

Son Kullanıcı, sayfalama arabirimindeki bir düğmeye tıkladığında, bir geri gönderme işlemi ve aşağıdaki sunucu tarafı iş akışı başlar:

1. GridView s (veya DetailsView ya da FormView) `PageIndexChanging` olayı ateşlenir
2. ObjectDataSource, BLL 'den *Tüm* verileri yeniden ister. GridView s `PageIndex` ve `PageSize` özellik değerleri, BLL 'den döndürülen kayıtların GridView 'da gösterilmesini belirlemek için kullanılır
3. GridView s `PageIndexChanged` olayı ateşlenir

2\. adımda, ObjectDataSource veri kaynağındaki tüm verileri yeniden ister. Bu sayfalama stili, genellikle varsayılan olarak, `AllowPaging` özelliği `true`olarak ayarlanırken disk belleği davranışının kullanıldığı şekilde *varsayılan sayfalama*olarak adlandırılır. Varsayılan sayfalama ile, veri Web denetimi her bir veri sayfası için tüm kayıtları alır, ancak bir kayıt alt kümesi gerçekten tarayıcıya gönderilen HTML 'ye işlense bile. Veritabanı verileri BLL veya ObjectDataSource tarafından önbelleğe alınmamışsa, varsayılan disk belleği yeterince büyük sonuç kümelerinde veya çok sayıda eşzamanlı kullanıcı içeren Web uygulamalarında kullanılamaz.

Sonraki öğreticide, *Özel sayfalama*uygulamayı nasıl uygulayacağınızı inceleyeceğiz. Özel sayfalama sayesinde, ObjectDataSource 'a, istenen veri sayfası için gereken tam kayıt kümesini almak için özellikle de talimat verebilirsiniz. Imagine de, özel sayfalama, büyük sonuç kümeleri aracılığıyla sayfalama verimliliğini büyük ölçüde geliştirir.

> [!NOTE]
> Varsayılan sayfalama, yeterince büyük sonuç kümeleriyle veya çok sayıda kullanıcıya sahip sitelerde sayfalama yaparken uygun olmasa da, özel sayfalama 'nin uygulanması için daha fazla değişiklik ve çaba gerektirdiğini ve bir onay kutusu denetimi kadar basit olmadığını (varsayılan olarak) unutmayın. sayfalama). Bu nedenle, varsayılan sayfalama, küçük ve düşük trafikli web siteleri için ideal seçim veya daha kolay ve daha hızlı bir şekilde uygulanması için görece küçük sonuç kümelerinde sayfalama olabilir.

Örneğin, veritabanımızda 100 ' den fazla ürün sunamayacağımız için, özel sayfalama açısından en düşük performans kazancı, büyük olasılıkla bunu uygulamak için gereken çabaya göre denkleştirilir. Ancak, bir gün binlerce ürüne sahip *olabilir ve özel sayfalama uygulamamız* , uygulamamızın ölçeklenebilirliğini büyük ölçüde yumuşatır.

## <a name="step-4-customizing-the-paging-experience"></a>4\. Adım: sayfalama deneyimini özelleştirme

Veri Web denetimleri, Kullanıcı sayfalama deneyimini geliştirmek için kullanılabilecek birçok özellik sağlar. Örneğin, `PageCount` özelliği, kaç tane toplam sayfa olduğunu gösterir, `PageIndex` özelliği ziyaret edilen geçerli sayfayı gösterir ve kullanıcıyı belirli bir sayfaya hızlı bir şekilde taşımak için ayarlanabilir. Bu özelliklerin Kullanıcı sayfalama deneyimini geliştirmek üzere nasıl kullanılacağını göstermek için, kullanıcıya şu anda ziyaret ettikleri sayfayı ve belirli bir sayfaya hızlıca atlayabilecekleri bir DropDownList denetimiyle birlikte bir etiket Web denetimi ekleyelim .

İlk olarak, sayfanıza bir etiket Web denetimi ekleyin, `ID` özelliğini `PagingInformation`olarak ayarlayın ve `Text` özelliğini temizleyin. Ardından, GridView s `DataBound` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample5.vb)]

Bu olay işleyicisi, `PagingInformation` etiket s `Text` özelliğini, kullanıcıya şu anda kaç adet toplam sayfa `Products.PageCount` `Products.PageIndex + 1` olduğunu bildiren bir iletiye bir ileti ekler (`Products.PageIndex`, 0 ' dan başlayarak dizini oluşturulmuş olduğundan `PageIndex` özelliğine 1 ekledik). `DataBound` olayı, her veri GridView 'a her bağlandığında `PageIndexChanged` olay işleyicisi yalnızca sayfa dizini değiştirildiğinde harekete geçirilir çünkü `PageIndexChanged` olay işleyicisine izin vermek için, `DataBound` olay işleyicisinde bu etiketi ata `Text` özelliğini seçtim. GridView ilk sayfada ilk kez veri bağlandığında, `PageIndexChanging` olayı tetiklemez (`DataBound` olay olur).

Bu ek olarak, Kullanıcı artık ziyaret ettikleri sayfayı ve toplam veri sayfası sayısını belirten bir ileti gösteriliyor.

[Geçerli sayfa numarasını ![ve toplam sayfa sayısı görüntülenir](paging-and-sorting-report-data-vb/_static/image19.png)](paging-and-sorting-report-data-vb/_static/image18.png)

**Şekil 10**: geçerli sayfa numarası ve toplam sayfa sayısı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-and-sorting-report-data-vb/_static/image20.png))

Etiket denetimine ek olarak, Ayrıca, GridView 'daki sayfa numaralarını listeleyen bir DropDownList denetimi de şu anda seçili olan sayfayla birlikte eklenir. Buradaki fikir, kullanıcının geçerli sayfadan diğerine hızlı bir şekilde geçebileceği, yalnızca DropDownList 'den yeni sayfa dizinini seçmenizde yarar vardır. Tasarımcı 'ya bir DropDownList ekleyerek başlayın, `ID` özelliğini `PageList` olarak ayarlayarak ve AutoPostBack öğesini akıllı etiketinden etkinleştir seçeneğini kontrol edin.

Sonra, `DataBound` olay işleyicisine dönün ve aşağıdaki kodu ekleyin:

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample6.vb)]

Bu kod, `PageList` DropDownList içindeki öğeleri temizleyerek başlar. Bu durum, değişiklik yapılacak sayfaların sayısını beklemediğinden gereksiz görünebilir, ancak diğer kullanıcılar sistemi aynı anda kullanıyor, bu da `Products` tablosundan kayıt ekliyor veya kaldırmış olabilir. Bu tür eklemeler veya silmeler, veri sayfalarının sayısını değiştirebilir.

Daha sonra, sayfa numaralarını yeniden oluşturuyoruz ve geçerli GridView ile eşleyen bir tane `PageIndex` varsayılan olarak seçili olmalıdır. Bunu, 0 ' dan `PageCount - 1`bir döngüyle gerçekleştirdik, her yinelemede yeni bir `ListItem` ekliyor ve geçerli yineleme dizini GridView s `PageIndex` özelliğine eşitse `Selected` özelliğini true olarak ayarlıyoruz.

Son olarak, kullanıcının listeden farklı bir öğe seçilişinde harekete geçen DropDownList s `SelectedIndexChanged` olayı için bir olay işleyicisi oluşturuyoruz. Bu olay işleyicisini oluşturmak için, tasarımcıda DropDownList 'e çift tıklayın, ardından aşağıdaki kodu ekleyin:

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample7.vb)]

Şekil 11 ' de gösterildiği gibi, yalnızca GridView s `PageIndex` özelliğini değiştirmek verilerin GridView 'a yeniden bağlanmasına neden olur. GridView s `DataBound` olay işleyicisinde, uygun DropDownList `ListItem` seçilidir.

[![sayfa 6 aşağı açılan liste öğesini seçerken Kullanıcı otomatik olarak altıncı sayfaya alınır](paging-and-sorting-report-data-vb/_static/image22.png)](paging-and-sorting-report-data-vb/_static/image21.png)

**Şekil 11**: sayfa 6 aşağı açılan liste öğesini seçerken Kullanıcı otomatik olarak altıncı sayfaya alınır ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-and-sorting-report-data-vb/_static/image23.png))

## <a name="step-5-adding-bi-directional-sorting-support"></a>5\. Adım: Iki yönlü sıralama desteği ekleme

Çift yönlü sıralama desteği eklemek, sayfalama desteği eklemek kadar basittir; GridView s akıllı etiketinden sıralamayı etkinleştir seçeneğini kontrol edin (GridView s [`AllowSorting` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx) `true`olarak ayarlar). Bu, GridView s alanlarının her bir üst listesini, tıklandığı zaman geri göndermeye neden olan ve tıklanan sütuna göre artan sırada sıralanan verileri döndüren LinkButtons olarak işler. Aynı üst bilgi LinkButton düğmesine tıkladığınızda verileri azalan sırada yeniden sıralayın.

> [!NOTE]
> Türü belirtilmiş veri kümesi yerine özel bir veri erişim katmanı kullanıyorsanız, GridView s akıllı etiketinde sıralama etkinleştirme seçeneğine sahip olmayabilirsiniz. Yalnızca sıralamayı yerel olarak destekleyen veri kaynaklarına bağlanan GridViews bu onay kutusunu kullanabilir. Yazılan veri kümesi, ADO.NET DataTable çağrıldığında, belirtilen ölçütlere göre DataTable s DataRow ' ı sıralayan bir `Sort` yöntemi sağladığından, yerleşik sıralama desteği sağlar.

DAL, sıralamayı yerel olarak destekleyen nesneler döndürmezse, verileri sıralayabilir veya verileri DAL tarafından sıralanmış olarak sıralamak için, ObjectDataSource 'u Iş mantığı katmanına geçirecek şekilde yapılandırmanız gerekir. Gelecekteki bir öğreticide Iş mantığı ve veri erişim katmanlarında verileri sıralamayı inceleyeceğiz.

Sıralama LinkButtons, geçerli renkler (ziyaret edilmemiş bir bağlantı için mavi ve ziyaret edilen bir bağlantı için koyu kırmızı) üst bilgi satırının arka plan rengiyle çakışan HTML köprüleri olarak işlenir. Bunun yerine, bir veya daha fazla ziyaret edilip edilmediğine bakılmaksızın, her başlık satırı bağlantısının beyaz olarak görüntülenmesine izin verin. Bu, `Styles.css` sınıfına aşağıdakiler eklenerek gerçekleştirilebilir:

[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample8.css)]

Bu söz dizimi, HeaderStyle sınıfını kullanan bir öğe içinde bu köprüleri görüntülerken beyaz metni kullanacağınızı gösterir.

Bu CSS eklendikten sonra, sayfayı bir tarayıcı aracılığıyla ziyaret ettiğinizde, ekranınızda Şekil 12 ' ye benzer görünmelidir. Özellikle, Şekil 12 ' de, Fiyat alanı s üst bilgi bağlantısına tıklandıktan sonra sonuçlar gösterilmektedir.

[![sonuçlar, BirimFiyat tarafından artan düzende sıralandı](paging-and-sorting-report-data-vb/_static/image25.png)](paging-and-sorting-report-data-vb/_static/image24.png)

**Şekil 12**: sonuçlar BirimFiyat tarafından artan düzende sıralanmışsa ([tam boyutlu görüntüyü görüntülemek için tıklayın](paging-and-sorting-report-data-vb/_static/image26.png))

## <a name="examining-the-sorting-workflow"></a>Sıralama Iş akışını İnceleme

Tüm GridView alanları BoundField, CheckBoxField, TemplateField ve benzeri bir `SortExpression` özelliğine sahiptir ve bu alan sıralama üst bilgi bağlantısına tıklandığında verileri sıralamak için kullanılması gereken ifadeyi gösterir. GridView 'da Ayrıca bir `SortExpression` özelliği de vardır. Sıralama üst bilgisi LinkButton tıklandığında, GridView bu alanın `SortExpression` değerini `SortExpression` özelliğine atar. Ardından, veriler ObjectDataSource 'tan yeniden alınır ve GridView s `SortExpression` özelliğine göre sıralanır. Aşağıdaki listede, bir son kullanıcı GridView 'daki verileri sıralarken transpires olan adımların sırası ayrıntıları verilmiştir:

1. GridView s [sıralama olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx) ateşlenir
2. GridView s [`SortExpression` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) , sıralama üst bilgisi LinkButton öğesine tıklandığı alanın `SortExpression` ayarlanır
3. ObjectDataSource, BLL 'deki tüm verileri yeniden alır ve ardından GridView s 'yi kullanarak verileri sıralar `SortExpression`
4. GridView s `PageIndex` özelliği 0 olarak sıfırlanır. Bu, kullanıcının sıralama verilerinin ilk sayfasına döndürüldüğü anlamına gelir (disk belleği desteğinin uygulandığı varsayılarak)
5. GridView s [`Sorted` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx) ateşlenir

Varsayılan sıralamada olduğu gibi, varsayılan sıralama seçeneği BLL 'deki *Tüm* kayıtları yeniden alır. Sayfalama olmadan sıralamayı kullanırken veya varsayılan sayfalama ile sıralamayı kullanırken, bu performans isabetini (veritabanı verilerini önbelleğe alma işleminin kısaltması) aşmak için bir yol yoktur. Ancak gelecek öğreticide göreceğiniz gibi, özel sayfalama kullanılırken verileri etkili bir şekilde sıralamak mümkün olacaktır.

GridView 'un akıllı etiketindeki açılan listede bir ObjectDataSource 'u GridView 'a bağlarken, her GridView alanının otomatik olarak `ProductsRow` sınıfındaki veri alanı adına atanan `SortExpression` özelliği vardır. Örneğin, `ProductName` BoundField `SortExpression`, aşağıdaki bildirime dayalı biçimlendirmede gösterildiği gibi `ProductName`olarak ayarlanır:

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample9.aspx)]

Bir alan, `SortExpression` özelliğini temizleyerek (boş bir dizeye atayarak) sıralanabilir olması için yapılandırılabilir. Bunu göstermek için, müşterilerimize ürünlerimizi fiyata göre sıraladığımızdan düşünün. `UnitPrice` BoundField `SortExpression` özelliği, bildirime dayalı biçimlendirmeden veya alanlar iletişim kutusunda kaldırılabilir (GridView s akıllı etiketinde sütunları düzenle bağlantısına tıklanarak erişilebilir).

![Sonuçlar, BirimFiyat tarafından artan düzende sıralandı](paging-and-sorting-report-data-vb/_static/image27.png)

**Şekil 13**: sonuçlar BirimFiyat tarafından artan düzende sıralanmışsa

`UnitPrice` BoundField için `SortExpression` özelliği kaldırıldıktan sonra, üst bilgi bir bağlantı yerine metin olarak işlenir ve böylece kullanıcılar verileri fiyata göre sıralanmasını önler.

[![SortExpression özelliğini kaldırarak kullanıcılar artık ürünleri fiyata göre sıralayamazsınız](paging-and-sorting-report-data-vb/_static/image29.png)](paging-and-sorting-report-data-vb/_static/image28.png)

**Şekil 14**: SortExpression özelliğini kaldırarak kullanıcılar artık ürünleri fiyata göre sıralayamazsınız ([tam boyutlu görüntüyü görüntülemek için tıklatın](paging-and-sorting-report-data-vb/_static/image30.png))

## <a name="programmatically-sorting-the-gridview"></a>GridView 'ı programlama yoluyla sıralama

GridView 'un içeriğini programlama yoluyla programlama yoluyla da sıralayabilirsiniz [`Sort`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx). [`SortDirection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` ya da `Descending`) ile birlikte sıralamak için `SortExpression` değerini geçirin ve GridView s verileri yeniden sıralanır.

`UnitPrice` göre sıralamayı kapatdığımız nedenin, müşterilerimizin yalnızca en düşük fiyatlı ürünleri satın aldığımızdan endişelentiğimiz için olduğunu düşünün. Bununla birlikte, bunları en pahalı ürünlerin satın almasını teşvik etmek istiyoruz. bu nedenle, ürünleri fiyata göre sıralayıp yalnızca en pahalı fiyattan en düşük düzeyde.

Bunu gerçekleştirmek için, sayfaya bir düğme web denetimi ekleyin, `ID` özelliğini `SortPriceDescending`ve `Text` özelliğini fiyata göre sırala olarak ayarlayın. Sonra, tasarımcıda düğme denetimini çift tıklayarak düğme s `Click` olayı için bir olay işleyicisi oluşturun. Aşağıdaki kodu bu olay işleyicisine ekleyin:

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample10.vb)]

Bu düğmeye tıkladığınızda, Kullanıcı fiyata göre sıralanan ürünlerin en pahalı ve en ucuz (bkz. Şekil 15) ile ilk sayfaya döndürülür.

[Düğmeye tıklamak ![, ürünleri en pahalı olan en düşük düzeyde sıralar](paging-and-sorting-report-data-vb/_static/image32.png)](paging-and-sorting-report-data-vb/_static/image31.png)

**Şekil 15**: düğmeye tıkladığınızda en pahalı olan ürünleri en az ([tam boyutlu görüntüyü görüntülemek için tıklatın](paging-and-sorting-report-data-vb/_static/image33.png))

## <a name="summary"></a>Özet

Bu öğreticide, her ikisi de bir CheckBox denetimi kadar kolay olan varsayılan sayfalama ve sıralama yeteneklerini nasıl uygulayacağınızı gördünüz! Bir kullanıcı verileri veri üzerinden sıralarken, benzer bir iş akışı kaldırımları:

1. Geri gönderme ensues
2. Veri Web denetimi için ön düzey olay ateşlenir (`PageIndexChanging` veya `Sorting`)
3. Tüm veriler ObjectDataSource tarafından yeniden alınır
4. Veri Web denetimi-düzey sonrası olay ateşlenir (`PageIndexChanged` veya `Sorted`)

Temel sayfalama ve sıralamayı uygularken, daha verimli özel sayfalama kullanmak veya sayfalama veya sıralama arabirimini daha da geliştirmek için daha fazla çaba kullanılması gerekir. Gelecekteki öğreticiler, bu konuları keşfedebilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](creating-a-customized-sorting-user-interface-cs.md)
> [İleri](efficiently-paging-through-large-amounts-of-data-vb.md)
