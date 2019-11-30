---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: "Visual Studio kullanarak ASP.NET Web dağıtımı: test 'e dağıtma | Microsoft Docs"
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 738318cce442fdc5d58dd1e4c992d4941be2487e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591248"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a>Visual Studio kullanarak ASP.NET Web dağıtımı: test 'e dağıtma

[Tom Dykstra](https://github.com/tdykstra) tarafından

Bu öğretici serisi, Visual Studio 2017 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

Azure 'a dağıtmanın güncel bir sürümü için bkz. [Azure 'da ASP.NET Core Web uygulaması oluşturma](/azure/app-service/app-service-web-get-started-dotnet).

## <a name="overview"></a>Genel bakış

Bu öğreticide, yerel bilgisayarınızda Internet Information Server 'a (IIS) bir ASP.NET Web uygulaması dağıtırsınız.

Genellikle bir uygulama geliştirirken, çalıştırın ve Visual Studio 'da test edersiniz. Varsayılan olarak, Visual Studio 2017 ' deki Web uygulaması projeleri geliştirme Web sunucusu olarak IIS Express kullanır. IIS Express, Visual Studio geliştirme sunucusundan (Cassini olarak da bilinir) tam IIS gibi davranır, bu da Visual Studio 2017 'nin varsayılan olarak kullandığı. Ancak, geliştirme Web sunucusu tam olarak IIS gibi bir işe yarar. Sonuç olarak, bir uygulama Visual Studio 'da doğru şekilde çalışabilir ve test verebilir, ancak IIS 'e dağıtıldığında başarısız olur.

Uygulamanızı iki şekilde güvenilir bir şekilde test edebilirsiniz:

1. Uygulamanızı üretim ortamınıza dağıtmak üzere daha sonra kullanacağınız süreci kullanarak geliştirme bilgisayarınızda IIS 'e dağıtın.

   Visual Studio 'Yu bir Web projesi çalıştırdığınızda IIS kullanmak üzere yapılandırabilirsiniz, ancak bu, dağıtım işleminizi test edebilir. Bu yöntem, dağıtım işleminizi doğrular ve uygulamanız IIS altında doğru şekilde çalışır.

2. Uygulamanızı üretim ortamınıza benzer bir test ortamına dağıtın. 
 
   Bu öğreticiler için üretim ortamı Azure App Service Web Apps. İdeal test ortamı, Azure hizmetinde oluşturulmuş ek bir Web uygulamasıdır. Aynı şekilde, bir üretim Web uygulamasıyla aynı şekilde ayarlanacaksa, yalnızca test için kullanacaksınız.

2\. seçenek, test etmenin en güvenilir yoludur. Seçenek 2 ' yi kullanırsanız, 1 seçeneğini kullanmanız gerekmez. Ancak, üçüncü taraf bir barındırma sağlayıcısına dağıtım yapıyorsanız, 2. seçenek uygun olmayabilir veya pahalı olabilir, bu nedenle bu öğretici serisi her iki yöntemi de gösterir. 2\. seçenek Kılavuzu, [üretim ortamına dağıtma](deploying-to-production.md) öğreticisinde verilmiştir.

Visual Studio 'da Web sunucuları kullanma hakkında daha fazla bilgi için bkz. [ASP.NET Web projeleri Için Visual Studio 'Da Web sunucuları](https://msdn.microsoft.com/library/58wxa9w5.aspx).

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey işe yaramazsa, [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.

## <a name="download-the-contoso-university-starter-project"></a>Contoso Üniversitesi başlangıç projesini indirin

Contoso Üniversitesi Visual Studio başlangıç çözümünü ve projesini indirin ve yükleyin. Bu çözüm tamamlanmış öğreticiyi içerir. 

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a>IIS 'yi yükler

Geliştirme bilgisayarınızda IIS 'e dağıtmak için IIS ve Web Dağıtımı yüklü olduğunu doğrulayın. Varsayılan olarak, Visual Studio Web Dağıtımı yüklenir, ancak IIS varsayılan Windows 10, Windows 8 veya Windows 7 yapılandırmasına dahil değildir. Daha önce IIS yüklediyseniz ve varsayılan uygulama havuzu zaten .NET 4 ' e ayarlandıysa, [sonraki bölüme](#sqlexpress)atlayın.

1. IIS ve Web Dağıtımı yüklemek için [Web Platformu Yükleyicisi 'ni (WPı)](https://www.microsoft.com/web/downloads/platform.aspx) kullanmanız önerilir. WPı, gerekirse IIS ve Web Dağıtımı önkoşulları içeren önerilen bir IIS yapılandırması yüklüyor.

   IIS, Web Dağıtımı veya gerekli bileşenlerinden herhangi birini zaten yüklediyseniz, WPı yalnızca eksik olanları da yüklüyor.

   * IIS ve Web Dağıtımı yüklemek için Web Platformu Yükleyicisi 'ni kullanın:
    
     ![WPI kullanarak IIS 'yi yükler](deploying-to-iis/_static/image30.png)

     ![WPI kullanarak Web Dağıtımı yüklemesi](deploying-to-iis/_static/image31.png)

     IIS 7 ' nin yükleneceğini belirten iletiler görürsünüz. Bağlantı, Windows 8 ' de IIS 8 için geçerlidir; Ancak, Windows 8 ve üzeri için, ASP.NET 4,7 ' nin yüklü olduğundan emin olmak için aşağıdaki adımları izleyin:

   * Programlar **ve özellikler** >  > **Windows özelliklerini açıp kapatmak**Için **Denetim Masası** > **Programlar** 'ı açın.

   * **Internet Information Services**, **World Wide Web Hizmetleri**ve **uygulama geliştirme özellikleri**' ni genişletin.
   
   * **ASP.NET 4,7** ' ın seçili olduğunu doğrulayın.

     ![ASP.NET 4,7 seçin](deploying-to-iis/_static/image1a.png)

   * **World Wide Web Services** ve **IIS Yönetim konsolunun** seçili olduğunu doğrulayın. Bu, IIS ve IIS Yöneticisi 'Ni kurar.
    
     ![World Wide Web hizmetleri seçin](deploying-to-iis/_static/image24.png)    
  
   * **Tamam ' ı**seçin. Yükleme gerçekleşmediğini belirten iletişim kutusu iletileri görüntülenir.

IIS yüklendikten sonra, .NET Framework sürüm 4 ' ün varsayılan uygulama havuzuna atandığından emin olmak için **IIS Yöneticisi 'ni** çalıştırın.

1. **Çalıştır** iletişim kutusunu açmak için WINDOWS + R tuşlarına basın.

   (Windows 8 veya sonraki sürümlerde, **Başlangıç** sayfasına "Çalıştır" yazın. Windows 7 ' de, **Başlat** menüsünden **Çalıştır** ' ı seçin. **Çalıştır** **Başlat** menüsünde değilse, görev çubuğuna sağ tıklayın, **Özellikler**' i seçin, **Başlat menüsü** sekmesini seçin, **Özelleştir**' i seçin ve **komutu Çalıştır**' ı seçin.)

2. "İnetmgr" yazın ve **Tamam**' ı seçin.

3. **Bağlantılar** bölmesinde, sunucu düğümünü genişletin ve **uygulama havuzları**' nı seçin. **Uygulama havuzları** bölmesinde, aşağıdaki çizimde gösterildiği gibi, **DefaultAppPool** .NET Framework sürüm 4 ' e atanırsa, sonraki bölüme atlayın.

   ![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image5a.png)

4. Yalnızca iki uygulama havuzu görürseniz ve her ikisi de .NET Framework 2,0 olarak ayarlanırsa, IIS 'de ASP.NET 4 ' ü yükleyebilirsiniz.

   Windows 8 veya üzeri için, ASP.NET 4,7 ' nin yüklü olduğundan emin olmak için önceki bölüme bakın veya bkz. [Windows 8 ve Windows Server 2012 üzerinde ASP.NET 4,5 ' yi yükleme](https://support.microsoft.com/kb/2736284). Windows 7 için Windows **Başlat** menüsünde **komut istemi** ' ni sağ tıklatıp **yönetici olarak çalıştır**' ı seçerek bir komut istemi penceresi açın. Aşağıdaki komutları kullanarak IIS 'de ASP.NET 4 ' ü yüklemek için [aspnet\_regııs. exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) ' yi çalıştırın. (32 bitlik sistemlerde, "Framework64" değerini "Framework" ile değiştirin.)

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   Bu komut .NET Framework 4 için yeni uygulama havuzları oluşturur, ancak varsayılan uygulama havuzu 2,0 olarak ayarlanmıştır. .NET 4 ' ü hedefleyen bir uygulamayı bu uygulama havuzuna dağıtmakta olursunuz, bu nedenle uygulama havuzunu .NET 4 ' e değiştirin.

5. **IIS Yöneticisi 'ni**kapattıysanız, yeniden çalıştırın, sunucu düğümünü genişletin ve **uygulama havuzları**' nı seçin.

6. **Uygulama havuzları** bölmesinde, **DefaultAppPool**' ı seçin. **Eylemler** bölmesinde **temel ayarlar**' ı seçin.

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. **Uygulama havuzunu Düzenle** iletişim kutusunda **.NET CLR sürümünü** **.NET CLR v 4.0.30319**olarak değiştirin. **Tamam ' ı**seçin.

   ![Selecting_. NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

Artık bir Web uygulamasını IIS 'de yayımlamaya hazırsınız. Ancak, öncelikle test için veritabanları oluşturun.

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a>SQL Server Express yüklensin

LocalDB, IIS 'de çalışmak üzere tasarlanmamıştır, bu nedenle test ortamınızın SQL Server Express yüklü olması gerekir. Visual Studio 2010 SQL Server Express kullanıyorsanız, varsayılan olarak zaten yüklüdür. Visual Studio 2012 veya sonraki bir sürümü kullanıyorsanız SQL Server Express ' yi yükleyebilirsiniz.

SQL Server Express yüklemek için indirme merkezi 'nden indirin ve yükleyin [: Microsoft SQL Server 2017 Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express). 

SQL Server Yükleme Merkezi ' nin ilk sayfasında, **yeni SQL Server tek başına yükleme ' yi seçin veya var olan bir yüklemeye özellikler ekleyin** ve varsayılan seçimleri kabul eden yönergeleri izleyin. Yükleme sihirbazında, varsayılan ayarları kabul edin. Yükleme seçenekleri hakkında daha fazla bilgi için bkz. [Yükleme sihirbazından SQL Server yükleme (Kurulum)](https://msdn.microsoft.com/library/ms143219.aspx).

## <a name="create-sql-server-express-databases-for-the-test-environment"></a>Test ortamı için SQL Server Express veritabanları oluşturun

Contoso Üniversitesi uygulaması iki veritabanına sahiptir: 

1. Üyelik veritabanı 
2. Uygulama veritabanı 

Bu veritabanlarını iki ayrı veritabanına veya tek bir veritabanına dağıtabilirsiniz. Bunları birleştirmek, aralarında veritabanı birleştirmeleri daha kolay hale getirir. 

Üçüncü taraf bir barındırma sağlayıcısına dağıtım yapıyorsanız barındırma planınız, bunları birleştirme nedeninizi de verebilir. Örneğin, sağlayıcı birden fazla veritabanı için daha fazla ücret alabilir veya birden fazla veritabanına izin verebilir.

Bu öğreticide, test ortamında iki veritabanına ve hazırlama ve üretim ortamlarındaki bir veritabanına dağıtırsınız.

Visual Studio 'daki **Görünüm** menüsünden **Sunucu Gezgini** (visual Web Developer 'da**veritabanı Gezgini** ) öğesini seçin. **Veri bağlantıları** ' na sağ tıklayın ve **Yeni SQL Server veritabanı oluştur**' u seçin.

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

**Yeni SQL Server veritabanı oluştur** iletişim kutusunda, **sunucu adı** kutusuna ".\SQLEXPRESS" ve **Yeni veritabanı adı** kutusuna "ASPNET-contosouniversity" yazın. **Tamam ' ı**seçin.

![ASPNET-ContosoUniversity oluşturma](deploying-to-iis/_static/image9.png)

`ContosoUniversity`adlı yeni bir SQL Server Express okul veritabanı oluşturmak için aynı yordamı izleyin.

**Sunucu Gezgini** iki yeni veritabanını gösterir.

![Sunucu Gezgini yeni veritabanları](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a>Yeni veritabanları için bir verme betiği oluşturun

Uygulama, geliştirme bilgisayarınızda IIS 'de çalıştığında, uygulama, veritabanına erişmek için varsayılan uygulama havuzunun kimlik bilgilerini kullanır. Ancak, varsayılan olarak, uygulama havuzunun veritabanlarını açma izni yoktur. Bu izin vermek için bir komut dosyası çalıştırmanız gereken anlamına gelir. Bu bölümde, uygulamanın IIS 'de çalıştırıldığında veritabanlarını açabildiğinden emin olmak için bu betiği oluşturacak ve daha sonra çalıştıracaksınız.

Bir metin düzenleyicisinde, aşağıdaki SQL komutlarını yeni bir dosyaya kopyalayın ve *ver. SQL*olarak kaydedin. 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

Visual Studio 'da Contoso Üniversitesi çözümünü açın. Çözüme (projelerden birine değil) sağ tıklayın ve **Ekle**' yi seçin. **Mevcut öğe**' yi seçin, *izin ver. SQL*' e gidin ve açın.

> [!NOTE]
> Bu komut dosyası, bu öğreticide belirtildiği üzere Windows 10, Windows 8 veya Windows 7 ' de SQL Server Express 2012 veya sonraki bir sürümüyle çalışmak üzere tasarlanmıştır. SQL Server veya Windows 'un farklı bir sürümünü kullanıyorsanız veya IIS 'yi bilgisayarınızda farklı şekilde ayarlarsanız, bu betikteki değişiklikler gerekli olabilir. SQL Server betikler hakkında daha fazla bilgi için bkz. [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).

> [!NOTE] 
> **Güvenlik notunun** Bu betik, çalışma zamanında veritabanına erişen kullanıcıya `db_owner` izinleri verir. Bu, üretim ortamında sahip olduğunuz şeydir. Bazı senaryolarda, yalnızca dağıtım için tam veritabanı şeması güncelleştirme izinlerine sahip bir Kullanıcı belirtmek ve yalnızca verileri okuma ve yazma izinlerine sahip farklı bir kullanıcının çalışma süresini belirtmek isteyebilirsiniz. Daha fazla bilgi için, bu öğreticide daha sonra [Code First Migrations Için otomatik Web. config değişikliklerini gözden geçirme](#reviewingmigrations) bölümüne bakın.

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a>Uygulama veritabanında verme betiğini çalıştırma

Veritabanı dağıtımı [Dbdacfx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) sağlayıcısını kullandığından, yayımlama profilini dağıtım sırasında üyelik veritabanında çalıştıracak şekilde yapılandırabilirsiniz. Uygulama veritabanını dağıtma yöntemi olan Code First Migrations dağıtım sırasında betikleri çalıştıramazsınız. Bu, uygulama veritabanında dağıtımdan önce betiği el ile çalıştırmanız gerektiği anlamına gelir.

1. Visual Studio 'da daha önce oluşturduğunuz *ver. SQL* dosyasını açın.

2. **Bağlan**' ı seçin. 

    ![Bağlan düğmesi](deploying-to-iis/_static/image11.png)

3. **Sunucuya Bağlan** iletişim kutusunda, **sunucu adı**olarak *.\SQLEXPRESS* yazın. **Bağlan**' ı seçin.

4. Veritabanı açılan listesinde **Contosouniversity**' i seçin. **Yürüt**' ü seçin. 

   ![](deploying-to-iis/_static/image12.png)

Uygulama çalışırken veritabanı tabloları oluşturmak için, varsayılan uygulama havuzu kimliği artık uygulama veritabanında yeterli izinlere sahip Code First Migrations.

## <a name="publish-to-iis"></a>IIS 'de Yayımla

Visual Studio ve Web Dağıtımı kullanarak IIS 'ye dağıtabileceğiniz çeşitli yollar vardır:

* Visual Studio tek tıklamayla Yayımla 'yı kullanın.
* Komut satırından yayımlayın.
* Bir dağıtım paketi oluşturun ve IIS Yöneticisi 'Ni kullanarak yüklemeyi yapın. Paket, IIS 'de bir site yüklemek için gereken tüm dosya ve meta verileri içeren bir. zip dosyasına sahiptir.
* Bir dağıtım paketi oluşturun ve komut satırını kullanarak yüklemeyi yapın.

Önceki öğreticilerde, Visual Studio 'Yu otomatik hale getirmek için ayarlama işlemi, bu yöntemlerin tümü için geçerlidir. Bu öğreticilerde, ilk iki yöntemi kullanacaksınız. Dağıtım paketlerini kullanma hakkında daha fazla bilgi için bkz. Visual Studio ve ASP.NET için Web dağıtımı Içerik haritasında Web [dağıtım paketi oluşturarak ve yükleyerek Web uygulaması dağıtma](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) .

Yayımlamadan önce, Visual Studio 'Yu yönetici modunda çalıştırdığınızdan emin olun. Başlık çubuğunda **(yönetici)** öğesini görmüyorsanız Visual Studio 'yu kapatın. Windows 8 (veya üzeri) **Başlangıç** sayfasında veya Windows 7 **Başlat** menüsünde, Visual Studio simgesine sağ tıklayıp **yönetici olarak çalıştır**' ı seçin. Yönetici modu yalnızca yerel bilgisayarda IIS 'e yayımlarken yayımlama için gereklidir.

### <a name="create-the-publish-profile"></a>Yayımlama profili oluşturma

1. **Çözüm Gezgini**, **contosouniversity** projesine ( **contosouniversity. dal** projesi değil) sağ tıklayın. **Yayımla**' yı seçin. **Yayımla** sayfası görüntülenir.

2. **Yeni profil**' i seçin. **Bir Yayımla hedefi seç** iletişim kutusu görüntülenir.

3. **IIS, FTP, vb**. seçin. **Profil oluştur**' u seçin. **Yayımla** Sihirbazı görüntülenir.

   ![Web Yayımlama Sihirbazı profil sekmesi](deploying-to-iis/_static/image26.png)

4. **Yayımla yöntemi** açılan menüsünden **Web dağıtımı**' yi seçin.

5. **Sunucu**için *localhost*girin.

6. **Site adı**Için *varsayılan Web sitesi/contosouniversity*yazın.

7. **Hedef URL 'si**için *http://localhost/ContosoUniversity* girin.

   **Hedef URL** ayarı gerekli değil. Visual Studio uygulamayı dağıtma işlemini bitirdiğinde varsayılan tarayıcınızı otomatik olarak bu URL 'ye açar. Tarayıcının dağıtımdan sonra otomatik olarak açılmasını istemiyorsanız, bu kutuyu boş bırakın.

8. Ayarların doğru olduğunu doğrulamak için **bağlantıyı doğrula** ' yı seçin ve yerel bilgisayarda IIS 'ye bağlanabilirsiniz.

   Yeşil onay işareti, bağlantının başarılı olduğunu doğrular.

   ![Web 'i Yayımlama Sihirbazı bağlantı sekmesi](deploying-to-iis/_static/image27.png)

9. **Ayarlar** sekmesine Ilerlemek için **İleri ' yi** seçin.

10. **Yapılandırma** açılan kutusu, dağıtılacak derleme yapılandırmasını belirtir. Varsayılan **Sürüm**değerine ayarlı bırakın. Bu öğreticide hata ayıklama derlemeleri dağıtmazsınız.

11. **Dosya yayımlama seçeneklerini**genişletin. **Dosyaları uygulama\_veri klasöründen hariç tut**' u seçin.

    Uygulama, test ortamında, *App\_Data* klasöründeki. mdf dosyalarını değil, yerel SQL Server Express örneğinde oluşturduğunuz veritabanlarına erişir.

12. **Yayımlama sırasında ön derlemeyi** bırakın ve **Hedefteki ek dosyaları kaldırın** onay kutularını işaretsiz bırakın.

    ![Ayarlar sekmesinde dosya yayımlama seçenekleri](deploying-to-iis/_static/image15a.png)

    Ön derleme, genellikle büyük siteler için yararlı olan bir seçenektir. Site yayımlandıktan sonra ilk kez bir sayfa istendiğinde başlangıç süresini azaltabilir.

    Bu ilk dağıtımınız olduğundan ve hedef klasörde henüz hiçbir dosya olmadığından, ek dosyaları kaldırmanız gerekmez.

    > [!NOTE] 
    > Aynı siteye sonraki bir dağıtım için **Hedefteki ek dosyaları Kaldır** ' ı seçerseniz, dağıtım yapmadan önce hangi dosyaların silineceğini önceden görmeniz için önizleme özelliğini kullandığınızdan emin olun. Beklenen davranış, Web Dağıtımı projenizde sildiğiniz hedef sunucudaki dosyaları silecek. Ancak, kaynak ve hedef klasörler altındaki tüm klasör yapısı karşılaştırılır; Web Dağıtımı, bazı senaryolarda silmek istemediğiniz dosyaları silebilir.
    > 
    > Örneğin, kök klasöre bir proje dağıtırken sunucuda bir alt klasörde Web uygulamanız varsa, alt klasör silinir. Contoso.com adresinde ana site için bir projeniz ve contoso.com/blog adresinde blog için başka bir proje olabilir. Blog uygulaması bir alt klasör içinde. Ana siteyi dağıtırken **Hedefteki ek dosyaları Kaldır** ' ı seçerseniz, Blog uygulaması silinir.
    > 
    > Başka bir örnek için, uygulama\_veri klasörünüz beklenmedik bir şekilde silinebilir. SQL Server Compact gibi belirli veritabanları, veritabanı dosyalarını uygulama\_veri klasöründe depolar. İlk dağıtımdan sonra, veritabanı dosyalarını sonraki dağıtımlarda kopyalamaya devam etmek istemezsiniz, bu nedenle **uygulama\_verilerini** paket/Yayımla sekmesinde hariç tut ' u seçersiniz. Seçili **Hedefteki ek dosyaları kaldırırsanız** , veritabanı dosyalarınız ve uygulama\_veri klasörünün kendisi bir sonraki yayımladıktan sonra silinir.

### <a name="configure-deployment-for-the-membership-database"></a>Üyelik veritabanı için dağıtımı yapılandırma

Aşağıdaki adımlar, iletişim kutusunun **veritabanları** bölümünde **DefaultConnection** veritabanı için geçerlidir.

1. **Uzak bağlantı dizesi** kutusuna yeni SQL Server Express üyelik veritabanına işaret eden aşağıdaki bağlantı dizesini girin.

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   **Çalışma zamanında bu bağlantı dizesini kullan** seçili olduğundan, dağıtım işlemi bu bağlantı dizesini dağıtılan Web. config dosyasına koyar.

    Bağlantı dizesini **Sunucu Gezgini**de alabilirsiniz. **Sunucu Gezgini**, **veri bağlantıları** ' nı genişletin ve **&lt;MachineName&gt;\sqlexpress.aspnet-ContosoUniversity** veritabanını seçin ve ardından **Özellikler** penceresinden **bağlantı dizesi** değerini kopyalayın. Bu bağlantı dizesinde silebilmeniz için kullanabileceğiniz bir ek ayar olacaktır: `Pooling=False`.

2. **Veritabanını güncelleştir**' i seçin.

   Bu, veritabanı şemasının dağıtım sırasında hedef veritabanında oluşturulmasına neden olur. Sonraki adımlarda, çalıştırmak için gereken ek betikleri belirtin: bir veritabanı, varsayılan uygulama havuzuna ve diğeri veri dağıtmaya erişim vermek için.

3. **Veritabanı güncelleştirmelerini Yapılandır**' ı seçin.
 
4. **Veritabanı güncelleştirmelerini Yapılandır** ILETIŞIM kutusunda **SQL betiği Ekle**' yi seçin. Daha önce çözüm klasöründen kaydettiğiniz *Grant. SQL* betiğine gidin.

5. *ASPNET-Data-dev. SQL* betiğini eklemek için işlemi tekrarlayın.

   ![Üyelik veritabanı için veritabanı güncelleştirmelerini yapılandırma](deploying-to-iis/_static/image16.png)

6. **Kapat**' ı seçin.

### <a name="configure-deployment-for-the-application-database"></a>Uygulama veritabanı için dağıtımı yapılandırma

Visual Studio bir Entity Framework `DbContext` sınıfı algıladığında, bir **güncelleştirme veritabanı** yerine **yürütme Code First Migrations** onay kutusu olan **veritabanları** bölümünde bir giriş oluşturur. Bu öğreticide, Code First Migrations dağıtımı belirtmek için bu onay kutusunu kullanacaksınız.

Bazı senaryolarda, veritabanı dağıtmak için geçiş yerine dbDacFx sağlayıcısını kullanmak istiyorsanız bir `DbContext` veritabanı kullanıyor olabilirsiniz. Bu durumda, MSDN 'de ASP.NET Web dağıtımı hakkında SSS bölümüne bakın [nasıl yaparım?, geçiş olmadan Code First veritabanı dağıtma](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) .

Aşağıdaki adımlar iletişim kutusunun **veritabanları** bölümünde **SchoolContext** veritabanı için geçerlidir.

1. **Uzak bağlantı dizesi** kutusuna yeni SQL Server Express uygulama veritabanına işaret eden aşağıdaki bağlantı dizesini girin.

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   **Çalışma zamanında bu bağlantı dizesini kullan** seçili olduğundan, dağıtım işlemi bu bağlantı dizesini dağıtılan Web. config dosyasına koyar.

   Uygulama veritabanı bağlantı dizesini, üyelik veritabanı bağlantı dizesiyle aynı şekilde **Sunucu Gezgini** de alabilirsiniz.

2. **Code First Migrations Yürüt ' ü seçin (uygulama başlatma üzerinde çalışır)** .

   Bu seçenek, dağıtım sürecinin `MigrateDatabaseToLatestVersion` başlatıcısı belirlemek için dağıtılan Web. config dosyasını yapılandırmasına neden olur. Bu başlatıcı, uygulama ilk kez dağıtımdan sonra veritabanına eriştiğinde veritabanını en son sürüme otomatik olarak güncelleştirir.

### <a name="configure-publish-profile-transforms"></a>Yayımlama profili dönüşümlerini yapılandırma

1. **Kapat**' ı seçin. Değişiklikleri kaydetmek isteyip istemediğiniz sorulduğunda **Evet** ' i seçin.

2. **Çözüm Gezgini**, **Özellikler**' i genişletin, **publishprofiles**' ı genişletin.

3. *Customprofile. pubxml* öğesine sağ tıklayın ve *test. pubxml*olarak yeniden adlandırın.

4. *Test. pubxml*öğesine sağ tıklayın. **Yapılandırma dönüşümü Ekle**' yi seçin.

   ![Yapılandırma dönüştürme menüsü Ekle](deploying-to-iis/_static/image17.png)

   Visual Studio *Web. test. config* dönüştürme dosyasını oluşturur ve açar.

5. *Web. test. config* dönüştürme dosyasında, açma yapılandırması etiketinden hemen sonra aşağıdaki kodu ekleyin.

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    Test yayımlama profilini kullandığınızda, bu dönüşüm ortam göstergesini "test" olarak ayarlar. Dağıtılan sitede "Contoso Üniversitesi" H1 başlığından sonra "(test)" görürsünüz.

6. Dosyayı kaydedin ve kapatın.

7. *Web. test. config* dosyasına sağ tıklayın ve kodlanmış dönüşümün beklenen değişiklikleri ürettiğinden emin olmak Için **Önizleme dönüşümü** ' nü seçin.

    **Web. config önizleme** penceresinde hem *Web. Release. config* dönüştürmeleri hem de *Web. test. config* dönüşümleri uygulamanın sonucu gösterilir.

### <a name="preview-the-deployment-updates"></a>Dağıtım güncelleştirmelerini önizleyin

1. Web 'i **Yayımla** sihirbazını yeniden açın (contosouniversity projesine sağ tıklayın, **Yayımla**' yı ve ardından **Önizleme**' yi seçin).

2. **Önizleme** iletişim kutusunda, kopyalanacak dosyaların listesini görmek Için **önizlemeyi Başlat** ' ı seçin. 

   ![Önizlemeyi Yayımla](deploying-to-iis/_static/image29.png)

   Ayrıca, üyelik veritabanında çalıştırılacak betikleri görmek için **Önizleme veritabanı** bağlantısını da seçebilirsiniz. (Code First Migrations dağıtım için hiçbir betik çalıştırılmadı, bu nedenle uygulama veritabanının önizlemesi için bir şey yok.)

3. **Yayımla**' yı seçin.

   Visual Studio Yönetici modunda değilse, bir izin hata iletisi alabilirsiniz. Bu durumda, Visual Studio 'yu kapatın, yönetici modunda açın ve yeniden yayımlamayı deneyin.

   Visual Studio yönetici modundaysa, **Çıkış** penceresi başarılı derlemeyi ve yayımlamayı raporlar.

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   Profil **bağlantısı** Yayımla SEKMESINDEKI **hedef URL** kutusuna URL 'yi girdiyseniz, tarayıcı otomatik olarak bilgisayarınızda IIS 'de çalışan Contoso Üniversitesi giriş sayfasında açılır.

## <a name="test-in-the-test-environment"></a>Test ortamında test

Ortam göstergesinin "(dev)" yerine "(test)" gösterdiğine dikkat edin. Bu, ortam göstergesinin *Web. config* dönüştürmesinin başarılı olduğunu gösterir.

Code First, veritabanını eğitmen verileriyle içerdiğini doğrulamak için **eğitmenler** sayfasını çalıştırın. Bu sayfayı seçtiğinizde yüklenmesi birkaç dakika sürebilir çünkü Code First veritabanını oluşturup `Seed` metodunu çalıştırır. (Giriş sayfasında olduğunuzda, uygulama veritabanına henüz erişmeyi denemediği için bu değil.)

Dağıtılan veritabanının öğrenci olmadığını doğrulamak için **öğrenciler** sekmesini seçin.

**Öğrenciler** menüsünden **öğrenci Ekle** ' yi seçin. Öğrenci ekleyin ve ardından **öğrenciler** sayfasında yeni öğrenci 'yi görüntüleyin. Bu, veritabanına başarıyla yazabildiğini doğrular.

**Kurslar** menüsünde **kredileri Güncelleştir**' i seçin. **Kredilerin güncelleştirilmesi** sayfasında yönetici izinleri olması gerekir, bu nedenle **oturum açma** sayfası görüntülenir. Daha önce oluşturduğunuz yönetici hesabı kimlik bilgilerini girin ("admin" ve "devpwd"). **Kredileri güncelleştirme** sayfası görüntülenir. Bu, önceki öğreticide oluşturduğunuz yönetici hesabının, test ortamına doğru şekilde dağıtıldığını doğrular.

*C:\inetpub\wwwroot\contosouniversity* klasöründe yalnızca içindeki yer tutucu dosyasına sahip bir *ELMAH* klasörü bulunduğunu doğrulayın.

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a>Code First Migrations için otomatik Web. config değişikliklerini gözden geçirin

*C:\ınetpub\wwwroot\contosouniversity* konumundaki dağıtılan uygulamadaki *Web. config* dosyasını açın ve dağıtım işleminin veritabanını en son sürüme otomatik olarak güncelleştirmek için Code First Migrations yapılandırıldığını görebilirsiniz.

![](deploying-to-iis/_static/image21.png)

Dağıtım işlemi, Code First Migrations veritabanı şemasını güncelleştirmek için özel olarak kullanılacak yeni bir bağlantı dizesi de oluşturmuştur:

![Database_Publish bağlantı dizesi](deploying-to-iis/_static/image22.png)

Bu ek bağlantı dizesi, veritabanı şeması güncelleştirmeleri için bir kullanıcı hesabı ve uygulama veri erişimi için farklı bir kullanıcı hesabı belirtmenizi sağlar. Örneğin, DB **\_Owner** rolünü, DB **\_datawriter** rollerine sahip Code First Migrations ve **DB\_DataReader** 'a atayabilirsiniz. Bu, uygulamadaki zararlı olabilecek kodun veritabanı şemasını değiştirmesini engelleyen yaygın bir savunma derinlemesine bir modeldir. (Örneğin, bu durum başarılı bir SQL ekleme saldırısında olabilir.) Bu öğreticiler bu kalıbı kullanmaz. Senaryonuza bu kalıbı uygulamak için şu adımları uygulayın:

1. Web 'i **Yayımla** sihirbazında **Ayarlar** sekmesinde, tam veritabanı şeması güncelleştirme izinlerine sahip bir Kullanıcı belirten bağlantı dizesini girin. **Çalışma zamanında bu bağlantı dizesini kullan** onay kutusunu temizleyin. Dağıtılan Web. config dosyasında bu `DatabasePublish` bağlantı dizesi olur.

2. Uygulamanın çalışma zamanında kullanmasını istediğiniz bağlantı dizesi için bir Web. config dosyası dönüştürmesi oluşturun.

## <a name="summary"></a>Özet

Artık uygulamanızı geliştirme bilgisayarınızda IIS 'e dağıtmış ve bu uygulamayı test edersiniz.

![Testteki giriş sayfası](deploying-to-iis/_static/image23.png)

Bu, dağıtım işleminin uygulamanın içeriğini doğru konuma (dağıtmak istemediğiniz dosyalar hariç) kopyaladığını ve ayrıca dağıtım sırasında Web Dağıtımı IIS 'nin doğru şekilde yapılandırıldığını doğrular. Sonraki öğreticide, henüz yapılmamış bir dağıtım görevini bulan bir test daha çalıştıracaksınız: *ağaç \ Ah* klasöründe klasör izinlerini ayarlama.

## <a name="more-information"></a>Daha fazla bilgi

IIS veya IIS Express Visual Studio 'da çalıştırma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- IIS.net sitesinde [genel bakış IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) .
- Scott Guthrie 'nin bloguna [IIS Express tanıtımı](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) .
- [ASP.NET Web projeleri Için Visual Studio 'Daki Web sunucuları](https://msdn.microsoft.com/library/58wxa9w5.aspx).
- ASP.NET sitesindeki [IIS ve ASP.NET geliştirme sunucusu arasındaki temel farklılıklar](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) .

Uygulamanız Orta güvende çalıştığında oluşabilecek sorunlar hakkında daha fazla bilgi için, bkz. [ASP.NET uygulamalarını](http://www.4guysfromrolla.com/articles/100307-1.aspx) , dla sitesinden dört guys üzerinde barındırma.

> [!div class="step-by-step"]
> [Önceki](project-properties.md)
> [İleri](setting-folder-permissions.md)
