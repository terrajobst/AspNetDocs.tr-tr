---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
title: Veri değişikliği arabirimini özelleştirme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, standart metin kutusu ve CheckBox denetimlerini alternatı ile değiştirerek düzenlenebilir bir GridView 'un arayüzünü nasıl özelleştireceğinizi inceleyeceğiz.
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 4830d984-bd2c-4a08-bfe5-2385599f1f7d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 85ec7bdde6b2bffbbda066b0441bbd36b7072197
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74584924"
---
# <a name="customizing-the-data-modification-interface-vb"></a>Veri Değişikliği Arabirimini Özelleştirme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_VB.exe) veya [PDF 'yi indirin](customizing-the-data-modification-interface-vb/_static/datatutorial20vb1.pdf)

> Bu öğreticide, standart metin kutusu ve CheckBox denetimlerini alternatif giriş Web denetimleriyle değiştirerek, düzenlenebilir bir GridView 'un arayüzünü nasıl özelleştireceğinizi inceleyeceğiz.

## <a name="introduction"></a>Giriş

GridView ve DetailsView tarafından kullanılan BoundFields ve CheckBoxFields alanları, salt okuma, düzenlenebilir ve eklenebilir arabirimleri işleyebilme nedeniyle verileri değiştirme sürecini basitleştirir. Bu arabirimler, ek bildirim temelli biçimlendirme veya kod ekleme gerekmeden işlenebilir. Ancak, BoundField ve CheckBoxField arabirimlerinin, gerçek dünyada senaryolar için genellikle gerekli olan özelleştirme olmaması gerekir. Bir GridView veya DetailsView içindeki düzenlenebilir veya Insertable arabirimini özelleştirmek için bunun yerine TemplateField kullanılması gerekir.

[Önceki öğreticide](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) , doğrulama Web denetimleri ekleyerek veri değiştirme arabirimlerini özelleştirmeyi gördük. Bu öğreticide, gerçek veri toplama Web denetimlerini nasıl özelleştireceğiz, BoundField ve CheckBoxField 'ın standart metin kutusu ve CheckBox denetimlerini alternatif giriş Web denetimleriyle değiştirme bölümüne bakacağız. Özellikle, bir ürünün adı, kategorisi, tedarikçisi ve Discontinued durumunun güncelleştirilmesini sağlayan düzenlenebilir bir GridView oluşturacağız. Belirli bir satırı düzenlediğinizde, kategori ve tedarikçi alanları, aralarından seçim yapabileceğiniz kullanılabilir kategori ve tedarikçiler kümesini içeren DropDownLists olarak işlenir. Ayrıca, CheckBoxField 'ın varsayılan onay kutusunu iki seçenek sunan bir RadioButtonList denetimiyle değiştireceğiz: "etkin" ve "Discontinued".

[GridView 'un Düzenle arabirimi ![DropDownLists ve RadioButtons Içerir](customizing-the-data-modification-interface-vb/_static/image2.png)](customizing-the-data-modification-interface-vb/_static/image1.png)

**Şekil 1**: GridView 'ın düzenleyen arabirimi Dropdownlists ve RadioButtons içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image3.png))

## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>1\. Adım: uygun`UpdateProduct`aşırı yüklemeyi oluşturma

Bu öğreticide, bir ürünün adı, kategorisi, tedarikçisini ve Discontinued durumunun düzenlenmesine izin veren düzenlenebilir bir GridView oluşturacağız. Bu nedenle, bu dört ürün değerini ve `ProductID`beş giriş parametresi kabul eden bir `UpdateProduct` aşırı yüklemeye ihtiyacımız var. Önceki yüklerimizde olduğu gibi, şöyle olacaktır:

1. Belirtilen `ProductID`için veritabanından ürün bilgilerini alın,
2. `ProductName`, `CategoryID`, `SupplierID`ve `Discontinued` alanlarını güncelleştirin ve
3. TableAdapter 'ın `Update()` yöntemi aracılığıyla, güncelleştirme isteğini DAL 'ye gönderin.

Breçekimi için, bu belirli aşırı yükte, bir ürünün artık üretici tarafından sunulan tek ürün olmadığı için iş kuralı denetimini atlıyorum. Mantığınızı tercih ediyorsanız veya, ideal olarak, mantığı ayrı bir yönteme yeniden ekleyerek ekleyebilirsiniz.

Aşağıdaki kod, `ProductsBLL` sınıfındaki yeni `UpdateProduct` aşırı yüklemeyi gösterir:

[!code-vb[Main](customizing-the-data-modification-interface-vb/samples/sample1.vb)]

## <a name="step-2-crafting-the-editable-gridview"></a>2\. Adım: düzenlenebilir GridView taslağı oluşturma

`UpdateProduct` aşırı yüklemesi eklendiğinde, düzenlenebilir GridView sitemizi oluşturmaya hazırız. `EditInsertDelete` klasöründeki `CustomizedUI.aspx` sayfasını açın ve tasarımcıya bir GridView denetimi ekleyin. Sonra, GridView 'un akıllı etiketinden yeni bir ObjectDataSource oluşturun. `ProductBLL` sınıfının `GetProducts()` yöntemi aracılığıyla ürün bilgilerini almak ve yeni oluşturduğumuz `UpdateProduct` aşırı yüklemesini kullanarak ürün verilerini güncelleştirmek için ObjectDataSource 'ı yapılandırın. Ekle ve SIL sekmelerinden açılan listelerden (hiçbiri) seçeneğini belirleyin.

[![, yeni oluşturulan UpdateProduct Overload 'ı kullanmak üzere ObjectDataSource 'u yapılandırmak için](customizing-the-data-modification-interface-vb/_static/image5.png)](customizing-the-data-modification-interface-vb/_static/image4.png)

**Şekil 2**: ObjectDataSource 'ı yeni oluşturulan `UpdateProduct` aşırı yüklemeyi kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image6.png))

Veri değiştirme öğreticilerinin tamamında gördüğimize göre, Visual Studio tarafından oluşturulan ObjectDataSource için bildirime dayalı sözdizimi, `original_{0}``OldValuesParameterFormatString` özelliğini atar. Bu şekilde, yöntemlerimiz orijinal `ProductID` değerinin geçirilmesini beklemediği için Iş mantığı Katmanımızla birlikte çalışmaz. Bu nedenle, önceki öğreticilerde yaptığımız gibi, bu özellik atamasını bildirime dayalı sözdiziminden kaldırmak için bir dakikanızı ayırın veya bunun yerine bu özelliğin değerini `{0}`olarak ayarlayın.

Bu değişiklikten sonra, ObjectDataSource 'un bildirim temelli işaretleme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample2.aspx)]

`OldValuesParameterFormatString` özelliğinin kaldırıldığını ve `UpdateProduct` aşırı yükümüzü tarafından beklenen giriş parametrelerinin her biri için `UpdateParameters` koleksiyonunda bir `Parameter` olduğunu unutmayın.

ObjectDataSource, ürün değerlerinin yalnızca bir alt kümesini güncelleştirmek üzere yapılandırıldığında, GridView Şu anda *Tüm* ürün alanlarını gösterir. GridView 'ı düzenlemek için biraz zaman ayırın:

- Yalnızca `ProductName`, `SupplierName`, `CategoryName` BoundFields ve `Discontinued` CheckBoxField 'ı içerir
- `CategoryName` ve `SupplierName` alanlar `Discontinued` CheckBoxField 'dan önce (solunda) görünür
- `CategoryName` ve `SupplierName` BoundFields ' `HeaderText` özelliği sırasıyla "Category" ve "tedarikçinin" olarak ayarlanmıştır
- Düzen desteği etkin (GridView 'un akıllı etiketinde Düzenle onay kutusunu işaretleyin)

Bu değişikliklerden sonra, tasarımcı aşağıda gösterilen GridView 'un bildirime dayalı sözdizimi ile şekil 3 ' e benzer.

[Gereksiz alanları GridView 'dan kaldırmak ![](customizing-the-data-modification-interface-vb/_static/image8.png)](customizing-the-data-modification-interface-vb/_static/image7.png)

**Şekil 3**: GridView 'Daki gereksiz alanları kaldırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image9.png))

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample3.aspx)]

Bu noktada, GridView 'un salt okunurdur davranışı tamamlanmıştır. Veriler görüntülenirken, her ürün GridView 'da bir satır olarak işlenir ve ürünün adı, kategorisi, tedarikçisi ve Discontinued durumunu gösterir.

[GridView 'un salt okunurdur arabirimi ![Tamam](customizing-the-data-modification-interface-vb/_static/image11.png)](customizing-the-data-modification-interface-vb/_static/image10.png)

**Şekil 4**: GridView 'un salt okunurdur arabirimi tamamlanmıştır ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image12.png))

> [!NOTE]
> [Veri öğreticisini ekleme, güncelleştirme ve silmeye genel bakış](an-overview-of-inserting-updating-and-deleting-data-cs.md)konusunda anlatıldığı gibi, GridView s görüntüleme durumunun etkinleştirilmesi (varsayılan davranış) açısından önemli değildir. GridView s `EnableViewState` özelliğini `false`olarak ayarlarsanız, eşzamanlı kullanıcıların kayıtları yanlışlıkla silmesini veya düzenlemesini sağlamak için bir risk çalıştırırsınız. Daha fazla bilgi için bkz. [Uyarı: ASP.NET 2,0 GridViews/DetailsView/formviews ile, görüntüleme ve/veya silme ve görünüm durumunu devre dışı bırakma desteği](http://scottonwriting.net/sowblog/posts/10054.aspx) .

## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>3\. Adım: Kategori ve tedarikçi düzenlemesi arabirimleri için DropDownList kullanma

`ProductsRow` nesnesinin `CategoryID`, `CategoryName`, `SupplierID`ve `SupplierName` özelliklerini içerdiğini, `Products` veritabanı tablosundaki gerçek yabancı anahtar KIMLIĞI değerlerini ve `Name` ve `Categories` tablolarında karşılık gelen `Suppliers` değerlerini sağlayan özelliklerini içerdiğini unutmayın. `ProductRow``CategoryID` ve `SupplierID` her ikisi de okunabilir ve yazılır, ancak `CategoryName` ve `SupplierName` özellikleri salt okunurdur olarak işaretlenir.

`CategoryName` ve `SupplierName` özelliklerinin salt okuma durumu nedeniyle, karşılık gelen BoundFields `ReadOnly` özelliği `True`olarak ayarlanmıştır, bu değerlerin bir satır düzenlendiğinde değiştirilmesini önler. `ReadOnly` özelliğini `False`, `CategoryName` ve `SupplierName` BoundFields alanlarını düzenlenmek üzere metin olarak ayarlayabiliriz. ancak, bu tür bir yaklaşım, `UpdateProduct` ve `CategoryName` girişleri alan `SupplierName` aşırı yüklemesi olmadığından, Kullanıcı ürünü güncelleştirmeye çalıştığında bir özel durum oluşmasına neden olur. Aslında, iki nedenden dolayı böyle bir aşırı yükleme oluşturmak istemezsiniz:

- `Products` tabloda `SupplierName` veya `CategoryName` alanları yoktur, ancak `SupplierID` ve `CategoryID`. Bu nedenle, yöntetiğimiz bu belirli KIMLIK değerlerini (arama tablolarının değerlerini değil) geçirilmesini istiyoruz.
- Kullanıcının, kullanılabilir kategorileri ve tedarikçileri ve doğru yazımlar hakkında bilgi sahibi olması gerektiğinden, tedarikçinin veya kategorinin adını belirtmesini gerektirmek ideal olandan daha küçüktür.

Tedarikçi ve kategori alanları, salt okuma modunda (şimdi olduğu gibi) kategori ve tedarikçiler adlarını ve düzenleme sırasında uygulanabilir seçeneklerin açılan listesini görüntülemelidir. Son Kullanıcı, bir açılan liste kullanarak, arasından seçim yapabileceğiniz kategorileri ve tedarikçileri hızla görebilir ve seçimini daha kolay hale getirebilirler.

Bu davranışı sağlamak için, `SupplierName` ve `CategoryName` BoundFields alanlarını `ItemTemplate` `SupplierName` ve `CategoryName` değerlerini yayar ve `EditItemTemplate` kullanılabilir kategorileri ve tedarikçileri listelemek için bir DropDownList denetimi kullanan Templatealanlara dönüştürmemiz gerekir.

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>`Categories`ve`Suppliers`DropDownLists ekleme

`SupplierName` ve `CategoryName` BoundFields alanlarını TemplateFields 'e dönüştürerek: GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayarak başlatın; sol alt taraftaki listeden BoundField seçiliyor; ve "Bu alanı TemplateField 'a Dönüştür" bağlantısına tıklayın. Dönüştürme işlemi, aşağıdaki bildirime dayalı sözdiziminde gösterildiği gibi hem `ItemTemplate` hem de `EditItemTemplate`bir TemplateField oluşturacaktır:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample4.aspx)]

BoundField salt okunurdur olarak işaretlendiğinden, hem `ItemTemplate` hem de `EditItemTemplate`, `Text` özelliği geçerli veri alanına (`CategoryName`, Yukarıdaki sözdiziminde) bağlantılı olan bir etiket Web denetimi içerir. Label Web denetimini bir DropDownList denetimiyle değiştirerek `EditItemTemplate`değiştirmemiz gerekiyor.

Önceki öğreticilerde gördüğünüze göre, şablon tasarımcı aracılığıyla veya doğrudan bildirime dayalı sözdiziminden düzenlenebilir. Tasarımcı aracılığıyla düzenlemek için GridView 'un akıllı etiketindeki Şablonları Düzenle bağlantısına tıklayın ve Kategori alanının `EditItemTemplate`birlikte çalışmayı seçin. Etiket Web denetimini kaldırın ve bir DropDownList denetimiyle değiştirin, DropDownList 'in ID özelliği `Categories`olarak ayarlanıyor.

[![TexBox 'ı kaldırıp EditItemTemplate 'e bir DropDownList ekleyin](customizing-the-data-modification-interface-vb/_static/image14.png)](customizing-the-data-modification-interface-vb/_static/image13.png)

**Şekil 5**: texbox 'ı kaldırın ve `EditItemTemplate` bir DropDownList ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image15.png))

Daha sonra DropDownList 'i kullanılabilir kategorilerle doldurmamız gerekir. DropDownList 'in akıllı etiketindeki veri kaynağı Seç bağlantısına tıklayın ve `CategoriesDataSource`adlı yeni bir ObjectDataSource oluşturmayı tercih edin.

[![CategoriesDataSource adlı yeni bir ObjectDataSource denetimi oluşturma](customizing-the-data-modification-interface-vb/_static/image17.png)](customizing-the-data-modification-interface-vb/_static/image16.png)

**Şekil 6**: `CategoriesDataSource` adlı yeni bir ObjectDataSource denetimi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image18.png))

Bu ObjectDataSource 'un tüm kategorileri döndürmesini sağlamak için, `CategoriesBLL` sınıfın `GetCategories()` yöntemine bağlayın.

[![, ObjectDataSource 'a CategoriesBLL 'nin GetCategories () metoduna bağlama](customizing-the-data-modification-interface-vb/_static/image20.png)](customizing-the-data-modification-interface-vb/_static/image19.png)

**Şekil 7**: ObjectDataSource `CategoriesBLL``GetCategories()` yöntemine bağlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image21.png))

Son olarak, DropDownList ayarlarını, `CategoryName` alanı her bir DropDownList `ListItem`, değer olarak kullanılan `CategoryID` alanıyla birlikte görüntülenmek üzere yapılandırın.

[![CategoryName alanı ve değer olarak kullanılan KategoriNo](customizing-the-data-modification-interface-vb/_static/image23.png)](customizing-the-data-modification-interface-vb/_static/image22.png)

**Şekil 8**: `CategoryName` alanın görüntülendiğini ve değer olarak kullanılan `CategoryID` ([tam boyutlu görüntüyü görüntülemek için tıklatın](customizing-the-data-modification-interface-vb/_static/image24.png))

Bu değişiklikleri yaptıktan sonra, `CategoryName` TemplateField içindeki `EditItemTemplate` için bildirime dayalı biçimlendirme hem DropDownList hem de ObjectDataSource içerecektir:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> `EditItemTemplate` DropDownList 'in görünüm durumunun etkin olması gerekir. Yeni veri bağlama sözdizimini DropDownList 'in bildirime dayalı sözdizimine ve `Eval()` gibi veri bağlama komutlarına ekleyeceğiz, `Bind()` yalnızca görünüm durumu etkin olan denetimlerde görünebilir.

`SupplierName` TemplateField `EditItemTemplate``Suppliers` adlı bir DropDownList eklemek için bu adımları tekrarlayın. Bu, `EditItemTemplate` bir DropDownList eklemeyi ve başka bir ObjectDataSource oluşturmayı kapsar. Ancak `Suppliers` DropDownList 'in ObjectDataSource, `SuppliersBLL` sınıfının `GetSuppliers()` yöntemini çağırmak üzere yapılandırılmalıdır. Ayrıca, `Suppliers` DropDownList öğesini `CompanyName` alanını görüntüleyecek şekilde yapılandırın ve `SupplierID` alanını `ListItem` s değeri olarak kullanın.

İki `EditItemTemplate` için DropDownLists eklendikten sonra, sayfayı bir tarayıcıya yükleyin ve Chef Anton 'ın Cajun Mevsiming ürünü için Düzenle düğmesine tıklayın. Şekil 9 ' da gösterildiği gibi, ürünün kategorisi ve tedarikçi sütunları, aralarından seçim yapabileceğiniz kullanılabilir kategorileri ve tedarikçileri içeren açılır listeler olarak işlenir. Ancak, her iki açılır listedeki *ilk* öğe varsayılan olarak (tedarikçi olarak kategori ve Exotic Litids) seçili olduğunu, ancak Chef Anton 'ın, yeni Orleans Cajun Delights tarafından sağlanan bir koşullu engel olmasına rağmen.

[aşağı açılan listelerdeki Ilk öğe ![varsayılan olarak seçilidir](customizing-the-data-modification-interface-vb/_static/image26.png)](customizing-the-data-modification-interface-vb/_static/image25.png)

**Şekil 9**: açılan listelerdeki Ilk öğe varsayılan olarak seçilidir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image27.png))

Ayrıca, Güncelleştir ' e tıkladığınızda, ürünün `CategoryID` ve `SupplierID` değerlerinin `NULL`olarak ayarlandığını görürsünüz. Bu istenmeyen davranışların her ikisi de `EditItemTemplate` s içindeki DropDownLists, temel alınan ürün verilerinden herhangi bir veri alanına bağlanmadığından oluşur.

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>DropDownLists`CategoryID`ve`SupplierID`veri alanlarına bağlama

Düzenlenmiş ürünün kategori ve tedarikçi açılan listelerinin uygun değerlere ayarlanmış olması ve bu değerlerin güncelleştirme ' ye tıklandıktan sonra BLL 'nin `UpdateProduct` yöntemine geri gönderilmesini sağlamak için, DropDownLists ' `SelectedValue` özelliklerini iki yönlü veri bağlamayı kullanarak `CategoryID` ve `SupplierID` veri alanlarına bağlamanız gerekir. Bunu `Categories` DropDownList ile başarmak için, bildirime dayalı sözdizimine doğrudan `SelectedValue='<%# Bind("CategoryID") %>'` ekleyebilirsiniz.

Alternatif olarak, tasarımcı aracılığıyla şablonu düzenleyerek ve DropDownList 'in akıllı etiketindeki DataBindings 'i düzenle bağlantısına tıklayarak DropDownList 'in DataBindings 'i ayarlayabilirsiniz. Sonra, `SelectedValue` özelliğinin iki yönlü veri bağlama (bkz. Şekil 10) kullanarak `CategoryID` alanına bağlanması gerektiğini gösterir. `SupplierID` veri alanını `Suppliers` DropDownList 'e bağlamak için bildirim temelli ya da tasarımcı işlemini tekrarlayın.

[CategoryID 'yi, Iki yönlü veri bağlamayı kullanarak DropDownList 'in SelectedValue özelliğine bağlama ![](customizing-the-data-modification-interface-vb/_static/image29.png)](customizing-the-data-modification-interface-vb/_static/image28.png)

**Şekil 10**: Iki yönlü veri bağlama kullanarak `CategoryID` DropDownList 'In `SelectedValue` özelliğine bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image30.png))

Bağlamalar iki DropDownLists 'ın `SelectedValue` özelliklerine uygulandıktan sonra, düzenlenen ürünün kategorisi ve tedarikçi sütunları varsayılan olarak geçerli ürünün değerlerini sağlar. Güncelleştirme ' ye tıklandıktan sonra, seçili açılan liste öğesinin `CategoryID` ve `SupplierID` değerleri `UpdateProduct` yöntemine geçirilir. Şekil 11 ' de veri bağlama deyimleri eklendikten sonra öğretici gösterilmektedir; Chef Anton 'ın Cajun sezonu için seçilen aşağı açılan liste öğelerinin doğru bir şekilde ve yeni Orleans Cajun Delights olduğunu aklınızda edin.

[Düzenlenen ürünün geçerli kategorisi ve tedarikçinin değerleri varsayılan olarak seçilidir ![](customizing-the-data-modification-interface-vb/_static/image32.png)](customizing-the-data-modification-interface-vb/_static/image31.png)

**Şekil 11**: düzenlenmiş ürünün geçerli kategorisi ve tedarikçi değerleri varsayılan olarak seçilidir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image33.png))

## <a name="handlingnullvalues"></a>`NULL`değerlerini işleme

`Products` tablosundaki `CategoryID` ve `SupplierID` sütunları `NULL`olabilir, ancak `EditItemTemplate` bir değeri temsil etmek için bir liste öğesi dahil değildir. Bu iki sonuçlara sahiptir:

- Kullanıcı, bir ürünün kategorisini veya tedarikçisine`NULL` olmayan bir değerden `NULL` birine değiştirmek için arabirimimizi kullanamaz
- Bir üründe `NULL` `CategoryID` veya `SupplierID`varsa, Düzenle düğmesine tıkladığınızda bir özel durum ortaya kalır. Bunun nedeni, `Bind()` deyimindeki `CategoryID` (veya `SupplierID`) tarafından döndürülen `NULL` değerin DropDownList içindeki bir değere eşlenmediği durumdur (DropDownList, `SelectedValue` özelliği liste öğeleri koleksiyonunda *olmayan* bir değere ayarlandığında bir özel durum oluşturur).

`NULL` `CategoryID` ve `SupplierID` değerlerini desteklemek için her DropDownList 'e başka bir `ListItem` eklememiz gerekir. Bu, `NULL` değerini temsil eder. DropDownList öğreticisi [Ile ana/ayrıntı filtrelemesinde](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) , dropdownlist 'in `AppendDataBoundItems` özelliğini `True` olarak ayarlamayı ve ek `ListItem`el ile eklemeyi kapsayan bir veri bağlama DropDownList 'e nasıl ek `ListItem` ekleneceğini gördük. Bununla birlikte, bu önceki öğreticide, `-1``Value` bir `ListItem` ekledik. Ancak, ASP.NET ' deki veri bağlama mantığı, boş bir dizeyi `NULL` değerine otomatik olarak dönüştürecek ve tam tersi olur. Bu nedenle, bu öğreticide `ListItem``Value` boş bir dize olmasını istiyoruz.

Her iki DropDownLists ' `AppendDataBoundItems` özelliğini `True`olarak ayarlayarak başlayın. Sonra, bildirim biçimlendirmesinin şöyle görünmesi için her bir DropDownList 'e aşağıdaki `<asp:ListItem>` öğesini ekleyerek `NULL` `ListItem` ekleyin:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample6.aspx)]

Bu `ListItem`için metin değeri olarak "(None)" kullanmayı seçtim, ancak isterseniz de boş bir dize olacak şekilde değiştirebilirsiniz.

> [!NOTE]
> *Bir DropDownList öğreticisi Ile ana/ayrıntı filtrelemesinde* gördüğünüz gibi, `ListItem` s bir DropDownList 'e, Özellikler penceresi dropdownlist 'in `Items` özelliğine tıklayarak (`ListItem` koleksiyonu düzenleyicisini görüntüleyen) bir DropDownList 'e eklenebilir. Ancak bildirim temelli söz dizimi aracılığıyla Bu öğreticinin `NULL` `ListItem` eklediğinizden emin olun. `ListItem` koleksiyonu düzenleyicisini kullanıyorsanız, oluşturulan bildirime dayalı sözdizimi, boş bir dize atandığında `Value` ayarını tamamen atlar, şöyle bildirime dayalı biçimlendirme oluşturulur: `<asp:ListItem>(None)</asp:ListItem>`. Bu durum zararsız görünebilir, ancak eksik değer DropDownList 'in yerinde `Text` özellik değerini kullanmasına neden olur. Yani bu `NULL` `ListItem` seçilmişse, "(None)" değerinin `CategoryID`atanması denenmeyeceği anlamına gelir. Bu, özel durum ile sonuçlanır. `Value=""`açıkça ayarlayarak, `NULL` `ListItem` seçildiğinde `CategoryID` `NULL` bir değer atanır.

Suppliers DropDownList için bu adımları tekrarlayın.

Bu ek `ListItem`, düzen arabirimi artık Şekil 12 ' de gösterildiği gibi, bir ürünün `CategoryID` ve `SupplierID` alanlarına `NULL` değerleri atayabilirler.

[Ürünün kategorisine veya sağlayıcısına NULL değer atamak için ![(yok) seçeneğini belirleyin](customizing-the-data-modification-interface-vb/_static/image35.png)](customizing-the-data-modification-interface-vb/_static/image34.png)

**Şekil 12**: bir ürünün kategorisine veya sağlayıcısına `NULL` değer atamak Için (hiçbiri) seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image36.png))

## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>4\. Adım: Discontinued durumu için RadioButton kullanma

Şu anda products ' `Discontinued` Data alanı, salt okunurdur ve düzenlenmekte olan satır için etkin onay kutusu için devre dışı bir onay kutusu oluşturan CheckBoxField kullanılarak ifade edilir. Bu Kullanıcı Arabirimi genellikle uygun olsa da, bir TemplateField kullanarak gerekirse özelleştirebiliriz. Bu öğreticide, kullanıcının ürünün `Discontinued` değerini belirtebileceğiniz iki seçenek olan "etkin" ve "kullanımdan kaldırıldı" olarak, CheckBoxField 'ı bir RadioButtonList denetimi kullanan TemplateField olarak değiştirelim.

`Discontinued` CheckBoxField ' ı bir TemplateField ' a dönüştürerek `ItemTemplate` ve `EditItemTemplate`bir TemplateField oluşturacak şekilde başlatın. Her iki şablon da `Discontinued` veri alanına bağlanan `Checked` özelliğini içeren bir onay kutusu içerir. Bu, `ItemTemplate`onay kutusunun `Enabled` özelliğinin `False`olarak ayarlandığı tek fark.

Hem `ItemTemplate` hem de `EditItemTemplate` onay kutusunu bir RadioButtonList denetimiyle değiştirin, hem RadioButtonLists ' `ID` özelliklerini `DiscontinuedChoice`olarak ayarlayarak. Sonra, RadioButtonLists her biri, "false" değeri ve "Discontinued" etiketli "bir" true "değeri ile bir" etkin "etiketlenmiş iki radyo düğmesi içereceğini gösterir. Bunu gerçekleştirmek için, doğrudan bildirim temelli söz dizimi aracılığıyla `<asp:ListItem>` öğelerini girebilir veya tasarımcıdan `ListItem` koleksiyonu düzenleyicisini kullanabilirsiniz. Şekil 13 ' te, iki radyo düğmesi seçeneği belirtildiğinde `ListItem` koleksiyonu Düzenleyicisi gösterilmektedir.

[![etkin ve Discontinued seçeneklerini RadioButtonList 'e ekleme](customizing-the-data-modification-interface-vb/_static/image38.png)](customizing-the-data-modification-interface-vb/_static/image37.png)

**Şekil 13**: RadioButtonList 'e etkin ve Discontinued seçenekleri ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image39.png))

`ItemTemplate` içindeki RadioButtonList düzenlenememesi nedeniyle, `Enabled` özelliğini `False`olarak ayarlayın ve `Enabled` özelliğini `True` `EditItemTemplate`(varsayılan) olarak bırakın. Bu, radyo düğmelerini düzenlenmeyen satırda salt okunurdur, ancak kullanıcının düzenlenen satır için RadioButton değerlerini değiştirmesine izin verir.

Ürünün `Discontinued` Data alanına bağlı olarak uygun radyo düğmesinin seçilmesi için, hala RadioButtonList denetimlerini ' `SelectedValue` özelliklerini atacağız. Bu öğreticide daha önce incelenmekte olan DropDownLists gibi, bu veri bağlama söz dizimi doğrudan bildirim temelli biçimlendirmeye eklenebilir ya da RadioButtonLists ' akıllı etiketlerindeki DataBindings düzenleme bağlantısı aracılığıyla doğrudan eklenebilir.

İki RadioButtonLists ekleyip yapılandırdıktan sonra, `Discontinued` TemplateField 'ın bildirim temelli işaretleme şöyle görünmelidir:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample7.aspx)]

Bu değişikliklerle `Discontinued` sütunu, bir onay kutusu listesinden radyo düğmesi çiftleri listesine dönüştürüldü (bkz. Şekil 14). Bir ürünü düzenlediğinizde, uygun radyo düğmesi seçilir ve ürünün Discontinued durumu diğer radyo düğmesini seçip Güncelleştir ' i tıklatarak güncellenebilir.

[![Discontinued onay kutuları radyo düğmesi çiftlerine göre değiştirilmiştir](customizing-the-data-modification-interface-vb/_static/image41.png)](customizing-the-data-modification-interface-vb/_static/image40.png)

**Şekil 14**: Discontinued onay kutuları radyo düğmesi çiftlerine göre değiştirilmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](customizing-the-data-modification-interface-vb/_static/image42.png))

> [!NOTE]
> `Products` veritabanındaki `Discontinued` sütununda `NULL` değeri olmadığından, arabirimdeki `NULL` bilgileri yakalamaya endişelenmemiz gerekmiyor. Ancak, `Discontinued` sütunu `NULL` değerler içeriyorsa, `Value`, kategori ve tedarikçi DropDownLists gibi boş bir dizeye (`Value=""`) ayarlanmış olan listeye bir üçüncü radyo düğmesi eklemek istiyoruz.

## <a name="summary"></a>Özet

BoundField ve CheckBoxField, salt okunurdur, düzenledikten ve ekleme arabirimlerini otomatik olarak işlerken, özelleştirme yeteneği yoktur. Genellikle, (Bu öğreticide gördüğünüz gibi) veya veri toplama Kullanıcı arabirimini özelleştirerek (Bu öğreticide gördüğümüz gibi), düzen veya ekleme arabirimini özelleştirmeniz gerekir. Arabirimi TemplateField ile özelleştirmek aşağıdaki adımlarda toplanabilir:

1. TemplateField ekleme veya var olan bir BoundField veya CheckBoxField 'ı TemplateField 'a dönüştürme
2. Gerekli olduğu gibi arabirimi artırmak
3. Uygun veri alanlarını iki yönlü veri bağlamayı kullanarak yeni eklenen Web denetimlerine bağlama

Yerleşik ASP.NET Web denetimlerini kullanmanın yanı sıra, bir TemplateField şablonlarını özel, derlenen sunucu denetimleriyle ve Kullanıcı denetimleriyle de özelleştirebilirsiniz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
> [İleri](implementing-optimistic-concurrency-vb.md)
