---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: 'Uygulama yaşam döngüsü yönetimi: geliştirmeden üretime | Microsoft Docs'
author: jrjlee
description: Bu konuda, kurgusal bir şirketin test, hazırlama ve üretim ortamları aracılığıyla bir ASP.NET Web uygulamasının dağıtımını nasıl yönettiği gösterilmektedir...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 230cf4393db0ee19cfc42ed54359d61e7926a49d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640667"
---
# <a name="application-lifecycle-management-from-development-to-production"></a>Uygulama Yaşam Döngüsü Yönetimi: Geliştirmeden Üretime

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, kurgusal bir şirketin, sürekli bir geliştirme sürecinin bir parçası olarak test, hazırlama ve üretim ortamları aracılığıyla bir ASP.NET Web uygulamasının dağıtımını nasıl yönettiği gösterilmektedir. Konu başlığı boyunca bağlantılar, belirli görevlerin nasıl gerçekleştirileceği hakkında daha fazla bilgi ve izlenecek yollar için sağlanır.
> 
> Bu konu, kuruluştaki Web dağıtımıyla ilgili bir [dizi öğretici](deploying-web-applications-in-enterprise-scenarios.md) için yüksek düzeyde bir genel bakış sağlamak üzere tasarlanmıştır. Burada&#x2014;açıklanan öğreticilerin, bu görevlerin ve tekniklerle ilgili ayrıntılı bilgiler sağlaması hakkında daha fazla bilgi sahibi olmadığınız durumlarda endişelenmeyin.
> 
> > [!NOTE]
> > Basitlik sağlamak için bu konu, dağıtım sürecinin bir parçası olarak veritabanlarını güncelleştirme konusunda ele almaz. Ancak, veritabanları için artımlı güncelleştirmeler yapmak birçok kurumsal dağıtım senaryosunda gereksinimidir ve bu öğreticide daha sonra bu öğretici serisinde nasıl gerçekleştirileceğini gösteren yönergeler bulabilirsiniz. Daha fazla bilgi için bkz. [veritabanı projelerini dağıtma](../web-deployment-in-the-enterprise/deploying-database-projects.md).

## <a name="overview"></a>Genel bakış

Burada gösterilen dağıtım süreci, Kurumsal Web dağıtımı 'nda açıklanan Fabrikam, Inc. dağıtım senaryosuna dayanır [: senaryoya genel bakış](enterprise-web-deployment-scenario-overview.md). Bu konuyu inceetmeden önce senaryoya genel bakış konusunu okumalısınız. Temelde, senaryo, bir kuruluşun tipik bir kurumsal ortamdaki çeşitli aşamalar aracılığıyla makul bir karmaşık Web uygulamasının dağıtımını, [Ilgili kişi Yöneticisi çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)nasıl yönettiğini inceler.

Yüksek düzeyde, Contact Manager çözümü geliştirme ve dağıtım sürecinin bir parçası olarak bu aşamalardan geçer:

1. Geliştirici bazı kodları Team Foundation Server (TFS) 2010 ' ye denetler.
2. TFS kodu oluşturur ve takım projesiyle ilişkili tüm birim testlerini çalıştırır.
3. TFS, çözümü test ortamına dağıtır.
4. Geliştirici ekibi, çözümü test ortamında doğrular ve doğrular.
5. Hazırlama ortamı Yöneticisi, dağıtımın herhangi bir soruna neden olup olmayacağını belirlemek için hazırlama ortamında "ne tür" dağıtımı gerçekleştirir.
6. Hazırlama ortamı Yöneticisi, hazırlama ortamına canlı bir dağıtım gerçekleştirir.
7. Çözüm, hazırlama ortamında Kullanıcı kabul testini üstden geçer.
8. Web dağıtım paketleri üretim ortamına el ile aktarılır.

Bu aşamalar sürekli bir geliştirme döngüsünün bir parçasını oluşturur.

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

Uygulamada, her aşamada daha ayrıntılı olarak baktığımızda göreceğiniz gibi süreç bundan biraz daha karmaşıktır. Fabrikam, Inc. her hedef ortam için dağıtım için farklı bir yaklaşım kullanır.

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

Bu konunun geri kalanında bu dağıtım yaşam döngüsünün bu temel aşamaları incededir:

- **Önkoşullar**: dağıtım mantığınızı yerine koyabilmeniz için sunucu altyapınızı nasıl yapılandırmanız gerekir.
- İlk **geliştirme ve dağıtım**: çözümünüzü ilk kez dağıtmadan önce yapmanız gerekenler.
- **Test 'e dağıtım**: bir geliştirici yeni kodu iade ettiğinde, içeriği bir test ortamına otomatik olarak paketleme ve dağıtma.
- **Hazırlama dağıtımı**: belirli derlemeleri bir hazırlama ortamına dağıtma ve bir dağıtımın herhangi bir soruna neden olmamasını sağlamak için "durum" dağıtımları gerçekleştirme.
- **Üretime dağıtım**: ağ altyapısı uzaktan dağıtımı engellediğinde, Web paketlerini bir üretim ortamına aktarma.

## <a name="prerequisites"></a>Önkoşullar

Herhangi bir dağıtım senaryosunda ilk görev, sunucu altyapınızın dağıtım araçlarınızın ve tekniklerinizin gereksinimlerini karşıladığından emin olunması. Bu durumda, Fabrikam, Inc. sunucu altyapısını şunun gibi yapılandırmıştır:

- TFS, bir takım projesi koleksiyonu, derleme denetleyicileri ve yapı aracıları içerecek şekilde yapılandırılmıştır. Daha fazla bilgi için bkz. [Otomatik Web dağıtımı için Team Foundation Server yapılandırma](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) .
- Test ortamı, [Senaryo: Web dağıtımı için bir test ortamı yapılandırma](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md) ve [Web dağıtımı yayımlaması (uzak Aracı) Için bir Web sunucusu yapılandırma](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)bölümünde açıklandığı gibi Web Deployment Agent hizmeti ("uzak Aracı") kullanılarak uzak dağıtımları kabul edecek şekilde yapılandırılmıştır.
- Hazırlama ortamı, [Senaryo: Web dağıtımı Için hazırlama ortamı yapılandırma](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md) ve [Web Dağıtımı yayımlaması (Web dağıtımı işleyicisi) Için bir Web sunucusu yapılandırma](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)bölümünde açıklandığı gibi Web dağıtımı işleyici uç noktası kullanılarak uzak dağıtımları kabul edecek şekilde yapılandırılmıştır.
- Üretim ortamı, bir yöneticinin, Web dağıtımı [için bir üretim ortamı yapılandırma](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md) ve [Web dağıtımı yayımlaması (çevrimdışı dağıtım) Için bir Web sunucusu yapılandırma](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)konusunda açıklandığı gibi, Web DAĞıTıM paketlerini Internet Information Services (IIS) uygulamasına el ile içeri aktarmaya izin verecek şekilde yapılandırılmıştır.

## <a name="initial-development-and-deployment"></a>İlk geliştirme ve dağıtım

Fabrikam, Inc. geliştirme ekibinin, Contact Manager çözümünü ilk kez dağıtabilmesi için, bu görevleri gerçekleştirmesi gerekir:

- TFS 'de yeni bir takım projesi oluşturun.
- Dağıtım mantığını içeren Microsoft Build Engine (MSBuild) proje dosyaları oluşturun.
- Dağıtım süreçlerini tetikleyen TFS derleme tanımlarını oluşturun.

### <a name="create-a-new-team-project"></a>Yeni takım projesi oluştur

- TFS Yöneticisi, ramiz Walters, [TFS 'de bir takım projesi oluşturma](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)bölümünde açıklandığı gibi, uygulama için yeni bir takım projesi oluşturur. Daha sonra, müşteri adayı geliştiricisi, Matt hink bir çatı çözümü oluşturur. [Kaynak denetimine Içerik ekleme](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)bölümünde açıklandığı gibi, dosyalarını TFS 'deki yeni takım projesine denetler.

### <a name="create-the-deployment-logic"></a>Dağıtım mantığını oluşturma

Matt hink, [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını kullanarak çeşitli özel MSBuild proje dosyaları oluşturur. Matt oluşturduğunda:

- Dağıtım işlemini çalıştıran *Publish. proj* adlı bir proje dosyası. Bu dosya çözümdeki projeleri oluşturan MSBuild hedeflerini, Web paketleri oluşturmayı ve paketleri bir hedef sunucu ortamına dağıtmayı içerir.
- *Env-dev. proj* ve *env-Stage. proj*adlı ortama özgü proje dosyaları. Bunlar, bağlantı dizeleri, hizmet uç noktaları ve Web paketini alacak uzak hizmetin ayrıntıları gibi sırasıyla, test ortamına ve hazırlama ortamına özgü ayarları içerir. Belirli hedef ortamları için doğru ayarları seçme konusunda rehberlik için bkz. [hedef ortam Için dağıtım özelliklerini yapılandırma](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

Dağıtımı çalıştırmak için, bir Kullanıcı MSBuild veya takım derlemesi kullanarak *Publish. proj* dosyasını yürütür ve bir komut satırı bağımsız değişkeni olarak ilgili ortama özgü proje dosyasının (*env-dev. proj* veya *env-Stage. proj*) konumunu belirtir. *Publish. proj* dosyası daha sonra, her hedef ortam için tam bir yayımlama yönergeleri kümesi oluşturmak üzere ortama özgü proje dosyasını içeri aktarır.

> [!NOTE]
> Bu özel proje dosyalarının çalışma şekli, MSBuild 'i çağırmak için kullandığınız mekanizmaya bağımsızdır. Örneğin, [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklandığı gibi doğrudan MSBuild komut satırını kullanabilirsiniz. [Bir dağıtım komut dosyası oluşturma ve çalıştırma](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)bölümünde açıklandığı gibi, proje dosyalarını bir komut dosyasından çalıştırabilirsiniz. Alternatif olarak, [dağıtımı destekleyen bir yapı tanımı oluşturma](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)bölümünde açıklandığı gibi, proje dosyalarını TFS 'deki bir yapı tanımından çalıştırabilirsiniz.  
> Her durumda, nihai sonuç aynı&#x2014;MSBuild ile birleştirilmiş proje dosyası yürütülür ve çözümünüzü hedef ortama dağıtır. Bu, yayımlama işleminizi nasıl tetikleytiğiyle ilgili büyük bir esneklik sağlar.

Özel proje dosyalarını oluşturduktan sonra, Matt onları bir çözüm klasörüne ekler ve bunları kaynak denetimine iade eder.

### <a name="create-build-definitions"></a>Derleme tanımları oluştur

Son bir hazırlık görevi olarak, Matt ve Ramiz yeni takım projesi için üç derleme tanımı oluşturmak üzere birlikte çalışır:

- **Deploytotest**. Bu, Contact Manager çözümünü oluşturur ve her bir iade gerçekleştiğinde onu test ortamına dağıtır.
- **Deploytohazırlama**. Bu, bir geliştirici derlemeyi sıraya alırken, belirtilen bir önceki derlemeden alınan kaynakları hazırlama ortamına dağıtır.
- **Deploytohazırlama-whatIf**. Bu, bir geliştirici derlemeyi sıraya alırken hazırlama ortamına "durum" dağıtımını gerçekleştirir.

Aşağıdaki bölümler, bu derleme tanımlarının her biri hakkında daha fazla ayrıntı sağlar.

## <a name="deployment-to-test"></a>Teste dağıtım

Fabrikam, Inc. ' deki geliştirme ekibi, doğrulama ve doğrulama, kullanılabilirlik testi, Uyumluluk testi ve geçici ya da keşif testi gibi çeşitli yazılım test etkinliklerini gerçekleştirmek için test ortamlarını korur.

Geliştirme ekibi, TFS 'de **Deploytotest**adlı bir derleme tanımı oluşturdu. Bu derleme tanımı, bir sürekli tümleştirme tetikleyicisi kullanır. Bu, Fabrikam, Inc. geliştirme ekibinin bir üyesi her seferinde bir iade işlemi gerçekleştirdiğinde yapı işleminin çalıştırıldığı anlamına gelir. Bir yapı tetiklendiğinde, derleme tanımı şu şekilde olur:

- ContactManager. sln çözümünü oluşturun. Bu da çözüm içindeki her projeyi oluşturur.
- Çözüm klasörü yapısındaki tüm birim testlerini çalıştırın (çözüm başarıyla oluşturulmadıysanız).
- Dağıtım işlemini denetleyen özel proje dosyalarını çalıştırın (çözüm başarıyla oluşturulur ve herhangi bir birim testini geçirir).

Nihai sonuç, çözümün başarıyla oluşturulup birim testlerini geçirirse, Web paketleri ve diğer dağıtım kaynakları test ortamına dağıtılır.

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>Dağıtım Işlemi nasıl çalışır?

**Deploytotest** derleme tanımı, MSBuild 'e şu bağımsız değişkenleri sağlar:

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]

Ekip derlemesi çözüm içindeki projeleri oluşturduğunda, **Deployonbuild = true** ve **deploytarget = paket** özellikleri kullanılır. Proje bir Web uygulaması projesi olduğunda, bu özellikler MSBuild 'e proje için bir Web dağıtım paketi oluşturma talimatını verecektir. **Targetenvpropsfile** özelliği *Publish. proj* dosyasına aktarılacak ortama özgü proje dosyasını nerede bulacağını söyler.

> [!NOTE]
> Bunun gibi bir yapı tanımı oluşturma hakkında ayrıntılı yönergeler için, bkz. [dağıtımı destekleyen bir yapı tanımı oluşturma](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).

*Publish. proj* dosyası çözümdeki her bir projeyi oluşturan hedefleri içerir. Ancak, dosyayı takım derlemesinde yürütüyorsanız bu derleme hedeflerini atlayan koşullu mantığı da içerir. Bu, birim testlerini çalıştırma özelliği gibi ekip oluşturma tekliflerinin ek derleme işlevlerinden yararlanmanızı sağlar. Çözüm derlemesi veya birim testleri başarısız olursa, *Publish. proj* dosyası yürütülmez ve uygulama dağıtılacaktır.

Koşul mantığı, **Buildinginteambuild** özelliği hesaplanarak gerçekleştirilir. Bu, projelerinizi derlemek için takım derlemesi kullandığınızda otomatik olarak **true** olarak ayarlanan bir MSBuild özelliğidir.

## <a name="deployment-to-staging"></a>Hazırlama dağıtımı

Bir yapı, test ortamındaki geliştirici ekibinin tüm gereksinimlerini karşılıyorsa, ekip aynı derlemeyi hazırlama ortamına dağıtmak isteyebilir. Hazırlama ortamları genellikle, örneğin sunucu belirtimleri, işletim sistemleri ve yazılım ve ağ yapılandırması açısından, üretim veya "canlı" ortamının özellikleriyle eşleşecek şekilde yapılandırılır. Hazırlama ortamları genellikle yük testi, Kullanıcı kabul testi ve daha geniş iç incelemeler için kullanılır. Derlemeler hazırlama ortamına doğrudan yapı sunucusundan dağıtılır.

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

Çözümü hazırlama ortamına dağıtmak için kullanılan derleme tanımları **deploytohazırlama-whatIf** ve **deploytohazırlama**, bu özellikleri paylaşma:

- Aslında hiçbir şey oluşturmazlar. Ramiz çözümü hazırlama ortamına dağıttığında, test ortamında önceden doğrulanmış ve doğrulanmış olan belirli bir derlemeyi dağıtmak istemektedir. Derleme tanımlarının yalnızca dağıtım işlemini denetleyen özel proje dosyalarını çalıştırması gerekir.
- Ramiz bir derlemeyi tetiklerse, derleme sunucusundan dağıtmak istediği kaynakları hangi yapıda içerdiğini belirtmek için derleme parametrelerini kullanır.
- Derleme tanımları otomatik olarak tetiklenmez. Ramiz, çözümü hazırlama ortamına dağıtmak istediğinde bir derlemeyi el ile sıraya alır.

Bu, hazırlama ortamına dağıtım için üst düzey bir işlemdir:

1. Ramiz Walters, hazırlama ortamı Yöneticisi, **Deploytohazırlama-whatIf** derleme tanımını kullanarak bir derlemeyi kuyruğa alır. Ramiz hangi derlemeyi dağıtmak istediğini belirtmek için derleme tanımı parametrelerini kullanır.
2. **Deploytohazırlama-whatIf** derleme tanımı, özel proje dosyalarını "durum" modunda çalıştırır. Bu günlük dosyalarını, ramiz bir canlı dağıtım gerçekleştiriyor gibi oluşturur, ancak aslında hedef ortamda herhangi bir değişiklik yapmaz.
3. Ramiz, hazırlama ortamında dağıtımın etkilerini belirlemek için günlük dosyalarını gözden geçirir. Özellikle, ramiz nelerin ekleneceğini, nelerin güncelleştirileceğini ve nelerin silineceğini denetlemek istiyor.
4. Ramiz, dağıtımın mevcut kaynak veya verilerde istenmeyen bir değişiklik yapmayadüşünmemesi durumunda, bir derlemeyi **Deploytohazırlama** derleme tanımını kullanarak sıraya alır.
5. **Deploytohazırlama** derleme tanımı özel proje dosyalarını çalıştırır. Bu, dağıtım kaynaklarını hazırlama ortamında birincil web sunucusuna yayımlar.
6. Web grubu çerçevesi (WFF) denetleyicisi, hazırlama ortamındaki Web sunucularını eşitler. Bu, uygulamayı sunucu grubundaki tüm Web sunucularında kullanılabilir hale getirir.

### <a name="how-does-the-deployment-process-work"></a>Dağıtım Işlemi nasıl çalışır?

**Deploytohazırlama** derleme tanımı, MSBuild 'e şu bağımsız değişkenleri sağlar:

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]

**Targetenvpropsfile** özelliği *Publish. proj* dosyasına aktarılacak ortama özgü proje dosyasını nerede bulacağını söyler. **Outputroot** özelliği, yerleşik değeri geçersiz kılar ve dağıtmak istediğiniz kaynakları içeren yapı klasörünün konumunu gösterir. Ramiz derlemeyi sıraladığı zaman, **Outputroot** özelliği için güncelleştirilmiş bir değer sağlamak üzere **Parametreler** sekmesini kullanır.

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> Bunun gibi bir yapı tanımı oluşturma hakkında daha fazla bilgi için bkz. [belirli bir derlemeyi dağıtma](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md).

**Deploytohazırlama-whatIf** derleme tanımı, **deploytohazırlama** derleme tanımıyla aynı dağıtım mantığını içerir. Bununla birlikte, **whatIf = true**ek bağımsız değişkenini içerir:

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]

*Publish. proj* dosyasında, **whatIf** özelliği tüm dağıtım kaynaklarının "durum" modunda yayımlanması gerektiğini gösterir. Diğer bir deyişle, günlük dosyaları, dağıtım ilerlemiş gibi oluşturulur, ancak hedef ortamda hiçbir şey değiştirilmez. Bu, belirli bir dağıtımın&#x2014;etkisini özellikle, nelerin ekleneceğini, nelerin güncelleştirileceğini ve herhangi bir değişiklik yapmadan önce ne silineceğini&#x2014;değerlendirmenizi sağlar.

> [!NOTE]
> "Ne tür" dağıtımları yapılandırma hakkında daha fazla bilgi için, bkz. ["What If" dağıtımı gerçekleştirme](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md).

Uygulamanızı hazırlama ortamında birincil web sunucusuna dağıttıktan sonra WFF, uygulamayı sunucu grubundaki tüm sunucular arasında otomatik olarak eşitler.

> [!NOTE]
> Web sunucularını eşitlemeye yönelik WFF 'yi yapılandırma hakkında daha fazla bilgi için bkz. [Web grubu çerçevesiyle sunucu grubu oluşturma](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md).

## <a name="deployment-to-production"></a>Üretime dağıtım

Hazırlama ortamında bir derleme onaylandığında Fabrikam, Inc. ekibi uygulamayı üretim ortamında yayımlayabilir. Üretim ortamı, uygulamanın "canlı" olduğu ve son kullanıcıların hedef kitliğine ulaştığı yerdir.

Üretim ortamı, Internet 'e yönelik bir çevre ağındadır. Bu, yapı sunucusunu içeren iç ağdan yalıtılmıştır. Üretim ortamı Yöneticisi olan Lisa Andrews, Web dağıtım paketlerini derleme sunucusundan el ile kopyalayıp birincil üretim Web sunucusunda IIS 'ye içeri aktarmalıdır.

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

Bu, üretim ortamına dağıtım için üst düzey bir işlemdir:

1. Geliştirici ekibi, bir yapılandırmanın üretime dağıtım için hazırlanmaya uygun olduğunu öneren bir yapı sağlar. Ekip, derleme sunucusundaki bırakma klasörü içindeki Web Dağıtım paketlerinin konumunun LISA olduğunu önerir.
2. Lisa, derleme sunucusundan Web paketlerini toplar ve bunları üretim ortamında birincil web sunucusuna kopyalar.
3. LISA, Web paketlerini birincil web sunucusunda içeri aktarmak ve yayımlamak için IIS Yöneticisi 'Ni kullanır.
4. WFF denetleyicisi, üretim ortamındaki Web sunucularını eşitler. Bu, uygulamayı sunucu grubundaki tüm Web sunucularında kullanılabilir hale getirir.

### <a name="how-does-the-deployment-process-work"></a>Dağıtım Işlemi nasıl çalışır?

IIS Yöneticisi, Web paketlerinin bir IIS Web sitesinde yayımlanmasını kolaylaştıran bir uygulama paketi Içeri aktarma Sihirbazı içerir. Bu yordamı gerçekleştirme hakkında yönergeler için bkz. [Web paketlerini el Ile yükleme](../web-deployment-in-the-enterprise/manually-installing-web-packages.md).

## <a name="conclusion"></a>Sonuç

Bu konu, tipik bir kurumsal ölçekte Web uygulaması için dağıtım yaşam döngüsünün bir resmini sağladı.

Bu konu, Web uygulaması dağıtımının çeşitli yönlerine rehberlik sağlayan bir öğretici serisinin bir parçasını oluşturur. Uygulamada, dağıtım sürecinin her aşamasında birçok ek görev ve dikkat edilecek şey vardır ve bunların tümünü tek bir yönergede ele alınması mümkün değildir. Daha fazla bilgi için şu öğreticilere bakın:

- [Kuruluşta Web dağıtımı](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Bu öğreticide, MSBuild ve IIS Web Dağıtım Aracı (Web Dağıtımı) kullanılarak Web Dağıtım teknikleri hakkında kapsamlı bir giriş sunulmaktadır.
- [Web dağıtımı Için sunucu ortamlarını yapılandırma](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). Bu öğretici, çeşitli dağıtım senaryolarını desteklemek üzere Windows Server ortamlarını yapılandırma hakkında rehberlik sağlar.
- [Otomatik Web dağıtımı için Team Foundation Server yapılandırma](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). Bu öğretici, dağıtım mantığını TFS derleme işlemlerine tümleştirme hakkında rehberlik sağlar.
- [Gelişmiş kurumsal Web dağıtımı](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). Bu öğretici, kuruluşların karşılaştığı daha karmaşık dağıtım güçlüklerinden bazılarının nasıl ele alınacağını gösteren yönergeler sağlar.

> [!div class="step-by-step"]
> [Öncekini](enterprise-web-deployment-scenario-overview.md)
