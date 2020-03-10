---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Web Pages (Razor) API 'SI hızlı başvurusu | Microsoft Docs
author: Rick-Anderson
description: Bu sayfa, en yaygın kullanılan nesneler, Özellikler ve Razor söz dizimi ile ASP.NET Web sayfalarını programlama yöntemlerine ilişkin kısa örnekler içeren bir liste içerir.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574335"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="edc98-103">ASP.NET Web Pages (Razor) API 'SI hızlı başvurusu</span><span class="sxs-lookup"><span data-stu-id="edc98-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="edc98-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="edc98-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="edc98-105">Bu sayfa, en yaygın kullanılan nesneler, Özellikler ve Razor söz dizimi ile ASP.NET Web sayfalarını programlama yöntemlerine ilişkin kısa örnekler içeren bir liste içerir.</span><span class="sxs-lookup"><span data-stu-id="edc98-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="edc98-106">"(V2)" ile işaretlenen açıklamalar ASP.NET Web Pages sürüm 2 ' de tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="edc98-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="edc98-107">API başvuru belgeleri için MSDN 'deki [ASP.NET Web sayfaları başvuru belgelerine](https://go.microsoft.com/fwlink/?LinkId=208659) bakın.</span><span class="sxs-lookup"><span data-stu-id="edc98-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="edc98-108">Yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="edc98-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="edc98-109">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="edc98-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="edc98-110">Bu öğretici Ayrıca ASP.NET Web Pages 2 ve ASP.NET Web Pages 1,0 (v2 olarak işaretlenmiş Özellikler hariç) ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="edc98-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>

<span data-ttu-id="edc98-111">Bu sayfa, aşağıdakiler için başvuru bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="edc98-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="edc98-112">Sınıflar</span><span class="sxs-lookup"><span data-stu-id="edc98-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="edc98-113">Veri</span><span class="sxs-lookup"><span data-stu-id="edc98-113">Data</span></span>](#Data)
- [<span data-ttu-id="edc98-114">Yardımcı</span><span class="sxs-lookup"><span data-stu-id="edc98-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="edc98-115">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="edc98-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="edc98-116">Sınıflar</span><span class="sxs-lookup"><span data-stu-id="edc98-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="edc98-117">Uygulamadaki herhangi bir sayfa tarafından paylaşılabilecek verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="edc98-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="edc98-118">Aşağıdaki örnekteki gibi, aynı verilere erişmek için dinamik `App` özelliğini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="edc98-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="edc98-119">Bir dize değerini bir Boole değerine dönüştürür (true/false).</span><span class="sxs-lookup"><span data-stu-id="edc98-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="edc98-120">Dize doğru/yanlış temsil ediyorsa, false veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="edc98-121">Bir dize değerini Tarih/saate dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-121">Converts a string value to date/time.</span></span> <span data-ttu-id="edc98-122">Dize bir tarih/saat temsil etmediği zaman `DateTime.MinValue` veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="edc98-123">Bir dize değerini ondalık bir değere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="edc98-124">Dize bir ondalık değeri temsil ediyorsa 0,0 veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="edc98-125">Bir dize değerini bir float öğesine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-125">Converts a string value to a float.</span></span> <span data-ttu-id="edc98-126">Dize bir ondalık değeri temsil ediyorsa 0,0 veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="edc98-127">Bir dize değerini bir tamsayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-127">Converts a string value to an integer.</span></span> <span data-ttu-id="edc98-128">Dize bir tamsayıyı temsil ediyorsa 0 veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="edc98-129">İsteğe bağlı ek yol parçalarıyla, yerel bir dosya yolundan tarayıcı ile uyumlu bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc98-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="edc98-130">*Değeri* HTML kodlu çıktı olarak IŞLEMEK yerine HTML biçimlendirmesi olarak işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="edc98-131">Değer bir dizeden belirtilen türe dönüştürülebiliyorsa, true döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="edc98-132">Nesnenin veya değişkenin değeri yoksa true döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="edc98-133">İstek bir GÖNDERISE, true döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="edc98-134">(Başlangıç istekleri genellikle bir GET olur.)</span><span class="sxs-lookup"><span data-stu-id="edc98-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="edc98-135">Bu sayfaya uygulanacak bir düzen sayfasının yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="edc98-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="edc98-136">Geçerli istekteki sayfa, düzen sayfaları ve kısmi sayfalar arasında paylaşılan verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="edc98-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="edc98-137">Aşağıdaki örnekteki gibi, aynı verilere erişmek için dinamik `Page` özelliğini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="edc98-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="edc98-138">(Düzen sayfaları) Herhangi bir adlandırılmış bölümde olmayan bir içerik sayfasının içeriğini işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="edc98-139">Belirtilen yolu ve isteğe bağlı ek verileri kullanarak bir içerik sayfası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc98-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="edc98-140">`PageData` konuma (örnek 1) veya anahtara göre ek parametrelerin değerlerini alabilirsiniz (örnek 2).</span><span class="sxs-lookup"><span data-stu-id="edc98-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="edc98-141">(Düzen sayfaları) Adında bir içerik bölümü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc98-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="edc98-142">Bir bölümü isteğe bağlı *yapmak için false olarak ayarlayın.*</span><span class="sxs-lookup"><span data-stu-id="edc98-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="edc98-143">HTTP tanımlama bilgisinin değerini alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="edc98-144">Geçerli istekte karşıya yüklenen dosyaları alır.</span><span class="sxs-lookup"><span data-stu-id="edc98-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="edc98-145">Bir formda (dizeler olarak) gönderilen verileri alır.</span><span class="sxs-lookup"><span data-stu-id="edc98-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="edc98-146">`Request[key]` hem `Request.Form` hem de `Request.QueryString` koleksiyonlarını denetler.</span><span class="sxs-lookup"><span data-stu-id="edc98-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="edc98-147">URL sorgu dizesinde belirtilen verileri alır.</span><span class="sxs-lookup"><span data-stu-id="edc98-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="edc98-148">`Request[key]` hem `Request.Form` hem de `Request.QueryString` koleksiyonlarını denetler.</span><span class="sxs-lookup"><span data-stu-id="edc98-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="edc98-149">Form öğesi, sorgu dizesi değeri, tanımlama bilgisi veya üst bilgi değeri için istek doğrulamayı seçmeli olarak devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="edc98-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="edc98-150">İstek doğrulaması varsayılan olarak etkindir ve kullanıcıların biçimlendirme veya diğer potansiyel tehlikeli içerik almasını engeller.</span><span class="sxs-lookup"><span data-stu-id="edc98-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="edc98-151">Yanıta bir HTTP sunucusu üst bilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="edc98-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="edc98-152">Sayfa çıkışını belirli bir süre için önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="edc98-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="edc98-153">İsteğe bağlı olarak, her sayfa erişiminde zaman aşımını sıfırlamak için *kayan* , sayfa isteğindeki her farklı sorgu dizesi için sayfanın farklı sürümlerini önbelleğe almak için *varyByParams* ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="edc98-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="edc98-154">Tarayıcı isteğini yeni bir konuma yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="edc98-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="edc98-155">Tarayıcıya gönderilen HTTP durum kodunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="edc98-156">*Verilerin* içeriğini isteğe bağlı bir MIME türü ile yanıta yazar.</span><span class="sxs-lookup"><span data-stu-id="edc98-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="edc98-157">Bir dosyanın içeriğini yanıta yazar.</span><span class="sxs-lookup"><span data-stu-id="edc98-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="edc98-158">(Düzen sayfaları) Bir ada sahip bir içerik bölümü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="edc98-159">HTML kodlamalı bir dizenin kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="edc98-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="edc98-160">HTML biçimlendirmesinde işleme için bir dizeyi kodlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="edc98-161">Belirtilen sanal yol için sunucu fiziksel yolunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="edc98-162">URL 'deki metnin kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="edc98-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="edc98-163">Bir URL 'ye konacak metni kodlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="edc98-164">Kullanıcı Tarayıcıyı kapatana kadar var olan bir değeri alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="edc98-165">Nesnenin değerinin dize gösterimini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="edc98-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="edc98-166">URL 'den ek verileri alır (örneğin, */MyPage/ExtraData*).</span><span class="sxs-lookup"><span data-stu-id="edc98-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="edc98-167">Belirtilen kullanıcının parolasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="edc98-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="edc98-168">Hesap onaylama belirtecini kullanarak bir hesabı onaylar.</span><span class="sxs-lookup"><span data-stu-id="edc98-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="edc98-169">Belirtilen Kullanıcı adı ve parolayla yeni bir kullanıcı hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc98-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="edc98-170">Bir onay belirteci gerektirmek için, RequireConfirmationToken için doğru geçirin *.*</span><span class="sxs-lookup"><span data-stu-id="edc98-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="edc98-171">Şu anda oturum açmış olan kullanıcının tamsayı tanımlayıcısını alır.</span><span class="sxs-lookup"><span data-stu-id="edc98-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="edc98-172">Şu anda oturum açmış olan kullanıcının adını alır.</span><span class="sxs-lookup"><span data-stu-id="edc98-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="edc98-173">Kullanıcının parolayı sıfırlayabilmesi için kullanıcıya e-posta ile gönderilebilecek bir parola sıfırlama belirteci üretir.</span><span class="sxs-lookup"><span data-stu-id="edc98-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="edc98-174">Kullanıcı adından kullanıcı KIMLIĞINI döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="edc98-175">Geçerli Kullanıcı oturum açtıysa, doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="edc98-176">Kullanıcı onaylanmışsa (örneğin, bir onay e-postası aracılığıyla) true döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="edc98-177">Geçerli kullanıcının adı belirtilen kullanıcı adıyla eşleşiyorsa, doğru değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="edc98-178">Tanımlama bilgisinde bir kimlik doğrulama belirteci ayarlayarak kullanıcıyı ' de günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="edc98-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="edc98-179">Kimlik doğrulama belirteci tanımlama bilgisini kaldırarak kullanıcıyı günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="edc98-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="edc98-180">Kullanıcının kimliği doğrulanmazsa, HTTP durumunu 401 (Yetkisiz) olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="edc98-181">Geçerli Kullanıcı belirtilen rollerden birinin üyesi değilse, HTTP durumunu 401 (yetkisiz) olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="edc98-182">Geçerli Kullanıcı Kullanıcı *adı*tarafından belirtilen kullanıcı DEĞILSE, HTTP durumunu 401 (yetkisiz) olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="edc98-183">Parola sıfırlama belirteci geçerliyse, kullanıcının parolasını yeni parola olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="edc98-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="edc98-184">Veri</span><span class="sxs-lookup"><span data-stu-id="edc98-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="edc98-185">INSERT, DELETE veya UPDATE gibi bir *SQLstatement* (isteğe bağlı parametrelerle) çalıştırır ve etkilenen kayıtların sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="edc98-186">En son eklenen satırdaki kimlik sütununu döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="edc98-187">Belirtilen veritabanı dosyasını veya *Web. config* dosyasından adlandırılmış bir bağlantı dizesi kullanılarak belirtilen veritabanını açar.</span><span class="sxs-lookup"><span data-stu-id="edc98-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="edc98-188">Bağlantı dizesini kullanarak bir veritabanı açar.</span><span class="sxs-lookup"><span data-stu-id="edc98-188">Opens a database using the connection string.</span></span> <span data-ttu-id="edc98-189">(Bu, bir bağlantı dizesi adı kullanan `Database.Open`karşıttır.)</span><span class="sxs-lookup"><span data-stu-id="edc98-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="edc98-190">*SQLstatement* (isteğe bağlı olarak parametreleri geçirme) kullanarak veritabanını sorgular ve sonuçları bir koleksiyon olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="edc98-191">*SQLstatement* (isteğe bağlı parametrelerle) yürütür ve tek bir kayıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="edc98-192">*SQLstatement* (isteğe bağlı parametrelerle) yürütür ve tek bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="edc98-193">Yardımcı</span><span class="sxs-lookup"><span data-stu-id="edc98-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="edc98-194">Belirtilen KIMLIK için Google Analytics JavaScript kodunu işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="edc98-195">Belirtilen proje için StatCounter Analytics JavaScript kodunu işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="edc98-196">Belirtilen hesap için Yahoo Analytics JavaScript kodunu işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="edc98-197">Bir aramayı Bing 'e geçirir.</span><span class="sxs-lookup"><span data-stu-id="edc98-197">Passes a search to Bing.</span></span> <span data-ttu-id="edc98-198">Aranacak siteyi ve arama kutusu için bir başlığı belirtmek üzere `Bing.SiteUrl` ve `Bing.SiteTitle` özelliklerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edc98-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="edc98-199">Normalde bu özellikleri *\_AppStart* sayfasında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="edc98-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="edc98-200">Bir grafiği başlatır.</span><span class="sxs-lookup"><span data-stu-id="edc98-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="edc98-201">Grafiğe bir açıklama ekler.</span><span class="sxs-lookup"><span data-stu-id="edc98-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="edc98-202">Grafiğe bir dizi değer ekler.</span><span class="sxs-lookup"><span data-stu-id="edc98-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="edc98-203">Belirtilen veriler için bir karma döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="edc98-204">Varsayılan algoritma `sha256`.</span><span class="sxs-lookup"><span data-stu-id="edc98-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="edc98-205">Facebook kullanıcılarının sayfalarla bağlantı yapmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="edc98-206">Dosyaları karşıya yüklemek için Kullanıcı arabirimini işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="edc98-207">Belirtilen Xbox oyuncu etiketini işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="edc98-208">Belirtilen e-posta adresi için Gravatar görüntüsünü işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="edc98-209">Veri nesnesini JavaScript Nesne Gösterimi (JSON) biçimindeki bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="edc98-210">JSON kodlu bir giriş dizesini, yinelemek veya veritabanına eklemek için bir veri nesnesine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="edc98-211">Belirtilen başlığı ve isteğe bağlı URL 'YI kullanarak sosyal ağ bağlantılarını işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="edc98-212">Bir hata iletisini form alanıyla ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="edc98-212">Associates an error message with a form field.</span></span> <span data-ttu-id="edc98-213">Bu üyeye erişmek için `ModelState` yardımcısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="edc98-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="edc98-214">Bir hata iletisini bir formla ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="edc98-214">Associates an error message with a form.</span></span> <span data-ttu-id="edc98-215">Bu üyeye erişmek için `ModelState` yardımcısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="edc98-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="edc98-216">Doğrulama hatası yoksa true döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="edc98-217">Bu üyeye erişmek için `ModelState` yardımcısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="edc98-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="edc98-218">Bir nesnenin özelliklerini ve değerlerini ve tüm alt nesneleri işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="edc98-219">ReCAPTCHA doğrulama testini işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="edc98-220">ReCAPTCHA hizmeti için ortak ve özel anahtarları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="edc98-221">Normalde bu özellikleri *\_AppStart* sayfasında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="edc98-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="edc98-222">ReCAPTCHA testinin sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="edc98-223">ASP.NET Web sayfaları hakkında durum bilgilerini işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="edc98-224">Belirtilen kullanıcı için Twitter akışı işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="edc98-225">Belirtilen arama metni için bir Twitter akışı işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="edc98-226">Belirtilen dosya için isteğe bağlı genişlik ve yükseklik içeren bir Flash video oynatıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc98-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="edc98-227">Belirtilen dosya için bir Windows Media Player 'ı isteğe bağlı genişlik ve yükseklik ile işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="edc98-228">Belirtilen *. xap* dosyası için gerekli genişlik ve yüksekliğe sahip bir Silverlight oynatıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc98-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="edc98-229">*Anahtar*tarafından belirtilen nesneyi veya nesne bulunamazsa null değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="edc98-230">*Anahtar* tarafından belirtilen nesneyi önbellekten kaldırır.</span><span class="sxs-lookup"><span data-stu-id="edc98-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="edc98-231">*Değeri* , *anahtar*tarafından belirtilen ad altında önbelleğe koyar.</span><span class="sxs-lookup"><span data-stu-id="edc98-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="edc98-232">Bir sorgudaki verileri kullanarak yeni bir `WebGrid` nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc98-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="edc98-233">HTML tablosunda verileri göstermek için biçimlendirmeyi işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="edc98-234">`WebGrid` nesnesi için bir sayfalayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc98-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="edc98-235">Belirtilen yoldan bir görüntü yükler.</span><span class="sxs-lookup"><span data-stu-id="edc98-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="edc98-236">Belirtilen görüntüyü bir filigran olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="edc98-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="edc98-237">Görüntüye belirtilen metni ekler.</span><span class="sxs-lookup"><span data-stu-id="edc98-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="edc98-238">Görüntüyü yatay veya dikey olarak çevirir.</span><span class="sxs-lookup"><span data-stu-id="edc98-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="edc98-239">Karşıya dosya yükleme sırasında bir görüntü gönderildiğinde bir görüntü yükler.</span><span class="sxs-lookup"><span data-stu-id="edc98-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="edc98-240">Görüntüyü yeniden boyutlandırır.</span><span class="sxs-lookup"><span data-stu-id="edc98-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="edc98-241">Görüntüyü sola veya sağa döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="edc98-242">Görüntüyü belirtilen yola kaydeder.</span><span class="sxs-lookup"><span data-stu-id="edc98-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="edc98-243">SMTP sunucusu için parolayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="edc98-244">Normalde bu özelliği *\_AppStart* sayfasında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="edc98-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="edc98-245">Bir e-posta iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="edc98-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="edc98-246">SMTP sunucusu adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-246">Sets the SMTP server name.</span></span> <span data-ttu-id="edc98-247">Normalde bu özelliği *\_AppStart* sayfasında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="edc98-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="edc98-248">SMTP sunucusu için Kullanıcı adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edc98-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="edc98-249">Normalde bu özelliği *\_AppStart* sayfasında ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="edc98-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="edc98-250">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="edc98-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="edc98-251">v2 Belirtilen alan için bir doğrulama hata iletisi işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="edc98-252">v2 Tüm doğrulama hatalarının listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="edc98-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="edc98-253">v2 Belirtilen doğrulama türü için bir kullanıcı girişi öğesi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="edc98-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="edc98-254">v2 Doğrulama hata iletilerini biçimlendirmek için, istemci tarafı doğrulama için CSS sınıfı özniteliklerini dinamik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="edc98-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="edc98-255">(Uygun istemci komut dosyası kitaplıklarına başvurmanız ve CSS sınıfları tanımlamanız gerekir.)</span><span class="sxs-lookup"><span data-stu-id="edc98-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="edc98-256">v2 Kullanıcı girişi alanı için istemci tarafı doğrulamayı etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="edc98-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="edc98-257">(Uygun istemci komut dosyası kitaplıklarına başvurmanız gerekir.)</span><span class="sxs-lookup"><span data-stu-id="edc98-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="edc98-258">v2 Doğrulama için kayıt defteri \ kırmızı olan tüm Kullanıcı giriş öğeleri geçerli değerler içeriyorsa true döndürür.</span><span class="sxs-lookup"><span data-stu-id="edc98-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="edc98-259">v2 Kullanıcıların, Kullanıcı girişi öğesi için bir değer sağlamaları gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="edc98-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="edc98-260">v2 Kullanıcıların, Kullanıcı giriş öğelerinin her biri için değer sağlaması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="edc98-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="edc98-261">Bu yöntem özel bir hata iletisi belirtmenize izin vermez.</span><span class="sxs-lookup"><span data-stu-id="edc98-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="edc98-262">v2 `Validation.Add` yöntemini kullandığınızda bir doğrulama testi belirtir.</span><span class="sxs-lookup"><span data-stu-id="edc98-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
