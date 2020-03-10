---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: Takım derleme dağıtımı için Izinleri yapılandırma | Microsoft Docs
author: jrjlee
description: Bu konuda, derleme sunucunuzun otomatik b 'nin bir parçası olarak Web sunucularına ve veritabanı sunucularına içerik dağıtmasını sağlamak için izinlerin nasıl yapılandırılacağı açıklanmaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5699f72af6b8d7f18d1a2c631dfdedd63c66e1e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638427"
---
# <a name="configuring-permissions-for-team-build-deployment"></a>Takım Derleme Dağıtımı İzinlerini Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, yapı sunucunuzun otomatik derleme sürecinin bir parçası olarak Web sunucularına ve veritabanı sunucularına içerik dağıtmasına olanak tanımak için izinlerin nasıl yapılandırılacağı açıklanmaktadır.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="task-overview"></a>Göreve genel bakış

Team Foundation Server (TFS) 2010 derleme hizmetini yüklediğinizde, hizmetin çalıştırmasını istediğiniz kimliği belirtirsiniz. Bu, varsayılan olarak ağ hizmeti hesabıdır. Alternatif olarak, yapı hizmetini bir etki alanı hesabı kullanarak çalışacak şekilde yapılandırabilirsiniz.

Windows kimlik doğrulaması gerektiren ve takım derlemesi kullanarak otomatikleştirmeyi planladığınız dağıtım görevleri, yapı hizmeti kimliği kullanılarak çalışır. Bu nedenle, web sunucularınızda ve veritabanı sunucularınızda yapı hizmeti kimliğine gerekli izinleri vermeniz gerekir.

> [!NOTE]
> Ağ hizmeti hesabı, diğer bilgisayarların kimliğini doğrulamak için makine hesabını kullanır. Makine hesapları * [etki alanı adı]\[makine adı] * **$** &#x2014;, örneğin, **FABRIKAM\TFSBUILD $** . Bu nedenle, yapı hizmetiniz ağ hizmeti kimliğini kullanarak çalıştırılıyorsa, yapı sunucunuz için makine hesap kimliği için gerekli tüm izinleri vermelisiniz.

## <a name="configuring-web-server-permissions"></a>Web sunucusu Izinlerini yapılandırma

[Web dağıtımına doğru yaklaşımı seçme](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)konusunda açıklandığı gibi, bir uzak Web sunucusuna Web paketleri dağıtmak istiyorsanız kullanabileceğiniz iki ana yaklaşım vardır:

- Hedef sunucuda *Web Deployment Agent hizmetini* (uzak aracı olarak da bilinir) hedefleyerek uygulamayı uzak bir konumdan dağıtın.
- Hedef sunucuda *Internet Information Services* (*IIS) Web dağıtımı işleyicisini* hedefleyerek uzak bir konumdan uygulamayı dağıtın.

Bu durumda uzak aracının iki anahtar sınırlaması vardır:

- Uzak aracı yalnızca NTLM kimlik doğrulamasını destekler. Diğer bir deyişle, dağıtımın derleme hizmeti kimliğini&#x2014;kullanması gerekir, başka bir hesabın kimliğine bürünemiyoruz.
- Uzak aracıyı kullanmak için, dağıtımı gerçekleştiren hesabın hedef sunucuda bir yönetici olması gerekir.

Birlikte, bu iki sınırlama, uzak aracının otomatikleştirilmiş bir ekip derleme dağıtımı için istenmeyen bir şekilde yaklaşımını yapar. Bu yaklaşımı kullanmak için, yapı hizmeti hesabını herhangi bir hedef Web sunucusunda yönetici yapmanız gerekir.

Buna karşılık Web Dağıtımı Işleyicisi yaklaşımı çeşitli avantajlar sunar:

- Web Dağıtımı Işleyici, HTTPS üzerinden temel kimlik doğrulamasını destekler ve bu sayede alternatif bir hesabın kimlik bilgilerini IIS Web Dağıtım aracına (Web Dağıtımı) geçirebilirsiniz.
- Yönetici olmayan kullanıcıların Web Dağıtımı Işleyicisini kullanarak belirli IIS Web sitelerine içerik dağıtmasını sağlamak için hedef Web sunucularını yapılandırabilirsiniz.

Sonuç olarak, takım derlemeden Web paketi dağıtımını otomatikleştirdiğiniz zaman Web Dağıtımı Işleyicisini hedeflemek açıkça tercih edilir. Önerilen işlem budur:

1. Dağıtım için kullanmak üzere düşük ayrıcalıklı bir etki alanı hesabı oluşturun.
2. Web Dağıtımı Işleyicisini yapılandırın ve hesaba, [bir Web sunucusunu Web dağıtımı yayımlama Için yapılandırma (Web dağıtımı işleyicisi)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)bölümünde açıklandığı gibi belırlı bir IIS Web sitesine içerik dağıtmak için gerekli izinleri verin.
3. Web Dağıtımı çağırın ve temel kimlik doğrulamasını kullanarak ve dağıtımı gerçekleştirmek için oluşturduğunuz etki alanı hesabının kimlik bilgilerini sağlayarak Web Dağıtımı Işleyicisini hedefleyin.

[Ilgili kişi Yöneticisi](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) örnek çözümünde, ortama özgü proje dosyasında kimlik doğrulama türünü (temel veya NTLM), Web dağıtımı kimlik bilgilerini ve uç nokta adresini (uzak aracı veya Web dağıtımı işleyicisi) belirtirsiniz. Bu değerler, proje dosyası yürütüldüğünde bir Web Dağıtımı komutunu formüle eklemek ve çalıştırmak için kullanılır. Daha fazla bilgi için bkz. [Web paketleri dağıtma](../web-deployment-in-the-enterprise/deploying-web-packages.md).

İzinleri yapılandırma dahil Web Dağıtımı Işleyicisini yapılandırma hakkında daha fazla bilgi için bkz. [bir Web sunucusunu Web dağıtımı yayımlaması Için yapılandırma (Web dağıtımı işleyicisi)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md). Uzak Aracıyı yapılandırma hakkında daha fazla bilgi için bkz. [bir Web sunucusunu Web dağıtımı yayımlama Için yapılandırma (uzak Aracı)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).

## <a name="configuring-database-server-permissions"></a>Veritabanı sunucusu Izinlerini yapılandırma

SQL Server bir veritabanı dağıtmak için şunları yapmanız gerekir:

- SQL Server örneğinde dağıtım hesabı için bir oturum açma oluşturun.
- SQL Server örneğinde oturum açma **dbcreator** izinlerini verin.
- İlk dağıtımdan sonra, hedef veritabanındaki **db\_Owner** rolüne oturum açmayı ekleyin. Bu, sonraki dağıtımlarda, yeni bir veritabanı oluşturmak yerine var olan bir veritabanını değiştirmekte olduğunuz için gereklidir.

NTLM kimlik doğrulaması ya da SQL Server kimlik doğrulaması kullanarak bir SQL Server örneğine kimlik doğrulaması yapabilirsiniz:

- NTLM kimlik doğrulaması kullanıyorsanız yukarıda açıklanan izinleri derleme hizmeti hesabına vermeniz gerekir.
- SQL Server kimlik doğrulaması kullanıyorsanız yukarıda açıklanan izinleri SQL Server hesabına vermeniz gerekir. Ayrıca, veritabanını dağıtmak için kullandığınız bağlantı dizesinde Kullanıcı adı ve parola SQL Server dahil etmeniz gerekir.

Veritabanı dağıtımı için izinleri yapılandırma hakkında adım adım ayrıntılar için bkz. [Web dağıtımı yayımlama Için veritabanı sunucusunu yapılandırma](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).

## <a name="conclusion"></a>Sonuç

Bu noktada, takım derlemeden Web uygulaması ve veritabanı dağıtımlarını otomatikleştirdiğiniz zaman kimlik doğrulama seçenekleriyle birlikte, gerekli izinleri anlamalısınız. Ayrıca, IIS Web sunucularında ve SQL Server veritabanı sunucularında gerekli izinleri de uygulayabilmelisiniz.

## <a name="further-reading"></a>Daha Fazla Bilgi

Windows Server ortamlarını uzaktan dağıtımı destekleyecek şekilde yapılandırma hakkında daha fazla bilgi için bkz. [Web dağıtımı Için sunucu ortamlarını yapılandırma](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).

> [!div class="step-by-step"]
> [Öncekini](deploying-a-specific-build.md)
