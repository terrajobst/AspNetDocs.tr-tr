---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
title: SQL önbellek bağımlılıklarını kullanma (C#) | Microsoft Docs
author: rick-anderson
description: En basit önbelleğe alma stratejisi, önbelleğe alınan verilerin belirli bir süre sonra dolmasına izin verecektir. Ancak bu basit yaklaşım, önbelleğe alınan verilerin bakımı olduğu anlamına gelir...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 0e91842c-7f10-4aed-8c23-4ee3e2774014
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
msc.type: authoredcontent
ms.openlocfilehash: 5bc27a08e39606c25b8f99d6ea057d2a853f08a6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611924"
---
# <a name="using-sql-cache-dependencies-c"></a>SQL Önbellek Bağımlılıklarını Kullanma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_CS.zip) veya [PDF 'yi indirin](using-sql-cache-dependencies-cs/_static/datatutorial61cs1.pdf)

> En basit önbelleğe alma stratejisi, önbelleğe alınan verilerin belirli bir süre sonra dolmasına izin verecektir. Ancak bu basit yaklaşım, önbelleğe alınmış verilerin temel alınan veri kaynağıyla hiçbir ilişki olmadığı anlamına gelir. Bu, çok uzun tutulan eski veriler veya çok yakında zaman aşımına uğradı. Daha iyi bir yaklaşım, SqlCacheDependency sınıfını temel alınan veriler SQL veritabanında değiştirilene kadar önbelleğe kalacak şekilde kullanmaktır. Bu öğreticide nasıl yapılacağı gösterilmektedir.

## <a name="introduction"></a>Giriş

[Mimari](caching-data-in-the-architecture-cs.md) öğreticilerde [önbelleğe alma verilerinde](caching-data-with-the-objectdatasource-cs.md) incelenen önbelleğe alma teknikleri, verileri belirli bir süre geçtikten sonra önbellekten çıkarmak için zamana dayalı bir süre sonu kullandı. Bu yaklaşım, veri açısından önbelleğe almanın performans kazançlarını dengelemek için en kolay yoldur. Bir sayfa geliştiricisi *x* saniyelik zaman aşımı süresini seçerek, yalnızca *x* saniye boyunca önbelleğe alma işleminin performans avantajlarından faydalanmayı gizlemektir, ancak verilerin en fazla *x* saniyeden daha uzun bir süre daha fazla olmadığı kadar kolay bir şekilde kalmaz. Kuşkusuz, statik veriler için *x* , [uygulama başlangıç öğreticisindeki önbelleğe alma verilerinde](caching-data-at-application-startup-cs.md) incelenen gibi Web uygulamasının kullanım ömrüne genişletilebilir.

Veritabanı verilerini önbelleğe alırken, zaman tabanlı süre sonu genellikle kullanım kolaylığı için seçilir, ancak genellikle yetersiz bir çözümdür. İdeal olarak, veritabanı verileri, temel alınan veriler veritabanında değiştirilene kadar önbellekte kalır; yalnızca önbellek çıkarılmalıdır. Bu yaklaşım, önbelleğe almanın performans avantajlarını en üst düzeye çıkarır ve eski verilerin süresini en aza indirir. Bununla birlikte, bu avantajlardan faydalanmak için, temel alınan veritabanı verilerinin ne zaman değiştirildiğini bilen ve ilgili öğeleri önbellekten çıkarmanın bir sistem olması gerekir. ASP.NET 2,0 ' den önce, sayfa geliştiricileri bu sistemi uygulamaktan sorumludur.

ASP.NET 2,0, karşılık gelen önbelleğe alınmış öğelerin çıkarılenebilmesi için veritabanında bir değişikliğin ne zaman gerçekleştiğini belirlemede bir [`SqlCacheDependency` sınıfı](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx) ve gerekli altyapıyı sağlar. Temel alınan verilerin ne zaman değiştiğini belirlemek için iki teknik vardır: bildirim ve yoklama. Bildirim ve yoklama arasındaki farkları tartışdıktan sonra, yoklamayı desteklemek için gereken altyapıyı oluşturacağız ve ardından `SqlCacheDependency` sınıfının bildirime dayalı ve program aracılığıyla senaryolarında nasıl kullanılacağını keşfedeceğiz.

## <a name="understanding-notification-and-polling"></a>Bildirim ve yoklamayı anlama

Bir veritabanındaki verilerin ne zaman değiştirildiğini tespit etmek için kullanılabilecek iki teknik vardır: bildirim ve yoklama. Bildirim ile, sorgu en son çalıştırılmasından bu yana belirli bir sorgunun sonuçları değiştirildiğinde veritabanı otomatik olarak ASP.NET çalışma zamanını uyarır. bu noktada sorguyla ilişkili olan önbelleğe alınan öğeler çıkarılmıştır. Yoklama ile veritabanı sunucusu, belirli tabloların en son ne zaman güncelleştirildiği hakkında bilgileri saklar. ASP.NET çalışma zamanı, önbelleğe girildiklerinden beri hangi tabloların değiştiğini denetlemek için veritabanını düzenli aralıklarla yoklar. Verilerin değiştirildiği tablolarda ilişkili önbellek öğeleri çıkarıldı.

Bildirim seçeneği yoklamaya göre daha az kurulum gerektirir ve tablo düzeyi yerine sorgu düzeyindeki değişiklikleri izlediğinden daha ayrıntılı bir hale gelir. Ne yazık ki, bildirimler yalnızca Microsoft SQL Server 2005 ' in (yani Express olmayan sürümler) tüm sürümlerinde kullanılabilir. Ancak yoklama seçeneği 7,0 ' dan 2005 ' e kadar tüm Microsoft SQL Server sürümleri için kullanılabilir. Bu öğreticiler SQL Server 2005 ' nin Express sürümünü kullandığından yoklama seçeneğini ayarlamaya ve kullanmaya odaklanacağız. SQL Server 2005 s bildirim özellikleri hakkında daha fazla kaynak için Bu öğreticinin sonundaki daha fazla okuma bölümüne bakın.

Yoklamayla veritabanı, üç sütun içeren `AspNet_SqlCacheTablesForChangeNotification` adlı bir tablo (`tableName`, `notificationCreated`ve `changeId`) içerecek şekilde yapılandırılmalıdır. Bu tablo, Web uygulamasında bir SQL önbellek bağımlılığında kullanılması gerekebilecek verilerin bulunduğu her tablo için bir satır içerir. `tableName` sütunu, tablonun tabloya eklendiği tarihi ve saati gösteren `notificationCreated` tablodaki adı belirtir. `changeId` sütunu `int` türündedir ve ilk değeri 0 ' dır. Değeri, tablodaki her değişiklikle artırılır.

`AspNet_SqlCacheTablesForChangeNotification` tablosuna ek olarak, veritabanının SQL önbellek bağımlılığında görünebilen her bir tabloya tetikleyici eklemesi de gerekir. Bu Tetikleyiciler, bir satır eklendiğinde, güncelleştirildiğinde veya silindiğinde ve `AspNet_SqlCacheTablesForChangeNotification`içindeki tablo `changeId` değerini artırırsanız yürütülür.

ASP.NET çalışma zamanı, verileri bir `SqlCacheDependency` nesnesi kullanarak önbelleğe alırken tablo için geçerli `changeId` izler. Veritabanı düzenli aralıklarla denetlenir ve farklı bir `changeId` değeri, verilerin önbelleğe alındığı bu yana tabloda bir değişiklik olduğunu gösterdiği için, `changeId` veritabanındaki değerden farklı olan `SqlCacheDependency` nesneleri çıkarıldı.

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>1\. adım: `aspnet_regsql.exe`komut satırı programını keşfetme

Yoklama yaklaşımıyla, veritabanının yukarıda açıklanan altyapıyı içerecek şekilde kurulması gerekir: önceden tanımlanmış bir tablo (`AspNet_SqlCacheTablesForChangeNotification`), bir dizi saklı yordam ve Web uygulamasındaki SQL önbellek bağımlılıklarında kullanılabilecek her tablo üzerinde Tetikleyiciler. Bu tablolar, saklı yordamlar ve Tetikleyiciler, `$WINDOWS$\Microsoft.NET\Framework\version` klasöründe bulunan `aspnet_regsql.exe`komut satırı programı aracılığıyla oluşturulabilir. `AspNet_SqlCacheTablesForChangeNotification` tablosu ve ilişkili saklı yordamları oluşturmak için komut satırından aşağıdakileri çalıştırın:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample1.cmd)]

> [!NOTE]
> Bu komutları yürütmek için belirtilen veritabanı oturum açma [`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx) ve [`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx) rollerde olmalıdır. Veritabanına gönderilen T-SQL ' i `aspnet_regsql.exe` komut satırı programı tarafından incelemek için, [Bu Blog girdisine](http://scottonwriting.net/sowblog/posts/10709.aspx)bakın.

Örneğin, Windows kimlik doğrulaması kullanarak `ScottsServer` adlı bir veritabanı sunucusunda `pubs` adlı bir Microsoft SQL Server veritabanına yoklamaya yönelik altyapıyı eklemek için, uygun dizine gidin ve komut satırından, şunu girin:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample2.cmd)]

Veritabanı düzeyi altyapısı eklendikten sonra, Tetikleyicileri SQL önbellek bağımlılıklarında kullanılacak olan tablolara eklememiz gerekir. `aspnet_regsql.exe` komut satırı programını yeniden kullanın, ancak `-t` anahtarını kullanarak tablo adını belirtin ve `-et`kullanın `-ed` anahtarını kullanmak yerine, şöyle olması gerekir:

[!code-html[Main](using-sql-cache-dependencies-cs/samples/sample3.html)]

Tetikleyicileri `authors` ve `ScottsServer``pubs` veritabanındaki `titles` tablolarına eklemek için şunu kullanın:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample4.cmd)]

Bu öğretici için Tetikleyicileri `Products`, `Categories`ve `Suppliers` tablolarına ekleyin. Adım 3 ' te belirli komut satırı sözdizimine bakacağız.

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>2\. adım: `App_Data` Microsoft SQL Server 2005 Express Edition veritabanına başvurma

`aspnet_regsql.exe` komut satırı programı, gerekli yoklama altyapısını eklemek için veritabanı ve sunucu adını gerektirir. Ancak `App_Data` klasöründe bulunan Microsoft SQL Server 2005 Express veritabanı için veritabanı ve sunucu adı nedir? Veritabanı ve sunucu adlarının ne olduğunu keşfetmesi yerine, en basit yaklaşımın veritabanını `localhost\SQLExpress` veritabanı örneğine eklemek ve [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)kullanarak verileri yeniden adlandırmak için olduğunu buldum. Makinenizde yüklü olan SQL Server 2005 ' nin tam sürümlerinden birine sahipseniz, büyük olasılıkla bilgisayarınızda zaten SQL Server Management Studio yüklü olmalıdır. Yalnızca Express Edition kullanıyorsanız, ücretsiz [Microsoft SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)'ı indirebilirsiniz.

Visual Studio 'Yu kapatarak başlayın. Sonra, SQL Server Management Studio açın ve Windows kimlik doğrulaması kullanarak `localhost\SQLExpress` sunucusuna bağlanmayı seçin.

![Localhost\SQLExpress sunucusuna Ekle](using-sql-cache-dependencies-cs/_static/image1.gif)

**Şekil 1**: `localhost\SQLExpress` sunucusuna iliştirme

Sunucuya bağlandıktan sonra, Management Studio sunucuyu gösterir ve veritabanları, güvenlik ve diğerleri için alt klasörlere sahip olur. Veritabanları klasörüne sağ tıklayın ve Ekle seçeneğini belirleyin. Bu işlem veritabanlarını Ekle iletişim kutusunu getirir (bkz. Şekil 2). Ekle düğmesine tıklayın ve Web uygulamanızın `App_Data` klasörünüzdeki `NORTHWND.MDF` veritabanı klasörünü seçin.

[![kuzeydoğu ekleyin. App_Data klasöründen MDF veritabanı](using-sql-cache-dependencies-cs/_static/image2.gif)](using-sql-cache-dependencies-cs/_static/image1.png)

**Şekil 2**: `App_Data` klasöründen `NORTHWND.MDF` veritabanını iliştirin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image2.png))

Bu, veritabanını veritabanları klasörüne ekler. Veritabanı adı, veritabanı dosyasının tam yolu olabilir veya tam yol bir [GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)ile sona erer. ASPNET\_regsql. exe komut satırı aracını kullanırken bu uzun veritabanı adını yazmak zorunda kalmamak için, yeni eklenen veritabanına sağ tıklayıp Yeniden Adlandır ' ı seçerek veritabanını daha fazla insan dostu bir adla yeniden adlandırın. Veritabanımı Dataöğreticiler olarak yeniden adlandırdım.

![Eklenmiş veritabanını daha kolay bir adla yeniden adlandırın](using-sql-cache-dependencies-cs/_static/image3.gif)

**Şekil 3**: Eklenmiş veritabanını daha kolay bir adla yeniden adlandırın

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>3\. adım: Bir veri tabanı, Northwind veritabanına yoklama altyapısı ekleniyor

Artık `NORTHWND.MDF` veritabanını `App_Data` klasöründen eklediğimiz için, yoklama altyapısını eklemeye hazırız. Veritabanını Dataöğreticileri olarak yeniden adlandırdığınız varsayılarak, aşağıdaki dört komutu çalıştırın:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample5.cmd)]

Bu dört komutu çalıştırdıktan sonra, Management Studio veritabanı adına sağ tıklayın, görevler alt menüsüne gidin ve ayır ' ı seçin. Sonra Management Studio kapatın ve Visual Studio 'Yu yeniden açın.

Visual Studio yeniden açıldıktan sonra, Sunucu Gezgini aracılığıyla veritabanına detaya gidin. Yeni tabloya (`AspNet_SqlCacheTablesForChangeNotification`), yeni saklı yordamlara ve `Products`, `Categories`ve `Suppliers` tablolarına yönelik tetikleyicilere göz önünde bulunmaktadır.

![Veritabanı artık gerekli yoklama altyapısını Içerir](using-sql-cache-dependencies-cs/_static/image4.gif)

**Şekil 4**: Veritabanı artık gerekli yoklama altyapısını Içerir

## <a name="step-4-configuring-the-polling-service"></a>4\. Adım: Yoklama hizmetini yapılandırma

Veritabanında gerekli tabloları, Tetikleyicileri ve saklı yordamları oluşturduktan sonra, son adım, kullanılacak veritabanlarını ve yoklama sıklığını milisaniye olarak belirterek `Web.config` aracılığıyla gerçekleştirilen yoklama hizmetini yapılandırmaktır. Aşağıdaki biçimlendirme, her saniye bir kez Northwind veritabanını yoklar.

[!code-xml[Main](using-sql-cache-dependencies-cs/samples/sample6.xml)]

`<add>` öğesindeki (NorthwindDB) `name` değeri, okunabilir bir adı belirli bir veritabanıyla ilişkilendirir. SQL önbellek bağımlılıklarıyla çalışırken, burada tanımlanan veritabanı adına ve önbelleğe alınan verilerin dayandığı tabloya başvurmaları gerekir. Adım 6 ' da SQL önbellek bağımlılıklarını önbelleğe alınmış verilerle programlı bir şekilde ilişkilendirmek için `SqlCacheDependency` sınıfını nasıl kullanacağınızı inceleyeceğiz.

SQL önbellek bağımlılığı kurulduktan sonra, yoklama sistemi her `pollTime` milisaniyede `<databases>` öğelerinde tanımlanan veritabanlarına bağlanır ve `AspNet_SqlCachePollingStoredProcedure` saklı yordamını yürütür. `aspnet_regsql.exe` komut satırı aracını kullanarak adım 3 ' te geri eklenen bu saklı yordam, `AspNet_SqlCacheTablesForChangeNotification`içindeki her kayıt için `tableName` ve `changeId` değerlerini döndürür. Güncel olmayan SQL önbelleği bağımlılıkları önbellekten çıkarıldı.

`pollTime` ayarı, performans ve veri kullanımı arasında bir zorunluluğunu getirir tanıtır. Küçük bir `pollTime` değeri veritabanına yönelik istek sayısını artırır, ancak eski verileri önbellekten daha hızlı bir şekilde çıkarır. Daha büyük bir `pollTime` değeri, veritabanı isteklerinin sayısını azaltır, ancak arka uç verilerinin ne zaman değiştiği ve ilgili önbellek öğelerinin ne zaman çıkarıldığı arasındaki gecikmeyi artırır. Neyse ki veritabanı isteği basit ve hafif bir tablodan yalnızca birkaç satır döndüren basit bir saklı yordam yürütüyor. Ancak, veritabanı erişimi ile uygulamanızın veri kullanımı arasında ideal bir denge bulmak için farklı `pollTime` değerleri ile denemeler yapın. İzin verilen en küçük `pollTime` değeri 500 ' dir.

> [!NOTE]
> Yukarıdaki örnek, `<sqlCacheDependency>` öğesinde tek bir `pollTime` değeri sağlar, ancak isteğe bağlı olarak `<add>` öğesinde `pollTime` değeri belirtebilirsiniz. Bu, birden çok veritabanınız varsa ve veritabanı başına yoklama sıklığını özelleştirmek istiyorsanız yararlıdır.

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>5\. Adım: SQL önbellek bağımlılıklarıyla bildirimli olarak çalışma

1 ile 4 arasındaki adımlarda, gerekli veritabanı altyapısını ayarlama ve yoklama sistemini yapılandırma hakkında baktık. Bu altyapıda, artık programlı veya bildirime dayalı teknikler kullanarak ilişkili bir SQL önbellek bağımlılığı ile veri önbelleğine öğe ekleyebiliriz. Bu adımda, SQL önbellek bağımlılıklarıyla bildirimli olarak nasıl çalışacağımız anlatılmaktadır. Adım 6 ' da programlama yaklaşımına bakacağız.

[ObjectDataSource Ile önbelleğe alma verileri](caching-data-with-the-objectdatasource-cs.md) , ObjectDataSource 'un bildirime dayalı önbelleğe alma yeteneklerini araştırın. Yalnızca `EnableCaching` özelliğini `true` ve `CacheDuration` özelliğini bir zaman aralığına ayarlayarak, ObjectDataSource, belirtilen Aralık için temel alınan nesnesinden döndürülen verileri otomatik olarak önbelleğe alınır. ObjectDataSource bir veya daha fazla SQL önbellek bağımlılığı da kullanabilir.

SQL önbellek bağımlılıklarını bildirimli olarak kullanmayı göstermek için, `Caching` klasöründeki `SqlCacheDependencies.aspx` sayfasını açın ve araç kutusundan bir GridView 'u tasarımcı üzerine sürükleyin. GridView s `ID` `ProductsDeclarative` ve akıllı etiketinden `ProductsDataSourceDeclarative`adlı yeni bir ObjectDataSource 'a bağlamayı seçin.

[![Productsdatasourcebildirime adlı yeni bir ObjectDataSource oluşturun](using-sql-cache-dependencies-cs/_static/image5.gif)](using-sql-cache-dependencies-cs/_static/image3.png)

**Şekil 5**: `ProductsDataSourceDeclarative` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image4.png))

ObjectDataSource 'ı `ProductsBLL` sınıfını kullanacak şekilde yapılandırın ve SEÇIM sekmesindeki açılan listeyi `GetProducts()`olarak ayarlayın. GÜNCELLEŞTIRME sekmesinde, üç giriş parametresiyle `UpdateProduct` aşırı yüklemeyi seçin-`productName`, `unitPrice`ve `productID`. Ekle ve SIL sekmelerinde açılan listeleri (yok) olarak ayarlayın.

[![UpdateProduct Overload ' i üç giriş parametresiyle kullanın](using-sql-cache-dependencies-cs/_static/image6.gif)](using-sql-cache-dependencies-cs/_static/image5.png)

**Şekil 6**: Üç giriş parametresiyle UpdateProduct Overload kullanın ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image6.png))

[INSERT ve DELETE sekmeleri için açılan listeyi (yok) olarak ayarlamak ![](using-sql-cache-dependencies-cs/_static/image7.gif)](using-sql-cache-dependencies-cs/_static/image7.png)

**Şekil 7**: EKLEME ve SILME sekmeleri için açılan listeyi (yok) olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image8.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra Visual Studio, veri alanlarının her biri için GridView 'da BoundFields ve CheckBoxFields oluşturur. Tüm alanları kaldırın, `ProductName`, `CategoryName`ve `UnitPrice`ve bu alanları uygun gördüğünüz şekilde biçimlendirin. GridView s akıllı etiketinde, Sayfalamayı Etkinleştir, sıralamayı etkinleştir ve Düzenle onay kutularını etkinleştir ' i işaretleyin. Visual Studio, ObjectDataSource 'un `OldValuesParameterFormatString` özelliğini `original_{0}`olarak ayarlar. GridView s düzenleme özelliğinin düzgün çalışması için, bu özelliği tamamen bildirime dayalı sözdiziminden kaldırın veya `{0}`varsayılan değerine geri ayarlayın.

Son olarak, GridView üzerine bir etiket Web denetimi ekleyin ve `ID` özelliğini `ODSEvents` ve `EnableViewState` özelliğini `false`olarak ayarlayın. Bu değişiklikleri yaptıktan sonra, sayfanın bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir. SQL önbellek bağımlılığı işlevini göstermek için gerekli olmayan GridView alanlarında çok sayıda Aesthetic Characteristics özelleştirmesi yaptık.

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample7.aspx)]

Ardından, ObjectDataSource s `Selecting` olayı için bir olay işleyicisi oluşturun ve bu kodu aşağıdaki kodu ekleyin:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample8.cs)]

ObjectDataSource 'un `Selecting` olayının yalnızca temel alınan nesnesinden veri alırken harekete geçirilir. ObjectDataSource, verilere kendi önbelleğinden eriştiğinde bu olay tetiklenmez.

Şimdi bu sayfayı bir tarayıcı aracılığıyla ziyaret edin. Henüz herhangi bir önbelleğe alma işlemi gerçekleştirdiğimiz için, kılavuza her sayfa, sıralama veya düzenleme yaparken sayfada, Şekil 8 ' de gösterildiği gibi, olay tetiklenen metni görüntülemesi gerekir.

[GridView her Sayfalanışında, düzenlendiğinde veya sıralandığında her bir olay seçen ObjectDataSource ![](using-sql-cache-dependencies-cs/_static/image8.gif)](using-sql-cache-dependencies-cs/_static/image9.png)

**Şekil 8**: `Selecting` ObjectDataSource, GridView her Sayfalanışında, düzenlendiğinde veya sıralandığında başlatılır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image10.png))

[ObjectDataSource Ile verileri önbelleğe alma](caching-data-with-the-objectdatasource-cs.md) bölümünde gördüğünüz gibi, `EnableCaching` özelliğinin `true` olarak ayarlanması, ObjectDataSource 'un verilerini `CacheDuration` özelliği tarafından belirtilen süre için önbelleğe almasına neden olur. ObjectDataSource Ayrıca, bir veya daha fazla SQL önbellek bağımlılıklarını, bu model kullanılarak önbelleğe alınmış verilere ekleyen bir [`SqlCacheDependency` özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)sahiptir:

[!code-css[Main](using-sql-cache-dependencies-cs/samples/sample9.css)]

Burada *DatabaseName* , `Web.config``<add>` öğesinin `name` özniteliğinde belirtilen şekilde veritabanının adıdır ve *TableName* veritabanı tablosunun adıdır. Örneğin, Northwind s `Products` tablosuna karşı bir SQL önbellek bağımlılığını temel alarak verileri süresiz olarak önbelleğe alan bir ObjectDataSource oluşturmak için, ObjectDataSource s `EnableCaching` özelliğini `true` ve `SqlCacheDependency` özelliği NorthwindDB: Products olarak ayarlayın.

> [!NOTE]
> `EnableCaching` `true`ayarlayarak bir SQL önbellek bağımlılığı *ve* zaman tabanlı süre sonu kullanabilirsiniz, zaman aralığına `CacheDuration` ve veritabanı ve tablo adına `SqlCacheDependency`. Zaman tabanlı süre sonuna ulaşıldığında veya yoklama sistemi temeldeki veritabanı verilerinin değiştiğini, hangisi önce gerçekleştiğine bağlı olarak, ObjectDataSource bu verileri çıkarır.

`SqlCacheDependencies.aspx` GridView, iki tablodaki verileri görüntüler-`Products` ve `Categories` (ürün s `CategoryName` alanı `JOIN` `Categories`bir aracılığıyla alınır). Bu nedenle, iki SQL önbellek bağımlılığı belirtmek istiyoruz: NorthwindDB: Ürünler; NorthwindDB: Kategoriler.

[![, ürün ve kategorilerdeki SQL önbellek bağımlılıklarını kullanarak önbelleğe almayı destekleyecek şekilde yapılandırın](using-sql-cache-dependencies-cs/_static/image9.gif)](using-sql-cache-dependencies-cs/_static/image11.png)

**Şekil 9**: `Products` ve `Categories` SQL önbellek bağımlılıklarını kullanarak önbelleğe almayı desteklemek için ObjectDataSource 'u yapılandırın ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image12.png))

Önbelleğe almayı desteklemek için ObjectDataSource 'u yapılandırdıktan sonra, sayfayı bir tarayıcı aracılığıyla geri ziyaret edin. Yine, tetiklenen olayı seçen metin ilk sayfada görünmelidir, ancak sayfalama, sıralama veya Düzenle ya da Iptal düğmelerine tıklarken dışarıda olmalıdır. Bunun nedeni, veriler ObjectDataSource s önbelleğine yüklendikten sonra `Products` veya `Categories` tabloları değiştirilene veya veriler GridView aracılığıyla güncelleştirilene kadar orada kalır.

Kılavuz aracılığıyla hata ettikten ve olay harekete geçirilen metnin eksik olduğunu belirterek, yeni bir tarayıcı penceresi açın ve Düzenle, ekleme ve silme bölümündeki temel bilgiler öğreticisine gidin (`~/EditInsertDelete/Basics.aspx`). Bir ürünün adını veya fiyatını güncelleştirin. Ardından, ilk tarayıcı penceresine, farklı bir veri sayfası görüntüleyin, Kılavuzu sıralayın veya bir satır s Düzenle düğmesine tıklayın. Bu kez, temel alınan veritabanı verileri değiştirildiğinden harekete geçirilen olayın yeniden oluşturulması gerekir (bkz. Şekil 10). Metin görünmezse, birkaç dakika bekleyip yeniden deneyin. Yoklama hizmetinin her `pollTime` milisaniyede `Products` tablodaki değişiklikleri denetleyeceğini unutmayın. bu nedenle, temeldeki verilerin ne zaman güncelleştirildiği ve önbelleğe alınmış verilerin çıkarılma arasında bir gecikme vardır.

[Ürün tablosunu değiştirme ![önbelleğe alınmış ürün verilerini çıkarma](using-sql-cache-dependencies-cs/_static/image10.gif)](using-sql-cache-dependencies-cs/_static/image13.png)

**Şekil 10**: Ürün tablosunu değiştirme, önbelleğe alınmış ürün verilerini Çıkarşır ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image14.png))

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>6\. Adım: Program aracılığıyla`SqlCacheDependency`sınıfıyla çalışma

Mimari öğreticisindeki [önbelleğe alma verileri](caching-data-in-the-architecture-cs.md) ,, ObjectDataSource ile ön belleğe sıkı bir şekilde eşlenmesinin aksine, mimaride ayrı bir önbelleğe alma katmanı kullanmanın avantajlarından bakıyordu. Bu öğreticide, veri önbelleğiyle programlı bir şekilde çalıştığını göstermek için bir `ProductsCL` sınıfı oluşturduk. Önbelleğe alma katmanında SQL önbellek bağımlılıklarını kullanmak için `SqlCacheDependency` sınıfını kullanın.

Yoklama sistemiyle, bir `SqlCacheDependency` nesnesinin belirli bir veritabanı ve tablo çifti ile ilişkilendirilmesi gerekir. Aşağıdaki kod Örneğin, Northwind veritabanı s `Products` tablosuna göre bir `SqlCacheDependency` nesnesi oluşturur:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample10.cs)]

`SqlCacheDependency` s oluşturucusuna yönelik iki giriş parametresi sırasıyla veritabanı ve tablo adlarıdır. ObjectDataSource s `SqlCacheDependency` özelliğinde olduğu gibi, kullanılan veritabanı adı `Web.config``<add>` öğesinin `name` özniteliğinde belirtilen değerle aynıdır. Tablo adı, veritabanı tablosunun gerçek adıdır.

Bir `SqlCacheDependency` veri önbelleğine eklenen bir öğeyle ilişkilendirmek için, bağımlılığı kabul eden `Insert` yöntemi aşırı yüklemelerinin birini kullanın. Aşağıdaki kod, sınırsız bir süre için veri önbelleğine *değer* ekler, ancak bunu `Products` tablosundaki bir `SqlCacheDependency` ilişkilendirir. Kısacası, bellek kısıtlamaları nedeniyle veya yoklama sistemi `Products` tablosunun önbelleğe alındığı zamandan sonra değiştiğini algıladığı için *değer* önbellekte kalır.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample11.cs)]

Önbelleğe alma katmanı s `ProductsCL` sınıfı şu anda `Products` tablodaki verileri 60 saniyelik zaman tabanlı süre sonu ile önbelleğe alır. Bunun yerine SQL önbellek bağımlılıklarını kullanması için bu sınıfı güncelleştirmesine izin verin. Verileri önbelleğe eklemekten sorumlu olan `ProductsCL` sınıf s `AddCacheItem` yöntemi şu anda aşağıdaki kodu içerir:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample12.cs)]

Bu kodu `MasterCacheKeyArray` önbellek bağımlılığı yerine `SqlCacheDependency` nesnesini kullanacak şekilde güncelleştirin:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample13.cs)]

Bu işlevi test etmek için, var `ProductsDeclarative` olan GridView 'un altındaki sayfaya bir GridView ekleyin. Bu yeni GridView s `ID` `ProductsProgrammatic` ve akıllı etiketi aracılığıyla `ProductsDataSourceProgrammatic`adlı yeni bir ObjectDataSource 'a bağlayın. `ProductsCL` sınıfını kullanacak şekilde, seçme ve GÜNCELLEŞTIRME sekmelerindeki açılan listeleri sırasıyla `GetProducts` ve `UpdateProduct`olarak ayarlamak üzere yapılandırın.

[![, ObjectDataSource 'ı ProductsCL sınıfını kullanacak şekilde yapılandırma](using-sql-cache-dependencies-cs/_static/image11.gif)](using-sql-cache-dependencies-cs/_static/image15.png)

**Şekil 11**: ObjectDataSource 'ı `ProductsCL` sınıfını kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image16.png))

[![sekme seç açılan listesinden GetProducts yöntemini seçin](using-sql-cache-dependencies-cs/_static/image12.gif)](using-sql-cache-dependencies-cs/_static/image17.png)

**Şekil 12**: Sekme seç açılan listesinden `GetProducts` yöntemini seçin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image18.png))

[![GÜNCELLEŞTIRME sekmesi açılan listesinden UpdateProduct yöntemini seçin](using-sql-cache-dependencies-cs/_static/image13.gif)](using-sql-cache-dependencies-cs/_static/image19.png)

**Şekil 13**: GÜNCELLEŞTIRME sekmesi açılan listesinden UpdateProduct yöntemini seçin ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-cs/_static/image20.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra Visual Studio, veri alanlarının her biri için GridView 'da BoundFields ve CheckBoxFields oluşturur. Bu sayfaya eklenen ilk GridView gibi, tüm alanları kaldırın, ancak `ProductName`, `CategoryName`ve `UnitPrice`ve bu alanları uygun gördüğünüz şekilde biçimlendirin. GridView s akıllı etiketinde, Sayfalamayı Etkinleştir, sıralamayı etkinleştir ve Düzenle onay kutularını etkinleştir ' i işaretleyin. `ProductsDataSourceDeclarative` ObjectDataSource ile birlikte, Visual Studio `ProductsDataSourceProgrammatic` ObjectDataSource s `OldValuesParameterFormatString` özelliğini de `original_{0}`olarak ayarlar. GridView s düzenleme özelliğinin düzgün çalışması için, bu özelliği `{0}` geri ayarlayın (veya özellik atamasını bildirime dayalı sözdiziminden tamamen kaldırın).

Bu görevleri tamamladıktan sonra elde edilen GridView ve ObjectDataSource bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample14.aspx)]

Önbelleğe alma katmanında SQL önbellek bağımlılığını test etmek için `ProductCL` Class s `AddCacheItem` yönteminde bir kesme noktası ayarlayın ve ardından hata ayıklamayı başlatın. `SqlCacheDependencies.aspx`ilk kez ziyaret ettiğinizde, verilerin ilk kez istenir ve önbelleğe yerleştirilmesi için kesme noktası isabet etmelidir. Sonra, GridView 'da bir başka sayfaya geçin veya sütunlardan birini sıralayın. Bu, GridView 'un verilerini yeniden kaydetmesine neden olur, ancak `Products` veritabanı tablosu değiştirilmediğinden verilerin önbellekte bulunması gerekir. Veriler önbellekte tekrar tekrarlanmadığından bilgisayarınızda yeterli kullanılabilir bellek olduğundan emin olun ve yeniden deneyin.

GridView 'un birkaç sayfasında sayfaladıktan sonra ikinci bir tarayıcı penceresi açın ve Düzenle, ekleme ve silme bölümündeki temel bilgiler öğreticisine gidin (`~/EditInsertDelete/Basics.aspx`). Products tablosundan bir kaydı güncelleştirin ve ardından ilk tarayıcı penceresinden yeni bir sayfa görüntüleyin veya sıralama başlıklarından birine tıklayın.

Bu senaryoda, iki seçenekten birini göreceksiniz: kesme noktası isabet edecek ve bu, önbellekteki verilerin veritabanındaki değişiklik nedeniyle çıkarıldığını belirtir; ya da, kesme noktası isabet etmez, yani `SqlCacheDependencies.aspx` artık eski verileri gösterir. Kesme noktası isabet ettirilmemişse, büyük olasılıkla yoklama hizmeti, verilerin değiştiği bu yana başlatılmamıştır. Yoklama hizmetinin her `pollTime` milisaniyede `Products` tablodaki değişiklikleri denetleyeceğini unutmayın. bu nedenle, temeldeki verilerin ne zaman güncelleştirildiği ve önbelleğe alınmış verilerin çıkarılma arasında bir gecikme vardır.

> [!NOTE]
> Bu gecikmenin, `SqlCacheDependencies.aspx`' deki GridView aracılığıyla ürünlerden birini düzenlediğinizde görünmesi daha olasıdır. Mimari öğreticideki [önbelleğe alma verilerinde](caching-data-in-the-architecture-cs.md) , `ProductsCL` sınıf s `UpdateProduct` yöntemi aracılığıyla düzenlenmekte olan verilerin önbellekten çıkarılmakta olduğundan emin olmak için `MasterCacheKeyArray` önbellek bağımlılığını ekledik. Ancak, bu adımda daha önce `AddCacheItem` yöntemi değiştirirken bu önbellek bağımlılığını değiştirdik ve bu nedenle, yoklama sistemi `Products` tabloya değişikliği yükleyene kadar `ProductsCL` sınıfı önbelleğe alınmış verileri göstermeye devam edecektir. Adım 7 ' de `MasterCacheKeyArray` önbelleği bağımlılığını nasıl yeniden tanıtabileceksiniz.

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>7\. Adım: Birden çok bağımlılığı önbelleğe alınmış bir öğeyle ilişkilendirme

`MasterCacheKeyArray` önbellek bağımlılığının, onunla ilişkilendirilen tek bir öğe güncelleştirildiği sırada *Tüm* ürünle ilgili verilerin önbellekten çıkarıldığından emin olmak için kullanıldığını unutmayın. Örneğin, `GetProductsByCategoryID(categoryID)` yöntemi her benzersiz *CategoryID* değeri için `ProductsDataTables` örnekleri önbelleğe alır. Bu nesnelerden biri çıkarılmışsa, `MasterCacheKeyArray` önbellek bağımlılığı diğerlerinin de kaldırılmasını sağlar. Bu önbellek bağımlılığı olmadan, önbelleğe alınmış veriler değiştirildiğinde, diğer önbelleğe alınmış ürün verilerinin eski olma olasılığı vardır. Sonuç olarak, SQL önbellek bağımlılıklarını kullanırken `MasterCacheKeyArray` önbelleği bağımlılığını koruduğumuz önemli öneme sahiptir. Ancak, veri önbelleği s `Insert` yöntemi yalnızca tek bir bağımlılık nesnesine izin verir.

Ayrıca, SQL önbellek bağımlılıklarıyla çalışırken birden çok veritabanı tablosunu bağımlılıklar olarak ilişkilendirmemiz gerekebilir. Örneğin, `ProductsCL` sınıfında önbelleğe alınan `ProductsDataTable` her ürün için kategori ve Tedarikçi adlarını içerir, ancak `AddCacheItem` yöntemi yalnızca `Products`bir bağımlılık kullanır. Bu durumda, Kullanıcı bir kategorinin veya tedarikçinin adını Güncelleştir, önbelleğe alınmış ürün verileri önbellekte kalır ve güncel olmayacaktır. Bu nedenle, önbelleğe alınmış ürün verilerinin yalnızca `Products` tablosuna değil, `Categories` ve `Suppliers` tablolarında de bağlı olmasını istiyoruz.

[`AggregateCacheDependency` sınıfı](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx) , birden çok bağımlılığı bir önbellek öğesiyle ilişkilendirmek için bir yol sağlar. `AggregateCacheDependency` bir örnek oluşturarak başlayın. Sonra, `AggregateCacheDependency` s `Add` yöntemini kullanarak bağımlılıklar kümesini ekleyin. Öğesi bundan sonra veri önbelleğine eklenirken `AggregateCacheDependency` örneğini geçirin. `AggregateCacheDependency` örnek bağımlılarından *herhangi* biri değiştiğinde, önbelleğe alınmış öğe kaldırılır.

Aşağıda `ProductsCL` sınıf s `AddCacheItem` yönteminin güncelleştirilmiş kodu gösterilmektedir. Yöntemi `Products`, `Categories`ve `Suppliers` tabloları için `SqlCacheDependency` nesnelerle birlikte `MasterCacheKeyArray` önbellek bağımlılığı oluşturur. Bunlar, daha sonra `Insert` yöntemine geçirilen `aggregateDependencies`adlı bir `AggregateCacheDependency` nesnesi içinde birleştirilir.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample15.cs)]

Bu yeni kodu test edin. Artık `Products`, `Categories`veya `Suppliers` tablolarında yapılan değişiklikler önbelleğe alınmış verilerin çıkarılmasına neden olur. Üstelik, GridView aracılığıyla bir ürün düzenlenirken çağrılan `MasterCacheKeyArray` önbellek bağımlılığını çıkarmakta olan `ProductsCL` Class s `UpdateProduct` yöntemi, önbelleğe alınan `ProductsDataTable` çıkarılmasına ve verilerin bir sonraki istekte yeniden alınmasına neden olur.

> [!NOTE]
> SQL önbellek bağımlılıkları, [çıktı önbelleği](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)ile de kullanılabilir. Bu işlevselliğin bir gösterimi için bkz.: [SQL Server ile ASP.net çıktı önbelleği kullanma](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx).

## <a name="summary"></a>Özet

Veritabanı verilerini önbelleğe alırken, veriler veritabanında değiştirilene kadar önbellekte kalır. ASP.NET 2,0 ile SQL önbellek bağımlılıkları hem bildirim temelli hem de programlı senaryolarda oluşturulabilir ve kullanılabilir. Bu yaklaşımla ilgili güçlüklerden biri, verilerin değiştirildiği zaman keşfederdir. Microsoft SQL Server 2005 ' nin tam sürümleri, bir sorgu sonucu değiştiğinde bir uygulamayı uyarabilecek bildirim özellikleri sağlar. SQL Server 2005 ' nin Express sürümü ve SQL Server daha eski sürümleri için bunun yerine bir yoklama sisteminin kullanılması gerekir. Neyse ki, gerekli yoklama altyapısını ayarlama oldukça basittir.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Microsoft SQL Server 2005 ' de sorgu bildirimlerini kullanma](https://msdn.microsoft.com/library/ms175110.aspx)
- [Sorgu bildirimi oluşturma](https://msdn.microsoft.com/library/ms188669.aspx)
- [`SqlCacheDependency` sınıfıyla ASP.NET içinde önbelleğe alma](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server kayıt aracı (`aspnet_regsql.exe`)](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [`SqlCacheDependency` genel bakış](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Marko Rangel, Teresa Murphy ve Tepton Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](caching-data-at-application-startup-cs.md)
> [İleri](caching-data-with-the-objectdatasource-vb.md)
