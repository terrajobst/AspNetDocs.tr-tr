---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: Medya Biçimlendiricileri ASP.NET Web API 2 - ASP.NET 4.x
author: MikeWasson
description: Ek medya biçimleri için ASP.NET ASP.NET Web API desteği gösterilmektedir 4.x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418774"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="72bf0-103">ASP.NET Web API 2'deki medya Biçimlendiricileri</span><span class="sxs-lookup"><span data-stu-id="72bf0-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="72bf0-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="72bf0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="72bf0-105">Bu öğreticide, ASP.NET Web API'de ek medya biçimleri için destek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="72bf0-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="72bf0-106">Internet medya türleri</span><span class="sxs-lookup"><span data-stu-id="72bf0-106">Internet Media Types</span></span>

<span data-ttu-id="72bf0-107">Bir MIME türü olarak da bilinen bir medya türü bir veri parçasını biçimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="72bf0-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="72bf0-108">HTTP, ileti gövdesinin biçimi medya türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="72bf0-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="72bf0-109">Medya türü, iki dizeyi, bir tür ve alt oluşur.</span><span class="sxs-lookup"><span data-stu-id="72bf0-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="72bf0-110">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="72bf0-110">For example:</span></span>

- <span data-ttu-id="72bf0-111">metin/html</span><span class="sxs-lookup"><span data-stu-id="72bf0-111">text/html</span></span>
- <span data-ttu-id="72bf0-112">Görüntü/png</span><span class="sxs-lookup"><span data-stu-id="72bf0-112">image/png</span></span>
- <span data-ttu-id="72bf0-113">Uygulama/json</span><span class="sxs-lookup"><span data-stu-id="72bf0-113">application/json</span></span>

<span data-ttu-id="72bf0-114">HTTP iletisinin Varlık gövdesi içeriyorsa, Content-Type üst bilgisi, ileti gövdesinin biçimi belirtir.</span><span class="sxs-lookup"><span data-stu-id="72bf0-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="72bf0-115">Bu, ileti gövdesi içeriğini ayrıştırmayı alıcı bildirir.</span><span class="sxs-lookup"><span data-stu-id="72bf0-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="72bf0-116">Örneğin, bir HTTP yanıtı bir PNG görüntüsü içeriyorsa, yanıt aşağıdaki üst bilgileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="72bf0-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="72bf0-117">İstemci bir istek iletisi gönderirken bir Accept üst bilgisi dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72bf0-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="72bf0-118">Accept üst bilgisi, sunucunun istemci medya türde sunucudan istediği söyler.</span><span class="sxs-lookup"><span data-stu-id="72bf0-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="72bf0-119">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="72bf0-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="72bf0-120">Bu üst bilgi, istemci HTML, XHTML veya XML istediğini sunucu söyler.</span><span class="sxs-lookup"><span data-stu-id="72bf0-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="72bf0-121">Web API'sini nasıl serileştirir ve HTTP ileti gövdesi seri durumdan çıkarır medya türünü belirler.</span><span class="sxs-lookup"><span data-stu-id="72bf0-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="72bf0-122">Web API'si, XML, JSON, BSON ve form-urlencoded verileri için yerleşik desteği vardır ve ek medya türleri yazarak destekleyebilir bir *medya biçimlendiricisi*.</span><span class="sxs-lookup"><span data-stu-id="72bf0-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="72bf0-123">Bir medya biçimlendiricisi oluşturmak için bu sınıflardan birine türetilir:</span><span class="sxs-lookup"><span data-stu-id="72bf0-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="72bf0-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="72bf0-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="72bf0-125">Bu sınıfı kullanan zaman uyumsuz okuma ve yazma yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="72bf0-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="72bf0-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="72bf0-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="72bf0-127">Bu sınıfın türetildiği **MediaTypeFormatter** ancak zaman uyumlu okuma/yazma yöntemleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="72bf0-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="72bf0-128">Öğesinden türetme **BufferedMediaTypeFormatter** çünkü zaman uyumsuz kod yok, ancak çağıran iş parçacığını g/ç sırasında engellemek geldiğini de kolaydır.</span><span class="sxs-lookup"><span data-stu-id="72bf0-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="72bf0-129">Örnek: Bir CSV medya biçimlendiricisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="72bf0-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="72bf0-130">Aşağıdaki örnek, bir virgülle ayrılmış değerler (CSV) biçiminde bir ürün nesnesine serileştirebilen bir medya türü biçimlendiricisini gösterir.</span><span class="sxs-lookup"><span data-stu-id="72bf0-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="72bf0-131">Bu örnekte bu öğreticide tanımlanan ürün türü [bu destekler CRUD işlemleri bir Web API'si oluşturma](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span><span class="sxs-lookup"><span data-stu-id="72bf0-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="72bf0-132">Ürün nesnesinin tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="72bf0-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="72bf0-133">Bir CSV biçimlendirici uygulamak için türetilen bir sınıf tanımlama **BufferedMediaTypeFormatter**:</span><span class="sxs-lookup"><span data-stu-id="72bf0-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="72bf0-134">Oluşturucuda Biçimlendiricinin desteklediği medya türleriyle ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72bf0-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="72bf0-135">Bu örnekte, bir tek bir medya türü biçimlendirici destekler &quot;metin/csv&quot;:</span><span class="sxs-lookup"><span data-stu-id="72bf0-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="72bf0-136">Geçersiz kılma **CanWriteType** serialize yöntemi, biçimlendirici türlerini belirtmek için:</span><span class="sxs-lookup"><span data-stu-id="72bf0-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="72bf0-137">Bu örnekte, biçimlendirici tek serileştirebiliyorsa `Product` nesneleri koleksiyonlarının yanı sıra `Product` nesneleri.</span><span class="sxs-lookup"><span data-stu-id="72bf0-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="72bf0-138">Benzer şekilde, geçersiz kılma **CanReadType** yöntemi, biçimlendirici türlerini belirtmek için seri durumdan çıkarabilen.</span><span class="sxs-lookup"><span data-stu-id="72bf0-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="72bf0-139">Yöntemi yalnızca döndürecek şekilde bu örnekte, biçimlendirici seri durumundan çıkarma desteklemiyor **false**.</span><span class="sxs-lookup"><span data-stu-id="72bf0-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="72bf0-140">Son olarak, geçersiz kılma **WriteToStream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="72bf0-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="72bf0-141">Bu yöntem bir tür yazarak bir akışa serileştirir.</span><span class="sxs-lookup"><span data-stu-id="72bf0-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="72bf0-142">Ayrıca, biçimlendirici seri durumundan çıkarma destekliyorsa, geçersiz kılma **ReadFromStream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="72bf0-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="72bf0-143">Bir medya biçimlendiricisi Web API ardışık düzenine eklemek için</span><span class="sxs-lookup"><span data-stu-id="72bf0-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="72bf0-144">Bir medya türü biçimlendiricisi Web API ardışık düzenine eklemek için **Biçimlendiricileri** özelliği **HttpConfiguration** nesne.</span><span class="sxs-lookup"><span data-stu-id="72bf0-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="72bf0-145">Karakter kodlamaları</span><span class="sxs-lookup"><span data-stu-id="72bf0-145">Character Encodings</span></span>

<span data-ttu-id="72bf0-146">İsteğe bağlı olarak, bir medya biçimlendiricisi UTF-8 veya ISO 8859-1 gibi birden çok karakter kodlamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="72bf0-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="72bf0-147">Oluşturucusunun içinde bir veya daha fazla Ekle [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) türlerine **SupportedEncodings** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="72bf0-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="72bf0-148">Varsayılan ilk kodlama yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="72bf0-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="72bf0-149">İçinde **WriteToStream** ve **ReadFromStream** yöntemleri çağırmak [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) tercih edilen karakter kodlamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="72bf0-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="72bf0-150">Bu yöntem Desteklenen kodlamalar listesiyle istek üstbilgilerini eşleşir.</span><span class="sxs-lookup"><span data-stu-id="72bf0-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="72bf0-151">Döndürülen kullanın **kodlama** okuma veya yazma akıştan zaman:</span><span class="sxs-lookup"><span data-stu-id="72bf0-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
