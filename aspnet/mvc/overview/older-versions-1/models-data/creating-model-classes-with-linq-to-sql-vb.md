---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: LINQ to SQL ile model sınıfları oluşturma (VB) | Microsoft Docs
author: microsoft
description: Bu öğreticinin amacı, bir ASP.NET MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu öğreticide, model c 'yi derlemeyi öğreneceksiniz...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 88a5f1037d93ef3bdc95bf60b6005ebb254ab440
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588524"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a>LINQ to SQL ile Model Sınıfları Oluşturma (VB)

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> Bu öğreticinin amacı, bir ASP.NET MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu öğreticide, Microsoft LINQ to SQL avantajlarından yararlanarak model sınıfları oluşturmayı ve veritabanı erişimi yapmayı öğreneceksiniz.

Bu öğreticinin amacı, bir ASP.NET MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu öğreticide, Microsoft LINQ to SQL avantajlarından yararlanarak model sınıfları oluşturmayı ve veritabanı erişimi yapmayı öğreneceksiniz.

Bu öğreticide, temel bir film veritabanı uygulaması oluşturacağız. Mümkün olan en hızlı ve en kolay şekilde film veritabanı uygulaması oluşturarak başlayacağız. Tüm veri erişimlerimizi doğrudan denetleyici eylemlerimizden gerçekleştirdik.

Daha sonra, depo deseninin nasıl kullanılacağını öğrenirsiniz. Depo deseninin kullanılması biraz daha fazla iş gerektirir. Ancak, bu düzenin benimseme avantajı, değiştirilecek ve kolayca test edebileceğiniz uygulamalar oluşturmanıza olanak sağlar.

## <a name="what-is-a-model-class"></a>Model sınıfı nedir?

MVC modeli, MVC görünümünde veya MVC denetleyicisinde bulunmayan tüm uygulama mantığını içerir. Özellikle bir MVC modeli, tüm uygulama iş ve veri erişim mantığınızı içerir.

Veri erişim mantığınızı uygulamak için çeşitli farklı teknolojiler kullanabilirsiniz. Örneğin, veri erişim sınıflarınızı Microsoft Entity Framework, Nhazırda beklet, Subsonic veya ADO.NET sınıfları kullanarak oluşturabilirsiniz.

Bu öğreticide, veritabanını sorgulamak ve güncelleştirmek için LINQ to SQL kullanıyorum. LINQ to SQL, bir Microsoft SQL Server veritabanıyla etkileşim kurmak için çok kolay bir yöntem sağlar. Ancak, ASP.NET MVC çerçevesinin herhangi bir şekilde LINQ to SQL bağlı olmadığını anlamak önemlidir. ASP.NET MVC, herhangi bir veri erişim teknolojisi ile uyumludur.

## <a name="create-a-movie-database"></a>Film veritabanı oluşturma

Bu öğreticide, model sınıfları nasıl oluşturabileceğiniz hakkında daha fazla anlamak için basit bir film veritabanı uygulaması oluşturacağız. İlk adım yeni bir veritabanı oluşturmaktır. Çözüm Gezgini penceresindeki uygulama\_veri klasörüne sağ tıklayın ve **Ekle, yeni öğe**menü seçeneğini belirleyin. SQL Server veritabanı şablonunu seçin, MoviesDB. mdf adını verin ve **Ekle** düğmesine tıklayın (bkz. Şekil 1).

[Yeni bir SQL Server veritabanı ekleme ![](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**Şekil 01**: yeni bir SQL Server veritabanı ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))

Yeni veritabanını oluşturduktan sonra, App\_Data klasöründeki MoviesDB. mdf dosyasını çift tıklayarak veritabanını açabilirsiniz. MoviesDB. mdf dosyasına çift tıklamak Sunucu Gezgini penceresini açar (bkz. Şekil 2).

|   | Sunucu Gezgini penceresine Visual Web Developer kullanılırken Veritabanı Gezgini penceresi denir. |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

[Sunucu Gezgini penceresini kullanarak ![](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**Şekil 02**: Sunucu Gezgini penceresini kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))

Veritabanımızın filmimizi temsil eden bir tablo eklememiz gerekiyor. Tablolar klasörüne sağ tıklayın ve **Yeni Tablo Ekle**menü seçeneğini belirleyin. Bu menü seçeneği belirlendiğinde Tablo Tasarımcısı açılır (bkz. Şekil 3).

[Sunucu Gezgini penceresini kullanarak ![](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**Şekil 03**: Tablo Tasarımcısı ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))

Veritabanı tablomuza aşağıdaki sütunları eklememiz gerekiyor:

| **Sütun adı** | **Veri türü** | **Null değerlere izin ver** |
| --- | --- | --- |
| Numarasını | int | False |
| Başlık | Nvarchar (200) | False |
| Ktörü | nvarchar (50) | False |

Kimlik sütununda iki özel şey yapmanız gerekir. İlk olarak, Tablo Tasarımcısı sütunu seçip bir anahtarın simgesine tıklayarak ID sütununu birincil anahtar sütunu olarak işaretlemeniz gerekir. LINQ to SQL, veritabanına yönelik ekleme veya güncelleştirme gerçekleştirirken birincil anahtar sütunlarınızı belirtmenizi gerektirir.

Ardından, Evet değerini **,** Identity özelliğine (bkz. Şekil 3) atayarak kimlik sütununu kimlik sütunu olarak işaretlemeniz gerekir. Bir kimlik sütunu, tabloya yeni bir veri satırı eklediğinizde otomatik olarak yeni bir sayı atanan sütundur.

Bu değişiklikleri yaptıktan sonra, tabloyu tblMovie adıyla kaydedin. Kaydet düğmesine tıklayarak tabloyu kaydedebilirsiniz.

## <a name="create-linq-to-sql-classes"></a>LINQ to SQL sınıfları oluşturma

MVC modelimiz tblMovie veritabanı tablosunu temsil eden LINQ to SQL sınıflar içerir. Bu LINQ to SQL sınıfları oluşturmanın en kolay yolu modeller klasörüne sağ tıklayın, **Ekle, yeni öğe**, LINQ to SQL sınıfları şablonunu seçin, sınıflara film. dbml adını verir ve **Ekle** düğmesine (bkz. Şekil 4) tıklayın.

[LINQ to SQL sınıfları oluşturma ![](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**Şekil 04**: LINQ to SQL sınıfları oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))

Film LINQ to SQL sınıfları oluşturduktan hemen sonra, Nesne İlişkisel Tasarımcısı görünür. Veritabanı tablolarını, belirli veritabanı tablolarını temsil eden LINQ to SQL sınıfları oluşturmak için Sunucu Gezgini penceresinden Nesne İlişkisel Tasarımcısı sürükleyebilirsiniz. TblMovie veritabanı tablosunu Nesne İlişkisel Tasarımcısı eklememiz gerekiyor (bkz. Şekil 4).

[Nesne İlişkisel Tasarımcısı kullanarak ![](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**Şekil 05**: nesne ilişkisel Tasarımcısı kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))

Varsayılan olarak Nesne İlişkisel Tasarımcısı, tasarımcı üzerine sürüklediğiniz veritabanı tablosuyla aynı ada sahip bir sınıf oluşturur. Ancak, tblMovie sınıfımızı çağırmak istemiyorum. Bu nedenle, tasarımcıda sınıfın adına tıklayın ve sınıfın adını filmle değiştirin.

Son olarak, LINQ to SQL sınıflarını kaydetmek için **Kaydet** düğmesine (disketin resmi) tıklaması gerektiğini unutmayın. Aksi takdirde LINQ to SQL sınıfları Nesne İlişkisel Tasarımcısı oluşturulmaz.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Bir denetleyici eyleminde LINQ to SQL kullanma

Artık LINQ to SQL sınıflarımız olduğuna göre, veritabanından veri almak için bu sınıfları kullanabiliriz. Bu bölümde, LINQ to SQL sınıflarını doğrudan bir denetleyici eylemi içinde kullanmayı öğreneceksiniz. Bir MVC görünümündeki tblMovies veritabanı tablosundan film listesi görüntüleriz.

İlk olarak, HomeController sınıfını değiştirmemiz gerekiyor. Bu sınıf, uygulamanızın denetleyiciler klasöründe bulunabilir. Sınıfı, liste 1 ' deki sınıfa benzemek üzere değiştirin.

**Listeleme 1 – `Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

Liste 1 ' deki dizin () eylemi, MoviesDB veritabanını temsil etmek için bir LINQ to SQL DataContext Sınıfı (MovieDataContext) kullanır. MoveDataContext sınıfı, Visual Studio Nesne İlişkisel Tasarımcısı tarafından oluşturuldu.

TblMovies veritabanı tablosundan tüm filmleri almak için DataContext 'e karşı bir LINQ sorgusu gerçekleştirilir. Film listesi, filmler adlı bir yerel değişkene atanır. Son olarak, film listesi görünüm verileri aracılığıyla görünüme geçirilir.

Filmleri göstermek için bir sonraki adımda Dizin görünümünü değiştirmemiz gerekiyor. Dizin görünümünü Views\Home\ klasöründe bulabilirsiniz. Dizin görünümünü, liste 2 ' de görünüm gibi görünecek şekilde güncelleştirin.

**Listeleme 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

Değiştirilen dizin görünümü görünümün en üstünde bir &lt;% @ Import Namespace%&gt; yönergesini içerdiğine dikkat edin. Bu yönerge MvcApplication1 ad alanını içeri aktarır. Bu ad alanı, model sınıflarıyla çalışmak için gereklidir: özellikle, görünümde film sınıfı.

Liste 2 ' deki görünüm, ViewData. Model özelliği tarafından temsil edilen tüm öğeler boyunca yinelenen her döngü Için bir içerir. Title özelliğinin değeri her film için görüntülenir.

ViewData. model özelliğinin değeri bir IEnumerable 'a dönüştürültiğine dikkat edin. Bu, ViewData. model içeriklerinin döngüsü için gereklidir. Burada başka bir seçenek de kesin türü belirtilmiş bir görünüm oluşturmaktır. Türü kesin belirlenmiş bir görünüm oluşturduğunuzda, ViewData. model özelliğini bir görünümün arka plan kod sınıfında belirli bir türe atamalısınız.

Uygulamayı, HomeController sınıfını ve Dizin görünümünü değiştirdikten sonra çalıştırırsanız boş bir sayfa alırsınız. TblMovies veritabanı tablosunda film kaydı olmadığından boş bir sayfa alacaksınız.

TblMovies veritabanı tablosuna kayıt eklemek için, Sunucu Gezgini penceresinde tblMovies veritabanı tablosuna sağ tıklayın (Visual Web Developer 'da Veritabanı Gezgini Window) ve **tablo verilerini göster**menü seçeneğini belirleyin. Görüntülenen Kılavuzu kullanarak film kayıtları ekleyebilirsiniz (bkz. Şekil 5).

[film ekleme ![](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**Şekil 06**: film ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))

TblMovies tablosuna bazı veritabanı kayıtları ekledikten ve uygulamayı çalıştırırsanız, Şekil 7 ' de sayfayı görürsünüz. Tüm film veritabanı kayıtları madde işaretli bir listede görüntülenir.

[Dizin görünümüyle film görüntüleme ![](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**Şekil 07**: filmleri Dizin görünümüyle görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))

## <a name="using-the-repository-pattern"></a>Depo deseninin kullanımı

Önceki bölümde, sınıfları doğrudan bir denetleyici eylemi içinde LINQ to SQL kullandık. MovieDataContext sınıfını doğrudan dizin () denetleyicisi eyleminden kullandık. Basit bir uygulama durumunda bunu yaparken bir sorun yoktur. Ancak, bir denetleyici sınıfında LINQ to SQL doğrudan çalışmak, daha karmaşık bir uygulama oluşturmanız gerektiğinde sorunlar oluşturur.

Bir denetleyici sınıfı içinde LINQ to SQL kullanmak, daha sonra veri erişim teknolojilerinin değiştirilmesini zorlaştırır. Örneğin, Microsoft LINQ to SQL kullanarak veri erişim teknolojiniz olarak Microsoft Entity Framework kullanmaya geçiş yapabilirsiniz. Bu durumda, uygulamanızın içindeki veritabanına erişen her denetleyiciyi yeniden yazmanız gerekir.

Bir denetleyici sınıfı içinde LINQ to SQL kullanmak, uygulamanız için birim testlerini oluşturmayı zorlaştırır. Normalde, birim testlerini gerçekleştirirken bir veritabanıyla etkileşime geçmek istemezsiniz. Veritabanı sunucunuzu değil, Uygulama mantığınızı test etmek için birim testlerinizi kullanmak istiyorsunuz.

Daha sonra değişiklik yapılacak ve daha kolay test edebileceğiniz bir MVC uygulaması oluşturmak için depo düzenini kullanmayı göz önünde bulundurmanız gerekir. Depo modelini kullanırken, tüm veritabanı erişim mantığınızı içeren ayrı bir depo sınıfı oluşturursunuz.

Depo sınıfını oluşturduğunuzda, depo sınıfı tarafından kullanılan tüm yöntemleri temsil eden bir arabirim oluşturursunuz. Denetleyicileriniz dahilinde, kodunuzu depo yerine arabirime yazarsınız. Bu şekilde, gelecekte farklı veri erişimi teknolojileri kullanarak depoyu uygulayabilirsiniz.

Listeleme 3 ' teki arabirim IMovieRepository olarak adlandırılmıştır ve ListAll () adlı tek bir yöntemi temsil eder.

**Listeleme 3 – `Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

Listeleme 4 ' teki depo sınıfı IMovieRepository arabirimini uygular. IMovieRepository arabirimi için gereken yönteme karşılık gelen ListAll () adlı bir yöntem içerdiğine dikkat edin.

**Listeleme 4 – `Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

Son olarak, kod 5 ' teki MoviesController sınıfı depo modelini kullanır. Artık LINQ to SQL sınıflarını doğrudan kullanmaz.

**Listeleme 5 – `Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

Kod 5 ' teki MoviesController sınıfının iki Oluşturucusu olduğunu unutmayın. Parametresiz oluşturucusu olan ilk Oluşturucu, uygulamanız çalışırken çağırılır. Bu Oluşturucu, MovieRepository sınıfının bir örneğini oluşturur ve ikinci oluşturucuya geçirir.

İkinci oluşturucunun tek bir parametresi vardır: bir IMovieRepository parametresi. Bu Oluşturucu, yalnızca parametresinin değerini \_deposu adlı bir sınıf düzeyi alanına atar.

MoviesController sınıfı, bağımlılık ekleme düzeniyle adlandırılan bir yazılım tasarımı deseninin avantajlarından yararlanır. Özellikle, Oluşturucu bağımlılığı ekleme adlı bir şeyi kullanıyor. Bu düzenle ilgili daha fazla bilgiyi, Marwler ile aşağıdaki makaleyi okuyarak okuyabilirsiniz:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

MoviesController sınıfındaki tüm kodun (ilk Oluşturucu hariç), gerçek MovieRepository sınıfı yerine IMovieRepository arabirimiyle etkileşime gireceğini görürsünüz. Kod, arabirimin somut bir uygulanması yerine soyut bir arabirimle etkileşime girer.

Uygulama tarafından kullanılan veri erişim teknolojisini değiştirmek istiyorsanız, IMovieRepository arabirimini alternatif veritabanı erişim teknolojisini kullanan bir sınıfla uygulamanız yeterlidir. Örneğin, bir EntityFrameworkMovieRepository sınıfı veya SubSonicMovieRepository sınıfı oluşturabilirsiniz. Denetleyici sınıfı arabirime karşı programlanmış olduğundan, IMovieRepository 'in yeni bir uygulamasını denetleyici sınıfına geçirebilir ve sınıf çalışmaya devam edebilir.

Ayrıca, MoviesController sınıfını test etmek isterseniz, sahte bir film havuzu sınıfını MoviesController 'e geçirebilirsiniz. IMovieRepository sınıfını veritabanına gerçekten erişemediği halde IMovieRepository arabiriminin tüm gerekli yöntemlerini içeren bir sınıfla uygulayabilirsiniz. Böylece, gerçekten gerçek bir veritabanına erişmeden MoviesController sınıfını test edebilirsiniz.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, Microsoft LINQ to SQL avantajlarından yararlanarak nasıl MVC model sınıfları oluşturacağınızı göstermektir. Veritabanı verilerini bir ASP.NET MVC uygulamasında görüntülemek için iki strateji inceliyoruz. İlk olarak, LINQ to SQL sınıfları oluşturduk ve sınıfları doğrudan bir denetleyici eylemi içinde kullandınız. Bir denetleyici içinde LINQ to SQL sınıfları kullanmak, veritabanı verilerini bir MVC uygulamasında hızlı ve kolay bir şekilde görüntülemenizi sağlar.

Daha sonra, veritabanı verilerini görüntülemek için biraz daha zor, ancak kesinlikle daha fazla sanallaştırılan yol araştırdık. Depo deseninin avantajlarından faydalantık ve tüm veritabanı erişim mantığımızı ayrı bir depo sınıfına yerleştirdik. Denetleyicimizde, tüm kodumuzu somut bir sınıf yerine bir arabirime göre yazdık. Depo deseninin avantajı, gelecekte veritabanı erişim teknolojilerini kolayca değiştirmenize olanak tanıdığından, denetleyici sınıflarınızı kolayca test etmemizi sağlar.

> [!div class="step-by-step"]
> [Önceki](creating-model-classes-with-the-entity-framework-vb.md)
> [İleri](displaying-a-table-of-database-data-vb.md)
