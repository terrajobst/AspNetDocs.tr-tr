---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: Film modeli ve tablosuna yeni alan ekleme (C#) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 40b02a2f608f07091ce6b5339688a1e6290e2e37
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540805"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a>Film Modeli ve Tablosuna Yeni Alan Ekleme (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.
> 
> 
> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Kaynak koduna sahip bir Visual Web C# Developer projesi, bu konuyla birlikte kullanılabilecek. [Sürümü C# indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.

Bu bölümde, model sınıflarında bazı değişiklikler yapar ve veritabanı şemasını model değişiklikleriyle eşleşecek şekilde nasıl güncelleştirebileceğinizi öğreneceksiniz.

## <a name="adding-a-rating-property-to-the-movie-model"></a>Film modeline bir derecelendirme özelliği ekleme

Yeni bir `Rating` özelliğini varolan `Movie` sınıfına ekleyerek başlayın. *Movie.cs* dosyasını açın ve bunun gibi `Rating` özelliğini ekleyin:

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

Tüm `Movie` sınıfı artık aşağıdaki kod gibi görünür:

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

**Hata ayıkla** &gt;**Build Movie** menü komutunu kullanarak uygulamayı yeniden derleyin.

Artık `Model` sınıfını güncelleştirmiş olduğunuza göre, yeni `Rating` özelliğini desteklemek için *\Views\Movies\Index.cshtml* ve *\Views\Movies\Create.cshtml* View şablonlarını da güncelleştirmeniz gerekir.

*\Views\Movies\Index.cshtml* dosyasını açın ve **Fiyat** sütununun hemen ardından `<th>Rating</th>` bir sütun başlığı ekleyin. Sonra, `@item.Rating` değerini işlemek için şablonun sonuna yakın bir `<td>` sütunu ekleyin. Güncelleştirilmiş *Index. cshtml* görünüm şablonu şöyle görünür:

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

Sonra, *\Views\Movies\Create.cshtml* dosyasını açın ve formun sonuna yakın olan aşağıdaki biçimlendirmeyi ekleyin. Bu, yeni bir film oluşturulduğunda bir derecelendirme belirleyebilmeniz için bir metin kutusu oluşturur.

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>Model ve veritabanı şeması farklılıklarını yönetme

Artık uygulama kodunu yeni `Rating` özelliğini destekleyecek şekilde güncelleştirdiniz.

Şimdi uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Bunu yaptığınızda, aşağıdaki hatayı görürsünüz:

![](adding-a-new-field/_static/image1.png)

Bu hatayı, uygulamadaki güncelleştirilmiş `Movie` modeli sınıfı artık var olan veritabanının `Movie` tablosunun şemasından farklı olduğu için görüyorsunuz. (Veritabanı tablosunda `Rating` sütunu yoktur.)

Varsayılan olarak, bu öğreticide yaptığınız gibi, otomatik olarak bir veritabanı oluşturmak için Entity Framework Code First kullandığınızda Code First veritabanının şemasının oluşturulduğu model sınıflarıyla eşitlenmiş olup olmadığını izlemeye yardımcı olmak üzere veritabanına tablo ekler. Eşitlenmiyorsa Entity Framework bir hata oluşturur. Bu durum, çalışma zamanında yalnızca (hataları gizleyerek) bulabileceğiniz geliştirme zamanında sorunları izlemenizi kolaylaştırır. Eşitleme denetimi özelliği, yalnızca gördüğünüz hata iletisinin görüntülenmesine neden olur.

Hatayı çözmek için iki yaklaşım vardır:

1. Entity Framework yeni model sınıfı şemasına göre otomatik olarak veritabanını bırakıp yeniden oluşturmayı sağlayabilirsiniz. Bu yaklaşım, model ve veritabanı şemasını bir araya getirebilmenizi sağladığından bir test veritabanı üzerinde etkin geliştirme yaparken çok kullanışlı bir yöntemdir. Bunun yanında, bu yaklaşımı bir üretim veritabanında *kullanmak istemezsiniz,* ancak bu, veritabanında var olan verileri kaybetmeniz olur.
2. Mevcut veritabanının şemasını model sınıflarıyla eşleşecek şekilde açıkça değiştirin. Bu yaklaşımın avantajı, verilerinizi tutmanızı kullanmaktır. Bu değişikliği el ile ya da bir veritabanı değişiklik betiği oluşturarak yapabilirsiniz.

Bu öğreticide, ilk yaklaşımı kullanacağız — Entity Framework Code First, her zaman otomatik olarak veritabanını yeniden oluşturmanız gerekir.

## <a name="automatically-re-creating-the-database-on-model-changes"></a>Model değişikliklerinde veritabanını otomatik olarak yeniden oluşturma

Uygulamayı, uygulama için modeli her değiştirdiğinizde Code First otomatik olarak bırakır ve yeniden oluşturacak şekilde, uygulamayı güncelleştirelim.

> [!NOTE] 
> 
> **Uyarı** Bu yaklaşımı, veritabanını yalnızca geliştirme veya test veritabanı kullanırken ve gerçek verileri içeren bir üretim veritabanında *hiçbir zaman* otomatik olarak bırakıp yeniden oluşturmaya yönelik olarak etkinleştirmeniz gerekir. Bunu bir üretim sunucusunda kullanmak, veri kaybına yol açabilir.

**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.

![](adding-a-new-field/_static/image2.png)

"Movieınitializer" sınıfını adlandırın. `MovieInitializer` sınıfını aşağıdaki kodu içerecek şekilde güncelleştirin:

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

`MovieInitializer` sınıfı, model tarafından kullanılan veritabanının bırakılması ve model sınıfları değiştiğinde otomatik olarak yeniden oluşturulması gerektiğini belirtir. Kod, veritabanında oluşturulduğu zaman (veya yeniden oluşturulduğunda) otomatik olarak veritabanına eklenecek bazı varsayılan verileri belirtmek için bir `Seed` yöntemi içerir. Bu, bir model değişikliğini her seferinde el ile doldurmanıza gerek kalmadan veritabanını bazı örnek verilerle doldurmak için kullanışlı bir yol sağlar.

`MovieInitializer` sınıfını tanımladığınıza göre, uygulama her çalıştığında model sınıflarının veritabanındaki şemadan farklı olup olmadığını kontrol etmek için bu şekilde bağlantı kurmak isteyeceksiniz. Bunlar ise, bir veritabanını modeliyle eşleşecek şekilde yeniden oluşturmak ve ardından veritabanını örnek verilerle doldurmak için başlatıcıyı çalıştırabilirsiniz.

`MvcMovies` projesinin kökündeki *Global. asax* dosyasını açın:

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

*Global. asax* dosyası, proje için tüm uygulamayı tanımlayan sınıfı içerir ve uygulama ilk kez başladığında çalışan bir `Application_Start` olay işleyicisi içerir.

Şimdi dosyanın en üstüne iki using ifadesi ekleyelim. İlki Entity Framework ad alanına başvurur ve ikincisi `MovieInitializer` sınıfımızın yaşadığı ad alanına başvurur:

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

Ardından, aşağıdaki gibi `Application_Start` yöntemini bulun ve yönteminin başına `Database.SetInitializer` bir çağrı ekleyin:

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

Az önce eklediğiniz `Database.SetInitializer` deyimin şeması ve veritabanı eşleşmezse, `MovieDBContext` örneği tarafından kullanılan veritabanının otomatik olarak silinip yeniden oluşturulması gerektiğini gösterir. Gördüğünüz gibi, veritabanını `MovieInitializer` sınıfında belirtilen örnek verilerle de dolduracaktır.

*Global. asax* dosyasını kapatın.

Uygulamayı yeniden çalıştırın ve */filmler* URL 'sine gidin. Uygulama başlatıldığında, model yapısının artık veritabanı şemasıyla eşleşmediğini algılar. Yeni model yapısıyla eşleşecek şekilde veritabanını otomatik olarak yeniden oluşturur ve veritabanını örnek filmlerle doldurur:

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın. Bir derecelendirme ekleyebileceğinizi unutmayın.

[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)

**Oluştur**'u tıklatın. Yeni film, derecelendirme de dahil, artık filmler listesinde görüntülenir:

[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)

Bu bölümde, model nesnelerini nasıl değiştirebileceğiniz ve veritabanını değişikliklerle eşitlenmiş halde tutan bir şekilde gördünüz. Ayrıca, senaryoları deneyebilmeniz için yeni oluşturulan bir veritabanını örnek verilerle doldurmanın bir yolunu öğrenmiş olursunuz. Daha sonra model sınıflarına daha zengin doğrulama mantığı ekleme ve bazı iş kurallarının uygulanmasını sağlama konusuna bakalım.

> [!div class="step-by-step"]
> [Önceki](examining-the-edit-methods-and-edit-view.md)
> [İleri](adding-validation-to-the-model.md)
