---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57797052"
---
> <span data-ttu-id="e82c9-101">Uygulama kimlik veri deposu olarak SQLite kullanıyorsa, bazı komutlar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="e82c9-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="e82c9-102">Veritabanı altyapısı, kısıtlamaları nedeniyle `Alter` komutları şu özel durum:</span><span class="sxs-lookup"><span data-stu-id="e82c9-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="e82c9-103">"System.NotSupportedException: "SQLite bu geçiş işlemi desteklemiyor."</span><span class="sxs-lookup"><span data-stu-id="e82c9-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="e82c9-104">Geçici bir çözüm, Code First geçişleri tabloları değiştirmek için veritabanında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e82c9-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
