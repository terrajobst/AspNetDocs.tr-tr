---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: OData v4 'de ASP.NET Web API 2,2 kullanılarak varlık Ilişkileri | Microsoft Docs
author: MikeWasson
description: 'Çoğu veri kümesi varlıklar arasındaki ilişkileri tanımlar: müşterilerin siparişleri vardır; Kitaplar yazar. ürünlerin tedarikçileri vardır. OData kullanarak, istemciler üzerinde gezinerişebilir...'
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598695"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>ASP.NET Web API 2,2 kullanarak OData v4 'de varlık Ilişkileri

, [Mike te son](https://github.com/MikeWasson)

> Çoğu veri kümesi varlıklar arasındaki ilişkileri tanımlar: müşterilerin siparişleri vardır; Kitaplar yazar. ürünlerin tedarikçileri vardır. OData kullanarak, istemciler varlık ilişkilerine gidebilir. Bir ürün verildiğinde, tedarikçiyi bulabilirsiniz. Ayrıca ilişkiler oluşturabilir veya kaldırabilirsiniz. Örneğin, tedarikçiyi bir ürün için ayarlayabilirsiniz.
>
> Bu öğreticide, ASP.NET Web API kullanılarak OData v4 'de bu işlemlerin nasıl destekleyeceği gösterilmektedir. Öğretici, [ASP.NET Web API 2 kullanarak bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md)öğreticisinde derleme oluşturur.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
> - Web API 2.1
> - OData v4
> - Visual Studio 2013 (Visual Studio 2017 'yi [buraya](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)indirin)
> - Entity Framework 6
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>Öğretici sürümleri
>
> OData sürüm 3 için bkz. [OData v3 'de varlık Ilişkilerini destekleme](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).

## <a name="add-a-supplier-entity"></a>Tedarikçi varlığı ekleme

> [!NOTE]
> Öğretici, [ASP.NET Web API 2 kullanarak bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md)öğreticisinde derleme oluşturur.

İlk olarak, ilgili bir varlığına ihtiyacımız var. Modeller klasörüne `Supplier` adlı bir sınıf ekleyin.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

`Product` sınıfına bir gezinti özelliği ekleyin:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

`ProductsContext` sınıfına yeni bir **Dbset** ekleyin, böylece Entity Framework tedarikçinin tablosunu veritabanına dahil eder.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

WebApiConfig.cs ' de, varlık veri modeline ayarlanmış bir &quot;Suppliers&quot; varlık ekleyin:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>Bir tedarikçiler denetleyicisi ekleme

Controllers klasörüne bir `SuppliersController` sınıfı ekleyin.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

Bu denetleyiciye CRUD işlemlerinin nasıl ekleneceğini göstermiyorum. Adımlar, ürünler denetleyicisi ile aynıdır (bkz. [OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md)).

## <a name="getting-related-entities"></a>Ilgili varlıkları alma

Bir ürünün tedarikçilerini almak için istemci bir GET isteği gönderir:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

Bu isteği desteklemek için, `ProductsController` sınıfına aşağıdaki yöntemi ekleyin:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

Bu yöntem varsayılan adlandırma kuralını kullanır

- Yöntem adı: GetX, burada X, gezinti özelliğidir.
- Parametre adı: *anahtar*

Bu adlandırma kuralını izlerseniz, Web API 'SI, HTTP isteğini denetleyici yöntemiyle otomatik olarak eşler.

Örnek HTTP isteği:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

Örnek HTTP yanıtı:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>İlişkili bir koleksiyon alınıyor

Önceki örnekte, bir ürünün bir tedarikçisi vardır. Bir gezinti özelliği de bir koleksiyonu döndürebilir. Aşağıdaki kod, bir tedarikçinin ürünlerini alır:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

Bu durumda, yöntemi **SingleResult&lt;t** yerine bir **ıqueryable** döndürür&gt;

Örnek HTTP isteği:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

Örnek HTTP yanıtı:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>Varlıklar arasında Ilişki oluşturma

OData, mevcut iki varlık arasında ilişki oluşturmayı veya kaldırmayı destekler. OData v4 terminolojisinde, ilişki&quot;bir &quot;başvurudur. (OData v3 'de ilişkiye bir *bağlantı*adı verilir. Protokol farkları Bu öğreticiye göre farklılık görmez.)

Bir başvurunun, `/Entity/NavigationProperty/$ref`form ile kendi URI 'SI vardır. Örneğin, bir ürün ve tedarikçiyle ilgili başvurunun ele aldığı URI aşağıda verilmiştir:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

İstemci bir ilişki eklemek için bu adrese bir POST veya PUT isteği gönderir.

- Gezinti özelliği `Product.Supplier`gibi tek bir varlık ise koyun.
- Gezinti özelliği `Supplier.Products`gibi bir koleksiyon ise, gönder.

İsteğin gövdesi, ilişkide diğer varlığın URI 'sini içerir. Örnek bir istek aşağıda verilmiştir:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

Bu örnekte, istemci, KIMLIK = 6 olan ürün `Supplier` için $ref URI 'si olan `/Products(6)/Supplier/$ref`için bir PUT isteği gönderir. İstek başarılı olursa, sunucu bir 204 (Içerik yok) yanıtı gönderir:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

`Product`bir ilişki eklemek için denetleyici yöntemi aşağıda verilmiştir:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

*NavigationProperty* parametresi ayarlanacak ilişkiyi belirtir. (Varlıkta birden fazla gezinti özelliği varsa, daha fazla `case` deyimi ekleyebilirsiniz.)

*Bağlantı* parametresi, tedarikçinin URI 'sini içerir. Web API 'SI, bu parametrenin değerini almak için istek gövdesini otomatik olarak ayrıştırır.

Tedarikçiyi aramak için, *bağlantı* parametresinin bir PARÇASı olan kimliğe (veya anahtara) ihtiyacımız var. Bunu yapmak için aşağıdaki yardımcı yöntemi kullanın:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

Temelde, bu yöntem, URI yolunu kesimlere bölmek için OData kitaplığını kullanır, anahtarı içeren segmenti bulur ve anahtarı doğru türe dönüştürür.

## <a name="deleting-a-relationship-between-entities"></a>Varlıklar arasındaki Ilişkiyi silme

İstemci bir ilişkiyi silmek için $ref URI 'sine bir HTTP DELETE isteği gönderir:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

Bir ürün ve tedarikçi arasındaki ilişkiyi silmek için denetleyici yöntemi aşağıda verilmiştir:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

Bu durumda `Product.Supplier`, 1 ' den fazla ilişkinin &quot;1&quot; sonuna kadar olan, `null``Product.Supplier` ayarlayarak ilişkiyi kaldırabilirsiniz.

Bir ilişkinin &quot;çok&quot; sonunda, istemci hangi ilgili varlığın kaldırılacağını belirtmelidir. Bunu yapmak için istemci, isteğin sorgu dizesinde ilgili varlığın URI 'sini gönderir. Örneğin, "Product 1" öğesini "Tedarikçi 1" öğesinden kaldırmak için:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

Web API 'de bunu desteklemek için `DeleteRef` metoduna fazladan bir parametre dahil etmemiz gerekir. Bir ürünü `Supplier.Products` ilişkisinden kaldırmak için denetleyici yöntemi aşağıda verilmiştir.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

*Anahtar* parametresi, tedarikçinin anahtarıdır ve *relatedkey* parametresi, `Products` ilişkisinden kaldırılacak ürünün anahtarıdır. Web API 'sinin anahtarı otomatik olarak sorgu dizesinden aldığından emin olmanız gerektiğini unutmayın.
