---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2-ASP.NET 4. x ile eylem sonuçları
author: MikeWasson
description: ASP.NET Web API 'sinin döndürülen değeri bir denetleyici eyleminden ASP.NET 4. x içinde HTTP yanıt iletisine nasıl dönüştüreceğini açıklar.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557059"
---
# <a name="action-results-in-web-api-2"></a>Web API 2’de Eylem Sonuçları

[!INCLUDE[](~/includes/coreWebAPI.md)]

Bu konu, ASP.NET Web API 'sinin geri dönüş değerini bir denetleyici eyleminden bir HTTP yanıt iletisine nasıl dönüştürdüğü açıklanmaktadır.

Bir Web API denetleyicisi eylemi aşağıdakilerden herhangi birini döndürebilir:

1. void
2. **HttpResponseMessage**
3. **Ihttpactionresult**
4. Diğer bir tür

Bunların ne olduğuna bağlı olarak, Web API 'SI, HTTP yanıtı oluşturmak için farklı bir mekanizma kullanır.

| Dönüş türü | Web API 'sinin yanıtı nasıl oluşturur |
| --- | --- |
| void | Boş 204 döndürün (Içerik yok) |
| **HttpResponseMessage** | Doğrudan bir HTTP yanıt iletisine dönüştürün. |
| **Ihttpactionresult** | Bir **HttpResponseMessage**oluşturmak Için **ExecuteAsync** çağrısı YAPıN ve ardından bir http yanıt iletisine dönüştürün. |
| Diğer tür | Serileştirilmiş dönüş değerini yanıt gövdesine yazın; 200 döndürün (Tamam). |

Bu konunun geri kalanında her bir seçenek daha ayrıntılı olarak açıklanmaktadır.

## <a name="void"></a>void

Dönüş türü `void`ise, Web API 'SI yalnızca 204 (Içerik yok) durum koduna sahip bir boş HTTP yanıtı döndürür.

Örnek denetleyici:

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP yanıtı:

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

Eylem bir [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)döndürürse, Web API 'si, yanıtı doldurmak Için **HttpResponseMessage** nesnesinin özelliklerini kullanarak döndürülen değeri doğrudan bir http yanıt iletisine dönüştürür.

Bu seçenek, yanıt iletisi üzerinde çok fazla denetim sağlar. Örneğin, aşağıdaki denetleyici eylemi Cache-Control üst bilgisini ayarlar.

[!code-csharp[Main](action-results/samples/sample3.cs)]

Yanıt:

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

Bir etki alanı modelini **Createresbir** yöntemine geçirirseniz, Web API 'si, serileştirilmiş modeli yanıt gövdesine yazmak için bir [medya biçimlendirici](../formats-and-model-binding/media-formatters.md) kullanır.

[!code-csharp[Main](action-results/samples/sample5.cs)]

Web API 'SI, biçimlendirici 'yi seçmek için istekteki Accept üst bilgisini kullanır. Daha fazla bilgi için bkz. [Içerik anlaşması](../formats-and-model-binding/content-negotiation.md).

## <a name="ihttpactionresult"></a>IHttpActionResult

**Ihttpactionresult** ARABIRIMI Web API 2 ' de tanıtılmıştı. Temelde, bir **HttpResponseMessage** fabrikası tanımlar. **Ihttpactionresult** arabirimini kullanmanın bazı avantajları aşağıda verilmiştir:

- Denetleyicileriniz için [birim testini](../testing-and-debugging/unit-testing-controllers-in-web-api.md) basitleştirir.
- Ayrı sınıflara HTTP yanıtları oluşturmak için ortak mantığı taşımaktır.
- , Yanıtı oluşturan alt düzey ayrıntıları gizleyerek, denetleyici eyleminin amacını daha net hale getirir.

**Ihttpactionresult** , zaman uyumsuz olarak bir **HttpResponseMessage** örneği oluşturan **ExecuteAsync**tek bir yöntem içerir.

[!code-csharp[Main](action-results/samples/sample6.cs)]

Bir denetleyici eylemi bir **ıhttpactionresult**döndürürse, Web API 'Si bir **HttpResponseMessage**oluşturmak için **ExecuteAsync** yöntemini çağırır. Daha sonra **HttpResponseMessage** 'YI bir http yanıt iletisine dönüştürür.

Bir düz metin yanıtı oluşturan **ıhttpactionresult** öğesinin basit bir uygulaması aşağıda verilmiştir:

[!code-csharp[Main](action-results/samples/sample7.cs)]

Örnek denetleyici eylemi:

[!code-csharp[Main](action-results/samples/sample8.cs)]

Yanıt:

[!code-console[Main](action-results/samples/sample9.cmd)]

Daha sık, **[System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** ad alanında tanımlanan **ıhttpactionresult** uygulamalarını kullanırsınız. **Apicontroller** sınıfı, bu yerleşik eylem sonuçlarını döndüren yardımcı yöntemleri tanımlar.

Aşağıdaki örnekte, istek mevcut bir ürün KIMLIĞIYLE eşleşmezse, denetleyici bir 404 (bulunamadı) yanıtı oluşturmak için [Apicontroller. NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) yöntemini çağırır. Aksi takdirde, denetleyici, ürünü içeren bir 200 (Tamam) yanıtı oluşturan [Apicontroller. ok](https://msdn.microsoft.com/library/dn314591.aspx)öğesini çağırır.

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>Diğer dönüş türleri

Diğer tüm dönüş türleri için Web API 'SI, dönüş değerini seri hale getirmek için bir [medya biçimlendirici](../formats-and-model-binding/media-formatters.md) kullanır. Web API 'SI, serileştirilmiş değeri yanıt gövdesine yazar. Yanıt durum kodu 200 ' dir (Tamam).

[!code-csharp[Main](action-results/samples/sample11.cs)]

Bu yaklaşımın bir dezavantajı, 404 gibi doğrudan bir hata kodu döndürmemelidir. Ancak, hata kodları için bir **Httpresponseexception** oluşturabilirsiniz. Daha fazla bilgi için bkz. [ASP.NET Web API 'de özel durum işleme](../error-handling/exception-handling.md).

Web API 'SI, biçimlendirici 'yi seçmek için istekteki Accept üst bilgisini kullanır. Daha fazla bilgi için bkz. [Içerik anlaşması](../formats-and-model-binding/content-negotiation.md).

Örnek istek

[!code-console[Main](action-results/samples/sample12.cmd)]

Örnek yanıt

[!code-console[Main](action-results/samples/sample13.cmd)]
