---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: Modele sütun ekleme | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543584"
---
# <a name="adding-a-column-to-the-model"></a>Modele Sütun Ekleme

[Scott Hanselman](https://github.com/shanselman) tarafından

> Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız. Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.

Bu bölümde, veritabanımızın şemasında nasıl değişiklik yapacağımız ve uygulamamız içindeki değişiklikleri işleyebiliriz.

Film tablosuna bir "derecelendirme" sütunu ekleyelim. IDE 'ye dönün ve Veritabanı Gezgini tıklayın. Film tablosuna sağ tıklayıp tablo tanımını aç ' ı seçin.

Aşağıda görüldüğü gibi bir "derecelendirme" sütunu ekleyin. Artık hiç derecelendirme olmadığından, sütun null değerlere izin verebilir. Kaydet’e tıklayın.

[![filmlerini tabloları Düzenle](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

Sonra, Çözüm Gezgini dönün ve filmler. edmx dosyasını açın (\Modeller klasöründe bulunur). Tasarım yüzeyine (beyaz alan) sağ tıklayın ve modeli veritabanından Güncelleştir ' i seçin.

[![filmler-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

Bu, "Güncelleştirme Sihirbazı" nı başlatacaktır. İçindeki Yenile sekmesine tıklayın ve son ' a tıklayın. Ardından, film modeli sınıfımız yeni sütunla güncelleştirilecektir.

![Güncelleştirme Sihirbazı (2)](getting-started-with-mvc-part8/_static/image5.png)

Son ' a tıkladıktan sonra modelimizin film varlığına yeni derecelendirme sütununun eklendiğini görebilirsiniz.

[![filmi varlık](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

Veritabanı modeline bir sütun ekledik, ancak görünümler bunun hakkında bilgi sahibi değil.

## <a name="update-views-with-model-changes"></a>Model değişiklikleriyle görünümleri güncelleştirme

Yeni derecelendirme sütununu yansıtmak için görünüm şablonlarımızı güncelleştirebilmemiz için birkaç yol vardır. Bu görünümleri Görünüm Ekle iletişim kutusu aracılığıyla oluşturduğumuz için bunları silip yeniden oluşturarız. Bununla birlikte, genellikle insanlar ilk scafkatnesten görünüm şablonlarında değişiklikler yapmış olur ve oluşturma için KIMLIK alanına yaptığımız gibi alanları el ile eklemek veya silmek olacaktır.

\Views\Movies\Index.aspx şablonunu açın ve film tablosunun baş &lt;&gt;derecelendirme&lt;/TH&gt; ekleyin. Tarzı sonra mayın ekledim. Ardından, aynı sütun konumunda, ancak aşağı doğru, yeni Derecelendirmem için bir satır ekleyin.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

Son Index. aspx şablonumuz şöyle görünür:

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

Daha sonra \Views\Movies\Create.aspx şablonunu açıp yeni derecelendirme özelliği için bir etiket ve metin kutusu ekleyin:

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

Son Create. aspx şablonumuz bu şekilde görünür ve tarayıcının başlığını ve ikincil &lt;H2&gt; başlığını burada "film oluşturma" gibi bir şekilde değiştirelim!

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

Uygulamanızı çalıştırın ve şimdi oluştur sayfasına eklenen veritabanında yeni bir alanınız var. Yeni bir film ekleyin-bu kez bir derecelendirmeye sahip ve Oluştur ' a tıklayın.

[Film oluşturma-Windows Internet Explorer ![](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

Oluştur ' a tıkladıktan sonra, yeni filmin veritabanındaki yeni derecelendirme sütunuyla listelendiği dizin sayfasına gönderilir

[![film listesi-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

Bu temel öğretici, denetleyicileri oluşturma, bunları görünümlerle ilişkilendirme ve sabit kodlanmış verileri geçirme konusunda çalışmaya başladım. Daha sonra bir veritabanı oluşturulup tasarlıyoruz ve veri yerleştirdik. Veritabanından alınan verileri aldık ve bir HTML tablosunda görüntüliyoruz. Daha sonra kullanıcının Web uygulamasının içinden veritabanına veri eklemesine izin veren bir oluşturma formu ekledik. Doğrulama ekledik, sonra doğrulamayı istemci tarafında JavaScript 'ı kullanacak şekilde yaptık. Son olarak, veritabanını yeni bir veri sütunu içerecek şekilde değiştirdik ve bu yeni verileri oluşturmak ve göstermek için iki sayfamızı güncelleştiririz.

Artık ASP.NET MVC hakkında daha fazla bilgi edinmek için [https://asp.net/mvc](https://asp.net/mvc) ' de ara düzeyi Öğreticimize "[MVC müzik mağazamız](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" ve birçok video ve kaynak üzerinde geçiş yapmayı öneririz!

Keyfini çıkarın!

- Scott Hanselman-Twitter 'da [http://hanselman.com](http://hanselman.com) ve [@shanselman](http://twitter.com/shanselman) .

> [!div class="step-by-step"]
> [Öncekini](getting-started-with-mvc-part7.md)
