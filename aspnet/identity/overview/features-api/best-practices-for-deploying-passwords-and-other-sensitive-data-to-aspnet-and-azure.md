---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: ASP.NET ve Azure App Service-ASP.NET 4. x ' e parola ve diğer hassas verileri dağıtma
author: Rick-Anderson
description: Bu öğreticide, kodunuzun güvenli bir şekilde nasıl depolayıp erişebileceği hakkında bilgi verilmektedir. En önemli nokta, hiç bir parola veya başka bir sen depolamamalısınız...
ms.author: riande
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8356a90611f791779cc4ff4730038d82cd76242f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457056"
---
# <a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>Parolaların ve diğer hassas verilerin ASP.NET ve Azure App Service’e dağıtılması için en iyi yöntemler

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticide, kodunuzun güvenli bir şekilde nasıl depolayıp erişebileceği hakkında bilgi verilmektedir. En önemli nokta, parolaları veya diğer hassas verileri kaynak kodunda asla depomamalıdır ve geliştirme ve test modunda üretim gizli dizilerini kullanmamanız gerekir.
> 
> Örnek kod, bir veritabanı bağlantı dizesi parolası, Twilio, Google ve SendGrid güvenli anahtarlarına erişmesi gereken basit bir WebJob konsol uygulamasıdır ve bir ASP.NET MVC uygulamasıdır.
> 
> Şirket içi ayarlar ve PHP de bahsedilir.

- [Geliştirme ortamında parolalarla çalışma](#pwd)
- [Geliştirme ortamında bağlantı dizeleriyle çalışma](#con)
- [WebJobs konsol uygulamaları](#wj)
- [Gizli dizileri Azure 'a dağıtma](#da)
- [Şirket Içi ve PHP notları](#not)
- [Ek Kaynaklar](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>Geliştirme ortamında parolalarla çalışma

Öğreticiler, önemli verileri hiçbir şekilde kaynak kodunda depolamadığınızı bir desteklenmediği uyarısıyla ile tam olarak kaynak kodunda gösterir. Örneğin, [SMS ve email 2FA öğreticisi ile ASP.NET MVC 5 uygulaması](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) , *Web. config* dosyasında aşağıdakileri gösterir:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

*Web. config* dosyası kaynak kodudur, bu nedenle bu gizli dizileri hiçbir şekilde bu dosyada depolanmaz. Neyse ki `<appSettings>` öğesi, hassas uygulama yapılandırma ayarları içeren bir dış dosya belirtmenize izin veren bir `file` özniteliğine sahiptir. Dış dosya kaynak ağacınızı denetmadığından, tüm sırlarınızı harici bir dosyaya taşıyabilirsiniz. Örneğin, aşağıdaki biçimlendirmede, *Appsettingsgizlilikler. config* dosyası tüm uygulama gizli dizilerini içerir:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

Dış dosyadaki biçimlendirme (Bu örnekteki*Appsettingsgizlilikler. config* ), *Web. config* dosyasında bulunan işaretlemedir:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

ASP.NET çalışma zamanı, dış dosyanın içeriğini &lt;appSettings&gt; öğesindeki işaretlerle birleştirir. Belirtilen dosya bulunamazsa, çalışma zamanı dosya özniteliğini yok sayar.

> [!WARNING]
> Güvenlik- *gizli dizileri. config* dosyanızı projenize eklemeyin veya kaynak denetimine iade edin. Varsayılan olarak, Visual Studio `Build Action` `Content`olarak ayarlar ve bu da dosyanın dağıtıldığı anlamına gelir. Daha fazla bilgi için bkz. [proje klasörünüzdeki tüm dosyalar nasıl dağıtılır?](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) *Gizli dizi. config* dosyası için herhangi bir uzantıyı kullanabilseniz de, yapılandırma dosyaları IIS tarafından sunulmadığından *. config*' i saklamak en iyisidir. Ayrıca, *Appsettingsgizlilikler. config* dosyasının *Web. config* dosyasından iki dizin düzeyi olduğunu ve bu nedenle çözüm dizininden tamamen tükendiğine dikkat edin. Dosyayı çözüm dizininden taşıyarak git &quot;\*&quot; deponuza eklemez.

<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>Geliştirme ortamında bağlantı dizeleriyle çalışma

Visual Studio, [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)kullanan yeni ASP.NET projeleri oluşturur. LocalDB, özellikle geliştirme ortamı için oluşturulmuştur. Parola gerektirmez, bu nedenle gizli dizileri kaynak kodunuza iade etmelerini engellemek için bir şey yapmanız gerekmez. Bazı geliştirme ekipleri, parola gerektiren SQL Server (veya başka bir DBMS) tam sürümlerini kullanır.

Tüm `<connectionStrings>` işaretlemesini değiştirmek için `configSource` özniteliğini kullanabilirsiniz. Biçimlendirmeyi birleştiren `<appSettings>` `file` özniteliğinin aksine, `configSource` özniteliği biçimlendirmenin yerini alır. Aşağıdaki biçimlendirmede *Web. config* dosyasında `configSource` özniteliği gösterilmektedir:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> Bağlantı dizelerinizi bir dış dosyaya taşımak ve Visual Studio 'Nun yeni bir Web sitesi oluşturmasını sağlamak için yukarıda gösterildiği gibi `configSource` özniteliğini kullanırsanız, bir veritabanı kullandığınızı algılayamaz ve Visual Studio 'dan Azure 'a yayımladığınızda veritabanını yapılandırma seçeneğini almazsınız. `configSource` özniteliğini kullanıyorsanız, Web sitenizi ve veritabanınızı oluşturup dağıtmak için PowerShell kullanabilirsiniz veya yayımlamadan önce Web sitesini ve veritabanını portalda oluşturabilirsiniz. [New-AzureWebsitewithDB. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) betiği yeni bir Web sitesi ve veritabanı oluşturur.

> [!WARNING]
> Güvenlik- *Appsettingsgizlilikler. config* dosyasından farklı olarak, dış bağlantı dizeleri dosyası kök *Web. config* dosyasıyla aynı dizinde olmalıdır, bu yüzden kaynak deponuza iade etmeyin.

> [!NOTE]
> **Gizli dizileri dosyasında güvenlik uyarısı:** En iyi uygulama, test ve geliştirmede üretim gizli dizilerini kullanmamalıdır. Test veya geliştirmede üretim parolalarının kullanılması, bu gizli dizileri sızıntısına neden oluyor.

<a id="wj"></a>
## <a name="webjobs-console-apps"></a>WebJobs konsol uygulamaları

Bir konsol uygulaması tarafından kullanılan *app. config* dosyası göreli yolları desteklemez, ancak mutlak yolları destekler. Gizli dizileri proje dizininizin dışına taşımak için mutlak bir yol kullanabilirsiniz. Aşağıdaki biçimlendirme *C:\secrets\appsettingssecrets.exe* dosyasındaki gizli dizileri ve *app. config* dosyasında hassas olmayan verileri gösterir.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>Gizli dizileri Azure 'a dağıtma

Web uygulamanızı Azure 'a dağıttığınızda, *Appsettingsgizlilikler. config* dosyası dağıtılır (Bu, istediğiniz şeydir). [Azure yönetim portalı](https://azure.microsoft.com/services/management-portal/) giderek bunu el ile ayarlarsanız şunları yapabilirsiniz:

1. [https://portal.azure.com](https://portal.azure.com)gidin ve Azure kimlik bilgilerinizle oturum açın.
2. **&gt; Web Apps**' e tıklayın ve ardından Web uygulamanızın adına tıklayın.
3. **Tüm ayarlar &gt; uygulama ayarları**' na tıklayın.

**Uygulama ayarları** ve **bağlantı dizesi** değerleri, *Web. config* dosyasındaki aynı ayarları geçersiz kılar. Bizim örneğimizde, bu ayarları Azure 'a dağıtmuyoruz, ancak bu anahtarlar *Web. config* dosyasında olsaydı portalda gösterilen ayarlar öncelik kazanır.

En iyi uygulama bir [DevOps iş akışını](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md) takip etmek ve [Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (ya da [Chef](http://www.opscode.com/chef/) veya [pupevcil hayvan](http://puppetlabs.com/puppet/what-is-puppet)gibi başka bir çatı) kullanarak Azure 'da bu değerleri ayarlamayı otomatik hale getirmenizi sağlar. Aşağıdaki PowerShell betiği, şifreli gizli dizileri diske dışarı aktarmak için [Export-CliXml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) kullanır:

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

Yukarıdaki betikte, ' name ', '&quot;FB\_AppSecret&quot; veya "dallı bir sır" gibi gizli anahtarın adıdır. Betik tarafından oluşturulan ". Credential" dosyasını tarayıcınızda görüntüleyebilirsiniz. Aşağıdaki kod parçacığı, kimlik bilgisi dosyalarının her birini sınar ve adlandırılan Web uygulaması için gizli dizileri ayarlar:

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> Güvenlik-PowerShell betiğinin parolalarını veya diğer gizli dizileri eklemeyin. bunu yapmak, hassas verileri dağıtmak için bir PowerShell betiği kullanma amacını erteler. [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet 'i, parola almak için güvenli bir mekanizma sağlar. UI isteminin kullanılması, bir parolanın sızmasını önleyebilir.

### <a name="deploying-db-connection-strings"></a>DB bağlantı dizelerini dağıtma

DB bağlantı dizeleri, uygulama ayarlarına benzer şekilde işlenir. Web uygulamanızı Visual Studio 'dan dağıtırsanız, bağlantı dizesi sizin için yapılandırılır. Bunu portalda doğrulayabilirsiniz. Bağlantı dizesini ayarlamak için önerilen yol PowerShell 'dir. PowerShell betiğinin bir örneği için, bir Web sitesi ve veritabanı oluşturur ve Web sitesindeki bağlantı dizesini ayarlar, [New-AzureWebsitewithDB. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) dosyasını [Azure betik kitaplığı](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)'ndan indirin.

<a id="not"></a>
## <a name="notes-for-php"></a>PHP notları

Hem **uygulama ayarları** hem de **bağlantı dizeleri** için anahtar-değer çiftleri Azure App Service ' de ortam değişkenlerine depolandığından, herhangi bir Web uygulaması çerçevesini (PHP gibi) kullanan geliştiriciler bu değerleri kolayca alabilir. Bkz. Stefan Schackow 'ın [Windows Azure Web siteleri: uygulama dizeleri ve bağlantı dizelerinin nasıl](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) çalıştığı, uygulama ayarlarını ve bağlantı dizelerini okumak IÇIN bir PHP kod parçacığı gösteren blog gönderisi.

## <a name="notes-for-on-premises-servers"></a>Şirket içi sunucular için notlar

Şirket içi Web sunucularına dağıtıyorsanız, [yapılandırma dosyalarının yapılandırma bölümlerini şifreleyerek](https://msdn.microsoft.com/library/ff647398.aspx)gizli dizileri korumaya yardımcı olabilirsiniz. Alternatif olarak, Azure Web siteleri için önerilen aynı yaklaşımı kullanabilirsiniz: yapılandırma dosyalarında geliştirme ayarlarını koruyun ve üretim ayarları için ortam değişkeni değerlerini kullanabilirsiniz. Ancak, bu durumda, Azure Web siteleri 'nde otomatik olan işlevler için uygulama kodu yazmanız gerekir: ortam değişkenlerinden ayarları alın ve bu değerleri yapılandırma dosyası ayarları yerine kullanın veya şu durumlarda yapılandırma dosyası ayarlarını kullanın: ortam değişkenleri bulunamadı.

<a id="addRes"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

Bir Web uygulaması + veritabanı oluşturan bir PowerShell betiğine örnek için, bağlantı dizesi + uygulama ayarları ' nı ayarlar, [New-AzureWebsitewithDB. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) dosyasını [Azure betik kitaplığı](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)'ndan indirin. 

Bkz. Stefan Schackow 'ın [Windows Azure Web siteleri: uygulama dizeleri ve bağlantı dizeleri nasıl çalışır?](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)

İnceleme için özel, Barry Dorrans ( [@blowdart](https://twitter.com/blowdart) ) ve Carlos Farre için teşekkürler.
