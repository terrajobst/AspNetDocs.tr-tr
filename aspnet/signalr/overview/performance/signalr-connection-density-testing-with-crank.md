---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: Crank ile SignalR bağlantı yoğunluğu testi | Microsoft Docs
author: bradygaster
description: Crank ile SignalR Bağlantı Yoğunluğu Testi
ms.author: bradyg
ms.date: 02/22/2015
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: 901e039fbb81651ed18d560c99745b7e7f716e01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558340"
---
# <a name="signalr-connection-density-testing-with-crank"></a>Crank ile SignalR Bağlantı Yoğunluğu Testi

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, bir uygulamayı birden çok sanal istemci ile test etmek için Crank aracının nasıl kullanılacağı açıklanır.

Uygulamanız barındırma ortamında (bir Azure Web rolü, IIS veya Owın kullanılarak şirket içinde barındırılan) çalışıyorsa, Crank aracını kullanarak uygulamanın yüksek düzeyde bağlantı yoğunluğu 'na yanıtını test edebilirsiniz. Barındırma ortamı bir Internet Information Services (IIS) sunucusu, bir Owın konağı veya bir Azure Web rolü olabilir. (Not: performans sayaçları Azure App Service Web Apps üzerinde kullanılamaz, bu nedenle bir bağlantı yoğunluğu testinizden performans verileri alınamaz.)

Bağlantı yoğunluğu, bir sunucuda kurulabilecek eşzamanlı TCP bağlantısı sayısını ifade eder. Her TCP bağlantısı kendi yükünü doğurur ve çok sayıda boştaki bağlantı açmak sonunda bellek sorunu oluşturur.

[SignalR codebase,](https://github.com/signalr/signalr) **Crank**adlı bir yük testi aracı içerir. Crank 'ın en son sürümü GitHub 'daki [Geliştirme dalında](https://github.com/SignalR/signalr/tree/dev) bulunabilir. SignalR codebase 'in dev dalının bir zip arşivini [buradan](https://github.com/SignalR/SignalR/archive/dev.zip)indirebilirsiniz.

Crank, sunucu donanımında mümkün olan toplam boşta bağlantı sayısını hesaplamak için sunucunun belleğini tamamen doygunluğu sağlamak üzere kullanılabilir. Alternatif olarak, belirli bir sayı veya belirli bir bellek eşiğine ulaşılana kadar bağlantıları düzenleyerek, sunucuyu belirli bir bellek baskısı altında test etmek için Crank ' ı da kullanabilirsiniz.

Sınama yaparken, kaynakların herhangi bir yarışmasını önlemek için uzak istemciler (örneğin, TCP bağlantıları ve bellek) kullanılması önemlidir. Sunucunun tam kapasitesine (bellek veya CPU) ulaşmasını engelleyebilen herhangi bir performans sorunlarına yol olmamasını sağlamak için istemci (ler) i izleyin. Sunucuyu tam olarak yüklemek için istemci sayısını artırmanız gerekebilir.

### <a name="running-a-connection-density-test"></a>Bağlantı yoğunluğu testi çalıştırma

Bu bölümde, bir SignalR uygulamasında bir bağlantı yoğunluğu testi çalıştırmak için gereken adımlar açıklanmaktadır.

1. [SignalR kod temelinin geliştirme dalını](https://github.com/SignalR/SignalR/archive/dev.zip)indirin ve derleyin. Bir komut isteminde &lt;proje dizini&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug. gidin
2. Uygulamanızı kendi hedeflenen barındırma ortamına dağıtın. Uygulamanızın kullandığı uç noktayı bir yere unutmayın; Örneğin, Başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md)oluşturulan uygulamada, uç nokta `http://<yourhost>:8080/signalr`.
3. Sunucuya [SignalR performans sayaçlarını](signalr-performance.md#perfcounters) yükler. Uygulamanız Azure üzerinde çalışıyorsa, bkz. [Azure Web rolünde SignalR performans sayaçlarını kullanma](using-signalr-performance-counters-in-an-azure-web-role.md).

Kod temeli indirip yapılandırdıktan sonra ana bilgisayarınızda yüklü performans sayaçlarını yükledikten sonra, `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` klasöründe Crank komut satırı aracı bulunur.

Crank aracı için kullanılabilen seçenekler şunlardır:

- **/?** : Yardım ekranını gösterir. Kullanılabilir seçenekler, **URL** parametresi atlanırsa de görüntülenir.
- **/URL**: SignalR BAĞLANTıLARıNıN URL 'si. Bu parametre zorunludur. Varsayılan eşlemeyi kullanan bir SignalR uygulaması için yol "/SignalR" ile sona acaktır.
- **/Transport**: kullanılan taşımanın adı. Varsayılan değer `auto`, kullanılabilir en iyi Protokolü seçmeyecektir. Seçenekler arasında `WebSockets`, `ServerSentEvents`ve `LongPolling` (`ForeverFrame`, Internet Explorer yerine .NET istemcisi kullanıldığından, Crank için bir seçenek değildir) bulunur. SignalR 'ın aktarımları nasıl seçtiği hakkında daha fazla bilgi için bkz. [aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).
- **/BatchSize**: her bir toplu işte eklenen istemci sayısı. Varsayılan değer 50 ' dir.
- **/Connectınterval**: bağlantı ekleme arasındaki milisaniye cinsinden Aralık. Varsayılan değer 500 ' dir.
- **/Connections**: uygulamayı yüklemek ve test etmek için kullanılan bağlantı sayısı. Varsayılan değer 100.000 ' dir.
- **/ConnectTimeout**: testi iptal etmeden önce saniye cinsinden zaman aşımı. Varsayılan değer 300 ' dir.
- **Minservermbayt**: ulaşmak için en düşük sunucu megabayt. Varsayılan değer 500 ' dir.
- **Sendbytes**: sunucuya bayt cinsinden gönderilen yükün boyutu. Varsayılan değer, 0'dur.
- **Sendınterval**: sunucuya iletiler arasındaki milisaniye cinsinden gecikme. Varsayılan değer 500 ' dir.
- **SendTimeout**: sunucuya iletiler için milisaniye olarak zaman aşımı. Varsayılan değer 300 ' dir.
- **Controllerurl**: bir istemcinin bir Denetleyici Hub 'ını barındıracağı URL. Varsayılan değer null (Controller Hub yoktur). Denetleyici Hub 'ı Crank oturumu başladığında başlatılır; Denetleyici Hub 'ı ve Crank arasında başka iletişim kurulamadı.
- **Numclients**: uygulamaya bağlanacak sanal istemci sayısı. Varsayılan değer bir.
- **Logfile**: test çalıştırması için logfile dosya adı. Varsayılan, `crank.csv` değeridir.
- **SampleInterval**: performans sayacı örnekleri arasındaki milisaniye cinsinden süre. Varsayılan değer 1000 ' dir.
- **Signalrınstance**: sunucudaki performans sayaçlarının örnek adı. Varsayılan değer istemci bağlantı durumunu kullanmaktır.

### <a name="example"></a>Örnek

Aşağıdaki komut, bağlantı noktası 8080 ' de, 100 bağlantıları kullanılarak "ControllerHub" adlı bir hub ile bağlantı noktası üzerinde bir uygulama barındıran `pfsignalr` adlı bir siteyi test edecektir.

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`
