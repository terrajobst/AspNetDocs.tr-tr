---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
title: Bildirim temelli parametrelerC#() | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, bir DetailsView denetiminde görüntülenecek verileri seçmek için bir parametre kümesinin sabit kodlanmış bir değere nasıl kullanılacağını göstereceğiz.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 603c9bd3-b895-4ec6-853b-0c81ff36d580
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
msc.type: authoredcontent
ms.openlocfilehash: 87c8cfe064abc536e6015b0e553618981da9fefe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74613306"
---
# <a name="declarative-parameters-c"></a>Bildirim Temelli Parametreler (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_5_CS.exe) veya [PDF 'yi indirin](declarative-parameters-cs/_static/datatutorial05cs1.pdf)

> Bu öğreticide, bir DetailsView denetiminde görüntülenecek verileri seçmek için bir parametre kümesinin sabit kodlanmış bir değere nasıl kullanılacağını göstereceğiz.

## <a name="introduction"></a>Giriş

[Son öğreticide](displaying-data-with-the-objectdatasource-cs.md) , `ProductsBLL` sınıfından `GetProducts()` yöntemini çağıran bir ObjectDataSource denetimine bağlanan GridView, DetailsView ve FormView denetimleriyle verileri görüntüleme konusunda baktık. `GetProducts()` yöntemi, Northwind veritabanının `Products` tablosundaki tüm kayıtlarla doldurulmuş kesin türü belirtilmiş bir DataTable döndürür. `ProductsBLL` sınıfı ürünlerin yalnızca alt kümelerini döndürmek için ek yöntemler içerir-`GetProductByProductID(productID)`, `GetProductsByCategoryID(categoryID)`ve `GetProductsBySupplierID(supplierID)`. Bu üç yöntem, döndürülen ürün bilgilerinin nasıl filtreleneceğini gösteren bir giriş parametresi bekler.

ObjectDataSource, giriş parametreleri bekleyen yöntemleri çağırmak için kullanılabilir, ancak bunu yapmak için bu parametrelerin değerlerinin nereden geldiği belirtilmelidir. Parametre değerleri sabit kodlanmış olabilir veya: QueryString değerleri, oturum değişkenleri, sayfadaki bir Web denetiminin özellik değeri veya diğerleri dahil olmak üzere çeşitli dinamik kaynaklardan gelebilir.

Bu öğreticide, bir parametre kümesinin sabit kodlanmış bir değere nasıl kullanılacağını gösteren bir başlangıç hallelim. Özellikle, belirli bir ürünle ilgili bilgileri görüntüleyen sayfaya bir DetailsView ekleme hakkında bilgi vereceğiz. Bu, Chef Anton 'nin Gumbo karışımı, yani 5 `ProductID`. Daha sonra, bir Web denetimine göre parametre değerinin nasıl ayarlanacağını öğreneceğiz. Özellikle, kullanıcının bir ülkede yer almasına izin vermek için bir metin kutusu kullanacağız. Bu, sonrasında söz konusu ülkede bulunan tedarikçilerin listesini görmek için bir düğmeye tıklayabilirler.

## <a name="using-a-hard-coded-parameter-value"></a>Sabit kodlanmış bir parametre değeri kullanma

İlk örnek için, `BasicReporting` klasöründeki `DeclarativeParams.aspx` sayfasına bir DetailsView denetimi ekleyerek başlayın. DetailsView 'un akıllı etiketinde, açılan listeden yeni veri kaynağı&gt; &lt;seçin ve bir ObjectDataSource eklemeyi seçin.

[Sayfaya bir ObjectDataSource eklemek ![](declarative-parameters-cs/_static/image2.png)](declarative-parameters-cs/_static/image1.png)

**Şekil 1**: sayfaya bir ObjectDataSource ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image3.png))

Bu, ObjectDataSource denetiminin veri kaynağı seçme Sihirbazı ' nı otomatik olarak başlatır. Sihirbazın ilk ekranından `ProductsBLL` sınıfını seçin.

[ProductsBLL sınıfını seçin ![](declarative-parameters-cs/_static/image5.png)](declarative-parameters-cs/_static/image4.png)

**Şekil 2**: `ProductsBLL` sınıfını seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image6.png))

`GetProductByProductID(productID)` yöntemini kullanmak istediğimiz belirli bir ürünle ilgili bilgileri göstermek istiyoruz.

[![GetProductByProductID (ProductID) yöntemini seçin](declarative-parameters-cs/_static/image8.png)](declarative-parameters-cs/_static/image7.png)

**Şekil 3**: `GetProductByProductID(productID)` yöntemini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image9.png))

Seçtiğimiz Yöntem bir parametre içerdiğinden, sihirbazda kullanılacak değeri tanımlamanız istentiğimiz için, sihirbaza yönelik bir ekran daha vardır. Sol taraftaki listede, seçilen yöntemin tüm parametreleri gösterilir. `GetProductByProductID(productID)` için yalnızca bir `productID`vardır. Sağ tarafta seçili parametre için değeri belirtebilir. Parametre kaynak açılan listesi, parametre değeri için çeşitli olası kaynakları numaralandırır. `productID` parametresi için sabit kodlanmış 5 değeri belirtmek istediğimiz için, parametre kaynağını yok olarak bırakın ve DefaultValue metin kutusuna 5 girin.

[ProductID parametresi için sabit kodlanmış bir parametre değeri olarak 5 ![kullanılır](declarative-parameters-cs/_static/image11.png)](declarative-parameters-cs/_static/image10.png)

**Şekil 4**: `productID` parametresi Için 5 sabit kodlanmış bir parametre değeri kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image12.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, ObjectDataSource denetiminin bildirim temelli biçimlendirmesi, `SelectMethod` özelliğinde tanımlanan yöntemin her biri için `SelectParameters` koleksiyonundaki bir `Parameter` nesnesi içerir. Bu örnekte kullandığımız yöntem yalnızca tek bir giriş parametresi beklediği için `parameterID`, burada yalnızca bir giriş vardır. `SelectParameters` koleksiyonu `System.Web.UI.WebControls` ad alanındaki `Parameter` sınıfından türetilen herhangi bir sınıfı içerebilir. Sabit kodlanmış parametre değerleri için temel `Parameter` sınıfı kullanılır, ancak diğer parametre kaynağı seçenekleri için türetilmiş bir `Parameter` sınıfı kullanılır; gerekirse kendi [özel parametre türlerinizi](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11)de oluşturabilirsiniz.

[!code-aspx[Main](declarative-parameters-cs/samples/sample1.aspx)]

> [!NOTE]
> Kendi bilgisayarınızda takip ediyorsanız, bu noktada gördüğünüz bildirime dayalı biçimlendirme `InsertMethod`, `UpdateMethod`ve `DeleteMethod` özelliklerinin yanı sıra `DeleteParameters`için değerler içerebilir. ObjectDataSource 'un veri kaynağı seçme Sihirbazı, ekleme, güncelleştirme ve silme için kullanılacak `ProductBLL` yöntemlerini otomatik olarak belirtir, bu nedenle açıkça silinmediğiniz takdirde yukarıdaki biçimlendirmeye dahil edilir.

Bu sayfayı ziyaret ederken, veri Web denetimi ObjectDataSource 'un `Select` yöntemini çağırır. Bu, `productID` giriş parametresi için sabit kodlanmış 5 değerini kullanarak `ProductsBLL` sınıfının `GetProductByProductID(productID)` yöntemini çağıracaktır. Yöntemi, Chef Anton 'nin Gumbo karışımı (`ProductID` 5 ile ürün) hakkında bilgi içeren, kesin olarak belirlenmiş `ProductDataTable` bir nesne döndürür.

[Chef Anton 'nin Gumbo karışımı hakkında ![bilgi görüntülenir](declarative-parameters-cs/_static/image14.png)](declarative-parameters-cs/_static/image13.png)

**Şekil 5**: Chef Anton 'Nin Gumbo karışımı hakkında bilgi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image15.png))

## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>Parametre değerini bir Web denetiminin özellik değerine ayarlama

ObjectDataSource 'un parametre değerleri, sayfadaki bir Web denetiminin değerine göre de ayarlanabilir. Bunu göstermek için, Kullanıcı tarafından belirtilen bir ülkede bulunan tüm tedarikçileri listeleyen bir GridView 'e sahip olalım. Bu başlatmayı başarmak için, kullanıcının bir ülke adı girebileceği sayfaya bir metin kutusu ekleyin. Bu TextBox denetiminin `ID` özelliğini `CountryName`olarak ayarlayın. Ayrıca bir düğme web denetimi de ekleyin.

[![ID adlı sayfaya bir TextBox ekleyin](declarative-parameters-cs/_static/image17.png)](declarative-parameters-cs/_static/image16.png)

**Şekil 6**: `ID` `CountryName` ile sayfaya bir TextBox ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image18.png))

Sonra, sayfaya bir GridView ekleyin ve akıllı etiketinden yeni bir ObjectDataSource eklemek için öğesini seçin. Üretici bilgilerini göstermek istediğimiz için sihirbazın ilk ekranından `SuppliersBLL` sınıfını seçin. İkinci ekrandan `GetSuppliersByCountry(country)` yöntemini seçin.

[![GetSuppliersByCountry (Country) yöntemini seçin](declarative-parameters-cs/_static/image20.png)](declarative-parameters-cs/_static/image19.png)

**Şekil 7**: `GetSuppliersByCountry(country)` yöntemini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image21.png))

`GetSuppliersByCountry(country)` yönteminde bir giriş parametresi bulunduğundan, sihirbaz bir kez daha yeniden parametre değeri seçmeye yönelik son bir ekran içerir. Bu kez, parametre kaynağını denetim olarak ayarlayın. Bu, ControlID açılan listesini sayfadaki denetimlerin adlarıyla dolduracaktır; listeden `CountryName` denetimini seçin. Sayfa ilk kez ziyaret edildiğinde `CountryName` metin kutusu boş olur, bu nedenle hiçbir sonuç döndürülmez ve hiçbir şey gösterilmez. Bazı sonuçları varsayılan olarak göstermek istiyorsanız, DefaultValue metin kutusunu uygun şekilde ayarlayın.

[![parametre değerini CountryName denetim değeri olarak ayarlayın](declarative-parameters-cs/_static/image23.png)](declarative-parameters-cs/_static/image22.png)

**Şekil 8**: parametre değerini `CountryName` denetim değerine ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image24.png))

ObjectDataSource 'un bildirim temelli biçimlendirmesi, standart `Parameter` nesnesi yerine [ControlParameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx) kullanılarak ilk örneğimizden biraz farklılık gösterir. `ControlParameter`, Web denetiminin `ID` belirtmek için ek özelliklere ve parametresi için kullanılacak özellik değerine sahiptir (`PropertyName`). Veri kaynağı Yapılandırma Sihirbazı, bir metin kutusu için büyük olasılıkla parametre değeri için `Text` özelliğini kullanmak isteyeceğiz. Ancak, Web denetiminden farklı bir özellik değeri kullanmak isterseniz, `PropertyName` değerini buradan değiştirebilir veya sihirbazdaki "Gelişmiş özellikleri göster" bağlantısına tıklayabilirsiniz.

[!code-aspx[Main](declarative-parameters-cs/samples/sample2.aspx)]

`CountryName` metin kutusu boş olduğunda sayfa ilk kez ziyaret edildiğinde. ObjectDataSource 'un `Select` yöntemi GridView tarafından hala çağrılır, ancak `null` değeri `GetSuppliersByCountry(country)` yöntemine geçirilir. TableAdapter `null` bir veritabanı `NULL` değerine (`DBNull.Value`) dönüştürür, ancak `GetSuppliersByCountry(country)` yöntemi tarafından kullanılan sorgu `NULL` parametresi için bir `@CategoryID` değeri belirtildiğinde herhangi bir değer döndürmüyor şekilde yazılır. Kısacası, hiçbir üretici döndürülmez.

Ziyaretçi bir ülkeye girdiğinde ve geri göndermeye neden olacak şekilde tedarikçileri göster düğmesine tıkladıktan sonra, ObjectDataSource 'un `Select` yöntemi yeniden çağrılır ve bu, TextBox denetiminin `Text` değerini `country` parametresi olarak geçirerek yeniden sorgular.

[Kanada 'daki bu tedarikçiler ![gösteriliyor](declarative-parameters-cs/_static/image26.png)](declarative-parameters-cs/_static/image25.png)

**Şekil 9**: Kanada 'Daki tedarikçiler gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](declarative-parameters-cs/_static/image27.png))

## <a name="showing-all-suppliers-by-default"></a>Tüm tedarikçileri varsayılan olarak gösterme

İlk olarak sayfayı görüntülerken tedarikçilerinin hiçbirini göstermek yerine, ilk olarak *Tüm* tedarikçileri göstermek istiyoruz. böylece, metin kutusuna bir ülke adı girerek kullanıcının listeyi yavaşlayabilmesini sağlar. TextBox boş olduğunda, `SuppliersBLL` sınıfın `GetSuppliersByCountry(country)` yöntemi *`country`* giriş parametresi için `null` bir değere geçirilir. Bu `null` değer daha sonra DAL `GetSupplierByCountry(country)` yöntemine geçirilir ve burada, aşağıdaki sorgudaki `@Country` parametresi için bir veritabanı `NULL` değerine çevrilir:

[!code-sql[Main](declarative-parameters-cs/samples/sample3.sql)]

`Country = NULL` ifadesi her zaman, `Country` sütunu `NULL` değere sahip olan kayıtlar için de false döndürür; Bu nedenle, hiçbir kayıt döndürülmez.

Ülke metin kutusu boş olduğunda *Tüm* tedarikçileri döndürmek IÇIN, BLL 'deki `GetSuppliersByCountry(country)` yöntemi, ülke parametresi `null` ve diğer bir DEYIŞLE, dal `GetSuppliersByCountry(country)` yöntemini çağırmak için `GetSuppliers()` metodunu artırabilir. Bu, ülke belirtilmediğinde tüm tedarikçileri döndürme ve ülke parametresi dahil, tedarikçinin uygun alt kümesini döndürür.

`SuppliersBLL` sınıfındaki `GetSuppliersByCountry(country)` yöntemini aşağıdaki şekilde değiştirin:

[!code-csharp[Main](declarative-parameters-cs/samples/sample4.cs)]

Bu değişiklik ile `DeclarativeParams.aspx` sayfası, ilk ziyaret edildiğinde (veya `CountryName` metin kutusu boş olduğunda) tüm tedarikçileri gösterir.

[![tüm tedarikçiler artık varsayılan olarak gösteriliyor](declarative-parameters-cs/_static/image29.png)](declarative-parameters-cs/_static/image28.png)

**Şekil 10**: tüm tedarikçiler artık varsayılan olarak gösteriliyor ([tam boyutlu görüntüyü görüntülemek için tıklatın](declarative-parameters-cs/_static/image30.png))

## <a name="summary"></a>Özet

Yöntemleri giriş parametreleriyle birlikte kullanmak için, ObjectDataSource 'un `SelectParameters` koleksiyonundaki parametrelerin değerlerini belirtmemiz gerekir. Farklı parametre türleri, parametre değerinin farklı kaynaklardan elde edilebilir olmasını sağlar. Varsayılan parametre türü, sabit kodlanmış bir değer kullanır, ancak kolayca (bir kod satırı olmadan) parametre değerleri, sayfada Web denetimlerinin QueryString, oturum değişkenleri, tanımlama bilgileri ve hatta Kullanıcı tarafından girilen değerlerden elde edilebilir.

Bu öğreticide, bildirim temelli parametre değerlerinin nasıl kullanılacağını gösteren örnekler. Ancak, geçerli tarih ve saat gibi mevcut olmayan bir parametre kaynağı kullanmanın veya sitemizin üyeliği kullanıyorsa, ziyaretçi Kullanıcı KIMLIĞI gibi durumlar olabilir. Bu tür senaryolarda, temel nesnenin metodunu çağıran ObjectDataSource 'tan önce parametre değerlerini program aracılığıyla ayarlayabiliriz. Bunu bir [sonraki öğreticide](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)nasıl gerçekleştireceğinizi öğreneceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](displaying-data-with-the-objectdatasource-cs.md)
> [İleri](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
