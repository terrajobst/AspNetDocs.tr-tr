---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: 'Senaryo: Web dağıtımı için üretim ortamını yapılandırma | Microsoft Docs'
author: jrjlee
description: Bu konuda, bir üretim ortamı için tipik bir Web Dağıtım senaryosu açıklanmakta ve benzer bir şekilde ayarlamak için gerçekleştirmeniz gereken görevler açıklanmaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2d76e715cdbf6ec484fa0ff98b3b3d1d8dfd3961
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635424"
---
# <a name="scenario-configuring-a-production-environment-for-web-deployment"></a>Senaryo: Web Dağıtımı için Üretim Ortamı Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, bir üretim ortamı için tipik bir Web Dağıtım senaryosu açıklanmakta ve benzer bir ortam kurmak için gerçekleştirmeniz gereken görevler açıklanmaktadır.

Üretim ortamı, bir Web uygulaması veya bir Web sitesi için son hedefdir. Bu noktada, uygulamanız test aracılığıyla yapılır, bir hazırlama ortamına dağıtıldı ve "canlı çalış" a hazırlanıyor. Bir üretim ortamının özellikleri, Web içeriğinizin doğası ve amacına, kuruluşunuzun boyutuna, hedef hedef kitlenize ve birçok başka etkene göre farklılık gösterebilir. Kurumsal ölçekli bir senaryoda, üretim ortamı şu özelliklere sahip olabilir:

- Ortam, genellikle Yük Devretme Kümelemesi ve veritabanı yansıtma ile birlikte birden fazla yük dengeli Web sunucusundan ve bir veya daha fazla veritabanı sunucusundan oluşur.
- Ortam Internet 'e sunulduğundan, iç ağınızdan ayrılmış olması olasıdır. Bu, bir çevre ağındaki farklı bir alt ağda olabilir, farklı bir etki alanında olabilir ve tamamen farklı bir ağ altyapısında olabilir.
- Geliştiriciler ve derleme sunucusu işlem hesaplarının üretim sunucularında yönetici ayrıcalıklarına sahip olma olasılığı yüksektir.
- Uygulamalardaki değişiklikler test veya hazırlama dağıtımlarından daha az sıklıkta dağıtılır.

> [!NOTE]
> Bir veritabanı dağıtımının birden çok sunucu arasında ölçeklendirilmesi, Bu öğreticinin kapsamı dışındadır. Bu alan hakkında daha fazla bilgi için lütfen [çevrimiçi SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx)'a başvurun.

Örneğin, [öğretici senaryolarımızda](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), bir ekip derleme sunucusu, kullanıcıların Contact Manager çözümünü oluşturmasına ve tek bir adımda hazırlama ortamına dağıtmasına izin veren derleme tanımları içerir. Uygulama üretime dağıtılmaya hazırsa, güvenlik gereksinimleri ve ağ altyapısı tarafından uygulanan kısıtlamalar nedeniyle, üretim ortamı yöneticisinin Web paketini bir üretim Web sunucusuna el ile kopyalaması ve içeri aktarması gerekir Internet Information Services (IIS) Yöneticisi üzerinden.

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a>Çözüme genel bakış

Bu senaryoda, dağıtım gereksinimlerinin bir analizinden bu olguları getirebilirsiniz:

- Güvenlik kısıtlamaları ve ağ yapılandırması nedeniyle, üretim ortamını tek tıklamaları veya otomatik dağıtımı destekleyecek şekilde yapılandıramazsınız. Çevrimdışı dağıtım, bu senaryoda yalnızca önemli yaklaşımdır.
- Üretim ortamı birden çok Web sunucusu içerir, bu nedenle bir sunucu grubu oluşturmak için Web grubu çerçevesini (WFF) kullanabilirsiniz. Bu yaklaşımı kullanarak, yöneticinin uygulamayı yalnızca bir Web sunucusuna (birincil sunucu) aktarması gerekir ve WFF, dağıtımı üretim ortamındaki diğer tüm Web sunucularında çoğaltacaktır.

Bu konular, bu görevleri gerçekleştirmek için ihtiyacınız olan tüm bilgileri sağlar:

- [Web grubu çerçevesiyle bir sunucu grubu oluşturun](configuring-a-database-server-for-web-deploy-publishing.md). Bu konu, Web platformu ürünlerinin ve bileşenlerinin, yapılandırma ayarlarının ve Web sitelerinin ve uygulamaların birden çok yük dengeli Web sunucusunda çoğaltılmasını sağlamak üzere WFF kullanarak bir sunucu grubu oluşturma ve yapılandırmayı açıklar.
- [Bir Web sunucusunu Web dağıtımı yayımlaması (çevrimdışı dağıtım) Için yapılandırın](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md). Bu konuda, temiz bir Windows Server 2008 R2 derlemesinden başlayarak yöneticilerin web paketlerini el ile içeri aktarıp dağıtmalarına olanak tanıyan bir Web sunucusu oluşturma işlemi açıklanmaktadır.
- [Web dağıtımı yayımlaması için bir veritabanı sunucusu yapılandırın](configuring-a-database-server-for-web-deploy-publishing.md). Bu konuda, bir veritabanı sunucusunun varsayılan bir SQL Server 2008 R2 yüklemesinden başlayarak uzaktan erişim ve dağıtımı destekleyecek şekilde nasıl yapılandırılacağı açıklanmaktadır.

## <a name="further-reading"></a>Daha Fazla Bilgi

Tipik bir geliştirici test ortamını yapılandırma hakkında yönergeler için bkz. [Senaryo: Web dağıtımı Için test ortamı yapılandırma](scenario-configuring-a-test-environment-for-web-deployment.md). Tipik bir hazırlama ortamını yapılandırma hakkında yönergeler için bkz. [Senaryo: Web dağıtımı Için hazırlama ortamı yapılandırma](scenario-configuring-a-staging-environment-for-web-deployment.md).

> [!div class="step-by-step"]
> [Önceki](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [İleri](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
