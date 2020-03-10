---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: MSBuild proje dosyalarından Windows PowerShell betikleri çalıştırma | Microsoft Docs
author: jrjlee
description: Bu konu, bir Windows PowerShell betiğini derleme ve dağıtım sürecinin bir parçası olarak nasıl çalıştıracağınızı açıklar. Bir betiği yerel olarak (diğer bir deyişle, b üzerinde) çalıştırabilirsiniz.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548512"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>MSBuild Proje Dosyalarından Windows PowerShell Betikleri Çalıştırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, bir Windows PowerShell betiğini derleme ve dağıtım sürecinin bir parçası olarak nasıl çalıştıracağınızı açıklar. Bir betiği yerel olarak (diğer bir deyişle, yapı sunucusunda) veya uzaktan bir hedef Web sunucusu ya da veritabanı sunucusu gibi uzak bir şekilde çalıştırabilirsiniz.
> 
> Dağıtım sonrası bir Windows PowerShell Betiği çalıştırmak isteyebileceğiniz birçok neden vardır. Örneğin, şunları yapmak isteyebilirsiniz:
> 
> - Kayıt defterine özel bir olay kaynağı ekleyin.
> - Karşıya yüklemeler için bir dosya sistemi dizini oluşturun.
> - Yapı dizinlerini temizleyin.
> - Girişleri özel bir günlük dosyasına yazın.
> - Kullanıcıları yeni sağlanan bir Web uygulamasına davet eden e-postalar gönderin.
> - Uygun izinlere sahip kullanıcı hesapları oluşturun.
> - SQL Server örnekleri arasında çoğaltmayı yapılandırın.
> 
> Bu konu, bir Microsoft Build Engine (MSBuild) proje dosyasındaki özel bir hedeften yerel olarak ve Uzaktan Windows PowerShell betiklerini nasıl çalıştıracağınızı gösterir.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="task-overview"></a>Göreve genel bakış

Bir Windows PowerShell betiğini otomatik veya tek adımlı dağıtım sürecinin bir parçası olarak çalıştırmak için, bu üst düzey görevleri gerçekleştirmeniz gerekir:

- Windows PowerShell betiğini çözümünüze ve kaynak denetimine ekleyin.
- Windows PowerShell betiğinizi çağıran bir komut oluşturun.
- Komutunuz tüm ayrılmış XML karakterlerini kaçış.
- Özel MSBuild proje dosyanızda bir hedef oluşturun ve komutunu çalıştırmak için **Exec** görevini kullanın.

Bu konu başlığı altında, bu yordamların nasıl gerçekleştirileceği gösterilmektedir. Bu konudaki görevler ve izlenecek yollar, MSBuild hedefleri ve özellikleri hakkında zaten bilgi sahibi olduğunuzu ve bir derleme ve dağıtım işlemini sağlamak için özel bir MSBuild proje dosyası kullanmayı anladığınızı varsayar. Daha fazla bilgi için bkz. [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md) ve [derleme sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

## <a name="creating-and-adding-windows-powershell-scripts"></a>Windows PowerShell betikleri oluşturma ve ekleme

Bu konudaki görevler, MSBuild 'ten komut dosyalarının nasıl çalıştırılacağını göstermek için **Logdeploy. ps1** adlı örnek bir Windows PowerShell betiği kullanır. **Logdeploy. ps1** betiği, bir günlük dosyasına tek satırlık bir girdi yazan basit bir işlev içerir:

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

**Logdeploy. ps1** betiği iki parametreyi kabul eder. İlk parametre, giriş eklemek istediğiniz günlük dosyasının tam yolunu temsil eder ve ikinci parametre günlük dosyasında kaydetmek istediğiniz dağıtım hedefini temsil eder. Betiği çalıştırdığınızda bu biçimdeki günlük dosyasına bir satır ekler:

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

**Logdeploy. ps1** betiğini MSBuild için kullanılabilir hale getirmek için şunları yapmanız gerekir:

- Betiği kaynak denetimine ekleyin.
- Visual Studio 2010 ' de çözümünüze betiği ekleyin.

Betiği derleme sunucusunda mi yoksa uzak bir bilgisayarda mı çalıştırmayı planladığınızdan bağımsız olarak çözüm içeriklerinizi dağıtmanız gerekmez. Bir seçenek, betiği bir çözüm klasörüne eklemektir. Iletişim Yöneticisi örneğinde, dağıtım işleminin bir parçası olarak Windows PowerShell betiğini kullanmak istiyorsanız, betiği Publish Solution klasörüne eklemek mantıklı olur.

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

Çözüm klasörlerinin içerikleri, derleme sunucularına kaynak malzeme olarak kopyalanır. Ancak, herhangi bir proje çıkışının hiçbir parçasını oluşturmazlar.

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>Yapı sunucusunda Windows PowerShell betiği yürütme

Bazı senaryolarda, projelerinizi oluşturan bilgisayarda Windows PowerShell betikleri çalıştırmak isteyebilirsiniz. Örneğin, yapı klasörlerini temizlemek veya girdileri özel bir günlük dosyasına yazmak için bir Windows PowerShell betiği kullanabilirsiniz.

Sözdizimi açısından, bir MSBuild proje dosyasından Windows PowerShell betiğini çalıştırmak, düzenli bir komut isteminden bir Windows PowerShell betiği çalıştırma ile aynıdır. PowerShell. exe yürütülebilir dosyasını çağırmanız ve Windows PowerShell 'in çalıştırmasını istediğiniz komutları sağlamak için **– komut** anahtarını kullanmanız gerekir. (Windows PowerShell V2 'de, **– File** anahtarını da kullanabilirsiniz). Komutun şu biçimde olması gerekir:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

Örneğin:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

Betiğinizin yolu boşluk içeriyorsa, dosya yolunu tek tırnak içine almanız gerekir. Şu komutu içerecek şekilde zaten kullanmış olduğunuzdan çift tırnak işareti kullanamazsınız:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

MSBuild 'ten bu komutu çağırdığınızda dikkat etmeniz gereken bazı ek durumlar vardır. İlk olarak, komut dosyasının sessizce yürütüldüğünü sağlamak için **– etkileşimsiz** bayrağını dahil etmelisiniz. Ardından, **– ExecutionPolicy** bayrağını uygun bir bağımsız değişken değeriyle birlikte eklemeniz gerekir. Bu, Windows PowerShell 'in betiğinizi uygulayabileceği Yürütme ilkesini belirtir ve varsayılan yürütme ilkesini geçersiz kılmanızı sağlar. Bu, betiğinizin yürütülmesini engelleyebilir. Bu bağımsız değişken değerleri arasından seçim yapabilirsiniz:

- **Kısıtlanmamış** bir değer, komut dosyasının imzalanıp Imzalanmadığına bakılmaksızın Windows PowerShell 'in betiğinizi yürütmesine izin verir.
- **RemoteSigned** değeri, Windows PowerShell 'in yerel makinede oluşturulan imzasız betikleri yürütmesine izin verir. Ancak, başka bir yerde oluşturulan betikler imzalanmalıdır. (Uygulamada, bir yapı sunucusunda yerel olarak bir Windows PowerShell betiği oluşturmuş olmanız çok düşüktür).
- **AllSigned** değeri, Windows PowerShell 'in yalnızca imzalı betikleri yürütmesine izin verir.

Varsayılan yürütme ilkesi, Windows PowerShell 'in herhangi bir betik dosyasını çalıştırmasını önleyen **kısıtlanmıştır**.

Son olarak, Windows PowerShell komutunuz içinde oluşan tüm ayrılmış XML karakterlerini atlamanız gerekir:

- Tek tırnak **&amp;apos;** ile Değiştir
- Çift tırnak **&amp;quot;** ile Değiştir
- Yer işaretleri **&amp;amp** ile Değiştir

- Bu değişiklikleri yaptığınızda komutunuz şuna benzeyecektir:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

Özel MSBuild proje dosyanız içinde, yeni bir hedef oluşturabilir ve bu komutu çalıştırmak için **Exec** görevini kullanabilirsiniz:

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

Bu örnekte şunları unutmayın:

- Parametre değerleri ve Windows PowerShell yürütülebilir dosyasının konumu gibi tüm değişkenler, MSBuild özellikleri olarak bildirilmiştir.
- Kullanıcıların bu değerleri komut satırından geçersiz kılmasını sağlamak için koşullar dahildir.
- **Msdeploycomputername** özelliği proje dosyasında başka bir yerde bildirilmiştir.

Yapı işleminizin bir parçası olarak bu hedefi yürüttüğünüzde, Windows PowerShell, komutunuzu çalıştırır ve belirttiğiniz dosyaya bir günlük girdisi yazar.

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>Uzak bilgisayarda Windows PowerShell betiğini yürütme

Windows PowerShell, [Windows Uzaktan Yönetimi](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM) aracılığıyla uzak bilgisayarlarda komut dosyalarını çalıştırabilme özelliğine sahiptir. Bunu yapmak için [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet 'ini kullanmanız gerekir. Bu, betiği uzak bilgisayarlara kopyalamadan bir veya daha fazla uzak bilgisayara karşı komut dosyanızı yürütmenize olanak sağlar. Tüm sonuçlar, betiği çalıştırdığınız yerel bilgisayara döndürülür.

> [!NOTE]
> Windows PowerShell komut dosyalarını uzak bir bilgisayarda yürütmek için **Invoke-Command** cmdlet 'ini kullanmadan önce, uzak iletileri kabul etmek Için bir WinRM dinleyicisi yapılandırmanız gerekir. Bunu, uzak bilgisayarda **winrm quickconfig** komutunu çalıştırarak yapabilirsiniz. Daha fazla bilgi için bkz. [Windows Uzaktan Yönetimi Için yükleme ve yapılandırma](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).

Bir Windows PowerShell penceresinden, uzak bir bilgisayarda **Logdeploy. ps1** betiğini çalıştırmak için bu sözdizimini kullanın:

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> Komut dosyasını çalıştırmak için **Invoke-Command** kullanmanın farklı diğer yolları vardır ancak bu yaklaşım, parametre değerleri sağlamanız ve boşluklar içeren yolları yönetmeniz gerektiğinde en basittir.

Bunu bir komut isteminden çalıştırdığınızda, Windows PowerShell yürütülebilirini çağırmanız ve yönergelerinizi sağlamak için **– komut** parametresini kullanmanız gerekir:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

Daha önce olduğu gibi, MSBuild 'ten komutunu çalıştırdığınızda bazı ek anahtarlar sağlamanız ve ayrılmış XML karakterlerinin önüne kaçış yapmanız gerekir:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

Son olarak, daha önce olduğu gibi, komutunu yürütmek için özel bir MSBuild hedefi içindeki **Exec** görevini kullanabilirsiniz:

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

Yapı işleminizin bir parçası olarak bu hedefi yürüttüğünüzde, Windows PowerShell, komut dosyanızı **– ComputerName** bağımsız değişkeninde belirttiğiniz bilgisayarda çalıştırır.

## <a name="conclusion"></a>Sonuç

Bu konu, bir MSBuild proje dosyasından Windows PowerShell komut dosyasının nasıl çalıştırılacağını açıklamaktadır. Bu yaklaşımı, bir otomatik veya tek adımlı derleme ve dağıtım sürecinin bir parçası olarak yerel olarak veya uzak bir bilgisayarda Windows PowerShell betiğini çalıştırmak için kullanabilirsiniz.

## <a name="further-reading"></a>Daha Fazla Bilgi

Windows PowerShell betikleri imzalama ve yürütme ilkelerini yönetme hakkında rehberlik için bkz. [Windows PowerShell betiklerini çalıştırma](https://technet.microsoft.com/library/ee176949.aspx). Windows PowerShell komutlarını uzak bir bilgisayardan çalıştırmaya ilişkin yönergeler için bkz. [uzak komutları çalıştırma](https://technet.microsoft.com/library/dd819505.aspx).

Dağıtım işlemini denetlemek için özel MSBuild proje dosyalarını kullanma hakkında daha fazla bilgi için bkz. [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md) ve [derleme sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

> [!div class="step-by-step"]
> [Önceki](taking-web-applications-offline-with-web-deploy.md)
> [İleri](troubleshooting-the-packaging-process.md)
