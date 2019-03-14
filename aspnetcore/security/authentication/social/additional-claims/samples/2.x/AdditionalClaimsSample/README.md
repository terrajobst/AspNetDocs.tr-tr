---
ms.openlocfilehash: 09cd8e639238b998212b813cba5bc1aa85f36a75
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072318"
---
# <a name="aspnet-core-external-authentication-provider-additional-claims-sample-aspnet-core-2x"></a><span data-ttu-id="5cfbf-101">ASP.NET Core Dış kimlik doğrulama sağlayıcısının ek örnek kimliğini (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="5cfbf-101">ASP.NET Core External Authentication Provider Additional Claims Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="5cfbf-102">Bu örnek, Google kimlik doğrulama sağlayıcısı kullanarak Google kullanıcı verilerinden ek talep oluşturma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5cfbf-102">This sample illustrates establishing additional claims from Google user data using the Google authentication provider.</span></span> <span data-ttu-id="5cfbf-103">Bu örneğe eşlik edecek [ek talep ve dış sağlayıcılardan gelen belirteçleri kalıcı](https://docs.microsoft.com/aspnet/core/security/authentication/social/additional-claims).</span><span class="sxs-lookup"><span data-stu-id="5cfbf-103">This sample accompanies [Persist additional claims and tokens from external providers](https://docs.microsoft.com/aspnet/core/security/authentication/social/additional-claims).</span></span>

<span data-ttu-id="5cfbf-104">Örneği kullanmak için geçerli bir Google istemci kimliği ve gizli dizisinde sağlamak `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="5cfbf-104">To use the sample, provide a valid Google Client ID and Secret in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="5cfbf-105">Daha fazla bilgi için [Google dış oturum açma Kurulumu](https://docs.microsoft.com/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="5cfbf-105">For more information, see [Google external login setup](https://docs.microsoft.com/aspnet/core/security/authentication/social/google-logins).</span></span>
