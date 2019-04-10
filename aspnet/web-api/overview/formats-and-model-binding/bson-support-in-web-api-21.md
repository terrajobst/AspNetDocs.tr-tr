---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: BSON desteği ASP.NET Web API 2.1 - ASP.NET 4.x
author: MikeWasson
description: BSON bir Web API denetleyicisi (sunucu tarafı) ve bir .NET istemci uygulaması için ASP.NET kullanmayı gösterir 4.x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 911e2abcfd277075b3cba71e624ec6390b99a15e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382241"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="61680-103">ASP.NET Web API 2.1 sürümünde BSON desteği</span><span class="sxs-lookup"><span data-stu-id="61680-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="61680-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="61680-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="61680-105">Bu konuda, Web API denetleyicinizde (sunucu tarafı) ve bir .NET istemci uygulamasında BSON kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="61680-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="61680-106">Web API 2.1 BSON desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="61680-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="61680-107">BSON nedir?</span><span class="sxs-lookup"><span data-stu-id="61680-107">What is BSON?</span></span>

<span data-ttu-id="61680-108">[BSON](http://bsonspec.org/) bir ikili serileştirme biçimidir.</span><span class="sxs-lookup"><span data-stu-id="61680-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="61680-109">"BSON", "İçin ikili JSON" anlamına gelir, ancak BSON ve JSON çok farklı serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="61680-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="61680-110">BSON olan "JSON benzeri", çünkü nesneleri ad-değer çiftleri, JSON ile benzer olarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="61680-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="61680-111">JSON, sayısal veri türleri değil dizeleri bayt depolanır</span><span class="sxs-lookup"><span data-stu-id="61680-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="61680-112">BSON, basit, kolay taranabilir ve hızlı kodlama/kod çözme için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="61680-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="61680-113">BSON, JSON'a boyutu karşılaştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="61680-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="61680-114">Verilere bağlı olarak bir BSON yükü daha küçük veya büyük bir JSON yükü olabilir.</span><span class="sxs-lookup"><span data-stu-id="61680-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="61680-115">İkili verileri base64 kodlu olmadığı için bir görüntü dosyası gibi ikili verileri seri hale getirme için BSON JSON küçüktür.</span><span class="sxs-lookup"><span data-stu-id="61680-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="61680-116">Bir Ayrıştırıcı kod çözme olmadan öğeleri atlayabilirsiniz öğeleri bir uzunluğu alanıyla önünde taramak BSON belgeleri kolaydır.</span><span class="sxs-lookup"><span data-stu-id="61680-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="61680-117">Sayısal veri türleri olmayan dizeler numaraları olarak depolandığından kodlama ve kodunu çözme ve verimlidir.</span><span class="sxs-lookup"><span data-stu-id="61680-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="61680-118">.NET istemci uygulamaları gibi yerel istemci JSON veya XML gibi metin tabanlı biçimler yerine BSON kullanımından yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="61680-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="61680-119">JavaScript JSON yükü doğrudan dönüştürebilirsiniz çünkü tarayıcı istemcileri için büyük olasılıkla JSON ile takılıyor isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61680-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="61680-120">Neyse ki, Web API'si kullanan [içerik anlaşması](content-negotiation.md), API'nizi hem biçimleri için destek ve seçin istemci olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="61680-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="61680-121">BSON sunucu üzerindeki etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="61680-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="61680-122">Web API yapılandırmanızda ekleme **BsonMediaTypeFormatter** biçimlendiricileri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="61680-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="61680-123">Artık Web API'sini istemci "application/bson" isterse, BSON biçimlendirici kullanır.</span><span class="sxs-lookup"><span data-stu-id="61680-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="61680-124">BSON diğer medya türleri ile ilişkilendirilecek SupportedMediaTypes koleksiyona ekleyin.</span><span class="sxs-lookup"><span data-stu-id="61680-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="61680-125">Aşağıdaki kod, desteklenen medya türleri için "application/vnd.contoso" ekler:</span><span class="sxs-lookup"><span data-stu-id="61680-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="61680-126">Örnek HTTP oturumu</span><span class="sxs-lookup"><span data-stu-id="61680-126">Example HTTP Session</span></span>

<span data-ttu-id="61680-127">Bu örnekte, aşağıdaki model sınıfı artı basit bir Web API denetleyicisi kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="61680-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="61680-128">Bir istemci, aşağıdaki HTTP isteği gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="61680-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="61680-129">Yanıt şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="61680-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="61680-130">Ben ikili verileri burada yerine &quot;.&quot; karakter.</span><span class="sxs-lookup"><span data-stu-id="61680-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="61680-131">Aşağıdaki ekranda Fiddler programlarla ham onaltılık değerleri görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="61680-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="61680-132">BSON HttpClient kullanma</span><span class="sxs-lookup"><span data-stu-id="61680-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="61680-133">.NET istemci uygulamaları, BSON biçimlendirici ile kullanabileceğiniz **HttpClient**.</span><span class="sxs-lookup"><span data-stu-id="61680-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="61680-134">Hakkında daha fazla bilgi için **HttpClient**, bkz: [bir Web API'si bir .NET istemcinin çağırma](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="61680-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="61680-135">Aşağıdaki kod, BSON kabul eder ve yanıt BSON yükü seri durumdan çıkarır bir GET isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="61680-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="61680-136">BSON sunucudan istek için Accept üst bilgisi için "application/bson" ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="61680-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="61680-137">Yanıt gövdesi seri durumdan çıkarılacak kullanın **BsonMediaTypeFormatter**.</span><span class="sxs-lookup"><span data-stu-id="61680-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="61680-138">Yanıt gövdesi okunurken, bunu belirtmeniz gerekmez, bu Biçimlendiricinin varsayılan biçimlendiricileri koleksiyonunda değildir:</span><span class="sxs-lookup"><span data-stu-id="61680-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="61680-139">Sonraki örnek, BSON içeren bir POST isteği göndermek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="61680-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="61680-140">Bu kod çoğunu önceki örnekle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="61680-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="61680-141">Ancak **PostAsync** yöntemini belirtin **BsonMediaTypeFormatter** biçimlendirici olarak:</span><span class="sxs-lookup"><span data-stu-id="61680-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="61680-142">Üst düzey ilkel türler seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="61680-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="61680-143">Her BSON belge, anahtar/değer çifti listesidir. BSON belirtimi, bir tamsayı veya dize gibi tek bir ham değerini serileştirmeye yönelik bir söz dizimi tanımlamıyor.</span><span class="sxs-lookup"><span data-stu-id="61680-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="61680-144">Bu sınırlara yakın çalışmak için **BsonMediaTypeFormatter** ilkel türler, özel bir durum olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="61680-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="61680-145">Seri hale getirme önce değeri bir anahtar/değer çifti "Value" anahtarı ile dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="61680-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="61680-146">Örneğin, bir API denetleyicisi bir tamsayı döndürür varsayalım:</span><span class="sxs-lookup"><span data-stu-id="61680-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="61680-147">Seri hale getirme önce BSON biçimlendirici bu aşağıdaki anahtar/değer çifti dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="61680-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="61680-148">Seri durumdan, biçimlendirici verileri özgün değerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="61680-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="61680-149">Ancak, web API'NİZİN ham değer döndürürse bu durumu işlemek farklı bir BSON Ayrıştırıcıyı kullanarak istemcileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="61680-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="61680-150">Genel olarak, ham değerler yerine, yapılandırılmış veriler döndüren düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="61680-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61680-151">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="61680-151">Additional Resources</span></span>

[<span data-ttu-id="61680-152">Web API BSON örneği</span><span class="sxs-lookup"><span data-stu-id="61680-152">Web API BSON Sample</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[<span data-ttu-id="61680-153">Medya Biçimlendiricileri</span><span class="sxs-lookup"><span data-stu-id="61680-153">Media Formatters</span></span>](media-formatters.md)
