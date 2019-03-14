---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073377"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a>Nasıl derleme/güvenli kullanıcı veri örneği çalıştırma

* Gizli dizi Yöneticisi Aracı ile parola ayarlayın:

  `dotnet user-secrets set SeedUserPW <pw>`

* Veritabanını Güncelleştir:

    `dotnet ef database update`

* Projede HTTPS'yi etkinleştirme
