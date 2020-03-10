---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: Geçici hata Işleme (Azure ile gerçek hayatta bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 11/03/2015
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: e798cb83cfb97db63fef6dc38c8f62804461d01b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617329"
---
# <a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>Geçici hata Işleme (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Gerçek bir dünya bulutu uygulaması tasarlarken, düşünmek zorunda olduğunuz işlemlerden biri geçici hizmet kesintilerini nasıl ele alınacağını aşağıda bulabilirsiniz. Bu sorun, ağ bağlantılarına ve dış hizmetlere bağlı olduğunuzdan bulut uygulamalarında benzersiz bir öneme sahiptir. Genellikle kendi kendini onaran çok az göz alabilir ve bunları akıllıca işlemek üzere hazırlanmamışsa müşterileriniz için kötü bir deneyim elde edersiniz.

## <a name="causes-of-transient-failures"></a>Geçici hataların nedenleri

Bulut ortamında, başarısız olan ve bırakılan veritabanı bağlantılarının düzenli olarak gerçekleşmekte olduğunu fark edeceksiniz. Bu kısmen, Web sunucunuzun ve veritabanı sunucunuzun doğrudan fiziksel bağlantısı olduğu şirket içi ortamla karşılaştırıldığında daha fazla yük dengeleyicileri olduğu için önemlidir. Ayrıca, bazen çok kiracılı bir hizmete bağımlı olduğunuzda, hizmeti kullanan başka bir kişi bu hizmete yoğun bir şekilde ulaşıyorsa hizmete yapılan çağrıların daha yavaş veya zaman aşımına uğrar olduğunu görürsünüz. Diğer durumlarda, hizmeti çok sık vurmaya yönelik kullanıcı da olabilir ve hizmet, hizmetin diğer kiracılarını olumsuz etkilemesini engellemek için bağlantıyı (bağlantıları reddeder) kasıtlı olarak kısıtlar.

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>Geçici hataların etkisini azaltmak için akıllı yeniden deneme/geri kapatma mantığını kullanın

Bir özel durum oluşturmak ve müşterinize mevcut olmayan ya da hata sayfasını görüntülemek yerine, genellikle geçici olan hataları algılayabilir ve hata ile sonuçlanan işlemi, uzun süre başarılı olacak şekilde otomatik olarak yeniden deneyebilirsiniz. İşlemin çoğu ikinci TRY üzerinde başarılı olur ve bir sorun olduğunu fark eden müşteri olmadan hatayı kurtarmanız gerekir.

Akıllı yeniden deneme mantığı uygulayabileceğiniz çeşitli yollar vardır.

- Microsoft Patterns &amp; uygulamalar grubu, SQL veritabanı erişimi için ADO.NET kullanıyorsanız (Entity Framework değil) her şeyi yapan [geçici bir hata Işleme uygulaması bloğuna](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx) sahiptir. Yeniden denemeler için bir ilke ayarlarsınız; bir sorgu veya komutu yeniden denemek için kaç kez ve denemeler arasında ne kadar süre bekleneceğini ve SQL kodunuzu bir *using* bloğunda sarın.

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    TFH Ayrıca [Azure rol içi önbellek](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx) ve [Service Bus](https://azure.microsoft.com/services/service-bus/)destekler.
- Entity Framework kullandığınızda, genellikle doğrudan SQL bağlantılarıyla çalışmadığınızda, bu desenler ve uygulamalar paketini kullanamazsınız, ancak Entity Framework 6 Bu tür bir yeniden deneme mantığını çerçeveye doğru bir şekilde oluşturur. Aynı şekilde, yeniden deneme stratejisini belirttikten sonra EF, veritabanına her eriştiğinde bu stratejiyi kullanır.

    Bu özelliği, BT BT uygulamasında kullanmak için, *DBConfiguration* 'dan türeyen ve yeniden deneme mantığını açmak zorunda olduğumuz bir sınıf eklemektir.

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    Framework 'ün genellikle geçici hatalar olarak tanımladığı SQL veritabanı özel durumları için gösterilen kod, yeniden denemeler arasında bir üstel geri dönme gecikmesi ve 5 saniyelik en fazla gecikme ile işlemi yeniden denemek için EF 'i bildirir. Üstel geri dönüş, her başarısız yeniden denendikten sonra yeniden denemeden önce daha uzun bir süre bekleyebileceği anlamına gelir. Bir satırdaki üç denemeye başarısız olursa, bir özel durum oluşturur. Devre kesicileri hakkında aşağıdaki bölümde üstel geri ve sınırlı sayıda yeniden deneme olmasını istediğinizi açıklanmaktadır.

    BT uygulaması blob 'Lar için yaptığı ve .NET Storage istemci API 'sinin aynı tür mantığı zaten uyguladığı için Azure Storage hizmetini kullanırken benzer sorunlarla karşılaşmış olabilirsiniz. Yeniden deneme ilkesini belirtmeniz yeterlidir veya varsayılan ayarlarla memnunsanız bile bunu yapmanız gerekmez.

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>Devre kesiciler

Çok uzun bir süre boyunca çok fazla kez yeniden denemek istemediğiniz birkaç neden vardır:

- Başarısız istekleri kalıcı olarak yeniden denemeye çok fazla Kullanıcı diğer kullanıcıların deneyimini düşürebilir. Milyonlarca kişinin hepsi yinelenen yeniden deneme istekleri hazırsa, IIS dağıtım kuyruklarını ve uygulamanızın başka bir şekilde işleyebildiği isteklere hizmet etmesini önlüyordur.
- Bir hizmet hatası nedeniyle herkes yeniden deneniyorsa, bu nedenle hizmetin kurtarmaya başladığında taşarak birçok istek sıraya alınır.
- Hatanın azaltma nedeni varsa ve hizmetin azaltma için kullandığı bir zaman penceresi varsa, devam eden yeniden denemeler söz konusu pencereyi taşıyabilir ve azaltmaya devam eder.
- Bir Web sayfasının işlemesini bekleyen bir kullanıcı olabilir. İnsanların çok uzun sürmesini sağlamak, daha sonra tekrar denemek için bunları daha hızlı bir şekilde gerçekleştirmek için daha sinir bozucu olabilir.

Üstel geri dönüş, bir hizmetin uygulamanızdan aldığı yeniden deneme sıklığını sınırlayarak bu sorundan bazılarını ele alır. Ayrıca, *devre kesicilerin*de olması gerekir: Bu, uygulamanızın yeniden denemeyi durdurduğu ve aşağıdakilerden biri gibi başka bir işlem yapması gerektiği anlamına gelir:

- Özel geri dönüş. Yeniden evden bir stok fiyatı alamazsanız, Bloomberg adresinden edinebilirsiniz ya da veritabanından veri alamazsanız önbellekten alabilirsiniz.
- Sessiz başarısız oldu. Bir hizmetten ihtiyacınız olan şey uygulamanız için hepsi veya-herhangi bir şey değilse, verileri alırken null değeri döndürün. Bir çözüm BT görevi görüntülüyorsanız ve BLOB hizmeti yanıt vermiyorsa, görev ayrıntılarını görüntü olmadan görüntüleyebilirsiniz.
- Hızlı bir şekilde başarısız oldu. Diğer kullanıcılar için hizmet kesintilerine neden olabilecek veya bir daraltma penceresini genişletecek yeniden deneme istekleri ile hizmetin taşmasını önlemek için Kullanıcı hatası. Kolay bir "daha sonra yeniden dene" iletisi görüntüleyebilirsiniz.

Tek boyutuna uyan, tüm yeniden deneme ilkesi yoktur. Zaman uyumsuz bir arka plan çalışan işleminde, kullanıcının yanıt beklediği zaman uyumlu bir Web uygulamasında olduğundan daha uzun süre bekleyebilirsiniz. Bir ilişkisel veritabanı hizmeti için, önbellek hizmeti için yaptığınız denemeler arasında daha uzun süre bekleyebilirsiniz. İşte sayıların nasıl farklılık gösterebileceğini gösteren bir fikir vermek için önerilen bazı örnek yeniden deneme ilkeleri aşağıda verilmiştir. ("Hızlı Ilk", ilk yeniden denemeden önce gecikme olmaz.

![Örnek yeniden deneme ilkeleri](transient-fault-handling/_static/image1.png)

SQL veritabanı yeniden deneme ilkesi Kılavuzu için bkz. [SQL veritabanında geçici hata ve bağlantı hatalarını giderme](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/).

## <a name="summary"></a>Özet

Yeniden deneme/kapatma stratejisi, geçici hataların çoğu zaman müşteriye görünmez hale getirmenize yardımcı olabilir ve Microsoft, ADO.NET, Entity Framework veya Azure depolama hizmetini kullanıp kullanmayacağınızı denemenize olanak tanıyan işlerinizi en aza indirmek için kullanabileceğiniz çerçeveler sağlar.

Bir [sonraki bölümde](distributed-caching.md), dağıtılmış önbelleğe alma 'yı kullanarak performansı ve güvenilirliği nasıl iyileştirebileceğimizi inceleyeceğiz.

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için aşağıdaki kaynaklara bakın:

Belgeler

- [Azure Cloud Services 'de büyük ölçekli hizmetler tasarlamak Için En Iyi uygulamalar](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Simms ve Michael Thomassy ' i Işaretleyen Teknik İnceleme. Failsafe serisine benzer ancak daha fazla nasıl yapılır ayrıntılarına gider. Telemetri ve Tanılamalar bölümüne bakın.
- [Failsafe: dayanıklı bulut mimarilerine yönelik rehberlik](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Marc Mercuri, Ulrich Homann ve Andrew Townhill tarafından Teknik İnceleme. FailSafe video serisinin Web sayfası sürümü.
- [Microsoft desenleri ve uygulamaları-Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). Bkz. yeniden deneme stili, Zamanlayıcı Aracısı gözetmen stili.
- [Azure SQL veritabanı 'Nda hata toleransı](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx). Web günlüğü gönderisi,
- [Entity Framework-bağlantı dayanıklılığı/yeniden deneme mantığı](https://msdn.microsoft.com/data/dn456835). Entity Framework 6 ' nın geçici hata işleme özelliğini kullanma ve özelleştirme.
- [Bir ASP.NET MVC uygulamasındaki Entity Framework Ile bağlantı dayanıklılığı ve komut yakalaşmayı](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). Dört bölümden oluşan bir öğretici serisinin dördüncü bölümünde, SQL veritabanı için EF 6 Connection esnekliği özelliğinin nasıl ayarlanacağı gösterilmektedir.

Videolar

- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz bölümden oluşan seriler. , Microsoft Müşteri danışmanlık ekibi (CAT) deneyiminden gerçek müşterilerle çekilen hikayelerle, yüksek düzeyde kavramlar ve mimari ilkeleri çok erişilebilir ve ilginç bir şekilde sunar. Bölüm 3 ' teki devre kesicilerin tartışmalarına 40:55 adresinden itibaren bakın.
- [Büyük oluşturma: Azure müşterileri-Bölüm II 'den öğrenilen dersler](https://channel9.msdn.com/Events/Build/2012/3-030). Simms 'nin hata, geçici hata işleme ve her şeyi işaretleme için tasarlama hakkında işaret edin.

Kod örneği

- [Azure 'Da bulut hizmeti temelleri](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). [Şirket kitaplığı geçici hata Işleme bloğunun](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/) (TFH) nasıl kullanılacağını gösteren Microsoft Azure müşteri danışmanlık ekibi tarafından oluşturulan örnek uygulama. Daha fazla bilgi için bkz. [Bulut Hizmeti Temelleri Veri Erişim Katmanı – Geçici Hata İşleme](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx). TFH, doğrudan ADO.NET kullanılarak veritabanı erişimi için önerilir (Entity Framework kullanmadan).

> [!div class="step-by-step"]
> [Önceki](monitoring-and-telemetry.md)
> [İleri](distributed-caching.md)
