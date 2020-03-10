---
uid: web-pages/overview/data/5-working-with-data
title: ASP.NET Web Pages (Razor) sitelerindeki bir veritabanıyla çalışmaya giriş | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde, bir veritabanından verilere erişme ve ASP.NET Web sayfaları kullanılarak görüntüleme açıklanmaktadır.
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586536"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) sitelerindeki bir veritabanıyla çalışmaya giriş

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde veritabanı oluşturmak için Microsoft WebMatrix araçları 'nın nasıl kullanılacağı ve verileri görüntüleme, ekleme, düzenleme ve silme gibi sayfalar oluşturma işlemlerinin nasıl yapılacağı açıklanır.
> 
> **Şunları öğreneceksiniz:** 
> 
> - Veritabanı oluşturma.
> - Veritabanına bağlanma.
> - Verileri bir Web sayfasında görüntüleme.
> - Veritabanı kayıtlarını ekleme, güncelleştirme ve silme.
> 
> Makalesinde sunulan özellikler şunlardır:
> 
> - Microsoft SQL Server Compact Edition veritabanıyla çalışma.
> - SQL sorgularıyla çalışma.
> - `Database` sınıfı.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - WebMatrix 2
>   
> 
> Bu öğretici WebMatrix 3 ile de kullanılabilir. ASP.NET Web sayfaları 3 ve Visual Studio 2013 (veya Web için Visual Studio Express 2013) kullanabilirsiniz; Ancak, Kullanıcı arabirimi farklı olacaktır.

## <a name="introduction-to-databases"></a>Veritabanlarına giriş

Tipik bir adres kitabı düşünün. Adres defterindeki her giriş için (yani, her bir kişi için) adı, soyadı, adresi, e-posta adresi ve telefon numarası gibi çeşitli bilgi parçaları vardır.

Bu gibi verileri resimlerin tipik bir yolu, satırlar ve sütunlar içeren bir tablo gibidir. Veritabanı koşullarında, her satır genellikle kayıt olarak adlandırılır. Her bir sütun (bazen alan olarak adlandırılır) her veri türü için bir değer içerir: adı, soyadı ve benzeri.

| **ID** | **FirstName** | **Soyadı** | **Adrestir** | **E-posta** | **Numarası** |
| --- | --- | --- | --- | --- | --- |
| 1\. | Jim | Abrus | 210 lük St Orca WA 98031 | jim@contoso.com | 555 0100 |
| 2 | Terry | Adams | 1234 Main St. Seattle WA 99011 | terry@cohowinery.com | 555 0101 |

Çoğu veritabanı tablolarında, tabloda, bir müşteri numarası, hesap numarası vb. gibi benzersiz bir tanımlayıcı içeren bir sütun olması gerekir. Bu, tablonun *birincil anahtarı*olarak bilinir ve tablodaki her satırı tanımlamak için kullanırsınız. Örnekte, KIMLIK sütunu, adres defterinin birincil anahtarıdır.

Veritabanlarının bu temel olarak anlaşılmasından sonra basit bir veritabanı oluşturmayı ve veri ekleme, değiştirme ve silme gibi işlemleri yapmayı öğrenirsiniz.

> [!TIP] 
> 
> **İlişkisel veritabanları**
> 
> Metin dosyaları ve elektronik tablolar dahil olmak üzere çok çeşitli yollarla verileri saklayabilirsiniz. Çoğu iş için, veriler ilişkisel bir veritabanında depolanır.
> 
> Bu makale, veritabanlarına çok daha fazla gidemez. Ancak, bunlar hakkında biraz bilgi edinmek için yararlı olabilir. İlişkisel bir veritabanında, bilgiler mantıksal olarak ayrı tablolara bölünür. Örneğin, okul için bir veritabanı öğrenciler ve sınıf teklifleri için ayrı tablolar içerebilir. Veritabanı yazılımı (örneğin SQL Server), tablolar arasındaki ilişkileri dinamik olarak oluşturmanıza imkan tanıyan güçlü komutları destekler. Örneğin, bir zamanlama oluşturmak için öğrenciler ve sınıflar arasında mantıksal bir ilişki oluşturmak üzere ilişkisel veritabanını kullanabilirsiniz. Verileri ayrı tablolarda depolamak tablo yapısının karmaşıklığını azaltır ve gereksiz verileri tablolarda saklama gereksinimini azaltır.

## <a name="creating-a-database"></a>Veritabanı Oluşturma

Bu yordamda, WebMatrix 'e dahil olan SQL Server Compact veritabanı tasarım aracını kullanarak Smallbakarate adlı bir veritabanının nasıl oluşturulacağı gösterilmektedir. Kod kullanarak bir veritabanı oluşturabilseniz de, WebMatrix gibi bir tasarım aracı kullanarak veritabanı ve veritabanı tablolarını oluşturmak daha normaldir.

1. WebMatrix 'i başlatın ve hızlı başlangıç sayfasında, **şablondan site**' ye tıklayın.
2. **Boş site**' yi seçin ve **site adı** kutusuna "smallbakgir" yazın ve ardından **Tamam**' a tıklayın. Site, WebMatrix 'te oluşturulur ve görüntülenir.
3. Sol bölmede **veritabanları** çalışma alanına tıklayın.
4. Şeritte **Yeni veritabanı**' na tıklayın. Siteniz ile aynı adda boş bir veritabanı oluşturulur.
5. Sol bölmede, **Smallbakmes. sdf** düğümünü genişletin ve **Tablolar**' a tıklayın.
6. Şeritte **Yeni tablo**' ya tıklayın. WebMatrix tablo tasarımcısını açar.

    ![görüntüyle](5-working-with-data/_static/image1.jpg)
7. **Ad** sütununa tıklayın ve &quot;kimliği&quot;girin.
8. **Veri türü** sütununda **int**' i seçin.
9. **Birincil anahtar mı yapılsın** ? seçenekleri **Evet**olarak **belirleyin** .

    Adından da anlaşılacağı gibi, **birincil anahtar** veritabanına bunun tablonun birincil anahtarı olacağını söyler. **Kimliği** , veritabanına her yeni kayıt için otomatik olarak bir kimlik numarası oluşturmasını ve bir sonraki ardışık numarayı (1 ' den başlayarak) atamasını söyler.
10. Sonraki satıra tıklayın. Düzenleyici yeni bir sütun tanımı başlatır.
11. Ad değeri için &quot;ad&quot;girin.
12. **Veri türü**için &quot;nvarchar&quot; seçin ve uzunluğu 50 olarak ayarlayın. `nvarchar` 'ın *var* olan bölümü veritabanına bu sütundaki verilerin boyutu, kaydın kaydına göre değişebilen bir dize olacağını söyler. ( *N* ön eki, alanın, Unicode verileri tutan herhangi bir alfabeyi veya yazma sistemini &#8212; temsil eden karakter verilerini tutabileceğini gösteren *Ulusal*temsil eder.)
13. **Null değerlere Izin ver** seçeneğini **Hayır**olarak ayarlayın. Bu, *ad* sütununun boş bırakılmadığından zorlanır.
14. Aynı işlemi kullanarak, *Açıklama*adlı bir sütun oluşturun. **Veri türü** değerini "nvarchar" ve 50 olarak ayarlayın ve **null değerlere izin ver** değerini false olarak ayarlayın.
15. *Price*adlı bir sütun oluşturun. **Veri türünü "para" olarak** ayarlayın ve **null değerlere izin ver** değerini false olarak ayarlayın.
16. Üstteki kutuya &quot;ürün&quot;adını adlandırın.

    İşiniz bittiğinde, tanım şöyle görünür:

    ![görüntüyle](5-working-with-data/_static/image2.png)
17. Tabloyu kaydetmek için CTRL + S tuşlarına basın.

## <a name="adding-data-to-the-database"></a>Veritabanına veri ekleme

Artık, bu makalede daha sonra çalışacağımız bazı örnek verileri veritabanınıza ekleyebilirsiniz.

1. Sol bölmede, **Smallbakmes. sdf** düğümünü genişletin ve **Tablolar**' a tıklayın.
2. Ürün tablosuna sağ tıklayın ve ardından **veriler**' e tıklayın.
3. Düzenle bölmesinde, aşağıdaki kayıtları girin:

    | **Ad** | **Açıklama** | **Bkz** |
    | --- | --- | --- |
    | Ekmek | Her gün yeni bir bakmış. | 2.99 |
    | Çilekli pasta | Bahçemizdeki organik strawberrıes ile yapılır. | 9.99 |
    | Apple pasta | İkinci olarak yalnızca anneciğim pastana. | 12.99 |
    | Pecan pasta | Bu şekilde karşılaşırsanız, sizin için bu sizin için önemlidir. | 10.99 |
    | Açık pasta | Dünyanın en iyi yanlarına göre yapılır. | 11.99 |
    | Çörekler | Çocuklarınız ve çocuklarınız bunları seveceksiniz. | 7.99 |

    *Kimlik* sütunu için herhangi bir şey girmeniz gerekeceğini unutmayın. *ID* sütununu oluştururken, **Identity** özelliği true olarak ayarlanır, bu da otomatik olarak doldurulmasına neden olur.

    Verileri girmeyi tamamladığınızda Tablo Tasarımcısı şöyle görünür:

    ![görüntüyle](5-working-with-data/_static/image3.jpg)
4. Veritabanı verilerini içeren sekmeyi kapatın.

## <a name="displaying-data-from-a-database"></a>Veritabanından verileri görüntüleme

Verileri içeren bir veritabanına sahip olduktan sonra, verileri bir ASP.NET Web sayfasında görüntüleyebilirsiniz. Görüntülenecek tablo satırlarını seçmek için, veritabanına geçirdiğiniz bir komut olan bir SQL ifadesini kullanırsınız.

1. Sol bölmede **dosyalar** çalışma alanına tıklayın.
2. Web sitesinin kökünde *ListProducts. cshtml*adlı yenı bir cshtml sayfası oluşturun.
3. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    İlk kod bloğunda, daha önce oluşturduğunuz *Smallbakarah. sdf* dosyasını (veritabanı) açarsınız. `Database.Open` yöntemi *. sdf* dosyasının web sitenizin *App\_Data* klasöründe olduğunu varsayar. ( *. Sdf* uzantısını &#8212; aslında belirtmeniz gerekmez, bunu yaparsanız `Open` yöntemi çalışmaz.)

    > [!NOTE]
    > *Uygulama\_veri* klasörü, veri dosyalarını depolamak için kullanılan ASP.NET içinde özel bir klasördür. Daha fazla bilgi için bu makalenin ilerleyen kısımlarında [bir veritabanına bağlanma](#SB_ConnectingToADatabase) bölümüne bakın.

    Ardından, aşağıdaki SQL `Select` ifadesini kullanarak veritabanını sorgulamak için bir istek yaparsınız:

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    İfadesinde, sorgulanacak tabloyu `Product` tanımlar. `*` karakteri sorgunun tablodaki tüm sütunları döndürmesi gerektiğini belirtir. (Sütunları yalnızca bir kısmını görmek isterseniz, sütunları virgülle ayırarak ayrı ayrı listeleyebilirsiniz.) `Order By` yan tümcesi, verilerin bu durumda *ad* sütununa göre &#8212; nasıl sıralanacağını gösterir. Bu, verilerin her satır için *ad* sütununun değerine göre alfabetik olarak sıralandığı anlamına gelir.

    Sayfanın gövdesinde, biçimlendirme, verileri göstermek için kullanılacak bir HTML tablosu oluşturur. `<tbody>` öğesinin içinde, sorgu tarafından döndürülen her bir veri satırını tek tek almak için bir `foreach` döngüsü kullanırsınız. Her veri satırı için bir HTML tablo satırı (`<tr>` öğesi) oluşturursunuz. Daha sonra her bir sütun için HTML tablosu hücreleri (`<td>` öğeleri) oluşturursunuz. Döngüden her gittiğinizde, veritabanının bir sonraki kullanılabilir satırı `row` değişkenidir (bunu `foreach` ifadesinde ayarlarsınız). Satırdan ayrı bir sütun almak için `row.Name` veya `row.Description` ya da istediğiniz sütunun adının ne olduğunu seçebilirsiniz.
4. Sayfayı bir tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) Sayfada aşağıdaki gibi bir liste görüntülenir:

    ![görüntüyle](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> **Yapılandırılmış Sorgu Dili (SQL)**
> 
> SQL, bir veritabanındaki verileri yönetmek için en ilişkisel veritabanlarında kullanılan bir dildir. Veri almanıza ve güncelleştirmenizi sağlayan ve veritabanı tabloları oluşturmanıza, değiştirmenize ve yönetmenize olanak tanıyan komutları içerir. SQL, bir programlama dilinden (WebMatrix 'te kullandığınız gibi) farklıdır, bu da veritabanını istediğiniz gibi söylemeniz ve verilerin nasıl alınacağını ya da görevin nasıl gerçekleştirileceğini anlamak için veritabanının işi olduğunu düşünvidir. Aşağıda bazı SQL komutlarının örnekleri ve ne yapacaklarıdır:
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> Bu, *Fiyat* değeri 10 ' dan büyükse *ürün* tablosundaki kayıtlardan *kimliği*, *adı*ve *Fiyat* sütunlarını getirir ve *ad* sütununun değerlerine göre sonuçları alfabetik sırada döndürür. Bu komut, ölçütlere uyan kayıtları veya hiçbir kayıt eşleşmezse boş bir kümeyi içeren bir sonuç kümesi döndürür.
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> Bu, *ürün* tablosuna yeni bir kayıt ekler, *ad* sütununu &quot;croissant&quot;, *Açıklama* sütununu ise bir düzleme&quot;&quot;ve fiyatı 1,99 olarak ayarlar.
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> Bu komut, son kullanma tarihi sütunu 1 Ocak 2008 ' den daha eski olan *ürün* tablosundaki kayıtları siler. (Bu, *ürün* tablosunun elbette böyle bir sütun olduğunu varsayar.) Tarih, AA/GG/YYYY biçiminde girilir, ancak yerel ayarınız için kullanılan biçimde girilmelidir.
> 
> `Insert Into` ve `Delete` komutları sonuç kümeleri döndürmez. Bunun yerine, komuttan kaç kaydın etkilendiğini belirten bir sayı döndürür.
> 
> Bu işlemlerden bazıları (kayıtları ekleme ve silme gibi) için, işlemi isteyen işlemin veritabanında uygun izinlere sahip olması gerekir. Bu nedenle, veritabanına bağlanırken genellikle bir Kullanıcı adı ve parola sağlamanız gerekir.
> 
> Onlarca SQL komutu vardır, ancak hepsi bunun gibi bir model izler. SQL komutlarını kullanarak veritabanı tabloları oluşturabilir, tablodaki kayıt sayısını sayabilir, fiyatları hesaplayabilir ve birçok daha fazla işlem gerçekleştirebilirsiniz.

## <a name="inserting-data-in-a-database"></a>Veritabanına veri ekleme

Bu bölümde, kullanıcıların *ürün* veritabanı tablosuna yeni bir ürün eklemesine olanak tanıyan bir sayfa oluşturma gösterilmektedir. Yeni bir ürün kaydı eklendikten sonra sayfa, önceki bölümde oluşturduğunuz *ListProducts. cshtml* sayfasını kullanarak güncelleştirilmiş tabloyu görüntüler.

Sayfa, kullanıcının girdiği verilerin veritabanı için geçerli olduğundan emin olmak için doğrulama içerir. Örneğin, sayfadaki kod tüm gerekli sütunlar için bir değer girildiğinden emin olmanızı sağlar.

1. Web sitesinde *ınsertproducts. cshtml*adlı yenı bir cshtml dosyası oluşturun.
2. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    Sayfanın gövdesi, kullanıcıların bir ad, açıklama ve fiyat girmelerini sağlayan üç metin kutusu içeren bir HTML formu içerir. Kullanıcılar **Ekle** düğmesine tıkladığınızda, sayfanın üst kısmındaki kod *smallbakuna. sdf* veritabanına bir bağlantı açar. Daha sonra, `Request` nesnesini kullanarak kullanıcının gönderdiği değerleri alır ve bu değerleri yerel değişkenlere atar.

    Kullanıcının gerekli her sütun için bir değer girdiğini doğrulamak için, doğrulamak istediğiniz her bir `<input>` öğesini kaydedersiniz:

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    `Validation` Yardımcısı, kaydettiğiniz alanların her birinde bir değer olup olmadığını denetler. Kullanıcıdan aldığınız bilgileri işleyebilmeniz için genellikle yaptığınız `Validation.IsValid()`denetleyerek doğrulama işleminin başarılı olup olmadığını test edebilirsiniz:

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    (`&&` işleci anlamına gelir — bu test, *Bu bir form GÖNDERISCIDIR ve tüm alanlar doğrulamayı geçtiğinde*olur.)

    Tüm sütunlar (hiçbiri boş) doğrulandıktan sonra, verileri eklemek ve ardından sonraki gösterildiği gibi yürütmek için bir SQL açıklaması oluşturun:

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    Eklenecek değerler için parametre yer tutucuları (`@0`, `@1`, `@2`) dahil edersiniz.

    > [!NOTE]
    > Bir güvenlik önlemi olarak, önceki örnekte gördüğünüz gibi parametreleri kullanarak her zaman bir SQL ifadesine değer geçirin. Bu size, kullanıcının verilerini doğrulama şansı sağlar ve veritabanınıza kötü amaçlı komutlar gönderme girişimlerine karşı korunmaya yardımcı olur (bazen SQL ekleme saldırıları olarak adlandırılır).

    Sorguyu yürütmek için, bu ifadeyi, yer tutucular için değiştirilecek değerleri içeren değişkenleri geçirerek kullanın:

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    `Insert Into` deyimleri yürütüldükten sonra, kullanıcıyı bu satırı kullanarak ürünleri listeleyen sayfaya gönderirsiniz:

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    Doğrulama başarılı olmadıysa, eklemeyi atlayın. Bunun yerine, sayfada birikmiş hata mesajlarını (varsa) görüntüleyebilen bir yardımınızın olması gerekir:

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    İşaretlemede stil bloğunun `.validation-summary-errors`adlı bir CSS sınıfı tanımını içerdiğine dikkat edin. Bu, herhangi bir doğrulama hatası içeren `<div>` öğesi için varsayılan olarak kullanılan CSS sınıfının adıdır. Bu durumda, CSS sınıfı doğrulama özeti hatalarının kırmızı ve kalın olarak görüntülendiğini belirtir, ancak istediğiniz biçimlendirmeyi göstermek için `.validation-summary-errors` sınıfını tanımlayabilirsiniz.

### <a name="testing-the-insert-page"></a>Ekleme sayfasını test etme

1. Sayfayı bir tarayıcıda görüntüleyin. Sayfa, aşağıdaki çizimde gösterilenle benzer bir form görüntüler.

    ![görüntüyle](5-working-with-data/_static/image5.jpg)
2. Tüm sütunlar için değerler girin, ancak *Fiyat* sütununu boş bıraktığınızdan emin olun.
3. **Ekle**'ye tıklayın. Sayfada aşağıdaki çizimde gösterildiği gibi bir hata iletisi görüntülenir. (Yeni bir kayıt oluşturulmaz.)

    ![görüntüyle](5-working-with-data/_static/image6.jpg)
4. Formu tamamen doldurun ve ardından **Ekle**' ye tıklayın. Bu kez, *ListProducts. cshtml* sayfası görüntülenir ve yeni kaydı gösterir.

## <a name="updating-data-in-a-database"></a>Veritabanındaki verileri güncelleştirme

Veriler bir tabloya girildikten sonra güncelleştirmeniz gerekebilir. Bu yordamda, daha önce veri ekleme için oluşturuldıklarıyla benzer iki sayfa oluşturma işlemi gösterilir. İlk sayfa ürünleri görüntüler ve kullanıcıların değiştirmek için bir tane seçmesini sağlar. İkinci sayfa, kullanıcıların düzenlemeleri gerçekten yapıp kaydetmelerini sağlar.

> [!NOTE] 
> 
> **Önemli** Bir üretim web sitesinde, genellikle verilerde değişiklik yapmasına izin verilen kişileri kısıtlayabilirsiniz. Üyeliği ayarlama ve kullanıcılara sitede görevler gerçekleştirme izni verme yolları hakkında bilgi için bkz. [ASP.NET Web Pages sitesine güvenlik ve üyelik ekleme](https://go.microsoft.com/fwlink/?LinkId=202904).

1. Web sitesinde, *Editproducts. cshtml*adlı yenı bir cshtml dosyası oluşturun.
2. Dosyadaki mevcut biçimlendirmeyi aşağıdaki kodla değiştirin:

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    Bu sayfa ile *ListProducts. cshtml* sayfası arasındaki tek fark, bu sayfadaki HTML tablosunun **düzenleme** bağlantısı görüntüleyen ek bir sütun içerir. Bu bağlantıya tıkladığınızda, seçili kaydı düzenleyebileceğiniz *UpdateProducts. cshtml* sayfasına (daha sonra oluşturacaksınız) gidersiniz.

    **Düzenleme** bağlantısını oluşturan koda bakın:

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    Bu, `href` özniteliği dinamik olarak ayarlanmış olan bir HTML `<a>` öğesi oluşturur. `href` özniteliği kullanıcı bağlantıya tıkladığında görüntülenecek sayfayı belirtir. Ayrıca geçerli satırın `Id` değerini bağlantıya geçirir. Sayfa çalıştırıldığında, sayfa kaynağı bunlar gibi bağlantılar içerebilir:

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    `href` özniteliğinin `UpdateProducts/n`olarak ayarlandığını, burada *n* 'nin bir ürün numarası olduğunu unutmayın. Bir Kullanıcı bu bağlantılardan birine tıkladığında, elde edilen URL şöyle görünür:

    `http://localhost:18816/UpdateProducts/6`

    Diğer bir deyişle, düzenlenecek ürün numarası URL 'ye geçirilecektir.
3. Sayfayı bir tarayıcıda görüntüleyin. Sayfa, verileri şöyle bir biçimde görüntüler:

    ![görüntüyle](5-working-with-data/_static/image7.jpg)

    Daha sonra, kullanıcıların verileri gerçekten güncelleştirebilmenizi sağlayan sayfayı oluşturacaksınız. Güncelleştirme sayfası, kullanıcının girdiği verileri doğrulamak için doğrulama içerir. Örneğin, sayfadaki kod tüm gerekli sütunlar için bir değer girildiğinden emin olmanızı sağlar.
4. Web sitesinde *UpdateProducts. cshtml*adlı yenı bir cshtml dosyası oluşturun.
5. Dosyadaki varolan biçimlendirmeyi aşağıdaki ile değiştirin.

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    Sayfanın gövdesi, bir ürünün görüntülendiği ve kullanıcıların bunu düzenleyebilecekleri bir HTML formu içerir. Görüntülenecek ürünü almak için bu SQL ifadesini kullanın:

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    Bu, KIMLIĞI `@0` parametresine geçirilen değerle eşleşen ürünü seçer. ( *Kimlik* birincil anahtar olduğundan ve bu nedenle benzersiz olması gerektiğinden, bu şekilde yalnızca bir ürün kaydı seçilebilir.) Bu `Select` bildirimine geçirilecek KIMLIK değerini almak için, URL 'nin bir parçası olarak, aşağıdaki sözdizimini kullanarak sayfaya geçirilen değeri okuyabilirsiniz:

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    Ürün kaydını gerçekten getirmek için, yalnızca bir kayıt döndüren `QuerySingle` yöntemini kullanırsınız:

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    Tek satır `row` değişkenine döndürülür. Her sütundan veri alabilir ve bunu şöyle yerel değişkenlere atayabilirsiniz:

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    Formun biçimlendirmesinde, bu değerler, aşağıdaki gibi katıştırılmış kod kullanılarak tek tek metin kutularında otomatik olarak görüntülenir:

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    Kodun bu bölümü, güncellenen ürün kaydını görüntüler. Kayıt görüntülenirken, Kullanıcı sütunları tek tek düzenleyebilir.

    Kullanıcı, formu **Güncelleştir** düğmesine tıklayarak gönderdiğinde, `if(IsPost)` bloğundaki kod çalıştırılır. Bu, kullanıcının `Request` nesnesinden değerlerini alır, değerleri değişkenlerde depolar ve her bir sütunun doldurulduğunu doğrular. Doğrulama başarılı olursa, kod aşağıdaki SQL Update ifadesini oluşturur:

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    Bir SQL `Update` ifadesinde güncelleştirilecek her sütunu ve ayarlanacak değeri belirtirsiniz. Bu kodda, değerler `@0`, `@1`, `@2`vb. parametre yer tutucuları kullanılarak belirtilir. (Daha önce belirtildiği gibi, güvenlik için, parametreleri kullanarak her zaman bir SQL ifadesine değer geçirmeniz gerekir.)

    `db.Execute` yöntemini çağırdığınızda, değerleri içeren değişkenleri SQL deyimindeki parametrelere karşılık gelen sırayla geçirirsiniz:

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    `Update` deyimleri yürütüldükten sonra, kullanıcıyı düzenleme sayfasına yeniden yönlendirmek için aşağıdaki yöntemi çağırın:

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    Etki, kullanıcının veritabanındaki verilerin güncelleştirilmiş bir listesini görmüdür ve başka bir ürünü düzenleyebilirler.
6. Sayfayı kaydedin.
7. *Editproducts. cshtml* sayfasını çalıştırın (güncelleştirme sayfasını değil) ve ardından düzenlemek üzere bir ürün seçmek için **Düzenle** ' ye tıklayın. *UpdateProducts. cshtml* sayfası görüntülenir ve seçtiğiniz kaydı gösterir.

    ![görüntüyle](5-working-with-data/_static/image8.jpg)
8. Değişiklik yapıp **Güncelleştir**' e tıklayın. Ürün listesi, güncelleştirilmiş verilerle birlikte gösterilir.

## <a name="deleting-data-in-a-database"></a>Veritabanındaki verileri silme

Bu bölümde, kullanıcıların *ürün veritabanı tablosundan bir ürünü silmesine* izin verilmektedir. Örnek iki sayfadan oluşur. İlk sayfada, kullanıcılar silinecek bir kayıt seçer. Silinecek kayıt daha sonra ikinci bir sayfada görüntülenir ve bu da kayıtları silmek istediğini doğrulayabilirler.

> [!NOTE] 
> 
> **Önemli** Bir üretim web sitesinde, genellikle verilerde değişiklik yapmasına izin verilen kişileri kısıtlayabilirsiniz. Üyeliği ayarlama ve kullanıcı sitede görevleri yerine getirmek için yetkilendirme yolları hakkında bilgi için bkz. [ASP.NET Web Pages sitesine güvenlik ve üyelik ekleme](https://go.microsoft.com/fwlink/?LinkId=202904).

1. Web sitesinde *Listproductsfordelete. cshtml*adlı yenı bir cshtml dosyası oluşturun.
2. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    Bu sayfa, daha önce *Editproducts. cshtml* sayfasına benzerdir. Ancak, her bir ürün için bir **düzenleme** bağlantısı görüntülemek yerine, bir **Delete** bağlantısı görüntüler. **Silme** bağlantısı, biçimlendirmede aşağıdaki katıştırılmış kod kullanılarak oluşturulur:

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    Bu, kullanıcılar bağlantıya tıkladığınızda aşağıdakine benzer bir URL oluşturur:

    `http://<server>/DeleteProduct/4`

    URL, *DeleteProduct. cshtml* adlı bir sayfa çağırır (daha sonra oluşturacağınız) ve SILINECEK ürünün kimliğini (burada, 4) geçirir.
3. Dosyayı kaydedin, ancak açık bırakın.
4. *DeleteProduct. cshtml*adlı başka BIR cHTML dosyası oluşturun. Var olan içeriği aşağıdaki ile değiştirin:

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    Bu sayfa *Listproductsfordelete. cshtml* tarafından çağrılır ve kullanıcıların bir ürünü silmek istediğini onaylamasını sağlar. Silinecek ürünü listelemek için aşağıdaki kodu kullanarak URL 'den silinecek ürünün KIMLIĞINI alırsınız:

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    Daha sonra sayfa, kullanıcıdan kaydı gerçekten silmek için bir düğmeye tıklatabuyor. Bu önemli bir güvenlik ölçümüdür: Web sitenizde verileri güncelleştirme veya silme gibi hassas işlemler gerçekleştirdiğinizde, bu işlemler her zaman bir POST işlemi kullanılarak yapılmalıdır, bir alma işlemi değil. Siteniz, bir GET işlemi kullanılarak bir silme işleminin gerçekleştirilebilmesi için ayarlandıysa, herkes `http://<server>/DeleteProduct/4` gibi bir URL 'YI geçirebilir ve veritabanınızda istedikleri şeyi silebilir. Silmeyi ekleyerek ve silme işleminin yalnızca bir GÖNDERI kullanılarak gerçekleştirilebilmesi için sayfayı kodlayarak, sitenize bir güvenlik ölçüsü eklersiniz.

    Gerçek silme işlemi, ilk olarak bu bir POST işlemi olduğunu ve KIMLIğIN boş olmadığını doğrulayan aşağıdaki kod kullanılarak gerçekleştirilir:

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    Kod, belirtilen kaydı silen bir SQL ifadesini çalıştırır ve ardından kullanıcıyı listeleme sayfasına yeniden yönlendirir.
5. Bir tarayıcıda *Listproductsfordelete. cshtml* dosyasını çalıştırın.

    ![görüntüyle](5-working-with-data/_static/image9.jpg)
6. Ürünlerden biri için **silme** bağlantısına tıklayın. Bu kaydı silmek istediğinizi onaylamak için *DeleteProduct. cshtml* sayfası görüntülenir.
7. **Sil** düğmesine tıklayın. Ürün kaydı silinir ve sayfa güncelleştirilmiş bir ürün listesi ile yenilenir.

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a>Veritabanına bağlanma
> 
> Veritabanına iki şekilde bağlanabilirsiniz. Birincisi `Database.Open` yöntemini kullanmaktır ve veritabanı dosyasının adını ( *. sdf* uzantısı) belirtmek için:
> 
> `var db = Database.Open("SmallBakery");`
> 
> `Open` yöntemi bu olduğunu varsayar. *sdf* dosyası, Web sitesinin *App\_Data* klasöründedir. Bu klasör, verileri tutmak için özel olarak tasarlanmıştır. Örneğin, Web sitesinin verileri okumasına ve yazmasına izin vermek için uygun izinlere sahip olması ve bir güvenlik ölçüsü olması, WebMatrix bu klasörden dosyalara erişime izin vermez.
> 
> İkinci yöntem bir bağlantı dizesi kullanmaktır. Bir bağlantı dizesi, bir veritabanına nasıl bağlanılacağıyla ilgili bilgi içerir. Bu bir dosya yolu içerebilir veya bu sunucuya bağlanmak için bir Kullanıcı adı ve parola ile birlikte bir SQL Server veritabanının adını yerel veya uzak bir sunucuya dahil edebilir. (Bir barındırma sağlayıcısının sitesi gibi SQL Server Merkezi olarak yönetilen bir sürümünde verileri tutarsanız, veritabanı bağlantı bilgilerini belirtmek için her zaman bir bağlantı dizesi kullanırsınız.)
> 
> WebMatrix 'te, bağlantı dizeleri genellikle *Web. config*ADLı bir XML dosyasında depolanır. Adından da anlaşılacağı gibi, sitenizin gerekli olabileceği bağlantı dizeleri de dahil olmak üzere, sitenin yapılandırma bilgilerini depolamak için Web sitenizin kökündeki bir *Web. config* dosyası kullanabilirsiniz. Bir *Web. config* dosyasındaki bağlantı dizesinin bir örneği aşağıdaki gibi görünebilir:
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> Örnekte, bağlantı dizesi bir sunucuda çalışan bir SQL Server örneğindeki bir veritabanını (yerel *. sdf* dosyasının aksine) işaret eder. `myServer` ve `myDatabase`ilgili adları yerine getirmeniz ve `username` ve `password`için SQL Server oturum açma değerlerini belirtmeniz gerekir. (Kullanıcı adı ve parola değerleri, Windows kimlik bilgilerinizle aynı veya barındırma sağlayıcınızın kendi sunucularında oturum açmak için size verdiği değerler olarak aynı değildir. İhtiyaç duyduğunuz tam değerler için yöneticiye danışın.)
> 
> `Database.Open` yöntemi esnektir, çünkü bir Database *. sdf* dosyasının veya *Web. config* dosyasında depolanan bir bağlantı dizesinin adını geçirmenize izin verir. Aşağıdaki örnek, önceki örnekte gösterilen bağlantı dizesi kullanılarak veritabanına nasıl bağlanılacağını gösterir:
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> Belirtildiği gibi `Database.Open` yöntemi, bir veritabanı adı veya bağlantı dizesi iletmenize olanak tanır ve bunu kullanmayı da anlayabilir. Bu, Web sitenizi dağıtırken (yayımladığınızda) çok yararlı olur. Sitenizi geliştirirken ve sınarken *App\_Data* klasöründe bir *. sdf* dosyası kullanabilirsiniz. Daha sonra, sitenizi bir üretim sunucusuna taşıdığınızda, *Web. config* dosyasında *. sdf* dosyanız ile aynı ada sahip olan ancak bu, barındırma sağlayıcısının veritabanına &#8212; , kodunuzu değiştirmeye gerek kalmadan işaret eden bir bağlantı dizesi kullanabilirsiniz.
> 
> Son olarak, bir bağlantı dizesiyle doğrudan çalışmak istiyorsanız, `Database.OpenConnectionString` yöntemini çağırabilir ve *Web. config* dosyasında yalnızca birinin adı yerine gerçek bağlantı dizesine geçirebilirsiniz. Bu, bazı nedenlerle bağlantı dizesine (veya *. sdf* dosya adı gibi) erişim sahibi olmadığınız durumlarda, sayfa çalışmadığı sürece yararlı olabilir. Ancak çoğu senaryoda, bu makalede açıklandığı gibi `Database.Open` kullanabilirsiniz.

## <a name="additional-resources"></a>Ek Kaynaklar

- [SQL Server Compact](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [WebMatrix 'te bir SQL Server veya MySQL veritabanına bağlanma](https://go.microsoft.com/fwlink/?LinkId=208661)
- [ASP.NET Web Sayfaları Sitelerinde Kullanıcı Girişini Doğrulama](https://go.microsoft.com/fwlink/?LinkId=253002)
