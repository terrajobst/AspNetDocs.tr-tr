---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: ASP.NET Web API 2 - ASP.NET OData sorgu seçeneklerini destekleme 4.x
author: MikeWasson
description: Kod örnekleri ile genel bakış için ASP.NET ASP.NET Web API 2'de destekleyen OData sorgu seçeneklerini gösterir 4.x.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 428e4942e42436585049c1e84cd7b07a4a79c0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59411572"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="1b265-103">ASP.NET Web API 2 OData sorgu seçeneklerini destekleme</span><span class="sxs-lookup"><span data-stu-id="1b265-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="1b265-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1b265-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1b265-105">Bu genel bakışta kod örnekleri ile ASP.NET Web API 2'de destekleyen OData sorgu seçenekleri için ASP.NET gösterir. 4.x.</span><span class="sxs-lookup"><span data-stu-id="1b265-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="1b265-106">OData OData sorgu değiştirmek için kullanılan parametreleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1b265-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="1b265-107">İstemci, bu parametreleri istek URI sorgu dizesinde gönderir.</span><span class="sxs-lookup"><span data-stu-id="1b265-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="1b265-108">Örneğin, sonuçları sıralamak için bir istemci $orderby parametresini kullanır:</span><span class="sxs-lookup"><span data-stu-id="1b265-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="1b265-109">Bu parametreleri OData belirtiminden çağırır *sorgu seçenekleri*.</span><span class="sxs-lookup"><span data-stu-id="1b265-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="1b265-110">Projenizdeki herhangi bir Web API denetleyicisi için OData sorgu seçenekleri etkinleştirebilirsiniz &#8212; denetleyici bir OData uç nokta olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1b265-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="1b265-111">Bu, filtreleme ve sıralama için herhangi bir Web API'sini uygulama gibi özellikleri eklemek için kullanışlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b265-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="1b265-112">Lütfen bu makaleyi okuyun, sorgu seçeneklerini etkinleştirmeden önce [OData güvenlik rehberi](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="1b265-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="1b265-113">OData sorgu seçenekleri etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1b265-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="1b265-114">Örnek sorgular</span><span class="sxs-lookup"><span data-stu-id="1b265-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="1b265-115">Sunucu tabanlı disk belleği</span><span class="sxs-lookup"><span data-stu-id="1b265-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="1b265-116">Sorgu seçenekleri sınırlama</span><span class="sxs-lookup"><span data-stu-id="1b265-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="1b265-117">Sorgu seçenekleri doğrudan çağırma</span><span class="sxs-lookup"><span data-stu-id="1b265-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="1b265-118">Sorgu doğrulama</span><span class="sxs-lookup"><span data-stu-id="1b265-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="1b265-119">OData sorgu seçenekleri etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1b265-119">Enabling OData Query Options</span></span>

<span data-ttu-id="1b265-120">Web API'si, aşağıdaki OData sorgu seçeneklerini destekler:</span><span class="sxs-lookup"><span data-stu-id="1b265-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="1b265-121">Seçenek</span><span class="sxs-lookup"><span data-stu-id="1b265-121">Option</span></span> | <span data-ttu-id="1b265-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1b265-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b265-123">$expand</span><span class="sxs-lookup"><span data-stu-id="1b265-123">$expand</span></span> | <span data-ttu-id="1b265-124">İlgili varlıklar satır içi genişletir.</span><span class="sxs-lookup"><span data-stu-id="1b265-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="1b265-125">$filter</span><span class="sxs-lookup"><span data-stu-id="1b265-125">$filter</span></span> | <span data-ttu-id="1b265-126">Sonuçları bir Boolean koşulu temel alarak filtreler.</span><span class="sxs-lookup"><span data-stu-id="1b265-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="1b265-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="1b265-127">$inlinecount</span></span> | <span data-ttu-id="1b265-128">Sunucu yanıt olarak eşleşen varlıkların toplam sayısı dahil etmek anlatır.</span><span class="sxs-lookup"><span data-stu-id="1b265-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="1b265-129">(Sunucu tarafı disk belleği için kullanışlıdır.)</span><span class="sxs-lookup"><span data-stu-id="1b265-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="1b265-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="1b265-130">$orderby</span></span> | <span data-ttu-id="1b265-131">Sonuçları sıralar.</span><span class="sxs-lookup"><span data-stu-id="1b265-131">Sorts the results.</span></span> |
| <span data-ttu-id="1b265-132">$select</span><span class="sxs-lookup"><span data-stu-id="1b265-132">$select</span></span> | <span data-ttu-id="1b265-133">Yanıta dahil etmek için hangi özelliklerin seçer.</span><span class="sxs-lookup"><span data-stu-id="1b265-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="1b265-134">$skip</span><span class="sxs-lookup"><span data-stu-id="1b265-134">$skip</span></span> | <span data-ttu-id="1b265-135">İlk n sonuç atlar.</span><span class="sxs-lookup"><span data-stu-id="1b265-135">Skips the first n results.</span></span> |
| <span data-ttu-id="1b265-136">$top</span><span class="sxs-lookup"><span data-stu-id="1b265-136">$top</span></span> | <span data-ttu-id="1b265-137">Yalnızca ilk n sonuç döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b265-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="1b265-138">OData sorgu seçeneklerini kullanmak için bunları açıkça etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b265-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="1b265-139">Bunları etkinleştirmek için uygulamanın tamamını veya belirli denetleyicileri veya belirli eylemler için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1b265-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="1b265-140">OData sorgu seçeneklerini etkinleştirmek istiyorsanız arama **EnableQuerySupport** üzerinde **HttpConfiguration** başlangıçta sınıfı:</span><span class="sxs-lookup"><span data-stu-id="1b265-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="1b265-141">**EnableQuerySupport** yöntem sorgu seçenekleri için genel olarak döndüren bir denetleyici eylemi sağlar bir **Iqueryable** türü.</span><span class="sxs-lookup"><span data-stu-id="1b265-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="1b265-142">Uygulamanın tamamı için etkin sorgu seçenekleri istemiyorsanız, bunları belirli bir denetleyici eylemleri için ekleyerek etkinleştirebilirsiniz **[Queryable]** özniteliği eylem yöntemine.</span><span class="sxs-lookup"><span data-stu-id="1b265-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="1b265-143">Örnek sorgular</span><span class="sxs-lookup"><span data-stu-id="1b265-143">Example Queries</span></span>

<span data-ttu-id="1b265-144">Bu bölümde, OData sorgu seçeneklerini kullanarak olası sorgu türleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1b265-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="1b265-145">Sorgu seçenekleri hakkındaki özel ayrıntılar için OData belgelerine bakın [www.odata.org](http://www.odata.org/).</span><span class="sxs-lookup"><span data-stu-id="1b265-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="1b265-146">$ Hakkında bilgi için genişletin ve bkz $select, [$select kullanarak $expand ve ASP.NET Web API OData $value](using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="1b265-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="1b265-147">**İstemci tabanlı disk belleği**</span><span class="sxs-lookup"><span data-stu-id="1b265-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="1b265-148">Büyük varlık kümeleri için istemci sonuçları sayısını sınırlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b265-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="1b265-149">Örneğin, bir istemci, sonraki sonuç sayfasını almak için "İleri" bağlantıları ile bir kerede 10 girişleri gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="1b265-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="1b265-150">Bunu yapmak için istemci $top ve $skip seçeneklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1b265-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="1b265-151">En fazla girdi sayısı bu değeri döndürmek için $top seçeneği sunar ve atlanacak girdi sayısı $skip seçeneği sunar.</span><span class="sxs-lookup"><span data-stu-id="1b265-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="1b265-152">Önceki örnekte girişleri 21 ile 30 getirir.</span><span class="sxs-lookup"><span data-stu-id="1b265-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="1b265-153">**Filtreleme**</span><span class="sxs-lookup"><span data-stu-id="1b265-153">**Filtering**</span></span>

<span data-ttu-id="1b265-154">$Filter seçeneği bir Boole ifadesi uygulayarak, sonuçları filtrelemek için bir istemci olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="1b265-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="1b265-155">Filtre ifadeleri oldukça güçlü; Bunlar, mantıksal ve aritmetik işleçler, dize işlevleri ve tarih işlevleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1b265-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="1b265-156">Kategorisindeki tüm ürünler "Toys" eşit döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b265-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="1b265-157">`http://localhost/Products?$filter=Category` EQ 'Toys'</span><span class="sxs-lookup"><span data-stu-id="1b265-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="1b265-158">Fiyat 10'dan küçük olan tüm ürünleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b265-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="1b265-159">`http://localhost/Products?$filter=Price` lt 10</span><span class="sxs-lookup"><span data-stu-id="1b265-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="1b265-160">Mantıksal işleçler: Tüm ürünleri döndürmek burada fiyat > 5 ve fiyat = < = 15.</span><span class="sxs-lookup"><span data-stu-id="1b265-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="1b265-161">`http://localhost/Products?$filter=Price` Ge 5 ve fiyat le 15</span><span class="sxs-lookup"><span data-stu-id="1b265-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="1b265-162">Dize işlevleri: "Zz" olan tüm ürünleri adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b265-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="1b265-163">Tarih işlevleri: ReleaseDate tüm ürünleriyle 2005'ten sonra döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b265-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="1b265-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span><span class="sxs-lookup"><span data-stu-id="1b265-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="1b265-165">**Sıralama**</span><span class="sxs-lookup"><span data-stu-id="1b265-165">**Sorting**</span></span>

<span data-ttu-id="1b265-166">Sonuçları sıralamak için $orderby filtreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b265-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="1b265-167">Fiyat göre sıralayın.</span><span class="sxs-lookup"><span data-stu-id="1b265-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="1b265-168">Fiyat (yüksekten en düşüğe) azalan düzende sırala.</span><span class="sxs-lookup"><span data-stu-id="1b265-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="1b265-169">Kategoriye göre sıralayın ve ardından fiyat kategorilerde azalan düzende sırala.</span><span class="sxs-lookup"><span data-stu-id="1b265-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="1b265-170">Sunucu tabanlı disk belleği</span><span class="sxs-lookup"><span data-stu-id="1b265-170">Server-Driven Paging</span></span>

<span data-ttu-id="1b265-171">Veritabanınızı milyonlarca kayıt varsa, bunları göndermek istemiyorsanız bir yük içinde tüm.</span><span class="sxs-lookup"><span data-stu-id="1b265-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="1b265-172">Bunu önlemek için sunucu, tek bir yanıtta gönderen giriş sayısını sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b265-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="1b265-173">Sunucu disk belleği'ni etkinleştirmek için **PageSize** özelliğinde **Queryable** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="1b265-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="1b265-174">En fazla girdi sayısı bu değeri döndürülecek değerdir.</span><span class="sxs-lookup"><span data-stu-id="1b265-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="1b265-175">Denetleyicinizi OData biçimi döndürürse, yanıt gövdesi veri sonraki sayfaya bir bağlantı içerir:</span><span class="sxs-lookup"><span data-stu-id="1b265-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="1b265-176">İstemci, bir sonraki sayfayı almak için bu bağlantıyı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b265-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="1b265-177">İstemci sonuç kümesinde girişleri toplam sayısını öğrenmek $inlinecount sorgu seçeneği değerine sahip "inlinecount" ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b265-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="1b265-178">Değer "inlinecount" toplam sayı bu sayıyı yanıta eklenecek sunucunun bildirir:</span><span class="sxs-lookup"><span data-stu-id="1b265-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="1b265-179">Sonraki sayfa bağlantıları hem de satır içi sayı OData biçimini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1b265-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="1b265-180">OData sayısı ve bağlantı tutacak yanıt gövdesi içinde özel alanlar tanımlar nedenidir.</span><span class="sxs-lookup"><span data-stu-id="1b265-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>


<span data-ttu-id="1b265-181">OData olmayan biçimleri için sonraki sayfa ve satır içi bağlantıları sayısı, sorgu sonuçlarında sarmalama tarafından desteklemek için tanımlanabilir bir **PageResult&lt;T&gt;**  nesne.</span><span class="sxs-lookup"><span data-stu-id="1b265-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="1b265-182">Ancak, biraz daha fazla kod gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1b265-182">However, it requires a bit more code.</span></span> <span data-ttu-id="1b265-183">Aşağıda bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1b265-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="1b265-184">Bir örnek JSON yanıtı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1b265-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="1b265-185">Sorgu seçenekleri sınırlama</span><span class="sxs-lookup"><span data-stu-id="1b265-185">Limiting the Query Options</span></span>

<span data-ttu-id="1b265-186">Sorgu seçenekleri istemci çok fazla sunucuda çalıştırılan sorguyu üzerinde denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b265-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="1b265-187">Bazı durumlarda, güvenlik veya performans nedenleriyle kullanılabilir seçenekler sınırlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b265-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="1b265-188">**[Queryable]** özniteliği bazı yerleşik özelliklerinde bu.</span><span class="sxs-lookup"><span data-stu-id="1b265-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="1b265-189">Bazı örnekler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1b265-189">Here are some examples.</span></span>

<span data-ttu-id="1b265-190">Yalnızca $skip ve $top, sayfalama ve başka hiçbir şey desteklemek için izin ver:</span><span class="sxs-lookup"><span data-stu-id="1b265-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="1b265-191">Veritabanında oluşturulmuyor özellikleri sıralama önlemek belirli özellikleri yalnızca tarafından sıralanmasına izin vermek:</span><span class="sxs-lookup"><span data-stu-id="1b265-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="1b265-192">"Eq" mantıksal işlevi ancak diğer mantıksal işlevler izin ver:</span><span class="sxs-lookup"><span data-stu-id="1b265-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="1b265-193">Tüm aritmetik işleçlere izin verme:</span><span class="sxs-lookup"><span data-stu-id="1b265-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="1b265-194">Oluşturarak, genel bir seçenekler kısıtlayabilirsiniz bir **Queryableattribute'taki** örneği ve aktarması **EnableQuerySupport** işlevi:</span><span class="sxs-lookup"><span data-stu-id="1b265-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="1b265-195">Sorgu seçenekleri doğrudan çağırma</span><span class="sxs-lookup"><span data-stu-id="1b265-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="1b265-196">Yerine **[Queryable]** özniteliği doğrudan denetleyicinizin sorgu seçeneklerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b265-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="1b265-197">Bunu yapmak için bir **ODataQueryOptions** denetleyici yöntemin parametre.</span><span class="sxs-lookup"><span data-stu-id="1b265-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="1b265-198">Bu durumda, ihtiyacınız olmayan **[Queryable]** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="1b265-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="1b265-199">Web API doldurur **ODataQueryOptions** URI'SİNDEN sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="1b265-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="1b265-200">Sorgu uygulamak için başarılı bir **Iqueryable** için **ApplyTo** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1b265-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="1b265-201">Başka bir yöntem döndürür **Iqueryable**.</span><span class="sxs-lookup"><span data-stu-id="1b265-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="1b265-202">Yoksa, Gelişmiş senaryolar için bir **Iqueryable** sorgu sağlayıcısı inceleyebilirsiniz **ODataQueryOptions** ve başka bir forma sorgu seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="1b265-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="1b265-203">(Örneğin, RaghuRam Nadiminti'nın blog yayınına bakın [çevirme OData sorgularını hql'e](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), da içeren bir [örnek](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span><span class="sxs-lookup"><span data-stu-id="1b265-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="1b265-204">Sorgu doğrulama</span><span class="sxs-lookup"><span data-stu-id="1b265-204">Query Validation</span></span>

<span data-ttu-id="1b265-205">**[Queryable]** özniteliği sorgu yürütülmeden önce doğrular.</span><span class="sxs-lookup"><span data-stu-id="1b265-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="1b265-206">Doğrulama adımını içinde gerçekleştirilen **QueryableAttribute.ValidateQuery** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1b265-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="1b265-207">Doğrulama işlemi ayrıca özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b265-207">You can also customize the validation process.</span></span>

<span data-ttu-id="1b265-208">Ayrıca bkz: [OData güvenlik rehberi](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="1b265-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="1b265-209">Geçersiz kılma sınıfları almak için diğer bir deyişle, Doğrulayıcı birini ilk olarak tanımlanan **Web.Http.OData.Query.Validators** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1b265-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="1b265-210">Örneğin, aşağıdaki Doğrulayıcı sınıfını $orderby seçeneği için 'desc' seçeneğini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="1b265-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="1b265-211">Alt **[Queryable]** geçersiz kılmak için öznitelik **ValidateQuery** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1b265-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="1b265-212">Ardından, özel özniteliği ayarlayın ya da genel olarak veya denetleyici başına:</span><span class="sxs-lookup"><span data-stu-id="1b265-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="1b265-213">Kullanıyorsanız **ODataQueryOptions** doğrudan Doğrulayıcı seçenekleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="1b265-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
