---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API 'SI ile OData v4 'de açık türler | Microsoft Docs
author: microsoft
description: OData v4 'de, açık bir tür, tür tanımında belirtilen özelliklerin yanı sıra dinamik özellikler içeren yapısal bir türdür. Aç...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622180"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API ile OData v4 'de açık türler

[Microsoft](https://github.com/microsoft) tarafından

> OData v4 'de, *açık bir tür* , tür tanımında belirtilen özelliklerin yanı sıra dinamik özellikler içeren yapısal bir türdür. Açık türler, veri modellerinize esneklik eklemenizi sağlar. Bu öğreticide, ASP.NET Web API OData 'de açık türlerin nasıl kullanılacağı gösterilmektedir.
> 
> Bu öğreticide, ASP.NET Web API 'sinde bir OData uç noktası oluşturmayı bildiğiniz varsayılmaktadır. Aksi takdirde, okumaya başlamak için önce [bir OData v4 uç noktası oluşturun](create-an-odata-v4-endpoint.md) .
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Web API OData 5,3
> - OData v4

Birincisi, bazı OData terminolojisi:

- Varlık türü: anahtarı olan yapılandırılmış bir tür.
- Karmaşık tür: anahtar içermeyen yapılandırılmış bir tür.
- Açık tür: dinamik özelliklere sahip bir tür. Hem varlık türleri hem de karmaşık türler açık olabilir.

Dinamik bir özelliğin değeri basit bir tür, karmaşık tür veya numaralandırma türü olabilir; ya da bu türlerden birinin bir koleksiyonu. Açık türler hakkında daha fazla bilgi için bkz. [OData v4 belirtimi](http://www.odata.org/documentation/odata-version-4-0/).

## <a name="install-the-web-odata-libraries"></a>Web OData kitaplıklarını yükler

En son Web API OData kitaplıklarını yüklemek için NuGet Paket Yöneticisi 'Ni kullanın. Paket Yöneticisi konsol penceresinde:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>CLR türlerini tanımlama

EDM modellerini CLR türleri olarak tanımlayarak başlayın.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Varlık Veri Modeli (EDM) oluşturulduğunda,

- `Category` bir sabit listesi türüdür.
- `Address` karmaşık bir türdür. (Bir anahtarı yoktur, bu nedenle bir varlık türü değildir.)
- `Customer` bir varlık türüdür. (Bir anahtarı vardır.)
- `Press` açık bir karmaşık türdür.
- `Book` açık bir varlık türüdür.

Açık bir tür oluşturmak için CLR türünün, dinamik özellikleri tutan `IDictionary<string, object>`türünde bir özelliği olmalıdır.

## <a name="build-the-edm-model"></a>EDM modelini oluşturma

EDM 'yi oluşturmak için **ODataConventionModelBuilder** kullanıyorsanız, `Press` ve `Book`, bir `IDictionary<string, object>` özelliğinin varlığına göre otomatik olarak açık türler olarak eklenir.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Ayrıca, **ODataModelBuilder**kullanarak EDM 'yi açıkça de oluşturabilirsiniz.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>OData denetleyicisi ekleme

Ardından, bir OData denetleyicisi ekleyin. Bu öğreticide, yalnızca GET ve POST isteklerini destekleyen ve varlıkları depolamak için bellek içi bir liste kullanan Basitleştirilmiş bir denetleyici kullanacağız.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

İlk `Book` örneğinin dinamik özellikleri olmadığına dikkat edin. İkinci `Book` örneği aşağıdaki dinamik özelliklere sahiptir:

- "Yayımlandı": temel tür
- "Yazarlar": temel türlerin koleksiyonu
- "Diğer kategoriler": sabit listesi türleri koleksiyonu.

Ayrıca, bu `Book` örneğinin `Press` özelliği aşağıdaki dinamik özelliklere sahiptir:

- "Blog": temel tür
- "Adres": karmaşık tür

## <a name="query-the-metadata"></a>Meta verileri sorgulama

OData meta veri belgesini almak için `~/$metadata`için bir GET isteği gönderin. Yanıt gövdesi şuna benzer görünmelidir:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

Meta veri belgesinden şunları görebilirsiniz:

- `Book` ve `Press` türleri için `OpenType` özniteliğinin değeri true 'dur. `Customer` ve `Address` türlerinde bu öznitelik yok.
- `Book` varlık türü üç tanımlı özelliğe sahiptir: ıSBN, title ve Press. OData meta verileri CLR sınıfından `Book.Properties` özelliğini içermez.
- Benzer şekilde, `Press` karmaşık tür yalnızca iki tane tanımlanmış özelliğe sahiptir: ad ve kategori. Meta veriler CLR sınıfından `Press.DynamicProperties` özelliğini içermez.

## <a name="query-an-entity"></a>Bir varlığı sorgulama

ISBN ile "978-0-7356-7942-9" değerine eşit olan kitabı almak için `~/Books('978-0-7356-7942-9')`için bir GET isteği gönderin. Yanıt gövdesi şuna benzer olmalıdır. (Daha okunaklı olması için girintilenir.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Dinamik özelliklerin, belirtilen özelliklerle birlikte satır içine dahil edildiğini unutmayın.

## <a name="post-an-entity"></a>Bir varlık GÖNDERIN

Bir kitap varlığı eklemek için `~/Books`bir POST isteği gönderin. İstemci, istek yükünde dinamik özellikleri ayarlayabilir.

Örnek bir istek aşağıda verilmiştir. "Price" ve "yayınlanan" özelliklerine göz önünde edin.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Denetleyici yönteminde bir kesme noktası ayarlarsanız, Web API 'sinin bu özellikleri `Properties` sözlüğüne eklediğine bakabilirsiniz.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Ek Kaynaklar

[OData açık türü örneği](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
