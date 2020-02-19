---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: Film modeli ve tablosuna yeni alan ekleme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457706"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a>Film Modeli ve Tablosuna Yeni Alan Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.

Bu bölümde, değişikliğin veritabanına uygulanması için model sınıflarında bazı değişiklikleri geçirmek üzere Entity Framework Code First Migrations kullanacaksınız.

Varsayılan olarak, bu öğreticide yaptığınız gibi, otomatik olarak bir veritabanı oluşturmak için Entity Framework Code First kullandığınızda Code First veritabanının şemasının oluşturulduğu model sınıflarıyla eşitlenmiş olup olmadığını izlemeye yardımcı olmak üzere veritabanına tablo ekler. Eşitlenmiyorsa Entity Framework bir hata oluşturur. Bu durum, çalışma zamanında yalnızca (hataları gizleyerek) bulabileceğiniz geliştirme zamanında sorunları izlemenizi kolaylaştırır.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>Model değişiklikleri için Code First Migrations ayarlama

Visual Studio 2012 kullanıyorsanız, veritabanı aracını açmak için Çözüm Gezgini *film. mdf* dosyasına çift tıklayın. Web için Visual Studio Express Veritabanı Gezgini gösterir, Visual Studio 2012 Sunucu Gezgini gösterecektir. Visual Studio 2010 kullanıyorsanız SQL Server Nesne Gezgini kullanın.

Veritabanı aracında (Veritabanı Gezgini, Sunucu Gezgini veya SQL Server Nesne Gezgini), filmler veritabanını bırakmak için `MovieDBContext` ' a sağ tıklayın ve **Sil** ' i seçin.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

Çözüm Gezgini için geri gidin. Filmler veritabanını kaldırmak için *filmler. mdf* dosyasına sağ tıklayın ve **Sil** ' i seçin.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

Hata olmadığından emin olmak için uygulamayı derleyin.

**Araçlar** menüsünden **NuGet Paket Yöneticisi**’ne ve ardından **Paket Yöneticisi Konsolu**’na tıklayın.

![Paket Man 'ı Ekle](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

`PM>` isteminde **Paket Yöneticisi konsolu** penceresinde "Enable-geçişler-ContextTypeName MvcMovie. modeller. MovieDBContext" yazın.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

**Enable-geçişler** komutu (yukarıda gösterilmiştir) yeni bir *geçişler* klasöründe bir *Configuration.cs* dosyası oluşturur.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

Visual Studio, *Configuration.cs* dosyasını açar. *Configuration.cs* dosyasındaki `Seed` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

`Movie` altındaki kırmızı dalgalı çizgiye sağ tıklayın ve ardından **mvcmovie. modeller** **kullanarak** **Çözümle** ' yi seçin.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

Bunun yapılması Aşağıdaki using ifadesini ekler:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> Code First Migrations her geçişten sonra `Seed` yöntemini çağırır (yani, Paket Yöneticisi konsolundaki **Update-Database** ' i çağırarak) ve bu yöntem önceden eklenmiş satırları güncelleştirir veya henüz yoksa onları ekler.

**Projeyi derlemek IÇIN CTRL-SHIFT-B tuşlarına basın.** (Bu noktada derlenmezseniz aşağıdaki adımlar başarısız olur.)

Sonraki adım, ilk geçiş için bir `DbMigration` sınıfı oluşturmaktır. Bu geçiş, yeni bir veritabanı oluşturur. bu nedenle, önceki bir adımda bulunan *Movie. mdf* dosyasını silmiş olursunuz.

**Paket Yöneticisi konsolu** penceresinde, ilk geçişi oluşturmak için "Add-geçiş Initial" komutunu girin. "Initial" adı rasgele olur ve oluşturulan geçiş dosyasını adlandırmak için kullanılır.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

Code First Migrations, *geçişler* klasöründe başka bir sınıf dosyası oluşturur ( *{datestamp}\_Initial.cs* ) ve bu sınıf veritabanı şemasını oluşturan kodu içerir. Geçiş dosya adı, sıralamaya yardımcı olması için zaman damgasıyla önceden düzeltilir. *{DateStamp}\_Initial.cs* dosyasını Inceleyin, film DB için film tablosu oluşturma yönergelerini içerir. Aşağıdaki yönergelerdeki veritabanını güncelleştirdiğinizde, bu *{dateStamp}\_Initial.cs* dosyası ÇALıŞACAKTıR ve DB şemasını oluşturacaktır. Ardından, VERITABANıNı test verileriyle doldurmak için **çekirdek** yöntemi çalışacaktır.

**Paket Yöneticisi konsolunda**, veritabanını oluşturmak ve **çekirdek** yöntemini çalıştırmak için "Update-Database" komutunu girin.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

Bir tablonun zaten var olduğunu ve oluşturulamayabileceğini belirten bir hata alırsanız, veritabanını sildikten sonra ve `update-database`çalıştırmadan önce uygulamayı çalıştırmanızdan kaynaklanıyor olabilirsiniz. Bu durumda, *filmler. mdf* dosyasını yeniden silin ve `update-database` komutunu yeniden deneyin. Yine de bir hata alırsanız, geçişler klasörünü ve içeriğini silin ve ardından bu sayfanın üst kısmındaki yönergelerden başlayın (yani, *filmler. mdf* dosyasını silin ve ardından geçişlere devam edin).

Uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Çekirdek veriler görüntülenir.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>Film modeline bir derecelendirme özelliği ekleme

Yeni bir `Rating` özelliğini varolan `Movie` sınıfına ekleyerek başlayın. *Models\movie.cs* dosyasını açın ve bunun gibi `Rating` özelliğini ekleyin:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

Tüm `Movie` sınıfı artık aşağıdaki kod gibi görünür:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

**Derlemeyi** &gt;**Build filmi** oluştur menü komutunu kullanarak veya CTRL-SHIFT-B tuşlarına basarak uygulamayı oluşturun.

Artık `Model` sınıfını güncelleştirmiş olduğunuza göre, yeni `Rating` özelliğini tarayıcı görünümünde görüntülemek için *\Views\Movies\Index.cshtml* ve *\Views\Movies\Create.cshtml* View şablonlarını da güncelleştirmeniz gerekir.

<em>\Views\Movies\Index.cshtml</em> dosyasını açın ve <strong>Fiyat</strong> sütununun hemen ardından `<th>Rating</th>` bir sütun başlığı ekleyin. Sonra, `@item.Rating` değerini işlemek için şablonun sonuna yakın bir `<td>` sütunu ekleyin. Güncelleştirilmiş <em>Index. cshtml</em> görünüm şablonu şöyle görünür:

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

Sonra, *\Views\Movies\Create.cshtml* dosyasını açın ve formun sonuna yakın olan aşağıdaki biçimlendirmeyi ekleyin. Bu, yeni bir film oluşturulduğunda bir derecelendirme belirleyebilmeniz için bir metin kutusu oluşturur.

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

Artık uygulama kodunu yeni `Rating` özelliğini destekleyecek şekilde güncelleştirdiniz.

Şimdi uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Bunu yaptığınızda, aşağıdaki hatalardan birini görürsünüz:

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

Bu hatayı, uygulamadaki güncelleştirilmiş `Movie` modeli sınıfı artık var olan veritabanının `Movie` tablosunun şemasından farklı olduğu için görüyorsunuz. (Veritabanı tablosunda `Rating` sütunu yoktur.)

Hatayı çözmek için birkaç yaklaşım vardır:

1. Entity Framework yeni model sınıfı şemasına göre otomatik olarak veritabanını bırakıp yeniden oluşturmayı sağlayabilirsiniz. Bu yaklaşım, bir test veritabanı üzerinde etkin geliştirme yaparken çok kullanışlıdır; modeli ve veritabanı şemasını birlikte hızla gelişmenize olanak tanır. Bunun yanında, bu yaklaşımı bir üretim veritabanında *kullanmak istemezsiniz,* ancak bu, veritabanında var olan verileri kaybetmeniz olur. Bir veritabanının test verileriyle otomatik olarak çekirdeği oluşturmak için bir başlatıcı kullanılması, genellikle bir uygulama geliştirmenin üretken bir yoludur. Entity Framework veritabanı başlatıcıları hakkında daha fazla bilgi için bkz. Tom Dykstra 's [ASP.NET MVC/Entity Framework öğreticisi](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).
2. Mevcut veritabanının şemasını model sınıflarıyla eşleşecek şekilde açıkça değiştirin. Bu yaklaşımın avantajı, verilerinizi tutmanızı kullanmaktır. Bu değişikliği el ile ya da bir veritabanı değişiklik betiği oluşturarak yapabilirsiniz.
3. Veritabanı şemasını güncelleştirmek için Code First Migrations kullanın.

Bu öğretici için Code First Migrations kullanacağız.

Çekirdek yöntemini yeni sütun için bir değer sağlayacak şekilde güncelleştirin. Migrations\Configuration.cs dosyasını açın ve her bir film nesnesine bir derecelendirme alanı ekleyin.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın ve aşağıdaki komutu girin:

`add-migration AddRatingMig`

`add-migration` komutu, geçiş çerçevesinin geçerli film modelini geçerli film DB şemasıyla incelemesini ve VERITABANıNı yeni modele geçirmek için gerekli kodu oluşturmasını söyler. Addrampamig rastgele ve geçiş dosyasını adlandırmak için kullanılır. Geçiş adımı için anlamlı bir ad kullanılması yararlı olur.

Bu komut tamamlandığında, Visual Studio yeni `DbMigration` türetilen sınıfı tanımlayan sınıf dosyasını açar ve `Up` yönteminde yeni sütunu oluşturan kodu görebilirsiniz.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresinde "Güncelleştir-veritabanı" komutunu girin.

Aşağıdaki görüntüde, **Paket Yöneticisi konsol** penceresinde çıkış gösterilmektedir (ön bekleyen Addesmig tarih damgası farklı olacaktır.)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

Uygulamayı yeniden çalıştırın ve/filmler URL 'sine gidin. Yeni derecelendirme alanını görebilirsiniz.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın. Bir derecelendirme ekleyebileceğinizi unutmayın.

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

**Oluştur**'a tıklayın. Yeni film, derecelendirme de dahil, artık filmler listesinde görüntülenir:

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

Ayrıca, düzenleme, Ayrıntılar ve Searchındex görünüm şablonlarına `Rating` alanını da eklemeniz gerekir.

**Paket Yöneticisi konsol** penceresinde "Güncelleştir-veritabanı" komutunu tekrar girebilir ve şema modelle eşleştiğinden hiçbir değişiklik yapılmaz.

Bu bölümde, model nesnelerini nasıl değiştirebileceğiniz ve veritabanını değişikliklerle eşitlenmiş halde tutan bir şekilde gördünüz. Ayrıca, senaryoları deneyebilmeniz için yeni oluşturulan bir veritabanını örnek verilerle doldurmanın bir yolunu öğrenmiş olursunuz. Daha sonra model sınıflarına daha zengin doğrulama mantığı ekleme ve bazı iş kurallarının uygulanmasını sağlama konusuna bakalım.

> [!div class="step-by-step"]
> [Önceki](examining-the-edit-methods-and-edit-view.md)
> [İleri](adding-validation-to-the-model.md)
