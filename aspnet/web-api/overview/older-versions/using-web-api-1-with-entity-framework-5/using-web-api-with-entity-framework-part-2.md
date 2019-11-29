---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: '2\. Bölüm: etki alanı modellerini oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600367"
---
# <a name="part-2-creating-the-domain-models"></a>2\. Bölüm: etki alanı modellerini oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>Model Ekle

Entity Framework yaklaşımın üç yolu vardır:

- Veritabanı-ilk: bir veritabanı ile başlar ve Entity Framework kodu oluşturur.
- Model-önce: bir görsel modelle başlar ve Entity Framework hem veritabanını hem de kodu oluşturur.
- Kod-önce: kodla başlar ve veritabanını Entity Framework oluşturur.

İlk kod yaklaşımı kullanıyoruz, bu nedenle etki alanı nesnelerimizi POCOs (düz-eski CLR nesneleri) olarak tanımlayarak başladık. Kod-ilk yaklaşımla, etki alanı nesneleri, işlemler veya kalıcılık gibi veritabanı katmanını desteklemek için ek kod gerektirmez. (Özellikle, [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) sınıfından devralması gerekmez.) Entity Framework veritabanı şemasını nasıl oluşturduğunu denetlemek için veri açıklamalarını kullanmaya devam edebilirsiniz.

POCOs, [veritabanı durumunu](https://msdn.microsoft.com/library/system.data.entitystate.aspx)tanımlayan ek özellikler taşımadığından, kolayca JSON veya XML olarak serileştirilir. Bununla birlikte, öğreticide daha sonra göreceğiniz gibi Entity Framework modellerinizi her zaman doğrudan istemcilere sunmalısınız.

Aşağıdaki POCOs 'ları oluşturacağız:

- Ürün
- Siparişi
- OrderDetail

Her bir sınıfı oluşturmak için Çözüm Gezgini modeller klasörüne sağ tıklayın. Bağlam menüsünden **Ekle** ' yi ve ardından sınıf ' ı seçin **.**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

Aşağıdaki uygulamayla bir `Product` sınıfı ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

Kural gereği, Entity Framework `Id` özelliğini birincil anahtar olarak kullanır ve veritabanını veritabanı tablosundaki bir kimlik sütunuyla eşler. Yeni bir `Product` örneği oluşturduğunuzda, veritabanı değeri oluşturduğundan `Id`için bir değer ayarlayamazsınız.

**ScaffoldColumn** özniteliği, ASP.NET MVC 'nin bir düzenleyici formu oluştururken `Id` özelliğini atlamasını söyler. **Gerekli** öznitelik, modeli doğrulamak için kullanılır. `Name` özelliğinin boş olmayan bir dize olması gerektiğini belirtir.

`Order` sınıfını ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

`OrderDetail` sınıfını ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>Yabancı anahtar Ilişkileri

Bir sipariş birçok sipariş ayrıntısı içerir ve her sipariş ayrıntısı tek bir ürüne başvurur. Bu ilişkileri göstermek için `OrderDetail` sınıfı `OrderId` ve `ProductId`adlı özellikleri tanımlar. Entity Framework, bu özelliklerin yabancı anahtarları temsil ettiğini ve veritabanına yabancı anahtar kısıtlamaları eklemesini sağlar.

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

`Order` ve `OrderDetail` sınıfları, ilişkili nesnelere başvurular içeren "gezinti" özelliklerini de içerir. Sipariş verildiğinde, gezinti özelliklerini izleyerek sırayla ürünlere gidebilirsiniz.

Projeyi şimdi derle. Entity Framework, modellerin özelliklerini saptamak için yansıma kullanır, bu nedenle veritabanı şemasını oluşturmak için derlenmiş bir bütünleştirilmiş kod gerektirir.

## <a name="configure-the-media-type-formatters"></a>Medya türü Formatlayıcıları yapılandırma

[Medya türü biçimlendirici](../../formats-and-model-binding/media-formatters.md) , Web API 'si http yanıt gövdesini yazdığında verilerinizi seri hale getirilen bir nesnedir. Yerleşik Biçimlendiriciler JSON ve XML çıkışını destekler. Varsayılan olarak, bu formatlayıcılara her ikisi de değere göre tüm nesneleri serileştirilir.

Değere göre serileştirme, bir nesne grafiğinde döngüsel başvurular varsa bir sorun oluşturur. Bu, `Order` ve `OrderDetail` sınıflarıyla tam olarak yapılır çünkü her biri birbirlerine bir başvuru içerir. Biçimlendirici başvuruları izler, her bir nesneyi değere göre yazıyor ve daireler içinde yer alır. Bu nedenle, varsayılan davranışı değiştirmemiz gerekiyor.

Çözüm Gezgini ' de, uygulama\_Başlat klasörünü genişletin ve WebApiConfig.cs adlı dosyayı açın. `WebApiConfig` sınıfına aşağıdaki kodu ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

Bu kod, nesne başvurularını korumak için JSON biçimlendirici olarak ayarlar ve XML biçimlendirici 'yi işlem hattından tamamen kaldırır. (XML biçimlendirici nesne başvurularını korumak için yapılandırabilirsiniz, ancak bu çok daha fazla çalışmalardır ve bu uygulama için yalnızca JSON gereklidir. Daha fazla bilgi için bkz. [Döngüsel nesne başvurularını işleme](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)

> [!div class="step-by-step"]
> [Önceki](using-web-api-with-entity-framework-part-1.md)
> [İleri](using-web-api-with-entity-framework-part-3.md)
