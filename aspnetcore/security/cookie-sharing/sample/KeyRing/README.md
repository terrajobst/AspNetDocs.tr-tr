---
ms.openlocfilehash: 17ae8088e2e570628883ea5f8d71e093e6ed7cc8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071547"
---
# <a name="data-protection-key-folder"></a><span data-ttu-id="15065-101">Veri koruma anahtarı klasörü</span><span class="sxs-lookup"><span data-stu-id="15065-101">Data protection key folder</span></span>

<span data-ttu-id="15065-102">Veri koruma anahtarları için paylaşılan bir klasör oluşturmak için yer tutucu dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="15065-102">This file is a placeholder to create a shared folder for data protection keys.</span></span>

<span data-ttu-id="15065-103">Bir üretim dağıtımında, anahtarları asla iade bu dizinde dosya ve geliştirme kök dışında kaynak denetimine yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="15065-103">In a production deployment, place the keys outside of the development root and never check-in files in this directory into source control.</span></span> <span data-ttu-id="15065-104">Veri koruma anahtarları dosyalarında DPAPI veya bir X509Certificate ile koruyun.</span><span class="sxs-lookup"><span data-stu-id="15065-104">Protect data protection keys in the files with DPAPI or an X509Certificate.</span></span>

<span data-ttu-id="15065-105">Bkz: [ASP.NET Core veri koruması: Tüketici API'leri, yapılandırma, genişletilebilirlik API'leri ve uygulama](https://docs.microsoft.com/aspnet/core/security/data-protection/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="15065-105">See [Data Protection in ASP.NET Core: Consumer APIs, configuration, extensibility APIs and implementation](https://docs.microsoft.com/aspnet/core/security/data-protection/) for more information.</span></span>
