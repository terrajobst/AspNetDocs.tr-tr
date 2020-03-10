---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: Entity Framework model sınıfları oluşturma (VB) | Microsoft Docs
author: microsoft
description: Bu öğreticide, ASP.NET MVC 'yi Microsoft Entity Framework kullanmayı öğreneceksiniz. ADO.NET varlığı oluşturmak için varlık Sihirbazı 'nı nasıl kullanacağınızı öğrenirsiniz...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: f6c896c6f5f6d898ac6f99d5998fb29cb73bcb10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543332"
---
# <a name="creating-model-classes-with-the-entity-framework-vb"></a>Entity Framework ile Model Sınıfları Oluşturma (VB)

[Microsoft](https://github.com/microsoft) tarafından

> Bu öğreticide, ASP.NET MVC 'yi Microsoft Entity Framework kullanmayı öğreneceksiniz. ADO.NET Varlık Veri Modeli oluşturmak için varlık Sihirbazı 'nı nasıl kullanacağınızı öğrenirsiniz. Bu öğreticide, Entity Framework kullanarak veritabanı verilerini seçme, ekleme, güncelleştirme ve silmeyi gösteren bir Web uygulaması oluşturacağız.

Bu öğreticinin amacı, bir ASP.NET MVC uygulaması oluştururken Microsoft Entity Framework kullanarak veri erişim sınıfları oluşturmayı açıklamaktır. Bu öğreticide, Microsoft Entity Framework 'in önceki bilgileri bulunmamaktadır. Bu öğreticinin sonuna kadar Entity Framework kullanarak veritabanı kayıtlarını seçme, ekleme, güncelleştirme ve silme işlemlerinin nasıl yapılacağını anlayacaksınız.

Microsoft Entity Framework, bir veritabanından otomatik olarak veri erişim katmanı oluşturmanıza olanak sağlayan bir nesne Ilişkisel eşleme (O/RM) aracıdır. Entity Framework, veri erişim sınıflarınızı el ile oluşturmaya yönelik sıkıcı çalışmalardan kaçınmanızı sağlar.

> [!NOTE] 
> 
> ASP.NET MVC ile Microsoft Entity Framework arasında önemli bir bağlantı yoktur. Entity Framework için ASP.NET MVC ile kullanabileceğiniz çeşitli alternatifler vardır. Örneğin, MVC model sınıflarınızı Microsoft LINQ to SQL, Nhazırda bekleme veya alt Sonic gibi diğer O/RM araçlarını kullanarak oluşturabilirsiniz.

ASP.NET MVC ile Microsoft Entity Framework nasıl kullanabileceğinizi göstermek için basit bir örnek uygulama oluşturacağız. Film veritabanı kayıtlarını görüntülemenizi ve düzenlemenizi sağlayan bir film veritabanı uygulaması oluşturacağız.

Bu öğreticide, Service Pack 1 ile Visual Studio 2008 veya Visual Web Developer 2008 sahip olduğunuz varsayılır. Entity Framework kullanabilmeniz için hizmet paketi 1 ' i kullanmanız gerekir. Visual Studio 2008 Service Pack 1 veya Visual Web Developer with Service Pack 1 ' i aşağıdaki adresten indirebilirsiniz:

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

## <a name="creating-the-movie-sample-database"></a>Film örnek veritabanı oluşturma

Film veritabanı uygulaması, aşağıdaki sütunları içeren filmler adlı bir veritabanı tablosu kullanır:

| Sütun adı | Veri Türü | Null değerlere izin verilsin mi? | Birincil anahtar mi? |
| --- | --- | --- | --- |
| Kimlik | int | False | Doğru |
| Başlık | Nvarchar (100) | False | False |
| Direktörü | Nvarchar (100) | False | False |

Aşağıdaki adımları izleyerek, bu tabloyu bir ASP.NET MVC projesine ekleyebilirsiniz:

1. Çözüm Gezgini penceresindeki uygulama\_veri klasörüne sağ tıklayın ve **Ekle, yeni öğe** menü seçeneğini belirleyin.
2. **Yeni öğe Ekle** iletişim kutusunda **SQL Server veritabanı**' nı seçin, veritabanına MoviesDB. mdf adını verin ve **Ekle** düğmesine tıklayın.
3. Sunucu Gezgini/Veritabanı Gezgini penceresini açmak için MoviesDB. mdf dosyasına çift tıklayın.
4. MoviesDB. mdf veritabanı bağlantısını genişletin, tablolar klasörüne sağ tıklayın ve **Yeni Tablo Ekle**menü seçeneğini belirleyin.
5. Tablo Tasarımcısı kimliği, başlığı ve yönetmen sütunlarını ekleyin.
6. Yeni tabloyu film adı ile kaydetmek için **Kaydet** düğmesine (disketin simgesine sahiptir) tıklayın.

Filmler veritabanı tablosunu oluşturduktan sonra tabloya bazı örnek veriler eklemelisiniz. Filmler tablosuna sağ tıklayın ve **tablo verilerini göster**menü seçeneğini belirleyin. Sahte film verilerini görüntülenen kılavuza girebilirsiniz.

## <a name="creating-the-adonet-entity-data-model"></a>ADO.NET Varlık Veri Modeli oluşturma

Entity Framework kullanmak için bir Varlık Veri Modeli oluşturmanız gerekir. Bir veritabanından otomatik olarak bir Varlık Veri Modeli oluşturmak için Visual Studio *varlık veri modeli Sihirbazı* 'ndan yararlanabilirsiniz.

Aşağıdaki adımları uygulayın:

1. Çözüm Gezgini penceresinde modeller klasörüne sağ tıklayın ve menü seçeneğini **Ekle, yeni öğe**' yi seçin.
2. **Yeni öğe Ekle** Iletişim kutusunda veri kategorisini seçin (bkz. Şekil 1).
3. **ADO.NET varlık veri modeli** şablonunu seçin, MoviesDBModel. edmx adını varlık veri modeli verin ve **Ekle** düğmesine tıklayın. **Ekle** düğmesine tıkladığınızda veri modeli Sihirbazı başlatılır.
4. **Model Içeriğini seçin** adımında, **bir veritabanından oluştur** seçeneğini belirleyin ve **Ileri** düğmesine (bkz. Şekil 2) tıklayın.
5. **Veri bağlantınızı seçin** adımında, MoviesDB. mdf veritabanı bağlantısını seçin, varlıklar bağlantı ayarları adı MoviesDBEntities yazın ve **İleri** düğmesine tıklayın (bkz. Şekil 3).
6. **Veritabanı nesnelerinizi seçin** adımında, film veritabanı tablosunu seçin ve **son** düğmesine tıklayın (bkz. Şekil 4).

Bu adımları tamamladıktan sonra, ADO.NET Varlık Veri Modeli Tasarımcısı (Entity Desisgner) açılır.

**Şekil 1 – yeni bir Varlık Veri Modeli oluşturma**

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

**Şekil 2 – model Içeriğini seçin adımı**

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

**Şekil 3: veri bağlantınızı seçin**

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

**Şekil 4: veritabanı nesnelerinizi seçin**

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a>ADO.NET Varlık Veri Modeli değiştirme

Bir Varlık Veri Modeli oluşturduktan sonra, Entity Desisgner avantajlarından yararlanarak modeli değiştirebilirsiniz (bkz. Şekil 5). Çözüm Gezgini penceresindeki modeller klasöründe bulunan MoviesDBModel. edmx dosyasını çift tıklayarak Entity Desisgner dilediğiniz zaman açabilirsiniz.

**Şekil 5 – ADO.NET Varlık Veri Modeli Tasarımcısı**

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

Örneğin, varlık modeli verileri Sihirbazının oluşturduğu sınıfların adlarını değiştirmek için Entity Desisgner kullanabilirsiniz. Sihirbaz, filmler adlı yeni bir veri erişim sınıfı oluşturdu. Diğer bir deyişle, sihirbaz sınıfı veritabanı tablosuyla aynı adı vermiştir. Belirli bir film örneğini temsil etmek için bu sınıfı kullanacağından, sınıfı filmlerden filme yeniden adlandırdık.

Bir varlık sınıfını yeniden adlandırmak isterseniz, Entity Desisgner sınıf adına çift tıklayıp yeni bir ad girebilirsiniz (bkz. Şekil 6). Alternatif olarak, Entity Desisgner bir varlık seçtikten sonra Özellikler penceresi varlığın adını değiştirebilirsiniz.

**Şekil 6 – bir varlık adını değiştirme**

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

Kaydet düğmesine (disketin simgesi) tıklayarak bir değişiklik yaptıktan sonra Varlık Veri Modeli kaydetmeyi unutmayın. Arka planda Entity Desisgner, Visual Basic .NET sınıflarının bir kümesini oluşturur. Bu sınıfları, Çözüm Gezgini penceresinden MoviesDBModel. Designer. vb dosyasını açarak görüntüleyebilirsiniz.

Entity Desisgner bir sonraki sefer kullandığınızda değişikliklerinizin üzerine yazılacak olduğundan, Designer. vb dosyasındaki kodu değiştirmeyin. Tasarımcı. vb dosyasında tanımlanan varlık sınıflarının işlevlerini genişletmek istiyorsanız, *kısmi sınıfları* ayrı dosyalarda oluşturabilirsiniz.

#### <a name="selecting-database-records-with-the-entity-framework"></a>Entity Framework ile veritabanı kayıtlarını seçme

Film kayıtlarının listesini görüntüleyen bir sayfa oluşturarak film veritabanı uygulamamızı oluşturmaya başlayalım. Liste 1 ' deki ana denetleyici dizin () adlı bir eylem gösterir. Index () eylemi, Entity Framework avantajlarından yararlanarak film veritabanı tablosundan tüm film kayıtlarını döndürür.

**Listeleme 1 – Controllers\homecontroller.exe**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

Listeleme 1 ' deki denetleyicinin bir Oluşturucu içerdiğine dikkat edin. Oluşturucu \_DB adlı bir sınıf düzeyi alanı başlatır. \_DB alanı, Microsoft Entity Framework tarafından oluşturulan veritabanı varlıklarını temsil eder. \_DB alanı, Entity Desisgner tarafından oluşturulan MoviesDBEntities sınıfının bir örneğidir.

\_DB alanı, filmler veritabanı tablosundan kayıtları almak için dizin () eylemi içinde kullanılır. \_DB ifadesi. MovieSet, filmler veritabanı tablosundaki tüm kayıtları temsil eder. ToList () yöntemi, film kümesini genel bir film nesneleri koleksiyonuna dönüştürmek için kullanılır: liste (film).

Film kayıtları LINQ to Entities yardımıyla alınır. Liste 1 ' deki dizin () eylemi, veritabanı kayıtlarının kümesini almak için LINQ *yöntemi sözdizimini* kullanır. Tercih ederseniz, bunun yerine LINQ *sorgu söz dizimini* kullanabilirsiniz. Aşağıdaki iki deyim de aynı şeyi yapar:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

En sezgisel bulduğunuz LINQ söz dizimi, yöntem sözdizimi veya sorgu söz dizimini kullanın. İki yaklaşım arasında performans farkı yoktur. tek fark stil olur.

Kod 2 ' deki görünüm, film kayıtlarını görüntülemek için kullanılır.

**Listeleme 2 – Views\home\ındex.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

Liste 2 ' deki görünüm, her film kaydı boyunca yinelenen her bir döngü **için** bir içerir ve film kaydının başlık ve yönetmen özelliklerinin değerlerini görüntüler. Her kaydın yanında bir Düzenle ve Sil bağlantısının görüntülendiğini unutmayın. Ayrıca, görünümün alt kısmında bir film ekle bağlantısı görünür (bkz. Şekil 7).

**Şekil 7 – dizin görünümü**

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

Dizin görünümü *türü belirlenmiş bir görünüm*. Dizin görünümü bir Inherits özniteliği içeren &lt;% @ Page%&gt; yönergesine sahip. Inherits özniteliği ViewData. model özelliğini film nesnelerinin bir listesi (film) türü kesin belirlenmiş bir genel liste koleksiyonuna yayınlar.

## <a name="inserting-database-records-with-the-entity-framework"></a>Entity Framework ile veritabanı kayıtları ekleme

Yeni kayıtların bir veritabanı tablosuna eklenmesini kolaylaştırmak için Entity Framework kullanabilirsiniz. Kod 3 ' te, yeni kayıtları film veritabanı tablosuna eklemek için kullanabileceğiniz giriş denetleyicisi sınıfına eklenen iki yeni eylem bulunur.

**Listeleme 3 – Controllers\homecontroller.exe (ekleme yöntemleri)**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

İlk Add () eylemi yalnızca bir görünüm döndürür. Görünüm yeni bir film veritabanı kaydı eklemek için bir form içerir (bkz. Şekil 8). Formu gönderdiğinizde, ikinci Add () eylemi çağrılır.

İkinci Add () eyleminin AcceptVerbs özniteliğiyle birlikte tasarlandığına dikkat edin. Bu eylem, yalnızca bir HTTP POST işlemi gerçekleştirilirken çağrılabilir. Diğer bir deyişle, bu eylem yalnızca bir HTML formu deftere nakledilirken çağrılabilir.

İkinci Add () eylemi, Entity Framework film sınıfının yeni bir örneğini oluşturur, ASP.NET MVC TryUpdateModel () yönteminin yardımıyla. TryUpdateModel () yöntemi, form koleksiyonundaki alanları Add () yöntemine geçirilir ve bu HTML form alanlarının değerlerini film sınıfına atar.

Entity Framework kullanırken, bir varlık sınıfının özelliklerini güncelleştirmek için TryUpdateModel veya UpdateModel yöntemlerini kullanırken bir "beyaz liste" özelliği sağlamanız gerekir.

Sonra, Add () eylemi bazı basit form doğrulaması gerçekleştirir. Eylem hem başlık hem de yönetmen özelliklerinin değerleri olduğunu doğrular. Doğrulama hatası varsa, ModelState 'e bir doğrulama hata iletisi eklenir.

Doğrulama hataları yoksa, filmler veritabanı tablosuna Entity Framework yardımıyla yeni bir film kaydı eklenir. Yeni kayıt veritabanına aşağıdaki iki kod satırı ile eklenir:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

Kodun ilk satırı yeni film varlığını Entity Framework tarafından izlenen Film kümesine ekler. İkinci kod satırı, arka plandaki veritabanına geri izlenmekte olan filmlerde yapılan tüm değişiklikleri kaydeder.

**Şekil 8 – ekleme görünümü**

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a>Veritabanı kayıtlarını Entity Framework güncelleştirme

Yeni bir veritabanı kaydı eklemek istediğimiz yaklaşımda, bir veritabanı kaydını Entity Framework düzenlemek için neredeyse aynı yaklaşımı izleyebilirsiniz. 4\. liste, Edit () adlı iki yeni denetleyici eylemi içerir. İlk düzenleme () eylemi, bir film kaydını düzenlemek için bir HTML formu döndürür. İkinci düzenleme () eylemi veritabanını güncelleştirmeye çalışır.

**Listeleme 4 – Controllers\homecontroller.exe (düzenleme yöntemleri)**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

İkinci düzenleme () eylemi, düzenlenmekte olan filmin kimliğiyle eşleşen veritabanından film kaydını alarak başlatılır. Aşağıdaki LINQ to Entities deyimleri, belirli bir kimlikle eşleşen ilk veritabanı kaydını ifade eden:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

Ardından, HTML form alanlarının değerlerini film varlığının özelliklerine atamak için TryUpdateModel () yöntemi kullanılır. Güncelleştirilecek özelliklerin tam olarak belirtilmesi için bir beyaz liste sağlandığına dikkat edin.

Daha sonra, hem film başlığının hem de yönetmen özelliklerinin değerleri olduğunu doğrulamak için bazı basit doğrulama gerçekleştirilir. Herhangi bir özellikte bir değer eksikse, ModelState ve ModelState 'e bir doğrulama hata iletisi eklenir. IsValid, false değerini döndürür.

Son olarak, doğrulama hatası yoksa, temeldeki filmler veritabanı tablosu, SaveChanges () yöntemi çağırarak herhangi bir değişiklikle güncellenir.

Veritabanı kayıtlarını düzenlediğinizde, düzenlenmekte olan kaydın kimliğini veritabanı güncelleştirmesini gerçekleştiren denetleyici eylemine geçirmeniz gerekir. Aksi takdirde, denetleyici eylemi temel alınan veritabanında hangi kaydın güncelleşeceğimizi bilmez. 5\. listede yer alan düzenleme görünümü, düzenlenmekte olan veritabanı kaydının kimliğini temsil eden bir gizli form alanı içerir.

**Listeleme 5 – Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Entity Framework ile veritabanı kayıtlarını silme

Bu öğreticide yer açmanız gereken son veritabanı işlemi veritabanı kayıtlarını siliyor. Belirli bir veritabanı kaydını silmek için, liste 6 ' daki denetleyici eylemini kullanabilirsiniz.

**6--\Controllers\homecontroller.exe dosyasını listeleme (silme eylemi)**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

Delete () eylemi önce eyleme geçirilen kimlikle eşleşen film varlığını alır. Daha sonra, DeleteObject () yöntemi ve ardından SaveChanges () yöntemi çağırarak film veritabanından silinir. Son olarak, Kullanıcı dizin görünümüne yeniden yönlendirilir.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, ASP.NET MVC ve Microsoft Entity Framework avantajlarından yararlanarak veritabanı odaklı web uygulamaları nasıl oluşturacağınızı göstermektir. Veritabanı kayıtlarını seçmenizi, eklemenizi, güncelleştirmenizi ve silmenizi sağlayan bir uygulama oluşturmayı öğrendiniz.

İlk olarak, Visual Studio içinden bir Varlık Veri Modeli oluşturmak için Varlık Veri Modeli Sihirbazı 'nı nasıl kullanabileceğinizi tartıştık. Daha sonra, bir veritabanı tablosundan veritabanı kayıtları kümesini almak için LINQ to Entities kullanmayı öğreneceksiniz. Son olarak, veritabanı kayıtlarını eklemek, güncelleştirmek ve silmek için Entity Framework kullandık.

> [!div class="step-by-step"]
> [Önceki](validation-with-the-data-annotation-validators-cs.md)
> [İleri](creating-model-classes-with-linq-to-sql-vb.md)
