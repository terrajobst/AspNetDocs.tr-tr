---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
title: BLL ve DAL düzeyi özel durumları işleme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, düzenlenebilir bir DataList 'in güncelleştirme iş akışı sırasında oluşturulan özel durumları nasıl ele aldığımızda görüyoruz.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: ca665073-b379-4239-9404-f597663ca65e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: 319ab44f2e65afc77f6f89ca8aa58c529f40d05c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78593669"
---
# <a name="handling-bll--and-dal-level-exceptions-vb"></a>BLL ve DAL Düzeyi Özel Durumları İşleme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_VB.exe) veya [PDF 'yi indirin](handling-bll-and-dal-level-exceptions-vb/_static/datatutorial38vb1.pdf)

> Bu öğreticide, düzenlenebilir bir DataList 'in güncelleştirme iş akışı sırasında oluşturulan özel durumları nasıl ele aldığımızda görüyoruz.

## <a name="introduction"></a>Giriş

DataList öğreticisinde [verileri düzenlemeyle ve silmeye genel bakış](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md) bölümünde, basit düzenlemeler ve silme özellikleri sunan bir DataList oluşturduk. Tam işlevsel olsa da, düzen veya silme işlemi sırasında oluşan herhangi bir hata işlenmemiş bir özel durumla sonuçlandığı için Kullanıcı dostu hale geldi. Örneğin, ürün adını atlama veya bir ürünü düzenlediğinizde, çok ekonomik bir fiyat değeri girilmesi, bir özel durum oluşturur. Bu özel durum kodda yakalanmadığından, ASP.NET çalışma zamanına kadar kabarcıklar, daha sonra özel durum s ayrıntılarını Web sayfasında görüntüler.

[Bir ASP.NET sayfa öğreticisindeki BLL ve dal düzeyi özel durumları işleme](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) bölümünde gördüğünüz gibi, iş mantığı veya veri erişim katmanlarının derinliğinden bir özel durum ortaya çıktığında, özel durum ayrıntıları ObjectDataSource 'a ve ardından GridView 'a döndürülür. Bu özel durumları, ObjectDataSource veya GridView için `Updated` ya da `RowUpdated` olay işleyicileri oluşturarak, bir özel durum olup olmadığını ve özel durumun işlendiğini belirten bir şekilde nasıl işleyeceğinizi gördük.

Ancak, DataList öğreticilerimiz, verileri güncelleştirmek ve silmek için ObjectDataSource 'u kullanmıyor. Bunun yerine, doğrudan BLL 'ye karşı çalışıyoruz. BLL veya DAL kaynaklı özel durumları algılamak için, ASP.NET sayfamıza ait arka plan kodu içinde özel durum işleme kodu uygulamamız gerekir. Bu öğreticide, düzenlenebilir bir DataList s güncelleştirme iş akışı sırasında oluşturulan özel durumları daha fazla ele alma hakkında bilgi edineceksiniz.

> [!NOTE]
> DataList öğreticisindeki *verileri düzenlemeyle ve silmeye genel bir bakış* içinde, güncelleştiren ve Silinmede bir ObjectDataSource Ile ilgili bazı teknikler, DataList 'ten veri düzenlemeyle ve silinirken farklı teknikler tartışıyoruz. Bu teknikleri kullandıysanız, BLL veya DAL içinden özel durumları, ObjectDataSource s `Updated` veya `Deleted` olay işleyicileri aracılığıyla işleyebilirsiniz.

## <a name="step-1-creating-an-editable-datalist"></a>1\. Adım: düzenlenebilir bir DataList oluşturma

Güncelleştirme iş akışı sırasında oluşan özel durumları işlemeye endişelenmeden önce, ilk olarak düzenlenebilir bir DataList oluşturalım. `EditDeleteDataList` klasöründeki `ErrorHandling.aspx` sayfasını açın, tasarımcıya bir DataList ekleyin, `ID` özelliğini `Products`olarak ayarlayın ve `ProductsDataSource`adlı yeni bir ObjectDataSource ekleyin. ObjectDataSource, kayıt seçmek için `ProductsBLL` sınıf s `GetProducts()` metodunu kullanacak şekilde yapılandırın; INSERT, UPDATE ve DELETE sekmelerindeki açılan listeleri (None) olarak ayarlayın.

[![GetProducts () yöntemini kullanarak ürün bilgilerini döndürün](handling-bll-and-dal-level-exceptions-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-vb/_static/image1.png)

**Şekil 1**: `GetProducts()` yöntemini kullanarak ürün bilgilerini döndürün ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-vb/_static/image3.png))

ObjectDataSource Sihirbazı 'nı tamamladıktan sonra Visual Studio, DataList için otomatik olarak bir `ItemTemplate` oluşturur. Bunu, her ürün adını ve fiyatını görüntüleyen ve bir Düzenle düğmesi içeren bir `ItemTemplate` değiştirin. Ardından, ad ve fiyat ve güncelleştirme ve Iptal düğmeleri için TextBox Web denetimiyle bir `EditItemTemplate` oluşturun. Son olarak, DataList s `RepeatColumns` özelliğini 2 olarak ayarlayın.

Bu değişikliklerden sonra, sayfanızın bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir. Düzenleme, Iptal ve güncelleştirme düğmelerinin `CommandName` özelliklerinin sırasıyla düzenleme, Iptal etme ve güncelleştirme olarak ayarlanmış olduğundan emin olmak için çift işaretleyin.

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample1.aspx)]

> [!NOTE]
> Bu öğreticide, DataList s görünüm durumu etkinleştirilmelidir.

Bir tarayıcıdan ilerleme durumunu görüntülemek için bir dakikanızı ayırın (bkz. Şekil 2).

[![her ürün bir düzenleme düğmesi Içerir](handling-bll-and-dal-level-exceptions-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-vb/_static/image4.png)

**Şekil 2**: her ürün bir düzenleme düğmesi içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-vb/_static/image6.png))

Şu anda Düzenle düğmesi yalnızca bir geri göndermeye neden olur ancak ürünü düzenlenebilir hale getirir. Düzenlemesini etkinleştirmek için, DataList s `EditCommand`, `CancelCommand`ve `UpdateCommand` olayları için olay işleyicileri oluşturuyoruz. `EditCommand` ve `CancelCommand` olaylar, DataList s `EditItemIndex` özelliğini güncelleştirip verileri DataList 'e yeniden bağlamasını sağlar:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample2.vb)]

`UpdateCommand` olay işleyicisi biraz daha karmaşıktır. `DataKeys` koleksiyonundan düzenlenen ürün `ProductID`, `EditItemTemplate`metin kutularına ürün adı ve fiyat ile birlikte okuması gerekir ve DataList 'i düzenleme öncesi durumuna döndürmeden önce `ProductsBLL` Class s `UpdateProduct` yöntemini çağırır.

Şimdilik, DataList öğreticisindeki *verileri düzenlemenin ve silmenin genel bakış* bölümünde yalnızca `UpdateCommand` olay işleyicisindeki tam olarak aynı kodu kullanalım. 2\. adımdaki özel durumları düzgün bir şekilde işlemek için kodu ekleyeceğiz.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample3.vb)]

Hatalı biçimli bir birim fiyatı,-$5,00 gibi geçersiz bir birim fiyatı değeri veya ürün adının atlanmasından kaynaklanan geçersiz bir giriş olduğunda, bir özel durum oluşturulur. `UpdateCommand` olay işleyicisi bu noktada herhangi bir özel durum işleme kodu içermediğinden, özel durum ASP.NET çalışma zamanına kadar kabarcığa alınır ve burada son kullanıcıya gösterilir (bkz. Şekil 3).

![Işlenmeyen bir özel durum oluştuğunda, Son Kullanıcı bir hata sayfası görür](handling-bll-and-dal-level-exceptions-vb/_static/image7.png)

**Şekil 3**: Işlenmeyen bir özel durum oluştuğunda, Son Kullanıcı bir hata sayfası görür

## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>2\. Adım: UpdateCommand olay Işleyicisindeki özel durumları düzgün şekilde Işleme

Güncelleştirme iş akışı sırasında, `UpdateCommand` olay işleyicisi, BLL veya DAL içinde özel durumlar oluşabilir. Örneğin, bir Kullanıcı çok pahalı bir fiyat girerse, `UpdateCommand` olay işleyicisindeki `Decimal.Parse` ifade bir `FormatException` özel durumu oluşturur. Kullanıcı ürün adını atlar veya fiyatın negatif bir değeri varsa, DAL bir özel durum yükseltir.

Bir özel durum oluştuğunda, sayfanın kendisi içinde bilgilendirici bir ileti görüntülenmesini istiyoruz. `ID` `ExceptionDetails`olarak ayarlanan sayfaya bir etiket Web denetimi ekleyin. Etiket s metnini, `Styles.css` dosyasında tanımlanan `Warning` CSS sınıfına `CssClass` özelliğini atayarak kırmızı, çok büyük, kalın ve italik yazı tipinde görüntülenecek şekilde yapılandırın.

Bir hata oluştuğunda, yalnızca etiketin bir kez görüntülenmesini istiyoruz. Diğer bir deyişle, sonraki geri göndermelerde, etiket s uyarı iletisi kaybolmalıdır. Bu, etiket s `Text` özelliği ya da `Visible` özelliğinin `Page_Load` olay işleyicisindeki `False` ( [bir ASP.NET sayfa öğreticisindeki BLL-ve dal düzeyindeki özel durumları işleme](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) geri aldığımız gibi) veya etiket s görünüm durumu desteğini devre dışı bırakarak gerçekleştirilebilir. Bu, ikinci seçeneği kullanalım.

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample4.aspx)]

Bir özel durum ortaya çıktığında, özel durumun ayrıntılarını `ExceptionDetails` Label Control s `Text` özelliğine atayacağız. Görünüm durumu devre dışı olduğundan, sonraki geri göndermeler için `Text` özelliği, programlı değişiklikler kaybedilir, varsayılan metne geri döndürülüyor (boş bir dize), böylece uyarı iletisi gizler.

Sayfada faydalı bir ileti görüntülenmesi için bir hata ortaya çıktığında, `UpdateCommand` olay işleyicisine `Try ... Catch` bir blok eklememiz gerekir. `Try` bölümü bir özel duruma neden olabilecek kodu içerir, ancak `Catch` bloğu bir özel durumun tarafında yürütülen kodu içerir. `Try ... Catch` bloğu hakkında daha fazla bilgi için .NET Framework belgelerindeki [özel durum Işleme temelleri](https://msdn.microsoft.com/library/2w8f0bss.aspx) bölümüne göz atın.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample5.vb)]

`Try` bloğundaki kod tarafından herhangi bir tür özel durum oluşturulduğunda, `Catch` blok kodu yürütülmeye başlayacaktır. Oluşturulan özel durumun türü `DbException`, `NoNullAllowedException`, `ArgumentException`, vb., ilk yerde hatanın tam olarak precipitated bağlıdır. Veritabanı düzeyinde bir sorun varsa, bir `DbException` oluşturulur. `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`veya `ReorderLevel` alanları için geçersiz bir değer girilirse, `ArgumentException` sınıfında bu alan değerlerini doğrulamak için kod eklediğimiz için bir `ProductsDataTable` oluşturulur (bkz. [Iş mantığı katmanı oluşturma](../introduction/creating-a-business-logic-layer-vb.md) Öğreticisi).

İleti metnini yakalanan özel durum türüne dayandırarak son kullanıcıya daha yararlı bir açıklama sağlayabiliriz. [Bir ASP.NET sayfa öğreticisindeki BLL ve dal düzeyi özel durumları işleme ile](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) neredeyse özdeş bir formda kullanılan aşağıdaki kod bu ayrıntı düzeyini sağlar:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample6.vb)]

Bu öğreticiyi tamamlayabilmeniz için, yakalanan `Exception` örneğini geçirerek `Catch` bloğundan `DisplayExceptionDetails` yöntemini çağırmanız yeterlidir (`ex`).

`Try ... Catch` bloğu yerinde olduğunda, kullanıcılara 4 ve 5. şekil olarak daha bilgilendirici bir hata iletisi sunulur. DataList 'in düzenleme modunda kaldığı bir özel durum durumunda olduğunu unutmayın. Bunun nedeni, özel durum oluşduktan sonra, DataList 'i önceden düzenlenen duruma getiren kodu atlayarak denetim akışı `Catch` bloğuna hemen yeniden yönlendirilir.

[Kullanıcı gerekli bir alanı atladığında bir hata Iletisi ![görüntülenir](handling-bll-and-dal-level-exceptions-vb/_static/image9.png)](handling-bll-and-dal-level-exceptions-vb/_static/image8.png)

**Şekil 4**: Kullanıcı gerekli bir alanı atladığında bir hata iletisi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](handling-bll-and-dal-level-exceptions-vb/_static/image10.png))

[Negatif fiyat girerken bir hata Iletisi ![görüntülenir](handling-bll-and-dal-level-exceptions-vb/_static/image12.png)](handling-bll-and-dal-level-exceptions-vb/_static/image11.png)

**Şekil 5**: negatif bir fiyat girerken bir hata iletisi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](handling-bll-and-dal-level-exceptions-vb/_static/image13.png))

## <a name="summary"></a>Özet

GridView ve ObjectDataSource, iş akışı güncelleştirme ve silme sırasında oluşturulan özel durumlar hakkında bilgi ve özel durumun bir istisna olup olmadığını göstermek üzere ayarlanabileceği Özellikler içeren son düzey olay işleyicileri sağlar alınan. Ancak bu özellikler, DataList ile çalışırken ve BLL doğrudan kullanıldığında kullanılamaz. Bunun yerine, özel durum işleme uygulamamız sorumludur.

Bu öğreticide, `UpdateCommand` olay işleyicisine bir `Try ... Catch` bloğu ekleyerek düzenlenebilir bir DataList s güncelleştirme iş akışına nasıl özel durum işlemenin ekleneceğini gördük. Güncelleştirme iş akışı sırasında bir özel durum ortaya çıktığında, `Catch` blok kodu yürütülür ve bu, `ExceptionDetails` etiketinde yararlı bilgiler görüntüler.

Bu noktada, DataList, özel durumların ilk yerde oluşmasını önlemeye yönelik bir çaba yapmaz. Negatif bir fiyatın bir özel durumla sonuçlanabileceğini bildiğimiz halde, bir kullanıcının bu tür geçersiz bir girişi girmesini önleyemeyecek şekilde hiçbir işlevsellik eklemediniz. Sonraki öğreticimizde, `EditItemTemplate`doğrulama denetimleri ekleyerek geçersiz Kullanıcı girişinin neden olduğu özel durumların azaltılmasına nasıl yardımcı olmaya başlayacağız.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Özel Durumlar için Tasarım Yönergeleri](https://msdn.microsoft.com/library/ms298399.aspx)
- [Hata günlüğü modülleri ve işleyiciler (ELMAH)](http://workspaces.gotdotnet.com/elmah) (günlüğe kaydetme hataları için açık kaynak kitaplığı)
- [.NET Framework 2,0 Için Kuruluş kitaplığı](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en) (özel durum yönetimi uygulama bloğunu içerir)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni, UK ön PISA idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](performing-batch-updates-vb.md)
> [İleri](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)
