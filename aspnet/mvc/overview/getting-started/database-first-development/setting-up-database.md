---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 'Öğretici: MVC 5 kullanarak EF ile çalışmaya başlama Database First'
description: Bu öğretici, mevcut bir veritabanıyla nasıl başlayacağınızı ve kullanıcıların verilerle etkileşime geçmesini sağlayan bir Web uygulamasını hızlıca oluşturmayı gösterir.
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583526"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a>Öğretici: MVC 5 kullanarak EF ile çalışmaya başlama Database First

MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz. Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir. Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir. Serinin son bölümünde, doğrulama gereksinimlerini belirtmek ve biçimlendirmeyi göstermek için veri modeline veri açıklamalarını ekleme hakkında bilgi edineceksiniz. İşiniz bittiğinde, Azure App Service için bir .NET uygulaması ve SQL veritabanı dağıtmayı öğrenmek üzere bir Azure makalesine ilerleyebilirsiniz.

Bu öğretici, mevcut bir veritabanıyla nasıl başlayacağınızı ve kullanıcıların verilerle etkileşime geçmesini sağlayan bir Web uygulamasını hızlıca oluşturmayı gösterir. Web uygulamasını derlemek için 6 ve MVC 5 Entity Framework kullanır. ASP.NET Scafkatlama özelliği, verileri görüntülemek, güncelleştirmek, oluşturmak ve silmek için otomatik olarak kod üretmenizi sağlar. Visual Studio 'da yayımlama araçlarını kullanarak, siteyi ve veritabanını kolayca Azure 'a dağıtabilirsiniz.

Serinin bu bölümü, veritabanı oluşturmaya ve verilerle doldurmaya odaklanır.

Bu seri, Tom Dykstra ve Rick Anderson ' den katkılarla yazılmıştır. Yorumlar bölümünde kullanıcılardan gelen geri bildirimlere göre geliştirilmiştir.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Veritabanını ayarlama

## <a name="prerequisites"></a>Önkoşullar

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a>Veritabanını ayarlama

Var olan bir veritabanına sahip olma ortamını taklit etmek için, önce önceden doldurulan bazı verileri içeren bir veritabanı oluşturun ve sonra veritabanına bağlanan Web uygulamanızı oluşturun.

Bu öğretici, Visual Studio 2017 ile LocalDB kullanılarak geliştirilmiştir. LocalDB yerine var olan bir veritabanı sunucusunu kullanabilirsiniz, ancak Visual Studio sürümünüze ve veritabanı türüne bağlı olarak, Visual Studio 'daki tüm veri araçları desteklenmeyebilir. Araçlar veritabanınız için kullanılabilir değilse, veritabanınızın yönetim paketi içindeki bazı veritabanına özgü adımlardan bazılarını gerçekleştirmeniz gerekebilir.

Visual Studio sürümünüzde veritabanı araçlarıyla ilgili bir sorununuz varsa, veritabanı araçlarının en son sürümünü yüklediğinizden emin olun. Veritabanı araçları 'nı güncelleştirme veya yükleme hakkında bilgi için bkz. [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).

Visual Studio 'Yu başlatın ve bir **SQL Server veritabanı projesi**oluşturun. Projeyi **Contososıtydata**olarak adlandırın.

![veritabanı projesi oluştur](setting-up-database/_static/image1.png)

Artık boş bir veritabanı projeniz var. Bu veritabanını Azure 'a dağıtabilmeniz için, Azure SQL veritabanı 'nı projenin hedef platformu olarak ayarlarsınız. Hedef platformun ayarlanması aslında veritabanını dağıtmaz; yalnızca veritabanı projesinin hedef platformla uyumlu olduğunu doğrulayacağı anlamına gelir. Hedef platformu ayarlamak için, projenin **özelliklerini** açın ve hedef platform için **Microsoft Azure SQL veritabanı** seçin.

Tabloları tanımlayan SQL betikleri ekleyerek, bu öğretici için gereken tabloları oluşturabilirsiniz. Projenize sağ tıklayın ve yeni bir öğe ekleyin. **Tablolar ve görünümler** > **tablosu** seçin ve *öğrenci*olarak adlandırın.

Tablo dosyasında, tabloyu oluşturmak için T-SQL komutunu aşağıdaki kodla değiştirin.

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

Tasarım penceresinin kodla otomatik olarak eşitlendiğine dikkat edin. Kod ya da tasarımcı ile çalışabilirsiniz.

![kodu ve tasarımı göster](setting-up-database/_static/image5.png)

Başka bir tablo ekleyin. Bu kez kurs yapın ve aşağıdaki T-SQL komutunu kullanın.

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

Ve kayıt adlı bir tablo oluşturmak için bir kez daha tekrarlayın.

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

Veritabanınızı, veritabanı dağıtıldıktan sonra çalıştırılan bir betik aracılığıyla verilerle doldurabilirsiniz. Projeye bir dağıtım sonrası betiği ekleyin. Projenize sağ tıklayın ve yeni bir öğe ekleyin. **Dağıtım sonrası betiği** > **Kullanıcı betikleri** ' ni seçin. Varsayılan adı kullanabilirsiniz.

Dağıtım sonrası betiğine aşağıdaki T-SQL kodunu ekleyin. Bu betik, eşleşen bir kayıt bulunduğunda veritabanına veri ekler. Veritabanına girmiş olduğunuz herhangi bir veriyi üzerine yazmaz veya silmez.

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

Veritabanı projenizi her dağıttığınızda dağıtım sonrası komut dosyasının çalıştırıldığını unutmayın. Bu nedenle, bu betiği yazarken gereksinimlerinize dikkatlice göz önüne almanız gerekir. Bazı durumlarda, projenin her dağıtılışında bilinen bir veri kümesinden baştan başlamak isteyebilirsiniz. Diğer durumlarda, mevcut verileri dilediğiniz şekilde değiştirmek istemeyebilirsiniz. Gereksinimlerinize bağlı olarak, dağıtım sonrası bir betik veya betiğe dahil etmek için gerekenler hakkında karar verebilirsiniz. Veritabanınızı bir dağıtım sonrası betiği ile doldurma hakkında daha fazla bilgi için, [SQL Server veritabanı projesine veri ekleme](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)bölümüne bakın.

Artık 4 SQL betik dosyasına sahipsiniz ancak gerçek tablo yok. Veritabanı projenizi LocalDB 'ye dağıtmaya hazırlanıyor. Visual Studio 'da, veritabanı projenizi derlemek ve dağıtmak için Başlat düğmesine (veya F5) tıklayın. Derleme ve dağıtımın başarılı olduğunu doğrulamak için **Çıkış** sekmesini kontrol edin.

Yeni veritabanının oluşturulduğunu görmek için **SQL Server Nesne Gezgini** açın ve projenin adını doğru yerel veritabanı sunucusunda (Bu durumda **(LocalDB) \ProjectsV13**) arayın.

Tabloların verilerle doldurulduğunu görmek için bir tabloya sağ tıklayın ve **verileri görüntüle**' yi seçin.

![tablo verilerini göster](setting-up-database/_static/image9.png)

Tablo verilerinin düzenlenebilir bir görünümü görüntülenir. Örneğin, **tablo** > **dbo. kurs** > **verileri görüntüle**' yi seçerseniz, üç sütunlu (**Kurs**, **başlık**ve **krediler**) ve dört satır içeren bir tablo görürsünüz.

## <a name="additional-resources"></a>Ek kaynaklar

Code First geliştirmenin açıklayıcı bir örneği için bkz. [ASP.NET MVC 5 Ile çalışmaya](../introduction/getting-started.md)başlama. Daha gelişmiş bir örnek için bkz. [ASP.NET MVC 4 uygulaması için Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

Hangi Entity Framework yaklaşımın kullanılacağını seçme kılavuzu için, bkz. [Entity Framework geliştirme yaklaşımları](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Veritabanını ayarlama

Web uygulaması ve veri modelleri oluşturmayı öğrenmek için bir sonraki öğreticiye ilerleyin.
> [!div class="nextstepaction"]
> [Web uygulaması ve veri modellerini oluşturma](creating-the-web-application.md)
