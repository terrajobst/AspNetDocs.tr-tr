---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: Her şeyi otomatikleştirin (Azure ile gerçek hayatta bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: e741a753a36ebdaefbff8eee0b38911785c716ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584947"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a>Her şeyi otomatikleştirin (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitaba giriş için [ilk bölüme](introduction.md)bakın.

Tüm yazılım geliştirme projeleri için, ancak özellikle de bulut projelerine uygulanabilecek ilk üç model. Bu model, geliştirme görevlerini otomatikleştirme ile ilgilidir. El ile gerçekleştirilen işlemlerin yavaş ve hataya açık olması nedeniyle önemli bir konudur; mümkün olduğunca çoğunu otomatik hale getirmek, hızlı, güvenilir ve çevik iş akışını ayarlamanıza yardımcı olur. Şirket içi bir ortamda otomatikleştirilmesi zor veya imkansız olan birçok görevi kolayca otomatikleştirebileceğiniz için, bulut geliştirmesi için benzersiz bir öneme sahiptir. Örneğin, yeni Web sunucusu ve arka uç VM 'Leri, veritabanları, BLOB depolama (dosya depolaması), kuyruklar vb. dahil olmak üzere tüm test ortamlarını ayarlayabilirsiniz.

## <a name="devops-workflow"></a>DevOps Iş akışı

Giderek, "DevOps" terimini duydunuz. Yazılım verimli bir şekilde geliştirmek için geliştirme ve işlem görevlerini tümleştirmeniz gereken bir tanımanın geliştirildiği bir terimdir. Etkinleştirmek istediğiniz iş akışı türü, bir uygulama geliştirebileceğiniz, bunu dağıtabileceğiniz, onun üretim kullanımından öğrendiğiniz, öğrendiklerinize yanıt olarak değiştirebileceğiniz ve döngüyü hızlı ve güvenilir bir şekilde tekrarlamanız için tek bir uygulamadır.

Bazı başarılı bulut geliştirme ekipleri, bir günde birden çok kez canlı ortama dağıtılır. Azure ekibi, her 2-3 ayda bir büyük güncelleştirmeyi dağıtmak için kullanılır, ancak şimdi her 2-3 haftada bir 2-3 günde bir ve ana yayınlar için küçük güncelleştirmeleri yayınlar. Bu temposunda e alma, müşteri geri bildirimlerine yanıt almanıza yardımcı olur.

Bunu yapmak için, tekrarlanabilir, güvenilir, öngörülebilir ve süresi düşük olan bir geliştirme ve dağıtım döngüsünü etkinleştirmeniz gerekir.

![DevOps iş akışı](automate-everything/_static/image1.png)

Diğer bir deyişle, bir özellik için bir fikriniz olduğunda ve müşteriler onu kullanırken ve geri bildirim sağlanması mümkün olduğunca kısa olmalıdır. İlk üç desen – her şeyi, kaynak denetimi ve sürekli tümleştirmeyi ve teslimi otomatikleştirin. bu tür bir işlemi etkinleştirmek için önerdiğimiz en iyi yöntemler vardır.

## <a name="azure-management-scripts"></a>Azure Yönetim betikleri

[Bu e-kitaba giriş](introduction.md)bölümünde, Azure yönetim portalı Web tabanlı konsolu gördünüz. Yönetim Portalı, Azure 'da dağıttığınız tüm kaynakları izlemenize ve yönetmenize olanak sağlar. Web uygulamaları ve sanal makineler gibi hizmetleri oluşturup silmenin yanı sıra bu hizmetleri yapılandırmak, hizmet işlemlerini izlemek ve benzeri işlemler için kolay bir yoldur. Harika bir araçtır, ancak kullanmak el ile gerçekleştirilen bir işlemdir. Herhangi bir boyutta bir üretim uygulaması geliştiriyorsanız ve özellikle bir ekip ortamında, Azure 'u öğrenmek ve araştırmak için Portal kullanıcı arabiriminden gidip kaldı yaptığınız işlemleri otomatikleştirebilmeniz önerilir.

Yönetim portalında veya Visual Studio 'da el ile yapabileceğiniz her şey, REST yönetim API 'SI çağırarak da yapılabilir. [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)kullanarak komut dosyaları yazabilir veya [Chef](http://www.opscode.com/chef/) veya [pupevcil hayvan](http://puppetlabs.com/puppet/what-is-puppet)gibi açık kaynak bir çerçeve kullanabilirsiniz. Bash komut satırı aracını bir Mac veya Linux ortamında da kullanabilirsiniz. Azure 'un tüm bu farklı ortamlara yönelik betik API 'Leri vardır ve betik yerine kod yazmak istemeniz durumunda [.NET Yönetim API 'si](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) vardır.

BT BT uygulaması için, bir test ortamı oluşturma ve projeyi bu ortama dağıtma işlemlerini otomatikleştiren bazı Windows PowerShell betikleri oluşturduğumuz ve bu betiklerin bazı içeriğini inceleyeceğiz.

## <a name="environment-creation-script"></a>Ortam oluşturma betiği

Bakacağımız ilk betik, *New-AzureWebsiteEnv. ps1*olarak adlandırılmıştır. BT BT uygulamasını test etmek için dağıtabileceğiniz bir Azure ortamı oluşturur. Bu betiğin gerçekleştirdiği ana görevler şunlardır:

- Bir web uygulaması oluşturun.
- Depolama hesabı oluşturma. (Blob 'lar ve kuyruklar için gereklidir, sonraki bölümlerde göreceğiniz gibi.)
- Bir SQL veritabanı sunucusu ve iki veritabanı oluşturun: bir uygulama veritabanı ve bir üyelik veritabanı.
- Azure 'da, uygulamanın depolama hesabına ve veritabanlarına erişmek için kullanacağı ayarları depolayın.
- Dağıtımı otomatikleştirmek için kullanılacak ayar dosyaları oluşturun.

### <a name="run-the-script"></a>Betiği çalıştırın

> [!NOTE]
> Bu bölümde, betikleri çalıştırmak için girdiğiniz betiklerin ve komutların örnekleri gösterilmektedir. Bu bir demo ve betikleri çalıştırmak için bilmeniz gereken her şeyi sağlamaz. Adım adım nasıl yapılır yönergeleri için bkz. [ek: BT örneğini onarma örnek uygulaması](the-fix-it-sample-application.md#deploybase).

Azure hizmetlerini yöneten bir PowerShell betiğini çalıştırmak için Azure PowerShell konsolunu yüklemeli ve Azure aboneliğinizle çalışacak şekilde yapılandırmalısınız. Ayarladıktan sonra, aşağıdaki gibi bir komutla BT ortamı oluşturma komut dosyasını çalıştırın:

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

`Name` parametresi, veritabanı ve depolama hesapları oluşturulurken kullanılacak adı belirtir ve `SqlDatabasePassword` parametresi, SQL veritabanı için oluşturulacak yönetici hesabının parolasını belirtir. Daha sonra bakabilmemiz için kullanabileceğiniz başka parametreler de vardır.

![PowerShell penceresi](automate-everything/_static/image2.png)

Komut dosyası tamamlandıktan sonra, yönetim portalı 'nda oluşturulan ' de görebilirsiniz. İki veritabanı bulacaksınız:

![Veritabanları](automate-everything/_static/image3.png)

Depolama hesabı:

![Depolama hesabı](automate-everything/_static/image4.png)

Ve bir Web uygulaması:

![Web sitesi](automate-everything/_static/image5.png)

Web uygulamasının **yapılandırma** sekmesinde, BT BT uygulaması için ayarlanan depolama hesabı AYARLARıNA ve SQL veritabanı bağlantı dizelerine sahip olduğunu görebilirsiniz.

![appSettings ve connectionStrings](automate-everything/_static/image6.png)

*Otomasyon* klasörü artık *&lt;bir WebSiteName&gt;. pubxml* dosyası içeriyor. Bu dosya, MSBuild 'in, uygulamayı yeni oluşturulan Azure ortamına dağıtmak için kullanacağı ayarları depolar. Örneğin:

[!code-xml[Main](automate-everything/samples/sample1.xml)]

Gördüğünüz gibi, betik tam bir test ortamı oluşturdu ve tüm işlem yaklaşık 90 saniye içinde yapılır.

Takımınızda başka birisi bir test ortamı oluşturmak istiyorsa, yalnızca betiği çalıştırabilir. Bu yalnızca hızlıdır, ancak aynı zamanda, kullanmakta olduğunuz bir ortamı kullandığından emin olabilirler. Herkesin yönetim portalı Kullanıcı arabirimini kullanarak el ile ayarlama yapacağından emin olmanız gerekir.

### <a name="a-look-at-the-scripts"></a>Betiklerin bir görünümü

Bu işi gerçekleştiren üç komut dosyası vardır. Komut satırından bir tane çağırır ve görevlerden bazılarını yapmak için otomatik olarak diğerini kullanır:

- *New-AzureWebSiteEnv. ps1* , ana betiktir.

    - *New-AzureStorage. ps1* , depolama hesabı oluşturur.
    - *New-AzureSql. ps1* veritabanlarını oluşturur.

### <a name="parameters-in-the-main-script"></a>Ana betikteki parametreler

*New-AzureWebSiteEnv. ps1*ana betiği çeşitli parametreleri tanımlar:

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

İki parametre gereklidir:

- Betiğin oluşturduğu Web uygulamasının adı. (Bu URL için de kullanılır: `<name>.azurewebsites.net`.)
- Veritabanı sunucusunun oluşturduğu yeni yönetici kullanıcı için parola.

İsteğe bağlı parametreler, veri merkezi konumunu (varsayılan olarak "Batı ABD"), veritabanı sunucusu yönetici adını (varsayılan olarak "dbuser") ve veritabanı sunucusu için bir güvenlik duvarı kuralını belirtmenize olanak tanır.

### <a name="create-the-web-app"></a>Web uygulaması oluşturma

Komut dosyası ilk şey, Web uygulaması adı ve konum parametresi değerlerine geçerek `New-AzureWebsite` cmdlet 'ini çağırarak Web uygulamasını oluşturmaktır:

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a>Depolama hesabı oluşturma

Ardından ana betik, depolama hesabı adı için " *&lt;WebSiteName&gt;* Storage" öğesini ve Web uygulamasıyla aynı veri merkezi konumunu belirterek *New-AzureStorage. ps1* betiğini çalıştırır.

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

*New-AzureStorage. ps1* , depolama hesabını oluşturmak için `New-AzureStorageAccount` cmdlet 'ini çağırır ve hesap adını ve erişim anahtarı değerlerini döndürür. Depolama hesabındaki bloblara ve kuyruklara erişmek için uygulamanın bu değerlere ihtiyacı olacaktır.

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

Her zaman yeni bir depolama hesabı oluşturmak istemeyebilirsiniz; isteğe bağlı olarak, var olan bir depolama hesabını kullanmak üzere yönlendiren bir parametre ekleyerek betiği geliştirebilirsiniz.

### <a name="create-the-databases"></a>Veritabanlarını oluşturma

Ana betik daha sonra varsayılan veritabanı ve Güvenlik Duvarı kural adlarını ayarladıktan sonra, *New-AzureSql. ps1*veritabanı oluşturma betiğini çalıştırır:

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

Veritabanı oluşturma betiği, dev makinesinin IP adresini alır ve bir güvenlik duvarı kuralı ayarlayarak geliştirme makinesinin sunucuya bağlanıp yönetmesine izin verebilir. Veritabanı oluşturma betiği daha sonra veritabanlarını ayarlamaya yönelik birkaç adımdan geçer:

- `New-AzureSqlDatabaseServer` cmdlet 'ini kullanarak sunucuyu oluşturur.

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- Geliştirme makinesinin sunucuyu yönetmesini ve Web uygulamasının bu sunucuya bağlanmasını sağlamak için güvenlik duvarı kuralları oluşturur. 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- `New-AzureSqlDatabaseServerContext` cmdlet 'ini kullanarak sunucu adı ve kimlik bilgilerini içeren bir veritabanı bağlamı oluşturur.

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText`, parolayı şifrelemek için `ConvertTo-SecureString` cmdlet 'ini çağıran ve `Get-Credential` cmdlet 'inin döndürdüğü aynı türdeki bir `PSCredential` nesnesi döndüren betikteki bir işlevdir.
- `New-AzureSqlDatabase` cmdlet 'ini kullanarak uygulama veritabanını ve üyelik veritabanını oluşturur.

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- Her veritabanı için bir bağlantı dizesi oluşturmak üzere yerel olarak tanımlanmış bir işlevi çağırır. Uygulama veritabanlarına erişmek için bu bağlantı dizelerini kullanacaktır. 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    Get-SQLAzureDatabaseConnectionString, içinde sağlanan parametre değerlerinden bağlantı dizesini oluşturan betikte tanımlanan bir işlevdir.

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- Veritabanı sunucusu adı ve bağlantı dizelerini içeren bir karma tablo döndürür.

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

BT uygulaması, ayrı üyelik ve uygulama veritabanlarını kullanır. Ayrıca, hem üyelik hem de uygulama verilerinin tek bir veritabanına yerleştirilme olasılığı vardır.

### <a name="store-app-settings-and-connection-strings"></a>Mağaza uygulama ayarları ve bağlantı dizeleri

Azure, Web. config dosyasındaki `appSettings` veya `connectionStrings` koleksiyonlarını okumayı denediğinde uygulamaya döndürülen ayarları ve bağlantı dizelerini otomatik olarak geçersiz kılan bir özelliğe sahiptir. Bu, dağıtırken [Web. config dönüştürmeleri](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) uygulamanın bir alternatifidir. Daha fazla bilgi için bu e-kitapta daha sonra [hassas verileri Azure 'Da depolama](source-control.md#appsettings) bölümüne bakın.

Ortam oluşturma betiği, Azure 'da çalıştığı zaman, uygulamanın depolama hesabına ve veritabanlarına erişmesi gereken tüm `appSettings` ve `connectionStrings` değerlerini depolar.

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

[Yeni relik](http://newrelic.com/) , [izleme ve telemetri](monitoring-and-telemetry.md) bölümünde gösterdiğimiz bir telemetri çerçevesidir. Ortam oluşturma betiği, yeni relik ayarlarını da kullandığından emin olmak için Web uygulamasını yeniden başlatır.

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a>Dağıtım için hazırlanma

İşlemin sonunda, ortam oluşturma betiği dağıtım betiği tarafından kullanılacak dosyaları oluşturmak için iki işlevi çağırır.

Bu işlevlerden biri bir yayımlama profili *(&lt;WebSiteName&gt;. pubxml* dosyası) oluşturur. Kod, yayımlama ayarlarını almak için Azure REST API çağırır ve bilgileri bir *. publishsettings* dosyasına kaydeder. Daha sonra, yayımlama profilini içeren *. pubxml* dosyasını oluşturmak için bu dosyadaki bilgileri bir şablon dosyası (*pubxml. Template*) ile birlikte kullanır. Bu iki adımlı işlem, Visual Studio 'da yapabileceklerinizi taklit ediyor: bir *. publishsettings* dosyası indirip bir yayımlama profili oluşturmak için içeri aktarma.

Diğer işlev, dağıtım betiğinin *. pubxml* dosyası ile birlikte kullanacağı ayarları içeren bir *website-Environment. xml* dosyası oluşturmak için başka bir şablon dosyası (Web sitesi-Environment. Template) kullanır.

### <a name="troubleshooting-and-error-handling"></a>Sorun giderme ve hata işleme

Betikler, programlar gibidir: başarısız olabilirler ve hatanın ne olduğuna ve neden olduğu konusunda ne zaman daha fazla bilgi edinmek istiyorsunuz? Bu nedenle, ortam oluşturma betiği, tüm ayrıntılı iletilerin görüntülenebilmesi için `SilentlyContinue` `VerbosePreference` değişkenin değerini `Continue` olarak değiştirir. Ayrıca, `ErrorActionPreference` değişkeninin değerini `Continue` `Stop`olarak değiştirir, böylece komut dosyası Sonlandırılmamış hatalardan karşılaştığında bile devam eder:

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

Herhangi bir iş yapmadan önce, komut dosyası başlangıç saatini, tamamlandığında geçen süreyi hesaplayabilmesi için depolar:

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

Çalışmayı tamamladıktan sonra, komut dosyası geçen süreyi görüntüler:

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

Her anahtar işlemi için, betik ayrıntılı iletiler yazar, örneğin:

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a>Dağıtım betiği

*New-AzureWebsiteEnv. ps1* betiğinin ortam oluşturma için ne olduğu; *Publish-AzureWebsite. ps1* betiği uygulama dağıtımı için de bunu yapar.

Dağıtım betiği, Web uygulamasının adını ortam oluşturma betiği tarafından oluşturulan *website-Environment. xml* dosyasından alır.

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

*. Publishsettings* dosyasından dağıtım Kullanıcı parolasını alır:

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

Projeyi oluşturup dağıtan [MSBuild](http://msbuildbook.com/) komutunu yürütür:

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

Komut satırında `Launch` parametresini belirttiyseniz, varsayılan tarayıcınızı Web sitesi URL 'sine açmak için `Show-AzureWebsite` cmdlet 'ini çağırır.

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

Dağıtım betiğini şunun gibi bir komutla çalıştırabilirsiniz:

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

Bu işlem tamamlandığında, tarayıcı `<websitename>.azurewebsites.net` URL 'sindeki bulutta çalışan siteyle birlikte açılır.

![Windows Azure 'a dağıtılan BT uygulamasını onarma](automate-everything/_static/image7.png)

## <a name="summary"></a>Özet

Bu betiklerle aynı adımların aynı sırada her zaman aynı şekilde yürütüleceğinden emin olabilirsiniz. Bu, ekipteki her geliştiricinin bir şeyi kaçırmayın veya bir şeyi başka bir ekip üyesinin ortamında veya üretimde aynı şekilde çalışmayan kendi makinesine özel bir şekilde dağıtmamaları için yardımcı olur.

Benzer bir şekilde, REST API, Windows PowerShell betiklerini, .NET dil API 'sini veya Linux veya Mac 'te çalıştırabileceğiniz bir bash yardımcı programını kullanarak yönetim portalında yapabileceğiniz Azure yönetim işlevlerinin çoğunu otomatik hale getirebilirsiniz.

Bir [sonraki bölümde](source-control.md) , kaynak kodu ' na bakacağız ve kendi betiklerinizi kaynak kodu deponuza eklemek için neden önemli olduğunu açıklayacağız.

## <a name="resources"></a>Kaynaklar

- [Azure Için Windows PowerShell 'ı yükleyip yapılandırın](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1). Azure PowerShell cmdlet 'lerinin nasıl yükleneceğini ve Azure hesabınızı yönetmek için bilgisayarınızda ihtiyacınız olan sertifikanın nasıl yükleneceğini açıklar. Bu, Başlarken PowerShell 'in kendisi için kaynaklara bağlantıları da olduğundan başlamak için harika bir yerdir.
- [Azure betik merkezi](https://docs.microsoft.com/azure/automation/automation-runbook-gallery). Azure hizmetlerini yöneten, başlangıç öğreticilerini, cmdlet başvuru belgelerini ve kaynak kodunu ve örnek betikleri içeren Azure hizmetlerini yöneten komut dosyaları geliştirmeye yönelik kaynaklara WindowsAzure.com portalı
- [Hafta sonu Scripter: Azure ve PowerShell Ile çalışmaya](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)başlama. Windows PowerShell 'e adanmış bir blogda bu gönderi, Azure yönetim işlevleri için PowerShell 'i kullanmaya harika bir giriş sağlar.
- [Azure platformlar arası komut satırı arabirimini yükleyip yapılandırın](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest). Mac ve Linux 'ta ve Windows sistemlerine yönelik olarak çalışan bir Azure Scripting çerçevesi için Başlangıç Öğreticisi.
- [Azure SDK 'larını ve araçlarını indirme konusunun komut satırı araçları bölümü](https://azure.microsoft.com/downloads/). Azure için komut satırı araçlarıyla ilgili belge ve indirmeler için Portal sayfası.
- [Azure Yönetim kitaplıkları ve .NET ile her şeyi otomatikleştirme](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Scott Hanselman, Azure için .NET Yönetim API 'sini tanıtır.
- [Geliştirme ve test ortamlarında yayımlamak Için Windows PowerShell betikleri kullanma](https://msdn.microsoft.com/library/azure/dn642480.aspx). Visual Studio 'nun Web projeleri için otomatik olarak oluşturduğu yayımlama betiklerini nasıl kullanacağınızı açıklayan MSDN belgeleri.
- [PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597). Visual Studio 'da Windows PowerShell için dil desteği ekleyen Visual Studio uzantısı.

> [!div class="step-by-step"]
> [Önceki](introduction.md)
> [İleri](source-control.md)
