---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: Gelişmiş kurumsal Web dağıtımı | Microsoft Docs
author: jrjlee
description: Bu öğreticide, birçok kurumsal dağıtım senaryosunda gereken veya istenen çeşitli görevlerin nasıl gerçekleştirileceği gösterilir. Italyan translati için...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: bf4c7d021763017592483df35cb717295c4924aa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587607"
---
# <a name="advanced-enterprise-web-deployment"></a>Gelişmiş Kurumsal Web Dağıtımı

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu öğreticide, birçok kurumsal dağıtım senaryosunda gereken veya istenen çeşitli görevlerin nasıl gerçekleştirileceği gösterilir.
> 
> Bu öğreticilerin Italyanca çevirisi için [http://www.lucamorelli.it](http://www.lucamorelli.it)ziyaret edin.

Bu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, WINDOWS COMMUNICATION FOUNDATION&#x2014;(WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) çözümünü kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren iki [](../web-deployment-in-the-enterprise/understanding-the-build-process.md)proje&#x2014;dosyası tarafından denetlendiği ve ortama özgü derleme ve dağıtım ayarlarını Içeren, derleme işlemini anlama bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="scenario-overview"></a>Senaryoya Genel Bakış

Bu öğreticiler için üst düzey senaryo, [Kurumsal Web dağıtımında açıklanmıştır: senaryoya genel bakış](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md). Bu öğreticide çalışmaya başlamadan önce bu konuyu incelemenizi öneririz.

## <a name="how-to-use-this-tutorial"></a>Bu öğreticiyi kullanma

- Bu öğreticideki konuların her biri kendi içindedir ve kurumsal dağıtım senaryolarında oluşan belirli bir zorluk veya sorunu ele alır. Bu konularda belirli bir sırada çalışmanız gerekmez. Ancak, bu öğretici bazı gelişmiş görevleri ele almaktadır. Bu nedenle, kurumsal öğreticideki [Web dağıtımının](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) bu içerikten en iyi şekilde yararlanmak için sunduğu kavramların ve tekniklerin öğrenmesini öğrenmeniz gerekir.
- Bu öğretici aşağıdaki konuları içerir:
- ["What If" dağıtımı gerçekleştiriliyor](performing-a-what-if-deployment.md). Çok sayıda senaryoda, herhangi bir değişiklik yapmadan önce bir hedef ortamda veya var olan herhangi bir içerik üzerinde önerilen bir dağıtımın etkisini öğrenmek isteyeceksiniz. Bu konu başlığı altında herhangi bir değişiklik yapmadan, bir hedef ortama içerik dağıtmışsınız gibi, günlük dosyaları ve veritabanı güncelleştirme betikleri oluşturmak için "ne yapılır" dağıtımının nasıl çalıştırılabildiği açıklanmaktadır. Bu kaynakların çözümlenmesi, canlı dağıtımdan önce olası sorunları belirlemenize yardımcı olabilir.
- [Birden çok ortam Için veritabanı dağıtımlarını özelleştirme](customizing-database-deployments-for-multiple-environments.md). Bir veritabanı projesini birden çok hedefe dağıttığınızda, genellikle her bir hedef ortam için dağıtım özelliklerini özelleştirmek isteyeceksiniz. Örneğin, test ortamlarında veritabanını her dağıtımda genellikle yeniden oluşturmanız gerekir, hazırlık veya üretim ortamlarında verilerinizi korumak için artımlı güncelleştirmeler yapmanız çok daha olasıdır. Bu konu başlığı altında, her hedef ortam için ortama özel dağıtım yapılandırma (. sqldeployment) dosyası oluşturarak bu özellik değişikliklerinin dağıtım mantığınıza nasıl dahil edileceğini açıklanmaktadır.
- Test ortamlarına veritabanı rolü üyelikleri dağıtma. Her dağıtımda&#x2014;bir veritabanını yeniden oluşturduğunuzda bir sürekli TÜMLEŞTIRME (CI) yapısının parçası olarak bir test ortamına&#x2014;dağıtın ve genellikle veritabanı rolü üyeliklerini her seferinde yapılandırmanız gerekir. Örneğin, genellikle Web uygulamanızla ilişkili uygulama havuzu kimliğine izin vermeniz gerekir. Bu konu, dağıtım mantığınıza bir dağıtım sonrası SQL betiği ekleyerek bu süreci otomatikleştirebileceğinizi açıklamaktadır.
- [Kurumsal ortamlara üyelik veritabanları dağıtma](deploying-membership-databases-to-enterprise-environments.md). ASP.NET üyelik veritabanlarının dağıtım sürecini karmaşıklaştırmak için çeşitli özellikleri vardır. Örneğin, yalnızca bir şema dağıtımı veritabanını işlemsel olmayan bir durumda bırakır. Çoğu senaryoda, her hedef ortamda doğrudan bir üyelik veritabanı oluşturulması tercih edilir. Ancak, bir üyelik veritabanı dağıtmanız gerekiyorsa, bu konuda, ilgili zorlukları karşılamak için kullanabileceğiniz yaklaşımlardan bazıları açıklanmaktadır.
- [Dosya ve klasörlerin dağıtımdan dışlanması](excluding-files-and-folders-from-deployment.md). Bazı senaryolarda, Web paketinizin içeriğini belirli hedef ortamlara uyarlamak isteyeceksiniz. Örneğin, bir test ortamına dağıtırken, istemci tarafı hata ayıklamayı desteklemek için JavaScript kitaplıklarının tam sürümlerini dahil etmek isteyebilirsiniz, ancak bir hazırlama veya üretim ortamına dağıtırken kitaplıkların küçültülmüş sürümlerini kullanın. Bu konu, paket oluşturma işleminden belirli dosya ve klasörleri nasıl dışarıda bırakabileceğinizi açıklamaktadır.
- [Web dağıtımı Ile Web uygulamalarını çevrimdışına alma](taking-web-applications-offline-with-web-deploy.md). Bir hazırlık veya üretim ortamına çözümler dağıttığınızda, genellikle dağıtım işlemi süresince Web uygulamalarınızı çevrimdışına almanız gerekir. Bu konu başlığı altında, dağıtım işleminin başlangıcında Web uygulamanıza bir *uygulama\_çevrimdışı. htm* dosyasını nasıl ekleyebileceğiniz ve sonunda nasıl kaldırabileceğinizi anlatmaktadır. *App\_offline. htm* dosyası yerinde olduğunda, Web uygulamasına gözatabilen tüm kullanıcılar otomatik olarak *App\_. htm* dosyasına yönlendirilir.
- [MSBuild 'Ten Windows PowerShell betikleri çalıştırma](running-windows-powershell-scripts-from-msbuild-project-files.md). Birçok dağıtım senaryosu, kayıt defterine özel olay kaynakları ekleme veya SQL Server örnekleri arasında çoğaltmayı yapılandırma gibi daha karmaşık dağıtım sonrası eylemleri gerektirir. Bu eylemler genellikle Windows PowerShell betikleri aracılığıyla gerçekleştirilir. Bu konu, derleme ve dağıtım sürecinin bir parçası olarak bir Microsoft Build Engine (MSBuild) proje dosyasından Windows PowerShell komut dosyalarının nasıl çalıştırılacağını açıklamaktadır.
- [Paketleme sürecinde sorun giderme](troubleshooting-the-packaging-process.md). Web yayımlama işlem hattı (WPP), Web uygulaması projelerine yönelik paketleme işlemi hakkında ayrıntılı bilgi oluşturmak için kullanabileceğiniz **Enablepackageprocessloggingandassert** adlı bir MSBuild özelliği tanımlar. Bu konu, özelliğinin ne yaptığını ve nasıl kullanılacağını açıklar.

## <a name="key-technologies"></a>Anahtar teknolojileri

Bu öğretici, otomatik derleme ve Web dağıtımını desteklemek için bu ürünlerin ve teknolojilerin nasıl kullanılacağına odaklanır:

- Visual Studio 2010 ve Team Foundation Server (TFS) 2010
- MSBuild ve TFS takım derlemesi
- Internet Information Services (IIS) 7,5
- IIS Web Dağıtım Aracı (Web Dağıtımı) 2,1
- VSDBCMD. exe veritabanı dağıtım yardımcı programı

## <a name="other-tutorials-in-this-series"></a>Bu serideki diğer öğreticiler

Bu, kurumsal ölçekte Web dağıtımında bir dizi beş öğreticilerin bir parçasını oluşturur. Serideki diğer öğreticiler şunlardır:

- [Kurumsal senaryolarda Web uygulamaları dağıtma](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Bu giriş içeriği, öğretici serisi için bağlamsal arka plan sağlar. Öğretici senaryosunu açıklar ve diziler genelinde açıklanan görevlerin ve talimatların daha geniş bir uygulama yaşam döngüsü yönetimi (ALM) sürecine sığması gösterilmektedir.
- [Kuruluşta Web dağıtımı](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Bu öğreticide, MSBuild proje dosyaları, WPP, Web Dağıtımı ve diğer ilgili teknolojiler hakkında kavramsal bir giriş sunulmaktadır. Karmaşık dağıtım süreçlerini yönetmek için bu araçları birlikte nasıl kullanabileceğinizi açıklar.
- [Web dağıtımı Için sunucu ortamlarını yapılandırma](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). Bu öğreticide, Windows sunucularının Web Deployment Agent hizmeti (uzak Aracı) veya Web Dağıtımı Işleyicisi ile uzak veritabanı dağıtımı kullanılarak uzak Web paketi dağıtımı gibi çeşitli dağıtım senaryolarını destekleyecek şekilde nasıl yapılandırılacağı açıklanmaktadır. Kendi ortamınız için uygun dağıtım yöntemini seçme konusunda rehberlik sağlar ve Web grubu çerçevesinin (WFF) bir sunucu grubundaki tüm Web sunucuları arasında dağıtılan Web uygulamalarını çoğaltmak için nasıl kullanılacağını açıklar.
- [Web dağıtımı için Team Foundation Server yapılandırılıyor](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). Bu öğreticide, bir CI işleminin parçası olarak otomatik dağıtım ve belirli derlemelerin el ile tetiklenen çeşitli dağıtım senaryolarını desteklemek üzere TFS 'nin nasıl yapılandırılacağı açıklanmaktadır.

> [!div class="step-by-step"]
> [Next](performing-a-what-if-deployment.md)
