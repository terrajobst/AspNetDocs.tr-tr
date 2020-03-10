---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: What If dağıtımı gerçekleştirme | Microsoft Docs
author: jrjlee
description: Bu konu, Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) ve V... kullanarak ' ne tür ' (veya benzetimli) dağıtımların nasıl gerçekleştirileceğini açıklamaktadır.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628893"
---
# <a name="performing-a-what-if-deployment"></a>Sınama Dağıtımı Gerçekleştirme

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) ve VSDBCMD kullanarak "ne tür" (veya benzetimli) dağıtımların nasıl gerçekleştirileceğini açıklamaktadır. Bu, uygulamanızı dağıtmadan önce belirli bir hedef ortamda dağıtım mantığınızın etkilerini belirlemenizi sağlar.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme ve dağıtım sürecinin, her hedef ortam için uygulanan derleme yönergelerini içeren iki proje&#x2014;dosyası tarafından denetlendiği ve ortama özgü derleme ve dağıtım ayarlarını içeren, proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="performing-a-what-if-deployment-for-web-packages"></a>Web paketleri için "What If" dağıtımını gerçekleştirme

Web Dağıtımı, "durum" (veya deneme) modunda dağıtım gerçekleştirmenize olanak tanıyan işlevselliği içerir. Yapıtları "ne tür" modda dağıtırken, Web Dağıtımı dağıtımı gerçekleştirdiyseniz bir günlük dosyası oluşturur, ancak aslında hedef sunucuda herhangi bir şeyi değiştirmez. Günlük dosyasını gözden geçirmek, dağıtımınızın hedef sunucuda sahip olacağı etkiyi özellikle anlamanıza yardımcı olabilir:

- Ne eklenir.
- Nelerin güncelleştirileceği.
- Ne silinecek?

"Durum" dağıtımı aslında hedef sunucudaki herhangi bir şeyi değiştirmezse, her zaman ne yapamayacağı, dağıtımın başarılı olup olmayacağını tahmin etmez.

[Web paketlerini dağıtma](../web-deployment-in-the-enterprise/deploying-web-packages.md)bölümünde açıklandığı gibi, doğrudan MSDeploy. exe komut satırı yardımcı programını kullanarak veya&#x2014;yapı işleminin oluşturduğu *. deploy. cmd* dosyasını çalıştırarak, Web dağıtımı kullanarak Web Paketleri dağıtabilirsiniz.

MSDeploy. exe dosyasını doğrudan kullanıyorsanız, Komutunuz için **– whatIf** bayrağını ekleyerek bir "ne tür" dağıtımı çalıştırabilirsiniz. Örneğin, ContactManager. Mvc. zip paketini bir hazırlama ortamına dağıttıysanız ne olacağını değerlendirmek için MSDeploy komutu şuna benzemelidir:

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

"Ne tür" dağıtımının sonuçlarını karşıladığınızda, bir canlı dağıtımı çalıştırmak için **– whatIf** bayrağını kaldırabilirsiniz.

> [!NOTE]
> MSDeploy. exe için komut satırı seçenekleri hakkında daha fazla bilgi için, [Web dağıtımı Işlem ayarları](https://technet.microsoft.com/library/dd569089(WS.10).aspx)' na bakın.

*. Deploy. cmd* dosyasını kullanıyorsanız, komutinizdeki **/y** bayrağı ("Evet," veya güncelleştirme modu) yerine **/t** bayrağını (deneme modu) ekleyerek bir "ne tür" dağıtımı çalıştırabilirsiniz. Örneğin, *. deploy. cmd* dosyasını çalıştırarak ContactManager. Mvc. zip paketini dağıttıysanız ne olacağını değerlendirmek için, komutunuz şuna benzemelidir:

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

"Deneme modu" dağıtımınızın sonuçlarını karşıladığınızda, bir Live Deployment çalıştırmak için **/t** bayrağını bir **/y** bayrağıyla değiştirebilirsiniz:

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> *. Deploy. cmd* dosyaları için komut satırı seçenekleri hakkında daha fazla bilgi için bkz. [nasıl yapılır: dağıtım paketini Deploy. cmd dosyasını kullanarak oluşturma](https://msdn.microsoft.com/library/ff356104.aspx). Herhangi bir bayrak belirtmeden *. deploy. cmd* dosyasını çalıştırırsanız, komut istemi kullanılabilir bayrakların bir listesini görüntüler.

## <a name="performing-a-what-if-deployment-for-databases"></a>Veritabanları için "What If" dağıtımını gerçekleştirme

Bu bölümde, artımlı, şema tabanlı veritabanı dağıtımı gerçekleştirmek için VSDBCMD yardımcı programını kullandığınız varsayılır. Bu yaklaşım, [veritabanı projelerini dağıtma](../web-deployment-in-the-enterprise/deploying-database-projects.md)konusunda daha ayrıntılı olarak açıklanmıştır. Burada açıklanan kavramları uygulamadan önce bu konuyu öğrenmeniz önerilir.

**Dağıtım** modunda VSDBCMD kullandığınızda, VSDBCMD 'nin gerçekten veritabanını dağıtıp dağıtmadığını denetlemek için **/dd** (veya **/DeployToDatabase**) bayrağını kullanabilirsiniz veya yalnızca bir dağıtım betiği oluşturur. Bir. dbschema dosyası dağıtıyorsanız, bu davranış şu şekilde yapılır:

- **/Dd +** veya **/dd**belirtirseniz, VSDBCMD bir dağıtım betiği oluşturacak ve veritabanını dağıtacaktır.
- **/DDI** belirtirseniz veya anahtarı atlarsanız, VSDBCMD yalnızca bir dağıtım betiği oluşturacaktır.

> [!NOTE]
> . Dbschema dosyası yerine. DeployManifest dosyası dağıtıyorsanız, **/dd** anahtarının davranışı çok daha karmaşıktır. Temelde,. DeployManifest dosyası **true**değerine sahip bir **DeployToDatabase** öğesi içeriyorsa, VSDBCMD, **/dd** anahtarının değerini yoksayar. [Veritabanı projelerini dağıtmak](../web-deployment-in-the-enterprise/deploying-database-projects.md) bu davranışı tam olarak açıklar.

Örneğin, veritabanının gerçekten dağıtımı yapılmadan **ContactManager** veritabanı için bir dağıtım betiği oluşturmak üzere VSDBCMD komutunuz şuna benzemelidir:

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

VSDBCMD, bir fark veritabanı dağıtım aracıdır ve bu nedenle dağıtım betiği, mevcut veritabanını (varsa) belirtilen şemaya güncelleştirmek için gereken tüm SQL komutlarını içerecek şekilde dinamik olarak oluşturulur. Dağıtım betiğini gözden geçirmek, dağıtımınızın geçerli veritabanında ve içerdiği verilerde hangi etkiyi kullanacağını belirlemek için kullanışlı bir yoldur. Örneğin, şunları öğrenmek isteyebilirsiniz:

- Mevcut tabloların kaldırılıp kaldırılmayacağı ve bunun veri kaybına neden olup olmadığı.
- Örneğin, tabloları böyor veya birleştiriyorsanız, işlem sırasının veri kaybı riski olup olmadığı.

Dağıtım betiğiyle memnunsanız, değişiklikleri yapmak için VSDBCMD 'yi bir **/dd +** bayrağıyla yineleyebilirsiniz. Alternatif olarak, gereksinimlerinizi karşılayacak şekilde dağıtım betiğini düzenleyebilir ve ardından veritabanı sunucusunda el ile yürütebilirsiniz.

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>"What If" Işlevselliğini özel proje dosyalarıyla tümleştirme

Daha karmaşık dağıtım senaryolarında, derleme ve dağıtım mantığınızı kapsüllemek için, [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklandığı gibi özel bir Microsoft Build Engine (MSBuild) proje dosyası kullanmak isteyeceksiniz. Örneğin, [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) örnek çözümünde *Publish. proj* dosyası:

- Çözümü oluşturur.
- ContactManager. Mvc uygulamasını paketlemek ve dağıtmak için Web Dağıtımı kullanır.
- ContactManager. Service uygulamasını paketlemek ve dağıtmak için Web Dağıtımı kullanır.
- **ContactManager** veritabanını dağıtır.

Birden çok Web paketi ve/veya veritabanının dağıtımını bu şekilde tek adımlı bir işlemle tümleştirdiğinizde, tüm dağıtımı bir "işlem" modunda gerçekleştirme seçeneğini de isteyebilirsiniz.

*Publish. proj* dosyası bunu nasıl yapabileceğinizi gösterir. İlk olarak, "durum" değerini depolamak için bir özellik oluşturmanız gerekir:

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

Bu durumda, varsayılan değeri **false**olan **whatIf** adlı bir özellik oluşturdunuz. Bu değeri, kısa süre içinde göreceğiniz gibi, bir komut satırı parametresinde özelliği **true** olarak ayarlayarak geçersiz kılabilir.

Sonraki aşama, bayrakların **whatIf** özellik değerini yansıtması için Web dağıtımı ve VSDBCMD komutlarının parametreleştiriyor. Örneğin, bir sonraki hedef ( *Publish. proj* dosyasından alınan ve Basitleştirilmiş), bir Web paketini dağıtmak için *. deploy. cmd* dosyasını çalıştırır. Varsayılan olarak, komut bir **/y** anahtarı ("Yes" veya Update Mode) içerir. **WhatIf** değeri **true**olarak ayarlanırsa, bu, bir **/t** anahtarıyla (deneme veya "ne tür" mod) ile değiştirilmiştir.

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

Benzer şekilde, bir sonraki hedef, bir veritabanını dağıtmak için VSDBCMD yardımcı programını kullanır. Varsayılan olarak, bir **/dd** anahtarı dahil edilmez. Bu, VSDBCMD 'nin bir dağıtım betiği üretebileceği ancak veritabanını&#x2014;başka bir deyişle "bir if" senaryosunda dağıtmayacak anlamına gelir. **WhatIf** özelliği **true**olarak ayarlanmamışsa, bir **/dd** anahtarı eklenir ve VSDBCMD veritabanını dağıtır.

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

Proje dosyanızdaki ilgili tüm komutları parametreleştirmek için aynı yaklaşımı kullanabilirsiniz. "Ne tür" dağıtımı çalıştırmak istediğinizde, komut satırından yalnızca bir **whatIf** Özellik değeri sağlayabilirsiniz:

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

Bu şekilde, tüm proje bileşenleriniz için bir "ne tür" dağıtımını tek bir adımda çalıştırabilirsiniz.

## <a name="conclusion"></a>Sonuç

Bu konu, Web Dağıtımı, VSDBCMD ve MSBuild kullanılarak "ne tür" dağıtımlar çalıştırmayı açıklamaktadır. "Ne yapılır" dağıtımı, hedef ortamda herhangi bir değişiklik yapmadan önce önerilen bir dağıtımın etkisini değerlendirmenize imkan tanır.

## <a name="further-reading"></a>Daha Fazla Bilgi

Web Dağıtımı komut satırı sözdizimi hakkında daha fazla bilgi için bkz. [Web dağıtımı Işlem ayarları](https://technet.microsoft.com/library/dd569089(WS.10).aspx). *. Deploy. cmd* dosyasını kullanırken komut satırı seçeneklerine ilişkin yönergeler için bkz. [nasıl yapılır: dağıtım paketini Deploy. cmd dosyasını kullanarak kullanma](https://msdn.microsoft.com/library/ff356104.aspx). VSDBCMD komut satırı söz dizimi hakkında yönergeler için bkz [. VSDBCMD Için komut satırı başvurusu. EXE (dağıtım ve şema Içeri aktarma)](https://msdn.microsoft.com/library/dd193283.aspx).

> [!div class="step-by-step"]
> [Önceki](advanced-enterprise-web-deployment.md)
> [İleri](customizing-database-deployments-for-multiple-environments.md)
