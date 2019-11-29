---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: '3\. kısım: yönetici denetleyicisi oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600038"
---
# <a name="part-3-creating-an-admin-controller"></a>3\. kısım: yönetici denetleyicisi oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a>Yönetici denetleyicisi ekleme

Bu bölümde, ürünlerde CRUD (oluşturma, okuma, güncelleştirme ve silme) işlemlerini destekleyen bir Web API denetleyicisi ekleyeceğiz. Denetleyici, veritabanı katmanıyla iletişim kurmak için Entity Framework kullanacaktır. Bu denetleyici yalnızca yöneticiler tarafından kullanılabilir. Müşteriler, ürünlere başka bir denetleyici üzerinden erişir.

Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın. **Ekle** ve sonra **Denetleyici**' yi seçin.

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

**Denetleyici Ekle** iletişim kutusunda denetleyiciyi `AdminController`adlandırın. **Şablon**altında Entity Framework&quot;kullanarak okuma/yazma eylemleri Ile &quot;API denetleyicisi ' ni seçin. **Model sınıfı**altında "Product (productstore. modeller)" öğesini seçin. **Veri bağlamı**altında "yeni veri bağlamı&gt;&lt;" öğesini seçin.

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> **Model sınıfı** açılır liste herhangi bir model sınıfı göstermezse, projeyi derlediğinizden emin olun. Entity Framework yansıma kullanır, bu nedenle derlenen derlemeye ihtiyaç duyuyor.

"&lt;yeni veri bağlamı&gt;" seçildiğinde, **Yeni veri bağlamı** iletişim kutusu açılır. Veri bağlamını `ProductStore.Models.OrdersContext`olarak adlandırın.

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

**Yeni veri bağlamı** iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın. **Denetleyici Ekle** Iletişim kutusunda **Ekle**' ye tıklayın.

Projeye eklenen:

- **DbContext**'ten türetilen `OrdersContext` adlı bir sınıf. Bu sınıf, POCO modelleri ve veritabanı arasında Tutkallamayı sağlar.
- `AdminController`adlı bir Web API denetleyicisi. Bu denetleyici `Product` örneklerine CRUD işlemlerini destekler. Entity Framework iletişim kurmak için `OrdersContext` sınıfını kullanır.
- Web. config dosyasında yeni bir veritabanı bağlantı dizesi.

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

OrdersContext.cs dosyasını açın. Oluşturucunun, veritabanı bağlantı dizesinin adını belirttiğinden emin olun. Bu ad, Web. config dosyasına eklenen bağlantı dizesine başvurur.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

Aşağıdaki özellikleri `OrdersContext` sınıfına ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

Bir **Dbset** , sorgulanabilen bir varlık kümesini temsil eder. `OrdersContext` sınıfı için tüm liste aşağıda verilmiştir:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

`AdminController` sınıfı, temel CRUD işlevlerini uygulayan beş yöntemi tanımlar. Her yöntem, istemcinin çağırabileceği bir URI 'ye karşılık gelir:

| Controller yöntemi | Açıklama | {1&gt;URI&lt;1} | HTTP yöntemi |
| --- | --- | --- | --- |
| GetProducts | Tüm ürünleri alır. | API/ürünler | Al |
| GetProduct | KIMLIĞE göre bir ürün bulur. | API/ürünler/*kimlik* | Al |
| PutProduct | Bir ürünü güncelleştirir. | API/ürünler/*kimlik* | KONUR |
| PostProduct | Yeni bir ürün oluşturur. | API/ürünler | Yayınla |
| DeleteProduct | Bir ürünü siler. | API/ürünler/*kimlik* | DELETE |

Her yöntem, veritabanını sorgulamak için `OrdersContext` çağırır. Değişiklikleri veritabanında kalıcı hale getirmek için koleksiyonu değiştiren Yöntemler (PUT, POST ve DELETE) çağrısı `db.SaveChanges`. Denetleyiciler her HTTP isteği için oluşturulur ve sonra, bir yöntem döndürülmadan önce değişiklikleri kalıcı hale getirmek gerekir.

## <a name="add-a-database-initializer"></a>Veritabanı başlatıcısı ekleme

Entity Framework, veritabanını başlangıçta doldurmanıza ve modeller değiştiğinde veritabanını otomatik olarak yeniden oluşturmaya olanak tanıyan iyi bir özelliğe sahiptir. Bu özellik geliştirme sırasında faydalıdır, çünkü modelleri değiştirseniz bile, her zaman test verilerinize sahip olursunuz.

Çözüm Gezgini, modeller klasörüne sağ tıklayın ve `OrdersContextInitializer`adlı yeni bir sınıf oluşturun. Aşağıdaki uygulamada yapıştırın:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

**Dropcreatedatabaseifmodelchanges** sınıfından devralarak, model sınıflarını her değiştirtiğimiz zaman veritabanını Entity Framework. Entity Framework veritabanını oluşturduğunda (veya yeniden oluşturduğunda) tabloları doldurmak için **çekirdek** yöntemini çağırır. Örnek bir sipariş ve örnek bir sipariş eklemek için **çekirdek** yöntemi kullanıyoruz.

Bu özellik test için idealdir, ancak bir model sınıfı değiştirirse verilerinizi kaybedeceğinizi, üretim ortamında **Dropcreatedatabaseifmodelchanges** sınıfını kullanmayın.

Ardından, Global. asax dosyasını açın ve aşağıdaki kodu **uygulama\_başlangıç** yöntemine ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a>Denetleyiciye Istek gönderme

Bu noktada hiçbir istemci kodu yazmadınız, ancak Web API 'sini bir Web tarayıcısı veya [Fiddler](http://www.fiddler2.com/fiddler2/)gıbı bir http hata ayıklama aracı kullanarak çağırabilirsiniz. Visual Studio 'da hata ayıklamayı başlatmak için F5 tuşuna basın. Web tarayıcınız `http://localhost:*portnum*/`için açılır; burada *portnum* , bir bağlantı noktası numarasıdır.

"`http://localhost:*portnum*/api/admin`öğesine HTTP isteği gönderin. Entity Framework veritabanının oluşturulması ve sağlaması gerektiğinden, ilk isteğin tamamlanabilmesi yavaş olabilir. Yanıt aşağıdakine benzer bir şey olmalıdır:

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> [Önceki](using-web-api-with-entity-framework-part-2.md)
> [İleri](using-web-api-with-entity-framework-part-4.md)
