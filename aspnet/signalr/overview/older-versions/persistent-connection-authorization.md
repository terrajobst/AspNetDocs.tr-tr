---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: SignalR kalıcı bağlantıları için kimlik doğrulaması ve yetkilendirme (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: Bu konu, kalıcı bir bağlantıda yetkilendirmeyi nasıl zorlayabileceğinizi açıklamaktadır. Güvenliği bir SignalR uygulamasıyla tümleştirme hakkında genel bilgi için,...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536542"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="6dd38-104">Kalıcı SignalR Bağlantıları için Kimlik Doğrulaması ve Yetkilendirme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="6dd38-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>

<span data-ttu-id="6dd38-105">, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6dd38-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="6dd38-106">Bu konu, kalıcı bir bağlantıda yetkilendirmeyi nasıl zorlayabileceğinizi açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="6dd38-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="6dd38-107">Güvenliği bir SignalR uygulamasıyla tümleştirme hakkında genel bilgi için bkz. [güvenliğe giriş](index.md).</span><span class="sxs-lookup"><span data-stu-id="6dd38-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="6dd38-108">Yetkilendirmeyi zorla</span><span class="sxs-lookup"><span data-stu-id="6dd38-108">Enforce authorization</span></span>

<span data-ttu-id="6dd38-109">Bir [Persistentconnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) kullanırken yetkilendirme kurallarını zorlamak için `AuthorizeRequest` yöntemini geçersiz kılmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dd38-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="6dd38-110">`Authorize` özniteliğini kalıcı bağlantılarla kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="6dd38-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="6dd38-111">`AuthorizeRequest` yöntemi, kullanıcının istenen eylemi gerçekleştirme yetkisine sahip olduğunu doğrulamak için her istekten önce SignalR çerçevesi tarafından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="6dd38-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="6dd38-112">`AuthorizeRequest` yöntemi istemciden çağrılmaz; Bunun yerine, uygulamanızın standart kimlik doğrulama mekanizmasıyla kullanıcının kimliğini doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dd38-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="6dd38-113">Aşağıdaki örnekte isteklerin kimliği doğrulanmış kullanıcılarla nasıl sınırlandıralınacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6dd38-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="6dd38-114">AuthorizeRequest yönteminde özelleştirilmiş herhangi bir yetkilendirme mantığını ekleyebilirsiniz; Örneğin, bir kullanıcının belirli bir role ait olup olmadığını denetleme.</span><span class="sxs-lookup"><span data-stu-id="6dd38-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
