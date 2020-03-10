---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: Visual Studio 2010 kullanarak kurumsal senaryolarda Web uygulamaları dağıtma | Microsoft Docs
author: jrjlee
description: Bu öğretici kümesinde, Web uygulamalarını çeşitli kurumsal senaryolarda dağıtmak için kullanabileceğiniz araçlar ve teknikler açıklanmaktadır. En iyi kullanımı nasıl yapılacağını açıklar...
ms.author: riande
ms.date: 05/03/2012
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: eb7b82d16079d4d086af1919d092fb28db60d8b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574160"
---
# <a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a>Visual Studio 2010 kullanarak Kurumsal Senaryolarda Web Uygulamaları dağıtma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu öğretici kümesinde, Web uygulamalarını çeşitli kurumsal senaryolarda dağıtmak için kullanabileceğiniz araçlar ve teknikler açıklanmaktadır. Visual Studio 2010, Microsoft Build Engine (MSBuild), Internet Information Services (IIS) 7,5, IIS Web Dağıtım Aracı (Web Dağıtımı), Web grubu çerçevesi (WFF) ve VSDBCMD. exe gibi yardımcı programlar gibi teknolojilerin en iyi şekilde nasıl kullanılacağını açıklar. dağıtım sürecini kolaylaştırın ve yönetin. Kavramsal genel bakış ve görev odaklı kılavuz içerir ve şunları yapmanıza yardımcı olur:
> 
> - Kurumsal ölçekte bir Web uygulaması için dağıtım gereksinimlerini gözden geçirin ve oluşturun.
> - Web dağıtımını desteklemek için test, hazırlama ve üretim Web sunucusu ortamlarını yapılandırın.
> - Otomatik Web dağıtımını desteklemek için Team Foundation Server (TFS) sürekli tümleştirme (CI) süreçlerini yapılandırın.
> - Değişen gereksinimler ve kısıtlamalarla, farklı sunucu ortamlarına kurumsal ölçekli web uygulamaları dağıtın.
> - Farklı sunucu ortamlarında çalışan Web uygulamalarına değişiklikleri dağıtın.
> 
> > [!NOTE]
> > Bu öğreticiler TFS 'nin bir CI sunucusu olarak kullanımını açıklarken, kılavuz her bir CI sunucusuna kolayca uyarlanmıştır. Öğreticilerin anlaşılması ve faydalanma hakkında ayrıntılı bilgi sahibi olmanız gerekmez.
> 
> 
> Bu öğreticilerin Italyanca çevirisi için [http://www.lucamorelli.it](http://www.lucamorelli.it)ziyaret edin.

## <a name="about-the-authors"></a>Yazarlar hakkında

Jason Lee, çeşitli yıllarda Microsoft ürünleri ve teknolojileri (özellikle SharePoint ve ASP.NET) ile çalıştığı, [Içerik yöneticisine](http://www.contentmaster.com/) sahip bir sorumlu teknoloji. Jason, bilgi işlem sırasında bir PhD barındırır ve şu anda MCPD ve MCTS sertifikalı. Jason 'in teknik blogunu [www.jrjlee.com](http://www.jrjlee.com/)adresinden okuyabilirsiniz.

Benjamin Curry, kariyer sırasında teknik incelemeleri, SDK belgelerini, PowerPoint sunularını ve öğreticiyi ve çevrimiçi eğitim kurslarını yazan, [Içerik yöneticisine](http://www.contentmaster.com/) sahip bir sorumlu teknoloji. ASP.NET belgeleri ekibinin orijinal bir üyesi, Microsoft 'un bir yılda on yıl boyunca Web teknolojileri ile çalıştık.

## <a name="target-audience"></a>Hedef kitle

Bu öğretici kümesi, kurumsal ölçekte Web uygulamaları oluşturmak için Visual Studio 2010 kullanan ASP.NET Web uygulaması geliştiricileri ve çözüm mimarilerine yöneliktir. İçerikten en iyi şekilde yararlanmak için, Visual Studio 2010 ve ASP.NET MVC 3, Windows Communication Foundation (WCF), IIS, SQL gibi Microsoft Web platformu teknolojilerinin bir açıklaması ile birlikte, TFS ile temel bir benzerlik sahibi olmanız gerekir. Sunucu ve Visual Studio veritabanı projeleri. Ancak, dağıtım araçları ve teknolojileri hakkında bilgi sahibi olmanız veya CI sistemlerini nasıl ayarlayabileceğinizi bilmeniz gerekmez.

## <a name="requirements"></a>Gereksinimler

İzlenecek yolları izlemek ve bu öğreticilerin açıkladığı görevleri gerçekleştirmek için, bu yazılımı geliştirme bilgisayarınıza yüklemeniz gerekir:

- Visual Studio 2010 Premium veya Ultimate Edition Service Pack 1
- .NET Framework 4,0
- .NET Framework 3,5 Service Pack 1
- ASP.NET MVC 3.0
- IIS 7.5 Express
- SQL Server Express 2008 R2

Bu izlenecek yollar boyunca açıklanan dağıtım adımlarını gerçekleştirmek için, örnek Web uygulaması dağıtım ortamlarına erişiminizin olması gerekir. En iyi sonuçlar için, bu ortamların kuruluşunuzun kurumsal dağıtım düzenini yansıtması gerekir. Daha sonra, bu belgede verilen izlenecek yolları, kendi kuruluşunuzun dağıtım ortamlarını ve gereksinimlerini yansıtacak şekilde değiştirebilirsiniz.

## <a name="series-contents"></a>Seri Içerikleri

Bu tanıtım bölümü, iki konuda daha oluşur. Bunlar, aşağıdaki öğreticiler için daha geniş bir bağlam sağlamak üzere tasarlanmıştır:

- [Kurumsal Web dağıtımı: senaryoya genel bakış](enterprise-web-deployment-scenario-overview.md). Bu konuda, bu serideki öğreticilerin her birini izleyen senaryo açıklanmaktadır. Bu senaryo, kurumsal ölçekte bir Web uygulaması geliştirdiğinden Fabrikam, Inc. adlı kurgusal bir şirketin uygulama yaşam döngüsü yönetimi (ALM) gereksinimlerine odaklanır.
- [Uygulama yaşam döngüsü yönetimi: geliştirmeden üretime kadar](application-lifecycle-management-from-development-to-production.md). Bu konu, bir dağıtım işlemine yüksek düzeyde, uçtan uca bir genel bakış sağlar. Fabrikam, Inc., sürekli bir geliştirme sürecinin bir parçası olarak test, hazırlama ve üretim ortamları aracılığıyla bir kurumsal ölçekte ASP.NET Web uygulamasını nasıl taşıdığını gösterir.

Seriler dört öğretici kümesi içerir. Her biri Web dağıtımının farklı yönlerine odaklanır:

- [Kuruluşta Web dağıtımı](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Bu öğreticide, MSBuild proje dosyaları, Web yayımlama işlem hattı, Web Dağıtımı ve diğer ilgili teknolojiler hakkında kavramsal bir giriş sunulmaktadır. Karmaşık dağıtım süreçlerini yönetmek için bu araçları birlikte nasıl kullanabileceğinizi açıklar.
- [Web dağıtımı Için sunucu ortamlarını yapılandırma](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). Bu öğreticide, Windows sunucularının Web Deployment Agent hizmeti ("uzak Aracı") veya Web Dağıtımı Işleyicisi ile uzak veritabanı dağıtımı kullanılarak uzak Web paketi dağıtımı gibi çeşitli dağıtım senaryolarını destekleyecek şekilde nasıl yapılandırılacağı açıklanmaktadır. Kendi ortamınız için uygun dağıtım yöntemini seçme konusunda rehberlik sağlar ve Dağıtılmış Web uygulamalarını bir sunucu grubundaki tüm Web sunucuları arasında çoğaltmak için WFF 'nin nasıl kullanılacağını açıklar.
- [Web dağıtımı için Team Foundation Server yapılandırılıyor](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). Bu öğreticide, bir CI işleminin parçası olarak otomatik dağıtım ve belirli derlemelerin el ile tetiklenen çeşitli dağıtım senaryolarını desteklemek üzere TFS 'nin nasıl yapılandırılacağı açıklanmaktadır.
- [Gelişmiş kurumsal Web dağıtımı](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). Bu öğreticide, birden çok ortam için veritabanı dağıtımlarını özelleştirme, dağıtımdan dosya ve klasörleri dışarıda bırakma ve dağıtım işlemi sırasında Web uygulamalarını çevrimdışına alma gibi çeşitli gelişmiş dağıtım görevlerinin nasıl yapılacağı açıklanmaktadır. .

## <a name="where-to-start"></a>Nereden başlatılacak

Bu öğretici kümesi, bir başvuru uygulama sağlamak ve görevlere izin vermek ve ortak bir bağlam için izlenecek yollar sağlamak üzere kurgusal bir işletme dağıtım senaryosu ile birlikte gerçekçi karmaşıklık düzeyine sahip örnek bir çözüm kullanır. Sonraki konu olan [Kurumsal Web dağıtımı: senaryoya genel bakış](enterprise-web-deployment-scenario-overview.md), senaryoyu ve örnek çözümü tanıtır. Buradan, gereksinimlerinize en yakından eşleşen öğreticiler ve konular üzerinden çalışabilirsiniz.

> [!div class="step-by-step"]
> [Next](enterprise-web-deployment-scenario-overview.md)
