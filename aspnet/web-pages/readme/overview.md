---
uid: web-pages/readme/overview
title: WebMatrix Benioku | Microsoft Docs
author: rick-anderson
description: WebMatrix ve ASP.NET Web Pages (Razor) 1,0 yayın Benioku dosyası
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563471"
---
# <a name="webmatrix-readme"></a>WebMatrix Benioku dosyası

13 Ocak 2011

## <a name="contents"></a>İçindekiler

> [!NOTE]
> Bu benioku, WebMatrix 'in 1,0 sürümü için geçerlidir.

- [Genel bakış](#Overview)
- [Yükleme](#Installation_Notes)
- [Uygulamaları yayımlama](#InstructionsForPublishingApplications)
- [Değişiklikler ve sorunlar](#ChangesAndIssues)

    - [WebMatrix 1,0 yüklemesi](#Known_Issues_Installation)
    - [ASP.NET Web Sayfaları](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [Uygulamaları yükleme](#Known_Issues_Installing_Applications)
    - [Uygulamaları yayımlama](#Known_Issues_Publishing_Applications)
- [Daha fazla bilgi için](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>Genel bakış

> Microsoft WebMatrix 1,0, dakikalar içinde yüklenen ücretsiz bir Web geliştirme yığınıdır. Tek ve tümleşik bir deneyim oluşturmak için veritabanı ve programlama çerçeveleri ile bir Web sunucusunu tümleştirir. WebMatrix kullanarak kendi ASP.NET veya PHP Web sitenizi kodlayın, test edin ve yayımlayın ya da DotNetNuke, dönen Raco, WordPress veya Joomla gibi popüler açık kaynaklı uygulamaları kullanarak yeni bir Web sitesini başlatmak için WebMatrix 'i kullanabilirsiniz. WebMatrix, Web sitenizi Internet üzerinde çalıştıracak olan güçlü Web sunucusu, veritabanı altyapısı ve çerçeveler ortamını kullanır. Bu, geliştirmeden üretime sorunsuz ve sorunsuz bir şekilde geçiş yapar.

<a id="Installation_Notes"></a>

## <a name="installation"></a>Yükleme

> WebMatrix 1,0 ' ü yüklemek için, ilk olarak [Microsoft Web Platformu Yükleyicisi 3,0](https://go.microsoft.com/fwlink/?LinkID=194638)' ü yüklemeniz gerekir. Web Platformu Yükleyicisi 'ni yükledikten sonra WebMatrix 'i yüklemek için bu uygulamayı kullanabilirsiniz.
> 
> Yükleme sırasında sorunlarla karşılaşırsanız [Microsoft Web Platformu Yükleyicisi sorun giderme sorunları](https://go.microsoft.com/fwlink/?LinkId=196212)bölümüne bakın.

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>Uygulamaları yayımlama

> Bkz. [uygulamaları yayımlamak Için adım adım yönergeler](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>Değişiklikler ve sorunlar

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>WebMatrix 1,0 yükleme sorunları

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>Sorun: WebMatrix 1,0 yalnızca Microsoft .NET Framework 4 ' ü destekleyen platformlarda kullanılabilir

> WebMatrix için .NET Framework sürüm 4 gerekir. Bazı durumlarda, WebMatrix 1,0 yükleyicisi, desteklenen yapılandırma kümesinin parçası olmayan bir platforma yükleme denemenize imkan tanır. Özellikle, SP1 güncelleştirmesi olmayan Windows Vista, WebMatrix yüklemesine başlamanızı sağlar, ancak .NET Framework 4 bileşeni başarısız olur ve yüklemenizi engeller.
> 
> **Geçici çözüm**  
> Aşağıdakileri içeren desteklenen bir platforma yükler:
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 veya sonraki sürümü
> - Windows XP SP3
> - Windows Server 2003 SP2

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>Sorun: Microsoft Visual Studio 2008 SP1 olmadan Microsoft Visual Studio 2008 yüklenirse WebMatrix 1,0 yüklenemiyor

> **Geçici çözüm**  
> [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 'ı Microsoft İndirme Merkezi ' nden yükleyin.

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>Sorun: SQL Server Compact 4,0 için bazı derlemeler GAC 'de yüklü değil

> SQL Server Compact 4,0 için yönetilen derlemeler, SQL Server Compact 4,0 ' i bir 64 bit bilgisayara yüklediğinizde ve bilgisayarda yalnızca .NET Framework 3,5 SP1 Istemci profili yüklü olduğunda genel derleme önbelleği 'ne (GAC) yerleştirilmez. GAC 'de yüklü olmayan yönetilen derlemeler şunlardır:
> 
> - *System. Data. SqlServerCe. dll* (ADO.NET sağlayıcısı)
> - *System. Data. SqlServerCe. Entity. dll* (ADO.NET Entity Framework)
> 
> **Geçici çözüm**  
> SQL Server Compact 4,0 'yi kaldırın. Aşağıdaki konumdan .NET Framework 3,5 SP1 'in tam sürümünü indirip yükleyin:  
>   
> [Microsoft .NET Framework 3,5 Service Pack 1 (tam paket)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> SQL Server Compact 4,0 yeniden yükleyin.

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>Sorun: komut satırı kullanılarak SQL Server Compact kaldırılamıyor

> Komut satırı seçeneklerini kullanarak SQL Server Compact kaldırılması bu sürümde çalışmaz.
> 
> **Geçici çözüm**  
> 4,0 Microsoft SQL Server Compact kaldırmak için Windows Denetim Masası 'ndaki *Programlar ve Özellikler ' i* kullanın.

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET Web Sayfaları

Belgenin bu bölümünde, Razor söz dizimi ile ASP.NET Web sayfalarının 1,0 sürümündeki yeni özellikler, değişiklikler ve bilinen sorunlar açıklanmaktadır.

- [Yeni özellikler](#NewFeatures)
- [Değişikliklerine](#Changes)
- [Sorunlar](#Issues)

#### <a id="NewFeatures"></a>Yeni özellikler

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>Yeni: paket yöneticisini devre dışı bırakmak için yapılandırma ayarı eklendi

> *Web. config* dosyasındaki `<appSettings>` öğesi için yeni bir `asp:AdminManagerEnabled` anahtarı vardır ve bu, paket yöneticisini tamamen devre dışı bırakmanızı sağlar. Bu öğe için varsayılan değer true 'dur, yani *Web. config* dosyasına dahil edilmediğinde, Paket Yöneticisi etkindir. Paket yöneticisini devre dışı bırakmak için, aşağıdaki öğeyi Web sitesinin kökündeki *Web. config* dosyasına ekleyin:
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>Değişikliklerine

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>Değişiklik: "Web sayfaları: AdminFolderVirtualPath" anahtarı "ASP: AdminFolderVirtualPath" olarak yeniden adlandırıldı

> Paket yöneticisinin konumunu belirtmek için *Web. config* dosyasına eklenebilen `webPages:AdminFolderVirtualPath` anahtarı, `webPages` ad alanı yerine `asp:` ad alanını kullanacak şekilde yeniden adlandırıldı. Bu öğeyi kullandıysanız yapılandırma dosyasında yeniden adlandırmanız gerekir.

#### <a id="Issues"></a> Bilinen Sorunlar

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>Sorun: üyelik kullanıcıları için parolalar artık tanınmıyor

> Üyelik (oturum açma) parolalarının oluşturulması ve depolanması için algoritma daha güvenli olacak şekilde değiştirildi. Sonuç olarak, ASP.NET Razor 'nin Beta sürümlerinde oluşturulan Üyeler (kullanıcılar) için depolanan parolalar tanınmaz. 
> 
> **Geçici çözüm** Site henüz üretime yerleştirmemişse, Kullanıcı kayıtlarını üyelik veritabanından kaldırın. Veritabanı canlı ise, üyelik veritabanındaki mevcut parolaları program aracılığıyla yeniden oluşturun.

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>Sorun: üyelik için özel bir kullanıcı tablosu kullanılırken beklenmeyen davranış

> Bir ASP.NET Razor Web sitesinin üyelik sağlayıcısını başlatmak için `WebSecurity.InitializeDatabaseConnection` yöntemini çağırın. (WebMatrix 'te, başlatıcı site şablonu *\_AppStart. cshtml* dosyasında Bu metoda bir çağrı içerir.) Bu yöntemin `autoCreateTables` parametresi true olarak ayarlanmışsa (varsayılan olarak, başlatıcı site şablonunda true olarak ayarlanır) ve tanınmayan bir tablo adı yönteme (ikinci parametre) geçirilirse Yöntem bir hata oluşturmaz. Bunun yerine, tabloyu otomatik olarak oluşturur.
> 
> Bu, üyelik için özel bir kullanıcı tablosu kullanmayı amaçlıyorsanız ancak yanlış tablo adını `WebSecurity.InitializeDatabaseConnection` yöntemine geçirirseniz bir sorun olabilir. Yöntemi varsayılan olarak, belirttiğiniz tablo yoksa ve bunun yerine yeni bir tablo oluşturduğunda bir hata oluşturmaz, uygulama çalışıyor olarak görünebilir. Ancak, Özel Kullanıcı tablonuza (ve içindeki alanlarda) bağlı olan uygulama kodu sonunda beklenmedik hatalarla başarısız olabilir.
> 
> **Geçici çözüm**  
> `InitializeDatabaseConnection` yönteminde geçirilen adın, üyelik veritabanındaki kullanıcı profili tablosuyla eşleştiğinden emin olun veya `autoCreateTables` parametresinin false olarak ayarlandığından emin olun.

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a>Sorun: "Yönetici modülü ~/App\_Data için erişim gerektiriyor" hata iletisi

> Bazı durumlarda, kullanıcı oluşturmaya veya başka bir şekilde ASP.NET üyelik sistemiyle çalışmayı denemek sayfanın *Yönetim modülünün ~/App\_verilerine erişmesi gereken*hatayı görüntülemesine neden olabilir. Bu durum, IIS veya IIS Express 'nin altında çalıştığı hesabın, Web sitesi kökünde *uygulama\_veri* klasörü oluşturma ve bu klasöre yazma izinleri yoksa oluşur. 
> 
> **Geçici çözüm** Web sitesi için el ile *uygulama\_veri* klasörü oluşturun. Daha sonra uygulamanın altında çalıştığı Windows hesabının (genellikle ağ HIZMETI) uygulamanın kök klasörleri ve App\_verileri gibi alt klasörler için okuma/yazma izinlerine sahip olduğundan emin olun. [SQL Server Express Kullanıcı örneği oluşturma ve ASP.NET Web uygulaması projeleriyle](https://support.microsoft.com/kb/2002980)Ilgili Bilgi Bankası makalesi sorunlarını daha ayrıntılı olarak bulabilirsiniz.

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>Sorun: "SQL Server bir kullanıcı örneği oluşturulamadı" hatası

> Bir WebMatrix Web uygulaması SQL Server Express kullanıyorsa ve Windows 7 veya Windows Server 2008 R2 üzerinde IIS 7,5 çalıştırıyorsa, SQL Server kullanıcının yerel uygulama yolunu çalışma zamanında alamadığını belirten bir hata görebilirsiniz.
> 
> **Geçici çözüm** Uygulamanın altında çalıştığı Windows hesabının (genellikle ağ HIZMETI) uygulamanın kök klasörleri ve *App\_verileri*gibi alt klasörler için okuma/yazma izinlerine sahip olduğundan emin olun. [SQL Server Express Kullanıcı örneği oluşturma ve ASP.NET Web uygulaması projeleriyle](https://support.microsoft.com/kb/2002980)Ilgili Bilgi Bankası makalesi sorunlarını daha ayrıntılı olarak bulabilirsiniz.

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>Sorun: Package Manager kaynakları veya Package-Manager parolalarını içeren dosyalar IIS 6,0 ve öncesi sürümlerde kullanılabilir

> RC2 sürümü kullanılarak oluşturulmuş bir ASP.NET Web Pages (Razor) uygulaması dağıtırsanız ve uygulama */App\_Data/admin*altında bir *password. txt* veya *packageso,. txt* dosyası içeriyorsa, IIS 6,0, istenirse dosyayı kullanacaktır ve bu da paket yöneticisi örneğinizin parolalarını açığa çıkarmış olabilir. 
> 
> **Geçici çözüm** Password. *txt* veya *packageso,. txt* dosyasını *password. config* veya *packageso,. config*olarak yeniden adlandırın. Varsayılan olarak, IIS 6,0 *. config* uzantısına sahip dosyalara sahip değildir. (IIS 7 ' de, *uygulama\_veri* klasörüne hiçbir dosya sunulmadığından, dosyaları yeniden adlandırmanıza gerek kalmaz.)

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>Sorun: Beta 3 sürümü kullanılarak yüklenen paketleri kaldırmak, paket bileşenlerini tamamen kaldırmaz

> Beta 3 sürümündeki Paket Yöneticisi 'ni kullanarak bir paket yüklediyseniz ve sonra geçerli sürümü kullanarak kaldırmayı denerseniz, paket tümüyle kaldırılmaz. Paket yöneticisinin **Kaldır** düğmesinin kullanılması bazı bileşenleri kaldırır, ancak paketin kitaplık kodunu bırakır ve *Package. config* dosyasını güncelleştirmez.
> 
> **Geçici çözüm**   
> Şu adımları uygulayın:  
> 1. *App\_Data\packages* klasörünü silin. Bu, tüm paketleri kaldırır.   
> 2. Web sitesinin kökündeki *Packages. config* dosyasını silin.

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>Sorun: Visual Studio 'Da, Web tabanlı paket yöneticisini çağırmak uygulamayı çevrimdışı duruma getirir

> Visual Studio 'da (WebMatrix değil) çalışıyorsanız ve Paket Yöneticisi 'ni başlatmak için *\_yönetici* işlevini kullanırsanız, Visual Studio uygulamayı çevrimdışına alır ve *uygulamayı çevrimdışı. htm\_* Web sitesi köküne gönderir ve bu da paket yöneticisini kullanma yeteneğinizi kesintiye uğraşır.
> 
> [!NOTE]
> Web tabanlı Paket Yöneticisi arabirimini kullanırken genellikle bu davranışı görseniz de, *App\_veri* klasöründeki dosyaları ekler, kaldırırsanız veya değiştirirseniz aynı davranış oluşur.
> 
> **Geçici çözüm**   
> Visual Studio 'da paketlerle çalışmak için, Web tabanlı Paket Yöneticisi yerine NuGet uzantısını kullanın. Daha fazla bilgi için bkz. [NuGet belgeleri](https://docs.microsoft.com/nuget/). *App\_Data* klasöründeki diğer dosyalarla çalışıyorsanız, bu sorundan kaçınmak için dosyaları başka bir yerde tutmayı göz önünde bulundurun. Bu pratik değilse, *uygulamayı çevrimdışı. htm dosyası\_* el ile silin veya site yeniden çevrimiçi olana kadar bekleyin (varsayılan olarak 30 saniye sonra).

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>Sorun: Visual Studio IntelliSense ve proje şablonları yalnızca ASP.NET MVC sürüm 3 ' te kullanılabilir

> ASP.NET Web sayfalarının yüklenmesi, Visual Studio için IntelliSense ve ASP.NET Web sayfaları uygulamalarına yönelik proje şablonları gibi araçları da yüklemez.
> 
> **Geçici çözüm** Visual Studio 'da ASP.NET Web Pages uygulamaları için IntelliSense ve proje şablonları kullanmak üzere, Web Platformu Yükleyicisi veya [tek başına yükleyici](https://go.microsoft.com/fwlink/?LinkID=191797)aracılığıyla ASP.NET MVC 3 RC 'yi yükleme.

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>Sorun: bir ara sunucu aracılığıyla akışları veya diğer dış verileri okuma

> Siteyi çalıştıran sunucu bir proxy sunucusunun arkasındaysa, sitenizin dışından gelen bilgileri okuyabilmeniz için *Web. config* dosyasındaki proxy bilgilerini yapılandırmanız gerekebilir. Örneğin, `ReCaptcha` yardımcısını kullanıyorsanız, yardımcı, reCAPTCHA hizmeti ile iletişim kurar, ancak proxy sunucunuz tarafından engelleniyor olabilir. Benzer şekilde, ASP.NET Web sayfalarında kullanılan ve paket yöneticisi tarafından kullanılan akış gibi akışlar ara sunucu yapılandırması gerektirebilir.
> 
> Bir dış hizmetle çalışırken veya paket akışı ile çalışırken sorunlarla karşılaşırsanız, aşağıdaki öğeleri uygulamanızın kök *Web. config* dosyasına yerleştirin:
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> Proxy sunucu yapılandırma hakkında daha fazla bilgi için, MSDN Web sitesindeki [&lt;proxy&gt; öğesi (ağ ayarları)](https://msdn.microsoft.com/library/sa91de1e.aspx) bölümüne bakın.

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>Sorun: .NET Framework sürüm 4 ' ü kaldırmak, Razor sözdizimi ile ASP.NET Web sayfalarını devre dışı bırakır

> .NET Framework sürüm 4 ' ü kaldırıp yeniden yüklerseniz, Razor söz dizimi Web sayfaları devre dışı bırakılır. *. Cshtml* uzantılı sayfalar düzgün çalışmaz. ASP.NET Web sayfaları, bir derlemeyi makine kök *Web. config* dosyasına kaydeder ve .NET Framework kaldırıldığında bu dosya kaldırılır. .NET Framework yeniden yüklemek, yapılandırma dosyasının yeni bir sürümünü yüklüyor, ancak ASP.NET Web Pages derlemesinin başvurusunu eklemez.
> 
> **Geçici çözüm** .NET Framework yeniden yükledikten sonra, ASP.NET Web sayfalarını Razor söz dizimi yeniden yükleyin. Bu, genellikle aşağıdaki konumda olan makine kökündeki *Web. config* dosyasına aşağıdaki öğeyi ekler:  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>Sorun: Extensionless URL 'Leri IIS 7 veya IIS 7,5 üzerinde. cshtml/. vbhtml dosyalarını bulamıyor

> IIS 7 veya IIS 7,5 ' de, aşağıdakine benzer bir URL 'ye sahip istekler *. cshtml* veya *. vbhtml* uzantısına sahip sayfaları bulamaz:  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> Bu sorun ortaya çıkar çünkü URL yeniden yazma özelliği IIS 7 veya IIS 7,5 için varsayılan olarak etkinleştirilmemiştir. Likeliest senaryosu, IIS Express kullanarak yerel olarak test ederken sorunu görmemelidir, ancak Web sitenizi bir barındırma web sitesine dağıttığınızda bu sorunla karşılaşırsınız.
> 
> **Geçici çözüm**
> 
> - Sunucu bilgisayar üzerinde denetiminiz varsa, sunucu bilgisayarda, [belırlı ııs 7,0 veya ııs 7,5 işleyicilerinin, URL 'lerin noktayla bitmeyen istekleri işlemesini sağlayan bir güncelleştirmede](https://support.microsoft.com/kb/980368)açıklanan güncelleştirmeyi yükleyebilirsiniz.
> - Sunucu bilgisayarı üzerinde denetiminiz yoksa (örneğin, bir barındırma web sitesine dağıtıyorsanız), aşağıdakileri Web sitesinin *Web. config* dosyasına ekleyin: 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>Sorun: SQL Server Compact yüklü olmayan bir bilgisayara uygulama dağıtma

> SQL Server Compact veritabanlarını içeren uygulamalar, SQL Server Compact yüklü olmayan bir bilgisayarda çalıştırılabilir. Microsoft WebMatrix 1,0, bu ikili dosyaları sizin için otomatik olarak kopyalar ve uygun *Web. config* dosyası dönüşümlerini gerçekleştirir.
> 
> **Geçici çözüm** Bu dosyaları kopyalamanız ve *Web. config* dosyasının el ile değişiklikleri yapmanız gerekiyorsa, şunları yapın:
> 
> 1. Veritabanı altyapısı derlemelerini hedef bilgisayardaki uygulamanın *bin* klasörüne (ve alt klasörlerine) kopyalayın:  
> 
>    - *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*  Kopyala  
>      *\Bin* 'e
>    - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* dosyasını *\bin\x86* ' ya kopyalayın
>    - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* *  **'i** *\bin\amd64* dizinine kopyalayın
> 
> 2. Web sitesinin kök klasöründe bir *Web. config* dosyası oluşturun veya açın. (WebMatrix 1,0 ' de, **dosya türü seç** Iletişim kutusunda **Tümü** ' ne tıkladığınızda bu dosya türü kullanılabilir.)
> 3. Aşağıdaki öğeyi `<configuration>` öğesinin bir alt öğesi olarak ekleyin (`<system.web>` öğesinin içinde değil):
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>Sorun: "Database" ve "WebGrid" yardımcıları Visual Basic sürümünde Orta güvende çalışmıyor

> Visual Basic kullanıyorsanız ( *. vbhtml* dosyaları oluşturma), uygulama orta güveni kullanmak üzere ayarlandıysa `Database` ve `WebGrid` yardımcıları çalışmaz.
> 
> **Geçici çözüm**  
> Visual Studio 2010 kullanıyorsanız, Service Pack 1 sürümünü yükleyerek bu sorunu çözebilirsiniz. SP1 sürümünün son sürümü kullanılabilir olana kadar, Microsoft Indirme merkezi 'ndeki [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) sayfasından SP1 'in beta sürümünü indirebilirsiniz.   
>   
> Bu pratik değilse veya Visual Studio 2010 kullanmıyorsanız, geçici olarak uygulamayı tam güven kullanacak şekilde ayarlayabilirsiniz.

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>Sorun: "ApplicationPart" kaynaklarına dışarıdan erişilebilir

> Bir derleme `ApplicationPart` sınıfından türetilen nesneler içeriyorsa, bu derlemenin kaynakları `ResourceRouteHandler` sınıfı tarafından gösterilir. Örneğin, aşağıdaki URL 'YI göz önünde bulundurun:  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> Bu istek, *System. Web. Web sayfası. Administration. dll* derlemesindeki tüm kaynak dizelerini indirir. Tüm katıştırılmış kaynaklar (statik içerik olarak sunulmayı amaçlananlar bile) indirilir. Katıştırılmış kaynaklar hassas bilgiler içeriyorsa bu, bir güvenlik riskini temsil edebilir. 
> 
> **Geçici çözüm**   
> Bir **applicationpart** nesnesi oluşturursanız, bu **applicationpart** nesnesinin derlemesi ile ilişkili gömülü kaynakların hassas bilgiler içermediğinden emin olun.

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> WebMatrix 'e yönelik yükleme sorunları hakkında daha fazla bilgi için bu belgede daha önce [WebMatrix yükleme sorunları](#Known_Issues_Installation) bölümüne bakın.

Belgenin bu bölümünde, WebMatrix geliştirme ortamı için bilinen sorunlar açıklanmaktadır.

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>Sorun: Web. config dosyasındaki bir veritabanı bağlantı dizesinin Kullanıcı adı veya Paroladaki değişiklikler veritabanları çalışma alanına yansıtılmıyor

> **Geçici çözüm**  
> 
> 1. *Web. config* dosyasında, bağlantı dizesindeki veritabanı adını değiştirin (örneğin, "1" ekleyin).
> 2. *Web. config* dosyasını kaydedin.
> 3. **Veritabanları** ' na tıklayın ve yenileyin.
> 4. *Web. config* dosyasındaki bağlantı dizesindeki veritabanı adını özgün veritabanı adına geri değiştirin.
> 5. *Web. config* dosyasını kaydedin.
> 6. **Veritabanları** ' na tıklayın ve yenileyin.

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>Sorun: WebMatrix tarafından oluşturulan klasörler silinemez

> WebMatrix yükseltilmiş izinler kullanılarak çalışıyorsa (yani, Windows 'ta **yönetici olarak çalıştır** seçeneğini kullanarak WebMatrix 'i başlattığınızda), WebMatrix tarafından oluşturulan klasörler Windows Gezgini kullanılarak silinemez.
> 
> **Geçici çözüm**  
> Yükseltilmiş izinleri kullanarak Windows Gezgini 'ni çalıştırın. Aşağıdaki adımları uygulayın:  
> 
> 1. Windows 'ta **Başlat**' a tıklayın.
> 2. "Windows Gezgini" yazın ve **Windows Gezgini**için girişe sağ tıklayın.
> 3. **Yönetici olarak çalıştır**' a tıklayın. Daha sonra klasörleri silebilirsiniz.

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>Sorun: WebMatrix 1,0, yükseltme gerektiren belirli görevleri gerçekleştiremiyor

> WebMatrix 1,0, aşağıdaki durumlarda ek bileşenler yükleme gibi yükseltme gerektiren belirli görevleri gerçekleştiremiyor:
> 
> - Windows Vista veya Windows 7 ' de, yönetici ayrıcalıklarına sahip olmayan bir hesapla oturum açarsınız ve Kullanıcı hesabı denetimi (UAC) devre dışı bırakılır.
> - Microsoft Windows XP veya Microsoft Windows Server 2003 kullanıyorsunuz.
> 
> **Geçici çözüm**  
> WebMatrix 1,0 ' deki görevlerin çoğu, yönetici izni gerektirmez. Bu işlemler için, işlemi yönetici olarak gerçekleştirebilir veya aşağıdaki adımları izleyebilirsiniz:
> 
> - Windows Vista veya Windows 7 ' de UAC 'yi etkinleştirin.
> - Windows XP 'de, kullanıcıyı Administrators güvenlik grubuna ekleyin.

#### <a name="issue-site-from-web-gallery-is-disabled"></a>Sorun: "Web galerisinden site" devre dışı

> Web Platformu Yükleyicisi 3,0 yüklü değilse, **Web galerisinden site** seçeneği devre dışıdır.
> 
> **Geçici çözüm**  
> [3,0 Microsoft Web Platformu Yükleyicisi](https://go.microsoft.com/fwlink/?LinkID=194638)'yi yükler.

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>Sorun: Google Chrome bir çalıştır seçeneği olarak kullanılamıyor

> Google Chrome, **giriş** sekmesinde **Çalıştır** altında bulunan tarayıcılar listesinde gösterilmez.
> 
> **Geçici çözüm**  
> Google Chrome 'un bazı sürümleri, Windows 'daki varsayılan programlar özelliği ile kendilerini doğru bir şekilde kaydetmez. Geçici bir çözüm olarak, Google Chrome 'u başlatın, *Google Chrome ' ı Özelleştir ve denetle* menüsüne tıklayın, *Seçenekler*' e ve ardından *Google Chrome varsayılan tarayıcımı oluştur*' a tıklayın.

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>Sorun: "yabancı anahtar" iletişim kutusu birincil anahtar girmeye izin vermiyor

> **Yabancı anahtar** iletişim kutusu birincil anahtar tablosundan birincil anahtar adını girmenize izin vermez.
> 
> **Geçici çözüm**  
> Bu bilerek yapılır. Birincil anahtar tablosundan birincil anahtar adını girmeniz gerekmez.

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>Sorun: IntelliSense Razor söz dizimi, C#veya Visual Basic için WebMatrix 'te kullanılamaz

> IntelliSense, HTML ve CSS için WebMatrix 'te desteklenir. Ancak, diğer diller için kullanılamaz. 
> 
> **Geçici çözüm**   
> Yok.

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>Sorun: HTML ve CSS için IntelliSense, bağlamsal olarak uygun olmayan öğeler önerir

> WebMatrix 'te biçimlendirme için IntelliSense, [css 2,1 şemasını](http://www.w3.org/TR/CSS2/)kullanarak [XHTML 1,0 GEÇIŞLI şema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) ve CSS kullanarak HTML 'yi destekler. IntelliSense bu belirli şemaları temel aldığı için, belirli Etiketler, öznitelikler veya özellikler geçerli sayfa veya stil tanımına uygun olmayan önerilebilir olabilir. HTML için Ayrıca, hatalı oluşturulmuş XHTML (örneğin, Etiketler kapatılmadığı zaman) olarak yorumlanabilecek içerikte beklenmedik önerilere yol açabilir. Bu sorun, ekleme noktası tamamlanmamış bir etiketin içindeyse daha belirgin olabilir; Bu durumda, IntelliSense yeni açma etiketleri önerebilir veya diğer hatalı öneriler sunabilir. 
> 
> **Geçici çözüm**   
> HTML için iyi biçimlendirilmiş, tam bir XHTML sayfasında çalıştığınızdan emin olun. CSS için geçici çözüm yoktur.

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>Sorun: IntelliSense siz yazarken çağrılmıyor

> Bazen, IntelliSense HTML olarak çağrılamaz veya düzenleyicide CSS girilmeyebilir. Özellikle, ekleme noktası başka bir öğenin veya bir dosyanın sonunda doğrudan olduğunda bu durum oluşabilir. 
> 
> **Geçici çözüm**   
> Ekleme noktasının etrafında boşluk olduğundan ve ekleme noktasının bir dosyanın sonunda olmadığından emin olun. Ayrıca, Ctrl + Space tuşlarına basarak IntelliSense 'i el ile çağırabilirsiniz.

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>Sorun: IntelliSense devre dışı bırakmak için kullanılabilir bir kullanıcı arabirimi yok

> WebMatrix 1,0, IntelliSense 'i devre dışı bırakmak için Kullanıcı arabirimi veya hareket sağlar. 
> 
> **Geçici çözüm**   
> , IntelliSense 'i devre dışı bırakan bir anahtar içeren aşağıdaki komutu kullanarak WebMatrix 'i başlatın:  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express, aşağıdaki URL 'de bulunan kendi Benioku dosyasına sahiptir:

[https://go.microsoft.com/fwlink/?LinkID=207675&amp; CLCID = 0x409](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact, aşağıdaki URL 'de bulunan kendi Benioku dosyasına sahiptir:

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

WebMatrix 'in bir parçası olarak SQL Server Compact yükleme ile ilgili sorunlar hakkında bilgi için, bu belgenin önceki bölümlerinde bulunan [WebMatrix yükleme sorunları](#Known_Issues_Installation) bölümüne bakın.

### <a id="Known_Issues_Installing_Applications"></a>Uygulamaları yükleme

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>Sorun: kullanıcının Belgelerim klasörü bir ağ paylaşımında yeniden yönlendiriliyorsa, uygulamanın yüklenmesi uzun zaman alabilir

> **Geçici çözüm**  
> Yok. Uygulamanın yüklenmesi biraz zaman alabilir, ancak doğru şekilde yüklenir.

### <a id="Known_Issues_Publishing_Applications"></a>Uygulamaları yayımlama

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>Sorun: bir SQL Compact veritabanı yayımlanırken "gerekli izinler alınamıyor" hatası

> WebMatrix, .NET Framework sürüm 3,5 çalıştıran bir sunucuya SQL Server Compact için destek ikililerini, orta düzeydeki bir yapılandırma ile tam olarak desteklemez.
> 
> **Geçici çözüm**  
> Tercih edilen geçici çözüm, .NET Framework 4 ' ü sunucuya yüklemektir. Alternatif olarak, şunları yapın:
> 
> 1. Aşağıdaki öğeleri *Web\_düz güven. config* dosyasındaki `SecurityClasses` bölümüne ekleyin:
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. *Web\_düz güven. config* dosyasında aşağıdaki gerekli izinlerle yeni bir izin kümesi oluşturun:
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. Aşağıdaki öğeleri *Web\_düz güven. config* dosyasına yerleştirerek SQL Server Compact izin kümesini uygulayın:
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>Sorun: Galeri ve PhpBB Web uygulamaları, yayımlamadan sonra bir "hizmet kullanılamıyor" hatası görüntüler

> Bazı durumlarda, bir uygulamanın yayımlanması "hizmet kullanılamıyor" hatası oluşmasına neden olur.
> 
> **Geçici çözüm**  
> WebMatrix 'te, **yayınlama ayarları** penceresinde sunucu adının sonuna bir ters eğik çizgi ekleyin (\) ve uygulamayı yeniden yayımlayın.

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>Sorun: Bu web sitesi yerleşimi ve bağlantılar yayımlandıktan sonra kopuk

> Bir Mooteksiz uygulamayı yayımladıktan sonra, uygulama düzgün çalışmaz.
> 
> **Geçici çözüm**  
> WebMatrix 'te, **yayınlama ayarları** penceresinde **site adı** alanının sonuna bir eğik çizgi (/) ekleyin ve uygulamayı yeniden yayımlayın.

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>Sorun: nopCommerce yayımlama bir veritabanı hatasıyla başarısız oluyor

> NopCommerce 'i yayımlama başarısız oluyor ve "NOP\_günlük tablosuna ekle" gibi bir veritabanı hatası oluştu.
> 
> **Geçici çözüm**  
> 
> 1. WebMatrix 'te, nopCommerce 'i yerel olarak başlatmak için **Çalıştır** ' a tıklayın.
> 2. Yönetim sayfasında oturum açın.
> 3. **Sistem** menüsüne tıklayın.
> 4. **Günlük** seçeneğine tıklayın.
> 5. **Günlüğü Temizle** düğmesini tıklatın.
> 6. NopCommerce 'i yeniden yayımlayın.

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>Sorun: yayımlanmış bir siteyi karşıdan yüklerken SilverStripe CMS bir "HTTP 500 PHP FCGı hatası" görüntülüyor

> **Geçici çözüm**  
> **Yayımlanan siteyi karşıdan yükle**' ye tıkladıktan sonra, **Yayımlama önizlemesi**' nde `silverstripe-cache/manifest_main` atlayın. Bu dosya, önbelleğe alma amacıyla kullanılır ve her bilgisayara özeldir.

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>Sorun: yayımlanmış bir siteyi karşıdan yüklerken "'/' uygulamasında sunucu hatası" alt metin görüntülenir

> **Geçici çözüm**  
> Sitenin *Web. config* dosyasını açın ve veritabanı bağlantı DIZESINDEKI Kullanıcı kimliğini ve parolayı SQL Server yönetici kimlik bilgileri ("sa" kimlik bilgileri) ile değiştirin.
> 
> Alternatif olarak, oturum açtığınız kullanıcı hesabına `db_owner` izinlerle izin vermek için aşağıdaki adımları izleyin:
> 
> 1. Web platformu yükleyicisini kullanarak SQL Server Management Studio yükleme.
> 2. Yerel SQL Server Express örneğine bağlanın (varsayılan olarak, `.\SQLEXPRESS`).
> 3. &gt; [ *Localsubtextdatabase]* &gt; **güvenlik** &gt; **Kullanıcılar** &gt; *[localsubtextuser*] (varsayılan değer `subtextuser`], sağ tıklayın ve **Özellikler**' **e tıklayın.**
> 4. Rol üyeliği bölümünde **db\_Owner** ' ı seçin.

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>Sorun: "hedef URL" alanı http://veya https://ön eki değilse, site yayımlamadan sonra çalışmayabilir

> **Yayımlama ayarları** iletişim kutusunda, hedef URL `http://` veya `https://`ile başlamadıysanız, site dağıtımdan sonra çalışmayabilir.
> 
> **Geçici çözüm**  
> Bir siteyi yayımlamadan önce, **yayınlama ayarları** iletişim KUTUSUNDAKI hedef URL 'nin `http://` veya `https://`ile başlayacağını doğrulayın.

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>Sorun: bir MySQL veritabanının yayımlanması "veritabanı yayımlanamadı. Uzak veritabanı betiği çalıştıramadığı takdirde bu durum oluşabilir. "

> Hata çeşitli nedenlerden kaynaklanabilir. Bu hatayı görebileceğiniz bir nedeni, veritabanı betiğinin tek tırnak karakteri (') içermesi ve hedef MySQL veritabanının varsayılan karakter kümesinin UTF-8 ' e olmaması olabilir.
> 
> **Geçici çözüm**  
> Uzak MySQL veritabanı için varsayılan karakter kümesini UTF-8 olarak ayarlayın.

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>Sorun: site yayımladıktan veya indirildikten sonra bazı bağlantılar DotNetNuke 'da görünür değil

> Bir DotNetNuke sitesi yayımladığınızda veya indirdiğinizde, sitede yeni bağlantıların görünmesini sağlamak için Önbelleği temizlemeniz gerekebilir.
> 
> **Geçici çözüm**
> 
> 1. "Konak" olarak oturum açın.
> 2. Konak menüsüne gidin ve **konak ayarları**' nı seçin.
> 3. Aşağı kaydırın ve **Gelişmiş ayarlar**altında **performans ayarları**' nı genişletin.
> 4. Sayfalar için **önbelleği temizle** bağlantısına tıklayın.
> 5. Sayfanın en altına gidin ve uygulamayı yeniden başlatın.

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>Sorun: yayımlanmış bir siteyi indirdikten sonra Atomsıte içindeki bazı bağlantılar kopuk

> **Geçici çözüm**  
> *Service. config* dosyasında, *Users. config* dosyasında ve tüm *. xml* dosyalarında, URL dizesini (örneğin, `http://myhost.com/atomsite`) yerel bir dosyayla değiştirin (örneğin, `http://localhost:1239`).

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>Sorun: WordPress gibi MySQL tabanlı uygulamalar bir veritabanı hatasını yayımlayamaz ve bildiremez

> WebMatrix, varsayılan olarak MySQL 'i UTF-8 karakter kümesiyle birlikte yüklüyor. MySQL 'i kendinize yüklerseniz ve karakter kümesi UTF-8 değilse (örneğin, Latin1), veritabanları için yayımlama işlemi başarısız olabilir.
> 
> **Geçici çözüm**
> 
> 1. MySQL için karakter kümesini UTF-8 olarak değiştirin. (Ayrıntılar için bkz. MySQL web sitesinde [sunucu karakter kümesi ve harmanlama](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) .)
> 2. Uygulamayı yeniden yükleyin.
> 3. Uygulamayı yeniden yayımlayın.

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>Sorun: tarayıcı tabanlı kurulum özellikli uygulamalar için "yayımlanmış siteyi Indirme" başarısız oluyor

> Bazı uygulamalar (örneğin, Kentico CMS), bir veritabanı oluşturma gibi yükleme sonrası kurulumu gerçekleştirmek için bunları tarayıcıda açmanızı gerektirir. Tarayıcı tabanlı kurulumu tamamlamadan bunun gibi bir uygulamayı yayımlarsanız, uzak bir sunucudan aynı siteyi indirmeyi denemek başarısız olur.
> 
> **Geçici çözüm**  
> Siteyi yayımlamadan önce tarayıcı tabanlı kurulumu sona erdirin.

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>Sorun: "yayımlanmış siteyi Indirme" DotNetNuke ve Kooboo CMS için bir veritabanı hatasıyla başarısız oluyor

> Bir sunucudan bir uygulamayı indirmeye çalışırsanız ve **Yayımlama ayarları** iletişim kutusunda veritabanı bağlantı dizesinde yönetici kimlik bilgileriniz varsa, yayımlama günlüğünde şu hatayı görebilirsiniz:
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **Geçici çözüm**  
> Pratik ise, veritabanı için yönetici olmayan kimlik bilgilerini kullanarak siteyi yeniden yayımlayın (veya yayımladınız).

<a id="More_Info"></a>

## <a name="for-more-information"></a>Daha Fazla Bilgi İçin

WebMatrix 1,0 hakkında daha fazla bilgi için aşağıdaki Web sitelerine bakın:

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation. Tüm hakları saklıdır. [Kullanım koşulları](https://msdn.microsoft.cos/cc300389.aspx).
