---
ms.openlocfilehash: d7ef9b11af8ee11e4ec84404f8cdeb0b89384a3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57130456"
---
## <a name="forward-request-information-with-a-proxy-or-load-balancer"></a>İleri bir proxy ile ilgili bilgi isteyin veya yük dengeleyici

Uygulamayı bir ara sunucu veya yük dengeleyici arkasında dağıtılırsa, özgün istek bilgilerden bazılarını istek üst bilgileri uygulamada iletilmesi. Bu bilgiler genellikle güvenli istek düzeni içerir (`https`), konak ve istemci IP adresi. Uygulamaları otomatik olarak bulmak ve özgün istek bilgileri kullanmak için bu istek üst bilgilerini okuma yok.

Düzeni, dış sağlayıcıları ile kimlik doğrulaması akışı etkiler bağlantı oluşturmada kullanılır. Güvenli düzeni kaybetme (`https`) yanlış güvenli olmayan yeniden yönlendirme URL'ler oluşturulurken uygulamada sonuçlanır.

İletilen üstbilgileri ara yazılım, özgün istek bilgileri uygulama isteği işleme için kullanılabilir hale getirmek için kullanın.

Daha fazla bilgi için bkz. <xref:host-and-deploy/proxy-load-balancer>.
