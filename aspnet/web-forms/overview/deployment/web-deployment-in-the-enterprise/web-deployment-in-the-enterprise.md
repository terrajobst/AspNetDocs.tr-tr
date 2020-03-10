---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: Kuruluşta Web dağıtımı | Microsoft Docs
author: jrjlee
description: Bu öğreticide, kurumsal ölçekte Web uygulamalarının dağıtımını dengeleyerek yönettiğinizde karşılaştığınız birçok zorluğu nasıl karşılamakta olduğunuz açıklanmaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: bc7bb676a71af4ec3451aa3adf3c03ce3b5200d5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628172"
---
# <a name="web-deployment-in-the-enterprise"></a>Kurumda Web Dağıtımı

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu öğreticide, kurumsal ölçekte Web uygulamalarının dağıtımını geliştirme, test, hazırlama ve üretim ortamlarında yönettiğinizde karşılaşabileceğiniz birçok zorluğu ele alma açıklanmaktadır. Öğreticide, çeşitli genel görevler ve yordamlarda size rehberlik etmek için kavramsal ve görev odaklı içerik karışımından oluşan bir başvuru çözümü bulunur.
> 
> Bu öğreticilerin Italyanca çevirisi için [http://www.lucamorelli.it](http://www.lucamorelli.it)ziyaret edin.

## <a name="enterprise-deployment-challenges"></a>Kurumsal Dağıtım zorlukları

Kuruluşlar, karmaşık, kurumsal ölçekte çözümlerin dağıtımını yönetmek üzere görüntiklerinde genellikle bu güçlükleri öğreniyor:

- Geliştirici veya test ortamları, hazırlama platformları ve üretim sunucuları gibi birden çok ortama proje dağıtabilmeniz gerekir. Çözümün her ortam için farklı yapılandırma ayarlarıyla dağıtılması gerekir.
- Tek adımlı veya otomatik derleme ve dağıtım sürecinin bir parçası olarak birden fazla bağımlı projeyi aynı anda dağıtmanız gerekir.
- Otomatik bir işlemden dağıtım sürücünüzü sağlayabilmeniz gerekir. Örneğin, yeni kod iade edildiğinde bir test ortamına Web uygulamaları dağıtmak için bir sürekli tümleştirme (CI) işlemi kullanmak istiyorsunuz.
- Geliştiricilerin, doğru yapılandırma ayarlarına veya her hedef ortam için gerekli kimlik bilgilerine sahip olması olası olduğundan, dağıtım işlemini denetleyebilmeniz ve dağıtım değişkenlerini Visual Studio 'Nun dışında ayarlamanız gerekir.
- Şema tabanlı veritabanı projelerini dağıtmanız ve sonraki dağıtımlarda mevcut verileri korumanız gerekir.
- Kullanıcı hesabı verilerini dağıtmadan, üyelik veritabanlarını bir geçici temele göre dağıtmanız gerekir. Ayrıca, mevcut kullanıcı hesabı verilerini kaybetmeden dağıtılan üyelik veritabanlarının şemasını güncelleştirmeniz gerekebilir.
- Çeşitli hedef ortamlara içerik dağıtırken belirli dosya veya klasörleri hariç bırakmanız gerekir.

## <a name="overview-of-approach"></a>Yaklaşıma genel bakış

Bu öğreticide, bu serideki diğer öğreticiler ile birlikte, yukarıda açıklanan güçlükleri karşılamak için bu üst düzey yaklaşımı kullanır.

- **Genel derleme ve dağıtım sürecini denetlemek için özel Microsoft Build Engine (MSBuild) proje dosyaları kullanın.**
- Bu, çözümdeki her projeyi tek, komut dosyalı bir işlemin parçası olarak derleyip dağıtmanıza imkan tanır.
- Ortama özel ayarlar, ortama özgü basit proje dosyaları kullanılarak yapılandırılır. Farklı ortamlara yönelik dağıtımları yapılandırmak için çözüm yapılandırmalarının ve yayımlama profillerinin kullanıldığı Visual Studio merkezli yaklaşımının aksine, bu yaklaşım dağıtım işlemini Visual Studio 'Nun dışından yapılandırmanıza ve yönetmenize olanak sağlar. Bu, geliştiricilerin bağlantı dizeleri, hizmet uç noktaları, sunucu kimlik bilgileri ve hedef ortamlar için diğer dağıtım değişkenleriyle ilgili bilgi sahibi olmayacağı anlamına gelir.
- Özel proje dosyaları, takım derlemesi tarafından Team Foundation Server (TFS) iş akışının bir parçası olarak çağrılabilir. Bu, CI senaryoları için otomatik dağıtımı yapılandırmanızı sağlar.

**Web uygulaması projelerini paketlemek ve dağıtmak için Internet Information Services (IIS) Web Dağıtım aracı 'nı (Web Dağıtımı) kullanın.**

- Web Dağıtımı, Web uygulaması içeriğinizi, bağımlılıklar, yapılandırma ayarları, güvenlik ayarları ve diğer gereksinimlerle birlikte bir hedef IIS Web sunucusuna paketlemenizi ve dağıtmanızı sağlayan bir çerçeve sağlar.
- Tüm paketleme ve dağıtım sürecinin özel MSBuild proje dosyalarınızda içinden denetimini yapabilirsiniz. Ayrıca, bağlantı dizeleri, hizmet uç noktaları ve IIS hedef ayrıntıları gibi Web Dağıtım paketinize eşlik eden yapılandırma ayarlarını da düzenleyebilirsiniz.
- Web yayımlama işlem hattı ile birlikte Web Dağıtımı, dağıtımlarınızı özelleştirmenize olanak sağlayan çok sayıda genişletilebilirlik noktası sunar. Örneğin, istenmeyen dosya ve klasörleri Web Dağıtım paketlerinizden dışlamak kolaydır.

**Veritabanı şemalarını dağıtmak ve güncelleştirmek için VSDBCMD. exe yardımcı programını kullanın.**

- VSDBCMD, bir Visual Studio veritabanı projesi oluşturduğunuzda oluşturulan bir veritabanı şema dosyasından (. dbschema) veritabanları dağıtmanıza olanak tanır. Buna karşılık, Web Dağıtımı dahil edilen veritabanı dağıtım işlevleri, mevcut veritabanlarını yerel bir SQL Server örneğinden dağıtmaya daha uygundur.
- Visual Studio 'nun veritabanı projelerini dağıtmaya yönelik işlevselliğinin aksine, VSDBCMD varolan bir hedef veritabanına fark güncelleştirmeleri dağıtmanızı sağlar. Bu, veritabanı şemasını yükseltirken mevcut tüm verileri korumanıza olanak sağlar.
- VSDBCMD komutlarını özel MSBuild proje dosyalarınız içinden çalıştırabilirsiniz.

## <a name="content-map"></a>İçerik haritası

Bu öğretici dört ana alana giren konuları içerir.

Bu konu başlığı altında, başvuru&#x2014;çözümü Contact Manager çözümü&#x2014;ele alınır ve bunun nasıl indirileceği ve yerel makinenizde nasıl yapılandırılacağı açıklanır:

- [Kişi Yöneticisi Çözümü](the-contact-manager-solution.md)
- [Kişi Yöneticisi Çözümünü Ayarlama](setting-up-the-contact-manager-solution.md)

Bu konularda MSBuild proje dosyaları tanıtılmaktadır, özel proje dosyalarını nasıl oluşturup kullanabileceğinizi ve Ilgili kişi Yöneticisi çözümü için dağıtım sürecini nasıl yürütebilmeniz açıklanmaktadır:

- [Proje Dosyasını Anlama](understanding-the-project-file.md)
- [Derleme İşlemini Anlama](understanding-the-build-process.md)

Bu konularda, derleme ve paketleme işleminin nasıl çalıştığı, derleme işleminin Web yayımlama işlem hattı ile nasıl tümleştirileceği, dağıtım parametrelerinin nasıl değiştirileceği ve hedefe Web paketlerinin nasıl dağıtılacağı dahil olmak üzere Web uygulaması dağıtımı anlatılmaktadır lý

- [Web Uygulaması Projelerini Derleme ve Paketleme](building-and-packaging-web-application-projects.md)
- [Web Paketi Dağıtımı için Parametreleri Yapılandırma](configuring-parameters-for-web-package-deployment.md)
- [Web Paketleri Dağıtma](deploying-web-packages.md)

- [Veritabanı projelerini dağıtmak](deploying-database-projects.md) , her yaklaşımın avantajları ve dezavantajları Ile birlikte Visual Studio veritabanı projelerini dağıtmak için kullanabileceğiniz farklı teknikleri açıklar. [Dağıtım komut dosyası oluşturma ve çalıştırma](creating-and-running-a-deployment-command-file.md) , dağıtım mantığınızı kapsülleyen ve karmaşık çözümleri tek adımlı bir işlem olarak dağıtmanıza imkan tanıyan basit bir komut dosyasının nasıl oluşturulacağını açıklar.
- Son olarak, [Web paketlerinin el Ile yüklenmesi](manually-installing-web-packages.md) , Web paketlerini IIS 'e aktarmanıza yönelik olarak öğreticiyi gösterir.

## <a name="key-technologies"></a>Anahtar teknolojileri

Bu öğreticideki konular öncelikle derleme ve dağıtımı yönetmek için bu teknolojileri kullanır:

- Visual Studio 2010
- MSBuild
- IıS 7,5
- Web Deploy 2.0
- VSDBCMD. exe veritabanı dağıtım yardımcı programı

## <a name="other-tutorials-in-this-series"></a>Bu serideki diğer öğreticiler

Bu, kurumsal ölçekte Web dağıtımında bir dizi beş öğreticilerin bir parçasını oluşturur. Serideki diğer öğreticiler şunlardır:

- [Kurumsal senaryolarda Web uygulamaları dağıtma](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Bu giriş içeriği, öğretici serisi için bağlamsal arka plan sağlar. Öğretici senaryosunu açıklar ve diziler genelinde açıklanan görevlerin ve talimatların daha geniş bir uygulama yaşam döngüsü yönetimi (ALM) sürecine sığması gösterilmektedir.
- [Web dağıtımı Için sunucu ortamlarını yapılandırma](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). Bu öğreticide, Windows sunucularının Web Deployment Agent hizmeti (uzak Aracı) veya Web Dağıtımı Işleyicisi ile uzak veritabanı dağıtımı kullanılarak uzak Web paketi dağıtımı gibi çeşitli dağıtım senaryolarını destekleyecek şekilde nasıl yapılandırılacağı açıklanmaktadır. Kendi ortamınız için uygun dağıtım yöntemini seçme konusunda rehberlik sağlar ve Web grubu çerçevesinin (WFF) bir sunucu grubundaki tüm Web sunucuları arasında dağıtılan Web uygulamalarını çoğaltmak için nasıl kullanılacağını açıklar.
- [Web dağıtımı için Team Foundation Server yapılandırılıyor](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). Bu öğreticide, bir CI işleminin parçası olarak otomatik dağıtım ve belirli derlemelerin el ile tetiklenen çeşitli dağıtım senaryolarını desteklemek üzere TFS 'nin nasıl yapılandırılacağı açıklanmaktadır.
- [Gelişmiş kurumsal Web dağıtımı](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). Bu öğreticide, birden çok ortam için veritabanı dağıtımlarını özelleştirme, dağıtımdan dosya ve klasörleri dışarıda bırakma ve dağıtım işlemi sırasında Web uygulamalarını çevrimdışına alma gibi çeşitli gelişmiş dağıtım görevlerinin nasıl yapılacağı açıklanmaktadır. .

> [!div class="step-by-step"]
> [Next](the-contact-manager-solution.md)
