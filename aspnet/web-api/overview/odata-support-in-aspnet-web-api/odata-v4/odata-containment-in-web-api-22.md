---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Web API 2,2 kullanarak OData v4 'da kapsama | Microsoft Docs
author: rick-anderson
description: Geleneksel olarak, bir varlığa yalnızca bir varlık kümesi içinde kapsülleniyorsa erişilebilir. Ancak OData v4 iki ek seçenek sunar, tek ve Con...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 50050e40c4c42bf6d769d077c27864ee6417d4db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525125"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a>Web API 2,2 kullanarak OData v4 'de kapsama

Jinfu tan tarafından

> Geleneksel olarak, bir varlığa yalnızca bir varlık kümesi içinde kapsülleniyorsa erişilebilir. Ancak OData v4, her ikisi de hem WebAPI 2,2 ' nin desteklediği iki ek seçenek sunar.

Bu konuda, WebApi 2,2 ' de OData uç noktasında bir kapsama nasıl tanımlanacağı gösterilmektedir. Kapsama hakkında daha fazla bilgi için bkz. [içerme, OData v4 ile geliyor](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx). Web API 'de OData v4 uç noktası oluşturmak için, bkz. [ASP.NET Web apı 2,2 kullanarak OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md).

İlk olarak, bu veri modelini kullanarak OData hizmetinde bir kapsama alanı modeli oluşturacağız:

![Veri modeli](odata-containment-in-web-api-22/_static/image1.png)

Hesap birçok Paymentınstruments (PI) içerir, ancak bir PI için bir varlık kümesi tanımlamadık. Bunun yerine, PSIS 'ye yalnızca bir hesap üzerinden erişilebilir.

Bu konu başlığında kullanılan çözümü [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)adresinden indirebilirsiniz.

## <a name="defining-the-data-model"></a>Veri modeli tanımlama

1. CLR türlerini tanımlayın.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained` özniteliği, içerme gezintisi özellikleri için kullanılır.
2. CLR türlerini temel alan EDM modelini oluşturun.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `ODataConventionModelBuilder`, `Contained` özniteliği ilgili gezinti özelliğine eklenirse, EDM modelinin oluşturulmasını işleymeyecektir. Özellik bir koleksiyon türü ise, bir `GetCount(string NameContains)` işlevi de oluşturulacaktır.

    Oluşturulan meta veriler aşağıdaki gibi görünür:

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget` özniteliği, Gezinti özelliğinin bir içerme olduğunu gösterir.

## <a name="define-the-containing-entity-set-controller"></a>İçerilen varlık kümesi denetleyicisini tanımlayın

Kapsanan varlıkların kendi denetleyicisi yok; eylem, kapsayan varlık kümesi denetleyicisinde tanımlanmıştır. Bu örnekte, bir AccountsController vardır ancak Paymentınstrumentscontroller yoktur.

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

OData yolu 4 veya daha fazla kesimdeyse, yukarıdaki denetleyicideki `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` gibi yalnızca öznitelik yönlendirme işe yarar. Aksi halde, hem öznitelik hem de geleneksel yönlendirme işe yarar: Örneğin, `GetPayInPIs(int key)` eşleşir `GET ~/Accounts(1)/PayinPIs`.

*Bu makalenin özgün içeriği için yem hu için teşekkürler.*
