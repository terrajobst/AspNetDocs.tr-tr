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
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519342"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="df840-103">ASP.NET Web API 2,1 ' de BSON desteği</span><span class="sxs-lookup"><span data-stu-id="df840-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="df840-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="df840-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="df840-105">Bu konu, Web API denetleyicinizde (sunucu tarafında) ve bir .NET istemci uygulamasında BSON 'un nasıl kullanılacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="df840-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="df840-106">Web API 2,1, BSON için destek sunar.</span><span class="sxs-lookup"><span data-stu-id="df840-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="df840-107">BSON nedir?</span><span class="sxs-lookup"><span data-stu-id="df840-107">What is BSON?</span></span>

<span data-ttu-id="df840-108">[BSon](http://bsonspec.org/) , ikili serileştirme biçimidir.</span><span class="sxs-lookup"><span data-stu-id="df840-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="df840-109">"BSON", "binary JSON" anlamına gelir, ancak BSON ve JSON çok farklı şekilde serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="df840-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="df840-110">Nesneler JSON ile benzer şekilde ad-değer çiftleri olarak temsil edildiği için BSON "JSON benzeri" dir.</span><span class="sxs-lookup"><span data-stu-id="df840-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="df840-111">JSON 'ın aksine, sayısal veri türleri dize değil, bayt olarak depolanır</span><span class="sxs-lookup"><span data-stu-id="df840-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="df840-112">BSON, basit, tarama kolay ve kodlama/kodu çözme hızlı olacak şekilde tasarlandı.</span><span class="sxs-lookup"><span data-stu-id="df840-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="df840-113">BSON, JSON olarak boyut olarak karşılaştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="df840-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="df840-114">Verilere bağlı olarak bir BSON yükü, JSON yükünden daha küçük veya daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="df840-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="df840-115">Bir görüntü dosyası gibi ikili verileri seri hale getirmek için, ikili veriler Base64 kodlamalı olmadığından BSON, JSON 'dan daha küçüktür.</span><span class="sxs-lookup"><span data-stu-id="df840-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="df840-116">Bir uzunluğun bir uzunluk alanı ön ekine sahip olduğu için BSON belgelerinin taranması kolaydır. bu nedenle bir Ayrıştırıcı, öğeleri kod çözme olmadan atlayabilir.</span><span class="sxs-lookup"><span data-stu-id="df840-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="df840-117">Kodlama ve kod çözme etkilidir, çünkü sayısal veri türleri dize değil, sayı olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="df840-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="df840-118">.NET istemci uygulamaları gibi yerel istemciler, JSON veya XML gibi metin tabanlı biçimlerin yerine BSON kullanma özelliğinden yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="df840-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="df840-119">JavaScript doğrudan JSON yükünü dönüştürebildiğinden, tarayıcı istemcileri için muhtemelen JSON ile kontrol etmek isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="df840-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="df840-120">Neyse ki, Web API 'SI [içerik anlaşması](content-negotiation.md)kullanır, bu nedenle API 'niz her iki biçimi de destekleyebilir ve istemcinin seçmesini sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="df840-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="df840-121">Sunucuda BSON etkinleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="df840-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="df840-122">Web API yapılandırmanızda **bsonmediatypeformatter** ' ı biçimlendiricileri koleksiyonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="df840-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="df840-123">İstemci "Application/bSon" istediğinde, Web API BSON biçimlendirici 'yı kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="df840-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="df840-124">BSON 'u diğer medya türleriyle ilişkilendirmek için, bunları SupportedMediaTypes koleksiyonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="df840-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="df840-125">Aşağıdaki kod, desteklenen medya türlerine "application/vnd. contoso" ekler:</span><span class="sxs-lookup"><span data-stu-id="df840-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="df840-126">Örnek HTTP oturumu</span><span class="sxs-lookup"><span data-stu-id="df840-126">Example HTTP Session</span></span>

<span data-ttu-id="df840-127">Bu örnekte, aşağıdaki model sınıfını ve basit bir Web API denetleyicisi kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="df840-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="df840-128">İstemci aşağıdaki HTTP isteğini gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="df840-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="df840-129">Yanıt şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="df840-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="df840-130">Burada ikili verileri &quot;değiştirdim.&quot; karakterler.</span><span class="sxs-lookup"><span data-stu-id="df840-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="df840-131">Fiddler 'dan aşağıdaki ekran görüntüsü ham onaltılık değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="df840-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="df840-132">HttpClient ile BSON kullanma</span><span class="sxs-lookup"><span data-stu-id="df840-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="df840-133">.NET istemcileri uygulamaları, **HttpClient**Ile bSon biçimlendirici 'yi kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="df840-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="df840-134">**HttpClient**hakkında daha fazla bilgi için bkz. [.net istemcisinden Web API 'si çağırma](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="df840-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="df840-135">Aşağıdaki kod BSON kabul eden bir GET isteği gönderir ve ardından yanıtta BSON yükü kaldırır.</span><span class="sxs-lookup"><span data-stu-id="df840-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="df840-136">Sunucudan BSON istemek için Accept üst bilgisini "Application/bSon" olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="df840-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="df840-137">Yanıt gövdesinin serisini kaldırmak için **Bsonmediatypeformatter**' ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="df840-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="df840-138">Bu biçimlendirici varsayılan biçimlendiricileri koleksiyonda değil, yanıt gövdesini okurken belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="df840-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="df840-139">Sonraki örnek, BSON içeren bir POST isteğinin nasıl gönderileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="df840-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="df840-140">Bu kodun çoğu, önceki örnekle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="df840-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="df840-141">Ancak, **Postaeşitleme** yönteminde, biçimlendirici olarak **Bsonmediatypeformatter** belirtin:</span><span class="sxs-lookup"><span data-stu-id="df840-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="df840-142">Üst düzey temel türler seri hale getiriliyor</span><span class="sxs-lookup"><span data-stu-id="df840-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="df840-143">Her BSON belge, anahtar/değer çiftleri listesidir. BSON belirtimi, bir tamsayı veya dize gibi tek bir ham değerin serileştirilmesi için bir sözdizimi tanımlamaz.</span><span class="sxs-lookup"><span data-stu-id="df840-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="df840-144">Bu sınırlamaya geçici bir çözüm bulmak için **Bsonmediatypeformatter** temel türleri özel bir durum olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="df840-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="df840-145">Serileştirilden önce, değeri "Value" anahtarına sahip bir anahtar/değer çiftine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="df840-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="df840-146">Örneğin, API denetleyicinizin bir tamsayı döndürdüğünü varsayalım:</span><span class="sxs-lookup"><span data-stu-id="df840-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="df840-147">Seri hale getirmadan önce BSON biçimlendiricisi bunu şu anahtar/değer çiftine dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="df840-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="df840-148">Seri durumdan çıkarma sırasında biçimlendirici, verileri özgün değerine geri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="df840-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="df840-149">Ancak, Web API 'niz ham değerler döndürürse, farklı bir BSON ayrıştırıcısı kullanan istemcilerin bu durumu işlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="df840-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="df840-150">Genel olarak, ham değerler yerine yapılandırılmış verileri döndürmeyi göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="df840-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df840-151">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="df840-151">Additional Resources</span></span>

[<span data-ttu-id="df840-152">Web API BSON örneği</span><span class="sxs-lookup"><span data-stu-id="df840-152">Web API BSON Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[<span data-ttu-id="df840-153">Medya biçimleri</span><span class="sxs-lookup"><span data-stu-id="df840-153">Media Formatters</span></span>](media-formatters.md)
