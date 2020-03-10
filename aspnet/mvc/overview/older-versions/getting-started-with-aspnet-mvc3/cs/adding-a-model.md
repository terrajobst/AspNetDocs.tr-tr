---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: Model ekleme (C#) | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a5f494eaa05bcfcd9d49873db728d71c1fd332c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540868"
---
# <a name="adding-a-model-c"></a>Model Ekleme (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Kaynak koduna sahip bir Visual Web C# Developer projesi, bu konuyla birlikte kullanılabilecek. [Sürümü C# indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/adding-a-model.md) geçin.

## <a name="adding-a-model"></a>Model Ekleme

Bu bölümde, bir veritabanında film yönetmeye yönelik bazı sınıflar ekleyeceksiniz. Bu sınıflar, ASP.NET MVC uygulamasının "model" bir parçası olacaktır.

Bu model sınıflarını tanımlamak ve bunlarla çalışmak için Entity Framework olarak bilinen .NET Framework veri erişim teknolojisini kullanacaksınız. Entity Framework (genellikle EF olarak adlandırılır) *Code First*adlı bir geliştirme paradigmasını destekler. Code First basit sınıflar yazarak model nesneleri oluşturmanızı sağlar. (Bunlar, "düz eski CLR nesnelerinden" POCO sınıfları olarak da bilinir.) Daha sonra veritabanı, çok temiz ve hızlı bir geliştirme iş akışını sağlayan sınıflarınızda anında oluşturulmuş olabilir.

## <a name="adding-model-classes"></a>Model sınıfları ekleme

**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.

![](adding-a-model/_static/image1.png)

*Sınıfı* "film" olarak adlandırın.

[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)

Aşağıdaki beş özelliği `Movie` sınıfına ekleyin:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Bir veritabanındaki filmleri göstermek için `Movie` sınıfını kullanacağız. Bir `Movie` nesnesinin her örneği, bir veritabanı tablosundaki bir satıra karşılık gelir ve `Movie` sınıfının her özelliği tablodaki bir sütunla eşlenir.

Aynı dosyada, aşağıdaki `MovieDBContext` sınıfını ekleyin:

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` sınıfı, bir veritabanında `Movie` sınıf örneklerinin getirmeyi, depolanmasını ve güncelleştirilmesini işleyen Entity Framework film veritabanı bağlamını temsil eder. `MovieDBContext`, Entity Framework tarafından belirtilen `DbContext` taban sınıftan türetilir. `DbContext` ve `DbSet`hakkında daha fazla bilgi için bkz. [Entity Framework Için üretkenlik iyileştirmeleri](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).

`DbContext` ve `DbSet`başvuramayacak şekilde, dosyanın en üstüne aşağıdaki `using` ifadesini eklemeniz gerekir:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Tamamlanmış *Movie.cs* dosyası aşağıda gösterilmiştir.

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>Bağlantı dizesi oluşturma ve SQL Server Compact çalışma

Oluşturduğunuz `MovieDBContext` sınıf veritabanına bağlanma ve `Movie` nesneleri veritabanı kayıtlarına eşleme görevini işler. Tek bir soru sorabilirsiniz, ancak hangi veritabanının bağlanacağı de bu şekilde belirlenir. Bunu, uygulamanın *Web. config* dosyasına bağlantı bilgilerini ekleyerek yapabilirsiniz.

Uygulama kök *Web. config* dosyasını açın. ( *Görünümler* klasöründeki *Web. config* dosyası değil.) Aşağıdaki görüntüde hem *Web. config* dosyaları gösterilmektedir; *Web. config* dosyasını daire içinde kırmızı olarak açın.

![](adding-a-model/_static/image4.png)

Aşağıdaki bağlantı dizesini *Web. config* dosyasındaki `<connectionStrings>` öğesine ekleyin.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

Aşağıdaki örnek, *Web. config* dosyasının yeni bağlantı dizesi eklenmiş bir bölümünü gösterir:

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

Bu küçük miktarda kod ve XML, film verilerini göstermek ve bir veritabanında depolamak için yazmanız gereken her şey vardır.

Daha sonra, film verilerini göstermek ve kullanıcıların yeni film listeleri oluşturmasına izin vermek için kullanabileceğiniz yeni bir `MoviesController` sınıfı oluşturacaksınız.

> [!div class="step-by-step"]
> [Önceki](adding-a-view.md)
> [İleri](accessing-your-models-data-from-a-controller.md)
