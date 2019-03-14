---
ms.openlocfilehash: 4a4ad30846d1993b3e561c96c00fbf9a0c7f3929
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070881"
---
# <a name="aspnet-core-url-rewriting-sample-aspnet-core-2x"></a><span data-ttu-id="77353-101">ASP.NET Core URL yeniden yazma örnek (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="77353-101">ASP.NET Core URL Rewriting Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="77353-102">Bu örnek bir ASP.NET Core kullanımını 2.x URL yeniden yazma ara yazılımı.</span><span class="sxs-lookup"><span data-stu-id="77353-102">This sample illustrates usage of ASP.NET Core 2.x URL Rewriting Middleware.</span></span> <span data-ttu-id="77353-103">Uygulama URL yeniden yönlendirme ve URL yeniden yazma seçenekleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="77353-103">The app demonstrates URL redirect and URL rewriting options.</span></span>

<span data-ttu-id="77353-104">Kurallardan biri için bir istek URL'si uygulandığında örnek çalışırken, dosya olmayan yanıtları yeniden ya da yeniden yönlendirilen URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="77353-104">When running the sample, non-file responses return the rewritten or redirected URL when one of the rules is applied to a request URL.</span></span> <span data-ttu-id="77353-105">İstek URL'si, ara yazılım tarafından yazılan sonra XML ve metin dosyasının örnekleri için statik dosya ara yazılımlarını dosya işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="77353-105">For the XML and text file examples, Static File Middleware serves the file after the request URL is rewritten by the middleware.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="77353-106">Bu örnekte örnekleri</span><span class="sxs-lookup"><span data-stu-id="77353-106">Examples in this sample</span></span>

* `AddRedirect("redirect-rule/(.*)", "redirected/$1")`
  - <span data-ttu-id="77353-107">Başarılı durum kodu: 302 (Found)</span><span class="sxs-lookup"><span data-stu-id="77353-107">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="77353-108">Örnek (yeniden yönlendirme): **/redirect-rule / {capture_group}** için **/redirected/ {capture_group}**</span><span class="sxs-lookup"><span data-stu-id="77353-108">Example (redirect): **/redirect-rule/{capture_group}** to **/redirected/{capture_group}**</span></span>
* `AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", skipRemainingRules: true)`
  - <span data-ttu-id="77353-109">Başarılı durum kodu: 200 (TAMAM)</span><span class="sxs-lookup"><span data-stu-id="77353-109">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="77353-110">Örnek (yeniden): **/rewrite-rule / {capture_group_1} / {capture_group_2}** için **/ yeniden? var1 {capture_group_1} = & var2 {capture_group_2} =**</span><span class="sxs-lookup"><span data-stu-id="77353-110">Example (rewrite): **/rewrite-rule/{capture_group_1}/{capture_group_2}** to **/rewritten?var1={capture_group_1}&var2={capture_group_2}**</span></span>
* `AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")`
  - <span data-ttu-id="77353-111">Başarılı durum kodu: 302 (Found)</span><span class="sxs-lookup"><span data-stu-id="77353-111">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="77353-112">Örnek (yeniden yönlendirme): **/apache-mod-rules-redirect / {capture_group}** için **/ yeniden yönlendirilen? kimliği = {capture_group}**</span><span class="sxs-lookup"><span data-stu-id="77353-112">Example (redirect): **/apache-mod-rules-redirect/{capture_group}** to **/redirected?id={capture_group}**</span></span>
* `AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")`
  - <span data-ttu-id="77353-113">Başarılı durum kodu: 200 (TAMAM)</span><span class="sxs-lookup"><span data-stu-id="77353-113">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="77353-114">Örnek (yeniden): **/iis-rules-rewrite / {capture_group}** için **/ yeniden? kimliği = {capture_group}**</span><span class="sxs-lookup"><span data-stu-id="77353-114">Example (rewrite): **/iis-rules-rewrite/{capture_group}** to **/rewritten?id={capture_group}**</span></span>
* `Add(RedirectXmlFileRequests)`
  - <span data-ttu-id="77353-115">Başarılı durum kodu: 301 (kalıcı olarak taşındı)</span><span class="sxs-lookup"><span data-stu-id="77353-115">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="77353-116">Örnek (yeniden yönlendirme): **/file.xml** için **/xmlfiles/file.xml**</span><span class="sxs-lookup"><span data-stu-id="77353-116">Example (redirect): **/file.xml** to **/xmlfiles/file.xml**</span></span>
* `Add(RewriteTextFileRequests)`
  - <span data-ttu-id="77353-117">Başarılı durum kodu: 200 (TAMAM)</span><span class="sxs-lookup"><span data-stu-id="77353-117">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="77353-118">Örnek (yeniden): **/some_file.txt** için **/file.txt**</span><span class="sxs-lookup"><span data-stu-id="77353-118">Example (rewrite): **/some_file.txt** to **/file.txt**</span></span>
* `Add(new RedirectImageRequests(".png", "/png-images")))`<br>`Add(new RedirectImageRequests(".jpg", "/jpg-images")))`
  - <span data-ttu-id="77353-119">Başarılı durum kodu: 301 (kalıcı olarak taşındı)</span><span class="sxs-lookup"><span data-stu-id="77353-119">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="77353-120">Örnek (yeniden yönlendirme): **/image.png** için **/png-images/image.png**</span><span class="sxs-lookup"><span data-stu-id="77353-120">Example (redirect): **/image.png** to **/png-images/image.png**</span></span>
  - <span data-ttu-id="77353-121">Örnek (yeniden yönlendirme): **/image.jpg** için **/jpg-images/image.jpg**</span><span class="sxs-lookup"><span data-stu-id="77353-121">Example (redirect): **/image.jpg** to **/jpg-images/image.jpg**</span></span>

## <a name="use-a-physicalfileprovider"></a><span data-ttu-id="77353-122">Bir PhysicalFileProvider kullanın</span><span class="sxs-lookup"><span data-stu-id="77353-122">Use a PhysicalFileProvider</span></span>

<span data-ttu-id="77353-123">De edinebilirsiniz bir `IFileProvider` oluşturarak bir `PhysicalFileProvider` uygulamasına geçirilecek `AddApacheModRewrite()` ve `AddIISUrlRewrite()` yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="77353-123">You can also obtain an `IFileProvider` by creating a `PhysicalFileProvider` to pass into the `AddApacheModRewrite()` and `AddIISUrlRewrite()` methods:</span></span>

```csharp
using Microsoft.Extensions.FileProviders;
PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
```

## <a name="secure-redirection-extensions"></a><span data-ttu-id="77353-124">Güvenli bir yeniden yönlendirme uzantıları</span><span class="sxs-lookup"><span data-stu-id="77353-124">Secure redirection extensions</span></span>

<span data-ttu-id="77353-125">Bu örnek içeren `WebHostBuilder` uygulama URL'lerini kullanacak şekilde yapılandırma (`https://localhost:5001`, `https://localhost`) ve bir test sertifikası (*testCert.pfx*) güvenli bir yeniden yönlendirme yöntemleri keşfetme yardımcı olmak için.</span><span class="sxs-lookup"><span data-stu-id="77353-125">This sample includes `WebHostBuilder` configuration for the app to use URLs (`https://localhost:5001`, `https://localhost`) and a test certificate (*testCert.pfx*) to assist in exploring the secure redirect methods.</span></span> <span data-ttu-id="77353-126">Sunucu bağlantı noktası 443 atanan sahipse veya kullanımda, `https://localhost` örnek işe yaramazsa&mdash;Kaldır `ListenOptions` için bağlantı noktası 443 `CreateWebHostBuilder` yöntemi *Program.cs* dosya veya bağlantı noktası 443 üzerinde bağlamayı Kaldır Sunucu bağlantı noktası, Kestrel'in kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77353-126">If the server already has port 443 assigned or in use, the `https://localhost` example doesn't work&mdash;remove the `ListenOptions` for port 443 in the `CreateWebHostBuilder` method of the *Program.cs* file or unbind port 443 on the server so that Kestrel can use the port.</span></span>

| <span data-ttu-id="77353-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="77353-127">Method</span></span>                           | <span data-ttu-id="77353-128">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="77353-128">Status Code</span></span> |    <span data-ttu-id="77353-129">Bağlantı Noktası</span><span class="sxs-lookup"><span data-stu-id="77353-129">Port</span></span>    |
| -------------------------------- | :---------: | :--------: |
| `.AddRedirectToHttpsPermanent()` |     <span data-ttu-id="77353-130">301</span><span class="sxs-lookup"><span data-stu-id="77353-130">301</span></span>     | <span data-ttu-id="77353-131">null (465)</span><span class="sxs-lookup"><span data-stu-id="77353-131">null (465)</span></span> |
| `.AddRedirectToHttps()`          |     <span data-ttu-id="77353-132">302</span><span class="sxs-lookup"><span data-stu-id="77353-132">302</span></span>     | <span data-ttu-id="77353-133">null (465)</span><span class="sxs-lookup"><span data-stu-id="77353-133">null (465)</span></span> |
| `.AddRedirectToHttps(301)`       |     <span data-ttu-id="77353-134">301</span><span class="sxs-lookup"><span data-stu-id="77353-134">301</span></span>     | <span data-ttu-id="77353-135">null (465)</span><span class="sxs-lookup"><span data-stu-id="77353-135">null (465)</span></span> |
| `.AddRedirectToHttps(301, 5001)` |     <span data-ttu-id="77353-136">301</span><span class="sxs-lookup"><span data-stu-id="77353-136">301</span></span>     |    <span data-ttu-id="77353-137">5001</span><span class="sxs-lookup"><span data-stu-id="77353-137">5001</span></span>    |
