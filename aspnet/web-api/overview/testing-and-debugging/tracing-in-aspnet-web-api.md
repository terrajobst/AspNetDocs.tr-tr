---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2 ' de izleme | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'sinde izlemenin nasıl etkinleştirileceğini gösterir.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598555"
---
# <a name="tracing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de izleme

, [Mike te son](https://github.com/MikeWasson)

> Web tabanlı bir uygulamada hata ayıklamaya çalışırken, uygun bir izleme günlüğü kümesi için bir değiştirme yoktur. Bu öğreticide, ASP.NET Web API 'sinde izlemenin nasıl etkinleştirileceği gösterilmektedir. Bu özelliği, Web API çerçevesinin denetleyicinizi uyguladıktan önce ve sonra ne yaptığını izlemek için kullanabilirsiniz. Ayrıca, kendi kodunuzu izlemek için de kullanabilirsiniz.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
> - [Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (visual Studio 2015 ile de geçerlidir)
> - Web API 2
> - [Microsoft. AspNet. WebApi. Tracing](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>Web API 'de System. Diagnostics Izlemeyi etkinleştir

İlk olarak yeni bir ASP.NET Web uygulaması projesi oluşturacağız. Visual Studio 'da, **Dosya** menüsünden **Yeni** > **Proje**' yi seçin. **Şablonlar**, **Web**, **ASP.NET Web uygulaması**' nı seçin.

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

Web API 'SI proje şablonunu seçin.

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

**Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni ve ardından **paket yönetim konsolu**' nu seçin.

Paket Yöneticisi konsolu penceresinde aşağıdaki komutları yazın.

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

İlk komut en son Web API izleme paketini yüklüyor. Ayrıca çekirdek Web API paketlerini de güncelleştirir. İkinci komut, WebApi. WebHost paketini en son sürüme güncelleştirir.

> [!NOTE]
> Web API 'nin belirli bir sürümünü hedeflemek istiyorsanız, izleme paketini yüklerken-Version bayrağını kullanın.

WebApiConfig.cs dosyasını uygulama\_başlangıç klasöründe açın. **Register** yöntemine aşağıdaki kodu ekleyin.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

Bu kod, [Systemdiagnosticstracewriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) SıNıFıNı Web API ardışık düzenine ekler. **Systemdiagnosticstracewriter** sınıfı, izlemeleri [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)öğesine yazar.

İzlemeleri görmek için, uygulamayı hata ayıklayıcıda çalıştırın. Tarayıcıda `/api/values` adresine gidin.

![](tracing-in-aspnet-web-api/_static/image5.png)

Trace deyimleri, Visual Studio 'daki çıkış penceresine yazılır. ( **Görünüm** menüsünde **Çıkış**' ı seçin).

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

**Systemdiagnosticstracewriter** izlemeleri **System. Diagnostics. Trace**'e yazardığı için, ek izleme dinleyicilerini kaydedebilirsiniz; Örneğin, bir günlük dosyasına izlemeler yazmak için. İzleme yazarları hakkında daha fazla bilgi için MSDN 'deki [Izleme dinleyicileri](https://msdn.microsoft.com/library/4y5y10s7.aspx) konusuna bakın.

### <a name="configuring-systemdiagnosticstracewriter"></a>SystemDiagnosticsTraceWriter 'ı yapılandırma

Aşağıdaki kod, izleme yazıcısının nasıl yapılandırılacağını gösterir.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

Denetleyebilmeniz gereken iki ayar vardır:

- Isverbose: yanlışsa, her izleme en az bilgi içerir. True ise izlemeler daha fazla bilgi içerir.
- MinimumLevel: en düşük izleme düzeyini ayarlar. İzleme düzeyleri, sırasıyla hata ayıklama, bilgi, uyarı, hata ve önemli.

## <a name="adding-traces-to-your-web-api-application"></a>Web API uygulamanıza Izleme ekleme

İzleme yazıcısı eklemek, Web API işlem hattı tarafından oluşturulan izlemelere anında erişim sağlar. İzleme yazıcısını, kendi kodunuzu izlemek için de kullanabilirsiniz:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

İzleme yazıcısını almak için **HttpConfiguration. Services. GetTraceWriter**' ı çağırın. Denetleyiciden, bu yönteme **Apicontroller. Configuration** özelliği aracılığıyla erişilebilir.

Bir izleme yazmak için **ıstracewriter. Trace** yöntemini doğrudan çağırabilirsiniz, ancak [ıstracewriterextensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) sınıfı daha kolay olan bazı uzantı yöntemlerini tanımlar. Örneğin, yukarıda gösterilen **Info** yöntemi Izleme düzeyi **bilgiyle**bir izleme oluşturur.

## <a name="web-api-tracing-infrastructure"></a>Web API Izleme altyapısı

Bu bölümde, Web API 'SI için özel bir izleme yazıcısının nasıl yazılacağı açıklanmaktadır.

Microsoft. AspNet. WebApi. Tracing paketi, Web API 'sinde daha genel bir izleme altyapısının üzerine kurulmuştur. Microsoft. AspNet. WebApi. Tracing kullanmak yerine, [NLog](http://nlog-project.org/) veya [Log4net](http://logging.apache.org/log4net/)gibi başka bir izleme/günlüğe kaydetme kitaplığı da takabilirsiniz.

İzlemeleri toplamak için **ıstracewriter** arabirimini uygulayın. İşte basit bir örnek:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

**Istracewriter. Trace** yöntemi bir izleme oluşturur. Çağıran bir kategori ve izleme düzeyi belirtir. Kategori, Kullanıcı tanımlı herhangi bir dize olabilir. **İzleme** uygulamanız aşağıdakileri yapması gerekir:

1. Yeni bir izleme kaydı **oluşturun.** Bunu gösterildiği gibi istek, kategori ve İzleme düzeyiyle başlatın. Bu değerler, çağıran tarafından sağlanır.
2. *Traceaction* temsilcisini çağırın. Bu temsilcinin içinde çağıranın, izleme **ecord**öğesinin geri kalanını doldurması beklenir.
3. İstediğiniz günlüğekaydetme tekniğini kullanarak izleme kaydını yazın. Burada gösterilen örnek yalnızca **System. Diagnostics. Trace**öğesine çağrı yapılır.

## <a name="setting-the-trace-writer"></a>Izleme yazıcısını ayarlama

İzlemeyi etkinleştirmek için, Web API 'nizi **ıstracewriter** uygulamanızı kullanacak şekilde yapılandırmanız gerekir. Bunu, aşağıdaki kodda gösterildiği gibi **HttpConfiguration** nesnesi aracılığıyla yapabilirsiniz:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

Yalnızca bir izleme yazıcısı etkin olabilir. Web API 'SI varsayılan olarak hiçbir şey olmayan &quot;op&quot; izleyiciyi ayarlar. (&quot;-op&quot; izleyici, izleme kodunun bir izleme yazmadan önce izleme yazıcısının **null** olup olmadığını kontrol etmek zorunda kalmayacak şekilde bulunur.)

## <a name="how-web-api-tracing-works"></a>Web API Izlemenin çalışması

Web API 'de izleme bir *façlade* düzeni kullanır: izleme etkinleştirildiğinde, Web API 'si, istek işlem hattının çeşitli kısımlarını izleme çağrıları gerçekleştiren sınıflarla sarmalar.

Örneğin, bir denetleyici seçerken, işlem hattı **IHttpControllerSelector** arabirimini kullanır. İzleme etkinken, işlem hattı **IHttpControllerSelector** uygulayan ancak gerçek uygulamaya çağrı yapan bir sınıf ekler:

![Web API izleme façlade modelini kullanır.](tracing-in-aspnet-web-api/_static/image8.png)

Bu tasarımın avantajları şunlardır:

- İzleme yazıcısı eklemeyin, izleme bileşenleri örneklenemez ve hiçbir performans etkisi olmaz.
- **IHttpControllerSelector** gibi varsayılan Hizmetleri kendi özel uygulamanıza göre değiştirirseniz, izleme sarmalayıcı nesne tarafından yapıldığından izleme etkilenmez.

Varsayılan **ıstracemanager** hizmetini değiştirerek tüm Web API izleme çerçevesini kendi özel çerçevesinden da değiştirebilirsiniz:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

İzleme sisteminizi başlatmak için **ıstracemanager. Initialize** uygulamasını uygulayın. Bunun, Web API 'sinde yerleşik olarak bulunan tüm izleme kodları da dahil olmak üzere *Tüm Trace çerçevesinin* yerini aldığını unutmayın.
