---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager çözümü | Microsoft Docs
author: jrjlee
description: Bu öğreticide, gerçekçi bir uygulama olan&#x2014;kurumsal ölçekte bir uygulamayı&#x2014;temsil etmek üzere Contact Manager çözümü örnek bir çözümü kullanılmaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586270"
---
# <a name="the-contact-manager-solution"></a>Kişi Yöneticisi Çözümü

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu [öğretici serisi](web-deployment-in-the-enterprise.md) , gerçek bir karmaşıklık düzeyi&#x2014;olan kurumsal ölçekte bir&#x2014;uygulamayı temsil etmek üzere ilgili kişi Yöneticisi çözümünü örnek bir çözüm kullanır. Bu konuda, Contact Manager çözümü tanıtılmakta, çözümün temel bileşenleri açıklanmakta ve bu tür bir uygulamayı bir kurumsal ortamdaki çeşitli hedef platformlara dağıtmanın güçlükleri tanımlanmaktadır.
> 
> Bu öğreticilerdeki konularda çalışırken, kurumsal dağıtım senaryolarında belirli zorlukları nasıl karşılabileceğinizi gösteren bir başvuru uygulama olarak Contact Manager çözümünü kullanabilirsiniz. Bir sonraki konu, [Contact Manager çözümünü ayarlama](setting-up-the-contact-manager-solution.md), çözümün geliştirici iş istasyonunda nasıl indirileceği ve çalıştırılacağı açıklanmaktadır.

## <a name="solution-overview"></a>Çözüme genel bakış

Ilgili kişi Yöneticisi çözümü, dört ayrı projeden oluşur:

![](the-contact-manager-solution/_static/image1.png)

- **ContactManager. Mvc**. Bu, çözüm için giriş noktasını temsil eden bir ASP.NET MVC 3 Web uygulaması projem. Kullanıcılara kişi ayrıntıları oluşturma ve görüntüleme yeteneği sağlama gibi bazı temel Web uygulaması işlevleri sunar. Uygulama, kimlik doğrulama ve yetkilendirmeyi yönetmek üzere kişileri ve ASP.NET uygulama Hizmetleri veritabanını yönetmek için bir Windows Communication Foundation (WCF) hizmetini kullanır.
- **ContactManager. Database**. Bu bir Visual Studio veritabanı projem. Proje, iletişim ayrıntılarını depolayan bir veritabanının şemasını tanımlar.
- **ContactManager. Service**. Bu bir WCF Web hizmeti projem. WCF hizmeti, çağıranların **ContactManager** veritabanında oluşturma, alma, güncelleştirme ve SILME (CRUD) işlemlerini gerçekleştirmesine olanak tanıyan bir uç nokta sunar. Hizmet, **ContactManager** veritabanını ve **ContactManager. Common. dll** derlemesini kullanır.
- **ContactManager. Common**. Bu bir sınıf kitaplığı projem. WCF hizmeti bu derlemede tanımlanan türleri kullanır.

Çözüm, Yayımla adlı bir çözüm klasörünü de içerir. Bu, derleme ve dağıtım sürecini nasıl denetleyebileceğinizi ve işleyebileceğinizi gösteren çeşitli özel proje dosyalarını ve komut dosyalarını içerir. Bunlar, Bu öğreticinin ilerleyen kısımlarında daha ayrıntılı bir şekilde ele alınmıştır.

Kavramsal düzeyde, çözümün bileşenleri şu şekilde bir araya sığacak:

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> ASP.NET MVC 3 Web uygulaması ASP.NET üyelik sağlayıcısını kullandığında, Web uygulaması içindeki tüm sayfalar anonim erişime izin verir. Bu, gerçekçi bir yapılandırma değildir. Ancak çözüm, Kullanıcı hesaplarını ve rolleri yapılandırmadan çözümü dağıtmanızı ve test etmeniz için bu şekilde ayarlanır.

## <a name="deployment-challenges"></a>Dağıtım zorlukları

Ilgili kişi Yöneticisi çözümü, birçok kurumsal dağıtım senaryosunda ortak olan çeşitli dağıtım güçlükleri gösterir:

- Çözüm birden çok bağımlı projeden oluşur. Bu projeleri eşzamanlı olarak dağıtmanız gerekir.
- Bağlantı dizeleri ve hizmet uç noktalarının her ortam için güncelleştirilmeleri gerekir ve çok sayıda durumda bu bilgiler geliştirici tarafından kullanılamaz.
- **ContactManager** veritabanını hazırlama ve üretim ortamlarına dağıtırken, sonraki dağıtımlarda mevcut verileri korumanız gerekir.
- ASP.NET uygulama Hizmetleri veritabanını dağıttığınızda, bazı yapılandırma verilerini dağıtmanız gerekir, ancak herhangi bir kullanıcı hesabı verisini atlayabilirsiniz.
- Projeler, dağıtılmayacak bazı dosya ve klasörleri içerir. Dağıtım işleminden bu dosya ve klasörleri hariç bırakmanız gerekir.
- Çözümün, bir Team Foundation Server (TFS) yapı sunucusundan otomatik dağıtımı desteklemesi gerekir.

## <a name="conclusion"></a>Sonuç

Bu konu, Contact Manager çözümüne üst düzey bir genel bakış sağladı ve birçok kurumsal dağıtım senaryosunda yaygın olarak karşılaşılan bazı dağıtım güçlüklerinden bazılarını tanımladı. Bu öğreticideki geri kalan konularda, bu zorlukları karşılamak için kullanabileceğiniz tekniklerin bazıları açıklanır.

Bir sonraki konu, [Contact Manager çözümünü ayarlama](setting-up-the-contact-manager-solution.md), çözümün geliştirici iş istasyonunda nasıl indirileceği ve çalıştırılacağı açıklanmaktadır.

> [!div class="step-by-step"]
> [Önceki](web-deployment-in-the-enterprise.md)
> [İleri](setting-up-the-contact-manager-solution.md)
