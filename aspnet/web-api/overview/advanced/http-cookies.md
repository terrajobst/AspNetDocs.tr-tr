---
uid: web-api/overview/advanced/http-cookies
title: HTTP tanımlama bilgileri ASP.NET Web API'si - ASP.NET 4.x
author: MikeWasson
description: Gönderme ve HTTP tanımlama bilgileri için ASP.NET Web API'de alma işlemini açıklamaktadır 4.x.
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: cd6391582f05ab80c4bd45a455a2ce488d1186c1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418332"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="95e83-103">ASP.NET Web API’de HTTP Tanımlama Bilgileri</span><span class="sxs-lookup"><span data-stu-id="95e83-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="95e83-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="95e83-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="95e83-105">Bu konu, göndermek ve Web API'de HTTP tanımlama bilgileri almak açıklar.</span><span class="sxs-lookup"><span data-stu-id="95e83-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="95e83-106">Arka planda HTTP tanımlama bilgileri</span><span class="sxs-lookup"><span data-stu-id="95e83-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="95e83-107">Bu bölüm, tanımlama bilgisi HTTP düzeyinde nasıl uygulandığını kısa genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="95e83-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="95e83-108">Ayrıntılar için başvurun [RFC 6265](http://tools.ietf.org/html/rfc6265).</span><span class="sxs-lookup"><span data-stu-id="95e83-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="95e83-109">Bir tanımlama bilgisi, HTTP yanıtında bir sunucuya gönderdiği verilerin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="95e83-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="95e83-110">İstemci (isteğe bağlı) tanımlama bilgisi depolar ve sonraki isteklerde authenticateasync döndürür.</span><span class="sxs-lookup"><span data-stu-id="95e83-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="95e83-111">Bu, istemci ve sunucu durumu paylaşmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="95e83-111">This allows the client and server to share state.</span></span> <span data-ttu-id="95e83-112">Bir tanımlama bilgisi ayarlamak için sunucunun yanıtta bir Set-Cookie üst bilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="95e83-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="95e83-113">Bir tanımlama bilgisinin biçimi isteğe bağlı öznitelikleri ile bir ad-değer çiftidir.</span><span class="sxs-lookup"><span data-stu-id="95e83-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="95e83-114">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="95e83-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="95e83-115">Özniteliklere sahip bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="95e83-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="95e83-116">Bir tanımlama bilgisinin sunucuya döndürülmesi için istemcinin sonraki istekleri tanımlama bilgisi üstbilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="95e83-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="95e83-117">Bir HTTP yanıtı birden çok Set-Cookie üst bilgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="95e83-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="95e83-118">İstemciyi tek bir tanımlama bilgisi üstbilgisi kullanarak çok sayıda tanımlama bilgisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="95e83-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="95e83-119">Projenin kapsamına ve süresine bir tanımlama bilgisinin Set-Cookie üst bilgisindeki aşağıdaki öznitelikleri tarafından denetlenir:</span><span class="sxs-lookup"><span data-stu-id="95e83-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="95e83-120">**Etki alanı**: İstemci, hangi etki alanı tanımlama bilgisi alması gereken söyler.</span><span class="sxs-lookup"><span data-stu-id="95e83-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="95e83-121">Örneğin, etki alanı "example.com" ise, istemci her alt etki alanının example.com tanımlama bilgisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="95e83-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="95e83-122">Belirtilmezse, kaynak sunucu etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="95e83-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="95e83-123">**Yol**: Tanımlama bilgisinin etki alanı içinde belirtilen yol kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="95e83-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="95e83-124">Belirtilmezse, istek URI'si yolu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="95e83-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="95e83-125">**Süresi dolmadan**: Tanımlama bilgisinin süre sonu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="95e83-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="95e83-126">Belirtecin süresi dolduğunda, istemcinin tanımlama bilgisi siler.</span><span class="sxs-lookup"><span data-stu-id="95e83-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="95e83-127">**Max-Age**: Tanımlama bilgisinin yaş üst sınırını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="95e83-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="95e83-128">En uzun geçerlilik süresi ulaştığında istemci tanımlama bilgisi siler.</span><span class="sxs-lookup"><span data-stu-id="95e83-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="95e83-129">Her iki `Expires` ve `Max-Age` ayarlanması `Max-Age` önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="95e83-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="95e83-130">Ayarlanmış ise, geçerli oturumu sona erdiğinde istemci tanımlama bilgisi siler.</span><span class="sxs-lookup"><span data-stu-id="95e83-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="95e83-131">("Oturumu" tam anlamı kullanıcı aracısı tarafından belirlenir.)</span><span class="sxs-lookup"><span data-stu-id="95e83-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="95e83-132">Ancak, istemciler tanımlama bilgilerini yoksayabilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="95e83-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="95e83-133">Örneğin, kullanıcı gizlilik nedenleriyle tanımlama bilgilerini devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95e83-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="95e83-134">Süresi dolacak veya depolanan tanımlama bilgisi sayısını sınırlamak için önce istemcileri tanımlama bilgilerini silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95e83-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="95e83-135">Gizlilik nedeniyle istemciler genellikle "üçüncü taraf" tanımlama bilgilerini, kaynak sunucu etki alanı burada eşleşmiyor reddeder.</span><span class="sxs-lookup"><span data-stu-id="95e83-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="95e83-136">Kısacası, sunucu tanımlama bilgilerini ayarlar geri alamazsınız güvenmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="95e83-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="95e83-137">Web API'de tanımlama bilgileri</span><span class="sxs-lookup"><span data-stu-id="95e83-137">Cookies in Web API</span></span>

<span data-ttu-id="95e83-138">Bir HTTP yanıtına bir tanımlama bilgisi eklemek için oluşturun bir **CookieHeaderValue** tanımlama bilgisini temsil eden örneği.</span><span class="sxs-lookup"><span data-stu-id="95e83-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="95e83-139">Ardından çağırın **AddCookies** alanında tanımlanan genişletme yöntemi **System.Net.Http. HttpResponseHeadersExtensions** tanımlama bilgisi eklemek için sınıfı.</span><span class="sxs-lookup"><span data-stu-id="95e83-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="95e83-140">Örneğin, aşağıdaki kod, içinde bir denetleyici eylemi bir tanımlama bilgisi ekler:</span><span class="sxs-lookup"><span data-stu-id="95e83-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="95e83-141">Dikkat **AddCookies** dizisi alır **CookieHeaderValue** örnekleri.</span><span class="sxs-lookup"><span data-stu-id="95e83-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="95e83-142">Bir istemci isteğinde tanımlama bilgileri ayıklamak için çağrı **GetCookies** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="95e83-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="95e83-143">A **CookieHeaderValue** koleksiyonunu içeren **CookieState** örnekleri.</span><span class="sxs-lookup"><span data-stu-id="95e83-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="95e83-144">Her **CookieState** bir tanımlama bilgisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="95e83-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="95e83-145">Almak için dizin oluşturucu yöntemi kullanın. bir **CookieState** adıyla gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="95e83-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="95e83-146">Yapılandırılmış bir tanımlama bilgisi verisi</span><span class="sxs-lookup"><span data-stu-id="95e83-146">Structured Cookie Data</span></span>

<span data-ttu-id="95e83-147">Bunlar depolar kaç tanımlama bilgilerini çoğu tarayıcısı sınırlamak&#8212;toplam hem etki alanı sayısı.</span><span class="sxs-lookup"><span data-stu-id="95e83-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="95e83-148">Bu nedenle, çok sayıda tanımlama bilgisini ayarlamak yerine tek bir tanımlama, yapılandırılmış veriler yerleştirmenin yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="95e83-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="95e83-149">RFC 6265 tanımlama bilgisi veri yapısı tanımlamıyor.</span><span class="sxs-lookup"><span data-stu-id="95e83-149">RFC 6265 does not define the structure of cookie data.</span></span>


<span data-ttu-id="95e83-150">Kullanarak **CookieHeaderValue** sınıfı, tanımlama bilgisi verisi için ad-değer çiftlerinin listesini iletebilir.</span><span class="sxs-lookup"><span data-stu-id="95e83-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="95e83-151">Bu ad-değer çiftleri Set-Cookie üst bilgisindeki formu URL kodlanmış veriler olarak kodlanmış:</span><span class="sxs-lookup"><span data-stu-id="95e83-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="95e83-152">Önceki kod, şu Set-Cookie üst bilgisini üretir:</span><span class="sxs-lookup"><span data-stu-id="95e83-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="95e83-153">**CookieState** sınıfı bir tanımlama bilgisinde istek iletisi alt değerleri okumak için bir dizin oluşturucu yöntemi sağlar:</span><span class="sxs-lookup"><span data-stu-id="95e83-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="95e83-154">Örnek: Ayarlayın ve bir ileti işleyicisi tanımlama bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="95e83-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="95e83-155">Önceki örneklerde, bir Web API denetleyicisi içinde tanımlama bilgilerini kullanma gösterdi.</span><span class="sxs-lookup"><span data-stu-id="95e83-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="95e83-156">Başka bir seçenek kullanmaktır [ileti işleyicileri](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="95e83-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="95e83-157">İleti işleyicileri denetleyicileri daha işlem hattındaki daha önce çağrılır.</span><span class="sxs-lookup"><span data-stu-id="95e83-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="95e83-158">Bir ileti işleyicisi isteği ulaşır denetleyicisi önce tanımlama bilgilerini istekten okuyun veya denetleyicisi yanıt oluşturduktan sonra yanıta tanımlama bilgileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="95e83-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="95e83-159">Aşağıdaki kod, oturum kimliklerini oluşturmaya yönelik bir ileti işleyicisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="95e83-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="95e83-160">Oturum kimliği, bir tanımlama bilgisinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="95e83-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="95e83-161">Oturum tanımlama bilgisi için istek işleyicisi denetler.</span><span class="sxs-lookup"><span data-stu-id="95e83-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="95e83-162">İstek tanımlama bilgisi içermiyorsa, işleyici, yeni bir oturum kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="95e83-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="95e83-163">Her iki durumda da, oturum kimliği işleyici depolar **HttpRequestMessage.Properties** özellik paketi.</span><span class="sxs-lookup"><span data-stu-id="95e83-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="95e83-164">Ayrıca HTTP yanıtı oturum tanımlama bilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="95e83-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="95e83-165">Bu uygulama, istemciden gelen oturum kimliği, sunucu tarafından gerçekten verildiğini doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="95e83-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="95e83-166">Form kimlik doğrulaması olarak kullanmayın!</span><span class="sxs-lookup"><span data-stu-id="95e83-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="95e83-167">HTTP tanımlama bilgisi yönetim noktası örneğin göstermektir.</span><span class="sxs-lookup"><span data-stu-id="95e83-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="95e83-168">Bir denetleyici oturum kimliği alabilirsiniz **HttpRequestMessage.Properties** özellik paketi.</span><span class="sxs-lookup"><span data-stu-id="95e83-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
