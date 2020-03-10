---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2-ASP.NET 4. x içindeki medya biçimleri
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Web API 'sinde ek medya biçimlerinin nasıl destekleyeceği gösterilmektedir.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557255"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="ed220-103">ASP.NET Web API 2 ' de medya biçimleri</span><span class="sxs-lookup"><span data-stu-id="ed220-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="ed220-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ed220-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ed220-105">Bu öğreticide, ASP.NET Web API 'sinde ek medya biçimlerinin nasıl destekleyeceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ed220-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="ed220-106">Internet medya türleri</span><span class="sxs-lookup"><span data-stu-id="ed220-106">Internet Media Types</span></span>

<span data-ttu-id="ed220-107">MIME türü olarak da bilinen bir medya türü, bir veri parçasının biçimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ed220-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="ed220-108">HTTP 'de medya türleri ileti gövdesinin biçimini tanımlarlar.</span><span class="sxs-lookup"><span data-stu-id="ed220-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="ed220-109">Medya türü iki dizeden oluşur, bir türü ve alt türü.</span><span class="sxs-lookup"><span data-stu-id="ed220-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="ed220-110">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ed220-110">For example:</span></span>

- <span data-ttu-id="ed220-111">metin/html</span><span class="sxs-lookup"><span data-stu-id="ed220-111">text/html</span></span>
- <span data-ttu-id="ed220-112">resim/png</span><span class="sxs-lookup"><span data-stu-id="ed220-112">image/png</span></span>
- <span data-ttu-id="ed220-113">uygulama/json</span><span class="sxs-lookup"><span data-stu-id="ed220-113">application/json</span></span>

<span data-ttu-id="ed220-114">Bir HTTP iletisi bir varlık gövdesi içerdiğinde, Content-Type üstbilgisi ileti gövdesinin biçimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ed220-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="ed220-115">Bu, alıcıya ileti gövdesinin içeriğini ayrıştırmayı söyler.</span><span class="sxs-lookup"><span data-stu-id="ed220-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="ed220-116">Örneğin, bir HTTP yanıtı bir PNG görüntüsü içeriyorsa, yanıt aşağıdaki üst bilgilere sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed220-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="ed220-117">İstemci bir istek iletisi gönderdiğinde, bir Accept üst bilgisi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ed220-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="ed220-118">Accept üst bilgisi sunucuya, istemcinin sunucudan istediği medya türlerini bildirir.</span><span class="sxs-lookup"><span data-stu-id="ed220-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="ed220-119">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ed220-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="ed220-120">Bu üst bilgi, sunucuya istemcinin HTML, XHTML veya XML istediğini söyler.</span><span class="sxs-lookup"><span data-stu-id="ed220-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="ed220-121">Medya türü, Web API 'sinin HTTP ileti gövdesini serileştirerek ve serileştirmesi gerektiğini belirler.</span><span class="sxs-lookup"><span data-stu-id="ed220-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="ed220-122">Web API 'si, XML, JSON, BSON ve form-urlencoded verileri için yerleşik desteğe sahiptir ve *medya biçimlendirici*yazarak ek medya türlerini destekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed220-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="ed220-123">Bir medya biçimlendirici oluşturmak için, bu sınıflardan birini türet:</span><span class="sxs-lookup"><span data-stu-id="ed220-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="ed220-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed220-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="ed220-125">Bu sınıf zaman uyumsuz okuma ve yazma yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed220-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="ed220-126">[Bufferedmediatypeformatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed220-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="ed220-127">Bu sınıf, **MediaTypeFormatter** 'dan türetilir ancak zaman uyumlu okuma/yazma yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed220-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="ed220-128">**Bufferedmediatypeformatter** 'dan türetme, zaman uyumsuz kod olmadığı için daha basittir, ancak aynı zamanda çağıran iş parçacığının g/ç sırasında engelleyebileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ed220-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="ed220-129">Örnek: CSV medya biçimlendiricisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ed220-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="ed220-130">Aşağıdaki örnek, bir ürün nesnesini bir virgülle ayrılmış değerler (CSV) biçimine seri hale getirebilen bir medya türü biçimlendirici gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed220-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="ed220-131">Bu örnek, [CRUD Işlemlerini destekleyen bir Web API 'Si oluşturma](../older-versions/creating-a-web-api-that-supports-crud-operations.md)öğreticisinde tanımlanan ürün türünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed220-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="ed220-132">Ürün nesnesinin tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ed220-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="ed220-133">Bir CSV biçimlendirici uygulamak için, **Bufferedmediatypeformatter**'dan türeyen bir sınıf tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="ed220-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="ed220-134">Oluşturucuda, biçimlendiricinin desteklediği medya türlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ed220-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="ed220-135">Bu örnekte, biçimlendirici tek bir medya türünü destekler &quot;metin/CSV&quot;:</span><span class="sxs-lookup"><span data-stu-id="ed220-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="ed220-136">Biçimlendiricinin seri hale getirebileceği türleri belirtmek için **CanWriteType** yöntemini geçersiz kılın:</span><span class="sxs-lookup"><span data-stu-id="ed220-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="ed220-137">Bu örnekte, biçimlendirici tek `Product` nesnelerinin yanı sıra `Product` nesne koleksiyonlarını seri hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed220-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="ed220-138">Benzer şekilde, biçimlendirici 'in seri durumdan çıkarabileceği türleri göstermek için **CanReadType** yöntemini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="ed220-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="ed220-139">Bu örnekte, biçimlendirici serisini kaldırma ' yı desteklemez, bu nedenle metot yalnızca **false**değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ed220-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="ed220-140">Son olarak, **WriteToStream** yöntemini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="ed220-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="ed220-141">Bu yöntem bir akışa yazarak bir türü seri hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ed220-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="ed220-142">Biçimlendirici seri durumdan çıkarmayı destekliyorsa **ReadFromStream** yöntemini de geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="ed220-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="ed220-143">Web API ardışık düzenine medya biçimlendirici ekleme</span><span class="sxs-lookup"><span data-stu-id="ed220-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="ed220-144">Web API ardışık düzenine bir medya türü biçimlendirici eklemek için **HttpConfiguration** nesnesindeki **Formatters** özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ed220-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="ed220-145">Karakter kodlamaları</span><span class="sxs-lookup"><span data-stu-id="ed220-145">Character Encodings</span></span>

<span data-ttu-id="ed220-146">İsteğe bağlı olarak, bir medya biçimlendiricisi UTF-8 veya ISO 8859-1 gibi birden çok karakter kodlamasını destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ed220-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="ed220-147">Oluşturucuda, **Supportedencotypes** koleksiyonuna bir veya daha fazla [System. Text. Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) türü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ed220-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="ed220-148">Önce varsayılan kodlamayı yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="ed220-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="ed220-149">**WriteToStream** ve **ReadFromStream** yöntemlerinde, tercih edilen karakter kodlamasını seçmek için [MediaTypeFormatter. selectkarakterencoding](https://msdn.microsoft.com/library/hh969054.aspx) ' i çağırın.</span><span class="sxs-lookup"><span data-stu-id="ed220-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="ed220-150">Bu yöntem, istek üst bilgilerini desteklenen Kodlamalar listesiyle eşleştirir.</span><span class="sxs-lookup"><span data-stu-id="ed220-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="ed220-151">Akıştan okurken veya yazarken döndürülen **kodlamayı** kullanın:</span><span class="sxs-lookup"><span data-stu-id="ed220-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
