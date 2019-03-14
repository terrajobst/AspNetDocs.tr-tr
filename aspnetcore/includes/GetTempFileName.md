---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165872"
---
<span data-ttu-id="c9392-101">**Uyarı**: Aşağıdaki kod `GetTempFileName`, hangi oluşturur bir `IOException` 65535'ten fazla dosyaları önceki geçici dosyalar siliniyor olmadan oluşturulduysa.</span><span class="sxs-lookup"><span data-stu-id="c9392-101">**Warning**: The following code uses `GetTempFileName`, which throws an `IOException` if more than 65535 files are created without deleting previous temporary files.</span></span> <span data-ttu-id="c9392-102">Gerçek bir uygulamada geçici dosyaları silin veya kullanın `GetTempPath` ve `GetRandomFileName` geçici dosya adları oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c9392-102">A real app should either delete temporary files or use `GetTempPath` and `GetRandomFileName` to create temporary file names.</span></span> <span data-ttu-id="c9392-103">65535 dosyaları sınırı sunucu başına olduğundan başka bir uygulama sunucusunda 65535 tüm dosyaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9392-103">The 65535 files limit is per server, so another app on the server can use up all 65535 files.</span></span> 
