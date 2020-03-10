---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4\. Bölüm: ürünleri listeleme | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 4\. bölüm, GridView contenr ile ürünleri listelemeyi içerir...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566985"
---
# <a name="part-4-listing-products"></a>4\. Bölüm: Ürünleri Listeleme

[ali Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir. Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 4\. bölüm, GridView denetimiyle ürünlerin dökümünü içerir.

## <a id="_Toc260221670"></a>GridView denetimiyle ürünleri listeleme

Çözümünüzde "sağ tıklayıp" "Ekle" ve "yeni öğe" seçeneğini belirleyerek ProductsList. aspx sayfamızı uygulamaya başlayalım.

![](tailspin-spyworks-part-4/_static/image1.jpg)

"Ana sayfa kullanarak Web formu" seçeneğini belirleyin ve ProductsList. aspx "bir sayfa adı girin.

"Ekle" ye tıklayın.

![](tailspin-spyworks-part-4/_static/image2.jpg)

Ardından, site. Master sayfasını yerleştirdiğiniz "stiller" klasörünü seçin ve "klasör Içeriği" penceresinden seçin.

![](tailspin-spyworks-part-4/_static/image3.jpg)

Sayfayı oluşturmak için "Tamam" a tıklayın.

Veritabanımız aşağıda görüldüğü gibi ürün verileriyle doldurulmuştur.

![](tailspin-spyworks-part-4/_static/image4.jpg)

Sayfanız oluşturulduktan sonra, bu ürün verilerine erişmek için bir varlık veri kaynağı kullanacağız, ancak bu örnekte ürün varlıklarını seçmemiz gerekir ve döndürülen öğeleri yalnızca seçili kategoriye ait olanlarla kısıtlayacağız.

Bunu gerçekleştirmek için, EntityDataSource 'un WHERE yan tümcesini otomatik olarak oluşturmasını söyleyecektir ve WHERE parametresini belirteceğiz.

"Ürün kategorisi menüsündeki" menü öğelerini oluşturduğumuzda bu bağlantıyı, her bir bağlantı için QueryString öğesine CategoryID ekleyerek dinamik olarak oluşturuyoruz. Varlık veri kaynağına, bu QueryString parametresinden WHERE parametresini türetmesini söylüreceğiz.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

Daha sonra, ListView denetimini ürünlerin bir listesini görüntüleyecek şekilde yapılandıracağız. En iyi bir alışveriş deneyimi oluşturmak için, ListVew 'imizde görüntülenecek olan her bir ürüne yönelik birkaç kısa özelliği sıkıştıracağız.

- Ürün adı ürünün ayrıntı görünümünün bir bağlantısı olacaktır.
- Ürünün fiyatı görüntülenir.
- Ürünün bir görüntüsü görüntülenir ve uygulamamızda bir katalog görüntüleri dizininden görüntüyü dinamik olarak seçeceğiz.
- Belirli ürünü, alışveriş sepetine hemen eklemek için bir bağlantı ekleyeceğiz.

ListView denetim örneğimiz için biçimlendirme aşağıda verilmiştir.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

Görüntülenen her ürün için birçok bağlantı dinamik olarak derleniyor.

Ayrıca, yeni sayfayı test etmeden önce, ürün kataloğu görüntülerinin dizin yapısını aşağıda gösterildiği gibi oluşturmanız gerekir.

![](tailspin-spyworks-part-4/_static/image1.png)

Ürün görüntülerimizin erişilebilir olması, ürün listesi sayfamızı test edebilir.

![](tailspin-spyworks-part-4/_static/image5.jpg)

Sitenin giriş sayfasından kategori listesi bağlantılarından birine tıklayın.

![](tailspin-spyworks-part-4/_static/image6.jpg)

Şimdi ProductDetails. aspx sayfasını ve AddToCart işlevini uygulamamız gerekir.

Daha önce yaptığımız gibi, site ana sayfasını kullanarak ProductDetails. aspx adlı bir sayfa adı oluşturmak için File-New&gt;kullanın.

Veritabanında belirli ürün kaydına erişmek için bir EntityDataSource denetimi kullanacağız ve ürün verilerini aşağıdaki gibi göstermek için bir ASP.NET FormView denetimi kullanacağız.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

Biçimlendirme biraz komik bir şekilde görünüyorsa endişelenmeyin. Yukarıdaki biçimlendirme, daha sonra uygulayacağımız birkaç özellik için görüntü düzeninde yer bırakır.

Alışveriş sepeti, uygulamamızda daha karmaşık mantığı temsil eder. Başlamak için File-&gt;New ' i kullanarak MyShoppingCart. aspx adlı bir sayfa oluşturun.

ShoppingCart. aspx adını seçmediğini unutmayın.

Veritabanımız "ShoppingCart" adlı bir tablo içeriyor. Bir Varlık Veri Modeli oluşturduğumuz veritabanındaki her tablo için bir sınıf oluşturuldu. Bu nedenle Varlık Veri Modeli, "ShoppingCart" adlı bir varlık sınıfı oluşturdu. Modeli, alışveriş sepeti uygulamamız için bu adı kullanabilmemiz veya gereksinimlerinize göre uzatmamız için düzenleyebiliriz, ancak çakışmayı önlemek için yalnızca bir ad seçmek yerine kabul edeceğiz.

Ayrıca, bir basit alışveriş sepeti oluşturmak ve alışveriş sepeti gösterimi ile alışveriş sepeti mantığını katıştırmak için de dikkat edin. Ayrıca, alışveriş sepetimizi tamamen ayrı bir Iş katmanında uygulamayı da tercih edebilirsiniz.

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-3.md)
> [İleri](tailspin-spyworks-part-5.md)
