---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
title: DataList 'in düzenleyen arabirimini özelleştirme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, bir, DropDownLists ve CheckBox içeren bir DataList için daha zengin bir düzen arabirimi oluşturacağız.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: a5d13067-ddfb-4c36-8209-0f69fd40e45c
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 81f5a7f6737f544f577447f263dbd37dbc8279d9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74623669"
---
# <a name="customizing-the-datalists-editing-interface-c"></a>DataList'in Düzenleme Arabirimini Özelleştirme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_CS.exe) veya [PDF 'yi indirin](customizing-the-datalist-s-editing-interface-cs/_static/datatutorial40cs1.pdf)

> Bu öğreticide, bir, DropDownLists ve CheckBox içeren bir DataList için daha zengin bir düzen arabirimi oluşturacağız.

## <a name="introduction"></a>Giriş

DataList 'teki biçimlendirme ve Web denetimleri, düzenlenebilir arabirimini tanımlar `EditItemTemplate`. Şimdiye kadar incelediğimiz tüm düzenlenebilir DataList örneklerinde, düzenlenebilir arabirim metin kutusu Web denetimlerinden oluşur. [Önceki öğreticide](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md) , doğrulama denetimleri ekleyerek düzenleme zamanı kullanıcı deneyimini geliştirdik.

`EditItemTemplate`, DropDownLists, RadioButtonLists, takvimler gibi metin kutusu dışındaki Web denetimlerini içerecek şekilde daha da genişletilebilir. Metin kutularına olduğu gibi, diğer Web denetimlerini içerecek şekilde, düzen arabirimini özelleştirirken, aşağıdaki adımları uygulayın:

1. `EditItemTemplate`Web denetimini ekleyin.
2. Uygun özelliğe karşılık gelen veri alanı değerini atamak için DataBinding sözdizimini kullanın.
3. `UpdateCommand` olay işleyicisinde, programlı olarak Web denetim değerine erişin ve uygun BLL metoduna geçirin.

Bu öğreticide, bir, DropDownLists ve CheckBox içeren bir DataList için daha zengin bir düzen arabirimi oluşturacağız. Özellikle ürün bilgilerini listeleyen bir DataList oluşturacağız ve ürün adı, sağlayıcı, kategori ve Discontinued durumunun güncelleştirilmesini sağlar (bkz. Şekil 1).

[![düzen arabirimi bir TextBox, Iki DropDownLists ve bir CheckBox Içerir](customizing-the-datalist-s-editing-interface-cs/_static/image2.png)](customizing-the-datalist-s-editing-interface-cs/_static/image1.png)

**Şekil 1**: düzen arabirimi bir TextBox, Iki dropdownlists ve bir onay kutusu içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image3.png))

## <a name="step-1-displaying-product-information"></a>1\. Adım: ürün bilgilerini görüntüleme

DataList 'ler düzenlenebilir arabirimini oluşturabilmeniz için önce salt okunurdur arabirimini derlemeniz gerekir. `CustomizedUI.aspx` sayfasını `EditDeleteDataList` klasöründen açıp tasarımcıdan sayfaya bir DataList ekleyerek `ID` özelliğini `Products`olarak ayarlayarak başlayın. DataList s akıllı etiketinden yeni bir ObjectDataSource oluşturun. Bu yeni ObjectDataSource `ProductsDataSource` adlandırın ve `ProductsBLL` Class s `GetProducts` yönteminden verileri almak üzere yapılandırın. Önceki düzenlenebilir DataList öğreticilerinde olduğu gibi, düzenlenen ürün bilgilerini doğrudan Iş mantığı katmanına giderek güncelleştireceğiz. Buna uygun olarak, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden (hiçbiri) açılan listeleri ayarlayın.

[GÜNCELLEŞTIRME, ekleme ve SILME sekmeleri aşağı açılan listelerini (hiçbiri) ayarlamak ![](customizing-the-datalist-s-editing-interface-cs/_static/image5.png)](customizing-the-datalist-s-editing-interface-cs/_static/image4.png)

**Şekil 2**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerini ayarlama açılan listelerini (yok) ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image6.png))

ObjectDataSource yapılandırıldıktan sonra Visual Studio, döndürülen veri alanlarının her biri için adı ve değeri listeleyen DataList için varsayılan bir `ItemTemplate` oluşturur. `ItemTemplate`, şablonun ürün adını kategori adı, tedarikçi adı, Fiyat ve Discontinued durumuyla birlikte bir `<h4>` öğesinde listelediğinden bu şekilde değiştirin. Ayrıca, bir Düzenle düğmesi ekleyin ve `CommandName` özelliğinin Düzenle olarak ayarlandığından emin olun. `ItemTemplate` için bildirim temelli biçimlendirme şu şekildedir:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

Yukarıdaki biçimlendirme ürün bilgilerini, ürün adı için bir &lt;H4&gt; başlığını ve kalan alanlar için dört sütunlu `<table>` kullanarak düzenler. `Styles.css`tanımlanmış `ProductPropertyLabel` ve `ProductPropertyValue` CSS sınıfları önceki öğreticilerde ele alınmıştır. Şekil 3 ' te bir tarayıcıdan görüntülendiklerinde ilerleme durumu gösterilmektedir.

[Ad, tedarikçi, kategori, Discontinued durumu ve her ürünün fiyatı ![görüntülenir](customizing-the-datalist-s-editing-interface-cs/_static/image8.png)](customizing-the-datalist-s-editing-interface-cs/_static/image7.png)

**Şekil 3**: ad, tedarikçi, kategori, Discontinued durumu ve her bir ürünün fiyatı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image9.png))

## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>2\. Adım: düzen arabirimine Web denetimleri ekleme

Özelleştirilmiş DataList düzenlemesi arabirimini oluşturmanın ilk adımı, gerekli Web denetimlerini `EditItemTemplate`eklemektir. Özellikle, kategori için bir DropDownList ve bir tedarikçi için bir DropDownList ve Discontinued durumu için bir onay kutusu gerekir. Bu örnekte ürün fiyatı düzenlenebilir olmadığından, etiketi Web denetimi kullanarak görüntülemeye devam edebiliriz.

Düzenleme arabirimini özelleştirmek için, DataList s akıllı etiketinden Şablonları Düzenle bağlantısına tıklayın ve açılan listeden `EditItemTemplate` seçeneğini belirleyin. `EditItemTemplate` bir DropDownList ekleyin ve `ID` `Categories`olarak ayarlayın.

[Kategoriler için DropDownList eklemek ![](customizing-the-datalist-s-editing-interface-cs/_static/image11.png)](customizing-the-datalist-s-editing-interface-cs/_static/image10.png)

**Şekil 4**: Kategoriler Için bir DropDownList ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image12.png))

Ardından, DropDownList s akıllı etiketinden veri kaynağı seç seçeneğini belirleyin ve `CategoriesDataSource`adlı yeni bir ObjectDataSource oluşturun. Bu ObjectDataSource 'ı `CategoriesBLL` Class s `GetCategories()` metodunu kullanacak şekilde yapılandırın (bkz. Şekil 5). Ardından, DropDownList s veri kaynağı Yapılandırma Sihirbazı her bir `ListItem` s `Text` ve `Value` özellikleri için veri alanlarının kullanılmasını ister. DropDownList 'in `CategoryName` veri alanını göstermesini ve Şekil 6 ' da gösterildiği gibi `CategoryID` değerini kullanmasını sağlayabilirsiniz.

[![CategoriesDataSource adlı yeni bir ObjectDataSource oluşturma](customizing-the-datalist-s-editing-interface-cs/_static/image14.png)](customizing-the-datalist-s-editing-interface-cs/_static/image13.png)

**Şekil 5**: `CategoriesDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image15.png))

[DropDownList s görüntüleme ve değer alanlarını yapılandırma ![](customizing-the-datalist-s-editing-interface-cs/_static/image17.png)](customizing-the-datalist-s-editing-interface-cs/_static/image16.png)

**Şekil 6**: DropDownList s görüntüleme ve değer alanlarını yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image18.png))

Tedarikçilere yönelik bir DropDownList oluşturmak için bu adım dizisini tekrarlayın. Bu DropDownList için `ID` `Suppliers` olarak ayarlayın ve ObjectDataSource `SuppliersDataSource`adlandırın.

İki DropDownLists eklendikten sonra, Discontinued durumu için bir onay kutusu ve ürün adı için bir TextBox ekleyin. CheckBox ve TextBox için `ID` s öğesini sırasıyla `Discontinued` ve `ProductName`olarak ayarlayın. Kullanıcının ürün adı için bir değer sağladığından emin olmak için bir RequiredFieldValidator ekleyin.

Son olarak, Güncelleştir ve Iptal düğmelerini ekleyin. Bu iki düğme için, `CommandName` özelliklerinin sırasıyla güncelleştir ve Iptal olarak ayarlandığını unutmayın.

Düzenleme arabirimini istediğiniz gibi düzenleyebilirsiniz. Aşağıdaki bildirim temelli söz dizimi ve ekran görüntüsünde gösterildiği gibi, salt okuma arabiriminden aynı dört sütunlu `<table>` düzeni kullanmayı kabul ediyorum:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample2.aspx)]

[![düzen arabirimi salt okuma arabirimi gibi düzenlenmiştir](customizing-the-datalist-s-editing-interface-cs/_static/image20.png)](customizing-the-datalist-s-editing-interface-cs/_static/image19.png)

**Şekil 7**: düzen arabirimi salt okuma arabirimi gibi düzenlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image21.png))

## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>3\. Adım: EditCommand ve CancelCommand olay Işleyicilerini oluşturma

Şu anda, `EditItemTemplate` veri bağlama söz dizimi yoktur (`UnitPriceLabel`dışında `ItemTemplate`). Veri bağlama söz dizimini bir kez daha ekleyeceğiz, ancak ilk olarak DataList s `EditCommand` ve `CancelCommand` olayları için olay işleyicileri oluşturalım. `EditCommand` olay işleyicisinin sorumluluğunun, düzenleme düğmesine tıklandığı DataList öğesi için düzenleme arabirimini işleymesinin, `CancelCommand` s işinin DataList 'i düzenleme öncesi durumuna döndürmesidir.

Bu iki olay işleyicisini oluşturun ve aşağıdaki kodu kullanın:

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample3.cs)]

Bu iki olay işleyicisi yerine, Düzenle düğmesine tıkladığınızda düzenleme arabirimi görüntülenir ve Iptal düğmesine tıklandığında düzenlenen öğe salt okunurdur moduna döndürülür. Şekil 8 ' de Chef Anton s Gumbo Mix için Düzenle düğmesine tıklandıktan sonra DataList görüntülenir. Henüz bir veri bağlama sözdizimini düzen arabirimine eklemediğimiz için `ProductName` metin kutusu boş, `Discontinued` onay kutusu işaretlenmemiş ve `Categories` ve `Suppliers` DropDownLists tarafından seçilen ilk öğe.

[Düzenle düğmesine tıklamak ![düzenleme arabirimini görüntüler](customizing-the-datalist-s-editing-interface-cs/_static/image23.png)](customizing-the-datalist-s-editing-interface-cs/_static/image22.png)

**Şekil 8**: Düzenle düğmesine tıkladığınızda düzenleme arabirimi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image24.png))

## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>4\. Adım: bağlama sözdizimini, düzen arabirimine ekleme

Düzen arabiriminin geçerli ürün değerlerini görüntülemesi için veri alanı değerlerini uygun Web denetimi değerlerine atamak üzere veri bağlama söz dizimini kullandık. Veri bağlama söz dizimi, Şablonları Düzenle ekranına gidip Web denetimleri akıllı etiketleri ' nden DataBindings bağlantısını Düzenle ' ye tıklayarak tasarımcı aracılığıyla uygulanabilir. Alternatif olarak, veri bağlama söz dizimi doğrudan bildirime dayalı biçimlendirmeye eklenebilir.

`ProductName` veri alanı değerini `ProductName` TextBox s `Text` özelliğine, `CategoryID` ve `SupplierID` veri alanı değerlerini `Categories` ve `Suppliers` DropDownLists `SelectedValue` özelliklerine ve `Discontinued` veri alanı değerini `Discontinued` onay kutusu s `Checked` özelliğine atayın. Bu değişiklikleri, tasarımcı aracılığıyla ya da doğrudan bildirime dayalı biçimlendirme aracılığıyla yaptıktan sonra, sayfayı bir tarayıcı aracılığıyla geri ziyaret edin ve Chef Anton s Gumbo Mix için Düzenle düğmesine tıklayın. Şekil 9 ' da gösterildiği gibi, veri bağlama söz dizimi geçerli değerleri TextBox, DropDownLists ve CheckBox içine ekledi.

[Düzenle düğmesine tıklamak ![düzenleme arabirimini görüntüler](customizing-the-datalist-s-editing-interface-cs/_static/image26.png)](customizing-the-datalist-s-editing-interface-cs/_static/image25.png)

**Şekil 9**: Düzenle düğmesine tıkladığınızda düzenleme arabirimi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image27.png))

## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>5\. Adım: Kullanıcı değişikliklerini, UpdateCommand olay Işleyicisine kaydetme

Kullanıcı bir ürünü düzenlediğinde ve Güncelleştir düğmesine tıkladığında, bir geri gönderme gerçekleşir ve DataList `UpdateCommand` olayı başlatılır. Olay İşleyicide, veritabanındaki ürünü güncelleştirmek için `EditItemTemplate` ve arabirimdeki Web denetimlerinden değerleri okuduk. Önceki öğreticilerde gördüğünüz gibi, güncelleştirilmiş ürünün `ProductID` `DataKeys` koleksiyonu aracılığıyla erişilebilir. Aşağıdaki kodun gösterdiği gibi, Kullanıcı tarafından girilen alanlara `FindControl("controlID")`kullanılarak Web denetimlerine programlı olarak başvurulduğunda erişilir:

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample4.cs)]

Kod, sayfadaki tüm doğrulama denetimlerinin geçerli olduğundan emin olmak için `Page.IsValid` özelliğine danışarak başlatılır. `Page.IsValid` `True`, düzenlenen ürün s `ProductID` değeri `DataKeys` koleksiyonundan okunurdur ve `EditItemTemplate` veri girişi Web denetimlerine programlı olarak başvurulur. Daha sonra, bu Web denetimlerinde bulunan değerler, daha sonra uygun `UpdateProduct` aşırı yüklemeye geçirilmiş değişkenlere okunurdur. Veriler güncelleştirildikten sonra DataList, önceden düzenlenen durumuna döndürülür.

> [!NOTE]
> Kodu ve bu örneği odaklanmış tutmak için, [BLL ve dal düzeyi özel](handling-bll-and-dal-level-exceptions-cs.md) durum öğreticisinde eklenen özel durum işleme mantığını atlıyorum. Alıştırma olarak, bu Öğreticiyi tamamladıktan sonra bu işlevselliği ekleyin.

## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>6\. Adım: NULL CategoryID ve SupplierID değerlerini Işleme

Northwind veritabanı, `Products` tablo s `CategoryID` ve `SupplierID` sütunları için `NULL` değerleri sağlar. Ancak, düzen arabirimimiz Şu anda `NULL` değerleri barındıramamaktadır. `CategoryID` veya `SupplierID` sütunları için `NULL` değerine sahip bir ürünü düzenlemeye başladığımızda, şuna benzer bir hata iletisi içeren bir `ArgumentOutOfRangeException` alacaksınız: *' Categories ' öğe listesinde bulunmadığından, geçersiz bir SelectedValue içeriyor.* Ayrıca, şu anda bir ürün kategorisi veya tedarikçi değerini`NULL` olmayan bir değerden `NULL` bir değere değiştirme yolu yoktur.

Kategori ve tedarikçi DropDownLists için `NULL` değerlerini desteklemek üzere, ek bir `ListItem`eklememiz gerekiyor. Bu `ListItem`için `Text` değer olarak (hiçbiri) kullanmayı seçtim, ancak d isterseniz bunu başka bir şekilde (boş bir dize gibi) değiştirebilirsiniz. Son olarak, DropDownLists `AppendDataBoundItems` `True`olarak ayarlamayı unutmayın. Bunu unutursanız, DropDownList 'e Bağlan Kategoriler ve tedarikçiler statik olarak eklenen `ListItem`üzerine yazar.

Bu değişiklikleri yaptıktan sonra, DataList s `EditItemTemplate` ' deki DropDownLists işaretlemesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample5.aspx)]

> [!NOTE]
> Statik `ListItem` s, tasarımcı aracılığıyla veya doğrudan bildirime dayalı sözdizimi aracılığıyla bir DropDownList 'e eklenebilir. Bir veritabanı `NULL` değerini temsil etmek için bir DropDownList öğesi eklenirken, bildirime dayalı söz dizimi aracılığıyla `ListItem` eklediğinizden emin olun. Tasarımcıda `ListItem` koleksiyonu düzenleyicisini kullanıyorsanız, oluşturulan bildirime dayalı sözdizimi, boş bir dize atandığında `Value` ayarını tamamen atlar, şöyle bildirime dayalı biçimlendirme oluşturulur: `<asp:ListItem>(None)</asp:ListItem>`. Bu durum zararsız görünebilir, ancak eksik `Value` DropDownList 'in yerinde `Text` özellik değerini kullanmasına neden olur. Yani, bu `NULL` `ListItem` seçilirse, (Bu öğreticide`CategoryID` veya `SupplierID`, bu öğreticide) değerin (yok), bir özel durumla sonuçlanabileceği anlamına gelir. `Value=""`açıkça ayarlayarak, `NULL` `ListItem` seçildiğinde ürün verileri alanına bir `NULL` değeri atanır.

Bir tarayıcıdan ilerleme durumunu görüntülemek için bir dakikanızı ayırın. Bir ürünü düzenlediğinizde, `Categories` ve `Suppliers` DropDownLists öğesinin her ikisinin de DropDownList başlangıcında bir (None) seçeneği olduğunu unutmayın.

[Kategoriler ve satıcılar DropDownLists ![, (None) seçeneği içerir](customizing-the-datalist-s-editing-interface-cs/_static/image29.png)](customizing-the-datalist-s-editing-interface-cs/_static/image28.png)

**Şekil 10**: `Categories` ve `Suppliers` Dropdownlists (yok) seçeneği içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-datalist-s-editing-interface-cs/_static/image30.png))

(None) seçeneğini bir veritabanı `NULL` değeri olarak kaydetmek için `UpdateCommand` olay işleyicisine dönmemiz gerekiyor. `categoryIDValue` ve `supplierIDValue` değişkenlerini null değer atanabilir tamsayılar olacak şekilde değiştirin ve yalnızca DropDownList s `SelectedValue` boş bir dize değilse `Nothing` dışında bir değer atayın:

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample6.cs)]

Bu değişiklik ile, Kullanıcı bir `NULL` veritabanı değerine karşılık gelen açılan listelerden birinden (hiçbiri) seçeneğini belirlediyseniz, `Nothing` değeri `UpdateProduct` BLL yöntemine geçirilir.

## <a name="summary"></a>Özet

Bu öğreticide, üç farklı giriş Web denetimi içeren bir metin kutusu, iki DropDownLists ve onay kutusu içeren daha karmaşık bir DataList Editing arabirimi oluşturmayı, doğrulama denetimleriyle birlikte gördük. Yapılandırma arabirimini oluştururken, adımlar, kullanılan Web denetimlerinden bağımsız olarak aynıdır: bir Web denetimlerini DataList s 'e ekleyerek başlayın `EditItemTemplate`; uygun Web denetimi özellikleriyle ilgili veri alanı değerlerini atamak için DataBinding sözdizimini kullanın; `UpdateCommand` olay işleyicisinde, Web denetimlerine ve uygun özelliklerine programlı bir şekilde erişin ve değerlerini BLL 'e geçirerek bu özelliklere sahiptir.

Bir düzen arabirimi oluştururken, ister yalnızca metin kutuları, ister farklı Web denetimleri koleksiyonu olsun, veritabanı `NULL` değerlerini doğru şekilde işlediğinizden emin olun. `NULL` s için hesaplama yaparken, yalnızca bir düzen arabiriminde var olan bir `NULL` değerini doğru görüntülemediğinizi ve ayrıca bir değeri `NULL`olarak işaretlemek için bir yol sunuyoruz. Veritecleriyle ilgili olan DropDownLists için genellikle, `Value` özelliği açıkça boş bir dizeye (`Value=""`) ayarlanmış statik bir `ListItem` ekleme ve `UpdateCommand` olay işleyicisine `NULL``ListItem` seçili olup olmadığını belirleme için bir kod ekleme anlamına gelir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler dennıs Patterson, David suru ve Randy SCHMIDT olarak değiştirildi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)
> [İleri](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
