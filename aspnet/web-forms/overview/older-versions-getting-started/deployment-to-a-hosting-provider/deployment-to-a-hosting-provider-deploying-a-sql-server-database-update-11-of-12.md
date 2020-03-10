---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: SQL Server veritabanı güncelleştirmesi dağıtma-11/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528128"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: SQL Server veritabanı güncelleştirmesi dağıtma-11/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Windows Azure Web sitelerine nasıl dağıtılacağını gösterir. bkz. [ASP.NET Web Deployment for Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bu öğreticide, bir veritabanı güncelleştirmesinin tam bir SQL Server veritabanına nasıl dağıtılacağı gösterilmektedir. Code First Migrations, veritabanını güncelleştirme işinin tümünü yaptığından, işlem [veritabanı güncelleştirme](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) öğreticisinde SQL Server Compact için yaptığınız işlemle neredeyse aynıdır.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="adding-a-new-column-to-a-table"></a>Tabloya yeni sütun ekleme

Öğreticinin bu bölümünde, bir veritabanı değişikliği ve ilgili kod değişiklikleri yapıp, bunları test ve üretim ortamlarına dağıtmaya hazırlanmaya yönelik olarak Visual Studio 'da test edersiniz. Değişiklik, `Instructor` varlığına `OfficeHours` bir sütun eklenmesini ve yeni bilgilerin **eğitmenler** Web sayfasında görüntülenmesini içerir.

ContosoUniversity. DAL projesinde *Instructor.cs* öğesini açın ve `HireDate` ve `Courses` özellikleri arasına aşağıdaki özelliği ekleyin:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

Yeni sütunu test verileriyle birleştirmek için Başlatıcı sınıfını güncelleştirin. *Migrations\configuration.cs* ' i açın ve `var instructors = new List<Instructor>` başlayan kod bloğunu yeni sütunu içeren aşağıdaki kod bloğu ile değiştirin:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

ContosoUniversity projesinde, *eğitmenler. aspx* ' i açın ve ilk `GridView` denetimindeki kapatma `</Columns>` etiketinden hemen önce, Office saatleri için yeni bir şablon alanı ekleyin:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

Çözümü derleyin.

**Paket Yöneticisi konsol** penceresini açın ve **varsayılan proje**olarak contosouniversity. dal ' i seçin.

Aşağıdaki komutları girin:

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

Uygulamayı çalıştırın ve **eğitmenler** sayfasını seçin. Entity Framework, veritabanını yeniden oluşturduğundan ve test verileriyle kullandığından, sayfanın yüklenmesi normalden biraz daha uzun sürer.

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>Veritabanı güncelleştirmesini test ortamına dağıtma

Code First Migrations kullandığınızda, SQL Server bir veritabanı değişikliğini dağıtma yöntemi SQL Server Compact ile aynıdır. Ancak, SQL Server Compact, hala SQL Server geçirilecek şekilde ayarlandığından test yayımlama profilini değiştirmeniz gerekir.

İlk adım, önceki öğreticide oluşturduğunuz bağlantı dizesi dönüştürmelerinin kaldırılması olur. Bunlara geçiş için **Package/PUBLISH SQL** sekmesini yapılandırmadan önce yaptığınız gibi, yayımlama profilinde bağlantı dizesi dönüştürmeleri belirtebileceğiniz SQL Server için bunlar artık gerekli değildir.

*Web. test. config* dosyasını açın ve `connectionStrings` öğesini kaldırın. *Web. test. config* dosyasında kalan tek dönüşüm, `appSettings` öğesindeki `Environment` değeri içindir.

Şimdi yayımlama profilini güncelleştirebilir ve test ortamında yayımlayabilirsiniz.

Web 'i **Yayımla** sihirbazını açın ve ardından **profil** sekmesine geçin.

**Test** yayımlama profilini seçin.

**Ayarlar** sekmesini seçin.

**Yeni veritabanı yayımlama iyileştirmelerini etkinleştir**' e tıklayın.

**SchoolContext**için bağlantı dizesi kutusuna, önceki öğreticideki *Web. test. config* dönüştürme dosyasında kullandığınız değeri girin:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

**Code First Migrations Yürüt ' ü seçin (uygulama başlatma üzerinde çalışır)** . (Visual Studio sürümünüz içinde, onay kutusu **Code First Migrations uygulanabilir**olarak etiketlenir.)

**DefaultConnection**bağlantı dizesi kutusunda, önceki öğreticideki *Web. test. config* dönüştürme dosyasında kullandığınız değeri girin:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

**Güncelleştirme veritabanını** işaretsiz bırak.

**Yayımla**’ta tıklayın.

Visual Studio, kod değişikliklerini test ortamına dağıtır ve tarayıcıyı Contoso Üniversitesi giriş sayfasında açar.

Eğitmenler sayfasını seçin.

Uygulama bu sayfayı çalıştırdığında veritabanına erişmeye çalışır. Code First Migrations veritabanının güncel olup olmadığını denetler ve en son geçişin henüz uygulandığını bulur. Code First Migrations en son geçişi uygular, `Seed` yöntemini çalıştırır ve ardından sayfa normal şekilde çalışır. Yeni Office saatleri sütununu, sağlanan verilerle birlikte görürsünüz.

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>Veritabanı güncelleştirmesini üretim ortamına dağıtma

Üretim ortamı için yayımlama profilini de değiştirmeniz gerekir. Bu durumda, güncelleştirilmiş bir. publishsettings dosyasını içeri aktararak var olan profili kaldırır ve yeni bir tane oluşturabilirsiniz. Güncelleştirilmiş dosya, Cytanium adresindeki SQL Server veritabanı için bağlantı dizesini içerir.

Test ortamına dağıtırken gördüğünüz gibi, artık *Web. Production. config* dönüştürme dosyasında bağlantı dizesi dönüştürmeleri gerekmez. Bu dosyayı açın ve `connectionStrings` öğesini kaldırın. Geri kalan dönüşümler, `appSettings` öğesindeki `Environment` değeri ve ELMAH hata raporlarına erişimi kısıtlayan `location` öğesi içindir.

Üretim için yeni bir yayımlama profili oluşturmadan önce, güncelleştirilmiş bir. publishsettings dosyasını [Üretim ortamında dağıtım](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) öğreticisinde daha önce yaptığınız şekilde indirin. (Cytanium Denetim Masası 'nda **Web siteleri**' ne ve ardından **contosouniversity.com** Web sitesine tıklayın. **Web yayımlama** sekmesini seçin ve ardından **Bu web sitesi Için yayımlama profilini indir**' e tıklayın.) Bunu yaptığınız neden,. publishsettings dosyasında veritabanı bağlantı dizesini seçmektir. Hala SQL Server Compact kullandığınızdan ve henüz Cytanium adresinde SQL Server veritabanı oluşturmadığından, bağlantı dizesi dosyayı ilk kez indirdikten sonra kullanılamıyor.

Artık yayımlama profilini güncelleştirebilir ve üretim ortamında yayımlayabilirsiniz.

Web 'i **Yayımla** sihirbazını açın ve ardından **profil** sekmesine geçin.

**Profilleri Yönet**' e tıklayın ve ardından üretim profilini silin.

Bu değişikliği kaydetmek için **Web 'ı Yayımla** Sihirbazı 'nı kapatın.

Web 'i **Yayımla** Sihirbazı 'nı yeniden açın ve ardından **içeri aktar**' a tıklayın.

Geçici bir URL kullanıyorsanız, **bağlantı** SEKMESINDE **hedef URL** 'yi uygun değere değiştirin.

**İleri**'ye tıklayın.

**Ayarlar** sekmesinde, **Yeni veritabanı yayımlama iyileştirmelerini etkinleştir**' e tıklayın.

**SchoolContext**için bağlantı dizesi açılan listesinde, Cytanium bağlantı dizesini seçin.

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

**Code First geçişleri Yürüt ' ü seçin (uygulama başlatma üzerinde çalışır)** .

**DefaultConnection**için bağlantı dizesi açılan listesinde Cytanium bağlantı dizesini seçin.

**Profil** sekmesini seçin, **profilleri Yönet**' e tıklayın ve profili "contosouniversity.com-Web dağıtımı" iken "üretim" olarak yeniden adlandırın.

Değişikliği kaydetmek için yayımlama profilini kapatın ve sonra yeniden açın.

**Yayımla**’ta tıklayın. (Gerçek bir üretim web sitesi için, *uygulamayı çevrimdışı. htm\_* kopyalayın ve yayımlamadan önce proje klasörünüze yerleştirip dağıtım tamamlandığında kaldırabilirsiniz.)

Visual Studio, kod değişikliklerini test ortamına dağıtır ve tarayıcıyı Contoso Üniversitesi giriş sayfasında açar.

Eğitmenler sayfasını seçin.

Code First Migrations, veritabanını test ortamında olduğu gibi güncelleştirir. Yeni Office saatleri sütununu, sağlanan verilerle birlikte görürsünüz.

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

Bir SQL Server veritabanı kullanarak veritabanı değişikliğini içeren bir uygulama güncelleştirmesini başarıyla dağıttınız.

## <a name="more-information"></a>Daha Fazla Bilgi

Bu, bir ASP.NET Web uygulamasını bir üçüncü taraf barındırma sağlayıcısına dağıtmaya yönelik bu öğretici serisini tamamlar. Bu öğreticilerde ele alınan konuların herhangi biri hakkında daha fazla bilgi için MSDN Web sitesindeki [ASP.NET dağıtım Içerik haritasına](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) bakın.

## <a name="acknowledgements"></a>Bildirimler

Bu öğretici serisinin içeriğine önemli bir katkı yapan kişiler için teşekkür ederiz:

- [Alberto Poblacion, MVP &amp; MCT, Ispanya](https://mvp.support.microsoft.com/profile/Alberto)
- Jarod Ferguson, veri platformu geliştirme MVP, Birleşik Devletler
- Harsh Mittal, Microsoft
- [Kristina Olson, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope, Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava, Microsoft
- [Raffaele Rialdi, Italya](http://www.iamraf.net/)
- [Rick Anderson, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayılan diyez, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Srđan Božović, Sırbistan](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [İleri](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
