---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: veritabanı güncelleştirmesi dağıtma-9/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564444"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: veritabanı güncelleştirmesi dağıtma-9/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bu öğreticide, bir veritabanı değişikliği ve ilgili kod değişiklikleri yapar, değişiklikleri Visual Studio 'da test edin ve ardından güncelleştirme hem test hem de üretim ortamlarına dağıtılır.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="adding-a-new-column-to-a-table"></a>Tabloya yeni sütun ekleme

Bu bölümde, `Student` ve `Instructor` varlıkları için `Person` taban sınıfına bir Doğum tarihi sütunu eklersiniz. Ardından, eğitmen verilerini görüntüleyen sayfayı yeni sütunu görüntüleyecek şekilde güncelleştirin.

*Contosouniversity. dal* projesinde, *Person.cs* açın ve `Person` sınıfının sonuna aşağıdaki özelliği ekleyin (bundan sonra iki kapatma küme ayracı olmalıdır):

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

Ardından, yeni sütun için bir değer sağlayacak şekilde çekirdek yöntemini güncelleştirin. *Migrations\configuration.cs* ' i açın ve `var instructors = new List<Instructor>` başlayan kod bloğunu, Doğum tarihi bilgilerini içeren aşağıdaki kod bloğu ile değiştirin:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

ContosoUniversity projesinde, *eğitmenler. aspx* ' i açın ve Doğum tarihini göstermek için yeni bir şablon alanı ekleyin. İşe alma tarihi ve Office ataması için olanlar arasına ekleyin:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

(Kod girintileme eşitlenmemiş ise, CTRL + K tuşlarına basabilir ve sonra dosyayı otomatik olarak yeniden biçimlendirmek için CTRL-D ' ye basabilirsiniz.)

Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın. ContosoUniversity. DAL ' nin hala **varsayılan proje**olarak seçildiğinden emin olun.

**Paket Yöneticisi konsolu** penceresinde, **varsayılan proje**olarak **contosouniversity. dal** ' ı seçin ve aşağıdaki komutu girin:

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

Bu komut tamamlandığında, Visual Studio yeni `DbMigration` sınıfını tanımlayan sınıf dosyasını açar ve `Up` yönteminde yeni sütunu oluşturan kodu görebilirsiniz.

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresine aşağıdaki komutu girin (contosouniversity. dal projesinin hala seçili olduğundan emin olun):

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

Komut tamamlandığında, uygulamayı çalıştırın ve eğitmenler sayfasını seçin. Sayfa yüklendiğinde, yeni Doğum tarihi alanına sahip olduğunu görürsünüz.

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>Veritabanı güncelleştirmesini test ortamına dağıtma

**Çözüm Gezgini** contosouniversity projesini seçin.

Web 'de **Yayımla** araç çubuğunda, **Test** yayımlama profilini seçin ve ardından **Web 'i Yayımla**' yı tıklatın. (Araç çubuğu devre dışıysa, **Çözüm Gezgini**' de contosouniversity projesini seçin.)

Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı giriş sayfasında açılır. Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için Eğitmenler sayfasını çalıştırın. Uygulama bu sayfanın veritabanına erişmeye çalıştığında, Code First veritabanı şemasını güncelleştirir ve `Seed` metodunu çalıştırır. Sayfa görüntülendiğinde, içindeki tarihlerle birlikte beklenen **Doğum tarihi** sütununu görürsünüz.

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>Veritabanı güncelleştirmesini üretim ortamına dağıtma

Artık üretime dağıtabilirsiniz. Tek fark, kullanıcıların siteye erişmelerini ve bu nedenle değişiklikleri dağıttığınız sırada veritabanını güncellemesini engellemek için *offline. htm\_uygulamanızı* kullanmanızdır. Üretim dağıtımı için aşağıdaki adımları uygulayın:

- *Uygulamayı çevrimdışı. htm dosyasını\_* üretim sitesine yükleyin.
- Visual Studio 'da, Web 'de üretim profilini seçin, **Yayımla** araç çubuğundan ve **Web 'i Yayımla**' ya tıklayın.
- Uygulamayı, üretim sitesinden *çevrimdışı. htm dosyasını\_* silin.

> [!NOTE]
> Uygulamanız üretim ortamında kullanımda olsa da bir yedekleme planı uygulamanız gerekir. Diğer bir deyişle, *School-prod. sdf* ve *ASPNET-prod. sdf* dosyalarını düzenli olarak üretim sitesinden güvenli bir depolama konumuna kopyalamanız ve bu tür yedeklemelerin çeşitli nesilleri tutmanız gerekir. Veritabanını güncelleştirdiğinizde, değişiklikten hemen önce bir yedekleme kopyası oluşturmalısınız. Daha sonra, bir hata yaparsanız ve bunu üretime dağıtana kadar bulamadıysanız, veritabanını bozmadan önce bulunduğu duruma geri yükleyemezsiniz.

Visual Studio tarayıcıda giriş sayfası URL 'sini açtığında, *app\_offline. htm* sayfası görüntülenir. *Uygulamayı\_çevrimdışı. htm* dosyasını sildikten sonra, güncelleştirmenin başarıyla dağıtıldığını doğrulamak için giriş sayfanıza yeniden gidebilirsiniz.

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

Artık test ve üretime bir veritabanı değişikliği içeren bir uygulama güncelleştirmesi dağıttıysanız. Sonraki öğreticide, veritabanınızı SQL Server Compact SQL Server Express ve SQL Server 'e nasıl geçirebileceğiniz gösterilmektedir.

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [İleri](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
