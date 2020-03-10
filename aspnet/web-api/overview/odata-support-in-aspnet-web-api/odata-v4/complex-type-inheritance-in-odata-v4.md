---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: OData v4 'de ASP.NET Web API 'SI ile karmaşık tür devralma | Microsoft Docs
author: microsoft
description: OData v4 belirtimine göre, karmaşık bir tür başka bir karmaşık türden devralınabilir. (Karmaşık tür, anahtar içermeyen yapılandırılmış bir türdür.) Web API 'SI...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556310"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>OData v4 'de ASP.NET Web API 'SI ile karmaşık tür devralma

[Microsoft](https://github.com/microsoft) tarafından

> OData v4 [belirtimine](http://www.odata.org/documentation/odata-version-4-0/)göre, karmaşık bir tür başka bir karmaşık türden devralınabilir. ( *Karmaşık* tür, anahtar içermeyen yapılandırılmış bir türdür.) Web API OData 5,3 karmaşık tür devralmayı destekler.
> 
> Bu konu, karmaşık devralma türleri ile bir varlık veri modeli (EDM) oluşturmayı gösterir. Tüm kaynak kodu için bkz. [OData karmaşık türü devralma örneği](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Web API OData 5,3
> - OData v4

## <a name="model-hierarchy"></a>Model hiyerarşisi

Karmaşık tür devralmayı göstermek için aşağıdaki sınıf hiyerarşisini kullanacağız.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape` soyut bir karmaşık türdür. `Rectangle`, `Triangle`ve `Circle` `Shape`türetilmiş karmaşık türlerdir ve `RoundRectangle` `Rectangle`türetilir. `Window` bir varlık türüdür ve bir `Shape` örneği içerir.

Bu türleri tanımlayan CLR sınıfları aşağıda verilmiştir.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>EDM modelini oluşturma

EDM 'yi oluşturmak için, CLR türlerindeki devralma ilişkilerini gösteren **ODataConventionModelBuilder**kullanabilirsiniz.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

Ayrıca, **ODataModelBuilder**kullanarak EDM 'yi açıkça de oluşturabilirsiniz. Bu daha fazla kod alır, ancak EDM üzerinde daha fazla denetim sağlar.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

Bu iki örnek aynı EDM şemasını oluşturur.

## <a name="metadata-document"></a>Meta veri belgesi

Karmaşık tür devralmayı gösteren OData meta veri belgesi aşağıda verilmiştir.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

Meta veri belgesinden şunları görebilirsiniz:

- `Shape` karmaşık tür soyuttur.
- `Rectangle`, `Triangle`ve `Circle` karmaşık türün temel türü `Shape`vardır.
- `RoundRectangle` türünün temel türü `Rectangle`vardır.

## <a name="casting-complex-types"></a>Karmaşık türleri atama

Karmaşık türlerde atama artık desteklenmektedir. Örneğin, aşağıdaki sorgu bir `Shape` `Rectangle`yayınlar.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

Yanıt yükü şu şekildedir:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
