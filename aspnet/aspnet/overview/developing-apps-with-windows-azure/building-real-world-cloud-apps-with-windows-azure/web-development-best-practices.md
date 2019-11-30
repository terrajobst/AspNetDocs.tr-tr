---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Web geliştirme En Iyi uygulamaları (Azure ile gerçek hayatta bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: 0956aaaf1f6a1a0d2f5d93f98cb6959cec98dbaf
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582700"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Web geliştirme En Iyi uygulamaları (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

İlk üç desen çevik bir geliştirme süreci ayarlamakmıştı. geri kalan mimari ve kodlardır. Bu, bir Web geliştirme en iyi uygulamaları koleksiyonudur:

- Bir akıllı yük dengeleyicinin arkasındaki [durum bilgisiz Web sunucuları](#stateless) .
- [Oturum durumunu önleyin](#sessionstate) (veya bundan kaçınmak için bir veritabanı yerine dağıtılmış önbellek kullanın).
- [BIR CDN kullanarak](#cdn) , statik dosya varlıklarını (görüntüler, betikler) önbelleğe alma.
- Çağrı engellemeyi önlemek için [.NET 4.5 'in zaman uyumsuz desteğini kullanın](#async) .

Bu uygulamalar yalnızca bulut uygulamaları için değil tüm Web geliştirme işlemleri için geçerlidir, ancak özellikle de bulut uygulamaları için önemlidir. Bulut ortamı tarafından sunulan son derece esnek ölçeklendirmeyi en iyi şekilde kullanmanıza yardımcı olmak üzere birlikte çalışır. Bu uygulamaları izlemeden, uygulamanızı ölçeklendirmeye çalıştığınızda sınırlamalar ile karşılaşırsınız.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>Akıllı yük dengeleyicinin arkasında durum bilgisiz Web katmanı

*Durum bilgisiz Web katmanı* , herhangi bir uygulama verisini Web sunucusu belleğinde veya dosya sisteminde depolamazsanız anlamına gelir. Web katmanınızın durum bilgisiz olması, daha iyi bir müşteri deneyimi sağlamanıza ve paradan tasarruf etmenize olanak sağlar:

- Web katmanı durumsuz ve bir yük dengeleyicinin arkasında yer alıyorsa, sunucuları dinamik olarak ekleyerek veya kaldırarak uygulama trafiğinden değişikliklere hızlıca yanıt verebilirsiniz. Yalnızca kullandığınız sürece sunucu kaynakları için ödeme yaptığınız bulut ortamında, isteğe bağlı değişikliklere yanıt verme özelliği büyük tasarrufa çevrilebilir.
- Durum bilgisiz Web katmanı, uygulamanın ölçeğini genişletmek için mimari olarak çok daha basittir. Bu, ölçekleme ihtiyaçlarına daha hızlı yanıt vermenize ve süreçte geliştirme ve test konusunda daha az para harcamanıza olanak sağlar.
- Şirket içi sunucular gibi bulut sunucularının, her zaman düzeltme ve yeniden başlatılması gerekir; Web katmanı durum bilgisiz ise, bir sunucu geçici olarak kaldığında trafiği yeniden yönlendirme işlemi hatalara veya beklenmeyen davranışlara neden olmaz.

En gerçek dünya uygulamalarının, bir Web oturumu için durumu depolaması gerekir; Buradaki ana nokta onu Web sunucusunda depolamadır. Bir önbellek sağlayıcısı kullanarak, durumu tanımlama bilgilerinde istemci veya işlem sunucusu tarafında ASP.NET oturum durumu gibi başka yollarla da saklayabilirsiniz. Dosyaları yerel dosya sistemi yerine [Windows Azure Blob Storage](unstructured-blob-storage.md) 'da saklayabilirsiniz.

Web katmanınız durum bilgisiz ise, Windows Azure Web siteleri 'nde bir uygulamayı ölçeklendirmenin ne kadar kolay olduğunu gösteren bir örnek olarak, yönetim portalındaki bir Windows Azure Web sitesinin **Ölçek** sekmesine bakın:

![Ölçek sekmesi](web-development-best-practices/_static/image1.png)

Web sunucuları eklemek istiyorsanız örnek sayısı kaydırıcısını sağa sürüklemeniz yeterlidir. 5 olarak ayarlayın ve **Kaydet**' e tıklayın ve saniyeler Içinde, Microsoft Azure 'da Web sitenizin trafiğinizi işleyen 5 Web sunucusu vardır.

![Beş örnek](web-development-best-practices/_static/image2.png)

Örnek sayısını kolayca 3 ' e veya 1 ' e geri döndürebilmeniz yeterlidir. Ölçeği geri döndüğünüzde, Microsoft Azure 'un saate göre değil, dakikaya göre ücretlendirilmesi anında tasarruf etmeye başlar.

Ayrıca, Windows Azure 'un CPU kullanımına göre Web sunucularının sayısını otomatik olarak artırmasını veya azaltmasını söyleyebilirsiniz. Aşağıdaki örnekte, CPU kullanımı %60 altına gittiğinde, Web sunucularının sayısı en az 2 ' ye düşürülecektir ve CPU kullanımı %80 ' nin üzerinde olursa, Web sunucularının sayısı en fazla 4 ' e yükseltilir.

![CPU kullanımına göre ölçeklendir](web-development-best-practices/_static/image3.png)

Ya da sitenizin yalnızca çalışma saatlerinde meşgul olacağını biliyorsanız ne olur? Windows Azure 'a, gündüz saati sırasında birden çok sunucu çalıştırmasını ve tek bir sunucu evente, Nights ve hafta sonlarını azaltmasını söyleyebilirsiniz. Aşağıdaki ekran görüntüleri serisi, Web sitesinin, çalışma saatleri boyunca saat ve 4 sunucu çalıştırmak üzere, 8 ile 5 PM arasında bir sunucuyu nasıl ayarlayacağınızı gösterir.

![Zamanlamaya göre ölçeklendir](web-development-best-practices/_static/image4.png)

![Zamanlama sürelerini ayarlama](web-development-best-practices/_static/image5.png)

![Gündüz zamanlaması](web-development-best-practices/_static/image6.png)

![Weekgece zamanlaması](web-development-best-practices/_static/image7.png)

![Hafta sonu zamanlaması](web-development-best-practices/_static/image8.png)

Ayrıca, bu tüm elbette, portalda ve portalda de yapılabilir.

Uygulamanızın ölçeklendirme özelliği, Microsoft Azure 'da neredeyse sınırsız olduğundan, Web katmanını durum bilgisiz halinde tutarak sunucu VM 'lerini dinamik olarak eklemek veya kaldırmak için gereken engelleri ortadan kaldırırsınız.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>Oturum durumunu önleyin

Bir Kullanıcı oturumu için bir durum biçiminin depolanmasını önlemek için genellikle gerçek dünyada bir bulut uygulamasında pratik değildir ancak bazı yaklaşımlar performansı ve ölçeklenebilirliği diğerlerinden daha fazla etkiler. Durumu depolamanız gerekirse, en iyi çözüm durum miktarını küçük tutmak ve tanımlama bilgilerinde depolamak olur. Bu uygun değilse, bir sonraki en iyi çözüm [Dağıtılmış, bellek içi önbellek](distributed-caching.md#sessionstate)için bir sağlayıcıyla ASP.NET oturum durumunu kullanmaktır. Performans ve ölçeklenebilirlik açısından en kötü çözüm, veritabanı tarafından desteklenen bir oturum durumu sağlayıcısı kullanmaktır.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>Statik dosya varlıklarını önbelleğe almak için CDN kullanma

CDN, Content Delivery Network için bir kısaltdır. Bir CDN sağlayıcısına görüntü ve betik dosyaları gibi statik dosya varlıkları sağlarsınız ve sağlayıcı bu dosyaları tüm dünyada veri merkezlerinde önbelleğe alır, böylece her kişi uygulamanıza erişebildiklerinden, önbelleğe alınmış olması için görece hızlı yanıt ve düşük gecikme süresi alırlar varlıklar. Bu, sitenin genel yükleme süresini hızlandırır ve web sunucularınızda yükü azaltır. Coğrafi olarak geniş bir şekilde dağıtılan bir hedef kitleye ulaşmanız durumunda CDNs özellikle önemlidir.

Windows Azure 'da bir CDN vardır ve Windows Azure 'da veya herhangi bir Web barındırma ortamında çalışan bir uygulamada diğer CDNs kullanabilirsiniz.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>Çağrı engellemeyi önlemek için .NET 4.5 'in zaman uyumsuz desteğini kullanın

.NET 4,5, C# görevlerin zaman uyumsuz olarak işlemesini çok daha basit hale getirmek IÇIN ve vb programlama dillerini geliştirmiştir. Zaman uyumsuz programlama avantajı, aynı anda birden çok Web hizmeti çağrısı yapmak istediğinizde gibi paralel işleme durumları için değildir. Ayrıca, Web sunucunuzun yüksek yük koşullarında daha verimli ve güvenilir bir şekilde çalışmasını sağlar. Bir Web sunucusu yalnızca kullanılabilir sayıda iş parçacığına sahiptir ve yüksek yük koşulları altında, tüm iş parçacıkları kullanımda olduğunda, gelen isteklerin iş parçacıkları serbest olana kadar beklemesi gerekir. Uygulama kodunuz veritabanı sorguları ve Web hizmeti çağrısı gibi görevleri zaman uyumsuz olarak işlemezse, sunucu bir g/ç yanıtı beklerken birçok iş parçacığı gereksiz yere bağlı olur. Bu, sunucunun yüksek yük koşulları altında işleyebileceği trafik miktarını sınırlandırır. Zaman uyumsuz programlama ile, bir Web hizmetini veya veritabanını döndürmek için bekleyen iş parçacıkları, veri alınana kadar yeni isteklere hizmet vermek için serbest bırakılır. Meşgul bir Web sunucusunda, yüzlerce veya binlerce istek daha sonra işlem için iş parçacıklarının serbest bırakılabileceği şekilde beklenmez.

Daha önce gördüğünüz gibi, Web sitenizi artıracak Web sunucusu sayısını azaltmak oldukça kolay bir işlemdir. Bu nedenle, bir sunucu daha fazla işleme sağlayabiliyorsa, bu kadar birçok işlem yapmanız gerekmez ve belirli bir trafik hacmi için daha az sunucuya ihtiyacınız olduğundan maliyetlerinizi azaltabilirsiniz.

.NET 4,5 zaman uyumsuz programlama modeli desteği Web Forms, MVC ve Web API 'SI için ASP.NET 4,5 ' ye dahildir; Entity Framework 6 ' da ve [Windows Azure Storage API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)' de.

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4,5 ' de zaman uyumsuz destek

ASP.NET 4,5 ' de, zaman uyumsuz programlama desteği yalnızca dile değil, MVC, Web Forms ve Web API çerçevelerine de eklenmiştir. Örneğin, bir ASP.NET MVC denetleyici eylemi yöntemi bir Web isteğinden verileri alır ve verileri tarayıcıya gönderilmek üzere HTML oluşturan bir görünüme geçirir. Genellikle eylem yönteminin bir Web sayfasında gösterilmesi veya bir Web sayfasına girilen verileri kaydetmesi için bir veritabanından veya Web hizmetinden veri alması gerekir. Bu senaryolarda, eylem yöntemini zaman uyumsuz yapmak kolaydır: bir *ActionResult* nesnesi döndürmek yerine, *görev&lt;ActionResult&gt;* döndürür ve yöntemi *Async* anahtar sözcüğüyle işaretler. Yöntemi içinde, bir kod satırı bekleme süresi içeren bir işlemden sonra, await anahtar sözcüğüyle işaretlersiniz.

Veritabanı sorgusu için bir depo yöntemi çağıran basit bir eylem yöntemi aşağıda verilmiştir:

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

İşte veritabanı çağrısını zaman uyumsuz olarak işleyen yöntemin aynısı:

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

' In altında, derleyici uygun zaman uyumsuz kodu oluşturur. Uygulama `FindTaskByIdAsync`çağrısı yaptığında, ASP.NET `FindTask` isteği yapar ve ardından çalışan iş parçacığını geri alabilir ve başka bir isteği işlemek için kullanılabilir hale getirir. `FindTask` isteği tamamlandığında, bu çağrıdan sonra gelen kodu işlemeye devam etmek için bir iş parçacığı yeniden başlatılır. `FindTask` isteğin başlatıldığı ve verilerin döndürüldüğü zaman arasında aradaki bir iş parçacığına sahip olursunuz, aksi takdirde, yanıt beklenmek üzere bağlı olacak şekilde, yararlı işler gerçekleştirebilirsiniz.

Zaman uyumsuz kod için bazı ek yük vardır, ancak düşük yük koşullarında bu ek yük göz ardı edilebilir, ancak yüksek yük koşullarında, diğer durumlarda kullanılabilir iş parçacıkları için bekleyen istekleri işleyebileceksiniz.

Bu tür zaman uyumsuz programlamayı ASP.NET 1,1 tarihinden itibaren yapmak mümkün, ancak yazmak, hataya açık ve hata ayıklama zor bir sorun oluştu. Bu nedenle, ASP.NET 4,5 ' de kodlama basitleştirildiğimiz için artık bu değil.

### <a name="async-support-in-entity-framework-6"></a>Entity Framework 6 ' da zaman uyumsuz destek

4,5 ' de zaman uyumsuz desteğin bir parçası olarak Web hizmeti çağrıları, yuvalar ve dosya sistemi g/ç için zaman uyumsuz destek sunduk, ancak Web uygulamaları için en yaygın model bir veritabanına ulaşmalıdır ve veri kitaplıklarımız zaman uyumsuz olarak desteklenmez. Artık Entity Framework 6, veritabanı erişimi için zaman uyumsuz destek ekler.

Entity Framework 6 ' da, bir sorgunun veya komutun veritabanına gönderilmesine neden olan tüm yöntemler zaman uyumsuz sürümlere sahiptir. Buradaki örnekte *Find* yönteminin Async sürümü gösterilmektedir.

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

Bu zaman uyumsuz destek yalnızca ekleme, silme, güncelleştirme ve basit bulma için değil, LINQ sorguları ile de kullanılabilir:

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

Bu kodda, bir sorgunun veritabanına gönderilmesine neden olan yöntemi olan `ToList` yönteminin `Async` bir sürümü vardır. `Where` ve `OrderByDescending` yöntemleri yalnızca sorguyu yapılandırır, ancak `ToListAsync` yöntemi sorguyu yürütür ve yanıtı `result` değişkenine depolar.

## <a name="summary"></a>Özet

Burada özetlenen Web geliştirme en iyi uygulamalarını herhangi bir Web programlama çerçevesinde ve herhangi bir bulut ortamında uygulayabilirsiniz, ancak ASP.NET ve Windows Azure 'da araçlara kolayca ulaşabilirsiniz. Bu desenleri izlerseniz, Web katmanınızı kolayca ölçeklendirebilirsiniz ve her sunucu daha fazla trafik işleyebildiğinden, harcamalarınızı en aza indirirsiniz.

[Sonraki bölümde](single-sign-on.md) , bulutun çoklu oturum açma senaryolarına nasıl izin vertığı gösterilmektedir.

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için aşağıdaki kaynaklara bakın.

Durum bilgisiz Web sunucuları:

- [Microsoft düzenleri ve uygulamaları-otomatik ölçeklendirme Kılavuzu](https://msdn.microsoft.com/library/dn589774.aspx).
- [Windows Azure Web siteleri 'nde ARR 'Nin örnek benzeşimini devre dışı bırakma](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/). Erez Benari tarafından blog gönderisi, Windows Azure Web siteleri 'nde oturum benzeşimini açıklar.

'Ye

- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz parçalı video serisi. Bölüm 3 ' teki CDN tartışmasına 1:34:00 adresinden itibaren bakın.
- [Microsoft desenleri ve uygulamaları statik Içerik barındırma düzeni](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN İncelemeleri](http://www.cdnreviews.com/). Birçok CDNs 'ye genel bakış.

Zaman uyumsuz programlama:

- [ASP.NET MVC 4 ' te zaman uyumsuz yöntemler kullanılıyor](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md). Rick Anderson ile öğretici.
- [Async ve await Ile zaman uyumsuz programlamaC# (ve Visual Basic)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx). Zaman uyumsuz programlama için ktionale, ASP.NET 4,5 ' de nasıl çalıştığını ve bunu uygulamak için kod yazmayı açıklayan MSDN teknik incelemesi.
- [Zaman uyumsuz sorgu Entity Framework ve Kaydet](https://msdn.microsoft.com/data/jj819165)
- [Zaman uyumsuz kullanarak ASP.NET Web uygulamaları oluşturma](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7). ROWA Miller tarafından video sunumu. , Zaman uyumsuz programlamanın, yüksek yük koşulları altında Web sunucusu aktarım hızına önemli artışların nasıl kolaylaştırdığı hakkında bir grafik tanıtımı içerir.
- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz parçalı video serisi. Ölçeklenebilirlik sırasında zaman uyumsuz programlamayı etkileyen tartışmalar için, bkz. Bölüm 4 ve Bölüm 8.
- [ASP.NET 4,5 ' de zaman uyumsuz yöntemlerin kullanıldığı Magic, önemli bir Gotcha](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). Scott Hanselman tarafından, öncelikli olarak ASP.NET Web Forms uygulamalarında zaman uyumsuz kullanma hakkında blog gönderisi.

Daha fazla Web geliştirme için en iyi uygulamalar için aşağıdaki kaynaklara bakın:

- [Bu örnek, En Iyi uygulama uygulamalarını düzeltir](the-fix-it-sample-application.md#bestpractices). Bu e-kitabın eki, BT BT uygulamasında uygulanan bir dizi en iyi uygulamayı listeler.
- [Web geliştiricisi denetim listesi](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [Önceki](continuous-integration-and-continuous-delivery.md)
> [İleri](single-sign-on.md)
