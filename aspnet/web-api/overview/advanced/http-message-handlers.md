---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API 'SI içindeki HTTP Ileti Işleyicileri-ASP.NET 4. x
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Web API 'sindeki HTTP ileti işleyicilerine genel bakış
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622586"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 'de HTTP Ileti Işleyicileri

, [Mike te son](https://github.com/MikeWasson)

*İleti işleyicisi* , http isteği alan ve http yanıtı döndüren bir sınıftır. İleti işleyicileri soyut **HttpMessageHandler** sınıfından türetilir.

Genellikle, bir dizi ileti işleyicisi birlikte zincirleme yapılır. İlk işleyici bir HTTP isteği alır, bazı işlemleri yapar ve isteği bir sonraki işleyiciye verir. Bir noktada yanıt oluşturulur ve zinciri yedekler. Bu düzene *temsilci seçme* işleyicisi denir.

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a>Sunucu tarafı Ileti Işleyicileri

Sunucu tarafında, Web API 'SI ardışık düzeni bazı yerleşik ileti işleyicileri kullanır:

- **HttpServer** , konaktan gelen isteği alır.
- **Httproutingdispatcher** , isteği yola göre dağıtır.
- **Httpcontrollerdispatcher** , Isteği BIR Web API denetleyicisine gönderir.

Komut hattına özel işleyiciler ekleyebilirsiniz. İleti işleyicileri, HTTP iletileri düzeyinde (denetleyici eylemleri yerine) çalışan çapraz kesme sorunları için uygundur. Örneğin, bir ileti işleyicisi şunları içerebilir:

- İstek üst bilgilerini okuyun veya değiştirin.
- Yanıtlara bir yanıt üst bilgisi ekleyin.
- İstekleri denetleyiciye ulaşmadan önce doğrulayın.

Bu diyagramda, ardışık düzene yerleştirilmiş iki özel işleyici gösterilmektedir:

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> İstemci tarafında HttpClient Ayrıca ileti işleyicilerini kullanır. Daha fazla bilgi için bkz. [HttpClient Ileti işleyicileri](httpclient-message-handlers.md).

## <a name="custom-message-handlers"></a>Özel Ileti Işleyicileri

Özel bir ileti işleyicisi yazmak için, **System .net. http. DelegatingHandler** 'ten türetirsiniz ve **sendadsync** yöntemini geçersiz kılın. Bu yöntem aşağıdaki imzaya sahiptir:

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

Yöntemi, giriş olarak bir **HttpRequestMessage** alır ve zaman uyumsuz bir **HttpResponseMessage**döndürür. Tipik bir uygulama şunları yapar:

1. İstek iletisini işleyin.
2. İsteği iç işleyiciye göndermek için `base.SendAsync` çağırın.
3. İç işleyici bir yanıt iletisi döndürür. (Bu adım zaman uyumsuzdur.)
4. Yanıtı işleyin ve çağırana döndürün.

Önemsiz bir örnek aşağıda verilmiştir:

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> `base.SendAsync` çağrısı zaman uyumsuzdur. İşleyici Bu çağrıdan sonra herhangi bir çalışmayı yapar, gösterildiği gibi **await** anahtar sözcüğünü kullanın.

Ayrıca, bir temsilci işleyicisi iç işleyiciyi atlayabilir ve yanıtı doğrudan oluşturabilir:

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

Bir temsilci işleyicisi `base.SendAsync`çağrılmadan yanıt oluşturursa, istek işlem hattının geri kalanını atlar. Bu, isteği doğrulayan bir işleyici için yararlı olabilir (hata yanıtı oluşturma).

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a>İşlem hattına Işleyici ekleme

Sunucu tarafında bir ileti işleyicisi eklemek için, işleyiciyi **HttpConfiguration. MessageHandlers** koleksiyonuna ekleyin. Projeyi oluşturmak için "ASP.NET MVC 4 Web uygulaması" şablonunu kullandıysanız, bunu **WebApiConfig** sınıfının içinde yapabilirsiniz:

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

İleti işleyicileri **Messagehandlers** koleksiyonunda göründükleri sırada çağrılır. İç içe olduklarından yanıt iletisi diğer yönde hareket eder. Diğer bir deyişle, son işleyici yanıt iletisini ilk kez alır.

İç işleyicileri ayarlamanız gerekmez; Web API çerçevesi, ileti işleyicilerini otomatik olarak bağlar.

[Kendi kendine barındırıyorsanız](../older-versions/self-host-a-web-api.md), **Httpselfhostconfiguration** sınıfının bir örneğini oluşturun ve işleyicileri **messagehandlers** koleksiyonuna ekleyin.

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

Şimdi özel ileti işleyicilerinin bazı örneklerine göz atalım.

## <a name="example-x-http-method-override"></a>Örnek: X-HTTP-Method-override

X-HTTP-Method-override standart olmayan bir HTTP üst bilgisi. PUT veya DELETE gibi belirli HTTP istek türlerini gönderemediği istemciler için tasarlanmıştır. Bunun yerine, istemci bir POST isteği gönderir ve X-HTTP-Method-override üst bilgisini istenen metoda ayarlar. Örneğin:

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

X-HTTP-Method-override için destek ekleyen bir ileti işleyicisi aşağıda verilmiştir:

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

**Sendadsync** yönteminde, işleyici istek ILETISININ bir post isteği olup olmadığını ve X-http-Method-override üst bilgisini içerip içermediğini denetler. Bu durumda, üst bilgi değerini doğrular ve sonra istek metodunu değiştirir. Son olarak, işleyici iletiyi sonraki işleyiciye geçirmek için `base.SendAsync` çağırır.

İstek **httpcontrollerdispatcher** sınıfına ulaştığında, **httpcontrollerdispatcher** isteği güncelleştirilmiş istek yöntemine göre yönlendirir.

## <a name="example-adding-a-custom-response-header"></a>Örnek: özel yanıt üst bilgisi ekleme

Her yanıt iletisine özel bir üst bilgi ekleyen bir ileti işleyicisi aşağıda verilmiştir:

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

İlk olarak, işleyici isteği iç ileti işleyicisine geçirmek için `base.SendAsync` çağırır. İç işleyici bir yanıt iletisi döndürür, ancak bunu zaman uyumsuz bir **görev&lt;t&gt;** nesnesi kullanarak yapar. Yanıt iletisi `base.SendAsync` zaman uyumsuz olarak tamamlanana kadar kullanılamaz.

Bu örnek, `SendAsync` tamamlandıktan sonra zaman uyumsuz olarak çalışmayı gerçekleştirmek için **await** anahtar sözcüğünü kullanır. .NET Framework 4,0 ' i hedefliyorsanız,&lt;T&gt;**görevini** kullanın **. Yönteme devam** edin:

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a>Örnek: bir API anahtarı denetleniyor

Bazı Web Hizmetleri, istemcilerin istemesi için bir API anahtarı içermesini gerektirir. Aşağıdaki örnek bir ileti işleyicisinin geçerli bir API anahtarı için istekleri nasıl denetlegösterdiğini gösterir:

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

Bu işleyici, URI sorgu dizesinde API anahtarını arar. (Bu örnekte, anahtarın bir statik dize olduğunu varsaytık. Gerçek bir uygulama, büyük olasılıkla daha karmaşık doğrulama kullanır.) Sorgu dizesi anahtarı içeriyorsa, işleyici isteği iç işleyiciye geçirir.

İstek geçerli bir anahtara sahip değilse, işleyici durum 403 olan bir yanıt iletisi oluşturur, yasak. Bu durumda, işleyici `base.SendAsync`çağırmaz, bu nedenle iç işleyici isteği hiçbir şekilde almaz veya denetleyici yapmaz. Bu nedenle, denetleyici tüm gelen isteklerin geçerli bir API anahtarı olduğunu varsayabilir.

> [!NOTE]
> API anahtarı yalnızca belirli denetleyici eylemlerine geçerliyse, ileti işleyicisi yerine bir eylem filtresi kullanmayı düşünün. İşlem filtreleri URI yönlendirmesi gerçekleştirildikten sonra çalışır.

## <a name="per-route-message-handlers"></a>Yol başına Ileti Işleyicileri

**HttpConfiguration. messagehandlers** koleksiyonundaki işleyiciler küresel olarak uygulanır.

Alternatif olarak, yolu tanımlarken belirli bir yola bir ileti işleyicisi ekleyebilirsiniz:

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

Bu örnekte, istek URI 'SI "Route2" ile eşleşiyorsa, istek `MessageHandler2`gönderilir. Aşağıdaki diyagramda bu iki yolun işlem hattı gösterilmektedir:

![](http-message-handlers/_static/image4.png)

`MessageHandler2` varsayılan **Httpcontrollerdispatcher**'ın yerini aldığını unutmayın. Bu örnekte, `MessageHandler2` yanıtı oluşturur ve "Route2" ile eşleşen istekler hiçbir şekilde denetleyiciye gitmez. Bu, tüm Web API denetleyici mekanizmasını kendi özel uç noktanızla değiştirmenize olanak sağlar.

Alternatif olarak, yönlendirme başına ileti işleyicisi, daha sonra bir denetleyiciye dağıtırsa **Httpcontrollerdispatcher**öğesine temsilci seçebilir.

![](http-message-handlers/_static/image5.png)

Aşağıdaki kod, bu yolun nasıl yapılandırılacağını göstermektedir:

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
