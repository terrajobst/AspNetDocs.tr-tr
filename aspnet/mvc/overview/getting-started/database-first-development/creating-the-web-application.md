---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'Öğretici: ASP.NET MVC ile EF Database First için Web uygulaması ve veri modelleri oluşturma'
description: Bu öğretici, Web uygulaması oluşturmaya ve veritabanı tablolarınıza göre veri modellerini oluşturmaya odaklanmaktadır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616272"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a>Öğretici: ASP.NET MVC ile EF Database First için Web uygulaması ve veri modelleri oluşturma

 MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz. Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir. Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.

Bu öğretici, Web uygulaması oluşturmaya ve veritabanı tablolarınıza göre veri modellerini oluşturmaya odaklanmaktadır.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * ASP.NET web uygulaması oluşturma
> * Modelleri oluşturma

## <a name="prerequisites"></a>Önkoşullar

* [MVC 5 kullanarak Entity Framework 6 Database First kullanmaya başlama](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a>ASP.NET web uygulaması oluşturma

Yeni bir çözümde veya veritabanı projesiyle aynı çözümde, Visual Studio 'da yeni bir proje oluşturun ve **ASP.NET Web uygulaması** şablonunu seçin. Projeyi **Contososite**olarak adlandırın.

![proje oluştur](creating-the-web-application/_static/image1.png)

**Tamam**’a tıklayın.

Yeni ASP.NET projesi penceresinde **MVC** şablonunu seçin. Uygulamayı daha sonra buluta dağıtacağından, şimdi için **bulut seçeneğinde Konağı** temizleyebilirsiniz. Uygulamayı oluşturmak için **Tamam** ' ı tıklatın.

Proje varsayılan dosya ve klasörlerle oluşturulur.

Bu öğreticide Entity Framework 6 kullanacaksınız. NuGet Paketlerini Yönet penceresi aracılığıyla projenizdeki Entity Framework sürümünü bir kez daha kontrol edebilirsiniz. Gerekirse, Entity Framework sürümünüzü güncelleştirin.

![sürümü göster](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a>Modelleri oluşturma

Artık veritabanı tablolarından Entity Framework modeller oluşturacaksınız. Bu modeller, verilerle çalışmak için kullanacağınız sınıflardır. Her model veritabanındaki bir tabloyu yansıtır ve tablodaki sütunlara karşılık gelen özellikleri içerir.

**Modeller** klasörüne sağ tıklayın ve **Ekle** ' ye ve **Yeni öğe**' yi seçin.

Yeni öğe Ekle penceresinde, sol bölmedeki **veriler** ' i seçin ve orta bölmedeki seçeneklerden **ADO.net varlık veri modeli** . Yeni model dosyası **Contosomodel**olarak adlandırın.

**Ekle**'yi tıklatın.

Varlık Veri Modeli sihirbazında, **veritabanından EF Designer**' ı seçin.

**İleri**'ye tıklayın.

Geliştirme ortamınızda tanımlanmış veritabanı bağlantılarınız varsa, bu bağlantılardan birini önceden seçmiş olabilirsiniz. Ancak, Bu öğreticinin ilk bölümünde oluşturduğunuz veritabanına yeni bir bağlantı oluşturmak istersiniz. **Yeni bağlantı** düğmesine tıklayın.

Bağlantı Özellikler penceresi, veritabanınızın oluşturulduğu yerel sunucunun adını girin (Bu örnekte **(LocalDB) \ProjectsV13**). Sunucu adını sağladıktan sonra, kullanılabilir veritabanlarından Contosoüniversıdata ' ı seçin.

![bağlantı özelliklerini ayarlama](creating-the-web-application/_static/image8.png)

**Tamam**’a tıklayın.

Doğru bağlantı özellikleri artık gösteriliyor. Web. config dosyasında bağlantı için varsayılan adı kullanabilirsiniz.

**İleri**'ye tıklayın.

En son Entity Framework sürümünü seçin.

**İleri**'ye tıklayın.

Üç tabloya yönelik modeller oluşturmak için **Tablolar** ' ı seçin.

**Son**'a tıklayın.

Bir güvenlik uyarısı alırsanız, şablonu çalıştırmaya devam etmek için **Tamam** ' ı seçin.

Modeller veritabanı tablolarından oluşturulur ve tablolar arasındaki özellikleri ve ilişkileri gösteren bir diyagram görüntülenir.

![Model diyagramı](creating-the-web-application/_static/image11.png)

Modeller klasörü artık veritabanından oluşturulan modellerle ilgili birçok yeni dosya içerir.

**ContosoModel.Context.cs** dosyası **DbContext** sınıfından türetilen bir sınıf içerir ve bir veritabanı tablosuna karşılık gelen her model sınıfı için bir özellik sağlar. **Course.cs**, **enrollment.cs**ve **Student.cs** dosyaları, veritabanları tablolarını temsil eden model sınıflarını içerir. Yapı iskelesi ile çalışırken hem bağlam sınıfını hem de model sınıflarını kullanacaksınız.

Bu öğreticiye devam etmeden önce projeyi derleyin. Sonraki bölümde, veri modellerini temel alan kod oluşturacaksınız, ancak bu bölüm, proje oluşturulmadığında çalışmaz.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Bir ASP.NET Web uygulaması oluşturuldu
> * Modeller üretildi

Veri modellerini temel alan oluşturma kodu oluşturma hakkında bilgi edinmek için sonraki öğreticiye ilerleyin.
> [!div class="nextstepaction"]
> [Görünümler üretiliyor](generating-views.md)
