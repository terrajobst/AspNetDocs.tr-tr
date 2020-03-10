---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Veritabanını temel almak için Code First Migrations kullanın | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557458"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a>Veritabanını temel almak için Code First Migrations kullanın

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Bu bölümde, veritabanını test verileriyle temel almak için EF 'te [Code First Migrations](https://msdn.microsoft.com/data/jj591621) kullanacaksınız.

**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-console[Main](part-3/samples/sample1.cmd)]

Bu komut, projenize geçişler adlı bir klasör ve geçişler klasöründe Configuration.cs adlı bir kod dosyası ekler.

![](part-3/_static/image1.png)

Configuration.cs dosyasını açın. Aşağıdaki **using** ifadesini ekleyin.

[!code-csharp[Main](part-3/samples/sample2.cs)]

Ardından aşağıdaki kodu **Configuration. tohum** yöntemine ekleyin:

[!code-csharp[Main](part-3/samples/sample3.cs)]

Paket Yöneticisi konsolu penceresinde aşağıdaki komutları yazın:

[!code-console[Main](part-3/samples/sample4.cmd)]

İlk komut veritabanını oluşturan kodu oluşturur ve ikinci komut bu kodu yürütür. Veritabanı yerel olarak, [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)kullanılarak oluşturulur.

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>API 'YI keşfet (Isteğe bağlı)

Uygulamayı hata ayıklama modunda çalıştırmak için F5 tuşuna basın. Visual Studio IIS Express başlar ve Web uygulamanızı çalıştırır. Daha sonra Visual Studio bir tarayıcı başlatır ve uygulamanın giriş sayfasını açar.

Visual Studio bir Web projesi çalıştırdığında, bir bağlantı noktası numarası atar. Aşağıdaki görüntüde, bağlantı noktası numarası 50524 ' dir. Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görürsünüz.

![](part-3/_static/image3.png)

Giriş sayfası ASP.NET MVC kullanılarak uygulanır. Sayfanın üst kısmında, "API" yazan bir bağlantı vardır. Bu bağlantı sizi, Web API 'SI için otomatik olarak oluşturulan bir yardım sayfasına getirir. (Bu yardım sayfasının nasıl oluşturulduğunu ve sayfaya kendi belgelerinizi nasıl ekleyebileceğiniz hakkında bilgi edinmek için bkz. [ASP.NET Web API Için yardım sayfaları oluşturma](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) İstek ve yanıt biçimi dahil olmak üzere API hakkındaki ayrıntıları görmek için yardım sayfası bağlantılarına tıklayabilirsiniz.

![](part-3/_static/image4.png)

API, veritabanında CRUD işlemlerine izin vermez. Aşağıdaki, API 'YI özetler.

| Yazarlar |  |
| --- | -- |
| GET api/authors | Tüm yazarları al. |
| GET api/authors/{id} | KIMLIĞE göre yazar alın. |
| POST /api/authors | Yeni bir yazar oluşturun. |
| PUT /api/authors/{id} | Var olan bir yazarı güncelleştirin. |
| DELETE /api/authors/{id} | Bir yazarı silin. |

| Kitaplar |  |
| --- | -- |
| GET /api/books | Tüm kitapları alın. |
| GET /api/books/{id} | KIMLIĞE göre bir kitap alın. |
| POST /api/books | Yeni bir kitap oluşturun. |
| PUT /api/books/{id} | Mevcut bir kitabı güncelleştirin. |
| DELETE /api/books/{id} | Bir kitabı silin. |

## <a name="view-the-database-optional"></a>Veritabanını görüntüleme (Isteğe bağlı)

Update-database komutunu çalıştırdığınızda EF veritabanını oluşturup `Seed` yöntemi olarak çağırılır. Uygulamayı yerel olarak çalıştırdığınızda EF, [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)kullanır. Visual Studio 'da veritabanını görüntüleyebilirsiniz. **Görünüm** menüsünde **SQL Server Nesne Gezgini**'ni seçin.

![](part-3/_static/image5.png)

**Sunucuya Bağlan** iletişim kutusunda, **sunucu adı** düzenleme kutusuna "(LocalDB) \v11.0" yazın. **Kimlik doğrulama** seçeneğini "Windows kimlik doğrulaması" olarak bırakın. **Bağlan**'a tıklayın.

![](part-3/_static/image6.png)

Visual Studio, LocalDB 'ye bağlanır ve SQL Server Nesne Gezgini penceresinde var olan veritabanlarınızı gösterir. EF 'in oluşturduğu tabloları görmek için düğümleri genişletebilirsiniz.

![](part-3/_static/image7.png)

Verileri görüntülemek için bir tabloya sağ tıklayın ve **verileri görüntüle**' yi seçin.

![](part-3/_static/image8.png)

Aşağıdaki ekran görüntüsünde kitaplar tablosu için sonuçlar gösterilmektedir. , Veritabanının çekirdek verilerle birlikte doldurulduğunu ve tablo, yazarlar tablosunun yabancı anahtarını içerdiğini unutmayın.

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [Önceki](part-2.md)
> [İleri](part-4.md)
