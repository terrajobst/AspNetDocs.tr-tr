---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: Test ortamlarına veritabanı rolü üyelikleri dağıtma | Microsoft Docs
author: jrjlee
description: Bu konu, bir test ortamına çözüm dağıtımının bir parçası olarak veritabanı rollerine Kullanıcı hesaplarının nasıl ekleneceğini açıklar. İçeren bir çözümü dağıttığınızda...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587593"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a>Test Ortamlarına Veritabanı Rol Üyelikleri Dağıtma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, bir test ortamına çözüm dağıtımının bir parçası olarak veritabanı rollerine Kullanıcı hesaplarının nasıl ekleneceğini açıklar.
> 
> Hazırlama veya üretim ortamına veritabanı projesi içeren bir çözüm dağıttığınızda, genellikle geliştiricinin Kullanıcı hesaplarının veritabanı rollerine eklenmesini otomatikleştirmesini istemezsiniz. Çoğu durumda, geliştirici hangi kullanıcı hesaplarının hangi veritabanı rollerine eklenmesi gerektiğini bilmez ve bu gereksinimler herhangi bir zamanda değişebilir. Ancak, bir geliştirme veya test ortamına veritabanı projesi içeren bir çözüm dağıttığınızda, durum genellikle farklı olur:
> 
> - Geliştirici genellikle bir günde birkaç kez çözümü düzenli aralıklarla yeniden dağıtır.
> - Veritabanı genellikle her dağıtımda yeniden oluşturulur. Bu, veritabanı kullanıcılarının oluşturulması ve her dağıtımdan sonra rollere eklenmesi gerektiği anlamına gelir.
> - Geliştirici genellikle hedef geliştirme veya test ortamı üzerinde tam denetime sahiptir.
> 
> Bu senaryoda, otomatik olarak veritabanı kullanıcıları oluşturmak ve dağıtım işleminin bir parçası olarak veritabanı rolü üyelikleri atamak yararlı olur.
> 
> Anahtar faktörü, bu işlemin hedef ortama göre koşullu olması gerekir. Hazırlama veya üretim ortamına dağıtım yapıyorsanız, işlemi atlamak istiyorsunuz. Bir geliştiriciye veya test ortamına dağıtım yapıyorsanız, daha fazla müdahale etmeden rol üyelikleri dağıtmak istersiniz. Bu konuda, bu zorluğu ele almak için kullanabileceğiniz bir yaklaşım açıklanmaktadır.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="task-overview"></a>Göreve genel bakış

Bu konuda aşağıdakiler varsayılmaktadır:

- Proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklandığı gibi, çözüm dağıtımına bölünmüş proje dosyası yaklaşımını kullanabilirsiniz.
- [Yapı sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md)bölümünde açıklandığı gibi, veritabanı projenizi dağıtmak için, proje dosyasından VSDBCMD ' i çağırın.

Bir veritabanı projesini bir test ortamına dağıtırken veritabanı kullanıcıları oluşturmak ve rol üyelikleri atamak için şunları yapmanız gerekir:

- Gerekli veritabanı değişikliklerini yapan bir Transact Yapılandırılmış Sorgu Dili (Transact-SQL) betiği oluşturun.
- SQL betiğini çalıştırmak için sqlcmd. exe yardımcı programını kullanan bir Microsoft Build Engine (MSBuild) hedefi oluşturun.
- Çözümünüzü bir test ortamına dağıttığınızda, proje dosyalarınızı hedefi çağıracak şekilde yapılandırın.

Bu konu, bu yordamların her birini nasıl gerçekleştirekullanacağınızı gösterir.

## <a name="scripting-the-database-role-memberships"></a>Veritabanı rolü üyeliklerini komut dosyası oluşturma

Bir Transact-SQL komut dosyasını çok çeşitli yollarla ve seçtiğiniz herhangi bir konumda oluşturabilirsiniz. En kolay yaklaşım, Visual Studio 2010 ' de çözümünüz içinde betik oluşturmaktır.

**Bir SQL betiği oluşturmak için**

1. **Çözüm Gezgini** penceresinde, veritabanı proje düğümünüz ' ı genişletin.
2. **Betikler** klasörüne sağ tıklayın, **Ekle**' nin üzerine gelin ve **Yeni klasör**' e tıklayın.
3. Klasör adı olarak **Test** yazın ve ardından ENTER tuşuna basın.
4. **Test** klasörüne sağ tıklayın, **Ekle**' nin üzerine gelin ve ardından **komut dosyası**' na tıklayın.
5. **Yeni öğe Ekle** iletişim kutusunda, betiğe anlamlı bir ad verin (örneğin, **Addrolemembersevk. SQL**) ve ardından **Ekle**' ye tıklayın.

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. *Addrolemembersevk. SQL* dosyasında, aşağıdakileri içeren Transact-SQL deyimlerini ekleyin:

    1. Veritabanınıza erişecek SQL Server oturum açma için bir veritabanı kullanıcısı oluşturun.
    2. Veritabanı kullanıcısını gerekli herhangi bir veritabanı rolüne ekleyin.
7. Dosya şuna benzemelidir:

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. Dosyayı kaydedin.

## <a name="executing-the-script-on-the-target-database"></a>Betiği hedef veritabanında yürütme

İdeal olarak, veritabanı projenizi dağıtırken dağıtım sonrası komut dosyasının bir parçası olarak gerekli Transact-SQL komut dosyalarını çalıştırırsınız. Ancak, dağıtım sonrası betikleri çözüm yapılandırmalarına veya derleme özelliklerine göre koşullu olarak mantıksal bir şekilde yürütmenize izin vermez. Alternatif, sqlcmd. exe komutunu yürüten bir **hedef** öğe oluşturarak SQL komut dosyalarınızı doğrudan MSBuild proje dosyasından çalıştırmakdır. Komut dosyanızı hedef veritabanında çalıştırmak için bu komutu kullanabilirsiniz:

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> Sqlcmd komut satırı seçenekleri hakkında daha fazla bilgi için bkz. [sqlcmd yardımcı programı](https://msdn.microsoft.com/library/ms162773.aspx).

Bu komutu bir MSBuild hedefine eklemeden önce, komut dosyasının çalıştırılmasını istediğiniz koşulları göz önünde bulundurmanız gerekir:

- Rol üyeliklerini değiştirmeden önce hedef veritabanının mevcut olması gerekir. Bu nedenle, veritabanı dağıtımından *sonra* bu betiği çalıştırmanız gerekir.
- Betiğin yalnızca test ortamları için yürütülmesi için bir koşul eklemeniz gerekir.
- Diğer bir deyişle "ne tür" dağıtımı&#x2014;çalıştırıyorsanız, dağıtım betikleri oluşturuyorsanız ancak bunları&#x2014;ÇALıŞTıRMADıYSANıZ, SQL betiğini çalıştırmanız gerekmez.

[Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını, Contact Manager örnek çözümünde gösterildiği gıbı kullanıyorsanız SQL betiğinizin derleme yönergelerini şöyle bölebilirsiniz:

- Gerekli ortama özgü özellikler, izinlerin dağıtılacağını belirleyen özelliği ile birlikte, ortama özgü proje dosyasında (örneğin, *env-dev. proj*) gidip gelmelidir.
- MSBuild hedefinin kendisi, hedef ortamlar arasında değişmeyecek özelliklerle birlikte, evrensel proje dosyasına (örneğin, *Publish. proj*) gitmelidir.

Ortama özgü proje dosyasında, veritabanı sunucusu adını, hedef veritabanı adını ve kullanıcının rol üyelikleri dağıtıp dağıtmayacağını belirtmesini sağlayan bir Boolean özelliğini tanımlamanız gerekir.

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

Evrensel proje dosyasında, sqlcmd yürütülebilir dosyasının konumunu ve çalıştırmak istediğiniz SQL komut dosyasının konumunu sağlamanız gerekir. Bu özellikler hedef ortamdan bağımsız olarak aynı kalır. Ayrıca sqlcmd komutunu yürütmek için bir MSBuild hedefi oluşturmanız gerekir.

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

Diğer hedeflere yararlı olabilecek şekilde, sqlcmd yürütülebilir dosyasının konumunu statik özellik olarak eklemediğine dikkat edin. Buna karşılık, hedef yürütülmeden önce gerekli olmadıkları için SQL betiğinizin konumunu ve sqlcmd komutunun sözdizimini hedef içinde dinamik özellikler olarak tanımlarsınız. Bu durumda, **Deploytestdbpermissions** hedefi yalnızca bu koşullar karşılandığında yürütülür:

- **Deploytestdbrolemembersevk** özelliği **true**olarak ayarlanır.
- Kullanıcı bir **whatIf = true** bayrağı belirtmemiştir.

Son olarak, hedefi çağırmayı unutmayın. *Publish. proj* dosyasında, varsayılan **fullpublish** hedefinin bağımlılık listesine hedefi ekleyerek bunu yapabilirsiniz. **Publishdbpackages** hedefi yürütülene kadar **Deploytestdbpermissions** hedefinin yürütülmediğinden emin olmanız gerekir.

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a>Sonuç

Bu konu, veritabanı projesi dağıtırken veritabanı kullanıcılarını ve rol üyeliklerini dağıtım sonrası eylem olarak ekleyebileceğiniz bir yol açıklanır. Bu, genellikle bir test ortamında bir veritabanını düzenli olarak yeniden oluşturduğunuzda faydalıdır, ancak veritabanlarını hazırlama veya üretim ortamlarına dağıtırken genellikle kaçınılmalıdır. Bu nedenle, veritabanı kullanıcıları ve rol üyeliklerinin yalnızca bunu yapmak uygun olduğunda oluşturulması için gerekli koşullu mantığı kullandığınızdan emin olmanız gerekir.

## <a name="further-reading"></a>Daha Fazla Bilgi

Veritabanı projelerini dağıtmak için VSDBCMD kullanma hakkında daha fazla bilgi için bkz. [veritabanı projelerini dağıtma](../web-deployment-in-the-enterprise/deploying-database-projects.md). Farklı hedef ortamları için veritabanı dağıtımlarını Özelleştirme Kılavuzu için bkz. [birden çok ortam Için veritabanı dağıtımlarını özelleştirme](customizing-database-deployments-for-multiple-environments.md). Dağıtım işlemini denetlemek için özel MSBuild proje dosyalarını kullanma hakkında daha fazla bilgi için bkz. [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md) ve [derleme sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md). Sqlcmd komut satırı seçenekleri hakkında daha fazla bilgi için bkz. [sqlcmd yardımcı programı](https://msdn.microsoft.com/library/ms162773.aspx).

> [!div class="step-by-step"]
> [Önceki](customizing-database-deployments-for-multiple-environments.md)
> [İleri](deploying-membership-databases-to-enterprise-environments.md)
