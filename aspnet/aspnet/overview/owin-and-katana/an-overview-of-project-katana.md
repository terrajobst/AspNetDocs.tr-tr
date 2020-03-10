---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: Proje Katana öğesine genel bakış | Microsoft Docs
author: howarddierking
description: ASP.NET Framework on yıldan daha uzun süredir ve platform, sayaçsuz Web siteleri ve hizmetleri geliştirmeyi etkinleştirdi. Web uygulaması olarak...
ms.author: riande
ms.date: 08/30/2013
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: 1f28db822930cdfd2ebf4cf9bb27d173f4aa4201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617238"
---
# <a name="an-overview-of-project-katana"></a>Project Katana’ya Genel Bakış

[Howard Dierking](https://github.com/howarddierking)

> ASP.NET Framework on yıldan daha uzun süredir ve platform, sayaçsuz Web siteleri ve hizmetleri geliştirmeyi etkinleştirdi. Web uygulaması geliştirme stratejileri geliştirmekle birlikte, Framework ASP.NET MVC ve ASP.NET Web API gibi teknolojilerle adım adım gelişiyor. Web uygulaması geliştirme, bir sonraki evde bulut bilgi işlem dünyasına sahip olduğu için, proje [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) bileşeni ASP.NET uygulamalarına, esnek, taşınabilir, hafif ve daha iyi performans sağlar. proje [katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) bulutu ASP.NET uygulamalarınızı en iyi duruma getirir.

## <a name="why-katana--why-now"></a>Neden Katana: neden?

 Birinin bir geliştirici çerçevesini veya Son Kullanıcı ürününü ele almamasını ne olursa olsun, ürünün oluşturulması için temel alınan görüşmelerin ve ürünün ne şekilde oluşturulduğunu bilmenin bir parçası olduğunu anlamak önemlidir. ASP.NET ilk olarak, aklınızda iki müşteriyle oluşturulmuştur.   
  
**İlk müşteri grubu klasik ASP geliştiricilerinden oluşur.** Bu sırada ASP, biçimlendirme ve sunucu tarafı komut dosyası aracılığıyla dinamik, veri odaklı web siteleri ve uygulamalar oluşturmaya yönelik birincil teknolojiden biridir. ASP çalışma zamanı, temel alınan HTTP protokolünün ve Web sunucusunun temel yönlerini soyutlan ve bu tür oturum ve uygulama durumu yönetimi, önbellek, vb. için erişim sağlayan bir nesne kümesiyle sunucu tarafı betiği sağladı. Güçlü, klasik ASP uygulamaları, boyut ve karmaşıklık bakımından Grey olarak yönetilmesi için bir zorluk haline geldi. Bu, büyük olasılıkla kod ve biçimlendirmenin araya alınmasıyla sonuçlanan kod çoğaltmasıyla bağlanmış komut dosyası ortamlarında bulunan yapının olmamasından kaynaklanır. ASP.NET, klasik ASP 'nin güçlerinin bir kısmını ele alırken büyük bir süre içinde .NET Framework, Ayrıca sunucu tarafı programlama modelini koruyarak, nesne yönelimli diller tarafından sunulan kod kuruluşundan faydalanır. Klasik ASP geliştiricilerinin alışkın olduğu.

**ASP.NET için hedef müşterilerin ikinci grubu Windows iş uygulaması geliştiricileri idi.** Klasik ASP geliştiricilerinin aksine, daha fazla HTML biçimlendirmesi oluşturmak üzere HTML biçimlendirme ve kod yazmaya alışkın olan, WinForms geliştiricileri (VB6 geliştiricileri gibi), bir tuval ve zengin bir kullanıcı kümesi içeren tasarım zamanı deneyimine alışkın arabirim denetimleri. ASP.NET 'in ilk sürümü: "Web Forms" olarak da bilinen, sorunsuz bir geliştirici deneyimi oluşturmak için Kullanıcı arabirimi bileşenleri için sunucu tarafı olay modeliyle birlikte benzer bir tasarım zamanı deneyimi ve bir altyapı özellikleri kümesi (ViewState gibi) sağladı istemci ve sunucu tarafı programlama arasında. Web Forms, Web 'in, WinForms geliştiricilere tanıdık gelen durum bilgisi olan bir olay modeli altında durum bilgisiz bir şekilde gizledi.

### <a name="challenges-raised-by-the-historical-model"></a>Geçmiş modeli tarafından oluşturulan sorunlar

**Net sonuç, çok, özellik açısından zengin bir çalışma zamanı ve geliştirici programlama modelidir.** Bununla birlikte, bu özellik zenginleştirme, birkaç önemli zorluk ile karşılaşıyor. İlk olarak, Framework tek parçalı olarak, aynı System. Web. dll derlemesinde sıkı bir şekilde farklı işlev birimleri (örneğin, Web Forms çerçevesi olan çekirdek HTTP nesneleri) ile **tek parçalı**olarak çalışır. İkinci olarak, ASP.NET daha büyük .NET Framework bir parçası olarak eklenmiştir, bu da **yayınlar arasındaki sürenin yıl düzeninde olması** anlamına gelir. Bu, hızlı bir şekilde gelişen Web geliştirmede gerçekleşen tüm değişikliklerle çalışmaya devam etmesini ASP.NET için zorlaştırıyor. Son olarak, System. Web. dll ' nin kendisi belirli bir Web barındırma seçeneğine birkaç farklı yolla bağlanmış: Internet Information Services (IIS).

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>Evoluo adımları: ASP.NET MVC ve ASP.NET Web API 'SI

Web geliştirmede çok sayıda değişiklik oluyordu! Web uygulamaları, büyük çerçeveler yerine bir dizi küçük, odaklanmış bileşen olarak geliştirilmiştir. Bileşenlerin sayısı ve serbest bırakıldığı sıklık, çok daha hızlı bir hızda arttı. Web ile hızlanmasını sağlamak, çerçevelerin daha büyük ve daha zengin özelliklere sahip olmak yerine daha küçük, ayrılmış ve daha fazla odaklı olmasını gerektirdiğinden, **ASP.NET ekibi tek bir çerçeve yerine ASP.net 'i takılabilir bir Web bileşenleri ailesi olarak etkinleştirmek için birkaç bağımsız adım**attı.

İlk değişikliklerden biri, iyi bilinen model-görünüm-denetleyici (MVC) tasarım deseninin en çok popülerliği olan, Ruby on rayları gibi web geliştirme çerçeveleri sayesinde artmıştı. Bu Web uygulamaları oluşturma stili, ASP.NET için ilk satış noktalarından biri olan biçimlendirme ve iş mantığı ayrımı devam ederken geliştirici üzerinde uygulamanın biçimlendirmesi üzerinde daha fazla denetim vermiştir. Bu Web uygulaması geliştirme tarzının talebini karşılamak için, Microsoft, **bant dışı ASP.NET MVC** 'yi (.NET Framework dahil değil) geliştirerek daha sonra bir daha iyi konuma yerleştirme fırsatı aldı. ASP.NET MVC bağımsız bir indirme olarak yayımlandı. Bu, mühendisliğe daha önce mümkün olandan çok daha sık sunma esnekliği verdi.

Web uygulaması geliştirmede bir diğer büyük kaydırma, dinamik, sunucu tarafından oluşturulan Web sayfalarından, **Ajax istekleri aracılığıyla arka uç Web API 'leri ile**iletişim kuran istemci tarafı komut dosyası tarafından oluşturulan sayfanın dinamik bölümlerine statik ilk biçimlendirmeye kadar geçiydi. Bu mimari SHIFT, Web API 'Lerinin yüksemine ve ASP.NET Web API çerçevesinin geliştirilmesine yardımcı oldu. ASP.NET MVC 'de olduğu gibi, ASP.NET Web API 'sinin yayını daha fazla modüler bir çerçeve olarak ASP.NET daha fazla gelişmeye yönelik başka bir fırsat sağlamıştır. Mühendislik ekibi, fırsattan ve **yerleşik ASP.NET Web API 'sinin avantajlarından yararlanarak System. Web. dll ' de bulunan herhangi bir çekirdek çerçeve türünün bağımlılığı yoktur**. Bu iki şeyi etkinleştirdi: ilk olarak, ASP.NET Web API 'sinin tamamen kendi kendine bağımsız olarak gelişebileceği anlamına gelir (ve NuGet aracılığıyla teslim edildiği için hızlı bir şekilde yinelenemeye devam edebilir). İkincisi, System. Web. dll ' ye yönelik dış bağımlılıklar olmadığından ve bu nedenle, IIS 'de hiçbir bağımlılık olmadığından, ASP.NET Web API 'SI özel bir konakta (örneğin, bir konsol uygulaması, Windows hizmeti vb.) çalıştırma özelliğini içeriyordu.

### <a name="the-future-a-nimble-framework"></a>Gelecek: A Işlemlerimizin Framework

Framework bileşenlerini diğerinden ayırarak ve sonra NuGet üzerinde serbest bırakarak, çerçeveler artık **daha bağımsız ve daha hızlı bir şekilde yineleyebilir**. Ayrıca, Web API 'sinin kendi kendine barındırma yeteneğinin gücü ve esnekliği, Hizmetleri için **küçük ve hafif bir ana bilgisayar** isteyen geliştiricilere çok çekici bir şekilde sahiptir. Benzer şekilde, diğer çerçevelerin de bu özelliği istediği ve bu şekilde her bir Framework 'ün kendi temel adresinde kendi ana bilgisayar işleminde çalıştığı ve bağımsız olarak yönetilmek için gereken yeni bir zorluk ortaya çıkması. Modern bir Web uygulaması genellikle statik dosya hizmeti, dinamik sayfa oluşturma, Web API ve daha yeni gerçek zamanlı/anında iletme bildirimleri destekler. Bu hizmetlerin her birinin çalıştırılması ve ayrı olarak yönetilmesi gerekir.

Bir geliştiricinin birçok farklı bileşenden ve çerçevelerden bir uygulama oluşturup daha sonra bu uygulamayı destekleyen bir konakta çalıştırmasına imkan tanıyan tek bir barındırma soyutlaması gerekiyordu.

## <a name="the-open-web-interface-for-net-owin"></a>.NET için açık Web arabirimi (OWıN)

 Ruby topluluğundaki [rafa](http://rack.github.io/) göre elde edilen avantajlardan yararlanarak, .net Community 'nin birkaç üyesi, Web sunucuları ve çerçeve bileşenleri arasında bir soyutlama oluşturmak için ayarlanmıştır. OWıN soyutlaması için iki tasarım hedefi basittir ve diğer çerçeve türlerinde mümkün olan en az bağımlılığı gerçekleştirmesidir. Bu iki amaç sağlamaya yardımcı olur:

- Yeni bileşenler daha kolay geliştirilebilir ve tüketilebilir.
- Uygulamalar, konaklar ve potansiyel olarak tüm platformlar/işletim sistemleri arasında daha kolay bir şekilde eklenebilir.

Elde edilen soyutlama iki çekirdekli öğeden oluşur. İlki ortam sözlüğüdür. Bu veri yapısı, bir HTTP isteğini ve yanıtını işlemek için gereken tüm durumu ve ilgili sunucu durumunu saklamaktan sorumludur. Ortam sözlüğü aşağıdaki gibi tanımlanır:

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

Bir OWIN uyumlu Web sunucusu, ortam sözlüğünün bir HTTP isteği ve yanıtı için gövde akışları ve üst bilgi koleksiyonları gibi verilerle doldurulmasından sorumludur. Daha sonra, sözlüğü ek değerlerle doldurmak veya güncelleştirmek ve yanıt gövdesi akışına yazmak için uygulama veya çerçeve bileşenlerinin sorumluluğundadır.

Ortam sözlüğü için türü belirtmenin yanı sıra, OWıN belirtimi, temel sözlük anahtar değer çiftlerinin bir listesini tanımlar. Örneğin, aşağıdaki tabloda bir HTTP isteği için gereken sözlük anahtarları gösterilmektedir:

| Anahtar Adı | Değer açıklaması |
| --- | --- |
| `"owin.RequestBody"` | Varsa istek gövdesine sahip bir akış. Stream. null, istek gövdesi yoksa bir yer tutucu olarak kullanılabilir. [Istek gövdesine](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics)bakın. |
| `"owin.RequestHeaders"` | İstek üst bilgilerinin `IDictionary<string, string[]>`. Bkz. [üst bilgiler](http://owin.org/html/owin.html#3-3-headers). |
| `"owin.RequestMethod"` | İsteğin HTTP istek yöntemini içeren bir `string` (örneğin, `"GET"`, `"POST"`). |
| `"owin.RequestPath"` | İstek yolunu içeren bir `string`. Yol, uygulama temsilcisinin "köküne" göre olmalıdır; bkz. [yollar](http://owin.org/html/owin.html#5-3-paths). |
| `"owin.RequestPathBase"` | Uygulama temsilcisinin "köküne" karşılık gelen istek yolunun bölümünü içeren bir `string`; bkz. [yollar](http://owin.org/html/owin.html#5-3-paths). |
| `"owin.RequestProtocol"` | Protokol adı ve sürümünü içeren bir `string` (örn. `"HTTP/1.0"` veya `"HTTP/1.1"`). |
| `"owin.RequestQueryString"` | Önde gelen "?" olmadan HTTP istek URI 'sinin sorgu dizesi bileşenini içeren `string` (örn. `"foo=bar&baz=quux"`). Değer boş bir dize olabilir. |
| `"owin.RequestScheme"` | İstek için kullanılan URI şemasını içeren bir `string` (örneğin, `"http"`, `"https"`); bkz. [URI şeması](http://owin.org/html/owin.html#5-1-uri-scheme). |

OWIN 'ın ikinci anahtar öğesi uygulama temsilcisidir. Bu, bir OWıN uygulamasındaki tüm bileşenler arasında birincil arabirim görevi gören bir işlev imzasıdır. Uygulama temsilcisinin tanımı aşağıdaki gibidir:

`Func<IDictionary<string, object>, Task>;`

Daha sonra uygulama temsilcisi, işlevin ortam sözlüğünü girdi olarak kabul ettiği ve bir görev döndürdüğü Func temsilci türünün bir uygulamasıdır. Bu tasarım, geliştiriciler için çeşitli etkilere sahiptir:

- OWIN bileşenleri yazmak için gereken çok az sayıda tür bağımlılığı vardır. Bu, OWIN 'un erişilebilirliğini büyük ölçüde geliştiricilere yükseltir.
- Zaman uyumsuz tasarım, özellikle daha fazla g/ç yoğun işlemlerdeki bilgi işlem kaynaklarını işlemeye kadar verimli olmasını sağlar.
- Uygulama temsilcisi atomik bir yürütme birimidir ve ortam sözlüğü temsilci üzerinde bir parametre olarak yapıldığından, OWIN bileşenleri karmaşık HTTP işleme işlem hatları oluşturmak için kolayca birlikte zincirleme yapılabilir.

Uygulama perspektifinden, OWıN bir belirtimdir ([http://owin.org/html/owin.html](http://owin.org/html/owin.html)). Hedefi bir sonraki Web çerçevesi değil, Web çerçeveleri ve Web sunucularının nasıl etkileşim kurabileceğine ilişkin bir belirtim değil.

[Owın](http://owin.org/) veya [Katana](https://github.com/aspnet/AspNetKatana/wiki)'ı araştırdıysanız, [Owın NuGet paketini](http://nuget.org/packages/Owin) ve Owin. dll dosyasını da fark etmiş olabilirsiniz. Bu kitaplık, OWIN belirtiminin [4. bölümünde](http://owin.org/html/owin.html#4-application-startup) açıklanan başlangıç dizisini şekillendirir ve coleştirir. tek bir arabirim olan [ıappbuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs). OWıN sunucularını derlemek için gerekli olmasa da, [ıappbuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs) arabirimi somut bir başvuru noktası sağlar ve bu, Katana proje bileşenleri tarafından kullanılır.

## <a name="project-katana"></a>Proje Katana

Hem [Owin](http://owin.org/html/owin.html) belirtimi hem de *Owin. dll* , topluluk sahipliğinde ve topluluk açık kaynaklı çalışmalardır, [Katana](https://github.com/aspnet/AspNetKatana/wiki) proje, hala açık kaynak olan Owin bileşenleri kümesini temsil eder, Microsoft tarafından oluşturulup serbest bırakılır. Bu bileşenler, ana bilgisayarlar ve sunucular gibi altyapı bileşenlerinin yanı sıra, [SignalR](../../../signalr/index.md) ve [ASP.NET Web API](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md)gibi çerçeveler için kimlik doğrulama bileşenleri ve bağlamaları gibi işlevsel bileşenleri içerir. Proje aşağıdaki üç üst düzey hedefle sahiptir: 

- **Taşınabilir** – bileşenler kullanılabilir hale geldiğinde yeni bileşenleri kolayca yerine yenilerini yerleştiribilmelidir. Bu, çerçeveden sunucuya ve ana bilgisayara kadar tüm bileşen türlerini içerir. Bu hedefin etkili olması, Microsoft çerçeveleri üçüncü taraf sunucularında ve konaklarda çalışırken, üçüncü taraf çerçevelerin Microsoft sunucularında sorunsuz bir şekilde çalışmasını sağlamaktır.
- **Modüler/esnek**– varsayılan olarak açık olan çok sayıda çerçevenin aksine, Katana proje bileşenleri küçük ve odaklanmış olmalıdır ve uygulamada hangi bileşenlerin kullanılacağını belirlemede uygulama geliştiricisi üzerinde denetim sağlar.
- **Hafif/** performans ve ölçeklenebilir – bir çerçevenin geleneksel kavramının uygulama geliştiricisi tarafından açıkça eklenen küçük, odaklanmış bileşenlere bölünmesi sayesinde, sonuçta elde edilen bir katana uygulama daha az bilgi işlem kaynağı tüketebilir ve sonuç olarak diğer sunucu ve çerçeve türleriyle daha fazla yük işleyebilir. Uygulamanın gereksinimleri temel altyapıdan daha fazla özellik talep ettiği için, bunlar OWıN ardışık düzenine eklenebilir, ancak bu, uygulama geliştiricisi kapsamında açık bir karar olmalıdır. Ek olarak, alt düzey bileşenlerin substitutability, kullanılabilir hale geldiği anlamına gelir, bu uygulamaları bozmadan OWıN uygulamalarının performansını artırmak için yeni yüksek performanslı sunucuların sorunsuz bir şekilde tanıtılabilir.

## <a name="getting-started-with-katana-components"></a>Katana bileşenleriyle çalışmaya başlama

İlk kez sunulmasından sonra, bir Web sunucusunu yazıp çalıştırabileceği için, en kısa şekilde, insanların dikkatini çekecek olan [Node. js](http://nodejs.org/) çerçevesinin bir yönü. Katana hedefleri [Node. js](http://nodejs.org/)' nin hafif şekilde çerçevelediği takdirde, bu, katkı ana 'nın, geliştiricilerin ASP.NET Web uygulamaları geliştirmeye yönelik her şeyi oluşturmasını zorlamadan, bu verileri, tek bir deyişle [Node. js](http://nodejs.org/) ' nin (ve gibi çerçeveler) sağladığı avantajlardan haberdar ederek özetleyebilir. Bu deyimin doğru olması için, Katana proje ile çalışmaya başlamak, [Node. js](http://nodejs.org/)' nin doğası gereği aynı şekilde basittir.

## <a name="creating-hello-world"></a>"Merhaba Dünya!" oluşturuluyor

JavaScript ve .NET geliştirme arasındaki bir önemli farkı, bir derleyicinin varlığı (veya yokludır). Bu nedenle, bir basit Katana sunucu için başlangıç noktası bir Visual Studio projem. Ancak, en az proje türüyle başlayabiliriz: boş ASP.NET Web uygulaması.

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

Ardından, [Microsoft. Owin. Host. SystemWeb](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) NuGet paketini projeye yükleyeceğiz. Bu paket, ASP.NET istek ardışık düzeninde çalışan bir OWıN sunucusu sağlar. Bu, [NuGet galerisinde](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) bulunabilir ve Visual Studio Paket Yöneticisi iletişim kutusu ya da Paket Yöneticisi konsolu kullanılarak aşağıdaki komutla yüklenebilir:

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

`Microsoft.Owin.Host.SystemWeb` paketini yüklemek, birkaç ek paketi bağımlılıklar olarak yükler. Bu bağımlılıklardan biri, OWıN uygulamalarının geliştirilmesi için çeşitli yardımcı türler ve yöntemler sağlayan bir kitaplık olan `Microsoft.Owin`. Aşağıdaki "Hello World" sunucusunu hızlı bir şekilde yazmak için bu türleri kullanabiliriz.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

Bu çok basit Web sunucusu artık Visual Studio **F5** komutu kullanılarak çalıştırılabilir ve hata ayıklama için tam destek içerir.

## <a name="switching-hosts"></a>Konakları değiştirme

Varsayılan olarak, önceki "Hello World" örneği, IIS bağlamında System. Web kullanan ASP.NET istek ardışık düzeninde çalışır. Bu, kendi kendine bir OWıN ardışık düzeninin esneklik ve yeteneklerini, IIS 'nin genel olarak vadede sağladığı esneklikten faydalanabilir. Ancak, IIS tarafından sunulan avantajların gerekmediği ve istenen daha küçük, daha hafif bir ana bilgisayar için olduğu durumlar olabilir. Ne gerekir, daha sonra basit Web sunucunuzu IIS ve System. Web dışında çalıştırmak için?

Taşınabilirlik hedefini göstermek için, bir Web sunucusu konaktan bir komut satırı ana bilgisayarına geçiş yapmak için, yeni sunucu ve ana bilgisayar bağımlılıklarını projenin çıkış klasörüne eklemek ve ardından ana bilgisayarı başlatmak gerekir. Bu örnekte, Web sunucunuzu `OwinHost.exe` adlı bir katana konakta barındıracağız ve Katana HttpListener tabanlı sunucuyu kullanacaksınız. Diğer Katana bileşenlere benzer şekilde, bunlar aşağıdaki komutu kullanarak NuGet 'den elde edilir:

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

Daha sonra, komut satırından proje kök klasörüne gidebilir ve `OwinHost.exe` (ilgili NuGet paketinin Araçlar klasörüne yüklenmiş olan) çalıştırmanız yeterlidir. Varsayılan olarak, `OwinHost.exe` HttpListener tabanlı sunucuyu aramak için yapılandırılır ve ek bir yapılandırma gerekmez. `http://localhost:5000/` için bir Web tarayıcısında gezinmek, şimdi konsolundan çalıştırılan uygulamayı gösterir.

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Katana mimarisi

 Katana bileşen mimarisi, bir uygulamayı aşağıda gösterildiği gibi dört mantıksal katmana böler: *ana bilgisayar, sunucu, ara yazılım* ve *uygulama*. Bileşen mimarisi, bu katmanların uygulamalarının, uygulamanın yeniden derlenmesi gerekmeden birçok durumda kolayca yerine geçen bir şekilde katılabilmesini sağlayabilir.   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>Ana bilgisayar

 Konağın sorumludur:

- Temel alınan işlemi yönetme.
- Bir sunucu seçimine ve isteklerin işlenebileceği bir OWıN işlem hattının oluşturulmasını sağlayan iş akışını düzenleyin.

  Mevcut olduğunda, Katana tabanlı uygulamalar için 3 birincil barındırma seçeneği vardır:  
  
**IIS/ASP. net**: Standart HttpModule ve HttpHandler türlerini kullanma, owın ardışık düzenleri, ASP.NET istek akışının bir PARÇASı olarak IIS üzerinde çalışabilir. ASP.NET barındırma desteği, Microsoft. AspNet. Host. SystemWeb NuGet paketini bir Web uygulaması projesine yükleyerek etkinleştirilir. Ayrıca, IIS hem ana bilgisayar hem de sunucu olarak davrandığı için, OWıN sunucu/ana bilgisayar ayrımı bu NuGet paketinde bir bütün olarak belirlenir, yani SystemWeb ana bilgisayarı kullanılıyorsa bir geliştirici alternatif sunucu uygulamasını yerine geçemez.  
  
**Özel ana bilgisayar**: Katana bileşen paketi, bir geliştiricinin bir konsol uygulaması, Windows hizmeti vb. gibi kendi özel işleminde uygulamaları barındırmasını sağlar. Bu yetenek, Web API 'SI tarafından sunulan Self-Host özelliğine benzer. Aşağıdaki örnek Web API kodunun özel bir konağını göstermektedir:  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Katana uygulamaya yönelik Self-Host kurulumu benzerdir:

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

Web API 'si ile Katana konak örnekleri arasındaki bir önemli farkı, Web API yapılandırma kodunun Katana Self-Host örneğinde eksik olması gerektiğidir. Hem taşınabilirlik hem de bileşim sağlamak için, Katana, sunucuyu başlatan kodu istek işleme ardışık düzenini yapılandıran koddan ayırır. Web API 'sini yapılandıran kod, daha sonra WebApplication. Start içinde tür parametresi olarak belirtilen sınıf başlangıcında bulunur.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

Başlangıç sınıfı, makalenin ilerleyen kısımlarında daha ayrıntılı olarak ele alınacaktır. Ancak, bir katana Self-Host işlemini başlatmak için gereken kod, ASP.NET Web API Self-Host uygulamalarında, bugün kullanmakta olduğunuz koda benzer şekilde görünür.

**Owinhost. exe**: bazıları, Katana Web uygulamalarını çalıştırmak için özel bir işlem yazmak isteymekle çalışırken, bir sunucu başlatabilir ve uygulamalarını çalıştırabilecek önceden oluşturulmuş bir yürütülebilir dosya başlatmayı tercih eder. Bu senaryoda, Katana bileşen paketi `OwinHost.exe`içerir. Bir projenin kök dizininden çalıştırıldığında, bu yürütülebilir bir sunucu başlatır (varsayılan olarak HttpListener sunucusunu kullanır) ve kullanıcının başlangıç sınıfını bulmak ve çalıştırmak için kuralları kullanır. Daha ayrıntılı denetim için, çalıştırılabilir bir dizi ek komut satırı parametresi sağlar.

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>Sunucu

 Ana bilgisayar, uygulamanın çalıştırıldığı işlemin başlatılması ve bakımında sorumlu olsa da, sunucunun sorumluluğu bir ağ yuvası açmak, istekleri dinlemek ve Kullanıcı tarafından belirtilen OWIN bileşenleri işlem hattı aracılığıyla göndermektir (sizin tarafınızdan zaten fark görmüş olabilir, bu işlem hattı uygulama geliştiricisinin başlangıç sınıfında belirtilir). Şu anda, Katana proje iki sunucu uygulaması içerir: 

- **Microsoft. Owin. Host. SystemWeb**: daha önce belirtildiği gibi, ASP.NET ardışık DÜZENINDE bulunan IIS, hem konak hem de sunucu olarak davranır. Bu nedenle, bu barındırma seçeneğini seçerken IIS, işlem etkinleştirme ve HTTP isteklerini dinler gibi ana bilgisayar düzeyinde sorunları yönetir. ASP.NET Web uygulamaları için, istekleri ASP.NET işlem hattına gönderir. Katana SystemWeb ana makinesi, HTTP işlem hattı üzerinden akar ve Kullanıcı tarafından belirtilen OWıN ardışık düzeninde yollayarak istekleri ele almak için bir ASP.NET HttpModule ve HttpHandler kaydeder.
- **Microsoft. Owin. Host. HttpListener**: adı gösterildiği üzere bu Katana sunucu, bir yuva açmak ve istekleri geliştirici tarafından belirtilen bir owın ardışık düzenine göndermek Için .NET Framework HttpListener sınıfını kullanır. Bu, şu anda hem Katana Self-Host API 'SI hem de OwinHost. exe için varsayılan sunucu seçiminizdir.

## <a name="middlewareframework"></a>Ara yazılım/çerçeve

 Daha önce belirtildiği gibi, sunucu bir istemciden bir istek kabul ettiğinde, bunu geliştiricinin başlangıç kodu tarafından belirtilen bir işlem hattı ile geçirmekten sorumludur. Bu işlem hattı bileşenleri, ara yazılım olarak bilinir.  
 En temel düzeyde, bir OWIN ara yazılım bileşeninin, çağrılabilir olması için OWıN uygulama temsilcisini uygulaması gerekir.

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

Ancak, bir ara yazılım bileşenlerinin geliştirilmesini ve birleşimini basitleştirmek için, Katana, ara yazılım bileşenleri için el ile yapılan kuralları ve yardımcı türleri destekler. Bunların en yaygın sürümü `OwinMiddleware` sınıfıdır. Bu sınıf kullanılarak oluşturulan özel bir ara yazılım bileşeni, aşağıdakine benzer şekilde görünür: 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 Bu sınıf `OwinMiddleware`türetilir, ardışık düzendeki bir sonraki ara yazılımın bir örneğini bağımsız değişkenlerinden biri olarak kabul eden bir Oluşturucu uygular ve ardından bunu temel oluşturucuya geçirir. Ara yazılımı yapılandırmak için kullanılan ek bağımsız değişkenler, sonraki ara yazılım parametresinden sonra Oluşturucu parametreleri olarak da bildirilmiştir.   
  
Çalışma zamanında, ara yazılım geçersiz kılınan `Invoke` yöntemi aracılığıyla yürütülür. Bu yöntem `OwinContext`türünde tek bir bağımsız değişken alır. Bu bağlam nesnesi, daha önce açıklanan `Microsoft.Owin` NuGet paketi tarafından sağlanır ve istek, yanıt ve ortam sözlüğüne, bazı ek yardımcı türlerle birlikte kesin olarak yazılmış erişim sağlar.   
  
Ara yazılım sınıfı, uygulama başlangıç kodundaki OWıN ardışık düzenine aşağıdaki gibi kolayca eklenebilir:   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

Katana altyapı bir OWıN ara yazılım bileşenlerini bir işlem hattı oluşturduğundan ve bileşenlerin işlem hattına katılmak için uygulama temsilcisini desteklemesi gerektiğinden, ara yazılım bileşenleri basit günlükçülerin ASP.NET, Web API veya [SignalR](../../../signalr/index.md)gibi tüm çerçevelere kadar karmaşıklık halinde değişebilir. Örneğin, ASP.NET Web API 'sini önceki OWıN ardışık düzenine eklemek için aşağıdaki başlangıç kodunun eklenmesi gerekir:

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Katana altyapısı, yapılandırma yöntemindeki ıappbuilder nesnesine eklendikleri sıraya göre ara yazılım bileşenlerinin işlem hattını oluşturur. Bizim örneğimizde, Loggerara yazılımı, bu isteklerin sonunda nasıl işlendiği bağımsız olarak, işlem hattı üzerinden akan tüm istekleri işleyebilir. Bu, bir ara yazılım bileşeninin (örn. bir kimlik doğrulama bileşeni) birden çok bileşen ve çerçeve (ör. ASP.NET Web API 'SI, SignalR ve statik dosya sunucusu) içeren bir işlem hattı için istekleri işleyebildiği güçlü senaryolar sunar.
 
## <a name="applications"></a>Uygulamalar

Önceki örneklerde gösterildiği gibi, OWıN ve Katana proje yeni bir uygulama programlama modeli olarak düşünülmemelidir, ancak uygulama programlama modellerini ve çerçevelerini sunucu ve barındırma altyapısından ayırmak için bir soyutlama değil. Örneğin, Web API uygulamaları oluştururken, geliştirici çerçevesi, uygulamanın Katana projeden bileşenler kullanılarak OWıN ardışık düzeninde çalışıp çalışmadığını bağımsız olarak ASP.NET Web API çerçevesini kullanmaya devam edecektir. OWıN ile ilgili kodun uygulama geliştiricisi tarafından görülebileceği tek bir konum, geliştiricinin OWıN ardışık düzenini yerleştirmekte olduğu uygulama başlangıç kodu olacaktır. Başlangıç kodunda, geliştirici, genellikle gelen istekleri işleyecek her bir ara yazılım bileşeni için bir dizi UseXx ifadesi kaydeder. Bu deneyim, geçerli System. Web dünyasında HTTP modüllerini kaydetme ile aynı etkiye sahip olacaktır. Genellikle, ASP.NET Web API 'SI veya [SignalR](../../../signalr/index.md) gibi daha büyük bir Framework ara yazılımı, işlem hattının sonuna kaydedilir. Kimlik doğrulama veya önbelleğe alma gibi çapraz kesme ara yazılım bileşenleri genellikle işlem hattının sonuna doğru kaydedilir, böylece işlem hattında daha sonra kaydedilen tüm çerçeveler ve bileşenler için istekleri işleyirler. Ara yazılım bileşenlerinin birbirleriyle ve temel alınan altyapı bileşenlerinden bu şekilde ayrılması, bileşenlerin, genel sistemin kararlı kalmasını sağlarken farklı Velde gelişmesine olanak sağlar.

## <a name="components--nuget-packages"></a>Bileşenler – NuGet paketleri

Birçok geçerli kitaplık ve çerçeve gibi, Katana proje bileşenleri bir NuGet paketleri kümesi olarak dağıtılır. Yaklaşan sürüm 2,0 için, Katana paket bağımlılık grafiği aşağıdaki gibi görünür. (Daha büyük görünüm için görüntüye tıklayın.)

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

Katana projesindeki neredeyse her paket, Owın paketinde doğrudan veya dolaylı olarak bağlıdır. Bu, OWIN belirtiminin 4. bölümünde açıklanan uygulama başlatma sırasının somut bir uygulamasını sağlayan ıappbuilder arabirimini içeren paket olduğunu unutmayın. Ayrıca, paketlerin birçoğu, HTTP istekleri ve yanıtları ile çalışmaya yönelik bir dizi yardımcı türü sağlayan Microsoft. Owin 'a bağımlıdır. Paketin geri kalanı, barındırma altyapısı paketleri (sunucular veya konaklar) veya ara yazılım olarak sınıflandırılabilir. Katana proje dışındaki paketler ve bağımlılıklar turuncu olarak görüntülenir.

Katana 2,0 barındırma altyapısı hem SystemWeb hem de HttpListener tabanlı sunucuları, OwinHost. exe ' yi kullanarak OWıN uygulamalarını çalıştırmaya yönelik Owınhost paketini ve bir üzerinde kendi kendine barındırma uygulamaları için Microsoft. Owin. Hosting paketini içerir. özel ana bilgisayar (ör. konsol uygulaması, Windows hizmeti vb.)

Katana 2,0 için, ara yazılım bileşenleri temelde farklı kimlik doğrulama yöntemi sağlamaya odaklanılmıştır. Tanılama için bir ek ara yazılım bileşeni sağlanır ve bu, başlangıç ve hata sayfası desteğini sunar. OWIN, Microsoft ve üçüncü taraflar tarafından geliştirilen bir ara yazılım bileşenlerinin ekosistemi olan soyutlamadır.

## <a name="conclusion"></a>Sonuç

 En baştan, Katana Projenin hedefi oluşturmamıştır ve böylece geliştiricilerin henüz başka bir Web çerçevesini öğrenmelerine izin vermez. Bunun yerine, amaç .NET Web uygulaması geliştiricilerine daha önce mümkün olandan daha fazla seçenek sunmak için bir soyutlama oluşturmaktır. Normal bir Web uygulaması yığınının mantıksal katmanlarını değiştirilebilen bir bileşen kümesine bölerek, Katana proje, bu bileşenlere ilişkin her türlü bir fiyata yönelik olarak yığının tamamında bulunan bileşenlerin kullanımını sağlar. Katana soyutlamadaki tüm bileşenleri derleyerek, Katana çerçeveleri ve bunların üzerine inşa olan uygulamaların çeşitli farklı sunucular ve konaklar arasında taşınabilir olmasını sağlar. Katana, geliştiriciyi yığının denetimine yerleştirerek, geliştiricinin basit veya özellik açısından zengin Web yığınının nasıl olması gerektiği hakkında üstün seçim yapmalarını sağlar.  

## <a name="for-more-information-about-katana"></a>Katana hakkında daha fazla bilgi için

- GitHub 'daki Katana proje: [https://github.com/aspnet/AspNetKatana/](https://github.com/aspnet/AspNetKatana/).
- Video: [ASP.net Için Katana proje-OWIN](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET), Howard Dierking.

## <a name="acknowledgements"></a>Bildirimler

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/): (Twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) Rick, Microsoft Azure ve MVC üzerinde odaklanan bir kıdemli programlama yazdır.
- [Scott Hanselman](http://www.hanselman.com/blog/): (Twitter [@shanselman](https://twitter.com/shanselman) )
- [Jon Galloway](https://weblogs.asp.net/jgalloway/default.aspx): (Twitter [@jongalloway](https://twitter.com/jongalloway) )
