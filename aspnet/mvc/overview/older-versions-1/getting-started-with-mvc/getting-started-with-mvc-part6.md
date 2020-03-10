---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: Oluşturma yöntemi ekleme ve görünüm oluşturma | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543661"
---
# <a name="adding-a-create-method-and-create-view"></a>Oluşturma Metodu ve Oluşturma Görünümü Ekleme

[Scott Hanselman](https://github.com/shanselman) tarafından

> Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız. Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.

Bu bölümde, kullanıcıların veritabanımızda yeni filmler oluşturmalarına olanak tanımak için gereken desteği uygulayacağız. Bunu/Movies/Create URL eylemini uygulayarak yapacağız.

/Movies/Create URL 'SI uygulamak iki adımlı bir işlemdir. Bir Kullanıcı/Movies/Create URL 'sini ilk kez ziyaret ettiğinde, yeni bir filmi girmek için dolduracakları bir HTML formu göstermek istiyoruz. Sonra, Kullanıcı formu gönderdiğinde ve verileri sunucuya geri gönderdiğinde, postalanan içerikleri almak ve veritabanınıza kaydetmek istiyoruz.

Bu iki adımı, MoviesController sınıfımızın içindeki iki Create () yöntemi içinde uygulayacağız. Bir yöntemde, kullanıcının yeni bir film oluşturmak için doldurması gereken &lt;formu&gt; gösterilir. İkinci yöntem, Kullanıcı &lt;form&gt; sunucuya geri gönderdiğinde ve veritabanı içinde yeni bir filmi kaydederken, gönderilen verilerin işlenmesini işleyecek.

Bunu uygulamak için MoviesController sınıfımızı ekleyeceğiniz kod aşağıda verilmiştir:

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

Yukarıdaki kod, denetleyicimiz dahilinde ihtiyaç duyduğumuz tüm kodu içerir.

Şimdi kullanıcıya form görüntülemek için kullanacağımız görünüm oluştur şablonunu uygulayalim. İlk oluşturma yöntemine sağ tıklayıp film formumuza yönelik görünüm şablonunu oluşturmak için "Görünüm Ekle" seçeneğini belirleyin.

Görünüm şablonunu görünüm veri sınıfı olarak bir "film" geçireceğiz ve "oluşturma" şablonu "scafkatlamak" isteyeceğiz.

[![Görünüm Ekle](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

Ekle düğmesine tıkladıktan sonra, \Movies\Create.aspx görünüm şablonu sizin için oluşturulur. "İçeriği görüntüle" açılan menüsünden "Oluştur" 'u seçtiğimiz için, Görünüm Ekle iletişim kutusu bizim için varsayılan içerikleri otomatik olarak "scafkatlama" olarak seçtik. Yapı iskelesi, bir HTML &lt;formu oluşturdu&gt;, doğrulama hatası iletileri için bir yer ve yapı iskelesi film hakkında bilgi sahibi olduğu için, sınıfımızın her bir özelliği için etiket ve alanları oluşturmuştur.

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

Veritabanımız otomatik olarak bir filmi bir KIMLIK verdiğinden, modele başvuran bu alanları kaldıralim. Oluşturma Görünümümüzden kimlik. &lt;&gt;göstergeden sonra 7 satırı kaldırın&lt;/Legend&gt; alanları, istediğimiz KIMLIK alanını gösterir.

Şimdi yeni bir film oluşturup veritabanına ekleyelim. Bunu uygulamayı yeniden çalıştırıp "/Filmler" URL 'sini ziyaret ederek ve yeni film eklemek için "Oluştur" bağlantısına tıklayarak yapacağız.

[![oluştur-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

Oluştur düğmesine tıkladığımızda, bu formdaki verileri yeni oluşturduğumuz/Movies/Create yöntemine geri göndereceğiz (HTTP POST aracılığıyla). Sistem, "numTimes" ve "Name" parametresini URL 'den otomatik olarak alıp daha önce bir yöntemde parametrelere eşleştirirse olduğu gibi, sistem otomatik olarak bir GÖNDERINDEN form alanlarını alır ve bunları bir nesne ile eşler. Bu durumda, HTML 'deki alanlardan "ReleaseDate" ve "title" gibi değerler otomatik olarak bir filmin yeni bir örneğinin doğru özelliklerine yerleştirilecek.

MoviesController bir kez ikinci oluşturma yöntemine göz atalım. Bağımsız değişken olarak "film" nesnesini nasıl aldığına dikkat edin:

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

Bu film nesnesi daha sonra oluşturma eylemi yönteminizin [HttpPost] sürümüne geçirilir ve bunu veritabanına kaydettik ve ardından Kullanıcı, kaydedilen sonucu film listesinde gösteren Index () eylem yöntemine geri yönlendirdik:

[![film listesi-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

Filmlerimizin doğru olup olmadığını denetliyoruz, ancak veritabanı başlık olmadan bir filmi kaydetmemize izin vermez. Kullanıcıya veritabanı hata vermeden önce bunu söylememiz durumunda bu iyi bir durum olabilir. Uygulamamıza doğrulama desteği ekleyerek bunu bir sonraki adımda yapacağız.

> [!div class="step-by-step"]
> [Önceki](getting-started-with-mvc-part5.md)
> [İleri](getting-started-with-mvc-part7.md)
