---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: Kurumsal ortamlara üyelik veritabanları dağıtma | Microsoft Docs
author: jrjlee
description: Bu konuda, ASP.NET uygulama hizmetleri veritabanları sağladığınızda (daha yaygın...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: 50f49af502b75aa5ad52756a76a5e7340aca53f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526007"
---
# <a name="deploying-membership-databases-to-enterprise-environments"></a>Kurumsal Ortamlara Üyelik Veritabanları Dağıtma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, test, hazırlama veya üretim ortamlarında ASP.NET uygulama hizmetleri veritabanları (üyelik veritabanları olarak da bilinir) sağladığınızda aşmaya ihtiyacınız olan önemli noktalar ve güçlükler açıklanmaktadır. Ayrıca, bu zorlukları karşılamak için kullanabileceğiniz yaklaşımları açıklar.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>Üyelik veritabanını dağıtırken sorunlar nelerdir?

Çoğu durumda, bir veritabanı için bir dağıtım stratejisi devetiniz varsa, dikkate almanız gereken ilk şey, hangi verileri dağıtmaktır. Geliştirme veya test ortamında, hızlı ve kolay testi kolaylaştırmak için Kullanıcı hesabı verilerini dağıtmak isteyebilirsiniz. Hazırlama veya üretim ortamında, Kullanıcı hesabı verilerini dağıtmak istemeniz çok düşüktür.

Ne yazık ki ASP.NET üyelik veritabanları, bu kararı çok daha karmaşık hale getirmek için bazı özel güçlükleri ortaya çıkarabilir:

- Yalnızca şemadan oluşan bir dağıtım, üyelik veritabanını işlemsel olmayan bir durumda bırakır. Bunun nedeni, üyelik veritabanının, veritabanının çalışması için ihtiyaç duyduğu bazı yapılandırma verilerini ( **aspnet\_SchemaVersions** tablosunda) içermesidir. Bu nedenle, Kullanıcı hesabı verilerini dışlamak üzere üyelik veritabanınızın yalnızca şema dağıtımını gerçekleştirirseniz, temel yapılandırma verilerini eklemek için bir dağıtım sonrası betiği çalıştırmanız gerekir.
- Üyelik veritabanınızın nasıl yapılandırıldığına bağlı olarak, üyelik sağlayıcısı, parolaları şifrelemek ve veritabanında depolamak için makine anahtarını kullanabilir. Bu durumda, veritabanıyla dağıttığınız tüm Kullanıcı hesabı verileri hedef sunucuda kullanılamaz hale gelir. Bu nedenle, Kullanıcı hesabı verilerinin dağıtımı desteklenen bir senaryo değildir.

## <a name="choosing-a-membership-database-strategy"></a>Üyelik veritabanı stratejisi seçme

Bir kurumsal sunucu ortamında üyelik veritabanının nasıl sağlanacağını seçerken bu yönergeleri kullanın:

- Mümkün olan yerlerde, üyelik veritabanlarını dağıtmayın. Bunun yerine, hedef veritabanı sunucusunda üyelik veritabanını el ile oluşturun. Üyelik veritabanı şemanızı özelleştirmediyseniz, [ASP.NET SQL Server kayıt aracı 'nı (aspnet\_regsql. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)kullanarak hedefte SITU 'da yeni bir tane oluşturmanız yeterlidir.
- Bir üyelik veritabanını dağıtmak istiyorsanız, ancak bir üyelik veritabanı&#x2014;dağıtmak istiyorsanız, veritabanı şemasında&#x2014;kapsamlı değişiklikler yaptıysanız, Kullanıcı hesabı verilerini hariç tutmak için üyelik veritabanının yalnızca şema bir dağıtımını gerçekleştirmeniz, sonra gerekli yapılandırma verilerini eklemek için dağıtım sonrası bir betik çalıştırmanız gerekir. [Nasıl yapılır: ASP.NET üyelik veritabanını Kullanıcı hesapları dahil etmeden dağıtma](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)konusunda şu yaklaşımlar hakkında geniş kapsamlı yönergeler bulabilirsiniz.

*Üyelik veritabanınızın şemasının büyük olasılıkla oldukça statik*olduğunu unutmamak önemlidir. Üyelik veritabanını özelleştirmiş olsanız bile, şemayı düzenli&#x2014;olarak güncelleştirmeniz gerekecektir. Bu, bir Web uygulamasındaki kodla veya bir veritabanı projesinde aynı sıklıkta değiştirilmeyeceğidir. Bu nedenle, herhangi bir otomatik veya tek adımlı dağıtım işlemlerine üyelik veritabanını eklemeniz gerekmez.

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>VSDBCMD kullanarak bir üyelik veritabanı şemasını güncelleştirme

İlk dağıtımdan sonra üyelik veritabanınızın yapısını değiştirirseniz, veritabanını yeniden dağıtmak için Internet Information Services (IIS) Web Dağıtım aracı 'nı (Web Dağıtımı) kullanmak istemeyebilirsiniz. Web Dağıtımı ' deki veritabanı dağıtım işlevleri, bir hedef veritabanına&#x2014;değişiklik güncellemeleri yapma özelliğini içermez, bu da veritabanını bırakıp yeniden oluşturmanız gerekir Web dağıtımı. Bu, genellikle hazırlama veya üretim ortamlarında istenmeyen olan mevcut kullanıcı hesabı verilerinin kaybedilmediği anlamına gelir.

Alternatif, VSDBCMD yardımcı programını kullanarak hedef veritabanınızın şemasını güncelleştirebilir. VSDBCMD iki önemli özelliği içerir. İlk olarak, var olan bir veritabanının şemasını bir. dbschema dosyasına aktarabilir. İkinci olarak, bir. dbschema dosyasını varolan bir veritabanına fark güncelleştirmesi olarak dağıtabilir, bu da yalnızca hedef veritabanını güncel hale getirmek için gerekli değişiklikleri yaptığı ve herhangi bir veri kaybetmemeniz anlamına gelir.

Bu üst düzey adımları, bir üyelik veritabanı şemasını güncelleştirmek için kullanabilirsiniz:

1. Kaynak üyelik veritabanınız için bir. dbschema dosyası oluşturmak üzere VSDBCMD **Import** eylemini kullanın. Bu yordam, [komut Isteminden nasıl yapılır: bir şemayı Içeri aktarma](https://msdn.microsoft.com/library/dd172135.aspx)konusunda açıklanmaktadır.
2. . Dbschema dosyasını hedef üyelik veritabanınıza dağıtmak için VSDBCMD **Deploy** eylemini kullanın. Bu yordam, [VSDBCMD Için komut satırı başvurusunda açıklanmıştır. EXE (dağıtım ve şema Içeri aktarma)](https://msdn.microsoft.com/library/dd193283.aspx).

## <a name="conclusion"></a>Sonuç

Bu konuda, çeşitli hedef ortamlarda ASP.NET üyelik veritabanları sağlamanız gerektiğinde karşılaşabileceğiniz bazı sorunlar açıklanmaktadır. Özellikle, yalnızca şema dağıtımlarının üyelik veritabanını işlemsel olmayan bir durumda bırakacağı ve Kullanıcı hesabı verilerinin dağıtılmasının neden desteklenmediği açıklanmıştı. Bu konu başlığı altında, üyelik veritabanlarının farklı senaryolarda nasıl sağlanması, dağıtılması ve güncelleştirilmesi konusunda yönergeler de sunulmuştur.

## <a name="further-reading"></a>Daha Fazla Bilgi

VSDBCMD kullanma hakkında daha fazla bilgi ve örnek için bkz [. VSDBCMD Için komut satırı başvurusu. EXE (dağıtım ve şema Içeri aktarma)](https://msdn.microsoft.com/library/dd193283.aspx) ve [nasıl yapılır: bir şemayı komut Isteminden içeri aktarma](https://msdn.microsoft.com/library/dd172135.aspx). ASPNET\_regsql. exe ' yi kullanarak üyelik veritabanları oluşturma hakkında daha fazla bilgi için bkz. [ASP.NET SQL Server kayıt aracı (aspnet\_regsql. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx). Üyelik veritabanlarının dağıtımı hakkında daha fazla genel bilgi için, bkz. [nasıl yapılır: ASP.NET üyelik veritabanını Kullanıcı hesapları dahil etmeden dağıtma](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx).

> [!div class="step-by-step"]
> [Önceki](deploying-database-role-memberships-to-test-environments.md)
> [İleri](excluding-files-and-folders-from-deployment.md)
