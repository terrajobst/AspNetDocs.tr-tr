---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165872"
---
**Uyarı**: Aşağıdaki kod `GetTempFileName`, hangi oluşturur bir `IOException` 65535'ten fazla dosyaları önceki geçici dosyalar siliniyor olmadan oluşturulduysa. Gerçek bir uygulamada geçici dosyaları silin veya kullanın `GetTempPath` ve `GetRandomFileName` geçici dosya adları oluşturmak için. 65535 dosyaları sınırı sunucu başına olduğundan başka bir uygulama sunucusunda 65535 tüm dosyaları kullanabilirsiniz. 
