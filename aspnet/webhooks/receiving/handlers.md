---
uid: webhooks/receiving/handlers
title: ASP.NET Web kancaları işleyicileri | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancalarında istekleri işleme.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637874"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="29f0b-103">ASP.NET Web kancaları işleyicileri</span><span class="sxs-lookup"><span data-stu-id="29f0b-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="29f0b-104">Web kancaları istekleri bir Web kancası alıcısı tarafından doğrulandıktan sonra, Kullanıcı kodu tarafından işlenmek üzere hazırlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="29f0b-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="29f0b-105">Burada *işleyiciler* gelir.</span><span class="sxs-lookup"><span data-stu-id="29f0b-105">This is where *handlers* come in.</span></span> <span data-ttu-id="29f0b-106">İşleyiciler [ıwebkancahandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) arabiriminden türetilir, ancak genellikle doğrudan arabirimden türetmek yerine [webkancahandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="29f0b-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="29f0b-107">Bir Web kancası isteği bir veya daha fazla işleyici tarafından işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="29f0b-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="29f0b-108">İşleyiciler, karşılık gelen *Order* özelliği en küçükten en büyüğe doğru, sıranın basit bir tamsayı olduğu (1 ile 100 arasında olması önerilir) sırayla çağrılır:</span><span class="sxs-lookup"><span data-stu-id="29f0b-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![Web kancası Işleyici sırası özelliği diyagramı](_static/Handlers.png)

<span data-ttu-id="29f0b-110">Bir işleyici, isteğe bağlı olarak Web Kancahandlercontext üzerinde *Response* özelliğini ayarlayabilir ve bu da işlemin durdurulmasına ve yanıt, Web KANCASıNA http yanıtı olarak geri gönderilmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="29f0b-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="29f0b-111">Yukarıdaki örnekte, C Işleyicisi, B 'den daha yüksek bir sıraya sahip olduğundan ve B yanıtı ayarlamadığından, Işleyici C çağırılır.</span><span class="sxs-lookup"><span data-stu-id="29f0b-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="29f0b-112">Yanıtın ayarlanması genellikle yalnızca yanıtın kaynak API 'ye geri bilgi taşıyabileceği Web kancaları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="29f0b-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="29f0b-113">Bunun nedeni örneğin, yanıtın Web kancalarının nereden geldiğini bir kanala geri nakledildiği yer.</span><span class="sxs-lookup"><span data-stu-id="29f0b-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="29f0b-114">İşleyiciler yalnızca belirli bir alıcıdan Web kancaları almak istiyorsanız alıcı özelliğini ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="29f0b-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="29f0b-115">Bunlar, tüm bunlar için çağırdıkları alıcıyı ayarlamazsanız.</span><span class="sxs-lookup"><span data-stu-id="29f0b-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="29f0b-116">Yanıtın diğer yaygın kullanımı, Web kancasının artık etkin olmadığını ve başka hiçbir isteğin gönderilmesi gerektiğini göstermek için *410 geçmiş* bir yanıt kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="29f0b-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="29f0b-117">Varsayılan olarak, bir işleyici tüm Web kancası alıcıları tarafından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="29f0b-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="29f0b-118">Ancak, *alıcı* özelliği bir işleyicinin adına ayarlandıysa, bu işleyici Bu alıcıdan yalnızca Web kancası isteklerini alacaktır.</span><span class="sxs-lookup"><span data-stu-id="29f0b-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="29f0b-119">Web kancasını işleme</span><span class="sxs-lookup"><span data-stu-id="29f0b-119">Processing a WebHook</span></span>

<span data-ttu-id="29f0b-120">Bir işleyici çağrıldığında, Web kancası isteği hakkında bilgi içeren bir [Webkancahandlercontext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) alır.</span><span class="sxs-lookup"><span data-stu-id="29f0b-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="29f0b-121">*Veri özelliğinden genellıkle* http istek gövdesi verileri bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="29f0b-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="29f0b-122">Verilerin türü genellikle JSON veya HTML form verileri olur, ancak isterseniz daha belirli bir türe atama mümkündür.</span><span class="sxs-lookup"><span data-stu-id="29f0b-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="29f0b-123">Örneğin, ASP.NET Webkancaları tarafından oluşturulan özel Web kancaları, [Customnotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) türünde aşağıdaki gibi oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="29f0b-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="29f0b-124">Kuyruğa alınan Işlem</span><span class="sxs-lookup"><span data-stu-id="29f0b-124">Queued Processing</span></span>

<span data-ttu-id="29f0b-125">Birçok Web kancası gönderisini bir yanıt üretilmez ve saniyeler içinde oluşturulmazsa Web kancasını yeniden gönderecektir.</span><span class="sxs-lookup"><span data-stu-id="29f0b-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="29f0b-126">Bu, işleyicinizin bu zaman dilimi içindeki işlemeyi, tekrar çağrılabilmesi için tamamlaması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="29f0b-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="29f0b-127">İşlem daha uzun sürer veya ayrı ayrı işlenirse, Web kancası isteği bir kuyruğa (örneğin, [Azure depolama kuyruğu](https://msdn.microsoft.com/library/azure/dd179353.aspx)) göndermek Için [Webkancaqueuehandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="29f0b-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="29f0b-128">[Web kancası Queuehandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) uygulamasının bir ana hattı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="29f0b-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
