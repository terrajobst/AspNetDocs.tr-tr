---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: Kimlik doğrulama ve kalıcı SignalR bağlantıları için yetkilendirme (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: Bu konu, kalıcı bir bağlantı üzerinde Yetkilendirme zorlamak açıklar. Bir SignalR uygulamasına güvenlik tümleştirme hakkında genel bilgi...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: c4a2c9b4fa05e43ade98fb521c59f8645b43ffea
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069012"
---
<a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>Kalıcı SignalR Bağlantıları için Kimlik Doğrulaması ve Yetkilendirme (SignalR 1.x)
====================
tarafından [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konu, kalıcı bir bağlantı üzerinde Yetkilendirme zorlamak açıklar. Bir SignalR uygulamasına güvenlik tümleştirme hakkında genel bilgi için bkz. [güvenliğine giriş](index.md).


## <a name="enforce-authorization"></a>Yetkilendirme zorla

Kullanırken yetkilendirme kurallarını zorunlu tutmak için bir [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) geçersiz kılmanız gerekir `AuthorizeRequest` yöntemi. Kullanamazsınız `Authorize` özniteliği ile kalıcı bağlantılar. `AuthorizeRequest` Yöntemi, kullanıcının istenen eylemi gerçekleştirmek için yetkili olup olmadığını doğrulamak için her istek öncesinde SignalR Framework tarafından çağırılır. `AuthorizeRequest` Yöntemi istemci tarafından çağrılmaz; bunun yerine, uygulamanızın standart kimlik doğrulama mekanizması kullanıcının kimliğini.

Aşağıdaki örnekte, istekleri kimlik doğrulaması yapılan kullanıcılara sınırlamak gösterilmektedir.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

Tüm özelleştirilmiş yetkilendirme mantığının AuthorizeRequest yöntemi ekleyebilirsiniz; gibi bir kullanıcının belirli bir role ait olup olmadığı denetleniyor.
