---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
title: FormView 'un şablonlarını kullanma (C#) | Microsoft Docs
author: rick-anderson
description: DetailsView 'un aksine FormView, alanlardan oluşamaz. Bunun yerine, FormView şablonlar kullanılarak işlenir. Bu öğreticide F... kullanmayı inceleyeceğiz.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d3f062af-88cf-426d-af44-e41f32c41672
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
msc.type: authoredcontent
ms.openlocfilehash: 013c6878aad1a2277b0a334c096ff16ed84a95f1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74625647"
---
# <a name="using-the-formviews-templates-c"></a>FormView 'un şablonlarını (C#) kullanma

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_14_CS.exe) veya [PDF 'yi indirin](using-the-formview-s-templates-cs/_static/datatutorial14cs1.pdf)

> DetailsView 'un aksine FormView, alanlardan oluşamaz. Bunun yerine, FormView şablonlar kullanılarak işlenir. Bu öğreticide, verilerin daha az rigıd görüntüsünü sunmak için FormView denetimini kullanmayı inceleyeceğiz.

## <a name="introduction"></a>Giriş

Son iki öğreticilerde, GridView ' i özelleştirmeyi ve DetailsView ' ın TemplateFields kullanarak çıktıları denetimlerini nasıl özelleştireceğinizi gördünüz. TemplateFields, belirli bir alanın içeriğinin yüksek bir şekilde özelleştirilmeye olanak tanır, ancak sonunda hem GridView hem de DetailsView, kılavuz benzeri bir görünüm ' e sahiptir. Birçok senaryo için, ızgara benzeri düzen idealdir, ancak daha akıcı, daha az rigıd görüntüleme gerekir. Tek bir kayıt görüntülenirken, FormView denetimi kullanılarak akıcı bir düzen mümkündür.

DetailsView 'un aksine FormView, alanlardan oluşamaz. Bir FormView 'a bir BoundField veya TemplateField ekleyemezsiniz. Bunun yerine, FormView şablonlar kullanılarak işlenir. FormView öğesini tek bir TemplateField içeren bir DetailsView denetimi olarak düşünün. FormView aşağıdaki şablonları destekler:

- FormView 'da görüntülenecek olan belirli kaydı oluşturmak için kullanılan `ItemTemplate`
- isteğe bağlı üst bilgi satırını belirtmek için kullanılan `HeaderTemplate`
- isteğe bağlı bir altbilgi satırını belirtmek için kullanılan `FooterTemplate`
- FormView 'un `DataSource` hiçbir kayıt olmadığında `EmptyDataTemplate`, `EmptyDataTemplate` denetimin işaretlemesini işlemek için `ItemTemplate` yerine kullanılır
- `PagerTemplate`, sayfalama etkinleştirilmiş olan FormViews için sayfalama arabirimini özelleştirmek için kullanılabilir
- `EditItemTemplate` / `InsertItemTemplate`, bu işlevselliği destekleyen FormViews için Düzenle arabirimini veya ekleme arabirimini özelleştirmek için kullanılır

Bu öğreticide, ürünlerin daha az rigıd görüntüsünü sunmak için FormView denetimini kullanmayı inceleyeceğiz. Ad, kategori, tedarikçi ve benzeri alanları yerine, FormView 'un `ItemTemplate`, bir üst bilgi öğesinin ve bir `<table>` birleşimini kullanarak bu değerleri gösterir (bkz. Şekil 1).

[DetailsView 'da görülen kılavuza benzer düzenin FormView 'un sonlarını ![](using-the-formview-s-templates-cs/_static/image2.png)](using-the-formview-s-templates-cs/_static/image1.png)

**Şekil 1**: FormView, DetailsView 'Da görülen kılavuza benzer düzende kesilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-formview-s-templates-cs/_static/image3.png))

## <a name="step-1-binding-the-data-to-the-formview"></a>1\. Adım: verileri FormView 'a bağlama

`FormView.aspx` sayfasını açın ve araç kutusundan bir FormView öğesini tasarımcı üzerine sürükleyin. İlk olarak FormView eklendiğinde, bir `ItemTemplate` gerekli olduğunu belirten bir gri kutu olarak görünür.

[![ItemTemplate sağlanana kadar tasarımcı 'da Işlenemiyor](using-the-formview-s-templates-cs/_static/image5.png)](using-the-formview-s-templates-cs/_static/image4.png)

**Şekil 2**: FormView bir `ItemTemplate` sağlanana kadar tasarımcı 'da işlenemiyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-formview-s-templates-cs/_static/image6.png))

`ItemTemplate` el ile oluşturulabilir (bildirim temelli söz dizimi aracılığıyla) veya FormView, tasarımcı aracılığıyla bir veri kaynağı denetimine bağlayarak otomatik olarak oluşturulabilir. Bu otomatik oluşturulan `ItemTemplate` her alanın adını ve `Text` özelliği alanın değerine bağlanan bir etiket denetimini listeleyen HTML içerir. Bu yaklaşım ayrıca, her ikisi de veri kaynağı denetimi tarafından döndürülen her bir veri alanı için giriş denetimleriyle doldurulan bir `InsertItemTemplate` ve `EditItemTemplate`otomatik olarak oluşturur.

Şablonu otomatik oluşturmak istiyorsanız, FormView 'un akıllı etiketinden `ProductsBLL` sınıfının `GetProducts()` yöntemini çağıran yeni bir ObjectDataSource denetimi ekleyin. Bu, bir `ItemTemplate`, `InsertItemTemplate`ve `EditItemTemplate`ile bir FormView oluşturacaktır. Kaynak görünümünden `InsertItemTemplate` ve `EditItemTemplate` kaldırın, ancak henüz düzenlemenizi veya eklemeyi destekleyen bir FormView oluşturma konusunda ilgileniyoruz. Bundan sonra, üzerinde çalışmak üzere temiz bir tablet olması için `ItemTemplate` içindeki biçimlendirmeyi temizleyin.

`ItemTemplate` el ile oluşturmayı tercih ediyorsanız, ObjectDataSource 'u araç kutusu 'ndan tasarımcı üzerine sürükleyerek ekler ekleyebilir ve yapılandırabilirsiniz. Ancak, FormView 'un veri kaynağını tasarımcıdan ayarlamazsanız. Bunun yerine, kaynak görünümüne gidin ve FormView 'un `DataSourceID` özelliğini, ObjectDataSource 'un `ID` değerine el ile ayarlayın. Sonra `ItemTemplate`el ile ekleyin.

Hangi yaklaşımdan bağımsız olarak, bu noktada FormView 'un bildirim temelli biçimlendirmesi şöyle görünmelidir:

[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample1.aspx)]

FormView 'un akıllı etiketinde sayfalama etkinleştir onay kutusunu işaretleyin. Bu, `AllowPaging="True"` özniteliğini FormView 'un bildirime dayalı sözdizimine ekler. Ayrıca, `EnableViewState` özelliğini false olarak ayarlayın.

## <a name="step-2-defining-theitemtemplates-markup"></a>2\. Adım:`ItemTemplate`Işaretlemesini tanımlama

Olan FormView, ObjectDataSource denetimine bağlamakta ve sayfalama desteklemek üzere yapılandırıldıktan sonra `ItemTemplate`için içerik belirtmeye hazırız. Bu öğreticide, ürün adının bir `<h3>` başlığında görüntülenmesini görelim. Bundan sonra, ilk ve üçüncü sütunların özellik adlarını ve ikinci ve dördüncü liste değerlerini listelebileceği dört sütunlu bir tabloda kalan ürün özelliklerini göstermek için bir HTML `<table>` kullanalım.

Bu biçimlendirme, tasarımcıda FormView 'un şablon düzenlemesi arabiriminden veya bildirime dayalı sözdizimi aracılığıyla el ile girilebilir. Şablonlarla çalışırken, genellikle bildirim temelli söz dizimi ile doğrudan çalışmayı daha hızlı buldum, ancak en rahat olan yöntemleri kullanmayı ücretsiz olarak öğrendim.

Aşağıdaki biçimlendirme `ItemTemplate`yapısı tamamlandıktan sonra FormView bildirim temelli işaretlemesini gösterir:

[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample2.aspx)]

Veri bağlama sözdiziminin `<%# Eval("ProductName") %>`, örneğin doğrudan şablonun çıktısına eklenebilir olduğuna dikkat edin. Diğer bir deyişle, bir etiket denetiminin `Text` özelliğine atanması gerekmez. Örneğin, `ProductName` değeri, `<h3><%# Eval("ProductName") %></h3>`kullanarak `<h3>` öğesinde görüntülenir, bu da ürün Chai 'nin `<h3>Chai</h3>`olarak işlenir.

`ProductPropertyLabel` ve `ProductPropertyValue` CSS sınıfları, `<table>`ürün özelliği adlarının ve değerlerinin stilini belirtmek için kullanılır. Bu CSS sınıfları `Styles.css` tanımlanmıştır ve özellik adlarının kalın ve sağa hizalı olmasına ve özellik değerlerine doğru bir doldurma eklemesine neden olur.

FormView ile kullanılabilen bir CheckBoxField olmadığından, `Discontinued` değerini bir onay kutusu olarak göstermek için kendi onay kutusu denetiminizi eklememiz gerekir. `Enabled` özelliği false olarak ayarlanır, salt okunurdur ve CheckBox 'ın `Checked` özelliği `Discontinued` veri alanının değerine bağlanır.

`ItemTemplate` tamamlandıktan sonra ürün bilgileri çok daha akıcı bir şekilde görüntülenir. Son öğreticideki DetailsView çıktısını (Şekil 3) Bu öğreticide FormView tarafından oluşturulan çıktıyı karşılaştırın (Şekil 4).

[Rigıd DetailsView çıkışını ![](using-the-formview-s-templates-cs/_static/image8.png)](using-the-formview-s-templates-cs/_static/image7.png)

**Şekil 3**: Rigıd DetailsView çıkışı ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-formview-s-templates-cs/_static/image9.png))

[Sıvı FormView çıkışını ![](using-the-formview-s-templates-cs/_static/image11.png)](using-the-formview-s-templates-cs/_static/image10.png)

**Şekil 4**: akışkan FormView çıkışı ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-formview-s-templates-cs/_static/image12.png))

## <a name="summary"></a>Özet

GridView ve DetailsView denetimlerinin çıktısı TemplateFields kullanılarak özelleştirilmişse, her ikisi de verileri kılavuz benzeri bir kutu biçiminde de sunar. Bu süreler için, tek bir kaydın daha az rigıd düzeni kullanılarak gösterilmesi gerektiğinde, FormView ideal bir seçimdir. DetailsView gibi, FormView `DataSource`tek bir kayıt oluşturur, ancak bu, DetailsView 'tan farklı olarak yalnızca şablonlardan oluşur ve alanları desteklemez.

Bu öğreticide gördüğünüz gibi, FormView tek bir kayıt görüntülenirken daha esnek bir düzen sağlar. Gelecek öğreticilerde, FormsView ile aynı düzeyde esneklik sağlayan, ancak birden çok kayıt (GridView gibi) görüntüleyebilen DataList ve Repeater denetimlerini inceleyeceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için baş gözden geçiren E.R. idi Gilmore. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](using-templatefields-in-the-detailsview-control-cs.md)
> [İleri](displaying-summary-information-in-the-gridview-s-footer-cs.md)
