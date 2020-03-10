---
uid: whitepapers/aspnet-web-deployment-content-map
title: ASP.NET Web dağıtımı-önerilen kaynaklar | Microsoft Docs
author: rick-anderson
description: Bu konu, Visual Studio 2010, Visual Web de... kullanarak ASP.NET Web uygulamalarının IIS 'e nasıl dağıtılacağı (yayımlanacağı) hakkındaki belge kaynaklarına bağlantılar sağlar.
ms.author: riande
ms.date: 03/14/2014
ms.assetid: 58b583cd-c4ab-47a3-8527-8c92c298c91f
msc.legacyurl: /whitepapers/aspnet-web-deployment-content-map
msc.type: content
ms.openlocfilehash: 96873c8f2b0ad2415f371aceb651400c801a3338
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636992"
---
# <a name="aspnet-web-deployment---recommended-resources"></a>ASP.NET Web Dağıtımı - Önerilen Kaynaklar

> Bu konu, Visual Studio 2010, Visual Web Developer 2010 ve sonraki sürümlerini kullanarak ASP.NET Web uygulamalarının IIS 'e nasıl dağıtılacağı (yayımlanacağı) hakkındaki belge kaynaklarına bağlantılar sağlar.
> 
> Harika bir blog gönderisi, [StackOverflow](http://stackoverflow.com) iş parçacığı veya yararlı olabilecek başka bir bağlantı biliyorsanız, bağlantıyı kullanarak [bize e-posta gönderin](mailto:aspnetue@microsoft.com?subject=Deployment%20Content%20Map) .
> 
> > [!NOTE] 
> > 
> > Bu kaynakların birçoğu, yalnızca [Visual Studio Web yayımlama güncelleştirmesinin](https://go.microsoft.com/fwlink/?LinkID=208120)yeni bir sürümünü yüklerseniz kullanılabilir olan dağıtım özelliklerini anlatmaktadır. Bazı özellikler yalnızca Visual Studio 2012 veya Visual Studio 2013 kullanılabilir.

Bu konu aşağıdaki bölümleri içermektedir:

- [Web projeleri için dağıtım seçeneklerini anlama](#understanding)
- [Bir ASP.NET uygulaması için barındırma sağlayıcılarını bulma](#findinghosting)
- [Visual Studio 'dan bir Web uygulaması dağıtma](#fromvs)
- [Web dağıtım paketi oluşturup yükleyerek Web uygulaması dağıtma](#package)
- [Sürekli tümleştirme (CI) işlemi kullanarak Web uygulaması dağıtma](#ci)
- [Dağıtım sırasında hedef Web. config dosyasındaki veya App. config dosyasındaki ayarları değiştirmek için Web. config dönüşümlerini kullanma](#transforms)
- [Dağıtım sırasında hedef Web uygulamasındaki ayarları değiştirmek için Web Dağıtımı parametrelerini kullanma](#webdeployparms)
- [Dağıtım sırasında bir uygulamanın çevrimiçi olduğundan emin olma](#appoffline)
- [Web uygulaması dağıtımının bir parçası olarak bir veritabanını veya değişiklikleri veritabanına dağıtma](#databasewithweb)
- [Web uygulaması dağıtımından ayrı bir veritabanı dağıtma](#databaseseparate)
- [Üyelik ve profil oluşturma gibi ASP.NET uygulama hizmetlerini kullanan bir Web uygulamasını dağıtma](#aspnetmembership)
- [Dağıtım için ön derleme](#precompiling)
- [İntranet Web uygulaması dağıtma](#intranet)
- [Otomatik olarak kutudan çıkar olmayan ortak dağıtım görevlerini otomatikleştirme](#automating)
- [Geliştiricilerin Web Dağıtımı kullanarak Web uygulamalarını dağıtabilmeleri için Web sunucularını yapılandırma](#configuringservers)
- [Sunucuları barındırma sağlayıcısı için yapılandırma](#hostingprovider)
- [Dağıtım sorunlarını giderme](#troubleshooting)
- [Belirli bir dağıtım sorusu ile ilgili yardım alma](#gettinghelp)
- [Ek Kaynaklar](#additional)

<a id="understanding"></a>

## <a name="understanding-deployment-options-for-web-projects"></a>Web projeleri için dağıtım seçeneklerini anlama

- [Visual Studio ve ASP.net Için Web dağıtımına genel bakış](https://msdn.microsoft.com/library/dd394698.aspx) (MSDN).
- [Windows Azure Web sitesi dağıtma](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Windows Azure Web sitelerine, [sürekli teslim](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) ( [kaynak denetiminden](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)otomatik) ve Visual Studio kullanarak Web projeleri dağıtmaya yönelik kaynakları ve bağlantıları açıklar.
- [Visual Studio 2012 Web yayımlama geliştirmeleri](../visual-studio/overview/2012/visual-studio-2012-web-publishing-improvements.md) (Scott Hanselman tarafından video).
- VS 2010 (Vishal Joshi 'ın blogu) [Içindeki Web dağıtımı Için genel bakış gönderisi](http://vishaljoshi.blogspot.com/2009/09/overview-post-for-web-deployment-in-vs.html) . Daha eski bir blog gönderisi ancak Visual Studio 2010 kaynaklarından bazıları, hala Visual Studio 2012 için geçerli olan bilgilere sahip.

<a id="findinghosting"></a>

## <a name="finding-hosting-providers-for-an-aspnet-application"></a>Bir ASP.NET uygulaması için barındırma sağlayıcılarını bulma

- [ASP.NET barındırma](https://asp.net/hosting)

<a id="fromvs"></a>

## <a name="deploying-a-web-application-from-visual-studio"></a>Visual Studio 'dan bir Web uygulaması dağıtma

- [Windows Azure Web sitesi dağıtma](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Seçenekleri açıklar ve Windows Azure Web sitelerine Web projeleri dağıtmaya yönelik kaynaklara bağlantılar sağlar. Visual Studio 'dan dağıtma hakkında bir bölüm içerir.
- [Visual Studio kullanarak Web dağıtımı ASP.net](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). 12 parçalı öğretici serisi, Web uygulamalarının SQL Server veritabanlarıyla nasıl dağıtılacağını gösterir. Veritabanı dağıtımı için hem dbDacFx sağlayıcısını hem de Entity Framework Code First Migrations kullanır. Ayrıca, [Web. config dosyası dönüştürmeleri](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md), [tek tek dosyaları dağıtma](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md#specificfiles), [komut satırı dağıtımı](../web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment.md)ve [Visual Studio Web yayımlama işlem hattının. pubxml dosyalarını düzenleyerek nasıl özelleştirileceği](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)hakkında bilgiler içerir. Web Forms, MVC ve Web API 'SI de dahil olmak üzere tüm ASP.NET Web projeleri için geçerlidir.)
- [Nasıl yapılır: Visual Studio 'Da tek tıklamayla yayımlama kullanarak Web projesi dağıtma](https://msdn.microsoft.com/library/dd465337.aspx) (Visual Studio Web Yayımlama Sihirbazı için başvuru bilgileri)
- [Visual Studio kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md). Bu, bu bölümün üst kısmında listelenen **Visual Studio kullanılarak ASP.NET Web dağıtımının** önceki bir sürümüdür. Genellikle SQL Server Compact veritabanlarının nasıl dağıtılacağı ve SQL Server Compact SQL Server tam sürümüne nasıl geçirileceğiyle ilgili bilgiler için artık yararlı olur.
- [Depolama tabloları, kuyrukları ve Blobları (Microsoft Azure sitesi) kullanan .net çok katmanlı uygulama](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) . 5 parçalı öğretici serisi, bir MVC projesinin nasıl oluşturulacağını ve bir Microsoft Azure bulut hizmetine nasıl dağıtılacağını gösterir.

<a id="package"></a>
## <a name="deploying-a-web-application-by-creating-and-installing-a-web-deployment-package"></a>Web dağıtım paketi oluşturup yükleyerek Web uygulaması dağıtma

- [Nasıl yapılır: Visual Studio 'Da Web dağıtım paketi oluşturma](https://msdn.microsoft.com/library/dd465323.aspx) (MSDN).
- [Nasıl yapılır: Visual Studio (MSDN) tarafından oluşturulan Deploy. cmd dosyasını kullanarak dağıtım paketini yükler](https://msdn.microsoft.com/library/ff356104.aspx) .
- [Geliştirme kutusu ve üçüncü taraf ana bilgisayar (sayılan Web günlüğü) ÜZERINDE IIS 'e dağıtmak için bir Web dağıtımı paketi kullanma](http://sedodream.com/2011/11/08/UsingAWebDeployPackageToDeployToIISOnTheDevBoxAndToAThirdPartyHost.aspx) . IIS Yöneticisi 'ni kullanarak yerel bilgisayara ve uzaktan yönetim için IIS Yöneticisi 'Ni destekleyen bir barındırma şirketinde IIS 'de bir dağıtım paketi yükler.
- [Visual Studio 2010](https://www.iis.net/learn/publish/using-web-deploy/building-a-web-deploy-package-from-visual-studio-2010) (IIS.NET Web sitesinden) Web dağıtımı paketi oluşturma. Komut satırı paketi oluşturma ve yükleme yönergelerini içerir.
- [Her yerde Yayımla](http://sedodream.com/2012/03/14/PackageWebUpdatedAndVideoBelow.aspx) (sayılan Hashi blogu). Birden çok hedef ortam için Web. config dosyasını dönüştürme sürecini otomatikleştiren bir NuGet paketi tanıtır, böylece birden çok sunucuya bir paket dağıtabilmenizi sağlayabilirsiniz. Ayrıca, sayılan karmaya göre [Packageweb videosunu](https://www.youtube.com/watch?v=-LvUJFI8CzM) inceleyin.

Ayrıca aşağıdaki bölüme bakın.

<a id="ci"></a>

## <a name="deploying-a-web-application-using-a-continuous-integration-ci-process"></a>Sürekli tümleştirme (CI) işlemi kullanarak Web uygulaması dağıtma

- [Sürekli tümleştirme ve sürekli teslim (Microsoft Azure ile gerçek hayatta bulut uygulamaları oluşturma).](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) Sürekli tümleştirmeyi ve sürekli teslimi tanıtan E-kitap bölümü.
- [Windows Azure Web sitesi dağıtma](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Windows Azure Web sitelerine Web projeleri dağıtmaya yönelik kaynakların seçeneklerini ve bağlantılarını açıklar. Kaynak denetiminden dağıtımı otomatikleştirme hakkında bir bölüm içerir.
- [Kurumsal senaryolarda Web uygulamaları dağıtma](../web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). 40-bölüm öğreticisi serisi, Visual Studio 2010 ve Team Foundation Server 2010 kullanarak bir CI işlemindeki dağıtımı nasıl otomatikleştirebileceğinizi gösterir.
- [Microsoft Build Engine içinde: Sayed HashMe ve William Bartholomew Ile MSBuild ve Team Foundation Build kullanımı](http://msbuildbook.com). Bu bir Web kaynağı değil, bir kitaptır, ancak sürekli tümleştirme senaryoları için MSBuild 'in nasıl yapılandırılacağını öğrenmek için temel bir kılavuzdur.
- [MSBuild Uzantı paketi](https://github.com/mikefourie/MSBuildExtensionPack). Dağıtım görevlerini içerir.
- [Team Foundation yapı özelleştirme Kılavuzu](https://aka.ms/vsarsolutions). Team Foundation Server ayarlama sırasında ALM Rantasyon belgeleri Web dağıtımını kapsar ve öğreticiler ve videolar içerir.
- [BIR CI sunucusundan Yavaşcheetah XML dönüşümleri](http://sedodream.com/2011/12/12/SlowCheetahXMLTransformsFromACIServer.aspx) (sayılan karmaya ait blog). App. config ve diğer XML dosyalarını dönüştürmek için bir Visual Studio eklentisi olan Yavaşcheetah 'ın nasıl kullanılacağını açıklar.

Ayrıca bkz. bu sayfada daha sonra [dağıtım sırasında uygulamanın çevrimdışı olduğundan emin olma](aspnet-web-deployment-content-map.md#appoffline) .

<a id="transforms"></a>

## <a name="using-webconfig-transformations-to-change-settings-in-the-destination-webconfig-file-or-appconfig-file-during-deployment"></a>Dağıtım sırasında hedef Web. config dosyasındaki veya App. config dosyasındaki ayarları değiştirmek için Web. config dönüşümlerini kullanma

- [Web. config dosyası dönüştürmeleri](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md).
- [Visual Studio (MSDN) kullanarak Web proje dağıtımı Için Web. config dönüştürme söz dizimi](https://msdn.microsoft.com/library/dd465326.aspx) .
- [Web araçları 2012,2-Web. config dönüşümleri](https://www.youtube.com/watch?v=HdPK8mxpKEI) (sayılan karmaya göre YouTube videosu). Web. config dönüştürmelerini ayarlamayı ve önizlemeyi gösterir.
- [Web. config dönüşümünü devre dışı Nasıl yaparım?.](https://msdn.microsoft.com/library/ee942158.aspx#disable_web_config_transformation) (MSDN).
- [Web. config dönüştürmeleri yerine Web Dağıtımı parametrelerini ne zaman kullanmalıyım?](https://msdn.microsoft.com/library/ee942158.aspx#web_deploy_parameters) (MSDN).
- [Xdt (XML belge dönüşümü) CodePlex.com 'de yayınlandı](https://blogs.msdn.com/b/webdev/archive/2013/04/23/xdt-xml-document-transform-released-on-codeplex-com.aspx) (.NET Web geliştirme ve araçlar blogu). Web. config dosyası dönüştürme motorunun kaynak kodunun kullanılabilirliğini duyurur ve onu kullanan bazı araçları listeler.
- [Windows Azure Web siteleri: uygulama dizeleri ve bağlantı dizeleri nasıl çalışır](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure blog). Web. config 'e alternatif olarak, hedef ortamınız Windows Azure Web siteleri ise ve `appSettings` ya da `connectionStrings`dönüştürmek istiyorsanız dönüştürür.

<a id="webdeployparms"></a>

## <a name="using-web-deploy-parameters-to-change-settings-in-the-destination-web-application-during-deployment"></a>Dağıtım sırasında hedef Web uygulamasındaki ayarları değiştirmek için Web Dağıtımı parametrelerini kullanma

- [Nasıl yapılır: bir Web dağıtım paketinde (MSDN) Web dağıtımı parametrelerini kullanma](https://msdn.microsoft.com/library/ff398068.aspx) .
- [MSDeploy: yayımlama profilini temel alarak yayımlama sırasında uygulama ayarlarını güncelleştirme](http://sedodream.com/2013/03/02/MSDeployHowToUpdateAppSettingsOnPublishBasedOnThePublishProfile.aspx) (sayılan karmaya 'nın blogu). Web dağıtımı parametrelerinin Visual Studio yayımlama profillerine nasıl tümleştirileceğini gösterir.
- [Web dağıtımı Parametreleştirme](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-parameterization) (IIS.NET Web sitesi).
- (Vishal Joshi 'ın blogu) [eyleminde Parametreleştirme Web dağıtımı](http://vishaljoshi.blogspot.com/2010/07/web-deploy-parameterization-in-action.html) .
- [Web dağıtımı Parameterleştirme vs. Web. config dönüşümü](http://vishaljoshi.blogspot.com/2010/06/parameterization-vs-webconfig.html) (Vishal Joshi 'ın blogu).
- [Windows Azure Web siteleri: uygulama dizeleri ve bağlantı dizeleri nasıl çalışır](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure blog). Hedef ortamınız Windows Azure Web siteleri ise ve `appSettings` veya `connectionStrings`parametreleştirmek istiyorsanız Web Dağıtım parametrelerine bir alternatif.

<a id="appoffline"></a>

## <a name="making-sure-an-application-is-off-line-during-deployment"></a>Dağıtım sırasında bir uygulamanın çevrimiçi olduğundan emin olma

- [Visual Studio kullanarak Web dağıtımı ASP.net: bir kod güncelleştirmesi dağıtma](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md). **Dağıtım sırasında uygulamayı çevrimdışına alma** bölümüne bakın.
- [Yayımlamadan önce bir uygulamayı çevrimdışına alma](https://www.iis.net/learn/publish/deploying-application-packages/taking-an-application-offline-before-publishing) (IIS.net sitesi). Web Dağıtımı 3,0 ' de yerleşik olarak bulunan ve bir uygulamanın çevrimdışı. htm dosyasını\_işlemeyi otomatikleştiren bir özelliği açıklar. Bu özellik, çevrimdışı. htm dosyaları\_özel uygulamayla birlikte çalışmaz.
- [Yayımlama sırasında Web uygulamanızı çevrimdışına alma](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx) (sayılan Hashma blogu). Çevrimdışı. htm dosyası\_özel bir uygulama kullanma sürecini otomatikleştirme.
- [Uygulama çevrimdışı ve usechecksum Için Web Yayımlama güncelleştirmeleri](https://blogs.msdn.com/b/webdev/archive/2013/10/30/web-publishing-updates-for-app-offline-and-usechecksum.aspx) (Microsoft Web geliştirme blogu). App\_offline. htm dosyasının kullanımını otomatikleştirme için başka bir seçenek.
- [Web Dağıtımı 3,5 RTW](https://blogs.iis.net/msdeploy/archive/2013/07/09/webdeploy-3-5-rtw.aspx) (IIS.net site). Özel uygulama için Web Dağıtımı 3,5 ' deki yeni özellik çevrimdışı. htm dosyaları\_.

<a id="databasewithweb"></a>

## <a name="deploying-a-database-or-changes-to-a-database-as-part-of-web-application-deployment"></a>Web uygulaması dağıtımının bir parçası olarak bir veritabanını veya değişiklikleri veritabanına dağıtma

- [Visual Studio 'Da veritabanı dağıtımını yapılandırma](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) (MSDN). Bir Web projesi ile veritabanı dağıtmaya yönelik seçeneklere genel bakış.
- [Visual Studio kullanarak Web dağıtımı ASP.net](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). 12 parçalı öğretici serisi, dbDacFx sağlayıcısı ve Entity Framework Code First Migrations kullanarak veritabanı dağıtımını gösterir.
- [Nasıl yapılır: Visual Studio 'Da tek tıklamayla yayımlama kullanarak Web projesi dağıtma](https://msdn.microsoft.com/library/dd465337.aspx) (MSDN).
- [Üyelik, OAuth ve SQL veritabanı ile bir Microsoft Azure Web sitesine güvenli bir ASP.NET MVC 5 uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Üyelik ve uygulama verileri için tek bir SQL Server veritabanı kullanan bir uygulama oluşturup dağıtan uzun bir öğretici.
- [Visual Studio kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md). 12 parçalı öğretici serisi, SQL Server Compact veritabanlarının nasıl dağıtılacağını ve SQL Server Compact SQL Server tam sürümüne nasıl geçirileceğiyle gösterilir.

Ayrıca bkz. Web dağıtım paketi oluşturup yükleyerek Web uygulaması dağıtma ve bu sayfada daha önce bir sürekli tümleştirme (CI) işlemi kullanarak Web uygulaması dağıtma.

<a id="databaseseparate"></a>

## <a name="deploying-a-database-separately-from-web-application-deployment"></a>Web uygulaması dağıtımından ayrı bir veritabanı dağıtma

- [SQL Server veri araçları](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx) (MSDN).
- [SQL Server veritabanı projesine veri ekleme](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx) (SQL Server veri araçları ekip blogu). Bir veritabanı dağıtırken hem şemayı hem de verileri dağıtma.
- [Windows Azure 'A veritabanı dağıtma](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate) (Microsoft Azure sitesi)
- [Veritabanlarını Windows Azure SQL veritabanına geçirme (eski adıyla SQL Azure)](https://msdn.microsoft.com/library/windowsazure/ee730904.aspx) (MSDN).
- [SSDT kullanarak bir veritabanını SQL Azure geçirme](https://blogs.msdn.com/b/ssdt/archive/2012/04/19/migrating-a-database-to-sql-azure-using-ssdt.aspx) (SQL Server veri araçları ekip blogu).
- [Veri merkezli uygulamaları Microsoft Azure 'A geçirme](https://msdn.microsoft.com/library/jj156154.aspx) (MSDN).
- [SQL Server veritabanlarını Windows Azure SQL veritabanı 'na](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN) geçirme.

<a id="aspnetmembership"></a>

## <a name="deploying-a-web-application-that-uses-aspnet-application-services-such-as-membership-and-profiling"></a>Üyelik ve profil oluşturma gibi ASP.NET uygulama hizmetlerini kullanan bir Web uygulamasını dağıtma

- [Üyelik, OAuth ve SQL veritabanı ile bir Microsoft Azure Web sitesine güvenli bir ASP.NET MVC 5 uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Üyelik ve uygulama verileri için tek bir SQL Server veritabanı kullanan bir uygulama oluşturup dağıtan uzun bir öğretici.
- [ASP.NET Identity](https://asp.net/identity/). ASP.NET Identity kaynakları.
- [Visual Studio kullanarak Web dağıtımı ASP.net](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). 12 parçalı öğretici serisi, ASP.NET üyelik veritabanının nasıl dağıtılacağını gösterir.
- [Uygulama hizmetleri kullanan bir Web sitesi yapılandırma](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs.md). Web sitesi projeleri için, ancak Web uygulaması projeleri için de geçerlidir.
- [Üretim Web sitesindeki kullanıcılar ve roller](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs.md). Web sitesi projeleri için, ancak Web uygulaması projeleri için de geçerlidir.

<a id="precompiling"></a>

## <a name="precompiling-for-deployment"></a>Dağıtım için ön derleme

- [ASP.NET Web uygulaması projesi ön derlemesine genel bakış](https://msdn.microsoft.com/library/aa983464.aspx) (MSDN).
- [Web 'ı paketle/yayımlayın sekmesi, proje özellikleri](https://msdn.microsoft.com/library/dd410108.aspx) (MSDN).
- [Gelişmiş ön derleme ayarları Iletişim kutusu](https://msdn.microsoft.com/library/hh475319.aspx) (MSDN).

<a id="intranet"></a>

## <a name="deploying-an-intranet-web-application"></a>İntranet Web uygulaması dağıtma

- [Visual Studio 2013 'de ASP.net Ile şirket Içi kurumsal kimlik doğrulama seçeneğini (ADFS) kullanın](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/) (Vıttorio Bertoccı tarafından blog).
- [ASP.NET MVC (MSDN) kullanarak bir Intranet sitesi oluşturma](https://msdn.microsoft.com/library/gg703322(VS.98).aspx) . Visual Studio 2010 için daha eski izlenecek yol, Visual Studio 2013 tanıtılan intranet proje şablonlarındaki önemli değişiklikleri yansıtmaz.

<a id="automating"></a>

## <a name="automating-common-deployment-tasks-that-are-not-automated-out-of-the-box"></a>Otomatik olarak kutudan çıkar olmayan ortak dağıtım görevlerini otomatikleştirme

- [Visual Studio kullanarak Web dağıtımı ASP.net: ek dosyalar dağıtma](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md).
- [Web yayımlaması üzerinde klasör Izinleri ayarlanıyor](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) (sayılan karmaya 'nın blogu).
- [Hedef dosyayı bir Web proje paketine (Web geliştirme araçları blogu) kayıt defteri ayarlarını içerecek şekilde genişletme](https://blogs.msdn.com/webdevtools/archive/2010/02/09/how-to-extend-target-file-to-include-registry-settings-for-web-project-package.aspx) .
- [XML (Web. config) dönüşümünü genişletme](http://sedodream.com/2010/09/09/ExtendingXMLWebconfigConfigTransformation.aspx) (sayılan hashist blogu). Özel XDT dönüştürmeleri oluşturmayı gösterir.
- [Web Dağıtım Aracı (MSDeploy) özel sağlayıcısı 1](http://sedodream.com/2010/03/11/WebDeploymentToolMSDeployCustomProviderTake1.aspx) (sayılan bir karmadan blog) alır. Web Dağıtımı özel sağlayıcının nasıl oluşturulacağını gösterir.
- [Com bileşenlerini paketleme ve dağıtma](https://blogs.msdn.com/webdevtools/archive/2010/03/03/how-to-package-and-deploy-com-component.aspx) (Web geliştirme araçları blogu).
- [.NET derlemelerini paketleme](https://blogs.msdn.com/webdevtools/archive/2010/02/19/how-to-package-com-component.aspx) (Web geliştirme araçları blogu). GAC 'ye derlemeler dağıtma.
- [Her şeyi ziyaret edin-IIS, Web dağıtımı ve diğer malzemelerle](http://www.tugberkugurlu.com/archive/script-out-everything-initialize-your-windows-azure-vm-for-your-web-server-with-iis-web-deploy-and-other-stuff) (tugberk ugurlu 'ın blogu) Web sunucunuz Için WINDOWS Azure VM 'nizi başlatın.

<a id="configuringservers"></a>

## <a name="configuring-web-servers-so-that-developers-can-deploy-web-applications-to-them-using-web-deploy"></a>Geliştiricilerin Web Dağıtımı kullanarak Web uygulamalarını dağıtabilmeleri için Web sunucularını yapılandırma

- [Yönetici ve yönetici olmayan dağıtımlar için Web dağıtımı yükleme ve yapılandırma](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy) (IIS.net sitesi).

<a id="hostingprovider"></a>

## <a name="configuring-servers-for-a-hosting-provider"></a>Sunucuları barındırma sağlayıcısı için yapılandırma

- [Microsoft ASP.NET 4 barındırma dağıtım kılavuzu](https://go.microsoft.com/fwlink/?LinkId=191365) (Microsoft İndirme Merkezi).
- [Bir PROFIL XML dosyası](https://www.iis.net/learn/web-hosting/joining-the-web-hosting-gallery/generate-a-profile-xml-file) (IIS.net sitesi) oluşturun.

<a id="troubleshooting"></a>

## <a name="troubleshooting-deployment-problems"></a>Dağıtım sorunlarını giderme

- [Visual Studio 'Da Microsoft Azure Web siteleri 'Nde sorun giderme](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) (Microsoft Azure sitesi).
- [Visual Studio kullanarak Web dağıtımını ASP.net: sorun giderme](../web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting.md).
- [Web dağıtımı karşılaşılan yaygın sorunları giderme](https://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-common-problems-with-web-deploy).
- [Web dağıtımı hata kodları](https://www.iis.net/learn/publish/troubleshooting-web-deploy/web-deploy-error-codes) (IIS.net site).
- [Visual Studio ve ASP.net Için Web dağıtımı hakkında SSS](https://msdn.microsoft.com/library/ee942158.aspx) (MSDN).
- [IIS ile ASP.NET geliştirme sunucusu arasındaki temel farklılıklar](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md).
- [Geliştirme ve üretim arasındaki yaygın yapılandırma farklılıkları](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs.md).
- [ASP.NET uygulamalarını Orta güvende barındırma](http://www.4guysfromrolla.com/articles/100307-1.aspx) (Rolla sitesinden 4 guys).

<a id="gettinghelp"></a>

## <a name="getting-help-with-a-specific-deployment-question"></a>Belirli bir dağıtım sorusu ile ilgili yardım alma

- [ASP.NET yapılandırma ve dağıtım Forumu](https://forums.asp.net/26.aspx/1?Configuration and Deployment).
- [StackOverflow.com](http://www.StackOverflow.com).

<a id="additional"></a>

## <a name="additional-resources"></a>Ek Kaynaklar

Bu bölüm, Visual Studio ve IIS dağıtım araçları 'nı kullanma hakkında daha fazla bilgi edinmek için yararlı olan ek kaynaklara bağlantılar sağlar.

Aşağıdaki Bloglar genellikle Visual Studio Web dağıtımı hakkında bilgi içerir:

- [Microsoft bloguna Web geliştirme araçları](https://blogs.msdn.com/b/webdevtools/).
- [Sayılan hashbir Web günlüğü](http://www.sedodream.com/).

Aşağıdaki kaynaklar, Visual Studio 'Nun Web uygulaması proje dağıtım görevlerini gerçekleştirmek için kullandığı IIS çerçevesini Web Dağıtımı hakkında belgeler sağlar. IIS.net Web sitesindeki [Web Dağıtım aracı forumundaki](https://go.microsoft.com/fwlink/?LinkId=149411) Web dağıtımı hakkında soru sorabilirsiniz.

- [Web dağıtımı giriş](https://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy).
- [Web dağıtımı yükleme ve yapılandırma](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy).
- [Web dağıtımı kurulumunu otomatikleştirmek Için PowerShell betikleri](https://www.iis.net/learn/publish/using-web-deploy/powershell-scripts-for-automating-web-deploy-setup).
- [Web Dağıtım aracı](https://go.microsoft.com/fwlink/?LinkId=151481). TechNet sitesindeki Web Dağıtımı belgeler için en üst düzey İçindekiler düğümü. Faydalı başvuru bilgileri içerir, ancak çoğu TechNet sayfası yıl boyunca güncelleştirilmemiş olabilir.
- [Microsoft. Web. Deployment Ad alanı](https://go.microsoft.com/fwlink/?LinkId=148630). API belgeleri, sürüm 1,0 ' den bu yana güncelleştirilmemiş.
- [Microsoft Web dağıtımı ekibi blogu](https://blogs.iis.net/msdeploy/default.aspx).
- [IIS.NET Web sitesinde Yayımla sekmesi](https://www.iis.net/learn/publish).
