---
uid: web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
title: ASP.NET 4,5 'de zaman uyumsuz yöntemler kullanma | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ücretsiz olarak bulunan Web için Visual Studio Express 2012 kullanarak zaman uyumsuz bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgiler verilir...
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a585c9a2-7c8e-478b-9706-90f3739c50d1
msc.legacyurl: /web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 7abc3d7acc60d7d868958f2a313bc408f96c95a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78625197"
---
# <a name="using-asynchronous-methods-in-aspnet-45"></a>ASP.NET 4.5 Sürümünde Zaman Uyumsuz Metotlar Kullanma

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticide, ücretsiz bir Microsoft Visual Studio sürümü olan [Web için Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11)' i kullanarak zaman uyumsuz bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgiler verilir. [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)' i de kullanabilirsiniz. Aşağıdaki bölümler Bu öğreticiye dahil edilmiştir.
> 
> - [Isteklerin Iş parçacığı havuzu tarafından nasıl Işlendiği](#HowRequestsProcessedByTP)
> - [Zaman uyumlu veya zaman uyumsuz yöntemler seçme](#ChoosingSyncVasync)
> - [Örnek uygulama](#SampleApp)
> - [Şeyler zaman uyumlu sayfası](#GizmosSynch)
> - [Zaman uyumsuz şeyler sayfası oluşturma](#CreatingAsynchGizmos)
> - [Paralel olarak birden çok Işlem gerçekleştirme](#Parallel)
> - [Iptal belirteci kullanma](#CancelToken)
> - [Yüksek eşzamanlılık/yüksek gecikmeli Web hizmeti çağrıları için sunucu yapılandırması](#ServerConfig)
> 
> Bu öğretici için bir örnek aşağıda verilmiştir:  
> [GitHub](https://github.com/) sitesinde [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/) .

ASP.NET 4,5 Web sayfaları, [.net 4,5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) ' de, [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)türünde bir nesne döndüren zaman uyumsuz yöntemleri kaydetmenizi sağlar. .NET Framework 4, [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) olarak adlandırılan bir zaman uyumsuz programlama kavramı sunmuştur ve ASP.NET 4,5 [görevi](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)destekler. Görevler, **görev** türü ve [System. Threading. Tasks](https://msdn.microsoft.com/library/system.threading.tasks.aspx) ad alanındaki ilgili türler tarafından temsil edilir. .NET Framework 4,5, [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) nesneleriyle çalışmayı önceki zaman uyumsuz yaklaşımlardan çok daha az karmaşık olan [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ve [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcükleriyle bu zaman uyumsuz destek üzerinde oluşturulur. [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) anahtar sözcüğü, kod parçasının zaman uyumsuz olarak başka bir kod parçasına beklemesi gerektiğini belirten sözdizimsel bir toplu özelliktir. [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüğü, yöntemleri görev tabanlı zaman uyumsuz yöntemler olarak işaretlemek için kullanabileceğiniz bir ipucunu temsil eder. **Await**, **Async**ve **Task** nesnesinin birleşimi, .NET 4,5 'e zaman uyumsuz kod yazmanızı çok daha kolay hale getirir. Zaman uyumsuz yöntemlere yönelik yeni model *görev tabanlı zaman uyumsuz* model (**tap**) olarak adlandırılır. Bu öğreticide, [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ve [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüklerini ve [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) ad alanını kullanarak zaman uyumsuz programlama hakkında bazı benzerlik olduğunu varsaymaktadır.

[Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ve [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüklerini ve [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) ad alanını kullanma hakkında daha fazla bilgi için aşağıdaki başvurulara bakın.

- [Teknik İnceleme: .NET 'te asynchrony](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Zaman uyumsuz/await SSS](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio zaman uyumsuz programlama](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>Isteklerin Iş parçacığı havuzu tarafından nasıl Işlendiği

Web sunucusunda .NET Framework, ASP.NET isteklerine hizmet vermek için kullanılan iş parçacıklarının havuzunu tutar. Bir istek geldiğinde, bu isteği işlemek için havuzdan bir iş parçacığı gönderilir. İstek zaman uyumlu olarak işleniyorsa, istek işlenirken isteği işleyen iş parçacığı meşgul olur ve bu iş parçacığı başka bir isteğe hizmet edemez.   
  
İş parçacığı havuzu çok sayıda meşgul iş parçacığına uyum sağlayacak kadar büyük hale getirilbildiğinden bu bir sorun olmayabilir. Ancak, iş parçacığı havuzundaki iş parçacıklarının sayısı sınırlıdır (.NET 4,5 için varsayılan en yüksek 5.000 ' dir). Uzun süreli çok sayıda istek olan büyük uygulamalarda, kullanılabilir tüm iş parçacıkları meşgul olabilir. Bu koşul, iş parçacığı başlangıçadı olarak bilinir. Bu koşula ulaşıldığında, Web sunucusu istekleri sıralar. İstek sırası dolarsa, Web sunucusu istekleri HTTP 503 durumu (sunucu çok meşgul) ile reddeder. CLR iş parçacığı havuzunda yeni iş parçacığı kısıtlamalarıyla ilgili sınırlamalar vardır. Eşzamanlılık burstise (yani, Web siteniz çok fazla sayıda istek alabilir) ve yüksek gecikme süresine sahip arka uç çağrıları nedeniyle tüm kullanılabilir istek iş parçacıkları meşgul olur, sınırlı iş parçacığı ekleme oranı uygulamanızın yanıt vermesini çok kötü hale getirir. Ayrıca, iş parçacığı havuzuna eklenen her yeni iş parçacığının ek yükü vardır (1 MB yığın bellek gibi). Zaman uyumlu yöntemler kullanan bir Web uygulaması iş parçacığı havuzunun .NET 4,5 varsayılan en yüksek değeri olan 5 ' e kadar büyüdüğü yüksek gecikme süreli çağrılara hizmet verebilir zaman uyumsuz yöntemler ve yalnızca 50 iş parçacığı. Zaman uyumsuz iş yaparken her zaman bir iş parçacığı kullanmıyoruz. Örneğin, zaman uyumsuz bir Web hizmeti isteği yaptığınızda, ASP.NET **zaman uyumsuz** Yöntem çağrısı ve **await**arasında herhangi bir iş parçacığı kullanmaz. İş parçacığı havuzunun yüksek gecikme süresine sahip isteklere kullanımı, büyük bir bellek parmak izine ve sunucu donanımının kötü kullanımına neden olabilir.

## <a name="processing-asynchronous-requests"></a>Zaman uyumsuz Istekleri işleme

Başlangıçta çok sayıda eşzamanlı istek olduğunu veya bir bursty yüküne sahip olan Web uygulamalarında (eşzamanlılık aniden ani artışlar), Web hizmeti zaman uyumsuz olarak çağrılar uygulamanızın yanıt hızını artırır. Zaman uyumsuz bir istek, zaman uyumlu bir istek olarak işlemek için aynı süreyi alır. Örneğin, bir istek iki saniyelik bir Web hizmeti çağrısı yapıyorsa, istek zaman uyumlu veya zaman uyumsuz olarak yapılıp yapılmadıklarında iki saniye sürer. Ancak, zaman uyumsuz bir çağrı sırasında, bir iş parçacığının, ilk isteğin tamamlanmasını beklediği sırada diğer isteklere yanıt vermemesi engellenmez. Bu nedenle, uzun süre çalışan işlemleri çağıran çok sayıda eşzamanlı istek olduğunda zaman uyumsuz istekler istek sıraya alma ve iş parçacığı havuzunun büyümesini önler.

## <a id="ChoosingSyncVasync"></a>Zaman uyumlu veya zaman uyumsuz yöntemler seçme

Bu bölümde, zaman uyumlu veya zaman uyumsuz yöntemlerin ne zaman kullanılacağı hakkında yönergeler listelenir. Bunlar yalnızca kılavuzlardır; zaman uyumsuz yöntemlerin performansla yardım edilip edilmeyeceğini öğrenmek için her uygulamayı ayrı ayrı inceleyin.

Genel olarak, aşağıdaki koşullar için zaman uyumlu yöntemleri kullanın:

- İşlemler basit veya kısa çalışıyor.
- Basitlik, verimlilik açısından daha önemlidir.
- İşlemler, yoğun disk veya ağ yükü içeren işlemler yerine öncelikle CPU operasyonlardır. CPU 'ya bağlı işlemlerde zaman uyumsuz yöntemlerin kullanılması, hiçbir avantaj sağlamaz ve daha fazla yüke neden olur.

Genel olarak, aşağıdaki koşullar için zaman uyumsuz yöntemleri kullanın:

- Zaman uyumsuz yöntemler aracılığıyla tüketilen hizmetleri arıyorsanız ve .NET 4,5 veya üzeri bir sürümü kullanıyorsunuz.
- İşlemler, CPU ile bağlantılı olarak ağ bağlantılı veya g/ç-bağlantılı.
- Paralellik, kod basitliği dışında daha önemlidir.
- Kullanıcıların uzun süre çalışan bir isteği iptal etmelerini sağlayan bir mekanizma sağlamak istiyorsunuz.
- İş parçacıklarını anahtarlama avantajı, bağlam anahtarı maliyetini ortaya çıktı. Genel olarak, zaman uyumlu yöntemi ASP.NET istek iş parçacığını engelliyorsa zaman uyumsuz olarak bir yöntem yapmanız gerekir. Çağrıyı zaman uyumsuz yaparak, ASP.NET istek iş parçacığı, Web hizmeti isteğinin tamamlanmasını beklerken hiçbir iş yapmamasını engellenmemiş.
- Test, engelleme işlemlerinin site performansı açısından bir performans sorunu olduğunu ve IIS 'nin bu engelleme çağrıları için zaman uyumsuz yöntemleri kullanarak daha fazla istek hizmet verebilir olduğunu gösterir.

  İndirilebilir örnek, zaman uyumsuz yöntemlerin etkin bir şekilde nasıl kullanılacağını gösterir. Belirtilen örnek, ASP.NET 4,5 ' de zaman uyumsuz programlama için basit bir gösteri sağlamak üzere tasarlanmıştır. Örnek, ASP.NET içinde zaman uyumsuz programlama için bir başvuru mimarisi olmak üzere tasarlanmamıştır. Örnek program, görevi çağıran [ASP.NET Web API](../../../web-api/index.md) yöntemlerini çağırır. uzun süre çalışan Web hizmeti çağrılarına benzetim yapmak için [gecikme](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) . Çoğu üretim uygulaması, zaman uyumsuz yöntemlerin kullanımı için bu tür açık avantajları göstermez.   
  
Birkaç uygulama tüm yöntemlerin zaman uyumsuz olmasını gerektirir. Genellikle, birkaç zaman uyumlu yöntemi zaman uyumsuz yöntemlere dönüştürmek, gereken iş miktarı için en iyi verimlilik artışı sağlar.

## <a id="SampleApp"></a>Örnek uygulama

Örnek uygulamayı [GitHub](https://github.com/) sitesindeki [https://github.com/RickAndMSFT/Async-ASP.NET](https://github.com/RickAndMSFT/Async-ASP.NET) indirebilirsiniz. Depo üç projeden oluşur:

- *WebAppAsync*: Web API **WebAPIpwg** hizmetini tüketen ASP.NET Web Forms projesi. Bu öğreticinin çoğu kodu bu projeden oluşur.
- *WebAPIpgw*: `Products, Gizmos and Widgets` denetleyicilerini uygulayan ASP.NET MVC 4 Web API projesi. *WebAppAsync* projesi ve *Mvc4Async* projesi için verileri sağlar.
- *Mvc4Async*: başka bir öğreticide kullanılan kodu IÇEREN ASP.NET MVC 4 projesi. **WebAPIpwg** HIZMETINE Web API çağrıları yapar.

## <a id="GizmosSynch"></a>Şeyler zaman uyumlu sayfası

 Aşağıdaki kod, bir şeyler listesini göstermek için kullanılan `Page_Load` zaman uyumlu yöntemini gösterir. (Bu makale için, Gizmo kurgusal bir makine aygıtıdır.) 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample1.cs)]

Aşağıdaki kod, Gizmo hizmetinin `GetGizmos` yöntemini gösterir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample2.cs)]

`GizmoService GetGizmos` yöntemi bir URI 'yi bir ASP.NET Web API HTTP hizmetine geçirir ve bu, şeyler verilerinin bir listesini döndürür. *WebAPIpgw* projesi, Web API `gizmos, widget` ve `product` denetleyicilerinin uygulamasını içerir.  
Aşağıdaki görüntüde örnek projeden şeyler sayfası gösterilmektedir.

![Şeyler](using-asynchronous-methods-in-aspnet-45/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>Zaman uyumsuz şeyler sayfası oluşturma

Örnek, zaman uyumsuz programlama için gereken karmaşık dönüştürmeleri sürdürmekten önce derleyicinin sorumlu olmasını sağlamak için yeni [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ve [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) anahtar sözcüklerini (.NET 4,5 ve Visual Studio 2012 ' de kullanılabilir) kullanır. Derleyici, zaman uyumlu denetim akış yapılarını kullanarak C#kod yazmanızı sağlar ve derleyici, iş parçacıklarını engellemeyi önlemek için geri çağırmaları kullanmak için gereken dönüştürmeleri otomatik olarak uygular.

ASP.NET zaman uyumsuz sayfaları, `Async` özniteliği "true" olarak ayarlanmış [sayfa](https://msdn.microsoft.com/library/ydy4x04a.aspx) yönergesini içermelidir. Aşağıdaki kod, *GizmosAsync. aspx* sayfası için `Async` özniteliği "true" olarak ayarlanan [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) yönergesini gösterir.

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample3.aspx?highlight=1)]

Aşağıdaki kod `Gizmos` zaman uyumlu `Page_Load` yöntemini ve `GizmosAsync` zaman uyumsuz sayfasını gösterir. Tarayıcınız [HTML 5 &lt;mark&gt; öğesini](http://www.w3.org/wiki/HTML/Elements/mark)destekliyorsa, `GizmosAsync` değişiklikleri sarı vurgulamada görürsünüz.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample4.cs)]

Zaman uyumsuz sürüm:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample5.cs?highlight=3,6-7,9,11)]

 `GizmosAsync` sayfanın zaman uyumsuz olmasını sağlamak için aşağıdaki değişiklikler uygulandı.

- [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) yönergesinin `Async` özniteliği "true" olarak ayarlanmış olmalıdır.
- `RegisterAsyncTask` yöntemi, zaman uyumsuz olarak çalışan kodu içeren zaman uyumsuz bir görevi kaydetmek için kullanılır.
- Yeni `GetGizmosSvcAsync` yöntemi [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüğüyle işaretlenir, bu da derleyiciye gövdenin parçaları için geri çağrılar oluşturmasını ve döndürülen bir `Task` otomatik olarak oluşturmasını söyler.
- &quot;zaman uyumsuz&quot; zaman uyumsuz metot adına eklendi. "Async" eklenmesi gerekli değildir, ancak zaman uyumsuz yöntemler yazılırken kuralıdır.
- Yeni `GetGizmosSvcAsync` yönteminin dönüş türü `Task`. `Task` dönüş türü, devam eden çalışmayı temsil eder ve zaman uyumsuz işlemin tamamlanmasını beklemek için bir tanıtıcı ile metodun çağıranlarını sağlar.
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) anahtar sözcüğü Web hizmeti çağrısına uygulandı.
- Zaman uyumsuz Web hizmeti API 'SI çağrıldı (`GetGizmosAsync`).

`GetGizmosSvcAsync` yönteminin içinde başka bir zaman uyumsuz yöntem `GetGizmosAsync` çağırılır. `GetGizmosAsync` hemen, veriler kullanılabilir olduğunda sonunda tamamlanacak bir `Task<List<Gizmo>>` döndürür. Gizmo verilerine sahip olana kadar başka bir şey yapmak istemediğiniz için, kod görevi bekler ( **await** anahtar sözcüğünü kullanarak). **Await** anahtar sözcüğünü yalnızca **Async** anahtar sözcüğüyle açıklama eklenen yöntemlerde kullanabilirsiniz.

**Await** anahtar sözcüğü, görev tamamlanana kadar iş parçacığını engellemez. Görevin geri kalanını görevde geri çağırma olarak imzalar ve hemen döndürür. Beklenen görev sonunda tamamlandığında, bu geri aramayı çağırır ve bu nedenle, yöntemin hemen kapandığı yerde yürütmeye devam eder. [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ve [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüklerini ve [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) ad alanını kullanma hakkında daha fazla bilgi için bkz. [Async References](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async).

Aşağıdaki kod, `GetGizmos` ve `GetGizmosAsync` yöntemlerini göstermektedir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample6.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample7.cs?highlight=1,4-8)]

 Zaman uyumsuz değişiklikler, yukarıdaki **GizmosAsync** yapılan değişikliklerle benzerdir. 

- Yöntem imzasına [zaman uyumsuz](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüğüyle açıklama eklendi, dönüş türü `Task<List<Gizmo>>`olarak değiştirildi ve *zaman uyumsuz* Yöntem adına eklenmiş.
- Zaman uyumsuz [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) sınıfı, zaman uyumlu [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) sınıfı yerine kullanılır.
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) anahtar sözcüğü [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)[GetAsync](https://msdn.microsoft.com/library/hh158944(VS.110).aspx) zaman uyumsuz metoduna uygulandı.

Aşağıdaki görüntüde zaman uyumsuz Gizmo görünümü gösterilmektedir.

![async](using-asynchronous-methods-in-aspnet-45/_static/image2.png)

Şeyler verilerinin tarayıcılar sunumu, zaman uyumlu çağrı tarafından oluşturulan görünümle aynıdır. Tek fark, zaman uyumsuz sürümdür ağır yüklerin altında daha performanslı olabilir.

## <a name="registerasynctask-notes"></a>RegisterAsyncTask notları

`RegisterAsyncTask` ile kullanıma alınan Yöntemler, [PreRender](https://msdn.microsoft.com/library/ms178472.aspx)'dan hemen sonra çalışacaktır. Ayrıca, aşağıdaki kodda gösterildiği gibi, zaman uyumsuz void sayfa olaylarını doğrudan de kullanabilirsiniz:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample8.cs)]

Zaman uyumsuz void olaylardaki downsıde, geliştiricilerin artık olaylar yürütülürken tam denetime sahip olmayacaktır. Örneğin, hem. aspx hem de bir. Ana `Page_Load` olaylarını tanımlar ve bunlardan biri veya her ikisi zaman uyumsuzdur, yürütme sırası garanti edilemez. Olay işleyicileri (örneğin `async void Button_Click`) için aynı ındeary sırası geçerli değildir. Çoğu geliştirici için kabul edilebilir olması gerekir, ancak yürütme sırası üzerinde tam denetim gerektiren, yalnızca bir görev nesnesi döndüren yöntemleri kullanan `RegisterAsyncTask` gibi API 'Leri kullanmalıdır.

## <a id="Parallel"></a>Paralel olarak birden çok Işlem gerçekleştirme

Zaman uyumsuz yöntemlerin bazı bağımsız işlemler gerçekleştirmesi gerektiğinde zaman uyumlu yöntemler üzerinde önemli bir avantajı vardır. Belirtilen örnekteki zaman uyumlu sayfa *PWG. aspx*(ürünler, pencere öğeleri ve şeyler için), ürünlerin, pencere öğelerinin ve şeyler 'in bir listesini almak için üç Web hizmeti çağrısının sonuçlarını görüntüler. Bu hizmetleri sağlayan [ASP.NET Web API](../../../web-api/index.md) projesi, görevi kullanır [.](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) gecikme veya yavaş ağ çağrılarının benzetimini yapmak için gecikme. Gecikme 500 milisaniyeye ayarlandığında, zaman uyumsuz *Pwgasync. aspx* sayfasında, zaman uyumlu `PWG` sürümü 1.500 milisaniyeye göre daha fazla 500 milisaniyelik sürer. Zaman uyumlu *PWG. aspx* sayfası aşağıdaki kodda gösterilmiştir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample9.cs)]

Arka plandaki zaman uyumsuz `PWGasync` kodu aşağıda gösterilmiştir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample10.cs?highlight=5,11,21)]

Aşağıdaki görüntüde, zaman uyumsuz *Pwgasync. aspx* sayfasından döndürülen görünüm gösterilmektedir.

![](using-asynchronous-methods-in-aspnet-45/_static/image3.png)

## <a id="CancelToken"></a>Iptal belirteci kullanma

`Task`döndüren zaman uyumsuz yöntemler, [sayfa](https://msdn.microsoft.com/library/ydy4x04a.aspx) yönergesinin `AsyncTimeout` özniteliğiyle birlikte sağlandığında bir [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) parametresi alırlar. Aşağıdaki kod, saniye olarak zaman aşımı olan *GizmosCancelAsync. aspx* sayfasını gösterir.

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample11.aspx?highlight=1)]

Aşağıdaki kod *GizmosCancelAsync.aspx.cs* dosyasını gösterir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample12.cs?highlight=6,9)]

Belirtilen örnek uygulamada, *GizmosCancelAsync* bağlantısının seçilmesi, *GizmosCancelAsync. aspx* sayfasını çağırır ve zaman uyumsuz çağrının iptalini (zaman aşımına göre) gösterir. Gecikme süresi rastgele bir aralık dahilinde olduğundan, zaman aşımı hata iletisini almak için sayfayı birkaç kez yenilemeniz gerekebilir.

## <a id="ServerConfig"></a>Yüksek eşzamanlılık/yüksek gecikmeli Web hizmeti çağrıları için sunucu yapılandırması

Zaman uyumsuz bir Web uygulamasının avantajlarını gerçekleştirmek için, varsayılan sunucu yapılandırmasında bazı değişiklikler yapmanız gerekebilir. Zaman uyumsuz Web uygulamanızı yapılandırırken ve stres testi yaparken aşağıdakileri aklınızda bulundurun.

- Windows 7, Windows Vista, Windows 8 ve tüm Windows istemci işletim sistemlerinde en fazla 10 eşzamanlı istek vardır. Yüksek yük altında zaman uyumsuz yöntemlerin avantajlarını görmek için bir Windows Server işletim sistemi gerekir.
- Aşağıdaki komutu kullanarak, yükseltilmiş bir komut isteminden .NET 4,5 'yi IIS ile kaydedin:  
  %windir%\Microsoft.NET\Framework64 \v4.0.30319\aspnet\_regııs-ı  
  Bkz [. asp.NET IIS Kayıt Aracı (Aspnet\_regııs. exe)](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- [Http. sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) kuyruk sınırını 1.000 varsayılan değerinden 5.000 ' e artırmanız gerekebilir. Ayar çok düşükse, http 503 durumu ile [http. sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) Red isteklerini görebilirsiniz. HTTP. sys kuyruk sınırını değiştirmek için:

    - IIS Yöneticisi 'ni açın ve uygulama havuzları bölmesine gidin.
    - Hedef uygulama havuzuna sağ tıklayın ve **Gelişmiş ayarlar**' ı seçin.  
        ![gelişmiş](using-asynchronous-methods-in-aspnet-45/_static/image4.png)
    - **Gelişmiş ayarlar** Iletişim kutusunda *sıra uzunluğu değerini* 1.000 5.000 olarak değiştirin.  
        ![kuyruğu uzunluğu](using-asynchronous-methods-in-aspnet-45/_static/image5.png)  
  
  Yukarıdaki görüntülerde, uygulama havuzu .NET 4,5 kullanıyor olsa da, .NET Framework 'ün v 4.0 olarak listelendiğini göz önünde bulunur. Bu tutarsızlığı anlamak için aşağıdakilere bakın:

- [.NET sürüm oluşturma ve Çoklu hedefleme-.NET 4,5, .NET 4,0 için yerinde bir yükseltmektedir](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
- [IIS uygulamasını veya AppPool 'ı 2,0 yerine ASP.NET 3,5 kullanacak şekilde ayarlama](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
- [.NET Framework Sürümleri ve Bağımlılıkları](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)

- Uygulamanız HTTP üzerinden bir arka uçta iletişim kurmak için Web Hizmetleri veya System.NET kullanıyorsa, [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) öğesini artırmanız gerekebilir. ASP.NET uygulamaları için bu, otomatik yapılandırma özelliği tarafından CPU sayısının 12 katı ile sınırlıdır. Yani, bir dört proc üzerinde en fazla 12 \* 4 = 48 bir IP uç noktasına eşzamanlı bağlantı sağlayabilirsiniz. Bu, [Otomatik](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)olarak bağlı olduğundan, bir ASP.NET uygulamasında `maxconnection` artırmanın en kolay yolu, [System .net. ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) ' i *global. asax* dosyasındaki from `Application_Start` yönteminde Program aracılığıyla ayarlamaya yönelik bir yöntemdir. Örnek için bkz. örnek indirme.
- .NET 4,5 ' de, [maxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) için 5000 varsayılan değer iyi olmalıdır.

## <a name="contributors"></a>Katkıda Bulunanlar

- [Levi Broick](http://stackoverflow.com/users/59641/levi)
- [Tom Dykstra](http://www.bing.com/search?q=site%3Aasp.net+%22Tom+Dykstra%22+-forums.asp.net&amp;qs=n&amp;form=QBRE&amp;pq=site%3Aasp.net+%22tom+dykstra%22+-forums.asp.net&amp;sc=8-42&amp;sp=-1&amp;sk=)
- [Atacan Solson](http://bradwilson.typepad.com/)
- [HongMei Ge](https://blogs.msdn.com/b/hongmeig/)
