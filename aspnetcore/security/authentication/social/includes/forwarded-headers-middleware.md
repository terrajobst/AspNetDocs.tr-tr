---
ms.openlocfilehash: d7ef9b11af8ee11e4ec84404f8cdeb0b89384a3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57130456"
---
## <a name="forward-request-information-with-a-proxy-or-load-balancer"></a><span data-ttu-id="661aa-101">İleri bir proxy ile ilgili bilgi isteyin veya yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="661aa-101">Forward request information with a proxy or load balancer</span></span>

<span data-ttu-id="661aa-102">Uygulamayı bir ara sunucu veya yük dengeleyici arkasında dağıtılırsa, özgün istek bilgilerden bazılarını istek üst bilgileri uygulamada iletilmesi.</span><span class="sxs-lookup"><span data-stu-id="661aa-102">If the app is deployed behind a proxy server or load balancer, some of the original request information might be forwarded to the app in request headers.</span></span> <span data-ttu-id="661aa-103">Bu bilgiler genellikle güvenli istek düzeni içerir (`https`), konak ve istemci IP adresi.</span><span class="sxs-lookup"><span data-stu-id="661aa-103">This information usually includes the secure request scheme (`https`), host, and client IP address.</span></span> <span data-ttu-id="661aa-104">Uygulamaları otomatik olarak bulmak ve özgün istek bilgileri kullanmak için bu istek üst bilgilerini okuma yok.</span><span class="sxs-lookup"><span data-stu-id="661aa-104">Apps don't automatically read these request headers to discover and use the original request information.</span></span>

<span data-ttu-id="661aa-105">Düzeni, dış sağlayıcıları ile kimlik doğrulaması akışı etkiler bağlantı oluşturmada kullanılır.</span><span class="sxs-lookup"><span data-stu-id="661aa-105">The scheme is used in link generation that affects the authentication flow with external providers.</span></span> <span data-ttu-id="661aa-106">Güvenli düzeni kaybetme (`https`) yanlış güvenli olmayan yeniden yönlendirme URL'ler oluşturulurken uygulamada sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="661aa-106">Losing the secure scheme (`https`) results in the app generating incorrect insecure redirect URLs.</span></span>

<span data-ttu-id="661aa-107">İletilen üstbilgileri ara yazılım, özgün istek bilgileri uygulama isteği işleme için kullanılabilir hale getirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="661aa-107">Use Forwarded Headers Middleware to make the original request information available to the app for request processing.</span></span>

<span data-ttu-id="661aa-108">Daha fazla bilgi için bkz. <xref:host-and-deploy/proxy-load-balancer>.</span><span class="sxs-lookup"><span data-stu-id="661aa-108">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>
