---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: İzleme ve telemetri (Azure ile gerçek hayatta bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: 44941c9fd0dcd3223604fc4a4f2836f587578acb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585600"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>İzleme ve telemetri (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Birçok kişi, uygulamasının uygulamalarının ne zaman olduğu konusunda bilgi sahibi olmalarını sağlamak için müşterileri kullanır. Bu, özellikle bulutta değil, her yerde en iyi yöntem değildir. Hızlı bildirim garantisi yoktur ve bildirim aldığınızda, genellikle ne olduğu hakkında en az veya yanıltıcı veriler alırsınız. İyi telemetri ve günlüğe kaydetme sistemleriyle, uygulamanızda neler olduğunu biliyor olabilirsiniz ve yanlış bir şeyler olduğunda hemen öğreniyor ve ile çalışmak için yararlı sorun giderme bilgileri bulabilirsiniz.

## <a name="buy-or-rent-a-telemetry-solution"></a>Telemetri çözümü satın alma veya kira

> [!NOTE]
> Bu makale [Application Insights](/azure/application-insights/app-insights-overview) yayınlanmadan önce yazılmıştır. Azure 'da Telemetri Çözümleri için tercih edilen yaklaşım Application Insights. Daha fazla bilgi için bkz. [ASP.NET Web siteniz için Application Insights ayarlama](/azure/application-insights/app-insights-asp-net) .

Bulut ortamı hakkında harika olan şeylerden biri, yakın bir şekilde satın alma veya sizin için uygun hale getirmenin oldukça kolay bir işlemdir. Telemetri bir örnektir. Çok çaba duymadan, iyi maliyetli bir telemetri sistemini çalışır duruma getirebilirsiniz. Azure ile tümleştirilen harika iş ortakları vardır ve bunlardan bazılarının ücretsiz katmanları vardır. bu sayede, hiçbir şey için temel telemetri alabilirsiniz. Azure 'da Şu anda kullanılabilir olanlardan yalnızca birkaçını bulabilirsiniz:

- [Yeni relik](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [DynaTrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) , izleme özelliklerini de içerir.

Bir telemetri sistemi kullanmanın ne kadar kolay olduğunu göstermek için yeni bir relik ayarlamayı hızla adım adım inceleyeceğiz.

Azure Yönetim Portalı ' nda hizmete kaydolun. **Yeni**' ye ve ardından **Mağaza**' ya tıklayın. **Eklenti Seç** iletişim kutusu görüntülenir. Aşağı kaydırın ve **Yeni relik**' e tıklayın.

![Eklenti Seç](monitoring-and-telemetry/_static/image1.png)

Sağ oka tıklayın ve istediğiniz hizmet katmanını seçin. Bu tanıtımda ücretsiz katmanı kullanacağız.

![Eklentiyi Kişiselleştir](monitoring-and-telemetry/_static/image2.png)

Sağ oka tıklayın, "satın al" seçeneğini onaylayın ve yeni relik artık portalda eklenti olarak gösterilir.

![Satın alma gözden geçirme](monitoring-and-telemetry/_static/image3.png)

![Yönetim Portalı 'nda yeni relik eklentisi](monitoring-and-telemetry/_static/image4.png)

**Bağlantı bilgileri**' ne tıklayın ve lisans anahtarını kopyalayın.

![Bağlantı bilgileri](monitoring-and-telemetry/_static/image5.png)

Portalda Web uygulamanızın **Yapılandır** sekmesine gidin, **performans izlemeyi** **eklenti**olarak ayarlayın ve **eklenti Seç** açılan listesini **Yeni relik**olarak ayarlayın. Ardından **Kaydet**' e tıklayın.

![Yapılandır sekmesinde yeni relik](monitoring-and-telemetry/_static/image6.png)

Visual Studio 'da, yeni relik NuGet paketini uygulamanıza yükler.

![Yapılandır sekmesinde geliştirici Analizi](monitoring-and-telemetry/_static/image7.png)

Uygulamayı Azure 'a dağıtın ve kullanmaya başlayın. Yeni relik izlemeye yönelik bazı etkinlikler sağlamak için birkaç çözüm görevi oluşturun.

Ardından portalın **Eklentiler** sekmesinde **Yeni relik** sayfasına dönün ve **Yönet**' e tıklayın. Portal, sizi kimlik doğrulaması için çoklu oturum açma 'yı kullanarak yeni relik yönetim portalına gönderir, böylece kimlik bilgilerinizi yeniden girmeniz gerekmez. Genel Bakış sayfasında çeşitli performans istatistikleri sunulmaktadır. (Genel Bakış sayfasının tam boyutunu görmek için resme tıklayın.)

[![yeni relik Izleme sekmesi](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

Görebileceğiniz istatistiğin bazıları aşağıda verilmiştir:

- Günün farklı saatlerinde ortalama yanıt süresi.

    ![Yanıt süresi](monitoring-and-telemetry/_static/image10.png)
- Gün sayısı (dakika başına isteklerde), günün farklı saatlerinde.

    ![Trafiği](monitoring-and-telemetry/_static/image11.png)
- Farklı HTTP isteklerini işlemek için harcanan sunucu CPU süresi.

    ![Web Işlem süreleri](monitoring-and-telemetry/_static/image12.png)
- Uygulama kodunun farklı bölümlerinde harcanan CPU süresi:

    ![İzleme ayrıntıları](monitoring-and-telemetry/_static/image13.png)
- Geçmiş performans istatistikleri.

    ![Geçmiş performans](monitoring-and-telemetry/_static/image14.png)
- Blob hizmeti gibi harici hizmetlere ve hizmetin ne kadar güvenilir ve hızlı yanıt verdiğini gösteren bir çağrı.

    ![Dış hizmetler](monitoring-and-telemetry/_static/image15.png)

    ![Dış hizmetler](monitoring-and-telemetry/_static/image16.png)

    ![Dış hizmet](monitoring-and-telemetry/_static/image17.png)
- Dünyanın neresinde veya ABD web uygulaması trafiğinden nereden geldiği hakkında bilgi.

    ![Coğrafya](monitoring-and-telemetry/_static/image18.png)

Ayrıca, raporları ve olayları da ayarlayabilirsiniz. Örneğin, hataları görmeye başladığınızda sorun için uyarı destek personeline bir e-posta gönderebilirsiniz.

![Raporlar](monitoring-and-telemetry/_static/image19.png)

Yeni relik, telemetri sistemine yalnızca bir örnektir; Bunu diğer hizmetlerden de edinebilirsiniz. Bulutun kullanımı herhangi bir kod yazmak zorunda kalmadan, en az veya ücretsiz bir masraf için, uygulamanızın nasıl kullanıldığı ve müşterilerinizin gerçekten ne yaşdığı hakkında daha fazla bilgi edinebilirsiniz.

<a id="log"></a>
## <a name="log-for-insight"></a>Öngörüler için günlüğe kaydet

Bir telemetri paketi iyi bir ilk adımdır, ancak yine de kendi kodunuzu işaretlememelisiniz. Telemetri hizmeti size bir sorun olduğunda size bildirir ve müşterilerin ne yaşar olduğunu söyler, ancak kodunuzda neler olduğuna ilişkin çok sayıda öngörü sunmayabilir.

Uygulamanızın ne yaptığını görmek için bir üretim sunucusuna uzaktan gerek olmasını istemezsiniz. Bu, bir sunucuya sahip olduğunuzda, ancak yüzlerce sunucuya ölçeklendirdiğinizde ve ne zaman uzak bir sürümüne ihtiyacınız olduğunu bilmediğinizde pratik olabilir mi? Günlüğe kaydetme, sorunları çözümlemek ve hatalarını ayıklamak için üretim sunucularına hiçbir şekilde uzaktan ihtiyacınız olmayan bilgiler sağlamalıdır. Sorunları yalnızca günlüklerde yalıtmak için yeterli bilgileri günlüğe kaydetmelisiniz.

### <a name="log-in-production"></a>Üretimde oturum aç

Çok sayıda insan, yalnızca bir sorun olduğunda ve hata ayıklamak istediklerinde üretimde izlemeyi açabilir. Bu, bir sorunun farkında olduğunuz zaman ile ilgili yararlı sorun giderme bilgileri hakkında önemli bir gecikme ortaya çıkarabilir. Ve aldığınız bilgiler aralıklı hatalar için yararlı olmayabilir.

Bulut ortamında, depolamanın her zaman üretimde oturum açmasını her zaman nerede bırakılabileceği, bulut ortamında neleri öneririz. Bu şekilde, hatalar zaten günlüğe kaydedilir ve zaman içinde ortaya çıkan veya düzenli olarak farklı zamanlarda oluşan sorunları çözümlemenize yardımcı olabilecek geçmiş verileriniz vardır. Eski günlükleri silmek için temizleme işlemini otomatikleştirebilir, ancak bu tür bir işlemin daha pahalı olduğunu fark edebilirsiniz.

Ek günlük harcama miktarı, sorun giderme süresi ve para miktarı ile karşılaştırıldığında, bir şeyler yanlış kaldığında daha önce kullanılabilir olan tüm bilgilere sahip olabilirsiniz. Daha sonra, bir sorun 8:00 son gece etrafında rastgele bir hata olduğunu söylediklerinde, ancak hatayı anımsamadığında, sorunun ne olduğunu kolayca öğrenebilirsiniz.

Bir ay $4 ' den az olduğunda, her şeyi göz önünde bulundurarak, günlük kaydı kitaplığınızın zaman uyumsuz olduğundan emin olmak için en az 50 gigabayt oturum açma performansı vardır.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>İşlem gerektiren günlüklerden haberdar olan günlükleri ayırt etme

Günlükler BILGILENDIRMEYE yöneliktir (bir şeyi bilmeniz istiyorum) veya hareket (bir şey yapmak istiyorum). Yalnızca bir kişi ya da otomatikleştirilmiş bir işlemin işlem yapması için gerekli olan konularda yalnızca eylem günlüklerini yazmaya dikkat edin. Çok fazla sayıda Işlem günlüğü gürültü oluşturacak ve bu, orijinal sorunları bulmak için tamamen bu kadar çok iş gerektirir. Ve hareket günlükleriniz, destek personeline e-posta göndermek gibi bazı eylemleri otomatik olarak tetikleriyorsa, bu tür eylemlerin tek bir sorun tarafından tetiklenmesine izin vermekten kaçının.

.NET System. Diagnostics izlenirken, günlüklere hata, uyarı, bilgi ve hata ayıklama/ayrıntı düzeyi atanabilir. Işlem günlükleri için hata düzeyini ayırarak ve BILGI günlükleri için alt düzeyleri kullanarak, Işlem günlüklerini bilgilendirebilirler.

![Günlüğe kaydetme düzeyleri](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>Çalışma zamanında günlük düzeylerini yapılandırma

Her zaman üretimde oturum açmak çok iyi bir uygulamadır, ancak uygulamanızı yeniden dağıtmanıza veya yeniden başlatmanıza gerek kalmadan, günlük kaydı yaptığınız ayrıntı düzeyinde ayarlamanıza olanak tanıyan bir günlüğe kaydetme çerçevesi uygulamaktır. Örneğin, `System.Diagnostics` ' de izleme tesis kullandığınızda hata, uyarı, bilgi ve hata ayıklama/ayrıntılı günlükleri oluşturabilirsiniz. Üretim sırasında hata, uyarı ve bilgi günlüklerini her zaman günlüğe kaydetmenizi ve büyük/küçük harfe göre sorun giderme için hata ayıklama/ayrıntılı günlük eklemek istediğinizi öneririz.

Azure App Service Web Apps, dosya sistemine, tablo depolamasına veya blob depolamaya `System.Diagnostics` günlükleri yazmak için yerleşik desteğe sahiptir. Her depolama hedefi için farklı günlüğe kaydetme düzeyleri seçebilir ve uygulamanızı yeniden başlatmadan hızlı bir şekilde günlüğe kaydetme düzeyini değiştirebilirsiniz. HDInsight 'ın BLOB depolama ile doğrudan nasıl çalışacağını bildiği için BLOB depolama desteği, uygulama günlüklerinizde [HDInsight](https://docs.microsoft.com/azure/hdinsight/) analiz işlerinin çalıştırılmasını kolaylaştırır.

### <a name="log-exceptions"></a>Özel Durumları Günlüğe Kaydetme

Yalnızca *özel durum yerleştirmeyin. Günlük kodunuzda ToString ()* . Bu, bağlamsal bilgileri bırakır. SQL hataları söz konusu olduğunda, SQL hata numarasını bırakır. Tüm özel durumlar için bağlam bilgilerini, özel durumunun kendisini ve iç özel durumları, sorun giderme için gerekli olacak her şeyi sağladığınızdan emin olmak için ekleyin. Örneğin, bağlam bilgileri sunucu adı, işlem tanımlayıcısı ve Kullanıcı adı (parola veya herhangi bir gizli dizi) içerebilir.

Özel durum günlüğü ile doğru şeyi yapmak için her bir geliştiriciye güveniyorsanız, bunlardan bazıları olmayacaktır. Her seferinde doğru şekilde yapıldığından emin olmak için, günlükçü arabiriminize özel durum işleme oluşturun: özel durum nesnesini günlükçü sınıfına geçirin ve özel durum verilerini günlükçü sınıfında doğru şekilde günlüğe kaydedin.

### <a name="log-calls-to-services"></a>Hizmetlere günlük çağrıları

Bir veritabanı veya REST API ya da herhangi bir dış hizmet olsun, uygulamanız bir hizmete her çağırdığında bir günlük yazmanızı kesinlikle öneririz. Günlüklerinizi yalnızca başarı veya başarısızlık göstergesi değil, her isteğin ne kadar sürdüğünü ekleyin. Bulut ortamında, genellikle tüm kesintiler yerine yavaşlamalarla ilgili sorunları görürsünüz. Normalde 10 milisaniyeye sahip olan bir şey aniden bir saniye almaya başlayabilir. Birisi uygulamanızın yavaş olduğunu söyledikçe, yeni relik 'e veya sahip olduğunuz telemetri hizmetine bakmak ve deneyimlerini doğrulamanız ve sonra neden yavaş olduğuna ilişkin ayrıntıları görmek için kendi günlüklerinizi bakabilmek isteyebilirsiniz.

### <a name="use-an-ilogger-interface"></a>ILogger arabirimi kullanma

Bir üretim uygulaması oluşturduğunuzda ne yapmanız önerilir basit bir *ILogger* arabirimi oluşturmak ve içindeki bazı yöntemleri kontrol etmek. Bu, daha sonra günlüğe kaydetme uygulamasının değiştirilmesini kolaylaştırır ve bunu yapmak için tüm kodunuzun üzerine gitmemelidir. Çözüm uygulamasının tamamında `System.Diagnostics.Trace` sınıfını kullanabiliriz, ancak bunun yerine *ıllogger*uygulayan bir günlüğe kaydetme sınıfındaki kapakların altında kullanıyoruz ve uygulama genelinde *ILogger* Yöntem çağrıları yaptık.

Bu şekilde, günlüğü daha zengin hale getirmek istiyorsanız, [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) istediğiniz günlük mekanizmasıyla değiştirebilirsiniz. Örneğin, uygulamanız büyüdükçe [NLog](http://nlog-project.org/) veya [Kurumsal kitaplık günlüğü uygulama bloğu](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)gibi daha kapsamlı bir günlük paketi kullanmak istediğinize karar verebilirsiniz. ([Log4Net](http://logging.apache.org/log4net/) başka bir popüler günlük çerçevesidir ancak zaman uyumsuz günlüğe kaydetme yapmaz.)

NLog gibi bir Framework kullanmanın olası bir nedeni, günlük çıkışını ayrı yüksek hacimli ve yüksek değerli veri depolarına bölmek için kullanılır. Bu, hızlı sorguları yürütmenize gerek kalmaz büyük hacimlere yönelik verileri verimli bir şekilde depolamanıza yardımcı olur. böylece, hareket verilerine hızlı erişim sağlar.

### <a name="semantic-logging"></a>Anlam günlüğe kaydetme

Daha kullanışlı tanılama bilgileri üreten günlüğe kaydetme işleminin görece yeni bir yolu için bkz. [Enterprise Library anlam günlüğü uygulama bloğu (blok)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). BLOK, daha fazla yapılandırılmış ve sorgulanabilir Günlükler oluşturmanızı sağlamak üzere .NET 4,5 ' de [Windows Için olay izleme](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) ve [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) desteği kullanır. Günlüğe girdiğiniz her bir olay türü için farklı bir yöntem tanımlarsınız ve bu, yazdığınız bilgileri özelleştirmenize olanak sağlar. Örneğin, bir SQL veritabanı hatasını günlüğe kaydetmek için bir `LogSQLDatabaseError` yöntemi çağırabilirsiniz. Bu tür bir özel durum için, önemli bir bilgi parçasının hata numarası olduğunu bildiğiniz için, yöntem imzasına bir hata numarası parametresi ekleyebilir ve hata numarasını yazdığınız günlük kaydında ayrı bir alan olarak kaydedebilirsiniz. Bu sayı ayrı bir alanda olduğundan, hata numarasını bir ileti dizesinde zaten saydıysanız, SQL hata numaralarına göre daha kolay ve güvenilir bir şekilde rapor alabilirsiniz.

## <a name="logging-in-the-fix-it-app"></a>BT BT uygulamasında günlüğe kaydetme

### <a name="the-ilogger-interface"></a>ILogger arabirimi

Bu, çözüm uygulamasındaki *ILogger* arabirimidir.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

Bu yöntemler, *System. Diagnostics*tarafından desteklenen aynı dört düzeyde Günlükler yazmanızı sağlar. Traceapı yöntemleri, dış hizmet çağrılarının gecikme süresiyle ilgili bilgilerle günlüğe kaydedilmesine yöneliktir. Hata ayıklama/ayrıntı düzeyi için bir yöntemler kümesi de ekleyebilirsiniz.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger arabiriminin günlükçü uygulama

Arabirimin uygulanması gerçekten basittir. Temel olarak yalnızca standart *System. Diagnostics* yöntemlerine çağrı yapılır. Aşağıdaki kod parçacığında, her üç bilgi yönteminin ve bir birinin her biri gösterilmektedir.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>ILogger yöntemlerini çağırma

BT BT uygulamasındaki her kod bir özel durumu yakalar, özel durum ayrıntılarını günlüğe kaydetmek için bir *ILogger* yöntemi çağırır. Veritabanı, blob hizmeti ya da bir REST API her ne zaman bir çağrı yaptığında, çağrıdan önce bir kronometre başlatılır, hizmet döndüğünde kronometre 'u sonlandırır ve başarı veya başarısızlık hakkındaki bilgilerle birlikte geçen süreyi günlüğe kaydeder.

Günlük iletisinin sınıf adı ve yöntem adını içerdiğine dikkat edin. Günlük iletilerinin, uygulama kodunun hangi bölümünün yazabileceğinizden emin olmak iyi bir uygulamadır.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

Böylece BT uygulamasının her bir SQL veritabanı çağrısı yaptığı her seferinde, çağrıyı, çağıran yöntemi ve tam olarak ne kadar zaman sürdüğünü görebilirsiniz.

![Günlüklerde SQL veritabanı sorgusu](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

Günlüklere göz atmaya giderseniz, zaman veritabanının Take değişkeninin olduğunu görebilirsiniz. Bu bilgiler yararlı olabilir: uygulama tüm bunları günlüğe kaydettiğinden, veritabanı hizmetinin zaman içinde nasıl gerçekleştiridiğiyle ilgili geçmiş eğilimlerini çözümleyebilirsiniz. Örneğin, bir hizmet çoğu zaman hızlı olabilir, ancak istekler başarısız olabilir veya yanıt belirli zamanlarda yavaşlayabilir.

Blob hizmeti için aynı şeyi yapabilirsiniz. her uygulama yeni bir dosyayı her yüklediğinde, bir günlük bulunur ve her bir dosyayı karşıya yüklemek için ne kadar sürdüğünü tam olarak görebilirsiniz.

![Blob karşıya yükleme günlüğü](monitoring-and-telemetry/_static/image23.png)

Her bir hizmeti her çağırdığınızda yazmak üzere yalnızca birkaç ek kod satırı vardır ve birisi bir sorunla karşılaştığında, tam olarak ne olduğunu, bir hata olup olmadığını ve yalnızca yavaş çalışıyor olsa bile, bir sorun olduğunu bilirsiniz. Sorunun kaynağını bir sunucuda uzaktan açmaya gerek kalmadan veya hata olduktan sonra günlüğü açıp yeniden oluşturmayı umuyoruz.

## <a name="dependency-injection-in-the-fix-it-app"></a>BT BT uygulamasına bağımlılık ekleme

Yukarıda gösterilen örnekteki depo oluşturucusunun günlükçü arabirimi uygulamasını nasıl aldığından merak edebilirsiniz:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

Uygulamayı uygulamaya bağlamak için uygulama, [AutoFac](http://autofac.org/)ile [bağımlılık ekleme](http://en.wikipedia.org/wiki/Dependency_injection)(dı) kullanır. Dı, kodunuzun tamamında birçok yerde bir arabirime dayalı bir nesne kullanmanıza olanak sağlar ve yalnızca arabirim örneği oluşturulurken kullanılan uygulamayı tek bir yerde belirtmeniz gerekir. Bu, uygulamanın değiştirilmesini kolaylaştırır: Örneğin, System. Diagnostics günlükçüsü ' yi bir NLog günlükçüsü ile değiştirmek isteyebilirsiniz. Ya da otomatik test için, günlükçü 'nin bir sahte sürümünü yerine koymak isteyebilirsiniz.

BT uygulaması, tüm depolarda ve tüm denetleyicilerde DI kullanır. Denetleyici sınıflarının oluşturucuları bir *ıtaskrepository* arabirimini, deponun bir günlükçü arabirimi aldığı şekilde alır:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

Uygulama, bu oluşturucular için *Taskrepository* ve *günlükçü* örneklerini otomatik olarak sağlamak için AutoFac dı kitaplığını kullanır.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

Bu kod, bir oluşturucunun hiçbir yerde bir *ILogger* arabirimine ihtiyacı olduğunu, *günlükçü* sınıfının bir örneğini geçirdiğini ve bir *ıfixittaskrepository* arabirimine Ihtiyaç duyduğunda, *fixittaskrepository* sınıfının bir örneğini geçirdiğini söyler.

[AutoFac](http://autofac.org/) , kullanabileceğiniz birçok bağımlılık ekleme çerçevelerinden biridir. Diğer popüler bir tane, Microsoft düzenleri ve uygulamaları tarafından önerilen ve desteklenen [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)'dir.

## <a name="built-in-logging-support-in-azure"></a>Azure 'da yerleşik günlük desteği

Azure, [Azure App Service Web Apps için aşağıdaki günlük](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)türlerini destekler:

- System. Diagnostics izleme (siteyi yeniden başlatmadan sırasıyla açık ve kapalı bir şekilde düzeyler ayarlayabilirsiniz).
- Windows olayları.
- IIS günlükleri (HTTP/FREB).

Azure, [Cloud Services ' de aşağıdaki günlük](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)türlerini destekler:

- System. Diagnostics izleme.
- Performans sayaçları.
- Windows olayları.
- IIS günlükleri (HTTP/FREB).
- Özel dizin izleme.

Bu BT uygulaması, System. Diagnostics izlemesini kullanır. Sistemi etkinleştirmek için yapmanız gereken tek şey. bir Web uygulamasında tanılama günlüğü, portalda bir anahtarı ters çevirme veya REST API çağırma. Portalda sitenizin **yapılandırma** sekmesine tıklayın ve **Uygulama Tanılama** bölümünü görmek için sayfayı aşağı kaydırın. Günlüğe kaydetmeyi açabilir veya kapatabilir ve istediğiniz günlüğe kaydetme düzeyini seçebilirsiniz. Azure 'un günlükleri dosya sistemine veya bir depolama hesabına yazmasını sağlayabilirsiniz.

![Yapılandır sekmesinde Uygulama Tanılama ve site tanılama](monitoring-and-telemetry/_static/image24.png)

Azure 'da günlüğü etkinleştirdikten sonra, Visual Studio çıktı penceresinde oluşturuldukları gibi günlükleri görebilirsiniz.

![Akış günlükleri menüsü](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![Akış günlükleri menüsü](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

Ayrıca, depolama hesabınıza yazılır ve bunları Visual Studio veya [Azure Depolama Gezgini](https://azure.microsoft.com/features/storage-explorer/) **Sunucu Gezgini** gibi Azure depolama tablo hizmetine erişebilen herhangi bir araçla görüntüleyebilirsiniz.

![Sunucu Gezgini oturum açar](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>Özet

Kullanıma hazır bir telemetri sistemi uygulamak, kendi kodunuzda oturum açmak ve Azure 'da günlüğe kaydetmeyi yapılandırmak oldukça basittir. Üretim sorunlarınız varsa, bir telemetri sisteminin ve özel günlüklerin birleşimi, sorunları müşterilerinizin önemli bir sorunu haline gelmeden hızlı bir şekilde çözmenize yardımcı olur.

[Sonraki bölümde](transient-fault-handling.md) , araştırmanız gereken üretim sorunları haline gelmemesi için geçici hataların nasıl işleneceğini inceleyeceğiz.

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için aşağıdaki kaynaklara bakın.

Temel olarak telemetri ile ilgili belgeler:

- [Microsoft desenleri ve uygulamaları-Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). Bkz. Izleme ve Telemetri kılavuzu, hizmet ölçümü Kılavuzu, sistem durumu uç nokta Izleme düzeni ve çalışma zamanı yeniden yapılandırma düzeni.
- [Bulutta kuruş doldurma: Azure Web siteleri 'Nde yeni relik performansı Izleme etkinleştiriliyor](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx).
- [Azure Cloud Services 'de büyük ölçekli hizmetler tasarlamak Için En Iyi uygulamalar](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Simms ve Michael Thomassy ' i Işaretleyen Teknik İnceleme. Telemetri ve Tanılamalar bölümüne bakın.
- [Application Insights Ile yeni nesil geliştirme](https://msdn.microsoft.com/magazine/dn683794.aspx). MSDN Magazine makalesi.

Genellikle günlüğe kaydetme ile ilgili belgeler:

- [Anlamsal günlük uygulama bloğu (blok)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). NEIL Mackenzie, blok ile anlam günlüğe kaydetme durumunu gösterir.
- [Anlamsal günlük yapılandırılmış ve anlamlı Günlükler oluşturma](https://channel9.msdn.com/Events/Build/2013/3-336). Video Jülyen Dominguez, blok ile anlam günlüğe kaydetme durumunu gösterir.
- [EF6 SQL günlüğü – 1. Bölüm: basit günlük kaydı](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/). Arthur Vicranlılar, Entity Framework tarafından yürütülen sorguların EF 6 ' da nasıl günlüğe alınacağını gösterir.
- [Bir ASP.NET MVC uygulamasındaki Entity Framework Ile bağlantı dayanıklılığı ve komut yakalaşmayı](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). Dört bölümden oluşan bir öğretici serisinde, Entity Framework tarafından veritabanına gönderilen SQL komutlarının günlüğe kaydetmek için EF 6 komut yakatım özelliğinin nasıl kullanılacağını gösterir.
- [5,0 çağıran bilgi C# özniteliklerini kullanarak günlüğe kaydetmeyi geliştirme](http://www.dotnetcurry.com/showarticle.aspx?ID=972). Çağıran metodun adını sabit kodlamadan kolayca günlüğe kaydetme veya el ile almak için yansıma kullanma.

Temel olarak sorun giderme ile ilgili belgeler:

- [Azure sorunlarını ayıklama &amp; Web günlüğü](https://blogs.msdn.com/b/kwill/).
- [AzureTools: Azure Geliştirici desteği ekibi tarafından kullanılan tanılama yardımcı programı](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true). , Çok çeşitli tanılama ve izleme araçlarını indirmek ve çalıştırmak için bir Azure VM 'de kullanılabilen bir araç için indirme bağlantısı sağlar. Belirli bir sanal makinede bir sorunu tanılamanıza gerek duyduğunuzda faydalıdır.
- [Visual Studio 'yu kullanarak Azure App Service bir Web uygulamasının sorunlarını giderin](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio). System. Diagnostics izlemeyi ve uzaktan hata ayıklamayı kullanmaya başlamak için adım adım öğretici.

Videolar:

- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz bölümden oluşan seriler. , Microsoft Müşteri danışmanlık ekibi (CAT) deneyiminden gerçek müşterilerle çekilen hikayelerle, yüksek düzeyde kavramlar ve mimari ilkeleri çok erişilebilir ve ilginç bir şekilde sunar. Bölüm 4 ve 9, izleme ve telemetri hakkında. Bölüm 9, izleme hizmetleri MetricsHub, AppDynamics, yeni relik ve Pagerharcı 'e genel bakış içerir.
- [Büyük oluşturma: Azure müşterileri-Bölüm II 'den öğrenilen dersler](https://channel9.msdn.com/Events/Build/2012/3-030). Simms 'nin hata tasarlama ve her şeyi işaretleme hakkında işaret edin. Failsafe serisine benzer ancak daha fazla nasıl yapılır ayrıntılarına gider.

Kod örneği:

- [Azure 'Da bulut hizmeti temelleri](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Microsoft Azure müşteri danışmanlık ekibi tarafından oluşturulan örnek uygulama. Aşağıdaki makalelerde açıklandığı gibi telemetri ve günlüğe kaydetme uygulamalarını gösterir. Örnek, [NLog](http://nlog-project.org/)kullanarak uygulama günlüğünü uygular. İlgili belgeler için bkz. [telemetri ve günlüğe kaydetme hakkında dört TechNet wiki makalesi dizisi](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon).

> [!div class="step-by-step"]
> [Önceki](design-to-survive-failures.md)
> [İleri](transient-fault-handling.md)
