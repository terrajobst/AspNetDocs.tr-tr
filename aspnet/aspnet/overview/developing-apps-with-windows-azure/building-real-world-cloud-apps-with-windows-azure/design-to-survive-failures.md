---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
title: Hatalara yönelik tasarım (Azure ile gerçek hayatta bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 364ce84e-5af8-4e08-afc9-75a512b01f84
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
msc.type: authoredcontent
ms.openlocfilehash: 348232af531b5d53dc3cb46d6d2c7931d95a572d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617728"
---
# <a name="design-to-survive-failures-building-real-world-cloud-apps-with-azure"></a>Arızalara yönelik tasarım (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Herhangi bir tür uygulama oluştururken düşünmek zorunda olduğunuz işlemlerden biri, ancak özellikle de birçok kişinin kullanacağı bulutta çalışacak şekilde, uygulamayı sorunsuz bir şekilde işleyebilmesi ve değer sunmaya devam edebilmesi için uygulamayı tasarlayacaksınız. üç. Yeterli zaman verildiğinde, hiçbir ortamda veya herhangi bir yazılım sisteminde yanlış bir şey olacak. Uygulamanızın bu durumları nasıl işleyeceği, müşterilerinizin ne kadar zaman aldığını ve sorunları analiz etmek ve çözmek için ne kadar zaman harcamanız gerektiğini belirler.

## <a name="types-of-failures"></a>Başarısızlık türleri

Farklı şekilde işlemek istediğiniz iki temel başarısızlık kategorisi vardır:

- Geçici, sürekli ağ bağlantısı sorunları gibi kendi kendini onaran hataları.
- Müdahale gerektiren hatalarda

Geçici hatalara karşı, uygulamanın çoğu kez hızlı ve otomatik olarak kurtarımasından emin olmak için bir yeniden deneme ilkesi uygulayabilirsiniz. Müşterileriniz biraz daha uzun bir yanıt süresi fark edebilir, aksi takdirde etkilenmezler. [Geçici hata işleme](transient-fault-handling.md)bölümünde bu hataları işlemenin bazı yollarını göstereceğiz.

Başarısızlık sırasında, sorunlar oluştuğunda ve kök neden analizini kolaylaştırdığınızda size hemen bildirimde bulunan izleme ve günlüğe kaydetme işlevlerini uygulayabilirsiniz. [İzleme ve telemetri](monitoring-and-telemetry.md)bölümünde bu tür hataların üstünde kalmanıza yardımcı olacak bazı yollar göstereceğiz.

## <a name="failure-scope"></a>Hata kapsamı

Ayrıca, tek bir makinenin etkilenip etkilenmediğini, SQL veritabanı veya depolama gibi bir hizmetin tamamını veya tüm bölge olduğunu düşünmek zorunda olursunuz.

![Hata kapsamı](design-to-survive-failures/_static/image1.png)

### <a name="machine-failures"></a>Makine arızaları

Azure 'da, başarısız olan bir sunucu yeni bir sunucu tarafından otomatik olarak değiştirildi ve iyi tasarlanmış bir bulut uygulaması bu türden bir hatadan otomatik olarak ve hızla kurtarır. Daha önce durum bilgisiz bir web katmanının ölçeklenebilirlik avantajlarını inceleyeceğiz ve başarısız bir sunucudan kurtarma kolaylığı, bu durum nedeniyle oluşan başka bir avantajdır. Kurtarma kolaylığı Ayrıca, SQL veritabanı ve Azure App Service Web Apps gibi hizmet olarak platform (PaaS) özelliklerinin avantajlarından biridir. Donanım arızaları nadir olarak görülebilir, ancak bu hizmetler bu hizmetleri otomatik olarak işler. Bu hizmetlerden birini kullanırken makine başarısızlıklarını işlemek için de kod yazmanız gerekmez.

### <a name="service-failures"></a>Hizmet sorunları

Bulut uygulamaları genellikle birden çok hizmeti kullanır. Örneğin, BT uygulaması, SQL veritabanı hizmetini, depolama hizmetini ve Web uygulamasını Azure App Service dağıtım olarak kullanır. Bağlı olduğunuz hizmetlerden biri başarısız olursa uygulamanız ne olur? Bazı hizmet hatalarıyla ilgili bir "Üzgünüz, daha sonra yeniden deneyin" iletisi, yapabileceğiniz en iyi yöntem olabilir. Ancak birçok senaryoda daha iyi yapabilirsiniz. Örneğin, arka uç veri depetinin süresi kapalıysa Kullanıcı girişini kabul edebilir, "İsteğiniz alındı" olarak görüntüleyebilir ve bu girişi başka bir yerde saklayın. ardından, ihtiyacınız olan hizmet tekrar çalışır durumda olduğunda girişi alabilir ve işleyebilirsiniz.

[Kuyruk merkezli çalışma deseninin](queue-centric-work-pattern.md) bölümü, bu senaryoyu işlemenin bir yolunu gösterir. BT uygulaması, görevleri SQL veritabanı 'nda depolar, ancak SQL veritabanı kapatıldığında çalışmaktan çıkmak zorunda değildir. Bu bölümde, bir görevde bir görev için Kullanıcı girişini depolamayı ve bir çalışan işlemi kullanarak kuyruğu okuyup görevi güncelleştirmeyi öğreneceksiniz. SQL kapalıysa, BT görevlerini oluşturma özelliği etkilenmez; çalışan işlemi, SQL veritabanı kullanılabilir olduğunda yeni görevleri bekleyebilir ve işleyebilir.

### <a name="region-failures"></a>Bölge arızaları

Tüm bölgeler başarısız olabilir. Doğal bir olağanüstü durum bir veri merkezini yok edebilir, bir meteor tarafından düzleştirilir, veri merkezindeki santral hattı, cohoe ile birlikte bir kbıg, vb. gibi bir çiftçisi tarafından kesilebilir. Uygulamanız Stricken veri merkezinde barındırılıyorsa ne olur? Azure 'da uygulamanızı birden çok bölgede çalışacak şekilde ayarlamak mümkündür. bu sayede bir olağanüstü durum varsa başka bir bölgede çalışmaya devam edersiniz. Bu tür sorunlar son derece nadir oluşumlardır ve çoğu uygulama, bu sıralamanın arızalarıyla kesintisiz hizmet sağlamak için gerekli olan pota 'u atmıyor. Bir bölge hatası aracılığıyla uygulamanızın kullanılabilir tutulması hakkında bilgi edinmek için bölümün sonundaki kaynaklar bölümüne bakın.

Azure 'un hedefi, bu tür hataların tümünü çok daha kolay bir şekilde işlemeyi sağlamaktır ve bunu aşağıdaki bölümlerde nasıl yaptığımız hakkında bazı örnekler görürsünüz.

## <a name="slas"></a>SLA’lar

Kullanıcılar genellikle Bulut ortamındaki hizmet düzeyi sözleşmeleri (SLA 'Lar) hakkında bilgi duylar. Bunlar temel olarak, şirketlerinin hizmetin ne kadar güvenilir olduğunu öğrenmelerini sağlardır. % 99,9 SLA, hizmetin% 99,9 ' nin doğru şekilde çalışmasını beklemeniz gerektiğini gösterir. Bu, bir SLA için oldukça tipik bir değerdir ve çok yüksek bir sayı gibi bir süre boyunca dolar İşte, çeşitli SLA sayısını yılda bir yıla, aya ve haftaya kadar ne kadar kapalı kalma oranı gösteren bir tablo.

![SLA tablosu](design-to-survive-failures/_static/image2.png)

Bu nedenle,% 99,9 SLA, hizmetiniz bir ayda 8,76 saat veya 43,2 dakika sürebilir. Bu, çoğu kişinin fark etenden daha fazla zaman. Bu nedenle bir geliştirici olarak belirli bir aşağı doğru sürenin mümkün olduğunu ve düzgün bir şekilde işleneceğini bilmek istersiniz. Bazı bir noktada uygulamanızı kullanmaya devam eteceğiz ve bir hizmetin kapatılması ve müşterinin olumsuz etkisini en aza indirmek istiyorsunuz.

Bir SLA hakkında bilmeniz gereken tek şey, ne zaman çerçeve, her ay veya her yıl için mi sıfırlandığını belirtir? Azure 'da, yıllık bir SLA 'nın her ay sizin için daha iyi olan saat sayısını sıfırladığımızdan, yıllık bir SLA 'yı bir dizi iyi aydan ayırarak, bu yıl sizin için daha iyi bir şekilde sıfırlayacağız.

Tabii ki, SLA 'dan daha iyi hale getirebilmemiz için her zaman amaçlayın; genellikle bundan çok daha küçüktür. Taahhüdizin, en uzun süre için daha uzun süre boyunca faturalandırılıyoruz. Geri aldığınız para miktarı muhtemelen, daha fazla çalışma zamanının iş etkisi için sizi tamamen dengeleyemez, ancak SLA 'nın bu yönü bir zorlama ilkesi görevi görür ve çok önemli bir işlem yaptığımız olduğunu bilmenizi sağlar.

### <a name="composite-slas"></a>Bileşik SLA'lar

SLA 'Lara baktığınız zaman, her bir hizmetin ayrı bir SLA 'Sı bulunan bir uygulamada birden fazla hizmet kullanmanın etkileri olduğunu düşünmek için önemli bir şeydir. Örneğin, BT uygulamasının çözümü Azure App Service Web Apps, Azure depolama ve SQL veritabanı kullanır. Bu e-kitabın Aralık 2013 ' de yazıldığı tarih itibarıyla SLA numaraları aşağıda verilmiştir:

![SLA Web sitesi, depolama, SQL veritabanı](design-to-survive-failures/_static/image3.png)

Bu hizmet SLA 'larını temel alarak uygulama için beklediğiniz en uzun süre nedir? Bu durumda, aşağı doğru zamanın en kötü SLA yüzdesine veya% 99,9 ' e eşit olacağını düşünebilirsiniz. Bu, üç hizmetin her zaman aynı anda başarısız olması durumunda doğru olacaktır, ancak bu durum gerçekte ne olur? Her hizmet farklı zamanlarda bağımsız olarak başarısız olabilir, bu nedenle, bireysel SLA numaralarını çarparak bileşik SLA 'yı hesaplamanız gerekir.

![Bileşik SLA](design-to-survive-failures/_static/image4.png)

Bu nedenle, uygulamanız ayda yalnızca 43,2 dakika değil, bu durumda 3 kez, ayda bir, 108 dakika ve Azure SLA sınırları dahilinde olmaya devam edebilir.

Bu sorun Azure için benzersiz değildir. Gerçekte, kullanılabilir herhangi bir bulut hizmeti için en iyi bulut SLA 'larını sağlıyoruz ve satıcının bulut hizmetlerini kullanıyorsanız, bununla uğraşmak için benzer sorunlarla karşılaşırsınız. Bu önemli noktalar, uygulamalarınızı veya kullanıcılarınızı etkilemek için yeterince bir süre gerçekleşebileceğinden, kaçınılmaz hizmet başarısızlıklarını nasıl işlemek için uygulamanızı nasıl tasarlayabileceğinize ilişkin düşünceli bir öneme sahiptir.

### <a name="cloud-slas-compared-to-enterprise-down-time-experience"></a>Bulut SLA 'Ları, kurumsal bir süre deneyimiyle karşılaştırılır

Kişiler bazen "Kurumsal uygulamamda bu sorunlarla hiç neden olmadım." Gerçek zamanlı olarak ne kadar süre boyunca sorun yaşıyorsanız, genellikle "Iyi" bir şey olur. Ne kadar sıklıkla karşılaşırsanız, "Bu," Bazen yeni bir sunucu yedeklememiz veya yüklemeniz ya da yazılım güncelleştirmeniz gerekir. " Kuşkusuz, bu süre aşağı doğru sayılır. Çoğu kurumsal uygulama, özellikle de görev açısından kritik olmadıkça, hizmet SLA 'larımız tarafından izin verilen süreden daha fazla süre için geçerlidir. Ancak, sunucunuz ve altyapınız olduğunda ve bunu sizin sorumluluğunuzda ve kontrol ederken, daha az bir şekilde aşağı doğru bir şekilde sunmaktan çekinmeyin. Bir bulut ortamında başka birine bağlı olursunuz ve ne olduğunu bilmiyorsanız bu konuda daha fazla endişeli olabilirsiniz.

Bir kuruluş, bir bulut SLA 'sından aldığınız zamandan daha büyük bir süre elde edildiğinde, bu, donanıma çok daha fazla ücret harcaarak bunu yapabilirler. Bulut hizmeti bunu yapacağından, Hizmetleri için çok daha fazla ücret ödemeniz gerekebilir. Bunun yerine, uygun maliyetli bir hizmettir ve yazılımınızı tasarlayabilmeniz gerekir ve bu sayede yazılım, kaçınılmaz hataların en düşük kesintilere karşı sürmesine neden olur. Cloud App Designer olarak işiniz, felaketler önlemek için hata oluşmasını önlemek ve donanım üzerinde değil, yazılıma odaklanarak bunu yapmanız çok önemlidir. Kurumsal uygulamalar, hatalara göre ortalama süresi en üst düzeye çıkarmak için, bulut uygulamaları kurtarma süresini en aza indirir.

### <a name="not-all-cloud-services-have-slas"></a>Tüm bulut hizmetlerinde SLA 'Lar yok

Her bulut hizmetinin de SLA 'sı olmadığı farkında olun. Uygulamanız, zaman garantisi olmayan bir hizmete bağımlıysa, Imagine olabileceğiniz kadar uzun bir süre daha fazla olabilir. Örneğin, sitenizde Facebook veya Twitter gibi bir sosyal sağlayıcı kullanarak oturum açma özelliğini etkinleştirirseniz, bir SLA olup olmadığını öğrenmek için hizmet sağlayıcısına danışın ve bir tane olmadığını fark edebilirsiniz. Ancak, kimlik doğrulama hizmeti kapalı olursa veya sizin oluşturduğunuz istek hacminin desteklenemez, müşterileriniz uygulamanızı kapatır. Günler veya daha uzun bir süre için kapatılabilir. Yeni bir uygulamanın oluşturucuları yüzlerce milyonlarca indirme bekliyordu ve Facebook kimlik doğrulaması üzerinde bir bağımlılık aldı, ancak bu hizmet için SLA yoktu ve keşfedilmeden önce Facebook ile iletişim kurmadı.

### <a name="not-all-downtime-counts-toward-slas"></a>Tüm kapalı kalma süresi SLA 'Lara doğru sayılır

Bazı bulut Hizmetleri, uygulamanız tarafından kullanılıyorsa hizmeti kasıtlı olarak reddedebilir. Bu, *daraltma*olarak adlandırılır. Bir hizmetin SLA 'sı varsa, bu koşulları kısıtlayabilecek koşulları sağlamalıdır ve uygulama tasarımınızın bu koşullara uymaması ve olması durumunda, azaltmaya uygun şekilde yanıt verebilmesi gerekir. Örneğin, bir hizmetin istekleri saniye başına belirli bir sayıyı aşarsanız başarısız olmaya başladıklarında, ortadan kaldırma işleminin devam etmesine neden olacak kadar hızlı otomatik yeniden deneme olmadığından emin olmak istersiniz. [Geçici hata işleme](transient-fault-handling.md)bölümünde daraltma hakkında söylediğimiz daha fazla bilgi edineceksiniz.

## <a name="summary"></a>Özet

Bu bölümde, gerçek bir dünya bulutu uygulamasının, hatalardan sorunsuz bir şekilde devam etmek için nasıl tasarlanacağını fark etmenize yardımcı olmaya çalışıldı. [Sonraki bölümde](monitoring-and-telemetry.md), bu serideki kalan desenler, bunu yapmak için kullanabileceğiniz bazı stratejiler hakkında daha fazla ayrıntıya gider:

- Doğru [izleme ve telemetri](monitoring-and-telemetry.md)sayesinde, müdahale gerektiren hatalardan hızlı bir şekilde ulaşın ve bunları çözmek için yeterli bilgiye sahip olursunuz.
- Akıllı yeniden deneme mantığını uygulayarak [geçici hataları işleyin](transient-fault-handling.md) , böylece uygulamanızın otomatik olarak geri dönmesi mümkün olduğunda [devre kesici](transient-fault-handling.md#circuitbreakers) mantığa geri dönebilir.
- Veritabanı erişimiyle işleme, gecikme süresi ve bağlantı sorunlarını en aza indirmek için [dağıtılmış önbelleğe alma](distributed-caching.md) özelliğini kullanın.
- [Sıra merkezli iş düzeniyle](queue-centric-work-pattern.md)gevşek bir şekilde, arka uç kapatıldığında uygulamanızın ön ucu çalışmaya devam edebilmeleri için

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için bu e-kitap ve aşağıdaki kaynakların ilerleyen bölümlerinde bölümüne bakın.

Belgelerle

- [Failsafe: dayanıklı bulut mimarilerine yönelik rehberlik](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Marc Mercuri, Ulrich Homann ve Andrew Townhill tarafından Teknik İnceleme. FailSafe video serisinin Web sayfası sürümü.
- [Azure Cloud Services 'de büyük ölçekli hizmetler tasarlamak Için En Iyi uygulamalar](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Simms ve Michael Thomassy ' i Işaretleyen Teknik İnceleme.
- [Azure Iş sürekliliği teknik kılavuzu](https://msdn.microsoft.com/library/windowsazure/hh873027.aspx). Patrick ve Jason Roth tarafından hazırlanan Teknik İnceleme.
- [Azure uygulamaları Için olağanüstü durum kurtarma ve yüksek kullanılabilirlik](https://msdn.microsoft.com/library/windowsazure/dn251004.aspx). Michael Mckesize, Hanu Kommalapati ve Jason Roth tarafından Teknik İnceleme.
- [Microsoft desenleri ve uygulamaları-Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). Bkz. çok veri merkezi dağıtım kılavuzu, devre kesici stili.
- [Azure desteği-hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).
- [Azure SQL veritabanı 'Nda Iş sürekliliği](https://msdn.microsoft.com/library/windowsazure/hh852669.aspx). SQL veritabanı yüksek kullanılabilirlik ve olağanüstü durum kurtarma özellikleri hakkındaki belgeler.
- [Azure sanal makinelerinde SQL Server Için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx).

Videolar:

- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz bölümden oluşan seriler. , Microsoft Müşteri danışmanlık ekibi (CAT) deneyiminden gerçek müşterilerle çekilen hikayelerle, yüksek düzeyde kavramlar ve mimari ilkeleri çok erişilebilir ve ilginç bir şekilde sunar. 1\. ve 8. bölüm, bulut uygulamaları tasarlama nedenlerinden kaynaklanan hatalara karşı ayrıntılı bir şekilde devam ediyor. Ayrıca, Bölüm 2 ' de 49:57 ' de başlayan, Bölüm 2 ' de hata noktaları ve hata modları hakkındaki inceleme tartışmasına ve 56:05 ' den başlayarak Bölüm 40:55 3 ' teki devre ayırıcılarının tartışmalarına bakın.
- [Büyük oluşturma: Azure müşterileri-Bölüm II 'den öğrenilen dersler](https://channel9.msdn.com/Events/Build/2012/3-030). Simms 'nin hata tasarlama ve her şeyi işaretleme hakkında işaret edin. Failsafe serisine benzer ancak daha fazla nasıl yapılır ayrıntılarına gider.

> [!div class="step-by-step"]
> [Önceki](unstructured-blob-storage.md)
> [İleri](monitoring-and-telemetry.md)
