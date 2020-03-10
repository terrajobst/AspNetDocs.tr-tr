---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: Bir .NET Istemcisinden OData hizmetini çağırma (C#) | Microsoft Docs
author: MikeWasson
description: Bu öğreticide, bir C# istemci uygulamasından bir OData hizmetinin nasıl çağrılacağını gösterilmektedir. Öğretici Visual Studio 2013 kullanılan yazılım sürümleri (Visual S ile birlikte çalışarak...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614683"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a>Bir .NET İstemcisinden OData Hizmetine Çağrı Yapma (C#)

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> Bu öğreticide, bir C# istemci uygulamasından bir OData hizmetinin nasıl çağrılacağını gösterilmektedir.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (Visual Studio 2012 ile birlikte geçerlidir)
> - [WCF Veri Hizmetleri İstemci Kitaplığı](https://msdn.microsoft.com/library/cc668772.aspx)
> - Web API 2. (Örnek OData hizmeti Web API 2 kullanılarak oluşturulmuştur, ancak istemci uygulaması Web API 'sine bağımlı değildir.)

Bu öğreticide, OData hizmetini çağıran bir istemci uygulaması oluşturma konusunda adım adım göstereceğiz. OData hizmeti aşağıdaki varlıkları kullanıma sunar:

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

Aşağıdaki makalelerde, Web API 'de OData hizmetinin nasıl uygulanacağı açıklanır. (Ancak, bu öğreticiyi anlamak için bunları okumanız gerekmez.)

- [Web API 2 ' de OData uç noktası oluşturma](creating-an-odata-endpoint.md)
- [Web API 2 ' de OData varlık Ilişkileri](working-with-entity-relations.md)
- [Web API 2’de OData Eylemleri](odata-actions.md)

## <a name="generate-the-service-proxy"></a>Hizmet proxy 'Si oluşturma

İlk adım bir hizmet proxy 'si oluşturmak için kullanılır. Hizmet proxy 'si OData hizmetine erişim yöntemlerini tanımlayan bir .NET sınıfıdır. Proxy, Yöntem çağrılarını HTTP isteklerine çevirir.

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

Visual Studio 'da OData hizmeti projesini açarak başlayın. Hizmeti IIS Express ' de yerel olarak çalıştırmak için CTRL + F5 tuşlarına basın. Yerel adresi, Visual Studio 'Nun atadığı bağlantı noktası numarası dahil olmak üzere unutmayın. Proxy 'yi oluştururken bu adrese ihtiyacınız olacak.

Ardından, Visual Studio 'nun başka bir örneğini açın ve bir konsol uygulaması projesi oluşturun. Konsol uygulaması OData istemci uygulamamız olacaktır. (Ayrıca, projeyi hizmetle aynı çözüme da ekleyebilirsiniz.)

> [!NOTE]
> Kalan adımlar konsol projesine başvurur.

Çözüm Gezgini, **Başvurular** ' a sağ tıklayın ve **hizmet başvurusu Ekle**' ı seçin.

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

**Hizmet başvurusu Ekle** iletişim kutusunda, OData hizmetinin adresini yazın:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

Burada *bağlantı* noktası numarasıdır.

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

**Ad alanı**Için "ProductService" yazın. Bu seçenek, proxy sınıfının ad alanını tanımlar.

**Git**' e tıklayın. Visual Studio, hizmette varlıkları saptamak için OData meta veri belgesini okur.

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

Projeniz için proxy sınıfını eklemek üzere **Tamam** ' a tıklayın.

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>Hizmet proxy sınıfının bir örneğini oluşturma

`Main` yönteminizin içinde, proxy sınıfının yeni bir örneğini aşağıdaki gibi oluşturun:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

Yine, hizmetinizin çalıştığı gerçek bağlantı noktası numarasını kullanın. Hizmetinizi dağıttığınızda, canlı hizmetin URI 'sini kullanırsınız. Proxy 'yi güncelleştirmeniz gerekmez.

Aşağıdaki kod, istek URI 'Lerini konsol penceresine yazdıran bir olay işleyicisi ekler. Bu adım gerekli değildir, ancak her sorgu için URI 'Leri görmek ilginç olur.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>Hizmeti sorgulama

Aşağıdaki kod, OData hizmetinden ürünlerin listesini alır.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

HTTP isteğini göndermek veya yanıtı ayrıştırmak için herhangi bir kod yazmanıza gerek olmadığını unutmayın. **Foreach** döngüsünde `Container.Products` koleksiyonunu Numaralandırdığınızda proxy sınıfı bunu otomatik olarak yapar.

Uygulamayı çalıştırdığınızda, çıkış aşağıdaki gibi görünmelidir:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

KIMLIĞE göre bir varlık almak için bir `where` yan tümcesi kullanın.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

Bu konunun geri kalanında, yalnızca hizmeti çağırmak için gereken kod olan `Main` işlevinin tamamını göstermiyorum.

## <a name="apply-query-options"></a>Sorgu seçeneklerini Uygula

OData filtrelemeye, sıralamaya, sayfa verilerine ve benzeri şekilde kullanılabilecek [sorgu seçeneklerini](../supporting-odata-query-options.md) tanımlar. Hizmet proxy 'sinde, çeşitli LINQ ifadelerini kullanarak bu seçenekleri uygulayabilirsiniz.

Bu bölümde kısa örnekler göstereceğiz. Daha fazla ayrıntı için MSDN 'de [LINQ hususları (WCF veri Hizmetleri)](https://msdn.microsoft.com/library/ee622463.aspx) konusuna bakın.

### <a name="filtering-filter"></a>Filtreleme ($filter)

Filtrelemek için bir `where` yan tümcesi kullanın. Aşağıdaki örnek ürün kategorisine göre filtreliyor.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

Bu kod, aşağıdaki OData sorgusuna karşılık gelir.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

Proxy 'nin `where` yan tümcesini OData `$filter` ifadesine dönüştürtiğine dikkat edin.

### <a name="sorting-orderby"></a>Sıralama ($orderby)

Sıralamak için bir `orderby` yan tümcesi kullanın. Aşağıdaki örnek fiyata göre, en yüksekten en düşüğe göre sıralanır.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

Buna karşılık gelen OData isteği aşağıda verilmiştir.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>İstemci tarafı sayfalama ($skip ve $top)

Büyük varlık kümelerinde istemci, sonuçların sayısını sınırlamak isteyebilir. Örneğin, bir istemci tek seferde 10 girdi gösterebilir. Bu, *istemci tarafı sayfalama*olarak adlandırılır. (Sunucunun sonuç sayısını sınırlayan [sunucu tarafı sayfalama](../supporting-odata-query-options.md#server-paging)da vardır.) İstemci tarafı sayfalama gerçekleştirmek için LINQ **Skip** ve **Al** yöntemlerini kullanın. Aşağıdaki örnek ilk 40 sonucunu atlar ve sonraki 10 ' un sürer.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

Buna karşılık gelen OData isteği şöyledir:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>Seç ($select) ve genişlet ($expand)

İlgili varlıkları eklemek için `DataServiceQuery<t>.Expand` yöntemini kullanın. Örneğin, her bir `Product`için `Supplier` eklemek için:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

Buna karşılık gelen OData isteği şöyledir:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

Yanıtın şeklini değiştirmek için LINQ **Select** yan tümcesini kullanın. Aşağıdaki örnek, başka hiçbir özellik olmadan yalnızca her bir ürünün adını alır.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

Buna karşılık gelen OData isteği şöyledir:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Bir SELECT yan tümcesi, ilgili varlıkları içerebilir. Bu durumda, **Expand**çağırmayın; Bu durumda ara sunucu genişletmeyi otomatik olarak ekler. Aşağıdaki örnek, her bir ürünün adını ve tedarikçiyi alır.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

Buna karşılık gelen OData isteği aşağıda verilmiştir. **$Expand** seçeneğini içerdiğine dikkat edin.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

$Select ve $expand hakkında daha fazla bilgi için bkz. [Web API 2 ' de $SELECT, $expand ve $value kullanma](../using-select-expand-and-value.md).

## <a name="add-a-new-entity"></a>Yeni varlık Ekle

Bir varlık kümesine yeni bir varlık eklemek için, *EntitySet* 'in varlık kümesinin adı olduğu `AddToEntitySet`çağırın. Örneğin, `AddToProducts` `Products` varlık kümesine yeni bir `Product` ekler. Proxy oluşturduğunuzda WCF Veri Hizmetleri, bu kesin türü belirtilmiş **AddTo** yöntemlerini otomatik olarak oluşturur.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

İki varlık arasında bir bağlantı eklemek için **AddLink** ve **SetLink** yöntemlerini kullanın. Aşağıdaki kod yeni bir tedarikçi ve yeni bir ürün ekler ve bunlar arasında bağlantılar oluşturur.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

Gezinti özelliği bir koleksiyon olduğunda **AddLink** kullanın. Bu örnekte, tedarikçide `Products` koleksiyonuna bir ürün ekliyoruz.

Gezinti özelliği tek bir varlık olduğunda **SetLink** kullanın. Bu örnekte, üründe `Supplier` özelliğini ayarlarız.

## <a name="update--patch"></a>Güncelleştirme/düzeltme eki

Bir varlığı güncelleştirmek için **UpdateObject** yöntemini çağırın.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

**SaveChanges**öğesini çağırdığınızda güncelleştirme gerçekleştirilir. Varsayılan olarak, WCF bir HTTP BIRLEŞTIRME isteği gönderir. **Patchonupdate** SEÇENEĞI, WCF 'ye bunun yerıne BIR http Patch göndermesini söyler.

> [!NOTE]
> Düzeltme Eki neden BIRLEŞMELIDIR? Özgün HTTP 1,1 belirtimi ([RCF 2616](http://tools.ietf.org/html/rfc2616)), "Kısmi güncelleştirme" semantiğine sahip HERHANGI bir http yöntemi tanımlamıyor. Kısmi güncelleştirmeleri desteklemek için, OData belirtimi MERGE metodunu tanımladı. 2010 ' de, [RFC 5789](http://tools.ietf.org/html/rfc5789) kısmi GÜNCELLEŞTIRMELER için Patch metodunu tanımladı. Bu [blog gönderisine](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) ait geçmişin WCF veri Hizmetleri blogundan bazılarını okuyabilirsiniz. Bugün, düzeltme eki BIRLEŞTIRME üzerinden tercih edilir. Web API 'SI yapı iskelesi tarafından oluşturulan OData denetleyicisi her iki yöntemi de destekler.

Tüm varlığı (PUT semantiğini) değiştirmek istiyorsanız, **Replaceonupdate** seçeneğini belirtin. Bu, WCF 'nin bir HTTP PUT isteği göndermesini sağlar.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>Bir varlığı silme

Bir varlığı silmek için **DeleteObject**çağırın.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>OData eylemini çağırma

OData 'de, [Eylemler](odata-actions.md) , varlıklarda CRUD işlemleri olarak kolayca tanımlanmayan sunucu tarafı davranışları eklemenin bir yoludur.

OData meta veri belgesinde eylemler açıklanmakta olsa da, proxy sınıfı kendileri için kesin tür belirtilmiş Yöntemler oluşturmaz. Genel **Execute** metodunu kullanarak yine de bir OData eylemi çağırabilirsiniz. Ancak, parametrelerin ve dönüş değerinin veri türlerini bilmeniz gerekecektir.

Örneğin, `RateProduct` eylemi `Int32` türü "derecelendirme" adlı parametreyi alır ve bir `double`döndürür. Aşağıdaki kod, bu eylemin nasıl çağıralınacağını gösterir.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

Daha fazla bilgi için bkz.[hizmet işlemlerini ve eylemleri çağırma](https://msdn.microsoft.com/library/hh230677.aspx).

Bir seçenek, kapsayıcıyı çağıran türü kesin belirlenmiş bir yöntem sağlamak için **kapsayıcı** sınıfını genişletmenin bir seçenektir:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
