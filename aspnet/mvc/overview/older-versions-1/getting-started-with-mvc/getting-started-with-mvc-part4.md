---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: Veritabanı oluşturma | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581440"
---
# <a name="creating-a-database"></a>Veritabanı Oluşturma

[Scott Hanselman](https://github.com/shanselman) tarafından

> Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız. Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.

Bu bölümde, film Verilerimizi depolamak ve almak için kullanacağımız yeni bir SQL Express veritabanı oluşturacağız. Visual Web Developer IDE içinden Görünüm ' ü seçin | Sunucu Gezgini. Veri bağlantıları ' na sağ tıklayıp bağlantı ekle... ' ye tıklayın.

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

Veri kaynağı seç iletişim kutusunda Microsoft SQL Server ' ı seçin ve devam ' ı seçin.

![](getting-started-with-mvc-part4/_static/image2.png)

Bağlantı Ekle iletişim kutusunda, sunucu adınız için ".\SQLEXPRESS" yazın ve yeni veritabanınızın adı olarak "Filmler" yazın.

[![bağlantı iletişim kutusu Ekle](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

Tamam ' a tıkladığınızda bu veritabanını oluşturmak isteyip istemediğiniz sorulur. Evet ' i seçin.

[![film oluşturmak mı istiyorsunuz?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

Artık Sunucu Gezgini boş bir veritabanınız var.

![Yeni Tablo Ekle](getting-started-with-mvc-part4/_static/image7.png)

Tablolar ' a sağ tıklayıp tablo Ekle ' ye tıklayın. Tablo Tasarımcısı görüntülenir. Kimlik, başlık, ReleaseDate, tarz ve fiyat için sütun ekleyin. KIMLIK sütununa sağ tıklayıp birincil anahtarı ayarla ' ya tıklayın. Tasarım alanlarım şu şekilde görünür.

[![veritabanı tablo Düzenleyicisi](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

Ayrıca, kimlik sütununu seçin ve aşağıdaki sütun özellikleri altında "kimlik belirtimi" ni "Evet" olarak değiştirin.

[![IsIdentity-Column özellikleri](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

Bitirdiğinizde, araç çubuğundaki Kaydet simgesine tıklayın veya dosya ' yı seçin | Menüden kaydedin ve tablonuzu "**film**" (tekil) olarak adlandırın. Bir veritabanı ve tablo aldık!

[![ad seçin](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

Sunucu Gezgini ' ye dönüp film tablosuna sağ tıklayıp "tablo verilerini göster" i seçin. Veritabanınızda bazı veriler olduğundan birkaç film girin.

[Veritabanı tablosu düzenlemesini ![](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>Model Oluşturma

Şimdi, IDE 'nin sağ tarafındaki Çözüm Gezgini geri dönün ve modeller klasörüne sağ tıklayıp Ekle | ' yi seçin. Yeni öğe.

[![addnewmodelıdıtem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

Yeni veritabanımızda bir varlık modeli oluşturacağız. Bu, projemizi, veritabanımızın içindeki verileri sorgulamanızı ve işlememizi kolaylaştıran bir sınıf kümesi ekler. İletişim kutusunun sol tarafındaki veri düğümünü seçin ve ardından ADO.NET Varlık Veri Modeli öğesi şablonunu seçin. It. edmx olarak adlandırın.

[AddNewDataModel ![](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

"Ekle" düğmesine tıklayın. Bu daha sonra "Varlık Veri Modeli Sihirbazı" nı başlatacaktır.

Açılan yeni iletişim kutusunda veritabanından oluştur ' u seçin. Yeni bir veritabanı oluşturduğumuzdan, yalnızca yeni veritabanımız ve tablosuyla ilgili Entity Framework söylememiz gerekir. Veritabanı bağlantınızı web uygulamamız yapılandırması ' nda kaydetmek için Ileri ' ye tıklayın. Şimdi tablolar ve film onay kutusunu işaretleyip son ' a tıklayın.

[![Varlık Veri Modeli Sihirbazı](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

Şimdi yeni film tabloımızı Entity Framework Designer görebilir ve koddan bu tabloya erişebilirsiniz.

[![filmler-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

Tasarım yüzeyinde bir "film" sınıfı görebilirsiniz. Bu sınıf, veritabanımızda "film" tablosuyla eşlenir ve içindeki her bir özellik tabloyla eşleşen bir sütunla eşlenir. Bir "film" sınıfının her örneği, "film" tablosu içindeki bir satıra karşılık gelir.

Entity Framework tarafından kullanılan varsayılan adlandırma ve eşleme kurallarını beğenmezseniz, bunları değiştirmek veya özelleştirmek için Entity Framework tasarımcısını kullanabilirsiniz. Bu uygulama için Varsayılanları kullanacağız ve dosyayı olduğu gibi kaydetmelisiniz.

Şimdi, bazı gerçek verilerle çalışalım!

> [!div class="step-by-step"]
> [Önceki](getting-started-with-mvc-part3.md)
> [İleri](getting-started-with-mvc-part5.md)
