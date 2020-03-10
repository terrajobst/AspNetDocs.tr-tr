---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Web API 2,2 kullanarak tek bir OData v4 oluşturma | Microsoft Docs
author: rick-anderson
description: Bu konu başlığı altında, Web API 2,2 ' de bir OData uç noktasında tek bir tekil nasıl tanımlanacağı gösterilmektedir.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622089"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>Web API 2,2 kullanarak tek bir OData v4 oluşturma

Zoe Luo tarafından

> Geleneksel olarak, bir varlığa yalnızca bir varlık kümesi içinde kapsülleniyorsa erişilebilir. Ancak OData v4, her ikisi de hem WebAPI 2,2 ' nin desteklediği iki ek seçenek sunar.

Bu makalede, Web API 2,2 ' de bir OData uç noktasında tekil nasıl tanımlanacağı gösterilmektedir. Tekil nedir ve bunu kullanmanın avantajlarından faydalanmanız hakkında bilgi edinmek için, bkz. [özel varlığınızı tanımlamak için tek tek kullanma](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx). Web API 'de OData v4 uç noktası oluşturmak için, bkz. [ASP.NET Web apı 2,2 kullanarak OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md). 

Aşağıdaki veri modelini kullanarak Web API projenizde tek bir oluşturacak:

![Veri Modeli](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

Tek bir adlandırılmış `Umbrella` `Company`türüne göre tanımlanır ve `Employees` adlı bir varlık kümesi `Employee`türüne göre tanımlanır.

Bu öğreticide kullanılan çözüm [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)'ten indirilebilir.

## <a name="define-the-data-model"></a>Veri modelini tanımlama

1. CLR türlerini tanımlayın.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. CLR türlerini temel alan EDM modelini oluşturun.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    Burada `builder.Singleton<Company>("Umbrella")`, model oluşturucunun EDM modelinde tek bir adlandırılmış `Umbrella` oluşturmasını söyler.

    Oluşturulan meta veriler aşağıdaki gibi görünür:

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    Meta verilerden, `Employees` varlık kümesindeki Gezinti özelliğinin `Company` Singleton `Umbrella`bağlandığını görebiliriz. Yalnızca `Umbrella` `Company` türüne sahip olduğundan bağlama `ODataConventionModelBuilder`tarafından otomatik olarak gerçekleştirilir. Modelde belirsizlik varsa, bir gezinti özelliğini açıkça tek bir şekilde bağlamak için `HasSingletonBinding` kullanabilirsiniz. `HasSingletonBinding`, CLR tür tanımında `Singleton` özniteliği ile aynı etkiye sahiptir:

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>Tek denetleyiciyi tanımlama

EntitySet denetleyicisi gibi, tek denetleyici `ODataController`devralır ve tek denetleyici adı `[singletonName]Controller`olmalıdır.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

Farklı istek türlerini işlemek için, denetleyicide önceden tanımlanmış olması gerekir. Varsayılan olarak, WebApi 2,2 ' de **öznitelik yönlendirme** etkindir. Örneğin, öznitelik yönlendirme kullanarak `Company` `Revenue` sorgulamayı işlemeye yönelik bir eylem tanımlamak için aşağıdakileri kullanın:

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

Her bir eylem için öznitelikleri tanımlamanızı istemiyorsanız, yalnızca, [OData yönlendirme kurallarını](../odata-routing-conventions.md)izleyen eylemlerinizi tanımlamanız yeterlidir. Tek bir sorgulama için anahtar gerekli olmadığından, tek denetleyicide tanımlanan eylemler, EntitySet denetleyicisinde tanımlanan eylemlerden biraz farklıdır.

Başvuru için, tek denetleyicideki her eylem tanımı için yöntem imzaları aşağıda listelenmiştir.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

Temel olarak, hizmet tarafında yapmanız gereken tek şey budur. [Örnek proje](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) , çözümün ve tek tek 'nın nasıl kullanılacağını gösteren OData istemcisinin tüm kodlarını içerir. İstemci, [OData v4 Istemci uygulaması oluşturma](create-an-odata-v4-client-app.md)bölümündeki adımları izleyerek oluşturulur.

arasında yetersiz alanla karşılaştı. 

*Bu makalenin özgün içeriği için yem hu için teşekkürler.*
