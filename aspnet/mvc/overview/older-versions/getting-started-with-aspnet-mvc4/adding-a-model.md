---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: Model ekleme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457810"
---
# <a name="adding-a-model"></a>Model Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.

Bu bölümde, bir veritabanında film yönetmeye yönelik bazı sınıflar ekleyeceksiniz. Bu sınıflar, ASP.NET MVC uygulamasının bir parçası&quot; &quot;modeli olacaktır.

Bu model sınıflarını tanımlamak ve bunlarla çalışmak için [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) olarak bilinen .NET Framework veri erişim teknolojisini kullanacaksınız. Entity Framework (genellikle EF olarak adlandırılır) *Code First*adlı bir geliştirme paradigmasını destekler. Code First basit sınıflar yazarak model nesneleri oluşturmanızı sağlar. (Bunlar ayrıca, &quot;düz eski CLR nesnelerinden POCO sınıfları olarak da bilinir.&quot;) Daha sonra veritabanı, çok temiz ve hızlı bir geliştirme iş akışını sağlayan sınıflarınızda anında oluşturulmuş olabilir.

## <a name="adding-model-classes"></a>Model sınıfları ekleme

**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.

![](adding-a-model/_static/image1.png)

Film&quot;&quot;*sınıf* adını girin.

Aşağıdaki beş özelliği `Movie` sınıfına ekleyin:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Bir veritabanındaki filmleri göstermek için `Movie` sınıfını kullanacağız. Bir `Movie` nesnesinin her örneği, bir veritabanı tablosundaki bir satıra karşılık gelir ve `Movie` sınıfının her özelliği tablodaki bir sütunla eşlenir.

Aynı dosyada, aşağıdaki `MovieDBContext` sınıfını ekleyin:

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` sınıfı, bir veritabanında `Movie` sınıf örneklerinin getirmeyi, depolanmasını ve güncelleştirilmesini işleyen Entity Framework film veritabanı bağlamını temsil eder. `MovieDBContext`, Entity Framework tarafından belirtilen `DbContext` taban sınıftan türetilir.

`DbContext` ve `DbSet`başvuramayacak şekilde, dosyanın en üstüne aşağıdaki `using` ifadesini eklemeniz gerekir:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Tamamlanmış *Movie.cs* dosyası aşağıda gösterilmiştir. (Gerekmeyen bazı using deyimleri kaldırılmıştır.)

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Bağlantı Dizesi Oluşturma ve SQL Server LocalDB ile Çalışma

Oluşturduğunuz `MovieDBContext` sınıf veritabanına bağlanma ve `Movie` nesneleri veritabanı kayıtlarına eşleme görevini işler. Tek bir soru sorabilirsiniz, ancak hangi veritabanının bağlanacağı de bu şekilde belirlenir. Bunu, uygulamanın *Web. config* dosyasına bağlantı bilgilerini ekleyerek yapabilirsiniz.

Uygulama kök *Web. config* dosyasını açın. ( *Görünümler* klasöründeki *Web. config* dosyası değil.) Kırmızı renkle özetlenen *Web. config* dosyasını açın.

![](adding-a-model/_static/image2.png)

Aşağıdaki bağlantı dizesini *Web. config* dosyasındaki `<connectionStrings>` öğesine ekleyin.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

Aşağıdaki örnek, *Web. config* dosyasının yeni bağlantı dizesi eklenmiş bir bölümünü gösterir:

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

Bu küçük miktarda kod ve XML, film verilerini göstermek ve bir veritabanında depolamak için yazmanız gereken her şey vardır.

Daha sonra, film verilerini göstermek ve kullanıcıların yeni film listeleri oluşturmasına izin vermek için kullanabileceğiniz yeni bir `MoviesController` sınıfı oluşturacaksınız.

> [!div class="step-by-step"]
> [Önceki](adding-a-view.md)
> [İleri](accessing-your-models-data-from-a-controller.md)
