---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
title: Birden çok ortam için veritabanı dağıtımlarını özelleştirme | Microsoft Docs
author: jrjlee
description: 'Bu konu, dağıtım sürecinin bir parçası olarak bir veritabanının özelliklerinin belirli hedef ortamlara nasıl yapılandırılacağını açıklamaktadır. Note: konu başlığı...'
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a172979a-1318-4318-a9c6-4f9560d26267
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
msc.type: authoredcontent
ms.openlocfilehash: 8ae8cb1a322afb95c5d2e8d5e73c7825c7b2fe5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78604029"
---
# <a name="customizing-database-deployments-for-multiple-environments"></a>Birden Çok Ortam için Veritabanı Dağıtımlarını Özelleştirme

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, dağıtım sürecinin bir parçası olarak bir veritabanının özelliklerinin belirli hedef ortamlara nasıl yapılandırılacağını açıklamaktadır.
> 
> > [!NOTE]
> > Bu konuda, MSBuild. exe ve VSDBCMD. exe kullanarak bir Visual Studio 2010 veritabanı projesi dağıttığınız varsayılmaktadır. Bu yaklaşımı neden seçebilecek hakkında daha fazla bilgi için bkz. [Enterprise 'Ta Web dağıtımı](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) ve [veritabanı projelerini dağıtma](../web-deployment-in-the-enterprise/deploying-database-projects.md).
> 
> 
> Birden çok hedefe bir veritabanı projesi dağıttığınızda, genellikle her bir hedef ortam için veritabanı dağıtım özelliklerini özelleştirmek isteyeceksiniz. Örneğin, test ortamlarında veritabanını her dağıtımda genellikle yeniden oluşturmanız gerekir, hazırlık veya üretim ortamlarında verilerinizi korumak için artımlı güncelleştirmeler yapmanız çok daha olasıdır.
> 
> Visual Studio 2010 veritabanı projesinde, dağıtım ayarları bir dağıtım yapılandırma (. sqldeployment) dosyası içinde yer alır. Bu konu, ortama özel dağıtım yapılandırma dosyalarını nasıl oluşturacağınız ve VSDBCMD parametresi olarak kullanmak istediğiniz bir parametreyi nasıl belirtmektir.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="task-overview"></a>Göreve genel bakış

Bu konuda aşağıdakiler varsayılmaktadır:

- Proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklandığı gibi, çözüm dağıtımına bölünmüş proje dosyası yaklaşımını kullanabilirsiniz.
- [Yapı sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md)bölümünde açıklandığı gibi, veritabanı projenizi dağıtmak için, proje dosyasından VSDBCMD ' i çağırın.

Hedef ortamlar arasında veritabanı dağıtım özelliklerini farklı şekilde destekleyen bir dağıtım sistemi oluşturmak için şunları yapmanız gerekir:

- Her hedef ortam için bir dağıtım yapılandırma (. sqldeployment) dosyası oluşturun.
- Dağıtım yapılandırma dosyasını bir komut satırı anahtarı olarak belirten bir VSDBCMD komutu oluşturun.
- Bir Microsoft Build Engine (MSBuild) proje dosyasında VSDBCMD komutunu parametreleştirin, böylece VSDBCMD seçeneklerinin hedef ortama uygun olması gerekir.

Bu konu, bu yordamların her birini nasıl gerçekleştirekullanacağınızı gösterir.

## <a name="creating-environment-specific-deployment-configuration-files"></a>Ortama özel dağıtım yapılandırma dosyaları oluşturma

Varsayılan olarak, bir veritabanı projesi *Database. sqldeployment*adlı tek bir dağıtım yapılandırma dosyası içerir. Bu dosyayı Visual Studio 2010 ' de açarsanız, kullanabileceğiniz farklı dağıtım seçeneklerini görebilirsiniz:

- **Dağıtım karşılaştırma harmanlaması**. Bu, projenizin veritabanı harmanlamasını ( *kaynak* harmanlama) veya hedef sunucunuzun veritabanı harmanlamasını ( *hedef* harmanlama) kullanmayı seçmenizi sağlar. Çoğu durumda, bir geliştirme veya test ortamına dağıtırken kaynak harmanlamayı kullanmak isteyeceksiniz. Bir hazırlık veya üretim ortamına dağıtırken, birlikte çalışabilirlik sorunlarından kaçınmak için genellikle hedef harmanlamanın değişmeden kalmasını istersiniz.
- **Veritabanı özelliklerini dağıtın**. Bu, Database *. sqlsettings* dosyasında tanımlandığı şekilde veritabanı özelliklerinin uygulanıp uygulanmayacağını seçmenize olanak sağlar. Bir veritabanını ilk kez dağıttığınızda, veritabanı özelliklerini dağıtmanız gerekir. Var olan bir veritabanını güncelleştiriyorsanız özellikler zaten yerinde olmalıdır ve bunları yeniden dağıtmanız gerekmez.
- **Veritabanını her zaman yeniden oluşturun**. Bu, hedef veritabanını her dağıttığınız zaman yeniden oluşturmayı seçmenizi veya hedef veritabanını şemanıza göre güncel hale getirmek için artımlı değişiklikler yapmanızı sağlar. Veritabanını yeniden oluşturursanız, var olan veritabanındaki tüm verileri kaybedersiniz. Bu nedenle, hazırlık veya üretim ortamları için dağıtımları genellikle **false** olarak ayarlamanız gerekir.
- **Veri kaybı oluşmayabilir, artımlı dağıtımı engelleyin**. Bu, veritabanı şemasında yapılan bir değişiklik veri kaybına neden olursa dağıtımın durdurulup durdurulmayacağını seçmenizi sağlar. Genellikle bunu bir üretim ortamına dağıtım için **doğru** olarak ayarlarsanız, önemli verileri müdahale etmek ve korumak için bir fırsat sağlar. **Veritabanını her zaman false olarak yeniden oluşturursanız** , bu ayarınhiçbir etkisi olmayacaktır.
- **Dağıtımı tek kullanıcı modunda yürütün**. Bu genellikle geliştirme veya test ortamlarındaki bir sorun değildir. Ancak, hazırlık veya üretim ortamları için dağıtım için genellikle bunu **true** olarak ayarlamanız gerekir. Bu, dağıtım devam ederken kullanıcıların veritabanında değişiklik yapmalarını önler.
- **Dağıtımdan önce veritabanını yedekleyin**. Bunu, veri kaybına karşı bir önlem olarak bir üretim ortamına dağıtırken, genellikle **doğru** olarak ayarlarsınız. Hazırlama veritabanınız çok miktarda veri içeriyorsa, hazırlama ortamına dağıtırken bunu **true** olarak ayarlamak da isteyebilirsiniz.
- **Hedef veritabanındaki, ancak veritabanı projesinde olmayan nesneler IÇIN drop deyimleri üretin**. Çoğu durumda bu, bir veritabanında artımlı değişiklikler yapmanın tam ve önemli bir parçasıdır. **Veritabanını her zaman false olarak yeniden oluşturursanız** , bu ayarınhiçbir etkisi olmayacaktır.
- **CLR türlerini güncelleştirmek IÇIN alter assembly deyimlerini kullanmayın**. Bu ayar, SQL Server ortak dil çalışma zamanı (CLR) türlerini daha yeni derleme sürümlerine güncelleştirme şeklini belirler. Çoğu senaryoda bu, **false** olarak ayarlanmalıdır.

Bu tabloda, farklı hedef ortamları için tipik dağıtım ayarları gösterilmektedir. Ancak, ayarlarınız tam gereksinimlerinize bağlı olarak farklı olabilir.

|  | Geliştirici/test | Hazırlama/tümleştirme | Üretim |
| --- | --- | --- | --- |
| **Dağıtım karşılaştırma harmanlama** | Kaynak | Hedef | Hedef |
| **Veritabanı özelliklerini dağıtma** | Doğru | Yalnızca ilk kez | Yalnızca ilk kez |
| **Veritabanını her zaman yeniden oluştur** | Doğru | False | False |
| **Veri kaybı oluşmayabilir, artımlı Dağıtımı engelle** | False | Belki de | Doğru |
| **Dağıtım betiğini tek kullanıcılı modda yürütme** | False | Doğru | Doğru |
| **Dağıtımdan önce veritabanını yedekleme** | False | Belki de | Doğru |
| **Hedef veritabanındaki, ancak veritabanı projesinde olmayan nesneler için DROP deyimleri oluşturma** | False | Doğru | Doğru |
| **ALTER ASSEMBLY deyimlerini kullanarak CLR türlerini güncelleştirme** | False | False | False |

> [!NOTE]
> Veritabanı dağıtım özellikleri ve ortam konuları hakkında daha fazla bilgi için, bkz. [veritabanı proje ayarlarına genel bakış](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx), [nasıl yapılır: dağıtım ayrıntıları için özellikleri yapılandırma](https://msdn.microsoft.com/library/dd172125.aspx), [yalıtılmış bir geliştirme ortamında veritabanı oluşturma ve dağıtma](https://msdn.microsoft.com/library/dd193409.aspx)ve [veritabanlarını bir hazırlama veya üretim ortamında yapılandırma ve dağıtma](https://msdn.microsoft.com/library/dd193413.aspx).

Bir veritabanı projesinin birden çok hedefe dağıtımını desteklemek için, her hedef ortam için bir dağıtım yapılandırma dosyası oluşturmanız gerekir.

**Ortama özgü bir yapılandırma dosyası oluşturmak için**

1. Visual Studio 2010 ' de, **Çözüm Gezgini** penceresinde, veritabanı projenize sağ tıklayın ve ardından **Özellikler**' e tıklayın.
2. Veritabanı projesi özellikleri sayfasında, **Dağıt** sekmesinde, **dağıtım yapılandırma dosyası** satırında **Yeni**' ye tıklayın.

    ![](customizing-database-deployments-for-multiple-environments/_static/image1.png)
3. **Yeni dağıtım yapılandırma dosyası** iletişim kutusunda dosyaya anlamlı bir ad verin (örneğin, **TestEnvironment. sqldeployment**) ve ardından **Kaydet**' e tıklayın.
4. *[Filename] * * *. sqldeployment** sayfasında, dağıtım özelliklerini hedef ortamınızın gereksinimleriyle eşleşecek şekilde ayarlayın ve dosyayı kaydedin.

    ![](customizing-database-deployments-for-multiple-environments/_static/image2.png)
5. Yeni dosya, veritabanı projenizdeki Özellikler klasörüne eklendiğine dikkat edin.

    ![](customizing-database-deployments-for-multiple-environments/_static/image3.png)

## <a name="specifying-the-deployment-configuration-file-in-vsdbcmd"></a>VSDBCMD 'de dağıtım yapılandırma dosyasını belirtme

Visual Studio 2010 içinde çözüm yapılandırmalarını (hata ayıklama ve yayın gibi) kullandığınızda, bir dağıtım yapılandırma dosyasını her yapılandırmayla ilişkilendirebilirsiniz. Belirli bir yapılandırma oluşturduğunuzda, yapı işlemi yapılandırmaya özgü dağıtım yapılandırma dosyasını işaret eden yapılandırmaya özgü bir dağıtım bildirim dosyası oluşturur. Bununla birlikte, bu öğreticilerde açıklanan, dağıtıma yönelik yaklaşımlardan biri, kişilere Visual Studio 2010 ve çözüm yapılandırmalarına gerek kalmadan dağıtım sürecini denetleme olanağı vermektir. Bu yaklaşımda, çözüm yapılandırması, hedef dağıtım ortamından bağımsız olarak aynıdır. Veritabanı dağıtımınızı belirli bir hedef ortama uyarlamak için, dağıtım yapılandırma dosyanızı belirtmek üzere VSDBCMD komut satırı seçeneklerini kullanabilirsiniz.

VSDBCMD dosyanızda bir dağıtım yapılandırma dosyası belirtmek için **p:/DeploymentConfigurationFile** anahtarını kullanın ve dosyanızın tam yolunu sağlayın. Bu, dağıtım bildiriminin tanımladığı dağıtım yapılandırma dosyasını geçersiz kılar. Örneğin, **ContactManager** veritabanını bir test ortamına dağıtmak IÇIN bu VSDBCMD komutunu kullanabilirsiniz:

[!code-console[Main](customizing-database-deployments-for-multiple-environments/samples/sample1.cmd)]

> [!NOTE]
> Yapı işleminin dosyayı çıkış dizinine kopyaladığında. sqldeployment dosyanızı yeniden adlandırabileceğini unutmayın.

Dağıtım öncesi veya dağıtım sonrası SQL betiklerinizde SQL komut değişkenlerini kullanırsanız, ortama özgü bir. sqlcmdvars dosyasını dağıtımınızla ilişkilendirmek için benzer bir yaklaşım kullanabilirsiniz. Bu durumda,. sqlcmdvars dosyanızı tanımlamak için **p:/SqlCommandVariablesFile** anahtarını kullanın.

## <a name="running-the-vsdbcmd-command-from-an-msbuild-project-file"></a>Bir MSBuild proje dosyasından VSDBCMD komutunu çalıştırma

MSBuild hedefi içindeki bir **Exec** görevi kullanarak MSBuild proje dosyasından VSDBCMD komutunu çağırabilirsiniz. En basit biçiminde şöyle görünür:

[!code-xml[Main](customizing-database-deployments-for-multiple-environments/samples/sample2.xml)]

- Uygulamada, proje dosyalarınızın okunmasını ve yeniden kullanılmasını kolaylaştırmak için çeşitli komut satırı parametrelerini depolamak üzere özellikler oluşturmak isteyeceksiniz. Bu, kullanıcıların ortama özgü bir proje dosyasında özellik değerleri sağlamasını veya varsayılan değerleri MSBuild komut satırından geçersiz kılmasını kolaylaştırır. [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını kullanırsanız, derleme yönergelerinizi ve özelliklerini iki Dosya arasında uygun şekilde bölmeniz gerekir:
- Dağıtım yapılandırma dosya adı, veritabanı bağlantı dizesi ve hedef veritabanı adı gibi ortama özgü ayarların ortama özgü proje dosyasında olması gerekir.
- VSDBCMD komutunu çalıştıran MSBuild hedefi, VSDBCMD yürütülebilir dosyasının konumu gibi evrensel özelliklerle birlikte, evrensel proje dosyasına gitmelidir.

Ayrıca,. DeployManifest dosyasının oluşturulup kullanıma hazırlanabilmesi için VSDBCMD ' i çağırmadan önce veritabanı projesini oluşturduğunuzdan emin olmanız gerekir. Bu yaklaşımın tam bir örneğini, [Contact Manager örnek çözümünde](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)proje dosyaları boyunca size yol gösteren [derleme işlemini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md)konusunda görebilirsiniz.

## <a name="conclusion"></a>Sonuç

Bu konu, MSBuild ve VSDBCMD kullanarak veritabanı projelerini dağıtırken veritabanı özelliklerini farklı hedef ortamlara nasıl özelleştirebileceğiniz açıklanmıştır. Bu yaklaşım, daha büyük, kurumsal ölçekli çözümlerin parçası olarak veritabanı projelerini dağıtmanız gerektiğinde faydalıdır. Bu çözümler genellikle korumalı geliştirme veya test ortamları, hazırlama veya tümleştirme platformları, üretim veya canlı ortamlar gibi birden çok hedefe dağıtılır. Bu hedef ortamların her biri genellikle benzersiz bir veritabanı dağıtım özellikleri kümesi gerektirir.

## <a name="further-reading"></a>Daha Fazla Bilgi

VSDBCMD. exe ' yi kullanarak veritabanı projelerini dağıtma hakkında daha fazla bilgi için bkz. [veritabanı projelerini dağıtma](../web-deployment-in-the-enterprise/deploying-database-projects.md). Dağıtım işlemini denetlemek için özel MSBuild proje dosyalarını kullanma hakkında daha fazla bilgi için bkz. [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md) ve [derleme sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

MSDN 'deki Bu makaleler veritabanı dağıtımı hakkında daha genel rehberlik sağlar:

- [Veritabanı proje ayarlarına genel bakış](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)
- [Nasıl yapılır: dağıtım ayrıntıları için özellikleri yapılandırma](https://msdn.microsoft.com/library/dd172125.aspx)
- [Yalıtılmış bir geliştirme ortamına veritabanları oluşturun ve dağıtın](https://msdn.microsoft.com/library/dd193409.aspx)
- [Hazırlama veya üretim ortamına veritabanları oluşturun ve dağıtın](https://msdn.microsoft.com/library/dd193413.aspx)

> [!div class="step-by-step"]
> [Önceki](performing-a-what-if-deployment.md)
> [İleri](deploying-database-role-memberships-to-test-environments.md)
