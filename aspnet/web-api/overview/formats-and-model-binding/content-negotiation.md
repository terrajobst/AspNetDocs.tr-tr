---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API-ASP.NET 4. x içinde içerik anlaşması
author: MikeWasson
description: ASP.NET Web API 'sinin ASP.NET 4. x için HTTP içerik anlaşmasını nasıl uyguladığını açıklar.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622271"
---
# <a name="content-negotiation-in-aspnet-web-api"></a>ASP.NET Web API 'de içerik anlaşması

, [Mike te son](https://github.com/MikeWasson)

Bu makalede, ASP.NET Web API 'sinin ASP.NET 4. x için içerik anlaşmasını nasıl uyguladığı açıklanır.

HTTP belirtimi (RFC 2616), "birden fazla temsili varsa belirli bir yanıt için en iyi temsili seçme işlemi" olarak içerik anlaşmasını tanımlar. HTTP 'de içerik anlaşmasına yönelik birincil mekanizma şu istek başlıklardır:

- **Kabul et:** "Application/JSON," application/xml "gibi yanıt için kabul edilebilir medya türleri veya &quot;application/vnd gibi özel bir medya türü. örnek + XML&quot;
- **Accept-Charset:** UTF-8 veya ISO 8859-1 gibi hangi karakter kümeleri kabul edilebilir.
- **Accept-Encoding:** Gzip gibi hangi içerik kodlamaları kabul edilebilir.
- **Accept-Language:** Tercih edilen doğal dil ("en-US" gibi).

Sunucu ayrıca HTTP isteğinin diğer bölümlerine da bakabilirler. Örneğin, istek bir AJAX isteği gösteren bir X-requested-with üst bilgisi içeriyorsa, Accept üst bilgisi yoksa sunucu JSON olarak varsayılan olabilir.

Bu makalede, Web API 'sinin Accept ve Accept-Charset üst bilgilerini nasıl kullandığını inceleyeceğiz. (Şu anda, Accept-Encoding veya Accept-Language için yerleşik destek yoktur.)

## <a name="serialization"></a>Serileştirme

Bir Web API denetleyicisi bir kaynağı CLR türü olarak döndürürse, işlem hattı döndürülen değeri serileştirir ve HTTP yanıt gövdesine yazar.

Örneğin, aşağıdaki denetleyici eylemini göz önünde bulundurun:

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

İstemci şu HTTP isteğini gönderebilir:

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

Yanıt olarak, sunucunun şunları gönderebileceğini:

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

Bu örnekte, istemci JSON, JavaScript veya "her şeyi" (\*/\*) istedi. Sunucu, `Product` nesnesinin JSON temsili ile yanıt verdi. Yanıttaki Içerik türü üstbilgisinin &quot;Application/JSON&quot;olarak ayarlandığını unutmayın.

Bir denetleyici, bir **HttpResponseMessage** nesnesi de döndürebilir. Yanıt gövdesi için bir CLR nesnesi belirtmek üzere **Createres,** Extension metodunu çağırın:

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

Bu seçenek, yanıtın ayrıntıları üzerinde daha fazla denetim sağlar. Durum kodunu ayarlayabilir, HTTP üst bilgileri ekleyebilir ve benzeri bir durumla devam edebilirsiniz.

Kaynağı serileştiren nesneye *medya biçimlendirici*denir. Medya formatlayıcıları, **MediaTypeFormatter** sınıfından türetilir. Web API 'si, XML ve JSON için medya biçimleri sağlar ve diğer medya türlerini desteklemek için özel biçimleri de oluşturabilirsiniz. Özel bir biçimlendirici yazma hakkında daha fazla bilgi için bkz. [medya biçimleri](media-formatters.md).

## <a name="how-content-negotiation-works"></a>Içerik anlaşması nasıl kullanılır?

İlk olarak, işlem hattı **HttpConfiguration** nesnesinden **ıtentnegotiator** hizmetini alır. Ayrıca, **HttpConfiguration. biçimlendiricileri** koleksiyonundan medya formatlayıcıları listesini alır.

Sonra, işlem hattı **ıditentnegotiator. Negotiate**çağırır, geçirme:

- Seri hale getirilecek nesnenin türü
- Medya formatlayıcıları koleksiyonu
- HTTP isteği

**Negotiate** yöntemi iki bilgi parçası döndürür:

- Kullanılacak biçimlendirici
- Yanıt için medya türü

Bir biçimlendirici bulunmazsa, **Negotiate** yöntemi **null**DEĞERINI döndürür ve istemci http hatası 406 (kabul edilemez) alır.

Aşağıdaki kod, bir denetleyicinin içerik anlaşmasını doğrudan nasıl çağırabileceği gösterilmektedir:

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

Bu kod, işlem hattının otomatik olarak ne olduğuna eşdeğerdir.

## <a name="default-content-negotiator"></a>Varsayılan Içerik Negotiator

**Defaultcontentnegotiator** sınıfı, **ıtenttrnegotiator**'ın varsayılan uygulamasını sağlar. Bir biçimlendirici seçmek için birkaç ölçüt kullanır.

İlk olarak, biçimlendirici türü seri hale getirmek için gereklidir. Bu, **MediaTypeFormatter. CanWriteType**çağırarak doğrulanır.

Ardından, içerik Negotiator her bir biçimlendirici üzerinde bakar ve HTTP isteğiyle ne kadar iyi eşleşme olduğunu değerlendirir. Eşleşmeyi değerlendirmek için, içerik Negotiator, biçimlendirici üzerinde iki şeyi arar:

- Desteklenen medya türlerinin bir listesini içeren **Supportedmediatypes** koleksiyonu. İçerik Negotiator, istek kabul üstbilgisiyle bu listeyi eşleştirmeye çalışır. Accept üst bilgisinin aralıklar içerebileceğini unutmayın. Örneğin, "metin/düz" metin/\* veya \*/\*için bir eşleşmedir.
- **MediaTypeMapping** nesnelerinin bir listesini Içeren **mediatypemappings** koleksiyonu. **MediaTypeMapping** sınıfı, medya türleriyle http isteklerini eşleştirmek için genel bir yol sağlar. Örneğin, özel bir HTTP üst bilgisini belirli bir medya türüyle eşleyebilir.

Birden çok eşleşme varsa, en yüksek kalite faktörüyle eşleşme kazanır. Örneğin:

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

Bu örnekte, Application/JSON 'ın kapsanan bir kalite faktörü 1,0, bu nedenle application/xml üzerinden tercih edilir.

Hiçbir eşleşme bulunmazsa, içerik Negotiator, varsa istek gövdesinin medya türüyle eşleştirmeye çalışır. Örneğin, istek JSON verisi içeriyorsa, içerik Negotiator bir JSON biçimlendiricisi arar.

Hala eşleşme yoksa, Negotiator, türü seri hale getirmek için yalnızca ilk biçimlendirici seçer.

## <a name="selecting-a-character-encoding"></a>Bir karakter kodlaması seçme

Bir biçimlendirici seçildikten sonra, içerik Negotiator, biçimlendirici üzerindeki **Supportedencoular** özelliğine bakarak en iyi karakter kodlamasını seçer ve istekteki Accept-Charset üstbilgisine (varsa) karşılık gelir.
