---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: Dağıtılmış önbelleğe alma (Azure ile gerçek hayatta bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: c66187b990a828c53bd2f8115e3c9660fc6022ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582805"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>Dağıtılmış önbelleğe alma (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Önceki bölümde geçici hata işleme ve bu önbelleğe alma, devre kesici stratejisi olarak belirtiliyor. Bu bölümde, ne zaman kullanılacağı, kullanımı için ortak desenler ve Azure 'da nasıl uygulanacağı dahil olmak üzere önbelleğe alma hakkında daha fazla arka plan sunulmaktadır.

## <a name="what-is-distributed-caching"></a>Dağıtılmış önbelleğe alma nedir?

Önbellek, verileri bellekte depolayarak sık erişilen uygulama verilerine yüksek aktarım hızı ve düşük gecikmeli erişim sağlar. Bir bulut uygulaması için en kullanışlı önbellek türü, verilerin ayrı bir Web sunucusunun belleğinde, ancak diğer bulut kaynaklarında depolanmayacağı ve önbelleğe alınan verilerin bir uygulamanın Web sunucularının (veya diğer bulut sanal makinelerinin uygulama tarafından kullanılan e).

![aynı önbellek sunucularına erişen birden çok Web sunucusunu gösteren diyagram](distributed-caching/_static/image1.png)

Uygulama, sunucu ekleyerek veya kaldırarak ya da yükseltmeler veya hatalar nedeniyle sunucular değiştirildiğinde, önbelleğe alınmış veriler, uygulamayı çalıştıran her sunucu tarafından erişilebilir kalır.

Kalıcı bir veri deposuna yönelik yüksek gecikmeli veri erişiminin önlenmesini önleyerek önbelleğe alma, uygulama yanıt hızını önemli ölçüde iyileştirebilir. Örneğin, önbellekten verilerin alınması, ilişkisel bir veritabanından alınmadan çok daha hızlıdır.

Önbelleğe almanın bir tarafı avantajı kalıcı veri deposuna daha az trafik düşürür, bu da kalıcı veri deposu için veri çıkış ücretleri olduğunda daha düşük maliyetlere neden olabilir.

## <a name="when-to-use-distributed-caching"></a>Dağıtılmış önbelleğe alma ne zaman kullanılır?

Önbelleğe alma, verilerin yazılmasına kıyasla daha fazla okuyan uygulama iş yükleri için ve veri modeli, verileri depolamak ve önbellekte veri almak için kullandığınız anahtar/değer organizasyonunu desteklediğinde en iyi şekilde kullanılır. Uygulama kullanıcıları çok sayıda ortak veriyi paylaştığında de daha yararlı olur; Örneğin, her kullanıcı genellikle bu kullanıcıya özgü verileri alıyorsa, önbellek pek çok avantaj sağlamaz. Verilerin sık değiştirilmediği ve tüm müşterilerin aynı verilere bakdığı için, önbelleğe almanın çok yararlı olduğu bir örnek bir ürün kataloğudur.

Önbelleğe almanın avantajı, sürekli olarak daha fazla bir uygulama ölçeklendirilirken, kalıcı veri deposunun aktarım hızı ve gecikme gecikmeleri, genel uygulama performansı açısından daha fazla sınıra neden olur. Ancak, performansı daha da farklı nedenlerle önbelleğe alma işlemini uygulayabilirsiniz. Kullanıcıya gösterildiğinde tam olarak güncel olması gereken veriler için, önbellek erişimi, kalıcı veri deposunun yanıt vermediği veya kullanılamadığı durumlarda bir devre kesici işlevi görebilir.

## <a name="popular-cache-population-strategies"></a>Popüler önbellek popülasyon stratejileri

Önbellekten veri alabilmek için öncelikle bu dosyayı depolamanız gerekir. Bir önbellekte ihtiyacınız olan verileri almak için birkaç strateji vardır:

- Isteğe bağlı/önbelleğe alma

    Uygulama, verileri önbellekten almaya çalışır ve önbellekte veri olmadığında ("isabetsizlik"), uygulama verileri önbellekte depolar, böylece bir sonraki sefer kullanılabilir hale gelir. Uygulamanın bir dahaki sefer aynı verileri almaya çalıştığında, önbellekte ne aradığını bulur ("isabet"). Veritabanında değiştirilen önbelleğe alınmış verileri getirmeyi engellemek için, veri deposunda değişiklik yaparken önbelleği geçersiz kılın.
- Arka planda veri gönderme

    Arka plan hizmetleri, verileri düzenli bir zamanlamaya göre önbelleğe gönderir ve uygulama her zaman önbellekten çeker. Bu yaklaşım, her zaman en son verileri döndürmemenizi gerektirmeyen yüksek gecikmeli veri kaynaklarıyla harika bir şekilde çalışmaktadır.
- Devre kesici

    Uygulama normalde kalıcı veri deposuyla doğrudan iletişim kurar, ancak kalıcı veri deposunda kullanılabilirlik sorunları olduğunda, uygulama verileri önbellekten alır. Veriler önbelleğe alınmış ya da arka planda veri gönderme stratejisi kullanılarak önbelleğe alınmış olabilir. Bu, performans geliştirme stratejisi yerine bir hata işleme stratejisidir.

Verileri önbellekte tutmak için, uygulamanız verileri oluşturduğunda, güncelleştirdiğinde veya silerse ilgili önbellek girdilerini silebilirsiniz. Uygulamanızın bazı durumlarda biraz zaman güncel olmayan verileri almasını istiyorsanız, eski önbellek verilerinin nasıl olabildiğinden ilgili bir sınır ayarlamak için yapılandırılabilir bir zaman aşımı süresine güvenebilirsiniz.

Mutlak süre sonu (önbellek öğesi oluşturulduktan bu yana geçen süre) veya kayan süre sonu (önbellek öğesine en son erişildiği zamandan bu yana geçen süre) yapılandırabilirsiniz. Verilerin çok eski hale gelmesini engellemek için önbellek süre sonu mekanizmasına bağlı olduğunuzda mutlak süre sonu kullanılır. BT uygulamasını düzelttikten sonra eski önbellek öğelerini el ile çıkaracağız ve en güncel verileri önbellekte tutmak için kayan süre sonu kullanacağız. Seçtiğiniz süre sonu ilkesinden bağımsız olarak, önbelleğin bellek sınırına ulaşıldığında önbelleğin en eski (en son kullanılan veya LRU) öğelerini otomatik olarak çıkaracaktır.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>BT uygulamasının düzeltilmesi için örnek önbellek kodu

Aşağıdaki örnek kodda, bir çözüm düzeltmesini alırken önbelleği ilk olarak denetliyoruz. Görev önbellekte bulunursa, döndürüyoruz; bulunamazsa, veritabanından alınır ve önbellekte depolar. `FindTaskByIdAsync` yöntemine önbelleğe alma eklemek için yapacağınız değişiklikler vurgulanır.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Bir çözüm düzeltmesini güncelleştirdiğinizde veya sildiğinizde, önbelleğe alınmış görevi geçersiz kılmak (kaldırmanız) gerekir. Aksi takdirde, gelecekteki bu görevi okumaya çalışır ve eski verileri önbellekten almaya devam eder.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

Bunlar basit önbelleğe alma kodunu göstermeye yönelik örneklerdir; önbelleğe alma, indirilebilir çözüm projesinde uygulanmadı.

## <a name="azure-caching-services"></a>Azure önbelleğe alma hizmetleri

Azure aşağıdaki önbelleğe alma hizmetlerini sunmaktadır: [Azure Redis Cache](https://msdn.microsoft.com/library/dn690523.aspx) ve [Azure yönetilen önbelleği](https://msdn.microsoft.com/library/dn386094.aspx). Azure Redsıs Cache, popüler [Açık kaynaklı Redis Cache](http://redis.io/) dayanır ve çoğu önbelleğe alma senaryosunda ilk seçenektir.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>Önbellek sağlayıcısını kullanarak ASP.NET oturum durumu

[Web geliştirme en iyi uygulamaları](web-development-best-practices.md)bölümünde belirtildiği gibi, oturum durumunu kullanmaktan kaçınmak en iyi uygulamadır. Uygulamanız oturum durumu gerektiriyorsa, bir sonraki en iyi yöntem, ölçeği genişletme özelliğini (Web sunucusunun birden çok örneğini) etkinleştirmediği için varsayılan bellek içi sağlayıcıyı kullanmaktan kaçınmaktır. ASP.NET SQL Server oturum durumu sağlayıcısı, birden çok Web sunucusunda çalışan bir sitenin oturum durumunu kullanmasına olanak sağlar, ancak bellek içi sağlayıcıya kıyasla yüksek bir gecikme süresi ücreti doğurur. Oturum durumunu kullanmanız gerekiyorsa en iyi çözüm, [Azure önbelleği Için oturum durumu sağlayıcısı](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)gibi bir önbellek sağlayıcısı kullanmaktır.

## <a name="summary"></a>Özet

BT uygulamasının yanıt süresini ve ölçeklenebilirliğini artırmak için önbelleğe almayı nasıl uygulayabileceğini ve veritabanı kullanılamadığında uygulamanın okuma işlemlerine yanıt vermeye devam etmesini sağlayabilirsiniz. [Sonraki bölümde](queue-centric-work-pattern.md) , ölçeklenebilirliği daha fazla geliştirmeyi ve uygulamanın yazma işlemleri için yanıt vermeye devam etmeyi nasıl sağlayacağınızı göstereceğiz.

## <a name="resources"></a>Kaynaklar

Önbelleğe alma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın.

Belgeler

- [Azure önbelleği](https://msdn.microsoft.com/library/gg278356.aspx). Azure 'da önbelleğe alma hakkında resmi MSDN belgeleri.
- [Microsoft desenleri ve uygulamaları-Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). Bkz. önbelleğe alma kılavuzu ve önbellek stili.
- [Failsafe: dayanıklı bulut mimarilerine yönelik rehberlik](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Marc Mercuri, Ulrich Homann ve Andrew Townhill tarafından Teknik İnceleme. Önbelleğe alma hakkında bölümüne bakın.
- [Azure Cloud Services 'de büyük ölçekli hizmetler tasarlamak Için En Iyi uygulamalar](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Anlatımı. Simms ve Michael Thomassy ' i Işaretleyen Teknik İnceleme. Dağıtılmış önbelleğe alma bölümüne bakın.
- [Ölçeklenebilirlik yolu üzerinde dağıtılmış önbelleğe alma](https://msdn.microsoft.com/magazine/dd942840.aspx). Daha eski bir (2009) MSDN Magazine makalesi, ancak genel olarak dağıtılmış önbelleğe alma konusuna açıkça yazılmış bir giriş; , FailSafe ve En Iyi Yöntemler Teknik İncelemeleri 'nin önbelleğe alma bölümlerinden daha ayrıntılı gider.

Videolar

- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz bölümden oluşan seriler. Bulut uygulamalarının nasıl mimaralınacağını gösteren 400 düzey bir görünüm sunar. Bu seri teorik ve nedenlere odaklanır; daha fazla bilgi için, bkz. büyük seri oluşturma Simms 'yi Işaret edin. Bölüm 3 ' teki önbelleğe alma tartışmalarına 1:24:14 adresinden itibaren bakın.
- [Oluşturma büyük: Azure müşterileri tarafından öğrenilen Dersler-Bölüm ı](https://channel9.msdn.com/Events/Build/2012/3-029). Simon Davvıes, 46:00 adresinden başlayarak dağıtılmış önbelleğe almayı tartışır. Failsafe serisine benzer ancak daha fazla nasıl yapılır ayrıntılarına gider. Sununun 31 Ekim 2012 ' te verildiği, bu nedenle 2013 ' de tanıtılan Azure App Service Web Apps Önbellek hizmetini kapsamıyor.

Kod örneği

- [Azure 'Da bulut hizmeti temelleri](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Dağıtılmış önbelleğe alma uygulayan örnek uygulama. Bkz. Web günlüğü gönderi [bulut hizmeti temelleri – önbelleğe alma temelleri](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx).

> [!div class="step-by-step"]
> [Önceki](transient-fault-handling.md)
> [İleri](queue-centric-work-pattern.md)
