---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: Dağıtım komut dosyası oluşturma ve çalıştırma | Microsoft Docs
author: jrjlee
description: Bu konuda, Microsoft Build Engine (MSBuild) proje dosyalarını tek adımlı, yeniden... kullanarak bir dağıtımı çalıştırmanıza imkan tanıyan bir komut dosyasının nasıl oluşturulacağı açıklanmaktadır.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634311"
---
# <a name="creating-and-running-a-deployment-command-file"></a>Dağıtım Komut Dosyası Oluşturma ve Çalıştırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, Microsoft Build Engine (MSBuild) proje dosyalarını kullanarak bir dağıtımı tek adımlı, yinelenebilir bir işlem olarak çalıştırmanıza olanak tanıyan bir komut dosyasının nasıl oluşturulacağı açıklanmaktadır.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, WINDOWS COMMUNICATION FOUNDATION&#x2014;(WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager](the-contact-manager-solution.md) çözümünü kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren iki [](understanding-the-build-process.md)proje&#x2014;dosyası tarafından denetlendiği ve ortama özgü derleme ve dağıtım ayarlarını Içeren, derleme işlemini anlama bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="process-overview"></a>İşleme genel bakış

Bu konu başlığında, hedef ortamınıza yinelenebilir bir dağıtım gerçekleştirmek için bu proje dosyalarını kullanan bir komut dosyası oluşturmayı ve çalıştırmayı öğreneceksiniz. Temelde, komut dosyasının yalnızca bir MSBuild komutu içermesi gerekir:

- MSBuild 'in ortam-agstik *Publish. proj* dosyasını yürütmesini söyler.
- *Publish. proj* dosyasına, ortama özgü proje ayarlarını ve nerede bulunacağı dosyayı içerdiğini söyler.

## <a name="create-an-msbuild-command"></a>MSBuild komutu oluşturma

[Derleme işlemini anlama](understanding-the-build-process.md)bölümünde açıklandığı gibi, örneğin,&#x2014; *env-dev. proj*&#x2014;gibi ortama özgü proje dosyası, derleme zamanında ortam belirsiz *Publish. proj* dosyasına aktarılmak üzere tasarlanmıştır. Birlikte, bu iki dosya, çözümünüzü nasıl derleyip dağıtacağınızı söyleyen bir dizi yönerge sağlar.

*Publish. proj* dosyası ortama özgü proje dosyasını içeri aktarmak Için bir **içeri aktarma** öğesi kullanır.

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

Bu nedenle, Contact Manager çözümünü derlemek ve dağıtmak için MSBuild. exe ' yi kullandığınızda şunları yapmanız gerekir:

- *Publish. proj* dosyasında MSBuild. exe ' yi çalıştırın.
- **Targetenvpropsfile**adlı bir komut satırı parametresi sağlayarak ortama özgü proje dosyasının konumunu belirtin.

Bunu yapmak için MSBuild komutunuz şuna benzemelidir:

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

Buradan, yinelenebilir, tek adımlı bir dağıtıma geçiş yapmak için basit bir adımdır. Tek yapmanız gereken, MSBuild komutlarınızı bir. cmd dosyasına eklemektir. Contact Manager çözümünde, Yayımla klasörü, tam olarak bunu yapan *Publish-dev. cmd* adlı bir dosya içerir.

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> **/Fl** anahtarı, MSBuild. exe ' nin çağrıldığı çalışma dizininde *MSBuild. log* adlı bir günlük dosyası oluşturmak için MSBuild 'e bildirir.

Contact Manager çözümünü dağıtmak veya yeniden dağıtmak için tüm yapmanız gereken *Publish-dev. cmd* dosyasını çalıştırmaktır. Dosyayı çalıştırdığınızda MSBuild şu şekilde olur:

- Çözümdeki tüm projeleri derleyin.
- Web uygulaması projeleri için dağıtılabilir Web paketleri oluşturun.
- Veritabanı projeleri için. dbschema ve. DeployManifest dosyaları oluşturun.
- Web paketlerini Web sunucusuna dağıtın.
- Veritabanını veritabanı sunucusuna dağıtın.

## <a name="run-the-deployment"></a>Dağıtımı çalıştırma

Hedef ortamınız için bir komut dosyası oluşturduğunuzda, yalnızca dosyayı çalıştırarak tüm dağıtımı tamamlayabilmelisiniz.

**Iletişim Yöneticisi çözümünü test ortamınıza dağıtmak için**

1. Geliştirici iş istasyonunuzda Windows Gezgini ' ni açın ve *Publish-dev. cmd* dosyasının konumuna gidin.
2. Dosyayı çalıştırmak için çift tıklayın.
3. **Dosya Aç – güvenlik uyarısı** iletişim kutusu görüntülenirse **Çalıştır**' a tıklayın.
4. Yapılandırma ayarlarınız ve test sunucularınız doğru ayarlandıysa, MSBuild proje dosyalarını işlemeyi tamamladığında, komut Istemi penceresinde bir **Yapı başarılı** iletisi gösterilir.

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. Çözümü bu ortama ilk kez dağıttığınız zaman, **ContactManager** veritabanındaki **DB\_datawriter** ve **DB\_DataReader** rollerine test Web sunucusu makine hesabını eklemeniz gerekir. Bu yordam, [Web dağıtımı yayımlama için bir veritabanı sunucusunu yapılandırma](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)bölümünde açıklanmaktadır.

    > [!NOTE]
    > Bu izinleri yalnızca veritabanını oluştururken atamanız gerekir. Varsayılan olarak, derleme işlemi her dağıtımda&#x2014;veritabanını yeniden oluşturmayacak, var olan veritabanını en son şemayla karşılaştırır ve yalnızca gerekli değişiklikleri yapar. Sonuç olarak, yalnızca çözümü ilk kez dağıttığınızda bu veritabanı rollerini eşlemeniz gerekir.
6. Internet Explorer 'ı açın ve Contact Manager uygulamasının URL 'sine gidin (örneğin, `http://testweb1:85/ContactManager/`).
7. Uygulamanın beklendiği gibi çalıştığını ve kişiler ekleyebildiğinizi doğrulayın.

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a>Sonuç

MSBuild yönergelerinizi içeren bir komut dosyası oluşturmak, belirli bir hedef ortama çok projeli bir çözüm oluşturmanın ve dağıtmanın hızlı ve kolay bir yolunu sağlar. Çözümünüzü birden çok hedef ortama tekrar tekrar dağıtmanız gerekiyorsa, birden çok komut dosyası oluşturabilirsiniz. Her komut dosyasında, MSBuild komutu aynı evrensel proje dosyasını oluşturur, ancak ortama özgü farklı bir proje dosyası belirtir. Örneğin, bir geliştirici veya test ortamında yayımlanacak bir komut dosyası bu MSBuild komutunu içerebilir:

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

Hazırlama ortamında yayımlanacak bir komut dosyası bu MSBuild komutunu içerebilir:

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> Kendi sunucu ortamlarınız için ortama özgü proje dosyalarını özelleştirmeye ilişkin yönergeler için bkz. [hedef ortam Için dağıtım özelliklerini yapılandırma](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

Ayrıca, MSBuild komutlarınızda özellikleri geçersiz kılarak veya farklı anahtarlar ayarlayarak her bir ortam için yapı işlemini özelleştirebilirsiniz. Daha fazla bilgi için bkz. [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311.aspx).

> [!div class="step-by-step"]
> [Önceki](deploying-database-projects.md)
> [İleri](manually-installing-web-packages.md)
