---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2,1-ASP.NET 4. x içinde BSON desteği
author: MikeWasson
description: BSON 'un bir Web API denetleyicisindeki (sunucu tarafında) ve ASP.NET 4. x için bir .NET istemci uygulamasındaki nasıl kullanılacağını gösterir.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: ccbc0372120301b1cd8d4cdc86bd9fba9404d8ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622299"
---
# <a name="bson-support-in-aspnet-web-api-21"></a>ASP.NET Web API 2,1 ' de BSON desteği

, [Mike te son](https://github.com/MikeWasson)

Bu konu, Web API denetleyicinizde (sunucu tarafında) ve bir .NET istemci uygulamasında BSON 'un nasıl kullanılacağını göstermektedir. Web API 2,1, BSON için destek sunar. 

## <a name="what-is-bson"></a>BSON nedir?

[BSon](http://bsonspec.org/) , ikili serileştirme biçimidir. "BSON", "binary JSON" anlamına gelir, ancak BSON ve JSON çok farklı şekilde serileştirilir. Nesneler JSON ile benzer şekilde ad-değer çiftleri olarak temsil edildiği için BSON "JSON benzeri" dir. JSON 'ın aksine, sayısal veri türleri dize değil, bayt olarak depolanır

BSON, basit, tarama kolay ve kodlama/kodu çözme hızlı olacak şekilde tasarlandı.

- BSON, JSON olarak boyut olarak karşılaştırılabilir. Verilere bağlı olarak bir BSON yükü, JSON yükünden daha küçük veya daha büyük olabilir. Bir görüntü dosyası gibi ikili verileri seri hale getirmek için, ikili veriler Base64 kodlamalı olmadığından BSON, JSON 'dan daha küçüktür.
- Bir uzunluğun bir uzunluk alanı ön ekine sahip olduğu için BSON belgelerinin taranması kolaydır. bu nedenle bir Ayrıştırıcı, öğeleri kod çözme olmadan atlayabilir.
- Kodlama ve kod çözme etkilidir, çünkü sayısal veri türleri dize değil, sayı olarak depolanır.

.NET istemci uygulamaları gibi yerel istemciler, JSON veya XML gibi metin tabanlı biçimlerin yerine BSON kullanma özelliğinden yararlanabilir. JavaScript doğrudan JSON yükünü dönüştürebildiğinden, tarayıcı istemcileri için muhtemelen JSON ile kontrol etmek isteyeceksiniz.

Neyse ki, Web API 'SI [içerik anlaşması](content-negotiation.md)kullanır, bu nedenle API 'niz her iki biçimi de destekleyebilir ve istemcinin seçmesini sağlayabilir.

## <a name="enabling-bson-on-the-server"></a>Sunucuda BSON etkinleştiriliyor

Web API yapılandırmanızda **bsonmediatypeformatter** ' ı biçimlendiricileri koleksiyonuna ekleyin.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

İstemci "Application/bSon" istediğinde, Web API BSON biçimlendirici 'yı kullanacaktır.

BSON 'u diğer medya türleriyle ilişkilendirmek için, bunları SupportedMediaTypes koleksiyonuna ekleyin. Aşağıdaki kod, desteklenen medya türlerine "application/vnd. contoso" ekler:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>Örnek HTTP oturumu

Bu örnekte, aşağıdaki model sınıfını ve basit bir Web API denetleyicisi kullanacağız:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

İstemci aşağıdaki HTTP isteğini gönderebilir:

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

Yanıt şu şekildedir:

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

Burada ikili verileri &quot;değiştirdim.&quot; karakterler. Fiddler 'dan aşağıdaki ekran görüntüsü ham onaltılık değerleri gösterir.

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>HttpClient ile BSON kullanma

.NET istemcileri uygulamaları, **HttpClient**Ile bSon biçimlendirici 'yi kullanabilir. **HttpClient**hakkında daha fazla bilgi için bkz. [.net istemcisinden Web API 'si çağırma](../advanced/calling-a-web-api-from-a-net-client.md).

Aşağıdaki kod BSON kabul eden bir GET isteği gönderir ve ardından yanıtta BSON yükü kaldırır.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

Sunucudan BSON istemek için Accept üst bilgisini "Application/bSon" olarak ayarlayın:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

Yanıt gövdesinin serisini kaldırmak için **Bsonmediatypeformatter**' ı kullanın. Bu biçimlendirici varsayılan biçimlendiricileri koleksiyonda değil, yanıt gövdesini okurken belirtmeniz gerekir:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

Sonraki örnek, BSON içeren bir POST isteğinin nasıl gönderileceğini gösterir.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

Bu kodun çoğu, önceki örnekle aynıdır. Ancak, **Postaeşitleme** yönteminde, biçimlendirici olarak **Bsonmediatypeformatter** belirtin:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>Üst düzey temel türler seri hale getiriliyor

Her BSON belge, anahtar/değer çiftleri listesidir. BSON belirtimi, bir tamsayı veya dize gibi tek bir ham değerin serileştirilmesi için bir sözdizimi tanımlamaz.

Bu sınırlamaya geçici bir çözüm bulmak için **Bsonmediatypeformatter** temel türleri özel bir durum olarak değerlendirir. Serileştirilden önce, değeri "Value" anahtarına sahip bir anahtar/değer çiftine dönüştürür. Örneğin, API denetleyicinizin bir tamsayı döndürdüğünü varsayalım:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

Seri hale getirmadan önce BSON biçimlendiricisi bunu şu anahtar/değer çiftine dönüştürür:

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

Seri durumdan çıkarma sırasında biçimlendirici, verileri özgün değerine geri dönüştürür. Ancak, Web API 'niz ham değerler döndürürse, farklı bir BSON ayrıştırıcısı kullanan istemcilerin bu durumu işlemesi gerekir. Genel olarak, ham değerler yerine yapılandırılmış verileri döndürmeyi göz önünde bulundurmanız gerekir.

## <a name="additional-resources"></a>Ek Kaynaklar

[Web API BSON örneği](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[Medya biçimleri](media-formatters.md)
