---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Veri aktarımı nesneleri (Dto) oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 1af29955e8040c34840d4c77fc2006f59d2324dd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59395283"
---
# <a name="create-data-transfer-objects-dtos"></a>Veri Aktarımı Nesneleri (DTO) Oluşturma

tarafından [Mike Wasson](https://github.com/MikeWasson)

[Projeyi yükle](https://github.com/MikeWasson/BookService)

Sağ istemciye veritabanı varlıklarını şimdi web API kullanıma sunar. İstemci, doğrudan veritabanı tablolarına eşleyen veri alır. Ancak, her zaman iyi bir fikir değildir. Bazen istemciye göndermek veri şeklini değiştirmek istiyorsunuz. Örneğin, aşağıdakileri yapabilirsiniz:

- Döngüsel başvurular (önceki bölüme bakın) kaldırın.
- İstemciler görüntülemek için görmemesi belirli özellikleri gizleyin.
- Yükü boyutunu azaltmak için bazı özellikler atlayın.
- İstemciler için daha kullanışlı hale getirmek için iç içe geçmiş nesneleri içeren nesne grafiklerini düzleştirin.
- "Güvenlik açıklarını aşırı gönderme" kaçının. (Bkz [Model doğrulama](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) fazla posta hakkında ayrıntılı bilgi için.)
- Veritabanı katmanı, hizmet katmanından ayırırsınız.

Bunu gerçekleştirmek için tanımlayabileceğiniz bir *veri aktarımı nesnesi* (DTO). Bir DTO verileri ağ üzerinden nasıl gönderilir tanımlayan bir nesnedir. Kitap varlığı ile nasıl çalıştığına bakalım. Modeller klasörü içinde iki DTO sınıfı ekleyin:

[!code-csharp[Main](part-5/samples/sample1.cs)]

`BookDetailDTO` Sınıfı içeren kitap modelinden hariç tüm özellikler `AuthorName` yazar adını tutacak bir dizedir. `BookDTO` Sınıfı içeren bir alt kümesini özelliklerinden `BookDetailDTO`.

Ardından, iki GET yöntemleri yerine `BooksController` sınıfı sürümleriyle Dto döndürür. LINQ kullanacağız **seçin** Dto'lar kitap varlıklardan dönüştürülecek ifade.

[!code-csharp[Main](part-5/samples/sample2.cs)]

Yeni oluşturulan SQL işte `GetBooks` yöntemi. EF LINQ çevirir gördüğünüz **seçin** içine bir SQL SELECT deyimi.

[!code-sql[Main](part-5/samples/sample3.sql)]

Son olarak, değişiklik `PostBook` yöntemi bir DTO döndürür.

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> Bu öğreticide, biz Dto'lar için el ile kod dönüştürüyoruz. Gibi bir kitaplık kullanmak üzere başka bir seçenektir [AutoMapper](http://automapper.org/) dönüştürme otomatik olarak işler.
> 
> [!div class="step-by-step"]
> [Önceki](part-4.md)
> [İleri](part-6.md)
