---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 'Senaryo: Web dağıtımı için bir test ortamı yapılandırma | Microsoft Docs'
author: jrjlee
description: Bu konuda, geliştirici veya test ortamları için tipik bir Web Dağıtım senaryosu açıklanmakta ve bir sı kurmak için gerçekleştirmeniz gereken görevler açıklanmaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: d580e550f2461837f0e8a4e477273348b49cb53e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637818"
---
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a>Senaryo: Web Dağıtımı için Test Ortamı Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, geliştirici veya test ortamları için tipik bir Web Dağıtım senaryosu açıklanmakta ve benzer bir ortam kurmak için gerçekleştirmeniz gereken görevler açıklanmaktadır.

Geliştiriciler Web uygulamaları üzerinde çalışırken, genellikle, uygulamalarına yapılan değişiklikleri gerçekçi bir ayarda test etmek için kullanabilecekleri bir sunucu ortamına erişim verilir. Bu tür bir geliştirme veya test ortamı genellikle şu özelliklere sahiptir:

- Ortam, tek bir Web sunucusundan ve tek bir veritabanı sunucusundan oluşur.
- Geliştiriciler, uygulamaları uygulamalarının gereksinimlerine göre yapılandırmalarına olanak sağlamak için genellikle sunucularda yönetici ayrıcalıklarına sahiptir.
- Uygulamalarda yapılan değişiklikler sıklıkla dağıtılır, bu nedenle ortamın tek adımlı veya otomatik dağıtımı desteklemesi gerekir.

Örneğin [öğretici senaryolarımızda](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Matt hink fabrikam 'daki bir geliştirici, Inc. Matt, Contact Manager çözümü üzerinde çalışıyor ve düzenli olarak değişiklikleri bir test ortamına dağıtmaları gerekir. Matt, test Web sunucusunda ve test veritabanı sunucusunda bir yöneticdir. Başlangıçta, bir çözümü doğrudan test ortamına dağıtabilmelidir.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

İş ilerledikçe ve daha fazla geliştirici takıma katılırsanız, Contact Manager çözümü Team Foundation Server (TFS) içinde sürekli tümleştirme (CI) için yapılandırılmıştır. Bir geliştirici içeriği her denetlediğinde, takım derlemesi çözümü derleyip, herhangi bir birim testini çalıştırmalıdır ve çözümü otomatik olarak test ortamına dağıtır.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>Çözüme genel bakış

Test ortamının uzak bir bilgisayardan tek adımlı veya otomatik dağıtımı desteklemesi gerekir, bu nedenle iki ana yaklaşımdan birini tercih edersiniz. Şunları yapabilirsiniz:

- Web Deployment Agent hizmetini ("uzak Aracı") kullanarak dağıtımı desteklemek için test Web sunucusunu yapılandırın.
- Test Web sunucusunu Web Dağıtımı işleyicisini kullanarak dağıtımı destekleyecek şekilde yapılandırın.

> [!NOTE]
> Ayrıca, Isteğe bağlı [Web dağıtımı](https://technet.microsoft.com/library/ee517345(WS.10).aspx) ("geçici aracı") de kullanabilirsiniz. Bu, gereksinimler ve kısıtlamalar açısından uzak Aracı yaklaşımına benzerdir.

Bu durumda, geliştiricilerin hedef sunucularda yönetici ayrıcalıkları vardır ve test ortamı katı güvenlik kısıtlamalarına tabi değildir, bu nedenle mantıksal seçim, test Web sunucusunu uzak aracıyı kullanarak dağıtımı destekleyecek şekilde yapılandırmaktır. Bu daha az karmaşıktır ve Web Dağıtımı Işleyici yaklaşımına göre daha az başlangıç yapılandırması gerektirir. Ayrıca, veritabanı sunucunuzu uzaktan erişim ve dağıtımı destekleyecek şekilde yapılandırmanız gerekir.

Bu konular, bu görevleri gerçekleştirmek için ihtiyacınız olan tüm bilgileri sağlar:

- [Bir Web sunucusunu Web dağıtımı yayımlaması (uzak Aracı) Için yapılandırın](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md). Bu konuda, temiz bir Windows Server 2008 R2 derlemesinden başlayarak uzak Aracı yaklaşımını kullanarak Web Dağıtımı yayımlamayı destekleyen bir Web sunucusunun nasıl oluşturulacağı açıklanmaktadır.
- [Web dağıtımı yayımlaması için bir veritabanı sunucusu yapılandırın](configuring-a-database-server-for-web-deploy-publishing.md). Bu konuda, bir veritabanı sunucusunun varsayılan bir SQL Server 2008 R2 yüklemesinden başlayarak uzaktan erişim ve dağıtımı destekleyecek şekilde nasıl yapılandırılacağı açıklanmaktadır.

## <a name="further-reading"></a>Daha Fazla Bilgi

Tipik bir hazırlama ortamını yapılandırma hakkında yönergeler için bkz. [Senaryo: Web dağıtımı Için hazırlama ortamı yapılandırma](scenario-configuring-a-staging-environment-for-web-deployment.md). Tipik bir üretim ortamını yapılandırma hakkında yönergeler için bkz. [Senaryo: Web dağıtımı Için üretim ortamı yapılandırma](scenario-configuring-a-production-environment-for-web-deployment.md).

> [!div class="step-by-step"]
> [Önceki](choosing-the-right-approach-to-web-deployment.md)
> [İleri](scenario-configuring-a-staging-environment-for-web-deployment.md)
