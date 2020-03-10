---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: '7\. Bölüm: özellik ekleme | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 7, hesap yeniden görünümü gibi ek özellikler ekler...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641997"
---
# <a name="part-7-adding-features"></a>7\. Bölüm: Özellik Ekleme

[ali Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir. Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 7, hesap incelemesi, Ürün İncelemeleri ve "popüler öğeler" ve "Ayrıca satın alınan" Kullanıcı denetimleri gibi ek özellikler ekler.

## <a id="_Toc260221673"></a>Özellik ekleme

Kullanıcılar kataloğumuza göz atabiliyor, bunları kendi alışveriş sepetine yerleştirse ve kullanıma alma işlemini tamamlayabilse de, sitemizi geliştirmek için dahil ettiğimiz birçok destekleyici özelliği vardır.

1. Hesap Incelemesi (verilen siparişleri listeleyin ve ayrıntıları görüntüleyin.)
2. İlk sayfaya belirli bir içeriğe özgü içerik ekleyin.
3. Kullanıcıların katalogdaki ürünleri Incelemesine izin vermek için bir özellik ekleyin.
4. Popüler öğeleri göstermek ve bu denetimi ön sayfaya yerleştirmek için bir kullanıcı denetimi oluşturun.
5. "Ayrıca satın alınmış" Kullanıcı denetimi oluşturun ve ürün ayrıntıları sayfasına ekleyin.
6. Kişi sayfası ekleyin.
7. Hakkında bir sayfa ekleyin.
8. Genel hata

## <a id="_Toc260221674"></a>Hesap Incelemesi

"Account" klasöründe, farklı bir OrderList. aspx adlı ve diğer adlandırılmış OrderDetails. aspx adlı iki. aspx sayfası oluşturun

OrderList. aspx, daha önce yaptığımız gibi GridView ve EntityDataSource denetimlerinden faydalanır.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSource, Kullanıcı oturumunun oturum açması sırasında bir oturum değişkeninde belirlediğimiz Kullanıcı adında (burada, bkz. parametre) filtrelenmiş Orders tablosundan kayıtlar seçer.

GridView 'un Hyperlinkalanındaki bu parametreleri de göz önünde bulabilirsiniz:

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

Bu, OrderDetails. aspx sayfasına bir QueryString parametresi olarak OrderID alanını belirten her ürün için sipariş ayrıntıları görünümünün bağlantısını belirtir.

## <a id="_Toc260221675"></a>OrderDetails. aspx

Siparişe ve bir FormView 'a erişmek için bir EntityDataSource denetimi kullanacağız ve tüm sipariş satır öğelerini görüntüleyen bir GridView ile başka bir EntityDataSource 'a sahiptir.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

Arka plan kodu dosyasında (OrderDetails.aspx.cs), iki adet evetme tutuyoruz.

İlk olarak OrderDetails 'in her zaman bir OrderID aldığından emin olmanız gerekir.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

Ayrıca, satır öğelerinden sipariş toplamını hesaplamakta ve görüntüleriz.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>Giriş sayfası

Default. aspx sayfasına bazı statik içerik ekleyelim.

İlk olarak bir "Içerik" klasörü ve bir Resimler klasörü oluşturacak (ana sayfada kullanılacak bir görüntü de ekleyeceğiz.)

Default. aspx sayfasının en alt yer tutucusuna aşağıdaki biçimlendirmeyi ekleyin.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>Ürün Incelemeleri

İlk olarak, bir ürün incelemesi girmek için kullandığımız bir formun bağlantısını içeren bir düğme ekleyeceğiz.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

ProductID 'yi sorgu dizesinde geçirdiğimiz unutulmamalıdır

Daha sonra, BelgeAdı \ Add. aspx adlı sayfayı ekleyelim

Bu sayfa, ASP.NET AJAX denetim araç setini kullanacaktır. Daha önce yapmadıysanız, [DevExpress](http://devexpress.com/act) 'den indirebilirsiniz ve burada [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)Visual Studio ile kullanmak üzere araç takımını ayarlamaya yönelik yönergeler vardır.

Tasarım modunda, araç kutusu ' ndan denetimleri ve Doğrulayıcıları sürükleyin ve aşağıdaki gibi bir form oluşturun.

![](tailspin-spyworks-part-7/_static/image2.jpg)

Biçimlendirme şuna benzer şekilde görünecektir.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

İncelemeleri girebilmemiz için artık bu İncelemeleri ürün sayfasında görüntülemesine olanak tanır.

Bu biçimlendirmeyi ProductDetails. aspx sayfasına ekleyin.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

Uygulamamızı şimdi çalıştırmak ve bir ürüne gitmek, müşteri incelemeleri dahil ürün bilgilerini gösterir.

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>Popüler öğeler denetimi (Kullanıcı denetimleri oluşturma)

Web sitenizdeki satışları artırmak için, "müstehcen satış" popüler veya ilgili ürünlere birkaç özellik ekleyeceğiz.

Bu özelliklerden ilki, ürün kataloğumuza ait daha popüler ürünün bir listesi olacaktır.

Uygulamamızın giriş sayfasında en çok satılan öğeleri göstermek için bir "Kullanıcı denetimi" oluşturacağız. Bu bir denetim olacağı için, Visual Studio tasarımcısında denetimi istediğiniz herhangi bir sayfada sürükleyip bırakarak bu denetimi herhangi bir sayfada kullanabiliriz.

Visual Studio 'nun Çözüm Gezgini ' nde çözüm adına sağ tıklayın ve "denetimler" adlı yeni bir dizin oluşturun. Bunun yapılması gerekli olmasa da, "denetimler" dizinindeki tüm Kullanıcı denetimlerimizi oluşturarak projemizi düzenli tutmaya yardımcı olacak.

Denetimler klasörüne sağ tıklayın ve "yeni öğe" yi seçin:

![](tailspin-spyworks-part-7/_static/image4.jpg)

"Popularıtems" denetiimizin bir adını belirtin. Kullanıcı denetimleri için dosya uzantısının. ascx değil. aspx olduğunu unutmayın.

Popüler öğelerimiz Kullanıcı denetimi, aşağıdaki gibi tanımlanacak.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

Burada, bu uygulamada henüz kullandığımız bir yöntemi kullanıyoruz. Yineleyici denetimini kullandık ve bir veri kaynağı denetimi kullanmak yerine, yineleyici denetimini bir LINQ to Entities sorgusunun sonuçlarına bağlamamız yapıyoruz.

Denetiminizin arkasındaki kodda aşağıdaki gibi yaptık.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

Ayrıca Denetim işaretimizin en üstündeki bu önemli satırı göz önünde bulundurulın.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

En popüler öğeler dakika temelinde değiştirilmeyeceği için uygulamamız performansını artırmak üzere bir aching yönergesi ekleyebiliriz. Bu yönerge, Denetim kodunun yalnızca, denetimin önbelleğe alınan çıktısı zaman aşımına uğradığında yürütülmesine neden olur. Aksi takdirde, denetimin çıktısının önbelleğe alınmış sürümü kullanılacaktır.

Şimdi yaptığımız tek şey, default. aspx sayfamızda yeni denetimimizi içerir.

Bir denetimin örneğini varsayılan formumuzu Aç sütununa yerleştirmek için sürükle ve bırak öğesini kullanın.

![](tailspin-spyworks-part-7/_static/image5.jpg)

Uygulamamızı çalıştırdığımızda, giriş sayfasında en popüler öğeler görüntülenir.

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>"Ayrıca satın alınan" denetim (parametrelerle Kullanıcı denetimleri)

Oluşturacağımız ikinci Kullanıcı denetimi, bağlam özelliği ekleyerek bir sonraki düzeye göre daha fazla satıyor olacaktır.

En üstteki "Ayrıca satın alınan" öğeleri hesaplama mantığı önemsiz değildir.

"Ayrıca satın almış olan" denetim, seçili olan ProductID için OrderDetails kayıtlarını (daha önce satın alınan) seçer ve bulunan her benzersiz sipariş için OrderID 'leri alacak.

Ardından, tüm bu siparişlerden ürünleri Al ' ı seçeceğiz ve satın alınan miktarları toplammız gerekir. Ürünleri bu miktar toplamına göre sıralayacak ve ilk beş öğeyi görüntüleyecek.

Bu mantığın karmaşıklığı verildiğinde, bu algoritmayı saklı yordam olarak uygulayacağız.

Saklı yordam için T-SQL aşağıdaki gibidir.

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

Bu saklı yordamın (SelectPurchasedWithProducts) uygulamamıza dahil ettiğimiz sırada olduğunu ve belirttiğimiz Varlık Veri Modeli oluşturduğumuzdan, gereken tablo ve görünümlere ek olarak, Varlık Veri Modeli Bu saklı yordamı içermelidir.

Saklı yordama Varlık Veri Modeli erişmek için, işlevi içeri aktarmanız gerekir.

Çözüm Gezgini 'ndeki Varlık Veri Modeli çift tıklayarak tasarımcıda açın ve model tarayıcısını açın, sonra tasarımcıya sağ tıklayıp "Işlev Içeri aktarma Ekle" seçeneğini belirleyin.

![](tailspin-spyworks-part-7/_static/image1.png)

Bu işlem, bu iletişim kutusunu açar.

![](tailspin-spyworks-part-7/_static/image2.png)

Yukarıda gördüğünüz gibi alanları doldurun, "SelectPurchasedWithProducts" öğesini seçin ve içeri aktarılan işlevimizin adı için yordam adını kullanın.

"Tamam" a tıklayın.

Bunu yaptıktan sonra, modeldeki başka herhangi bir öğe olabileceğinden, saklı yordama göre programlayabilirsiniz.

Bu nedenle, "denetimlerimiz" klasöründe AlsoPurchased. ascx adlı yeni bir kullanıcı denetimi oluşturun.

Bu denetimin biçimlendirmesi, Popularıtems denetimine çok tanıdık gelecektir.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

Önemli farkı, öğenin işlenmesi, ürüne göre farklı olacağı için çıktıyı önbelleğe alma işlemlerdir.

ProductID, denetimin bir "özelliği" olacaktır.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

Denetimin PreRender olay işleyicisinde üç şey yapmak için göz yorduk.

1. ProductID 'nin ayarlandığından emin olun.
2. Geçerli bir ürünle satın alınmış ürünler olup olmadığını görün.
3. Bazı öğelerin #2 belirlendiği şekilde çıkışını yapın.

Saklı yordamı model aracılığıyla çağırmanın ne kadar kolay olduğunu öğrenin.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

"Ayrıca satın alındı" olduğunu belirlemekten sonra, yineleyicisi 'ni sorgu tarafından döndürülen sonuçlara bağlayabiliriz.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

"Ayrıca satın alınmış" öğeler yoksa kataloğumuzdan diğer popüler öğeleri görüntüleriz.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

"Ayrıca satın alınan" öğeleri görüntülemek için ProductDetails. aspx sayfasını açın ve AlsoPurchased denetimini, bu konumda görünmesini sağlamak üzere Çözüm Gezgini 'nden sürükleyin.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

Bu işlem, ProductDetails sayfasının en üstünde bulunan denetime bir başvuru oluşturur.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

AlsoPurchased Kullanıcı denetimi bir ProductID numarası gerektirdiğinden, sayfanın geçerli veri modeli öğesine karşı bir eval ekstresi kullanarak denetimizin ProductID özelliğini ayarlayacağız.

![](tailspin-spyworks-part-7/_static/image3.png)

Şimdi oluşturup çalıştırdığımızda bir ürüne gözattığınızda, "Ayrıca satın alındı" öğelerini görtik.

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-6.md)
> [İleri](tailspin-spyworks-part-8.md)
