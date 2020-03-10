---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: Web dağıtımı için Team Foundation Server yapılandırma | Microsoft Docs
author: jrjlee
description: Bu öğreticide, çözümleri derlemek ve çeşitli hedef ortamlara Web içeriği dağıtmak üzere Team Foundation Server (TFS) 2010 ' nin nasıl yapılandırılacağı gösterilir. Bu...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 638d696abbc5f05957c0ed2eb7ebb65fce7813ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528394"
---
# <a name="configuring-team-foundation-server-for-web-deployment"></a>Team Foundation Server’ı Web Dağıtımı için Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu öğreticide, çözümleri derlemek ve çeşitli hedef ortamlara Web içeriği dağıtmak üzere Team Foundation Server (TFS) 2010 ' nin nasıl yapılandırılacağı gösterilir. Bu, bir geliştirici her değişiklik yaptığında içeriği otomatik olarak dağıttığınız sürekli tümleştirme (CI) senaryolarını içerir. Ayrıca, bir yöneticinin test ortamında derleme doğrulandıktan ve doğrulandıktan sonra belirli bir derlemeyi hazırlama ortamına dağıtmak istediği el ile tetikleyici senaryolarını de içerebilir. Bu öğreticideki konular aşağıdakiler dahil olmak üzere tüm yapılandırma sürecinde size kılavuzluk eder:
> 
> - TFS 'de yeni bir takım projesi oluşturma.
> - Kaynak denetimine içerik ekleme.
> - Bir yapı sunucusunu CI ve dağıtımı destekleyecek şekilde yapılandırma.
> - Dağıtım mantığını içeren bir yapı tanımı oluşturma.
> - Otomatik dağıtım için izinleri yapılandırma.
> 
> Bu öğreticilerin Italyanca çevirisi için [http://www.lucamorelli.it](http://www.lucamorelli.it)ziyaret edin.

Bu öğreticide, TFS 2010 ' i yüklediğinizi ve ilk yapılandırma sürecinin bir parçası olarak bir takım projesi koleksiyonu oluşturduğunuzdan varsayılmaktadır. [Visual Studio 2010 Için Team Foundation Yükleme Kılavuzu](https://go.microsoft.com/?linkid=9805132) , bu görevler hakkında kapsamlı yönergeler sağlar.

## <a name="context"></a>Bağlam

Bu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alan bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, WINDOWS COMMUNICATION FOUNDATION&#x2014;(WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) çözümünü kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren iki [](../web-deployment-in-the-enterprise/understanding-the-build-process.md)proje&#x2014;dosyası tarafından denetlendiği ve ortama özgü derleme ve dağıtım ayarlarını Içeren, derleme işlemini anlama bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="scenario-overview"></a>Senaryoya Genel Bakış

Bu öğreticiler için üst düzey senaryo, [Kurumsal Web dağıtımında açıklanmıştır: senaryoya genel bakış](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md). Bu öğreticide çalışmaya başlamadan önce bu konuyu incelemenizi öneririz.

## <a name="how-to-use-this-tutorial"></a>Bu öğreticiyi kullanma

Bu öğreticide açıklanan görevleri ilk kez gerçekleştirdiyseniz veya örnek çözümü kullanarak örnekleri izlemek isterseniz, öğretici konularında sırasıyla çalışmanız gerekir. Alternatif olarak, belirli görevler için tek tek konuları kılavuz olarak kullanabilirsiniz. Bu öğretici aşağıdaki konuları içerir:

- [TFS 'de bir takım projesi oluşturma](creating-a-team-project-in-tfs.md). Bir takım projesi, kaynak denetimi, işlem yönetimi ve TFS 'de derleme için temel birimdir. Kaynak denetimine İçerik ekleyebilmeniz veya yapı tanımları oluşturabilmeniz için önce bir takım projesi oluşturmanız gerekir.
- [Kaynak denetimine Içerik ekleniyor](adding-content-to-source-control.md). Bir ekip projesi oluşturduktan sonra kaynak denetimine içerik eklemeye başlayabilirsiniz. Yapıları yapılandırmaya başlayabilmeniz için, tüm dış bağımlılıklarla birlikte projelerinizi ve çözümlerinizi eklemeniz gerekir.
- [Web dağıtımı için BIR TFS derleme sunucusu yapılandırma](configuring-a-tfs-build-server-for-web-deployment.md). Takım projesi içeriğinizi derlemek istiyorsanız, bir yapı sunucusu yapılandırmanız gerekir. Çoğu durumda bu, TFS yüklemenizin ayrı bir makinesinde olmalıdır. Bir yapı sunucusunu yapılandırmak için, TFS derleme hizmetini yükleyip yapılandırmanız, Visual Studio 2010 ' i yüklemeniz, derleme denetleyicileri ve derleme aracıları oluşturmanız, kodunuzun ihtiyaç duyduğu ürünleri veya bileşenleri, başarıyla derlemek ve yüklemek için yüklemeniz gerekir. Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı).
- [Dağıtımı destekleyen bir yapı tanımı oluşturuluyor](creating-a-build-definition-that-supports-deployment.md). TFS 'de derlemeleri sıraya almayı veya tetiklemeyi başlatabilmeniz için önce takım projeniz için en az bir yapı tanımı oluşturmanız gerekir. Yapı tanımı, yapıya dahil edilmesi gereken şeyler, derlemeyi tetiklemeniz gerekenler ve takım derlemesinin derleme çıkışlarını gönderebilmesi dahil olmak üzere, yapı için her yönü tanımlar. Otomatikleştirilmiş derlemelerinize dağıtım mantığını dahil etmenizi sağlayan özel Microsoft Build Engine (MSBuild) proje dosyalarını çalıştırmak için bir yapı tanımı yapılandırabilirsiniz.
- [Belirli bir derlemeyi dağıtma](deploying-a-specific-build.md). Birçok senaryoda, hedef ortama en son yapı yerine belirli bir derlemeyi dağıtmak isteyeceksiniz. Bu durumda, belirli bir bırakma klasöründen içerik dağıtan bir yapı tanımı yapılandırabilirsiniz.
- [Ekip derleme dağıtımı Için Izinleri yapılandırma](configuring-permissions-for-team-build-deployment.md). Yapı Hizmeti içeriği otomatik derleme işleminin bir parçası olarak dağıtmaktır, herhangi bir hedef Web sunucusunda ve veritabanı sunucusunda yapı hizmeti hesabına çeşitli izinler vermeniz gerekir.

## <a name="key-technologies"></a>Anahtar teknolojileri

Bu öğretici, otomatik derleme ve Web dağıtımını desteklemek için bu ürünlerin ve teknolojilerin nasıl kullanılacağına odaklanır:

- Visual Studio Team Foundation Server 2010
- Takım derlemesi ve MSBuild
- Web Dağıtımı

Öğretici ayrıca Windows Server 2008 R2, IIS 7,5, SQL Server 2008 R2, ASP.NET 4,0 ve ASP.NET MVC 3 ' ün kullanımına de dokunur.

## <a name="other-tutorials-in-this-series"></a>Bu serideki diğer öğreticiler

Bu, kurumsal ölçekte Web dağıtımında bir dizi beş öğreticilerin bir parçasını oluşturur. Serideki diğer öğreticiler şunlardır:

- [Kurumsal senaryolarda Web uygulamaları dağıtma](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Bu giriş içeriği, öğretici serisi için bağlamsal arka plan sağlar. Öğretici senaryosunu açıklar ve diziler genelinde açıklanan görevlerin ve talimatların daha geniş bir uygulama yaşam döngüsü yönetimi (ALM) sürecine sığması gösterilmektedir.
- [Kuruluşta Web dağıtımı](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Bu öğreticide, MSBuild proje dosyaları, Web yayımlama işlem hattı (WPP), Web Dağıtımı ve diğer ilgili teknolojiler hakkında kavramsal bir giriş sunulmaktadır. Karmaşık dağıtım süreçlerini yönetmek için bu araçları birlikte nasıl kullanabileceğinizi açıklar.
- [Web dağıtımı Için sunucu ortamlarını yapılandırma](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). Bu öğreticide, Windows sunucularının Web Deployment Agent hizmeti (uzak Aracı) veya Web Dağıtımı Işleyicisi ile uzak veritabanı dağıtımı kullanılarak uzak Web paketi dağıtımı gibi çeşitli dağıtım senaryolarını destekleyecek şekilde nasıl yapılandırılacağı açıklanmaktadır. Kendi ortamınız için uygun dağıtım yöntemini seçme konusunda rehberlik sağlar ve Web grubu çerçevesinin (WFF) bir sunucu grubundaki tüm Web sunucuları arasında dağıtılan Web uygulamalarını çoğaltmak için nasıl kullanılacağını açıklar.
- [Gelişmiş kurumsal Web dağıtımı](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). Bu öğreticide, birden çok ortam için veritabanı dağıtımlarını özelleştirme, dağıtımdan dosya ve klasörleri dışarıda bırakma ve dağıtım işlemi sırasında Web uygulamalarını çevrimdışına alma gibi çeşitli gelişmiş dağıtım görevlerinin nasıl yapılacağı açıklanmaktadır. .

> [!div class="step-by-step"]
> [Next](creating-a-team-project-in-tfs.md)
