---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: SQL Server Compact veritabanları dağıtma-2/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: 56ceabc79947967846d342354fd033510be5f05a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78568119"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: SQL Server Compact veritabanları dağıtma-2/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bu öğreticide, dağıtım için iki SQL Server Compact veritabanı ve veritabanı altyapısının nasıl ayarlanacağı gösterilmektedir.

Veritabanı erişimi için Contoso University uygulaması, .NET Framework dahil edilmediğinden uygulamayla birlikte dağıtılması gereken aşağıdaki yazılımları gerektirir:

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) (veritabanı altyapısı).
- [ASP.net evrensel sağlayıcılar](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (ASP.NET üyelik sisteminin SQL Server Compact kullanmasını sağlar)
- [Entity Framework 5,0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)(geçişle Code First).

Veritabanı yapısı ve uygulamanın iki veritabanındaki verilerin bazı (tümü değil) dağıtılması da sağlanmalıdır. Genellikle, bir uygulama geliştirirken, canlı bir siteye dağıtmak istemediğiniz bir veritabanına test verileri girersiniz. Ancak, dağıtmak istediğiniz bazı üretim verilerini de girebilirsiniz. Bu öğreticide, dağıtım sırasında gerekli yazılımların ve doğru verilerin dahil edilmesini sağlamak için Contoso Üniversitesi projesini yapılandıracaksınız.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Compact ve SQL Server Express

Örnek uygulama 4,0 SQL Server Compact kullanır. Bu veritabanı altyapısı, Web siteleri için görece yeni bir seçenektir; SQL Server Compact önceki sürümleri bir Web barındırma ortamında çalışmaz. SQL Server Compact, SQL Server Express geliştirme ve tam SQL Server dağıtma konusunda daha yaygın olarak karşılaşılan senaryolarla karşılaştırıldığında birkaç avantaj sunar. Seçtiğiniz barındırma sağlayıcısına bağlı olarak, bazı sağlayıcılar bir tam SQL Server veritabanını desteklemek için ek ücret ödetiğinden, dağıtım için SQL Server Compact olabilir. Veritabanı altyapısını Web uygulamanızın bir parçası olarak dağıtabileceğiniz için SQL Server Compact ek ücret alınmaz.

Ancak, onun sınırlamalarından da haberdar olmanız gerekir. SQL Server Compact, saklı yordamları, Tetikleyicileri, görünümleri veya çoğaltmayı desteklemez. (SQL Server Compact tarafından desteklenmeyen SQL Server özelliklerinin tüm listesi için bkz. [SQL Server Compact ve SQL Server arasındaki farklılıklar](https://msdn.microsoft.com/library/bb896140.aspx).) Ayrıca, SQL Server Express ve SQL Server veritabanlarında şemaları ve verileri işlemek için kullanabileceğiniz araçlardan bazıları SQL Server Compact ile çalışmaz. Örneğin, SQL Server Compact veritabanları ile Visual Studio 'da SQL Server Management Studio veya SQL Server Veri Araçları kullanamazsınız. SQL Server Compact veritabanlarıyla çalışmak için başka seçenekleriniz vardır:

- SQL Server Compact için sınırlı veritabanı işleme işlevselliği sunan Visual Studio 'da Sunucu Gezgini kullanabilirsiniz.
- [WebMatrix](https://www.microsoft.com/web/webmatrix/)'in veritabanı işleme özelliğini kullanarak Sunucu Gezgini daha fazla özelliğe sahip olabilirsiniz.
- [SQL Server Compact araç kutusu](https://github.com/ErikEJ/SqlCeToolbox) ve [SQL Compact Data ve şema betiği yardımcı programı](https://github.com/ErikEJ/SqlCeToolbox)gibi görece tam özellikli üçüncü taraf veya açık kaynak araçları kullanabilirsiniz.
- Veritabanı şemasını işlemek için kendi DDL (veri tanımlama dili) betiklerinizi yazabilir ve çalıştırabilirsiniz.

SQL Server Compact ile başlayabilir ve ardından gereksinimleriniz geliştikçe daha sonra yükseltebilirsiniz. Bu serideki sonraki öğreticiler, SQL Server Compact SQL Server Express ve SQL Server arasında nasıl geçiş yapılacağını gösterir. Bununla birlikte, yeni bir uygulama oluşturuyorsanız ve yakın gelecekte SQL Server ihtiyaç duyduğunuz için, en iyisi SQL Server veya SQL Server Express ile başlamayız.

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>Dağıtım için SQL Server Compact veritabanı altyapısını yapılandırma

Contoso Üniversitesi uygulamasındaki veri erişimi için gereken yazılım aşağıdaki NuGet paketleri yüklenerek eklenmiştir:

- [SqlServerCompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System. Web. Providers](http://nuget.org/List/Packages/System.Web.Providers) (ASP.net Universal Providers)
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework. SqlServerCompact](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

Bağlantılar bu paketlerin güncel sürümlerini işaret ediyor. Bu, bu öğretici için indirdiğiniz Başlatıcı projesinde yüklü olandan daha yeni olabilir. Bir barındırma sağlayıcısına dağıtım için Entity Framework 5,0 veya sonraki bir sürümü kullandığınızdan emin olun. Code First Migrations önceki sürümleri tam güven gerektirir ve uygulamanız orta düzeyde güvende çalışır. Orta güven hakkında daha fazla bilgi için bkz. [test ortamı olarak IIS 'ye dağıtma](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) öğreticisi.

NuGet paketi yüklemesi, bu yazılımı uygulamayla dağıtmak için ihtiyaç duyduğunuz her şeyi üstlenir. Bazı durumlarda bu, Web. config dosyasını değiştirme ve çözümü her oluşturduğunuzda çalışan PowerShell betikleri ekleme gibi görevleri içerir. **NuGet kullanmadan bu özelliklerden herhangi biri için (SQL Server Compact ve Entity Framework) destek eklemek istiyorsanız, aynı çalışmayı el ile yapabilmeniz için NuGet paket yüklemesinin ne yaptığını bildiğinize emin olun.**

Başarılı bir dağıtım sağlamak için NuGet 'in gerçekleştirmeniz gereken her şeyi karşılayıp bir istisna vardır. SqlServerCompact NuGet paketi, yerel derlemeleri proje *bin* klasörü altındaki *x86* ve *AMD64* alt klasörlerine kopyalayan bir oluşturma sonrası betiği ekler, ancak betik projedeki bu klasörleri içermez. Sonuç olarak, bunları projeye el ile eklemediğiniz sürece Web Dağıtımı hedef Web sitesine kopyalamamasını sağlar. (Bu davranış, varsayılan dağıtım yapılandırmasından kaynaklanır; bu öğreticilerde kullanmayabilmeniz gereken başka bir seçenek ise bu davranışı denetleyen ayarı değiştirkullanmaktır. Değiştirebileceğiniz ayar yalnızca, **Proje özellikleri** penceresinin **Package/Publish Web** sekmesinde **dağıtılacak öğeler** altında **uygulamayı çalıştırmak için gereken dosyalardır** . Bu ayarın değiştirilmesi genellikle önerilmez çünkü bu, daha fazla dosyanın daha fazla sayıda daha fazla dosya dağıtımına gerek duyulduğundan daha fazla. Alternatifler hakkında daha fazla bilgi için bkz. [Proje özelliklerini yapılandırma](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md) öğreticisi.)

Projeyi derleyin ve ardından **Çözüm Gezgini** daha önce yapmadıysanız **tüm dosyaları göster** ' e tıklayın. **Yenile**' ye tıklamanız da gerekebilir.

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

**AMD64** ve **x86** klasörlerini görmek için **bin** klasörünü genişletin ve ardından bu klasörleri seçin, sağ tıklayın ve **projeye dahil et**' i seçin.

![amd64_and_x86_in_Solution_Explorer. png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

Klasör simgeleri, klasörün projeye dahil edildiğini gösterecek şekilde değişir.

![Solution_Explorer_amd64_included.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>Uygulama veritabanı dağıtımı için Code First Migrations yapılandırma

Bir uygulama veritabanını dağıttığınızda, genellikle geliştirme veritabanınızı yalnızca test amaçlı olarak yalnızca sınama amacıyla bu, içindeki verilerin büyük bir kısmını üretime dağıtmazsınız. Örneğin, bir test veritabanındaki öğrenci adları kurgusal değildir. Öte yandan, genellikle yalnızca veritabanı yapısını hiç veri olmadan dağıtamazsınız. Test Veritabanınızdaki bazı veriler gerçek veriler olabilir ve kullanıcılar uygulamayı kullanmaya başladığınızda bu durumda olmalıdır. Örneğin, veritabanınız geçerli bir sınıf değerleri veya gerçek departman adları içeren bir tabloya sahip olabilir.

Bu ortak senaryonun benzetimini yapmak için, yalnızca üretimde olmasını istediğiniz verileri veritabanına ekleyen bir Code First Migrations tohum yöntemi yapılandıracaksınız. Bu çekirdek Yöntem test verilerini eklemez çünkü Code First üretim sırasında veritabanını oluşturduktan sonra üretimde çalışacaktır.

Geçiş işleminden önce Code First önceki sürümlerinde, geliştirme sırasında her model değiştiğinden veritabanının tamamen silinmesi ve sıfırdan yeniden oluşturulması gerekiyordu, çünkü geliştirme sırasında her model değişikliğine yönelik olarak test verilerinin eklenmesi yaygındır. Code First Migrations ile test verileri, veritabanı değişikliklerinden sonra tutulur, bu nedenle çekirdek yöntemindeki test verileri dahil değildir. İndirdiğiniz proje, başlatıcı sınıfının çekirdek yöntemindeki tüm verileri dahil etmek için geçiş öncesi yöntemini kullanır. Bu öğreticide Başlatıcı sınıfını devre dışı bırakıp geçişleri etkinleştireceksiniz. Daha sonra, yalnızca üretime eklenmesini istediğiniz verileri eklemek için geçişler yapılandırma sınıfındaki çekirdek yöntemi güncelleştireceksiniz.

Aşağıdaki diyagramda uygulama veritabanının şeması gösterilmektedir:

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

Bu öğreticiler için, site ilk dağıtıldığında `Student` ve `Enrollment` tablolarının boş olması gerektiğini varsayabilirsiniz. Diğer tablolar, uygulama canlı kaldığında önceden yüklenmesi gereken verileri içerir.

Code First Migrations kullanacağınız için, artık **Dropcreatedatabaseifmodelchanges** Code First başlatıcısı 'nı kullanmanız gerekmez. Bu başlatıcının kodu, ContosoUniversity. DAL projesindeki SchoolInitializer.cs dosyasıdır. Web. config dosyasının **appSettings** öğesindeki bir ayar, uygulama veritabanına ilk kez erişmeyi her denediğinde bu başlatıcının çalışmasına neden olur:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

Uygulama Web. config dosyasını açın ve appSettings öğesinden Code First Başlatıcı sınıfını belirten öğeyi kaldırın. AppSettings öğesi şu şekilde görünür:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> Bir başlatıcı sınıfı belirtmenin başka bir yolu da, *Global. asax* dosyasındaki `Application_Start` yönteminde `Database.SetInitializer` çağırarak yapılır. Başlatıcıyı belirtmek için bu yöntemi kullanan bir projede geçişleri etkinleştirirseniz, bu kod satırını kaldırın.

Sonra Code First Migrations etkinleştirin.

İlk adım, ContosoUniversity projesinin başlangıç projesi olarak ayarlandığından emin olmak. **Çözüm Gezgini**, contosouniversity projesine sağ tıklayın ve **Başlangıç projesi olarak ayarla**' yı seçin. Code First Migrations, veritabanı bağlantı dizesini bulmak için başlangıç projesine bakacaktır.

**Araçlar** menüsünden **NuGet Paket Yöneticisi**’ne ve ardından **Paket Yöneticisi Konsolu**’na tıklayın.

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

**Paket Yöneticisi konsol** penceresinin en üstündeki contosouniversity. dal ' i varsayılan proje olarak seçin ve ardından `PM>` istemine "Enable-geçişler" yazın.

![Enable-migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

Bu komut, ContosoUniversity. DAL projesindeki yeni bir *geçişler* klasöründe bir *Configuration.cs* dosyası oluşturur.

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

"Enable-geçişler" komutu Code First bağlam sınıfını içeren projede yürütülmesi gerektiğinden DAL projesini seçtiniz. Bu sınıf bir sınıf kitaplığı projesinde olduğunda, Code First Migrations çözüm için başlangıç projesindeki veritabanı bağlantı dizesini arar. ContosoUniversity çözümünde, Web projesi başlangıç projesi olarak ayarlanmıştır. (Bağlantı dizesine sahip projeyi Visual Studio 'da başlangıç projesi olarak belirlemek istemiyorsanız, PowerShell komutunda başlangıç projesini belirtebilirsiniz. Enable-geçişler komutunun komut sözdizimini görmek için "Get-Help Enable-geçişler" komutunu girebilirsiniz.)

Configuration.cs dosyasını açın ve `Seed` yöntemindeki açıklamaları aşağıdaki kodla değiştirin:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

`List` başvurular, ad alanı için henüz bir `using` deyiminiz olmadığından bunlar altında kırmızı dalgalı çizgilere sahiptir. `List` örneklerinden birine sağ tıklayın ve **Çözümle**' ye tıklayın ve ardından **System. Collections. Generic kullanma**' ya tıklayın.

![Using ifadesiyle çözümle](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

Bu menü seçimi, dosyanın en üstüne yakın `using` deyimlerine aşağıdaki kodu ekler.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> `Seed` yöntemine kod eklemek, veritabanına sabit veri ekleyebilmenizin birçok yönteminden biridir. Alternatif olarak, her bir geçiş sınıfının `Up` ve `Down` yöntemlerine kod eklemektir. `Up` ve `Down` yöntemleri, veritabanı değişikliklerini uygulayan kodu içerir. [Veritabanı güncelleştirme](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) öğreticisinde bunlara örnekler görürsünüz.
> 
> Ayrıca, `Sql` yöntemini kullanarak SQL deyimlerini yürüten bir kod yazabilirsiniz. Örneğin, bölüm tablosuna bir bütçe sütunu ekliyorsanız ve bir geçişin parçası olarak tüm bölüm bütçelerini $1.000,00 olarak başlatmak istiyorsanız, bu geçiş için `Up` yöntemine aşağıdaki kod satırını ekleyebilirsiniz:
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> Bu öğretici için gösterilen bu örnek, Code First Migrations `Configuration` sınıfının `Seed` yönteminde `AddOrUpdate` yöntemini kullanır. Code First Migrations her geçişten sonra `Seed` yöntemini çağırır ve bu yöntem önceden eklenmiş satırları güncelleştirir veya henüz yoksa ekler. `AddOrUpdate` yöntemi senaryonuz için en iyi seçim olmayabilir. Daha fazla bilgi için bkz. Julie Lerman 'ın blogundan [EF 4,3 AddOrUpdate yöntemiyle ilgilenme](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) .

Projeyi derlemek için CTRL-SHIFT-B tuşlarına basın.

Sonraki adım, ilk geçiş için bir `DbMigration` sınıfı oluşturmaktır. Bu geçişin yeni bir veritabanı oluşturmasını istiyorsunuz, bu nedenle zaten mevcut olan veritabanını silmeniz gerekir. SQL Server Compact veritabanları, *App\_Data* klasöründeki *. sdf* dosyalarında bulunur. **Çözüm Gezgini**, *. sdf* dosyaları tarafından temsil edilen iki SQL Server Compact veritabanını görmek Için contosouniversity projesindeki *uygulama\_verileri* ' ni genişletin.

*Okul. sdf* dosyasına sağ tıklayın ve **Sil**' e tıklayın.

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

**Paket Yöneticisi konsolu** penceresinde, ilk geçişi oluşturmak ve "ilk" olarak adlandırmak için "Add-geçiş Initial" komutunu girin.

![migration_command Ekle](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First Migrations *geçişler* klasöründe başka bir sınıf dosyası oluşturur ve bu sınıf veritabanı şemasını oluşturan kodu içerir.

**Paket Yöneticisi konsolunda**, veritabanını oluşturmak ve **çekirdek** yöntemini çalıştırmak için "Update-Database" komutunu girin.

![güncelleştirme-database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

(Bir tablonun zaten var olduğunu ve oluşturulamayabileceğini belirten bir hata alırsanız, veritabanını sildikten sonra ve `update-database`çalıştırmadan önce uygulamayı çalıştırmanızdan kaynaklanıyor olabilirsiniz. Bu durumda, *okul. sdf* dosyasını yeniden silin ve `update-database` komutunu yeniden deneyin.)

Uygulamayı çalıştırın. Artık öğrenciler sayfası boştur, ancak eğitmenler sayfası eğitmenler içerir. Bu, uygulamayı dağıttıktan sonra üretime alacağınız şeydir.

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

Proje artık *okul* veritabanını dağıtmaya hazırdır.

## <a name="creating-a-membership-database-for-deployment"></a>Dağıtım için bir üyelik veritabanı oluşturma

Contoso Üniversitesi uygulaması, kullanıcıların kimliğini doğrulamak ve yetkilendirmek için ASP.NET üyelik sistemi ve Forms kimlik doğrulamasını kullanır. Sayfalarından birine yalnızca yöneticiler erişebilir. Bu sayfayı görmek için, uygulamayı çalıştırın ve **Kurslar**' ın altındaki açılır menüden **kredileri Güncelleştir** ' i seçin. Uygulama, yalnızca Yöneticiler **kredileri güncelleştirme** sayfasını kullanma yetkisine sahip olduğu Için **oturum açma** sayfasını görüntüler.

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

"Pas $ w0rd" parolasını kullanarak "Yönetici" olarak oturum açın ("w0rd" içinde "o" harfi yerine sıfır sayısını görürsünüz). Oturum açtıktan sonra **kredileri güncelleştirme** sayfası görüntülenir.

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

Bir siteyi ilk kez dağıttığınızda, test için oluşturduğunuz Kullanıcı hesaplarının çoğunun veya tümünün hariç tutulması yaygındır. Bu durumda, bir yönetici hesabı ve Kullanıcı hesabı dağıtacaksınız. Test hesaplarını el ile silmek yerine, yalnızca üretimde ihtiyacınız olan bir yönetici kullanıcı hesabına sahip yeni bir üyelik veritabanı oluşturacaksınız.

> [!NOTE]
> Üyelik veritabanı, hesap parolalarının karmasını depolar. Hesapların bir makineden diğerine dağıtılması için, karma yordamların hedef sunucuda kaynak bilgisayarda olduklarından farklı karmaları oluşturmadıklarından emin olmanız gerekir. Varsayılan algoritmayı değiştirmedikçe, ASP.NET Universal sağlayıcılarını kullandığınızda aynı karmaları oluşturur. Varsayılan algoritma HMACSHA256 ' dir ve Web. config dosyasındaki **[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** öğesinin **doğrulama** özniteliğinde belirtilir.

Üyelik veritabanı Code First Migrations tarafından korunmaz ve veritabanında test hesaplarıyla (okul veritabanı için olduğu gibi) bir otomatik Başlatıcı yoktur. Bu nedenle, test verilerinin kullanılabilmesini sağlamak için yeni bir tane oluşturmadan önce test veritabanının bir kopyasını yaparsınız.

**Çözüm Gezgini**, *App\_Data* klasöründeki *Aspnet. sdf* dosyasını *ASPNET-dev. sdf*olarak yeniden adlandırın. (Kopya yapmayın, yeniden adlandırın; bir süre içinde yeni bir veritabanı oluşturacaksınız.)

**Çözüm Gezgini**, Web projesinin (contosoüniversitesi, CONTOSOUNIVERSITY. dal değil) seçili olduğundan emin olun. Ardından, **Proje** menüsünde **ASP.net Configuration** ' ı seçerek **Web sitesi yönetim aracı**'nı (WAT) çalıştırın.

**Güvenlik** sekmesini seçin.

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

**Roller oluştur veya Yönet** ' e tıklayın ve bir **yönetici** rolü ekleyin.

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

**Güvenlik** sekmesine geri gidin, **Kullanıcı oluştur**' a tıklayın ve yönetici olarak "Yönetici" kullanıcısını ekleyin. **Kullanıcı oluştur** sayfasındaki **Kullanıcı oluştur** düğmesine tıklamadan önce **yönetici** onay kutusunu seçtiğinizden emin olun. Bu öğreticide kullanılan parola "pas $ w0rd" ve herhangi bir e-posta adresi girebilirsiniz.

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

Tarayıcıyı kapatın. **Çözüm Gezgini**, yeni *Aspnet. sdf* dosyasını görmek için Yenile düğmesine tıklayın.

![New_aspnet.sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

**Aspnet. sdf** öğesine sağ tıklayın ve **projeye dahil et**' i seçin.

## <a name="distinguishing-development-from-production-databases"></a>Üretim veritabanlarından geliştirmeyi ayırt etme

Bu bölümde, geliştirme sürümlerinin School-Dev. sdf ve aspnet-Dev. sdf ve üretim sürümleri School-Prod. sdf ve aspnet-Prod. sdf olacak şekilde veritabanlarını yeniden adlandırmanız gerekir. Bu gerekli değildir, ancak bunu yapmak, veritabanlarının test ve üretim sürümlerini almanızı sağlamanıza yardımcı olur.

**Çözüm Gezgini**, **Yenile** ' ye tıklayın ve daha önce oluşturduğunuz okul veritabanını görmek için uygulama\_verileri klasörünü genişletin; sağ tıklayın ve **projeye dahil et**' i seçin.

![Including_School. sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

*Aspnet. sdf* öğesini *ASPNET-prod. sdf*olarak yeniden adlandırın.

*Okul. sdf* ' i *School-dev. sdf*olarak yeniden adlandırın.

Uygulamayı Visual Studio 'da çalıştırdığınızda, veritabanı dosyalarının *-Üretim* sürümlerini kullanmak istemezsiniz, *-dev* sürümlerini kullanmak istersiniz. Bu nedenle, Web. config dosyasındaki bağlantı dizelerini veritabanlarının *-dev* sürümlerini işaret etmek üzere değiştirmeniz gerekir. (Bir School-Prod. sdf dosyası oluşturmadınız, ancak Code First uygulamanızı ilk kez çalıştırdığınızda bu veritabanını üretimde oluşturabileceğinden bu işlem tamam.)

Uygulama Web. config dosyasını açın ve bağlantı dizelerini bulun:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

"Aspnet. sdf" öğesini "aspnet-Dev. sdf" olarak değiştirin ve "okul. sdf" öğesini "School-Dev. sdf" olarak değiştirin:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

SQL Server Compact veritabanı altyapısı ve her iki veritabanı artık dağıtılmaya hazırdır. Aşağıdaki öğreticide, geliştirme, test ve üretim ortamlarında farklı olması gereken ayarlar için otomatik *Web. config* dosyası dönüştürmeleri ayarlarsınız. (Değiştirilmesi gereken ayarlar arasında bağlantı dizeleridir, ancak bir yayımlama profili oluştururken bu değişiklikleri daha sonra ayarlarsınız.)

## <a name="more-information"></a>Daha Fazla Bilgi

NuGet hakkında daha fazla bilgi için bkz. NuGet ve [NuGet belgeleriyle](http://docs.nuget.org/docs/start-here/overview) [Proje kitaplıklarını yönetme](https://msdn.microsoft.com/magazine/hh547106.aspx) . NuGet 'i kullanmak istemiyorsanız, ne zaman yüklendiğini belirlemek için bir NuGet paketini nasıl analiz edeceğinizi öğrenmeniz gerekir. (Örneğin, *Web. config* dönüşümlerini yapılandırabilir, PowerShell betiklerini derleme zamanında çalışacak şekilde yapılandırabilir vs.) NuGet 'in nasıl çalıştığı hakkında daha fazla bilgi edinmek için, bkz. özellikle bir paket ve [yapılandırma dosyası ve kaynak kodu dönüştürmeleri](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations) [oluşturma ve yayımlama](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) .

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [İleri](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
