---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: Film modeline ve veritabanı tablosuna yeni bir alan ekleme (VB) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: b2b26b6009c55f02c8a4159bda839fe7aefea4c0
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457277"
---
# <a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a>Film Modeli ve Tablosuna Yeni Alan Ekleme (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Bu konuyla birlikte VB.NET kaynak koduna sahip bir Visual Web Developer projesi mevcuttur. [Vb.NET sürümünü indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). İsterseniz C#, Bu öğreticinin [ C# sürümüne](../cs/adding-a-new-field.md) geçin.

Bu bölümde, model sınıflarında bazı değişiklikler yapar ve veritabanı şemasını model değişiklikleriyle eşleşecek şekilde nasıl güncelleştirebileceğinizi öğreneceksiniz.

## <a name="adding-a-rating-property-to-the-movie-model"></a>Film modeline bir derecelendirme özelliği ekleme

Yeni bir `Rating` özelliğini varolan `Movie` sınıfına ekleyerek başlayın. *Movie.cs* dosyasını açın ve bunun gibi `Rating` özelliğini ekleyin:

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

Tüm `Movie` sınıfı artık aşağıdaki kod gibi görünür:

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

**Hata ayıkla** &gt;**Build Movie** menü komutunu kullanarak uygulamayı yeniden derleyin.

Artık `Model` sınıfını güncelleştirmiş olduğunuza göre, yeni `Rating` özelliğini desteklemek için *\Views\Movies\Index.vbhtml* ve *\Views\Movies\Create.vbhtml* View şablonlarını da güncelleştirmeniz gerekir.

<em>\Views\Movies\Index.vbhtml</em> dosyasını açın ve <strong>Fiyat</strong> sütununun hemen ardından `<th>Rating</th>` bir sütun başlığı ekleyin. Sonra, `@item.Rating` değerini işlemek için şablonun sonuna yakın bir `<td>` sütunu ekleyin. Güncelleştirilmiş <em>Index. vbhtml</em> görünüm şablonu şöyle görünür:

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

Sonra, *\Views\Movies\Create.vbhtml* dosyasını açın ve formun sonuna yakın olan aşağıdaki biçimlendirmeyi ekleyin. Bu, yeni bir film oluşturulduğunda bir derecelendirme belirleyebilmeniz için bir metin kutusu oluşturur.

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

Sınıfı Movieınitializer&quot;&quot;adlandırın. `MovieInitializer` sınıfını aşağıdaki kodu içerecek şekilde güncelleştirin:

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

`MovieInitializer` sınıfı, model tarafından kullanılan veritabanının bırakılması ve model sınıfları değiştiğinde otomatik olarak yeniden oluşturulması gerektiğini belirtir. Kod, veritabanında oluşturulduğu zaman (veya yeniden oluşturulduğunda) otomatik olarak veritabanına eklenecek bazı varsayılan verileri belirtmek için bir `Seed` yöntemi içerir. Bu, bir model değişikliğini her seferinde el ile doldurmanıza gerek kalmadan veritabanını bazı örnek verilerle doldurmak için kullanışlı bir yol sağlar.

`MovieInitializer` sınıfını tanımladığınıza göre, uygulama her çalıştığında model sınıflarının veritabanındaki şemadan farklı olup olmadığını kontrol etmek için bu şekilde bağlantı kurmak isteyeceksiniz. Bunlar ise, bir veritabanını modeliyle eşleşecek şekilde yeniden oluşturmak ve ardından veritabanını örnek verilerle doldurmak için başlatıcıyı çalıştırabilirsiniz.

`MvcMovies` projesinin kökündeki *Global. asax* dosyasını açın:

*Global. asax* dosyası, proje için tüm uygulamayı tanımlayan sınıfı içerir ve uygulama ilk kez başladığında çalışan bir `Application_Start` olay işleyicisi içerir.

`Application_Start` yöntemi bulun ve yöntemin başındaki `Database.SetInitializer` için aşağıda gösterildiği gibi bir çağrı ekleyin:

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

Az önce eklediğiniz `Database.SetInitializer` deyimin şeması ve veritabanı eşleşmezse, `MovieDBContext` örneği tarafından kullanılan veritabanının otomatik olarak silinip yeniden oluşturulması gerektiğini gösterir. Gördüğünüz gibi, veritabanını `MovieInitializer` sınıfında belirtilen örnek verilerle de dolduracaktır.

*Global. asax* dosyasını kapatın.

Uygulamayı yeniden çalıştırın ve */filmler* URL 'sine gidin. Uygulama başlatıldığında, model yapısının artık veritabanı şemasıyla eşleşmediğini algılar. Yeni model yapısıyla eşleşecek şekilde veritabanını otomatik olarak yeniden oluşturur ve veritabanını örnek filmlerle doldurur:

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın. Bir derecelendirme ekleyebileceğinizi unutmayın.

[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)

**Oluştur**'a tıklayın. Yeni film, derecelendirme de dahil, artık filmler listesinde görüntülenir:

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

Bu bölümde, model nesnelerini nasıl değiştirebileceğiniz ve veritabanını değişikliklerle eşitlenmiş halde tutan bir şekilde gördünüz. Ayrıca, senaryoları deneyebilmeniz için yeni oluşturulan bir veritabanını örnek verilerle doldurmanın bir yolunu öğrenmiş olursunuz. Daha sonra model sınıflarına daha zengin doğrulama mantığı ekleme ve bazı iş kurallarının uygulanmasını sağlama konusuna bakalım.

> [!div class="step-by-step"]
> [Önceki](examining-the-edit-methods-and-edit-view.md)
> [İleri](adding-validation-to-the-model.md)
