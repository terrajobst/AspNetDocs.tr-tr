---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: klasör Izinlerini ayarlama-6/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 85a77a196cf3458bbb2e6308838a846936cd070b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630510"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: klasör Izinlerini ayarlama-6/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bu öğreticide, uygulamanın bu klasörde günlük dosyaları oluşturabilmesi için dağıtılan Web sitesindeki *ELMAH* klasörü için klasör izinlerini ayarlarsınız.

Visual Studio geliştirme sunucusunu (Cassini) kullanarak Visual Studio 'da bir Web uygulamasını test ettiğinizde, uygulama kimliğiniz altında çalışır. Büyük olasılıkla geliştirme bilgisayarınızda bir yöneticidir ve herhangi bir klasördeki herhangi bir dosya için herhangi bir şey yapmak üzere tam yetkiye sahip olursunuz. Ancak bir uygulama IIS altında çalıştığında, sitenin atandığı uygulama havuzu için tanımlanan kimlik altında çalışır. Bu, genellikle sınırlı izinlere sahip sistem tanımlı bir hesaptır. Varsayılan olarak, Web uygulamanızın dosya ve klasörlerinde okuma ve yürütme izinlerine sahiptir, ancak yazma erişimine sahip değildir.

Bu durum, uygulamanız Web uygulamalarında ortak olması gereken dosyaları oluşturduğunda veya güncelleştirirse bir sorun haline gelir. Contoso University uygulamasında, ELMAH, hatalarla ilgili ayrıntıları kaydetmek için *ELMAH* klasöründe XML dosyaları oluşturur. ELMAH gibi bir şey kullanmasanız bile siteniz, kullanıcıların dosyaları karşıya yüklemesine veya sitenizdeki bir klasöre veri yazan diğer görevleri gerçekleştirmesine izin verebilir.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="testing-error-logging-and-reporting"></a>Hata günlüğü ve raporlamayı test etme

Uygulamanın IIS 'de düzgün bir şekilde nasıl çalışmadığını görmek için (Visual Studio 'da test ettiğinizde), normalde ELMAH tarafından günlüğe kaydedilecek bir hataya neden olabilir ve ardından ayrıntıları görmek için ELMAH hata günlüğünü açın. ELMAH bir XML dosyası oluşturamadı ve hata ayrıntılarını depoladıysa boş bir hata raporu görürsünüz.

Bir tarayıcı açın ve `http://localhost/ContosoUniversity`gidin ve sonra *Studentsxxx. aspx*gibi GEÇERSIZ bir URL isteyin. Web. config dosyasındaki `customErrors` ayarı "RemoteOnly" olduğundan ve IIS 'yi yerel olarak çalıştırdığınız için *Genericerrorpage. aspx* sayfası yerine sistem tarafından oluşturulan bir hata sayfası görürsünüz:

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

Şimdi hata raporunu görmek için *ELMAH. axd* ' i çalıştırın. ELMAH, *ELMAH* KLASÖRÜNDE bir XML dosyası oluşturamadığı için boş bir hata günlüğü sayfası görürsünüz:

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>ELMAH klasörü üzerinde yazma Izni ayarlama

Klasör izinlerini el ile ayarlayabilir veya dağıtım sürecinin otomatik bir parçası yapabilirsiniz. Bunu otomatik hale getirmek, karmaşık MSBuild kodu gerektirir ve yalnızca ilk dağıttığınız zaman bunu yapmanız gerektiğinden, bu öğretici yalnızca el ile nasıl yapılacağını gösterir. (Dağıtım işleminin bu bölümünü oluşturma hakkında daha fazla bilgi için bkz. [Web 'de klasör Izinlerini ayarlama](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) , saymış hashed 'in blogu üzerinde yayımlama.)

**Windows Gezgini**'nde *C:\inetpub\wwwroot\contosoüniversitesi*' ne gidin. *ELMAH* klasörüne sağ tıklayın, **Özellikler**' i seçin ve ardından **güvenlik** sekmesini seçin.

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

( **Grup veya Kullanıcı adları** listesinde **DefaultAppPool** ÖĞESINI görmüyorsanız, bilgisayarınızda IIS ve ASP.NET 4 ' ü ayarlamak için bu öğreticide belirtilenden farklı bir yöntem kullanmışsınızdır. Bu durumda, Contoso Üniversitesi uygulamasına atanan uygulama havuzu tarafından kullanılan kimliği öğrenin ve bu kimliğe yazma izni verin. Bu öğreticinin sonundaki uygulama havuzu kimlikleri hakkındaki bağlantılara bakın.)

**Düzenle**‘ye tıklayın. **ELMAH izinleri** iletişim kutusunda, **DefaultAppPool**' ı seçin ve ardından **izin ver** sütununda **yazma** onay kutusunu seçin.

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

Her iki iletişim kutusunda **Tamam** ' a tıklayın.

## <a name="retesting-error-logging-and-reporting"></a>Hata günlüğü ve raporlama yeniden sınanıyor

Aynı şekilde bir hataya neden olan (hatalı URL iste) ve **hata günlüğü** sayfasını çalıştırarak test edin. Bu kez hata sayfada görüntülenir.

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

Ayrıca, bu klasörde SQL Server Compact veritabanı dosyalarınız olduğundan ve bu veritabanlarındaki verileri güncelleştirebilmeniz gerekeceğinden, *uygulama\_veri* klasörü üzerinde yazma izninizin olması gerekir. Ancak, bu durumda, dağıtım işlemi *App\_veri* klasörü üzerinde yazma iznini otomatik olarak ayarlayan için ek bir şey yapmanız gerekmez.

Contoso Üniversitesi 'nin yerel bilgisayarınızda IIS 'de düzgün şekilde çalışmasını sağlamak için gereken tüm görevleri tamamladınız. Bir sonraki öğreticide, bir barındırma sağlayıcısına dağıtarak siteyi genel kullanıma sunulacaktır.

## <a name="more-information"></a>Daha Fazla Bilgi

Bu örnekte, ELMAH 'nin günlük dosyalarını kaydedememesinin nedeni oldukça açıktır. Sorun nedeninin açık olmadığı durumlarda IIS izlemeyi kullanabilirsiniz; IIS.net sitesinde [IIS 7 ' de Izleme kullanarak başarısız Isteklerin sorunlarını giderme](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) bölümüne bakın.

Uygulama havuzu kimliklerine izin verme hakkında daha fazla bilgi için, IIS.net sitesindeki [dosya sistemi ACL 'Leri aracılığıyla IIS 'Deki](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) [uygulama havuzu kimlikleri](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) ve güvenli içerik bölümüne bakın.

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [İleri](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
