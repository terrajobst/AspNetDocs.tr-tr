---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: 'Visual Studio kullanarak ASP.NET Web dağıtımı: veritabanı dağıtımı için hazırlanma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: cdcb3578725c41e3c801afd54e6d34455bc4b281
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618523"
---
# <a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>Visual Studio kullanarak ASP.NET Web dağıtımı: veritabanı dağıtımı için hazırlanma

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

Bu öğreticide, projenin veritabanı dağıtımına nasıl hazırlanalınacağı gösterilmektedir. Uygulama, hazırlama ve üretim ortamlarına, veritabanı yapısı ve uygulamanın iki veritabanındaki verilerin bazıları (hepsi değil) dağıtılması gerekir.

Genellikle, bir uygulama geliştirirken, canlı bir siteye dağıtmak istemediğiniz bir veritabanına test verileri girersiniz. Ancak, dağıtmak istediğiniz bazı üretim verileri de olabilir. Bu öğreticide, Contoso Üniversitesi projesini yapılandırıp SQL betiklerini, dağıtırken doğru verilerin dahil edilmesini sağlayacak şekilde hazırlarsınız.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

Örnek uygulama SQL Server Express LocalDB kullanır. SQL Server Express, SQL Server ücretsiz sürümüdür. Genellikle geliştirme sırasında kullanılır çünkü SQL Server tam sürümleriyle aynı veritabanı altyapısını temel alır. SQL Server Express ile test edebilir ve uygulamanın üretimde aynı şekilde davranmasını sağlayacak şekilde, SQL Server sürümleri arasında değişen özellikler için birkaç özel durum ile emin olabilirsiniz.

LocalDB, veritabanlarıyla *. mdf* dosyaları olarak çalışmanıza olanak sağlayan SQL Server Express özel bir yürütme modudur. Genellikle, LocalDB veritabanı dosyaları bir Web projesinin *App\_Data* klasöründe tutulur. SQL Server Express ' deki Kullanıcı örneği özelliği ayrıca *. mdf* dosyalarıyla çalışmanıza olanak sağlar ancak kullanıcı örneği özelliği kullanım dışıdır; Bu nedenle, LocalDB *. mdf* dosyalarıyla çalışma için önerilir.

Genellikle SQL Server Express üretim Web uygulamaları için kullanılmaz. LocalDB 'nin IIS ile çalışmak üzere tasarlanmadığı için, bir Web uygulamasıyla üretim kullanımı önerilmez.

Visual Studio 2012 ' de, LocalDB, Visual Studio ile varsayılan olarak yüklenir. Visual Studio 2010 ve önceki sürümlerde SQL Server Express (LocalDB olmadan), Visual Studio ile varsayılan olarak yüklenir; Bu nedenle, [Bu serinin ilk öğreticideki](introduction.md)önkoşulların biri olarak bu nedenle yüklenmenizin nedeni budur.

LocalDB dahil SQL Server sürümleri hakkında daha fazla bilgi için, [SQL Server veritabanlarıyla çalışan](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver)aşağıdaki kaynaklara bakın.

## <a name="entity-framework-and-universal-providers"></a>Entity Framework ve evrensel sağlayıcılar

Veritabanı erişimi için Contoso University uygulaması, .NET Framework dahil edilmediğinden uygulamayla birlikte dağıtılması gereken aşağıdaki yazılımları gerektirir:

- [ASP.net evrensel sağlayıcılar](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (ASP.NET üyelik SISTEMININ Azure SQL veritabanı 'nı kullanmasına olanak sağlar)
- [Varlık Çerçevesi](https://msdn.microsoft.com/library/gg696172.aspx)

Bu yazılım NuGet paketlerine eklendiğinden, proje zaten gerekli derlemelerin projeyle dağıtılması için ayarlanmıştır. (Bağlantılar bu paketlerin güncel sürümlerini işaret ediyor. Bu, bu öğretici için indirdiğiniz Başlatıcı projesinde yüklü olandan daha yeni olabilir.)

Azure yerine bir üçüncü taraf barındırma sağlayıcısına dağıtıyorsanız, Entity Framework 5,0 veya sonraki bir sürümü kullandığınızdan emin olun. Code First Migrations önceki sürümleri için tam güven gerekir ve barındırma sağlayıcılarının çoğu, uygulamanızı Orta güvende çalıştıracaktır. Orta güven hakkında daha fazla bilgi için bkz. [test ortamı olarak IIS 'ye dağıtma](deploying-to-iis.md) öğreticisi.

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>Uygulama veritabanı dağıtımı için Code First Migrations yapılandırma

Contoso Üniversitesi uygulama veritabanı Code First tarafından yönetilir ve Code First Migrations kullanarak dağıtırsınız. Code First Migrations kullanarak veritabanı dağıtımına genel bir bakış için, [Bu serideki ilk öğreticiye](introduction.md)bakın.

Bir uygulama veritabanını dağıttığınızda, genellikle geliştirme veritabanınızı yalnızca test amaçlı olarak yalnızca sınama amacıyla bu, içindeki verilerin büyük bir kısmını üretime dağıtmazsınız. Örneğin, bir test veritabanındaki öğrenci adları kurgusal değildir. Öte yandan, genellikle yalnızca veritabanı yapısını hiç veri olmadan dağıtamazsınız. Test Veritabanınızdaki bazı veriler gerçek veriler olabilir ve kullanıcılar uygulamayı kullanmaya başladığınızda bu durumda olmalıdır. Örneğin, veritabanınız geçerli bir sınıf değerleri veya gerçek departman adları içeren bir tabloya sahip olabilir.

Bu ortak senaryonun benzetimini yapmak için, yalnızca üretimde olmasını istediğiniz verileri veritabanına ekleyen bir Code First Migrations `Seed` yöntemi yapılandıracaksınız. Bu `Seed` yöntemi test verilerini eklemememelidir, çünkü Code First veritabanını üretimde oluşturduktan sonra üretimde çalışacaktır.

Geçiş işleminden önce Code First önceki sürümlerinde, geliştirme sırasında her model değiştikçe, veritabanının tamamen silinmesi ve sıfırdan yeniden oluşturulması gerekiyordu, çünkü bu da test verilerini eklemek için `Seed` metotlandı. Code First Migrations ile, test verileri veritabanı değişikliklerinden sonra tutulur, bu nedenle `Seed` yönteminde test verilerinin dahil edilmesi gerekmez. İndirdiğiniz proje, başlatıcı sınıfının `Seed` yönteminde tüm verileri dahil etme yöntemini kullanır. Bu öğreticide, bu başlatıcı sınıfını devre dışı bırakıp geçişleri etkinleştireceksiniz. Daha sonra, geçişleri yapılandırma sınıfındaki `Seed` yöntemi, yalnızca üretime eklemek istediğiniz verileri eklemek için güncelleştireceksiniz.

Aşağıdaki diyagramda uygulama veritabanının şeması gösterilmektedir:

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

Bu öğreticiler için, site ilk dağıtıldığında `Student` ve `Enrollment` tablolarının boş olması gerektiğini varsayabilirsiniz. Diğer tablolar, uygulama canlı kaldığında önceden yüklenmesi gereken verileri içerir.

### <a name="disable-the-initializer"></a>Başlatıcıyı devre dışı bırakma

Code First Migrations kullanacağınız için, `DropCreateDatabaseIfModelChanges` Code First başlatıcısı 'nı kullanmanız gerekmez. Bu başlatıcının kodu, ContosoUniversity. DAL projesindeki *SchoolInitializer.cs* dosyasıdır. *Web. config* dosyasının `appSettings` öğesindeki bir ayar, uygulama veritabanına ilk kez erişmeyi her denediğinde bu başlatıcının çalışmasına neden olur:

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

Uygulama *Web. config* dosyasını açın ve Code First Başlatıcı sınıfını belirten `add` öğesini kaldırın veya not edin. `appSettings` öğesi şu şekilde görünür:

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> Bir başlatıcı sınıfı belirtmenin başka bir yolu da, *Global. asax* dosyasındaki `Application_Start` yönteminde `Database.SetInitializer` çağırarak yapılır. Başlatıcıyı belirtmek için bu yöntemi kullanan bir projede geçişleri etkinleştirirseniz, bu kod satırını kaldırın.

> [!NOTE]
> Visual Studio 2013 kullanıyorsanız, şu adımları adım 2 ve 3: (a) ila PMC 'de "Update-Package EntityFramework-Version 6.1.1" girerek geçerli EF sürümünü alın. Daha sonra (b) derleme hatalarının bir listesini almak ve bunları onarmak için projeyi derleyin. Artık mevcut olmayan ad alanları için using deyimlerini Sil ' e sağ tıklayıp, gerekli oldukları yerleri kullanarak eklemek ve System. Data. EntityState 'in oluşumlarını System. Data. Entity. EntityState olarak değiştirmek için Çözümle ' ye tıklayın.

### <a name="enable-code-first-migrations"></a>Code First Migrations etkinleştir

1. ContosoUniversity projesinin (ContosoUniversity. DAL değil) başlangıç projesi olarak ayarlandığından emin olun. **Çözüm Gezgini**, contosouniversity projesine sağ tıklayın ve **Başlangıç projesi olarak ayarla**' yı seçin. Code First Migrations, veritabanı bağlantı dizesini bulmak için başlangıç projesine bakacaktır.
2. **Araçlar** menüsünde **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin.

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. **Paket Yöneticisi konsol** penceresinin en üstündeki contosouniversity. dal ' i varsayılan proje olarak seçin ve ardından `PM>` istemine "Enable-geçişler" yazın.

    ![geçişleri Etkinleştir komutu](preparing-databases/_static/image4.png)

    ( *Enable-geçişleri* komutunun tanınmadığını belirten bir hata alırsanız, *Update-Package EntityFramework* komutunu girin ve yeniden yükleyin ve tekrar deneyin.)

    Bu komut, ContosoUniversity. DAL projesinde bir *geçişler* klasörü oluşturur ve bu klasöre iki dosya koyar: geçişleri yapılandırmak için kullanabileceğiniz bir *Configuration.cs* dosyası ve veritabanını oluşturan ilk geçiş için bir *InitialCreate.cs* dosyası.

    ![Geçişler klasörü](preparing-databases/_static/image5.png)

    `enable-migrations` komutunun Code First bağlam sınıfını içeren projede yürütülmesi gerektiğinden, **Paket Yöneticisi konsolunun** **varsayılan proje** açılan listesinden dal projesini seçtiniz. Bu sınıf bir sınıf kitaplığı projesinde olduğunda, Code First Migrations çözüm için başlangıç projesindeki veritabanı bağlantı dizesini arar. ContosoUniversity çözümünde, Web projesi başlangıç projesi olarak ayarlanmıştır. Visual Studio 'da başlangıç projesi olarak bağlantı dizesine sahip projeyi atamak istemiyorsanız, PowerShell komutunda başlangıç projesini belirtebilirsiniz. Komut sözdizimini görmek için `get-help enable-migrations`komutunu girin.

    Veritabanı zaten mevcut olduğundan `enable-migrations` komutu otomatik olarak ilk geçişi oluşturdu. Diğer bir deyişle geçişler veritabanını oluşturur. Bunu yapmak için, geçişleri etkinleştirmeden önce ContosoUniversity veritabanını silmek için **Sunucu Gezgini** veya **SQL Server Nesne Gezgini** kullanın. Geçişleri etkinleştirdikten sonra, "Add-Migration ınitialcreate" komutunu girerek ilk geçişi el ile oluşturun. Daha sonra "Update-Database" komutunu girerek veritabanını oluşturabilirsiniz.

### <a name="set-up-the-seed-method"></a>Çekirdek yöntemi ayarlama

Bu öğreticide, Code First Migrations `Configuration` sınıfının `Seed` metoduna kod ekleyerek sabit veri ekleyeceksiniz. Code First Migrations her geçişten sonra `Seed` yöntemini çağırır.

`Seed` yöntemi her geçişten sonra çalıştığından, ilk geçişten sonra tablolarda zaten veri bulunur. Bu durumu işlemek için, zaten eklenmiş olan satırları güncelleştirmek için `AddOrUpdate` yöntemini kullanacaksınız ya da henüz mevcut değilse eklemeniz gerekir. `AddOrUpdate` yöntemi senaryonuz için en iyi seçim olmayabilir. Daha fazla bilgi için bkz. Julie Lerman 'ın blogundan [EF 4,3 AddOrUpdate yöntemiyle ilgilenme](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) .

1. *Configuration.cs* dosyasını açın ve `Seed` yöntemindeki açıklamaları aşağıdaki kodla değiştirin:

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. `List` başvurular, ad alanı için henüz bir `using` deyiminiz olmadığından bunlar altında kırmızı dalgalı çizgilere sahiptir. `List` örneklerinden birine sağ tıklayın ve **Çözümle**' ye tıklayın ve ardından **System. Collections. Generic kullanma**' ya tıklayın.

    ![Using ifadesiyle çözümle](preparing-databases/_static/image6.png)

    Bu menü seçimi, dosyanın en üstüne yakın `using` deyimlerine aşağıdaki kodu ekler.

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. Projeyi derlemek için CTRL-SHIFT-B tuşlarına basın.

Proje şimdi *Contosouniversity* veritabanını dağıtmaya hazırdır. Uygulamayı dağıttıktan sonra, ilk kez çalıştırdığınızda ve veritabanına erişen bir sayfaya gittiğinizde, Code First veritabanını oluşturacak ve bu `Seed` yöntemini çalıştıracaktır.

> [!NOTE]
> `Seed` yöntemine kod eklemek, veritabanına sabit veri ekleyebilmenizin birçok yönteminden biridir. Alternatif olarak, her bir geçiş sınıfının `Up` ve `Down` yöntemlerine kod eklemektir. `Up` ve `Down` yöntemleri, veritabanı değişikliklerini uygulayan kodu içerir. [Veritabanı güncelleştirme](deploying-a-database-update.md) öğreticisinde bunlara örnekler görürsünüz.
> 
> Ayrıca, `Sql` yöntemini kullanarak SQL deyimlerini yürüten bir kod yazabilirsiniz. Örneğin, bölüm tablosuna bir bütçe sütunu ekliyorsanız ve bir geçişin parçası olarak tüm bölüm bütçelerini $1.000,00 olarak başlatmak istiyorsanız, bu geçiş için `Up` yöntemine aşağıdaki kod satırını ekleyebilirsiniz:
> 
> `Sql("UPDATE Department SET Budget = 1000");`

## <a name="create-scripts-for-membership-database-deployment"></a>Üyelik veritabanı dağıtımı için betikler oluşturma

Contoso Üniversitesi uygulaması, kullanıcıların kimliğini doğrulamak ve yetkilendirmek için ASP.NET üyelik sistemi ve Forms kimlik doğrulamasını kullanır. **Kredilerin güncelleştirilmesi** sayfasına yalnızca yönetici rolünde olan kullanıcılar erişebilir.

Uygulamayı çalıştırın ve **Kurslar**' a ve ardından **kredileri Güncelleştir**' e tıklayın.

![Kredileri Güncelleştir 'e tıklayın](preparing-databases/_static/image7.png)

**Güncelleştirme kredileri** sayfası yönetimsel ayrıcalıklar gerektirdiğinden **oturum aç** sayfası görüntülenir.

*Yönetici* Kullanıcı adı ve *devpwd* olarak parolayı girin ve **oturum aç**' a tıklayın.

![Oturum açma sayfası](preparing-databases/_static/image8.png)

**Kredileri güncelleştirme** sayfası görüntülenir.

![Krediler sayfasını Güncelleştir](preparing-databases/_static/image9.png)

Kullanıcı ve rol bilgileri, *Web. config* dosyasındaki **DefaultConnection** bağlantı dizesi tarafından belirtilen *ASPNET-contosoüniversitesi* veritabanıdır.

Bu veritabanı Entity Framework Code First tarafından yönetilmiyor, bu nedenle dağıtmak için geçişleri kullanamazsınız. Veritabanı şemasını dağıtmak için dbDacFx sağlayıcısını kullanacaksınız ve yayımlama profilini veritabanı tablolarına ilk verileri ekleyecek bir betiği çalıştıracak şekilde yapılandıracaksınız.

> [!NOTE]
> Yeni bir ASP.NET üyelik sistemi (şimdi ASP.NET Identity olarak adlandırılır) Visual Studio 2013 ile tanıtılmıştı. Yeni sistem, hem uygulama hem de üyelik tablolarını aynı veritabanında tutmanıza olanak sağlar ve Code First Migrations kullanarak her ikisini de dağıtabilirsiniz. Örnek uygulama, Code First Migrations kullanılarak dağıtılabilecek önceki ASP.NET üyelik sistemini kullanır. Bu üyelik veritabanını dağıtmaya yönelik yordamlar, uygulamanızın Entity Framework Code First tarafından oluşturulmamış bir SQL Server veritabanı dağıtması gereken başka bir senaryoya da uygulanır.

Burada, genellikle geliştirmede sahip olduğunuz üretimde aynı verileri istemezsiniz. Bir siteyi ilk kez dağıttığınızda, test için oluşturduğunuz Kullanıcı hesaplarının çoğunun veya tümünün hariç tutulması yaygındır. Bu nedenle, indirilen projenin iki üyelik veritabanı vardır: *ASPNET-ContosoUniversity. mdf* ile geliştirme kullanıcıları ve *ASPNET-ContosoUniversity-prod. mdf* ile üretim kullanıcıları. Bu öğreticide, Kullanıcı adları her iki veritabanlarında de aynıdır: *yönetici* ve *yönetici olmayan*. Her iki kullanıcının da geliştirme veritabanında *devpwd* parolası ve üretim veritabanında *prodpwd* vardır.

Geliştirme kullanıcılarını, test ortamına ve üretim kullanıcılarına hazırlama ve üretime dağıtırsınız. Bunu yapmak için, bir diğeri geliştirme ve üretim için bir tane olmak üzere bu öğreticide iki SQL komut dosyası oluşturacaksınız ve sonraki öğreticilerde, Yayımlama sürecini onları çalıştıracak şekilde yapılandıracaksınız.

> [!NOTE]
> Üyelik veritabanı, hesap parolalarının karmasını depolar. Hesapların bir makineden diğerine dağıtılması için, karma yordamların hedef sunucuda kaynak bilgisayarda olduklarından farklı karmaları oluşturmadıklarından emin olmanız gerekir. Varsayılan algoritmayı değiştirmedikçe, ASP.NET Universal sağlayıcılarını kullandığınızda aynı karmaları oluşturur. Varsayılan algoritma HMACSHA256 ' dir ve Web. config dosyasındaki **[machineKey](https://msdn.microsoft.com/library/system.web.configuration.machinekeysection.aspx)** öğesinin **doğrulama** özniteliğinde belirtilir.

Veri Dağıtım betiklerini SQL Server Management Studio (SSMS) kullanarak veya üçüncü taraf bir aracı kullanarak el ile oluşturabilirsiniz. Bu öğreticinin geri kalanında, SSMS 'de nasıl yapılacağı gösterilir, ancak SSMS 'yi yüklemek ve kullanmak istemiyorsanız, projenin tamamlanmış sürümünden betikleri alabilir ve bunları çözüm klasöründe depoladığınız bölüme atlayabilirsiniz.

SSMS 'yi yüklemek için [Indirme merkezi 'nden yükleyin: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062) , [Tr\x64\sqlmanagementstudio\_x64\_trk. exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe) veya [trınstall\sqlmanagementstudio\_x86\_trk. exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe)' ye tıklayın. Sisteminiz için yanlış bir tane seçerseniz, yüklemesi başarısız olur ve diğerini de deneyebilirsiniz.

(Bunun 600 megabaytindir olduğunu unutmayın. Yüklenmesi uzun zaman alabilir ve bilgisayarınızın yeniden başlatılmasını gerektirir.)

SQL Server Yükleme Merkezi ' nin ilk sayfasında, **yeni SQL Server tek başına yükleme ' ye tıklayın veya var olan bir yüklemeye özellikler ekleyin**ve varsayılan seçimleri kabul ederek yönergeleri izleyin.

### <a name="create-the-development-database-script"></a>Geliştirme veritabanı betiği oluşturma

1. SSMS 'yi çalıştırın.
2. **Sunucuya Bağlan** iletişim kutusunda, **sunucu adı**olarak *(LocalDB) \v11.0* girin, **kimlik doğrulamasını** **Windows kimlik**doğrulaması olarak bırakın ve sonra **Bağlan**' a tıklayın.

    ![SSMS sunucuya Bağlan](preparing-databases/_static/image10.png)
3. **Nesne Gezgini** penceresinde **veritabanları**' nı genişletin, **ASPNET-Contosouniversity**öğesine sağ tıklayın, **Görevler**' e ve ardından **komut dosyaları oluştur**' a tıklayın.

    ![SSMS betik oluştur](preparing-databases/_static/image11.png)
4. **Betikleri oluştur ve Yayımla** Iletişim kutusunda **betik seçeneklerini ayarla**' ya tıklayın.

    Varsayılan **tüm veritabanı ve tüm veritabanı nesneleri** ve istediğiniz şey olduğu Için, **nesneleri Seç** adımını atlayabilirsiniz.
5. **Gelişmiş**'e tıklayın.

    ![SSMS komut dosyası seçenekleri](preparing-databases/_static/image12.png)
6. **Gelişmiş betik seçenekleri** iletişim kutusunda, **betikteki veri türlerine**aşağı kaydırın ve açılan listede **yalnızca veri** seçeneğine tıklayın.
7. **BETIK kullanım veritabanını** **yanlış**olarak değiştirin. USE deyimleri Azure SQL veritabanı için geçerli değildir ve test ortamında SQL Server Express dağıtım için gerekli değildir.

    ![Yalnızca SSMS betik verileri, USE bildirisi yok](preparing-databases/_static/image13.png)
8. **Tamam**'a tıklayın.
9. **Komut dosyaları oluştur ve Yayımla** Iletişim kutusunda **dosya adı** kutusu, betiğin nerede oluşturulacağını belirtir. Çözüm klasörünüzün yolunu (ContosoUniversity. sln dosyasını içeren klasör) ve dosya adını *ASPNET-Data-dev. SQL*olacak şekilde değiştirin.
10. **İleri** ' ye tıklayarak **Özet** sekmesine gidin ve ardından yeniden **İleri** ' ye tıklayarak betiği oluşturun.

    ![SSMS betiği oluşturuldu](preparing-databases/_static/image14.png)
11. **Son**'a tıklayın.

### <a name="create-the-production-database-script"></a>Üretim veritabanı betiğini oluşturma

Projeyi üretim veritabanıyla çalıştırmadığınız için, henüz LocalDB örneğine eklenmez. Bu nedenle, önce veritabanını iliştirmelisiniz.

1. SSMS **Nesne Gezgini** **veritabanları** ' na sağ tıklayın ve **Ekle**' ye tıklayın.

    ![SSMS Iliştirme](preparing-databases/_static/image15.png)
2. **Veritabanları Ekle** Iletişim kutusunda **Ekle** ' ye tıklayın ve ardından *App\_veri* klasöründeki *ASPNET-ContosoUniversity-prod. mdf* dosyasına gidin.

     ![SSMS eklenecek. mdf dosyası Ekle](preparing-databases/_static/image16.png)
3. **Tamam**'a tıklayın.
4. Daha önce üretim dosyası için bir komut dosyası oluşturmak üzere kullandığınız yordamın aynısını izleyin. Betik dosyası *ASPNET-Data-prod. SQL*olarak adlandırın.

## <a name="summary"></a>Özet

Her iki veritabanı artık dağıtılmaya hazırdır ve çözüm klasörünüzde iki veri dağıtım betiğinin olması gerekir.

![Veri dağıtımı betikleri](preparing-databases/_static/image17.png)

Aşağıdaki öğreticide, dağıtımı etkileyen proje ayarlarını yapılandırır ve dağıtılan uygulamada farklı olması gereken ayarlar için otomatik *Web. config* dosyası dönüştürmeleri ayarlarsınız.

## <a name="more-information"></a>Daha fazla bilgi

NuGet hakkında daha fazla bilgi için bkz. NuGet ve [NuGet belgeleriyle](http://docs.nuget.org/docs/start-here/overview) [Proje kitaplıklarını yönetme](https://msdn.microsoft.com/magazine/hh547106.aspx) . NuGet 'i kullanmak istemiyorsanız, ne zaman yüklendiğini belirlemek için bir NuGet paketini nasıl analiz edeceğinizi öğrenmeniz gerekir. (Örneğin, *Web. config* dönüşümlerini yapılandırabilir, PowerShell betiklerini derleme zamanında çalışacak şekilde yapılandırabilir vs.) NuGet 'in nasıl çalıştığı hakkında daha fazla bilgi edinmek için bkz. bir paket ve [yapılandırma dosyası ve kaynak kodu dönüştürmeleri](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations) [oluşturma ve yayımlama](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) .

> [!div class="step-by-step"]
> [Önceki](introduction.md)
> [İleri](web-config-transformations.md)
