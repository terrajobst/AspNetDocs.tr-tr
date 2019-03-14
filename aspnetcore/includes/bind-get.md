---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074238"
---
> [!WARNING]
> Güvenlik nedenleriyle, bağlama kabul gerekir `GET` sayfa modeli özellikleri veri isteği. Özellikleri için eşleme önce kullanıcı girişi doğrulayın. İçin kabul `GET` bağlama, sorgu dizesi veya rota değerlerini senaryolarda belirtirken yararlıdır.
>
> Bir özelliği bağlamak `GET` istekleri, ayarlar [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) özniteliğin `SupportsGet` özelliğini `true`: `[BindProperty(SupportsGet = true)]`
