---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 'Visual Studio kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: giriş-1/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: ea88da1e6d510f706fc7ca370cfa32974c1243f8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525636"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>Visual Studio kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: giriş-1/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).
> 
> Bu öğreticiler, öncelikle test için yerel geliştirme bilgisayarınızda IIS 'ye, sonra da üçüncü taraf bir barındırma sağlayıcısına dağıtım sürecinde size rehberlik sağlar. Dağıttığınız uygulama bir uygulama veritabanını ve bir ASP.NET üyelik veritabanını kullanır. SQL Server Compact ve SQL Server Compact 'yi kullanmaya başlayın ve sonraki öğreticilerde, veritabanı değişikliklerinin nasıl dağıtılacağı ve SQL Server ' ye nasıl geçirileceği gösterilmektedir.
> 
> Öğreticiler, Visual Studio 'da ASP.NET ile nasıl çalışabileceğinizi kabul eder. Aksi takdirde, başlamak için [temel bir ASP.NET Web Forms öğreticisi](../tailspin-spyworks/tailspin-spyworks-part-1.md) veya [temel bir ASP.NET MVC öğreticisidir](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md).
> 
> Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET dağıtım forumuna](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)gönderebilirsiniz.

## <a name="overview"></a>Genel bakış

Bu öğreticiler, öncelikle test için yerel geliştirme bilgisayarınızda IIS 'ye, sonra da üçüncü taraf bir barındırma sağlayıcısına dağıtım sürecinde size rehberlik sağlar. Dağıttığınız uygulama bir uygulama veritabanını ve bir ASP.NET üyelik veritabanını kullanır. SQL Server Compact ve SQL Server Compact 'yi kullanmaya başlayın ve sonraki öğreticilerde, veritabanı değişikliklerinin nasıl dağıtılacağı ve SQL Server ' ye nasıl geçirileceği gösterilmektedir.

Sorun giderme sayfasında 11 ' in tümünde ve her türlü öğreticilerin sayısı – dağıtım sürecinin korunal hale gelebilir. Aslında, bir site dağıtmaya yönelik temel yordamlar, öğretici kümesinin görece küçük bir parçasını yapar. Bununla birlikte, gerçek dünyada durumlarda genellikle dağıtım için bazı küçük ancak önemli ek yönler hakkında bilgi almanız gerekir — örneğin, hedef sunucuda klasör izinleri ayarlama. Öğreticilerde bu ek tekniklerin çoğunu, öğreticilerin gerçek bir uygulamayı başarıyla dağıtmanıza engel olabilecek bilgilerin çıkmasının bir bölümünü ekledik.

Öğreticiler sırayla çalışacak şekilde tasarlanmıştır ve her bölüm önceki bölümde oluşturulur. Bununla birlikte, durumunuza uygun olmayan parçaları atlayabilirsiniz. (Parçaların atlanması, sonraki öğreticilerde yordamları ayarlamanızı gerektirebilir.)

## <a name="intended-audience"></a>Hedef Kitle

Öğreticiler, Küçük kuruluşlarda veya diğer ortamlarda çalışan ASP.NET geliştiricilerine (burada) sahiptir:

- Sürekli tümleştirme işlemi (otomatik derlemeler ve dağıtım) kullanılmaz.
- Üretim ortamı, üçüncü taraf bir barındırma sağlayıcıdır.
- Bir kişi genellikle birden çok rolü doldurur (aynı kişi geliştirir, sınar ve dağıtır).

Kurumsal ortamlarda, sürekli tümleştirme süreçlerini uygulamak daha normaldir ve üretim ortamı genellikle şirketin kendi sunucuları tarafından barındırılır. Farklı kişiler genellikle farklı roller de gerçekleştirir. Kurumsal Dağıtım hakkında daha fazla bilgi için bkz. [Enterprise senaryolarında Web uygulamaları dağıtma](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).

Her boyuttaki kuruluşlar de Web uygulamalarını Azure 'a dağıtabilir ve bu öğreticilerde gösterilen yordamların çoğu Azure Uygulama Hizmetleri Web Apps de geçerlidir. Azure 'a giriş için bkz. [https://azure.microsoft.com](https://azure.microsoft.com).

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>Öğreticilerde gösterilen barındırma sağlayıcısı

Öğreticiler, barındırma şirketiyle bir hesap ayarlama ve uygulamayı bu barındırma sağlayıcısına dağıtma sürecinde size kılavuzluk eden bir işlemdir. Öğreticilerin canlı bir Web sitesine dağıtmanın tüm deneyimini görebilmesi için belirli bir barındırma şirketi seçilmiştir. Her barındırma şirketi farklı özellikler sağlar ve sunucularına dağıtım deneyimi biraz farklılık gösterir. Ancak, bu öğreticide açıklanan işlem, genel işlem için tipik bir işlemdir.

Bu öğretici için kullanılan barındırma sağlayıcısı, Cytanium.com, kullanılabilir birçok bir tane ve bu öğreticide kullanımı bir onay veya öneri oluşturmaz.

## <a name="deploying-web-site-projects"></a>Web sitesi projelerini dağıtma

Contoso University, bir Visual Studio Web uygulaması projem. Bu öğreticide gösterilen dağıtım yöntemlerinin ve araçların çoğu [Web sitesi projelerine](https://msdn.microsoft.com/library/dd547590.aspx)uygulanmaz. Web sitesi projelerini dağıtma hakkında daha fazla bilgi için bkz. [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects).

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC projelerini dağıtma

Bu öğreticide, bir ASP.NET Web Forms projesi dağıtırsınız, ancak nasıl yapılacağını öğrendiği her şey ASP.NET MVC için de geçerlidir. Visual Studio MVC projesi yalnızca başka bir Web uygulaması projesi biçimidir. Tek fark, ASP.NET MVC 'yi veya hedef sürümünüzü desteklemeyen bir barındırma sağlayıcısına dağıtım yapıyorsanız, projenize uygun ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0) veya [MVC 4](http://nuget.org/packages/aspnetmvc)) NuGet paketini yüklediğinizden emin olmanız gerekir.

## <a name="programming-language"></a>Programlama dili

Örnek uygulama kullanır C# C#, ancak öğreticiler bilgi gerektirmez ve öğreticiler tarafından gösterilen dağıtım teknikleri dile özgü değildir.

## <a name="troubleshooting-during-this-tutorial"></a>Bu öğretici sırasında sorun giderme

Dağıtım sırasında bir hata oluştuğunda veya dağıtılan Site doğru şekilde çalıştırılmazsa, hata iletileri her zaman bir çözüm sağlamaz. Bazı yaygın sorun senaryolarında size yardımcı olmak için [sorun giderme başvurusu sayfası](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md) kullanılabilir. Bir hata iletisi alırsanız veya öğreticilerle karşılaştığınızdan bir şey çalışmadıysanız, sorun giderme sayfasını kontrol ettiğinizden emin olun.

## <a name="comments-welcome"></a>Yorumlara hoş geldiniz

Öğreticilerle ilgili açıklamalar hoş geldiniz ve öğretici, öğreticinin ne zaman güncelleştirildiği, öğretici açıklamalarında sunulan geliştirmeler için hesap düzeltmelerini veya önerilerini almak üzere her çaba sunulacaktır.

## <a name="prerequisites"></a>Önkoşullar

Başlamadan önce, Windows 7 veya sonraki bir sürüme sahip olduğunuzdan ve bilgisayarınızda aşağıdaki ürünlerden birinin yüklü olduğundan emin olun:

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [Web için Visual Studio 2012 RC veya Visual Studio Express 2012 RC](https://go.microsoft.com/fwlink/?LinkId=240162)

Visual Studio 2010 SP1 veya Visual Web Developer Express 2010 SP1 'e sahipseniz, aşağıdaki ürünleri de yükleyebilirsiniz:

- [.Net Için Azure SDK (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) (Web yayımlama güncelleştirmesini içerir)
- [SQL Server Compact 4,0 için Microsoft Visual Studio 2010 SP1 araçları](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

Öğreticiyi tamamlayabilmeniz için bazı başka yazılımlar gerekir, ancak henüz yüklü olması gerekmez. Öğretici, ihtiyacınız olduğunda yükleme adımlarında size kılavuzluk eder.

## <a name="downloading-the-sample-application"></a>Örnek uygulama indiriliyor

Dağıttığınız uygulama Contoso University olarak adlandırılır ve sizin için zaten oluşturulmuştur. Bu, [ASP.NET sitesindeki Entity Framework öğreticiler](https://asp.net/entity-framework/tutorials)bölümünde açıklanan Contoso University uygulamasına bağlı olarak, bir üniversite Web sitesinin basitleştirilmiş bir sürümüdür.

Önkoşulları yükledikten sonra [Contoso University Web uygulamasını](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)indirin. *. Zip* dosyası projenin birden çok sürümünü ve tüm 12 öğreticilerini IÇEREN bir PDF dosyasını içerir. Öğreticinin adımları aracılığıyla çalışmak için Contosoüniversitesi-BEGIN ile başlayın. Projenin öğreticilerin sonunda nasıl göründüğünü görmek için ContosoUniversity-End ' i açın. Projenin, öğretici 10 ' da tam SQL Server geçiş işleminden önce nasıl göründüğünü görmek için ContosoUniversity-AfterTutorial09 ' i açın.

Öğretici adımları aracılığıyla çalışmaya hazırlanmak için ContosoUniversity-Begin ' i Visual Studio projeleriyle çalışmak için kullandığınız klasöre kaydedin. Varsayılan olarak aşağıdaki klasördür:

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

(Bu öğreticideki ekran görüntüleri için, proje klasörü `C`: sürücü ' deki kök dizinde bulunur.)

Visual Studio 'yu başlatın, projeyi açın ve CTRL-F5 tuşlarına basarak çalıştırın.

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

Web sitesi sayfalarına menü çubuğundan erişilebilir ve aşağıdaki işlevleri gerçekleştirmenize izin verilir:

- Öğrenci istatistiklerini görüntüleyin (hakkında sayfası).
- Öğrencileri görüntüleyin, düzenleyin, silin ve ekleyin.
- Kursları görüntüleyin ve düzenleyin.
- Eğitmenleri görüntüleyin ve düzenleyin.
- Departmanları görüntüleyin ve düzenleyin.

Aşağıda, birkaç temsili sayfanın ekran görüntüleri verilmiştir.

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>Dağıtımı etkileyen uygulama özelliklerini gözden geçirme

Uygulamanın aşağıdaki özellikleri, nasıl dağıtabileceğinizi veya dağıtmak için ne yapmanız gerektiğini etkiler. Bunların her biri, serideki aşağıdaki öğreticilerde daha ayrıntılı olarak açıklanmıştır.

- Contoso University, öğrenci ve eğitmen adları gibi uygulama verilerini depolamak için bir SQL Server Compact veritabanı kullanır. Veritabanı, test verilerinin ve üretim verilerinin bir karışımını içerir ve üretime dağıttığınızda test verilerini dışlayamazsınız. Öğretici serisinde daha sonra SQL Server Compact SQL Server ' den geçiş yapabilirsiniz.
- Uygulama, Kullanıcı hesabı bilgilerini bir SQL Server Compact veritabanında depolayan ASP.NET üyelik sistemini kullanır. Uygulama, bazı kısıtlı bilgilere erişimi olan bir yönetici kullanıcıyı tanımlar. Üyelik veritabanını test hesapları olmadan, tek bir yönetici hesabıyla dağıtmanız gerekir.
- Uygulama veritabanı ve üyelik veritabanı veritabanı altyapısı olarak SQL Server Compact kullandığından, veritabanı altyapısını barındırma sağlayıcısına ve veritabanlarının kendilerine dağıtmanız gerekir.
- Uygulama, ASP.NET evrensel üyelik sağlayıcılarını kullanarak üyelik sisteminin verilerini bir SQL Server Compact veritabanında depolayabilmesini sağlayabilir. Evrensel üyelik sağlayıcılarını içeren derlemenin uygulamayla dağıtılması gerekir.
- Uygulama, uygulama veritabanındaki verilere erişmek için 5,0 Entity Framework kullanır. Entity Framework 5,0 içeren derlemenin uygulamayla dağıtılması gerekir.
- Uygulama, üçüncü taraf hata günlüğü ve raporlama yardımcı programını kullanır. Bu yardımcı program, uygulamayla birlikte dağıtılması gereken bir derlemede sunulmaktadır.
- Hata günlüğü yardımcı programı, XML dosyalarındaki hata bilgilerini bir dosya klasörüne yazar. ASP.NET tarafından dağıtılan sitede çalıştığı hesabın bu klasöre yazma iznine sahip olduğundan ve bu klasörü dağıtımdan dışlamak zorunda olduğunuzdan emin olmanız gerekir. (Aksi takdirde, test ortamındaki hata günlüğü verileri üretime dağıtılabilir ve/veya üretim hata günlüğü dosyaları silinebilir.)
- Uygulama, hedef ortama (test veya üretime) ve derleme yapılandırmasına (hata ayıklama veya sürüm) bağlı olarak değiştirilmesi gereken diğer ayarlara bağlı olarak, dağıtılan *Web. config* dosyasında değiştirilmesi gereken bazı ayarları içerir.
- Visual Studio çözümü bir sınıf kitaplığı projesi içerir. Yalnızca bu projenin oluşturduğu derleme, projenin kendisi değil dağıtılmalıdır.

Serideki bu ilk öğreticide, örnek Visual Studio projesini indirdiniz ve uygulamayı nasıl dağıtabileceğinizi etkileyen site özellikleri incelendi. Aşağıdaki öğreticilerde, bu öğelerin bazılarını otomatik olarak işlenecek şekilde ayarlayarak dağıtıma hazırlandınız. Başkalarının el ile ilgileni.

> [!div class="step-by-step"]
> [Next](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
