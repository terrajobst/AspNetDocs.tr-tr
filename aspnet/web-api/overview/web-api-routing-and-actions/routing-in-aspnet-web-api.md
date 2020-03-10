---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 'SI içinde yönlendirme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557612"
---
# <a name="routing-in-aspnet-web-api"></a>ASP.NET Web API'de yönlendirme

, [Mike te son](https://github.com/MikeWasson)

Bu makalede, ASP.NET Web API 'SI, HTTP isteklerini denetleyicilere nasıl yönlendirdiğini açıklar.

> [!NOTE]
> ASP.NET MVC hakkında bilgi sahibiyseniz, Web API yönlendirmesi MVC yönlendirmeye çok benzer. Temel fark, Web API 'sinin eylemi seçmek için URI yolunu değil HTTP fiilini kullanması gerektiğidir. Ayrıca, Web API 'sinde MVC stili yönlendirmeyi de kullanabilirsiniz. Bu makalede, ASP.NET MVC hakkında herhangi bir bilgi varsayılmaktadır.

## <a name="routing-tables"></a>Yönlendirme tabloları

ASP.NET Web API 'sinde, *DENETLEYICI* http isteklerini işleyen bir sınıftır. Denetleyicinin genel yöntemlerine *eylem yöntemleri* veya yalnızca *Eylemler*denir. Web API çerçevesi bir istek aldığında, isteği bir eyleme yönlendirir.

Hangi eylemin çalıştırılacağını öğrenmek için Framework bir *yönlendirme tablosu*kullanır. Web API 'SI için Visual Studio proje şablonu varsayılan bir yol oluşturur:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

Bu yol, *uygulama\_başlangıç* dizinine yerleştirilmiş *WebApiConfig.cs* dosyasında tanımlanır:

![](routing-in-aspnet-web-api/_static/image1.png)

`WebApiConfig` sınıfı hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'Sini yapılandırma](../advanced/configuring-aspnet-web-api.md).

Web API 'sini Self barındırdıysanız, yönlendirme tablosunu doğrudan `HttpSelfHostConfiguration` nesnesi üzerinde ayarlamanız gerekir. Daha fazla bilgi için bkz. [kendi kendine konak bir Web API 'si](../older-versions/self-host-a-web-api.md).

Yönlendirme tablosundaki her giriş bir *yol şablonu*içerir. Web API 'si için varsayılan yol şablonu &quot;API/{Controller}/{id}&quot;. Bu şablonda &quot;API&quot; bir değişmez değer segmenti ve {Controller} ve {id} yer tutucu değişkenleridir.

Web API çerçevesi bir HTTP isteği aldığında, URI 'yi yönlendirme tablosundaki yol şablonlarından biriyle eşleştirmeye çalışır. Hiçbir yol eşleşirse, istemci bir 404 hatası alır. Örneğin, aşağıdaki URI 'Ler varsayılan yol ile eşleşir:

- /api/Contacts
- /api/Contacts/1
- /api/products/gizmo1

Ancak, &quot;API&quot; segmentinden olmadığından aşağıdaki URI eşleşmez:

- /Contacts/1

> [!NOTE]
> Yol içinde "API" kullanmanın nedeni ASP.NET MVC yönlendirme ile çarpışmalardan kaçınmaktır. Böylece, bir MVC denetleyicisine &quot;/Contacts&quot; ve/api/&quot; Contacts &quot;bir Web API denetleyicisine gidebilirsiniz. Kuşkusuz, bu kuralı beğenmezseniz varsayılan yol tablosunu değiştirebilirsiniz.

Eşleşen bir yol bulunduğunda Web API 'SI denetleyiciyi ve eylemi seçer:

- Denetleyiciyi bulmak için Web API 'SI, *{Controller}* değişkeninin değerine&quot; &quot;denetleyicisi ekler.
- Eylemi bulmak için Web API 'SI HTTP fiiline bakar ve sonra adı bu HTTP fiili adıyla başlayan bir eylem arar. Örneğin, GET isteğiyle, Web API 'SI &quot;GetContact&quot; veya &quot;GetAllContacts&quot;gibi &quot;alma&quot;önekli bir eylem arar. Bu kural yalnızca GET, POST, PUT, DELETE, HEAD, OPTIONS ve PATCH fiilleri için geçerlidir. Denetleyicinizdeki öznitelikleri kullanarak diğer HTTP fiillerini etkinleştirebilirsiniz. Daha sonra bir örnek görürsünüz.
- Yol şablonundaki *{ID}* gibi diğer yer tutucu değişkenleri eylem parametreleriyle eşleştirilir.

Şimdi örneği inceleyelim. Aşağıdaki denetleyiciyi tanımladığınızı varsayalım:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

İşte, her biri için çağrılan eylem ile birlikte bazı olası HTTP istekleri şunlardır:

| HTTP fiili | URI yolu | Eylem | Parametre |
| --- | --- | --- | --- |
| GET | API/ürünler | GetAllProducts | *seçim* |
| GET | API/ürünler/4 | GetProductById | 4 |
| DELETE | API/ürünler/4 | DeleteProduct | 4 |
| POST | API/ürünler | *(eşleşme yok)* |  |

Varsa URI 'nin *{id}* segmentinin, eylemin *kimlik* parametresine eşlendiğine dikkat edin. Bu örnekte, denetleyici bir *ID* parametresi ve biri parametresi olmayan iki GET yöntemini tanımlar.

Ayrıca, denetleyici bir &quot;Post...&quot; yöntemi tanımlamadığı için POST isteğinin başarısız olacağını unutmayın.

## <a name="routing-variations"></a>Yönlendirme çeşitlemeleri

Önceki bölümde ASP.NET Web API 'SI için temel yönlendirme mekanizması açıklanmaktadır. Bu bölümde bazı Çeşitlemeler açıklanmaktadır.

### <a name="http-verbs"></a>HTTP fiilleri

HTTP fiilleri için adlandırma kuralını kullanmak yerine, eylem yöntemini aşağıdaki özniteliklerden biriyle dekoratarak bir eylem için HTTP fiilini açık bir şekilde belirtebilirsiniz:

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

Aşağıdaki örnekte `FindProduct` yöntemi GET istekleri ile eşlenir:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

Bir eylem için birden çok HTTP fiillerine izin vermek veya GET, PUT, POST, DELETE, HEAD, OPTIONS ve PATCH dışındaki HTTP fiillerine izin vermek için, HTTP fiillerinin bir listesini alan `[AcceptVerbs]` özniteliğini kullanın.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>Eylem adına göre yönlendirme

Varsayılan yönlendirme şablonuyla, Web API 'SI eylemi seçmek için HTTP fiilini kullanır. Bununla birlikte, işlem adının URI 'ye dahil edildiği bir yol da oluşturabilirsiniz:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

Bu yol şablonunda, *{Action}* parametresi denetleyicisindeki eylem yöntemini adlandırır. Bu yönlendirme stili ile, izin verilen HTTP fiillerini belirtmek için özniteliklerini kullanın. Örneğin, denetleyicinizin aşağıdaki yöntemi olduğunu varsayalım:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

Bu durumda, "API/ürünler/Ayrıntılar/1" için bir GET isteği `Details` yöntemi ile eşlenir. Bu yönlendirme stili ASP.NET MVC ile benzerdir ve bir RPC stili API 'SI için uygun olabilir.

`[ActionName]` özniteliğini kullanarak eylem adını geçersiz kılabilirsiniz. Aşağıdaki örnekte, API/ürünler/küçük resim/*kimlik*&quot;eşlenen iki eylem vardır. Bunlardan biri GET 'i destekler ve diğeri GÖNDERISINI destekler:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>Eylem dışı

Bir yöntemin eylem olarak çağrılmasını engellemek için `[NonAction]` özniteliğini kullanın. Bu, başka bir işlem yönlendirme kurallarıyla eşleşse bile, yöntemin bir eylem olmadığı çerçeveye işaret eder.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu konu, yönlendirmenin üst düzey bir görünümünü sağladı. Daha fazla ayrıntı için bkz. [Yönlendirme ve eylem seçimi](routing-and-action-selection.md); bu, ÇERÇEVENIN bir URI ile bir yol ile nasıl eşleştiğini açıklar, bir denetleyiciyi seçer ve ardından çağrılacak eylemi seçer.
