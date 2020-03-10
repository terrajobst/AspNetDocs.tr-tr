---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2 OData-ASP.NET 4. x için Güvenlik Kılavuzu
author: MikeWasson
description: ASP.NET 4. x üzerinde ASP.NET Web API 2 için OData aracılığıyla bir veri kümesini kullanıma alırken dikkate alınması gereken güvenlik sorunlarını açıklar.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556499"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 OData için Güvenlik Kılavuzu

, [Mike te son](https://github.com/MikeWasson)

Bu konuda, ASP.NET 4. x üzerinde ASP.NET Web API 2 için OData aracılığıyla bir veri kümesini kullanıma alırken göz önünde bulundurmanız gereken bazı güvenlik sorunları açıklanmaktadır.

## <a name="edm-security"></a>EDM güvenliği

Sorgu semantiği, temel alınan model türlerine değil, varlık veri modeli (EDM) tabanlıdır. EDM öğesinden bir özelliği hariç tutabilir ve sorgu görünür olmayacaktır. Örneğin, modelinize bir maaş özelliği olan bir çalışan türü içerdiğini varsayalım. Bu özelliği, istemcilerinden gizlemek için EDM 'ten dışlamak isteyebilirsiniz.

EDM 'ten bir özelliği dışmanın iki yolu vardır. **[Ignoredatamember]** özniteliğini model sınıfındaki özellikte ayarlayabilirsiniz:

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

Ayrıca, özelliği EDM aracılığıyla program aracılığıyla da kaldırabilirsiniz:

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>Sorgu güvenliği

Kötü amaçlı veya Naïve istemcisi, yürütülmesi çok uzun süren bir sorgu oluşturabilir. En kötü durumda, bu, hizmetinize erişimi kesintiye uğratabilir.

**[Queryable]** özniteliği sorguyu ayrıştırır, doğrular ve uygular bir eylem filtresidir. Filtre, sorgu seçeneklerini bir LINQ ifadesine dönüştürür. OData denetleyicisi bir **IQueryable** türü döndürdüğünde, **IQueryable** LINQ sağlayıcısı LINQ ifadesini bir sorguya dönüştürür. Bu nedenle, performans kullanılan LINQ sağlayıcısına ve ayrıca veri kümenizin veya veritabanı şemanızın belirli özelliklerine bağlıdır.

ASP.NET Web API 'sinde OData sorgu seçeneklerini kullanma hakkında daha fazla bilgi için bkz. [OData sorgu seçeneklerini destekleme](supporting-odata-query-options.md).

Tüm istemcilerin güvenilir olduğunu (örneğin, bir kurumsal ortamda) biliyorsanız veya veri kümeniz küçükse, sorgu performansı bir sorun olmayabilir. Aksi takdirde, aşağıdaki önerileri göz önünde bulundurmanız gerekir.

- Farklı sorgularla hizmetinizi test edin ve DB 'yi profili yapın.
- Tek bir sorguda büyük bir veri kümesi döndürmeyi önlemek için sunucu odaklı sayfalama özelliğini etkinleştirin. Daha fazla bilgi için bkz. [sunucu odaklı sayfalama](supporting-odata-query-options.md#server-paging). 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- $Filter ve $orderby gerekiyor mu? Bazı uygulamalar $top ve $skip kullanarak istemci disk belleğine izin verebilir, ancak diğer sorgu seçeneklerini devre dışı bırakabilir. 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- $Orderby kümelenmiş dizindeki özelliklerle kısıtlamayı düşünün. Büyük verileri kümelenmiş dizin olmadan sıralama yavaş olur. 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- Maksimum düğüm sayısı: **[sorgulanabilir]** üzerindeki **MaxNodeCount** özelliği, $Filter sözdizimi ağacında izin verilen en fazla düğüm sayısını ayarlar. Varsayılan değer 100 ' dir, ancak daha düşük bir değer ayarlamak isteyebilirsiniz, çünkü çok sayıda düğüm derlemek için yavaş olabilir. Bu, özellikle bir ara LINQ sağlayıcısı kullanmadan LINQ to Objects (örneğin, bellekte bir koleksiyonda LINQ sorguları) kullanıyorsanız geçerlidir. 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- Herhangi bir () ve tüm () işlevlerini devre dışı bırakmayı düşünün, çünkü bunlar yavaş olabilir. 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- Herhangi bir dize özelliği örneğin, büyük&#8212;dizeler içeriyorsa, bir ürün açıklaması veya blog girdisi&#8212;dize işlevlerini devre dışı bırakmayı düşünün. 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- Gezinti özelliklerinde filtrelemeye izin vermeme seçeneğini göz önünde bulundurun. Gezinme özelliklerine filtre uygulamak, veritabanı şemanıza bağlı olarak yavaş olabilecek bir birleşime yol açabilir. Aşağıdaki kod, gezinti özelliklerinin filtrelenmesini önleyen bir sorgu doğrulayıcısı gösterir. Sorgu Doğrulayıcıları hakkında daha fazla bilgi için bkz. [sorgu doğrulaması](supporting-odata-query-options.md#query-validation). 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- Veritabanınız için özelleştirilmiş bir doğrulayıcı yazarak $filter sorguları kısıtlamayı düşünün. Örneğin, bu iki sorguyu göz önünde bulundurun: 

  - Son adı ' A ' ile başlayan aktörlere sahip tüm filmler.
  - 1994 içinde yayınlanan tüm filmler.

    Filmler aktörlere göre dizinlenmediği takdirde, ilk sorgu DB altyapısının tüm film listesini taramasını gerektirebilir. İkinci sorgu kabul edilebilir olabilir, ancak film yayın yılı tarafından dizine alınır.

    Aşağıdaki kod, "ReleaseYear" ve "title" özelliklerinde filtrelemeye izin veren ancak başka hiçbir özellik bulunmayan bir doğrulayıcısı gösterir.

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- Genel olarak, hangi $filter işlevleri gerektiğini göz önünde bulundurun. İstemcileriniz $filter tam ifade etmek gerekmiyorsa, izin verilen işlevleri sınırlayabilirsiniz.
