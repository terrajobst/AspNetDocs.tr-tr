---
uid: web-api/overview/advanced/httpclient-message-handlers
title: ASP.NET Web API 'SI içindeki HttpClient Ileti Işleyicileri-ASP.NET 4. x
author: MikeWasson
description: ASP.NET 4. x içinde ASP.NET Web API 'SI için özel ileti işleyicileri oluşturma
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557647"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="3522f-103">ASP.NET Web API 'sinde HttpClient Ileti Işleyicileri</span><span class="sxs-lookup"><span data-stu-id="3522f-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="3522f-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3522f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3522f-105">*İleti işleyicisi* , http isteği alan ve http yanıtı döndüren bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="3522f-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="3522f-106">Genellikle, bir dizi ileti işleyicisi birlikte zincirleme yapılır.</span><span class="sxs-lookup"><span data-stu-id="3522f-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="3522f-107">İlk işleyici bir HTTP isteği alır, bazı işlemleri yapar ve isteği bir sonraki işleyiciye verir.</span><span class="sxs-lookup"><span data-stu-id="3522f-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="3522f-108">Bir noktada yanıt oluşturulur ve zinciri yedekler.</span><span class="sxs-lookup"><span data-stu-id="3522f-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="3522f-109">Bu düzene *temsilci seçme* işleyicisi denir.</span><span class="sxs-lookup"><span data-stu-id="3522f-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="3522f-110">İstemci tarafında, **HttpClient** sınıfı istekleri işlemek için bir ileti işleyicisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="3522f-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="3522f-111">Varsayılan işleyici, isteği ağ üzerinden gönderen ve sunucudan gelen yanıtı alan **HttpClientHandler**' dir.</span><span class="sxs-lookup"><span data-stu-id="3522f-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="3522f-112">İstemci ardışık düzenine özel ileti işleyicileri ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3522f-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="3522f-113">ASP.NET Web API 'SI Ayrıca sunucu tarafında ileti işleyicileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="3522f-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="3522f-114">Daha fazla bilgi için bkz. [http Ileti işleyicileri](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="3522f-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="3522f-115">Özel Ileti Işleyicileri</span><span class="sxs-lookup"><span data-stu-id="3522f-115">Custom Message Handlers</span></span>

<span data-ttu-id="3522f-116">Özel bir ileti işleyicisi yazmak için, **System .net. http. DelegatingHandler** 'ten türetirsiniz ve **sendadsync** yöntemini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="3522f-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="3522f-117">Yöntem imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3522f-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="3522f-118">Yöntemi, giriş olarak bir **HttpRequestMessage** alır ve zaman uyumsuz bir **HttpResponseMessage**döndürür.</span><span class="sxs-lookup"><span data-stu-id="3522f-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="3522f-119">Tipik bir uygulama şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="3522f-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="3522f-120">İstek iletisini işleyin.</span><span class="sxs-lookup"><span data-stu-id="3522f-120">Process the request message.</span></span>
2. <span data-ttu-id="3522f-121">İsteği iç işleyiciye göndermek için `base.SendAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="3522f-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="3522f-122">İç işleyici bir yanıt iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3522f-122">The inner handler returns a response message.</span></span> <span data-ttu-id="3522f-123">(Bu adım zaman uyumsuzdur.)</span><span class="sxs-lookup"><span data-stu-id="3522f-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="3522f-124">Yanıtı işleyin ve çağırana döndürün.</span><span class="sxs-lookup"><span data-stu-id="3522f-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="3522f-125">Aşağıdaki örnek, giden istek için özel üst bilgi ekleyen bir ileti işleyicisini gösterir:</span><span class="sxs-lookup"><span data-stu-id="3522f-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="3522f-126">`base.SendAsync` çağrısı zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="3522f-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="3522f-127">İşleyici Bu çağrıdan sonra herhangi bir iş yaparsanız, yöntemi tamamlandıktan sonra yürütmeyi sürdürmeye yönelik **await** anahtar sözcüğünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="3522f-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="3522f-128">Aşağıdaki örnek, hata kodlarını günlüğe kaydeden bir işleyiciyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="3522f-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="3522f-129">Günlüğe kaydetme işlemi çok ilginç değildir, ancak örnek işleyicinin içindeki yanıta nasıl alınacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3522f-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="3522f-130">Istemci ardışık düzenine Ileti Işleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="3522f-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="3522f-131">**HttpClient**'a özel işleyiciler eklemek Için **Httpclientfactory. Create** metodunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3522f-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="3522f-132">İleti işleyicileri, **oluşturma** yöntemine geçirdiğiniz sırada çağırılır.</span><span class="sxs-lookup"><span data-stu-id="3522f-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="3522f-133">İşleyiciler iç içe olduğundan, yanıt iletisi diğer yönde dolaşır.</span><span class="sxs-lookup"><span data-stu-id="3522f-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="3522f-134">Diğer bir deyişle, son işleyici yanıt iletisini ilk kez alır.</span><span class="sxs-lookup"><span data-stu-id="3522f-134">That is, the last handler is the first to get the response message.</span></span>
