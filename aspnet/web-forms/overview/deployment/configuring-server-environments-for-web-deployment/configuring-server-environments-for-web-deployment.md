---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: Web dağıtımı için sunucu ortamlarını yapılandırma | Microsoft Docs
author: jrjlee
description: Bu öğreticide, tek tıklamalı veya otomatik, Web sitesi dağıtımını desteklemek için sunucu ortamlarını nasıl ayarlayabileceği ve farklı bir şekilde farklı bir şekilde yayımlacaksınız...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 073161ce4faa3b7ba6749d7dfbaa5309eeca4f74
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634472"
---
# <a name="configuring-server-environments-for-web-deployment"></a>Sunucu Ortamlarını Web Dağıtımı için Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu öğreticide, tek tıklamalı veya otomatik, Web sitesi dağıtımını desteklemek için sunucu ortamlarının nasıl ayarlanacağı ve çeşitli farklı senaryolarda yayımlama gösterilmektedir. Öğreticide, bir Web sunucusu yapılandırmak ve bir Web grubu çerçevesi (WFF) sunucu grubu kurmak için belirli yaklaşımları desteklemek üzere bir Web sunucusu yapılandırma gibi çeşitli görevleri tamamlama konusunda size kılavuzluk eden konular yer almaktadır. üst düzey uçtan uca rehberlik.
> 
> Öğretici, Kurumsal Web dağıtımı 'nda açıklanan Fabrikam, Inc. dağıtım senaryosunu kullanır: örnekler ve ağ altyapısı için bir başvuru noktası olarak [senaryoya genel bakış](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) .
> 
> Bu öğreticilerin Italyanca çevirisi için [http://www.lucamorelli.it](http://www.lucamorelli.it)ziyaret edin.

Bu öğretici aşağıdaki konuları içerir:

- [Web Dağıtımı için Doğru Yaklaşımı Seçme](choosing-the-right-approach-to-web-deployment.md)
- [Senaryo: Web Dağıtımı için Test Ortamı Yapılandırma](scenario-configuring-a-test-environment-for-web-deployment.md)
- [Senaryo: Web Dağıtımı için Hazırlama Ortamı Yapılandırma](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [Senaryo: Web Dağıtımı için Üretim Ortamı Yapılandırma](scenario-configuring-a-production-environment-for-web-deployment.md)
- [Bir Web Sunucusunu Web Dağıtımı Yayımlama için Yapılandırma (Uzak Aracı)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [Bir Web Sunucusunu Web Dağıtımı Yayımlama için Yapılandırma (Web Dağıtımı İşleyicisi)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [Bir Web Sunucusunu Web Dağıtımı Yayımlama için Yapılandırma (Çevrimdışı Dağıtım)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [Bir Veritabanı Sunucusunu Web Dağıtımı Yayımlama için Yapılandırma](configuring-a-database-server-for-web-deploy-publishing.md)
- [Web Farm Framework ile Sunucu Grubu Oluşturma](creating-a-server-farm-with-the-web-farm-framework.md)
- [Hedef Ortam için Dağıtım Özelliklerini Yapılandırma](configuring-deployment-properties-for-a-target-environment.md)

[Web dağıtımına doğru yaklaşımı seçerek](choosing-the-right-approach-to-web-deployment.md)ilk konu, Web uygulamalarını yayımlamak için kullanabileceğiniz ana yaklaşımları Internet INFORMATION SERVICES (IIS) Web Dağıtım aracı (Web Dağıtımı) 2,0 ' i kullanarak açıklar. Ayrıca her yaklaşımla eşlenen senaryoları tanımlar. Buradan, her senaryo konusu, bu görevleri tamamlamanıza yardımcı olması için, çalışmanız gereken görevlere yönelik yüksek düzeyde bir genel bakış sağlar ve üzerinde çalışmanız gereken konuları tanımlar.

Çözümünüzü derlemek ve dağıtmak için [Yapı sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md) bölümünde açıklanan bölünmüş proje dosyası yaklaşımını kullanıyorsanız, [hedef ortam Için dağıtım özelliklerini yapılandırma](configuring-deployment-properties-for-a-target-environment.md)son konu başlığı altında, ortama özgü proje dosyalarının farklı hedef ortamlara dağıtılması için nasıl yapılandırılacağı açıklanmaktadır.

## <a name="key-technologies"></a>Anahtar teknolojileri

Bu öğreticide, Web dağıtımını desteklemek için bu ürünlerin ve teknolojilerin nasıl kullanılacağı ele alınmaktadır:

- IıS 7,5
- Web Dağıtımı 2. x
- WFF 2. x
- IIS Web yönetimi hizmeti (WMSvc)

Öğretici ayrıca Windows Server 2008 R2 'nin kullanımına, SQL Server 2008 R2, ASP.NET 4,0 ve ASP.NET MVC 3 ' ün kullanımına de dokunur.

## <a name="other-tutorials-in-this-series"></a>Bu serideki diğer öğreticiler

Bu, kurumsal ölçekte Web dağıtımında bir dizi beş öğreticilerin bir parçasını oluşturur. Serideki diğer öğreticiler şunlardır:

- [Kurumsal senaryolarda Web uygulamaları dağıtma](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Bu giriş içeriği, öğretici serisi için bağlamsal arka plan sağlar. Öğretici senaryosunu açıklar ve diziler genelinde açıklanan görevlerin ve talimatların daha geniş bir uygulama yaşam döngüsü yönetimi (ALM) sürecine sığması gösterilmektedir.
- [Kuruluşta Web dağıtımı](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Bu öğreticide Microsoft Build Engine (MSBuild) proje dosyaları, Web yayımlama işlem hattı, Web Dağıtımı ve diğer ilgili teknolojiler hakkında kavramsal bir giriş sunulmaktadır. Karmaşık dağıtım süreçlerini yönetmek için bu araçları birlikte nasıl kullanabileceğinizi açıklar.
- [Web dağıtımı için Team Foundation Server yapılandırılıyor](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). Bu öğreticide, sürekli tümleştirme (CI) sürecinin bir parçası olarak otomatik dağıtım ve belirli yapıların el ile tetiklenen dağıtımları gibi çeşitli dağıtım senaryolarını desteklemek üzere Team Foundation Server (TFS) uygulamasının nasıl yapılandırılacağı açıklanmaktadır.
- [Gelişmiş kurumsal Web dağıtımı](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). Bu öğreticide, birden çok ortam için veritabanı dağıtımlarını özelleştirme, dağıtımdan dosya ve klasörleri dışarıda bırakma ve dağıtım işlemi sırasında Web uygulamalarını çevrimdışına alma gibi çeşitli gelişmiş dağıtım görevlerinin nasıl yapılacağı açıklanmaktadır. .

> [!div class="step-by-step"]
> [Next](choosing-the-right-approach-to-web-deployment.md)
