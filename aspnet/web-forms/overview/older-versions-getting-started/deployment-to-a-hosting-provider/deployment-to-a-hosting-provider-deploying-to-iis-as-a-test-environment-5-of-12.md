---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: "Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: IIS 'e test ortamı olarak dağıtma-5/12 | Microsoft Docs"
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5d85232ff2cb229d771d517db7173721c9e277bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635130"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: IIS 'e test ortamı olarak dağıtma-5/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bu öğreticide, yerel bilgisayarda IIS 'ye bir ASP.NET Web uygulamasının nasıl dağıtılacağı gösterilmektedir.

Bir uygulama geliştirirken, genellikle Visual Studio 'da çalıştırarak test edersiniz. Bu, varsayılan olarak, Visual Studio geliştirme sunucusunu (Cassini olarak da bilinir) kullandığınız anlamına gelir. Visual Studio geliştirme sunucusu, Visual Studio 'da geliştirme sırasında test yapmayı kolaylaştırır, ancak tam olarak IIS gibi çalışmaz. Sonuç olarak, uygulamayı Visual Studio 'da test ettiğinizde doğru şekilde çalışacak, ancak barındırma ortamında IIS 'e dağıtıldığında başarısız olur.

Uygulamanızı bu yollarla daha güvenilir bir şekilde test edebilirsiniz:

1. Geliştirme sırasında Visual Studio 'da test ettiğinizde, Visual Studio geliştirme sunucusu yerine IIS Express veya tam IIS kullanın. Bu yöntem genellikle sitenizin IIS altında nasıl çalışacağını daha doğru bir şekilde taklit eder. Ancak, bu yöntem dağıtım işleminizi test etmez veya dağıtım işleminin sonucunun doğru şekilde çalışacağını doğrular.
2. Daha sonra üretim ortamınıza dağıtmak için kullanacağınız süreci kullanarak uygulamayı geliştirme bilgisayarınızda IIS 'e dağıtın. Bu yöntem, uygulamanızın IIS altında doğru şekilde çalışacağını doğrulamaya ek olarak dağıtım işleminizi doğrular.
3. Uygulamayı üretim ortamınıza olabildiğince yakın bir test ortamına dağıtın. Bu öğreticiler için üretim ortamı bir üçüncü taraf barındırma sağlayıcısı olduğundan, ideal test ortamı barındırma sağlayıcısına sahip ikinci bir hesap olacaktır. Bu ikinci hesabı yalnızca test için kullanırsınız, ancak üretim hesabıyla aynı şekilde ayarlanır.

Bu öğreticide, seçenek 2 ' nin adımları gösterilmektedir. Seçenek 3 ' e yönelik kılavuzluk, [üretim ortamı](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) öğreticisine dağıtmanın sonunda verilmiştir ve Bu öğreticinin sonunda, 1. seçenek için kaynakların bağlantıları vardır.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="configuring-the-application-to-run-in-medium-trust"></a>Uygulamayı Orta güvende çalışacak şekilde yapılandırma

IIS yüklemeden ve dağıtımına dağıtılmadan önce, sitenin tipik bir paylaşılan barındırma ortamında olacak şekilde daha fazla çalışmasını sağlamak için bir Web. config dosya ayarını değiştirirsiniz.

Barındırma sağlayıcıları genellikle Web sitenizi *Orta güvende*çalıştırır, bu da izin verilmeyen bazı şeyler olduğu anlamına gelir. Örneğin, uygulama kodu Windows kayıt defterine erişemez ve uygulamanızın klasör hiyerarşisinin dışındaki dosyaları okuyamaz veya yazamaz. Varsayılan olarak, uygulamanız yerel bilgisayarınızda *yüksek güvende* çalışır, bu da uygulamanın üretime dağıtırken başarısız olabilecek işlemleri yapabileceği anlamına gelir. Bu nedenle, test ortamının üretim ortamını daha doğru yansıtması için uygulamayı Orta güvende çalışacak şekilde yapılandırırsınız.

Uygulama Web. config dosyasında, bu örnekte gösterildiği gibi **System. Web** öğesine bir **güven** öğesi ekleyin.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

Uygulama artık yerel bilgisayarınızda bile IIS 'de Orta güvende çalışacaktır. Bu ayar, üretimde başarısız olabilecek bir şey yapmak için uygulama kodu tarafından yapılan her türlü girişimden erken yakalamanıza olanak tanır.

> [!NOTE]
> Entity Framework Code First Migrations kullanıyorsanız, sürüm 5,0 veya sonraki bir sürümün yüklü olduğundan emin olun. Entity Framework sürüm 4,3 ' de, geçişler veritabanı şemasını güncelleştirmek için tam güven gerektirir.

## <a name="installing-iis-and-web-deploy"></a>IIS ve Web Dağıtımı yükleme

Geliştirme bilgisayarınızda IIS 'e dağıtmak için IIS ve Web Dağıtımı yüklü olmalıdır. Bunlar varsayılan Windows 7 yapılandırmasına dahil edilmez. Hem IIS hem de Web Dağıtımı zaten yüklediyseniz, sonraki bölüme atlayın.

Web Platformu Yükleyicisi IIS için önerilen bir yapılandırma yüklediği ve gerekirse IIS ve Web Dağıtımı önkoşullarını otomatik olarak yüklediği için [Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx) 'nin YÜKLENMESI, ııs ve Web dağıtımı yüklemek için tercih edilen yoldur.

IIS ve Web Dağıtımı yüklemek üzere Web Platformu Yükleyicisi 'ni çalıştırmak için aşağıdaki bağlantıyı kullanın. IIS, Web Dağıtımı veya gerekli bileşenlerinden herhangi birini zaten yüklediyseniz, Web Platformu Yükleyicisi yalnızca eksik olanları kurar.

- [WebPI kullanarak IIS ve Web Dağıtımı 'yi yükleyip](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>Varsayılan uygulama havuzunu .NET 4 ' e ayarlama

IIS yüklendikten sonra, .NET Framework sürüm 4 ' ün varsayılan uygulama havuzuna atandığından emin olmak için **IIS Yöneticisi 'ni** çalıştırın.

Windows **Başlat** menüsünde **Çalıştır**' ı seçin, "inetmgr" yazın ve ardından **Tamam**' ı tıklatın. ( **Çalıştır** komutu **Başlangıç** menünüzde değilse, açmak Için Windows tuşuna ve R tuşuna basabilirsiniz. Ya da görev çubuğuna sağ tıklayın, **Özellikler**' e tıklayın, **Başlat menüsü** sekmesini seçin, **Özelleştir**' e tıklayın ve **komutu Çalıştır**' ı seçin.)

**Bağlantılar** bölmesinde, sunucu düğümünü genişletin ve **uygulama havuzları**' nı seçin. **Uygulama havuzları** bölmesinde, aşağıdaki çizimde gösterildiği gibi, **DefaultAppPool** .NET Framework sürüm 4 ' e atanırsa, sonraki bölüme atlayın.

[![Inetmgr_showing_4.0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

Yalnızca iki uygulama havuzu görürseniz ve her ikisi de .NET Framework 2,0 ' e ayarlanırsa, IIS 'de ASP.NET 4 ' ü yüklemelisiniz:

- Windows **Başlat** menüsünde **komut istemi** ' ni sağ tıklatıp **yönetici olarak çalıştır**' ı seçerek bir komut istemi penceresi açın. Ardından, aşağıdaki komutları kullanarak IIS 'de ASP.NET 4 ' ü yüklemek için [aspnet\_regııs. exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) ' yi çalıştırın. (64 bitlik sistemlerde "Framework" yerine "Framework64" koyun.)

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![aspnet_regiis_installing_ASP. NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    Bu komut .NET Framework 4 için yeni uygulama havuzları oluşturur, ancak varsayılan uygulama havuzu hala 2,0 olarak ayarlanır. .NET 4 ' ü hedefleyen bir uygulamayı bu uygulama havuzuna dağıtacaksınız, bu nedenle uygulama havuzunu .NET 4 olarak değiştirmeniz gerekir.

**IIS Yöneticisi 'ni**kapattıysanız yeniden çalıştırın, sunucu düğümünü genişletin **ve uygulama havuzları ' na tıklayarak** **uygulama havuzları** bölmesini yeniden görüntüleyin.

**Uygulama havuzları** bölmesinde, **DefaultAppPool**' e tıklayın ve ardından **Eylemler** bölmesinde **temel ayarlar**' a tıklayın.

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

**Uygulama havuzunu Düzenle** iletişim kutusunda **.NET Framework sürümünü** **.NET Framework v 4.0.30319** olarak değiştirin ve **Tamam**' a tıklayın.

[![Selecting_. NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

Artık IIS 'de yayımlamaya hazırsınız.

## <a name="publishing-to-iis"></a>IIS 'de yayımlama

Visual Studio 2010 ve Web Dağıtımı kullanarak dağıtabileceğiniz çeşitli yollar vardır:

- Visual Studio tek tıklamayla Yayımla 'yı kullanın.
- Bir *dağıtım paketi* oluşturun ve IIS Yöneticisi Kullanıcı arabirimini kullanarak yükler. Dağıtım paketi, IIS 'de bir site yüklemek için gereken tüm dosyaları ve meta verileri içeren bir *. zip* dosyasından oluşur.
- Bir dağıtım paketi oluşturun ve komut satırını kullanarak yüklemeyi yapın.

Önceki öğreticilerde, dağıtım görevlerini otomatikleştirmek üzere Visual Studio 'Yu otomatik hale getirmek için ayarlama işlemi, bu üç yöntemin tümü için geçerlidir. Bu öğreticilerde bu yöntemlerin ilkini kullanacaksınız. Dağıtım paketlerini kullanma hakkında daha fazla bilgi için bkz. [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx).

Yayımlamadan önce, Visual Studio 'Yu yönetici modunda çalıştırdığınızdan emin olun. (Windows 7 **Başlat** menüsünde, kullanmakta olduğunuz Visual Studio sürümü simgesine sağ tıklayın ve **yönetici olarak çalıştır**' ı seçin.) Yönetici modu, yalnızca yerel bilgisayarda IIS 'e yayımlarken yayımlama için gereklidir.

**Çözüm Gezgini**, contosouniversity projesine (contosouniversity. dal projesi değil) sağ tıklayın ve **Yayımla**' yı seçin.

**Web 'ı Yayımla** Sihirbazı görüntülenir.

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

Aşağı açılan listede **&lt;yeni...&gt;** öğesini seçin.

**Yeni profil** iletişim kutusunda "test" yazın ve ardından **Tamam**' a tıklayın.

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

Bu ad, daha önce oluşturduğunuz Web. test. config dönüştürme dosyasının orta düğümüyle aynıdır. Bu yazışma, Web. test. config dönüştürmelerinin bu profili kullanarak yayımladığınızda uygulanmasına neden olur.

Sihirbaz otomatik olarak **bağlantı** sekmesine ilerler.

**Hizmet URL 'si** kutusuna *localhost*yazın.

**Site/uygulama** kutusuna *varsayılan Web sitesi/contosouniversity*yazın.

**Hedef URL** kutusuna `http://localhost/ContosoUniversity`girin.

**Hedef URL** ayarı gerekli değil. Visual Studio uygulamayı dağıtma işlemini bitirdiğinde varsayılan tarayıcınızı otomatik olarak bu URL 'ye açar. Tarayıcının dağıtımdan sonra otomatik olarak açılmasını istemiyorsanız, bu kutuyu boş bırakın.

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

Ayarların doğru olduğunu doğrulamak için **bağlantıyı doğrula** ' ya tıklayın ve yerel bilgisayarda IIS 'ye bağlanabilirsiniz.

Yeşil onay işareti, bağlantının başarılı olduğunu doğrular.

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

**Ayarlar** sekmesine Ilerlemek için **İleri** ' ye tıklayın.

**Yapılandırma** açılan kutusu, dağıtılacak derleme yapılandırmasını belirtir. Varsayılan değer, istediğiniz şeydir.

**Hedefteki ek dosyaları Kaldır** onay kutusunu işaretsiz bırakın. İlk dağıtımınız olduğundan, hedef klasörde henüz hiçbir dosya olmayacaktır.

**Veritabanları** bölümünde, **SchoolContext**için bağlantı dizesi kutusuna aşağıdaki değeri girin:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

**Çalışma zamanında bu bağlantı dizesini kullan** seçili olduğundan, dağıtım işlemi bu bağlantı dizesini dağıtılan Web. config dosyasına yerleştirir.

Ayrıca, **SchoolContext**altında **Uygula Code First Migrations**' yi seçin. Bu seçenek, dağıtım sürecinin `MigrateDatabaseToLatestVersion` başlatıcısı belirlemek için dağıtılan Web. config dosyasını yapılandırmasına neden olur. Bu başlatıcı, uygulama ilk kez dağıtımdan sonra veritabanına eriştiğinde veritabanını en son sürüme otomatik olarak güncelleştirir.

**DefaultConnection**bağlantı dizesi kutusunda aşağıdaki değeri girin:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

**Güncelleştirme veritabanını** işaretsiz bırak. Üyelik veritabanı, App\_verilerinde. sdf dosyası kopyalanarak dağıtılır ve dağıtım işleminin bu veritabanıyla başka bir şey yapmak istemezsiniz.

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

**Önizleme** sekmesine Ilerlemek için **İleri** ' ye tıklayın.

Kopyalanacak dosyaların listesini görmek için **Önizleme** sekmesinde **önizlemeyi Başlat** ' a tıklayın.

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

**Yayımla**’ta tıklayın.

Visual Studio Yönetici modunda değilse, bir izin hatasını belirten bir hata iletisi alabilirsiniz. Bu durumda, Visual Studio 'yu kapatın, yönetici modunda açın ve yeniden yayımlamayı deneyin.

Visual Studio yönetici modundaysa, **Çıkış** penceresi başarılı derlemeyi ve yayımlamayı raporlar.

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

Tarayıcı, yerel bilgisayarda IIS 'de çalışan Contoso Üniversitesi giriş sayfasında otomatik olarak açılır.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>Test ortamında test etme

Ortam göstergesinin "(dev)" yerine "(test)" gösterdiğine dikkat edin; bu, ortam göstergesinin *Web. config* dönüştürmesinin başarılı olduğunu gösterir.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

Dağıtılan veritabanının öğrenci olmadığını doğrulamak için **öğrenciler** sayfasını çalıştırın. Bu sayfayı seçtiğinizde yüklenmesi birkaç dakika sürebilir çünkü Code First veritabanını oluşturup `Seed` metodunu çalıştırır. (Giriş sayfasında olduğunuzda, uygulama veritabanına henüz erişmeyi denemediği için bu değil.)

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

Code First, veritabanını eğitmen verileriyle birlikte içerdiğini doğrulamak için **eğitmenler** sayfasını çalıştırın:

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

**Öğrenciler menüsünde** **öğrencileri Ekle** ' yi seçin, bir öğrenci ekleyin ve ardından **öğrenciler** sayfasında yeni öğrenci 'yi görüntüleyerek veritabanına başarıyla yazabildiğinizi doğrulayın:

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

**Kurslar** menüsünde **kredileri Güncelleştir**' i seçin. **Kredilerin güncelleştirilmesi** sayfasında yönetici izinleri olması gerekir, bu nedenle **oturum açma** sayfası görüntülenir. Daha önce oluşturduğunuz yönetici hesabı kimlik bilgilerini girin ("admin" ve "pas $ w0rd"). **Kredileri güncelleştirme** sayfası görüntülenir ve bu, önceki öğreticide oluşturduğunuz yönetici hesabının test ortamına doğru şekilde dağıtıldığını doğrular.

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

*ELMAH* klasörünün yalnızca içindeki yer tutucu dosyası ile bulunduğunu doğrulayın.

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>Code First Migrations için otomatik Web. config değişikliklerini gözden geçirme

*C:\ınetpub\wwwroot\contosouniversity* konumundaki dağıtılan uygulamadaki *Web. config* dosyasını açın ve dağıtım işleminin veritabanını en son sürüme otomatik olarak güncelleştirmek için Code First Migrations yapılandırıldığını görebilirsiniz.

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

Dağıtım işlemi, Code First Migrations veritabanı şemasını güncelleştirmek için özel olarak kullanılacak yeni bir bağlantı dizesi de oluşturmuştur:

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

Bu ek bağlantı dizesi, veritabanı şeması güncelleştirmeleri için bir kullanıcı hesabı ve uygulama verileri erişimi için farklı bir kullanıcı hesabı belirtmenizi sağlar. Örneğin, DB\_Owner rolünü Code First Migrations ve DB\_DataReader ve DB\_DataWriter rollerine atayabilirsiniz. Bu, uygulamadaki zararlı olabilecek kodun veritabanı şemasını değiştirmesini engelleyen yaygın bir savunma derinlemesine bir modeldir. (Örneğin, bu durum başarılı bir SQL ekleme saldırısında olabilir.) Bu model bu öğreticiler tarafından kullanılmaz. SQL Server Compact için uygulanmaz ve bu serinin sonraki bir öğreticide SQL Server geçirdiğinizde uygulanmaz. Cytanium sitesi, Cytanium adresinde oluşturduğunuz SQL Server veritabanına erişmek için yalnızca bir kullanıcı hesabı sunar. Senaryonuza bu kalıbı uygulayabiliyorsanız, aşağıdaki adımları gerçekleştirerek bunu yapabilirsiniz:

1. **Web 'ı Yayımla** sihirbazının **Ayarlar** sekmesinde, tam veritabanı şeması güncelleştirme izinlerine sahip bir Kullanıcı belirten bağlantı dizesini girin ve **çalışma zamanında bu bağlantı dizesini kullan** onay kutusunu temizleyin. Dağıtılan Web. config dosyasında bu `DatabasePublish` bağlantı dizesi olur.
2. Uygulamanın çalışma zamanında kullanmasını istediğiniz bağlantı dizesi için bir Web. config dosyası dönüştürmesi oluşturun.

Uygulamanızı geliştirme bilgisayarınızda IIS 'e dağıtmış ve orada test edersiniz. Bu, dağıtım işleminin uygulamanın içeriğini doğru konuma (dağıtmak istemediğiniz dosyalar hariç) kopyaladığını ve ayrıca dağıtım sırasında Web Dağıtımı IIS 'nin doğru şekilde yapılandırıldığını doğrular. Sonraki öğreticide, henüz yapılmamış bir dağıtım görevini bulan bir test daha çalıştıracaksınız: *ELMAH* klasöründe klasör izinlerini ayarlama.

## <a name="more-information"></a>Daha Fazla Bilgi

IIS veya IIS Express Visual Studio 'da çalıştırma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- IIS.net sitesinde [genel bakış IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) .
- Scott Guthrie 'nin bloguna [IIS Express tanıtımı](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) .
- [Nasıl yapılır: Visual Studio 'Da Web projeleri Için Web sunucusu belirtme](https://msdn.microsoft.com/library/ms178108.aspx).
- ASP.NET sitesindeki [IIS ve ASP.NET geliştirme sunucusu arasındaki temel farklılıklar](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) .
- [ASP.NET MVC veya Web Forms UYGULAMANıZıN IIS 7 ' de Rick Anderson 'nin blogu üzerinde 30 saniye Içinde test edin](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) . Bu giriş, Visual Studio geliştirme sunucusu (Cassini) ile testlerin neden IIS Express test olarak güvenilir olmadığını ve IIS Express içindeki testlerin IIS 'de test olarak güvenilir olmadığı konusunda örnekler sağlar.

Uygulamanız Orta güvende çalıştığında oluşabilecek sorunlar hakkında daha fazla bilgi için, bkz. The [ASP.net Applications](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the The The The The The The The The The Rolla site.

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [İleri](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
