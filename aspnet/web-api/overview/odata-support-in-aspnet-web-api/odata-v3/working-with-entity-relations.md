---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: OData v3 'de Web API 2 ile varlık Ilişkilerini destekleme | Microsoft Docs
author: MikeWasson
description: 'Çoğu veri kümesi varlıklar arasındaki ilişkileri tanımlar: müşterilerin siparişleri vardır; Kitaplar yazar. ürünlerin tedarikçileri vardır. OData kullanarak, istemciler üzerinde gezinerişebilir...'
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600307"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a>OData v3 'de Web API 2 ile varlık Ilişkilerini destekleme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> Çoğu veri kümesi varlıklar arasındaki ilişkileri tanımlar: müşterilerin siparişleri vardır; Kitaplar yazar. ürünlerin tedarikçileri vardır. OData kullanarak, istemciler varlık ilişkilerine gidebilir. Bir ürün verildiğinde, tedarikçiyi bulabilirsiniz. Ayrıca ilişkiler oluşturabilir veya kaldırabilirsiniz. Örneğin, tedarikçiyi bir ürün için ayarlayabilirsiniz.
> 
> Bu öğreticide, ASP.NET Web API 'sinde bu işlemleri nasıl destekleyeceği gösterilmektedir. Öğretici, [Web API 2 Ile OData v3 uç noktası oluşturma](creating-an-odata-endpoint.md)öğreticisinde oluşturulur.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Web API 2
> - OData sürüm 3
> - Entity Framework 6

## <a name="add-a-supplier-entity"></a>Tedarikçi varlığı ekleme

İlk olarak OData akışınıza yeni bir varlık türü eklememiz gerekiyor. `Supplier` sınıfı ekleyeceğiz.

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

Bu sınıf, varlık anahtarı için bir dize kullanır. Uygulamada, bir tamsayı anahtar kullanmaktan daha az ortak olabilir. Ancak, OData 'in diğer anahtar türlerini tamsayıların yanı sıra nasıl işleyeceğini de öğrenecektir.

Sonra, `Product` sınıfına bir `Supplier` özelliği ekleyerek bir ilişki oluşturacağız:

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

`ProductServiceContext` sınıfına yeni bir **Dbset** ekleyin, böylece Entity Framework `Supplier` tablosunu veritabanına dahil eder.

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

WebApiConfig.cs ' de, EDM modeline bir "Suppliers" varlığı ekleyin:

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a>Gezinti özellikleri

Bir ürünün tedarikçilerini almak için istemci bir GET isteği gönderir:

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

Burada "Tedarikçi" `Product` türünde bir gezinti özelliğidir. Bu durumda `Supplier` tek bir öğe anlamına gelir, ancak bir gezinti özelliği de bir koleksiyon (bire çok veya çoktan çoğa ilişki) döndürebilir.

Bu isteği desteklemek için, `ProductsController` sınıfına aşağıdaki yöntemi ekleyin:

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

*Anahtar* parametresi ürünün anahtarıdır. Yöntemi bu durumda bir `Supplier` örneği&#8212;olan ilgili varlığı döndürür. Yöntem adı ve parametre adı her ikisi de önemlidir. Genel olarak, gezinti özelliği "X" olarak adlandırılmışsa, "GetX" adlı bir yöntem eklemeniz gerekir. Yöntem, üst öğenin anahtarının veri türüyle eşleşen "*Key*" adlı bir parametre almalıdır.

*Anahtar* parametresine **[Fromodatauri]** özniteliğini eklemek de önemlidir. Bu öznitelik, Web API 'sini istek URI 'sinden anahtar ayrıştırdığında OData sözdizimi kurallarını kullanmasını söyler.

## <a name="creating-and-deleting-links"></a>Bağlantı oluşturma ve silme

OData iki varlık arasında ilişki oluşturmayı veya kaldırmayı destekler. OData terminolojisinde ilişki bir "bağlantıdır". Her bağlantının *varlık*/$Links/*varlık*biçiminde bir URI 'si vardır. Örneğin, üründen tedarikçiye bağlantı şu şekilde görünür:

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

Yeni bir bağlantı oluşturmak için, istemci bağlantı URI 'sine bir POST isteği gönderir. İsteğin gövdesi, hedef varlığın URI 'sidir. Örneğin, "CTSO" anahtarına sahip bir tedarikçi olduğunu varsayalım. "Product (1)" öğesinden "tedarikçisine (' CTSO ')" bir bağlantı oluşturmak için, istemci aşağıdakine benzer bir istek gönderir:

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

Bir bağlantıyı silmek için, istemci bağlantı URI 'sine bir DELETE isteği gönderir.

**Bağlantı oluşturma**

Bir istemcinin ürün-tedarikçi bağlantıları oluşturmasını sağlamak için, `ProductsController` sınıfına aşağıdaki kodu ekleyin:

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

Bu yöntem üç parametre alır:

- *anahtar*: ana varlığa yönelik anahtar (ürün)
- *NavigationProperty*: Gezinti özelliğinin adı. Bu örnekte, geçerli olan tek gezinti özelliği "Tedarikçi" dir.
- *bağlantı*: Ilgili varlığın OData URI 'si. Bu değer, istek gövdesinden alınır. Örneğin, bağlantı URI 'SI "`http://localhost/odata/Suppliers('CTSO')`, yani, ID = ' CTSO ' olan tedarikçide olabilir.

Yöntemi, tedarikçiyi aramak için bağlantıyı kullanır. Eşleşen Tedarikçi bulunursa, yöntemi `Product.Supplier` özelliğini ayarlar ve sonucu veritabanına kaydeder.

En zor bölümü, bağlantı URI 'sini ayrıştırır. Temel olarak, bu URI 'ye bir GET isteği gönderme sonucunun benzetimini yapmanız gerekir. Aşağıdaki yardımcı yöntemi bunun nasıl yapılacağını gösterir. Yöntemi, Web API yönlendirme işlemini çağırır ve ayrıştırılmış OData yolunu temsil eden bir **ODataPath** örneğini geri alır. Bir bağlantı URI 'SI için segmentlerin biri varlık anahtarı olmalıdır. (Değilse, istemci hatalı bir URI gönderdi.)

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

**Bağlantılar siliniyor**

Bir bağlantıyı silmek için `ProductsController` sınıfına aşağıdaki kodu ekleyin:

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

Bu örnekte, gezinti özelliği tek bir `Supplier` varlıktır. Gezinti özelliği bir koleksiyon ise, bir bağlantıyı silmenin URI 'SI ilgili varlık için bir anahtar içermelidir. Örneğin:

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

Bu istek, müşteri 1 ' den sipariş 1 ' i kaldırır. Bu durumda, DeleteLink yöntemi aşağıdaki imzaya sahip olacaktır:

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

*RelatedKey* parametresi ilgili varlık için anahtarı verir. Bu nedenle `DeleteLink` yönteminde, *anahtar* parametresine göre birincil varlığı bulun, *RelatedKey* parametresiyle ilgili varlığı bulun ve ardından ilişkilendirmeyi kaldırın. Veri modelinize bağlı olarak her iki `DeleteLink`sürümünü de uygulamanız gerekebilir. Web API 'SI, istek URI 'sine bağlı olarak doğru sürümü çağırır.
