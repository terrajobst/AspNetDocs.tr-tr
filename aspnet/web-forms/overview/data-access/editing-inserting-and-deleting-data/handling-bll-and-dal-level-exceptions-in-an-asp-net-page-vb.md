---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
title: Bir ASP.NET sayfasında BLL ve DAL düzeyi özel durumları işleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide kolay bir şekilde nasıl görüntüleneceğini, bilgilendirici bir hata iletisinin bir ekleme, güncelleştirme veya silme işlemi sırasında bir özel durum oluşması gerektiğini görüyoruz...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 129d4338-1315-4f40-89b5-2b84b807707d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
msc.type: authoredcontent
ms.openlocfilehash: ee277596ade18d2603892d134b47c2c8697836bb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620894"
---
# <a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-vb"></a>Bir ASP.NET Sayfasında BLL ve DAL Düzeyi Özel Durumları İşleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_VB.exe) veya [PDF 'yi indirin](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/datatutorial18vb1.pdf)

> Bu öğreticide, bir ASP.NET Data Web denetiminin INSERT, Update veya delete işlemi sırasında bir özel durum ortaya çıkan hata iletisinin nasıl görüntüleneceğini göreceğiz.

## <a name="introduction"></a>Giriş

Katmanlı uygulama mimarisi kullanarak bir ASP.NET Web uygulamasındaki verilerle çalışma, aşağıdaki üç genel adımı içerir:

1. Iş mantığı katmanının hangi yönteminin çağrılması gerektiğini ve hangi parametre değerlerini geçitirsiniz öğrenin. Parametre değerleri sabit olarak kodlanmış, programlı olarak atanan veya Kullanıcı tarafından girilen girişler olabilir.
2. Yöntemi çağırın.
3. Sonuçları işleyin. Veri döndüren bir BLL yöntemi çağrılırken bu, verileri bir veri Web denetimine bağlamayı gerektirebilir. Verileri değiştiren BLL yöntemleri için bu, bir dönüş değerine göre bazı işlemleri gerçekleştirmeyi veya 2. adımda bulunan özel durumları sorunsuz bir şekilde işlemeyi içerebilir.

[Önceki öğreticide](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)gördüğümüz gibi, hem ObjectDataSource hem de Data Web denetimleri, 1 ve 3. adımlar için genişletilebilirlik noktaları sağlar. Örneğin, GridView, kendi `RowUpdating` olayını kendi alan değerlerini ObjectDataSource 'un `UpdateParameters` koleksiyonuna atamadan önce tetikleyen. `RowUpdated` olayı, ObjectDataSource işlemi tamamladıktan sonra tetiklenir.

1\. adım sırasında başlatılan olayları zaten inceledik ve giriş parametrelerini özelleştirmek veya işlemi iptal etmek için nasıl kullanılabilecekleri görüldü. Bu öğreticide, işlem tamamlandıktan sonra yangın olaylarımıza dikkat ederiz. Bu son düzey olay işleyicileriyle, diğer şeyler arasında, işlem sırasında bir özel durumun oluşup olmadığını belirleyebilir ve düzgün şekilde işleyebilir, ekranda standart ASP.NET yerine kolay ve bilgilendirici bir hata iletisi görüntüleyebilirsiniz özel durum sayfası.

Bu düzey son olaylarla çalışmayı göstermek için, düzenlenebilir bir GridView 'da ürünleri listeleyen bir sayfa oluşturalım. Bir ürünü güncelleştirirken, bir özel durum ASP.NET sayfamızda bir sorun oluştuğunu açıklayan GridView 'un üzerinde kısa bir ileti görüntüler. Haydi başlayın!

## <a name="step-1-creating-an-editable-gridview-of-products"></a>1\. Adım: ürünlerin düzenlenebilir bir GridView oluşturma

Önceki öğreticide, `ProductName` ve `UnitPrice`yalnızca iki alan ile düzenlenebilir bir GridView oluşturduk. Bu, her ürün alanı için bir parametre yerine yalnızca üç giriş parametresini kabul eden (ürünün adı, birim fiyatı ve KIMLIĞI) `ProductsBLL` sınıfın `UpdateProduct` yöntemi için ek bir aşırı yük oluşturulmasını gerektirir. Bu öğreticide, bu tekniği bir daha alıştıralım, ürün adını, birim başına miktarı, birim fiyatını ve stoktaki birimleri görüntüleyen düzenlenebilir bir GridView oluşturmaya, ancak stoktaki ad, birim fiyatı ve birimlerin düzenlenmesine izin verir.

Bu senaryoya uyum sağlamak için, dört parametre kabul eden bir `UpdateProduct` yönteminin başka bir aşırı yüklemesine ihtiyacımız vardır: ürünün adı, birim fiyatı, stoktaki birimler ve KIMLIK. `ProductsBLL` sınıfına aşağıdaki yöntemi ekleyin:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample1.vb)]

Bu yöntem tamamlandıktan sonra, bu dört özel ürün alanını düzenlemenizi sağlayan ASP.NET sayfasını oluşturmaya hazırız. `EditInsertDelete` klasöründeki `ErrorHandling.aspx` sayfasını açın ve tasarımcı aracılığıyla sayfaya bir GridView ekleyin. GridView 'u yeni bir ObjectDataSource 'a bağlayın, `Select()` yöntemini `ProductsBLL` sınıfının `GetProducts()` yöntemiyle ve `Update()` yöntemini yeni oluşturulan `UpdateProduct` Aşırı yükte eşleyerek.

[![dört giriş parametresi kabul eden UpdateProduct yöntemi aşırı yüklemesini kullanın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image1.png)

**Şekil 1**: dört giriş parametresi kabul eden `UpdateProduct` yöntemi aşırı yüklemesini kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image3.png))

Bu, dört parametreli `UpdateParameters` koleksiyonu olan bir ObjectDataSource ve ürün alanlarının her biri için bir alan içeren bir GridView oluşturur. ObjectDataSource 'un bildirime dayalı biçimlendirmesi `OldValuesParameterFormatString` özelliğini `original_{0}`atar, bu da BLL sınıfınızın `original_productID` adlı bir giriş parametresi beklemediği için bir özel duruma neden olur. Bu ayarı, bildirime dayalı sözdiziminden tamamen kaldırmayı unutmayın (veya varsayılan değere ayarlayın, `{0}`).

Daha sonra, GridView 'un yalnızca `ProductName`, `QuantityPerUnit`, `UnitPrice`ve `UnitsInStock` BoundFields içermesini sağlar. Ayrıca, gerekli olan herhangi bir alan düzeyi biçimlendirme (`HeaderText` özelliklerini değiştirme gibi) uygulamayı da ücretsiz olarak kullanabilirsiniz.

Önceki öğreticide, `UnitPrice` BoundField 'ı hem salt okuma modunda hem de düzenleme modunda bir para birimi olarak biçimlendirme hakkında bilgi verdik. Burada aynı şekilde yapalim. Bu, Şekil 2 ' de gösterildiği gibi, BoundField 'un `DataFormatString` özelliğini `{0:c}`, `HtmlEncode` özelliğini `false`ve `ApplyFormatInEditMode` `true`olarak ayarlamayı unutmayın.

[![UnitPrice BoundField 'ı para birimi olarak görüntülenecek şekilde yapılandırın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image4.png)

**Şekil 2**: `UnitPrice` BoundField öğesini para birimi olarak görüntülenecek şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image6.png))

`UnitPrice`, düzen arabirimindeki bir para birimi olarak biçimlendirmek için, para birimi biçimli dizeyi bir `decimal` değere ayrıştırır ve GridView 'un `RowUpdating` olayı için bir olay işleyicisi oluşturulması gerekir. Kullanıcının bir `UnitPrice` değer sağlalarından emin olmak için son öğreticiden `RowUpdating` olay işleyicisinin de kontrol olduğunu unutmayın. Bununla birlikte, bu öğretici için kullanıcının fiyatı yok saymasına izin verlim.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample2.vb)]

GridView, bir `QuantityPerUnit` BoundField içerir, ancak bu BoundField yalnızca görüntüleme amacıyla olmalıdır ve Kullanıcı tarafından düzenlenememelidir. Bunu düzenlemek için, BoundFields ' `ReadOnly` özelliğini `true`olarak ayarlamanız yeterlidir.

[![, QuantityPerUnit BoundField öğesini salt okunurdur hale getirme](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image7.png)

**Şekil 3**: `QuantityPerUnit` BoundField öğesini salt okunurdur yapma ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image9.png))

Son olarak, GridView 'un akıllı etiketindeki Düzenle özelliğini etkinleştir onay kutusunu işaretleyin. Bu adımları tamamladıktan sonra, `ErrorHandling.aspx` sayfasının tasarımcısı Şekil 4 ' e benzer görünmelidir.

[Gerekli BoundFields alanlarını kaldırmak ![ve Düzenle etkinleştir onay kutusunu Işaretleyin](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image10.png)

**Şekil 4**: gerekli boundfields alanlarını kaldırın ve Düzenle etkinleştir onay kutusunu işaretleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image12.png))

Bu noktada, tüm ürünlerin ' `ProductName`, `QuantityPerUnit`, `UnitPrice`ve `UnitsInStock` alanlarının bir listesi vardır; Ancak, yalnızca `ProductName`, `UnitPrice`ve `UnitsInStock` alanları düzenlenebilir.

[![kullanıcılar artık hisse senedi alanlarında ürünlerin adlarını, fiyatlarını ve birimlerini kolayca düzenleyebilir](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image13.png)

**Şekil 5**: kullanıcılar artık hisse senedi alanlarında ürünlerin adlarını, fiyatlarını ve birimlerini kolayca düzenleyebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image15.png))

## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>2\. Adım: DAL düzeyinde özel durumları düzgün şekilde Işleme

Düzenlenebilir GridView, kullanıcılar düzenlenmiş ürünün adı, fiyatı ve stok birimleri için geçerli değerler girerken wonderfully çalışırken, geçersiz değerler girilmesi özel bir duruma neden olur. Örneğin, `ProductName` değeri kullanılmazsa, `ProductsRow` sınıfındaki `ProductName` özelliğinin `AllowDBNull` özelliği `false`olarak ayarlanmış olduğundan, [Ullallowedexception](https://msdn.microsoft.com/library/default.asp?url=/library/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp) oluşturulmasına neden olur. veritabanı kapalıysa, veritabanına bağlanmaya çalışılırken TableAdapter tarafından bir `SqlException` atılır. Herhangi bir eylemde bulunmadan, bu özel durumlar veri erişim katmanından Iş mantığı katmanına, ardından ASP.NET sayfasına ve son olarak ASP.NET çalışma zamanına göre balon üzerinden yapılır.

Web uygulamanızın nasıl yapılandırıldığına ve uygulamayı `localhost`ziyaret edip etmediğine bağlı olarak, işlenmeyen bir özel durum genel sunucu hatası sayfasına, ayrıntılı bir hata raporuna veya Kullanıcı dostu bir Web sayfasına neden olabilir. ASP.NET çalışma zamanının yakalanamayan bir özel duruma yanıt vermesi hakkında daha fazla bilgi için bkz. ASP.NET ve [customErrors öğesinde](https://msdn.microsoft.com/library/h0hfz6fc(VS.80).aspx) [Web uygulaması hata işleme](http://www.15seconds.com/issue/030102.htm) .

Şekil 6 `ProductName` değerini belirtmeden bir ürünü güncelleştirmeye çalışırken karşılaşılan ekranı gösterir. Bu, `localhost`üzerinden geldiğinde varsayılan ayrıntılı hata raporunun görüntülendiğini bildirir.

[Ürün adının atlanması ![, özel durum ayrıntılarını görüntüler](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image16.png)

**Şekil 6**: ürünün adının atlanması, özel durum ayrıntılarını görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image18.png))

Bu tür özel durum ayrıntıları, bir uygulamayı test ederken yararlı olsa da, bir özel durum durumunda bu ekran ile bir son kullanıcı sunumu ideal olarak küçüktür. Son Kullanıcı büyük olasılıkla `NoNullAllowedException` ne olduğunu veya neden neden olduğunu bilmez. Daha iyi bir yaklaşım, kullanıcıyı güncelleştirmeye çalışırken bir sorun olduğunu açıklayan daha Kullanıcı dostu bir iletiyle sunmasıdır.

İşlemi gerçekleştirirken bir özel durum oluşursa, hem ObjectDataSource hem de Data Web denetimindeki en son düzey olaylar, bunu tespit etmek ve özel durumu ASP.NET çalışma zamanına kadar kabarcıklanma 'dan iptal etmek için bir yol sağlar. Bizim örneğimizde, bir özel durumun tetikleyip tetiklenmeyeceğini belirleyen GridView 'un `RowUpdated` olayı için bir olay işleyicisi oluşturalım ve varsa, özel durum ayrıntılarını bir etiket Web denetiminde görüntüler.

ASP.NET sayfasına bir etiket ekleyerek başlayın, `ID` özelliğini `ExceptionDetails` olarak ayarlayıp `Text` özelliğini temizleyerek. Kullanıcının bu iletiye göz çekmesini sağlamak için, `CssClass` özelliğini, önceki öğreticideki `Styles.css` dosyasına eklediğimiz bir CSS sınıfı olan `Warning`olarak ayarlayın. Bu CSS sınıfının etiket metninin kırmızı, italik, kalın ve çok büyük yazı tipinde görüntülenmesine neden olduğunu unutmayın.

[Sayfaya bir etiket Web denetimi eklemek ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image19.png)

**Şekil 7**: sayfaya bir etiket Web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image21.png))

Bu etiket Web denetiminin yalnızca bir özel durum oluşturulduktan hemen sonra görünmesini istiyoruz, `Page_Load` olay işleyicisinde `Visible` özelliğini false olarak ayarlayın:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample3.vb)]

Bu kodla, ilk sayfada ziyaret eden geri göndermeler ve sonraki geri göndermeler `ExceptionDetails` denetimin `Visible` özelliği `false`olarak ayarlanmıştır. Bir DAL ya da BLL düzeyi özel durumunun, GridView 'un `RowUpdated` olay işleyicisinde algılayabilmemiz durumunda, `ExceptionDetails` denetiminin `Visible` özelliğini true olarak ayarlayacağız. Web denetimi olay işleyicileri sayfa yaşam döngüsünün `Page_Load` olay işleyiciden sonra gerçekleşmesinden, etiket gösterilir. Bununla birlikte, bir sonraki geri göndermede, `Page_Load` olay işleyicisi `Visible` özelliğini `false`geri döndürecek ve yeniden görünümden Gizleyeceğiniz.

> [!NOTE]
> Alternatif olarak, bildirim temelli sözdiziminde `Visible` özelliği `false` atayarak ve görünüm durumunu devre dışı bırakarak (`EnableViewState` özelliğini `false`olarak ayarlayarak) `Page_Load` `ExceptionDetails` denetimin `Visible` özelliğini ayarlamak için zorunludur 'yi kaldırabiliriz. Bu alternatif yaklaşımı gelecekteki bir öğreticide kullanacağız.

Etiket denetimi eklendiğinde, sonraki adımımız GridView 'un `RowUpdated` olayı için olay işleyicisi oluşturmaktır. Tasarımcıda GridView ' i seçin, Özellikler penceresi gidin ve daha sonra GridView 'un olaylarını listeleyerek şimşek simgesine tıklayın. Bu öğreticide daha önce bu olay için bir olay işleyicisi oluşturduğumuz, GridView 'un `RowUpdating` olayı için bir giriş olmalıdır. `RowUpdated` olayı için de bir olay işleyicisi oluşturun.

![GridView 'un RowUpdated olayı için bir olay Işleyicisi oluşturun](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image22.png)

**Şekil 8**: GridView 'un `RowUpdated` olayı Için bir olay işleyicisi oluşturun

> [!NOTE]
> Ayrıca, arka plan kod sınıfı dosyasının en üstündeki açılan listelerden olay işleyicisini de oluşturabilirsiniz. Sol taraftaki açılan listeden GridView ' i ve sağdaki `RowUpdated` olayını seçin.

Bu olay işleyicisini oluşturmak, ASP.NET sayfasının arka plan kod sınıfına aşağıdaki kodu ekler:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample4.vb)]

Bu olay işleyicisinin ikinci giriş parametresi, özel durumları işlemek için ilgilendiğiniz üç özellik içeren [GridViewUpdatedEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx)türünde bir nesnedir:

- oluşturulan özel duruma bir başvuru `Exception`; hiçbir özel durum atılmışsa, bu özelliğin değeri `null` olur
- özel durumun `RowUpdated` olay işleyicisinde işlenip işlenmediğini gösteren bir Boole değeri `ExceptionHandled`; `false` (varsayılan), özel durum, ASP.NET çalışma zamanına kadar bir yeniden oluşturulur.
- Düzenlenmiş GridView satırı `true` olarak ayarlanırsa `KeepInEditMode` düzenleme modunda kalır; `false` (varsayılan), GridView satırı salt okunurdur moduna geri döner

Bu durumda, `Exception` `null`olup olmadığını kontrol etmelidir, yani işlem gerçekleştirilirken bir özel durum ortaya çıkar. Böyle bir durum söz konusu olduğunda şunları yapmak istiyoruz:

- `ExceptionDetails` etiketinde Kullanıcı dostu bir ileti görüntüle
- Özel durumun işlendiğini belirtin
- GridView satırını düzenleme modunda tut

Aşağıdaki kod bu hedefleri gerçekleştirir:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample5.vb)]

Bu olay işleyicisi, `e.Exception` `null`olup olmadığını denetleyerek başlar. Aksi takdirde, `ExceptionDetails` etiketinin `Visible` özelliği `true` ve `Text` özelliği "ürünü güncelleştirirken bir sorun oluştu." olarak ayarlanır. Oluşturulan gerçek özel durumun ayrıntıları `e.Exception` nesnenin `InnerException` özelliğinde yer alır. Bu iç özel durum incelenir ve belirli bir tür ise, `ExceptionDetails` etiketin `Text` özelliğine ek ve yararlı bir ileti eklenir. Son olarak, `ExceptionHandled` ve `KeepInEditMode` özelliklerinin ikisi de `true`olarak ayarlanmıştır.

Şekil 9 ürünün adını atlayarak bu sayfanın ekran görüntüsünü gösterir; Şekil 10 geçersiz bir `UnitPrice` değeri (-50) girerken sonuçları gösterir.

[![, BoundField değeri Içermelidir](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image23.png)

**Şekil 9**: `ProductName` BoundField bir değer içermelidir ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image25.png))

[![negatif UnitPrice değerine Izin verilmez](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image26.png)

**Şekil 10**: negatif `UnitPrice` değerlere izin verilmez ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image28.png))

`e.ExceptionHandled` özelliğini `true`olarak ayarlayarak `RowUpdated` olay işleyicisi özel durumu işlediğinin gösterdi. Bu nedenle, özel durum ASP.NET çalışma zamanına yayılmaz.

> [!NOTE]
> Şekil 9 ve 10, geçersiz kullanıcı girişi nedeniyle oluşturulan özel durumları işlemek için düzgün bir yol gösterir. İdeal olarak, bu tür geçersiz girişler ilk yerde Iş mantığı katmanına hiçbir şekilde ulaşmayacaktır, çünkü ASP.NET sayfası, `ProductsBLL` sınıfının `UpdateProduct` yöntemini çağırmadan önce kullanıcının girişlerinin geçerli olduğundan emin olmalıdır. Bir sonraki öğreticimizde, Iş mantığı katmanına gönderilen verilerin iş kurallarına uygun olduğundan emin olmak için, ekleme ve arabirimlerin nasıl doğrulanabileceksiniz hakkında bilgi edineceksiniz. Doğrulama denetimleri, Kullanıcı tarafından sağlanan veriler geçerli olana kadar `UpdateProduct` yönteminin çağrılmasını engellemez, ancak aynı zamanda veri girişi sorunlarını tanımlamaya yönelik daha bilgilendirici bir kullanıcı deneyimi sağlar.

## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>3\. Adım: BLL düzeyi özel durumları düzgün şekilde Işleme

Veri ekleme, güncelleştirme veya silme sırasında, veri erişim katmanı, verilerle ilgili bir hatanın karşısında bir özel durum oluşturabilir. Veritabanı çevrimdışı olabilir, gerekli bir veritabanı tablosu sütununda belirtilen bir değer bulunmayabilir veya tablo düzeyi kısıtlaması ihlal edilmiş olabilir. Tamamen verilerle ilgili özel durumların yanı sıra, Iş mantığı katmanı iş kurallarının ihlal edildiğini göstermek için özel durumlar kullanabilir. [Iş mantığı katmanı oluşturma](../introduction/creating-a-business-logic-layer-vb.md) öğreticisinde, örneğin, özgün `UpdateProduct` aşırı yüküne bir iş kuralı denetimi ekledik. Özellikle, Kullanıcı bir ürünü kullanımdan kaldırıldı olarak işaretlerken, ürünün tedarikçiden temin ettiğimiz tek bir ürün olmaması gerekiyordu. Bu durum ihlal edilirse, bir `ApplicationException` oluşturulur.

Bu öğreticide oluşturulan `UpdateProduct` aşırı yüklemesi için, `UnitPrice` alanın özgün `UnitPrice` değerinin iki katından daha fazla yeni bir değere ayarlanmasına imkan tanıyan bir iş kuralı ekleyelim. Bunu gerçekleştirmek için `UpdateProduct` aşırı yüklemesini bu denetimi gerçekleştirecek şekilde ayarlayın ve kural ihlal edilirse bir `ApplicationException` oluşturur. Updated yöntemi aşağıda verilmiştir:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample6.vb)]

Bu değişiklik ile, var olan fiyattan iki kat daha fazla olan fiyat güncelleştirmesi `ApplicationException` oluşturulmasına neden olur. DAL tarafından oluşturulan özel durum gibi, bu BLL-yükseltilen `ApplicationException`, GridView 'un `RowUpdated` olay işleyicisinde algılanır ve işlenebilir. Aslında, `RowUpdated` olay işleyicisinin kodu yazıldığı gibi, bu özel durumu doğru bir şekilde algılar ve `ApplicationException``Message` özellik değerini görüntüler. Şekil 11 ' de, bir Kullanıcı Chai 'nin fiyatını $50,00 ' den daha büyük olan $19,95 ' e güncelleştirmeyi denediğinde bir ekran görüntüsü gösterilir.

[Iş kuralları ![, fiyata Izin vermeyen bir ürünün fiyatından daha fazla](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image29.png)

**Şekil 11**: iş kuralları, fiyata izin vermeyen bir ürünün fiyatından daha fazla ([tam boyutlu görüntüyü görüntülemek için tıklatın](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image31.png))

> [!NOTE]
> İdeal olarak iş mantığı kurallarımız, `UpdateProduct` yöntemi aşırı yüklerini ve ortak bir yöntemi yeniden düzenlenmiş. Bu, okuyucu için bir alıştırma olarak kalır.

## <a name="summary"></a>Özet

Ekleme, güncelleştirme ve silme işlemleri sırasında, hem veri Web denetimi hem de ObjectDataSource, gerçek işlemi izleyen ön ve son düzey olayları harekete geçirme ile ilgilidir. Bu öğreticide ve önceki bir yapıda çalışırken, GridView 'un `RowUpdating` olayı harekete geçirilir ve ardından ObjectDataSource 'un temel alınan nesnesine Update komutu yapıldığında, ObjectDataSource 'un `Updating` olayı izlenir. İşlem tamamlandıktan sonra, ObjectDataSource 'un `Updated` olayı harekete geçirilir ve ardından GridView 'un `RowUpdated` olayı izlenir.

İşlem sonuçlarını incelemek ve yanıtlamak için giriş parametrelerini veya son düzey olayları özelleştirmek amacıyla, ön seviye olaylar için olay işleyicileri oluşturalım. Son düzey olay işleyicileri, işlem sırasında bir özel durumun oluşup oluşmadığını saptamak için en yaygın olarak kullanılır. Bir özel durumun söz konusu olduğunda, bu düzey son olay işleyicileri isteğe bağlı olarak kendi özel durumunu işleyebilir. Bu öğreticide, kolay bir hata iletisi görüntüleyerek böyle bir özel durumu nasıl işleyeceğinizi gördük.

Sonraki öğreticide, veri biçimlendirme sorunlarından kaynaklanan özel durumların olasılığını nasıl azaltabileceğiz (örneğin, negatif bir `UnitPrice`girme). Özellikle, Düzenle ve arabirimleri ekleme hakkında doğrulama denetimleri ekleme bölümüne bakacağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren Liz Öğeledi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
> [İleri](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
