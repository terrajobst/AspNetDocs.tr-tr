---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
title: DataList 'te verileri düzenlemeyle ve silmeye genel bakış (C#) | Microsoft Docs
author: rick-anderson
description: DataList 'in yerleşik olarak düzenlenmesinin ve silinmesinin eksik olması halinde, bu öğreticide, o dili düzenlemenizi ve silmeyi destekleyen bir DataList oluşturmayı inceleyeceğiz...
ms.author: riande
ms.date: 10/30/2006
ms.assetid: c3b0c86e-fe98-41ee-b26f-ca38cddaa75e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 481c9a14b1ebfe36ffcddd0237701bc04266e393
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74629307"
---
# <a name="an-overview-of-editing-and-deleting-data-in-the-datalist-c"></a>DataList (C#) Içinde verileri düzenlemeyle ve silmeye genel bakış

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_CS.exe) veya [PDF 'yi indirin](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/datatutorial36cs1.pdf)

> DataList 'in yerleşik olarak düzenlenen ve silinen özellikleri olmadığı sürece, bu öğreticide, temel alınan verilerinin düzenlenmesinin ve silinmesini destekleyen bir DataList oluşturmayı öğreneceksiniz.

## <a name="introduction"></a>Giriş

[Verileri ekleme, güncelleştirme ve silme konusunda genel bir bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) için, uygulama mimarisi, bir ObjectDataSource ve GridView, DetailsView ve FormView denetimleri kullanılarak veri ekleme, güncelleştirme ve silme işlemlerinin nasıl yapıldığını inceledik. ObjectDataSource ve bu üç veri Web denetimi ile basit veri değiştirme arabirimlerini uygulamak, bir snap ve yalnızca akıllı etiketten bir onay kutusu gösteriydi. Yazılması gereken kod yok.

Ne yazık ki DataList, GridView denetiminde devralınan yerleşik bir Düzenle ve silme özelliğine sahip değildir. Bildirim temelli veri kaynağı denetimleri ve kod içermeyen veri değişikliği sayfaları kullanılamadığında, bu eksik işlevsellik, DataList 'in önceki ASP.NET sürümünden bir relik olmasından kaynaklanır. ASP.NET 2,0 ' deki DataList, GridView olarak Box veri değiştirme yeteneklerini sunmadığından, bu işlevselliği dahil etmek için ASP.NET 1. x tekniklerini kullanabiliriz. Bu yaklaşım için bir kod gerekir, ancak bu öğreticide göreceğiniz gibi DataList 'in bu işlemde yardımcı olacak bazı olaylar ve özellikler vardır.

Bu öğreticide, temel alınan verilerinin düzenlenmesinin ve silinmesini destekleyen bir DataList oluşturma hakkında bilgi edineceksiniz. Gelecekteki öğreticiler, giriş alanı doğrulaması, veri erişimi veya Iş mantığı katmanlarından oluşan özel durumları düzgün bir şekilde işleme gibi daha gelişmiş düzenlemeler ve silme senaryolarına de olanak sağlayacak.

> [!NOTE]
> DataList gibi, Repeater denetimi ekleme, güncelleştirme veya silme için kutudan çıkan işlevlerden yokdur. Bu işlevsellik eklenebilirken, DataList, bu tür özellikleri eklemeyi kolaylaştıran yineleyicisi 'nde bulunmayan özellikleri ve olayları içerir. Bu nedenle, bu öğretici ve ileride düzenlenecek ve silinenler, DataList 'e tamamen odaklanacaktır.

## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>1\. Adım: Öğreticiler oluşturma ve silme Web sayfaları

Bir DataList 'ten verileri güncelleştirme ve silme konusunda keşfetmeye başlamadan önce, bu öğreticide ve sonraki birkaç adımda gerekli olacak web sitesi projemizdeki ASP.NET sayfalarını oluşturmak için bir süre sürme. `EditDeleteDataList`adlı yeni bir klasör ekleyerek başlayın. Ardından, aşağıdaki ASP.NET sayfalarını bu klasöre ekleyerek her bir sayfayı `Site.master` ana sayfasıyla ilişkilendirdiğinizden emin olun:

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![Öğreticiler için ASP.NET sayfaları ekleme](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image1.png)

**Şekil 1**: öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `EditDeleteDataList` klasöründeki `Default.aspx`, konusundaki öğreticileri de listeler. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image2.png)

**Şekil 2**: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image4.png))

Son olarak, sayfaları `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, DataList ve Repeater `<siteMapNode>`ile ana/ayrıntı raporlarından sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık DataList düzenlemesi ve öğreticileri silmek için öğeler içerir.

![Site Haritası artık DataList düzenlemesi ve öğreticileri silme için girdiler Içerir](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image5.png)

**Şekil 3**: site haritası artık DataList düzenlemesi ve öğreticileri silme Için girdiler içerir

## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>2\. Adım: verileri güncelleştirme ve silmeye yönelik teknikleri Inceleme

GridView ile verileri düzenlemenin ve silmenin daha kolay olması nedeniyle, kapsamanın yanı sıra GridView ve ObjectDataSource Concert 'da çalışır. [Ekleme, güncelleştirme ve silme öğreticisi Ile Ilişkili olayları İnceleme](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) bölümünde açıklandığı gibi, bir satır s Update düğmesine tıklandığında, GridView, iki yönlü veri `UpdateParameters` bağlamasını kullanan alanlarını otomatik olarak atar ve ardından bu objectdatasource s `Update()` metodunu çağırır.

Burada, DataList bu yerleşik işlevlerden herhangi birini sağlamıyor. Kullanıcı değerlerinin, ObjectDataSource 'un parametrelerine atandığından ve `Update()` yönteminin çağrıldığından emin olmak bizim sorumluluğunuzdadır. Bu Endeavor bizimle yardım etmek için, DataList aşağıdaki özellikleri ve olayları sağlar:

- Güncelleştirme veya silme sırasında **[`DataKeyField` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx)** , DataList 'te her öğeyi benzersiz bir şekilde tanımlayabilmelidir. Bu özelliği, görünen verilerin birincil anahtar alanı olarak ayarlayın. Bunun yapılması, DataList s [`DataKeys` koleksiyonunu](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx) her DataList öğesi için belirtilen `DataKeyField` değeriyle dolduracaktır.
- **[`EditCommand` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx)** , `CommandName` özelliği Düzenle olarak ayarlanan bir Button, LinkButton veya ImageButton tıklandığında harekete geçirilir.
- **[`CancelCommand` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx)** , `CommandName` özelliği Cancel olarak ayarlanan bir Button, LinkButton veya ImageButton tıklandığında harekete geçirilir.
- **[`UpdateCommand` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx)** , `CommandName` özelliği Update olarak ayarlanan bir Button, LinkButton veya ImageButton tıklandığında harekete geçirilir.
- **[`DeleteCommand` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx)** , `CommandName` özelliği Delete olarak ayarlanan bir Button, LinkButton veya ImageButton tıklandığında harekete geçirilir.

Bu özellikleri ve olayları kullanarak DataList 'teki verileri güncelleştirmek ve silmek için kullanabileceğiniz dört yaklaşım vardır:

1. **ASP.NET 1. x tekniklerini kullanarak** DataList, ASP.NET 2,0 ve objectdatasources 'tan önce vardı ve verileri programlama yoluyla tamamen güncelleştirebilir ve silebilir. Bu teknik, ObjectDataSource 'u tamamen geri alır ve verileri doğrudan Iş mantığı katmanından, her ikisi de görüntülenecek verileri alma ve bir kaydı güncelleştirirken ya da silen bir şekilde bağladık.
2. DataList 'in, GridView tarafından devralınan ve silinen özellikleri olmadığı sürece **seçme, güncelleme ve silme Için sayfada tek bir ObjectDataSource denetimi kullanmak** , bunları kendimize 'e ekleyemediğimiz bir neden yok. Bu yaklaşımda, GridView örneklerinde olduğu gibi bir ObjectDataSource kullanıyoruz, ancak ObjectDataSource s `UpdateCommand` olayı için, ObjectDataSource s parametrelerini ayarladığımız ve `Update()` metodunu çağıran bir olay işleyicisi oluşturması gerekir.
3. **Seçim için bir ObjectDataSource denetimi kullanma, ancak seçenek 2 ' yi kullanırken BLL Ile doğrudan güncelleştirme ve silme** , `UpdateCommand` olayına bir kod yazmanız, parametre değerleri atanması ve bu şekilde devam etmemiz gerekir. Bunun yerine, seçme için ObjectDataSource 'u kullanmayı ve doğrudan BLL 'ye karşı (1. seçenek gibi) çağrı yapmayı ve silmeyi seçebilirsiniz. Görüşimde doğrudan BLL ile veri güncelleştirme, ObjectDataSource 'un `UpdateParameters` ve `Update()` metodunu çağırarak daha fazla okunabilir kod sağlar.
4. **Bildirim kullanımı birden çok ObjectDataSources aracılığıyla** , önceki üç yaklaşımın hepsi bir kod gerektirir. Mümkün olduğunca çok bildirimli sözdizimi kullanmaya devam ediyorsanız, son bir seçenek sayfada birden çok ObjectDataSources bulundurmadır. İlk ObjectDataSource, verileri BLL 'den alır ve DataList 'e bağlar. Güncelleştirme için başka bir ObjectDataSource eklenir, ancak doğrudan DataList s `EditItemTemplate`içinde eklenir. Silme desteğini dahil etmek için `ItemTemplate`başka bir ObjectDataSource olması gerekir. Bu yaklaşımla birlikte, bu ekli ObjectDataSource, ObjectDataSource s parametrelerini Kullanıcı giriş denetimlerine bildirimli olarak bağlamak için `ControlParameters` kullanır (bunları DataList s `UpdateCommand` olay işleyicisinde programlama yoluyla belirtmek zorunda kalmak yerine). Bu yaklaşım, gömülü ObjectDataSource `Update()` veya `Delete()` komutunu çağırmam gereken ancak diğer üç yaklaşımdan çok daha az bir kod gerektirir. Buradaki altkenar, birden çok ObjectDataSources 'ın sayfanın kalabalıklığını ayıracaktır, genel okunabilirlik üzerinden

Yalnızca bu yaklaşımlardan birini kullanmaya zorlanırsa, en fazla esneklik sağladığından ve DataList 'in bu düzene uyum sağlayacak şekilde tasarlandığından, 1 seçeneğini seçtim. DataList, ASP.NET 2,0 veri kaynağı denetimleriyle çalışacak şekilde genişletilirken, resmi ASP.NET 2,0 veri Web denetimlerinin (GridView, DetailsView ve FormView) tüm genişletilebilirlik noktalarına veya özelliklerine sahip değildir. 2 ile 4 arasındaki seçenekler Merit olmadan değildir, ancak.

Bu ve gelecekte düzenlenecek olan öğreticiler, verileri güncelleştirmek ve silmek için BLL 'ye doğrudan çağrı yapmak için bir ObjectDataSource kullanır (seçenek 3).

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>3\. Adım: DataList 'i ekleme ve ObjectDataSource 'ı yapılandırma

Bu öğreticide, ürün bilgilerini listeleyen bir DataList oluşturacağız ve her ürün için, kullanıcıya adı ve fiyatı düzenleme ve ürünü tamamen silme yeteneği sağlar. Özellikle, bir ObjectDataSource kullanarak görüntülenecek kayıtları alacak, ancak BLL ile doğrudan bir şekilde güncelleştirme ve silme eylemleri gerçekleştirecek. DataList 'e, oluşturma ve silme yeteneklerini uygulama konusunda endişelenmekten önce, ilk olarak ürünleri salt bir salt okuma arabiriminde görüntüleme sayfasına ulaşın. Önceki öğreticilerde bu adımları incelediğimiz için, onları hızla ilerliyoruz.

`EditDeleteDataList` klasöründeki `Basics.aspx` sayfasını açıp Tasarım görünümü sayfada bir DataList ekleyin. Ardından, DataList s akıllı etiketinden yeni bir ObjectDataSource oluşturun. Ürün verileriyle çalıştık ve bu, `ProductsBLL` sınıfını kullanacak şekilde yapılandırın. *Tüm* ürünleri almak IÇIN, seç sekmesinden `GetProducts()` yöntemini seçin.

[![, ObjectDataSource 'ı ProductsBLL sınıfını kullanacak şekilde yapılandırma](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image6.png)

**Şekil 4**: ObjectDataSource 'ı `ProductsBLL` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image8.png))

[![GetProducts () yöntemini kullanarak ürün bilgilerini döndürün](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image9.png)

**Şekil 5**: `GetProducts()` yöntemini kullanarak ürün bilgilerini döndürün ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image11.png))

GridView gibi DataList, yeni veri eklemek için tasarlanmamıştır; Bu nedenle, Ekle sekmesindeki aşağı açılan listeden (hiçbiri) seçeneğini belirleyin. Güncelleştirmeler ve silmeler BLL aracılığıyla programlı olarak gerçekleştirileceği için GÜNCELLEŞTIRME ve SILME sekmeleri için de (yok) seçeneğini belirleyin.

[![, ObjectDataSource 'un INSERT, UPDATE ve DELETE sekmelerinde açılan listelerin (yok) olarak ayarlandığını onaylayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image12.png)

**Şekil 6**: OBJECTDATASOURCE 'un INSERT, Update ve DELETE sekmelerinde açılan listelerin (yok) olarak ayarlandığını onaylayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image14.png))

ObjectDataSource yapılandırıldıktan sonra, son ' a tıklayarak tasarımcıya geri döner. Geçmiş örneklerde yaptığımız gibi, ObjectDataSource yapılandırması tamamlanırken, Visual Studio otomatik olarak DropDownList için bir `ItemTemplate` oluşturur ve her veri alanını görüntüler. Bu `ItemTemplate` yalnızca ürün adı ve fiyatını görüntüleyen bir ile değiştirin. Ayrıca, `RepeatColumns` özelliğini 2 olarak ayarlayın.

> [!NOTE]
> *Verileri ekleme, güncelleştirme ve silme konusunda genel bakış* Öğreticimizi kullanarak verileri değiştirirken mimarimiz, ObjectDataSource 'un bildirim temelli işaretlemelerinden `OldValuesParameterFormatString` özelliğini kaldırmamız gerekir (veya varsayılan değerine sıfırlamanız `{0}`). Bununla birlikte, bu öğreticide yalnızca verileri almak için ObjectDataSource kullanıyoruz. Bu nedenle, ObjectDataSource 'un `OldValuesParameterFormatString` özellik değerini değiştirmesi gerekmez (öyle olmasa da, bunu yapamamakla kalmaz).

Varsayılan DataList `ItemTemplate` öğesini özelleştirilmiş bir şekilde değiştirdikten sonra, sayfanızdaki bildirim temelli biçimlendirme şuna benzer olmalıdır:

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample2.aspx)]

Bir tarayıcıdan ilerleme durumunu görüntülemek için bir dakikanızı ayırın. Şekil 7 ' de gösterildiği gibi, DataList her ürün için ürün adını ve birim fiyatını iki sütunda görüntüler.

[![ürünlerin adları ve fiyatları Iki sütunlu bir DataList 'te görüntülenir](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image15.png)

**Şekil 7**: ürün adları ve fiyatları iki sütunlu bir DataList 'te görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image17.png))

> [!NOTE]
> DataList, güncelleme ve silme işlemi için gereken birçok özelliğe sahiptir ve bu değerler Görünüm durumunda depolanır. Bu nedenle, verileri düzenlemenizi veya silmeyi destekleyen bir DataList oluştururken, DataList s görünüm durumunun etkinleştirilmesi önemlidir.  
>   
> Kurnaz okuyucusu düzenlenebilir GridViews, Ayrıntılar görünümleri ve formviews oluştururken görünüm durumunu devre dışı bırakadığımızda hatırlayabiliriz. Bunun nedeni, ASP.NET 2,0 Web denetimlerinin, Görünüm durumu gibi geri göndermeler arasında durum kalıcı olan ancak önemli olarak kabul edildiği *denetim durumunu*içerebileceğinden kaynaklanır.

GridView 'da görünüm durumunu devre dışı bırakmak, yalnızca önemsiz durum bilgilerini atlar, ancak denetim durumunu korur (Bu durum, düzen ve silme için gereken durumu içerir). ASP.NET 1. x zaman diliminde oluşturulan DataList, denetim durumunu kullanmaz ve bu nedenle görünüm durumunun etkin olması gerekir. Denetim durumu ve Görünüm durumu hakkında daha fazla bilgi için bkz. denetim durumu ve [Görünüm durumu karşılaştırması](https://msdn.microsoft.com/library/1whwt1k7.aspx) .

## <a name="step-4-adding-an-editing-user-interface"></a>4\. Adım: bir kullanıcı arabirimi düzenlemesi ekleme

GridView denetimi bir alanlar topluluğundan oluşur (BoundFields, CheckBoxFields, TemplateFields vb.). Bu alanlar, kendi işlenmiş işaretlemesini moduna göre ayarlayabilir. Örneğin, salt okuma modundayken, bir BoundField veri alanı değerini metin olarak görüntüler; düzenleme modundayken, `Text` özelliğine veri alanı değeri atanmış bir TextBox Web denetimi oluşturur.

Diğer yandan DataList, kendi öğelerini şablonlar kullanarak işler. Salt okuma öğeleri `ItemTemplate` kullanılarak işlenir, düzenleme modundaki öğeler `EditItemTemplate`aracılığıyla işlenir. Bu noktada, DataList 'umuz yalnızca bir `ItemTemplate`sahiptir. Öğe düzeyinde düzenleme işlevselliğini desteklemek için, düzenlenebilir öğe için gösterilecek biçimlendirmeyi içeren bir `EditItemTemplate` eklememiz gerekir. Bu öğreticide, ürün adı ve birim fiyatını düzenlemekte kullanılacak metin kutusu Web denetimlerini kullanacağız.

`EditItemTemplate`, bildirimli olarak veya tasarımcı aracılığıyla oluşturulabilir (DataList s akıllı etiketindeki Şablonları Düzenle seçeneği seçilerek). Şablonları Düzenle seçeneğini kullanmak için, önce akıllı etiketteki Şablonları Düzenle bağlantısına tıklayın ve ardından açılır listeden `EditItemTemplate` öğesini seçin.

[![DataList s EditItemTemplate ile çalışmayı kabul etme](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image18.png)

**Şekil 8**: DataList s `EditItemTemplate` ile çalışmayı kabul etme ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image20.png))

Ardından, ürün adı: ve fiyat: yazın ve ardından araç kutusundan iki TextBox denetimini tasarımcıda `EditItemTemplate` arabirimine sürükleyin. TextBoxes `ID` özelliklerini `ProductName` ve `UnitPrice`olarak ayarlayın.

[![ürün adı ve fiyat için bir metin kutusu ekleyin](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image21.png)

**Şekil 9**: ürün s adı ve fiyat Için bir metin kutusu ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image23.png))

Karşılık gelen ürün verileri alan değerlerini iki metin kutularının `Text` özelliklerine bağlamız gerekir. TextBoxes Akıllı Etiketler ' de, DataBindings düzenle bağlantısına tıklayın ve ardından şekil 10 ' da gösterildiği gibi uygun veri alanını `Text` özelliği ile ilişkilendirin.

> [!NOTE]
> `UnitPrice` veri alanını fiyat metin kutusu s `Text` alanına bağlarken, bunu bir para birimi değeri (`{0:C}`), genel bir sayı (`{0:N}`) olarak biçimlendirebilir veya biçimlendirilmemiş olarak bırakabilirsiniz.

![ProductName ve BirimFiyat veri alanlarını metin kutularının metin özelliklerine bağlayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image24.png)

**Şekil 10**: `ProductName` ve `UnitPrice` veri alanlarını metin kutularının `Text` özelliklerine bağlama

Şekil 10 ' da DataBindings düzenleme iletişim kutusunun, GridView veya DetailsView 'da TemplateField veya FormView 'daki bir şablon düzenlenirken mevcut olan Iki yönlü veri bağlama onay kutusunu *nasıl içermediği hakkında* dikkat edin. İki yönlü veri bağlama özelliği, giriş Web denetimine girilen değerin, verileri eklerken veya güncelleştirirken `InsertParameters` veya `UpdateParameters` ilgili ObjectDataSource 'a otomatik olarak atanması için izin verilir. DataList, bu öğreticide daha sonra göreceğiniz şekilde iki yönlü veri bağlamayı desteklemez. Kullanıcı, değişiklikleri yaptıktan ve verileri güncelleştirmeye hazırladıktan sonra, bu metin kutularına Özellikler `Text` ve değerlerini `ProductsBLL` sınıfındaki uygun `UpdateProduct` yöntemine geçirmemiz gerekir.

Son olarak, `EditItemTemplate`güncelleştirme ve Iptal düğmeleri eklememiz gerekiyor. [Ayrıntılar DataList öğreticisi ile bir madde Işaretli ana kayıt listesi kullanan ana/ayrıntı](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) bölümünde gördüğünüz gibi, `CommandName` özelliğine ayarlanmış bir düğme, LinkButton veya ImageButton, Repeater veya DataList içinden tıklandığı zaman yineleyici veya datalist s `ItemCommand` olayı tetiklenir. DataList için `CommandName` özelliği belirli bir değere ayarlanmışsa, ek bir olay da oluşturulabilir. Özel `CommandName` özellik değerleri, diğerleri arasında şunları içerir:

- İptal `CancelCommand` olayını başlatır
- Düzenle `EditCommand` olayını başlatır
- Güncelleştirme `UpdateCommand` olayını başlatır

`ItemCommand` olayına *ek* olarak bu olayların gerçekleştiğini aklınızda bulundurun.

`EditItemTemplate` iki düğme web denetimine ekleyin, biri `CommandName` Update olarak ayarlanır ve diğer s Iptal olarak ayarlanır. Bu iki düğme web denetimini ekledikten sonra tasarımcı şuna benzer görünmelidir:

[EditItemTemplate 'e ![güncelleştirme ve Iptal düğmeleri ekleme](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image25.png)

**Şekil 11**: `EditItemTemplate` güncelleştirme ve iptal düğmeleri ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image27.png))

`EditItemTemplate`, DataList 'in bildirim temelli biçimlendirmesinin, aşağıdaki gibi görünmelidir:

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>5\. Adım: düzenleme moduna girerken sıhhi tesisat ekleme

Bu noktada, DataList 'umuz `EditItemTemplate`aracılığıyla tanımlanan bir Editing arabirimine sahiptir; Ancak, şu anda bir kullanıcının bir ürün bilgilerini düzenlemek istediğini göstermek için sayfamızı ziyaret eden bir yolu yoktur. Tıklandığında, bu DataList öğesini düzenleme modunda işleyen her ürüne bir düzenleme düğmesi eklememiz gerekir. Tasarımcı ya da bildirimli olarak `ItemTemplate`bir düzenleme düğmesi ekleyerek başlayın. Düzenle düğmesi s `CommandName` özelliğini Düzenle olarak ayarlamaya emin olun.

Bu düzenleme düğmesini ekledikten sonra sayfayı bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Bu ek olarak, her ürün listesinin bir düzenleme düğmesi içermesi gerekir.

[EditItemTemplate 'e ![güncelleştirme ve Iptal düğmeleri ekleme](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image28.png)

**Şekil 12**: `EditItemTemplate` güncelleştirme ve iptal düğmeleri ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image30.png))

Düğmeye tıklamak geri göndermeye neden olur, ancak ürün listesini düzenleme *moduna almaz.* Ürünü düzenlenebilir hale getirmek için şunları yapmanız gerekir:

1. DataList s [`EditItemIndex` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) , düzenleme düğmesine tıklamış olan `DataListItem` dizini olarak ayarlayın.
2. Verileri DataList 'e yeniden bağlayın. DataList yeniden işlendiğinde, `ItemIndex` DataList s `EditItemIndex` 'e karşılık gelen `DataListItem` `EditItemTemplate`kullanılarak işlenir.

Düzenle düğmesine tıklandığında DataList s `EditCommand` olayı tetiklendiğinden, aşağıdaki kodla bir `EditCommand` olay işleyicisi oluşturun:

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample4.cs)]

`EditCommand` olay işleyicisi, düzenleme düğmesine tıklamış olan `DataListItem` bir başvuru içeren ikinci giriş parametresi olarak `DataListCommandEventArgs` türünde bir nesneye geçirilir (`e.Item`). Olay işleyicisi önce DataList s `EditItemIndex` düzenlenebilir `DataListItem` `ItemIndex` ayarlar ve DataList s `DataBind()` yöntemini çağırarak verileri DataList 'e yeniden bağlar.

Bu olay işleyicisini ekledikten sonra sayfayı bir tarayıcıda yeniden ziyaret edin. Düzenle düğmesine tıkladığınızda, tıklanan ürün düzenlenebilir hale gelir (bkz. Şekil 13).

[Düzenle düğmesine tıklamak ![, ürünü düzenlenebilir hale getirir](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image31.png)

**Şekil 13**: Düzenle düğmesine tıkladığınızda ürün düzenlenebilir hale gelir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image33.png))

## <a name="step-6-saving-the-user-s-changes"></a>6\. Adım: Kullanıcı değişikliklerini kaydetme

Düzenlenen ürün s Update veya Cancel düğmelerine tıklanması bu noktada hiçbir şey yapmaz; Bu işlevi eklemek için, DataList s `UpdateCommand` ve `CancelCommand` olayları için olay işleyicileri oluşturmanız gerekir. Düzenlenen ürün s Iptal düğmesine tıklandığı ve DataList 'i düzenleme öncesi durumuna döndürmeye çalışırken yürütülecek `CancelCommand` olay işleyicisini oluşturarak başlayın.

DataList 'in tüm öğelerini salt okuma modunda işlemesini sağlamak için şunları yapmanız gerekir:

1. DataList s [`EditItemIndex` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) var olmayan bir `DataListItem` dizininin dizinine ayarlayın. `DataListItem` dizinler `0`başladığından `-1` güvenli bir seçenektir.
2. Verileri DataList 'e yeniden bağlayın. `DataListItem` `ItemIndex` es, DataList s `EditItemIndex`'ye karşılık geldiğinden, DataList 'in tamamı salt okunurdur modda işlenir.

Bu adımlar aşağıdaki olay işleyici kodu ile gerçekleştirilebilir:

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample5.cs)]

Bu ek olarak, Iptal düğmesine tıklamak DataList 'i önceden düzenlenen durumuna döndürür.

Tamamlamamız gereken son olay işleyicisi `UpdateCommand` olay işleyicisidir. Bu olay işleyicisinin şunları yapması gerekir:

1. Kullanıcı tarafından girilen ürün adına ve fiyatına ve düzenlenmiş `ProductID`düzenlenen ürüne programlı bir şekilde erişin.
2. `ProductsBLL` sınıfında uygun `UpdateProduct` aşırı yüklemeyi çağırarak güncelleştirme işlemini başlatın.
3. DataList s [`EditItemIndex` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) var olmayan bir `DataListItem` dizininin dizinine ayarlayın. `DataListItem` dizinler `0`başladığından `-1` güvenli bir seçenektir.
4. Verileri DataList 'e yeniden bağlayın. `DataListItem` `ItemIndex` es, DataList s `EditItemIndex`'ye karşılık geldiğinden, DataList 'in tamamı salt okunurdur modda işlenir.

1 ve 2. adım, Kullanıcı değişikliklerinin kaydedilmesinden sorumludur; 3 ve 4. adımlar, değişiklikler kaydedildikten ve `CancelCommand` olay işleyicisinde gerçekleştirilen adımlarla aynı olduktan sonra DataList 'i önceden düzenlenen durumuna döndürür.

Güncelleştirilmiş ürün adını ve fiyatını almak için, `EditItemTemplate`içindeki TextBox Web denetimlerine programlı bir şekilde başvurmak üzere `FindControl` yöntemini kullanmanız gerekir. Ayrıca, düzenlenmiş ürün s `ProductID` değerini de edinmemiz gerekir. İlk olarak, ObjectDataSource 'u DataList 'e bağladığımızda, Visual Studio DataList s `DataKeyField` özelliğini veri kaynağından (`ProductID`) birincil anahtar değerine atamıştır. Bu değer daha sonra DataList s `DataKeys` koleksiyonundan elde edilebilir. `DataKeyField` özelliğinin gerçekten `ProductID`olarak ayarlandığından emin olmak için bir dakikanızı ayırın.

Aşağıdaki kod dört adımı uygular:

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample6.cs)]

Olay işleyicisi, düzenlenmiş ürün s `ProductID` `DataKeys` koleksiyonundan okunarak başlar. Sonra, `EditItemTemplate` iki metin kutusunda başvurulur ve `Text` özellikleri yerel değişkenlerde, `productNameValue` ve `unitPriceValue`depolanır. Girilen değerin bir para birimi simgesi varsa, yine de bir `Decimal` değere dönüştürülebilmesi için `UnitPrice` metin kutusundan değeri okumak üzere `Decimal.Parse()` yöntemini kullanırız.

> [!NOTE]
> `ProductName` ve `UnitPrice` metin kutularının değerleri yalnızca, metin kutuları metin özelliklerinde belirtilen bir değer varsa, productNameValue ve unitPriceValue değişkenlerine atanır. Aksi takdirde, bir veritabanı `NULL` değeri ile verileri güncelleştirme etkisi olan değişkenler için `Nothing` değeri kullanılır. Diğer bir deyişle, kodumuz boş dizeleri, GridView, DetailsView ve FormView denetimlerinde bulunan Editing arabiriminin varsayılan davranışı olan veritabanı `NULL` değerlerine dönüştürür.

Değerleri okuduktan sonra, `ProductsBLL` sınıf s `UpdateProduct` yöntemi, ürün adı, Fiyat ve `ProductID`geçirerek çağrılır. Olay işleyicisi, `CancelCommand` olay işleyicisindeki ile tam olarak aynı mantığı kullanarak DataList 'i önceden düzenlenen durumuna döndürerek tamamlanır.

`EditCommand`, `CancelCommand`ve `UpdateCommand` olay işleyicileri tamamlanmalı bir ziyaretçi bir ürünün adını ve fiyatını düzenleyebilir. Şekil 14-16 Bu Düzenle iş akışını işlem içinde göster.

[Sayfayı Ilk ziyaret edildiğinde ![, tüm ürünler salt okunurdur modunda](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image34.png)

**Şekil 14**: sayfayı ilk ziyaret edildiğinde, tüm ürünler salt okunurdur ve ([tam boyutlu görüntüyü görüntülemek için tıklatın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image36.png))

[Ürün adı veya fiyatını güncelleştirmek ![Düzenle düğmesine tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image37.png)

**Şekil 15**: ürün adı veya fiyatını güncelleştirmek Için Düzenle düğmesine tıklayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image39.png))

[Değeri değiştirdikten sonra ![, salt okunurdur moduna dönmek için Güncelleştir 'e tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image40.png)

**Şekil 16**: değeri değiştirdikten sonra, salt okuma moduna geri dönmek Için Güncelleştir ' e tıklayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image42.png))

## <a name="step-7-adding-delete-capabilities"></a>7\. Adım: silme özelliklerini ekleme

Bir DataList 'e silme özellikleri ekleme adımları, düzen özellikleri eklemeye yönelik olanlarla benzerdir. Kısacası, tıklandığında `ItemTemplate` bir Delete düğmesi eklememiz gerekir:

1. İlgili ürün s `ProductID` `DataKeys` koleksiyonu aracılığıyla okur.
2. `ProductsBLL` sınıf s `DeleteProduct` metodunu çağırarak silme işlemini gerçekleştirir.
3. Verileri DataList 'e yeniden bağlar.

`ItemTemplate`bir Delete düğmesi ekleyerek başlayalım.

Tıklandığı zaman, `CommandName` düzenleme, güncelleştirme veya Iptal eden bir düğme, DataList s `ItemCommand` olayını ek bir olayla birlikte (örneğin, düzenleme `EditCommand` olayını kullanırken) oluşturur. Benzer şekilde, DataList 'teki `CommandName` özelliği Delete olarak ayarlanan herhangi bir Button, LinkButton veya ImageButton, `DeleteCommand` olayının tetiklenmesine neden olur (`ItemCommand`ile birlikte).

`ItemTemplate`Düzenle düğmesinin yanına, `CommandName` özelliğini Delete olarak ayarlayarak bir Sil düğmesi ekleyin. Bu düğme eklendikten sonra, DataList s `ItemTemplate` bildirim temelli söz dizimi şöyle görünmelidir:

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample7.aspx)]

Ardından, aşağıdaki kodu kullanarak DataList s `DeleteCommand` olayı için bir olay işleyicisi oluşturun:

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample8.cs)]

Sil düğmesine tıklamak geri göndermeye neden olur ve DataList `DeleteCommand` olayını tetikler. Olay işleyicisinde, tıklanan ürün s `ProductID` değerine `DataKeys` koleksiyonundan erişilir. Ardından ürün, `ProductsBLL` Class s `DeleteProduct` yöntemi çağırarak silinir.

Ürünü sildikten sonra, verileri DataList 'e (`DataList1.DataBind()`) yeniden bağlamanız önemlidir, aksi takdirde DataList, yeni silinen ürünü göstermeye devam eder.

## <a name="summary"></a>Özet

DataList, nokta içermiyorsa ve Düzenle ' ye tıklayın ve GridView tarafından desteklenen destek ve silme ' ye tıklayıp, kısa bir kod ile bu özellikleri kapsayacak şekilde geliştirilebilir. Bu öğreticide, silinebilecek ve adı ve fiyatı düzenlenebilen ürünlerin iki sütunlu bir listesini nasıl oluşturacağınız gördük. Düzen ve silme desteği eklemek, `ItemTemplate` ve `EditItemTemplate`uygun Web denetimlerinin yanı sıra ilgili olay işleyicilerini oluşturmak, Kullanıcı tarafından girilen ve birincil anahtar değerlerini okumak ve Iş mantığı katmanı ile arabirim oluşturulması.

DataList 'e temel düzen ve silme özellikleri ekledik, ancak gelişmiş özelliklerden daha fazla yer yoktur. Örneğin, bir giriş alanı doğrulaması yok-bir Kullanıcı çok pahalı bir fiyat girerse, bir `Decimal`çok pahalı hale dönüştürmeye çalışırken `Decimal.Parse` bir özel durum oluşturulur. Benzer şekilde, Iş mantığındaki veya veri erişim katmanlarındaki verileri güncelleştirmede bir sorun varsa, kullanıcıya standart hata ekranı sunulacaktır. Silme düğmesinde hiçbir onay sıralaması olmadan, yanlışlıkla bir ürünü silmek çok olasıdır.

Gelecek öğreticilerde, Kullanıcı deneyimini düzenlemekle nasıl geliştireceğiniz hakkında bilgi edineceksiniz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticiye ilişkin müşteri adayı gözden geçirenler Zack Jones, Ken peşin PISA ve Randy SCHMIDT olarak değiştirildi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](performing-batch-updates-cs.md)
