---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: Bir denetleyiciden modelinizin verilerine erişme | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543752"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Bir Denetleyiciden Modelinizin Verilerine Erişme

[Scott Hanselman](https://github.com/shanselman) tarafından

> Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız. Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.

Bu bölümde yeni bir MoviesController sınıfı oluşturacağız ve film verilerimizi alan ve bir görünüm şablonu kullanarak tarayıcıya geri görüntüleyen bir kod yazacaksınız.

Denetleyiciler klasörüne sağ tıklayın ve yeni bir MoviesController oluşturun.

[![denetleyicisi ekleme](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

Bu işlem, projemizdeki \Controllers klasörü altında yeni bir "MoviesController.cs" dosyası oluşturur. Yeni doldurulan veritabanımızdan film listesini almak için MovieController 'ı güncelleştirelim.

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

Yalnızca 1984 Yaz 'dan sonra yayınlanan filmleri alabilmesi için bir LINQ sorgusu yaptık. Bu film listesini geri işlemek için bir görünüm şablonu gerekecektir, bu yüzden yöntemi sağ tıklayıp oluşturmak için Görünüm Ekle ' yi seçin.

Görünüm Ekle iletişim kutusunda, film&lt;bir liste geçirdiğimiz, görünüm şablonumuza film&gt;. Önceki sürelerden farklı olarak, Görünüm Ekle iletişim kutusunu kullandık ve "boş" bir şablon oluşturmayı tercih ediyoruz. bu kez, Visual Studio 'Nun bazı varsayılan içeriklerle ilgili bir görünüm şablonunu sizin için otomatik olarak "scafkatmayı" istediğini belirteceğiz. "İçerik görüntüle açılan menüsünden" liste "öğesini seçerek bunu yapacağız.

Yeni bir sınıf oluşturduğunuz zaman, Görünüm Ekle Iletişim kutusunda görünmesi için uygulamanızı derlemeniz gerektiğini unutmayın.

![Görünüm Ekle](getting-started-with-mvc-part5/_static/image3.png)

Ekle ' ye tıkladığınızda sistem, film listemizi görüntüleyen bir görünüm için kodu otomatik olarak oluşturur. Bu, daha önce Merhaba Dünya görünümünde yaptığımız gibi, &lt;H2&gt; başlığını "film listesi" gibi bir şekilde değiştirmek iyi bir zamandır.

[![filmler-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

Uygulamanızı çalıştırın ve adres çubuğunda/Filmler ' i ziyaret edin. Artık, denetleyicinin içindeki temel bir sorgu kullanarak veritabanından veri aldık ve verileri, film hakkında bilgi sahibi bir görünüme döndürtik. Bu görünümü daha sonra film listesinden dönerek ABD için bir veri tablosu oluşturur.

[![film listesi-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

Bu uygulamayla ilgili düzenleme, Ayrıntılar ve silme işlevlerini uygulamayız. bu nedenle, bizim için yapı iskelesi şablonunun oluşturduğu varsayılan bağlantılara gerek kalmaz. /Movies/Index.aspx dosyasını açın ve kaldırın.

Güncelleştirilmiş görünüm şablonumuza yönelik kaynak kodu, bu değişiklikleri yaptıktan sonra şöyle görünmelidir:

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

İhtiyaç duymayacağımız bağlantıları oluşturuyor, bu nedenle bunları bu örnek için sileceğiz. Yeni bağlantı oluşturduğumuz gibi, yeni bağlantımız da devam edeceğiz! Uygulamamız bu sütun kaldırılmış şekilde görünür.

[![film listesi-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

Şimdi film verilerimizden oluşan basit bir listemiz var. Ancak, "Yeni oluştur" bağlantısına tıkladığımızda, bağlanmadığımızda bir hata alırız! Bir oluşturma eylemi yöntemi uygulayalim ve bir kullanıcının veritabanımızda yeni filmler girmelerini olanaklı hale olalım.

> [!div class="step-by-step"]
> [Önceki](getting-started-with-mvc-part4.md)
> [İleri](getting-started-with-mvc-part6.md)
