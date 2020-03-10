---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
title: Toplu silme (C#) | Microsoft Docs
author: rick-anderson
description: Tek bir işlemde birden çok veritabanı kaydını silmeyi öğrenin. Kullanıcı arabirimi katmanında, önceki bir tut... içinde oluşturulan gelişmiş bir GridView üzerinde oluşturacağız.
ms.author: riande
ms.date: 06/26/2007
ms.assetid: ac6916d0-a5ab-4218-9760-7ba9e72d258c
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: ed832c38b4972f440ab64c141e29c85f0a9df920
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78589532"
---
# <a name="batch-deleting-c"></a>Toplu Silme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_CS.zip) veya [PDF 'yi indirin](batch-deleting-cs/_static/datatutorial65cs1.pdf)

> Tek bir işlemde birden çok veritabanı kaydını silmeyi öğrenin. Kullanıcı arabirimi katmanında, daha önceki bir öğreticide oluşturulan gelişmiş bir GridView üzerinde oluşturacağız. Veri erişim katmanında, tüm silmenin başarılı veya tüm silinmelerin geri alındığından emin olmak için bir işlem içindeki birden çok silme işlemini sardık.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](batch-updating-cs.md) , tam olarak düzenlenebilir bir GridView kullanılarak toplu düzenleme arabirimi oluşturma işlemi araştırılmış. Kullanıcıların birçok kaydı tek seferde düzenlemekte olduğu durumlarda, toplu bir düzenleyici arabirimi, son kullanıcının verimliliğini artırarak daha az sayıda geri yükleme ve klavyeden fareyle bağlam anahtarları gerektirir. Bu teknik benzer şekilde, kullanıcıların tek bir go 'da birçok kaydı silmesi için ortak olduğu sayfalar için de kullanışlıdır.

Çevrimiçi bir e-posta istemcisi kullanan herkes, en yaygın toplu Batch 'yi silme arabirimlerinden birini zaten biliyor: bir kılavuzdaki her satırdaki her satırdaki onay kutusu, karşılık gelen tüm Işaretlenmiş öğeleri Sil düğmesi (bkz. Şekil 1). Bu öğreticide, hem Web tabanlı arabirim oluşturma hem de bir kayıt serisini tek atomik bir işlem olarak silmek için bir yöntem olan önceki öğreticilerdeki tüm sabit işleri zaten yaptığımız için bu öğretici daha kısadır. [Onay kutuları ekleme öğreticisindeki GridView sütununda](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) , CheckBox 'ları Içeren bir GridView oluşturduk ve [bir Işlem öğreticisindeki sarmalama veritabanı değişiklikleri](wrapping-database-modifications-within-a-transaction-cs.md) içinde, bir `ProductID` değerlerinin `List<T>` silmek için bir işlem kullanan BLL 'de bir yöntem oluşturduk. Bu öğreticide, bir çalışma toplu işi oluşturmak için önceki deneyimlerimizi oluşturacak ve birleştirme işlemini gerçekleştireceğiz.

[Her satır ![onay kutusu Içerir](batch-deleting-cs/_static/image1.gif)](batch-deleting-cs/_static/image1.png)

**Şekil 1**: her satır bir onay kutusu içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-deleting-cs/_static/image2.png))

## <a name="step-1-creating-the-batch-deleting-interface"></a>1\. Adım: toplu Işi silme arabirimi oluşturma

[Onay kutusu öğreticisinin GridView sütununda bir GridView ekleme](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) arabirimini zaten oluşturduğumuz için, onu sıfırdan oluşturmak yerine `BatchDelete.aspx` kopyalamanız yeterlidir. `BatchData` klasöründeki `BatchDelete.aspx` sayfasını ve `EnhancedGridView` klasöründeki `CheckBoxField.aspx` sayfasını açarak başlayın. `CheckBoxField.aspx` sayfasında, kaynak görünümüne gidin ve Şekil 2 ' de gösterildiği gibi, `<asp:Content>` etiketleri arasındaki biçimlendirmeyi kopyalayın.

[CheckBoxField. aspx ' in bildirim temelli Işaretlemesini panoya kopyalamak ![](batch-deleting-cs/_static/image2.gif)](batch-deleting-cs/_static/image3.png)

**Şekil 2**: `CheckBoxField.aspx` bildirim temelli işaretlemesini panoya kopyalama ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-deleting-cs/_static/image4.png))

Sonra, `BatchDelete.aspx` ' deki kaynak görünümüne gidin ve Pano içeriğini `<asp:Content>` etiketleri içine yapıştırın. Ayrıca, kodu `CheckBoxField.aspx.cs` arka plan kod sınıfı içinden `BatchDelete.aspx.cs` (`DeleteSelectedProducts` düğme s `Click` olay işleyicisi, `ToggleCheckState` yöntemi ve `Click` ve `CheckAll` düğmeleri için `UncheckAll` olay işleyicileri) içine kopyalayın ve yapıştırın. Bu içeriğin üzerine kopyaladıktan sonra, `BatchDelete.aspx` sayfa arka plan kod sınıfı aşağıdaki kodu içermelidir:

[!code-csharp[Main](batch-deleting-cs/samples/sample1.cs)]

Bildirim temelli biçimlendirme ve kaynak kodu üzerine kopyaladıktan sonra, bir tarayıcıdan görüntüleyerek `BatchDelete.aspx` test etmek biraz zaman ayırın. Ürün adı, kategori ve fiyat onay kutusu ile birlikte her satır için GridView 'da ilk on ürünün listelendiği bir GridView görmeniz gerekir. Üç düğme olmalıdır: tümünü Işaretleyin, tümünün Işaretini kaldırın ve seçili ürünleri silin. Tümünü Işaretle düğmesine tıklamak tüm onay kutularını seçer, ancak tümünün Işaretini kaldır tüm onay kutularını temizler. Seçili ürünleri Sil ' i tıklatmak seçili ürünlerin `ProductID` değerlerini listeleyen bir ileti görüntüler, ancak ürünleri gerçekten silmez.

[CheckBoxField. aspx ' den arabirim ![Batchsilmesini. aspx ' e taşındı](batch-deleting-cs/_static/image3.gif)](batch-deleting-cs/_static/image5.png)

**Şekil 3**: `CheckBoxField.aspx` arabirimi `BatchDeleting.aspx` taşındı ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-deleting-cs/_static/image6.png))

## <a name="step-2-deleting-the-checked-products-using-transactions"></a>2\. Adım: Işlemleri kullanarak denetlenen ürünleri silme

Toplu iş silme arabirimi `BatchDeleting.aspx`' ye başarıyla kopyalanırsa, seçili ürünleri Sil düğmesinin, `ProductsBLL` sınıfındaki `DeleteProductsWithTransaction` yöntemi kullanılarak denetlenen ürünleri silmesi için kodu güncelleştirme işlemi devam etmektedir. [Bir işlem öğreticisindeki sarmalama veritabanı değişikliklerine](wrapping-database-modifications-within-a-transaction-cs.md) eklenen bu yöntem, `ProductID` değerlerinin `List<T>` giriş olarak kabul eder ve karşılık gelen her `ProductID` bir işlemin kapsamı içinde siler.

`DeleteSelectedProducts` Button s `Click` olay işleyicisi şu anda her bir GridView satırında yinelemek için aşağıdaki `foreach` döngüsünü kullanır:

[!code-csharp[Main](batch-deleting-cs/samples/sample2.cs)]

Her satır için `ProductSelector` onay kutusu Web denetimine program aracılığıyla başvurulur. İşaretliyse, satır s `ProductID` `DataKeys` koleksiyonundan alınır ve `DeleteResults` Label s `Text` özelliği, satırın silinmek üzere seçili olduğunu belirten bir ileti içerecek şekilde güncelleştirilir.

Yukarıdaki kod, `ProductsBLL` sınıf s `Delete` yöntemine yapılan çağrı geçersiz kılınan bir kaydı gerçekten silmez. Bu silme mantığı uygulanmıştı, kod ürünleri silecek ancak atomik bir işlem içinde değil. Yani, dizideki ilk birkaç silme işlemi başarılı oldu, ancak daha sonra bir başarısız oldu (Belki de bir yabancı anahtar kısıtlaması ihlali nedeniyle), bir özel durum oluşturulur ancak zaten silinmiş olan ürünler silinmiş olarak kalır.

Kararlılığını güvence altına almak için bunun yerine `ProductsBLL` Class s `DeleteProductsWithTransaction` metodunu kullanmanız gerekir. Bu yöntem `ProductID` değerleri listesini kabul ettiğinden, önce bu listeyi kılavuzdan derleyip sonra bir parametre olarak iletmemiz gerekir. Önce `int`türünde bir `List<T>` örneği oluşturacağız. `foreach` döngüsünde, seçilen ürünlerin `ProductID` değerlerini bu `List<T>`eklemesi gerekir. Döngüden sonra bu `List<T>` `ProductsBLL` sınıf s `DeleteProductsWithTransaction` metoduna geçirilmesi gerekir. `DeleteSelectedProducts` Button s `Click` olay işleyicisini aşağıdaki kodla güncelleştirin:

[!code-csharp[Main](batch-deleting-cs/samples/sample3.cs)]

Güncelleştirilmiş kod, `int` (`productIDsToDelete`) türünde bir `List<T>` oluşturur ve silinecek `ProductID` değerleriyle doldurur. `foreach` döngüsünden sonra, en az bir ürün seçilirse `ProductsBLL` sınıf s `DeleteProductsWithTransaction` metodu çağrılır ve bu liste geçirilir. `DeleteResults` etiketi de görüntülenir ve veriler GridView 'a yeniden bağlanır (böylece yeni silinen kayıtlar kılavuzda satır olarak görünmez).

Şekil 4 ' te, bir dizi satır silinmek üzere seçildikten sonra GridView gösterilmektedir. Şekil 5 ' te, seçili ürünleri Sil düğmesine tıklandıktan hemen sonra ekran gösterilir. Şekil 5 ' te, silinen kayıtların `ProductID` değerlerinin GridView 'un altındaki etikette görüntülendiğini ve bu satırların artık GridView 'da olmadığını unutmayın.

[![seçili ürünler silinecek](batch-deleting-cs/_static/image4.gif)](batch-deleting-cs/_static/image7.png)

**Şekil 4**: Seçili Ürünler silinecek ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-deleting-cs/_static/image8.png))

[![silinen ürünlerin ProductID değerleri GridView 'un altında listelenmiştir](batch-deleting-cs/_static/image5.gif)](batch-deleting-cs/_static/image9.png)

**Şekil 5**: silinen ürünler `ProductID` değerler GridView 'un altında listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](batch-deleting-cs/_static/image10.png))

> [!NOTE]
> `DeleteProductsWithTransaction` yöntemi kararlılığını test etmek için `Order Details` tablosundaki bir ürün için el ile bir giriş ekleyin ve ardından bu ürünü (diğer kişilerle birlikte) silmeyi deneyin. Ürünü ilişkili bir siparişle silmeye çalışırken bir yabancı anahtar kısıtlaması ihlali alırsınız, ancak seçilen diğer ürün silme işlemlerinin nasıl geri alınacağını aklınızda bulabilirsiniz.

## <a name="summary"></a>Özet

Batch silme arabirimi oluşturmak, CheckBox sütunuyla bir GridView eklemeyi ve tıklandığı zaman bir düğme web denetimini, tıklatıldığında seçili satırların tümünü tek atomik bir işlem olarak silecek şekilde içerir. Bu öğreticide, iki önceki öğreticide bir [GridView sütunu ekleyerek](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) ve [bir Işlem Içindeki veritabanı değişikliklerini sarmalayarak](wrapping-database-modifications-within-a-transaction-cs.md), bu tür bir arabirimi piecing ile birlikte geliştirdik. İlk öğreticide, CheckBox 'ları içeren bir GridView oluşturduğumuz ve ikinci bölümünde, bir `List<T>` `ProductID` değerleri geçirildiğinde bir işlemin kapsamı içinde silinen bir yöntemi uyguladık.

Sonraki öğreticide, toplu ekleme işlemi gerçekleştirmek için bir arabirim oluşturacağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Giesenow ve Teresa Murphy olduğunu gösterir. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](batch-updating-cs.md)
> [İleri](batch-inserting-cs.md)
