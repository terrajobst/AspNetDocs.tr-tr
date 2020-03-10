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
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 'sinde HttpClient Ileti Işleyicileri

, [Mike te son](https://github.com/MikeWasson)

*İleti işleyicisi* , http isteği alan ve http yanıtı döndüren bir sınıftır.

Genellikle, bir dizi ileti işleyicisi birlikte zincirleme yapılır. İlk işleyici bir HTTP isteği alır, bazı işlemleri yapar ve isteği bir sonraki işleyiciye verir. Bir noktada yanıt oluşturulur ve zinciri yedekler. Bu düzene *temsilci seçme* işleyicisi denir.

![](httpclient-message-handlers/_static/image1.png)

İstemci tarafında, **HttpClient** sınıfı istekleri işlemek için bir ileti işleyicisi kullanır. Varsayılan işleyici, isteği ağ üzerinden gönderen ve sunucudan gelen yanıtı alan **HttpClientHandler**' dir. İstemci ardışık düzenine özel ileti işleyicileri ekleyebilirsiniz:

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> ASP.NET Web API 'SI Ayrıca sunucu tarafında ileti işleyicileri kullanır. Daha fazla bilgi için bkz. [http Ileti işleyicileri](http-message-handlers.md).

## <a name="custom-message-handlers"></a>Özel Ileti Işleyicileri

Özel bir ileti işleyicisi yazmak için, **System .net. http. DelegatingHandler** 'ten türetirsiniz ve **sendadsync** yöntemini geçersiz kılın. Yöntem imzası şöyledir:

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

Yöntemi, giriş olarak bir **HttpRequestMessage** alır ve zaman uyumsuz bir **HttpResponseMessage**döndürür. Tipik bir uygulama şunları yapar:

1. İstek iletisini işleyin.
2. İsteği iç işleyiciye göndermek için `base.SendAsync` çağırın.
3. İç işleyici bir yanıt iletisi döndürür. (Bu adım zaman uyumsuzdur.)
4. Yanıtı işleyin ve çağırana döndürün.

Aşağıdaki örnek, giden istek için özel üst bilgi ekleyen bir ileti işleyicisini gösterir:

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

`base.SendAsync` çağrısı zaman uyumsuzdur. İşleyici Bu çağrıdan sonra herhangi bir iş yaparsanız, yöntemi tamamlandıktan sonra yürütmeyi sürdürmeye yönelik **await** anahtar sözcüğünü kullanın. Aşağıdaki örnek, hata kodlarını günlüğe kaydeden bir işleyiciyi gösterir. Günlüğe kaydetme işlemi çok ilginç değildir, ancak örnek işleyicinin içindeki yanıta nasıl alınacağını gösterir.

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>Istemci ardışık düzenine Ileti Işleyicileri ekleme

**HttpClient**'a özel işleyiciler eklemek Için **Httpclientfactory. Create** metodunu kullanın:

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

İleti işleyicileri, **oluşturma** yöntemine geçirdiğiniz sırada çağırılır. İşleyiciler iç içe olduğundan, yanıt iletisi diğer yönde dolaşır. Diğer bir deyişle, son işleyici yanıt iletisini ilk kez alır.
