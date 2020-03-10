---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: '6\. Bölüm: ürün ve sipariş denetleyicileri oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524992"
---
# <a name="part-6-creating-product-and-order-controllers"></a>6\. Bölüm: ürün ve sipariş denetleyicileri oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a>Ürün denetleyicisi ekleme

Yönetici denetleyicisi, yönetici ayrıcalıklarına sahip kullanıcılar içindir. Diğer yandan müşteriler ürünleri görüntüleyebilir, ancak oluşturamaz, güncelleştiremez veya silemez.

Post, put ve DELETE yöntemlerine erişimi kolayca kısıtlayabiliriz ve Get yöntemlerinin açık bırakılması gerekir. Ancak bir ürün için döndürülen verilere göz atın:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

`ActualCost` özelliği müşterilere görünür olmamalıdır! Çözüm, müşterilere görünür olması gereken özelliklerin bir alt kümesini içeren bir *veri aktarımı nesnesi* (DTO) tanımlamaktır. Örnekleri `ProductDTO` için LINQ for Project `Product` örnekleri kullanacağız.

Modeller klasörüne `ProductDTO` adlı bir sınıf ekleyin.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

Şimdi denetleyiciyi ekleyin. Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın. **Ekle**' yi ve ardından **Denetleyici**' yi seçin. **Denetleyici Ekle** iletişim kutusunda, denetleyiciyi &quot;productscontroller&quot;olarak adlandırın. **Şablon**altında **boş API denetleyicisi**' ni seçin.

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

Kaynak dosyadaki her şeyi aşağıdaki kodla değiştirin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

Denetleyici hala veritabanını sorgulamak için `OrdersContext` kullanır. Ancak `Product` örnekleri doğrudan döndürmek yerine, onları `ProductDTO` örneklerine eklemek için `MapProducts` çağırdık:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

`MapProducts` yöntemi bir **IQueryable**döndürür, bu nedenle sonucu diğer sorgu parametreleriyle oluşturabilirsiniz. Bunu sorguya bir **WHERE** yan tümcesi ekleyen `GetProduct` yönteminde görebilirsiniz:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a>Sipariş denetleyicisi ekleme

Daha sonra, kullanıcıların sipariş oluşturmalarına ve görüntülemesine imkan tanıyan bir denetleyici ekleyin.

Başka bir DTO ile başlayacağız. Çözüm Gezgini, modeller klasörüne sağ tıklayın ve `OrderDTO` adlı bir sınıf ekleyerek aşağıdaki uygulamayı kullanın:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

Şimdi denetleyiciyi ekleyin. Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın. **Ekle**' yi ve ardından **Denetleyici**' yi seçin. **Denetleyici Ekle** iletişim kutusunda aşağıdaki seçenekleri ayarlayın:

- **Denetleyici adı**bölümünde "orderscontroller" yazın.
- **Şablon**altında, "Entity Framework kullanarak okuma/yazma EYLEMLERI ile API denetleyicisi ' ni seçin.
- **Model sınıfı**altında &quot;Order (productstore. modeller)&quot;öğesini seçin.
- **Veri bağlamı sınıfı**altında &quot;OrdersContext (productstore. modeller)&quot;öğesini seçin.

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

**Ekle**'yi tıklatın. Bu, OrdersController.cs adlı bir dosya ekler. Sonra, denetleyicinin varsayılan uygulamasını değiştirmemiz gerekiyor.

İlk olarak, `PutOrder` ve `DeleteOrder` yöntemlerini silin. Bu örnekte, müşteriler mevcut siparişleri değiştiremez veya silemez. Gerçek bir uygulamada, bu durumları işlemek için çok sayıda arka uç mantığına ihtiyacınız vardır. (Örneğin, sipariş zaten sevk edildi mı?)

`GetOrders` yöntemini yalnızca kullanıcıya ait olan siparişleri döndürecek şekilde değiştirin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

`GetOrder` yöntemini aşağıdaki gibi değiştirin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

Bu yöntemde yaptığımız değişiklikler aşağıda verilmiştir:

- Dönüş değeri, bir `Order`yerine bir `OrderDTO` örneğidir.
- Sıraya yönelik veritabanını sorgulıyoruz, ilgili `OrderDetail` ve `Product` varlıklarını getirmek için [dbquery. Include](https://msdn.microsoft.com/library/gg696395) metodunu kullanırız.
- Bir projeksiyon kullanarak sonucu düzettik.

HTTP yanıtı, miktarları olan bir ürün dizisi içerir:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

Bu biçim, istemcilerin iç içe geçmiş varlıklar (sipariş, Ayrıntılar ve ürünler) içeren özgün nesne grafiğinden daha kolay kullanmasını sağlar.

`PostOrder`göz önünde bulundurmanız gereken son yöntem. Bu yöntem şu anda bir `Order` örneği alır. Ancak, bir istemci şöyle bir istek gövdesi gönderirse ne olacağını düşünün:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

Bu iyi yapılandırılmış bir sıradır ve Entity Framework, veritabanını veritabanına eklemesi gerekir. Ancak daha önce mevcut olmayan bir ürün varlığını içerir. İstemci, veritabanımızda yeni bir ürün oluşturdu! Bu, Koala yatak için bir sipariş görtiklerinde departmanı karşılama bölümünün bir şaşırmasını sağlar. Moral, bir POST veya PUT isteğinde kabul ettiğiniz veriler hakkında gerçekten dikkatli olun.

Bu sorundan kaçınmak için `PostOrder` yöntemini bir `OrderDTO` örneği alacak şekilde değiştirin. `Order`oluşturmak için `OrderDTO` kullanın.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

`ProductID` ve `Quantity` özelliklerini kullandığımızda, istemcinin ürün adı veya fiyat için gönderdiği tüm değerleri yok saydığımızda dikkat edin. Ürün KIMLIĞI geçerli değilse, veritabanındaki yabancı anahtar kısıtlamasını ihlal eder ve gerektiğinde ekleme işlemi başarısız olur.

İşte `PostOrder` yöntemi aşağıda verilmiştir:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

Son olarak, denetleyiciye **Yetkilendir** özniteliğini ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

Artık yalnızca kayıtlı kullanıcılar sipariş oluşturabilir veya görüntüleyebilir.

> [!div class="step-by-step"]
> [Önceki](using-web-api-with-entity-framework-part-5.md)
> [İleri](using-web-api-with-entity-framework-part-7.md)
