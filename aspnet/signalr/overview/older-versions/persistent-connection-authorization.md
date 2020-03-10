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
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>Kalıcı SignalR Bağlantıları için Kimlik Doğrulaması ve Yetkilendirme (SignalR 1.x)

, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konu, kalıcı bir bağlantıda yetkilendirmeyi nasıl zorlayabileceğinizi açıklamaktadır. Güvenliği bir SignalR uygulamasıyla tümleştirme hakkında genel bilgi için bkz. [güvenliğe giriş](index.md).

## <a name="enforce-authorization"></a>Yetkilendirmeyi zorla

Bir [Persistentconnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) kullanırken yetkilendirme kurallarını zorlamak için `AuthorizeRequest` yöntemini geçersiz kılmanız gerekir. `Authorize` özniteliğini kalıcı bağlantılarla kullanamazsınız. `AuthorizeRequest` yöntemi, kullanıcının istenen eylemi gerçekleştirme yetkisine sahip olduğunu doğrulamak için her istekten önce SignalR çerçevesi tarafından çağırılır. `AuthorizeRequest` yöntemi istemciden çağrılmaz; Bunun yerine, uygulamanızın standart kimlik doğrulama mekanizmasıyla kullanıcının kimliğini doğrulamanız gerekir.

Aşağıdaki örnekte isteklerin kimliği doğrulanmış kullanıcılarla nasıl sınırlandıralınacağını gösterilmektedir.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

AuthorizeRequest yönteminde özelleştirilmiş herhangi bir yetkilendirme mantığını ekleyebilirsiniz; Örneğin, bir kullanıcının belirli bir role ait olup olmadığını denetleme.
