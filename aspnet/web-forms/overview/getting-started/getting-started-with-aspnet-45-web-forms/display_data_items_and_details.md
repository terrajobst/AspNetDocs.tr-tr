---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: Veri öğelerini ve ayrıntıları görüntüleme | Microsoft Docs
author: Erikre
description: Bu öğretici serisinde, ASP.NET 4,7 ve Microsoft Visual Studio 2017 ile bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgiler gösterilir
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641115"
---
# <a name="display-data-items-and-details"></a>Veri öğelerini ve ayrıntılarını görüntüleme

by [Erik Reitan](https://github.com/Erikre)

> Bu öğretici serisi, ASP.NET 4,7 ve Microsoft Visual Studio 2017 ile bir ASP.NET Web Forms uygulamasının oluşturulmasına ilişkin temel bilgileri öğretir.

Bu öğreticide, ASP.NET Web Forms ve Code First Entity Framework ile veri öğelerini ve veri öğesi ayrıntılarını görüntülemeyi öğreneceksiniz. Bu öğretici, Wingtip Oyunstore öğretici serisinin bir parçası olarak önceki "UI ve gezinti" öğreticisini oluşturur. Bu Öğreticiyi tamamladıktan sonra *Productslist. aspx* sayfasında ürünleri ve *ProductDetails. aspx* sayfasında bir ürünün ayrıntılarını görürsünüz.

## <a name="youll-learn-how-to"></a>Şunları öğrenirsiniz:

- Veritabanındaki ürünleri göstermek için bir veri denetimi ekleyin
- Veri denetimini seçili verilere bağlama
- Veritabanından ürün ayrıntılarını göstermek için bir veri denetimi ekleyin
- Sorgu dizesinden bir değer alın ve veritabanından alınan verileri sınırlamak için bu değeri kullanın

### <a name="features-introduced-in-this-tutorial"></a>Bu öğreticide tanıtılan Özellikler:

- Model bağlama
- Değer sağlayıcıları

## <a name="add-a-data-control"></a>Veri denetimi ekleme

Bir sunucu denetimine veri bağlamak için birkaç farklı seçenek kullanabilirsiniz. En yaygın şunlar şunlardır:

* Veri kaynağı denetimi ekleme
* El ile kod ekleme
* Model bağlamayı kullanma

### <a name="use-a-data-source-control-to-bind-data"></a>Veri bağlamak için bir veri kaynağı denetimi kullanın

Veri kaynağı denetimi eklemek, veri kaynağı denetimini verileri görüntüleyen denetime bağlayabilmeniz için izin verir. Bu yaklaşımda, programlı olarak değil, sunucu tarafı denetimlerini veri kaynaklarına bağlamak için bildirimli olarak kullanabilirsiniz.

### <a name="code-by-hand-to-bind-data"></a>Verileri bağlamak için el ile kod

El ile kodlama şunları içerir:

1. Bir değer okunuyor
2. Null olup olmadığı denetleniyor
3. Uygun bir türe dönüştürülüyor
4. Dönüştürme başarılı denetleniyor
5. Sorgudaki değeri kullanma 

Bu yaklaşım, veri erişim mantığınız üzerinde tam denetime sahip olmanızı sağlar.

### <a name="use-model-binding-to-bind-data"></a>Veri bağlamak için model bağlamayı kullanma

Model bağlama, sonuçları çok daha az kodla bağlamanızı sağlar ve uygulamanızı genelinde işlevselliği yeniden kullanma olanağı sunar. Hala zengin, veri bağlama çerçevesi sağlarken kod odaklı veri erişim mantığı ile çalışmayı basitleştirir.

## <a name="display-products"></a>Ürünleri görüntüleme

Bu öğreticide, veri bağlamak için model bağlamayı kullanacaksınız. Veri seçmek üzere model bağlamayı kullanmak üzere bir veri denetimi yapılandırmak için, denetimin `SelectMethod` özelliğini sayfanın kodundaki bir yöntem adına ayarlarsınız. Veri denetimi, yöntemi sayfa yaşam döngüsünde uygun zamanda çağırır ve döndürülen verileri otomatik olarak bağlar. `DataBind` yöntemi açıkça çağrılmaya gerek yoktur.

1. **Çözüm Gezgini**, *ProductList. aspx*' i açın.
2. Var olan işaretlemeyi bu biçimlendirme ile değiştirin:   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

Bu kod, ürünleri göstermek için `productList` adlı bir **ListView** denetimi kullanır.

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

Şablonlar ve stiller ile **ListView** denetiminin verileri nasıl görüntülediğini tanımlarsınız. Herhangi bir yinelenen yapıdaki veriler için faydalıdır. Bu **ListView** örneği yalnızca veritabanı verilerini görüntülüyor olsa da, kod olmadan, kullanıcıların verileri düzenlemesini, eklemesini ve silmesini ve verileri sıralama ve görüntüleme olanağı sağlar.

**ListView** denetimindeki `ItemType` özelliğini ayarlayarak, veri bağlama ifadesi `Item` kullanılabilir ve denetimin türü kesin olarak belirlenmiş olur. Önceki öğreticide belirtildiği gibi, `ProductName`belirtmek gibi IntelliSense ile öğe nesnesi ayrıntılarını seçebilirsiniz:

![Veri öğelerini ve ayrıntıları görüntüleme-IntelliSense](display_data_items_and_details/_static/image1.png)

Ayrıca, `SelectMethod` bir değer belirtmek için model bağlama de kullanıyorsunuz. Bu değer (`GetProducts`), sonraki adımda ürünlerin gösterilmesi için arka plandaki koda ekleyeceğiniz yönteme karşılık gelir.

### <a name="add-code-to-display-products"></a>Ürünleri göstermek için kod ekleme

Bu adımda, veritabanındaki ürün verileriyle **ListView** denetimini doldurmak için kod ekleyeceksiniz. Kod, tüm ürünlerin ve bireysel kategori ürünlerinin gösterilmesini destekler.

1. **Çözüm Gezgini**, *ProductList. aspx* öğesine sağ tıklayın ve ardından **kodu görüntüle**' yi seçin.
2. *ProductList.aspx.cs* dosyasındaki mevcut kodu şu kodla değiştirin:   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

Bu kod, **ListView** denetiminin `ItemType` özelliğinin *ProductList. aspx* sayfasında başvurduğu `GetProducts` yöntemini gösterir. Sonuçları belirli bir veritabanı kategorisiyle sınırlamak için, kod *ProductList. aspx* sayfasına gidildiği zaman *ProductList. aspx* sayfasına geçirilen sorgu dizesi değerindeki `categoryId` değerini ayarlar. `System.Web.ModelBinding` ad alanındaki `QueryStringAttribute` sınıfı, `id`sorgu dizesi değişkeninin değerini almak için kullanılır. Bu, model bağlamaya, sorgu dizesinden bir değeri, çalışma zamanında `categoryId` parametresine bağlamayı denemeye yönlendirir.

Geçerli bir kategori bir sorgu dizesi olarak sayfaya geçirildiğinde, sorgunun sonuçları, veritabanındaki `categoryId` değerle eşleşen bu ürünlerle sınırlıdır. Örneğin, *Productslist. aspx* sayfası URL 'si ise:

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

Sayfa yalnızca `categoryId` `1`eşit olan ürünleri görüntüler.

Tüm ürünler, *ProductList. aspx* sayfası çağrıldığında hiçbir sorgu dizesi dahil edilmediğinde görüntülenir.

Bu yöntemlere ait değer kaynakları, *değer sağlayıcıları* ( *QueryString*gibi) olarak adlandırılır ve kullanılacak değer sağlayıcısını belirten parametre öznitelikleri, *değer sağlayıcı öznitelikleri* (örneğin, `id`) olarak adlandırılır. ASP.NET, sorgu dizesi, tanımlama bilgileri, form değerleri, denetimler, Görünüm durumu, oturum durumu ve profil özellikleri gibi Web Forms bir uygulamadaki tüm tipik Kullanıcı girişi kaynakları için değer sağlayıcıları ve karşılık gelen öznitelikler içerir. Ayrıca, özel değer sağlayıcıları yazabilirsiniz.

### <a name="run-the-application"></a>Uygulamayı çalıştırma

Tüm ürünleri veya bir kategorinin ürünlerini görüntülemek için uygulamayı şimdi çalıştırın.

1. Uygulamayı çalıştırmak için Visual Studio 'da **F5** tuşuna basın.  
   Tarayıcı açılır ve *default. aspx* sayfasını gösterir.

2. Ürün kategorisi gezinti menüsünden **otomobilleri** seçin.  
   *ProductList. aspx* sayfası yalnızca **araba** kategorisi ürünlerini gösterir. Bu öğreticide daha sonra ürün ayrıntıları görüntülenir.  

    ![Veri öğelerini ve ayrıntılarını görüntüleme-otomobiller](display_data_items_and_details/_static/image2.png)

3. Üstteki gezinti menüsünden **Ürünler** ' i seçin.  
   Ayrıca, *ProductList. aspx* sayfası görüntülenir, ancak bu kez tüm ürün listesini gösterir.   

    ![Veri öğelerini ve ayrıntıları görüntüleme-ürünler](display_data_items_and_details/_static/image3.png)

4. Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.

### <a name="add-a-data-control-to-display-product-details"></a>Ürün ayrıntılarını göstermek için bir veri denetimi ekleyin

Daha sonra, belirli ürün bilgilerini göstermek için önceki öğreticide eklediğiniz *ProductDetails. aspx* sayfasındaki biçimlendirmeyi değiştireceksiniz.

1. **Çözüm Gezgini**' de *ProductDetails. aspx*' i açın.

2. Var olan işaretlemeyi bu biçimlendirme ile değiştirin:

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    Bu kod, belirli ürün ayrıntılarını göstermek için bir **FormView** denetimi kullanır. Bu biçimlendirme, *ProductList. aspx* sayfasında verileri göstermek için kullanılan yöntemler gibi yöntemleri kullanır. **FormView** denetimi, bir veri kaynağından tek seferde tek bir kayıt göstermek için kullanılır. **FormView** denetimini kullandığınızda, veri bağlantılı değerleri göstermek ve düzenlemek için şablonlar oluşturursunuz. Bu şablonlar denetimleri, bağlama ifadelerini ve formun görünümünü ve işlevselliğini tanımlayan biçimlendirmeyi içerir.

Önceki biçimlendirmeyi veritabanına bağlamak ek kod gerektirir.

1. **Çözüm Gezgini**, *ProductDetails. aspx* öğesine sağ tıklayın ve ardından **kodu görüntüle**' ye tıklayın.  
   *ProductDetails.aspx.cs* dosyası görüntülenir.

2. Mevcut kodu şu kodla değiştirin:   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

Bu kod, bir "`productID`" sorgu dizesi değeri olup olmadığını denetler. Geçerli bir sorgu dizesi değeri bulunursa, eşleşen ürün görüntülenir. Sorgu dizesi bulunmazsa veya değeri geçerli değilse, ürün gösterilmez.

### <a name="run-the-application"></a>Uygulamayı çalıştırma

Artık, ürün KIMLIĞI temelinde bir ürünün görüntülendiğini görmek için uygulamayı çalıştırabilirsiniz.

1. Uygulamayı çalıştırmak için Visual Studio 'da **F5** tuşuna basın.  
   Tarayıcı açılır ve *default. aspx* sayfasını gösterir.

2. Kategori gezinti menüsünden **Boats** öğesini seçin.  
   *ProductList. aspx* sayfası görüntülenir.

3. Ürün listesinden **Kağıt bot** ' ı seçin.
   *ProductDetails. aspx* sayfası görüntülenir.

    ![Veri öğelerini ve ayrıntıları görüntüleme-ürünler](display_data_items_and_details/_static/image4.png)
    
4. Tarayıcıyı kapatın.

## <a name="additional-resources"></a>Ek kaynaklar

[Model bağlama ve Web formları ile verileri alma ve görüntüleme](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, ürünleri ve ürün ayrıntılarını göstermek için biçimlendirme ve kod eklediniz. Kesin tür belirtilmiş veri denetimleri, model bağlama ve değer sağlayıcıları hakkında bilgi edindiniz. Sonraki öğreticide, Wingtip Toys örnek uygulamasına bir alışveriş sepeti ekleyeceksiniz. 

> [!div class="step-by-step"]
> [Önceki](ui_and_navigation.md)
> [İleri](shopping-cart.md)
