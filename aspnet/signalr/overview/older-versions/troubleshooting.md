---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR sorunlarını giderme (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bu makalede, SignalR uygulamaları geliştirmeyle ilgili yaygın sorunlar açıklanmaktadır.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579606"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="86aef-103">SignalR Sorunlarını Giderme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="86aef-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="86aef-104">, [Patrick Fleti](https://github.com/pfletcher) tarafından</span><span class="sxs-lookup"><span data-stu-id="86aef-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="86aef-105">Bu belgede, SignalR ile ilgili genel sorun giderme sorunları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="86aef-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="86aef-106">Bu belge aşağıdaki bölümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="86aef-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="86aef-107">İstemci ve sunucu arasındaki Yöntemler sessizce başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="86aef-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="86aef-108">Diğer bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="86aef-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="86aef-109">Derleme ve sunucu tarafı hataları</span><span class="sxs-lookup"><span data-stu-id="86aef-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="86aef-110">Visual Studio sorunları</span><span class="sxs-lookup"><span data-stu-id="86aef-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="86aef-111">Internet Information Services sorunları</span><span class="sxs-lookup"><span data-stu-id="86aef-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="86aef-112">Azure sorunları</span><span class="sxs-lookup"><span data-stu-id="86aef-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="86aef-113">İstemci ve sunucu arasındaki Yöntemler sessizce başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="86aef-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="86aef-114">Bu bölümde, istemci ve sunucu arasındaki yöntem çağrısının anlamlı bir hata iletisi olmadan başarısız olması olası nedenleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="86aef-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="86aef-115">Bir SignalR uygulamasında, sunucuda istemcinin uyguladığı yöntemler hakkında bilgi bulunmamaktadır; sunucu bir istemci yöntemini çağırdığında, yöntem adı ve parametre verileri istemciye gönderilir ve yöntem yalnızca sunucunun belirtildiği biçimde varsa yürütülür.</span><span class="sxs-lookup"><span data-stu-id="86aef-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="86aef-116">İstemcide eşleşen bir yöntem bulunamazsa hiçbir şey olmaz ve sunucuda hiçbir hata iletisi oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="86aef-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="86aef-117">Çağrılmayan istemci yöntemlerini daha fazla araştırmak için, sunucudan hangi çağrıların geldiğini görmek üzere Hub üzerinde Start yöntemini çağırmadan önce günlüğe kaydetmeyi açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86aef-117">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="86aef-118">Bir JavaScript uygulamasında günlüğe kaydetmeyi etkinleştirmek için bkz. [istemci tarafı günlük kaydını etkinleştirme (JavaScript istemci sürümü)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="86aef-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="86aef-119">Bir .NET istemci uygulamasında günlüğe kaydetmeyi etkinleştirmek için bkz. [istemci tarafı günlük kaydını etkinleştirme (.NET istemci sürümü)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="86aef-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="86aef-120">Yanlış yazılmış Yöntem, yanlış Yöntem imzası veya yanlış hub adı</span><span class="sxs-lookup"><span data-stu-id="86aef-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="86aef-121">Çağrılan bir yöntemin adı veya imzası, istemcide uygun bir yöntemle tam olarak eşleşmiyorsa, çağrı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="86aef-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="86aef-122">Sunucu tarafından çağrılan yöntem adının istemcideki yöntemin adıyla eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="86aef-123">Ayrıca, SignalR, JavaScript 'e uygun olduğu gibi Camel-cased yöntemlerini kullanarak hub proxy 'sini oluşturur, bu nedenle sunucu üzerinde `SendMessage` adlı bir yöntem istemci proxy 'sinde `sendMessage` çağırılır.</span><span class="sxs-lookup"><span data-stu-id="86aef-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="86aef-124">Sunucu tarafı kodunuzda `HubName` özniteliğini kullanıyorsanız, kullanılan adın istemcide hub oluşturmak için kullanılan adla eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="86aef-125">`HubName` özniteliğini kullanmazsanız, bir JavaScript istemcisindeki hub 'ın adının ChatHub yerine chatHub gibi bir Camel-cased olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="86aef-126">İstemcide yinelenen Yöntem adı</span><span class="sxs-lookup"><span data-stu-id="86aef-126">Duplicate method name on client</span></span>

<span data-ttu-id="86aef-127">İstemcide yalnızca büyük/küçük harfe göre farklılık gösteren bir yinelenen Yöntem olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="86aef-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="86aef-128">İstemci uygulamanızın `sendMessage`adlı bir yöntemi varsa, ayrıca `SendMessage` adlı bir yöntemin de olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="86aef-129">İstemcide eksik JSON ayrıştırıcısı</span><span class="sxs-lookup"><span data-stu-id="86aef-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="86aef-130">SignalR, sunucu ile istemci arasındaki çağrıları seri hale getirmek için bir JSON ayrıştırıcısı bulunmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="86aef-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="86aef-131">İstemcinizin yerleşik bir JSON ayrıştırıcısı yoksa (Internet Explorer 7 gibi), uygulamanıza bir tane eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="86aef-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="86aef-132">JSON ayrıştırıcısı [buradan](http://nuget.org/packages/json2)indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86aef-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="86aef-133">Hub ve PersistentConnection söz dizimini karıştırma</span><span class="sxs-lookup"><span data-stu-id="86aef-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="86aef-134">SignalR iki iletişim modeli kullanır: hub 'Lar ve PersistentConnections.</span><span class="sxs-lookup"><span data-stu-id="86aef-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="86aef-135">Bu iki iletişim modelini çağırma söz dizimi, istemci kodunda farklıdır.</span><span class="sxs-lookup"><span data-stu-id="86aef-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="86aef-136">Sunucu kodunuzda bir hub eklediyseniz, tüm istemci kodunuzun uygun hub sözdizimini kullandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="86aef-137">**JavaScript istemcisinde bir PersistentConnection oluşturan JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="86aef-138">**Bir JavaScript istemcisinde hub proxy oluşturan JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="86aef-139">**C#bir yolu PersistentConnection ile eşleyen sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="86aef-140">**C#birden çok uygulamanız varsa, bir yolu hub 'a veya birden çok hub 'a eşleyen sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="86aef-141">Abonelikler eklenmeden önce bağlantı başlatıldı</span><span class="sxs-lookup"><span data-stu-id="86aef-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="86aef-142">Sunucudan çağrılabilecek Yöntemler proxy 'ye eklendikten sonra hub 'ın bağlantısı başlatılırsa, iletiler alınmaz.</span><span class="sxs-lookup"><span data-stu-id="86aef-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="86aef-143">Aşağıdaki JavaScript kodu hub 'ı düzgün olarak başlatmayacak:</span><span class="sxs-lookup"><span data-stu-id="86aef-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="86aef-144">**Hub iletilerinin alınmasına izin vermeyecek hatalı JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="86aef-145">Bunun yerine, Start çağrılmadan önce Yöntem aboneliklerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="86aef-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="86aef-146">**Bir hub 'a abonelikleri doğru şekilde ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="86aef-147">Hub proxy 'sinde eksik Yöntem adı</span><span class="sxs-lookup"><span data-stu-id="86aef-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="86aef-148">Sunucuda tanımlanan yöntemin istemcide abone olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="86aef-149">Sunucu, yöntemi tanımlasa da, istemci proxy 'sine yine de eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="86aef-150">Yöntemler istemci proxy 'sine aşağıdaki yollarla eklenebilir (metodun doğrudan hub değil, hub 'ın `client` üyesine eklendiğini unutmayın):</span><span class="sxs-lookup"><span data-stu-id="86aef-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="86aef-151">**Bir hub proxy 'sine yöntemler ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="86aef-152">Hub veya hub yöntemleri ortak olarak bildirilmemiş</span><span class="sxs-lookup"><span data-stu-id="86aef-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="86aef-153">İstemcide görünür olması için, hub uygulamasının ve yöntemlerinin `public`olarak bildirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="86aef-154">Farklı bir uygulamadan hub 'a erişme</span><span class="sxs-lookup"><span data-stu-id="86aef-154">Accessing hub from a different application</span></span>

<span data-ttu-id="86aef-155">SignalR hub 'Larına yalnızca SignalR istemcileri uygulayan uygulamalar üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="86aef-156">SignalR diğer iletişim kitaplıklarıyla (SOAP veya WCF Web Hizmetleri gibi) birlikte çalışamaz.) Hedef platformunuz için uygun bir SignalR istemcisi yoksa, sunucunun uç noktasına doğrudan erişemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="86aef-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="86aef-157">Verileri el ile serileştirme</span><span class="sxs-lookup"><span data-stu-id="86aef-157">Manually serializing data</span></span>

<span data-ttu-id="86aef-158">SignalR, yöntem parametrelerinizi seri hale getirmek için otomatik olarak JSON kullanır; bunu yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="86aef-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="86aef-159">Uzak hub yöntemi, OnConnected işlevindeki istemcide yürütülmedi</span><span class="sxs-lookup"><span data-stu-id="86aef-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="86aef-160">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-160">This behavior is by design.</span></span> <span data-ttu-id="86aef-161">`OnDisconnected` çağrıldığında, hub, daha fazla hub yönteminin çağrılmasına izin verilmeyen `Disconnected` durumuna zaten girdi.</span><span class="sxs-lookup"><span data-stu-id="86aef-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="86aef-162">**C#Onbağlantısız olayda kodu doğru şekilde yürüten sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="86aef-163">Bağlantı sınırına ulaşıldı</span><span class="sxs-lookup"><span data-stu-id="86aef-163">Connection limit reached</span></span>

<span data-ttu-id="86aef-164">Windows 7 gibi bir istemci işletim sisteminde IIS 'nin tam sürümünü kullanırken, 10 bağlantı sınırı uygulanır.</span><span class="sxs-lookup"><span data-stu-id="86aef-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="86aef-165">İstemci işletim sistemi kullanırken, bu sınırı önlemek için IIS Express kullanın.</span><span class="sxs-lookup"><span data-stu-id="86aef-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="86aef-166">Etki alanları arası bağlantı düzgün ayarlanmadı</span><span class="sxs-lookup"><span data-stu-id="86aef-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="86aef-167">Bir etki alanı bağlantısı (SignalR URL 'SI barındırma sayfasıyla aynı etki alanında olmayan bir bağlantı) doğru ayarlanmamışsa, bağlantı hata iletisi olmadan başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="86aef-168">Etki alanları arası iletişimin nasıl etkinleştirileceği hakkında bilgi için bkz. [etki alanları arası bağlantı oluşturma](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="86aef-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="86aef-169">NTLM (Active Directory) kullanılarak bağlantı .NET istemcisinde çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="86aef-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="86aef-170">Bağlantı düzgün yapılandırılmamışsa, bir .NET istemci uygulamasındaki bağlantı etki alanı güvenliği kullanan bir bağlantı başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="86aef-171">Bir etki alanı ortamında SignalR kullanmak için, önkoşul bağlantısı özelliğini aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="86aef-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="86aef-172">**C#bağlantı kimlik bilgilerini uygulayan istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="86aef-173">Diğer bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="86aef-173">Other connection issues</span></span>

<span data-ttu-id="86aef-174">Bu bölümde, bir bağlantı sırasında oluşan belirli belirtilerin veya hata iletilerinin nedenleri ve çözümleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="86aef-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="86aef-175">"Verilerin gönderilebilmesi için önce başlangıç çağrılmalıdır" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="86aef-176">Bu hata genellikle, kod, bağlantı başlatılmadan önce SignalR nesnelerine başvuruyorsa görülür.</span><span class="sxs-lookup"><span data-stu-id="86aef-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="86aef-177">İşleyiciler için kablolanın ve sunucu üzerinde tanımlanan yöntemleri çağıran LIKE bağlantısı, bağlantı tamamlandıktan sonra eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="86aef-178">`Start` çağrısının zaman uyumsuz olduğunu unutmayın, bu nedenle çağrıdan sonra kod, tamamlanmadan önce yürütülür.</span><span class="sxs-lookup"><span data-stu-id="86aef-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="86aef-179">Bir bağlantının tamamen başlatıldıktan sonra işleyiciler eklemenin en iyi yolu, bunları başlangıç yöntemine parametre olarak geçirilen bir geri çağırma işlevine koymasıdır:</span><span class="sxs-lookup"><span data-stu-id="86aef-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="86aef-180">**SignalR nesnelerine başvuran olay işleyicilerini doğru şekilde ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="86aef-181">Bu hata, SignalR nesnelerine hala başvurulurken bir bağlantı durdurulduğunda da görülür.</span><span class="sxs-lookup"><span data-stu-id="86aef-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="86aef-182">"301 kalıcı olarak taşındı" veya "302 geçici olarak taşındı" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="86aef-183">Bu hata, proje SignalR adlı bir klasör içeriyorsa, otomatik olarak oluşturulan ara sunucu ile müdahale edecek şekilde görülebilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="86aef-184">Bu hatayı önlemek için, uygulamanızda `SignalR` adlı bir klasör kullanmayın veya otomatik proxy oluşturmayı kapatın.</span><span class="sxs-lookup"><span data-stu-id="86aef-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="86aef-185">Daha fazla ayrıntı için [oluşturulan ara sunucuya ve ne işe yönelik](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) olarak bakın.</span><span class="sxs-lookup"><span data-stu-id="86aef-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="86aef-186">.NET veya Silverlight istemcisinde "403 Yasak" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="86aef-187">Bu hata, etki alanları arası iletişimin düzgün şekilde etkinleştirilmediği etki alanı ortamlarında oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="86aef-188">Etki alanları arası iletişimin nasıl etkinleştirileceği hakkında bilgi için bkz. [etki alanları arası bağlantı oluşturma](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="86aef-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="86aef-189">Bir Silverlight istemcisinde etki alanları arası bağlantı kurmak için bkz. [Silverlight istemcilerinden etki alanları arası bağlantılar](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span><span class="sxs-lookup"><span data-stu-id="86aef-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="86aef-190">"404 bulunamadı" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-190">"404 Not Found" error</span></span>

<span data-ttu-id="86aef-191">Bu sorunun çeşitli nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="86aef-191">There are several causes for this issue.</span></span> <span data-ttu-id="86aef-192">Aşağıdakilerin tümünü doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="86aef-192">Verify all of the following:</span></span>

- <span data-ttu-id="86aef-193">**Hub proxy adresi başvurusu doğru biçimlendirilmedi:** Bu hata genellikle oluşturulan Merkez ara sunucu adresinin başvurusu doğru biçimlendirilmediyse görülür.</span><span class="sxs-lookup"><span data-stu-id="86aef-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="86aef-194">Hub adresi başvurusunun düzgün şekilde yapıldığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="86aef-195">Ayrıntılar için [dinamik olarak oluşturulan ara sunucuya nasıl başvurulacağını](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="86aef-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="86aef-196">**Hub yolunu eklemeden önce uygulamaya rotalar ekleniyor:** Uygulamanız başka rotalar kullanıyorsa, eklenen ilk yolun `MapHubs`çağrısı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="86aef-197">"500 iç sunucu hatası"</span><span class="sxs-lookup"><span data-stu-id="86aef-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="86aef-198">Bu, çok çeşitli nedenleri olabilecek çok sayıda genel hatadır.</span><span class="sxs-lookup"><span data-stu-id="86aef-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="86aef-199">Hatanın ayrıntıları sunucunun olay günlüğünde görünmelidir veya sunucu hata ayıklaması aracılığıyla bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="86aef-200">Daha ayrıntılı hata bilgileri, sunucuda ayrıntılı hataları etkinleştirerek elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="86aef-201">Daha fazla bilgi için bkz. [hub sınıfında hataları işleme](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span><span class="sxs-lookup"><span data-stu-id="86aef-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="86aef-202">"TypeError: &lt;hubType&gt; tanımsız" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="86aef-203">`MapHubs` çağrısı düzgün şekilde yapılmazlarsa bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="86aef-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="86aef-204">Daha fazla bilgi için bkz. [SignalR rotasını kaydetme ve SignalR seçeneklerini yapılandırma](../guide-to-the-api/hubs-api-guide-server.md#route) .</span><span class="sxs-lookup"><span data-stu-id="86aef-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="86aef-205">JsonSerializationException Kullanıcı kodu tarafından işlenmedi</span><span class="sxs-lookup"><span data-stu-id="86aef-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="86aef-206">Yöntemlerinizi göndereceğiniz parametrelerin serileştirilebilir olmayan türler (Dosya tutamaçları veya veritabanı bağlantıları gibi) içermediği doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="86aef-207">İstemciye gönderilmesini istemediğiniz bir sunucu tarafı nesnesi üzerinde Üyeler kullanmanız gerekiyorsa (güvenlik veya serileştirme nedenleri için) `JSONIgnore` özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="86aef-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="86aef-208">"Protokol hatası: bilinmeyen aktarım" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="86aef-209">İstemci, SignalR 'nin kullandığı aktarımları desteklemiyorsa bu hata ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="86aef-210">SignalR ile hangi tarayıcıların kullanılabileceği hakkında bilgi için bkz. [taşıma ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports) .</span><span class="sxs-lookup"><span data-stu-id="86aef-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="86aef-211">"JavaScript hub ara sunucusu oluşturma devre dışı bırakıldı."</span><span class="sxs-lookup"><span data-stu-id="86aef-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="86aef-212">Bu hata, `signalr/hubs`konumundaki dinamik olarak oluşturulan ara sunucuya bir başvuru da dahil olmak üzere `DisableJavaScriptProxies` ayarlandıysa oluşur.</span><span class="sxs-lookup"><span data-stu-id="86aef-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="86aef-213">Proxy 'yi el ile oluşturma hakkında daha fazla bilgi için bkz. [oluşturulan ara sunucu ve sizin için ne yapar](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="86aef-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="86aef-214">"Bağlantı KIMLIĞI yanlış biçimde" veya "etkin bir SignalR bağlantısı sırasında Kullanıcı kimliği değiştirilemiyor" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="86aef-215">Kimlik doğrulaması kullanılıyorsa ve bağlantı durdurulmadan önce istemci günlüğe kaydedildiğinde bu hata görünebilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="86aef-216">Çözüm, istemciyi günlüğe kaydetmeden önce SignalR bağlantısını durdurmaktır.</span><span class="sxs-lookup"><span data-stu-id="86aef-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="86aef-217">"Yakalanamayan hata: SignalR: jQuery bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="86aef-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="86aef-218">Lütfen SignalR. JS dosyasından önce jQuery 'e başvurulduğundan emin olun "hata</span><span class="sxs-lookup"><span data-stu-id="86aef-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="86aef-219">SignalR JavaScript istemcisi jQuery 'yi çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="86aef-220">JQuery başvurusunun doğru olduğunu, kullanılan yolun geçerli olduğunu ve jQuery 'e başvurunun SignalR başvurusundan önce olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="86aef-221">"Yakalanamayan TypeError: '&lt;özelliği&gt;' tanımsız" hatası okunamıyor</span><span class="sxs-lookup"><span data-stu-id="86aef-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="86aef-222">Bu hata, jQuery veya hub proxy 'sinin düzgün şekilde başvurulmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86aef-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="86aef-223">JQuery ve hub proxy 'sine yönelik başvurunun doğru olduğunu, kullanılan yolun geçerli olduğunu ve jQuery 'e başvurunun, hub proxy 'sine yönelik başvurudan önce olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="86aef-224">Hub proxy 'sine yönelik varsayılan başvuru aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="86aef-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="86aef-225">**Hub proxy 'sine doğru şekilde başvuran HTML istemci tarafı kodu**</span><span class="sxs-lookup"><span data-stu-id="86aef-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="86aef-226">"RuntimeBinderException Kullanıcı kodu tarafından işlenmemiş" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="86aef-227">Yanlış `Hub.On` aşırı yüklemesi kullanıldığında bu hata ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="86aef-228">Yöntemin bir dönüş değeri varsa, dönüş türü genel bir tür parametresi olarak belirtilmelidir:</span><span class="sxs-lookup"><span data-stu-id="86aef-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="86aef-229">**İstemci üzerinde tanımlanan Yöntem (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="86aef-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="86aef-230">Bağlantı KIMLIĞI tutarsız veya sayfa yükleri arasındaki bağlantı sonları</span><span class="sxs-lookup"><span data-stu-id="86aef-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="86aef-231">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-231">This behavior is by design.</span></span> <span data-ttu-id="86aef-232">Hub nesnesi sayfa nesnesinde barındırıldığından, sayfa yenilendiğinde hub yok edilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="86aef-233">Çok sayfalı bir uygulamanın, sayfa yüklemeleri arasında tutarlı olmaları için kullanıcılar ve bağlantı kimlikleri arasındaki ilişkilendirmeyi koruması gerekir.</span><span class="sxs-lookup"><span data-stu-id="86aef-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="86aef-234">Bağlantı kimlikleri sunucuda `ConcurrentDictionary` nesne veya veritabanında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="86aef-235">"Değer null olamaz" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-235">"Value cannot be null" error</span></span>

<span data-ttu-id="86aef-236">İsteğe bağlı parametrelere sahip sunucu tarafı yöntemleri şu anda desteklenmiyor; isteğe bağlı parametre atlanırsa, yöntemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="86aef-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="86aef-237">Daha fazla bilgi için bkz. [Isteğe bağlı parametreler](https://github.com/SignalR/SignalR/issues/324).</span><span class="sxs-lookup"><span data-stu-id="86aef-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="86aef-238">"Firefox hata&gt;&lt;adresi" sunucu ile bağlantı kuramıyor "</span><span class="sxs-lookup"><span data-stu-id="86aef-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="86aef-239">WebSocket aktarımının anlaşması başarısız olursa ve bunun yerine başka bir aktarım kullanılıyorsa, bu hata iletisi Firebug 'da görülebilir.</span><span class="sxs-lookup"><span data-stu-id="86aef-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="86aef-240">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="86aef-241">"Uzak sertifika, .NET istemci uygulamasındaki doğrulama yordamına göre geçersiz" hatası</span><span class="sxs-lookup"><span data-stu-id="86aef-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="86aef-242">Sunucunuz için özel istemci sertifikaları gerekiyorsa, istek yapılmadan önce bağlantı için bir X509Certificate ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86aef-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="86aef-243">`Connection.AddClientCertificate`kullanarak sertifikayı bağlantıya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="86aef-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="86aef-244">Kimlik doğrulama zaman aşımına uğraydıktan sonra bağlantı düşer</span><span class="sxs-lookup"><span data-stu-id="86aef-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="86aef-245">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-245">This behavior is by design.</span></span> <span data-ttu-id="86aef-246">Bağlantı etkin durumdayken kimlik doğrulama bilgileri değiştirilemez; kimlik bilgilerini yenilemek için bağlantı durdurulmalıdır ve yeniden başlatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86aef-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="86aef-247">JQuery Mobile kullanılırken OnConnected iki kez çağırılır</span><span class="sxs-lookup"><span data-stu-id="86aef-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="86aef-248">jQuery Mobile 'ın `initializePage` işlevi, her sayfadaki betikleri yeniden yürütülmesine zorlar ve bu nedenle ikinci bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86aef-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="86aef-249">Bu soruna yönelik çözümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="86aef-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="86aef-250">JavaScript dosyanızı önce jQuery Mobile başvurusunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="86aef-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="86aef-251">`$.mobile.autoInitializePage = false`ayarlayarak `initializePage` işlevini devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="86aef-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="86aef-252">Bağlantıyı başlatmadan önce sayfanın başlatılmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="86aef-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="86aef-253">İletiler, gönderilen sunucu olayları kullanılarak Silverlight uygulamalarında gecikiyor</span><span class="sxs-lookup"><span data-stu-id="86aef-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="86aef-254">Silverlight üzerinde sunucu gönderme olayları kullanılırken iletiler gecikir.</span><span class="sxs-lookup"><span data-stu-id="86aef-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="86aef-255">Bunun yerine uzun yoklama kullanılmasına zorlamak için, bağlantıyı başlatırken aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="86aef-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="86aef-256">Süresiz çerçeve protokolü kullanılarak "izin reddedildi"</span><span class="sxs-lookup"><span data-stu-id="86aef-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="86aef-257">Bu bilinen bir sorundur ve [burada](https://github.com/SignalR/SignalR/issues/1963)açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="86aef-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="86aef-258">Bu belirti, en son JQuery kitaplığı kullanılarak görülebilir; geçici çözüm, uygulamanızın JQuery 1.8.2 sürümüne indirgenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="86aef-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="86aef-259">Derleme ve sunucu tarafı hataları</span><span class="sxs-lookup"><span data-stu-id="86aef-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="86aef-260">Aşağıdaki bölümde, derleyici ve sunucu tarafı çalışma zamanı hatalarına yönelik olası çözümler yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="86aef-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="86aef-261">Hub örneğine başvuru null</span><span class="sxs-lookup"><span data-stu-id="86aef-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="86aef-262">Her bağlantı için bir hub örneği oluşturulduğundan, kodunuzda bir hub örneği oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="86aef-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="86aef-263">Hub 'ın dışında bir hub 'daki yöntemleri çağırmak için, hub bağlamına bir başvuru elde etmek üzere bkz. [istemci yöntemlerini çağırma ve hub sınıfı dışından grupları yönetme](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) .</span><span class="sxs-lookup"><span data-stu-id="86aef-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="86aef-264">HTTPContext. Current. Session null</span><span class="sxs-lookup"><span data-stu-id="86aef-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="86aef-265">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-265">This behavior is by design.</span></span> <span data-ttu-id="86aef-266">SignalR, oturum durumunu etkinleştirmek çift yönlü mesajlaşmayı bozduğundan, ASP.NET oturum durumunu desteklemez.</span><span class="sxs-lookup"><span data-stu-id="86aef-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="86aef-267">Geçersiz kılınacak uygun yöntem yok</span><span class="sxs-lookup"><span data-stu-id="86aef-267">No suitable method to override</span></span>

<span data-ttu-id="86aef-268">Eski belgelerden veya bloglardan kod kullanıyorsanız bu hatayı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86aef-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="86aef-269">Değiştirilmiş veya kullanım dışı olan yöntemlerin adlarına başvurduğunuzdan emin olun (`OnConnectedAsync`gibi).</span><span class="sxs-lookup"><span data-stu-id="86aef-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="86aef-270">Hostcontexwesions. WebSocketServerUrl null</span><span class="sxs-lookup"><span data-stu-id="86aef-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="86aef-271">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-271">This behavior is by design.</span></span> <span data-ttu-id="86aef-272">Bu üye kullanımdan kaldırılmıştır ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="86aef-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="86aef-273">"' SignalR. hub ' adlı bir yol zaten yol koleksiyonunda" hata</span><span class="sxs-lookup"><span data-stu-id="86aef-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="86aef-274">Bu hata, uygulamanız tarafından `MapHubs` iki kez çağrılırsa görülür.</span><span class="sxs-lookup"><span data-stu-id="86aef-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="86aef-275">Bazı örnek uygulamalar doğrudan genel uygulama dosyasında `MapHubs` çağırır; diğer bir deyişle, çağrı bir sarmalayıcı sınıfında yapılır.</span><span class="sxs-lookup"><span data-stu-id="86aef-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="86aef-276">Uygulamanızın her ikisini de yapamadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="86aef-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="86aef-277">Visual Studio sorunları</span><span class="sxs-lookup"><span data-stu-id="86aef-277">Visual Studio issues</span></span>

<span data-ttu-id="86aef-278">Bu bölümde, Visual Studio 'da karşılaşılan sorunlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="86aef-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="86aef-279">Betik belgeleri düğümü Çözüm Gezgini görünmüyor</span><span class="sxs-lookup"><span data-stu-id="86aef-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="86aef-280">Öğreticilerimizden bazıları hata ayıklama sırasında Çözüm Gezgini ' deki "betik belgeleri" düğümüne yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="86aef-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="86aef-281">Bu düğüm JavaScript hata ayıklayıcısı tarafından üretilir ve yalnızca Internet Explorer 'da tarayıcı istemcilerinde hata ayıklanırken görüntülenir; Chrome veya Firefox kullanılıyorsa düğüm görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="86aef-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="86aef-282">JavaScript hata ayıklayıcı, Silverlight hata ayıklayıcısı gibi başka bir istemci hata ayıklayıcısı çalışıyorsa de çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="86aef-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="86aef-283">SignalR, Visual Studio 2008 veya önceki sürümlerde çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="86aef-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="86aef-284">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="86aef-284">This behavior is by design.</span></span> <span data-ttu-id="86aef-285">SignalR için .NET Framework 4 veya üzeri gerekir; Bu, SignalR uygulamalarının Visual Studio 2010 veya sonraki sürümlerde geliştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86aef-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="86aef-286">IIS sorunları</span><span class="sxs-lookup"><span data-stu-id="86aef-286">IIS issues</span></span>

<span data-ttu-id="86aef-287">Bu bölüm Internet Information Services sorunları içerir.</span><span class="sxs-lookup"><span data-stu-id="86aef-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="86aef-288">MapHubs çağrısından sonra Web sitesi kilitleniyor</span><span class="sxs-lookup"><span data-stu-id="86aef-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="86aef-289">Bu sorun, SignalR 'nin en son sürümünde düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="86aef-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="86aef-290">Yüklemenizi NuGet kullanarak güncelleştirerek, SignalR 'nin en son yayınlanan sürümünü kullandığınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="86aef-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="86aef-291">Azure sorunları</span><span class="sxs-lookup"><span data-stu-id="86aef-291">Azure issues</span></span>

<span data-ttu-id="86aef-292">Bu bölüm Microsoft Azure sorunları içerir.</span><span class="sxs-lookup"><span data-stu-id="86aef-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="86aef-293">Konu adları değiştirildikten sonra iletiler Azure arkadüzleminden alınmaz</span><span class="sxs-lookup"><span data-stu-id="86aef-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="86aef-294">Azure arkadüzlemi tarafından kullanılan konuların Kullanıcı tarafından yapılandırılabilir olması amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="86aef-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
