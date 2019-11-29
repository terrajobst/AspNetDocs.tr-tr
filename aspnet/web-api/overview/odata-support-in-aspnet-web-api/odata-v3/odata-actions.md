---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: ASP.NET Web API 2 ' de OData eylemlerini destekleme | Microsoft Docs
author: MikeWasson
description: "OData 'de, Eylemler, varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur. Eylemler için bazı kullanımlar şunlardır: Uygula..."
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600344"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de OData eylemlerini destekleme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> OData 'de, *Eylemler* , varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur. Bazı eylemler için kullanımları şunlardır:
> 
> - Karmaşık işlemleri uygulama.
> - Aynı anda birkaç varlığı düzenleme.
> - Yalnızca bir varlığın belirli özelliklerine yönelik güncelleştirmelere izin verme.
> - Bir varlıkta tanımlanmayan sunucuya bilgi gönderme.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Web API 2
> - OData sürüm 3
> - Entity Framework 6

## <a name="example-rating-a-product"></a>Örnek: bir ürünü derecelendirme

Bu örnekte, kullanıcıların ürünlerin hızına izin vermek ve ardından her ürün için Ortalama derecelendirmeleri göstermek istiyoruz. Veritabanında, ürünlere girilen derecelendirmelerin bir listesini depolayacağız.

Entity Framework derecelendirmeleri temsil etmek için kullandığımız model aşağıda verilmiştir:

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

Ancak istemcilerin bir `ProductRating` nesnesini bir "derecelendirmeler" koleksiyonuna NAKLETMESINI istemiyoruz. Intuicanlı, derecelendirme, ürünler koleksiyonuyla ilişkilendirilir ve istemcinin yalnızca derecelendirme değerini göndermesinin gerekli olması gerekir.

Bu nedenle, normal CRUD işlemlerini kullanmak yerine, bir istemcinin bir üründe çağırabileceği bir eylem tanımladık. OData terminolojisinde, eylem ürün varlıklarına *bağlanır* .

>Eylemlerin sunucuda yan etkileri vardır. Bu nedenle, bunlar HTTP POST istekleri kullanılarak çağırılır. Eylemler, hizmet meta verilerinde açıklanan parametrelere ve dönüş türlerine sahip olabilir. İstemci, parametreleri istek gövdesinde gönderir ve sunucu döndürülen değeri yanıt gövdesinde gönderir. "Ürünü derecelendirin" eylemini çağırmak için, istemci aşağıdaki gibi bir URI 'ye GÖNDERI gönderir:

[!code-console[Main](odata-actions/samples/sample2.cmd)]

POST isteğindeki veriler yalnızca ürün derecelendirmesidir:

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>Varlık Veri Modeli eylemi bildirme

Web API yapılandırmanızda, eylemi varlık veri modeli (EDM) öğesine ekleyin:

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

Bu kod, ürün varlıklarında gerçekleştirilebilecek bir eylem olarak "RateProduct" tanımlar. Ayrıca, eylemin "derecelendirme" adlı bir **int** parametre aldığını bildirir ve bir **int** değer döndürür.

## <a name="add-the-action-to-the-controller"></a>Eylemi denetleyiciye ekleyin

"RateProduct" eylemi ürün varlıklarına bağlanır. Eylemi uygulamak için, ürünler denetleyicisine `RateProduct` adlı bir yöntem ekleyin:

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

Yöntem adının EDM içindeki eylem adıyla eşleştiğinden emin olun. Yöntemi iki parametreye sahiptir:

- *anahtar*: ürünün derecelendirmek için anahtar.
- *Parametreler*: eylem parametresi değerlerinin bir sözlüğü.

Varsayılan yönlendirme kurallarını kullanıyorsanız, anahtar parametrenin "Key" olarak adlandırılması gerekir. Ayrıca, gösterildiği gibi **[Fromodatauri]** özniteliğini eklemek de önemlidir. Bu öznitelik, Web API 'sini istek URI 'sinden anahtar ayrıştırdığında OData sözdizimi kurallarını kullanmasını söyler.

Eylem parametrelerini almak için *Parameters* sözlüğünü kullanın:

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

İstemci eylem parametrelerini doğru biçimde gönderirse **ModelState. IsValid** değeri true 'dur. Bu durumda, **ODataActionParameters** sözlüğünü parametre değerlerini almak için kullanabilirsiniz. Bu örnekte, `RateProduct` eylemi "derecelendirme" adlı tek bir parametre alır.

## <a name="action-metadata"></a>Eylem meta verileri

Hizmet meta verilerini görüntülemek için/OData/$metadata adresine bir GET isteği gönderin. `RateProduct` eylemi bildiren meta verilerin bölümü aşağıda verilmiştir:

[!code-xml[Main](odata-actions/samples/sample7.xml)]

**FunctionImport** öğesi eylemi bildirir. Alanların çoğu kendi kendine açıklayıcıdır, ancak iki değer de şunları belirtmekte:

- **Ibındable** , eylemin hedef varlıkta en az bir kez çağrılabileceği anlamına gelir.
- **Ialwaysdable** , eylemin hedef varlıkta her zaman çağrılabileceği anlamına gelir.

Fark, bazı eylemlerin her zaman istemciler için kullanılabilir olduğu, ancak diğer eylemlerin da varlığın durumuna bağlı olabileceği durumdur. Örneğin, bir "satın alma" eylemi tanımladığınızı varsayalım. Yalnızca Stokta olan bir öğeyi satın alabilirsiniz. Öğe stokta yoksa, istemci bu eylemi çağıramıyor.

EDM 'yi tanımlarken, **eylem** yöntemi her zaman bağlanabilir bir eylem oluşturur:

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

Bu konunun ilerleyen kısımlarında, her zaman bağlanabilir eylemler ( *geçici* eylemler olarak da adlandırılır) hakkında konuşacağız.

## <a name="invoking-the-action"></a>Eylem çağrılıyor

Şimdi bir istemcinin bu eylemi nasıl çağıracağına bakalım. İstemcinin KIMLIĞI = 4 olan ürüne 2 derecelendirmesine izin vermek istediğini varsayalım. İstek gövdesi için JSON biçimini kullanan örnek bir istek iletisi aşağıda verilmiştir:

[!code-console[Main](odata-actions/samples/sample9.cmd)]

Yanıt iletisi aşağıda verilmiştir:

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>Bir eylemi varlık kümesine bağlama

Önceki örnekte, eylem tek bir varlığa bağlanır: istemci tek bir ürünü ücretler. Ayrıca, bir eylemi bir varlık koleksiyonuna bağlayabilirsiniz. Yalnızca aşağıdaki değişiklikleri yapmanız yeterlidir:

EDM öğesinde, varlığın **koleksiyon** özelliğine eylemi ekleyin.

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

Denetleyici yönteminde, *anahtar* parametresini atlayın.

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

Artık istemci, ürünler varlık kümesinde eylemi çağırır:

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>Koleksiyon parametrelerine sahip eylemler

Eylemler bir değer koleksiyonu alan parametrelere sahip olabilir. EDM 'da, parametreyi bildirmek için **&lt;t&gt;CollectionParameter** ' ı kullanın.

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

Bu, **int** değerlerinin bir koleksiyonunu alan "derecelendirmeler" adlı bir parametre bildirir. Denetleyici yönteminde, **ODataActionParameters** nesnesinden parametre değerini almaya devam edersiniz, ancak bundan sonra değer bir **ıcollection&lt;int&gt;** değeridir:

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>Geçici eylemler

"RateProduct" örneğinde, kullanıcılar her zaman bir ürüne ücret verebilir, böylece eylem her zaman kullanılabilir. Ancak bazı eylemler varlığın durumuna bağlıdır. Örneğin, bir video kiralama hizmetinde, "kullanıma alma" eylemi her zaman kullanılabilir değildir. (Bu videonun bir kopyasının kullanılabilir olup olmadığına bağlıdır.) Bu tür bir eyleme *geçici* eylem denir.

Hizmet meta verilerinde geçici bir **eylem, yanlış değerine eşit bir** şekilde yapılır. Bu aslında varsayılan değerdir, bu nedenle meta veriler şöyle görünür:

[!code-xml[Main](odata-actions/samples/sample16.xml)]

Bu önemlidir: bir eylem geçicidir, sunucu, eylem kullanılabilir olduğunda istemciye bunu söylemelidir. Bu, varlıktaki eyleme bir bağlantı ekleyerek bunu yapar. Bir film varlığına yönelik bir örnek aşağıda verilmiştir:

[!code-console[Main](odata-actions/samples/sample17.cmd)]

"#CheckOut" özelliği, kullanıma alma eyleminin bağlantısını içerir. Eylem kullanılamıyorsa sunucu bağlantıyı atlar.

EDM 'ta geçici bir eylem bildirmek için, **geçişli Entaction** metodunu çağırın:

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

Ayrıca, belirli bir varlık için bir eylem bağlantısı döndüren bir işlev sağlamanız gerekir. **HasActionLink**çağırarak bu işlevi ayarlayın. İşlevi bir lambda ifadesi olarak yazabilirsiniz:

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

Eylem kullanılabiliyorsa, lambda ifadesi eyleme bir bağlantı döndürür. OData seri hale getirici, varlığı serileştirtiğinde bu bağlantıyı içerir. Eylem kullanılabilir olmadığında, işlev `null`döndürür.

## <a name="additional-resources"></a>Ek Kaynaklar

[OData eylemleri örneği](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
