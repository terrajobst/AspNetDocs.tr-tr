---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: 'Kurumsal Web dağıtımı: senaryoya genel bakış | Microsoft Docs'
author: jrjlee
description: Bu öğretici kümesi, bir başvuru sağlamak için kurgusal bir kurumsal dağıtım senaryosu ile birlikte gerçekçi karmaşıklık düzeyine sahip örnek bir çözüm kullanır...
ms.author: riande
ms.date: 05/03/2012
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: 9786879844da13c21e6a953b1ab24b29ca8121e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574132"
---
# <a name="enterprise-web-deployment-scenario-overview"></a>Kurumsal Web Dağıtımı: Senaryoya Genel Bakış

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu öğretici kümesi, bir başvuru uygulama sağlamak ve görevlere izin vermek ve ortak bir bağlam için izlenecek yollar sağlamak üzere kurgusal bir işletme dağıtım senaryosu ile birlikte gerçekçi karmaşıklık düzeyine sahip örnek bir çözüm kullanır. Bu konuda öğretici senaryosu açıklanmakta ve örnek çözüm tanıtılmaktadır.

## <a name="scenario-description"></a>Senaryo açıklaması

Kurgusal bir şirket olan Fabrikam, Inc., uzak satış ekiplerinin bir web arabiriminden iletişim bilgilerini depolamasına ve almasına imkan tanıyan bir çözüm oluşturuyor.

Fabrikam, Inc. konumundaki uygulama yaşam döngüsü yönetimi (ALM) işlemleri, çözümün yazılım geliştirme sürecinin çeşitli aşamalarında üç sunucu ortamına dağıtılmasını gerektirir:

- Geliştirici testi veya "Sandbox" ortamı.
- İntranet tabanlı bir hazırlama ortamıdır.
- Internet 'e yönelik bir üretim ortamı.

Bu ortamların her biri farklı yapılandırma ve güvenlik gereksinimlerine sahiptir ve her biri benzersiz dağıtım zorlukları doğurur.

### <a name="the-fabrikam-inc-server-infrastructure"></a>Fabrikam, Inc. Server altyapısı

Bu, Fabrikam, Inc. ' deki üst düzey geliştirme ve dağıtım altyapısıdır.

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

Geliştirici iş istasyonları, kaynak denetim altyapısı, geliştirici test ortamı ve hazırlama ortamı, Fabrikam.net etki alanındaki intranet ağında bulunur. Üretim ortamı, bir güvenlik duvarı tarafından intranet ağından yalıtılmış bir çevre ağında (DMZ, sivil bölge ve denetimli alt ağ olarak da bilinir) bulunur. Bu, yaygın bir dağıtım senaryosudur: Internet 'e yönelik Web sunucularınızı güvenlik duvarları veya Ağ Geçidi sunucularının kullanımı aracılığıyla iç sunucu altyapınızdan yalıtabilirsiniz.

Bu örnekte:

- Ayrı derleme sunucusuna sahip bir Team Foundation Server (TFS) 2010 sunucusu, kaynak denetimi ve sürekli tümleştirme (CI) işlevselliği sağlar.
- Geliştirici sınama ortamı bir Internet Information Services (IIS) 7,5 Web sunucusu ve SQL Server 2008 R2 veritabanı sunucusu içerir.
- Üretim ortamı, bir Web grubu çerçevesi (WFF) denetleyici sunucusu tarafından eşitlenen birden çok IIS 7,5 Web sunucusunu SQL Server 2008 R2 veritabanı sunucusuyla birlikte içerir. Uygulamada veritabanı sunucusu, ölçeklenebilirliği ve kullanılabilirliği geliştirmek için kümeleme veya yansıtma kullanabilir.
- Hazırlama ortamı, üretim ortamının yapılandırmasını mümkün olduğunca yakından çoğaltmak için tasarlanmıştır.
- Güvenlik Duvarı ve ağ yalıtımı ilkeleri, intranetten çevre ağına doğrudan, Otomatik dağıtıma izin vermez.

Bu ortamların her birinin yapılandırması, ikinci öğreticide, [Web dağıtımı Için sunucu ortamlarını yapılandırma](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)konusunda daha ayrıntılı olarak açıklanmıştır.

### <a name="team-roles-for-alm"></a>ALM için takım rolleri

Bu kullanıcılar, Contact Manager çözümünü oluşturma, yönetme, derleme ve yayımlama ile ilgilidir:

- Matt hink, Fabrikam, Inc 'deki bir Web uygulaması geliştiricisiyseniz. Visual Studio 2010 kullanarak Contact Manager çözümünü geliştiren ekibin bir parçasıdır. Matt, geliştirici sınama ortamındaki sunucular üzerinde tam yönetici haklarına sahiptir ve bu sayede ortamı ihtiyaçlarını karşılayacak şekilde yapılandırabilir. Ayrıca, Contact Manager çözümü için kaynak kodu depoladığı Visual Studio 2010 TFS örneğine Kullanıcı erişimi de vardır.
- Ramiz Walters, Fabrikam, Inc. geliştirme ekibi için bir sunucu yöneticisidir. Ramiz TFS sunucusunda yönetim erişimine sahiptir, böylece TFS ve takım derlemesinin tüm yönlerini yapılandırabilirler. Ramiz Ayrıca test ve hazırlama Web sunucularına yönetim erişimine sahiptir ve test ve hazırlama ortamlarındaki veritabanı sunucuları için veritabanı Yöneticisi (DBA) görevi görür. Ramiz, TFS sunucusunda bu görevleri gerçekleştirmek için takım derlemesini yapılandırdı:

    - Bir Kullanıcı TFS 'ye bir dosyayı her denetlediğinde uygulama üzerinde birim testleri oluşturun ve çalıştırın. Bu, CI olarak adlandırılır.
    - Uygulama birim testlerini geçtiğinde, Contact Manager uygulamasını test ortamına otomatik olarak dağıtın. Bu, veritabanını ilk dağıtımda test sunucularına ve ilk dağıtımdan sonra veritabanında yapılan tüm güncelleştirmelere yayımlamayı içerir.
    - Tek adımlı bir işlemde, Contact Manager uygulamasını hazırlama ortamına dağıtın.
    - Bir Web sunucusu yöneticisinin ve bir DBA 'nın uygulamayı üretim ortamında yayımlayabilmesi için kullanabileceği bir Web paketi oluşturun.
- Lisa Andrews, Fabrikam, Inc. üretim sunucularına uygulama dağıtmaktan sorumlu bir sunucu yöneticisidir. TFS ekibi derlemesinin, Web dağıtım paketini, Contact Manager uygulamasını yapılandırdıktan sonra depoladığı paylaşıma okuma erişimi vardır. Ayrıca, uygulamayı üretime dağıtabilmesi için üretim Web sunucularına yönetim erişimi de vardır. Ayrıca, üretim ortamındaki veritabanı sunucusuna veritabanları ve veritabanı güncelleştirmeleri dağıtan DBA gibi davranır.

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a>Kişi Yöneticisi Çözümü

Contact Manager çözümü, kayıtlı, oturum açmış kullanıcıların bir Web arabirimi aracılığıyla kişi bilgilerini eklemesini ve düzenlemesini sağlamak üzere tasarlanmıştır. Ilgili kişi Yöneticisi çözümü, dört ayrı projeden oluşur:

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- **ContactManager. Mvc**. Bu, çözüm için giriş noktasını temsil eden bir ASP.NET MVC3 Web uygulaması projem. Kullanıcılara kişi ayrıntıları oluşturma ve görüntüleme yeteneği sağlama gibi bazı temel Web uygulaması işlevleri sunar. Uygulama, kimlik doğrulama ve yetkilendirmeyi yönetmek üzere kişileri ve ASP.NET uygulama Hizmetleri veritabanını yönetmek için bir Windows Communication Foundation (WCF) hizmetini kullanır.
- **ContactManager. Database**. Bu bir Visual Studio 2010 veritabanı projem. Proje, iletişim ayrıntılarını depolayan bir veritabanının şemasını tanımlar.
- **ContactManager. Service**. Bu bir WCF Web hizmeti projem. WCF, çağıranların Contact Manager veritabanında oluşturma, alma, güncelleştirme ve silme (CRUD) işlemlerini gerçekleştirmesine olanak tanıyan bir uç nokta gösterir. Hizmet, Contact Manager veritabanını ve ContactManager. Common. dll derlemesini kullanır.
- **ContactManager. Common**. Bu bir sınıf kitaplığı projem. WCF hizmeti bu derlemede tanımlanan türleri kullanır.

Bu serideki ilk öğreticide, [kuruluştaki Web dağıtımıyla](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)birlikte çözümün ve dağıtım gereksinimlerinin tamamen incelenmesi sağlanır.

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a>Dağıtım görevleri

Büyük bir kuruluştaki farklı ortamlara uygulama dağıtmaya yönelik çeşitli farklı görevler vardır. Bunlar, öğreticilerin kapsaması gereken önemli görevlerdir:

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

Bu belgede daha önce açıklanan kullanıcıların perspektifinden dağıtım işlemindeki her adımın bir listesi aşağıda verilmiştir:

1. Ekibin tüm üyeleri, temel dağıtım gereksinimlerini ve sorunlarını öğrenmek için Visual Studio 2010 ' deki Contact Manager çözümünü gözden geçirir.
2. Matt hink, dağıtım mantığının bir başlangıç testini yapmak için doğrudan geliştirici iş istasyonundan geliştirici sınama ortamına kişi Yöneticisi çözümünü dağıtabilir.
3. Matt hink, uygulamayı TFS 'deki kaynak denetimine ekler.
4. Ramiz Walters, ekip derlemesinde Ilgili Contact Manager çözümü için çeşitli derleme tanımları oluşturur. Bir derleme tanımı, bir Kullanıcı yeni kodu her denetlediğinde çözümü geliştirici sınama ortamına dağıtmak için CI kullanır. Başka bir derleme tanımı, kullanıcıların hazırlama ortamına gereken dağıtımları gerektiği şekilde tetiklemesine olanak tanır.
5. Kullanıcı yeni kodu her denetlediğinde, takım derlemesi çözüm bileşenlerini otomatik olarak oluşturur, birim testlerini çalıştırır ve yapı başarılı olduysa ve birim testleri başarılı olursa çözümü geliştirici sınama ortamına dağıtır.
6. Bir Kullanıcı hazırlama ortamına bir dağıtımı tetiklerse, çözüm paketlenir ve tek adımlı bir işlemde dağıtılır. Bu işlem, üretim ortamına el ile dağıtım için de bir paket oluşturur.
7. Lisa Andrews, 6. adımda oluşturulan Web paketini el ile içe aktararak uygulamayı üretim ortamına dağıtır.

### <a name="key-deployment-issues"></a>Anahtar dağıtım sorunları

Contact Manager çözümü ve Fabrikam, Inc. senaryosunda, karmaşık, kurumsal ölçekte çözümler dağıtırken karşılaşabileceğiniz çeşitli yaygın sorunlar ve güçlükler vurgulanmıştır. Örneğin:

- Geliştirici veya test ortamları, hazırlama platformları ve üretim sunucuları gibi birden çok ortama proje dağıtabilmeniz gerekir. Çözümün her ortam için farklı yapılandırma ayarlarıyla dağıtılması gerekir.
- Tek adımlı veya otomatik derleme ve dağıtım sürecinin bir parçası olarak birden fazla bağımlı projeyi aynı anda dağıtmanız gerekir.
- Otomatik bir işlemden dağıtım sürücünüzü sağlayabilmeniz gerekir. Örneğin, yeni kod iade edildiğinde bir hazırlama ortamına Web uygulamaları dağıtmak için bir CI işlemi kullanmak istersiniz.
- Geliştiricilerin, doğru yapılandırma ayarlarına veya her hedef ortam için gerekli kimlik bilgilerine sahip olması olası olduğundan, dağıtım işlemini denetleyebilmeniz ve dağıtım değişkenlerini Visual Studio 'Nun dışında ayarlamanız gerekir.
- Şema tabanlı veritabanı projelerini dağıtmanız ve sonraki dağıtımlarda mevcut verileri korumanız gerekir.
- Kullanıcı hesabı verilerini dağıtmadan, üyelik veritabanlarını bir geçici temele göre dağıtmanız gerekir. Ayrıca, mevcut kullanıcı hesabı verilerini kaybetmeden dağıtılan üyelik veritabanlarının şemasını güncelleştirmeniz gerekebilir.
- Çeşitli hedef ortamlara içerik dağıtırken belirli dosya veya klasörleri hariç bırakmanız gerekir.

Bunlara ek olarak, güncelleştirmeler sık sık olduğunda dağıtımı yönetme ve artımlı bazı ek sorunlar oluşturur. Örneğin:

- Bir geliştirici yeni kodu her denetlediğinde birim testlerini çalıştırırsınız. Çözümü yalnızca kod birim testlerini geçirirse dağıtmak istersiniz.
- Bir Web uygulamasını bir hazırlık veya üretim ortamına dağıtırken, dağıtım işlemi süresince kullanıcıları *çevrimdışı. htm\_bir uygulamaya* yönlendirmek istersiniz.
- Dağıtım etkinliklerini günlüğe kaydetmek istiyorsunuz. Dağıtım işlemi, belirlenen alıcılara başarılı veya başarısız dağıtımlara yönelik e-posta bildirimleri göndermelidir.
- Otomatik bir dağıtım başarısız olursa, dağıtım işlemi geçerli dağıtımı yeniden dener veya bunun yerine önceki Web paketini dağıtmalıdır.

> [!div class="step-by-step"]
> [Önceki](deploying-web-applications-in-enterprise-scenarios.md)
> [İleri](application-lifecycle-management-from-development-to-production.md)
