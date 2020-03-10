---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API-ASP.NET 4. x içindeki HTTP tanımlama bilgileri
author: MikeWasson
description: ASP.NET 4. x için Web API 'de HTTP tanımlama bilgilerinin nasıl gönderileceğini ve alınacağını açıklar.
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557689"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="1d5a0-103">ASP.NET Web API’de HTTP Tanımlama Bilgileri</span><span class="sxs-lookup"><span data-stu-id="1d5a0-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="1d5a0-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1d5a0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1d5a0-105">Bu konuda, Web API 'de HTTP tanımlama bilgilerinin nasıl gönderileceği ve alınacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="1d5a0-106">HTTP tanımlama bilgilerinde arka plan</span><span class="sxs-lookup"><span data-stu-id="1d5a0-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="1d5a0-107">Bu bölüm, tanımlama bilgilerinin HTTP düzeyinde nasıl uygulandığı hakkında kısa bir genel bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="1d5a0-108">Ayrıntılar için bkz. [RFC 6265](http://tools.ietf.org/html/rfc6265).</span><span class="sxs-lookup"><span data-stu-id="1d5a0-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="1d5a0-109">Tanımlama bilgisi, bir sunucunun HTTP yanıtında gönderdiği bir veri parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="1d5a0-110">İstemci (isteğe bağlı olarak) tanımlama bilgisini depolar ve sonraki isteklere geri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="1d5a0-111">Bu, istemci ve sunucunun durum paylaşmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-111">This allows the client and server to share state.</span></span> <span data-ttu-id="1d5a0-112">Bir tanımlama bilgisi ayarlamak için, sunucu yanıtta bir set-Cookie üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="1d5a0-113">Tanımlama bilgisinin biçimi, isteğe bağlı özniteliklere sahip bir ad-değer çiftleridir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="1d5a0-114">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1d5a0-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="1d5a0-115">Özniteliklere sahip bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1d5a0-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="1d5a0-116">Sunucuya bir tanımlama bilgisi döndürmek için, istemci sonraki isteklere bir tanımlama bilgisi üstbilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="1d5a0-117">Bir HTTP yanıtı, birden çok Set-Cookie üst bilgisi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="1d5a0-118">İstemci tek bir tanımlama bilgisi üstbilgisi kullanarak birden çok tanımlama bilgisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="1d5a0-119">Tanımlama bilgisinin kapsamı ve süresi, set-Cookie üstbilgisindeki öznitelikler tarafından denetlenir:</span><span class="sxs-lookup"><span data-stu-id="1d5a0-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="1d5a0-120">**Etki alanı**: istemciye hangi etki alanının tanımlama bilgisini alacağını söyler.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="1d5a0-121">Örneğin, etki alanı "example.com" ise, istemci, example.com öğesinin her alt etki alanını tanımlama bilgisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="1d5a0-122">Belirtilmezse, etki alanı kaynak sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="1d5a0-123">**Yol**: tanımlama bilgisini, etki alanı içinde belirtilen yol ile sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="1d5a0-124">Belirtilmemişse, istek URI 'sinin yolu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="1d5a0-125">**Süre sonu**: tanımlama bilgisi için bir sona erme tarihi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="1d5a0-126">İstemci, süresi dolduğu zaman tanımlama bilgisini siler.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="1d5a0-127">**Maksimum yaş**: tanımlama bilgisi için maksimum yaşı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="1d5a0-128">İstemci, en yüksek yaş sınırına ulaştığında tanımlama bilgisini siler.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="1d5a0-129">Hem `Expires` hem de `Max-Age` ayarlanırsa `Max-Age` öncelik kazanır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="1d5a0-130">Hiçbiri ayarlanmazsa, geçerli oturum sona erdiğinde istemci tanımlama bilgisini siler.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="1d5a0-131">("Oturumun" tam anlamı Kullanıcı Aracısı tarafından belirlenir.)</span><span class="sxs-lookup"><span data-stu-id="1d5a0-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="1d5a0-132">Ancak, istemcilerin tanımlama bilgilerini yoksayabilir farkında olun.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="1d5a0-133">Örneğin, bir kullanıcı gizlilik nedenleriyle tanımlama bilgilerini devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="1d5a0-134">İstemciler, tanımlama bilgilerini süresi dolmadan önce silebilir veya depolanan tanımlama bilgilerinin sayısını sınırlandırabilir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="1d5a0-135">Gizlilik nedenleriyle, istemciler genellikle etki alanının kaynak sunucuyla eşleşmediği "üçüncü taraf" tanımlama bilgilerini reddeder.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="1d5a0-136">Kısacası, sunucu, ayarladığı tanımlama bilgilerini geri almaya bağlı olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="1d5a0-137">Web API 'de tanımlama bilgileri</span><span class="sxs-lookup"><span data-stu-id="1d5a0-137">Cookies in Web API</span></span>

<span data-ttu-id="1d5a0-138">Bir HTTP yanıtına bir tanımlama bilgisi eklemek için, tanımlama bilgisini temsil eden bir **pişirme ıeheadervalue** örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="1d5a0-139">Ardından, System .net. http dosyasında tanımlanan **addCookies** uzantı yöntemini çağırın **. Tanımlama bilgisini eklemek için HttpResponseHeadersExtensions** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="1d5a0-140">Örneğin, aşağıdaki kod bir denetleyici eylemi içine bir tanımlama bilgisi ekler:</span><span class="sxs-lookup"><span data-stu-id="1d5a0-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="1d5a0-141">**AddCookies** 'in bir dizi **ıeheadervalue** örneği aldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="1d5a0-142">İstemci isteğinden tanımlama bilgilerini ayıklamak için **GetCookies** metodunu çağırın:</span><span class="sxs-lookup"><span data-stu-id="1d5a0-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="1d5a0-143">Bir **pişirme ıeheadervalue** , bir **CookieState** örnekleri koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="1d5a0-144">Her bir **CookieState** bir tanımlama bilgisini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="1d5a0-145">Adlı Dizin Oluşturucu yöntemini kullanarak, gösterildiği gibi, ada göre bir **CookieState** alın.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="1d5a0-146">Yapılandırılmış tanımlama bilgisi verileri</span><span class="sxs-lookup"><span data-stu-id="1d5a0-146">Structured Cookie Data</span></span>

<span data-ttu-id="1d5a0-147">Birçok tarayıcı, hem toplam numarayı hem de etki&#8212;alanı başına sayıyı depolayabileceği tanımlama bilgilerinin sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="1d5a0-148">Bu nedenle, birden çok tanımlama bilgisi ayarlamak yerine, yapılandırılmış verileri tek bir tanımlama bilgisine yerleştirmek yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="1d5a0-149">RFC 6265, tanımlama bilgisi verilerinin yapısını tanımlamaz.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="1d5a0-150">**Pişirme ıeheadervalue** sınıfını kullanarak, tanımlama bilgisi verileri için ad-değer çiftleri listesini geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="1d5a0-151">Bu ad-değer çiftleri, set-Cookie üstbilgisinde URL kodlu form verileri olarak kodlanır:</span><span class="sxs-lookup"><span data-stu-id="1d5a0-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="1d5a0-152">Önceki kod, aşağıdaki set-Cookie üst bilgisini üretir:</span><span class="sxs-lookup"><span data-stu-id="1d5a0-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="1d5a0-153">**CookieState** sınıfı, istek iletisindeki bir tanımlama bilgisinden alt değerleri okumak için bir Dizin Oluşturucu yöntemi sağlar:</span><span class="sxs-lookup"><span data-stu-id="1d5a0-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="1d5a0-154">Örnek: bir Ileti Işleyicisinde tanımlama bilgilerini ayarlama ve alma</span><span class="sxs-lookup"><span data-stu-id="1d5a0-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="1d5a0-155">Önceki örneklerde, bir Web API denetleyicisi içinden tanımlama bilgilerinin nasıl kullanılacağı gösterildi.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="1d5a0-156">Başka bir seçenek de [ileti işleyicilerini](http-message-handlers.md)kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="1d5a0-157">İleti işleyicileri, ardışık düzende denetleyicilerden daha önce çağrılır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="1d5a0-158">İleti işleyicisi, istek denetleyiciye ulaşmadan önce istekten tanımlama bilgilerini okuyabilir veya denetleyici yanıtı oluşturduktan sonra yanıta tanımlama bilgilerini ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="1d5a0-159">Aşağıdaki kod, oturum kimlikleri oluşturmak için bir ileti işleyicisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="1d5a0-160">Oturum KIMLIĞI bir tanımlama bilgisinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="1d5a0-161">İşleyici, oturum tanımlama bilgisi isteğini denetler.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="1d5a0-162">İstek tanımlama bilgisini içermiyorsa, işleyici yeni bir oturum KIMLIĞI oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="1d5a0-163">Her iki durumda da işleyici, oturum KIMLIĞINI **HttpRequestMessage. Properties** Özellik paketinde depolar.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="1d5a0-164">Ayrıca, oturum tanımlama bilgisini HTTP yanıtına ekler.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="1d5a0-165">Bu uygulama, istemciden gelen oturum KIMLIĞININ sunucu tarafından gerçekten yayımlandığını doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="1d5a0-166">Kimlik doğrulama formu olarak kullanmayın!</span><span class="sxs-lookup"><span data-stu-id="1d5a0-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="1d5a0-167">Örneğin noktası, HTTP tanımlama bilgisi yönetimini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="1d5a0-168">Denetleyici, **HttpRequestMessage. Properties** Özellik çantasından oturum kimliğini alabilir.</span><span class="sxs-lookup"><span data-stu-id="1d5a0-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
