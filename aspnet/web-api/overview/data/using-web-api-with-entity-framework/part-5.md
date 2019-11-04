---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Veri Aktarımı nesneleri oluşturma (DTOs) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445754"
---
# <a name="create-data-transfer-objects-dtos"></a>Veri Aktarımı Nesneleri (DTO) Oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Şu anda Web API 'imiz, veritabanı varlıklarını istemciye kullanıma sunuyor. İstemci doğrudan veritabanı tablolarınıza eşleyen verileri alır. Bununla birlikte, her zaman iyi bir fikir değildir. Bazen istemciye göndereceğiniz verilerin şeklini değiştirmek isteyebilirsiniz. Örneğin, şunları yapmak isteyebilirsiniz:

- Döngüsel başvuruları Kaldır (önceki bölüme bakın).
- İstemcilerin görüntülemesi beklenen belirli özellikleri gizleyin.
- Yük boyutunu azaltmak için bazı özellikleri atlayın.
- İstemcilere daha uygun hale getirmek için iç içe geçmiş nesneler içeren nesne grafiklerini düzleştirin.
- "Aşırı gönderme" güvenlik açıklarını önleyin. (Bkz. Yük nakli hakkında bir tartışma için [model doğrulama](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) .)
- Hizmet katmanınızı veritabanı katmanınızdan ayırın.

Bunu gerçekleştirmek için bir *veri aktarımı nesnesi* (DTO) tanımlayabilirsiniz. Bir DTO, verilerin ağ üzerinden nasıl gönderileceğini tanımlayan bir nesnedir. Bunun, kitap varlığıyla nasıl çalıştığını görelim. Modeller klasöründe, iki DTO sınıfı ekleyin:

[!code-csharp[Main](part-5/samples/sample1.cs)]

`BookDetailDto` sınıfı, kitabın yazar adını tutan bir dize olması `AuthorName` dışında, kitap modelindeki tüm özellikleri içerir. `BookDto` sınıfı `BookDetailDto`bir özellikler alt kümesini içerir.

Sonra, `BooksController` sınıfındaki iki GET yöntemini DTOs döndüren sürümlerle değiştirin. Kitap varlıklarından DTOs 'a dönüştürmek için LINQ **Select** ifadesini kullanacağız.

[!code-csharp[Main](part-5/samples/sample2.cs)]

Yeni `GetBooks` yöntemi tarafından oluşturulan SQL aşağıda verilmiştir. EF 'in LINQ **seçimini** BIR SQL SELECT ifadesine dönüştürdüğünde emin olabilirsiniz.

[!code-sql[Main](part-5/samples/sample3.sql)]

Son olarak, `PostBook` yöntemini bir DTO döndürecek şekilde değiştirin.

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> Bu öğreticide, kodda el ile DTOs 'a dönüştürüyoruz. Diğer bir seçenek de, dönüştürmeyi otomatik olarak işleyen [Automaber](http://automapper.org/) gibi bir kitaplık kullanmaktır.
> 
> [!div class="step-by-step"]
> [Önceki](part-4.md)
> [İleri](part-6.md)
