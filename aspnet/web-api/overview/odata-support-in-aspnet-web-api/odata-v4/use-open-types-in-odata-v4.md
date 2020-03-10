---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API 'SI ile OData v4 'de açık türler | Microsoft Docs
author: microsoft
description: OData v4 'de, açık bir tür, tür tanımında belirtilen özelliklerin yanı sıra dinamik özellikler içeren yapısal bir türdür. Aç...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622180"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="fea99-104">ASP.NET Web API ile OData v4 'de açık türler</span><span class="sxs-lookup"><span data-stu-id="fea99-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="fea99-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="fea99-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fea99-106">OData v4 'de, *açık bir tür* , tür tanımında belirtilen özelliklerin yanı sıra dinamik özellikler içeren yapısal bir türdür.</span><span class="sxs-lookup"><span data-stu-id="fea99-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="fea99-107">Açık türler, veri modellerinize esneklik eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fea99-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="fea99-108">Bu öğreticide, ASP.NET Web API OData 'de açık türlerin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fea99-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="fea99-109">Bu öğreticide, ASP.NET Web API 'sinde bir OData uç noktası oluşturmayı bildiğiniz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fea99-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="fea99-110">Aksi takdirde, okumaya başlamak için önce [bir OData v4 uç noktası oluşturun](create-an-odata-v4-endpoint.md) .</span><span class="sxs-lookup"><span data-stu-id="fea99-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fea99-111">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="fea99-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fea99-112">Web API OData 5,3</span><span class="sxs-lookup"><span data-stu-id="fea99-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="fea99-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="fea99-113">OData v4</span></span>

<span data-ttu-id="fea99-114">Birincisi, bazı OData terminolojisi:</span><span class="sxs-lookup"><span data-stu-id="fea99-114">First, some OData terminology:</span></span>

- <span data-ttu-id="fea99-115">Varlık türü: anahtarı olan yapılandırılmış bir tür.</span><span class="sxs-lookup"><span data-stu-id="fea99-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="fea99-116">Karmaşık tür: anahtar içermeyen yapılandırılmış bir tür.</span><span class="sxs-lookup"><span data-stu-id="fea99-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="fea99-117">Açık tür: dinamik özelliklere sahip bir tür.</span><span class="sxs-lookup"><span data-stu-id="fea99-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="fea99-118">Hem varlık türleri hem de karmaşık türler açık olabilir.</span><span class="sxs-lookup"><span data-stu-id="fea99-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="fea99-119">Dinamik bir özelliğin değeri basit bir tür, karmaşık tür veya numaralandırma türü olabilir; ya da bu türlerden birinin bir koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="fea99-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="fea99-120">Açık türler hakkında daha fazla bilgi için bkz. [OData v4 belirtimi](http://www.odata.org/documentation/odata-version-4-0/).</span><span class="sxs-lookup"><span data-stu-id="fea99-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="fea99-121">Web OData kitaplıklarını yükler</span><span class="sxs-lookup"><span data-stu-id="fea99-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="fea99-122">En son Web API OData kitaplıklarını yüklemek için NuGet Paket Yöneticisi 'Ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="fea99-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="fea99-123">Paket Yöneticisi konsol penceresinde:</span><span class="sxs-lookup"><span data-stu-id="fea99-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="fea99-124">CLR türlerini tanımlama</span><span class="sxs-lookup"><span data-stu-id="fea99-124">Define the CLR Types</span></span>

<span data-ttu-id="fea99-125">EDM modellerini CLR türleri olarak tanımlayarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="fea99-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="fea99-126">Varlık Veri Modeli (EDM) oluşturulduğunda,</span><span class="sxs-lookup"><span data-stu-id="fea99-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="fea99-127">`Category` bir sabit listesi türüdür.</span><span class="sxs-lookup"><span data-stu-id="fea99-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="fea99-128">`Address` karmaşık bir türdür.</span><span class="sxs-lookup"><span data-stu-id="fea99-128">`Address` is a complex type.</span></span> <span data-ttu-id="fea99-129">(Bir anahtarı yoktur, bu nedenle bir varlık türü değildir.)</span><span class="sxs-lookup"><span data-stu-id="fea99-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="fea99-130">`Customer` bir varlık türüdür.</span><span class="sxs-lookup"><span data-stu-id="fea99-130">`Customer` is an entity type.</span></span> <span data-ttu-id="fea99-131">(Bir anahtarı vardır.)</span><span class="sxs-lookup"><span data-stu-id="fea99-131">(It has a key.)</span></span>
- <span data-ttu-id="fea99-132">`Press` açık bir karmaşık türdür.</span><span class="sxs-lookup"><span data-stu-id="fea99-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="fea99-133">`Book` açık bir varlık türüdür.</span><span class="sxs-lookup"><span data-stu-id="fea99-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="fea99-134">Açık bir tür oluşturmak için CLR türünün, dinamik özellikleri tutan `IDictionary<string, object>`türünde bir özelliği olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fea99-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="fea99-135">EDM modelini oluşturma</span><span class="sxs-lookup"><span data-stu-id="fea99-135">Build the EDM Model</span></span>

<span data-ttu-id="fea99-136">EDM 'yi oluşturmak için **ODataConventionModelBuilder** kullanıyorsanız, `Press` ve `Book`, bir `IDictionary<string, object>` özelliğinin varlığına göre otomatik olarak açık türler olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="fea99-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="fea99-137">Ayrıca, **ODataModelBuilder**kullanarak EDM 'yi açıkça de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fea99-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="fea99-138">OData denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="fea99-138">Add an OData Controller</span></span>

<span data-ttu-id="fea99-139">Ardından, bir OData denetleyicisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fea99-139">Next, add an OData controller.</span></span> <span data-ttu-id="fea99-140">Bu öğreticide, yalnızca GET ve POST isteklerini destekleyen ve varlıkları depolamak için bellek içi bir liste kullanan Basitleştirilmiş bir denetleyici kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="fea99-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="fea99-141">İlk `Book` örneğinin dinamik özellikleri olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fea99-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="fea99-142">İkinci `Book` örneği aşağıdaki dinamik özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fea99-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="fea99-143">"Yayımlandı": temel tür</span><span class="sxs-lookup"><span data-stu-id="fea99-143">"Published": Primitive type</span></span>
- <span data-ttu-id="fea99-144">"Yazarlar": temel türlerin koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="fea99-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="fea99-145">"Diğer kategoriler": sabit listesi türleri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="fea99-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="fea99-146">Ayrıca, bu `Book` örneğinin `Press` özelliği aşağıdaki dinamik özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fea99-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="fea99-147">"Blog": temel tür</span><span class="sxs-lookup"><span data-stu-id="fea99-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="fea99-148">"Adres": karmaşık tür</span><span class="sxs-lookup"><span data-stu-id="fea99-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="fea99-149">Meta verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="fea99-149">Query the Metadata</span></span>

<span data-ttu-id="fea99-150">OData meta veri belgesini almak için `~/$metadata`için bir GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="fea99-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="fea99-151">Yanıt gövdesi şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="fea99-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="fea99-152">Meta veri belgesinden şunları görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fea99-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="fea99-153">`Book` ve `Press` türleri için `OpenType` özniteliğinin değeri true 'dur.</span><span class="sxs-lookup"><span data-stu-id="fea99-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="fea99-154">`Customer` ve `Address` türlerinde bu öznitelik yok.</span><span class="sxs-lookup"><span data-stu-id="fea99-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="fea99-155">`Book` varlık türü üç tanımlı özelliğe sahiptir: ıSBN, title ve Press.</span><span class="sxs-lookup"><span data-stu-id="fea99-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="fea99-156">OData meta verileri CLR sınıfından `Book.Properties` özelliğini içermez.</span><span class="sxs-lookup"><span data-stu-id="fea99-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="fea99-157">Benzer şekilde, `Press` karmaşık tür yalnızca iki tane tanımlanmış özelliğe sahiptir: ad ve kategori.</span><span class="sxs-lookup"><span data-stu-id="fea99-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="fea99-158">Meta veriler CLR sınıfından `Press.DynamicProperties` özelliğini içermez.</span><span class="sxs-lookup"><span data-stu-id="fea99-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="fea99-159">Bir varlığı sorgulama</span><span class="sxs-lookup"><span data-stu-id="fea99-159">Query an Entity</span></span>

<span data-ttu-id="fea99-160">ISBN ile "978-0-7356-7942-9" değerine eşit olan kitabı almak için `~/Books('978-0-7356-7942-9')`için bir GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="fea99-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="fea99-161">Yanıt gövdesi şuna benzer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fea99-161">The response body should look similar to the following.</span></span> <span data-ttu-id="fea99-162">(Daha okunaklı olması için girintilenir.)</span><span class="sxs-lookup"><span data-stu-id="fea99-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="fea99-163">Dinamik özelliklerin, belirtilen özelliklerle birlikte satır içine dahil edildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fea99-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="fea99-164">Bir varlık GÖNDERIN</span><span class="sxs-lookup"><span data-stu-id="fea99-164">POST an Entity</span></span>

<span data-ttu-id="fea99-165">Bir kitap varlığı eklemek için `~/Books`bir POST isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="fea99-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="fea99-166">İstemci, istek yükünde dinamik özellikleri ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="fea99-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="fea99-167">Örnek bir istek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fea99-167">Here is an example request.</span></span> <span data-ttu-id="fea99-168">"Price" ve "yayınlanan" özelliklerine göz önünde edin.</span><span class="sxs-lookup"><span data-stu-id="fea99-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="fea99-169">Denetleyici yönteminde bir kesme noktası ayarlarsanız, Web API 'sinin bu özellikleri `Properties` sözlüğüne eklediğine bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fea99-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="fea99-170">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fea99-170">Additional Resources</span></span>

[<span data-ttu-id="fea99-171">OData açık türü örneği</span><span class="sxs-lookup"><span data-stu-id="fea99-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
