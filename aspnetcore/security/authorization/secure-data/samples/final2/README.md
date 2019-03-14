---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073377"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="4a44b-101">Nasıl derleme/güvenli kullanıcı veri örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4a44b-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="4a44b-102">Gizli dizi Yöneticisi Aracı ile parola ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4a44b-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="4a44b-103">Veritabanını Güncelleştir:</span><span class="sxs-lookup"><span data-stu-id="4a44b-103">Update the database:</span></span>

    `dotnet ef database update`

* <span data-ttu-id="4a44b-104">Projede HTTPS'yi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4a44b-104">Enable HTTPS in the project</span></span>
