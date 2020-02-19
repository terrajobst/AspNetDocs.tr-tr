---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: Azure ile gerçek dünyada bulut uygulamaları oluşturma | Microsoft Docs
author: MikeWasson
description: Bu e-kitap, gerçek hayatta bulut çözümleri oluşturmaya yönelik desenler tabanlı bir yaklaşımda size yol gösterir. Desenler, geliştirme işlemine ve bir... için de geçerlidir.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: b88573b3702b755b155e8da35f5f8a67931bafc6
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457121"
---
# <a name="building-real-world-cloud-apps-with-azure"></a>Azure ile gerçek dünyada bulut uygulamaları oluşturma

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Bu e-kitap, gerçek hayatta bulut çözümleri oluşturmaya yönelik desenler tabanlı bir yaklaşımda size yol gösterir. Desenler, geliştirme süreci ve mimari ve kodlama uygulamalarına de uygulanır.
> 
> İçerik Scott Guthrie tarafından geliştirilen ve 2013 Haziran 'da (bölüm[1](http://vimeo.com/68215538), [Bölüm 2](http://vimeo.com/68215602)) ve Microsoft Tech Ed 2013 Avustralya 'da ([Bölüm 1,](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)bölüm [2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)), BT 'nin sunduğu bir sunuyu temel alır. [Diğer pek çok kişi](more-patterns-and-guidance.md#acknowledgments) , video 'dan yazılı biçime geçiş yaparken içeriği güncelleştirmiş ve genişletmektedir.

## <a name="intended-audience"></a>Hedef Kitle

Buluta yönelik bir geçiş yapmayı düşündüğünde veya bulut geliştirmeye yönelik yeni bir yazılım geliştirme hakkında daha fazla bilgi edinmek isteyen geliştiriciler burada, bilmeleri gereken en önemli kavramlar ve uygulamalar hakkında kısa bir genel bakış bulacaksınız. Kavramlar somut örneklerle gösterilmektedir ve her bölüm daha ayrıntılı bilgi için diğer kaynaklarla bağlantı sağlar. Örnekler ve ek kaynaklara bağlantılar Microsoft çerçeveleri ve hizmetleri içindir, ancak gösterilen ilkeler diğer web geliştirme çerçeveleri ve bulut ortamları için de geçerlidir.

Bulut için zaten geliştirmekte olan geliştiriciler burada daha başarılı hale getirmenize yardımcı olacak fikirler bulabilir. Serideki her bölüm bağımsız olarak okunabilir, böylece ilgilendiğiniz konuları seçip seçebilirsiniz.

Scott Guthrie 'yi izleyen herkes, *Azure Presentation Ile gerçek dünyada bulut uygulamaları oluşturuyor* ve daha fazla ayrıntı ve güncelleştirilmiş bilgi ister. bu bilgileri burada bulabilirsiniz.

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a>Bulut geliştirme desenleri

Bu e-kitap, bulut geliştirmesi için on dört önerilen deseni açıklamaktadır. "Model" burada, bir şeyler yapmak için önerilen bir yol olması açısından çok daha fazla şekilde kullanılır: bulut uygulamaları geliştirme, tasarlama ve kodlama hakkında ne kadar en iyi duruma gelir. Bunlar, bu adımları izlerseniz "başarı" başarılı olma "konusunda size yardımcı olacak önemli desenlerdir.

- [Her şeyi otomatikleştirin](automate-everything.md).

    - Yinelenen işlemlerde verimliliği en üst düzeye çıkarmak ve hataları en aza indirmek için betikleri kullanın.
    - Demo: Azure Yönetim betikleri.
- [Kaynak denetimi](source-control.md). 

    - DevOps iş akışını kolaylaştırmak için kaynak denetiminde dallanma yapısı ayarlayın.
    - Demo: kaynak denetimine komut dosyaları ekleyin.
    - Demo: hassas verileri kaynak denetiminden koruyun.
    - Demo: Visual Studio 'da git kullanın.
- [Sürekli tümleştirme ve teslim](continuous-integration-and-continuous-delivery.md). 

    - Her kaynak denetimi iadede derleme ve dağıtımı otomatikleştirin.
- [Web geliştirme en iyi uygulamaları](web-development-best-practices.md). 

    - Web katmanını durum bilgisiz olarak tut.
    - Demo: Azure App Service Web Apps ölçeklendirme ve otomatik ölçekleme.
    - Oturum durumunu önleyin.
    - CDN kullanılamaz olduğunda geri dönüş ile CDN kullanın.
    - Zaman uyumsuz programlama modeli kullanın.
    - Demo: ASP.NET MVC ve Entity Framework içinde zaman uyumsuz.
- [Çoklu oturum açma](single-sign-on.md). 

    - Azure Active Directory giriş.
    - Demo: Azure Active Directory kullanan bir ASP.NET uygulaması oluşturun.
- [Veri depolama seçenekleri](data-storage-options.md). 

    - Veri deposu türleri.
    - Doğru veri deposunu seçme.
    - Demo: Azure SQL veritabanı.
- [Veri bölümleme stratejileri](data-partitioning-strategies.md). 

    - İlişkisel bir veritabanının ölçeklendirilmesini kolaylaştırmak için verileri dikey, yatay veya her ikisine birden bölümleyin.
- [Yapılandırılmamış BLOB depolama alanı](unstructured-blob-storage.md). 

    - Blob hizmetini kullanarak dosyaları bulutta depolayın.
    - Demo: blob depolamayı, çözüm uygulamasında kullanma.
- [Hatalara devam etmek Için tasarım](design-to-survive-failures.md). 

    - Başarısızlık türleri.
    - Hata kapsamı.
    - SLA 'Ları anlama.
- [İzleme ve telemetri](monitoring-and-telemetry.md). 

    - Neden bir telemetri uygulaması satın almanız ve uygulamanızı işaretlemek için kendi kodunuzu yazmanız gerekir.
    - Demo: Azure için yeni relik
    - Demo: BT BT uygulamasındaki kodu günlüğe kaydetme.
    - Demo: BT BT uygulamasına bağımlılık ekleme.
    - Demo: Azure 'da yerleşik günlük desteği.
- [Geçici hata işleme](transient-fault-handling.md). 

    - Geçici hataların etkisini azaltmak için akıllı yeniden deneme/geri kapatma mantığını kullanın.
    - Demo: Entity Framework 6 ' da yeniden deneyin/geri dönün.
- [Dağıtılmış önbelleğe alma](distributed-caching.md). 

    - Dağıtılmış önbelleğe alma özelliğini kullanarak ölçeklenebilirliği geliştirme ve veritabanı işlem maliyetlerini azaltma.
- [Kuyruk merkezli çalışma stili](queue-centric-work-pattern.md). 

    - Web ve çalışan katmanlarını gevyana geçirerek yüksek kullanılabilirliği etkinleştirin ve ölçeklenebilirliği geliştirebilirsiniz.
    - Demo: BT BT uygulamasındaki Azure depolama kuyrukları.
- [Daha fazla bulut uygulaması deseni ve Kılavuzu](more-patterns-and-guidance.md).
- [Ek: Düzelt Örnek Uygulaması](the-fix-it-sample-application.md)

    - Bilinen Sorunlar
    - En İyi Uygulamalar
    - İndirme, oluşturma, çalıştırma ve dağıtma.

Bu desenler tüm bulut ortamları için geçerlidir, ancak Visual Studio, Team Foundation Service, ASP.NET ve Azure gibi Microsoft teknolojileri ve hizmetlerini temel alan örnekleri kullanarak bunları göstereceğiz.

Bu bölümün geri kalanında, BT örnek uygulamasını ve çözüm uygulamasının üzerinde çalıştığı Azure App Service Bulut ortamındaki Web Apps.

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a>Bu örnek uygulamayı düzeltir

Bu e-kitapta gösterilen ekran görüntüleri ve kod örneklerinin çoğu, son olarak [Scott Guthrie](https://weblogs.asp.net/scottgu/) tarafından geliştirilen ve önerilen bulut uygulaması geliştirme düzenlerini ve uygulamalarını göstermek için bu uygulamayı temel alır.

![BT uygulaması giriş sayfasını düzeltir](introduction/_static/image1.png)

Örnek uygulama, basit bir iş öğesi bilet sistemidir. Düzeltilmesi gerektiğinde, bir bilet oluşturur ve bu kişiye atar ve diğer kullanıcılar oturum açıp bu dosyalara atanan biletleri görebilir ve bilet, iş tamamlandığında tamamlandı olarak işaretleyebilir.

Bu, standart bir Visual Studio Web projem. Bu, ASP.NET MVC üzerine kurulmuştur ve bir SQL Server veritabanı kullanır. IIS Express yerel olarak çalışabilir ve bulutta çalıştırmak için bir Azure Web sitesine dağıtılabilir. Forms kimlik doğrulaması ve yerel bir veritabanı kullanarak ya da Google gibi bir sosyal sağlayıcı kullanarak oturum açabilirsiniz. (Daha sonra, Active Directory bir kurumsal hesapla oturum açma da göstereceğiz.)

![Oturum açma sayfası](introduction/_static/image2.png)

Oturum açtıktan sonra bir bilet oluşturabilir, bunu bir kişiye atayabilir ve daha sonra düzeltilmesi için bir resim yükleyebilirsiniz.

![Bir düzelme görevi oluşturun](introduction/_static/image3.png)

![Oluşturulan BT görevini düzeltir](introduction/_static/image4.png)

Oluşturduğunuz iş öğelerinin ilerlemesini izleyebilir, size atanan biletleri görebilir, Bilet ayrıntılarını görüntüleyebilir ve öğeleri tamamlandı olarak işaretleyebilirsiniz.

Bu özellik perspektifinden çok basit bir uygulamadır, ancak milyonlarca kullanıcıya ölçeklenebilmesi ve veritabanı hatalarından ve bağlantı sonlandırışları gibi şeylere dayanıklı olacak şekilde nasıl derleyeceksiniz. Ayrıca, geliştirme döngüsünü verimli ve hızlı bir şekilde tekrarlayarak, basit ve çevik bir geliştirme iş akışı oluşturmayı da öğreneceksiniz.

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a>Azure App Service Web Apps

BT BT uygulaması için kullanılan bulut ortamı, Web sitelerini çağırdığımız bir Azure hizmetidir. Bu hizmet, Azure 'da sanal makine oluşturmak ve bunların güncelleştirilmesini, IIS 'yi yüklemek ve yapılandırmak zorunda kalmadan kendi web uygulamanızı barındırabilmeniz için bir yoldur. Sitenizi sanal makinelerimizde barındırıyoruz ve sizin için otomatik olarak yedekleme ve kurtarma ve diğer hizmetleri sağlıyoruz. Web siteleri hizmeti ASP.NET, Node. js, PHP ve Python ile birlikte kullanılabilir. Visual Studio, Web Dağıtımı, FTP, git veya TFS kullanarak çok hızlı bir dağıtım yapmanızı sağlar. Genellikle bir dağıtımı başlattığınız zaman ve güncelleştirmeniz Internet üzerinden kullanılabilir olduğu zaman arasında birkaç saniye sürer. Kullanmaya başlamak her şey ücretsizdir ve trafiğiniz büyüdükçe ölçeği büyüleyebilirsiniz.

Arka planda Azure App Service Web Apps, kendi sanal makinelerinizdeki IIS kullanarak bir Web sitesi barındırıdıysanız kendiniz oluşturmanız gereken birçok mimari bileşeni ve özelliği sunar. Bir bileşen, IIS 'yi otomatik olarak yapılandıran ve uygulamanızı üzerinde çalıştırmak istediğiniz sayıda VM 'ye yükleyen bir dağıtım uç noktasıdır.

![Dağıtım hizmeti](introduction/_static/image5.png)

Bir Kullanıcı Web sitesini ziyaret ettiğinizde, bunlar IIS VM 'lerine doğrudan dönmez ve [uygulama Isteği yönlendirme (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) yük dengeleyicileri ' ne gider. Bunları kendi sunucularınız ile kullanabilirsiniz, ancak buradaki avantaj sizin için otomatik olarak ayarlanabiliyoruz. Oturum benzeşimi, IIS 'de sıra derinliği ve Web sitenizi barındıran VM 'lere trafik yönlendirmek için her bir makinedeki CPU kullanımı gibi hesap faktörlerine sahip akıllı bir buluşsal yöntem kullanır.

![ARR yük dengeleyici](introduction/_static/image6.png)

Bir makine kapalı olursa, Azure otomatik olarak rotasyondan alır, yeni bir sanal makine örneği getirir ve yeni örneğe trafiği yönlendirmeye başlar; tümü uygulamanız için bir süre boyunca devam eder.

![Makine hatasından otomatik kurtarma](introduction/_static/image7.png)

Tüm bu otomatik olarak gerçekleşir. Yapmanız gereken tek şey, Windows PowerShell, Visual Studio veya Azure yönetim portalı 'nı kullanarak bir Web sitesi oluşturur ve uygulamanızı buna dağıtır.

Visual Studio 'da bir Web uygulaması oluşturmayı ve bunu bir Azure Web sitesine dağıtmayı gösteren hızlı ve kolay bir adım adım öğretici için bkz. [Azure ve ASP.NET kullanmaya başlama](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).

<a id="summary"></a>
## <a name="summary"></a>Özet

Bu giriş, kitabın kapsayacağı konuların bir listesini, örnek uygulamanın ekran görüntülerini ve Azure App Service Bulut ortamındaki Web Apps kısa bir genel bakışı sağlamıştır. Bulutta uygulama geliştirmenin en iyi avantajlarından biri de bir test ortamı oluşturma ve kodunuzu buna dağıtma gibi yinelenen geliştirme görevlerini otomatikleştirmenin kolay bir yoludur. Bu, bir [sonraki bölümün](automate-everything.md)konusudur.

## <a name="resources"></a>Kaynaklar

Bu bölümde ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın.

Belgelerle

- [Azure App Service Web Apps](https://azure.microsoft.com/services/app-service/web/). Web Apps hakkındaki Azure belgeleri için Portal sayfası.
- [Web Apps, Cloud Services ve VM 'Ler: ne zaman kullanılır?](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) Bu bölümde gösterildiği gibi waw, Azure 'da Web Apps çalıştırmak için kullanabileceğiniz üç yönden biridir. Bu makalede üç yol arasındaki farklar açıklanmakta ve senaryonuz için hangisinin doğru olduğunu seçme konusunda rehberlik sunulmaktadır. Web siteleri gibi Cloud Services Azure 'un PaaS özelliğidir. VM 'Ler bir IaaS özelliğidir. PaaS ve IaaS hakkında bir açıklama için bkz. [veri seçenekleri](data-storage-options.md#paasiaas) bölümü.

Videolar:

- [Scott Guthrie, 0. adımda başlıyor-Azure Bulut İşletim Sistemi nedir?](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- [Web siteleri mimarisi-Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).
- [NIR Mashkowski Ile Azure Web siteleri Iç işlevleri](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).

> [!div class="step-by-step"]
> [Next](automate-everything.md)
