---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
title: DataList ve Repeater 'daki özel düğmeler (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, sistemdeki kategorileri listelemek için bir yineleyici kullanan bir arabirim oluşturacağız ve her bir kategori, assocı 'yi göstermek için bir düğme sağlar...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 1f42e332-78dc-438b-9e35-0c97aa0ad929
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: e8cb1054068327c25e057b6df1cc7506feec8d37
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78576393"
---
# <a name="custom-buttons-in-the-datalist-and-repeater-c"></a>DataList ve Repeater’daki Özel Düğmeler (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_CS.exe) veya [PDF 'yi indirin](custom-buttons-in-the-datalist-and-repeater-cs/_static/datatutorial46cs1.pdf)

> Bu öğreticide, sistemdeki kategorileri listelemek için bir yineleyici kullanan bir arabirim oluşturacağız, her kategori bir BulletedList denetimi kullanarak ilişkili ürünlerini göstermek için bir düğme sağlar.

## <a name="introduction"></a>Giriş

Son on yedi DataList ve Repeater öğreticilerinin tamamında hem salt okunurdur hem de onları düzenlemenizi ve silmenizi sağlıyoruz. Bir DataList içindeki özellikleri düzenlemenizi ve silmeyi kolaylaştırmak için, ' yi, tıklandığı zaman bir geri göndermeye neden olan ve düğme s `CommandName` özelliğine karşılık gelen bir DataList olayını harekete getiren `ItemTemplate` DataList 'e düğme ekledik. Örneğin, bir `ItemTemplate` `CommandName` Özellik değeri ile bir düğme eklemek, `EditCommand` DataList 'in geri göndermede tetiklenmesine neden olur; `CommandName` delete ile biri `DeleteCommand`oluşturur.

Düzenleme ve silme düğmelerine ek olarak, DataList ve Repeater denetimleri, tıklandığı sırada bazı özel sunucu tarafı mantığlarını, LinkButtons veya ımagebuttons da içerebilir. Bu öğreticide, sistemdeki kategorileri listelemek için bir yineleyici kullanan bir arabirim oluşturacağız. Her kategori için, yineleyici bir BulletedList denetimi kullanarak kategorinin ilişkili ürünlerini göstermek üzere bir düğme içerir (bkz. Şekil 1).

[Ürünleri göster bağlantısına tıklamak ![kategori öğeleri madde Işaretli bir listede görüntülenir](custom-buttons-in-the-datalist-and-repeater-cs/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image1.png)

**Şekil 1**: ürünleri göster bağlantısına tıkladığınızda kategori öğeleri madde Işaretli bir listede görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](custom-buttons-in-the-datalist-and-repeater-cs/_static/image3.png))

## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>1\. Adım: özel düğme öğreticisi Web sayfalarını ekleme

Özel bir düğme eklemeye bakmadan önce, Web sitesi projemizdeki Bu öğreticide gereken ASP.NET sayfalarını oluşturmak için önce bir süre sürme. `CustomButtonsDataListRepeater`adlı yeni bir klasör ekleyerek başlayın. Sonra, her bir sayfayı `Site.master` ana sayfayla ilişkilendirdiğinizden emin olmak için, aşağıdaki iki ASP.NET sayfasını bu klasöre ekleyin:

- `Default.aspx`
- `CustomButtons.aspx`

![Özel düğmelerle Ilgili öğreticiler için ASP.NET sayfaları ekleyin](custom-buttons-in-the-datalist-and-repeater-cs/_static/image4.png)

**Şekil 2**: özel düğmelerle ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `CustomButtonsDataListRepeater` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu Kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](custom-buttons-in-the-datalist-and-repeater-cs/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image5.png)

**Şekil 3**: `Default.aspx` `SectionLevelTutorialListing.ascx` Kullanıcı denetimini ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](custom-buttons-in-the-datalist-and-repeater-cs/_static/image7.png))

Son olarak, sayfaları `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, sayfalama ve, DataList ve yineleyici `<siteMapNode>`ile sıralama sonrasında aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık öğreticilerin düzenlenmesine, eklemeye ve silinmesine yönelik öğeler içerir.

![Site Haritası artık özel düğmeler öğreticisi için girişi Içerir](custom-buttons-in-the-datalist-and-repeater-cs/_static/image8.png)

**Şekil 4**: site haritası artık özel düğmeler öğreticisi Için girişi içerir

## <a name="step-2-adding-the-list-of-categories"></a>2\. Adım: kategorilerin listesini ekleme

Bu öğreticide, tüm kategorileri listeleyen bir yineleyici oluşturmanız gerekir ve tıklandığı sırada ilgili kategorinin ürünlerini madde işaretli bir listede görüntüler. İlk olarak sistemdeki kategorileri listeleyen basit bir yineleyici oluşturalım. `CustomButtonsDataListRepeater` klasöründeki `CustomButtons.aspx` sayfasını açarak başlayın. Araç kutusu ' ndan tasarımcı üzerine bir yineleyici sürükleyin ve `ID` özelliğini `Categories`olarak ayarlayın. Sonra, Repeater s akıllı etiketinden yeni bir veri kaynağı denetimi oluşturun. Özellikle, `CategoriesBLL` sınıf s `GetCategories()` yönteminden verilerini seçen `CategoriesDataSource` adlı yeni bir ObjectDataSource denetimi oluşturun.

[![, CategoriesBLL sınıfı s GetCategories () yöntemini kullanmak için ObjectDataSource 'ı yapılandırma](custom-buttons-in-the-datalist-and-repeater-cs/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image9.png)

**Şekil 5**: `CategoriesBLL` sınıf s `GetCategories()` metodunu ([tam boyutlu görüntüyü görüntülemek Için tıklayın](custom-buttons-in-the-datalist-and-repeater-cs/_static/image11.png)) kullanmak üzere ObjectDataSource 'ı yapılandırın

Visual Studio 'Nun veri kaynağına bağlı olarak varsayılan bir `ItemTemplate` oluşturduğu DataList denetiminden farklı olarak, Repeater s şablonlarının el ile tanımlanması gerekir. Ayrıca, Repeater s şablonlarının bildirimli olarak oluşturulması ve düzenlenmesi gerekir (diğer bir deyişle, yineleyicisi 'nin akıllı etiketinde şablon düzenleme yok seçeneği vardır).

Sol alt köşedeki kaynak sekmesine tıklayın ve bir `<h3>` öğesinde kategori adı ve bir paragraf etiketinde açıklamasını görüntüleyen bir `ItemTemplate` ekleyin; Her kategori arasında yatay bir kural (`<hr />`) görüntüleyen bir `SeparatorTemplate` ekleyin. Ayrıca, ürünleri göstermek için `Text` özelliği ayarlanmış bir LinkButton de ekleyin. Bu adımları tamamladıktan sonra, sayfa bildirim temelli işaretlerinizin aşağıdaki gibi görünmesi gerekir:

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample2.aspx)]

Şekil 6 bir tarayıcı aracılığıyla görüntülenirken sayfayı gösterir. Her kategori adı ve açıklaması listelenir. Tıklatıldığında ürünleri göster düğmesi geri göndermeye neden olur, ancak henüz hiçbir işlem gerçekleştirmez.

[Her kategorinin adı ve açıklaması ![, ürünleri göster LinkButton ile birlikte görüntülenir](custom-buttons-in-the-datalist-and-repeater-cs/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image12.png)

**Şekil 6**: her kategori adı ve açıklaması, ürünleri göster LinkButton Ile birlikte görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](custom-buttons-in-the-datalist-and-repeater-cs/_static/image14.png))

## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>3\. Adım: ürünleri göster LinkButton tıklandığında sunucu tarafı mantığını yürütme

DataList veya Repeater içindeki bir şablon içindeki düğme, LinkButton veya ImageButton ' ın her zaman tıklandığı, bir geri gönderme gerçekleşir ve DataList veya Repeater s `ItemCommand` olay ateşlenir. `ItemCommand` olayına ek olarak, DataList denetimi Ayrıca, düğme s `CommandName` özelliği ayrılmış dizelerinden birine ayarlanmışsa (silme, düzenleme, Iptal etme, güncelleştirme veya seçim), ancak `ItemCommand` olayı *her zaman* harekete geçirilir.

Bir düğmeye bir DataList veya Repeater içinde tıklandığında, hangi düğmenin tıklandığı (denetim içinde hem düzenleme hem de silme düğmesi gibi birden çok düğme olabilir) ve belki de bazı ek bilgiler (örneğin, düğmesine tıklanmış olan öğenin birincil anahtar değeri). Button, LinkButton ve ImageButton, değerlerinin `ItemCommand` olay işleyicisine geçirildiği iki özellik sağlar:

- şablondaki her düğmeyi tanımlamak için genellikle kullanılan bir dize `CommandName`
- birincil anahtar değeri gibi bazı veri alanı değerlerini tutmak için yaygın olarak kullanılan `CommandArgument`

Bu örnekte, LinkButton s `CommandName` özelliğini ShowProducts olarak ayarlayın ve geçerli kayıt birincil anahtar değeri `CategoryID`, veri bağlama söz dizimi `CategoryArgument='<%# Eval("CategoryID") %>'`kullanarak `CommandArgument` özelliğine bağlayın. Bu iki özelliği belirttikten sonra LinkButton s bildirime dayalı sözdizimi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample3.aspx)]

Düğmeye tıklandığında, bir geri gönderme gerçekleşir ve DataList veya Repeater s `ItemCommand` olayı ateşlenir. Olay işleyicisi, düğme s `CommandName` ve `CommandArgument` değerlerini geçti.

Yineleyici s `ItemCommand` olayı için bir olay işleyicisi oluşturun ve olay işleyicisine (`e`) geçirilen ikinci parametreyi aklınızda edin. Bu ikinci parametre [`RepeaterCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) türüdür ve aşağıdaki dört özelliğe sahiptir:

- tıklanan düğme s `CommandArgument` özelliğinin değerini `CommandArgument`
- düğme s `CommandName` özelliğinin değerini `CommandName`
- tıklanan düğme denetimine bir başvuru `CommandSource`
- tıklanan düğmeyi içeren [`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx) bir başvuru `Item`; Yineleyici ile bağlantılı her kayıt `RepeaterItem` olarak tanımlanır

Seçili Kategori `CategoryID` `CommandArgument` özelliği aracılığıyla geçirildiğinden, `ItemCommand` olay işleyicisindeki seçili kategoriyle ilişkili ürün kümesini edinebilirsiniz. Bu ürünler daha sonra `ItemTemplate` (henüz ekliyoruz) bir BulletedList denetimine bağlanabilir. Tüm bunlar, BulletedList eklemek, `ItemCommand` olay işleyicisine başvurmak ve seçili kategori için bu ürüne bağlamak, bu, 4. adımda yer vereceğiz.

> [!NOTE]
> DataList s `ItemCommand` olay işleyicisi, `RepeaterCommandEventArgs` sınıfıyla aynı dört özelliği sunan [`DataListCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx)türünde bir nesne geçirdi.

## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>4\. Adım: Seçili Kategori ürünlerini madde Işaretli bir listede görüntüleme

Seçilen kategori ürünleri, herhangi bir sayıda denetim kullanılarak Yineleyici s `ItemTemplate` içinde görüntülenebilir. İç içe geçmiş bir yineleyici, bir DataList, bir DropDownList, GridView ve benzeri bir ekleyebiliriz. Ürünleri madde işaretli bir liste olarak göstermek istediğimiz için BulletedList denetimini kullanacağız. `CustomButtons.aspx` sayfa bildirimli biçimlendirmeye dönerek, ürünleri göster LinkButton düğmesine `ItemTemplate` bir BulletedList denetimi ekleyin. BulletedLists s `ID` `ProductsInCategory`olarak ayarlayın. BulletedList, `DataTextField` özelliği ile belirtilen veri alanının değerini görüntüler; Bu denetime, ürün bilgileri bağlandığından, `DataTextField` özelliğini `ProductName`olarak ayarlayın.

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample4.aspx)]

`ItemCommand` olay işleyicisinde, bu denetime `e.Item.FindControl("ProductsInCategory")` kullanarak başvurun ve seçili kategoriyle ilişkili ürün kümesine bağlayın.

[!code-csharp[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample5.cs)]

`ItemCommand` olay işleyicisinde herhangi bir işlem gerçekleştirmeden önce, ilk olarak gelen `CommandName`değerini kontrol edin. `ItemCommand` olay işleyicisi *herhangi bir* düğmeye tıklandığında ateşlenir, şablonda birden çok düğme varsa, hangi eylemin yapılacağını ayırt etmek için `CommandName` değerini kullanın. Yalnızca tek bir düğmeye sahip olduğumuz, ancak form için iyi bir önleminizi alarak olduğundan, burada `CommandName` kontrol edilir. Sonra, seçilen kategorinin `CategoryID` `CommandArgument` özelliğinden alınır. Şablondaki BulletedList denetimine başvurulur ve `ProductsBLL` sınıf s `GetProductsByCategoryID(categoryID)` yönteminin sonuçlarına bağlanır.

DataList içindeki [verileri düzenlemenin ve silmenin genel bakışı](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)gibi bir DataList içindeki düğmeleri kullanan önceki öğreticilerde, belirli bir öğenin birincil anahtar değerini `DataKeys` koleksiyonu aracılığıyla belirledik. Bu yaklaşım DataList ile birlikte çalışarak, yineleyicisi bir `DataKeys` özelliğine sahip değildir. Bunun yerine, düğme s `CommandArgument` özelliği gibi birincil anahtar değerini sağlamak için alternatif bir yaklaşım kullandık veya birincil anahtar değerini şablon içinde gizli bir etiket Web denetimine atayarak ve değeri `e.Item.FindControl("LabelID")`kullanarak `ItemCommand` olay işleyicisine geri okuyacağız.

`ItemCommand` olay işleyicisini tamamladıktan sonra, bu sayfayı bir tarayıcıda test etmek için bir dakikanızı ayırın. Şekil 7 ' de gösterildiği gibi, ürünleri göster bağlantısına tıklamak geri göndermeye neden olur ve bir BulletedList içinde seçili kategori için ürünleri görüntüler. Ayrıca, diğer kategoriler ürün bağlantılarını gösterip göstermese de bu ürün bilgilerinin kaldığını unutmayın.

> [!NOTE]
> Bu raporun davranışını değiştirmek istiyorsanız, yalnızca tek bir kategori ürünleri aynı anda listelenirse, BulletedList Control s `EnableViewState` özelliğini `False`olarak ayarlamanız yeterlidir.

[Seçilen kategorinin ürünlerini göstermek için bir BulletedList ![kullanılır](custom-buttons-in-the-datalist-and-repeater-cs/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image15.png)

**Şekil 7**: seçili kategorinin ürünlerini görüntülemek Için bir BulletedList kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](custom-buttons-in-the-datalist-and-repeater-cs/_static/image17.png))

## <a name="summary"></a>Özet

DataList ve Repeater denetimleri, şablonları içinde herhangi bir sayıda düğme, bağlantı düğmesi veya ImageButton içerebilir. Bu tür düğmeler tıklandığında, geri göndermeye neden olur ve `ItemCommand` olayını yükseltir. Özel sunucu tarafı eylemini tıklanan bir düğmeyle ilişkilendirmek için `ItemCommand` olayı için bir olay işleyicisi oluşturun. Bu olay işleyicisinde ilk olarak hangi düğmenin tıklandığını belirleyen gelen `CommandName` değerini denetleyin. Ek bilgiler isteğe bağlı olarak düğme s `CommandArgument` özelliği aracılığıyla sağlanabilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider olarak gözden geçiren Dennis Patterson. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](custom-buttons-in-the-datalist-and-repeater-vb.md)
