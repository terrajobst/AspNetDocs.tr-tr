---
uid: signalr/overview/security/persistent-connection-authorization
title: SignalR kalıcı bağlantıları için kimlik doğrulaması ve yetkilendirme | Microsoft Docs
author: bradygaster
description: Bu konu, kalıcı bir bağlantıda yetkilendirmeyi nasıl zorlayabileceğinizi açıklamaktadır. Güvenliği bir SignalR uygulamasıyla tümleştirme hakkında genel bilgi için,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578878"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="72e40-104">Kalıcı SignalR Bağlantıları için Kimlik Doğrulaması ve Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="72e40-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="72e40-105">, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="72e40-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="72e40-106">Bu konu, kalıcı bir bağlantıda yetkilendirmeyi nasıl zorlayabileceğinizi açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="72e40-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="72e40-107">Güvenliği bir SignalR uygulamasıyla tümleştirme hakkında genel bilgi için bkz. [güvenliğe giriş](introduction-to-security.md).</span><span class="sxs-lookup"><span data-stu-id="72e40-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="72e40-108">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="72e40-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="72e40-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="72e40-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="72e40-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="72e40-110">.NET 4.5</span></span>
> - <span data-ttu-id="72e40-111">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="72e40-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="72e40-112">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="72e40-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="72e40-113">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="72e40-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="72e40-114">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="72e40-114">Questions and comments</span></span>
>
> <span data-ttu-id="72e40-115">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="72e40-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="72e40-116">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72e40-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="72e40-117">Yetkilendirmeyi zorla</span><span class="sxs-lookup"><span data-stu-id="72e40-117">Enforce authorization</span></span>

<span data-ttu-id="72e40-118">Bir [Persistentconnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) kullanırken yetkilendirme kurallarını zorlamak için `AuthorizeRequest` yöntemini geçersiz kılmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72e40-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="72e40-119">`Authorize` özniteliğini kalıcı bağlantılarla kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="72e40-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="72e40-120">`AuthorizeRequest` yöntemi, kullanıcının istenen eylemi gerçekleştirme yetkisine sahip olduğunu doğrulamak için her istekten önce SignalR çerçevesi tarafından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="72e40-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="72e40-121">`AuthorizeRequest` yöntemi istemciden çağrılmaz; Bunun yerine, uygulamanızın standart kimlik doğrulama mekanizmasıyla kullanıcının kimliğini doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72e40-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="72e40-122">Aşağıdaki örnekte isteklerin kimliği doğrulanmış kullanıcılarla nasıl sınırlandıralınacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="72e40-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="72e40-123">AuthorizeRequest yönteminde özelleştirilmiş herhangi bir yetkilendirme mantığını ekleyebilirsiniz; Örneğin, bir kullanıcının belirli bir role ait olup olmadığını denetleme.</span><span class="sxs-lookup"><span data-stu-id="72e40-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
