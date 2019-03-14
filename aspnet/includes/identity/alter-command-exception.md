---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57797052"
---
> Uygulama kimlik veri deposu olarak SQLite kullanıyorsa, bazı komutlar desteklenmez. Veritabanı altyapısı, kısıtlamaları nedeniyle `Alter` komutları şu özel durum:
>
> "System.NotSupportedException: "SQLite bu geçiş işlemi desteklemiyor." 
>
> Geçici bir çözüm, Code First geçişleri tabloları değiştirmek için veritabanında çalıştırın.
