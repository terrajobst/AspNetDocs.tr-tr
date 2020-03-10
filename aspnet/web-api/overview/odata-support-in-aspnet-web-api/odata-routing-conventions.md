---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2 OData-ASP.NET 4. x içindeki yönlendirme kuralları
author: MikeWasson
description: ASP.NET 4. x içindeki Web API 2 ' nin OData uç noktaları için kullandığı yönlendirme kurallarını açıklar.
ms.author: riande
ms.date: 07/31/2013
ms.custom: seoapril2019
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63df4a82cd8df92631485b2544117844cfd0ca56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614718"
---
# <a name="routing-conventions-in-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 OData içindeki yönlendirme kuralları

, [Mike te son](https://github.com/MikeWasson)

> Bu makalede, ASP.NET 4. x içindeki Web API 2 ' nin OData uç noktaları için kullandığı yönlendirme kuralları açıklanır.

Web API 'SI bir OData isteği aldığında, isteği bir denetleyici adı ve eylem adı ile eşler. Eşleme, HTTP yöntemini ve URI 'yi temel alır. Örneğin, `GET /odata/Products(1)` `ProductsController.GetProduct`eşlenir.

Bu makalenin 1. bölümünde, yerleşik OData yönlendirme kurallarını açıklıyorum. Bu kurallar, özel olarak OData uç noktaları için tasarlanmıştır ve varsayılan Web API yönlendirme sisteminin yerini alır. ( **MapODataRoute**' i çağırdığınızda değiştirme olur.)

Bölüm 2 ' de, özel yönlendirme kuralları eklemeyi gösterir. Şu anda yerleşik kurallar, tüm OData URI aralığını kapsamaz, ancak bunları ek durumları işleyecek şekilde genişletebilirsiniz.

- [Yerleşik yönlendirme kuralları](#conventions)
- [Özel yönlendirme kuralları](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>Yerleşik yönlendirme kuralları

Web API 'de OData yönlendirme kurallarını anladığımda, OData URI 'Lerini anlamak faydalı olabilir. [OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) aşağıdakilerden oluşur:

- Hizmet kökü
- Kaynak yolu
- Sorgu seçenekleri

![](odata-routing-conventions/_static/image1.png)

Yönlendirme için, önemli parça kaynak yoludur. Kaynak yolu kesimlere bölünür. Örneğin, `/Products(1)/Supplier` üç parçaya sahiptir:

- `Products`, "Ürünler" adlı bir varlık kümesini ifade eder.
- `1`, kümeden tek bir varlık seçen bir varlık anahtarıdır.
- `Supplier`, ilgili varlığı seçen bir gezinti özelliğidir.

Bu nedenle bu yol, 1. ürünün tedarikçisine sahiptir.

> [!NOTE]
> OData yol kesimleri, her zaman URI kesimlerine karşılık gelmez. Örneğin, "1" bir yol kesimi olarak değerlendirilir.

**Denetleyici adları.** Denetleyici adı her zaman kaynak yolunun kökündeki varlık kümesinden türetilir. Örneğin, kaynak yolu `/Products(1)/Supplier`ise, Web API 'SI `ProductsController`adlı bir denetleyici arar.

**Eylem adları.** Eylem adları, aşağıdaki tablolarda listelendiği gibi yol kesimlerinden ve varlık veri modelinden (EDM) türetilir. Bazı durumlarda, eylem adı için iki seçeneğiniz vardır. Örneğin, "Get" veya &quot;GetProducts&quot;.

**Varlıkları sorgulama**

| İstek | Örnek URI | Eylem Adı | Örnek eylem |
| --- | --- | --- | --- |
| /EntitySet al | /Products | GetEntitySet veya Get | GetProducts |
| /EntitySet (anahtar) Al | /Products (1) | GetEntityType veya Get | GetProduct |
| /EntitySet (anahtar)/Cast al | /Products (1)/models.Book | GetEntityType veya Get | GetBook |

Daha fazla bilgi için bkz. [salt bir OData uç noktası oluşturma](odata-v3/creating-an-odata-endpoint.md).

**Varlıkları oluşturma, güncelleştirme ve silme**

| İstek | Örnek URI | Eylem Adı | Örnek eylem |
| --- | --- | --- | --- |
| /EntitySet SONRASı | /Products | PostEntityType veya post | PostProduct |
| PUT/EntitySet (anahtar) | /Products (1) | PutEntityType veya put | PutProduct |
| /EntitySet (anahtar)/Cast koy | /Products (1)/models.Book | PutEntityType veya put | PutBook |
| PATCH/EntitySet (anahtar) | /Products (1) | PatchEntityType veya Patch | PatchProduct |
| PATCH/EntitySet (anahtar)/Cast | /Products (1)/models.Book | PatchEntityType veya Patch | PatchBook |
| /EntitySet 'i SIL (anahtar) | /Products (1) | DeleteEntityType veya delete | DeleteProduct |
| /EntitySet (anahtar)/Cast SIL | /Products (1)/models.Book | DeleteEntityType veya delete | DeleteBook |

**Gezinti özelliği sorgulama**

| İstek | Örnek URI | Eylem Adı | Örnek eylem |
| --- | --- | --- | --- |
| /EntitySet (anahtar)/gezinti al | /Products (1)/Tedarikçi | GetNavigationFromEntityType veya GetNavigation | GetSupplierFromProduct |
| /EntitySet (anahtar)/ro/Navigation al | /Products (1)/Models.Book/Author | GetNavigationFromEntityType veya GetNavigation | GetAuthorFromBook |

Daha fazla bilgi için bkz. [varlık ilişkileri Ile çalışma](odata-v3/working-with-entity-relations.md).

**Bağlantı oluşturma ve silme**

| İstek | Örnek URI | Eylem Adı |
| --- | --- | --- |
| /EntitySet (anahtar)/$links/Navigation SONRASı | /Products (1)/$links/Tedarikçi | CreateLink |
| /EntitySet (anahtar)/$links/Navigation koy | /Products (1)/$links/Tedarikçi | CreateLink |
| /EntitySet (anahtar)/$links/gezintiyi SIL | /Products (1)/$links/Tedarikçi | DeleteLink |
| /EntitySet (anahtar)/$links/Navigation (relatedKey) SIL | /Products/(1)/$links/Suppliers (1) | DeleteLink |

Daha fazla bilgi için bkz. [varlık ilişkileri Ile çalışma](odata-v3/working-with-entity-relations.md).

**Özellikler**

*Web API 2 gerektirir*

| İstek | Örnek URI | Eylem Adı | Örnek eylem |
| --- | --- | --- | --- |
| /EntitySet (anahtar)/Property al | /Products (1)/Name | GetPropertyFromEntityType veya GetProperty | GetNameFromProduct |
| /EntitySet (anahtar)/ro/Property al | /Products (1)/Models.Book/Author | GetPropertyFromEntityType veya GetProperty | GetTitleFromBook |

**Eylemler**

| İstek | Örnek URI | Eylem Adı | Örnek eylem |
| --- | --- | --- | --- |
| POST/EntitySet (anahtar)/Action | /Products (1)/ücret | ActionNameOnEntityType veya ActionName | RateOnProduct |
| POST/EntitySet (anahtar)/ro/Action | /Products (1)/Models.Book/CheckOut | ActionNameOnEntityType veya ActionName | CheckOutOnBook |

Daha fazla bilgi için bkz. [OData eylemleri](odata-v3/odata-actions.md).

**Yöntem Imzaları**

Yöntem imzaları için bazı kurallar aşağıda verilmiştir:

- Yol bir anahtar içeriyorsa, eylem *anahtar*adlı bir parametreye sahip olmalıdır.
- Yol, bir gezinti özelliğine bir anahtar içeriyorsa, eylem *RelatedKey*adlı bir parametreye sahip olmalıdır.
- **[Fromodatauri]** parametresiyle *anahtar* ve *RelatedKey* parametreleri süsle.
- POST ve PUT istekleri, varlık türünün bir parametresini alır.
- Düzeltme Eki istekleri, **Delta&lt;t&gt;** türünde bir parametre alır, burada *t* varlık türüdür.

Başvuru için, her yerleşik OData yönlendirme kuralı için yöntem imzalarını gösteren bir örnek aşağıda verilmiştir.

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>Özel yönlendirme kuralları

Şu anda yerleşik kurallar olası tüm OData URI 'Lerini kapsamaz. **IODataRoutingConvention** arabirimini uygulayarak yeni kurallar ekleyebilirsiniz. Bu arabirimin iki yöntemi vardır:

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **SelectController** denetleyicinin adını döndürür.
- **SelectAction** eylemin adını döndürür.

Her iki yöntem için de kural bu istek için uygulanmadığından, yöntemi null döndürmelidir.

**ODataPath** parametresi, ayrıştırılmış OData kaynak yolunu temsil eder. Kaynak yolunun her segmenti için bir tane olmak üzere **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** örneklerinin bir listesini içerir. **ODataPathSegment** soyut bir sınıftır; her segment türü **ODataPathSegment**öğesinden türetilen bir sınıf tarafından temsil edilir.

**ODataPath. TemplatePath** özelliği, tüm yol segmentlerinin bitiştirilmesi temsil eden bir dizedir. Örneğin, URI `/Products(1)/Supplier`, yol şablonu &quot;~/EntitySet/Key/Navigation&quot;olur. Segmentlerin doğrudan URI kesimlerine karşılık gelmediğine dikkat edin. Örneğin, varlık anahtarı (1) kendi **ODataPathSegment**olarak temsil edilir.

Genellikle, **IODataRoutingConvention** uygulamasında aşağıdakiler vardır:

1. Bu kuralın geçerli istek için geçerli olup olmadığını görmek için yol şablonunu karşılaştırın. Uygulama yoksa, null döndürün.
2. Kural geçerliyse, denetleyiciyi ve eylem adlarını türetmek için **ODataPathSegment** örneklerinin özelliklerini kullanın.
3. Eylemler için, işlem parametrelerine bağlanması gereken yol sözlüğüne herhangi bir değer ekleyin (genellikle varlık anahtarları).

Belirli bir örneğe bakalım. Yerleşik yönlendirme kuralları bir gezinti koleksiyonuna dizin oluşturmayı desteklemez. Diğer bir deyişle, aşağıdaki gibi URI 'Ler için bir kural yoktur:

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

Bu tür bir sorgu işlemek için özel bir yönlendirme kuralı aşağıda verilmiştir.

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

Notlar:

1. Bu sınıftaki **SelectController** yöntemi bu yeni yönlendirme kuralına uygun olduğundan **EntitySetRoutingConvention**öğesinden türedim. Bu, **SelectController**'ı yeniden uygulamam gerekmediği anlamına gelir.
2. Kural yalnızca GET istekleri için geçerlidir ve yalnızca yol şablonu &quot;~/EntitySet/Key/Navigation/Key&quot;olduğunda geçerlidir.
3. Eylem adı &quot;Get {EntityType}&quot;; burada *{EntityType}* , gezinti koleksiyonunun türüdür. Örneğin, Gettedarikçinin&quot;&quot;. &#8212; Yalnızca denetleyici eylemlerinizin eşleştiğinden emin olmak istediğiniz adlandırma kurallarını kullanabilirsiniz.
4. Eylem, *anahtar* ve *RelatedKey*adlı iki parametre alır. (Önceden tanımlanmış bazı parametre adlarının listesi için bkz. [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx).)

Sonraki adım, yönlendirme kuralları listesine yeni kuralı ekliyor. Bu, aşağıdaki kodda gösterildiği gibi yapılandırma sırasında gerçekleşir:

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

Aşağıda, çalışmak için yararlı olan bazı diğer örnek yönlendirme kuralları verilmiştir:

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [Nonbindavbleactionroutingconvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

Ayrıca, Web API 'sinin kendisi açık kaynak olduğundan, yerleşik yönlendirme kuralları için [kaynak kodu](http://aspnetwebstack.codeplex.com/) görebilirsiniz. Bunlar **System. Web. http. OData. Routing. kurallarına** ilişkin ad alanında tanımlanmıştır.
