---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Model ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 0d926c7a8bd99c56820208921c10e609da56d236
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519043"
---
# <a name="adding-a-model"></a>Model Ekleme

[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından

[!INCLUDE [Tutorial Note](index.md)]

Bu bölümde, bir veritabanında film yönetmeye yönelik bazı sınıflar ekleyeceksiniz. Bu sınıflar, ASP.NET MVC uygulamasının bir parçası&quot; &quot;modeli olacaktır.

Bu model sınıflarını tanımlamak ve bunlarla çalışmak için [Entity Framework](https://docs.microsoft.com/ef/) olarak bilinen .NET Framework veri erişim teknolojisini kullanacaksınız. Entity Framework (genellikle EF olarak adlandırılır) *Code First*adlı bir geliştirme paradigmasını destekler. Code First basit sınıflar yazarak model nesneleri oluşturmanızı sağlar. (Bunlar ayrıca, &quot;düz eski CLR nesnelerinden POCO sınıfları olarak da bilinir.&quot;) Daha sonra veritabanı, çok temiz ve hızlı bir geliştirme iş akışını sağlayan sınıflarınızda anında oluşturulmuş olabilir. Önce veritabanını oluşturmanız gerekiyorsa, MVC ve EF uygulama geliştirme hakkında bilgi edinmek için bu öğreticiyi izleyebilirsiniz. Daha sonra veritabanı ilk yaklaşımını kapsayan Tom Fizmakens [ASP.net Scafkatlama](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) öğreticisini izleyebilirsiniz.

## <a name="adding-model-classes"></a>Model sınıfları ekleme

**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.

![](adding-a-model/_static/image1.png)

Film&quot;&quot;*sınıf* adını girin.

Aşağıdaki beş özelliği `Movie` sınıfına ekleyin:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Bir veritabanındaki filmleri göstermek için `Movie` sınıfını kullanacağız. Bir `Movie` nesnesinin her örneği, bir veritabanı tablosundaki bir satıra karşılık gelir ve `Movie` sınıfının her özelliği tablodaki bir sütunla eşlenir.

Note: System. Data. Entity ve ilgili sınıfı kullanabilmek için [Entity Framework NuGet paketini](https://www.nuget.org/packages/EntityFramework/)yüklemeniz gerekir. Daha fazla yönerge için bağlantıyı izleyin.

Aynı dosyada, aşağıdaki `MovieDBContext` sınıfını ekleyin:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext` sınıfı, bir veritabanında `Movie` sınıf örneklerinin getirmeyi, depolanmasını ve güncelleştirilmesini işleyen Entity Framework film veritabanı bağlamını temsil eder. `MovieDBContext`, Entity Framework tarafından belirtilen `DbContext` taban sınıftan türetilir.

`DbContext` ve `DbSet`başvuramayacak şekilde, dosyanın en üstüne aşağıdaki `using` ifadesini eklemeniz gerekir:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Bunu using ifadesini el ile ekleyerek yapabilir veya kırmızı dalgalı çizgilerin üzerine geldiğinizde `Show potential fixes` ' a ve `using System.Data.Entity;` ' a tıklayabilirsiniz.

![](adding-a-model/_static/image2.png)

Note: kullanılmamış bazı `using` deyimleri kaldırılmıştır. Visual Studio, kullanılmayan bağımlılıkları gri olarak gösterecektir. Kullanılmayan bağımlılıkları gri bağımlılıklara göre kaldırıp `Show potential fixes` ' a ve kullanılmayan kullanımları Kaldır ' a tıklayabilirsiniz **.**

![](adding-a-model/_static/image3.png)

Son olarak bir model ekledik (MVC 'de d). Sonraki bölümde, veritabanı bağlantı dizesiyle çalışacaksınız.

> [!div class="step-by-step"]
> [Önceki](adding-a-view.md)
> [İleri](creating-a-connection-string.md)
