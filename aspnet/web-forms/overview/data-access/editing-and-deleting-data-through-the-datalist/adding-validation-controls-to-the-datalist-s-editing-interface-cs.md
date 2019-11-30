---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-cs
title: DataList 'in düzenleyen arabirimine doğrulama denetimleri ekleme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, daha fazla folipop Kullanıcı int düzenlemesi sağlamak için DataList 'in EditItemTemplate 'e doğrulama denetimleri eklemenin ne kadar kolay olduğunu görüyoruz.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 3ecc21c5-da0e-40ab-abb4-fac1e47398ad
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: e3c14b7098da832bd28f57026e81dcb7f7ba7130
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640492"
---
# <a name="adding-validation-controls-to-the-datalists-editing-interface-c"></a>DataList’in Düzenleme Arabirimine Doğrulama Denetimleri Ekleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_CS.exe) veya [PDF 'yi indirin](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/datatutorial39cs1.pdf)

> Bu öğreticide, daha fazla folipop düzenlemesi Kullanıcı arabirimi sağlamak için DataList 'in EditItemTemplate 'e doğrulama denetimleri eklemenin ne kadar kolay olduğunu görüyoruz.

## <a name="introduction"></a>Giriş

DataList 'in bu öğreticilerde şu ana kadar, eksik ürün adı veya negatif fiyat gibi geçersiz kullanıcı girişi bir özel durumla sonuçlansa da, veri alanı, düzenlemenin düzenlemesi, hiçbir öngörülü Kullanıcı giriş doğrulaması içermez. [Önceki öğreticide](handling-bll-and-dal-level-exceptions-cs.md) , oluşturulan özel durumlarla ilgili bilgileri yakalamak ve düzgün şekilde göstermek Için, DataList s `UpdateCommand` olay işleyicisine özel durum işleme kodu eklemeyi inceledik. Bununla birlikte, düzen arabirimi, bir kullanıcının ilk yere bu tür verileri girmesini engellemek için doğrulama denetimlerini içerir.

Bu öğreticide, daha fazla folipop düzenlemesi Kullanıcı arabirimi sağlamak için, DataList s `EditItemTemplate` doğrulama denetimleri eklemenin ne kadar kolay olduğunu görüyoruz. Özellikle, bu öğretici önceki öğreticide oluşturulan örneği alır ve uygun doğrulamayı dahil etmek için Düzenle arabirimini genişlettiğini.

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptionshandling-bll-and-dal-level-exceptions-csmd"></a>Adım 1: örneği[BLL ve dal düzeyi özel durumları Işlemeye](handling-bll-and-dal-level-exceptions-cs.md) çoğaltma

[BLL ve dal düzeyi özel durumları işleme](handling-bll-and-dal-level-exceptions-cs.md) öğreticisinde, ürünlerin adlarını ve fiyatlarını iki sütunlu, düzenlenebilir bir DataList içinde listeleyen bir sayfa oluşturduk. Bu öğreticide bizim amamız,, doğrulama denetimlerini dahil etmek için DataList s Editing arabirimini artırmak içindir. Özellikle, doğrulama mantığımız şunları sağlayacak:

- Ürün adının sağlanması gerekiyor
- Fiyat için girilen değerin geçerli bir para birimi biçimi olduğundan emin olun
- Negatif `UnitPrice` değeri geçersiz olduğundan, Fiyat için girilen değerin sıfıra eşit veya sıfırdan büyük olduğundan emin olun

Doğrulama eklemek için önceki örneği genişletmenin artırılmasına bakabilmeniz için önce, Bu öğreticinin `EditDeleteDataList` klasöründeki `ErrorHandling.aspx` sayfasından örneği çoğaltmamız gerekir `UIValidation.aspx`. Bunu elde etmek için `ErrorHandling.aspx` sayfa temelli biçimlendirme ve onun kaynak kodunu kopyalamanız gerekir. İlk olarak, aşağıdaki adımları gerçekleştirerek bildirim temelli biçimlendirmenin üzerine kopyalayın:

1. Visual Studio 'da `ErrorHandling.aspx` sayfasını açın
2. Sayfa bildirim temelli işaretleme sayfasına gidin (sayfanın altındaki kaynak düğmesine tıklayın)
3. Şekil 1 ' de gösterildiği gibi, `<asp:Content>` metni ve `</asp:Content>` etiketleri (3 ile 32 arasındaki satırlar) kopyalayın.

[&lt;ASP: Content&gt; Control Içindeki metni kopyalamak ![](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image1.png)

**Şekil 1**: `<asp:Content>` denetiminin içindeki metni kopyalama ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image3.png))

1. `UIValidation.aspx` sayfasını açın
2. Sayfa bildirim temelli işaretleme sayfasına gidin
3. `<asp:Content>` denetiminin içindeki metni yapıştırın.

Kaynak kodu üzerine kopyalamak için `ErrorHandling.aspx.vb` sayfasını açın ve yalnızca `EditDeleteDataList_ErrorHandling` sınıfının *içindeki* metni kopyalayın. `DisplayExceptionDetails` yöntemiyle birlikte üç olay işleyicisini (`Products_EditCommand`, `Products_CancelCommand`ve `Products_UpdateCommand`) kopyalayın, ancak sınıf bildirimini veya `using` deyimlerini **kopyalamayın.** Kopyalanmış *metni `UIValidation.aspx.vb`içindeki `EditDeleteDataList_UIValidation`* sınıfında yapıştırın.

`ErrorHandling.aspx` içerik ve kod üzerinden `UIValidation.aspx`' a taşıdıktan sonra, bir tarayıcıda sayfaları test etmek için bir dakikanızı ayırın. Aynı çıktıyı görmeniz ve bu iki sayfanın her birinde aynı işlevleri deneymelisiniz (bkz. Şekil 2).

[Uıvalidation. aspx sayfası ![ErrorHandling. aspx içindeki Işlevselliği taklit eder](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image4.png)

**Şekil 2**: `UIValidation.aspx` sayfası `ErrorHandling.aspx` işlevleri taklit eder ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image6.png))

## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>2\. Adım: doğrulama denetimlerini DataList s EditItemTemplate 'e ekleme

Veri girişi formları oluştururken, kullanıcıların gerekli alanları girmesi ve tüm sağlanmış girişlerinin yasal, düzgün biçimli değerler olması önemlidir. ASP.NET bir Kullanıcı girişinin geçerli olduğundan emin olmak için, tek bir giriş Web denetiminin değerini doğrulamak üzere tasarlanan beş yerleşik doğrulama denetimi sağlar:

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) bir değer sağlanmış olmasını sağlar
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) bir değeri başka bir Web denetim değeri veya sabit bir değere göre doğrular ya da değer s biçiminin belirtilen veri türü için geçerli olmasını sağlar
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) , bir değerin bir değer aralığı içinde olmasını sağlar
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) bir değeri [normal bir ifadeye](http://en.wikipedia.org/wiki/Regular_expression) doğrular
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) bir değeri özel, Kullanıcı tanımlı bir yönteme göre doğrular

Bu beş denetim hakkında daha fazla bilgi için, [doğrulama denetimlerini ekleme ve ekleme arabirim](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) öğreticisine geri dönüp [ASP.net hızlı başlangıç öğreticilerinin](https://quickstarts.asp.net) [doğrulama denetimleri bölümüne](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx) bakın.

Öğreticimiz için bir RequiredFieldValidator kullanarak, girilen fiyatın 0 ' dan büyük veya sıfıra eşit bir değere sahip olduğundan ve geçerli bir para birimi biçiminde sunulduğundan emin olmak için bir RequiredFieldValidator kullanması gerekir.

> [!NOTE]
> ASP.NET 1. x aynı beş doğrulama denetimine sahip olduğundan, ASP.NET 2,0, Internet Explorer 'a ek olarak tarayıcılar için ana iki istemci tarafı betik desteği ve bir sayfadaki doğrulama denetimlerini bölümleyebilme olanağı sunan bir dizi iyileştirme ekledi. doğrulama grupları. 2,0 sürümündeki yeni doğrulama denetimi özellikleri hakkında daha fazla bilgi için, [ASP.NET 2,0 ' de doğrulama denetimlerinin nasıl dağlamadiğini](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)inceleyin.

Gerekli doğrulama denetimlerini DataList s `EditItemTemplate`ekleyerek başlayalım. Bu görev tasarımcı aracılığıyla DataList 'in akıllı etiketindeki Şablonları Düzenle bağlantısına tıklayarak ya da bildirime dayalı sözdizimi aracılığıyla gerçekleştirilebilir. Tasarım görünümü Şablonları Düzenle seçeneğini kullanarak süreç boyunca ilerme. DataList s `EditItemTemplate`düzenlemeyi seçtikten sonra, araç kutusundan şablon düzenleme arabirimine sürükleyerek bir RequiredFieldValidator ekleyin ve bunu `ProductName` metin kutusundan sonra koyun.

[ProductName metin kutusu 'ndan sonra EditItemTemplate 'e bir RequiredFieldValidator eklemek ![](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image7.png)

**Şekil 3**: `ProductName` metin kutusuna `EditItemTemplate After` bir RequiredFieldValidator ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image9.png))

Tüm doğrulama denetimleri, tek bir ASP.NET Web denetiminin girişini doğrulayarak çalışır. Bu nedenle, yeni eklediğimiz bir RequiredFieldValidator `ProductName` metin kutusuna göre doğrulamanız gerekir; Bu işlem, doğrulama denetimi [`ControlToValidate` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) uygun Web denetiminin `ID` (`ProductName`, bu örnekte) ayarlanarak yapılır. Sonra, [`ErrorMessage` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) olarak ayarlayın \*için ürün adı ve [`Text` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) sağlamanız gerekir. Sağlanırsa `Text` Özellik değeri, doğrulama başarısız olursa doğrulama denetimi tarafından görüntülenen metindir. Gerekli `ErrorMessage` Özellik değeri, ValidationSummary denetimi tarafından kullanılır; `Text` Özellik değeri atlanırsa, `ErrorMessage` özelliği değeri geçersiz giriş üzerinde doğrulama denetimi tarafından görüntülenir.

Bu üç RequiredFieldValidator özelliğini ayarladıktan sonra, ekranınızın Şekil 4 ' e benzer olması gerekir.

[![ControlToValidate, ErrorMessage ve Text özelliklerini ayarlama](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image10.png)

**Şekil 4**: RequiredFieldValidator s `ControlToValidate`, `ErrorMessage`ve `Text` özelliklerini ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image12.png))

RequiredFieldValidator `EditItemTemplate`eklendiğinde, her şey, ürün için fiyat metin kutusu için gerekli doğrulamayı eklemektir. Kayıt düzenlenirken `UnitPrice` isteğe bağlı olduğundan, bir RequiredFieldValidator eklemesi gerekmez. Ancak, sağlanan `UnitPrice`, bir para birimi olarak düzgün biçimlendirildiğinden ve 0 ' dan büyük veya buna eşit olduğundan emin olmak için bir CompareValidator eklemesi gerekir.

`EditItemTemplate` CompareValidator ekleyin ve `ControlToValidate` özelliğini `UnitPrice`olarak ayarlayın, `ErrorMessage` özelliği, sıfıra eşit veya daha büyük olmalı ve para birimi sembolünü ve `Text` özelliğini \*öğesine içermemelidir. `UnitPrice` değerin 0 ' dan büyük veya 0 ' a eşit olması gerektiğini belirtmek için, CompareValidator s [`Operator` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) `GreaterThanEqual`, [`ValueToCompare` özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) 0 ve [`Type` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) `Currency`olarak ayarlayın.

Bu iki doğrulama denetimi eklendikten sonra, DataList s `EditItemTemplate` bildirim temelli sözdizimi şuna benzer olmalıdır:

[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

Bu değişiklikleri yaptıktan sonra sayfayı bir tarayıcıda açın. Bir ürünü düzenlenirken adı atlamaya veya geçersiz bir fiyat değeri girmeye çalışırsanız, TextBox ' ın yanında bir yıldız işareti görünür. Şekil 5 ' te gösterildiği gibi, $19,95 gibi para birimi sembolünü içeren bir fiyat değeri geçersiz sayılır. CompareValidator s `Currency` `Type`, basamak ayırıcılarına (kültür ayarlarına bağlı olarak virgüller veya noktalar gibi), önde gelen artı veya eksi işaretiyle izin verir, ancak para birimi simgesine izin *vermez* . Bu davranış, Düzenle arabirimi olarak Kullanıcı tarafından, `UnitPrice` para birimi biçimini kullanarak şu anda bir şekilde işler.

[![, geçersiz girişi olan metin kutularının yanında bir yıldız Işareti görünür](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image13.png)

**Şekil 5**: geçersiz giriş metin kutularının yanında bir yıldız işareti görünür ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image15.png))

Doğrulama olduğu gibi çalışırken, kullanıcının kabul edilebilir olmayan bir kaydı düzenlenirken para birimi sembolünü el ile kaldırması gerekir. Üstelik, düzen arabiriminde geçersiz girişler varsa, tıklatıldığında, bir geri gönderme Işlemini çağırır. İdeal olarak, Iptal düğmesi, Kullanıcı girişlerinin geçerliliğini ne olursa olsun, DataList 'i önceden düzenlenen durumuna döndürür. Ayrıca, DataList s `UpdateCommand` olay işleyicisinde ürün bilgilerini güncelleştirmeden önce sayfa verilerinin geçerli olduğundan emin olunması gerekir, çünkü doğrulama denetimleri istemci tarafı mantığı, tarayıcıları JavaScript desteklemeyen veya desteğinin devre dışı bırakıldığı kullanıcılar tarafından atlanabilir.

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>EditItemTemplate s UnitPrice metin kutusundan para birimi sembolünü kaldırma

CompareValidator s `Currency``Type`kullanılırken, doğrulanan giriş herhangi bir para birimi sembolü içermemelidir. Bu tür simgelerin varlığı, CompareValidator girişi geçersiz olarak işaretlamasına neden olur. Ancak, düzen arabirimimiz Şu anda `UnitPrice` metin kutusunda bir para birimi simgesi içermektedir, yani Kullanıcı, değişiklikleri kaydetmeden önce para birimi sembolünü açıkça kaldırmalıdır. Bu sorunu gidermek için üç seçenek vardır:

1. `EditItemTemplate`, `UnitPrice` metin kutusu değerinin para birimi olarak biçimlendirilmemesi için yapılandırın.
2. CompareValidator öğesini kaldırarak ve düzgün şekilde biçimlendirilen bir para birimi değerini denetleyen bir RegularExpressionValidator ile değiştirerek kullanıcının bir para birimi simgesi girmesine izin verin. Buradaki zorluk, bir para birimi değerini doğrulamak için normal ifadenin CompareValidator kadar basit olmadığını ve kültür ayarlarını eklemek isteseyk kod yazmayı gerektirmektir.
3. Doğrulama denetimini tamamen kaldırın ve GridView s `RowUpdating` olay işleyicisinde özel sunucu tarafı doğrulama mantığına güvenin.

Bu öğretici için 1. seçenek ile başlayalım. Şu anda `UnitPrice`, `EditItemTemplate`: `<%# Eval("UnitPrice", "{0:c}") %>`metin kutusu için veri bağlama ifadesi nedeniyle bir para birimi değeri olarak biçimlendirilir. `Eval` ifadesini `Eval("UnitPrice", "{0:n2}")`olarak değiştirin, bu sonucu iki basamaklı bir sayı olarak biçimlendirir. Bu, doğrudan bildirim temelli söz dizimi aracılığıyla veya DataList s `EditItemTemplate``UnitPrice` metin kutusundan DataBindings düzenle bağlantısına tıklayarak yapılabilir.

Bu değişiklik ile, düzenleme arabirimindeki biçimlendirilen Fiyat, Grup ayırıcısı olarak virgül ve ondalık ayırıcı olarak bir nokta, ancak para birimi sembolünü devre dışı bırakır.

> [!NOTE]
> Para birimi biçimi düzenlenebilir arabirimden kaldırılırken, para birimi sembolünü metin kutusu dışına metin olarak yerleştirmek yararlı buldum. Bu, kullanıcıya para birimi sembolünü sağlamamaları gerekmeyen bir ipucu görevi görür.

## <a name="fixing-the-cancel-button"></a>Iptal düğmesini Düzeltme

Varsayılan olarak, doğrulama Web denetimleri, istemci tarafında doğrulama gerçekleştirmek için JavaScript yayar. Bir düğme, LinkButton veya ImageButton tıklandığında, geri gönderme gerçekleşmeden önce sayfadaki doğrulama denetimleri istemci tarafında denetlenir. Geçersiz veriler varsa, geri gönderme iptal edilir. Ancak bazı düğmeler için, verilerin geçerliliği imse olabilir; Böyle bir durumda, geri gönderimin geçersiz veriler nedeniyle iptal edilmesi gerekir.

Iptal düğmesi böyle bir örnektir. Kullanıcının ürün adını atlayarak geçersiz veriler girdiğini düşünün ve sonra ürünü kaydetmek ve Iptal düğmesine isabet etmek istemiyorum. Şu anda, Iptal düğmesi sayfadaki doğrulama denetimlerini tetikler, bu da ürün adının eksik olduğunu ve geri göndermeyi önler. Kullanıcı, `ProductName` metin kutusuna bazı metinleri yazarak yalnızca, düzen işlemini iptal eder.

Neyse ki Button, LinkButton ve ImageButton, düğmenin tıklanmasının (varsayılan olarak `True`) gerekip gerekmediğini gösterebilen bir [`CausesValidation` özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx) sahiptir. Iptal düğmesine `CausesValidation` özelliğini `False`olarak ayarlayın.

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>Girdilerin UpdateCommand olay Işleyicide geçerli olduğundan emin olma

Doğrulama denetimleri tarafından oluşturulan istemci tarafı komut dosyası nedeniyle, bir Kullanıcı geçersiz giriş girerse, doğrulama denetimleri, `CausesValidation` özellikleri `True` (varsayılan) olan ImageButton veya ImageButton denetimleriyle başlatılan geri göndermeler iptal eder. Ancak, bir Kullanıcı, kötü bir tarayıcıyla veya JavaScript desteğinin devre dışı bırakıldığı bir tarayıcı ile ziyaret ediyorsanız, istemci tarafı doğrulama denetimleri yürütülmez.

Tüm ASP.NET doğrulama denetimleri, geri gönderme sonrasında doğrulama mantığını hemen yineler ve [`Page.IsValid` özelliği](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx)aracılığıyla sayfa s girişlerinin genel geçerliliğini raporlar. Ancak, sayfa akışı `Page.IsValid`değerine göre hiçbir şekilde kesintiye uğramaz veya durdurulmaz. Geliştirici olarak, `Page.IsValid` özelliğinin geçerli giriş verilerini varsayan kodla devam etmeden önce `True` bir değere sahip olduğundan emin olmak bizim sorumluluğunuzdadır.

Bir kullanıcının JavaScript devre dışı olması durumunda sayfamızı ziyaret eder, bir ürünü düzenler, çok pahalı bir fiyat değeri girer ve Güncelleştir düğmesine tıkladığında, istemci tarafı doğrulaması atlanır ve geri gönderme işlemi yapılır. Geri göndermede, ASP.NET Page s `UpdateCommand` olay işleyicisi yürütülür ve bir özel durum, bir `Decimal`çok pahalı bir şekilde ayrıştırılmaya çalışıldığında oluşur. Özel durum işleme yaptığımız için, böyle bir özel durum düzgün şekilde işlenecektir, ancak yalnızca `Page.IsValid` `True`bir değere sahipse, yalnızca `UpdateCommand` olay işleyicisine devam ederek, geçersiz verilerin ilk yerinde gezinmelerini engelleyebiliriz.

Aşağıdaki kodu, `Try` bloğundan hemen önce `UpdateCommand` olay işleyicisinin başlangıcına ekleyin:

[!code-csharp[Main](adding-validation-controls-to-the-datalist-s-editing-interface-cs/samples/sample2.cs)]

Bu ek olarak, ürün yalnızca gönderilen veriler geçerliyse güncelleştirilmesini deneyecektir. Çoğu Kullanıcı, doğrulama denetimleri istemci tarafı betikleri nedeniyle geçersiz verileri geri gönderemeyecek, ancak tarayıcıları JavaScript 'ı desteklemeyen veya JavaScript desteği devre dışı olan kullanıcılar, istemci tarafı denetimlerini atlayabilir ve geçersiz veriler gönderebilir.

> [!NOTE]
> Kurnaz okuyucusu GridView ile verileri güncelleştirirken, sayfa s arka plan kod sınıfımızda `Page.IsValid` özelliğini açıkça denetmamız gerekmedik. Bunun nedeni, GridView 'un `Page.IsValid` özelliğini bizimle danışmansı ve yalnızca bir `True`değeri döndürürse yalnızca güncelleştirme ile devam eder.

## <a name="step-3-summarizing-data-entry-problems"></a>3\. Adım: veri girişi sorunlarını özetleme

ASP.NET, beş doğrulama denetimine ek olarak, geçersiz veri algılayan bu doğrulama denetimlerinin `ErrorMessage` s öğesini görüntüleyen bir [ValidationSummary denetimini](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)içerir. Bu özet verileri Web sayfasında metin olarak veya kalıcı, istemci tarafı MessageBox aracılığıyla görüntülenebilir. Her türlü doğrulama sorununu özetleyen bir istemci tarafı MessageBox eklemek için bu öğreticiyi geliştirelim.

Bunu gerçekleştirmek için araç kutusu 'ndan tasarımcı üzerine bir ValidationSummary denetimi sürükleyin. Yalnızca Özeti bir MessageBox olarak görüntüleyecek şekilde yapılandırdığımız için ValidationSummary denetiminin konumu oldukça önemlidir. Denetim eklendikten sonra, [`ShowSummary` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) `False` ve [`ShowMessageBox` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) `True`olarak ayarlayın. Bu ek olarak, herhangi bir doğrulama hatası istemci tarafı MessageBox içinde özetlenir (bkz. Şekil 6).

[![doğrulama hataları, Istemci tarafı MessageBox içinde özetlenir](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image16.png)

**Şekil 6**: doğrulama hataları, Istemci tarafı MessageBox 'da özetlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image18.png))

## <a name="summary"></a>Özet

Bu öğreticide, Kullanıcı girdilerimizin güncelleştirme iş akışında kullanmayı denemeden önce geçerli olduğundan emin olmak için doğrulama denetimlerini kullanarak özel durumlar olasılığını nasıl azaltabiliriz. ASP.NET, belirli bir Web denetimi girişini incelemek ve giriş s geçerliliğini raporlamak için tasarlanan beş doğrulama Web denetimi sağlar. Bu öğreticide, ürün adının sağlandığından ve fiyatın sıfıra eşit veya sıfırdan büyük bir para birimi biçimine sahip olduğundan emin olmak için, bu beş bu beş denetimin iki denetimini kullandık.

DataList s Editing arabirimine doğrulama denetimleri eklemek, araç kutusundan `EditItemTemplate` sürüklemek ve çok sayıda özelliği ayarlamak kadar basittir. Varsayılan olarak, doğrulama denetimleri istemci tarafı doğrulama betiğini otomatik olarak yayar; Ayrıca, toplu sonucu `Page.IsValid` özelliğinde depolayarak, geri gönderme sırasında sunucu tarafı doğrulaması da sağlar. Bir Button, LinkButton veya ImageButton tıklandığında istemci tarafı doğrulamayı atlamak için düğme s `CausesValidation` özelliğini `False`olarak ayarlayın. Ayrıca, geri göndermede gönderilen verilerle herhangi bir görev yapmadan önce, `Page.IsValid` özelliğinin `True`döndürdüğünden emin olun.

Şimdiye kadar incelediğimiz tüm DataList Editing öğreticileri, ürün adı ve diğeri için bir metin kutusu olan çok basit bir Düzenle arabirimine sahipti. Ancak, düzen arabirimi, DropDownLists, takvimler, RadioButtons, CheckBox 'lar vb. gibi farklı Web denetimlerinin bir karışımını içerebilir. Bir sonraki öğreticimizde, çeşitli Web denetimleri kullanan bir arabirim oluşturmaya bakacağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticiye yönelik müşteri adayı gözden geçirenler dennıs Patterson, Ken ön PISA ve Liz Shulok. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](handling-bll-and-dal-level-exceptions-cs.md)
> [İleri](customizing-the-datalist-s-editing-interface-cs.md)
