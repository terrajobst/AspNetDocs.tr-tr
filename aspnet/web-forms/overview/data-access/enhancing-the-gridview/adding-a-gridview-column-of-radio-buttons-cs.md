---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
title: Radyo düğmelerinin GridView sütununu ekleme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğretici, kullanıcıya tek bir satırı seçmenin daha sezgisel bir yolunu sağlamak için bir GridView denetimine radyo düğmelerinin bir sütununu ekleme konusunda bilgi sağlamaktadır...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 32377145-ec25-4715-8370-a1c590a331d5
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
msc.type: authoredcontent
ms.openlocfilehash: b59cc64b14c6414e6558fdb8a281644db8386701
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593249"
---
# <a name="adding-a-gridview-column-of-radio-buttons-c"></a>Radyo Düğmelerinden Oluşan GridView Sütunu Ekleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_CS.exe) veya [PDF 'yi indirin](adding-a-gridview-column-of-radio-buttons-cs/_static/datatutorial51cs1.pdf)

> Bu öğretici, kullanıcıya GridView 'un tek bir satırını seçmenin daha sezgisel bir yolunu sağlamak için bir GridView denetimine radyo düğmelerinin bir sütununu ekleme konusunda bilgi sağlamaktadır.

## <a name="introduction"></a>Giriş

GridView denetimi, yerleşik işlevsellikten oluşan harika bir işlem sunar. Metin, resim, köprü ve düğme görüntülemek için bir dizi farklı alan içerir. Daha fazla özelleştirme için şablonları destekler. Fareyi birkaç tıklamayla, her satırın bir düğme aracılığıyla seçilebileceği ya da düzenlemenin veya silme yeteneklerini etkinleştirebileceğiniz bir GridView oluşturmak mümkün. Sunulan özelliklerin Plethora olmasına rağmen, genellikle ek, desteklenmeyen özelliklerin eklenmesi gereken durumlar olacaktır. Bu öğreticide ve sonraki iki adımda, ek özellikleri eklemek için GridView s işlevselliğinin nasıl geliştireceğiz anlatılmaktadır.

Bu öğretici ve bir sonraki adım, satır seçme işlemini geliştirmeyle odaklanılmıştır. [Ayrıntı ayrıntısı görünümü Ile seçilebilir bir ana GridView kullanan ana/ayrıntı](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)bölümünde incelenen gibi, GridView öğesine bir SELECT düğmesi Içeren bir CommandField ekleyebiliriz. Tıklandığında, bir geri gönderme ve GridView s `SelectedIndex` özelliği, Select düğmesine tıklanmış olan satırın dizinine güncelleştirilir. [Ayrıntı ayrıntısı görünümü öğreticisi Ile seçilebilir bir ana GridView kullanan ana/ayrıntı](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) bölümünde, bu özelliğin seçili GridView satırı ayrıntılarını görüntülemek için nasıl kullanılacağını gördük.

Seçim düğmesi birçok durumda çalışırken, diğerleri için de çalışmayabilir. Düğme kullanmak yerine, genellikle seçim için iki diğer kullanıcı arabirimi öğesi kullanılır: radyo düğmesi ve onay kutusu. GridView 'u, bir seçim düğmesi yerine, her satır bir radyo düğmesi veya onay kutusu içerecek şekilde artırabilir. Kullanıcının GridView kayıtlardan yalnızca birini seçebileceğiniz senaryolarda, radyo düğmesi seçim düğmesi üzerinde tercih edilebilir. Kullanıcının, Web tabanlı bir e-posta uygulamasında gibi birden çok kaydı seçip seçmediği durumlarda, kullanıcının onay kutusu silmek üzere birden çok ileti seçmek istediği durumlarda, seçme düğmesi veya radyo düğmesinden kullanılamayan işlevselliği sunar. Kullanıcı arabirimleri.

Bu öğretici, GridView 'a radyo düğmelerinin bir sütununu ekleme konusunda size bakar. Devam öğreticisi, onay kutularını kullanmayı araştırır.

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>Adım 1: GridView Web sayfalarını geliştirme oluşturma

GridView 'u radyo düğmelerinin bir sütununu içerecek şekilde geliştirmeyle önce, Web sitesi projemizdeki Bu öğretici ve sonraki iki için gereken ASP.NET sayfalarını oluşturmak için önce bir süre sürme. `EnhancedGridView`adlı yeni bir klasör ekleyerek başlayın. Ardından, aşağıdaki ASP.NET sayfalarını bu klasöre ekleyerek her bir sayfayı `Site.master` ana sayfasıyla ilişkilendirdiğinizden emin olun:

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`

![SqlDataSource ile Ilgili öğreticiler için ASP.NET sayfaları ekleyin](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.gif)

**Şekil 1**: SqlDataSource Ile ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `EnhancedGridView` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.png)

**Şekil 2**: `SectionLevelTutorialListing.ascx` kullanıcı denetimini `Default.aspx` ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.png))

Son olarak, bu dört sayfayı `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, SqlDataSource denetim `<siteMapNode>`kullanarak aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık öğreticilerin düzenlenmesine, eklemeye ve silinmesine yönelik öğeler içerir.

![Site Haritası artık GridView öğreticilerini geliştirmeyle ilgili girişler Içeriyor](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.gif)

**Şekil 3**: site haritası artık GridView öğreticilerini geliştirmeyle Ilgili girişler içeriyor

## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>2\. Adım: tedarikçileri bir GridView 'da görüntüleme

Bu öğretici için, her bir GridView satırı radyo düğmesi sunarak ABD 'deki tedarikçileri listeleyen bir GridView derlemenize olanak tanır. Radyo düğmesi aracılığıyla bir tedarikçi seçtikten sonra, Kullanıcı bir düğmeye tıklayarak tedarikçinin s ürünlerini görüntüleyebilir. Bu görev önemsiz bir işlem olsa da, özellikle karmaşık hale getirmek için çok sayıda alt tzellikleri vardır. Bu alt tçilere göre Delve yapmadan önce, tedarikçilerini listelemek için öncelikle bir GridView 'u alın.

Araç kutusundan Tasarımcı üzerine bir GridView sürükleyerek `EnhancedGridView` klasöründeki `RadioButtonField.aspx` sayfasını açın. GridView s `ID` `Suppliers` ve akıllı etiketinden, yeni bir veri kaynağı oluşturmayı seçin. Özellikle, `SuppliersBLL` nesnesinden verilerini çeken `SuppliersDataSource` adlı bir ObjectDataSource oluşturun.

[SuppliersDataSource adlı yeni bir ObjectDataSource oluşturma ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.png)

**Şekil 4**: `SuppliersDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.png))

[SuppliersBLL sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.png)

**Şekil 5**: ObjectDataSource 'ı `SuppliersBLL` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.png))

Bu tedarikçileri yalnızca ABD 'de listelemek istiyoruz, Seç sekmesinde açılan listeden `GetSuppliersByCountry(country)` yöntemini seçin.

[SuppliersBLL sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.png)

**Şekil 6**: `SuppliersBLL` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.png))

GÜNCELLEŞTIRME sekmesinden (yok) seçeneğini belirleyin ve Ileri ' ye tıklayın.

[SuppliersBLL sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.png)

**Şekil 7**: ObjectDataSource 'ı `SuppliersBLL` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.png))

`GetSuppliersByCountry(country)` yöntemi bir parametreyi kabul ettiğinden, veri kaynağını yapılandırma Sihirbazı bize bu parametrenin kaynağını ister. Sabit kodlanmış bir değer belirtmek için (Bu örnekte, bu örnekte), parametre kaynağı açılır listesini hiçbiri olarak ayarlayın ve metin kutusuna varsayılan değeri girin. Sihirbazı tamamladığınızda son ' a tıklayın.

[![, ülke parametresi için varsayılan değer olarak ABD 'yi kullanır](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.png)

**Şekil 8**: `country` parametresi Için varsayılan değer olarak USA kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.png))

Sihirbazı tamamladıktan sonra GridView, her bir tedarikçi veri alanı için bir BoundField içerir. `CompanyName`, `City`ve `Country` BoundFields hariç tümünü kaldırın ve `CompanyName` BoundFields `HeaderText` özelliğini tedarikçi olarak yeniden adlandırın. Bunu yaptıktan sonra GridView ve ObjectDataSource açıklayıcı sözdizimi aşağıdakine benzer şekilde görünmelidir.

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample2.aspx)]

Bu öğreticide, kullanıcının seçili Tedarikçi ürünlerini Tedarikçi listesiyle aynı sayfada veya farklı bir sayfada görüntülemesine izin verin. Buna uyum sağlamak için, sayfaya iki düğme web denetimi ekleyin. Bu iki düğmenin `ID` s `ListProducts` ve `SendToProducts`olarak ayarlandım ve `ListProducts` tıklandığında bir geri gönderme gerçekleştiğinde ve seçilen tedarikçinin s ürünleri aynı sayfada listelendiğinde, ancak `SendToProducts` tıklandığında, Kullanıcı ürünleri listeleyen başka bir sayfaya göre yatay olarak gösterilir.

Şekil 9 ' da, bir tarayıcıdan görüntülenirken `Suppliers` GridView ve iki düğme web denetimi gösterilmektedir.

[ABD 'deki Bu tedarikçilerin ad, şehir ve ülke bilgilerinin listelendiğini ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.png)

**Şekil 9**: ABD 'Deki Bu tedarikçilerin ad, şehir ve ülke bilgileri listelenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.png))

## <a name="step-3-adding-a-column-of-radio-buttons"></a>3\. Adım: radyo düğmelerinin bir sütununu ekleme

Bu noktada, `Suppliers` GridView 'un ABD 'deki her bir tedarikçinin şirket adını, şehrini ve ülkesini görüntüleyen üç Boundalanı vardır. Ancak radyo düğmelerinin bir sütununda hala yok. Ne yazık ki GridView, yerleşik bir RadioButtonField içermez; Aksi halde, yalnızca kılavuza eklemek ve bunu yapmak için yapmanız yeterli olacaktır. Bunun yerine, bir TemplateField ekleyebilir ve `ItemTemplate` radyo düğmesini işleyecek şekilde yapılandırarak her bir GridView satırı için radyo düğmesi elde edebilirsiniz.

Başlangıçta, bir TemplateField 'ın `ItemTemplate` bir RadioButton Web denetimi ekleyerek istenen kullanıcı arabiriminin uygulanbileceğini varsayabilirsiniz. Bu, GridView 'un her satırına tek bir radyo düğmesi ekler, ancak radyo düğmeleri gruplanamaz ve bu nedenle birbirini dışlamayan değildir. Diğer bir deyişle, bir son kullanıcı GridView 'dan aynı anda birden çok radyo düğmesini seçebiliyor.

Bir TemplateField for RadioButton Web denetimlerinin kullanılması, ihtiyaç duyduğumuz işlevleri sunmasa da, sonuçta elde edilen radyo düğmelerinin neden gruplanmadığını incelerken bu yaklaşımı uygulayalım. Üretici GridView 'a bir TemplateField ekleyerek başlayın ve en soldaki alan haline gelir. Ardından, GridView s akıllı etiketinden Şablonları Düzenle bağlantısına tıklayın ve araç kutusundan bir RadioButton Web denetimini TemplateField s `ItemTemplate` sürükleyin (bkz. Şekil 10). RadioButton s `ID` özelliğini `RowSelector` ve `GroupName` özelliğini `SuppliersGroup`olarak ayarlayın.

[ItemTemplate 'e RadioButton Web denetimi ekleme ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.png)

**Şekil 10**: `ItemTemplate` bir RadioButton Web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.png))

Bu eklemeleri tasarımcı aracılığıyla yaptıktan sonra, GridView s işaretlerinizin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample3.aspx)]

RadioButton s [`GroupName` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx) , bir dizi radyo düğmesini gruplandırmak için kullanılır. Aynı `GroupName` değerine sahip tüm RadioButton denetimleri gruplandırılmış olarak kabul edilir; tek seferde bir gruptan yalnızca bir radyo düğmesi seçilebilir. `GroupName` özelliği, işlenmiş radyo düğmesi s `name` özniteliği için değeri belirtir. Tarayıcı radyo düğmeleri `name` özniteliklerini inceleyerek radyo düğmesi gruplamalarını tespit edin.

RadioButton Web denetimiyle `ItemTemplate`eklendiğinde, bu sayfayı bir tarayıcı aracılığıyla ziyaret edin ve kılavuz satırları ' nda radyo düğmelerine tıklayın. Radyo düğmelerinin nasıl gruplandırılmadığını, Şekil 11 ' in gösterdiği gibi tüm satırları seçmenizi olanaklı hale getirmeyi unutmayın.

[![GridView s radyo düğmeleri gruplandırılmıyor](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.png)

**Şekil 11**: GridView s radyo düğmeleri gruplandırılmaz ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.png))

Radyo düğmelerinin gruplandırılmadığı nedeni, aynı `GroupName` özellik ayarına sahip olmasına rağmen işlenen `name` özniteliklerinin farklı olmasından kaynaklanır. Bu farkları görmek için tarayıcıdan bir görünüm/kaynak yapın ve radyo düğmesi işaretlemesini inceleyin:

[!code-html[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample4.html)]

`name` ve `id` özniteliklerinin her ikisi de Özellikler penceresi belirtilen şekilde tam değerler değildir, ancak başka bir sayıda `ID` değeri ile sona erer. Oluşturulan `id` ve `name` özniteliklerinin önüne eklenen ek `ID` değerleri, radyo düğmelerinin `ID` s `GridViewRow`, GridView s `ID`, Içerik denetim s `ID`ve Web formu s `ID`' ı denetler. Bu `ID` s, GridView 'daki her işlenmiş Web denetiminin benzersiz bir `id` ve `name` değerlerine sahip olmasını sağlayacak şekilde eklenir.

Her işlenen denetim farklı bir `name` ve `id` gerekir çünkü bu, tarayıcının istemci tarafında her denetimi benzersiz bir şekilde tanımlaması ve geri gönderme sırasında ne tür ya da değişikliğin gerçekleştiği Web sunucusuna nasıl tanımladığı. Örneğin, her bir RadioButton on Checked durumu değiştirildiğinde bazı sunucu tarafı kodları çalıştırmak istediğimiz düşünün. Bunu, RadioButton s `AutoPostBack` özelliğini `true` olarak ayarlayıp `CheckChanged` olayı için bir olay işleyicisi oluşturarak gerçekleştirebiliriz. Ancak, tüm radyo düğmelerinin işlenen `name` ve `id` değerleri aynı olsaydı, geri göndermede hangi RadioButton 'ın tıklandığını belirleyemedik.

Bunun kısaltması, RadioButton Web denetimini kullanarak bir GridView 'da radyo düğmelerinin bir sütununu oluşturmıyoruz. Bunun yerine, her bir GridView satırına uygun biçimlendirmenin eklendiğinden emin olmak için, bunun yerine tasarlanmayan eski tekniklerini kullanacağız.

> [!NOTE]
> RadioButton Web denetimi gibi, bir şablona eklenen radyo düğmesi HTML denetimi benzersiz `name` özniteliğini içerir, böylece kılavuzda radyo düğmelerinin grubu çözülemez. HTML denetimleri hakkında bilginiz yoksa, özellikle ASP.NET 2,0 ' de HTML denetimleri nadiren kullanıldığı için bu nota göz ardı edebilirsiniz. Ancak daha fazla bilgi edinmek istiyorsanız, bkz. [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx) s blog girişi [Web denetimleri ve HTML denetimleri](http://www.odetocode.com/Articles/348.aspx).

## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>Radyo düğmesi Işaretlemesi eklemek için değişmez bir denetim kullanma

GridView içindeki tüm radyo düğmelerini doğru bir şekilde gruplandırmak için radyo düğmeleri işaretlemesini `ItemTemplate`içine el ile eklemeniz gerekir. Her radyo düğmesi aynı `name` özniteliğine ihtiyaç duyuyor, ancak benzersiz bir `id` özniteliğine sahip olmalıdır (bir radyo düğmesine istemci tarafı betiği aracılığıyla erişmek istiyoruz). Bir Kullanıcı bir radyo düğmesini seçip sayfayı geri gönderdikten sonra, tarayıcı seçili radyo düğmesi s `value` özniteliğinin değerini geri gönderir. Bu nedenle, her radyo düğmesi için benzersiz bir `value` özniteliği gerekir. Son olarak, geri göndermede `checked` özniteliğini seçili bir radyo düğmesine eklediğinizden emin olmamız gerekir, aksi takdirde Kullanıcı bir seçim ve geri gönderdikten sonra radyo düğmeleri varsayılan durumlarına (tümü seçilmemiş) döndürülür.

Bir şablona alt düzey biçimlendirme eklemek için alınabilecek iki yaklaşım vardır. Bunlardan biri, arka plan kod sınıfında tanımlanan biçimlendirme yöntemlerine yapılan biçimlendirme ve çağrılar karışımı olarak yapılır. Bu teknik ilk olarak [GridView denetim öğreticisindeki TemplateFields kullanılarak](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) anlatılmıştır. Bizim örneğimizde şöyle görünebilir:

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample5.aspx)]

Burada `GetUniqueRadioButton` ve `GetRadioButtonValue`, her radyo düğmesi için uygun `id` ve `value` öznitelik değerlerini döndüren arka plan kod sınıfında tanımlanmış yöntemler olacaktır. Bu yaklaşım, `id` ve `value` özniteliklerinin atanması için iyi bir sonuç verir, `checked` ancak veri bağlama söz dizimi yalnızca veriler GridView 'a ilk bağlandığında yürütülür. Bu nedenle, GridView 'un görünüm durumu etkinse, biçimlendirme yöntemleri yalnızca sayfa ilk yüklendiğinde (veya GridView veri kaynağına açıkça yeniden bağlandığında) harekete geçilir ve bu nedenle `checked` özniteliğini ayarlayan işlev geri gönderme sırasında çağrılmaz. Bu, daha hafif bir sorun ve bu makalenin kapsamına çok daha fazla Bununla birlikte, yukarıdaki yaklaşımı kullanmayı ve bunu üzerinde takılcağınız noktaya kadar çalıştırmayı öneririz. Bu tür bir alıştırma, çalışma sürümüne daha yakın bir işlem yapmanıza rağmen GridView ve veri bağlama yaşam döngüsünün daha derin bir şekilde anlaşılmasına yardımcı olur.

Bir şablonda ekleme özel, düşük düzey biçimlendirme ve bu öğreticide kullanacağınız yaklaşım için diğer yaklaşım, şablona bir [değişmez değer denetimi](https://msdn.microsoft.com/library/sz4949ks(VS.80).aspx) eklemektir. Ardından, GridView s `RowCreated` veya `RowDataBound` olay işleyicisinde, sabit değer denetimine programlı olarak erişilebilir ve `Text` özelliği, yayma için biçimlendirme olarak ayarlanabilir.

' I TemplateField s `ItemTemplate`kaldırarak bir değişmez değer denetimiyle değiştirerek başlayın. Değişmez denetim s `ID` `RadioButtonMarkup`olarak ayarlayın.

[ItemTemplate 'e sabit bir denetim eklemek ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.png)

**Şekil 12**: `ItemTemplate` değişmez değer denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.png))

Sonra, GridView s `RowCreated` olayı için bir olay işleyicisi oluşturun. `RowCreated` olay, eklenen her satır için bir kez harekete geçirilir, verilerin GridView 'a yeniden bağlanıp bağlanmadığını belirtir. Diğer bir deyişle, veriler görünüm durumundan yeniden yüklendiğinde `RowCreated` olayı ateşlenir ve bu, `RowDataBound` yerine bu işlemi kullandığımızda olur (yalnızca veri Web denetimine açıkça bağlandığında harekete geçirilir).

Bu olay işleyicisinde yalnızca bir veri satırıyla ilgilendiğimiz takdirde devam etmek istiyoruz. Her veri satırı için, `RadioButtonMarkup` sabit denetimine programlı bir şekilde başvurmak ve `Text` özelliğini yayma için biçimlendirme olarak ayarlamak istiyoruz. Aşağıdaki kodda gösterildiği gibi, bulunan biçimlendirme `name` `id` `SuppliersGroup`özniteliği `RowSelectorX`olarak ayarlanmış bir radyo düğmesi oluşturur; burada *X* , GridView satırının dizinidir ve `value` özniteliği GridView satırının dizinine ayarlanır. bu

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample6.cs)]

Bir GridView satırı seçildiğinde ve geri gönderme gerçekleştiğinde, seçili tedarikçinin `SupplierID` ilgileniyoruz. Bu nedenle, birisi her radyo düğmesinin değerinin gerçek `SupplierID` (GridView satırının dizini yerine) olması gerektiğini düşünebilir. Bu, belirli koşullarda çalışacağından, bir `SupplierID`benimseme ve işlemeyi bir güvenlik riski oluşturur. Örneğin, GridView 'umuz yalnızca ABD 'deki tedarikçileri listeler. Ancak, `SupplierID` doğrudan radyo düğmesinden geçirildiyse, yanlış bir kullanıcının geri gönderme sırasında geri gönderilen `SupplierID` değerini değiştirme işlemi durdurulacak. `value`olarak satır dizinini kullanarak ve sonra `DataKeys` koleksiyonundan geri göndermede `SupplierID` alırken, kullanıcının yalnızca GridView satırlarından biriyle ilişkili `SupplierID` değerlerinden birini kullandığından emin olabilirsiniz.

Bu olay işleyicisi kodu eklendikten sonra, sayfayı bir tarayıcıda sınamak için bir dakikanızı alın. İlk olarak, kılavuzda yalnızca bir radyo düğmesinin seçilebileceğini unutmayın. Ancak, bir radyo düğmesini seçip düğmelerden birine tıkladığınızda, geri gönderme gerçekleşir ve radyo düğmelerinin hepsi başlangıçtaki durumlarına geri döndürülür (yani, geri gönderme sırasında seçili radyo düğmesi artık seçili değildir). Bunu yapmak için, `RowCreated` olay işleyicisini, geri gönderiden gönderilen seçili radyo düğmesi dizinini inceleyerek ve `checked="checked"` özniteliğini satır Dizin eşleştirmelerinin verilmiş biçimlendirmesine ekleyerek geliştirmemiz gerekir.

Geri gönderme gerçekleştiğinde, tarayıcı `name` geri gönderir ve seçilen radyo düğmesinin `value`. Değer, `Request.Form["name"]`kullanılarak programlı bir şekilde alınabilir. [`Request.Form` özelliği](https://msdn.microsoft.com/library/system.web.httprequest.form.aspx) , form değişkenlerini temsil eden bir [`NameValueCollection`](https://msdn.microsoft.com/library/system.collections.specialized.namevaluecollection.aspx) sağlar. Form değişkenleri, Web sayfasındaki form alanlarının adları ve değerleridir ve her geri gönderme başarılı olduğunda Web tarayıcısı tarafından geri gönderilir. GridView 'daki radyo düğmelerinin işlenmiş `name` özniteliği `SuppliersGroup`, Web sayfası geri gönderildiğinde tarayıcı Web sunucusuna geri `SuppliersGroup=valueOfSelectedRadioButton` gönderir (diğer form alanlarıyla birlikte). Bu bilgilere daha sonra, şu kullanılarak `Request.Form` özelliğinden erişilebilir: `Request.Form["SuppliersGroup"]`.

Seçilen radyo düğmesi dizinini yalnızca `RowCreated` olay işleyicisinde değil, ancak düğme Web denetimlerine yönelik `Click` olay işleyicilerde belirleyebilmemiz için, radyo düğmelerinden biri seçili değilse ve seçili dizin ' i `-1` döndüren arka plan kod sınıfına bir `SuppliersSelectedIndex` özelliği ekleyelim.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample7.cs)]

Bu özellik eklendikten sonra, `SuppliersSelectedIndex` `e.Row.RowIndex`eşitse, `RowCreated` olay işleyicisine `checked="checked"` işaretlemesini eklemeyi biliyoruz. Olay işleyicisini şu mantığı içerecek şekilde güncelleştirin:

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample8.cs)]

Bu değişiklik ile, geri gönderme sonrasında seçili radyo düğmesi seçili kalır. Hangi radyo düğmesinin seçili olduğunu belirtme imkanına göre, sayfa ilk kez ziyaret edildiğinde, ilk GridView satırı s radyo düğmesi seçildiğinde (varsayılan olarak, geçerli olan radyo düğmelerinden hiçbiri değil) seçili davranış). Varsayılan olarak ilk radyo düğmesini seçili olması için `if (SuppliersSelectedIndex == e.Row.RowIndex)` deyiminizi şu şekilde değiştirmeniz yeterlidir: `if (SuppliersSelectedIndex == e.Row.RowIndex || (!Page.IsPostBack && e.Row.RowIndex == 0))`.

Bu noktada, GridView 'a gruplanmış radyo düğmelerinin bir sütununu, tek bir GridView satırının seçilmesine ve geri göndermeler arasında hatırlanmasını sağlayan bir sütun ekledik. Sonraki adımlarımız, seçilen tedarikçi tarafından sunulan ürünleri görüntülemektir. Adım 4 ' te, kullanıcının seçili `SupplierID`göndermek için başka bir sayfaya nasıl yönlendirildiğinin görüyoruz. 5\. adımda, seçilen tedarikçinin ürünlerini aynı sayfada bir GridView 'da nasıl görüntülerimize değineceğiz.

> [!NOTE]
> Bir TemplateField kullanmak yerine (Bu uzun adım 3 ' ün odağı), uygun Kullanıcı arabirimini ve işlevselliğini işleyen özel bir `DataControlField` sınıfı oluşturabiliyoruz. [`DataControlField` sınıfı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.aspx) , BoundField, CheckBoxField, TemplateField ve diğer yerleşik GridView ve DetailsView alanlarının türetebileceği temel sınıftır. Özel bir `DataControlField` sınıfı oluşturmak, radyo düğmelerinin sütununun yalnızca bildirime dayalı söz dizimi kullanılarak eklenebileceği anlamına gelir ve ayrıca diğer Web sayfalarındaki ve diğer Web uygulamalarında işlevselliğin çoğaltılmasını önemli ölçüde daha kolay hale getirir.

ASP.NET ' de özel, derlenmiş denetimler oluşturduysanız, bunu yapmanın, dikkatli bir iş miktarı gerektirdiğini ve bunu dikkatle ele almanız gereken alt tleler ve uç durumlarının bir konağından bulunduğunu bilirsiniz. Bu nedenle, radyo düğmelerinin bir sütununu şimdilik özel bir `DataControlField` sınıfı olarak uygulamamız ve TemplateField seçeneğiyle kontrol edeceğiz. Belki de gelecekteki bir öğreticide özel `DataControlField` sınıfları oluşturma, kullanma ve dağıtma şansınız vardır!

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>4\. Adım: seçili tedarikçinin ürünlerini ayrı bir sayfada görüntüleme

Kullanıcı bir GridView satırı seçtikten sonra seçili tedarikçinin ürünlerini göstermemiz gerekiyor. Bazı durumlarda, bu ürünleri ayrı bir sayfada göstermek isteyebilir, diğerleri de aynı sayfada bunu yapmayı tercih edebiliriz. İlk olarak ürünlerin ayrı bir sayfada nasıl görüntüleneceğini inceleyin; 5. adımda seçili tedarikçinin ürünlerini göstermek için `RadioButtonField.aspx` GridView ekleme bölümüne bakacağız.

Şu anda sayfada `ListProducts` ve `SendToProducts`iki düğme web denetimi vardır. `SendToProducts` düğmesine tıklandığında, kullanıcıyı `~/Filtering/ProductsForSupplierDetails.aspx`göndermek istiyoruz. Bu sayfa, [Iki sayfa üzerinde ana/ayrıntı filtrelemesinde](../masterdetail/master-detail-filtering-across-two-pages-cs.md) oluşturulmuştur ve `SupplierID`adlı QueryString alanı aracılığıyla `SupplierID` geçirildiği tedarikçinin ürünlerini görüntüler.

Bu işlevi sağlamak için `SendToProducts` Button s `Click` olayı için bir olay işleyicisi oluşturun. Adım 3 ' te, radyo düğmesi seçili olan satırın dizinini döndüren `SuppliersSelectedIndex` özelliğini ekledik. Karşılık gelen `SupplierID`, GridView s `DataKeys` koleksiyonundan alınabilir ve Kullanıcı daha sonra `Response.Redirect("url")`kullanılarak `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` gönderilebilir.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample9.cs)]

Bu kod, GridView 'dan seçilmiş olan radyo düğmelerinden biri seçildiği sürece wonderfully ile işe yarar. Başlangıçta GridView 'un herhangi bir radyo düğmesi yoksa ve Kullanıcı `SendToProducts` düğmesine tıkladığında, `-1` `DataKeys` koleksiyonunun dizin aralığının dışında olduğundan bir özel durum oluşturulmasına neden olacak `SuppliersSelectedIndex` `-1`olur. Bu, bununla ilgili bir sorun değildir, ancak adım 3 ' te anlatıldığı gibi `RowCreated` olay işleyicisini güncelleştirmeye karar verdiyseniz, ilk olarak GridView 'un seçtiği ilk radyo düğmesine sahip olacak.

`SuppliersSelectedIndex` bir `-1`değerine uyum sağlamak için GridView 'un üzerindeki sayfaya bir etiket Web denetimi ekleyin. `ID` özelliğini `ChooseSupplierMsg`, `CssClass` özelliğini `Warning`, `EnableViewState` ve `Visible` özelliklerini `false`ve `Text` özelliğini olarak ayarlayın. CSS sınıfı `Warning` metni kırmızı, italik, kalın, büyük yazı tipiyle görüntüler ve `Styles.css`tanımlanmıştır. `EnableViewState` ve `Visible` özelliklerini `false`olarak ayarlayarak, etiket yalnızca denetim s `Visible` özelliğinin program aracılığıyla `true`olarak ayarlandığı geri göndermeler dışında işlenmez.

[GridView üzerinde bir etiket Web denetimi eklemek ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image21.png)

**Şekil 13**: GridView 'un üzerine bir etiket Web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image22.png))

Daha sonra, `SuppliersSelectedIndex` sıfırdan küçükse `ChooseSupplierMsg` etiketini göstermek için `Click` olay işleyicisini daha sonra `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` başka bir şekilde yeniden yönlendirin.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample10.cs)]

Bir tarayıcıdaki sayfayı ziyaret edin ve GridView 'dan bir tedarikçi seçmeden önce `SendToProducts` düğmesine tıklayın. Şekil 14 ' te gösterildiği gibi bu, `ChooseSupplierMsg` etiketini gösterir. Sonra bir sağlayıcı seçin ve `SendToProducts` düğmesine tıklayın. Bu işlem, seçili tedarikçinin sağladığı ürünleri listeleyen bir sayfaya yanıt vermez. Şekil 15 ' te, Bigfoot Brewerıes tedarikçisi seçildiğinde `ProductsForSupplierDetails.aspx` sayfası gösterilir.

[ChooseSupplierMsg etiketi, hiçbir tedarikçi seçilmemişse görüntülenir ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image23.png)

**Şekil 14**: seçili bir sağlayıcı yoksa `ChooseSupplierMsg` etiketi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-a-gridview-column-of-radio-buttons-cs/_static/image24.png))

[![seçilen tedarikçinin ürünleri ProductsForSupplierDetails. aspx içinde görüntülenir](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image25.png)

**Şekil 15**: seçili tedarikçinin ürünleri `ProductsForSupplierDetails.aspx` görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image26.png))

## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>5\. Adım: seçili tedarikçinin ürünlerini aynı sayfada görüntüleme

4\. adımda, seçilen tedarikçinin ürünlerini göstermek için kullanıcının başka bir Web sayfasına nasıl gönderileceğini gördük. Alternatif olarak, seçilen tedarikçinin ürünleri aynı sayfada görüntülenebilir. Bunu göstermek için, seçili tedarikçinin ürünlerini göstermek üzere `RadioButtonField.aspx` başka bir GridView ekleyeceğiz.

Bu ürünlerin yalnızca bir tedarikçi seçildikten sonra görüntülenmesini istiyoruz, `Suppliers` GridView 'un altına bir panel Web denetimi ekleyin, `ID` `ProductsBySupplierPanel` ve `Visible` özelliği `false`olarak ayarlanıyor. Panelin içinde, seçili Tedarikçiye ait metin ürünlerini ve ardından `ProductsBySupplier`adlı GridView 'u ekleyin. GridView s akıllı etiketinden `ProductsBySupplierDataSource`adlı yeni bir ObjectDataSource 'a bağlamayı seçin.

[![Productsbytedarikçinin GridView öğesini yeni bir ObjectDataSource 'a bağlama](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image27.png)

**Şekil 16**: `ProductsBySupplier` GridView 'ı yeni bir ObjectDataSource 'a bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image28.png))

Sonra, `ProductsBLL` sınıfını kullanmak için ObjectDataSource 'u yapılandırın. Yalnızca seçili tedarikçi tarafından sunulan ürünleri almak istediğimiz için, ObjectDataSource 'un verileri almak üzere `GetProductsBySupplierID(supplierID)` metodunu çağırmasını belirtin. GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinden açılan listelerden (hiçbiri) seçeneğini belirleyin.

[ObjectDataSource 'ı Getproductsbysupplierıd (SupplierID) yöntemini kullanacak şekilde yapılandırmak ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image29.png)

**Şekil 17**: `GetProductsBySupplierID(supplierID)` yöntemini kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image30.png))

[GÜNCELLEŞTIRME, ekleme ve SILME sekmelerinde açılan listeleri (yok) olarak ayarlamak ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image31.png)

**Şekil 18**: GÜNCELLEŞTIRME, ekleme ve silme sekmelerinde aşağı açılan listeleri (yok) olarak ayarlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image32.png))

Seçme, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerini yapılandırdıktan sonra Ileri ' ye tıklayın. `GetProductsBySupplierID(supplierID)` yöntemi bir giriş parametresi beklediği için, veri kaynağı oluşturma Sihirbazı bize parametre değeri kaynağını belirtmemizi ister.

Burada parametre değeri kaynağını belirtirken burada birkaç seçenek sunuyoruz. Varsayılan Parameter nesnesini kullanabiliriz ve `SuppliersSelectedIndex` özelliğinin değerini, ObjectDataSource s `Selecting` olay işleyicisindeki parametre s `DefaultValue` özelliğine atayabilirsiniz. Program aracılığıyla bir Yenileyici için [ObjectDataSource 'un parametre değerleri](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md) öğreticisini programlı bir şekilde ayarlamaya yönelik olarak, ObjectDataSource 'un parametrelerine bir değer atayarak

Alternatif olarak, bir ControlParameter kullanabilir ve `Suppliers` GridView s [`SelectedValue` özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx) başvurabilirsiniz (bkz. Şekil 19). GridView s `SelectedValue` özelliği, [`SelectedIndex` özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex.aspx)karşılık gelen `DataKey` değerini döndürür. Bu seçeneğin çalışması için, `ListProducts` düğmesine tıklandığında GridView s `SelectedIndex` özelliğini seçilen satıra program aracılığıyla ayarlamanız gerekir. Ek bir avantaj olarak, `SelectedIndex`ayarlayarak, seçilen kayıt `DataWebControls` teması içinde tanımlanan `SelectedRowStyle` alır (sarı bir arka plan).

[![bir ControlParameter kullanarak, parametre kaynağı olarak bir GridView öğeleri](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image33.png)

**Şekil 19**: bir ControlParameter 'U parametre kaynağı olarak ([tam boyutlu görüntüyü görüntülemek Için tıklayın](adding-a-gridview-column-of-radio-buttons-cs/_static/image34.png)) belirtmek için kullanın

Sihirbazı tamamladıktan sonra, Visual Studio ürün verileri alanları için otomatik olarak alanlar ekler. `ProductName`, `CategoryName`ve `UnitPrice` BoundFields hariç tümünü kaldırın ve `HeaderText` özelliklerini ürün, kategori ve fiyat olarak değiştirin. `UnitPrice` BoundField değerini, değeri bir para birimi olarak biçimlendirilecek şekilde yapılandırın. Bu değişiklikleri yaptıktan sonra, panel, GridView ve ObjectDataSource tarafından bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample11.aspx)]

Bu alıştırmayı tamamlayabilmeniz için, `true` düğmesine tıklandığında GridView s `SelectedIndex` özelliğini `SelectedSuppliersIndex` ve `ProductsBySupplierPanel` panel s `Visible` özelliği `ListProducts` olarak ayarlamanız gerekir. Bunu gerçekleştirmek için, `ListProducts` Button Web Control s `Click` Event için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample12.cs)]

GridView 'dan bir tedarikçi seçilmemişse, `ChooseSupplierMsg` etiketi görüntülenir ve `ProductsBySupplierPanel` paneli gizlenir. Aksi takdirde, bir tedarikçi seçildiyse `ProductsBySupplierPanel` görüntülenir ve GridView s `SelectedIndex` özelliği güncellenir.

Şekil 20 ' de, Bigfoot Brela sağlayıcısı seçildikten sonra sonuçları gösterir ve sayfadaki ürünleri göster düğmesi tıklandı.

[Bigfoot Brewerler tarafından sağlanan ürünlerin aynı sayfada listelenmesi ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image35.png)

**Şekil 20**: Bigfoot brewerler tarafından sağlanan ürünler aynı sayfada listelenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-a-gridview-column-of-radio-buttons-cs/_static/image36.png))

## <a name="summary"></a>Özet

[Ayrıntılar DetailView öğreticisi Ile seçilebilir bir ana GridView kullanan ana/ayrıntı](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) bölümünde açıklandığı gibi, `ShowSelectButton` özelliği `true`olarak ayarlanmış bir CommandField kullanarak bir GridView 'dan kayıtlar seçilebilir. Ancak CommandField, kendi düğmelerini normal basma düğmeleri, bağlantılar veya görüntüler olarak görüntüler. Alternatif bir satır seçimi Kullanıcı arabirimi, her GridView satırında bir radyo düğmesi veya onay kutusu sağlamaktır. Bu öğreticide radyo düğmelerinin bir sütununu nasıl ekleyeceğiniz anlatılmıştır.

Ne yazık ki, radyo düğmelerinin bir sütununu basit veya basit olarak bir tane olarak eklemek beklenmeyebilir. Bir düğmeye tıkladığınızda eklenebilen yerleşik bir RadioButtonField yoktur ve bir TemplateField içindeki RadioButton Web denetimini kullanmak kendi sorun kümesini tanıtır. Bu tür bir arabirimi sağlamak için, `RowCreated` olay sırasında özel bir `DataControlField` sınıfı oluşturmanız veya uygun HTML 'yi bir TemplateField ekleme gerekir.

Radyo düğmelerinin bir sütununu nasıl ekleyecekseniz, onay kutusu sütunu ekleme konusunda ilgilenmeniz bize izin verin. Bir Kullanıcı onay işaretiyle bir veya daha fazla GridView satırı seçip tüm seçili satırlarda (bir Web tabanlı e-posta istemcisinden bir e-posta kümesi seçip seçili tüm e-postaları sil ' i seçerek) bazı işlemler gerçekleştirebilir. Bir sonraki öğreticide, böyle bir sütunun nasıl ekleneceğini öğreneceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren, David suru idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](adding-a-gridview-column-of-checkboxes-cs.md)
