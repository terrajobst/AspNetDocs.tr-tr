---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: Yeni alan ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: d79655bfadff83095bf4cb84445f5efaf44d6a89
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519082"
---
# <a name="adding-a-new-field"></a>Yeni Alan Ekleme

[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından

[!INCLUDE [Tutorial Note](index.md)]

Bu bölümde, değişikliğin veritabanına uygulanması için model sınıflarında bazı değişiklikleri geçirmek üzere Entity Framework Code First Migrations kullanacaksınız.

Varsayılan olarak, bu öğreticide yaptığınız gibi, otomatik olarak bir veritabanı oluşturmak için Entity Framework Code First kullandığınızda Code First veritabanının şemasının oluşturulduğu model sınıflarıyla eşitlenmiş olup olmadığını izlemeye yardımcı olmak üzere veritabanına tablo ekler. Eşitlenmiyorsa Entity Framework bir hata oluşturur. Bu durum, çalışma zamanında yalnızca (hataları gizleyerek) bulabileceğiniz geliştirme zamanında sorunları izlemenizi kolaylaştırır.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>Model değişiklikleri için Code First Migrations ayarlama

Çözüm Gezgini gidin. Filmler veritabanını kaldırmak için *filmler. mdf* dosyasına sağ tıklayın ve **Sil** ' i seçin. *Filmler. mdf* dosyasını görmüyorsanız, kırmızı anahatta aşağıda gösterilen **tüm dosyaları göster** simgesine tıklayın.

![](adding-a-new-field/_static/image1.png)

Hata olmadığından emin olmak için uygulamayı derleyin.

**Araçlar** menüsünden **NuGet Paket Yöneticisi**’ne ve ardından **Paket Yöneticisi Konsolu**’na tıklayın.

![Paket Man 'ı Ekle](adding-a-new-field/_static/image2.png)

**Paket Yöneticisi konsol** penceresinde `PM>` istemine şunu girin:

Enable-geçişler-ContextTypeName MvcMovie. modeller. MovieDBContext

![](adding-a-new-field/_static/image3.png)

**Enable-geçişler** komutu (yukarıda gösterilmiştir) yeni bir *geçişler* klasöründe bir *Configuration.cs* dosyası oluşturur.

![](adding-a-new-field/_static/image4.png)

Visual Studio, *Configuration.cs* dosyasını açar. *Configuration.cs* dosyasındaki `Seed` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

`Movie` altındaki kırmızı dalgalı çizgi üzerine gelin ve `Show Potential Fixes` ' a tıklayın ve ardından **mvcmovie. modellerini** **kullanma** ' ya tıklayın.

![](adding-a-new-field/_static/image5.png)

Bunun yapılması Aşağıdaki using ifadesini ekler:

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> Code First Migrations her geçişten sonra `Seed` yöntemini çağırır (yani, Paket Yöneticisi konsolundaki **Update-Database** ' i çağırarak) ve bu yöntem önceden eklenmiş satırları güncelleştirir veya henüz yoksa onları ekler.
> 
> Aşağıdaki koddaki [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) yöntemi "upsert" bir işlem gerçekleştirir:
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> [Çekirdek](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) yöntemi her geçişte çalıştığı için, eklemeye çalıştığınız satırlar veritabanını oluşturan ilk geçişten sonra zaten mevcut olacağı için yalnızca verileri ekleyemezsiniz. "[Upsert](http://en.wikipedia.org/wiki/Upsert)" işlemi, zaten var olan bir satır eklemeye çalışırsanız, ancak uygulamayı test ederken yapmış olduğunuz verilerde yapılan değişiklikleri geçersiz kılar. Bazı tablolardaki test verileri ile bu durum oluşmasını istemeyebilirsiniz: bazı durumlarda verileri değiştirirken değişiklikler veritabanı güncelleştirmelerinden sonra kalmasını istiyor. Bu durumda, bir koşullu ekleme işlemi yapmak istiyorsanız, yalnızca mevcut değilse bir satır ekleyin.   
> 
> [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) metoduna geçirilen ilk parametre, bir satırın zaten var olup olmadığını denetlemek için kullanılacak özelliği belirtir. Sağlayabileceğinizden test filmi verileri için, listedeki her bir başlık benzersiz olduğundan bu amaçla `Title` özelliği kullanılabilir:
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> Bu kod, başlıkların benzersiz olduğunu varsayar. El ile yinelenen bir başlık eklerseniz, bir sonraki sefer geçiş işlemi yaptığınızda aşağıdaki özel durumu alırsınız.   
> 
> *Sıra birden fazla öğe içeriyor*  
> 
> [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) yöntemi hakkında daha fazla bilgi için, bkz. [EF 4,3 AddOrUpdate yöntemiyle dikkatli](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)olmak.

**Projeyi derlemek IÇIN CTRL-SHIFT-B tuşlarına basın.** (Bu noktada derleme yapmazsanız aşağıdaki adımlar başarısız olur.)

Sonraki adım, ilk geçiş için bir `DbMigration` sınıfı oluşturmaktır. Bu geçiş yeni bir veritabanı oluşturur. bu nedenle, önceki bir adımda bulunan *Movie. mdf* dosyasını silmiş olursunuz.

**Paket Yöneticisi konsolu** penceresinde, ilk geçişi oluşturmak için komutu `add-migration Initial` girin. "Initial" adı rasgele olur ve oluşturulan geçiş dosyasını adlandırmak için kullanılır.

![](adding-a-new-field/_static/image6.png)

Code First Migrations, *geçişler* klasöründe başka bir sınıf dosyası oluşturur ( *{datestamp}\_Initial.cs* ) ve bu sınıf veritabanı şemasını oluşturan kodu içerir. Geçiş dosya adı, sıralamaya yardımcı olması için zaman damgasıyla önceden düzeltilir. *{DateStamp}\_Initial.cs* dosyasını Inceleyerek, film DB için `Movies` tablo oluşturma yönergelerini içerir. Aşağıdaki yönergelerdeki veritabanını güncelleştirdiğinizde, bu *{dateStamp}\_Initial.cs* dosyası ÇALıŞACAKTıR ve DB şemasını oluşturacaktır. Ardından, VERITABANıNı test verileriyle doldurmak için **çekirdek** yöntemi çalışacaktır.

**Paket Yöneticisi konsolunda**veritabanını oluşturmak ve `Seed` metodunu çalıştırmak için `update-database` komutunu girin.

![](adding-a-new-field/_static/image7.png)

Bir tablonun zaten var olduğunu ve oluşturulamayabileceğini belirten bir hata alırsanız, veritabanını sildikten sonra ve `update-database`çalıştırmadan önce uygulamayı çalıştırmanızdan kaynaklanıyor olabilirsiniz. Bu durumda, *filmler. mdf* dosyasını yeniden silin ve `update-database` komutunu yeniden deneyin. Yine de bir hata alırsanız, geçişler klasörünü ve içeriğini silin ve ardından bu sayfanın üst kısmındaki yönergelerden başlayın (yani, *filmler. mdf* dosyasını silin ve ardından geçişlere devam edin). Hala bir hata alırsanız, SQL Server Nesne Gezgini açın ve veritabanını listeden kaldırın.

Uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Çekirdek veriler görüntülenir.

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>Film modeline bir derecelendirme özelliği ekleme

Yeni bir `Rating` özelliğini varolan `Movie` sınıfına ekleyerek başlayın. *Models\movie.cs* dosyasını açın ve bunun gibi `Rating` özelliğini ekleyin:

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

Tüm `Movie` sınıfı artık aşağıdaki kod gibi görünür:

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

Uygulamayı derleyin (Ctrl + Shift + B).

`Movie` sınıfına yeni bir alan eklediyseniz, bu yeni özelliğin dahil edilmesini sağlamak için bağlama *beyaz listesini* de güncelleştirmeniz gerekir. `Create` ve `Edit` eylem yöntemlerinin `bind` özniteliğini `Rating` özelliği içerecek şekilde güncelleştirin:

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

Ayrıca, tarayıcı görünümündeki yeni `Rating` özelliğini görüntülemek, oluşturmak ve düzenlemek için görünüm şablonlarını güncelleştirmeniz gerekir.

*\Views\Movies\Index.cshtml* dosyasını açın ve **Fiyat** sütununun hemen ardından `<th>Rating</th>` bir sütun başlığı ekleyin. Sonra, `@item.Rating` değerini işlemek için şablonun sonuna yakın bir `<td>` sütunu ekleyin. Güncelleştirilmiş *Index. cshtml* görünüm şablonu şöyle görünür:

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

Sonra, *\Views\Movies\Create.cshtml* dosyasını açın ve aşağıdaki vurgulanmış işaretlerle `Rating` alanını ekleyin. Bu, yeni bir film oluşturulduğunda bir derecelendirme belirleyebilmeniz için bir metin kutusu oluşturur.

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

Artık uygulama kodunu yeni `Rating` özelliğini destekleyecek şekilde güncelleştirdiniz.

Uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Bunu yaptığınızda, aşağıdaki hatalardan birini görürsünüz:

![](adding-a-new-field/_static/image9.png)  
  
' MovieDBContext ' bağlamını destekleyen model veritabanı oluşturulduktan sonra değiştirildi. Veritabanını güncelleştirmek için Code First Migrations kullanmayı düşünün (https://go.microsoft.com/fwlink/?LinkId=238269).

![](adding-a-new-field/_static/image10.png)

Bu hatayı, uygulamadaki güncelleştirilmiş `Movie` modeli sınıfı artık var olan veritabanının `Movie` tablosunun şemasından farklı olduğu için görüyorsunuz. (Veritabanı tablosunda `Rating` sütunu yoktur.)

Hatayı çözmek için birkaç yaklaşım vardır:

1. Entity Framework yeni model sınıfı şemasına göre otomatik olarak veritabanını bırakıp yeniden oluşturmayı sağlayabilirsiniz. Bu yaklaşım, bir test veritabanı üzerinde etkin geliştirme yaparken geliştirme döngüsünün başlarında çok daha kolay. modeli ve veritabanı şemasını birlikte hızla gelişmenize olanak tanır. Bunun yanında, bu yaklaşımı bir üretim veritabanında *kullanmak istemezsiniz,* ancak bu, veritabanında var olan verileri kaybetmeniz olur. Bir veritabanının test verileriyle otomatik olarak çekirdeği oluşturmak için bir başlatıcı kullanılması, genellikle bir uygulama geliştirmenin üretken bir yoludur. Entity Framework veritabanı başlatıcıları hakkında daha fazla bilgi için bkz. [ASP.NET MVC/Entity Framework öğreticisi](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).
2. Mevcut veritabanının şemasını model sınıflarıyla eşleşecek şekilde açıkça değiştirin. Bu yaklaşımın avantajı, verilerinizi tutmanızı kullanmaktır. Bu değişikliği el ile ya da bir veritabanı değişiklik betiği oluşturarak yapabilirsiniz.
3. Veritabanı şemasını güncelleştirmek için Code First Migrations kullanın.

Bu öğretici için Code First Migrations kullanacağız.

Çekirdek yöntemini yeni sütun için bir değer sağlayacak şekilde güncelleştirin. Migrations\Configuration.cs dosyasını açın ve her bir film nesnesine bir derecelendirme alanı ekleyin.

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın ve aşağıdaki komutu girin:

`add-migration Rating`

`add-migration` komutu, geçiş çerçevesinin geçerli film modelini geçerli film DB şemasıyla incelemesini ve VERITABANıNı yeni modele geçirmek için gerekli kodu oluşturmasını söyler. Ad *derecelendirmesi* rasgele ve geçiş dosyasını adlandırmak için kullanılır. Geçiş adımı için anlamlı bir ad kullanılması yararlı olur.

Bu komut tamamlandığında, Visual Studio yeni `DbMigration` türetilen sınıfı tanımlayan sınıf dosyasını açar ve `Up` yönteminde yeni sütunu oluşturan kodu görebilirsiniz.

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

Çözümü oluşturun ve ardından **Paket Yöneticisi konsolu** penceresine `update-database` komutunu girin.

Aşağıdaki görüntüde, **Paket Yöneticisi konsol** penceresinde çıkış gösterilmektedir (Tarih damgası ön bekleyen *Derecelendirme* farklı olacaktır.)

![](adding-a-new-field/_static/image11.png)

Uygulamayı yeniden çalıştırın ve/filmler URL 'sine gidin. Yeni derecelendirme alanını görebilirsiniz.

![](adding-a-new-field/_static/image12.png)

Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın. Bir derecelendirme ekleyebileceğinizi unutmayın.

![7_CreateRioII](adding-a-new-field/_static/image13.png)

**Oluştur**'u tıklatın. Yeni film, derecelendirme de dahil, artık filmler listesinde görüntülenir:

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

Artık proje geçişleri kullanıyor olduğuna göre, yeni bir alan eklediğinizde veya şemayı güncelleştirdiğinizde veritabanını bırakmalısınız. Sonraki bölümde, daha fazla şema değişikliği yapacağız ve veritabanını güncelleştirmek için geçişleri kullanacağız.

Ayrıca, `Rating` alanını Düzenle, Ayrıntılar ve Sil görünüm şablonlarına de eklemeniz gerekir.

**Paket Yöneticisi konsol** penceresinde "Güncelleştir-veritabanı" komutunu tekrar girebilir ve şema modelle eşleştiğinden geçiş kodu çalıştırılmaz. Bununla birlikte, "Update-Database" çalıştırmak `Seed` yöntemini yeniden çalıştırır ve çekirdek verilerinden herhangi birini değiştirdiyseniz değişiklikler kaybedilir çünkü `Seed` yöntemi de bu verileri çıkarır. Tom Dykstra 'in popüler [ASP.NET MVC/Entity Framework öğreticisinde](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)`Seed` yöntemi hakkında daha fazla bilgi edinebilirsiniz.

Bu bölümde, model nesnelerini nasıl değiştirebileceğiniz ve veritabanını değişikliklerle eşitlenmiş halde tutan bir şekilde gördünüz. Ayrıca, senaryoları deneyebilmeniz için yeni oluşturulan bir veritabanını örnek verilerle doldurmanın bir yolunu öğrenmiş olursunuz. Bu yalnızca Code First hızlı bir giriştir, konu hakkında daha kapsamlı bir öğretici için [ASP.NET MVC uygulaması için Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) konusuna bakın. Daha sonra model sınıflarına daha zengin doğrulama mantığı ekleme ve bazı iş kurallarının uygulanmasını sağlama konusuna bakalım.

> [!div class="step-by-step"]
> [Önceki](adding-search.md)
> [İleri](adding-validation.md)
