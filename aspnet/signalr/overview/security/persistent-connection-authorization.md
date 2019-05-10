---
uid: signalr/overview/security/persistent-connection-authorization
title: Kimlik doğrulama ve yetkilendirme kalıcı SignalR bağlantıları için | Microsoft Docs
author: bradygaster
description: Bu konu, kalıcı bir bağlantı üzerinde Yetkilendirme zorlamak açıklar. Bir SignalR uygulamasına güvenlik tümleştirme hakkında genel bilgi...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65113535"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="32605-104">Kalıcı SignalR Bağlantıları için Kimlik Doğrulaması ve Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="32605-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="32605-105">tarafından [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="32605-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="32605-106">Bu konu, kalıcı bir bağlantı üzerinde Yetkilendirme zorlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="32605-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="32605-107">Bir SignalR uygulamasına güvenlik tümleştirme hakkında genel bilgi için bkz. [güvenliğine giriş](introduction-to-security.md).</span><span class="sxs-lookup"><span data-stu-id="32605-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="32605-108">Bu konu başlığında kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="32605-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="32605-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="32605-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="32605-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="32605-110">.NET 4.5</span></span>
> - <span data-ttu-id="32605-111">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="32605-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="32605-112">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="32605-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="32605-113">SignalR eski sürümleri hakkında daha fazla bilgi için bkz: [SignalR eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="32605-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="32605-114">Sorularınız ve yorumlarınız</span><span class="sxs-lookup"><span data-stu-id="32605-114">Questions and comments</span></span>
>
> <span data-ttu-id="32605-115">Lütfen bu öğreticide sevmediğinizi nasıl ve ne sayfanın alt kısmındaki açıklamalarda geliştirebileceğimiz hakkında geri bildirim bırakın.</span><span class="sxs-lookup"><span data-stu-id="32605-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="32605-116">Öğretici için doğrudan ilgili olmayan sorularınız varsa, bunları gönderebilir [ASP.NET SignalR Forumu](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="32605-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="32605-117">Yetkilendirme zorla</span><span class="sxs-lookup"><span data-stu-id="32605-117">Enforce authorization</span></span>

<span data-ttu-id="32605-118">Kullanırken yetkilendirme kurallarını zorunlu tutmak için bir [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) geçersiz kılmanız gerekir `AuthorizeRequest` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="32605-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="32605-119">Kullanamazsınız `Authorize` özniteliği ile kalıcı bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="32605-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="32605-120">`AuthorizeRequest` Yöntemi, kullanıcının istenen eylemi gerçekleştirmek için yetkili olup olmadığını doğrulamak için her istek öncesinde SignalR Framework tarafından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="32605-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="32605-121">`AuthorizeRequest` Yöntemi istemci tarafından çağrılmaz; bunun yerine, uygulamanızın standart kimlik doğrulama mekanizması kullanıcının kimliğini.</span><span class="sxs-lookup"><span data-stu-id="32605-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="32605-122">Aşağıdaki örnekte, istekleri kimlik doğrulaması yapılan kullanıcılara sınırlamak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="32605-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="32605-123">Tüm özelleştirilmiş yetkilendirme mantığının AuthorizeRequest yöntemi ekleyebilirsiniz; gibi bir kullanıcının belirli bir role ait olup olmadığı denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="32605-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
