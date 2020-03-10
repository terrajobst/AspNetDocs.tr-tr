---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: Modele doğrulama ekleme | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543647"
---
# <a name="adding-validation-to-the-model"></a>Modele Doğrulama Ekleme

[Scott Hanselman](https://github.com/shanselman) tarafından

> Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız. Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.

Bu bölümde, uygulamamız içinde giriş doğrulamasını etkinleştirmek için gereken desteği uygulayacağız. Veritabanı içeriğimizin her zaman doğru olduğundan ve geçerli olmayan film verilerini girerken son kullanıcılara faydalı hata iletileri sağlamasına emin olacağız. Film sınıfına küçük bir doğrulama mantığı ekleyerek başlayacağız.

Model klasörüne sağ tıklayın ve sınıf Ekle ' yi seçin. Sınıf filminizi adlandırın.

Daha önce film varlığı modelini oluşturduğumuz, IDE bir film sınıfı oluşturdu. Aslında, film sınıfının bir bölümü bir dosyada ve başka bir bölümde olabilir. Buna kısmi bir sınıf denir. Film sınıfını başka bir dosyadan genişletecekiz.

Sisteme doğrulama ipuçları veren bazı özniteliklerle "arkadaş sınıfına" işaret eden kısmi bir film sınıfı oluşturacağız. Başlığı ve fiyatı gerekli olarak işaretleyecek ve ayrıca fiyatın belirli bir aralıkta yer aldığı insist. Modeller klasörüne sağ tıklayın ve sınıf Ekle ' yi seçin. Sınıf filminizi adlandırın ve Tamam düğmesine tıklayın. Kısmi film sınıfımız şöyle görünür.

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

Uygulamanızı yeniden çalıştırın ve 100 üzerinden fiyata sahip bir filmi girmeyi deneyin. Formu gönderdikten sonra bir hata alırsınız. Hata sunucu tarafında yakalanır ve form gönderildikten sonra gerçekleşir. ASP.NET MVC 'nin yerleşik HTML yardımcıların hata iletisini görüntülemesi ve metin kutusu öğelerinde ABD için değerleri korumak üzere yeterince akıllı olduğunu fark edin:

[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)

Bu harika bir işe yarar, ancak kullanıcıya sunucu dahil etmeden önce istemci tarafında, hemen bir şekilde söyleyebildiğimiz için bu iyi bir yoldur.

JavaScript ile bazı istemci tarafı doğrulanmasını etkinleştirelim.

## <a name="adding-client-side-validation"></a>Istemci tarafı doğrulama ekleme

Film sınıfımızın zaten bazı doğrulama öznitelikleri olduğundan, Create. aspx görünüm şablonumuza birkaç JavaScript dosyası eklememiz ve istemci tarafı doğrulamanın gerçekleşmesini sağlamak için bir kod satırı eklemeniz yeterlidir.

VWD içinden Görünümlerimize/film klasörmize gidip Create. aspx ' i açın.

Çözüm Gezgini betikler klasörünü açın ve aşağıdaki üç komut dosyasını &lt;Head&gt; etiketi içinde sürükleyin.

- MicrosoftAjax.js
- MicrosoftMvcValidation.js

Bu komut dosyalarının bu sırada görünmesini istiyorsunuz.

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

Ayrıca, bu tek satırı HTML. BeginForm üzerine ekleyin:

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

IDE içinde gösterilen kod aşağıda verilmiştir.

[![filmler-Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)

Uygulamanızı çalıştırın ve/Movies/Create yeniden ziyaret edin ve herhangi bir veri girmeden oluştur ' a tıklayın. Hata iletileri, sunucu Flash olmadan hemen görünür ve bu, verileri sunucuya geri gönderme ile ilişkilendirdik. Bunun nedeni, ASP.NET MVC 'nin hem istemcide (JavaScript kullanılarak) hem de sunucusunda girişi doğrulamadır.

[![oluştur-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)

Bu iyi bir fikir! Şimdi veritabanına başka bir sütun ekleyelim.

> [!div class="step-by-step"]
> [Önceki](getting-started-with-mvc-part6.md)
> [İleri](getting-started-with-mvc-part8.md)
