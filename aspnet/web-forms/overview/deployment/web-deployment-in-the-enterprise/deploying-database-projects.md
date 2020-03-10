---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
title: Veritabanı projelerini dağıtma | Microsoft Docs
author: jrjlee
description: 'Note: birçok kurumsal dağıtım senaryosunda, dağıtılmış bir veritabanına artımlı güncelleştirmeler yayımlama yeteneğinin olması gerekir. Alternatif yeniden oluşturmak...'
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 832f226a-1aa3-4093-8c29-ce4196793259
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
msc.type: authoredcontent
ms.openlocfilehash: 221808758492aedb8e8329364e511df28fd11105
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634269"
---
# <a name="deploying-database-projects"></a>Veritabanı Projeleri Dağıtma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> [!NOTE]
> Birçok kurumsal dağıtım senaryosunda, dağıtılmış bir veritabanına artımlı güncelleştirmeler yayımlama yeteneğinin olması gerekir. Diğer bir deyişle, veritabanını her dağıtımda yeniden oluşturmak, bu da var olan veritabanındaki tüm verileri kaybetmeniz anlamına gelir. Visual Studio 2010 ile çalışırken, VSDBCMD kullanmak, artımlı veritabanı yayımlaması için önerilen yaklaşımdır. Ancak, Visual Studio 'nun sonraki sürümü ve Web yayımlama işlem hattı (WPP) doğrudan artımlı yayımlamayı destekleyen araçları içerir.

Visual Studio 2010 ' de Contact Manager örnek çözümünü açarsanız, veritabanı projesinin dört dosya içeren bir Özellikler klasörü içerdiğini görürsünüz.

![](deploying-database-projects/_static/image1.png)

Proje dosyasıyla birlikte (Bu durumda*ContactManager. Database. dbproj* ), bu dosyalar derleme ve dağıtım sürecinin çeşitli yönlerini denetler:

- *Database. sqlcmdvars* dosyası, projeyi dağıtırken kullandığınız HERHANGI bir sqlcmd değişkeni için değerler sağlar. Her çözüm yapılandırması (örneğin, hata ayıklama ve yayın) farklı bir. sqlcmdvars dosyası belirtebilir.
- *Database. sqldeployment* dosyası, projenizde tanımlanan harmanlamayı ya da hedef sunucunun harmanlamasını kullanmak, hedef veritabanının her seferinde yeniden oluşturulup oluşturulmayacağını veya mevcut veritabanını güncel hale getirmek için bu şekilde değişiklik yapıp kılmayacağını, dağıtıma özgü ayarlar sağlar. Her çözüm yapılandırması, farklı bir. sqldeployment dosyası belirtebilir.
- *Database. sqlpermissions* dosyası, hedef veritabanına eklemek istediğiniz izinleri tanımlamak için KULLANABILECEĞINIZ bir XML belgesidir. Tüm çözüm konfigürasyonları aynı. sqlpermissions dosyasını paylaşır.
- *Database. sqlsettings* dosyası, veritabanı oluşturulurken kullanılacak harmanlama, karşılaştırma işleçleri davranışı vb. gibi veritabanı düzeyinde özellikleri belirtir. Tüm çözüm konfigürasyonları aynı. sqlsettings dosyasını paylaşır.

Bu dosyaların Visual Studio 'da açılması ve içerikleri öğrenmeniz bir süre harcamaktır.

Bir veritabanı projesi oluşturduğunuzda, yapı işlemi iki dosya oluşturur:

- Bir *veritabanı şeması* (. dbschema dosyası). Bu, XML biçiminde oluşturmak istediğiniz veritabanının şemasını açıklar.
- *Dağıtım bildirimi* (. DeployManifest dosyası). Bu, veritabanınızı oluşturmak ve dağıtmak için gereken tüm bilgileri içerir. Dağıtım yönergeleri (. sqldeployment dosyası) ve dağıtım öncesi veya dağıtım sonrası SQL betikleri gibi diğer kaynaklarla birlikte. dbschema dosyasına başvurur.

Bu kaynaklar arasındaki ilişkiyi gösterir:

![](deploying-database-projects/_static/image2.png)

Gördüğünüz gibi,. sqlsettings dosyası ve. sqlpermissions dosyası yapı işlemine yönelik girişlerdir. Veritabanı proje dosyası ile birlikte, bu dosyalar veritabanı şeması dosyasını oluşturmak için kullanılır. . Sqldeployment dosyası ve. sqlcmdvars dosyası, yapı işlemi değiştirilmeden geçer. Dağıtım bildirimi, veritabanı şemasının konumunu,. sqldeployment dosyasını,. sqlcmdvars dosyasını ve dağıtım öncesi veya dağıtım sonrası SQL betiklerini gösterir.

## <a name="why-use-vsdbcmd-to-deploy-a-database-project"></a>Bir veritabanı projesini dağıtmak için neden VSDBCMD kullanılmalıdır?

Veritabanı projelerini dağıtmaya yönelik çeşitli farklı yaklaşımlar vardır. Ancak, bunların hepsi bir veritabanı projesini kurumsal bir ortamdaki uzak sunuculara dağıtmak için uygun değildir. Veritabanı projesi dağıtımından istediğinizi göz önünde bulundurun. Kurumsal dağıtım senaryolarında, muhtemelen şunları yapmak isteyebilirsiniz:

- Veritabanı projesini uzak bir konumdan dağıtma özelliği.
- Var olan bir veritabanında artımlı güncelleştirmeler yapma özelliği.
- Dağıtım öncesi betikleri veya dağıtım sonrası betikleri ekleme özelliği.
- Dağıtımı birden çok hedef ortama uyarlayabilme özelliği.
- Veritabanı projesini daha büyük, genellikle komut dosyalı, tek adımlı bir çözüm dağıtımının parçası olarak dağıtma özelliği.

Bir veritabanı projesini dağıtmak için kullanabileceğiniz üç ana yaklaşım vardır:

- Visual Studio 2010 ' de veritabanı proje türüyle dağıtım işlevselliğini kullanabilirsiniz. Visual Studio 2010 ' de bir veritabanı projesi derleyip dağıtırken, dağıtım işlemi, derleme yapılandırmasına özel bir SQL tabanlı dağıtım dosyası oluşturmak için dağıtım bildirimini kullanır. Bu, zaten mevcut değilse veritabanını oluşturur veya zaten varsa veritabanında gerekli değişiklikleri yapar. Bu dosyayı hedef sunucunuzda çalıştırmak için SQLCMD. exe ' yi kullanabilir veya Visual Studio 'Yu dosyayı oluşturmak ve çalıştırmak için ayarlayabilirsiniz. Bu yaklaşımın dezavantajı, dağıtım ayarları üzerinde yalnızca sınırlı denetim sahibi olmanız olabilir. Ayrıca, ortama özgü değişken değerleri sağlamak için SQL dağıtım dosyasını da değiştirmeniz gerekebilir. Bu yaklaşımı yalnızca Visual Studio 2010 yüklü bir bilgisayardan kullanabilirsiniz ve geliştiricinin tüm hedef ortamlar için bağlantı dizelerini ve kimlik bilgilerini bilmeleri ve sağlaması gerekir.
- Bir [veritabanını bir Web uygulaması projesinin parçası olarak dağıtmak](https://msdn.microsoft.com/library/dd465343.aspx)için Internet INFORMATION SERVICES (IIS) Web Dağıtım aracı 'nı (Web dağıtımı) kullanabilirsiniz. Ancak, bir hedef sunucuda var olan bir yerel veritabanını çoğaltmak yerine bir veritabanı projesi dağıtmak istiyorsanız bu yaklaşım çok daha karmaşıktır. Veritabanı projesinin oluşturduğu SQL dağıtım betiğini çalıştırmak için Web Dağıtımı yapılandırabilirsiniz, ancak bunu yapmak için, Web uygulaması projeniz için özel bir WPP hedef dosyası oluşturmanız gerekir. Bu, dağıtım işlemine önemli miktarda karmaşıklık ekler. Ayrıca, Web Dağıtımı var olan veritabanlarına Artımlı güncelleştirmeleri doğrudan desteklemez. Bu yaklaşım hakkında daha fazla bilgi için bkz. [Web yayımlama işlem hattını paketlemek için veritabanı projesi DAĞıTıLAN SQL dosyasını genişletme](https://go.microsoft.com/?linkid=9805121).
- Veritabanı şemasını ya da dağıtım bildirimini kullanarak veritabanını dağıtmak için VSDBCMD yardımcı programını kullanabilirsiniz. VSDBCMD. exe ' yi, daha büyük, komut dosyalı dağıtım sürecinin bir parçası olarak veritabanlarını yayımlamanıza olanak tanıyan bir MSBuild hedefinden çağırabilirsiniz. . Sqlcmdvars dosyanızdaki ve diğer veritabanı özelliklerindeki değişkenleri, birden çok derleme yapılandırması oluşturmadan farklı ortamlarda dağıtımınızı özelleştirmenizi sağlayan bir VSDBCMD komutundan geçersiz kılabilirsiniz. VSDBCMD, fark eden işlevsellik sağlar, yani yalnızca hedef veritabanını veritabanı şemanıza göre hizalamak için gerekli değişiklikleri yapar. VSDBCMD, dağıtım işlemi üzerinde ayrıntılı denetim sağlayan çok çeşitli komut satırı seçenekleri de sunmaktadır.

Bu genel bakışta, genel bir kurumsal dağıtım senaryosuna en uygun yaklaşım olan VSDBCMD ' yi MSBuild ile birlikte kullanma makalesine bakabilirsiniz:

|  | Visual Studio 2010 | Web Deploy 2.0 | VSDBCMD.exe |
| --- | --- | --- | --- |
| Uzaktan dağıtımı destekliyor mu? | Evet | Evet | Evet |
| Artımlı güncelleştirmeler destekleniyor mu? | Evet | Hayır | Evet |
| Dağıtım öncesi/dağıtım sonrası betikleri destekliyor mu? | Evet | Evet | Evet |
| Çok ortamlı dağıtımı destekliyor mu? | Sınırlı | Sınırlı | Evet |
| Betikleştirilmiş dağıtımı destekliyor mu? | Sınırlı | Evet | Evet |

Bu konunun geri kalanında, veritabanı projelerini dağıtmak için VSDBCMD ' nin MSBuild ile kullanımı açıklanmaktadır.

## <a name="understanding-the-deployment-process"></a>Dağıtım sürecini anlama

VSDBCMD yardımcı programı veritabanı şemasını (. dbschema dosyası) veya dağıtım bildirimini (. DeployManifest dosyası) kullanarak bir veritabanını dağıtmanıza olanak tanır. Uygulamada, dağıtım bildirimi, çeşitli dağıtım özellikleri için varsayılan değerler sağlamanıza ve dağıtım öncesi veya dağıtım sonrası SQL betikleri çalıştırmak istediğinizi belirleyebilmenizi sağlayan dağıtım bildirimini neredeyse her zaman kullanacaksınız. Örneğin, bu VSDBCMD komutu, **ContactManager** veritabanını bir test ortamındaki veritabanı sunucusuna dağıtmak için kullanılır:

[!code-console[Main](deploying-database-projects/samples/sample1.cmd)]

Bu durumda:

- **/A** (veya **/Action**) anahtarı, VSDBCMD ' nin ne yapmak istediğinizi belirtir. Bunu **içeri** veya **dağıtıma**ayarlayabilirsiniz. **Içeri aktarma** seçeneği, var olan bir veritabanından bir. dbschema dosyası oluşturmak için kullanılır ve **Deploy** seçeneği bir. dbschema dosyasını hedef veritabanına dağıtmak için kullanılır.
- **/MANIFEST** (veya **/ManifestFile**) anahtarı, dağıtmak istediğiniz. DeployManifest dosyasını tanımlar. Bunun yerine. dbschema dosyasını kullanmak isterseniz, **/model** (veya **/ModelFile**) anahtarını kullanın.
- **/CS** (veya **/ConnectionString**) anahtarı, hedef veritabanı sunucusu için bağlantı dizesini sağlar. Bunun veritabanı oluşturmak için, VSDBCMD veritabanının&#x2014;adını içermediğinden sunucuya bağlanması gerektiğini unutmayın; tek bir veritabanına bağlanması gerekmez. . DeployManifest dosyanız bir bağlantı dizesi içeriyorsa, bu anahtarı atlayabilirsiniz. Anahtarı yine de kullanırsanız, anahtar değeri. DeployManifest değerini geçersiz kılar.
- <strong>/P: TargetDatabase</strong> özelliği, oluşturma sırasında hedef veritabanına atamak istediğiniz adı sağlar. Bu,. DeployManifest dosyasındaki <strong>TargetDatabase</strong> özelliğinin değerini geçersiz kılar. Çok çeşitli dağıtım özellikleri ayarlamak ve. sqlcmdvars dosyanızda belirtilen tüm SQLCMD değişkenlerini geçersiz kılmak için <strong>/p:</strong> <em>[Property Name]</em>sözdizimini kullanabilirsiniz.
- **/Dd +** (veya **/DeployToDatabase +** ) anahtarı, bir dağıtım oluşturup hedef ortama dağıtmak istediğinizi belirtir. **/Dd-** belirtirseniz veya anahtarı atlarsanız, VSDBCMD bir dağıtım betiği oluşturur, ancak bunu hedef ortama dağıtmaz. Bu anahtar genellikle karışıklık kaynağıdır ve sonraki bölümde daha ayrıntılı olarak açıklanmıştır.
- **/Script** (veya **/DeploymentScriptFile**) anahtarı, dağıtım betiğini nerede oluşturmak istediğinizi belirtir. Bu değer dağıtım sürecini etkilemez.

VSDBCMD hakkında daha fazla bilgi için bkz [. VSDBCMD Için komut satırı başvurusu. EXE (dağıtım ve şema Içeri aktarma)](https://msdn.microsoft.com/library/dd193283.aspx) ve [nasıl yapılır: VSDBCMD kullanarak bir veritabanını bir komut Isteminden dağıtıma hazırlama. EXE](https://msdn.microsoft.com/library/dd193258.aspx).

VSDBCMD 'yi MSBuild proje dosyasından nasıl kullanabileceğiniz hakkında bir örnek için bkz. [Yapı sürecini anlama](understanding-the-build-process.md). Birden çok ortam için veritabanı dağıtım ayarlarını yapılandırma örnekleri için bkz. [birden çok ortam Için veritabanı dağıtımlarını özelleştirme](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md).

## <a name="understanding-the-deploytodatabase-switch"></a>DeployToDatabase anahtarını anlama

**/Dd** veya **/DeployToDatabase** anahtarının davranışı, VSDBCMD 'yi bir. dbschema dosyası veya. DeployManifest dosyası ile kullanıp kullanmayacağınızı bağlıdır. Bir. dbschema dosyası kullanıyorsanız, davranış oldukça basittir:

- **/Dd +** veya **/dd**belirtirseniz, VSDBCMD bir dağıtım betiği oluşturacak ve veritabanını dağıtacaktır.
- **/DDI** belirtirseniz veya anahtarı atlarsanız, VSDBCMD yalnızca bir dağıtım betiği oluşturacaktır.

. DeployManifest dosyası kullanıyorsanız, davranış çok daha karmaşıktır. Bunun nedeni. DeployManifest dosyasında, veritabanının dağıtılıp dağıtılmadığını da belirleyen bir **DeployToDatabase** Özellik adı içerir.

[!code-xml[Main](deploying-database-projects/samples/sample2.xml)]

Bu özelliğin değeri, veritabanı projesinin özelliklerine göre ayarlanır. **Dağıtım betiği (. SQL) oluşturmak**için **Dağıt eylemini** ayarlarsanız, değer **false**olur. **Dağıtım betiği (. SQL) oluşturmak ve veritabanına dağıtmak**için **Dağıt eylemini** ayarlarsanız değer **true**olur.

> [!NOTE]
> Bu ayarlar, belirli bir yapı yapılandırması ve platformu ile ilişkilendirilir. Örneğin, **hata ayıklama** yapılandırması için ayarları yapılandırır ve ardından **Sürüm** yapılandırması ' nı kullanarak yayımlarsanız, ayarlarınız kullanılmaz.

![](deploying-database-projects/_static/image3.png)

> [!NOTE]
> Bu senaryoda, Visual Studio 2010 ' ın veritabanınızı dağıtmasını istemediğiniz için dağıtım **eylemi** her zaman **bir dağıtım betiği (. SQL) oluşturmak**üzere ayarlanmalıdır. Diğer bir deyişle, **DeployToDatabase** özelliği her zaman **false**olmalıdır.

Bir **DeployToDatabase** özelliği belirtildiğinde, **/dd** anahtarı yalnızca özellik değeri **false**olduğunda özelliği geçersiz kılar:

- **DeployToDatabase** özelliği **false**ise ve **/dd +** ya da **/dd**belirtirseniz VSDBCMD, **DeployToDatabase** özelliğini geçersiz kılar ve veritabanını dağıtır.
- **DeployToDatabase** özelliği **false**ise ve **/DDI** belirtirseniz veya anahtarı atlarsanız, VSDBCMD veritabanını dağıtmaz.
- **DeployToDatabase** özelliği **true**ise, VSDBCMD bu anahtarı yoksayar ve veritabanını dağıtır.
- Her durumda, veritabanını dağıtıp dağıtmaktan bağımsız olarak bir dağıtım betiği oluşturulur.

## <a name="conclusion"></a>Sonuç

Bu konu, Visual Studio 2010 ' deki veritabanı projelerine yönelik derleme ve dağıtım sürecine genel bir bakış sağlamıştır. Ayrıca, kurumsal ölçekte veritabanı dağıtımını desteklemek için VSDBCMD. exe ' yi MSBuild ile nasıl kullanabileceğinizi da açıklanmaktadır.

Bu uygulamada nasıl çalıştığı hakkında daha fazla bilgi için bkz. [birden çok ortam Için veritabanı dağıtımlarını özelleştirme](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md).

## <a name="further-reading"></a>Daha Fazla Bilgi

Her ortam için ayrı bir dağıtım yapılandırma dosyası oluşturarak veritabanı dağıtımlarını özelleştirme hakkında daha fazla bilgi için bkz. [birden çok ortam Için veritabanı dağıtımlarını özelleştirme](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md). Dağıtım sonrası betiği çalıştırarak veritabanı rolü üyeliklerini yapılandırma hakkında yönergeler için bkz. [test ortamlarına veritabanı rolü üyelikleri dağıtma](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md). Üyelik veritabanlarının getirmesindeki bazı benzersiz güçlükleri yönetme hakkında yönergeler için bkz. [Üyelik veritabanlarını kurumsal ortamlara dağıtma](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md).

MSDN 'deki bu konular, Visual Studio veritabanı projeleri ve veritabanı dağıtım işlemi hakkında daha geniş yönergeler ve arka plan bilgileri sağlar:

- [Visual Studio 2010 SQL Server veritabanı projeleri](https://msdn.microsoft.com/library/ff678491.aspx)
- [Veritabanı değişikliğini yönetme](https://msdn.microsoft.com/library/aa833404.aspx)
- [Nasıl yapılır: VSDBCMD kullanarak bir veritabanını bir komut Isteminden dağıtıma hazırlama. EXE](https://msdn.microsoft.com/library/dd193258.aspx)
- [Veritabanına genel bakış Derleme ve Dağıtım](https://msdn.microsoft.com/library/aa833165.aspx)

> [!div class="step-by-step"]
> [Önceki](deploying-web-packages.md)
> [İleri](creating-and-running-a-deployment-command-file.md)
