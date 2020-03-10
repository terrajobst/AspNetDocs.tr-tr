---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
title: SqlDataSource ile veri ekleme, güncelleştirme ve silme (VB) | Microsoft Docs
author: rick-anderson
description: Önceki öğreticilerde, ObjectDataSource denetiminin verileri ekleme, güncelleştirme ve silme için nasıl izin verileceğini öğrendik. SqlDataSource denetimi t 'yi destekliyor...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9673bef3-892c-45ba-a7d8-0da3d6f48ec5
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 4f7b282b09769272df8ff3a32aa4c509c8917481
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626562"
---
# <a name="inserting-updating-and-deleting-data-with-the-sqldatasource-vb"></a>SqlDataSource ile Veri Ekleme, Güncelleştirme ve Silme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_VB.exe) veya [PDF 'yi indirin](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/datatutorial49vb1.pdf)

> Önceki öğreticilerde, ObjectDataSource denetiminin verileri ekleme, güncelleştirme ve silme için nasıl izin verileceğini öğrendik. SqlDataSource denetimi aynı işlemleri destekler, ancak yaklaşım farklıdır ve bu öğretici, SqlDataSource 'un verileri eklemek, güncelleştirmek ve silmek için nasıl yapılandırılacağını gösterir.

## <a name="introduction"></a>Giriş

[Ekleme, güncelleştirme ve silme konusunda genel bir bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)Için, GridView denetimi yerleşik güncelleştirme ve silme özellikleri sağlarken, DetailsView ve FormView denetimleri, işlevselliği düzenlemenin ve silmenin yanı sıra destek ekleme olanağı içerir. Bu veri değiştirme özellikleri, bir kod satırı yazılması gerekmeden doğrudan bir veri kaynağı denetimine takılabilir. GridView, DetailsView ve FormView denetimleriyle ekleme, güncelleştirme ve silme işlemlerini kolaylaştırmak için ObjectDataSource kullanılarak incelenen [, güncelleştirmeye ve silmeye genel bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) . Alternatif olarak, SqlDataSource, ObjectDataSource yerine kullanılabilir.

INSERT, Update veya delete eylemini gerçekleştirmek için çağrılacak nesne katmanı yöntemlerini belirtmemiz gereken ObjectDataSource ile ekleme, güncelleştirme ve silme işlemini desteklemeyi sağlayan bu işlemi geri çekin. SqlDataSource ile yürütmek için `INSERT`, `UPDATE`ve `DELETE` SQL deyimleri (veya saklı yordamlar) sağlamamız gerekir. Bu öğreticide göreceğiniz gibi, bu deyimler el ile oluşturulabilir veya SqlDataSource s veri kaynağı Yapılandırma Sihirbazı tarafından otomatik olarak oluşturulabilir.

> [!NOTE]
> GridView, DetailsView ve FormView denetimlerinin ekleme, düzenlemesi ve silme yeteneklerini zaten tartıştığımız için, bu öğretici bu işlemleri desteklemek için SqlDataSource denetimini yapılandırmaya odaklanacaktır. Bu özellikleri GridView, DetailsView ve FormView içinde uygulamaya yönelik olarak, [ekleme, güncelleştirme ve silme konusunda genel bir bakış](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)Ile başlayan veri öğreticilerini düzenlemenin, eklemenin ve silmenin üzerine dönebilmeniz gerekir.

## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>1\. Adım:`INSERT`,`UPDATE`ve`DELETE`deyimlerini belirtme

Son iki öğreticilerde gördüğünüz gibi, bir SqlDataSource denetiminden veri almak için iki özellik ayarlamanız gerekir:

1. `ConnectionString`, sorgunun hangi veritabanına gönderileceğini belirtir ve
2. `SelectCommand`, sonuçları döndürmek için yürütülecek olan geçici SQL ifadesini veya saklı yordam adını belirten.

Parametreleri olan `SelectCommand` değerler için, parametre değerleri SqlDataSource s `SelectParameters` koleksiyonu aracılığıyla belirtilir ve sabit kodlanmış değerler, ortak parametre kaynak değerleri (QueryString alanları, oturum değişkenleri, Web denetim değerleri vb.) içerebilir veya program aracılığıyla atanabilir. SqlDataSource Control s `Select()` yöntemi programlı olarak veya bir veri Web denetiminden otomatik olarak çağrıldığında, veritabanına bir bağlantı oluşturulur, parametre değerleri sorguya atanır ve komut veritabanına shuttled kapalıdır. Sonuçlar, denetim s `DataSourceMode` özelliğinin değerine bağlı olarak veri kümesi veya DataReader olarak döndürülür.

Veri seçme ile birlikte, SqlDataSource denetimi `INSERT`, `UPDATE`ve `DELETE` SQL deyimlerini çok aynı şekilde sağlayarak veri eklemek, güncelleştirmek ve silmek için kullanılabilir. Yürütülecek `INSERT`, `UPDATE`ve `DELETE` SQL deyimlerinin `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özelliklerini atamanız yeterlidir. Deyimlerde parametreler varsa (Bunlar her zaman için), bunları `InsertParameters`, `UpdateParameters`ve `DeleteParameters` koleksiyonlara dahil edin.

Bir `InsertCommand`, `UpdateCommand`veya `DeleteCommand` değeri belirtilmişse, ilgili veri Web denetimi s akıllı etiketinde ekleme, yeniden Düzenle veya silmeyi etkinleştir seçeneğinin kullanılabilmesi için kullanılabilir hale gelir. Bunu göstermek için, [SqlDataSource denetim öğreticisi Ile sorgulama verilerinde](querying-data-with-the-sqldatasource-control-vb.md) oluşturduğumuz `Querying.aspx` sayfasından bir örnek alalım ve bunu silme yeteneklerini içerecek şekilde geliştirdik.

`InsertUpdateDelete.aspx` ve `Querying.aspx` sayfalarını `SqlDataSource` klasöründen açarak başlayın. Tasarımcı `Querying.aspx` sayfasında, ilk örnekteki SqlDataSource ve GridView ' i (`ProductsDataSource` ve `GridView1` denetimleri) seçin. İki denetimi seçtikten sonra, Düzen menüsüne gidin ve Kopyala ' yı seçin (veya yalnızca CTRL + C ' ye basın). Sonra, `InsertUpdateDelete.aspx` tasarımcısına gidin ve denetimlere yapıştırın. İki denetimi `InsertUpdateDelete.aspx`üzerine taşıdıktan sonra, sayfayı bir tarayıcıda test edin. `Products` veritabanı tablosundaki tüm kayıtlar için `ProductID`, `ProductName`ve `UnitPrice` sütunlarının değerlerini görmeniz gerekir.

[Tüm ürünlerin ![, ProductID tarafından sıralanan şekilde listelenmiştir](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.png)

**Şekil 1**: tüm ürünler `ProductID` göre sıralanmıştır ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.png))

## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>SqlDataSource s`DeleteCommand`ve`DeleteParameters`özellikleri ekleniyor

Bu noktada, tek yapmanız gereken `Products` tablosundan tüm kayıtları döndüren bir SqlDataSource ve bu verileri işleyen bir GridView sunuyoruz. Amacınız, kullanıcının GridView aracılığıyla ürünleri silmesine izin vermek için bu örneği genişletmektir. Bunu gerçekleştirmek için, SqlDataSource Control s `DeleteCommand` ve `DeleteParameters` özelliklerinin değerlerini belirtmemiz ve sonra GridView 'ı silmeyi destekleyecek şekilde yapılandırmanız gerekir.

`DeleteCommand` ve `DeleteParameters` özellikleri çeşitli yollarla belirtilebilir:

- Bildirim temelli söz dizimi
- Tasarımcıda Özellikler penceresi
- Veri kaynağını yapılandırma Sihirbazı ' nda özel bir SQL ifadesini veya saklı yordam belirleme ekranını seçin
- Veri kaynağını yapılandırma Sihirbazı ' nda bulunan görünüm tablosundan sütunları belirt ' in Gelişmiş düğmesi aracılığıyla, `DeleteCommand` ve `DeleteParameters` özelliklerde kullanılan `DELETE` SQL deyiminden ve parametre koleksiyonuna otomatik olarak otomatik olarak oluşturacak

Adım 2 ' de `DELETE` deyimin otomatik olarak nasıl oluşturulduğunu inceleyeceğiz. Şimdilik, veri kaynağı Yapılandırma Sihirbazı ya da bildirime dayalı sözdizimi seçeneği de yalnızca aynı zamanda çalışabilse de tasarımcı 'daki Özellikler penceresi kullanalım.

`InsertUpdateDelete.aspx`tasarımcıda `ProductsDataSource` SqlDataSource ' a tıklayın ve ardından Özellikler penceresi ' ı (Görünüm menüsünden Özellikler penceresi ' i seçin veya yalnızca F4 ' e basın). Bir üç nokta kümesini getirecek olan DeleteQuery özelliğini seçin.

![Özellikler penceresinden DeleteQuery özelliğini seçin](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.gif)

**Şekil 2**: Özellikler penceresinden DeleteQuery özelliğini seçin

> [!NOTE]
> SqlDataSource bir DeleteQuery özelliğine sahip değildir. Bunun yerine, DeleteQuery `DeleteCommand` ve `DeleteParameters` özelliklerinin bir birleşimidir ve yalnızca pencere tasarımcı aracılığıyla görüntülenirken Özellikler penceresi listelenmiştir. Kaynak görünümündeki Özellikler penceresi bakıyorsanız, bunun yerine `DeleteCommand` özelliğini bulacaksınız.

DeleteQuery özelliğindeki üç nokta işaretine tıklayarak komut ve parametre Düzenleyicisi iletişim kutusunu açın (bkz. Şekil 3). Bu iletişim kutusunda `DELETE` SQL ifadesini belirtebilir ve parametreleri belirtebilirsiniz. `DELETE` komut metin kutusuna aşağıdaki sorguyu girin (isterseniz el ile veya Sorgu Tasarımcısı kullanarak):

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample1.sql)]

Ardından, aşağıdaki parametre listesine `@ProductID` parametresini eklemek için parametreleri Yenile düğmesine tıklayın.

[![Özellikler penceresinden DeleteQuery özelliğini seçin](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.png)

**Şekil 3**: Özellikler penceresinden DeleteQuery özelliğini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.png))

Bu parametre için bir *değer sağlamadığınızda* (parametre kaynağını yok olarak bırakın). GridView 'a silme desteğini eklediğimiz bir kez, GridView bu parametre değerini, Sil düğmesine tıklanmış olan satır için `DataKeys` koleksiyonunun değerini kullanarak otomatik olarak sağlayacaktır.

> [!NOTE]
> `DELETE` sorgusunda kullanılan parametre adı, GridView, DetailsView veya FormView içindeki `DataKeyNames` değerinin adı ile aynı *olmalıdır* . Diğer bir deyişle, `DELETE` deyimindeki parametresi, Products tablosundaki birincil anahtar sütun adı (ve bu nedenle GridView 'daki DataKeyNames değeri) `ProductID`olduğundan, `@ProductID` (yani, deyin, `@ID`) olarak adlandırılır.

Parametre adı ve `DataKeyNames` değeri eşleşmiyorsa GridView, değeri otomatik olarak `DataKeys` koleksiyonundan atayamaz.

Silme ile ilgili bilgileri komut ve parametre Düzenleyicisi iletişim kutusuna girdikten sonra, ortaya çıkan bildirim işaretlemesini incelemek için Tamam ' a tıklayın ve kaynak görünümüne gidin:

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample2.aspx)]

`DeleteCommand` özelliğinin yanı sıra `<DeleteParameters>` bölümünü ve `productID`adlı parametre nesnesini de bir yere göz önünde.

## <a name="configuring-the-gridview-for-deleting"></a>GridView 'ı silmek için yapılandırma

`DeleteCommand` özelliği eklendiğinde, GridView s akıllı etiketi şimdi silmeyi etkinleştir seçeneğini içerir. Devam edin ve bu onay kutusunu işaretleyin. [Ekleme, güncelleştirme ve silme konusunda bir genel bakışta](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)açıklandığı gibi, GridView 'un `ShowDeleteButton` özelliği `True`olarak ayarlanmış bir CommandField eklemesine neden olur. Şekil 4 ' te gösterildiği gibi, sayfa bir tarayıcı ile ziyaret edildiğinde silme düğmesi de bulunur. Bazı ürünleri silerek bu sayfayı test edin.

[Her GridView satırı ![şimdi bir Sil düğmesi Içerir](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.png)

**Şekil 4**: her GridView satırı artık Sil düğmesini içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.png))

Bir Delete düğmesine tıklandıktan sonra, GridView, `ProductID` parametresini, DELETE düğmesine tıklanan satıra ait `DataKeys` Collection değerinin değerine atar ve SqlDataSource s `Delete()` yöntemini çağırır. Ardından SqlDataSource denetimi veritabanına bağlanır ve `DELETE` ifadesini yürütür. GridView daha sonra SqlDataSource 'a yeniden bağlanır, geri dönüp geçerli ürün kümesini (artık tam silinen kaydı içermez) görüntüler.

> [!NOTE]
> GridView, SqlDataSource parametrelerini doldurmak için `DataKeys` koleksiyonunu kullandığından, GridView s `DataKeyNames` özelliğinin birincil anahtarı oluşturan ve SqlDataSource s `SelectCommand` bu sütunları döndürdüğünden emin olun. Üstelik, SqlDataSource s `DeleteCommand` parametre adının `@ProductID`olarak ayarlanması önemlidir. `DataKeyNames` özelliği ayarlanmamışsa veya parametre `@ProductsID`adlandırılmadıysa, Sil düğmesine tıklamak geri göndermeye neden olur, ancak hiçbir kaydı aslında silmez.

Şekil 5 ' te bu etkileşim grafiksel olarak gösterilmiştir. Veri Web denetiminden ekleme, güncelleştirme ve silme ile ilişkili olayların zinciri hakkında daha ayrıntılı bir tartışma için [ekleme, güncelleştirme ve silme öğreticisi Ile Ilişkili olayları İnceleme](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) bölümüne geri bakın.

![GridView 'daki Sil düğmesine tıkladığınızda SqlDataSource s Delete () yöntemi çağırılır](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.gif)

**Şekil 5**: GridView 'Da Sil düğmesine tıkladığınızda SqlDataSource s `Delete()` yöntemi çağırılır

## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>2\. Adım:`INSERT`,`UPDATE`ve`DELETE`deyimlerini otomatik olarak oluşturma

1\. adım incelendi `INSERT`, `UPDATE`ve `DELETE` SQL deyimleri Özellikler penceresi veya denetim tarafından bildirime dayalı sözdizimi aracılığıyla belirtilebilir. Ancak, bu yaklaşım tek başına SQL deyimlerini el ile yazmanızı gerektirir ve bu, monotous ve hata durumunda olabilir. Neyse ki, veri kaynağı Yapılandırma Sihirbazı, görünüm ekranından sütunları belirt ' i kullanırken `INSERT`, `UPDATE`ve `DELETE` deyimlerinin otomatik olarak oluşturulmasını sağlayan bir seçenek sunar.

Bu otomatik oluşturma seçeneğini keşfedelim. `InsertUpdateDelete.aspx` tasarımcı 'ya bir DetailsView ekleyin ve `ID` özelliğini `ManageProducts`olarak ayarlayın. Ardından, DetailsView 'un akıllı etiketinde yeni bir veri kaynağı oluşturmayı ve `ManageProductsDataSource`adlı bir SqlDataSource oluşturmayı seçin.

[![ManageProductsDataSource adlı yeni bir SqlDataSource oluşturma](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.png)

**Şekil 6**: `ManageProductsDataSource` adlı yeni bir SqlDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.png))

Veri kaynağı Yapılandırma Sihirbazı ' ndan `NORTHWINDConnectionString` bağlantı dizesini kullanmayı ve Ileri ' yi tıklatın. Select Ifadesini Yapılandır ekranında, bir tablodaki sütunları belirt veya görünümü görüntüle radyo düğmesini seçili bırakın ve açılan listeden `Products` tablosunu seçin. Onay kutusu listesinden `ProductID`, `ProductName`, `UnitPrice`ve `Discontinued` sütunları seçin.

[Ürünler tablosunu kullanarak ![ProductID, ProductName, UnitPrice ve Discontinued sütunlarını döndürün](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.png)

**Şekil 7**: `Products` tablosunu kullanarak `ProductID`, `ProductName`, `UnitPrice`ve `Discontinued` sütunları döndürün ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image10.png))

Seçilen tablo ve sütunlara göre otomatik olarak `INSERT`, `UPDATE`ve `DELETE` deyimlerini oluşturmak için Gelişmiş düğmesine tıklayın ve `INSERT`, `UPDATE`ve `DELETE` deyimlerini oluştur onay kutusunu işaretleyin.

![INSERT, UPDATE ve DELETE deyimlerini oluştur onay kutusunu işaretleyin](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.gif)

**Şekil 8**: oluşturma `INSERT`, `UPDATE`ve `DELETE` deyimlerini denetle onay kutusu

`INSERT`, `UPDATE`ve `DELETE` deyimlerini oluştur onay kutusu yalnızca seçili tabloda bir birincil anahtar varsa ve döndürülen sütunlar listesine birincil anahtar sütunu (veya sütunları) dahil edildiğinde kullanıma sunulacaktır. `INSERT`oluştur, `UPDATE`ve `DELETE` deyimler onay kutusu işaretlendikten sonra seçilebilir hale gelen iyimser eşzamanlılık kullan onay kutusunu, iyimser eşzamanlılık denetimi sağlamak için ortaya çıkan `UPDATE` ve `DELETE` deyimlerdeki `WHERE` yan tümceleri daha iyi hale gelir. Şimdilik bu onay kutusunu işaretlenmemiş olarak bırakın; sonraki öğreticide SqlDataSource denetimiyle iyimser eşzamanlılığı inceleyeceğiz.

`INSERT`, `UPDATE`ve `DELETE` deyimlerini oluştur onay kutusunu işaretledikten sonra Tamam ' a tıklayarak, SELECT deyimini Yapılandır ekranına dönün, ardından Ileri ' ye tıklayın ve ardından son ' a tıklayarak veri kaynağı Yapılandırma Sihirbazı ' nı doldurun. Sihirbaz tamamlandıktan sonra Visual Studio, `ProductID`, `ProductName`ve `UnitPrice` sütunları ve `Discontinued` sütunu için bir CheckBoxField için DetailsView 'a BoundFields ekler. DetailsView 'un akıllı etiketinde, bu sayfayı ziyaret eden kullanıcının ürünlerin içinden ilerleyebilmesi için sayfalama etkinleştir seçeneğini işaretleyin. Ayrıca DetailsView s `Width` ve `Height` özelliklerini de temizleyin.

Akıllı etiketin eklemeyi etkinleştir, Düzenle etkinleştir ve mevcut silme seçeneklerini etkinleştir seçeneklerini görürsünüz. Bunun nedeni, SqlDataSource `InsertCommand`, `UpdateCommand`ve `DeleteCommand`için değerler içereceğinden aşağıdaki bildirime dayalı sözdizimidir:

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample3.aspx)]

SqlDataSource denetiminin `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özellikleri için değerleri otomatik olarak nasıl ayarlandığını aklınızda edin. `InsertCommand` ve `UpdateCommand` özelliklerinde başvurulan sütun kümesi `SELECT` deyimindekilerle dayanır. Diğer bir deyişle, `InsertCommand` ve `UpdateCommand`*her* ürün sütununa sahip olmak yerine, yalnızca `SelectCommand` belirtilen sütunlar vardır (daha az `ProductID`ve [`IDENTITY`](http://www.sqlteam.com/item.asp?ItemID=102)bu, düzenleme sırasında değeri değiştirilemez ve eklendiğinde otomatik olarak atanır). Ayrıca, `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özelliklerindeki her bir parametre için `InsertParameters`, `UpdateParameters`ve `DeleteParameters` koleksiyonlarında karşılık gelen parametreler vardır.

DetailsView 'un veri değiştirme özelliklerini açmak için, akıllı etiketinde ekleme, Düzenle ve silmeyi etkinleştir seçeneklerini işaretleyin. Bu, `ShowInsertButton`, `ShowEditButton`ve `ShowDeleteButton` özellikleri `True`olarak ayarlanmış bir CommandField ekler.

Tarayıcıdaki sayfayı ziyaret edin ve DetailsView 'a eklenen düzenleme, silme ve yeni düğmeleri aklınızda bulunur. Düzenle düğmesine tıkladığınızda, DetailsView, `ReadOnly` özelliği bir TextBox olarak `False` (varsayılan) ve CheckBoxField olarak bir CheckBox olarak ayarlanmış olan her bir BoundField görüntüleyen düzenleme moduna geçer.

[DetailsView 'un varsayılan Düzenle arabirimini ![](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image11.png)

**Şekil 9**: DetailsView 'un varsayılan düzenlenme arabirimi ([tam boyutlu görüntüyü görüntülemek için tıklayın](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image12.png))

Benzer şekilde, seçili olan ürünü silebilir veya sisteme yeni bir ürün ekleyebilirsiniz. `InsertCommand` deyimleri yalnızca `ProductName`, `UnitPrice`ve `Discontinued` sütunları ile çalıştığından, diğer sütunlarda, ekleme sırasında veritabanı tarafından atanan `NULL` veya varsayılan değerleri vardır. ObjectDataSource ile tıpkı, `InsertCommand` `NULL` s öğesine izin vermeyi desteklemeyen ve varsayılan bir değere sahip olmayan herhangi bir veritabanı tablo sütunu eksikse, `INSERT` bildirisini yürütmeye çalışırken bir SQL hatası oluşur.

> [!NOTE]
> DetailsView 'un ekleme ve düzenlemeyle ilgili hiçbir özelleştirme veya doğrulama düzeni yoktur. Doğrulama denetimleri eklemek veya arabirimleri özelleştirmek için, BoundFields alanlarını TemplateFields 'e dönüştürmeniz gerekir. Daha fazla bilgi için, [Denetim Için doğrulama denetimleri ekleme ve arabirimleri](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) ekleme ve [veri değişikliği arabirimi](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) öğreticilerini özelleştirme bölümüne bakın.

Ayrıca, güncelleştiren ve silmenin yanı sıra, DetailsView 'un yalnızca `DataKeyNames` özelliği yapılandırılmışsa bulunan geçerli ürün `DataKey` değerini kullandığını göz önünde bulundurun. Düzenlemenin veya silmenin hiçbir etkisi yoksa, `DataKeyNames` özelliğinin ayarlandığından emin olun.

## <a name="limitations-of-automatically-generating-sql-statements"></a>Otomatik olarak SQL deyimlerini oluşturma sınırlamaları

`INSERT`, `UPDATE`ve `DELETE` deyimlerini oluştur seçeneği yalnızca bir tablodan sütun çekerken kullanılabilir olduğundan, daha karmaşık sorgularda, 1. adımda yaptığımız gibi kendi `INSERT`, `UPDATE`ve `DELETE` deyimlerini yazmanız gerekir. Genellikle, SQL `SELECT` deyimleri, görüntüleme amacıyla bir veya daha fazla arama tablosundan veri getirmek için `JOIN` s kullanır (ürün bilgilerini görüntülerken `Categories` tablo s `CategoryName` alanı geri getirme gibi). Aynı zamanda, kullanıcının temel tabloya (Bu durumda`Products`) veri düzenlemesine, güncelleştirmesine veya eklemesine izin vermek isteyebilirsiniz.

`INSERT`, `UPDATE`ve `DELETE` deyimleri el ile girilebileceği sırada, aşağıdaki zaman kazandıran ipucunu göz önünde bulundurun. İlk olarak, `Products` tablosundan verileri geri çekmesini sağlamak için SqlDataSource 'u ayarlayın. `INSERT`, `UPDATE`ve `DELETE` deyimlerini otomatik olarak oluşturabilmeniz için, veri kaynağı Yapılandırma Sihirbazı ' nı bir tablo veya görünüm ekranından sütunları belirt ' i kullanın. Ardından, Sihirbazı tamamladıktan sonra, Özellikler penceresi SelectQuery öğesini (veya alternatif olarak, veri kaynağını yapılandırma sihirbazına geri dönün, ancak özel bir SQL ifadesini veya saklı yordamı belirtin seçeneğini kullanın) seçin. Sonra `SELECT` ifadesini `JOIN` söz dizimini içerecek şekilde güncelleştirin. Bu teknik, otomatik olarak oluşturulan SQL deyimlerinin zaman kazandıran avantajlarını sağlar ve daha özelleştirilmiş bir `SELECT` bildirimine izin verir.

`INSERT`, `UPDATE`ve `DELETE` deyimlerini otomatik olarak oluşturmanın diğer bir sınırlaması, `INSERT` ve `UPDATE` deyimlerdeki sütunlarda `SELECT` deyimi tarafından döndürülen sütunları temel alır. Bununla birlikte, daha fazla veya daha az alan güncelleştirmeniz veya eklemeniz gerekebilir. Örneğin, 2. adımdaki örnekte, `UnitPrice` BoundField salt okunurdur. Bu durumda, `UpdateCommand`görünmemelidir. Ya da GridView 'da görünmeyen bir tablo alanının değerini ayarlamak isteyebilir. Örneğin, yeni bir kayıt eklenirken `QuantityPerUnit` değerini TODO olarak ayarlamak isteyebilirsiniz.

Bu tür özelleştirmeler gerekliyse, sihirbazda Özellikler penceresi, özel bir SQL deyimi veya saklı yordam belirt seçeneğini veya bildirim temelli sözdizimini kullanarak el ile yapmanız gerekir.

> [!NOTE]
> Veri Web denetiminde karşılık gelen alanları olmayan parametreler eklenirken, bu parametre değerlerinin bir şekilde değer atanması gerektiğini aklınızda bulundurun. Bu değerler: doğrudan `InsertCommand` veya `UpdateCommand`sabit kodlanmış olabilir; önceden tanımlanmış bir kaynaktan gelebilir (QueryString, oturum durumu, sayfadaki Web denetimleri vb.); ya da, önceki öğreticide gördüğünüz gibi programlı bir şekilde atanabilir.

## <a name="summary"></a>Özet

Veri Web denetimlerinin yerleşik ekleme, düzenlemesi ve silme yeteneklerini kullanabilmesi için, bağlandıkları veri kaynağı denetimi bu işlevselliği sunmalıdır. Bu, SqlDataSource için `INSERT`, `UPDATE`ve `DELETE` SQL deyimlerinin `InsertCommand`, `UpdateCommand`ve `DeleteCommand` özelliklerine atanması gerektiği anlamına gelir. Bu özellikler ve karşılık gelen parametreler koleksiyonları el ile eklenebilir veya veri kaynağı Yapılandırma Sihirbazı aracılığıyla otomatik olarak oluşturulabilir. Bu öğreticide her iki tekniği de inceledik.

Iyimser eşzamanlılık öğreticisini [uygulayan](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) ObjectDataSource ile iyimser eşzamanlılık kullanmayı inceledik. Ayrıca, SqlDataSource denetimi iyimser eşzamanlılık desteği de sağlar. Adım 2 ' de belirtildiği gibi, `INSERT`, `UPDATE`ve `DELETE` deyimlerini otomatik olarak oluştururken, sihirbaz bir iyimser eşzamanlılık seçeneği sunar. Sonraki öğreticide göreceğiniz gibi, SqlDataSource ile iyimser eşzamanlılık kullanmak, `UPDATE` ve `DELETE` deyimlerdeki `WHERE` yan tümceleri değiştirerek verilerin sayfada son görüntülenmesinden bu yana değiştirilmemesini sağlar.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](using-parameterized-queries-with-the-sqldatasource-vb.md)
> [İleri](implementing-optimistic-concurrency-with-the-sqldatasource-vb.md)
