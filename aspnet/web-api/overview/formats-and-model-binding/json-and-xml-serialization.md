---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API-ASP.NET 4. x içinde JSON ve XML serileştirme
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Web API 'sindeki JSON ve XML formatlarını açıklar.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557472"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="868f6-103">ASP.NET Web API 'sinde JSON ve XML serileştirme</span><span class="sxs-lookup"><span data-stu-id="868f6-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="868f6-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="868f6-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="868f6-105">Bu makalede ASP.NET Web API 'sindeki JSON ve XML formatlayıcıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="868f6-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="868f6-106">ASP.NET Web API 'sinde, bir *medya türü biçimlendiricisi* şunları yapabilir:</span><span class="sxs-lookup"><span data-stu-id="868f6-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="868f6-107">Bir HTTP ileti gövdesinden CLR nesnelerini okuma</span><span class="sxs-lookup"><span data-stu-id="868f6-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="868f6-108">CLR nesnelerini bir HTTP ileti gövdesine yazma</span><span class="sxs-lookup"><span data-stu-id="868f6-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="868f6-109">Web API 'si hem JSON hem de XML için medya türü biçimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="868f6-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="868f6-110">Framework, varsayılan olarak bu biçimleri ardışık düzene ekler.</span><span class="sxs-lookup"><span data-stu-id="868f6-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="868f6-111">İstemciler, HTTP isteğinin Accept üst bilgisinde JSON veya XML isteğinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="868f6-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="868f6-112">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="868f6-112">Contents</span></span>

- [<span data-ttu-id="868f6-113">JSON medya türü biçimlendirici</span><span class="sxs-lookup"><span data-stu-id="868f6-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="868f6-114">Salt okunurdur özellikleri</span><span class="sxs-lookup"><span data-stu-id="868f6-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="868f6-115">Tarihle</span><span class="sxs-lookup"><span data-stu-id="868f6-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="868f6-116">Girintileme</span><span class="sxs-lookup"><span data-stu-id="868f6-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="868f6-117">Kamel büyük harfleri</span><span class="sxs-lookup"><span data-stu-id="868f6-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="868f6-118">Anonim ve zayıf türsüz nesneler</span><span class="sxs-lookup"><span data-stu-id="868f6-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="868f6-119">XML medya türü biçimlendirici</span><span class="sxs-lookup"><span data-stu-id="868f6-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="868f6-120">Salt okunurdur özellikleri</span><span class="sxs-lookup"><span data-stu-id="868f6-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="868f6-121">Tarihle</span><span class="sxs-lookup"><span data-stu-id="868f6-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="868f6-122">Girintileme</span><span class="sxs-lookup"><span data-stu-id="868f6-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="868f6-123">Tür başına XML serileştiricileri ayarlanıyor</span><span class="sxs-lookup"><span data-stu-id="868f6-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="868f6-124">JSON veya XML biçimlendirici kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="868f6-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="868f6-125">Döngüsel nesne başvurularını işleme</span><span class="sxs-lookup"><span data-stu-id="868f6-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="868f6-126">Test nesnesi serileştirme</span><span class="sxs-lookup"><span data-stu-id="868f6-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="868f6-127">JSON medya türü biçimlendirici</span><span class="sxs-lookup"><span data-stu-id="868f6-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="868f6-128">JSON biçimlendirmesi, **Jsonmediatypeformatter** sınıfı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="868f6-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="868f6-129">Varsayılan olarak, **Jsonmediatypeformatter** serileştirme gerçekleştirmek için [JSON.net](https://github.com/JamesNK/Newtonsoft.Json) kitaplığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="868f6-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="868f6-130">Json.NET, üçüncü taraf bir açık kaynak projem.</span><span class="sxs-lookup"><span data-stu-id="868f6-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="868f6-131">İsterseniz, Json.NET yerine **DataContractJsonSerializer** kullanmak Için **Jsonmediatypeformatter** sınıfını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="868f6-132">Bunu yapmak için **Usedatacontractjsonserializer** özelliğini **true**olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="868f6-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="868f6-133">JSON Seri Hale Getirme</span><span class="sxs-lookup"><span data-stu-id="868f6-133">JSON Serialization</span></span>

<span data-ttu-id="868f6-134">Bu bölümde, varsayılan [JSON.net](https://github.com/JamesNK/Newtonsoft.Json) serileştirici kullanılarak JSON biçimlendirici 'nin bazı belirli davranışları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="868f6-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="868f6-135">Bu, Json.NET kitaplığı hakkında kapsamlı bir belge olması anlamına gelir; daha fazla bilgi için [JSON.net belgelerine](http://james.newtonking.com/projects/json/help/)bakın.</span><span class="sxs-lookup"><span data-stu-id="868f6-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="868f6-136">Ne seri hale getirilebilir?</span><span class="sxs-lookup"><span data-stu-id="868f6-136">What Gets Serialized?</span></span>

<span data-ttu-id="868f6-137">Varsayılan olarak, tüm ortak özellikler ve alanlar serileştirilmiş JSON 'a dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="868f6-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="868f6-138">Bir özellik veya alanı atlamak için, bunu **Jsonıgnore** özniteliğiyle süsle.</span><span class="sxs-lookup"><span data-stu-id="868f6-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="868f6-139">&quot;kabul&quot; yaklaşımını tercih ediyorsanız, sınıfı **DataContract** özniteliğiyle süsler.</span><span class="sxs-lookup"><span data-stu-id="868f6-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="868f6-140">Bu öznitelik mevcutsa, **DataMember**öğesine sahip olmadıkları müddetçe Üyeler göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="868f6-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="868f6-141">Özel üyeleri seri hale getirmek için **DataMember** de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="868f6-142">Salt okunurdur özellikleri</span><span class="sxs-lookup"><span data-stu-id="868f6-142">Read-Only Properties</span></span>

<span data-ttu-id="868f6-143">Salt okuma özellikleri varsayılan olarak serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="868f6-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="868f6-144">Tarihler</span><span class="sxs-lookup"><span data-stu-id="868f6-144">Dates</span></span>

<span data-ttu-id="868f6-145">Varsayılan olarak, Json.NET tarihleri [ıso 8601](http://www.w3.org/TR/NOTE-datetime) biçiminde yazar.</span><span class="sxs-lookup"><span data-stu-id="868f6-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="868f6-146">UTC (Eşgüdümlü Evrensel Saat) tarihleri "Z" sonekiyle yazılır.</span><span class="sxs-lookup"><span data-stu-id="868f6-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="868f6-147">Yerel saat içindeki tarihler, saat dilimi konumunu içerir.</span><span class="sxs-lookup"><span data-stu-id="868f6-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="868f6-148">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="868f6-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="868f6-149">Varsayılan olarak, Json.NET saat dilimini korur.</span><span class="sxs-lookup"><span data-stu-id="868f6-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="868f6-150">DateTimeZoneHandling özelliğini ayarlayarak bunu geçersiz kılabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="868f6-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="868f6-151">ISO 8601 yerine [MICROSOFT JSON tarih biçimini](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) kullanmayı tercih ediyorsanız, serileştirici ayarlarındaki **DateFormatHandling** özelliğini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="868f6-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="868f6-152">Girintileme</span><span class="sxs-lookup"><span data-stu-id="868f6-152">Indenting</span></span>

<span data-ttu-id="868f6-153">Girintili JSON yazmak için **biçimlendirme** ayarını **biçimlendirme. girintili**olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="868f6-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="868f6-154">Kamel büyük harfleri</span><span class="sxs-lookup"><span data-stu-id="868f6-154">Camel Casing</span></span>

<span data-ttu-id="868f6-155">Veri modelinizi değiştirmeden JSON özellik adlarını kamel büyük küçük harfe yazmak için, seri hale getirici üzerinde **Camelcasepropertynamescontractresolver** ' ı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="868f6-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="868f6-156">Anonim ve zayıf türsüz nesneler</span><span class="sxs-lookup"><span data-stu-id="868f6-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="868f6-157">Bir eylem yöntemi, anonim bir nesne döndürebilir ve bunu JSON 'a seri hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="868f6-158">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="868f6-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="868f6-159">Yanıt iletisi gövdesinde şu JSON yer alacak:</span><span class="sxs-lookup"><span data-stu-id="868f6-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="868f6-160">Web API 'niz istemcilerden gevşek olarak yapılandırılmış JSON nesneleri alırsa, istek gövdesinin serisini bir **Newtonsoft. JSON. LINQ. JObject** türüne taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="868f6-161">Ancak, türü kesin belirlenmiş veri nesneleri kullanmak genellikle daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="868f6-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="868f6-162">Daha sonra verileri kendiniz ayrıştırmanıza gerek kalmaz ve model doğrulamasının avantajlarını elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="868f6-163">XML serileştiricisi anonim türleri veya **JObject** örneklerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="868f6-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="868f6-164">JSON verileriniz için bu özellikleri kullanırsanız, bu makalenin ilerleyen kısımlarında açıklandığı gibi, XML biçimlendirici ' i ardışık düzen öğesinden kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="868f6-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="868f6-165">XML medya türü biçimlendirici</span><span class="sxs-lookup"><span data-stu-id="868f6-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="868f6-166">XML biçimlendirmesi **Xmlmediatypeformatter** sınıfı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="868f6-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="868f6-167">Varsayılan olarak, **Xmlmediatypeformatter** serileştirme işlemini gerçekleştirmek için **DataContractSerializer** sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="868f6-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="868f6-168">Tercih ederseniz, **Xmlmediatypeformatter** 'ı **DataContractSerializer**yerine **XmlSerializer** 'ı kullanacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="868f6-169">Bunu yapmak için **useXmlSerializer** özelliğini **true**olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="868f6-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="868f6-170">**XmlSerializer** sınıfı, **DataContractSerializer**'dan daha dar bir tür kümesini destekler, ancak sonuçta elde edilen XML üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="868f6-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="868f6-171">Mevcut bir XML şemasıyla eşleşmesi gerekiyorsa **XmlSerializer** kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="868f6-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="868f6-172">XML seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="868f6-172">XML Serialization</span></span>

<span data-ttu-id="868f6-173">Bu bölümde, varsayılan **DataContractSerializer**kullanılarak XML biçimlendirici 'nin bazı belirli davranışları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="868f6-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="868f6-174">Varsayılan olarak, DataContractSerializer aşağıdaki gibi davranır:</span><span class="sxs-lookup"><span data-stu-id="868f6-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="868f6-175">Tüm genel okuma/yazma özellikleri ve alanları serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="868f6-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="868f6-176">Bir özellik veya alanı atlamak için, **ıgnoredatamember** özniteliğiyle süslenmiş.</span><span class="sxs-lookup"><span data-stu-id="868f6-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="868f6-177">Özel ve korunan Üyeler serileştirilmez.</span><span class="sxs-lookup"><span data-stu-id="868f6-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="868f6-178">Salt okuma özellikleri serileştirilmez.</span><span class="sxs-lookup"><span data-stu-id="868f6-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="868f6-179">(Ancak, salt okunurdur bir koleksiyon özelliğinin içeriği serileştirilir.)</span><span class="sxs-lookup"><span data-stu-id="868f6-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="868f6-180">Sınıf ve üye adları, sınıf bildiriminde göründükleri gibi XML 'e tam olarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="868f6-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="868f6-181">Varsayılan bir XML ad alanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="868f6-181">A default XML namespace is used.</span></span>

<span data-ttu-id="868f6-182">Serileştirme üzerinde daha fazla denetime ihtiyacınız varsa, bir sınıfı **DataContract** özniteliğiyle süslemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="868f6-183">Bu öznitelik mevcut olduğunda, sınıf aşağıdaki şekilde serileştirilir:</span><span class="sxs-lookup"><span data-stu-id="868f6-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="868f6-184">&quot;&quot; yaklaşımı: Özellikler ve alanlar varsayılan olarak serileştirilmez.</span><span class="sxs-lookup"><span data-stu-id="868f6-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="868f6-185">Bir özellik veya alanı seri hale getirmek için, bunu **DataMember** özniteliğiyle süsle.</span><span class="sxs-lookup"><span data-stu-id="868f6-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="868f6-186">Özel veya korumalı bir üyeyi seri hale getirmek için, bunu **DataMember** özniteliğiyle süsle.</span><span class="sxs-lookup"><span data-stu-id="868f6-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="868f6-187">Salt okuma özellikleri serileştirilmez.</span><span class="sxs-lookup"><span data-stu-id="868f6-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="868f6-188">Sınıf adının XML 'de nasıl göründüğünü değiştirmek için, **DataContract** özniteliğinde *Name* parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="868f6-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="868f6-189">Bir üye adının XML 'de nasıl göründüğünü değiştirmek için, **DataMember** özniteliğinde *Name* parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="868f6-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="868f6-190">XML ad alanını değiştirmek için, **DataContract** sınıfında *ad alanı* parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="868f6-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="868f6-191">Salt okunurdur özellikleri</span><span class="sxs-lookup"><span data-stu-id="868f6-191">Read-Only Properties</span></span>

<span data-ttu-id="868f6-192">Salt okuma özellikleri serileştirilmez.</span><span class="sxs-lookup"><span data-stu-id="868f6-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="868f6-193">Salt okunurdur bir özelliğin bir yedekleme özel alanı varsa, özel alanı **DataMember** özniteliğiyle işaretleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="868f6-194">Bu yaklaşım, sınıfında **DataContract** özniteliğini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="868f6-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="868f6-195">Tarihler</span><span class="sxs-lookup"><span data-stu-id="868f6-195">Dates</span></span>

<span data-ttu-id="868f6-196">Tarihler ISO 8601 biçiminde yazılır.</span><span class="sxs-lookup"><span data-stu-id="868f6-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="868f6-197">Örneğin, &quot;2012-05-23T20:21:37.9116538 Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="868f6-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="868f6-198">Girintileme</span><span class="sxs-lookup"><span data-stu-id="868f6-198">Indenting</span></span>

<span data-ttu-id="868f6-199">Girintili XML yazmak için **Girintile** özelliğini **true**olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="868f6-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="868f6-200">Tür başına XML serileştiricileri ayarlanıyor</span><span class="sxs-lookup"><span data-stu-id="868f6-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="868f6-201">Farklı CLR türleri için farklı XML serileştiricileri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="868f6-202">Örneğin, geriye doğru uyumluluk için **XmlSerializer** gerektiren belirli bir veri nesneniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="868f6-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="868f6-203">Bu nesne için **XmlSerializer** 'ı kullanabilir ve diğer türler için **DataContractSerializer** kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="868f6-204">Belirli bir tür için bir XML serileştirici ayarlamak için **setserializer**çağırın.</span><span class="sxs-lookup"><span data-stu-id="868f6-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="868f6-205">Bir **XmlSerializer** veya **XmlObjectSerializer**öğesinden türetilen herhangi bir nesne belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="868f6-206">JSON veya XML biçimlendirici kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="868f6-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="868f6-207">JSON biçimlendirici veya XML biçimlendirici, bunları kullanmak istemiyorsanız Formatters listesinden kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="868f6-208">Bunu yapmak için başlıca nedenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="868f6-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="868f6-209">Web API yanıtlarınızı belirli bir medya türüyle sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="868f6-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="868f6-210">Örneğin, yalnızca JSON yanıtlarını desteklemeye karar verebilir ve XML biçimlendirici ' ı kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="868f6-211">Varsayılan biçimlendiricisi özel bir biçimlendirici ile değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="868f6-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="868f6-212">Örneğin, JSON biçimlendirici bir JSON biçimlendiricisi kendi özel uygulamanıza göre değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="868f6-213">Aşağıdaki kod, varsayılan formatlamalara nasıl kaldırılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="868f6-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="868f6-214">Bunu, Global. asax dosyasında tanımlanan **uygulamanızdan\_start** yönteminden çağırın.</span><span class="sxs-lookup"><span data-stu-id="868f6-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="868f6-215">Döngüsel nesne başvurularını işleme</span><span class="sxs-lookup"><span data-stu-id="868f6-215">Handling Circular Object References</span></span>

<span data-ttu-id="868f6-216">Varsayılan olarak, JSON ve XML formatlayıcıları tüm nesneleri değer olarak yazar.</span><span class="sxs-lookup"><span data-stu-id="868f6-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="868f6-217">İki özellik aynı nesneye başvurursanız veya aynı nesne bir koleksiyonda iki kez görünürse, biçimlendirici nesneyi iki kez serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="868f6-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="868f6-218">Bu, nesne grafikleriniz döngüler içeriyorsa, bu bir sorundur çünkü seri hale getirici grafikte bir döngü algıladığında bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="868f6-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="868f6-219">Aşağıdaki nesne modellerini ve denetleyiciyi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="868f6-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="868f6-220">Bu eylemi çağırmak, biçimlendirici bir durum kodu 500 (Iç sunucu hatası) yanıtına çeviren bir özel durum oluşturulmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="868f6-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="868f6-221">JSON 'daki nesne başvurularını korumak için aşağıdaki kodu Global. asax dosyasındaki **Application\_start** yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="868f6-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="868f6-222">Artık denetleyici eylemi şuna benzer bir JSON döndürür:</span><span class="sxs-lookup"><span data-stu-id="868f6-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="868f6-223">Seri hale getiricinin her iki nesneye bir &quot;$id&quot; özelliği eklediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="868f6-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="868f6-224">Ayrıca, Employee. Department özelliğinin bir döngü oluşturduğunu algılar, bu yüzden değeri bir nesne başvurusuyla değiştirir: {&quot;$ref&quot;:&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="868f6-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="868f6-225">Nesne başvuruları JSON 'da standart değildir.</span><span class="sxs-lookup"><span data-stu-id="868f6-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="868f6-226">Bu özelliği kullanmadan önce, istemcilerinizin sonuçları ayrıştırabilecek olup olmayacağını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="868f6-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="868f6-227">Yalnızca grafikten döngüleri kaldırmak daha iyi olabilir.</span><span class="sxs-lookup"><span data-stu-id="868f6-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="868f6-228">Örneğin, çalışana kadar olan bağlantı bu örnekte gerçekten gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="868f6-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="868f6-229">XML 'deki nesne başvurularını korumak için iki seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="868f6-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="868f6-230">Daha basit seçenek, model sınıfınıza `[DataContract(IsReference=true)]` eklemektir.</span><span class="sxs-lookup"><span data-stu-id="868f6-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="868f6-231">*IsReference* parametresi nesne başvurularını mümkün bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="868f6-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="868f6-232">**DataContract** serileştirme kabul eder, bu nedenle ayrıca özelliklere **DataMember** öznitelikleri eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="868f6-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="868f6-233">Artık biçimlendirici şuna benzer bir XML oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="868f6-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="868f6-234">Model sınıfınıza ait özniteliklerin önüne geçmek istiyorsanız, başka bir seçenek vardır: yeni türe özgü bir **DataContractSerializer** örneği oluşturun ve bu tür Için *preserveObjectReferences* öğesini **true** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="868f6-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="868f6-235">Sonra bu örneği, XML medya türü biçimlendirici üzerinde tür başına seri hale getirici olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="868f6-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="868f6-236">Aşağıdaki kod bunun nasıl yapılacağını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="868f6-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="868f6-237">Test nesnesi serileştirme</span><span class="sxs-lookup"><span data-stu-id="868f6-237">Testing Object Serialization</span></span>

<span data-ttu-id="868f6-238">Web API 'nizi tasarlarken, veri nesnelerinizin nasıl seri hale getirileceğinin test olması yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="868f6-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="868f6-239">Bunu, denetleyici oluşturmadan veya bir denetleyici eylemi çağırmadan yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f6-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
