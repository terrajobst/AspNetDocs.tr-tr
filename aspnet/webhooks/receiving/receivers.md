---
uid: webhooks/receiving/receivers
title: ASP.NET Web kancası alıcıları | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancaları alıcıları
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574195"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="b406c-103">ASP.NET Web kancaları alıcıları</span><span class="sxs-lookup"><span data-stu-id="b406c-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="b406c-104">Web kancalarını alma, gönderenin kim olduğuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b406c-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="b406c-105">Bazen, abonenin gerçekten dinlediğini doğrulayan bir Web kancası kaydı için ek adımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="b406c-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="b406c-106">Bazı Web kancaları, HTTP POST isteğinin yalnızca bağımsız olarak alınabilecek olay bilgilerine bir başvuru içerdiği bir istek temelli model sağlar.</span><span class="sxs-lookup"><span data-stu-id="b406c-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="b406c-107">Genellikle güvenlik modeli oldukça bir bit olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="b406c-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="b406c-108">Web kancaları Microsoft ASP.NET amacı, Web kancalarının belirli bir çeşitlerini nasıl işleyeceğinizi öğrenmek zorunda kalmadan API 'nizi daha basit ve daha tutarlı hale getirir.</span><span class="sxs-lookup"><span data-stu-id="b406c-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="b406c-109">Web kancası alıcısı, belirli bir gönderenden Web kancalarını kabul edip doğrulamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="b406c-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="b406c-110">Web kancası alıcısı, her biri kendi yapılandırmasına sahip olan herhangi bir sayıda Web kancasını destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b406c-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="b406c-111">Örneğin, GitHub Web kancası alıcısı herhangi bir sayıdaki GitHub depoağından Web kancalarını kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="b406c-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="b406c-112">Web kancası alıcı URI 'Leri</span><span class="sxs-lookup"><span data-stu-id="b406c-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="b406c-113">Microsoft ASP.NET Web kancaları yükleyerek, açık uçlu hizmetlerden gelen Web kancası isteklerini kabul eden genel bir Web kancası denetleyicisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b406c-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="b406c-114">Bir istek geldiğinde, belirli bir Web kancası Göndericisini işlemek için yüklediğiniz uygun alıcıyı seçer.</span><span class="sxs-lookup"><span data-stu-id="b406c-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="b406c-115">Bu denetleyicinin URI 'si, hizmete kaydolmanızı sağlayan Web kancası URI 'sidir ve şu biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="b406c-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="b406c-116">Güvenlik nedenleriyle birçok Web kancası alıcısı URI 'nin bir *https* URI olmasını gerektirir ve bazı durumlarda, yalnızca amaçlanan TARAFıN yukarıdaki URI 'ye Web kancaları gönderebildiğini zorlamak için kullanılan ek bir sorgu parametresi de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b406c-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="b406c-117">`<receiver>` bileşen alıcının adı, örneğin `github` veya `slack`.</span><span class="sxs-lookup"><span data-stu-id="b406c-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="b406c-118">*{İd}* , belirli bir Web kancası alıcı yapılandırmasını tanımlamak için kullanılabilen isteğe bağlı bir tanıtıcıdır.</span><span class="sxs-lookup"><span data-stu-id="b406c-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="b406c-119">Bu, belirli bir alıcı ile N Web kancalarını kaydetmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b406c-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="b406c-120">Örneğin, aşağıdaki üç URI üç bağımsız Web kancalarına kaydolmak için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="b406c-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="b406c-121">Web kancası alıcısı yükleme</span><span class="sxs-lookup"><span data-stu-id="b406c-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="b406c-122">Web kancalarını Microsoft ASP.NET kullanarak Web kancaları almak için, önce Web kancaları almak istediğiniz Web kancası sağlayıcısı veya sağlayıcıları için NuGet paketini yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="b406c-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="b406c-123">NuGet paketleri, son bölümün desteklenen hizmeti gösterdiği [Microsoft. Aspnet. Webkancaları. alıcılar. \*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="b406c-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="b406c-124">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b406c-124">For example</span></span>

<span data-ttu-id="b406c-125">[Microsoft. Aspnet. Webkancalar. alıcılar. GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) , GitHub 'Dan ve [Microsoft. Aspnet. Webkancaları. alıcılar. alıcıları](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) tarafından oluşturulan Web kancalarını almak için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="b406c-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="b406c-126">Box, GitHub, MailChimp, PayPal, Iletici, Salesforce, bolluk, Stripe, Trello ve WordPress için destek bulabilirsiniz, ancak herhangi bir sayıda diğer sağlayıcıyı desteklemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="b406c-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="b406c-127">Web kancası alıcısını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b406c-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="b406c-128">Web kancası alıcıları [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) arabirimini aracılığıyla yapılandırılır ve bu arabirimin belirli uygulamaları herhangi bir bağımlılık ekleme modeli kullanılarak kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="b406c-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="b406c-129">Varsayılan uygulama, Web. config dosyasında ayarlanmış olan veya Azure Web Apps kullanılıyorsa [Azure portalından](https://portal.azure.com/)ayarlanabilir olan uygulama ayarlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b406c-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure Uygulama ayarları](_static/AzureAppSettings.png)

<span data-ttu-id="b406c-131">Uygulama ayarı anahtarlarının biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b406c-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="b406c-132">Bu değer, Web kancalarının kaydedildiği *{ID}* değerleriyle eşleşen değerlerin virgülle ayrılmış bir listesidir, örneğin:</span><span class="sxs-lookup"><span data-stu-id="b406c-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="b406c-133">Web kancası alıcısı başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="b406c-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="b406c-134">Web kancası alıcıları, genellikle *WebApiConfig* statik sınıfında kaydederek başlatılır, örneğin:</span><span class="sxs-lookup"><span data-stu-id="b406c-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
