---
uid: signalr/overview/getting-started/supported-platforms
title: Desteklenen platformlar | Microsoft Docs
author: bradygaster
description: Bu makalede, SignalR tarafından hangi istemcilerin ve sunucuların desteklendiği açıklanır.
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558634"
---
# <a name="supported-platforms"></a>Desteklenen Platformlar

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, SignalR tarafından hangi istemcilerin ve sunucuların desteklendiği açıklanır. 
> 
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
> 
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

SignalR çeşitli sunucu ve istemci yapılandırmalarında desteklenir. Ayrıca, her taşıma seçeneğinin kendi gereksinimleri vardır; bir taşımanın sistem gereksinimleri kullanılabilir değilse, SignalR diğer aktarımlara normal şekilde yük devretecektir. SignalR 'nin desteklediği taşıtlar hakkında daha fazla bilgi için bkz. [aktarımlar ve Fallyedekler](introduction-to-signalr.md#transports).

## <a name="server-system-requirements"></a>Sunucu sistem gereksinimleri

SignalR sunucu bileşeni çeşitli sunucu yapılandırmalarında barındırılabilir. Bu bölümde işletim sistemleri, .NET Framework, Internet Information Server ve diğer bileşenlerin desteklenen sürümleri açıklanmaktadır.

### <a name="supported-server-operating-systems"></a>Desteklenen sunucu işletim sistemleri

SignalR sunucu bileşeni, aşağıdaki sunucuda veya istemci işletim sistemlerinde barındırılabilir. SignalR 'nin WebSockets, Windows Server 2012, Windows Server 2016 veya Windows 8 kullanması gerektiğini unutmayın (sitenin .NET Framework sürümü 4,5 olarak ayarlandığı ve sitede Web Yuvaları etkin olduğu sürece Windows Azure Web sitelerinde WebSocket kullanılabilir. Yapılandırma sayfası).

- Windows Server 2016
- Windows Server 2012
- Windows Server 2008 R2
- Windows 10
- Windows 8
- Windows 7
- Microsoft Azure

### <a name="supported-server-net-framework-version"></a>Desteklenen sunucu .NET Framework sürümü

SignalR 2 yalnızca .NET Framework 4,5 ' de desteklenir. Güvenilirliği, uyumluluğu, kararlılığı ve performansı artıran güncelleştirmeler için [Önerilen güncelleştirmeler](#updates) bölümüne bakın.

### <a name="supported-server-iis-versions"></a>Desteklenen sunucu IIS sürümleri

SignalR IIS 'de barındırıldığı zaman aşağıdaki sürümler desteklenir. Bir istemci işletim sistemi (örneğin, geliştirme için (Windows 8 veya Windows 7), tüm IIS veya Cassini sürümleri için çok sayıda bağlantı kurulduğundan, bu yana çok çabuk ulaşılmış olan 10 eşzamanlı bağlantı olacağı için kullanılmayacağını unutmayın geçicidir, sıklıkla yeniden oluşturulur ve artık kullanılmıyor olarak silinir. IIS Express, istemci işletim sistemlerinde kullanılmalıdır.

Ayrıca, SignalR 'nin WebSocket kullanmasını, IIS 8 veya IIS 8 Express 'in kullanılması gerektiğini, sunucunun Windows 8, Windows Server 2012 veya sonraki bir sürümü kullanması gerektiğini ve IIS 'de WebSocket 'in etkinleştirilmesi gerektiğini unutmayın. IIS 'de WebSocket 'i etkinleştirme hakkında daha fazla bilgi için bkz. [ııs 8,0 WebSocket protokol desteği](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).

- IIS 8 veya IIS 8 Express.
- IIS 7 ve 7,5. [Uzantısız URL 'ler](https://support.microsoft.com/kb/980368) için destek gereklidir.
- IIS 'nin tümleşik modda çalışıyor olması gerekir; Klasik mod desteklenmez. IIS Klasik modda sunucu tarafından gönderilen olaylar taşıması kullanılarak çalıştırıldığında, 30 saniyeye kadar ileti gecikmeleri yaşanabilir.
- Barındırma uygulamasının tam güven modunda çalışıyor olması gerekir.

## <a name="client-system-requirements"></a>İstemci sistem gereksinimleri

SignalR, çeşitli istemci platformlarında kullanılabilir. Bu bölümde, Web tarayıcıları, Windows Masaüstü uygulamaları, Silverlight uygulamaları ve mobil cihazlarda SignalR kullanımı için sistem gereksinimleri açıklanmaktadır.

### <a name="web-browsers"></a>Web tarayıcıları

SignalR çeşitli web tarayıcılarında kullanılabilir, ancak genellikle yalnızca en son iki sürüm desteklenir.

Tarayıcılarda SignalR kullanan uygulamalar jQuery sürüm 1.6.4 veya büyük sonraki sürümlerini (1.7.2, 1.8.2 veya 1.9.1 gibi) kullanmalıdır.

SignalR aşağıdaki tarayıcılarda kullanılabilir:

- Microsoft Internet Explorer 8, 9, 10 ve 11 sürümleri. Modern, masaüstü ve mobil sürümler desteklenir.
- Mozilla Firefox: geçerli sürüm-1, hem Windows hem de Mac sürümleri.
- Google Chrome: geçerli sürüm-1, hem Windows hem de Mac sürümleri.
- Safari: geçerli sürüm-1, hem Mac hem de iOS sürümleri.
- Opera: yalnızca geçerli sürüm-1, Windows.
- Android Tarayıcısı

Belirli tarayıcıları gerektirmesinin yanı sıra, SignalR 'nin kullandığı çeşitli aktarımlar kendi gereksinimlerine sahiptir. Aşağıdaki aktarımlar aşağıdaki yapılandırmalarda desteklenir:

<a id="browser"></a>

**Web tarayıcısı taşıma gereksinimleri**

| Aktarım | Internet Explorer | Chrome (Windows veya iOS) | Firefox | Safari (OSX veya iOS) | Android |
| --- | --- | --- | --- | --- | --- |
| WebSockets | 10+ | geçerli-1 | geçerli-1 | geçerli-1 | Yok |
| Sunucu tarafından gönderilen olaylar | Yok | geçerli-1 | geçerli-1 | geçerli-1 | Yok |
| ForeverFrame | 8+ | Yok | Yok | Yok | 4.1 |
| Uzun yoklama | 8+ | geçerli-1 | geçerli-1 | geçerli-1 | 4.1 |

\*: tam işlevsellik için 6 + gereklidir.

#### <a name="unsupported-browsers"></a>Desteklenmeyen tarayıcılar

SignalR daha eski tarayıcı sürümlerinde önemli sorunlar olmadan *çalıştırılabiliyor* olsa da, bu hatalarda SignalR 'yi etkin bir şekilde test etmedik ve genellikle bunlarda görünebilen hataları düzelttik.

### <a name="windows-desktop-and-silverlight-applications"></a>Windows Masaüstü ve Silverlight uygulamaları

Bir Web tarayıcısında çalıştırmanın yanı sıra, SignalR tek başına Windows istemcisinde veya Silverlight uygulamalarında barındırılabilir. Windows Masaüstü ve Silverlight SignalR uygulamalarında aşağıdaki sistem gereksinimleri vardır.

- .NET 4 kullanan uygulamalar, Windows XP SP3 veya sonraki sürümlerinde desteklenir.
- .NET Framework 4,5 kullanan uygulamalar Windows Vista veya sonraki sürümlerde desteklenir.

İşletim sistemi ve .NET Framework gereksinimlerine ek olarak, SignalR için kullanılabilen aktarımların kendi gereksinimlerine sahip olması gerekir. Aşağıdaki aktarımlar aşağıdaki yapılandırmalarda desteklenir:

**Windows Masaüstü ve Silverlight aktarım gereksinimleri**

| Aktarım | .NET uygulaması | Silverlight |
| --- | --- | --- |
| Web Yuvaları | Windows 8 + ve .NET 4.5 + | Yok |
| Süresiz çerçeve | Yok | Yok |
| Sunucu tarafından gönderilen olaylar | .NET 4 + | 5+ |
| Uzun yoklama | .NET 4 + | 5+ |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a>Windows Mağazası ve Windows Phone uygulamaları

SignalR, Windows Mağazası uygulamaları ve Windows Phone 8 uygulamalarında kullanılabilir. Aşağıdaki aktarımlar aşağıdaki yapılandırmalarda desteklenir:

**Windows Mağazası ve Windows Phone taşıma gereksinimleri**

| Aktarım | Windows Mağazası/.NET | Windows Mağazası/JavaScript | Windows Phone/IE | Windows Phone/.NET |
| --- | --- | --- | --- | --- |
| WebSockets | Yok | Win8 + | 8+ | Yok |
| Süresiz çerçeve | Yok | Win8 + | 7.5+ | Yok |
| Sunucu tarafından gönderilen olaylar | Win8 + | Yok | Yok | 8+ |
| Uzun yoklama | Win8 + | Win8 + | 7.5+ | 8+ |

<a id="updates"></a>

## <a name="recommended-updates"></a>Önerilen güncelleştirmeler

SignalR sunucuları için aşağıdaki güncelleştirmeler önerilir:

- .NET Framework 4,5 Güncelleştirmesi [burada](https://support.microsoft.com/kb/2750149)bulunabilir.
- Microsoft, ASP.NET için düzenli olarak QFE 'leri yayımlayacaktır. Bunlar kullanılabilir olarak uygulanmalıdır.
