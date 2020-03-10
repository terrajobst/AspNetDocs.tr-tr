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
# <a name="aspnet-webhooks-receivers"></a>ASP.NET Web kancaları alıcıları

Web kancalarını alma, gönderenin kim olduğuna bağlıdır. Bazen, abonenin gerçekten dinlediğini doğrulayan bir Web kancası kaydı için ek adımlar vardır. Bazı Web kancaları, HTTP POST isteğinin yalnızca bağımsız olarak alınabilecek olay bilgilerine bir başvuru içerdiği bir istek temelli model sağlar. Genellikle güvenlik modeli oldukça bir bit olarak değişir.

Web kancaları Microsoft ASP.NET amacı, Web kancalarının belirli bir çeşitlerini nasıl işleyeceğinizi öğrenmek zorunda kalmadan API 'nizi daha basit ve daha tutarlı hale getirir.

Web kancası alıcısı, belirli bir gönderenden Web kancalarını kabul edip doğrulamaktan sorumludur. Web kancası alıcısı, her biri kendi yapılandırmasına sahip olan herhangi bir sayıda Web kancasını destekleyebilir. Örneğin, GitHub Web kancası alıcısı herhangi bir sayıdaki GitHub depoağından Web kancalarını kabul edebilir.

## <a name="webhook-receiver-uris"></a>Web kancası alıcı URI 'Leri

Microsoft ASP.NET Web kancaları yükleyerek, açık uçlu hizmetlerden gelen Web kancası isteklerini kabul eden genel bir Web kancası denetleyicisi alırsınız. Bir istek geldiğinde, belirli bir Web kancası Göndericisini işlemek için yüklediğiniz uygun alıcıyı seçer.

Bu denetleyicinin URI 'si, hizmete kaydolmanızı sağlayan Web kancası URI 'sidir ve şu biçimdedir:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

Güvenlik nedenleriyle birçok Web kancası alıcısı URI 'nin bir *https* URI olmasını gerektirir ve bazı durumlarda, yalnızca amaçlanan TARAFıN yukarıdaki URI 'ye Web kancaları gönderebildiğini zorlamak için kullanılan ek bir sorgu parametresi de içermelidir.

`<receiver>` bileşen alıcının adı, örneğin `github` veya `slack`.

*{İd}* , belirli bir Web kancası alıcı yapılandırmasını tanımlamak için kullanılabilen isteğe bağlı bir tanıtıcıdır. Bu, belirli bir alıcı ile N Web kancalarını kaydetmek için kullanılabilir. Örneğin, aşağıdaki üç URI üç bağımsız Web kancalarına kaydolmak için kullanılabilir:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>Web kancası alıcısı yükleme

Web kancalarını Microsoft ASP.NET kullanarak Web kancaları almak için, önce Web kancaları almak istediğiniz Web kancası sağlayıcısı veya sağlayıcıları için NuGet paketini yüklersiniz. NuGet paketleri, son bölümün desteklenen hizmeti gösterdiği [Microsoft. Aspnet. Webkancaları. alıcılar. *](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) olarak adlandırılır. Örneğin:

[Microsoft. Aspnet. Webkancalar. alıcılar. GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) , GitHub 'Dan ve [Microsoft. Aspnet. Webkancaları. alıcılar. alıcıları](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) tarafından oluşturulan Web kancalarını almak için destek sağlar.

Box, GitHub, MailChimp, PayPal, Iletici, Salesforce, bolluk, Stripe, Trello ve WordPress için destek bulabilirsiniz, ancak herhangi bir sayıda diğer sağlayıcıyı desteklemek mümkündür.

## <a name="configuring-a-webhook-receiver"></a>Web kancası alıcısını yapılandırma

Web kancası alıcıları [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) arabirimini aracılığıyla yapılandırılır ve bu arabirimin belirli uygulamaları herhangi bir bağımlılık ekleme modeli kullanılarak kaydedilebilir. Varsayılan uygulama, Web. config dosyasında ayarlanmış olan veya Azure Web Apps kullanılıyorsa [Azure portalından](https://portal.azure.com/)ayarlanabilir olan uygulama ayarlarını kullanır.

![Azure Uygulama ayarları](_static/AzureAppSettings.png)

Uygulama ayarı anahtarlarının biçimi aşağıdaki gibidir:

```
MS_WebHookReceiverSecret_<receiver>
```

Bu değer, Web kancalarının kaydedildiği *{ID}* değerleriyle eşleşen değerlerin virgülle ayrılmış bir listesidir, örneğin:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>Web kancası alıcısı başlatılıyor

Web kancası alıcıları, genellikle *WebApiConfig* statik sınıfında kaydederek başlatılır, örneğin:

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
