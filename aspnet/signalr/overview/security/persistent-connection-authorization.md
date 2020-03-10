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
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a>Kalıcı SignalR Bağlantıları için Kimlik Doğrulaması ve Yetkilendirme

, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konu, kalıcı bir bağlantıda yetkilendirmeyi nasıl zorlayabileceğinizi açıklamaktadır. Güvenliği bir SignalR uygulamasıyla tümleştirme hakkında genel bilgi için bkz. [güvenliğe giriş](introduction-to-security.md).
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Bu konunun önceki sürümleri
>
> SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
>
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

## <a name="enforce-authorization"></a>Yetkilendirmeyi zorla

Bir [Persistentconnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) kullanırken yetkilendirme kurallarını zorlamak için `AuthorizeRequest` yöntemini geçersiz kılmanız gerekir. `Authorize` özniteliğini kalıcı bağlantılarla kullanamazsınız. `AuthorizeRequest` yöntemi, kullanıcının istenen eylemi gerçekleştirme yetkisine sahip olduğunu doğrulamak için her istekten önce SignalR çerçevesi tarafından çağırılır. `AuthorizeRequest` yöntemi istemciden çağrılmaz; Bunun yerine, uygulamanızın standart kimlik doğrulama mekanizmasıyla kullanıcının kimliğini doğrulamanız gerekir.

Aşağıdaki örnekte isteklerin kimliği doğrulanmış kullanıcılarla nasıl sınırlandıralınacağını gösterilmektedir.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

AuthorizeRequest yönteminde özelleştirilmiş herhangi bir yetkilendirme mantığını ekleyebilirsiniz; Örneğin, bir kullanıcının belirli bir role ait olup olmadığını denetleme.
