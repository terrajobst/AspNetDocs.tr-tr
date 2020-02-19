---
uid: mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
title: ASP.NET MVC 4 ' te zaman uyumsuz yöntemler kullanma | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ücretsiz bir ve içeren Web için Visual Studio Express 2012 kullanarak zaman uyumsuz bir ASP.NET MVC web uygulaması oluşturma hakkında temel bilgiler verilir.
ms.author: riande
ms.date: 06/06/2012
ms.assetid: a56572ba-81c3-47af-826d-941e9c4775ec
msc.legacyurl: /mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 15692b18fc112c4c6cce4d50a243a0e8d5fb52a4
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457758"
---
# <a name="using-asynchronous-methods-in-aspnet-mvc-4"></a>ASP.NET MVC 4'te Zaman Uyumsuz Yöntemler Kullanma

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan [Web için Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11)kullanarak zaman uyumsuz BIR ASP.NET MVC web uygulaması oluşturma hakkında temel bilgileri öğretir. [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)' i de kullanabilirsiniz.
> 
> Bu öğretici için GitHub 'da bir örnek verilmiştir [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)

[.Net 4,5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) birleşimi IÇINDEKI ASP.NET MVC 4 [Denetleyici](https://msdn.microsoft.com/library/system.web.mvc.controller(VS.108).aspx) sınıfı, [görev&lt;ActionResult&gt;](https://msdn.microsoft.com/library/dd321424(VS.110).aspx)türünde bir nesne döndüren zaman uyumsuz eylem yöntemleri yazmanızı sağlar. .NET Framework 4, [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) olarak adlandırılan bir zaman uyumsuz programlama kavramı sunmuştur ve ASP.NET MVC 4 [görevi](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)destekler. Görevler, **görev** türü ve [System. Threading. Tasks](https://msdn.microsoft.com/library/system.threading.tasks.aspx) ad alanındaki ilgili türler tarafından temsil edilir. .NET Framework 4,5, [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) nesneleriyle çalışmayı önceki zaman uyumsuz yaklaşımlardan çok daha az karmaşık olan [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ve [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcükleriyle bu zaman uyumsuz destek üzerinde oluşturulur. [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) anahtar sözcüğü, kod parçasının zaman uyumsuz olarak başka bir kod parçasına beklemesi gerektiğini belirten sözdizimsel bir toplu özelliktir. [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüğü, yöntemleri görev tabanlı zaman uyumsuz yöntemler olarak işaretlemek için kullanabileceğiniz bir ipucunu temsil eder. **Await**, **Async**ve **Task** nesnesinin birleşimi, .NET 4,5 'e zaman uyumsuz kod yazmanızı çok daha kolay hale getirir. Zaman uyumsuz yöntemlere yönelik yeni model *görev tabanlı zaman uyumsuz* model (**tap**) olarak adlandırılır. Bu öğreticide, [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ve [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüklerini ve [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) ad alanını kullanarak zaman uyumsuz programlama hakkında bazı benzerlik olduğunu varsaymaktadır.

[Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ve [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüklerini ve [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) ad alanını kullanma hakkında daha fazla bilgi için aşağıdaki başvurulara bakın.

- [Teknik İnceleme: .NET 'te asynchrony](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Zaman uyumsuz/await SSS](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio zaman uyumsuz programlama](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>Isteklerin Iş parçacığı havuzu tarafından nasıl Işlendiği

Web sunucusunda .NET Framework, ASP.NET isteklerine hizmet vermek için kullanılan iş parçacıklarının havuzunu tutar. Bir istek geldiğinde, bu isteği işlemek için havuzdan bir iş parçacığı gönderilir. İstek zaman uyumlu olarak işleniyorsa, istek işlenirken isteği işleyen iş parçacığı meşgul olur ve bu iş parçacığı başka bir isteğe hizmet edemez.   
  
İş parçacığı havuzu çok sayıda meşgul iş parçacığına uyum sağlayacak kadar büyük hale getirilbildiğinden bu bir sorun olmayabilir. Ancak, iş parçacığı havuzundaki iş parçacıklarının sayısı sınırlıdır (.NET 4,5 için varsayılan en yüksek 5.000 ' dir). Uzun süreli çok sayıda istek olan büyük uygulamalarda, kullanılabilir tüm iş parçacıkları meşgul olabilir. Bu koşul, iş parçacığı başlangıçadı olarak bilinir. Bu koşula ulaşıldığında, Web sunucusu istekleri sıralar. İstek sırası dolarsa, Web sunucusu istekleri HTTP 503 durumu (sunucu çok meşgul) ile reddeder. CLR iş parçacığı havuzunda yeni iş parçacığı kısıtlamalarıyla ilgili sınırlamalar vardır. Eşzamanlılık burstise (yani, Web siteniz çok fazla sayıda istek alabilir) ve yüksek gecikme süresine sahip arka uç çağrıları nedeniyle tüm kullanılabilir istek iş parçacıkları meşgul olur, sınırlı iş parçacığı ekleme oranı uygulamanızın yanıt vermesini çok kötü hale getirir. Ayrıca, iş parçacığı havuzuna eklenen her yeni iş parçacığının ek yükü vardır (1 MB yığın bellek gibi). Zaman uyumlu yöntemler kullanan bir Web uygulaması iş parçacığı havuzunun .NET 4,5 varsayılan en yüksek değeri olan 5 ' e kadar büyüdüğü yüksek gecikme süreli çağrılara hizmet verebilir zaman uyumsuz yöntemler ve yalnızca 50 iş parçacığı. Zaman uyumsuz iş yaparken her zaman bir iş parçacığı kullanmıyoruz. Örneğin, zaman uyumsuz bir Web hizmeti isteği yaptığınızda, ASP.NET **zaman uyumsuz** Yöntem çağrısı ve **await**arasında herhangi bir iş parçacığı kullanmaz. İş parçacığı havuzunun yüksek gecikme süresine sahip isteklere kullanımı, büyük bir bellek parmak izine ve sunucu donanımının kötü kullanımına neden olabilir.

## <a name="processing-asynchronous-requests"></a>Zaman uyumsuz Istekleri işleme

Başlangıçta çok sayıda eşzamanlı istek sunan veya bir bursty yüküne sahip olan bir Web uygulamasında (eşzamanlılık aniden arttığında), Web hizmeti çağrılarının zaman uyumsuz yapılması uygulamanın yanıt hızını arttırır. Zaman uyumsuz bir istek, zaman uyumlu bir istek olarak işlemek için aynı süreyi alır. İstek iki saniyelik bir Web hizmeti çağrısı yapıyorsa, istek zaman uyumlu veya zaman uyumsuz olarak yapılıp yapılmadıklarında iki saniye sürer. Ancak zaman uyumsuz bir çağrı sırasında, bir iş parçacığının, ilk isteğin tamamlanmasını beklediği sırada diğer isteklere yanıt vermemesi engellenmez. Bu nedenle, uzun süre çalışan işlemleri çağıran çok sayıda eşzamanlı istek olduğunda zaman uyumsuz istekler istek sıraya alma ve iş parçacığı havuzunun büyümesini önler.

## <a id="ChoosingSyncVasync"></a>Zaman uyumlu veya zaman uyumsuz eylem yöntemleri seçme

Bu bölümde, zaman uyumlu veya zaman uyumsuz eylem yöntemlerinin ne zaman kullanılacağı hakkındaki yönergeler listelenmiştir. Bunlar yalnızca kılavuzlardır; zaman uyumsuz yöntemlerin performansla yardım edilip edilmeyeceğini öğrenmek için her uygulamayı ayrı ayrı inceleyin.

Genel olarak, aşağıdaki koşullar için zaman uyumlu yöntemleri kullanın:

- İşlemler basit veya kısa çalışıyor.
- Basitlik, verimlilik açısından daha önemlidir.
- İşlemler, yoğun disk veya ağ yükü içeren işlemler yerine öncelikle CPU operasyonlardır. CPU 'ya bağlı işlemlerde zaman uyumsuz eylem yöntemlerinin kullanılması, hiçbir avantaj sağlamaz ve daha fazla yüke neden olur.

Genel olarak, aşağıdaki koşullar için zaman uyumsuz yöntemleri kullanın:

- Zaman uyumsuz yöntemler aracılığıyla tüketilen hizmetleri arıyorsanız ve .NET 4,5 veya üzeri bir sürümü kullanıyorsunuz.
- İşlemler, CPU ile bağlantılı olarak ağ bağlantılı veya g/ç-bağlantılı.
- Paralellik, kod basitliği dışında daha önemlidir.
- Kullanıcıların uzun süre çalışan bir isteği iptal etmelerini sağlayan bir mekanizma sağlamak istiyorsunuz.
- İş parçacıklarını anahtarlama avantajı, bağlam anahtarı maliyetini ortaya çıktı. Genel olarak, zaman uyumlu yöntem ASP.NET istek iş parçacığı üzerinde bekliyorsa bir yöntemi zaman uyumsuz yapmanız gerekir. Çağrıyı zaman uyumsuz yaparak, ASP.NET istek iş parçacığı, Web hizmeti isteğinin tamamlanmasını beklerken hiçbir iş yapılmaz.
- Test, engelleme işlemlerinin site performansı açısından bir performans sorunu olduğunu ve IIS 'nin bu engelleme çağrıları için zaman uyumsuz yöntemleri kullanarak daha fazla istek hizmet verebilir olduğunu gösterir.

İndirilebilir örnek, zaman uyumsuz eylem yöntemlerinin etkin bir şekilde nasıl kullanılacağını gösterir. Belirtilen örnek, .NET 4,5 kullanılarak ASP.NET MVC 4 ' te zaman uyumsuz programlama basit bir gösterimi sağlamak üzere tasarlanmıştır. Örnek, ASP.NET MVC 'de zaman uyumsuz programlama için başvuru mimarisi olmak üzere tasarlanmamıştır. Örnek program, görevi çağıran [ASP.NET Web API](../../../web-api/index.md) yöntemlerini çağırır. uzun süre çalışan Web hizmeti çağrılarına benzetim yapmak için [gecikme](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) . Çoğu üretim uygulaması, zaman uyumsuz eylem yöntemlerinin kullanımı için bu tür açık avantajları göstermez.   
  
Birkaç uygulama tüm eylem yöntemlerinin zaman uyumsuz olmasını gerektirir. Genellikle, birkaç zaman uyumlu eylem yönteminin zaman uyumsuz yöntemlere dönüştürülmesi, gereken iş miktarı için en iyi verimlilik artışı sağlar.

## <a id="SampleApp"></a>Örnek uygulama

Örnek uygulamayı [GitHub](https://github.com/) sitesindeki [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET) indirebilirsiniz. Depo üç projeden oluşur:

- *Mvc4Async*: Bu öğreticide kullanılan kodu IÇEREN ASP.NET MVC 4 projesi. **WebAPIpgw** HIZMETINE Web API çağrıları yapar.
- *WebAPIpgw*: `Products, Gizmos and Widgets` denetleyicilerini uygulayan ASP.NET MVC 4 Web API projesi. *WebAppAsync* projesi ve *Mvc4Async* projesi için verileri sağlar.
- *WebAppAsync*: ASP.NET Web Forms projesi başka bir öğreticide kullanılır.

## <a id="GizmosSynch"></a>Şeyler Synchronous ACTION yöntemi

 Aşağıdaki kod, bir şeyler listesini göstermek için kullanılan zaman uyumlu `Gizmos` eylem yöntemini gösterir. (Bu makale için, Gizmo kurgusal bir makine aygıtıdır.) 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample1.cs)]

Aşağıdaki kod, Gizmo hizmetinin `GetGizmos` yöntemini gösterir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample2.cs)]

`GizmoService GetGizmos` yöntemi bir URI 'yi bir ASP.NET Web API HTTP hizmetine geçirir ve bu, şeyler verilerinin bir listesini döndürür. *WebAPIpgw* projesi, Web API `gizmos, widget` ve `product` denetleyicilerinin uygulamasını içerir.  
Aşağıdaki görüntüde örnek projeden şeyler görünümü gösterilmektedir.

![Şeyler](using-asynchronous-methods-in-aspnet-mvc-4/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>Zaman uyumsuz şeyler Action yöntemi oluşturma

Örnek, zaman uyumsuz programlama için gereken karmaşık dönüştürmeleri sürdürmekten önce derleyicinin sorumlu olmasını sağlamak için yeni [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ve [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) anahtar sözcüklerini (.NET 4,5 ve Visual Studio 2012 ' de kullanılabilir) kullanır. Derleyici, zaman uyumlu denetim akış yapılarını kullanarak C#kod yazmanızı sağlar ve derleyici, iş parçacıklarını engellemeyi önlemek için geri çağırmaları kullanmak için gereken dönüştürmeleri otomatik olarak uygular.

Aşağıdaki kod, zaman uyumlu `Gizmos` yöntemi ve `GizmosAsync` zaman uyumsuz yöntemi gösterir. Tarayıcınız [HTML 5 `<mark>` öğesini](http://www.w3.org/wiki/HTML/Elements/mark)destekliyorsa, `GizmosAsync` değişiklikleri sarı vurgulamada görürsünüz.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample3.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample4.cs?highlight=1,3,5)]

 `GizmosAsync` zaman uyumsuz olarak izin vermek için aşağıdaki değişiklikler uygulandı.

- Yöntemi [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüğüyle işaretlenir, bu da derleyiciye gövdenin parçaları için geri çağrılar oluşturmasını ve döndürülen bir `Task<ActionResult>` otomatik olarak oluşturmasını söyler.
- &quot;zaman uyumsuz&quot; metot adına eklendi. "Async" eklenmesi gerekli değildir, ancak zaman uyumsuz yöntemler yazılırken kuralıdır.
- Dönüş türü, `ActionResult` `Task<ActionResult>`olarak değiştirildi. `Task<ActionResult>` dönüş türü, devam eden çalışmayı temsil eder ve zaman uyumsuz işlemin tamamlanmasını beklemek için bir tanıtıcı ile metodun çağıranlarını sağlar. Bu durumda, çağıran Web hizmetidir. `Task<ActionResult>`, `ActionResult.` sonucuyla devam eden işi temsil eder
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) anahtar sözcüğü Web hizmeti çağrısına uygulandı.
- Zaman uyumsuz Web hizmeti API 'SI çağrıldı (`GetGizmosAsync`).

`GetGizmosAsync` yönteminin içinde başka bir zaman uyumsuz yöntem `GetGizmosAsync` çağırılır. `GetGizmosAsync` hemen, veriler kullanılabilir olduğunda sonunda tamamlanacak bir `Task<List<Gizmo>>` döndürür. Gizmo verilerine sahip olana kadar başka bir şey yapmak istemediğiniz için, kod görevi bekler ( **await** anahtar sözcüğünü kullanarak). **Await** anahtar sözcüğünü yalnızca **Async** anahtar sözcüğüyle açıklama eklenen yöntemlerde kullanabilirsiniz.

**Await** anahtar sözcüğü, görev tamamlanana kadar iş parçacığını engellemez. Görevin geri kalanını görevde geri çağırma olarak imzalar ve hemen döndürür. Beklenen görev sonunda tamamlandığında, bu geri aramayı çağırır ve bu nedenle, yöntemin hemen kapandığı yerde yürütmeye devam eder. [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ve [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüklerini ve [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) ad alanını kullanma hakkında daha fazla bilgi için bkz. [Async References](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async).

Aşağıdaki kod, `GetGizmos` ve `GetGizmosAsync` yöntemlerini göstermektedir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample5.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample6.cs?highlight=1,4-8)]

 Zaman uyumsuz değişiklikler, yukarıdaki **GizmosAsync** yapılan değişikliklerle benzerdir. 

- Yöntem imzasına [zaman uyumsuz](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) anahtar sözcüğüyle açıklama eklendi, dönüş türü `Task<List<Gizmo>>`olarak değiştirildi ve *zaman uyumsuz* Yöntem adına eklenmiş.
- , [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) sınıfı yerine zaman uyumsuz [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) sınıfı kullanılır.
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) anahtar sözcüğü [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) zaman uyumsuz yöntemlerine uygulandı.

Aşağıdaki görüntüde zaman uyumsuz Gizmo görünümü gösterilmektedir.

![async](using-asynchronous-methods-in-aspnet-mvc-4/_static/image2.png)

Şeyler verilerinin tarayıcılar sunumu, zaman uyumlu çağrı tarafından oluşturulan görünümle aynıdır. Tek fark, zaman uyumsuz sürümdür ağır yüklerin altında daha performanslı olabilir.

## <a id="Parallel"></a>Paralel olarak birden çok Işlem gerçekleştirme

Zaman uyumsuz eylem yöntemlerinin, bir eylemin birkaç bağımsız işlem gerçekleştirmesi gerektiğinde zaman uyumlu yöntemlerle önemli bir avantajı vardır. Belirtilen örnekte, zaman uyumlu Yöntem `PWG`(ürünler, pencere öğeleri ve şeyler için), ürünlerin, pencere öğelerinin ve şeyler 'in bir listesini almak için üç Web hizmeti çağrısının sonuçlarını görüntüler. Bu hizmetleri sağlayan [ASP.NET Web API](../../../web-api/index.md) projesi, görevi kullanır [.](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) gecikme veya yavaş ağ çağrılarının benzetimini yapmak için gecikme. Gecikme 500 milisaniyeye ayarlandığında, zaman uyumsuz `PWGasync` yöntemi, zaman uyumlu `PWG` sürümü 1.500 milisaniyeye göre daha fazla 500 milisaniyelik sürer. Zaman uyumlu `PWG` yöntemi aşağıdaki kodda gösterilmiştir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample7.cs)]

Zaman uyumsuz `PWGasync` yöntemi aşağıdaki kodda gösterilmiştir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample8.cs?highlight=1,3,12)]

Aşağıdaki görüntüde, **Pwgasync** yönteminden döndürülen görünüm gösterilmektedir.

![pwgAsync](using-asynchronous-methods-in-aspnet-mvc-4/_static/image3.png)

## <a id="CancelToken"></a>Iptal belirteci kullanma

`Task<ActionResult>`döndüren zaman uyumsuz eylem yöntemleri iptal edilir ve bu, [AsyncTimeout](https://msdn.microsoft.com/library/system.web.mvc.asynctimeoutattribute(VS.108).aspx) özniteliğiyle birlikte sağlandığında bir [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) parametresi alırlar. Aşağıdaki kod, 150 milisaniye zaman aşımı ile `GizmosCancelAsync` yöntemini gösterir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample9.cs?highlight=1-3,5,10)]

Aşağıdaki kod, [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) parametresini alan GetGizmosAsync aşırı yüklemesini gösterir.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample10.cs)]

Belirtilen örnek uygulamada, *Iptal belirteci demo* bağlantısını seçtiğinizde `GizmosCancelAsync` yöntemi çağrılıyordu ve zaman uyumsuz çağrının iptali gösterilmektedir.

## <a id="ServerConfig"></a>Yüksek eşzamanlılık/yüksek gecikmeli Web hizmeti çağrıları için sunucu yapılandırması

Zaman uyumsuz bir Web uygulamasının avantajlarını gerçekleştirmek için, varsayılan sunucu yapılandırmasında bazı değişiklikler yapmanız gerekebilir. Zaman uyumsuz Web uygulamanızı yapılandırırken ve stres testi yaparken aşağıdakileri aklınızda bulundurun.

- Windows 7, Windows Vista ve tüm Windows istemci işletim sistemlerinde en fazla 10 eşzamanlı istek vardır. Yüksek yük altında zaman uyumsuz yöntemlerin avantajlarını görmek için bir Windows Server işletim sistemi gerekir.
- .NET 4,5 ' i yükseltilmiş bir komut isteminden IIS ile kaydedin:  
  %windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet\_regııs-ı  
  Bkz [. asp.NET IIS Kayıt Aracı (Aspnet\_regııs. exe)](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- [Http. sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) kuyruk sınırını 1.000 varsayılan değerinden 5.000 ' e artırmanız gerekebilir. Ayar çok düşükse, http 503 durumu ile [http. sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) Red isteklerini görebilirsiniz. HTTP. sys kuyruk sınırını değiştirmek için:

    - IIS Yöneticisi 'ni açın ve uygulama havuzları bölmesine gidin.
    - Hedef uygulama havuzuna sağ tıklayın ve **Gelişmiş ayarlar**' ı seçin.  
        ![gelişmiş](using-asynchronous-methods-in-aspnet-mvc-4/_static/image4.png)
    - **Gelişmiş ayarlar** Iletişim kutusunda *sıra uzunluğu değerini* 1.000 5.000 olarak değiştirin.  
        ![kuyruğu uzunluğu](using-asynchronous-methods-in-aspnet-mvc-4/_static/image5.png)  
  
  Yukarıdaki görüntülerde, uygulama havuzu .NET 4,5 kullanıyor olsa da, .NET Framework 'ün v 4.0 olarak listelendiğini göz önünde bulunur. Bu tutarsızlığı anlamak için aşağıdakilere bakın:

    - [.NET sürüm oluşturma ve Çoklu hedefleme-.NET 4,5, .NET 4,0 için yerinde bir yükseltmektedir](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
    - [IIS uygulamasını veya AppPool 'ı 2,0 yerine ASP.NET 3,5 kullanacak şekilde ayarlama](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
    - [.NET Framework Sürümleri ve Bağımlılıkları](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)
- Uygulamanız HTTP üzerinden bir arka uçta iletişim kurmak için Web Hizmetleri veya System.NET kullanıyorsa, [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) öğesini artırmanız gerekebilir. ASP.NET uygulamaları için bu, otomatik yapılandırma özelliği tarafından CPU sayısının 12 katı ile sınırlıdır. Yani, bir dört proc üzerinde en fazla 12 \* 4 = 48 bir IP uç noktasına eşzamanlı bağlantı sağlayabilirsiniz. Bu, [Otomatik](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)olarak bağlı olduğundan, bir ASP.NET uygulamasında `maxconnection` artırmanın en kolay yolu, [System .net. ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) ' i *global. asax* dosyasındaki from `Application_Start` yönteminde Program aracılığıyla ayarlamaya yönelik bir yöntemdir. Örnek için bkz. örnek indirme.
- .NET 4,5 ' de, [maxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) için 5000 varsayılan değer iyi olmalıdır.
