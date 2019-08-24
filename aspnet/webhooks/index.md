---
uid: webhooks/index
title: ASP.NET Web kancalarına genel bakış | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancalarına giriş.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa65a20e1af16d58533e37fafc77ac246e0fe327
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000726"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="b6bc9-103">ASP.NET Web kancalarına genel bakış</span><span class="sxs-lookup"><span data-stu-id="b6bc9-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="b6bc9-104">Web kancaları, Web API 'Leri ve SaaS hizmetlerini birbirine bağlama için basit bir yayın/alt model sağlayan hafif bir HTTP modelidir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="b6bc9-105">Bir hizmette bir olay gerçekleştiğinde, kayıtlı abonelere HTTP POST isteği biçiminde bir bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="b6bc9-106">POST isteği, alıcının uygun şekilde davranmasına olanak sağlayan olayla ilgili bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="b6bc9-107">Web kancaları, basitliği nedeniyle [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [bolluk](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/)ve çok sayıda hizmet tarafından zaten kullanıma sunuldu daha fazla.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="b6bc9-108">Örneğin, bir Web kancası bir dosyanın [Dropbox](http://dropbox.com/)'ta değiştiğini veya bir kod değişikliğinin GitHub 'da kaydedilmiş olduğunu veya bir ödemenin [PayPal](http://www.paypal.com/)'de başlatıldığını ya da [Trello](http://www.trello.com/)'da bir kartın oluşturulduğunu gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="b6bc9-109">Olanaklar sınırsızdır!</span><span class="sxs-lookup"><span data-stu-id="b6bc9-109">The possibilities are endless!</span></span>

<span data-ttu-id="b6bc9-110">Web kancaları Microsoft ASP.NET, Web kancalarını ASP.NET uygulamanızın bir parçası olarak hem gönderilmesini hem de almanızı kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="b6bc9-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="b6bc9-111">Alma tarafında, Web kancalarını herhangi bir sayıda Web kancası sağlayıcısından almak ve işlemek için ortak bir model sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="b6bc9-112">[Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [iletici](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [bolluk](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) ve için destek içeren kutudan çıkar. [Zendesk](https://www.zendesk.com/) ancak daha fazla destek eklemek çok kolay.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="b6bc9-113">Gönderme tarafında, aboneliklerin yönetilmesi ve depolanması ve doğru abone kümesine olay bildirimleri gönderilmesi için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="b6bc9-114">Bu, abonelerin abone olabileceği kendi olay kümesini tanımlamanızı ve şeyler gerçekleştiğinde bunları bilgilendirmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="b6bc9-115">İki bölüm, senaryonuza bağlı olarak veya ayrı bir şekilde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="b6bc9-116">Yalnızca diğer hizmetlerden Web kancaları almanız gerekiyorsa yalnızca alıcı parçasını kullanabilirsiniz; yalnızca başkalarının kullanması için Web kancaları sunmak istiyorsanız, bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="b6bc9-117">Kod, ASP.NET Web API 2 ve ASP.NET MVC 5 ' i hedefler ve [GitHub 'Da OSS](https://github.com/aspnet/WebHooks)olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="b6bc9-118">Web kancalarına genel bakış</span><span class="sxs-lookup"><span data-stu-id="b6bc9-118">WebHooks Overview</span></span>

<span data-ttu-id="b6bc9-119">Web kancaları, hizmetten hizmete nasıl kullanıldığını, ancak temel fikrin aynı olduğunu gösterdiği anlamına gelen bir modeldir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="b6bc9-120">Web kancalarını, bir kullanıcının başka bir yerde yer aldığı olaylara abone olabileceği basit bir yayın/alt model olarak düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="b6bc9-121">Olay bildirimleri olay kendisiyle ilgili bilgiler içeren HTTP POST istekleri olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="b6bc9-122">Genellikle HTTP POST isteği, Web kancası göndericisi tarafından belirlenen ve Web kancasının tetiklenmesine neden olan olay hakkında bilgi içeren bir JSON nesnesi veya HTML form verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="b6bc9-123">Örneğin, [GitHub](http://www.github.com/) 'Dan bir Web kancası gönderi isteği gövdesi, belirli bir depoda açılmakta olan yeni bir sorun nedeniyle şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="b6bc9-123">For example, a WebHook POST request body from [GitHub](http://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="b6bc9-124">Web kancasının amaçlanan gönderenden gerçekten olduğundan emin olmak için POST isteğinin bir şekilde güvenli hale getirilmesi ve sonra alıcı tarafından doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="b6bc9-125">Örneğin, [GitHub Web kancaları](https://developer.github.com/webhooks/) , alıcı uygulama tarafından denetlenen istek gövdesinin karmasını Içeren bir *X-hub-Signature* http üst bilgisi içerir, böylece endişelenmenize gerek kalmaz.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="b6bc9-126">Web kancası akışı genellikle şuna benzer bir şekilde geçer:</span><span class="sxs-lookup"><span data-stu-id="b6bc9-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="b6bc9-127">Web kancası göndericisi, bir istemcinin abone olabileceği olayları kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="b6bc9-128">Olaylar, sistemdeki observable değişikliklerini, örneğin yeni bir veri öğesinin eklendiği, bir işlemin tamamlandığını veya başka bir şey olduğunu anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="b6bc9-129">Web kancası alıcısı dört şeyi içeren bir Web kancası kaydederek abone olur:</span><span class="sxs-lookup"><span data-stu-id="b6bc9-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="b6bc9-130">Olay bildiriminin HTTP POST isteği biçiminde nakledilmesi gereken bir URI;</span><span class="sxs-lookup"><span data-stu-id="b6bc9-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="b6bc9-131">Web kancasının tetiklenme gereken belirli olayları açıklayan bir filtre kümesi;</span><span class="sxs-lookup"><span data-stu-id="b6bc9-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="b6bc9-132">HTTP POST isteğini imzalamak için kullanılan gizli anahtar;</span><span class="sxs-lookup"><span data-stu-id="b6bc9-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="b6bc9-133">HTTP POST isteğine dahil edilecek ek veriler.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="b6bc9-134">Bu örnek, HTTP POST istek gövdesine eklenen ek HTTP üst bilgi alanları veya özellikleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="b6bc9-135">Bir olay gerçekleştiğinde, eşleşen Web kancası kayıtları bulunur ve HTTP POST istekleri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="b6bc9-136">Genellikle, HTTP POST isteklerinin oluşturulması bazı nedenlerle alıcının yanıt vermemesi veya HTTP POST isteğinin bir hata yanıtına neden olması halinde birkaç kez yeniden denenir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="b6bc9-137">Web kancaları Işleme Işlem hattı</span><span class="sxs-lookup"><span data-stu-id="b6bc9-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="b6bc9-138">Gelen Web kancaları için Microsoft ASP.NET Web kancaları işleme işlem hattı şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="b6bc9-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET Web kancaları Işleme Işlem hattı](_static/WebHookReceivers.png)

<span data-ttu-id="b6bc9-140">*Alıcılar* ve *işleyiciler*burada bulunan iki temel kavramlardır:</span><span class="sxs-lookup"><span data-stu-id="b6bc9-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="b6bc9-141">*Alıcılar* belirli bir gönderenden gelen Web kancası türünü işlemekten ve Web kancası isteğinin gerçekten amaçlanan gönderenden olduğundan emin olmak için güvenlik denetimlerinin zorlanmasından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="b6bc9-142">*İşleyiciler* genellikle kullanıcı kodunun belirli Web kancasını işleme çalıştırdığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="b6bc9-143">Aşağıdaki düğümlerde, bu kavramlar daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b6bc9-143">In the following nodes these concepts are described in more details.</span></span>
