---
uid: web-api/overview/advanced/httpclient-message-handlers
title: HttpClient ileti işleyicileri ASP.NET Web API'si - ASP.NET 4.x
author: MikeWasson
description: ASP.NET'te ASP.NET Web API'si için özel ileti işleyicileri 4.x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: bd52396064cd7007ee17705ba86b02aaf27cb4f0
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59401731"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="842b7-103">ASP.NET Web API'de HttpClient ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="842b7-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="842b7-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="842b7-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="842b7-105">A *ileti işleyicisi* HTTP isteği aldığında ve bir HTTP yanıtı döndüren bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="842b7-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="842b7-106">Genellikle, bir dizi ileti işleyicileri zincirleme birlikte.</span><span class="sxs-lookup"><span data-stu-id="842b7-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="842b7-107">İlk işleyici HTTP isteği aldığında, işlem yapar ve bir sonraki işleyici istek sağlar.</span><span class="sxs-lookup"><span data-stu-id="842b7-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="842b7-108">Belirli bir noktada yanıt oluşturulur ve zincirinde döner.</span><span class="sxs-lookup"><span data-stu-id="842b7-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="842b7-109">Bu düzen adı verilen bir *temsilci olarak görevlendirme* işleyici.</span><span class="sxs-lookup"><span data-stu-id="842b7-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="842b7-110">İstemci tarafında **HttpClient** sınıfını isteklerini işlemek için bir ileti işleyicisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="842b7-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="842b7-111">Varsayılan işleyici **HttpClientHandler**, ağ üzerinden isteği gönderir ve sunucudan yanıtı alır.</span><span class="sxs-lookup"><span data-stu-id="842b7-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="842b7-112">Özel ileti işleyicileri istemci ardışık düzende ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="842b7-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="842b7-113">ASP.NET Web API, sunucu tarafında ileti işleyicileri de kullanır.</span><span class="sxs-lookup"><span data-stu-id="842b7-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="842b7-114">Daha fazla bilgi için [HTTP ileti işleyicileri](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="842b7-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="842b7-115">Özel ileti işleyicileri</span><span class="sxs-lookup"><span data-stu-id="842b7-115">Custom Message Handlers</span></span>

<span data-ttu-id="842b7-116">Özel ileti işleyicisi yazmak için türetilen **System.Net.Http.DelegatingHandler** ve geçersiz kılma **SendAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="842b7-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="842b7-117">Aşağıda, yöntem imzası verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="842b7-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="842b7-118">Yöntem alır bir **HttpRequestMessage** giriş ve zaman uyumsuz olarak döndürür olarak bir **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="842b7-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="842b7-119">Tipik bir uygulaması şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="842b7-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="842b7-120">İşlem istek iletisi.</span><span class="sxs-lookup"><span data-stu-id="842b7-120">Process the request message.</span></span>
2. <span data-ttu-id="842b7-121">Çağrı `base.SendAsync` iç işleyici için istek gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="842b7-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="842b7-122">İç işleyici, bir yanıt iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="842b7-122">The inner handler returns a response message.</span></span> <span data-ttu-id="842b7-123">(Bu adım, zaman uyumsuz.)</span><span class="sxs-lookup"><span data-stu-id="842b7-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="842b7-124">Yanıta işlemek ve çağırana döndürmesi.</span><span class="sxs-lookup"><span data-stu-id="842b7-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="842b7-125">Aşağıdaki örnek, bir giden istek için özel bir başlık ekler bir ileti işleyicisini gösterir:</span><span class="sxs-lookup"><span data-stu-id="842b7-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="842b7-126">Çağrı `base.SendAsync` zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="842b7-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="842b7-127">İşleyici, bu çağrıdan sonra herhangi bir iş varsa, kullanmak **await** yöntemi tamamlandıktan sonra yürütülmesine devam etmek için anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="842b7-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="842b7-128">Aşağıdaki örnek, hata kodları günlükleri bir işleyici gösterir.</span><span class="sxs-lookup"><span data-stu-id="842b7-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="842b7-129">Günlük çok ilginç değil, ancak örnek işleyici içinde yanıt alın nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="842b7-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="842b7-130">İstemci işlem hattına ileti işleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="842b7-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="842b7-131">Özel işleyicileri eklemek için **HttpClient**, kullanın **HttpClientFactory.Create** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="842b7-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="842b7-132">İleti işleyicileri içine geçirdiğiniz sırayla çağrılır **Oluştur** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="842b7-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="842b7-133">Yanıt iletisi işleyicileri nedeniyle, diğer yönde hareket eder.</span><span class="sxs-lookup"><span data-stu-id="842b7-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="842b7-134">Diğer bir deyişle, son ilk yanıt iletisi işleyicidir.</span><span class="sxs-lookup"><span data-stu-id="842b7-134">That is, the last handler is the first to get the response message.</span></span>
