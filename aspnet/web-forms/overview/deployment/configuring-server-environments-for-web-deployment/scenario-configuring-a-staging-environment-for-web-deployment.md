---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 'Senaryo: Web dağıtımı için hazırlama ortamını yapılandırma | Microsoft Docs'
author: jrjlee
description: Bu konuda, hazırlama ortamı için tipik bir Web Dağıtım senaryosu açıklanmakta ve benzer bir env 'yi kurmak için gerçekleştirmeniz gereken görevler açıklanmaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eaa61ca850817f8dd98955b59e94be93389bf256
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637846"
---
# <a name="scenario-configuring-a-staging-environment-for-web-deployment"></a>Senaryo: Web Dağıtımı için Hazırlama Ortamı Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, bir hazırlama ortamı için tipik bir Web Dağıtım senaryosu açıklanmakta ve benzer bir ortam kurmak için gerçekleştirmeniz gereken görevler açıklanmaktadır.

Birçok kuruluş, Web uygulamalarına veya Web sitelerine yönelik güncelleştirmelerin önizlemesi için hazırlık ortamları kullanır. Bu, kuruluş dahilindeki kişilere site "canlı olmadan" veya diğer sözcüklerden bir üretim ortamına dağıtılmadan önce yeni işlevleri veya içeriği araştırma ve gözden geçirme şansı verir. Hazırlama ortamı, gerçekçi bir önizleme sağlamak için üretim ortamını mümkün olduğunca yakın bir şekilde çoğaltmak üzere tasarlanmıştır. Bu tür bir hazırlık ortamı genellikle şu özelliklere sahiptir:

- Ortam, genellikle Yük Devretme Kümelemesi ve veritabanı yansıtma ile birlikte birden fazla yük dengeli Web sunucusundan ve bir veya daha fazla veritabanı sunucusundan oluşur.
- Uygulamalar, bir geliştirme ekibi tarafından el ile veya bir ekip yapı sunucusu tarafından otomatik olarak dağıtılabilir.
- Uygulamaları dağıtan Kullanıcı veya işlem hesaplarının, hazırlama sunucularında yönetici ayrıcalıklarına sahip olması olası değildir.
- Uygulamalarda yapılan değişiklikler sıklıkla dağıtılır, bu nedenle ortamın tek adımlı veya otomatik dağıtımı desteklemesi gerekir.

> [!NOTE]
> Bir veritabanı dağıtımının birden çok sunucu arasında ölçeklendirilmesi, Bu öğreticinin kapsamı dışındadır. Bu alan hakkında daha fazla bilgi için lütfen [çevrimiçi SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx)'a başvurun.

Örneğin, [öğretici senaryolarımızda](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team FOUNDATION Server (TFS), Contact Manager çözümünü yönetir. Ramiz Walters TFS Yöneticisi, geliştiricilerin gereken hazırlama ortamına dağıtım tetiklemesine olanak tanıyan bir yapı tanımı oluşturmuştur.

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

Çoğu durumda, en son derlemeyi hazırlama ortamına dağıtmak istemeyebileceğine unutmayın. Bunun yerine, test ortamında zaten bir onaylama ve doğrulama işlemi olan belirli bir derlemeyi dağıtmak istemeniz çok daha olasıdır.

## <a name="solution-overview"></a>Çözüme genel bakış

Bu senaryoda, dağıtım gereksinimlerinin bir analizinden bu olguları getirebilirsiniz:

- Dağıtımı gerçekleştiren kullanıcı veya işlem hesabı, hazırlama sunucularında yönetici ayrıcalıklarına sahip olmayacaktır, bu nedenle hazırlama Web sunucularının yönetici olmayan dağıtımı desteklemesi gerekir. Bu nedenle, hazırlama Web sunucularını uzak aracı yerine Web Dağıtımı Işleyicisini kullanacak şekilde yapılandırmanız gerekir.
- Hazırlama ortamı birden çok Web sunucusu içerir, ancak tek tıklamayla veya otomatik dağıtımı desteklemesi gerekir, bu nedenle bir sunucu grubu oluşturmak için Web grubu çerçevesini (WFF) kullanmanız gerekir. Bu yaklaşımı kullanarak, bir uygulamayı bir Web sunucusuna (birincil sunucu) dağıtabilir ve WFF, hazırlama ortamındaki diğer tüm Web sunucularındaki dağıtımı çoğaltır.
- Dağıtımı gerçekleştiren kullanıcı veya işlem hesabı, veritabanı oluşturma izinlerine sahip olmalıdır. Bu nedenle, sunucu sunucusunu uzaktan erişim ve dağıtımı destekleyecek şekilde yapılandırmaya ek olarak, hesabı veritabanı sunucusundaki **dbcreator** sunucu rolüne eklemeniz gerekir.

Bu konular, bu görevleri gerçekleştirmek için ihtiyacınız olan tüm bilgileri sağlar:

- [Web grubu çerçevesiyle bir sunucu grubu oluşturun](creating-a-server-farm-with-the-web-farm-framework.md). Bu konu, Web platformu ürünlerinin ve bileşenlerinin, yapılandırma ayarlarının ve Web sitelerinin ve uygulamaların birden çok yük dengeli Web sunucusunda çoğaltılmasını sağlamak üzere WFF kullanarak bir sunucu grubu oluşturma ve yapılandırmayı açıklar.
- [Bir Web sunucusunu Web dağıtımı yayımlaması Için yapılandırın (Web dağıtımı işleyicisi)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md). Bu konuda, temiz bir Windows Server 2008 R2 derlemesinden başlayarak uzak Aracı yaklaşımını kullanarak Web Dağıtımı yayımlamayı destekleyen bir Web sunucusunun nasıl oluşturulacağı açıklanmaktadır.
- [Web dağıtımı yayımlaması için bir veritabanı sunucusu yapılandırın](configuring-a-database-server-for-web-deploy-publishing.md). Bu konuda, bir veritabanı sunucusunun varsayılan bir SQL Server 2008 R2 yüklemesinden başlayarak uzaktan erişim ve dağıtımı destekleyecek şekilde nasıl yapılandırılacağı açıklanmaktadır.

## <a name="further-reading"></a>Daha Fazla Bilgi

Tipik bir geliştirici test ortamını yapılandırma hakkında yönergeler için bkz. [Senaryo: Web dağıtımı Için test ortamı yapılandırma](scenario-configuring-a-test-environment-for-web-deployment.md). Tipik bir üretim ortamını yapılandırma hakkında yönergeler için bkz. [Senaryo: Web dağıtımı Için üretim ortamı yapılandırma](scenario-configuring-a-production-environment-for-web-deployment.md).

> [!div class="step-by-step"]
> [Önceki](scenario-configuring-a-test-environment-for-web-deployment.md)
> [İleri](scenario-configuring-a-production-environment-for-web-deployment.md)
