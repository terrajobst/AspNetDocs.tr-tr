---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077478"
---
# <a name="aspnet-core-response-caching-sample"></a>ASP.NET Core yanıt önbelleğe alma örneği

Bu örnek ASP.NET Core kullanımını [yanıt önbelleğe alma ara yazılımı](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).

Uygulama, dizin sayfasıyla yanıt dahil olmak üzere bir `Cache-Control` önbelleğe alma davranışını yapılandırmak için üst bilgi. Uygulama ayrıca ayarlar `Vary` yanıt yalnızca şu durumlarda hizmet önbelleğini yapılandırmak için üst bilgi `Accept-Encoding` sonraki istekleri üstbilgisinin özgün istekteki eşleşen.

Örnek çalışırken, dizin sayfası depolandığında ve 10 saniye boyunca önbelleğe önbelleğinden sunulur.
