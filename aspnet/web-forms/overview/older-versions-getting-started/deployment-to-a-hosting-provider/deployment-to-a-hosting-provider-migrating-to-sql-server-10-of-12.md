---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: "Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: SQL Server 'a geçme-10/12 | Microsoft Docs"
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573467"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: SQL Server geçiş-10/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bu öğreticide, SQL Server Compact SQL Server ' den nasıl geçiş yapılacağı gösterilmektedir. Bunu yapmak isteyebileceğiniz bir neden, saklı yordamlar, Tetikleyiciler, görünümler veya çoğaltma gibi SQL Server Compact desteklemediği SQL Server özelliklerden faydalanabilir. SQL Server Compact ve SQL Server arasındaki farklar hakkında daha fazla bilgi için bkz. [dağıtım SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) öğreticisi.

### <a name="sql-server-express-versus-full-sql-server-for-development"></a>Geliştirme için tam SQL Server SQL Server Express karşılaştırması

SQL Server yükseltmeye karar verdikten sonra, geliştirme ve test ortamlarınızda SQL Server veya SQL Server Express kullanmak isteyebilirsiniz. Araç desteğinin ve veritabanı altyapısı özelliklerinin farklılıklarına ek olarak, SQL Server Compact ve diğer SQL Server sürümleri arasındaki sağlayıcı uygulamalarında farklılıklar vardır. Bu farklılıklar aynı kodun farklı sonuçlar üretmesine neden olabilir. Bu nedenle SQL Server Compact geliştirme veritabanınız olarak tutmaya karar verirseniz, her dağıtımdan önce bir test ortamında sitenizi SQL Server veya SQL Server Express kapsamlı olarak test etmelisiniz.

SQL Server Compact aksine, SQL Server Express aslında aynı veritabanı altyapısıdır ve tam SQL Server aynı .NET sağlayıcısını kullanır. SQL Server Express ile test ettiğinizde, SQL Server ile aynı sonuçları elde etme konusunda emin olabilirsiniz. SQL Server kullanabileceğiniz SQL Server Express ile aynı veritabanı araçlarının çoğunu kullanabilirsiniz (bir önemli özel durumu [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)) ve saklanan yordamlar, görünümler, Tetikleyiciler ve çoğaltma gibi SQL Server diğer özellikleri destekler. (Ancak, genellikle bir üretim web sitesinde tam SQL Server kullanmanız gerekir. SQL Server Express, paylaşılan bir barındırma ortamında çalıştırılabilir, ancak bu için tasarlanmamıştır ve birçok barındırma sağlayıcısı bunu desteklemez.)

Visual Studio 2012 kullanıyorsanız, genellikle geliştirme ortamınız için SQL Server Express LocalDB ' yi seçersiniz çünkü bu, varsayılan olarak Visual Studio ile yüklenir. Ancak, LocalDB IIS 'de çalışmaz, bu nedenle test ortamınız için SQL Server ya da SQL Server Express kullanmanız gerekir.

### <a name="combining-databases-versus-keeping-them-separate"></a>Veritabanlarını birleştirmek ve ayrı tutmak

Contoso University uygulamasının iki SQL Server Compact veritabanı vardır: üyelik veritabanı (*Aspnet. sdf*) ve uygulama veritabanı (*okul. sdf*). Geçirdiğinizde, bu veritabanlarını iki ayrı veritabanına veya tek bir veritabanına geçirebilirsiniz. Uygulama veritabanınız ve üyelik veritabanınız arasındaki veritabanı birleştirmelerini kolaylaştırmak için bunları birleştirmek isteyebilirsiniz. Barındırma planınız, bunları birleştirmek için bir neden de sağlayabilir. Örneğin, barındırma sağlayıcısı birden çok veritabanı için daha fazla ücret alabilir veya birden fazla veritabanına izin verebilir. Bu, yalnızca tek bir SQL Server veritabanına izin veren, bu öğretici için kullanılan Cytanium Lite barındırma hesabı ile aynı durumdur.

Bu öğreticide şu şekilde iki veritabanınızı geçirirsiniz:

- Geliştirme ortamında iki LocalDB veritabanına geçiş yapın.
- Test ortamında iki SQL Server Express veritabanına geçiş yapın.
- Üretim ortamında bir birleştirilmiş tam SQL Server veritabanına geçiş yapın.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="installing-sql-server-express"></a>SQL Server Express yükleniyor

SQL Server Express, Visual Studio 2010 ile varsayılan olarak otomatik olarak yüklenir, ancak varsayılan olarak Visual Studio 2012 ile yüklenmez. SQL Server 2012 Express 'i yüklemek için aşağıdaki bağlantıya tıklayın

- [SQL Server Express 2012](https://www.microsoft.com/download/details.aspx?id=29062)

*TRK/x64/sqlexpr\_x64\_trk. exe* veya *trk/x86/Sqlexpr\_x86\_trk. exe*' yi seçin ve Yükleme sihirbazında varsayılan ayarları kabul edin. Yükleme seçenekleri hakkında daha fazla bilgi için bkz. [Yükleme sihirbazından SQL Server 2012 yükleme (Kurulum)](https://msdn.microsoft.com/library/ms143219.aspx).

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a>Test ortamı için SQL Server Express veritabanları oluşturma

Sonraki adım ASP.NET üyeliğini ve okul veritabanlarını oluşturmaktır.

**Görünüm** menüsünden **Sunucu Gezgini** (Visual Web Developer 'da**veritabanı Gezgini** ) öğesini seçin ve ardından **veri bağlantıları** ' na sağ tıklayıp **Yeni SQL Server veritabanı oluştur**' u seçin.

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

**Yeni SQL Server veritabanı oluştur** iletişim kutusunda, **sunucu adı** kutusuna ".\Sqlexpress" ve **Yeni veritabanı adı** kutusuna "ASPNET-test" yazın ve ardından **Tamam**' a tıklayın.

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

"Okul-test" adlı yeni bir SQL Server Express okul veritabanı oluşturmak için aynı yordamı izleyin.

(Geliştirme ortamı için her bir veritabanının ek bir örneğini oluşturacağından ve iki veritabanı kümesini ayırt edebilmeniz gerektiğinden, bu veritabanı adlarına "test" ekleniyor.

**Sunucu Gezgini** artık iki yeni veritabanını gösterir.

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a>Yeni veritabanları için bir verme betiği oluşturma

Uygulama, geliştirme bilgisayarınızda IIS 'de çalıştığında, uygulama, varsayılan uygulama havuzunun kimlik bilgilerini kullanarak veritabanına erişir. Ancak, varsayılan olarak, uygulama havuzu kimliğinin veritabanlarını açma izni yoktur. Bu nedenle, bu izni vermek için bir komut dosyası çalıştırmanız gerekir. Bu bölümde, uygulamanın IIS 'de çalıştırıldığında veritabanlarını açabildiğinden emin olmak için daha sonra çalıştıracağınız betiği oluşturun.

[Üretim ortamına dağıtma](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) öğreticisinde oluşturduğunuz çözümün *Solutionfiles* klasöründe, *Grant. SQL*adlı yeni bir SQL dosyası oluşturun. Aşağıdaki SQL komutlarını dosyaya kopyalayın ve sonra dosyayı kaydedip kapatın:

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> Bu komut dosyası, bu öğreticide belirtildiği üzere 2008 SQL Server ve Windows 7 ' de IIS ayarları ile çalışmak üzere tasarlanmıştır. SQL Server veya Windows 'un farklı bir sürümünü kullanıyorsanız veya IIS 'yi bilgisayarınızda farklı şekilde ayarlarsanız, bu betikteki değişiklikler gerekli olabilir. SQL Server betikler hakkında daha fazla bilgi için bkz. [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).

> [!NOTE] 
> 
> **Güvenlik notunun** Bu betik, çalışma zamanında veritabanına erişen kullanıcıya DB\_Owner izinleri verir, bu da üretim ortamında sahip olacaksınız. Bazı senaryolarda, yalnızca dağıtım için tam veritabanı şeması güncelleştirme izinlerine sahip olan bir Kullanıcı belirtmek ve yalnızca verileri okuma ve yazma izinlerine sahip farklı bir kullanıcının çalışma süresini belirtmek isteyebilirsiniz. Daha fazla bilgi için bkz. [bir test ortamı olarak IIS 'ye dağıtma](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)içindeki **Code First Migrations için otomatik Web. config değişikliklerini gözden geçirme** .

## <a name="configuring-database-deployment-for-the-test-environment"></a>Test ortamı için veritabanı dağıtımını yapılandırma

Ardından, Visual Studio 'Yu her veritabanı için aşağıdaki görevleri yapacağına olanak verecek şekilde yapılandıracaksınız:

- Hedef veritabanında kaynak veritabanının yapısını (tablolar, sütunlar, kısıtlamalar, vb.) oluşturan bir SQL betiği oluşturun.
- Kaynak veritabanının verilerini hedef veritabanındaki tablolara ekleyen bir SQL betiği oluşturun.
- Oluşturulan komut dosyalarını ve hedef veritabanında oluşturduğunuz verme betiğini çalıştırın.

**Proje özellikleri** penceresini açın ve **paket/yayımlama SQL** sekmesini seçin.

**Yapılandırma** açılan listesinde **etkin (yayın)** veya **yayın** ' ın seçili olduğundan emin olun.

**Bu sayfayı etkinleştir**' e tıklayın.

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

**Paket/YAYıMLAMA SQL** sekmesi, eski bir dağıtım yöntemi belirttiğinden, normal olarak devre dışıdır. Çoğu senaryoda, **Web 'ı Yayımla** sihirbazında veritabanı dağıtımını yapılandırmalısınız. SQL Server Compact SQL Server veya SQL Server Express arasında geçiş yapmak, bu yöntemin iyi bir seçenek olduğu özel bir durumdur.

**Web. config 'Den Içeri aktar**' a tıklayın.

![Selecting_Import_from_Web. config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

Visual Studio, *Web. config* dosyasında bağlantı dizelerini arar, üyelik veritabanı ve diğeri de okul veritabanı için bir tane bulur ve **veritabanı girdileri** tablosundaki her bağlantı dizesine karşılık gelen bir satır ekler. Bulduğu bağlantı dizeleri mevcut SQL Server Compact veritabanlarına yöneliktir ve bir sonraki adımınız Bu veritabanlarının nasıl ve nereye dağıtılacağını yapılandırmak olacaktır.

Veritabanı **girdileri** tablosunun altındaki veritabanı **girişi ayrıntıları** bölümüne veritabanı dağıtım ayarlarını girersiniz. **Veritabanı giriş ayrıntıları** bölümünde gösterilen ayarlar, aşağıdaki çizimde gösterildiği gibi, **veritabanı girdileri** tablosundaki herhangi bir satırla ilgilidir.

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a>Üyelik veritabanı için dağıtım ayarlarını yapılandırma

Üyelik veritabanına uygulanan ayarları yapılandırmak için **veritabanı girdileri** tablosundaki **DefaultConnection dağıtım** satırını seçin.

**Hedef veritabanı Için bağlantı dizesi**' nde, yeni SQL Server Express üyelik veritabanına işaret eden bir bağlantı dizesi girin. **Sunucu Gezgini**gerek duyduğunuz bağlantı dizesini alabilirsiniz. **Sunucu Gezgini**' de, **veri bağlantıları** ' nı genişletin ve **Aspnettest** veritabanını seçin, sonra **Özellikler** penceresinden **bağlantı dizesi** değerini kopyalayın.

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

Aynı bağlantı dizesi burada yeniden oluşturulur:

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

Bu bağlantı dizesini kopyalayın ve **paket/YAYıMLAMA SQL** sekmesinde **hedef veritabanı için bağlantı dizesine** yapıştırın.

**Var olan bir veritabanından çekme verilerinin ve/veya şemasının** seçildiğinden emin olun. Bu, SQL betiklerinin otomatik olarak oluşturulmasına ve hedef veritabanında çalışmasına neden olur.

**Kaynak veritabanı değeri Için bağlantı dizesi** *Web. config* dosyasından ayıklanır ve geliştirme SQL Server Compact veritabanına işaret eder. Bu, daha sonra hedef veritabanında çalıştırılacak betikleri oluşturmak için kullanılacak kaynak veritabanıdır. Veritabanının üretim sürümünü dağıtmak istediğinizden sonra, "aspnet-Dev. sdf" öğesini "aspnet-Prod. sdf" olarak değiştirin.

Verilerinizi (Kullanıcı hesapları ve rolleri) ve veritabanı yapısını kopyalamak istiyorsanız, **veritabanı komut dosyası seçeneklerini** **şemadan yalnızca** **şema ve verilerle**değiştirin.

Daha önce oluşturduğunuz verme betiklerini çalıştırmak için dağıtımı yapılandırmak üzere, bunları **veritabanı betikleri** bölümüne eklemeniz gerekir. **Komut dosyası Ekle**' ye tıklayın ve **SQL betikleri Ekle** iletişim kutusunda, Grant betiğini depoladığınız klasöre gidin (Bu, çözüm dosyanızı içeren klasördür). *Ver. SQL*adlı dosyayı seçin ve **Aç**' a tıklayın.

[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)

**Veritabanı girdilerindeki** **DefaultConnection dağıtım** satırının ayarları artık aşağıdaki şekilde görünür:

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>Okul veritabanı için dağıtım ayarlarını yapılandırma

Ardından, okul veritabanının dağıtım ayarlarını yapılandırmak için **veritabanı girdileri** tablosundaki **SchoolContext-Deployment** satırını seçin.

Yeni SQL Server Express veritabanının bağlantı dizesini almak için, daha önce kullandığınız yöntemi kullanabilirsiniz. Bu bağlantı dizesini **paket/YAYıMLAMA SQL** sekmesindeki **hedef veritabanı için bağlantı dizesine** kopyalayın.

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

**Var olan bir veritabanından çekme verilerinin ve/veya şemasının** seçildiğinden emin olun.

**Kaynak veritabanı değeri Için bağlantı dizesi** *Web. config* dosyasından ayıklanır ve geliştirme SQL Server Compact veritabanına işaret eder. Veritabanının üretim sürümünü dağıtmak için "School-Dev. sdf" öğesini "School-Prod. sdf" olarak değiştirin. (App\_Data klasöründe hiçbir School-Prod. sdf dosyası oluşturmadınız, bu dosyayı test ortamından Contosoüniversitesi proje klasöründeki App\_Data klasörüne kopyalayacaksınız.)

**Veritabanı komut dosyası seçeneklerini** **şema ve verilerle**değiştirin.

Ayrıca, bu veritabanı için uygulama havuzu kimliğine okuma ve yazma izni vermek üzere betiği çalıştırmak istiyorsanız, üyelik veritabanına yaptığınız gibi *Grant. SQL* komut dosyasını ekleyin.

İşiniz bittiğinde, **veritabanı girdilerindeki** **SchoolContext-Deployment** satırı ayarları aşağıdaki çizimde gösterildiği gibi görünür:

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

Değişiklikleri **paket/YAYıMLAMA SQL** sekmesine kaydedin.

*School-prod. sdf* dosyasını *C:\inetpub\wwwroot\contosoüniversıty\app\_Data* klasöründen contosouniversity projesindeki *App\_Data* klasörüne kopyalayın.

### <a name="specifying-transacted-mode-for-the-grant-script"></a>Verme betiği için Işlem temelli modu belirtme

Dağıtım işlemi, veritabanı şemasını ve verilerini dağıtan komut dosyaları oluşturur. Varsayılan olarak, bu betikler bir işlem içinde çalışır. Ancak, Özel betikler (verme betikleri gibi) varsayılan olarak bir işlemde çalışmaz. Dağıtım işlemi işlem modlarını karıştırırsa, betikler dağıtım sırasında çalıştırıldığında bir zaman aşımı hatası alabilirsiniz. Bu bölümde, özel betikleri bir işlemde çalışacak şekilde yapılandırmak için proje dosyasını düzenlersiniz.

**Çözüm Gezgini**, **contosouniversity** projesine sağ tıklayın ve **Projeyi Kaldır**' ı seçin.

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

Ardından projeye tekrar sağ tıklayın ve **ContosoUniversity. csproj Düzenle**' yi seçin.

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

Visual Studio Düzenleyicisi, proje dosyasının XML içeriğini gösterir. Birçok `PropertyGroup` öğesi olduğuna dikkat edin. (Görüntüde `PropertyGroup` öğelerinin içeriği atlandı.)

![Proje dosya Düzenleyicisi penceresi](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

`Condition` özniteliği olmayan ilki, yapı yapılandırmasına bakılmaksızın uygulanan ayarlar içindir. Bir `PropertyGroup` öğesi yalnızca hata ayıklama oluşturma yapılandırması için geçerlidir (`Condition` özniteliğini aklınızda), biri yalnızca yayın derleme yapılandırması için geçerlidir ve biri yalnızca test derleme yapılandırması için geçerlidir. Yayın derleme yapılandırması için `PropertyGroup` öğesinde, **paket/YAYıMLAMA SQL** sekmesine girdiğiniz ayarları içeren bir `PublishDatabaseSettings` öğesi görürsünüz. Belirttiğiniz tüm verme betiklerine karşılık gelen bir `Object` öğesi vardır ("ver. SQL" öğesinin iki örneğine dikkat edin). Varsayılan olarak, her bir verme betiği için `Source` öğesinin `Transacted` özniteliği `False`.

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

`Source` öğesinin `Transacted` özniteliğinin değerini `True`olarak değiştirin.

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

Proje dosyasını kaydedip kapatın ve ardından **Çözüm Gezgini** ' de projeye sağ tıklayıp **projeyi yeniden yükle**' yi seçin.

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a>Bağlantı dizeleri için Web. config dönüşümlerini ayarlama

**Paket/YAYıMLAMA SQL** sekmesine GIRDIĞINIZ yeni SQL Express veritabanlarının bağlantı dizeleri, yalnızca dağıtım sırasında hedef veritabanını güncelleştirmek için Web dağıtımı tarafından kullanılır. *Web. config* dönüşümlerini, dağıtılmış *Web. config* dosyasındaki bağlantı dizelerinin yeni SQL Server Express veritabanlarına işaret edecek şekilde ayarlamanız gerekir. ( **Paket/YAYıMLAMA SQL** sekmesini kullandığınızda, yayımlama profilinde bağlantı dizelerini yapılandıramazsınız.)

*Web. test. config* dosyasını açın ve `connectionStrings` öğesini aşağıdaki örnekteki `connectionStrings` öğesiyle değiştirin. (Bağlam sağlamak için burada gösterilen çevreleyen kodu değil, yalnızca connectionStrings öğesini kopyalamadığınızdan emin olun.)

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

Bu kod, her bir `add` öğesinin `connectionString` ve `providerName` özniteliklerinin dağıtılan *Web. config* dosyasında değiştirilmesini sağlar. Bu bağlantı dizeleri, **paket/YAYıMLAMA SQL** sekmesine girdiklerle aynı değildir. "MultipleActiveResultSets = true" ayarı, Entity Framework ve evrensel sağlayıcılar için gerekli olduğu için bunlara eklenmiştir.

## <a name="installing-sql-server-compact"></a>SQL Server Compact yükleniyor

SqlServerCompact NuGet paketi, Contoso Üniversitesi uygulaması için SQL Server Compact veritabanı altyapısı derlemelerini sağlar. Ancak artık uygulama değildir, ancak SQL Server veritabanlarında çalıştırılacak betikler oluşturmak için SQL Server Compact veritabanlarını okuyabilmelidir Web Dağıtımı. Web Dağıtımı SQL Server Compact veritabanlarını okumak üzere etkinleştirmek için, aşağıdaki bağlantıyı kullanarak geliştirme bilgisayarına SQL Server Compact ' i ( [Microsoft SQL Server Compact 4,0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)) kullanın.

## <a name="deploying-to-the-test-environment"></a>Test ortamına dağıtma

Test ortamında yayımlamak için, profil veritabanı ayarları yerine veritabanı yayımlaması için **paket/YAYıMLAMA SQL** sekmesini kullanmak üzere yapılandırılmış bir yayımlama profili oluşturmanız gerekir.

İlk olarak, var olan test profilini silin.

**Çözüm Gezgini**, contosouniversity projesine sağ tıklayın ve **Yayımla**' ya tıklayın.

**Profil** sekmesini seçin.

**Profilleri Yönet**' e tıklayın.

**Test**' i seçin, **Kaldır**' a ve ardından **Kapat**' a tıklayın.

Bu değişikliği kaydetmek için **Web 'ı Yayımla** Sihirbazı 'nı kapatın.

Sonra, yeni bir test profili oluşturun ve projeyi yayımlamak için onu kullanın.

**Çözüm Gezgini**, contosouniversity projesine sağ tıklayın ve **Yayımla**' ya tıklayın.

**Profil** sekmesini seçin.

Açılan listeden **yeni...&gt;&lt;** seçin ve profil adı olarak "test" yazın.

**Hizmet URL 'si** kutusuna *localhost*yazın.

**Site/uygulama** kutusuna *varsayılan Web sitesi/contosouniversity*yazın.

**Hedef URL** kutusuna `http://localhost/ContosoUniversity/`girin.

**İleri**'ye tıklayın.

**Ayarlar** sekmesi, **paket/yayımlama SQL** sekmesinin yapılandırıldığını ve yeni veritabanı yayımlama iyileştirmelerini etkinleştir ' e tıklayarak bunları geçersiz kılmak için bir fırsat sağlar. Bu dağıtım için **paket/SQL sekmesini Yayımla** ayarlarını geçersiz kılmak istemezsiniz, bu nedenle **İleri**' ye tıklamanız yeterlidir.

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

**Önizleme** sekmesindeki bir ileti, **yayımlanacak hiçbir veritabanı**olmadığını gösterir, ancak bu yalnızca yayımlama profilinde veritabanı yayımlamanın yapılandırılmadığı anlamına gelir.

**Yayımla**’ta tıklayın.

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

Visual Studio uygulamayı dağıtır ve tarayıcıyı test ortamında sitenin ana sayfasında açar. Daha önce gördüğünüz verilerin aynısını görüntülediğini görmek için Eğitmenler sayfasını çalıştırın. Öğrenci **Ekle** sayfasını çalıştırın, yeni bir öğrenci ekleyin ve ardından **öğrenciler** sayfasında yeni öğrenci 'yi görüntüleyin. Bu, veritabanını güncelleştirebildiğini doğrular. Üyelik veritabanının dağıtıldığını ve ona erişiminizin olduğunu doğrulamak için **kredileri güncelleştirme** sayfasını (oturum açmanız gerekir) seçin.

## <a name="creating-a-sql-server-database-for-the-production-environment"></a>Üretim ortamı için SQL Server veritabanı oluşturma

Artık test ortamına dağıttığınıza göre, üretime dağıtımı ayarlamaya hazırsınız demektir. Dağıtım için bir veritabanı oluşturarak, test ortamı için yaptığınız gibi başlarsınız. Genel bakışa geri çekmeniz sırasında Cytanium Lite barındırma planı yalnızca tek bir SQL Server veritabanına izin veriyor, bu nedenle iki değil yalnızca bir veritabanı ayarlarsınız. Üyelik ve okul SQL Server Compact veritabanlarının tüm tabloları ve verileri, üretimde tek bir SQL Server veritabanına dağıtılır.

[http://panel.cytanium.com](http://panel.cytanium.com)adresindeki Cytanium Denetim Masası ' na gidin. Fareyi **veritabanlarının** üzerinde tutun ve ardından **SQL Server 2008**' ye tıklayın.

[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)

**SQL Server 2008** sayfasında **veritabanı oluştur**' a tıklayın.

[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)

"Okul" veritabanını adlandırın ve **Kaydet**' e tıklayın. (Sayfa "contosou" önekini otomatik olarak ekler, bu nedenle geçerli ad "contosouSchool" olur.)

[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)

Aynı sayfada **Kullanıcı oluştur**' a tıklayın. Cytanium 'in sunucularında, tümleşik Windows güvenliği kullanmak yerine ve uygulama havuzu kimliğinin veritabanınızı açmasına izin vermek için, veritabanınızı açma yetkisine sahip bir Kullanıcı oluşturacaksınız. Kullanıcının kimlik bilgilerini üretim *Web. config* dosyasına gidecek bağlantı dizelerine ekleyeceksiniz. Bu adımda bu kimlik bilgilerini oluşturursunuz.

[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)

**SQL kullanıcı özellikleri** sayfasında gerekli alanları girin:

- Ad olarak "Contosoüniversıtyuser" yazın.
- Bir parola girin.
- Varsayılan veritabanı olarak **Contosouschool** ' u seçin.
- **Contosouschool** onay kutusunu seçin.

[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)

## <a name="configuring-database-deployment-for-the-production-environment"></a>Üretim ortamı için veritabanı dağıtımını yapılandırma

Artık, daha önce test ortamı için yaptığınız gibi **paket/YAYıMLAMA SQL** sekmesinde veritabanı dağıtım ayarlarını ayarlamaya hazırsınız.

**Proje özellikleri** penceresini açın, **paket/yayımlama SQL** sekmesini seçin ve **yapılandırma** açılan listesinde **etkin (yayın)** veya **yayın** ' ın seçili olduğundan emin olun.

Her bir veritabanı için dağıtım ayarlarını yapılandırdığınızda, üretim ve test ortamları için yapabilecekleriniz arasındaki temel fark, bağlantı dizelerini yapılandırma dizileridir. Test ortamı için farklı hedef veritabanı bağlantı dizelerini girdiniz, ancak üretim ortamında, her iki veritabanı için de hedef bağlantı dizesi aynı olacaktır. Bunun nedeni, her iki veritabanını üretimde bir veritabanına dağıtmaktan kaynaklanır.

### <a name="configuring-deployment-settings-for-the-membership-database"></a>Üyelik veritabanı için dağıtım ayarlarını yapılandırma

Üyelik veritabanına uygulanan ayarları yapılandırmak için, **veritabanı girdileri** tablosundaki **DefaultConnection-Deployment** satırını seçin.

**Hedef veritabanına yönelik bağlantı dizesinde**, az önce oluşturduğunuz yeni üretim SQL Server veritabanına işaret eden bir bağlantı dizesi girin. Bağlantı dizesine hoş geldiniz e-postaınızdan ulaşabilirsiniz. E-postanın ilgili bölümü aşağıdaki örnek bağlantı dizesini içerir:

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

Üç değişkeni değiştirdikten sonra, ihtiyacınız olan bağlantı dizesi şu örneğe benzer şekilde görünür:

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

Bu bağlantı dizesini kopyalayın ve **paket/YAYıMLAMA SQL** sekmesinde **hedef veritabanı için bağlantı dizesine** yapıştırın.

**Mevcut bir veritabanından çekme verilerinin ve/veya şemasının** hala seçili olduğundan ve **veritabanı komut dosyası seçeneklerinin** hala **şema ve veri**olduğundan emin olun.

**Veritabanı betikleri** kutusunda, Grant. SQL komut dosyasının yanındaki onay kutusunu temizleyin.

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>Okul veritabanı için dağıtım ayarlarını yapılandırma

Ardından, okul veritabanı ayarlarını yapılandırmak için **veritabanı girdileri** tablosundaki **SchoolContext-Deployment** satırını seçin.

Aynı bağlantı dizesini, üyelik veritabanı için bu alana kopyaladığınız **hedef veritabanı Için bağlantı dizesine** kopyalayın.

**Mevcut bir veritabanından çekme verilerinin ve/veya şemasının** hala seçili olduğundan ve **veritabanı komut dosyası seçeneklerinin** hala **şema ve veri**olduğundan emin olun.

**Veritabanı betikleri** kutusunda, Grant. SQL komut dosyasının yanındaki onay kutusunu temizleyin.

Değişiklikleri **paket/YAYıMLAMA SQL** sekmesine kaydedin.

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a>Web. config dönüşümlerini üretim veritabanlarına bağlantı dizeleri için ayarlama

Daha sonra, dağıtılmış *Web. config* dosyasındaki bağlantı dizelerinin yeni üretim veritabanına işaret edebilmesi için *Web. config* dönüşümlerini ayarlayacaksınız. Kullanmak Web Dağıtımı için **paket/YAYıMLAMA SQL** sekmesine girdiğiniz bağlantı dizesi, `MultipleResultSets` seçeneğinin eklenmesi dışında uygulamanın kullanması gereken uygulamayla aynıdır.

*Web. Production. config* dosyasını açın ve `connectionStrings` öğesini aşağıdaki örnekte olduğu gibi görünen bir `connectionStrings` öğesiyle değiştirin. (Bağlamı göstermek için belirtilen çevreleyen etiketlerin değil, yalnızca `connectionStrings` öğesini kopyalayın.)

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

Bazen *Web. config* dosyasındaki bağlantı dizelerini her zaman şifrelemenizi söyleyen tavsiyeler görürsünüz. Bu, kendi şirketinizin ağındaki sunuculara dağıtım yapıyorsanız uygun olabilir. Paylaşılan bir barındırma ortamına dağıtım yaparken, barındırma sağlayıcısının güvenlik uygulamalarına güvenmiş olursunuz ve bağlantı dizelerini şifrelemek gerekli veya pratik değildir.

## <a name="deploying-to-the-production-environment"></a>Üretim ortamına dağıtma

Artık üretime dağıtmaya hazırsınız. Web Dağıtımı, projenizin *App\_Data* klasöründeki SQL Server Compact veritabanlarını okur ve üretim SQL Server veritabanındaki tüm tablo ve verileri yeniden oluşturur. **Web 'ı paketle/Yayımla** sekmesi ayarlarını kullanarak yayımlamak için, üretim için yeni bir yayımlama profili oluşturmanız gerekir.

İlk olarak, önceki test profilini yaptığınız gibi mevcut üretim profilini silin.

**Çözüm Gezgini**, contosouniversity projesine sağ tıklayın ve **Yayımla**' ya tıklayın.

**Profil** sekmesini seçin.

**Profilleri Yönet**' e tıklayın.

**Üretimi**seçin, **Kaldır**' a ve ardından **Kapat**' a tıklayın.

Bu değişikliği kaydetmek için **Web 'ı Yayımla** Sihirbazı 'nı kapatın.

Sonra, yeni bir üretim profili oluşturun ve projeyi yayımlamak için onu kullanın.

**Çözüm Gezgini**, contosouniversity projesine sağ tıklayın ve **Yayımla**' ya tıklayın.

**Profil** sekmesini seçin.

**Içeri aktar**' a tıklayın ve daha önce indirdiğiniz. publishsettings dosyasını seçin.

**Bağlantı** sekmesinde, **hedef URL** 'yi doğru geçici URL olarak değiştirin, bu örnekte http://contosouniversity.com.vserver01.cytanium.com.

Profili üretim olarak yeniden adlandırın. ( **Profil** sekmesini seçin ve **profilleri Yönet** ' e tıklayın).

Değişikliklerinizi kaydetmek için **Web 'ı Yayımla** sihirbazını kapatın.

Veritabanının üretimde güncelleştirildiği gerçek bir uygulamada, yayımlamadan önce Şu iki adımı uygulayın:

1. Uygulamayı [üretim ortamına dağıtma](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) öğreticisinde gösterildiği gibi *çevrimdışı. htm\_* yükleyin.
2. *ASPNET-prod. sdf* ve *School-prod. sdf* dosyalarını üretim sitesinden contosouniversity projesinin *App\_Data* klasörüne kopyalamak Için Cytanium Denetim Masası 'nın **Dosya Yöneticisi** özelliğini kullanın. Bu, yeni SQL Server veritabanına dağıttığınız verilerin üretim Web siteniz tarafından yapılan en son güncelleştirmeleri içerdiğinden emin olmanızı sağlar.

Web 'de **Yayımla** araç çubuğunda, **Üretim** profili ' nin seçili olduğundan emin olun ve ardından **Yayımla**' ya tıklayın.

Yayımlamadan önce <em>app\_offline. htm</em> dosyasını karşıya yüklediyseniz, <em>uygulamayı\_çevrimdışı</em> olarak silmek için Cytanium Denetim Masası 'ndaki <strong>Dosya Yöneticisi</strong> yardımcı programını kullanmanız gerekir. test etmeden önce. Aynı zamanda <em>App\_Data</em> klasöründeki <em>. sdf</em> dosyalarını da silebilirsiniz.

Artık bir tarayıcı açabilir ve uygulamayı test ortamına dağıttıktan sonra yaptığınız şekilde test etmek için ortak sitenizin URL 'sine gidebilirsiniz.

## <a name="switching-to-sql-server-express-localdb-in-development"></a>Geliştirme sırasında SQL Server Express LocalDB 'ye geçiş yapma

Genel bakışta açıklandığı gibi, test ve üretimde kullandığınız geliştirme sırasında aynı veritabanı altyapısını kullanmak genellikle en iyisidir. (Geliştirme aşamasında SQL Server Express kullanmanın avantajı veritabanının geliştirme, test ve üretim ortamlarınızda aynı şekilde çalışacağınızdan emin olur.) Bu bölümde, uygulamayı Visual Studio 'dan çalıştırdığınızda SQL Server Express LocalDB 'yi kullanacak şekilde ContosoUniversity projesini ayarlayacaksınız.

Bu geçişi yapmanın en kolay yolu Code First ve üyelik sisteminin sizin için her iki yeni geliştirme veritabanı oluşturmasına izin verolmaktır. Geçirmek için bu yöntemin kullanılması üç adım gerektirir:

1. Bağlantı dizelerini yeni SQL Express LocalDB veritabanlarını belirtecek şekilde değiştirin.
2. Yönetici Kullanıcı oluşturmak için Web sitesi yönetim aracı 'nı çalıştırın. Bu, üyelik veritabanını oluşturur.
3. Uygulama veritabanını oluşturmak ve çekirdek oluşturmak için Code First Migrations Update-database komutunu kullanın.

### <a name="updating-connection-strings-in-the-webconfig-file"></a>Web. config dosyasındaki bağlantı dizeleri güncelleştiriliyor

*Web. config* dosyasını açın ve `connectionStrings` öğesini aşağıdaki kodla değiştirin:

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a>Üyelik veritabanı oluşturuluyor

**Çözüm Gezgini**, contosouniversity projesini seçin ve ardından **Proje** menüsünde **ASP.net Configuration** ' a tıklayın.

Güvenlik sekmesini seçin.

**Roller oluştur veya Yönet**' e tıklayın ve ardından bir **yönetici** rolü oluşturun.

Güvenlik sekmesine dönün.

**Kullanıcı oluştur**' a tıklayın ve **yönetici** onay kutusunu seçin ve yönetici adlı bir kullanıcı oluşturun.

**Web sitesi yönetim aracı**'nı kapatın.

### <a name="creating-the-school-database"></a>Okul veritabanı oluşturuluyor

Paket Yöneticisi konsol penceresini açın.

**Varsayılan proje** açılan listesinde CONTOSOUNIVERSITY. dal projesini seçin.

Aşağıdaki komutu girin:

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

Code First Migrations, veritabanını oluşturan Ilk geçişi uygular ve sonra Adddoğum tarihi geçişini uygular, ardından çekirdek yöntemini çalıştırır.

Denetimi-F5 tuşuna basarak siteyi çalıştırın. Test ve üretim ortamlarında yaptığınız gibi, **öğrenci Ekle** sayfasını çalıştırın, yeni bir öğrenci ekleyin ve ardından **öğrenciler** sayfasında yeni öğrenci 'yi görüntüleyin. Bu, okul veritabanının oluşturulduğunu ve başlatıldığını ve buna okuma ve yazma erişimi olduğunu doğrular.

, Üyelik veritabanının dağıtıldığını ve ona erişiminizin olduğunu doğrulamak için **kredileri Güncelle** sayfasını seçin ve oturum açın. Kullanıcı hesaplarınızı geçirmediyseniz, bir yönetici hesabı oluşturun ve çalıştığını doğrulamak için **kredileri Güncelleştir** sayfasını seçin.

## <a name="cleaning-up-sql-server-compact-files"></a>SQL Server Compact dosyalarını temizleme

Artık SQL Server Compact destek için bulunan dosyalar ve NuGet paketlerine ihtiyacınız yoktur. İsterseniz (Bu adım gerekli değildir), gereksiz dosyaları ve başvuruları temizleyebilirsiniz.

**Çözüm Gezgini**' de, *. sdf* dosyalarını *uygulama\_verileri* klasöründen ve *AMD64* ve *x86* klasörlerinden *bin* klasöründen silin.

**Çözüm Gezgini**, çözüme (projelerden birine değil) sağ tıklayın ve ardından **çözüm Için NuGet Paketlerini Yönet**' e tıklayın.

**NuGet Paketlerini Yönet** iletişim kutusunun sol bölmesinde **yüklü paketler**' i seçin.

**EntityFramework. SqlServerCompact** paketini seçin ve **Yönet**' e tıklayın.

**Projeleri Seç** iletişim kutusunda her iki proje de seçilidir. Paketi her iki projede da kaldırmak için, her iki onay kutusunu da temizleyin ve ardından **Tamam**' a tıklayın.

Bağımlı paketleri kaldırmak isteyip istemediğinizi soran iletişim kutusunda Hayır ' a tıklayın. Bunlardan biri, tutmanız gereken Entity Framework paketidir.

**Sqlservercompact** paketini kaldırmak için aynı yordamı izleyin. ( **EntityFramework. SqlServerCompact** paketi **sqlservercompact** paketine bağlı olduğundan, paketlerin bu sırada kaldırılması gerekir.)

Artık SQL Server Express ve tam SQL Server başarıyla geçirildi. Bir sonraki öğreticide, başka bir veritabanı değişikliğini yaparsınız ve test ve üretim veritabanlarınız SQL Server Express ve tam SQL Server kullanırken veritabanı değişikliklerinin nasıl dağıtılacağını görürsünüz.

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [İleri](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
