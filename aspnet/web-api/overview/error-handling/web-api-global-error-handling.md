---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2-ASP.NET 4. x içinde genel hata Işleme
author: davidmatson
description: ASP.NET 4. x için ASP.NET Web API 2 ' deki genel hata işlemeye genel bakış.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 94f2d6d31d0b37f9bb0077e6258c70a2dfb1918d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457745"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de genel hata Işleme

, [David Matson](https://github.com/davidmatson), [Rick Anderson](https://twitter.com/RickAndMSFT)

Bu konu, ASP.NET 4. x için ASP.NET Web API 2 ' deki genel hata işlemeye genel bir bakış sağlar. Günümüzde, Web API 'sinde hataları küresel olarak günlüğe kaydetmek veya işlemek için kolay bir yol yoktur. İşlenmeyen bazı özel durumlar [özel durum filtreleri](exception-handling.md)aracılığıyla işlenebilir, ancak özel durum filtrelerinin işleyemediği bazı durumlar vardır. Örneğin:

1. Denetleyici oluşturucularından oluşturulan özel durumlar.
2. İleti işleyicilerinden oluşturulan özel durumlar.
3. Yönlendirme sırasında oluşturulan özel durumlar.
4. Yanıt içeriği serileştirme sırasında oluşturulan özel durumlar.

Bu özel durumları günlüğe kaydetmek ve işlemek için basit ve tutarlı bir yol sağlamak istiyoruz. 

Özel durumları işlemek için kullanabileceğiniz iki büyük durum vardır. bir hata yanıtı gönderebiliyoruz ve tüm yaptığımız durum, özel durumun günlüğe kaydedileceği durumdur. İkinci durum için bir örnek, akış yanıtı içeriğinin ortasında bir özel durum oluşturulduğunda oluşur; Bu durumda durum kodu, üst bilgiler ve kısmi içerik zaten kablo genelinde olduğundan yeni bir yanıt iletisi gönderilmesi çok geç olduğundan bağlantıyı durdurduk. Özel durum yeni bir yanıt iletisi oluşturmak için işlenemese de, özel durumu günlüğe kaydetmeyi destekliyoruz. Hata tespit ettiğimiz durumlarda, aşağıda gösterildiği gibi uygun bir hata yanıtı döndürebiliriz:

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>Mevcut seçenekler

[Özel durum filtrelerine](exception-handling.md)ek olarak, [ileti işleyicileri](../advanced/http-message-handlers.md) tüm 500 düzeyinde yanıtları gözlemlemek için bugün kullanılabilir, ancak bu yanıtlara işlem yapılması, özgün hata hakkında bağlam olmadığından zor olabilir. İleti işleyicileri Ayrıca, işleyebilecekleri servis talepleriyle ilgili özel durum filtreleriyle aynı sınırlamalara sahip olmalıdır. Web API 'sinin hata koşullarını yakalayan izleme altyapısı olsa da, izleme altyapısı tanılama amaçlıdır ve üretim ortamlarında çalışmak üzere tasarlanmamıştır veya uygun değildir. Genel özel durum işleme ve günlük kaydı, üretim sırasında çalışabilecek ve var olan izleme çözümlerine takılmış olan hizmetler olmalıdır (örneğin, [ELMAH](https://code.google.com/p/elmah/) ).

### <a name="solution-overview"></a>Çözüme genel bakış

 İşlenmemiş özel durumları günlüğe kaydetmek ve işlemek için iki yeni kullanıcı tarafından değiştirilebilen hizmet, [ıexceptiongünlükçü](../releases/whats-new-in-aspnet-web-api-21.md) ve ıexceptionhandler sağlıyoruz. Hizmetler, iki temel fark ile çok benzerdir:

1. Birden çok özel durum Logger kaydını ancak yalnızca tek bir özel durum işleyicisini kaydetmeyi destekliyoruz.
2. Bağlantıyı durdurmak üzere yaptığımız halde, her zaman özel durum Günlükçüler çağırılır. Özel durum işleyicileri yalnızca hangi yanıt iletisini gönderileceğini seçebildiğimiz zaman çağrılabilir.

Her iki hizmet de özel durumun algılandığı noktadan ilgili bilgileri içeren bir özel durum bağlamına erişim sağlar, özellikle [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), [httprequestcontext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), oluşturulan özel durum ve özel durum kaynağıdır (Ayrıntılar aşağıda verilmiştir).

### <a name="design-principles"></a>Tasarım İlkeleri

1. **Son değişiklik yok** Bu işlevsellik küçük bir yayına eklendiğinden, çözümü etkileyen önemli bir kısıtlama, sözleşmelerin veya davranışın tür olarak hiçbir değişiklik oluşturmamasından kaynaklanır. Bu kısıtlama, özel durumları 500 yanıtlarına dönüştürmek üzere mevcut catch blokları açısından yapmak istediğimiz bazı temizleme işlemleri için yok. Bu ek temizlik, sonraki büyük bir sürüm için düşünebileceğiniz bir şeydir. Bu sizin için önemliyse lütfen [ASP.NET Web API Kullanıcı sessiyle](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)oylayın.
2. **Web API yapıları ile tutarlılığı sağlama** Web API 'sinin filtre işlem hattı, bir eyleme özgü, denetleyiciye özgü veya genel kapsamda mantığı uygulama esnekliğiyle birlikte çapraz kesme sorunlarını işlemenin harika bir yoludur. Özel durum filtreleri dahil olmak üzere filtreler, genel kapsamda kayıtlı olduğunda bile her zaman eylem ve denetleyici bağlamlarına sahiptir. Bu sözleşme, filtreler için anlamlı hale getirir, ancak genel kapsamlı bir şekilde özel durum filtrelerinin, hiçbir eylem veya denetleyici bağlamı mevcut olmayan ileti işleyicilerinden özel durumlar gibi bazı özel durum işleme durumlarında iyi bir uyum olmayacağı anlamına gelir. Özel durum işleme için filtreler tarafından sağlanan esnek kapsamları kullanmak istiyoruz, hala özel durum filtreleri gerekir. Ancak, bir denetleyici bağlamı dışında özel durum işlememiz gerekiyorsa, tam genel hata işleme (denetleyici bağlamı ve eylem bağlamı kısıtlamaları olmadan bir şey) için ayrı bir yapı da gerekir.

### <a name="when-to-use"></a>Ne zaman kullanılır?

- Özel durum Günlükçüler, Web API 'SI tarafından yakalanan işlenmemiş özel durumu görmek için çözümdür.
- Özel durum işleyicileri, Web API tarafından yakalanan işlenmemiş özel durumlara yönelik tüm olası yanıtları özelleştirmeye yönelik çözümdür.
- Özel durum filtreleri, belirli bir eylem veya denetleyiciyle ilgili alt küme işlenmemiş özel durumları işlemeye yönelik en kolay çözümdür.

### <a name="service-details"></a>Hizmet Ayrıntıları

 Özel durum günlükçüsü ve işleyici hizmeti arabirimleri, ilgili bağlamlara sahip basit zaman uyumsuz yöntemlerdir: 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 Ayrıca, bu arabirimlerin her ikisi için de temel sınıflar sunuyoruz. Çekirdek (eşitleme veya zaman uyumsuz) yöntemlerinin geçersiz kılınması önerilen zamanlarda günlüğe kaydetmek veya işlemek için gereklidir. Günlük kaydı için `ExceptionLogger` temel sınıfı, çekirdek günlük yönteminin her bir özel durum için yalnızca bir kez çağrıldığından emin olur (daha sonra çağrı yığınını yayıp yeniden yakalansa bile). `ExceptionHandler` temel sınıfı, yalnızca çağrı yığınının en üstündeki özel durumlar için, eski iç içe geçmiş catch bloklarını yoksayarak çekirdek işleme yöntemini çağırır. (Bu temel sınıfların Basitleştirilmiş sürümleri aşağıdaki ekte bulunur.) Hem `IExceptionLogger` hem de `IExceptionHandler`, bir `ExceptionContext`aracılığıyla özel durum hakkında bilgi alır.

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

Çerçeve bir özel durum günlükçüsü veya bir özel durum işleyicisi çağırdığında, her zaman bir `Exception` ve `Request`sağlar. Birim testi haricinde, her zaman `RequestContext`de sağlar. Nadiren `ControllerContext` ve `ActionContext` (yalnızca özel durum filtreleri için catch bloğundan çağrılırken) sağlar. Daha seyrek bir `Response`(yalnızca yanıtı yazmaya çalışırken bazı IIS durumlarında) sağlar. Bu özelliklerden bazıları `null`, özel durum sınıfının üyelerine erişmeden önce `null` denetlemek için tüketiciye ait olduğunu unutmayın.`CatchBlock` , özel durumu hangi catch bloğunun gördüğünüzü belirten bir dizedir. Catch bloğu dizeleri aşağıdaki gibidir:

- HttpServer (Sendadsync yöntemi)
- HttpControllerDispatcher (Sendadsync yöntemi)
- HttpBatchHandler (Sendadsync yöntemi)
- IExceptionFilter (ApiController 'in ExecuteAsync içindeki özel durum filtresi işlem hattının işlenmesi)
- OWıN Konağı:

    - HttpMessageHandlerAdapter. BufferResponseContentAsync (Çıktıyı arabelleğe almak için)
    - HttpMessageHandlerAdapter. CopyResponseContentAsync (akış çıktısı için)
- Web ana bilgisayarı:

    - HttpControllerHandler.WriteBufferedResponseContentAsync (for buffering output)
    - HttpControllerHandler. WriteStreamedResponseContentAsync (akış çıktısı için)
    - HttpControllerHandler. WriteErrorResponseContentAsync (arabelleğe alınan çıkış modu altında hata kurtarmasında hatalar için)

Catch bloğu dizelerinin listesi statik salt okunur özellikler aracılığıyla da kullanılabilir. (Temel catch blok dizesi, statik Exceptioncatchblokları üzerinde yer alır; kalanı OWıN ve Web ana makinesi için bir statik sınıfta görünür.`IsTopLevelCatchBlock` Yalnızca çağrı yığınının en üstünde özel durumları işlemek için önerilen kalıbı takip etmek için yararlıdır. İç içe geçmiş bir catch bloğunun gerçekleştiği her yerde özel durumları 500 yanıtlara dönüştürmek yerine, bir özel durum işleyicisi, ana bilgisayar tarafından görülene kadar özel durumların yayılmasına izin verebilir.

`ExceptionContext`ek olarak, bir günlükçü tam `ExceptionLoggerContext`bir bilgi parçasını alır:

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

`CanBeHandled`ikinci özelliği, bir günlükçü 'nin işlenmemiş bir özel durumu belirlemesine izin verir. Bağlantı durdurulmak üzereyken ve yeni yanıt iletisi ***gönderilemezse,*** Günlükçüler çağrılır, ancak işleyici çağrılmaz ve Günlükçüler bu senaryoyu bu özellikten tanımlayabilir.

`ExceptionContext`ek olarak, işleyici özel durumu işlemek için tam `ExceptionHandlerContext` ayarlayabileceği bir daha fazla özellik alır:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

Bir özel durum işleyicisi, `Result` özelliğini bir eylem sonucuna (örneğin, bir [Exceptionresult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [ınternalservererrorresult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [statuscoderesult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)veya özel bir sonuç) ayarlayarak bir özel durum işlediğini gösterir. `Result` özelliği null ise, özel durum işlenmeyecektir ve özgün özel durum yeniden oluşturulur.

Çağrı yığınının en üstündeki özel durumlar için, yanıtın API çağıranları için uygun olduğundan emin olmak için ek bir adım sunuyoruz. Özel durum konağa yayırsa, çağıran, genellikle uygun bir API hata yanıtı değil, genellikle HTML olan veya başka bir ana bilgisayar tarafından sunulan yanıtın sarı ekranını görür. Bu durumlarda, sonuç null olmayan bir şekilde başlar ve yalnızca özel bir özel durum işleyicisi `null` (işlenmemiş) olarak geri ayarlanırsa özel durum konağa yayılır. Bu tür durumlarda `null` için `Result` ayarlama iki senaryo için yararlı olabilir:

1. Web API 'SI öncesinde/dışında kaydedilmiş özel durum işleme ara yazılımı ile OWıN barındırılan Web API 'SI.
2. Bir tarayıcı aracılığıyla yerel hata ayıklama, sarı ekranın, işlenmemiş bir özel durum için yararlı bir yanıt olması durumunda.

Hem özel durum Günlükçüler hem de özel durum işleyicileri için, günlükçü veya işleyicinin kendisi bir özel durum oluşturursa kurtarılacak hiçbir şey yapmayız. (Özel durum yaymaya izin verme dışında, daha iyi bir yaklaşım varsa, bu sayfanın en altında geri bildirim bırakın.) Özel durum Günlükçüler ve işleyiciler için sözleşme, özel durumların arayanlara yaymasına izin vermemelidir; Aksi takdirde, özel durum, genellikle ana bilgisayar için bir HTML hatasına (ASP gibi) neden olacak şekilde yayılır. NET 'in sarı ekran) istemciye geri gönderilmekte (genellikle JSON veya XML bekleniyor API çağıranları için tercih edilen seçenek değildir).

## <a name="examples"></a>Örnekler

### <a name="tracing-exception-logger"></a>İzleme özel durum günlükçüsü

Aşağıdaki özel durum günlükçüsü, yapılandırılmış Izleme kaynaklarına özel durum verileri gönderir (Visual Studio 'daki hata ayıklama çıktısı penceresi dahil).

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>Özel hata Iletisi özel durum Işleyicisi

Aşağıda, desteğe bağlanmaya yönelik bir e-posta adresi de dahil olmak üzere istemcilere özel bir hata yanıtı verilmiştir.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>Özel durum filtrelerini kaydetme

Projenizi oluşturmak için "ASP.NET MVC 4 Web uygulaması" proje şablonunu kullanırsanız, Web API yapılandırma kodunuzu *uygulama/_Start* klasörüne `WebApiConfig` sınıfına koyun:

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>Ek: temel sınıf ayrıntıları

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
