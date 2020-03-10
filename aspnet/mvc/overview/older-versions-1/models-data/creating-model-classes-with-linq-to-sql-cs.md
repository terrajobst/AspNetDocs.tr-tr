---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: LINQ to SQL ile model sınıfları oluşturma (C#) | Microsoft Docs
author: microsoft
description: Bu öğreticinin amacı, bir ASP.NET MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu öğreticide, model c 'yi derlemeyi öğreneceksiniz...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: c27d1ffac3846fe4bc13b32c2ae91a63b2493126
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543542"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>LINQ to SQL ile Model Sınıfları Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> Bu öğreticinin amacı, bir ASP.NET MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu öğreticide, Microsoft LINQ to SQL avantajlarından yararlanarak model sınıfları oluşturmayı ve veritabanı erişimi yapmayı öğreneceksiniz.

Bu öğreticinin amacı, bir ASP.NET MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu öğreticide, Microsoft LINQ to SQL avantajlarından yararlanarak model sınıfları oluşturmayı ve veritabanı erişimini gerçekleştirmeyi öğreneceksiniz

Bu öğreticide, temel bir film veritabanı uygulaması oluşturacağız. Mümkün olan en hızlı ve en kolay şekilde film veritabanı uygulaması oluşturarak başlayacağız. Tüm veri erişimlerimizi doğrudan denetleyici eylemlerimizden gerçekleştirdik.

Daha sonra, depo deseninin nasıl kullanılacağını öğrenirsiniz. Depo deseninin kullanılması biraz daha fazla iş gerektirir. Ancak, bu düzenin benimseme avantajı, değiştirilecek ve kolayca test edebileceğiniz uygulamalar oluşturmanıza olanak sağlar.

## <a name="what-is-a-model-class"></a>Model sınıfı nedir?

MVC modeli, MVC görünümünde veya MVC denetleyicisinde bulunmayan tüm uygulama mantığını içerir. Özellikle bir MVC modeli, tüm uygulama iş ve veri erişim mantığınızı içerir.

Veri erişim mantığınızı uygulamak için çeşitli farklı teknolojiler kullanabilirsiniz. Örneğin, veri erişim sınıflarınızı Microsoft Entity Framework, Nhazırda beklet, Subsonic veya ADO.NET sınıfları kullanarak oluşturabilirsiniz.

Bu öğreticide, veritabanını sorgulamak ve güncelleştirmek için LINQ to SQL kullanıyorum. LINQ to SQL, bir Microsoft SQL Server veritabanıyla etkileşim kurmak için çok kolay bir yöntem sağlar. Ancak, ASP.NET MVC çerçevesinin herhangi bir şekilde LINQ to SQL bağlı olmadığını anlamak önemlidir. ASP.NET MVC, herhangi bir veri erişim teknolojisi ile uyumludur.

## <a name="create-a-movie-database"></a>Film veritabanı oluşturma

Bu öğreticide, model sınıfları nasıl oluşturabileceğiniz hakkında daha fazla anlamak için basit bir film veritabanı uygulaması oluşturacağız. İlk adım yeni bir veritabanı oluşturmaktır. Çözüm Gezgini penceresindeki uygulama\_veri klasörüne sağ tıklayın ve **Ekle, yeni öğe**menü seçeneğini belirleyin. **SQL Server veritabanı** şablonunu seçin, MoviesDB. mdf adını verin ve **Ekle** düğmesine tıklayın (bkz. Şekil 1).

[Yeni bir SQL Server veritabanı ekleme ![](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**Şekil 01**: yeni bir SQL Server veritabanı ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))

Yeni veritabanını oluşturduktan sonra, App\_Data klasöründeki MoviesDB. mdf dosyasını çift tıklayarak veritabanını açabilirsiniz. MoviesDB. mdf dosyasına çift tıklamak Sunucu Gezgini penceresini açar (bkz. Şekil 2).

Sunucu Gezgini penceresine Visual Web Developer kullanılırken Veritabanı Gezgini penceresi denir.

[Sunucu Gezgini penceresini kullanarak ![](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**Şekil 02**: Sunucu Gezgini penceresini kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))

Veritabanımızın filmimizi temsil eden bir tablo eklememiz gerekiyor. Tablolar klasörüne sağ tıklayın ve **Yeni Tablo Ekle**menü seçeneğini belirleyin. Bu menü seçeneği belirlendiğinde Tablo Tasarımcısı açılır (bkz. Şekil 3).

[Sunucu Gezgini penceresini kullanarak ![](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**Şekil 03**: Tablo Tasarımcısı ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))

Veritabanı tablomuza aşağıdaki sütunları eklememiz gerekiyor:

| **Sütun adı** | **Veri türü** | **Null değerlere izin ver** |
| --- | --- | --- |
| Kimlik | int | False |
| Başlık | Nvarchar (200) | False |
| Direktörü | nvarchar (50) | False |

Kimlik sütununda iki özel şey yapmanız gerekir. İlk olarak, Tablo Tasarımcısı sütunu seçip bir anahtarın simgesine tıklayarak ID sütununu birincil anahtar sütunu olarak işaretlemeniz gerekir. LINQ to SQL, veritabanına yönelik ekleme veya güncelleştirme gerçekleştirirken birincil anahtar sütunlarınızı belirtmenizi gerektirir.

Ardından, Evet değerini **,** Identity özelliğine (bkz. Şekil 3) atayarak kimlik sütununu kimlik sütunu olarak işaretlemeniz gerekir. Bir kimlik sütunu, tabloya yeni bir veri satırı eklediğinizde otomatik olarak yeni bir sayı atanan sütundur.

## <a name="create-linq-to-sql-classes"></a>LINQ to SQL sınıfları oluşturma

MVC modelimiz tblMovie veritabanı tablosunu temsil eden LINQ to SQL sınıflar içerir. Bu LINQ to SQL sınıfları oluşturmanın en kolay yolu modeller klasörüne sağ tıklayın, **Ekle, yeni öğe**, LINQ to SQL sınıfları şablonunu seçin, sınıflara film. dbml adını verir ve **Ekle** düğmesine (bkz. Şekil 4) tıklayın.

[LINQ to SQL sınıfları oluşturma ![](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**Şekil 04**: LINQ to SQL sınıfları oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))

Film LINQ to SQL sınıfları oluşturduktan hemen sonra, Nesne İlişkisel Tasarımcısı görünür. Veritabanı tablolarını, belirli veritabanı tablolarını temsil eden LINQ to SQL sınıfları oluşturmak için Sunucu Gezgini penceresinden Nesne İlişkisel Tasarımcısı sürükleyebilirsiniz. TblMovie veritabanı tablosunu Nesne İlişkisel Tasarımcısı eklememiz gerekiyor (bkz. Şekil 5).

[Nesne İlişkisel Tasarımcısı kullanarak ![](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**Şekil 05**: nesne ilişkisel Tasarımcısı kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))

Varsayılan olarak Nesne İlişkisel Tasarımcısı, tasarımcı üzerine sürüklediğiniz veritabanı tablosuyla aynı ada sahip bir sınıf oluşturur. Ancak, `tblMovie`sınıfımızı çağırmak istemiyorum. Bu nedenle, tasarımcıda sınıfın adına tıklayın ve sınıfın adını filmle değiştirin.

Son olarak, LINQ to SQL sınıflarını kaydetmek için **Kaydet** düğmesine (disketin resmi) tıklaması gerektiğini unutmayın. Aksi takdirde LINQ to SQL sınıfları Nesne İlişkisel Tasarımcısı oluşturulmaz.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Bir denetleyici eyleminde LINQ to SQL kullanma

Artık LINQ to SQL sınıflarımız olduğuna göre, veritabanından veri almak için bu sınıfları kullanabiliriz. Bu bölümde, LINQ to SQL sınıflarını doğrudan bir denetleyici eylemi içinde kullanmayı öğreneceksiniz. Bir MVC görünümündeki tblMovies veritabanı tablosundan film listesi görüntüleriz.

İlk olarak, HomeController sınıfını değiştirmemiz gerekiyor. Bu sınıf, uygulamanızın denetleyiciler klasöründe bulunabilir. Sınıfı, liste 1 ' deki sınıfa benzemek üzere değiştirin.

**Listeleme 1 – `Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

Liste 1 ' deki `Index()` eylemi, `MoviesDB` veritabanını temsil etmek için bir LINQ to SQL DataContext Sınıfı (`MovieDataContext`) kullanır. `MoveDataContext` sınıfı, Visual Studio Nesne İlişkisel Tasarımcısı tarafından oluşturulmuştur.

`tblMovies` veritabanı tablosundan tüm filmleri almak için DataContext 'e karşı bir LINQ sorgusu gerçekleştirilir. Film listesi, `movies`adlı bir yerel değişkene atanır. Son olarak, film listesi görünüm verileri aracılığıyla görünüme geçirilir.

Filmleri göstermek için bir sonraki adımda Dizin görünümünü değiştirmemiz gerekiyor. Dizin görünümünü `Views\Home\` klasöründe bulabilirsiniz. Dizin görünümünü, liste 2 ' de görünüm gibi görünecek şekilde güncelleştirin.

**Listeleme 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

Değiştirilen Dizin görünümünün, görünümün en üstünde bir `<%@ import namespace %>` yönergesi içerdiğine dikkat edin. Bu yönerge `MvcApplication1.Models namespace`içeri aktarır. Bu ad alanı, `model` sınıflarla çalışmak için gerekir: özellikle, görünümünde `Movie` sınıfı.

Liste 2 ' deki görünüm, `ViewData.Model` özelliği tarafından temsil edilen tüm öğeler arasında yinelenen bir `foreach` döngüsü içerir. `Title` özelliğinin değeri her `movie`için görüntülenir.

`ViewData.Model` özelliğinin değeri bir `IEnumerable`olarak yayınlandığına dikkat edin. `ViewData.Model`içerikleri arasında döngü uygulamak için bu gereklidir. Burada başka bir seçenek de kesin türü belirtilmiş bir `view`oluşturmaktır. Türü kesin belirlenmiş bir `view`oluşturduğunuzda, `ViewData.Model` özelliğini bir görünümün arka plan kod sınıfında belirli bir türe atamalısınız.

Uygulamayı, `HomeController` sınıfını ve Dizin görünümünü değiştirdikten sonra çalıştırırsanız boş bir sayfa alırsınız. `tblMovies` veritabanı tablosunda hiç film kaydı olmadığından boş bir sayfa alacaksınız.

`tblMovies` veritabanı tablosuna kayıt eklemek için Sunucu Gezgini penceresindeki `tblMovies` veritabanı tablosuna (Visual Web Developer 'da Veritabanı Gezgini penceresi) sağ tıklayın ve tablo verilerini göster menü seçeneğini belirleyin. Görüntülenen Kılavuzu kullanarak `movie` kayıtları ekleyebilirsiniz (bkz. Şekil 6).

[film ekleme ![](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**Şekil 06**: film ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))

`tblMovies` tablosuna bazı veritabanı kayıtları ekledikten ve uygulamayı çalıştırdıktan sonra, sayfayı Şekil 7 ' de görürsünüz. Tüm film veritabanı kayıtları madde işaretli bir listede görüntülenir.

[Dizin görünümüyle film görüntüleme ![](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**Şekil 07**: filmleri Dizin görünümüyle görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))

## <a name="using-the-repository-pattern"></a>Depo deseninin kullanımı

Önceki bölümde, sınıfları doğrudan bir denetleyici eylemi içinde LINQ to SQL kullandık. `MovieDataContext` sınıfını doğrudan `Index()` denetleyicisi eyleminden kullandık. Basit bir uygulama durumunda bunu yaparken bir sorun yoktur. Ancak, bir denetleyici sınıfında LINQ to SQL doğrudan çalışmak, daha karmaşık bir uygulama oluşturmanız gerektiğinde sorunlar oluşturur.

Bir denetleyici sınıfı içinde LINQ to SQL kullanmak, daha sonra veri erişim teknolojilerinin değiştirilmesini zorlaştırır. Örneğin, Microsoft LINQ to SQL kullanarak veri erişim teknolojiniz olarak Microsoft Entity Framework kullanmaya geçiş yapabilirsiniz. Bu durumda, uygulamanızın içindeki veritabanına erişen her denetleyiciyi yeniden yazmanız gerekir.

Bir denetleyici sınıfı içinde LINQ to SQL kullanmak, uygulamanız için birim testlerini oluşturmayı zorlaştırır. Normalde, birim testlerini gerçekleştirirken bir veritabanıyla etkileşime geçmek istemezsiniz. Veritabanı sunucunuzu değil, Uygulama mantığınızı test etmek için birim testlerinizi kullanmak istiyorsunuz.

Daha sonra değişiklik yapılacak ve daha kolay test edebileceğiniz bir MVC uygulaması oluşturmak için depo düzenini kullanmayı göz önünde bulundurmanız gerekir. Depo modelini kullanırken, tüm veritabanı erişim mantığınızı içeren ayrı bir depo sınıfı oluşturursunuz.

Depo sınıfını oluşturduğunuzda, depo sınıfı tarafından kullanılan tüm yöntemleri temsil eden bir arabirim oluşturursunuz. Denetleyicileriniz dahilinde, kodunuzu depo yerine arabirime yazarsınız. Bu şekilde, gelecekte farklı veri erişimi teknolojileri kullanarak depoyu uygulayabilirsiniz.

Listeleme 3 ' teki arabirim `IMovieRepository` olarak adlandırılır ve `ListAll()`adlı tek bir yöntemi temsil eder.

**Listeleme 3 – `Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

Listeleme 4 ' teki depo sınıfı `IMovieRepository` arabirimini uygular. `IMovieRepository` arabirimi için gereken yönteme karşılık gelen `ListAll()` adlı bir yöntem içerdiğine dikkat edin.

**Listeleme 4 – `Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

Son olarak, kod 5 ' teki `MoviesController` sınıfı depo modelini kullanır. Artık LINQ to SQL sınıflarını doğrudan kullanmaz.

**Listeleme 5 – `Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

Kod 5 ' teki `MoviesController` sınıfının iki Oluşturucusu olduğunu unutmayın. Parametresiz oluşturucusu olan ilk Oluşturucu, uygulamanız çalışırken çağırılır. Bu Oluşturucu, `MovieRepository` sınıfının bir örneğini oluşturur ve ikinci oluşturucuya geçirir.

İkinci oluşturucunun tek bir parametresi vardır: bir `IMovieRepository` parametresi. Bu Oluşturucu yalnızca parametre değerini `_repository`adlı bir sınıf düzeyi alanına atar.

`MoviesController` sınıfı, bağımlılık ekleme düzeniyle adlandırılan yazılım tasarımı düzeninden faydalanır. Özellikle, Oluşturucu bağımlılığı ekleme adlı bir şeyi kullanıyor. Bu düzenle ilgili daha fazla bilgiyi, Marwler ile aşağıdaki makaleyi okuyarak okuyabilirsiniz:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

`MoviesController` sınıfındaki tüm kodun (ilk Oluşturucu hariç), gerçek `MovieRepository` sınıfı yerine `IMovieRepository` arabirimiyle etkileşime gireceğini görürsünüz. Kod, arabirimin somut bir uygulanması yerine soyut bir arabirimle etkileşime girer.

Uygulama tarafından kullanılan veri erişim teknolojisini değiştirmek istiyorsanız, `IMovieRepository` arabirimini alternatif veritabanı erişim teknolojisini kullanan bir sınıfla uygulamanız yeterlidir. Örneğin, bir `EntityFrameworkMovieRepository` sınıfı veya bir `SubSonicMovieRepository` sınıfı oluşturabilirsiniz. Denetleyici sınıfı arabirime karşı programlanmış olduğundan, `IMovieRepository` yeni bir uygulamasını denetleyici sınıfına geçirebilir ve sınıf çalışmaya devam edebilir.

Ayrıca, `MoviesController` sınıfını test etmek isterseniz, sahte bir film havuzu sınıfını `HomeController`geçirebilirsiniz. Veritabanına gerçekten erişemediği, ancak `IMovieRepository` arabiriminin tüm gerekli yöntemlerini içeren bir sınıf ile `IMovieRepository` sınıfını uygulayabilirsiniz. Bu şekilde, gerçek bir veritabanına erişmek zorunda kalmadan `MoviesController` sınıfını test edebilirsiniz.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, Microsoft LINQ to SQL avantajlarından yararlanarak nasıl MVC model sınıfları oluşturacağınızı göstermektir. Veritabanı verilerini bir ASP.NET MVC uygulamasında görüntülemek için iki strateji inceliyoruz. İlk olarak, LINQ to SQL sınıfları oluşturduk ve sınıfları doğrudan bir denetleyici eylemi içinde kullandınız. Bir denetleyici içinde LINQ to SQL sınıfları kullanmak, veritabanı verilerini bir MVC uygulamasında hızlı ve kolay bir şekilde görüntülemenizi sağlar.

Daha sonra, veritabanı verilerini görüntülemek için biraz daha zor, ancak kesinlikle daha fazla sanallaştırılan yol araştırdık. Depo deseninin avantajlarından faydalantık ve tüm veritabanı erişim mantığımızı ayrı bir depo sınıfına yerleştirdik. Denetleyicimizde, tüm kodumuzu somut bir sınıf yerine bir arabirime göre yazdık. Depo deseninin avantajı, gelecekte veritabanı erişim teknolojilerini kolayca değiştirmenize olanak tanıdığından, denetleyici sınıflarınızı kolayca test etmemizi sağlar.

> [!div class="step-by-step"]
> [Önceki](creating-model-classes-with-the-entity-framework-cs.md)
> [İleri](displaying-a-table-of-database-data-cs.md)
