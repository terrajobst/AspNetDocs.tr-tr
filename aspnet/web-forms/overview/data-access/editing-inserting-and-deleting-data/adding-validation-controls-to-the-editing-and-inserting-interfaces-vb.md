---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
title: Düzenle ve ekleme arabirimlerine doğrulama denetimleri ekleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, daha fazla bilgi sağlamak için bir veri Web denetiminin EditItemTemplate ve InsertItemTemplate 'e doğrulama denetimleri eklemenin ne kadar kolay olduğunu görüyoruz.
ms.author: riande
ms.date: 07/17/2006
ms.assetid: e3d7028a-7a22-4a4f-babe-d53afc41c0e2
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c5ad110ee0836f0a464b02a2b29254e2e06381e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78592829"
---
# <a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-vb"></a>Düzenleme ve Ekleme Arabirimlerine Doğrulama Denetimleri Ekleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_VB.exe) veya [PDF 'yi indirin](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/datatutorial19vb1.pdf)

> Bu öğreticide, daha fazla folipop Kullanıcı arabirimi sağlamak üzere bir veri Web denetiminin EditItemTemplate ve InsertItemTemplate 'e doğrulama denetimleri eklemenin ne kadar kolay olduğunu görüyoruz.

## <a name="introduction"></a>Giriş

Son üç öğreticilerde araştırdığımız örneklerde GridView ve DetailsView denetimlerin hepsi BoundFields ve CheckBoxFields (GridView veya DetailsView bir veri kaynağına bağlanırken Visual Studio tarafından otomatik olarak eklenen alan türleri) ile oluşturulmuş Akıllı etiket aracılığıyla kontrol edin). GridView veya DetailsView içindeki bir satırı düzenlediğinizde, Salt okunabilir olmayan bu Fields alanları, son kullanıcının mevcut verileri değiştirebileceği metin kutularına dönüştürülür. Benzer şekilde, bir DetailsView denetimine yeni bir kayıt eklenirken, `InsertVisible` özelliği `True` olarak ayarlanmış olan BoundFields (varsayılan), kullanıcının yeni kaydın alan değerlerini sağlayabileceği boş metin kutuları olarak işlenir. Benzer şekilde, standart, salt okunurdur arabiriminde devre dışı bırakılan CheckBoxFields, düzen ve ekleme arabirimlerinde etkinleştirilmiş onay kutularına dönüştürülür.

BoundField ve CheckBoxField için varsayılan Düzenle ve ekleme arabirimleri faydalı olabilir, ancak arabirimin herhangi bir doğrulama sıralaması yoktur. Bir Kullanıcı, `ProductName` alanı atlama veya `UnitsInStock` için geçersiz bir değer (örneğin-50) girme gibi bir veri girişi yapıyorsa, uygulama mimarisinin derinlikleri içinden bir özel durum tetiklenir. Bu özel durum, [önceki öğreticide](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)gösterildiği gibi normal şekilde işlenebilirler, ancak kullanıcı arabiriminin düzenlenmesinde veya yerleştirilmesi, kullanıcının bu tür geçersiz verileri ilk yere girmesini engellemek için doğrulama denetimlerini içerir.

Özelleştirilmiş bir düzen veya ekleme arabirimi sağlamak için, BoundField veya CheckBoxField değerini TemplateField ile değiştirmeniz gerekir. [GridView denetiminde Templatefields kullanma](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) ve [DetailsView denetim öğreticilerinde templatefields kullanma](../custom-formatting/using-templatefields-in-the-detailsview-control-vb.md) konusunda tartışma konusu olan templatefields, farklı satır durumları için ayrı arabirimler tanımlayan birden çok şablondan oluşabilir. TemplateField 'ın `ItemTemplate`, DetailsView veya GridView denetimlerinde salt okunurdur alanları veya satırları işlerken kullanılır, ancak `EditItemTemplate` ve `InsertItemTemplate` sırasıyla düzen ve ekleme modları için kullanılacak arabirimleri gösterir.

Bu öğreticide, daha fazla folipop Kullanıcı arabirimi sağlamak üzere TemplateField 'ın `EditItemTemplate` ve `InsertItemTemplate` doğrulama denetimleri eklemenin ne kadar kolay olduğunu inceleyeceğiz. Özellikle bu öğretici, öğreticiyi [ekleme, güncelleştirme ve silme Ile Ilişkili olayları İnceleme](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) ve uygun doğrulamayı dahil etmek için Düzenle ve ekleme arabirimlerini genişletirken oluşturulan örneği alır.

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deleting"></a>Adım 1:[ekleme, güncelleştirme ve silme Ile Ilişkili olayları İnceleme](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) Işleminden örnek çoğaltılıyor

[Ekleme, güncelleştirme ve silme öğreticisiyle Ilişkili olayları incelerken](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) , düzenlenebilir bir GridView içindeki ürünlerin adlarını ve fiyatlarını listelenen bir sayfa oluşturduk. Ayrıca, Bu sayfa, `DefaultMode` özelliği `Insert`olarak ayarlanan ve böylece her zaman Insert modunda işlenen bir DetailsView içeriyordu. Bu DetailsView 'da, Kullanıcı yeni bir ürünün adını ve fiyatını girebilir, Ekle ' ye tıklayıp sisteme eklenmesini sağlayabilir (bkz. Şekil 1).

[Önceki örnek ![kullanıcıların yeni ürünler eklemesine ve var olanları düzenlemesine Izin verir](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image1.png)

**Şekil 1**: önceki örnek, kullanıcıların yeni ürünler eklemesine ve var olanları düzenlemesine olanak tanır ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image3.png))

Bu öğreticide bizim amamız,, doğrulama denetimleri sağlamak için DetailsView ve GridView 'un artırılması. Özellikle, doğrulama mantığımız şunları sağlayacak:

- Bir ürün eklenirken veya düzenlenirken adın sağlanması gerekir
- Bir kayıt eklenirken fiyatın sağlanması gerekir; bir kayıt düzenlenirken, yine de bir fiyat isteyecek, ancak daha önceki öğreticiden daha önce GridView 'un `RowUpdating` olay işleyicisindeki programlama mantığını kullanacaktır
- Fiyat için girilen değerin geçerli bir para birimi biçimi olduğundan emin olun

Doğrulama eklemek için önceki örneği genişletmenin artırılmasına bakabilmemiz için öncelikle `DataModificationEvents.aspx` sayfasından Bu öğreticinin sayfasına çoğaltılmamız gerekir, `UIValidation.aspx`. Bunu gerçekleştirmek için hem `DataModificationEvents.aspx` sayfanın bildirim temelli işaretlemesini hem de kaynak kodunu kopyalamanız gerekir. İlk olarak, aşağıdaki adımları gerçekleştirerek bildirim temelli biçimlendirmenin üzerine kopyalayın:

1. Visual Studio 'da `DataModificationEvents.aspx` sayfasını açın
2. Sayfanın bildirim temelli biçimlendirmesine gidin (sayfanın altındaki kaynak düğmesine tıklayın)
3. `<asp:Content>`, Şekil 2 ' de gösterildiği gibi, metni ve `</asp:Content>` etiketleri (3 ila 44) kopyalayın.

[&lt;ASP: Content&gt; Control Içindeki metni kopyalamak ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image4.png)

**Şekil 2**: `<asp:Content>` denetim içindeki metni kopyalama ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image6.png))

1. `UIValidation.aspx` sayfasını açın
2. Sayfanın bildirim temelli işaretlemesini git
3. `<asp:Content>` denetiminin içindeki metni yapıştırın.

Kaynak kodu üzerine kopyalamak için `DataModificationEvents.aspx.vb` sayfasını açın ve yalnızca `EditInsertDelete_DataModificationEvents` sınıfının *içindeki* metni kopyalayın. Üç olay işleyicisini (`Page_Load`, `GridView1_RowUpdating`ve `ObjectDataSource1_Inserting`) kopyalayın, ancak sınıf **bildirimini kopyalamayın.** Kopyalanmış *metni `UIValidation.aspx.vb`içindeki `EditInsertDelete_UIValidation`* sınıfında yapıştırın.

`DataModificationEvents.aspx` içerik ve koddan `UIValidation.aspx`' e taşıdıktan sonra, bir tarayıcıda ilerlemenizi test etmek biraz zaman ayırın. Aynı çıktıyı görmeniz ve bu iki sayfanın her birinde aynı işlevselliğe sahip olmanız gerekir (`DataModificationEvents.aspx` eylem sırasında ekran görüntüsü için Şekil 1 ' e geri bakın).

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>2\. Adım: BoundFields alanlarını TemplateFields 'e dönüştürme

Düzenle ve ekleme arabirimlerine doğrulama denetimleri eklemek için, DetailsView ve GridView denetimleri tarafından kullanılan BoundFields 'in TemplateFields 'e dönüştürülmesi gerekir. Bunu başarmak için, GridView ve DetailsView içindeki Akıllı Etiketler ' de sütunları Düzenle ve alanları Düzenle bağlantıları ' na tıklayın. Burada, BoundFields alanlarını seçip "Bu alanı TemplateField 'a Dönüştür" bağlantısına tıklayın.

[DetailsView 'ın ve GridView 'un BoundFields alanlarının her birini TemplateFields 'e dönüştürmek ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image7.png)

**Şekil 3**: DetailsView 'un ve GridView 'un Boundfields alanlarının her birini Templatefields 'e Dönüştür ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image9.png))

Alanlar iletişim kutusu aracılığıyla bir BoundField 'ı TemplateField 'a dönüştürmek, aynı salt okuma, düzenlemenin ve ekleme arabirimlerini BoundField 'un kendisi olarak gösteren bir TemplateField oluşturur. Aşağıdaki biçimlendirme, bir TemplateField 'a dönüştürüldükten sonra DetailsView içindeki `ProductName` alanı için bildirime dayalı sözdizimini gösterir:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample1.aspx)]

Bu TemplateField 'ın `ItemTemplate`, `EditItemTemplate`ve `InsertItemTemplate`otomatik olarak oluşturduğu üç şablon olduğunu unutmayın. `ItemTemplate`, bir etiket Web denetimi kullanarak tek bir veri alanı değeri (`ProductName`) görüntüler, `EditItemTemplate` ve `InsertItemTemplate`, veri alanını, iki yönlü veri bağlamayı kullanarak TextBox 'ın `Text` özelliği ile ilişkilendiren bir TextBox Web denetimindeki veri alanı değerini sunar. Bu sayfada yalnızca eklemek üzere DetailsView 'u kullandığımız için, `ItemTemplate` ve `EditItemTemplate` iki TemplateFields 'tan ayrılmakla kalmaz.

GridView, DetailsView 'un yerleşik ekleme özelliklerini desteklemediğinden, GridView 'un `ProductName` alanını TemplateField 'a dönüştürmek yalnızca bir `ItemTemplate` ve `EditItemTemplate`sonuçlanır:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample2.aspx)]

"Bu alanı TemplateField 'a Dönüştür" seçeneğine tıkladığınızda Visual Studio, şablonları dönüştürülmüş BoundField Kullanıcı arabirimini taklit eden bir TemplateField oluşturdu. Bu sayfayı bir tarayıcı aracılığıyla ziyaret ederek doğrulayabilirsiniz. Bunun yerine, TemplateFields görünümü ve davranışının, BoundFields kullanılırken deneyimle aynı olduğunu fark edeceksiniz.

> [!NOTE]
> Şablonlarda bulunan Düzenle arabirimlerini gerektiği gibi özelleştirebilirsiniz. Örneğin, `UnitPrice` TemplateFields metin kutusunu `ProductName` metin kutusu 'ndan daha küçük bir metin kutusu olarak oluşturulmasını istiyoruz. Bunu gerçekleştirmek için, TextBox 'ın `Columns` özelliğini uygun bir değere ayarlayabilir veya `Width` özelliği aracılığıyla mutlak bir genişlik sağlayabilirsiniz. Sonraki öğreticide, metin kutusunu alternatif bir veri girişi Web denetimiyle değiştirerek, düzen arabirimini tamamen özelleştirmeyi öğreneceksiniz.

## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>Adım 3: GridView 'un`EditItemTemplate` s 'ye doğrulama denetimleri ekleme

Veri girişi formları oluştururken, kullanıcıların gerekli alanları girmesi ve tüm sağlanmış girişlerin meşru, düzgün biçimli değerler olması önemlidir. ASP.NET, bir kullanıcının girişlerinin geçerli olduğundan emin olmak için, tek bir giriş denetiminin değerini doğrulamak üzere tasarlanan beş yerleşik doğrulama denetimi sağlar:

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) bir değer sağlanmış olmasını sağlar
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) bir değeri başka bir Web denetim değeri veya sabit bir değere göre doğrular ya da değerin biçiminin belirtilen veri türü için geçerli olmasını sağlar
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) , bir değerin bir değer aralığı içinde olmasını sağlar
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) bir değeri [normal bir ifadeye](http://en.wikipedia.org/wiki/Regular_expression) doğrular
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) bir değeri özel, Kullanıcı tanımlı bir yönteme göre doğrular

Bu beş denetim hakkında daha fazla bilgi için, [ASP.net hızlı başlangıç öğreticilerinin](https://asp.net/QuickStart/aspnet/) [doğrulama denetimleri bölümüne](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx) bakın.

Öğreticimiz için hem DetailsView hem de GridView 'un `ProductName` TemplateFields ve DetailsView 'un `UnitPrice` TemplateField ' da bir RequiredFieldValidator kullanması gerekir. Ayrıca, girilen fiyatın 0 ' dan büyük veya buna eşit bir değere sahip olduğundan ve geçerli bir para birimi biçiminde sunulduğundan emin olmak için, hem denetimlerin ' `UnitPrice` TemplateFields ' a bir CompareValidator eklemesi gerekir.

> [!NOTE]
> ASP.NET 1. x aynı beş doğrulama denetimine sahip olduğundan, ASP.NET 2,0, Internet Explorer dışındaki tarayıcılar için istemci tarafında iki komut dosyası desteğiyle ve bir sayfadaki doğrulama denetimlerini bölümleyebilme olanağı sunan bir dizi iyileştirme ekledi. doğrulama grupları. 2,0 sürümündeki yeni doğrulama denetimi özellikleri hakkında daha fazla bilgi için, [ASP.NET 2,0 ' de doğrulama denetimlerinin nasıl dağlamadiğini](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)inceleyin.

GridView 'un TemplateFields `EditItemTemplate` s öğesine gerekli doğrulama denetimlerini ekleyerek başlayalım. Bunu gerçekleştirmek için GridView 'un akıllı etiketindeki Şablonları Düzenle bağlantısına tıklayarak şablon düzenleme arabirimini açın. Buradan, açılan listeden hangi şablonun düzenleneceğini seçebilirsiniz. Düzen arabirimini artırmak istediğimiz için, `ProductName` ve `UnitPrice``EditItemTemplate` s için doğrulama denetimleri eklememiz gerekiyor.

[![ProductName ve BirimFiyat 'ın Editıtemtemplates 'i genişletmemiz gerekiyor](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image10.png)

**Şekil 4**: `ProductName` ve `UnitPrice``EditItemTemplate` öğeleri genişletireceğiz ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image12.png))

`ProductName` `EditItemTemplate`, araç kutusundan sürükleyerek bir RequiredFieldValidator ekleyin ve TextBox 'dan sonra koyun.

[ProductName EditItemTemplate 'e bir RequiredFieldValidator eklemek ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image13.png)

**Şekil 5**: `ProductName` `EditItemTemplate` bir RequiredFieldValidator ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image15.png))

Tüm doğrulama denetimleri, tek bir ASP.NET Web denetiminin girişini doğrulayarak çalışır. Bu nedenle, yeni eklediğimiz bir RequiredFieldValidator 'ın `EditItemTemplate`metin kutusuna göre doğrulanması gerektiğini belirtmemiz gerekir; Bu, doğrulama denetiminin [ControlToValidate özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) uygun Web denetiminin `ID` ayarlanarak gerçekleştirilir. Metin kutusu şu anda `TextBox1``ID` olmayan komut dosyası değil, ancak daha uygun bir şekilde değiştirelim. Şablondaki TextBox ' a tıklayın ve ardından Özellikler penceresi `ID` `TextBox1` ' den `EditProductName`' e değiştirin.

[![TextBox 'ın KIMLIĞINI EditProductName olarak değiştirme](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image16.png)

**Şekil 6**: TextBox 'ın `ID` `EditProductName` olarak değiştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image18.png))

Sonra, RequiredFieldValidator 'ın `ControlToValidate` özelliğini `EditProductName`olarak ayarlayın. Son olarak, [ErrorMessage özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) "ürün adını sağlamanız gerekir" ve [metin özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) "\*" olarak ayarlayın. Sağlanırsa `Text` Özellik değeri, doğrulama başarısız olursa doğrulama denetimi tarafından görüntülenen metindir. Gerekli `ErrorMessage` Özellik değeri, ValidationSummary denetimi tarafından kullanılır; `Text` Özellik değeri atlanırsa, `ErrorMessage` Özellik değeri aynı zamanda doğrulama denetimi tarafından geçersiz girişte görüntülenir.

Bu üç RequiredFieldValidator özelliğini ayarladıktan sonra ekranınızın Şekil 7 ' ye benzer olması gerekir.

[RequiredFieldValidator için ControlToValidate, ErrorMessage ve metin özelliklerini ayarlamak ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image19.png)

**Şekil 7**: RequiredFieldValidator `ControlToValidate`, `ErrorMessage`ve `Text` özelliklerini ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image21.png))

RequiredFieldValidator, `ProductName` `EditItemTemplate`eklendikçe, `UnitPrice` `EditItemTemplate`gerekli doğrulamayı eklemektir. Bu sayfada, bir kaydı düzenlenirken `UnitPrice` isteğe bağlı olduğundan, bir RequiredFieldValidator eklemesi gerekmez. Ancak, sağlanan `UnitPrice`, bir para birimi olarak düzgün biçimlendirildiğinden ve 0 ' dan büyük veya buna eşit olduğundan emin olmak için bir CompareValidator eklemesi gerekir.

CompareValidator `UnitPrice` `EditItemTemplate`eklemeden önce, önce TextBox Web denetiminin KIMLIĞINI `TextBox2` `EditUnitPrice`olarak değiştirelim. Bu değişikliği yaptıktan sonra, `ControlToValidate` özelliğini `EditUnitPrice`olarak ayarlayarak, `ErrorMessage` özelliğini "Price, sıfırdan büyük veya sıfıra eşit olmalıdır ve para birimi sembolünü" ve `Text` özelliğini "\*" ile içermemelidir.

`UnitPrice` değerin 0 ' dan büyük veya buna eşit olması gerektiğini belirtmek için, CompareValidator 'in [işleç özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) `GreaterThanEqual`, [ValueToCompare özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) "0" ve [Type özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) `Currency`olarak ayarlayın. Aşağıdaki bildirime dayalı sözdizimi, bu değişiklikler yapıldıktan sonra `UnitPrice` TemplateField `EditItemTemplate` gösterir:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample3.aspx)]

Bu değişiklikleri yaptıktan sonra sayfayı bir tarayıcıda açın. Bir ürünü düzenlenirken adı atlamaya veya geçersiz bir fiyat değeri girmeye çalışırsanız, TextBox ' ın yanında bir yıldız işareti görünür. Şekil 8 ' de gösterildiği gibi, $19,95 gibi para birimi sembolünü içeren bir fiyat değeri geçersiz sayılır. CompareValidator 'ın `Currency` `Type`, basamak ayırıcılarına (kültür ayarlarına bağlı olarak virgüller veya noktalar gibi), önde gelen artı veya eksi işaretiyle izin verir, ancak para birimi simgesine izin *vermez* . Bu davranış, Düzenle arabirimi olarak Kullanıcı tarafından, `UnitPrice` para birimi biçimini kullanarak şu anda bir şekilde işler.

> [!NOTE]
> *Ekleme, güncelleştirme ve silme öğreticisiyle Ilişkili olaylarda* , bir para birimi olarak biçimlendirmek için BoundField 'un `DataFormatString` özelliğini `{0:c}` olarak ayarlayacağız. Ayrıca, `ApplyFormatInEditMode` özelliğini true olarak ayarlayacağız. Bu, GridView 'ın düzenlenme arabiriminin `UnitPrice` bir para birimi olarak biçimlendirilmesine neden olur. BoundField bir TemplateField 'a dönüştürülürken, Visual Studio bu ayarları ve metin kutusu `Text` özelliğini, veri bağlama söz dizimi `<%# Bind("UnitPrice", "{0:c}") %>`kullanarak bir para birimi olarak biçimlendirdi.

[![, geçersiz girişi olan metin kutularının yanında bir yıldız Işareti görünür](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image22.png)

**Şekil 8**: geçersiz giriş metin kutularının yanında bir yıldız işareti görünür ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image24.png))

Doğrulama olduğu gibi çalışırken, kullanıcının kabul edilebilir olmayan bir kaydı düzenlenirken para birimi sembolünü el ile kaldırması gerekir. Bu sorunu gidermek için üç seçenek vardır:

1. `UnitPrice` değeri bir para birimi olarak biçimlendirilmemesi için `EditItemTemplate` yapılandırın.
2. CompareValidator öğesini kaldırarak ve düzgün şekilde biçimlendirilen bir para birimi değerini düzgün şekilde denetleyen bir RegularExpressionValidator ile değiştirerek kullanıcının bir para birimi simgesi girmesine izin verin. Buradaki sorun, bir para birimi değerini doğrulamak için normal ifadenin çok değil ve kültür ayarlarını eklemek isteseyk kod yazmayı gerektirecektir.
3. Doğrulama denetimini tamamen kaldırın ve GridView 'un `RowUpdating` olay işleyicisinde sunucu tarafı doğrulama mantığını kullanın.

Bu alıştırma için #1 seçenek ile başlayalım. Şu anda `UnitPrice`, `EditItemTemplate`: `<%# Bind("UnitPrice", "{0:c}") %>`metin kutusu için veri bağlama ifadesi nedeniyle bir para birimi olarak biçimlendirilir. Bind ifadesini `Bind("UnitPrice", "{0:n2}")`olarak değiştirin, bu da sonucu iki basamaklı bir sayı olarak biçimlendirir. Bu, doğrudan bildirime dayalı sözdizimi aracılığıyla veya `UnitPrice` TemplateField `EditItemTemplate` `EditUnitPrice` metin kutusundan DataBindings düzenle bağlantısına tıklayarak yapılabilir (bkz. Şekil 9 ve 10).

[Metin kutusunun DataBindings bağlantısını düzenle bağlantısına ![tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image25.png)

**Şekil 9**: TextBox 'ın DataBindings bağlantısını Düzenle ' ye tıklayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image27.png))

[Bağlama Ifadesinde biçim belirticisini belirtmek ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image28.png)

**Şekil 10**: `Bind` deyimindeki biçim belirticisini belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image30.png))

Bu değişiklik ile, düzenleme arabirimindeki biçimlendirilen Fiyat, Grup ayırıcısı olarak virgül ve ondalık ayırıcı olarak bir nokta, ancak para birimi sembolünü devre dışı bırakır.

> [!NOTE]
> `UnitPrice` `EditItemTemplate` bir RequiredFieldValidator içermez ve bu geri göndermeye ve güncelleştirme mantığını yorum olarak verir. Bununla birlikte, *ekleme, güncelleştirme ve silme öğreticisi Ile Ilişkili olayları inceledikten* sonra, `RowUpdating` olay işleyicisi, `UnitPrice` sağlanması için programlı bir denetim içerir. Bu mantığı kaldırmak, olduğu gibi bırakmak veya `UnitPrice` `EditItemTemplate`bir RequiredFieldValidator eklemek için ücretsizdir.

## <a name="step-4-summarizing-data-entry-problems"></a>4\. Adım: veri girişi sorunlarını özetleme

ASP.NET, beş doğrulama denetimine ek olarak, geçersiz veri algılayan bu doğrulama denetimlerinin `ErrorMessage` s öğesini görüntüleyen bir [ValidationSummary denetimini](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)içerir. Bu özet verileri Web sayfasında metin olarak veya kalıcı, istemci tarafı MessageBox aracılığıyla görüntülenebilir. Bu öğreticiyi, herhangi bir doğrulama sorununu özetleyen istemci tarafı MessageBox 'i içerecek şekilde geliştirelim.

Bunu gerçekleştirmek için araç kutusu 'ndan tasarımcı üzerine bir ValidationSummary denetimi sürükleyin. Doğrulama denetiminin konumu aslında bir MessageBox olarak yalnızca Özeti görüntüleyecek şekilde yapılandıracağız. Denetim eklendikten sonra [ShowSummary özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) `False` ve [showmessagebox özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) `True`olarak ayarlayın. Bu ek olarak, herhangi bir doğrulama hatası istemci tarafı MessageBox içinde özetlenir.

[![doğrulama hataları, Istemci tarafı MessageBox içinde özetlenir](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image31.png)

**Şekil 11**: doğrulama hataları, Istemci tarafı MessageBox 'da özetlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image33.png))

## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>5\. Adım: DetailsView 'un`InsertItemTemplate` doğrulama denetimlerini ekleme

Bu öğretici için kalan tümü, DetailsView 'un ekleme arabirimine doğrulama denetimleri eklemektir. DetailsView 'un şablonlarına doğrulama denetimleri ekleme işlemi, adım 3 ' te İncelenme ile aynıdır; Bu nedenle, bu adımdaki görevi yeniden seçeceğiz. GridView 'ın `EditItemTemplate` s ile yaptığımız gibi, metin kutularının `ID` ve `InsertProductName` ve `InsertUnitPrice``TextBox1` `TextBox2` yeniden adlandırmanızı öneririz.

`ProductName` `InsertItemTemplate`bir RequiredFieldValidator ekleyin. `ControlToValidate` şablondaki TextBox 'ın `ID`, `Text` özelliğini "\*" olarak ve `ErrorMessage` özelliğini "ürünün adını sağlamalısınız" olarak ayarlayın.

Yeni bir kayıt eklenirken Bu sayfa için `UnitPrice` gerektiğinden, `UnitPrice` `InsertItemTemplate`bir RequiredFieldValidator ekleyin, `ControlToValidate`, `Text`ve `ErrorMessage` özellikleri uygun şekilde ayarlar. Son olarak, `UnitPrice` `InsertItemTemplate` bir CompareValidator ekleyin; `ControlToValidate`, `Text`, `ErrorMessage`, `Type`, `Operator`ve `ValueToCompare` özelliklerini, GridView 'un `UnitPrice``EditItemTemplate`CompareValidator ile yaptığımız gibi yapılandırın.

Bu doğrulama denetimleri eklendikten sonra, adı sağlanmadığında veya fiyatı negatif bir sayı ise veya geçersiz şekilde biçimlendirildiyse sisteme yeni bir ürün eklenemez.

[![doğrulama mantığı, DetailsView 'un ekleme arabirimine eklendi](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image34.png)

**Şekil 12**: bir doğrulama mantığı, DetailsView 'un ekleme arabirimine eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image36.png))

## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>6\. Adım: doğrulama denetimlerini doğrulama gruplarına bölümleme

Sayfamız, iki mantıksal olarak farklı doğrulama denetimi kümesinden oluşur: GridView 'in düzenleyen arabirimine karşılık gelen ve DetailsView 'un ekleme arabirimine karşılık gelen kişiler. Varsayılan olarak, geri gönderme gerçekleştiğinde sayfadaki *Tüm* doğrulama denetimleri denetlenir. Ancak, bir kayıt düzenlenirken, DetailsView 'un ekleme arabiriminin doğrulama denetimlerinin doğrulanmasını istemiyorum. Şekil 13, Kullanıcı kusursuz bir şekilde yasal değerler içeren bir ürünü düzenlemekte olduğunda, ekleme arabirimindeki ad ve fiyat değerleri boş olduğu için güncelleştirme ' ye tıklamak bir doğrulama hatasına neden olur.

[bir ürünü güncelleştirmek ![, ekleme arabiriminin doğrulama denetimlerinin başlatılmasına neden olur](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image37.png)

**Şekil 13**: bir ürünü güncelleştirme, ekleme arabiriminin doğrulama denetimlerinin tetiklenmesine neden olur ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image39.png))

ASP.NET 2,0 ' deki doğrulama denetimleri, `ValidationGroup` özelliği aracılığıyla doğrulama gruplarında bölümlenebilir. Bir gruptaki doğrulama denetimleri kümesini ilişkilendirmek için `ValidationGroup` özelliğini aynı değere ayarlamanız yeterlidir. Öğreticimiz için, GridView 'un templatefields içindeki doğrulama denetimlerinin `ValidationGroup` özelliklerini `EditValidationControls` ve DetailsView 'un TemplateFields `ValidationGroup` özelliklerini `InsertValidationControls`olarak ayarlayın. Bu değişiklikler doğrudan bildirim temelli biçimlendirmede veya tasarımcı düzenleme şablonu arabirimini kullanırken Özellikler penceresi aracılığıyla yapılabilir.

Doğrulama denetimlerine ek olarak, ASP.NET 2,0 ' deki düğme ve düğmeyle ilgili denetimler de `ValidationGroup` özelliği içerir. Doğrulama grubunun Doğrulayıcıları, yalnızca bir geri gönderme işlemi aynı `ValidationGroup` özelliği ayarına sahip bir düğme tarafından oluşturulduğunda geçerliliğini denetledi. Örneğin, DetailsView 'un INSERT düğmesine `InsertValidationControls` doğrulama grubunu tetikleyebilmek için, CommandField 'ın `ValidationGroup` özelliğini `InsertValidationControls` olarak ayarlamanız gerekir (bkz. Şekil 14). Ayrıca, GridView 'un Commandfield'ın `ValidationGroup` özelliğini `EditValidationControls`olarak ayarlayın.

[DetailsView 'un CommandField's ValidationGroup özelliğini ınsertvalidationcontrols olarak ayarlamak ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image40.png)

**Şekil 14**: DetailsView 'un commandfield'ın `ValidationGroup` özelliğini `InsertValidationControls` olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image42.png))

Bu değişikliklerden sonra, DetailsView ve GridView 'un TemplateFields ve CommandFields 'ler şuna benzer olmalıdır:

DetailsView 'un TemplateFields ve CommandField 'ı

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample4.aspx)]

GridView 'un CommandField ve TemplateFields

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample5.aspx)]

Bu noktada, düzenleme özgü doğrulama denetimleri yalnızca GridView 'un Update düğmesine tıklandığında ve ekleme özgü doğrulama denetimleri yalnızca DetailsView 'un INSERT düğmesine tıklandığında harekete geçirerek, Şekil 13 ' te vurgulanan sorunu çözer. Ancak, bu değişiklik ile geçersiz veri girerken ValidationSummary denetimizin artık görüntülenmez. ValidationSummary denetimi bir `ValidationGroup` özelliği de içerir ve yalnızca doğrulama grubundaki bu doğrulama denetimlerine ait Özet bilgileri gösterir. Bu nedenle, biri `InsertValidationControls` doğrulama grubu ve diğeri `EditValidationControls`olmak üzere bu sayfada iki doğrulama denetimine sahip olmanız gerekir.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample6.aspx)]

Bu ek sayesinde öğreticimiz tamamlanmıştır!

## <a name="summary"></a>Özet

BoundFields hem ekleme hem de oluşturma arabirimi sağlayaken, arabirim özelleştirilemez. Genellikle, kullanıcının gerekli girişleri yasal bir biçimde girdiğinden emin olmak için Düzenle ve ekleme arabirimine doğrulama denetimleri eklemek istiyoruz. Bunu gerçekleştirmek için, BoundFields alanlarını TemplateFields 'e dönüştürmeniz ve doğrulama denetimlerini uygun şablona eklemesi gerekir. Bu öğreticide, hem DetailsView 'un ekleme arabirimine hem de GridView 'ın düzenleyen arabirimine doğrulama denetimleri ekleyerek, öğreticiyi ekleme *, güncelleştirme ve silme Ile Ilişkili olayları inceledikten* sonra gelen örneği genişlettik. Üstelik, ValidationSummary denetimini kullanarak Özet doğrulama bilgilerinin nasıl görüntüleneceğini ve sayfadaki doğrulama denetimlerinin ayrı doğrulama gruplarına nasıl bölümleyeceğinize de gördük.

Bu öğreticide gördüğümüz gibi, TemplateFields, denetim ve ekleme arabirimlerinin, doğrulama denetimlerini içerecek şekilde artırılmasına izin verir. TemplateFields ayrıca ek giriş Web denetimleri içerecek şekilde genişletilebilir ve metin kutusu, daha uygun bir Web denetimiyle değiştirilmesini sağlar. Bir sonraki öğreticimizde, bir yabancı anahtar (`CategoryID` veya `Products` tablosundaki `SupplierID` gibi) düzenlenirken ideal olan bir veri bağlantılı DropDownList denetimiyle metin kutusu denetiminin nasıl değiştirileceğini öğreneceksiniz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Liz Shulok ve Zack Jones. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
> [İleri](customizing-the-data-modification-interface-vb.md)
