---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: '7\. Bölüm: Ana sayfa oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598681"
---
# <a name="part-7-creating-the-main-page"></a>7\. Bölüm: Ana sayfa oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>Ana Sayfayı Oluşturma

Bu bölümde, ana uygulama sayfası oluşturacaksınız. Bu sayfa, yönetici sayfasından daha karmaşık olacaktır, bu nedenle bunu çeşitli adımlarda yaklaşıyoruz. Bu şekilde, daha gelişmiş altını gizleme. js tekniklerini görürsünüz. Sayfanın temel düzeni aşağıda verilmiştir:

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- "Ürünler" bir ürün dizisini tutar.
- "Sepet" miktarları olan bir ürün dizisini tutar. "Sepete Ekle" seçeneğine tıkladığınızda sepette güncelleştirme yapılır.
- "Siparişler" bir sıra kimliği dizisi içerir.
- "Ayrıntılar", bir dizi öğe olan (miktarları olan ürünler) bir sıra ayrıntısı tutar

HTML 'de veri bağlama veya betik olmadan bazı temel düzenleri tanımlayarak başlayacağız. Views/Home/Index. cshtml dosyasını açın ve tüm içeriği şu şekilde değiştirin:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

Sonra, bir komut dosyası bölümü ekleyin ve boş bir görünüm modeli oluşturun:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

Daha önce tasarım taslağı temel alınarak, görünüm modeliniz ürünler, sepet, siparişler ve Ayrıntılar için gözlemlenenler gerektirir. `AppViewModel` nesnesine aşağıdaki değişkenleri ekleyin:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

Kullanıcılar ürünler listesinden sepete öğeler ekleyebilir ve sepetten öğeleri kaldırabilir. Bu işlevleri kapsüllemek için, bir ürünü temsil eden başka bir görünüm modeli sınıfı oluşturacağız. Aşağıdaki kodu `AppViewModel`ekleyin:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

`ProductViewModel` sınıfı, ürünü sepet içine ve sepetinden taşımak için kullanılan iki işlevi içerir: `addItemToCart` bir ürünün bir birimini sepete ekler ve `removeAllFromCart` ürünün tüm miktarlarını kaldırır.

Kullanıcılar mevcut bir siparişi seçebilir ve sipariş ayrıntılarını alabilir. Bu işlevi başka bir görünüm modelinde kapsülliyoruz:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel` bir siparişle başlatılır ve sunucuya bir AJAX isteği göndererek sipariş ayrıntılarını getirir.

Ayrıca, `OrderDetailsViewModel``total` özelliğine de dikkat edin. Bu özellik, [hesaplanan observable](http://knockoutjs.com/documentation/computedObservables.html)adlı özel bir observable türüdür. Adından da anlaşılacağı gibi, hesaplanan bir observable, bu durumda, siparişin toplam maliyeti olan&#8212;bir hesaplanan değere veri bağlamanıza olanak tanır.

Sonra şu işlevleri `AppViewModel`ekleyin:

- `resetCart` tüm öğeleri sepetten kaldırır.
- `getDetails` bir siparişin ayrıntılarını alır (`details` listesine yeni bir `OrderDetailsViewModel` göndererek).
- `createOrder` yeni bir sipariş oluşturur ve sepeti boşaltır.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

Son olarak, ürünler ve siparişler için AJAX istekleri yaparak görünüm modelini başlatın:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

Daha fazla kod olan Tamam, ancak adım adım bir adım geliştirdik, bu sayede tasarımın açık olması gerekir. Artık HTML 'ye bazı altını gizleme. js bağlamaları ekleyebiliriz.

**Ürünler**

Ürün listesinin bağlamaları aşağıda verilmiştir:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

Bu, Products dizisinin üzerinde dolaşır ve adı ve fiyatı görüntüler. "Sıraya ekle" düğmesi yalnızca Kullanıcı oturum açtığında görünür.

"Sıraya ekle" düğmesi, ürünün `ProductViewModel` örneğindeki `addItemToCart` çağırır. Bu, altını gizleme. js ' nin iyi bir özelliğini gösterir: bir görünüm modeli diğer görünüm modellerini içerdiğinde, bağlamaları iç modele uygulayabilirsiniz. Bu örnekte, `foreach` içindeki bağlamalar `ProductViewModel` örneklerinin her birine uygulanır. Bu yaklaşım, tüm işlevleri tek bir görünüm modeline yerleştirmekten çok daha temizdir.

**Tin**

Sepetin bağlamaları aşağıda verilmiştir:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

Bu, sepet dizisinin üzerinde dolaşır ve adı, fiyatı ve miktarı görüntüler. "Kaldır" bağlantısının ve "sipariş oluştur" düğmesinin görünüm-model işlevlerine bağlandığını unutmayın.

**Siparişlerine**

Siparişler listesinin bağlamaları aşağıda verilmiştir:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

Bu, siparişlerin üzerinde dolaşır ve sipariş KIMLIĞINI gösterir. Bağlantıdaki tıklama olayı `getDetails` işlevine bağlıdır.

**Sipariş Ayrıntıları**

Sıra ayrıntılarının bağlamaları aşağıda verilmiştir:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

Bu, siparişteki öğeleri yineler ve ürünü, fiyatı ve miktarı görüntüler. Çevreleyen div yalnızca details dizisi bir veya daha fazla öğe içeriyorsa görünür.

## <a name="conclusion"></a>Sonuç

Bu öğreticide, veritabanıyla iletişim kurmak için Entity Framework kullanan bir uygulama oluşturdunuz ve veri katmanının en üstünde herkese açık bir arabirim sağlamak için ASP.NET Web API 'SI. HTML sayfalarını işlemek için ASP.NET MVC 4, sayfa yeniden yüklemeye gerek kalmadan dinamik etkileşimler sağlamak için de altını gizleme. js ' yi kullanırız.

Ek kaynaklar:

- [ASP.NET veri erişimi Içerik Haritası](https://msdn.microsoft.com/library/6759sth4.aspx)
- [Entity Framework Geliştirici Merkezi](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [Öncekini](using-web-api-with-entity-framework-part-6.md)
