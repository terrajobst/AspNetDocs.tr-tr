---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: Veri bağlantılı denetimler | Microsoft Docs
author: microsoft
description: Çoğu ASP.NET uygulaması, bir arka uç veri kaynağından bir ölçüde veri sunumuna güvenir. Veri bağlantılı denetimler, etkileşime geçen w 'ın bir parçası...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: 1154b38e0fa3d9d56cb407ae659c3b0d69871fda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603840"
---
# <a name="data-bound-controls"></a>Veri Sınırı Denetimleri

[Microsoft](https://github.com/microsoft) tarafından

> Çoğu ASP.NET uygulaması, bir arka uç veri kaynağından bir ölçüde veri sunumuna güvenir. Veri bağlantılı denetimler, dinamik Web uygulamalarında verilerle etkileşim kurmanın bir parçasıdır. ASP.NET 2,0, yeni bir BaseDataBoundControl sınıfı ve bildirim temelli sözdizimi dahil olmak üzere veri bağlantılı denetimlerde bazı önemli geliştirmeler sunar.

Çoğu ASP.NET uygulaması, bir arka uç veri kaynağından bir ölçüde veri sunumuna güvenir. Veri bağlantılı denetimler, dinamik Web uygulamalarında verilerle etkileşim kurmanın bir parçasıdır. ASP.NET 2,0, yeni bir BaseDataBoundControl sınıfı ve bildirim temelli sözdizimi dahil olmak üzere veri bağlantılı denetimlerde bazı önemli geliştirmeler sunar.

BaseDataBoundControl, DataBoundControl sınıfı ve HierarchicalDataBoundControl sınıfı için temel sınıf olarak davranır. Bu modülde, DataBoundControl öğesinden türetilen aşağıdaki sınıfları tartışacağız:

- AdRotator
- Liste denetimleri
- GridView
- FormView
- Işlenmemiş

Ayrıca, HierarchicalDataBoundControl sınıfından türetilen aşağıdaki sınıflar da tartışılıyoruz:

- TreeView
- Menü
- SiteMapPath

## <a name="databoundcontrol-class"></a>DataBoundControl sınıfı

DataBoundControl sınıfı, tablo veya liste stili verilerle etkileşim kurmak için kullanılan soyut bir sınıftır (VB 'de MustInherit olarak işaretlenir). Aşağıdaki denetimler DataBoundControl öğesinden türeyen bazı denetimlerdir.

## <a name="adrotator"></a>AdRotator

AdRotator denetimi, bir grafik başlığını belirli bir URL 'ye bağlı bir Web sayfasında görüntülemenize olanak sağlar. Görüntülenen grafik, denetimin özellikleri kullanılarak döndürülür. Bir sayfada belirli bir ad görüntüleme sıklığı, **Impressions** özelliği kullanılarak yapılandırılabilir ve reklamlar anahtar sözcük filtrelemesi kullanılarak filtrelenebilir.

AdRotator denetimleri, veri için bir XML dosyası ya da bir veritabanında tablo kullanır. Aşağıdaki öznitelikler, XML dosyalarında, AdRotator denetimini yapılandırmak için kullanılır.

### <a name="imageurl"></a>ImageUrl
Ad için görüntülenecek görüntünün URL 'SI.

### <a name="navigateurl"></a>NavigateUrl
Ad tıklandığında kullanıcının alınması gereken URL. Bu URL kodlamalı olmalıdır.

### <a name="alternatetext"></a>AlternateText
Araç ipucunda görüntülenen ve ekran okuyucular tarafından okunan alternatif metin. Ayrıca, ImageUrl tarafından belirtilen görüntü kullanılabilir olmadığında da görüntülenir.

### <a name="keyword"></a>Anahtar sözcüğü
Anahtar sözcük filtrelemesi kullanılırken kullanılabilecek bir anahtar sözcük tanımlar. Belirtilmişse, yalnızca anahtar sözcük filtresiyle eşleşen bir anahtar sözcüğü olan reklamlar görüntülenir.

### <a name="impressions"></a>İzlenimler
Belirli bir reklamı ne sıklıkta belirebilir belirleyen bir ağırlık numarası. Aynı dosyadaki diğer reklamların izlenimine göre belirlenir. Bir XML dosyasındaki tüm reklamlar için en büyük toplu değer sayısı 2.048.000.000 1 ' dir.

### <a name="height"></a>Yükseklik
Ad 'nin piksel cinsinden yüksekliği.

### <a name="width"></a>Genişlik
Ad 'nin piksel cinsinden genişliği.

> [!NOTE]
> Height ve Width öznitelikleri, AdRotator denetiminin kendisinin yüksekliğini ve genişliğini geçersiz kılar.

Tipik bir XML dosyası aşağıdaki gibi görünebilir:

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

Yukarıdaki örnekte, Contoso için ad, Impressions özniteliğinin değeri nedeniyle ASP.NET Web sitesi için ad olarak görünmeme olasılığı yüksektir.

Yukarıdaki XML dosyasındaki reklamları göstermek için, bir sayfaya bir AdRotator denetimi ekleyin ve **AdvertisementFile** özelliğini aşağıda GÖSTERILDIĞI gibi XML dosyasına işaret etmek üzere ayarlayın:

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

Bir veritabanı tablosunu AdRotator denetiminizin veri kaynağı olarak kullanmayı seçerseniz, önce aşağıdaki şemayı kullanarak bir veritabanı ayarlamanız gerekir:

| **Sütun adı** | **Veri türü** | **Açıklama** |
| --- | --- | --- |
| Kimlik | int | Birincil anahtar. Bu sütun herhangi bir ada sahip olabilir. |
| ImageUrl | nvarchar (*uzunluk*) | Ad için görüntülenecek görüntünün göreli veya mutlak URL 'SI. |
| NavigateUrl | nvarchar (*uzunluk*) | Ad için hedef URL. Bir değer sağlamazsanız, ad bir köprü değildir. |
| AlternateText | nvarchar (*uzunluk*) | Görüntü bulunamazsa görüntülenecek metin. Bazı tarayıcılarda metin bir araç Ipucu olarak görüntülenir. Alternatif metin Ayrıca, grafiği görmemesi gereken kullanıcıların açıklamasını sesli okuyabilmesini sağlamak için erişilebilirlik için de kullanılır. |
| Anahtar sözcüğü | nvarchar (*uzunluk*) | Sayfanın filtreleyebileceği ad için bir kategori. |
| İzlenimler | int (4) | Ad 'nin ne sıklıkta görüntülendiğini gösteren bir sayı. Sayı ne kadar büyükse ad görüntülenir. XML dosyasındaki tüm Impressions değerlerinin toplamı 2.048.000.000-1 ' i aşamaz. |
| Genişlik | int (4) | Resmin piksel cinsinden genişliği. |
| Yükseklik | int (4) | Resmin piksel cinsinden yüksekliği. |

Zaten farklı bir şemaya sahip bir veritabanınız varsa, bu,, AdRotator özniteliklerini mevcut veritabanınıza eşlemek için **AlternateTextField**, **ImageUrlField**ve **NavigateUrlField** özelliklerini kullanabilirsiniz. AdRotator denetimindeki verileri veritabanından göstermek için, sayfaya bir veri kaynağı denetimi ekleyin, veri kaynağı denetimi için bağlantı dizesini veritabanınıza işaret edin ve AdRotator denetiminin **DataSourceID** özelliğini veri kaynağı denetiminin kimliğine ayarlayın. AdRotator reklamları programlı bir şekilde yapılandırmanız gereken durumlarda, AdCreated olayını kullanın. AdCreated olayı iki parametre alır; bir nesne ve diğer AdCreatedEventArgs örneği. AdCreatedEventArgs, oluşturulmakta olan ad için bir başvurudur.

Aşağıdaki kod parçacığı, bir ad için program aracılığıyla ImageUrl, NavigateUrl ve AlternateText değerlerini ayarlar:

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>Liste denetimleri

Liste denetimleri ListBox, DropDownList, CheckBoxList, RadioButtonList ve BulletedList ' i içerir. Bu denetimlerin her biri, veri kaynağına veri bağlanabilir. Veri kaynağında görüntülenen metin olarak bir alan kullanırlar ve isteğe bağlı olarak bir öğenin değeri olarak ikinci bir alanı kullanabilir. Öğeler tasarım zamanında statik olarak da eklenebilir ve bir veri kaynağından eklenen statik öğeleri ve dinamik öğeleri karıştırabilirsiniz.

Bir liste denetimini veri bağlamak için sayfaya bir veri kaynağı denetimi ekleyin. Veri kaynağı denetimi için bir seçme komutu belirtin ve sonra liste denetiminin DataSourceID özelliğini veri kaynağı denetiminin KIMLIĞINE ayarlayın. Görüntüleme metnini ve denetimin değerini tanımlamak için **DataTextField** ve **DataValueField** özelliklerini kullanın. Ayrıca, aşağıdaki gibi, görüntüleme metninin görünümünü denetlemek için **DataTextFormatString** özelliğini de kullanabilirsiniz:

| **İfadesini** | **Açıklama** |
| --- | --- |
| Fiyat: {0:C} | Sayısal/ondalık veriler için. "Price:" sabit değerini ve ardından sayıları para birimi biçiminde görüntüler. Para birimi biçimi, **sayfa** yönergesinde veya Web. config dosyasında kültür özniteliğinde belirtilen kültür ayarına bağlıdır. |
| {0:D4} | Tamsayı verileri için. Ondalık sayılarla kullanılamaz. Tamsayılar dört karakter genişliğinde sıfır doldurulmuş bir alanda görüntülenir. |
| {0:N2}% | Sayısal veriler için. Sayıyı, 2 ondalık basamak duyarlıklı ve ardından "%" değişmez değeri ile görüntüler. |
| {0:000.0} | Sayısal/ondalık veriler için. Sayılar bir ondalık basamağa yuvarlanır. Üç sayıdan küçük sayılar sıfır dolduruldu. |
| {0:D} | Tarih/saat verileri için. Uzun tarih biçimini ("Perşembe, Ağustos 06, 1996") görüntüler. Tarih biçimi sayfanın veya Web. config dosyasının kültür ayarına bağlıdır. |
| {0:d} | Tarih/saat verileri için. Kısa tarih biçimini ("12/31/99") görüntüler. |
| {0: yy-aa-gg} | Tarih/saat verileri için. Tarihi sayısal yıl-gün biçiminde görüntüler (96-08-06) |

## <a name="gridview"></a>GridView

GridView denetimi, tablo verilerinde bir bildirime dayalı yaklaşım kullanarak görüntüleme ve düzenlemenin yanı sıra DataGrid denetiminin ardıdır. Aşağıdaki özellikler GridView denetiminde mevcuttur.

- SqlDataSource gibi veri kaynağı denetimlerine bağlama.
- Yerleşik sıralama özellikleri.
- Yerleşik güncelleştirme ve silme özellikleri.
- Yerleşik sayfalama özellikleri.
- Yerleşik satır seçme özellikleri.
- Özellikleri dinamik olarak ayarlamak, olayları işlemek vb. için GridView nesne modeline programlı erişim.
- Birden çok anahtar alanı.
- Köprü sütunları için birden çok veri alanı.
- Temalar ve stiller aracılığıyla özelleştirilebilir görünüm.

**Sütun alanları**

GridView denetimindeki her sütun bir DataControlField nesnesi tarafından temsil edilir. Varsayılan olarak, AutoGenerateColumns özelliği **true**olarak ayarlanır ve bu, veri kaynağındaki her alan Için bir AutoGeneratedField nesnesi oluşturur. Her alan daha sonra GridView denetimindeki bir sütun olarak işlenir ve her alanın veri kaynağında göründüğü sırayla oluşturulur. Ayrıca, **AutoGenerateColumns** özelliğini **false** olarak ayarlayıp kendi sütun alanı koleksiyonunuzu tanımlayarak **GridView** denetiminde hangi sütun alanlarının göründüğünü el ile denetleyebilirsiniz. Farklı sütun alanı türleri denetimdeki sütunların davranışını belirlenir.

Aşağıdaki tablo, kullanılabilecek farklı sütun alanı türlerini listeler.

| **Sütun alan türü** | **Açıklama** |
| --- | --- |
| BoundField | Bir veri kaynağındaki bir alanın değerini görüntüler. Bu, GridView denetiminin varsayılan sütun türüdür. |
| ButtonField | GridView denetimindeki her öğe için bir komut düğmesi görüntüler. Bu, Ekle veya Kaldır düğmesi gibi özel düğme denetimlerinin bir sütununu oluşturmanızı sağlar. |
| CheckBoxField | GridView denetimindeki her öğe için bir onay kutusu görüntüler. Bu sütun alanı türü genellikle Boole değeri olan alanları göstermek için kullanılır. |
| CommandField | Seçme, düzenlemenin veya silme işlemlerini gerçekleştirmek için önceden tanımlanmış komut düğmelerini görüntüler. |
| Hyperlinkalanı | Bir veri kaynağındaki bir alanın değerini köprü olarak görüntüler. Bu sütun alan türü, köprünün URL 'sine ikinci bir alan bağlamanıza olanak tanır. |
| ImageField | GridView denetimindeki her öğe için bir resim görüntüler. |
| TemplateField | GridView denetimindeki her öğe için, belirtilen şablona göre Kullanıcı tanımlı içeriği görüntüler. Bu sütun alanı türü, özel bir sütun alanı oluşturmanıza olanak sağlar. |

Bir sütun alanı koleksiyonunu bildirimli olarak tanımlamak için, önce GridView denetiminin açılış ve kapanış etiketleri arasında etiketleri **&gt;&lt;sütunları** açma ve kapatma ekleyin. Sonra, açma ve kapatma **&lt;sütunları** arasına dahil etmek istediğiniz sütun alanlarını listeleyin&gt;etiketleri. Belirtilen sütunlar, sütunlar koleksiyonuna listelenen sırayla eklenir. **Columns** koleksiyonu denetimdeki tüm sütun alanlarını depolar ve GridView denetimindeki Column alanlarını programlı bir şekilde yönetmenizi sağlar.

Açıkça tanımlanmış sütun alanları, otomatik olarak oluşturulan sütun alanlarıyla birlikte görüntülenebilir. Her ikisi de kullanıldığında, önce açıkça tanımlanmış sütun alanları işlenir ve ardından otomatik olarak oluşturulan sütun alanları izlenir.

## <a name="binding-to-data"></a>Verilere Bağlama

GridView denetimi bir veri kaynağı denetimine ( **SqlDataSource**, **ObjectDataSource**, vb. gibi) ve System. Collections. IEnumerable arabirimini (System. Data. DataView, System. Collections. ArrayList veya System. Collections. Hashtable gibi) uygulayan herhangi bir veri kaynağına bağlı olabilir. GridView denetimini uygun veri kaynağı türüne bağlamak için aşağıdaki yöntemlerden birini kullanın:

- Bir veri kaynağı denetimine bağlamak için, GridView denetiminin DataSourceID özelliğini veri kaynağı denetiminin ID değeri olarak ayarlayın. GridView denetimi otomatik olarak belirtilen veri kaynağı denetimine bağlanır ve sıralama, güncelleştirme, silme ve sayfalama işlevlerini gerçekleştirmek için veri kaynağı denetiminin olanaklarından yararlanabilir. Bu, verilere bağlanmak için tercih edilen yöntemdir.
- System. Collections. IEnumerable arabirimini uygulayan bir veri kaynağına bağlanmak için, programlama yoluyla GridView denetiminin DataSource özelliğini veri kaynağına ayarlayın ve ardından DataBind metodunu çağırın. Bu yöntemi kullanırken, GridView denetimi yerleşik sıralama, güncelleştirme, silme ve sayfalama işlevleri sağlamaz. Bu işlevselliği kendiniz sağlamanız gerekir.

## <a name="data-operations"></a>Veri İşlemleri

GridView denetimi, kullanıcının denetimdeki öğeleri sıralama, güncelleştirme, silme, seçme ve sayfa eklemesine izin veren birçok yerleşik özellik sağlar. GridView denetimi bir veri kaynağı denetimine bağlandığında, GridView denetimi veri kaynağı denetiminin olanaklarından yararlanabilir ve otomatik sıralama, güncelleme ve silme işlevlerini sağlayabilir.

> [!NOTE]
> GridView denetimi, diğer veri kaynağı türleriyle sıralama, güncelleştirme ve silme desteği sağlar; Ancak, bu işlemler için uygulamayla birlikte uygun bir olay işleyicisi sağlamanız gerekir.

Sıralama, kullanıcının GridView denetimindeki öğeleri sütunun başlığına tıklayarak belirli bir sütuna göre sıralamasını sağlar. Sıralamayı etkinleştirmek için, AllowSorting özelliğini **true**olarak ayarlayın.

Otomatik güncelleştirme, silme ve seçim işlevleri, bir **ButtonField** veya **TemplateField** sütun alanındaki bir düğme, sırasıyla "Düzenle", "Sil" ve "Seç" komut adı ile tıklandığında etkinleştirilir. AutoGenerateEditButton, AutoGenerateDeleteButton veya AutoGenerateSelectButton özelliği sırasıyla **true**olarak ayarlandıysa, GridView denetimi Edit, DELETE veya Select düğmesini kullanarak otomatik olarak bir **CommandField** sütun alanı ekleyebilir.

> [!NOTE]
> Veri kaynağına kayıt eklemek GridView denetimi tarafından doğrudan desteklenmez. Ancak, DetailsView veya FormView denetimiyle birlikte GridView denetimini kullanarak kayıt eklemek mümkündür.

Veri kaynağındaki tüm kayıtları aynı anda görüntülemek yerine, GridView denetimi kayıtları sayfalara kadar otomatik olarak bölebilir. Disk belleğini etkinleştirmek için AllowPaging özelliğini **true**olarak ayarlayın.

## <a name="customizing-the-user-interface"></a>Kullanıcı Arabirimini Özelleştirme

Denetimin farklı bölümlerinin stil özelliklerini ayarlayarak GridView denetiminin görünümünü özelleştirebilirsiniz. Aşağıdaki tabloda farklı stil özellikleri listelenmektedir.

| **Style özelliği** | **Açıklama** |
| --- | --- |
| AlternatingRowStyle | GridView denetimindeki alternatif veri satırları için stil ayarları. Bu özellik ayarlandığında, veri satırları RowStyle ayarları ve **AlternatingRowStyle** ayarları arasında dönüşümlü olarak görüntülenir. |
| Edıtrowstyle | GridView denetiminde düzenlenmekte olan satırın stil ayarları. |
| EmptyDataRowStyle | Veri kaynağı herhangi bir kayıt içermiyorsa GridView denetiminde görünen boş veri satırı için stil ayarları. |
| FooterStyle | GridView denetiminin altbilgi satırı için stil ayarları. |
| HeaderStyle | GridView denetiminin başlık satırı için stil ayarları. |
| PagerStyle | GridView denetiminin sayfalayıcı satırı için stil ayarları. |
| RowStyle | GridView denetimindeki veri satırları için stil ayarları. **AlternatingRowStyle** özelliği de ayarlandığında, veri satırları **RowStyle** ayarları ve **AlternatingRowStyle** ayarları arasında dönüşümlü olarak görüntülenir. |
| SelectedRowStyle | GridView denetimindeki seçili satır için stil ayarları. |

Ayrıca, denetimin farklı parçalarını gösterebilir veya gizleyebilirsiniz. Aşağıdaki tabloda, hangi parçaların gösterildiğini veya gizlendiğini denetleyen özellikler listelenmiştir.

| **Özellik** | **Açıklama** |
| --- | --- |
| ShowFooter | GridView denetiminin altbilgi bölümünü gösterir veya gizler. |
| ShowHeader | GridView denetiminin üstbilgi bölümünü gösterir veya gizler. |

### <a name="events"></a>Olaylar

GridView denetimi, programlama için kullanabileceğiniz çeşitli olaylar sağlar. Bu, bir olay meydana geldiğinde özel bir yordam çalıştırmanızı sağlar. Aşağıdaki tabloda, GridView denetimi tarafından desteklenen olaylar listelenmektedir.

| **Event** | **Açıklama** |
| --- | --- |
| PageIndexChanged | Sayfalayıcı düğmelerinden birine tıklandığında gerçekleşir, ancak GridView denetimi disk belleği işlemini işler. Bu olay genellikle Kullanıcı denetimdeki farklı bir sayfaya gittiğinde bir görev gerçekleştirmeniz gerektiğinde kullanılır. |
| PageIndexChanging | Sayfalayıcı düğmelerinden birine tıklandığında, ancak GridView denetimi disk belleği işlemini gerçekleştirmeden önce gerçekleşir. Bu olay genellikle sayfalama işlemini iptal etmek için kullanılır. |
| Rowcancelıngedit | Bir satırın Iptal düğmesine tıklandığında, ancak GridView denetimi düzenleme modundan çıktıktan sonra gerçekleşir. Bu olay genellikle iptal işlemini durdurmak için kullanılır. |
| RowCommand | GridView denetimindeki bir düğmeye tıklandığında gerçekleşir. Bu olay genellikle denetimde bir düğme tıklandığında bir görevi gerçekleştirmek için kullanılır. |
| RowCreated | GridView denetiminde yeni bir satır oluşturulduğunda gerçekleşir. Bu olay genellikle satır oluşturulduğu sırada bir satırın içeriğini değiştirmek için kullanılır. |
| Rowveriye bağlı | Veri satırı GridView denetimindeki veriye bağlandığında oluşur. Bu olay, genellikle satır veriye bağlandığında bir satırın içeriğini değiştirmek için kullanılır. |
| RowDeleted | Bir satırın Delete düğmesine tıklandığında, ancak GridView denetimi bu kaydı veri kaynağından sildiğinde gerçekleşir. Bu olay genellikle silme işleminin sonuçlarını denetlemek için kullanılır. |
| Rowsiliyor | Bir satırın Delete düğmesine tıklandığında, ancak GridView denetimi kaydı veri kaynağından sildiğinde gerçekleşir. Bu olay genellikle silme işlemini iptal etmek için kullanılır. |
| RowEditing | Bir satırın Edit düğmesine tıklandığında, ancak GridView denetimi düzenleme moduna girmeden önce gerçekleşir. Bu olay genellikle, düzen işlemini iptal etmek için kullanılır. |
| RowUpdated | Bir satırın Update düğmesine tıklandığında, ancak GridView denetimi satırı güncelleştirdikten sonra gerçekleşir. Bu olay genellikle güncelleştirme işleminin sonuçlarını denetlemek için kullanılır. |
| RowUpdating | Bir satırın Update düğmesine tıklandığında, ancak GridView denetimi satırı güncelleyen zaman gerçekleşir. Bu olay genellikle güncelleştirme işlemini iptal etmek için kullanılır. |
| SelectedIndexChanged olayını | Bir satırın Select düğmesine tıklandığında, ancak GridView denetimi Select işlemini işlediğinde gerçekleşir. Bu olay genellikle denetimde bir satır seçildikten sonra bir görevi gerçekleştirmek için kullanılır. |
| SelectedIndexChanging | Bir satırın Select düğmesine tıklandığında, ancak GridView denetimi Select işlemini işleymesinden önce oluşur. Bu olay genellikle seçim işlemini iptal etmek için kullanılır. |
| Sütununa | Bir sütunu sıralamak için köprünün tıklandığı, ancak GridView denetimi sıralama işlemini gerçekleştirdikten sonra gerçekleşir. Bu olay genellikle Kullanıcı bir sütunu sıralamak için bir köprüye tıkladıktan sonra bir görevi gerçekleştirmek için kullanılır. |
| Sıralama | Bir sütunu sıralamak için köprünün tıklandığı, ancak GridView denetimi sıralama işlemini gerçekleştirmeden önce gerçekleşir. Bu olay genellikle sıralama işlemini iptal etmek veya özel bir sıralama yordamı gerçekleştirmek için kullanılır. |

## <a name="formview"></a>FormView

FormView denetimi bir veri kaynağından tek bir kaydı göstermek için kullanılır. Bu, DetailsView denetimine benzer, ancak satır alanları yerine Kullanıcı tanımlı şablonları görüntüler. Kendi şablonlarınızın oluşturulması, verilerin nasıl görüntülendiğini denetleme konusunda daha fazla esneklik sağlar. FormView denetimi aşağıdaki özellikleri destekler:

- SqlDataSource ve ObjectDataSource gibi veri kaynağı denetimlerine bağlama.
- Yerleşik ekleme özellikleri.
- Yerleşik güncelleştirme ve silme özellikleri.
- Yerleşik sayfalama özellikleri.
- Özellikleri dinamik olarak ayarlamak, olayları işlemek vb. için FormView nesne modeline programlı erişim.
- Kullanıcı tanımlı şablonlar, Temalar ve stiller aracılığıyla özelleştirilebilir görünüm.

## <a name="templates"></a>Şablonlar

FormView denetiminin içeriği görüntülemesi için, denetimin farklı parçaları için şablon oluşturmanız gerekir. Çoğu şablon isteğe bağlıdır; Ancak, denetimin yapılandırıldığı mod için bir şablon oluşturmanız gerekir. Örneğin, kayıt eklemeyi destekleyen bir FormView denetiminin tanımlanmış bir ekleme öğesi şablonu olması gerekir. Aşağıdaki tabloda, oluşturabileceğiniz farklı şablonlar listelenmektedir.

| **Şablon türü** | **Açıklama** |
| --- | --- |
| EditItemTemplate | FormView denetimi düzenleme modundayken veri satırı içeriğini tanımlar. Bu şablon genellikle kullanıcının var olan bir kaydı düzenleyebileceği giriş denetimlerini ve komut düğmelerini içerir. |
| EmptyDataTemplate 'i | FormView denetimi herhangi bir kayıt içermeyen bir veri kaynağına bağlandığında görüntülenen boş veri satırı içeriğini tanımlar. Bu şablon genellikle kullanıcıya veri kaynağının hiçbir kayıt içermediğini bildiren içerikleri içerir. |
| FooterTemplate | Alt bilgi satırının içeriğini tanımlar. Bu şablon genellikle altbilgi satırında görüntülenmesini istediğiniz ek içerikleri içerir. Alternatif olarak, FooterText özelliğini ayarlayarak altbilgi satırında görüntülenecek metni de belirtebilirsiniz. |
| HeaderTemplate | Üst bilgi satırı için içeriği tanımlar. Bu şablon genellikle başlık satırında görüntülenmesini istediğiniz ek içerikleri içerir. Alternatif olarak, HeaderText özelliğini ayarlayarak başlık satırında görüntülenecek metni de belirtebilirsiniz. |
| Template | FormView denetimi salt okuma modundayken veri satırı içeriğini tanımlar. Bu şablon genellikle varolan bir kaydın değerlerini görüntüleyen içerikleri içerir. |
| InsertItemTemplate | FormView denetimi ekleme modundayken veri satırı içeriğini tanımlar. Bu şablon genellikle kullanıcının yeni bir kayıt ekleyebileceği giriş denetimlerini ve komut düğmelerini içerir. |
| PagerTemplate | Sayfalama özelliği etkinleştirildiğinde (AllowPaging özelliği **true**olarak ayarlandığında) sayfalayıcı satırı içeriğini tanımlar. Bu şablon genellikle kullanıcının başka bir kayda gidebileceği denetimleri içerir. |

Öğe düzenleme şablonu ve ekleme öğesi şablonu içindeki giriş denetimleri, iki yönlü bağlama ifadesi kullanılarak bir veri kaynağının alanlarına bağlanabilir. Bu, FormView denetiminin, bir güncelleştirme veya ekleme işlemi için giriş denetiminin değerlerini otomatik olarak ayıklamasına olanak tanır. İki yönlü bağlama ifadeleri, özgün alan değerlerini otomatik olarak göstermek için bir düzenleme öğesi şablonundaki giriş denetimlerine de izin verir.

### <a name="binding-to-data"></a>Verilere Bağlama

FormView denetimi bir veri kaynağı denetimine ( **SqlDataSource**, AccessDataSource, **ObjectDataSource** vb. gibi) veya System. Collections. IEnumerable arabirimini (System. Data. DataView, System. Collections. ArrayList ve System. Collections. Hashtable gibi) uygulayan herhangi bir veri kaynağına bağlı olabilir. FormView denetimini uygun veri kaynağı türüne bağlamak için aşağıdaki yöntemlerden birini kullanın:

- Bir veri kaynağı denetimine bağlamak için, FormView denetiminin DataSourceID özelliğini veri kaynağı denetiminin ID değeri olarak ayarlayın. FormView denetimi otomatik olarak belirtilen veri kaynağı denetimine bağlanır ve ekleme, güncelleştirme, silme ve sayfalama işlevlerini gerçekleştirmek için veri kaynağı denetiminin olanaklarından yararlanabilir. Bu, verilere bağlanmak için tercih edilen yöntemdir.
- **System. Collections. IEnumerable** arabirimini uygulayan bir veri kaynağına bağlamak için, program aracılığıyla FormView denetiminin DataSource özelliğini veri kaynağına ayarlayın ve ardından DataBind metodunu çağırın. Bu yöntemi kullanırken, FormView denetimi yerleşik ekleme, güncelleştirme, silme ve sayfalama işlevleri sağlamaz. İlgili olayı kullanarak bu işlevi sağlamanız gerekir.

## <a name="data-operations"></a>Veri İşlemleri

FormView denetimi, kullanıcının denetimdeki öğeleri güncelleştirme, silme, ekleme ve sayfada yer değiştirmesine izin veren birçok yerleşik özellik sağlar. FormView denetimi bir veri kaynağı denetimine bağlandığında, FormView denetimi veri kaynağı denetiminin olanaklarından yararlanabilir ve otomatik güncelleştirme, silme, ekleme ve sayfalama işlevlerini sağlayabilir. FormView denetimi, diğer veri kaynakları türleriyle güncelleştirme, silme, ekleme ve sayfalama işlemleri için destek sağlar; Ancak, bu işlemler için uygulamayla birlikte uygun bir olay işleyicisi sağlamanız gerekir.

FormView denetimi şablonlar kullandığından, işlemleri güncelleştirme, silme veya ekleme işlemlerini gerçekleştirmek üzere otomatik olarak komut düğmeleri oluşturmak için bir yol sağlamaz. Bu komut düğmelerini uygun şablona el ile eklemeniz gerekir. FormView denetimi, **CommandName** özelliklerinin belirli değerler olarak ayarlandığı belirli düğmeleri tanır. Aşağıdaki tabloda, FormView denetiminin tanıdığı komut düğmeleri listelenmektedir.

| **Düğme** | **CommandName değeri** | **Açıklama** |
| --- | --- | --- |
| İptal | Tıklatın | İşlemi iptal etmek ve Kullanıcı tarafından girilen değerleri atmak için işlemleri güncelleştirmek veya eklemek için kullanılır. FormView denetimi daha sonra DefaultMode özelliği tarafından belirtilen moda geri döner. |
| Sil | Silmeli | Veri kaynağından görüntülenmiş kaydı silmek için silme işlemlerinde kullanılır. ItemDeleted ve ItemDeleted olaylarını yükseltir. |
| Düzenle | Düzenle | FormView denetimini düzenleme moduna almak için işlemleri güncelleştirmek üzere kullanılır. **EditItemTemplate** özelliğinde belirtilen içerik veri satırı için görüntülenir. |
| Ekleme | Ekleyin | Kullanıcı tarafından belirtilen değerleri kullanarak veri kaynağına yeni bir kayıt eklemeye çalışacak işlemler ekleme işlemi sırasında kullanılır. , En mini ve bağımsız olayları yükseltir. |
| Yeni | Yeni | FormView denetimini Insert modunda yerleştirmek için ekleme işlemleri sırasında kullanılır. **InsertItemTemplate** özelliğinde belirtilen içerik veri satırı için görüntülenir. |
| Sayfasında | Sayfasında | Sayfalama işlemlerinde, disk belleği çalıştıran sayfalayıcı satırındaki bir düğmeyi temsil etmek için kullanılır. Sayfalama işlemini belirtmek için düğmenin **CommandArgument** özelliğini "ileri", "önceki", "First", "Last" veya gidilecek sayfanın dizini olarak ayarlayın. PageIndexChanging ve PageIndexChanged olaylarını yükseltir. |
| Güncelleştirme | Update | Veri kaynağındaki görüntülenmiş kaydı kullanıcı tarafından belirtilen değerlerle güncelleştirmeyi denemek için işlemleri güncelleştirmek üzere kullanılır. ItemUpdating ve ItemUpdated olaylarını yükseltir. |

Sil düğmesinden farklı olarak (görüntülenmiş kaydı hemen siler), Düzenle veya yeni düğme tıklandığında, FormView denetimi sırasıyla düzenleme veya ekleme moduna geçer. Düzenleme modunda, geçerli veri öğesi için **EditItemTemplate** özelliğinde bulunan içerik görüntülenir. Genellikle düzenleme öğesi şablonu, Düzenle düğmesi bir güncelleştirmeyle ve Iptal düğmesiyle değiştirilmeleri için tanımlanır. Alanın veri türü (TextBox veya CheckBox denetimi gibi) için uygun olan giriş denetimleri, genellikle kullanıcının değiştiremeyeceği bir alanın değeri ile birlikte görüntülenir. Güncelleştir düğmesine tıkladığınızda, veri kaynağındaki kayıt güncelleştirilir, ancak Iptal düğmesine tıkladığınızda herhangi bir değişiklik yapılır.

Benzer şekilde, **InsertItemTemplate** özelliğinde bulunan içerik, denetim ekleme modundayken veri öğesi için görüntülenir. Ekleme öğesi şablonu, genellikle yeni düğmenin bir INSERT ve Cancel düğmesiyle değiştirildiği ve Kullanıcı için yeni kayıt değerlerini girmesi için boş giriş denetimlerinin görüntülendiği şekilde tanımlanır. Ekle düğmesine tıklamak, kaydı veri kaynağına ekler, ancak Iptal düğmesine tıkladığınızda herhangi bir değişiklik yapılır.

FormView denetimi, kullanıcının veri kaynağındaki diğer kayıtlara gitmesini sağlayan bir sayfalama özelliği sağlar. Etkinleştirildiğinde, bir sayfalayıcı satırı, sayfa gezintisi denetimlerini içeren FormView denetiminde görüntülenir. Disk belleğini etkinleştirmek için **AllowPaging** özelliğini **true**olarak ayarlayın. Sayfa stili ve PagerSettings özelliğinde yer alan nesnelerin özelliklerini ayarlayarak sayfalayıcı satırını özelleştirebilirsiniz. Yerleşik sayfalayıcı satırı Kullanıcı arabirimini kullanmak yerine, **PagerTemplate** özelliğini kullanarak kendi Kullanıcı arabiriminizi oluşturabilirsiniz.

## <a name="customizing-the-user-interface"></a>Kullanıcı Arabirimini Özelleştirme

Denetimin farklı bölümlerinin stil özelliklerini ayarlayarak FormView denetiminin görünümünü özelleştirebilirsiniz. Aşağıdaki tabloda farklı stil özellikleri listelenmektedir.

| **Style özelliği** | **Açıklama** |
| --- | --- |
| Edıtrowstyle | FormView denetimi düzenleme modunda olduğunda veri satırı için stil ayarları. |
| EmptyDataRowStyle | Veri kaynağı herhangi bir kayıt içermiyorsa FormView denetiminde görünen boş veri satırı için stil ayarları. |
| FooterStyle | FormView denetiminin altbilgi satırı için stil ayarları. |
| HeaderStyle | FormView denetiminin üstbilgi satırı için stil ayarları. |
| InsertRowStyle | FormView denetimi ekleme modundayken veri satırı için stil ayarları. |
| PagerStyle | Sayfalama özelliği etkinken FormView denetiminde görünen sayfalayıcı satırı için stil ayarları. |
| RowStyle | FormView denetimi salt okuma modunda olduğunda veri satırı için stil ayarları. |

## <a name="events"></a>Olaylar

FormView denetimi, programlama için kullanabileceğiniz çeşitli olaylar sağlar. Bu, bir olay meydana geldiğinde özel bir yordam çalıştırmanızı sağlar. Aşağıdaki tabloda, FormView denetimi tarafından desteklenen olaylar listelenmektedir.

| **Event** | **Açıklama** |
| --- | --- |
| ItemCommand | FormView denetimi içindeki bir düğmeye tıklandığında gerçekleşir. Bu olay genellikle denetimde bir düğme tıklandığında bir görevi gerçekleştirmek için kullanılır. |
| ItemCreated | FormView denetiminde tüm FormViewRow nesneleri oluşturulduktan sonra gerçekleşir. Bu olay, genellikle bir kaydın görüntülenmeden önce değerlerini değiştirmek için kullanılır. |
| ItemDeleted | Bir Delete düğmesine ( **CommandName** özelliği "Delete" olarak ayarlanan bir düğmeye) tıklandığında gerçekleşir, ancak FormView denetimi veri kaynağından kaydı sildikten sonra. Bu olay genellikle silme işleminin sonuçlarını denetlemek için kullanılır. |
| Itemsiliyor | Bir Delete düğmesine tıklandığında, ancak FormView denetimi veri kaynağından kaydı silmeden önce oluşur. Bu olay genellikle silme işlemini iptal etmek için kullanılır. |
| Öğe yukarı | Bir INSERT düğmesine ( **CommandName** özelliği "INSERT" olarak ayarlanan bir düğmeye) tıklandığında gerçekleşir, ancak FormView denetimi kaydı ekledikten sonra. Bu olay genellikle ekleme işleminin sonuçlarını denetlemek için kullanılır. |
| Iteminyıting | Bir INSERT düğmesine tıklandığında, ancak FormView denetimi kaydı eklemeden oluşur. Bu olay genellikle ekleme işlemini iptal etmek için kullanılır. |
| ItemUpdated | Bir Update düğmesine ( **CommandName** özelliği "Update" olarak ayarlanmış bir düğmeye) tıklandığında, ancak FormView denetimi satırı güncelleştirdikten sonra gerçekleşir. Bu olay genellikle güncelleştirme işleminin sonuçlarını denetlemek için kullanılır. |
| ItemUpdating | Bir Update düğmesine tıklandığında, ancak FormView denetimi kaydı güncelleştirmediğinde gerçekleşir. Bu olay genellikle güncelleştirme işlemini iptal etmek için kullanılır. |
| ModeChanged | FormView denetimi modları değiştirdikten sonra oluşur (düzenleme, ekleme veya salt okuma modu için). Bu olay genellikle FormView denetimi modları değiştirdiğinde bir görevi gerçekleştirmek için kullanılır. |
| Modu değiştirme | FormView denetimi modları değiştirmeden önce oluşur (düzenleme, ekleme veya salt okuma modu için). Bu olay, genellikle bir mod değişikliğini iptal etmek için kullanılır. |
| PageIndexChanged | Sayfalayıcı düğmelerinden birine tıklandığında gerçekleşir, ancak FormView denetimi disk belleği işlemini işler. Bu olay genellikle Kullanıcı denetimdeki farklı bir kayda gittiğinde bir görev gerçekleştirmeniz gerektiğinde kullanılır. |
| PageIndexChanging | Sayfalayıcı düğmelerinden birine tıklandığında, ancak FormView denetimi disk belleği işlemini gerçekleştirmeden önce gerçekleşir. Bu olay genellikle sayfalama işlemini iptal etmek için kullanılır. |

## <a name="detailsview"></a>Işlenmemiş

DetailsView denetimi, tablodaki her alanın tablonun bir satırında görüntülendiği bir veri kaynağından tek bir kayıt göstermek için kullanılır. Ana ayrıntı senaryoları için bir GridView denetimiyle birlikte kullanılabilir. DetailsView denetimi aşağıdaki özellikleri destekler:

- SqlDataSource gibi veri kaynağı denetimlerine bağlama.
- Yerleşik ekleme özellikleri.
- Yerleşik güncelleştirme ve silme özellikleri.
- Yerleşik sayfalama özellikleri.
- Özellikleri dinamik olarak ayarlamak, olayları işlemek vb. için DetailsView nesne modeline programlı erişim.
- Temalar ve stiller aracılığıyla özelleştirilebilir görünüm.

## <a name="row-fields"></a>Satır Alanları

DetailsView denetimindeki her bir veri satırı, bir alan denetimi bildirerek oluşturulur. Farklı satır alanı türleri denetimdeki satırların davranışını belirrlar. Alan denetimleri DataControlField 'dan türetilir. Aşağıdaki tabloda, kullanılabilecek farklı satır alanı türleri listelenmektedir.

| **Sütun alan türü** | **Açıklama** |
| --- | --- |
| BoundField | Bir veri kaynağındaki bir alanın değerini metin olarak görüntüler. |
| ButtonField | DetailsView denetimindeki bir komut düğmesini görüntüler. Bu, Ekle veya Kaldır düğmesi gibi özel bir düğme denetimiyle bir satır görüntülemenizi sağlar. |
| CheckBoxField | DetailsView denetimindeki onay kutusunu görüntüler. Bu satır alanı türü genellikle Boole değeri olan alanları göstermek için kullanılır. |
| CommandField | DetailsView denetiminde düzenleme, ekleme veya silme işlemlerini gerçekleştirmek için yerleşik komut düğmelerini görüntüler. |
| Hyperlinkalanı | Bir veri kaynağındaki bir alanın değerini köprü olarak görüntüler. Bu satır alanı türü, köprünün URL 'sine ikinci bir alan bağlamanıza olanak tanır. |
| ImageField | DetailsView denetimindeki bir görüntüyü görüntüler. |
| TemplateField | DetailsView denetimindeki bir satır için, belirtilen şablona göre Kullanıcı tanımlı içeriği görüntüler. Bu satır alanı türü, özel bir satır alanı oluşturmanıza olanak sağlar. |

Varsayılan olarak, AutoGenerateRows özelliği **true**olarak ayarlanır, bu da veri kaynağındaki bağlanabilir türde her alan için otomatik olarak bir bağlantılı satır alanı üretir. Geçerli bağlanabilir türler dize, DateTime, Decimal, Guid ve temel türler kümesidir. Her alan daha sonra metin olarak bir satırda, her alanın veri kaynağında göründüğü sırada görüntülenir.

Satırları otomatik olarak oluşturmak, kayıttaki her alanı görüntülemenin hızlı ve kolay bir yolunu sağlar. Ancak, DetailsView denetiminin gelişmiş yeteneklerini kullanmak için, DetailsView denetimine dahil edilecek satır alanlarını açıkça bildirmeniz gerekir. Satır alanlarını bildirmek için, önce **AutoGenerateRows** özelliğini **false**olarak ayarlayın. Sonra, DetailsView denetiminin açılış ve kapanış etiketleri arasına etiketleri&gt;açma ve kapatma **&lt;alanları** ekleyin. Son olarak, açma ve kapatma **&lt;alanları&gt;** etiketleri arasına dahil etmek istediğiniz satır alanlarını listeleyin. Belirtilen satır alanları, alanlar koleksiyonuna listelenen sırayla eklenir. **Alanlar** koleksiyonu, DetailsView denetimindeki satır alanlarını programlı bir şekilde yönetmenizi sağlar.

> [!NOTE]
> Otomatik olarak oluşturulan satır alanları alanlar koleksiyonuna eklenmez.

## <a name="binding-to-data"></a>Verilere Bağlama

DetailsView denetimi, **SqlDataSource** veya AccessDataSource gibi bir veri kaynağı denetimine veya System. Data. DataView, System. Collections. ArrayList ve System. Collections. Hashtable gibi System. Collections. IEnumerable arabirimini uygulayan herhangi bir veri kaynağına bağlanabilir.

DetailsView denetimini uygun veri kaynağı türüne bağlamak için aşağıdaki yöntemlerden birini kullanın:

- Bir veri kaynağı denetimine bağlamak için, DetailsView denetiminin DataSourceID özelliğini veri kaynağı denetiminin ID değeri olarak ayarlayın. DetailsView denetimi, belirtilen veri kaynağı denetimine otomatik olarak bağlanır. Bu, verilere bağlanmak için tercih edilen yöntemdir.
- **System. Collections. IEnumerable** arabirimini uygulayan bir veri kaynağına bağlamak için, program aracılığıyla DetailsView denetiminin DataSource özelliğini veri kaynağına ayarlayın ve ardından DataBind metodunu çağırın.

## <a name="security"></a>Güvenlik

Bu denetim, kötü amaçlı istemci betiği içerebilecek Kullanıcı girişini göstermek için kullanılabilir. Uygulamanızda görüntülemeden önce yürütülebilir betik, SQL deyimleri veya diğer kod için bir istemciden gönderilen tüm bilgileri denetleyin. ASP.NET, Kullanıcı girişinde betiği ve HTML 'i engellemek için bir giriş isteği doğrulama özelliği sağlar.

## <a name="data-operations"></a>Veri İşlemleri

DetailsView denetimi, kullanıcının denetimdeki öğeleri güncelleştirme, silme, ekleme ve sayfada yer değiştirmesine izin veren yerleşik yetenekler sağlar. DetailsView denetimi bir veri kaynağı denetimine bağlandığında, DetailsView denetimi veri kaynağı denetiminin olanaklarından yararlanabilir ve otomatik güncelleştirme, silme, ekleme ve sayfalama işlevlerini sağlayabilir.

DetailsView denetimi, diğer veri kaynağı türleriyle güncelleştirme, silme, ekleme ve sayfalama işlemleri için destek sağlar; Ancak, bu işlemler için uygun bir olay işleyicisinde uygulama sağlamanız gerekir.

DetailsView denetimi, sırasıyla AutoGenerateEditButton, AutoGenerateDeleteButton veya AutoGenerateInsertButton özelliklerini **true**olarak ayarlayarak bir **CommandField** satır alanını düzenleme, silme veya yeni düğme ile otomatik olarak ekleyebilir. Sil düğmesinden farklı olarak (seçili kaydı hemen siler), Düzenle veya yeni düğme tıklandığında, DetailsView denetimi sırasıyla düzenleme veya ekleme moduna geçer. Düzenleme modunda Düzenle düğmesi bir güncelleştirmeyle ve Iptal düğmesiyle değiştirilmiştir. Alanın veri türü (TextBox veya CheckBox denetimi gibi) için uygun olan giriş denetimleri, kullanıcının değiştiremeyeceği bir alanın değeri ile görüntülenir. Güncelleştir düğmesine tıkladığınızda, veri kaynağındaki kayıt güncelleştirilir, ancak Iptal düğmesine tıkladığınızda herhangi bir değişiklik yapılır. Benzer şekilde, ekleme modunda yeni düğme bir INSERT ve Cancel düğmesi ile değiştirilmiştir ve kullanıcının yeni kayıt için değerleri girmesi için boş giriş denetimleri görüntülenir.

DetailsView denetimi, kullanıcının veri kaynağındaki diğer kayıtlara gitmesini sağlayan bir sayfalama özelliği sağlar. Etkinleştirildiğinde, sayfa gezintisi denetimleri sayfalayıcı satırında görüntülenir. Disk belleğini etkinleştirmek için AllowPaging özelliğini **true**olarak ayarlayın. Sayfalayıcı satırı, PagerStyle ve PagerSettings özellikleri kullanılarak özelleştirilebilir.

## <a name="customizing-the-user-interface"></a>Kullanıcı Arabirimini Özelleştirme

Denetimin farklı bölümlerinin stil özelliklerini ayarlayarak DetailsView denetiminin görünümünü özelleştirebilirsiniz. Aşağıdaki tabloda farklı stil özellikleri listelenmektedir.

| **Style özelliği** | **Açıklama** |
| --- | --- |
| AlternatingRowStyle | DetailsView denetimindeki alternatif veri satırları için stil ayarları. Bu özellik ayarlandığında, veri satırları RowStyle ayarları ve **AlternatingRowStyle** ayarları arasında dönüşümlü olarak görüntülenir. |
| CommandRowStyle | DetailsView denetimindeki yerleşik komut düğmelerini içeren satırın stil ayarları. |
| Edıtrowstyle | DetailsView denetimi düzenleme modunda olduğunda veri satırları için stil ayarları. |
| EmptyDataRowStyle | Veri kaynağı herhangi bir kayıt içermiyorsa, DetailsView denetiminde görünen boş veri satırı için stil ayarları. |
| FooterStyle | DetailsView denetiminin altbilgi satırı için stil ayarları. |
| HeaderStyle | DetailsView denetiminin başlık satırı için stil ayarları. |
| InsertRowStyle | DetailsView denetimi ekleme modunda olduğunda veri satırları için stil ayarları. |
| PagerStyle | DetailsView denetiminin sayfalayıcı satırı için stil ayarları. |
| RowStyle | DetailsView denetimindeki veri satırları için stil ayarları. **AlternatingRowStyle** özelliği de ayarlandığında, veri satırları **RowStyle** ayarları ve **AlternatingRowStyle** ayarları arasında dönüşümlü olarak görüntülenir. |
| FieldHeaderStyle | DetailsView denetiminin üstbilgi sütunu için stil ayarları. |

## <a name="events"></a>Olaylar

DetailsView denetimi, programlama için kullanabileceğiniz çeşitli olaylar sağlar. Bu, bir olay meydana geldiğinde özel bir yordam çalıştırmanızı sağlar. Aşağıdaki tabloda, DetailsView denetimi tarafından desteklenen olaylar listelenmektedir. DetailsView denetimi Ayrıca bu olayları temel sınıflarından devralır: veri bağlama, veri sınırlama, atılmış, Init, Load, PreRender ve render.

| **Event** | **Açıklama** |
| --- | --- |
| ItemCommand | DetailsView denetimindeki bir düğmeye tıklandığında gerçekleşir. |
| ItemCreated | DetailsView denetiminde tüm ayrıntılar Viewrow nesneleri oluşturulduktan sonra gerçekleşir. Bu olay, genellikle bir kaydın görüntülenmeden önce değerlerini değiştirmek için kullanılır. |
| ItemDeleted | Bir Delete düğmesine tıklandığında, ancak DetailsView denetimi veri kaynağından kaydı sildiğinde gerçekleşir. Bu olay genellikle silme işleminin sonuçlarını denetlemek için kullanılır. |
| Itemsiliyor | Bir Delete düğmesine tıklandığında, ancak DetailsView denetimi veri kaynağından kaydı sildiğinde gerçekleşir. Bu olay genellikle silme işlemini iptal etmek için kullanılır. |
| Öğe yukarı | Bir INSERT düğmesine tıklandığında, ancak DetailsView denetimi kaydı eklediğinde gerçekleşir. Bu olay genellikle ekleme işleminin sonuçlarını denetlemek için kullanılır. |
| Iteminyıting | Bir INSERT düğmesine tıklandığında, ancak DetailsView denetimi kaydı eklemeden oluşur. Bu olay genellikle ekleme işlemini iptal etmek için kullanılır. |
| ItemUpdated | Bir Update düğmesine tıklandığında, ancak DetailsView denetimi satırı güncelleştirdikten sonra gerçekleşir. Bu olay genellikle güncelleştirme işleminin sonuçlarını denetlemek için kullanılır. |
| ItemUpdating | Bir Update düğmesine tıklandığında, ancak DetailsView denetimi kaydı güncelleştirmediğinde gerçekleşir. Bu olay genellikle güncelleştirme işlemini iptal etmek için kullanılır. |
| ModeChanged | DetailsView denetimi modları değiştirdikten sonra oluşur (düzenleme, ekleme veya salt okuma modu). Bu olay genellikle, DetailsView denetimi modları değiştirdiğinde bir görevi gerçekleştirmek için kullanılır. |
| Modu değiştirme | DetailsView denetimi modları değiştirmeden önce oluşur (düzenleme, ekleme veya salt okuma modu). Bu olay, genellikle bir mod değişikliğini iptal etmek için kullanılır. |
| PageIndexChanged | Sayfalayıcı düğmelerinden biri tıklandığında gerçekleşir, ancak DetailsView denetimi disk belleği işlemini işler. Bu olay genellikle Kullanıcı denetimdeki farklı bir kayda gittiğinde bir görev gerçekleştirmeniz gerektiğinde kullanılır. |
| PageIndexChanging | Sayfalayıcı düğmelerinden biri tıklandığında, ancak DetailsView denetimi disk belleği işlemini gerçekleştirmeden önce gerçekleşir. Bu olay genellikle sayfalama işlemini iptal etmek için kullanılır. |

## <a name="the-menu-control"></a>Menü denetimi

ASP.NET 2,0 ' deki menü denetimi tam özellikli bir gezinti sistemi olacak şekilde tasarlanmıştır. SiteMapDataSource gibi hiyerarşik veri kaynakları için kolayca verilere izin verebilir.

Bir menü denetimleri yapısı bildirimli veya dinamik olarak tanımlanabilir ve tek bir kök düğümünden ve herhangi bir sayıda alt düğümden oluşur. Aşağıdaki kod, menü denetimi için bir menüyü bildirimli olarak tanımlar.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

Yukarıdaki örnekte, Home. aspx düğümü kök düğümdür. Diğer tüm düğümler, çeşitli düzeylerde kök düğüm içinde iç içe geçmiş.

Menü denetiminin oluşturabileceği iki tür menü vardır; statik menüler ve dinamik menüler. Statik menüler her zaman görünür olan menü öğelerinden oluşur. Dinamik menüler yalnızca Kullanıcı fare ile üzerine geldiğinde görünen menü öğelerinden oluşur. Müşteriler genellikle statik menüleri, çalışma zamanında çok fazla veri sınırına sahip menüler ile bildirimli ve dinamik menülere karıştırabilir. Aslında, dinamik ve statik menüler, popülasyon yöntemiyle ilgisiz değildir. *Statik* ve *dinamik* terimleri yalnızca menünün varsayılan olarak statik olarak gösterilip gösterilmeyeceğini veya yalnızca Kullanıcı bazı işlemleri yapması durumunda görüntülenip görüntülenmeyeceğini ifade eder.

**StaticDisplayLevels** özelliği, menünün kaç düzeyinin statik olduğunu ve bu nedenle varsayılan olarak görüntülendiğini yapılandırmak için kullanılır. Yukarıdaki örnekte, **StaticDisplayLevels** özelliğinin 2 değerine ayarlanması, menünün ana düğümü, müzik düğümünü ve filmler düğümünü statik olarak görüntülemesine neden olur. Diğer tüm düğümler, Kullanıcı üst düğümün üzerine geldiğinde dinamik olarak görüntülenir.

**MaximumDynamicDisplayLevels** özelliği, menünün görüntüleme yeteneğine sahip olduğu en fazla dinamik düzey sayısını yapılandırır. **MaximumDynamicDisplayLevels** özelliği tarafından belirtilen değerden daha yüksek bir düzeydeki dinamik menüler atılır.

> [!NOTE]
> MaximumDynamicDisplayLevels özelliği nedeniyle menülerin işleme görünmediği durumlarla karşılaşmanız neredeyse kesin. Bu durumlarda, özelliğinin müşteriler menülerinin görüntülenmesi için yeterince ayarlandığından emin olun.

## <a name="data-binding-the-menu-control"></a>Menü denetimini veri bağlama

Menü denetimi, SiteMapDataSource veya XMLDataSource gibi herhangi bir hiyerarşik veri kaynağına bağlanabilir. Web. sitemap dosyası ve şeması, menü denetimine yönelik bilinen bir API sağladığından, bir menü denetimine veri bağlama için en yaygın kullanılan yöntemdir. Aşağıdaki listede basit bir Web. sitemap dosyası gösterilmektedir.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

Bu durumda, giriş öğesi olan yalnızca bir kök siteMapNode öğesi olduğuna dikkat edin. Her siteMapNode için çeşitli öznitelikler yapılandırılabilir. En yaygın olarak kullanılan öznitelikler şunlardır:

- **URL** Kullanıcı menü öğesine tıkladığında görüntülenecek URL 'YI belirtir. Bu öznitelik yoksa, düğüm tıklandığında yalnızca geri gönderilir.
- **başlık** Menü öğesinde görüntülenen metni belirtir.
- **Açıklama** Düğüm için belge olarak kullanılır. Ayrıca fare, düğümün üzerine gelindiğinde bir araç ipucu olarak görüntülenir.
- **siteMapFile** İç içe Sitemaps için izin verir. Bu öznitelik, iyi biçimlendirilmiş bir ASP.NET sitemap dosyasına işaret etmelidir.
- **Roller** ASP.NET güvenlik kırpması tarafından denetlenerek bir düğümün görünümüne izin verir.

Bu özniteliklerin tümü isteğe bağlı olsa da, menünün davranışı belirtilmemişse, beklenmediğini unutmayın. Örneğin, *URL* özniteliği belirtilmişse ancak *Açıklama* özniteliği değilse, düğüm görünür olmayacaktır ve belirtilen URL 'ye gitmenin bir yolu olmayacaktır.

## <a name="controlling-a-menus-operation"></a>Menüler Işlemini denetleme

Bir ASP.NET Menu denetiminin işlemini etkileyen bazı özellikler vardır; **yönlendirme** özelliği, **DisappearAfter** özelliği, **StaticItemFormatString** özelliği ve **StaticPopOutImageUrl** özelliği bunlardan yalnızca birkaçıdır.

- **Yön** *yatay* veya *Dikey* olarak ayarlanabilir ve statik menü öğelerinin yatay olarak bir satırda mi yoksa dikey olarak mı düzenlendiğini ve bir diğerinin üzerine yığılmadığını denetler. Bu özellik dinamik menüleri etkilemez.
- **DisappearAfter** özelliği, fare konumundan uzağa taşındıktan sonra bir dinamik menünün görünür kalması gereken süreyi yapılandırır. Değer milisaniye cinsinden belirtilir ve varsayılan olarak 500 ' dir. Bu özelliğin-1 değerine ayarlanması, menünün hiçbir şekilde otomatik olarak kaybolmasına neden olur. Bu durumda, menü yalnızca kullanıcının menünün dışını tıkladığı zaman kaybolacaktır.
- **StaticItemFormatString** özelliği, menü sisteminizde tutarlı verkage 'in korunmasını kolaylaştırır. Bu özelliği belirtirken, veri kaynağında görünen açıklamanın yerine *{0}* girilmelidir. Örneğin, alıştırma 1 ' den menü öğesine sahip olmak için, ürünlerimiz sayfamızı ziyaret edin, vb., StaticItemFormatString için {0} sayfamızı ziyaret edin. Çalışma zamanında ASP.NET, {0} herhangi bir oluşumunu menü öğesi için doğru açıklama ile değiştirecek.
- **StaticPopOutImageUrl** özelliği, belirli bir menü düğümünün, üzerine gelindiğinde erişilebilen alt düğümlere sahip olduğunu göstermek için kullanılan resmi belirtir. Dinamik menüler varsayılan görüntüyü kullanmaya devam edecektir.

## <a name="templated-menu-controls"></a>Şablonlu menü denetimleri

Menü denetimi şablonlu bir denetimdir ve iki farklı ItemTemplate için izin verir; StaticItemTemplate ve DynamicItemTemplate. Bu şablonları kullanarak, menülere kolayca sunucu denetimleri veya Kullanıcı denetimleri ekleyebilirsiniz.

Visual Studio .NET içindeki şablonları düzenlemek için menüdeki akıllı etiket düğmesine tıklayın ve Şablonları Düzenle ' yi seçin. Daha sonra StaticItemTemplate veya DynamicItemTemplate 'i Düzenle arasında seçim yapabilirsiniz.

StaticItemTemplate 'e eklenen denetimler, sayfa yüklendiğinde statik menüde görünür. DynamicItemTemplate 'e eklenen herhangi bir denetim, tüm açılır menülerde görünür.

## <a name="menu-events"></a>Menü olayları

Menü denetiminin kendine özgü iki olayı vardır; **Menuıtemclicked** ve **menuıtemtıtemi veri** bağlama olayı.

Bir menü öğesine tıklandığında Menuıtemclicked olayı tetiklenir. Menü öğesi veri sınırına ulaştığında Menuıtemveriye bağlı bir olay tetiklenir. Olay işleyicisine geçirilen **MenuEventArgs** , öğe özelliği aracılığıyla menü öğesine erişim sağlar.

## <a name="controlling-a-menus-appearance"></a>Menüler görünümünü denetleme

Ayrıca, menüler için kullanılabilen birçok stili kullanarak bir menü denetiminin görünümünü de etkileyebilirsiniz. Bunlar arasında **StaticMenuStyle**, **DynamicMenuStyle**, **DynamicMenuItemStyle**, **DynamicSelectedStyle**ve **DynamicHoverStyle**bulunur. Bu özellikler standart bir HTML stil dizesi kullanılarak yapılandırılır. Örneğin, aşağıdakiler dinamik menülerin stilini etkiler.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> Üzerine gelme stillerinden herhangi birini kullanıyorsanız, ' de *runat* Element for *Server*olarak ayarlanan bir &lt;Head&gt; öğesi eklemeniz gerekecektir.

Menü denetimleri Ayrıca ASP.NET 2,0 temalarının kullanımını destekler.

## <a name="the-treeview-control"></a>TreeView denetimi

TreeView denetimi verileri ağaç benzeri bir yapıda görüntüler. Menü denetiminde olduğu gibi, SiteMapDataSource gibi herhangi bir hiyerarşik veri kaynağına kolayca veri bağlanabilir.

Müşterilerin ASP.NET 2,0 ' de TreeView denetimi hakkında sormasını olası ilk soru, ASP.NET 1. x için kullanılabilir olan TreeView IE WebControl ile ilişkili olup olmadığını belirtir. Bu değildir. ASP.NET 2,0 TreeView denetimi sıfırdan yazılmıştır ve daha önce sunulan IE TreeView WebControl üzerinde önemli bir geliştirme sunar.

Bir TreeView denetimini, menü denetimiyle tamamen aynı şekilde gerçekleştirildiği için bir site haritasına bağlama konusunda ayrıntıya geçeceğim. Ancak, TreeView denetiminin, çalıştığı şekilde bazı farklı farklılıkları vardır.

Varsayılan olarak, bir TreeView denetimi tamamen genişletilir. İlk yük sonrasında genişletmenin düzeyini değiştirmek için denetimin **ExpandDepth** özelliğini değiştirin. Bu özellikle, belirli düğümleri genişletmede TreeView 'un veri genişliyor olduğu durumlarda önemlidir.

## <a name="databinding-the-treeview-control"></a>TreeView denetimini veri bağlama

Menü denetiminden farklı olarak, TreeView, büyük miktarlarda veriyi işlemek için iyi bir sonuç verir. Bu nedenle, bir SiteMapDataSource veya XMLDataSource 'a veri bağlamayı ek olarak TreeView, genellikle veri kümesine veya diğer ilişkisel verilere bağlanır. TreeView denetiminin büyük miktarda veriye bağlı olduğu durumlarda, yalnızca denetimde görünür olan verilere bağlamak en iyisidir. Daha sonra veri bağlama, TreeView düğümleri genişletilmiş şekilde ek verilere bağlanabilir.

Bu durumlarda, TreeView 'un **PopulateOnDemand** özelliği *true*olarak ayarlanmalıdır. Daha sonra **TreeNodePopulate** yöntemi için bir uygulama sağlamanız gerekir.

## <a name="data-binding-without-postback"></a>Geri gönderme olmadan veri bağlama

Önceki örnekteki bir düğümü ilk kez genişlettiğinizde, sayfanın geri gönderdiğine ve yenilediğine dikkat edin. Bu örnekteki bir sorun değildir, ancak büyük miktarda veri içeren bir üretim ortamında olabileceğini hayal edebilirsiniz. Daha iyi bir senaryo, TreeView 'un düğümleri hala dinamik olarak doldurmasına, ancak sunucuya geri göndermenize gerek kalmaz.

**PopulateNodesFromClient** ve **PopulateOnDemand** özelliklerini true olarak ayarlayarak, ASP.net TreeView denetimi düğümleri geri gönderme olmadan dinamik olarak dolduracaktır. Üst düğüm genişletildiğinde, istemciden bir XMLHttp isteği yapılır ve OnTreeNodePopulate olayı tetiklenir. Sunucu, daha sonra alt düğümleri bağlamak için kullanılan bir XML veri Adası ile yanıt verir.

ASP.NET, bu işlevi uygulayan istemci kodunu dinamik olarak oluşturur. Betiği içeren &lt;betik&gt; etiketleri bir AXD dosyasına işaret eden oluşturulur. Örneğin, aşağıdaki listede XMLHttp isteğini üreten betik kodu için komut dosyası bağlantıları gösterilmektedir.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

Tarayıcınızda yukarıdaki AXD dosyasına gözatıp dosyayı açarsanız, XMLHttp isteğini uygulayan kodu görürsünüz. Bu yöntem, müşterilerin betik dosyasını değiştirmelerini engeller.

## <a name="controlling-the-operation-of-the-treeview-control"></a>TreeView denetiminin Işlemini denetleme

TreeView denetiminin, denetimin işlemini etkileyen birkaç özelliği vardır. En belirgin özellikler **ShowCheckBox**, **ShowExpandCollapse**ve **ShowLines**özelliklerdir.

**ShowCheckBox** özelliği, düğümlerin işlendiğinde bir onay kutusu görüntüleyip görüntülemediğinin etkilenmeyeceğini etkiler. Bu özellik için geçerli değerler None, **root**, **Parent**, **yaprak**ve **All** **'tur**. Bu, TreeView denetimini aşağıdaki gibi etkiler:

| **Özellik değeri** | **Etki** |
| --- | --- |
| Yok. | Onay kutuları herhangi bir düğümde gösterilmez. Varsayılan ayar budur. |
| Asıl | Onay kutusu yalnızca kök düğümünde görüntülenir. |
| Üst öğe | Onay kutusu yalnızca alt düğümleri olan düğümlerde görüntülenir. Bu alt düğümler üst düğümler veya yaprak düğümler olabilir. |
| Dağıtımı | Bir onay kutusu yalnızca alt düğümleri olmayan düğümlerde görüntülenir. |
| Tümü | Tüm düğümlerde bir onay kutusu görüntülenir. |

Onay kutuları kullanılırken, **CheckedNodes** özelliği geri gönderme sırasında denetlenen bir TreeView düğümleri koleksiyonu döndürür.

**ShowExpandCollapse** özelliği, kök ve üst düğümlerin yanındaki Genişlet/Daralt resminin görünümünü denetler. Bu özellik **false**olarak ayarlandıysa, TreeView düğümleri köprü olarak işlenir ve bağlantıya tıklanarak genişletilir/daraltılır.

**ShowLines** özelliği, ana düğümlerin alt düğümlere bağlanması için satırların görüntülenip görüntülenmediğini denetler. **False** olduğunda (varsayılan), hiçbir satır gösterilmez. **True**olduğunda TreeView denetimi, **lineımafolder** özelliği tarafından belirtilen klasördeki çizgi görüntülerini kullanır.

Visual Studio .NET 2005, TreeView çizgilerinin görünümünü özelleştirmek için bir çizgi tasarlayıcı aracı içerir. Bu araca aşağıdaki şekilde TreeView denetimindeki akıllı etiket düğmesini kullanarak erişebilirsiniz.

![](data-bound-controls/_static/image1.jpg)

**Şekil 1**

**Satır görüntülerini Özelleştir** menü seçeneğini belirlediğinizde, satır Tasarımcısı aracı başlatılır ve bu da TreeView çizgilerinin görünümünü yapılandırmanıza olanak tanır.

## <a name="treeview-events"></a>TreeView olayları

TreeView denetimi aşağıdaki benzersiz olaylara sahiptir:

- **SelectAction** özelliğini temel alan bir düğüm seçildiğinde SelectedNodeChanged oluşur.
- TreeNodeCheckChanged, bir düğümler CheckBoxState değiştiğinde oluşur.
- Bir düğüm **SelectAction** özelliğine dayalı olarak genişletildiğinde Treenodegenişletilen oluşur.
- Bir düğüm daraltıldığında Treenodedaraltılması oluşur.
- Bir düğüm veri bağlı olduğunda Treenodeveri sınırlama oluşur.
- Bir düğüm doldurulursa TreeNodePopulate oluşur.

**SelectAction** özelliği, bir düğüm seçildiğinde hangi olayın tetiklenme olduğunu yapılandırmanıza olanak tanır. SelectAction Özelliği aşağıdaki eylemleri sağlar:

- TreeNodeSelectAction. Expand, düğüm seçildiğinde Treenodegenişletilir.
- TreeNodeSelectAction. None, düğüm seçildiğinde hiçbir olay vermez.
- TreeNodeSelectAction. Select, düğüm seçildiğinde SelectedNodeChanged olayını başlatır.
- TreeNodeSelectAction. SelectExpand, düğüm seçildiğinde SelectedNodeChanged olayını ve Treenodegenişletilen olayını oluşturur.

## <a name="controlling-appearance-with-styles"></a>Görünümleri stillerle denetleme

TreeView denetimi, denetimin görünümünü stillerle denetlemek için birçok özellik sağlar. Aşağıdaki özellikler mevcuttur.

| **Özellik adı** | **Denetimler** |
| --- | --- |
| HoverNodeStyle | Fare üzerine gelindiğinde düğümlerin stilini denetler. |
| LeafNodeStyle | Yaprak düğümlerin stilini denetler. |
| NodeStyle | Tüm düğümlerin stilini denetler. Belirli düğüm stilleri (LeafNodeStyle gibi) bu stili geçersiz kılar. |
| ParentNodeStyle | Tüm üst düğümlerin stilini denetler. |
| RootNodeStyle | Kök düğümün stilini denetler. |
| SelectedNodeStyle | Seçili düğümün stilini denetler. |

Bu özelliklerin her biri salt okunurdur. Ancak, her biri **TreeNodeStyle** nesnesi döndürür ve bu nesnenin özellikleri *Property-Subproperty* biçimi kullanılarak değiştirilebilir. Örneğin, **SelectedNodeStyle**'ın **ForeColor** özelliğini ayarlamak için aşağıdaki sözdizimini kullanın:

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

Yukarıdaki etiketin kapandığına dikkat edin. Bunun nedeni, burada gösterilen bildirime dayalı sözdiziminin kullanılması nedeniyle, ağaç görünümleri düğümlerini HTML koduna da dahil edersiniz.

Stil özellikleri, *Property. Subproperty* biçimi kullanılarak kodda de belirtilebilir. Örneğin, kodda **RootNodeStyle** 'ın **ForeColor** özelliğini ayarlamak için aşağıdaki sözdizimini kullanın:

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> Farklı stil özelliklerinin kapsamlı bir listesi için TreeNodeStyle nesnesinin MSDN belgelerine bakın.

## <a name="the-sitemappath-control"></a>Bu denetim

Bu, ASP.NET geliştiricileri için bir içerik haritası denetimi sağlar. Diğer gezinti denetimleri gibi, SiteMapDataSource veya XmlDataSource gibi hiyerarşik veri kaynaklarına kolayca veri bağlanabilir.

Bir bu denetim, SiteMapNodeItem nesnelerinden oluşur. Üç tür düğüm vardır; Kök düğüm, üst düğümler ve geçerli düğüm. Kök düğüm, hiyerarşik yapının en üstündeki düğümdür. Geçerli düğüm geçerli sayfayı temsil eder. Diğer tüm düğümler üst düğümlerdir.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>Bu denetimin Işlemini denetleme

, Bu denetimin işlemini denetleyen özellikler aşağıdaki gibidir:

| **Özellik** | **Özelliğin açıklaması** |
| --- | --- |
| Parentlevelsgörüntülendi | Kaç üst düğümün görüntülendiğini denetler. Varsayılan değer, görüntülenen üst düğümlerin sayısı üzerinde hiçbir kısıtlama döndüren-1 ' dir. |
| PathDirection | , Tadına 'ın yönünü denetler. Geçerli değerler RootToCurrent (varsayılan) ve CurrentToRoot değerleridir. |
| PathSeparator | Bir bir veren denetimindeki düğümleri ayıran karakteri denetleyen bir dize. Varsayılan değer:. |
| RenderCurrentNodeAsLink | Geçerli düğümün bağlantı olarak işlenip işlenmeyeceğini denetleyen bir Boole değeri. Varsayılan değer Yanlış değeridir. |
| SkipLinkText | Sayfa ekran okuyucular tarafından görüntülendiğinde erişilebilirliğe yardımcı olur. Bu özellik ekran okuyucularının, bu denetimi atlamasına izin verir. Bu özelliği devre dışı bırakmak için, özelliğini String. Empty olarak ayarlayın. |

## <a name="templated-sitemappath-controls"></a>Şablonlu denetim denetimleri

SiteMapControl şablonlu bir denetimdir ve bu şekilde, denetimi görüntülerken kullanmak üzere farklı şablonlar tanımlayabilirsiniz. Bir bu denetim içindeki şablonları düzenlemek için, denetimdeki akıllı etiket düğmesine tıklayın ve menüden Şablonları Düzenle ' yi seçin. Bu, aşağıda gösterildiği gibi, kullanılabilir farklı şablonlar arasından seçim yapabileceğiniz SiteMapTasks menüsünü görüntüler.

![](data-bound-controls/_static/image2.jpg)

**Şekil 2**

**NodeTemplate** şablonu, her bir düğüme başvurur. Düğüm bir kök düğüm veya geçerli düğüm ve bir **RootNodeTemplate** ya da **CurrentNodeTemplate** yapılandırılmışsa, NodeTemplate geçersiz kılınır.

## <a name="sitemappath-events"></a>Bu olaylar

IBU denetim, Denetim sınıfından türetilmeyen iki olaya sahiptir; **ItemCreated** olayı ve **ıtemveriye** bağlı olayı. ItemCreated olayı, bir bir bir bir bir bir bir bir bir bir bir bir bir Bir bir bir bir bir, bir bir bir bir bir bir bir bir bir bir bir bir bir bir değer bağlama sırasında Bir **Sitemapnodeitemeventargs** nesnesi, öğe özelliği aracılığıyla belirli SiteMapNodeItem öğesine erişim sağlar.

## <a name="controlling-appearance-with-styles"></a>Görünümleri stillerle denetleme

Bir bir, bir bir bir bir bir bir denetim listesi için aşağıdaki stiller mevcuttur.

| **Özellik adı** | **Denetimler** |
| --- | --- |
| CurrentNodeStyle | Geçerli düğümün metin stilini denetler. |
| RootNodeStyle | Kök düğümün metin stilini denetler. |
| NodeStyle | Bir CurrentNodeStyle veya RootNodeStyle 'ın geçerli olmadığı varsayılarak tüm düğümlerin metin stilini denetler. |

NodeStyle özelliği, CurrentNodeStyle ya da RootNodeStyle tarafından geçersiz kılınır. Bu özelliklerin her biri salt okunurdur ve bir **Stil** nesnesi döndürür. Bu özelliklerden birini kullanarak bir düğümün görünümünü etkilemek için döndürülen stil nesnesinin özelliklerini ayarlamanız gerekecektir. Örneğin, aşağıdaki kod geçerli düğümün ForeColor özelliğini değiştirir.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

Özelliği de programlı olarak aşağıdaki gibi uygulanabilir:

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> Şablon uygulanmışsa, stil uygulanmaz.

## <a name="lab-1-configuring-an-aspnet-menu-control"></a>Lab 1: ASP.NET Menu denetimini yapılandırma

1. Yeni bir Web sitesi oluşturun.
2. Dosya, yeni, dosya ' yı seçerek ve dosya şablonları listesinden site haritası ' nı seçerek bir site haritası dosyası ekleyin.
3. Site haritasını (varsayılan olarak Web. sitemap) açın ve aşağıdaki listeye benzemek üzere değiştirin. Site Haritası dosyasında bağlanmakta olduğunuz sayfalar gerçekten yoktur, ancak bu alıştırma için bir sorun olmayacaktır.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. Tasarım görünümü varsayılan Web formunu açın.
5. Araç kutusunun Gezinti bölümünden sayfaya yeni bir menü denetimi ekleyin.
6. Araç kutusunun veri bölümünden yeni bir SiteMapDataSource ekleyin. SiteMapDataSource, sitenizdeki Web. sitemap dosyasını otomatik olarak kullanacaktır. (Web. *sitemap dosyası sitesinin kök klasöründe olmalıdır.* )
7. Menü denetimi ' ne tıklayın ve ardından akıllı etiket düğmesine tıklayarak menü görevleri iletişim kutusunu görüntüleyin.
8. Veri kaynağı seç açılan menüsünde SiteMapDataSource1 ' yi seçin.
9. Otomatik Biçimlendir bağlantısına tıklayın ve menü için bir biçim seçin.
10. Özellikler bölmesinde, **StaticDisplayLevels** özelliğini 2 olarak ayarlayın. Menü denetimi artık tasarımcıda giriş, ürünler ve Hizmetler düğümünü görüntülemelidir.
11. Menüsünü kullanmak için tarayıcınızda sayfaya gidin. (Site haritasına eklediğiniz sayfalar gerçekten mevcut olmadığından, bu dosyalara erişmeye çalıştığınızda bir hata görürsünüz.)

StaticDisplayLevels ve MaximumDynamicDisplayLevels özelliklerini değiştirmeyi deneyin ve menünün nasıl oluşturulduğunu nasıl etkilediğini görün.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>Laboratuvar 2: bir TreeView denetimini dinamik olarak bağlama

Bu alıştırma, yerel olarak çalıştırdığınız SQL Server olduğunu ve Northwind veritabanının SQL Server örneğinde bulunduğunu varsayar. Bu koşullar karşılanmazsa, lütfen örnekteki bağlantı dizesini değiştirin. Ayrıca, güvenilir bir bağlantı yerine SQL Server kimlik doğrulaması belirtmeniz gerekebileceğini unutmayın.

1. Yeni bir Web sitesi oluşturun.
2. Default. aspx için kod görünümüne geçin ve tüm kodu aşağıda listelenen kodla değiştirin. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. Sayfayı TreeView. aspx olarak kaydedin.
4. Sayfasına gözatamazsınız.
5. Sayfa ilk görüntülendiğinde, tarayıcınızdaki sayfanın kaynağını görüntüleyin. İstemciye yalnızca görünür düğümlerin gönderildiğini unutmayın.
6. Herhangi bir düğümün yanındaki artı işaretine tıklayın.
7. Sayfadaki kaynağı yeniden görüntüleyin. Yeni görüntülenen düğümlerin artık mevcut olduğuna dikkat edin.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>Laboratuvar 3: Ayrıntılar GridView ve DetailsView kullanarak verileri görüntüleme ve düzenlemeyle

1. Yeni bir Web sitesi oluşturun.
2. Web sitesine yeni bir Web. config ekleyin.
3. Web. config dosyasına aşağıda gösterildiği gibi bir bağlantı dizesi ekleyin: 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > Bağlantı dizesini ortamınıza göre değiştirmeniz gerekebilir.
4. Web. config dosyasını kaydedin ve kapatın.
5. Default. aspx ' i açın ve yeni bir SqlDataSource denetimi ekleyin.
6. SqlDataSource denetiminin KIMLIĞINI **Products**olarak değiştirin.
7. **SqlDataSource Tasks** menüsünde, **veri kaynağını Yapılandır**' a tıklayın.
8. Bağlantı açılan menüsünde **Northwind** ' i seçin ve ileri ' ye tıklayın.
9. **Ad** açılan listesinden **Ürünler** ' i seçin ve aşağıda gösterildiği gibi **ProductID**, **ProductName**, **BirimFiyat**ve **UnitsInStock** onay kutularını işaretleyin. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. **İleri**'ye tıklayın.
11. **Son**'a tıklayın.
12. Kaynak görünümüne geçin ve oluşturulan kodu inceleyin. , SqlDataSource denetimine eklenen **SelectCommand**, **DeleteCommand**, **InsertCommand**ve **UpdateCommand** 'e dikkat edin. Ayrıca eklenen parametrelere de dikkat edin.
13. Tasarım görünümü geçin ve sayfaya yeni bir GridView denetimi ekleyin.
14. **Veri kaynağı seç** açılan listesinden **Ürünler** ' i seçin.
15. **Sayfalamayı Etkinleştir** ' i işaretleyin ve aşağıda gösterildiği gibi **seçimi etkinleştirin** . 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. **Sütunları Düzenle** bağlantısına tıklayın ve **alanları otomatik oluştur** ' un seçili olduğundan emin olun.
17. **Tamam**’a tıklayın.
18. GridView denetimi seçili olduğunda, Özellikler bölmesinde **DataKeyNames** özelliğinin yanındaki düğmesine tıklayın.
19. **Kullanılabilir veri alanları** listesinden **ProductID** öğesini seçin ve eklemek için **&gt;** düğmesine tıklayın.
20. Tamam'a tıklayın.
21. Sayfaya yeni bir SqlDataSource denetimi ekleyin.
22. SqlDataSource denetiminin KIMLIĞINI **Ayrıntılar**olarak değiştirin.
23. SqlDataSource Tasks menüsünde, **veri kaynağını Yapılandır**' ı seçin.
24. Açılan listeden **Northwind** ' i seçin ve **İleri**' ye tıklayın.
25. <strong>Ad</strong> açılan listesinden <strong>Ürünler</strong> ' i seçin ve <strong>sütunlar</strong> liste kutusunda <strong>\</strong > * onay kutusunu işaretleyin.
26. **WHERE** düğmesine tıklayın.
27. **Sütun** açılan listesinden **ProductID** ' yi seçin.
28. Operatör açılan menüsünde **=** ' yi seçin.
29. **Kaynak** açılan menüsünden **Denetim** ' i seçin.
30. **DENETIM kimliği** açılan listesinden **GridView1** öğesini seçin.
31. WHERE yan tümcesini eklemek için **Ekle** düğmesine tıklayın.
32. **Tamam**’a tıklayın.
33. **Gelişmiş** düğmesine tıklayın ve **Insert, Update ve delete deyimlerini oluştur** onay kutusunu işaretleyin.
34. **Tamam**’a tıklayın.
35. **İleri** ' ye tıklayın ve **son**' a tıklayın.
36. Sayfaya bir DetailsView denetimi ekleyin.
37. **Veri kaynağı seç** açılan menüsünde **Ayrıntılar**' ı seçin.
38. Aşağıda gösterildiği gibi, **Düzenle etkinleştir** onay kutusunu işaretleyin. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. Sayfayı kaydedin ve default. aspx ' i tarayın.
40. DetailsView 'un otomatik olarak güncelleştirilmesini görmek için farklı kayıtlar ' ın yanındaki bağlantıyı **Seç** bağlantısına tıklayın.
41. DetailsView denetimindeki **düzenleme** bağlantısına tıklayın.
42. Kayıtta bir değişiklik yapıp **Güncelleştir**' e tıklayın.
