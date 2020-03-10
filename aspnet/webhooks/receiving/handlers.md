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
# <a name="aspnet-webhooks-handlers"></a>ASP.NET Web kancaları işleyicileri

Web kancaları istekleri bir Web kancası alıcısı tarafından doğrulandıktan sonra, Kullanıcı kodu tarafından işlenmek üzere hazırlanacaktır. Burada *işleyiciler* gelir. İşleyiciler [ıwebkancahandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) arabiriminden türetilir, ancak genellikle doğrudan arabirimden türetmek yerine [webkancahandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) sınıfını kullanır.

Bir Web kancası isteği bir veya daha fazla işleyici tarafından işlenebilir. İşleyiciler, karşılık gelen *Order* özelliği en küçükten en büyüğe doğru, sıranın basit bir tamsayı olduğu (1 ile 100 arasında olması önerilir) sırayla çağrılır:

![Web kancası Işleyici sırası özelliği diyagramı](_static/Handlers.png)

Bir işleyici, isteğe bağlı olarak Web Kancahandlercontext üzerinde *Response* özelliğini ayarlayabilir ve bu da işlemin durdurulmasına ve yanıt, Web KANCASıNA http yanıtı olarak geri gönderilmesine neden olur. Yukarıdaki örnekte, C Işleyicisi, B 'den daha yüksek bir sıraya sahip olduğundan ve B yanıtı ayarlamadığından, Işleyici C çağırılır.

Yanıtın ayarlanması genellikle yalnızca yanıtın kaynak API 'ye geri bilgi taşıyabileceği Web kancaları için geçerlidir. Bunun nedeni örneğin, yanıtın Web kancalarının nereden geldiğini bir kanala geri nakledildiği yer. İşleyiciler yalnızca belirli bir alıcıdan Web kancaları almak istiyorsanız alıcı özelliğini ayarlayabilir. Bunlar, tüm bunlar için çağırdıkları alıcıyı ayarlamazsanız.

Yanıtın diğer yaygın kullanımı, Web kancasının artık etkin olmadığını ve başka hiçbir isteğin gönderilmesi gerektiğini göstermek için *410 geçmiş* bir yanıt kullanmaktır.

Varsayılan olarak, bir işleyici tüm Web kancası alıcıları tarafından çağırılır. Ancak, *alıcı* özelliği bir işleyicinin adına ayarlandıysa, bu işleyici Bu alıcıdan yalnızca Web kancası isteklerini alacaktır.

## <a name="processing-a-webhook"></a>Web kancasını işleme

Bir işleyici çağrıldığında, Web kancası isteği hakkında bilgi içeren bir [Webkancahandlercontext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) alır. *Veri özelliğinden genellıkle* http istek gövdesi verileri bulunabilir.

Verilerin türü genellikle JSON veya HTML form verileri olur, ancak isterseniz daha belirli bir türe atama mümkündür. Örneğin, ASP.NET Webkancaları tarafından oluşturulan özel Web kancaları, [Customnotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) türünde aşağıdaki gibi oluşturulabilir:

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

  ## <a name="queued-processing"></a>Kuyruğa alınan Işlem

Birçok Web kancası gönderisini bir yanıt üretilmez ve saniyeler içinde oluşturulmazsa Web kancasını yeniden gönderecektir. Bu, işleyicinizin bu zaman dilimi içindeki işlemeyi, tekrar çağrılabilmesi için tamamlaması gerektiği anlamına gelir.

İşlem daha uzun sürer veya ayrı ayrı işlenirse, Web kancası isteği bir kuyruğa (örneğin, [Azure depolama kuyruğu](https://msdn.microsoft.com/library/azure/dd179353.aspx)) göndermek Için [Webkancaqueuehandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) kullanılabilir.

[Web kancası Queuehandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) uygulamasının bir ana hattı aşağıda verilmiştir:

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
