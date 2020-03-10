---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: Web paketlerini dağıtma | Microsoft Docs
author: jrjlee
description: Bu konu, Internet Information Services (IIS) Web Dağıtım aracı 'nı (Web...) kullanarak uzak bir sunucuya nasıl Web dağıtım paketleri yayımlayabileceğinizi açıklamaktadır.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 91b99e6e250342851aea6860164b6f6af54818d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575952"
---
# <a name="deploying-web-packages"></a>Web Paketleri Dağıtma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) 2,0 ' i kullanarak Web dağıtım paketlerini uzak bir sunucuya nasıl yayımlayacağınız açıklanmaktadır.
> 
> Bir Web paketini uzak bir sunucuya dağıtabilmeniz için iki ana yol vardır:
> 
> - MSDeploy. exe komut satırı yardımcı programını doğrudan kullanabilirsiniz.
> - Yapı işleminin oluşturduğu *[proje adı]. deploy. cmd* dosyasını çalıştırabilirsiniz.
> 
> Son sonuç kullandığınız yaklaşımdan bağımsız olarak aynıdır. Temel olarak, tüm *. deploy. cmd* dosyası, önceden belirlenmiş bazı değerlerle MSDeploy. exe ' yi çalıştırmak ve paketin dağıtılması için çok fazla bilgi sağlamanız gerekmez. Bu, dağıtım sürecini basitleştirir. Öte yandan, MSDeploy. exe ' nin kullanılması, paketinizin nasıl dağıtıldığına tam olarak daha fazla esneklik sağlar.
> 
> Kullandığınız yaklaşım, dağıtım işlemi üzerinde ne kadar denetim yapmanız gerektiğini ve Web Dağıtımı uzak aracı hizmetini mi yoksa Web Dağıtımı Işleyicisini mi hedeflemeyeceğinizi de içeren çeşitli faktörlere bağlıdır. Bu konu, her yaklaşımın nasıl kullanılacağını açıklar ve her yaklaşımın uygun olduğu zaman tanımlar.
> 
> Bu konudaki görevler ve izlenecek yollar şu şekilde kabul eder:
> 
> - Web uygulaması [projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md)bölümünde açıklandığı gibi Web uygulamanızı derlediniz ve paketlediniz.
> - [Web paketi dağıtımı Için parametreleri yapılandırma](configuring-parameters-for-web-package-deployment.md)bölümünde açıklandığı gibi, hedef ortamınız için doğru parametre değerlerini sağlamak üzere *SetParameters. xml* dosyasını değiştirdiniz.

[*Proje adı*] *. deploy. cmd* dosyası çalıştırmak, bir Web paketini dağıtmanın en kolay yoludur. Özellikle, *. deploy. cmd* dosyasını kullanmak MSDeploy. exe ' yi doğrudan kullanarak bu avantajları sağlar:

- Web dağıtım paketinin&#x2014;konumunu belirtmeniz gerekmez *. deploy. cmd* dosyası zaten nerede olduğunu biliyor.
- *SetParameters. xml* dosyasının&#x2014;konumunu belirtmeniz gerekmez. *Deploy. cmd* dosyası zaten nerede olduğunu biliyor.
- Kaynak ve hedef MSDeploy sağlayıcıları&#x2014;belirtmeniz gerekmez *. deploy. cmd* dosyası zaten hangi değerleri kullanacağınızı biliyor.
- MSDeploy işlem ayarlarını&#x2014;belirtmeniz gerekmez *. deploy. cmd* dosyası, yaygın olarak gereken değerleri MSDeploy. exe komutuna otomatik olarak ekler.

Bir Web paketini dağıtmak için *. deploy. cmd* dosyasını kullanmadan önce şunları yapmalısınız:

- *. Deploy. cmd* dosyası, [*Proje adı*]. *SetParameters. xml* dosyası ve Web paketi ([*Proje adı*]. *zip*) aynı klasörslardır.
- Web Dağıtımı (MSDeploy. exe), *. deploy. cmd* dosyasını çalıştıran bilgisayara yüklenir.

*. Deploy. cmd* dosyası çeşitli komut satırı seçeneklerini destekler. Dosyayı bir komut isteminden çalıştırdığınızda bu temel sözdizimidir:

[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]

Çalışır durumda bir deneme çalıştırması veya canlı dağıtım gerçekleştirmek isteyip istemediğinizi belirtmek için **/t** bayrağını veya **/y** bayrağını belirtmelisiniz (her iki bayrağı aynı komutta kullanmayın). Bu tablo, bu bayrakların her birinin amacını açıklamaktadır.

| Bayrağı | Açıklama |
| --- | --- |
| **/T** | Bir deneme çalıştırmasını belirten **– whatIf** bayrağıyla MSDeploy. exe ' yi çağırır. Paketi dağıtmak yerine, paketi dağıtdıysanız ne olacağı hakkında bir rapor oluşturur. |
| **/Y** | **– WhatIf** bayrağı olmadan MSDeploy. exe ' yi çağırır. Bu, paketi yerel bilgisayara veya belirtilen hedef sunucuya dağıtır. |
| **/M** | Hedef sunucu adını veya hizmet URL 'sini belirtir. Burada sağlayabilmeniz gereken değerler hakkında daha fazla bilgi için, bu konudaki **uç nokta hususları** bölümüne bakın. **/M** bayrağını atlarsanız, paket yerel bilgisayara dağıtılır. |
| **Sitedeki** | Dağıtım gerçekleştirmek için MSDeploy. exe ' nin kullanması gereken kimlik doğrulama türünü belirtir. Olası değerler **NTLM** ve **temel**' dir. **/A** bayrağını atlarsanız, kimlik doğrulama türü, Web dağıtımı uzak Aracı hizmetine dağıtım için **NTLM** , Web dağıtımı Işleyicisine dağıtım için de **temel** değer olarak kullanılacak. |
| **P** | Kullanıcı adını belirtir. Bu, yalnızca temel kimlik doğrulaması kullanıyorsanız geçerlidir. |
| **/P** | Parolayı belirtir. Bu, yalnızca temel kimlik doğrulaması kullanıyorsanız geçerlidir. |
| **/L** | Paketin yerel IIS Express örneğine dağıtılması gerektiğini belirtir. |
| **/G** | Paketin, [Tempagent sağlayıcı ayarı](https://technet.microsoft.com/library/ee517345(WS.10).aspx)kullanılarak dağıtıldığını belirtir. **/G** bayrağını atlarsanız, değer varsayılan olarak **false**şeklindedir. |

> [!NOTE]
> Yapı işlemi her bir Web paketi oluşturduğunda, bu dağıtım seçeneklerini açıklayan *[proje adı]. deploy-Readme. txt* adlı bir dosya da oluşturur.

Bu bayraklara ek olarak, Web Dağıtımı işlem ayarlarını ek *. deploy. cmd* parametreleri olarak belirtebilirsiniz. Belirttiğiniz diğer ayarlar yalnızca temel alınan MSDeploy. exe komutuna geçirilir. Bu ayarlar hakkında daha fazla bilgi için, [Web dağıtımı Işlem ayarları](https://technet.microsoft.com/library/dd569089(WS.10).aspx)' na bakın.

ContactManager. Mvc Web uygulaması projesini *. deploy. cmd* dosyasını çalıştırarak bir test ortamına dağıtmak istediğinizi varsayalım. Test ortamınız, [Web dağıtımı yayımlaması için bir Web sunucusu yapılandırma (uzak Aracı)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)bölümünde açıklandığı gibi Web dağıtımı uzak aracı hizmetini kullanacak şekilde yapılandırılmıştır. Web uygulamasını dağıtmak için sonraki adımları gerçekleştirmeniz gerekir.

**. Deploy. cmd dosyasını kullanarak bir Web uygulamasını dağıtmak için**

1. Web uygulaması [projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md)bölümünde açıklandığı gibi Web uygulaması projesini derleyin ve paketleyin.
2. [Web paketi dağıtımı Için parametreleri yapılandırma](configuring-parameters-for-web-package-deployment.md)bölümünde açıklandığı gibi, *ContactManager. Mvc. SetParameters. xml* dosyasını test ortamınız için doğru parametre değerlerini içerecek şekilde değiştirin.
3. Bir komut Istemi penceresi açın ve *ContactManager. Mvc. deploy. cmd* dosyasının konumuna gidin.
4. Bu komutu yazın ve ENTER tuşuna basın:

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

Bu örnekte:

- **/Y** bayrağı, bir deneme çalıştırması yapmak yerine gerçekten paketi dağıtmak istediğinizi belirtir.
- **/M** bayrağı, paketi TESTWEB1 adlı sunucuya dağıtmak istediğinizi belirtir. Bu değerden MSDeploy. exe, http://TESTWEB1/MSDeployAgentServicekonumundaki Web Dağıtımı uzak Aracı hizmetine paketi dağıtmaya çalışacaktır.
- **/A** bayrağı, NTLM kimlik doğrulaması kullanmak istediğinizi belirtir. Bu nedenle, bir Kullanıcı adı ve parola belirtmeniz gerekmez.

*. Deploy. cmd* dosyasını kullanmanın dağıtım sürecini basitleştirdiğini anlamak için, yukarıda gösterilen seçenekleri kullanarak *ContactManager. Mvc. deploy. cmd* ' yi çalıştırdığınızda oluşturulan ve yürütülen MSDeploy. exe komutuna göz atın.

[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]

Web paketini dağıtmak için *. deploy. cmd* dosyasını kullanma hakkında daha fazla bilgi için bkz. [nasıl yapılır: dağıtım paketini Deploy. cmd dosyasını kullanarak oluşturma](https://msdn.microsoft.com/library/ff356104.aspx).

## <a name="using-msdeployexe"></a>MSDeploy. exe kullanma

*. Deploy. cmd* dosyasının kullanılması genellikle dağıtım sürecini basitleştirir, ancak MSDeploy. exe ' nin doğrudan kullanılması tercih edildiğinde bazı durumlar vardır. Örneğin:

- Web Dağıtımı Işleyicisine yönetici olmayan bir kullanıcı olarak dağıtmak istiyorsanız *. deploy. cmd* dosyasını kullanamazsınız. Bunun nedeni, **uç nokta hususları**bölümünde açıklandığı gibi Web dağıtımı 2,0 ' deki bir hatadır.
- Farklı konumlardaki farklı *SetParameters. xml* dosyaları arasında el ile geçiş yapmak istiyorsanız MSDeploy. exe ' yi doğrudan kullanmayı tercih edebilirsiniz.
- Birkaç MSDeploy. exe komut satırı bağımsız değişkenini geçersiz kılmak istiyorsanız, MSDeploy. exe ' yi doğrudan kullanmayı tercih edebilirsiniz.

MSDeploy. exe kullandığınızda, üç temel bilgi parçası sağlamanız gerekir:

- A **–** verilerinizin nereden geldiğini gösteren kaynak parametre.
- Verilerinizin nereye gittiğini belirten A **– dest** parametresi.
- A **–** gerçekleştirmek istediğiniz [işlemi](https://technet.microsoft.com/library/dd568989(WS.10).aspx) belirten fiil parametresi.

MSDeploy. exe, kaynak ve hedef verileri işlemek için [Web dağıtımı sağlayıcılara](https://technet.microsoft.com/library/dd569040(WS.10).aspx) bağımlıdır. Web Dağıtımı, kullanılabilecek&#x2014;uygulama ve veri kaynakları aralığını temsil eden çok sayıda sağlayıcı içerir. örneğin, SQL Server VERITABANLARı, IIS Web sunucuları, sertifikalar, genel derleme ÖNBELLEĞI (GAC) derlemeleri, çeşitli farklı yapılandırma dosyaları ve diğer birçok veri türü için sağlayıcılar vardır. **– Source parametresi ve** **– dest** parametresinin her ikisi de, **– Source**: [*ProviderName*] = [*Location*] biçiminde bir sağlayıcı belirtmelidir. Bir Web paketini bir IIS Web sitesine dağıttığınızda, bu değerleri kullanmanız gerekir:

- **– Kaynak** sağlayıcı her zaman [pakettir](https://technet.microsoft.com/library/dd569019(WS.10).aspx). Örneğin:

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- **– Dest** sağlayıcı her zaman [Otomatik](https://technet.microsoft.com/library/dd569016(WS.10).aspx)' dir. Örneğin:

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- **– Verb** her zaman **eşitlenir**.

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

Ayrıca, [sağlayıcıya özgü diğer ayarları](https://technet.microsoft.com/library/dd569001(WS.10).aspx) ve genel [işlem ayarlarını](https://technet.microsoft.com/library/dd569089(WS.10).aspx)belirtmeniz gerekir. Örneğin, ContactManager. Mvc Web uygulamasını bir hazırlama ortamına dağıtmak istediğinizi varsayalım. Dağıtım Web Dağıtımı Işleyicisini hedefleyecek ve temel kimlik doğrulaması kullanmalıdır. Web uygulamasını dağıtmak için sonraki adımları gerçekleştirmeniz gerekir.

**MSDeploy. exe kullanarak bir Web uygulaması dağıtmak için**

1. Web uygulaması [projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md)bölümünde açıklandığı gibi Web uygulaması projesini derleyin ve paketleyin.
2. [Web paketi dağıtımı Için parametreleri yapılandırma](configuring-parameters-for-web-package-deployment.md)bölümünde açıklandığı gibi, *ContactManager. Mvc. SetParameters. xml* dosyasını hazırlama ortamınız için doğru parametre değerlerini içerecek şekilde değiştirin.
3. Bir komut Istemi penceresi açın ve MSDeploy. exe konumuna gidin. Bu genellikle%PROGRAMFILES%\IIS\Microsoft Web Dağıtımı V2\msdeploy.exe.
4. Bu komutu yazın ve ENTER tuşuna basın (satır sonlarını göz ardı edin):

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

Bu örnekte:

- **– Source** parametresi, **paket** sağlayıcısını belirtir ve Web paketinin konumunu gösterir.
- **– Dest** parametresi **Otomatik** sağlayıcıyı belirtir. **ComputerName** ayarı, hedef sunucuda Web dağıtımı işleyicisinin hizmet URL 'sini sağlar. **AuthType** ayarı, temel kimlik doğrulaması kullanmak istediğinizi ve bu nedenle bir **Kullanıcı adı** ve **parola**sağlamanız gerektiğini gösterir. Son olarak, **ıncludeacl 'ler = "false"** ayarı, kaynak Web uygulamanızdaki dosyaların erişim denetim listelerini (ACL 'ler) hedef sunucuya kopyalamak istemediğinizi belirtir.
- **– Verb: Sync** bağımsız değişkeni, hedef sunucudaki kaynak içeriğini çoğaltmak istediğinizi belirtir.
- **– Disablelink** bağımsız değişkenleri, hedef sunucuda uygulama havuzlarını, sanal dizin yapılandırması veya GÜVENLI yuva KATMANı (SSL) sertifikalarını çoğaltmak istediğinizi belirtir. Daha fazla bilgi için bkz. [Web dağıtımı link Extensions](https://technet.microsoft.com/library/dd569028(WS.10).aspx).
- **– Setparamfile** parametresi, *SetParameters. xml* dosyasının konumunu sağlar.
- **– Allowgüvenilmeyen** anahtar, Web dağıtımı güvenilir bir sertifika yetkilisi tarafından verilmemiş SSL sertifikalarını kabul edeceğini belirtir. Web Dağıtımı Işleyicisine dağıtım yapıyorsanız ve hizmet URL 'sini güvenli hale getirmek için otomatik olarak imzalanan bir sertifika kullandıysanız, bu anahtarı eklemeniz gerekir.

## <a name="automating-web-package-deployment"></a>Web paketi dağıtımını otomatikleştirme

Birçok kurumsal senaryoda, Web paketlerinizi daha büyük bir tek adımlı veya otomatik dağıtımın parçası olarak dağıtmak isteyeceksiniz. Web paketlerinizi *. deploy. cmd* dosyasını çalıştırarak veya doğrudan MSDeploy. exe ' yi kullanarak dağıtmayı tercih ettiğinize bakılmaksızın, komutlarınızı parametreleyebilir ve Microsoft Build Engine (MSBuild) proje dosyasındaki bir hedeften çağırabilirsiniz.

Contact Manager örnek çözümünde *Publish. proj* dosyasındaki **publishwebpackages** hedefine göz atın. Bu hedef, **Publishpackages**adlı bir öğe listesi tarafından tanımlanan her *. deploy. cmd* dosyası için bir kez çalışır. Hedef, her *. deploy. cmd* dosyası için bağımsız değişken değerlerinin tam kümesini oluşturmak için özellikleri ve öğe meta verilerini kullanır ve ardından komutunu çalıştırmak için **Exec** görevini kullanır.

[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]

> [!NOTE]
> Örnek çözümde proje dosya modeline daha geniş bir genel bakış ve genel olarak özel proje dosyalarına giriş için, bkz. [Proje dosyasını anlama](understanding-the-project-file.md) ve [derleme sürecini anlama](understanding-the-build-process.md).

## <a name="endpoint-considerations"></a>Uç nokta değerlendirmeleri

Web paketinizi *. deploy. cmd* dosyasını çalıştırarak veya MSDeploy. exe ' yi doğrudan kullanarak dağıtıp dağıtana, dağıtımınız için bir bilgisayar adı veya hizmet uç noktası belirtmeniz gerekir.

Hedef Web sunucusu Web Dağıtımı uzak Aracı hizmeti kullanılarak dağıtım için yapılandırılırsa, hedef hizmet URL 'sini hedef olarak belirtirsiniz.

[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]

Alternatif olarak, sunucu adını yalnızca hedef olarak belirtebilir ve Web Dağıtımı uzak Aracı hizmeti URL 'sini çıkaracaktır.

[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]

Hedef Web sunucusu Web Dağıtımı Işleyicisi kullanılarak dağıtım için yapılandırılırsa, hedef olarak IIS Web yönetimi hizmeti 'nin (WMSvc) uç nokta adresini belirtmeniz gerekir. Bu, varsayılan olarak şu biçimdedir:

[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]

*. Deploy. cmd* dosyasını veya MSDeploy. exe ' yi kullanarak bu uç noktaların herhangi birini hedefleyebilirsiniz. Ancak, Web Dağıtımı Işleyicisine yönetici olmayan bir kullanıcı olarak dağıtmak istiyorsanız, [bir Web sunucusunu Web dağıtımı yayımı Için yapılandırma (Web dağıtımı işleyicisi)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)bölümünde açıklandığı gibi, hizmet uç noktası adresine bir sorgu dizesi eklemeniz gerekir.

[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]

Bunun nedeni, yönetici olmayan kullanıcının IIS 'e sunucu düzeyinde erişimi yoktur; yalnızca belirli bir IIS Web sitesine erişimi vardır. Yazma sırasında, Web yayımlama ardışık düzeninde (WPP) oluşan bir hata nedeniyle, *. deploy. cmd* dosyasını sorgu dizesi içeren bir uç nokta adresi kullanarak çalıştıramazsınız. Bu senaryoda, Web paketinizi MSDeploy. exe ' yi doğrudan kullanarak dağıtmanız gerekir.

> [!NOTE]
> Web Dağıtımı uzak Aracı hizmeti ve Web Dağıtımı Işleyicisi hakkında daha fazla bilgi için bkz. [Web dağıtımına doğru yaklaşımı seçme](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md). Ortama özgü proje dosyalarını bu uç noktalara dağıtılacak şekilde yapılandırma hakkında yönergeler için bkz. [hedef ortam Için dağıtım özelliklerini yapılandırma](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

## <a name="authentication-considerations"></a>Kimlik doğrulama konuları

Web paketinizi *. deploy. cmd* dosyasını çalıştırarak veya doğrudan MSDeploy. exe ' yi kullanarak dağıtıp dağıttıklarından bağımsız bir kimlik doğrulama türü belirtmeniz gerekir. Web Dağıtımı olası iki değeri kabul eder: **NTLM** veya **temel**. Temel kimlik doğrulaması belirtirseniz, bir Kullanıcı adı ve parola sağlamanız da gerekir. Kimlik doğrulama türünü seçerken bilmeniz gereken çeşitli faktörler vardır:

- Web Dağıtımı uzak Aracı hizmetine dağıtım yapıyorsanız, NTLM kimlik doğrulaması kullanmanız gerekir. Uzak Aracı hizmeti temel kimlik doğrulama kimlik bilgilerini kabul etmez.
- Web Dağıtımı Işleyicisine dağıtım yapıyorsanız, NTLM veya temel kimlik doğrulaması kullanabilirsiniz. Varsayılan ayar temel kimlik doğrulamadır. Temel kimlik doğrulaması, Kullanıcı adlarını ve parolaları düz metin olarak aktarılsa da, Web Dağıtımı Işleyicisi her zaman SSL şifrelemesi kullandığından kimlik bilgileriniz korunur.
- Web Paketiniz bir veritabanı içeriyorsa ve Web sunucusu ve veritabanı sunucusu ayrı makinelerdir, [NTLM "çift atlama" sınırlaması](https://go.microsoft.com/?linkid=9805120)nedenıyle veritabanını NTLM kimlik doğrulaması kullanarak dağıtamazsınız. Dağıtım bağlantı dizeniz SQL Server kimlik bilgilerini kullanmanız veya Web Dağıtımı için temel kimlik doğrulama kimlik bilgilerini sağlamanız gerekir. Bu sorun, [Üyelik veritabanlarının kurumsal ortamlara dağıtılmasında](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)daha ayrıntılı bir şekilde açıklanmıştır.

## <a name="conclusion"></a>Sonuç

Bu konuda, *. deploy. cmd* dosyasını çalıştırarak veya doğrudan MSDeploy. exe ' yi kullanarak bir Web paketini nasıl dağıtabileceğiniz açıklanmıştır. Her yaklaşım uygun olduğunda ve bir dağıtım komutunu daha büyük bir tek adımlı veya otomatik yapı sürecinin bir parçası olarak nasıl parametreleştirilekullanabileceğinizi ve çalıştıracağınızı açıklandı.

## <a name="further-reading"></a>Daha Fazla Bilgi

Web dağıtım paketini oluşturma ve Parametreleştirme hakkında yönergeler için bkz. [Web uygulaması projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md) ve [Web paketi dağıtımı için parametreleri yapılandırma](configuring-parameters-for-web-package-deployment.md). Bir Team Foundation Server (TFS) örneğinden Web paketleri oluşturma ve dağıtma hakkında yönergeler için bkz. [Otomatik Web dağıtımı için Team Foundation Server yapılandırma](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). Dağıtım işlemini özelleştirme ve sorun giderme hakkında bilgi için, bkz. [dosyaları ve klasörleri dağıtımdan dışlama](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md).

> [!div class="step-by-step"]
> [Önceki](configuring-parameters-for-web-package-deployment.md)
> [İleri](deploying-database-projects.md)
