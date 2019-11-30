---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 'Visual Studio kullanarak Web dağıtımını ASP.NET: giriş | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, V... kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: 96dd31d949633e001fc595621bedbf74e98000fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640232"
---
# <a name="aspnet-web-deployment-using-visual-studio-introduction"></a>Visual Studio kullanarak Web dağıtımını ASP.NET: giriş

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, .NET için Azure SDK ile Visual Studio 2012 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Yordamların çoğu Visual Studio 2013 benzerdir.
> 
> Bir Web uygulamasını Internet üzerinden insanlar için kullanılabilir hale getirmek üzere geliştirirsiniz. Ancak, Web programlama öğreticileri genellikle geliştirme bilgisayarınızda çalışan bir şeyin nasıl alınacağını gösterdikten hemen sonra durur. Bu öğretici serisi, diğerlerinin nereden ayrıldığı yerde başlar: bir Web uygulaması oluşturdunuz, test edilmiştir ve başlamaya hazır. Sırada ne var? Bu öğreticiler, ilk olarak yerel geliştirme bilgisayarınızda, test için Azure 'a veya hazırlama ve üretim için bir üçüncü taraf barındırma sağlayıcısına nasıl dağıtım yapılacağını gösterir. Dağıtacağınız örnek uygulama, Entity Framework, SQL Server ve ASP.NET üyelik sistemi kullanan bir Web uygulaması projem. Örnek uygulama, ASP.NET Web Forms kullanır, ancak gösterilen yordamlar ASP.NET MVC ve Web API için de geçerlidir.
> 
> Bu öğreticiler, Visual Studio 'da ASP.NET ile nasıl çalışabileceğinizi bildiğinizi varsayar. Aksi takdirde, başlamak için [temel bir ASP.NET Web Forms öğreticisi](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md) veya [temel bir ASP.NET MVC öğreticisidir](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).
> 
> Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET Deployment Forumu](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) veya [StackOverflow](http://stackoverflow.com)'e gönderebilirsiniz.
> 
> Bu içerik [TechNet e-kitap galerisinde](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio)ücretsiz bir e-kitap olarak da kullanılabilir.

## <a name="overview"></a>Genel bakış

Bu öğreticiler, SQL Server veritabanları içeren bir ASP.NET Web uygulaması dağıtma konusunda size rehberlik eder. Öncelikle, test için yerel geliştirme bilgisayarınızda IIS 'e ve ardından Azure App Service ve Azure SQL veritabanı 'nda hazırlama ve üretim için Web Apps. Visual Studio tek tıklamayla Yayımla ' yı kullanarak nasıl dağıtacağınızı görürsünüz ve komut satırını kullanarak nasıl dağıtım yapılacağını görürsünüz.

Eğitim sayısı dağıtım sürecini korkuttabilir. Aslında temel yordamlar basittir. Bununla birlikte, gerçek dünyada durumlarda genellikle ek dağıtım görevleri yapmanız gerekir — örneğin, hedef sunucuda klasör izinleri ayarlama. Bu ek görevlerden bazılarını gördünüz, bu da öğreticilerin gerçek bir uygulamayı başarıyla dağıtmanıza engel olabilecek bilgilerin çıkmıyor olduğunu umuyoruz.

Öğreticiler sırayla çalışacak şekilde tasarlanmıştır ve her bölüm önceki bölümde oluşturulur. Durumunuza uygun olmayan parçaları atlayabilirsiniz, ancak daha sonra öğreticilerde daha sonra yordamları ayarlamanız gerekebilir.

## <a name="intended-audience"></a>Hedeflenen hedef kitle

Öğreticiler, şu durumlarda ortamlarda çalışan ASP.NET geliştiricileri için tasarlanmıştır:

- Üretim ortamı, Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcıdır.
- Dağıtım sürekli tümleştirme işlemiyle sınırlı değildir ancak doğrudan Visual Studio 'dan yapılabilir.

[Sürekli teslim](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) süreci kullanılarak [kaynak denetiminden](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md) dağıtım, komut satırından nasıl dağıtılacağını gösteren bir öğretici haricinde bu öğreticilerde ele alınmıyor. Sürekli teslim hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Sürekli tümleştirme ve sürekli teslim (Microsoft Azure ile gerçek hayatta bulut uygulamaları oluşturma)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [Azure App Service bir Web uygulaması dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [Kurumsal senaryolarda Web uygulamaları dağıtma](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md) (Visual Studio 2010 için yazılmış daha eski bir öğretici kümesi, kurumsal ortamlar için de faydalı bilgiler içerir.)

## <a name="using-a-third-party-hosting-provider"></a>Üçüncü taraf barındırma sağlayıcısı kullanma

Öğreticiler, bir Azure hesabı ayarlama ve uygulamayı hazırlama ve üretim için Azure App Service Web Apps dağıtım sürecinde size götürür. Ancak, tercih ettiğiniz üçüncü taraf bir barındırma sağlayıcısına dağıtmak için aynı temel yordamları kullanabilirsiniz. Öğreticilerin Azure 'a özgü işlemlerin üzerinde yaptığı yerlerde, bu, bir üçüncü taraf barındırma sağlayıcısında beklendiğiniz farklılıkları açıklar ve bu şekilde önerilerde bulunabilir.

## <a name="deploying-web-app-projects"></a>Web uygulaması projelerini dağıtma

Bu öğreticiler için indirileceği ve dağıttığınız örnek uygulama bir Visual Studio Web uygulaması projem. Ancak, Visual Studio için en son Web yayımlama güncelleştirmesini yüklerseniz, Web uygulaması projeleri için aynı dağıtım yöntemlerini ve araçlarını kullanabilirsiniz.

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC projelerini dağıtma

Örnek uygulama bir ASP.NET Web Forms projem, ancak nasıl yapılacağını öğrendiği her şey ASP.NET MVC için de geçerlidir. Visual Studio MVC projesi yalnızca başka bir Web uygulaması projesi biçimidir. Tek fark, ASP.NET MVC 'yi veya hedef sürümünüzü desteklemeyen bir barındırma sağlayıcısına dağıtım yapıyorsanız, projenize uygun ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0), [MVC 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0)veya [MVC 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)) NuGet paketini yüklediğinizden emin olmanız gerekir.

## <a name="programming-language"></a>Programlama dili

Örnek uygulama kullanır C# C#, ancak öğreticiler bilgi gerektirmez ve öğreticiler tarafından gösterilen dağıtım teknikleri dile özgü değildir.

## <a name="database-deployment-methods"></a>Veritabanı dağıtım yöntemleri

Visual Studio 'da Web dağıtımıyla birlikte SQL Server veritabanı dağıtmak için üç yol vardır:

- Entity Framework Code First Migrations
- DbDacFx Web Dağıtımı sağlayıcısı
- DbFullSql Web Dağıtımı sağlayıcısı

Bu öğreticide, bu yöntemlerin ilk ikisini kullanacaksınız. DbFullSql Web Dağıtımı sağlayıcısı, SQL Server Compact SQL Server ' den geçiş gibi bazı senaryolar haricinde artık önerilmeyen eski bir yöntemdir.

Bu öğreticide gösterilen Yöntemler, SQL Server Compact değil SQL Server veritabanlarına yöneliktir. SQL Server Compact veritabanının nasıl dağıtılacağı hakkında bilgi için, bkz. [SQL Server Compact Ile Visual Studio Web dağıtımı](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md).

Bu öğreticide gösterilen Yöntemler Web Dağıtımı Publish metodunu kullanmanızı gerektirir. FTP, dosya sistemi veya FPSE gibi farklı bir yayımlama yöntemini tercih ediyorsanız, Visual Studio ve ASP.NET için Web dağıtımı Içerik haritasında [Web uygulaması dağıtımından ayrı bir veritabanı dağıtma](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate) konusuna bakın.

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First Migrations

Entity Framework sürüm 4,3 ' de, Microsoft Code First Migrations tanıtılmıştır. Code First Migrations, bir veri modelinde artımlı değişiklikler yapma ve bu değişiklikleri veritabanına yayma sürecini otomatikleştirir. Code First önceki sürümlerinde, genellikle veri modelini her değiştirdiğinizde veritabanını bırakıp yeniden oluşturmaya Entity Framework izin verin. Test verilerinin kolayca yeniden oluşturulduğu için bu bir sorun değildir, ancak üretimde genellikle veritabanı şemasını veritabanını bırakmadan güncellemek istersiniz. Geçişler özelliği Code First veritabanını bırakıp yeniden oluşturmadan güncelleştirilmesini sağlar. Gerekli şema değişikliklerinin nasıl yapılacağı Code First otomatik olarak karar verebilir veya değişiklikleri özelleştiren kodu yazabilirsiniz. Code First Migrations giriş için bkz. [Code First Migrations](https://msdn.microsoft.com/library/hh770484.aspx).

Bir Web projesi dağıttığınızda, Visual Studio Code First Migrations tarafından yönetilen bir veritabanını dağıtma işlemini otomatikleştirebilir. Yayımlama profilini oluştururken, Çalıştır Code First Migrations etiketli bir onay kutusunu seçersiniz (uygulama başlatıldığında çalışır). Bu ayar, dağıtım işleminin, Code First `MigrateDatabaseToLatestVersion` Başlatıcı sınıfını kullanması için hedef sunucudaki uygulama Web. config dosyasını otomatik olarak yapılandırmasına neden olur.

Visual Studio, dağıtım işlemi sırasında veritabanıyla hiçbir şey yapmaz. Dağıtılan uygulama dağıtımdan sonra veritabanına ilk kez eriştiğinde, Code First otomatik olarak veritabanını oluşturur veya veritabanı şemasını en son sürüme güncelleştirir. Uygulama bir geçişler çekirdek yöntemi uygularsa, yöntem veritabanı oluşturulduktan sonra veya şema güncelleştirildikten sonra çalışır.

Bu öğreticide uygulama veritabanını dağıtmak için Code First Migrations kullanacaksınız.

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx Web Dağıtımı sağlayıcısı

Entity Framework Code First tarafından yönetilmeyen SQL Server veritabanı için, yayımlama profilini yapılandırırken veritabanını güncelleştir etiketli bir onay kutusunu seçebilirsiniz. İlk dağıtım sırasında dbDacFx sağlayıcısı, kaynak veritabanıyla eşleşecek şekilde hedef veritabanında tablolar ve diğer veritabanı nesneleri oluşturur. Sonraki dağıtımlarda sağlayıcı, kaynak ve hedef veritabanları arasında nelerin farklı olduğunu belirler ve hedef veritabanının şemasını kaynak veritabanıyla eşleşecek şekilde güncelleştirir. Varsayılan olarak, sağlayıcı, bir tablo veya sütun bırakıldığında olduğu gibi veri kaybına neden olan herhangi bir değişiklik yapmayacaktır.

Bu yöntem, veritabanı tablolarındaki verilerin dağıtımını otomatik hale getirmez, ancak bunu yapmak için betikler oluşturabilir ve Visual Studio 'Yu dağıtım sırasında çalıştıracak şekilde yapılandırabilirsiniz. Dağıtım sırasında betikleri çalıştırmanın başka bir nedeni de, veri kaybına neden olacağından otomatik olarak gerçekleştirilen şema değişiklikleri yapmadır.

Bu öğreticide, ASP.NET üyelik veritabanını dağıtmak için dbDacFx sağlayıcısını kullanacaksınız.

## <a name="troubleshooting-during-this-tutorial"></a>Bu öğretici sırasında sorun giderme

Dağıtım sırasında bir hata oluştuğunda veya dağıtılan Site doğru şekilde çalıştırılmazsa, hata iletileri her zaman açık bir çözüm sağlamaz. Bazı yaygın sorun senaryolarında size yardımcı olmak için [sorun giderme başvurusu sayfası](troubleshooting.md) kullanılabilir. Bir hata iletisi alırsanız veya öğreticilerle karşılaştığınızdan bir şey çalışmadıysanız, sorun giderme sayfasını kontrol ettiğinizden emin olun.

## <a name="comments-welcome"></a>Yorumlara hoş geldiniz

Öğreticilerle ilgili açıklamalar hoş geldiniz ve öğretici, öğreticinin ne zaman güncelleştirildiği, öğretici açıklamalarında sunulan geliştirmeler için hesap düzeltmelerini veya önerilerini almak üzere her çaba sunulacaktır.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Prerequisites

Bu öğretici aşağıdaki ürünler için yazılmıştır:

- Windows 8 veya Windows 7.
- [En son güncelleştirme](https://go.microsoft.com/fwlink/?LinkId=272486)ile Web Için visual Studio 2012 veya visual Studio 2012 Express.
- [Visual Studio için Azure SDK 2012](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio 2010 SP1 veya Visual Studio 2013 kullanarak öğreticiyi izleyebilirsiniz, ancak bazı ekran görüntüleri farklı olur ve bazı özellikler farklı olacaktır.

Visual Studio 2013 kullanıyorsanız, [Visual Studio 2013 Için Azure SDK 'yı](https://go.microsoft.com/fwlink/?LinkID=324322)yükleyebilirsiniz.

Visual Studio 2010 SP1 kullanıyorsanız, aşağıdaki yazılımları yükleyebilirsiniz:

- [Visual Studio için Azure SDK 2010](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server veri araçları](https://msdn.microsoft.com/library/hh500335.aspx).

Makinenizde zaten sahip olduğunuz SDK bağımlılıklarının sayısına bağlı olarak, Azure SDK 'sının yüklenmesi uzun zaman alabilir ve birkaç dakika ile bir yarı saat veya daha fazla sürebilir. SDK, Visual Studio Web yayımlama özelliklerine yönelik en son güncelleştirmeleri içerdiğinden Azure yerine bir üçüncü taraf barındırma sağlayıcısına yayımlamayı planlıyor olsanız bile Azure SDK gerekir.

> [!NOTE]
> Bu öğretici, Azure SDK 'sının 1.8.1 sürümüyle yazılmıştır. Daha sonra ek özelliklere sahip daha yeni sürümler yayımlanmıştır. Öğreticiler bu özelliklerden bahsetmek ve bunlarla ilgili daha fazla bilgi içeren kaynaklara bağlantı sağlamak için güncelleştirilmiştir.

Yönergeler ve ekran görüntüleri Windows 8 ' i temel alır, ancak Öğreticiler Windows 7 ' de açıklanır.

Öğreticiyi tamamlayabilmeniz için bazı başka yazılımlar gerekir, ancak henüz yüklü olması gerekmez. Öğretici, ihtiyacınız olduğunda yükleme adımlarında size kılavuzluk eder.

## <a name="download-the-sample-application"></a>Örnek uygulamayı indirin

Dağıttığınız uygulama Contoso University olarak adlandırılır ve sizin için önceden oluşturulmuştur. Bu, [ASP.NET sitesindeki Entity Framework öğreticiler](https://asp.net/entity-framework/tutorials)bölümünde açıklanan Contoso University uygulamasına bağlı olarak, bir üniversite Web sitesinin basitleştirilmiş bir sürümüdür.

Önkoşulları yükledikten sonra [Contoso University Web uygulamasını](https://go.microsoft.com/fwlink/p/?LinkId=282627)indirin. *. Zip* dosyası projenin birden çok sürümünü içerir. Öğreticinin adımları aracılığıyla çalışmak için, C# klasöründe bulunan projeyle başlayın. Projenin öğreticilerin sonunda nasıl göründüğünü görmek için, projeyi ContosoUniversity-End klasöründe açın.

Projeyi öğretici adımları aracılığıyla çalışmak üzere hazırlamak için aşağıdaki adımları uygulayın:

1. Contosouniversity çözüm dosyalarını C# , Visual Studio projeleriyle çalışmak için kullandığınız herhangi bir klasörde contosouniversity adlı bir klasörde bulunan klasörden kaydedin.

    Varsayılan olarak, aşağıdaki Visual Studio 2012 klasörüdür:

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    (Bu öğreticideki ekran görüntüleri için, proje klasörü `C`: sürücü ' deki kök dizinde bulunur.)
2. Visual Studio 'Yu başlatın ve projeyi açın.
3. **Çözüm Gezgini**, çözüme sağ tıklayın ve **Enablenuget paketini geri yükle**' ye tıklayın.
4. Çözümü oluşturun.
5. Derleme hataları alırsanız NuGet paketlerini el ile geri yükleyin:

    1. **Çözüm Gezgini**, çözüme sağ tıklayın ve ardından **çözüm Için NuGet Paketlerini Yönet**' e tıklayın.
    2. **NuGet Paketlerini Yönet** iletişim kutusunun en üstünde, **Bu çözümde bazı NuGet paketleri yok ' u görürsünüz. Geri yüklemek için tıklayın.** **Geri yükle** düğmesine tıklayın.
    3. Çözümü yeniden derleyin.
6. Uygulamayı çalıştırmak için CTRL-F5 tuşlarına basın.

    Uygulama, Contoso Üniversitesi giriş sayfasında açılır.

    ![Giriş sayfası geliştirme](introduction/_static/image1.png)

    (Visual Studio SQL Server Express LocalDB örneğini başlattığında bir bekleme süresi olabilir ve bu işlem çok uzun sürerse zaman aşımı hatası alabilirsiniz. Bu durumda, projeyi yeniden başlatmanız yeterlidir.)

Web sitesi sayfalarına menü çubuğundan erişilebilir ve aşağıdaki işlevleri gerçekleştirmenize izin verilir:

- Öğrenci istatistiklerini görüntüleyin (hakkında sayfası).
- Öğrencileri görüntüleyin, düzenleyin, silin ve ekleyin.
- Kursları görüntüleyin ve düzenleyin.
- Eğitmenleri görüntüleyin ve düzenleyin.
- Departmanları görüntüleyin ve düzenleyin.

Aşağıda, birkaç temsili sayfanın ekran görüntüleri verilmiştir.

![Öğrenciler sayfası geliştirme](introduction/_static/image2.png)

![Öğrenciler ekleme sayfası geliştirme](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>Dağıtımı etkileyen uygulama özelliklerini gözden geçirme

Uygulamanın aşağıdaki özellikleri, nasıl dağıtabileceğinizi veya dağıtmak için ne yapmanız gerektiğini etkiler. Bunların her biri, serideki aşağıdaki öğreticilerde daha ayrıntılı olarak açıklanmıştır.

- Contoso University, öğrenci ve eğitmen adları gibi uygulama verilerini depolamak için bir SQL Server veritabanı kullanır. Veritabanı, test verilerinin ve üretim verilerinin bir karışımını içerir ve üretime dağıttığınızda test verilerini dışlayamazsınız.
- Uygulama, Kullanıcı hesabı bilgilerini bir SQL Server veritabanında depolayan ASP.NET üyelik sistemini kullanır. Uygulama, bazı kısıtlı bilgilere erişimi olan bir yönetici kullanıcıyı tanımlar. Üyelik veritabanını test hesapları olmadan, ancak bir yönetici hesabıyla dağıtmanız gerekir.
- Uygulama, üçüncü taraf hata günlüğü ve raporlama yardımcı programını kullanır. Bu yardımcı program, uygulamayla birlikte dağıtılması gereken bir derlemede sunulmaktadır.
- Hata günlüğü yardımcı programı, XML dosyalarındaki hata bilgilerini bir dosya klasörüne yazar. ASP.NET tarafından dağıtılan sitede çalıştığı hesabın bu klasöre yazma iznine sahip olduğundan ve bu klasörü dağıtımdan dışlamak zorunda olduğunuzdan emin olmanız gerekir. (Aksi takdirde, test ortamındaki hata günlüğü verileri üretime dağıtılabilir ve/veya üretim hata günlüğü dosyaları silinebilir.)
- Uygulama, hedef ortama (test, hazırlama veya üretim) ve derleme yapılandırmasına (hata ayıklama veya sürüm) bağlı olarak değiştirilmesi gereken diğer ayarlara bağlı olarak, dağıtılan *Web. config* dosyasında değiştirilmesi gereken bazı ayarları içerir.
- Visual Studio çözümü bir sınıf kitaplığı projesi içerir. Yalnızca bu projenin oluşturduğu derleme, projenin kendisi değil dağıtılmalıdır.

## <a name="summary"></a>Özet

Serideki bu ilk öğreticide, örnek Visual Studio projesini indirdiniz ve uygulamayı nasıl dağıtabileceğinizi etkileyen site özellikleri incelendi. Aşağıdaki öğreticilerde, bu öğelerin bazılarını otomatik olarak işlenecek şekilde ayarlayarak dağıtıma hazırlandınız. Başkalarının el ile ilgileni.

> [!div class="step-by-step"]
> [Next](preparing-databases.md)
