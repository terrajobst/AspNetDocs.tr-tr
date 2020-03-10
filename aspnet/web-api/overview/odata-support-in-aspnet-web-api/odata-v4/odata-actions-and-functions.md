---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: ASP.NET Web API 2,2 kullanılarak OData v4 'deki eylemler ve Işlevler | Microsoft Docs
author: MikeWasson
description: OData 'de, Eylemler ve işlevler, varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur. Bu öğreticide nasıl yapılacağı gösterilmektedir...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556226"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>ASP.NET Web API 2,2 kullanılarak OData v4 'deki eylemler ve Işlevler

, [Mike te son](https://github.com/MikeWasson)

> OData 'de, Eylemler ve işlevler, varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur. Bu öğreticide, Web API 2,2 kullanılarak bir OData v4 uç noktasına eylemler ve işlevlerin nasıl ekleneceği gösterilmektedir. Öğretici, [ASP.NET Web API 2 kullanarak bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md) öğreticisinde derleme
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
> - Web API 2,2
> - OData v4
> - Visual Studio 2013 (Visual Studio 2017 'yi [buraya](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)indirin)
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>Öğretici sürümleri
>
> OData sürüm 3 için bkz. [ASP.NET Web API 2 ' de OData eylemleri](../odata-v3/odata-actions.md).

*Eylemler* ve *işlevler* arasındaki fark, eylemlerin yan etkileri olabilir ve işlevleri değildir. Hem eylemler hem de işlevler veri döndürebilir. Bazı eylemler için kullanımları şunlardır:

- Karmaşık işlemler.
- Aynı anda birkaç varlığı düzenleme.
- Yalnızca bir varlığın belirli özelliklerine yönelik güncelleştirmelere izin verme.
- Varlık olmayan verileri gönderme.

İşlevler, doğrudan bir varlığa veya koleksiyona karşılık gelen bilgileri döndürmek için faydalıdır.

Bir eylem (veya işlev) tek bir varlığı veya koleksiyonu hedefleyebilir. OData terminolojisinde bu *bağlamadır*. Ayrıca, hizmette statik işlemler olarak çağrılan &quot;ilişkisiz&quot; eylemlere/işlevlere sahip olabilirsiniz.

## <a name="example-adding-an-action"></a>Örnek: eylem ekleme

Bir ürünü derecelendirmek için bir eylem tanımlayalim.

> [!NOTE]
> Bu öğretici, [ASP.NET Web API 2 kullanarak bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md) öğreticisinde derleme

İlk olarak, derecelendirmeleri temsil etmek için bir `ProductRating` modeli ekleyin.

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

Ayrıca, `ProductsContext` sınıfına bir **Dbset** ekleyin, bu sayede EF veritabanında bir derecelendirme tablosu oluşturacaktır.

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>Eylemi EDM öğesine ekleyin

WebApiConfig.cs içinde aşağıdaki kodu ekleyin:

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

**EntityTypeConfiguration. Action** yöntemi varlık veri modeli 'NE (EDM) bir eylem ekler. **Parameter** yöntemi eylem için türü belirlenmiş bir parametre belirtir.

Bu kod ayrıca EDM için ad alanını ayarlar. Eylem için URI tam eylem adını içerdiğinden, ad alanı önemlidir:

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> Tipik bir IIS yapılandırmasında, bu URL 'deki nokta IIS 'nin 404 hatasını döndürmesine neden olur. Bunu, Web. config dosyanıza aşağıdaki bölümü ekleyerek çözebilirsiniz:

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>Eylem için bir denetleyici yöntemi ekleme

&quot;hız&quot; eylemini etkinleştirmek için aşağıdaki yöntemi `ProductsController`ekleyin:

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

Yöntem adının eylem adıyla eşleştiğinden emin olun. **[HttpPost]** özniteliği, YÖNTEMIN BIR http post yöntemi olduğunu belirtir.

İstemci, eylemi çağırmak için aşağıdakine benzer bir HTTP POST isteği gönderir:

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

&quot;ücret&quot; eylemi ürün örneklerine bağlanır, bu nedenle eylem URI 'si varlık URI 'sine eklenen tam eylem adıdır. (EDM ad alanını &quot;ProductService&quot;olarak belirlediğimiz için tam olarak nitelenmiş eylem adı &quot;ProductService. Rate&quot;.)

İsteğin gövdesi bir JSON yükü olarak eylem parametrelerini içerir. Web API 'si, JSON yükünü otomatik olarak bir **ODataActionParameters** nesnesine dönüştürür; bu yalnızca parametre değerlerinin bir sözlüğüdür. Denetleyici yönteminizin parametrelerine erişmek için bu sözlüğü kullanın.

İstemci eylem parametrelerini yanlış biçimde gönderirse **ModelState. IsValid** değeri false 'tur. Denetleyici yönteminizin bu bayrağını işaretleyin ve **IsValid** yanlış ise bir hata döndürün.

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>Örnek: bir Işlev ekleme

Şimdi en pahalı ürünü döndüren bir OData işlevi ekleyelim. Daha önce olduğu gibi ilk adım, EDM öğesine işlevi ekliyor. WebApiConfig.cs içinde aşağıdaki kodu ekleyin.

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

Bu durumda, işlevi ayrı ürün örnekleri yerine ürünler koleksiyonuna bağlanır. İstemciler bir GET isteği göndererek işlevi çağırır:

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

Bu işlev için Controller yöntemi aşağıda verilmiştir:

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

Yöntem adının işlev adıyla eşleştiğinden emin olun. **[HttpGet]** özniteliği, YÖNTEMIN BIR http get yöntemi olduğunu belirtir.

HTTP yanıtı aşağıda verilmiştir:

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>Örnek: Ilişkisiz bir Işlev ekleme

Önceki örnek bir koleksiyona bağlamıştı. Bu sonraki örnekte, *ilişkisiz* bir işlev oluşturacağız. İlişkisiz işlevler, hizmette statik işlemler olarak çağrılır. Bu örnekteki işlev, belirli bir posta kodu için satış vergisini döndürür.

WebApiConfig dosyasında, EDM öğesine işlevi ekleyin:

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

**İşlev** , varlık türü veya koleksiyon yerine doğrudan **ODataModelBuilder**üzerinde çağrıldığımızda dikkat edin. Bu, model Oluşturucu işlevinin ilişkisiz olduğunu söyler.

İşlevi uygulayan Controller yöntemi aşağıda verilmiştir:

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

Bu yöntemi hangi Web API denetleyicisine yerleştirdiğinizden bağımsız değildir. `ProductsController`yerleştirebilir veya ayrı bir denetleyici tanımlayabilirsiniz. **[ODataRoute]** ÖZNITELIĞI işlevin URI şablonunu tanımlar.

Örnek bir istemci isteği aşağıda verilmiştir:

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

HTTP yanıtı:

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
