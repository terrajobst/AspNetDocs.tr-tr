---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: 'Visual Studio kullanarak Web dağıtımı ASP.NET: sorun giderme | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 06/01/2015
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: b42476fca18b04f4557a216ee205cfd9220023e8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74623580"
---
# <a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a>Visual Studio kullanarak Web dağıtımı ASP.NET: sorun giderme

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

Bu sayfada, Visual Studio kullanarak bir ASP.NET Web uygulaması dağıtırken ortaya çıkabilecek bazı yaygın sorunlar açıklanmaktadır. Her biri için bir veya daha fazla olası nedenler ve ilgili çözümler sağlanır.

Gösterilen senaryolar hem Azure hem de üçüncü taraf barındırma sağlayıcıları için geçerlidir. Azure App Service Web Apps sorunlarını giderme hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Visual Studio 'Yu kullanarak Azure App Service bir Web uygulamasının sorunlarını giderme](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [Azure App Service Web Apps izleme](https://azure.microsoft.com/documentation/articles/web-sites-monitor//)
- [.Net Için Microsoft Azure SDK 2,0](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu 'nin blogu) duyurusu duyuruldu, Visual Studio 'da tanılama günlüklerinin nasıl alınacağı gösterilmektedir

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>'/' Uygulamasında sunucu hatası-geçerli özel hata ayarları hatanın ayrıntılarının uzaktan görüntülenmesini engelliyor

### <a name="scenario"></a>Senaryo

Bir siteyi uzak bir konağa dağıttıktan sonra, Web. config dosyasındaki customErrors ayarını belirten bir hata iletisi alırsınız ancak hatanın gerçek nedeninin ne olduğunu göstermez:

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Varsayılan olarak, ASP.NET, yalnızca Web uygulamanız yerel bilgisayarda çalışırken ayrıntılı hata bilgilerini gösterir. Genellikle, Web uygulamanız Internet üzerinden genel kullanıma sunulduğunda ayrıntılı hata bilgilerini göstermek istemezsiniz, çünkü saldırganlar uygulamada güvenlik açıklarını bulmak için bu bilgileri kullanabilir. Ancak, bir siteye bir site veya güncelleştirme dağıttığınızda, bazen bir şey yanlış olur ve gerçek hata iletisini almanız gerekir.

Uygulamanın uzak konakta çalışırken ayrıntılı hata iletileri görüntülemesini sağlamak için, Web. config dosyasını, customErrors modunu devre dışı bırakmak için düzenleyin, uygulamayı yeniden dağıtın ve uygulamayı yeniden çalıştırın:

1. Uygulama Web. config dosyasında, System. Web öğesinde bir customErrors öğesi varsa, mode özniteliğini "off" olarak değiştirin. Aksi takdirde, aşağıdaki örnekte gösterildiği gibi, System. Web öğesinde mode özniteliği "off" olarak ayarlanmış bir customErrors öğesi ekleyin: 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. Uygulamayı dağıtın.
3. Uygulamayı çalıştırın ve daha önce hatanın oluşmasına neden olan her şeyi tekrarlayın. Artık gerçek hata iletisinin ne olduğunu görebilirsiniz.
4. Hatayı çözümledikten sonra özgün customErrors ayarını geri yükleyin ve uygulamayı yeniden dağıtın.

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a>Bu dosya zaten mevcutsa, ' ContosoUniversity ' kopyası oluşturulamıyor/gölge kopyası oluşturulamıyor.

### <a name="scenario"></a>Senaryo

Visual Studio 'da bir projeyi çalıştırmayı denediğinizde aşağıdaki örnekte olduğu gibi ileti içeren bir hata sayfası alırsınız:

'/' Uygulamasında Sunucu Hatası. Bu dosya zaten mevcutsa, ' ContosoUniversity ' kopyası oluşturulamıyor/gölge kopyası oluşturulamıyor.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Bir dakika bekleyip Tarayıcıyı yenileyin veya siteyi yeniden derleyin ve tekrar çalıştırmayı deneyin.

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>SQL Server Compact kullanan bir Web sayfasında erişim reddedildi

### <a name="scenario"></a>Senaryo

SQL Server Compact kullanan bir siteyi dağıtırken ve veritabanına erişen dağıtılmış sitede bir sayfa çalıştırdığınız zaman, aşağıdaki hata iletisini görürsünüz:

Erişim reddedildi. (HRESULT özel durumu: 0x80070005 (E\_ACCESSREDDEDILDI))

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Sunucusundaki ağ HIZMETI hesabının, *bin\amd64* veya *BIN\X86* klasöründeki SQL SERVICE Compact Native ikililerini okuyabilmesi gerekir, ancak bu klasörler için okuma izinleri yoktur. Alt klasörlere izinleri genişletdiğinizden emin olmak için *bin* KLASÖRÜNDE ağ hizmeti için okuma izni ayarlayın.

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>Yetersiz Izinler nedeniyle yapılandırma dosyası okunamıyor

### <a name="scenario"></a>Senaryo

Yerel makinenizde IIS 'e bir uygulama dağıtmak için Visual Studio Publish düğmesine tıkladığınızda, yayımlama başarısız olur ve **Çıkış** penceresinde aşağıdakine benzer bir hata iletisi gösterilir:

' Makıne/YENIDEN YÖNLENDIRME ' IIS yapılandırma dosyası okunurken bir hata oluştu. Bu işlemi gerçekleştiren kimlik... Hata: yetersiz izinler nedeniyle yapılandırma dosyası okunamıyor.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Yerel makinenizde IIS 'de tek tıklamayla yayımlama 'yı kullanmak için, Visual Studio 'Yu yönetici izinleriyle çalıştırıyor olmanız gerekir. Visual Studio 'Yu kapatın ve yönetici izinleriyle yeniden başlatın.

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>Hedef bilgisayara bağlanılamadı... Belirtilen Işlemi kullanma

### <a name="scenario"></a>Senaryo

Uygulamayı dağıtmak için Visual Studio Publish düğmesine tıkladığınızda yayımlama başarısız olur ve **Çıkış** penceresi şuna benzer bir hata iletisi gösterir:

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Bir ara sunucu, hedef sunucuyla iletişimi kesintiye uğratma. Windows Denetim masasından veya Internet Explorer 'da **Internet seçenekleri** ' ni seçin ve **Bağlantılar** sekmesini seçin. **Internet özellikleri** Iletişim kutusunda **LAN ayarları**' na tıklayın. **Yerel ağ (LAN) ayarları** iletişim kutusunda **Ayarları otomatik olarak algıla** onay kutusunu temizleyin. Ardından Yayınla düğmesine tekrar tıklayın.

Sorun devam ederse, proxy veya güvenlik duvarı ayarları ile neler yapılabileceğini belirlemek için sistem yöneticinize başvurun. Web Dağıtımı, Web yönetimi hizmeti dağıtımı için standart olmayan bir bağlantı noktası kullandığından sorun oluşur (8172); Diğer bağlantılar için Web Dağıtımı 80 numaralı bağlantı noktasını kullanır. Bir üçüncü taraf barındırma sağlayıcısına dağıtım yaparken, genellikle Web yönetimi hizmetini kullanıyorsunuz.

## <a name="default-net-40-application-pool-does-not-exist"></a>Varsayılan .NET 4,0 uygulama havuzu yok

### <a name="scenario"></a>Senaryo

.NET Framework 4 gerektiren bir uygulamayı dağıtırken aşağıdaki hata iletisini görürsünüz:

Varsayılan .NET 4,0 uygulama havuzu yok veya uygulama eklenemedi. Lütfen bu makinede ASP.NET 4,0 'nin yüklü olduğunu doğrulayın.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

ASP.NET 4, IIS 'de yüklü değil. Dağıttığınız sunucu geliştirme Bilgisayarınız ise ve üzerinde Visual Studio 2010 yüklüyse, ASP.NET 4 bilgisayara yüklenir, ancak IIS 'de yüklenmemiş olabilir. Dağıttığınız sunucuda, yükseltilmiş bir komut istemi açın ve aşağıdaki komutları çalıştırarak IIS 'de ASP.NET 4 ' ü çalıştırın:

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

Ayrıca, varsayılan uygulama havuzunun .NET Framework sürümünü el ile ayarlamanız gerekebilir. Daha fazla bilgi için bu serideki IIS 'e test ortamı olarak dağıtma öğreticisine bakın.

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>Başlatma dizesinin biçimi, 0 dizininden başlayan belirtime uymuyor.

### <a name="scenario"></a>Senaryo

Tek tıklamayla yayımlama kullanarak bir uygulamayı dağıttıktan sonra, veritabanına erişen bir sayfa çalıştırdığınızda aşağıdaki hata iletisini alırsınız:

Başlatma dizesinin biçimi, 0 dizininden başlayan belirtime uymuyor.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Dağıtılan sitede *Web. config* dosyasını açın ve aşağıdaki örnekte olduğu gibi bağlantı dizesi değerlerinin `$(ReplaceableToken_`ile başlayıp başlamamadığını denetleyin:

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

Bağlantı dizeleri Bu örneğe benziyorsa, proje dosyasını düzenleyin ve aşağıdaki özelliği tüm derleme yapılandırmalarına yönelik PropertyGroup öğesine ekleyin:

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

Ardından uygulamayı yeniden dağıtın.

## <a name="http-500-internal-server-error"></a>HTTP 500 Iç sunucu hatası

### <a name="scenario"></a>Senaryo

Dağıtılan siteyi çalıştırdığınızda hatanın nedenini belirten özel bilgiler olmadan aşağıdaki hata iletisini görürsünüz:

HTTP hatası 500-Iç sunucu hatası.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

500 hataların pek çok nedeni vardır, ancak bu öğreticilerden sonra, Web. config dönüşüm dosyalarından birinde yanlış yere bir XML öğesi yerleştirmesiniz. Örneğin, doğrudan yapılandırma &lt;altında değil, &lt;System. Web&gt; altına bir &lt;location&gt; öğesi ekleyen dönüşümü yerleştirirseniz bu hatayı alırsınız. Dönüşümlerinin amaçlanan gibi çalıştığını doğrulamak için Web. config dönüşüm önizleme özelliğini kullanabilirsiniz. Çözüm, yanlış kodlanmış bir dönüşüm bulursanız dönüştürme dosyasını düzeltmek ve yeniden dağıtmak için kullanılır. Bir hata belirgin değilse, hangi birinin 500 hatasına neden olduğunu görmek için dönüşümler ve yeniden dağıtım için yorum yapmayı deneyin.

## <a name="http-50021-internal-server-error"></a>HTTP 500,21 Iç sunucu hatası

### <a name="scenario"></a>Senaryo

Dağıtılan siteyi çalıştırdığınızda aşağıdaki hata iletisini görürsünüz:

HTTP hatası 500,21-Iç sunucu hatası. "PageHandlerFactory-Integrated" işleyicisinin modül listesinde hatalı bir "ManagedPipelineHandler" modülü vardır.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Dağıttığınız site ASP.NET 4 hedefliyor, ancak ASP.NET 4, sunucuda IIS 'de kayıtlı değil. Sunucuda, yükseltilmiş bir komut istemi açın ve aşağıdaki komutları çalıştırarak ASP.NET 4 ' ü kaydedin:

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

Ayrıca, varsayılan uygulama havuzunun .NET Framework sürümünü el ile ayarlamanız gerekebilir. Daha fazla bilgi için bu serideki IIS 'e test ortamı olarak dağıtma öğreticisine bakın.

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a>SQL Server Express veritabanı uygulama\_verilerinde oturum açma başarısız oldu

### <a name="scenario"></a>Senaryo

*Web. config* dosyası bağlantı dizesini, *uygulama\_veri* klasörünüzdeki bir *. mdf* dosyası olarak bir SQL Server Express veritabanına işaret etmek üzere güncelleştirmiş ve uygulamayı ilk kez çalıştırdığınızda aşağıdaki hata iletisini görürsünüz:

System. Data. SqlClient. SqlException: oturum açma tarafından istenen "DatabaseName" veritabanı açılamıyor. Oturum açılamadı.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

*. Mdf* dosyasının adı, önceden var olan veritabanının *. mdf* dosyasını silseniz bile, bilgisayarınızda hiç bir zaman var olan herhangi bir SQL Server Express veritabanının adıyla eşleşemez. *. Mdf* dosyasının adını, hiç bir veritabanı adı olarak kullanılmamış bir adla değiştirin ve *Web. config* dosyasını yeni adı kullanacak şekilde değiştirin. Alternatif olarak, önceden var olan SQL Server Express veritabanlarını silmek için [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) kullanabilirsiniz.

## <a name="model-compatibility-cannot-be-checked"></a>Model uyumluluğu denetlenemiyor

### <a name="scenario"></a>Senaryo

*Web. config* dosyası bağlantı dizesini yeni bir SQL Server Express veritabanına işaret etmek üzere güncelleştirmiş ve uygulamayı ilk kez çalıştırdığınızda aşağıdaki hata iletisini görürsünüz:

Veritabanı model meta verileri içermediğinden model uyumluluğu denetlenemiyor. Includemetadataconvention 'ın DbModelBuilder kurallarına eklendiğinden emin olun.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Web. config dosyasına yerleştirdiğiniz veritabanı adı bilgisayarınızda daha önce kullanılıyorsa, içindeki bazı tablolarda bir veritabanı zaten var olabilir. Daha önce bilgisayarınızda kullanılmamış yeni bir ad seçin ve *Web. config* dosyasını bu yeni veritabanı adını kullanmak üzere işaret etmek üzere değiştirin. Alternatif olarak, var olan veritabanını silmek için [SQL Server Express yardımcı programını](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) veya [SQL Server Management Studio Express 'i](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) kullanabilirsiniz.

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>Bir betik Kullanıcı veya rol oluşturmaya çalıştığında SQL hatası

### <a name="scenario"></a>Senaryo

**Paket/YAYıMLAMA SQL** sekmesinde yapılandırılmış veritabanı dağıtımı kullanıyorsunuz, dağıtım SıRASıNDA çalışan SQL betikleri Kullanıcı oluşturma veya rol oluşturma komutları içerir ve bu komutlar yürütüldüğünde betik yürütme başarısız olur. Aşağıdakiler gibi daha ayrıntılı iletiler görebilirsiniz:

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

Bu hata, **SQL 'ı paketle/Yayımla** sekmesi yerine Web 'i **Yayımla** sihirbazında yapılandırdığınızda, [yapılandırma ve dağıtım](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forumundaki bir iş parçacığı oluşturun ve çözüm bu sorun giderme sayfasına eklenir.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Dağıtımı gerçekleştirmek için kullandığınız kullanıcı hesabının, Kullanıcı veya rol oluşturma izni yok. Örneğin, barındırma şirketi DB\_DataReader, DB\_DataWriter ve DB\_ddladmin rollerini sizin için ayarladığı Kullanıcı hesabına atayabilirler. Bunlar, çoğu veritabanı nesnesini oluşturmak için yeterlidir, ancak kullanıcı veya rol oluşturmaya yönelik değildir. Hatayı önlemenin bir yolu, veritabanı dağıtımından kullanıcılar ve roller dışlamamaktır. Bunu, veritabanının otomatik olarak oluşturulan betiği için PreSource öğesini düzenleyerek, bu sayede aşağıdaki öznitelikleri de içerecek şekilde düzenleyebilirsiniz:

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

Proje dosyasındaki PreSource öğesinin nasıl düzenleneceği hakkında daha fazla bilgi için bkz. [nasıl yapılır: proje dosyasında dağıtım ayarlarını düzenleme](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx). Geliştirme veritabanınızdaki kullanıcıların veya rollerinin hedef veritabanında olması gerekiyorsa, yardım almak için barındırma sağlayıcınızla görüşün.

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>Dağıtım sırasında Özel betikler çalıştırılırken zaman aşımı hatası SQL Server

### <a name="scenario"></a>Senaryo

Dağıtım sırasında çalışacak özel SQL betikleri belirttiniz ve Web Dağıtımı onları çalıştırdığında zaman aşımına uğrar.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Farklı işlem modlarına sahip birden çok betiğin çalıştırılması zaman aşımı hatalarına neden olabilir. Varsayılan olarak, otomatik olarak oluşturulan betikler bir işlemde çalışır, ancak özel betikler değildir. **Paket/YAYıMLAMA SQL** sekmesinde **var olan bir veritabanından verileri ve/veya şemayı çekme** seçeneğini BELIRLERSENIZ ve özel bir SQL betiği eklerseniz, tüm betiklerin aynı işlem ayarlarını kullanabilmesi için bazı betiklerdeki işlem ayarlarını değiştirmelisiniz. Daha fazla bilgi için bkz. [nasıl yapılır: bir Web uygulaması projesiyle veritabanı dağıtma](https://msdn.microsoft.com/library/dd465343.aspx).

İşlem ayarlarını, hepsi aynı olması ve bu hatayı almaya devam etmek için yapılandırdıysanız, olası bir geçici çözüm betikleri ayrı olarak çalıştırmak olur. SQL **paketleme/Yayımla** sekmesindeki **veritabanı betikleri** kılavuzunda, zaman aşımı hatasına neden olan betiğin **dahil** etme onay kutusunu temizleyip projeyi yayımlayın. Ardından **veritabanı betikleri** kılavuzuna geri dönün, bu betiğin **içerme** onay kutusunu seçin ve diğer betikler için **ekleme** onay kutularını temizleyin. Ardından projeyi yeniden yayımlayın. Bu kez yayımladığınızda, yalnızca seçilen özel betik çalışır.

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>Site bildiriminin akış verileri henüz kullanılamıyor

### <a name="scenario"></a>Senaryo

T (test) seçeneğiyle *Deploy. cmd* dosyasını kullanarak bir paket yüklerken aşağıdaki hata iletisini görürsünüz:

Hata: ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/Sqlscrıpt ' akış verileri henüz kullanılamıyor.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Hata iletisi, komutun bir test raporu oluşturmayacağı anlamına gelir. Ancak, y (gerçek yükleme) seçeneğini kullanırsanız komut çalıştırılabilir. İleti yalnızca komutu test modunda çalıştırırken bir sorun olduğunu gösterir.

## <a name="this-application-requires-managedruntimeversion-v40"></a>Bu uygulama ManagedRuntimeVersion v 4.0 gerektiriyor

### <a name="scenario"></a>Senaryo

Dağıtmaya çalıştığınızda aşağıdaki hata iletisini görürsünüz:

Kullanmaya çalıştığınız uygulama havuzu ' v 2.0 ' olarak ayarlanmış ' managedRuntimeVersion ' özelliğine sahip. Bu uygulama ' v 4.0 ' gerektirir.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

ASP.NET 4, IIS 'de yüklü değil. Dağıttığınız sunucu geliştirme Bilgisayarınız ise ve üzerinde Visual Studio 2010 yüklüyse, ASP.NET 4 bilgisayara yüklenir, ancak IIS 'de yüklenmemiş olabilir. Dağıttığınız sunucuda, yükseltilmiş bir komut istemi açın ve aşağıdaki komutları çalıştırarak IIS 'de ASP.NET 4 ' ü çalıştırın:

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>Microsoft. Web. Deployment. DeploymentProviderOptions yayınlanamadı

### <a name="scenario"></a>Senaryo

Bir paket dağıttığınızda aşağıdaki hata iletisini görürsünüz:

' Microsoft. Web. Deployment. DeploymentProviderOptions ' türündeki nesne ' Microsoft. Web. Deployment. DeploymentProviderOptions ' öğesine atanamıyor.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Web Dağıtımı 1,1 Kullanıcı arabirimini kullanarak IIS Manager 'dan Web Dağıtımı 2,0 ' nin yüklü olduğu bir sunucuya dağıtmaya çalışıyorsunuz. Bir paketi içeri aktararak dağıtmak üzere IIS uzaktan yönetim aracını kullanıyorsanız, bağlantıyı kurarken **yeni özellikler kullanılabilir** iletişim kutusunu işaretleyin. (Bu iletişim kutusu yalnızca bağlantı ilk kez oluşturulduğunda görüntülenebilir. Bağlantıyı temizlemek ve baştan başlamak için IIS Yöneticisi 'Ni kapatın ve komut istemine inetmgr/Reset süpürmeden girerek yeniden başlatın.) Listelenen özelliklerden biri **Web DAĞıTıMı UI**ise ve 8 ' den daha düşük bir sürüm numarası içeriyorsa, dağıttığınız sunucu, Web dağıtımı yüklü olan hem 1,1 hem de 2,0 sürümüne sahip olabilir. 2,0 yüklü bir istemciden dağıtım yapmak için sunucuda yalnızca Web Dağıtımı 2,0 yüklü olmalıdır. Bu sorunu çözmek için barındırma sağlayıcınıza başvurmanız gerekir.

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>SQL Server Compact yerel bileşenleri yüklenemiyor

### <a name="scenario"></a>Senaryo

Dağıtılan siteyi çalıştırdığınızda aşağıdaki hata iletisini görürsünüz:

8482 sürümünün ADO.NET sağlayıcısına karşılık gelen SQL Server Compact yerel bileşenleri yüklenemiyor. Doğru SQL Server Compact sürümünü yükler. Daha fazla bilgi için bkz. KB makalesi 974247.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Dağıtılan sitede, uygulamanın *bin* klasörü altında yerel Derlemelerle *AMD64* ve *x86* alt klasörleri yok. SQL Server Compact yüklü bir bilgisayarda, yerel derlemeler *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*konumunda bulunur. Doğru dosyaları bir Visual Studio projesindeki doğru klasörlere almanın en iyi yolu NuGet SqlServerCompact paketini yüklemektir. Paket yüklemesi, yerel derlemeleri *AMD64* ve *x86*'ya kopyalamak için derleme sonrası bir betik ekler. Ancak bunların dağıtılması için, bunları projeye el ile eklemeniz gerekir. Daha fazla bilgi için bkz. [dağıtma SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) öğreticisi.

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Bir Entity Framework Code First uygulaması dağıttıktan sonra "yol geçerli değil" hatası

### <a name="scenario"></a>Senaryo

Entity Framework Code First Migrations kullanan bir uygulamayı ve veritabanını App\_Data klasöründeki bir dosyaya depolayan SQL Server Compact gibi bir DBMS 'yi dağıtırsınız. İlk dağıtımınız sonrasında veritabanını oluşturmak için Code First Migrations yapılandırdınız. Uygulamayı çalıştırdığınızda aşağıdaki örnekte olduğu gibi bir hata iletisi alırsınız:

Yol geçerli değil. Veritabanı için dizini denetleyin. [Yol = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf]

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Code First veritabanını oluşturmaya çalışıyor, ancak uygulama\_veri klasörü yok. Dağıttığınız sırada *app\_Data* klasöründe herhangi bir dosya yoktu veya proje Özellikler penceresi **paket/yayımlama Web** sekmesinde **uygulama\_verileri hariç tut** ' u seçtiniz. Sunucuda kopyalanacak klasörde dosya yoksa dağıtım işlemi sunucuda bir klasör oluşturmaz. Veritabanında zaten bir veritabanı ayarlandıysa, yayımlama profilinde **Hedefteki ek dosyaları Kaldır** ' ı seçtiyseniz dağıtım işlemi dosyaları ve *uygulama\_veri* klasörünün kendisini siler. Sorunu çözmek için, *app\_veri* klasörüne. txt dosyası gibi bir yer tutucu dosyası yerleştirin, **uygulama\_** ' ın seçili olmadığından emin olun ve yeniden dağıtın.

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>"Temel aldığı RCW 'dan ayrılan COM nesnesi kullanılamaz."

### <a name="scenario"></a>Senaryo

Uygulamanızı dağıtmak için tek tıklamayla yayımlama 'yı başarıyla kullanıyorsunuz ve sonra bu hatayı almaya başlacaksınız:

Web Dağıtım görevi başarısız oldu. ('<https://serverurl.com/msdeploy.axd?site=sitename>' uzak Aracı URL 'sine yönelik istek tamamlanamadı.)  
 '<https://url/msdeploy.axd?site=sitename>' uzak Aracı URL 'sine yönelik istek tamamlanamadı.  
İstek durduruldu: istek iptal edildi.  
Temel alınan RCW 'dan ayrılan COM nesnesi kullanılamaz.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Bu hatayı çözmek için genellikle Visual Studio 'Nun kapatılıp yeniden başlatılması gerekir.

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a>Yayımlama için kullanılan Kullanıcı kimlik bilgilerinin setACL yetkilisi olmadığından dağıtım başarısız oluyor

### <a name="scenario"></a>Senaryo

Yayımlama, klasör izinlerini ayarlama yetkiniz olmadığını belirten bir hata ile başarısız olur (kullandığınız kullanıcı hesabı, setACL yetkilisi yoksa).

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Varsayılan olarak, Visual Studio sitenin kök klasöründe okuma izinlerini ayarlar ve App\_Data klasöründe yazma izinlerine sahiptir. Site klasörlerinin varsayılan izinlerinin doğru olduğunu ve ayarlanması gerekmediğini biliyorsanız,&lt;ıncludesetaclproviderto Destination&gt;(tek bir profili etkilemek için) veya WPP. targets dosyasına (tüm profilleri etkilemek için) **yanlış&lt;/ıncludesetaclproviderondestination&gt;** ekleyerek bu davranışı devre dışı bırakabilirsiniz. Bu dosyaların nasıl düzenleneceği hakkında daha fazla bilgi için bkz. [nasıl yapılır: profil (. pubxml) dosyalarında dağıtım ayarlarını düzenleme](https://msdn.microsoft.com/library/ff398069.aspx).

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a>Uygulama bir uygulama klasörüne yazmayı denediğinde erişim reddedildi hataları

### <a name="scenario"></a>Senaryo

Uygulama klasörlerinden birinde bir dosyayı oluşturmaya veya düzenlemeye çalıştığında, bu klasör için yazma yetkisi olmadığından uygulamanızın hataları.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Varsayılan olarak, Visual Studio sitenin kök klasöründe okuma izinlerini ayarlar ve App\_Data klasöründe yazma izinlerine sahiptir. Uygulamanızın bir alt klasöre yazma erişimi gerekiyorsa, klasör Izinlerini ayarlama ve bu serideki üretim ortamı öğreticilerine dağıtma bölümünde gösterildiği gibi bu klasör için izinleri ayarlayabilirsiniz. Uygulamanızın, sitenin kök klasörüne yazma erişimi olması gerekiyorsa, yayımlama profili dosyasına (tek bir profili etkilemek için) veya WPP. targets dosyasına (tüm profilleri etkilemek için) **&lt;ıncludesetaclproviderto destination&gt;False&lt;/ıncludesetaclproviderondestination&gt;** ekleyerek, kök klasörde salt okuma erişimi ayarlamayı engellemeniz gerekir. Bu dosyaların nasıl düzenleneceği hakkında daha fazla bilgi için bkz. [nasıl yapılır: profil (. pubxml) dosyalarında dağıtım ayarlarını düzenleme](https://msdn.microsoft.com/library/ff398069.aspx).

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>Yapılandırma hatası-targetFramework özniteliği, .NET Framework yüklü sürümünden daha sonraki bir sürüme başvuruyor

### <a name="scenario"></a>Senaryo

ASP.NET 4,5 hedefleyen bir Web projesini başarıyla yayımladınız, ancak uygulamayı çalıştırdığınızda (Web. config dosyasında customErrors modu "off" olarak ayarlandığında) aşağıdaki hatayı alırsınız:

Web. config dosyasının &lt;derlemesi&gt; öğesindeki ' targetFramework ' özniteliği yalnızca .NET Framework için sürüm 4,0 ' i ve üstünü hedeflemek için kullanılır (örneğin, '&lt;derlemesi targetFramework = "4.0"&gt;'). ' TargetFramework ' özniteliği şu anda .NET Framework yüklü olan sürümünden daha sonraki bir sürüme başvuruda bulunuyor. .NET Framework geçerli bir hedef sürümünü belirtin veya .NET Framework gerekli sürümünü yükler.

Hata sayfasının kaynak hata kutusu, hatanın nedeni olarak Web. config ' den aşağıdaki satırı vurgular:

&lt;derlemesi targetFramework = "4.5"/&gt;

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Sunucu, ASP.NET 4,5 desteklemez. ASP.NET 4,5 desteğinin ne zaman ve ne zaman ekleneceğini öğrenmek için barındırma sağlayıcısına başvurun. Sunucunun yükseltilmesi bir seçenek değilse, bunun yerine ASP.NET 4 veya önceki bir sürümünü hedefleyen bir Web projesi dağıtmanız gerekir.

Aynı hedefe bir ASP.NET 4 veya daha önceki bir Web projesi dağıtırsanız, **Web 'ı Yayımla** sihirbazının **Ayarlar** sekmesinde **Hedefteki ek dosyaları Kaldır** onay kutusunu seçin. **Hedefteki ek dosyaları Kaldır**' ı seçmezseniz, yapılandırma hata sayfasını almaya devam edersiniz.

Proje **özellikleri** penceresi bir hedef çerçeve açılan listesi içerir, ancak bu sorunu yalnızca **.NET Framework 4,5** ' den **.NET Framework 4**' e değiştirerek çözebilirsiniz. Hedef çerçeveyi önceki bir Framework sürümüne değiştirirseniz, projenin daha sonraki Framework sürümü derlemelerine başvuruları olur ve çalıştırılmaz. Bu başvuruları el ile değiştirmeniz veya .NET Framework 4 veya önceki bir sürümü hedefleyen yeni bir proje oluşturmanız gerekir. Daha fazla bilgi için bkz. [Web siteleri için .NET Framework Hedefleme](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).

## <a name="medium-trust-errors"></a>Orta güven hataları

### <a name="scenario"></a>Senaryo

Uygulamanızı üretimde çalıştırdığınızda, orta güvenle ilgili bir hata alır.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

Birçok üçüncü taraf barındırma sağlayıcısı, Web sitenizi Orta güvende çalıştırır, bu da izin verilmeyen bazı şeyler olduğu anlamına gelir. Örneğin, uygulama kodu Windows kayıt defterine erişemez ve uygulamanızın klasör hiyerarşisinin dışındaki dosyaları okuyamaz veya yazamaz. Varsayılan olarak, uygulamanız yerel bilgisayarınızda *tam güvende* çalışır, bu da uygulamanın üretime dağıtırken başarısız olabilecek işlemleri yapabileceği anlamına gelir.

Sorunu gidermek için, uygulamayı yerel IIS ortamında Orta güvende çalışacak şekilde yapılandırabilirsiniz. Bunu yapmak için uygulama *Web. config* dosyasını açın ve **System. Web** öğesine bu örnekte gösterildiği gibi bir **güven** öğesi ekleyin.

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

Uygulama artık yerel bilgisayarınızda bile IIS 'de Orta güvende çalışacaktır.

Azure orta düzeyde güven gerektirmediğinden, Azure App Service dağıtım yapıyorsanız bunu yapmayın. Bu öğreticinin Şubat 2012 ' de yazıldığı sırada, uygulamanızın Orta güvende çalışmasını sağlamak için bu yöntemin kullanılması, Azure 'da bir hataya neden olur.

Entity Framework Code First Migrations kullanıyorsanız ve uygulamanızı Orta güvende çalıştıran bir barındırma sağlayıcısına dağıtıyorsanız, sürüm 5,0 veya sonraki bir sürümün yüklü olduğundan emin olun. Entity Framework sürüm 4,3 ' de, geçişler veritabanı şemasını güncelleştirmek için tam güven gerektirir.

## <a name="http-40417-not-found-error"></a>HTTP 404,17 bulunamadı hatası

### <a name="scenario"></a>Senaryo

Dağıtım bilgisayarınızda dağıtılan siteyi IIS 'de çalıştırdığınızda, sunucunun varsayılan. aspx 'i işleyemadığını bildiren aşağıdaki hata iletisini görürsünüz:

HTTP hatası 404,17-bulunamadı

İstenen içerik betik gibi görünüyor ve statik dosya işleyicisi tarafından sunulmayacak.

### <a name="possible-cause-and-solution"></a>Olası nedeni ve çözümü

ASP.NET 4,5 bilgisayarınıza yüklenmemiş olabilir. ASP.NET 4,5 ' nin nasıl yükleneceğini açıklayan bu serideki test ortamı olarak IIS 'ye dağıtma öğreticisindeki adımlara bakın.

> [!div class="step-by-step"]
> [Öncekini](deploying-extra-files.md)
